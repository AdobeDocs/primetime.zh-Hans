---
description: 当视频的DRM元数据包含在媒体流中时，您可以在播放期间执行身份验证。
title: 在播放期间DRM验证
exl-id: fb244aad-38ae-4bc7-85b7-364cf59db8d6
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '194'
ht-degree: 0%

---

# 在播放期间DRM验证 {#drm-authentication-during-playback}

当视频的DRM元数据包含在媒体流中时，您可以在播放期间执行身份验证。

通过许可证轮换，使用多个DRM许可证对资产进行加密。 每次发现新的DRM元数据时， `DRMHelper` 方法用于检查DRM元数据是否需要DRM身份验证。

>[!TIP]
>
>在开始播放之前，请确定您是否在处理绑定域的许可证，以及是否需要域身份验证。 如果是，则完成域身份验证并加入域。

1. 当在资产中发现新的DRM元数据时，将在应用层发送事件。

   ```java
   mediaPlayer.addEventListener(MediaPlayerEvent.DRM_METADATA,  
                                drmMetadataInfoEventListener); 
   
   DRMMetadataInfoEventListener drmMetadataInfoEventListener =  
     new DRMMetadataInfoEventListener() { 
       @Override 
       public void onDRMMetadataInfo(DRMMetadataInfoEvent drmMetadataInfoEvent) { 
           ... 
       } 
   };
   ```

1. 使用 `DRMMetadata` 以检查是否需要身份验证。

   * 如果不需要进行身份验证，则无需执行任何操作，并且播放将继续进行，不会出现中断。
   * 如果需要身份验证，请完成DRM身份验证。

      由于此操作是异步执行的，并且是在其他线程中处理的，因此它不会影响用户界面，也不会影响视频播放。

1. 如果身份验证失败，则用户无法继续查看视频，并且播放停止。

<!--<a id="example_939B95F831A245869F9248E2767F260C"></a>-->

例如：

```java
DRMMetadataInfoEventListener drmMetadataInfoEventListener =  
  new DRMMetadataInfoEventListener() { 
    @Override 
    public void onDRMMetadataInfo(DRMMetadataInfoEvent drmMetadataInfoEvent) { 
        final DRMMetadataInfo drmMetadataInfo =  
          drmMetadataInfoEvent.getDRMMetadataInfo(); 
 
        if (drmMetadataInfo == null ||  
          !DRMHelper.isAuthNeeded(drmMetadataInfo.getDRMMetadata())) { 
            return; 
        } 
 
        // Perform DRM auth. 
        // Possible logic might take into consideration a threshold between the  
        // current player time and the DRM metadata start time. For the time being,  
        // we resolve it as soon as we receive the DRM metadata. 
 
        DRMManager drmManager = _mediaPlayer.getDRMManager(); 
        if (drmManager == null) { 
            return; 
        } 
 
        SharedPreferences sharedPreferences =  
          PreferenceManager.getDefaultSharedPreferences(getActivity()); 
        String authUser = sharedPreferences.getString(PrimetimeReference.SETTINGS_DRM_USERNAME,  
          getResources().getString(R.string.drmUsername)); 
        String authPass = sharedPreferences.getString(PrimetimeReference.SETTINGS_DRM_PASSWORD,  
          getResources().getString(R.string.drmPassword)); 
 
        DRMHelper.performDrmAuthentication(drmManager, drmMetadataInfo.getDRMMetadata(),  
          authUser, authPass, new DRMAuthenticationListener() { 
 
            @Override 
            public void onAuthenticationStart() { 
                ... 
            } 
 
            @Override 
            public void onAuthenticationError(int major,  
                                              int minor,  
                                              String erroString,  
                                              String serverErrorURL) { 
                if (getActivity() == null) { 
                    return; 
                } 
                _handler.post(new Runnable() { 
                    @Override 
                    public void run() { 
                        showToast(getString(R.string.drmAuthenticationError)); 
                        getActivity().finish(); 
                    } 
                }); 
            } 
 
            @Override 
            public void onAuthenticationComplete(byte[] authenticationToken) { 
            } 
 
        }); 
    } 
}; 
```
