---
description: 您可以指定多个题注样式选项，这些选项会覆盖原始题注中的样式选项。
title: 隐藏字幕样式选项
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '349'
ht-degree: 0%

---


# 隐藏字幕样式选项{#closed-caption-styling-options}

您可以指定多个题注样式选项，这些选项会覆盖原始题注中的样式选项。

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
>在定义默认值（例如`DEFAULT`）的选项中，该值引用最初指定题注时的设置。

<table frame="all" colsep="1" rowsep="1" id="table_87205DEFEE384AF4AF83952B15E18A42"> 
 <thead> 
  <tr rowsep="1"> 
   <th colname="1" class="entry"> 格式 </th> 
   <th colname="2" class="entry"> 说明 </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr rowsep="1"> 
   <td colname="1"> 字体 </td> 
   <td colname="2"> <p>字体类型。 </p> <p>只能设置为由<span class="codeph"> TextFormat.Font </span>明细列表定义的值，并表示（例如，带有或不带序列）的等间距。 </p> <p>提示： 设备上可用的实际字体可能有所不同，并在必要时使用替代。 带serif的单空间通常用作替代，尽管这种替代可以是系统特定的。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> 大小 </td> 
   <td colname="2"> <p>题注的大小。 </p> <p> 只能设置为由<span class="codeph"> TextFormat.Size </span>明细列表定义的值： 
     <ul compact="yes" id="ul_544BFC7A46474A74839477108F1AB1E9"> 
      <li id="li_A592ED46B8DF4D8FAD7AF3BD931A712B"> <span class="codeph"> 中 —  </span> 标准大小 </li> 
      <li id="li_4F8CEDE54965430EB707DD3D5B2E3F87"> <span class="codeph"> 大 —  </span> 比中大约30% </li> 
      <li id="li_D78D823883F54D869118BAB58257E377"> <span class="codeph"> 小 —  </span> 比中小约30% </li> 
      <li id="li_9299C13408584A38835F8D91BD048083"> <span class="codeph"> 默 </span> 认 — 题注的默认大小；与介质相同 </li> 
     </ul> </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> 字体颜色 </td> 
   <td colname="2"> <p>字体颜色。 </p> <p>只能设置为由<span class="codeph"> TextFormat.Color </span>明细列表定义的值。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> 背景颜色 </td> 
   <td colname="2"> <p>背景字符单元格颜色。 </p> <p>只能设置为可用于字体颜色的值。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> 字体不透明度 </td> 
   <td colname="2"> <p>文本的不透明度。 </p> <p>表示为0（完全透明）到100（完全不透明）之间的百分比。 <span class="codeph"> 字体的 </span> DEFAULT_OPACITY为100。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> 底嵌 </td> 
   <td colname="2"> <p>字幕窗口底部的垂直距离可避免字幕出现。 </p> <p>表示为题注窗口高度的百分比（例如“20%”）或像素数（例如“20”）。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> 安全区 </td> 
   <td colname="2"> <p>屏幕边缘周围0%到25%之间的区域，不显示字幕。 </p> <p>默认情况下，608/708的安全区域为12%，而WebVTT的安全区域为0%。 此设置允许应用程序覆盖该默认设置。 如果提供了两个值，例如字符串"10%,20%"，则第一个值是水平安全区，第二个值是垂直安全区。 如果提供了一个值，例如字符串"15%"，则垂直轴和水平轴都使用指定的安全区域。 </p> </td> 
  </tr> 
 </tbody> 
</table>

