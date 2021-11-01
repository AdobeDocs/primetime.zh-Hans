---
title: 关于CRL文件
description: 关于CRL文件
copied-description: true
exl-id: 126a323d-9433-4a1e-a617-2d3bbf717cce
source-git-commit: 6a00df9c061da43f6efa49d927873db629568597
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# 关于CRL文件 {#about-crl-files}

为了正常运行，个性化和许可证服务器需要将多个证书撤销列表(CRL)文件缓存到运行的应用程序服务器（例如Tomcat）上的磁盘中。 必须定期在磁盘上下载和缓存新的CRL文件。 如果允许磁盘上CRL文件的有效期失效，则个性化服务器将拒绝个性化客户端，许可证服务器将拒绝颁发许可证。

缓存到磁盘的CRL必须具有与相应URL匹配的文件名。 在文件名中，冒号“：”和“/”等特殊字符将转换为下划线“_”。

以下是个性化和许可证服务器所使用的外部托管CRL列表：

* **中间CRL:**

   * URL: [!DNL <ht<span></span>tps://crl2.adobe.com/Adobe/FlashAccessIntermediateCA.crl>]
   * 文件： [!DNL http___crl2.adobe.com_Adobe_FlashAccessIntermediateCA.crl]
   * 有效期：自创建以来大约12个月

* **根CRL:**

   * URL: [!DNL <ht<span></span>tps://crl2.adobe.com/Adobe/FlashAccessRootCA.crl>]
   * 文件： [!DNL http___crl2.adobe.com_Adobe_FlashAccessRootCA.crl]
   * 有效期：自创建后大约5年

* **最新CRL:**

   * URL: [!DNL <ht<span></span>tps://crl3.adobe.com/AdobeSystemsIncorporatedFlashAccessRuntime/LatestCRL.crl>]
   * 文件： [!DNL http___crl3.adobe.com_AdobeSystemsIncorporatedFlashAccessRuntime_LatestCRL.crl]
   * 有效期：自创建后大约3个月有效

要了解许可证服务器可以使用的外部托管CRL，请联系Adobe支持。

<!---

Commenting out because of a security vulnerability reported in Jira PSIRT-20689. 

The following are externally hosted CRLs that are used only by the License Servers:

* URL: `https://crl2.adobe.com/Adobe/FlashAccessIndividualizationCA.crl`

* File: `http___crl2.adobe.com_Adobe_FlashAccessIndividualizationCA.crl`

* Validity: Good for approximately 3 months from creation

* URL: `https://individualization-crl.primetime.adobe.com/FlashAccessIndividualizationCA.crl`

* File: `http___individualization-crl.primetime.adobe.com_FlashAccessIndividualizationCA.crl`

* Validity: Good for approximately 3 months from creation

* URL: `https://individualization-crl.s3-website-us-east-1.amazonaws.com/FlashAccessIndividualizationCA.crl`

* File: `http___individualization-crl.s3-website-us-east-1.amazonaws.com_FlashAccessIndividualizationCA.crl`

* Validity: Good for approximately 3 months from creation

--->

除了外部托管的CRL之外，您还可以创建和维护附加的CRL。 这是个性化CA CRL，在 [创建个性化CA CRL](../../../on-premises-i15n-server/server-configuration-section/server-properties/create-i15n-ca-crl.md) 文档的部分。

CRL计划在过期前45天进行更新。 这样，您就有足够的时间从Internet获取和安装新生成的CRL。 您必须在CRL文件过期之前对其进行更新。
