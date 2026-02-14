# SpatialComposition Schema

**别名 (Alias):** spcomp

**版本 (Version):** 1.0.1

用于定义项目或资产的空间结构层次结构的类。

本 Schema 包含用于建模基础设施空间结构的类。BIS 通常遵循 IfcSpatialStructureElement 描述的 IFC"空间结构"概念。

我们的目标是与 IFC 进行 1:1 的双向实例映射（不是_类_映射！）。往返转换可能导致提供_等效_但不_相同_的 IFC 模型的变化。

SpatialStructureElements 的层次结构使用 SpatialStructureElementAggregatesElements 关系构建，类似于 IfcRelAggregates。关系的"源"Element 是一个"聚合器"，它聚合本质上是聚合器不同表示但粒度更细的部分。

空间结构可以根据需要定义任意多个层次级别。

该层次结构可以被视为面向空间的"分解结构"，用于在命名的空间"桶"（SpatialStructureElements）中组织 `bis:PhysicalElements`（和其他 `bis:SpatialElement`）。SpatialStructureElement 混入的混入类 ISpatialOrganizer 表达了其在形成分解结构中的作用。`SpatialOrganizerHoldsSpatialElements` 关系将 `bis:SpatialElement` 分配到这些"桶"中。

有时有些 `bis:SpatialElements`（由于各种原因）需要与空间结构中的"桶"关联，尽管它们被其他"桶""持有"。`SpatialOrganizerReferencesSpatialElements` 允许建立这些次要关联，尽管关联的确切含义由数据作者决定。

![SpatialOrganizer](https://www.itwinjs.org/media/spatialorganizer-classes.png)

SpatialComposition Schema 还定义了标准学科无关空间结构概念的抽象基类。

这些类是 `Region`、`Site`、`Facility`、`FacilityPart` 和 `Space`。

![SpatialStructureElements](https://www.itwinjs.org/media/spatialstructure-classes.png)

除 Region 外，所有类都映射到 IFC 中的同名概念。

添加 Region 是为了更好地表示城市和其他地理概念。

作为 `bis:SpatialLocationElements`，这些类表示区域、场地、设施等物理实体的"空间位置视角"。

以设施为例，`spcomp:Facility` 不直接建模设施的物理性，而只建模它占据的空间体积。

理论上可能存在一个对应的 `physical:Facility` 与 `spcomp:Facility` 相关联，但实际上，我们发现应用程序倾向于不创建单个 `physical:Facility` 元素来整体表示设施，而只是以更细的粒度进行物理建模。

空间结构用于在没有显式物理结构的情况下构建物理元素。

空间结构通过"holds"和"references"关系组织物理视角中的元素。

通常，空间结构的层次将遵循以下顺序：Region、Site、Facility、FacilityPart、Space，但对于什么可以聚合什么没有严格的限制。可能有一个小型建筑位于桥梁的 FacilityPart 中。一个 Space 可以属于一个 Site。将来可能会定义特定于学科的"空间分解规则"，但不太可能在 Schema 中定义，因为它们可能是特定于项目的。

Zone 不是主要空间结构的一部分，但由它组织。`Zone` 混入 ISpatialOrganizer，因此可以作为一种沿其他"维度"（由其 ZoneType 指示）组织 `bis:SpatialElements` 的方式。

![Zones](https://www.itwinjs.org/media/zone-classes.png)

BIS 没有 IFC 有争议的"CompositionType"属性的直接等效项，该属性指示 IfcSpatialStructureElement 的给定实例代表给定实体的"复合体"、"元素"（离散个体）还是"部分"。BIS 允许在 Region 内嵌套 Region、在 Site 内嵌套 Site、在 Facility 内嵌套 Facility 等，以覆盖"建筑群"或"子建筑"等用例。

## 目录

- Entity Classes (实体类)
  - CompositeElement
  - Facility
  - FacilityPart
  - FacilityPartType
  - FacilityType
  - Region
  - RegionType
  - Site
  - SiteType
  - Space
  - SpaceType
  - SpatialStructureElement
  - SpatialStructureElementType
  - Zone
  - ZoneType
- Mixins (混入类)
  - ICompositeBoundary
  - ICompositeVolume
  - ISpatialOrganizer
- Relationship Classes (关系类)
  - CompositeComposesSubComposites
  - CompositeOverlapsSpatialElements
  - FacilityIsOfType
  - FacilityPartIsOfType
  - RegionIsOfType
  - SiteIsOfType
  - SpaceIsOfType
  - SpatialOrganizerHoldsSpatialElements
  - SpatialOrganizerReferencesSpatialElements
  - SpatialStructureElementAggregatesElements
  - SpatialStructureElementIsOfType
  - ZoneIsOfType

## Entity Classes (实体类)

### __CompositeElement__ _Abstract_ EntityClass (已弃用)

请改用 SpatialStructureElement 类，该类是此类的子类，用于向后兼容。

**已弃用：** 可能由其他 CompositeElement 组成的空间元素。

**基类 (Base Class):** BisCore:SpatialLocationElement

已弃用。

请改用 SpatialStructureElement 类，该类是此类的子类，用于向后兼容。

### __Facility__ _Abstract_ EntityClass

由建筑设施（如建筑、桥梁、道路、工厂/厂房、铁路、隧道等）占据的体积。

**基类 (Base Class):** SpatialComposition:SpatialStructureElement

等效于 IfcFacility。

参见 FacilityType。

### __FacilityPart__ (设施部分) _Abstract_ EntityClass

将 Facility 分解为大于 Space 的主要部分的体积。其含义因 Facility 类型而异，但对于建筑来说是楼层 (Storey)。

**基类 (Base Class):** SpatialComposition:SpatialStructureElement

### __FacilityPartType__ (设施部分类型) _Abstract_ EntityClass

通过关联用户可定义的自定义 Type 进一步特化 FacilityPart 的特定子类。

**基类 (Base Class):** SpatialComposition:SpatialStructureElementType

### __FacilityType__ (设施类型) _Abstract_ EntityClass

通过关联用户可定义的自定义 Type 进一步特化 Facility 的特定子类。

**基类 (Base Class):** SpatialComposition:SpatialStructureElementType

### __Region__ _Abstract_ EntityClass

Site 或较小 Region 所在的地理区域。其几何体通常以 2D 边界给出，但也可以 3D 体积给出。

**基类 (Base Class):** SpatialComposition:SpatialStructureElement

在 IFC 中没有直接等效项，但可以表示为大型 IfcSite。

预期使用 RegionType 来区分高度可变的 Region 类型，例如城市、区、自治市、县、州、Land、省、国家等。

### __RegionType__ (区域类型) _Abstract_ EntityClass

通过关联用户可定义的自定义 Type 进一步特化 Region 的特定子类。

**基类 (Base Class):** SpatialComposition:SpatialStructureElementType

### __Site__ _Abstract_ EntityClass

Facility 所在地理地点的空间位置。其几何体至少可以作为点给出，但更典型的是以 2D 边界或 3D 体积给出。

**基类 (Base Class):** SpatialComposition:SpatialStructureElement

等效于 IfcSite。

参见 SiteType。

### __SiteType__ (场地类型) _Abstract_ EntityClass

通过关联用户可定义的自定义 Type 进一步特化 Site 的特定子类。

**基类 (Base Class):** SpatialComposition:SpatialStructureElementType

### __Space__ _Abstract_ EntityClass

在 FacilityPart、Facility 或 Site 内提供某种功能的物理或虚拟边界体积。具体含义因 Facility 类型而异，但 Space 往往代表楼层内的房间或房间的重要功能部分。

**基类 (Base Class):** SpatialComposition:SpatialStructureElement

等效于 IfcSpace。

参见 SpaceType。

### __SpaceType__ (空间类型) _Abstract_ EntityClass

通过关联用户可定义的自定义 Type 进一步特化 Space 的特定子类。

**基类 (Base Class):** SpatialComposition:SpatialStructureElementType

### __SpatialStructureElement__ (空间结构元素) _Abstract_ EntityClass

用于形成空间分解结构的 Element。作为 ISpatialOrganizer，它可以显式地"持有"或"引用"SpatialElements。

**基类 (Base Class):** SpatialComposition:CompositeElement

等效于 IfcSpatialStructureElement。

参见 Schema 概述以获取更多信息。

#### 属性 (Properties)

| 名称 | 描述 | 类型 | 扩展类型 |
| --- | --- | --- | --- |
| Description | 此 Spatial Structure Element 的人类可读描述 | string |  |

### __SpatialStructureElementType__ (空间结构元素类型) _Abstract_ EntityClass

通过关联用户可定义的自定义 Type 进一步特化 Spatial Structure Element 的特定子类。

**基类 (Base Class):** BisCore:SpatialLocationType

这些类型允许不同地区的项目定义与其相关的 Spatial Structure Element 类型。

### __Zone__ _Abstract_ EntityClass

定义与特定目的关联的空间区域。作为 ISpatialOrganizer，它可以显式地"持有"或"引用"SpatialElements。

**基类 (Base Class):** BisCore:SpatialLocationElement

### __ZoneType__ (区域类型) _Abstract_ EntityClass

通过关联用户可定义的自定义 Type 进一步特化 Zone 的特定子类。

**基类 (Base Class):** BisCore:SpatialLocationType

与 Zone 一起使用，定义用于组织 `bis:SpatialElement` 的标准，该标准与主要空间分解结构"正交"。

例如，`ZoneType` 为"Tenancy"的 `Zone` 根据哪个租户租赁了哪个区域来划分空间。

## Mixins (混入类)

### __ICompositeBoundary__ _Abstract_ Mixin (已弃用)

与 CompositeElement 一起已弃用，因此不再推荐使用。

**已弃用：** 指示 CompositeElement 由曲线限定的可选接口。

**应用于 (Applies To):** CompositeElement

已弃用。

用于指示元素是边界类型的混入类，边界类型最常见的是一组弯曲几何体。

原始数据通常是地图上的点、边界描述字符串或类似形式。

`ICompositeBoundary` 是混入类，不映射到或从 IFC 映射。

### __ICompositeVolume__ _Abstract_ Mixin (已弃用)

与 CompositeElement 一起已弃用，因此不再推荐使用。

**已弃用：** 指示 CompositeElement 由体积限定的可选接口。

**应用于 (Applies To):** CompositeElement

已弃用。

用于指示元素是体积类型的混入类，体积类型最常见的是拉伸几何体。

`ICompositeVolume` 是混入类，不映射到或从 IFC 映射。

### __ISpatialOrganizer__ (空间组织者) _Abstract_ Mixin

使用 'SpatialOrganizerHoldsSpatialElements' 和 'SpatialOrganizerReferencesSpatialElements' 组织 bis:SpatialElements 的 bis:SpatialLocation。

**应用于 (Applies To):** SpatialLocationElement

组织可以根据任何"标准"或"维度"进行。

目前仅由 SpatialStructureElement 和 Zone 使用，`ISpatialOrganizer` 是用于组织 `bis:SpatialElement` 的 holds 和 references 关系的"源"端。

参见 Schema 概述以获取更多上下文。

## Relationship Classes (关系类)

### __CompositeComposesSubComposites__ RelationshipClass (已弃用)

请改用 SpatialStructureElementAggregatesSpatialStructureElements 关系，该关系是此关系的子类，用于向后兼容。

**已弃用**

**强度 (Strength):** Embedding

**强度方向 (Strength Direction):** Forward

#### Source

**Is Polymorphic:** true

**角色标签 (Role Label):** aggregates

**多重性 (Multiplicity):** (0..1)

**约束类 (Constraint Classes):**
- CompositeElement

#### Target

**Is Polymorphic:** true

**角色标签 (Role Label):** is aggregated by

**多重性 (Multiplicity):** (0..*)

**约束类 (Constraint Classes):**
- CompositeElement

### __CompositeOverlapsSpatialElements__ RelationshipClass (已弃用)

请改用 SpatialOrganizerHoldsSpatialElements 或 SpatialOrganizerReferencesSpatialElements 关系。

**已弃用：** 指示元素至少部分包含在 CompositeElement 内的关系。

**基类 (Base Class):** BisCore:ElementRefersToElements

**强度 (Strength):** Referencing

**强度方向 (Strength Direction):** Forward

已弃用。

请改用 SpatialOrganizerHoldsSpatialElements 或 SpatialOrganizerReferencesSpatialElements 关系。

### __FacilityIsOfType__ (Facility Is Of Facility Type) RelationshipClass

将 Facility 与其 Type 定义关联。

**基类 (Base Class):** SpatialComposition:SpatialStructureElementIsOfType

**强度 (Strength):** Referencing

**强度方向 (Strength Direction):** Forward

### __FacilityPartIsOfType__ (FacilityPart Is Of FacilityPart Type) RelationshipClass

将 FacilityPart 与其 Type 定义关联。

**基类 (Base Class):** SpatialComposition:SpatialStructureElementIsOfType

**强度 (Strength):** Referencing

**强度方向 (Strength Direction):** Forward

### __RegionIsOfType__ (Region Is Of Region Type) RelationshipClass

将 Region 与其 Type 定义关联。

**基类 (Base Class):** SpatialComposition:SpatialStructureElementIsOfType

**强度 (Strength):** Referencing

**强度方向 (Strength Direction):** Forward

### __SiteIsOfType__ (Site Is Of Site Type) RelationshipClass

将 Site 与其 Type 定义关联。

**基类 (Base Class):** SpatialComposition:SpatialStructureElementIsOfType

**强度 (Strength):** Referencing

**强度方向 (Strength Direction):** Forward

### __SpaceIsOfType__ (Space Is Of Space Type) RelationshipClass

将 Space 与其 Type 定义关联。

**基类 (Base Class):** SpatialComposition:SpatialStructureElementIsOfType

**强度 (Strength):** Referencing

**强度方向 (Strength Direction):** Forward

### __SpatialOrganizerHoldsSpatialElements__ (Spatial Organizer Holds Spatial Elements) RelationshipClass

组织 bis:SpatialElements，使每个 bis:SpatialElement 被 0 或 1 个"组织者""持有"。

**基类 (Base Class):** BisCore:ElementRefersToElements

**强度 (Strength):** Referencing

**强度方向 (Strength Direction):** Forward

"holds"关系用于将 `bis:SpatialElement` 组织成严格类别，使给定的 `bis:SpatialElement` 最多只被一个"组织者""持有"。

"组织"的范围（可以在其中检查每个组织者一个 SpatialElement 规则的范围）将根据混入 ISpatialOrganizer 的类而变化。

正如 SpatialStructureElement 和 Zone 所使用的，`SpatialOrganizerHoldsSpatialElements` 等效于 IfcRelContainedInSpatialStructure（反向导航）。

在该上下文中，在 IFC 和 BIS 中，"holds"_不_意味着几何空间包含，尽管在给定"空间结构元素"内空间包含的 `bis:SpatialElement`_很可能_被该"空间结构元素""持有"，除非它们已被分配（出于逻辑原因）给层次结构中更深的其他"空间结构元素"。例如，ElevatorShaft 可能只在空间上被整个建筑包含，但被分配为被"Basement"楼层"持有"。通常，如果 `bis:SpatialElement` 完全包含在 `Space` 中，它将被该 `Space`"持有"，但 `Space` 之外的元素（如分体式空调的"室外"一半）也可能被该 `Space`"持有"。

参见 Schema 概述以获取更多上下文。

### __SpatialOrganizerReferencesSpatialElements__ (Spatial Organizer References Spatial Elements) RelationshipClass

组织 bis:SpatialElements，使每个 bis:SpatialElement 可以被 0 个或多个"组织者""引用"。

**基类 (Base Class):** BisCore:ElementRefersToElements

**强度 (Strength):** Referencing

**强度方向 (Strength Direction):** Forward

"references"关系被希望松散组织 `bis:SpatialElement` 的"组织者"使用，使给定的 `bis:SpatialElement` 可以被多个"组织者""引用"。

正如 SpatialStructureElement 和 Zone 所使用的，`SpatialOrganizerReferencesSpatialElements` 等效于 IfcRelReferencedInSpatialStructure（反向导航）。

在该上下文中，在 IFC 和 BIS 中，关联的确切含义由数据作者决定。它可能与几何空间交集相关，也可能不相关。

例如，ElevatorShaft Element 可能被它_服务_的所有楼层"引用"，即使它可能不被它穿过但不服务的楼层引用。

参见 Schema 概述以获取更多上下文。

### __SpatialStructureElementAggregatesElements__ (Spatial Structure Element Aggregates Spatial Structure Elements) RelationshipClass

形成空间结构。聚合元素的体积不应重叠，通常应加起来等于聚合器（聚合元素）的体积，并在空间上位于聚合器内。

**基类 (Base Class):** SpatialComposition:CompositeComposesSubComposites

**强度 (Strength):** Embedding

**强度方向 (Strength Direction):** Forward

等效于 IfcRelAggregates。

形成严格的层次结构（一个空间结构元素只能被单个"聚合器"聚合）。

参见 Schema 概述以获取更多信息。

### __SpatialStructureElementIsOfType__ (Spatial Structure Element Is Of Spatial Structure Element Type) RelationshipClass

将 Spatial Structure Element 与其 Type 定义关联。

**基类 (Base Class):** BisCore:SpatialLocationIsOfType

**强度 (Strength):** Referencing

**强度方向 (Strength Direction):** Forward

### __ZoneIsOfType__ (Zone Is Of Zone Type) RelationshipClass

将 Zone 与其 Type 定义关联。

**基类 (Base Class):** BisCore:SpatialLocationIsOfType

**强度 (Strength):** Referencing

**强度方向 (Strength Direction):** Forward

---

**来源:** https://www.itwinjs.org/bis/domains/spatialcomposition.ecschema/
