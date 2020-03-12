---
description: 'null'
seo-description: 'null'
seo-title: 确定引用实施许可证服务器是否正常运行
title: 确定引用实施许可证服务器是否正常运行
uuid: afd82d6d-a11c-48ff-b48c-8f81d4b406a0
translation-type: tm+mt
source-git-commit: 19e7c941b3337c3b4d37f0b6a1350aac2ad8a0cc

---


# 确定引用实施许可证服务器是否正常运行 {#determining-if-reference-implementation-license-server-runs-properly}

有几种方法可确定您的参考实施许可证服务器是否已正确启动。 由于许可证服 [!DNL catalina.log] 务器会将日志记录到自己的日志文件，因此您可以查看日志可能不足。 请按照以下步骤确保您的参考实施已正确启动。

* 检查您的 [!DNL AdobeFlashAccess.log] 文件。 这是引用实施写入日志信息的位置。 此日志文件的位置由您的文件指示， [!DNL log4j.xml] 并可以对其进行修改以指向您需要的任何位置。 默认情况下，将日志文件复制到运行Catalina的工作目录中。

* 转到以下URL:服 [!DNL https:// flashaccess/license/v4]*务器：服务器端口&#x200B;*。 您应当看到文本“License Server is setup correctly（许可证服务器设置正确）”。

测试服务器是否正常运行的另一种方法是打包测试内容的一段，设置一个示例视频播放器，然后播放它。

以下过程描述了此过程：

1. 转到文件 [!DNL \Reference Implementation\Command Line Tools] 夹。

   请参 [阅安装命令行工具](../drm-reference-implementations/command-line-tools/install-command-line-tools.md) ，了解如何安装命令行工具。

1. 键入以下命令以创建简单的匿名DRM策略：

   ```
       java -jar libs\AdobePolicyManager.jar new policy_test.pol -x
   ```

   请参 [阅如何使用](../drm-reference-implementations/command-line-tools/configure-command-line-tools/policy-manager/policy-manager-command-line-usage.md) “DRM策略管理器”创建DRM策略的命令行使用。

1. 将文件 `encrypt.license.serverurl` 中的属 [!DNL flashaccesstools.properties] 性设置为许可证服务器的URL。

   For example, [!DNL https:// localhost:8080/]. 文 [!DNL flashaccesstools.properties] 件位于文件夹 [!DNL \Reference Implementation\Command Line Tools] 中。

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

1. 将两个生成的文件复制到Tomcat服 [!DNL webapps\ROOT\Content] 务器上的文件夹中。
1. 转到该目 [!DNL Reference Implementation\Sample Video Players\Desktop\Flash Player\Release] 录，并将内容复制到Tomcat服务器上的[!DNL webapps\ROOT\SVP\]文件夹。

1. 安装Flash Player 10.1版或更高版本。
1. 打开Web浏览器并转到以下URL: [!DNL        https:// localhost:8080/SVP/player.html]

1. 转到以下URL，然后单击 **[!UICONTROL Play]**: [!DNL https:// localhost:8080/Content/]*`your_encrypted_FLV`*.

1. 如果视频播放失败，请检查示例视频播放器的记录窗格中是否显示任何错误代码或是否将其添加到文 [!DNL AdobeFlashAccess.log] 件中。

   您现在可以在log4j.xml文件中 [!DNL AdobeFlashAccess.log] 搜索日志文件的位置，然后对其进行修改。 默认情况下，日志文件被复制到运行Catalina的工作目录中。

