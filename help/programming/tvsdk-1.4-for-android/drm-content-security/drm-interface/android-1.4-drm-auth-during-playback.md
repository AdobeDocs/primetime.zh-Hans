---
description: 当视频的DRM元数据包含在媒体流中时，在播放期间执行身份验证。
seo-description: 当视频的DRM元数据包含在媒体流中时，在播放期间执行身份验证。
seo-title: 播放期间的DRM身份验证
title: 播放期间的DRM身份验证
uuid: a1a63e3e-be34-49e1-96c4-ae266003b3d1
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# 播放期间的DRM身份验证 {#drm-authentication-during-playback}

当视频的DRM元数据包含在媒体流中时，在播放期间执行身份验证。

请考虑许可证轮换功能，该功能中的资产使用多个DRM许可证进行加密。 每次发现新的DRM元数据时，都使用 `DRMHelper` 方法检查DRM元数据是否需要DRM身份验证。

>[!NOTE]
>
>本教程不处理域绑定许可证。 理想情况下，在开始播放之前，请检查您是否在处理域绑定许可证。 如果是，请执行域身份验证（如果需要）并加入域。

1. 在资产中发现新的DRM元数据时，将在应用程序层调度一个事件。

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

1. 使用 `DRMMetadata` 检查是否需要身份验证。 如果没有，则不做；播放继续不间断。
1. 否则，请执行DRM身份验证。 由于此操作是异步的，并且是在不同的线程中处理的，因此它对用户界面和视频回放没有影响。
1. 如果身份验证失败，用户将无法继续观看视频，并停止播放。 否则，将继续不间断播放。

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
