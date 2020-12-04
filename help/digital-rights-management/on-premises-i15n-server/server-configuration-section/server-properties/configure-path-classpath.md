---
seo-title: 配置路径和类路径
title: 配置路径和类路径
uuid: cf10fafa-125e-450c-83ae-60b990dab6b5
translation-type: tm+mt
source-git-commit: d8e4c39c297d69b154baf0b4d67cf09b5cf0a9d4
workflow-type: tm+mt
source-wordcount: '149'
ht-degree: 1%

---


# 配置路径和类路径{#configure-the-path-and-classpath}

[!DNL flashaccess.war]包含[!DNL jsafeWithNative.jar]，它是Crypto-J库。 后者需要额外的本机库来执行加密操作。

1. 将本机[!DNL jsafe]库添加到路径中。

   * **Linux /  [!DNL libjsafe.so] -** 包含 [!DNL libjsafe.so] 路径的目录必须位于路径中（本机Crypto-J库也可用于其他平台）。例如，在`LD_LIBRARY_PATH`上设置[!DNL libjsafe.so]。

   * **Windows/- [!DNL jsafe.dll] Windows** 上的对应项 [!DNL libjsafe.so] 是适当的 [!DNL jsafe.dll]。
   这些库位于[!DNL thirdparty]库文件夹中。
1. 将[!DNL adobe-flashaccess-certs] jar文件之一放在类路径上。

       此JAR文件未包含在WAR文件中；必须将其显式添加到类路径中。
   
   * 开发服务器——应仅使用[!DNL adobe-flashaccess-certs-prerelease.jar]。
   * 生产服务器——应仅使用[!DNL adobe-flashaccess- certs.jar]

该分发包含[!DNL shared]文件夹，其中既包括jar文件，也包括预配置的[!DNL AdobeInitial.properties]文件。 Adobe建议通过[!DNL catalina.properties]文件将这些项目添加到`common.loader`。 例如：

```
common.loader=<Any Pre-Existing Values>,${catalina.home}/shared/classes,${catalina.home}/shared/lib/*.jar
```


