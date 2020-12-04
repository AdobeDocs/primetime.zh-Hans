---
description: 'null'
seo-description: 'null'
seo-title: 使用UI框架创建基本播放器
title: 使用UI框架创建基本播放器
uuid: d1a82dbb-1c05-4d0c-b6bc-e07cbede93cb
translation-type: tm+mt
source-git-commit: 4102780d0c7d0b96d120c1c2b3d14c47bc1b0e6f
workflow-type: tm+mt
source-wordcount: '136'
ht-degree: 1%

---


# 使用UI Framework{#create-a-basic-player-using-the-ui-framework}创建基本播放器

要使用UI框架创建基本播放器，请执行以下操作：

1. 为播放器实例创建`<div>`。

   例如：

   ```
   <div id="video1" > 
    </div>
   ```

1. 加载播放器。

   ```js
   <script> 
       (function(){ 
           var player = ptp.videoPlayer('#video1'); 
       })(); 
   </script>
   ```

   创建播放器时，指定的`<div>`元素会被赋予`ptp-main-video-div-style`的CSS类。 生成的DOM如下所示：

   ```
   <div id="video1" class="ptp-main-video-div-style"> 
       <video class="vp-video-element"></video> 
   </div>
   ```

1. 添加UI控件。

   例如，添加当鼠标悬停在播放器上时显示的控件条：

   ```js
   <script> 
       (function(){ 
           function myControlBarBehavior(element, configuration, player) { 
               return ptp.controlBarBehavior(element, configuration, player); 
           } 
           var player = ptp.videoPlayer('#video1', { 
               controlBar: { 
                   behavior: myControlBarBehavior, 
                   classNames: 'ptp-control-bar my_control_bar' 
               } 
           }); 
       })(); 
   </script>
   ```

   生成的DOM如下所示：

   ```
   <div id="video1" class="ptp-main-video-div-style"> 
       <div class="ptp-control-bar my_control_bar"></div> 
       <video class="vp-video-element"></video> 
   </div>
   ```

调用`ptp.videoPlayer()`返回的对象提供了一种行为，该行为包含TVSDK媒体播放器API并允许程序化控制播放。 当您对媒体播放器实例进行调用时，用户界面会根据媒体播放器触发的事件自行更新：

```js
<script> 
    (function(){ 
        var player = ptp.videoPlayer('#video1'); 
        player.loadResource( 'sample.mp4' ); 
    })(); 
</script>
```
