---
title: 部署许可证服务器
description: 部署许可证服务器
copied-description: true
exl-id: 1439a5b2-eccb-41b7-a4d3-0673e727fb13
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '292'
ht-degree: 0%

---

# 部署许可证服务器{#deploy-the-license-server}

1. 将您的参考实施war文件复制到 `webapps` 目录。

   要按原样使用参考实施许可证服务器，您只需复制许可证服务器WAR文件( `[DRM SDK DVD]\Reference Implementation\Server\Reference Implementation Server\\flashaccess.war`)到 `webapps` 目录。

   如果要自定义参考实施许可证服务器，请复制您从中构建的服务器war文件 `DRM SDK DVD]\Reference Implementation\Server\Reference Implementation Server\refimpl-build\wars` 到 `webapps` 目录。

   >[!NOTE]
   >
   >如果您之前部署了许可证服务器WAR文件，则可能需要删除 [!DNL webapps] 目录：
   >
   >* [!DNL webapps/flashaccess]
   >* [!DNL webapps/edcws]


   >[!NOTE]
   >
   >不部署 [!DNL edsws.war] 除非您需要与Flash媒体Rights Management(FMRMS) v1.5内容向后兼容。 （这是非常罕见的要求。）
   >
   >如果您希望阻止Tomcat解压缩WAR文件，请编辑 `server.xml` 在 `conf` 目录和集 `unpackWARs` 到 `false`.

1. 复制 `[DRM SDK DVD]\Reference Implementation\Server\Reference Implementation Server\resources\` 目录到 [!DNL tomcat] 目录。

   此 [!DNL resources] 目录包括：

   * [!DNL flashaccesstools.properties]  — 许可证服务器属性文件。
   * [!DNL log4j.xml]  — 许可证服务器日志记录配置
   * [!DNL *.pol]  — 示例DRM策略文件。

   此外，您还可以选择将Adobe认证文件复制到此位置。

1. 修改中的许可证服务器设置 [!DNL flashaccesstools.properties] 以反映服务器设置。

   至少应设置以下属性的值：

   * `config.resourcesDirectory`
   * `HandlerConfiguration.ServerTransportCredential`
   * `HandlerConfiguration.ServerTransportCredential.password`
   * `LicenseHandler.ServerCredential`
   * `LicenseHandler.ServerCredential.password`
   * `MetaDataConverter.SignatureParameters.ServerCredential`
   * `MetaDataConverter.SignatureParameters.ServerCredential.password`
   * `V2KeyParameters.LicenseServerUrl`
   * `V2KeyParameters.KeyOptions.AsymmetricKeyOptions.Certificate`
   * V2KeyParameters.LicenseServerTransportCertificate

1. 编辑 `catalina.properties` 文件（在Tomcat中） `conf` 目录；添加您的位置 [!DNL resources] 目录（或存储属性文件和其他资源文件的替代位置）到 `shared.loader` 属性。

   例如，如果您拥有 `flashaccess-refimpl.properties` 位于[！DNL [Tomcat主页]\resources\]：

   ```
   shared.loader=..\resources
   ```

   此位置 `flashaccess-refimpl.properties` 在类路径上。
1. 确保其他资源文件( [!DNL log4j.xml]，策略文件、认证)位于 [!DNL resources] 目录或其他位置，以及它们在 [!DNL flashaccess-refimpl.properties].

   您可能希望首先运行 `log4j` 处于调试模式。 In [!DNL log4j.xml]，设置 `debug` 为true：

   ```
   <log4j:configuration xmlns:log4j="https://jakarta.apache.org/log4j/"<b>debug="true"</b>>
   ...
   ```

1. 从Tomcat [!DNL bin] 目录，启动服务器。

   在Linux上：

   ```
   catalina.sh start
   ```

   在Windows上：

   ```
   catalina.bat start
   ```
