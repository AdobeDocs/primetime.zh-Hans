---
title: 命令行用法
description: 命令行用法
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
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

* `signaturefile` 指定位于AIR应用程序中的signatures.xml文件的路径 [!DNL META-INF] 目录

* `signingcert` 指定用于签署AIR应用程序的证书

>[!NOTE]
>
>要确定iOS应用程序的发布者ID，请使用 `-s` 选项并指定用于对iOS应用程序进行签名的证书。 ***需要Adobe Primetime才能构建可播放受访问保护内容的iOS应用程序***.
