# Formats Schema

**Alias:** f

**Version:** 1.0.0

标准 Format 定义集合

## 目录

- Formats
  - AmerFI
  - AmerI
  - AngleDMS
  - DefaultReal
  - DefaultRealU
  - DefaultRealUNS
  - Fractional
  - HMS
  - StationZ_1000_3
  - StationZ_100_2

### AmerFI (FeetInches) Format

**类型：** Fractional

**精度：** 8

**显示符号选项：** OnlyNegative

**格式特征**

- KeepSingleZero
- KeepDecimalPoint
- ShowUnitLabel

**分隔符：** None

### AmerI (Inches) Format

**类型：** Fractional

**精度：** 8

**显示符号选项：** OnlyNegative

**格式特征**

- KeepSingleZero
- ShowUnitLabel

**分隔符：** None

### AngleDMS (DegreesMinutesSeconds) Format

**类型：** Decimal

**精度：** 4

**显示符号选项：** OnlyNegative

**格式特征**

- KeepSingleZero
- KeepDecimalPoint
- ShowUnitLabel

**分隔符：** None

### DefaultReal (real) Format

**类型：** Decimal

**精度：** 6

**显示符号选项：** OnlyNegative

**格式特征**

- KeepSingleZero
- KeepDecimalPoint

**分隔符：** (Space)

### DefaultRealU (realu) Format

**类型：** Decimal

**精度：** 6

**显示符号选项：** OnlyNegative

**格式特征**

- KeepSingleZero
- KeepDecimalPoint
- ShowUnitLabel

**分隔符：** (Space)

### DefaultRealUNS Format

**类型：** Decimal

**精度：** 6

**显示符号选项：** OnlyNegative

**格式特征**

- KeepSingleZero
- KeepDecimalPoint
- ShowUnitLabel

**分隔符：** None

### Fractional (fract) Format

**类型：** Fractional

**精度：** 64

**显示符号选项：** OnlyNegative

**格式特征**

- KeepSingleZero
- KeepDecimalPoint

**分隔符：** (Space)

### HMS (HoursMinutesSeconds) Format

**类型：** Decimal

**精度：** 2

**显示符号选项：** OnlyNegative

**格式特征**

- KeepSingleZero
- KeepDecimalPoint
- ShowUnitLabel

**分隔符：** (Space)

### StationZ_1000_3 Format

**类型：** Station

**站点偏移大小：** 3

**精度：** 2

**显示符号选项：** OnlyNegative

**格式特征**

- TrailZeroes
- KeepSingleZero
- KeepDecimalPoint

**分隔符：** (Space)

### StationZ_100_2 Format

**类型：** Station

**站点偏移大小：** 2

**精度：** 2

**显示符号选项：** OnlyNegative

**格式特征**

- TrailZeroes
- KeepSingleZero
- KeepDecimalPoint

**分隔符：** (Space)

---

*原文链接：https://www.itwinjs.org/bis/domains/formats.ecschema/*

*最后更新：2025年6月11日*
