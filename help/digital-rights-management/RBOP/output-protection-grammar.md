---
description: 本节介绍配置输入的语法，强调有效和无效的输入选项，并解释如何解释忽略的可选字段。
seo-description: 本节介绍配置输入的语法，强调有效和无效的输入选项，并解释如何解释忽略的可选字段。
seo-title: RBOP语法
title: RBOP语法
uuid: d9064e39-593a-4767-b835-287640b4c94a
translation-type: tm+mt
source-git-commit: e60d285b9e30cdd19728e3029ecda995cd100ac9

---


# RBOP语法 {#rbop-grammar}

本节介绍配置输入的语法，强调有效和无效的输入选项，并解释如何解释忽略的可选字段。

基于分辨率的输出保护语法被定义为规则序列，其中每个规则可以具有多个有效的表单：

```
Rule ::=       
 
    Form 
     
AnotherRule ::=     
 
    DifferentForm 
```

## 应用语法规则 {#section_A7216BD585FF4EB88737B643B36C2781}

>[!NOTE]
>
>为了帮助提高语法的可读性，以下属性不会反映在语法中，但仍然保持真：

1. 对象中定义的对的顺序没有固定；因此，对的任何排列都是有效的。

   例如，如果我们定义了如下对象：

   ```
   {  
     "foo": <Foo>,  
     "bar":<Bar>,  
     "baz":<Baz>  
   }
   ```

   那么，以下结构也将被视为有效：=

   ```
   {  
     "baz":<Baz>,  
     "foo":<Foo>,  
     "bar":<Bar> 
   }
   ```

1. 对于对象中的每对，假定给定对象的给定实例中仅存在该对的1个实例。

   例如，如果我们定义了如下对象：

   ```
   {  
     "foo": <Foo>,  
     "bar":<Bar>,  
     "baz":<Baz>  
   }
   ```

   那么，以下实例将无效，因为同一对象中 `foo` 有两对：

   ```
   { 
     "foo":<Foo>,  
     "bar":<Bar>,  
     "baz":<Baz>,  
   } 
   ```

   同样，具有两个对象，如：

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

1. 对于可以选择一个或多个字符串序列的定义，请将字符串视为一组，其中重复的条目被视为单个条目。 例如， `["foo", "bar", "foo", "baz"]` 等同于 `["foo", "bar", "baz"]`

1. 为了定义数字，在规则(例如， `Digit Digits`)之间使用一个空间，但在应用规则时不应使用此空间。

   例如，如果我们用每个NonZeroInteger规则表示数字123 *，则它应表示为*`123``1 2 3`，而不是表示为，即使该规则包含NonZeroDigit和Digits之间的空格。

1. 某些规则允许使用多个表单。 在这些情况下，不同的表单由字符分 `'|'` 隔。

   例如，此规则：

   ```
   Foo ::= "A" | "B" | "C"
   ```

   表示实例 `Foo` 可替换为“A”、“B”或“C”。 这不应与跨多行的表单混淆；这是使更长表单更易读的功能。

## 《语法》 {#section_52189FD66B1A46BA9F8FDDE1D7C8E8E8}

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

## 语义学：合法但无效的配置 {#section_709BE240FF0041D4A1B0A0A7544E4966}

“示 *例输出保护配置* ”主题给出了一个有效的配置及其语义。 本主题的上一节 *介绍* ，配置的语法规则。 虽然语法有助于确保句法正确性，但存在语法上合法的配置，这些配置在语义上不正确（即它们不是逻辑配置）。 本节介绍的配置在语法 *上合法* ，但语 *义上不正确* 。 请记住，本节中的示例已减少到说明所讨论的方案所需的最低结构。

* 定义具有相同像素数的多个像素约束是无效的。

   ```
   {  
     "pixelConstraints":  
       [  
         { "pixelCount": 720 }  
       ]  
    }  
   ```

* 像素数不能超过指定的最大像素分辨率。

   ```
   { 
     "maxPixel": 720, 
     "pixelConstraints": 
       [ 
         {"pixelCount": 1080} 
       ] 
   } 
   ```
