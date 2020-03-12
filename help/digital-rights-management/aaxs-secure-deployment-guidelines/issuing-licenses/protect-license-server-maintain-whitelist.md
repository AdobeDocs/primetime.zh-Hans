---
seo-title: 维护受信任的内容包装程序的白名单
title: 维护受信任的内容包装程序的白名单
uuid: ad40993c-15c3-43b2-9593-7b75802cfe69
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# 维护受信任的内容包装程序的白名单{#maintain-a-whitelist-of-trusted-content-packagers}

白名 *单是受信任实体的列表* 。 对于内容打包程序，这些组织是内容所有者信任的组织，可以打包（或加密）FLV/F4V视频文件，从而创建DRM保护的内容。 在部署Adobe Access时，建议您维护受信任内容包装程序的白名单，并在发布许可证之前验证DRM保护文件的DRM元数据（DRM头）中包含的内容包装程序的标识。

要了解有关获取有关打包内容的实体的更多信息，请参 `V2ContentMetaData.getPackagerInfo()` 阅 *Adobe Access API参考*。
