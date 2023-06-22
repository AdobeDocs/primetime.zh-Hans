---
description: 本节介绍配置输入的语法，重点介绍有效和无效的输入选项，并解释如何解释省略的可选字段。
title: RBOP语法
exl-id: 311194ec-e59b-4145-b22b-6983e212fcab
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '461'
ht-degree: 0%

---

# RBOP语法 {#rbop-grammar}

本节介绍配置输入的语法，重点介绍有效和无效的输入选项，并解释如何解释省略的可选字段。

基于分辨率的输出保护语法被定义为一系列规则，其中每个规则可以有多个有效的形式：

```
Rule ::=       
 
    Form 
     
AnotherRule ::=     
 
    DifferentForm 
```

## 应用语法规则 {#section_A7216BD585FF4EB88737B643B36C2781}

>[!NOTE]
>
>为了帮助提高语法的可读性，以下属性未反映在语法中，但仍保留true：

1. 对象中定义的对的顺序不是固定的；因此，对的任何置换都是有效的。

   例如，如果我们定义了一个对象，如下所示：

   ```
   {  
     "foo": <Foo>,  
     "bar":<Bar>,  
     "baz":<Baz>  
   }
   ```

   则以下结构也将被视为有效： =

   ```
   {  
     "baz":<Baz>,  
     "foo":<Foo>,  
     "bar":<Bar> 
   }
   ```

1. 对于对象中的每个对，假定给定对象的给定实例中仅存在该对的1个实例。

   例如，如果我们定义了一个对象，如下所示：

   ```
   {  
     "foo": <Foo>,  
     "bar":<Bar>,  
     "baz":<Baz>  
   }
   ```

   则以下实例将无效，因为存在两个 `foo` 个对在同一对象中：

   ```
   { 
     "foo":<Foo>,  
     "bar":<Bar>,  
     "baz":<Baz>,  
   } 
   ```

   同样，有两个对象，例如：

   ```
   {  
     "foo": <Foo>,  
     "bar":<Bar>,  
     "baz":<Baz>  
   }
   ```

   和：

   ```
   {  
     "baz":<Baz>,  
     "foo":<Foo>,  
     "bar":<Bar> 
   }
   ```

   有效，因为它们是同一对象的独立实例。

1. 对于可能选择一个或多个字符串序列的定义，请将字符串视为一个集合，其中重复条目被视为单个条目。 例如， `["foo", "bar", "foo", "baz"]` 相当于 `["foo", "bar", "baz"]`

1. 定义数字时，规则之间使用空格，(例如， `Digit Digits`)，但在应用规则时不应使用此类空格。

   例如，如果我们表示 *一百二十三* 根据NonZeroInteger规则，它应表示为 `123` 而不是 `1 2 3`，即使规则在NonZeroDigit和Digits之间包含空格。

1. 某些规则允许使用多个表单。 在这些情况下，不同形式之间会使用 `'|'` 字符。

   例如，此规则：

   ```
   Foo ::= "A" | "B" | "C"
   ```

   表示实例 `Foo` 可以替换为“A”、“B”或“C”。 这不应与跨多行的表单混淆；这是使更长的表单更易读的功能。

## 语法 {#section_52189FD66B1A46BA9F8FDDE1D7C8E8E8}

```
PixelBasedOPConfig ::= 
      {} 
    | { "maxPixel": NonNegativeInteger } 
    | { "pixelConstraints": PixelConstraintsSeq } 
    | { "pixelConstraints": PixelConstraintsSeq, 
        "maxPixel": NonNegativeInteger } 
 
PixelConstraintsSeq ::= 
      [] 
    | [ PixelConstraints ] 
 
PixelConstraints ::= 
      PixelConstraint 
    | PixelConstraint, PixelConstraints 
 
PixelConstraint ::= 
      { "pixelCount": NonNegativeInteger } 
    | { "pixelCount": NonNegativeInteger, 
        "digital": DigitalOutputRestrictionsSeq } 
    | { "pixelCount": NonNegativeInteger, 
        "analog": AnalogOutputRestriction } 
    | { "pixelCount": NonNegativeInteger, 
        "ota": OTAOutputRestriction } 
    | { "pixelCount": NonNegativeInteger, 
        "digital": DigitalOutputRestrictionsSeq, 
        "analog": AnalogOutputRestriction } 
    | { "pixelCount": NonNegativeInteger, 
        "digital": DigitalOutputRestrictionsSeq, 
         "ota": OTAOutputRestriction } 
    | { "pixelCount": NonNegativeInteger, 
        "analog": AnalogOutputRestriction, 
        "ota": OTAOutputRestriction } 
    | { "pixelCount": NonNegativeInteger, 
        "digital": DigitalOutputRestrictionsSeq, 
        "analog": AnalogOutputRestriction, 
        "ota": OTAOutputRestriction } 
 
DigitalOutputRestrictionsSeq ::= 
      [] 
    | [ DigitalOutputRestrictions ] 
 
DigitalRestrictions ::= 
      DigitalRestriction 
    | DigitalRestriction, DigitalRestrictions 
 
DigitalRestriction ::= 
      { "output": DigitalOutputOption } 
    | { "output": DigitalOutputOption, "hdcp": HDCP } 
 
DigitalOutputOption ::= 
      "NO_PROTECTION" 
    | "USE_IF_AVAILABLE" 
    | "REQUIRED" 
    | "NO_PLAYBACK" 
 
HDCP ::= 
    { "major": PositiveInteger, "minor": NonNegativeInteger } 
 
AnalogOutputRestriction ::= 
    { "output": AnalogOutputOption } 
 
AnalogOutputOption ::= 
      "NO_PROTECTION" 
    | "USE_IF_AVAILABLE" 
    | "USE_IF_AVAILABLE_ACP" 
    | "USE_IF_AVAILABLE_CGMSA" 
    | "REQUIRED" 
    | "REQUIRED_ACP" 
    | "REQUIRED_CGMSA" 
    | "NO_PLAYBACK" 
 
OTAOutputRestriction ::= 
    { "whitelist": OTAWhitelistSeq } 
 
OTAWhitelistSeq ::= 
      [] 
    | [ OTAWhitelist ] 
 
OTAWhitelist ::= 
      OTAConnectionType 
    | OTAConnectionType, OTAWhitelist 
 
OTAConnectionType ::= 
      "MIRACAST" 
    | "AIRPLAY" 
    | "WIDI" 
    | "DLNA" 
 
NonNegativeInteger ::= 
      Digit 
    | NonZeroDigit Digits 
 
PositiveInteger ::= 
      NonZeroDigit 
    | NonZeroDigit Digits 
 
Digits ::= 
      Digit 
    | Digit Digits 
 
Digit ::= 
      0 
    | NonZeroDigit

NonZeroDigit ::= 
      1 
    | 2 
    | 3 
    | 4 
    | 5 
    | 6 
    | 7 
    | 8 
    | 9
```

## 语义：合法但无效的配置 {#section_709BE240FF0041D4A1B0A0A7544E4966}

此 *示例输出保护配置* 主题给出了一个有效的配置及其语义含义。 中的上一节 *此* 主题介绍了配置的语法规则。 虽然语法有助于确保语法正确，但存在语义上不正确的语法法律配置（即它们不符合逻辑）。 本节介绍以下配置 *语法* 合法的，但是 *语义上* 不正确。 请记住，本节中的示例已简化为说明所讨论情景所需的最低结构。

* 定义具有相同像素数的多个像素约束是无效的。

   ```
   {  
     "pixelConstraints":  
       [  
         { "pixelCount": 720 }  
       ]  
    }  
   ```

* 像素计数不能超过指定的最大像素分辨率。

   ```
   { 
     "maxPixel": 720, 
     "pixelConstraints": 
       [ 
         {"pixelCount": 1080} 
       ] 
   } 
   ```
