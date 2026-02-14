# Generic Schema

**别名：** generic

**版本：** 1.0.5

此 schema 包含完全通用的类。仅当没有足够的上下文来选择更具体的类时，才应使用这些类。

## 目录

- 实体类 (Entity Classes)
  - Callout
  - DetailCallout
  - DetailingSymbol
  - Document
  - ElevationCallout
  - Graphic3d
  - GraphicalModel3d
  - GraphicalType2d
  - Group
  - GroupModel
  - PhysicalMaterial
  - PhysicalObject
  - PhysicalType
  - PlanCallout
  - SectionCallout
  - SpatialLocation
  - SpatialLocationType
  - TitleText
  - ViewAttachmentLabel
- 关系类 (Relationship Classes)
  - CalloutRefersToDrawingModel
  - ViewAttachmentLabelAnnotatesViewAttachment

## 实体类 (Entity Classes)

### __Callout__ _抽象_ EntityClass

一个 generic:DetailingSymbol，用于标注对另一个 bis:Drawing 的引用。

**基类：** Generic:DetailingSymbol

#### 属性

| 名称 | 描述 | 类型 | 扩展类型 |
| --- | --- | --- | --- |
| DrawingModel |  | navigation |  |

继承属性

| 名称 | 描述 | 类型 | 扩展类型 |
| --- | --- | --- | --- |
| Model | 包含此 bis:Element 的 bis:Model。 | navigation |  |
| LastMod | bis:Element 的最后修改时间。此属性由核心框架维护，应用程序不应直接设置。 | dateTime |  |
| CodeSpec | CodeSpec 属性标识用于生成和验证此 bis:Element 代码值的 bis:CodeSpec。每个 bis:Element 实例的 CodeSpec、CodeScope 和 CodeValue 属性组合必须唯一。 | navigation |  |
| CodeScope | CodeScope 属性标识为代码值提供唯一性范围的 bis:Element。每个 bis:Element 实例的 CodeSpec、CodeScope 和 CodeValue 属性组合必须唯一。 | navigation |  |
| CodeValue | 可空字符串属性，保存 Element 的 Code 的实际文本。每个 bis:Element 实例的 CodeSpec、CodeScope 和 CodeValue 属性组合必须唯一。 | string |  |
| UserLabel | 用户提供的可选友好名称（与存储在 CodeValue 属性中的正式名称相对）。 | string |  |
| Parent | 拥有此 bis:Element 的父 bis:Element。 | navigation |  |
| FederationGuid | 用于跨仓库联合此 bis:Element 的 GUID。 | binary | BeGuid |
| JsonProperties | 用户和/或应用程序可用于持久化临时 JSON 值的字符串属性。 | string | Json |
| Category | 用于对此 bis:GeometricElement2d 实例进行分类的 bis:DrawingCategory。 | navigation |  |
| Origin | 此 bis:Element 的放置原点。 | point2d |  |
| Rotation | 此 bis:Element 的放置旋转角度（以度为单位）。 | double |  |
| BBoxLow | 此 bis:Element 的元素对齐边界框的"低"点。 | point2d |  |
| BBoxHigh | 此 bis:Element 的元素对齐边界框的"高"点。 | point2d |  |
| GeometryStream | 用于持久化此 bis:Element 几何图形的二进制流。 | binary | GeometryStream |
| TypeDefinition | 指向 TypeDefinition 的某个特化实例，该实例保存按类型而非按此 Element 实例变化的属性值。 | navigation |  |

### __DetailCallout__ (Detail Callout) _密封_ EntityClass

一个 generic:Callout，用于标注对详图图纸的引用。

**基类：** Generic:Callout

继承属性

| 名称 | 描述 | 类型 | 扩展类型 |
| --- | --- | --- | --- |
| Model | 包含此 bis:Element 的 bis:Model。 | navigation |  |
| LastMod | bis:Element 的最后修改时间。此属性由核心框架维护，应用程序不应直接设置。 | dateTime |  |
| CodeSpec | CodeSpec 属性标识用于生成和验证此 bis:Element 代码值的 bis:CodeSpec。每个 bis:Element 实例的 CodeSpec、CodeScope 和 CodeValue 属性组合必须唯一。 | navigation |  |
| CodeScope | CodeScope 属性标识为代码值提供唯一性范围的 bis:Element。每个 bis:Element 实例的 CodeSpec、CodeScope 和 CodeValue 属性组合必须唯一。 | navigation |  |
| CodeValue | 可空字符串属性，保存 Element 的 Code 的实际文本。每个 bis:Element 实例的 CodeSpec、CodeScope 和 CodeValue 属性组合必须唯一。 | string |  |
| UserLabel | 用户提供的可选友好名称（与存储在 CodeValue 属性中的正式名称相对）。 | string |  |
| Parent | 拥有此 bis:Element 的父 bis:Element。 | navigation |  |
| FederationGuid | 用于跨仓库联合此 bis:Element 的 GUID。 | binary | BeGuid |
| JsonProperties | 用户和/或应用程序可用于持久化临时 JSON 值的字符串属性。 | string | Json |
| Category | 用于对此 bis:GeometricElement2d 实例进行分类的 bis:DrawingCategory。 | navigation |  |
| Origin | 此 bis:Element 的放置原点。 | point2d |  |
| Rotation | 此 bis:Element 的放置旋转角度（以度为单位）。 | double |  |
| BBoxLow | 此 bis:Element 的元素对齐边界框的"低"点。 | point2d |  |
| BBoxHigh | 此 bis:Element 的元素对齐边界框的"高"点。 | point2d |  |
| GeometryStream | 用于持久化此 bis:Element 几何图形的二进制流。 | binary | GeometryStream |
| TypeDefinition | 指向 TypeDefinition 的某个特化实例，该实例保存按类型而非按此 Element 实例变化的属性值。 | navigation |  |
| DrawingModel |  | navigation |  |

### __DetailingSymbol__ (Detailing Symbol) _抽象_ EntityClass

放置在 bis:Drawing 或 bis:Sheet 上的图形详图符号。

**基类：** BisCore:GraphicalElement2d

继承属性

| 名称 | 描述 | 类型 | 扩展类型 |
| --- | --- | --- | --- |
| Model | 包含此 bis:Element 的 bis:Model。 | navigation |  |
| LastMod | bis:Element 的最后修改时间。此属性由核心框架维护，应用程序不应直接设置。 | dateTime |  |
| CodeSpec | CodeSpec 属性标识用于生成和验证此 bis:Element 代码值的 bis:CodeSpec。每个 bis:Element 实例的 CodeSpec、CodeScope 和 CodeValue 属性组合必须唯一。 | navigation |  |
| CodeScope | CodeScope 属性标识为代码值提供唯一性范围的 bis:Element。每个 bis:Element 实例的 CodeSpec、CodeScope 和 CodeValue 属性组合必须唯一。 | navigation |  |
| CodeValue | 可空字符串属性，保存 Element 的 Code 的实际文本。每个 bis:Element 实例的 CodeSpec、CodeScope 和 CodeValue 属性组合必须唯一。 | string |  |
| UserLabel | 用户提供的可选友好名称（与存储在 CodeValue 属性中的正式名称相对）。 | string |  |
| Parent | 拥有此 bis:Element 的父 bis:Element。 | navigation |  |
| FederationGuid | 用于跨仓库联合此 bis:Element 的 GUID。 | binary | BeGuid |
| JsonProperties | 用户和/或应用程序可用于持久化临时 JSON 值的字符串属性。 | string | Json |
| Category | 用于对此 bis:GeometricElement2d 实例进行分类的 bis:DrawingCategory。 | navigation |  |
| Origin | 此 bis:Element 的放置原点。 | point2d |  |
| Rotation | 此 bis:Element 的放置旋转角度（以度为单位）。 | double |  |
| BBoxLow | 此 bis:Element 的元素对齐边界框的"低"点。 | point2d |  |
| BBoxHigh | 此 bis:Element 的元素对齐边界框的"高"点。 | point2d |  |
| GeometryStream | 用于持久化此 bis:Element 几何图形的二进制流。 | binary | GeometryStream |
| TypeDefinition | 指向 TypeDefinition 的某个特化实例，该实例保存按类型而非按此 Element 实例变化的属性值。 | navigation |  |

### __Document__ _密封_ EntityClass

generic:Document 类用于无法进一步分类的 bis:Document 元素。应尽可能使用更具体的 bis:Document 子类。

**基类：** BisCore:Document

继承属性

| 名称 | 描述 | 类型 | 扩展类型 |
| --- | --- | --- | --- |
| Model | 包含此 bis:Element 的 bis:Model。 | navigation |  |
| LastMod | bis:Element 的最后修改时间。此属性由核心框架维护，应用程序不应直接设置。 | dateTime |  |
| CodeSpec | CodeSpec 属性标识用于生成和验证此 bis:Element 代码值的 bis:CodeSpec。每个 bis:Element 实例的 CodeSpec、CodeScope 和 CodeValue 属性组合必须唯一。 | navigation |  |
| CodeScope | CodeScope 属性标识为代码值提供唯一性范围的 bis:Element。每个 bis:Element 实例的 CodeSpec、CodeScope 和 CodeValue 属性组合必须唯一。 | navigation |  |
| CodeValue | 可空字符串属性，保存 Element 的 Code 的实际文本。每个 bis:Element 实例的 CodeSpec、CodeScope 和 CodeValue 属性组合必须唯一。 | string |  |
| UserLabel | 用户提供的可选友好名称（与存储在 CodeValue 属性中的正式名称相对）。 | string |  |
| Parent | 拥有此 bis:Element 的父 bis:Element。 | navigation |  |
| FederationGuid | 用于跨仓库联合此 bis:Element 的 GUID。 | binary | BeGuid |
| JsonProperties | 用户和/或应用程序可用于持久化临时 JSON 值的字符串属性。 | string | Json |

### __ElevationCallout__ (Elevation Callout) _密封_ EntityClass

一个 generic:Callout，用于标注对立面图纸的引用。

**基类：** Generic:Callout

继承属性

| 名称 | 描述 | 类型 | 扩展类型 |
| --- | --- | --- | --- |
| Model | 包含此 bis:Element 的 bis:Model。 | navigation |  |
| LastMod | bis:Element 的最后修改时间。此属性由核心框架维护，应用程序不应直接设置。 | dateTime |  |
| CodeSpec | CodeSpec 属性标识用于生成和验证此 bis:Element 代码值的 bis:CodeSpec。每个 bis:Element 实例的 CodeSpec、CodeScope 和 CodeValue 属性组合必须唯一。 | navigation |  |
| CodeScope | CodeScope 属性标识为代码值提供唯一性范围的 bis:Element。每个 bis:Element 实例的 CodeSpec、CodeScope 和 CodeValue 属性组合必须唯一。 | navigation |  |
| CodeValue | 可空字符串属性，保存 Element 的 Code 的实际文本。每个 bis:Element 实例的 CodeSpec、CodeScope 和 CodeValue 属性组合必须唯一。 | string |  |
| UserLabel | 用户提供的可选友好名称（与存储在 CodeValue 属性中的正式名称相对）。 | string |  |
| Parent | 拥有此 bis:Element 的父 bis:Element。 | navigation |  |
| FederationGuid | 用于跨仓库联合此 bis:Element 的 GUID。 | binary | BeGuid |
| JsonProperties | 用户和/或应用程序可用于持久化临时 JSON 值的字符串属性。 | string | Json |
| Category | 用于对此 bis:GeometricElement2d 实例进行分类的 bis:DrawingCategory。 | navigation |  |
| Origin | 此 bis:Element 的放置原点。 | point2d |  |
| Rotation | 此 bis:Element 的放置旋转角度（以度为单位）。 | double |  |
| BBoxLow | 此 bis:Element 的元素对齐边界框的"低"点。 | point2d |  |
| BBoxHigh | 此 bis:Element 的元素对齐边界框的"高"点。 | point2d |  |
| GeometryStream | 用于持久化此 bis:Element 几何图形的二进制流。 | binary | GeometryStream |
| TypeDefinition | 指向 TypeDefinition 的某个特化实例，该实例保存按类型而非按此 Element 实例变化的属性值。 | navigation |  |
| DrawingModel |  | navigation |  |

### __Graphic3d__ (3D Graphic) _密封_ EntityClass

generic:Graphic3d 类是 bis:GraphicalElement3d 的具体子类，可用于无法进一步分类的通用 3D 图形。应尽可能使用更具体的 bis:GraphicalElement3d 子类。

**基类：** BisCore:GraphicalElement3d

继承属性

| 名称 | 描述 | 类型 | 扩展类型 |
| --- | --- | --- | --- |
| Model | 包含此 bis:Element 的 bis:Model。 | navigation |  |
| LastMod | bis:Element 的最后修改时间。此属性由核心框架维护，应用程序不应直接设置。 | dateTime |  |
| CodeSpec | CodeSpec 属性标识用于生成和验证此 bis:Element 代码值的 bis:CodeSpec。每个 bis:Element 实例的 CodeSpec、CodeScope 和 CodeValue 属性组合必须唯一。 | navigation |  |
| CodeScope | CodeScope 属性标识为代码值提供唯一性范围的 bis:Element。每个 bis:Element 实例的 CodeSpec、CodeScope 和 CodeValue 属性组合必须唯一。 | navigation |  |
| CodeValue | 可空字符串属性，保存 Element 的 Code 的实际文本。每个 bis:Element 实例的 CodeSpec、CodeScope 和 CodeValue 属性组合必须唯一。 | string |  |
| UserLabel | 用户提供的可选友好名称（与存储在 CodeValue 属性中的正式名称相对）。 | string |  |
| Parent | 拥有此 bis:Element 的父 bis:Element。 | navigation |  |
| FederationGuid | 用于跨仓库联合此 bis:Element 的 GUID。 | binary | BeGuid |
| JsonProperties | 用户和/或应用程序可用于持久化临时 JSON 值的字符串属性。 | string | Json |
| Category | 用于对此 bis:GeometricElement3d 进行分类的 bis:SpatialCategory | navigation |  |
| InSpatialIndex | 如果为 true，此元素将在 Spatial Index 中有条目。 | boolean |  |
| Origin | 此 bis:Element 的放置原点。 | point3d |  |
| Yaw | 此 bis:Element 方向的 Yaw 角（以度为单位）。 | double |  |
| Pitch | 此 bis:Element 方向的 Pitch 角（以度为单位）。 | double |  |
| Roll | 此 bis:Element 方向的 Roll 角（以度为单位）。 | double |  |
| BBoxLow | 此 bis:Element 的元素对齐边界框的"低"点。 | point3d |  |
| BBoxHigh | 此 bis:Element 的元素对齐边界框的"高"点。 | point3d |  |
| GeometryStream | 用于持久化此 bis:Element 几何图形的二进制流。 | binary | GeometryStream |
| TypeDefinition | 指向 TypeDefinition 的某个特化实例，该实例保存按类型而非按此 Element 实例变化的属性值。 | navigation |  |

### __GraphicalModel3d__ (3D Graphical Model) _密封_ EntityClass

用于持久化 bis:GraphicalElement3d 实例的容器。

**基类：** BisCore:GraphicalModel3d

继承属性

| 名称 | 描述 | 类型 | 扩展类型 |
| --- | --- | --- | --- |
| ParentModel | 父 bis:Model 包含此 bis:Model 正在建模的 bis:Element。 | navigation |  |
| ModeledElement | 此 bis:Model 正在建模的 bis:Element。此 bis:Model 与被建模的 bis:Element 建模同一实体，但粒度更细。 | navigation |  |
| IsPrivate | 如果 IsPrivate 为 true，则此 bis:Model 不应出现在向用户显示的列表中。 | boolean |  |
| IsTemplate | 如果 IsTemplate 为 true，则此 bis:Model 用作创建新实例的模板。 | boolean |  |
| JsonProperties | 用户和/或应用程序可用于持久化临时 JSON 值的字符串属性。 | string | Json |
| LastMod | 此 Model 中任何元素的最后修改时间。 | dateTime |  |
| GeometryGuid | 每当此 GeometricModel 中的任何元素的几何图形发生更改时都会更改的 GUID。 | binary | BeGuid |
| IsNotSpatiallyLocated | 如果 IsNotSpatiallyLocated 为 true，则此 bis:GeometricModel3d 中的元素不在真实世界坐标中，也不会在空间索引中。 | boolean |  |
| IsPlanProjection | 如果 IsPlanProjection 为 true，则此 bis:GeometricModel3d 中的元素预期在 XY 平面中。 | boolean |  |

### __GraphicalType2d__ (2D Graphical Type) _密封_ EntityClass

generic:GraphicalType2d 类用于无法进一步分类的 bis:GraphicalType2d 元素。应尽可能使用更具体的 bis:GraphicalType2d 子类。

**基类：** BisCore:GraphicalType2d

继承属性

| 名称 | 描述 | 类型 | 扩展类型 |
| --- | --- | --- | --- |
| Model | 包含此 bis:Element 的 bis:Model。 | navigation |  |
| LastMod | bis:Element 的最后修改时间。此属性由核心框架维护，应用程序不应直接设置。 | dateTime |  |
| CodeSpec | CodeSpec 属性标识用于生成和验证此 bis:Element 代码值的 bis:CodeSpec。每个 bis:Element 实例的 CodeSpec、CodeScope 和 CodeValue 属性组合必须唯一。 | navigation |  |
| CodeScope | CodeScope 属性标识为代码值提供唯一性范围的 bis:Element。每个 bis:Element 实例的 CodeSpec、CodeScope 和 CodeValue 属性组合必须唯一。 | navigation |  |
| CodeValue | 可空字符串属性，保存 Element 的 Code 的实际文本。每个 bis:Element 实例的 CodeSpec、CodeScope 和 CodeValue 属性组合必须唯一。 | string |  |
| UserLabel | 用户提供的可选友好名称（与存储在 CodeValue 属性中的正式名称相对）。 | string |  |
| Parent | 拥有此 bis:Element 的父 bis:Element。 | navigation |  |
| FederationGuid | 用于跨仓库联合此 bis:Element 的 GUID。 | binary | BeGuid |
| JsonProperties | 用户和/或应用程序可用于持久化临时 JSON 值的字符串属性。 | string | Json |
| IsPrivate | 如果为 true，此 bis:DefinitionElement 不应在 GUI 中显示。 | boolean |  |
| Recipe |  | navigation |  |

### __Group__ _密封_ EntityClass

**基类：** BisCore:GroupInformationElement

继承属性

| 名称 | 描述 | 类型 | 扩展类型 |
| --- | --- | --- | --- |
| Model | 包含此 bis:Element 的 bis:Model。 | navigation |  |
| LastMod | bis:Element 的最后修改时间。此属性由核心框架维护，应用程序不应直接设置。 | dateTime |  |
| CodeSpec | CodeSpec 属性标识用于生成和验证此 bis:Element 代码值的 bis:CodeSpec。每个 bis:Element 实例的 CodeSpec、CodeScope 和 CodeValue 属性组合必须唯一。 | navigation |  |
| CodeScope | CodeScope 属性标识为代码值提供唯一性范围的 bis:Element。每个 bis:Element 实例的 CodeSpec、CodeScope 和 CodeValue 属性组合必须唯一。 | navigation |  |
| CodeValue | 可空字符串属性，保存 Element 的 Code 的实际文本。每个 bis:Element 实例的 CodeSpec、CodeScope 和 CodeValue 属性组合必须唯一。 | string |  |
| UserLabel | 用户提供的可选友好名称（与存储在 CodeValue 属性中的正式名称相对）。 | string |  |
| Parent | 拥有此 bis:Element 的父 bis:Element。 | navigation |  |
| FederationGuid | 用于跨仓库联合此 bis:Element 的 GUID。 | binary | BeGuid |
| JsonProperties | 用户和/或应用程序可用于持久化临时 JSON 值的字符串属性。 | string | Json |

### __GroupModel__ (Group Model) _密封_ EntityClass

**基类：** BisCore:GroupInformationModel

继承属性

| 名称 | 描述 | 类型 | 扩展类型 |
| --- | --- | --- | --- |
| ParentModel | 父 bis:Model 包含此 bis:Model 正在建模的 bis:Element。 | navigation |  |
| ModeledElement | 此 bis:Model 正在建模的 bis:Element。此 bis:Model 与被建模的 bis:Element 建模同一实体，但粒度更细。 | navigation |  |
| IsPrivate | 如果 IsPrivate 为 true，则此 bis:Model 不应出现在向用户显示的列表中。 | boolean |  |
| IsTemplate | 如果 IsTemplate 为 true，则此 bis:Model 用作创建新实例的模板。 | boolean |  |
| JsonProperties | 用户和/或应用程序可用于持久化临时 JSON 值的字符串属性。 | string | Json |
| LastMod | 此 Model 中任何元素的最后修改时间。 | dateTime |  |

### __PhysicalMaterial__ (Physical Material) _密封_ EntityClass

generic:PhysicalMaterial 类用于无法进一步分类的 bis:PhysicalMaterial 元素。应尽可能使用更具体的 bis:PhysicalMaterial 子类。

**基类：** BisCore:PhysicalMaterial

继承属性

| 名称 | 描述 | 类型 | 扩展类型 |
| --- | --- | --- | --- |
| Model | 包含此 bis:Element 的 bis:Model。 | navigation |  |
| LastMod | bis:Element 的最后修改时间。此属性由核心框架维护，应用程序不应直接设置。 | dateTime |  |
| CodeSpec | CodeSpec 属性标识用于生成和验证此 bis:Element 代码值的 bis:CodeSpec。每个 bis:Element 实例的 CodeSpec、CodeScope 和 CodeValue 属性组合必须唯一。 | navigation |  |
| CodeScope | CodeScope 属性标识为代码值提供唯一性范围的 bis:Element。每个 bis:Element 实例的 CodeSpec、CodeScope 和 CodeValue 属性组合必须唯一。 | navigation |  |
| CodeValue | 可空字符串属性，保存 Element 的 Code 的实际文本。每个 bis:Element 实例的 CodeSpec、CodeScope 和 CodeValue 属性组合必须唯一。 | string |  |
| UserLabel | 用户提供的可选友好名称（与存储在 CodeValue 属性中的正式名称相对）。 | string |  |
| Parent | 拥有此 bis:Element 的父 bis:Element。 | navigation |  |
| FederationGuid | 用于跨仓库联合此 bis:Element 的 GUID。 | binary | BeGuid |
| JsonProperties | 用户和/或应用程序可用于持久化临时 JSON 值的字符串属性。 | string | Json |
| IsPrivate | 如果为 true，此 bis:DefinitionElement 不应在 GUI 中显示。 | boolean |  |
| Density |  | double |  |
| RenderMaterial | 可选地引用用于显示 bis:PhysicalMaterial 的 bis:RenderMaterial。 | navigation |  |

### __PhysicalObject__ (Physical Object) _密封_ EntityClass

generic:PhysicalObject 类用于无法进一步分类的 bis:PhysicalElements。应尽可能使用更具体的 bis:PhysicalElement 子类。

**基类：** BisCore:PhysicalElement

继承属性

| 名称 | 描述 | 类型 | 扩展类型 |
| --- | --- | --- | --- |
| Model | 包含此 bis:Element 的 bis:Model。 | navigation |  |
| LastMod | bis:Element 的最后修改时间。此属性由核心框架维护，应用程序不应直接设置。 | dateTime |  |
| CodeSpec | CodeSpec 属性标识用于生成和验证此 bis:Element 代码值的 bis:CodeSpec。每个 bis:Element 实例的 CodeSpec、CodeScope 和 CodeValue 属性组合必须唯一。 | navigation |  |
| CodeScope | CodeScope 属性标识为代码值提供唯一性范围的 bis:Element。每个 bis:Element 实例的 CodeSpec、CodeScope 和 CodeValue 属性组合必须唯一。 | navigation |  |
| CodeValue | 可空字符串属性，保存 Element 的 Code 的实际文本。每个 bis:Element 实例的 CodeSpec、CodeScope 和 CodeValue 属性组合必须唯一。 | string |  |
| UserLabel | 用户提供的可选友好名称（与存储在 CodeValue 属性中的正式名称相对）。 | string |  |
| Parent | 拥有此 bis:Element 的父 bis:Element。 | navigation |  |
| FederationGuid | 用于跨仓库联合此 bis:Element 的 GUID。 | binary | BeGuid |
| JsonProperties | 用户和/或应用程序可用于持久化临时 JSON 值的字符串属性。 | string | Json |
| Category | 用于对此 bis:GeometricElement3d 进行分类的 bis:SpatialCategory | navigation |  |
| InSpatialIndex | 如果为 true，此元素将在 Spatial Index 中有条目。 | boolean |  |
| Origin | 此 bis:Element 的放置原点。 | point3d |  |
| Yaw | 此 bis:Element 方向的 Yaw 角（以度为单位）。 | double |  |
| Pitch | 此 bis:Element 方向的 Pitch 角（以度为单位）。 | double |  |
| Roll | 此 bis:Element 方向的 Roll 角（以度为单位）。 | double |  |
| BBoxLow | 此 bis:Element 的元素对齐边界框的"低"点。 | point3d |  |
| BBoxHigh | 此 bis:Element 的元素对齐边界框的"高"点。 | point3d |  |
| GeometryStream | 用于持久化此 bis:Element 几何图形的二进制流。 | binary | GeometryStream |
| TypeDefinition | 指向 TypeDefinition 的某个特化实例，该实例保存按类型而非按此 Element 实例变化的属性值。 | navigation |  |
| PhysicalMaterial | 指示构成 bis:PhysicalElement 的 bis:PhysicalMaterial。 | navigation |  |

### __PhysicalType__ (Physical Type) _密封_ EntityClass

generic:PhysicalType 类用于无法进一步分类的 bis:PhysicalType 元素。应尽可能使用更具体的 bis:PhysicalType 子类。

**基类：** BisCore:PhysicalType

继承属性

| 名称 | 描述 | 类型 | 扩展类型 |
| --- | --- | --- | --- |
| Model | 包含此 bis:Element 的 bis:Model。 | navigation |  |
| LastMod | bis:Element 的最后修改时间。此属性由核心框架维护，应用程序不应直接设置。 | dateTime |  |
| CodeSpec | CodeSpec 属性标识用于生成和验证此 bis:Element 代码值的 bis:CodeSpec。每个 bis:Element 实例的 CodeSpec、CodeScope 和 CodeValue 属性组合必须唯一。 | navigation |  |
| CodeScope | CodeScope 属性标识为代码值提供唯一性范围的 bis:Element。每个 bis:Element 实例的 CodeSpec、CodeScope 和 CodeValue 属性组合必须唯一。 | navigation |  |
| CodeValue | 可空字符串属性，保存 Element 的 Code 的实际文本。每个 bis:Element 实例的 CodeSpec、CodeScope 和 CodeValue 属性组合必须唯一。 | string |  |
| UserLabel | 用户提供的可选友好名称（与存储在 CodeValue 属性中的正式名称相对）。 | string |  |
| Parent | 拥有此 bis:Element 的父 bis:Element。 | navigation |  |
| FederationGuid | 用于跨仓库联合此 bis:Element 的 GUID。 | binary | BeGuid |
| JsonProperties | 用户和/或应用程序可用于持久化临时 JSON 值的字符串属性。 | string | Json |
| IsPrivate | 如果为 true，此 bis:DefinitionElement 不应在 GUI 中显示。 | boolean |  |
| Recipe |  | navigation |  |
| PhysicalMaterial | 指示给定 bis:PhysicalType 的 bis:PhysicalElements 所构成的 bis:PhysicalMaterial。 | navigation |  |

### __PlanCallout__ (Plan Callout) _密封_ EntityClass

一个 generic:Callout，用于标注对平面图纸的引用。

**基类：** Generic:Callout

继承属性

| 名称 | 描述 | 类型 | 扩展类型 |
| --- | --- | --- | --- |
| Model | 包含此 bis:Element 的 bis:Model。 | navigation |  |
| LastMod | bis:Element 的最后修改时间。此属性由核心框架维护，应用程序不应直接设置。 | dateTime |  |
| CodeSpec | CodeSpec 属性标识用于生成和验证此 bis:Element 代码值的 bis:CodeSpec。每个 bis:Element 实例的 CodeSpec、CodeScope 和 CodeValue 属性组合必须唯一。 | navigation |  |
| CodeScope | CodeScope 属性标识为代码值提供唯一性范围的 bis:Element。每个 bis:Element 实例的 CodeSpec、CodeScope 和 CodeValue 属性组合必须唯一。 | navigation |  |
| CodeValue | 可空字符串属性，保存 Element 的 Code 的实际文本。每个 bis:Element 实例的 CodeSpec、CodeScope 和 CodeValue 属性组合必须唯一。 | string |  |
| UserLabel | 用户提供的可选友好名称（与存储在 CodeValue 属性中的正式名称相对）。 | string |  |
| Parent | 拥有此 bis:Element 的父 bis:Element。 | navigation |  |
| FederationGuid | 用于跨仓库联合此 bis:Element 的 GUID。 | binary | BeGuid |
| JsonProperties | 用户和/或应用程序可用于持久化临时 JSON 值的字符串属性。 | string | Json |
| Category | 用于对此 bis:GeometricElement2d 实例进行分类的 bis:DrawingCategory。 | navigation |  |
| Origin | 此 bis:Element 的放置原点。 | point2d |  |
| Rotation | 此 bis:Element 的放置旋转角度（以度为单位）。 | double |  |
| BBoxLow | 此 bis:Element 的元素对齐边界框的"低"点。 | point2d |  |
| BBoxHigh | 此 bis:Element 的元素对齐边界框的"高"点。 | point2d |  |
| GeometryStream | 用于持久化此 bis:Element 几何图形的二进制流。 | binary | GeometryStream |
| TypeDefinition | 指向 TypeDefinition 的某个特化实例，该实例保存按类型而非按此 Element 实例变化的属性值。 | navigation |  |
| DrawingModel |  | navigation |  |

### __SectionCallout__ (Section Callout) _密封_ EntityClass

一个 generic:Callout，用于标注对剖面图纸的引用。

**基类：** Generic:Callout

继承属性

| 名称 | 描述 | 类型 | 扩展类型 |
| --- | --- | --- | --- |
| Model | 包含此 bis:Element 的 bis:Model。 | navigation |  |
| LastMod | bis:Element 的最后修改时间。此属性由核心框架维护，应用程序不应直接设置。 | dateTime |  |
| CodeSpec | CodeSpec 属性标识用于生成和验证此 bis:Element 代码值的 bis:CodeSpec。每个 bis:Element 实例的 CodeSpec、CodeScope 和 CodeValue 属性组合必须唯一。 | navigation |  |
| CodeScope | CodeScope 属性标识为代码值提供唯一性范围的 bis:Element。每个 bis:Element 实例的 CodeSpec、CodeScope 和 CodeValue 属性组合必须唯一。 | navigation |  |
| CodeValue | 可空字符串属性，保存 Element 的 Code 的实际文本。每个 bis:Element 实例的 CodeSpec、CodeScope 和 CodeValue 属性组合必须唯一。 | string |  |
| UserLabel | 用户提供的可选友好名称（与存储在 CodeValue 属性中的正式名称相对）。 | string |  |
| Parent | 拥有此 bis:Element 的父 bis:Element。 | navigation |  |
| FederationGuid | 用于跨仓库联合此 bis:Element 的 GUID。 | binary | BeGuid |
| JsonProperties | 用户和/或应用程序可用于持久化临时 JSON 值的字符串属性。 | string | Json |
| Category | 用于对此 bis:GeometricElement2d 实例进行分类的 bis:DrawingCategory。 | navigation |  |
| Origin | 此 bis:Element 的放置原点。 | point2d |  |
| Rotation | 此 bis:Element 的放置旋转角度（以度为单位）。 | double |  |
| BBoxLow | 此 bis:Element 的元素对齐边界框的"低"点。 | point2d |  |
| BBoxHigh | 此 bis:Element 的元素对齐边界框的"高"点。 | point2d |  |
| GeometryStream | 用于持久化此 bis:Element 几何图形的二进制流。 | binary | GeometryStream |
| TypeDefinition | 指向 TypeDefinition 的某个特化实例，该实例保存按类型而非按此 Element 实例变化的属性值。 | navigation |  |
| DrawingModel |  | navigation |  |

### __SpatialLocation__ (Spatial Location) _密封_ EntityClass

generic:SpatialLocation 类用于无法进一步分类的 bis:SpatialLocationElements。应尽可能使用更具体的 bis:SpatialLocationElement 子类。

**基类：** BisCore:SpatialLocationElement

继承属性

| 名称 | 描述 | 类型 | 扩展类型 |
| --- | --- | --- | --- |
| Model | 包含此 bis:Element 的 bis:Model。 | navigation |  |
| LastMod | bis:Element 的最后修改时间。此属性由核心框架维护，应用程序不应直接设置。 | dateTime |  |
| CodeSpec | CodeSpec 属性标识用于生成和验证此 bis:Element 代码值的 bis:CodeSpec。每个 bis:Element 实例的 CodeSpec、CodeScope 和 CodeValue 属性组合必须唯一。 | navigation |  |
| CodeScope | CodeScope 属性标识为代码值提供唯一性范围的 bis:Element。每个 bis:Element 实例的 CodeSpec、CodeScope 和 CodeValue 属性组合必须唯一。 | navigation |  |
| CodeValue | 可空字符串属性，保存 Element 的 Code 的实际文本。每个 bis:Element 实例的 CodeSpec、CodeScope 和 CodeValue 属性组合必须唯一。 | string |  |
| UserLabel | 用户提供的可选友好名称（与存储在 CodeValue 属性中的正式名称相对）。 | string |  |
| Parent | 拥有此 bis:Element 的父 bis:Element。 | navigation |  |
| FederationGuid | 用于跨仓库联合此 bis:Element 的 GUID。 | binary | BeGuid |
| JsonProperties | 用户和/或应用程序可用于持久化临时 JSON 值的字符串属性。 | string | Json |
| Category | 用于对此 bis:GeometricElement3d 进行分类的 bis:SpatialCategory | navigation |  |
| InSpatialIndex | 如果为 true，此元素将在 Spatial Index 中有条目。 | boolean |  |
| Origin | 此 bis:Element 的放置原点。 | point3d |  |
| Yaw | 此 bis:Element 方向的 Yaw 角（以度为单位）。 | double |  |
| Pitch | 此 bis:Element 方向的 Pitch 角（以度为单位）。 | double |  |
| Roll | 此 bis:Element 方向的 Roll 角（以度为单位）。 | double |  |
| BBoxLow | 此 bis:Element 的元素对齐边界框的"低"点。 | point3d |  |
| BBoxHigh | 此 bis:Element 的元素对齐边界框的"高"点。 | point3d |  |
| GeometryStream | 用于持久化此 bis:Element 几何图形的二进制流。 | binary | GeometryStream |
| TypeDefinition | 指向 TypeDefinition 的某个特化实例，该实例保存按类型而非按此 Element 实例变化的属性值。 | navigation |  |

### __SpatialLocationType__ (Spatial Location Type) _密封_ EntityClass

generic:SpatialLocationType 类用于无法进一步分类的 bis:SpatialLocationType 元素。应尽可能使用更具体的 bis:SpatialLocationType 子类。

**基类：** BisCore:SpatialLocationType

继承属性

| 名称 | 描述 | 类型 | 扩展类型 |
| --- | --- | --- | --- |
| Model | 包含此 bis:Element 的 bis:Model。 | navigation |  |
| LastMod | bis:Element 的最后修改时间。此属性由核心框架维护，应用程序不应直接设置。 | dateTime |  |
| CodeSpec | CodeSpec 属性标识用于生成和验证此 bis:Element 代码值的 bis:CodeSpec。每个 bis:Element 实例的 CodeSpec、CodeScope 和 CodeValue 属性组合必须唯一。 | navigation |  |
| CodeScope | CodeScope 属性标识为代码值提供唯一性范围的 bis:Element。每个 bis:Element 实例的 CodeSpec、CodeScope 和 CodeValue 属性组合必须唯一。 | navigation |  |
| CodeValue | 可空字符串属性，保存 Element 的 Code 的实际文本。每个 bis:Element 实例的 CodeSpec、CodeScope 和 CodeValue 属性组合必须唯一。 | string |  |
| UserLabel | 用户提供的可选友好名称（与存储在 CodeValue 属性中的正式名称相对）。 | string |  |
| Parent | 拥有此 bis:Element 的父 bis:Element。 | navigation |  |
| FederationGuid | 用于跨仓库联合此 bis:Element 的 GUID。 | binary | BeGuid |
| JsonProperties | 用户和/或应用程序可用于持久化临时 JSON 值的字符串属性。 | string | Json |
| IsPrivate | 如果为 true，此 bis:DefinitionElement 不应在 GUI 中显示。 | boolean |  |
| Recipe |  | navigation |  |

### __TitleText__ (Title Text) _密封_ EntityClass

包含标题文本的 generic:DetailingSymbol。

**基类：** Generic:DetailingSymbol

继承属性

| 名称 | 描述 | 类型 | 扩展类型 |
| --- | --- | --- | --- |
| Model | 包含此 bis:Element 的 bis:Model。 | navigation |  |
| LastMod | bis:Element 的最后修改时间。此属性由核心框架维护，应用程序不应直接设置。 | dateTime |  |
| CodeSpec | CodeSpec 属性标识用于生成和验证此 bis:Element 代码值的 bis:CodeSpec。每个 bis:Element 实例的 CodeSpec、CodeScope 和 CodeValue 属性组合必须唯一。 | navigation |  |
| CodeScope | CodeScope 属性标识为代码值提供唯一性范围的 bis:Element。每个 bis:Element 实例的 CodeSpec、CodeScope 和 CodeValue 属性组合必须唯一。 | navigation |  |
| CodeValue | 可空字符串属性，保存 Element 的 Code 的实际文本。每个 bis:Element 实例的 CodeSpec、CodeScope 和 CodeValue 属性组合必须唯一。 | string |  |
| UserLabel | 用户提供的可选友好名称（与存储在 CodeValue 属性中的正式名称相对）。 | string |  |
| Parent | 拥有此 bis:Element 的父 bis:Element。 | navigation |  |
| FederationGuid | 用于跨仓库联合此 bis:Element 的 GUID。 | binary | BeGuid |
| JsonProperties | 用户和/或应用程序可用于持久化临时 JSON 值的字符串属性。 | string | Json |
| Category | 用于对此 bis:GeometricElement2d 实例进行分类的 bis:DrawingCategory。 | navigation |  |
| Origin | 此 bis:Element 的放置原点。 | point2d |  |
| Rotation | 此 bis:Element 的放置旋转角度（以度为单位）。 | double |  |
| BBoxLow | 此 bis:Element 的元素对齐边界框的"低"点。 | point2d |  |
| BBoxHigh | 此 bis:Element 的元素对齐边界框的"高"点。 | point2d |  |
| GeometryStream | 用于持久化此 bis:Element 几何图形的二进制流。 | binary | GeometryStream |
| TypeDefinition | 指向 TypeDefinition 的某个特化实例，该实例保存按类型而非按此 Element 实例变化的属性值。 | navigation |  |

### __ViewAttachmentLabel__ (View Attachment Label) _密封_ EntityClass

包含视图附件标签的 generic:DetailingSymbol。

**基类：** Generic:DetailingSymbol

#### 属性

| 名称 | 描述 | 类型 | 扩展类型 |
| --- | --- | --- | --- |
| ViewAttachment |  | navigation |  |
| ClipGeometry | 定义图纸上包含与 View Attachment 相关的注释的区域。 | string | Json |

继承属性

| 名称 | 描述 | 类型 | 扩展类型 |
| --- | --- | --- | --- |
| Model | 包含此 bis:Element 的 bis:Model。 | navigation |  |
| LastMod | bis:Element 的最后修改时间。此属性由核心框架维护，应用程序不应直接设置。 | dateTime |  |
| CodeSpec | CodeSpec 属性标识用于生成和验证此 bis:Element 代码值的 bis:CodeSpec。每个 bis:Element 实例的 CodeSpec、CodeScope 和 CodeValue 属性组合必须唯一。 | navigation |  |
| CodeScope | CodeScope 属性标识为代码值提供唯一性范围的 bis:Element。每个 bis:Element 实例的 CodeSpec、CodeScope 和 CodeValue 属性组合必须唯一。 | navigation |  |
| CodeValue | 可空字符串属性，保存 Element 的 Code 的实际文本。每个 bis:Element 实例的 CodeSpec、CodeScope 和 CodeValue 属性组合必须唯一。 | string |  |
| UserLabel | 用户提供的可选友好名称（与存储在 CodeValue 属性中的正式名称相对）。 | string |  |
| Parent | 拥有此 bis:Element 的父 bis:Element。 | navigation |  |
| FederationGuid | 用于跨仓库联合此 bis:Element 的 GUID。 | binary | BeGuid |
| JsonProperties | 用户和/或应用程序可用于持久化临时 JSON 值的字符串属性。 | string | Json |
| Category | 用于对此 bis:GeometricElement2d 实例进行分类的 bis:DrawingCategory。 | navigation |  |
| Origin | 此 bis:Element 的放置原点。 | point2d |  |
| Rotation | 此 bis:Element 的放置旋转角度（以度为单位）。 | double |  |
| BBoxLow | 此 bis:Element 的元素对齐边界框的"低"点。 | point2d |  |
| BBoxHigh | 此 bis:Element 的元素对齐边界框的"高"点。 | point2d |  |
| GeometryStream | 用于持久化此 bis:Element 几何图形的二进制流。 | binary | GeometryStream |
| TypeDefinition | 指向 TypeDefinition 的某个特化实例，该实例保存按类型而非按此 Element 实例变化的属性值。 | navigation |  |

## 关系类 (Relationship Classes)

### __CalloutRefersToDrawingModel__ _密封_ RelationshipClass

**强度：** Referencing

**强度方向：** Backward

#### 源 (Source)

**是否多态：** true

**角色标签：** refers to

**多重性：** (0..*)

#### 约束类 (Constraint Classes)：

- Callout

#### 目标 (Target)

**是否多态：** true

**角色标签：** is referenced by

**多重性：** (0..1)

#### 约束类 (Constraint Classes)：

- DrawingModel

### __ViewAttachmentLabelAnnotatesViewAttachment__ _密封_ RelationshipClass

**强度：** Referencing

**强度方向：** Backward

#### 源 (Source)

**是否多态：** true

**角色标签：** annotates

**多重性：** (0..1)

#### 约束类 (Constraint Classes)：

- ViewAttachmentLabel

#### 目标 (Target)

**是否多态：** true

**角色标签：** is annotated by

**多重性：** (0..1)

#### 约束类 (Constraint Classes)：

- ViewAttachment
