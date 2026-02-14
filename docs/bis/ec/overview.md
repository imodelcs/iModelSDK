# ECObjects 信息建模语言概述

ECObjects 语言由具有属性的项组成。这些项通过"ECSchema"被分组到"域"中，ECSchema 为该域中的项提供容器和命名空间。ECSchema 中有多种类型的项，用于描述对象、关系、值类型和数量。每种项类型将在下面详细描述。

任何域的根都是 *ECSchema* 本身。

- **[ECSchema](./ec-schema.md)** 描述一个"域"——其主要内容是一组密切相关的各种类型的"ECClass"。ECSchema 的 name 属性用作其中定义的所有项的命名空间。ECSchema 中的所有项都有唯一的名称。

ECSchema 不能包含其他 ECSchema，但可以引用 ECSchema：

- **ECSchemaReference** 是 ECSchema 的成员，表示对另一个 ECSchema 的引用。当 ECSchema 包含的项以某种方式依赖于被引用的 ECSchema（例如，其 ECClass 继承自被引用 ECSchema 中的 ECClass）时，就需要 ECSchemaReference。

ECObjects 有一组固定的项，这些项有一组固定的属性，ECSchema 及其项的属性可以通过自定义属性进行扩展：

- **[ECCustomAttributes](./ec-custom-attributes.md)** 是 ECSchema 和某些 schema 项的可选子元素，用于保存应用于其父元素的扩展属性值。ECCustomAttributes 可以直接应用于 ECSchema 中大多数（但不是全部）类型的项，包括 ECSchema、ECClass 和 ECProperty。

接下来的 5 种项是 ECSchema 的直接成员，定义不同类型的 ECClass。所有 ECClass 都可以包含 **[ECProperties](./ec-property.md)**，这些属性定义了具有"原语"、"结构体"、数组或导航数据类型的命名属性。

- **[ECEntityClass](./ec-entity-class.md)** 描述一类对象，其实例可以单独实例化和标识。ECEntityClass 是唯一可以插入到仓库中的 ECClass 类型。

- **[ECMixinClass](./ec-mixin-class.md)** 描述一种特殊类型的抽象实体类，可以向实体类添加属性和次要继承层次结构。Mixin 类定义了跨越主要实体继承层次结构的概念，并保存公共属性定义。Mixin 可以用作关系端点。

- **[ECStructClass](./ec-struct-class.md)** 描述一类对象，其实例始终作为更大实体的一部分实例化，不能单独标识或寻址。ECStructClass 是唯一可以用作 ECProperty *数据类型* 的 ECClass 类型。

- **[ECCustomAttributeClass](./ec-custom-attribute-class.md)** 描述一类对象，其实例被"应用于" ECSchema 中的特定项，以扩展其元数据，超出项的内置属性。

- **[ECRelationshipClass](./ec-relationship-class.md)** 定义两个实体实例之间的连接。ECRelationshipClass 可以被认为是数据库中链接表或外键列的描述。它可以定义哪个端点拥有另一个、多重性以及每个端点的有效 ECEntityClass。

其余类型的元素也是 ECSchema 的直接成员：

- **[ECEnumeration](./ec-enumeration.md)** 定义一个命名类型，包含一组值-标签对，其中标签是非本地化的显示标签（可用于形成本地化键），值是持久化的原语值。值可以是字符串或整数。

- **[KindOfQuantity](./kindofquantity.md)** 描述属性值所测量的数量。例如，"Instrument" ECEntityClass 中名为"Pressure"的 ECProperty 可以具有 KindOfQuantity "RelativePressure"。"RelativePressure"可以指定持久化单位为 PSI，以及与该 KindOfQuantity 相关的其他元数据。

- **[PropertyCategory](./property-category.md)** 定义一个分类，可以与属性关联，并帮助识别其所分类属性的重要性。

- **[Unit](./ec-unit.md)** 根据其他单位定义度量单位

- **[InvertedUnit](./ec-unit.md#Inverted-Unit)** 反转现有单位，其量纲推导是无量纲的，如坡度。

- **[Constant](./ec-constant.md)** 定义一个常量值，可以在单位定义中使用

- **[Phenomenon](./ec-phenomenon.md)** 定义可测量的物理量

- **[UnitSystem](./ec-unitsystem.md)** 定义单位的松散分组

- **[Format](./ec-format.md)** 定义在向用户显示或用于报告时如何格式化数值

- **[Changes Between ECObjects 2 and 3](./differences-between-ec2-and-ec3.md)** 如果您在 PowerPlatform 中使用过 EC，这会很有帮助。

作为 ECSchema 直接成员的项必须具有在所有直接成员中唯一的名称，例如，ECEntityClass 不能与 ECStructClass 同名。唯一性通过不区分大小写的比较来确定。有关 EC 命名规则，请参见 [ECName](./ec-name.md)。
