---
description: 'null'
keywords: creative selection rules;AdobeTVSDKConfig
seo-description: 'null'
seo-title: 应用创意选择规则
title: 应用创意选择规则
uuid: 2f009776-201c-418e-aa8f-cb409d0046d8
translation-type: tm+mt
source-git-commit: 557f42cd9a6f356aa99e13386d9e8d65e043a6af

---


# 应用创意选择规则 {#apply-creative-selection-rules}

TVSDK通过以下方式应用创意选择规则：

* TVSDK首先应 `default` 用所有规则，然后是区域特定规则。
* TVSDK会忽略未为当前区域ID定义的任何规则。
* 一旦TVSDK应用默认规则，特定于区域的规则就可以根据规则所选择的创意的 `host` （域）匹配进一步更改创意优先 `default` 级。

* 在包含附加区域规则的示例规则文件中，一旦TVSDK应用规则，如果 `default` M3U8创意域不包含或 [!DNL my.domain.com] ，且广告区域是 [!DNL a.bcd.com]`1234`，则对创意进行重新排序，并首先播放Flash VPAID创意（如果有）。 否则，将播放MP4广告，依此类推，直至JavaScript。

* 如果选择了广告创意，而TVSDK无法本机播放( [!DNL .mp4]、 [!DNL .flv]等)，则TVSDK会发出重新打包请求。

请注意，TVSDK可以处理的广告类型仍通过中的设置 `validMimeTypes` 进行定义 `AuditudeSettings`。