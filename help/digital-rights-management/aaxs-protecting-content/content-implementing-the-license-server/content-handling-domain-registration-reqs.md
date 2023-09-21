---
title: 处理域注册请求
description: 处理域注册请求
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '553'
ht-degree: 0%

---

# 处理域注册请求{#handling-domain-registration-requests}

如果DRM元数据指示播放内容需要域注册，则客户端应用程序应调用DRMManager.addToDeviceGroup()ActionScriptAPI或joinLicenseDomain() iOS API。 如果客户端尚未向指定的域服务器注册（或者如果应用程序正在强制重新加入），则会发送域注册请求。 域服务器确定是否允许客户端加入域，并向客户端发出一个或多个域凭据。

* 请求处理程序类为 `com.adobe.flashaccess.sdk.protocol.domain.DomainRegistrationHandler`
* 请求消息类为 `com.adobe.flashaccess.sdk.protocol.domain.DomainRegistrationRequestMessage`
* 如果客户端和服务器都支持协议版本5，则请求URL为“元数据： + &quot;/flashaccess/domain/v4中的域服务器URL”。 否则，请求URL是元数据“ + &quot;/flashaccess/domain/v3”中的域服务器URL

初始化时 `DomainRegistrationHandler`，必须指定域服务器URL。 此URL将包含在处理程序颁发的域令牌中，以指示颁发令牌的域服务器。 该URL必须与任何要求向服务器注册域的策略中指定的域服务器URL匹配。

要确定是否允许客户端加入域，服务器可以检查请求中的计算机和用户信息。 请参阅 [使用计算机标识符](../../aaxs-protecting-content/content-implementing-the-license-server/content-processing-aaxs-requests/content-using-machine-ids.md) 有关如何识别和计数加入域的计算机的信息。 服务器还可以确定允许客户端加入哪个域。 请注意，客户机只能是每个域服务器URL的一个域的成员。 如果计算机已具有此域服务器URL的域令牌，则域注册请求将包含当前域名( `getRequestDomainName()`)。 对于重新加入请求，域服务器必须返回此域的当前域凭据集或返回错误（域服务器不能返回其他域的域凭据）。

如果域服务器需要身份验证才能加入域，则该请求应包含身份验证令牌。 与许可证请求一样，域注册可能需要用户名/密码或自定义身份验证。 请参阅 [用户身份验证](../../aaxs-protecting-content/content-introduction/content-usage-rules/content-authentication/content-user-authentication.md) 以了解有关处理身份验证令牌的详细信息。

域服务器负责存储和管理与每个域关联的域密钥。 当需要为域（域的第一个域注册）生成新密钥对时，调用 `generateDomainCredential` `(String, int, Principal, Date)`. 此方法将生成新的域密钥对和域证书。 域服务器必须存储私钥和证书，并在处理此域的后续请求时提供这些对象。 也可以为域生成新的密钥对，以滚动密钥。 将鼠标指针置于特定域的键上时，请确保在中递增键版本 `generateDomainCredential` 也一样。

以后每次机器向同一域注册时，都应使用相同的域私钥和证书。 调用 `addDomainCredential(DomainToken, PrivateKey)` 将现有的域凭据返回到客户端。 如果由于域密钥已更改而导致域有多个域凭据，则服务器应为当前域密钥和所有以前的域密钥提供域凭据，以便客户端可以使用绑定到旧域密钥的许可证。 这样可以将绑定到旧域令牌的许可证移动到新注册的计算机上并且仍然可以播放。
