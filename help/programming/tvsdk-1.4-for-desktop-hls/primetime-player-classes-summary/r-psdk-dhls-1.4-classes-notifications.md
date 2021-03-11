---
description: 这些类描述有关错误、警告和某些活动的消息，这些消息是出于日志和调试目的而出现的。
title: 通知类
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '280'
ht-degree: 0%

---


# 通知类{#notification-classes}

这些类描述有关错误、警告和某些活动的消息，这些消息是出于日志和调试目的而出现的。

包：[com.adobe.mediacore.notifications](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/notifications/package-detail.html)

| 类名 | 说明 |
|---|---|
| [通知](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/notifications/Notification.html) | 提供信息性消息、警告和错误的类。 封装[NotificationHistory](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/notifications/NotificationHistory.html)中单个通知事件的对象表示。 |
| [NotificationCode](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/notifications/NotificationCode.html) | 返回与提供的通知代码关联的说明，并为通知对象提供数值常量。 |
| [通知历史记录](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/notifications/NotificationHistory.html) | 存储通知对象日志的类。 [NotificationHistoryItem](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/notifications/NotificationHistoryItem.html)对象的循环列表，提供对通知事件历史列表的访问。 也就是说，它保持元素的列表，每个元素都包含[Notification](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/notifications/Notification.html)类的单独实例。 |
| [NotificationHistoryItem](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/notifications/NotificationHistoryItem.html) | 在[NotificationHistory](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/notifications/NotificationHistory.html)的循环列表中定义条目并保存通知及其时间戳的类。 |
| [NotificationType](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/notifications/NotificationType.html) | 包含受支持通知类型的类。 |

