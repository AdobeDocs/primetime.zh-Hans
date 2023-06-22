---
title: 附录B “调试提示”
description: 附录B “调试提示”
exl-id: ea024797-315e-47c0-99ea-1ac49c8c9697
source-git-commit: bfc3ba55c99daba561255760baf273b6538a3c6e
workflow-type: tm+mt
source-wordcount: '173'
ht-degree: 0%

---

# 附录B：调试提示 {#appendix-b-debugging-tips}

>[!NOTE]
>
>此页面上的内容仅供参考。 使用此API需要来自Adobe的当前许可证。 不允许未经授权的使用。


## 清除临时数据 {#clearing-temporary-data}

Adobe Primetime身份验证存储临时数据，例如浏览器缓存、LSO缓存和Cookie。 清除临时数据非常重要，这可确保您在测试时一切顺利。

- [清除浏览器缓存和Cookie](#clearing-the-browser-cache-and-cookies)
- [正在清除LSO缓存](#clearing-lsos-cache)\
    

## 清除浏览器缓存和Cookie {#clearing-the-browser-cache-and-cookies}

虽然浏览器可靠，但在Firefox中：“工具” — \>“清除最近的历史记录……” — \>在“清除的时间范围：”上选择“所有内容”；在“详细信息”上选择“Cookie”和“缓存” — \>单击“立即清除”。\
 

## 正在清除LSO缓存 {#clearing-lsos-cache}

访问 [Flash Player帮助](http://www.macromedia.com/support/documentation/en/flashplayer/help/settings_manager07.html).

选择 ```entitlement.\*``` （取决于测试的内容），然后单击“删除网站”。\
 

## 调试工具 {#tools}

Adobe Primetime身份验证工程师使用以下调试工具：

- Firebug - <http://www.getfirebug.com/>
- Flashbug （适用于flash player的调试版本） <https://addons.mozilla.org/en-US/firefox/addon/14465/>
- Live http标头 —  <https://addons.mozilla.org/en-US/firefox/addon/3829/>
- 费德勒 —  <http://www.fiddler2.com/fiddler2/>
- 查尔斯 —  <http://www.charlesproxy.com/>
- Wireshark - <http://www.wireshark.org/>


<!--
## Related Information

- [Programmer Integration Guide](/help/authentication/programmer-integration-guide-overview.md)

- [Using Charles Proxy (Tech Note)](https://tve.zendesk.com/hc/en-us/articles/204962849-Using-Charles-Proxy)
-->
