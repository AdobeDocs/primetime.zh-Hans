---
seo-title: 远程和本地iOS密钥交付
title: 远程和本地iOS密钥交付
uuid: 90f672e7-9301-4e14-adca-db2a8f951a83
translation-type: tm+mt
source-git-commit: 53654b740b03c6a79394d30704a41186d4655237

---


# 远程和本地iOS密钥交付 {#remote-and-local-ios-key-delivery}

Adobe Primetime支持以下选项，用于向iOS客户端进行关键交付：

* **远程** -按照HTTP实时流(HLS)规范中的指定执行；m3U8清单指定一个HTTPS路径，该路径包含AES密钥，该密钥应用于解密流中的以下加密段。 在Primetime DRM策 `Remote` 略中指定时，客户端设备必须连接到远程HTTPS服务器才能获取AES密钥。

* **本地** -当您在 `Local` Primetime DRM中指定而不是连接到AES密钥的因特网／网络时，本地HTTPS服务器会嵌入到iOS应用程序中，然后iOS应用程序会管理所有AES密钥请求。 嵌入式HTTPS服务器在P应用程序中自动设置和配置。 应用程序开发人员无需干预。

通过用于打包内容的Primetime DRM策略启用远程密钥交付。 如果要更改此设置，则必须重新打包内容。 如果启用远程密钥交付，则必须部署能够管理来自iOS客户端的密钥请求的Primetime DRM密钥服务器。 但是，对于其他平台上的客户端，工作流没有更改。

>[!NOTE] {class=&quot;- topic/note &quot;}
>
>密钥交付选择仅影响iOS客户端。 使用HLS内容的所有其他设备(如Android和Primetime on Desktop(Flash Player))始终使用密钥交付，即使已指 `Local` 定 `Remote` 也是如此。

