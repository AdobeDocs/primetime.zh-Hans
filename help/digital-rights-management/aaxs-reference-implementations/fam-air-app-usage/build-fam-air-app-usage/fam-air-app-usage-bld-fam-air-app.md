---
title: 构建Flash Access管理器AIR应用程序
description: 构建Flash Access管理器AIR应用程序
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '349'
ht-degree: 0%

---

# 构建Flash Access管理器AIR应用程序 {#building-the-flash-access-manager-air-application}

要从源代码构建Flash Access管理器AIR文件，您需要在计算机上安装Flex和AIR SDK。 MXML SWF在打包和运行应用程序之前，您必须使用 [!DNL amxmlc] 编译器。 此 [!DNL amxmlc] 编译器位于 [!DNL bin] Flex 4或更高版本SDK的目录。 如果需要，您可以设置路径环境变量以包含Flex SDK bin目录，以便更轻松地在命令行上运行实用程序。

使用以下过程构建Flash Access管理器AIR文件：

1. 打开命令shell或终端，然后导航到Flash Access管理器AIR应用程序的项目文件夹( [!DNL UI Tools\Flash Access Manager] （在“参考实施”目录中）。
1. 输入以下命令：

   ```
   amxmlc src\FlashAccessmanager.mxml
   ```

   正在运行 [!DNL amxmlc] 生成 [!DNL FlashAccessManager.swf]，其中包含应用程序的编译代码。

Adobe AIR SDK包含AIR Developer Tool (ADT)实用程序，可用于打包AIR应用程序并生成证书。 AIR应用程序应该进行数字签名；用户在安装未正确签名或完全未签名的应用程序时会收到警告。 要使用命令行生成证书，请打开与AIR应用程序位于同一文件夹中的控制台窗口，然后键入以下内容：

```
adt -certificate -cn SelfSigned 1024-RSA testCert.pfx  
<i class="+ topic ph hi-d="" i "="">
  some_password 
</i class="+ topic>
```

替换 *some_password* 选择密码。 几秒钟后，ADT应完成其证书生成过程，并且您应具有新的 [!DNL testCert.pfx] 文件创建路径。

接下来，使用ADT将应用程序打包到 [!DNL .air] 文件，使用命令：

```
adt -package -storetype pkcs12 -keystore testCert.pfx FlashAccessManager.air src\FlashAccessManager-app.xml . -C src assets
```

此命令告知ADT使用中的密钥文件打包您的应用程序 [!DNL testCert.pfx]. 在上面的行中，您可以配置ADT以将整个应用程序打包到一个名为的文件中 [!DNL FlashAccessManager.air]，并包含文件 [!DNL FlashAccessManager-app.xml] 和 [!DNL FlashAccessManager.swf] 和assets目录中的图像。

在此过程中，将提示您输入为新证书文件设置的密码。 进入，等一下，然后 [!DNL FlashAccessManager.air] 文件应与项目文件显示在同一目录中。
