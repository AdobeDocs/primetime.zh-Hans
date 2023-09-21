---
description: 此部分介绍不同版本的Flash Player和TVSDK中可用的功能。
title: RBOP客户端支持
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '338'
ht-degree: 0%

---

# RBOP客户端支持 {#rbop-client-support}

此部分介绍不同版本的Flash Player和TVSDK中可用的功能。

**错误分派**  — 当正在播放的内容分辨率超出DRM策略中定义的设备配置允许的分辨率时，下面列出的TVSDK平台会发送DRM运行时错误：

* Flash Player版本18到20
* Android — 版本
* iOS — 版本

>[!NOTE]
>
>* 所有Flash和移动平台都支持错误调度，但只有上面列出的TVSDK客户端会处理与RBOP相关的错误。
>* RBOP相关 [DRM客户端错误](https://help.adobe.com/en_US/primetime/drm/index.html#reference-DRM_Client_Error_Messages)：
>    * **3371**  — 基于许可证中的输出保护约束的解析格式不正确。
>    * **3372**  — 内容分辨率大于输出保护约束中指定的最大分辨率。 （如果有人尝试插入适用于其他设备的内容，则可能会发生这种情况。）
>    * **3373**  — 内容分辨率大于当前活动输出保护约束指定的分辨率。 （这意味着我们将不得不降级。 ）
>

**自动缩放**  — 用于缩减的技术因平台和Flash Player版本而异：

* Flash Player版本21：支持带有自动缩减缩放（智能比特率切换）的RBOP
* Windows上的Firefox版本38及更高版本（使用Access CDM）：Adobe会自动将较高比特率的流降级为较低比特率的流（与下载较低比特率的流相反）。

>[!NOTE]
>
>这些平台会自动缩小视频并以低于或等于DRM策略指定的分辨率显示内容。 使用此功能，只要有符合DRM策略限制的可用流，内容将始终回放给客户端。

**旧版输出保护**  — 使用版本18之前的Flash Player的客户端只能处理旧版OP限制。 具有Flash Player版本18及更高版本的客户端可以处理旧版或RBOP限制。 如果您正在设置RBOP限制，则还应该为旧版客户端设置旧版OP限制。 对于支持RBOP的客户，RBOP限制优先于旧版OP限制。
