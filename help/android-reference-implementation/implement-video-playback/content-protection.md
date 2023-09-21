---
description: Primetime播放器支持将Primetime DRM集成作为自定义DRM工作流。 这意味着您的应用程序必须在播放流之前实施DRM身份验证工作流。
title: DRM内容保护
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '366'
ht-degree: 0%

---

# DRM内容保护 {#drm-content-protection}

Primetime播放器支持将Primetime DRM集成作为自定义DRM工作流。 这意味着您的应用程序必须在播放流之前实施DRM身份验证工作流。

要启用此功能，TVSDK为您提供用于身份验证的DRM管理器。 参考实施提供了以下工作流的示例：

* 如何使用访问内容保护加载和播放HLS流，该保护针对低错误率和快速启动进行了优化。
* 如何加载和播放具有AES128内容保护的HLS流。
* 如何加载和播放具有PHLS内容保护的HLS流，该保护针对低错误率和快速启动进行了优化。

所有受DRM保护的内容都由内置到TVSDK中的DRM库自动处理。 但是，您可以使用TVSDK API回调公开错误处理、设备个性化优化和许可证获取。

## 向播放器添加内容保护 {#section_F1FC4322C35C4FE8A3B47FDC0A74221B}

您可以通过创建播放管理器或使用管理器工厂为播放器添加内容保护。

要创建内容保护管理器，请执行以下操作：

* 初始化DRM系统。

  以下代码示例显示了调用 `loadDRMServices` 在应用程序中 `onCreate()` 功能，以确保在开始播放之前启动DRM系统所需的任何初始化。

  ```java
  @Override 
   public void onCreate() { 
       super.onCreate();  
       DrmManager.loadDRMServices(getApplicationContext()); 
   }
  ```

* 预加载DRM许可证。

  以下代码示例显示了如何加载 `VideoItems` 内容列表完成加载时。 这将导致从许可证服务器获取DRM许可证并缓存到本地，以便当播放开始时，以最小的延迟加载内容。

  ```java
  DrmManager.preLoadDrmLicenses(item.getUrl(),  
    new MediaPlayerItemLoader.LoaderListener() { 
  
      @Override 
      public void onLoadComplete(MediaPlayerItem item) { 
          Player.logger.w(LOG_TAG + "::DRMPreload#onLoadComplete", item.getResource().getUrl()); 
      } 
  
      @Override 
      public void onError(MediaErrorCode errorCode, String s) { 
          Player.logger.e(LOG_TAG + "::DRMPreload#onError", s); 
      } 
  } 
  ```

  >[!NOTE]
  >
  >您可以在“设置”用户界面中将Precache DRM许可证设置为ON，以便在加载内容时预缓存DRM许可证。 但是，最佳实践是预加载特定项目，而不是预加载目录中的所有许可证。
  >
  >![](assets/precache-drm-licenses.jpg)

* 使用 `ManagerFactory` 要实施DRM错误处理，请确保以下代码行位于 [!DNL PlayerFragment.java] 文件：

  ```java
  drmManager = ManagerFactory.getDrmManager(config, mediaPlayer);
  ```

**相关API文档**

* [类DrmManager](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/manager/DrmManager.html)
* [DrmManagerEventListener](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/manager/DrmManager.DrmManagerEventListener.html)
