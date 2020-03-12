---
description: 'null'
seo-description: 'null'
seo-title: 检查许可证服务器是否正确启动
title: 检查许可证服务器是否正确启动
uuid: a6a034c9-b3c4-4e26-b901-d2c132c00c52
translation-type: tm+mt
source-git-commit: 19e7c941b3337c3b4d37f0b6a1350aac2ad8a0cc

---


# 检查许可证服务器是否正确启动 {#check-whether-the-license-server-started-properly}

有几种方法可确定您的参考实施许可证服务器是否已正确启动。 一种方法是检查日志， [!DNL catalina.log] 但这可能不够，因为许可证服务器会登录到自己的日志文件。
1. 检查您的 [!DNL AdobeFlashAccess.log] 文件。

   这是参考实施许可证服务器写入日志信息的位置。 此日志文件的位置由您的文件指示， [!DNL log4j.xml] 并可以对其进行修改以指向任何位置。 默认情况下，日志文件将复制到运行 `catalina` Tomcat脚本的工作目录。
1. 转到以下URL，并验证文本“License Server is set up correctly”（许可证服务器设置正确）是否显示：
   [!DNL ht<span></span>tps://localhost:8080/flashaccess/license/v4]
