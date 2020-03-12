---
seo-title: 处理域注册请求
title: 处理域注册请求
uuid: e0cef9c4-b2d1-4bec-8dce-50452bc826fb
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# 处理域注册请求{#handling-domain-registration-requests}

如果DRM元数据指示播放内容需要域注册，则客户端应用程序应调用DRMManager.addToDeviceGroup()ActionScript API或joinLicenseDomain()iOS API。 如果客户端尚未向指定的域服务器注册（或如果应用程序强制重新加入），则会发送域注册请求。 域服务器确定是否允许客户端加入域并向客户端发出一个或多个域凭证。

* 请求处理函数类为 `com.adobe.flashaccess.sdk.protocol.domain.DomainRegistrationHandler`
* 请求消息类为 `com.adobe.flashaccess.sdk.protocol.domain.DomainRegistrationRequestMessage`
* 如果客户端和服务器支持协议版本5，则请求URL为元数据中的“域服务器URL:+ &quot;/flashaccess/domain/v4&quot;。 否则，请求URL为元数据&quot; + &quot;/flashaccess/domain/v3&quot;中的域服务器URL

初始化时 `DomainRegistrationHandler`，必须指定域服务器URL。 此URL将包含在由处理程序发出的域令牌中，以指示发出令牌的域服务器。 该URL必须与任何需要向服务器进行域注册的策略中指定的域服务器URL匹配。

为了确定是否允许客户端加入域，服务器可以检查请求中的机器和用户信息。 有关如 [何识别和计数加入域的计算机的信息](../../aaxs-protecting-content/content-implementing-the-license-server/content-processing-aaxs-requests/content-using-machine-ids.md) ，请参阅使用计算机标识符。 服务器还可以确定允许客户端加入的域。 请注意，客户端可能只是每个域服务器URL一个域的成员。 如果计算机已具有此域服务器URL的域令牌，则域注册请求将包括当前域名( `getRequestDomainName()`)。 对于重新加入请求，域服务器必须返回此域的当前域凭据集或返回错误（域服务器不能返回其他域的域凭据）。

如果域服务器要求身份验证才能加入域，则请求应包含身份验证令牌。 与许可证请求一样，域注册可能需要用户名／密码或自定义身份验证。 有关处 [理身份验证令牌的详细信息](../../aaxs-protecting-content/content-introduction/content-usage-rules/content-authentication/content-user-authentication.md) ，请参阅用户身份验证。

域服务器负责存储和管理与每个域相关联的域密钥。 当需要为域（域的第一个域注册）生成新的密钥对时，调用 `generateDomainCredential``(String, int, Principal, Date)`。 此方法将生成新的域密钥对和域证书。 域服务器必须存储私钥和证书，并在处理此域的后续请求时提供这些对象。 还可以为域生成新的密钥对，以便在密钥上滚动。 当滚动到特定域的键时，请务必也增加键 `generateDomainCredential` 版本。

每当计算机注册到同一域时，应使用相同的域私钥和证书。 调 `addDomainCredential(DomainToken, PrivateKey)` 用以将现有域凭证返回给客户端。 如果由于域密钥已更改而域有多个域凭据，则服务器应为当前域密钥和所有以前的域密钥提供域凭据，以便客户端可以使用绑定到旧域密钥的许可证。 这使得绑定到旧域令牌的许可证可以移动到新注册的计算机并仍可播放。
