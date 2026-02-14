# Mixins

Mixins 在支持 BIS 中的跨领域协调方面发挥着关键作用。

Mixin 是遵循严格要求的抽象 EC 类，旨在提供所需功能，同时最大限度地减少混乱和实现成本。如果发现支持放松的用例，将来可能会放宽要求。Mixin 类的要求如下：

1. Mixin 是抽象 EC Entity 类。
2. Mixin 可以有 0 或 1 个基类。如果有基类，它必须是另一个 Mixin。
3. Mixin 必须定义 IsMixin 自定义属性。
4. Mixin 不得覆盖继承的属性。

Mixin 自定义属性定义如下：

```xml
<ECCustomAttributeClass typeName="IsMixin" description="Applied to abstract ECEntityClasses which serve as secondary base classes for normal ECEntityClasses." displayLabel="Is Mixin" appliesTo="EntityClass" modifier="Sealed" >
  <ECProperty propertyName="AppliesToEntityClass" typeName="string" description="This mixin may only be applied to entity classes which derive from is class.  Class Name should be fully specified as 'alias:ClassName'" />
</ECCustomAttributeClass>
```

类通过将 Mixin 类声明为基类来合并 Mixin。Mixin 从不是列出的第一个基类（该位置保留给"真正"的基类）。类可以实现多个 Mixin，但只能有一个"真正"的基类。合并 Mixin 的类也必须遵循严格的规则：

1. 合并类必须从 IsMixin 自定义属性中定义的 AppliesToEntityClass 继承。
2. 实现类不得具有与 Mixin 属性同名的继承属性。

通常，建议将 Mixin 用作关系端点。通过 Mixin 从属性检索数据的 ECSQL 查询可能会出现性能下降。因此，在 Mixin 中引入属性的决定应通过仔细分析需要它们的用例来完成。

按照约定，类接口式的 Mixin 类具有带"I"前缀的类名。类接口式的 Mixin 满足以下一个或多个条件：

1. Mixin 预期用作关系端点。
2. Mixin 预期由不知道哪个类合并了 Mixin 的代码或逻辑使用。
3. Mixin 没有属性，用作标记类。

---

| 下一篇：Model Fundamentals
|:---

最后更新：2025年6月11日
