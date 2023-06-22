---
description: 本指南提供了有关如何使用TVSDK for Android（使用Java实现）开发视频播放器应用程序的信息。
title: 产品概述、受众和本指南
exl-id: 3dfef60a-5547-494b-9bbe-74eb0440ec92
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '259'
ht-degree: 0%

---

# 产品概述、受众和本指南 {#product-overview-audience-and-this-guide}

本指南提供了有关如何使用TVSDK for Android（使用Java实现）开发视频播放器应用程序的信息。

<!--<a id="section_FC24E86A2E6442B8A3769160769BBDFA"></a>-->

* 有关TVSDK支持的功能列表，请参阅 [Primetime TVSDK功能](../../tvsdk-2.7-for-android/overview-prod-audience-guide/c-psdk-android-2.7-overview-of-the-player.md).
* 有关使用TVSDK的特定硬件和软件要求，请参阅 [要求](../../tvsdk-2.7-for-android/c-psdk-android-2.7-requirements.md).
* 有关可用API的列表，请参阅 [TVSDK Android API](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_2.7/).

## 产品概述 {#section_9664959F25C948878F2F7EF3D360CA95}

TVSDK包含API描述和代码示例，可帮助您将高级视频功能、内容保护和广告功能集成到播放器中。 您可以使用Java创建视频播放器用户界面。 TVSDK可帮助您将该用户界面连接到其媒体播放器。 这允许您根据媒体清单播放视频和广告。 您还可以使用TVSDK检索有关视频的信息、处理安全性以及控制和监视播放。

## Audience {#section_527860B373734D3BA89FCF5EC1F6DC37}

本指南假定您了解如何使用Java开发应用程序和视频播放器。 您可以使用Java实施视频播放器UI，并整合所需的TVSDK功能。

## 关于本指南 {#section_9A5B2FC506B34B5DB71CA827B307A4D0}

本指南提供的信息允许您在Android设备上使用Java将TVSDK功能合并到视频播放器中。

## 本指南中的命名空间表示法 {#section_8B866054E9ED4B5F99DCA7A681404632}

>[!TIP]
>
>TVSDK API命名空间前缀 [!DNL com.adobe.mediacore] 为简短起见，通常省略。
>
>如果上下文清晰，则在引用许多API元素时没有它们的父类指示符。
