---
title: "如何：以编程方式编写服务 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "服务, 创建"
  - "Windows 服务应用程序, 创建"
ms.assetid: 3abbb2ec-78d2-41e6-b9f9-6662d4e2cdc7
caps.latest.revision: 21
author: "ghogen"
ms.author: "ghogen"
manager: "douge"
caps.handback.revision: 21
---
# 如何：以编程方式编写服务
如果选择不使用 Windows 服务项目模板，可以通过自行设置继承和其他基础结构元素来编写自己的服务。  当以编程方式创建服务时，必须执行模板原本可以会为您处理的几个步骤：  
  
-   必须将服务类设置为从 <xref:System.ServiceProcess.ServiceBase> 类继承。  
  
-   必须为服务项目创建一个 `Main` 方法，定义要运行的服务并对这些服务调用 <xref:System.ServiceProcess.ServiceBase.Run%2A> 方法。  
  
-   必须重写 <xref:System.ServiceProcess.ServiceBase.OnStart%2A> 和 <xref:System.ServiceProcess.ServiceBase.OnStop%2A> 过程，并填写希望它们运行的任何代码。  
  
### 以编程方式编写服务  
  
1.  创建一个空项目，然后按下列这些步骤创建到所需命名空间的引用：  
  
    1.  在**“解决方案资源管理器”**中右击**“引用”**节点，再单击**“添加引用”**。  
  
    2.  在**“.NET Framework”**选项卡中，滚动到**“System.dll”**并单击**“选择”**。  
  
    3.  滚动到**“System.ServiceProcess.dll”**并单击**“选择”**。  
  
    4.  单击“确定”。  
  
2.  添加一个类并将其配置为从 <xref:System.ServiceProcess.ServiceBase> 继承：  
  
     [!code-csharp[VbRadconService#7](../../../samples/snippets/csharp/VS_Snippets_VBCSharp/VbRadconService/CS/MyNewService.cs#7)]
     [!code-vb[VbRadconService#7](../../../samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbRadconService/VB/MyNewService.vb#7)]  
  
3.  添加下列代码来配置服务类：  
  
     [!code-csharp[VbRadconService#8](../../../samples/snippets/csharp/VS_Snippets_VBCSharp/VbRadconService/CS/MyNewService.cs#8)]
     [!code-vb[VbRadconService#8](../../../samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbRadconService/VB/MyNewService.vb#8)]  
  
4.  为类创建 `Main` 方法，并使用它来定义类将包含的服务；`userService1` 是类的名称：  
  
     [!code-csharp[VbRadconService#9](../../../samples/snippets/csharp/VS_Snippets_VBCSharp/VbRadconService/CS/MyNewService.cs#9)]
     [!code-vb[VbRadconService#9](../../../samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbRadconService/VB/MyNewService.vb#9)]  
  
5.  重写 <xref:System.ServiceProcess.ServiceBase.OnStart%2A> 方法，并定义希望在服务启动时发生的任何处理。  
  
     [!code-csharp[VbRadconService#10](../../../samples/snippets/csharp/VS_Snippets_VBCSharp/VbRadconService/CS/MyNewService.cs#10)]
     [!code-vb[VbRadconService#10](../../../samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbRadconService/VB/MyNewService.vb#10)]  
  
6.  重写要为其定义自定义处理的其他任何方法，并编写代码以确定服务在各种情况中应采取的操作。  
  
7.  添加服务应用程序所必需的安装程序。  有关详细信息，请参阅 [如何：将安装程序添加到服务应用程序](../../../docs/framework/windows-services/how-to-add-installers-to-your-service-application.md)。  
  
8.  通过从**“生成”**菜单中选择**“生成解决方案”**来生成项目。  
  
    > [!NOTE]
    >  不要通过按 F5 来运行项目，不能以这种方式运行服务项目。  
  
9. 创建一个安装项目和自定义操作来安装服务。  有关示例，请参见[演练：在组件设计器中创建 Windows 服务应用程序](../../../docs/framework/windows-services/walkthrough-creating-a-windows-service-application-in-the-component-designer.md)。  
  
10. 安装服务。  有关详细信息，请参阅 [如何：安装和卸载服务](../../../docs/framework/windows-services/how-to-install-and-uninstall-services.md)。  
  
## 请参阅  
 [Windows 服务应用程序介绍](../../../docs/framework/windows-services/introduction-to-windows-service-applications.md)   
 [如何：创建 Windows 服务](../../../docs/framework/windows-services/how-to-create-windows-services.md)   
 [如何：将安装程序添加到服务应用程序](../../../docs/framework/windows-services/how-to-add-installers-to-your-service-application.md)   
 [如何：记录关于服务的信息](../../../docs/framework/windows-services/how-to-log-information-about-services.md)   
 [演练：在组件设计器中创建 Windows 服务应用程序](../../../docs/framework/windows-services/walkthrough-creating-a-windows-service-application-in-the-component-designer.md)