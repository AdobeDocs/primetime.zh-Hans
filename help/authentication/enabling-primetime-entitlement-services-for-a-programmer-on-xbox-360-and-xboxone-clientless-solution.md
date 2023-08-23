---
title: 为Xbox 360和XboxOne无客户端程序员启用Primetime授权服务
description: 为Xbox 360和XboxOne无客户端程序员启用Primetime授权服务
exl-id: ff7254de-9ea4-4c27-a186-d1c2eea12222
source-git-commit: 84a16ce775a0aab96ad954997c008b5265e69283
workflow-type: tm+mt
source-wordcount: '433'
ht-degree: 0%

---

# 为Xbox 360和XboxOne无客户端程序员启用Primetime授权服务 {#enabling-primetime-entitlement-services-for-a-programer-on-xbox-360-and-xboxone-clientless}

>[!NOTE]
>
>此页面上的内容仅供参考。 使用此API需要来自Adobe的当前许可证。 不允许未经授权使用。




1. 该程序员通过提供以下信息创建Zendesk票证，以启用Xbox 360/One用于Primetime身份验证无客户端解决方案：

   1. 平台：如Xbox 360、Xbox One

   1. 请求者ID：例如netgeo、CNN等。

1. Adobe将创建X509证书，并在其末尾配置私钥和口令。

1. Adobe将在票证中或通过电子邮件向程序员提供公共证书（X509证书）。

1. 然后，程序员需要在GDNP门户上为注册到Microsoft的应用程序安装该公共证书。

1. 然后，程序员将分别向Microsoft Xbox Live服务请求XboxOne或360的JWT（Java Web令牌）或STS令牌，该服务将使用步骤3中提供的X509公共证书进行加密。

1. 这些令牌包含Xbox设备的唯一deviceId。 使用“x”参数在授权标头中包含令牌（JWT或STS），如下所示：

   1. 对于Xbox 360，在发送到Primetime付费电视身份验证之前，XSTS令牌必须为Base64编码。
   1. 对于Xbox One，JWT已正确编码，因此不应进行额外编码。

1. 从Xbox设备发出的所有API调用都应在x参数中包含具有上述令牌的授权标头。



>[!NOTE]
>
>特别是Xbox有一些与数字签名相关的独特要求。 XBox控制台的设备ID包含在XSTS令牌中。  对于Xbox 360，这是一个加密的SAML断言；对于Xbox One，这是一个加密的JWT。 XBox控制台应用程序将整个XSTS令牌发送到Primetime付费电视身份验证。 Primetime付费电视身份验证使用其公钥解密令牌，解析令牌，然后从其中提取deviceId。

>[!NOTE]
>
>由于XSTS令牌的长度很大，因此XBox控制台存在技术限制：它无法将令牌作为HTTPGET参数发送到Primetime付费电视身份验证API。 为了解决这个问题，Primetime付费电视身份验证允许在调用API时发送XSTS令牌作为HTTP标头“授权”的一部分。 XSTS令牌必须使用从Primetime付费电视身份验证颁发给程序员的X.509证书中的公钥进行加密。 Primetime付费电视身份验证存储关联的私钥，并使用它解密XSTS令牌并从中提取deviceId。
