---
title: 确定参考实施许可证服务器是否正常运行
description: 确定参考实施许可证服务器是否正常运行
copied-description: true
exl-id: ef28e169-f8d2-4c7f-b606-aa4e811aae9b
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '349'
ht-degree: 0%

---

# 确定参考实施许可证服务器是否正常运行 {#determining-if-reference-implementation-license-server-is-running-properly}

有多种方法可确定服务器是否已正确启动。 查看 [!DNL catalina.log] 日志可能不够，因为许可证服务器将日志记录到自己的日志文件。 请按照以下步骤操作，以确保您的“参考实施”已正确启动。

* 检查您的 [!DNL AdobeFlashAccess.log] 文件。 这是参考实施写入日志信息的位置。 此日志文件的位置由您的 [!DNL log4j.xml] 文件并可修改为指向所需的任何位置。 默认情况下，日志文件将输出到运行catalina的工作目录中。

* 导航到以下URL： `https:///flashaccess/license/v4<your server:server port>`. 您应该会看到文本“License Server is setup correctly”。

测试服务器是否正确运行的另一种方法是打包测试内容，设置一个示例视频播放器并播放它。 以下过程描述了此过程：

1. 导航到 [!DNL \Reference Implementation\Command Line Tools] 文件夹。 有关安装命令行工具的信息，请参见 [安装命令行工具](../aaxs-reference-implementations/command-line-tools/aaxs-ref-impl-command-line-overview.md#installing-the-command-line-tools).

1. 使用以下命令创建一个简单的匿名策略：

   ```
       java -jar libs\AdobePolicyManager.jar new policy_test.pol -x
   ```

   有关使用Policy Manager创建策略的详细信息，请参见 [命令行用法](../aaxs-reference-implementations/command-line-tools/policy-manager/command-line-usage.md).

1. 设置 `encrypt.license.serverurl` 中的属性 [!DNL flashaccesstools.properties] 文件到许可证服务器的URL(例如， `https:// localhost:8080/`)。 此 [!DNL flashaccesstools.properties] 文件位于 [!DNL \Reference Implementation\Command Line Tools] 文件夹。

1. 使用以下命令打包一段内容：

   ```java
       java -jar libs\AdobePackager.jar  
   <i class="+ topic ph hi-d="" i "="">
   test_input_FLV  
   <i class="+ topic ph hi-d="" i "="">
   output_file  
               -p policy_test.pol 
   </i class="+ topic> 
   </i class="+ topic>
   ```

1. 将2个生成的文件复制到Tomcat [!DNL webapps\ROOT\Content] 文件夹。
1. 导航到 `Reference Implementation\Sample Video Players\Desktop\Flash Player\Release` 并将内容复制到Tomcat `webapps\ROOT\SVP\` 文件夹。
1. 安装Flash Player10.1或更高版本。
1. 打开Web浏览器并导航到以下URL：

   `https:// localhost:8080/SVP/player.html`
1. 导航到以下URL，然后单击“播放”按钮：

   `https:// localhost:8080/Content/<your_encrypted_FLV>`
1. 如果视频无法播放，请检查示例视频播放器的日志窗格中是否写入了任何错误代码，或在 `AdobeFlashAccess.log` 文件。 的位置 `AdobeFlashAccess.log` log文件由log4j.xml文件指示，并且可以修改以指向所需的任何位置。 默认情况下，日志文件将写入到运行catalina的工作目录中。
