---
title: 使用Ant准备口令
description: 使用Ant准备口令
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '40'
ht-degree: 0%

---

# 使用Ant准备口令{#prepare-passwords-using-ant}

使用Ant加密您的密码：

1. 导航到 `[DRM SDK DVD]\Reference Implementation\Server\Reference Implementation Server\refimpl/`
1. 设置 `sdkdir` 中的属性 [!DNL build-refimpl.xml] 指向包含Primetime DRM Java SDK的目录。
1. 运行以下命令：

   ```
   ant -f build-refimpl.xml
   ```
