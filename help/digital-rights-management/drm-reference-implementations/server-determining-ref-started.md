---
title: 检查许可证服务器是否正常启动
description: 检查许可证服务器是否正常启动
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '132'
ht-degree: 0%

---


# 检查许可证服务器是否正确启动{#check-whether-the-license-server-started-properly}

有几种方法可确定您的参考实施许可证服务器是否已正确启动。 一种方法是检查[!DNL catalina.log]日志，但这可能不够，因为许可证服务器会登录到自己的日志文件。
1. 检查您的[!DNL AdobeFlashAccess.log]文件。

   这是引用实施许可证服务器写入日志信息的位置。 此日志文件的位置由[!DNL log4j.xml]文件指示，可修改以指向任何位置。 默认情况下，日志文件将复制到运行`catalina` Tomcat脚本的工作目录中。
1. 转到以下URL，并验证文本“License Server is setup correctly”（许可证服务器设置正确）是否显示：
   [!DNL ht<span></span>tps://localhost:8080/flashaccess/license/v4]
