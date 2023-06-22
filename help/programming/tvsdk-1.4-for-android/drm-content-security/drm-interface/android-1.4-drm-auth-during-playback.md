---
description: 当视频的DRM元数据包含在媒体流中时，在播放期间执行身份验证。
title: 在播放期间DRM验证
exl-id: 3f190d37-291e-4a5e-811d-7e9984a6a44a
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '186'
ht-degree: 0%

---

# 在播放期间DRM验证 {#drm-authentication-during-playback}

当视频的DRM元数据包含在媒体流中时，在播放期间执行身份验证。

考虑使用许可证轮换功能，其中使用多个DRM许可证对资产进行加密。 每次发现新的DRM元数据时，请使用 `DRMHelper` 检查DRM元数据是否需要DRM身份验证的方法。

>[!NOTE]
>
>本教程不处理绑定域的许可证。 理想情况下，在开始播放之前，请检查您是否在处理域绑定的许可证。 如果是，则执行域身份验证（如果需要）并加入域。

1. 当在资产中发现新的DRM元数据时，将在应用层发送事件。

   ```java
   mediaPlayer.addEventListener(MediaPlayerEvent.DRM_METADATA,  
                                drmMetadataInfoEventListener); 
   
   DRMMetadataInfoEventListener drmMetadataInfoEventListener =  
     new DRMMetadataInfoEventListener() { 
           @Override 
           public void onDRMMetadataInfo(DRMMetadataInfoEvent drmMetadataInfoEvent) { 
           } 
   };
   ```

1. 使用 `DRMMetadata` 以检查是否需要身份验证。 如果不能，则不执行任何操作；播放将继续进行，不会出现中断。
1. 否则，执行DRM验证。 由于此操作是异步执行的，并且是在其他线程中处理的，因此它不会影响用户界面，也不会影响视频播放。
1. 如果身份验证失败，用户将无法继续查看视频，并且播放将停止。 否则，播放将继续无中断进行。

```java
DRMMetadataInfoEventListener drmMetadataInfoEventListener =  
  new DRMMetadataInfoEventListener() { 
    @Override 
    public void onDRMMetadataInfo(DRMMetadataInfoEvent drmMetadataInfoEvent) { 
        final DRMMetadataInfo drmMetadataInfo = drmMetadataInfoEvent.getDRMMetadataInfo(); 
 
        if (drmMetadataInfo == null || !DRMHelper.isAuthNeeded(drmMetadataInfo.getDRMMetadata())) { 
            return; 
        } 
 
        // Perform DRM auth. 
        // Possible logic might take into consideration a threshold between the current player time and the 
        // DRM metadata start time. For the time being, we resolve it as soon as we receive the DRM metadata. 
 
        DRMManager drmManager = _mediaPlayer.getDRMManager(); 
        if (drmManager == null) { 
            return; 
        } 
 
        SharedPreferences sharedPreferences = PreferenceManager.getDefaultSharedPreferences(getActivity()); 
        String authUser = sharedPreferences.getString(PrimetimeReference.SETTINGS_DRM_USERNAME,  
          getResources().getString(R.string.drmUsername)); 
          String authPass = sharedPreferences.getString(PrimetimeReference.SETTINGS_DRM_PASSWORD,  
          getResources().getString(R.string.drmPassword)); 
 
        DRMHelper.performDrmAuthentication(drmManager, drmMetadataInfo.getDRMMetadata(),  
          authUser, authPass, new DRMAuthenticationListener() { 
 
            @Override 
            public void onAuthenticationStart() { 
            } 
 
            @Override 
            public void onAuthenticationError(int major, int minor, String erroString, String serverErrorURL) { 
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
