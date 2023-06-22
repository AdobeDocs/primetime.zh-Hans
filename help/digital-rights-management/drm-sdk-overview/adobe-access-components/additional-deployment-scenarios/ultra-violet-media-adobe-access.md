---
title: UltraViolet介质和Adobe Primetime DRM
description: UltraViolet介质和Adobe Primetime DRM
copied-description: true
exl-id: 03b01a29-e8e0-4fb5-a685-63a745a6417c
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '478'
ht-degree: 0%

---

# UltraViolet介质和Adobe Primetime DRM {#ultraviolet-media-and-adobe-primetime-drm}

Adobe Primetime DRM可以与其他第三方内容流解决方案一起使用，以建立一个完整且安全的基于DRM的媒体分发生态系统。

紫罗兰( [https://www.myuv.com/](https://www.uvvu.com/))是一个数字版权身份验证和基于云的分发系统，它允许数字家庭娱乐内容的消费者通过多个平台和设备流式传输和下载购买的内容。 UltraViolet内容将使用通用加密(CENC)以通用文件格式(CFF)下载（或流式传输）。

与Adobe Primetime DRM一起建立紫外系统很容易。 以下用例描述了内容流行为：

<!--<a id="fig_cxy_dc2_44"></a>-->

![](assets/AdobeUV_web.png)

1. 内容所有者对CFF中的内容进行编码和打包。 已将打包内容许可给零售商进行分发。
1. 零售商将内容上传到数字服务提供商，如CDN。 该内容现已可供下载。 请注意，其中某些角色可以由一家或多家公司担任。

   最终用户拥有支持Adobe AIR的设备。 除此之外，用户还需要安装与UltraViewer兼容的应用程序。 该应用程序包含解析CFF并显示以供运行时使用的必要代码。 所有敏感加密操作都在安全运行时进行处理。
1. 应用程序可以触发设备的域加入，该设备与协调器交互。 协调者维护一个权限存储器、一个用户数据库和域。 使用Primetime DRM SDK构建协调器的域管理器，以实施特定于Primetime DRM的域加入/离开操作。
1. 然后，用户可以使用应用程序选择要从零售商处获取的视频。 零售商通常会提供一个Web门户并处理所有业务逻辑。
1. 然后，零售商与协调者交互以添加权限令牌。 然后，零售商将请求重定向到服务提供商，以便实际下载内容。
1. 如果设备尚未获得内容的许可证，它将使用CFF触发许可证请求。 该请求通常包括域证书、用户凭据以及有关应用程序的信息。 服务提供商运行遵循UltraViolet规范的Primetime DRM许可证服务器（使用Primetime DRM SDK开发）。
1. 服务提供商的UltraViolet业务逻辑根据需要与协调器交互，以检索适当的权限令牌来确定是否应颁发内容许可证。

   内容许可证已绑定到域。 客户端应用程序可以将许可证插入CFF文件。 内容现在可以在应用程序中回放，所有保护和使用规则执行都由Primetime DRM组件在运行时处理。
1. 同一最终用户拥有的其他设备和应用程序可以向协调者注册。 内容现在可以加载到其他Primetime DRM设备中，而无需任何外部事务。
