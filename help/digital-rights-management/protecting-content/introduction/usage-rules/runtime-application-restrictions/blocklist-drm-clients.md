---
title: DRM客户端阻止列表受限制无法访问受保护的内容
description: DRM客户端阻止列表受限制无法访问受保护的内容
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '400'
ht-degree: 0%

---

# DRM客户端阻止列表受限制无法访问受保护的内容 {#blocklist-of-drm-clients-restricted-from-accessing-protected-content}

此阻止列表指定无法访问受保护内容的Primetime DRM客户端。 您可以按客户端版本和平台阻止列表客户端。

示例用例：在出现安全违规时，可以将Primetime DRM客户端的较新版本指定为许可证获取和内容播放所需的最低版本。 许可证服务器在颁发许可证之前检查发出许可证请求的Primetime DRM客户端是否满足版本要求。 Primetime DRM客户端还会在播放内容之前检查许可证中的版本。 如果域可能会将许可证转移到另一台计算机，则需要此客户端检查。

Primetime DRM客户端版本可由下表指定的属性标识：

| **属性** | **支持的值** | **匹配条件** | **描述** |
|---|---|---|---|
| 环境 | `“PC”, “PortingKit”` | 完全匹配 | 标识客户端是否正在桌面或任何其他设备上运行。 |
| 操作系统 | `“Win”, “Mac”, “Linux”, “Android”, “iOS”, "ChromeOS"` | 完全匹配 | 平台 |
| 架构 | `“32”, “64”` | 完全匹配 | 32位或64位 |
| 屏幕类型 | `“PC”, “Mobile”, “TV”` | 完全匹配 | |
| 运行时版本 | 有效的版本号。 例如， `“2.0.0”, "3.0", "4.0", "11.0"`，等等。 | 如果客户端版本小于或等于指定的版本，则匹配。 | 版本号由数字和句点(“。”)组合指定 任何长度。 |
| Primetime DRM库版本 | 有效的版本号。 例如， `“2.0.0”`. | 如果客户端版本小于或等于指定的版本，则匹配。 | 版本号由数字和句点(“。”)组合指定 任何长度。 |
| OEM供应商 | OEM供应商字符串，该字符串可以位于颁发给将Primetime DRM移植到设备的客户的Runtime证书中。 | 完全匹配 | 使用移植工具包的设备的OEM供应商标识字符串。 |
| 模型 | 可在运行时证书中找到的模型字符串，该证书已颁发给将Primetime DRM移植到设备的客户。 例如， `"iOS_Mobile", "Android_Mobile", "Chrome", "ChromeOS_ARM", "WindowsOnARM", "AVE"` | 完全匹配 | 使用移植套件的设备的设备型号标识字符串。 |

>[!NOTE]
>
>在阻止列表中指定条目时，可以为上一个表中提到的一个或多个属性设置值。 任何未指定的属性都会被视为通配符。 如果Primetime DRM客户端与阻止列表条目中指定的所有值相匹配，则该客户端可能无法访问受保护的内容。
