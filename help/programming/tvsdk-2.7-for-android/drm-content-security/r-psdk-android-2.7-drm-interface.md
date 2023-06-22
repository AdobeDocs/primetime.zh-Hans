---
description: Primetime DRM解决方案的关键客户端元素是DRM管理器。 Android SDK附带的示例应用程序还包含一个DRMHelper类，该类可用于使某些DRM操作更容易实施。
title: Primetime DRM界面概述
exl-id: 37037419-fe3d-4e9e-a35d-e0accfba4e80
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '257'
ht-degree: 0%

---

# Primetime DRM界面概述 {#primetime-drm-interface-overview}

Primetime DRM解决方案的关键客户端元素是DRM管理器。 Android SDK附带的示例应用程序还包含一个DRMHelper类，该类可用于使某些DRM操作更容易实施。

<!--<a id="section_4DD54E085AB345FE9BE00865E56B28DB"></a>-->

Primetime DRM提供了一个可扩展的高效工作流，用于在TVSDK应用程序中实施内容保护。 通过为每个数字媒体文件创建许可证，您可以保护和管理视频内容的权限。

有关更多信息，请参阅TVSDK包中包含的DRM示例播放器代码。

以下是使用DRM时最重要的API元素：

* 媒体播放器中对实现DRM子系统的DRM管理器对象的引用：

   ```java
   MediaPlayer.getDRMManager();
   ```

   >[!TIP]
   >
   >此API将返回有效的 `DRMManager` 对象仅位于 `MediaPlayerEvent.DRM_METADATA` 被炒了。 如果您调用 `getDRMManager()` 在触发此事件之前，它可能会返回NULL。

* 此 `DRMHelper` 帮助程序类，在实施DRM工作流时很有用。
* A `DRMHelper` 元数据加载器方法，当DRM元数据位于与媒体不同的URL中时，该方法会加载元数据。

   ```java
   public static void loadDRMMetadata(final DRMManager drmManager,  
      final String drmMetadataUrl,  
      final DRMLoadMetadataListener loadMetadataListener);
   ```

* A `DRMHelper` 检查DRM元数据并确定是否需要身份验证的方法。

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

* `DRMHelper` 执行身份验证的方法。

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

* 通知应用程序各种DRM活动和状态的事件。

<!--<a id="section_F58941D68EB94A5EBD1C7454D2A1B17A"></a>-->

有关DRM的详细信息，请参见 [DRM文档](https://helpx.adobe.com/primetime/user-guide.html).
