---
title: 使用DRMStatusEvent类概述
description: 使用DRMStatusEvent类概述
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '78'
ht-degree: 0%

---


# 使用DRMStatusEvent类概述{#using-the-drmstatusevent-class-overview}

当Primetime DRM保护的内容开始成功播放时，将调度`DRMStatusEvent`对象。 (成功意味着许可证已经过验证，用户已通过身份验证并获得视图内容的授权)。

`DRMStatusEvent`对象包含与许可证相关的信息，包括许可证是否可以脱机使用或许可证过期以及内容无法再查看。
