# ECDbMap (ECDb DB Mapping) Schema

**Alias:** ecdbmap

**Version:** 2.0.4

自定义属性，用于自定义 ECDb 的 ECSchema 到数据库的映射。

## 目录

- Struct Classes
  - DbIndex
- Custom Attribute Classes
  - ClassMap
  - DbIndexList
  - ForeignKeyConstraint
  - ForeignKeyView
  - ImportRequiresVersion
  - JoinedTablePerDirectSubclass
  - LinkTableRelationshipMap
  - PropertyMap
  - QueryView
  - SchemaMap
  - ShareColumns
  - UseRequiresVersion

---

### DbIndex _Sealed_ StructClass

为 ECClass 指定数据库索引。

#### 属性

| 名称 | 描述 | 标签 | 类别 | 只读 | 优先级 |
| --- | --- | --- | --- | --- | --- |
| Name | 索引的名称。必须遵循 EC 标识符规则。它需要在数据库中全局唯一。 |  |  | false | 0 |
| IsUnique | 默认值：false。如果为 true，索引属性中的所有值必须唯一。 |  |  | false | 0 |
| Properties | 组成索引的属性列表。仅支持原始类型（primitive type）的属性。 |  |  | false | 0 |
| Where | 索引的 Where 约束 |  |  | false | 0 |

---

## Custom Attribute Classes

### ClassMap _Sealed_ CustomAttributeClass

**适用于：** EntityClass, RelationshipClass

#### 属性

| 名称 | 描述 | 标签 | 类别 | 只读 | 优先级 |
| --- | --- | --- | --- | --- | --- |
| MapStrategy | 定义 ECClass 如何映射到表。值：OwnTable（默认）、TablePerHierarchy、ExistingTable、NotMapped |  |  | false | 0 |
| TableName | 如果 MapStrategy 是 'ExistingTable'，在此提供表名。其他情况下不得设置。 |  |  | false | 0 |
| ECInstanceIdColumn | 可选地指定自定义 'primary key' 列的名称，该列必须是 Int64 类型。 |  |  | false | 0 |

---

### DbIndexList _Sealed_ CustomAttributeClass

**适用于：** EntityClass, RelationshipClass

#### 属性

| 名称 | 描述 | 标签 | 类别 | 只读 | 优先级 |
| --- | --- | --- | --- | --- | --- |
| Indexes | 此类属性上的索引列表。可用于提高查询性能或添加唯一约束。 |  |  | false | 0 |

---

### ForeignKeyConstraint _Sealed_ CustomAttributeClass

为此导航属性（navigation property）创建外键。

**适用于：** NavigationProperty

#### 属性

| 名称 | 描述 | 标签 | 类别 | 只读 | 优先级 |
| --- | --- | --- | --- | --- | --- |
| OnDeleteAction | 可能的值：NoAction（默认）、Cascade（删除父行时删除子行）、SetNull（子行中的外键属性设置为 NULL）、Restrict（如果仍有子行则不能删除父行）。 |  |  | false | 0 |
| OnUpdateAction | 可能的值：NoAction（默认）、Cascade（更新父主键时更新子外键）。 |  |  | false | 0 |

---

### ForeignKeyView _Sealed_ CustomAttributeClass

将关系标记为基于约束类（constraint class）上的导航属性的自动视图。

**适用于：** RelationshipClass

此 CA 可以应用于抽象 ECRelationship 类，它将尝试在其中一个约束类上找到匹配的导航属性，并根据该信息动态生成视图查询。基本上将关系转换为视图。

---

### ImportRequiresVersion _Sealed_ CustomAttributeClass

使 Schema 只能由特定 ECDb 版本或更高版本导入。

**适用于：** Schema

`ECDbRuntimeVersion` 值指定导入此 Schema 所需的 ECDb 版本。
此值与当前 ECDb 运行时已知的最高的 ECDb profile 版本进行比较，该版本可能高于当前打开的文件 profile 版本。
较旧版本的 ECDb 将拒绝导入具有此 CA 的 Schema（导入将被拒绝）。
如果 Schema 已在文件中，较旧版本的 ECDb 可以使用它，如果应限制使用，请改用 `UseRequiresVersion`。

使用示例：

```xml
<?xml version="1.0" encoding="utf-8" ?>
<ECSchema schemaName="Schema1" alias="s1" version="1.0.1" xmlns="http://www.bentley.com/schemas/Bentley.ECXML.3.2">
  <ECSchemaReference name="ECDbMap" version="02.00.02" alias="ecdbmap"/>
  <ECCustomAttributes>
    <ImportRequiresVersion xmlns="ECDbMap.02.00.02">
      <ECDbRuntimeVersion>4.0.0.5</ECDbRuntimeVersion>
    </ImportRequiresVersion>
  </ECCustomAttributes>
  <ECEntityClass typeName="Foo" >
    <ECProperty propertyName="Length" typeName="double" />
  </ECEntityClass>
</ECSchema>
```

#### 属性

| 名称 | 描述 | 标签 | 类别 | 只读 | 优先级 |
| --- | --- | --- | --- | --- | --- |
| ECDbRuntimeVersion | 必需。ECDb profile 版本号，例如 4.0.0.3。指的是运行时版本，不是文件版本。 |  |  | false | 0 |

---

### JoinedTablePerDirectSubclass _Sealed_ CustomAttributeClass

将子类及其子类映射到连接表。只能应用于使用 MapStrategy TablePerHierarchy 的层次结构中的类。

**适用于：** EntityClass

---

### LinkTableRelationshipMap _Sealed_ CustomAttributeClass

**适用于：** RelationshipClass

#### 属性

| 名称 | 描述 | 标签 | 类别 | 只读 | 优先级 |
| --- | --- | --- | --- | --- | --- |
| SourceECInstanceIdColumn | 可选。如果未设置，将使用默认列名 |  |  | false | 0 |
| TargetECInstanceIdColumn | 可选。如果未设置，将使用默认列名 |  |  | false | 0 |
| CreateForeignKeyConstraints | 默认值：true。如果设置为 false，链接表上不会创建外键约束。在这种情况下，删除实例不会删除链接表中的关系。 |  |  | false | 0 |
| AllowDuplicateRelationships | 默认值：false。如果设置为 true，则允许重复关系。 |  |  | false | 0 |

---

### PropertyMap _Sealed_ CustomAttributeClass

**适用于：** PrimitiveProperty

#### 属性

| 名称 | 描述 | 标签 | 类别 | 只读 | 优先级 |
| --- | --- | --- | --- | --- | --- |
| ColumnName | 如果未指定，则使用 ECProperty 名称。它必须遵循 EC 标识符规范。 |  |  | false | 0 |
| IsNullable | 如果为 false，此属性的值不能取消设置。 |  |  | false | 0 |
| IsUnique | 只允许此属性的值唯一。 |  |  | false | 0 |
| Collation | 指定此属性的字符串比较方式。可能的值：Binary（默认）：按位匹配。NoCase：与 binary 相同，但 ASCII 的 26 个大写字符在比较前转换为小写等效字符。注意它只转换 ASCII 字符。RTrim：与 binary 相同，但忽略尾随空格字符。 |  |  | false | 0 |

---

### QueryView _Sealed_ CustomAttributeClass

将类标记为基于 ECSQL 的视图。

**适用于：** EntityClass

允许定义一个抽象实体类，它不由实际数据支持，而是由 ECSql 查询支持，该查询被执行以获取类的实例。
有关如何使用视图的详细信息，请参阅 ECSqlReference。

视图必须返回 ECInstanceId 和 ECClassId。

使用视图的 Schema 示例：

```xml
<ECSchema schemaName="TestSchema" alias="ts" version="1.0.0" xmlns="http://www.bentley.com/schemas/Bentley.ECXML.3.2">
  <ECSchemaReference name='ECDbMap' version='02.00.03' alias='ecdbmap' />
  <ECEntityClass typeName="JsonObject">
    <ECProperty propertyName="json" typeName="string" extendedTypeName="Json" />
  </ECEntityClass>
  <ECEntityClass typeName="Pipe" modifier="Abstract">
    <ECCustomAttributes>
      <QueryView xmlns="ECDbMap.02.00.04">
        <Query>
          SELECT
            jo.ECInstanceId,
            ec_classid('TestSchema', 'Pipe') as [ECClassId]
            CAST(json_extract(jo.json, '$.diameter') AS INTEGER) [Diameter],
            CAST(json_extract(jo.json, '$.length') AS INTEGER) [Length],
            json_extract(jo.json, '$.material') [Material]
          FROM ts.JsonObject jo
          WHERE json_extract(jo.json, '$.type') = 'pipe'
        </Query>
      </QueryView>
    </ECCustomAttributes>
    <ECProperty propertyName="Diameter" typeName="int" />
    <ECProperty propertyName="Length" typeName="int"/>
    <ECProperty propertyName="Material" typeName="string" />
  </ECEntityClass>
</ECSchema>
```

`JsonObject` 可以填充以下数据：

```json
{"type": "pipe", "diameter": 10, "length": 100, "material": "steel"}
{"type": "pipe", "diameter": 15, "length": 200, "material": "copper"}
{"type": "pipe", "diameter": 20, "length": 150, "material": "plastic"}
{"type": "cable", "diameter": 5, "length": 500, "material": "copper","type": "coaxial"}
{"type": "cable", "diameter": 2, "length": 1000, "material": "fiber optic","type": "single-mode"}
{"type": "cable", "diameter": 3, "length": 750, "material": "aluminum","type": "twisted pair"}
```

运行此查询：

```sql
SELECT Length, Diameter, Material FROM ts.Pipe
```

将返回此结果：

| Length | Diameter | Material |
|--------|----------|----------|
| 100 | 10 | steel |
| 200 | 15 | copper |
| 150 | 20 | plastic |

#### 属性

| 名称 | 描述 | 标签 | 类别 | 只读 | 优先级 |
| --- | --- | --- | --- | --- | --- |
| Query | 只允许原始类型的 ECSql 查询 |  |  | false | 0 |

---

### SchemaMap _Sealed_ CustomAttributeClass

**适用于：** Schema

#### 属性

| 名称 | 描述 | 标签 | 类别 | 只读 | 优先级 |
| --- | --- | --- | --- | --- | --- |
| TablePrefix | 指定生成表的前缀。如果未指定，则使用 ECSchema 的别名 |  |  | false | 0 |

---

### ShareColumns _Sealed_ CustomAttributeClass

允许在 ECProperty 之间共享列。只能应用于 MapStrategy TablePerHierarchy

**适用于：** EntityClass, RelationshipClass

#### 属性

| 名称 | 描述 | 标签 | 类别 | 只读 | 优先级 |
| --- | --- | --- | --- | --- | --- |
| ApplyToSubclassesOnly | False（默认）：为应用此 CA 的 ECClass 及其所有子类的属性共享列。True：不为该 ECClass 共享列，但为其所有子类共享列。 |  |  | false | 0 |
| MaxSharedColumnsBeforeOverflow | 在使用溢出表之前使用的最大共享列数（可选）。如果未指定，ECDb 将创建尽可能多的共享列，直到表有 63 列。 |  |  | false | 0 |

---

### UseRequiresVersion _Sealed_ CustomAttributeClass

使 ECDb 拒绝查询具有此 CA 的类，如果条件不满足，则拒绝查询具有此 CA 的 CA。

**适用于：** AnyClass

可以应用于一个类，使得使用该类的查询需要最低的 ECDb 或 ECSql 版本。
当应用于自定义属性类时，该自定义属性将信息传递给它所应用的所有类。（也支持嵌套）。

将此应用于除关系、实体或自定义属性类以外的任何内容都没有效果。

`ECSqlVersion` 指定独立于 ECDb profile 版本维护的最低 ECSql 版本，并允许第二种跟踪更改的机制（sql 版本通常比 profile 版本更频繁地递增）

违反此 CA 设置的限制的 ECSql 查询将无法准备，并向 ECDb 问题报告器写入消息。

使用此 CA 不会限制哪些 ECDb 版本可以导入 Schema。要限制导入，请将 `ImportRequiresVersion` CA 应用于 Schema。

使用示例：

```xml
<?xml version="1.0" encoding="utf-8" ?>
<ECSchema schemaName="Schema1" alias="s1" version="1.0.1" xmlns="http://www.bentley.com/schemas/Bentley.ECXML.3.2">
  <ECSchemaReference name="ECDbMap" version="02.00.02" alias="ecdbmap"/>
  <ECCustomAttributeClass typeName="Bar" modifier="Sealed" appliesTo="EntityClass">
    <ECCustomAttributes>
      <UseRequiresVersion xmlns="ECDbMap.02.00.02">
        <ECDbRuntimeVersion>4.0.0.4</ECDbRuntimeVersion>
      </UseRequiresVersion>
    </ECCustomAttributes>
  </ECCustomAttributeClass>
  <ECEntityClass typeName="Foo" >
    <ECCustomAttributes>
      <Bar></Bar>
    </ECCustomAttributes>
    <ECProperty propertyName="Length" typeName="double" />
  </ECEntityClass>
</ECSchema>
```

直接应用于实体类的示例，限制其 ECSql 版本：

```xml
<ECEntityClass typeName="Foo" >
  <ECCustomAttributes>
    <UseRequiresVersion xmlns="ECDbMap.02.00.02">
      <ECSqlVersion>1.0.0.0</ECSqlVersion>
    </UseRequiresVersion>
  </ECCustomAttributes>
  <ECProperty propertyName="Length" typeName="double" />
</ECEntityClass>
<ECEntityClass typeName="Bar">
  <BaseClass>Foo</BaseClass>
</ECEntityClass>
```

上面示例中的类 `Bar` 也会受到限制的影响，因为它派生自 `Foo`。

#### 属性

| 名称 | 描述 | 标签 | 类别 | 只读 | 优先级 |
| --- | --- | --- | --- | --- | --- |
| ECDbRuntimeVersion | 可选。ECDb profile 版本号，例如 4.0.0.3。指的是运行时版本，不是文件版本。 |  |  | false | 0 |
| ECSqlVersion | 可选。EC SQL profile 版本号，例如 1.2.0.0。 |  |  | false | 0 |

---

*原文链接：https://www.itwinjs.org/bis/domains/ecdbmap.ecschema/*

*最后更新：2025年6月11日*
