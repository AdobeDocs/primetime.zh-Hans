---
description: 优先级规则定义广告创意的优先级顺序，这些广告创意将被选择用于从VAST/VMAP响应中回放。
keywords: priority rule;creative selection rules
seo-description: 优先级规则定义广告创意的优先级顺序，这些广告创意将被选择用于从VAST/VMAP响应中回放。
seo-title: 优先级规则
title: 优先级规则
uuid: 8716758f-686e-4927-8605-19c36091db65
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# 优先级规则{#priority-rules}

优先级规则定义广告创意的优先级顺序，这些广告创意将被选择用于从VAST/VMAP响应中回放。

## 优先级规则具有以下属性和可能的值：

<table id="table_ljp_tgx_hz">  
 <thead> 
  <tr> 
   <th class="entry"> 密钥</th> 
   <th class="entry"> 类型</th> 
   <th class="entry"> 值</th> 
   <th class="entry"> 说明</th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td><span class="codeph"> 优先级</span></td> 
   <td><span class="codeph"> 阵列</span></td> 
   <td></td> 
   <td> 一个小写mime类型的数组，它定义了播放时必须选择源创意的优先级。</td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> 项目</span></td> 
   <td><span class="codeph"> 字符串</span></td> 
   <td><span class="codeph"> 主机</span></td> 
   <td>当前仅支 <span class="codeph"> 持主机</span> 。 当匹配和定义值属性时 <span class="codeph"> ,</span> 此属性必 <span class="codeph"> 须存在</span> 。</td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> matches</span></td> 
   <td><span class="codeph"> 字符串</span></td> 
   <td><span class="codeph"> 多个</span></td> 
   <td>可能的值：
    <ul id="ul_tnf_2hx_hz"> 
     <li><span class="codeph"> eq</span> —— 等于</li> 
     <li><span class="codeph"> ne</span> —— 不等于</li> 
     <li><span class="codeph"> co</span> - contains</li> 
     <li><span class="codeph"> nc</span> —— 不包含</li> 
     <li><span class="codeph"> sw</span> —— 开始于</li> 
     <li><span class="codeph"> ew</span> —— 结束于</li> 
    </ul></td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> type</span></td> 
   <td><span class="codeph"> 字符串</span></td> 
   <td><span class="codeph"> 优先级</span></td> 
   <td>值必须始终为优先级 <span class="codeph"></span></td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> values</span></td> 
   <td><span class="codeph"> 阵列</span></td> 
   <td></td> 
   <td> <p>TVSDK将使用源创 <span class="codeph"> 作项目</span> 上的matches属性 <span class="codeph"></span> ，并与此数组中定义的值匹配</p> </td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> stream</span></td> 
   <td><span class="codeph"> 字符串</span></td> 
   <td></td> 
   <td> <p>值可以是 <span class="codeph"> vod</span> 或 <span class="codeph"> live</span></p> </td> 
  </tr> 
 </tbody> 
</table>

```
{
    "ads": {
        "rules": {
            "default": [
                {
                    "
<b>type</b>": "
<b>priority</b>",
                    "
<b>stream</b>": "vod",
                    "
<b>priority</b>": [
                        "application/x-mpegurl",
                        "application/vnd.apple.mpegurl",
                        "application/x-shockwave-flash",
                        "video/mp4",
                        "video/m4v",
                        "video/x-flv",
                        "video/webm"
                    ]
                },
                {
                    ...
                },
            ]
        }
    }
}
```

