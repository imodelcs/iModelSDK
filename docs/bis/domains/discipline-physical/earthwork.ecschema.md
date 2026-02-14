# Earthwork Schema

**Alias:** ew

**Version:** 1.0.0

Earthwork 领域的基础 schema。

包含 BIS 中建模土方工程活动的类。Earthwork（土方工程）涉及挖掘或建造路堤、移动和/或处理大量土壤或未成形岩石的工作。其目的是重新配置场地的地形以达到设计标高。

![Earthwork 类图](https://www.itwinjs.org/media/earthwork-classes.png)

## 目录

- Entity Classes（实体类）
  - Cut
  - CutType
  - Fill
  - FillType
  - SurfaceGrade
  - SurfaceGradeType
- Relationship Classes（关系类）
  - CutIsOfType
  - FillIsOfType
  - SurfaceGradeIsOfType

## Entity Classes（实体类）

### Cut（开挖）

一个 `bis:PhysicalElement`，用于建模通过挖掘或其他方式从现有地形或道路结构中移除的材料体积。

**Base Class:** BisCore:PhysicalElement

继承属性

| 名称 | 描述 | 类型 | 扩展类型 |
| --- | --- | --- | --- |
| Model | 包含此 `bis:Element` 的 `bis:Model`。 | navigation |  |
| LastMod | `bis:Element` 的最后修改时间。此属性由核心框架维护，应用程序不应直接设置。 | dateTime |  |
| CodeSpec | CodeSpec 属性标识用于生成和验证此 `bis:Element` 代码值的 `bis:CodeSpec`。CodeSpec、CodeScope 和 CodeValue 属性的组合对每个 `bis:Element` 实例必须是唯一的。 | navigation |  |
| CodeScope | CodeScope 属性标识为代码值提供唯一性范围的 `bis:Element`。CodeSpec、CodeScope 和 CodeValue 属性的组合对每个 `bis:Element` 实例必须是唯一的。 | navigation |  |
| CodeValue | 可空字符串属性，保存 Element 的 Code 的实际文本。CodeSpec、CodeScope 和 CodeValue 属性的组合对每个 `bis:Element` 实例必须是唯一的。 | string |  |
| UserLabel | 用户给出的可选友好名称（与存储在 CodeValue 属性中的正式名称相对）。 | string |  |
| Parent | 拥有此 `bis:Element` 的父 `bis:Element`。 | navigation |  |
| FederationGuid | 用于跨存储库联合此 `bis:Element` 的 GUID。 | binary | BeGuid |
| JsonProperties | 用户和/或应用程序可用于持久化临时 JSON 值的字符串属性。 | string | Json |
| Category | 用于对此 `bis:GeometricElement3d` 进行分类的 `bis:SpatialCategory` | navigation |  |
| InSpatialIndex | 如果为 true，此元素将在空间索引中有一个条目。 | boolean |  |
| Origin | 此 `bis:Element` 的放置原点。 | point3d |  |
| Yaw | 此 `bis:Element` 方向的 Yaw 角度（以度为单位）。 | double |  |
| Pitch | 此 `bis:Element` 方向的 Pitch 角度（以度为单位）。 | double |  |
| Roll | 此 `bis:Element` 方向的 Roll 角度（以度为单位）。 | double |  |
| BBoxLow | 此 `bis:Element` 的元素对齐边界框的"低"点。 | point3d |  |
| BBoxHigh | 此 `bis:Element` 的元素对齐边界框的"高"点。 | point3d |  |
| GeometryStream | 用于持久化此 `bis:Element` 几何图形的二进制流。 | binary | GeometryStream |
| TypeDefinition | 指向 TypeDefinition 的某个专门化的实例，该实例保存按类型而非按此 Element 实例变化的属性值。 | navigation |  |
| PhysicalMaterial | 指示 `bis:PhysicalElement` 由哪种 `bis:PhysicalMaterial` 制成。 | navigation |  |

由 `Cut` 建模的开挖材料，以后可以用作填方或作为废料丢弃。然而，Earthwork schema 并不旨在对此类过程进行建模。`Cut` 实例可以通过其 `PhysicalMaterial` 属性覆盖其对应 `CutType` 指定的要移除的 *Physical Material*。

`Cut` 应将其 *Volume*（体积）作为 *Polyface* 存储在其 `GeometryStream` 中。

`Cut` 必须包含在 `PhysicalModel` 中。默认情况下，`Cut` 实例应使用 Domain 级别的 `ew:Volume` 类别。

等效于 IfcEarthworksCut，主要区别是 IFC 的等效项不对开挖的材料进行建模，只对现有地形修改后产生的空隙进行建模。

### CutType（开挖类型）

定义可与 `ew:Cut` 实例关联的一组共享属性和分类（即"类型"）。

**Base Class:** BisCore:PhysicalType

继承属性

| 名称 | 描述 | 类型 | 扩展类型 |
| --- | --- | --- | --- |
| Model | 包含此 `bis:Element` 的 `bis:Model`。 | navigation |  |
| LastMod | `bis:Element` 的最后修改时间。此属性由核心框架维护，应用程序不应直接设置。 | dateTime |  |
| CodeSpec | CodeSpec 属性标识用于生成和验证此 `bis:Element` 代码值的 `bis:CodeSpec`。CodeSpec、CodeScope 和 CodeValue 属性的组合对每个 `bis:Element` 实例必须是唯一的。 | navigation |  |
| CodeScope | CodeScope 属性标识为代码值提供唯一性范围的 `bis:Element`。CodeSpec、CodeScope 和 CodeValue 属性的组合对每个 `bis:Element` 实例必须是唯一的。 | navigation |  |
| CodeValue | 可空字符串属性，保存 Element 的 Code 的实际文本。CodeSpec、CodeScope 和 CodeValue 属性的组合对每个 `bis:Element` 实例必须是唯一的。 | string |  |
| UserLabel | 用户给出的可选友好名称（与存储在 CodeValue 属性中的正式名称相对）。 | string |  |
| Parent | 拥有此 `bis:Element` 的父 `bis:Element`。 | navigation |  |
| FederationGuid | 用于跨存储库联合此 `bis:Element` 的 GUID。 | binary | BeGuid |
| JsonProperties | 用户和/或应用程序可用于持久化临时 JSON 值的字符串属性。 | string | Json |
| IsPrivate | 如果为 true，此 `bis:DefinitionElement` 不应在 GUI 中显示。 | boolean |  |
| Recipe |  | navigation |  |
| PhysicalMaterial | 指示给定 `bis:PhysicalType` 的 `bis:PhysicalElements` 由哪种 `bis:PhysicalMaterial` 制成。 | navigation |  |

`CutType` 的实例提供了可应用于 `Cut` 的额外分类。示例包括 Excavation（挖掘）、Trench（沟槽）或 Dredging（疏浚）。`CutType` 的实例可以选择通过其 `PhysicalMaterial` 属性指定要移除的单一 *Physical Material*。

等效于 IfcEarthworksCutTypeEnum。

### Fill（填方）

一个通过土方工程活动创建的 `bis:PhysicalElement`，用于建造路基或一般性地提高地面标高。

**Base Class:** BisCore:PhysicalElement

继承属性

| 名称 | 描述 | 类型 | 扩展类型 |
| --- | --- | --- | --- |
| Model | 包含此 `bis:Element` 的 `bis:Model`。 | navigation |  |
| LastMod | `bis:Element` 的最后修改时间。此属性由核心框架维护，应用程序不应直接设置。 | dateTime |  |
| CodeSpec | CodeSpec 属性标识用于生成和验证此 `bis:Element` 代码值的 `bis:CodeSpec`。CodeSpec、CodeScope 和 CodeValue 属性的组合对每个 `bis:Element` 实例必须是唯一的。 | navigation |  |
| CodeScope | CodeScope 属性标识为代码值提供唯一性范围的 `bis:Element`。CodeSpec、CodeScope 和 CodeValue 属性的组合对每个 `bis:Element` 实例必须是唯一的。 | navigation |  |
| CodeValue | 可空字符串属性，保存 Element 的 Code 的实际文本。CodeSpec、CodeScope 和 CodeValue 属性的组合对每个 `bis:Element` 实例必须是唯一的。 | string |  |
| UserLabel | 用户给出的可选友好名称（与存储在 CodeValue 属性中的正式名称相对）。 | string |  |
| Parent | 拥有此 `bis:Element` 的父 `bis:Element`。 | navigation |  |
| FederationGuid | 用于跨存储库联合此 `bis:Element` 的 GUID。 | binary | BeGuid |
| JsonProperties | 用户和/或应用程序可用于持久化临时 JSON 值的字符串属性。 | string | Json |
| Category | 用于对此 `bis:GeometricElement3d` 进行分类的 `bis:SpatialCategory` | navigation |  |
| InSpatialIndex | 如果为 true，此元素将在空间索引中有一个条目。 | boolean |  |
| Origin | 此 `bis:Element` 的放置原点。 | point3d |  |
| Yaw | 此 `bis:Element` 方向的 Yaw 角度（以度为单位）。 | double |  |
| Pitch | 此 `bis:Element` 方向的 Pitch 角度（以度为单位）。 | double |  |
| Roll | 此 `bis:Element` 方向的 Roll 角度（以度为单位）。 | double |  |
| BBoxLow | 此 `bis:Element` 的元素对齐边界框的"低"点。 | point3d |  |
| BBoxHigh | 此 `bis:Element` 的元素对齐边界框的"高"点。 | point3d |  |
| GeometryStream | 用于持久化此 `bis:Element` 几何图形的二进制流。 | binary | GeometryStream |
| TypeDefinition | 指向 TypeDefinition 的某个专门化的实例，该实例保存按类型而非按此 Element 实例变化的属性值。 | navigation |  |
| PhysicalMaterial | 指示 `bis:PhysicalElement` 由哪种 `bis:PhysicalMaterial` 制成。 | navigation |  |

`Fill` 的示例包括路基或其上方结构的一部分（如路面或道砟中的"软"层）。通常通过铺设和压实沙子和砾石等建筑材料形成。

`Fill` 应将其 *Volume*（体积）作为 *Polyface* 存储在其 `GeometryStream` 中。可以通过 `FillType` 的实例对 `Fill` 实例进行进一步分类。`Fill` 实例可以通过其 `PhysicalMaterial` 属性覆盖其对应 `FillType` 指定的 *Physical Material*。

`Fill` 必须包含在 `PhysicalModel` 中。默认情况下，`Fill` 实例应使用 Domain 级别的 `ew:Volume` 类别。

等效于 IfcEarthworksFill。

### FillType（填方类型）

定义可与 `ew:Fill` 实例关联的一组共享属性和分类（即"类型"）。

**Base Class:** BisCore:PhysicalType

继承属性

| 名称 | 描述 | 类型 | 扩展类型 |
| --- | --- | --- | --- |
| Model | 包含此 `bis:Element` 的 `bis:Model`。 | navigation |  |
| LastMod | `bis:Element` 的最后修改时间。此属性由核心框架维护，应用程序不应直接设置。 | dateTime |  |
| CodeSpec | CodeSpec 属性标识用于生成和验证此 `bis:Element` 代码值的 `bis:CodeSpec`。CodeSpec、CodeScope 和 CodeValue 属性的组合对每个 `bis:Element` 实例必须是唯一的。 | navigation |  |
| CodeScope | CodeScope 属性标识为代码值提供唯一性范围的 `bis:Element`。CodeSpec、CodeScope 和 CodeValue 属性的组合对每个 `bis:Element` 实例必须是唯一的。 | navigation |  |
| CodeValue | 可空字符串属性，保存 Element 的 Code 的实际文本。CodeSpec、CodeScope 和 CodeValue 属性的组合对每个 `bis:Element` 实例必须是唯一的。 | string |  |
| UserLabel | 用户给出的可选友好名称（与存储在 CodeValue 属性中的正式名称相对）。 | string |  |
| Parent | 拥有此 `bis:Element` 的父 `bis:Element`。 | navigation |  |
| FederationGuid | 用于跨存储库联合此 `bis:Element` 的 GUID。 | binary | BeGuid |
| JsonProperties | 用户和/或应用程序可用于持久化临时 JSON 值的字符串属性。 | string | Json |
| IsPrivate | 如果为 true，此 `bis:DefinitionElement` 不应在 GUI 中显示。 | boolean |  |
| Recipe |  | navigation |  |
| PhysicalMaterial | 指示给定 `bis:PhysicalType` 的 `bis:PhysicalElements` 由哪种 `bis:PhysicalMaterial` 制成。 | navigation |  |

`FillType` 的实例提供了可应用于 `Fill` 的额外分类。示例包括 Embankment（路堤）、Slope Fill（斜坡填方）或 Back Fill（回填）。`FillType` 的实例可以选择通过其 `PhysicalMaterial` 属性指定单一的 *Physical Material*。

等效于 IfcEarthworksFillTypeEnum。

### SurfaceGrade（表面坡度）

一个 `bis:PhysicalElement`，用于捕获通常在引入对现有地形的修改后的地面设计坡度。

**Base Class:** BisCore:PhysicalElement

继承属性

| 名称 | 描述 | 类型 | 扩展类型 |
| --- | --- | --- | --- |
| Model | 包含此 `bis:Element` 的 `bis:Model`。 | navigation |  |
| LastMod | `bis:Element` 的最后修改时间。此属性由核心框架维护，应用程序不应直接设置。 | dateTime |  |
| CodeSpec | CodeSpec 属性标识用于生成和验证此 `bis:Element` 代码值的 `bis:CodeSpec`。CodeSpec、CodeScope 和 CodeValue 属性的组合对每个 `bis:Element` 实例必须是唯一的。 | navigation |  |
| CodeScope | CodeScope 属性标识为代码值提供唯一性范围的 `bis:Element`。CodeSpec、CodeScope 和 CodeValue 属性的组合对每个 `bis:Element` 实例必须是唯一的。 | navigation |  |
| CodeValue | 可空字符串属性，保存 Element 的 Code 的实际文本。CodeSpec、CodeScope 和 CodeValue 属性的组合对每个 `bis:Element` 实例必须是唯一的。 | string |  |
| UserLabel | 用户给出的可选友好名称（与存储在 CodeValue 属性中的正式名称相对）。 | string |  |
| Parent | 拥有此 `bis:Element` 的父 `bis:Element`。 | navigation |  |
| FederationGuid | 用于跨存储库联合此 `bis:Element` 的 GUID。 | binary | BeGuid |
| JsonProperties | 用户和/或应用程序可用于持久化临时 JSON 值的字符串属性。 | string | Json |
| Category | 用于对此 `bis:GeometricElement3d` 进行分类的 `bis:SpatialCategory` | navigation |  |
| InSpatialIndex | 如果为 true，此元素将在空间索引中有一个条目。 | boolean |  |
| Origin | 此 `bis:Element` 的放置原点。 | point3d |  |
| Yaw | 此 `bis:Element` 方向的 Yaw 角度（以度为单位）。 | double |  |
| Pitch | 此 `bis:Element` 方向的 Pitch 角度（以度为单位）。 | double |  |
| Roll | 此 `bis:Element` 方向的 Roll 角度（以度为单位）。 | double |  |
| BBoxLow | 此 `bis:Element` 的元素对齐边界框的"低"点。 | point3d |  |
| BBoxHigh | 此 `bis:Element` 的元素对齐边界框的"高"点。 | point3d |  |
| GeometryStream | 用于持久化此 `bis:Element` 几何图形的二进制流。 | binary | GeometryStream |
| TypeDefinition | 指向 TypeDefinition 的某个专门化的实例，该实例保存按类型而非按此 Element 实例变化的属性值。 | navigation |  |
| PhysicalMaterial | 指示 `bis:PhysicalElement` 由哪种 `bis:PhysicalMaterial` 制成。 | navigation |  |

`SurfaceGrade` 应将其 *Surface*（表面）作为 *Polyface* 存储在其 `GeometryStream` 中。`SurfaceGrade` 实例可以通过其 `PhysicalMaterial` 属性覆盖其对应 `SurfaceGradeType` 指定的 *Physical Material*。

`SurfaceGrade` 必须包含在 `PhysicalModel` 中。默认情况下，`SurfaceGrade` 实例应使用 Domain 级别的 `ew:Grading` 类别。

### SurfaceGradeType（表面坡度类型）

定义可与 `ew:SurfaceGrade` 实例关联的一组共享属性和分类（即"类型"）。

**Base Class:** BisCore:PhysicalType

继承属性

| 名称 | 描述 | 类型 | 扩展类型 |
| --- | --- | --- | --- |
| Model | 包含此 `bis:Element` 的 `bis:Model`。 | navigation |  |
| LastMod | `bis:Element` 的最后修改时间。此属性由核心框架维护，应用程序不应直接设置。 | dateTime |  |
| CodeSpec | CodeSpec 属性标识用于生成和验证此 `bis:Element` 代码值的 `bis:CodeSpec`。CodeSpec、CodeScope 和 CodeValue 属性的组合对每个 `bis:Element` 实例必须是唯一的。 | navigation |  |
| CodeScope | CodeScope 属性标识为代码值提供唯一性范围的 `bis:Element`。CodeSpec、CodeScope 和 CodeValue 属性的组合对每个 `bis:Element` 实例必须是唯一的。 | navigation |  |
| CodeValue | 可空字符串属性，保存 Element 的 Code 的实际文本。CodeSpec、CodeScope 和 CodeValue 属性的组合对每个 `bis:Element` 实例必须是唯一的。 | string |  |
| UserLabel | 用户给出的可选友好名称（与存储在 CodeValue 属性中的正式名称相对）。 | string |  |
| Parent | 拥有此 `bis:Element` 的父 `bis:Element`。 | navigation |  |
| FederationGuid | 用于跨存储库联合此 `bis:Element` 的 GUID。 | binary | BeGuid |
| JsonProperties | 用户和/或应用程序可用于持久化临时 JSON 值的字符串属性。 | string | Json |
| IsPrivate | 如果为 true，此 `bis:DefinitionElement` 不应在 GUI 中显示。 | boolean |  |
| Recipe |  | navigation |  |
| PhysicalMaterial | 指示给定 `bis:PhysicalType` 的 `bis:PhysicalElements` 由哪种 `bis:PhysicalMaterial` 制成。 | navigation |  |

`SurfaceGradeType` 的实例提供了可应用于 `SurfaceGrade` 的额外分类。`SurfaceGradeType` 的实例可以选择通过其 `PhysicalMaterial` 属性指定单一的 *Physical Material*。

## Relationship Classes（关系类）

### CutIsOfType

类型-实例关系；指示特定的 `ew:Cut` 是定义的 `ew:CutType` 的实例。

**Base Class:** BisCore:PhysicalElementIsOfType

**Strength:** Referencing

**Strength Direction:** Forward

#### Source（源端）

**Is Polymorphic:** true

**Role Label:** is of

**Multiplicity:** (0..*)

#### Constraint Classes（约束类）:

- Cut

#### Target（目标端）

**Is Polymorphic:** true

**Role Label:** classifies

**Multiplicity:** (0..1)

#### Constraint Classes（约束类）:

- CutType

### FillIsOfType

类型-实例关系；指示特定的 `ew:Fill` 是定义的 `ew:FillType` 的实例。

**Base Class:** BisCore:PhysicalElementIsOfType

**Strength:** Referencing

**Strength Direction:** Forward

#### Source（源端）

**Is Polymorphic:** true

**Role Label:** is of

**Multiplicity:** (0..*)

#### Constraint Classes（约束类）:

- Fill

#### Target（目标端）

**Is Polymorphic:** true

**Role Label:** classifies

**Multiplicity:** (0..1)

#### Constraint Classes（约束类）:

- FillType

### SurfaceGradeIsOfType

类型-实例关系；指示特定的 `ew:SurfaceGrade` 是定义的 `ew:SurfaceGradeType` 的实例。

**Base Class:** BisCore:PhysicalElementIsOfType

**Strength:** Referencing

**Strength Direction:** Forward

#### Source（源端）

**Is Polymorphic:** true

**Role Label:** is of

**Multiplicity:** (0..*)

#### Constraint Classes（约束类）:

- SurfaceGrade

#### Target（目标端）

**Is Polymorphic:** true

**Role Label:** classifies

**Multiplicity:** (0..1)

#### Constraint Classes（约束类）:

- SurfaceGradeType
