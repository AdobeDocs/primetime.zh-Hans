---
title: 设置许可证服务器数据库
description: 设置许可证服务器数据库
copied-description: true
exl-id: be6232b4-bf51-486f-9c85-ab6f6ec6d9bd
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '217'
ht-degree: 0%

---

# 设置许可证服务器数据库{#set-up-the-license-server-database}

参考实施许可证服务器要求数据库支持以下内容：

* 用户身份验证
* 使用模型演示业务规则
* 元数据转换
* 域支持

匿名许可证获取不要求数据库正在运行。

>[!NOTE]
>
>此过程仅适用于Microsoft Windows。 对于其他操作系统，请参阅适用于您的操作系统的文档或参阅MySQL文档。

要运行许可证服务器，您需要安装和配置MySQL：

1. 在DVD上，转到 [!DNL Third Party\MySQL\Installer\5.1] 文件夹并启动安装程序。
1. 完成MySQL安装。
1. 选择 **[!UICONTROL Configure MySQL Server Now]** 以启动配置向导。
1. 在进入第五个屏幕之前，请使用默认设置或选择特定设置进行测试。
1. 在第五个屏幕上，选择 **[!UICONTROL Online Transaction Processing (OLTP)]** 或 **[!UICONTROL Manual Setting]** 并输入允许的最大连接数。
1. 记下root密码。
1. 要重新安装MySQL，如果需要稍后启动服务器，请完成以下步骤：
   1. 删除 *系统驱动器：* 文件夹。

      此文件夹位于 [!DNL \Documents and Settings\All Users\Application Data\MySQL].
   1. 删除旧的MySQL安装文件夹。

      例如， *系统驱动器：*，它位于 [!DNL \Program Files\MySQL\MySQL Server 5.1].
1. 要安装MySQL JDBC驱动程序5.1.7，请复制 [!DNL mysql-connector-java-5.1.7-bin.jar] 中的文件 [!DNL Third Party\MySQL\Installer\5.1] 在DVD上的文件夹 [!DNL ...\Tomcat6.0\lib] 目录。

   >[!NOTE]
   >
   >MySQL JDBC驱动程序5.1.7适用于Tomcat 6.0。不再支持旧版本的Tomcat。
