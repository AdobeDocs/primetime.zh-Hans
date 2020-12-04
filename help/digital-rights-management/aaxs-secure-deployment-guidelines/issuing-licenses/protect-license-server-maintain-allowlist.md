---
seo-title: 维护可信内容包装程序的允许列表
title: 维护可信内容包装程序的允许列表
uuid: ad40993c-15c3-43b2-9593-7b75802cfe69
translation-type: tm+mt
source-git-commit: 58bb3bedc5b0ac63afd96eb6101d9ad779e6deed
workflow-type: tm+mt
source-wordcount: '126'
ht-degree: 0%

---


# 维护受信任内容包装程序的允许列表{#maintain-a-allowlist-of-trusted-content-packagers}

**允许列表**&#x200B;是受信任实体的列表。 对于内容打包者，这些是内容所有者信任的组织来打包（或加密）FLV/F4V视频文件，从而创建DRM保护的内容。 部署Adobe访问时，建议您维护受信任内容打包程序的允许列表，并在发布许可证之前验证DRM保护文件的DRM元数据（DRM头）中包含的内容打包程序的标识。

要了解有关获取有关打包内容的实体的详细信息，请参阅&#x200B;*Adobe访问API参考*&#x200B;中的`V2ContentMetaData.getPackagerInfo()`。
