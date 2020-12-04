---
description: 这些类描述有关错误、警告和某些活动的消息，这些消息会出于记录和调试目的而出现问题。
seo-description: 这些类描述有关错误、警告和某些活动的消息，这些消息会出于记录和调试目的而出现问题。
seo-title: 通知类
title: 通知类
uuid: 3befc64b-4abd-47df-9c45-215b49029757
translation-type: tm+mt
source-git-commit: 91cea7acb8127e02b82e5242b9ad6ab0d12ce0eb
workflow-type: tm+mt
source-wordcount: '300'
ht-degree: 0%

---


# 通知类{#notification-classes}

这些类描述有关错误、警告和某些活动的消息，这些消息会出于记录和调试目的而出现问题。

包：[com.adobe.mediacore.notifications](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/notifications/package-detail.html)

| 类名称 | 说明 |
|---|---|
| [通知](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/notifications/Notification.html) | 提供信息性消息、警告和错误的类。 将单个通知事件的对象表示封装在[NotificationHistory](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/notifications/NotificationHistory.html)中。 |
| [通知代码](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/notifications/NotificationCode.html) | 返回与提供的通知代码关联的说明，并为通知对象提供数字常量。 |
| [通知历史记录](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/notifications/NotificationHistory.html) | 存储通知对象日志的类。 [NotificationHistoryItem](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/notifications/NotificationHistoryItem.html)对象的循环列表，提供对通知事件历史列表的访问。 也就是说，它保持元素的列表，每个元素都包含[Notification](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/notifications/Notification.html)类的单独实例。 |
| [NotificationHistoryItem](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/notifications/NotificationHistoryItem.html) | 在[NotificationHistory](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/notifications/NotificationHistory.html)的循环列表中定义一个条目并保存通知及其时间戳的类。 |
| [通知类型](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/notifications/NotificationType.html) | 包含受支持通知类型的类。 |

