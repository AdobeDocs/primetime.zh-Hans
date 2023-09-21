---
title: 使用DRMStatusEvent类概述
description: 使用DRMStatusEvent类概述
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '78'
ht-degree: 0%

---

# 使用DRMStatusEvent类概述 {#using-the-drmstatusevent-class-overview}

A `DRMStatusEvent` 当Primetime DRM保护的内容开始成功播放时，将调度对象。 （成功意味着验证许可证，并且用户经过身份验证并有权查看内容）。

此 `DRMStatusEvent` 对象包含与许可证相关的信息，包括许可证是否可以离线使用，或者许可证过期且内容无法再查看。
