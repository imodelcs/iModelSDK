# LinearReferencing Schema

**别名 (Alias):** lr

**版本 (Version):** 2.0.3

线性参考的基础 Schema。

包含核心类，用于指定沿线性对象的位置。

以下类图描述了 LinearReferencing Schema 中的核心混入类 (mix-ins)：

![LinearReferencing Mixins](https://www.itwinjs.org/media/linearreferencing-mixins.png)

以下类图描述了 LinearReferencing Schema 中的核心方面类 (aspect classes)：

![LinearReferencing Aspects](https://www.itwinjs.org/media/linearreferencing-aspects.png)

## 目录

- Entity Classes (实体类)
  - LinearLocation
  - LinearLocationElement
  - LinearLocationRecord
  - LinearLocationRecordElement
  - LinearPhysicalElement
  - LinearlyLocatedAttribution
  - LinearlyReferencedAtLocation
  - LinearlyReferencedFromToLocation
  - LinearlyReferencedLocation
  - Referent
  - ReferentElement
- Mixins (混入类)
  - ILinearElement
  - ILinearElementSource
  - ILinearLocationElement
  - ILinearlyLocated
  - ILinearlyLocatedAttribution
  - IReferent
- Struct Classes (结构类)
  - DistanceExpression
- Relationship Classes (关系类)
  - ILinearElementProvidedBySource
  - ILinearLocationLocatesElement
  - ILinearlyLocatedAlongILinearElement
  - ILinearlyLocatedAttributesElement
  - ILinearlyLocatedOwnsAtLocations
  - ILinearlyLocatedOwnsFromToLocations
  - IReferentReferencesElement
  - LinearlyReferencedAtPositionRefersToReferent
  - LinearlyReferencedFromPositionRefersToReferent
  - LinearlyReferencedToPositionRefersToReferent
  - LocatedElementOwnsLocatingElements
- Kind Of Quantities (量种类)
  - LENGTH

## Entity Classes (实体类)

### __LinearLocation__ (线性位置) _Sealed_ EntityClass

ILinearLocationElement 实现，将线性参考位置附加到非固有线性参考的 bis:Element。

**基类 (Base Class):** LinearReferencing:LinearLocationElement

### __LinearLocationElement__ (线性位置元素) _Abstract_ EntityClass

bis:SpatialLocationElement 子类的 ILinearLocationElement 实现的基类。

**基类 (Base Class):** BisCore:SpatialLocationElement

### __LinearLocationRecord__ (线性位置记录) _Sealed_ EntityClass

ILinearLocationElement 实现，将线性参考位置附加到非固有线性参考的 bis:Element。

**基类 (Base Class):** LinearReferencing:LinearLocationRecordElement

### __LinearLocationRecordElement__ (线性位置记录元素) _Abstract_ EntityClass

bis:InformationRecordElement 子类的 ILinearLocationElement 实现的基类。

**基类 (Base Class):** BisCore:InformationRecordElement

### __LinearPhysicalElement__ (线性定位的物理元素) _Abstract_ EntityClass

bis:PhysicalElement 子类的 ILinearLocationElement 实现的基类。

**基类 (Base Class):** BisCore:PhysicalElement

### __LinearlyLocatedAttribution__ (线性定位的空间属性) _Abstract_ EntityClass

Spatial Location Element 的 ILinearlyLocatedAttribution 实现的基类。

**基类 (Base Class):** BisCore:SpatialLocationElement

`LinearlyLocatedAttribution` 子类的实例必须包含在 `PhysicalModel` 或 `SpatialLocationModel` 中。

### __LinearlyReferencedAtLocation__ (线性参考的 At 位置) _Sealed_ EntityClass

携带沿 Linear-Element 的"at"线性参考位置的具体多方面类。

**基类 (Base Class):** LinearReferencing:LinearlyReferencedLocation

等效于 IfcPointByDistanceExpression。

#### 属性 (Properties)

| 名称 | 描述 | 类型 | 扩展类型 |
| --- | --- | --- | --- |
| AtPosition |  | struct |  |
| FromReferent |  | navigation |  |

### __LinearlyReferencedFromToLocation__ (线性参考的 From/To 位置) _Sealed_ EntityClass

携带沿 Linear-Element 的"from/to"线性参考位置的具体多方面类。

**基类 (Base Class):** LinearReferencing:LinearlyReferencedLocation

#### 属性 (Properties)

| 名称 | 描述 | 类型 | 扩展类型 |
| --- | --- | --- | --- |
| FromPosition |  | struct |  |
| FromPositionFromReferent |  | navigation |  |
| ToPosition |  | struct |  |
| ToPositionFromReferent |  | navigation |  |

### __LinearlyReferencedLocation__ (线性参考的位置) _Abstract_ EntityClass

携带线性参考位置的多方面的基类。

**基类 (Base Class):** BisCore:ElementMultiAspect

### __Referent__ (参考点) _Sealed_ EntityClass

IReferent 实现，将任何非固有线性参考的 bis:Element 转换为线性参考用途的 Referent。

**基类 (Base Class):** LinearReferencing:ReferentElement

### __ReferentElement__ (参考点元素) _Abstract_ EntityClass

Spatial Location Element 的 IReferent 实现的基类。

**基类 (Base Class):** BisCore:SpatialLocationElement

## Mixins (混入类)

### __ILinearElement__ (线性元素) _Abstract_ Mixin

旨在扮演 Linear-Elements 角色的 Element 子类应支持的混入类。

**应用于 (Applies To):** Element

Linear-Element 是一个一维对象，作为进行测量的轴。

等效于 IfcLinearPositioningElement。

#### 属性 (Properties)

| 名称 | 描述 | 标签 | 类别 | 只读 | 优先级 |
| --- | --- | --- | --- | --- | --- |
| StartValue | Linear-Element 起点处的沿距离值，从绝对零点测量。 | Start Value |  | false | 0 |
| LengthValue | Linear-Element 的长度测量值。 | Length |  | false | 0 |
| LinearElementSource | 提供此 Linear-Element 的源元素。 | Source |  | false | 0 |

### __ILinearElementSource__ (线性元素源) _Abstract_ Mixin

旨在提供 Linear-Element 的 Element 子类应支持的混入类。

**应用于 (Applies To):** Element

### __ILinearLocationElement__ (线性位置元素) _Abstract_ Mixin

位于 Linear-Element-Source 提供的 Linear-Element 上的 Element 子类应支持的混入类。

**基类 (Base Class):** LinearReferencing:ILinearlyLocated

**应用于 (Applies To):** Element

### __ILinearlyLocated__ (线性定位的元素) _Abstract_ Mixin

沿 Linear-Element 进行线性参考的 Element 的基础混入类。

**应用于 (Applies To):** Element

`ILinearlyLocated` 混入类的实现等效于 IfcLinearPlacement。

### __ILinearlyLocatedAttribution__ (线性定位的属性) _Abstract_ Mixin

表示其值位于 Linear-Element 上且仅适用于 Linear-Element-Source 一部分的属性的 Element 子类应支持的混入类。

**基类 (Base Class):** LinearReferencing:ILinearlyLocated

**应用于 (Applies To):** Element

#### 属性 (Properties)

| 名称 | 描述 | 标签 | 类别 | 只读 | 优先级 |
| --- | --- | --- | --- | --- | --- |
| AttributedElement | 被属性化的元素。 | Attributed Element |  | false | 0 |

### __IReferent__ _Abstract_ Mixin

可以扮演 Referent（Linear-Element 上的已知位置）角色的 Element 子类应支持的混入类。

**基类 (Base Class):** LinearReferencing:ILinearlyLocated

**应用于 (Applies To):** Element

等效于 IfcReferent。注意 IfcReferent 是 IfcLinearPositioningElement，因此对它的引用使用与对 IfcLinearPositioningElement 引用相同的 IfcRelPositions.RelatingPositioningElement。另一方面，`lr:IReferent` 通过其相应的导航属性从 lr:LinearlyReferencedAtLocation 或 lr:LinearlyReferencedFromToLocation 多方面引用。

#### 属性 (Properties)

| 名称 | 描述 | 标签 | 类别 | 只读 | 优先级 |
| --- | --- | --- | --- | --- | --- |
| ReferencedElement |  | Referenced Element |  | false | 0 |

## Struct Classes (结构类)

### __DistanceExpression__ StructClass

携带线性参考信息的核心结构。

`DistanceExpression` 结构允许以绝对术语（相对于 Linear-Element 的起点）或相对于 `lr:IReferent` 捕获测量值，或两者兼有。

`DistanceExpression` 结构等效于 IfcPointByDistanceExpression。

`LateralOffsetFromILinearElement` 和 `VerticalOffsetFromILinearElement` 值被假定为从 Linear-Element 上在 `DistanceAlongFromStart` 指示的位置计算的切线垂直测量。

`LateralOffsetFromILinearElement` 中的值被假定为对于 Linear-Element 右侧的横向偏移为正，对于左侧为负，相对于其从起点的方向。

`VerticalOffsetFromILinearElement` 中的值被假定为对于 Linear-Element 上方的垂直偏移为正，对于下方为负。

这些假设等效于 IfcAxis2PlacementLinear，其 `Axis` 和 `RefDirection` 属性描述了沿 BasisCurve 的感兴趣的线性位置处的切线的垂线。

#### 属性 (Properties)

| 名称 | 描述 | 标签 | 类别 | 只读 | 优先级 |
| --- | --- | --- | --- | --- | --- |
| DistanceAlongFromStart |  | Distance-along |  | false | 0 |
| LateralOffsetFromILinearElement |  | Lateral offset |  | false | 0 |
| VerticalOffsetFromILinearElement |  | Vertical offset |  | false | 0 |
| DistanceAlongFromReferent |  | Distance-along from Referent |  | false | 0 |

## Relationship Classes (关系类)

### __ILinearElementProvidedBySource__ RelationshipClass

将 Linear-Element 与其来源元素关联的关系。

**强度 (Strength):** Referencing

**强度方向 (Strength Direction):** Forward

#### Source

**Is Polymorphic:** true

**角色标签 (Role Label):** provided by

**多重性 (Multiplicity):** (0..*)

**约束类 (Constraint Classes):**
- ILinearElement

#### Target

**Is Polymorphic:** true

**角色标签 (Role Label):** provides

**多重性 (Multiplicity):** (0..1)

**约束类 (Constraint Classes):**
- ILinearElementSource

### __ILinearLocationLocatesElement__ RelationshipClass

指示由混入 ILinearLocationElement 的具体实例进行线性定位的 bis:Element 的关系。

**基类 (Base Class):** BisCore:ElementRefersToElements

**强度 (Strength):** Referencing

**强度方向 (Strength Direction):** Forward

等效于 IfcLinearPlacement.PlacesObject。

#### Source

**Is Polymorphic:** true

**角色标签 (Role Label):** linearly-locates

**多重性 (Multiplicity):** (0..*)

**约束类 (Constraint Classes):**
- ILinearLocationElement

#### Target

**Is Polymorphic:** true

**角色标签 (Role Label):** linearly-located by

**多重性 (Multiplicity):** (0..1)

**约束类 (Constraint Classes):**
- Element

### __ILinearlyLocatedAlongILinearElement__ RelationshipClass

### __ILinearlyLocatedAttributesElement__ RelationshipClass

指示由混入 ILinearlyLocatedAttribution 的具体实例进行属性化的 bis:Element 的关系。

**强度 (Strength):** Referencing

**强度方向 (Strength Direction):** Forward

#### Target

**Is Polymorphic:** true

**角色标签 (Role Label):** is attributed by

**多重性 (Multiplicity):** (0..1)

**约束类 (Constraint Classes):**
- Element

### __ILinearlyLocatedOwnsAtLocations__ RelationshipClass

记录 ILinearlyLocated 具体实例的多方面所有权的关系。

**基类 (Base Class):** BisCore:ElementOwnsMultiAspects

**强度 (Strength):** Embedding

**强度方向 (Strength Direction):** Forward

#### Source

**Is Polymorphic:** true

**角色标签 (Role Label):** owns

**多重性 (Multiplicity):** (1..1)

**约束类 (Constraint Classes):**
- ILinearlyLocated

### __ILinearlyLocatedOwnsFromToLocations__ RelationshipClass

记录 ILinearlyLocated 具体实例的多方面所有权的关系。

**基类 (Base Class):** BisCore:ElementOwnsMultiAspects

**强度 (Strength):** Embedding

**强度方向 (Strength Direction):** Forward

#### Source

**Is Polymorphic:** true

**角色标签 (Role Label):** owns

**多重性 (Multiplicity):** (1..1)

**约束类 (Constraint Classes):**
- ILinearlyLocated

### __IReferentReferencesElement__ RelationshipClass

指示用于线性参考用途的作为 Referent 的 bis:Element 的关系。

**强度 (Strength):** Referencing

**强度方向 (Strength Direction):** Forward

#### Source

**Is Polymorphic:** true

**角色标签 (Role Label):** references

**多重性 (Multiplicity):** (0..*)

**约束类 (Constraint Classes):**
- IReferent

#### Target

**Is Polymorphic:** true

**角色标签 (Role Label):** is referenced by

**多重性 (Multiplicity):** (0..1)

**约束类 (Constraint Classes):**
- Element

### __LinearlyReferencedAtPositionRefersToReferent__ RelationshipClass

指示特定线性参考 At 位置使用的参考点的关系。

**强度 (Strength):** Referencing

**强度方向 (Strength Direction):** Forward

#### Target

**Is Polymorphic:** true

**角色标签 (Role Label):** is referenced by

**多重性 (Multiplicity):** (0..1)

**约束类 (Constraint Classes):**
- IReferent

### __LinearlyReferencedFromPositionRefersToReferent__ RelationshipClass

指示特定线性参考 From 位置使用的参考点的关系。

**强度 (Strength):** Referencing

**强度方向 (Strength Direction):** Forward

#### Target

**Is Polymorphic:** true

**角色标签 (Role Label):** is referenced by

**多重性 (Multiplicity):** (0..1)

**约束类 (Constraint Classes):**
- IReferent

### __LinearlyReferencedToPositionRefersToReferent__ RelationshipClass

指示特定线性参考 To 位置使用的参考点的关系。

**强度 (Strength):** Referencing

**强度方向 (Strength Direction):** Forward

#### Target

**Is Polymorphic:** true

**角色标签 (Role Label):** is referenced by

**多重性 (Multiplicity):** (0..1)

**约束类 (Constraint Classes):**
- IReferent

### __LocatedElementOwnsLocatingElements__ RelationshipClass

将非固有线性定位的 bis:Element 与携带其线性参考位置的子 lr:ILinearLocationElements 关联。

**基类 (Base Class):** BisCore:ElementOwnsChildElements

**强度 (Strength):** Embedding

**强度方向 (Strength Direction):** Forward

#### Source

**Is Polymorphic:** true

**角色标签 (Role Label):** owns

**多重性 (Multiplicity):** (0..1)

**约束类 (Constraint Classes):**
- Element

## Kind Of Quantities (量种类)

### __LENGTH__ (线性参考长度) KindOfQuantity

---

**来源:** https://www.itwinjs.org/bis/domains/linearreferencing.ecschema/
