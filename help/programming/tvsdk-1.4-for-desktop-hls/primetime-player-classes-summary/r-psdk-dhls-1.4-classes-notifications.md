---
description: 这些类描述有关错误、警告和某些活动的消息，这些消息是出于记录和调试目的而发出的。
seo-description: 这些类描述有关错误、警告和某些活动的消息，这些消息是出于记录和调试目的而发出的。
seo-title: 通知类
title: 通知类
uuid: 3befc64b-4abd-47df-9c45-215b49029757
translation-type: tm+mt
source-git-commit: 91cea7acb8127e02b82e5242b9ad6ab0d12ce0eb

---


# 通知类 {#notification-classes}

这些类描述有关错误、警告和某些活动的消息，这些消息是出于记录和调试目的而发出的。

包： [com.adobe.mediacore.notifications](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/notifications/package-detail.html)

| 类名 | 说明 |
|---|---|
| [通知](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/notifications/Notification.html) | 提供信息性消息、警告和错误的类。 封装 [NotificationHistory中单个通知事件的对象表示](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/notifications/NotificationHistory.html)。 |
| [NotificationCode](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/notifications/NotificationCode.html) | 返回与提供的通知代码关联的说明，并为通知对象提供数字常量。 |
| [NotificationHistory](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/notifications/NotificationHistory.html) | 存储通知对象日志的类。 提供对通知事 [件历史记录列表访问权限的NotificationHistoryItem](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/notifications/NotificationHistoryItem.html) 对象的循环列表。 即，它维护一个元素列表，每个元素都包含 [Notification类的单独实例](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/notifications/Notification.html) 。 |
| [NotificationHistoryItem](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/notifications/NotificationHistoryItem.html) | 在 [](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/notifications/NotificationHistory.html) NotificationHistory中定义循环列表中的条目并保存通知及其时间戳的类。 |
| [NotificationType](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/notifications/NotificationType.html) | 包含支持的通知类型的类。 |

