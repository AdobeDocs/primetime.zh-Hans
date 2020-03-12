---
description: 参考实施服务器可以帮助您创建一个使用Adobe Primetime DRM Java SDK的所有功能的全功能许可证服务器。
seo-description: 参考实施服务器可以帮助您创建一个使用Adobe Primetime DRM Java SDK的所有功能的全功能许可证服务器。
seo-title: 许可证服务器
title: 许可证服务器
uuid: 39cb0d0f-f3dc-48e9-b6fd-6960a9ade291
translation-type: tm+mt
source-git-commit: 4102780d0c7d0b96d120c1c2b3d14c47bc1b0e6f

---


# 许可证服务器 {#license-server}

参考实施服务器可以帮助您创建一个使用Adobe Primetime DRM Java SDK的所有功能的全功能许可证服务器。

在该实现中，根据数据库中的用户条目对用户进行身份验证。 该服务器包括用于颁发许可证的演示业务逻辑，并提供对Flash Media Rights Management Server 1.0和1.5的兼容性支持。

## 许可证服务器要求 {#license-server-requirements}

许可证服务器要求：

* 安装Tomcat 6.0或更高版本
* 安装数据库，例如MySQL(在DVD上提供 [!DNL Third Party\MySQL])
* 确保您已安装Java 1.6或更高版本
* 要运行示例构建脚本，请确保您有Ant 1.8或更高版本

安装Tomcat和MySQL后，请与Adobe联系以获取所需的DRM凭据集。

## 构建许可证服务器 {#build-the-license-server}

>[!NOTE] {class=&quot;- topic/note &quot;}
>
>仅当您要修改源代码时，才需要构建许可证服务器。 为便于评估，您只需使用随附的WAR文件。

参考实施许可证服务器包括所有许可证服务器源代码( `([DRM SDK DVD]\Reference Implementation\Server\Reference Implementation Server\src/`)，以及Ant构建脚本( `[DRM SDK DVD]\Reference Implementation\Server\Reference Implementation Server\refimpl/build-refimpl.xml`)，您可以使用该脚本自定义许可证服务器以满足您的业务需求。

1. 修改Ant构建脚本以指定Primetime DRM SDK、Tomcat、MySQL和Log4J的位置。

   在文本 [!DNL build-refimpl.xml] 编辑器中打开文件并设置以下属性值：

   * `sdkdir`
   * `tomcatdir`
   * `mysqldir`
   * `log4jdir`

1. 在Ant构建脚本所在的 `all` 目录中，使用属性运行Ant构建脚本。

   ```
   ant -f build-refimpl.xml all
   ```

   Ant构建脚本创建包 [!DNL refimpl-build/wars] 含服务器WAR文件的目录。
