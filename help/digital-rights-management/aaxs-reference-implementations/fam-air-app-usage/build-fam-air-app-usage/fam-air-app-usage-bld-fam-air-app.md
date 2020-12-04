---
seo-title: 构建Flash Access管理器AIR应用程序
title: 构建Flash Access管理器AIR应用程序
uuid: 00927eb3-b8eb-4dd4-b528-91b70760c8cd
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '349'
ht-degree: 0%

---


# 构建Flash Access管理器AIR应用程序{#building-the-flash-access-manager-air-application}

要从源代码构建Flash Access管理器AIR文件，您需要在计算机上安装Flex和AIR SDK。 在打包并运行应用程序之前，必须使用[!DNL amxmlc]编译器将MXML代码编译为SWF文件。 [!DNL amxmlc]编译器可在Flex4或更高版本的SDK的[!DNL bin]目录中找到。 如果需要，可以将路径环境变量设置为包含FlexSDK bin目录，以便更轻松地在命令行运行实用程序。

请按照以下过程构建Flash Access管理器AIR文件：

1. 打开命令外壳程序或终端并导航到Flash Access管理器AIR应用程序的项目文件夹（“Reference Implementation”目录中的[!DNL UI Tools\Flash Access Manager]）。
1. 输入以下命令：

   ```
   amxmlc src\FlashAccessmanager.mxml
   ```

   运行[!DNL amxmlc]会生成[!DNL FlashAccessManager.swf]，它包含应用程序的编译代码。

Adobe AIRSDK包含AIR开发人员工具(ADT)实用程序，用于打包AIR应用程序和生成证书。 AIR应用程序应进行数字签名；安装未正确签名或完全未签名的应用程序时，用户将收到警告。 要使用命令行生成证书，请打开与AIR应用程序位于同一文件夹中的控制台窗口并键入以下内容：

```
adt -certificate -cn SelfSigned 1024-RSA testCert.pfx  
<i class="+ topic ph hi-d="" i "="">
  some_password 
</i class="+ topic>
```

使用您选择的密码替换&#x200B;*some_password*。 几秒钟后，ADT应完成其证书生成过程，您的应用程序目录中应有一个新的[!DNL testCert.pfx]文件。

接下来，使用ADT命令将应用程序打包到[!DNL .air]文件中：

```
adt -package -storetype pkcs12 -keystore testCert.pfx FlashAccessManager.air src\FlashAccessManager-app.xml . -C src assets
```

此命令告知ADT使用[!DNL testCert.pfx]中的键文件打包应用程序。 在上面的一行中，您配置ADT将整个应用程序打包到名为[!DNL FlashAccessManager.air]的文件中，并包含文件[!DNL FlashAccessManager-app.xml]和[!DNL FlashAccessManager.swf]以及资产目录中的图像。

在此过程中，将提示您输入为新证书文件设置的密码。 输入它，稍候，[!DNL FlashAccessManager.air]文件应显示在与项目文件相同的目录中。
