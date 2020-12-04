---
description: 优先级规则定义广告创意的优先级顺序，这些广告创意将被选择用于从VAST/VMAP响应中回放。
keywords: priority rule;creative selection rules
seo-description: 优先级规则定义广告创意的优先级顺序，这些广告创意将被选择用于从VAST/VMAP响应中回放。
seo-title: 优先级规则
title: 优先级规则
uuid: 4ca31dc7-9c5e-400c-9111-e7b6fc11a392
translation-type: tm+mt
source-git-commit: 812d04037c3b18f8d8cdd0d18430c686c3eee1ff
workflow-type: tm+mt
source-wordcount: '188'
ht-degree: 1%

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
   <td> 小写mime类型的数组，它定义了播放必须选择源创意的优先级。</td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> 物料</span></td> 
   <td><span class="codeph"> 字符串</span></td> 
   <td><span class="codeph"> 主机</span></td> 
   <td>目前仅支持<span class="codeph">主机</span>。 当<span class="codeph">匹配</span>和<span class="codeph">值</span>属性时，此属性必须存在。</td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> matches</span></td> 
   <td><span class="codeph"> 字符串</span></td> 
   <td><span class="codeph"> 多个</span></td> 
   <td>可能的值：
    <ul id="ul_tnf_2hx_hz"> 
     <li><span class="codeph"> eq</span> -等号</li> 
     <li><span class="codeph"> ne</span> -不等于</li> 
     <li><span class="codeph"> co</span> - contains</li> 
     <li><span class="codeph"> nc</span> -不包含</li> 
     <li><span class="codeph"> sw</span> -开始</li> 
     <li><span class="codeph"> 新</span> 的——结尾为</li> 
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
   <td><span class="codeph"> 阵列</span></td> 
   <td></td> 
   <td> <p>TVSDK将使用源创意的<span class="codeph">项</span>上的<span class="codeph">匹配</span>属性，并与此数组中定义的值匹配</p> </td> 
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

