# Analytical (Analytical) - iTwin.js

**Alias:** anlyt

**Version:** 1.0.1

专门化 Analytical domain schema 扩展的 BIS 类。

包含定义核心类的 schema，这些核心类被专门的 BIS Analytical Domain schema 使用，例如 Hydraulic analysis（水力分析）、Structural analysis（结构分析）、Thermal analysis（热分析）等。本 schema 不涵盖 Analytical Results（分析结果）或 Scenario Analysis（情景分析），这些将在未来单独处理。

每个专门的 BIS Analytical Domain 预期引入以下类的子类：anlyt:AnalyticalPartition、anlyt:AnalyticalModel、anlyt:AnalyticalElement，以及如果需要的话，anlyt:AnalyticalType。

## 目录

- Entity Classes
  - AnalyticalElement
  - AnalyticalModel
  - AnalyticalPartition
  - AnalyticalType
- Relationship Classes
  - AnalyticalElementIsOfType
  - AnalyticalSimulatesSpatialElement

## Entity Classes

### __AnalyticalElement__ (Analytical Element) _Abstract_ EntityClass

anlyt:AnalyticalElement 在空间上定位，根据专门的分析视角模拟零个或多个 bis:SpatialLocationElement 或 bis:PhysicalElement 实例。

**Base Class:** BisCore:GeometricElement3d

继承属性

| Name | Description | Type | Extended Type |
| --- | --- | --- | --- |
| Model | 包含此 bis:Element 的 bis:Model。 | navigation |  |
| LastMod | bis:Element 的最后修改时间。此属性由核心框架维护，应用程序不应直接设置。 | dateTime |  |
| CodeSpec | CodeSpec 属性标识用于生成和验证此 bis:Element 代码值的 bis:CodeSpec。CodeSpec、CodeScope 和 CodeValue 属性的组合对每个 bis:Element 实例必须是唯一的。 | navigation |  |
| CodeScope | CodeScope 属性标识为代码值提供唯一性作用域的 bis:Element。CodeSpec、CodeScope 和 CodeValue 属性的组合对每个 bis:Element 实例必须是唯一的。 | navigation |  |
| CodeValue | 可空字符串属性，保存 Element 的 Code 的实际文本。CodeSpec、CodeScope 和 CodeValue 属性的组合对每个 bis:Element 实例必须是唯一的。 | string |  |
| UserLabel | 用户给出的可选友好名称（与存储在 CodeValue 属性中的正式名称相对）。 | string |  |
| Parent | 拥有此 bis:Element 的父 bis:Element。 | navigation |  |
| FederationGuid | 用于跨仓库联合此 bis:Element 的 GUID。 | binary | BeGuid |
| JsonProperties | 用户和/或应用程序可用于持久化临时 JSON 值的字符串属性。 | string | Json |
| Category | 用于对此 bis:GeometricElement3d 进行分类的 bis:SpatialCategory | navigation |  |
| InSpatialIndex | 如果为 true，此元素将在 Spatial Index 中有一个条目。 | boolean |  |
| Origin | 此 bis:Element 的放置原点。 | point3d |  |
| Yaw | 此 bis:Element 方向的 Yaw 角度（以度为单位）。 | double |  |
| Pitch | 此 bis:Element 方向的 Pitch 角度（以度为单位）。 | double |  |
| Roll | 此 bis:Element 方向的 Roll 角度（以度为单位）。 | double |  |
| BBoxLow | 此 bis:Element 的元素对齐边界框的"低"点。 | point3d |  |
| BBoxHigh | 此 bis:Element 的元素对齐边界框的"高"点。 | point3d |  |
| GeometryStream | 用于持久化此 bis:Element 几何形状的二进制流。 | binary | GeometryStream |
| TypeDefinition | 指向 TypeDefinition 某个专门化的实例，该实例保存按类型而非按此 Element 实例变化的属性值。 | navigation |  |

anlyt:AnalyticalElement 预期由专门的 BIS Analytical Domain schema 子类化。

### __AnalyticalModel__ (Analytical Model) _Abstract_ EntityClass

用于持久化 anlyt:AnalyticalElement 实例的容器，用于建模专门的分析视角。

**Base Class:** BisCore:GeometricModel3d

继承属性

| Name | Description | Type | Extended Type |
| --- | --- | --- | --- |
| ParentModel | 父 bis:Model 包含此 bis:Model 正在子建模的 bis:Element。 | navigation |  |
| ModeledElement | 此 bis:Model 正在子建模的 bis:Element。此 bis:Model 与子 Modeled bis:Element 建模相同的 Entity，但以更细的粒度。 | navigation |  |
| IsPrivate | 如果 IsPrivate 为 true，则此 bis:Model 不应出现在显示给用户的列表中。 | boolean |  |
| IsTemplate | 如果 IsTemplate 为 true，则此 bis:Model 用作创建新实例的模板。 | boolean |  |
| JsonProperties | 用户和/或应用程序可用于持久化临时 JSON 值的字符串属性。 | string | Json |
| LastMod | 此 Model 中任何元素最后一次修改的时间。 | dateTime |  |
| GeometryGuid | 当此 GeometricModel 中的任何元素的几何形状发生变化时更改的 GUID。 | binary | BeGuid |
| IsNotSpatiallyLocated | 如果 IsNotSpatiallyLocated 为 true，则此 bis:GeometricModel3d 中的元素不在现实世界坐标中，也不会在空间索引中。 | boolean |  |
| IsPlanProjection | 如果 IsPlanProjection 为 true，则此 bis:GeometricModel3d 中的元素预期在 XY 平面中。 | boolean |  |

anlyt:AnalyticalModel 预期由专门的 BIS Analytical Domain schema 子类化。

### __AnalyticalPartition__ (Analytical Partition) _Abstract_ EntityClass

anlyt:AnalyticalPartition 元素表示在整体信息层次结构中存在专门的分析视角。anlyt:AnalyticalPartition 子类始终以 bis:Subject 为父级，并由 anlyt:AnalyticalModel 进行分解。

**Base Class:** BisCore:InformationPartitionElement

继承属性

| Name | Description | Type | Extended Type |
| --- | --- | --- | --- |
| Model | 包含此 bis:Element 的 bis:Model。 | navigation |  |
| LastMod | bis:Element 的最后修改时间。此属性由核心框架维护，应用程序不应直接设置。 | dateTime |  |
| CodeSpec | CodeSpec 属性标识用于生成和验证此 bis:Element 代码值的 bis:CodeSpec。CodeSpec、CodeScope 和 CodeValue 属性的组合对每个 bis:Element 实例必须是唯一的。 | navigation |  |
| CodeScope | CodeScope 属性标识为代码值提供唯一性作用域的 bis:Element。CodeSpec、CodeScope 和 CodeValue 属性的组合对每个 bis:Element 实例必须是唯一的。 | navigation |  |
| CodeValue | 可空字符串属性，保存 Element 的 Code 的实际文本。CodeSpec、CodeScope 和 CodeValue 属性的组合对每个 bis:Element 实例必须是唯一的。 | string |  |
| UserLabel | 用户给出的可选友好名称（与存储在 CodeValue 属性中的正式名称相对）。 | string |  |
| Parent | 拥有此 bis:Element 的父 bis:Element。 | navigation |  |
| FederationGuid | 用于跨仓库联合此 bis:Element 的 GUID。 | binary | BeGuid |
| JsonProperties | 用户和/或应用程序可用于持久化临时 JSON 值的字符串属性。 | string | Json |
| Description | 描述 partition 意图的人类可读字符串。 | string |  |

anlyt:AnalyticalPartition 预期由专门的 BIS Analytical Domain schema 子类化。

### __AnalyticalType__ (Analytical Type) _Abstract_ EntityClass

定义可以与 anlyt:AnalyticalElement 关联的一组共享属性（"类型"）。它不是为了替换 bis:PhysicalType（如果可用的话）。

**Base Class:** BisCore:TypeDefinitionElement

继承属性

| Name | Description | Type | Extended Type |
| --- | --- | --- | --- |
| Model | 包含此 bis:Element 的 bis:Model。 | navigation |  |
| LastMod | bis:Element 的最后修改时间。此属性由核心框架维护，应用程序不应直接设置。 | dateTime |  |
| CodeSpec | CodeSpec 属性标识用于生成和验证此 bis:Element 代码值的 bis:CodeSpec。CodeSpec、CodeScope 和 CodeValue 属性的组合对每个 bis:Element 实例必须是唯一的。 | navigation |  |
| CodeScope | CodeScope 属性标识为代码值提供唯一性作用域的 bis:Element。CodeSpec、CodeScope 和 CodeValue 属性的组合对每个 bis:Element 实例必须是唯一的。 | navigation |  |
| CodeValue | 可空字符串属性，保存 Element 的 Code 的实际文本。CodeSpec、CodeScope 和 CodeValue 属性的组合对每个 bis:Element 实例必须是唯一的。 | string |  |
| UserLabel | 用户给出的可选友好名称（与存储在 CodeValue 属性中的正式名称相对）。 | string |  |
| Parent | 拥有此 bis:Element 的父 bis:Element。 | navigation |  |
| FederationGuid | 用于跨仓库联合此 bis:Element 的 GUID。 | binary | BeGuid |
| JsonProperties | 用户和/或应用程序可用于持久化临时 JSON 值的字符串属性。 | string | Json |
| IsPrivate | 如果为 true，此 bis:DefinitionElement 不应在 GUI 中显示。 | boolean |  |
| Recipe |  | navigation |  |

anlyt:AnalyticalType 可以由专门的 BIS Analytical Domain schema 可选地子类化。它不是为了替换更适合由 bis:PhysicalType 覆盖的情况，而是用专门分析所需的数据来增强它。例如，analytical pump 应该引用 physical pump type，并用专门分析所需的数据来增强它。在 Hydraulic Analysis（水力分析）的情况下，例如，这样的数据可能包括覆盖 Operating Pump Curves（运行泵曲线）的类。

要在 Hydrological analysis（水文分析）中使用的 Storm Events（风暴事件）目录是一个例子，在这种情况下，引入 anlyt:AnalyticalType 的子类更合适。

## Relationship Classes

### __AnalyticalElementIsOfType__ RelationshipClass

类型-实例关系；表示特定的 anlyt:AnalyticalElement 是定义的 anlyt:AnalyticalType 的实例。

**Base Class:** BisCore:GeometricElement3dHasTypeDefinition

**Strength:** Referencing

**Strength Direction:** Forward

它旨在用于关联不适合由 bis:PhysicalType 实例表示的 anlyt:AnalyticalType 实例。例如，在 Hydrological Analysis 中使用的 analytical Storm 实例的类型是 N-years Storm Event。

#### Source

**Is Polymorphic:** true

**Role Label:** is of type

**Multiplicity:** (0..*)

#### Constraint Classes:

- AnalyticalElement

#### Target

**Is Polymorphic:** true

**Role Label:** is type of

**Multiplicity:** (0..1)

#### Constraint Classes:

- AnalyticalType

### __AnalyticalSimulatesSpatialElement__ RelationshipClass

将 anlyt:AnalyticalElement 与其模拟的 bis:SpatialLocationElement 或 bis:PhysicalElement 关联，基于专门的分析视角。

**Base Class:** BisCore:ElementRefersToElements

**Strength:** Referencing

**Strength Direction:** Forward

例如，Hydraulic analysis 中的 analytical pump station 可以与其模拟的所有 physical pumps 相关联。

#### Source

**Is Polymorphic:** true

**Role Label:** simulates

**Multiplicity:** (0..*)

#### Constraint Classes:

- AnalyticalElement

#### Target

**Is Polymorphic:** true

**Role Label:** is simulated by

**Multiplicity:** (0..*)

#### Constraint Classes:

- SpatialElement

---

## 参考来源

- [Analytical (Analytical) - iTwin.js](https://www.itwinjs.org/bis/domains/analytical.ecschema/)
