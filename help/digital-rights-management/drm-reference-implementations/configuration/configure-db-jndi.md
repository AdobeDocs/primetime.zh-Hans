---
title: 配置许可证服务器数据库
description: 配置许可证服务器数据库
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '294'
ht-degree: 0%

---

# 配置许可证服务器数据库{#configure-the-license-server-database}

要通过设置数据库模式并用示例数据填充数据库来配置示例数据库，请执行以下操作：

1. 打开MySQL命令行。

   **在Windows上 —** 单击  **[!UICONTROL Window's Start Menu]** > **[!UICONTROL MySQL]** > **[!UICONTROL MySQL Server 5.1]** > **[!UICONTROL MySQL Command Line Client]**

   **在Linux等上**  — 类型 `MySQL`.

1. 执行以下SQL脚本：

   mysql>源&#39;&#39; `"[DRM SDK DVD]\Reference Implementation\Server\Reference Implementation Server\dbscript\createsampledb.sql" dbscript\createsampledb.sql`&quot;

   此脚本添加用户帐户 `dbuser`，通过Web应用程序建立连接，并创建数据库模式。

   >[!NOTE]
   >
   >确保没有分号( `;`)。

1. 编辑 `PopulateSampleDB.sql` 该脚本填充表中的示例数据以包含用于测试的数据。

   此脚本位于 `[DRM SDK DVD]\Reference Implementation\Server\Reference Implementation Server\dbscript\ dbscript\` 文件夹。
1. 执行 [!DNL PopulateSampleDB] 脚本，可像在步骤2中一样填充数据。

   >[!NOTE]
   >
   >第一次运行 [!DNL CreateSampleDB.sql] 脚本出现以下错误：

   您可以安全地忽略此错误。 它只在您第一次运行此脚本时发生。

您需要配置数据库连接池(DBCP)，它使用Jakarta-Commons数据库连接池。 JNDI数据源TestDB配置为利用此应用程序服务器连接池。 要将数据库连接更改为指向不在本地主机上的MySQL服务器，请修改以下文件之一：

* 此 [!DNL META-INF\context.xml] 文件，指定许可证服务器数据库在 [!DNL flashaccess.war] 文件。

* 此 `[DRM SDK DVD]\Reference Implementation\Server\Reference Implementation Server\refimpl\WebContent/META-INF\context.xml` 文件。

并使用更新的文件重新创建WAR文件。

要更改其中的任何参数，请编辑 [!DNL context.xml] 中的文件 [!DNL WebContent] 目录并使用Ant脚本重新创建WAR文件。 要优化数据库，请更改此文件中的JNDI数据源设置。

如果您在Eclipse中调试参考实施项目，请添加 `$CATALINA_HOME\lib\tomcat-dbcp.jar` 到您的运行/调试配置。

>[!NOTE]
>
>如果您运行 [!DNL flashaccess.war] 文件，不需要执行此步骤。
