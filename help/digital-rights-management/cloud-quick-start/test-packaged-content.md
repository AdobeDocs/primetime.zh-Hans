---
title: 测试打包的内容
description: 测试打包的内容
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '89'
ht-degree: 0%

---

# 测试打包的内容 {#test-the-packaged-content}

您应该使用公开可用的Adobe Primetime Desktop Player(通过Flash Player)验证打包操作是否成功。 此播放器仅支持HDS内容。 要测试HLS内容，需要启用了Primetime浏览器TVSDK的播放器。

1. 将您的内容托管在Web服务器上。
1. 在https://drmtest2.adobe.com:8080/AccessPlayer/player.html上启动Primetime DRM(以前称为Adobe访问)播放器。
1. 将URL粘贴到HDS清单( [!DNL .f4m])进入播放器的导航字段，然后单击 **[!UICONTROL Play]** 按钮。
