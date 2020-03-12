---
description: 要继续为随Flash Media Rights Management Server(FMRMS)1.0或1.5一起打包的内容发放许可证，您必须将许可证和DRM策略数据从LiveCycle ES服务器迁移到基于Adobe Primetime DRM SDK的客户新服务器。
seo-description: 要继续为随Flash Media Rights Management Server(FMRMS)1.0或1.5一起打包的内容发放许可证，您必须将许可证和DRM策略数据从LiveCycle ES服务器迁移到基于Adobe Primetime DRM SDK的客户新服务器。
seo-title: 从FMRMS 1.0或1.5迁移到Adobe Primetime DRM 2.0或更高版本
title: 从FMRMS 1.0或1.5迁移到Adobe Primetime DRM 2.0或更高版本
uuid: 49ecbbd2-d83b-4bf2-841e-c3f9e5d5e141
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# 从FMRMS 1.0或1.5迁移到Adobe Primetime DRM 2.0或更高版本{#migrate-from-fmrms-or-to-adobe-primetime-drm-or-later}

要继续为随Flash Media Rights Management Server(FMRMS)1.0或1.5一起打包的内容发放许可证，您必须将许可证和DRM策略数据从LiveCycle ES服务器迁移到基于Adobe Primetime DRM SDK的客户新服务器。

要迁移，请完成以下任务：

1. 导入许可证信息：

   1. 要将许可证信息从LiveCycle ES导入到基于Primetime DRM的服务器，请参阅文件夹中的示例数据库脚 [!DNL Reference Implementation\Server\migration\db] 本。
   1. 运行示例脚本，将MySQL、Oracle或SQL Server数据库中的相关数据导出为CSV文件格式。
   1. 从LiveCycle ES导出数据后，将数据导入到数据库。

      导出的许可证信息包括：

      * 许可证ID
      * 在打包时分配的内容ID
      * 正在应用的DRM策略的ID
      * 内容打包的时间
      * 内容加密密钥
      在将1.x内容元数据转换为Primetime DRM元数据格式之前，需要提供此信息。 在参考实现中，此数据存储在许可证数据库表中并由使用 `RefImplMetadataConvReqHandler`。 For more information, see `FMRMSv1RequestHandler` and `FMRMSv1MetadataHandler`.


1. 将FMRMS策略转换为Primetime DRM格式：

   1. 在应用DRM策略以转换元数据并为版本1.0或版本1.5内容颁发许可证之前，请将现有DRM策略转换为Primetime DRM格式。

      该文 `Reference Implementation\Server\migration` 件夹包含用于创建基于旧版DRM策略的Primetime DRM策略的示例代码。 要从FMRMS 1.0迁移到Primetime DRM，请参阅示 `V1_0PolicyConverter.java` 例。
   1. 通过运行脚本编译示 `ant-f build-migration.xml build-1.0-converter` 例代码，该脚本在和目录中搜索1.0和Primetime DRM [!DNL libs/1.0] 库 [!DNL libs/flashaccess] 。

   1. 编辑文 [!DNL converter.properties] 件以指向LiveCycle ES服务器。
   1. 运 `ant -f build-migration.xml migrate-all-1.0-policies` 行以将所有FMRMS 1.0 DRM策略转换为Primetime DRM格式。

      要从FMRMS 1.5迁移到Primetime DRM，请参阅示 `V1_5PolicyConverter.java` 例。

   1. 通过运行脚本编译示 `ant-f build-migration.xml build-1.5-converter` 例代码，该脚本希望1.5和3.0库位于和目 [!DNL libs/1.5] 录 [!DNL libs/flashaccess] 中。

   1. 编辑文 [!DNL converter.properties] 件以指向LiveCycle ES服务器。
   1. 运 `ant -f build-migration.xml migrate-all-1.5-policies` 行以将所有FMRMS 1.5 DRM策略转换为Primetime DRM格式。

      转换的DRM策略将保存为一组文件。 该文 `DRM PolicyConverter` 件将生成一个CSV格式的文件，其中包括将旧DRM策略ID映射到新DRM策略ID。 可以将此文件导入到引 [!DNL PolicyConversion] 用实现数据库中的表，该表由使用 `RefImplMetadataConvReqHandler`。

1. 支持1.x兼容性请求和 `FMRMSv1RequestHandler` 属性 `FMRMSv1MetadataHandler` :

   1. 在相关数据已迁移到基于Primetime DRM的服务器后，实现对1.x兼容性请求的支持。

      有关如何处理这些类型请求的示例，请参 `RefImplUpgradeV1ClientHandler` 阅参 `RefImplMetadataConvReqHandler` 考实现和中。

