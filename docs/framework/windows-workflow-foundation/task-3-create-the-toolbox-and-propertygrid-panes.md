---
title: "任务 3：创建工具箱窗格和属性网格窗格 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 72c1546a-eed5-4f0f-a616-719a163414f4
caps.latest.revision: 15
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 15
---
# 任务 3：创建工具箱窗格和属性网格窗格
在此任务中，您将创建**“工具箱”**和**“属性网格”**窗格并将它们添加到重新承载的 [!INCLUDE[wfd1](../../../includes/wfd1-md.md)] 中。  
  
 为了方便参考，在本主题的结尾提供了在完成[重新承载工作流设计器](../../../docs/framework/windows-workflow-foundation//rehosting-the-workflow-designer.md)系列主题中的三个任务后 MainWindow.xaml.cs 文件中应存在的代码。  
  
### 创建工具箱并将其添加到网格中  
  
1.  打开您通过执行[任务 2：承载工作流设计器](../../../docs/framework/windows-workflow-foundation//task-2-host-the-workflow-designer.md)中描述的过程获得的 HostingApplication 项目。  
  
2.  在**“解决方案资源管理器”**窗格中，右击 MainWindow.xaml 文件，然后选择**“查看代码”**。  
  
3.  在 `MainWindow` 类中添加一个 `GetToolboxControl` 方法，该方法创建 <xref:System.Activities.Presentation.Toolbox.ToolboxControl>，将一个新的**“工具箱”**类别添加到**“工具箱”**中，并将 <xref:System.Activities.Statements.Assign> 和 <xref:System.Activities.Statements.Sequence> 活动类型分配给该类别。  
  
    ```csharp  
  
    private ToolboxControl GetToolboxControl()  
    {  
        // Create the ToolBoxControl.  
        ToolboxControl ctrl = new ToolboxControl();  
  
        // Create a category.  
        ToolboxCategory category = new ToolboxCategory("category1");  
  
        // Create Toolbox items.  
        ToolboxItemWrapper tool1 =   
            new ToolboxItemWrapper("System.Activities.Statements.Assign",   
            typeof(Assign).Assembly.FullName, null, "Assign");  
  
        ToolboxItemWrapper tool2 = new ToolboxItemWrapper("System.Activities.Statements.Sequence",   
            typeof(Sequence).Assembly.FullName, null, "Sequence");  
  
        // Add the Toolbox items to the category.  
        category.Add(tool1);  
        category.Add(tool2);  
  
        // Add the category to the ToolBox control.  
        ctrl.Categories.Add(category);  
        return ctrl;  
    }  
  
    ```  
  
4.  在 `MainWindow` 类中添加一个私有的 `AddToolbox` 方法，该方法将**“工具箱”**放置在网格上的左列中。  
  
    ```csharp  
  
    private void AddToolBox()  
    {  
        ToolboxControl tc = GetToolboxControl();  
        Grid.SetColumn(tc, 0);  
        grid1.Children.Add(tc);  
    }  
  
    ```  
  
5.  在 `MainWindow()` 类构造函数中添加对 `AddToolBox` 方法的调用，如以下代码所示。  
  
    ```csharp  
  
    public MainWindow()  
    {  
        InitializeComponent();  
        this.RegisterMetadata();  
        this.AddDesigner();  
  
        this.AddToolBox();  
    }  
  
    ```  
  
6.  按“F5”生成并运行解决方案。应显示包含 <xref:System.Activities.Statements.Assign> 和 <xref:System.Activities.Statements.Sequence> 活动的**“工具箱”**。  
  
### 创建属性网格  
  
1.  在**“解决方案资源管理器”**窗格中，右击 MainWindow.xaml 文件，然后选择**“查看代码”**。  
  
2.  在 `MainWindow` 类中添加 `AddPropertyInspector` 方法以将**属性网格**窗格放置在网格上的最右侧列中。  
  
    ```csharp  
  
    private void AddPropertyInspector()  
    {  
        Grid.SetColumn(wd.PropertyInspectorView, 2);  
        grid1.Children.Add(wd.PropertyInspectorView);              
    }  
  
    ```  
  
3.  在 `MainWindow()` 类构造函数中添加对 `AddPropertyInspector` 方法的调用，如以下代码所示。  
  
    ```csharp  
  
    public MainWindow()  
    {  
        InitializeComponent();  
        this.RegisterMetadata();  
        this.AddDesigner();  
        this.AddToolBox();  
  
        this.AddPropertyInspector();   
    }  
  
    ```  
  
4.  按 F5 生成并运行解决方案。应显示**“工具箱”**、工作流设计画布和**属性网格**窗格，并且将 <xref:System.Activities.Statements.Assign> 活动或 <xref:System.Activities.Statements.Sequence> 活动拖动到设计画布上时，属性网格应根据突出显示的活动进行更新。  
  
## 示例  
 现在，MainWindow.xaml.cs 文件应包含以下代码。  
  
```  
  
using System;  
using System.Collections.Generic;  
using System.Linq;  
using System.Text;  
using System.Windows;  
using System.Windows.Controls;  
using System.Windows.Data;  
using System.Windows.Documents;  
using System.Windows.Input;  
using System.Windows.Media;  
using System.Windows.Media.Imaging;  
using System.Windows.Navigation;  
using System.Windows.Shapes;  
//dlls added  
using System.Activities;  
using System.Activities.Core.Presentation;  
using System.Activities.Presentation;  
using System.Activities.Presentation.Metadata;  
using System.Activities.Presentation.Toolbox;  
using System.Activities.Statements;  
using System.ComponentModel;  
  
namespace HostingApplication  
{  
    /// <summary>  
    /// Interaction logic for MainWindow.xaml  
    /// </summary>  
    public partial class MainWindow : Window  
    {  
        private WorkflowDesigner wd;  
  
        public MainWindow()  
        {  
            InitializeComponent();  
            RegisterMetadata();  
            AddDesigner();  
            this.AddToolBox();  
            this.AddPropertyInspector();  
        }  
  
        private void AddDesigner()  
        {  
            //Create an instance of WorkflowDesigner class.  
            this.wd = new WorkflowDesigner();  
  
            //Place the designer canvas in the middle column of the grid.  
            Grid.SetColumn(this.wd.View, 1);  
  
            //Load a new Sequence as default.  
            this.wd.Load(new Sequence());  
  
            //Add the designer canvas to the grid.  
            grid1.Children.Add(this.wd.View);  
        }  
  
        private void RegisterMetadata()  
        {  
            DesignerMetadata dm = new DesignerMetadata();  
            dm.Register();  
        }  
  
        private ToolboxControl GetToolboxControl()  
        {  
            // Create the ToolBoxControl.  
            ToolboxControl ctrl = new ToolboxControl();  
  
            // Create a category.  
            ToolboxCategory category = new ToolboxCategory("category1");  
  
            // Create Toolbox items.  
            ToolboxItemWrapper tool1 =  
                new ToolboxItemWrapper("System.Activities.Statements.Assign",  
                typeof(Assign).Assembly.FullName, null, "Assign");  
  
            ToolboxItemWrapper tool2 = new ToolboxItemWrapper("System.Activities.Statements.Sequence",  
                typeof(Sequence).Assembly.FullName, null, "Sequence");  
  
            // Add the Toolbox items to the category.  
            category.Add(tool1);  
            category.Add(tool2);  
  
            // Add the category to the ToolBox control.  
            ctrl.Categories.Add(category);  
            return ctrl;  
        }  
  
        private void AddToolBox()  
        {  
            ToolboxControl tc = GetToolboxControl();  
            Grid.SetColumn(tc, 0);  
            grid1.Children.Add(tc);  
        }  
  
        private void AddPropertyInspector()  
        {  
            Grid.SetColumn(wd.PropertyInspectorView, 2);  
            grid1.Children.Add(wd.PropertyInspectorView);  
        }  
  
    }  
}  
  
```  
  
## 请参阅  
 [重新承载工作流设计器](../../../docs/framework/windows-workflow-foundation//rehosting-the-workflow-designer.md)   
 [任务 1：创建一个新的 Windows Presentation Foundation 应用程序](../../../docs/framework/windows-workflow-foundation//task-1-create-a-new-wpf-app.md)   
 [任务 2：承载工作流设计器](../../../docs/framework/windows-workflow-foundation//task-2-host-the-workflow-designer.md)