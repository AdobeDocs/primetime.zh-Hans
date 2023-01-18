---
title: 导出共享分数较高的帐户的信息
description: 导出共享分数较高的帐户的信息。
exl-id: df41ddd2-fde3-4861-abd4-6e32f0be9ea5
source-git-commit: dcd89849937f4893705423465be4003948739eeb
workflow-type: tm+mt
source-wordcount: '727'
ht-degree: 1%

---

# 导出共享分数较高的帐户的信息 {#export-account-info-high-score}

帐户IQ允许您根据帐户的IQ导出前1000个订阅者帐户的帐户共享详细信息 [共享概率](/help/AccountIQ/product-concepts.md#account-sharing-probability-def). 导出的CSV文件中的数据按 [区段](/help/AccountIQ/product-concepts.md#segment-def)，对于 [指定时间范围](/help/AccountIQ/product-concepts.md#time-frame-def).

可在 [一般使用情况报表](/help/AccountIQ/general-usage-reports.md) 和 [共享帐户报表](/help/AccountIQ/shared-acc-reports.md) 页面。

>[!NOTE]
>
>对于“一般使用情况”和“共享帐户”报表页面，下载的CSV文件中的数字不同。 这是因为“常规使用情况报表”页面具有其他过滤器，供程序员为设备数、IP和邮政编码选择阈值。 因此，从“常规使用情况”报表导出的数据基于应用的附加阈值过滤器。

![常规用法中的导出选项](assets/export.png)

要导出订阅者的帐户共享信息，请执行以下操作：

1. 按照 [如何定义区段和选择时间范围](/help/AccountIQ/howto-select-segment-timeframe.md) 从 [区段和时间范围](/help/AccountIQ/segments-timeframe.md) 的上界。

1. 选择 **导出前1000个帐户** 用于导出共享概率最高的1000个订阅者的帐户信息的选项。

使用导出选项时，将具有最高共享概率（针对定义的时间范围）的1000个帐户的统计信息下载到本地计算机的Downloads文件夹中。

>[!NOTE]
>
>下载的CSV文件可以使用任何读取CSV文件的应用程序(例如Microsoft Excel)打开。

![csv格式的导出数据](assets/exported-csv.png)

*图：以CSV格式导出的共享帐户数据*

## 导出报表中的列 {#columns-in-export}

**周/月**

在 **粒度和时间范围** 区段选择器中的选项，其中需要共享统计信息。

**MVPD**

如果您是程序员用户，则列会显示订阅者帐户所属的MVPD。

**订阅者Id**

我们一直在讨论的特定帐户。

**最少设备数**

实际设备数（该流内容）几乎肯定大于为特定帐户指定的最小设备数。

>[!NOTE]
>
>实际设备数（该流内容）肯定大于为特定帐户指定的最小设备数。

**最低人数**

使用这些设备进行活动流式内容的绝对最小人数。

>[!NOTE]
>
>实际人数（该流内容）几乎肯定比为特定帐户指定的最低人数要多得多。

**# IP数**

从中流式处理内容的IP地址数。

**位置数**

从中流式传输内容的位置数量（基于邮政编码）。

**#城市**

流播放的城市数量。

**#状态**

进行流播放的状态数。

**#群集**

非重复项的数量 [聚类](/help/AccountIQ/product-concepts.md#cluster-def) 流播放的地方。

**地理范围（英里）**

与帐户关联的流位置之间的最大距离。

**# AuthN OK**

用户在该时段内使用该帐户登录的次数。

**#身份验证Z OK**

MVPD授权流或授予（访问内容）该帐户的次数。

**播放请求数**

时间段内的实际流数量。

>[!NOTE]
>
>**#身份验证Z OK** 通常小于 **播放请求数** 因为Adobe会缓存来自MVPD的授权长达24小时。 此列不适用于MVPD。

**#渠道**

帐户在该时间段内已监视的不同渠道的总数。

>[!NOTE]
>
>**#渠道** 包括不一定属于已登录程序员的渠道。
>
>显示该帐户的号码是因为该帐户监视了您的渠道，但同时也在该时间段内访问了其他渠道。

**使用模式**

此列中的数字是映射到我们标识所有用户帐户的14种模式之一的标识符。

*表：使用模式的导出CSV映射中的使用模式标识符*

| ID | 1 | 2 | 3 | 4 | 5和8 | 6 | 7 | 9 | 10和11 | 12 | 13 | 14 |
|---|---|---|---|---|---|---|---|---|---|---|---|---|
| 使用模式 | 常规用户 | 旅行者或通勤者 | 大家庭 | 亲朋好友 | 社交群组共享 | 一大群朋友 | 并发流 | 社区共享 | 不确定行为 | 小家庭 | 第二个家 | 异常使用 |

{style=&quot;table-layout:auto&quot;}

**共享概率**

共享概率是指特定帐户共享其凭据的概率。

>[!NOTE]
>
> 所有帐户（在选定的区段中）的共享概率平均值用于计算 [共享级别](/help/AccountIQ/dashboard.md#sharing-level) 的 [汇总共享分数](/help/AccountIQ/dashboard.md#aggregated-sharing).
