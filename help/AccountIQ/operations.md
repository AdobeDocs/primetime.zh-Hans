---
title: 帐户IQ中的操作
description: 帐户IQ中的操作包括采取措施对订阅者帐户执行自动化和批量操作并跟踪其效果。
exl-id: ba6bceca-221c-42db-b207-804e4b9f6d54
source-git-commit: 5b34fbe26078ae761d61179975366505c5628c9c
workflow-type: tm+mt
source-wordcount: '467'
ht-degree: 0%

---

# 操作 {#operations-tab-next-steps}

了解订阅者的使用模式并识别选定区段的密码共享（使用帐户IQ中的Reports &amp; Analytics）后，您可以针对目标采取有针对性的操作以缓解密码共享。

帐户IQ中的“操作”功能可帮助您通过称为“操作”的重点过程，有效地处理和管理凭据共享。 它为您提供了多种选项，可为特定的用户组设计目标、根据目标定制定位操作，并在将来的持续时间内自动执行这些操作。 通过操作功能，您不仅可以创建和执行操作，还可以衡量操作的影响。 因此，通过评估影响，您可以调整策略以优化影响，无论是转换借款者还是减少凭据共享。

要查看 **操作** 页面选择 **操作** 选项 **操作** 在帐户IQ应用程序的左侧导航中。 “操作”页面列出了帐户IQ系统上已存在的所有操作及其详细信息。

![](assets/operations-page.png)

*图：帐户IQ中现有操作的列表和详细信息*

在“操作”页面上，您可以：

* 查看帐户IQ中已存在的操作列表

* 查看操作详细信息，如：

   * 状态（已计划、正在运行、已结束、错误或已停止）

   * 进度（完成百分比）

   * 目标受众（要在上运行操作的区段）

   * 计划（开始和结束日期）

   * 操作的创建和结束日期

* [创建新操作](/help/AccountIQ/operation-affecting-user-segment.md)

* [查看操作报表](#operation-reports)

<!--* Search from the list of operations using Search field

* Stop an operation.

* Create a duplicate operation.

* [Configure columns of Operations details page](#configure-columns)-->

## 查看操作报表 {#operation-reports}

您可以通过查看操作报告来分析其影响。 要查看操作的报表，请执行以下操作：

1. 在主“操作”页上选择操作名称。

   报表以堆叠列图的形式显示。

   ![](assets/operation-impact-report.png)

   *图：操作报告，以查看操作的影响*

   X轴表示评估期，Y轴表示操作的影响（以评估期段内区段中的帐户数衡量）。 每个杆分成三部分。

   * 其中一部分表示仍满足操作区段标准的帐户数。

   * 另一部分表示该期间最初位于区段中但不再满足操作区段标准的活动帐户数量。

   * 第三部分是该期间未活动的帐户。
   >[!NOTE]
   >
   >第一个栏表示在评估期开始时满足操作区段条件的帐户数。

   随着时间的推移，该图表通过指示已相对于原始标准（例如，共享概率超过90并使用5个以上设备）更改其行为或已变为非活动状态的帐户数，来显示操作（通过操作）的效果。

<!--For example, in the above image the variable on the y-axis is number of accounts. Looking at the graph you can compare the number of accounts that are in the operations' segment versus the number of accounts that are outside the operations segment at a particular time (such as week 2nd of the operations evaluation period). Therefore, you can analyze how over the evaluation period do number of accounts vary within the operation segment and outside the segment.

So, if your operation was to send out warning emails to suspecting accounts, and accounts in operations segment were those with sharing probability more than 90 and using more than 5 devices to stream content, then in the beginning of the evaluation period accounts in segment are more than 17 thousand. This number changes over the evaluation period as shown in the graph, thereby indicating the impact of operation. Based on the evaluation, you can take remedial measures on suspecting accounts, or continue with the operation, or adjust your strategy for better outcomes to curb credential sharing.-->

1. 要关闭报表并返回到主“操作”页面，请选择 **操作** 选项 **操作** 中。

<!--

![](assets/operations-details.png)

*Figure: Operation details*
## Configure columns {#configure-columns}

You can select the icon to **Configure columns** on the top of the operations table.

![](assets/config-columns.png)

*Figure: Configure columns of Operations details page*-->