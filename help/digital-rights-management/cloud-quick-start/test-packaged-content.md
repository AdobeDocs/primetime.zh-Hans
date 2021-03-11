---
title: 测试打包内容
description: 测试打包内容
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '89'
ht-degree: 0%

---


# 测试打包内容{#test-the-packaged-content}

您应通过使用公开可用的Adobe Primetime Desktop Player(通过Flash Player)验证打包操作是否成功。 此播放器只能支持HDS内容。 为了测试HLS内容，需要启用Primetime Browser TVSDK的播放器。

1. 将内容托管在Web服务器上。
1. 启动Primetime DRM(以前称为Adobe访问)播放器，网址为https://drmtest2.adobe.com:8080/AccessPlayer/player.html。
1. 将URL粘贴到HDS清单([!DNL .f4m])到播放器的导航字段中，然后单击&#x200B;**[!UICONTROL Play]**&#x200B;按钮。
