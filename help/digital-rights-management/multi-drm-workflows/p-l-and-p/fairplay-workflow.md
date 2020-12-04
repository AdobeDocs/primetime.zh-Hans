---
description: DRM工作流包括打包您的内容、为内容提供许可以及从您自己的视频应用程序回放受保护的内容。 每个DRM解决方案的工作流程通常都相似，但细节中有一些不同。
seo-description: DRM工作流包括打包您的内容、为内容提供许可以及从您自己的视频应用程序回放受保护的内容。 每个DRM解决方案的工作流程通常都相似，但细节中有一些不同。
seo-title: FairPlay的多DRM工作流程
title: FairPlay的多DRM工作流程
uuid: cd940a70-400c-435e-8322-55bd624164e1
translation-type: tm+mt
source-git-commit: 1b9792a10ad606b99b6639799ac2aacb707b2af5
workflow-type: tm+mt
source-wordcount: '1514'
ht-degree: 0%

---


# FairPlay的多DRM工作流{#multi-drm-workflow-for-fairplay}

DRM工作流包括打包您的内容、为内容提供许可以及从您自己的视频应用程序回放受保护的内容。 每个DRM解决方案的工作流程通常都相似，但细节中有一些不同。

此多DRM工作流程将指导您完成使用Apple FairPlay保护的HLS内容的设置、打包、授权和回放。 此工作流还包含用于实现脱机播放和许可证轮换的可选说明。

## 为FairPlay启用ExpressPlay服务{#enable-expressplay-service-for-fairplay}

Apple的FairPlay DRM解决方案需要在您将其与ExpressPlay DRM服务一起使用时进行一些设置。 这包括从Apple获取凭据并将其上传到ExpressPlay。

按照以下步骤启用ExpressPlay服务以保护FairPlay内容。

1. 从Apple获取凭据。

   这些凭据是唯一提供给每个服务提供商的。 您必须填写以下表单来申请：[https://developer.apple.com/contact/fps/](https://developer.apple.com/contact/fps/)。

   >[!NOTE]
   >
   >选择&#x200B;**[!UICONTROL Content Provider]**&#x200B;作为主角色。

   在您的请求获得批准后，Apple将向您发送&#x200B;*FairPlay流部署包*。
1. 生成证书签名请求。

   您可以使用[!DNL openssl]生成公钥／私钥对和证书签名请求(CSR)。

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
      >此步骤的说明位于&#x200B;*FairPlay流部署包*&#x200B;中，但为方便起见，此处包含这些说明。 如果您对此过程部分有任何问题，请查看&#x200B;*FairPlayCertificateCreation.pdf*（在部署包中）中的说明。

1. 通过Apple开发人员门户上传您的CSR。
   1. 开发团队的团队代理必须登录[!DNL developer.apple.com/account]。
   1. 单击&#x200B;**[!UICONTROL Certificates, Identifiers & Profiles]**，然后选择页面左上角的&#x200B;**[!UICONTROL iOS, tvOS, watchOS]**&#x200B;下拉框，然后单击页面左侧的&#x200B;**[!UICONTROL Certificates->Production]**。
   1. 单击页面右上角的&#x200B;**[!UICONTROL +]**&#x200B;按钮以请求新证书。 选择&#x200B;**[!UICONTROL Production]**&#x200B;下的&#x200B;**[!UICONTROL FairPlay Streaming Certificate]**&#x200B;选项。

      将打开&#x200B;*添加iOS证书*&#x200B;对话框。
   1. 在&#x200B;*添加iOS证书*&#x200B;中，上传您在步骤2.b.中生成的CSR文件，然后单击&#x200B;**[!UICONTROL Generate]**。

      您的应用程序密码键(ASK)显示在同一对话框中。
   1. 记下您的ASK并将其存储在安全位置。
   1. ASK中的密钥完成证书生成，然后单击&#x200B;**[!UICONTROL Continue]**。
   1. 验证已保存ASK后，单击&#x200B;**[!UICONTROL Generate]**&#x200B;继续。

      >[!NOTE]
      >
      >保存ASK副本并安全地存储它非常重要。 *如果您的ASK受到破坏，您将无法再通过FairPlay流保护您的内容。* 只有一(1)个ASK分配给您的团队。该值将不再提供，您以后也无法检索它。

   1. 下载FPS证书。

      请务必将私钥（从步骤2.a.）和公钥（您在此步骤中下载的FPS证书）的备份副本保存到安全位置。
1. 使用您的FairPlay凭据设置您的ExpressPlay帐户。
   1. 假设您在步骤3.h中下载的证书名称。是[!DNL fairplay.cer]。
   1. 使用Apple Keychain Access实用程序打开[!DNL fairplay.cer]文件。
   1. 在右上方的搜索字段中输入“ `fairplay`”，过滤您的许多证书。
   1. 识别公司的FairPlay证书。

      您的公司名应与Apple颁发的证书相关联。
   1. 通过选择展开箭头展开证书，然后右键单击您的私钥。
   1. 选择&#x200B;**[!UICONTROL Export "Your Company Name"]**&#x200B;并保存[!DNL .p12]文件。

      系统将要求您指定密码来保护此文件。 请记下此密码，因为您需要随凭据包一起发送此密码。
   1. 在[www.expressplay.com](https://www.expressplay.com)上登录您的帐户。
   1. 单击左上角的&#x200B;**[!UICONTROL DRM SERVICES]**，然后选择&#x200B;**[!UICONTROL FairPlay]**&#x200B;选项卡。
   1. 将您的FairPlay凭据上传到您的ExpressPlay帐户。

      1. 创建一个包含ASK值的文本文件(应该有32个字符，例如：`1234567890abcdef1234567890abcdef`)，然后选择此文件进行上传。
      1. 从步骤4.f中选择PKCS12文件。。
      1. 在步骤4.f中输入PKCS12文件密码。
      1. 单击“上传”按钮。

现在，您可以使用ExpressPlay for FairPlay服务创建具有FairPlay内容保护的iOS应用程序或HTML5页面以及[!DNL fairplay.cer]证书。

<!--<a id="fig_sjr_2pn_sv"></a>-->

![](assets/multi_drm_expressplay_drm_services_web.png)

### 将您的内容打包以用于FairPlay {#package-your-content-for-fairplay}

要打包内容，您可以使用AdobeOffline Packager或其他工具，如ExpressPlay的Bento4打包程序。

打包者准备视频以进行回放（例如，将原始文件分割并放入清单中），并使用您选择的DRM解决方案（本例中为FairPlay）保护视频：

* [AdobeFairPlay DRM的Offline Packager](https://helpx.adobe.com/content/dam/help/en/primetime/guides/offline_packager_getting_started.pdf#page=21)
* [ExpressPlay Packagers - HLS的Bento4](https://www.bento4.com/developers/hls/)

<!--<a id="fig_jbn_fw5_xw"></a>-->

![](assets/pkg_lic_play_hls_web.png)

1. 打包您的内容。

   以下是使用Adobe脱机包装程序的打包示例。 Packager使用一个配置文件（例如[!DNL fairplay.xml]），它类似于：

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

   * `in_path` -此入口指向本地打包机上源视频的位置。
   * `out_type` -此条目描述打包输出的类型，本例中为FairPlay的HLS。
   * `out_path` -您希望输出转到的本地计算机上的位置。
   * `drm_sys` -要打包的DRM解决方案。这是`FAIRPLAY`。
   * `frag_dur` -片段持续时间（以秒为单位）。
   * `target_dur` - HLS输出的目标持续时间。
   * `key_file_path` -这是包装机上用作内容加密密钥(CEK)的许可证文件的位置。它是一个16字节的十六进制Base-64编码字符串。
   * `iv_file_path` -这是包装机上IV文件的位置。
   * `key_url` -文件标记 `EXT-X-KEY` 的URI参 [!DNL .m3u8] 数。
   * `content_id` -默认值。

   如[Packager文档](https://helpx.adobe.com/content/dam/help/en/primetime/guides/offline_packager_getting_started.pdf#page=7)中所述，“作为最佳实践，请创建一个配置文件，其中包含要用于生成输出的常用选项。 然后，通过将特定选项作为命令行参数提供来创建输出。”

   ```
   java -jar OfflinePackager.jar -in_path sample.mp4 -out_type hls 
   -out_path out_file_path -drm -drm_sys FAIRPLAY -key_file_path "creds/fairplay.bin" 
   -key_url "user_provided_value"
   ```

   生成的M3U8文件具有`EXT-X-KEY`属性，如下所示：

   ```
   #EXT-X-KEY:METHOD=SAMPLE-AES,URI="user_provided_value",​
   KEYFORMAT="com.apple.streamingkeydelivery",KEYFORMATVERSIONS="1" 
   ```

### 设置FairPlay的策略{#setting-policies-for-fairplay}

您可以使用授权服务器为受FairPlay保护的内容设置策略。 您可以设置自己的，或利用Adobe提供的示例授权服务器。

Adobe提供示例ExpressPlay授权服务器(SEES)，其中显示如何执行&#x200B;*基于时间的*&#x200B;和&#x200B;*设备绑定*&#x200B;授权。 此示例授权服务器构建在ExpressPlay服务之上。

[引用服务器：示例ExpressPlay授权服务器(SEES)](../../multi-drm-workflows/feature-topics/sees-reference-server.md)

* [参考服务：基于时间的授权](../../multi-drm-workflows/feature-topics/sees-reference-server-time-entitlement.md)
* [参考服务：设备绑定授权](../../multi-drm-workflows/feature-topics/sees-reference-server-binding-entitlement.md)

## FairPlay的许可和播放{#licensing-and-playback-for-fairplay}

授权和播放FairPlay保护的内容需要在视频清单文件(skd:)中使用的方案与ExpressPlay令牌请求(https:)中使用的方案之间交换URL方案。

有关从iOS TVSDK客户端实现许可和回放的说明，请参阅：[在TVSDK应用程序中启用Apple FairPlay](../../../programming/tvsdk-3x-ios-prog/ios-3x-drm-content-security/ios-3x-apple-fairplay-tvsdk.md)。 您还可以选择为FairPlay实施脱机播放和许可证轮换。

## HLS脱机与FairPlay {#section_047A05D1E3B64883858BC601CFC8F759}

您可能希望使用户能够在无法检索到FairPlay保护的内容时播放其内容，因为该播放器与Web相隔离（如在飞机上）。

开始此任务之前，请下载并阅读Apple文档&#x200B;**“Offline Playback with FairPlay Streaming and HTTP Live Streaming”**。 阅读指南，了解如何下载传输流(TS)段并将其保存到本地机器。

利用此工作流为FairPlay实施脱机播放：

1. 下载HLS TS段。
1. 从FairPlay服务器请求永久租赁许可证（请参阅&#x200B;**“FairPlay永久租赁策略”**）。
1. 保存`persistentContentKey`。
1. 脱机播放FairPlay内容。

>[!NOTE]
>
>如果保留的内容密钥已过期，客户端上的FairPlay流不会开始解密。 但是，如果内容密钥在播放期间过期，则它将继续用户体验。
>
>有关详细信息，请参阅[使用HTTP实时流](https://developer.apple.com/library/content/documentation/AudioVideo/Conceptual/MediaPlaybackGuide/Contents/Resources/en.lproj/HTTPLiveStreaming/HTTPLiveStreaming.html#//apple_ref/doc/uid/TP40016757-CH11-SW3)文档。

### FairPlay许可证轮换{#section_D32AA08C61474B4F876AC2A5F18CB879}

许可证轮换是一种防止长期播放的内容的许可证黑客的方案。

在M3U8清单中，每个关键标签将应用于以下TS区段，直到下一个关键标签或文件结束。

要添加许可证轮替，请执行以下操作：

* 在许可证轮换期间插入新的FairPlay密钥标签。

   可以添加任意数量的关键标记。

   对于线性内容，请确保在M3U8窗口中保留最新的关键标签。 当有大约两个TS区段需要播放时（大约20秒）,iOS将请求下一个M3U8。 如果新的M3U8包含新的关键标签，则所有关键请求都将立即发生。 将不再请求以前的现有密钥。 iOS将等待所有关键请求完成，然后播放将开始。

   对于具有许可证轮换的VOD内容，所有关键请求都将在播放开始时进行。

   以下是带密钥旋转的示例M3U8:

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
