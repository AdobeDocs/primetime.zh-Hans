---
title: 确定参考实施许可证服务器是否正常运行
description: 确定参考实施许可证服务器是否正常运行
copied-description: true
exl-id: 97ca0b6c-2661-4cdc-b8d0-dcc545f009f6
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '362'
ht-degree: 0%

---

# 确定参考实施许可证服务器是否正常运行 {#determining-if-reference-implementation-license-server-runs-properly}

有多种方法可确定参考实施许可证服务器是否已正确启动。 您可以查看 [!DNL catalina.log] 日志可能不够，因为许可证服务器将日志记录到自己的日志文件。 请按照以下步骤操作，以确保您的“参考实施”已正确启动。

* 检查您的 [!DNL AdobeFlashAccess.log] 文件。 这是参考实施写入日志信息的位置。 此日志文件的位置由您的 [!DNL log4j.xml] 文件并可修改为指向所需的任何位置。 默认情况下，日志文件会复制到运行catalina的工作目录中。

* 转到以下URL： [!DNL https:// flashaccess/license/v4]*您的服务器：服务器端口*. 您应该会看到文本“License Server is setup correctly”。

测试服务器是否正确运行的另一种方法是打包测试内容的区段，设置一个示例视频播放器，然后播放它。

以下过程描述了此过程：

1. 转到 [!DNL \Reference Implementation\Command Line Tools] 文件夹。

   参见 [安装命令行工具](../drm-reference-implementations/command-line-tools/install-command-line-tools.md) 有关如何安装命令行工具的信息。

1. 键入以下命令以创建简单的匿名DRM策略：

   ```
       java -jar libs\AdobePolicyManager.jar new policy_test.pol -x
   ```

   参见 [命令行用法](../drm-reference-implementations/command-line-tools/configure-command-line-tools/policy-manager/policy-manager-command-line-usage.md) 有关如何使用DRM策略管理器创建DRM策略。

1. 设置 `encrypt.license.serverurl` 中的属性 [!DNL flashaccesstools.properties] 文件到许可证服务器的URL。

   例如， [!DNL https:// localhost:8080/]. 此 [!DNL flashaccesstools.properties] 文件位于 [!DNL \Reference Implementation\Command Line Tools] 文件夹。

1. 键入以下命令以打包内容的区段：

```
       java -jar libs\AdobePackager.jar  
       <i class="+ topic ph hi-d="" i "="">
         test_input_FLV  
        <i class="+ topic ph hi-d="" i "="">
       output_file  
               -p policy_test.pol 
       </i class="+ topic> 
       </i class="+ topic>
```

1. 将两个生成的文件复制到 [!DNL webapps\ROOT\Content] 文件夹（在Tomcat服务器上）。
1. 转到 [!DNL Reference Implementation\Sample Video Players\Desktop\Flash Player\Release] 目录，并将内容复制到 [!DNL webapps\ROOT\SVP\] 文件夹（在Tomcat服务器上）。

1. 安装Flash Player版本10.1或更高版本。
1. 打开Web浏览器，然后转到以下URL： [!DNL        https:// localhost:8080/SVP/player.html]

1. 转到以下URL，然后单击 **[!UICONTROL Play]**： [!DNL https:// localhost:8080/Content/] *`your_encrypted_FLV`*.

1. 如果视频无法播放，请检查示例视频播放器的日志窗格中是否显示了任何错误代码，或是否将其添加到 [!DNL AdobeFlashAccess.log] 文件。

   您现在可以搜索 [!DNL AdobeFlashAccess.log] log4j.xml文件中的日志文件，然后对其进行修改。 默认情况下，日志文件会复制到运行catalina的工作目录中。
