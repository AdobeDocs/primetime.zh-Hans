---
seo-title: 许可证获取过程详细信息
title: 许可证获取过程详细信息
uuid: 4825c49e-fa6f-4c98-9d21-a2743930ca2e
translation-type: tm+mt
source-git-commit: 3fdef12b717bb6f70ca27d9278de61d709f8349c

---


# 许可证获取过程详细信息 {#license-acquisition-process-details}

此过程显示Primetime DRM受保护内容工作流程的详细API级视图：

1. 使用对 `URLLoader` 象，加载受保护内容的元数据文件的字节。

   将此对象设置为变量，如 `metadata_bytes`。 所有由Primetime DRM控制的内容都包含Primetime DRM元数据。 打包内容时，此元数据可以与内容一起另存为单独的元数据文件( [!DNL .metadata])。 或者，元数据可以采用Base64编码并插入到视频清单文件的正文中。 有关详细信息，请参阅 [打包媒体文件](../protecting-content/packaging-media-overview/packaging-media-files.md)。
   1. 如有必要，请从字符串 `!` 的开头删除感叹号。
   1. 如果HLS或HDS内容需要，请在传递之前将Base64编码字符串中包含的元数据解码为二进制数据。
1. 创建实 `DRMContentData` 例。

   将此代码放入try-catch块中：

   ```
   new DRMContentData(metadata_bytes)
   ```

   其中 `metadata_bytes` 是步骤 `URLLoader` 1中获取的对象。

   [iOS:DRMMetadata](https://help.adobe.com/en_US/primetime/api/drm-apis/client/ios/interface_d_r_m_metadata.html)

   [Android:DRMMetadata](https://help.adobe.com/en_US/primetime/api/drm-apis/client/android/index.html)

1. 创建监听器以监听对 `DRMStatusEvent` 象 `DRMErrorEvent` 并从对象调 `DRMManager` 度。

   ```
   DRMManager.addEventListener(DRMStatusEvent.DRM_STATUS, onDRMStatus); 
   DRMManager.addEventListener(DRMErrorEvent.DRM_ERROR, onDRMError);
   ```

   在监听 `DRMStatusEvent` 器中，检查许可证是否有效（非空）。 在监听 `DRMErrorEvent` 器中，处理 `DRMErrorEvents`。 请参 *阅本指南中的使用DRMStatusEvent类**和使用DRMErrorEvent类* 。

1. 加载播放内容所需的许可证。
首先，尝试加载本地存储的许可证以播放内容：

   ```
   DRMManager.loadvoucher(drmContentData, LoadVoucherSetting.LOCAL_ONLY)
   ```

   [Android:DRMManager.acquireLicense()](https://help.adobe.com/en_US/primetime/api/drm-apis/client/android/com/adobe/ave/drm/DRMManager.html#acquireLicense(com.adobe.ave.drm.DRMMetadata,%20com.adobe.ave.drm.DRMAcquireLicenseSettings,%20com.adobe.ave.drm.DRMOperationErrorCallback,%20com.adobe.ave.drm.DRMLicenseAcquiredCallback))

   [iOS:acquireLicense:](https://help.adobe.com/en_US/primetime/api/drm-apis/client/ios/interface_d_r_m_manager.html#a52accb5ed5b49d6e5d91277d78279f1b)

   加载完成后，对象 `DRMManager` 将调度 `DRMStatusEvent.DRM_Status`。

1. 检查对 `DRMVoucher` 象。


   如果对 `DRMVoucher` 象不为null，则许可证有效。 转到步骤9。

   [Android:DRMLicenseApperiedCallback](https://help.adobe.com/en_US/primetime/api/drm-apis/client/android/com/adobe/ave/drm/DRMLicenseAcquiredCallback.html)

   [iOS:DRMLicenseAppired](https://help.adobe.com/en_US/primetime/api/drm-apis/client/ios/_d_r_m_interface_8h.html#afe5a9e3a003f312ee268d9b00927fa6d)
1. 检查此内容的策略所需的身份验证方法。

   使用属 `DRMContentData.authenticationMethod` 性。
   1. 如果身份验证方 `ANONYMOUS`法为，请转到步骤9。 

      [Android:DRMAuthenticationMethod](https://help.adobe.com/en_US/primetime/api/drm-apis/client/android/index.html?com/adobe/ave/drm/DRMLicenseAcquiredCallback.html)

      [iOS:DRMAuthenticationMethod](https://help.adobe.com/en_US/primetime/api/drm-apis/client/ios/_d_r_m_interface_8h.html#a2003f29af93898b52a4123c2dd92c457)
   1. 如果身份验证方 `USERNAME_AND_PASSWORD`法为，则应用程序必须提供允许用户输入凭据的机制。

      将用户凭据传递给许可证服务器以验证用户身份：

      ```
      DRMManager.authenticate( metadata.serverURL, metadata.domain, username, password)
      ```

      如果身 `DRMManager` 份验证 `DRMAuthenticationErrorEvent` 失败，则将调度一个，或 `DRMAuthenticationCompleteEvent` 者如果身份验证成功。 为这些事件创建监听器。

      [Android:authenticate()](https://help.adobe.com/en_US/primetime/api/drm-apis/client/android/com/adobe/ave/drm/DRMManager.html#authenticate(com.adobe.ave.drm.DRMMetadata,%20java.lang.String,%20java.lang.String,%20java.lang.String,%20java.lang.String,%20com.adobe.ave.drm.DRMOperationErrorCallback,%20com.adobe.ave.drm.DRMAuthenticationCompleteCallback))

      [iOS:身份验证：](https://help.adobe.com/en_US/primetime/api/drm-apis/client/ios/interface_d_r_m_manager.html#a169c1441f196a834094a8e0f5ecb4aca)

      >[!NOTE]
      >
      >Adobe建议使用更安全的机制提供凭据。 有关参考，请参 [阅KeyGenParameterSpec](https://developer.android.com/reference/android/security/keystore/KeyGenParameterSpec.html)。

   1. 如果身份验证方 `UNKNOWN`法为，则必须使用自定义身份验证方法。

      在这种情况下，内容提供商已安排以带外方式进行身份验证，而不是使用Primetime API。 自定义身份验证过程必须生成可传递给方法的身份验证 `DRMManager.setAuthenticationToken()` 令牌。

      [Android:setAuthenticationToken()](https://help.adobe.com/en_US/primetime/api/drm-apis/client/android/com/adobe/ave/drm/DRMManager.html#setAuthenticationToken(com.adobe.ave.drm.DRMMetadata,%20java.lang.String,%20byte[],%20com.adobe.ave.drm.DRMOperationErrorCallback,%20com.adobe.ave.drm.DRMOperationCompleteCallback))

      [iOS:setAuthenticationToken:](https://help.adobe.com/en_US/primetime/api/drm-apis/client/ios/interface_d_r_m_manager.html#a17884b5d9bcc5b0b39503f61140f9b09)

      >[!NOTE]
      >
      >或者，无论使用哪种验证方 `.setAuthenticationToken()` 法，都可用于将自定义数据从客户端发送到许可证服务器。 这是API的过载，因为此机制是在获取许可证时将动态自定义数据从客户端发送到许可证服务器的唯一方法。 在 [Primetime DRM(Adobe Access)论坛的多个论坛帖子中，对自定义数据传输方法进行了深入讨论 ](https://forums.adobe.com/community/adobe_access)。

1. 如果身份验证失败，您的应用程序必须返回步骤6。

   确保您的应用程序具有处理和限制重复身份验证失败的机制。 例如，在三次尝试后，您向用户显示一条消息，指示身份验证失败且无法播放内容。
1. 要使用存储的令牌而不是提示用户输入凭据，请使用方法设置 `DRMManager.setAuthenticationToken()` 令牌。

   然后，您从许可证服务器下载许可证并按步骤6播放内容。
   1. **可选：** 如果身份验证成功，您可以捕获身份验证令牌，该令牌是缓存在内存中的字节数组。

      将此令牌与属性一起 `DRMAuthenticationCompleteEvent.token` 获取。 您可以存储和使用身份验证令牌，这样用户就不必重复输入此内容的凭据。 许可证服务器确定验证令牌的有效期。

      [Android:OperationComplete()](https://help.adobe.com/en_US/primetime/api/drm-apis/client/android/com/adobe/ave/drm/DRMOperationCompleteCallback.html)

      [iOS:DRMOperationComplete](https://help.adobe.com/en_US/primetime/api/drm-apis/client/ios/_d_r_m_interface_8h.html#a5f2392ec6661b51bf7b0df71cd514731)
1. 如果身份验证成功，请从许可证服务器下载许可证：

   ```
   DRMManager.loadvoucher( 
      drmContentData, 
      LoadVoucherSetting.FORCE_REFRESH)
   ```

   加载完成后，对象 `DRMManager` 将调度 `DRMStatusEvent.DRM_STATUS`。 侦听此事件，调度该事件后，您可以播放内容。  通过创建Primetime对象并调用其方法播放视 `play()` 频：

   ```
   stream = new Primetime(connection); 
   stream.addEventListener(DRMStatusEvent.DRM _STATUS, drmStatusHandler); 
   stream.addEventListener(DRMErrorEvent.DRM_ERROR, drmErrorHandler); 
   stream.addEventListener(NetStatusEvent.NET_STATUS, netStatusHandler); 
   stream.client = new CustomClient(); 
   video.attachPrimetime(stream); 
   stream.play(videoURL);
   ```

   [Android:acquireLicense()](https://help.adobe.com/en_US/primetime/api/drm-apis/client/android/com/adobe/ave/drm/DRMManager.html#acquireLicense(com.adobe.ave.drm.DRMMetadata,%20com.adobe.ave.drm.DRMAcquireLicenseSettings,%20com.adobe.ave.drm.DRMOperationErrorCallback,%20com.adobe.ave.drm.DRMLicenseAcquiredCallback))

   [iOS:acquireLicense:](https://help.adobe.com/en_US/primetime/api/drm-apis/client/ios/interface_d_r_m_manager.html#a52accb5ed5b49d6e5d91277d78279f1b)