# Information Models and Elements

> 原文: [Information Models and Elements - iTwin.js](https://www.itwinjs.org/bis/guide/other-perspectives/information-models-and-elements/)

## 简介 (Introduction)

BIS 存储库包含多种类型的元素。

PhysicalElements 用于对现实世界中的物理对象进行建模。

RoleElements 用于对对象可能具有的角色或功能进行建模。

InformationContentElements 用于对纯信息进行建模。

BIS 定义了一组 InformationContentElement 子类，以进一步分类和专业化不同类型信息的行为。

## 关键信息元素类 (Key Information Element Classes)

![关键信息类](https://www.itwinjs.org/media/information-element-classes.png)

### InformationContentElement

InformationContentElement 是用于建模纯信息实体的抽象基类。

只有核心框架应该直接从 InformationContentElement 子类化。

域和应用程序开发人员应该从 InformationContentElement 最合适的子类开始。

### InformationRecordElement

InformationRecordElement 是用于建模信息记录的抽象基类。

如果没有其他 InformationContentElement 子类合适，InformationRecordElement 是默认选择。

例如，导入电子表格可能会导致创建 InformationRecordElements。

InformationRecordElement 通常由 InformationRecordModel 包含。

### DefinitionElement

DefinitionElement 保存旨在共享的配置相关信息。

DefinitionElement 子类包括：

- Category（类别）
- SubCategory（子类别）
- RenderMaterial（渲染材质）
- PhysicalMaterial（物理材质）
- AnnotationTextStyle（注释文本样式）
- LineStyle（线型）
- Texture（纹理）
- ModelSelector（模型选择器）
- CategorySelector（类别选择器）
- DisplayStyle（显示样式）
- ViewDefinition（视图定义）
- GeometryPart（几何部件）

DefinitionElement 始终由 DefinitionModel 包含。

DefinitionModel 可用于收集相关的定义。

使用示例：

- 每个"目录"一个 DefinitionModel，其中每个 DefinitionModel 与一个目录相关联，并包含每个目录条目的 DefinitionElement。
- 用户可以创建一个 DefinitionModel 来收集项目标准（样式、类别等）。
- 开发人员可以创建一个私有的 DefinitionModel 来保存应用程序或域定义及配置设置。

旨在让任何写入 iModel 的逻辑可发现的 DefinitionElement 实例需要按照 Organizing Repository-Global Definition Elements（组织存储库全局定义元素）中指定的指南进行组织。

### InformationPartitionElement

InformationPartitionElement 是元素的抽象基类，这些元素表示在整个存储库信息层次结构中存在新的建模视角。

InformationPartitionElement 始终以 Subject 为父级，并由 Model 进行分解。

InformationPartitionElement 始终由 RepositoryModel 包含。

有关更多详细信息，请参阅 Information Hierarchy（信息层次结构）。

### InformationReferenceElement

InformationReferenceElement 是用于建模实体的抽象基类，其主要目的是引用其他内容。

例如，任何类型的超链接或分组类型的信息。

InformationReferenceElement 子类包括：

- GroupInformationElement
- LinkElement
- Subject

#### GroupInformationElement

GroupInformationElement 是用于建模实体的抽象基类，其主要目的是引用一组相关元素。

例如，DgnV8 命名组被映射到 GroupInformationElement 的子类。

#### LinkElement

LinkElement 是用于建模超链接的抽象基类。

LinkElement 基类包括：

- UrlLink
- RepositoryLink
- EmbeddedFileLink

#### Subject

Subject 是用于标识存储库所涉及内容的元素。

Subject 是对这些外部事物的逻辑引用。

有关更多详细信息，请参阅 Information Hierarchy（信息层次结构）。

### Document

Document 是旨在作为一个整体被理解的信息集合。

Document 子类包括：

- Drawing（图纸）
- Sheet（图页）

## 特定信息元素的典型模型 (Typical Models for Specific Information Elements)

下表列出了通常包含 InformationContentElements 特定子类的 Model 类型：

| Element Class | Model Class |
| --- | --- |
| InformationRecordElement | InformationRecordModel |
| DefinitionElement | DefinitionModel |
| InformationPartitionElement | RepositoryModel |
| InformationReferenceElement | LinkModel 或其他 InformationModel |
| GroupInformationElement | GroupInformationModel |
| Document | DocumentListModel |

---

| 下一篇: Schema Customization
|:---|
