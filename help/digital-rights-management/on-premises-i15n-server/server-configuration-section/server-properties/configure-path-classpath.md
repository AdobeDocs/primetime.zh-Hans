---
seo-title: 配置路径和类路径
title: 配置路径和类路径
uuid: cf10fafa-125e-450c-83ae-60b990dab6b5
translation-type: tm+mt
source-git-commit: d8e4c39c297d69b154baf0b4d67cf09b5cf0a9d4

---


# 配置路径和类路径{#configure-the-path-and-classpath}

包 [!DNL flashaccess.war] 含 [!DNL jsafeWithNative.jar]的是Crypto-J库。 后者需要额外的本机库来执行加密操作。

1. 将本机库 [!DNL jsafe] 添加到路径中。

   * **Linux /[!DNL libjsafe.so]-** 包含路径的目 [!DNL libjsafe.so] 录必须位于路径中（本机Crypto-J库也可用于其他平台）。 例如，设置 [!DNL libjsafe.so] 为开 `LD_LIBRARY_PATH`。

   * **Windows /[!DNL jsafe.dll]-** Windows上的对应项 [!DNL libjsafe.so] 是适当的 [!DNL jsafe.dll]。
   这些库位于库文件夹 [!DNL thirdparty] 中。
1. 将一个jar文 [!DNL adobe-flashaccess-certs] 件放在类路径上。

       此JAR文件不包含在WAR文件中；必须将其显式添加到类路径中。
   
   * 开发服务器——应仅使用 [!DNL adobe-flashaccess-certs-prerelease.jar]。
   * 生产服务器——应仅使用 [!DNL adobe-flashaccess- certs.jar]

分发包含一 [!DNL shared] 个文件夹，其中既包括jar文件，也包括预配置的文 [!DNL AdobeInitial.properties] 件。 Adobe建议您通过文件将这些项目 `common.loader` 添加到 [!DNL catalina.properties] 中。 例如：

```
common.loader=<Any Pre-Existing Values>,${catalina.home}/shared/classes,${catalina.home}/shared/lib/*.jar
```


