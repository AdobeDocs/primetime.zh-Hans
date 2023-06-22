---
title: 设置数据库和配置JNDI数据源
description: 设置数据库和配置JNDI数据源
copied-description: true
exl-id: ed22f095-924b-4792-8a10-e7548fab2c3b
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '521'
ht-degree: 0%

---

# 设置数据库和配置JNDI数据源 {#setting-up-the-database-and-configuring-the-jndi-datasource}

参考实施许可证服务器要求数据库支持以下功能：

* 用户身份验证
* 使用模型演示业务规则
* 元数据转换
* 域支持

匿名许可证获取不需要运行数据库。

>[!NOTE]
>
>本节中的说明适用于Microsoft Windows平台。 对于其他操作系统，请参阅适用于您的操作系统的文档或参阅MySQL文档。

要运行许可证服务器，您需要安装和配置MySQL 5.1.34：

1. 运行MySQL安装程序(位于DVD上的第三个Party\MySQL\Installer\5.1文件夹中)。
1. 在安装过程结束时，检查 **[!UICONTROL Configure MySQL Server Now]** 以启动配置向导。 使用默认设置或选择特定设置进行测试，但您必须在第5个屏幕上选择的设置除外 **[!UICONTROL Online Transaction Processing (OLTP)]** 或 **[!UICONTROL Manual Setting]** 并输入允许的最大连接数。

1. 记下root密码。
1. 如果需要重新安装MySQL，请按照以下步骤操作，以避免在之后启动服务器时出现问题：

   * 删除文件夹 *系统驱动器：* [!DNL \Documents and Settings\All Users\Application Data\MySQL].

   * 删除旧的MySQL安装文件夹：例如， *系统驱动器：* [!DNL \Program Files\MySQL\MySQL Server 5.1].

接下来，您需要安装MySQL JDBC驱动程序5.1.7。要执行此操作，请复制 [!DNL mysql-connector-java-5.1.7-bin.jar] (可在 [!DNL Third Party\MySQL\Installer\5.1] 文件夹)到Tomcat Server lib目录： [!DNL ...\Tomcat6.0\lib].

>[!NOTE]
>
>MySQL JDBC驱动程序5.1.7适用于Tomcat 6.0。不支持旧版本的Tomcat。

通过设置数据库模式并使用示例数据填充数据库来设置示例数据库。 为此，请执行以下步骤：

1. 转到  **[!UICONTROL Window's Start Menu]** > **[!UICONTROL MySQL]** > **[!UICONTROL MySQL Server 5.1]** > **[!UICONTROL MySQL Command Line Client]** .
1. 键入密码后，执行以下SQL脚本以添加用户帐户 `dbuser` 用于通过Web应用程序建立连接并创建数据库模式（确保末尾没有“；”）。 只需按Enter。)：

   ```
       mysql> source “Reference Implementation\Server\dbscript\createsampledb.sql”
   ```

1. 编辑在表中填充示例数据的脚本，以包含用于测试的数据： [!DNL Reference Implementation\Server\dbscript\PopulateSampleDB.sql].
1. 执行此脚本以像在步骤2中一样填充数据。

>[!NOTE]
>
>第一次运行 [!DNL CreateSampleDB.sql] 脚本您将收到以下错误：

*错误1396 (HY000)：对“dbuser”@&#39;localhost&#39;查询正常，执行DROP USER操作失败，0行受到影响（0.00秒）。*

您可以安全地忽略此错误。 仅当您首次运行此脚本时，才会发生这种情况。

此时，您需要配置数据库连接池(DBCP)。 DBCP使用Jakarta-Commons数据库连接池。 JNDI数据源TestDB配置为利用此应用程序服务器连接池。 要将数据库连接更改为指向不在本地主机上的MySQL服务器，请修改 [!DNL META-INF\context.xml] 文件（指定许可证服务器数据库的位置、用户名和密码） [!DNL flashaccess.war]，或进行修改 [!DNL \Reference Implementation\Server\refimpl\WebContent\META-INF\context.xml] 并使用更新的文件重新创建WAR文件。 要更改其中的任何参数，请编辑 [!DNL context.xml] ，并使用Ant脚本重新创建WAR文件。 要优化数据库，请更改此文件中的JNDI数据源设置。

如果您在Eclipse中调试参考实施项目，则需要添加 `$CATALINA_HOME\lib\tomcat-dbcp.jar` 到您的运行/调试配置。 如果您运行 [!DNL flashaccess.war] 文件，该文件位于独立Tomcat 6.0服务器上。
