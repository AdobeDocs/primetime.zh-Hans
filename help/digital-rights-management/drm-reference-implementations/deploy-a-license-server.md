---
description: 'null'
seo-description: 'null'
seo-title: 部署许可证服务器
title: 部署许可证服务器
uuid: bee7ead1-ed13-4894-80f9-5196bf2f818f
translation-type: tm+mt
source-git-commit: 29149594c4b41956a091ef27093304e74ff15f2f

---


# 部署许可证服务器{#deploy-the-license-server}

1. 将您的参考实现war文件复制到Tomcat服 `webapps` 务器上的目录中。

   要按原样使用参考实施许可证服务器，您只需将许可证服务器WAR文件( `[DRM SDK DVD]\Reference Implementation\Server\Reference Implementation Server\\flashaccess.war`)复制到Tomcat服 `webapps` 务器上的目录中。

   如果要自定义参考实施许可证服务器，请将您从中构建的服务器war文件复制 `DRM SDK DVD]\Reference Implementation\Server\Reference Implementation Server\refimpl-build\wars` 到目录 `webapps` 中。

   >[!NOTE]
   >
   >如果您之前部署了许可证服务器WAR文件，则可能需要删除Tomcat服务器上目录中 [!DNL webapps] 未打包的WAR目录：       >
   >
   >* [!DNL webapps/flashaccess]
   >* [!DNL webapps/edcws]


   >[!NOTE]
   >
   >除非您需 [!DNL edsws.war] 要与Flash Media Rights Management(FMRMS)v1.5内容向后兼容，否则不要部署。 （这是非常罕见的要求。）
   >
   >如果您希望阻止Tomcat解包WAR文件，请在目 `server.xml` 录中编 `conf` 辑并设置 `unpackWARs` 为 `false`。

1. 将目录的整个内 `[DRM SDK DVD]\Reference Implementation\Server\Reference Implementation Server\resources\` 容复制到您的目 [!DNL tomcat] 录中。

   该 [!DNL resources] 目录包括：

   * [!DNL flashaccesstools.properties] -许可证服务器属性文件。
   * [!DNL log4j.xml] -许可证服务器日志记录配置
   * [!DNL *.pol] -示例DRM策略文件。
   此外，您还可以选择将Adobe认证文件复制到此位置。

1. 在中修改许可证服务器设 [!DNL flashaccesstools.properties] 置，以反映您的服务器设置。

   至少为以下属性设置值：

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

1. 编辑Tomcat `catalina.properties` 目录中的文 `conf` 件；将目录的位 [!DNL resources] 置（或存储属性文件和其他资源文件的替代位置）添加到属 `shared.loader` 性。

   例如，如果您位于[! `flashaccess-refimpl.properties` DNL [Tomcat home]\resources\]:

   ```
   shared.loader=..\resources
   ```

   它将放 `flashaccess-refimpl.properties` 在类路径上。
1. 确保您的其他资源文件( [!DNL log4j.xml]策略文件、证书)位于目录中，或位于类路径中， [!DNL resources] 或位于其中指定的位置 [!DNL flashaccess-refimpl.properties]。

   您最初可能希望在调试模 `log4j` 式下运行。 在 [!DNL log4j.xml]中，设 `debug` 置为true:

   ```
   <log4j:configuration xmlns:log4j="https://jakarta.apache.org/log4j/"<b>debug="true"</b>>
   ...
   ```

1. 从Tomcat目 [!DNL bin] 录启动服务器。

   在Linux上：

   ```
   catalina.sh start
   ```

   在Windows上：

   ```
   catalina.bat start
   ```
