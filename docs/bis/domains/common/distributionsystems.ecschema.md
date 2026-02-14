# DistributionSystems Schema

**别名 (Alias):** dsys

**版本 (Version):** 1.0.2

用于定义分配系统的 Schema。

本 Schema 包含用于分配系统物理建模的类——分配系统是旨在接收、存储、维护、分配或控制分配介质流动的网络。然而，本 Schema 的主要目标不是建模网络连接，而是建模参与分配系统的元素的物理属性及其物理连接或连接点。

一个 BIS DistributionSystem 由 IDistributionElement 组成，它们可以是引导流动的 IDistributionFlowElement、控制 IDistributionFlowElement 的 IDistributionControlElement，或者对 DistributionSystem 相关观测的 IDistributionSensorElement。

一个给定的 bis:PhysicalElement 可以实现多个 IDistributionFlowElement、IDistributionControlElement 和 IDistributionFlowElement。

以下类图描述了 DistributionSystems Schema 中的主要类和关系：

![DistributionSystems](https://www.itwinjs.org/media/distributionsystems.png)

![DistributionPorts](https://www.itwinjs.org/media/distributionports.png)

## 目录

- Entity Classes (实体类)
  - DistributionPort
  - DistributionPortType
  - DistributionSystem
  - PortConnection
- Mixins (混入类)
  - IDistributionControlElement
  - IDistributionElement
  - IDistributionElementType
  - IDistributionFlowElement
  - IDistributionSensorElement
- Relationship Classes (关系类)
  - DistributionElementOwnsDistributionPorts
  - DistributionElementTypeUsesPortTypes
  - DistributionSystemGroupsDistributionElements
  - PhysicalElementRealizesConnection
  - PortConnectionObjectifiesConnection
  - PortConnectsToPorts
- Enumerations (枚举)
  - PortDirection

## Entity Classes (实体类)

### __DistributionPort__ (分配端口) _Abstract_ EntityClass

分配元素的入口或出口，特定物质可以通过它流动。

**基类 (Base Class):** BisCore:SpatialLocationElement

分配端口是分配元素的流动连接点，特定物质可以通过它流动。

分配端口定义了分配流动元素的物理连接和物质、电力或数据流动点。DistributionPort 的子类应通过添加相关属性（如管道的 FlowVolume 或电气的 RatedVoltage）来专门化给定领域中的分配端口。尽管 `DistributionPort` 作为 `bis:SpatialLocationElement` 的子类，如果需要可以有自己的几何体，但端口通常没有任何可见的几何体。这种几何体通常由父分配元素捕获。但是，`DistributionPort` 实例必须设置其 _Origin_ 和 _Placement_ 属性，以指示其位置和方向。

分配端口由 `DistributionElement` 拥有，因为它们本质上是该元素整体定义的一部分，类似于墙上的开口。`DistributionElementOwnsDistributionPorts` 关系用于 `DistributionElement` 拥有 `DistributionPorts`。

等效于 IfcDistributionPort。

#### 属性 (Properties)

| 名称 | 描述 | 类型 | 扩展类型 |
| --- | --- | --- | --- |
| Description | Distribution Port 的人类可读描述 | string |  |
| Direction | 端口方向：例如 Input、Output、InputOrOutput、InputAndOutput。 | PortDirection |  |

继承属性

| 名称 | 描述 | 类型 | 扩展类型 |
| --- | --- | --- | --- |
| Model | 包含此 bis:Element 的 bis:Model。 | navigation |  |
| LastMod | bis:Element 的最后修改时间。由核心框架维护，应用程序不应直接设置。 | dateTime |  |
| CodeSpec | CodeSpec 属性标识用于生成和验证此 bis:Element 代码值的 bis:CodeSpec。CodeSpec、CodeScope 和 CodeValue 属性的组合对于每个 bis:Element 实例必须是唯一的。 | navigation |  |
| CodeScope | CodeScope 属性标识为代码值提供唯一性范围的 bis:Element。CodeSpec、CodeScope 和 CodeValue 属性的组合对于每个 bis:Element 实例必须是唯一的。 | navigation |  |
| CodeValue | 保存 Element 代码实际文本的可空字符串属性。CodeSpec、CodeScope 和 CodeValue 属性的组合对于每个 bis:Element 实例必须是唯一的。 | string |  |
| UserLabel | 用户给定的可选友好名称（与存储在 CodeValue 属性中的正式名称相对）。 | string |  |
| Parent | 拥有此 bis:Element 的父 bis:Element。 | navigation |  |
| FederationGuid | 用于在存储库之间联合此 bis:Element 的 GUID。 | binary | BeGuid |
| JsonProperties | 用户和/或应用程序可用于持久化临时 JSON 值的字符串属性。 | string | Json |
| Category | 用于对此 bis:GeometricElement3d 进行分类的 bis:SpatialCategory。 | navigation |  |
| InSpatialIndex | 如果为 true，则此元素将在空间索引中有条目。 | boolean |  |
| Origin | 此 bis:Element 的放置原点。 | point3d |  |
| Yaw | 此 bis:Element 方向的偏航角（以度为单位）。 | double |  |
| Pitch | 此 bis:Element 方向的俯仰角（以度为单位）。 | double |  |
| Roll | 此 bis:Element 方向的翻滚角（以度为单位）。 | double |  |
| BBoxLow | 此 bis:Element 元素对齐边界框的"低"点。 | point3d |  |
| BBoxHigh | 此 bis:Element 元素对齐边界框的"高"点。 | point3d |  |
| GeometryStream | 用于持久化此 bis:Element 几何体的二进制流。 | binary | GeometryStream |
| TypeDefinition | 指向 TypeDefinition 某个特化的实例，其中保存的是按类型而非按此元素实例变化的属性值。 | navigation |  |

### __DistributionPortType__ (分配端口类型) _Abstract_ EntityClass

定义一组共享属性，其值按 IDistributionElement 类型而非按实例变化。

**基类 (Base Class):** BisCore:SpatialLocationType

### __DistributionSystem__ (分配系统) EntityClass

旨在接收、存储、维护、分配或控制分配介质流动的网络。

**基类 (Base Class):** BisCore:PhysicalSystem

一个常见的例子是供暖热水系统，它由泵、水箱和用于将热水分配到终端的互连管道系统组成。

DistributionSystem 通过 `DistributionSystemGroupsDistributionElements` 关系对 DistributionElement 进行分组。

等效于 IfcDistributionSystem。

### __PortConnection__ (端口连接) EntityClass

指示两个分配端口之间连接的元素。

**基类 (Base Class):** BisCore:InformationRecordElement

`PortConnection` 实例在需要时将 2 个或更多 DistributionPort 之间的物理连接具体化。这通常是建模粒度级别包括实现连接的任何物理元素时的情况。在这种情况下，可以使用 `PortConnectionIsRealizedByPhysicalElements` 关系找到实现元素。

## Mixins (混入类)

### __IDistributionControlElement__ (分配控制元素) _Abstract_ Mixin

可以混入 bis:PhysicalElement 的接口，指示它是控制分配系统其他元素的 IDistributionElement。

**基类 (Base Class):** DistributionSystems:IDistributionElement

**应用于 (Applies To):** PhysicalElement

这些元素通常用于控制分配系统元素和变量，如温度、压力、功率、照明级别等。

参见 DistributionSystems。

等效于 IfcDistributionControlElement 的控制预定义类型。

### __IDistributionElement__ (分配元素) _Abstract_ Mixin

`IDistributionElement` 是参与分配系统的所有元素的泛化。IDistributionElement 的典型示例包括（但不限于）：

- 供暖系统中的元素
- 制冷系统中的元素
- 通风系统中的元素
- 管道系统中的元素
- 电气系统中的元素
- 通信网络系统中的元素

它定义了分配系统中任何 HVAC、电气、卫生或其他元素的出现。`IDistributionElement` 预期通过 `DistributionElementOwnsDistributionPorts` 关系类拥有至少一个 `DistributionPort`。

等效于 IfcDistributionElement。

分配元素应分配给它完全包含的最细粒度 SpatialStructureElement 元素。

- Space 是 distributionElement 的默认容器
- 如果分配元素跨越多个空间，则 Story 是容器
- 如果分配元素跨越多个楼层，则 Building 是默认容器。

### __IDistributionElementType__ (分配元素类型) _Abstract_ Mixin

可以混入 bis:PhysicalType 的接口，定义一组共享属性，其值按 IDistributionElement 类型而非按实例变化。

**应用于 (Applies To):** PhysicalType

### __IDistributionFlowElement__ (分配流动元素) _Abstract_ Mixin

可以混入 bis:PhysicalElement 的接口，指示它是促进能量或物质（如空气、水或电力）分配的 IDistributionElement。

**基类 (Base Class):** DistributionSystems:IDistributionElement

**应用于 (Applies To):** PhysicalElement

参见 DistributionSystems。

等效于 IfcDistributionFlowElement。

### __IDistributionSensorElement__ (分配传感器元素) _Abstract_ Mixin

可以混入 bis:PhysicalElement 的接口，指示它是观察影响分配系统条件的 IDistributionElement。

**基类 (Base Class):** DistributionSystems:IDistributionElement

**应用于 (Applies To):** PhysicalElement

分配传感器元素可用于测量温度、湿度、压力或流量等变量。

参见 DistributionSystems。

等效于 IfcDistributionControlElement 的传感预定义类型，**而不是** `IfcSensor`。

## Relationship Classes (关系类)

### __DistributionElementOwnsDistributionPorts__ _Abstract_ RelationshipClass

将子分配端口与父分配元素关联的关系。

**基类 (Base Class):** BisCore:ElementOwnsChildElements

**强度 (Strength):** Embedding

**强度方向 (Strength Direction):** Forward

#### Target

**Is Polymorphic:** true

**角色标签 (Role Label):** is owned by

**多重性 (Multiplicity):** (1..*)

**约束类 (Constraint Classes):**
- DistributionPort

### __DistributionElementTypeUsesPortTypes__ _Abstract_ RelationshipClass

将 IDistributionElementType 与其使用的 DistributionPortTypes 关联的关系。

**基类 (Base Class):** BisCore:ElementRefersToElements

**强度 (Strength):** Referencing

**强度方向 (Strength Direction):** Forward

#### Target

**Is Polymorphic:** true

**角色标签 (Role Label):** is used by

**多重性 (Multiplicity):** (0..*)

**约束类 (Constraint Classes):**
- DistributionPortType

### __DistributionSystemGroupsDistributionElements__ (Distribution System Groups Distribution Elements) RelationshipClass

用于标识 DistributionSystem 成员的 dsys:IDistributionElements 的关系。

**基类 (Base Class):** BisCore:PhysicalSystemGroupsMembers

**强度 (Strength):** Referencing

**强度方向 (Strength Direction):** Forward

#### Source

**Is Polymorphic:** true

**角色标签 (Role Label):** groups

**多重性 (Multiplicity):** (0..*)

**约束类 (Constraint Classes):**
- DistributionSystem

#### Target

**Is Polymorphic:** true

**角色标签 (Role Label):** is grouped by

**多重性 (Multiplicity):** (0..*)

**约束类 (Constraint Classes):**
- IDistributionElement

### __PhysicalElementRealizesConnection__ RelationshipClass

指示实现 DistributionPorts 之间连接的 Physical Element(s)。

**基类 (Base Class):** BisCore:ElementRefersToElements

**强度 (Strength):** Referencing

**强度方向 (Strength Direction):** Forward

当 DistributionPorts 之间的连接需要具体化时，可以引入 `PortConnection` 实例，通过其 _PortConnection_ 导航属性被 `PortConnectsToPort` 关系引用。然后可以使用 `PhysicalElementRealizesConnection` 关系将 Physical Elements 与此类 `PortConnection` 实例关联。

注意，实现连接的 Physical Elements 不是直接使 DistributionSystem 中物质流动的元素。因此，它们本身通常不是 `IDistributionElement`。

示例包括用于 Pipe 之间连接的螺栓、环或水泥。

等效于 IfcRelConnectsPorts 的 _RealizingElement_ 属性。

#### Source

**Is Polymorphic:** true

**角色标签 (Role Label):** realizes

**多重性 (Multiplicity):** (0..*)

**约束类 (Constraint Classes):**
- PhysicalElement

#### Target

**Is Polymorphic:** true

**角色标签 (Role Label):** is realized by

**多重性 (Multiplicity):** (0..1)

**约束类 (Constraint Classes):**
- PortConnection

### __PortConnectionObjectifiesConnection__ RelationshipClass

指示 DistributionPorts 之间的连接由 PortConnection 元素具体化。

**强度 (Strength):** Referencing

**强度方向 (Strength Direction):** Forward

#### Source

**Is Polymorphic:** true

**角色标签 (Role Label):** objectifies

**多重性 (Multiplicity):** (0..1)

**约束类 (Constraint Classes):**
- PortConnection

#### Target

**Is Polymorphic:** true

**角色标签 (Role Label):** is objectified by

**多重性 (Multiplicity):** (0..*)

**约束类 (Constraint Classes):**
- PortConnectsToPorts

### __PortConnectsToPorts__ _Abstract_ RelationshipClass

指示 DistributionPort 连接到其他 DistributionPort。

**基类 (Base Class):** BisCore:ElementRefersToElements

**强度 (Strength):** Referencing

**强度方向 (Strength Direction):** Forward

#### Source

**Is Polymorphic:** true

**角色标签 (Role Label):** connects to

**多重性 (Multiplicity):** (0..*)

**约束类 (Constraint Classes):**
- DistributionPort

#### Target

**Is Polymorphic:** true

**角色标签 (Role Label):** is connected by

**多重性 (Multiplicity):** (0..*)

**约束类 (Constraint Classes):**
- DistributionPort

## Enumerations (枚举)

### __PortDirection__ Enumeration

**支持类型 (Backing Type):** int

**严格 (Strict):** true

| 标签 | 值 | 描述 |
| --- | --- | --- |
| Undefined | 0 |  |
| Input | 1 |  |
| Output | 2 |  |
| Input Or Output | 3 |  |
| Input And Output | 4 |  |

---

**来源:** https://www.itwinjs.org/bis/domains/distributionsystems.ecschema/
