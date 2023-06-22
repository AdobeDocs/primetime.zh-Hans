---
description: 这些类描述有关TVSDK发布的错误、警告和一些活动的消息，以进行日志记录和调试。
title: 通知类
exl-id: b869c201-2731-42e5-a20e-282edd2caddc
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '434'
ht-degree: 0%

---

# 通知类{#notification-classes}

这些类描述有关TVSDK发布的错误、警告和一些活动的消息，以进行日志记录和调试。

包： [com.adobe.mediacore](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/package-summary.html)  包： [com.adobe.mediacore.session](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/session/package-summary.html)

| 类名 | 描述 |
|---|---|
| MediaPlayerNotification。 [错误](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayerNotification.Error.html) | 描述导致播放器停止播放的错误通知的类。 这是 [MediaPlayerNotification](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayerNotification.html) 通知类型ERROR的。 |
| MediaPlayerNotification。 [信息](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayerNotification.Info.html) | 描述信息性通知的类。 这是 [MediaPlayerNotification](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayerNotification.html) 通知类型INFO的。 |
| MediaPlayerNotification。 [警告](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayerNotification.Warning.html) | 描述警告通知的类。 这是 [MediaPlayerNotification](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayerNotification.html) 通知类型WARNING。 |
| [MediaPlayerNotification](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayerNotification.html) | 提供信息性消息、警告和错误的类。 在中封装单个通知事件的对象表示形式 [通知历史记录](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/session/NotificationHistory.html). |
| MediaPlayerNotification。 [通知代码](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayerNotification.NotificationCode.html) | 返回与提供的通知代码关联的描述。 |
| [通知历史记录](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/session/NotificationHistory.html) | 存储通知对象日志的类。 循环列表 [Notificationhistory.Item](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/session/NotificationHistory.Item.html) 提供对通知事件历史记录列表访问权限的对象。 也就是说，它维护一个元素列表，每个元素都包含 [MediaPlayerNotification](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayerNotification.html) 类。 (In [session](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/session/package-summary.html) 包。) |
| 通知历史记录。 [项目](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/session/NotificationHistory.Item.html) | 在中定义循环列表中的条目的类 [通知历史记录](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/session/NotificationHistory.html) 并保存通知及其时间戳。 |
| MediaPlayerNotification。 [条目类型](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayerNotification.EntryType.html) | 包含支持的通知类型的类。 |
