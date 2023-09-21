---
description: DRM工作流涉及打包内容、为内容提供许可以及从您自己的视频应用程序中回放受保护的内容。 每个DRM解决方案的工作流程通常都相似，但细节方面有一些差异。
title: 公平播放的多DRM工作流
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '1470'
ht-degree: 0%

---

# 公平播放的多DRM工作流 {#multi-drm-workflow-for-fairplay}

DRM工作流涉及打包内容、为内容提供许可以及从您自己的视频应用程序中回放受保护的内容。 每个DRM解决方案的工作流程通常都相似，但细节方面有一些差异。

此多DRM工作流可引导您完成受Apple FairPlay保护的HLS内容的设置、打包、许可和播放。 此工作流还包括有关实施离线播放和许可证轮换的可选说明。

## 为FairPlay启用ExpressPlay服务 {#enable-expressplay-service-for-fairplay}

Apple的FairPlay DRM解决方案在与ExpressPlay DRM服务一起使用时需要一些设置。 这包括从Apple获取凭据并将其上传到ExpressPlay。

按照以下步骤启用ExpressPlay服务以进行FairPlay内容保护。

1. 从Apple获取凭据。

   这些凭据被唯一地提供给每个服务提供商。 您必须填写以下表格以请求这些权限： [https://developer.apple.com/contact/fps/](https://developer.apple.com/contact/fps/).

   >[!NOTE]
   >
   >选择 **[!UICONTROL Content Provider]** 用于主要角色。

   您的请求获得批准后，Apple会向您发送 *FairPlay流部署包*.
1. 生成证书签名请求。

   您可以使用 [!DNL openssl] 以生成公钥/私钥对和证书签名请求(CSR)。

   1. 生成密钥对。

      ```
      openssl genrsa -aes256 -out privatekey.pem 1024 
      ```

   1. 生成CSR。

      ```
      openssl req -new -sha1 -key privatekey.pem -out certreq.csr  
        -subj "/CN=SubjectName /OU=OrganizationalUnit /O=Organization /C=US"
      ```

      >[!NOTE]
      >
      >此步骤的说明位于 *FairPlay流部署包*，出于方便起见，包含在此处。 如果您对流程的这一部分有任何疑问，请查看 *FairPlayCertificateCreation.pdf* （在您的部署包中）。

1. 通过Apple开发人员门户上传CSR。
   1. 开发团队的团队代理必须登录 [!DNL developer.apple.com/account].
   1. 单击 **[!UICONTROL Certificates, Identifiers & Profiles]**，然后选择 **[!UICONTROL iOS, tvOS, watchOS]** 下拉菜单，然后单击 **[!UICONTROL Certificates->Production]** 页面左侧。
   1. 单击 **[!UICONTROL +]** 按钮来请求新证书。 选择 **[!UICONTROL FairPlay Streaming Certificate]** 下的选项 **[!UICONTROL Production]**.

      此 *添加iOS证书* 对话框打开。
   1. 在 *添加iOS证书*，上传在步骤2.b.中生成的CSR文件，然后单击 **[!UICONTROL Generate]**.

      您的应用程序密钥(ASK)会显示在同一对话框中。
   1. 写下您的ASK ，并将其存储在安全位置。
   1. 在ASK中获取密钥以完成证书生成并单击 **[!UICONTROL Continue]**.
   1. 确认已保存ASK后，单击 **[!UICONTROL Generate]** 以继续。

      >[!NOTE]
      >
      >请务必保存ASK的副本并安全地保存它。 *如果ASK遭到破坏，您将无法再使用FairPlay流媒体保护您的内容。* 只有一(1)个ASK分配给您的团队。 将不再提供该值，并且您以后无法检索它。

   1. 下载FPS证书。

      请确保将私钥（步骤2.a.）和公钥（在此步骤中下载的FPS证书）的备份副本保存在安全位置。
1. 使用您的FairPlay凭据设置您的ExpressPlay帐户。
   1. 假设您在步骤3.h.中下载的证书名称是 [!DNL fairplay.cer].
   1. 打开 [!DNL fairplay.cer] Apple密钥链访问实用程序的文件。
   1. 通过输入&quot; `fairplay`”图标。
   1. 识别您公司的FairPlay证书。

      您的公司名称应与Apple颁发的证书关联。
   1. 选择展开箭头并右键单击您的私钥以展开证书。
   1. 选择 **[!UICONTROL Export "Your Company Name"]** 并保存 [!DNL .p12] 文件。

      系统将要求您指定密码来保护此文件。 记下此密码，因为您将需要随凭据包发送此密码。
   1. 登录您的帐户 [www.expressplay.com](https://www.expressplay.com).
   1. 单击 **[!UICONTROL DRM SERVICES]** 左上角，然后选择 **[!UICONTROL FairPlay]** 选项卡。
   1. 将您的FairPlay凭据上传到ExpressPlay帐户。

      1. 创建一个包含ASK值（应为32个字符）的文本文件，例如： `1234567890abcdef1234567890abcdef`)，并选择要上传的文件。
      1. 从Step 4.f.中选择要上载的PKCS12文件。
      1. 输入Step 4.f中的PKCS12文件密码。
      1. 单击“上载”按钮。

现在，您可以创建具有FairPlayHTML保护的iOS应用程序或内容页面，以及您的 [!DNL fairplay.cer] 使用FairPlay的ExpressPlay服务的证书。

<!--<a id="fig_sjr_2pn_sv"></a>-->

![](assets/multi_drm_expressplay_drm_services_web.png)

### 打包您的内容以用于FairPlay {#package-your-content-for-fairplay}

要打包内容，您可以使用AdobeOffline Packager或其他工具，如ExpressPlay的Bento4打包程序。

打包人员准备视频以进行播放（例如，将原始文件分段并将其放入清单），并使用您选择的DRM解决方案（在本例中为FairPlay）保护视频：

* [用于FairPlay DRM的Adobe脱机打包程序](https://helpx.adobe.com/content/dam/help/en/primetime/guides/offline_packager_getting_started.pdf#page=21)
* [ExpressPlay打包程序 — 适用于HLS的Bento4](https://www.bento4.com/developers/hls/)

<!--<a id="fig_jbn_fw5_xw"></a>-->

![](assets/pkg_lic_play_hls_web.png)

1. 打包您的内容。

   以下是使用Adobe离线打包程序的打包示例。 Packager使用配置文件(例如， [!DNL fairplay.xml])，它类似于：

   ```
   <config>
   <in_path>mp4_file_path</in_path>
   <out_type>hls</out_type>
   <out_path>out_file_path</out_path>
   <drm/>
   <drm_sys>FAIRPLAY</drm_sys>
   <frag_dur>4</frag_dur>
   <target_dur>6</target_dur>
   <key_file_path>creds/fairplay.bin</key_file_path>
   <iv_file_path>creds/iv.bin</iv_file_path>
   <key_url>user_provided_value</key_url>
   <content_id>_default_</content_id>
   </config>
   ```

   * `in_path`  — 此入口指向本地打包计算机上源视频的位置。
   * `out_type`  — 此条目描述打包输出的类型，在本例中为FairPlay的HLS。
   * `out_path`  — 本地计算机上要输出内容的位置。
   * `drm_sys`  — 您打包的DRM解决方案。 这是 `FAIRPLAY` 这种情况下。
   * `frag_dur`  — 片段持续时间（以秒为单位）。
   * `target_dur` - HLS输出的目标持续时间。
   * `key_file_path`  — 这是用作内容加密密钥(CEK)的打包计算机上的许可证文件的位置。 它是一个Base-64编码的16字节十六进制字符串。
   * `iv_file_path`  — 这是包装机器上IV文件的位置。
   * `key_url`  — 的URI参数 `EXT-X-KEY` 的标记 [!DNL .m3u8] 文件。
   * `content_id`  — 默认值。

   如附注所述， [Packager文档](https://helpx.adobe.com/content/dam/help/en/primetime/guides/offline_packager_getting_started.pdf#page=7)，“最佳做法是，创建包含要用于生成输出的常用选项的配置文件。 然后，通过提供特定选项作为命令行参数来创建输出。”

   ```
   java -jar OfflinePackager.jar -in_path sample.mp4 -out_type hls 
   -out_path out_file_path -drm -drm_sys FAIRPLAY -key_file_path "creds/fairplay.bin" 
   -key_url "user_provided_value"
   ```

   生成的M3U8文件具有 `EXT-X-KEY` 属性如下所示：

   ```
   #EXT-X-KEY:METHOD=SAMPLE-AES,URI="user_provided_value",​
   KEYFORMAT="com.apple.streamingkeydelivery",KEYFORMATVERSIONS="1" 
   ```

### 设置公平竞争政策 {#setting-policies-for-fairplay}

您可以使用授权服务器为受FairPlay保护的内容设置策略。 您可以自行设置，也可以使用Adobe提供的样本权利服务器。

Adobe提供了一个ExpressPlay授权服务器(SEES)示例来说明如何操作 *基于时间* 和 *设备绑定* 权利。 此示例权利文件服务器基于ExpressPlay服务构建。

[参考服务器：示例ExpressPlay授权服务器(SEES)](../../multi-drm-workflows/feature-topics/sees-reference-server.md)

* [参考服务：基于时间的授权](../../multi-drm-workflows/feature-topics/sees-reference-server-time-entitlement.md)
* [参考服务：设备绑定授权](../../multi-drm-workflows/feature-topics/sees-reference-server-binding-entitlement.md)

## FairPlay的许可和播放 {#licensing-and-playback-for-fairplay}

对受FairPlay保护的内容进行许可和播放需要交换URL方案，即视频清单文件(skd：)中使用的方案和ExpressPlay令牌请求(https：)中使用的方案。

此处提供了从iOS TVSDK客户端实施许可和播放的操作说明： [在TVSDK应用程序中启用Apple FairPlay](../../../programming/tvsdk-3x-ios-prog/ios-3x-drm-content-security/ios-3x-apple-fairplay-tvsdk.md). 您还可以选择为FairPlay实施离线播放和许可证轮换。

## 使用FairPlay的HLS离线 {#section_047A05D1E3B64883858BC601CFC8F759}

您可能希望允许用户在无法检索受FairPlay保护的内容许可时播放该内容，因为播放器与Web隔离（例如在飞机上）。

在开始此任务之前，请下载并阅读Apple文档 **“使用FairPlay流和HTTP实时流进行离线播放”**. 阅读指南，了解如何下载传输流(TS)区段并将它们保存到本地计算机。

使用以下工作流为FairPlay实施离线播放：

1. 下载HLS TS区段。
1. 从FairPlay服务器请求永久租赁许可证(请参阅 **“FairPlay持续租赁政策”**)。
1. 保存 `persistentContentKey`.
1. 离线播放FairPlay内容。

>[!NOTE]
>
>如果保留的内容密钥已过期，则客户端上的FairPlay流不会开始解密。 但是，如果内容键在播放期间过期，则将继续提供用户体验。
>
>请参阅 [使用HTTP实时流](https://developer.apple.com/library/content/documentation/AudioVideo/Conceptual/MediaPlaybackGuide/Contents/Resources/en.lproj/HTTPLiveStreaming/HTTPLiveStreaming.html#//apple_ref/doc/uid/TP40016757-CH11-SW3) 文档，以了解更多详细信息。

### FairPlay许可证轮换 {#section_D32AA08C61474B4F876AC2A5F18CB879}

许可证轮换是一种防止对长时间播放的内容进行许可证黑客攻击的方案。

在M3U8清单中，每个密钥标记将应用于以下TS区段，直到下一个密钥标记或文件结尾。

要添加许可证轮换，请执行以下操作：

* 在许可证轮换期间插入新的FairPlay密钥标记。

  可添加任意数量的关键标记。

  对于线性内容，请确保在M3U8窗口中保留最新的密钥标记。 大约还剩两个TS区段可供播放（大约20秒）时，iOS将请求下一个M3U8。 如果新的M3U8包含新的关键标记，所有关键请求都将立即发生。 将不再请求以前的现有密钥。 iOS将等待所有关键请求完成，然后再开始播放。

  对于包含许可证轮换的VOD内容，所有关键请求都将在播放开始时发生。

  以下是带有密钥轮换的示例M3U8：

  ```
  #EXTM3U
  #EXT-X-TARGETDURATION:10
  #EXT-X-VERSION:5
  #EXT-X-MEDIA-SEQUENCE:0
  #EXT-X-PLAYLIST-TYPE:VOD
  #EXT-X-KEY:METHOD=SAMPLE-AES,URI="skd://one?cek=1dc2cc71d913f4f74eca0c4632
  212b25&iv=e21f0f72b6363ff6143737cb1e9ca8d7",KEYFORMAT="com.apple.streaming
  keydelivery",KEYFORMATVERSIONS="1"
  #EXTINF:10,
  fileSequence0.ts
  #EXTINF:10,
  fileSequence1.ts
  #EXTINF:10,
  fileSequence2.ts
  #EXTINF:10,
  fileSequence3.ts
  #EXTINF:10,
  fileSequence4.ts
  #EXTINF:10,
  fileSequence5.ts
  #EXTINF:10,
  fileSequence6.ts
  #EXTINF:10,
  fileSequence7.ts
  #EXTINF:10,
  #EXT-X-KEY:METHOD=SAMPLE-AES,URI="skd://two?cek=f6efc698b96cf8f4fa46d5237d
  337c77&iv=18401077091784bcda8079acf978dc95",KEYFORMAT="com.apple.streaming
  keydelivery",KEYFORMATVERSIONS="1"
  #EXTINF:10,
  fileSequence8.ts
  #EXTINF:10,
  ```
