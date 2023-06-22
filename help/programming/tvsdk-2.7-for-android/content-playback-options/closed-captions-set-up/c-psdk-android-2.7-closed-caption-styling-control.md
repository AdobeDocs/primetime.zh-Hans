---
description: 您可以使用TextFormat类为隐藏式字幕轨道提供样式信息，该类设置播放器显示的隐藏式字幕的样式。
title: 控制隐藏式字幕样式
exl-id: fa96f9f5-f709-4749-90c8-cf237cf074c0
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '853'
ht-degree: 0%

---

# 控制隐藏式字幕样式 {#control-closed-caption-styling}

您可以使用TextFormat类为隐藏式字幕轨道提供样式信息，该类设置播放器显示的隐藏式字幕的样式。

此类封装隐藏式字幕样式信息，如字体类型、大小、颜色和背景不透明度。

## 设置隐藏式字幕样式 {#section_C9B5E75C70DD42E59DC4DD0F308C8216}

您可以使用TVSDK方法设置隐藏式字幕文本的样式。

1. 等待媒体播放器至少处于 `PREPARED` 状态。
1. 创建 `TextFormatBuilder` 实例。

   您可以现在提供所有隐藏式字幕样式参数，也可以稍后设置它们。

   TVSDK将隐藏式字幕样式信息封装在 `TextFormat` 界面。 此 `TextFormatBuilder` 类创建实现此接口的对象。

   ```java
   public TextFormatBuilder( 
      TextFormat.Font font, 
      TextFormat.Size size, 
      TextFormat.FontEdge fontEdge, 
      java.lang.String fontColor, 
      java.lang.String backgroundColor, 
      java.lang.String fillColor, 
      java.lang.String edgeColor, 
      int fontOpacity, 
      int backgroundOpacity, 
      int fillOpacity 
      java.lang.String bottomInset, 
      java.lang.String safeArea)
   ```

1. 获取对实现 `TextFormat` 界面，调用 `TextFormatBuilder.toTextFormat` 公共方法。

   >[!NOTE]
   >
   >这会返回 `TextFormat` 可应用于媒体播放器的对象。

   ```java
   public TextFormat toTextFormat()
   ```

1. （可选）通过执行以下操作之一获取当前隐藏式字幕样式设置：

   * 使用以下方式获取所有样式设置 `MediaPlayer.getCCStyle` 返回值是 `TextFormat` 界面。

      ```java
      /** 
      * @return the current closed captioning style.  
      * If no style was previously set, it returns a TextFormat object 
      * with default values for each attribute. 
      * @throws MediaPlayerException if media player was already released. 
      */ 
      public TextFormat getCCStyle() throws MediaPlayerException;
      ```

   * 通过，逐个获取设置 `TextFormat` 接口getter方法。

      ```java
      public java.lang.String getFontColor(); 
      public java.lang.String getBackgroundColor(); 
      public java.lang.String getFillColor(); // retrieve the font fill color 
      public java.lang.String getEdgeColor(); // retrieve the font edge color 
      public TextFormat.Size getSize(); // retrieve the font size 
      public TextFormat.FontEdge getFontEdge(); // retrieve the font edge type 
      public TextFormat.Font getFont(); // retrieve the font type 
      public int getFontOpacity(); 
      public int getBackgroundOpacity(); 
      public java.lang.String getBottomInset(java.lang.String bi); 
      public java.lang.String getSafeArea(java.lang.String sa);
      ```

1. 要更改样式设置，请执行下列操作之一：

   * 使用setter方法 `MediaPlayer.setCCStyle`，传递的实例 `TextFormat` 界面：

      ```java
      /** 
      * Sets the closed captioning style. Used to control the closed captioning font, 
      * size, color, edge and opacity.  
      * 
      * This method is safe to use even if the current media stream doesn't have closed 
      * captions. 
      * 
      * @param textFormat 
      * @throws MediaPlayerException 
      */ 
      public void setCCStyle(TextFormat textFormat) throws MediaPlayerException;
      ```

   * 使用 `TextFormatBuilder` 类，用于定义单独的setter方法。

      此 `TextFormat` interface定义了一个不可变对象，因此只有getter方法而没有setter方法。 只能使用设置隐藏式字幕样式参数 `TextFormatBuilder` 类：

      ```java
      // set font type 
      public void setFont(Font font)  
      public void setBackgroundColor(String backgroundColor) 
      public void setFillColor(String fillColor) 
      // set the font-edge color 
      public void setEdgeColor(String edgeColor)  
      // set the font size 
      public void setSize(Size size)  
      // set the font edge type 
      public void setFontEdge(FontEdge fontEdge)  
      public void setFontOpacity(int fontOpacity) 
      public void setBackgroundOpacity(int backgroundOpacity) 
      // set the font-fill opacity level 
      public void setFillOpacity(int fillOpacity)  
      public void setFontColor(String fontColor) 
      public void setBottomInset(String bi) 
      public void setSafeArea(String sa) 
      public void setTreatSpaceAsAlphaNum(bool)
      ```

      >[!IMPORTANT]
      >
      >**颜色设置：** 在Android TVSDK 2.X中，对隐藏式字幕的颜色样式进行了增强。 增强功能允许使用表示RGB颜色值的十六进制字符串设置隐藏字幕颜色。 RGB十六进制颜色表示是您在Photoshop等应用程序中使用的熟悉6字节字符串：
      >
      >* FFFFFF =黑色
      >* 000000 =白色
      >* FF0000 =红色
      >* 00FF00 =绿色
      >* 0000FF =蓝色

      >
      >等等。
      >
      >在您的应用程序中，每当您将颜色样式信息传递到 `TextFormatBuilder`，您仍会使用 `Color` 枚举与以前一样，但现在您必须添加 `getValue()` 颜色来获取字符串形式的值。 例如：
      >
      >
      ```
      >tfb = tfb.setBackgroundColor(TextFormat.Color.RED <b>.getValue()</b>);
      >```

设置隐藏式字幕样式是一种异步操作，因此可能需要几秒钟才能在屏幕上显示更改。

## 隐藏式字幕样式选项 {#section_6D685EC2D58C42A2BDDD574EDFCCC2A0}

您可以指定多个字幕样式选项，这些选项将覆盖原始字幕中的样式选项。

```java
public TextFormatBuilder( 
   Font font, 
   Size size, 
   FontEdge fontEdge, 
   String fontColor, 
   String backgroundColor, 
   String fillColor, 
   String edgeColor, 
   int fontOpacity, 
   int backgroundOpacity, 
   int fillOpacity,  
   String bottomInset 
   String safeArea)
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
   <td colname="2"> <p>字体类型。 </p> <p>只能设置为由定义的值 <span class="codeph"> TextFormat.Font </span> 枚举并表示，例如，带或不带衬线的等宽。 </p> <p>提示：设备上可用的实际字体可能有所不同，必要时会使用替换。 带有衬线的等宽通常用作替换，尽管此替换可以是系统特定的。 </p> </td> 
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
   <td colname="2"> <p>字体颜色。 </p> <p>只能设置为由 <span class="codeph"> 文本格式。颜色 </span> 明细列表。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> 边缘颜色 </td> 
   <td colname="2"> <p>边缘效果的颜色。 </p> <p>可以设置为字体颜色可用的任何值。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> 背景颜色 </td> 
   <td colname="2"> <p>背景字符单元格颜色。 </p> <p>只能设置为可用于字体颜色的值。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> 填充颜色 </td> 
   <td colname="2"> <p>文本所在窗口背景的颜色。 </p> <p>可以设置为字体颜色可用的任何值。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> 字体不透明度 </td> 
   <td colname="2"> <p>文本的不透明度。 </p> <p>以0（完全透明）到100（完全不透明）的百分比表示。 <span class="codeph"> DEFAULT_OPACITY </span> 对于，字体为100。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> 背景不透明度 </td> 
   <td colname="2"> <p>背景字符单元格的不透明度。 </p> <p>以0（完全透明）到100（完全不透明）的百分比表示。 <span class="codeph"> DEFAULT_OPACITY </span> 背景为100。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> 填充不透明度 </td> 
   <td colname="2"> <p>字幕窗口背景的不透明度。 </p> <p>以0（完全透明）到100（完全不透明）的百分比表示。 <span class="codeph"> DEFAULT_OPACITY </span> 表示填充为0。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> 下内凹 </td> 
   <td colname="2"> <p>要避免的字幕与字幕窗口底部的垂直距离。 </p> <p>以字幕窗口高度的百分比（例如“20%”）或像素数（例如“20”）表示。 </p> </td> 
  </tr> 
  <tr rowsep="0"> 
   <td colname="1"> 安全区域 </td> 
   <td colname="2"> <p>屏幕边缘附近0%到25%之间不显示字幕的区域。 </p> <p>默认情况下，WebVTT的安全区域为0%。 此设置允许您的应用程序覆盖该默认值。 如果提供了两个值，例如，字符串“10%，20%”，则第一个值是水平安全区域，第二个值是垂直安全区域。 如果提供一个值（例如，字符串“15%”），则垂直轴和水平轴都会使用指定的安全区域。 </p> </td> 
  </tr> 
 </tbody> 
</table>

## 题注格式示例 {#section_58E8E82494EC4683B010FFDE67485CF9}

以下示例说明了如何指定隐藏式字幕格式。

**示例1：显式指定格式值**

```java
private final MediaPlayer.PlaybackEventListener _playbackEventListener = 
  new MediaPlayer.PlaybackEventListener() { 
    @Override 
    public void onPrepared() { 
        // Set CC style. 
        TextFormat tf = new TextFormatBuilder( 
            TextFormat.Font.DEFAULT, 
            TextFormat.Size.DEFAULT, 
            TextFormat.FontEdge.DEFAULT, 
            TextFormat.Color.DEFAULT.getValue(), 
            TextFormat.Color.DEFAULT.getValue(), 
            TextFormat.Color.DEFAULT.getValue(), 
            TextFormat.Color.DEFAULT.getValue(), 
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
public  
<b>TextFormatBuilder</b>( 
    Font font, Size size, FontEdge fontEdge, 
    String fontColor, String backgroundColor,  
    String fillColor, String edgeColor, 
    int fontOpacity, int backgroundOpacity, 
    int fillOpacity); 
/** 
* Creates a TextFormat with the parameters supplied to this builder. 
*/ 
public TextFormat  
<b>toTextFormat</b>(); 
/** 
* Sets the text font. 
* @param font The desired font 
* @return This builder object to allow chaining calls 
*/ 
public  
<b>TextFormatBuilder</b> setFont(Font font); 
...
```
