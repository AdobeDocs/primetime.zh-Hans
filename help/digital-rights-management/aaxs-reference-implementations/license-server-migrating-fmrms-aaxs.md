---
seo-title: 从FMRMS 1.0或1.5迁移到AdobeAccess 2.0及更高版本
title: 从FMRMS 1.0或1.5迁移到AdobeAccess 2.0及更高版本
uuid: 05caeb39-0c62-4053-87a9-8e89030a188d
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '466'
ht-degree: 0%

---


# 从FMRMS 1.0或1.5迁移到AdobeAccess 2.0及更高版本{#migrating-from-fmrms-or-to-adobe-access-and-above}

为了继续为使用Flash媒体Rights Management服务器(FMRMS)1.0或1.5打包的内容颁发许可证，许可证和策略数据必须基于Adobe访问SDK从LiveCycleES服务器迁移到客户的新服务器。 重要步骤是：

1. 导入许可证信息
1. 将FMRMS策略转换为Adobe访问格式
1. 通过`FMRMSv1RequestHandler`和`FMRMSv1MetadataHandler`支持1.x兼容性请求

要从LiveCycleES将许可证信息导入基于Adobe访问的服务器，请参阅[!DNL Reference Implementation\Server\migration\db]文件夹中提供的示例数据库脚本。 提供了示例脚本，用于将相关数据从MySQL、Oracle或SQL Server数据库导出为CSV文件格式。 导出数据后，即可将其导入您选择的数据库。 导出的许可证信息包括许可证ID、打包时分配的内容ID、所使用策略的ID、内容打包时间以及内容加密密钥。 对于Adobe访问，需要此信息才能将1.x内容元数据转换为Adobe访问元数据格式（请参阅`FMRMSv1RequestHandler`和`FMRMSv1MetadataHandler`）。 在参考实现中，此数据存储在许可证数据库表中，并由`RefImplMetadataConvReqHandler`使用。

现有策略需要转换为Adobe访问格式，以便在转换元数据和为1.0或1.5内容颁发许可证时使用这些策略。 参考Implementation\Server\migration folder contains sample code for creating an Adobe Access policy based on older policies。

如果要从FMRMS 1.0迁移到Adobe访问，请参阅V1_0PolicyConverter.java示例。 通过运行“ `ant-f build-migration.xml build-1.0-converter`”(脚本要求1.0和Adobe访问库分别位于[!DNL libs/1.0]和libs/flashaccess中)编译示例代码。 编辑converter.properties文件以指向您的LiveCycleES服务器。 然后运行“ `ant -f build-migration.xml migrate-all-1.0-policies`”，将所有FMRMS 1.0策略转换为Adobe访问格式。

如果要从FMRMS 1.5迁移到Adobe访问，请参阅V1_5PolicyConverter.java示例。 通过运行“ `ant-f build-migration.xml build-1.5-converter`”（脚本希望1.5和3.0库分别位于libs/1.5和libs/flashaccess中）编译示例代码。 编辑converter.properties文件以指向您的LiveCycleES服务器。 然后运行“ `ant -f build-migration.xml migrate-all-1.5-policies`”，将所有FMRMS 1.5策略转换为Adobe访问格式。

转换的策略将写入一组文件。 此外，PolicyConverter将输出一个CSV文件，其中包含旧策略ID到新策略ID的映射。 此文件可导入到参考实现数据库的“PolicyConversion”表中，并由`RefImplMetadataConvReqHandler`使用。

将相关数据迁移到基于Adobe访问的服务器后，即可实施对1.x兼容性请求的支持。 有关如何处理这些类型请求的示例，请参见参考实现中的`RefImplUpgradeV1ClientHandler`和`RefImplMetadataConvReqHandler`。
