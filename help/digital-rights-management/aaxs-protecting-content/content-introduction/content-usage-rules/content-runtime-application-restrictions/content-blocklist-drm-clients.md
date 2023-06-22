---
title: DRM客户端访问受保护内容时受限制的阻止列表
description: DRM客户端访问受保护内容时受限制的阻止列表
copied-description: true
exl-id: 74ddb5ed-4e68-4570-9cd5-bfc699609972
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '377'
ht-degree: 0%

---

# DRM客户端访问受保护内容时受限制的阻止列表 {#blocklist-of-drm-clients-restricted-from-accessing-protected-content}

**Adobe访问DRM模块版本访问受保护内容时受到限制。**

指定无法访问内容的DRM客户端。 由DRM客户端版本和平台指定。

示例用例：在出现安全违规时，可以将DRM客户端的较新版本指定为许可证获取和内容播放所需的最低版本。 许可证服务器在发出许可证之前检查发出许可证请求的DRM客户端是否满足版本要求。 在播放内容之前，DRM客户端还检查许可证中的DRM版本。 如果域中的许可证可能传输到另一台计算机，则需要此客户端检查。

DRM客户机版本可由下表指定的属性标识：

| **属性** | **支持的值** | **匹配条件** | **描述** |
|---|---|---|---|
| 环境 | “PC”、“PortingKit” | 完全匹配 | 标识客户端是在桌面还是任何其他设备上运行。 |
| 操作系统 | &quot;Win&quot;、&quot;Mac&quot;、&quot;Linux&quot;、&quot;Android&quot;、&quot;iOS&quot;、&quot;ChromeOS&quot; | 完全匹配 | Platform |
| 架构 | “32”, “64” | 完全匹配 | 32位或64位 |
| 屏幕类型 | “PC”、“移动”、“电视” | 完全匹配 |  |
| 运行时版本 | 有效的版本号。 例如，“2.0.0”、“3.0”、“4.0”、“11.0”等。 | 如果客户端版本小于或等于指定的版本，则匹配。 | 版本号由数字和句点(“。”)组合指定 任意长度。 |
| DRM库版本 | 有效的版本号。 例如，“2.0.0”。 | 如果客户端版本小于或等于指定的版本，则匹配。 | 版本号由数字和句点(“。”)组合指定 任意长度。 |
| OEM供应商 | OEM供应商字符串 | 完全匹配 | 使用移植工具包的设备的OEM供应商标识字符串。 |
| 模型 | 模型字符串。 例如，“iOS_Mobile”、“Android_Mobile”、“Chrome”、“ChromeOS_ARM”、“WindowsOnARM”、“AVE” | 完全匹配 | 使用移植套件的设备的设备型号标识字符串。 |

>[!NOTE]
>
>在阻止列表中指定条目时，可以为上一个表中提到的一个或多个属性设置值。 任何未指定属性都会被视为通配符。 如果DRM客户端与阻止列表条目中指定的所有值相匹配，则该客户端可能无法访问受保护的内容。
