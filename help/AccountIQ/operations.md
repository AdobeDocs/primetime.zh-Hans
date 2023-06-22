---
title: 帐户IQ中的操作
description: 帐户IQ中的操作涉及对订阅者帐户执行自动化和批量操作以及跟踪其影响的操作。
exl-id: ba6bceca-221c-42db-b207-804e4b9f6d54
source-git-commit: 5b34fbe26078ae761d61179975366505c5628c9c
workflow-type: tm+mt
source-wordcount: '467'
ht-degree: 0%

---

# 操作 {#operations-tab-next-steps}

了解订阅者的使用模式并确定选定区段的密码共享后（使用帐户IQ中的Reports &amp; Analytics），您可以采取有针对性的操作以实现缓解密码共享的目标。

Account IQ中的操作功能可帮助您通过称为操作的专门过程有效地处理和管理凭据共享。 它为您提供了选项，用于为特定订阅者帐户组设计目标、定制定向操作（基于目标），并在未来持续时间自动执行这些操作。 通过“操作”功能，您不仅可以创建和执行操作，还可以衡量它们的影响。 因此，通过评估影响，您可以调整策略以优化影响，无论是转化借款人还是缓解凭据共享。

查看 **操作** 页面选择 **操作** 下的选项 **操作** 帐户IQ应用程序的左侧导航区域中。 “操作”页面列出帐户IQ系统上已存在的所有操作及其详细信息。

![](assets/operations-page.png)

*图：帐户IQ中现有操作的列表和详细信息*

在“操作”页面上，您可以：

* 查看帐户IQ中已存在的操作列表

* 查看操作详细信息，例如：

   * 状态（“已计划”、“正在运行”、“已结束”、“错误”或“已停止”）

   * 进度（完成百分比）

   * 目标受众（要运行操作的区段）

   * 计划（工序的起始日期和终止日期）

   * 操作的创建和结束日期

* [创建新操作](/help/AccountIQ/operation-affecting-user-segment.md)

* [查看工序报表](#operation-reports)

<!--* Search from the list of operations using Search field

* Stop an operation.

* Create a duplicate operation.

* [Configure columns of Operations details page](#configure-columns)-->

## 查看工序报表 {#operation-reports}

您可以通过查看操作报表来分析操作的影响。 要查看工序报表，请执行以下操作：

1. 在主“操作”页上选择操作名称。

   报表以栈叠柱状图的形式显示。

   ![](assets/operation-impact-report.png)

   *图：用于查看运营影响的运营报表*

   X轴表示评估期，而Y轴描述操作的影响（根据评估期中区段中的帐户数）。 每条杆分为三个部分。

   * 一部分表示仍满足工序段标准的帐户数。

   * 另一部分表示该期间的活动帐户数，这些活动帐户最初位于区段中，但不再满足操作区段的标准。

   * 第三部分代表该期间未启用的账户。
   >[!NOTE]
   >
   >第一栏表示在评估期开始时满足工序段条件的帐户数。

   随着时间的推移，此图表通过指示帐户数量来显示您操作（通过操作）的效果，这些帐户的行为相对于原始标准发生了更改（例如，共享概率超过90且使用超过5台设备），或者已停用。

<!--For example, in the above image the variable on the y-axis is number of accounts. Looking at the graph you can compare the number of accounts that are in the operations' segment versus the number of accounts that are outside the operations segment at a particular time (such as week 2nd of the operations evaluation period). Therefore, you can analyze how over the evaluation period do number of accounts vary within the operation segment and outside the segment.

So, if your operation was to send out warning emails to suspecting accounts, and accounts in operations segment were those with sharing probability more than 90 and using more than 5 devices to stream content, then in the beginning of the evaluation period accounts in segment are more than 17 thousand. This number changes over the evaluation period as shown in the graph, thereby indicating the impact of operation. Based on the evaluation, you can take remedial measures on suspecting accounts, or continue with the operation, or adjust your strategy for better outcomes to curb credential sharing.-->

1. 要关闭报告并返回主“操作”页，请选择 **操作** 下的选项 **操作** 在左侧导航中。

<!--

![](assets/operations-details.png)

*Figure: Operation details*
## Configure columns {#configure-columns}

You can select the icon to **Configure columns** on the top of the operations table.

![](assets/config-columns.png)

*Figure: Configure columns of Operations details page*-->