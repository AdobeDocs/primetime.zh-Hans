---
description: 您应将播放器的UI逻辑与管理广告点击的过程分开。 为此，一种方法是为一个活动实施多个片段。
seo-description: 您应将播放器的UI逻辑与管理广告点击的过程分开。 为此，一种方法是为一个活动实施多个片段。
seo-title: 分离可点击广告流程
title: 分离可点击广告流程
uuid: c37f5916-eb25-41ec-b5f4-efb82ec56371
translation-type: tm+mt
source-git-commit: 812d04037c3b18f8d8cdd0d18430c686c3eee1ff

---


# 分离可点击广告流程 {#separate-the-clickable-ad-process}

您应将播放器的UI逻辑与管理广告点击的过程分开。 为此，一种方法是为一个活动实施多个片段。

1. 实现一个片段以包含 `MediaPlayer`。

   此片段应调用 `notifyClick()` 并负责视频播放。

   ```java
   public class PlayerFragment extends SherlockFragment { 
       ... 
       public void notifyAdClick () { 
           _mediaPlayer.notifyClick(); 
       } 
       ... 
   } 
   ```

1. 实现不同的片段以显示指示广告可单击的UI元素，监视该UI元素，并将用户单击传达到包含该片段的片段 `MediaPlayer`。

   此片段应声明用于片段通信的接口。 该片段在其生命周期方法中捕获接 `onAttach()` 口实现，并可以调用接口方法与活动通信。

   ```java
   public class PlayerClickableAdFragment extends SherlockFragment { 
       private ViewGroup viewGroup; 
       private Button button; 
       OnAdUserInteraction callback; 
       @Override 
       public View onCreateView(LayoutInflater inflater,  
                                ViewGroup container,  
                                Bundle savedInstanceState) { 
           // the custom fragment is defined by a custom button 
           viewGroup = (ViewGroup) inflater.inflate(R.layout.fragment_player_clickable_ad,  
                                                    container, false); 
           button = (Button) viewGroup.findViewById(R.id.clickButton); 
   
           // register a click listener to detect user interaction 
           button.setOnClickListener(new View.OnClickListener() { 
               @Override 
               public void onClick(View v) { 
                   // send the event back to the activity 
                   callback.onAdClick(); 
               } 
           }); 
           viewGroup.setVisibility(View.INVISIBLE); 
           return viewGroup; 
       } 
   
       public void hide() { 
           viewGroup.setVisibility(View.INVISIBLE); 
       } 
   
       public void show() { 
           viewGroup.setVisibility(View.VISIBLE);     
       } 
   
       @Override 
       public void onAttach(Activity activity) { 
           super.onAttach(activity); 
           // attaches the interface implementation 
           // if the container activity does not implement the methods  
           // from the interface an exception will be thrown 
           try { 
               callback = (OnAdUserInteraction) activity; 
           } catch (ClassCastException e) { 
               throw new ClassCastException(activity.toString() 
                   + " must implement OnAdUserInteraction"); 
           }     
       } 
   
       // user defined interface that allows fragment communication 
       // must be implemented by the container activity 
       public interface OnAdUserInteraction { 
           public void onAdClick(); 
       } 
   } 
   ```

