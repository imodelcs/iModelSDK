# Functional Schema

__Alias:__ func

__Version:__ 1.0.4

Functional schema 定义了供特定学科功能域使用的通用基类。

Functional domain schema 包含定义 "Functional"（功能）建模视角的核心类。

"Functional" 视角将 Object（对象）视为一个功能实体，而非具有形态和质量的物理 Entity（实体）。功能实体在使用时会执行某些活动。

常言道 "形式追随功能"（form follows function）。将 "Functional" 视角与 "Physical"（物理）视角分离，可以独立地对 "形式" 和 "功能" 进行建模。功能建模/规划可以先于物理建模进行，并由不同的责任方处理。通常有多个物理 Entity 可以实现给定的功能。特定的物理 Entity 可能在整个设计过程中逐步细化，也可能在 Object 运营期间发生变化。

Functional Modeling Perspective 是抽象的。领域作者应该特化 FunctionalPartition、FunctionalModel 以及 FunctionalElement 的一个或多个子类，以表达其学科在功能建模方面的特定需求，例如建筑功能规划或工厂流程建模。

## 目录

- Entity Classes（实体类）
  - FunctionalBreakdownElement
  - FunctionalComponentElement
  - FunctionalComposite
  - FunctionalElement
  - FunctionalModel
  - FunctionalPartition
  - FunctionalPortion
  - FunctionalType
- Relationship Classes（关系类）
  - DrawingGraphicRepresentsFunctionalElement
  - FunctionalElementIsOfType
  - PhysicalElementFulfillsFunction

## Entity Classes

### __FunctionalBreakdownElement__ (Functional Breakdown) _Abstract_ EntityClass

func:FunctionalBreakdownElement 对聚合功能 Entity 进行建模，其子 func:FunctionalElements 对其各个部分进行建模。

__Base Class:__ Functional:FunctionalElement

继承属性

| Name | Description | Type | Extended Type |
| --- | --- | --- | --- |
| Model | 包含此 bis:Element 的 bis:Model。 | navigation |  |
| LastMod | bis:Element 的最后修改时间。此属性由核心框架维护，应用程序不应直接设置。 | dateTime |  |
| CodeSpec | CodeSpec 属性标识用于生成和验证此 bis:Element 代码值的 bis:CodeSpec。每个 bis:Element 实例的 CodeSpec、CodeScope 和 CodeValue 属性组合必须唯一。 | navigation |  |
| CodeScope | CodeScope 属性标识为代码值提供唯一性作用域的 bis:Element。每个 bis:Element 实例的 CodeSpec、CodeScope 和 CodeValue 属性组合必须唯一。 | navigation |  |
| CodeValue | 可空字符串属性，保存 Element 的 Code 的实际文本。每个 bis:Element 实例的 CodeSpec、CodeScope 和 CodeValue 属性组合必须唯一。 | string |  |
| UserLabel | 用户给定的可选友好名称（与存储在 CodeValue 属性中的正式名称相对）。 | string |  |
| Parent | 拥有此 bis:Element 的父 bis:Element。 | navigation |  |
| FederationGuid | 用于跨仓库联合此 bis:Element 的 GUID。 | binary | BeGuid |
| JsonProperties | 用户和/或应用程序可用于持久化临时 JSON 值的字符串属性。 | string | Json |
| TypeDefinition |  | navigation |  |

FunctionalBreakdownElement 和 FunctionalComponentElement 旨在一起使用，采用一种不使用 sub-models（子模型）的功能建模风格。如果您使用 sub-modeling，请直接特化 `FunctionalElement`。

### __FunctionalComponentElement__ (Functional Component) _Abstract_ EntityClass

func:FunctionalComponentElement 对 "原子" 功能 Entity 进行建模，该实体不会被更细粒度地建模，也没有 "子" 部分。

__Base Class:__ Functional:FunctionalElement

继承属性

| Name | Description | Type | Extended Type |
| --- | --- | --- | --- |
| Model | 包含此 bis:Element 的 bis:Model。 | navigation |  |
| LastMod | bis:Element 的最后修改时间。此属性由核心框架维护，应用程序不应直接设置。 | dateTime |  |
| CodeSpec | CodeSpec 属性标识用于生成和验证此 bis:Element 代码值的 bis:CodeSpec。每个 bis:Element 实例的 CodeSpec、CodeScope 和 CodeValue 属性组合必须唯一。 | navigation |  |
| CodeScope | CodeScope 属性标识为代码值提供唯一性作用域的 bis:Element。每个 bis:Element 实例的 CodeSpec、CodeScope 和 CodeValue 属性组合必须唯一。 | navigation |  |
| CodeValue | 可空字符串属性，保存 Element 的 Code 的实际文本。每个 bis:Element 实例的 CodeSpec、CodeScope 和 CodeValue 属性组合必须唯一。 | string |  |
| UserLabel | 用户给定的可选友好名称（与存储在 CodeValue 属性中的正式名称相对）。 | string |  |
| Parent | 拥有此 bis:Element 的父 bis:Element。 | navigation |  |
| FederationGuid | 用于跨仓库联合此 bis:Element 的 GUID。 | binary | BeGuid |
| JsonProperties | 用户和/或应用程序可用于持久化临时 JSON 值的字符串属性。 | string | Json |
| TypeDefinition |  | navigation |  |

FunctionalComponentElement 和 FunctionalBreakdownElement 旨在一起使用，采用一种不使用 sub-models 的功能建模风格。如果您使用 sub-modeling，请直接特化 `FunctionalElement`。

### __FunctionalComposite__ (Functional Composite) EntityClass _已弃用_

现在的最佳实践是从 FunctionalBreakdownElement 继承。

已弃用：请改为从 FunctionalBreakdownElement 继承。

__Base Class:__ Functional:FunctionalBreakdownElement

继承属性

| Name | Description | Type | Extended Type |
| --- | --- | --- | --- |
| Model | 包含此 bis:Element 的 bis:Model。 | navigation |  |
| LastMod | bis:Element 的最后修改时间。此属性由核心框架维护，应用程序不应直接设置。 | dateTime |  |
| CodeSpec | CodeSpec 属性标识用于生成和验证此 bis:Element 代码值的 bis:CodeSpec。每个 bis:Element 实例的 CodeSpec、CodeScope 和 CodeValue 属性组合必须唯一。 | navigation |  |
| CodeScope | CodeScope 属性标识为代码值提供唯一性作用域的 bis:Element。每个 bis:Element 实例的 CodeSpec、CodeScope 和 CodeValue 属性组合必须唯一。 | navigation |  |
| CodeValue | 可空字符串属性，保存 Element 的 Code 的实际文本。每个 bis:Element 实例的 CodeSpec、CodeScope 和 CodeValue 属性组合必须唯一。 | string |  |
| UserLabel | 用户给定的可选友好名称（与存储在 CodeValue 属性中的正式名称相对）。 | string |  |
| Parent | 拥有此 bis:Element 的父 bis:Element。 | navigation |  |
| FederationGuid | 用于跨仓库联合此 bis:Element 的 GUID。 | binary | BeGuid |
| JsonProperties | 用户和/或应用程序可用于持久化临时 JSON 值的字符串属性。 | string | Json |
| TypeDefinition |  | navigation |  |

### __FunctionalElement__ (Functional Element) _Abstract_ EntityClass

func:FunctionalElement 对最终由物理 Entity 实现的所需功能进行建模。

__Base Class:__ BisCore:RoleElement

对特定功能 Entity 进行建模——即在使用时会执行特定活动的事物。功能 Entity 本质上是非几何的，被视为 Object 所扮演的 "角色"（roles）。

#### Properties

| Name | Description | Type | Extended Type |
| --- | --- | --- | --- |
| TypeDefinition |  | navigation |  |

继承属性

| Name | Description | Type | Extended Type |
| --- | --- | --- | --- |
| Model | 包含此 bis:Element 的 bis:Model。 | navigation |  |
| LastMod | bis:Element 的最后修改时间。此属性由核心框架维护，应用程序不应直接设置。 | dateTime |  |
| CodeSpec | CodeSpec 属性标识用于生成和验证此 bis:Element 代码值的 bis:CodeSpec。每个 bis:Element 实例的 CodeSpec、CodeScope 和 CodeValue 属性组合必须唯一。 | navigation |  |
| CodeScope | CodeScope 属性标识为代码值提供唯一性作用域的 bis:Element。每个 bis:Element 实例的 CodeSpec、CodeScope 和 CodeValue 属性组合必须唯一。 | navigation |  |
| CodeValue | 可空字符串属性，保存 Element 的 Code 的实际文本。每个 bis:Element 实例的 CodeSpec、CodeScope 和 CodeValue 属性组合必须唯一。 | string |  |
| UserLabel | 用户给定的可选友好名称（与存储在 CodeValue 属性中的正式名称相对）。 | string |  |
| Parent | 拥有此 bis:Element 的父 bis:Element。 | navigation |  |
| FederationGuid | 用于跨仓库联合此 bis:Element 的 GUID。 | binary | BeGuid |
| JsonProperties | 用户和/或应用程序可用于持久化临时 JSON 值的字符串属性。 | string | Json |

### __FunctionalModel__ (Functional Model) EntityClass

用于持久化 func:FunctionalElement 实例的容器。

__Base Class:__ BisCore:RoleModel

继承属性

| Name | Description | Type | Extended Type |
| --- | --- | --- | --- |
| ParentModel | 父 bis:Model 包含此 bis:Model 正在建模的 bis:Element。 | navigation |  |
| ModeledElement | 此 bis:Model 正在建模的 bis:Element。此 bis:Model 与被建模的 bis:Element 建模同一个 Entity，但粒度更细。 | navigation |  |
| IsPrivate | 如果 IsPrivate 为 true，则此 bis:Model 不应出现在向用户显示的列表中。 | boolean |  |
| IsTemplate | 如果 IsTemplate 为 true，则此 bis:Model 用作创建新实例的模板。 | boolean |  |
| JsonProperties | 用户和/或应用程序可用于持久化临时 JSON 值的字符串属性。 | string | Json |
| LastMod | 此 Model 中任何 Element 的最后修改时间。 | dateTime |  |

应被视为抽象的。它应该被特化以容纳特定学科的功能 Elements。

### __FunctionalPartition__ (Functional Partition) EntityClass

func:FunctionalPartition 元素为其父 bis:Subject 建立 "Functional" 建模视角。它旨在被特化，应被视为 "抽象的"。

__Base Class:__ BisCore:InformationPartitionElement

继承属性

| Name | Description | Type | Extended Type |
| --- | --- | --- | --- |
| Model | 包含此 bis:Element 的 bis:Model。 | navigation |  |
| LastMod | bis:Element 的最后修改时间。此属性由核心框架维护，应用程序不应直接设置。 | dateTime |  |
| CodeSpec | CodeSpec 属性标识用于生成和验证此 bis:Element 代码值的 bis:CodeSpec。每个 bis:Element 实例的 CodeSpec、CodeScope 和 CodeValue 属性组合必须唯一。 | navigation |  |
| CodeScope | CodeScope 属性标识为代码值提供唯一性作用域的 bis:Element。每个 bis:Element 实例的 CodeSpec、CodeScope 和 CodeValue 属性组合必须唯一。 | navigation |  |
| CodeValue | 可空字符串属性，保存 Element 的 Code 的实际文本。每个 bis:Element 实例的 CodeSpec、CodeScope 和 CodeValue 属性组合必须唯一。 | string |  |
| UserLabel | 用户给定的可选友好名称（与存储在 CodeValue 属性中的正式名称相对）。 | string |  |
| Parent | 拥有此 bis:Element 的父 bis:Element。 | navigation |  |
| FederationGuid | 用于跨仓库联合此 bis:Element 的 GUID。 | binary | BeGuid |
| JsonProperties | 用户和/或应用程序可用于持久化临时 JSON 值的字符串属性。 | string | Json |
| Description | 描述分区背后意图的人类可读字符串。 | string |  |

func:FunctionalPartition 元素为其父 bis:Subject 建立 "Functional" 建模视角。它旨在被特化，应被视为 "抽象的"。

有关 "Functional" 建模视角的定义，请参阅 Functional。

### __FunctionalPortion__ (Functional Portion) EntityClass _已弃用_

现在的最佳实践是从 FunctionalComponentElement 子类继承，并在需要分解概念时混入 ISubModeledElement。

已弃用：Functional Portion 是一个 Functional Component，它将在单独的（子）Functional Model 中被更详细地分解。

__Base Class:__ Functional:FunctionalComponentElement

继承属性

| Name | Description | Type | Extended Type |
| --- | --- | --- | --- |
| Model | 包含此 bis:Element 的 bis:Model。 | navigation |  |
| LastMod | bis:Element 的最后修改时间。此属性由核心框架维护，应用程序不应直接设置。 | dateTime |  |
| CodeSpec | CodeSpec 属性标识用于生成和验证此 bis:Element 代码值的 bis:CodeSpec。每个 bis:Element 实例的 CodeSpec、CodeScope 和 CodeValue 属性组合必须唯一。 | navigation |  |
| CodeScope | CodeScope 属性标识为代码值提供唯一性作用域的 bis:Element。每个 bis:Element 实例的 CodeSpec、CodeScope 和 CodeValue 属性组合必须唯一。 | navigation |  |
| CodeValue | 可空字符串属性，保存 Element 的 Code 的实际文本。每个 bis:Element 实例的 CodeSpec、CodeScope 和 CodeValue 属性组合必须唯一。 | string |  |
| UserLabel | 用户给定的可选友好名称（与存储在 CodeValue 属性中的正式名称相对）。 | string |  |
| Parent | 拥有此 bis:Element 的父 bis:Element。 | navigation |  |
| FederationGuid | 用于跨仓库联合此 bis:Element 的 GUID。 | binary | BeGuid |
| JsonProperties | 用户和/或应用程序可用于持久化临时 JSON 值的字符串属性。 | string | Json |
| TypeDefinition |  | navigation |  |

### __FunctionalType__ (Functional Type) _Abstract_ EntityClass

定义可与 func:FunctionalElement 关联的一组共享属性（即 "类型"）。

__Base Class:__ BisCore:TypeDefinitionElement

继承属性

| Name | Description | Type | Extended Type |
| --- | --- | --- | --- |
| Model | 包含此 bis:Element 的 bis:Model。 | navigation |  |
| LastMod | bis:Element 的最后修改时间。此属性由核心框架维护，应用程序不应直接设置。 | dateTime |  |
| CodeSpec | CodeSpec 属性标识用于生成和验证此 bis:Element 代码值的 bis:CodeSpec。每个 bis:Element 实例的 CodeSpec、CodeScope 和 CodeValue 属性组合必须唯一。 | navigation |  |
| CodeScope | CodeScope 属性标识为代码值提供唯一性作用域的 bis:Element。每个 bis:Element 实例的 CodeSpec、CodeScope 和 CodeValue 属性组合必须唯一。 | navigation |  |
| CodeValue | 可空字符串属性，保存 Element 的 Code 的实际文本。每个 bis:Element 实例的 CodeSpec、CodeScope 和 CodeValue 属性组合必须唯一。 | string |  |
| UserLabel | 用户给定的可选友好名称（与存储在 CodeValue 属性中的正式名称相对）。 | string |  |
| Parent | 拥有此 bis:Element 的父 bis:Element。 | navigation |  |
| FederationGuid | 用于跨仓库联合此 bis:Element 的 GUID。 | binary | BeGuid |
| JsonProperties | 用户和/或应用程序可用于持久化临时 JSON 值的字符串属性。 | string | Json |
| IsPrivate | 如果为 true，此 bis:DefinitionElement 不应在 GUI 中显示。 | boolean |  |
| Recipe |  | navigation |  |

`FunctionalElement` 的 `FunctionalType` 与可能用于实现该功能的 `PhysicalElement` 的 `PhysicalType` 是不同的。

## Relationship Classes

### __DrawingGraphicRepresentsFunctionalElement__ RelationshipClass

将 bis:DrawingGraphic 实例与其表示的 func:FunctionalElement 实例相关联。

__Base Class:__ BisCore:DrawingGraphicRepresentsElement

__Strength:__ Referencing

__Strength Direction:__ Forward

用于将原理图与 `FunctionalElement` 关联。

#### Source

__Is Polymorphic:__ true

__Role Label:__ represents

__Multiplicity:__ (0..*)

约束类：

- DrawingGraphic

#### Target

__Is Polymorphic:__ true

__Role Label:__ is represented by

__Multiplicity:__ (0..*)

约束类：

- FunctionalElement

### __FunctionalElementIsOfType__ RelationshipClass

类型-实例关系；指示特定的 func:FunctionalElement 是已定义 func:FunctionalType 的实例。

__Strength:__ Referencing

__Strength Direction:__ Forward

#### Source

__Is Polymorphic:__ true

__Role Label:__ is of type

__Multiplicity:__ (0..*)

约束类：

- FunctionalElement

#### Target

__Is Polymorphic:__ true

__Role Label:__ is type of

__Multiplicity:__ (0..1)

约束类：

- FunctionalType

### __PhysicalElementFulfillsFunction__ RelationshipClass

将 func:FunctionalElement 实例（对所需功能进行建模）与对实现该功能的物理 Entity 进行建模的 bis:PhysicalElement 实例相关联。

__Base Class:__ BisCore:ElementRefersToElements

__Strength:__ Referencing

__Strength Direction:__ Forward

可能存在其他关系（在其他地方定义），用于指示 `PhysicalElement` 可能用于实现功能的 `PhysicalType`。

#### Source

__Is Polymorphic:__ true

__Role Label:__ fulfills

__Multiplicity:__ (0..*)

约束类：

- PhysicalElement

#### Target

__Is Polymorphic:__ true

__Role Label:__ is fulfilled by

__Multiplicity:__ (0..*)

约束类：

- FunctionalElement
