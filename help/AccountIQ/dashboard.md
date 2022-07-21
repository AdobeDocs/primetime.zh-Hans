---
title: 帐户IQ功能板
description: 功能板通过分析大量订阅者数据来帮助实现密码共享实例的精准定位。
exl-id: 616da2a5-c9fe-40ea-90cf-f565bc13e764
source-git-commit: 8e041e6bb3b0f607eb421be002904e3a8a447f52
workflow-type: tm+mt
source-wordcount: '499'
ht-degree: 0%

---

# 功能板 {#dashboard}

功能板汇总和汇总了一组图表和报表中的数据，这些图表和报表旨在对帐户共享的范围和影响进行高级概述。 它提供了一个页面，其中包含来自帐户IQ的主要报表和量度。

![帐户IQ仪表板](assets/dashboard-capture.png)

## 平均共享分数 — 当前区段的汇总 {#aggregated-sharing}

“汇总共享分数”面板提供了一个顶行读出，用于总结在帐户和流量方面共享的数量和影响。

这些值有助于您了解订阅者共享凭据的规模，从而可以衡量是否需要对其执行操作。

![](assets/aggregate-sharing-score.png)

![](assets/aggregate-sharing-score.svg)

以下三个量度是“聚合共享得分”的组件。

### 共享级别 {#sharing-level}

共享级别量规显示选定时间范围内共享的所有订阅者帐户（在定义的区段中）的百分比。

根据在所选时间范围内从一个所选程序员频道流传输的一组所选MVPD中每个帐户的共享概率的平均值计算的值。

![](assets/sharing-level.png)

趋势指示器显示中量度值与上一时间范围相比的百分比变化。

### 从共享帐户使用 {#usage-from-shared-accounts}

此量规指示所有订阅者帐户的使用百分比是来自定义区段和时间段的共享帐户。 该量规将使用范围（从共享帐户）标记为0到100%。 这些范围（称为“低”、“中”、“高”和“异常”）均基于行业平均值。

您还可以看到趋势指示器，该指示器显示与上一个时间范围相比，来自共享帐户的使用情况增加或减少。

![](assets/usage-4mshared-accounts.png)

### 总体共享分数 {#overall-sharing-score}

整体共享分数是共享分数的组合，包括“共享级别”和“从共享帐户使用z”。

与行业相比，它提供的价值旨在反映共享的相对影响。 其用途与信用评分类似，用单个数字概述情况。 但在这种情况下，数字越高，潜在危害就越大。

![](assets/overall-sharing-score.png)

<!--### MVPDs in segment {#mvpd-in-segment}

It is a table of risk indices and accounts totals for the top MVPDs ranked by overall usage or account sharing.

![](assets/mvpds-in-segment.png)-->

### 全行业MVPD整体共享分数 {#top-mvpds}

此表提供了区段中MVPD的不同汇总共享得分的比较视图。

>[!NOTE]
>
>此表将整体行业数据用于比较目的，而不是区段中由这些MVPD表示的数据。

![](assets/top-mvpds.png)

### 按渠道和MVPD共享分数 {#sharin-score-by-channels-and-mvpds}

此表提供了在当前区段中为MVPD共享所选渠道分数的比较视图。

![](assets/sharing-scores-by-channels-mvpds.png)

### 帐户共享概率 {#accounts-sharing-probability}

此图表将分为几类：分享概率五倍数的范围，从非常低(0-20%)到非常高(80=100%)。

>[!NOTE]
>
>条形图使用对数刻度。


![](assets/dashboard-ac-sharing-prob.png)

### 通过共享概率级别确定的帐户数量和使用情况 {#number-of-accounts-usage-sharing-probability}

此面板提供了表格视图，其中将帐户划分为从非常低(0-20%)到非常高(80=100%)的共享概率五分位数范围，每个五分位数的共享帐户相关使用情况。

![](assets/no-acc-usage-prob-level.png)
