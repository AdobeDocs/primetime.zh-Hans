---
description: Primetime播放器支持Primetime DRM集成作为自定义DRM工作流。 这意味着您的应用程序必须在播放流之前实施DRM身份验证工作流。
title: DRM内容保护
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '366'
ht-degree: 0%

---


# DRM内容保护{#drm-content-protection}

Primetime播放器支持Primetime DRM集成作为自定义DRM工作流。 这意味着您的应用程序必须在播放流之前实施DRM身份验证工作流。

要启用此功能，TVSDK会为您提供DRM管理器以进行身份验证。 引用实现提供了以下工作流的示例：

* 如何使用Access内容保护来加载和播放HLS流，该内容保护针对低错误率和快速开始进行了优化。
* 如何使用AES128内容保护加载和播放HLS流。
* 如何使用PHLS内容保护来加载和播放HLS流，该保护针对低错误率和快速开始进行了优化。

所有受DRM保护的内容都由TVSDK中内置的DRM库自动处理。 但是，您可以使用TVSDK API回调公开错误处理、设备个性化优化和许可证获取。

## 为播放器{#section_F1FC4322C35C4FE8A3B47FDC0A74221B}添加内容保护

可以通过创建播放管理器或使用管理器工厂为播放器添加内容保护。

要创建内容保护管理器，请执行以下操作：

* 初始化DRM系统。

   下面的代码示例显示了如何在应用程序`onCreate()`函数中调用`loadDRMServices`，以确保在播放启动之前启动DRM系统所需的任何初始化。

   ```java
   @Override 
    public void onCreate() { 
        super.onCreate();  
        DrmManager.loadDRMServices(getApplicationContext()); 
    }
   ```

* 预载DRM许可证。

   下面的代码示例显示当内容列表完成加载时加载`VideoItems`。 这将导致从许可证服务器获取DRM许可证并在本地缓存，这样，在播放开始时，内容将以最小延迟加载。

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
   >您可以在“设置”用户界面中将Precache DRM许可证设置为“打开”，以在加载内容时预缓存DRM许可证。 但是，最佳实践是预载特定项目，而不是预先预定目录中的所有许可证。
   >
   >![](assets/precache-drm-licenses.jpg)

* 要使用`ManagerFactory`实现DRM错误处理，请确保在[!DNL PlayerFragment.java]文件中包含以下代码行：

   ```java
   drmManager = ManagerFactory.getDrmManager(config, mediaPlayer);
   ```

**相关API文档**

* [类DrmManager](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/manager/DrmManager.html)
* [DrmManagerEventListener](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/manager/DrmManager.DrmManagerEventListener.html)