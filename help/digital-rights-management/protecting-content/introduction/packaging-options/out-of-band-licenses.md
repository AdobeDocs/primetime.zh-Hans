---
title: 带外许可证
description: 带外许可证
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '96'
ht-degree: 0%

---

# 带外许可证 {#out-of-band-licenses}

使用Primetime DRM，您可以实施一个工作流程，其中客户端在带外获取预生成的许可证，因此无需部署许可证服务器。 要支持此工作流，应在打包时指定指示没有许可证服务器可用的选项。 这会阻止客户端尝试从许可证服务器为此内容请求许可证。

指示许可证服务器不可用的内容只能在Primetime DRM客户端版本3.0或更高版本上播放。 旧版客户端需要升级才能播放此内容。
