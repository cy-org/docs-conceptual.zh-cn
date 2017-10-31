---
title: "重新承载设计器 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: b676ad31-5f64-4d84-9a36-b4d7113a2f4d
caps.latest.revision: 9
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 9
---
# 重新承载设计器
设计器重新承载是一个常用方案，它是指在自定义应用程序内部承载工作流设计画布。Visual Studio 是大多数人所熟知的承载应用程序，然而在很多方案中，应用程序中的工作流设计器可能会很有用：  
  
-   监视应用程序（允许最终用户直观地查看进程以及有关进程的运行时数据，例如，当前活动状态、聚合执行时间数据或其他关于工作流实例的信息）。  
  
-   允许用户使用有限的活动集合自定义进程的应用程序。  
  
 为了支持这些类型的应用程序，.NET Framework 内附带了工作流设计器，它可以在 WPF 应用程序内或在具有适当的 WPF 承载编码的 WinForms 应用程序内承载。此示例演示：  
  
-   重新承载 WF 设计器。  
  
-   使用重新承载的工具箱和属性网格。  
  
## 重新承载设计器  
 此示例演示如何创建 WPF 布局以包含在以下网格布局中可见的设计器（因空间有限，省略工具箱编码）。需注意包含设计器和属性网格的边框的命名。  
  
```xaml  
<Grid>  
    <Grid.ColumnDefinitions>  
        <ColumnDefinition Width="2*"/>  
        <ColumnDefinition Width="7*"/>  
        <ColumnDefinition Width="3*"/>  
    </Grid.ColumnDefinitions>  
    <Border Grid.Column="0">  
        <sapt:ToolboxControl>...</sapt:ToolboxControl>  
    </Border>  
    <Border Grid.Column="1" Name="DesignerBorder"/>  
    <Border Grid.Column="2" Name="PropertyBorder"/>  
</Grid>  
  
```  
  
 接下来，此示例创建设计器，并将其主 <xref:System.Activities.Presentation.WorkflowDesigner.View%2A> 和 <xref:System.Activities.Presentation.WorkflowDesigner.PropertyInspectorView%2A> 与用户界面中适当的容器相关联。以下示例中有几行额外的代码需要解释一下。需要调用 <xref:System.Activities.Core.Presentation.DesignerMetadata.Register%2A> 来为 [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)] 附带的活动关联默认的活动设计器。调用 <xref:System.Activities.Presentation.WorkflowDesigner.Load%2A>，以在要编辑的 WF 项中进行传递。最后，将 <xref:System.Activities.Presentation.WorkflowDesigner.View%2A>（主画布）和 <xref:System.Activities.Presentation.WorkflowDesigner.PropertyInspectorView%2A>（属性网格）放置在用户界面的图面上。  
  
```csharp  
protected override void OnInitialized(EventArgs e)  
{  
   base.OnInitialized(e);  
   // register metadata  
   (new DesignerMetadata()).Register();  
  
   // create the workflow designer  
   WorkflowDesigner wd = new WorkflowDesigner();  
   wd.Load(new Sequence());  
   DesignerBorder.Child = wd.View;  
   PropertyBorder.Child = wd.PropertyInspectorView;  
}  
  
```  
  
## 使用重新承载的工具栏  
 此示例在 XAML 中以声明方式使用重新承载的工具箱控件。请注意，在代码中可以将一个类型传递给 <xref:System.Activities.Presentation.Toolbox.ToolboxItemWrapper> 构造函数。  
  
```xaml  
<!-- Copyright (c) Microsoft Corporation. All rights reserved-->  
<Window x:Class="Microsoft.Samples.DesignerRehosting.RehostingWfDesigner"  
        xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"  
        xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"  
        xmlns:sapt="clr-namespace:System.Activities.Presentation.Toolbox;assembly=System.Activities.Presentation"  
        xmlns:sys="clr-namespace:System;assembly=mscorlib"  
        Title="Window1" Height="600" Width="900">  
    <Window.Resources>  
        <sys:String x:Key="AssemblyName">System.Activities, Version=4.0.0.0, Culture=neutral, PublicKeyToken=31bf3856ad364e35</sys:String>  
    </Window.Resources>  
    <Grid>  
        <Grid.ColumnDefinitions>  
            <ColumnDefinition Width="2*"/>  
            <ColumnDefinition Width="7*"/>  
            <ColumnDefinition Width="3*"/>  
        </Grid.ColumnDefinitions>  
        <Border Grid.Column="0">  
            <sapt:ToolboxControl>  
                <sapt:ToolboxCategory CategoryName="Basic">  
                    <sapt:ToolboxItemWrapper AssemblyName="{StaticResource AssemblyName}" >  
                        <sapt:ToolboxItemWrapper.ToolName>  
                            System.Activities.Statements.Sequence  
                        </sapt:ToolboxItemWrapper.ToolName>  
                       </sapt:ToolboxItemWrapper>  
                    <sapt:ToolboxItemWrapper  AssemblyName="{StaticResource AssemblyName}">  
                        <sapt:ToolboxItemWrapper.ToolName>  
                            System.Activities.Statements.WriteLine  
                        </sapt:ToolboxItemWrapper.ToolName>  
  
                    </sapt:ToolboxItemWrapper>  
                    <sapt:ToolboxItemWrapper  AssemblyName="{StaticResource AssemblyName}">  
                        <sapt:ToolboxItemWrapper.ToolName>  
                            System.Activities.Statements.If  
                        </sapt:ToolboxItemWrapper.ToolName>  
  
                    </sapt:ToolboxItemWrapper>  
                    <sapt:ToolboxItemWrapper  AssemblyName="{StaticResource AssemblyName}">  
                        <sapt:ToolboxItemWrapper.ToolName>  
                            System.Activities.Statements.While  
                        </sapt:ToolboxItemWrapper.ToolName>  
  
                    </sapt:ToolboxItemWrapper>  
                </sapt:ToolboxCategory>  
            </sapt:ToolboxControl>  
        </Border>  
        <Border Grid.Column="1" Name="DesignerBorder"/>  
        <Border Grid.Column="2" Name="PropertyBorder"/>  
    </Grid>  
</Window>  
  
```  
  
#### 使用示例  
  
1.  在 [!INCLUDE[vs2010](../../../../includes/vs2010-md.md)] 中打开 DesignerRehosting.sln 解决方案。  
  
2.  按 F5 编译并运行应用程序。  
  
3.  一个 WPF 应用程序启动并显示一个重新承载的设计器。  
  
> [!IMPORTANT]
>  您的计算机上可能已安装这些示例。在继续操作之前，请先检查以下（默认）目录：  
>   
>  `<安装驱动器>:\WF_WCF_Samples`  
>   
>  如果此目录不存在，请访问[针对 .NET Framework 4 的 Windows Communication Foundation \(WCF\) 和 Windows Workflow Foundation \(WF\) 示例](http://go.microsoft.com/fwlink/?LinkId=150780)（可能为英文网页），下载所有 [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 和 [!INCLUDE[wf1](../../../../includes/wf1-md.md)] 示例。此示例位于以下目录：  
>   
>  `<安装驱动器>:\WF_WCF_Samples\WCF\Basic\DesignerRehosting\Basic`  
  
## 请参阅