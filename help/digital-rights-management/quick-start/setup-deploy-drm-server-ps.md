---
title: 设置和部署用于受保护流处理的服务器
description: 设置和部署用于受保护流处理的服务器
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '172'
ht-degree: 0%

---

# 设置和部署用于受保护流处理的服务器 {#set-up-and-deploy-the-server-for-protected-streaming}

1. 在Primetime DRM DVD上设置配置文件夹：

   `\Adobe Access Server for Protected Streaming\configs\`
1. 复制示例 `configs` 文件夹到您的 `<Tomcat_installation_dir>` 并将复制的文件夹重命名为 `licenseserver`.

   configs文件夹的路径现在应为 `<Tomcat_install_dir>\licenseserver\`.
1. 运行 `Scrambler.bat` 在Primetime DRM中获取传输和许可证服务器PFX文件的加密密码 `<DVD>` `\Adobe Access Server for Protected Streaming\` 目录：

   * `Scrambler.bat <Adobe-provided transport credential password>`
   * `Scrambler.bat <Adobe-provided license server credential password>`

1. 将PFX文件复制到 `<TomcatInstallDir>\licenseserver\flashaccessserver\tenants\<tenant-name>\` 目录。
1. 在中编辑相应的租户配置 `<TomcatInstallDir>\licenseserver\flashaccessserver\tenants\sampletenant\flashaccess-tenant.xml`，具有以下设置：

   ```
   Configuration|Tenant|Credentials|TransportCredential|File|path=<filename-transport-credential-PFX> 
   Configuration|Tenant|Credentials|TransportCredential|File|password=<scrambled-transportcredential-password> 
   Configuration|Tenant|Credentials|LicenseServerCredential|File|path=<fielname-license-servercredential-PFX> 
   Configuration|Tenant|Credentials|LicenseServerCredential|File|password=<scrambled-license-servercredential-password>
   ```

1. 运行 `Validator.bat` 用于验证配置的实用程序有效：

   ```
   Validator.bat -g -r <absolute-path-to TomcatInstallDir\licenseserver>
   ```

1. 复制 `flashaccessserver.war` 文件从CD到 `<TomcatInstallDir>\webapps\` 目录。
1. 如果Tomcat正在运行，请按停止正在运行的Tomcat实例 `<CTRL-C>` （如果是从命令窗口启动的）。 如果Tomcat是作为Windows服务安装的，您还可以从Windows服务应用程序中停止服务器。
1. 要启动Tomcat，请输入以下命令：

   ```
   <TomcatInstallDir>\bin\catalina run
   ```

1. 要验证设置，请在浏览器中输入以下URL：

   ```
    https://<LicenseServer>:8080/flashaccessserver/flashaccess/license/v2
   ```
