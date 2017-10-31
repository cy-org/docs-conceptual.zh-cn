---
title: "如何：绑定到方法 | Microsoft Docs"
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
  - "绑定, 到方法"
  - "类, ObjectDataProvider"
  - "Data Binding — 数据绑定, 使用 ObjectDataProvider 绑定到方法"
  - "方法, 绑定"
  - "ObjectDataProvider 类"
ms.assetid: 5f55e71e-2182-42a0-88d1-700cc1427a7a
caps.latest.revision: 10
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 9
---
# 如何：绑定到方法
下面的示例演示如何使用 <xref:System.Windows.Data.ObjectDataProvider> 绑定到方法。  
  
## 示例  
 在本例中，`TemperatureScale` 是一个类，它有一个方法 `ConvertTemp`，该方法接收两个参数（分别为 `double` 类型和 `enum` 类型的 `TempType`），并将给定值从一个温标转换为另一个温标。  在下面的示例中，<xref:System.Windows.Data.ObjectDataProvider> 用于实例化 `TemperatureScale` 对象。  将使用两个指定参数调用 `ConvertTemp` 方法。  
  
 [!code-xml[BindToMethod#WindowResources](../../../../samples/snippets/csharp/VS_Snippets_Wpf/BindToMethod/CS/Window1.xaml#windowresources)]  
  
 方法可以作为资源使用，因此您可绑定到其结果。  在以下示例中，<xref:System.Windows.Controls.TextBox> 的 <xref:System.Windows.Controls.TextBox.Text%2A> 属性和 <xref:System.Windows.Controls.ComboBox> 的 <xref:System.Windows.Controls.Primitives.Selector.SelectedValue%2A> 绑定到方法的两个参数。  用户可借此指定要转换到的温度以及要转换自的温标。  请注意，<xref:System.Windows.Data.Binding.BindsDirectlyToSource%2A> 设置为 `true`，因为我们要绑定到 <xref:System.Windows.Data.ObjectDataProvider> 实例的 <xref:System.Windows.Data.ObjectDataProvider.MethodParameters%2A> 属性，而不是绑定到由 <xref:System.Windows.Data.ObjectDataProvider> 包装的对象（`TemperatureScale` 对象）的属性。  
  
 用户修改 <xref:System.Windows.Controls.TextBox> 的内容或 <xref:System.Windows.Controls.ComboBox> 的选定内容时，最后一个 <xref:System.Windows.Controls.Label> 的 <xref:System.Windows.Controls.ContentControl.Content%2A> 将更新。  
  
 [!code-xml[BindToMethod#UI](../../../../samples/snippets/csharp/VS_Snippets_Wpf/BindToMethod/CS/Window1.xaml#ui)]  
  
 转换器 `DoubleToString` 接收一个 double 类型的数据，并以 <xref:System.Windows.Data.IValueConverter.Convert%2A> 方向（从[绑定资源](GTMT)到[绑定目标](GTMT)，绑定目标是 <xref:System.Windows.Controls.TextBox.Text%2A> 属性）将其转换为 string 类型，并以 <xref:System.Windows.Data.IValueConverter.ConvertBack%2A> 方向将 `string` 转换为 `double`。  
  
 `InvalidationCharacterRule` 是一个 <xref:System.Windows.Controls.ValidationRule>，用于检查无效字符。  默认的错误模板是一个围绕在 <xref:System.Windows.Controls.TextBox> 四周的红色边框，用于在输入值不是一个 double 类型的值时向用户发出通知。  
  
## 请参阅  
 [帮助主题](../../../../docs/framework/wpf/data/data-binding-how-to-topics.md)   
 [绑定到枚举](../../../../docs/framework/wpf/data/how-to-bind-to-an-enumeration.md)