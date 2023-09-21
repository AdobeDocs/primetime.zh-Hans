---
description: 要使用自定义外观，必须编写与default-video-controls.css类似的自定义设置，并在播放器中引用此新自定义设置。
title: 自定义外观
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '218'
ht-degree: 0%

---

# 自定义外观{#custom-skins}

要使用自定义外观，必须编写与default-video-controls.css类似的自定义设置，并在播放器中引用此新自定义设置。

例如，您可以使用以下选项之一：

* `<link rel="stylesheet" href="css/common_style.css">`
* `<link rel="stylesheet" href="css/custom-video-controls1.css">`

您可以进行以下类型的更改：

* 按钮和文本的前景色

  所有具有前景的控件都使用 `vid-skin-fgcolor` 类。 要更改所有控件的前景，请使用 `vid-skin-fgcolor` 类并指定所需的颜色。
* 按钮和文本的背景颜色

  所有具有前景的控件都使用 `vid-skin-bgcolor` 类。 要更改所有控件的前景，请使用以下方式迭代所有元素 `vid-skin-bgcolor` 类并指定所需的颜色。
* 播放头形状

  播放头可以是方形或圆形。 要更改播放头，请添加 `square` 或 `round` 分类至 `playhead` 元素。
* 缓冲旋转器的样式

  引用播放器提供了以下旋转器样式，这些样式可在播放器缓冲内容时显示：

   * 叠加文本( `overlay-text`)
   * 矩形旋转图标( `spinner`)
   * 信号( `signal`)
   * 垂直条( `vertical`)

     >[!TIP]
     >
     >要使用任何缓冲旋转器，必须在buffering-overlay元素中添加类。 例如，要使用 `overlay-text`，将以下行添加到 `BufferOverlay.js` 文件：
     >
     >```js
     >var overlay = document.getElementById("buffering-overlay"); 
     >overlay.classList.add ("spinner");
     >```
     >
