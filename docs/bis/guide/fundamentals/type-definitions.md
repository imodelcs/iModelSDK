# Type Definitions

如果我们考虑由主 `Element` 建模的某个主实体，`Element` 的 ECEntityClass 告诉我们它是什么类型的实体，并且可以为建模实体添加新的 ECProperties。我们可以进一步将实例分类为子集，其中每个子集具有共享的属性值集。这些不同的属性值集中的每一个都是主实体的"type"（以具有所有这些共同的属性值为特征）。属性在 `TypeDefinitionElement` 的子类中定义，该子类定义了值据说随"type"变化的属性。

`TypeDefinitionElement` 类似于 IfcTypeObject。

实际上，这些"type"往往对应于产品型号（不要与 bis:Model 混淆），例如 Mazda 型号"RX-7"汽车。产品型号编号通常标识目录中的条目。目录条目将包括给定产品型号的所有实例共享的其他属性值。`TypeDefinitionElement` 表示这样的目录条目，`Code` 是产品型号编号。即使主 `Element` 是"定制的"并且实际上不来自目录，它仍然可以有一个定制的"目录条目"，例如具有与其他实例不共同的定制值的 `TypeDefinitionElement` 实例。它本质上是一个只有一个实例的"type"。

`TypeDefinitionElement` 补充类继承。它们在两个重要方面与类继承不同：

- `TypeDefinitionElement` 是 BIS Repository 中的"实例数据"。您可以在不更改 BIS Domain Schema 的情况下添加 `TypeDefinitionElement` 的新实例。
- `TypeDefinitionElement` 包含由其 `TypeDefinitionElement` ECEntityClass 定义的 ECProperties 的值，但不能引入新的 ECProperties。

主 `Element` 实例将具有与其类型实例（例如 `PhysicalType` 的子类）的关系（例如 `PhysicalElementIsOfType`）。被建模实体的完整属性通过组合主 `Element` 实例的属性值与其关联的 `TypeDefinitionElement` 实例的属性值来找到。

如果主 `Element` 实例具有与其 `TypeDefinition` 中同名的 ECProperty，则实例特定的值将覆盖类型特定的值。这类似于 IFC 处理应用于实例或类型的 Property Sets 的方式。

例如，假设我们使用 ECEntityClass `DoubleHungWindow` 建模双悬窗。大多数双悬窗是从目录订购的，您可以获得的窗口高度和宽度的排列组合只有目录中列出的那些。DoubleHungWindow ECEntityClass 的作者还将定义 `TypeDefinition`（或其子类 `PhysicalType`）`DoubleHungWindowType` 的子类，该子类具有双悬窗随类型（随目录条目）而不是随实例变化的所有属性的 ECProperties，例如 `Height`、`Width` 和 `IsInsulated`。对于许多产品，除了实体的空间位置外，随实例变化的不多。对于我们的双悬窗，可能有 4 种类型，每种都有作为其产品型号编号的 `CodeValue`：2x4I、2x3I、2x4U、2x3U。在 GUI 中，适用于给定主 `Element` ECEntityClass 的 `TypeDefinitionElement` 实例列表可用于填充给定 ECEntityClass 的可用"type"下拉列表。可以通过定义 `PhysicalElementIsOfType` 关系的特化来缩小可用类型列表。

下图显示了建模离心泵的 `PhysicalElement` 的类层次结构以及关联的 `PhysicalType` 和连接它们的专用关系。有关所用约定的详细信息，请参阅 Class-diagram Conventions。

![PhysicalTypes](https://www.itwinjs.org/media/physical-types.png)

虽然我们在这里以 PhysicalElements 为例描述类型，但此模式可以应用于其他类型的 Elements。关系 `GeometricElement2dHasTypeDefinition` 和 `GeometricElement3dHasTypeDefinition` 使该模式可用于几何元素，但可以添加新的关系类以支持其他类型 Elements 的"type-system"。

---

| 下一篇：Categories
|:---
