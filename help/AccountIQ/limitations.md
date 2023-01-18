---
title: 限制和已知问题
description: 产品中的已知问题。
exl-id: 08d65716-8b6a-4300-acda-fec63e1e6815
source-git-commit: dcd89849937f4893705423465be4003948739eeb
workflow-type: tm+mt
source-wordcount: '415'
ht-degree: 0%

---

# 已知问题和限制 {#known-issues}

Adobe通过其产品提供强大的功能和无缝的用户体验。 当前版本（版本1.1）的“帐户IQ”可高度置信地为流提供商提供使用和订阅共享分析。 但是，在即将发布的版本中，将解决以下限制。

* 在功能板或报表页面中定义同类群组时，当前没有添加量度的选项，例如 **设备数量** 以优化区段。 此功能将在不久的将来提供。

* 在估算个人帐户的分享分数时，帐户IQ采用一种保守的方法，使公司能够满怀信心地采取行动进行共享。 但是，这种方法往往低估了在许多帐户中汇总的共享总量。

* 的 [整体共享分数](/help/AccountIQ/dashboard.md#overall-sharing-score) 当前仅包含 [共享级别](/help/AccountIQ/dashboard.md#sharing-level) 和 [从共享帐户使用](/help/AccountIQ/dashboard.md#usage-from-shared-accounts). 未来版本会考虑其他量度。

* 在功能板或报表页面中定义同类群组时，MVPD和渠道的选择器现在缺少搜索机制。

* 在功能板或报表页面中定义同类群组时，最多只能选择10个MVPD和程序员（或单个渠道）。

* 导出帐户统计信息的选项仅限于导出1000个帐户，目前为止。

* 要选择的选项 [区段类型](#segment-type) 定义操作时， **固定帐户数**. 的 **帐户的变量数** 选项将在即将发布的版本中提供。

* 左侧导航中的基准测试、检测模型、区段、快照和规则部分当前处于禁用状态，将在即将发布的版本中提供。

* 创建 [操作](/help/AccountIQ/operation-affecting-user-segment.md)，则只能识别两种 [操作](/help/AccountIQ/operation-affecting-user-segment.md) 当前 — 并发监控规则和外部操作。

* 目前，只能创建和 [计划](/help/AccountIQ/operation-affecting-user-segment.md#action). 将来的版本将允许您暂停、恢复和完全管理它们。

* 由于使用的数据集比较有限，隔离模式无法真正反映共享量。 因此，隔离模式下的MVPD无法与任何其他MVPD进行比较。 <!--do we need to separate out this limitation, which is from a different persona i.e. only for Programmer persona?-->

* 定义新 [区段](/help/AccountIQ/segments-timeframe.md) 对于操作，您可以添加量度。 但是，如果选择保存的区段，则无法添加更多量度来优化该区段。

* 粒度和时间范围选择器限制为一周或一个月，这意味着只能在一周或一个月内评估数据。

* 当前在粒度和时间范围选择器中禁用了预定义间隔，并且将在将来版本中提供。
