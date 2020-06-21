---
description: 'null'
seo-description: 'null'
seo-title: 限制访问受保护内容的DRM客户端的块列表
title: 限制访问受保护内容的DRM客户端的块列表
uuid: 38bc024e-0c5b-4c1c-8d4b-94b9e0fec67e
translation-type: tm+mt
source-git-commit: 9d2e046ae259c05fb4c278f464c9a26795e554fc
workflow-type: tm+mt
source-wordcount: '405'
ht-degree: 0%

---


# 限制访问受保护内容的DRM客户端的块列表 {#blocklist-of-drm-clients-restricted-from-accessing-protected-content}

此块列表指定无法访问受保护内容的Primetime DRM客户端。 您可以按客户端版本和平台阻止列表客户端。

示例用例： 在发生安全违规事件，可将Primetime DRM客户端的较新版本指定为获取许可证和内容回放所需的最低版本。 许可证服务器在颁发许可证之前检查发出许可证请求的Primetime DRM客户端是否满足版本要求。 Primetime DRM客户端还在播放内容之前检查许可证中的版本。 如果许可证可能转移到另一台计算机的域，则需要进行此客户端检查。

Primetime DRM客户端版本可由下表中指定的属性标识：

| **属性** | **支持的值** | **匹配条件** | **说明** |
|---|---|---|---|
| 环境 | `“PC”, “PortingKit”` | 精确匹配 | 标识客户端是在桌面上还是任何其他设备上运行。 |
| 操作系统 | `“Win”, “Mac”, “Linux”, “Android”, “iOS”, "ChromeOS"` | 精确匹配 | Platform |
| 架构 | `“32”, “64”` | 精确匹配 | 32位或64位 |
| 屏幕类型 | `“PC”, “Mobile”, “TV”` | 精确匹配 |  |
| 运行时版本 | 有效版本号。 例如， `“2.0.0”, "3.0", "4.0", "11.0"`等等。 | 如果客户端版本小于或等于指定的版本，则匹配。 | 版本号指定为数字和句点(“”)的组合。 任意长度的。 |
| Primetime DRM库版本 | 有效版本号。 例如， `“2.0.0”`。 | 如果客户端版本小于或等于指定的版本，则匹配。 | 版本号指定为数字和句点(“”)的组合。 任意长度的。 |
| OEM供应商 | 可位于向将Primetime DRM移植到设备的客户颁发的运行时证书中的OEM供应商字符串。 | 精确匹配 | 使用移植工具包的设备的OEM供应商标识字符串。 |
| 模型 | 可位于向将Primetime DRM移植到设备的客户颁发的运行时证书中的模型字符串。 例如，`"iOS_Mobile", "Android_Mobile", "Chrome", "ChromeOS_ARM", "WindowsOnARM", "AVE"` | 精确匹配 | 使用移植工具包的设备的设备模型标识字符串。 |

>[!NOTE] {class=&quot;-主题／注释&quot;
>
>在块列表中指定条目时，可以为上表中提及的一个或多个属性设置值。 未指定的任何属性均视为通配符。 如果Primetime DRM客户端与块列表条目中指定的所有值匹配，则该客户端可能无法访问受保护的内容。

