---
description: MediaPlayerNotification提供与播放器状态相关的信息。
title: 通知内容
exl-id: dc46f717-f08b-4d52-82ea-88107076f4fb
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '125'
ht-degree: 0%

---

# 通知内容{#notification-content}

MediaPlayerNotification提供与播放器状态相关的信息。

TVSDK提供了按时间顺序排列的 `MediaPlayerNotification` 通知。 每个通知都包含以下信息：

* 时间戳
* 包含以下元素的诊断元数据：

   * 键入INFO、WARN或ERROR
   * `code`：通知的数值表示形式。
   * `name`：人类可读的通知描述，如SEEK_ERROR
   * `metadata`：包含有关通知的相关信息的键/值对。 例如，一个名为的键 `URL` 提供一个值，该值为与通知相关的URL。

   * `innerNotification`：对另一个的引用 `MediaPlayerNotification` 直接影响此通知的对象。

您可以将此信息存储在本地，以供以后分析使用，也可以将其发送到远程服务器以进行日志记录和图形显示。
