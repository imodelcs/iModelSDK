# Physical Materials（物理材质）

## 简介

正确捕获 `PhysicalElement`（物理元素）的 `PhysicalMaterial`（物理材质）对于工程量统计（Quantity takeoffs）和材料估算非常重要。需要注意的是，在 BIS 中，`PhysicalMaterial` 的概念与 `RenderMaterial` 不同。前者定义了物理对象所构成的物质，而后者则捕获用于显示的材质渲染属性。

## Physical Material 类层次结构

物理材质在 BIS 中使用 `DefinitionElement` 的抽象子类 `PhysicalMaterial` 进行建模，该类定义在 *BisCore* schema 中。`bis:PhysicalMaterial` 的更具体子类定义在单独的核心层 `PhysicalMaterial` schema 中，涵盖了基础设施中使用的主要物理材质。它包括 `Aggregate`（骨料）、`Aluminum`（铝）、`Asphalt`（沥青）和 `Concrete`（混凝土）等密封子类。`PhysicalMaterial` schema 中包含的物理材质列表可能会随时间增长。

在某些情况下，特别是在转换遗留数据时，软件可能对物理材质了解不足，无法根据 `PhysicalMaterial` schema 提供的类进行分类。对于这些情况，核心层 `Generic` schema 包含一个 `generic:PhysicalMaterial` 类。

下面的类图展示了 `PhysicalMaterial` 类层次结构。有关所用约定的详细信息，请参阅类图约定（Class-diagram Conventions）。

![图1：Physical Material 类层次结构](https://www.itwinjs.org/media/physical-material-classes.png)

## Types 和 Elements 中的 Physical Materials

在 BIS 中，物理对象的物理材质主要通过其物理类型（physical type）来捕获。`bis:PhysicalType` 提供了一个 `PhysicalMaterial` 导航属性，可用于引用适用的 `bis:PhysicalMaterial` 具体实例。这样，任何引用给定 `bis:PhysicalType` 的 `bis:PhysicalElement` 都共享同一个 `bis:PhysicalMaterial` 实例。

对于特定 `bis:PhysicalElement` 实例由不同于其 `bis:PhysicalType` 所引用的物理材质制成的情况，`bis:PhysicalElement` 实例可以通过其自身的 `PhysicalMaterial` 导航属性进行覆盖。

下面的类图展示了 `PhysicalElement`、`PhysicalType` 和 `PhysicalMaterial` 之间的关系。有关所用约定的详细信息，请参阅类图约定（Class-diagram Conventions）。

![图2：Types 和 Elements 中的 Physical Materials](https://www.itwinjs.org/media/physical-material-type-element.png)

除物理视角（Physical）以外的建模视角可能也需要捕获物理材质信息。此类建模视角的每个具体实现可以选择以自己的方式引用 `PhysicalMaterial` 实例。下面的类图显示了来自 `StructuralAnalytical` 域（别名 `sa`）的示例。有关所用约定的详细信息，请参阅类图约定（Class-diagram Conventions）。

![图3：其他建模视角中的 Physical Materials](https://www.itwinjs.org/media/physical-material-analytical-type.png)

## 异质组件

由不同材料制成的部件组成的物理组件并不罕见。这种用例跨越多个学科，从复合墙和结构梁到刚性路面结构。上述 BIS 中的方法为每个 `PhysicalElement` 实例关联一个且仅一个 `PhysicalMaterial` 实例。因此，异质组件通过将 `PhysicalMaterial` 实例与被组装的部件而不是父组件相关联来处理。

下面的实例图显示了作为异质组件的组合梁示例。有关所用约定的详细信息，请参阅实例图约定（Instance-diagram Conventions）。

![图4：异质组件](https://www.itwinjs.org/media/heterogeneous-assemblies.png)

---

| 下一篇：Quantity takeoffs: Guidelines（工程量统计：指南）
|:---
