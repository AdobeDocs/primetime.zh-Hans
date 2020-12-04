---
description: 'null'
seo-description: 'null'
seo-title: 允许播放受保护内容的Primetime DRM应用程序的允许列表
title: 允许播放受保护内容的Primetime DRM应用程序的允许列表
uuid: 23dd4faf-7992-4ee9-97ce-c6004ee995c2
translation-type: tm+mt
source-git-commit: 1b9792a10ad606b99b6639799ac2aacb707b2af5
workflow-type: tm+mt
source-wordcount: '145'
ht-degree: 0%

---


# 允许播放受保护内容的Primetime DRM应用程序的允许列表{#allowlist-for-primetime-drm-applications-allowed-to-play-protected-content}

允许列表指定允许播放内容的AIR、iOS和Android应用程序。 它还指定AIR和iOS应用程序ID、最低版本、最高版本和发布者ID。

示例用例：使用此规则将播放限制到特定应用程序，或控制可访问内容的应用程序的版本。

>[!NOTE]
>
>如果使用AdobeFlash Builder构建受保护的应用程序，则必须确保不在调试模式下部署该应用程序。 在“调试”模式下部署应用程序时，Flash Builder会将`.debug`附加到AIR应用程序 ID，这会导致Primetime DRM中的允许列表功能表现异常。
