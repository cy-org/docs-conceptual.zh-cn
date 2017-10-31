---
title: "对服务操作失败进行监视 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 59472ba3-8ebf-4479-bd7b-f440d5e636cb
caps.latest.revision: 6
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 6
---
# 对服务操作失败进行监视
如果为应用程序启用了分析跟踪，则可以在事件查看器中轻松地监视服务失败。本主题演示如何确定服务操作失败的时间，以及如何确定失败的原因。  
  
### 确定服务操作失败信息  
  
1.  通过单击**“开始”**、**“运行”**并输入 `eventvwr.exe` 来打开事件查看器。  
  
2.  如果尚未启用分析跟踪，请展开**“应用程序和服务日志”**、**“Microsoft”**、**“Windows”**、**“应用程序服务器”\-\>“应用程序”**。选择**“视图”**、**“显示分析和调试日志”**。右击**“分析”**，然后选择**“启用日志”**。保持事件查看器打开，以便在服务操作失败后可以查看跟踪。  
  
3.  接下来，打开在 [!INCLUDE[vs_current_long](../../../../../includes/vs-current-long-md.md)] 的[入门教程](../../../../../docs/framework/wcf/getting-started-tutorial.md)中创建的示例。请注意，必须以管理员身份运行 [!INCLUDE[vs_current_long](../../../../../includes/vs-current-long-md.md)]，以便可以创建该服务。如果安装了 [!INCLUDE[indigo2](../../../../../includes/indigo2-md.md)] 示例，则可以打开[入门](../../../../../docs/framework/wcf/samples/getting-started-sample.md)，其中包含本教程中创建的完整项目。  
  
4.  在服务器项目的 Program.cs 文件中，将以下代码行添加到 `CalculatorService` 类中 `Divide` 方法的开头：  
  
    ```  
    if (n2 == 0) throw new DivideByZeroException();  
  
    ```  
  
5.  在客户端项目的 Program.cs 文件中，将分配给 value2 的值更改为零：  
  
    ```  
    //Call the Divide service operation  
    value1 = 22.00D;  
    value2 = 0.00D;  
    result = client.Divide(value1, value2);  
    Console.WriteLine("Divide({0}, {1}) = {2}", value1, value2, result);  
  
    ```  
  
6.  通过按**“Ctrl\+F5”**来执行该服务器应用程序而不进行调试。  
  
7.  打开 Visual Studio 命令提示。定位到客户端目录，然后从命令行执行该客户端。  
  
8.  在事件查看器中，禁用并刷新分析日志，然后按事件 ID 对事件排序。查找事件 ID 为 [219 \- ServiceException](../../../../../docs/framework/wcf/diagnostics/etw/219-serviceexception.md)（描述服务失败）的事件。  
  
    ```Output  
    消息处理过程中出现了“System.DivideByZeroException”类型的未经处理的异常。完整异常 ToString: System.DivideByZeroException: 试图除以零。  
    ```  
  
    > [!NOTE]
    >  事件在发送到事件查看器时将被缓冲；可能不会立即显示失败事件。