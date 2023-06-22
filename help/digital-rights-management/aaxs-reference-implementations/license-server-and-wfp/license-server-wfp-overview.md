---
title: 许可证服务器和观察文件夹打包程序概述
description: 许可证服务器和观察文件夹打包程序概述
copied-description: true
exl-id: 1a355068-7ad6-4cc2-8447-49251dae3ff8
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '454'
ht-degree: 0%

---

# 许可证服务器和观察文件夹打包程序概述 {#license-server-and-watched-folder-packager-overview}

reference implementation server可以帮助您使用Adobe访问SDK创建许可证服务器。 在此实现中，基于数据库中的用户条目对用户进行身份验证。 服务器包括用于颁发许可证的演示业务逻辑。 它还实现了对Flash媒体Rights Management服务器1.0和1.5的兼容性支持。

参考实施服务器还包括打包程序的观察文件夹实施。 此组件可以与许可证服务器一起部署，也可以部署在单独的计算机上。 通过此打包程序实施，可以创建多个Watched文件夹。 将内容放入watched文件夹后，打包程序会自动打包内容。

许可证服务器和打包程序部署为单独的WAR文件，因此您可以选择是在单独的服务器上运行它们，还是在单个Apache Tomcat®实例中运行。 许可证服务器位于 [!DNL flashaccess.war] 打包员在里面 [!DNL flashaccess-packager.war]. 可选 [!DNL edcws.war] 包含对来自FMRMS 1.x客户端的许可证请求的支持。

参考实施示例代码演示了以下功能：

* 许可证服务器：

   * 处理身份验证请求，使用数据库验证用户名/密码
   * 处理许可证请求并确定使用许可证链接时要颁发的许可证类型。
   * 为包含多个策略的内容颁发许可证
   * 颁发支持将远程密钥交付到iOS客户端的许可证(需要Adobe Primetime)
   * 颁发需要外部查找/检索内容加密密钥(CEK)的许可证
   * 使用数据库确定用户是否有权查看内容
   * 使用策略更新列表
   * 使用计算机吊销列表
   * 使用HSM或PKCS12文件存储凭据
   * 加密属性文件中指定的密码
   * 指定多个许可证服务器或传输凭据（续订凭据后，旧凭据将保留在服务器上，以便无需重新打包即可使用现有内容）
   * 限制允许向许可证服务器发出请求的DRM/运行时版本
   * 设置客户端时钟回溯首选项
   * 限制请求时间和服务器时间之间允许的时间差（以防止重放攻击）
   * 处理来自FMRMS 1.x客户端的请求(触发FMRMS 1.x客户端升级到AdobeAccess 2.0或更高版本)
   * 使用存储在数据库中的FMRMS 1.x许可证信息，快速将FMRMS 1.x元数据转换为Adobe访问元数据
   * 用于将FMRMS 1.x策略转换为Adobe访问策略的示例代码
   * 用于从现有数据库导入FMRMS 1.x许可证信息的示例脚本
   * 获取服务器版本
   * 域注册
   * 域取消注册
   * 同步请求
   * 许可证退回

* Packager服务器：

   * 实施自动打包添加到watched文件夹中的内容的打包程序实施
   * 使用HSM或PKCS12文件存储凭据
   * 加密属性文件中指定的密码
   * 使用AIR应用程序配置打包程序、创建策略和创建策略更新列表
