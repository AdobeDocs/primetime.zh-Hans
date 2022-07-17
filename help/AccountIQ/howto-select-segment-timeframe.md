---
title: 定义区段和时间范围
description: 定义区段和时间范围
source-git-commit: a23de698b073d271df9b04494ff59f5d5a194c9d
workflow-type: tm+mt
source-wordcount: '579'
ht-degree: 0%

---

# 定义区段和时间范围 {#define-segment}

在帐户IQ中查看或分析报表时，首先要定义区段并选择评估的时间范围。 [区段](/help/AccountIQ/product-concepts.md#segmet-def) 是指符合您的评估标准（订阅MVPD并查看特定渠道）的所有订阅者或查看者。

![](assets/segment-panel.png)

*图：区段和时间范围选择*

在帐户IQ中所有报表页面的顶部，有一个面板，可通过选择MVPD、渠道程序员、粒度和时间范围来定义区段。

## 区段选择 {#select-segment}

### 在区段中选择MVPD {#select-segment-mvpds}

从中选择MVPD **区段中的MVPD** 选项：

1. 单击或点按 **区段中的MVPD** 下拉选项。

   >[!NOTE]
   >
   >**全部** 默认情况下会选择行业MVPD。 从此处，您可以选择 **按共享分数排名前10个MVPD**, **按使用情况列出的前10个MVPD**, **前10个按帐户划分的MVPD**，或单个MVPD。 但是，要选择单个MVPD，您需要取消选择 **全部**.

1. 单击或点按所需的MVPD。

   您可以通过取消选择某个MVPD来从选定范围中删除该MVPD。

1. 单击或点按 **应用选择** 才能让您的选择生效。 否则，您将放弃所做的选择。

   >[!NOTE]
   >
   >如果选择隔离模式，则无法选择任何其他MVPD。

### 在区段中选择渠道 {#select-segment-channels}

从 **区段中的渠道** 选项：

1. 单击或点按 **区段中的渠道** 下拉选项。

   >[!NOTE]
   >
   >**全部** 默认情况下，会选择您公司的程序员渠道。 要选择单个渠道或程序员，您必须先取消选择 **全部**.

1. 单击或点按所需的渠道或程序员。

   中的顶级列表项 **区段中的渠道** are [程序员](/help/AccountIQ/product-concepts.md#programmer-def) 公司和程序员名下的清单是他们的 [渠道](/help/AccountIQ/product-concepts.md#channel-def). 您可以在程序员下选择单个渠道，也可以选择程序员，并且该程序员下渠道的所有活动都包含在报表和图表结果中。

   ![](assets/programmer-channels.png)

   *图：渠道选择器中列出的程序员和渠道*

   >[!IMPORTANT]
   >
   >在程序员下选择单个渠道的结果与选择程序员的结果不同。
   >
   >
   >当您选择单个渠道时，这些渠道的活动会在某些报表中单独进行划分。 但是，当您选择所有这些渠道的父程序员时，这些渠道的所有活动都将包含在报表中，但不会在报表中单独进行划分。

1. 单击或点按 **应用选择** 才能让您的选择生效。

>[!NOTE]
>
>在MVPD或程序员下拉菜单中，您不能选择10个以上的项目。

### 取消选择MVPD和渠道 {#deselect-segment-mvpds-channels}

除了在 **区段中的MVPD** 和 **区段中的渠道** 区段选择器中，您可以通过以下方式取消选择之前选择的MVPD和渠道：

* 选择 **删除** 图标(![删除图标](assets/remove-icon.png))的名称以及区段选择器下方显示的渠道。

* 您还可以使用 **清除选择** 删除之前选择的所有MVPD或频道。

![](assets/segment-panel-selection1.png)

*图：区段和时间范围面板中的选定MVPD和渠道*

![](assets/segment-panel-selection.png)

*图：区段和时间范围面板中的选定MVPD和渠道*

## 粒度和时间范围选择 {#granularity-timeframe}

要选择评估的时间段，请执行以下操作：

1. 选择 **粒度和时间范围** 日期选取器。

1. 选择 **周** 或 **月** 从 **聚合方式** 选项来设置评估的粒度。

   ![](assets/granularity-timeframe-weekwise.png)

   *图：用于选择粒度和时间范围的日期选取器*

1. 选择粒度后，可以使用向前或向后箭头及时向前或向后移动。

1. 指定过去的时间段（基于所选粒度的月或周）以进行评估。

1. 选择 **应用选择** 以确保您的选择生效。
