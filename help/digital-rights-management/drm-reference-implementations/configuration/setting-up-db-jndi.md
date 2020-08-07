---
description: 'null'
seo-description: 'null'
seo-title: 设置许可证服务器数据库
title: 设置许可证服务器数据库
uuid: aa6185f2-8e9d-4b65-971a-b7534d910580
translation-type: tm+mt
source-git-commit: 1b9792a10ad606b99b6639799ac2aacb707b2af5
workflow-type: tm+mt
source-wordcount: '219'
ht-degree: 0%

---


# 设置许可证服务器数据库{#set-up-the-license-server-database}

引用实施许可证服务器需要一个数据库来支持以下内容：

* 用户身份验证
* 使用模型演示业务规则
* 元数据转换
* 域支持

匿名获取许可证不要求数据库正在运行。

>[!NOTE]
>
>此过程仅适用于Microsoft Windows。 有关其他操作系统，请参阅操作系统文档或MySQL文档。

要运行许可证服务器，您需要安装和配置MySQL:

1. 在DVD上，转到文件夹 [!DNL Third Party\MySQL\Installer\5.1] 并开始安装项目。
1. 完成MySQL安装。
1. 选择 **[!UICONTROL Configure MySQL Server Now]** 以开始配置向导。
1. 在第五个屏幕之前，请使用默认设置或为测试选择特定设置。
1. 在第五个屏幕上，选 **[!UICONTROL Online Transaction Processing (OLTP)]** 择或 **[!UICONTROL Manual Setting]** 输入允许的最大连接数。
1. 写下根密码。
1. 要重新安装MySQL，如果您以后需要开始服务器，请完成以下步骤：
   1. 删除系 *统驱动器：* 文件夹。

      此文件夹位于 [!DNL \Documents and Settings\All Users\Application Data\MySQL]。
   1. 删除旧的MySQL安装文件夹。

      例如， *系统驱动*&#x200B;器：，位于 [!DNL \Program Files\MySQL\MySQL Server 5.1]。
1. 要安装MySQL JDBC驱动程序5.1.7，请将DVD上 [!DNL mysql-connector-java-5.1.7-bin.jar] 的文 [!DNL Third Party\MySQL\Installer\5.1] 件夹中的文件复制到Tomcat服 [!DNL ...\Tomcat6.0\lib] 务器上的目录。

   >[!NOTE]
   >
   >MySQL JDBC驱动程序5.1.7可与Tomcat 6.0一起使用。不再支持旧版本的Tomcat。

