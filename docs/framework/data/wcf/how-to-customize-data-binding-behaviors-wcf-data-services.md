---
title: "如何：自定义数据绑定行为（WCF 数据服务） | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-oob"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "WCF 数据服务, 自定义"
  - "WCF 数据服务, 数据绑定"
ms.assetid: 40476b89-8941-4771-8d21-2fe430c85a9d
caps.latest.revision: 2
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 2
---
# 如何：自定义数据绑定行为（WCF 数据服务）
通过 [!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)]，您可以提供当向绑定集合中添加对象或从中移除对象时或检测到属性更改时由 <xref:System.Data.Services.Client.DataServiceCollection%601> 调用的自定义逻辑。  此自定义逻辑作为方法提供，作为 <xref:System.Func%602> 委托引用，如果在自定义方法完成时仍应执行默认行为，则返回 `false` 值；如果事件的后续处理应停止，则返回 `true` 值。  
  
 本主题中的示例为 <xref:System.Data.Services.Client.DataServiceCollection%601> 的 `entityChanged` 和 `entityCollectionChanged` 参数提供了自定义方法。  本主题中的示例使用 Northwind 示例数据服务和自动生成的客户端数据服务类。  此服务和这些客户端数据类是在完成 [WCF 数据服务快速入门](../../../../docs/framework/data/wcf/quickstart-wcf-data-services.md)时创建的。  
  
## 示例  
 下面的 XAML 文件代码隐藏页使用当更改绑定到绑定集合的数据时调用的自定义方法来创建 <xref:System.Data.Services.Client.DataServiceCollection%601>。  当发生 <xref:System.Collections.ObjectModel.ObservableCollection%601.CollectionChanged> 事件时，提供的方法阻止从数据服务删除已从绑定集合移除的项。  当发生 <xref:System.Collections.ObjectModel.ObservableCollection%601.PropertyChanged> 事件时，验证 `ShipDate` 值以确保不对已发货的订单进行更改。  
  
 [!code-csharp[Astoria Northwind Client#WpfDataBindingCustom](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria northwind client/cs/customerorderscustom.xaml.cs#wpfdatabindingcustom)]
 [!code-vb[Astoria Northwind Client#WpfDataBindingCustom](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria northwind client/vb/customerorderscustom.xaml.vb#wpfdatabindingcustom)]
 [!code-vb[Astoria Northwind Client#WpfDataBindingCustom](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria northwind client/vb/customerorderscustom2.xaml.vb#wpfdatabindingcustom)]  
  
## 示例  
 下面的 XAML 定义上例的窗口。  
  
 [!code-xml[Astoria Northwind Client#WpfDataBindingCustomXaml](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria northwind client/vb/customerorderscustom.xaml#wpfdatabindingcustomxaml)]  
  
## 请参阅  
 [WCF 数据服务客户端库](../../../../docs/framework/data/wcf/wcf-data-services-client-library.md)