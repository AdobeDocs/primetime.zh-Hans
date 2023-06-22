---
keywords: 创意选择规则；AdobeTVSDKConfig
title: 应用创意选择规则
description: 应用创意选择规则
copied-description: true
exl-id: ec77d3b1-573c-4751-a472-bb9c0aa0b602
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '166'
ht-degree: 0%

---

# 应用创意选择规则 {#apply-creative-selection-rules}

TVSDK通过以下方式应用创意选择规则：

* TVSDK适用于所有 `default` 规则优先，区域特定的规则优先。
* TVSDK会忽略任何未为当前区域ID定义的规则。
* 一旦TVSDK应用默认规则，区域特定的规则即可根据 `host` （域）匹配由选定的创意内容 `default` 规则。

* 在包含其他区域规则的示例规则文件中，一旦TVSDK应用 `default` 规则(如果M3U8创意域不包含 `my.domain.com` 或 `a.bcd.com` 广告区域为 `1234`，会对创意内容重新排序，并首先播放FlashVPAID创意内容（如果可用）。 否则，将播放MP4广告，依此类推，一直到JavaScript。

* 如果选择了广告创意，则TVSDK无法本机播放( [!DNL .mp4]， [!DNL .flv]，等等)，TVSDK会发出重新打包请求。

请注意，可由TVSDK处理的广告类型仍通过 `validMimeTypes` 在中设置 `AuditudeSettings`.

<!-- 

In Android 2.5 API docs, I see a 
<span class="codeph"> setValidMimeTypes</span> but not a 
<span class="codeph"> getValidMimeTypes</span>.

 -->
