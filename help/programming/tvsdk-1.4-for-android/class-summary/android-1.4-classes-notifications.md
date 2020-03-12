---
description: 这些类描述有关错误、警告和TVSDK为记录和调试而发出的某些活动的消息。
seo-description: 这些类描述有关错误、警告和TVSDK为记录和调试而发出的某些活动的消息。
seo-title: 通知类
title: 通知类
uuid: e231a2d0-6190-4251-87db-ca46d2aee60d
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# 通知类{#notification-classes}

这些类描述有关错误、警告和TVSDK为记录和调试而发出的某些活动的消息。

包： [com.adobe.mediacore包](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/package-summary.html) : [com.adobe.mediacore.session](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/session/package-summary.html)

| 类名 | 说明 |
|---|---|
| MediaPlayerNotification。 [错误](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayerNotification.Error.html) | 描述导致播放器停止播放的错误通知的类。 这是通知 [类型为](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayerNotification.html) ERROR的MediaPlayerNotification。 |
| MediaPlayerNotification。 [信息](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayerNotification.Info.html) | 描述信息通知的类。 这是通知 [类型](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayerNotification.html) INFO的MediaPlayerNotification。 |
| MediaPlayerNotification。 [警告](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayerNotification.Warning.html) | 描述警告通知的类。 这是通知 [类型为WARNING](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayerNotification.html) 的MediaPlayerNotification。 |
| [MediaPlayerNotification](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayerNotification.html) | 提供信息性消息、警告和错误的类。 封装 [NotificationHistory中单个通知事件的对象表示](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/session/NotificationHistory.html)。 |
| MediaPlayerNotification。 [NotificationCode](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayerNotification.NotificationCode.html) | 返回与提供的通知代码关联的说明。 |
| [NotificationHistory](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/session/NotificationHistory.html) | 存储通知对象日志的类。 提供对通知事 [件历史记录列表访问权限的NotificationHistory.Item](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/session/NotificationHistory.Item.html) 对象的循环列表。 即，它维护一个元素列表，每个元素都包含 [MediaPlayerNotification类的单独实例](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayerNotification.html) 。 (在会 [话包中](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/session/package-summary.html) 。) |
| 通知历史记录。 [项目](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/session/NotificationHistory.Item.html) | 在 [](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/session/NotificationHistory.html) NotificationHistory中定义循环列表中的条目并保存通知及其时间戳的类。 |
| MediaPlayerNotification。 [EntryType](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayerNotification.EntryType.html) | 包含支持的通知类型的类。 |