---
title: 概述
description: 概述
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '203'
ht-degree: 0%

---


# AIR Publisher ID实用程序{#air-publisher-id-utility}

在构建AIR文件时，AIR开发人员工具(ADT)会自动生成一个发布者ID。 AIR Publisher ID实用程序([!DNL AdobePublisherIDUtility.jar])计算AIR应用程序的Publisher ID。

发布者ID对于用于构建AIR文件的证书是唯一的。 如果对多个AIR应用程序重复使用同一证书，则所有AIR应用程序都具有相同的发布者ID。 成功发行版1.5.2的AIR发行版不会将生成的发布者ID添加到文件。 因此，如果您计划使用AIR应用程序允许列表，请使用此工具确定发布者ID。

>[!NOTE]
>
>用于AIR允许列表实施的发布者ID与应用程序发布者在应用程序的[!DNL application.xml]文件中指定的发布者ID不同。

## AIR Publisher ID实用程序命令行用法{#air-publisher-id-utility-command-line-usage}

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

* 
   * `signaturefile`*指定AIR应用程序文件的路径，该 [!DNL signatures.xml] 文件位于应用程序目 [!DNL META-INF] 录中

* `signingcert` 指定用于对AIR应用程序进行签名的证书

>[!NOTE]
>
>要确定Android应用程序的发布者ID，您需要使用`-s`选项指定用于对Android应用程序包(APK)进行签名的证书。 Primetime DRM是构建可播放受DRM保护的内容的Android应用程序所必需的。