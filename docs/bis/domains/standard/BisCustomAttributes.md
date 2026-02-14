# BisCustomAttributes (BIS Custom Attributes) Schema

**Alias:** bisCA

**Version:** 1.0.0

用于表示 BIS 概念的自定义属性。

## 目录

- Custom Attribute Classes
  - SchemaLayerInfo
- Enumerations
  - SchemaLayer

## Custom Attribute Classes

### SchemaLayerInfo _Sealed_ CustomAttributeClass

声明 Schema 在 BIS Schema 层次结构中的目标层。

**适用于：** Schema

BIS Schema 应该使用 `SchemaLayerInfo` `CustomAttribute` 进行标记，以启用与 Schema 引用相关的验证和错误检查。

#### 属性

| 名称 | 描述 | 标签 | 类别 | 只读 | 优先级 |
| --- | --- | --- | --- | --- | --- |
| Value | Schema 在 BIS Schema 层次结构中所针对的层。 |  |  | false | 0 |

## Enumerations

### SchemaLayer Enumeration

**基础类型：** string

定义 BIS Schema 层次结构中的层。

**严格：** true

| 标签 | 值 | 描述 |
| --- | --- | --- |
| Core | Core | 用于定义所有其他 BIS Schema 的最基本概念和关键组织策略的 Schema 层。 |
| Common | Common | 用于定义多个学科使用的抽象概念和模式的 Schema 层。 |
| Discipline-Physical | DisciplinePhysical | 用于针对特定学科，关注物理/空间及密切相关概念的 Schema 层。 |
| Discipline-Other | DisciplineOther | 用于针对特定学科，定义除物理之外的其他建模视角概念的 Schema 层。 |
| Application | Application | 用于定义其他 Schema 不需要或不想引用的概念的 Schema 层。 |

特定层的 Schema 只能引用同一层或更低层的 Schema。

---

*原文链接：https://www.itwinjs.org/bis/domains/biscustomattributes.ecschema/*

*最后更新：2024年5月15日*
