---
title: 命令行使用
description: 命令行使用
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '75'
ht-degree: 0%

---


# 命令行使用{#command-line-usage}

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

* `signaturefile` 指定位于应用程序目录中的AIR应用程序的signatures.xml文件的路 [!DNL META-INF] 径

* `signingcert` 指定用于对AIR应用程序进行签名的证书

>[!NOTE]
>
>要确定iOS应用程序的发布者ID，请使用`-s`选项并指定用于对iOS应用程序进行签名的证书。 ***Adobe Primetime是构建可播放受访问保护的内容的iOS应用程序所必需的***。

