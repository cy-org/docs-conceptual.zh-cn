---
title: "如何：创建自定义活动模板 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 6760a5cc-6eb8-465f-b4fa-f89b39539429
caps.latest.revision: 4
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 4
---
# 如何：创建自定义活动模板
可使用自定义活动模板来自定义活动（包括自定义复合活动）的配置，使用户无需单独创建每个活动并手动配置其属性和其他设置。可在 [!INCLUDE[wfd1](../../../includes/wfd1-md.md)] 的**“工具箱”**中或从重新承载的设计器访问这些自定义模板，用户可将自定义模板从工具箱或该设计器中拖到预配置的设计图面上。[!INCLUDE[wfd2](../../../includes/wfd2-md.md)] 附带此类模板的好例子：[消息传递活动设计器](../Topic/Messaging%20Activity%20Designers.md) 类别中的 [SendAndReceiveReply 模板设计器](../Topic/SendAndReceiveReply%20Template%20Designer.md) 和  [ReceiveAndSendReply 模板设计器](../Topic/ReceiveAndSendReply%20Template%20Designer.md)。  
  
 本主题中的第一个过程描述如何为 **Delay** 活动创建一个自定义活动模板，而第二个过程则简要描述如何使该活动可供在 [!INCLUDE[wfd2](../../../includes/wfd2-md.md)] 中用来验证此自定义模板是否正常工作。  
  
 自定义活动模板必须实现 <xref:System.Activities.Presentation.IActivityTemplateFactory>。此接口具有一个 <xref:System.Activities.Presentation.IActivityTemplateFactory.Create%2A> 方法，可利用此方法创建和配置模板中使用的活动实例。  
  
### 为 Delay 活动创建模板  
  
1.  启动 [!INCLUDE[vs2010](../../../includes/vs2010-md.md)]。  
  
2.  在**“文件”**菜单上，指向**“新建”**，然后选择**“项目”**。  
  
     此时将打开**“新建项目”**对话框。  
  
3.  在**“项目类型”**窗格中，根据您的首选语言从**“Visual C\#”**项目或**“Visual Basic”**组选择**“工作流”**。  
  
4.  在**“模板”**窗格中选择**“活动库”**。  
  
5.  在**“名称”**框中，输入 `DelayActivityTemplate`。  
  
6.  接受**“位置”**和**“解决方案名称”**文本框中的默认值，然后单击**“确定”**。  
  
7.  在**“解决方案资源管理器”**中，右击 DelayActivityTemplate 项目的“引用”目录，并选择**“添加引用”**以打开**“添加引用”**对话框。  
  
8.  转到**“.NET”**选项卡，从左侧的**“组件名称”**列中选择**“PresentationFramework”**，然后单击**“确定”**添加对 PresentationFramework.dll 文件的引用。  
  
9. 重复此过程以添加对 System.Activities.Presentation.dll 文件和 WindowsBase.dll 文件的引用。  
  
10. 在**“解决方案资源管理器”**中，右击 DelayActivityTemplate 项目，然后依次选择**“添加”**和**“新建项”**以打开**“添加新项”**对话框。  
  
11. 选择**“类”**模板，将其命名为 MyDelayTemplate，然后单击**“确定”**。  
  
12. 打开 MyDelayTemplate.cs 文件并添加下面的语句。  
  
    ```  
  
    //Namespaces added  
    using System.Activities;  
    using System.Activities.Statements;  
    using System.Activities.Presentation;  
    using System.Windows;  
  
    ```  
  
13. 使用带有以下代码的 `MyDelayActivity` 类来实现 <xref:System.Activities.Presentation.IActivityTemplateFactory>。这会将延迟时间配置为 10 秒。  
  
    ```  
  
    public sealed class MyDelayActivity : IActivityTemplateFactory  
    {  
        public Activity Create(System.Windows.DependencyObject target)  
        {  
            return new System.Activities.Statements.Delay  
            {  
                DisplayName = "DelayActivityTemplate",  
                Duration = new TimeSpan(0, 0, 10)  
  
            };  
        }  
    }  
  
    ```  
  
14. 从**“生成”**菜单中选择**“生成解决方案”**以生成 DelayActivityTemplate.dll 文件。  
  
### 使模板在工作流设计器中可用  
  
1.  在**“解决方案资源管理器”**中，右击 DelayActivityTemplate 解决方案，然后依次选择**“添加”**和**“新建项目”**以打开**“添加新项目”**对话框。  
  
2.  选择**“工作流控制台应用程序”**模板，将其命名为 `CustomActivityTemplateApp`，然后单击**“确定”**。  
  
3.  在**“解决方案资源管理器”**中，右击 CustomActivityTemplateApp 项目的“引用”目录，然后选择**“添加引用”**以打开**“添加引用”**对话框。  
  
4.  转到**“项目”**选项卡，从左侧的**“项目名称”**列中选择**“DelayActivityTemplate”**，然后单击**“确定”**以添加对第一个过程中创建的 DelayActivityTemplate.dll 文件的引用。  
  
5.  在**“解决方案资源管理器”**中，右击 CustomActivityTemplateApp 项目，然后选择**“生成”**以编译应用程序。  
  
6.  在**“解决方案资源管理器”**中，右击 CustomActivityTemplateApp 项目，然后选择**“设为启动项目”**。  
  
7.  从**“调试”**菜单中选择**“开始执行\(不调试\)”**，然后在 cmd.exe 窗口中提供提示时按任意键以继续。  
  
8.  打开 Workflow1.xaml 文件，再打开**“工具箱”**。  
  
9. 在**“DelayActivityTemplate”**类别中找到**“MyDelayActivity”**模板。将此模板拖动到设计图面上。在**“属性”**窗口中确认已将 `Duration` 属性设置为 10 秒。  
  
## 示例  
 MyDelayActivity.cs 文件应包含以下代码。  
  
```  
  
using System;  
using System.Collections.Generic;  
using System.Linq;  
using System.Text;  
  
//Namespaces added  
using System.Activities;  
using System.Activities.Statements;  
using System.Activities.Presentation;  
using System.Windows;  
  
namespace DelayActivityTemplate  
{  
    public sealed class MyDelayActivity : IActivityTemplateFactory  
    {  
        public Activity Create(System.Windows.DependencyObject target)  
        {  
            return new System.Activities.Statements.Delay  
            {  
                DisplayName = "DelayActivityTemplate",  
                Duration = new TimeSpan(0, 0, 10)  
  
            };  
        }  
    }  
}  
  
```  
  
## 请参阅  
 <xref:System.Activities.Presentation.IActivityTemplateFactory>   
 [自定义工作流设计体验](../../../docs/framework/windows-workflow-foundation//customizing-the-workflow-design-experience.md)