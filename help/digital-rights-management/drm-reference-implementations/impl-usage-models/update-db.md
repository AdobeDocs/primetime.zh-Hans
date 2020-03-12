---
seo-title: 更新参考实现DB
title: 更新参考实现DB
uuid: 2883045e-ad62-466d-94a2-fc45ded2a4f5
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# 更新参考实现DB{#update-the-reference-implementation-db}

要控制将许可证颁发给指定用户的使用模式，请将条目添加到参考实现数据库。

1. 向表中添加 `Customer` 条目。

   该表 `Customer` 包括用户名和用于验证用户的口令。 它还指示用户是否有订阅(根据订阅使用模式发出的许 *可* )。

1. 根据“下载到自有”或“视频点播”使用模式授予用户访问权限。

       将条目添加到“CustomerAuthorization”表以指定：
   
   * 使用模型
   * 用户可以访问的每段内容

有关如何填充每个表的详细信息，请参 [!DNL PopulateSampleDB.sql] 阅脚本(包含在目录中的Primetime DRM DVD [!DNL Reference Implementation/Server/Reference Implementation Server/dbscript/] 中)。
