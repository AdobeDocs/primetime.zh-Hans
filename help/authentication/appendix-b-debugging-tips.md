---
title: 附录B“调试提示”
description: 附录B“调试提示”
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '173'
ht-degree: 0%

---


# 附录B:调试提示 {#appendix-b-debugging-tips}

>[!NOTE]
>
>此页面上的内容仅供参考。 使用此API需要获得Adobe的当前许可证。 不允许未经授权使用。


## 清除临时数据 {#clearing-temporary-data}

Adobe Primetime身份验证存储临时数据，如浏览器缓存、LSOs缓存和Cookie。 清除临时数据非常重要，这可确保您在测试时获得完整的信息。

- [清除浏览器缓存和Cookie](#clearing-the-browser-cache-and-cookies)
- [清除LSOs缓存](#clearing-lsos-cache)\
    

## 清除浏览器缓存和Cookie {#clearing-the-browser-cache-and-cookies}

它可靠，但在Firefox中是：&quot;Tools&quot; -\> &quot;Clear Recent History...&quot; -\>在“清除时间范围：”上，选择“Everything”；和“详细信息”：选中“Cookie”和“Cache” — \>单击“立即清除”。\
 

## 清除LSOs缓存 {#clearing-lsos-cache}

访问 [Flash Player帮助](http://www.macromedia.com/support/documentation/en/flashplayer/help/settings_manager07.html).

选择 ```entitlement.\*``` （具体取决于测试的内容）并单击“删除网站”。\
 

## 调试工具 {#tools}

Adobe Primetime身份验证工程师使用以下调试工具：

- Firebug - <http://www.getfirebug.com/>
- Flashbug（与Flash播放器的调试版本配合使用） <https://addons.mozilla.org/en-US/firefox/addon/14465/>
- Live http头 —  <https://addons.mozilla.org/en-US/firefox/addon/3829/>
- Fiddler - <http://www.fiddler2.com/fiddler2/>
- Charles - <http://www.charlesproxy.com/>
- Wireshark - <http://www.wireshark.org/>


<!--
## Related Information

- [Programmer Integration Guide](/help/authentication/programmer-integration-guide-overview.md)

- [Using Charles Proxy (Tech Note)](https://tve.zendesk.com/hc/en-us/articles/204962849-Using-Charles-Proxy)
-->