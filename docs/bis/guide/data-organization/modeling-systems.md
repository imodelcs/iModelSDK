# 建模系统

物理基础设施的存在是为了实现一个或多个功能。校园的功能是为人们提供学习。建筑物为人们的工作和娱乐提供庇护。锁组件帮助为空间提供安全保障。景观系统的主要功能可能是提供悦目的美学。有些功能被显式建模（请参阅 Functional Models and Elements），但即使它们没有被建模，现实世界的功能是物理基础设施存在的原因。

> "物理系统"是一组共同实现功能的物理对象。

这些对象可能在物理上连接也可能不连接。给定对象可能在多个系统中发挥作用，例如泵在管道系统、电气系统、安全系统、噪音消减系统等中都有作用。由于系统的这种概念不是物理对象或其组织固有的，而是由建模者对物理对象安排目的的感知定义的，BIS 将物理系统建模为根据其功能目的逻辑分组 `PhysicalElement`s 的"信息元素"。

因此，`PhysicalSystem` Element 不是 `bis:PhysicalElement` 的子类，而是 `bis:GroupInformationElement` 的子类。您可以将其视为"关于物理系统的信息"，而不是直接建模物理系统本身的物理对象。`PhysicalSystem` 因此支持类似于 SpatialComposition 的 `PhysicalElements` 的次要组织。

`bis:PhysicalSystemGroupsMembers` 关系用于指示哪些元素是给定系统的一部分。它允许单个 `PhysicalElement` 成为多个 `PhysicalSystems` 的一部分。

我们预期 Models 沿着自然系统边界组织将是常见的。如果 `PhysicalSystemGroupsMembers` 关系指向一个被子建模的 Element，其子 Model 的所有 Elements 都被视为系统的一部分。

> BIS 工作组正在考虑 `PhysicalSystem` 指示 `PhysicalPartition`（及其子 Model 中的所有 Elements）是物理系统一部分的方式。

## 系统倾向于与责任保持一致

按物理系统组织 `PhysicalModel`s 与 SRPP 一致，因为责任通常按系统分配。

例如，建筑师负责建筑物的建筑_系统_。这些_系统_以有用的方式分区和庇护空间。建筑师将使用一个或多个_系统_，其子 Models 包含构成建筑系统一部分的详细墙、窗和门。

结构工程师负责支撑建筑物的结构_系统_的结构构件。结构工程师将使用一个或多个_系统_，其子 Models 包含构成结构_系统_的梁、柱和承重墙。

由于承重墙（结构工程师的责任）通常是建筑_系统_的一部分，`PhysicalSystemGroupsMembers` 关系可用于将它们"分组"到建筑_系统_中。

在不同的上下文中（如不同的生命周期阶段），责任会发生变化，领域 schemas 应该有足够的灵活性来处理这些情况。在设计期间，建筑师和结构工程师对他们设计的系统负有法律责任。在运营期间，建筑和结构都是设施经理的责任。理论上，当将设计数字孪生转换为运营数字孪生时，建筑和结构 Models 可以合并为一个。在实践中，这可能不常见，因为 `Model`s 的分离对设施经理来说不是真正的问题，保持分离将使启动新的改造资本项目更容易。无论如何，__软件对 `Element`s 如何组织到 `Model`s 中的预期不应太"僵化"__。

---

| 下一篇：Organizing Definition Elements
|:---
