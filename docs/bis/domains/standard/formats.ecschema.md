# Formats Schema

**别名 (Alias):** f

**版本 (Version):** 1.0.0

Format 定义的标准集合

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

---

### __AmerFI__ (FeetInches) Format

**类型 (Type):** Fractional（分数）

**精度 (Precision):** 8

**符号显示选项 (Show Sign Option):** OnlyNegative（仅负数）

**Format Traits（格式特征）**

- KeepSingleZero - 保留单个零
- KeepDecimalPoint - 保留小数点
- ShowUnitLabel - 显示单位标签

**分隔符 (Separator):** None（无）

---

### __AmerI__ (Inches) Format

**类型 (Type):** Fractional（分数）

**精度 (Precision):** 8

**符号显示选项 (Show Sign Option):** OnlyNegative（仅负数）

**Format Traits（格式特征）**

- KeepSingleZero - 保留单个零
- ShowUnitLabel - 显示单位标签

**分隔符 (Separator):** None（无）

---

### __AngleDMS__ (DegreesMinutesSeconds) Format

**类型 (Type):** Decimal（十进制）

**精度 (Precision):** 4

**符号显示选项 (Show Sign Option):** OnlyNegative（仅负数）

**Format Traits（格式特征）**

- KeepSingleZero - 保留单个零
- KeepDecimalPoint - 保留小数点
- ShowUnitLabel - 显示单位标签

**分隔符 (Separator):** None（无）

---

### __DefaultReal__ (real) Format

**类型 (Type):** Decimal（十进制）

**精度 (Precision):** 6

**符号显示选项 (Show Sign Option):** OnlyNegative（仅负数）

**Format Traits（格式特征）**

- KeepSingleZero - 保留单个零
- KeepDecimalPoint - 保留小数点

**分隔符 (Separator):** Space（空格）

---

### __DefaultRealU__ (realu) Format

**类型 (Type):** Decimal（十进制）

**精度 (Precision):** 6

**符号显示选项 (Show Sign Option):** OnlyNegative（仅负数）

**Format Traits（格式特征）**

- KeepSingleZero - 保留单个零
- KeepDecimalPoint - 保留小数点
- ShowUnitLabel - 显示单位标签

**分隔符 (Separator):** Space（空格）

---

### __DefaultRealUNS__ Format

**类型 (Type):** Decimal（十进制）

**精度 (Precision):** 6

**符号显示选项 (Show Sign Option):** OnlyNegative（仅负数）

**Format Traits（格式特征）**

- KeepSingleZero - 保留单个零
- KeepDecimalPoint - 保留小数点
- ShowUnitLabel - 显示单位标签

**分隔符 (Separator):** None（无）

---

### __Fractional__ (fract) Format

**类型 (Type):** Fractional（分数）

**精度 (Precision):** 64

**符号显示选项 (Show Sign Option):** OnlyNegative（仅负数）

**Format Traits（格式特征）**

- KeepSingleZero - 保留单个零
- KeepDecimalPoint - 保留小数点

**分隔符 (Separator):** Space（空格）

---

### __HMS__ (HoursMinutesSeconds) Format

**类型 (Type):** Decimal（十进制）

**精度 (Precision):** 2

**符号显示选项 (Show Sign Option):** OnlyNegative（仅负数）

**Format Traits（格式特征）**

- KeepSingleZero - 保留单个零
- KeepDecimalPoint - 保留小数点
- ShowUnitLabel - 显示单位标签

**分隔符 (Separator):** Space（空格）

---

### __StationZ_1000_3__ Format

**类型 (Type):** Station（桩号）

**Station Offset Size（桩号偏移大小）:** 3

**精度 (Precision):** 2

**符号显示选项 (Show Sign Option):** OnlyNegative（仅负数）

**Format Traits（格式特征）**

- TrailZeroes - 尾随零
- KeepSingleZero - 保留单个零
- KeepDecimalPoint - 保留小数点

**分隔符 (Separator):** Space（空格）

---

### __StationZ_100_2__ Format

**类型 (Type):** Station（桩号）

**Station Offset Size（桩号偏移大小）:** 2

**精度 (Precision):** 2

**符号显示选项 (Show Sign Option):** OnlyNegative（仅负数）

**Format Traits（格式特征）**

- TrailZeroes - 尾随零
- KeepSingleZero - 保留单个零
- KeepDecimalPoint - 保留小数点

**分隔符 (Separator):** Space（空格）

---

## 术语说明

| 英文术语 | 中文说明 |
|---------|---------|
| Fractional | 分数格式，用于表示分数值（如 1/2, 3/4） |
| Decimal | 十进制格式，用于表示小数值 |
| Station | 桩号格式，常用于道路、铁路等线性工程的里程标记 |
| Precision | 精度，表示小数位数或分数的分母 |
| Show Sign Option | 符号显示选项，控制正负号的显示方式 |
| OnlyNegative | 仅在负数时显示符号 |
| Format Traits | 格式特征，定义数值显示的具体行为 |
| KeepSingleZero | 保留单个零（如 0.5 而非 .5） |
| KeepDecimalPoint | 保留小数点（如 1. 而非 1） |
| ShowUnitLabel | 显示单位标签 |
| TrailZeroes | 尾随零，在数值后补零以达到指定精度 |
| Separator | 分隔符，用于分隔数值和单位 |

---

*最后更新: 2025年6月11日*

*原文链接: https://www.itwinjs.org/bis/domains/formats.ecschema/*
