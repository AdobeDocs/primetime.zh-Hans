---
seo-title: 服务器属性文件
title: 服务器属性文件
uuid: 3d3a0ee3-009f-4d62-9587-7e487ecdcafd
translation-type: tm+mt
source-git-commit: 4102780d0c7d0b96d120c1c2b3d14c47bc1b0e6f

---


# 服务器属性文件 {#server-properties-files}

服务器需要两个配置文件，一个用于许可证服务器，一个用于打包程序。 两个文件都必须放在类路径上。 属性文件包含由Adobe发出的凭据的位置。 这些凭据可以指定为。pfx文件和密码，或者通过为存储在HSM上的凭证提供别名和密码来指定。

有关每个参数的特定值和用法的详细信息，请参阅属性文件。 示例属性文件位于引用实现的“资源”目录中(引用Implementation\Server\resources)。

为确保凭据密码的安全性，我们提供了一个工具(CraskUtil.class)，用于在密码输入flashaccess-refimpl.properties或flashaccess-refimpl-packager.properties文件之前对其进行加密。

要正确准备凭据的密码，请执行以下操作：

1. 转到 [!DNL Reference Implementation\Server\refimpl\scrambler]。
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

>[!NOTE] {class=&quot;- topic/note &quot;}
>
>上一个示例使用分号(;)作为分隔符。 对于Microsoft Windows以外的平台，请使用冒号(:)作为分隔符。

该实用程序输出加密密码，您必须将其复制到文 [!DNL .properties] 件中。
