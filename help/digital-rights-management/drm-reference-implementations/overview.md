---
description: 'null'
seo-description: 'null'
seo-title: 关于引用实现
title: 关于引用实现
uuid: f08fdb4b-aaa8-4871-bb62-1a21d5abdd8d
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '565'
ht-degree: 0%

---


# 关于引用实现{#about-the-reference-implementations}

本指南描述Adobe PrimetimeDRM参考实现的安装、配置和操作。

>[!NOTE]
>
>Primetime DRM以前称为Adobe访问，在此之前称为Flash Access。

Primetime DRM参考实施包括以下组件：

* **命令行工具** -这些工具基于Primetime DRM许可证服务器中使用的相同Primetime DRM SDK代码。您可以从命令行执行打包、许可和其他DRM任务，并在使用命令行工具和许可证服务器之间无缝切换。
* **许可证服务器** -一种功能齐全、可自定义的许可证服务器（下面将其描述为您的许可证服务器选项之一）。

**许可证服务器选项：**

* **Primetime DRM参考实现** -本指南的主题，此参考实现包含一个强大的DRM许可证服务器，它展示Primetime DRM SDK提供的所有功能。此实现附带源代码和构建代码的说明。 此实现不按原样使用（尽管包含可快速部署的[!DNL .war]文件）。 它主要用于构建您自己的自定义许可证服务器的参考。

   许可证服务器功能：

   * 通过使用数据库验证用户名／口令来管理身份验证请求。
   * 管理许可证请求并确定应用许可证链接时正在颁发的许可证类型。
   * 为包含多个Primetime DRM策略的内容颁发许可证。
   * 向iOS客户机发放支持远程密钥投放的许可证，这需要Primetime DRM。
   * 发放需要对内容加密密钥(CEK)进行外部查找和检索的许可证。
   * 搜索视图库以确定用户是否获得对内容的授权。
   * 搜索Primetime DRM策略更新列表。
   * 搜索机器吊销列表。
   * 使用HSM或PKCS12文件存储凭据。
   * 加密在属性文件中指定的密码。
   * 在续订凭据后指定多个许可证服务器或传输凭据。

      旧凭据在服务器上进行维护，这样用户无需重新打包即可继续视图现有内容。
   * 限制允许向许可证服务器发出请求的DRM/运行时版本。
   * 设置客户端时钟窗口回放首选项。
   * 限制请求时间和服务器时间之间允许的时间差以防止重放攻击。
   * 管理来自FMRMS 1.x客户端的请求

      例如，触发FMRMS 1.x客户端以升级到Primetime DRM 2.0或更高版本。
   * 通过使用存储在数据库中的FMRMS 1.x许可证信息，按需将FMRMS 1.x元数据转换为Primetime DRM元数据。
   * 将FMRMS 1.x策略转换为示例代码的Primetime DRM策略。
   * 从现有数据库导入FMRMS 1.x许可证信息以获取示例脚本。
   * 获取服务器版本
   * 域注册
   * 域取消注册
   * 同步请求
   * 许可退回

* **用于受保护流的Primetime DRM**  Server —— 这是一个随时可用的二进制文件，您只需花费很少的精力即可快速实现。对于希望快速显示概念验证的客户来说，这是一个不错的选项；如果您的自定义DRM需求最小，*可以*&#x200B;作为生产选项。 有关详细信息，请参阅下面的相关信息。

* **Primetime Cloud DRM服务** -这是一个Adobe托管的许可证服务器，可用于提供许可证。（您必须是Primetime许可证持有人才能使用此服务。） 此Adobe云服务可免除您构建自己的服务所需的费用、维护和工程。 有关详细信息，请参阅下面的相关信息。

