---
seo-title: 为服务器属性文件准备口令
title: 为服务器属性文件准备口令
uuid: 2d876eb0-b1a5-4c30-ae96-0a22f6a03910
translation-type: tm+mt
source-git-commit: 7e8df034035fe465fbe403949ef828e7811ced2e
workflow-type: tm+mt
source-wordcount: '137'
ht-degree: 0%

---


# 准备服务器属性文件{#preparing-passwords-for-the-server-properties-files}的密码

为确保凭据密码的安全性，在将密码输入[!DNL flashaccess-refimpl.properties]或[!DNL flashaccess-refimpl-packager.properties]文件之前，会提供一个工具来加密密码。

要使用提供的ANT脚本运行该工具：

* 转到&#x200B;*`<Reference Implementation Server Path>`* [!DNL \refimpl]

* 确保[!DNL build-refimpl.xml]中的`sdkdir`属性指向包含Adobe访问SDK的目录
* 使用ANT运行以下命令：

   ```
       ant -f build-refimpl.xml
   ```

* 出现提示时，键入凭据的口令

要使用Java运行工具，请执行以下操作：

* 转至&#x200B;*`<Reference Implementation Server Path>`*\ [!DNL scrambler]

* 在命令提示符下，输入命令：

* 在Windows上：

   ```
   java -classpath path_to_adobe-flashaccess-sdk.jar;.  
   com.adobe.flashaccess.refimpl.util.ScrambleUtil your_pfx_password
   ```

* 在Linux上：

   ```
       java -classpath path_to_adobe-flashaccess-sdk.jar;.  
       com.adobe.flashaccess.refimpl.util.ScrambleUtil your_pfx_password
   ```

实用程序将输出加密密码，您必须将其复制到。properties文件。

>[!NOTE]
>
>使用随参考实现提供的密码加扰实用程序编码的密码将无法与Adobe Access Server的受保护流应用程序一起使用。
