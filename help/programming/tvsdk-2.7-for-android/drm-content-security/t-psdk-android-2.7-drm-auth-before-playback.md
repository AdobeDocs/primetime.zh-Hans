---
description: 当视频的DRM元数据与媒体流分开时，您应在开始播放之前进行身份验证。
title: 播放前的DRM验证
exl-id: b3267363-f734-44a6-99f5-e155deb53f3e
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '339'
ht-degree: 0%

---

# 播放前的DRM验证 {#drm-authentication-before-playback}

当视频的DRM元数据与媒体流分开时，您应在开始播放之前进行身份验证。

视频资源可以具有关联的DRM元数据文件，例如：

* `"url": "https://www.domain.com/asset.m3u8"`
* `"drmMetadata": "https://www.domain.com/asset.metadata"`

在此示例中，您可以使用 `DRMHelper` 方法下载DRM元数据文件的内容、解析该文件并检查是否需要DRM身份验证。

1. 使用 `loadDRMMetadata` 加载元数据URL内容并将下载的字节解析为 `DRMMetadata`.

   >[!TIP]
   >
   >此方法是异步的，它创建自己的线程。

   ```java
   public static void loadDRMMetadata( 
       final DRMManager drmManager, 
       final String drmMetadataUrl,  
       final DRMLoadMetadataListener loadMetadataListener); 
   ```

   例如：

   ```java
   DRMHelper.loadDRMMetadata(drmManager,  
                                      metadataURL,  
                                      new DRMLoadMetadataListener());
   ```

1. 通知用户此操作是异步执行的，最好让用户意识到这一点。

   如果用户不知道该操作是异步执行的，他们可能会想知道为什么尚未开始播放。 例如，您可以在下载和解析DRM元数据时显示旋转滚轮。

1. 在中实施回调 `DRMLoadMetadataListener`.

   此 `loadDRMMetadata` 调用这些事件处理程序。

   ```java
   public interface DRMLoadMetadataListener { 
   
       public void onLoadMetadataUrlStart(); 
   
       /** 
       * @param authNeeded 
       * whether DRM authentication is needed. 
       * @param drmMetadata 
       * the parsed DRMMetadata obtained.    */ 
       public void onLoadMetadataUrlComplete(boolean authNeeded, DRMMetadata drmMetadata); 
       public void onLoadMetadataUrlError(); 
   } 
   ```

   以下是有关处理程序的其他详细信息：

   * `onLoadMetadataUrlStart` 检测元数据URL加载何时开始。
   * `onLoadMetadataUrlComplete` 检测元数据URL何时完成加载。
   * `onLoadMetadataUrlError` 指示元数据加载失败。

1. 加载完成后，检查 `DRMMetadata` 用于确定是否需要进行DRM身份验证的对象。

   ```java
   public static boolean isAuthNeeded(DRMMetadata drmMetadata);
   ```

   例如：

   ```java
   @Override 
   public void onLoadMetadataUrlComplete(boolean authNeeded, DRMMetadata drmMetadata) {  
       Log.i(LOG_TAG + "#onLoadMetadataUrlComplete",  
             "Loaded metadata URL contents. Auth needed:" + authNeeded + "."); 
       if (!authNeeded) { 
           // Auth is not required. Start player activity.     
           showLoadingSpinner(false);     
           startPlayerActivity(ASSET_URL); 
           return; 
       } 
   } 
   ```

1. 完成以下任务之一：

   * 如果不需要身份验证，则开始播放。
   * 如果需要身份验证，请获取许可证以完成身份验证。

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
      */ 
      public static void performDrmAuthentication( 
           final DRMManager drmManager,  
           final DRMMetadata drmMetadata, 
           final String authUser,  
           final String authPass,  
           final DRMAuthenticationListener authenticationListener);
      ```

      在本例中，为了简化起见，明确对用户名和密码进行了编码：

      ```java
      DRMHelper.performDrmAuthentication(drmManager,  
                                         drmMetadata,  
                                         DRM_USERNAME,  
                                         DRM_PASSWORD, new DRMAuthenticationListener() { 
          @Override 
          public void onAuthenticationStart() { 
              Log.i(LOG_TAG + "#onAuthenticationStart", "DRM authentication started."); 
              // Spinner is already showing. 
          } 
          @Override 
          public void onAuthenticationError(int major,  
                                            int minor,  
                                            String errorString,  
                                            String serverErrorURL) { 
              Log.e(LOG_TAG +  
                    "#onAuthenticationError",  
                    "DRM authentication failed. " +  
                    major + " 0x" + Long.toHexString(minor)); 
              showToast(getString(R.string.drmAuthenticationError));   
              showLoadingSpinner(false); 
          } 
          @Override 
          public void onAuthenticationComplete(byte[] authenticationToken) { 
              Log.i(LOG_TAG +  
                    "#onAuthenticationComplete", "Auth successful. Launching content."); 
              showLoadingSpinner(false); 
              startPlayerActivity(ASSET_URL); 
          } 
      }); 
      ```

1. 使用事件侦听器检查身份验证状态。

   此过程意味着网络通信，因此这也是异步操作。

   ```java
   public interface DRMAuthenticationListener { 
       /** 
       * Called to indicate that DRM authentication has started. 
       */ 
       public void onAuthenticationStart(); 
       /** 
       * Called to indicate that DRM authentication has been successful. 
       * 
       * @param authenticationToken 
       * the obtained token, which can be stored locally. 
       */ 
       public void onAuthenticationComplete(byte[] authenticationToken); 
       /** 
       * Called to indicate that an error occurred while performing the DRM 
       * authentication. 
       * 
       * @param major 
       * the major code. 
       * @param minorC 
       * the minor code. 
       * @param errorString 
       * the exception thrown. 
       * @param serverErrorURL 
       * the URL of the server  
       * on which the error occurred 
       */ 
       public void onAuthenticationError(int major,  
                                         int minor,  
                                         String errorString,  
                                         String serverErrorURL); 
   } 
   ```

1. 如果身份验证成功，则开始播放。
1. 如果身份验证失败，请通知用户，并且不要开始播放。

   您的应用程序必须处理任何身份验证错误。 如果在播放之前未能成功进行身份验证，则会导致TVSDK处于错误状态，并且播放停止。 您的应用程序必须解决此问题，重置播放器，然后重新加载资源。
