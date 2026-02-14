# Schema Versioning and Generations（Schema 版本控制和代际）

## Schema Versions

随着产品（应用程序和服务）的发展，它们将需要新的或不同的数据组织。由于数据组织在 schemas 中定义，schemas 必须更改以支持更新的产品。这导致需要明确地对 schemas 进行版本控制。

Schema versioning 不应与 data versioning 混淆。数据将由用户非常频繁地更改。Schemas 更改频率较低，仅在需要新数据组织的改进产品发布时更改。

## Schema Upgrade Strategy 的必要性

大多数 iModels 由多个产品访问。产品将通过 iModelHub 同步。产品存储的数据将由单个（版本化的）schemas 集合组织。

确保所有产品都可以使用 iModel 中 schemas 的一种潜在策略是将使用的产品限制为为 iModel 中 schemas 的确切版本编写的产品子集。如果希望更新产品并且该更新需要更新的 schemas，则所有访问 iModel 的产品同时更新。当使用超过非常小数量的应用程序和服务时，这很快就变成了一个难以维持的策略。因此，我们的 schema evolution strategy 需要适应非对齐的产品发布。

BIS schema upgrade strategy 基于 _Generations_ 的概念，这与 _Minor Schema Upgrades_ 和 _Major Schema Upgrades_ 密切相关。

一些不直接与 iModels 一起工作的服务将使用 _BIS semantics_。这些服务也将受益于本节中描述的 versioning strategy。

## EC Schema Versioning

有明确的 EC schema versioning 规则，这些规则基于 schema upgrade 期间所做更改的影响。

### Minor Schema Upgrades

Minor schema upgrades 是不破坏为先前 schema 编写的应用程序兼容性的 schema 更改。

Minor schema upgrades __只能__包括：

- 添加 optional classes
- 在 class hierarchy 中间添加类
- 添加 optional properties
- 添加 Kinds of Quantities
- 添加和删除 Property Categories
- 放宽约束
  - Class modifier 从 Sealed 更改为 None
  - 使 relationship constraint 多态或降低最小值或增加最大 cardinality
- 对不影响代码（或含义）的项目的更改，例如：
  - display label、role label 或 description 更改
  - presentation unit 或 format 更改（在 KindOfQuantity 定义中或通过将属性切换到具有相同 persistence unit 的不同 KindOfQuantity）
  - 任何其他仅影响 presentation 的更改

Minor schema upgrades __不能__包括：

- 删除 classes
- 删除 properties
- 更改 class definition（例如，更改 base class 使该类不再'是'原始 base class）
- 更改 property definition（例如，更改类型或更改 KindOfQuantity 如果它更改 persistence unit）
- 更改 relationship constraints 或 strength 或缩小 cardinality

### Major Schema Upgrades

Major schema upgrade 可能会破坏为先前 schema 编写的应用程序的兼容性。任何不符合 minor 条件的 schema 更改都是 major。触发 major schema change 的一些更改示例包括：

- 删除 class
- 删除 property
- 重命名 class 或 property
- 以使 former parent class 不再是 direct ancestor 的方式更改 base class（目前任何 parent class 的更改都是 major schema upgrade）
- 更改 property 的类型
- 更改 relationship constraints 或 cardinality

### Schema Version Numbers

为了能够检测对读取数据向后兼容但对写入数据不向后兼容的 schema 更改，EC Schema version numbers 有 3 个部分

| 数字 | 含义 | 更改意味着 |
| --- | --- | --- |
| 第1位 (read) | Schema 的 Generation，保证（_如果数字匹配_）较新 schemas 的数据可以由较旧的软件__读取__。 | 不能假设与先前 schema versions 的兼容性（破坏 _read_ 和 _write_ 逻辑） |
| 第2位 (write) | Schema 的 Sub-generation，保证（_如果数字匹配_）较新 schemas 的数据可以由较旧的软件__写入__。 | 已向 schema 添加内容，这破坏了现有的 _write_ 逻辑（但不破坏 _read_ 逻辑） |
| 第3位 (minor) | 最不重要的版本号，随 _read/write_ 兼容的添加而递增。 | 已向 schema 添加内容，但它们不破坏现有的 schema _read_ 或 _write_ 逻辑。 |

这个 3 位系统与 Semantic Versioning 中描述的标准 3 位 versioning strategy 有点不同。这主要是由于 Semantic Versioning 涉及 APIs 和代码而不是 schemas。

### 中间版本号

第二个 _write_ 版本号有点难以理解 - _它如何对应 Major Schema Updates 和 Minor Schema Updates？_

实际上，第二个 _write_ 版本号在 schema upgrade 可以被视为数据写入者的 major update，但只是数据读取者的 minor update 时更新。

例如，考虑在 schema 1 中我们有一个存储成绩的 _Student_ class，具有（double）properties：

- _Language_
- _Math_
- _Science_
- _Music_
- _Overall GPA_（前 4 个属性的平均值）

如果 schema 2 向 _Student_ 添加一个 double property _Psychology_，则 _Overall GPA_ 的含义略有变化，因此，为 Schema 1 编写的应用程序：

- 仍然可以安全地读取 schema 1 中的所有值
- 无法修改 schema 1 中的任何值，因为它们可能会错误地设置 _Overall GPA_

为具有 _write_ 版本更改的 schema update 更新数据通常需要一些自定义逻辑。这不应该令人惊讶，因为先前数据是由与较新 schema 不写入兼容的应用程序编写的。

#### 写入不兼容更改的示例

- 在现有 class 的新 property 上添加 _Not Null_ 或 _Unique_ constraint
- 在现有 class 上添加带有 _Foreign Key_ constraint 的新 _Navigation Property_

还有其他写入不兼容更改的示例，但是，它们被软件禁止，因为它们会修改 EC 内容如何映射到数据库（这通常是不允许的）：

- 在现有 property 上添加 _Not Null_ 或 _Unique_ constraint
- 向现有 class 添加新的 unique index
- 向现有 _Navigation Property_ 添加 _Foreign Key_ constraint

### Application Schema Compatibility Logic

为特定 schema 版本编写的应用程序与可能具有不同 schema 版本的 repository 一起工作的一般逻辑将是：

- 如果 repository 中的 schema 较新（或相同）：
  - 如果第一位数字匹配，应用程序可以安全读取。
  - 如果前两位数字匹配，应用程序可以安全写入（和读取）。
  - 如果没有数字匹配，则 schema 属于不同的 generation，应用程序无法执行任何操作。
- 如果 repository 中的 schema 较旧：
  - 如果前两位数字匹配，应用程序可以升级 repository schema 而不会破坏其他应用程序的读取或写入。
  - 如果仅第一位数字匹配，应用程序可以升级 repository schema，但升级将阻止某些较旧的应用程序写入。
  - 如果没有数字匹配，则 schema 属于不同的 generation，应用程序无法执行任何操作。

## BIS Generations

Major schema upgrades 在任何发展的产品或系统中最终都是必需的。如果允许每个 Domain 选择其主要 schema updates 何时发生，那么 - 由于 BIS 将有大量 Domains - 几乎每个 BIS 版本都会包含一些 major schema updates。

为了避免持续 major schema updates 的混淆，定义了 BIS Generations 并限制了 major schema updates。

### BIS Generation

BIS Generation 由一系列版本组成，在此期间不允许任何 Domain 进行 major schema upgrades。由于 minor schema upgrades 不会破坏应用程序兼容性，基于相同 BIS Generation 的任何应用程序都可以通过 iModel 一起工作。

EC Schemas 的 3 位 schema version numbers（_Read.Write.Minor_）允许定义两种类型的 Major schema version。作为__紧急__出口，允许在 Generation 内更改 _Write_ 版本号，但这将受到严格阻止。为确保对 _Write_ 版本号的更改受到足够重视，建议对任何此类 _Write_ 更改进行 OCTO review。

必须记住，repositories 可以从一个 Generation 更新到下一个 Generation 而不会丢失数据。只能与来自单个 Generation 的 repositories 一起工作的是单个应用程序。

### Generation Schema Numbering

由于 BIS Generations 与 major schema upgrades 紧密对齐，因此自然使用 Generation number 作为所有 BIS Domains 的 major schema version。Generation 中所有 schemas 的编号是 _Generation.Write.Minor_，其中 BIS repository 中的所有 _Generation_ 数字匹配。_Write_ 数字几乎总是 0。_Minor_ 数字可以并且将会变化。

---

| 下一篇：Schema Production Status
|:---|
