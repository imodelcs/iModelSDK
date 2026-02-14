# Quantity Takeoffs: 指南

> 原文: [Quantity takeoffs: Guidelines - iTwin.js](https://www.itwinjs.org/v4/bis/guide/physical-perspective/qto-guidelines/)
>
> 翻译日期: 2026-02-13

## 介绍 (Introduction)

Quantity takeoffs 和 material estimating 是 BIS 的重要用例。它们的计算可应用于众多应用程序，如 Carbon Footprint（碳足迹）、Costing（成本估算）和 Construction scheduling（施工进度计划）。Physical Materials 解释了 BIS 中的标准模式，以便理解任何 Physical Element 由何种 Physical Material 构成。实现 material estimating 的下一步涉及解释实际的工程量值。

## 通用方法 (General approach)

预期每个 Discipline-Physical schema 都应使用适合该领域的名称和适用的 Kind of Quantity 定义，将相关工程量作为其类的一等属性（first-class properties）包含在内。

## 回退策略 (Fallback strategies)

由于并非 Discipline-Physical 层的所有 BIS schema 都具有与工程量相关的属性，因此需要一种回退方法。此方法主要针对需要为尚不存在或可能尚未具有等效属性的 BIS 域写入工程量相关数据的 iModel Connectors 和 iModel-writers。

第一种回退策略是使用 Quantity Takeoffs Aspects schema 中的 aspect 类。它包含许多常用的与工程量相关的属性，可以作为 unique-aspects 附加到任何 Element 上。

作为最后手段，如果标准域或 QTO schema 中没有可用的属性，iModel Connector 或 iModel-writer 可以将它们引入自己的 Application-level schema 中。此策略应被视为临时的，并应向 BIS Working Group 请求添加那些缺失的与工程量相关的属性。

## 数据对齐过渡期间的数据重复 (Data duplication during transitions to data-alignment)

如前所述，上述描述的用于存储 Discipline-Physical schema 中缺失的工程量相关属性的回退方法被视为临时解决方案。一旦这些缺失的属性被添加到适当的域中，在技术上对这些概念进行对齐后，iModel Connectors 和 iModel writers 应当更新以指向它们。

然而，仍然预期 iModel Connectors 和 iModel writers 继续以其使用的回退方法写入相同的数据，以防止对其输出的任何现有消费者造成立即中断。因此，他们应规划从回退策略到对齐方法的过渡，通过提供一段特定的时间来重复数据。为特定 iModel Connector 或 iModel writer 组件决定的过渡期的详细信息应相应地传达给其消费者。

## Quantity Takeoff 属性的可发现性 (Discoverability of Quantity Takeoff properties)

与工程量相关的属性定义包含 Kind of Quantity 元数据的预期使其能够基于其持久化单位（persistence unit）进行基本发现。

例如，一个有兴趣发现捕获有关 Element 的体积量（Volumetric quantity）的属性的应用程序，可以通过收集其持久化单位为立方米（cubic metres）的任何属性来实现。

---

| 下一篇: Functional Models and Elements
|:---|
