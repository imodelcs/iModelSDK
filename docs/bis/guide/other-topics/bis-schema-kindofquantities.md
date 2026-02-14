# BIS Schema KindOfQuantities (BIS Schema 数量类型)

> 原文: [KindOfQuantities in BIS](https://www.itwinjs.org/bis/guide/other-topics/kindofquantities/)
>
> 最后更新: 2025年6月11日

在 BIS schema 中选择 [KindOfQuantity](../../ec/kindofquantity.md) 需要反映其所代表的属性分组和默认显示格式的预期协调级别。一般来说，需要记住三个协调级别：

1. 在整个 BIS 生态系统中通用
2. 在特定 schema 子集中通用
3. 特定于 iModel Connector 或应用程序

## 整个 BIS 生态系统中通用的 KindOfQuantity

在 [AecUnits](../../domains/aecunits.ecschema.md) schema 中定义的 KindOfQuantity 应被那些其分组和默认显示格式旨在在整个 BIS 生态系统中（不论涉及哪个学科）保持协调的属性所引用。

例如，`aecu:LENGTH` KindOfQuantity 可以被任何层级 schema 中的属性引用。如果在应用程序中更改了 `aecu:LENGTH` 的显示格式，新的显示格式将应用于所有学科中引用它的属性值。

## 在 schema 子集中通用的 KindOfQuantity

当属性分组和默认格式的协调仅期望在 schema 子集的属性之间进行时，建议引入一个单独的 schema 来定义它们。

[RoadRailUnits](../../domains/roadrailunits.ecschema.md) schema 是此类协调的一个示例。例如，它定义了一个 `rru:LENGTH` KindOfQuantity，被道路和铁路 schema 中的属性引用，这些属性的显示格式预期会一起变化，并且与公共 `aecu:LENGTH` KindOfQuantity 中指定的设置不同。也就是说，`aecu:LENGTH` 列出了四种可能的显示单位：米、毫米、英尺-英寸和纯英尺，但道路和铁路领域通常使用的显示单位列表是不同的——米、英尺和测量英尺。

## 特定于 iModel Connector 或应用程序

当 iModel Connector 或应用程序需要现有底层 schema 未涵盖的特殊 `KindOfQuantity` 时，此类特殊 `KindOfQuantity` 应在 Connector 或应用程序特定的 schema 中定义。仍然建议将这些特殊 KindOfQuantity 引入单独的 schema，以便更好地控制 schema 升级的范围。这样，在单独的 KindOfQuantity 导向 schema 中捕获的显示格式设置可以被调整，而无需强制更改实际的域 schema。

---

| 下一篇: [BIS Schema Validation](./bis-schema-validation.md)
|:---
