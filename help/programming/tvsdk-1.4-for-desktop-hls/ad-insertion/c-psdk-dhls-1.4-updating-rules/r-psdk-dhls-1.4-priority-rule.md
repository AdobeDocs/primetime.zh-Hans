---
description: 优先级规则定义将从VAST/VMAP响应中选择用于播放的广告创意的优先级顺序。
keywords: 优先级规则；创意选择规则
title: 优先级规则
exl-id: a045e102-1c16-46b5-8322-0bcab086ac67
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '169'
ht-degree: 0%

---

# 优先级规则{#priority-rules}

优先级规则定义将从VAST/VMAP响应中选择用于播放的广告创意的优先级顺序。

## 优先级规则具有以下属性和可能值：

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
   <td><span class="codeph"> 优先级</span></td> 
   <td><span class="codeph"> 数组</span></td> 
   <td></td> 
   <td> 一个小写mime类型数组，定义必须从中选择源创意内容才能播放的优先级。</td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> 项目</span></td> 
   <td><span class="codeph"> 字符串</span></td> 
   <td><span class="codeph"> 主机</span></td> 
   <td>当前仅限 <span class="codeph"> 主机</span> 受支持。 此属性必须存在于 <span class="codeph"> 匹配</span> 和 <span class="codeph"> 值</span> 属性已定义。</td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> 匹配</span></td> 
   <td><span class="codeph"> 字符串</span></td> 
   <td><span class="codeph"> 多个</span></td> 
   <td>可能的值：
    <ul id="ul_tnf_2hx_hz"> 
     <li><span class="codeph"> eq</span>  — 等于</li> 
     <li><span class="codeph"> ne</span>  — 不等于</li> 
     <li><span class="codeph"> co</span>  — 包含</li> 
     <li><span class="codeph"> nc</span>  — 不包含</li> 
     <li><span class="codeph"> 软件</span>  — 开头为</li> 
     <li><span class="codeph"> ew</span>  — 结束于</li> 
    </ul></td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> type</span></td> 
   <td><span class="codeph"> 字符串</span></td> 
   <td><span class="codeph"> 优先级</span></td> 
   <td>该值必须始终为 <span class="codeph"> 优先级</span></td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> 值</span></td> 
   <td><span class="codeph"> 数组</span></td> 
   <td></td> 
   <td> <p>TVSDK将使用 <span class="codeph"> 匹配</span> 上的属性 <span class="codeph"> 项目</span> ，并与此数组中定义的值进行匹配</p> </td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> 流</span></td> 
   <td><span class="codeph"> 字符串</span></td> 
   <td></td> 
   <td> <p>值可以是 <span class="codeph"> vod</span> 或 <span class="codeph"> 实时</span></p> </td> 
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
