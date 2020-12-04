---
description: 要继续为随Flash媒体Rights Management服务器(FMRMS)1.0或1.5一起打包的内容颁发许可证，您必须将许可证和DRM策略数据从LiveCycleES服务器迁移到基于Adobe PrimetimeDRM SDK的客户新服务器。
seo-description: 要继续为随Flash媒体Rights Management服务器(FMRMS)1.0或1.5一起打包的内容颁发许可证，您必须将许可证和DRM策略数据从LiveCycleES服务器迁移到基于Adobe PrimetimeDRM SDK的客户新服务器。
seo-title: 从FMRMS 1.0或1.5迁移到Adobe PrimetimeDRM 2.0或更高版本
title: 从FMRMS 1.0或1.5迁移到Adobe PrimetimeDRM 2.0或更高版本
uuid: 49ecbbd2-d83b-4bf2-841e-c3f9e5d5e141
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '554'
ht-degree: 0%

---


# 从FMRMS 1.0或1.5迁移到Adobe PrimetimeDRM 2.0或更高版本{#migrate-from-fmrms-or-to-adobe-primetime-drm-or-later}

要继续为随Flash媒体Rights Management服务器(FMRMS)1.0或1.5一起打包的内容颁发许可证，您必须将许可证和DRM策略数据从LiveCycleES服务器迁移到基于Adobe PrimetimeDRM SDK的客户新服务器。

要迁移，请完成以下任务:

1. 导入许可证信息：

   1. 要从LiveCycleES将许可证信息导入基于Primetime DRM的服务器，请参阅[!DNL Reference Implementation\Server\migration\db]文件夹中的示例数据库脚本。
   1. 运行示例脚本，将相关数据从MySQL、Oracle或SQL Server数据库导出为CSV文件格式。
   1. 从LiveCycleES导出数据后，将数据导入到数据库。

      导出的许可证信息包括：

      * 许可证ID
      * 在打包时分配的内容ID
      * 正在应用的DRM策略的ID
      * 内容打包的时间
      * 内容加密密钥

      在将1.x内容元数据转换为Primetime DRM元数据格式之前，需要提供此信息。 在引用实现中，此数据存储在许可证数据库表中，并由`RefImplMetadataConvReqHandler`使用。 有关详细信息，请参阅`FMRMSv1RequestHandler`和`FMRMSv1MetadataHandler`。


1. 将FMRMS策略转换为Primetime DRM格式：

   1. 在应用DRM策略转换元数据并为版本1.0或版本1.5内容颁发许可证之前，请将现有DRM策略转换为Primetime DRM格式。

      `Reference Implementation\Server\migration`文件夹包含创建基于旧DRM策略的Primetime DRM策略的示例代码。 要从FMRMS 1.0迁移到Primetime DRM，请参阅`V1_0PolicyConverter.java`示例。
   1. 通过运行`ant-f build-migration.xml build-1.0-converter`脚本编译示例代码，该脚本搜索[!DNL libs/1.0]和[!DNL libs/flashaccess]目录中的1.0和Primetime DRM库。

   1. 编辑[!DNL converter.properties]文件以指向LiveCycleES服务器。
   1. 运行`ant -f build-migration.xml migrate-all-1.0-policies`将所有FMRMS 1.0 DRM策略转换为Primetime DRM格式。

      要从FMRMS 1.5迁移到Primetime DRM，请参阅`V1_5PolicyConverter.java`示例。

   1. 通过运行`ant-f build-migration.xml build-1.5-converter`脚本编译示例代码，该脚本要求1.5和3.0库位于[!DNL libs/1.5]和[!DNL libs/flashaccess]目录中。

   1. 编辑[!DNL converter.properties]文件以指向LiveCycleES服务器。
   1. 运行`ant -f build-migration.xml migrate-all-1.5-policies`将所有FMRMS 1.5 DRM策略转换为Primetime DRM格式。

      转换的DRM策略将保存为一组文件。 `DRM PolicyConverter`将生成一个CSV格式的文件，其中包括将旧DRM策略ID映射到新DRM策略ID。 可以将此文件导入到引用实现数据库中的[!DNL PolicyConversion]表，其中`RefImplMetadataConvReqHandler`使用此文件。

1. 支持`FMRMSv1RequestHandler`和`FMRMSv1MetadataHandler`属性的1.x兼容性请求：

   1. 相关数据迁移到基于Primetime DRM的服务器后，实现对1.x兼容性请求的支持。

      有关如何处理这些类型请求的示例，请参见参考实现中的`RefImplUpgradeV1ClientHandler`和`RefImplMetadataConvReqHandler`。

