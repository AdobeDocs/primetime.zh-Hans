---
description: 使用Adobe Primetime DRM SDK时，必须创建License Server。 当使用Primetime DRM保护内容时，只有在许可证服务器向消费者颁发许可证后才能查看内容。 如果使用基于身份的许可，则基于密码的身份验证可确保只有经过授权的用户才能打开和查看内容。
title: 实施许可证服务器
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '159'
ht-degree: 0%

---


# 实施许可证服务器{#implement-a-license-server}

使用Adobe Primetime DRM SDK时，必须创建License Server。 当使用Primetime DRM保护内容时，只有在许可证服务器向消费者颁发许可证后才能查看内容。 如果使用基于身份的许可，则基于密码的身份验证可确保只有经过授权的用户才能打开和查看内容。

实施License Server时，必须从Adobe获取必要的数字证书。 有关请求证书的详细说明，请参阅Primetime DRM证书注册文档。

要了解有关实施License Server和获取数字证书的更多信息，请参阅*使用Adobe Primetime DRM SDK保护内容。*
