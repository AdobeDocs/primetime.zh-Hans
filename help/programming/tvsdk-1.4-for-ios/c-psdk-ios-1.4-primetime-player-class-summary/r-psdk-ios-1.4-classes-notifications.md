---
description: 这些类描述有关错误、警告和TVSDK出于记录和调试目的而发出的某些活动的消息。
seo-description: 这些类描述有关错误、警告和TVSDK出于记录和调试目的而发出的某些活动的消息。
seo-title: 通知类
title: 通知类
uuid: 08c29efe-245d-4a6d-80c6-cd561cbf3b5f
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '277'
ht-degree: 0%

---


# 通知类{#notification-classes}

这些类描述有关错误、警告和TVSDK出于记录和调试目的而发出的某些活动的消息。

| 类名称 | 说明 |
|---|---|
| [PTMediaError](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTMediaError.html) | 描述导致播放器停止播放的错误通知的类。 这是通知类型为ERROR的[PTNotification](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTNotification.html)。 |
| [PTMediaPlayerNotifications](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTMediaPlayerNotifications.html) | 列表由Primetime Player框架调度的所有通知。 |
| [PTNotification](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTNotification.html) | 提供信息性消息、警告和错误的类。 将单个通知事件的对象表示封装在[PTNotificationHistory](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTNotificationHistory.html)中。 |
| [PTNotificationHistory](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTNotificationHistory.html) | 存储通知对象[PTNotificationHistoryItem](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTNotificationHistoryItem.html)对象日志的类，该对象提供对通知事件历史列表的访问。 也就是说，它保持元素的列表，每个元素都包含[PTNotification](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTNotification.html)的单独实例 |
| [PTNotificationHistoryItem](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTNotificationHistoryItem.html) | 在[PTNotificationHistory](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTNotificationHistory.html)的循环列表中定义条目并保存通知及其时间戳的类。 |

