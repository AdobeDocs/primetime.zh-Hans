---
title: 检查许可证服务器是否正确启动
description: 检查许可证服务器是否正确启动
copied-description: true
exl-id: 05995a75-9468-4237-9091-a07606297772
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '132'
ht-degree: 0%

---

# 检查许可证服务器是否正确启动 {#check-whether-the-license-server-started-properly}

有多种方法可确定参考实施许可证服务器是否已正确启动。 一种方法是检查 [!DNL catalina.log] 日志，但这可能不够，因为许可证服务器会记录到自己的日志文件。
1. 检查您的 [!DNL AdobeFlashAccess.log] 文件。

   这是参考实施许可证服务器写入日志信息的位置。 此日志文件的位置由您的 [!DNL log4j.xml] 文件并可修改为指向任何位置。 默认情况下，日志文件将复制到运行日志的工作目录中 `catalina` Tomcat脚本。
1. 转到以下URL，并验证是否显示了“License Server设置正确”文本：
   [!DNL ht<span></span>tps://localhost:8080/flashaccess/license/v4]
