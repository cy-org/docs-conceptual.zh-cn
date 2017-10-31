---
title: "配置工作流服务中的序列化 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: aa70b290-a2ee-4c3c-90ea-d0a7665096ae
caps.latest.revision: 4
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 4
---
# 配置工作流服务中的序列化
工作流服务是 [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 服务，因此可以选择使用 <xref:System.Runtime.Serialization.DataContractSerializer>（默认）或 <xref:System.Xml.Serialization.XmlSerializer>。编写非工作流服务时，将在服务或操作协定上指定要使用的序列化程序的类型。创建 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 工作流服务时，不会在代码中指定这些协定，而是在运行时通过协定推理生成这些协定。[!INCLUDE[crabout](../../../../includes/crabout-md.md)]协定推理的更多信息，请参见[在工作流中使用协定](../../../../docs/framework/wcf/feature-details/using-contracts-in-workflow.md)。序列化程序是使用 <xref:System.ServiceModel.Activities.Receive.SerializerOption%2A> 属性指定的。这可在设计器中进行设置，如下图所示。  
  
 ![设置序列化程序](../../../../docs/framework/wcf/feature-details/media/settingserialzier.png "SettingSerialzier")  
  
 序列化程序也可在代码中进行设置，如下面的示例所示。  
  
```  
Receive approveExpense = new Receive  
            {  
                OperationName = "ApproveExpense",  
                CanCreateInstance = true,  
                ServiceContractName = "FinanceService",  
                SerializerOption = SerializerOption.DataContractSerializer,  
                Content = ReceiveContent.Create(new OutArgument<Expense>(expense))  
            };  
  
```  
  
 也可在工作流服务上指定已知类型。[!INCLUDE[crabout](../../../../includes/crabout-md.md)]已知类型的更多信息，请参见[数据协定已知类型](../../../../docs/framework/wcf/feature-details/data-contract-known-types.md)。可在设计器或代码中指定已知类型。若要在设计器中指定已知类型，请在属性窗口中单击 <xref:System.ServiceModel.Activities.Receive> 活动的 KnownTypes 属性旁边的省略号按钮，如下图所示。  
  
 ![KnownTypes 属性](../../../../docs/framework/wcf/feature-details/media/knowntypes.png "KnownTypes")  
  
 这将显示“类型集合编辑器”，您可以在其中搜索和指定已知类型。  
  
 ![添加已知类型](../../../../docs/framework/wcf/feature-details/media/typecollectionseditor.gif "TypeCollectionsEditor")  
  
 单击**“添加新类型”**链接，并使用下拉菜单选择或搜索某个类型添加到已知类型集合。若要在代码中指定已知类型，请使用 <xref:System.ServiceModel.Activities.Receive.KnownTypes%2A> 属性，如下面的示例所示。  
  
```  
Receive approveExpense = new Receive  
            {  
                OperationName = "ApproveExpense",  
                CanCreateInstance = true,  
                ServiceContractName = "FinanceService",  
                SerializerOption = SerializerOption.DataContractSerializer,  
                Content = ReceiveContent.Create(new OutArgument<Expense>(expense))  
            };  
            approveExpense.KnownTypes.Add(typeof(Travel));  
            approveExpense.KnownTypes.Add(typeof(Meal));  
  
```  
  
 若要查看演示如何配置工作流服务的序列化的完整代码示例，请参见[在工作流服务中设置消息格式](../../../../docs/framework/windows-workflow-foundation/samples/formatting-messages-in-workflow-services.md)。