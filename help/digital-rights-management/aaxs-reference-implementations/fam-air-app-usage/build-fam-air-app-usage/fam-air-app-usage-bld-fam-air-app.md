---
seo-title: 构建Flash Access Manager AIR应用程序
title: 构建Flash Access Manager AIR应用程序
uuid: 00927eb3-b8eb-4dd4-b528-91b70760c8cd
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# 构建Flash Access Manager AIR应用程序 {#building-the-flash-access-manager-air-application}

要从源代码构建Flash Access Manager AIR文件，您需要在计算机上安装Flex和AIR SDK。 在打包并运行应用程序之前，必须使用编译器将MXML代码编译为SWF文 [!DNL amxmlc] 件。 编译 [!DNL amxmlc] 器位于Flex 4或更 [!DNL bin] 高版本SDK的目录中。 如果需要，您可以将路径环境变量设置为包含Flex SDK bin目录，以便更轻松地在命令行运行实用程序。

请按照以下过程构建Flash Access Manager AIR文件：

1. 打开命令shell或终端，然后导航到Flash Access Manager AIR应用程序的项目文件夹(在“参 [!DNL UI Tools\Flash Access Manager] 考实施”目录中)。
1. 输入以下命令：

   ```
   amxmlc src\FlashAccessmanager.mxml
   ```

   运 [!DNL amxmlc] 行生 [!DNL FlashAccessManager.swf]成，它包含应用程序的编译代码。

Adobe AIR SDK包含AIR Developer Tool(ADT)实用程序，用于打包AIR应用程序和生成证书。 AIR应用程序应进行数字签名；在安装未正确签名或完全未签名的应用程序时，用户将收到警告。 要使用命令行生成证书，请打开与AIR应用程序位于同一文件夹中的控制台窗口，然后键入以下内容：

```
adt -certificate -cn SelfSigned 1024-RSA testCert.pfx  
<i class="+ topic ph hi-d="" i "="">
  some_password 
</i class="+ topic>
```

使用 *您选择的口令替换some_password* 。 几秒钟后，ADT应完成其证书生成过程，并且您应在应用程序目 [!DNL testCert.pfx] 录中有一个新文件。

接下来，使用命令ADT将应用程序打 [!DNL .air] 包到文件中：

```
adt -package -storetype pkcs12 -keystore testCert.pfx FlashAccessManager.air src\FlashAccessManager-app.xml . -C src assets
```

此命令告知ADT使用中的键文件打包应用程序 [!DNL testCert.pfx]。 在上面的行中，您配置ADT以将整个应用程序打包到一个名为的文件中 [!DNL FlashAccessManager.air]，并包含来自资源目录的 [!DNL FlashAccessManager-app.xml][!DNL FlashAccessManager.swf] 文件和图像。

在此过程中，系统将提示您输入为新证书文件设置的密码。 输入它，等等，文件应 [!DNL FlashAccessManager.air] 该显示在与项目文件相同的目录中。
