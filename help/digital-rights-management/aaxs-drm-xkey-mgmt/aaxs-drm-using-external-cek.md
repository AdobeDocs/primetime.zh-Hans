---
description: 使用外部CEK功能，使用您现有的CKMS进行许可证的打包和打包。
seo-description: 使用外部CEK功能，使用您现有的CKMS进行许可证的打包和打包。
seo-title: 使用外部CEK购买和打包许可证
title: 使用外部CEK购买和打包许可证
uuid: 1bfd8c6c-4ae9-47de-8247-085b5360127d
translation-type: tm+mt
source-git-commit: fe9493d610bc6fb97d30351c707b73cda92c67a0
workflow-type: tm+mt
source-wordcount: '249'
ht-degree: 0%

---


# 使用外部CEK进行销售和打包许可{#using-external-cek-to-vend-and-package-licenses}

使用外部CEK功能，使用您现有的CKMS进行许可证的打包和打包。

## EncryptContentWithExternalKey.java

这是一个命令行工具，它将AAXS加密视频并创建元数据，该元数据将&#x200B;*不*&#x200B;包含CEK（受AAXS许可证服务器的公共证书保护）。 相反，该工具会将CEK ID嵌入到视频的元数据中。

在获取许可证期间，AAXS许可证服务器在元数据中观察一个标志，该标志标识此内容是使用外部CEK保护的。 许可证服务器将从元数据中提取CEK ID，然后查询安全存储库/CKMS以检索相应的CEK。

## 打包工作流

1. 确保您使用的是Java 1.6.0_24或更高版本。
1. 要查看工具用法：`java -jar AdobePackager_ExternalCEK.jar`
1. 要打包内容，请执行以下操作：

   ```
   java -jar AdobePackager_ExternalCEK.jar sample.flv encrypted.flv abc abcdef0123456789 
       policy.pol https://path-to-your-server:8090 <license-server-public-cert.pem> 
       <license-server-private-key.pfx> <private-key-password>
   ```

>[!NOTE]
>
>* Java源代码可以使用包含的ANT `build-samples.xml`
>* Flash AccessSDK(`adobe-flashaccess-sdk.jar`)必须位于类路径中

>



## 服务器工作流

1. 设置引用实施。
1. 如果存在，请清除以前的参考实施部署：

   1. `delete <tomcat>\work\Catalina\*.*`
   1. `delete <tomcat>\conf\Catalina\*.*`
   1. `delete <tomcat>\logs\*.*`

1. 验证在[!DNL flashaccess-refimpl.properties]旁边是否有一个[!DNL CEKDepot.properties]文件

1. 从Adobe Primetime播放器发起许可证请求
1. 观察Ref Impl日志中类似于：

   ```
   DEBUG [com.adobe.flashaccess.refimpl.web.RefImplLicenseReqHandler.REQUESTS] 
     Used CEK ID:{abc} to retrieve CEK: {abcdef0123456789} from depot
   ```

   1. 您可能必须更改[!DNL log4j.xml]设置才能以`DEBUG`级别登录（默认情况下，`INFO`设置为）

## 已知问题

无
