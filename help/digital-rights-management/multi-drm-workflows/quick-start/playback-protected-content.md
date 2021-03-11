---
description: 要测试DRM解决方案，您需要一个视频应用程序来处理您使用的特定DRM解决方案。 此播放器可以是Adobe提供的示例播放器，或您自己的基于TVSDK的视频应用程序。
title: 播放受保护的内容
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '550'
ht-degree: 0%

---


# 播放受保护的内容{#playback-your-protected-content}

要测试DRM解决方案，您需要一个视频应用程序来处理您使用的特定DRM解决方案。 此播放器可以是Adobe提供的示例播放器，或您自己的基于TVSDK的视频应用程序。

1. 使用从ExpressPlay服务器返回的令牌响应中的许可证服务器URL来测试是否可以播放受保护的内容。

   * **Widevine**  — 直接使用从ExpressPlay许可证令牌请求接收到的Widevine响应。
   * **PlayReady**  — 从您的许可证令牌请求返回的JSON对象中获取许可证服务器URL和令牌。
   * **FairPlay**  — 直接使用从ExpressPlay许可证令牌请求中接收的FairPlay响应。

1. 使用您自己的播放器或现有的Adobe范例播放器测试受保护内容的播放。

   提供受保护内容的URL（M3U8或MPD清单的位置，具体取决于您正在测试的DRM解决方案）。

   根据您测试的播放器提供的界面，可能会要求您提供许可证URL和标记，它们分别作为输入字段中的字符串、粘贴到文本框中的JSON对象或作为URL中的查询参数。

   下面列出了测试播放器的一些可能性：

   * HTML5参考播放器：

      ```
      https://ptdemos.com/html5/internal/1_2/2.4_GM/samples/reference/reference_player.html
      ```

   * Shaka Player:

      ```
      https://shaka-player-demo.appspot.com
      ```

   * 示例TVSDK播放器（正在开发中） — 

   ```
   https://drmtest2.adobe.com/TVSDK_HTML5/samples/reference/reference_player.html
   ```

   **在测试FairPlay设置时检查播放：** 在使用ExpressPlay许可证服务器时，FairPlay需要执行一些额外步骤来播放内容。如果您使用[!DNL curl]测试连接（如[授权](../../multi-drm-workflows/quick-start/handle-the-licensing.md)中所述），则需要&#x200B;*编辑M3U8清单*（您的打包内容），如下所示：

1. 将从许可证令牌请求返回的响应添加到清单中的`#EXT-X-KEY:`标记；和
1. 将该URL的协议从响应（现在在清单中），从`https://`更改为`skd://`。

   以下是使用FairPlay测试播放的完整示例，包括许可步骤：

1. 使用FairPlay许可证令牌请求获取您的许可证令牌URL。 （使用您自己的生产客户身份验证器，并确保使用打包FairPlay内容时使用的相同CEK和`iv`。） 运行以下命令以获取示例内容的许可证令牌URL:

   ```
   curl -v "https://fp-gen.service.expressplay.com/hms/fp/token? 
   customerAuthenticator=[YOUR-PRODUCTION-AUTHENTICATOR]&errorFormat=json 
   &contentKey CEK as query parameter contentKey 
   =[YOUR CONTENT KEY]&iv=[YOUR IV]"
   ```

   您应该返回一个包含类似以下内容的许可证令牌URL的响应：

   ```
   https://fp.service.expressplay.com:80/hms/fp/rights/? 
   ExpressPlayToken=AQAAABNlKcEAAABQaTjshua3cWjG_Il3fvhf3g-CR1rn 
   JKdtaVaAnhkfTCW0bWAU76YgwForbrXhD5tXUHhfP7FD1svvLPxN5qomYsnwY 
   SSwcDq1ZnRtXunFLueTw6LAL52aZllMLasCSzYRMaAVHw 
   ```

1. 将返回的许可证令牌URL响应放入您的M3U8清单中，并将&#x200B;*将许可证令牌URL的方案从`https://`更改为* `sdk://`。 以下是M3U8清单中#EXT-X-KEY标签的示例：

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
   >上述信息仅适用于FairPlay设置的测试。 它可能不适用于您的生产设置，具体取决于您配置FairPlay处理程序的方式。 有关详细信息，请参阅[在iOS应用程序中启用Apple FairPlay](../../../programming/tvsdk-3x-ios-prog/ios-3x-drm-content-security/ios-3x-apple-fairplay-tvsdk.md)。

如果播放视频，您已成功打包并许可了您的内容。 如果视频播放不畅，请查看疑难解答页以找到一些解决问题的可能解决方案。

<!--<a id="example_603D92A1F3924467B5D66EC862B8F59C"></a>-->

例如，下面是上面列出的第一个测试播放器中的UI部分，您可以在其中提供从ExpressPlay服务器获得的许可信息：

<!--<a id="fig_zjy_q2c_rw"></a>-->

![](assets/sample-player-drm-settings-web.png)
