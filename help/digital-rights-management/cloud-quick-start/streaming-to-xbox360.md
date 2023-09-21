---
title: 在播放器中设置XSTS令牌
description: 在播放器中设置XSTS令牌
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '841'
ht-degree: 0%

---

# 流到Xbox360（可选） {#streaming-to-xboc360}

Primetime DRM可在Xbox360平台上使用。 但是，仅支持受保护的流使用案例，而不支持全套DRM策略权限。 不支持非流式DRM策略权限，如设备域组。 尝试播放内容时，Xbox360会忽略不支持的权限。

Xbox支持的Primetime DRM策略权限包括：
* 数字输出保护
* 许可证脱机缓存结束日期
* 许可证开始日期
* 许可证结束日期
* 播放窗口持续时间（秒）

如果内容已打包到其他Primetime平台(如iOS、Android或Desktop)，则可能不必重新打包以流到Xbox360。

Xbox360的一个注意事项是，每次在M3U8中遇到EXT-X-KEY标记时，它都必须始终联系密钥服务器。 在iOS中，DRM策略设置(policy.requireKeyServer)将导致iOS Primetime视频播放器从localhost检索AES解密密钥，而Xbox将始终尝试从远程密钥服务器中检索解密密钥。 没有DRM策略权限来指示Xbox应用程序从localhost检索AES解密密钥。 由于此要求，EXT-X-KEY条目必须在M3U8中且指向Primetime Cloud DRM端点。 此URL通过以下方式设置 &lt;key_url> OfflinePackager.jar配置文件中的config_hls.xml。

如果您希望打包内容一次，并将其流入所有Primetime目标，并且希望将iOS设备配置为不从远程keyserver检索密钥，则可以使用属性为policy.requireKeyServer=false的DRM策略来打包内容（例如在policy_ios_localkeyserver.pol中）。 iOS设备将在本地检索AES密钥，而Xbox设备将忽略此属性，并联系Primetime Cloud DRM密钥服务器以获取解密密钥。

>！注意
>
>所有Xbox360请求都必须利用自定义身份验证/>授权。这是因为在Xbox360平台上，Xbox Live利用Xbox安全令牌服务器(XSTS)令牌进行身份验证。
>Primetime Cloud DRM许可证服务器使用XSTS令牌验证Xbox设备和发出许可证请求的用户完整性。 但是，验证XSTS令牌需要客户的私有Xbox Live供应商密钥，Primetime Cloud DRM不会存储此密钥。 因此，当Primetime Cloud DRM收到来自Xbox 360客户端的许可证请求时，Primetime Cloud DRM会将XSTS令牌转发到Primetime客户的后端身份验证/授权服务器。 Primetime客户的服务器
>之后，将解析并验证XSTS令牌，以确保使用客户的应用程序发布者密钥对其进行签名。
>要从Xbox360客户端传递XSTS令牌，请同步设置令牌以响应MediaPlayer.RequestKeyAttribute >事件，详情请见此处： **在播放器中设置XSTS令牌。** Custom Authentication和Entitlement目录的软件版本中包含一个后端身份验证/授权服务器示例。XSTS令牌的验证将在此处详细讨论： **Xbox Live XSTS令牌验证。**


## 在播放器中设置XSTS令牌 {#set-the-xsts-token-in-your-player}

在Xbox360中，您需要异步设置令牌以响应 `MediaPlayer.RequestKeyAttribute` 事件。

设置XSTS令牌。

与您的软件捆绑在一起的示例应用程序说明了如何在播放器中设置XSTS令牌。 以下是示例播放器中的相关代码片段：

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

对于XSTS请求， `customerSpecificAuthToken` 字段将包含Base64编码的XSTS令牌。 示例 `XSTSValidator` 代码检查Base64解码令牌是否存在 `EncryptedAssertion` 元素；但是，您可以使用其他方法区分这些请求和非Xbox请求。 例如，您可以使用其他URL。

响应消息中返回的策略将覆盖随Xbox密钥请求提供的DRM元数据中的原始策略。 Xbox客户端仅支持策略功能的子集，并且这些字段是将会覆盖原始策略的唯一字段。

需要执行其他设置步骤来支持令牌解密和验证。 您必须加载 [!DNL xsts_partner_cert.pfx] 和 [!DNL x_secure_token_service.part.xboxlive.com.cer] 凭据放入JKS格式密钥库中，然后作为系统属性提供给后端授权服务器 `xsts-keystore`. 默认情况下，合作伙伴 [!DNL .pfx] 具有别名 `xsts`，并且令牌验证证书具有别名 `xsts-verify-cert`. 您也可以使用系统属性覆盖这些内容。 最后，还有一个系统特性 `xsts-keystore-password` 没有默认设置且包含密钥库密码的密码。 系统属性由 `XSTSValidator` 代码概述如下：

| 系统属性 | 默认值 | 注释 |
|---|---|---|
| xsts-keystore | xsts.jks | 验证器使用的JKS格式密钥库。 |
| xsts-keystore-password | | 密钥库的密码 |
| xsts-alias | xsts | 用于从密钥库中检索解密密钥的别名 |
| xsts-verify-cert-alias | xsts-verify-cert | 用于从密钥库检索验证证书的别名 |

## 为XSTS验证器创建JKS{#create-jks-for-an-xsts-validator}

1. 了解位于合作伙伴中的私有证书的别名 [!DNL .pfx] 文件。

   ```
   keytool -list -storetype pkcs12 -keystore xsts_partner_cert.pfx -v 
   ```

1. 转换 [!DNL .pfx] 到 [!DNL .jks].

   ```
   keytool -importkeystore -srckeystore xsts_partner_cert.pfx -srcstoretype PKCS12 \  
           -keystore xsts.jks -srcalias  
   <alias> -destalias xsts
   ```

   (其中 `<alias>` 是您在步骤1中发现的专用证书的别名。)
1. 导入 [!DNL x_secure_token_service.part.xboxlive.com.cer].

   ```
   keytool -importcert -alias xsts-verify-cert -keystore xsts.jks \  
           -file x_secure_token_service.part.xboxlive.com.cer 
   ```

1. Put [!DNL xsts.jks] 在Tomcat主目录中，定义 `-Dxsts-keystore-password=****` 给汤凯的。

如果 [!DNL xsts_partner_cert.pfx] 和 [!DNL xsts.jks] 使用不同的密码，请更新 `xsts` 密码输入 `jks` 让他们变得一样。

```
keytool -keypasswd -keystore xsts.jks -alias xsts 
```
