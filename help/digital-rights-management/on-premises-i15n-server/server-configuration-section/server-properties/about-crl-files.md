---
title: 关于CRL文件
description: 关于CRL文件
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '305'
ht-degree: 0%

---


# 关于CRL文件{#about-crl-files}

为了正常运行，个性化和许可证服务器需要将多个证书吊销列表(CRL)文件缓存到正在运行的应用程序服务器上的磁盘（例如，Tomcat）。 必须定期在磁盘上下载和缓存新的CRL文件。 如果允许在磁盘上失效CRL文件的有效期，个性化服务器将拒绝对客户端进行个性化，而许可证服务器将拒绝颁发许可证。

缓存到磁盘的CRL必须具有与相应URL匹配的文件名。 在文件名中，冒号“：”和“/”斜杠等特殊字符将转换为下划线“_”。

以下是个性化和许可证服务器使用的外部托管CRL列表:

* **中间CRL:**

   * URL:[!DNL <ht<span></span>tps://crl2.adobe.com/Adobe/FlashAccessIntermediateCA.crl>]
   * 文件：[!DNL http___crl2.adobe.com_Adobe_FlashAccessIntermediateCA.crl]
   * 有效性：从创建到大约12个月

* **根CRL:**

   * URL:[!DNL <ht<span></span>tps://crl2.adobe.com/Adobe/FlashAccessRootCA.crl>]
   * 文件：[!DNL http___crl2.adobe.com_Adobe_FlashAccessRootCA.crl]
   * 有效性：在创建后约5年内有效

* **最新CRL:**

   * URL:[!DNL <ht<span></span>tps://crl3.adobe.com/AdobeSystemsIncorporatedFlashAccessRuntime/LatestCRL.crl>]
   * 文件：[!DNL http___crl3.adobe.com_AdobeSystemsIncorporatedFlashAccessRuntime_LatestCRL.crl]
   * 有效性：从创建到大约3个月

以下是仅由许可证服务器使用的外部托管CRL:

* URL:[!DNL <ht<span></span>tps://crl2.adobe.com/Adobe/FlashAccessIndividualizationCA.crl>]
* 文件：[!DNL http___crl2.adobe.com_Adobe_FlashAccessIndividualizationCA.crl]
* 有效性：从创建到大约3个月

* URL:[!DNL <ht<span></span>tps://individualization-crl.primetime.adobe.com/FlashAccessIndividualizationCA.crl>]
* 文件：[!DNL http___individualization-crl.primetime.adobe.com_FlashAccessIndividualizationCA.crl]
* 有效性：从创建到大约3个月

* URL:[!DNL <ht<span></span>tps://individualization-crl.s3-website-us-east-1.amazonaws.com/FlashAccessIndividualizationCA.crl]>
* 文件：[!DNL http___individualization-crl.s3-website-us-east-1.amazonaws.com_FlashAccessIndividualizationCA.crl]
* 有效性：从创建到大约3个月

除了上述CRL之外，您还必须创建并维护附加CRL。 这是个性化CA CRL，如本文档的[创建个性化CA CRL](../../../on-premises-i15n-server/server-configuration-section/server-properties/create-i15n-ca-crl.md)部分中所指定。

CRL计划在过期前45天进行更新。 这应允许您有足够的时间从Internet获取和安装新生成的CRL。 在CRL文件过期之前，您必须小心更新它们。
