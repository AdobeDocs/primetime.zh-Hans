---
description: 要继续为已与Flash媒体Rights Management服务器(FMRMS) 1.0或1.5打包的内容颁发许可证，您必须将许可证和DRM策略数据从LiveCycleES服务器迁移到客户基于Adobe Primetime DRM SDK的新服务器。
title: 从FMRMS 1.0或1.5迁移到Adobe Primetime DRM 2.0或更高版本
exl-id: 6490f2ad-4863-4b41-9ebd-1de47da4250b
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '499'
ht-degree: 0%

---

# 从FMRMS 1.0或1.5迁移到Adobe Primetime DRM 2.0或更高版本{#migrate-from-fmrms-or-to-adobe-primetime-drm-or-later}

要继续为已与Flash媒体Rights Management服务器(FMRMS) 1.0或1.5打包的内容颁发许可证，您必须将许可证和DRM策略数据从LiveCycleES服务器迁移到客户基于Adobe Primetime DRM SDK的新服务器。

要迁移，请完成以下任务：

1. 导入许可证信息：

   1. 要将许可证信息从LiveCycleES导入基于Primetime DRM的服务器，请参阅 [!DNL Reference Implementation\Server\migration\db] 文件夹。
   1. 运行示例脚本，将相关数据从MySQL、Oracle或SQL Server数据库导出为CSV文件格式。
   1. 从LiveCycleES导出数据后，将数据导入数据库。

      导出的许可证信息包括：

      * 许可证ID
      * 打包时分配的内容ID
      * 正在应用的DRM策略的ID
      * 打包内容的时间
      * 内容加密密钥

      在将1.x内容元数据转换为Primetime DRM元数据格式之前，需要提供此信息。 在参考实现中，此数据存储在许可证数据库表中，并由以下人员使用 `RefImplMetadataConvReqHandler`. 有关更多信息，请参阅 `FMRMSv1RequestHandler` 和 `FMRMSv1MetadataHandler`.


1. 将FMRMS策略转换为Primetime DRM格式：

   1. 在应用DRM策略转换元数据并颁发版本1.0或版本1.5内容的许可证之前，请将现有DRM策略转换为Primetime DRM格式。

      此 `Reference Implementation\Server\migration` 文件夹中包含用于创建基于旧版DRM策略的Primetime DRM策略的示例代码。 要从FMRMS 1.0迁移到Primetime DRM，请参阅 `V1_0PolicyConverter.java` 示例。
   1. 通过运行编译示例代码 `ant-f build-migration.xml build-1.0-converter` 脚本，该脚本将在中搜索1.0和Primetime DRM库 [!DNL libs/1.0] 和 [!DNL libs/flashaccess] 目录。

   1. 编辑 [!DNL converter.properties] 文件指向您的LiveCycleES服务器。
   1. 运行 `ant -f build-migration.xml migrate-all-1.0-policies` 将所有FMRMS 1.0 DRM策略转换为Primetime DRM格式。

      要从FMRMS 1.5迁移到Primetime DRM，请参阅 `V1_5PolicyConverter.java` 示例。

   1. 通过运行编译示例代码 `ant-f build-migration.xml build-1.5-converter` 脚本，它希望1.5和3.0库位于 [!DNL libs/1.5] 和 [!DNL libs/flashaccess] 目录。

   1. 编辑 [!DNL converter.properties] 文件指向您的LiveCycleES服务器。
   1. 运行 `ant -f build-migration.xml migrate-all-1.5-policies` 将所有FMRMS 1.5 DRM策略转换为Primetime DRM格式。

      转换后的DRM策略将另存为一组文件。 此 `DRM PolicyConverter` 生成一个CSV格式的文件，该文件包括旧DRM策略ID与新DRM策略ID的映射。 您可以将此文件导入 [!DNL PolicyConversion] 参考实施数据库中的表，该表由 `RefImplMetadataConvReqHandler`.

1. 支持1.x兼容性请求 `FMRMSv1RequestHandler` 和 `FMRMSv1MetadataHandler` 属性：

   1. 将相关数据迁移到基于Primetime DRM的服务器后，对1.x兼容性请求提供支持。

      有关如何处理这些类型请求的示例，请参见 `RefImplUpgradeV1ClientHandler` 和 `RefImplMetadataConvReqHandler` 在参考实施中。
