---
description: 标准化规则定义URL转换以应用于从VAST/VMAP响应获得的源创意URL。
keywords: normalize rule;creative selection rules
seo-description: 标准化规则定义URL转换以应用于从VAST/VMAP响应获得的源创意URL。
seo-title: 标准化规则
title: 标准化规则
uuid: b3ca2c8e-133a-4630-8109-17bf0a91843d
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# 标准化规则{#normalize-rules}

标准化规则定义URL转换以应用于从VAST/VMAP响应获得的源创意URL。

## 标准化规则具有以下属性和可能的值：

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
   <td><span class="codeph"> type</span></td> 
   <td><span class="codeph"> 字符串</span></td> 
   <td><span class="codeph"> 标准化</span></td> 
   <td>该值必须始终为标准 <span class="codeph"> 化</span>。</td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> 项目</span></td> 
   <td><span class="codeph"> 字符串</span></td> 
   <td><span class="codeph"> 主机</span></td> 
   <td>当前仅支 <span class="codeph"> 持主机</span> 。 当匹配和定义值属性时 <span class="codeph"> ,</span> 此属性必 <span class="codeph"> 须存在</span> 。</td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> matches</span></td> 
   <td></td> 
   <td></td> 
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
   <td><span class="codeph"> values</span></td> 
   <td><span class="codeph"> 阵列</span></td> 
   <td></td> 
   <td>TVSDK将使用源创 <span class="codeph"> 作项目上的</span> matches <span class="codeph"> 属性</span> ，并与此数组中定义的值匹配。</td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> 查找</span></td> 
   <td><span class="codeph"> 正则</span></td> 
   <td></td> 
   <td> 要在源创意URL上应用以匹配的正则表达式。</td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> 替换</span></td> 
   <td><span class="codeph"> 正则</span></td> 
   <td></td> 
   <td> 要在源创意URL上应用并基于匹配进行替换的正则表达式。</td> 
  </tr> 
 </tbody> 
</table>

```
{
    "ads": {
        "rules": {
            "default": [
                {
                ...
                }
                {
                    "
<b>type</b>": "
<b>normalize</b>",
                    "
<b>item</b>": "host",
                    "
<b>matches</b>": "ew",
                    "
<b>values</b>": [
                        "redirector.gvt1.com"
                    ],
                    "
<b>find</b>": "videoplayback/(.*?)/expire/.*?/(.*?)/signature/.*?/",
                    "
<b>replace</b>": "videoplayback/$1/expire//$2/signature//"
                }                
            ]
        }
    }
}
```

