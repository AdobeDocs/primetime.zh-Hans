---
seo-title: Xbox Live XSTS令牌验证
title: Xbox Live XSTS令牌验证
uuid: 9647f8ee-32d6-4bed-bae2-8b36a72d04ce
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# Xbox Live XSTS令牌验证{#xbox-live-xsts-token-validation}

对于XSTS请求，字 `customerSpecificAuthToken` 段将包含Base64编码的XSTS令牌。 样本代 `XSTSValidator` 码检查Base64解码的令牌是否存在元 `EncryptedAssertion` 素；但是，您可以使用其他方法来区分这些请求和非Xbox请求。 例如，您可以使用其他URL。

响应消息中返回的策略将覆盖随Xbox密钥请求提供的DRM元数据中的原始策略。 Xbox客户端只支持部分策略功能，这些字段是将覆盖原始策略的唯一字段。

需要其他设置步骤来支持令牌解密和验证。 必须将和凭 [!DNL xsts_partner_cert.pfx] 据加载 [!DNL x_secure_token_service.part.xboxlive.com.cer] 到JKS格式密钥库中，然后作为系统属性将其提供给后端授权服务器 `xsts-keystore`。 默认情况下，合作伙 [!DNL .pfx] 伴具有别名， `xsts`而令牌验证证书具有别名 `xsts-verify-cert`。 您还可以使用系统属性覆盖这些属性。 最后，有一个系统属 `xsts-keystore-password` 性没有默认值，并且包含keystore密码。 代码读取的系统属 `XSTSValidator` 性概述如下：

| 系统属性 | 默认值 | 评论 |
|---|---|---|
| `xsts-keystore` | `xsts.jks` | 验证程序使用的JKS格式密钥库。 |
| `xsts-keystore-password` |  | 密钥库的密码 |
| `xsts-alias` | `xsts` | 用于从密钥库检索解密密钥的别名 |
| `xsts-verify-cert-alias` | `xsts-verify-cert` | 用于从密钥库检索验证证书的别名 |

