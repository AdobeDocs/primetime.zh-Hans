---
description: 'null'
seo-description: 'null'
seo-title: 设置许可证服务器数据库
title: 设置许可证服务器数据库
uuid: aa6185f2-8e9d-4b65-971a-b7534d910580
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# 设置许可证服务器数据库{#set-up-the-license-server-database}

参考实施许可证服务器需要一个数据库来支持以下内容：

* 用户身份验证
* 使用模型演示业务规则
* 元数据转换
* 域支持

获取匿名许可证不要求数据库运行。

>[!NOTE] {class=&quot;- topic/note &quot;}
>
>此过程仅适用于Microsoft Windows。 有关其他操作系统，请参阅操作系统的文档或MySQL文档。

要运行许可证服务器，您需要安装和配置MySQL:

1. 在DVD上，转到文件夹 [!DNL Third Party\MySQL\Installer\5.1] 并启动安装程序。
1. 与MySQL安装竞争。
1. 选择 **[!UICONTROL Configure MySQL Server Now]** 以启动配置向导。
1. 在第五个屏幕之前，请使用默认设置或为测试选择特定设置。
1. 在第五个屏幕上，选择或 **[!UICONTROL Online Transaction Processing (OLTP)]** 输 **[!UICONTROL Manual Setting]** 入允许的最大连接数。
1. 记下根密码。
1. 要重新安装MySQL，如果需要稍后启动服务器，请完成以下步骤：
   1. 删除系 *统驱动器：* 文件夹。

      此文件夹位于 [!DNL \Documents and Settings\All Users\Application Data\MySQL]。
   1. 删除旧的MySQL安装文件夹。

      例如， *系统驱动器：*，它位于 [!DNL \Program Files\MySQL\MySQL Server 5.1]。
1. 要安装MySQL JDBC驱动程序5.1.7，请将DVD上 [!DNL mysql-connector-java-5.1.7-bin.jar] 的文件夹中的 [!DNL Third Party\MySQL\Installer\5.1] 文件复制到Tomcat服务器 [!DNL ...\Tomcat6.0\lib] 上的目录中。

   >[!NOTE] {class=&quot;- topic/note &quot;}
   >
   >MySQL JDBC驱动程序5.1.7可与Tomcat 6.0一起使用。不再支持旧版Tomcat。

