---
description: 要使用自定义外观，您必须编写类似于default-video-controls.css的自定义内容，并在播放器中引用此新自定义内容。
seo-description: 要使用自定义外观，您必须编写类似于default-video-controls.css的自定义内容，并在播放器中引用此新自定义内容。
seo-title: 自定义外观
title: 自定义外观
uuid: bc71926e-0dec-4628-8248-911224a7a6c2
translation-type: tm+mt
source-git-commit: 5df9a8b98baaf1cd1803581d2b60c7ed4261a0e8
workflow-type: tm+mt
source-wordcount: '242'
ht-degree: 0%

---


# 自定义外观{#custom-skins}

要使用自定义外观，您必须编写类似于default-video-controls.css的自定义内容，并在播放器中引用此新自定义内容。

例如，您可以使用以下选项之一：

* `<link rel="stylesheet" href="css/common_style.css">`
* `<link rel="stylesheet" href="css/custom-video-controls1.css">`

您可以进行以下类型的更改：

* 按钮和文本的前景色

   具有前景的所有控件都使用该 `vid-skin-fgcolor` 类。 要更改所有控件的前景，请使用类遍历所有元素 `vid-skin-fgcolor` 并指定所需的颜色。
* 按钮和文本的背景颜色

   具有前景的所有控件都使用该 `vid-skin-bgcolor` 类。 要更改所有控件的前景，请使用类遍历所有元素 `vid-skin-bgcolor` 并指定所需的颜色。
* 播放头的形状

   播放头可以是方形或圆形。 要更改播放头，请向元素 `square` 添加 `round` 或类 `playhead` 别。
* 缓冲旋转器的样式

   引用播放器提供以下旋转器的样式，可在播放器缓冲内容时显示：

   * 叠加文本( `overlay-text`)
   * 矩形微调框( `spinner`)
   * 信号( `signal`)
   * 竖条( `vertical`)

      >[!TIP]
      >
      >要使用任何缓冲旋转器，必须在buffering-overlay元素中添加类。 例如，要使用 `overlay-text`，请在文件中添加以 `BufferOverlay.js` 下行：
      >
      >
      ```js
      >var overlay = document.getElementById("buffering-overlay"); 
      >overlay.classList.add ("spinner");
      >```

