---
description: 这些类描述有关TVSDK发布的错误、警告和一些活动的消息，以进行日志记录和调试。
title: 通知类
exl-id: 97a01418-f747-4a6e-bfa5-e680438e40c5
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '256'
ht-degree: 0%

---

# 通知类 {#notification-classes}

这些类描述有关TVSDK发布的错误、警告和一些活动的消息，以进行日志记录和调试。

| **类名** | **描述** |
|---|---|
| [PTMediaError](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTMediaError.html) | 描述导致播放器停止播放的错误通知的类。 这是 [PTN通知](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTNotification.html) 通知类型ERROR的。 |
| [PTMediaPlayerNotifications](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTMediaPlayerNotifications.html) | 列出Primetime播放器框架调度的所有通知。 |
| [PTN通知](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTNotification.html) | 提供信息性消息、警告和错误的类。 在中封装单个通知事件的对象表示形式 [PTNotificationHistory](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTNotificationHistory.html). |
| [PTNotificationHistory](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTNotificationHistory.html) | 存储通知对象日志的类 [PTNotificationHistoryItem](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTNotificationHistoryItem.html) 提供对通知事件历史记录列表访问权限的对象。 也就是说，它维护一个元素列表，每个元素都包含 [PTN通知](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTNotification.html) |
| [PTNotificationHistoryItem](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTNotificationHistoryItem.html) | 在中定义循环列表中的条目的类 [PTNotificationHistory](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTNotificationHistory.html) 并保存通知及其时间戳。 |
