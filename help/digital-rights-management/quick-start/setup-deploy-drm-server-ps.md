---
seo-title: 为受保护的流设置和部署服务器
title: 为受保护的流设置和部署服务器
uuid: 300a1b63-0bf0-48a8-977d-212563025c19
translation-type: tm+mt
source-git-commit: e60d285b9e30cdd19728e3029ecda995cd100ac9
workflow-type: tm+mt
source-wordcount: '172'
ht-degree: 0%

---


# 为受保护的流{#set-up-and-deploy-the-server-for-protected-streaming}设置和部署服务器

1. 在Primetime DRM DVD上设置配置文件夹：

   `\Adobe Access Server for Protected Streaming\configs\`
1. 将示例`configs`文件夹复制到`<Tomcat_installation_dir>`，并将复制的文件夹重命名为`licenseserver`。

   配置文件夹的路径现在应为`<Tomcat_install_dir>\licenseserver\`。
1. 运行`Scrambler.bat`以获取Primetime DRM `<DVD>` `\Adobe Access Server for Protected Streaming\`目录中传输和许可证服务器PFX文件的加密密码：

   * `Scrambler.bat <Adobe-provided transport credential password>`
   * `Scrambler.bat <Adobe-provided license server credential password>`

1. 将PFX文件复制到`<TomcatInstallDir>\licenseserver\flashaccessserver\tenants\<tenant-name>\`目录。
1. 使用以下设置编辑`<TomcatInstallDir>\licenseserver\flashaccessserver\tenants\sampletenant\flashaccess-tenant.xml`中的相应租户配置：

   ```
   Configuration|Tenant|Credentials|TransportCredential|File|path=<filename-transport-credential-PFX> 
   Configuration|Tenant|Credentials|TransportCredential|File|password=<scrambled-transportcredential-password> 
   Configuration|Tenant|Credentials|LicenseServerCredential|File|path=<fielname-license-servercredential-PFX> 
   Configuration|Tenant|Credentials|LicenseServerCredential|File|password=<scrambled-license-servercredential-password>
   ```

1. 运行`Validator.bat`实用程序以验证配置是否有效：

   ```
   Validator.bat -g -r <absolute-path-to TomcatInstallDir\licenseserver>
   ```

1. 将`flashaccessserver.war`文件从CD复制到`<TomcatInstallDir>\webapps\`目录。
1. 如果Tomcat正在运行，请通过在命令窗口中按`<CTRL-C>`来停止正在运行的Tomcat实例（如果它是从命令窗口启动的）。 如果Tomcat是作为Windows服务安装的，您还可以从Windows Services应用程序停止服务器。
1. 要开始Tomcat，请输入以下命令：

   ```
   <TomcatInstallDir>\bin\catalina run
   ```

1. 要验证设置，请在浏览器中输入以下URL:

   ```
    https://<LicenseServer>:8080/flashaccessserver/flashaccess/license/v2
   ```
