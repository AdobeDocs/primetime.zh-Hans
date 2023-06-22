---
title: 使用UI框架创建基本播放器
description: 使用UI框架创建基本播放器
copied-description: true
exl-id: 78629042-fd87-406b-af42-229e34d48162
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '134'
ht-degree: 0%

---

# 使用UI框架创建基本播放器{#create-a-basic-player-using-the-ui-framework}

要使用UI框架创建基本播放器，请执行以下操作：

1. 创建 `<div>` 用于您的播放器实例。

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

   创建播放器时，指定 `<div>` 元素的CSS类为 `ptp-main-video-div-style`. 生成的DOM如下所示：

   ```
   <div id="video1" class="ptp-main-video-div-style"> 
       <video class="vp-video-element"></video> 
   </div>
   ```

1. 添加UI控件。

   例如，添加一个控制栏，当鼠标悬停在播放器上时，该栏会显示：

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

调用时返回的对象 `ptp.videoPlayer()` 提供包装TVSDK媒体播放器API的行为，并允许以编程方式控制播放。 在媒体播放器实例上调用时，用户界面会根据媒体播放器触发的事件自行更新：

```js
<script> 
    (function(){ 
        var player = ptp.videoPlayer('#video1'); 
        player.loadResource( 'sample.mp4' ); 
    })(); 
</script>
```
