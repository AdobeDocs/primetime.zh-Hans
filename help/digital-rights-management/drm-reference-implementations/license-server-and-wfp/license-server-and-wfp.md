---
description: 参考实施服务器可以帮助您创建使用Adobe Primetime DRM Java SDK所有功能的全功能许可证服务器。
title: 许可证服务器
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '269'
ht-degree: 0%

---

# 许可证服务器 {#license-server}

参考实施服务器可以帮助您创建使用Adobe Primetime DRM Java SDK所有功能的全功能许可证服务器。

在此实现中，基于数据库中的用户条目对用户进行身份验证。 服务器包括用于颁发许可证的演示业务逻辑，并为Flash介质Rights Management服务器1.0和1.5提供兼容性支持。

## 许可证服务器要求 {#license-server-requirements}

许可证服务器要求：

* 安装Tomcat 6.0或更高版本
* 安装数据库，例如MySQL(可在DVD上获得，位于 [!DNL Third Party\MySQL])
* 确保您已安装Java 1.6或更高版本
* 要运行示例生成脚本，请确保您具有Ant 1.8或更高版本

安装Tomcat和MySQL后，请联系Adobe以获取所需的DRM凭据集。

## 构建许可证服务器 {#build-the-license-server}

>[!NOTE]
>
>仅当要修改源代码时，才需要构建许可证服务器。 出于评估目的，您只需将WAR文件作为已发运文件使用。

参考实施许可证服务器包括所有许可证服务器源代码( `([DRM SDK DVD]\Reference Implementation\Server\Reference Implementation Server\src/`)，以及Ant生成脚本( `[DRM SDK DVD]\Reference Implementation\Server\Reference Implementation Server\refimpl/build-refimpl.xml`)，您可以根据业务需要自定义许可证服务器。

1. 修改Ant生成脚本以指定Primetime DRM SDK、Tomcat、MySQL和Log4J的位置。

   打开 [!DNL build-refimpl.xml] 文件，并设置以下属性值：

   * `sdkdir`
   * `tomcatdir`
   * `mysqldir`
   * `log4jdir`

1. 运行Ant生成脚本 `all` 属性，位于Ant生成脚本所在的目录中。

   ```
   ant -f build-refimpl.xml all
   ```

   Ant生成脚本将创建 [!DNL refimpl-build/wars] 包含服务器WAR文件的目录。
