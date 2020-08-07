---
description: 'null'
seo-description: 'null'
seo-title: 配置许可证服务器数据库
title: 配置许可证服务器数据库
uuid: 6d34e849-1616-46bd-ad18-4f98e6c45af7
translation-type: tm+mt
source-git-commit: 1b9792a10ad606b99b6639799ac2aacb707b2af5
workflow-type: tm+mt
source-wordcount: '296'
ht-degree: 0%

---


# 配置许可证服务器数据库{#configure-the-license-server-database}

要配置示例模式库，请设置数据库并使用示例数据填充数据库：

1. 调出MySQL命令行。

   **在Windows上——单** 击 **[!UICONTROL Window's Start Menu]** > **[!UICONTROL MySQL]** > **[!UICONTROL MySQL Server 5.1]** > **[!UICONTROL MySQL Command Line Client]**

   **在Linux等上。** -类型 `MySQL`。

1. 执行以下SQL脚本：

   mysql>源“ `"[DRM SDK DVD]\Reference Implementation\Server\Reference Implementation Server\dbscript\createsampledb.sql" dbscript\createsampledb.sql`”

   此脚本添加用户帐户 `dbuser`、通过Web应用程序建立连接并创建数据库模式。

   >[!NOTE]
   >
   >确保脚本末尾 `;`没有分号()。

1. 编辑 `PopulateSampleDB.sql` 在表中填充示例数据的脚本，以包含测试数据。

   此脚本位于文件 `[DRM SDK DVD]\Reference Implementation\Server\Reference Implementation Server\dbscript\ dbscript\` 夹中。
1. 执行 [!DNL PopulateSampleDB] 脚本以填充数据，就像在步骤2中一样。

   >[!NOTE]
   >
   >第一次运行脚本时， [!DNL CreateSampleDB.sql] 会出现以下错误：

   您可以安全地忽略此错误。 它仅在您第一次运行此脚本时发生。

您需要配置使用Jakarta-Commons数据库连接池的数据库连接池(DBCP)。 将JNDI数据源TestDB配置为利用此应用程序服务器连接池。 要更改数据库连接以指向不在localhost上的MySQL服务器，请修改以下文件之一：

* 文 [!DNL META-INF\context.xml] 件，指定文件中许可证服务器数据库的位置、用户名和口 [!DNL flashaccess.war] 令。

* 文 `[DRM SDK DVD]\Reference Implementation\Server\Reference Implementation Server\refimpl\WebContent/META-INF\context.xml` 件。

并使用更新的文件重新创建WAR文件。

要更改这些参数中的任何一个，请 [!DNL context.xml] 编辑目录 [!DNL WebContent] 中的文件，然后使用Ant脚本重新创建WAR文件。 要调整数据库，请更改此文件中的JNDI数据源设置。

如果在Eclipse中调试引用实施项目，请添 `$CATALINA_HOME\lib\tomcat-dbcp.jar` 加到运行／调试配置中。

>[!NOTE]
>
>如果在独立 [!DNL flashaccess.war] 的Tomcat 6.0服务器上运行该文件，则不需要执行此步骤。

