# ECClass

ECObjects 中有 5 种类型的 ECClass：[ECEntityClass](./ec-entity-class.md)、[ECMixinClass](./ec-mixin-class.md)、[ECStructClass](./ec-struct-class.md)、[ECCustomAttributeClass](./ec-custom-attribute-class.md) 和 [ECRelationshipClass](./ec-relationship-class.md)。本节将介绍所有 ECClass 类型的共同点。

每种类类型建模不同类型的对象。ECEntityClass 建模业务对象，这些对象可以单独实例化并具有 Id。ECStructClass 建模复杂属性类型，通常称为结构体。ECCustomAttributeClass 建模应用于其他 schema 元素以提供额外元数据的对象。ECRelationshipClass 建模 ECEntityClass 之间的连接。

所有类都支持在其自己的类类型内进行继承。因此，ECEntityClass 可以将另一个 ECEntityClass 作为其基类，但不能将 ECStructClass 作为基类。ECRelationshipClass 仅支持单继承，而 ECEntityClass 使用"mixins"支持有限形式的多继承。

## 通用类属性

**typeName** 定义此 ECClass 的名称。必须是有效的 [ECName](./ec-name.md)，并且在 schema 中的所有其他项中唯一。

**description** 类的用户面向描述。已本地化，可能会在 UI 中显示。

**displayLabel** 本地化的显示标签，将在 GUI 中使用，代替名称。如果未设置，将使用类的 Type Name。

**modifier** 将类标识为抽象或密封的。
- 有效选项有：

  - None（默认）—— 普通的、可实例化的类。对于 ECRelationshipClass 类型无效。
  - Abstract —— 抽象类，无法实例化。
  - Sealed —— 普通的、可实例化的类，但不能用作基类或拥有子类

## 自定义属性

ECClass 可以应用 [Custom Attributes](./ec-custom-attributes.md) 并继承应用于其基类的自定义属性。应用于基类的自定义属性可以通过将相同的自定义属性应用于派生类来覆盖。

## 通用子元素

[ECCustomAttributes](./ec-custom-attributes.md) _(0..1)_

BaseClass _(0..*)_

- 基类的多重性根据各个 ECClass Type 而变化。

[ECPrimitiveProperty](./ec-property.md#ecprimitiveproperty) _(0..*)_

[ECStructProperty](./ec-property.md#ecstructproperty) _(0..*)_

[ECArrayProperty](./ec-property.md#ecprimitivearrayproperty) _(0..*)_

[ECStructArrayProperty](./ec-property.md#ecstructarrayproperty) _(0..*)_

## 基 ECClass 的遍历顺序

基类以深度优先的方式遍历，用于所有目的，包括属性继承（给定命名 ECProperty 的第一次出现"获胜"）。例如，给定这组简化的 ECClass 定义：

```xml
<ECEntityClass typeName="Root"/> //定义一个属性"A"

<ECEntityClass typeName="B1">
  <BaseClass>Root</BaseClass>
</ECEntityClass>

<ECEntityClass typeName="B2"/> // 定义一个属性"A"

<ECEntityClass typeName="Foo">
  <BaseClass>B1</BaseClass>
  <BaseClass>B2</BaseClass>
</ECEntityClass>
```

遍历顺序将是：Foo、B1、Root、B2，Root 的属性"A"定义将"获胜"，但如果 Foo 首先定义 B2：

```xml
<ECEntityClass typeName="Foo">
  <BaseClass>B2</BaseClass>
  <BaseClass>B1</BaseClass>
</ECEntityClass>
```

遍历顺序将是：Foo、B2、B1、Root，B2 的属性"A"定义将"获胜"。如果我们通过多继承引入"菱形模式"，将"Root"添加为 B2 的 BaseClass，遍历顺序（使用我们的第二个 Foo 定义）将是：Foo、B2、Root、B1、Root。如果多态算法正在寻找"Root"的子类，它将在第一次遇到"Root"时停止。
