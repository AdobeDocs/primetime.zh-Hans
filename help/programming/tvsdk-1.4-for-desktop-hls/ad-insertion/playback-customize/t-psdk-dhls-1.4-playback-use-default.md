---
description: 您可以选择使用默认广告行为。
seo-description: 您可以选择使用默认广告行为。
seo-title: 使用默认播放行为
title: 使用默认播放行为
uuid: 7139384c-167a-4cab-816a-c02fb723a5cb
translation-type: tm+mt
source-git-commit: adef0bbd52ba043f625f38db69366c6d873c586d

---


# 使用默认播放行为{#use-the-default-playback-behavior}

您可以选择使用默认广告行为。

要使用默认行为，请执行以下操作：

    *如果您实施自己的“ContentFactory”类，则在您实施“doRetrieveAdPolicySelector”时返回“DefaultAdPolicySelector”的新实例。
    
    &quot;
    公共类CustomContentFactory扩展ContentFactory {
    
    //...
    //您的广告类自定义代码
    //...
    
    /***
    *@inherit
    */
    override functiondoRetrieveAdPolicySelector(item:MediaPolicyItem):AdPolicySelector{return new DefaultAdPolicyPolicySelector{
    reter}如果您没有自定义的“RetrerieviveAdAdAdAdPlayer”内容，
    
    
    
    
    
    Player选择器(iePlePlayer)，则类，TVSDK使用“DefaultAdPolicySelector”。