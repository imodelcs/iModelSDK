# Class-diagram Conventions (类图约定)

> 原文: [Class-diagram Conventions](https://www.itwinjs.org/bis/guide/references/class-diagram-conventions/)
>
> 最后更新: 2025年6月11日

## 简介

本页解释了本指南以及各个 BIS schema 文档中**类**图所使用的约定。

## 颜色

节点的颜色由类/实体类型决定。以下是类图中使用的按类/实体类型划分的默认颜色：

- `Elements\Models`
  - `Definition` - 浅青色 (#EDF4F6)
  - `Physical` - 浅蓝色 (#96C8FF)
  - `Functional or Analytical` - 浅绿色 (#C8FFC8)
  - `Spatial Location` - 浅黄色 (#FFFF96)
- `Other`
  - `Aspects` - 浅橙色 (#FFC896)
  - `Relationships` - 紫色 (#C896FF)
  - `Mixins, Structs, Enums, Other` - 灰色 (#C8C8C8)

![Colors](../../media/class-diagram-colors.png)

## 形状、轮廓和类名样式

所有实体类都有**矩形**形状边框。节点的轮廓和类名样式由类修饰符决定：

| 修饰符 | 类名样式 | 线条样式 | 线条粗细 |
|--------|----------|----------|----------|
| `Abstract` | 粗体 + 斜体 | 虚线 | 1 |
| `None (default)` | 粗体 | 实线 | 1 |
| `Sealed` | 粗体 + 下划线 | 实线 | 2 |

![Shapes](../../media/class-diagram-shapes.png)

## 继承/关系

箭头用于指示关系和继承。箭头上存在标签表示这是关系而不是继承。

- `Inheritance` - 从派生类指向基类的箭头，**没有标签**。
- `Relationship` - 从源端点指向目标端点的箭头，带有描述关系的标签。可能包含类似 UML 的多重性（[链接](https://www.uml-diagrams.org/multiplicity.html)），但可以是自由格式。

![Inheritance/Relationships](../../media/class-diagram-relationships.png)

关系通过将标签链接到关系类定义来详细说明，类似于 UML 中的 "association class" 模式。链接没有箭头，使用虚线。

![Association classes](../../media/class-diagram-relationships-details.png)

## 内容

以下约定适用于所有定义：类、struct、关系等。

类内容按顺序排列：

- `Stereotype` -（可选）有关详细信息请参见 [Stereotypes](#stereotypes)
- `Class name` - **粗体文本**，如果没有 stereotype 则是第一行
- `Description` -（可选）紧随类名之后，**斜体文本**
- `Properties` -（可选）属性列表，格式为：`'- <name><separator> <type> [<description>]'`，其中：
  - `name` - 属性名称
  - `separator` - 如果是常规属性则为 ":"，如果是导航属性则为 " ->"
  - `type` - 属性类型，可能是：
    - `primitive` - EC 基本类型（[完整列表](https://www.itwinjs.org/bis/ec/primitive-types/)）例如 string、double、point3d、IGeometry 等
    - `array` - double[]、SomeStruct[] 等
    - `enum` - 枚举名称，例如 "SomeEnum"
    - `navigation` - 端点类名称，例如 "PhysicalElement"
  - `description` -（可选）斜体描述，应从新行开始

![Content](../../media/class-diagram-content-elements.png)

关系类的 `Source` 和 `Target` 属性可以按以下格式定义：`'- <endPoint>: <multiplicity>, <class>, [polymorphic]'`，其中：

- `endPoint` - 关系端点，"Source" 或 "Target"
- `multiplicity` - 类似 UML 的关系多重性（[链接](https://www.uml-diagrams.org/multiplicity.html)），格式为 (x..y)
- `class` - 关系端点的类名
- `polymorphic` -（可选）如果关系端点是多态的，添加 "polymorphic" 后缀

![Content](../../media/class-diagram-content-relationships.png)

## Stereotypes

类似 UML 的 **stereotypes**（配置文件类）可以可选地添加到节点以添加上下文特定的含义。

Stereotypes 应按以下格式定义：`'<<Name>>'`，应作为节点的第一行放置，并以大写字母开头。

以下 stereotypes **必须**添加：

- `Relationship class` - **<<Relationship>>**
- `Aspect class` - **<<Aspect>>**
- `Mixin class` - **<<Mixin>>**
- `Struct` - **<<Struct>>**
- `Enumeration` - **<<Enum>>**

![Stereotypes](../../media/class-diagram-stereotypes.png)

## 示例

![Example](../../media/class-diagram-example.webp)

## 附加约定

- 从其他 schema 引用的类使用 schema 别名前缀，格式为：`'<alias>:<name>'`，例如 "bis:DefinitionElement"

## 情境示例

- 仅包含引用类名称的节点，与该类的单个定义分开，用于较大的类图中，当放置继承/关系箭头否则会很困难时，因为线条可能延伸很长距离或穿过其他类。

![Situational](../../media/class-diagram-situational-gaps.png)

- 以下分组方法用于基类有许多派生类的情况：

![Situational](../../media/class-diagram-situational-inheritance.png)
