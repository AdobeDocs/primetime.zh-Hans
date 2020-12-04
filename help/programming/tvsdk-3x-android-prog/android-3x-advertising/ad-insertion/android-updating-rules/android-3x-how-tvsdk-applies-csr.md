---
description: 'null'
keywords: creative selection rules;AdobeTVSDKConfig
seo-description: 'null'
seo-title: 应用创意选择规则
title: 应用创意选择规则
uuid: 66e55f95-25ce-4838-b222-63ee34e535d1
translation-type: tm+mt
source-git-commit: 3fdae2b6babb578d2cacff970fd9c7b53ad2c5dc
workflow-type: tm+mt
source-wordcount: '164'
ht-degree: 0%

---


# 应用创意选择规则{#apply-creative-selection-rules}

TVSDK通过以下方式应用创意选择规则：

* TVSDK首先应用所有`default`规则，然后应用区域特定规则。
* TVSDK会忽略未为当前区域ID定义的任何规则。
* 一旦TVSDK应用默认规则，区域特定规则可根据`default`规则所选创意的`host`（域）匹配项进一步更改创意优先级。

* 在包含附加区域规则的示例规则文件中，一旦TVSDK应用`default`规则，如果M3U8创意域不包含`my.domain.com`或`a.bcd.com`且广告区域为`1234`，创意将重新排序，FlashVPAID创意将首先播放（如果可用）。 否则，将播放MP4广告，依此类推，直至JavaScript。

* 如果选择了广告创意，而TVSDK无法本机播放（[!DNL .mp4]、[!DNL .flv]等），则TVSDK将发出重新打包请求。

请注意，TVSDK可以处理的广告类型仍通过`AuditudeSettings`中的`validMimeTypes`设置进行定义。

<!-- 

In Android 2.5 API docs, I see a 
<span class="codeph"> setValidMimeTypes</span> but not a 
<span class="codeph"> getValidMimeTypes</span>.

 -->

