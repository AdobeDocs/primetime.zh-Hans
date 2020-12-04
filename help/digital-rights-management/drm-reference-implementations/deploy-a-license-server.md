---
description: 'null'
seo-description: 'null'
seo-title: 部署许可证服务器
title: 部署许可证服务器
uuid: bee7ead1-ed13-4894-80f9-5196bf2f818f
translation-type: tm+mt
source-git-commit: 5df9a8b98baaf1cd1803581d2b60c7ed4261a0e8
workflow-type: tm+mt
source-wordcount: '294'
ht-degree: 0%

---


# 部署许可证服务器{#deploy-the-license-server}

1. 将参考实现war文件复制到Tomcat服务器上的`webapps`目录。

   要按原样使用引用实施许可证服务器，您只需将许可证服务器WAR文件(`[DRM SDK DVD]\Reference Implementation\Server\Reference Implementation Server\\flashaccess.war`)复制到Tomcat服务器上的`webapps`目录。

   如果要自定义引用实施许可证服务器，请将您从`DRM SDK DVD]\Reference Implementation\Server\Reference Implementation Server\refimpl-build\wars`构建的服务器war文件复制到`webapps`目录。

   >[!NOTE]
   >
   >如果以前部署了许可证服务器WAR文件，则可能需要删除Tomcat服务器[!DNL webapps]目录中未打包的WAR目录：
   >
   >* [!DNL webapps/flashaccess]
   >* [!DNL webapps/edcws]


   >[!NOTE]
   >
   >除非您需要与Flash媒体Rights Management(FMRMS)v1.5内容向后兼容，否则不要部署[!DNL edsws.war]。 （这是非常罕见的要求。）
   >
   >如果您希望阻止Tomcat解包WAR文件，请编辑`conf`目录中的`server.xml`，并将`unpackWARs`设置为`false`。

1. 将`[DRM SDK DVD]\Reference Implementation\Server\Reference Implementation Server\resources\`目录的整个内容复制到[!DNL tomcat]目录中。

   [!DNL resources]目录包括：

   * [!DNL flashaccesstools.properties] -许可证服务器属性文件。
   * [!DNL log4j.xml] -许可证服务器日志记录配置
   * [!DNL *.pol] - DRM策略文件示例。

   此外，您还可以选择将Adobe认证文件复制到此位置。

1. 修改[!DNL flashaccesstools.properties]中的许可证服务器设置以反映您的服务器设置。

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

1. 编辑Tomcat `conf`目录中的`catalina.properties`文件；将[!DNL resources]目录的位置（或存储属性文件和其他资源文件的备用位置）添加到`shared.loader`属性中。

   例如，如果`flashaccess-refimpl.properties`位于[!DNL [Tomcat home]\resources\]中：

   ```
   shared.loader=..\resources
   ```

   这会将`flashaccess-refimpl.properties`放在类路径上。
1. 确保您的其他资源文件（[!DNL log4j.xml]、策略文件、证书）位于[!DNL resources]目录中，或位于类路径中，或位于其在[!DNL flashaccess-refimpl.properties]中指定的位置。

   您最初可能希望在调试模式下运行`log4j`。 在[!DNL log4j.xml]中，将`debug`设置为true:

   ```
   <log4j:configuration xmlns:log4j="https://jakarta.apache.org/log4j/"<b>debug="true"</b>>
   ...
   ```

1. 从Tomcat [!DNL bin]目录中开始服务器。

   在Linux上：

   ```
   catalina.sh start
   ```

   在Windows上：

   ```
   catalina.bat start
   ```
