---
seo-title: 维护受信任内容打包程序的允许列表
title: 维护受信任内容打包程序的允许列表
uuid: ad40993c-15c3-43b2-9593-7b75802cfe69
translation-type: tm+mt
source-git-commit: 9d2e046ae259c05fb4c278f464c9a26795e554fc
workflow-type: tm+mt
source-wordcount: '121'
ht-degree: 0%

---


# 维护受信任内容打包程序的允许列表{#maintain-a-allowlist-of-trusted-content-packagers}

allowlist *是受信任* 实体的列表。 对于内容打包者，这些是内容所有者信任的组织来打包（或加密）FLV/F4V视频文件，从而创建DRM保护的内容。 部署Adobe Access时，建议您保留受信任内容包装程序的允许列表，并在发布许可证之前验证DRM保护文件的DRM元数据（DRM头）中包含的内容包装程序的身份。

要了解有关获取有关打包内容的实体的更多信息，请参 `V2ContentMetaData.getPackagerInfo()` 阅Adobe *Access API参考*。
