---
title: 许可证服务器和观察文件夹打包程序概述
description: 许可证服务器和观察文件夹打包程序概述
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '454'
ht-degree: 0%

---

# 许可证服务器和观察文件夹打包程序概述 {#license-server-and-watched-folder-packager-overview}

reference implementation server可以帮助您使用Adobe访问SDK创建许可证服务器。 在此实现中，基于数据库中的用户条目对用户进行身份验证。 服务器包括用于颁发许可证的演示业务逻辑。 它还对Flash MediaRights Management服务器1.0和1.5实现了兼容性支持。

该参考实现服务器还包括该打包程序的观察文件夹实现。 此组件可以与许可证服务器一起部署或在单独的计算机上部署。 通过此打包程序实施，可以创建多个watched文件夹。 当内容放入watched文件夹时，打包程序会自动打包内容。

许可证服务器和打包程序将部署为单独的WAR文件，因此您可以选择是在单独的服务器上运行它们，还是在单个Apache Tomcat®实例中运行。 许可证服务器位于 [!DNL flashaccess.war] 包装工在 [!DNL flashaccess-packager.war]. 可选 [!DNL edcws.war] 包含对来自FMRMS 1.x客户端的许可证请求的支持。

参考实施示例代码演示了以下功能：

* 许可证服务器：

   * 处理身份验证请求，使用数据库验证用户名/密码
   * 处理许可证请求并确定使用许可证链接时要颁发的许可证类型。
   * 为包含多个策略的内容颁发许可证
   * 颁发支持将远程密钥交付到iOS客户端的许可证(需要Adobe Primetime)
   * 签发需要外部查找/检索内容加密密钥(CEK)的许可证
   * 使用数据库确定用户是否有权查看内容
   * 使用策略更新列表
   * 使用计算机吊销列表
   * 使用HSM或PKCS12文件存储凭据
   * 加密属性文件中指定的密码
   * 指定多个许可证服务器或传输凭据（续订凭据后，旧凭据将保留在服务器上，因此无需重新打包即可使用现有内容）
   * 限制允许向许可证服务器发出请求的DRM/运行时版本
   * 设置客户端时钟回溯首选项
   * 限制请求时间和服务器时间之间允许的时间差（以防止重放攻击）
   * 处理来自FMRMS 1.x客户端的请求(触发FMRMS 1.x客户端升级到AdobeAccess 2.0或更高版本)
   * 使用存储在数据库中的FMRMS 1.x许可证信息，快速将FMRMS 1.x元数据转换为Adobe访问元数据
   * 用于将FMRMS 1.x策略转换为Adobe访问策略的示例代码
   * 用于从现有数据库导入FMRMS 1.x许可证信息的示例脚本
   * 获取服务器版本
   * 域注册
   * 域注销
   * 同步请求
   * 许可证退回

* Packager服务器：

   * 实施自动打包添加到观察文件夹的内容的打包程序实施
   * 使用HSM或PKCS12文件存储凭据
   * 加密属性文件中指定的密码
   * 使用AIR应用程序配置打包程序、创建策略和创建策略更新列表
