---
description: 您可以使用TextFormat类为隐藏字幕轨道提供样式信息，该类设置由播放器显示的隐藏字幕的样式。
seo-description: 您可以使用TextFormat类为隐藏字幕轨道提供样式信息，该类设置由播放器显示的隐藏字幕的样式。
seo-title: 控制隐藏式字幕样式
title: 控制隐藏式字幕样式
uuid: fa4f637f-f13c-465d-8eee-5e66a6dd9db2
translation-type: tm+mt
source-git-commit: 5df9a8b98baaf1cd1803581d2b60c7ed4261a0e8
workflow-type: tm+mt
source-wordcount: '882'
ht-degree: 0%

---


# 控制隐藏式字幕样式 {#control-closed-caption-styling}

您可以使用TextFormat类为隐藏字幕轨道提供样式信息，该类设置由播放器显示的隐藏字幕的样式。

此类封装隐藏式字幕样式信息，如字体类型、大小、颜色和背景不透明度。

## 设置隐藏字幕样式 {#section_C9B5E75C70DD42E59DC4DD0F308C8216}

可以使用TVSDK方法设置隐藏字幕文本的样式。

1. 等待媒体播放器至少处于该状 `PREPARED` 态。
1. 创建实 `TextFormatBuilder` 例。

   您现在可以提供所有隐藏式字幕样式参数，也可以稍后设置。

   TVSDK将隐藏字幕样式信息封装在界 `TextFormat` 面中。 类创 `TextFormatBuilder` 建实现此接口的对象。

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

1. 要获取对实现该接口的对象的引 `TextFormat` 用，请调用 `TextFormatBuilder.toTextFormat` public方法。

   >[!NOTE]
   >
   >这将返回 `TextFormat` 可应用于媒体播放器的对象。

   ```java
   public TextFormat toTextFormat()
   ```

1. （可选）通过执行下列操作之一来获取当前隐藏式字幕样式设置：

   * 获取所有样式设置， `MediaPlayer.getCCStyle` 其中返回值是界面的一个 `TextFormat` 实例。

      ```java
      /** 
      * @return the current closed captioning style.  
      * If no style was previously set, it returns a TextFormat object 
      * with default values for each attribute. 
      * @throws MediaPlayerException if media player was already released. 
      */ 
      public TextFormat getCCStyle() throws MediaPlayerException;
      ```

   * 通过接口getter方法，一次只获 `TextFormat` 取一个设置。

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

   * 使用setter方 `MediaPlayer.setCCStyle`法，传递接口的实 `TextFormat` 例：

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

   * 使用类 `TextFormatBuilder` ，它定义单个setter方法。

      接 `TextFormat` 口定义不可变的对象，因此只有getter方法和没有setter。 您只能使用类设置隐藏字幕样式 `TextFormatBuilder` 参数：

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
      >**颜色设置：** 在Android TVSDK 2.X中，对隐藏式字幕的颜色样式进行了增强。 该增强功能允许使用表示RGB颜色值的十六进制字符串设置隐藏字幕颜色。 RGB十六进制颜色表示法是您在诸如Photoshop之类的应用程序中使用的熟悉的6字节字符串：
      >
      >    * FFFFFF =黑色
      >    * 000000 =白色
      >    * FF0000 =红色
      >    * 00FF00 =绿色
      >    * 0000FF =蓝色

      >
      >等等。
      >
      >在应用程序中，无论何时将颜色样 `TextFormatBuilder`式信息传递给 `Color` ，您仍然像以前一样使用明细列表，但现在必须添加到颜色 `getValue()` 中才能将值作为字符串获得。 例如：

      ```
      tfb = tfb.setBackgroundColor(TextFormat.Color.RED <b>.getValue()</b>);
      ```




设置隐藏式字幕样式是一个异步操作，因此更改可能需要几秒钟时间才能显示在屏幕上。

## 隐藏字幕样式选项 {#section_6D685EC2D58C42A2BDDD574EDFCCC2A0}

您可以指定多个题注样式选项，这些选项将覆盖原始题注中的样式选项。

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
在定义默认值的选项(例 `DEFAULT`如，)中，该值指最初指定字幕时的设置。

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
   <td colname="2"> <p>字体类型。 </p> <p>只能设置为由TextFormat.Font明细列表定 <span class="codeph"> 义并表示 </span> 的值，例如，单隔带或不带序列。 </p> <p>提示： 设备上可用的实际字体可能有所不同，并在必要时使用替换。 带serifs的单空间通常用作替代，尽管这种替代可以是系统特定的。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> 大小 </td> 
   <td colname="2"> <p>题注的大小。 </p> <p> 只能设置为由TextFormat.Size明细列表定 <span class="codeph"> 义的 </span> 值： 
     <ul compact="yes" id="ul_544BFC7A46474A74839477108F1AB1E9"> 
      <li id="li_A592ED46B8DF4D8FAD7AF3BD931A712B"> <span class="codeph"> 中- </span> 标准大小 </li> 
      <li id="li_4F8CEDE54965430EB707DD3D5B2E3F87"> <span class="codeph"> 大 </span> -比中大约30% </li> 
      <li id="li_D78D823883F54D869118BAB58257E377"> <span class="codeph"> 小 </span> -比中小约30% </li> 
      <li id="li_9299C13408584A38835F8D91BD048083"> <span class="codeph"> 默 </span> 认——题注的默认大小；与介质相同 </li> 
     </ul> </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> 字体边缘 </td> 
   <td colname="2"> <p>用于字体边缘的效果，如凸起或无。 </p> <p>只能设置为由TextFormat.FontEdge明细列表定 <span class="codeph"> 义的 </span> 值。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> 字体颜色 </td> 
   <td colname="2"> <p>字体颜色。 </p> <p>只能设置为由TextFormat.Color明细列表定 <span class="codeph"> 义的 </span> 值。 </p> </td> 
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
   <td colname="2"> <p>文本所在窗口的背景颜色。 </p> <p>可以设置为任何可用于字体颜色的值。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> 字体不透明度 </td> 
   <td colname="2"> <p>文本的不透明度。 </p> <p>以0（完全透明）到100（完全不透明）的百分比表示。 <span class="codeph"> 字体的 </span> DEFAULT_OPACITY为100。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> 背景不透明度 </td> 
   <td colname="2"> <p>背景字符单元格的不透明度。 </p> <p>以0（完全透明）到100（完全不透明）的百分比表示。 <span class="codeph"> 背景的 </span> DEFAULT_OPACITY为100。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> 填充不透明度 </td> 
   <td colname="2"> <p>题注窗口背景的不透明度。 </p> <p>以0（完全透明）到100（完全不透明）的百分比表示。 <span class="codeph"> 填充的DEFAULT_ </span> OPACITY为0。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> 底部插入 </td> 
   <td colname="2"> <p>字幕窗口底部的垂直距离可避免出现。 </p> <p>表示为题注窗口高度的百分比（例如“20%”）或像素数（例如“20”）。 </p> </td> 
  </tr> 
  <tr rowsep="0"> 
   <td colname="1"> 安全区域 </td> 
   <td colname="2"> <p>屏幕边缘周围的一个区域，在0%到25%之间不显示字幕。 </p> <p>默认情况下，WebVTT的安全区域为0%。 此设置允许应用程序覆盖该默认值。 如果提供了两个值，例如字符串“10%,20%”，则第一个值是水平安全区，第二个值是垂直安全区。 如果提供一个值，例如字符串“15%”，则垂直轴和水平轴都使用指定的安全区域。 </p> </td> 
  </tr> 
 </tbody> 
</table>

## 题注格式示例 {#section_58E8E82494EC4683B010FFDE67485CF9}

以下是一些示例，用于说明如何指定隐藏式字幕格式。

**示例1:显式指定格式值**

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

**示例2:在参数中指定格式值**

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
