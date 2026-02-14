# Federated Digital Twins（联邦数字孪生）

**原文链接**: [Federated Digital Twins for Infrastructure Engineering](https://www.itwinjs.org/bis/guide/intro/federated-digital-twins/)

---

Bentley 将 "Digital Twin"（数字孪生）定义为物理事物及其（可选的）相关流程的数字表示，包括系统的功能和人员与组织的角色。Digital Twin 还可以包括事物和流程的分析与仿真模型。

Bentley 将 "iTwin" 定义为基础设施数字孪生（Infrastructure Digital Twin），通过数字表示的联邦实现，例如 iModels、Reality Data、Sensor (IoT) Data 等。

## 与物理现实的连接

Digital Twin 的一个关键区别特征是与真实 **物理世界** 的连接。这种"连接"可以通过 IoT 传感器（用于物理现实中快速变化的特征）、通过定期测量（如激光扫描、摄影测量或其他测量系统，用于以天或周为单位而非秒为单位变化的物理现实特征）、或通过设计或勘测（用于本质上"固定"的物理现实特征，如道路的位置和几何形状）来建立。

## Physical Backbone（物理骨干）

基础设施资产的物理现实模型（包括几何、材料等物理属性）构成了 Digital Twin 的"骨干"。它们是 IoT 测量、活动和流程仿真、以及可视化理解孪生体及其与现实连接的"上下文"。

## 共享而非孤立

Digital Twin 的另一个区别特征是它不是特定于应用程序的，而是旨在被多个应用程序和服务共享，这与每个应用程序都有自己的孤立数据库的传统应用程序形成对比。这对于 Physical Backbone 尤其如此。几乎每个应用程序和服务都会使用它或将其信息与它关联。这影响了 Digital Twin 中信息的分解方式。

## 对齐（Aligned）

Digital Twin 应该是一个用于编写服务和应用程序的紧密数字副本。不幸的是，许多用于创建孤立的、通常是特定领域信息的应用程序在设计时并没有考虑到这样崇高的目标（通常是因为它们在实际可行之前就已经被构思出来了）。人们有时将这些数据格式称为"暗数据"，不是因为它们没有价值，而是因为如果没有原始应用程序，它们就无法解读。以 BIS 为基础，数字副本可以通过"对齐"源应用程序之间的共同概念，使这些数据更易于理解和访问。BIS 体现了数字孪生服务和应用程序的标准分类法、数据结构和关系。iModel Connectors 的一个关键角色是执行这种对齐，这样即使 iModels 包含来自不同来源的信息，它们也能保持一致。

## 联邦化（Federated）

iModels 是 iTwins 的核心，但并非所有信息都属于 iModel。例如，iModels 不是存储视频的合适位置。IoT 数据变化太快，而且已有成熟的 IoT 系统和数据历史记录器。

总会存在一些现有的数据"孤岛"（无论出于何种原因）没有被迁移到 iModels 中，但包含应该成为我们 Digital Twin 一部分的信息。

为了实现包含 iModels 和其他表示形式的紧密 Digital Twin，iTwin Platform 提供了将多种表示形式联邦化为紧密 Digital Twin 的服务和软件组件。

## 生命周期阶段的 Digital Twins

Digital Twins 促进现有建成基础设施的运营（运营 Digital Twin），但它们在其他基础设施生命周期阶段同样相关。

在施工期间，拥有待建设施以及施工现场基础设施和设备（如模板、脚手架、起重机等）的施工 Digital Twin 是有用的。施工 Digital Twin 连接到施工设备的 IoT。它通过测量系统定期更新以跟踪进度和库存。它可用于规划和模拟施工活动和进度。

在设计期间，待建设施的数字副本在设计 Digital Twin 中创建，同时创建的还有分析和仿真模型。

Physical Backbone 是运营、施工和设计孪生体之间的共同核心。它在设计阶段创建，在施工和运营阶段使用和更新。当启动新的设施改造资本项目时，运营孪生体的 Physical Backbone 是新设计孪生体现有条件的基础。

## 指导原则

从我们在生命周期阶段特定的 Digital Twins 之间共享 Physical Backbone 中产生了两个关键理念：

- 以终为始（Begin with the end in mind）
- 所有项目都是棕地项目（All projects are brownfield projects）

_以终为始_ 提醒我们，Physical Backbone 在阶段之间共享，应包含运营所需的物理特征（例如被跟踪物品的序列号）。在实际操作中，运营数据应在设计和施工阶段自然产生，例如在设备安装时捕获序列号。

_所有项目都是棕地项目_ 提醒我们，项目发生在现有环境中，要么是现有基础设施的"棕地"，要么是自然环境。应该能够使用运营 Digital Twin 的 Physical Backbone 作为新设计 Digital Twin 的起点。

相反，完全特定于某个阶段的数据应与 Physical Backbone 分离，如本文档其他主题所述。

---

| 下一步：Modeling with BIS
|:---