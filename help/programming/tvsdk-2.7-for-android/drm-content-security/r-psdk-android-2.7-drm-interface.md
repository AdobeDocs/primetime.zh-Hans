---
description: Primetime DRM解决方案的关键客户端元素是DRM管理器。 Android SDK附带的范例应用程序还包含一个DRMHelper类，可用于使某些DRM操作更易于实现。
title: Primetime DRM界面概述
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '257'
ht-degree: 0%

---


# Primetime DRM接口概述{#primetime-drm-interface-overview}

Primetime DRM解决方案的关键客户端元素是DRM管理器。 Android SDK附带的范例应用程序还包含一个DRMHelper类，可用于使某些DRM操作更易于实现。

<!--<a id="section_4DD54E085AB345FE9BE00865E56B28DB"></a>-->

Primetime DRM提供可扩展、高效的工作流，可在TVSDK应用程序中实施内容保护。 您可以通过为每个数字媒体文件创建许可证来保护和管理视频内容的权利。

有关详细信息，请参阅TVSDK包中包含的DRM示例播放器代码。

以下是使用DRM时最重要的API元素：

* 媒体播放器中对实现DRM子系统的DRM管理器对象的引用：

   ```java
   MediaPlayer.getDRMManager();
   ```

   >[!TIP]
   >
   >仅当`MediaPlayerEvent.DRM_METADATA`被触发后，此API才会返回有效的`DRMManager`对象。 如果在此事件触发之前调用`getDRMManager()`，它可能返回NULL。

* `DRMHelper`帮助类，在实现DRM工作流时非常有用。
* `DRMHelper`元数据加载器方法，当DRM元数据位于与媒体分离的URL中时，加载该元数据。

   ```java
   public static void loadDRMMetadata(final DRMManager drmManager,  
      final String drmMetadataUrl,  
      final DRMLoadMetadataListener loadMetadataListener);
   ```

* 一种`DRMHelper`方法，用于检查DRM元数据并确定是否需要身份验证。

   ```java
   /** 
   * Return whether authentication is needed for the provided 
   * DRMMetadata. 
   * 
   * @param drmMetadata 
   * The desired DRMMetadata on which to check whether auth is needed. 
   * @return whether authentication is required for the provided metadata 
   */ 
   public static boolean isAuthNeeded(DRMMetadata drmMetadata);
   ```

* `DRMHelper` 方法。

   ```java
   /** 
   * Helper method to perform DRM authentication. 
   * 
   * @param drmManager 
   * the DRMManager, used to perform the authentication. 
   * @param drmMetadata 
   * the DRMMetadata, containing the DRM specific information. 
   * @param authenticationListener 
   * the listener, on which the user can be notified about the 
   * authentication process status. 
   * @param authUser 
   * the DRM username provider by the user. 
   * @param authPass 
   * the DRM password provided by the user. 
   */ 
   public static void performDrmAuthentication(final DRMManager drmManager,  
   final DRMMetadata drmMetadata,  
   final String authUser,  
   final String authPass,  
   final DRMAuthenticationListener authenticationListener);
   ```

* 事件，通知您的应用程序各种DRM活动和状态。

<!--<a id="section_F58941D68EB94A5EBD1C7454D2A1B17A"></a>-->

有关DRM的详细信息，请参阅[DRM文档](https://helpx.adobe.com/primetime/user-guide.html)。
