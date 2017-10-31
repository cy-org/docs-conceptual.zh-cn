---
title: "本地化特性和注释 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-wpf"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Localization — 本地化, 特性"
  - "Localization — 本地化, 注释"
ms.assetid: ead2d9ac-b709-4ec1-a924-39927a29d02f
caps.latest.revision: 15
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 14
---
# 本地化特性和注释
[!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] 本地化注释是由开发人员提供的 [!INCLUDE[TLA#tla_titlexaml](../../../../includes/tlasharptla-titlexaml-md.md)] 源代码中的属性，用来提供本地化规则和提示。  [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] 本地化注释中包含两组信息：可本地化特性和任意形式的本地化注释。  可本地化特性由 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 本地化 API 用来指示将对哪些资源进行本地化。  任意形式的本地化注释是指应用程序作者希望包括的任何信息。  
  
   
  
<a name="Localizer_Comments_"></a>   
## 本地化注释  
 如果标记应用程序的作者对 [!INCLUDE[TLA#tla_titlexaml](../../../../includes/tlasharptla-titlexaml-md.md)] 中的特定元素具有一定的要求（如对文本长度、字体系列或字号进行约束），那么，他们可以借助于 [!INCLUDE[TLA#tla_titlexaml](../../../../includes/tlasharptla-titlexaml-md.md)] 代码中的注释将该信息传达给本地化人员。  下面是用来向源代码中添加注释的过程：  
  
1.  应用程序开发人员向 [!INCLUDE[TLA#tla_titlexaml](../../../../includes/tlasharptla-titlexaml-md.md)] 源代码中添加本地化注释。  
  
2.  在生成过程中，可以在 .proj 文件中指定是将任意形式的本地化注释留在程序集内、去掉部分注释还是去掉所有的注释。  已去掉的注释将放在一个单独的文件中。  您可以使用如下所示的 `LocalizationDirectivesToLocFile` 标记来指定您的选项：  
  
     `<LocalizationDirectivesToLocFile>` *值* `</LocalizationDirectivesToLocFile>`  
  
3.  下面是可以赋予的值：  
  
    -   **None** \- 注释和特性均留在程序集内，而且不生成单独的文件。  
  
    -   **CommentsOnly** \- 仅去掉程序集内的注释，并将它们放在一个单独的 LocFile 中。  
  
    -   **All** \- 去掉程序集内的注释和特性，并将它们放在一个单独的 LocFile 文件中。  
  
4.  当从 [!INCLUDE[TLA2#tla_baml](../../../../includes/tla2sharptla-baml-md.md)] 中提取可本地化的资源时，可本地化特性将由 [!INCLUDE[TLA2#tla_baml](../../../../includes/tla2sharptla-baml-md.md)] 本地化 API 保留。  
  
5.  以后可以将仅包含任意形式注释的本地化注释文件合并到本地化过程中。  
  
 下面的示例演示如何向 [!INCLUDE[TLA#tla_titlexaml](../../../../includes/tlasharptla-titlexaml-md.md)] 文件中添加本地化注释。  
  
 `<TextBlock x:Id = "text01"`  
  
 `FontFamily = "Microsoft Sans Serif"`  
  
 `FontSize = "12"`  
  
 `Localization.Attributes = "$Content (Unmodifiable Readable Text)`  
  
 `FontFamily (Unmodifiable Readable)"`  
  
 `Localization.Comments = "$Content (Trademark)`  
  
 `FontSize (Trademark font size)" >`  
  
 `Microsoft`  
  
 `</TextBlock>`  
  
 在上面的示例中，Localization.Attributes 部分包含本地化特性，Localization.Comments 部分包含自由形式的注释。  下面的几个表显示了各个特性和注释及其对于本地化人员的含义。  
  
|本地化特性|含义|  
|-----------|--------|  
|$Content（无法修改的可读文本）|TextBlock 元素的内容无法修改。  本地化人员不能更改“Microsoft”一词。  该内容对于本地化人员来说是可见的（可读的）。  该内容属于文本类别。|  
|FontFamily（无法修改的可读文本）|TextBlock 元素的字体系列属性无法更改，但是它对于本地化人员是可见的。|  
  
|任意形式的本地化注释|含义|  
|----------------|--------|  
|$Content（商标）|应用程序作者告诉本地化人员 TextBlock 元素中的内容是商标。|  
|FontSize（商标的字号）|应用程序作者指示字号属性应当遵循标准商标大小。|  
  
### 可本地化特性  
 Localization.Attributes 中的信息包含一系列信息对：目标值名称及其相关的可本地化值。  目标名称可以是属性名称或者特殊的 $Content 名称。  如果这是属性名称，则目标值是该属性的值。  如果这是 $Content，则目标值是该元素的内容。  
  
 有三种类型的特性：  
  
-   **Category**。  该属性指定某个值是否应当从本地化工具中修改。  请参见 <xref:System.Windows.LocalizabilityAttribute.Category%2A>。  
  
-   **Readability**。  该属性指定某个值是否应当从本地化工具中读取（和显示）。  请参见 <xref:System.Windows.LocalizabilityAttribute.Readability%2A>。  
  
-   **Modifiability**。  该属性指定本地化工具是否允许对某个值进行修改。  请参见 <xref:System.Windows.LocalizabilityAttribute.Modifiability%2A>。  
  
 这些特性可以按照由空格分开的任何顺序来指定。  如果指定了重复特性，则最后一个特性将重写前面的特性。  例如，Localization.Attributes \= "Unmodifiable Modifiable" 会将 Modifiability 设置为 Modifiable，因为最后一个值是 Modifiable。  
  
 Modifiability 和 Readability 的名称已经揭示了自身的含义。  Category 特性提供的预定义类别可帮助本地化人员翻译文本。  类别（如 Text、Label 和 Title）为本地化人员提供了有关如何翻译文本的信息。  还有一些特殊类别：None、Inherit、Ignore 和 NeverLocalize。  
  
 下表显示了这些特殊类别的含义。  
  
|类别|含义|  
|--------|--------|  
|无|没有为目标值定义类别。|  
|Inherit|目标值从其父级继承类别。|  
|忽略|在本地化过程中忽略目标值。  Ignore 仅影响当前值，  而不会影响子节点。|  
|NeverLocalize|不能对当前值进行本地化。  元素的子级可以继承此类别。|  
  
<a name="Localization_Comments"></a>   
## 本地化注释  
 Localization.Comments 包含与目标值有关的任意形式的字符串。  应用程序开发人员可以添加一些信息，以便为本地化人员提供有关如何翻译应用程序文本的提示。  注释的格式可以是由“\(\)”括起来的任何字符串。  可以使用“\\”来对字符进行转义。  
  
## 请参阅  
 [WPF 的全球化](../../../../docs/framework/wpf/advanced/globalization-for-wpf.md)   
 [使用自动布局创建按钮](../../../../docs/framework/wpf/advanced/how-to-use-automatic-layout-to-create-a-button.md)   
 [使用网格进行自动布局](../../../../docs/framework/wpf/advanced/how-to-use-a-grid-for-automatic-layout.md)   
 [对应用程序进行本地化](../../../../docs/framework/wpf/advanced/how-to-localize-an-application.md)