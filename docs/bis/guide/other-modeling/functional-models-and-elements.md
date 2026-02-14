# Functional Models and Elements

> 原文: [Functional Models and Elements - iTwin.js](https://www.itwinjs.org/bis/guide/other-perspectives/functional-models-and-elements/)

## 简介 (Introduction)

功能域 (functional domain) 允许定义代表系统或流程的对象。这些对象定义了系统中对象的需求。例如，一个 Functional Pump（功能泵）具有定义流程所需流体流量的属性。

流程的功能定义通常在项目设计的早期阶段确定。这些对象会出现在设计图纸和数据表中。Functional 对象最终将在 Physical model（物理模型）中创建。物理对象将通过 _fulfills_（实现）关系与功能对象相关联。

![模型层次结构](https://www.itwinjs.org/media/func-phys-graphic.png)

## 功能元素 (Functional Elements)

所有 Functional 类都在 Functional schema（功能模式）中定义，其别名为 `func`。

有两种类型的功能元素：`func:FunctionalBreakdownElement` 和 `func:FunctionalComponentElement`。

这两个类都继承自抽象类 `func.FunctionalElement`。

![类层次结构](https://www.itwinjs.org/media/role-element.png)

FunctionalBreakdownElements 用于在功能模型中定义分解结构。这些元素将其他 FunctionalBreakdownElements 或 FunctionComponentElements 分组。例如，一个 Plant Unit（工厂单元）将包含 Plant Sub-Units（工厂子单元）。一个 Plant Sub-Unit 包含 Equipment（设备）和 Pipeline（管道）。或者一个 BuildingRequirement（建筑需求）包含 BuildingStoryRequirements（楼层需求），而 BuildingStoryRequirements 又包含 SpaceRequirements（空间需求）。

FunctionalComponent 元素用于表示单个工程需求对象。例如，Pumps（泵）、Valves（阀门）。这些类包含定义组件工程需求的属性。

## 功能模型 (FunctionalModels)

`func:FunctionalModel` 类在功能域模式中定义。

FunctionalModels 包含定义系统或流程所需的 FunctionalElements。

通常会有多个 FunctionalModel，但每个都与不同的流程或系统相关联。

目前，Plant（工厂）和 Building（建筑）应用程序会创建功能模型。由于这两个应用程序都将其所有功能对象放入一个模型中，因此还没有需要对 Functional model 进行子类化。

### 功能模型的内容 (Contents of Functional Models)

FunctionalModels 包含 FunctionBreakdownElements 和 FunctionalComponentElements。

这些模型将包含描述系统或流程所需的所有元素。

例如，建筑应用程序通常每栋建筑创建一个 FunctionalModel。

### 模型层次结构中的功能模型 (Functional Models in Model Hierarchy)

在目前的大多数情况下，功能模型对与根主题相关的分区进行建模。

![模型层次结构](https://www.itwinjs.org/media/funcmodelhier.png)

## 示例 (Example)

在 Plant 功能域中，有一整套类用于定义工厂流程的功能需求。包括 Equipment（设备）、Piping（管道）和 Instrument（仪表）功能组件类。还有功能分解类。这些类可能因项目类型而异。发电厂项目有 Units（单元）、Sub-Units（子单元）、Building（建筑）和 Systems（系统）。炼油厂项目有 Units（单元）、Areas（区域）、Services（服务）和 Systems（系统）。工厂应用程序允许用户定义这些功能分解类以满足其需求。此层次结构由分组关系定义。树的顺序在演示规则中定义。Functional Components 可能被分组在多个 Functional Breakdown 层次结构中。例如，一个泵可能同时存在于 S1 子单元和 NSSS 工厂系统中。

Plant 确实有用于管道和仪表回路的功能分解，它们将功能组件分组，并且始终是功能分解层次结构的末端。它们只能通过添加属性进行配置。有许多不可配置的关系将功能组件相互关联，以定义功能模型的布局。**参见下面的类图。有关所用约定的详细信息，请参阅 Class-diagram Conventions（类图约定）。**

![模型层次结构](https://www.itwinjs.org/media/plantfuncmodel.png)

---

| 下一篇: Analysis Models and Elements
|:---|
