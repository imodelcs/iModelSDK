# BIS Glossary (BIS 术语表)

> 原文: [BIS Glossary](https://www.itwinjs.org/bis/guide/references/glossary/)
>
> 最后更新: 2025年6月11日

本文档定义了 BIS 文档中使用的关键术语。

| 术语 | 描述 |
|------|------|
| **BIS Repository** | 具有由 BIS 定义的语义和结构的信息存储库。[iModels](#imodel) 是 BIS Repository 的一种实现。 |
| **BIS** | Base Infrastructure Schemas。用于建模建筑基础设施（如建筑物、道路、桥梁、工厂等）的协调 schema 系列。BIS 还解决了基础设施相关工作流所需的概念（如文档、图纸、需求、问题等）。 |
| **BisCore** | BIS 的基础域。任何其他域中的所有 ECClass 都必须（直接或间接）从 BisCore 类派生。 |
| **Category** | GeometricElement 的一个属性，用于对其几何图形进行"分类"。每个 GeometricElement 被分配到一个且仅一个 Category。每个视图中可以控制 Category 的可见性（开/关）。Category 类似于 DGN 中的*层（levels）*、DWG 中的*图层（layers）*和 RVT 中的*类别（categories）*。 |
| **Class** | 参见 [ECClass](#ecclass)。 |
| **Code** | Entity 的文本标识符，编码了有关 Entity 的一些信息，个人可以解码和理解。在 BIS 中，Code 使用 *bis:Element* 的三个属性建模：CodeValue、CodeSpec 和 CodeScope。参见 [Codes](../fundamentals/codes.md)。 |
| **CodeScope Property** | Element 的导航属性，指向一个 Element，该 Element 指示 CodeValue 的*唯一性范围*。参见 [Codes](../fundamentals/codes.md)。 |
| **CodeSpec** | "Code Specification"，指定 Code 如何编码和解码。参见 [Codes](../fundamentals/codes.md)。 |
| **CodeSpec Property** | Element 的导航属性，指向一个 [CodeSpec](#codespec)，指定 Code 如何编码和解码。参见 [Codes](../fundamentals/codes.md)。 |
| **CodeValue Property** | Element 的可空字符串属性，包含 Element 表示的 [Entity](#entity) 的人类可读标识符。参见 [Codes](../fundamentals/codes.md)。 |
| **DefinitionElement** | InformationContentElement 的子类，包含帮助*定义*其他 Elements 的信息，旨在被多个 Elements 引用（即共享）。 |
| **DictionaryModel** | 存储库全局 `DefinitionElement` 实例的特殊模型。每个 BIS Repository 有且仅有一个 DictionaryModel。可以通过代码为 'BisCore.DictionaryModel' 的 `DefinitionPartition` 访问，该 Partition 始终作为 iModel 根 `Subject` 的子元素创建。 |
| **Digital Twin** | 现实世界某部分的数字表示。Digital Twin 应设计为可供多个应用程序使用（与应用程序特定的"孤岛"数据库形成对比）。完整的 Digital Twin 通常是来自多个存储库的数据联邦（例如 BIS Repository 如 iModel，加上 Reality Data 服务、IoT 数据服务、资产生命周期信息管理服务等）。 |
| **Domain** | 定义特定学科或工作领域信息的一组命名 ECClass。域中的所有类最终必须从 BisCore 类派生。域的 ECClass 在 ECSchema 文件中定义，因此术语*域*和*ECSchema*通常可以互换使用。参见 [Domain Schemas](../../domains/)。 |
| **DrawingModel** | 包含图纸图形的 2D 模型。DrawingModel 可以是尺寸标注的或非尺寸标注的。 |
| **EC** | *Entity Classification* 的缩写。此前缀用于指代 BIS 的元数据系统。 |
| **ECClass** | 定义对象类型的命名属性和关系集。BIS Repository 中的数据由 ECClass 定义。 |
| **ECProperty** | ECClass 的命名成员。 |
| **ECRelationship** | ECClass 实例之间的命名关系类型和基数。 |
| **ECSchema** | ECClass 和 ECRelationship 的命名组。 |
| **Element** | BIS 存储库中用于建模 Entity 的最抽象类和最小可单独识别的构建块。可以有对应于不同建模视角的 Element 子类。多个 Elements 可以关联在一起以建模 Object 的不同视角。 |
| **ElementAspect** | 向单个 Element 添加属性和/或关系以添加更多详细信息的 BIS 类。例如，ElementAspect 可用于记录仅在特定情况下或 Element 生命周期的某些阶段才需要的信息。ElementAspect *归属于*其拥有的 Element，并随拥有它的 Element 一起删除。 |
| **ElementId** | BIS Repository 中 Element 的 64 位唯一 Id。对于 iModel，ElementId 通过组合 24 位 BriefcaseId 和 40 位顺序分配的值来分配。 |
| **ElementOwnsChildElements** | 将 Element 与*子*Elements 关联，这些子 Elements 表示父 Element 建模的 [Entity](#entity) 的*部分*。Element 子类可以允许使用子 Elements 建模其部分，或者允许使用另一个 Model 的 ModelModelsElement 关系来表达部分的详细模型，但不能两者兼有。 |
| **Entity** | 在给定上下文和建模视角中相关的任何语义处理的*Object*或其部分的泛化。 |
| **FederationGuid** | Element 建模的 [Entity](#entity) 的可选 128 位 [全局唯一标识符](https://en.wikipedia.org/wiki/Universally_unique_identifier)。通常，FederationGuid 由外部系统分配，用于将 Elements *联合*到其外部含义。在 BIS Repository 内，FederationGuid 必须唯一，因此可用作 Element 的次要标识符（当存在时）。 |
| **GeometricElement** | *bis:Element* 和抽象基类，用于建模本质上具有几何图形的 Entity。 |
| **GeometricModel** | Model 的子类，可以包含 GeometricElements。 |
| **GeometryPart** | 可以由许多 GeometricElements 共享的命名 GeometryStream。 |
| **GeometryStream** | 描述 GeometricElement 几何属性的几何基元集合。GeometryStream 的各个成员可以在不同的 [SubCategory](#subcategory) 中，并且可以引用 GeometryParts。 |
| **Granularity** | Model 中 Elements 的比例或细节级别。 |
| **iModel** | 使用 [SQLite](https://www.sqlite.org) 和 iModelHub 作为分布式数据库实现的 BIS Repository。[iModels](/learning/imodels/) 是最常见的 BIS Repository。一个 iModel 的多个副本可能同时存在，每个副本保存在 Briefcase 中并通过 iModelHub 的 ChangeSets 同步。 |
| **InformationPartitionElement** | RepositoryModel 中的 Element，标识从 Partition 的建模视角建模 Subject 的 BIS Repository 部分。Partition 必须是 Subject 的子元素，Subject 可以有多个专门的 Partition Elements（如 PhysicalPartition、FunctionalPartition）作为子元素。 |
| **Model** | 用于更详细描述另一个 Element（其 *ModeledElement*）的 Elements 集合。每个 Element 通过 ModelContainsElements 关系*包含在*一个且仅一个 Model 中。以这种方式，Models 形成 Elements 的层次结构。有许多 Model 子类（如 PhysicalModel、FunctionalModel 等）。 |
| **ModelContainsElements** | 强制每个 Element 恰好属于一个 Model 的关系。 |
| **ModeledElement** | 被 Model *子建模*或*更详细分解*的 Element。注意，Model 的*名称***是**其 ModeledElement 的名称，Model 的 *ParentModel***是**其 ModeledElement 的 Model。ModeledElement 混入 `ISubModeledElement`，也可以称为 "SubModeledElement"。 |
| **Modeling Perspective** | "查看"或"思考" Object 的方式，例如功能、物理、空间、财务等。 |
| **ModelModelsElement** | 将 Model 与 Element 关联的关系，该 Model 更详细地建模该 Element。换句话说，Model 将较粗粒度的 Element 分解为由较细粒度 Elements 组成的更详细的子 Model。此关系允许 BIS 在同一 BIS Repository 内以多种粒度一致地建模现实。 |
| **Object** | 事物、过程或信息在自然界中出现的形式。不用于指代 ECClass 实例或其他建模构造。 |
| **Perspective** | 参见 [Modeling Perspective](#modeling-perspective)。 |
| **PhysicalModel** | `SpatialModel` 的子类，用于物理视角，包含 `PhysicalElement` 和 `SpatialLocationElement`。 |
| **Relationship** | 参见 [ECRelationship](#ecrelationship)。 |
| **RepositoryModel** | 特殊的 Model，是 BIS Repository 中 Models 层次结构的根。每个 BIS Repository 有且仅有一个 RepositoryModel，它是唯一没有 ModelModelsElement 关系指向另一个 Element 的 Model。 |
| **RoleElement** | *bis:Element* 和抽象基类，用于建模由 Entity 承担的角色，这些角色不是 Entity 本身固有的。 |
| **Schema** | 参见 [ECSchema](#ecschema)。 |
| **SheetModel** | *一张纸*的数字表示。Sheet Models 是有界纸张坐标中的 2D 模型。SheetModels 可以包含注释 Elements 以及对 2D 或 3D 视图的引用。 |
| **Spatial Coordinate System** | BIS Repository 的 3D 坐标系。单位始终是米（参见 ACS）。空间坐标系的原点 (0,0,0) 可以通过 [EcefLocation](https://en.wikipedia.org/wiki/ECEF) 在地球上定位。 |
| **SpatialModel** | GeometricModel 的子类，包含 BIS Repository 空间坐标系中的 3D Elements。 |
| **SpatialViewDefinition** | ViewDefinition 的子类，显示一个或多个 SpatialModels。 |
| **SubCategory** | [Category](#category) 的细分。SubCategories 允许 GeometricElements 拥有多个可以独立可见和样式化的几何片段。重要的是要理解 SubCategory **不是** Category（即 Categories *不*嵌套），并且 SubCategory 始终细分单个 Category。 |
| **Subject, Root** | RepositoryModel 中的主要 Subject，以文本形式命名或简要描述存储库建模的现实世界 Object。存储库中始终有且仅有一个根 Subject。根 Subject 及其子 Subject 有效地形成存储库的*目录*。 |
| **Subject** | RepositoryModel 中的 Element，以文本形式命名或简要描述存储库建模的重要现实世界 Object。每个 Subject 要么是根 Subject，要么是另一个 Subject 的子元素。 |
| **ViewDefinition** | `DefinitionElement` 的子类，保存 View 的持久状态。 |
