---
description: 要使用自定义外观，您必须编写类似于default-video-controls.css的自定义内容，并在播放器中引用此新自定义内容。
title: 自定义外观
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '218'
ht-degree: 0%

---


# 自定义外观{#custom-skins}

要使用自定义外观，您必须编写类似于default-video-controls.css的自定义内容，并在播放器中引用此新自定义内容。

例如，您可以使用以下选项之一：

* `<link rel="stylesheet" href="css/common_style.css">`
* `<link rel="stylesheet" href="css/custom-video-controls1.css">`

您可以进行以下类型的更改：

* 按钮和文本的前景色

   具有前景的所有控件都使用`vid-skin-fgcolor`类。 要更改所有控件的前景，请使用`vid-skin-fgcolor`类遍历所有元素并指定所需的颜色。
* 按钮和文本的背景颜色

   具有前景的所有控件都使用`vid-skin-bgcolor`类。 要更改所有控件的前景，请使用`vid-skin-bgcolor`类遍历所有元素并指定所需的颜色。
* 播放头的形状

   游戏头可以是方形或圆形。 要更改播放头，请向`playhead`元素添加`square`或`round`类。
* 缓冲旋转器的样式

   引用播放器提供以下旋转器样式，可在播放器缓冲内容时显示：

   * 叠加文本(`overlay-text`)
   * 矩形微调框(`spinner`)
   * 信号(`signal`)
   * 竖条(`vertical`)

      >[!TIP]
      >
      >要使用任何缓冲旋转器，必须在buffering-overlay元素中添加类。 例如，要使用`overlay-text`，请在`BufferOverlay.js`文件中添加以下行：
      >
      >
      ```js
      >var overlay = document.getElementById("buffering-overlay"); 
      >overlay.classList.add ("spinner");
      >```

