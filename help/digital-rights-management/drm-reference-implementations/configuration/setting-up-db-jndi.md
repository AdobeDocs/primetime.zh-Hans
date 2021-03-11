---
title: 设置许可证服务器数据库
description: 设置许可证服务器数据库
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '217'
ht-degree: 0%

---


# 设置许可证服务器数据库{#set-up-the-license-server-database}

参考实施许可证服务器需要一个数据库来支持以下内容：

* 用户身份验证
* 使用模型演示业务规则
* 元数据转换
* 域支持

匿名获取许可证不要求数据库运行。

>[!NOTE]
>
>此过程仅适用于Microsoft Windows。 有关其他操作系统，请参阅操作系统的文档或查看MySQL文档。

要运行许可证服务器，您需要安装并配置MySQL:

1. 在DVD上，转到[!DNL Third Party\MySQL\Installer\5.1]文件夹并开始安装项目。
1. 参与MySQL安装。
1. 选择&#x200B;**[!UICONTROL Configure MySQL Server Now]**&#x200B;以开始配置向导。
1. 在第五个屏幕之前，请使用默认设置或为测试选择特定设置。
1. 在第五个屏幕上，选择&#x200B;**[!UICONTROL Online Transaction Processing (OLTP)]**&#x200B;或&#x200B;**[!UICONTROL Manual Setting]**&#x200B;并输入允许的最大连接数。
1. 写下根密码。
1. 要重新安装MySQL，如果您需要稍后开始服务器，请完成以下步骤：
   1. 删除&#x200B;*系统驱动器：*&#x200B;文件夹。

      此文件夹位于[!DNL \Documents and Settings\All Users\Application Data\MySQL]中。
   1. 删除旧的MySQL安装文件夹。

      例如，*系统驱动器：*，位于[!DNL \Program Files\MySQL\MySQL Server 5.1]中。
1. 要安装MySQL JDBC驱动程序5.1.7，请将DVD上[!DNL Third Party\MySQL\Installer\5.1]文件夹中的[!DNL mysql-connector-java-5.1.7-bin.jar]文件复制到Tomcat服务器上的[!DNL ...\Tomcat6.0\lib]目录。

   >[!NOTE]
   >
   >MySQL JDBC驱动程序5.1.7可与Tomcat 6.0一起使用。不再支持旧版Tomcat。

