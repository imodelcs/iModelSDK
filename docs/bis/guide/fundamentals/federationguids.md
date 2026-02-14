# FederationGuids

每个 BIS `Element` 都有一个可选的 128 位全局唯一标识符，称为 `FederationGuid`。它实际上标识 Element 表示的现实世界实体，而不是 Element 本身。通常，FederationGuid 由外部系统分配，以将 Elements 联合到其外部含义。

## 唯一性范围

分配的 FederationGuid 被强制在单个 BIS Repository 中唯一。但是，多个 BIS Repositories 可以使用相同的 FederationGuid 来引用同一个现实世界实体。

因此，跨多个 BIS Repositories 具有相同 FederationGuid 的 Elements 的 Code 通常是相同的，除非此类 Code 被强制在 iTwin 中的所有 BIS Repositories 中唯一。

## 建模视角和粒度

请注意，FederationGuid 隐式地表示特定粒度和建模视角的现实世界实体。因此，在不同建模视角中表示相同现实世界实体的 Elements 预期被分配不同的 FederationGuid。也就是说，如果现实世界实体被物理地、功能地和分析地建模，则在每个建模视角中表示它的 Elements 预期被分配不同的 FederationGuid。

同样的期望适用于不同粒度的现实世界实体建模。也就是说，如果同一现实世界实体通过信息层次结构中描述的任何技术被建模为更细粒度 Elements 的聚合，则这些 Elements 中的每一个预期被分配与整体实体的 FederationGuid 不同的 FederationGuid。

## Element 外部标识

当存储在 iModel 中时，如果 Element 未被其数据写入者分配 `FederationGuid`，则会收到一个唯一的 `FederationGuid`。此行为使 Element 的 FederationGuid 能够用作其 iModel 外部的系统可以利用的稳定标识符。

这样，Element 可以在 BIS Repository 中被删除和重新创建，这可能会更改其在 iModel 中的 ElementId，但只要保留其 FederationGuid，就不会影响引用它的任何外部系统。

---

| 下一篇：ElementAspect Fundamentals
|:---

最后更新：2025年6月11日
