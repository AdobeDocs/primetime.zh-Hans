---
description: MediaPlayerNotification提供与播放器状态相关的信息。
title: 通知内容
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '125'
ht-degree: 0%

---


# 通知内容{#notification-content}

MediaPlayerNotification提供与播放器状态相关的信息。

TVSDK提供`MediaPlayerNotification`通知的时间列表。 每个通知都包含以下信息：

* 时间戳
* 包含以下元素的诊断元数据：

   * 类型信息、警告或错误
   * `code`:通知的数字表示。
   * `name`:通知的用户可读描述，如SEEK_ERROR
   * `metadata`:包含有关通知的相关信息的键/值对。例如，名为`URL`的键提供一个值，该值是与通知相关的URL。

   * `innerNotification`:直接影响此 `MediaPlayerNotification` 通知的对象的引用。

您可以将此信息存储在本地以备以后分析，或将其发送到远程服务器以进行记录和图形表示。
