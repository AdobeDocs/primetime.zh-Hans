---
title: 允许播放受保护内容的Primetime DRM应用程序允许列表
description: 允许播放受保护内容的Primetime DRM应用程序允许列表
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '143'
ht-degree: 0%

---

# 允许播放受保护内容的Primetime DRM应用程序允许列表 {#allowlist-for-primetime-drm-applications-allowed-to-play-protected-content}

允许列表可指定允许播放内容的AIR、iOS和Android应用程序。 它还指定了AIR和iOS应用程序ID、最低版本、最高版本和发布者ID。

示例用例：使用此规则可以将播放限制在特定应用程序，或控制可以访问内容的应用程序的版本。

>[!NOTE]
>
>如果使用AdobeFlash Builder来构建受保护的应用程序，则必须确保不要在“调试”模式下部署应用程序。 在调试模式下部署应用程序时，Flash Builder会附加 `.debug` 到AIR应用程序ID，这会导致Primetime DRM中的允许列表功能出现意外行为。
