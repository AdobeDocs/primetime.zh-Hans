---
description: 要测试DRM解决方案，您需要一个视频应用程序，该应用程序可以处理您正在使用的特定DRM解决方案。 此播放器可以是Adobe提供的示例播放器，也可以是您自己的基于TVSDK的视频应用程序。
title: 播放受保护的内容
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '550'
ht-degree: 0%

---

# 播放受保护的内容 {#playback-your-protected-content}

要测试DRM解决方案，您需要一个视频应用程序，该应用程序可以处理您正在使用的特定DRM解决方案。 此播放器可以是Adobe提供的示例播放器，也可以是您自己的基于TVSDK的视频应用程序。

1. 使用从ExpressPlay服务器返回的令牌响应中的许可证服务器URL测试是否可以播放受保护的内容。

   * **维德万**  — 直接使用从您的ExpressPlay许可证令牌请求收到的Widevine响应。
   * **PlayReady**  — 从许可证令牌请求返回的JSON对象中获取许可证服务器URL和令牌。
   * **公平游戏**  — 直接使用从您的ExpressPlay许可证令牌请求收到的FairPlay响应。

1. 使用您自己的播放器或现有的Adobe示例播放器来测试受保护内容的播放。

   提供受保护内容的URL（M3U8或MPD清单的位置，具体取决于您测试的DRM解决方案）。

   根据您测试的播放器提供的界面，可能会要求您提供许可证URL和令牌，将它们作为输入字段中的字符串进行分隔，或作为JSON对象粘贴到文本框中，或作为URL中的查询参数。

   此处列出了测试播放器的一些可能性：

   * HTML5引用播放器：

     ```
     https://ptdemos.com/html5/internal/1_2/2.4_GM/samples/reference/reference_player.html
     ```

   * Shaka播放器：

     ```
     https://shaka-player-demo.appspot.com
     ```

   * TVSDK播放器示例（开发中） — 

   ```
   https://drmtest2.adobe.com/TVSDK_HTML5/samples/reference/reference_player.html
   ```

   **在测试FairPlay设置时检查播放：** 使用ExpressPlay许可证服务器时，FairPlay需要一些额外的步骤才能播放内容。 如果您使用 [!DNL curl] 以测试连接（如中所述） [许可](../../multi-drm-workflows/quick-start/handle-the-licensing.md))，您需要 *编辑M3U8清单* （已打包的内容）如下所示：

1. 将您从许可证令牌请求返回的响应添加到 `#EXT-X-KEY:` 标签进行标记；以及
1. 从响应（现在位于清单中）更改该URL的协议，从 `https://` 到 `skd://`.

   以下是使用FairPlay测试播放的完整示例，包括许可步骤：

1. 使用FairPlay许可证令牌请求获取您的许可证令牌URL。 (使用您自己的生产客户验证器，并确保使用相同的CEK和 `iv` 用来打包您的FairPlay内容。) 运行以下命令以获取示例内容的许可证令牌URL：

   ```
   curl -v "https://fp-gen.service.expressplay.com/hms/fp/token? 
   customerAuthenticator=[YOUR-PRODUCTION-AUTHENTICATOR]&errorFormat=json 
   &contentKey CEK as query parameter contentKey 
   =[YOUR CONTENT KEY]&iv=[YOUR IV]"
   ```

   您应该使用许可证令牌URL返回响应，该URL如下所示：

   ```
   https://fp.service.expressplay.com:80/hms/fp/rights/? 
   ExpressPlayToken=AQAAABNlKcEAAABQaTjshua3cWjG_Il3fvhf3g-CR1rn 
   JKdtaVaAnhkfTCW0bWAU76YgwForbrXhD5tXUHhfP7FD1svvLPxN5qomYsnwY 
   SSwcDq1ZnRtXunFLueTw6LAL52aZllMLasCSzYRMaAVHw 
   ```

1. 将返回的许可证令牌URL响应放入您的M3U8清单，并且 *将许可证令牌URL的方案更改为* `sdk://` 从 `https://`. 以下是M3U8清单中的#EXT-X-KEY标记示例：

   ```
   #EXT-X-KEY:METHOD=SAMPLE-AES, 
   URI="skd://fp.service.expressplay.com:80/hms/fp/rights/? 
   ExpressPlayToken=AQAAABNlKcEAAABQaTjshua3cWjG_Il3fvhf3g- 
   CR1rnJKdtaVaAnhkfTCW0bWAU76YgwForbrXhD5tXUHhfP7FD1svvLPx 
   N5qomYsnwYSSwcDq1ZnRtXunFLueTw6LAL52aZllMLasCSzYRMaAVHw", 
   KEYFORMAT="com.apple.streamingkeydelivery",KEYFORMATVERSIONS="1"
   ```

   >[!NOTE]
   >
   >上述信息仅适用于您的FairPlay设置的测试。 它可能不适用于您的生产设置，具体取决于您配置FairPlay处理程序的方式。 请参阅 [在iOS应用程序中启用Apple FairPlay](../../../programming/tvsdk-3x-ios-prog/ios-3x-drm-content-security/ios-3x-apple-fairplay-tvsdk.md) 以了解详细信息。

如果播放了视频，则表示您已成功打包您的内容并授予许可。 如果您的视频无法播放，请查看故障排除页面，以了解针对您的问题的一些可能解决方案。

<!--<a id="example_603D92A1F3924467B5D66EC862B8F59C"></a>-->

例如，下面是上面列出的第一个测试播放器中的UI部分，其中提供了从ExpressPlay服务器获取的许可信息：

<!--<a id="fig_zjy_q2c_rw"></a>-->

![](assets/sample-player-drm-settings-web.png)
