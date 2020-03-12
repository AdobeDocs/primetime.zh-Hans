---
description: 'null'
seo-description: 'null'
seo-title: 确定引用实施许可证服务器是否正常运行
title: 确定引用实施许可证服务器是否正常运行
uuid: 84d32c94-7594-464e-a883-5338b52de2bf
translation-type: tm+mt
source-git-commit: e60d285b9e30cdd19728e3029ecda995cd100ac9

---


# 确定引用实施许可证服务器是否正常运行 {#determining-if-reference-implementation-license-server-is-running-properly}

有几种方法可确定服务器是否已正确启动。 查看日 [!DNL catalina.log] 志可能不够，因为许可证服务器会登录到自己的日志文件。 请按照以下步骤确保您的参考实施已正确启动。

* 检查您的 [!DNL AdobeFlashAccess.log] 文件。 这是引用实施写入日志信息的位置。 此日志文件的位置由您的文件指示， [!DNL log4j.xml] 并可以对其进行修改以指向您需要的任何位置。 默认情况下，日志文件将输出到运行Catalina的工作目录。

* 导航到以下URL: `https:///flashaccess/license/v4<your server:server port>`. 您应当看到文本“License Server is setup correctly（许可证服务器设置正确）”。

测试服务器是否正确运行的另一种方法是打包测试内容、设置示例视频播放器并播放它。 以下过程描述了此过程：

1. 导览至文 [!DNL \Reference Implementation\Command Line Tools] 件夹。 有关安装命令行工具的信息，请参 [阅安装命令行工具](../aaxs-reference-implementations/command-line-tools/aaxs-ref-impl-command-line-overview.md#installing-the-command-line-tools)。

1. 使用以下命令创建一个简单的匿名策略：

   ```
       java -jar libs\AdobePolicyManager.jar new policy_test.pol -x
   ```

   有关使用策略管理器创建策略的详细信息，请参阅 [命令行使用](../aaxs-reference-implementations/command-line-tools/policy-manager/command-line-usage.md)。

1. 将文件 `encrypt.license.serverurl` 中的属 [!DNL flashaccesstools.properties] 性设置为许可证服务器的URL(例如， `https:// localhost:8080/`)。 文件 [!DNL flashaccesstools.properties] 位于文件夹下 [!DNL \Reference Implementation\Command Line Tools] 方。

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

1. 将生成的2个文件复制到Tomcat文 [!DNL webapps\ROOT\Content] 件夹。
1. 导览至 `Reference Implementation\Sample Video Players\Desktop\Flash Player\Release` 内容并将其复制到Tomcat文 `webapps\ROOT\SVP\` 件夹。
1. 安装Flash Player 10.1或更高版本。
1. 打开Web浏览器并导航到以下URL:

   `https:// localhost:8080/SVP/player.html`
1. 导航到以下URL，然后单击“播放”按钮：

   `https:// localhost:8080/Content/<your_encrypted_FLV>`
1. 如果视频播放失败，请检查是否在示例视频播放器的记录窗格中或文件中写入了任何错误 `AdobeFlashAccess.log` 代码。 日志文件的 `AdobeFlashAccess.log` 位置由log4j.xml文件指示，可以修改为指向所需的任何位置。 默认情况下，日志文件会写入运行Catalina的工作目录中。
