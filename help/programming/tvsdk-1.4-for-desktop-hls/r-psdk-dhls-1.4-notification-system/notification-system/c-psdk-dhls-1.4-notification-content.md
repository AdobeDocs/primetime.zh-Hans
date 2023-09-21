---
description: MediaPlayerNotification提供与播放器状态相关的信息。
title: 通知内容
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '125'
ht-degree: 0%

---

# 通知内容{#notification-content}

MediaPlayerNotification提供与播放器状态相关的信息。

TVSDK按时间顺序列出了以下列表： `MediaPlayerNotification` 通知。 每个通知都包含以下信息：

* 时间戳
* 诊断元数据包含以下元素：

   * 键入INFO、WARN或ERROR
   * `code`：通知的数值表示形式。
   * `name`：人类可读的通知描述，如SEEK_ERROR
   * `metadata`：包含有关通知的信息的键/值对。 例如，名为的键 `URL` 提供一个值，该值为与通知相关的URL。

   * `innerNotification`：对另一个的引用 `MediaPlayerNotification` 直接影响此通知的对象。

您可以将此信息存储在本地，以供以后分析使用，也可以将其发送到远程服务器以供日志记录和图形显示。
