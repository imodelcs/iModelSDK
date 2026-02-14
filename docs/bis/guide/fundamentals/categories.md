# Categories

`Category` 是 `GeometricElement` 的一个属性，用于显示目的对其几何进行分类。也就是说，每个 GeometricElement 都在一个且仅一个 Category 中。此外，Categories 不是分层的，也就是说，不允许将 Category 定义为另一个 Category 的父级。

Category 的可见性（开/关）可以按视图控制。

Categories 类似于 DGN 中的 levels 和 DWG 中的 layers，作为几何分类构造。

Categories 类似于 RVT 中的 categories，作为启用几何部分可见性和样式控制的构造的父概念——即 SubCategory。

有关 BIS 中语义与几何分类的更多信息，请参阅 Classifying Elements。

## Category 类

有三个 Category 类，具有以下层次结构：

- `DefinitionElement`
  - `Category`（抽象）
    - `DrawingCategory`（具体且密封）
    - `SpatialCategory`（具体且密封）

`DrawingCategory` 用于通过 `GeometricElement2dIsInCategory`（具体且密封）关系对 `GeometricElement2d` 元素进行分类。`GeometricElement2dIsInCategory` 将每个 `GeometricElement2d` 与恰好 1 个 `DrawingCategory` 相关联。

`SpatialCategory` 用于通过 `GeometricElement3dIsInCategory`（具体且密封）关系对 `GeometricElement3d` 元素进行分类。`GeometricElement3dIsInCategory` 将每个 `GeometricElement3d` 与恰好 1 个 `SpatialCategory` 相关联。

请注意，Categories 对于不是 GeometricElements 子类的 Elements 不相关。

## SubCategories

`SubCategory` 是 `Category` 的细分。SubCategories 允许 GeometricElements 具有多个可以独立可见和样式化（颜色、线条样式、透明度等）的 Geometry 片段。

> 重要的是要理解 `SubCategory` 不是 `Category`（即 Categories 不嵌套）。GeometricElements 总是与 Category 相关联，而不是与 SubCategory 相关联。也就是说，说 `GeometricElement` "在" `SubCategory` 上是没有意义的。

`SubCategory` 总是细分单个 `Category`。此关系由 `CategoryOwnsSubCategories` 关系定义。每个 Category 都有一个称为默认 SubCategory 的 SubCategory。

SubCategories 类似于 DGN 中的 levels、DWG 中的 layers 和 RVT 中的 subcategories，作为直接参与几何可见性和样式化的构造。

Category 的示例是"Window"。"Window" Category 可能包含 SubCategories "Pane"、"Mullion" 和 "Hardware"。如果显示 Window Category，则可以显示"Pane" SubCategory，而可以关闭"Mullion" SubCategory。

注意：如果 GeometricElement 的 Category 关闭，则不显示该元素，句号。SubCategory 仅在元素的 Category 显示时相关。

## Category 和 SubCategory Rank

Categories 和 SubCategories 有一个称为 `Rank` 的属性，由以下枚举定义。它旨在捕获给定 Category 或 SubCategory 在什么级别被提出。应用程序可以依靠 `Rank` 属性来理解给定 Category 或 SubCategory 的目的（如果适用）。

```cpp
enum class Rank
{
  System = 0,      //!< 此 category 由系统预定义
  Domain = 1,      //!< 此 category 由 domain 定义。
  Application = 2, //!< 此 category 由应用程序定义。
  User = 3,        //!< 此 category 由用户定义。
};
```

## Category 和 SubCategory CodeValue

Category 和 SubCategory 名称来自其 `CodeValue`。

为了避免创建不可打印、对用户不可区分和/或无法导出到其他系统的名称，Category 和 SubCategory 名称中不允许使用以下字符：

```
<>\/."?*|,='&\n\t
```

## Category CodeScope

Category 是 DefinitionElement 的子类，因此必须在 DefinitionModels 中。按照约定，Categories 的 Codes 的作用域是其 DefinitionModel。

对于特定于学科或 Domain 的 Categories，创建一个 DefinitionModel 并将其用于您的 Categories。这允许每个 Domain 拥有唯一的 Categories 集合，即使它们的名称在 Domains 之间不一定唯一。

## SubCategory CodeScope

`SubCategory` 的 `CodeScope` 始终是其父 `Category`。也就是说，SubCategory CodeValues 仅在其 Category 内唯一。

## GeometryStreams 中的 SubCategory 引用

每个 `GeometricElement2d` 和 `GeometricElement3d` 都有一个 `Category`。它们还有一个定义 `Element` 几何的 `GeometryStream` 属性。在该 GeometryStream 中，可以对元素 Category 的 SubCategoryIds 进行 0..N 引用，以控制 GeometryStream 中条目的可见性和样式。任何引用不是元素 Category 的 SubCategory 的 SubCategoryId 都将被拒绝。

## 数据写入应用程序和 Categories

在 BIS repository 上同步外部数据或直接创作它的每个应用程序应将其 Categories 存储在其自己的 Editing Channel 上。这样每个应用程序都可以拥有自己的 Categories 集合，而不会有彼此名称冲突的风险。

应用程序应考虑 Standard BIS Domains 提出的 SpatialCategories（如果适用）。

## Categories 的标准化

Categories 最终由用户控制。用户可能有兴趣最终标准化 BIS repository 中使用的 Categories 和 Subcategories 列表，尤其是当其数据由不同应用程序创建时。Standard BIS Domains 以及 Applications 可能会向某些 GeometricElements 建议默认 Categories，以帮助实现该目标。

作为默认值提出的 Categories 可能对应于 Domain 中的一个或多个类（"Door"、"Pavement"、"Beam"等）。

每个 `GeometricElement` 子类不需要自己的默认 `Category`。两种常见的 Category 模式是：

1. Category 用于一个类及其所有后代类。
2. Category 用于一组具有某种概念相似性但不适合规则 1 的不相关类。

---

| 下一篇：Information Hierarchy
|:---
