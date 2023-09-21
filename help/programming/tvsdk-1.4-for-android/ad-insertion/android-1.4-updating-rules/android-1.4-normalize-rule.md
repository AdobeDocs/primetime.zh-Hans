---
description: 标准化规则定义URL转换，以应用于从VAST/VMAP响应获得的源创意URL。
keywords: 标准化规则；创意选择规则
title: 标准化规则
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '168'
ht-degree: 0%

---

# 标准化规则{#normalize-rules}

标准化规则定义URL转换，以应用于从VAST/VMAP响应获得的源创意URL。

**表2：标准化规则具有以下属性和可能的值：**

<table id="table_ljp_tgx_hz">  
 <thead> 
  <tr> 
   <th class="entry"> 键</th> 
   <th class="entry"> 类型</th> 
   <th class="entry"> 值</th> 
   <th class="entry"> 描述</th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td><span class="codeph"> type</span></td> 
   <td><span class="codeph"> 字符串</span></td> 
   <td><span class="codeph"> 规范化</span></td> 
   <td>该值必须始终为 <span class="codeph"> 规范化</span>.</td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> 项目</span></td> 
   <td><span class="codeph"> 字符串</span></td> 
   <td><span class="codeph"> 主机</span></td> 
   <td>当前仅限 <span class="codeph"> 主机</span> 受支持。 此属性必须存在于 <span class="codeph"> 匹配</span> 和 <span class="codeph"> 值</span> 属性已定义。</td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> 匹配</span></td> 
   <td></td> 
   <td></td> 
   <td>可能的值：
    <ul id="ul_tnf_2hx_hz"> 
     <li><span class="codeph"> eq</span>  — 等于</li> 
     <li><span class="codeph"> ne</span>  — 不等于</li> 
     <li><span class="codeph"> co</span>  — 包含</li> 
     <li><span class="codeph"> nc</span>  — 不包含</li> 
     <li><span class="codeph"> 软件</span>  — 开头为</li> 
     <li><span class="codeph"> 新建</span>  — 结尾为</li> 
    </ul></td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> 值</span></td> 
   <td><span class="codeph"> 数组</span></td> 
   <td></td> 
   <td>TVSDK将使用 <span class="codeph"> 匹配</span> 上的属性 <span class="codeph"> 项目</span> ，并与此数组中定义的值进行匹配。</td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> 查找</span></td> 
   <td><span class="codeph"> 正则表达式</span></td> 
   <td></td> 
   <td> 应用于要匹配的源创意URL的正则表达式。</td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> replace</span></td> 
   <td><span class="codeph"> 正则表达式</span></td> 
   <td></td> 
   <td> 根据匹配项应用于要替换的源创意URL的正则表达式。</td> 
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
