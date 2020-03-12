---
description: 'null'
seo-description: 'null'
seo-title: 在播放器中设置XSTS令牌
title: 在播放器中设置XSTS令牌
uuid: 8995e029-deee-4e23-9cda-a50de8c4f2c0
translation-type: tm+mt
source-git-commit: c37061c116b8a6bc8ce085dc89dc8aadd0a2e490

---


# 流式播放到Xbox360（可选） {#streaming-to-xboc360}

Primetime DRM可用于Xbox360平台。 但是，仅支持受保护的流用例，不支持全套DRM策略权限。 不支持非流DRM策略权限，如设备域组。 Xbox360在尝试播放内容时忽略不支持的权限。

Xbox支持的Primetime DRM政策权限包括：
* 数字输出保护
* 许可证脱机缓存结束日期
* 许可证开始日期
* 许可证结束日期
* 播放窗口持续时间（秒）

如果内容已针对iOS、Android或桌面等其他Primetime平台打包，则可能不必重新打包即可流式传输到Xbox360。

Xbox360的一个注意事项是，每次在M3U8中遇到EXT-X-KEY标签时，它必须始终连接到关键服务器。 与iOS不同，在iOS中，DRM策略设置(policy.requireKeyServer)将导致iOS Primetime视频播放器从localhost检索AES解密密钥，Xbox将始终尝试从远程密钥服务器检索解密密钥。 没有DRM策略权限指示Xbox应用程序从localhost检索AES解密密钥。 由于这一要求，EXT-X-KEY条目必须位于指向Primetime Cloud DRM端点的M3U8中。 此URL通过OfflinePackager.jar配置文件config_hls.xml中的&lt;key_url>设置。

如果您希望将内容打包一次并使其流化到所有Primetime目标，并将iOS设备配置为不从远程密钥服务器检索密钥，则可以使用属性policy.requireKeyServer=false的DRM策略（如policy_ios_localkeyserver.pol）来打包内容。 iOS设备将在本地检索AES密钥，而Xbox设备将忽略此属性并连接到Primetime Cloud DRM密钥服务器以获取解密密钥。

>!Note
>
>所有Xbox360请求必须使用“自定义身份验证”/>“授权”。这是因为在Xbox360平台上，Xbox Live >使用Xbox安全令牌服务器(XSTS)令牌用于>身份验证目的。
>Primetime Cloud DRM许可证服务器使用XSTS令牌>验证Xbox设备和发出>许可证请求的用户的完整性。 但是，验证XSTS令牌需要>客户的专用Xbox Live供应商密钥，Primetime Cloud DRM不存储该密钥。 因此，当Primetime Cloud DRM收到Xbox 360客户端发出的>许可证请求时，Primetime Cloud DRM >将将XSTS令牌转发到Primetime客户的后端>身份验证／授权服务器。 Primetime客户的服务器
>然后，将解析并验证XSTS令牌，以确保它已使用客户的应用程序发布者密钥进行>签名。
>要从Xbox360客户端传递XSTS令牌，请设置令牌>同步以响应MediaPlayer.RequestKeyAttribute >event —— 此处有详细说明：在 **播放器中设置XSTS令牌。** 在“自定义身份验证”>“授权”目录中，软件版本中包含一个后端身份验证／授权服务器示例。在此处将进一步详细讨论XSTS令牌的验证： **Xbox Live XSTS令牌验证。**


## 在播放器中设置XSTS令牌 {#set-the-xsts-token-in-your-player}

在Xbox360中，您可以异步设置令牌以响应该事 `MediaPlayer.RequestKeyAttribute` 件。

设置XSTS令牌。

与软件捆绑的范例应用程序演示如何在播放器中设置XSTS令牌。 以下是示例播放器中的相关代码片断：

```
   MediaPlayer mMediaPlayer;  
 
mMediaPlayer.RequestKeyAttribute += Player_RequestKeyAttribute;  
 
private void Player_RequestKeyAttribute(object sender, RequestKeyAttributeEventArgs args) {  
    string token = "";  
    // XBOX XSTS Token...  
    KeyAttribute keyAttribute = new KeyAttribute(System.Text.Encoding.UTF8.GetBytes(token), null);  
    mMediaPlayer.SetKeyAttribute(args.RequestIdentifier, keyAttribute);  
} 
```

## Xbox Live XSTS令牌验证 {#xbox-live-xsts-token-validation}

对于XSTS请求，字 `customerSpecificAuthToken` 段将包含Base64编码的XSTS令牌。 样本代 `XSTSValidator` 码检查Base64解码的令牌是否存在元 `EncryptedAssertion` 素；但是，您可以使用其他方法来区分这些请求和非Xbox请求。 例如，您可以使用其他URL。

响应消息中返回的策略将覆盖随Xbox密钥请求提供的DRM元数据中的原始策略。 Xbox客户端只支持部分策略功能，这些字段是将覆盖原始策略的唯一字段。

需要其他设置步骤来支持令牌解密和验证。 必须将和凭 [!DNL xsts_partner_cert.pfx] 据加载 [!DNL x_secure_token_service.part.xboxlive.com.cer] 到JKS格式密钥库中，然后作为系统属性将其提供给后端授权服务器 `xsts-keystore`。 默认情况下，合作伙 [!DNL .pfx] 伴具有别名， `xsts`而令牌验证证书具有别名 `xsts-verify-cert`。 您还可以使用系统属性覆盖这些属性。 最后，有一个系统属 `xsts-keystore-password` 性没有默认值，并且包含keystore密码。 代码读取的系统属 `XSTSValidator` 性概述如下：

| 系统属性 | 默认值 | 评论 |
|---|---|---|
| xsts-keystore | xsts.jks | 验证程序使用的JKS格式密钥库。 |
| xsts-keystore-password |  | 密钥库的密码 |
| xsts-alias | xsts | 用于从密钥库检索解密密钥的别名 |
| xsts-verify-cert-alias | xsts-verify-cert | 用于从密钥库检索验证证书的别名 |

## 为XSTS验证程序创建JKS{#create-jks-for-an-xsts-validator}

1. 查找位于合作伙伴文件中的私人证书别名 [!DNL .pfx] 名称。

   ```
   keytool -list -storetype pkcs12 -keystore xsts_partner_cert.pfx -v 
   ```

1. 转换 [!DNL .pfx] 为 [!DNL .jks]。

   ```
   keytool -importkeystore -srckeystore xsts_partner_cert.pfx -srcstoretype PKCS12 \  
           -keystore xsts.jks -srcalias  
   <alias> -destalias xsts
   ```

   (其中 `<alias>` 是您在步骤1中发现的专用证书的别名。)
1. 导入 [!DNL x_secure_token_service.part.xboxlive.com.cer]。

   ```
   keytool -importcert -alias xsts-verify-cert -keystore xsts.jks \  
           -file x_secure_token_service.part.xboxlive.com.cer 
   ```

1. 放 [!DNL xsts.jks] 入Tomcat主目录，为Tomcat定 `-Dxsts-keystore-password=****` 义。

如果 [!DNL xsts_partner_cert.pfx] 和使 [!DNL xsts.jks] 用的密码不同，请更新中的 `xsts` 密码， `jks` 以使它们相同。

```
keytool -keypasswd -keystore xsts.jks -alias xsts 
```
