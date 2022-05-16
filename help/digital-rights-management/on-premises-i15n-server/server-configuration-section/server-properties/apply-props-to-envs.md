---
description: '必须配置服务器属性才能反映您的环境。 您可以使用以下任一方法执行此操作 '
title: 将属性应用到服务器环境
exl-id: 0c78011a-e8c8-43a8-8c2d-a5c4ed54a8d7
source-git-commit: 0019a95fa9ca6d21249533d559ce844897ab67cf
workflow-type: tm+mt
source-wordcount: '249'
ht-degree: 0%

---

# 将属性应用到服务器环境{#apply-properties-to-server-environments}

必须配置服务器属性才能反映您的环境。 您可以使用以下任一方法执行此操作：

* [!DNL flashaccess-i15n.properties]  — 每个 [!DNL .war] 文件

* [!DNL AdobeInitial.properties]  — 位于 [!DNL /shared] 文件夹

   您可以使用此文件覆盖WAR文件中设置的属性，如下所示：

   1. 在 [!DNL AdobeInitial.properties]
   1. 位置 [!DNL AdobeInitial.properties] 类路径上。

   >[!NOTE]
   >
   >Adobe建议您使用 [!DNL AdobeInitial.properties] 文件，因为这样，您就可以更新应用程序WAR文件，而不会丢失您可能在 [!DNL flashaccess-i15n.properties] 文件。

* Java系统属性机制。

您可以将单个属性应用到以下特定服务器环境：

* *开发*
* *暂存*
* *生产*

使用此功能，您可以对所有服务器环境使用相同的WAR文件。 要将属性应用于特定环境，请附加两个下划线字符(“ `__`&#39;)加上资产的以下环境代码之一 *name*:

* `DEV`
* `STAGE`
* `PROD`

<!--<a id="example_A7A58E3EE8DA4114B4F7A9EEB69D50CA"></a>-->

例如，将日志级别设置为 `INFO` 和 `DEBUG` 对于您的开发服务器：

```
log.Level=INFO  
log.Level__DEV=DEBUG 
```

服务器对属性使用此搜索顺序：

1. `propertyname_environment` in [!DNL AdobeInitial.properties]

1. `propertyname_environment` in [!DNL flashaccess-15n.properties]

1. `propertyname_environment` 在Java系统属性中
1. `propertyname` in [!DNL AdobeInitial.properties]

1. `propertyname` in [!DNL flashaccess-15n.properties]

1. `propertyname` 在Java系统属性中

>[!NOTE]
>
>启动服务器时，必须将服务器的环境名称指定为Java系统属性。 例如，在以 [!DNL catalina.bat]，请设置 `CATALINA_OPTS` 环境变量如下所示：
>-DENVIRONMENT_NAME=[ 开发 |暂存 | PROD ]
