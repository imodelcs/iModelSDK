# BIS Schema Units (BIS Schema 单位)

> 原文: [Physical Units in BIS](https://www.itwinjs.org/bis/guide/other-topics/units/)
>
> 最后更新: 2025年6月11日

BIS 和 iModels 始终使用一套明确定义的物理单位系统。

## 物理单位必须是 SI 基本单位或 SI 导出单位

BIS schema 中的所有物理属性值（包括几何数据）必须是：

- [SI 基本单位](https://en.wikipedia.org/wiki/SI_base_unit) (m, kg, s, A, K, mol, cd)
- [SI 导出单位](https://en.wikipedia.org/wiki/SI_derived_unit)（不带前缀）(Hz, rad, sr, N, Pa, J, W, C, V, F, Ω, S, Wb, T, H, C, lm, lx, Bq, Gy, Sv, kat)

因此，可以对物理值进行数学运算而无需考虑单位：

```ts
Mass = Density * Volume; // 不需要单位转换
```

> 注意：在 iModels 中，所有坐标数据都以米为单位存储。

> 注意：带有前缀的单位（如 kilometer、millimeter、kilowatt 和 millivolt）是不允许的。

## 角度单位

角度单位是**弧度**（radians），因为这是角度的 SI 导出单位。类似地，立体角的单位是**球面度**（steradians）。

> 这可能看起来有些不便，因为 "90" 比 "1.5707963267948966192313216916398" 更容易识别。但是请注意，存储单位不会直接展示给用户。

使用弧度是为了保持数学计算的一致性。

例如：

```ts
(光通量，单位：流明) = (发光强度，单位：坎德拉) * (立体角，单位：球面度)

(能量，单位：焦耳) = (扭矩，单位：牛顿-米) * (旋转角度，单位：弧度)
```

## Roll、Pitch 和 Yaw 的例外

`Roll`、`Pitch` 和 `Yaw`（在 `GeometricElement3d`、`ViewDefinition3d`、`AuxCoordinateSystem3d` 中）是特殊处理的。它们以**度**定义，并在 EC schema 中声明为无单位。

类似地，以下属性也以度定义并在 EC schema 中声明为无单位：

- `Angle` in AuxCoordSystem2d
- `Rotation` in GeometricElement2d
- `LensAngle` in ViewDefinition3d
- `RotationAngle` in ViewDefinition2d

## SI 单位不适用于名称和文本

SI 单位要求仅适用于数值物理属性和几何属性；不适用于文本属性。"90-Degree Elbow"（90度弯头）是一个可接受的文本值。

---

| 下一篇: [BIS Schema KindOfQuantities](./bis-schema-kindofquantities.md)
|:---
