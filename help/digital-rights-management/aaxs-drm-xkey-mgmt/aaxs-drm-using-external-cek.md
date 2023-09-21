---
description: 使用外部CEK功能可使用现有CKMS来购买和打包许可证。
title: 使用外部CEK购买和打包许可证
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '227'
ht-degree: 0%

---

# 使用外部CEK购买和打包许可证{#using-external-cek-to-vend-and-package-licenses}

使用外部CEK功能可使用现有CKMS来购买和打包许可证。

## EncryptContentWithExternalKey.java

这是一个命令行工具，将对视频进行AAXS加密并创建元数据，以 *非* 包含CEK（受AAXS许可证服务器的公共证书保护）。 相反，该工具会将CEK ID嵌入到视频的元数据中。

在许可证获取期间，AAXS许可证服务器会观察元数据中的标记，该标记标识此内容已使用外部CEK进行了保护。 许可证服务器将从元数据中提取CEK ID，然后查询安全存储库/CKMS以检索相应的CEK。

## 打包工作流程

1. 确保您使用的是Java 1.6.0_24或更高版本。
1. 要查看工具用法，请执行以下操作： `java -jar AdobePackager_ExternalCEK.jar`
1. 要打包内容，请执行以下操作：

   ```
   java -jar AdobePackager_ExternalCEK.jar sample.flv encrypted.flv abc abcdef0123456789 
       policy.pol https://path-to-your-server:8090 <license-server-public-cert.pem> 
       <license-server-private-key.pfx> <private-key-password>
   ```

>[!NOTE]
>
>* 可以使用包含的ANT构建Java源代码 `build-samples.xml`
>* FLASH ACCESSSDK ( `adobe-flashaccess-sdk.jar`)必须在类路径上
>

## 服务器工作流

1. 设置参考实施。
1. 如果存在，请清理以前的参考实施部署：

   1. `delete <tomcat>\work\Catalina\*.*`
   1. `delete <tomcat>\conf\Catalina\*.*`
   1. `delete <tomcat>\logs\*.*`

1. 验证是否存在 [!DNL CEKDepot.properties] 文件与 [!DNL flashaccess-refimpl.properties]

1. 从Adobe Primetime Player启动许可证请求
1. 观察参考实施日志，了解类似于以下内容的情况：

   ```
   DEBUG [com.adobe.flashaccess.refimpl.web.RefImplLicenseReqHandler.REQUESTS] 
     Used CEK ID:{abc} to retrieve CEK: {abcdef0123456789} from depot
   ```

   1. 您可能需要更改 [!DNL log4j.xml] 要登录的设置 `DEBUG` 级别( `INFO` 默认设置)

## 已知问题

无
