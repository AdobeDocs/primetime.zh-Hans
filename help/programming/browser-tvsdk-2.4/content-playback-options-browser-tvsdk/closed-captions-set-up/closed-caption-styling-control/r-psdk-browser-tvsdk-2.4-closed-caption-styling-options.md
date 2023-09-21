---
description: 您可以指定多个标题样式选项，这些选项将覆盖原始标题中的样式选项。
title: 隐藏式字幕样式选项
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '349'
ht-degree: 0%

---

# 隐藏式字幕样式选项{#closed-caption-styling-options}

您可以指定多个标题样式选项，这些选项将覆盖原始标题中的样式选项。

```js
new TextFormat( 
   font,  
   fontColor,  
   edgeColor,  
   fontEdge,  
   backgroundColor,  
   fillColor,  
   size,  
   fontOpacity,  
   backgroundOpacity,  
   fillOpacity, 
   bottomInset, 
   safeArea) 
```

>[!TIP]
>
>在定义默认值的选项中(例如， `DEFAULT`)，该值是指最初指定描述时的设置。

<table frame="all" colsep="1" rowsep="1" id="table_87205DEFEE384AF4AF83952B15E18A42"> 
 <thead> 
  <tr rowsep="1"> 
   <th colname="1" class="entry"> 格式 </th> 
   <th colname="2" class="entry"> 描述 </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr rowsep="1"> 
   <td colname="1"> 字体 </td> 
   <td colname="2"> <p>字体类型。 </p> <p>只能设置为由定义的值 <span class="codeph"> TextFormat.Font </span> 枚举并表示，例如，带衬线或不带衬线的等宽值。 </p> <p>提示：设备上可用的实际字体可能有所不同，必要时会使用替换。 通常使用带衬线的等宽作为替代，尽管此替代可以特定于系统。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> 大小 </td> 
   <td colname="2"> <p>题注的大小。 </p> <p> 只能设置为由 <span class="codeph"> TextFormat.Size </span> 明细列表： 
     <ul compact="yes" id="ul_544BFC7A46474A74839477108F1AB1E9"> 
      <li id="li_A592ED46B8DF4D8FAD7AF3BD931A712B"> <span class="codeph"> 中 </span>  — 标准大小 </li> 
      <li id="li_4F8CEDE54965430EB707DD3D5B2E3F87"> <span class="codeph"> 大 </span>  — 比中型大约30% </li> 
      <li id="li_D78D823883F54D869118BAB58257E377"> <span class="codeph"> 小 </span>  — 比中型小约30% </li> 
      <li id="li_9299C13408584A38835F8D91BD048083"> <span class="codeph"> 默认 </span>  — 字幕的默认大小；与“中”相同 </li> 
     </ul> </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> 字体颜色 </td> 
   <td colname="2"> <p>字体颜色。 </p> <p>只能设置为由 <span class="codeph"> TextFormat.Color </span> 明细列表。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> 背景颜色 </td> 
   <td colname="2"> <p>背景字符单元格颜色。 </p> <p>只能设置为可用于字体颜色的值。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> 字体不透明度 </td> 
   <td colname="2"> <p>文本的不透明度。 </p> <p>以0（完全透明）到100（完全不透明）的百分比表示。 <span class="codeph"> DEFAULT_OPACITY </span> 字体为100。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> 下内缩 </td> 
   <td colname="2"> <p>要避免的字幕与字幕窗口底部的垂直距离。 </p> <p>以题注窗口高度的百分比（例如，“20%”）或像素数（例如，“20”）表示。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> 安全区域 </td> 
   <td colname="2"> <p>屏幕边缘附近0%到25%之间不显示字幕的区域。 </p> <p>默认情况下，608/708的安全区域为12%，WebVTT的安全区域为0%。 此设置允许您的应用程序覆盖该默认值。 如果提供了两个值，例如字符串“10%，20%”，则第一个值是水平安全区域，第二个值是垂直安全区域。 如果提供一个值（例如，字符串“15%”），则垂直轴和水平轴都会使用指定的安全区域。 </p> </td> 
  </tr> 
 </tbody> 
</table>
