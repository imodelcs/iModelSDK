# ECSchema

ECSchema 是所有其他 ECObject 项的根容器，并为其包含的每个项提供命名空间。一个 schema 可以被另一个 schema 引用，但不能嵌入到另一个 schema 中。因此，ECObjects 中的命名空间没有层次结构。

## 属性

**schemaName** schema 的名称以及 schema 内项的命名空间。必须在给定系统中唯一，并且是有效的 [ECName](./ec-name.md)。应该是人类可读的，并尽可能避免缩写。

**alias** schema 名称的简短形式，在长度受限时使用。

- alias 遵循与 schema 名称相同的命名规则。
- 与 schema 名称一样，alias 必须在给定系统中唯一。与 schema 名称不同的是，如果 alias 与另一个 alias 冲突，将附加一个数字以确保在当前上下文中的唯一性。
- schema 名称始终一致，但 alias 在某些上下文中可能会改变。

**version** 三位版本号，格式为 `RR.WW.mm`，即 `Read.Write.Minor`。

- 增加 Read 版本号表示新格式的数据不再能使用旧 schema 读取。
- 增加 Write 版本表示数据仍然可以使用旧 schema 读取，但不能写入。
- 增加 Minor 版本表示对 schema 的更改完全是非破坏性的。

**description** schema 的可选且本地化的纯文本描述。

**displayLabel** schema 的可选且本地化的标签，用于在 UI 中显示

## 子元素

[ECSchemaReference](#ecschemareference) _(0..*)_

[ECCustomAttributes](./ec-custom-attributes.md) _(0..1)_

[ECEntityClass](./ec-entity-class.md) _(0..*)_

[ECMixinClass](./ec-mixin-class.md) _(0..*)_

[ECStructClass](./ec-struct-class.md) _(0..*)_

[ECCustomAttributeClass](./ec-custom-attribute-class.md) _(0..*)_

[ECRelationshipClass](./ec-relationship-class.md) _(0..*)_

[ECEnumeration](./ec-enumeration.md) _(0..*)_

[KindOfQuantity](./kindofquantity.md) _(0..*)_

[PropertyCategory](./property-category.md) _(0..*)_

## ECSchemaReference

包含标识被引用 schema 的所有信息。

不支持循环引用，这将导致无法加载具有循环引用的 schema。

### Schema 引用属性

**name** 被引用的 ECSchema 的名称。必须与被引用 schema 的 Schema Name 匹配。

**version** 被引用的 ECSchema 的版本。

> 被引用的 schema 使用"最新兼容匹配"定位，其中 read 和 write 版本必须匹配，并且定位到的 schema 的 minor 版本必须等于或大于 schema 引用中列出的版本

**alias** 引用被引用 schema 中的项时使用的 alias。此 alias 通常与被引用 schema 中定义的 alias 匹配，但可能不同。如果不同，它仅在包含 ECSchemaReference 的 schema 的上下文中有效。

## 示例

```xml
<ECSchema schemaName="BisCore" alias="bis" version="01.00.18" xmlns="http://www.bentley.com/schemas/Bentley.ECXML.3.2" displayLabel="BIS Core" description="The BIS core schema contains classes that all other domain schemas extend.">
    <ECSchemaReference name="CoreCustomAttributes" version="01.00.03" alias="CoreCA"/>

        <ECCustomAttributes>
        <ProductionStatus xmlns="CoreCustomAttributes.01.00.03">
            <SupportedUse>NotForProduction</SupportedUse>
        </ProductionStatus>
    </ECCustomAttributes>

    ....

</ECSchema>
```

```json
{
  "$schema": "https://dev.bentley.com/json_schemas/ec/32/ecschema",
  "name": "BisCore",
  "version": "01.00.18",
  "alias": "bis",
  "label": "BIS Core",
  "description": "The BIS core schema contains classes that all other domain schemas extend.",
  "references": [
    {
      "name": "CoreCustomAttributes",
      "version": "01.00.04"
    }
  ],
  "customAttributes": [
    {
      "className": "CoreCustomAttributes.ProductionStatus",
      "SupportedUse": "NotForProduction"
    }
  ],
  "items": {
    ...
  }
}
```
