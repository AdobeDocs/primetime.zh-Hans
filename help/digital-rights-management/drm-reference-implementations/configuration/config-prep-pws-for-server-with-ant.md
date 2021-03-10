---
title: 使用Ant准备密码
description: 使用Ant准备密码
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '40'
ht-degree: 0%

---


# 使用Ant{#prepare-passwords-using-ant}准备口令

使用Ant加密密码：

1. 导航到`[DRM SDK DVD]\Reference Implementation\Server\Reference Implementation Server\refimpl/`
1. 在[!DNL build-refimpl.xml]中设置`sdkdir`属性，以指向包含Primetime DRM Java SDK的目录。
1. 运行以下命令：

   ```
   ant -f build-refimpl.xml
   ```

