---
title: 在用户区段上创建操作并跟踪效果
description: 如何创建对定义的用户区段产生影响和跟踪影响的操作。
exl-id: ab74f857-e178-4120-8f9c-655ec921d096
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '1007'
ht-degree: 0%

---

# 在用户区段上创建操作 {#operation-to-track-segment}

帐户IQ上的每个报表页面都有一个 **创建新操作** 选项帮助您创建工作流以自动化（和简化）订阅者帐户的各种（批量）操作；定义规则以指定示例、定义操作并记录和分析这些操作的影响。 在要创建操作的页面上，您可以定义将在其中执行操作的用户组示例，并安排在将来的日期运行操作。

要创建操作，请执行以下操作：

1. 使用中的步骤，定义您的区段（同类群组），以在任何报告或功能板页面上进行分析 [定义区段和时间范围](/help/AccountIQ/howto-select-segment-timeframe.md).

1. 选择 **创建新操作** 选项在任意报告或仪表板页面上可用。 此 **创建新操作** 页面。

   ![用于创建新操作的页面](assets/create-new-operations.png)
   *图：用于创建新操作的页面*

1. 在 **创建新操作** 页面，在表单字段中填写以下项目的详细信息：

   * [操作名称](#operation-details) 操作详细信息
   * 要在下运行操作的区段 [目标区段](#segment) 并使用优化区段 [其他分段](#additional-segmentation)
   * [区段类型](#segment-type) 下 [目标区段](#segment)
   * [操作](#action)
   * [计划激活](#schedule)

1. [保存操作](#save-operation).

## 操作详细信息 {#operation-details}

+++程序员 — 操作详细信息

将新操作命名为 **操作名称** “操作详细信息”下的字段。 例如，“*测试多重身份验证对MVPD X的订阅者的影响”或“限制并发监视中的流数量”或“限制MVPD D的订阅者查看来自20个以上设备的频道“N”*“。

+++

+++MVPD — 操作详细信息

将新操作命名为 **操作名称** “操作详细信息”下的字段。 例如，“*测试多重身份验证对频道N的查看器的影响”或“限制并发监控中的流数量”或“限制查看频道“N”的订阅者从20台以上的设备访问*“。

+++

## 目标区段 {#segment}

+++程序员 — 目标区段

此 **区段** 此处定义将由此操作操作的用户；或操作的示例组。 默认区段为 **区段** 您使用以下方式选择 [区段和时间范围面板](/help/AccountIQ/howto-select-segment-timeframe.md) ，位于上面步骤1中的主报表或功能板页面上。

<!--* The first segment entry in the **Segment** section, by default, shows the **segment** you selected in the step 1.

* The **segment evaluation period** is the time period of analysis you selected in step 1 from **Granularity and Timeframe** option.
![](assets/operations-segment-selection.png)
*Figure: Segment and timeframe selection on the main page*-->

此区段定义将受到所创建操作影响的订阅者。 例如，您选择的区段可能指定 *名为“C”的MVPD的所有订阅者帐户，他们查看频道“N Sports”*.

+++

+++MVPD — 目标区段

此 **区段** 此处定义将由此操作操作的用户；或操作的示例组。 默认区段为 **区段** 您使用以下方式选择 [区段和时间范围面板](/help/AccountIQ/howto-select-segment-timeframe.md) ，位于上面步骤1中的主报表或功能板页面上。

<!--* The first segment entry in the **Segment** section, by default, shows the **segment** you selected in the step 1.

* The **segment evaluation period** is the time period of analysis you selected in step 1 from **Granularity and Timeframe** option.
![](assets/operations-segment-selection.png)
*Figure: Segment and timeframe selection on the main page*-->

此区段定义将受到所创建操作影响的订阅者（特定渠道的查看者）。 例如，您的（默认）区段包括 *查看频道“N Sports”的所有订户帐户*.
+++

### 其他分段 {#additional-segmentation}

此外，您还可以通过添加更多量度来优化目标区段。 例如，您可以添加大于90%的共享概率作为另一个量度。 所以，现在的问题陈述是 *“为名为‘C’的MVPD的订阅者帐户创建一个操作，这些订阅者正在查看共享概率大于90%的频道‘N Sports’”*.

![](assets/additional-segment.gif)

*图：其他分段*

此外，如果您通过添加另一个设备数量指标来优化操作，则更新的问题语句将如下所示 *“为名为‘C’的MVPD订阅者帐户创建一个操作，这些订阅者正在查看共享得分高于90且使用5台以上设备在评估期间查看内容的频道‘N Sports’”*.

![](assets/refined-segment.png)

*图：使用总体共享分数和设备数量指标优化示例区段*

这样，用户组将变得更加精细。 因此，通过添加更多量度和条件，您可以进一步限定该区段以定义要运营的帐户。

### 区段类型 {#segment-type}

区段类型是指在整个运营评估期间处理区段的方式。

![](assets/segment-type.png)

*图：使用区段类型细化要操作的区段数*

<!--The segment type option allows you to further refine your segment based on the evaluation period (or time).

**Fixed number of accounts** 

When you select **Fixed number of accounts** segment type, then you need to specify an evaluation period as well.

By doing so, you are fixing the sample size for evaluation in terms of numbers. You are making Account IQ identify a specific set of users (that meet the criteria of defined evaluation period and segment metrics) to operate on. The analysis and graphs will be generated for this specific set of users only (identified initially) throughout the operation.

**Variable number of accounts**

When you select **Variable number of accounts** segment type, you do not limit the number of accounts in segment. The accounts which fall under the defined segment metrics are the part of the segment, and the number of accounts will change continuously during the course of operation.-->

>[!IMPORTANT]
>
>您只能使用 **固定帐户数** 选项，从现在开始。 要选择的选项 **帐户的可变数量** 将在即将发布的版本中提供。

<!--

you tell Account IQ in the beginning of the operation which number of accounts to operate on.

Account IQ system only has a segment definition, and during the operation it looks into all the accounts that fit that segments.

the number of accounts in segment is not limited, the accounts that fall under defined segment metrics will be part of the segment, and the no of accounts will change continuously, as there are no specific limitations - like an evaluation period in the past.When the segment is defined (which in this example is, subscriber accounts of MVPD 'C' who are viewing the channel 'N Sports' that have a sharing score above 80 and are using 10 different IPs) and we also identified a time period to evaluate a segment. This identifies X number of accounts as sample (for example 5000). How many devices they are using?
It identifies x-number of accounts (5000)...a very specific set of users that meet this criteria.
for every period that we schedule (within that operation) during that operation) we will look at those 5K users that are originally identified and we will present graph about them. How are the sharing scores coming up?u We identified a period. Are their sharing scores going up? Are there fewer of them who are meeting this definition?
Fixed versus variable is the way the treated in fixed or variable way.

1. we identified a fixed set of accounts.
2. we evaluate those specific accounts on criteria throughout the operation.

General idea independent of graph is that we will evaluate a set of accounts identified initially, for no of periods during operation and generate graphs against that.
Those are the 5000 users for which I will create graphs for for every period of the operation.

**Variable number of accounts**
We do not identify any initial set of accounts, we just have a segment definition.
Each period during the operation, we go and look into all the accounts that fit that segments.
If it is not a fixed segment, I won't initially evaluate it. I won't have an initial set of 5000. Instead at every period during the evaluation I will evaluate the segment then, and then I will produce graph about the next 3000 users.
the......will vary from period to period.

if not fixed segment, then I won't initially evaluate or have initial set of 5000, instead at every period during an operation and the.-->

## 操作 {#action}

此 **操作** 定义您将对定义的区段执行的操作。

您可以执行两种类型的操作：

* 使用与帐户IQ集成的系统执行的操作；例如 **并发监测** <!--[Concurrency Monitoring](https://tve.helpdocsonline.com/concurrency-monitoring-introduction), or Adobe Target-->.

* 用于创建和处理Account IQ外部且未与Account IQ系统集成的工作流的操作。 例如，渠道程序员“N”向MVPD“C”的所有订阅者发送批量电子邮件的操作。

>[!NOTE]
>
>通过创建操作，您不仅可以指定操作并定义其范围，还可以开始记录这些操作的影响。

## 计划{#schedule}

您可以通过设置开始日期和结束日期来安排操作的激活。

>[!NOTE]
>
>开始日期和结束日期的粒度与您在定义区段时使用的评估粒度相同 **区段和时间范围面板**，步骤1.
>
>
>因此，如果您将粒度选择为“周”，则开始日期和结束日期将按周表示（例如，第14周）；如果您将粒度选择为“月”，则开始日期和结束日期将按月表示。


>[!IMPORTANT]
>
>开始日期必须晚于评估期，同时也要晚于当前日期。 同样，结束日期还必须晚于开始日期和当前日期。

### 保存操作 {#save-operation}

在保存操作时，将显示一个消息屏幕，告知您在此操作中定义的区段也保存以供将来使用。 但是，您需要为此区段命名。

![](assets/save-operation.png)

*图：保存操作并指定区段名称*

>[!NOTE]
>
>最佳实践是，根据您正在执行的操作并结合将执行的区段来命名您的操作。

<!--In future you can select this saved segment when defining a segment for your analysis on the main reports page. Moreover, the saved segment is also listed when you create an operation the next time.

![](assets/saved-segment-operations-page.png)

*Figure: Saved segments in segment selector on Create new operations page* 

>[!IMPORTANT]
>
>When creating an operation, if you select a segment that was previously created then you cannot add new metrics to it and refine it.
>
>Adding new metrics creates a new segment, but you cannot modify an existing segment.-->

创建操作后，该操作将从开始日期运行到您指定的结束日期。

在主页面上可看到已保存操作的详细信息 [操作](/help/AccountIQ/operations.md) 页面。

![](assets/new-operation-created.png)

*图：新创建的操作在主“操作”页面上列出*
