---
description: MediaPlayerNotification提供与播放器状态相关的信息。
seo-description: MediaPlayerNotification提供与播放器状态相关的信息。
seo-title: 通知内容
title: 通知内容
uuid: c2321a49-1b60-4e44-b8e2-a023b764d779
translation-type: tm+mt
source-git-commit: 7e8df034035fe465fbe403949ef828e7811ced2e

---


# 通知内容{#notification-content}

MediaPlayerNotification提供与播放器状态相关的信息。

TVSDK提供通知的时间顺序 `MediaPlayerNotification` 列表。 每个通知都包含以下信息：

* 时间戳
* 包含以下元素的诊断元数据：

   * 类型信息、警告或错误
   * `code`:通知的数字表示。
   * `name`:通知的可读描述，如SEEK_ERROR
   * `metadata`:包含有关通知的相关信息的键／值对。 例如，名为的键 `URL` 提供一个值，该值是与通知相关的URL。

   * `innerNotification`:对直接影响此通 `MediaPlayerNotification` 知的其他对象的引用。

您可以将此信息存储在本地以供以后分析，或将其发送到远程服务器进行记录和图形表示。
