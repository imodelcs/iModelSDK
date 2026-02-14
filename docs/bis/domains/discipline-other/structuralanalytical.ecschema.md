# StructuralAnalysis ECSchema

> **Structural Analysis Schema** - 结构分析 Schema
>
> **别名 (Alias):** `sa`
>
> **版本:** 01.00.05
>
> **Schema 层级:** DisciplineOther

## 概述

StructuralAnalysis Schema 定义了用于结构分析的数据模型，包含拓扑元素、构件 (Member)、支承 (Support)、荷载 (Load) 等核心概念。该 Schema 继承自 Analytical Schema，遵循 BIS (Base Infrastructure Schema) 框架。

**注意:** 此 Schema 当前标记为 `NotForProduction`（非生产用途）。

## 引用的 Schema

| Schema | 版本 | 别名 |
|--------|------|------|
| CoreCustomAttributes | 01.00.03 | CoreCA |
| BisCustomAttributes | 01.00.00 | bisCA |
| BisCore | 01.00.10 | bis |
| Profiles | 01.00.00 | prf |
| Analytical | 01.00.00 | anlyt |
| AecUnits | 01.00.03 | AECU |

---

## 枚举类型 (Enumerations)

### PlacementPoint - 放置点

定义 Profile 边界框上的标准放置点。

| 值 | 名称 | 显示标签 | 描述 |
|---|------|---------|------|
| 0 | LeftBottom | Left Bottom | 最底部左侧 Profile 边界框点 |
| 1 | MiddleBottom | Middle Bottom | 最底部中心 Profile 边界框点 |
| 2 | RightBottom | Right Bottom | 最底部右侧 Profile 边界框点 |
| 3 | LeftMiddle | Left Middle | Profile 边界框水平中线最左侧点 |
| 4 | MiddleMiddle | Middle Middle | Profile 边界框中心点 |
| 5 | RightMiddle | Right Middle | Profile 边界框水平中线最右侧点 |
| 6 | LeftTop | Left Top | 最顶部左侧 Profile 边界框点 |
| 7 | MiddleTop | Middle Top | 最顶部中心 Profile 边界框点 |
| 8 | RightTop | Right Top | 最顶部右侧 Profile 边界框点 |
| 9 | Centroid | Centroid | 形状切面可完美平衡的点（形心） |
| 10 | CentroidBottom | Centroid Bottom | 最底部水平线上最接近几何形心的点 |
| 11 | LeftCentroid | Left Centroid | 最左侧垂直线上最接近几何形心的点 |
| 12 | RightCentroid | Right Centroid | 最右侧垂直线上最接近几何形心的点 |
| 13 | CentroidTop | Centroid Top | 最顶部水平线上最接近几何形心的点 |
| 14 | ShearCenter | Shear Centre | 施加外力不会使 Profile 扭转的点（剪切中心） |
| 15 | ShearBottom | Shear Bottom | 最底部水平线上最接近剪切中心的点 |
| 16 | LeftShear | Left Shear | 最左侧垂直线上最接近剪切中心的点 |
| 17 | RightShear | Right Shear | 最右侧垂直线上最接近剪切中心的点 |
| 18 | ShearTop | Shear Top | 最顶部水平线上最接近剪切中心的点 |

### CurveMemberClassificationType - 曲线构件分类类型

用于设置 CurveMember 的分类。

| 值 | 名称 | 显示标签 | 描述 |
|---|------|---------|------|
| 0 | Unset | Unset | 分类未定义 |
| 1 | Beam | Beam | 主要承受垂直于梁长度方向荷载的结构构件 |
| 2 | Column | Column | 主要承受沿梁长度方向荷载的结构构件 |
| 3 | HorizontalBrace | Horizontal Brace | 常用于承受风和地震压力等横向荷载的结构系统，每层的水平面支撑提供水平力传递到垂直支撑平面的荷载路径 |
| 4 | StripFooting | Strip Footing | 为墙或密集排列的柱提供连续、水平（或有时阶梯状）条形基础的结构构件 |
| 5 | Pedestal | Pedestal | 安装柱子的基座 |
| 6 | Pile | Pile | 深基础的垂直结构构件，在建筑工地打入或钻入地下深处 |
| 7 | VerticalBrace | Vertical Brace | 常用于承受风和地震压力等横向荷载的结构系统，柱线之间的垂直面支撑提供水平力传递到地面的荷载路径 |

### SurfaceMemberClassificationType - 表面构件分类类型

用于设置 SurfaceMember 的分类。

| 值 | 名称 | 显示标签 |
|---|------|---------|
| 0 | Unset | Unset |
| 1 | Cladding | Cladding（覆层） |
| 2 | Footing | Footing（基础） |
| 3 | PileCap | Pile Cap（桩帽） |
| 4 | Slab | Slab（板） |
| 5 | SpreadFooting | Spread Footing（扩展基础） |
| 6 | Wall | Wall（墙） |

### PlacementSurface - 放置表面

用于设置表面的位置。

| 值 | 名称 | 显示标签 | 描述 |
|---|------|---------|------|
| 0 | Top | Top | 拓扑定义表面的顶部边界 |
| 1 | Middle | Middle | 拓扑定义表面深度中点的边界 |
| 2 | Bottom | Bottom | 拓扑定义表面的底部边界 |

### BendingBehaviorValue - 弯曲行为值

描述构件对横向荷载的结构行为。

| 值 | 名称 | 显示标签 | 描述 |
|---|------|---------|------|
| 0 | Unset | Unset | 表示此值从未设置 |
| 1 | OneWay | One Way | 此构件可在一个方向（沿区域 r 轴）跨越横向荷载 |
| 2 | TwoWay | Two Way | 此构件可在两个（垂直）方向（r 轴和 s 轴）跨越横向荷载 |
| 3 | TwoWayTwistFree | Two Way Twist Free | 此构件可在两个（垂直）方向跨越横向荷载，但不能抵抗（r-s）扭转弯矩 |

### LoadResistance - 荷载抵抗

根据构件能抵抗的荷载类型进行分类。

| 值 | 名称 | 显示标签 | 描述 |
|---|------|---------|------|
| 0 | Unset | Unset | 值未设置 |
| 1 | GravityOnly | Gravity only | 仅抵抗重力荷载 |
| 2 | GravityAndLateral | Gravity and Lateral | 同时抵抗重力和横向荷载 |
| 3 | LateralOnly | Lateral only | 仅抵抗横向荷载 |
| 4 | NonStructural | Non Structural | 不用于抵抗荷载 |

### AxialBehavior - 轴向行为

描述构件在轴向荷载作用下的结构行为。

| 值 | 名称 | 显示标签 | 描述 |
|---|------|---------|------|
| 0 | Unset | Unset | 值未设置 |
| 1 | CompressionAndTension | Compression and Tension | 同时抵抗压力和拉力 |
| 2 | CompressionOnly | Compression only | 抵抗轴向压力，但不抵抗轴向拉力 |
| 3 | TensionOnly | Tension only | 抵抗轴向拉力，但不抵抗轴向压力 |

### ReleaseType - 释放类型

用于指定 Release（约束释放）的类型。

| 值 | 名称 | 显示标签 |
|---|------|---------|
| 0 | Unspecified | Unspecified（未指定） |
| 1 | Released | Released（释放） |
| 2 | Fixed | Fixed（固定） |

### CoordinateSystem - 坐标系

用于设置荷载的坐标系。

| 值 | 名称 | 显示标签 | 描述 |
|---|------|---------|------|
| 0 | Global | Global | 荷载定义在全局坐标系中 |
| 1 | Local | Local | 荷载定义在宿主的局部坐标系中 |

### LoadType - 荷载类型

用于在 LoadContainer 中指定荷载类型。

| 值 | 名称 | 显示标签 | 描述 |
|---|------|---------|------|
| 0 | Unset | Unset | 荷载类型未设置 |
| 1 | Other | Other | 荷载类型未被其他可用类型指定 |
| 2 | Blast | Blast | 爆炸产生的冲击波力 |
| 3 | DeadUnspecified | Dead Unspecified | 不随时间变化且来源未指定的荷载 |
| 4 | DeadStructure | Dead Structure | 结构自重产生的恒载 |
| 5 | DeadSuperimposed | Dead Superimposed | 除结构自重以外的恒载 |
| 6 | DeadConstruction | Dead Construction | 仅在施工期间存在的非结构恒载 |
| 7 | EarthPressureUnspecified | Earth Pressure Unspecified | 某未指定设计水平的土压力 |
| 8 | EarthPressureService | Earth Pressure Service | 正常使用极限状态的土压力荷载 |
| 9 | EarthPressureUltimate | Earth Pressure Ultimate | 极限极限状态的土压力荷载 |
| 10 | Equipment | Equipment | 设备产生的荷载 |
| 11 | FloorUnspecified | Floor Unspecified | 楼面荷载，无进一步说明 |
| 12 | FloorConstruction | Floor Construction | 仅在施工期间存在的楼面荷载 |
| 13 | FloorResidential | Floor Residential | 住宅使用产生的楼面荷载 |
| 14 | FloorOffice | Floor Office | 办公使用产生的楼面荷载 |
| 15 | FloorAssembly | Floor Assembly | 集会使用产生的楼面荷载 |
| 16 | FloorStorage | Floor Storage | 储存使用产生的楼面荷载 |
| 17 | FloorRetail | Floor Retail | 零售/购物使用产生的楼面荷载 |
| 18 | FluidUnspecified | Fluid Unspecified | 流体产生的荷载，无进一步说明 |
| 19 | FluidContained | Fluid Contained | 已知密度的流体被已知高度的墙容纳（如水箱或油箱） |
| 20 | FluidUncontained | Fluid Uncontained | 未知密度或未知高度的流体（如静水洪水） |
| 21 | GroundWaterPressure | Ground Water Pressure | 地下水压力产生的荷载 |
| 22 | Hydrodynamic | Hydrodynamic | 运动流体产生的荷载 |
| 23 | Hydrostatic | Hydrostatic | 静水压力产生的荷载 |
| 24 | Ice | Ice | 大气冰（雨在结构上冻结等） |
| 25 | MechanicalVibration | Mechanical Vibration | 振荡或旋转设备产生的荷载 |
| 26 | Notional | Notional | 由垂直荷载产生的横向荷载，考虑初始缺陷的影响 |
| 27 | ParkingUnspecified | Parking Unspecified | 停车使用产生的楼面荷载 |
| 28 | ParkingLight | Parking Light | 轻型车辆停车使用产生的楼面荷载 |
| 29 | ParkingHeavy | Parking Heavy | 重型车辆停车使用产生的楼面荷载 |
| 30 | PostTensioning | Post Tensioning | 后张拉应用产生的荷载 |
| 31 | PostTensioningRestraint | Post Tensioning Restraint | 后张拉约束产生的理论荷载 |
| 32 | Hyperstatic | Hyperstatic | 后张拉约束产生的理论荷载 |
| 33 | RoofUnspecified | Roof Unspecified | 屋面荷载，无进一步说明 |
| 34 | RoofAccess | Roof Access | 屋面检查、维修等产生的屋面荷载 |
| 35 | RoofRain | Roof Rain | 雨水积聚产生的屋面荷载 |
| 36 | RoofSnowUnspecified | Roof Snow Unspecified | 雪荷载，无进一步说明 |
| 37 | RoofSnowUniform | Roof Snow Uniform | 均匀雪荷载，通常作为 RoofSnowDrift 的替代 |
| 38 | RoofSnowDrift | Roof Snow Drift | 堆积雪荷载，通常作为 RoofSnowUniform 的替代 |
| 39 | SeismicUnspecified | Seismic Unspecified | 某未指定设计水平的地震荷载 |
| 40 | SeismicService | Seismic Service | 正常使用极限状态的地震荷载 |
| 41 | SeismicUltimate | Seismic Ultimate | 极限极限状态的地震荷载 |
| 42 | Settlement | Settlement | 支座沉降产生的荷载 |
| 43 | Shrinkage | Shrinkage | 构件收缩产生的荷载 |
| 44 | Thermal | Thermal | 温度变化或温差产生的荷载 |
| 45 | TimeHistory | Time History | 随时间非线性施加的力产生的荷载 |
| 46 | WindUnspecified | Wind Unspecified | 某未指定设计水平的风荷载 |
| 47 | WindService | Wind Service | 正常使用极限状态的风荷载 |
| 48 | WindUltimate | Wind Ultimate | 极限极限状态的风荷载 |

### LoadCombinationType - 荷载组合类型

指定将荷载组合成单一组的方法。

| 值 | 名称 | 显示标签 | 描述 |
|---|------|---------|------|
| 0 | Normal | Normal | 正常组合 |
| 1 | ABS | ABS | 绝对值法 |
| 2 | SRSS | SRSS | 平方和平方根法 |

### CurveVariationType - 曲线变化类型

曲线荷载变化类型的枚举。

| 值 | 名称 | 显示标签 | 描述 |
|---|------|---------|------|
| 0 | Linear | Linear | 曲线点上的力沿宿主曲线线性变化 |
| 1 | Parabola | Parabola | 点上的力沿宿主曲线抛物线变化 |

### SurfaceVariationType - 表面变化类型

表面荷载变化类型的枚举。

| 值 | 名称 | 显示标签 | 描述 |
|---|------|---------|------|
| 0 | Plane | Plane | 平面点上的力从平面中某特定点线性变化 |
| 1 | Parabola | Parabola | 平面点上的力从平面中某特定点抛物线变化 |

### SpringBehaviorType - 弹簧行为类型

| 值 | 名称 | 显示标签 | 描述 |
|---|------|---------|------|
| 0 | CompressionOnly | Compression Only | 支承仅抵抗压力 |
| 1 | TensionOnly | Tension Only | 支承仅抵抗拉力 |
| 2 | CompressionAndTension | Compression and Tension | 支承同时抵抗压力和拉力 |

### MaterialProfileCategoryType - 材料剖面类别类型

MaterialProfile 的角色。

| 值 | 名称 | 显示标签 |
|---|------|---------|
| 0 | LoadBearing | Load Bearing（承重） |

---

## 实体类 (Entity Classes)

### 模型与分区

#### StructuralAnalysisModel

**显示标签:** Structural Analysis Model

**描述:** 包含所有 StructuralAnalysis 元素的 Model。

**基类:** `anlyt:AnalyticalModel`

**修饰符:** Sealed

---

#### StructuralAnalysisPartition

**显示标签:** Structural Analysis Partition

**描述:** StructuralAnalysisPartition 元素表示在整体信息层次结构中存在专门的 StructuralAnalysis 视角。

**基类:** `anlyt:AnalyticalPartition`

**导航属性:**

| 属性名 | 关系 | 描述 |
|--------|------|------|
| DefaultDefinitionContainer | StructuralAnalysisPartitionRefersToDefinitionContainer | 定义元素的默认位置 |

**修饰符:** Sealed

---

### 拓扑类 (Topology Classes)

#### TopologyElement

**显示标签:** Topology Element

**描述:** 所有拓扑相关类的抽象基类。

**基类:** `anlyt:AnalyticalElement`

**修饰符:** Abstract

---

#### SharedTopologyElement

**显示标签:** Shared Topology Element

**描述:** 可被多个其他元素共享的抽象拓扑类。共享定义了拓扑网络的连接性。每个子类也是特定维度性的最低级别概念（Face 是最低的 2D 概念）。

**基类:** `TopologyElement`

**修饰符:** Abstract

---

#### PrivateTopologyElement

**显示标签:** Private Topology Element

**描述:** 不共享的每种拓扑类型的公共父类抽象类。每个子类表示共享拓扑的直接或间接集合。每个子类也是相同维度性拓扑的集合。

**基类:** `TopologyElement`

**修饰符:** Abstract

---

#### Vertex

**显示标签:** Vertex

**描述:** 3D 空间中已识别的位置点。

**基类:** `SharedTopologyElement`, `IDefinedPoint`

**属性:**

| 属性名 | 类型 | 描述 | 数量类型 |
|--------|------|------|----------|
| Point | point3d | 描述 Vertex 位置。点仅在 Vertex 创建时设置，无法修改 | AECU:LENGTH |

**修饰符:** Sealed

---

#### Edge

**显示标签:** Edge

**描述:** 3D 空间中已识别的曲线位置。

**基类:** `SharedTopologyElement`

**属性:**

| 属性名 | 类型 | 描述 |
|--------|------|------|
| Curve | Bentley.Geometry.Common.IGeometry | 定义 Edge 位置的非自相交曲线 |

**导航属性:**

| 属性名 | 关系 | 描述 |
|--------|------|------|
| StartVertex | EdgeHasStartVertex | 起点 Vertex |
| EndVertex | EdgeHasEndVertex | 终点 Vertex |

**修饰符:** Sealed

---

#### Face

**显示标签:** Face

**描述:** 由 Loop 边界的表面。

**基类:** `SharedTopologyElement`, `ILoopOwner`, `IPathsOwner`

**修饰符:** Sealed

---

#### Path (抽象)

**显示标签:** Path

**描述:** 定义连续分析曲线的 Edge 系列。

**基类:** `PrivateTopologyElement`

**修饰符:** Abstract

---

#### Loop

**显示标签:** Loop

**描述:** 闭合的 Path，定义 Face 的边界。

**基类:** `Path`

**修饰符:** Sealed

---

#### Wire

**显示标签:** Wire

**描述:** 不需要闭合且不定义面边界的 Path。

**基类:** `Path`

**修饰符:** Sealed

---

#### FaceSet

**显示标签:** Face Set

**描述:** 具有兼容方向的边连接 Face 集合。

**基类:** `PrivateTopologyElement`

**修饰符:** Abstract

---

#### Sheet

**显示标签:** Sheet

**描述:** 可以是开放或闭合的 FaceSet，不边界 Region（未来概念）。Sheet 也被限制为具有单一基础 Surface。

**基类:** `FaceSet`

**修饰符:** Sealed

---

### 构件类 (Member Classes)

#### Member (抽象)

**显示标签:** Member

**描述:** 所有构件类的抽象基类。

**基类:** `StructuralAnalysisElement`, `IStoryAssignable`

**修饰符:** Abstract

---

#### CurveMember

**显示标签:** Curve Member

**描述:** 定义沿 Path 定位的构件，其行为沿该 Path 定义。

**基类:** `Member`, `IWireOwner`, `IDefinedCurve`

**属性:**

| 属性名 | 类型 | 描述 | 数量类型 |
|--------|------|------|----------|
| PlacementPoint | string | Curve Member 拓扑与 Profile 相交的点 | - |
| Classification | CurveMemberClassificationType | 此 Curve Member 的用例 | - |
| StartRigidZoneLength | double | 定义 Curve Member 起始处的刚性区长度。刚性区指定 Curve Member 在该区域内不变形 | AECU:LENGTH_SHORT |
| EndRigidZoneLength | double | 定义 Curve Member 终点处的刚性区长度 | AECU:LENGTH_SHORT |
| Offset | point2d | 在局部坐标系中定义的 2D 偏移 | AECU:LENGTH_SHORT |
| IsProfileMirrored | boolean | 指定 Profile 是否应关于方向镜像 | - |

**修饰符:** Sealed

---

#### SurfaceMember

**显示标签:** Surface Member

**描述:** 定义由 Sheet 定位的构件。

**基类:** `Member`, `ISheetOwner`, `IStructuralSurface`, `IDefinedSurface`, `bis:IParentElement`

**属性:**

| 属性名 | 类型 | 描述 |
|--------|------|------|
| Classification | SurfaceMemberClassificationType | 此 Surface Member 的用例 |

**修饰符:** Sealed

---

#### SurfaceMemberRegion (抽象)

**显示标签:** Surface Member Region

**描述:** 定义具有不同行为（或为开口）的 SurfaceMember 区域。

**基类:** `StructuralAnalysisElement`, `ISheetOwner`

**修饰符:** Abstract

---

#### SurfaceMemberModifier

**显示标签:** Surface Member Modifier

**描述:** 定义具有不同行为的 SurfaceMember 实体区域。

**基类:** `SurfaceMemberRegion`, `IStructuralSurface`

**属性:**

| 属性名 | 类型 | 描述 |
|--------|------|------|
| Priority | int | 定义 SurfaceMemberModifier 的优先级。数字越高优先级越高 |

**修饰符:** Sealed

---

#### SurfaceMemberOpening

**显示标签:** Surface Member Opening

**描述:** 定义 SurfaceMember 的空洞区域。

**基类:** `SurfaceMemberRegion`

**修饰符:** Sealed

---

### 支承类 (Support Classes)

#### Support (抽象)

**显示标签:** Support

**描述:** 所有支承类的抽象基类。

**基类:** `StructuralAnalysisElement`, `IStoryAssignable`

**修饰符:** Abstract

---

#### PointSupport

**显示标签:** Point Support

**描述:** 位于单点的支承。

**基类:** `Support`, `IDefinedPoint`

**属性:**

| 属性名 | 类型 | 描述 |
|--------|------|------|
| RAxis | point3d | 局部坐标系的 R 轴 |
| SAxis | point3d | 局部坐标系的 S 轴 |

**导航属性:**

| 属性名 | 关系 | 描述 |
|--------|------|------|
| Vertex | PointSupportRefersToVertex | 此实例支撑的 Vertex |
| Behavior | PointSupportRefersToPointSupportBehavior | Point Support Behavior |

**修饰符:** Sealed

---

#### CurveSupport

**显示标签:** Curve Support

**描述:** 位于曲线上的支承。

**基类:** `Support`, `IWireOwner`, `IDefinedCurve`

**导航属性:**

| 属性名 | 关系 | 描述 |
|--------|------|------|
| Behavior | CurveSupportRefersToCurveSupportBehavior | 定义支承在其位置的行为方式 |

**修饰符:** Sealed

---

#### SurfaceSupport

**显示标签:** Surface Support

**描述:** 位于表面上的支承。

**基类:** `Support`, `ISheetOwner`, `IDefinedSurface`

**导航属性:**

| 属性名 | 关系 | 描述 |
|--------|------|------|
| Behavior | SurfaceSupportRefersToSurfaceSupportBehavior | 定义支承在其位置的行为方式 |

**修饰符:** Sealed

---

### 荷载类 (Load Classes)

#### Load (抽象)

**显示标签:** Load

**描述:** 影响分析构件的荷载。

**基类:** `StructuralAnalysisElement`

**属性:**

| 属性名 | 类型 | 描述 |
|--------|------|------|
| CoordinateSystem | CoordinateSystem | 荷载的局部坐标系 |

**修饰符:** Abstract

---

#### PointLoad

**显示标签:** Point Load

**描述:** 作用于点的荷载。

**基类:** `Load`

**修饰符:** Sealed

---

#### CurveLoad

**显示标签:** Curve Load

**描述:** 沿曲线施加的荷载。

**基类:** `Load`

**修饰符:** Sealed

---

#### SurfaceLoad

**显示标签:** Surface Load

**描述:** 在表面上施加的荷载。

**基类:** `Load`

**修饰符:** Sealed

---

### 荷载容器与组合

#### LoadContainer (抽象)

**显示标签:** Load Container

**描述:** 荷载的集合。

**基类:** `StructuralAnalysisElement`, `bis:IParentElement`

**属性:**

| 属性名 | 类型 | 描述 |
|--------|------|------|
| LoadType | LoadType | 荷载类型 |
| SelfWeightVector | Point3d | 自重向量 |

**修饰符:** Abstract

---

#### LoadGroup

**显示标签:** Load Group

**描述:** 仅用于分组目的的荷载集合。

**基类:** `LoadContainer`

**修饰符:** Sealed

---

#### LoadCase

**显示标签:** Load Case

**描述:** 作为工况作用于结构的荷载集合。

**基类:** `LoadContainer`, `ILoadCondition`

**修饰符:** Sealed

---

#### LoadCombinationInformation

**显示标签:** Load Combination

**描述:** 将一组同时或顺序应用于结构的荷载工况分组的元素。

**基类:** `bis:InformationRecordElement`, `ILoadCondition`

**属性:**

| 属性名 | 类型 | 描述 |
|--------|------|------|
| SrssFactor | double | 乘以 SRSS 添加的荷载条件乘积的系数 |

**修饰符:** Sealed

---

#### FactoredLoadCase

**显示标签:** Factored Load Case

**基类:** `FactoredLoadCondition`

**属性:**

| 属性名 | 类型 | 描述 |
|--------|------|------|
| Factor | double | 应用于组的系数 |
| LoadCombinationType | LoadCombinationType | 荷载组合类型 |

**导航属性:**

| 属性名 | 关系 | 描述 |
|--------|------|------|
| LoadCase | FactoredLoadCaseRefersToLoadCase | 荷载工况 |

**修饰符:** Sealed

---

### 行为方面类 (Behavior Aspect Classes)

#### BehaviorAspect (抽象)

**显示标签:** Behavior Aspect

**描述:** 为元素定义结构行为。

**基类:** `bis:ElementUniqueAspect`

**修饰符:** Abstract

---

#### BendingBehaviorAspect

**显示标签:** Bending Behavior Aspect

**描述:** 为 IStructuralSurface 在承受横向荷载时分配分析行为。

**基类:** `SurfaceMemberBehaviorAspect`

**属性:**

| 属性名 | 类型 | 描述 |
|--------|------|------|
| BendingBehaviorValue | BendingBehaviorValue | 提供行为值 |

**修饰符:** Sealed

---

#### LoadResistanceBehaviorAspect

**显示标签:** Load Resistance Behavior Aspect

**描述:** 构件荷载抵抗。

**基类:** `MemberBehaviorAspect`

**属性:**

| 属性名 | 类型 | 描述 |
|--------|------|------|
| LoadResistance | LoadResistance | 荷载抵抗值 |

**修饰符:** Sealed

---

#### CamberBehaviorAspect

**显示标签:** Camber Behavior Aspect

**描述:** 为 CurveMember 提供起拱行为。

**基类:** `CurveMemberBehaviorAspect`

**属性:**

| 属性名 | 类型 | 描述 | 数量类型 |
|--------|------|------|----------|
| CamberValue | double | 起拱值 | AECU:LENGTH_SHORT |

**修饰符:** Sealed

---

#### AxialBehaviorAspect

**显示标签:** Axial Behavior Aspect

**描述:** 将构件定义为具有特定的轴向结构行为。

**基类:** `CurveMemberBehaviorAspect`

**属性:**

| 属性名 | 类型 | 描述 |
|--------|------|------|
| Type | AxialBehavior | 指定轴向行为类型 |

**修饰符:** Sealed

---

### 释放方面类 (Release Aspect Classes)

#### ReleaseAspect (抽象)

**显示标签:** Release Aspect

**描述:** 构件的释放。

**基类:** `bis:ElementMultiAspect`

**修饰符:** Abstract

---

#### VertexReleaseAspect (抽象)

**显示标签:** Vertex Release Aspect

**描述:** 构件的顶点释放。

**基类:** `ReleaseAspect`

**导航属性:**

| 属性名 | 关系 | 描述 |
|--------|------|------|
| Vertex | VertexReleaseAspectRefersToVertex | Vertex |

**修饰符:** Abstract

---

#### LogicalVertexReleaseAspect

**显示标签:** Logical Vertex Release Aspect

**描述:** 构件的顶点释放。

**基类:** `VertexReleaseAspect`

**属性:**

| 属性名 | 类型 | 描述 |
|--------|------|------|
| TranslationalRAxis | ReleaseType | 平移 R 轴的释放 |
| TranslationalSAxis | ReleaseType | 平移 S 轴的释放 |
| TranslationalTAxis | ReleaseType | 平移 T 轴的释放 |
| RotationalRAxis | ReleaseType | 旋转 R 轴的释放 |
| RotationalSAxis | ReleaseType | 旋转 S 轴的释放 |
| RotationalTAxis | ReleaseType | 旋转 T 轴的释放 |

**修饰符:** Sealed

---

### 支承行为类 (Support Behavior Classes)

#### SupportBehavior (抽象)

**显示标签:** Support Behavior

**描述:** 定义支承的固定行为。

**基类:** `bis:DefinitionElement`

**修饰符:** Abstract

---

#### PointSupportBehavior

**显示标签:** Point Support Behavior

**描述:** 定义点支承的固定行为。

**基类:** `SupportBehavior`

**导航属性:**

| 属性名 | 描述 |
|--------|------|
| TranslationalRAxis | R 轴平移固定行为 |
| TranslationalSAxis | S 轴平移固定行为 |
| TranslationalTAxis | T 轴平移固定行为 |
| RotationalRAxis | R 轴旋转固定行为 |
| RotationalSAxis | S 轴旋转固定行为 |
| RotationalTAxis | T 轴旋转固定行为 |

**修饰符:** Sealed

---

#### CurveSupportBehavior

**显示标签:** Curve Support Behavior

**描述:** 定义曲线支承的固定行为。

**基类:** `SupportBehavior`

**修饰符:** Sealed

---

#### SurfaceSupportBehavior

**显示标签:** Surface Support Behavior

**描述:** 定义表面支承的行为。

**基类:** `SupportBehavior`

**修饰符:** Sealed

---

### 类型定义类 (Type Definition Classes)

#### CurveMemberType (抽象)

**显示标签:** Curve Member Type

**描述:** 分组曲线构件的类型。

**基类:** `anlyt:AnalyticalType`

**修饰符:** Abstract

---

#### MaterialProfileType

**显示标签:** Material Profile Type

**描述:** 共享材料和 Profile 的曲线构件类型。

**基类:** `SingleCurveMemberType`

**导航属性:**

| 属性名 | 关系 | 描述 |
|--------|------|------|
| MaterialProfile | MaterialProfileTypeHasMaterialProfile | Material Profile |

**修饰符:** Sealed

---

#### MaterialProfileDefinition (抽象)

**显示标签:** Material Profile Definition

**描述:** 定义配对 Profile 和 PhysicalMaterial 元素的基类。

**基类:** `bis:DefinitionElement`

**属性:**

| 属性名 | 类型 | 描述 |
|--------|------|------|
| Name | string | 用于识别的 MaterialProfile 名称 |
| Description | string | MaterialProfile 的描述 |
| Category | MaterialProfileCategoryType | MaterialProfile 的角色 |

**导航属性:**

| 属性名 | 关系 | 描述 |
|--------|------|------|
| Material | MaterialProfileRefersToMaterial | 引用的 PhysicalMaterial |

**修饰符:** Abstract

---

#### MaterialProfile

**显示标签:** Material Profile

**描述:** Profile 和 PhysicalMaterial 的单一配对。

**基类:** `MaterialProfileDefinition`

**导航属性:**

| 属性名 | 关系 | 描述 |
|--------|------|------|
| Profile | MaterialProfileRefersToProfile | 引用的 Profile |
| Material | MaterialProfileRefersToMaterial | 引用的 PhysicalMaterial |

**修饰符:** Sealed

---

#### TaperedMaterialProfile

**显示标签:** Tapered Material Profile

**描述:** 定义具有线性变化 Profile 的 CurveMember。

**基类:** `MaterialProfileDefinition`

**导航属性:**

| 属性名 | 关系 | 描述 |
|--------|------|------|
| StartProfile | TaperedMaterialProfileRefersToStartProfile | CurveMember 起点处的 Profile |
| EndProfile | TaperedMaterialProfileRefersToEndProfile | CurveMember 终点处的 Profile |

**修饰符:** Sealed

---

#### SteelJoistType

**显示标签:** Steel Joist Type

**基类:** `CurveMemberType`

**属性:**

| 属性名 | 类型 | 描述 |
|--------|------|------|
| Depth | double | 深度 |

**修饰符:** Sealed

---

#### SurfaceType (抽象)

**显示标签:** Surface Type

**描述:** 为 IStructuralSurface 定义表面类型。

**基类:** `anlyt:AnalyticalType`

**修饰符:** Abstract

---

#### SimpleSurfaceType

**显示标签:** Simple Surface Type

**描述:** 简单表面类型。

**基类:** `SurfaceType`

**属性:**

| 属性名 | 类型 | 描述 | 数量类型 |
|--------|------|------|----------|
| Thickness | double | IStructuralSurfaces 的厚度 | AECU:LENGTH_SHORT |

**导航属性:**

| 属性名 | 关系 | 描述 |
|--------|------|------|
| Material | SimpleSurfaceTypeRefersToMaterial | 所有具有此类型的 IStructuralSurfaces 的材料 |

**修饰符:** Sealed

---

#### SteelDeckType

**显示标签:** Steel Deck Type

**描述:** 钢承板类型。

**基类:** `SurfaceType`

**修饰符:** Sealed

---

#### CompositeDeckType

**显示标签:** Composite Deck Type

**描述:** 组合楼板类型。

**基类:** `SurfaceType`

**属性:**

| 属性名 | 类型 | 描述 |
|--------|------|------|
| Thickness | double | 厚度 |

**修饰符:** Sealed

---

#### TaperedSurfaceType

**显示标签:** Tapered Surface Type

**基类:** `SurfaceType`

**属性:**

| 属性名 | 类型 | 描述 |
|--------|------|------|
| Location1 | Point2d | 位置 1 |
| Location2 | Point2d | 位置 2 |
| Location3 | Point2d | 位置 3 |
| Thickness1 | double | 厚度 1 |
| Thickness2 | double | 厚度 2 |
| Thickness3 | double | 厚度 3 |

**修饰符:** Sealed

---

### 位置定义 Mixin 类

#### IDefinedPoint

**显示标签:** Point Location definition

**描述:** 直接或间接定义 3D 空间中点的元素。

**Mixin 应用于:** `bis:Element`

**修饰符:** Abstract

---

#### IDefinedCurve

**显示标签:** Curve Location definition

**描述:** 直接或间接定义曲线位置和清晰坐标系的元素，其 z 轴沿曲线。元素可能有基点定义；如果没有，所有基点应被认为位于 z 轴上。

**Mixin 应用于:** `bis:Element`

**属性:**

| 属性名 | 类型 | 描述 |
|--------|------|------|
| Orientation | Point3d | 曲线的方向（法向）向量 |

**修饰符:** Abstract

---

#### IDefinedSurface

**显示标签:** Surface Location definition

**描述:** 直接或间接定义表面位置和清晰坐标系的元素，其 x 和 y 轴在表面中。元素可能有顶、底和中心定义；如果没有，顶、底和中心应被认为位于表面上。

**Mixin 应用于:** `bis:Element`

**属性:**

| 属性名 | 类型 | 描述 | 数量类型 |
|--------|------|------|----------|
| SurfaceOrigin | Point3d | 定义局部坐标系起点的表面上的点 | AECU:LENGTH |
| RAxis | Point3d | 定义局部坐标系的第一向量。此向量应来自表面原点处的切平面 | - |

**修饰符:** Abstract

---

#### IStoryAssignable

**显示标签:** IStory Assignable

**描述:** 可分配给 Story 的元素。

**Mixin 应用于:** `StructuralAnalysisElement`

**导航属性:**

| 属性名 | 关系 | 描述 |
|--------|------|------|
| Story | IStoryAssignableRefersToStory | 此元素所在的 Story |

**修饰符:** Abstract

---

#### IStructuralSurface

**显示标签:** Solid Surface

**描述:** 由表面和厚度定义的元素。

**Mixin 应用于:** `StructuralAnalysisElement`

**属性:**

| 属性名 | 类型 | 描述 | 数量类型 |
|--------|------|------|----------|
| PlacementSurface | PlacementSurface | Sheet 定义 IStructuralSurface 的区域位置，高度由厚度（由相关 SurfaceType 提供）定义，该厚度挤出位置区域 | - |
| Offset | double | PlacementSurface 仅提供少数情况来解释位置区域（Sheet）。Offset 为较少见的情况提供更多灵活性 | AECU:LENGTH_SHORT |
| LayoutDirection | Point3d | 用于定义如何放置钢承板 Profile 的方向 | - |

**修饰符:** Abstract

---

### 其他元素类

#### Story

**显示标签:** Story

**描述:** 定义结构中的标高空间，元素可以引用。

**基类:** `StructurePart`

**属性:**

| 属性名 | 类型 | 描述 | 数量类型 |
|--------|------|------|----------|
| Elevation | double | 此楼层的标高 | AECU:LENGTH |

**修饰符:** Sealed

---

#### Structure (已弃用)

**显示标签:** Structure

**描述:** DEPRECATED - 不再创建 Structure 实例。分析元素应直接插入到 StructuralAnalysisPartition 模型中。

**基类:** `StructuralAnalysisElement`, `bis:ISubModeledElement`

**修饰符:** Sealed (Deprecated)

---

## 结构类 (Struct Classes)

### PointForce

**描述:** 点上的力。

| 属性名 | 类型 | 描述 | 数量类型 |
|--------|------|------|----------|
| FX | double | X 轴方向的力 | AECU:FORCE |
| FY | double | Y 轴方向的力 | AECU:FORCE |
| FZ | double | Z 轴方向的力 | AECU:FORCE |
| MX | double | 绕 X 轴的力矩 | AECU:MOMENT |
| MY | double | 绕 Y 轴的力矩 | AECU:MOMENT |
| MZ | double | 绕 Z 轴的力矩 | AECU:MOMENT |

---

### LinearForce

**描述:** 单位长度的力。

| 属性名 | 类型 | 描述 | 数量类型 |
|--------|------|------|----------|
| FX | double | X 轴方向单位长度的力 | AECU:LINEAR_FORCE |
| FY | double | Y 轴方向单位长度的力 | AECU:LINEAR_FORCE |
| FZ | double | Z 轴方向单位长度的力 | AECU:LINEAR_FORCE |
| MX | double | 绕 X 轴单位长度的力矩 | AECU:LINEAR_MOMENT |
| MY | double | 绕 Y 轴单位长度的力矩 | AECU:LINEAR_MOMENT |
| MZ | double | 绕 Z 轴单位长度的力矩 | AECU:LINEAR_MOMENT |

---

### AreaForce

**描述:** 单位面积的力。

| 属性名 | 类型 | 描述 | 数量类型 |
|--------|------|------|----------|
| FX | double | X 轴方向单位面积的力 | AECU:AREA_FORCE |
| FY | double | Y 轴方向单位面积的力 | AECU:AREA_FORCE |
| FZ | double | Z 轴方向单位面积的力 | AECU:AREA_FORCE |
| MX | double | 绕 X 轴单位面积的力矩 | AECU:AREA_MOMENT |
| MY | double | 绕 Y 轴单位面积的力矩 | AECU:AREA_MOMENT |
| MZ | double | 绕 Z 轴单位面积的力矩 | AECU:AREA_MOMENT |

---

## 荷载值方面类 (Load Value Aspect Classes)

### LoadValueAspect (抽象)

**显示标签:** Load Value Aspect

**描述:** 必须应用于荷载的值。

**基类:** `bis:ElementUniqueAspect`

**修饰符:** Abstract

---

### PointLoadValueAspect (抽象)

**显示标签:** Point Load Value Aspect

**描述:** 定义点荷载属性的基类。

**基类:** `LoadValueAspect`

**修饰符:** Abstract

---

### ForcePointLoadValueAspect

**显示标签:** Point Force Value Aspect

**描述:** 定义点荷载的力。

**基类:** `PointLoadValueAspect`

**结构属性:**

| 属性名 | 类型 | 描述 |
|--------|------|------|
| Force | PointForce | 力值 |

**修饰符:** Sealed

---

### CurveLoadValueAspect (抽象)

**显示标签:** Curve Load Value Aspect

**描述:** 可分配给 CurveLoad 的 LoadValueAspect。

**基类:** `LoadValueAspect`

**修饰符:** Abstract

---

### UniformForceCurveLoadValueAspect

**显示标签:** Uniform Curve Force Value Aspect

**描述:** 沿曲线长度具有恒定力的 CurveLoadValueAspect。

**基类:** `UniformCurveLoadValueAspect`

**结构属性:**

| 属性名 | 类型 | 描述 |
|--------|------|------|
| Force | LinearForce | 线性力值 |

**修饰符:** Sealed

---

### VaryingForceCurveLoadValueAspect

**显示标签:** Varying Curve Force Value Aspect

**描述:** 力的 VaryingCurveLoadValueAspect。

**基类:** `VaryingCurveLoadValueAspect`

**结构数组属性:**

| 属性名 | 类型 | 描述 |
|--------|------|------|
| Forces | LinearForce[] | 力值 |

**修饰符:** Sealed

---

### SurfaceLoadValueAspect (抽象)

**显示标签:** Surface Load Value Aspect

**描述:** 可分配给 SurfaceLoad 的 LoadValueAspect。

**基类:** `LoadValueAspect`

**修饰符:** Abstract

---

### UniformForceSurfaceLoadValueAspect

**显示标签:** Uniform Surface Force Value Aspect

**描述:** 力的 UniformSurfaceLoadValueAspect。

**基类:** `UniformSurfaceLoadValueAspect`

**结构属性:**

| 属性名 | 类型 | 描述 |
|--------|------|------|
| Force | AreaForce | 面积力值 |

**修饰符:** Sealed

---

### VaryingForceSurfaceLoadValueAspect

**显示标签:** Curve Force Value Aspect

**描述:** 力的 VaryingSurfaceLoadValueAspect。

**基类:** `VaryingSurfaceLoadValueAspect`

**结构数组属性:**

| 属性名 | 类型 | 描述 |
|--------|------|------|
| Forces | AreaForce[] | 力值 |

**修饰符:** Sealed

---

### 相对位置方面类 (Relative Location Aspect Classes)

#### RelativeLocationAspect (抽象)

**显示标签:** Relative Location Aspect

**描述:** 定义相对位置的抽象类。

**基类:** `bis:ElementUniqueAspect`

**修饰符:** Abstract

---

#### RelativePointLocationAspect (抽象)

**显示标签:** Relative Point Location Aspect

**描述:** 相对于其他元素的点。

**基类:** `RelativeLocationAspect`

**修饰符:** Abstract

---

#### PointRelativeToPointAspect

**显示标签:** Point Relative to Point Aspect

**描述:** 相对于点的点。

**基类:** `RelativePointLocationAspect`

**修饰符:** Sealed

---

#### PointRelativeToCurveAspect

**显示标签:** Point Relative to Curve Location Aspect

**描述:** 相对于曲线的点。

**基类:** `RelativePointLocationAspect`

**属性:**

| 属性名 | 类型 | 描述 | 数量类型 |
|--------|------|------|----------|
| Location | double | 曲线上定义点的分数参数（0.0 - 1.0） | - |
| Offset | Point2d | 由位置曲线法向和副法向定义的平面内的偏移 | AECU:LENGTH_SHORT |
| PlacementPoint | PlacementPoint | 宿主上荷载所在的放置点 | - |

**修饰符:** Sealed

---

#### PointRelativeToSurfaceAspect

**显示标签:** Point Relative to Surface Location Aspect

**描述:** 相对于表面的点。

**基类:** `RelativePointLocationAspect`

**属性:**

| 属性名 | 类型 | 描述 | 数量类型 |
|--------|------|------|----------|
| Location | Point2d | 位置由宿主 r 和 s 轴定义的 2D 坐标系定义 | - |
| Offset | double | 偏移 | AECU:LENGTH_SHORT |
| PlacementSurface | PlacementSurface | 定义此荷载在表面宿主上的对齐 | - |

**修饰符:** Sealed

---

#### RelativeCurveLocationAspect (抽象)

**显示标签:** Relative Curve Location Aspect

**描述:** 相对于其他元素的曲线。

**基类:** `RelativeLocationAspect`

**修饰符:** Abstract

---

#### CurveRelativeToCurveAspect

**显示标签:** Curve Relative to Curve Aspect

**描述:** 定义宿主曲线中曲线荷载的位置。

**基类:** `RelativeCurveLocationAspect`

**属性:**

| 属性名 | 类型 | 描述 | 数量类型 |
|--------|------|------|----------|
| Start | double | 宿主曲线上的分数参数（'0.0' - 曲线起点） | - |
| End | double | 宿主曲线上的分数参数（'0.0' - 曲线起点，1.0 - 终点） | - |
| Offset | Point2d | 由宿主曲线法向和副法向定义的平面内的偏移 | AECU:LENGTH_SHORT |
| PlacementPoint | PlacementPoint | 与宿主曲线关联的剖面上的放置点 | - |

**修饰符:** Sealed

---

#### CurveRelativeToSurfaceAspect

**显示标签:** Curve Relative to Surface Location Aspect

**描述:** 相对于表面的曲线。

**基类:** `RelativeCurveLocationAspect`

**属性:**

| 属性名 | 类型 | 描述 | 数量类型 |
|--------|------|------|----------|
| Location | Bentley.Geometry.Common.IGeometry | 描述宿主表面上荷载位置的曲线 | - |
| Offset | double | 沿法向距表面的距离 | AECU:LENGTH_SHORT |
| PlacementSurface | PlacementSurface | 施加荷载的放置表面 | - |

**修饰符:** Sealed

---

#### RelativeSurfaceLocationAspect (抽象)

**显示标签:** Relative Surface Location Aspect

**描述:** 相对于其他元素的表面。

**基类:** `RelativeLocationAspect`

**修饰符:** Abstract

---

#### SurfaceRelativeToSurfaceAspect

**显示标签:** Surface Relative to Surface Location Aspect

**描述:** 相对于表面的表面。

**基类:** `RelativeSurfaceLocationAspect`

**属性:**

| 属性名 | 类型 | 描述 | 数量类型 |
|--------|------|------|----------|
| Location | Bentley.Geometry.Common.IGeometry | 位置 | - |
| Offset | double | 偏移 | AECU:LENGTH_SHORT |
| PlacementSurface | PlacementSurface | 施加荷载的放置表面 | - |

**修饰符:** Sealed

---

## Aspect 类

### OrientedEdgeAspect

**显示标签:** Oriented Edge Aspect

**描述:** 此 Aspect 存储 Path 的 Edge（及相关数据）。

**基类:** `bis:ElementMultiAspect`

**属性:**

| 属性名 | 类型 | 描述 |
|--------|------|------|
| Index | int | Path 中 Edge 顺序的零基索引 |
| IsForwardDirection | boolean | 显示方向是否与边缘方向匹配 |

**修饰符:** Sealed

---

### OrientedFaceAspect

**显示标签:** Oriented Face Aspect

**描述:** 此 Aspect 存储 FaceSet 的 Face（及相关数据）。

**基类:** `bis:ElementMultiAspect`

**属性:**

| 属性名 | 类型 | 描述 |
|--------|------|------|
| IsForwardDirection | boolean | 显示方向是否与 Face 方向匹配 |

**修饰符:** Sealed

---

---

## 主要关系类 (Key Relationship Classes)

### StructuralAnalysisModelBreaksDownPartition

**描述:** 将 StructuralAnalysisModel 与其子模型的 StructuralAnalysisPartition 关联。

| 源 | 目标 | 强度 |
|---|------|------|
| StructuralAnalysisModel (0..1) | StructuralAnalysisPartition (0..1) | embedding |

---

### EdgeHasStartVertex / EdgeHasEndVertex

**描述:** Edge 与其起点/终点 Vertex 的关系。

| 源 | 目标 | 强度 |
|---|------|------|
| Edge (0..*) | Vertex (1..1) | referencing |

---

### FaceOwnsBoundaryLoop

**描述:** Face 拥有描述其外边界的 Loop。

| 源 | 目标 | 强度 |
|---|------|------|
| Face (0..1) | Loop (1..1) | embedding |

---

### CurveMemberIsOfCurveMemberType

**描述:** CurveMember 与其类型的关系。

| 源 | 目标 | 强度 |
|---|------|------|
| CurveMember (0..*) | CurveMemberType (1..1) | referencing |

---

### IStructuralSurfaceRefersToSurfaceType

**描述:** IStructuralSurface 与其 SurfaceType 的关系。

| 源 | 目标 | 强度 |
|---|------|------|
| IStructuralSurface (0..*) | SurfaceType (1..1) | referencing |

---

### LoadContainerOwnsLoads

**描述:** LoadContainer 拥有其子荷载。

| 源 | 目标 | 强度 |
|---|------|------|
| LoadContainer (1..1) | Load (0..*) | embedding |

---

### SupportRepresentsMembers

**描述:** 定义由支承表示的构件。

| 源 | 目标 | 强度 |
|---|------|------|
| Support (0..*) | Member (0..*) | referencing |

---

## 已弃用的类

以下类已被弃用，不应在新实现中使用：

- **Structure** - 不再创建实例。分析元素应直接插入到 StructuralAnalysisPartition 模型中。
- **LoadCombination** - 应使用 LoadCombinationInformation 替代。
- **FactoredLoadConditionAspect** 及其子类 - 应使用 LoadCombinationInformation 和 FactoredLoadCondition 替代。

---

## 参考来源

- 本地 Schema 文件: `c:\dev\iModelSDK\source\bis-schemas\Domains\3-DisciplineOther\StructuralAnalysis\StructuralAnalysis.ecschema.xml`
- iTwin.js 文档: https://www.itwinjs.org/bis/
