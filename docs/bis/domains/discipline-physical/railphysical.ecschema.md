# RailPhysical Schema

__Alias:__ rlphys

__Version:__ 1.0.0

Rail 领域的主 schema。

## 目录

- 实体类 (Entity Classes)
  - RailNetwork
  - Railway

## 实体类 (Entity Classes)

### __RailNetwork__ (铁路网) EntityClass

通往 Rail 网络物理建模的入口元素。

__Base Class:__ RoadRailPhysical:TransportationNetwork

继承的属性

| 名称 | 描述 | 类型 | 扩展类型 |
| --- | --- | --- | --- |
| Model | 包含此 bis:Element 的 bis:Model。 | navigation |  |
| LastMod | bis:Element 的最后修改时间。此属性由核心框架维护，应用程序不应直接设置。 | dateTime |  |
| CodeSpec | CodeSpec 属性标识用于生成和验证此 bis:Element 代码值的 bis:CodeSpec。每个 bis:Element 实例的 CodeSpec、CodeScope 和 CodeValue 属性组合必须唯一。 | navigation |  |
| CodeScope | CodeScope 属性标识为代码值提供唯一性作用域的 bis:Element。每个 bis:Element 实例的 CodeSpec、CodeScope 和 CodeValue 属性组合必须唯一。 | navigation |  |
| CodeValue | 可空字符串属性，保存 Element 代码的实际文本。每个 bis:Element 实例的 CodeSpec、CodeScope 和 CodeValue 属性组合必须唯一。 | string |  |
| UserLabel | 用户给定的可选友好名称（与存储在 CodeValue 属性中的正式名称相对）。 | string |  |
| Parent | 拥有此 bis:Element 的父 bis:Element。 | navigation |  |
| FederationGuid | 用于跨仓库联合此 bis:Element 的 GUID。 | binary | BeGuid |
| JsonProperties | 用户和/或应用程序可用于持久化临时 JSON 值的字符串属性。 | string | Json |
| Category | 用于对此 bis:GeometricElement3d 进行分类的 bis:SpatialCategory | navigation |  |
| InSpatialIndex | 如果为 true，此元素将在空间索引中有条目。 | boolean |  |
| Origin | 此 bis:Element 的放置原点。 | point3d |  |
| Yaw | 此 bis:Element 方向的偏航角（以度为单位）。 | double |  |
| Pitch | 此 bis:Element 方向的俯仰角（以度为单位）。 | double |  |
| Roll | 此 bis:Element 方向的翻滚角（以度为单位）。 | double |  |
| BBoxLow | 此 bis:Element 的元素对齐包围盒的"低"点。 | point3d |  |
| BBoxHigh | 此 bis:Element 的元素对齐包围盒的"高"点。 | point3d |  |
| GeometryStream | 用于持久化此 bis:Element 几何图形的二进制流。 | binary | GeometryStream |
| TypeDefinition | 指向 TypeDefinition 某个特化实例，该实例保存按类型而非按此 Element 实例变化的属性值。 | navigation |  |
| PhysicalMaterial | 指示 bis:PhysicalElement 由何种 bis:PhysicalMaterial 制成。 | navigation |  |

### __Railway__ (铁路) _Sealed_ EntityClass

一条 Pathway，具有一条或多条轨道，客运和货运列车沿其运行。

__Base Class:__ RoadRailPhysical:PathwayElement

继承的属性

| 名称 | 描述 | 类型 | 扩展类型 |
| --- | --- | --- | --- |
| Model | 包含此 bis:Element 的 bis:Model。 | navigation |  |
| LastMod | bis:Element 的最后修改时间。此属性由核心框架维护，应用程序不应直接设置。 | dateTime |  |
| CodeSpec | CodeSpec 属性标识用于生成和验证此 bis:Element 代码值的 bis:CodeSpec。每个 bis:Element 实例的 CodeSpec、CodeScope 和 CodeValue 属性组合必须唯一。 | navigation |  |
| CodeScope | CodeScope 属性标识为代码值提供唯一性作用域的 bis:Element。每个 bis:Element 实例的 CodeSpec、CodeScope 和 CodeValue 属性组合必须唯一。 | navigation |  |
| CodeValue | 可空字符串属性，保存 Element 代码的实际文本。每个 bis:Element 实例的 CodeSpec、CodeScope 和 CodeValue 属性组合必须唯一。 | string |  |
| UserLabel | 用户给定的可选友好名称（与存储在 CodeValue 属性中的正式名称相对）。 | string |  |
| Parent | 拥有此 bis:Element 的父 bis:Element。 | navigation |  |
| FederationGuid | 用于跨仓库联合此 bis:Element 的 GUID。 | binary | BeGuid |
| JsonProperties | 用户和/或应用程序可用于持久化临时 JSON 值的字符串属性。 | string | Json |
| Category | 用于对此 bis:GeometricElement3d 进行分类的 bis:SpatialCategory | navigation |  |
| InSpatialIndex | 如果为 true，此元素将在空间索引中有条目。 | boolean |  |
| Origin | 此 bis:Element 的放置原点。 | point3d |  |
| Yaw | 此 bis:Element 方向的偏航角（以度为单位）。 | double |  |
| Pitch | 此 bis:Element 方向的俯仰角（以度为单位）。 | double |  |
| Roll | 此 bis:Element 方向的翻滚角（以度为单位）。 | double |  |
| BBoxLow | 此 bis:Element 的元素对齐包围盒的"低"点。 | point3d |  |
| BBoxHigh | 此 bis:Element 的元素对齐包围盒的"高"点。 | point3d |  |
| GeometryStream | 用于持久化此 bis:Element 几何图形的二进制流。 | binary | GeometryStream |
| TypeDefinition | 指向 TypeDefinition 某个特化实例，该实例保存按类型而非按此 Element 实例变化的属性值。 | navigation |  |
| PhysicalMaterial | 指示 bis:PhysicalElement 由何种 bis:PhysicalMaterial 制成。 | navigation |  |
| MainAlignment |  | navigation |  |

---

最后更新: 2025年6月11日

---

**原文链接:** https://www.itwinjs.org/bis/domains/railphysical.ecschema/
