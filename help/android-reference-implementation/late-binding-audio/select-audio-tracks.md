---
title: 选择音轨
description: 选择音轨
copied-description: true
exl-id: d4a7260a-82dd-4b57-8037-b91815d9b954
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '136'
ht-degree: 0%

---

# 选择音轨{#select-the-audio-tracks}

要为后期捆绑音频选择音频曲目，请实施 [IAAConfig](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/config/IAAConfig.html).

| 收件人…… | 呼叫…… |
|---|---|
| 获取可用AA跟踪的列表 | [getAudioTracks()](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/manager/AAManager.html#getAudioTracks()) |
| 获取当前选定的曲目 | [getSelectedAudioTrack()](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/manager/AAManager.html#getSelectedAudioTrack()) |
| 选择AA曲目 | [selectAlternateAudioTrack()](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/manager/AAManager.html#selectAlternateAudioTrack(int)) |

以下代码示例说明了参考实施如何从TVSDK获取音频曲目并将选定的曲目分配给关联的媒体项目：

```java
/** 
 * Displays a chooser dialog, allowing the user to select the desired 
 * alternate audio track. 
 */ 
private void displayAlternateAudioDialog() { 
    PrimetimeReference.logger.i(LOG_TAG + "#selectAlternateAudio", 
      "Displaying alternate audio chooser dialog."); 
    final int selectedAlternateAudio = aaManager.getSelectedAudioTrackIndex(); 
    if (selectedAlternateAudio != AAManagerOn.INVALID_AUDIO_TRACK) { 
        final String items[] = aaManager.getAudioTracks(); 
        new AlertDialog.Builder(getActivity()) 
          .setTitle(R.string.PlayerControlAADialogTitle) 
          .setSingleChoiceItems(items, selectedAlternateAudio, 
          new DialogInterface.OnClickListener() { 
              public void onClick(DialogInterface dialog, int whichButton) { 
                  boolean result =  
                    aaManager.selectAlternateAudioTrack(whichButton); 
                  if (result) { 
                      PrimetimeReference.logger.i(LOG_TAG 
                                                  + "#selectAlternateAudio", 
                                                  "Audio track selection successful"); 
                  } else { 
                      PrimetimeReference.logger.i(LOG_TAG 
                                            + "#selectAlternateAudio", 
                                            "Audio track selection failed"); 
                  } 
                  // Dismiss dialog. 
                  dialog.cancel(); 
              } 
          }).setNegativeButton(R.string.PlayerControlCCDialogCancel, 
                               new DialogInterface.OnClickListener() { 
              public void onClick(DialogInterface dialog, 
                                    int whichButton) { 
                                // Just cancel the dialog. 
              } 
          }).show(); 
 
    } else { 
        PrimetimeReference.logger.i(LOG_TAG + "#selectAlternateAudioFailed", 
                "Unable to detect the currently selected audio track."); 
        Toast.makeText(getActivity(), 
                "Unable to detect the currently selected audio track", 
                Toast.LENGTH_SHORT).show(); 
    } 
} 
```
