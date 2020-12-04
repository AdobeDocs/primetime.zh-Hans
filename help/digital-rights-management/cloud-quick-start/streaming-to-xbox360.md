---
description: 'null'
seo-description: 'null'
seo-title: 在播放器中设置XSTS令牌
title: 在播放器中设置XSTS令牌
uuid: 8995e029-deee-4e23-9cda-a50de8c4f2c0
translation-type: tm+mt
source-git-commit: c37061c116b8a6bc8ce085dc89dc8aadd0a2e490
workflow-type: tm+mt
source-wordcount: '843'
ht-degree: 0%

---


# 流到Xbox360（可选）{#streaming-to-xboc360}

Primetime DRM可在Xbox360平台上使用。 但是，仅支持“受保护流”用例，不支持完整的DRM策略权限套件。 不支持非流DRM策略权限，如设备域组。 Xbox360在尝试播放内容时忽略不支持的权限。

Xbox支持的Primetime DRM政策权利包括：
* 数字输出保护
* 许可证脱机缓存结束日期
* 许可开始日期
* 许可证结束日期
* 播放窗口持续时间（秒）

如果内容已经打包用于其他Primetime平台（如iOS、Android或桌面），则可能不必重新打包以流式传输到Xbox360。

Xbox360的一个注意事项是，每次在M3U8中遇到EXT-X-KEY标签时，它必须始终与关键服务器连接。 与iOS不同，在iOS中，DRM策略设置(policy.requireKeyServer)将导致iOS Primetime视频播放器从localhost检索AES解密密钥，Xbox将始终尝试从远程密钥服务器检索解密密钥。 没有DRM策略权利指示Xbox应用程序检索AES解密
localhost中的键。 由于这一要求，EXT-X-KEY条目必须位于指向Primetime Cloud DRM端点的M3U8中。 此URL通过OfflinePackager.jar配置文件config_hls.xml中的&lt;key_url>设置。

如果您希望将内容打包一次并使其流化到所有Primetime目标，并将iOS设备配置为不从远程密钥服务器检索密钥，则可以使用属性policy.requireKeyServer=false的DRM策略（如policy_ios_localkeyserver.pol）来打包内容。 iOS设备将在本地检索AES密钥，而Xbox设备将忽略此属性并连接到Primetime Cloud DRM密钥服务器
解密密钥。

>!Note
>
>所有Xbox360请求必须使用“自定义身份验证”/>“授权”。这是因为在Xbox360平台上，Xbox Live >利用Xbox安全令牌服务器(XSTS)令牌来进行身份验证。
>Primetime Cloud DRM许可证服务器使用XSTS令牌>验证Xbox设备和发出>许可证请求的用户的完整性。 但是，验证XSTS令牌需要>客户的专用Xbox Live供应商密钥，Primetime Cloud DRM>不存储该密钥。 因此，当Primetime Cloud DRM收到Xbox 360客户端发出的超过一个许可证请求时，Primetime Cloud DRM >将将XSTS令牌转发到Primetime客户的后端>身份验证／授权服务器。 Primetime客户的服务器
>然后，将解析并验证XSTS令牌，以确保它使用客户的应用程序发布者密钥进行>签名。
>要从Xbox360客户端传递XSTS令牌，请设置令牌>同步以响应MediaPlayer.RequestKeyAttribute >事件-详情请见：**在播放器中设置XSTS令牌。** “自定义身份验证”>“授权”目录中的软件版本中包含一个示例后端身份验证／授权服务器。此处将进一步详细讨论XSTS令牌的验证： **Xbox Live XSTS令牌验证。**


## 在播放器{#set-the-xsts-token-in-your-player}中设置XSTS令牌

在Xbox360中，您以异步方式设置令牌以响应`MediaPlayer.RequestKeyAttribute`事件。

设置XSTS令牌。

与软件捆绑的范例应用程序演示如何在播放器中设置XSTS令牌。 以下是示例播放器中的相关代码片段：

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

## Xbox Live XSTS令牌验证{#xbox-live-xsts-token-validation}

对于XSTS请求，`customerSpecificAuthToken`字段将包含Base64编码的XSTS令牌。 示例`XSTSValidator`代码检查Base64解码的令牌是否存在`EncryptedAssertion`元素；但是，您可以使用其他方法来区分这些请求和非Xbox请求。 例如，您可以使用其他URL。

响应消息中返回的策略将覆盖随Xbox密钥请求提供的DRM元数据中的原始策略。 Xbox客户端只支持策略功能的子集，这些字段是将覆盖原始策略的唯一字段。

需要其他设置步骤来支持令牌解密和验证。 必须将[!DNL xsts_partner_cert.pfx]和[!DNL x_secure_token_service.part.xboxlive.com.cer]凭据加载到JKS格式密钥库中，然后作为系统属性`xsts-keystore`提供给后端授权服务器。 默认情况下，合作伙伴[!DNL .pfx]具有别名`xsts`，令牌验证证书具有别名`xsts-verify-cert`。 您还可以使用系统属性覆盖这些属性。 最后，有一个系统属性`xsts-keystore-password`，它没有默认值，并且包含密钥库密码。 `XSTSValidator`代码读取的系统属性概述如下：

| 系统属性 | 默认值 | 评论 |
|---|---|---|
| xsts-keystore | xsts.jks | 验证程序使用的JKS格式密钥库。 |
| xsts-keystore-password |  | 密钥库的密码 |
| xsts-alias | xst | 用于从密钥库检索解密密钥的别名 |
| xsts-verify-cert-alias | xsts-verify-cert | 用于从密钥库检索验证证书的别名 |

## 为XSTS validator{#create-jks-for-an-xsts-validator}创建JKS

1. 查找位于合作伙伴[!DNL .pfx]文件中的私人证书的别名。

   ```
   keytool -list -storetype pkcs12 -keystore xsts_partner_cert.pfx -v 
   ```

1. 将[!DNL .pfx]转换为[!DNL .jks]。

   ```
   keytool -importkeystore -srckeystore xsts_partner_cert.pfx -srcstoretype PKCS12 \  
           -keystore xsts.jks -srcalias  
   <alias> -destalias xsts
   ```

   （其中`<alias>`是您在步骤1中发现的专用证书的别名。）
1. 导入[!DNL x_secure_token_service.part.xboxlive.com.cer]。

   ```
   keytool -importcert -alias xsts-verify-cert -keystore xsts.jks \  
           -file x_secure_token_service.part.xboxlive.com.cer 
   ```

1. 将[!DNL xsts.jks]放在Tomcat主目录中，并为Tomcat定义`-Dxsts-keystore-password=****`。

如果[!DNL xsts_partner_cert.pfx]和[!DNL xsts.jks]使用不同的口令，请更新`jks`中的`xsts`口令，使其相同。

```
keytool -keypasswd -keystore xsts.jks -alias xsts 
```
