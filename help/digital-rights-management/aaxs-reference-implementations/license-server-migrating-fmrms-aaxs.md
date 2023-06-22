---
title: 从FMRMS 1.0或1.5迁移到Adobe访问2.0及更高版本
description: 从FMRMS 1.0或1.5迁移到Adobe访问2.0及更高版本
copied-description: true
exl-id: 9aadf9a0-a7c5-466b-9dd1-c1bab2b8bfc6
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '466'
ht-degree: 0%

---

# 从FMRMS 1.0或1.5迁移到Adobe访问2.0及更高版本 {#migrating-from-fmrms-or-to-adobe-access-and-above}

为了继续为使用Flash媒体Rights Management服务器(FMRMS) 1.0或1.5打包的内容颁发许可证，必须基于Adobe访问SDK将许可证和策略数据从LiveCycleES服务器迁移到客户的新服务器。 重要步骤包括：

1. 导入许可证信息
1. 将FMRMS策略转换为Adobe访问格式
1. 支持1.x兼容性请求，通过 `FMRMSv1RequestHandler` 和 `FMRMSv1MetadataHandler`

要将许可证信息从LiveCycleES导入基于Adobe访问的服务器，请参阅 [!DNL Reference Implementation\Server\migration\db] 文件夹。 提供了示例脚本，用于将相关数据从MySQL、Oracle或SQL Server数据库导出为CSV文件格式。 导出数据后，可将其导入到您选择的数据库中。 导出的许可证信息包括许可证ID、打包时分配的内容ID、使用的策略的ID、打包内容的时间以及内容加密密钥。 对于Adobe访问，需要此信息才能将1.xAdobe元数据转换为“内容访问”元数据格式(请参阅 `FMRMSv1RequestHandler` 和 `FMRMSv1MetadataHandler`)。 在参考实现中，此数据存储在许可证数据库表中，由以下人员使用 `RefImplMetadataConvReqHandler`.

现有策略需要转换为Adobe访问格式，以便在转换1.0或1.5内容的元数据和颁发许可证时使用这些策略。 Reference Implementation\Server\migration文件夹包含基于旧策略创建Adobe访问策略的示例代码。

如果要从FMRMS 1.0迁移到Adobe访问，请参阅V1_0PolicyConverter.java示例。 通过运行&#39;&#39;编译示例代码 `ant-f build-migration.xml build-1.0-converter`“”(脚本预期1.0和Adobe访问库位于 [!DNL libs/1.0] 和libs/flashaccess)。 编辑converter.properties文件以指向您的LiveCycleES服务器。 然后运行» `ant -f build-migration.xml migrate-all-1.0-policies`”以将所有FMRMS 1.0策略转换为Adobe访问格式。

如果要从FMRMS 1.5迁移到Adobe访问，请参阅V1_5PolicyConverter.java示例。 通过运行&#39;&#39;编译示例代码 `ant-f build-migration.xml build-1.5-converter`“（脚本预期1.5和3.0库分别位于libs/1.5和libs/flashaccess中）。 编辑converter.properties文件以指向您的LiveCycleES服务器。 然后运行» `ant -f build-migration.xml migrate-all-1.5-policies`”以将所有FMRMS 1.5策略转换为Adobe访问格式。

转换后的策略将写入一组文件。 此外，PolicyConverter将输出一个CSV文件，该文件包含旧策略ID到新策略ID的映射。 此文件可以导入到参考实施数据库的“PolicyConversion”表中，并将由以下人员使用 `RefImplMetadataConvReqHandler`.

在相关数据迁移到基于Adobe访问的服务器后，您就可以对1.x兼容性请求实施支持。 参见 `RefImplUpgradeV1ClientHandler` 和 `RefImplMetadataConvReqHandler` 在参考实施中有关如何处理这些类型请求的示例。
