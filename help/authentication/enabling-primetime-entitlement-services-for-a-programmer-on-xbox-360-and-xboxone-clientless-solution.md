---
title: 在Xbox 360和XboxOne无客户端上为程序启用Primetime授权服务
description: 在Xbox 360和XboxOne无客户端上为程序启用Primetime授权服务
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '433'
ht-degree: 0%

---


# 在Xbox 360和XboxOne无客户端上为程序启用Primetime授权服务 {#enabling-primetime-entitlement-services-for-a-programer-on-xbox-360-and-xboxone-clientless}

>[!NOTE]
>
>此页面上的内容仅供参考。 使用此API需要获得Adobe的当前许可证。 不允许未经授权使用。




1. 程序员通过提供以下信息，为Xbox 360/One启用Primetime身份验证无客户端解决方案创建Zendesk票证：

   1. 平台：例如Xbox 360、Xbox One

   1. 请求者ID:例如netgeo、CNN等

1. Adobe将创建X509证书并在其末尾配置私钥和密码。

1. Adobe将在票证中或通过电子邮件向程序提供公共证书（X509证书）。

1. 然后，程序员需要在GDNP门户中安装该公共证书，以便向Microsoft注册应用程序。

1. 然后，程序员将分别从Microsoft Xbox Live服务请求XboxOne或360的JWT（Java Web令牌）或STS令牌，该令牌将使用步骤3中提供的X509公共证书进行加密。

1. 这些令牌包含Xbox设备的唯一deviceId。 使用“x”参数在授权标头中包含令牌（JWT或STS），如下所示：

   1. 对于Xbox 360,XSTS令牌必须采用Base64编码，然后才能发送到Primetime付费电视身份验证。
   1. 对于Xbox One，JWT已正确编码，因此不应进行额外编码。 

1. 来自Xbox设备的所有API调用都应包含授权标头，该标头在x参数中具有上述令牌。

 

>[!NOTE]
>
>Xbox尤其具有一些与数字签名相关的独特要求。 XBox控制台的设备ID包含在XSTS令牌中。  对于Xbox 360，这是加密的SAML断言；对于Xbox One，这是加密的JWT。 XBox控制台应用程序会将整个XSTS令牌发送到Primetime付费电视身份验证。 Primetime pay-TV身份验证使用其公钥对令牌解密，解析令牌，并从中提取deviceId 。

>[!NOTE]
>
>由于XSTS令牌的长度较大，因此XBox控制台存在技术限制：无法将令牌作为HTTPGET参数发送到Primetime付费电视身份验证API。 要解决此问题，Primetime付费电视身份验证允许在调用API时，将XSTS令牌作为HTTP标头“授权”的一部分发送。 XSTS令牌必须使用Primetime付费电视身份验证中颁发给程序员的X.509证书中的公钥进行加密。 Primetime pay-TV身份验证会存储关联的私钥，并使用它解密XSTS令牌并从中提取deviceId。  


