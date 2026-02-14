# Terrain Schema

__别名:__ trrn

__版本:__ 1.0.0

Terrain 领域的基础 schema。

此 schema 包含用于提供 _context_ 地形的类。地形的开挖、填充和修改在 Earthwork schema 中定义。

有关 iModel 中如何定义地形的详细信息，请参阅 `ITerrain` 文档。

![Terrain 类图](https://www.itwinjs.org/media/terrain-classes.png)

## 目录

- Entity Classes
  - Terrain
  - TerrainBoundary
  - TerrainBreakline
  - TerrainDrapeBoundary
  - TerrainDrapeVoid
  - TerrainHole
  - TerrainIsland
  - TerrainReference
  - TerrainSourceContour
  - TerrainSourceFeatureElement
  - TerrainSpotElevation
  - TerrainVoid
- Mixins
  - ITerrain
- Relationship Classes
  - ITerrainOwnsBoundary
  - TerrainOwnsSourceFeatures
  - TerrainReferenceViaRepositoryLink

## Entity Classes

### __Terrain__ (地形) EntityClass

一个 `bis:PhysicalElement`，用于对地球上一小部分区域的基础地形进行建模。

__基类:__ BisCore:PhysicalElement

继承属性

| 名称 | 描述 | 类型 | 扩展类型 |
| --- | --- | --- | --- |
| Model | 包含此 bis:Element 的 bis:Model。 | navigation |  |
| LastMod | bis:Element 的最后修改时间。此属性由核心框架维护，不应由应用程序直接设置。 | dateTime |  |
| CodeSpec | CodeSpec 属性标识用于生成和验证此 bis:Element 代码值的 bis:CodeSpec。CodeSpec、CodeScope 和 CodeValue 属性的组合对于每个 bis:Element 实例必须是唯一的。 | navigation |  |
| CodeScope | CodeScope 属性标识为代码值提供唯一性范围的 bis:Element。CodeSpec、CodeScope 和 CodeValue 属性的组合对于每个 bis:Element 实例必须是唯一的。 | navigation |  |
| CodeValue | 可空字符串属性，保存 Element 代码的实际文本。CodeSpec、CodeScope 和 CodeValue 属性的组合对于每个 bis:Element 实例必须是唯一的。 | string |  |
| UserLabel | 用户给定的可选友好名称（与存储在 CodeValue 属性中的正式名称相对）。 | string |  |
| Parent | 拥有此 bis:Element 的父 bis:Element。 | navigation |  |
| FederationGuid | 用于在仓库之间联合此 bis:Element 的 GUID。 | binary | BeGuid |
| JsonProperties | 用户和/或应用程序可用于持久化临时 JSON 值的字符串属性。 | string | Json |
| Category | 用于对此 bis:GeometricElement3d 进行分类的 bis:SpatialCategory | navigation |  |
| InSpatialIndex | 如果为 true，则此元素将在空间索引中有条目。 | boolean |  |
| Origin | 此 bis:Element 的放置原点。 | point3d |  |
| Yaw | 此 bis:Element 方向的偏航角（以度为单位）。 | double |  |
| Pitch | 此 bis:Element 方向的俯仰角（以度为单位）。 | double |  |
| Roll | 此 bis:Element 方向的翻滚角（以度为单位）。 | double |  |
| BBoxLow | 此 bis:Element 的元素对齐边界框的"低"点。 | point3d |  |
| BBoxHigh | 此 bis:Element 的元素对齐边界框的"高"点。 | point3d |  |
| GeometryStream | 用于持久化此 bis:Element 几何图形的二进制流。 | binary | GeometryStream |
| TypeDefinition | 指向 TypeDefinition 的某个特化实例，该实例保存按类型而非按此 Element 实例变化的属性值。 | navigation |  |
| PhysicalMaterial | 指示构成 bis:PhysicalElement 的 bis:PhysicalMaterial。 | navigation |  |

`Terrain` 用于为可能预期会更改的资产和项目定义 _context_，因此它完全包含在 iModel 中。`Terrain` 预期为中小规模，以免对 iModel 的性能产生负面影响。大型地形预期由 `TerrainReference` 捕获。

每个 `Terrain` 拥有多个 `TerrainSourceFeature`，它们捕获 `Terrain` 中非计算得出的细节，例如其边界、breakline 或 spot elevation。等高线、流向箭头或三角形等计算细节不应作为 `Terrain` 的子元素捕获。相反，它们预期在显示时计算。如果需要用于图纸制作，它们仍然可以在 iModel 中作为 `DrawingModel` 中的 `DrawingElement` 捕获。

已完成计算的 `Terrain` 将把计算出的 _Surface_ 作为 _Polyface_ 存储在其 `GeometryStream` 中。

`Terrain` 必须包含在 `PhysicalModel` 中。为 `TerrainReference` 选择包含 `Model` 的相同影响也适用于 `Terrain`。

默认情况下，`Terrain` 的实例应使用 Domain 级别的 `trrn:Terrain` 类别。

### __TerrainBoundary__ (地形边界) EntityClass

一个 `bis:SpatialLocationElement`，用于捕获 ITerrain 元素正在建模的最大外部范围。

__基类:__ BisCore:SpatialLocationElement

继承属性

| 名称 | 描述 | 类型 | 扩展类型 |
| --- | --- | --- | --- |
| Model | 包含此 bis:Element 的 bis:Model。 | navigation |  |
| LastMod | bis:Element 的最后修改时间。此属性由核心框架维护，不应由应用程序直接设置。 | dateTime |  |
| CodeSpec | CodeSpec 属性标识用于生成和验证此 bis:Element 代码值的 bis:CodeSpec。CodeSpec、CodeScope 和 CodeValue 属性的组合对于每个 bis:Element 实例必须是唯一的。 | navigation |  |
| CodeScope | CodeScope 属性标识为代码值提供唯一性范围的 bis:Element。CodeSpec、CodeScope 和 CodeValue 属性的组合对于每个 bis:Element 实例必须是唯一的。 | navigation |  |
| CodeValue | 可空字符串属性，保存 Element 代码的实际文本。CodeSpec、CodeScope 和 CodeValue 属性的组合对于每个 bis:Element 实例必须是唯一的。 | string |  |
| UserLabel | 用户给定的可选友好名称（与存储在 CodeValue 属性中的正式名称相对）。 | string |  |
| Parent | 拥有此 bis:Element 的父 bis:Element。 | navigation |  |
| FederationGuid | 用于在仓库之间联合此 bis:Element 的 GUID。 | binary | BeGuid |
| JsonProperties | 用户和/或应用程序可用于持久化临时 JSON 值的字符串属性。 | string | Json |
| Category | 用于对此 bis:GeometricElement3d 进行分类的 bis:SpatialCategory | navigation |  |
| InSpatialIndex | 如果为 true，则此元素将在空间索引中有条目。 | boolean |  |
| Origin | 此 bis:Element 的放置原点。 | point3d |  |
| Yaw | 此 bis:Element 方向的偏航角（以度为单位）。 | double |  |
| Pitch | 此 bis:Element 方向的俯仰角（以度为单位）。 | double |  |
| Roll | 此 bis:Element 方向的翻滚角（以度为单位）。 | double |  |
| BBoxLow | 此 bis:Element 的元素对齐边界框的"低"点。 | point3d |  |
| BBoxHigh | 此 bis:Element 的元素对齐边界框的"高"点。 | point3d |  |
| GeometryStream | 用于持久化此 bis:Element 几何图形的二进制流。 | binary | GeometryStream |
| TypeDefinition | 指向 TypeDefinition 的某个特化实例，该实例保存按类型而非按此 Element 实例变化的属性值。 | navigation |  |

每个 `ITerrain` 实例预期有一个 `TerrainBoundary`。

如果 `ITerrain` 已经计算完成，它会有一个由 `TerrainBoundary` 类型的单个子元素捕获的 _Boundary_，该子元素将边界的几何细节作为闭合线串（即无弧线）存储在其 `GeometryStream` 中，编码为单个 _LineString3d_。_LineString3d_ 的第一个和最后一个点应相同。

默认情况下，`TerrainBoundary` 的实例应使用 Domain 级别的 `trrn:Boundary` 类别。

### __TerrainBreakline__ (地形断线) EntityClass

一个 TerrainSourceFeature，用于捕获地形中发生坡度急剧变化的线性特征。

__基类:__ Terrain:TerrainSourceFeatureElement

继承属性

| 名称 | 描述 | 类型 | 扩展类型 |
| --- | --- | --- | --- |
| Model | 包含此 bis:Element 的 bis:Model。 | navigation |  |
| LastMod | bis:Element 的最后修改时间。此属性由核心框架维护，不应由应用程序直接设置。 | dateTime |  |
| CodeSpec | CodeSpec 属性标识用于生成和验证此 bis:Element 代码值的 bis:CodeSpec。CodeSpec、CodeScope 和 CodeValue 属性的组合对于每个 bis:Element 实例必须是唯一的。 | navigation |  |
| CodeScope | CodeScope 属性标识为代码值提供唯一性范围的 bis:Element。CodeSpec、CodeScope 和 CodeValue 属性的组合对于每个 bis:Element 实例必须是唯一的。 | navigation |  |
| CodeValue | 可空字符串属性，保存 Element 代码的实际文本。CodeSpec、CodeScope 和 CodeValue 属性的组合对于每个 bis:Element 实例必须是唯一的。 | string |  |
| UserLabel | 用户给定的可选友好名称（与存储在 CodeValue 属性中的正式名称相对）。 | string |  |
| Parent | 拥有此 bis:Element 的父 bis:Element。 | navigation |  |
| FederationGuid | 用于在仓库之间联合此 bis:Element 的 GUID。 | binary | BeGuid |
| JsonProperties | 用户和/或应用程序可用于持久化临时 JSON 值的字符串属性。 | string | Json |
| Category | 用于对此 bis:GeometricElement3d 进行分类的 bis:SpatialCategory | navigation |  |
| InSpatialIndex | 如果为 true，则此元素将在空间索引中有条目。 | boolean |  |
| Origin | 此 bis:Element 的放置原点。 | point3d |  |
| Yaw | 此 bis:Element 方向的偏航角（以度为单位）。 | double |  |
| Pitch | 此 bis:Element 方向的俯仰角（以度为单位）。 | double |  |
| Roll | 此 bis:Element 方向的翻滚角（以度为单位）。 | double |  |
| BBoxLow | 此 bis:Element 的元素对齐边界框的"低"点。 | point3d |  |
| BBoxHigh | 此 bis:Element 的元素对齐边界框的"高"点。 | point3d |  |
| GeometryStream | 用于持久化此 bis:Element 几何图形的二进制流。 | binary | GeometryStream |
| TypeDefinition | 指向 TypeDefinition 的某个特化实例，该实例保存按类型而非按此 Element 实例变化的属性值。 | navigation |  |

`TerrainBreakline` 用于指定发生坡度急剧变化的线性特征，如路面边缘、沟底、山脊等。任何纵向元素都可以定义为 breakline。一个 `TerrainBreakline` 通常捕获一个这样的线性特征，但如果它们不捕获每个 breakline 特征的额外数据，则多个特征可以由单个 `TerrainBreakline` 实例捕获。

`TerrainBreakline` 将其几何细节作为线串（即无弧线）存储在其 `GeometryStream` 中，这些线串可以是开放的或闭合的。这些线串应编码为 _LineString3d_。如果单个 `TerrainBreakline` 实例正在捕获多个 breakline，则每个 breakline 应编码为 `GeometryStream` 中的单独 _LineString3d_。

默认情况下，`TerrainBreakline` 的实例应使用 Domain 级别的 `trrn:Breakline` 类别。

### __TerrainDrapeBoundary__ (地形悬垂边界) EntityClass

一个 TerrainSourceFeature，用于捕获通过悬垂在底层表面上确定其高程的表面边界。

__基类:__ Terrain:TerrainSourceFeatureElement

继承属性

| 名称 | 描述 | 类型 | 扩展类型 |
| --- | --- | --- | --- |
| Model | 包含此 bis:Element 的 bis:Model。 | navigation |  |
| LastMod | bis:Element 的最后修改时间。此属性由核心框架维护，不应由应用程序直接设置。 | dateTime |  |
| CodeSpec | CodeSpec 属性标识用于生成和验证此 bis:Element 代码值的 bis:CodeSpec。CodeSpec、CodeScope 和 CodeValue 属性的组合对于每个 bis:Element 实例必须是唯一的。 | navigation |  |
| CodeScope | CodeScope 属性标识为代码值提供唯一性范围的 bis:Element。CodeSpec、CodeScope 和 CodeValue 属性的组合对于每个 bis:Element 实例必须是唯一的。 | navigation |  |
| CodeValue | 可空字符串属性，保存 Element 代码的实际文本。CodeSpec、CodeScope 和 CodeValue 属性的组合对于每个 bis:Element 实例必须是唯一的。 | string |  |
| UserLabel | 用户给定的可选友好名称（与存储在 CodeValue 属性中的正式名称相对）。 | string |  |
| Parent | 拥有此 bis:Element 的父 bis:Element。 | navigation |  |
| FederationGuid | 用于在仓库之间联合此 bis:Element 的 GUID。 | binary | BeGuid |
| JsonProperties | 用户和/或应用程序可用于持久化临时 JSON 值的字符串属性。 | string | Json |
| Category | 用于对此 bis:GeometricElement3d 进行分类的 bis:SpatialCategory | navigation |  |
| InSpatialIndex | 如果为 true，则此元素将在空间索引中有条目。 | boolean |  |
| Origin | 此 bis:Element 的放置原点。 | point3d |  |
| Yaw | 此 bis:Element 方向的偏航角（以度为单位）。 | double |  |
| Pitch | 此 bis:Element 方向的俯仰角（以度为单位）。 | double |  |
| Roll | 此 bis:Element 方向的翻滚角（以度为单位）。 | double |  |
| BBoxLow | 此 bis:Element 的元素对齐边界框的"低"点。 | point3d |  |
| BBoxHigh | 此 bis:Element 的元素对齐边界框的"高"点。 | point3d |  |
| GeometryStream | 用于持久化此 bis:Element 几何图形的二进制流。 | binary | GeometryStream |
| TypeDefinition | 指向 TypeDefinition 的某个特化实例，该实例保存按类型而非按此 Element 实例变化的属性值。 | navigation |  |

如果地形的限制在其源上已明确定义，则每个 `Terrain` 实例预期最多有一个 `TerrainDrapeBoundary`。

`TerrainDrapeBoundary` 将其几何细节作为闭合线串（即无弧线）存储在其 `GeometryStream` 中，编码为 _LineString3d_。Z 坐标应相同（平面）。_LineString3d_ 的第一个和最后一个点应相同。

默认情况下，`TerrainDrapeBoundary` 的实例应使用 Domain 级别的 `trrn:DrapeBoundary` 类别。

### __TerrainDrapeVoid__ (地形悬垂空洞) EntityClass

一个 TerrainSourceFeature，用于捕获由闭合形状定义的区域，该区域描绘了不应使用的缺失或无效数据区域。它通过悬垂在底层表面上确定其高程。

__基类:__ Terrain:TerrainSourceFeatureElement

继承属性

| 名称 | 描述 | 类型 | 扩展类型 |
| --- | --- | --- | --- |
| Model | 包含此 bis:Element 的 bis:Model。 | navigation |  |
| LastMod | bis:Element 的最后修改时间。此属性由核心框架维护，不应由应用程序直接设置。 | dateTime |  |
| CodeSpec | CodeSpec 属性标识用于生成和验证此 bis:Element 代码值的 bis:CodeSpec。CodeSpec、CodeScope 和 CodeValue 属性的组合对于每个 bis:Element 实例必须是唯一的。 | navigation |  |
| CodeScope | CodeScope 属性标识为代码值提供唯一性范围的 bis:Element。CodeSpec、CodeScope 和 CodeValue 属性的组合对于每个 bis:Element 实例必须是唯一的。 | navigation |  |
| CodeValue | 可空字符串属性，保存 Element 代码的实际文本。CodeSpec、CodeScope 和 CodeValue 属性的组合对于每个 bis:Element 实例必须是唯一的。 | string |  |
| UserLabel | 用户给定的可选友好名称（与存储在 CodeValue 属性中的正式名称相对）。 | string |  |
| Parent | 拥有此 bis:Element 的父 bis:Element。 | navigation |  |
| FederationGuid | 用于在仓库之间联合此 bis:Element 的 GUID。 | binary | BeGuid |
| JsonProperties | 用户和/或应用程序可用于持久化临时 JSON 值的字符串属性。 | string | Json |
| Category | 用于对此 bis:GeometricElement3d 进行分类的 bis:SpatialCategory | navigation |  |
| InSpatialIndex | 如果为 true，则此元素将在空间索引中有条目。 | boolean |  |
| Origin | 此 bis:Element 的放置原点。 | point3d |  |
| Yaw | 此 bis:Element 方向的偏航角（以度为单位）。 | double |  |
| Pitch | 此 bis:Element 方向的俯仰角（以度为单位）。 | double |  |
| Roll | 此 bis:Element 方向的翻滚角（以度为单位）。 | double |  |
| BBoxLow | 此 bis:Element 的元素对齐边界框的"低"点。 | point3d |  |
| BBoxHigh | 此 bis:Element 的元素对齐边界框的"高"点。 | point3d |  |
| GeometryStream | 用于持久化此 bis:Element 几何图形的二进制流。 | binary | GeometryStream |
| TypeDefinition | 指向 TypeDefinition 的某个特化实例，该实例保存按类型而非按此 Element 实例变化的属性值。 | navigation |  |

`TerrainVoid` 描述的相同限制也适用于 `TerrainDrapeVoid`。

`TerrainDrapeVoid` 将其几何细节作为闭合线串（即无弧线）存储在其 `GeometryStream` 中，编码为 _LineString3d_。Z 坐标应相同（平面）。_LineString3d_ 的第一个和最后一个点应相同。如果单个 `TerrainVoid` 实例正在捕获多个 void 特征，则每个 void 特征应编码为 `GeometryStream` 中的单独 _LineString3d_。

默认情况下，`TerrainVoid` 的实例应使用 Domain 级别的 `trrn:Void` 类别。

### __TerrainHole__ (地形孔洞) EntityClass

一个 TerrainSourceFeature，用于捕获由闭合形状定义的区域，该区域描绘了忽略当前地形并使用底层地形的区域。

__基类:__ Terrain:TerrainSourceFeatureElement

继承属性

| 名称 | 描述 | 类型 | 扩展类型 |
| --- | --- | --- | --- |
| Model | 包含此 bis:Element 的 bis:Model。 | navigation |  |
| LastMod | bis:Element 的最后修改时间。此属性由核心框架维护，不应由应用程序直接设置。 | dateTime |  |
| CodeSpec | CodeSpec 属性标识用于生成和验证此 bis:Element 代码值的 bis:CodeSpec。CodeSpec、CodeScope 和 CodeValue 属性的组合对于每个 bis:Element 实例必须是唯一的。 | navigation |  |
| CodeScope | CodeScope 属性标识为代码值提供唯一性范围的 bis:Element。CodeSpec、CodeScope 和 CodeValue 属性的组合对于每个 bis:Element 实例必须是唯一的。 | navigation |  |
| CodeValue | 可空字符串属性，保存 Element 代码的实际文本。CodeSpec、CodeScope 和 CodeValue 属性的组合对于每个 bis:Element 实例必须是唯一的。 | string |  |
| UserLabel | 用户给定的可选友好名称（与存储在 CodeValue 属性中的正式名称相对）。 | string |  |
| Parent | 拥有此 bis:Element 的父 bis:Element。 | navigation |  |
| FederationGuid | 用于在仓库之间联合此 bis:Element 的 GUID。 | binary | BeGuid |
| JsonProperties | 用户和/或应用程序可用于持久化临时 JSON 值的字符串属性。 | string | Json |
| Category | 用于对此 bis:GeometricElement3d 进行分类的 bis:SpatialCategory | navigation |  |
| InSpatialIndex | 如果为 true，则此元素将在空间索引中有条目。 | boolean |  |
| Origin | 此 bis:Element 的放置原点。 | point3d |  |
| Yaw | 此 bis:Element 方向的偏航角（以度为单位）。 | double |  |
| Pitch | 此 bis:Element 方向的俯仰角（以度为单位）。 | double |  |
| Roll | 此 bis:Element 方向的翻滚角（以度为单位）。 | double |  |
| BBoxLow | 此 bis:Element 的元素对齐边界框的"低"点。 | point3d |  |
| BBoxHigh | 此 bis:Element 的元素对齐边界框的"高"点。 | point3d |  |
| GeometryStream | 用于持久化此 bis:Element 几何图形的二进制流。 | binary | GeometryStream |
| TypeDefinition | 指向 TypeDefinition 的某个特化实例，该实例保存按类型而非按此 Element 实例变化的属性值。 | navigation |  |

`TerrainHole` 可用于标记不使用或不显示的 Terrain 区域。TerrainHole 通常用于标记不打算使用的设计地形区域。一个 `TerrainHole` 通常捕获一个 hole 特征，但如果它们不捕获每个 hole 特征的额外数据，则多个特征可以由单个 `TerrainHole` 实例捕获。

`TerrainHole` 将其几何细节作为闭合线串（即无弧线）存储在其 `GeometryStream` 中，编码为单个 _LineString3d_。_LineString3d_ 的第一个和最后一个点应相同。如果单个 `TerrainHole` 实例正在捕获多个 hole 特征，则每个 hole 特征应编码为 `GeometryStream` 中的单独 _LineString3d_。

默认情况下，`TerrainHole` 的实例应使用 Domain 级别的 `trrn:Hole` 类别。

### __TerrainIsland__ (地形岛屿) EntityClass

一个 TerrainSourceFeature，用于捕获由闭合形状定义的区域，该区域标示了地形空洞内存在数据的区域。

__基类:__ Terrain:TerrainSourceFeatureElement

继承属性

| 名称 | 描述 | 类型 | 扩展类型 |
| --- | --- | --- | --- |
| Model | 包含此 bis:Element 的 bis:Model。 | navigation |  |
| LastMod | bis:Element 的最后修改时间。此属性由核心框架维护，不应由应用程序直接设置。 | dateTime |  |
| CodeSpec | CodeSpec 属性标识用于生成和验证此 bis:Element 代码值的 bis:CodeSpec。CodeSpec、CodeScope 和 CodeValue 属性的组合对于每个 bis:Element 实例必须是唯一的。 | navigation |  |
| CodeScope | CodeScope 属性标识为代码值提供唯一性范围的 bis:Element。CodeSpec、CodeScope 和 CodeValue 属性的组合对于每个 bis:Element 实例必须是唯一的。 | navigation |  |
| CodeValue | 可空字符串属性，保存 Element 代码的实际文本。CodeSpec、CodeScope 和 CodeValue 属性的组合对于每个 bis:Element 实例必须是唯一的。 | string |  |
| UserLabel | 用户给定的可选友好名称（与存储在 CodeValue 属性中的正式名称相对）。 | string |  |
| Parent | 拥有此 bis:Element 的父 bis:Element。 | navigation |  |
| FederationGuid | 用于在仓库之间联合此 bis:Element 的 GUID。 | binary | BeGuid |
| JsonProperties | 用户和/或应用程序可用于持久化临时 JSON 值的字符串属性。 | string | Json |
| Category | 用于对此 bis:GeometricElement3d 进行分类的 bis:SpatialCategory | navigation |  |
| InSpatialIndex | 如果为 true，则此元素将在空间索引中有条目。 | boolean |  |
| Origin | 此 bis:Element 的放置原点。 | point3d |  |
| Yaw | 此 bis:Element 方向的偏航角（以度为单位）。 | double |  |
| Pitch | 此 bis:Element 方向的俯仰角（以度为单位）。 | double |  |
| Roll | 此 bis:Element 方向的翻滚角（以度为单位）。 | double |  |
| BBoxLow | 此 bis:Element 的元素对齐边界框的"低"点。 | point3d |  |
| BBoxHigh | 此 bis:Element 的元素对齐边界框的"高"点。 | point3d |  |
| GeometryStream | 用于持久化此 bis:Element 几何图形的二进制流。 | binary | GeometryStream |
| TypeDefinition | 指向 TypeDefinition 的某个特化实例，该实例保存按类型而非按此 Element 实例变化的属性值。 | navigation |  |

一个 `TerrainIsland` 通常捕获一个 island 特征，但如果它们不捕获每个 island 特征的额外数据，则多个特征可以由单个 `TerrainIsland` 实例捕获。

`TerrainIsland` 将其几何细节作为闭合线串（即无弧线）存储在其 `GeometryStream` 中，编码为 _LineString3d_。_LineString3d_ 的第一个和最后一个点应相同。如果单个 `TerrainIsland` 实例正在捕获多个 island 特征，则每个 island 特征应编码为 `GeometryStream` 中的单独 _LineString3d_。

默认情况下，`TerrainIsland` 的实例应使用 Domain 级别的 `trrn:Island` 类别。

### __TerrainReference__ (地形引用) EntityClass

对 `bis:RepositoryLink` 的引用，捕获为地球一部分提供基础地形的服务位置。

__基类:__ BisCore:PhysicalElement

`TerrainReference` 中的地形数据始终由服务提供，但可以在本地缓存。提供 `TerrainReference` 的服务位置由存储在 iModel 全局 `RealityDataSourcesModel` 中的 `RepositoryLink` 实例捕获。该实例通过 `RepositoryLink` 导航属性引用。

当多个 `TerrainReference` 重叠时，将使用具有最高 `Priority` 的 `TerrainReference`。

`TerrainReference` 必须包含在 `PhysicalModel` 中。选择包含 `Model` 有以下影响：

- 地形的可见性与 `Model` 中其他 `Element` 的可见性一起控制。
- 这意味着负责 `Model` 中其他 `Element` 的一方也负责 `TerrainReference`。

每个 `TerrainReference` 都有一个在关联的 `RealityDataMask` 元素中捕获的 _Footprint_。此 _Footprint_ 用于裁剪具有较低优先级的 `TerrainReference` 的重叠区域。

![Terrain 实例](https://www.itwinjs.org/media/terrain-instances.png)

#### 属性

| 名称 | 描述 | 类型 | 扩展类型 |
| --- | --- | --- | --- |
| RepositoryLink | 对捕获提供地形的服务位置的 bis:RepositoryLink 的引用。 | navigation |  |
| Priority | 此 ITerrain 相对于其他 ITerrain 的相对优先级。当 ITerrain 重叠时，使用具有较大 Priority 的那个。 | int |  |

继承属性

| 名称 | 描述 | 类型 | 扩展类型 |
| --- | --- | --- | --- |
| Model | 包含此 bis:Element 的 bis:Model。 | navigation |  |
| LastMod | bis:Element 的最后修改时间。此属性由核心框架维护，不应由应用程序直接设置。 | dateTime |  |
| CodeSpec | CodeSpec 属性标识用于生成和验证此 bis:Element 代码值的 bis:CodeSpec。CodeSpec、CodeScope 和 CodeValue 属性的组合对于每个 bis:Element 实例必须是唯一的。 | navigation |  |
| CodeScope | CodeScope 属性标识为代码值提供唯一性范围的 bis:Element。CodeSpec、CodeScope 和 CodeValue 属性的组合对于每个 bis:Element 实例必须是唯一的。 | navigation |  |
| CodeValue | 可空字符串属性，保存 Element 代码的实际文本。CodeSpec、CodeScope 和 CodeValue 属性的组合对于每个 bis:Element 实例必须是唯一的。 | string |  |
| UserLabel | 用户给定的可选友好名称（与存储在 CodeValue 属性中的正式名称相对）。 | string |  |
| Parent | 拥有此 bis:Element 的父 bis:Element。 | navigation |  |
| FederationGuid | 用于在仓库之间联合此 bis:Element 的 GUID。 | binary | BeGuid |
| JsonProperties | 用户和/或应用程序可用于持久化临时 JSON 值的字符串属性。 | string | Json |
| Category | 用于对此 bis:GeometricElement3d 进行分类的 bis:SpatialCategory | navigation |  |
| InSpatialIndex | 如果为 true，则此元素将在空间索引中有条目。 | boolean |  |
| Origin | 此 bis:Element 的放置原点。 | point3d |  |
| Yaw | 此 bis:Element 方向的偏航角（以度为单位）。 | double |  |
| Pitch | 此 bis:Element 方向的俯仰角（以度为单位）。 | double |  |
| Roll | 此 bis:Element 方向的翻滚角（以度为单位）。 | double |  |
| BBoxLow | 此 bis:Element 的元素对齐边界框的"低"点。 | point3d |  |
| BBoxHigh | 此 bis:Element 的元素对齐边界框的"高"点。 | point3d |  |
| GeometryStream | 用于持久化此 bis:Element 几何图形的二进制流。 | binary | GeometryStream |
| TypeDefinition | 指向 TypeDefinition 的某个特化实例，该实例保存按类型而非按此 Element 实例变化的属性值。 | navigation |  |
| PhysicalMaterial | 指示构成 bis:PhysicalElement 的 bis:PhysicalMaterial。 | navigation |  |

### __TerrainSourceContour__ (地形源等高线) EntityClass

一个 TerrainSourceFeature，用于捕获作为地形源数据创建的相同高程的线性元素。

__基类:__ Terrain:TerrainSourceFeatureElement

继承属性

| 名称 | 描述 | 类型 | 扩展类型 |
| --- | --- | --- | --- |
| Model | 包含此 bis:Element 的 bis:Model。 | navigation |  |
| LastMod | bis:Element 的最后修改时间。此属性由核心框架维护，不应由应用程序直接设置。 | dateTime |  |
| CodeSpec | CodeSpec 属性标识用于生成和验证此 bis:Element 代码值的 bis:CodeSpec。CodeSpec、CodeScope 和 CodeValue 属性的组合对于每个 bis:Element 实例必须是唯一的。 | navigation |  |
| CodeScope | CodeScope 属性标识为代码值提供唯一性范围的 bis:Element。CodeSpec、CodeScope 和 CodeValue 属性的组合对于每个 bis:Element 实例必须是唯一的。 | navigation |  |
| CodeValue | 可空字符串属性，保存 Element 代码的实际文本。CodeSpec、CodeScope 和 CodeValue 属性的组合对于每个 bis:Element 实例必须是唯一的。 | string |  |
| UserLabel | 用户给定的可选友好名称（与存储在 CodeValue 属性中的正式名称相对）。 | string |  |
| Parent | 拥有此 bis:Element 的父 bis:Element。 | navigation |  |
| FederationGuid | 用于在仓库之间联合此 bis:Element 的 GUID。 | binary | BeGuid |
| JsonProperties | 用户和/或应用程序可用于持久化临时 JSON 值的字符串属性。 | string | Json |
| Category | 用于对此 bis:GeometricElement3d 进行分类的 bis:SpatialCategory | navigation |  |
| InSpatialIndex | 如果为 true，则此元素将在空间索引中有条目。 | boolean |  |
| Origin | 此 bis:Element 的放置原点。 | point3d |  |
| Yaw | 此 bis:Element 方向的偏航角（以度为单位）。 | double |  |
| Pitch | 此 bis:Element 方向的俯仰角（以度为单位）。 | double |  |
| Roll | 此 bis:Element 方向的翻滚角（以度为单位）。 | double |  |
| BBoxLow | 此 bis:Element 的元素对齐边界框的"低"点。 | point3d |  |
| BBoxHigh | 此 bis:Element 的元素对齐边界框的"高"点。 | point3d |  |
| GeometryStream | 用于持久化此 bis:Element 几何图形的二进制流。 | binary | GeometryStream |
| TypeDefinition | 指向 TypeDefinition 的某个特化实例，该实例保存按类型而非按此 Element 实例变化的属性值。 | navigation |  |

一个 `TerrainSourceContour` 通常捕获一条等高线，但如果它们不捕获每条等高线的额外数据，则多条等高线可以由单个 `TerrainSourceContour` 实例捕获。

`TerrainSourceContour` 将其几何细节作为开放或闭合线串（即无弧线）存储在其 `GeometryStream` 中，编码为 _LineString3d_。如果是闭合的，则 _LineString3d_ 的第一个和最后一个点应相同。如果单个 `TerrainSourceContour` 实例正在捕获多条等高线，则每条等高线应编码为 `GeometryStream` 中的单独 _LineString3d_。

默认情况下，`TerrainSourceContour` 的实例应使用 Domain 级别的 `trrn:SourceContour` 类别。

### __TerrainSourceFeatureElement__ _Abstract_ EntityClass

一个 `bis:SpatialLocationElement`，作为捕获父 Terrain 元素特定细节的元素的基类，这些细节来自用于创建 Terrain 元素的源数据。

__基类:__ BisCore:SpatialLocationElement

继承属性

| 名称 | 描述 | 类型 | 扩展类型 |
| --- | --- | --- | --- |
| Model | 包含此 bis:Element 的 bis:Model。 | navigation |  |
| LastMod | bis:Element 的最后修改时间。此属性由核心框架维护，不应由应用程序直接设置。 | dateTime |  |
| CodeSpec | CodeSpec 属性标识用于生成和验证此 bis:Element 代码值的 bis:CodeSpec。CodeSpec、CodeScope 和 CodeValue 属性的组合对于每个 bis:Element 实例必须是唯一的。 | navigation |  |
| CodeScope | CodeScope 属性标识为代码值提供唯一性范围的 bis:Element。CodeSpec、CodeScope 和 CodeValue 属性的组合对于每个 bis:Element 实例必须是唯一的。 | navigation |  |
| CodeValue | 可空字符串属性，保存 Element 代码的实际文本。CodeSpec、CodeScope 和 CodeValue 属性的组合对于每个 bis:Element 实例必须是唯一的。 | string |  |
| UserLabel | 用户给定的可选友好名称（与存储在 CodeValue 属性中的正式名称相对）。 | string |  |
| Parent | 拥有此 bis:Element 的父 bis:Element。 | navigation |  |
| FederationGuid | 用于在仓库之间联合此 bis:Element 的 GUID。 | binary | BeGuid |
| JsonProperties | 用户和/或应用程序可用于持久化临时 JSON 值的字符串属性。 | string | Json |
| Category | 用于对此 bis:GeometricElement3d 进行分类的 bis:SpatialCategory | navigation |  |
| InSpatialIndex | 如果为 true，则此元素将在空间索引中有条目。 | boolean |  |
| Origin | 此 bis:Element 的放置原点。 | point3d |  |
| Yaw | 此 bis:Element 方向的偏航角（以度为单位）。 | double |  |
| Pitch | 此 bis:Element 方向的俯仰角（以度为单位）。 | double |  |
| Roll | 此 bis:Element 方向的翻滚角（以度为单位）。 | double |  |
| BBoxLow | 此 bis:Element 的元素对齐边界框的"低"点。 | point3d |  |
| BBoxHigh | 此 bis:Element 的元素对齐边界框的"高"点。 | point3d |  |
| GeometryStream | 用于持久化此 bis:Element 几何图形的二进制流。 | binary | GeometryStream |
| TypeDefinition | 指向 TypeDefinition 的某个特化实例，该实例保存按类型而非按此 Element 实例变化的属性值。 | navigation |  |

`TerrainSourceFeatureElement` 将其几何细节存储在其 `GeometryStream` 中。

### __TerrainSpotElevation__ (地形高程点) EntityClass

一个 TerrainSourceFeature，用于捕获与地形中任何其他点没有功能关系的特定点位置。

__基类:__ Terrain:TerrainSourceFeatureElement

继承属性

| 名称 | 描述 | 类型 | 扩展类型 |
| --- | --- | --- | --- |
| Model | 包含此 bis:Element 的 bis:Model。 | navigation |  |
| LastMod | bis:Element 的最后修改时间。此属性由核心框架维护，不应由应用程序直接设置。 | dateTime |  |
| CodeSpec | CodeSpec 属性标识用于生成和验证此 bis:Element 代码值的 bis:CodeSpec。CodeSpec、CodeScope 和 CodeValue 属性的组合对于每个 bis:Element 实例必须是唯一的。 | navigation |  |
| CodeScope | CodeScope 属性标识为代码值提供唯一性范围的 bis:Element。CodeSpec、CodeScope 和 CodeValue 属性的组合对于每个 bis:Element 实例必须是唯一的。 | navigation |  |
| CodeValue | 可空字符串属性，保存 Element 代码的实际文本。CodeSpec、CodeScope 和 CodeValue 属性的组合对于每个 bis:Element 实例必须是唯一的。 | string |  |
| UserLabel | 用户给定的可选友好名称（与存储在 CodeValue 属性中的正式名称相对）。 | string |  |
| Parent | 拥有此 bis:Element 的父 bis:Element。 | navigation |  |
| FederationGuid | 用于在仓库之间联合此 bis:Element 的 GUID。 | binary | BeGuid |
| JsonProperties | 用户和/或应用程序可用于持久化临时 JSON 值的字符串属性。 | string | Json |
| Category | 用于对此 bis:GeometricElement3d 进行分类的 bis:SpatialCategory | navigation |  |
| InSpatialIndex | 如果为 true，则此元素将在空间索引中有条目。 | boolean |  |
| Origin | 此 bis:Element 的放置原点。 | point3d |  |
| Yaw | 此 bis:Element 方向的偏航角（以度为单位）。 | double |  |
| Pitch | 此 bis:Element 方向的俯仰角（以度为单位）。 | double |  |
| Roll | 此 bis:Element 方向的翻滚角（以度为单位）。 | double |  |
| BBoxLow | 此 bis:Element 的元素对齐边界框的"低"点。 | point3d |  |
| BBoxHigh | 此 bis:Element 的元素对齐边界框的"高"点。 | point3d |  |
| GeometryStream | 用于持久化此 bis:Element 几何图形的二进制流。 | binary | GeometryStream |
| TypeDefinition | 指向 TypeDefinition 的某个特化实例，该实例保存按类型而非按此 Element 实例变化的属性值。 | navigation |  |

一个 `TerrainSpotElevation` 通常捕获一个点，但如果它们不捕获每个高程点的额外数据，则多个点可以由单个 `TerrainSpotElevation` 实例捕获。

`TerrainSpotElevation` 将其几何细节作为 _PointString3d_ 存储在其 `GeometryStream` 中。`TerrainSpotElevation` 捕获的高程可以从 _PointString3d_ 中每个点的 Z 坐标读取。如果单个 `TerrainSpotElevation` 实例仅捕获一个 Spot elevation，则其 `GeometryStream` 应包含只有一个点的 _PointString3d_。

默认情况下，`TerrainSpotElevation` 的实例应使用 Domain 级别的 `trrn:SpotElevation` 类别。

### __TerrainVoid__ (地形空洞) EntityClass

一个 TerrainSourceFeature，用于捕获由闭合形状定义的区域，该区域描绘了不应使用的缺失或无效数据区域。

__基类:__ Terrain:TerrainSourceFeatureElement

继承属性

| 名称 | 描述 | 类型 | 扩展类型 |
| --- | --- | --- | --- |
| Model | 包含此 bis:Element 的 bis:Model。 | navigation |  |
| LastMod | bis:Element 的最后修改时间。此属性由核心框架维护，不应由应用程序直接设置。 | dateTime |  |
| CodeSpec | CodeSpec 属性标识用于生成和验证此 bis:Element 代码值的 bis:CodeSpec。CodeSpec、CodeScope 和 CodeValue 属性的组合对于每个 bis:Element 实例必须是唯一的。 | navigation |  |
| CodeScope | CodeScope 属性标识为代码值提供唯一性范围的 bis:Element。CodeSpec、CodeScope 和 CodeValue 属性的组合对于每个 bis:Element 实例必须是唯一的。 | navigation |  |
| CodeValue | 可空字符串属性，保存 Element 代码的实际文本。CodeSpec、CodeScope 和 CodeValue 属性的组合对于每个 bis:Element 实例必须是唯一的。 | string |  |
| UserLabel | 用户给定的可选友好名称（与存储在 CodeValue 属性中的正式名称相对）。 | string |  |
| Parent | 拥有此 bis:Element 的父 bis:Element。 | navigation |  |
| FederationGuid | 用于在仓库之间联合此 bis:Element 的 GUID。 | binary | BeGuid |
| JsonProperties | 用户和/或应用程序可用于持久化临时 JSON 值的字符串属性。 | string | Json |
| Category | 用于对此 bis:GeometricElement3d 进行分类的 bis:SpatialCategory | navigation |  |
| InSpatialIndex | 如果为 true，则此元素将在空间索引中有条目。 | boolean |  |
| Origin | 此 bis:Element 的放置原点。 | point3d |  |
| Yaw | 此 bis:Element 方向的偏航角（以度为单位）。 | double |  |
| Pitch | 此 bis:Element 方向的俯仰角（以度为单位）。 | double |  |
| Roll | 此 bis:Element 方向的翻滚角（以度为单位）。 | double |  |
| BBoxLow | 此 bis:Element 的元素对齐边界框的"低"点。 | point3d |  |
| BBoxHigh | 此 bis:Element 的元素对齐边界框的"高"点。 | point3d |  |
| GeometryStream | 用于持久化此 bis:Element 几何图形的二进制流。 | binary | GeometryStream |
| TypeDefinition | 指向 TypeDefinition 的某个特化实例，该实例保存按类型而非按此 Element 实例变化的属性值。 | navigation |  |

位于 `TerrainVoid` 区域内的 `TerrainSpotElevation` 或 `TerrainBreakline` 将被忽略。也就是说，不使用位于空洞区域内的点或 breakline 数据，并且不在空洞区域内创建三角形。void 坐标包含在三角剖分中，连续 void 坐标之间的 void 线作为 drape line 插入到表面上。因此，它们不会改变表面的坡度或高程。`TerrainVoid` 永远不会覆盖 `TerrainIsland`。

一个 `TerrainVoid` 通常捕获一个 void 特征，但如果它们不捕获每个 void 特征的额外数据，则多个特征可以由单个 `TerrainVoid` 实例捕获。

`TerrainVoid` 将其几何细节作为闭合线串（即无弧线）存储在其 `GeometryStream` 中，编码为 _LineString3d_。_LineString3d_ 的第一个和最后一个点应相同。如果单个 `TerrainVoid` 实例正在捕获多个 void 特征，则每个 void 特征应编码为 `GeometryStream` 中的单独 _LineString3d_。

默认情况下，`TerrainVoid` 的实例应使用 Domain 级别的 `trrn:Void` 类别。

## Mixins

### __ITerrain__ _Abstract_ Mixin

由 `bis:PhysicalElement` 子类支持的 mix-in，用于对地球一部分的基础地形进行建模。

__应用于:__ PhysicalElement

`ITerrain` 是一个通用的 mix-in，预期由为资产和项目定义静态 _context_ 的 element-class 实现。

iModel 中有三种地形类型：

1. _Background Default Terrain_（在 iModel 设置中定义）
2. `TerrainReference`
3. `Terrain`

`TerrainReference` 和 `Terrain` 实现 `ITerrain`。这三种地形类型的交互方式如下。

_Background Default Terrain_ 来自服务（通常是 Cesium World Terrain）。此背景地形通常在全球范围内可用。对于 iModel，在没有定义其他地形的地方使用 _Background Default Terrain_。

`TerrainReference` 也从服务提供地形，而 `Terrain` 在 iModel 本身中完全捕获地形。

由 `TerrainReference` 和 `Terrain` 定义的地形通常来自专门为所考虑的项目或资产捕获的数据，通常比 _Background Default Terrain_ 提供的地形更准确和/或更及时。

`TerrainReference` 和 `Terrain` 在重叠的地方总是替代 _Background Default Terrain_ 使用。在许多大型项目中，将提供多个 `TerrainReference` 和 `Terrain`。例如，一个 `TerrainReference` 可以为整个项目场地提供低分辨率地形，而其他 `Terrain` 可以为大部分工作将发生的重点区域定义高分辨率地形。在 `TerrainReference` 和 `Terrain` 重叠的地方，将使用 `Terrain` 元素。

在 Digital Twins 中，所有三种类型的地形都可以为基础设施提供 context 或场地的起始（或当前）条件，但更典型的是由 _Background Default Terrain_ 和 `TerrainReference` 来提供。

## Relationship Classes

### __ITerrainOwnsBoundary__ RelationshipClass

__基类:__ BisCore:ElementOwnsChildElements

__强度:__ Embedding

__强度方向:__ Forward

#### Source

__Is Polymorphic:__ true

__角色标签:__ owns

__多重性:__ (0..1)

#### 约束类:

- ITerrain

#### Target

__Is Polymorphic:__ true

__角色标签:__ is owned by

__多重性:__ (0..*)

#### 约束类:

- TerrainBoundary

### __TerrainOwnsSourceFeatures__ RelationshipClass

### __TerrainReferenceViaRepositoryLink__ RelationshipClass

使 TerrainReference 能够引用捕获提供其详细信息的服务位置的 bis:RepositoryLink 的关系。

__强度:__ Referencing

__强度方向:__ Forward

#### Source

__Is Polymorphic:__ true

__角色标签:__ refers to

__多重性:__ (0..*)

#### 约束类:

- TerrainReference

#### Target

__Is Polymorphic:__ true

__角色标签:__ is referenced by

__多重性:__ (0..1)

#### 约束类:

- RepositoryLink
