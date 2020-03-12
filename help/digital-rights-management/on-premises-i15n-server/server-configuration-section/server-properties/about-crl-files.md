---
seo-title: 关于CRL文件
title: 关于CRL文件
uuid: 672c3ca0-5c5d-4ec7-83b1-f0f8e34c8d09
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# 关于CRL文件 {#about-crl-files}

为了正常运行，个性化和许可证服务器需要将多个证书撤销列表(CRL)文件缓存到正在运行的应用程序服务器（例如Tomcat）上的磁盘中。 必须定期在磁盘上下载和缓存新的CRL文件。 如果允许在磁盘上失效CRL文件的有效期，个性化服务器将拒绝对客户端进行个性化，许可证服务器将拒绝颁发许可证。

缓存到磁盘的CRL必须具有与相应URL匹配的文件名。 在文件名中，冒号“:”和“/”等特殊字符将转换为下划线“_”。

以下是个性化和许可证服务器使用的外部托管CRL列表：

* **中级CRL:**

   * URL: [!DNL <ht<span></span>tps://crl2.adobe.com/Adobe/FlashAccessIntermediateCA.crl>]
   * 文件： [!DNL http___crl2.adobe.com_Adobe_FlashAccessIntermediateCA.crl]
   * 有效性：从创建到创建大约12个月

* **根CRL:**

   * URL: [!DNL <ht<span></span>tps://crl2.adobe.com/Adobe/FlashAccessRootCA.crl>]
   * 文件： [!DNL http___crl2.adobe.com_Adobe_FlashAccessRootCA.crl]
   * 有效性：从创建开始大约5年

* **最新CRL:**

   * URL: [!DNL <ht<span></span>tps://crl3.adobe.com/AdobeSystemsIncorporatedFlashAccessRuntime/LatestCRL.crl>]
   * 文件： [!DNL http___crl3.adobe.com_AdobeSystemsIncorporatedFlashAccessRuntime_LatestCRL.crl]
   * 有效性：从创建到创建大约3个月

以下是仅由许可证服务器使用的外部托管CRL:

* URL: [!DNL <ht<span></span>tps://crl2.adobe.com/Adobe/FlashAccessIndividualizationCA.crl>]
* 文件： [!DNL http___crl2.adobe.com_Adobe_FlashAccessIndividualizationCA.crl]
* 有效性：从创建到创建大约3个月

* URL: [!DNL <ht<span></span>tps://individualization-crl.primetime.adobe.com/FlashAccessIndividualizationCA.crl>]
* 文件： [!DNL http___individualization-crl.primetime.adobe.com_FlashAccessIndividualizationCA.crl]
* 有效性：从创建到创建大约3个月

* URL: [!DNL <ht<span></span>tps://individualization-crl.s3-website-us-east-1.amazonaws.com/FlashAccessIndividualizationCA.crl]>
* 文件： [!DNL http___individualization-crl.s3-website-us-east-1.amazonaws.com_FlashAccessIndividualizationCA.crl]
* 有效性：从创建到创建大约3个月

除了上述CRL之外，您还必须创建并维护额外的CRL。 这是个性化CA CRL，如本文档的“创建个性化 [CA CRL](../../../on-premises-i15n-server/server-configuration-section/server-properties/create-i15n-ca-crl.md) ”部分中所述。

CRL计划在过期前45天进行更新。 这样，您就有足够的时间从Internet获取和安装新生成的CRL。 在CRL文件过期之前，您必须小心更新这些文件。
