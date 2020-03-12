---
description: 这些类描述有关错误、警告和TVSDK为记录和调试而发出的某些活动的消息。
seo-description: 这些类描述有关错误、警告和TVSDK为记录和调试而发出的某些活动的消息。
seo-title: 通知类
title: 通知类
uuid: 8a276056-775f-432d-a4b4-722f6e4e278f
translation-type: tm+mt
source-git-commit: 557f42cd9a6f356aa99e13386d9e8d65e043a6af

---


# 通知类 {#notification-classes}

这些类描述有关错误、警告和TVSDK为记录和调试而发出的某些活动的消息。

| **类名** | **说明** |
|---|---|
| [PTMediaError](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTMediaError.html) | 描述导致播放器停止播放的错误通知的类。 这是通知 [类型](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTNotification.html) ERROR的PTN通知。 |
| [PTMediaPlayerNotifications](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTMediaPlayerNotifications.html) | 列出由Primetime Player框架调度的所有通知。 |
| [PTNotification](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTNotification.html) | 提供信息性消息、警告和错误的类。 封装PTNotificationHistory中单个通知事件的对 [象表示](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTNotificationHistory.html)。 |
| [PTNotificationHistory](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTNotificationHistory.html) | 存储通知对象PTNotificationHistoryItem对象日志的类 [](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTNotificationHistoryItem.html) ，用于提供对通知事件历史记录列表的访问。 即，它保留一个元素列表，每个元素都包含 [PTNotification的一个单独实例](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTNotification.html) |
| [PTNotificationHistoryItem](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTNotificationHistoryItem.html) | 在 [](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTNotificationHistory.html) PTNotificationHistory的循环列表中定义一个条目并保存通知及其时间戳的类。 |

