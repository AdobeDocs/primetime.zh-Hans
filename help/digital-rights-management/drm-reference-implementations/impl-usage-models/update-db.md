---
seo-title: 更新参考实施数据库
title: 更新参考实施数据库
uuid: 2883045e-ad62-466d-94a2-fc45ded2a4f5
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '122'
ht-degree: 0%

---


# 更新参考实现DB{#update-the-reference-implementation-db}

要控制将许可证颁发给指定用户的使用模式，请将条目添加到参考实现数据库。

1. 将条目添加到`Customer`表。

   `Customer`表包含用户名和用于验证用户的口令。 它还指示用户是否具有订阅(根据&#x200B;*订阅*&#x200B;使用模式颁发的许可证)。

1. 根据“下载自有”或“视频点播”使用模式授予用户访问权限。

       将条目添加到“CustomerAuthorization”表以指定：
   
   * 使用模型
   * 用户可以访问的每段内容

有关如何填充每个表的详细信息，请参阅[!DNL PopulateSampleDB.sql]脚本（包含在[!DNL Reference Implementation/Server/Reference Implementation Server/dbscript/]目录的Primetime DRM DVD中）。
