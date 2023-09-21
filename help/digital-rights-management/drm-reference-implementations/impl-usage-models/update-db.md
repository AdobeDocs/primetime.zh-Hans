---
title: 更新引用实现DB
description: 更新引用实现DB
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '122'
ht-degree: 0%

---

# 更新引用实现DB{#update-the-reference-implementation-db}

要控制向指定用户颁发许可证的使用模型，请将条目添加到参考实现数据库中。

1. 将条目添加到 `Customer` 表格。

   此 `Customer` 该表包含用于验证用户的用户名和口令。 它还指示用户是否具有订阅(根据 *订阅* 使用模式)。

1. 根据“下载到拥有”或“视频点播”使用模型授予用户访问权限。

       将条目添加到“CustomerAuthorization”表以指定：
   
   * 使用模式
   * 用户可以访问的每个内容区段

有关如何填充每个表的详细信息，请参见 [!DNL PopulateSampleDB.sql] 脚本(包含在您的Primetime DRM DVD [!DNL Reference Implementation/Server/Reference Implementation Server/dbscript/] 目录)。
