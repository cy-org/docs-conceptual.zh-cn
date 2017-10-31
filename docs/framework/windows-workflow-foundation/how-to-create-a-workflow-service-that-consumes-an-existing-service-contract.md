---
title: "如何：创建使用现有服务协定的工作流服务 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 11d11b59-acc4-48bf-8e4b-e97b516aa0a9
caps.latest.revision: 5
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 5
---
# 如何：创建使用现有服务协定的工作流服务
[!INCLUDE[net_v45](../../../includes/net-v45-md.md)] 以协定优先工作流开发的形式实现了 Web 服务与工作流之间的更佳集成。通过协定优先工作流开发工具，您可以首先用代码来设计协定。该工具随后会针对协定中的操作，在工具箱中自动生成活动模板。  
  
> [!NOTE]
>  本主题提供了有关创建协定优先工作流服务的分步指南。[!INCLUDE[crabout](../../../includes/crabout-md.md)] 协定优先工作流服务开发的更多信息，请参见[协定优先的工作流服务开发](../../../docs/framework/windows-workflow-foundation//contract-first-workflow-service-development.md)。  
  
### 创建工作流项目  
  
1.  在 [!INCLUDE[vs_current_short](../../../includes/vs-current-short-md.md)] 中，选择**“文件”**、**“新建项目”**。在**“模板”**树中的**“C\#”**节点下选择**“WCF”**节点，然后选择**“WCF 工作流服务应用程序”**模板。  
  
2.  将新项目命名为 `ContractFirst`，然后单击**“确定”**。  
  
### 创建服务协定  
  
1.  在**解决方案资源管理器**中右键单击该项目，然后选择**“添加”**、**“新建项...”**。选择左侧的**“代码”**节点和右侧的**“类”**模板。将新类命名为 `IBookService`，然后单击**“确定”**。  
  
2.  在显示的代码窗口的顶部，向 `System.Servicemodel` 添加一个 Using 语句。  
  
    ```  
    using System.ServiceModel;  
    ```  
  
3.  将示例类定义更改为以下接口定义。  
  
    ```  
    [ServiceContract]  
        public interface IBookService  
        {  
            [OperationContract]  
            void Buy(string bookName);  
  
            [OperationContract(IsOneWay=true)]  
            void Checkout();  
        }  
    ```  
  
4.  通过按**“Ctrl\+Shift\+B”**来生成项目。  
  
### 导入服务协定  
  
1.  在**解决方案资源管理器**中右键单击该项目，然后选择**“导入服务协定”**。在**“\<当前项目\>”**下面，打开所有子节点，然后选择**“IBookService”**。单击**“确定”**。  
  
2.  将会打开一个对话框，提示您该操作已成功完成，并且在生成该项目后，所生成的活动将出现在工具箱中。单击**“确定”**。  
  
3.  通过按**“Ctrl\+Shift\+B”**生成项目，这样，导入的活动将出现在工具箱中。  
  
4.  在**解决方案资源管理器**中，打开 Service1.xamlx。该工作流服务将出现在设计器中。  
  
5.  选择**“Sequence”**活动。在“属性”窗口中，单击**“ImplementedContract”**属性中的**“...”**按钮。在显示的**“类型集合编辑器”**窗口中，单击**“类型”**下拉列表，然后选择**“浏览类型...”** 条目。在**“浏览并选择 .Net 类型”**对话框中的**“\<当前项目\>”**下面，打开所有子节点，然后选择**“IBookService”**。单击**“确定”**。在**“类型集合编辑器”**对话框中，单击**“确定”**。  
  
6.  选择并删除**“ReceiveRequest”**和**“SendResponse”**活动。  
  
7.  将**“Buy\_ReceiveAndSendReply”**和**“Checkout\_Receive”**活动从工具箱拖动到**“Sequential Service”**活动上。