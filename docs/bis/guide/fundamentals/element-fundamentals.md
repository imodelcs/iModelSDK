# Element 基础

BIS `Element` 表示被建模的实体。例如：泵、梁、合同、公司、流程、需求、文档、人员等。

## BIS Element 属性

元素的属性在其 Schema 中定义。BIS 中的每个 Element 都继承自 `Element` 类。本节描述 Element 类的属性，因此也是 iModel 中每个 Element 都具有的属性。

### CodeSpec

参见 CodeSpec

### CodeScope

参见 CodeScope

### CodeValue

参见 CodeValue

### FederationGuid

参见 FederationGuids

### UserLabel

每个 BIS `Element` 都有一个可选的 `UserLabel` 属性，用于提供用户熟悉的别名。

UserLabel 可以在 GUI 中作为替代的"更友好"名称，例如，`CodeValue`="R-134" 的房间可能有 `UserLabel`="大厨房"或 `UserLabel`="约翰的办公室"。

对 `UserLabel` 没有唯一性约束。

除数据转换程序外，UserLabel 总是留给用户输入，而不是程序生成的。

### JsonProperties

`JsonProperties` 成员以 JSON 格式在 Element 上保存实例特定的临时数据。它是一个键值对字典，其中键是一个命名空间（见下文），值是一个 JSON 对象。通过这种方式，`JsonProperties` 成员可以在任何元素上保存任何形式和复杂度的外部定义（即 BIS 之外）的数据。

存储在 `JsonProperties` 成员中的临时数据被假定为 iModel 内部的，因此不会在通用 iTwin.js 控件和应用程序的用户界面中显示。

为了避免命名值时的冲突，`JsonProperties` 的顶级成员名称保留给命名空间。命名空间没有注册表，因此应选择足够长且唯一的名称以避免碰撞的可能性（至少 8 个字符）。

> 注意：所有 JSON 属性名称，以及命名空间，都是区分大小写的。

#### `UserProps` 命名空间

JsonProperties 中有一个保留的命名空间叫 `UserProps`。UserProps 中的所有值都应由用户添加，应用程序代码不应在此存储信息。用户应使用具有自己命名范围规则的名称存储其属性，例如大写前缀以避免冲突。但由于他们知道只有自己的内部数据保存在 UserProps 中，他们不需要担心与应用程序的冲突。

例如，一个 Element 可能具有以下 JsonProperties 集合：

```json
{
  "ABCConnector_props": {
    "conversionStatus": "incomplete",
    "lastConversionElapsedTime": "15.35"
  },
  "XYZConnector_props": {
    "conversionQualityScore": 100,
    "conversionDataCache": 22
  },
  "UserProps": {
    "BTTE_contractInfo": {
      "contractor": "Ace Manufacturing",
      "contractId": "1032SW3"
    },
    "BTTE_approvals": {
      "reviewers": ["Tom", "Justine", "Nate"],
      "date": "2018-02-11",
      "notes": ""
    }
  }
}
```

### JsonProperties 的优缺点

JSON 属性的最大优点是它们不需要任何 Schema 或前期工作。JSON 属性的缺点是：

- 无类型安全。没有任何机制可以控制为任何属性名存储的内容。
- 无必需数据。没有任何机制可以定义某些属性必须被定义的要求。
- 存储在 `JsonProperties` 成员中的数据不会在通用 iTwin.js 控件和应用程序的用户界面中显示。

### JsonProperties 与 ECSQL

可以使用常规 json_XXX 函数通过 ECSQL 查询存储在任何 Element 类的 `JsonProperties` 成员中的数据。以下示例检索 `ABCConnector_props.conversionStatus` Json 值不等于 `incomplete` 的 Elements 的 `ABCConnector_props.lastConversionElapsedTime` Json 值。

```sql
SELECT json_extract(JsonProperties, '$.ABCConnector_props.lastConversionElapsedTime')
FROM bis.Element
WHERE json_extract(JsonProperties, '$.ABCConnector_props.conversionStatus') <> 'incomplete'
```

有关支持的函数的更多信息，请参阅 JSON functions and operators。

## Elements 与 Models

每个 Element 位于单个 Model 中。该 Model 包含并拥有该 Element。除非首先删除所有 Elements，否则无法删除 Models。Models 为其 Elements 提供上下文和范围。

每个 `Model` 对某个 `Element` 进行子建模，意味着它建模与 `Element` 相同的主题，但粒度更细。这是信息层次结构的基本构建块，是 BIS 的关键原则，支持在单个 Repository 中从多个视角和多个粒度对现实进行建模。它还在每个 BIS Repository 中产生连贯和可预测的结构，其中所有信息都可以追溯到整个 BIS Repository 的单个根 Subject。

"每个 Model 子建模一个 Element"规则有一个例外：每个 BIS Repository 中恰好有一个 RepositoryModel 不子建模另一个 Element（至少不是同一个 BIS Repository 中的另一个 Element）。这个 RepositoryModel 位于 Model/Element 信息层次结构的顶部。

## iModels 中的 ElementIds

当存储在 iModel 中时，Elements 还有一个唯一的 64 位本地标识符，称为 ElementId。ElementId 是在通过将 BriefcaseId 存储在高 24 位中，并将下一个可用的序列号存储在低 40 位中来创建新 Elements 时生成的。这允许在任何 Briefcase 中创建新 Elements，而不必担心 ElementId 冲突。

BriefcaseId 是分配给 Briefcase 的唯一标识符。Briefcase 是一个 SQLite 数据库，以可查询和可编辑的形式保存 iModel 一个版本的所有信息。

## Elements 与子 Elements

一个 Element 可以有子 Elements。父 Element 和子 Elements 必须位于同一个 Model 中。父子关系意味着所有权和级联删除。这在下面的 Assemblies 部分中有更多讨论。

## 核心 Element 类

这些是在 `BisCore` schema 中定义的 Element 子类，所有其他 Element 类必须从中继承：

- `GeometricElement`
- `InformationContentElement`
- `RoleElement`

![Core Element Classes](https://www.itwinjs.org/media/core-element-types.png)

### GeometricElement

`GeometricElement` 表示任何我们选择建模为本质上几何的现实世界实体，以便可以图形化显示。

这包括物理实体（如配电盘、梁和泵）以及几何上下文中的图形图形（线、弧、圆和注释如文本、图等）。

仅仅具有几何属性并不一定足以使实体由 `GeometricElement` 表示；例如，钢截面形状是 `DefinitionElement`，而不是 `GeometricElement`。

![Geometric Element](https://www.itwinjs.org/media/geometric-element.png)

`BisCore` schema 中定义的 `GeometricElement` 层次结构如上图所示。

2d 分支中类的简要描述：

- `GeometricElement2d` - 本质上是 2d 的 Element。
- `GraphicalElement2d` - 保存图形信息而不是具有业务含义的几何体的 2d Element。
- `DrawingGraphic` - 旨在放置在 Drawing 上的 2d 图形 Element。

3d 分支中类的简要描述：

- `GeometricElement3d` - 本质上是 3d 的 Element。
- `GraphicalElement3d` - 保存图形信息而不是具有业务含义的几何体的 3d Element。示例包括文本注释或 3d 条形图。`GraphicalElement3d` 的实例通常由于空白原因定位，因为它们不与现实世界的 3d 空间相关联。
- `SpatialElement` - 表示存在于现实世界 3d 空间中并与其相关的实体的 Element。
- `PhysicalElement` - 表示真实物理实体（即有质量的实体）的 SpatialElement。
- `SpatialLocationElement` - 表示现实世界中某个定义点、曲线、表面或体积的 SpatialElement。空间位置不是物理的，没有质量。示例包括地界线、分区范围、alignment 或网格线。

### InformationContentElement

`InformationContentElement` 是为携带和跟踪信息而存在的 Element。Information Elements 本质上是非几何的，不能图形化显示，但可以包含几何属性（用于定义或规范目的）。

示例包括：

- 文档
- 共享定义
- 需求
- 规范
- 信息记录

![Information Element](https://www.itwinjs.org/media/information-element.png)

有关 BisCore 中 `InformationContentElement` 子类的详细信息，请参阅 Information Models and Elements。

### RoleElement

角色在 BIS 将特定于应用程序的领域孤岛分解为允许共享和利用公共信息的片段的能力中起着至关重要的作用（双关语）。

![Role Element](https://www.itwinjs.org/media/role-element.png)

![Person Lawyer Father Son Example](https://www.itwinjs.org/media/person-lawyer-father-son.png)

![Person Lawyer Father Son Example 2](https://www.itwinjs.org/media/person-lawyer-father-son-2.png)

![Pollution Risk Example](https://www.itwinjs.org/media/pollution-risk-example.png)

角色通过 PhysicalElement 相互链接。

每个角色可能包含一些冗余信息，但通常应共享 `PhysicalElement` 的物理形式和属性。

在我们的虚拟世界中，角色可能与 PhysicalElements "不同步"，甚至可以在没有相应 PhysicalElement 存在的情况下存在。这些不同步的情况通常代表不完整的工作（P&ID 已更改，但 3d 模型尚未更新以反映更改），但有时反映长期条件（车辆角色在资产管理系统中建模，但不需要创建卡车的物理模型）。

## Assemblies

Element 可以选择具有父 Element。父 Elements 必须与其子 Elements 在同一个 Model 中。可以通过这些父子关系创建 Elements 层次结构（注意：层次结构中的所有 Elements 将驻留在同一个 Model 中）。作为父 Element 的 Element 可以被认为组装其子 Elements，它们统称为 Assembly。Assemblies 可以嵌套。不允许父子关系的循环网络。

Assemblies 意味着所有权和级联删除。当删除父 Element 时，其所有子 Elements 也会被删除。

Assemblies 往往遵循三种模式：

1. Assembly 纯粹是一个聚合；父 Element 的主要角色是将子 Elements 分组在一起（示例：钢筋笼将各种钢筋收集在一起）
2. Assembly 是一个详细说明；父 Element 中的属性（或其他信息）允许生成子 Elements（示例：管道支架生成管夹、梁夹和螺纹杆）
3. Assembly 是一个带有修改的项目；父 Element 定义子 Elements 修改的基础（示例：BeamCope 修改 Beam）

由于 Element 只能有一个父 Element，因此领域和应用程序协调以确保不存在 Element 应该具有哪个父 Element 的冲突非常重要。协调父级的最佳通用规则是领域作者确定哪些 Elements（如果有）可以作为其 Elements 的父级。

Elements 类通常分为四类：

1. Element 可以有任何父级或没有父级（示例：Bolt）。
2. Element 不能有父级。
3. Element 只能有特定类的父级。
4. Element 总是有父级，但对父级的类几乎没有限制（示例：Hole）。

在设计 assemblies 时，必须注意避免重复计算。

另请参阅下面的 IParentElement 和 ISubModeledElement 部分。

## IParentElement 和 ISubModeledElement

本节尽量不重复 Model Fundamentals 和 Information Hierarchy 中的材料。

如果您对 Elements 如何被子建模有疑问，您可能需要浏览这些文章。

有两个 mixin 声明和定义 Element 的关键行为：

- `IParentElement` - 此 Element 可以是父 Element
- `ISubModeledElement` - 此 Element 可以有关联的子 Model

Element 类不包括这两个接口中的任何一个，因此默认情况下没有 Element 可以有子级或可以被子建模。许多 Elements 不需要子 Elements 或子 Models，因此不会使用这两个 mixin 中的任何一个。Bolt 类是不需要这两个的类的示例。

这些 mixin 预期是互斥的。没有实现 `IParentElement` 的类也会实现 `ISubModeledElement`。这两个 mixin 被认为是互斥的原因是这两个概念（拥有子级和拥有子 Model）都是进行更细粒度建模的手段，同时使用这两种技术可能会导致混乱和重复计算。

## 父子关系

所有 Element 父子关系都继承自 `ElementOwnsChildElements`，不应直接使用。

有 `ElementOwnsChildElements` 关系的特化（子类）可以阐明父级和子级的关系。

示例包括：

- `PhysicalElementAssemblesElements` - 用于指示子 Elements 聚合到父 Element 中，其几何完全是聚合。
- `ElementEncapsulatesChildElements` - 当子 Elements 表示内部数据时使用，通常不向用户公开或在父 Element 上下文之外有用。
- `SubjectOwnsSubjects`、`SubjectOwnsPartitionElements` - 这些关系用于约束作为 `Subject` Element 的有效子级的 Elements 集合。

## Groups

虽然父子关系具有嵌入强度并意味着独占所有权，但分组关系具有引用强度并意味着非独占成员资格。

分组技术将根据分组成员 Elements 集合是：

1. Element 的主要角色或
2. Element 的次要角色而变化。

在第一种情况下，使用 `ElementGroupsMembers` 关系将组成员与代表整个组的 `GroupInformationElement` 关联起来。

`GroupInformationElement` 除了分组之外没有其他存在的理由。

在第二种情况下，可以使用标准的 1:N 关系，并隐含分组。

这种情况下的分组 Element 将是有价值的，无论它是否有成员。

---

| 下一篇：Codes
|:---
