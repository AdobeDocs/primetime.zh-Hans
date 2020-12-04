---
description: '您必须配置服务器属性以反映您的环境。 您可以使用以下任意方式执行此操作 '
seo-description: '您必须配置服务器属性以反映您的环境。 您可以使用以下任意方式执行此操作 '
seo-title: 将属性应用于服务器环境
title: 将属性应用于服务器环境
uuid: a1ee0d6c-b5e7-4689-b7c8-b155176faf1c
translation-type: tm+mt
source-git-commit: d8e4c39c297d69b154baf0b4d67cf09b5cf0a9d4
workflow-type: tm+mt
source-wordcount: '275'
ht-degree: 0%

---


# 将属性应用于服务器环境{#apply-properties-to-server-environments}

您必须配置服务器属性以反映您的环境。 您可以使用以下任一方式执行此操作：

* [!DNL flashaccess-i15n.properties] -每个文件中包含的示 [!DNL .war] 例

* [!DNL AdobeInitial.properties] -示例位于DVD [!DNL /shared] 上的文件夹中

   您可以使用此文件覆盖在WAR文件中设置的属性，如下所示：

   1. 在[!DNL AdobeInitial.properties]中设置覆盖属性值
   1. 将[!DNL AdobeInitial.properties]放在类路径上。

   >[!NOTE]
   >
   >Adobe建议您使用[!DNL AdobeInitial.properties]文件，因为这样，您就可以更新应用程序WAR文件，而不会丢失您在[!DNL flashaccess-i15n.properties]文件中执行的任何以前的属性配置设置。

* Java System属性机制。

您可以将单个属性应用到这些特定服务器环境:

* *开发*
* *暂存*
* *制作*

利用此功能，您可以对所有服务器环境使用同一WAR文件。 要将属性应用于特定环境，请在属性&#x200B;*名称*&#x200B;后面附加两个下划线字符(“`__`”)，并加上以下环境代码之一：

    * “DEV
    ”* “STAGE
    ”* “PROD”

<!--<a id="example_A7A58E3EE8DA4114B4F7A9EEB69D50CA"></a>-->

例如，要将生产和分阶段服务器的日志级别设置为`INFO`，将开发服务器的日志级别设置为`DEBUG`:

```
log.Level=INFO  
log.Level__DEV=DEBUG 
```

服务器对属性采用以下搜索顺序：

1. `propertyname_environment` in  [!DNL AdobeInitial.properties]

1. `propertyname_environment` in  [!DNL flashaccess-15n.properties]

1. `propertyname_environment` 在Java系统属性中
1. `propertyname` in  [!DNL AdobeInitial.properties]

1. `propertyname` in  [!DNL flashaccess-15n.properties]

1. `propertyname` 在Java系统属性中

>[!NOTE]
>
>启动服务器时，必须将服务器的环境名称指定为Java系统属性。 例如，在以[!DNL catalina.bat]启动Tomcat时，按如下方式设置`CATALINA_OPTS`环境变量：
>-DENVIRONMENT_NAME=[开发 | STAGE | PROD ]
