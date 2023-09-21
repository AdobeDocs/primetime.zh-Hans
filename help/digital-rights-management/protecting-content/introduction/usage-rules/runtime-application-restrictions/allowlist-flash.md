---
title: Adobe®Flash®播放器SWF的允许列表
description: Adobe®Flash®播放器SWF的允许列表
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '128'
ht-degree: 0%

---

# Adobe®Flash®播放器SWF的允许列表{#allowlist-for-adobe-flash-player-swfs}

此允许列表指定允许播放内容的SWF文件。

指定包含SWFURL或使用SWF内容计算的SHA-256摘要的SWF文件。 如果使用SHA-256摘要，则此使用规则还指定允许客户端下载和验证SWF的最长时间。

示例用例：在概念上等同于Flash Media Server中的SWF验证，但在客户端强制实施，以限制哪些视频播放器可以播放内容。 请注意，与父SWF相比，Primetime DRM在子SWF的强制实施方面的行为有所不同。
