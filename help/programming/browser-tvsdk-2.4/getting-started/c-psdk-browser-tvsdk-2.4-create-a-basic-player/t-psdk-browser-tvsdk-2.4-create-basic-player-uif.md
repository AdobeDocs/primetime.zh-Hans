---
description: 'null'
seo-description: 'null'
seo-title: 使用UI框架创建基本播放器
title: 使用UI框架创建基本播放器
uuid: d1a82dbb-1c05-4d0c-b6bc-e07cbede93cb
translation-type: tm+mt
source-git-commit: 4102780d0c7d0b96d120c1c2b3d14c47bc1b0e6f

---


# 使用UI框架创建基本播放器{#create-a-basic-player-using-the-ui-framework}

要使用UI框架创建基本播放器，请执行以下操作：

1. 为您的 `<div>` 播放器实例创建。

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

   创建播放器时，将为指 `<div>` 定的元素提供CSS类 `ptp-main-video-div-style`。 生成的DOM显示如下：

   ```
   <div id="video1" class="ptp-main-video-div-style"> 
       <video class="vp-video-element"></video> 
   </div>
   ```

1. 添加UI控件。

   例如，添加当鼠标悬停在播放器上时显示的控件栏：

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

调用返回的对象提 `ptp.videoPlayer()` 供了一种行为，该行为将TVSDK媒体播放器API封装起来，并允许程序化控制播放。 当您对媒体播放器实例进行调用时，用户界面会根据媒体播放器触发的事件自我更新：

```js
<script> 
    (function(){ 
        var player = ptp.videoPlayer('#video1'); 
        player.loadResource( 'sample.mp4' ); 
    })(); 
</script>
```
