---
description: DRM客户端错误是TVSDK客户端错误的一个子集。
title: DRM客户端错误消息参考
exl-id: 3d74cb92-c0a7-4eab-91b8-7e60a9c33df4
source-git-commit: 1bc2f6c230c262babf2958c32fee31afcad04c2f
workflow-type: tm+mt
source-wordcount: '5173'
ht-degree: 1%

---

# DRM客户端错误消息参考 {#client-error-message-reference}

DRM客户端错误是TVSDK客户端错误的一个子集，与DRM相关的错误代码范围从3300到3399。

## DRM客户端错误 {#drm-client-errors}

| 错误代码 | 助记符 | 补救措施 |
|---|---|---|
| 3300 | 优惠券无效 | 分发商的软件应该做什么： <ul><li> 如果您使用的是Google Chrome，并且处于无痕模式，而Flash Player版本低于11.6，则可能会发生此错误。 我们建议播放器检查浏览器的版本号，并建议用户退出无痕模式。</li><li> 再次请求许可证。 如果请求成功，则无需记录或上报。 如果请求不成功，请记录导致错误的内容。 `subErrorId` 包含行错误（如果存在）。</li></ul> 分发程序应执行的操作： <ul><li> 如果Flash低于版本11.6的Chrome以外的配置上的重试不成功，则打包中可能会发生失败。</li><li>检查该问题是否特定于某些内容和重新打包。</li></ul> |
| 3301 | 身份验证失败 | 服务器无法对客户端进行身份验证或授权。<ul><li>分发商的软件应采取任何必要的操作来重新建立用户的凭据，或指导用户获取对内容的访问权限。</li><li>分发服务器应确认其授权和身份验证机制运行正常。 如果分发商不打算使用身份验证或授权功能，则应检查违规内容的策略是否需要身份验证，并参阅诊断策略/许可证差异。</li></ul> 有关此错误代码的详细信息，请参阅 [DRM错误3301原因和解决方法](https://forums.adobe.com/thread/1277149). |
| 3302 | RequireSSL | 对于Primetime DRM 4.0及更高版本，当远程密钥URL不使用HTTPS作为方案时，会在iOS上引发此错误。 需要HTTPS。 <ul><li>如果分发服务器使用的版本低于Primetime DRM版本4，或至少使用版本4，但平台不是iOS，则分发服务器的软件应记录该错误。 此错误仅在iOS上引发。</li><li>如果分发商的软件至少是Primetime DRM版本4，并且平台是iOS，则分发商必须将他们使用的远程密钥服务器URL更改为HTTPS。 如果分发商仅使用HTTP，则可能必须设置HTTPS服务器。 否则，分销商需要提交记录的信息以Adobe并上报问题。</li></ul> |
| 3303 | ContentExpired | 根据内容提供商设置的规则，您查看的内容已过期。  `subErrorId` 包含特定于客户端的错误或行错误。 <ul><li>分发服务器的软件应尝试从服务器重新获取许可证一次，以确定是否有新的未过期的许可证可用。 如果没有许可证可用或许可证已过期，则允许用户获取新的许可证，或者通知用户内容无法观看。</li></ul> 如果内容已打包带有过期日期/结束日期的策略，并且许可证服务器日志报告PolicyEvaluationException，则声明策略结束日期已过期（服务器错误代码303）。 检查服务器的日志文件以进行验证。<br>如果可能，客户应检查他们在打包过程中使用的策略，以查看它是否已过期。 Java命令行工具是： <ul><li>java -jar libs/AdobePolicyManager.jar</li><li> detail demo.pol</li><li>分销商应确认许可证过期日期是否按预期配置。</li></ul> 有关此错误代码的详细信息，请参阅 [使用实时流的AMS/FMS的3303（内容已过期）？](https://forums.adobe.com/thread/1300813) |
| 3304 | AuthorizationFailed | 当前用户无权查看内容。 以其他用户身份登录。<br>有关此错误代码的更多信息，请参阅错误代码3301。 |
| 3305 | ServerConnectionFailed | 由于网络延迟或客户端脱机，与许可证或域服务器的连接超时。 通常，subErrorId包含HTTP返回代码。<ul><li>分发服务器的软件应尝试与已知正常的服务器建立网络连接。 如果尝试失败，则提示用户重新连接到网络。 如果尝试成功，请将其记录。</li><li>分发服务器应验证任何正在使用的许可证和域服务器是否在线并从客户端网络可见。</li></ul>有关此错误代码的详细信息，请参阅 [DRM 3305 ServerConnectionFailed原因和解决方法](https://forums.adobe.com/thread/1284947.) |
| 3306 | Clientupdaterequired | 当前客户端无法完成请求的操作，但更新的客户端可能能够完成请求。<br>这可能有几个原因：<ul><li>使用的共享域在此客户端上不可用。 当播放在Chrome上运行时，可能出现这种情况，但是其他任何浏览器都无法正常工作，反之亦然。<br>**注意：** Chrome使用的PHDS/PHLS密钥与其他浏览器使用的不同。</li><li>在5.0之前的iOS版本上运行时，应用程序尝试添加多个DRMSession。</li><li>仅支持版本2时，元数据的版本为3或更高版本。</li><li>分发商的软件应提醒用户并中止操作。 如果软件能够确定升级是否可用，则以适合平台的方式将用户引导至该升级。</li><li>如果问题是由共享域引起的，分发服务器将需要向Adobe确认更新的运行时或库。 在Flash运行时的情况下，分发服务器可以直接在其应用程序中强制升级。 对于库，分发服务器将需要获取更新的库，重建其应用程序并将其部署到其用户。</li></ul>如果由于多个DRMSessions而出现问题，分发服务器将需要更新其应用程序以在添加多个DRMSessions之前检查iOS版本号。 或者，他们可以将其应用程序限制分发到iOS版本5及更高版本。<br>如果由于元数据版本高于版本2而出现问题，则问题可能是元数据已损坏。 他们可以尝试重建元数据并查看结果。 如果他们仍然看到问题，请记录问题并升级至Adobe。<br>有关此错误代码的详细信息，请参阅 [如何纠正3306 DRMErrorEvent错误代码](https://forums.adobe.com/thread/1266675). |
| 3307 | 内部故障 | 这通常表示Primetime DRM代码中的错误，除非存在如下所示的已知错误，否则属于意外情况。subErrorId包含特定于客户端的错误或行错误。<ul><li>如果Windows上的Flash是Chrome，而浏览器版本是11.6(SWF版本19或更高版本)，则分发服务器的软件应假定用户在infobar上按“拒绝”，并将此视为一个3368。</li><li>如果浏览器不是Chrome或Flash版本不是11.6时出现3307，则分发服务器应升级为Adobe。</li></ul>**注意：** 3307：1107296344 (FailedToGetBrokerHandle)可能会在Chrome浏览器版本24-28中发生。 |
| 3308 | WrongLicenseKey | 当使用的许可证包含用于解密内容的错误密钥时，将引发此错误。 subErrorId包含特定于客户端的错误或行错误。<br>生成此错误似乎只有两种方式：<ul><li>客户已修改用于生成许可证的标准Adobe工具（例如，许可方服务器Java框架）。 在这种情况下，许可证包含可能未与任何内容对应的错误密钥。</li><li>客户已使用相同的许可证ID颁发了多个许可证。 在这种情况下，客户端上存在多个与内容元数据匹配的许可证，并且Primetime DRM代码选择了错误的许可证来使用。</li><li>分发服务器的软件应尝试从服务器重新获取许可证。</li><li>如果没有许可证可用或许可证已过期，请提供工作流以便用户获取新许可证，或者通知用户内容无法观看，并记录问题。</li><li> 如果这是域绑定的内容(适用于AIR)，则提供用户加入域的方法。</li><li>分发服务器应：</li><li> 确认他们尚未自定义Primetime DRM许可证服务器的许可证颁发部分。</li><li>验证他们是否为所有许可证颁发了唯一的许可证ID。</li><li>使Adobe问题升级。</li></ul> |
| 3309 | CorruptedAdditionalHeader | 如果标头大于65536字节，则会发生这种情况。<ul><li>分发服务器的软件应记录导致错误的内容段。</li><li>分发服务器应确认错误可随特定内容片段重现。 重新打包损坏的内容。</li></ul> |
| 3310 | AppIDMismatch | 应用程序不允许列出。 Android、iOS或FlashSWF。<br>subErrorId： 1000942；播放受保护的流时出错。 FAXS错误。<br>客户端可能还会报告pubID （应用程序发布者ID）的空字符串。<br>**Android：** Android应用程序与正在使用的应用程序不匹配。 请记住，Android中调试密钥库的目录通常与发行密钥库的目录不同。<br>**iOS：** 请参阅 [允许列表iOS应用程序](/help/programming/tvsdk-3x-ios-prog/ios-3x-drm-content-security/ios-3x-allowlist-your-ios-application.md) TVSDK iOS指南中的文档。 |
| 3312 | 许可证完整性 | 再次从服务器下载许可证。 |
| 3313 | WriteMicrosafeFailed | 当系统无法写入文件系统时，会出现此问题。 subErrorIdcontains客户端特定的错误或行错误。<br>在Microsoft Windows上，当加密的内容具有licenseID或policyID太长时，Active X或NPAPI插件flash player可能会引发错误3313。 这是因为Windows中的最大路径长度。 （Pepper插件没有此问题。）<ul><li>分发服务器的软件应提示用户确认其用户目录未锁定，也不在已满或已锁定的卷上。</li><li>如果分发服务器使用的是AIR而不是Flash，则问题可能是由路径长度限制引起的。 分销商应将其AIR应用程序的名称缩短为一些合理的名称。</li></ul> |
| 3314 | CorruptedDRMMetadata | 此错误通常表示内容与测试PKI证书一起打包，并且播放器使用生产PKI构建，反之亦然。<br>subErrorId包含特定于客户端的错误或行错误。<ul><li>分发服务器的软件应记录导致该错误的内容段。</li><li>分发服务器应确认该错误可随特定内容片段重现。</li></ul>您可能需要重新打包损坏的内容。 |
| 3315 | PermissionDenied | 存在已知的错误，当预期出现3305时，可能会引发此错误代码。 有关详细信息，请参阅错误代码3305。<br>AIR加载的远程SWF不允许访问Primetime DRM功能。 如果在网络访问期间发生安全错误，也可能会引发此错误代码。 例如，目标服务器未通过使用crossdomain.xml进行连接的客户端，或crossdomain.xmlis不可访问。<br>有关更多信息，请参阅 [DRM错误3315可能的根本原因和解决方法](https://forums.adobe.com/thread/1266592). |
| 3317 | AAXS_LoadAdobeCPF失败 | **重要提示：** 这是一个罕见的错误，通常不会在生产环境中发生。<br>如果出现错误，您可以执行以下操作之一：<ul><li>如果您使用的是AIR，请重新安装AIR。</li><li>如果您使用的是Flash Player，请重新下载AdobeCP模块。</li></ul> |
| 3318 | IncompatibleAdobeCPVersion | **重要提示：** 这是一个罕见的错误，通常不会在生产环境中发生。<br>如果出现错误，您可以执行以下操作之一：<ul><li>如果您使用的是AIR，请重新安装AIR。</li><li>如果您使用的是Flash Player，请重新下载AdobeCP模块。</li></ul> |
| 3319 | MissingAdobeCPGetAPI | **重要提示：** 这是一个罕见的错误，通常不会在生产环境中发生。<br>如果出现错误，您可以执行以下操作之一：<ul><li>如果您使用的是AIR，请重新安装AIR。</li><li>如果您使用的是Flash Player，请重新下载AdobeCP模块。</li></ul> |
| 3320 | 主机失败 | **重要提示：** 这是一个罕见的错误，通常不会在生产环境中发生。<br>如果出现错误，您可以执行以下操作之一：<ul><li>如果您使用的是AIR，请重新安装AIR。</li><li>下载AdobeCP并重新Flash播放器，因为其中任一解决方案可能不同步。</li></ul>该应用程序只需要更新Flash Player，这会导致再次下载AdobeCP。 |
| 3321 | I15nFailed | 使用密钥设置客户端的过程失败。 subErrorId包含特定于客户端、特定于服务器或行的错误。<ul><li>分发服务器的软件应至少重试一次该操作。</li></ul>如果您在Windows上使用Google Chrome，请解释如何允许不在沙盒中的插件访问。 有关更多信息，请参阅Google Chrome的非沙盒访问被拒绝。<ul><li>分发服务器应完成以下任务之一：</li><li>如果错误在各个平台之间保持一致，则应使用Adobe来重新计算问题。</li><li>如果错误仅限于Windows上的Chrome，请引导用户允许无沙盒插件访问。</li></ul>分销商应将其SWF更新至版本19或更高版本。 对于特定于Chrome的3321错误，会引发3368错误。 错误3368可以由分发服务器的软件更具体地处理。 此更改已在Chrome稳定渠道版本26.0.1410.43中引入。<br>**注意：** Flash播放器版本11.1到11.6可能发生错误3321：1090519056。我们建议您升级到最新的Flash Player版本。<br>有关更多信息，请参阅 [DRM错误3321原因和解决方法](https://forums.adobe.com/thread/1277138). |
| 3322 | DeviceBindingFailed | 设备似乎与初始化时存在的配置不匹配。 subErrorId包含特定于客户端的错误或行错误。<br>分发服务器的软件应完成以下任务之一：<ul><li>如果设备未使用Flash Player，而是使用AIR、iOS等， `callDRMManager.resetDRMVouchers()`.</li></ul>如果iOS上发生问题且处于开发阶段，请要求开发人员确认在从第三方预发行分发系统（例如HockeyApp）下载的内部版本和从Xcode下载的本地内部版本之间进行切换时，是否发现该问题。 在从HockeyApp分发的版本和从Xcode分发的版本之间切换时，不会完全覆盖以前安装的属性。 这种情况可能会触发3322错误。<br>要解决此问题，开发人员应先从设备中删除旧内部版本，然后再安装新内部版本。<ul><li>如果设备正在使用Flash Player，并且在3322或3346错误代码中无法使用，请参阅Adobe中有关如何以编程方式重置您的DRM许可证存储区的说明。 [Chrome中的DRM错误3322/3346/3368（信息栏问题）](https://forums.adobe.com/message/5535907#5535907).</li></ul>此错误不应频繁发生。 在使用漫游配置文件的公司环境中，如果用户正在查看受DRM保护的内容，则当用户从不同计算机登录时，发生错误3322的可能性会增加。 如有可能，分发服务器应尝试从用户处获取此信息。<br>如果错误频繁发生，请升级至Adobe。 您必须通知Adobe重置许可证存储是否已解决问题，并告知Adobe哪些浏览器上发生了错误。<br>有关更多信息，请参阅以下文章：<ul><li>https://forums.adobe.com/message/5520902</li><li>https://forums.adobe.com/message/5535911</li><li>https://forums.adobe.com/message/5748618</li><li>https://forums.adobe.com/message/6061165</li></ul> |
| 3323 | CorruptedGlobalStateStore | DRM客户端使用的文件已被意外修改。 subErrorId包含特定于客户端的错误或行错误。<ul><li>分发服务器的软件应引导用户按照与错误代码3322相同的方式进行重置。</li><li>如果GlobalStore的故障率高于用户群硬盘的预期故障率，请将问题升级至Adobe。</li></ul> |
| 3324 | MachineTokenInvalid | 许可证服务器可能无法连接到证书吊销列表(CRL)服务器以刷新其CRL文件，或者客户端计算机正在请求许可证服务器已吊销的许可证/身份验证。<br>在服务器日志中，错误代码111 isMachineTokenInvalid。 然而，在客户端级别，错误代码111被转换为错误代码3324。<br>DRM许可证服务器管理员应检查客户的许可证服务器是否能够检索AdobeCRL文件。 如果客户使用的是Tomcat，则可以检查tomcat/temp/目录以查看是否存在4个.CRL文件。<ul><li>如果文件位于此目录中，双击Windows资源管理器和CRL查看器应用程序中的文件，确定是否有任何文件已过期。</li><li>如果tomcat/temp/中没有文件，则可以假定由于防火墙或路由问题，此许可证服务器从未能够访问AdobeCRL服务器。</li></ul>有关详细信息，请参阅防火墙规则。<br>如果CRL文件不可用或已过期，则必须确认是否可以访问许可证服务器。 在客户的许可证服务器上打开一个网络探查器（例如Charles或Wireshark），重新启动服务器，然后让客户端尝试从服务器请求许可证。<br>您可以观察网络流量，以查看对以下URL端点的调用是否成功：<br>**注意：** 您还可以在浏览器中输入以下CRL URL，以查看是否可以手动下载每个文件。<ul><li>[https://crl2.adobe.com/Adobe/FlashAccessIndividualizationCA.crl](https://crl2.adobe.com/Adobe/FlashAccessIndividualizationCA.crl)</li><li>[https://crl2.adobe.com/Adobe/FlashAccessIntermediateCA.crl](http://crl2.adobe.com/Adobe/FlashAccessIntermediateCA.crl)</li><li>[https://crl2.adobe.com/Adobe/FlashAccessRootCA.crl](http://crl2.adobe.com/Adobe/FlashAccessRootCA.crl)</li><li>[https://crl3.adobe.com/AdobeSystemsIncorporatedFlashAccessRuntime/LatestCRL.crl](http://crl3.adobe.com/AdobeSystemsIncorporatedFlashAccessRuntime/LatestCRL.crl)</li></ul>如果防火墙规则处于打开状态，并且当前没有任何3324错误，则可能是临时网络问题。 检查客户的服务器日志（可能位于/tomcat/logs/目录中），以确定许可证服务器尝试获取证书吊销列表时是否出现错误。<br>**注意：** 在续订CRL文件时，如果大量客户端（或突发）报告3324错误，可能会发生临时网络问题。 网络问题解决后，3324问题也得以解决。<br>如果所有4个CRL文件都存在于tomcat/temp/目录中，并且客户端仍收到3324错误，则对CRL文件的文件访问可能会出现问题。<br>要解决此问题，您可能需要查看日志并清除现有CRL文件。<br>如果没有服务器问题，则提示用户按照错误代码3322中的说明进行重置。 |
| 3325 | CorruptedServerStateStore | DRM客户端使用的文件已被意外修改。 subErrorId包含特定于客户端的错误或行错误。<ul><li>分发服务器的软件应再次重试该操作，因为AdobeCP已在内部删除了违规服务器存储，重试应会成功。 如果重试失败，请记录问题。</li><li>如果重试失败率高于用户群硬盘的预期失败率，则将问题升级至Adobe。</li></ul> |
| 3326 | StoreTamperingDetected | 许可证存储已被篡改或损坏，无法再使用。<br>分发服务器的软件应引导用户按照错误代码3322中所述的方式进行重置。 |
| 3327 | ClockTamperingDetected | 修复时钟或再次获取身份验证/许可证/域许可证。 |
| 3328 | ServerErrorTryArgety | 这是服务器端错误，服务器无法完成来自客户端的请求。 例如，当服务器繁忙、HTTP/500、服务器没有解密请求所需的密钥等情况时，就会发生此错误。<br>在客户端，无法确定哪里出错。 客户必须查看Primetime DRM服务器日志（通常称为AdobeFlashAccess.log），以确定哪里出了问题。 日志中始终有一个描述性很强的栈栈跟踪指示问题。 subErrorId包含服务器特定的错误或行错误。<br>分发服务器应查看服务器日志，以识别哪个服务器正在发送此错误。 对于具有子错误代码101的3328错误，服务器无法解密请求。 客户必须验证许可证服务器上安装的许可证/传输服务器证书是否与打包期间使用的证书匹配和相对应。<br>此外，如果客户使用参考实施，他们必须确保flashaccessrefimpl.properties文件中没有指定主证书和其他证书的拼写错误。<br> |
| 3329 | ApplicationSpecificError | Primetime DRM不知道特定于应用程序的子错误代码。 subErrorId包含来自发布服务器自定义许可证服务器的特定于服务器的错误。 服务器在特定于应用程序的命名空间中返回了错误。 |
| 3330 | 需要身份验证 | 当内容配置为在获取许可证之前要求客户端进行身份验证时，会发生此错误。<ul><li>分发商的软件应该对用户进行身份验证，然后再次获取许可证。 如果您的服务不打算使用身份验证，请记录导致此错误的内容标识。</li><li>此错误不应要求提升，除非不应将内容配置为要求身份验证。 在这种情况下，请使用适当的策略重新打包违规内容。 如果内容已正确打包，请参阅诊断策略/许可证差异。</li></ul> |
| 3331 | ContentNotYetValid | 获得的许可证尚未生效。 要解决此问题，请检查客户端时钟设置是否正确。 要设置客户端时钟，请重新打包内容或修改许可证服务器配置。 |
| 3332 | CachedLicenseExpired | 再次从服务器获取许可证。 |
| 3333 | PlaybackWindowsExpired | 您必须通知用户，在策略过期之前，他们无法播放此内容。 |
| 3334 | InvalidDRMPlatform | 此平台不允许播放内容，例如，因为内容提供商已将Primetime DRM配置为拒绝对平台上Primetime DRM的内容，或者共享域绑定许可证已绑定到用于不同分区的共享域令牌。<br>如果未使用适当的（CDM功能选通）打包器认证来打包内容，CDM可能会引发此错误。 有关详细信息，请参阅CDM功能选通。<br>如果内容与不正确的PHDS/PHLS证书一起打包，则该内容可能在Chrome中有效，但在其他浏览器中无效（反之亦然）。<br>**注意：** 这是因为Chrome使用不同的PHDS/PHLS证书。<br>要确认使用了哪个证书，请转储内容元数据的详细信息并查找收件人证书。 |
| 3335 | InvalidDRMVersion | 要解决此问题，请完成以下任务之一：<ul><li>升级AIR</li><li>对于Flash Player，请升级AdobeCP模块并重试播放。</li></ul> |
| 3336 | InvalidRuntimePlatform | 此平台不允许播放内容，例如，因为内容提供商已将Primetime DRM配置为拒绝向平台上的FP/AIR发送内容。 |
| 3337 | InvalidRuntimeVersion | 如果内容或服务器配置为拒绝播放特定版本的Flash或AIR运行时，则会发生这种情况。<ul><li>如果用户使用的是可以升级Flash的操作系统，则分发服务器的软件应提示用户升级Flash并重试。 否则，建议用户使用其他计算机。</li><li>如果怀疑错误3337s，请确定特定内容是否出现该错误，然后重新打包该内容。 如果内容正确打包，请参阅诊断策略/许可证差异。</li></ul> |
| 3338 | UnknownConnectionType | 无法检测连接类型，策略要求您打开输出保护。 仅当封装的内容需要数字或模拟输出保护时，才可能出现此问题。<br>早于版本11.8.800.168的Flash Player版本中存在的一个问题，该问题会导致内容上偶尔出现错误3338，策略指出该内容保护为USE IF AVAILABLE。 此问题已在版本11.8.800.168及更高版本中修复。<ul><li>分发商的软件选择不需要输出保护的内容的变体（例如HD流的SD变体）。 如果onUSE_IF_AVAILABLE内容出现错误3338，请检查播放器版本号。 如果播放器版本低于11.8.800.168，建议用户升级Flash Player。 如果在11.8.800.168以上的版本中出现错误3338，请记录导致该错误的内容。</li><li>分发服务器应检查导致此错误的内容，并验证该内容的策略是否为模拟和数字输出设置NO_PROTECTION或USE_IF_AVAILABLE。 如果无意中将内容打包为NO_OUTPUT或REQUIRED ，请重新打包内容。 如果内容正确打包，请参阅诊断策略/许可证差异。 否则，将升级至Adobe。</li></ul>有关更多信息，请参阅 [将DRM策略设置为USE_IF_AVAILABLE时出现意外的3338错误](https://forums.adobe.com/message/5518688)？ |
| 3339 | NoAnalogPlaybackAllowed | 无法在模拟设备上播放。 要解决此问题，请连接数字设备。 |
| 3340 | NoAnalogProtectionAvail | 无法播放内容，因为连接的模拟外部显示设备（显示器/电视）没有正确的功能（例如，该设备没有Macrovision或ACP）。 |
| 3341 | NoDigitalPlaybackAllowed | 无法在数字设备上播放内容。 |
| 3342 | NoDigitalProtectionAvail | 连接的数字外部显示设备（显示器/电视）没有正确的功能。 例如，设备没有HDCP。 |
| 3343 | 内部错误 | 目前已知此错误最初发生在发布新版本的Flash之后。 发生此错误的原因是Flash在Flash打开时升级，这会使Flash处于不良状态，直到浏览器重新启动。<ul><li>分发服务器的软件应完成以下任务：</li><li>建议用户关闭或退出所有浏览器，然后重新打开。</li><li>检查Flash的版本是否为当前版本。</li></ul>如果版本不是最新的，建议客户升级，关闭其浏览器中的所有选项卡，然后重新打开。<ul><li>如果在成功重新启动浏览器后似乎出现错误，请升级至Adobe。 发布新版本后，我们建议您联系Adobe支持，以查看后台更新问题是否已修复。</li></ul> |
| 3344 | MissingAdobeCPModule | 未正确安装Flash或AIR的一部分。<br>要解决此问题，请完成以下任务之一：<ul><li>对于AIR，用户必须卸载并重新安装AIR。</li><li>对于Flash Player，请调用System.update。</li></ul> |
| 3346 | 迁移失败 | 分发服务器的软件应执行以下操作之一：<ul><li>如果AIR，请调用 `DRMManager.resetDRMVouchers()`.</li><li>如果Flash因错误3322或3346而不可用，用户应转到 [https://forums.adobe.com/message/5535907#5535907](https://forums.adobe.com/message/5535907#5535907) 并按照Adobe文章的说明以编程方式重置其DRM许可证存储区。</li><li>如果此错误频繁发生，分发服务器应提供要Adobe的频率播放器版本和浏览器版本的详细信息。</li></ul>有关更多信息，请参阅以下论坛文章：<ul><li>[Chrome中的DRM错误3322/3346/3368（信息栏问题）](https://forums.adobe.com/message/5520902)</li><li>[硬件更改后出现3322或3346错误](https://forums.adobe.com/message/5535911)</li></ul> |
| 3347 | 设备功能不足 | 此错误的主要含义是许可证具有客户端的DRM证书指示它无法满足的约束。 在颁发客户端DRM证书时，将定义以下“硬件功能”：<ul><li>**非用户访问总线。** 如果 **true**&#x200B;时，解密的媒体绝不会流经总线或进入主内存（应用程序可访问该主内存）。 如果 **false**，内容在解密后可供应用程序访问。</li><li>**信任的硬件根目录。** 如果 **true**，则启动时加载到设备上的所有软件均会根据仅在硬件中可用的密钥或摘要进行验证。 当针对客户端的DRM证书打开许可证时，客户端会检查这两个约束，并且故障会立即发生。 在颁发许可证之前，还可以在服务器端检查这些限制。</li></ul>此错误的次要含义是许可证设置了“Jailbreak Enforcement”策略，并在设备上检测到越狱。 此检查定期在客户端完成，无法在服务器端检查。<br>分发商可以更新策略并删除限制。 对于设备功能策略，发出包含 — devCapabilitiesV1flag且无参数的策略更新命令。 对于jailbreak强制执行setpolicy.enforceJailbreak=false。 |
| 3348 | HardStopIntervalExpired | 硬停止间隔已过期。 |
| 3349 | 服务器版本太高 | 服务器运行的版本高于客户端支持的最高版本。 |
| 3350 | ServerVersionTooLow | 服务器运行的版本低于客户端支持的最低版本。 |
| 3351 | 域令牌无效 | 域令牌无效。 要解决此问题，请再次向域注册。 |
| 3352 | DomainTokenTooOld | 域令牌早于许可证所需的令牌。 要解决此问题，请再次向域注册。 |
| 3353 | DomainTokenToNew | 域令牌比许可证所需的令牌新。 |
| 3354 | DomainTokenExpired | 域令牌已过期。 |
| 3355 | DomainjoinFailed | 域加入失败。 |
| 3356 | NoMateriableRoot | 未找到V3叶许可证的根许可证。 |
| 3357 | NoValidEmbeddedLicense | 未找到有效的嵌入式许可证。 |
| 3358 | NoACPProtectionAvailable | 无法回放，因为连接的模拟设备没有ACP保护。 |
| 3359 | NoCGSMAProtectionAvailable | 无法回放，因为连接的模拟设备没有CGMSA保护。 |
| 3360 | 需要域注册 | 内容需要域注册。 |
| 3361 | NotRegisteredToDomain | 计算机未注册到指定元数据的域。 |
| 3362 | OperationtimeoutError | 异步操作花费的时间比配置的maxOperationTimeout长。<br>**注意：** 此错误代码仅由iOS DRMNative Framework返回。 |
| 3363 | UnsupportedIOSPlaylistError | M3U8播放列表包含不支持的内容，或缺少必需的#EXT-X-FAXS-CM DRM元数据对象。<br>**注意：** 此错误代码仅由iOS DRMNative Framework返回。 |
| 3364 | NoDeviceId | 框架请求了设备ID，但返回的值为空。<br>框架请求了设备ID，但返回的值为空。<br>在Chrome浏览器设置中，用户不应选择 **允许受保护内容的标识符** 复选框。 |
| 3365 | IncognitomodeNotAllowed | 此浏览器/平台组合不允许在无痕模式下播放受DRM保护的内容。<br>分发服务器的软件应建议用户退出无痕模式或使用其他浏览器。 有关更多信息，请参阅 [DRM错误3365原因和解决方法](https://forums.adobe.com/thread/1266622). |
| 3366 | Badparameter | 主机运行时使用错误的参数调用了Primetime DRM库。 |
| 3367 | BadSignal | M3U8清单签名失败。<br>**注意：** 此错误代码仅由iOS DRMNative Framework或AVE返回。 |
| 3368 | UserSettingsNoAccess | 用户已取消该操作，或已输入不允许访问系统的设置。<br>此错误仅在SWF版本19或更高版本中引发。 为了向后兼容，对于SWF版本18或更低版本，会引发错误代码3321。<br>分发商的软件应引导用户说明如何允许无沙盒插件访问。 有关更多信息，请参阅 [Chrome中的DRM错误3322/3346/3368（信息栏问题）](https://forums.adobe.com/message/5520902). |
| 3369 | InterfaceNotAvailable | 所需的浏览器界面不可用。 此问题仅在Pepper上出现。 Flash插件与浏览器版本之间可能存在不匹配。<br>分发商的软件应指导用户确保他们安装了最新版本的浏览器。<br>如果此错误的发生次数增加，并且这些错误对应于已发布的浏览器更新，则将提升到Adobe。 |
| 3370 | ContentIdSettingsNoAccess | 用户已禁用 **允许受保护内容设置的标识符。**<br>**注意：** Pepper版本13.0.0.x或更高版本中出现此错误。<br>分发商的软件和/或操作团队应指导用户启用 **允许受保护内容的标识符** 设置。<br>有关更多信息，请参阅 [https://forums.adobe.com/message/6518323#6518323](https://forums.adobe.com/message/6518323#6518323). |
| 3371 | NoOPConstraintInPixelConstraints | 基于许可证中的输出保护约束的解析格式不正确。<br>分发服务器的软件应显示一条错误消息。 要求用户使用内容标题将问题报告给分发服务器。<br>分发服务器应使用有效策略重新打包内容。 |
| 3372 | 分辨率大于最大分辨率 | 内容的分辨率大于输出保护约束中指定的最大分辨率。<br>如果分发商的操作团队在日志中看到此错误，他们应该检查基于解析度的输出保护策略，并在必要时重新打包内容。<br>有关基于分辨率的输出保护的更多信息，请参阅关于基于分辨率的输出保护。 |
| 3373 | DisplayResolutionLargerThanConstrain | 内容分辨率大于当前活动输出保护约束指定的分辨率。<br>如果分发商的操作团队在日志中看到此错误，他们应该检查基于解析度的输出保护策略，并在必要时重新打包内容。<br>有关基于分辨率的输出保护的更多信息，请参阅关于基于分辨率的输出保护。 |
| 3374 | ClientCommProcessFailed | 在客户端通信处理（例如，请求生成、响应处理、错误的身份验证令牌等）期间失败。 |

## 3328的子错误代码映射 {#suberror-code-mapping-for-3328}

| SubError | 描述 |
|---|---|
| 100-1000 | 由Adobe许可证服务器保留 |
| 10000 - 20000 | 由Adobe的个性化服务器保留 |
| 20100-21000 | 为AdobeXbox keyserver保留。<br>此范围内的错误将映射到常规Primetime DRM服务器SDK错误消息引用，如下所示：<br>Xbox keyserver错误= DRM服务器错误+ 0x20000<br>例如，Xbox Keyserver错误20202等同于DRM服务器SDK错误202 |
| 100xxxx | 为客户端子错误代码保留 |
