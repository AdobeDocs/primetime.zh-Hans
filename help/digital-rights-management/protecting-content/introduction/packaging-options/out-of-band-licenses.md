---
seo-title: 带外许可证
title: 带外许可证
uuid: 43397ce5-6c52-429d-b7fa-fa8c91cf9742
translation-type: tm+mt
source-git-commit: c78d3c87848943a0be3433b2b6a543822a7e1c15

---


# 带外许可证 {#out-of-band-licenses}

使用Primetime DRM，您可以实现一个工作流，在该工作流中，客户端可以在带外获得预生成的许可证，因此无需部署许可证服务器。 要支持此工作流，应在打包时指定一个选项，指示没有可用的许可证服务器。 这防止了客户端尝试从许可证服务器请求此内容的许可证。

指示许可证服务器不可用的内容只能在Primetime DRM客户端版本3.0或更高版本上播放。 旧客户端需要升级才能播放此内容。
