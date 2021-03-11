---
title: 确定引用实施许可证服务器是否正常运行
description: 确定引用实施许可证服务器是否正常运行
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '362'
ht-degree: 0%

---


# 确定引用实施许可证服务器是否正常运行{#determining-if-reference-implementation-license-server-runs-properly}

有几种方法可确定您的参考实施许可证服务器是否已正确启动。 您可以视图[!DNL catalina.log]日志可能不足，因为许可证服务器会登录到自己的日志文件。 请按照以下步骤确保您的参考实施已正确启动。

* 检查您的[!DNL AdobeFlashAccess.log]文件。 这是引用实施写入日志信息的位置。 此日志文件的位置由[!DNL log4j.xml]文件指示，可进行修改以指向您想要的任何位置。 默认情况下，将日志文件复制到运行catalina的工作目录中。

* 转到以下URL:[!DNL https:// flashaccess/license/v4]*您的服务器：服务器端口*。 您应当看到文本“License Server is setup correatly（许可证服务器设置正确）”。

测试服务器是否正常运行的另一种方法是打包测试内容的一部分，设置一个示例视频播放器，然后播放它。

以下过程描述了此过程：

1. 转到[!DNL \Reference Implementation\Command Line Tools]文件夹。

   有关如何安装命令行工具，请参阅[安装命令行工具](../drm-reference-implementations/command-line-tools/install-command-line-tools.md)。

1. 键入以下命令以创建简单的匿名DRM策略：

   ```
       java -jar libs\AdobePolicyManager.jar new policy_test.pol -x
   ```

   有关如何使用DRM策略管理器创建DRM策略，请参阅[命令行用法](../drm-reference-implementations/command-line-tools/configure-command-line-tools/policy-manager/policy-manager-command-line-usage.md)。

1. 将[!DNL flashaccesstools.properties]文件中的`encrypt.license.serverurl`属性设置为许可证服务器的URL。

   例如，[!DNL https:// localhost:8080/]。 [!DNL flashaccesstools.properties]文件位于[!DNL \Reference Implementation\Command Line Tools]文件夹中。

1. 键入以下命令以打包内容的段：

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

1. 将两个生成的文件复制到Tomcat服务器上的[!DNL webapps\ROOT\Content]文件夹。
1. 转到[!DNL Reference Implementation\Sample Video Players\Desktop\Flash Player\Release]目录，并将内容复制到Tomcat服务器上的 [!DNL webapps\ROOT\SVP\] 文件夹。

1. 安装Flash Player 10.1或更高版本。
1. 打开Web浏览器并转到以下URL:[!DNL        https:// localhost:8080/SVP/player.html]

1. 转到以下URL，然后单击&#x200B;**[!UICONTROL Play]**:[!DNL https:// localhost:8080/Content/] *`your_encrypted_FLV`*。

1. 如果视频播放失败，请检查示例视频播放器的日志窗格中是否显示任何错误代码或是否已添加到[!DNL AdobeFlashAccess.log]文件。

   您现在可以在log4j.xml文件中搜索[!DNL AdobeFlashAccess.log]日志文件的位置，然后对其进行修改。 默认情况下，日志文件将复制到运行catalina的工作目录中。

