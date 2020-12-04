---
description: 'null'
seo-description: 'null'
seo-title: 使用Ant准备密码
title: 使用Ant准备密码
uuid: 9419ab0d-b448-4881-9d26-35c00f0b13bc
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '42'
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

