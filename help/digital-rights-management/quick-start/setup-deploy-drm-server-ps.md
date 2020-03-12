---
seo-title: 为受保护的流设置和部署服务器
title: 为受保护的流设置和部署服务器
uuid: 300a1b63-0bf0-48a8-977d-212563025c19
translation-type: tm+mt
source-git-commit: e60d285b9e30cdd19728e3029ecda995cd100ac9

---


# 为受保护的流设置和部署服务器 {#set-up-and-deploy-the-server-for-protected-streaming}

1. 在Primetime DRM DVD上设置配置文件夹：

   `\Adobe Access Server for Protected Streaming\configs\`
1. 将示例文件 `configs` 夹复制到您的文 `<Tomcat_installation_dir>` 件夹，并将复制的文件夹重命名为 `licenseserver`。

   configs文件夹的路径现在应为 `<Tomcat_install_dir>\licenseserver\`。
1. 运行 `Scrambler.bat` 以获取Primetime DRM目录中传输和许可证服务器PFX文件的加密密 `<DVD>``\Adobe Access Server for Protected Streaming\` 码：

   * `Scrambler.bat <Adobe-provided transport credential password>`
   * `Scrambler.bat <Adobe-provided license server credential password>`

1. 将PFX文件复制到目 `<TomcatInstallDir>\licenseserver\flashaccessserver\tenants\<tenant-name>\` 录。
1. 使用以下设置在中编 `<TomcatInstallDir>\licenseserver\flashaccessserver\tenants\sampletenant\flashaccess-tenant.xml`辑相应的租户配置：

   ```
   Configuration|Tenant|Credentials|TransportCredential|File|path=<filename-transport-credential-PFX> 
   Configuration|Tenant|Credentials|TransportCredential|File|password=<scrambled-transportcredential-password> 
   Configuration|Tenant|Credentials|LicenseServerCredential|File|path=<fielname-license-servercredential-PFX> 
   Configuration|Tenant|Credentials|LicenseServerCredential|File|password=<scrambled-license-servercredential-password>
   ```

1. 运行实 `Validator.bat` 用程序验证配置是否有效：

   ```
   Validator.bat -g -r <absolute-path-to TomcatInstallDir\licenseserver>
   ```

1. 将文 `flashaccessserver.war` 件从CD复制到目 `<TomcatInstallDir>\webapps\` 录。
1. 如果Tomcat正在运行，请在命令窗口中按 `<CTRL-C>` 下（如果是从命令窗口启动的）以停止正在运行的Tomcat实例。 如果Tomcat是作为Windows服务安装的，则还可以从Windows Services应用程序停止服务器。
1. 要启动Tomcat，请输入以下命令：

   ```
   <TomcatInstallDir>\bin\catalina run
   ```

1. 要验证设置，请在浏览器中输入以下URL:

   ```
    https://<LicenseServer>:8080/flashaccessserver/flashaccess/license/v2
   ```
