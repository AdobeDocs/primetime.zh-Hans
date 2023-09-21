---
description: 必须配置服务器属性以反映环境。 您可以使用以下任一方式执行此操作
title: 将属性应用于服务器环境
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '249'
ht-degree: 0%

---

# 将属性应用于服务器环境{#apply-properties-to-server-environments}

必须配置服务器属性以反映环境。 您可以使用以下任一方式执行此操作：

* [!DNL flashaccess-i15n.properties]  — 包含于每份 [!DNL .war] 文件

* [!DNL AdobeInitial.properties]  — 位于 [!DNL /shared] DVD上的文件夹

  您可以使用此文件覆盖WAR文件中设置的属性，如下所示：

   1. 在中设置覆盖属性值 [!DNL AdobeInitial.properties]
   1. 地标 [!DNL AdobeInitial.properties] 在类路径上。

  >[!NOTE]
  >
  >Adobe建议您使用 [!DNL AdobeInitial.properties] 文件，因此您可以更新应用程序WAR文件，而不会丢失之前在 [!DNL flashaccess-i15n.properties] 文件。

* Java系统属性机制。

您可以将单个属性应用于这些特定的服务器环境：

* *开发*
* *暂存*
* *生产*

利用此功能，您可以对所有服务器环境使用相同的WAR文件。 要将属性应用于特定环境，请附加两个下划线字符(&#39; `__`&#39;)加上属性中的以下环境代码之一 *name*：

* `DEV`
* `STAGE`
* `PROD`

<!--<a id="example_A7A58E3EE8DA4114B4F7A9EEB69D50CA"></a>-->

例如，要将日志级别设置为 `INFO` 用于生产和暂存服务器，以及 `DEBUG` 对于开发服务器：

```
log.Level=INFO  
log.Level__DEV=DEBUG 
```

服务器对属性采用以下搜索顺序：

1. `propertyname_environment` 在 [!DNL AdobeInitial.properties]

1. `propertyname_environment` 在 [!DNL flashaccess-15n.properties]

1. `propertyname_environment` 在Java系统属性中
1. `propertyname` 在 [!DNL AdobeInitial.properties]

1. `propertyname` 在 [!DNL flashaccess-15n.properties]

1. `propertyname` 在Java系统属性中

>[!NOTE]
>
>启动服务器时，必须将服务器的环境名称指定为Java System属性。 例如，在启动Tomcat时 [!DNL catalina.bat]，设置 `CATALINA_OPTS` 环境变量，如下所示：
>-DENVIRONMENT_NAME=[开发 |暂存 |生产]
