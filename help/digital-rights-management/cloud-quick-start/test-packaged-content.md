---
seo-title: 测试打包内容
title: 测试打包内容
uuid: 99df417a-85ce-45da-bfcf-33df2197bf5b
translation-type: tm+mt
source-git-commit: b7f52b71bde1d7bf59ef51d4f6f90dfaa07e347b
workflow-type: tm+mt
source-wordcount: '89'
ht-degree: 0%

---


# 测试打包内容{#test-the-packaged-content}

您应通过使用公开可用的Adobe Primetime桌面播放器(通过Flash Player)验证打包操作是否成功。 此播放器只能支持HDS内容。 为了测试HLS内容，需要支持Primetime浏览器TVSDK的播放器。

1. 将内容托管在Web服务器上。
1. 启动Primetime DRM(以前称为Adobe访问)播放器，网址为https://drmtest2.adobe.com:8080/AccessPlayer/player.html。
1. 将URL粘贴到HDS清单([!DNL .f4m])到播放器的导航字段中，然后单击&#x200B;**[!UICONTROL Play]**&#x200B;按钮。
