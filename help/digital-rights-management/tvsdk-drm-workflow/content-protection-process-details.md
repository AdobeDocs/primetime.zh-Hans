---
title: 许可证获取流程详细信息
description: 许可证获取流程详细信息
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '968'
ht-degree: 0%

---

# 许可证获取流程详细信息 {#license-acquisition-process-details}

此流程提供了Primetime DRM受保护内容工作流的详细API级别视图：

1. 使用 `URLLoader` 对象，加载受保护内容元数据文件的字节。

   将此对象设置为变量，例如 `metadata_bytes`. 所有由Primetime DRM控制的内容均具有Primetime DRM元数据。 在打包内容时，此元数据可以另存为单独的元数据文件( [!DNL .metadata])作为分隔符。 或者，元数据可以是Base64编码并插入到视频清单文件的正文中。 有关更多信息，请参阅 [正在打包媒体文件](../protecting-content/packaging-media-overview/packaging-media-files.md).
   1. 如有必要，请移除感叹号 `!` 从字符串的开头开始。
   1. 如果是HLS或HDS内容所必需的，请先将Base64编码的字符串中包含的元数据解码为二进制数据，然后再传递该数据。
1. 创建 `DRMContentData` 实例。

   将此代码置于try-catch块中：

   ```
   new DRMContentData(metadata_bytes)
   ```

   位置 `metadata_bytes` 是 `URLLoader` 步骤1中获得的对象。

   [iOS： DRMetadata](https://help.adobe.com/en_US/primetime/api/drm-apis/client/ios/interface_d_r_m_metadata.html)

   [Android：DRMMetadata](https://help.adobe.com/en_US/primetime/api/drm-apis/client/android/index.html)

1. 创建监听程序以监听 `DRMStatusEvent` 和 `DRMErrorEvent` 分派自 `DRMManager` 对象。

   ```
   DRMManager.addEventListener(DRMStatusEvent.DRM_STATUS, onDRMStatus); 
   DRMManager.addEventListener(DRMErrorEvent.DRM_ERROR, onDRMError);
   ```

   在 `DRMStatusEvent` 侦听器，检查许可证是否有效（不是null）。 在 `DRMErrorEvent` 侦听器，句柄 `DRMErrorEvents`. 请参阅 *使用DRMStatusEvent类* 和 *使用DRMErrorEvent类* 本指南内容。

1. 加载播放内容所需的许可证。
首先，尝试加载本地存储的许可证以播放内容：

   ```
   DRMManager.loadvoucher(drmContentData, LoadVoucherSetting.LOCAL_ONLY)
   ```

   [Android：DRMManager.acquireLicense()](https://help.adobe.com/en_US/primetime/api/drm-apis/client/android/com/adobe/ave/drm/DRMManager.html#acquireLicense(com.adobe.ave.drm.DRMMetadata,%20com.adobe.ave.drm.DRMAcquireLicenseSettings,%20com.adobe.ave.drm.DRMOperationErrorCallback,%20com.adobe.ave.drm.DRMLicenseAcquiredCallback))

   [iOS：acquireLicense：](https://help.adobe.com/en_US/primetime/api/drm-apis/client/ios/interface_d_r_m_manager.html#a52accb5ed5b49d6e5d91277d78279f1b)

   加载完成后， `DRMManager` 对象调度 `DRMStatusEvent.DRM_Status`.

1. 查看 `DRMVoucher` 对象。


   如果 `DRMVoucher` 对象不为null，许可证有效。 转到步骤9。

   [Android：DRMLicenseAcquiredCallback](https://help.adobe.com/en_US/primetime/api/drm-apis/client/android/com/adobe/ave/drm/DRMLicenseAcquiredCallback.html)

   [iOS： DRMLicenseAcquired](https://help.adobe.com/en_US/primetime/api/drm-apis/client/ios/_d_r_m_interface_8h.html#afe5a9e3a003f312ee268d9b00927fa6d)
1. 检查此内容的策略所需的身份验证方法。

   使用 `DRMContentData.authenticationMethod` 属性。
   1. 如果身份验证方法为 `ANONYMOUS`，转到步骤9。 

      [Android：DRMAuthenticationMethod](https://help.adobe.com/en_US/primetime/api/drm-apis/client/android/index.html?com/adobe/ave/drm/DRMLicenseAcquiredCallback.html)

      [iOS： DRMAuthenticationMethod](https://help.adobe.com/en_US/primetime/api/drm-apis/client/ios/_d_r_m_interface_8h.html#a2003f29af93898b52a4123c2dd92c457)
   1. 如果身份验证方法为 `USERNAME_AND_PASSWORD`，您的应用程序必须提供一种机制，让用户输入凭据。

      将用户的凭据传递到许可证服务器以验证用户：

      ```
      DRMManager.authenticate( metadata.serverURL, metadata.domain, username, password)
      ```

      此 `DRMManager` 调度 `DRMAuthenticationErrorEvent` 如果身份验证失败，或者 `DRMAuthenticationCompleteEvent` 如果验证成功。 为这些事件创建侦听器。

      [Android：authenticate()](https://help.adobe.com/en_US/primetime/api/drm-apis/client/android/com/adobe/ave/drm/DRMManager.html#authenticate(com.adobe.ave.drm.DRMMetadata,%20java.lang.String,%20java.lang.String,%20java.lang.String,%20java.lang.String,%20com.adobe.ave.drm.DRMOperationErrorCallback,%20com.adobe.ave.drm.DRMAuthenticationCompleteCallback))

      [iOS：身份验证：](https://help.adobe.com/en_US/primetime/api/drm-apis/client/ios/interface_d_r_m_manager.html#a169c1441f196a834094a8e0f5ecb4aca)

      >[!NOTE]
      >
      >Adobe建议使用更安全的机制来提供凭据。 欲了解相关信息，请参见 [KeyGenParameterSpec](https://developer.android.com/reference/android/security/keystore/KeyGenParameterSpec.html).

   1. 如果身份验证方法为 `UNKNOWN`，则必须使用自定义身份验证方法。

      在这种情况下，内容提供商已安排以带外方式完成身份验证，而不使用Primetime API。 自定义身份验证过程必须生成可传递给 `DRMManager.setAuthenticationToken()` 方法。

      [Android：setAuthenticationToken()](https://help.adobe.com/en_US/primetime/api/drm-apis/client/android/com/adobe/ave/drm/DRMManager.html#setAuthenticationToken(com.adobe.ave.drm.DRMMetadata,%20java.lang.String,%20byte[]，%20com.adobe.ave.drm.DRMOperationErrorCallback，%20com.adobe.ave.drm.DRMOperationCompleteCallback))

      [iOS： setAuthenticationToken：](https://help.adobe.com/en_US/primetime/api/drm-apis/client/ios/interface_d_r_m_manager.html#a17884b5d9bcc5b0b39503f61140f9b09)

      >[!NOTE]
      >
      >或者，无论采用何种身份验证方法， `.setAuthenticationToken()` 用于将自定义数据从客户端发送到许可证服务器。 这是API的一种过载，因为此机制是在获取许可证时将动态自定义数据从客户端发送到许可证服务器的唯一方法。 自定义数据传输方法将在以下论坛帖子中深入讨论： [Primetime DRM(Adobe访问)论坛](https://forums.adobe.com/community/adobe_access).

1. 如果身份验证失败，应用程序必须返回到步骤6。

   确保您的应用程序具有处理并限制重复身份验证失败的机制。 例如，在三次尝试后，您会向用户显示一条消息，指示身份验证已失败且内容无法播放。
1. 要使用存储的令牌而不是提示用户输入凭据，请使用以下内容设置令牌： `DRMManager.setAuthenticationToken()` 方法。

   然后，从许可证服务器下载许可证并播放内容，如步骤6中所示。
   1. **可选：** 如果身份验证成功，您可以捕获身份验证令牌，它是内存中缓存的字节数组。

      使用获取此令牌 `DRMAuthenticationCompleteEvent.token` 属性。 您可以存储和使用身份验证令牌，这样用户就不必为此内容重复输入凭据。 许可证服务器确定身份验证令牌的有效期。

      [Android：OperationComplete()](https://help.adobe.com/en_US/primetime/api/drm-apis/client/android/com/adobe/ave/drm/DRMOperationCompleteCallback.html)

      [iOS： DRMOperationComplete](https://help.adobe.com/en_US/primetime/api/drm-apis/client/ios/_d_r_m_interface_8h.html#a5f2392ec6661b51bf7b0df71cd514731)
1. 如果身份验证成功，请从许可证服务器下载许可证：

   ```
   DRMManager.loadvoucher( 
      drmContentData, 
      LoadVoucherSetting.FORCE_REFRESH)
   ```

   加载完成后， `DRMManager` 对象调度 `DRMStatusEvent.DRM_STATUS`. 收听此事件，并在发送该事件时播放内容。  通过创建Primetime对象并调用其来播放视频 `play()` 方法：

   ```
   stream = new Primetime(connection); 
   stream.addEventListener(DRMStatusEvent.DRM _STATUS, drmStatusHandler); 
   stream.addEventListener(DRMErrorEvent.DRM_ERROR, drmErrorHandler); 
   stream.addEventListener(NetStatusEvent.NET_STATUS, netStatusHandler); 
   stream.client = new CustomClient(); 
   video.attachPrimetime(stream); 
   stream.play(videoURL);
   ```

   [Android：acquireLicense()](https://help.adobe.com/en_US/primetime/api/drm-apis/client/android/com/adobe/ave/drm/DRMManager.html#acquireLicense(com.adobe.ave.drm.DRMMetadata,%20com.adobe.ave.drm.DRMAcquireLicenseSettings,%20com.adobe.ave.drm.DRMOperationErrorCallback,%20com.adobe.ave.drm.DRMLicenseAcquiredCallback))

   [iOS：acquireLicense：](https://help.adobe.com/en_US/primetime/api/drm-apis/client/ios/interface_d_r_m_manager.html#a52accb5ed5b49d6e5d91277d78279f1b)
