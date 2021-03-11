---
title: 服务器属性文件
description: 服务器属性文件
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '182'
ht-degree: 0%

---


# 服务器属性文件{#server-properties-files}

服务器需要两个配置文件，一个用于许可证服务器，一个用于打包程序。 必须将两个文件都放在类路径上。 属性文件包含由Adobe发出的凭据的位置。 这些凭据可以指定为.pfx文件和密码，或通过为存储在HSM上的凭据提供别名和密码来指定。

有关每个参数的特定值和用法的详细信息，请参阅属性文件。 示例属性文件位于引用实现的“资源”目录(引用Implementation\Server\resources)中。

为确保凭据密码的安全性，会提供一个工具(ScrapyUtil.class)，用于在密码输入flashaccess-refimpl.properties或flashaccess-refimpl-packager.properties文件之前对其进行加密。

要正确准备凭据密码，请执行以下操作：

1. 转到[!DNL Reference Implementation\Server\refimpl\scrambler]。
1. 在命令提示符下，输入命令：

   ```
   java -classpath  
   <i class="+ topic ph hi-d="" i "="">
   path_to_adobe-flashaccess-sdk.jar.; 
        com.adobe.flashaccess.refimpl.util.ScrambleUtil " 
   <i class="+ topic ph hi-d="" i "="">
   your_pfx_password" 
   </i class="+ topic> 
   </i class="+ topic>
   ```

>[!NOTE]
>
>上例使用分号(;)作为分隔符。 对于Microsoft Windows以外的平台，请使用冒号(:)作为分隔符。

该实用程序输出加密密码，您必须将其复制到[!DNL .properties]文件。
