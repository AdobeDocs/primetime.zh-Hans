---
title: 使用DRMStatusEvent类概述
description: 使用DRMStatusEvent类概述
copied-description: true
exl-id: 1fc2d28e-ee21-462e-8d81-2ecb5ac0d962
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '78'
ht-degree: 0%

---

# 使用DRMStatusEvent类概述 {#using-the-drmstatusevent-class-overview}

A `DRMStatusEvent` 当Primetime DRM保护的内容开始成功播放时，将调度对象。 （成功表示许可证已验证，用户已进行身份验证并有权查看内容）。

此 `DRMStatusEvent` 对象包含与许可证相关的信息，包括许可证是否可以脱机使用，或者许可证过期且内容无法再查看。
