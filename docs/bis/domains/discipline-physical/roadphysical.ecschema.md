# RoadPhysical Schema

**Alias:** rdphys

**Version:** 1.0.0

Road domain 的主 schema。

## 目录

- Entity Classes
  - RoadNetwork
  - Roadway

## Entity Classes

### __RoadNetwork__ (Road Network) EntityClass

Road network 物理建模的入口点元素。

**Base Class:** RoadRailPhysical:TransportationNetwork

继承属性

| Name | Description | Type | Extended Type |
| --- | --- | --- | --- |
| Model | 包含此 bis:Element 的 bis:Model。 | navigation |  |
| LastMod | bis:Element 的最后修改时间。此属性由核心框架维护，应用程序不应直接设置。 | dateTime |  |
| CodeSpec | CodeSpec 属性标识用于生成和验证此 bis:Element 的 code value 的 bis:CodeSpec。CodeSpec、CodeScope 和 CodeValue 属性的组合对每个 bis:Element 实例必须是唯一的。 | navigation |  |
| CodeScope | CodeScope 属性标识为 code value 提供唯一性范围的 bis:Element。CodeSpec、CodeScope 和 CodeValue 属性的组合对每个 bis:Element 实例必须是唯一的。 | navigation |  |
| CodeValue | 可为空的字符串属性，保存 Element 的 Code 的实际文本。CodeSpec、CodeScope 和 CodeValue 属性的组合对每个 bis:Element 实例必须是唯一的。 | string |  |
| UserLabel | 用户给出的可选友好名称（与存储在 CodeValue 属性中的正式名称相对）。 | string |  |
| Parent | 拥有此 bis:Element 的父 bis:Element。 | navigation |  |
| FederationGuid | 用于在仓库之间联合此 bis:Element 的 GUID。 | binary | BeGuid |
| JsonProperties | 用户和/或应用程序可用于持久化临时 JSON 值的字符串属性。 | string | Json |
| Category | 用于对此 bis:GeometricElement3d 进行分类的 bis:SpatialCategory。 | navigation |  |
| InSpatialIndex | 如果为 true，此元素将在 Spatial Index 中有条目。 | boolean |  |
| Origin | 此 bis:Element 的放置原点。 | point3d |  |
| Yaw | 此 bis:Element 方向的 Yaw 角度（以度为单位）。 | double |  |
| Pitch | 此 bis:Element 方向的 Pitch 角度（以度为单位）。 | double |  |
| Roll | 此 bis:Element 方向的 Roll 角度（以度为单位）。 | double |  |
| BBoxLow | 此 bis:Element 的元素对齐边界框的"低"点。 | point3d |  |
| BBoxHigh | 此 bis:Element 的元素对齐边界框的"高"点。 | point3d |  |
| GeometryStream | 用于持久化此 bis:Element 几何图形的二进制流。 | binary | GeometryStream |
| TypeDefinition | 指向 TypeDefinition 某个特化实例，该实例保存按类型而非按此 Element 实例变化的属性值。 | navigation |  |
| PhysicalMaterial | 指示 bis:PhysicalElement 由何种 bis:PhysicalMaterial 制成。 | navigation |  |

### __Roadway__ (Roadway) _Sealed_ EntityClass

具有平滑或铺砌表面的 Pathway，用于机动车、马车等通行。

**Base Class:** RoadRailPhysical:PathwayElement

继承属性

| Name | Description | Type | Extended Type |
| --- | --- | --- | --- |
| Model | 包含此 bis:Element 的 bis:Model。 | navigation |  |
| LastMod | bis:Element 的最后修改时间。此属性由核心框架维护，应用程序不应直接设置。 | dateTime |  |
| CodeSpec | CodeSpec 属性标识用于生成和验证此 bis:Element 的 code value 的 bis:CodeSpec。CodeSpec、CodeScope 和 CodeValue 属性的组合对每个 bis:Element 实例必须是唯一的。 | navigation |  |
| CodeScope | CodeScope 属性标识为 code value 提供唯一性范围的 bis:Element。CodeSpec、CodeScope 和 CodeValue 属性的组合对每个 bis:Element 实例必须是唯一的。 | navigation |  |
| CodeValue | 可为空的字符串属性，保存 Element 的 Code 的实际文本。CodeSpec、CodeScope 和 CodeValue 属性的组合对每个 bis:Element 实例必须是唯一的。 | string |  |
| UserLabel | 用户给出的可选友好名称（与存储在 CodeValue 属性中的正式名称相对）。 | string |  |
| Parent | 拥有此 bis:Element 的父 bis:Element。 | navigation |  |
| FederationGuid | 用于在仓库之间联合此 bis:Element 的 GUID。 | binary | BeGuid |
| JsonProperties | 用户和/或应用程序可用于持久化临时 JSON 值的字符串属性。 | string | Json |
| Category | 用于对此 bis:GeometricElement3d 进行分类的 bis:SpatialCategory。 | navigation |  |
| InSpatialIndex | 如果为 true，此元素将在 Spatial Index 中有条目。 | boolean |  |
| Origin | 此 bis:Element 的放置原点。 | point3d |  |
| Yaw | 此 bis:Element 方向的 Yaw 角度（以度为单位）。 | double |  |
| Pitch | 此 bis:Element 方向的 Pitch 角度（以度为单位）。 | double |  |
| Roll | 此 bis:Element 方向的 Roll 角度（以度为单位）。 | double |  |
| BBoxLow | 此 bis:Element 的元素对齐边界框的"低"点。 | point3d |  |
| BBoxHigh | 此 bis:Element 的元素对齐边界框的"高"点。 | point3d |  |
| GeometryStream | 用于持久化此 bis:Element 几何图形的二进制流。 | binary | GeometryStream |
| TypeDefinition | 指向 TypeDefinition 某个特化实例，该实例保存按类型而非按此 Element 实例变化的属性值。 | navigation |  |
| PhysicalMaterial | 指示 bis:PhysicalElement 由何种 bis:PhysicalMaterial 制成。 | navigation |  |
| MainAlignment |  | navigation |  |

---

最后更新：2025年6月11日

---

**来源：** [https://www.itwinjs.org/bis/domains/roadphysical.ecschema/](https://www.itwinjs.org/bis/domains/roadphysical.ecschema/)
