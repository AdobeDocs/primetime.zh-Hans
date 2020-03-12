---
description: 当视频的DRM元数据包含在媒体流中时，您可以在播放期间执行身份验证。
seo-description: 当视频的DRM元数据包含在媒体流中时，您可以在播放期间执行身份验证。
seo-title: 播放期间的DRM身份验证
title: 播放期间的DRM身份验证
uuid: d44acfb2-796b-4c60-b622-db01e58042cc
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b

---


# 播放期间的DRM身份验证 {#drm-authentication-during-playback}

当视频的DRM元数据包含在媒体流中时，您可以在播放期间执行身份验证。

借助许可证轮替，一个资产将用多个DRM许可证加密。 每次发现新的DRM元数据时，都 `DRMHelper` 会使用这些方法检查DRM元数据是否需要DRM身份验证。

>[!TIP]
>
>在开始播放之前，确定您是否在处理域绑定许可证以及是否需要域身份验证。 如果是，请完成域身份验证并加入域。

1. 在资产中发现新的DRM元数据时，将在应用程序层调度一个事件。

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

1. 使用 `DRMMetadata` 检查是否需要身份验证。

   * 如果不需要身份验证，则无需执行任何操作，并且回放将继续不间断。
   * 如果需要身份验证，请完成DRM身份验证。

      由于此操作是异步的，并且是在不同的线程中处理的，因此它对用户界面和视频回放没有影响。

1. 如果身份验证失败，用户无法继续观看视频，并且播放停止。

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
