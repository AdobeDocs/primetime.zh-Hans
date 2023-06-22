---
title: 使用Java准备密码
description: 使用Java准备密码
copied-description: true
exl-id: 69d551c4-e13b-473a-86ed-36b5ba24f6b8
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '22'
ht-degree: 0%

---

# 使用Java准备密码{#prepare-passwords-using-java}

运行 `ScrambleUtil.class` 使用Java：

1. 导航到 `[DRM SDK DVD]\Reference Implementation\Server\Reference Implementation Server\refimpl/scrambler/ refimpl/scrambler/`
1. 在命令行中，键入：

   ```
   java -classpath [DRM SDK DVD]/SDK/adobe-flashaccess-sdk.jar;  
       com.adobe.flashaccess.refimpl.util.ScrambleUtil your_pfx_password
   ```
