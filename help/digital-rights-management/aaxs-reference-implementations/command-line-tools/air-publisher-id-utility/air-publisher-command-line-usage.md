---
title: 命令行用法
description: 命令行用法
copied-description: true
exl-id: 67056085-beb5-4f54-8962-369bc32d7907
source-git-commit: 79cab347d0daa01549fbf8a9b37bf0a91c14648e
workflow-type: tm+mt
source-wordcount: '75'
ht-degree: 0%

---

# 命令行用法 {#command-line-usage}

要运行该工具，请使用以下语法：

```
java -jar AdobePublisherIDUtility.jar 
<i class="+ topic ph hi-d="" i "="">
 <i class="+ topic ph hi-d="" i "="">
  signaturefile 
  java -jar AdobePublisherIDUtility.jar -s 
  <i class="+ topic ph hi-d="" i "="">
    signingcert
  </i class="+ topic>
 </i class="+ topic>
</i class="+ topic>
```

* `signaturefile` 指定位于应用程序中的AIR应用程序signatures.xml文件的路径 [!DNL META-INF] 目录

* `signingcert` 指定用于对AIR应用程序进行签名的证书

>[!NOTE]
>
>要确定iOS应用程序的发布者ID，请使用 `-s` 选项，并指定用于对iOS应用程序进行签名的证书。 ***Adobe Primetime需要构建可播放受访问保护内容的iOS应用程序***.
