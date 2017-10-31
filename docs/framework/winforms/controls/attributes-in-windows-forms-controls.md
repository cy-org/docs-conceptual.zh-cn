---
title: "Windows 窗体控件中的特性 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-winforms"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "jsharp"
helpviewer_keywords: 
  - "特性 [Windows 窗体]"
  - "特性 [Windows 窗体], 类"
  - "特性 [Windows 窗体], 控件属性"
  - "特性 [Windows 窗体], 数据绑定属性"
ms.assetid: 2c5640e9-6c6c-49d7-a5e4-a768f6be7853
caps.latest.revision: 15
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 15
---
# Windows 窗体控件中的特性
.NET Framework 提供了多种可应用于自定义控件和组件的成员的特性。  这些特性中有些会影响类的运行时行为，有些会影响设计时行为。  
  
## 控件和组件属性的特性  
 下表显示了可应用于属性或自定义控件和组件的其他成员的特性。  有关使用其中许多特性的示例，请参见 [如何：应用 Windows 窗体控件中的特性](../../../../docs/framework/winforms/controls/how-to-apply-attributes-in-windows-forms-controls.md)。  
  
|特性|说明|  
|--------|--------|  
|<xref:System.ComponentModel.AmbientValueAttribute>|指定将传递给属性的值，以使该属性从另一个来源获取其值。  这称为*“环境”*。|  
|<xref:System.ComponentModel.BrowsableAttribute>|指定某一属性或事件是否应在**“属性”**窗口中显示。|  
|<xref:System.ComponentModel.CategoryAttribute>|指定在设置为 <xref:System.Windows.Forms.PropertySort> 模式的 <xref:System.Windows.Forms.PropertyGrid> 控件中显示时对属性或事件进行分组的类别的名称。|  
|<xref:System.ComponentModel.DefaultValueAttribute>|指定属性的默认值。|  
|<xref:System.ComponentModel.DescriptionAttribute>|指定属性或事件的说明。|  
|<xref:System.ComponentModel.DisplayNameAttribute>|为属性、事件或不接受参数的 `public` `void` 方法指定显示名称。|  
|<xref:System.ComponentModel.EditorAttribute>|指定用于更改属性的编辑器。|  
|<xref:System.ComponentModel.EditorBrowsableAttribute>|指定某一属性或方法在编辑器中可见。|  
|<xref:System.ComponentModel.Design.HelpKeywordAttribute>|指定类或成员的上下文关键字。|  
|<xref:System.ComponentModel.LocalizableAttribute>|指定是否应本地化某一属性。|  
|<xref:System.ComponentModel.PasswordPropertyTextAttribute>|指示对象的文本表示形式由星号等字符遮盖。|  
|<xref:System.ComponentModel.ReadOnlyAttribute>|指定此特性所绑定到的属性在设计时是只读的还是可读\/写的。|  
|<xref:System.ComponentModel.RefreshPropertiesAttribute>|指示在关联属性值更改时应刷新属性网格。|  
|<xref:System.ComponentModel.TypeConverterAttribute>|指定对于此特性绑定到的对象要使用哪种类型作为转换器。|  
  
## 数据绑定属性的特性  
 下表显示了可用于指定自定义控件和组件如何与数据绑定交互的特性。  
  
|特性|说明|  
|--------|--------|  
|<xref:System.ComponentModel.BindableAttribute>|指定属性是否通常用于绑定。|  
|<xref:System.ComponentModel.ComplexBindingPropertiesAttribute>|指定组件的数据源和数据成员属性。|  
|<xref:System.ComponentModel.DefaultBindingPropertyAttribute>|指定组件的默认绑定属性。|  
|<xref:System.ComponentModel.LookupBindingPropertiesAttribute>|指定组件的数据源和数据成员属性。|  
|<xref:System.ComponentModel.AttributeProviderAttribute>|启用特性重定向。|  
  
## 类的特性  
 下表显示了可用于在设计时指定自定义控件和组件的行为的特性。  
  
|特性|说明|  
|--------|--------|  
|<xref:System.ComponentModel.DefaultEventAttribute>|指定组件的默认事件。|  
|<xref:System.ComponentModel.DefaultPropertyAttribute>|指定组件的默认属性。|  
|<xref:System.ComponentModel.DesignerAttribute>|指定用于为组件实现设计时服务的类。|  
|<xref:System.ComponentModel.DesignerCategoryAttribute>|为属于某一类别的类指定设计器。|  
|<xref:System.ComponentModel.ToolboxItemAttribute>|表示工具箱项的特性。|  
|<xref:System.ComponentModel.ToolboxItemFilterAttribute>|为工具箱项指定要使用的筛选器字符串和筛选器类型。|  
  
## 请参阅  
 <xref:System.Attribute>   
 [如何：应用 Windows 窗体控件中的特性](../../../../docs/framework/winforms/controls/how-to-apply-attributes-in-windows-forms-controls.md)   
 [Extending Design\-Time Support](../Topic/Extending%20Design-Time%20Support.md)   
 [使用 .NET Framework 开发自定义 Windows 窗体控件](../../../../docs/framework/winforms/controls/developing-custom-windows-forms-controls.md)