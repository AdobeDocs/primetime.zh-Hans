---
description: 优先级规则定义将从VAST/VMAP响应中回放的广告创意的优先级顺序。
keywords: 优先级规则；创意选择规则
title: 优先级规则
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '169'
ht-degree: 1%

---


# 优先级规则{#priority-rules}

优先级规则定义将从VAST/VMAP响应中回放的广告创意的优先级顺序。

## 优先级规则具有以下属性和可能的值：

<table id="table_ljp_tgx_hz">  
 <thead> 
  <tr> 
   <th class="entry"><b>键</b></th> 
   <th class="entry"><b>类型</b></th> 
   <th class="entry"><b>值</b></th> 
   <th class="entry"><b>说明</b></th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td><span class="codeph"> 优先级</span></td> 
   <td><span class="codeph"> 数组</span></td> 
   <td></td> 
   <td> 小写mime类型的数组，它定义了播放必须选择源创意的优先级。</td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> 项目</span></td> 
   <td><span class="codeph"> 字符串</span></td> 
   <td><span class="codeph"> 主机</span></td> 
   <td>当前仅支持<span class="codeph">主机</span>。 当<span class="codeph">匹配</span>和<span class="codeph">值</span>属性时，必须存在此属性。</td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> matches</span></td> 
   <td><span class="codeph"> 字符串</span></td> 
   <td><span class="codeph"> 多个</span></td> 
   <td>可能的值：
    <ul id="ul_tnf_2hx_hz"> 
     <li><span class="codeph"> eq</span>  — 等于</li> 
     <li><span class="codeph"> ne</span>  — 不等于</li> 
     <li><span class="codeph"> co</span> - contains</li> 
     <li><span class="codeph"> nc</span>  — 不包含</li> 
     <li><span class="codeph"> 软件</span> -开始</li> 
     <li><span class="codeph"> 最</span> 终，</li> 
    </ul></td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> 类型</span></td> 
   <td><span class="codeph"> 字符串</span></td> 
   <td><span class="codeph"> 优先级</span></td> 
   <td>值必须始终为<span class="codeph">优先级</span></td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> 值</span></td> 
   <td><span class="codeph"> 数组</span></td> 
   <td></td> 
   <td> <p>TVSDK将使用源创作的<span class="codeph">项</span>上的<span class="codeph"> matches</span>属性，并与此数组中定义的值匹配</p> </td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> 流</span></td> 
   <td><span class="codeph"> 字符串</span></td> 
   <td></td> 
   <td> <p>值可以是<span class="codeph"> vod</span>或<span class="codeph"> live</span></p> </td> 
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
