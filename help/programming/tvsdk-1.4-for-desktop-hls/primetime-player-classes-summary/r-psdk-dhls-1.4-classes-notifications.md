---
description: 这些类描述有关错误、警告以及某些活动的消息，这些消息指出在日志记录和调试方面存在问题。
title: 通知类
exl-id: d8af783f-1e80-4e50-89b8-97643ff6670b
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '280'
ht-degree: 0%

---

# 通知类 {#notification-classes}

这些类描述有关错误、警告以及某些活动的消息，这些消息指出在日志记录和调试方面存在问题。

包： [com.adobe.mediacore.notifications](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/notifications/package-detail.html)

| 类名 | 描述 |
|---|---|
| [通知](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/notifications/Notification.html) | 提供信息性消息、警告和错误的类。 在中封装单个通知事件的对象表示形式 [通知历史记录](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/notifications/NotificationHistory.html). |
| [通知代码](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/notifications/NotificationCode.html) | 返回与提供的通知代码关联的说明，并为通知对象提供数值常量。 |
| [通知历史记录](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/notifications/NotificationHistory.html) | 存储通知对象日志的类。 循环列表 [NotificationhistoryItem](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/notifications/NotificationHistoryItem.html) 提供对通知事件历史记录列表访问权限的对象。 也就是说，它维护一个元素列表，每个元素都包含 [通知](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/notifications/Notification.html) 类。 |
| [NotificationhistoryItem](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/notifications/NotificationHistoryItem.html) | 在中定义循环列表中的条目的类 [通知历史记录](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/notifications/NotificationHistory.html) 并保存通知及其时间戳。 |
| [通知类型](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/notifications/NotificationType.html) | 包含支持的通知类型的类。 |
