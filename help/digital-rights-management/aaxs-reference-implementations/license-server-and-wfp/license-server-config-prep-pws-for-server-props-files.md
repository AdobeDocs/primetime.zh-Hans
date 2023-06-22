---
title: 为服务器属性文件准备密码
description: 为服务器属性文件准备密码
copied-description: true
exl-id: 70f75640-7075-450a-8191-dc348bd269b8
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '137'
ht-degree: 0%

---

# 为服务器属性文件准备密码 {#preparing-passwords-for-the-server-properties-files}

为确保凭据密码的安全性，在密码输入到系统之前会提供工具对密码进行加密 [!DNL flashaccess-refimpl.properties] 或 [!DNL flashaccess-refimpl-packager.properties] 文件。

要使用提供的ANT脚本运行该工具，请执行以下操作：

* 转到 *`<Reference Implementation Server Path>`* [!DNL \refimpl]

* 确保 `sdkdir` 中的属性 [!DNL build-refimpl.xml] 指向包含AdobeSDK的目录
* 使用ANT运行以下命令：

   ```
       ant -f build-refimpl.xml
   ```

* 出现提示时，键入凭据的密码

要使用Java运行工具，请执行以下操作：

* 转到 *`<Reference Implementation Server Path>`*\ [!DNL scrambler]

* 在命令提示符下，输入以下命令：

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

该实用程序输出加密的密码，您必须将其复制到.properties文件中。

>[!NOTE]
>
>使用参考实现中提供的密码置乱实用程序编码的密码不能用于Adobe Access Server for Protected Streaming。
