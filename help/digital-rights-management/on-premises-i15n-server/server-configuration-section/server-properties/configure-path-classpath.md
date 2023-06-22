---
title: 配置路径和类路径
description: 配置路径和类路径
copied-description: true
exl-id: e6e9f837-4e3d-43e1-971d-3fa0ccaeff39
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '149'
ht-degree: 0%

---

# 配置路径和类路径{#configure-the-path-and-classpath}

此 [!DNL flashaccess.war] 包含 [!DNL jsafeWithNative.jar]，即Crypto-J库。 后者需要额外的本机库来执行加密操作。

1. 添加本机 [!DNL jsafe] 库到您的路径。

   * **Linux / [!DNL libjsafe.so] -** 包含的目录 [!DNL libjsafe.so] 必须位于路径上（本机加密J库也可用于其他平台）。 例如，设置 [!DNL libjsafe.so] 日期 `LD_LIBRARY_PATH`.

   * **Windows / [!DNL jsafe.dll] -** Windows上的对应项 [!DNL libjsafe.so] 是否合适 [!DNL jsafe.dll].
   您可以在以下位置使用这些库： [!DNL thirdparty] 库文件夹。
1. 放一个 [!DNL adobe-flashaccess-certs] 类路径上的jar文件。

       此JAR文件未包含在WAR文件中；必须将其显式添加到类路径中。
   
   * 开发服务器 — 应仅使用 [!DNL adobe-flashaccess-certs-prerelease.jar].
   * 生产服务器 — 应仅使用 [!DNL adobe-flashaccess- certs.jar]

该分布包括 [!DNL shared] 包含jar文件以及预配置的文件夹 [!DNL AdobeInitial.properties] 文件。 Adobe建议将这些项目添加到 `common.loader` 通过 [!DNL catalina.properties] 文件。 例如：

```
common.loader=<Any Pre-Existing Values>,${catalina.home}/shared/classes,${catalina.home}/shared/lib/*.jar
```
