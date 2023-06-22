---
title: 使用DRMStatusEvent类概述
description: 使用DRMStatusEvent类概述
copied-description: true
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '74'
ht-degree: 0%

---


# 概述 {#using-the-drmstatusevent-class-overview}

A `DRMStatusEvent` 当Primetime DRM保护的内容开始成功播放时，将调度对象。 （成功表示许可证已验证，用户已进行身份验证并有权查看内容）。

此 `DRMStatusEvent` 对象包含与许可证相关的信息，包括许可证是否可以脱机使用，或者许可证过期且内容无法再查看。
