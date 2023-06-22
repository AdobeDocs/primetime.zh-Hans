---
title: Xbox Live XSTS令牌验证
description: Xbox Live XSTS令牌验证
copied-description: true
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '231'
ht-degree: 0%

---


# Xbox Live XSTS令牌验证{#xbox-live-xsts-token-validation}

对于XSTS请求， `customerSpecificAuthToken` 字段将包含Base64编码的XSTS令牌。 示例 `XSTSValidator` 代码检查Base64解码令牌是否存在 `EncryptedAssertion` 元素；但是，您可以使用其他方法区分这些请求和非Xbox请求。 例如，您可以使用其他URL。

响应消息中返回的策略将覆盖随Xbox密钥请求提供的DRM元数据中的原始策略。 Xbox客户端仅支持一部分策略功能，并且这些字段是唯一将覆盖原始策略的字段。

需要执行额外的设置步骤来支持令牌解密和验证。 您必须加载 [!DNL xsts_partner_cert.pfx] 和 [!DNL x_secure_token_service.part.xboxlive.com.cer] 凭据输入到JKS格式密钥库中，然后作为系统属性提供给后端授权服务器 `xsts-keystore`. 默认情况下，合作伙伴 [!DNL .pfx] 具有别名 `xsts`，并且令牌验证证书具有别名 `xsts-verify-cert`. 您也可以使用系统属性覆盖这些属性。 最后，还有一个系统特性 `xsts-keystore-password` 没有默认设置的，并且包含密钥库密码。 由读取的系统属性 `XSTSValidator` 准则概述如下：

| 系统属性 | 默认值 | 注释 |
|---|---|---|
| `xsts-keystore` | `xsts.jks` | 验证器使用的JKS格式密钥库。 |
| `xsts-keystore-password` |  | 密钥库的密码 |
| `xsts-alias` | `xsts` | 用于从密钥库中检索解密密钥的别名 |
| `xsts-verify-cert-alias` | `xsts-verify-cert` | 用于从密钥库检索验证证书的别名 |

