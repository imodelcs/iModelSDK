# BIS Schema Validation (BIS Schema 验证)

> 原文: [BIS Schema Validation](https://www.itwinjs.org/bis/guide/other-topics/bis-schema-validation/)
>
> 最后更新: 2025年6月11日

Schema 规则的可变性和潜在复杂性导致需要对 BIS schema 进行质量控制和长期可维护性。

## BIS 使用 EC v3

BIS 使用 EC v3 定义。EC v3 是 EC 的一个更清晰定义和更严格的版本，已在 Bentley 广泛使用超过 10 年。

BIS 被模块化为一组相互关联的**域**（每个域在一个单独的 ECSchema 中表达），它们是一致、协调和受约束的，以最大化整个基于 BIS 的生态系统的功能。"原始" EC 中可用的一些灵活性在 BIS 中不可用。例如，在域 ECSchema 中定义的所有 ECClass（除了 BisCore 本身）都需要从 BisCore 中的某个 ECClass 派生。

除非另有说明，本文档中对 "schema"、"class" 和 "property" 的所有引用均指 ECSchema、ECClass 和 ECProperty。

## 验证规则

BIS Schema 根据一组规则进行验证。如果违反一条规则，整个 schema 将无法通过验证。

规则根据它们验证的 Schema 的不同部分进行分类。

### 通用（Schema）规则

#### BIS-001

Schema 必须加载并通过 EC3.1 [spec 验证](../../ec/ec-schema-validation.md)。

#### BIS-002

Schema 的 ECXML 版本必须至少为 3.1。

- `<ECSchema ... xmlns=http://www.bentley.com/schemas/Bentley.ECXML.3.1 />`

#### BIS-003

Schema 不得引用任何 EC2 或 EC3.0 schema。

#### BIS-004

Schema 必须指定三部分版本号

- 版本号必须采用 RR.WW.mm 格式（即 Read.Write.Minor）
- 每个版本组件必须用零填充到两位数字（例如 01.02.00）

#### BIS-005

Schema 引用必须指定三部分版本号（格式同上）。

#### BIS-006

如果 schema 名称中包含 'dynamic'（不区分大小写），则必须应用 **CoreCA:DynamicSchema** 自定义属性。

#### BIS-007

同一 schema 内的类不能具有相同的显示标签。

#### BIS-008

Schema 不应引用已弃用的 schema。

#### BIS-009

Schema 引用中的别名必须与 schema 定义的别名相同。

### 类规则

#### BIS-100

同一类和类别内的属性不能具有相同的显示标签。

#### BIS-101

不在 **BisCore**、**Functional** 或 **Generic** schema 内的类不能应用 **bis:ClassHasHandler**。

#### BIS-102

类不应从已弃用的类派生。

#### BIS-103

类不应有已弃用的属性。

#### BIS-104

类不应有已弃用 struct 类型的属性。

#### BIS-105

类不应使用已弃用的自定义属性。

### 自定义属性类

#### BIS-400

自定义属性类不能有基类。

### 实体类规则

#### BIS-600

实体类必须从 BIS 层次结构派生。

#### BIS-601

实体类只能从一个基实体类派生。

#### BIS-602

实体类不能从多个基类继承属性。

#### BIS-603

Mixin 属性不能覆盖从基实体类继承的实体属性。

#### BIS-604

如果存在任何 aspect（从 **bis:ElementMultiAspect** 派生的 ECClass），则必须有一个从 **bis:ElementOwnsMultiAspects** 关系派生的关系，并将此类作为目标约束支持。

- 如果 schema 应用了 **CoreCA:DynamicSchema** CA，则视为警告。

#### BIS-605

如果存在任何 aspect（从 **bis:ElementUniqueAspect** 派生的 ECClass），则必须有一个从 **bis:ElementOwnsUniqueAspect** 关系派生的关系，并将此类作为目标约束支持。

- 如果 schema 应用了 **CoreCA:DynamicSchema** CA，则视为警告。

#### BIS-606

实体类不能同时实现 **bis:IParentElement** 和 **bis:ISubModeledElement**。

#### BIS-607

实体类不能子类化以下类：

- **bis:PhysicalModel**
- **bis:SpatialLocationModel**
- **bis:GroupInformationModel**
- **bis:InformationRecordModel**
- **bis:DefinitionModel**
  - **bis:DictionaryModel** 和 **bis:RepositoryModel** 是唯一允许子类化 **bis:DefinitionModel** 的类
- **bis:DocumentListModel**
- **bis:LinkModel**

#### BIS-608

属性覆盖不能更改持久化单位。

#### BIS-609

**bis:Model** 的子类不能在 **BisCore** 之外定义额外的属性。

#### BIS-610

实体类不能子类化已弃用的类。

#### BIS-611

实体类不应从已弃用的 mixin 类派生。

### KindOfQuantities

#### BIS-1001

KindOfQuantity 必须使用 SI 单位作为其持久化单位。

#### BIS-1002

KindOfQuantity 不能有重复的显示格式。

### Mixin 规则

#### BIS-1100

Mixin 类不能覆盖继承的属性。

### 属性

#### BIS-1300

属性不应为 **long** 类型。如果表示外键，这些属性应为导航属性；如果表示数字，应为 **int** 或 **double** 类型。

#### BIS-1301

同一类和类别内的属性不能具有相同的显示标签。

#### BIS-1302

属性必须使用以下支持的 ExtendedTypes：

- **BeGuid**
- **GeometryStream**
- **Json**
- **URI**

#### BIS-1303

属性不得使用自定义属性 **bis:CustomHandledProperty**，除非在其父类上定义了自定义属性 **bis:ClassHasHandler**（**不是**从基类派生的）。

### 关系类

#### BIS-1500

关系类不得使用 holding 强度。

#### BIS-1501

如果强度是 embedding 且方向是 forward，关系类的源约束多重性上限不得大于 1。

#### BIS-1502

如果强度是 embedding 且方向是 backward，关系类的目标约束多重性上限不得大于 1。

#### BIS-1503

如果只有一个具体约束集，关系类不得有抽象约束。

#### BIS-1504

关系类不得有 **bis:ElementAspect** 目标约束（如果方向是 backward 则是源约束），除非它们从 **bis:ElementOwnsUniqueAspect** 或 **bis:ElementOwnsMultiAspects** 派生。

#### BIS-1505

Embedding 关系不应在类名中包含 'Has'。

#### BIS-1506

关系约束不应使用已弃用的类或 mixin 作为约束类。

#### BIS-1507

关系约束不应使用已弃用的类或 mixin 作为抽象约束。

#### BIS-1508

关系约束不应使用从已弃用基类或已弃用 mixin 类派生的约束类。

#### BIS-1509

关系约束不应使用从已弃用基类或已弃用 mixin 类派生的抽象约束。

### Struct 类

#### BIS-1700

Struct 类不能有基类。

---

| 下一篇: [BIS Glossary](../references/bis-glossary.md)
|:---
