---
title: 配置路径和类路径
description: 配置路径和类路径
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '149'
ht-degree: 1%

---


# 配置路径和类路径{#configure-the-path-and-classpath}

[!DNL flashaccess.war]包含[!DNL jsafeWithNative.jar]，该库是Crypto-J库。 后者需要额外的本机库来执行加密操作。

1. 将本机[!DNL jsafe]库添加到路径中。

   * **Linux/- [!DNL libjsafe.so] 包** 含的目 [!DNL libjsafe.so] 录必须位于路径上（本机Crypto-J库也可用于其他平台）。例如，在`LD_LIBRARY_PATH`上设置[!DNL libjsafe.so]。

   * **Windows/- [!DNL jsafe.dll] Windows** 上的对应项 [!DNL libjsafe.so] 是合适的 [!DNL jsafe.dll]。
   这些库位于[!DNL thirdparty]库文件夹中。
1. 将[!DNL adobe-flashaccess-certs] jar文件之一放在类路径上。

       此JAR文件未包含在WAR文件中；必须将其显式添加到类路径中。
   
   * 开发服务器 — 应仅使用[!DNL adobe-flashaccess-certs-prerelease.jar]。
   * 生产服务器 — 应仅使用[!DNL adobe-flashaccess- certs.jar]

分发包括[!DNL shared]文件夹，其中既包括jar文件，也包括预配置的[!DNL AdobeInitial.properties]文件。 Adobe建议您通过[!DNL catalina.properties]文件将这些项目添加到`common.loader`。 例如：

```
common.loader=<Any Pre-Existing Values>,${catalina.home}/shared/classes,${catalina.home}/shared/lib/*.jar
```


