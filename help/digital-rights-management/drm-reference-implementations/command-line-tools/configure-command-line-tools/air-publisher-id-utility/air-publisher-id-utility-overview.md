---
title: 概述
description: 概述
copied-description: true
exl-id: 07f2ef0b-c6aa-4574-a3ae-18685a090cf2
source-git-commit: a1fc67b708f3d5821532d3827639adbadf15f6b4
workflow-type: tm+mt
source-wordcount: '203'
ht-degree: 0%

---

# AIR发布者ID实用程序 {#air-publisher-id-utility}

构建AIR文件时，AIR开发人员工具(ADT)会自动生成发布者ID。 AIR Publisher ID实用程序( [!DNL AdobePublisherIDUtility.jar])将计算AIR应用程序的发布者ID。

发布者ID对于用于构建AIR文件的证书是唯一的。 如果您为多个AIR应用程序重复使用同一证书，则所有AIR应用程序都具有相同的发布者ID。 成功于1.5.2版的AIR版本不会将生成的发布者ID添加到文件中。 因此，如果您计划使用AIR应用程序允许列表，请使用此工具确定发布者ID。

>[!NOTE]
>
>用于AIR允许列表实施的发布者ID与应用程序发布者在应用程序的 [!DNL application.xml] 文件。

## AIR Publisher ID实用程序命令行用法 {#air-publisher-id-utility-command-line-usage}

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

* `signaturefile` 指定AIR应用程序的路径 [!DNL signatures.xml] 文件，位于应用程序中 [!DNL META-INF] 目录

* `signingcert` 指定用于对AIR应用程序进行签名的证书

>[!NOTE]
>
>要确定Android应用程序的发布者ID，您需要使用 `-s` 选项，以指定用于对Android应用程序包(APK)进行签名的证书。 构建可播放受Primetime DRM保护的内容的Android应用程序时，需要使用Primetime DRM。
