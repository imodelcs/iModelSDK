# Schema Customization（Schema 定制）

## 介绍

虽然 BIS 建模了建筑基础设施世界的大部分内容，并且不断添加新的特定领域 domain schemas，但不可避免地需要存储 BIS 尚未涵盖的数据。出现这种情况的常见场景包括：

- 对现有 BIS 概念的定制和扩展（通常按项目或按公司）
- 供应商特定信息
- 从其他基础设施相关数据库传输信息（例如通过 iModel connectors）
- 建模 BIS 中目前不存在的概念
- 需要向 Elements 添加非结构化信息

本页面讨论创建和控制这些数据（称为"custom data"）的可用策略，并提供最佳实践建议。Custom data 应根据数据性质以及 property definitions 和值的差异进行不同的建模。

按类或类型变化的属性应使用 property definitions 建模，按实例变化的属性应使用 Json 建模。

## Vendor Data 和相关目录

供应商通常需要定义 Element subclasses 和相关的 Type subclasses。例如，泵供应商可能定义一个 Pump subclass（BigCo:MonsterPump）和相关的 PumpType subclass（BigCo:MonsterPumpType）。

BigCo:MonsterPumpType 可能定义四个新属性：

- ModelNumber
- Power
- InletDiameter
- OutletDiameter

BigCo:MonsterPump 可能定义一个新属性：

- OutletLength

当 BigCo 的泵目录分发时，它将包括：

- BigCo:MonsterPump class definition
- BigCo:MonsterPumpType class definition
- 多个 BigCo:MonsterPumpType 实例（定义可供购买的泵类型）

## 从其他数据库导入的数据（包括通过 iModel Connectors）

将数据从其他数据库转换为 BIS 数据的技术（通常是 iModel connectors）通常需要从原生数据库中的类结构转换为 BIS 类结构。BIS schema 很少能"开箱即用"。通常，转换器需要定义一个 dynamic schema，然后将数据从原生 DB 转换为新 dynamic schema 类的实例（可能还有一些标准 BIS 类的实例）。

## Dynamic Schema Minor Change 注意事项

由于 dynamic schemas 是 BIS schemas 的扩展，它们必须遵循 BIS schemas 的规则以防止升级问题。这些规则在 Schema Versioning and Generations 中定义。这些规则中最值得注意的是类和属性不能被删除或显著重新定义。通常，只允许向 schemas 添加内容。

## Minor（BIS）Schema Upgrade 注意事项

如 Schema Versioning and Generations 中定义，BIS schemas 可以在 generation 内的几乎任何时间升级。Dynamic schemas 中的类总是从 BIS 类继承，因此它们可能几乎随时受到这些 minor upgrades 的影响。

这些 minor schema upgrades 的最大危险是 BIS 类可能添加一个与 dynamic subclass 中属性同名的属性。当升级后的 schema 导入 BIS repository 时，此类将导致问题。

类名冲突（在 BIS 中添加的类与 dynamic schema 中的类同名）不是技术问题，因为类由包含它们的 schema 名称限定。但是，重复的类名可能导致用户混淆。

## Generational（BIS）Schema Upgrade 注意事项

如 Schema Versioning and Generations 中定义，generational changes 允许对 schemas 进行根本性更改，并且必须伴随理解如何将数据（Elements 和 Models）从一个 generation 的 schemas 映射到另一个的代码。Generational mapping 代码可能非常复杂；例如，它可能包括：

- 1:1, 1:N, N:1, N:N instance mapping
- 1:1, 1:N, N:1, N:N property mapping
- 在类之间移动属性（作为一个简单的例子，从 PhysicalElementType subclass 移动到其相关的 PhysicalElement subclass）
- 重新排列 Model hierarchy

---

| 下一篇：Data Evolution Across Time
|:---|
