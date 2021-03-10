---
keywords: 创意选择规则；AdobeTVSDKonfig
title: 应用创意选择规则
description: 应用创意选择规则
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '166'
ht-degree: 0%

---


# 应用创意选择规则{#apply-creative-selection-rules}

TVSDK通过以下方式应用创意选择规则：

* TVSDK首先应用所有`default`规则，然后应用特定于区域的规则。
* TVSDK会忽略未为当前区域ID定义的任何规则。
* 一旦TVSDK应用默认规则，特定于区域的规则可根据`default`规则所选创意的`host`（域）匹配进一步更改创意优先级。

* 在包含附加区域规则的示例规则文件中，一旦TVSDK应用`default`规则，如果M3U8创意域不包含[!DNL my.domain.com]或[!DNL a.bcd.com]且广告区域为`1234`，则对创意进行重新排序，并首先播放FlashVPAID创意（如果可用）。 否则，将播放MP4广告，依此类推，直至JavaScript。

* 如果选择了广告创意，而TVSDK无法本机播放（[!DNL .mp4]、[!DNL .flv]等），则TVSDK会发出重新打包请求。

请注意，TVSDK可以处理的广告类型仍通过`AuditudeSettings`中的`validMimeTypes`设置进行定义。
