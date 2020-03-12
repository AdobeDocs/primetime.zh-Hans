---
description: '您必须配置服务器属性以反映您的环境。 您可以使用以下任意一种方式执行此操作 '
seo-description: '您必须配置服务器属性以反映您的环境。 您可以使用以下任意一种方式执行此操作 '
seo-title: 将属性应用于服务器环境
title: 将属性应用于服务器环境
uuid: a1ee0d6c-b5e7-4689-b7c8-b155176faf1c
translation-type: tm+mt
source-git-commit: d8e4c39c297d69b154baf0b4d67cf09b5cf0a9d4

---


# 将属性应用于服务器环境{#apply-properties-to-server-environments}

您必须配置服务器属性以反映您的环境。 您可以使用以下任意一种方式执行此操作：

* [!DNL flashaccess-i15n.properties] -每个文件中包含的示 [!DNL .war] 例

* [!DNL AdobeInitial.properties] -示例位于DVD [!DNL /shared] 上的文件夹中

   您可以使用此文件覆盖在WAR文件中设置的属性，如下所示：

   1. 在 [!DNL AdobeInitial.properties]
   1. 放在 [!DNL AdobeInitial.properties] 类路径上。
   >[!NOTE]
   >
   >Adobe建议您使用该文件，因为这样，您就可以更新应用程序WAR文件，而不会丢失您在文件中可能完成的任何以前的属性配置设置的 [!DNL AdobeInitial.properties][!DNL flashaccess-i15n.properties] 风险。

* Java System属性机制。

您可以将单个属性应用到这些特定的服务器环境：

* *开发*
* *暂存*
* *制作*

利用此功能，您可以对所有服务器环境使用相同的WAR文件。 要将属性应用到特定环境，请在属性名称后面附加两个下划线字符(&#39; `__`&#39;)，并加上下列环境代码之 *一*:

    * “DEV”
    * “STAGE”
    * “PROD”

<!--<a id="example_A7A58E3EE8DA4114B4F7A9EEB69D50CA"></a>-->

例如，要将生产和分阶段服务 `INFO` 器的日志级别设置为，以及将开发服 `DEBUG` 务器的日志级别设置为：

```
log.Level=INFO  
log.Level__DEV=DEBUG 
```

服务器对属性采用以下搜索顺序：

1. `propertyname_environment` in [!DNL AdobeInitial.properties]

1. `propertyname_environment` in [!DNL flashaccess-15n.properties]

1. `propertyname_environment` 在Java系统属性中
1. `propertyname` in [!DNL AdobeInitial.properties]

1. `propertyname` in [!DNL flashaccess-15n.properties]

1. `propertyname` 在Java系统属性中

>[!NOTE]
>
>启动服务器时，必须将服务器的环境名称指定为Java System属性。 例如，在将Tomcat启动时， [!DNL catalina.bat]请按如下 `CATALINA_OPTS` 方式设置环境变量：
>-DENVIRONMENT_NAME=[ DEV| STAGE| PROD ]
