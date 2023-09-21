---
description: 您可以使用TextFormat类为隐藏式字幕字幕提供样式信息。 这会设置播放器显示的任何隐藏式字幕的样式。
title: 控制隐藏式字幕样式
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '656'
ht-degree: 0%

---

# 控制隐藏式字幕样式 {#control-closed-caption-styling-overview}

您可以使用TextFormat类为隐藏式字幕字幕提供样式信息。 这会设置播放器显示的任何隐藏式字幕的样式。

此类封装隐藏式字幕样式信息，如字体类型、大小、颜色和背景不透明度。 关联的帮助程序类， `TextFormatBuilder`，更便于使用隐藏式字幕样式设置。

## 设置隐藏式字幕样式 {#set-closed-caption-styles}

您可以使用TVSDK方法设置隐藏式字幕文本的样式。

1. 等待媒体播放器至少处于“已准备”状态。
1. 创建 `TextFormatBuilder` 实例。

   您可以立即提供所有隐藏式字幕样式参数，也可以稍后设置它们。

   TVSDK将隐藏式字幕样式信息封装在 `TextFormat` 界面。 此 `TextFormatBuilder` 类创建实现此接口的对象。

   ```java
   public TextFormatBuilder( 
      Font font, 
      Size size, 
      FontEdge fontEdge, 
      Color fontColor, 
      Color backgroundColor, 
      Color fillColor, 
      Color edgeColor, 
      int fontOpacity, 
      int backgroundOpacity, 
      int fillOpacity)
   ```

1. 要获取对实现 `TextFormat` 界面，调用 `TextFormatBuilder.toTextFormat` 公共方法。

   这会返回 `TextFormat` 可应用于媒体播放器的对象。

   ```java
   public TextFormat toTextFormat()
   ```

1. （可选）通过执行以下操作之一获取当前隐藏式字幕样式设置：

   * 使用以下方式获取所有样式设置 `MediaPlayer.getCCStyle`.

     返回值是 `TextFormat` 界面。

     ```js
     /** 
     * @return the current closed captioning style.  
     * If no style was previously set, it returns a TextFormat object 
     * with default values for each attribute. 
     * @throws IllegalStateException if media player was already released. 
     */ 
     public TextFormat getCCStyle() throws IllegalStateException;
     ```

   * 通过，逐个获取设置 `TextFormat` 接口getter方法。

     ```js
     public Color getFontColor(); 
     public Color getBackgroundColor(); 
     public Color getFillColor(); // retrieve the font fill color 
     public Color getEdgeColor(); // retrieve the font edge color 
     public Size getSize(); // retrieve the font size 
     public FontEdge getFontEdge(); // retrieve the font edge type 
     public Font getFont(); // retrieve the font type 
     public int getFontOpacity(); 
     public int getBackgroundOpacity();
     ```

1. 要更改样式设置，请执行下列操作之一：

   >[!NOTE]
   >
   >无法更改WebVTT字幕的大小。

   * 使用setter方法 `MediaPlayer.setCCStyle`，传递的实例 `TextFormat` 界面：

     ```js
     /** 
     * Sets the closed captioning style. Used to control the closed captioning font, 
     * size, color, edge and opacity.  
     * 
     * This method is safe to use even if the current media stream doesn't have closed 
     * captions. 
     * 
     * @param textFormat 
     * @throws IllegalStateException 
     */ 
     public void setCCStyle(TextFormat textFormat) throws IllegalStateException;
     ```

   * 使用 `TextFormatBuilder` 类，用于定义单独的setter方法。

     此 `TextFormat` interface定义了一个不可变对象，因此只有getter方法而没有setter。 只能使用设置隐藏式字幕样式参数 `TextFormatBuilder` class：

     ```js
     // set font type 
     public void setFont(Font font)  
     public void setBackgroundColor(Color backgroundColor) 
     public void setFillColor(Color fillColor) 
     // set the font-edge color 
     public void setEdgeColor(Color edgeColor)  
     // set the font size 
     public void setSize(Size size)  
     // set the font edge type 
     public void setFontEdge(FontEdge fontEdge)  
     public void setFontOpacity(int fontOpacity) 
     public void setBackgroundOpacity(int backgroundOpacity) 
     // set the font-fill opacity level 
     public void setFillOpacity(int fillOpacity)  
     public void setFontColor(Color fontColor)
     ```

设置隐藏式字幕样式是一种异步操作，因此可能需要几秒钟才能在屏幕上显示更改。

## 隐藏式字幕样式选项 {#closed-caption-styling-options}

您可以指定多个标题样式选项，这些选项将覆盖原始标题中的样式选项

```
public TextFormatBuilder(
 Font font,
 Size size,
 FontEdge fontEdge,
 Color fontColor,
 Color backgroundColor,
 Color fillColor,
 Color edgeColor,
 int fontOpacity,
 int backgroundOpacity,
 int fillOpacity,
 String bottomInset)
```

>[!TIP]
>
>在定义默认值的选项（例如DEFAULT）中，该值是指最初指定标题时的设置。

<table frame="all" colsep="1" rowsep="1" id="table_87205DEFEE384AF4AF83952B15E18A42"> 
 <thead> 
  <tr rowsep="1"> 
   <th colname="1" class="entry"><b> 格式 </b></th> 
   <th colname="2" class="entry"> <b>描述</b> </th> 
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
   <td colname="1"> 字体边缘 </td> 
   <td colname="2"> <p>用于字体边缘的效果，如凸起或无。 </p> <p>只能设置为由定义的值 <span class="codeph"> TextFormat.FontEdge </span> 明细列表。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> 字体颜色 </td> 
   <td colname="2"> <p>字体颜色。 </p> <p>只能设置为由 <span class="codeph"> TextFormat.Color </span> 明细列表。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> 边缘颜色 </td> 
   <td colname="2"> <p>边缘效果的颜色。 </p> <p>可设置为字体颜色可用的任何值。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> 背景颜色 </td> 
   <td colname="2"> <p>背景字符单元格颜色。 </p> <p>只能设置为可用于字体颜色的值。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> 填充颜色 </td> 
   <td colname="2"> <p>文本所在窗口的背景颜色。 </p> <p>可设置为字体颜色可用的任何值。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> 字体不透明度 </td> 
   <td colname="2"> <p>文本的不透明度。 </p> <p>以0（完全透明）到100（完全不透明）的百分比表示。 <span class="codeph"> DEFAULT_OPACITY </span> 字体为100。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> 背景不透明度 </td> 
   <td colname="2"> <p>背景字符单元格的不透明度。 </p> <p>以0（完全透明）到100（完全不透明）的百分比表示。 <span class="codeph"> DEFAULT_OPACITY </span> 背景为100。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> 填充不透明度 </td> 
   <td colname="2"> <p>题注窗口背景的不透明度。 </p> <p>以0（完全透明）到100（完全不透明）的百分比表示。 <span class="codeph"> DEFAULT_OPACITY </span> 填充为0。 </p> </td> 
  </tr> 
 </tbody> 
</table>

## 题注格式示例 {#examples-caption-formatting}

您可以指定隐藏式字幕格式。

**示例1：显式指定格式值**

```java
private final MediaPlayer.PlaybackEventListener  
  _playbackEventListener = new MediaPlayer.PlaybackEventListener() { 
    @Override 
    public void onPrepared() { 
        // Set CC style. 
        TextFormat tf = new TextFormatBuilder(TextFormat.Font.DEFAULT, 
        TextFormat.Size.DEFAULT, 
        TextFormat.FontEdge.DEFAULT, 
        TextFormat.Color.DEFAULT, 
        TextFormat.Color.DEFAULT, 
        TextFormat.Color.DEFAULT, 
        TextFormat.Color.DEFAULT, 
        TextFormat.DEFAULT_OPACITY, 
        TextFormat.DEFAULT_OPACITY, 
        TextFormat.DEFAULT_OPACITY).toTextFormat(); 
        mediaPlayer.setCCStyle(tf); 
        ... 
    } 
} 
```

**示例2：在参数中指定格式值**

```java
/** 
* Constructor using parameters to initialize a TextFormat. 
* 
* @param font 
* The desired font. 
* @param size 
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
public TextFormatBuilder( 
    Font font, Size size, FontEdge fontEdge, 
    Color fontColor, Color backgroundColor,  
    Color fillColor, Color edgeColor, 
    int fontOpacity, int backgroundOpacity, 
    int fillOpacity); 
 
/** 
* Creates a TextFormat with the parameters supplied to this builder. 
*/ 
public TextFormat toTextFormat(); 
 
/** 
* Sets the text font. 
* @param font The desired font 
* @return This builder object to allow chaining calls 
*/ 
public TextFormatBuilder setFont(Font font); 
... 
```
