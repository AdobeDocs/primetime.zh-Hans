---
title: 集成媒体令牌验证器
description: 集成媒体令牌验证器
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '916'
ht-degree: 0%

---


# 集成媒体令牌验证器

>[!NOTE]
>
>此页面上的内容仅供参考。 使用此API需要获得Adobe的当前许可证。 不允许未经授权使用。

## 关于媒体令牌验证器 {#about-media-token-verifier}

授权成功后，Adobe Primetime身份验证会创建一个长期授权(AuthZ)令牌。  AuthZ令牌可以传递到客户端，也可以存储在服务器端，具体取决于客户端的平台。  (请参阅 [了解令牌](/help/authentication/programmer-overview.md#understanding-tokens) ，以了解令牌如何存储在不同客户端系统上，以及其他详细信息。)


AuthZ令牌可授权站点用户查看给定的资源。  它的典型生存时间(TTL)为6到24小时，令牌将在此之后过期。 **对于实际查看访问，Primetime身份验证使用AuthZ令牌生成一个短暂的媒体令牌，您可以获取该令牌并将其传递到媒体服务器**. 这些短时间的媒体令牌的TTL非常短（通常为几分钟）。


在AccessEnabler集成中，您可通过 `setToken()` 回调。 对于无客户端API集成，您可以通过 `<SP_FQDN>/api/v1/tokens/media` API调用。 令牌是以明文形式发送的字符串，由Adobe签名，使用基于PKI（公钥基础结构）的令牌保护。 使用基于PKI的保护，令牌使用非对称密钥进行签名，由认证机构颁发给Adobe。


由于客户端上没有对令牌进行验证，因此恶意用户可能会使用工具注入假 `setToken()` 调用。 因此，您 **无法** 只是依赖于 `setToken()` 在考虑用户是否已授权时触发。 您必须验证短暂的令牌本身是否合法。 执行验证的工具是媒体令牌验证器库。


>[!TIP]
>
>您必须将返回的令牌字符串的整个长度传递到媒体令牌验证器以进行验证。

## 使用媒体令牌验证器验证短暂的令牌 {#validate-short-livedttokens}

我们建议程序员将令牌发送到使用媒体令牌验证器库的Web服务，以便在实际启动视频流之前验证令牌。 短生存期媒体令牌的极短TTL被定义为足够长，以允许在生成令牌的服务器和验证令牌的服务器之间出现时钟同步问题，但不再存在。



的 [媒体令牌验证器库](https://adobeprimetime.zendesk.com/auth/v2/login/signin?return_to=https%3A%2F%2Ftve.zendesk.com%2Fhc%2Fen-us%2Farticles%2F204963159-Media-Token-Verifier-library&amp;theme=hc&amp;locale=en-us&amp;brand_id=343429&amp;auth_origin=343429%2Cfalse%2Ctrue){target=_blank} 适用于Primetime身份验证合作伙伴。



媒体令牌验证器库包含在Java存档中 `mediatoken-verifier-VERSION.jar`. 库定义：

* 令牌验证API(`ITokenVerifier` 界面)，包含JavaDoc文档
* 用于验证令牌是否确实来自Adobe的Adobe公钥
* 参考实现(`com.adobe.entitlement.test.EntitlementVerifierTest.java`)，以显示如何使用验证器API以及如何使用库中包含的Adobe公钥来验证其源


存档包含所有依赖项和证书密钥库。 包含的证书密钥库的默认密码为“123456”。

* 验证库需要JDK版本1.5或更高版本。
* 使用首选的JCE提供程序对签名算法“SHA256WithRSA”进行签名。


**验证器库必须是用于分析令牌内容的唯一方法。 程序员不应解析令牌并提取数据本身，因为令牌格式无法得到保证，并且可能会在将来发生更改。** 只有验证器API才能正常运行。 直接解析字符串可能会暂时起作用，但在格式可能发生更改时，会在将来出现问题。 验证器API从令牌中检索信息，例如：

* 令牌是否有效( `isValid()` 方法)?
* 与令牌( `getResourceID()` 方法);这可以与（并且应该与） `setToken()` 函数回调。 如果二者不匹配，这可能表示欺诈行为。
* 发出令牌的时间(`getTimeIssued()` 方法)。
* TTL(`getTimeToLive()` 方法)。
* 从MVPD(`getUserSessionGUID()` 方法)。
* 用于验证用户身份的分发商ID（如果是） — 为分发商提供身份验证的代理MVPD。

## 使用验证器API {#using-verifier-api}

的 `ITokenVerifier` 类定义用于验证给定资源的令牌真实性的方法。 使用 `ITokenVerifier` 分析响应于 `setToken()` 请求。


的 `isValid()` 方法是验证令牌的主要方法。 需要一个参数，即资源ID。 如果您传递了空资源ID，此方法将仅验证令牌真实性和有效期。


的 `isValid()` 方法会返回以下状态值之一：



| VALID_TOKEN | 所有验证都成功 |
|--------------------|-----------------------------------------|
| INVALID_TOKEN_FORMAT | 令牌格式无效 |
| INVALID_SIGNATURE | 无法验证令牌真实性 |
| TOKEN_EXPIRED | 令牌TTL无效 |
| INVALID_RESOURCE_ID | 令牌对给定资源无效 |
| ERROR_UNKNOWN | 尚未验证令牌 |

其他方法可提供对资源ID的特定访问、发布时间以及给定令牌的生存时间。

* 使用 `getResourceID()` 要检索与令牌关联的资源ID，并将其与setToken()请求返回的ID进行比较。
* 使用 `getTimeIssued()` 用于检索令牌发出的时间。
* 使用 `getTimeToLive()` 来检索TTL。
* 使用 `getUserSessionGUID()` 用于检索由MVPD设置的匿名化GUID。
* 使用 `getMvpdId()` 用于检索已对用户进行身份验证的MVPD的ID。
* 使用 `getProxyMvpdId()` 用于检索已对用户进行身份验证的代理MVPD的ID。

## 示例代码 {#sample-code}

媒体令牌验证器存档包含引用实施(`com.adobe.entitlement.test.EntitlementVerifierTest.java`)和使用测试类调用API的示例。 此示例(`com.adobe.entitlement.text.EntitlementVerifierTest.java`)说明了令牌验证库与媒体服务器的集成。


```Java
package com.adobe.entitlement.test; 
import com.adobe.entitlement.verifier.CryptoDataHolder;
import com.adobe.entitlement.verifier.ITokenVerifier;
import com.adobe.entitlement.verifier.ITokenVerifierFactory;
import com.adobe.entitlement.verifier.SimpleTokenPKISignatureVerifierFactory;
import com.adobe.tve.crypto.SignatureVerificationCredential; 
import java.io.InputStream; 

public class EntitlementVerifierTest { 
    String mRequestorID = null;
    String mTokenToVerify = null;
    String mPathToCertificate = null;
    String mKeystoreType = null;
    String mKeystorePasswd = null;
    String mResourceID = null;

    public static void main(String[] args) { 
        if (args == null || args.length < 2 ) {
            System.out.println("Incorrect args: Usage: EntitlementVerifierTest requestorID tokenToVerify [resourceID]");
            return;
        } 
        String requestorID = args[0];
        String tokenToVerify = args[1];
        String pathToCertificate = "media_token_keystore.jks"; // the default keystore provided in the entitlement jar 
        String keystoreType = "jks";
        String keystorePasswd = "123456"; // password for the default keystore 
        if (requestorID == null || tokenToVerify == null) {
            System.out.println("One or more arguments is null");
            return;
        } 
        System.out.println("RequestorID: " + requestorID);
        System.out.println("token: " + tokenToVerify);
        System.out.println("cert: " + pathToCertificate);
        System.out.println("keystoretype: " + keystoreType);
        System.out.println("keystore passwd: " + keystorePasswd);
        String resourceID = null;
        if (args.length > 2) {
            resourceID = args[2];
        }
        System.out.println("Resource ID: " + resourceID);
        EntitlementVerifierTest verifier = new EntitlementVerifierTest(requestorID,
            tokenToVerify, pathToCertificate, keystoreType, keystorePasswd, resourceID);
        verifier.verifyToken();
    } 

    protected EntitlementVerifierTest(String inRequestorID,
                                      String inTokenToVerify,
                                      String inPathToCertificate,
                                      String inKeystoreType,
                                      String inKeystorePasswd, String inResourceID) {
        mRequestorID = inRequestorID;
        mTokenToVerify = inTokenToVerify;
        mPathToCertificate = inPathToCertificate;
        mKeystoreType = inKeystoreType;
        mKeystorePasswd = inKeystorePasswd;
        mResourceID = inResourceID;
    } 

    protected void verifyToken() {
        // It is expected that the SignatureVerificationCredential and 
        // CryptoDataHolder could be created at Init time in a web application 
        // and be reused for all token verifications. 
        CryptoDataHolder cryptoData = createCryptoDataHolder(mPathToCertificate, mKeystoreType, mKeystorePasswd);
        ITokenVerifierFactory tokenVerifierFactory = new SimpleTokenPKISignatureVerifierFactory();
        ITokenVerifier tokenVerifier = tokenVerifierFactory.getInstance(mRequestorID, mTokenToVerify, cryptoData);
        ITokenVerifier.eReturnValue status = tokenVerifier.isValid(mResourceID);
        System.out.println("Is token Valid? : " + status.toString());
        System.out.println("Token User ID: " + tokenVerifier.getUserSessionGUID());
        System.out.println("Token was generated at: " + tokenVerifier.getTimeIssued());

        System.out.println("Token Mvpd ID: " + tokenVerifier.getMvpdId());
        System.out.println("Token Proxy Mvpd ID: " + tokenVerifier.getProxyMvpdId());
    } 
    protected CryptoDataHolder createCryptoDataHolder(String pathToCertificate,
                                                      String keystoreType, String keystorePasswd) {
        SignatureVerificationCredential verificationCredential =
            readShortTokenVerificationCredential(pathToCertificate, keystoreType, keystorePasswd);
        CryptoDataHolder cryptoData = new CryptoDataHolder();
        cryptoData.setCertificateInfo(verificationCredential);
        return cryptoData;
    } 
    protected SignatureVerificationCredential readShortTokenVerificationCredential(String keystoreFile,
                                                                                   String keystoreType,
                                                                                   String keystorePasswd) {
        SignatureVerificationCredential cred = null; 
        if (keystoreFile != null){
            try {
                // load the keystore file 
                ClassLoader loader = EntitlementVerifierTest.class.getClassLoader();
                InputStream certInputStream =  loader.getResourceAsStream(keystoreFile);
                if (certInputStream != null) {
                    cred = new SignatureVerificationCredential(certInputStream, keystorePasswd, keystoreType);          
                }
            }
            catch (Exception e) {
                System.out.println("Error creating short token server credentials: " + e.getMessage());
            }
        }
        if (cred == null) {
            System.out.println("Error creating short token server credentials");
        } 
        return cred;
    } 
}
```
