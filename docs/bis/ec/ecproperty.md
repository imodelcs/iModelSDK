# ECProperty

本节首先描述 ECObjects 中 5 种属性类型的共同部分，然后详细介绍每种类型。ECObjects 支持的 5 种属性类型是 [ECPrimitiveProperty](#ecprimitiveproperty)、[ECStructProperty](#ecstructproperty)、[ECArrayProperty](#ecprimitivearrayproperty)、[ECStructArrayProperty](#ecstructarrayproperty) 和 [ECNavigationProperty](#ecnavigationproperty)。

每种属性类型建模对象中包含的不同类型的命名值。

所有属性类型都可以有一个由基类遍历算法确定的单一基属性。派生属性或属性覆盖不能更改属性类型或持久化单位（通过 KindOfQuantity）。派生属性从其基属性继承自定义属性，应用于派生属性的自定义属性覆盖相同类的继承属性。

### 通用属性

**name** 类中属性的名称。必须是有效的 [ECName](./ec-name.md)，并且在其存在的类中唯一。

**typeName** 属性的数据类型。有效的数据类型取决于属性类型。

**description** 属性的用户面向描述。已本地化，可能会在 UI 中显示。

**displayLabel** 本地化的显示标签，将在 GUI 中使用，代替名称。如果未设置，将使用属性的名称。

**readOnly** 如果为 true，属性只能初始化为一个值，一旦设置就不能更改。

**priority** 一个数字值，指定此属性相对于类中定义的其他属性的重要性。

**kindOfQuantity** 要与此属性关联的 [Kind Of Quantity](./kindofquantity.md) 的名称。

**category** 要对此属性进行分类的 [Property Category](./property-category.md) 的名称。

### 自定义属性

ECProperties 可以应用 [Custom Attributes](./ec-custom-attributes.md) 并继承应用于它们覆盖的任何属性的自定义属性。应用于基属性的自定义属性可以通过将相同的自定义属性应用于派生属性来覆盖。

### 通用子元素

[ECCustomAttributes](./ec-custom-attributes.md) _(0..1)_

## ECPrimitiveProperty

ECPrimitiveProperty 在 [ECClass](./ec-class.md) 中建模具有有限的 [primitive value types](./primitive-types.md) 和 [ECEnumerations](./ec-enumeration.md) 集合的属性，可以在任何类型的 [ECClass](./ec-class.md) 中使用。

### 原语属性附加可选属性

**minimumValue** 此属性的最小有效值。支持原语类型 int、long 和 double。

**maxmimumValue** 此属性的最大有效值。支持原语类型 int、long 和 double。

**minimumLength** 最小有效长度。支持原语类型 string 和 binary。

**maximumLength** 最小有效长度。支持原语类型 string 和 binary。

**extendedTypeName** 要与此属性关联的扩展类型的名称。有关更多信息，请参见扩展类型部分。扩展类型是具有指定扩展类型的值的特殊内存处理程序。扩展类型不能更改值的存储，如果找不到扩展类型，将使用基本类型。

### 原语属性示例

```xml
<ECProperty propertyName="OverallHeight" typeName="double" kindOfQuantity="AECU:LENGTH_SHORT"/>
```

```json
{
  "name": "OverallHeight",
  "type": "PrimitiveProperty",
  "description": "Overall Height of the Door",
  "label": "Overall Height",
  "kindOfQuantity": "AecUnits.LENGTH_SHORT",
  "typeName": "double"
},
```

## ECPrimitiveArrayProperty

原语数组属性（`ECArrayProperty`）建模由 64 位无符号整数索引的相同类型的原语值数组。数组可以指定最小和最大条目数，并支持稀疏索引。数组属性可以具有对原语属性有效的任何类型。

### 原语数组属性附加可选属性

**minOccurs** 默认为 0。表示数组中的最小元素数。

**maxOccurs** 表示 ECArrayProperty 中元素的最大数量。对于没有上限的数组，使用"unbounded"。

**extendedTypeName** 要与此属性关联的扩展类型的名称。有关更多信息，请参见扩展类型部分。

### 原语数组属性示例

```xml
<ECArrayProperty propertyName="PropertyNames" typeName="string" minOccurs="0" maxOccurs="unbounded"/>
```

```json
{
  "name": "PropertyNames",
  "type": "PrimitiveArrayProperty",
  "typeName": "string",
  "minOccurs": 0,
  "maxOccurs": 2147483647
}
```

## ECStructProperty

结构体属性（`ECStructProperty`）建模其值是 [ECStructClass](./ec-struct-class) 嵌入实例的复杂属性，不支持多态。属性的 typeName 必须设置为 [ECStructClass](./ec-struct-class.md)。

## 结构体属性示例

```xml
<ECStructProperty propertyName="AtPosition" typeName="DistanceExpression"/>
```

```json
{
  "name": "AtPosition",
  "type": "StructProperty",
  "label": "At-Position",
  "typeName": "LinearReferencing.DistanceExpression"
},
```

有关结构体类定义信息，请参见 [EC Struct Class](./ec-struct-class.md)。

## ECStructArrayProperty

结构体数组属性（`ECStructArrayProperty`）建模 ECStructClass 嵌入实例值数组，不支持多态。属性的 typeName 必须设置为 [ECStructClass](./ec-struct-class.md)。

### 结构体数组属性附加可选属性

**minOccurs** 默认为 0。表示数组中的最小元素数。

**maxOccurs** 表示 ECArrayProperty 中元素的最大数量。对于没有上限的数组，使用"unbounded"。

### 结构体数组属性示例

```xml
<ECStructArrayProperty propertyName="Forces" typeName="LinearForce" displayLabel="Forces" description="Force values." />
```

```json
{
  "name": "Forces",
  "type": "StructArrayProperty",
  "description": "Force values.",
  "label": "Forces",
  "typeName": "StructuralAnalysis.LinearForce",
  "minOccurs": 0,
  "maxOccurs": 2147483647
}
```

## ECNavigationProperty

导航属性建模对另一个实例的引用，即相关实例。此引用可以简单到相关实例的 Id，它实际上可能指向实例的内存副本、加载相关实例的 URL 或选择相关实例的查询。

> 导航属性仅对可以作为关系端点的类有效：ECEntityClass、ECMixinClass 和 ECRelationshipClass。

导航属性还有其他规则：

- 只能指向单一端点。也就是说，它必须指向最大限制为 1 的端点。
- 必须添加到被引用关系支持的最基本 ECEntityClass。
- 必须引用层次结构中的根关系。
- 被引用的关系不能被派生类中的属性覆盖覆盖[]。

### 导航属性附加可选属性

**relationshipName** 此导航属性遍历以获取相关实例的关系。

**direction** 遍历被引用关系的方向

### 导航属性示例

```xml
<ECNavigationProperty propertyName="Parent" relationshipName="ElementOwnsChildElements" direction="backward" />
```

```json
{
  "name": "Parent",
  "type": "NavigationProperty",
  "relationshipName": "BisCore.ElementOwnsChildElements",
  "direction": "Backward"
},
```
