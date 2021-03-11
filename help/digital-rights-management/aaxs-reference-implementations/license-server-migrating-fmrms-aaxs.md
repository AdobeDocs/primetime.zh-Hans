---
title: 从FMRMS 1.0或1.5迁移到Adobe Access 2.0及更高版本
description: 从FMRMS 1.0或1.5迁移到Adobe Access 2.0及更高版本
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '466'
ht-degree: 0%

---


# 从FMRMS 1.0或1.5迁移到Adobe Access 2.0及更高版本{#migrating-from-fmrms-or-to-adobe-access-and-above}

为了继续为使用Flash Media Rights Management Server(FMRMS)1.0或1.5打包的内容颁发许可证，许可证和策略数据必须基于Adobe Access SDK从LiveCycle ES服务器迁移到客户的新服务器。 重要步骤是：

1. 导入许可证信息
1. 将FMRMS策略转换为Adobe访问格式
1. 通过`FMRMSv1RequestHandler`和`FMRMSv1MetadataHandler`支持1.x兼容性请求

要将许可证信息从LiveCycle ES导入基于Adobe Access的服务器，请参阅[!DNL Reference Implementation\Server\migration\db]文件夹中提供的示例库脚本。 提供了示例脚本，用于将MySQL、Oracle或SQL Server数据库中的相关数据导出为CSV文件格式。 导出数据后，即可将其导入您选择的数据库。 导出的许可证信息包括许可证ID、打包时分配的内容ID、使用的策略ID、打包内容的时间以及内容加密密钥。 对于Adobe访问，需要此信息才能将1.x内容元数据转换为Adobe访问元数据格式（请参阅`FMRMSv1RequestHandler`和`FMRMSv1MetadataHandler`）。 在参考实现中，此数据存储在许可证数据库表中并由`RefImplMetadataConvReqHandler`使用。

现有策略需要转换为“Adobe访问”格式，以便在转换元数据和颁发1.0或1.5内容的许可证时使用这些策略。 参考Implementation\Server\migration folder contains sample code for creating an Adobe Access policy based on older policies。

如果要从FMRMS 1.0迁移到Adobe Access，请参阅V1_0PolicyConverter.java示例。 通过运行“ `ant-f build-migration.xml build-1.0-converter`”编译示例代码(脚本希望1.0和Adobe Access库分别位于[!DNL libs/1.0]和libs/flashaccess中)。 编辑converter.properties文件以指向您的LiveCycle ES服务器。 然后运行“ `ant -f build-migration.xml migrate-all-1.0-policies`”，将所有FMRMS 1.0策略转换为Adobe Access格式。

如果您是从FMRMS 1.5迁移到Adobe Access，请参阅V1_5PolicyConverter.java示例。 通过运行“ `ant-f build-migration.xml build-1.5-converter`”编译示例代码（脚本希望1.5和3.0库分别位于libs/1.5和libs/flashaccess中）。 编辑converter.properties文件以指向您的LiveCycle ES服务器。 然后运行“ `ant -f build-migration.xml migrate-all-1.5-policies`”，将所有FMRMS 1.5策略转换为Adobe Access格式。

转换的策略将写入一组文件。 此外，PolicyConverter将输出一个CSV文件，其中包含将旧策略ID映射到新策略ID的映射。 此文件可以导入到参考实现数据库中的“PolicyConversion”表中，并将由`RefImplMetadataConvReqHandler`使用。

将相关数据迁移到基于Adobe Access的服务器后，您就可以实施对1.x兼容性请求的支持。 有关如何处理这些类型请求的示例，请参阅参考实现中的`RefImplUpgradeV1ClientHandler`和`RefImplMetadataConvReqHandler`。
