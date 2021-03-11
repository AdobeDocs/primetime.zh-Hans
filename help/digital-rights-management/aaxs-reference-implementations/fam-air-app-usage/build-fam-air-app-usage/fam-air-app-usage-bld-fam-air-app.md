---
title: 构建Flash Access Manager AIR应用程序
description: 构建Flash Access Manager AIR应用程序
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '349'
ht-degree: 0%

---


# 构建Flash Access Manager AIR应用程序{#building-the-flash-access-manager-air-application}

要从源代码构建Flash Access Manager AIR文件，您需要在计算机上安装Flex和AIR SDK。 在打包并运行应用程序之前，必须使用[!DNL amxmlc]编译器将MXML代码编译为SWF文件。 [!DNL amxmlc]编译器位于Flex 4或更高版本SDK的[!DNL bin]目录中。 如果需要，您可以设置路径环境变量以包含Flex SDK bin目录，以便更轻松地在命令行上运行实用程序。

请按照以下过程构建Flash Access Manager AIR文件：

1. 打开命令shell或终端，并导航到Flash Access Manager AIR应用程序的项目文件夹(“Reference Implementation”（参考实施）目录中的[!DNL UI Tools\Flash Access Manager]。
1. 输入以下命令：

   ```
   amxmlc src\FlashAccessmanager.mxml
   ```

   运行[!DNL amxmlc]会生成[!DNL FlashAccessManager.swf]，它包含应用程序的编译代码。

Adobe AIR SDK包含用于打包AIR应用程序和生成证书的AIR开发人员工具(ADT)实用程序。 AIR应用程序应进行数字签名；安装未正确签名或完全未签名的应用程序时，用户将收到警告。 要使用命令行生成证书，请打开与AIR应用程序位于同一文件夹中的控制台窗口，然后键入以下内容：

```
adt -certificate -cn SelfSigned 1024-RSA testCert.pfx  
<i class="+ topic ph hi-d="" i "="">
  some_password 
</i class="+ topic>
```

使用您选择的密码替换&#x200B;*some_password*。 几秒钟后，ADT应完成其证书生成过程，您的应用程序目录中应有一个新的[!DNL testCert.pfx]文件。

接下来，使用命令ADT将应用程序打包到[!DNL .air]文件中：

```
adt -package -storetype pkcs12 -keystore testCert.pfx FlashAccessManager.air src\FlashAccessManager-app.xml . -C src assets
```

此命令告知ADT使用[!DNL testCert.pfx]中的键文件打包应用程序。 在上面的一行中，您配置ADT以将您的整个应用程序打包到名为[!DNL FlashAccessManager.air]的文件中，并包括文件[!DNL FlashAccessManager-app.xml]和[!DNL FlashAccessManager.swf]以及资产目录中的图像。

在此过程中，将提示您输入为新证书文件设置的密码。 输入它，等待片刻，[!DNL FlashAccessManager.air]文件应与项目文件显示在同一目录中。
