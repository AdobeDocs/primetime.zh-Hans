---
description: UI框架是浏览器TVSDK上的一个UI层，它提供各种现成的与视频播放器相关的UI结构。 您可以通过对点进行适合您环境的更改来创建高度可自定义的播放器。
title: UI框架
exl-id: 3175c74b-c08d-4a83-97e4-fe0a8dcf9d86
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '842'
ht-degree: 0%

---

# UI框架 {#the-ui-framework}

UI框架是浏览器TVSDK上的一个UI层，它提供各种现成的与视频播放器相关的UI结构。 您可以通过对点进行适合您环境的更改来创建高度可自定义的播放器。

>[!TIP]
>
>可视化（外观设计）和UI行为是可自定义的。

您可以重写自己的行为或覆盖某些默认行为的功能。 您还可以通过从头开始编写行为来重用随SDK提供的行为。

## 创建基本播放器 {#section_30E4812C4DDA4B519C9C837930B6AE45}

`primetimevisualapi.min.js` 是UI框架库，其所有功能都通过全局对象ptp公开。 在以下示例中， `videoPlayer` 方法创建底层播放器：

```js
<script src="scripts/primetimevisualapi.min.js"></script> 
<script> 
    (function(){ 
        var player = ptp.videoPlayer('#video1'); 
    })(); 
</script>
```

## 配置播放器 {#section_9FC936B983CD40439E6D7675197B226C}

您可以通过以下方式之一配置播放器：

* 使用JSON对象
* 使用API

为了生成JSON对象，浏览器TVSDK提供了UI配置器工具。 在工具中，您可以选择各种设置，然后单击 **[!UICONTROL Test Configuration]** 验证设置，然后单击 **[!UICONTROL Download Configuration]** 以下载设置。 下载文件的内容将用作JSON对象，以传递到 `ptp.videoPlayer` API。

**如何运行UI配置器工具**：

1. 托管 `frameworks` 本地Web服务器上的浏览器TVSDK中提供的文件夹。
1. 要打开该工具，请打开浏览器并导航到 `< path-to-hosted-frameworks-folder>/ui-framework/ui-configurator/`.

**配置播放器的行为**

您可以通过以下方式之一配置播放器行为：

>[!TIP]
>
>对于某些设置，这两个选项均可用。

* **使用videoBehavior API** `ptp.videoPlayer` 返回 `ptp.videoBehavior`，可配置底层视频播放器。 如果需要配置某些与播放相关的设置，可以使用此选项。

   ```js
   player.setAbrControlParameters ({object})
   ```

* **将配置对象传递到videoPlayer函数** 使用此对象时，除了上面讨论的播放设置之外，还可以配置UI的行为。 调用方需要指定必须更改的参数，播放器将继续使用未指定参数的默认值。

   ```js
   var player = ptp.videoPlayer('#video1', { 
           player: { 
               abrControlParameters : {object} 
       }, 
       controlBar : {object} 
   });
   ```

   在上述示例中，ABR控制参数是使用配置对象配置的。 还传递了一个对象以配置控制栏行为。

   有关配置对象的结构，请参阅下面的查看配置对象结构部分。

* **访问AdobePSDK.MediaPlayer** 您可以使用 `videoPlayer.getMediaPlayer` 在某些需要访问浏览器TVSDK的MediaPlayer的高级用例中。

* **配置播放器的外观** 有关为播放器设置外观的详细信息，请参阅 [为播放器蒙皮](../../browser-tvsdk-2.4/c-psdk-browser-2.4-userinterface/c-psdk-browser-tvsdk-2.4-skin-the-player.md).

## 修改默认行为 {#section_D5D692638FFF4BEF81F7BE70E438CCE9}

在UI框架术语中，行为是定义特定组件的可视部分和交互部分的结构。 通过使用下面列出的对象结构，您可以修改要在行为中更改的内容。

例如，在体积块滑块可见后，如果不想隐藏它，请使用以下示例：

```js
var customVolumeSliderBehavior = function (element, configuration, player) { 
    function neverHide() { 
        // do nothing 
 } 
 
    var api = ptp.volumeSliderBehavior(element, configuration, player) 
        .compose({ 
            hide: neverHide 
 }); 
    return api; 
}; 
var player = ptp.videoPlayer('.videoHolder', { 
    controlBar : { 
        volume: { 
            slider: { 
                behavior: customVolumeSliderBehavior 
 } 
        } 
    } 
}
```

>[!NOTE]
>
>根据您想要的自定义，您可以在行为中覆盖某些功能或编写您自己的行为。 有关可覆盖哪些功能的更多信息，请参阅 [UI框架](https://help.adobe.com/en_US/primetime/api/psdk/btvsdk-ui-framework/index.html) api文档。

## 引用 {#section_0A76A3F44D8A49B09FE4C83F3FACCB76}

以下是一些其他参考信息：

* **查看配置对象结构** 这是一个完整的对象结构，通过行为的默认元素以分层方式提及所有默认行为。 在示例配置中，使用UI工厂来创建元素。 您可以使用相同的元素或使用首选方法来构建元素。

   您只需指定要更改的零件，其余功能将从缺省值中选择。 首先，根据用例，您需要提供 `SingleViewConfigurationObject` 或 `MultiViewConfigurationObject` 结构。

   ```js
   var DEFAULT_CONTROL_BAR_CONFIG = { 
       behavior: ptp.controlBarBehavior, 
       element: ptp.factories.simpleDivFactory(null, ptp.elementGetter(selector), 'ptp-control-bar'), 
       audioTrack: { 
           behavior: ptp.audioTrackButtonBehavior, 
           element: ptp.factories.simpleButtonFactory('audioTrackBtn', ptp.elementGetter('.ptp-control-bar'), 
               'ptp-control ptp-btn-control ptp-button-background ptp-btn-audio-track ptp-control-bar-btn') 
       }, 
       closedCaption: { 
           behavior: ptp.closedCaptionButtonBehavior, 
           element: ptp.factories.simpleButtonFactory('cc', ptp.elementGetter('.ptp-control-bar'), 
               'ptp-control ptp-btn-control ptp-button-background ' + 
               'ptp-btn-closed-caption ptp-control-bar-btn hidden', 
               'CC') 
       }, 
       displayTime: { 
           behavior: ptp.timeRemainingBehavior, 
           element: ptp.factories.simpleDivFactory('displayTime', ptp.elementGetter('.ptp-control-bar'), 
               'ptp-control ptp-txt-control ptp-txt-display-time') 
       }, 
       fastForward: { 
           behavior: ptp.fastForwardButtonBehavior, 
           element: ptp.factories.simpleButtonFactory('fastForward', ptp.elementGetter('.ptp-control-bar'), 
               'ptp-control ptp-btn-control ptp-button-background ptp-btn-fastforward ptp-control-bar-btn', 
               'Fast Forward') 
       }, 
       fastRewind: { 
           behavior: ptp.fastRewindButtonBehavior, 
           element: ptp.factories.simpleButtonFactory('fastRewind', ptp.elementGetter('.ptp-control-bar'), 
               'ptp-control ptp-btn-control ptp-button-background ptp-btn-fastrewind ptp-control-bar-btn', 
               'Fast Rewind') 
       }, 
       fullScreen: { 
           behavior: ptp.fullScreenButtonBehavior, 
           element: ptp.factories.simpleButtonFactory('fullScreen', ptp.elementGetter('.ptp-control-bar'), 
               'ptp-control ptp-btn-control ptp-button-background ptp-btn-fullscreen ptp-control-bar-btn', 
               'Full Screen') 
       }, 
       moreOptions: { 
           behavior: ptp.moreOptionsButtonBehavior, 
           element: ptp.factories.simpleButtonFactory('moreOptions', ptp.elementGetter('.ptp-control-bar'), 
               'ptp-control ptp-btn-control ptp-button-background ptp-btn-more-options ptp-control-bar-btn', 
               'More Options') 
       }, 
       multiView: { 
           behavior: ptp.multiViewButtonBehavior, 
           element: ptp.factories.simpleButtonFactory('multiView', ptp.elementGetter('.ptp-control-bar'), 
               'ptp-control ptp-btn-control ptp-button-background ptp-btn-multiview ptp-control-bar-btn', 
               'Multi View') 
       }, 
       socialButton: { 
           behavior: ptp.shareVideoButtonBehavior, 
           element: ptp.factories.simpleButtonFactory('shareVideo', ptp.elementGetter('.ptp-control-bar'), 
               'ptp-control ptp-btn-control ptp-button-background ptp-btn-share-video ptp-control-bar-btn', 
               'Share Video') 
       }, 
       volume: { 
           behavior: ptp.volumeBehavior, 
           element: ptp.factories.simpleDivFactory('volume', ptp.elementGetter('.ptp-control-bar'), 
               'ptp-control ptp-volume-control ptp-control-bar-btn'), 
           mute: { 
               behavior: ptp.muteButtonBehavior, 
               element: ptp.factories.simpleButtonFactory('mute', ptp.elementGetter('.ptp-volume-control'), 
                   'ptp-control ptp-button-background ptp-btn-volume', 'Mute') 
           }, 
           slider: { 
               behavior: ptp.volumeSliderBehavior, 
               element: ptp.factories.simpleSliderFactory('volumeSlider', ptp.elementGetter('.ptp-volume-control'), 
                   'ptp-control ptp-volume-slider ptp-volume-hidden', 'Volume') 
           } 
       }, 
       pip: { 
           behavior: ptp.pipButtonBehavior, 
           element: ptp.factories.simpleButtonFactory('pip', ptp.elementGetter('.ptp-control-bar'), 
               'ptp-control ptp-btn-control ptp-button-background ptp-btn-pip ptp-control-bar-btn', 'PIP') 
       }, 
       playPause: { 
           behavior: ptp.playPauseButtonBehavior, 
           element: ptp.factories.simpleButtonFactory('play', ptp.elementGetter('.ptp-control-bar'), 
               'ptp-control ptp-btn-control ptp-button-background ptp-btn-playpause ptp-control-bar-btn', 
               'Play') 
       }, 
       rewind: { 
           behavior: ptp.rewindButtonBehavior, 
           element: ptp.factories.simpleButtonFactory('rewind', ptp.elementGetter('.ptp-control-bar'), 
               'ptp-control ptp-btn-control ptp-button-background ptp-btn-rewind ptp-control-bar-btn', 
               'Rewind') 
       }, 
       scrubBar: { 
           element: ptp.factories.simpleDivFactory('scrubBar', ptp.elementGetter('.ptp-control-bar'), 'ptp-scrub-bar'), 
           behavior: ptp.scrubBarBehavior, 
    }, 
     bufferProgressBar: { 
               element: ptp.factories.simpleDivFactory('bufferProgressBar', ptp.elementGetter('.ptp-scrub-bar'), 
                   'ptp-buffer-progress-bar'), 
               behavior: ptp.bufferProgressBarBehavior 
     }, 
       seekToBar: { 
               element: ptp.factories.simpleDivFactory('seekToBar', ptp.elementGetter('.ptp-scrub-bar'), 'ptp-seek-to-bar'), 
               behavior: ptp.seekToBarBehavior 
     }, 
       playbackProgressBar: { 
               element: ptp.factories.simpleDivFactory('playbackProgressBar', ptp.elementGetter('.ptp-scrub-bar'), 
                   'ptp-playback-progress-bar'), 
               behavior: ptp.playProgressBarBehavior 
     }, 
       playHead: { 
               element: ptp.factories.simpleDivFactory('playHead', ptp.elementGetter('.ptp-scrub-bar'), 'ptp-progress-bar-play-head'), 
               behavior: ptp.playHeadBehavior 
     } 
       }, 
       slowRewind: { 
           behavior: ptp.slowRewindButtonBehavior, 
           element: ptp.factories.simpleButtonFactory('slowRewind', ptp.elementGetter('.ptp-control-bar'), 
               'ptp-control ptp-btn-control ptp-button-background ptp-btn-slowrewind ptp-control-bar-btn', 
               'Slow Rewind'), 
           enabled: true 
    }, 
       slowForward: { 
           behavior: ptp.slowForwardButtonBehavior, 
           element: ptp.factories.simpleButtonFactory('slowForward', ptp.elementGetter('.ptp-control-bar'), 
               'ptp-control ptp-btn-control ptp-button-background ptp-btn-slowforward ptp-control-bar-btn', 
               'Slow Forward') 
       }, 
       spacer: { 
           element: ptp.factories.simpleDivFactory('spacer', ptp.elementGetter('.ptp-control-bar'), 'ptp-fill-spacer') 
       }, 
       trickPlayRateDisplay: { 
           behavior: ptp.trickPlayRateDisplayBehavior, 
           element: ptp.factories.simpleDivFactory('trickPlayDisplay', 
               ptp.elementGetter('.ptp-control-bar'), 
               'ptp-control ptp-btn-control ptp-control-bar-trick-play-rate hidden') 
       } 
   }; 
   var DEFAULT_LOCALIZATION_CONFIG = { 
       locale: 'en-US', 
       behavior: mapLocalizer, 
       localizationMap: { 
           'en-US': { 
               OK: 'Okay', 
               CANCEL: 'Cancel', 
               DEFAULT: 'Default', 
               NONE: 'None', 
               FONT_MONO_W_SERIF: 'Monospaced With Serifs', 
               FONT_PROP_W_SERIF: 'Proportional with Serifs', 
               FONT_MONO_WO_SERIF: 'Monospaced without Serifs', 
               FONT_CASUAL: 'Casual', 
               FONT_CURSIVE: 'Cursive', 
               FONT_SMALL_CAPS: 'Small Capitals', 
               FONT_EDGE_DEFAULT: 'Default', 
               FONT_EDGE_NONE: 'None', 
               FONT_EDGE_RAISED: 'Raised', 
               FONT_EDGE_DEPRESSED: 'Depressed', 
               FONT_EDGE_UNIFORM: 'Uniform', 
               FONT_EDGE_DROP_SHADOW_LEFT: 'Drop Shadow Left', 
               FONT_EDGE_DROP_SHADOW_RIGHT: 'Drop Shadow Right', 
               SIZE_SMALL: 'Small', 
               SIZE_MEDIUM: 'Medium', 
               SIZE_LARGE: 'Large', 
               COLOR_BLACK: 'Black', 
               COLOR_GREY: 'Grey', 
               COLOR_WHITE: 'White', 
               COLOR_BRIGHT_WHITE: 'Bright White', 
               COLOR_DARK_RED: 'Dark Red', 
               COLOR_RED: 'Red', 
               COLOR_BRIGHT_RED: 'Bright Red', 
               COLOR_DARK_GREEN: 'Dark Green', 
               COLOR_GREEN: 'Green', 
               COLOR_BRIGHT_GREEN: 'Bright Green', 
               COLOR_DARK_BLUE: 'Dark Blue', 
               COLOR_BLUE: 'Blue', 
               COLOR_BRIGHT_BLUE: 'Bright Blue', 
               COLOR_DARK_YELLOW: 'Dark Yellow', 
               COLOR_YELLOW: 'Yellow', 
               COLOR_BRIGHT_YELLOW: 'Bright Yellow', 
               COLOR_DARK_MAGENTA: 'Dark Magenta', 
               COLOR_MAGENTA: 'Magenta', 
               COLOR_BRIGHT_MAGENTA: 'Bright Magenta', 
               COLOR_DARK_CYAN: 'Dark Cyan', 
               COLOR_CYAN: 'Cyan', 
               COLOR_BRIGHT_CYAN: 'Bright Cyan', 
               REPLAY: 'Replay', 
               PLAY: 'Play', 
               PAUSE: 'Pause', 
               STOP: 'Stop' 
     } 
       } 
   }; 
   var DEFAULT_AUDIO_TRACK_SELECTION_CONFIG = { 
       behavior: ptp.audioTrackSelectionPanelBehavior, 
       element: ptp.factories.simpleDivFactory('audioTrackSelectionPanel', ptp.elementGetter(selector), 
           'ptp-audio-track-selection-panel hidden'), 
       audioTrackSelectionPanelHeader: { 
           behavior: ptp.audioTrackSelectionPanelHeader, 
           element: ptp.factories.simpleDivFactory('header', ptp.elementGetter('.ptp-audio-track-selection-panel'), 
               'ptp-panel-header ptp-audio-track-selection-header'), 
           audioTrackSelectionPanelCloseButton: { 
               behavior: ptp.buttonBehavior, 
               element: ptp.factories.simpleDivFactory('closeButton', ptp.elementGetter('.ptp-audio-track-selection-header'), 
                   'ptp-control ptp-btn-control ptp-panel-close-btn', 'X') 
           }, 
           audioTrackSelectionPanelTitle: { 
               element: ptp.factories.simpleDivFactory('title', ptp.elementGetter('.ptp-audio-track-selection-header'), 
                   'ptp-panel-title', 'Audio Track') 
           } 
       }, 
       audioTrackSelectionPanelSeparator: { 
           element: ptp.factories.simpleHRFactory('audioTrackSelectionPanelSeparator', 
               ptp.elementGetter('.ptp-audio-track-selection-panel'), 'ptp-hr-separator') 
       }, 
       audioTrackSelectionMenu: { 
           behavior: ptp.audioTrackSelectionMenu, 
           element: ptp.factories.simpleDivFactory('audioTrackSelectionMenu', ptp.elementGetter('.ptp-audio-track-selection-panel'), 
               'ptp-audio-track-selection-menu', 'Menu TBD') 
       } 
   }; 
   
   var DEFAULT_CLOSED_CAPTION_LANGUAGE_PANEL_CONFIG = { 
       behavior: ptp.closedCaptionLanguagePanelBehavior, 
       element: ptp.factories.simpleDivFactory('closedCaptionLanguagePanel', ptp.elementGetter(selector), 
           'ptp-closed-caption-panel hidden ptp-closed-caption-language-panel'), 
       closedCaptionLanguagePanelHeader: { 
           behavior: ptp.closedCaptionLanguagePanelHeader, 
           element: ptp.factories.simpleDivFactory('header', ptp.elementGetter('.ptp-closed-caption-language-panel'), 
               'ptp-panel-header ptp-closed-caption-language-header'), 
           closedCaptionLanguageCloseButton: { 
               behavior: ptp.buttonBehavior, 
               element: ptp.factories.simpleDivFactory('closeButton', ptp.elementGetter('.ptp-closed-caption-language-header'), 
                   'ptp-control ptp-btn-control ptp-panel-close-btn', 'X') 
           }, 
           closedCaptionLanguageTitle: { 
               element: ptp.factories.simpleDivFactory('title', ptp.elementGetter('.ptp-closed-caption-language-header'), 
                   'ptp-panel-title', 'Closed Captions') 
           }, 
           closedCaptionLanguageOptionsButton: { 
               behavior: ptp.buttonBehavior, 
               element: ptp.factories.simpleDivFactory('title', ptp.elementGetter('.ptp-closed-caption-language-header'), 
                   'ptp-closed-caption-options-btn', 'Options') 
           } 
       }, 
       closedCaptionLanguageSeparator: { 
           element: ptp.factories.simpleHRFactory('closedCaptionLanguageSeparator', ptp.elementGetter('.ptp-closed-caption-panel'), 
               'ptp-hr-separator') 
       }, 
       closedCaptionOptions: { 
           behavior: ptp.closedCaptionLanguageMenu, 
           element: ptp.factories.simpleDivFactory('captionLanguageMenu', ptp.elementGetter('.ptp-closed-caption-panel'), 
               'ptp-scroll-bar ptp-closed-caption-language-menu') 
       } 
   }; 
   
   var DEFAULT_CLOSED_CAPTION_OPTIONS_PANEL_CONFIG = { 
       behavior: ptp.closedCaptionOptionsPanelBehavior, 
       element: ptp.factories.simpleDivFactory('closedCaptionOptionsPanel', ptp.elementGetter(selector), 
           'ptp-closed-caption-panel hidden ptp-closed-caption-options-panel'), 
       closedCaptionOptionsHeader: { 
           behavior: ptp.closedCaptionOptionsPanelHeader, 
           element: ptp.factories.simpleDivFactory('closedCaptionOptionsHeader', ptp.elementGetter('.ptp-closed-caption-options-panel'), 
               'ptp-panel-header ptp-closed-caption-options-header'), 
           closedCaptionOptionsCloseButton: { 
               behavior: ptp.buttonBehavior, 
               element: ptp.factories.simpleDivFactory('closedCaptionOptionsCloseButton', 
                   ptp.elementGetter('.ptp-closed-caption-options-header'), 
                   'ptp-control ptp-btn-control ptp-panel-close-btn', '<') 
           }, 
           closedCaptionOptionsTitle: { 
               element: ptp.factories.simpleDivFactory('closedCaptionOptionsTitle', 
                   ptp.elementGetter('.ptp-closed-caption-options-header'), 'ptp-panel-title', 'Closed Captions') 
           }, 
           closedCaptionLanguageDoneButton: { 
               behavior: ptp.buttonBehavior, 
               element: ptp.factories.simpleDivFactory('closedCaptionLanguageDoneButton', 
                   ptp.elementGetter('.ptp-closed-caption-options-header'), 'ptp-closed-caption-done-btn', 'Done') 
           } 
       }, 
       closedCaptionOptionsHeaderSeparator: { 
           element: ptp.factories.simpleHRFactory('closedCaptionOptionsHeaderSeparator', 
               ptp.elementGetter('.ptp-closed-caption-options-panel'), 'ptp-hr-separator') 
       }, 
       closedCaptionOptionsMenu: { 
           behavior: ptp.closedCaptionOptionsMenu, 
           element: ptp.factories.simpleDivFactory('closedCaptionOptionsMenu', ptp.elementGetter('.ptp-closed-caption-options-panel'), 
               'ptp-closed-caption-options-menu'), 
           closedCaptionOptionsMainMenu: { 
               behavior: ptp.closedCaptionOptionsMainMenu, 
               element: ptp.factories.simpleDivFactory('closedCaptionOptionsMainMenu', 
                   ptp.elementGetter('.ptp-closed-caption-options-menu'), 
                   'ptp-scroll-bar ptp-closed-caption-options-main-menu'), 
               closedCaptionOptionsFontStyle: { 
                   behavior: ptp.buttonBehavior, 
                   element: ptp.factories.simpleDivFactory('closedCaptionOptionsFontStyle', 
                       ptp.elementGetter('.ptp-closed-caption-options-main-menu'), 
                       'ptp-closed-caption-options-menu-item', 'Font Style') 
               }, 
               closedCaptionOptionsFontSize: { 
                   behavior: ptp.buttonBehavior, 
                   element: ptp.factories.simpleDivFactory('closedCaptionOptionsFontSize', 
                       ptp.elementGetter('.ptp-closed-caption-options-main-menu'), 
                       'ptp-closed-caption-options-menu-item', 'Font Size') 
               }, 
               closedCaptionOptionsFontColor: { 
                   behavior: ptp.buttonBehavior, 
                   element: ptp.factories.simpleDivFactory('closedCaptionOptionsFontColor', 
                       ptp.elementGetter('.ptp-closed-caption-options-main-menu'), 
                       'ptp-closed-caption-options-menu-item', 'Font Color') 
               }, 
               closedCaptionOptionsFontOpacity: { 
                   behavior: ptp.buttonBehavior, 
                   element: ptp.factories.simpleDivFactory('closedCaptionOptionsFontOpacity', 
                       ptp.elementGetter('.ptp-closed-caption-options-main-menu'), 
                       'ptp-closed-caption-options-menu-item', 'Font Opacity') 
               }, 
               closedCaptionOptionsBackgroundColor: { 
                   behavior: ptp.buttonBehavior, 
                   element: ptp.factories.simpleDivFactory('closedCaptionOptionsBackgroundColor', 
                       ptp.elementGetter('.ptp-closed-caption-options-main-menu'), 
                       'ptp-closed-caption-options-menu-item', 'Background Color') 
               }, 
               closedCaptionOptionsBackgroundOpacity: { 
                   behavior: ptp.buttonBehavior, 
                   element: ptp.factories.simpleDivFactory('closedCaptionOptionsBackgroundOpacity', 
                       ptp.elementGetter('.ptp-closed-caption-options-main-menu'), 
                       'ptp-closed-caption-options-menu-item', 'Background Opacity') 
               }, 
               closedCaptionOptionsFillColor: { 
                   behavior: ptp.buttonBehavior, 
                   element: ptp.factories.simpleDivFactory('closedCaptionOptionsFillColor', 
                       ptp.elementGetter('.ptp-closed-caption-options-main-menu'), 
                       'ptp-closed-caption-options-menu-item', 'Fill Color') 
               }, 
               closedCaptionOptionsFillOpacity: { 
                   behavior: ptp.buttonBehavior, 
                   element: ptp.factories.simpleDivFactory('closedCaptionOptionsFillOpacity', 
                       ptp.elementGetter('.ptp-closed-caption-options-main-menu'), 
                       'ptp-closed-caption-options-menu-item', 'Fill Opacity') 
               }, 
               closedCaptionOptionsFontEdge: { 
                   behavior: ptp.buttonBehavior, 
                   element: ptp.factories.simpleDivFactory('closedCaptionOptionsFontEdge', 
                       ptp.elementGetter('.ptp-closed-caption-options-main-menu'), 
                       'ptp-closed-caption-options-menu-item', 'Stroke Weight') 
               }, 
               closedCaptionOptionsFontEdgeColor: { 
                   behavior: ptp.buttonBehavior, 
                   element: ptp.factories.simpleDivFactory('closedCaptionOptionsFontEdgeColor', 
                       ptp.elementGetter('.ptp-closed-caption-options-main-menu'), 
                       'ptp-closed-caption-options-menu-item', 'Stroke Color') 
               } 
           }, 
           closedCaptionOptionsMenuSeparator: { 
               element: ptp.factories.simpleHRFactory('closedCaptionOptionsMenuSeparator', 
                   ptp.elementGetter('.ptp-closed-caption-options-menu'), 
                   'ptp-closed-caption-options-menu-separator') 
           }, 
           closedCaptionOptionsSubMenu: { 
               behavior: ptp.closedCaptionOptionsSubMenu, 
               closedCaptionOptionsFontStyleSubMenu: { 
                   behavior: ptp.verticalListMenu, 
                   element: ptp.factories.simpleDivFactory('closedCaptionOptionsFontStyleSubMenu', 
                       ptp.elementGetter('.ptp-closed-caption-options-menu'), 
                       'ptp-scroll-bar ptp-closed-caption-options-sub-menu hidden') 
               }, 
               closedCaptionOptionsFontEdgeSubMenu: { 
                   behavior: ptp.verticalListMenu, 
                   element: ptp.factories.simpleDivFactory('closedCaptionOptionsFontEdgeSubMenu', 
                       ptp.elementGetter('.ptp-closed-caption-options-menu'), 
                       'ptp-scroll-bar ptp-closed-caption-options-sub-menu hidden') 
               }, 
               closedCaptionOptionsFontEdgeColorSubMenu: { 
                   behavior: ptp.verticalListMenu, 
                   element: ptp.factories.simpleDivFactory('closedCaptionOptionsFontEdgeColorSubMenu', 
                       ptp.elementGetter('.ptp-closed-caption-options-menu'), 
                       'ptp-scroll-bar ptp-closed-caption-options-sub-menu hidden') 
               }, 
               closedCaptionOptionsFontSizeSubMenu: { 
                   behavior: ptp.verticalListMenu, 
                   element: ptp.factories.simpleDivFactory('closedCaptionOptionsFontSizeSubMenu', 
                       ptp.elementGetter('.ptp-closed-caption-options-menu'), 
                       'ptp-scroll-bar ptp-closed-caption-options-sub-menu hidden') 
               }, 
               closedCaptionOptionsFontColorSubMenu: { 
                   behavior: ptp.verticalListMenu, 
                   element: ptp.factories.simpleDivFactory('closedCaptionOptionsFontColorSubMenu', 
                       ptp.elementGetter('.ptp-closed-caption-options-menu'), 
                       'ptp-scroll-bar ptp-closed-caption-options-sub-menu hidden') 
               }, 
               closedCaptionOptionsFontOpacitySubMenu: { 
                   behavior: ptp.sliderMenu, 
                   element: ptp.factories.simpleDivFactory('closedCaptionOptionsFontOpacitySubMenu', 
                       ptp.elementGetter('.ptp-closed-caption-options-menu'), 
                       'ptp-closed-caption-options-sub-menu ptp-closed-caption-options-opacity-slider hidden') 
               }, 
               closedCaptionOptionsBackgroundColorSubMenu: { 
                   behavior: ptp.verticalListMenu, 
                   element: ptp.factories.simpleDivFactory('closedCaptionOptionsBackgroundColorSubMenu', 
                       ptp.elementGetter('.ptp-closed-caption-options-menu'), 
                       'ptp-scroll-bar ptp-closed-caption-options-sub-menu hidden') 
               }, 
               closedCaptionOptionsBackgroundOpacitySubMenu: { 
                   behavior: ptp.sliderMenu, 
                   element: ptp.factories.simpleDivFactory('closedCaptionOptionsBackgroundOpacitySubMenu', 
                       ptp.elementGetter('.ptp-closed-caption-options-menu'), 
                       'ptp-closed-caption-options-sub-menu ptp-closed-caption-options-opacity-slider hidden') 
               }, 
               closedCaptionOptionsFillColorSubMenu: { 
                   behavior: ptp.verticalListMenu, 
                   element: ptp.factories.simpleDivFactory('closedCaptionOptionsFillColorSubMenu', 
                       ptp.elementGetter('.ptp-closed-caption-options-menu'), 
                       'ptp-scroll-bar ptp-closed-caption-options-sub-menu hidden') 
               }, 
               closedCaptionOptionsFillOpacitySubMenu: { 
                   behavior: ptp.sliderMenu, 
                   element: ptp.factories.simpleDivFactory('closedCaptionOptionsFillOpacitySubMenu', 
                       ptp.elementGetter('.ptp-closed-caption-options-menu'), 
                       'ptp-closed-caption-options-sub-menu ptp-closed-caption-options-opacity-slider hidden') 
               } 
           } 
       }, 
       closedCaptionOptionsPreviewSeparator: { 
           element: ptp.factories.simpleHRFactory('closedCaptionOptionsPreviewSeparator', 
               ptp.elementGetter('.ptp-closed-caption-options-panel'), 'ptp-hr-separator') 
       }, 
       closedCaptionPreviewPanel: { 
           behavior: ptp.closedCaptionPreviewPanel, 
           text: 'Sample Captions', 
           element: ptp.factories.simpleDivFactory('closedCaptionPreviewPanel', 
               ptp.elementGetter('.ptp-closed-caption-options-panel'), 
               'ptp-closed-caption-preview-panel', 'Sample Captions') 
       }, 
       closedCaptionOptionsFooterSeparator: { 
           element: ptp.factories.simpleHRFactory('closedCaptionOptionsFooterSeparator', 
               ptp.elementGetter('.ptp-closed-caption-options-panel'), 'ptp-hr-separator') 
       }, 
       closedCaptionOptionsFooter: { 
           behavior: ptp.closedCaptionOptionsFooter, 
           element: ptp.factories.simpleDivFactory('closedCaptionOptionsFooter', 
               ptp.elementGetter('.ptp-closed-caption-options-panel'), 'ptp-closed-caption-options-footer'), 
           closedCaptionOptionsResetButton: { 
               behavior: ptp.buttonBehavior, 
               element: ptp.factories.simpleDivFactory('closedCaptionOptionsResetButton', 
                   ptp.elementGetter('.ptp-closed-caption-options-footer'), 
                   'ptp-closed-caption-options-reset-button', 'Reset to Default') 
           }, 
           closedCaptionOptionsApplyButton: { 
               behavior: ptp.buttonBehavior, 
               element: ptp.factories.simpleDivFactory('closedCaptionOptionsApplyButton', 
                   ptp.elementGetter('.ptp-closed-caption-options-footer'), 
                   'ptp-closed-caption-options-apply-button', 'Apply') 
           } 
       } 
   }; 
   
   var DEFAULT_SHARE_VIDEO_PANEL_CONFIG = { 
       behavior: ptp.shareVideoPanelBehavior, 
       element: ptp.factories.simpleDivFactory('shareVideoPanel', ptp.elementGetter(selector), 'ptp-share-video-panel hidden'), 
       shareVideoPanelHeader: { 
           behavior: ptp.shareVideoPanelHeader, 
           element: ptp.factories.simpleDivFactory('shareVideoPanelHeader', ptp.elementGetter('.ptp-share-video-panel'), 
               'ptp-panel-header ptp-share-video-panel-header'), 
           shareVideoPanelCloseButton: { 
               behavior: ptp.buttonBehavior, 
               element: ptp.factories.simpleDivFactory('shareVideoPanelCloseButton', ptp.elementGetter('.ptp-share-video-panel-header'), 
                   'ptp-control ptp-btn-control ptp-panel-close-btn', 'X') 
           }, 
           shareVideoPanelTitle: { 
               element: ptp.factories.simpleDivFactory('shareVideoPanelTitle', ptp.elementGetter('.ptp-share-video-panel-header'), 
                   'ptp-panel-title', 'Social Share') 
           } 
       }, 
       shareVideoPanelHeaderSeparator: { 
           element: ptp.factories.simpleHRFactory('shareVideoPanelHeaderSeparator', ptp.elementGetter('.ptp-share-video-panel'), 
               'ptp-hr-separator') 
       }, 
       shareVideoPanelMenu: { 
           element: ptp.factories.simpleDivFactory('shareVideoPanelMenu', ptp.elementGetter('.ptp-share-video-panel'), 
               'share-video-panel-menu'), 
           behavior: ptp.shareVideoPanelMenu, 
           shareVideoPanelFacebookBtn: { 
               behavior: ptp.buttonBehavior, 
               element: ptp.factories.simpleDivFactory('shareVideoPanelFacebookBtn', ptp.elementGetter('.share-video-panel-menu'), 
                   'ptp-btn-control ptp-button-background ptp-share-video-panel-menu-item ' + 
                   'ptp-btn-share-video-facebook') 
           }, 
           shareVideoPanelTwitterBtn: { 
               behavior: ptp.buttonBehavior, 
               element: ptp.factories.simpleDivFactory('shareVideoPanelTwitterBtn', ptp.elementGetter('.share-video-panel-menu'), 
                   'ptp-btn-control ptp-button-background ptp-share-video-panel-menu-item ' + 
                   'ptp-btn-share-video-twitter') 
           }, 
           shareVideoPanelGoogleBtn: { 
               behavior: ptp.buttonBehavior, 
               element: ptp.factories.simpleDivFactory('shareVideoPanelGoogleBtn', ptp.elementGetter('.share-video-panel-menu'), 
                   'ptp-btn-control ptp-button-background ptp-share-video-panel-menu-item ' + 
                   'ptp-btn-share-video-google-plus') 
           }, 
           shareVideoPanelLinkedinBtn: { 
               behavior: ptp.buttonBehavior, 
               element: ptp.factories.simpleDivFactory('shareVideoPanelLinkedinBtn', ptp.elementGetter('.share-video-panel-menu'), 
                   'ptp-btn-control ptp-button-background ptp-share-video-panel-menu-item ' + 
                   'ptp-btn-share-video-linkedin') 
           } 
       } 
   }; 
   
   var DEFAULT_MORE_OPTIONS_CONTROL_PANEL_CONFIG = { 
       behavior: ptp.moreOptionsControlPanel, 
       element: ptp.factories.simpleDivFactory('moreOptionsControlPanel', ptp.elementGetter(selector), 
           'ptp-more-options-control-panel hidden'), 
       moreOptionsControlPanelHeader: { 
           behavior: ptp.moreOptionsControlPanelHeader, 
           element: ptp.factories.simpleDivFactory('moreOptionsControlPanelHeader', 
               ptp.elementGetter('.ptp-more-options-control-panel'), 
               'ptp-panel-header ptp-more-options-control-panel-header'), 
           moreOptionsControlPanelCloseButton: { 
               behavior: ptp.buttonBehavior, 
               element: ptp.factories.simpleDivFactory('moreOptionsControlPanelCloseButton', 
                   ptp.elementGetter('.ptp-more-options-control-panel-header'), 
                   'ptp-control ptp-btn-control ptp-panel-close-btn', 'X') 
           }, 
           moreOptionsControlPanelTitle: { 
               element: ptp.factories.simpleDivFactory('moreOptionsPanelTitle', 
                   ptp.elementGetter('.ptp-more-options-control-panel-header'), 
                   'ptp-panel-title', 'Options') 
           } 
       }, 
       moreOptionsPanelHeaderSeparator: { 
           element: ptp.factories.simpleHRFactory('moreOptionsPanelHeaderSeparator', 
               ptp.elementGetter('.ptp-more-options-control-panel'), 
               'ptp-hr-separator') 
       }, 
       moreOptionsPanelMenu: { 
           element: ptp.factories.simpleDivFactory('moreOptionsPanelMenu', 
               ptp.elementGetter('.ptp-more-options-control-panel'), 
               'ptp-more-options-control-panel-menu'), 
           behavior: ptp.moreOptionsControlPanelMenu, 
           audioTrackButton: { 
               behavior: ptp.audioTrackButtonBehavior, 
               element: ptp.factories.simpleButtonFactory('audioTrackBtn', ptp.elementGetter('.ptp-more-options-control-panel-menu'), 
                   'ptp-control ptp-btn-control ptp-button-background ptp-btn-audio-track ' + 
                   'ptp-more-options-control-panel-menu-item ' + 
                   'ptp-more-options-menu-btn', 
                   'Audio Track') 
           }, 
           multiViewButton: { 
               behavior: ptp.multiViewButtonBehavior, 
               element: ptp.factories.simpleButtonFactory('multiView', ptp.elementGetter('.ptp-more-options-control-panel-menu'), 
                   'ptp-control ptp-btn-control ptp-button-background ptp-btn-multiview ' + 
                   'ptp-more-options-control-panel-menu-item ' + 
                   'ptp-more-options-menu-btn', 
                   'Multi View') 
           }, 
           pipButton: { 
               behavior: ptp.pipButtonBehavior, 
               element: ptp.factories.simpleButtonFactory('pip', ptp.elementGetter('.ptp-more-options-control-panel-menu'), 
                   'ptp-control ptp-btn-control ptp-button-background ptp-btn-pip ' + 
                   'ptp-more-options-control-panel-menu-item ' + 
                   'ptp-more-options-menu-btn', 'PIP') 
           }, 
           socialButton: { 
               behavior: ptp.shareVideoButtonBehavior, 
               element: ptp.factories.simpleButtonFactory('shareVideo', ptp.elementGetter('.ptp-more-options-control-panel-menu'), 
                   'ptp-control ptp-btn-control ptp-button-background ptp-btn-share-video ' + 
                   'ptp-more-options-control-panel-menu-item ' + 
                   'ptp-more-options-menu-btn', 
                   'Share Video') 
           } 
       } 
   }; 
   
   SingleViewConfigurationObject = { 
       element: ptp.elementGetter(selector), 
       classNames: 'ptp-root-element', 
       behavior: ptp.singleViewBehavior, 
       logLevel: 0, 
       logOutput: null, 
       player: { 
           element: ptp.factories.simpleDivFactory('videoPlayer', ptp.elementGetter(selector), 
               'ptp-main-video-div-style ptp-background-style'), 
           behavior: ptp.videoBehavior, 
           autoPlay: true, 
           bufferingOverlay: { 
               behavior: ptp.bufferingOverlayBehavior, 
               element: ptp.createDiv('bufferingOverlay', ptp.elementGetter('.ptp-main-video-div-style'), 'ptp-buffering-overlay') 
           }, 
           errorMessagePanel: { 
               behavior: ptp.errorMessagePanelBehavior, 
               element: ptp.createDiv('errorMessagePanel', ptp.elementGetter('.ptp-main-video-div-style'), 'ptp-error-message-panel hidden') 
           }, 
           controlsDisabledInAd: //same as ptp.videoBehavior.setControlsDisabledInAd  
    mediaPlayerItemConfig: //same as ptp.videoBehavior.setMediaPlayerItemConfig  
      abrControlParameters: //same as ptp.videoBehavior.setAbrControlParameters  
     bufferControlParameters: //same as ptp.videoBehavior.setBufferControlParameters  
     ccVisibility: //same as ptp.videoBehavior.setCCVisibility  
      ccStyle: //same as ptp.videoBehavior.setCCStyle  
     mediaResource: //same as ptp.videoBehavior.setMediaResource  
     volume: //same as ptp.videoBehavior.setVolume 
     }, 
   
       pip: { 
           element: ptp.factories.simpleDivFactory('pip', ptp.elementGetter(selector), 'ptp-pip-video-div'), 
               behavior: ptp.videoBehavior, 
               bufferingOverlay: { 
               behavior: ptp.bufferingOverlayBehavior, 
                   element: ptp.createDiv('bufferingOverlay', ptp.elementGetter('.ptp-pip-video-div'), 'ptp-buffering-overlay') 
           }, 
           errorMessagePanel: { 
               behavior: ptp.errorMessagePanelBehavior, 
                   element: ptp.createDiv('errorMessagePanel', ptp.elementGetter('.ptp-pip-video-div'), 'ptp-error-message-panel hidden') 
           }, 
           autoPlay: false 
     }, 
       localization: DEFAULT_LOCALIZATION_CONFIG, 
       controlBar: DEFAULT_CONTROL_BAR_CONFIG, 
       audioTrackSelectionPanel: DEFAULT_AUDIO_TRACK_SELECTION_CONFIG, 
       closedCaptionLanguagePanel: DEFAULT_CLOSED_CAPTION_LANGUAGE_PANEL_CONFIG, 
       closedCaptionOptionsPanel: DEFAULT_CLOSED_CAPTION_OPTIONS_PANEL_CONFIG, 
       moreOptionsControlPanel: DEFAULT_MORE_OPTIONS_CONTROL_PANEL_CONFIG, 
       shareVideoPanel: DEFAULT_SHARE_VIDEO_PANEL_CONFIG 
   }; 
   
   MultiViewConfigurationObject = { 
       element: ptp.elementGetter(selector), 
       classNames: 'ptp-root-element', 
       behavior: ptp.multiViewBehavior, 
       logLevel: 0, 
       logOutput: null, 
       multiVideoHolder: { 
           element: ptp.factories.simpleDivFactory('multiViewPlayer', ptp.elementGetter(selector), 'ptp-multi-view-container') 
       }, 
       views: [ 
           { 
               player: {} // see in SingleViewConfigurationObject above 
     } 
       ], 
       localization: DEFAULT_LOCALIZATION_CONFIG, 
       controlBar: DEFAULT_CONTROL_BAR_CONFIG, 
       audioTrackSelectionPanel: DEFAULT_AUDIO_TRACK_SELECTION_CONFIG, 
       closedCaptionLanguagePanel: DEFAULT_CLOSED_CAPTION_LANGUAGE_PANEL_CONFIG, 
       closedCaptionOptionsPanel: DEFAULT_CLOSED_CAPTION_OPTIONS_PANEL_CONFIG, 
       moreOptionsControlPanel: DEFAULT_MORE_OPTIONS_CONTROL_PANEL_CONFIG, 
       shareVideoPanel: DEFAULT_SHARE_VIDEO_PANEL_CONFIG 
   };
   ```

* **辅助函数结构** 此结构由以下内容组成：

   * **工厂** 要创建可视化元素，您可以使用 `ptp.factories.simpleButtonFactory`， `ptp.factories.simpleDivFactory`， `ptp.factories.simpleHRFactory`、和 `ptp.factories.simpleSliderFactory`. 欲了解更多信息，请参见 [UI框架](https://help.adobe.com/en_US/primetime/api/psdk/btvsdk-ui-framework/index.html) api文档。

   * **Mixins** Mixin是可组合模块，可以在行为中组合以使用通用结构。 例如，许多组件希望了解可能影响其行为的更改，例如在播放广告时。 所有这些元素将添加 `adBreak` 类。

      以下是如何实施内置mixin的示例 `adBreakStyling`：

      ```js
      adBreakStyling = function (element, player) { 
          ... 
          ... 
          return composable().compose({ 
              init: init, 
              manageAdBreakStyle: manageAdBreakStyle 
       }); 
      }
      ```

      以下是一个行为如何使用此mixin：

      ```js
      customBehavior = function (element, configuration, player) { 
          var api = 
              component(element, configuration, player, clickHandler).compose( 
                  adBreakStyling(element, player).compose({ 
                      init: init, 
                  })); 
          return api; 
      }
      ```

      现在 `customBehavior` 可以使用由公开的所有方法 `adBreakStyling`，在本例中，为 `manageAdBreakStyle`. 另一个用例是当mixin可以添加事件侦听器时，并且在处理程序中，mixin可以通过某种方式修改元素。 随后，使用此mixin的组件将自动拥有此功能。

   * **Utils** 某些实用程序，例如 `ptp.elementGetter`，在配置部分中使用和 `ptp.deepmerge`可以帮助您编写或扩展行为。 欲了解更多信息，请参见 [UI框架](https://help.adobe.com/en_US/primetime/api/psdk/btvsdk-ui-framework/index.html) api文档。
