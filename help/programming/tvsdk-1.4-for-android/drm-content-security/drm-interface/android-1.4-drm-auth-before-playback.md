---
description: 当视频的DRM元数据与媒体流分开时，请在开始播放之前执行身份验证。
title: 播放前的DRM验证
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '338'
ht-degree: 0%

---

# 播放前的DRM验证 {#drm-authentication-before-playback}

当视频的DRM元数据与媒体流分开时，请在开始播放之前执行身份验证。

视频资产可以具有关联的DRM元数据文件。 例如：

* &quot;url&quot;： &quot;ht<span></span>tps://www.domain.com/asset.m3u8”
* &quot;drmMetadata&quot;： &quot;ht<span></span>tps://www.domain.com/asset.metadata”

如果是这种情况，请使用 `DRMHelper` 方法下载DRM元数据文件的内容，解析该文件，并检查是否需要DRM身份验证。

1. 使用 `loadDRMMetadata` 加载元数据URL内容并将下载的字节解析为 `DRMMetadata`.

   与任何其他网络操作一样，此方法也是异步的，会创建自己的线程。

   ```java
   public static void loadDRMMetadata( 
       final DRMManager drmManager, 
       final String drmMetadataUrl,  
       final DRMLoadMetadataListener loadMetadataListener); 
   ```

   例如：

   ```java
   DRMHelper.loadDRMMetadata(drmManager, metadataURL, new DRMLoadMetadataListener());
   ```

1. 由于操作是异步执行的，因此最好让用户意识到这一点。 否则，他会奇怪为什么他的播放没有开始。 例如，在下载和解析DRM元数据时显示旋转滚轮。
1. 在中实施回调 `DRMLoadMetadataListener`. 此 `loadDRMMetadata` 调用这些事件处理程序（调度这些事件）。

   ```java
   public interface  
    <b>DRMLoadMetadataListener</b> { 
    public void  
    <b>onLoadMetadataUrlStart</b>(); 
    /** 
     * @param authNeeded 
     * whether DRM authentication is needed. 
     * @param drmMetadata 
     * the parsed DRMMetadata obtained.    */ 
    public void  
    <b>onLoadMetadataUrlComplete</b>(boolean authNeeded, DRMMetadata drmMetadata); 
    public void  
    <b>onLoadMetadataUrlError</b>(); 
   }
   ```

   * `onLoadMetadataUrlStart` 检测元数据URL何时开始加载。
   * `onLoadMetadataUrlComplete` 检测元数据URL何时完成加载。
   * `onLoadMetadataUrlError` 指示元数据加载失败。

1. 加载完成后，检查 `DRMMetadata` 对象以查看是否需要DRM身份验证。

   ```java
   public static boolean <b>isAuthNeeded</b>(DRMMetadata drmMetadata);
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
   ```

1. 如果不需要身份验证，则开始播放。
1. 如果需要身份验证，请通过获取许可证来执行身份验证。

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

   为了简单起见，此示例显式编码用户名称和密码。

   ```java
   DRMHelper.performDrmAuthentication(drmManager, drmMetadata, DRM_USERNAME, DRM_PASSWORD,  
     new DRMAuthenticationListener() { 
       @Override 
       public void onAuthenticationStart() { 
           Log.i(LOG_TAG + "#onAuthenticationStart", "DRM authentication started."); 
           // Spinner is already showing. 
       } 
       @Override 
       public void onAuthenticationError(int major, int minor, String errorString, String serverErrorURL) {  
           Log.e(LOG_TAG + "#onAuthenticationError", "DRM authentication failed. " +  
             major + " 0x" + Long.toHexString(minor)); 
           showToast(getString(R.string.drmAuthenticationError));   
           showLoadingSpinner(false); 
       } 
       @Override 
       public void onAuthenticationComplete(byte[] authenticationToken) { 
           Log.i(LOG_TAG + "#onAuthenticationComplete", "Auth successful. Launching content."); 
           showLoadingSpinner(false); 
           startPlayerActivity(ASSET_URL); 
       } 
   }); 
   ```

1. 这也意味着网络通信，因此这也是异步操作。 使用事件侦听器检查身份验证状态。

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
       public void onAuthenticationError(int major, int minor,  
         String errorString, String serverErrorURL); 
   } 
   ```

1. 如果身份验证成功，则开始播放。
1. 如果身份验证不成功，则通知用户，并且不要开始播放。

您的应用程序必须处理任何身份验证错误。 未能在播放之前成功进行身份验证，会导致TVSDK进入错误状态。 即，它将其状态更改为ERROR，生成包含DRM库中的错误代码的错误，并且播放停止。 您的应用程序必须解决问题，重置播放器，然后重新加载资源。
