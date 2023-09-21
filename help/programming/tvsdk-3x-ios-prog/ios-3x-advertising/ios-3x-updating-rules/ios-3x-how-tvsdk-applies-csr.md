---
keywords: 创意选择规则；AdobeTVSDKConfig
title: 应用创意选择规则
description: 应用创意选择规则
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '166'
ht-degree: 0%

---

# 应用创意选择规则 {#apply-creative-selection-rules}

TVSDK通过以下方式应用创意选择规则：

* TVSDK适用于所有 `default` 规则在前，区域特定的规则在后。
* TVSDK会忽略任何未为当前区域ID定义的规则。
* 一旦TVSDK应用默认规则，区域特定的规则即可根据 `host` （域）匹配由以下用户选择的创意内容 `default` 规则。

* 在包含其他区域规则的示例规则文件中，一旦TVSDK应用 `default` 规则（如果M3U8创意域不包含） [!DNL my.domain.com] 或 [!DNL a.bcd.com] 广告区域为 `1234`，会对创意内容重新排序，并首先播放FlashVPAID创意内容（如果可用）。 否则，将播放MP4广告，依此类推，一直到JavaScript。

* 如果选择了广告创意，则TVSDK无法本机播放( [!DNL .mp4]， [!DNL .flv]等)，TVSDK会发出重新打包请求。

请注意，可由TVSDK处理的广告类型仍通过 `validMimeTypes` 在中设置 `AuditudeSettings`.
