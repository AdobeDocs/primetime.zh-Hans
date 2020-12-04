---
seo-title: UltraViolet媒体和Adobe PrimetimeDRM
title: UltraViolet媒体和Adobe PrimetimeDRM
uuid: 7076c0f9-e092-48e4-9118-8a414bd03c7a
translation-type: tm+mt
source-git-commit: 635e2893439c5459907c54d2c3bd86f58da0eec5
workflow-type: tm+mt
source-wordcount: '478'
ht-degree: 0%

---


# UltraViolet媒体和Adobe PrimetimeDRM {#ultraviolet-media-and-adobe-primetime-drm}

Adobe PrimetimeDRM可以与其他第三方内容流解决方案一起使用，以建立一个完整且安全的基于DRM的媒体分发生态系统。

UltraVoilet([https://www.myuv.com/](https://www.uvvu.com/))是一种数字版权认证和基于云的分发系统，它使数字家庭娱乐内容的消费者能够通过多个平台和设备来流和下载购买的内容。 UltraViolet内容将使用通用加密(CENC)以通用文件格式(CFF)下载（或流式传输）。

可以轻松地与Adobe PrimetimeDRM一起建立紫外线系统。 以下用例描述了内容流行为：

<!--<a id="fig_cxy_dc2_44"></a>-->

![](assets/AdobeUV_web.png)

1. 内容所有者将内容编码并打包为CFF。 打包内容授权给零售商进行分发。
1. 零售商将内容上传到数字服务提供商，如CDN。 内容现在可供下载。 请注意，这些角色中的某些角色可由一个或多个公司扮演。

   最终用户有支持Adobe AIR的设备。 除此之外，用户还需要安装符合UltraViolet规范的应用程序。 应用程序包含解析CFF并呈现给运行时使用的必要代码。 所有敏感加密操作都在安全运行时中处理。
1. 应用程序可以触发设备的域连接，该连接与协调器交互。 协调员维护一个权限柜、一个用户数据库和域。 协调人的域管理器使用Primetime DRM SDK构建，以实施特定于Primetime DRM的域加入／离开操作。
1. 然后，用户可以使用应用程序选择他们希望从零售商处获得的视频。 该零售商通常提供一个Web门户并处理所有业务逻辑。
1. 然后，零售商与协调员交互以添加权限令牌。 然后，零售商会将请求重定向到服务提供商，以便进行实际内容下载。
1. 如果设备尚未获得内容的许可证，它将使用CFF触发许可证请求。 该请求通常包括域证书、用户凭据和有关该应用程序的信息。 该服务提供商运行一个Primetime DRM许可证服务器（使用Primetime DRM SDK），它遵循UltraViolet规范。
1. 服务提供商的UltraVoilet业务逻辑会根据需要与协调者交互，以检索适当的权利令牌以确定是否应颁发内容许可证。

   内容许可证绑定到域。 客户端应用程序可以将许可证插入CFF文件。 内容现在可在应用程序中回放，运行时的Primetime DRM组件将处理所有保护和使用规则实施。
1. 同一最终用户拥有的其他设备和应用程序可以向协调器进行注册。 现在，无需任何外部交易即可在其他Primetime DRM设备中加载内容。