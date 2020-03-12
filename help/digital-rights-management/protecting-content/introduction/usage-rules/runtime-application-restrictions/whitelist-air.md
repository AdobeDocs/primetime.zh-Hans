---
description: 'null'
seo-description: 'null'
seo-title: 允许播放受保护内容的Primetime DRM应用程序白名单
title: 允许播放受保护内容的Primetime DRM应用程序白名单
uuid: 23dd4faf-7992-4ee9-97ce-c6004ee995c2
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# 允许播放受保护内容的Primetime DRM应用程序白名单{#whitelist-for-primetime-drm-applications-allowed-to-play-protected-content}

白名单指定允许播放内容的AIR、iOS和Android应用程序。 它还指定AIR和iOS应用程序ID、最低版本、最高版本和发布者ID。

示例用例：使用此规则将播放限制到特定应用程序，或控制可访问内容的应用程序版本。

>[!NOTE] {class=&quot;- topic/note &quot;}
>
>如果使用Adobe Flash Builder构建受保护的应用程序，则必须确保不在“调试”模式下部署该应用程序。 在“调试”模式下部署应用程序时，Flash Builder会附加到AIR应用程序ID `.debug` ，这会导致Primetime DRM中的白名单功能表现出意外。

