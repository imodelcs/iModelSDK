# 单一责任方原则（SRPP）

在基础设施工程的整个信息生命周期中，信息的责任是一个关键问题。这些责任影响所有相关信息仓库的组织，包括 BIS Repositories。

因此，当我们能够识别 BIS Repository 中任何信息的单一责任方时，这很有帮助。为了便于识别信息的责任方，所有领域作者和开发人员都应遵循这两条规则：

- 一个 `Model` 在任何给定时间点应该有一个单一责任方。
- 被子建模的 `Element`s 可能与其子 `Model` 有不同的责任方。

第一条规则有助于将 `Model`s 映射到 ISO 19650 "information containers"，以及其他实际考虑因素。第二条规则允许责任方将 `Element` 的详细子建模责任委托给另一方。

![责任方](https://www.itwinjs.org/media/srpp-responsible-parties.png)

责任方可以是组织或个人。由于不同学科通常有不同的责任方，自然地，不应该在单个 Model 中建模多个学科。

在物理视角中，责任通常根据系统分配，一方负责设计给定系统。这驱动了物理分区内的组织。有关详细信息，请参阅 Physical Hierarchy。

SRPP 本质上定义了一个工作流驱动的约束，用于将 `Element`s 组织到 Models 中。在该约束内，关于 `Element`/`Model` 组织有高度的灵活性。通常，由单方负责的 `Element`s 和 `Model`s 的组织应该由预期的用户工作流驱动，同时牢记 Model Fundamentals 中描述的 `Model`s 的实际影响。

---

| 下一篇：Organizing Models and Elements
|:---

最后更新：2025年6月11日
