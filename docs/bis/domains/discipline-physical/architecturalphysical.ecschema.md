# ArchitecturalPhysical ECSchema

**别名 (Alias):** ArchPhys

**版本 (Version):** 1.0.3

## 概述

Architectural Physical Schema（建筑物理 Schema）包含用于建模建筑学科中物理元素的具体类。

该 Schema 还包含所有类的 `PhysicalTypes`。但需要注意的是，并非所有 `bis:PhysicalElement` 的子类都应该有 PhysicalType。请参阅 PhysicalType 文档以了解更多信息。

## 目录

- [实体类 (Entity Classes)](#实体类-entity-classes)
  - [Casework](#casework)
  - [CaseworkType](#caseworktype)
  - [Ceiling](#ceiling)
  - [CeilingType](#ceilingtype)
  - [CurtainWall](#curtainwall)
  - [CurtainWallType](#curtainwalltype)
  - [Door](#door)
  - [DoorType](#doortype)
  - [Floor](#floor)
  - [FloorType](#floortype)
  - [Furniture](#furniture)
  - [FurnitureType](#furnituretype)
  - [Railing](#railing)
  - [RailingType](#railingtype)
  - [Ramp](#ramp)
  - [RampType](#ramptype)
  - [Roof](#roof)
  - [RoofType](#rooftype)
  - [Stair](#stair)
  - [StairType](#stairtype)
  - [TransportationMechanism](#transportationmechanism)
  - [TransportationMechanismType](#transportationmechanismtype)
  - [Wall](#wall)
  - [WallLeaf](#wallleaf)
  - [WallLeafType](#wallleaftype)
  - [WallType](#walltype)
  - [Window](#window)
  - [WindowType](#windowtype)
- [关系类 (Relationship Classes)](#关系类-relationship-classes)
  - [CaseworkIsOfType](#caseworkisoftype)
  - [CeilingIsOfType](#ceilingisoftype)
  - [CurtainWallIsOfType](#curtainwallisoftype)
  - [DoorIsOfType](#doorisoftype)
  - [FloorIsOfType](#floorisoftype)
  - [FurnitureIsOfType](#furnitureisoftype)
  - [RailingIsOfType](#railingisoftype)
  - [RampIsOfType](#rampisoftype)
  - [RoofIsOfType](#roofisoftype)
  - [StairIsOfType](#stairisoftype)
  - [TransportationMechanismIsOfType](#transportationmechanismisoftype)
  - [WallIsOfType](#wallisoftype)
  - [WallLeafIsOfType](#wallleafisoftype)
  - [WallOwnsWallLeafs](#wallownswalleafs)
  - [WindowIsOfType](#windowisoftype)

---

## 实体类 (Entity Classes)

### Casework

**基类 (Base Class):** BisCore:PhysicalElement

Casework（柜体/细木工）表示建筑中的柜类元素。

#### 继承属性 (Inherited Properties)

| 名称 | 描述 | 类型 | 扩展类型 |
| --- | --- | --- | --- |
| Model | 包含此 bis:Element 的 bis:Model。 | navigation |  |
| LastMod | bis:Element 的最后修改时间。由核心框架维护，不应由应用程序直接设置。 | dateTime |  |
| CodeSpec | CodeSpec 属性标识用于生成和验证此 bis:Element 代码值的 bis:CodeSpec。CodeSpec、CodeScope 和 CodeValue 属性的组合对于每个 bis:Element 实例必须是唯一的。 | navigation |  |
| CodeScope | CodeScope 属性标识为代码值提供唯一性范围的 bis:Element。CodeSpec、CodeScope 和 CodeValue 属性的组合对于每个 bis:Element 实例必须是唯一的。 | navigation |  |
| CodeValue | 可空字符串属性，保存 Element 代码的实际文本。CodeSpec、CodeScope 和 CodeValue 属性的组合对于每个 bis:Element 实例必须是唯一的。 | string |  |
| UserLabel | 用户给出的可选友好名称（与存储在 CodeValue 属性中的正式名称相对）。 | string |  |
| Parent | 拥有此 bis:Element 的父 bis:Element。 | navigation |  |
| FederationGuid | 用于跨存储库联合此 bis:Element 的 GUID。 | binary | BeGuid |
| JsonProperties | 用户和/或应用程序可用于持久化临时 JSON 值的字符串属性。 | string | Json |
| Category | 用于对此 bis:GeometricElement3d 进行分类的 bis:SpatialCategory | navigation |  |
| InSpatialIndex | 如果为 true，则此元素将在空间索引中有一个条目。 | boolean |  |
| Origin | 此 bis:Element 的放置原点。 | point3d |  |
| Yaw | 此 bis:Element 方向的偏航角（以度为单位）。 | double |  |
| Pitch | 此 bis:Element 方向的俯仰角（以度为单位）。 | double |  |
| Roll | 此 bis:Element 方向的翻滚角（以度为单位）。 | double |  |
| BBoxLow | 此 bis:Element 的元素对齐边界框的"低"点。 | point3d |  |
| BBoxHigh | 此 bis:Element 的元素对齐边界框的"高"点。 | point3d |  |
| GeometryStream | 用于持久化此 bis:Element 几何图形的二进制流。 | binary | GeometryStream |
| TypeDefinition | 指向 TypeDefinition 的某个特化实例，该实例保存按类型而非按此 Element 实例变化的属性值。 | navigation |  |
| PhysicalMaterial | 指示 bis:PhysicalElement 所用材料对应的 bis:PhysicalMaterial。 | navigation |  |

---

### CaseworkType

**显示名称:** Casework Type

**基类 (Base Class):** BisCore:PhysicalType

通过关联用户可定义的自定义 Type，进一步特化 Casework 的特定子类。

#### 继承属性 (Inherited Properties)

| 名称 | 描述 | 类型 | 扩展类型 |
| --- | --- | --- | --- |
| Model | 包含此 bis:Element 的 bis:Model。 | navigation |  |
| LastMod | bis:Element 的最后修改时间。由核心框架维护，不应由应用程序直接设置。 | dateTime |  |
| CodeSpec | CodeSpec 属性标识用于生成和验证此 bis:Element 代码值的 bis:CodeSpec。CodeSpec、CodeScope 和 CodeValue 属性的组合对于每个 bis:Element 实例必须是唯一的。 | navigation |  |
| CodeScope | CodeScope 属性标识为代码值提供唯一性范围的 bis:Element。CodeSpec、CodeScope 和 CodeValue 属性的组合对于每个 bis:Element 实例必须是唯一的。 | navigation |  |
| CodeValue | 可空字符串属性，保存 Element 代码的实际文本。CodeSpec、CodeScope 和 CodeValue 属性的组合对于每个 bis:Element 实例必须是唯一的。 | string |  |
| UserLabel | 用户给出的可选友好名称（与存储在 CodeValue 属性中的正式名称相对）。 | string |  |
| Parent | 拥有此 bis:Element 的父 bis:Element。 | navigation |  |
| FederationGuid | 用于跨存储库联合此 bis:Element 的 GUID。 | binary | BeGuid |
| JsonProperties | 用户和/或应用程序可用于持久化临时 JSON 值的字符串属性。 | string | Json |
| IsPrivate | 如果为 true，则此 bis:DefinitionElement 不应在 GUI 中显示。 | boolean |  |
| Recipe |  | navigation |  |
| PhysicalMaterial | 指示给定 bis:PhysicalType 的 bis:PhysicalElements 所用材料对应的 bis:PhysicalMaterial。 | navigation |  |

---

### Ceiling

**基类 (Base Class):** BisCore:PhysicalElement

Ceiling（天花板）表示建筑中的顶部覆盖元素。

#### 继承属性 (Inherited Properties)

| 名称 | 描述 | 类型 | 扩展类型 |
| --- | --- | --- | --- |
| Model | 包含此 bis:Element 的 bis:Model。 | navigation |  |
| LastMod | bis:Element 的最后修改时间。由核心框架维护，不应由应用程序直接设置。 | dateTime |  |
| CodeSpec | CodeSpec 属性标识用于生成和验证此 bis:Element 代码值的 bis:CodeSpec。CodeSpec、CodeScope 和 CodeValue 属性的组合对于每个 bis:Element 实例必须是唯一的。 | navigation |  |
| CodeScope | CodeScope 属性标识为代码值提供唯一性范围的 bis:Element。CodeSpec、CodeScope 和 CodeValue 属性的组合对于每个 bis:Element 实例必须是唯一的。 | navigation |  |
| CodeValue | 可空字符串属性，保存 Element 代码的实际文本。CodeSpec、CodeScope 和 CodeValue 属性的组合对于每个 bis:Element 实例必须是唯一的。 | string |  |
| UserLabel | 用户给出的可选友好名称（与存储在 CodeValue 属性中的正式名称相对）。 | string |  |
| Parent | 拥有此 bis:Element 的父 bis:Element。 | navigation |  |
| FederationGuid | 用于跨存储库联合此 bis:Element 的 GUID。 | binary | BeGuid |
| JsonProperties | 用户和/或应用程序可用于持久化临时 JSON 值的字符串属性。 | string | Json |
| Category | 用于对此 bis:GeometricElement3d 进行分类的 bis:SpatialCategory | navigation |  |
| InSpatialIndex | 如果为 true，则此元素将在空间索引中有一个条目。 | boolean |  |
| Origin | 此 bis:Element 的放置原点。 | point3d |  |
| Yaw | 此 bis:Element 方向的偏航角（以度为单位）。 | double |  |
| Pitch | 此 bis:Element 方向的俯仰角（以度为单位）。 | double |  |
| Roll | 此 bis:Element 方向的翻滚角（以度为单位）。 | double |  |
| BBoxLow | 此 bis:Element 的元素对齐边界框的"低"点。 | point3d |  |
| BBoxHigh | 此 bis:Element 的元素对齐边界框的"高"点。 | point3d |  |
| GeometryStream | 用于持久化此 bis:Element 几何图形的二进制流。 | binary | GeometryStream |
| TypeDefinition | 指向 TypeDefinition 的某个特化实例，该实例保存按类型而非按此 Element 实例变化的属性值。 | navigation |  |
| PhysicalMaterial | 指示 bis:PhysicalElement 所用材料对应的 bis:PhysicalMaterial。 | navigation |  |

---

### CeilingType

**显示名称:** Ceiling Type

**基类 (Base Class):** BisCore:PhysicalType

通过关联用户可定义的自定义 Type，进一步特化 Ceiling 的特定子类。

#### 继承属性 (Inherited Properties)

| 名称 | 描述 | 类型 | 扩展类型 |
| --- | --- | --- | --- |
| Model | 包含此 bis:Element 的 bis:Model。 | navigation |  |
| LastMod | bis:Element 的最后修改时间。由核心框架维护，不应由应用程序直接设置。 | dateTime |  |
| CodeSpec | CodeSpec 属性标识用于生成和验证此 bis:Element 代码值的 bis:CodeSpec。CodeSpec、CodeScope 和 CodeValue 属性的组合对于每个 bis:Element 实例必须是唯一的。 | navigation |  |
| CodeScope | CodeScope 属性标识为代码值提供唯一性范围的 bis:Element。CodeSpec、CodeScope 和 CodeValue 属性的组合对于每个 bis:Element 实例必须是唯一的。 | navigation |  |
| CodeValue | 可空字符串属性，保存 Element 代码的实际文本。CodeSpec、CodeScope 和 CodeValue 属性的组合对于每个 bis:Element 实例必须是唯一的。 | string |  |
| UserLabel | 用户给出的可选友好名称（与存储在 CodeValue 属性中的正式名称相对）。 | string |  |
| Parent | 拥有此 bis:Element 的父 bis:Element。 | navigation |  |
| FederationGuid | 用于跨存储库联合此 bis:Element 的 GUID。 | binary | BeGuid |
| JsonProperties | 用户和/或应用程序可用于持久化临时 JSON 值的字符串属性。 | string | Json |
| IsPrivate | 如果为 true，则此 bis:DefinitionElement 不应在 GUI 中显示。 | boolean |  |
| Recipe |  | navigation |  |
| PhysicalMaterial | 指示给定 bis:PhysicalType 的 bis:PhysicalElements 所用材料对应的 bis:PhysicalMaterial。 | navigation |  |

---

### CurtainWall

**显示名称:** Curtain Wall

**基类 (Base Class):** BisCore:PhysicalElement

CurtainWall（幕墙）表示建筑中的非承重外墙系统，通常由金属框架和玻璃或轻质面板组成。

#### 继承属性 (Inherited Properties)

| 名称 | 描述 | 类型 | 扩展类型 |
| --- | --- | --- | --- |
| Model | 包含此 bis:Element 的 bis:Model。 | navigation |  |
| LastMod | bis:Element 的最后修改时间。由核心框架维护，不应由应用程序直接设置。 | dateTime |  |
| CodeSpec | CodeSpec 属性标识用于生成和验证此 bis:Element 代码值的 bis:CodeSpec。CodeSpec、CodeScope 和 CodeValue 属性的组合对于每个 bis:Element 实例必须是唯一的。 | navigation |  |
| CodeScope | CodeScope 属性标识为代码值提供唯一性范围的 bis:Element。CodeSpec、CodeScope 和 CodeValue 属性的组合对于每个 bis:Element 实例必须是唯一的。 | navigation |  |
| CodeValue | 可空字符串属性，保存 Element 代码的实际文本。CodeSpec、CodeScope 和 CodeValue 属性的组合对于每个 bis:Element 实例必须是唯一的。 | string |  |
| UserLabel | 用户给出的可选友好名称（与存储在 CodeValue 属性中的正式名称相对）。 | string |  |
| Parent | 拥有此 bis:Element 的父 bis:Element。 | navigation |  |
| FederationGuid | 用于跨存储库联合此 bis:Element 的 GUID。 | binary | BeGuid |
| JsonProperties | 用户和/或应用程序可用于持久化临时 JSON 值的字符串属性。 | string | Json |
| Category | 用于对此 bis:GeometricElement3d 进行分类的 bis:SpatialCategory | navigation |  |
| InSpatialIndex | 如果为 true，则此元素将在空间索引中有一个条目。 | boolean |  |
| Origin | 此 bis:Element 的放置原点。 | point3d |  |
| Yaw | 此 bis:Element 方向的偏航角（以度为单位）。 | double |  |
| Pitch | 此 bis:Element 方向的俯仰角（以度为单位）。 | double |  |
| Roll | 此 bis:Element 方向的翻滚角（以度为单位）。 | double |  |
| BBoxLow | 此 bis:Element 的元素对齐边界框的"低"点。 | point3d |  |
| BBoxHigh | 此 bis:Element 的元素对齐边界框的"高"点。 | point3d |  |
| GeometryStream | 用于持久化此 bis:Element 几何图形的二进制流。 | binary | GeometryStream |
| TypeDefinition | 指向 TypeDefinition 的某个特化实例，该实例保存按类型而非按此 Element 实例变化的属性值。 | navigation |  |
| PhysicalMaterial | 指示 bis:PhysicalElement 所用材料对应的 bis:PhysicalMaterial。 | navigation |  |

---

### CurtainWallType

**显示名称:** CurtainWall Type

**基类 (Base Class):** BisCore:PhysicalType

通过关联用户可定义的自定义 Type，进一步特化 CurtainWall 的特定子类。

#### 继承属性 (Inherited Properties)

| 名称 | 描述 | 类型 | 扩展类型 |
| --- | --- | --- | --- |
| Model | 包含此 bis:Element 的 bis:Model。 | navigation |  |
| LastMod | bis:Element 的最后修改时间。由核心框架维护，不应由应用程序直接设置。 | dateTime |  |
| CodeSpec | CodeSpec 属性标识用于生成和验证此 bis:Element 代码值的 bis:CodeSpec。CodeSpec、CodeScope 和 CodeValue 属性的组合对于每个 bis:Element 实例必须是唯一的。 | navigation |  |
| CodeScope | CodeScope 属性标识为代码值提供唯一性范围的 bis:Element。CodeSpec、CodeScope 和 CodeValue 属性的组合对于每个 bis:Element 实例必须是唯一的。 | navigation |  |
| CodeValue | 可空字符串属性，保存 Element 代码的实际文本。CodeSpec、CodeScope 和 CodeValue 属性的组合对于每个 bis:Element 实例必须是唯一的。 | string |  |
| UserLabel | 用户给出的可选友好名称（与存储在 CodeValue 属性中的正式名称相对）。 | string |  |
| Parent | 拥有此 bis:Element 的父 bis:Element。 | navigation |  |
| FederationGuid | 用于跨存储库联合此 bis:Element 的 GUID。 | binary | BeGuid |
| JsonProperties | 用户和/或应用程序可用于持久化临时 JSON 值的字符串属性。 | string | Json |
| IsPrivate | 如果为 true，则此 bis:DefinitionElement 不应在 GUI 中显示。 | boolean |  |
| Recipe |  | navigation |  |
| PhysicalMaterial | 指示给定 bis:PhysicalType 的 bis:PhysicalElements 所用材料对应的 bis:PhysicalMaterial。 | navigation |  |

---

### Door

**基类 (Base Class):** BisCore:PhysicalElement

Door（门）表示建筑中的门元素。

#### 属性 (Properties)

| 名称 | 描述 | 类型 | 扩展类型 |
| --- | --- | --- | --- |
| OverallHeight | 门的整体高度 | double |  |
| OverallWidth | 门的整体宽度 | double |  |
| Description |  | string |  |

#### 继承属性 (Inherited Properties)

| 名称 | 描述 | 类型 | 扩展类型 |
| --- | --- | --- | --- |
| Model | 包含此 bis:Element 的 bis:Model。 | navigation |  |
| LastMod | bis:Element 的最后修改时间。由核心框架维护，不应由应用程序直接设置。 | dateTime |  |
| CodeSpec | CodeSpec 属性标识用于生成和验证此 bis:Element 代码值的 bis:CodeSpec。CodeSpec、CodeScope 和 CodeValue 属性的组合对于每个 bis:Element 实例必须是唯一的。 | navigation |  |
| CodeScope | CodeScope 属性标识为代码值提供唯一性范围的 bis:Element。CodeSpec、CodeScope 和 CodeValue 属性的组合对于每个 bis:Element 实例必须是唯一的。 | navigation |  |
| CodeValue | 可空字符串属性，保存 Element 代码的实际文本。CodeSpec、CodeScope 和 CodeValue 属性的组合对于每个 bis:Element 实例必须是唯一的。 | string |  |
| UserLabel | 用户给出的可选友好名称（与存储在 CodeValue 属性中的正式名称相对）。 | string |  |
| Parent | 拥有此 bis:Element 的父 bis:Element。 | navigation |  |
| FederationGuid | 用于跨存储库联合此 bis:Element 的 GUID。 | binary | BeGuid |
| JsonProperties | 用户和/或应用程序可用于持久化临时 JSON 值的字符串属性。 | string | Json |
| Category | 用于对此 bis:GeometricElement3d 进行分类的 bis:SpatialCategory | navigation |  |
| InSpatialIndex | 如果为 true，则此元素将在空间索引中有一个条目。 | boolean |  |
| Origin | 此 bis:Element 的放置原点。 | point3d |  |
| Yaw | 此 bis:Element 方向的偏航角（以度为单位）。 | double |  |
| Pitch | 此 bis:Element 方向的俯仰角（以度为单位）。 | double |  |
| Roll | 此 bis:Element 方向的翻滚角（以度为单位）。 | double |  |
| BBoxLow | 此 bis:Element 的元素对齐边界框的"低"点。 | point3d |  |
| BBoxHigh | 此 bis:Element 的元素对齐边界框的"高"点。 | point3d |  |
| GeometryStream | 用于持久化此 bis:Element 几何图形的二进制流。 | binary | GeometryStream |
| TypeDefinition | 指向 TypeDefinition 的某个特化实例，该实例保存按类型而非按此 Element 实例变化的属性值。 | navigation |  |
| PhysicalMaterial | 指示 bis:PhysicalElement 所用材料对应的 bis:PhysicalMaterial。 | navigation |  |

---

### DoorType

**显示名称:** Door Type

**基类 (Base Class):** BisCore:PhysicalType

Door Physical Type（门物理类型）。

#### 继承属性 (Inherited Properties)

| 名称 | 描述 | 类型 | 扩展类型 |
| --- | --- | --- | --- |
| Model | 包含此 bis:Element 的 bis:Model。 | navigation |  |
| LastMod | bis:Element 的最后修改时间。由核心框架维护，不应由应用程序直接设置。 | dateTime |  |
| CodeSpec | CodeSpec 属性标识用于生成和验证此 bis:Element 代码值的 bis:CodeSpec。CodeSpec、CodeScope 和 CodeValue 属性的组合对于每个 bis:Element 实例必须是唯一的。 | navigation |  |
| CodeScope | CodeScope 属性标识为代码值提供唯一性范围的 bis:Element。CodeSpec、CodeScope 和 CodeValue 属性的组合对于每个 bis:Element 实例必须是唯一的。 | navigation |  |
| CodeValue | 可空字符串属性，保存 Element 代码的实际文本。CodeSpec、CodeScope 和 CodeValue 属性的组合对于每个 bis:Element 实例必须是唯一的。 | string |  |
| UserLabel | 用户给出的可选友好名称（与存储在 CodeValue 属性中的正式名称相对）。 | string |  |
| Parent | 拥有此 bis:Element 的父 bis:Element。 | navigation |  |
| FederationGuid | 用于跨存储库联合此 bis:Element 的 GUID。 | binary | BeGuid |
| JsonProperties | 用户和/或应用程序可用于持久化临时 JSON 值的字符串属性。 | string | Json |
| IsPrivate | 如果为 true，则此 bis:DefinitionElement 不应在 GUI 中显示。 | boolean |  |
| Recipe |  | navigation |  |
| PhysicalMaterial | 指示给定 bis:PhysicalType 的 bis:PhysicalElements 所用材料对应的 bis:PhysicalMaterial。 | navigation |  |

---

### Floor

**基类 (Base Class):** BisCore:PhysicalElement

Floor（地板/楼板）表示建筑中的水平楼板元素。

#### 继承属性 (Inherited Properties)

| 名称 | 描述 | 类型 | 扩展类型 |
| --- | --- | --- | --- |
| Model | 包含此 bis:Element 的 bis:Model。 | navigation |  |
| LastMod | bis:Element 的最后修改时间。由核心框架维护，不应由应用程序直接设置。 | dateTime |  |
| CodeSpec | CodeSpec 属性标识用于生成和验证此 bis:Element 代码值的 bis:CodeSpec。CodeSpec、CodeScope 和 CodeValue 属性的组合对于每个 bis:Element 实例必须是唯一的。 | navigation |  |
| CodeScope | CodeScope 属性标识为代码值提供唯一性范围的 bis:Element。CodeSpec、CodeScope 和 CodeValue 属性的组合对于每个 bis:Element 实例必须是唯一的。 | navigation |  |
| CodeValue | 可空字符串属性，保存 Element 代码的实际文本。CodeSpec、CodeScope 和 CodeValue 属性的组合对于每个 bis:Element 实例必须是唯一的。 | string |  |
| UserLabel | 用户给出的可选友好名称（与存储在 CodeValue 属性中的正式名称相对）。 | string |  |
| Parent | 拥有此 bis:Element 的父 bis:Element。 | navigation |  |
| FederationGuid | 用于跨存储库联合此 bis:Element 的 GUID。 | binary | BeGuid |
| JsonProperties | 用户和/或应用程序可用于持久化临时 JSON 值的字符串属性。 | string | Json |
| Category | 用于对此 bis:GeometricElement3d 进行分类的 bis:SpatialCategory | navigation |  |
| InSpatialIndex | 如果为 true，则此元素将在空间索引中有一个条目。 | boolean |  |
| Origin | 此 bis:Element 的放置原点。 | point3d |  |
| Yaw | 此 bis:Element 方向的偏航角（以度为单位）。 | double |  |
| Pitch | 此 bis:Element 方向的俯仰角（以度为单位）。 | double |  |
| Roll | 此 bis:Element 方向的翻滚角（以度为单位）。 | double |  |
| BBoxLow | 此 bis:Element 的元素对齐边界框的"低"点。 | point3d |  |
| BBoxHigh | 此 bis:Element 的元素对齐边界框的"高"点。 | point3d |  |
| GeometryStream | 用于持久化此 bis:Element 几何图形的二进制流。 | binary | GeometryStream |
| TypeDefinition | 指向 TypeDefinition 的某个特化实例，该实例保存按类型而非按此 Element 实例变化的属性值。 | navigation |  |
| PhysicalMaterial | 指示 bis:PhysicalElement 所用材料对应的 bis:PhysicalMaterial。 | navigation |  |

---

### FloorType

**显示名称:** Floor Type

**基类 (Base Class):** BisCore:PhysicalType

通过关联用户可定义的自定义 Type，进一步特化 Floor 的特定子类。

#### 继承属性 (Inherited Properties)

| 名称 | 描述 | 类型 | 扩展类型 |
| --- | --- | --- | --- |
| Model | 包含此 bis:Element 的 bis:Model。 | navigation |  |
| LastMod | bis:Element 的最后修改时间。由核心框架维护，不应由应用程序直接设置。 | dateTime |  |
| CodeSpec | CodeSpec 属性标识用于生成和验证此 bis:Element 代码值的 bis:CodeSpec。CodeSpec、CodeScope 和 CodeValue 属性的组合对于每个 bis:Element 实例必须是唯一的。 | navigation |  |
| CodeScope | CodeScope 属性标识为代码值提供唯一性范围的 bis:Element。CodeSpec、CodeScope 和 CodeValue 属性的组合对于每个 bis:Element 实例必须是唯一的。 | navigation |  |
| CodeValue | 可空字符串属性，保存 Element 代码的实际文本。CodeSpec、CodeScope 和 CodeValue 属性的组合对于每个 bis:Element 实例必须是唯一的。 | string |  |
| UserLabel | 用户给出的可选友好名称（与存储在 CodeValue 属性中的正式名称相对）。 | string |  |
| Parent | 拥有此 bis:Element 的父 bis:Element。 | navigation |  |
| FederationGuid | 用于跨存储库联合此 bis:Element 的 GUID。 | binary | BeGuid |
| JsonProperties | 用户和/或应用程序可用于持久化临时 JSON 值的字符串属性。 | string | Json |
| IsPrivate | 如果为 true，则此 bis:DefinitionElement 不应在 GUI 中显示。 | boolean |  |
| Recipe |  | navigation |  |
| PhysicalMaterial | 指示给定 bis:PhysicalType 的 bis:PhysicalElements 所用材料对应的 bis:PhysicalMaterial。 | navigation |  |

---

### Furniture

**基类 (Base Class):** BisCore:PhysicalElement

Furniture（家具）表示建筑中的家具元素。

#### 继承属性 (Inherited Properties)

| 名称 | 描述 | 类型 | 扩展类型 |
| --- | --- | --- | --- |
| Model | 包含此 bis:Element 的 bis:Model。 | navigation |  |
| LastMod | bis:Element 的最后修改时间。由核心框架维护，不应由应用程序直接设置。 | dateTime |  |
| CodeSpec | CodeSpec 属性标识用于生成和验证此 bis:Element 代码值的 bis:CodeSpec。CodeSpec、CodeScope 和 CodeValue 属性的组合对于每个 bis:Element 实例必须是唯一的。 | navigation |  |
| CodeScope | CodeScope 属性标识为代码值提供唯一性范围的 bis:Element。CodeSpec、CodeScope 和 CodeValue 属性的组合对于每个 bis:Element 实例必须是唯一的。 | navigation |  |
| CodeValue | 可空字符串属性，保存 Element 代码的实际文本。CodeSpec、CodeScope 和 CodeValue 属性的组合对于每个 bis:Element 实例必须是唯一的。 | string |  |
| UserLabel | 用户给出的可选友好名称（与存储在 CodeValue 属性中的正式名称相对）。 | string |  |
| Parent | 拥有此 bis:Element 的父 bis:Element。 | navigation |  |
| FederationGuid | 用于跨存储库联合此 bis:Element 的 GUID。 | binary | BeGuid |
| JsonProperties | 用户和/或应用程序可用于持久化临时 JSON 值的字符串属性。 | string | Json |
| Category | 用于对此 bis:GeometricElement3d 进行分类的 bis:SpatialCategory | navigation |  |
| InSpatialIndex | 如果为 true，则此元素将在空间索引中有一个条目。 | boolean |  |
| Origin | 此 bis:Element 的放置原点。 | point3d |  |
| Yaw | 此 bis:Element 方向的偏航角（以度为单位）。 | double |  |
| Pitch | 此 bis:Element 方向的俯仰角（以度为单位）。 | double |  |
| Roll | 此 bis:Element 方向的翻滚角（以度为单位）。 | double |  |
| BBoxLow | 此 bis:Element 的元素对齐边界框的"低"点。 | point3d |  |
| BBoxHigh | 此 bis:Element 的元素对齐边界框的"高"点。 | point3d |  |
| GeometryStream | 用于持久化此 bis:Element 几何图形的二进制流。 | binary | GeometryStream |
| TypeDefinition | 指向 TypeDefinition 的某个特化实例，该实例保存按类型而非按此 Element 实例变化的属性值。 | navigation |  |
| PhysicalMaterial | 指示 bis:PhysicalElement 所用材料对应的 bis:PhysicalMaterial。 | navigation |  |

---

### FurnitureType

**显示名称:** Furniture Type

**基类 (Base Class):** BisCore:PhysicalType

通过关联用户可定义的自定义 Type，进一步特化 Furniture 的特定子类。

#### 继承属性 (Inherited Properties)

| 名称 | 描述 | 类型 | 扩展类型 |
| --- | --- | --- | --- |
| Model | 包含此 bis:Element 的 bis:Model。 | navigation |  |
| LastMod | bis:Element 的最后修改时间。由核心框架维护，不应由应用程序直接设置。 | dateTime |  |
| CodeSpec | CodeSpec 属性标识用于生成和验证此 bis:Element 代码值的 bis:CodeSpec。CodeSpec、CodeScope 和 CodeValue 属性的组合对于每个 bis:Element 实例必须是唯一的。 | navigation |  |
| CodeScope | CodeScope 属性标识为代码值提供唯一性范围的 bis:Element。CodeSpec、CodeScope 和 CodeValue 属性的组合对于每个 bis:Element 实例必须是唯一的。 | navigation |  |
| CodeValue | 可空字符串属性，保存 Element 代码的实际文本。CodeSpec、CodeScope 和 CodeValue 属性的组合对于每个 bis:Element 实例必须是唯一的。 | string |  |
| UserLabel | 用户给出的可选友好名称（与存储在 CodeValue 属性中的正式名称相对）。 | string |  |
| Parent | 拥有此 bis:Element 的父 bis:Element。 | navigation |  |
| FederationGuid | 用于跨存储库联合此 bis:Element 的 GUID。 | binary | BeGuid |
| JsonProperties | 用户和/或应用程序可用于持久化临时 JSON 值的字符串属性。 | string | Json |
| IsPrivate | 如果为 true，则此 bis:DefinitionElement 不应在 GUI 中显示。 | boolean |  |
| Recipe |  | navigation |  |
| PhysicalMaterial | 指示给定 bis:PhysicalType 的 bis:PhysicalElements 所用材料对应的 bis:PhysicalMaterial。 | navigation |  |

---

### Railing

**基类 (Base Class):** BisCore:PhysicalElement

Railing（栏杆）表示建筑中的栏杆元素。

#### 继承属性 (Inherited Properties)

| 名称 | 描述 | 类型 | 扩展类型 |
| --- | --- | --- | --- |
| Model | 包含此 bis:Element 的 bis:Model。 | navigation |  |
| LastMod | bis:Element 的最后修改时间。由核心框架维护，不应由应用程序直接设置。 | dateTime |  |
| CodeSpec | CodeSpec 属性标识用于生成和验证此 bis:Element 代码值的 bis:CodeSpec。CodeSpec、CodeScope 和 CodeValue 属性的组合对于每个 bis:Element 实例必须是唯一的。 | navigation |  |
| CodeScope | CodeScope 属性标识为代码值提供唯一性范围的 bis:Element。CodeSpec、CodeScope 和 CodeValue 属性的组合对于每个 bis:Element 实例必须是唯一的。 | navigation |  |
| CodeValue | 可空字符串属性，保存 Element 代码的实际文本。CodeSpec、CodeScope 和 CodeValue 属性的组合对于每个 bis:Element 实例必须是唯一的。 | string |  |
| UserLabel | 用户给出的可选友好名称（与存储在 CodeValue 属性中的正式名称相对）。 | string |  |
| Parent | 拥有此 bis:Element 的父 bis:Element。 | navigation |  |
| FederationGuid | 用于跨存储库联合此 bis:Element 的 GUID。 | binary | BeGuid |
| JsonProperties | 用户和/或应用程序可用于持久化临时 JSON 值的字符串属性。 | string | Json |
| Category | 用于对此 bis:GeometricElement3d 进行分类的 bis:SpatialCategory | navigation |  |
| InSpatialIndex | 如果为 true，则此元素将在空间索引中有一个条目。 | boolean |  |
| Origin | 此 bis:Element 的放置原点。 | point3d |  |
| Yaw | 此 bis:Element 方向的偏航角（以度为单位）。 | double |  |
| Pitch | 此 bis:Element 方向的俯仰角（以度为单位）。 | double |  |
| Roll | 此 bis:Element 方向的翻滚角（以度为单位）。 | double |  |
| BBoxLow | 此 bis:Element 的元素对齐边界框的"低"点。 | point3d |  |
| BBoxHigh | 此 bis:Element 的元素对齐边界框的"高"点。 | point3d |  |
| GeometryStream | 用于持久化此 bis:Element 几何图形的二进制流。 | binary | GeometryStream |
| TypeDefinition | 指向 TypeDefinition 的某个特化实例，该实例保存按类型而非按此 Element 实例变化的属性值。 | navigation |  |
| PhysicalMaterial | 指示 bis:PhysicalElement 所用材料对应的 bis:PhysicalMaterial。 | navigation |  |

---

### RailingType

**显示名称:** Railing Type

**基类 (Base Class):** BisCore:PhysicalType

通过关联用户可定义的自定义 Type，进一步特化 Railing 的特定子类。

#### 继承属性 (Inherited Properties)

| 名称 | 描述 | 类型 | 扩展类型 |
| --- | --- | --- | --- |
| Model | 包含此 bis:Element 的 bis:Model。 | navigation |  |
| LastMod | bis:Element 的最后修改时间。由核心框架维护，不应由应用程序直接设置。 | dateTime |  |
| CodeSpec | CodeSpec 属性标识用于生成和验证此 bis:Element 代码值的 bis:CodeSpec。CodeSpec、CodeScope 和 CodeValue 属性的组合对于每个 bis:Element 实例必须是唯一的。 | navigation |  |
| CodeScope | CodeScope 属性标识为代码值提供唯一性范围的 bis:Element。CodeSpec、CodeScope 和 CodeValue 属性的组合对于每个 bis:Element 实例必须是唯一的。 | navigation |  |
| CodeValue | 可空字符串属性，保存 Element 代码的实际文本。CodeSpec、CodeScope 和 CodeValue 属性的组合对于每个 bis:Element 实例必须是唯一的。 | string |  |
| UserLabel | 用户给出的可选友好名称（与存储在 CodeValue 属性中的正式名称相对）。 | string |  |
| Parent | 拥有此 bis:Element 的父 bis:Element。 | navigation |  |
| FederationGuid | 用于跨存储库联合此 bis:Element 的 GUID。 | binary | BeGuid |
| JsonProperties | 用户和/或应用程序可用于持久化临时 JSON 值的字符串属性。 | string | Json |
| IsPrivate | 如果为 true，则此 bis:DefinitionElement 不应在 GUI 中显示。 | boolean |  |
| Recipe |  | navigation |  |
| PhysicalMaterial | 指示给定 bis:PhysicalType 的 bis:PhysicalElements 所用材料对应的 bis:PhysicalMaterial。 | navigation |  |

---

### Ramp

**基类 (Base Class):** BisCore:PhysicalElement

Ramp（坡道）是一种在两个高程之间过渡的倾斜元素。

#### 继承属性 (Inherited Properties)

| 名称 | 描述 | 类型 | 扩展类型 |
| --- | --- | --- | --- |
| Model | 包含此 bis:Element 的 bis:Model。 | navigation |  |
| LastMod | bis:Element 的最后修改时间。由核心框架维护，不应由应用程序直接设置。 | dateTime |  |
| CodeSpec | CodeSpec 属性标识用于生成和验证此 bis:Element 代码值的 bis:CodeSpec。CodeSpec、CodeScope 和 CodeValue 属性的组合对于每个 bis:Element 实例必须是唯一的。 | navigation |  |
| CodeScope | CodeScope 属性标识为代码值提供唯一性范围的 bis:Element。CodeSpec、CodeScope 和 CodeValue 属性的组合对于每个 bis:Element 实例必须是唯一的。 | navigation |  |
| CodeValue | 可空字符串属性，保存 Element 代码的实际文本。CodeSpec、CodeScope 和 CodeValue 属性的组合对于每个 bis:Element 实例必须是唯一的。 | string |  |
| UserLabel | 用户给出的可选友好名称（与存储在 CodeValue 属性中的正式名称相对）。 | string |  |
| Parent | 拥有此 bis:Element 的父 bis:Element。 | navigation |  |
| FederationGuid | 用于跨存储库联合此 bis:Element 的 GUID。 | binary | BeGuid |
| JsonProperties | 用户和/或应用程序可用于持久化临时 JSON 值的字符串属性。 | string | Json |
| Category | 用于对此 bis:GeometricElement3d 进行分类的 bis:SpatialCategory | navigation |  |
| InSpatialIndex | 如果为 true，则此元素将在空间索引中有一个条目。 | boolean |  |
| Origin | 此 bis:Element 的放置原点。 | point3d |  |
| Yaw | 此 bis:Element 方向的偏航角（以度为单位）。 | double |  |
| Pitch | 此 bis:Element 方向的俯仰角（以度为单位）。 | double |  |
| Roll | 此 bis:Element 方向的翻滚角（以度为单位）。 | double |  |
| BBoxLow | 此 bis:Element 的元素对齐边界框的"低"点。 | point3d |  |
| BBoxHigh | 此 bis:Element 的元素对齐边界框的"高"点。 | point3d |  |
| GeometryStream | 用于持久化此 bis:Element 几何图形的二进制流。 | binary | GeometryStream |
| TypeDefinition | 指向 TypeDefinition 的某个特化实例，该实例保存按类型而非按此 Element 实例变化的属性值。 | navigation |  |
| PhysicalMaterial | 指示 bis:PhysicalElement 所用材料对应的 bis:PhysicalMaterial。 | navigation |  |

---

### RampType

**显示名称:** Ramp Type

**基类 (Base Class):** BisCore:PhysicalType

通过关联用户可定义的自定义 Type，进一步特化 Ramp 的特定子类。

#### 继承属性 (Inherited Properties)

| 名称 | 描述 | 类型 | 扩展类型 |
| --- | --- | --- | --- |
| Model | 包含此 bis:Element 的 bis:Model。 | navigation |  |
| LastMod | bis:Element 的最后修改时间。由核心框架维护，不应由应用程序直接设置。 | dateTime |  |
| CodeSpec | CodeSpec 属性标识用于生成和验证此 bis:Element 代码值的 bis:CodeSpec。CodeSpec、CodeScope 和 CodeValue 属性的组合对于每个 bis:Element 实例必须是唯一的。 | navigation |  |
| CodeScope | CodeScope 属性标识为代码值提供唯一性范围的 bis:Element。CodeSpec、CodeScope 和 CodeValue 属性的组合对于每个 bis:Element 实例必须是唯一的。 | navigation |  |
| CodeValue | 可空字符串属性，保存 Element 代码的实际文本。CodeSpec、CodeScope 和 CodeValue 属性的组合对于每个 bis:Element 实例必须是唯一的。 | string |  |
| UserLabel | 用户给出的可选友好名称（与存储在 CodeValue 属性中的正式名称相对）。 | string |  |
| Parent | 拥有此 bis:Element 的父 bis:Element。 | navigation |  |
| FederationGuid | 用于跨存储库联合此 bis:Element 的 GUID。 | binary | BeGuid |
| JsonProperties | 用户和/或应用程序可用于持久化临时 JSON 值的字符串属性。 | string | Json |
| IsPrivate | 如果为 true，则此 bis:DefinitionElement 不应在 GUI 中显示。 | boolean |  |
| Recipe |  | navigation |  |
| PhysicalMaterial | 指示给定 bis:PhysicalType 的 bis:PhysicalElements 所用材料对应的 bis:PhysicalMaterial。 | navigation |  |

---

### Roof

**基类 (Base Class):** BisCore:PhysicalElement

Roof（屋顶）表示建筑的顶部覆盖结构。

#### 继承属性 (Inherited Properties)

| 名称 | 描述 | 类型 | 扩展类型 |
| --- | --- | --- | --- |
| Model | 包含此 bis:Element 的 bis:Model。 | navigation |  |
| LastMod | bis:Element 的最后修改时间。由核心框架维护，不应由应用程序直接设置。 | dateTime |  |
| CodeSpec | CodeSpec 属性标识用于生成和验证此 bis:Element 代码值的 bis:CodeSpec。CodeSpec、CodeScope 和 CodeValue 属性的组合对于每个 bis:Element 实例必须是唯一的。 | navigation |  |
| CodeScope | CodeScope 属性标识为代码值提供唯一性范围的 bis:Element。CodeSpec、CodeScope 和 CodeValue 属性的组合对于每个 bis:Element 实例必须是唯一的。 | navigation |  |
| CodeValue | 可空字符串属性，保存 Element 代码的实际文本。CodeSpec、CodeScope 和 CodeValue 属性的组合对于每个 bis:Element 实例必须是唯一的。 | string |  |
| UserLabel | 用户给出的可选友好名称（与存储在 CodeValue 属性中的正式名称相对）。 | string |  |
| Parent | 拥有此 bis:Element 的父 bis:Element。 | navigation |  |
| FederationGuid | 用于跨存储库联合此 bis:Element 的 GUID。 | binary | BeGuid |
| JsonProperties | 用户和/或应用程序可用于持久化临时 JSON 值的字符串属性。 | string | Json |
| Category | 用于对此 bis:GeometricElement3d 进行分类的 bis:SpatialCategory | navigation |  |
| InSpatialIndex | 如果为 true，则此元素将在空间索引中有一个条目。 | boolean |  |
| Origin | 此 bis:Element 的放置原点。 | point3d |  |
| Yaw | 此 bis:Element 方向的偏航角（以度为单位）。 | double |  |
| Pitch | 此 bis:Element 方向的俯仰角（以度为单位）。 | double |  |
| Roll | 此 bis:Element 方向的翻滚角（以度为单位）。 | double |  |
| BBoxLow | 此 bis:Element 的元素对齐边界框的"低"点。 | point3d |  |
| BBoxHigh | 此 bis:Element 的元素对齐边界框的"高"点。 | point3d |  |
| GeometryStream | 用于持久化此 bis:Element 几何图形的二进制流。 | binary | GeometryStream |
| TypeDefinition | 指向 TypeDefinition 的某个特化实例，该实例保存按类型而非按此 Element 实例变化的属性值。 | navigation |  |
| PhysicalMaterial | 指示 bis:PhysicalElement 所用材料对应的 bis:PhysicalMaterial。 | navigation |  |

---

### RoofType

**显示名称:** Roof Type

**基类 (Base Class):** BisCore:PhysicalType

通过关联用户可定义的自定义 Type，进一步特化 Roof 的特定子类。

#### 继承属性 (Inherited Properties)

| 名称 | 描述 | 类型 | 扩展类型 |
| --- | --- | --- | --- |
| Model | 包含此 bis:Element 的 bis:Model。 | navigation |  |
| LastMod | bis:Element 的最后修改时间。由核心框架维护，不应由应用程序直接设置。 | dateTime |  |
| CodeSpec | CodeSpec 属性标识用于生成和验证此 bis:Element 代码值的 bis:CodeSpec。CodeSpec、CodeScope 和 CodeValue 属性的组合对于每个 bis:Element 实例必须是唯一的。 | navigation |  |
| CodeScope | CodeScope 属性标识为代码值提供唯一性范围的 bis:Element。CodeSpec、CodeScope 和 CodeValue 属性的组合对于每个 bis:Element 实例必须是唯一的。 | navigation |  |
| CodeValue | 可空字符串属性，保存 Element 代码的实际文本。CodeSpec、CodeScope 和 CodeValue 属性的组合对于每个 bis:Element 实例必须是唯一的。 | string |  |
| UserLabel | 用户给出的可选友好名称（与存储在 CodeValue 属性中的正式名称相对）。 | string |  |
| Parent | 拥有此 bis:Element 的父 bis:Element。 | navigation |  |
| FederationGuid | 用于跨存储库联合此 bis:Element 的 GUID。 | binary | BeGuid |
| JsonProperties | 用户和/或应用程序可用于持久化临时 JSON 值的字符串属性。 | string | Json |
| IsPrivate | 如果为 true，则此 bis:DefinitionElement 不应在 GUI 中显示。 | boolean |  |
| Recipe |  | navigation |  |
| PhysicalMaterial | 指示给定 bis:PhysicalType 的 bis:PhysicalElements 所用材料对应的 bis:PhysicalMaterial。 | navigation |  |

---

### Stair

**基类 (Base Class):** BisCore:PhysicalElement

Stair（楼梯）表示建筑中的楼梯元素。

#### 继承属性 (Inherited Properties)

| 名称 | 描述 | 类型 | 扩展类型 |
| --- | --- | --- | --- |
| Model | 包含此 bis:Element 的 bis:Model。 | navigation |  |
| LastMod | bis:Element 的最后修改时间。由核心框架维护，不应由应用程序直接设置。 | dateTime |  |
| CodeSpec | CodeSpec 属性标识用于生成和验证此 bis:Element 代码值的 bis:CodeSpec。CodeSpec、CodeScope 和 CodeValue 属性的组合对于每个 bis:Element 实例必须是唯一的。 | navigation |  |
| CodeScope | CodeScope 属性标识为代码值提供唯一性范围的 bis:Element。CodeSpec、CodeScope 和 CodeValue 属性的组合对于每个 bis:Element 实例必须是唯一的。 | navigation |  |
| CodeValue | 可空字符串属性，保存 Element 代码的实际文本。CodeSpec、CodeScope 和 CodeValue 属性的组合对于每个 bis:Element 实例必须是唯一的。 | string |  |
| UserLabel | 用户给出的可选友好名称（与存储在 CodeValue 属性中的正式名称相对）。 | string |  |
| Parent | 拥有此 bis:Element 的父 bis:Element。 | navigation |  |
| FederationGuid | 用于跨存储库联合此 bis:Element 的 GUID。 | binary | BeGuid |
| JsonProperties | 用户和/或应用程序可用于持久化临时 JSON 值的字符串属性。 | string | Json |
| Category | 用于对此 bis:GeometricElement3d 进行分类的 bis:SpatialCategory | navigation |  |
| InSpatialIndex | 如果为 true，则此元素将在空间索引中有一个条目。 | boolean |  |
| Origin | 此 bis:Element 的放置原点。 | point3d |  |
| Yaw | 此 bis:Element 方向的偏航角（以度为单位）。 | double |  |
| Pitch | 此 bis:Element 方向的俯仰角（以度为单位）。 | double |  |
| Roll | 此 bis:Element 方向的翻滚角（以度为单位）。 | double |  |
| BBoxLow | 此 bis:Element 的元素对齐边界框的"低"点。 | point3d |  |
| BBoxHigh | 此 bis:Element 的元素对齐边界框的"高"点。 | point3d |  |
| GeometryStream | 用于持久化此 bis:Element 几何图形的二进制流。 | binary | GeometryStream |
| TypeDefinition | 指向 TypeDefinition 的某个特化实例，该实例保存按类型而非按此 Element 实例变化的属性值。 | navigation |  |
| PhysicalMaterial | 指示 bis:PhysicalElement 所用材料对应的 bis:PhysicalMaterial。 | navigation |  |

---

### StairType

**显示名称:** Stair Type

**基类 (Base Class):** BisCore:PhysicalType

通过关联用户可定义的自定义 Type，进一步特化 Stair 的特定子类。

#### 继承属性 (Inherited Properties)

| 名称 | 描述 | 类型 | 扩展类型 |
| --- | --- | --- | --- |
| Model | 包含此 bis:Element 的 bis:Model。 | navigation |  |
| LastMod | bis:Element 的最后修改时间。由核心框架维护，不应由应用程序直接设置。 | dateTime |  |
| CodeSpec | CodeSpec 属性标识用于生成和验证此 bis:Element 代码值的 bis:CodeSpec。CodeSpec、CodeScope 和 CodeValue 属性的组合对于每个 bis:Element 实例必须是唯一的。 | navigation |  |
| CodeScope | CodeScope 属性标识为代码值提供唯一性范围的 bis:Element。CodeSpec、CodeScope 和 CodeValue 属性的组合对于每个 bis:Element 实例必须是唯一的。 | navigation |  |
| CodeValue | 可空字符串属性，保存 Element 代码的实际文本。CodeSpec、CodeScope 和 CodeValue 属性的组合对于每个 bis:Element 实例必须是唯一的。 | string |  |
| UserLabel | 用户给出的可选友好名称（与存储在 CodeValue 属性中的正式名称相对）。 | string |  |
| Parent | 拥有此 bis:Element 的父 bis:Element。 | navigation |  |
| FederationGuid | 用于跨存储库联合此 bis:Element 的 GUID。 | binary | BeGuid |
| JsonProperties | 用户和/或应用程序可用于持久化临时 JSON 值的字符串属性。 | string | Json |
| IsPrivate | 如果为 true，则此 bis:DefinitionElement 不应在 GUI 中显示。 | boolean |  |
| Recipe |  | navigation |  |
| PhysicalMaterial | 指示给定 bis:PhysicalType 的 bis:PhysicalElements 所用材料对应的 bis:PhysicalMaterial。 | navigation |  |

---

### TransportationMechanism

**显示名称:** Transportation Mechanism

**基类 (Base Class):** BisCore:PhysicalElement

TransportationMechanism（运输机制）表示建筑中的垂直运输设备，如电梯、自动扶梯等。

#### 继承属性 (Inherited Properties)

| 名称 | 描述 | 类型 | 扩展类型 |
| --- | --- | --- | --- |
| Model | 包含此 bis:Element 的 bis:Model。 | navigation |  |
| LastMod | bis:Element 的最后修改时间。由核心框架维护，不应由应用程序直接设置。 | dateTime |  |
| CodeSpec | CodeSpec 属性标识用于生成和验证此 bis:Element 代码值的 bis:CodeSpec。CodeSpec、CodeScope 和 CodeValue 属性的组合对于每个 bis:Element 实例必须是唯一的。 | navigation |  |
| CodeScope | CodeScope 属性标识为代码值提供唯一性范围的 bis:Element。CodeSpec、CodeScope 和 CodeValue 属性的组合对于每个 bis:Element 实例必须是唯一的。 | navigation |  |
| CodeValue | 可空字符串属性，保存 Element 代码的实际文本。CodeSpec、CodeScope 和 CodeValue 属性的组合对于每个 bis:Element 实例必须是唯一的。 | string |  |
| UserLabel | 用户给出的可选友好名称（与存储在 CodeValue 属性中的正式名称相对）。 | string |  |
| Parent | 拥有此 bis:Element 的父 bis:Element。 | navigation |  |
| FederationGuid | 用于跨存储库联合此 bis:Element 的 GUID。 | binary | BeGuid |
| JsonProperties | 用户和/或应用程序可用于持久化临时 JSON 值的字符串属性。 | string | Json |
| Category | 用于对此 bis:GeometricElement3d 进行分类的 bis:SpatialCategory | navigation |  |
| InSpatialIndex | 如果为 true，则此元素将在空间索引中有一个条目。 | boolean |  |
| Origin | 此 bis:Element 的放置原点。 | point3d |  |
| Yaw | 此 bis:Element 方向的偏航角（以度为单位）。 | double |  |
| Pitch | 此 bis:Element 方向的俯仰角（以度为单位）。 | double |  |
| Roll | 此 bis:Element 方向的翻滚角（以度为单位）。 | double |  |
| BBoxLow | 此 bis:Element 的元素对齐边界框的"低"点。 | point3d |  |
| BBoxHigh | 此 bis:Element 的元素对齐边界框的"高"点。 | point3d |  |
| GeometryStream | 用于持久化此 bis:Element 几何图形的二进制流。 | binary | GeometryStream |
| TypeDefinition | 指向 TypeDefinition 的某个特化实例，该实例保存按类型而非按此 Element 实例变化的属性值。 | navigation |  |
| PhysicalMaterial | 指示 bis:PhysicalElement 所用材料对应的 bis:PhysicalMaterial。 | navigation |  |

---

### TransportationMechanismType

**显示名称:** TransportationMechanism Type

**基类 (Base Class):** BisCore:PhysicalType

通过关联用户可定义的自定义 Type，进一步特化 TransportationMechanism 的特定子类。

#### 继承属性 (Inherited Properties)

| 名称 | 描述 | 类型 | 扩展类型 |
| --- | --- | --- | --- |
| Model | 包含此 bis:Element 的 bis:Model。 | navigation |  |
| LastMod | bis:Element 的最后修改时间。由核心框架维护，不应由应用程序直接设置。 | dateTime |  |
| CodeSpec | CodeSpec 属性标识用于生成和验证此 bis:Element 代码值的 bis:CodeSpec。CodeSpec、CodeScope 和 CodeValue 属性的组合对于每个 bis:Element 实例必须是唯一的。 | navigation |  |
| CodeScope | CodeScope 属性标识为代码值提供唯一性范围的 bis:Element。CodeSpec、CodeScope 和 CodeValue 属性的组合对于每个 bis:Element 实例必须是唯一的。 | navigation |  |
| CodeValue | 可空字符串属性，保存 Element 代码的实际文本。CodeSpec、CodeScope 和 CodeValue 属性的组合对于每个 bis:Element 实例必须是唯一的。 | string |  |
| UserLabel | 用户给出的可选友好名称（与存储在 CodeValue 属性中的正式名称相对）。 | string |  |
| Parent | 拥有此 bis:Element 的父 bis:Element。 | navigation |  |
| FederationGuid | 用于跨存储库联合此 bis:Element 的 GUID。 | binary | BeGuid |
| JsonProperties | 用户和/或应用程序可用于持久化临时 JSON 值的字符串属性。 | string | Json |
| IsPrivate | 如果为 true，则此 bis:DefinitionElement 不应在 GUI 中显示。 | boolean |  |
| Recipe |  | navigation |  |
| PhysicalMaterial | 指示给定 bis:PhysicalType 的 bis:PhysicalElements 所用材料对应的 bis:PhysicalMaterial。 | navigation |  |

---

### Wall

**基类 (Base Class):** BisCore:PhysicalElement

Wall（墙）表示建筑中的墙体元素。

#### 属性 (Properties)

| 名称 | 描述 | 类型 | 扩展类型 |
| --- | --- | --- | --- |
| Height | 墙的高度 | double |  |
| Width | 墙的宽度（厚度） | double |  |
| GrossVolume | 墙的毛体积 | double |  |
| NetVolume | 墙的净体积 | double |  |
| GrossSideArea | 墙中心处的毛面积 | double |  |
| Length | 沿墙中心线的长度 | double |  |
| NetSideArea | 墙中心处的净面积 | double |  |
| GrossFootprintArea | 墙的毛底面积 | double |  |
| NetFootprintArea | 墙的净底面积 | double |  |

#### 继承属性 (Inherited Properties)

| 名称 | 描述 | 类型 | 扩展类型 |
| --- | --- | --- | --- |
| Model | 包含此 bis:Element 的 bis:Model。 | navigation |  |
| LastMod | bis:Element 的最后修改时间。由核心框架维护，不应由应用程序直接设置。 | dateTime |  |
| CodeSpec | CodeSpec 属性标识用于生成和验证此 bis:Element 代码值的 bis:CodeSpec。CodeSpec、CodeScope 和 CodeValue 属性的组合对于每个 bis:Element 实例必须是唯一的。 | navigation |  |
| CodeScope | CodeScope 属性标识为代码值提供唯一性范围的 bis:Element。CodeSpec、CodeScope 和 CodeValue 属性的组合对于每个 bis:Element 实例必须是唯一的。 | navigation |  |
| CodeValue | 可空字符串属性，保存 Element 代码的实际文本。CodeSpec、CodeScope 和 CodeValue 属性的组合对于每个 bis:Element 实例必须是唯一的。 | string |  |
| UserLabel | 用户给出的可选友好名称（与存储在 CodeValue 属性中的正式名称相对）。 | string |  |
| Parent | 拥有此 bis:Element 的父 bis:Element。 | navigation |  |
| FederationGuid | 用于跨存储库联合此 bis:Element 的 GUID。 | binary | BeGuid |
| JsonProperties | 用户和/或应用程序可用于持久化临时 JSON 值的字符串属性。 | string | Json |
| Category | 用于对此 bis:GeometricElement3d 进行分类的 bis:SpatialCategory | navigation |  |
| InSpatialIndex | 如果为 true，则此元素将在空间索引中有一个条目。 | boolean |  |
| Origin | 此 bis:Element 的放置原点。 | point3d |  |
| Yaw | 此 bis:Element 方向的偏航角（以度为单位）。 | double |  |
| Pitch | 此 bis:Element 方向的俯仰角（以度为单位）。 | double |  |
| Roll | 此 bis:Element 方向的翻滚角（以度为单位）。 | double |  |
| BBoxLow | 此 bis:Element 的元素对齐边界框的"低"点。 | point3d |  |
| BBoxHigh | 此 bis:Element 的元素对齐边界框的"高"点。 | point3d |  |
| GeometryStream | 用于持久化此 bis:Element 几何图形的二进制流。 | binary | GeometryStream |
| TypeDefinition | 指向 TypeDefinition 的某个特化实例，该实例保存按类型而非按此 Element 实例变化的属性值。 | navigation |  |
| PhysicalMaterial | 指示 bis:PhysicalElement 所用材料对应的 bis:PhysicalMaterial。 | navigation |  |

---

### WallLeaf

**显示名称:** Wall Leaf

**基类 (Base Class):** BisCore:PhysicalElement

WallLeaf（墙层）表示复合墙中的单个墙层。

#### 属性 (Properties)

| 名称 | 描述 | 类型 | 扩展类型 |
| --- | --- | --- | --- |
| Height | 墙层的高度 | double |  |
| Length | 沿墙层中心线的长度 | double |  |
| Width | 墙层的宽度（厚度） | double |  |

#### 继承属性 (Inherited Properties)

| 名称 | 描述 | 类型 | 扩展类型 |
| --- | --- | --- | --- |
| Model | 包含此 bis:Element 的 bis:Model。 | navigation |  |
| LastMod | bis:Element 的最后修改时间。由核心框架维护，不应由应用程序直接设置。 | dateTime |  |
| CodeSpec | CodeSpec 属性标识用于生成和验证此 bis:Element 代码值的 bis:CodeSpec。CodeSpec、CodeScope 和 CodeValue 属性的组合对于每个 bis:Element 实例必须是唯一的。 | navigation |  |
| CodeScope | CodeScope 属性标识为代码值提供唯一性范围的 bis:Element。CodeSpec、CodeScope 和 CodeValue 属性的组合对于每个 bis:Element 实例必须是唯一的。 | navigation |  |
| CodeValue | 可空字符串属性，保存 Element 代码的实际文本。CodeSpec、CodeScope 和 CodeValue 属性的组合对于每个 bis:Element 实例必须是唯一的。 | string |  |
| UserLabel | 用户给出的可选友好名称（与存储在 CodeValue 属性中的正式名称相对）。 | string |  |
| Parent | 拥有此 bis:Element 的父 bis:Element。 | navigation |  |
| FederationGuid | 用于跨存储库联合此 bis:Element 的 GUID。 | binary | BeGuid |
| JsonProperties | 用户和/或应用程序可用于持久化临时 JSON 值的字符串属性。 | string | Json |
| Category | 用于对此 bis:GeometricElement3d 进行分类的 bis:SpatialCategory | navigation |  |
| InSpatialIndex | 如果为 true，则此元素将在空间索引中有一个条目。 | boolean |  |
| Origin | 此 bis:Element 的放置原点。 | point3d |  |
| Yaw | 此 bis:Element 方向的偏航角（以度为单位）。 | double |  |
| Pitch | 此 bis:Element 方向的俯仰角（以度为单位）。 | double |  |
| Roll | 此 bis:Element 方向的翻滚角（以度为单位）。 | double |  |
| BBoxLow | 此 bis:Element 的元素对齐边界框的"低"点。 | point3d |  |
| BBoxHigh | 此 bis:Element 的元素对齐边界框的"高"点。 | point3d |  |
| GeometryStream | 用于持久化此 bis:Element 几何图形的二进制流。 | binary | GeometryStream |
| TypeDefinition | 指向 TypeDefinition 的某个特化实例，该实例保存按类型而非按此 Element 实例变化的属性值。 | navigation |  |
| PhysicalMaterial | 指示 bis:PhysicalElement 所用材料对应的 bis:PhysicalMaterial。 | navigation |  |

---

### WallLeafType

**显示名称:** Wall Leaf Type

**基类 (Base Class):** BisCore:PhysicalType

通过关联用户可定义的自定义 Type，进一步特化 WallLeaf 的特定子类。

#### 继承属性 (Inherited Properties)

| 名称 | 描述 | 类型 | 扩展类型 |
| --- | --- | --- | --- |
| Model | 包含此 bis:Element 的 bis:Model。 | navigation |  |
| LastMod | bis:Element 的最后修改时间。由核心框架维护，不应由应用程序直接设置。 | dateTime |  |
| CodeSpec | CodeSpec 属性标识用于生成和验证此 bis:Element 代码值的 bis:CodeSpec。CodeSpec、CodeScope 和 CodeValue 属性的组合对于每个 bis:Element 实例必须是唯一的。 | navigation |  |
| CodeScope | CodeScope 属性标识为代码值提供唯一性范围的 bis:Element。CodeSpec、CodeScope 和 CodeValue 属性的组合对于每个 bis:Element 实例必须是唯一的。 | navigation |  |
| CodeValue | 可空字符串属性，保存 Element 代码的实际文本。CodeSpec、CodeScope 和 CodeValue 属性的组合对于每个 bis:Element 实例必须是唯一的。 | string |  |
| UserLabel | 用户给出的可选友好名称（与存储在 CodeValue 属性中的正式名称相对）。 | string |  |
| Parent | 拥有此 bis:Element 的父 bis:Element。 | navigation |  |
| FederationGuid | 用于跨存储库联合此 bis:Element 的 GUID。 | binary | BeGuid |
| JsonProperties | 用户和/或应用程序可用于持久化临时 JSON 值的字符串属性。 | string | Json |
| IsPrivate | 如果为 true，则此 bis:DefinitionElement 不应在 GUI 中显示。 | boolean |  |
| Recipe |  | navigation |  |
| PhysicalMaterial | 指示给定 bis:PhysicalType 的 bis:PhysicalElements 所用材料对应的 bis:PhysicalMaterial。 | navigation |  |

---

### WallType

**显示名称:** Wall Type

**基类 (Base Class):** BisCore:PhysicalType

通过关联用户可定义的自定义 Type，进一步特化 Wall 的特定子类。

#### 继承属性 (Inherited Properties)

| 名称 | 描述 | 类型 | 扩展类型 |
| --- | --- | --- | --- |
| Model | 包含此 bis:Element 的 bis:Model。 | navigation |  |
| LastMod | bis:Element 的最后修改时间。由核心框架维护，不应由应用程序直接设置。 | dateTime |  |
| CodeSpec | CodeSpec 属性标识用于生成和验证此 bis:Element 代码值的 bis:CodeSpec。CodeSpec、CodeScope 和 CodeValue 属性的组合对于每个 bis:Element 实例必须是唯一的。 | navigation |  |
| CodeScope | CodeScope 属性标识为代码值提供唯一性范围的 bis:Element。CodeSpec、CodeScope 和 CodeValue 属性的组合对于每个 bis:Element 实例必须是唯一的。 | navigation |  |
| CodeValue | 可空字符串属性，保存 Element 代码的实际文本。CodeSpec、CodeScope 和 CodeValue 属性的组合对于每个 bis:Element 实例必须是唯一的。 | string |  |
| UserLabel | 用户给出的可选友好名称（与存储在 CodeValue 属性中的正式名称相对）。 | string |  |
| Parent | 拥有此 bis:Element 的父 bis:Element。 | navigation |  |
| FederationGuid | 用于跨存储库联合此 bis:Element 的 GUID。 | binary | BeGuid |
| JsonProperties | 用户和/或应用程序可用于持久化临时 JSON 值的字符串属性。 | string | Json |
| IsPrivate | 如果为 true，则此 bis:DefinitionElement 不应在 GUI 中显示。 | boolean |  |
| Recipe |  | navigation |  |
| PhysicalMaterial | 指示给定 bis:PhysicalType 的 bis:PhysicalElements 所用材料对应的 bis:PhysicalMaterial。 | navigation |  |

---

### Window

**基类 (Base Class):** BisCore:PhysicalElement

Window（窗）表示建筑中的窗户元素。

#### 属性 (Properties)

| 名称 | 描述 | 类型 | 扩展类型 |
| --- | --- | --- | --- |
| OverallHeight | 窗的整体高度 | double |  |
| OverallWidth | 窗的整体宽度 | double |  |
| Description |  | string |  |

#### 继承属性 (Inherited Properties)

| 名称 | 描述 | 类型 | 扩展类型 |
| --- | --- | --- | --- |
| Model | 包含此 bis:Element 的 bis:Model。 | navigation |  |
| LastMod | bis:Element 的最后修改时间。由核心框架维护，不应由应用程序直接设置。 | dateTime |  |
| CodeSpec | CodeSpec 属性标识用于生成和验证此 bis:Element 代码值的 bis:CodeSpec。CodeSpec、CodeScope 和 CodeValue 属性的组合对于每个 bis:Element 实例必须是唯一的。 | navigation |  |
| CodeScope | CodeScope 属性标识为代码值提供唯一性范围的 bis:Element。CodeSpec、CodeScope 和 CodeValue 属性的组合对于每个 bis:Element 实例必须是唯一的。 | navigation |  |
| CodeValue | 可空字符串属性，保存 Element 代码的实际文本。CodeSpec、CodeScope 和 CodeValue 属性的组合对于每个 bis:Element 实例必须是唯一的。 | string |  |
| UserLabel | 用户给出的可选友好名称（与存储在 CodeValue 属性中的正式名称相对）。 | string |  |
| Parent | 拥有此 bis:Element 的父 bis:Element。 | navigation |  |
| FederationGuid | 用于跨存储库联合此 bis:Element 的 GUID。 | binary | BeGuid |
| JsonProperties | 用户和/或应用程序可用于持久化临时 JSON 值的字符串属性。 | string | Json |
| Category | 用于对此 bis:GeometricElement3d 进行分类的 bis:SpatialCategory | navigation |  |
| InSpatialIndex | 如果为 true，则此元素将在空间索引中有一个条目。 | boolean |  |
| Origin | 此 bis:Element 的放置原点。 | point3d |  |
| Yaw | 此 bis:Element 方向的偏航角（以度为单位）。 | double |  |
| Pitch | 此 bis:Element 方向的俯仰角（以度为单位）。 | double |  |
| Roll | 此 bis:Element 方向的翻滚角（以度为单位）。 | double |  |
| BBoxLow | 此 bis:Element 的元素对齐边界框的"低"点。 | point3d |  |
| BBoxHigh | 此 bis:Element 的元素对齐边界框的"高"点。 | point3d |  |
| GeometryStream | 用于持久化此 bis:Element 几何图形的二进制流。 | binary | GeometryStream |
| TypeDefinition | 指向 TypeDefinition 的某个特化实例，该实例保存按类型而非按此 Element 实例变化的属性值。 | navigation |  |
| PhysicalMaterial | 指示 bis:PhysicalElement 所用材料对应的 bis:PhysicalMaterial。 | navigation |  |

---

### WindowType

**显示名称:** Window Type

**基类 (Base Class):** BisCore:PhysicalType

通过关联用户可定义的自定义 Type，进一步特化 Window 的特定子类。

#### 继承属性 (Inherited Properties)

| 名称 | 描述 | 类型 | 扩展类型 |
| --- | --- | --- | --- |
| Model | 包含此 bis:Element 的 bis:Model。 | navigation |  |
| LastMod | bis:Element 的最后修改时间。由核心框架维护，不应由应用程序直接设置。 | dateTime |  |
| CodeSpec | CodeSpec 属性标识用于生成和验证此 bis:Element 代码值的 bis:CodeSpec。CodeSpec、CodeScope 和 CodeValue 属性的组合对于每个 bis:Element 实例必须是唯一的。 | navigation |  |
| CodeScope | CodeScope 属性标识为代码值提供唯一性范围的 bis:Element。CodeSpec、CodeScope 和 CodeValue 属性的组合对于每个 bis:Element 实例必须是唯一的。 | navigation |  |
| CodeValue | 可空字符串属性，保存 Element 代码的实际文本。CodeSpec、CodeScope 和 CodeValue 属性的组合对于每个 bis:Element 实例必须是唯一的。 | string |  |
| UserLabel | 用户给出的可选友好名称（与存储在 CodeValue 属性中的正式名称相对）。 | string |  |
| Parent | 拥有此 bis:Element 的父 bis:Element。 | navigation |  |
| FederationGuid | 用于跨存储库联合此 bis:Element 的 GUID。 | binary | BeGuid |
| JsonProperties | 用户和/或应用程序可用于持久化临时 JSON 值的字符串属性。 | string | Json |
| IsPrivate | 如果为 true，则此 bis:DefinitionElement 不应在 GUI 中显示。 | boolean |  |
| Recipe |  | navigation |  |
| PhysicalMaterial | 指示给定 bis:PhysicalType 的 bis:PhysicalElements 所用材料对应的 bis:PhysicalMaterial。 | navigation |  |

---

## 关系类 (Relationship Classes)

### CaseworkIsOfType

**显示名称:** Casework Is Of Casework Type

**基类 (Base Class):** BisCore:PhysicalElementIsOfType

**强度 (Strength):** Referencing

**强度方向 (Strength Direction):** Forward

将 Casework 与其 Type 定义关联。

#### Source

- **Is Polymorphic:** true
- **Role Label:** is of type
- **Multiplicity:** (0..*)
- **Constraint Classes:** Casework

#### Target

- **Is Polymorphic:** true
- **Role Label:** is type of
- **Multiplicity:** (0..1)
- **Constraint Classes:** CaseworkType

---

### CeilingIsOfType

**显示名称:** Ceiling Is Of Ceiling Type

**基类 (Base Class):** BisCore:PhysicalElementIsOfType

**强度 (Strength):** Referencing

**强度方向 (Strength Direction):** Forward

将 Ceiling 与其 Type 定义关联。

#### Source

- **Is Polymorphic:** true
- **Role Label:** is of type
- **Multiplicity:** (0..*)
- **Constraint Classes:** Ceiling

#### Target

- **Is Polymorphic:** true
- **Role Label:** is type of
- **Multiplicity:** (0..1)
- **Constraint Classes:** CeilingType

---

### CurtainWallIsOfType

**显示名称:** CurtainWall Is Of CurtainWall Type

**基类 (Base Class):** BisCore:PhysicalElementIsOfType

**强度 (Strength):** Referencing

**强度方向 (Strength Direction):** Forward

将 CurtainWall 与其 Type 定义关联。

#### Source

- **Is Polymorphic:** true
- **Role Label:** is of type
- **Multiplicity:** (0..*)
- **Constraint Classes:** CurtainWall

#### Target

- **Is Polymorphic:** true
- **Role Label:** is type of
- **Multiplicity:** (0..1)
- **Constraint Classes:** CurtainWallType

---

### DoorIsOfType

**显示名称:** Door Is Of Door Type

**基类 (Base Class):** BisCore:PhysicalElementIsOfType

**强度 (Strength):** Referencing

**强度方向 (Strength Direction):** Forward

将 Door 与其 Type 定义关联。

#### Source

- **Is Polymorphic:** true
- **Role Label:** is of type
- **Multiplicity:** (0..*)
- **Constraint Classes:** Door

#### Target

- **Is Polymorphic:** true
- **Role Label:** is type of
- **Multiplicity:** (0..1)
- **Constraint Classes:** DoorType

---

### FloorIsOfType

**显示名称:** Floor Is Of Floor Type

**基类 (Base Class):** BisCore:PhysicalElementIsOfType

**强度 (Strength):** Referencing

**强度方向 (Strength Direction):** Forward

将 Floor 与其 Type 定义关联。

#### Source

- **Is Polymorphic:** true
- **Role Label:** is of type
- **Multiplicity:** (0..*)
- **Constraint Classes:** Floor

#### Target

- **Is Polymorphic:** true
- **Role Label:** is type of
- **Multiplicity:** (0..1)
- **Constraint Classes:** FloorType

---

### FurnitureIsOfType

**显示名称:** Furniture Is Of Furniture Type

**基类 (Base Class):** BisCore:PhysicalElementIsOfType

**强度 (Strength):** Referencing

**强度方向 (Strength Direction):** Forward

将 Furniture 与其 Type 定义关联。

#### Source

- **Is Polymorphic:** true
- **Role Label:** is of type
- **Multiplicity:** (0..*)
- **Constraint Classes:** Furniture

#### Target

- **Is Polymorphic:** true
- **Role Label:** is type of
- **Multiplicity:** (0..1)
- **Constraint Classes:** FurnitureType

---

### RailingIsOfType

**显示名称:** Railing Is Of Railing Type

**基类 (Base Class):** BisCore:PhysicalElementIsOfType

**强度 (Strength):** Referencing

**强度方向 (Strength Direction):** Forward

将 Railing 与其 Type 定义关联。

#### Source

- **Is Polymorphic:** true
- **Role Label:** is of type
- **Multiplicity:** (0..*)
- **Constraint Classes:** Railing

#### Target

- **Is Polymorphic:** true
- **Role Label:** is type of
- **Multiplicity:** (0..1)
- **Constraint Classes:** RailingType

---

### RampIsOfType

**显示名称:** Ramp Is Of Ramp Type

**基类 (Base Class):** BisCore:PhysicalElementIsOfType

**强度 (Strength):** Referencing

**强度方向 (Strength Direction):** Forward

将 Ramp 与其 Type 定义关联。

#### Source

- **Is Polymorphic:** true
- **Role Label:** is of type
- **Multiplicity:** (0..*)
- **Constraint Classes:** Ramp

#### Target

- **Is Polymorphic:** true
- **Role Label:** is type of
- **Multiplicity:** (0..1)
- **Constraint Classes:** RampType

---

### RoofIsOfType

**显示名称:** Roof Is Of Roof Type

**基类 (Base Class):** BisCore:PhysicalElementIsOfType

**强度 (Strength):** Referencing

**强度方向 (Strength Direction):** Forward

将 Roof 与其 Type 定义关联。

#### Source

- **Is Polymorphic:** true
- **Role Label:** is of type
- **Multiplicity:** (0..*)
- **Constraint Classes:** Roof

#### Target

- **Is Polymorphic:** true
- **Role Label:** is type of
- **Multiplicity:** (0..1)
- **Constraint Classes:** RoofType

---

### StairIsOfType

**显示名称:** Stair Is Of Stair Type

**基类 (Base Class):** BisCore:PhysicalElementIsOfType

**强度 (Strength):** Referencing

**强度方向 (Strength Direction):** Forward

将 Stair 与其 Type 定义关联。

#### Source

- **Is Polymorphic:** true
- **Role Label:** is of type
- **Multiplicity:** (0..*)
- **Constraint Classes:** Stair

#### Target

- **Is Polymorphic:** true
- **Role Label:** is type of
- **Multiplicity:** (0..1)
- **Constraint Classes:** StairType

---

### TransportationMechanismIsOfType

**显示名称:** TransportationMechanism Is Of TransportationMechanism Type

**基类 (Base Class):** BisCore:PhysicalElementIsOfType

**强度 (Strength):** Referencing

**强度方向 (Strength Direction):** Forward

将 TransportationMechanism 与其 Type 定义关联。

#### Source

（未在原文中指定详细约束）

#### Target

（未在原文中指定详细约束）

---

### WallIsOfType

**显示名称:** Wall Is Of Wall Type

**基类 (Base Class):** BisCore:PhysicalElementIsOfType

**强度 (Strength):** Referencing

**强度方向 (Strength Direction):** Forward

将 Wall 与其 Type 定义关联。

#### Source

- **Is Polymorphic:** true
- **Role Label:** is of type
- **Multiplicity:** (0..*)
- **Constraint Classes:** Wall

#### Target

- **Is Polymorphic:** true
- **Role Label:** is type of
- **Multiplicity:** (0..1)
- **Constraint Classes:** WallType

---

### WallLeafIsOfType

**显示名称:** Wall Leaf Is Of Wall Leaf Type

**基类 (Base Class):** BisCore:PhysicalElementIsOfType

**强度 (Strength):** Referencing

**强度方向 (Strength Direction):** Forward

将 WallLeaf 与其 Type 定义关联。

#### Source

- **Is Polymorphic:** true
- **Role Label:** is of type
- **Multiplicity:** (0..*)
- **Constraint Classes:** WallLeaf

#### Target

- **Is Polymorphic:** true
- **Role Label:** is type of
- **Multiplicity:** (0..1)
- **Constraint Classes:** WallLeafType

---

### WallOwnsWallLeafs

**显示名称:** Wall Owns Wall Leafs

**基类 (Base Class):** BisCore:ElementOwnsChildElements

**强度 (Strength):** Embedding

**强度方向 (Strength Direction):** Forward

表示 Wall 拥有 WallLeaf 的父子关系。

#### Source

- **Is Polymorphic:** true
- **Role Label:** Wall leaf related to
- **Multiplicity:** (0..1)
- **Constraint Classes:** Wall

#### Target

- **Is Polymorphic:** true
- **Role Label:** Wall leaf owned by
- **Multiplicity:** (0..*)
- **Constraint Classes:** WallLeaf

---

### WindowIsOfType

**显示名称:** Window Is Of Window Type

**基类 (Base Class):** BisCore:PhysicalElementIsOfType

**强度 (Strength):** Referencing

**强度方向 (Strength Direction):** Forward

将 Window 与其 Type 定义关联。

#### Source

- **Is Polymorphic:** true
- **Role Label:** is of type
- **Multiplicity:** (0..*)
- **Constraint Classes:** Window

#### Target

- **Is Polymorphic:** true
- **Role Label:** is type of
- **Multiplicity:** (0..1)
- **Constraint Classes:** WindowType

---

## 另见

- [BisCore ECSchema](../core/biscore.ecschema.md)
- [PhysicalType 文档](../concepts/physical-type.md)
- [iTwin.js 官方文档](https://www.itwinjs.org/)

---

> 原文来源: https://www.itwinjs.org/bis/domains/architecturalphysical.ecschema/
