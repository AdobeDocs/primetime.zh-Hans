---
title: 常规使用情况报表
description: 常规使用情况报表
exl-id: 1272073a-61fe-47ec-aced-2e8055b6b11e
source-git-commit: a2181a8fd7334f19b8387a31c71527d4f689ab9d
workflow-type: tm+mt
source-wordcount: '1281'
ht-degree: 0%

---

# 常规使用情况报表 {#general-usage-reports}

帐户IQ报表是基本的分析工具和报表，可让您深入分析数据以隔离 [同类群](/help/AccountIQ/product-concepts.md#segmet-def)、识别异常，并了解您的帐户特征。

“一般使用情况报表”页面提供了根据使用的帐户设备数、检测到的IP和相应的邮政编码划分子组量度的工具。

<!--Divide the content in cohorts.

Content filters
device filters

segment and definition replicate to cohorts. Number of people and number of account that ......
content consumption.....-->

所有报表均基于使用 [区段和期限](/help/AccountIQ/howto-select-segment-timeframe.md) 的上界。 您可以通过在 [快照概述 — 超过阈值的帐户](#snapshot-overview) 的上界。

<!--To view General Usage Reports:

1. Select the desired MVPDs from the **MVPDs in Segment** option.

2. Select the desired programmer channels from the **Channels in Segment** Option.

3. Select an appropriate time frame from the **Granularity and time frame** option.

   Using the above options you have defined segments for your analysis. Based on your segment selection, following graphs and reports are displayed.

4. You can fine tune your selection and further narrow it down by specifying (number of devices, number of IPs, and number of zip codes) thresholds in [Snapshot Overview - Accounts above thresholds](#snapshot-overview) widget/panel.-->

## AuthN OK / AuthZ OK / Play请求/唯一订阅者 {#authn-authz-playreq-uniquesubs}

此处的折线图可让您查看在定义的区段的选定时间范围内AuthN OK、AuthZ OK、Play Requests和Unique Subscribers值随时间的变化。

+++程序员 —  **AuthN OK / AuthZ OK / Play请求/唯一订阅者**

![](assets/progr-line-graph-gu.png)


*图：针对程序员用户的AuthN OK / AuthZ OK / Play请求/唯一订阅者*


+++


+++MVPD- **AuthN OK / AuthZ OK /唯一订阅者**

![](assets/mvpd-line-graph-gu.png)


*图：MVPD用户的AuthN OK / AuthZ OK /唯一订阅者*


+++

x轴显示当前时间范围内的单位，y轴表示该时段内的基本订阅者活动量度。 利用折线图，可比较MVPD订阅者和您在区段选择面板中选择的渠道的以下值：

* **AuthN OK**

   AuthN OK是成功身份验证的次数。 有关更多信息和定义，请参阅 [产品概念：AuthN OK](/help/AccountIQ/product-concepts.md#authn-ok-def).

* **AuthZ OK**

   AuthZ OK是成功授权的数量。 有关更多信息和定义，请参阅 [产品概念：AuthZ OK](/help/AccountIQ/product-concepts.md#authz-ok-def).

* **播放请求**

   播放请求是播放请求的数量。 有关更多信息和定义，请参阅 [产品概念：播放请求](/help/AccountIQ/product-concepts.md#play-requests-def)

   >[!NOTE]
   >
   >播放请求折线图不适用于MVPD用户。


* **独特订阅者**

   独特订阅者是成功独特订阅者的数量。 有关更多信息和定义，请参阅 [产品概念：独特订阅者](/help/AccountIQ/product-concepts.md#unique-subscriber-def)

   >[!NOTE]
   >
   >如果程序员使用AdobeTempPass（免费预览）是区段的一部分，则独特订阅者总数还包括独特设备数。

## 快照概述 — 超过阈值的帐户 {#snapshot-overview}

使用此附加过滤器微调您的分析和报表，以设置各种使用阈值。 在通过选择所需的MVPD和渠道来定义区段（或同类群组）以进行分析后，您还可以使用以下过滤器来分析订阅者行为：

* 设备数量阈值

* IP阈值数

* 邮政编码阈值数

当您在 [帐户区段 — 基于选定的阈值](#account-segments-basedon-segments) 面板中，您可以在中查看影响：

* [每个帐户每周（或每月）的设备数](#devices-week-account)

* [每个帐户的每周（或月）位置](#locations-week-account)

* [每个帐户的每周（或月）IP数](#ip-week-account)

* [帐户区段的历史视图](#account-segment-historical-view)

>[!NOTE]
>
>每个阈值的默认值为4。 这意味着，“一般使用情况”页面会显示MVPD的分析，该MVPD的订阅者使用四台（及四台以上）设备，从四个（及更多）不同的地理位置和四个（及更多）不同的邮政编码获取内容。

### 帐户区段 — 基于选定的阈值 {#account-segments-basedon-segments}

的 **帐户区段 — 基于选定的阈值** 面板为您提供了设置设备数量、IP数量和邮政编码数量阈值（介于1到10之间）的选项。

该图表显示：

* 订户帐户的绝对数，以及

* 占该段用户帐户总数的百分比，

   使用X个设备数、Y个IP数和Z个邮政编码，以在某个时间范围内从您的渠道中为（定义的）MVPD使用内容。

![](assets/select-thresholds.png)

## 每个帐户每周（或每月）的设备数 {#devices-week-account}

的 **条形图** 根据订阅者如何使用其设备访问内容，提供使用行为的分析。

x轴绘制“帐户数”，y轴绘制“设备数”。 根据您为每个帐户的设备数量设置的阈值，它将标记在一周的持续时间内从特定数量的设备消费内容的订阅者帐户的绝对数量。

![](assets/bar-gr-devices-w-acc.png)

将鼠标悬停在条形（特定于设备数量）上时，会显示一个标签，用于提供有关每周使用这些许多设备来流式传输渠道内容的订户帐户数量（以及区段中订户帐户总数的百分比）的信息。

该图表还标记以下内容：

* 用于标记您设置的阈值的红线。

* 用于标记用户帐户每周（或月）使用的不同设备平均数的绿线。

您可以将阈值级别与帐户使用的不同设备的每周平均数量进行比较，以判断共享级别。

此图还粗略介绍了使用的设备数量多于设置阈值的用户帐户百分比。

圆环图可帮助您一目了然地判断使用超过设置阈值（在一个时间范围内）的设备消费渠道内容的订户帐户的数量。

![](assets/donut-devices-w-acc.png)

## 每个帐户的每周（或月）位置 {#locations-week-account}

赞 [每个帐户每周（或每月）的设备数](#devices-week-account)，每周（或每月）每帐户位置量度可帮助您分析不同位置的订阅者帐户使用情况，从而更加紧密地识别密码共享。 x轴绘制“帐户数”，y轴绘制“位置数”。

此量度的结果与数量 [每个帐户每周（或每月）的设备数](#devices-week-account) 和数量 [每个帐户的每周（或月）IP数](#ip-week-account) 帮助您更准确地判断密码共享实例；这样，真正的用户就不会被计入其中。

![](assets/graph-loc-week-acc.png)

定义区段并设置位置数的阈值后，即可从图表中识别：

* 每周从（特定）x个位置访问内容的订阅者数量（和百分比）。

* 从超过阈值的位置查看内容的订阅者帐户总数的百分比。

* 将每周平均值（帐户不同位置的数量）与阈值进行比较。

## 每个帐户的每周（或月）IP数 {#ip-week-account}

类似于 [每个帐户每周（或每月）的设备数](#devices-week-account) 和 [每个帐户的每周（或月）位置](#locations-week-account), **每个帐户每周的IP数** 量度可让您更精确、更粒度地分析密码共享。

x轴绘制“帐户数”，y轴绘制“IP数”。

![](assets/graph-ip-week-acc.png)

定义区段（通过选择MVPD和渠道）并设置IP数量的阈值后，即可从图表中识别：

* 一周内从（特定）x个IP数量消费内容的订阅者数量（和百分比）。

* 从超过阈值的IP地址查看内容的订阅者帐户总数的百分比。

* 将每周平均值（帐户的不同IP数）与阈值进行比较。

## 帐户区段 — 历史视图 {#account-segment-historical-view}

历史视图条形图可帮助您比较不同时间范围内的使用量度。 此外，它还会合并标绘各种使用量度，例如 [每个帐户每周（或每月）的设备数](#devices-week-account), [每个帐户的每周（或月）位置](#locations-week-account)和 [每个帐户的每周（或月）IP数](#ip-week-account).

* x轴绘制时间范围，y轴绘制订户帐户、设备、位置和IP的数量。

* 橙色色条表示各个时间范围内的区段。

* 折线图绘制 [每个帐户每周（或每月）的设备数](#devices-week-account), [每个帐户的每周（或月）位置](#locations-week-account)和 [每个帐户的每周（或月）IP数](#ip-week-account) 值。

![](assets/historical-view.png)

* 蓝色条表示某个时间范围内整个行业的活动订阅者总数。

* 您可以选择特定图例，这些图例有助于您缩放图表。

![](assets/historical-view-total.png)

>[!MORELIKETHIS]
>
>* 了解如何使用“一般使用情况报表”中的过滤器导出选定区段中前1000个订阅者的报表 [导出前1000个帐户](/help/AccountIQ/export-acc-information.md) 选项。

