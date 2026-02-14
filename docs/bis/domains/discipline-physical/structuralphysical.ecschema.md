# StructuralPhysical ECSchema

**Alias:** sp

**Version:** 1.0.1

**源文档:** https://www.itwinjs.org/bis/domains/structuralphysical.ecschema/

此 schema 包含用于建模构成基础设施结构系统的现实世界物理实体的类。

下图展示了 StructuralPhysical schema 中的主要类和关系：

![StructuralPhysical classes](https://www.itwinjs.org/media/structuralphysical-classes.png)

## 目录

- Entity Classes
  - Beam
  - Brace
  - Column
  - FoundationMember
  - Pile
  - PileCap
  - Slab
  - SpreadFooting
  - StripFooting
  - StructuralElement
  - StructuralMember
  - StructuralPhysicalModel
  - Wall

## Entity Classes

### Beam (梁)

**Base Class:** StructuralPhysical:StructuralMember

**继承属性**

| 名称 | 描述 | 类型 | 扩展类型 |
| --- | --- | --- | --- |
| Model | 包含此 bis:Element 的 bis:Model。 | navigation |  |
| LastMod | bis:Element 的最后修改时间。由核心框架维护，应用程序不应直接设置。 | dateTime |  |
| CodeSpec | CodeSpec 属性标识用于生成和验证此 bis:Element 代码值的 bis:CodeSpec。每个 bis:Element 实例的 CodeSpec、CodeScope 和 CodeValue 属性组合必须唯一。 | navigation |  |
| CodeScope | CodeScope 属性标识为代码值提供唯一性范围的 bis:Element。每个 bis:Element 实例的 CodeSpec、CodeScope 和 CodeValue 属性组合必须唯一。 | navigation |  |
| CodeValue | 可空字符串属性，保存 Element 的 Code 的实际文本。每个 bis:Element 实例的 CodeSpec、CodeScope 和 CodeValue 属性组合必须唯一。 | string |  |
| UserLabel | 用户给出的可选友好名称（与存储在 CodeValue 属性中的正式名称相对）。 | string |  |
| Parent | 拥有此 bis:Element 的父 bis:Element。 | navigation |  |
| FederationGuid | 用于在仓库之间联合此 bis:Element 的 GUID。 | binary | BeGuid |
| JsonProperties | 用户和/或应用程序可用于持久化临时 JSON 值的字符串属性。 | string | Json |
| Category | 用于对此 bis:GeometricElement3d 进行分类的 bis:SpatialCategory。 | navigation |  |
| InSpatialIndex | 如果为 true，则此元素将在 Spatial Index 中有条目。 | boolean |  |
| Origin | 此 bis:Element 的放置原点。 | point3d |  |
| Yaw | 此 bis:Element 方向的 Yaw 角度（以度为单位）。 | double |  |
| Pitch | 此 bis:Element 方向的 Pitch 角度（以度为单位）。 | double |  |
| Roll | 此 bis:Element 方向的 Roll 角度（以度为单位）。 | double |  |
| BBoxLow | 此 bis:Element 的元素对齐边界框的"低"点。 | point3d |  |
| BBoxHigh | 此 bis:Element 的元素对齐边界框的"高"点。 | point3d |  |
| GeometryStream | 用于持久化此 bis:Element 几何图形的二进制流。 | binary | GeometryStream |
| TypeDefinition | 指向 TypeDefinition 的某个特化实例，该实例保存按类型而非按此 Element 实例变化的属性值。 | navigation |  |
| PhysicalMaterial | 指示 bis:PhysicalElement 所使用的 bis:PhysicalMaterial。 | navigation |  |

`Beam` 通常是水平或近乎水平的结构构件，旨在主要通过抗弯来承受荷载。

`Beam` 实例的分类可以通过 `BeamType` 实例实现。`Beam` 必须包含在 `PhysicalModel` 中。

等效于 IfcBeam。

---

### Brace (支撑)

**Base Class:** StructuralPhysical:StructuralMember

**继承属性**

| 名称 | 描述 | 类型 | 扩展类型 |
| --- | --- | --- | --- |
| Model | 包含此 bis:Element 的 bis:Model。 | navigation |  |
| LastMod | bis:Element 的最后修改时间。由核心框架维护，应用程序不应直接设置。 | dateTime |  |
| CodeSpec | CodeSpec 属性标识用于生成和验证此 bis:Element 代码值的 bis:CodeSpec。每个 bis:Element 实例的 CodeSpec、CodeScope 和 CodeValue 属性组合必须唯一。 | navigation |  |
| CodeScope | CodeScope 属性标识为代码值提供唯一性范围的 bis:Element。每个 bis:Element 实例的 CodeSpec、CodeScope 和 CodeValue 属性组合必须唯一。 | navigation |  |
| CodeValue | 可空字符串属性，保存 Element 的 Code 的实际文本。每个 bis:Element 实例的 CodeSpec、CodeScope 和 CodeValue 属性组合必须唯一。 | string |  |
| UserLabel | 用户给出的可选友好名称（与存储在 CodeValue 属性中的正式名称相对）。 | string |  |
| Parent | 拥有此 bis:Element 的父 bis:Element。 | navigation |  |
| FederationGuid | 用于在仓库之间联合此 bis:Element 的 GUID。 | binary | BeGuid |
| JsonProperties | 用户和/或应用程序可用于持久化临时 JSON 值的字符串属性。 | string | Json |
| Category | 用于对此 bis:GeometricElement3d 进行分类的 bis:SpatialCategory。 | navigation |  |
| InSpatialIndex | 如果为 true，则此元素将在 Spatial Index 中有条目。 | boolean |  |
| Origin | 此 bis:Element 的放置原点。 | point3d |  |
| Yaw | 此 bis:Element 方向的 Yaw 角度（以度为单位）。 | double |  |
| Pitch | 此 bis:Element 方向的 Pitch 角度（以度为单位）。 | double |  |
| Roll | 此 bis:Element 方向的 Roll 角度（以度为单位）。 | double |  |
| BBoxLow | 此 bis:Element 的元素对齐边界框的"低"点。 | point3d |  |
| BBoxHigh | 此 bis:Element 的元素对齐边界框的"高"点。 | point3d |  |
| GeometryStream | 用于持久化此 bis:Element 几何图形的二进制流。 | binary | GeometryStream |
| TypeDefinition | 指向 TypeDefinition 的某个特化实例，该实例保存按类型而非按此 Element 实例变化的属性值。 | navigation |  |
| PhysicalMaterial | 指示 bis:PhysicalElement 所使用的 bis:PhysicalMaterial。 | navigation |  |

`Brace` 是一种结构构件，旨在为结构提供侧向支撑，通过抵抗侧向力来确保稳定性。它通常作为对角元素，连接到其他构件。作为 `StructuralMember`，它为承载目的的整体结构系统的完整性和刚度做出贡献。

`Brace` 实例的分类可以通过 `BraceType` 实例实现。`Brace` 必须包含在 `PhysicalModel` 中。

等效于 PredefinedType 等于 IfcMemberTypeEnum.BRACE 的 IfcMember。

---

### Column (柱)

**Base Class:** StructuralPhysical:StructuralMember

**继承属性**

| 名称 | 描述 | 类型 | 扩展类型 |
| --- | --- | --- | --- |
| Model | 包含此 bis:Element 的 bis:Model。 | navigation |  |
| LastMod | bis:Element 的最后修改时间。由核心框架维护，应用程序不应直接设置。 | dateTime |  |
| CodeSpec | CodeSpec 属性标识用于生成和验证此 bis:Element 代码值的 bis:CodeSpec。每个 bis:Element 实例的 CodeSpec、CodeScope 和 CodeValue 属性组合必须唯一。 | navigation |  |
| CodeScope | CodeScope 属性标识为代码值提供唯一性范围的 bis:Element。每个 bis:Element 实例的 CodeSpec、CodeScope 和 CodeValue 属性组合必须唯一。 | navigation |  |
| CodeValue | 可空字符串属性，保存 Element 的 Code 的实际文本。每个 bis:Element 实例的 CodeSpec、CodeScope 和 CodeValue 属性组合必须唯一。 | string |  |
| UserLabel | 用户给出的可选友好名称（与存储在 CodeValue 属性中的正式名称相对）。 | string |  |
| Parent | 拥有此 bis:Element 的父 bis:Element。 | navigation |  |
| FederationGuid | 用于在仓库之间联合此 bis:Element 的 GUID。 | binary | BeGuid |
| JsonProperties | 用户和/或应用程序可用于持久化临时 JSON 值的字符串属性。 | string | Json |
| Category | 用于对此 bis:GeometricElement3d 进行分类的 bis:SpatialCategory。 | navigation |  |
| InSpatialIndex | 如果为 true，则此元素将在 Spatial Index 中有条目。 | boolean |  |
| Origin | 此 bis:Element 的放置原点。 | point3d |  |
| Yaw | 此 bis:Element 方向的 Yaw 角度（以度为单位）。 | double |  |
| Pitch | 此 bis:Element 方向的 Pitch 角度（以度为单位）。 | double |  |
| Roll | 此 bis:Element 方向的 Roll 角度（以度为单位）。 | double |  |
| BBoxLow | 此 bis:Element 的元素对齐边界框的"低"点。 | point3d |  |
| BBoxHigh | 此 bis:Element 的元素对齐边界框的"高"点。 | point3d |  |
| GeometryStream | 用于持久化此 bis:Element 几何图形的二进制流。 | binary | GeometryStream |
| TypeDefinition | 指向 TypeDefinition 的某个特化实例，该实例保存按类型而非按此 Element 实例变化的属性值。 | navigation |  |
| PhysicalMaterial | 指示 bis:PhysicalElement 所使用的 bis:PhysicalMaterial。 | navigation |  |

`Column` 是通常与结构网格交点对齐的垂直结构构件。通常，它作为垂直或近乎垂直的结构构件，通过压缩将上方结构的重量传递到下方的其他元素。

`Column` 实例的分类可以通过 `ColumnType` 实例实现。`Column` 必须包含在 `PhysicalModel` 中。

等效于 IfcColumn。

---

### FoundationMember (基础构件)

**Base Class:** StructuralPhysical:StructuralMember

**继承属性**

| 名称 | 描述 | 类型 | 扩展类型 |
| --- | --- | --- | --- |
| Model | 包含此 bis:Element 的 bis:Model。 | navigation |  |
| LastMod | bis:Element 的最后修改时间。由核心框架维护，应用程序不应直接设置。 | dateTime |  |
| CodeSpec | CodeSpec 属性标识用于生成和验证此 bis:Element 代码值的 bis:CodeSpec。每个 bis:Element 实例的 CodeSpec、CodeScope 和 CodeValue 属性组合必须唯一。 | navigation |  |
| CodeScope | CodeScope 属性标识为代码值提供唯一性范围的 bis:Element。每个 bis:Element 实例的 CodeSpec、CodeScope 和 CodeValue 属性组合必须唯一。 | navigation |  |
| CodeValue | 可空字符串属性，保存 Element 的 Code 的实际文本。每个 bis:Element 实例的 CodeSpec、CodeScope 和 CodeValue 属性组合必须唯一。 | string |  |
| UserLabel | 用户给出的可选友好名称（与存储在 CodeValue 属性中的正式名称相对）。 | string |  |
| Parent | 拥有此 bis:Element 的父 bis:Element。 | navigation |  |
| FederationGuid | 用于在仓库之间联合此 bis:Element 的 GUID。 | binary | BeGuid |
| JsonProperties | 用户和/或应用程序可用于持久化临时 JSON 值的字符串属性。 | string | Json |
| Category | 用于对此 bis:GeometricElement3d 进行分类的 bis:SpatialCategory。 | navigation |  |
| InSpatialIndex | 如果为 true，则此元素将在 Spatial Index 中有条目。 | boolean |  |
| Origin | 此 bis:Element 的放置原点。 | point3d |  |
| Yaw | 此 bis:Element 方向的 Yaw 角度（以度为单位）。 | double |  |
| Pitch | 此 bis:Element 方向的 Pitch 角度（以度为单位）。 | double |  |
| Roll | 此 bis:Element 方向的 Roll 角度（以度为单位）。 | double |  |
| BBoxLow | 此 bis:Element 的元素对齐边界框的"低"点。 | point3d |  |
| BBoxHigh | 此 bis:Element 的元素对齐边界框的"高"点。 | point3d |  |
| GeometryStream | 用于持久化此 bis:Element 几何图形的二进制流。 | binary | GeometryStream |
| TypeDefinition | 指向 TypeDefinition 的某个特化实例，该实例保存按类型而非按此 Element 实例变化的属性值。 | navigation |  |
| PhysicalMaterial | 指示 bis:PhysicalElement 所使用的 bis:PhysicalMaterial。 | navigation |  |

`FoundationMember` 是一种基础结构元素，旨在将建筑荷载传递到地面。它作为结构层次结构中的基类，为整个结构提供必要的支撑和稳定性。此类进一步特化为特定类型的基础构件，如 footing（基础底座）或 pile（桩），这些特化类根据特定的承载和地面条件进行定制。作为基本组件，它确保从上方结构到下方支撑地面的荷载安全有效传递。

---

### Pile (桩)

**Base Class:** StructuralPhysical:FoundationMember

**继承属性**

| 名称 | 描述 | 类型 | 扩展类型 |
| --- | --- | --- | --- |
| Model | 包含此 bis:Element 的 bis:Model。 | navigation |  |
| LastMod | bis:Element 的最后修改时间。由核心框架维护，应用程序不应直接设置。 | dateTime |  |
| CodeSpec | CodeSpec 属性标识用于生成和验证此 bis:Element 代码值的 bis:CodeSpec。每个 bis:Element 实例的 CodeSpec、CodeScope 和 CodeValue 属性组合必须唯一。 | navigation |  |
| CodeScope | CodeScope 属性标识为代码值提供唯一性范围的 bis:Element。每个 bis:Element 实例的 CodeSpec、CodeScope 和 CodeValue 属性组合必须唯一。 | navigation |  |
| CodeValue | 可空字符串属性，保存 Element 的 Code 的实际文本。每个 bis:Element 实例的 CodeSpec、CodeScope 和 CodeValue 属性组合必须唯一。 | string |  |
| UserLabel | 用户给出的可选友好名称（与存储在 CodeValue 属性中的正式名称相对）。 | string |  |
| Parent | 拥有此 bis:Element 的父 bis:Element。 | navigation |  |
| FederationGuid | 用于在仓库之间联合此 bis:Element 的 GUID。 | binary | BeGuid |
| JsonProperties | 用户和/或应用程序可用于持久化临时 JSON 值的字符串属性。 | string | Json |
| Category | 用于对此 bis:GeometricElement3d 进行分类的 bis:SpatialCategory。 | navigation |  |
| InSpatialIndex | 如果为 true，则此元素将在 Spatial Index 中有条目。 | boolean |  |
| Origin | 此 bis:Element 的放置原点。 | point3d |  |
| Yaw | 此 bis:Element 方向的 Yaw 角度（以度为单位）。 | double |  |
| Pitch | 此 bis:Element 方向的 Pitch 角度（以度为单位）。 | double |  |
| Roll | 此 bis:Element 方向的 Roll 角度（以度为单位）。 | double |  |
| BBoxLow | 此 bis:Element 的元素对齐边界框的"低"点。 | point3d |  |
| BBoxHigh | 此 bis:Element 的元素对齐边界框的"高"点。 | point3d |  |
| GeometryStream | 用于持久化此 bis:Element 几何图形的二进制流。 | binary | GeometryStream |
| TypeDefinition | 指向 TypeDefinition 的某个特化实例，该实例保存按类型而非按此 Element 实例变化的属性值。 | navigation |  |
| PhysicalMaterial | 指示 bis:PhysicalElement 所使用的 bis:PhysicalMaterial。 | navigation |  |

`Pile` 是由木材、混凝土或钢制成的细长结构元素，通过打入、喷射或嵌入地面来支撑荷载。它被归类为 deep foundation（深基础），将荷载传递到更深的地下层以获得增强的稳定性和支撑。

`Pile` 实例的分类可以通过 `PileType` 实例实现。`Pile` 必须包含在 `PhysicalModel` 中。

等效于 IfcPile。

---

### PileCap (桩帽)

**Base Class:** StructuralPhysical:FoundationMember

**继承属性**

| 名称 | 描述 | 类型 | 扩展类型 |
| --- | --- | --- | --- |
| Model | 包含此 bis:Element 的 bis:Model。 | navigation |  |
| LastMod | bis:Element 的最后修改时间。由核心框架维护，应用程序不应直接设置。 | dateTime |  |
| CodeSpec | CodeSpec 属性标识用于生成和验证此 bis:Element 代码值的 bis:CodeSpec。每个 bis:Element 实例的 CodeSpec、CodeScope 和 CodeValue 属性组合必须唯一。 | navigation |  |
| CodeScope | CodeScope 属性标识为代码值提供唯一性范围的 bis:Element。每个 bis:Element 实例的 CodeSpec、CodeScope 和 CodeValue 属性组合必须唯一。 | navigation |  |
| CodeValue | 可空字符串属性，保存 Element 的 Code 的实际文本。每个 bis:Element 实例的 CodeSpec、CodeScope 和 CodeValue 属性组合必须唯一。 | string |  |
| UserLabel | 用户给出的可选友好名称（与存储在 CodeValue 属性中的正式名称相对）。 | string |  |
| Parent | 拥有此 bis:Element 的父 bis:Element。 | navigation |  |
| FederationGuid | 用于在仓库之间联合此 bis:Element 的 GUID。 | binary | BeGuid |
| JsonProperties | 用户和/或应用程序可用于持久化临时 JSON 值的字符串属性。 | string | Json |
| Category | 用于对此 bis:GeometricElement3d 进行分类的 bis:SpatialCategory。 | navigation |  |
| InSpatialIndex | 如果为 true，则此元素将在 Spatial Index 中有条目。 | boolean |  |
| Origin | 此 bis:Element 的放置原点。 | point3d |  |
| Yaw | 此 bis:Element 方向的 Yaw 角度（以度为单位）。 | double |  |
| Pitch | 此 bis:Element 方向的 Pitch 角度（以度为单位）。 | double |  |
| Roll | 此 bis:Element 方向的 Roll 角度（以度为单位）。 | double |  |
| BBoxLow | 此 bis:Element 的元素对齐边界框的"低"点。 | point3d |  |
| BBoxHigh | 此 bis:Element 的元素对齐边界框的"高"点。 | point3d |  |
| GeometryStream | 用于持久化此 bis:Element 几何图形的二进制流。 | binary | GeometryStream |
| TypeDefinition | 指向 TypeDefinition 的某个特化实例，该实例保存按类型而非按此 Element 实例变化的属性值。 | navigation |  |
| PhysicalMaterial | 指示 bis:PhysicalElement 所使用的 bis:PhysicalMaterial。 | navigation |  |

`PileCap` 是一种钢筋混凝土板，放置在多根桩的顶部，将上部结构的荷载均匀分配到各桩上。它作为基础组件，通过连接桩并将上方建筑或结构的荷载传递到下方更深、更稳定的土壤或岩层，确保稳定的支撑。

`PileCap` 实例的分类可以通过 `PileCapType` 实例实现。`PileCap` 必须包含在 `PhysicalModel` 中。

等效于 PredefinedType 等于 IfcFootingTypeEnum.PILE_CAP 的 IfcFooting。

---

### Slab (板)

**Base Class:** StructuralPhysical:StructuralMember

**继承属性**

| 名称 | 描述 | 类型 | 扩展类型 |
| --- | --- | --- | --- |
| Model | 包含此 bis:Element 的 bis:Model。 | navigation |  |
| LastMod | bis:Element 的最后修改时间。由核心框架维护，应用程序不应直接设置。 | dateTime |  |
| CodeSpec | CodeSpec 属性标识用于生成和验证此 bis:Element 代码值的 bis:CodeSpec。每个 bis:Element 实例的 CodeSpec、CodeScope 和 CodeValue 属性组合必须唯一。 | navigation |  |
| CodeScope | CodeScope 属性标识为代码值提供唯一性范围的 bis:Element。每个 bis:Element 实例的 CodeSpec、CodeScope 和 CodeValue 属性组合必须唯一。 | navigation |  |
| CodeValue | 可空字符串属性，保存 Element 的 Code 的实际文本。每个 bis:Element 实例的 CodeSpec、CodeScope 和 CodeValue 属性组合必须唯一。 | string |  |
| UserLabel | 用户给出的可选友好名称（与存储在 CodeValue 属性中的正式名称相对）。 | string |  |
| Parent | 拥有此 bis:Element 的父 bis:Element。 | navigation |  |
| FederationGuid | 用于在仓库之间联合此 bis:Element 的 GUID。 | binary | BeGuid |
| JsonProperties | 用户和/或应用程序可用于持久化临时 JSON 值的字符串属性。 | string | Json |
| Category | 用于对此 bis:GeometricElement3d 进行分类的 bis:SpatialCategory。 | navigation |  |
| InSpatialIndex | 如果为 true，则此元素将在 Spatial Index 中有条目。 | boolean |  |
| Origin | 此 bis:Element 的放置原点。 | point3d |  |
| Yaw | 此 bis:Element 方向的 Yaw 角度（以度为单位）。 | double |  |
| Pitch | 此 bis:Element 方向的 Pitch 角度（以度为单位）。 | double |  |
| Roll | 此 bis:Element 方向的 Roll 角度（以度为单位）。 | double |  |
| BBoxLow | 此 bis:Element 的元素对齐边界框的"低"点。 | point3d |  |
| BBoxHigh | 此 bis:Element 的元素对齐边界框的"高"点。 | point3d |  |
| GeometryStream | 用于持久化此 bis:Element 几何图形的二进制流。 | binary | GeometryStream |
| TypeDefinition | 指向 TypeDefinition 的某个特化实例，该实例保存按类型而非按此 Element 实例变化的属性值。 | navigation |  |
| PhysicalMaterial | 指示 bis:PhysicalElement 所使用的 bis:PhysicalMaterial。 | navigation |  |

`Slab` 是一种可以垂直围合空间的建筑构件。它可以在建筑物中作为下部支撑（地板）或上部结构（屋顶板）。

`Slab` 实例的分类可以通过 `SlabType` 实例实现。`Slab` 必须包含在 `PhysicalModel` 中。

等效于 IfcSlab。

---

### SpreadFooting (扩展基础/独立基础)

**Base Class:** StructuralPhysical:FoundationMember

**继承属性**

| 名称 | 描述 | 类型 | 扩展类型 |
| --- | --- | --- | --- |
| Model | 包含此 bis:Element 的 bis:Model。 | navigation |  |
| LastMod | bis:Element 的最后修改时间。由核心框架维护，应用程序不应直接设置。 | dateTime |  |
| CodeSpec | CodeSpec 属性标识用于生成和验证此 bis:Element 代码值的 bis:CodeSpec。每个 bis:Element 实例的 CodeSpec、CodeScope 和 CodeValue 属性组合必须唯一。 | navigation |  |
| CodeScope | CodeScope 属性标识为代码值提供唯一性范围的 bis:Element。每个 bis:Element 实例的 CodeSpec、CodeScope 和 CodeValue 属性组合必须唯一。 | navigation |  |
| CodeValue | 可空字符串属性，保存 Element 的 Code 的实际文本。每个 bis:Element 实例的 CodeSpec、CodeScope 和 CodeValue 属性组合必须唯一。 | string |  |
| UserLabel | 用户给出的可选友好名称（与存储在 CodeValue 属性中的正式名称相对）。 | string |  |
| Parent | 拥有此 bis:Element 的父 bis:Element。 | navigation |  |
| FederationGuid | 用于在仓库之间联合此 bis:Element 的 GUID。 | binary | BeGuid |
| JsonProperties | 用户和/或应用程序可用于持久化临时 JSON 值的字符串属性。 | string | Json |
| Category | 用于对此 bis:GeometricElement3d 进行分类的 bis:SpatialCategory。 | navigation |  |
| InSpatialIndex | 如果为 true，则此元素将在 Spatial Index 中有条目。 | boolean |  |
| Origin | 此 bis:Element 的放置原点。 | point3d |  |
| Yaw | 此 bis:Element 方向的 Yaw 角度（以度为单位）。 | double |  |
| Pitch | 此 bis:Element 方向的 Pitch 角度（以度为单位）。 | double |  |
| Roll | 此 bis:Element 方向的 Roll 角度（以度为单位）。 | double |  |
| BBoxLow | 此 bis:Element 的元素对齐边界框的"低"点。 | point3d |  |
| BBoxHigh | 此 bis:Element 的元素对齐边界框的"高"点。 | point3d |  |
| GeometryStream | 用于持久化此 bis:Element 几何图形的二进制流。 | binary | GeometryStream |
| TypeDefinition | 指向 TypeDefinition 的某个特化实例，该实例保存按类型而非按此 Element 实例变化的属性值。 | navigation |  |
| PhysicalMaterial | 指示 bis:PhysicalElement 所使用的 bis:PhysicalMaterial。 | navigation |  |

`SpreadFooting` 是一种 shallow foundation（浅基础）元素，将柱的荷载分布到宽阔的区域内。它通常由混凝土垫组成，将柱的重量分散到下方的地面，减少对土壤的压力。这种类型的基础旨在确保柱的稳定性和支撑，是建筑基础的重要组成部分。

`SpreadFooting` 实例的分类可以通过 `SpreadFootingType` 实例实现。`SpreadFooting` 必须包含在 `PhysicalModel` 中。

等效于 PredefinedType 等于 IfcFootingTypeEnum.PAD_FOOTING 的 IfcFooting。

---

### StripFooting (条形基础)

**Base Class:** StructuralPhysical:FoundationMember

**继承属性**

| 名称 | 描述 | 类型 | 扩展类型 |
| --- | --- | --- | --- |
| Model | 包含此 bis:Element 的 bis:Model。 | navigation |  |
| LastMod | bis:Element 的最后修改时间。由核心框架维护，应用程序不应直接设置。 | dateTime |  |
| CodeSpec | CodeSpec 属性标识用于生成和验证此 bis:Element 代码值的 bis:CodeSpec。每个 bis:Element 实例的 CodeSpec、CodeScope 和 CodeValue 属性组合必须唯一。 | navigation |  |
| CodeScope | CodeScope 属性标识为代码值提供唯一性范围的 bis:Element。每个 bis:Element 实例的 CodeSpec、CodeScope 和 CodeValue 属性组合必须唯一。 | navigation |  |
| CodeValue | 可空字符串属性，保存 Element 的 Code 的实际文本。每个 bis:Element 实例的 CodeSpec、CodeScope 和 CodeValue 属性组合必须唯一。 | string |  |
| UserLabel | 用户给出的可选友好名称（与存储在 CodeValue 属性中的正式名称相对）。 | string |  |
| Parent | 拥有此 bis:Element 的父 bis:Element。 | navigation |  |
| FederationGuid | 用于在仓库之间联合此 bis:Element 的 GUID。 | binary | BeGuid |
| JsonProperties | 用户和/或应用程序可用于持久化临时 JSON 值的字符串属性。 | string | Json |
| Category | 用于对此 bis:GeometricElement3d 进行分类的 bis:SpatialCategory。 | navigation |  |
| InSpatialIndex | 如果为 true，则此元素将在 Spatial Index 中有条目。 | boolean |  |
| Origin | 此 bis:Element 的放置原点。 | point3d |  |
| Yaw | 此 bis:Element 方向的 Yaw 角度（以度为单位）。 | double |  |
| Pitch | 此 bis:Element 方向的 Pitch 角度（以度为单位）。 | double |  |
| Roll | 此 bis:Element 方向的 Roll 角度（以度为单位）。 | double |  |
| BBoxLow | 此 bis:Element 的元素对齐边界框的"低"点。 | point3d |  |
| BBoxHigh | 此 bis:Element 的元素对齐边界框的"高"点。 | point3d |  |
| GeometryStream | 用于持久化此 bis:Element 几何图形的二进制流。 | binary | GeometryStream |
| TypeDefinition | 指向 TypeDefinition 的某个特化实例，该实例保存按类型而非按此 Element 实例变化的属性值。 | navigation |  |
| PhysicalMaterial | 指示 bis:PhysicalElement 所使用的 bis:PhysicalMaterial。 | navigation |  |

`StripFooting` 是一种 shallow foundation（浅基础）元素，旨在支撑线性结构，如墙。它是连续的混凝土条带，将墙的荷载分散到更宽的区域内，减少对土壤的压力。这种类型的基础用于确保墙的稳定性和支撑，特别是在承重墙中，是建筑基础的关键组件。

`StripFooting` 实例的分类可以通过 `StripFootingType` 实例实现。`StripFooting` 必须包含在 `PhysicalModel` 中。

等效于 PredefinedType 等于 IfcFootingTypeEnum.STRIP_FOOTING 的 IfcFooting。

---

### StructuralElement (结构元素) *抽象类*

**Base Class:** BisCore:PhysicalElement

**继承属性**

| 名称 | 描述 | 类型 | 扩展类型 |
| --- | --- | --- | --- |
| Model | 包含此 bis:Element 的 bis:Model。 | navigation |  |
| LastMod | bis:Element 的最后修改时间。由核心框架维护，应用程序不应直接设置。 | dateTime |  |
| CodeSpec | CodeSpec 属性标识用于生成和验证此 bis:Element 代码值的 bis:CodeSpec。每个 bis:Element 实例的 CodeSpec、CodeScope 和 CodeValue 属性组合必须唯一。 | navigation |  |
| CodeScope | CodeScope 属性标识为代码值提供唯一性范围的 bis:Element。每个 bis:Element 实例的 CodeSpec、CodeScope 和 CodeValue 属性组合必须唯一。 | navigation |  |
| CodeValue | 可空字符串属性，保存 Element 的 Code 的实际文本。每个 bis:Element 实例的 CodeSpec、CodeScope 和 CodeValue 属性组合必须唯一。 | string |  |
| UserLabel | 用户给出的可选友好名称（与存储在 CodeValue 属性中的正式名称相对）。 | string |  |
| Parent | 拥有此 bis:Element 的父 bis:Element。 | navigation |  |
| FederationGuid | 用于在仓库之间联合此 bis:Element 的 GUID。 | binary | BeGuid |
| JsonProperties | 用户和/或应用程序可用于持久化临时 JSON 值的字符串属性。 | string | Json |
| Category | 用于对此 bis:GeometricElement3d 进行分类的 bis:SpatialCategory。 | navigation |  |
| InSpatialIndex | 如果为 true，则此元素将在 Spatial Index 中有条目。 | boolean |  |
| Origin | 此 bis:Element 的放置原点。 | point3d |  |
| Yaw | 此 bis:Element 方向的 Yaw 角度（以度为单位）。 | double |  |
| Pitch | 此 bis:Element 方向的 Pitch 角度（以度为单位）。 | double |  |
| Roll | 此 bis:Element 方向的 Roll 角度（以度为单位）。 | double |  |
| BBoxLow | 此 bis:Element 的元素对齐边界框的"低"点。 | point3d |  |
| BBoxHigh | 此 bis:Element 的元素对齐边界框的"高"点。 | point3d |  |
| GeometryStream | 用于持久化此 bis:Element 几何图形的二进制流。 | binary | GeometryStream |
| TypeDefinition | 指向 TypeDefinition 的某个特化实例，该实例保存按类型而非按此 Element 实例变化的属性值。 | navigation |  |
| PhysicalMaterial | 指示 bis:PhysicalElement 所使用的 bis:PhysicalMaterial。 | navigation |  |

抽象类 `StructuralElement` 是 `StructuralMember` 的泛化。

等效于 IfcStructuralItem。

---

### StructuralMember (结构构件)

**Base Class:** StructuralPhysical:StructuralElement

**继承属性**

| 名称 | 描述 | 类型 | 扩展类型 |
| --- | --- | --- | --- |
| Model | 包含此 bis:Element 的 bis:Model。 | navigation |  |
| LastMod | bis:Element 的最后修改时间。由核心框架维护，应用程序不应直接设置。 | dateTime |  |
| CodeSpec | CodeSpec 属性标识用于生成和验证此 bis:Element 代码值的 bis:CodeSpec。每个 bis:Element 实例的 CodeSpec、CodeScope 和 CodeValue 属性组合必须唯一。 | navigation |  |
| CodeScope | CodeScope 属性标识为代码值提供唯一性范围的 bis:Element。每个 bis:Element 实例的 CodeSpec、CodeScope 和 CodeValue 属性组合必须唯一。 | navigation |  |
| CodeValue | 可空字符串属性，保存 Element 的 Code 的实际文本。每个 bis:Element 实例的 CodeSpec、CodeScope 和 CodeValue 属性组合必须唯一。 | string |  |
| UserLabel | 用户给出的可选友好名称（与存储在 CodeValue 属性中的正式名称相对）。 | string |  |
| Parent | 拥有此 bis:Element 的父 bis:Element。 | navigation |  |
| FederationGuid | 用于在仓库之间联合此 bis:Element 的 GUID。 | binary | BeGuid |
| JsonProperties | 用户和/或应用程序可用于持久化临时 JSON 值的字符串属性。 | string | Json |
| Category | 用于对此 bis:GeometricElement3d 进行分类的 bis:SpatialCategory。 | navigation |  |
| InSpatialIndex | 如果为 true，则此元素将在 Spatial Index 中有条目。 | boolean |  |
| Origin | 此 bis:Element 的放置原点。 | point3d |  |
| Yaw | 此 bis:Element 方向的 Yaw 角度（以度为单位）。 | double |  |
| Pitch | 此 bis:Element 方向的 Pitch 角度（以度为单位）。 | double |  |
| Roll | 此 bis:Element 方向的 Roll 角度（以度为单位）。 | double |  |
| BBoxLow | 此 bis:Element 的元素对齐边界框的"低"点。 | point3d |  |
| BBoxHigh | 此 bis:Element 的元素对齐边界框的"高"点。 | point3d |  |
| GeometryStream | 用于持久化此 bis:Element 几何图形的二进制流。 | binary | GeometryStream |
| TypeDefinition | 指向 TypeDefinition 的某个特化实例，该实例保存按类型而非按此 Element 实例变化的属性值。 | navigation |  |
| PhysicalMaterial | 指示 bis:PhysicalElement 所使用的 bis:PhysicalMaterial。 | navigation |  |

类 `StructuralMember` 是所有结构项的基类。此类不是抽象的，可用于定义任何通用结构元素，但如果有可用的已定义子类，建议使用该子类。`StructuralMember` 实例必须包含在 `PhysicalModels` 中。

`StructuralMember` 实例的分类可以通过 `StructuralMemberType` 实例实现。

`StructuralMember` 应作为任何特化类的基类。

等效于 IfcStructuralMember。

---

### StructuralPhysicalModel (结构物理模型) *已弃用*

应使用 PhysicalModel 代替此类。

**Base Class:** BisCore:PhysicalModel

**继承属性**

| 名称 | 描述 | 类型 | 扩展类型 |
| --- | --- | --- | --- |
| ParentModel | 父 bis:Model 包含此 bis:Model 正在子建模的 bis:Element。 | navigation |  |
| ModeledElement | 此 bis:Model 正在子建模的 bis:Element。此 bis:Model 与子建模的 bis:Element 建模相同的 Entity，但粒度更细。 | navigation |  |
| IsPrivate | 如果 IsPrivate 为 true，则此 bis:Model 不应出现在向用户显示的列表中。 | boolean |  |
| IsTemplate | 如果 IsTemplate 为 true，则此 bis:Model 用作创建新实例的模板。 | boolean |  |
| JsonProperties | 用户和/或应用程序可用于持久化临时 JSON 值的字符串属性。 | string | Json |
| LastMod | 此 Model 中任何元素的最后修改时间。 | dateTime |  |
| GeometryGuid | 每当此 GeometricModel 中的任何元素的几何图形发生更改时都会更改的 GUID。 | binary | BeGuid |
| IsNotSpatiallyLocated | 如果 IsNotSpatiallyLocated 为 true，则此 bis:GeometricModel3d 中的元素不在现实世界坐标中，并且不会在空间索引中。 | boolean |  |
| IsPlanProjection | 如果 IsPlanProjection 为 true，则此 bis:GeometricModel3d 中的元素预期位于 XY 平面中。 | boolean |  |

*此类已被弃用。请勿使用。*

应用程序、服务和组件绝不应创建此类的实例。请改用 `PhysicalModel`。

---

### Wall (墙)

**Base Class:** StructuralPhysical:StructuralMember

**继承属性**

| 名称 | 描述 | 类型 | 扩展类型 |
| --- | --- | --- | --- |
| Model | 包含此 bis:Element 的 bis:Model。 | navigation |  |
| LastMod | bis:Element 的最后修改时间。由核心框架维护，应用程序不应直接设置。 | dateTime |  |
| CodeSpec | CodeSpec 属性标识用于生成和验证此 bis:Element 代码值的 bis:CodeSpec。每个 bis:Element 实例的 CodeSpec、CodeScope 和 CodeValue 属性组合必须唯一。 | navigation |  |
| CodeScope | CodeScope 属性标识为代码值提供唯一性范围的 bis:Element。每个 bis:Element 实例的 CodeSpec、CodeScope 和 CodeValue 属性组合必须唯一。 | navigation |  |
| CodeValue | 可空字符串属性，保存 Element 的 Code 的实际文本。每个 bis:Element 实例的 CodeSpec、CodeScope 和 CodeValue 属性组合必须唯一。 | string |  |
| UserLabel | 用户给出的可选友好名称（与存储在 CodeValue 属性中的正式名称相对）。 | string |  |
| Parent | 拥有此 bis:Element 的父 bis:Element。 | navigation |  |
| FederationGuid | 用于在仓库之间联合此 bis:Element 的 GUID。 | binary | BeGuid |
| JsonProperties | 用户和/或应用程序可用于持久化临时 JSON 值的字符串属性。 | string | Json |
| Category | 用于对此 bis:GeometricElement3d 进行分类的 bis:SpatialCategory。 | navigation |  |
| InSpatialIndex | 如果为 true，则此元素将在 Spatial Index 中有条目。 | boolean |  |
| Origin | 此 bis:Element 的放置原点。 | point3d |  |
| Yaw | 此 bis:Element 方向的 Yaw 角度（以度为单位）。 | double |  |
| Pitch | 此 bis:Element 方向的 Pitch 角度（以度为单位）。 | double |  |
| Roll | 此 bis:Element 方向的 Roll 角度（以度为单位）。 | double |  |
| BBoxLow | 此 bis:Element 的元素对齐边界框的"低"点。 | point3d |  |
| BBoxHigh | 此 bis:Element 的元素对齐边界框的"高"点。 | point3d |  |
| GeometryStream | 用于持久化此 bis:Element 几何图形的二进制流。 | binary | GeometryStream |
| TypeDefinition | 指向 TypeDefinition 的某个特化实例，该实例保存按类型而非按此 Element 实例变化的属性值。 | navigation |  |
| PhysicalMaterial | 指示 bis:PhysicalElement 所使用的 bis:PhysicalMaterial。 | navigation |  |

`Wall` 是一种可以围合或分隔空间的垂直建筑元素。墙通常是垂直或近乎垂直的平面元素，通常设计用于承受结构荷载。

`Wall` 实例的分类可以通过 `WallType` 实例实现。`Wall` 必须包含在 `PhysicalModel` 中。

等效于 IfcWall。
