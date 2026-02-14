# Instance-diagram Conventions (实例图约定)

> 原文: [Instance-diagram Conventions](https://www.itwinjs.org/bis/guide/references/instance-diagram-conventions/)
>
> 最后更新: 2025年6月11日

## 简介

本页解释了本指南以及各个 BIS schema 文档中**实例**图所使用的约定。

## 颜色

对于 **Elements**，颜色由元素类型决定：

- `Information` - 浅青色 (#EDF4F6)
- `Physical` - 浅蓝色 (#96C8FF)
- `Functional or Analytical` - 浅绿色 (#C8FFC8)
- `Spatial Location` - 浅黄色 (#FFFF96)
- `Drawing` - 紫色 (#C896FF)

![Element colors](../../media/instance-diagram-colors-elements.png)

所有 **Models** 都使用白色 (#FFFFFF) 着色，因为它们的类型可以从其 modeled-element 推断出来。

![Model colors](../../media/instance-diagram-colors-models.png)

## 形状和轮廓

Models 由**嵌套节点**表示。

Models 和 Elements 都具有**圆角矩形**形状和**实线，粗细 1** 的轮廓。

![Element colors](../../media/instance-diagram-shapes.png)

## 关系

所有关系箭头由**实线箭头**表示，**粗细 1**。

- `Parent owns child` - 从子元素指向其父元素的箭头。**默认情况下不添加标签**，但如果特定的父子关系与给定上下文相关，则会添加自定义标签。
- `Model sub-models Element` - 从 model 指向被子建模的 element（即 model 分解的 element）的箭头。
- `Other relationships` - 从源元素指向目标元素的箭头，带有描述关系的**标签**。

![Relationships](../../media/instance-diagram-relationships.png)

## 内容

以下约定适用于所有 **Element** 实例（包括 aspects）。

实例内容按顺序排列：

- `Class name` - **粗体文本**，第一行
- `Code/UserLabel` -（可选）紧随类名之后，用引号包围，例如 `"The Taj Mahal"`
- `Properties` -（可选）属性列表，格式为：`'- <name> <operator> <value>'`，其中：
  - `name` - 属性名称
  - `operator` - 如果是常规属性则为 "="，如果是导航属性则为 "->"
  - `value` - 属性值。如果是导航属性，则添加 Code/UserLabel，例如 `"The Taj Mahal"`

![Content](../../media/instance-diagram-content.png)

**Models** 有一个可选的标签，表示 model 的具体类型或上下文特定信息，例如正在建模的现实世界实体是什么。参见 [shapes and outlines example](#shapes-and-outlines)。

## 示例

![Example](../../media/instance-diagram-example.png)
