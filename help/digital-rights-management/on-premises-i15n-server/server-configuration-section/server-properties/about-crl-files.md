---
title: 关于CRL文件
description: 关于CRL文件
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '270'
ht-degree: 0%

---

# 关于CRL文件 {#about-crl-files}

为了正常运行，个性化和许可证服务器需要在运行的应用程序服务器（例如Tomcat）上缓存若干证书吊销列表(CRL)文件到磁盘。 新的CRL文件必须定期下载并缓存在磁盘上。 如果允许磁盘上的CRL文件的有效期过期，则Individualization Server将拒绝个性化客户端，而License Server将拒绝颁发许可证。

缓存到磁盘的CRL必须具有匹配相应URL的文件名。 冒号“：”和“/”斜杠等特殊字符在文件名中转换为下划线“_”。

以下是由个性化和许可证服务器使用的外部托管的CRL列表：

* **中间CRL：**

   * URL： [!DNL <ht<span></span>tps://crl2.adobe.com/Adobe/FlashAccessIntermediateCA.crl>]
   * 文件： [!DNL http___crl2.adobe.com_Adobe_FlashAccessIntermediateCA.crl]
   * 有效期：在创建后约12个月内有效

* **根CRL：**

   * URL： [!DNL <ht<span></span>tps://crl2.adobe.com/Adobe/FlashAccessRootCA.crl>]
   * 文件： [!DNL http___crl2.adobe.com_Adobe_FlashAccessRootCA.crl]
   * 有效性：从创建起约5年有效

* **最新CRL：**

   * URL： [!DNL <ht<span></span>tps://crl3.adobe.com/AdobeSystemsIncorporatedFlashAccessRuntime/LatestCRL.crl>]
   * 文件： [!DNL http___crl3.adobe.com_AdobeSystemsIncorporatedFlashAccessRuntime_LatestCRL.crl]
   * 有效性：从创建起约3个月有效

要了解许可证服务器可以使用的外部托管CRL，请与Adobe支持部门联系。

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

除了外部托管的CRL之外，您还可以创建和维护其他CRL。 这是个性化CA CRL，如 [创建个性化CA CRL](../../../on-premises-i15n-server/server-configuration-section/server-properties/create-i15n-ca-crl.md) 章节。

CRL计划在过期前45天更新。 这样您就有充足的时间从Internet获取并安装新生成的CRL。 在CRL文件过期之前，您必须注意对其进行更新。
