---
description: 您可以控制隐藏式字幕的可见性。 当可见性打开时，将显示当前选定的轨道。 如果更改当前轨道，则可见性设置保持不变。
title: 控制隐藏字幕可见性
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '209'
ht-degree: 0%

---


# 控制隐藏字幕可见性{#control-closed-caption-visibility}

您可以控制隐藏式字幕的可见性。 当可见性打开时，将显示当前选定的轨道。 如果更改当前轨道，则可见性设置保持不变。

>[!TIP]
>
>如果当播放器进入搜索模式时显示隐藏字幕文本，则在搜索完成后不再显示该文本。 相反，几秒钟后，TVSDK在结束搜索位置后在视频中显示下一个隐藏字幕文本。

>[!NOTE]
>
>隐藏式字幕的可见性值在`ClosedCaptionsVisibility`中定义。
>
>
```
>public static const HIDDEN:String = hidden; 
>public static const VISIBLE:String = visible;
>```

1. 等待`MediaPlayer`至少具有PREPARED状态（请参阅[等待有效状态](../../t-psdk-dhls-1.4-configure/c-psdk-dhls-1.4-ui-configure/t-psdk-dhls-1.4-ui-state-prepared-wait-for.md)）。
1. 要获取隐藏字幕的当前可见性设置，请使用`MediaPlayer`中的getter方法，它返回一个可见性值。

   ```
   public function get ccVisibility():String
   ```

1. 要更改隐藏式字幕的可见性，请使用setter方法，将可见性值从`ClosedCaptionsVisibility`传递。

   例如：

   ```
   public function set ccVisibility(value:String):void
   ```

1. 定义下拉列表。

   ```
   <s:DropDownList id="ccTracksList" width="85" 
                   dataProvider="{_ccTracks}" 
                   change="onCCTrackChange(event)" 
                   prompt="CC"/>
   ```

1. 定义隐藏字幕轨道的可绑定数组。

   ```
   [Bindable] private var _ccTracks:ArrayCollection =  
     new ArrayCollection(); // active tracks 
   ```

1. 设置监听器。

   ```
   player.addEventListener(MediaPlayerItemEvent.ITEM_CREATED, onItemCreated); 
   player.addEventListener(MediaPlayerItemEvent.CAPTIONS_UPDATED, onCaptionUpdated);
   ```

   要从销毁代码中删除监听器：

   ```
   player.removeEventListener(MediaPlayerItemEvent.ITEM_CREATED, onItemCreated); 
   player.removeEventListener(MediaPlayerItemEvent.CAPTIONS_UPDATED, onCaptionUpdated);
   ```

1. 当用户从列表中做出选择时，创建并更新列表。

   ```
   private function onCCTrackChange(event:IndexChangeEvent):void { 
       var ccTrackIndex:int = event.newIndex; 
       var ccTracks:Vector.<ClosedCaptionsTrack> =  
         _player.currentItem.closedCaptionsTracks; 
       if (ccTrackIndex == 0) { 
           _player.ccVisibility = MediaPlayer.INVISIBLE; 
       } 
       else if (ccTrackIndex <= _ccTracks.length) { 
           var index:Number = findFromActiveIndex(ccTracks, ccTrackIndex - 1); 
           _player.currentItem.selectClosedCaptionsTrack(ccTracks[index]); 
           _player.ccVisibility = MediaPlayer.VISIBLE; 
       } 
   } 
   
   private function findFromActiveIndex(ccTracks:Vector.<ClosedCaptionsTrack>,  
     ccTrackIndex:int):Number { 
       var count:Number = 0; 
       for each (var ccTrack:ClosedCaptionsTrack in ccTracks) { 
           if (count < ccTrackIndex) 
               count = count + 1; 
           else 
               return count; 
       } 
       return -1; 
   } 
   
   private function onItemCreated(event:MediaPlayerItemEvent):void { 
       ... (you are likely to need more code here for other reasons) 
       updateCCTracks(_player.currentItem.closedCaptionsTracks); 
   } 
   
   private function onCaptionUpdated(event:MediaPlayerItemEvent):void { 
       ... (you are likely to need more code here for other reasons) 
       updateCCTracks(_player.currentItem.closedCaptionsTracks,  
                     (_player.ccVisibility == MediaPlayer.VISIBLE) ?  
                      _player.currentItem.selectedClosedCaptionsTrack : null); 
   } 
   
   private function updateCCTracks(tracks:Vector.<ClosedCaptionsTrack>,  
     selectedTrack:ClosedCaptionsTrack = null):void { 
       _ccTracks.removeAll(); 
   
       _ccTracks.addItem( 
           { 
               "label": "CC off", 
               "data": "cc-off" 
           } 
       ); 
   
       var selectedIndex:int = 0; 
       for each (var ccTrack:ClosedCaptionsTrack in tracks) { 
           _ccTracks.addItem( 
               { 
                   "label": ccTrack.name, 
                   "data": ccTrack.name 
               } 
           ); 
           if (selectedTrack && ccTrack.name == selectedTrack.name && 
           ccTrack.language == selectedTrack.language && 
           ccTrack.serviceType == selectedTrack.serviceType) { 
               selectedIndex = _ccTracks.length - 1; 
           } 
       } 
   
       var hasCC:Boolean = _ccTracks.length > 0; 
       ccTracksList.enabled = hasCC; 
       ccTracksList.mouseEnabled = hasCC; 
       ccTracksList.selectedIndex = selectedIndex; 
   } 
   ```

