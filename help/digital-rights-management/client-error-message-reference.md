---
description: 'DRM客户端错误是TVSDK客户端错误的子集。 '
seo-description: 'DRM客户端错误是TVSDK客户端错误的子集。 '
seo-title: DRM客户端错误消息参考
title: DRM客户端错误消息参考
translation-type: tm+mt
source-git-commit: e644e8497e118e2d03e72bef727c4ce1455d68d6

---


# DRM客户端错误消息参考 {#client-error-message-reference}

DRM客户端错误是TVSDK客户端错误的子集，与DRM相关的错误代码范围在3300到3399之间。

## DRM客户端错误 {#drm-client-errors}

| 错误代码 | 助记符 | 补救 |
|---|---|---|
| 3300 | 凭证无效 | 发行商的软件应该做什么： <ul><li> 如果您使用Google Chrome，并且您处于Incognito模式，并且您的Flash Player版本低于11.6，则可能会发生此错误。 我们建议播放器检查浏览器的版本号，并建议用户退出Incognito模式。</li><li> 再次请求许可证。 如果请求成功，则无需记录或升级。 如果请求失败，请记录导致错误的内容。 `subErrorId` 包含行错误（如果有）。</li></ul> 发行商应做的事： <ul><li> 如果对于Chrome以外的Flash版本低于11.6的配置重试失败，则打包中可能出现故障。</li><li>检查问题是否特定于某些内容并重新打包。</li></ul> |
| 3301 | 身份验证失败 | 服务器无法验证或授权客户端。<ul><li>发行商的软件应采取任何必要措施重新建立用户凭据或指导用户访问内容。</li><li>分销商应确认其授权和身份验证机制正常工作。 如果分发商不打算使用身份验证或授权功能，他们应检查违规内容的策略是否需要身份验证，并查看诊断策略／许可证差异。</li></ul> 有关此错误代码的详细信息，请参阅 [DRM错误3301的原因和分辨率](https://forums.adobe.com/thread/1277149)。 |
| 3302 | RequireSSL | 对于Primetime DRM 4.0及更高版本，当远程密钥URL不使用HTTPS作为方案时，iOS上会引发此错误。 需要HTTPS。 <ul><li>如果发行商使用的版本比Primetime DRM版本4早，或至少是版本4，但平台不是iOS，发行商的软件应记录该错误。 此错误仅在iOS上引发。</li><li>如果发行商的软件至少是Primetime DRM版本4，而平台是iOS，则发行商必须更改其用于HTTPS的远程密钥服务器URL。 如果他们只使用HTTP，则分发者可能必须设置HTTPS服务器。 否则，分销商需要将已记录的信息提交给Adobe并升级问题。</li></ul> |
| 3303 | ContentExpired | 您查看的内容已根据内容提供者设置的规则过期。  `subErrorId` 包含客户端特定的错误或行错误。 <ul><li>发行商的软件应尝试从服务器重新获取许可证一次，以确定新的未过期许可证是否可用。 如果没有可用的许可证或许可证已过期，则允许用户获取新的许可证，或通知用户内容无法观看。</li></ul> 如果内容已打包有过期／结束日期已失效的策略，且许可证服务器日志报告PolicyEvaluationException，则声明策略结束日期已失效（服务器错误代码303）。 检查服务器的日志文件以进行验证。<br>如果可能，客户应检查打包过程中使用的策略，以查看该策略是否已过期。 Java命令行工具是： <ul><li>java -jar libs/AdobePolicyManager.jar</li><li> detail demo.pol</li><li>发行商应确认许可证的到期日是否按预期配置。</li></ul> 有关此错误代码的详细信息，请参 [阅使用实时流的AMS/FMS的3303（内容已过期）?](https://forums.adobe.com/thread/1300813) |
| 3304 | 授权失败 | 当前用户无权查看内容。 以其他用户身份登录。<br>有关此错误代码的详细信息，请参阅错误代码3301。 |
| 3305 | ServerConnectionFailed | 由于网络延迟或客户端处于脱机状态，与许可证或域服务器的连接超时。 通常，subErrorId包含HTTP返回代码。<ul><li>发行商的软件应尝试连接到已知良好的服务器。 如果尝试失败，则提示用户重新连接到网络。 如果尝试成功，请记录它。</li><li>分销商应验证正在使用的任何许可证和域服务器是否在线，并从客户端网络中可见。</li></ul>有关此错误代码的详细信息，请参 [阅DRM 3305 ServerConnectionFailed原因和解决方案](https://forums.adobe.com/thread/1284947.) |
| 3306 | ClientUpdateRequired | 当前客户端无法完成所请求的操作，但更新的客户端可能能够完成请求。<br>这可能有几个原因：<ul><li>使用的共享域在此客户端上不可用。 在Chrome上播放时，这种情况很可能发生，但不会出现任何其他浏览器，反之亦然。<br>**注意：**Chrome使用的PHDS/PHLS密钥与其他浏览器使用的不同。</li><li>当应用程序在低于5.0的iOS版本上运行时，正尝试添加多个DRMSession。</li><li>当仅支持版本2时，元数据的版本为3或更高。</li><li>发行商的软件应提醒用户并中止操作。 如果软件可以确定某个升级是否可用，请以适当的方式将用户定向到该平台进行升级。</li><li>如果问题是由于共享域而发生的，则分销商需要向Adobe查询更新的运行时或库。 对于Flash运行时，发行商可以直接在其应用程序中强制升级。 对于图书馆，分销商需要获得更新的图书馆，重建其应用程序并将其部署到其用户。</li></ul>如果问题是由于多个DRMSassiens而发生的，则分销商需要更新其应用程序以在添加多个DRMSassion之前检查iOS版本号。 或者，他们可以限制将其应用程序分发到iOS版本5及更高版本。<br>如果由于元数据版本高于版本2而导致出现问题，则问题可能已损坏元数据。 他们可以尝试重建元数据并查看结果。 如果他们继续发现问题，请记录问题并上报给Adobe。<br>有关此错误代码的详细信息，请参 [阅如何纠正3306 DRMErrorEvent错误代码](https://forums.adobe.com/thread/1266675)。 |
| 3307 | InternalFailure | 这通常表示Primetime DRM代码中的错误，并且是意外的，除非存在已知错误，如下面所示。subErrorId包含客户端特定错误或行错误。<ul><li>如果浏览器是Windows上的Chrome，而Flash版本为11.6（SWF版本19或更高版本），则发行商的软件应假定用户在信息栏上按下“拒绝”，并将其视为3368。</li><li>如果浏览器不是Chrome或Flash版本不是11.6时出现3307，分销商应升级至Adobe。</li></ul>**注意：** 3307:1107296344(FailedToGetBrokerHandle)可能发生在Chrome浏览器版本24-28中。 |
| 3308 | WrongLicenseKey | 每当使用的许可证包含用于解密内容的错误密钥时，都会引发此错误。 subErrorId包含客户端特定的错误或行错误。<br>生成此错误的方法似乎只有两种：<ul><li>客户修改了用于生成许可证的标准Adobe工具（例如，许可证服务器Java框架）。 在这种情况下，许可证包含的密钥可能与任何内容不对应。</li><li>客户已使用相同的许可证ID颁发了多个许可证。 在这种情况下，客户端上有多个可用的许可证，这些许可证与内容元数据匹配，并且Primetime DRM代码选择了错误的许可证供使用。</li><li>发行商的软件应尝试从服务器重新获取许可证。</li><li>如果没有可用的许可证或许可证已过期，请为用户提供一个获取新许可证的工作流，或通知用户内容无法观看，然后记录问题。</li><li> 如果这是域绑定内容（对于AIR），请为用户提供加入域的方式。</li><li>分销商应：</li><li> 确认他们尚未自定义Primetime DRM许可证服务器的许可证发行部分。</li><li>验证他们是否为所有许可证颁发唯一的许可证ID。</li><li>使用Adobe升级问题。</li></ul> |
| 3309 | 损坏的AdditionalHeader | 如果头大于65536字节，则会发生这种情况。<ul><li>发行商的软件应记录导致错误的内容。</li><li>分销商应确认错误在特定内容中是可复制的。 重新打包损坏的内容。</li></ul> |
| 3310 | AppIDMismatch | 应用程序未列入白名单。 Android、iOS或Flash SWF。<br>subErrorId:邮编：1000942;播放受保护的流时出错。 FAXS错误。<br>也可能客户端报告pubID（应用程序发布者ID）的空字符串。<br>**Android:**Android应用程序与使用的应用程序不匹配。 请记住，Android中调试密钥库的目录通常与发行版密钥库的目录不同。<br>**iOS:** 请参阅TVSDK iOS指南中的白名单中的iOS应用程序文档。 |
| 3312 | 许可证完整性 | 再次从服务器下载许可证。 |
| 3313 | WriteMicrosafeFailed | 当系统无法写入文件系统时，会出现此问题。 subErrorId包含客户端特定的错误或行错误。<br>在Microsoft Windows上，当加密内容的licenseID或policyID过长时，Active X或NPAPI插件Flash播放器可能会引发错误3313。 这是因为Windows中路径长度最大。 （Pepper plugin没有此问题。）<ul><li>发行商的软件应提示用户确认其用户目录未锁定，或者卷已满或已锁定。</li><li>如果分销商使用的是AIR而不是Flash，则问题可能由路径长度限制引起。 分销商应将其AIR应用程序的名称缩短到合理的名称。</li></ul> |
| 3314 | 损坏的DRMMetadata | 此错误通常表示内容已使用测试PKI证书进行打包，而播放器是使用生产PKI构建的，反之亦然。<br>subErrorId包含客户端特定的错误或行错误。<ul><li>发行商的软件应记录导致错误的内容。</li><li>分销商应确认该错误在特定内容中是可再现的。</li></ul>您可能必须重新打包损坏的内容。 |
| 3315 | PermissionDenied | 存在已知错误，当需要3305时，可能会引发此错误代码。 有关详细信息，请参阅错误代码3305。<br>不允许AIR加载的远程SWF访问Primetime DRM功能。 如果在网络访问过程中发生安全错误，也可能引发此错误代码。 例如，目标服务器不能通过使用crossdomain.xml连接客户端，或者crossdomain.xmlis不可访问。<br>有关详细信息，请参 [阅DRM错误3315可能的根本原因和分辨率](https://forums.adobe.com/thread/1266592)。 |
| 3317 | AAXS_LoadAdobeCPFailed | **重要说明：** 这是一个罕见的错误，通常在生产环境中不会发生。<br>如果确实发生错误，您可以执行下列操作之一：<ul><li>如果您使用的是AIR，请重新安装AIR。</li><li>如果您使用的是Flash Player，请再次下载AdobeCP模块。</li></ul> |
| 3318 | 不兼容AdobeCPVersion | **重要说明：** 这是一个罕见的错误，通常在生产环境中不会发生。<br>如果确实发生错误，您可以执行下列操作之一：<ul><li>如果您使用的是AIR，请重新安装AIR。</li><li>如果您使用的是Flash Player，请再次下载AdobeCP模块。</li></ul> |
| 3319 | 缺少AdobeCPGetAPI | **重要说明：** 这是一个罕见的错误，通常在生产环境中不会发生。<br>如果确实发生错误，您可以执行下列操作之一：<ul><li>如果您使用的是AIR，请重新安装AIR。</li><li>如果您使用的是Flash Player，请再次下载AdobeCP模块。</li></ul> |
| 3320 | 主机失败 | **重要说明：** 这是一个罕见的错误，通常在生产环境中不会发生。<br>如果确实发生错误，您可以执行下列操作之一：<ul><li>如果您使用的是AIR，请重新安装AIR。</li><li>再次下载AdobeCP和Flash Player，因为任一解决方案都可能不同步。</li></ul>该应用程序只需更新Flash Player，这会导致再次下载AdobeCP。 |
| 3321 | I15nFailed | 为客户端提供密钥的过程失败。 subErrorId包含客户端特定的、服务器特定的或行错误。<ul><li>发行商的软件应至少重试一次操作。</li></ul>如果您在Windows上使用Google Chrome，请提供有关如何允许不在沙箱中的插件访问的说明。 有关详细信息，请参阅Google Chrome的无沙箱访问被拒绝。<ul><li>分销商应完成以下任务之一：</li><li>如果错误跨平台一致，您应该向Adobe说明问题。</li><li>如果错误仅限于Windows上的Chrome，请引导用户允许未沙箱化的插件访问。</li></ul>分发商应将其SWF更新至版本19或更高版本。 对于Chrome特定的3321错误，将引发3368错误。 错误3368可由发行商的软件更具体地处理。 此更改在Chrome Stable通道版本26.0.1410.43中引入。注<br>**意：**错误3321:1090519056可能发生在Flash Player版本11.1到11.6中。我们建议您升级到最新的Flash Player版本。<br>有关详细信息，请参[阅DRM错误3321原因和分辨率](https://forums.adobe.com/thread/1277138)。 |
| 3322 | DeviceBindingFailed | 设备看起来与初始化时的配置不匹配。 subErrorId包含客户端特定的或行错误。<br>发行商的软件应完成以下任务之一：<ul><li>如果设备未使用Flash Player，并且正在使用AIR、iOS等，则调用DRMManager.resetDRMVouchers()。</li></ul>如果在开发阶段的iOS上发生此问题，请要求开发人员确认在从第三方预发行版分发系统（例如HockeyApp）下载的构建和从Xcode本地构建之间切换时是否观察到该问题。 在从HockeyApp分发的内部版本和从Xcode分发的内部版本之间切换时，不会完全覆盖以前安装的属性。 这种情况可能触发3322错误。<br>要解决此问题，开发人员应在安装新版本之前从设备中删除旧版本。<ul><li>如果设备正在使用Flash Player，并且无法从3322或3346错误代码中使用，请参阅Adobe的说明，了解如何在 [DRM Error 3322/3346/3368（信息栏问题）中有计划地重置您的DRM许可证存储](https://forums.adobe.com/message/5535907#5535907)。</li></ul>此错误不应经常发生。 在使用漫游配置文件的企业环境中，如果用户查看的是受DRM保护的内容，则随着用户从不同计算机登录而出现的概率错误3322会增加。 如果可能，分销商应尝试从用户处获取此信息。<br>如果错误频繁发生，请升级到Adobe。 无论重置许可证存储是否解决了问题，您都必须通知Adobe，并告知Adobe在哪些浏览器上发生错误。<br>有关详细信息，请参阅以下文章：<ul><li>https://forums.adobe.com/message/5520902</li><li>https://forums.adobe.com/message/5535911</li><li>https://forums.adobe.com/message/5748618</li><li>https://forums.adobe.com/message/6061165</li></ul> |
| 3323 | CorruptGlobalStateStore | DRM客户端使用的文件意外修改。 subErrorId包含客户端特定的或行错误。<ul><li>发行商的软件应引导用户以与错误代码3322相同的方式重置。</li><li>如果GlobalStore的故障率高于用户群硬盘的预期故障率，请将问题上报给Adobe。</li></ul> |
| 3324 | MachineTokenInvalid | 许可证服务器可能无法连接到证书撤销列表(CRL)服务器以刷新其CRL文件，或者客户端计算机正在请求已被许可证服务器撤销的许可证／身份验证。<br>在服务器日志中，错误代码111 isMachineTokenInvalid。 但是，在客户端级别，错误代码111被转换为错误代码3324。<br>DRM许可证服务器管理员应检查客户的许可证服务器是否曾经能够检索Adobe CRL文件。 如果客户使用Tomcat，则可以检查tomcat/temp/目录以查看是否有4个。CRL文件。<ul><li>如果文件位于此目录中，请在Windows资源管理器中双击文件，在CRL查看器应用程序中，确定其中是否有任何文件已过期。</li><li>如果tomcat/temp/中没有文件，则可以假定此许可证服务器由于防火墙或路由问题从未能够连接到Adobe CRL服务器。</li></ul>有关详细信息，请参阅防火墙规则。<br>如果CRL文件不可用或已过期，则必须确认是否可以访问许可证服务器。 在客户的许可证服务器上打开网络嗅探器（例如Charles或Wireshark），重新启动服务器，并让客户端尝试从服务器请求许可证。<br>您可以观察网络流量，以查看对以下URL端点的调用是否成功：注<br>**意：**您还可以在浏览器中输入以下CRL URL，以查看是否可以手动下载每个文件。<ul><li>[https://crl2.adobe.com/Adobe/FlashAccessIndividualizationCA.crl](https://crl2.adobe.com/Adobe/FlashAccessIndividualizationCA.crl)</li><li>[https://crl2.adobe.com/Adobe/FlashAccessIntermediateCA.crl](http://crl2.adobe.com/Adobe/FlashAccessIntermediateCA.crl)</li><li>[https://crl2.adobe.com/Adobe/FlashAccessRootCA.crl](http://crl2.adobe.com/Adobe/FlashAccessRootCA.crl)</li><li>[https://crl3.adobe.com/AdobeSystemsIncorporatedFlashAccessRuntime/LatestCRL.crl](http://crl3.adobe.com/AdobeSystemsIncorporatedFlashAccessRuntime/LatestCRL.crl)</li></ul>如果防火墙规则是打开的，且当前没有3324错误，则可能存在临时网络问题。 检查客户的服务器日志（可能位于/tomcat/logs/目录中），以确定当许可证服务器尝试获取证书撤销列表时是否发生错误。<br>**注意：**在更新CRL文件时，当大量客户端（或突发）向临时网络问题报告3324错误时，可能会发生错误。 网络问题解决后，3324问题也解决了。<br>如果tomcat/temp/目录中存在所有4个CRL文件，并且客户端仍收到3324个错误，则CRL文件可能存在文件访问问题。<br>要解决此问题，您可能需要查看日志并清除现有CRL文件。<br>如果没有服务器问题，请提示用户重置，如错误代码3322中所述。 |
| 3325 | CorruptServerStateStore | DRM客户端使用的文件意外修改。 subErrorId包含客户端特定的或行错误。<ul><li>发行商的软件应再次重试该操作，因为AdobeCP已在内部删除了违规服务器存储，并且应成功重试。 如果重试失败，请记录问题。</li><li>如果重试失败的速率大于用户群硬盘的预期失败率，请将问题升级到Adobe。</li></ul> |
| 3326 | StoreParchetingDetected | 许可证存储已被篡改或损坏，无法再使用。<br>发行商的软件应引导用户按照错误代码3322中所述的方式重置。 |
| 3327 | ClockAppheringDetected | 修复时钟或再次获得授权／许可／域许可。 |
| 3328 | ServerErrorTryAgain | 这是服务器端错误，服务器无法完成来自客户端的请求。 例如，当服务器繁忙、HTTP/500、服务器没有解密请求所需的密钥等时，可能会发生此错误。<br>在客户端上，无法确定出什么问题。 客户必须查看Primetime DRM服务器日志（通常称为AdobeFlashAccess.log），以确定出错的原因。 日志中始终有一个描述性很强的堆栈跟踪，用于指示问题。 subErrorId包含服务器特定的错误或行错误。<br>分销商应查看服务器日志以识别哪个服务器发送此错误。 对于子错误代码为101的3328错误，服务器无法解密该请求。 客户必须验证安装在许可证服务器上的许可证／传输服务器证书是否与打包过程中使用的证书匹配并对应。<br>此外，如果客户使用引用实施，则必须确保在指定主证书和附加证书的flashaccessrefimpl.properties文件中没有错别字。<br> |
| 3329 | ApplicationSpecificError | Primetime DRM不知道特定于应用程序的子错误代码。 subErrorId包含来自发布者自定义的许可证服务器的服务器特定错误。 服务器在特定于应用程序的命名空间中返回一个错误。 |
| 3330 | NeedAuthentication | 当内容配置为要求客户端在获取许可证之前进行身份验证时，会发生此错误。<ul><li>发行商的软件应验证用户身份，然后再次获得许可。 如果您的服务不打算使用身份验证，请记录导致此错误的内容的标识。</li><li>除非将内容配置为需要身份验证，否则此错误不应要求升级。 在这种情况下，请使用正确的策略重新打包违规内容。 如果内容打包正确，请参阅诊断策略／许可证差异。</li></ul> |
| 3331 | ContentNotYetValid | 获得的许可证尚无效。 要解决此问题，请检查客户端时钟是否设置得不正确。 要设置客户端时钟，请重新打包内容或修改许可证服务器配置。 |
| 3332 | CachedLicenseExpired | 再次从服务器获取许可证。 |
| 3333 | PlaybackWindowExpired | 您必须通知用户，在策略过期之前，他们无法播放此内容。 |
| 3334 | DRMPlatform无效 | 不允许此平台播放内容，因为，例如，内容提供者已配置Primetime DRM以拒绝平台上的Primetime DRM的内容，或共享域绑定许可证绑定到用于其他分区的共享域令牌。<br>如果内容未通过使用适当的（CDM功能选通）包装程序认证来打包，则CDM可能会引发此错误。 有关详细信息，请参阅CDM功能门控。<br>如果内容打包时使用的PHDS/PHLS证书不正确，则该内容可能在Chrome中工作，但在其他浏览器中不工作（反之亦然）。<br>**注意：**这是因为Chrome使用不同的PHDS/PHLS证书。<br>要确认正在使用哪个证书，请转储内容元数据的详细信息并查找收件人证书。 |
| 3335 | DRMVersion无效 | 要解决此问题，请完成以下任务之一：<ul><li>升级AIR</li><li>对于Flash Player，请升级AdobeCP模块，然后重试回放。</li></ul> |
| 3336 | InvalidRuntimePlatform | 不允许此平台播放内容，因为例如，内容提供商已配置Primetime DRM以拒绝平台上的FP/AIR提供内容。 |
| 3337 | InvalidRuntimeVersion | 如果内容或服务器配置为拒绝播放特定版本的Flash或AIR运行时，则会发生这种情况。<ul><li>如果用户在Flash可升级的操作系统上，则发行商的软件应提示用户升级Flash，然后重试。 否则，建议用户使用其他计算机。</li><li>如果怀疑出错3337s，请识别是否针对特定内容发生错误，并重新打包该内容。 如果正确打包了内容，请参阅诊断策略／许可证差异。</li></ul> |
| 3338 | UnknownConnectionType | 无法检测连接类型，并且策略要求您打开“输出保护”。 仅当内容打包需要数字或模拟输出保护时，才会出现此问题。<br>低于版本11.8.800.168的Flash Player版本中的一个问题导致错误3338偶尔在策略指示内容保护为“USE IF AVAILABLE（如果可用）”的内容上发生。 此问题已在版本11.8.800.168及更高版本中修复。<ul><li>发行商的软件选择不需要输出保护的内容的变体（例如HD流的SD变体）。 如果USE_IF_AVAILABLE内容发生错误3338，请检查播放器版本号。 如果播放器版本小于11.8.800.168，建议用户升级Flash Player。 如果错误3338发生在高于11.8.800.168的版本上，请记录导致错误的内容。</li><li>分销商应检查导致此错误的内容，并验证内容的策略是否为模拟和数字输出设置了NO_PROTECTION或USE_IF_AVAILABLE。 如果内容因疏忽而与NO_OUTPUT或REQUIRED一起打包，请重新打包内容。 如果正确打包了内容，请参阅诊断策略／许可证差异。 否则将呈报给Adobe。</li></ul>有关详细信息，请 [参阅当DRM策略设置为USE_IF_AVAILABLE时，是否获得意外的3338错误](https://forums.adobe.com/message/5518688)? |
| 3339 | NoAnalogPlaybackAllowed | 无法在模拟设备上回放。 要解决此问题，请连接数字设备。 |
| 3340 | NoAnalogProtectionAvail | 无法播放内容，因为连接的模拟外部显示设备（监视器／电视）没有正确的功能（例如，设备没有Macrovision或ACP）。 |
| 3341 | NoDigitalPlaybackAllowed | 无法在数字设备上播放内容。 |
| 3342 | NoDigitalProtectionAvail | 连接的数字外部显示设备（显示器／电视）没有正确的功能。 例如，设备没有HDCP。 |
| 3343 | 内部错误 | 当前已知该错误最初在发布新版Flash后发生。 这是因为在Flash打开时Flash升级了，这使Flash在浏览器重新启动之前处于不良状态。<ul><li>发行商的软件应完成以下任务：</li><li>建议用户关闭或退出所有浏览器，然后重新打开。</li><li>检查Flash的版本是否为最新版本。</li></ul>如果版本不是最新版本，建议客户升级，关闭其浏览器中的所有选项卡，然后重新打开。<ul><li>如果在成功重新启动浏览器后出现错误，请升级到Adobe。 发布新版本后，我们建议您联系Adobe支持部门以了解后台更新问题是否已得到修复。</li></ul> |
| 3344 | 缺少AdobeCPModule | 部分Flash或AIR安装不正确。<br>要解决此问题，请完成以下任务之一：<ul><li>对于AIR，用户必须再次卸载并安装AIR。</li><li>对于Flash Player，调用System.update。</li></ul> |
| 3346 | 迁移失败 | 发行商的软件应执行下列操作之一：<ul><li>如果是AIR，则调用DRMManager.resetDRMVouchers()。</li><li>如果Flash因错误3322或3346而无法使用，用户应转到 [https://forums.adobe.com/message/5535907#5535907](https://forums.adobe.com/message/5535907#5535907) ，并按照Adobe文章的说明以编程方式重置其DRM许可证存储。</li><li>如果此错误频繁发生，分销商应向Adobe提供有关频率播放器版本和浏览器版本的详细信息。</li></ul>有关详细信息，请参阅以下论坛文章：<ul><li>[Chrome中的DRM错误3322/3346/3368（信息栏问题）](https://forums.adobe.com/message/5520902)</li><li>[硬件更改后出现3322或3346错误](https://forums.adobe.com/message/5535911)</li></ul> |
| 3347 | InsufficibleDeviceCapabilities | 此错误的主要含义是许可证具有客户端的DRM证书指示其无法满足的约束。 颁发客户端DRM证书时，将定义以下“硬件功能”:<ul><li>**非用户可访问的总线。** 如果 **为真**，则解密的媒体从不会流经总线或进入应用程序可以访问它的主存储器。 如果 **为false**，则在解密后，应用程序可能可以访问内容。</li><li>**硬件信任根。** 如果 **为true**，则在设备上启动时加载的所有软件都会针对仅在硬件中可用的密钥或摘要进行验证。 当针对客户端的DRM证书打开许可证并且立即失败时，在客户端检查这两个限制。 在发布许可证之前，还可以在服务器端检查这些限制。</li></ul>此错误的次要含义是许可证已设置“Jailbreak Enforcement”策略，并且已在设备上检测到jailbreak。 此检查在客户端定期完成，在服务器端无法检查。<br>分销商可以更新策略并删除限制。 对于设备功能策略，发出包含-devCapabilitiesV1标志且无参数的策略更新命令。 用于jailbreak enforcementsetpolicy.enforceJailbreak=false。 |
| 3348 | HardStopIntervalExpired | 硬停止间隔已过期。 |
| 3349 | ServerVersionTooHigh | 服务器运行的版本高于客户端支持的最高版本。 |
| 3350 | ServerVersionTooLow | 服务器运行的版本低于客户端支持的最低版本。 |
| 3351 | DomainTokenInvalid | 域令牌无效。 要解决此问题，请再次向域注册。 |
| 3352 | DomainTokenTooOld | 域令牌比许可证所需的令牌旧。 要解决此问题，请再次向域注册。 |
| 3353 | DomainTokenTooNew | 域令牌比许可证所需的令牌新。 |
| 3354 | DomainTokenExpired | 域令牌已过期。 |
| 3355 | DomainJoinFailed | 域加入失败。 |
| 3356 | NoEncodeRoot | 找不到V3叶许可证的根许可证。 |
| 3357 | NoValidEmbeddedLicense | 未找到有效的嵌入式许可。 |
| 3358 | NoACPProtectionAvailable | 无法回放，因为连接的模拟设备没有ACP保护。 |
| 3359 | NoCGSMAProtectionAvailable | 无法回放，因为连接的模拟设备没有CGMSA保护。 |
| 3360 | DomainRegistrationRequired | 内容需要域注册。 |
| 3361 | NotRegisteredToDomain | 计算机未注册到指定元数据的域。 |
| 3362 | OperationTimeoutError | 异步操作比配置的maxOperationTimeout所花费的时间更长。<br>**注意：**此错误代码仅由iOS DRMNative Framework返回。 |
| 3363 | 不支持的IOSPlaylistError | M3U8播放列表包含不支持的内容，或缺少必需的#EXT-X-FAXS-CM DRM元数据对象。<br>**注意：**此错误代码仅由iOS DRMNative Framework返回。 |
| 3364 | NoDeviceId | 框架请求了设备ID，但返回的值为空。<br>框架请求了设备ID，但返回的值为空。<br>在Chrome浏览器设置中，用户不应选中“允许受 **保护内容的标识符** ”复选框。 |
| 3365 | IncognitoModeNotAllowed | 此浏览器／平台组合不允许在Incognito模式下播放受DRM保护的内容。<br>发行商的软件应建议用户退出Incognito模式或使用其他浏览器。 有关详细信息，请参 [阅DRM错误3365的原因和分辨率](https://forums.adobe.com/thread/1266622)。 |
| 3366 | BadParameter | 主机运行时使用错误的参数称为Primetime DRM库。 |
| 3367 | BadSignature | M3U8清单签名失败。<br>**注意：**此错误代码仅由iOS DRMNative Framework或AVE返回。 |
| 3368 | UserSettingsNoAccess | 用户取消了操作或输入了不允许访问系统的设置。<br>此错误仅在SWF版本19或更高版本中引发。 为了向后兼容，对于SWF版本18或更早版本，将引发错误代码3321。<br>分销商的软件应引导用户说明如何允许未沙箱化插件访问。 有关详细信息，请参 [阅Google Chrome的无沙箱访问被拒绝](https://helpx.adobe.com/adobe-access/kb/error-3321.html) , [Chrome中的DRM错误3322/3346/3368（信息栏问题）](https://forums.adobe.com/message/5520902)。 |
| 3369 | InterfaceNotAvailable | 必需的浏览器界面不可用。 此问题仅在Pepper上发生。 Flash插件与浏览器版本之间可能不匹配。<br>发行商的软件应指导用户确保他们安装了最新版本的浏览器。<br>如果此错误的发生率在增加，并且与正在发布的浏览器更新相对应，则升级到Adobe。 |
| 3370 | ContentIdSettingsNoAccess | 用户已禁用了“允许 **保护内容的标识符”设置。**<br>**注意：** 在Pepper版本13.0.0.x或更高版本中出现此错误。<br>发行商的软件和／或操作团队应指导用户启用“允许 **受保护内容的标识符** ”设置。<br>有关详细信息，请参 [阅https://forums.adobe.com/message/6518323#6518323](https://forums.adobe.com/message/6518323#6518323)。 |
| 3371 | NoOPConstraintInPixelConstraints | 基于许可证中的输出保护限制的分辨率格式不正确。<br>发行商的软件应显示错误消息。 要求用户向分销商报告问题并提供内容标题。<br>分销商应使用有效的策略重新打包内容。 |
| 3372 | 分辨率LagerThanMax分辨率 | 内容的分辨率大于在输出保护约束中指定的最大分辨率。<br>如果分销商的操作团队在其日志中看到此错误，则应查看基于分辨率的输出保护策略，并在必要时重新打包内容。<br>有关基于分辨率的输出保护的详细信息，请参阅关于基于分辨率的输出保护。 |
| 3373 | DisplayResolutionLagerThanConstrain | 内容的分辨率大于当前活动的输出保护约束所指定的分辨率。<br>如果分销商的操作团队在其日志中看到此错误，则应查看基于分辨率的输出保护策略，并在必要时重新打包内容。<br>有关基于分辨率的输出保护的详细信息，请参阅关于基于分辨率的输出保护。 |
| 3374 | ClientCommProcessFailed | 在客户端通信处理期间失败，例如，请求生成、响应处理、错误的身份验证令牌等。 |

## 3328的子错误代码映射 {#suberror-code-mapping-for-3328}

| SubError | 说明 |
|---|---|
| 100-1000 | 由Adobe的License Server保留 |
| 10000 - 20000 | 由Adobe的个性化服务器保留 |
| 20100-21000 | 为Adobe Xbox密钥服务器保留。<br>此范围中的错误映射到一般Primetime DRM Server SDK错误消息参考，如下所示：<br>Xbox Keyserver错误= DRM Server Error + 0x20000<br>例如，Xbox Keyserver Error 20202等同于DRM Server SDK Error 202 |
| 100xxxx | 保留给客户端子错误代码 |