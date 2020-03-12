---
description: 本节介绍不同版本的Flash Player和TVSDK提供的功能。
seo-description: 本节介绍不同版本的Flash Player和TVSDK提供的功能。
seo-title: RBOP客户端支持
title: RBOP客户端支持
uuid: d1d0f788-7bc1-488c-807e-be47f83725e9
translation-type: tm+mt
source-git-commit: e60d285b9e30cdd19728e3029ecda995cd100ac9

---


# RBOP客户端支持 {#rbop-client-support}

本节介绍不同版本的Flash Player和TVSDK提供的功能。

**错误调度** -当正在播放的内容的分辨率超过在DRM策略中定义的设备配置允许的分辨率时，下面列出的TVSDK平台将调度DRM运行时错误：

* Flash Player版本18至20
* Android —— 版本
* iOS —— 版本

>[!NOTE]
>
>* 所有Flash和移动平台都支持错误调度，但只有上面列出的TVSDK客户端会处理与RBOP相关的错误。
>* 与RBOP相关的 [DRM客户端错误](https://help.adobe.com/en_US/primetime/drm/index.html#reference-DRM_Client_Error_Messages):>
   >    * **3371** —— 基于许可证中的输出保护限制的错误分辨率。
   >    * **3372** —— 内容的分辨率大于在输出保护约束中指定的最大分辨率。 （如果有人尝试注入用于其他设备的内容，则可能会发生这种情况。）
   >    * **3373** —— 内容的分辨率大于当前活动的输出保护约束所指定的分辨率。 （这意味着我们必须降级。）
>



**自动缩减** -用于缩减的技术因平台和Flash Player版本而异：

* Flash Player版本21:支持RBOP（自动缩减）（智能比特率切换）
* Windows上的Firefox版本38及更高版本（带有Access CDM）:Adobe会自动将较高比特率的流降级到较低比特率的流（而不是下载较低等级的流）。

>[!NOTE]
>
>这些平台会自动缩小视频，并以低于或等于DRM策略指定分辨率的分辨率显示内容。 利用此功能，只要有满足DRM策略限制的可用流，内容将始终回放到客户端。

**旧版输出保护** -使用版本18之前的Flash Player的客户端只能处理旧版OP限制。 使用Flash Player版本18及更高版本的客户端可以处理旧版或RBOP限制。 如果要设置RBOP限制，则还应为较旧的客户端设置旧版OP限制。 对于支持RBOP的客户，RBOP限制比旧版OP限制要大。
