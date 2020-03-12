---
seo-title: 设置数据库并配置JNDI数据源
title: 设置数据库并配置JNDI数据源
uuid: 1326523f-c053-4169-a934-1b2d3907b1f4
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# 设置数据库并配置JNDI数据源 {#setting-up-the-database-and-configuring-the-jndi-datasource}

参考实施许可证服务器需要一个数据库来支持以下功能：

* 用户身份验证
* 使用模型演示业务规则
* 元数据转换
* 域支持

获取匿名许可证不需要数据库运行。

>[!NOTE] {class=&quot;- topic/note &quot;}
>
>本节中的说明针对Microsoft Windows平台。 有关其他操作系统，请参阅操作系统的文档或MySQL文档。

要运行许可证服务器，您需要安装和配置MySQL 5.1.34:

1. 运行MySQL安装程序(位于DVD上的第三个Party\MySQL\Installer\5.1文件夹中)。
1. 在安装过程结束时，选中以 **[!UICONTROL Configure MySQL Server Now]** 启动配置向导。 为测试目的使用默认设置或选择特定设置，但第5个屏幕上必须选择或 **[!UICONTROL Online Transaction Processing (OLTP)]** 输 **[!UICONTROL Manual Setting]** 入允许的最大连接数。

1. 记下根密码。
1. 如果需要重新安装MySQL，请按照以下步骤操作，以避免在以后启动服务器时出现问题：

   * 删除文件夹系 *统驱动器：*[!DNL \Documents and Settings\All Users\Application Data\MySQL].

   * 删除旧的MySQL安装文件夹：例如，系 *统驱动器：*[!DNL \Program Files\MySQL\MySQL Server 5.1].

接下来，您需要安装MySQL JDBC驱动程序5.1.7。为此，请将( [!DNL mysql-connector-java-5.1.7-bin.jar] 位于DVD上的文 [!DNL Third Party\MySQL\Installer\5.1] 件夹中)复制到Tomcat Server lib目录： [!DNL ...\Tomcat6.0\lib].

>[!NOTE] {class=&quot;- topic/note &quot;}
>
>MySQL JDBC驱动程序5.1.7可与Tomcat 6.0一起使用。不支持旧版Tomcat。

通过设置数据库架构并使用示例数据填充数据库来设置示例数据库。 为此，请执行以下步骤：

1. 转到 **[!UICONTROL Window's Start Menu]** > **[!UICONTROL MySQL]** > **[!UICONTROL MySQL Server 5.1]** > **[!UICONTROL MySQL Command Line Client]** 。
1. 在键入密码后，执行以下SQL脚本以添加用于通过Web应用程序建立连接的用户帐户并创建数据库架构（确保最后没有“;”）。 `dbuser` 只需按Enter键。):

   ```
       mysql> source “Reference Implementation\Server\dbscript\createsampledb.sql”
   ```

1. 编辑在表中填充样本数据的脚本，以包含用于测试目的的数据： [!DNL Reference Implementation\Server\dbscript\PopulateSampleDB.sql].
1. 执行此脚本以填充数据，就像在步骤2中一样。

>[!NOTE] {class=&quot;- topic/note &quot;}
>
>第一次运行脚本时， [!DNL CreateSampleDB.sql] 您将收到以下错误：

*错误1396(HY000):对于“dbuser”@“localhost”查询OK，操作DROP USER失败，影响0行（0.00秒）。*

您可以安全地忽略此错误。 这仅在您第一次运行此脚本时发生。

此时，您需要配置数据库连接池(DBCP)。 DBCP使用Jakarta-Commons Database Connection Pool。 将JNDI数据源TestDB配置为利用此应用程序服务器连接池。 要将数据库连接更改为指向不在localhost上的MySQL服务器，请修改位于其中的文件（指定许可证服务器数据库的位置、用户名和口令），或使用更新的文件修改 [!DNL META-INF\context.xml][!DNL flashaccess.war][!DNL \Reference Implementation\Server\refimpl\WebContent\META-INF\context.xml] 并重新创建WAR文件。 要更改这些参数中的任何一个，请编 [!DNL context.xml] 辑位于WebContent目录中的参数，然后使用Ant脚本重新创建WAR文件。 要调整数据库，请更改此文件中的JNDI数据源设置。

如果在Eclipse中调试“参考实施”项目，则需要将其添 `$CATALINA_HOME\lib\tomcat-dbcp.jar` 加到运行／调试配置中。 如果在独立的Tomcat 6.0服务器上运 [!DNL flashaccess.war] 行该文件，则不需要执行此步骤。
