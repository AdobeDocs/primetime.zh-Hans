---
description: 可以使用ClosedCaptionStyles类为隐藏式字幕轨道提供样式信息。 这将设置播放器显示的任何隐藏式字幕的样式。
seo-description: 可以使用ClosedCaptionStyles类为隐藏式字幕轨道提供样式信息。 这将设置播放器显示的任何隐藏式字幕的样式。
seo-title: 控制隐藏式字幕样式
title: 控制隐藏式字幕样式
uuid: 506c06d3-8fe0-46c9-9ed6-5b35d21c021c
translation-type: tm+mt
source-git-commit: b67a9dcb0abb07f4fdff4e03d9d6c0b07ff45127

---


# 控制隐藏式字幕样式{#control-closed-caption-styling}

可以使用ClosedCaptionStyles类为隐藏式字幕轨道提供样式信息。 这将设置播放器显示的任何隐藏式字幕的样式。

此类封装隐藏式字幕样式信息，如字体类型、大小、颜色和背景不透明度。 关联的帮助类 `ClosedCaptionStylesBuilder`便于使用隐藏式字幕样式设置。

## 设置隐藏式字幕样式 {#section_DAE84659D1964DB1B518F91B59AF29D9}

可以使用TVSDK方法设置隐藏式字幕文本的样式。

1. 等待MediaPlayer至少拥有PREPARED状态(请参 [阅等待有效状态](../../../tvsdk-1.4-for-desktop-hls/t-psdk-dhls-1.4-configure/c-psdk-dhls-1.4-ui-configure/t-psdk-dhls-1.4-ui-state-prepared-wait-for.md))。
1. 要更改样式设置，请执行下列操作之一：

   * 使用帮 `ClosedCaptionStylesBuilder` 助程序类(在幕 `ClosedCaptionStyles` 后操作)。
   * 直接使 `ClosedCaptionStyles` 用类。

>[!NOTE]
>
>设置隐藏式字幕样式是一种异步操作，因此更改可能需要最长几秒钟才能显示在屏幕上。

## 隐藏式字幕样式选项 {#section_D28F50B98C0D48CF89C4FB6DC81C5185}

您可以使用类为隐藏式字幕轨道提供样式 `ClosedCaptionStyles` 信息。 这将设置播放器显示的任何隐藏式字幕的样式。

```
public function TextFormat( 
   font:String = default,  
   size:String = default,  
   fontEdge:String = default,  
   fontColor:String = default,  
   backgroundColor:String = default,  
   fillColor:String = default,  
   edgeColor:String = default,  
   fontOpacity:int,  
   backgroundOpacity:int,  
   fillOpacity:int)
```

>[!TIP]
>
>在定义默认值(例如， `DEFAULT`)的选项中，该值引用最初指定题注时的设置。

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
   <td colname="2"> <p>字体类型。 </p> <p>只能设置为由 <span class="codeph"></span> ClosedCaptionStyles.FONT数组定义的值，并表示（例如，有或没有serif）等间距。 
     <code class="syntax actionscript">
       public&nbsp;static&nbsp;const&nbsp;FONT&nbsp;:Array&nbsp;=&nbsp;[ 
      &nbsp;AVCaptionStyle.DEFAULT, 
      &nbsp;AVCaptionStyle.MONOSPACE_WITH_SERIFS, 
      &nbsp;AVCaptionStyle.MONOSPACED_WITHOUT_SERIFS, 
      &nbsp;AVCaptionStyle.PROPORTIONAL_WITH_SERIFS, 
      &nbsp;AVCaptionStyle.PROPORTIONAL_WITHOUT_SERIFS, 
      &nbsp;AVCaptionStyle.CASUAL, 
      &nbsp;AVCaptionStyle.CURSIVE, 
      &nbsp;AVCaptionStyle.SMALL_CAPITALS 
      &nbsp;]; 
     </code> </p> <p>提示： 设备上可用的实际字体可能会有所不同，并在必要时使用替换。 带serifs的单空间通常用作替代，尽管这种替代可以是系统特定的。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> 大小 </td> 
   <td colname="2"> <p>题注的大小。 </p> <p> 只能设置为由ClosedCaptionStyles.FONT_SIZE数组定 <span class="codeph"> 义的 </span> 值： 
     <ul compact="yes" id="ul_544BFC7A46474A74839477108F1AB1E9"> 
      <li id="li_A592ED46B8DF4D8FAD7AF3BD931A712B"> <span class="codeph"> 中 </span> 型——标准尺寸 </li> 
      <li id="li_4F8CEDE54965430EB707DD3D5B2E3F87"> <span class="codeph"> 大- </span> 大约比中大30% </li> 
      <li id="li_D78D823883F54D869118BAB58257E377"> <span class="codeph"> 小 </span> 型——大约比中型小30% </li> 
      <li id="li_9299C13408584A38835F8D91BD048083"> <span class="codeph"> 默 </span> 认——题注的默认大小；与介质相同 </li> 
     </ul> </p> <p>提示： 通过更改DefaultMediaPlayer.ccStyles setter函数的size参数，可以更改WebVTT字幕的 <span class="codeph"> 字体大 </span> 小。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> 字体边缘 </td> 
   <td colname="2"> <p>用于字体边缘的效果，如凸起或无。 </p> <p>只能设置为由ClosedCaptionStyles.FONT_EDGE数组定 <span class="codeph"> 义的 </span> 值。 
     <code class="syntax actionscript">
       public&nbsp;static&nbsp;const&nbsp;FONT_EDGE&nbsp;:Array&nbsp;=&nbsp;[ 
      &nbsp;&nbsp;&nbsp;&nbsp;AVCaptionStyle.DEFAULT, 
      &nbsp;&nbsp;&nbsp;&nbsp;AVCaptionStyle.NONE, 
      &nbsp;&nbsp;&nbsp;&nbsp;AVCaptionStyle.RAISED, 
      &nbsp;&nbsp;&nbsp;&nbsp;AVCaptionStyle.DEPRESSED, 
      &nbsp;&nbsp;&nbsp;&nbsp;AVCaptionStyle.UNIFORM, 
      &nbsp;&nbsp;&nbsp;&nbsp;AVCaptionStyle.LEFT_DROP_SHADOW, 
      &nbsp;&nbsp;&nbsp;&nbsp;AVCaptionStyle.RIGHT_DROP_SHADOW 
      &nbsp;]; 
     </code> </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> 字体颜色 </td> 
   <td colname="2"> <p>字体颜色。 </p> <p>只能设置为由ClosedCaptionStyles.COLOR数组定 <span class="codeph"> 义的 </span> 值。 
     <code class="syntax actionscript">
       public&nbsp;static&nbsp;const&nbsp;COLOR&nbsp;:Array&nbsp;=&nbsp;[ 
      &nbsp;&nbsp;&nbsp;&nbsp;AVCaptionStyle.DEFAULT, 
      &nbsp;&nbsp;&nbsp;&nbsp;AVCaptionStyle.BLACK, 
      &nbsp;&nbsp;&nbsp;&nbsp;AVCaptionStyle.GRAY, 
      &nbsp;&nbsp;&nbsp;&nbsp;AVCaptionStyle.WHITE, 
      &nbsp;&nbsp;&nbsp;&nbsp;AVCaptionStyle.BRIGHT_WHITE, 
      &nbsp;&nbsp;&nbsp;&nbsp;AVCaptionStyle.RED, 
      &nbsp;&nbsp;&nbsp;&nbsp;AVCaptionStyle.DARK_RED, 
      &nbsp;&nbsp;&nbsp;&nbsp;AVCaptionStyle.BRIGHT_RED, 
      &nbsp;&nbsp;&nbsp;&nbsp;AVCaptionStyle.GREEN, 
      &nbsp;&nbsp;&nbsp;&nbsp;AVCaptionStyle.DARK_GREEN, 
      &nbsp;&nbsp;&nbsp;&nbsp;AVCaptionStyle.BRIGHT_GREEN, 
      &nbsp;&nbsp;&nbsp;&nbsp;AVCaptionStyle.BLUE, 
      &nbsp;&nbsp;&nbsp;&nbsp;AVCaptionStyle.DARK_BLUE, 
      &nbsp;&nbsp;&nbsp;&nbsp;AVCaptionStyle.BRIGHT_BLUE, 
      &nbsp;&nbsp;&nbsp;&nbsp;AVCaptionStyle.YELLOW, 
      &nbsp;&nbsp;&nbsp;&nbsp;AVCaptionStyle.DARK_YELLOW, 
      &nbsp;&nbsp;&nbsp;&nbsp;AVCaptionStyle.BRIGHT_YELLOW, 
      &nbsp;&nbsp;&nbsp;&nbsp;AVCaptionStyle.MAGENTA, 
      &nbsp;&nbsp;&nbsp;&nbsp;AVCaptionStyle.DARK_MAGENTA, 
      &nbsp;&nbsp;&nbsp;&nbsp;AVCaptionStyle.BRIGHT_MAGENTA, 
      &nbsp;&nbsp;&nbsp;&nbsp;AVCaptionStyle.CYAN, 
      &nbsp;&nbsp;&nbsp;&nbsp;AVCaptionStyle.DARK_CYAN, 
      &nbsp;&nbsp;&nbsp;&nbsp;AVCaptionStyle.BRIGHT_CYAN&nbsp;&nbsp;&nbsp;]; 
     </code> </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> 边缘颜色 </td> 
   <td colname="2"> <p>边缘效果的颜色。 </p> <p>可以设置为任何可用于字体颜色的值。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> 背景颜色 </td> 
   <td colname="2"> <p>背景字符单元格颜色。 </p> <p>只能设置为可用于字体颜色的值。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> 填充颜色 </td> 
   <td colname="2"> <p>文本所在窗口的背景颜色。 </p> <p>可以设置为任何可用于字体颜色的值。 </p> <p>重要说明： 这不适用于WebVTT字幕，因为WebVTT不使用此功能。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> 字体不透明度 </td> 
   <td colname="2"> <p>文本的不透明度。 </p> <p>以0（完全透明）到100（完全不透明）的百分比表示。 <span class="codeph"> 字体的DEFAULT_ </span> OPACITY为100。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> 背景不透明度 </td> 
   <td colname="2"> <p>背景字符单元格的不透明度。 </p> <p>以0（完全透明）到100（完全不透明）的百分比表示。 <span class="codeph"> 背景的DEFAULT_ </span> OPACITY为100。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> 填充不透明度 </td> 
   <td colname="2"> <p>题注窗口背景的不透明度。 </p> <p>以0（完全透明）到100（完全不透明）的百分比表示。 <span class="codeph"> 填充的DEFAULT_ </span> OPACITY为0。 </p> </td> 
  </tr> 
 </tbody> 
</table>

## 示例：题注格式化 {#section_63E33840B7A14D26990046E2ACF2ECA1}

您可以指定隐藏式字幕格式。

## 示例1:显式指定格式值 {#section_BD7B48F3B66D4E9290E1CB2F464E08E4}

```
private function onStatusChanged(event:MediaPlayerStatusChangeEvent):void { 
    var formatBuilder:TextFormatBuilder = new TextFormatBuilder(); 
    formatBuilder.font = Font.DEFAULT,  
    formatBuilder.fontSize = FontSize.DEFAULT,  
    formatBuilder.fontEdge = FontEdge.DEFAULT,  
    formatBuilder.fontColor = Color.DEFAULT,  
    formatBuilder.backgroundColor = Color.DEFAULT,  
    formatBuilder.fillColor = Color.DEFAULT,  
    formatBuilder.edgeColor = Color.DEFAULT,  
    formatBuilder.fontOpacity = .DEFAULT_OPACITY,  
    formatBuilder.backgroundOpacity = Font.DEFAULT_OPACITY,  
    formatBuilder.fillOpacity = TextFormat.DEFAULT_OPACITY 
    mediaPlayer.set CCStyle(formatBuilder.toTextFormat()); 
} 
```

## 示例2:在参数中指定格式值 {#section_147036D7C31C4010A5A7DF49997014A9}

```
/** 
* Constructor using parameters to initialize a TextFormat. 
* 
* @param font 
* The desired font. 
* @param fontSize 
* The desired text size. 
* @param fontEdge 
* The desired font edge. 
* @param fontColor 
* The desired font color. 
* @param backgroundColor 
* The desired background color. 
* @param fillColor 
* The desired fill color. 
* @param edgeColor 
* The desired color to draw the text edges. 
* @param fontOpacity 
* The desired font opacity. 
* @param backgroundOpacity 
* The desired background opacity. 
* @param fillOpacity 
* The desired fill opacity. 
*/ 
public function TextFormatBuilder(font:Font, fontSize:FontSize, fontEdge:FontEdge,  
                                  fontColor:Color, backgroundColor:Color,  
                                  fillColor:Color, edgeColor:Color, fontOpacity:int, 
                                  backgroundOpacity:int, fillOpacity:int); 
/** 
* Creates a TextFormat with the parameters supplied to this builder. 
*/ 
public function toTextFormat():TextFormat; 
... 
```
