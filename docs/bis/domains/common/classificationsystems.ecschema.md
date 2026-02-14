# ClassificationSystems Schema

**别名 (Alias):** clsf

**版本 (Version):** 1.0.4

用于元素分类的 Schema。

本 Schema 包含用于建模分类系统的类，分类系统是用于对现实世界对象进行分类或归类的有组织定义集合。

在 BIS 中，一个 ClassificationSystem 由一个或多个 ClassificationTable 组成。每个 `ClassificationTable` 是一个 `ISubModeledElement`，其子模型包含 Classification。在子模型中，Classification 可以使用 ClassificationOwnsSubClassifications 父子关系进行层级排列，并使用 ClassificationGroup 和 ClassificationGroupGroupsClassifications 进行分组。

![类和实例图](https://www.itwinjs.org/media/classification-systems.png)

## 目录

- Entity Classes (实体类)
  - Classification
  - ClassificationGroup
  - ClassificationSystem
  - ClassificationTable
- Relationship Classes (关系类)
  - ClassificationGroupGroupsClassifications
  - ClassificationOwnsSubClassifications
  - ClassificationSystemOwnsClassificationTable
  - ClassificationSystemOwnsClassifications
  - DefinitionModelBreaksDownClassificationTable
  - ElementHasClassifications

## Entity Classes (实体类)

### __Classification__ (分类) EntityClass

表示分类系统中单个条目的元素。

**基类 (Base Class):** BisCore:DefinitionElement

`Classification` 元素代表分类系统将现实世界对象归入其中的一个"类"或"类别"。

`Classification` 元素始终持久化在作为所属 `ClassificationTable` 子模型的 `bis:DefinitionModel` 中。

- OmniClass 11-13 11 11 和 UniClass 2015 En_20_10_45 是分类的示例
- 分类的 Code 应具有以下组件：必须采用 (ClassificationTable.id, ClassificationName, CodeSpecId("Classification")) 的形式
  - `CodeSpec.Id` - 名称为 `"clsf:Classification"` 的 CodeSpec 的 Id。
  - `CodeScope.Id` - 父元素或包含模型的 Id，应为以下之一：
    - 对于像 OmniClass 和 UniClass 这样复杂分类系统的顶级分类，应为包含的 `ClassificationTable` 的 Id。
    - 对于子分类的情况，应为父 `Classification` 的 Id，除非分类系统要求表中的所有子分类都是唯一的（此时应为包含的 `ClassificationTable` 的 Id）
  - `CodeValue` - 分类的名称。

一个 `Classification` 可以通过 `ClassificationOwnsSubClassifications` 关系特化另一个 `Classification` 元素。

- MasterFormat: 00 31 13 Preliminary Schedules -> 00 31 13.13 Preliminary Project Schedule 和 OmniClass Table 13: 13-11 00 00 Space Planning Types -> 13-11 11 00 Planned Work Space 是分类特化的示例。

一个元素可以通过 `ElementHasClassifications` 关系被分类为多个 Classification。

参见概述。

等效于 IfcClassificationReference。

#### 属性 (Properties)

| 名称 | 描述 | 类型 | 扩展类型 |
| --- | --- | --- | --- |
| Description | 此 Classification 的描述 | string |  |
| Rank | Classification 的 Rank 表示它是如何创建的、谁知道它以及它可以在哪里使用。 | DefinitionElementRank |  |

继承属性

| 名称 | 描述 | 类型 | 扩展类型 |
| --- | --- | --- | --- |
| Model | 包含此 bis:Element 的 bis:Model。 | navigation |  |
| LastMod | bis:Element 的最后修改时间。由核心框架维护，应用程序不应直接设置。 | dateTime |  |
| CodeSpec | CodeSpec 属性标识用于生成和验证此 bis:Element 代码值的 bis:CodeSpec。CodeSpec、CodeScope 和 CodeValue 属性的组合对于每个 bis:Element 实例必须是唯一的。 | navigation |  |
| CodeScope | CodeScope 属性标识为代码值提供唯一性范围的 bis:Element。CodeSpec、CodeScope 和 CodeValue 属性的组合对于每个 bis:Element 实例必须是唯一的。 | navigation |  |
| CodeValue | 保存 Element 代码实际文本的可空字符串属性。CodeSpec、CodeScope 和 CodeValue 属性的组合对于每个 bis:Element 实例必须是唯一的。 | string |  |
| UserLabel | 用户给定的可选友好名称（与存储在 CodeValue 属性中的正式名称相对）。 | string |  |
| Parent | 拥有此 bis:Element 的父 bis:Element。 | navigation |  |
| FederationGuid | 用于在存储库之间联合此 bis:Element 的 GUID。 | binary | BeGuid |
| JsonProperties | 用户和/或应用程序可用于持久化临时 JSON 值的字符串属性。 | string | Json |
| IsPrivate | 如果为 true，则此 bis:DefinitionElement 不应在 GUI 中显示。 | boolean |  |

### __ClassificationGroup__ (分类组) EntityClass

ClassificationGroup 用于对分类进行分组。

**基类 (Base Class):** BisCore:GroupInformationElement

`ClassificationGroup` 是 `Classification` 元素的组，按照原始分类系统中的分组方式。`Classification` 元素通过 `ClassificationGroupGroupsClassifications` 关系分配给一个组。

- MasterFormat subdivisions 和 ASHRAE 62.1 Occupancy Category groupings 是分类组的示例。

`ClassificationGroup` 元素旨在持久化在作为所属 `ClassificationTable` 子模型的 `bis:DefinitionModel` 中。

参见概述。

不映射到或从 IFC 映射，因为 IFC 中不存在组的概念。

#### 属性 (Properties)

| 名称 | 描述 | 类型 | 扩展类型 |
| --- | --- | --- | --- |
| Description | 此 ClassificationGroup 的描述 | string |  |

### __ClassificationSystem__ (分类系统) EntityClass

用于表示分类系统的元素。

**基类 (Base Class):** BisCore:DefinitionElement

`ClassificationSystem` 标识各个 Classification 所属的分类系统。

对于知名和外部定义的标准，名称 (CodeValue) 通常足以标识分类系统。消费应用程序只需要创建或使用具有适当名称的实例。对于这些情况，可以直接使用 `ClassificationSystem` 类。

在其他情况下，如果分类系统是自定义的或不太知名的，可能需要子类化 `ClassificationSystem` 来标识特定类型的分类系统。

参见概述。

- 建议将全局适用的 `ClassificationSystem` 元素放在 DictionaryModel 中。但是，如果分类系统是出于某种目的局部的，将 `ClassificationSystem` 元素放在任何其他 DefinitionModel 中也是合理的。
- 所有全局 `ClassificationSystem` 元素的 Code 应具有以下组件：
  - `CodeSpec.Id` - 名称为 `"clsf:ClassificationSystem"` 的 CodeSpec 的 Id。
  - `CodeScope.Id` - 全局分类系统的根 SubjectId。如果分类系统不被视为全局的，这应该是根 SubjectId 以外的其他值。
  - `CodeValue` - 应设置为 `name + " " + edition`。
- UniClass 2015、UniClass 2018 和 OmniClass 是分类系统的示例。组织也可能有自己的自定义分类系统。

预期任何 iModel 都不会包含所有已知的分类系统。相反，iModel 只会包含该 iModel 使用的那些分类系统，并且可能只包含分类系统层次结构中被使用的部分。

`ClassificationSystem` 和 `ClassificationTable` 的组合等效于 IfcClassification。

#### 属性 (Properties)

| 名称 | 描述 | 类型 | 扩展类型 |
| --- | --- | --- | --- |
| Source | 此分类的来源（或发布者） | string |  |
| Edition | 分类符号派生自的分类系统的版本或版本号。 | string |  |
| Location | 分类的资源标识符或定位符，以 URI、URN 或 URL 形式提供。 | string |  |
| Description | 此 ClassificationSystem 的描述 | string |  |
| Rank | ClassificationSystem 的 Rank 表示它是如何创建的、谁知道它以及它可以在哪里使用。 | DefinitionElementRank |  |

### __ClassificationTable__ (分类表) EntityClass

用于表示分类系统中表的元素。

**基类 (Base Class):** BisCore:DefinitionElement

`ClassificationTable` 定义原始 ClassificationSystem 源中定义的 `ClassificationSystem` 中的表。分类表代表将分类系统划分为用于不同目的的分类。

- _OmniClass Construction Entities by Function - Table 11_ 和 _UniClass 2015 En Entities_ 是分类表的示例。
- 所有 `ClassificationTable` 元素的 Code 应具有以下组件：
  - `CodeSpec.Id` - 名称为 `"clsf:ClassificationTable"` 的 CodeSpec 的 Id。
  - `CodeScope.Id` - 拥有它的 `ClassificationSystem` 的 Id，应与 `ClassificationTable` 的 `Parent.Id` 属性相同。
  - `CodeValue` - 分类表的名称。

`ClassificationTable` 将在其子模型中包含 `Classification` 和 `ClassificationGroup` 元素。

参见概述。

`ClassificationSystem` 和 `ClassificationTable` 的组合等效于 IfcClassification。

#### 属性 (Properties)

| 名称 | 描述 | 类型 | 扩展类型 |
| --- | --- | --- | --- |
| Description | 此 ClassificationTable 的描述 | string |  |
| Rank | ClassificationTable 的 Rank 表示它是如何创建的、谁知道它以及它可以在哪里使用。 | DefinitionElementRank |  |

## Relationship Classes (关系类)

### __ClassificationGroupGroupsClassifications__ RelationshipClass

将 Classification 映射到其组。

**基类 (Base Class):** BisCore:ElementGroupsMembers

**强度 (Strength):** Referencing

**强度方向 (Strength Direction):** Forward

#### Source

**Is Polymorphic:** true

**角色标签 (Role Label):** groups

**多重性 (Multiplicity):** (0..*)

**约束类 (Constraint Classes):**
- ClassificationGroup

#### Target

**Is Polymorphic:** true

**角色标签 (Role Label):** is grouped in

**多重性 (Multiplicity):** (0..*)

**约束类 (Constraint Classes):**
- Classification

### __ClassificationOwnsSubClassifications__ RelationshipClass

用于表示一个分类特化另一个分类的关系。

**基类 (Base Class):** BisCore:ElementOwnsChildElements

**强度 (Strength):** Embedding

**强度方向 (Strength Direction):** Forward

#### Source

**Is Polymorphic:** true

**角色标签 (Role Label):** owns

**多重性 (Multiplicity):** (0..1)

**约束类 (Constraint Classes):**
- Classification

#### Target

**Is Polymorphic:** true

**角色标签 (Role Label):** is owned by

**多重性 (Multiplicity):** (0..*)

**约束类 (Constraint Classes):**
- Classification

### __ClassificationSystemOwnsClassificationTable__ RelationshipClass

将分类系统映射到其表。

**基类 (Base Class):** BisCore:ElementOwnsChildElements

**强度 (Strength):** Embedding

**强度方向 (Strength Direction):** Forward

按照命名约定，此关系类本应命名为 `ClassificationSystemOwnsClassificationTables`（复数），但发布时使用了不合规的名称，发布后更改会造成破坏性影响。

#### Target

**Is Polymorphic:** true

**角色标签 (Role Label):** is owned by

**多重性 (Multiplicity):** (0..*)

**约束类 (Constraint Classes):**
- ClassificationTable

### __ClassificationSystemOwnsClassifications__ RelationshipClass (已弃用)

已确定即使是简单的 ClassificationSystems 也应该使用 ClassificationTable 层来维护一种一致的查询相关 Classifications 的方式。

**已弃用：** 标识由分类系统直接拥有的分类。

**基类 (Base Class):** BisCore:ElementOwnsChildElements

**强度 (Strength):** Embedding

**强度方向 (Strength Direction):** Forward

#### Target

**Is Polymorphic:** true

**角色标签 (Role Label):** is owned by

**多重性 (Multiplicity):** (0..*)

**约束类 (Constraint Classes):**
- Classification

### __DefinitionModelBreaksDownClassificationTable__ (DefinitionModel 子模型化 ClassificationTable) RelationshipClass

将 bis:DefinitionModel 与其子模型化的 ClassificationTable 关联起来。

**基类 (Base Class):** BisCore:ModelModelsElement

**强度 (Strength):** Embedding

**强度方向 (Strength Direction):** Backward

#### Source

**Is Polymorphic:** false

**角色标签 (Role Label):** models

**多重性 (Multiplicity):** (0..1)

**约束类 (Constraint Classes):**
- DefinitionModel

#### Target

**Is Polymorphic:** true

**角色标签 (Role Label):** is modeled by

**多重性 (Multiplicity):** (0..1)

**约束类 (Constraint Classes):**
- ClassificationTable

### __ElementHasClassifications__ RelationshipClass

将 Classifications 分配给 Elements。

**基类 (Base Class):** BisCore:ElementRefersToElements

**强度 (Strength):** Referencing

**强度方向 (Strength Direction):** Forward

#### Source

**Is Polymorphic:** true

**角色标签 (Role Label):** has classification

**多重性 (Multiplicity):** (0..*)

**约束类 (Constraint Classes):**
- Element

#### Target

**Is Polymorphic:** true

**角色标签 (Role Label):** classifies

**多重性 (Multiplicity):** (0..*)

**约束类 (Constraint Classes):**
- Classification

---

**来源:** https://www.itwinjs.org/bis/domains/classificationsystems.ecschema/

**最后更新:** 2025年7月8日
