# Units (Units) Schema

**Alias:** u

**Version:** 1.0.9

系统的标准 Unit 定义集合

## 概述

Units Schema 定义了 BIS 系统中使用的标准单位集合，包括：

- **Units** - 各种物理量的单位定义
- **Inverted Units** - 反转单位
- **Constants** - 常量定义
- **Phenomena** - 现象（物理量）定义
- **Unit Systems** - 单位系统

## 主要单位类别

### 长度单位 (Length)
- `M` (m) - 米，SI 基本单位
- `CM` (cm) - 厘米
- `MM` (mm) - 毫米
- `KM` (km) - 千米
- `FT` (ft) - 英尺
- `IN` (in) - 英寸
- `MILE` (mi) - 英里
- `YRD` (yd) - 码
- `UM` (µm) - 微米

### 面积单位 (Area)
- `SQ_M` (m²) - 平方米
- `SQ_CM` (cm²) - 平方厘米
- `SQ_MM` (mm²) - 平方毫米
- `SQ_KM` (km²) - 平方千米
- `SQ_FT` (ft²) - 平方英尺
- `SQ_IN` (in²) - 平方英寸
- `HECTARE` (ha) - 公顷
- `ACRE` (acres) - 英亩

### 体积单位 (Volume)
- `CUB_M` (m³) - 立方米
- `CUB_CM` (cm³) - 立方厘米
- `CUB_FT` (ft³) - 立方英尺
- `LITRE` (L) - 升
- `GALLON` (gal) - 加仑
- `GALLON_IMPERIAL` (gal (imp)) - 英制加仑

### 质量单位 (Mass)
- `KG` (kg) - 千克，SI 基本单位
- `G` (g) - 克
- `MG` (mg) - 毫克
- `TONNE` (tonne) - 公吨
- `LBM` (lb) - 磅质量
- `OZM` (oz) - 盎司质量

### 时间单位 (Time)
- `S` (s) - 秒，SI 基本单位
- `MS` (ms) - 毫秒
- `MIN` (min) - 分钟
- `HR` (h) - 小时
- `DAY` (days) - 天
- `WEEK` (week) - 周
- `YR` (years) - 年

### 力单位 (Force)
- `N` - 牛顿，SI 单位
- `KN` (kN) - 千牛顿
- `MN` (MN) - 兆牛顿
- `LBF` (lbf) - 磅力
- `KGF` (kgf) - 千克力

### 压力单位 (Pressure)
- `PA` (N/m²) - 帕斯卡，SI 单位
- `KPA` (kPa) - 千帕
- `MPA` (MPa) - 兆帕
- `BAR` (bar) - 巴
- `PSI` (lbf/in²) - 磅每平方英寸
- `ATM` (atm) - 标准大气压

### 温度单位 (Temperature)
- `K` - 开尔文，SI 基本单位
- `CELSIUS` (°C) - 摄氏度
- `FAHRENHEIT` (°F) - 华氏度
- `RANKINE` (°R) - 兰氏度

### 速度/加速度单位 (Velocity/Acceleration)
- `M_PER_SEC` (m/s) - 米每秒
- `KM_PER_HR` (km/h) - 千米每小时
- `FT_PER_SEC` (ft/s) - 英尺每秒
- `MPH` (mi/h) - 英里每小时
- `M_PER_SEC_SQ` (m/sec²) - 米每秒平方
- `G` - 重力加速度

### 角度单位 (Angle)
- `RAD` (rad) - 弧度，SI 单位
- `ARC_DEG` (°) - 度
- `ARC_MINUTE` (') - 角分
- `ARC_SECOND` ('') - 角秒
- `REVOLUTION` (r) - 转

### 功/能量单位 (Work/Energy)
- `J` - 焦耳，SI 单位
- `KJ` (kJ) - 千焦
- `BTU` (Btu) - 英热单位
- `KWH` (kW·h) - 千瓦时

### 功率单位 (Power)
- `W` - 瓦特，SI 单位
- `KW` (kW) - 千瓦
- `MW` (MW) - 兆瓦
- `HP` (hp) - 马力

### 电流单位 (Current)
- `A` - 安培，SI 基本单位
- `KA` (KA) - 千安
- `MA` (mA) - 毫安

### 电压单位 (Electric Potential)
- `VOLT` (V) - 伏特，SI 单位
- `KV` (KV) - 千伏
- `MV` (MV) - 兆伏

### 频率单位 (Frequency)
- `HZ` (Hz) - 赫兹，SI 单位
- `KHZ` (KHz) - 千赫
- `MHZ` (MHz) - 兆赫

### 流量单位 (Volumetric Flow)
- `CUB_M_PER_SEC` (m³/s) - 立方米每秒
- `LITRE_PER_SEC` (L/s) - 升每秒
- `GALLON_PER_MIN` (gal/min) - 加仑每分钟
- `CUB_FT_PER_SEC` (ft³/s) - 立方英尺每秒

### 密度单位 (Density)
- `KG_PER_CUB_M` (kg/m³) - 千克每立方米
- `G_PER_CUB_CM` (g/cm³) - 克每立方厘米
- `LBM_PER_CUB_FT` (lb/ft³) - 磅每立方英尺

### 力矩单位 (Torque)
- `N_M` (N·m) - 牛顿米
- `KN_M` (kN·m) - 千牛顿米
- `LBF_FT` (lbf·ft) - 磅力英尺

### 百分比/比率单位
- `PERCENT` (%) - 百分比
- `DECIMAL_PERCENT` - 小数百分比
- `COEFFICIENT` - 无量纲系数

## 常量 (Constants)

以下是 Units Schema 中定义的数学和物理常量：

| 名称 | 描述 |
|------|------|
| `PI` | 圆周率 π |
| `TWO_PI` | 2π |
| `HALF_PI` | π/2 |
| `QUARTER_PI` | π/4 |
| `DEG360` | 360 度 |
| `STD_G` | 标准重力加速度 |

SI 前缀常量：
| 名称 | 值 |
|------|------|
| `ATTO` | 10⁻¹⁸ |
| `FEMTO` | 10⁻¹⁵ |
| `PICO` | 10⁻¹² |
| `NANO` | 10⁻⁹ |
| `MICRO` | 10⁻⁶ |
| `MILLI` | 10⁻³ |
| `CENTI` | 10⁻² |
| `DECI` | 10⁻¹ |
| `DECA` | 10¹ |
| `HECTO` | 10² |
| `KILO` | 10³ |
| `MEGA` | 10⁶ |
| `GIGA` | 10⁹ |
| `TERA` | 10¹² |
| `PETA` | 10¹⁵ |
| `EXA` | 10¹⁸ |
| `ZETTA` | 10²¹ |
| `YOTTA` | 10²⁴ |

## 现象 (Phenomena)

现象定义了物理量的维度：

| 名称 | 描述 |
|------|------|
| `LENGTH` | 长度 |
| `AREA` | 面积 |
| `VOLUME` | 体积 |
| `MASS` | 质量 |
| `TIME` | 时间 |
| `TEMPERATURE` | 温度 |
| `VELOCITY` | 速度 |
| `ACCELERATION` | 加速度 |
| `FORCE` | 力 |
| `PRESSURE` | 压力 |
| `ENERGY_DENSITY` | 能量密度 |
| `WORK` | 功 |
| `POWER` | 功率 |
| `ANGLE` | 角度 |
| `ANGULAR_VELOCITY` | 角速度 |
| `FREQUENCY` | 频率 |
| `CURRENT` | 电流 |
| `ELECTRIC_POTENTIAL` | 电势 |
| `ELECTRIC_CHARGE` | 电荷 |
| `DENSITY` | 密度 |
| `VOLUMETRIC_FLOW` | 体积流量 |
| `TORQUE` | 力矩 |
| `SLOPE` | 坡度 |
| `CURRENCY` | 货币 |
| `PROBABILITY` | 概率 |

## 单位系统 (Unit Systems)

| 名称 | 描述 |
|------|------|
| `SI` | 国际单位制 |
| `METRIC` | 公制 |
| `USCUSTOM` | 美国惯用单位 |
| `USSURVEY` | 美国测量单位 |
| `IMPERIAL` | 英制 |
| `INTERNATIONAL` | 国际 |
| `INDUSTRIAL` | 工业 |
| `MARITIME` | 海事 |
| `CGS` | 厘米-克-秒制 |
| `FINANCE` | 金融 |
| `STATISTICS` | 统计 |
| `CONSTANT` | 常量 |

## 反转单位 (Inverted Units)

反转单位用于表示倒数关系：

| 名称 | 描述 |
|------|------|
| `FT_HORIZONTAL_PER_FT_VERTICAL` | 水平英尺每垂直英尺 |
| `HORIZONTAL_PER_VERTICAL` | 水平每垂直 |
| `M_HORIZONTAL_PER_M_VERTICAL` | 水平米每垂直米 |

## 单位定义格式

单位通过以下属性定义：

- **Definition** - 单位的数学定义表达式
- **Phenomenon** - 单位所属的物理现象
- **Unit System** - 单位所属的单位系统
- **Numerator** - 分子（用于派生单位）
- **Denominator** - 分母（用于派生单位）
- **Offset** - 偏移量（用于温度等单位）

### 示例

#### 摄氏度定义
```
Definition: K
Phenomenon: TEMPERATURE
Unit System: METRIC
Offset: 273.15
```

#### 华氏度定义
```
Definition: CELSIUS
Phenomenon: TEMPERATURE
Unit System: USCUSTOM
Numerator: 5
Denominator: 9
Offset: -32
```

#### 度定义
```
Definition: [PI]*RAD
Phenomenon: ANGLE
Unit System: METRIC
Numerator: 1
Denominator: 180
```

---

*原文链接：https://www.itwinjs.org/bis/domains/units.ecschema/*

*最后更新：2025年6月11日*
