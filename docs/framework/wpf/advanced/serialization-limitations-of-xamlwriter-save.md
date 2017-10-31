---
title: "XamlWriter.Save 的序列化限制 | Microsoft Docs"
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
  - "XamlWriter.Save 的限制"
  - "XamlWriter.Save 的序列化限制"
  - "XamlWriter.Save, 序列化限制"
ms.assetid: f86acc91-2b67-4039-8555-505734491d36
caps.latest.revision: 10
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 9
---
# XamlWriter.Save 的序列化限制
[!INCLUDE[TLA#tla_api](../../../../includes/tlasharptla-api-md.md)] <xref:System.Windows.Markup.XamlWriter.Save%2A> 可用于将 [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] 应用程序的内容序列化为一个[!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] 文件。  但是，对于明确序列化的内容还有一些显著的限制。  本主题论述了这些限制和某些一般注意事项。  
  
   
  
<a name="Run_Time__Not_Design_Time_Representation"></a>   
## 运行时表示形式而非设计时表示形式  
 通过调用 <xref:System.Windows.Markup.XamlWriter.Save%2A> 对内容进行序列化的基本原理是：在运行时会生成序列化对象的表示形式。  在将 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 作为内存中的对象进行加载时，原始 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 文件的许多设计时属性可能已经优化或丢失，而且在调用 <xref:System.Windows.Markup.XamlWriter.Save%2A> 进行序列化时未保留这些属性。  序列化的结果是应用程序的结构化逻辑树的有效表示形式，但并不一定是生成该树的原始 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)]。  这些问题使得将 <xref:System.Windows.Markup.XamlWriter.Save%2A> 序列化用作大型 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 设计图面的一部分变得极为困难。  
  
<a name="Serialization_is_Self_Contained"></a>   
## 序列化是独立的  
 <xref:System.Windows.Markup.XamlWriter.Save%2A> 的序列化输出是独立的；序列化的所有内容都包含在单个 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 页面中，该页面具有单个根元素而且没有除 [!INCLUDE[TLA2#tla_uri#plural](../../../../includes/tla2sharptla-urisharpplural-md.md)] 以外的外部引用。  例如，如果您的页面从应用程序资源引用了资源，则这些资源看上去如同正在进行序列化的页面的一个组件。  
  
<a name="Extension_References_are_Dereferenced"></a>   
## 取消引用扩展引用  
 由各种标记扩展格式（如 `StaticResource` 或 `Binding`）对对象进行的公共引用将会由序列化过程取消引用。  当应用程序运行时创建内存中的对象时，已经将这些公共引用取消引用，而且 <xref:System.Windows.Markup.XamlWriter.Save%2A> 逻辑不会重新访问原始的 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 来将这些引用还原到序列化的输出。  这样可能会将任何数据绑定或资源获得的值冻结为运行时表示形式最后使用的值，并且只能有限地或间接地区别这样的值与任何其他在本地设置的值。  由于图像存在于项目中，因此图像也会序列化为图像的对象引用（而不是原始的源引用），从而会丢失原来引用的文件名或 [!INCLUDE[TLA2#tla_uri](../../../../includes/tla2sharptla-uri-md.md)]。  即使在同一页面内声明的资源也会序列化到引用点处，而不是作为资源集合的键进行保留。  
  
<a name="Event_Handling_is_Not_Preserved"></a>   
## 不保留事件处理  
 当对通过 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 添加的事件处理程序进行序列化后，不会保留这些事件处理程序。  没有代码隐藏功能（而且也没有相关的 x:Code 机制）的 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 无法对运行时的过程逻辑进行序列化。  因为序列化是独立的并局限于逻辑树，所以没有工具可用于存储事件处理程序。  因此，事件处理程序特性（即特性本身和命名处理程序的字符串值）都会从输出 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 中移除。  
  
<a name="Realistic_Scenarios_for_Use_of_XAMLWriter_Save"></a>   
## 使用 XAMLWriter.Save 的真实方案  
 虽然这里列出的限制相当多，但仍然有几种适当的方案适合使用 <xref:System.Windows.Markup.XamlWriter.Save%2A> 进行序列化。  
  
-   向量或图形输出：呈现的区域的输出可用于在重新加载时重新生成相同的向量或图形。  
  
-   多格式文本和流文档：输出中会保留文本以及文本内的所有元素格式和元素包容。  这对类似于剪贴板功能的机制可能非常有用。  
  
-   保留业务对象数据：如果您已经在自定义元素中存储了数据（如 [!INCLUDE[TLA2#tla_xml](../../../../includes/tla2sharptla-xml-md.md)] 数据），则只要您的业务对象遵循基本的 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 规则（如提供自定义构造函数和按引用属性值转换），这些业务对象就可以通过序列化永久保留。