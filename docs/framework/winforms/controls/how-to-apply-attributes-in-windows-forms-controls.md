---
title: "如何：应用 Windows 窗体控件中的特性 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-winforms"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "jsharp"
helpviewer_keywords: 
  - "特性 [Windows 窗体], 应用"
  - "控件 [Windows 窗体], 应用特性"
  - "Windows 窗体控件, 应用特性"
ms.assetid: af0a3f7f-155b-4ba1-83c4-9cf721331a06
caps.latest.revision: 10
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 10
---
# 如何：应用 Windows 窗体控件中的特性
若要开发与设计环境正确交互，并在运行时正确执行的组件和控件，您需要将特性正确地应用于类和成员。  
  
## 示例  
 下面的代码示例演示如何使用一个自定义控件上的多个特性。  该控件演示了一个简单的日志功能。  当该控件绑定到某个数据源时，它会在 <xref:System.Windows.Forms.DataGridView> 控件中显示由数据源发送的值。  如果某个值超过了由 `Threshold` 属性指定的值，则会引发 `ThresholdExceeded` 事件。  
  
 `AttributesDemoControl` 使用 `LogEntry` 类记录值。  `LogEntry` 类是一个模板类，这意味着它的参数化由它记录的类型确定。  例如，如果 `AttributesDemoControl` 记录 `float` 类型的值，则每个 `LogEntry` 实例按如下方法进行声明和使用。  
  
 [!code-csharp[System.ComponentModel.AttributesDemoControl#110](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.ComponentModel.AttributesDemoControl/CS/form1.cs#110)]
 [!code-vb[System.ComponentModel.AttributesDemoControl#110](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.ComponentModel.AttributesDemoControl/VB/form1.vb#110)]  
  
> [!NOTE]
>  由于 `LogEntry` 是由任意类型参数化的，因此它必须使用反射来对该参数类型进行操作。  为了使阈值功能起作用，参数类型 `T` 必须实现 <xref:System.IComparable> 接口。  
  
 承载 `AttributesDemoControl` 的窗体定期查询性能计数器。  每个值都打包在相应类型的 `LogEntry` 中，并添加至窗体的 <xref:System.Windows.Forms.BindingSource>。  `AttributesDemoControl` 通过其数据绑定接收值，并在 <xref:System.Windows.Forms.DataGridView> 控件中显示该值。  
  
 [!code-csharp[System.ComponentModel.AttributesDemoControl#1](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.ComponentModel.AttributesDemoControl/CS/attributesdemocontrol.cs#1)]
 [!code-vb[System.ComponentModel.AttributesDemoControl#1](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.ComponentModel.AttributesDemoControl/VB/attributesdemocontrol.vb#1)]  
  
 [!code-csharp[System.ComponentModel.AttributesDemoControl#100](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.ComponentModel.AttributesDemoControl/CS/form1.cs#100)]
 [!code-vb[System.ComponentModel.AttributesDemoControl#100](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.ComponentModel.AttributesDemoControl/VB/form1.vb#100)]  
  
 第一个代码示例为 `AttributesDemoControl` 实现。  第二个代码示例演示一个使用 `AttributesDemoControl` 的窗体。  
  
## 类级特性  
 某些特性是在类一级应用的。  下面的代码示例展示了常用于 Windows 窗体控件的特性。  
  
 [!code-csharp[System.ComponentModel.AttributesDemoControl#20](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.ComponentModel.AttributesDemoControl/CS/attributesdemocontrol.cs#20)]
 [!code-vb[System.ComponentModel.AttributesDemoControl#20](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.ComponentModel.AttributesDemoControl/VB/attributesdemocontrol.vb#20)]  
  
### TypeConverter 特性  
 <xref:System.ComponentModel.TypeConverterAttribute> 是另一个常用的类级特性。  下面的代码示例展示如何在 `LogEntry` 类中使用该属性。  此示例还演示了一个针对 `LogEntry` 类型的 <xref:System.ComponentModel.TypeConverter> 实现，称为 `LogEntryTypeConverter`。  
  
 [!code-csharp[System.ComponentModel.AttributesDemoControl#5](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.ComponentModel.AttributesDemoControl/CS/attributesdemocontrol.cs#5)]
 [!code-vb[System.ComponentModel.AttributesDemoControl#5](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.ComponentModel.AttributesDemoControl/VB/attributesdemocontrol.vb#5)]  
  
## 成员级特性  
 某些特性在成员一级应用。  下面的代码示例演示了一些常用于 Windows 窗体控件的属性的特性。  
  
 [!code-csharp[System.ComponentModel.AttributesDemoControl#21](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.ComponentModel.AttributesDemoControl/CS/attributesdemocontrol.cs#21)]
 [!code-vb[System.ComponentModel.AttributesDemoControl#21](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.ComponentModel.AttributesDemoControl/VB/attributesdemocontrol.vb#21)]  
  
### AmbientValue 特性  
 下面的代码示例演示了 <xref:System.ComponentModel.AmbientValueAttribute> 并显示了支持它与设计环境进行交互的代码。  此交互称为“环境”。  
  
 [!code-csharp[System.ComponentModel.AttributesDemoControl#23](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.ComponentModel.AttributesDemoControl/CS/attributesdemocontrol.cs#23)]
 [!code-vb[System.ComponentModel.AttributesDemoControl#23](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.ComponentModel.AttributesDemoControl/VB/attributesdemocontrol.vb#23)]  
  
### Databinding 特性  
 下面的示例演示了一个复杂数据绑定的实现。  前面所示的类级 <xref:System.ComponentModel.ComplexBindingPropertiesAttribute> 指定要用于数据绑定的 `DataSource` 和 `DataMember` 属性。  <xref:System.ComponentModel.AttributeProviderAttribute> 指定 `DataSource` 属性将绑定至的类型。  
  
 [!code-csharp[System.ComponentModel.AttributesDemoControl#25](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.ComponentModel.AttributesDemoControl/CS/attributesdemocontrol.cs#25)]
 [!code-vb[System.ComponentModel.AttributesDemoControl#25](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.ComponentModel.AttributesDemoControl/VB/attributesdemocontrol.vb#25)]  
  
 [!code-csharp[System.ComponentModel.AttributesDemoControl#26](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.ComponentModel.AttributesDemoControl/CS/attributesdemocontrol.cs#26)]
 [!code-vb[System.ComponentModel.AttributesDemoControl#26](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.ComponentModel.AttributesDemoControl/VB/attributesdemocontrol.vb#26)]  
  
## 编译代码  
  
-   承载 `AttributesDemoControl` 的窗体需要有一个对 `AttributesDemoControl` 程序集的引用才能完成生成。  
  
## 请参阅  
 <xref:System.IComparable>   
 <xref:System.Windows.Forms.DataGridView>   
 [使用 .NET Framework 开发自定义 Windows 窗体控件](../../../../docs/framework/winforms/controls/developing-custom-windows-forms-controls.md)   
 [Windows 窗体控件中的特性](../../../../docs/framework/winforms/controls/attributes-in-windows-forms-controls.md)   
 [How to: Serialize Collections of Standard Types with the DesignerSerializationVisibilityAttribute](../Topic/How%20to:%20Serialize%20Collections%20of%20Standard%20Types%20with%20the%20DesignerSerializationVisibilityAttribute.md)