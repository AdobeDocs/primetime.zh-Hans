---
description: 您可以使用Primetime数字版权管理(DRM)系统的功能来提供对视频内容的安全访问。 或者，您也可以使用第三方DRM解决方案作为Adobe集成Primetime DRM解决方案的替代方案。
seo-description: 您可以使用Primetime数字版权管理(DRM)系统的功能来提供对视频内容的安全访问。 或者，您也可以使用第三方DRM解决方案作为Adobe集成Primetime DRM解决方案的替代方案。
seo-title: Primetime DRM界面概述
title: Primetime DRM界面概述
uuid: 71479464-8356-4732-9774-da9f6084e6ad
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# 概述 {#primetime-drm-interface-overview}

您可以使用Primetime数字版权管理(DRM)系统的功能来提供对视频内容的安全访问。 或者，您也可以使用第三方DRM解决方案作为Adobe集成Primetime DRM解决方案的替代方案。

<!--<a id="section_4DD54E085AB345FE9BE00865E56B28DB"></a>-->

有关第三方DRM解决方案的可用性，请咨询Adobe代表。

Primetime数字版权管理(DRM)系统的关键客户端元素是DRM管理器。 Android SDK附带的范例应用程序包括一 `DRMHelper` 个类，它演示了如何使某些DRM操作更易于实现。

Primetime DRM提供了一个可伸缩、高效的工作流，用于在TVSDK应用程序中实施内容保护。 通过为每个数字媒体文件创建许可证，您可以保护和管理视频内容的权限。

请参阅TVSDK包中包含的DRM示例播放器代码。

以下是使用DRM时最重要的API元素：

* 媒体播放器中对实现DRM子系统的DRM管理器对象的引用：

   ```java
   MediaPlayer.getDRMManager();
   ```

   >[!TIP]
   >
   >此API仅在触发 `DRMManager` 后返回有效 `MediaPlayerEvent.DRM_METADATA` 对象。 如果在此事 `getDRMManager()` 件触发之前调用，它可能返回NULL。

* 帮 `DRMHelper` 助程序类，在实现DRM工作流时非常有用。

   您可以在中 `DRMHelper` 看到 `ReferencePlayer`。

* 一种 `DRMHelper` 元数据加载器方法，当DRM元数据位于与媒体分离的URL中时，加载该元数据。

   ```java
   public static void loadDRMMetadata(final DRMManager drmManager,  
      final String drmMetadataUrl,  
      final DRMLoadMetadataListener loadMetadataListener);
   ```

* 一种 `DRMHelper` 检查DRM元数据以确定是否需要身份验证的方法。

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

<!--<a id="section_899BD9061D484E1BBA46E84617C36867"></a>-->

其他相关API元素：

* [com.adobe.ave.drm.DRMManager](https://help.adobe.com/en_US/primetime/api/drm/com/adobe/ave/drm/DRMManager.html)
* [com.adobe.ave.drm.DRMMetdata](https://help.adobe.com/en_US/primetime/api/drm/com/adobe/ave/drm/DRMMetadata.html)
* [com.adobe.ave.drm.DRMPolicy](https://help.adobe.com/en_US/primetime/api/drm/com/adobe/ave/drm/DRMPolicy.html)
* [com.adobe.ave.drm.DRMAuthenticationMethod](https://help.adobe.com/en_US/primetime/api/drm/com/adobe/ave/drm/DRMAuthenticationMethod.html)
* [com.adobe.ave.drm.DRMAuthenticationCompleteCallback](https://help.adobe.com/en_US/primetime/api/drm/com/adobe/ave/drm/DRMAuthenticationCompleteCallback.html)
* [com.adobe.ave.drm.DRMOperationErrorCallback](https://help.adobe.com/en_US/primetime/api/drm/com/adobe/ave/drm/DRMOperationErrorCallback.html)
* com.adobe.mediacore.drm.DRMAuthenticateListener

<!-- 
Comment Type: draft
(https://help.adobe.com/en_US/primetime/api/psdk/javadoc_2.4/com/adobe/mediacore/drm/DRMAuthenticateListener.html)

-->
<!--<a id="section_F58941D68EB94A5EBD1C7454D2A1B17A"></a>-->

有关DRM的详细信息，请参阅 [Adobe Primetime DRM文档](https://helpx.adobe.com/primetime/user-guide.html)。
