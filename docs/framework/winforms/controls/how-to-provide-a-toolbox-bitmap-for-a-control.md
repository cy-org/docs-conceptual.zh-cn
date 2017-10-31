---
title: "如何：为控件提供工具箱位图 | Microsoft Docs"
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
  - "位图 [Windows 窗体], 自定义控件"
  - "自定义控件 [Windows 窗体], 工具箱位图"
  - "工具箱 [Windows 窗体], 添加自定义控件的位图"
ms.assetid: 0ed0840a-616d-41ba-a27d-3573241932ad
caps.latest.revision: 20
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 20
---
# 如何：为控件提供工具箱位图
如果希望在**“工具箱”**中为控件显示特殊图标，可以通过使用 <xref:System.Drawing.ToolboxBitmapAttribute> 来指定一个特定的图像。  此类是一种特性，这是一种可以附加到其他类上的特殊类。  有关特性的更多信息，对于 [!INCLUDE[vbprvb](../../../../includes/vbprvb-md.md)] 请参见 [NOT IN BUILD: Attributes Overview in Visual Basic](http://msdn.microsoft.com/zh-cn/0d0cff64-892d-4f57-83bd-bef388553d4f)，对于 [!INCLUDE[csprcs](../../../../includes/csprcs-md.md)] 请参见 [特性](../Topic/Attributes%20\(C%23%20and%20Visual%20Basic\).md)。  
  
 通过使用 <xref:System.Drawing.ToolboxBitmapAttribute>，可以指定一个字符串来指示一个 16 x 16 像素位图的路径和文件名。  此位图在添加到**“工具箱”**后显示在对应的控件旁边。  还可以指定 <xref:System.Type>，在这种情况下会加载与该类型关联的位图。  如果您同时指定 <xref:System.Type> 和字符串，则控件在包含 <xref:System.Type> 参数所指定类型的程序集中，搜索名称由字符串参数指定的图像资源。  
  
### 指定控件的工具箱位图  
  
1.  将 <xref:System.Drawing.ToolboxBitmapAttribute> 添加至控件的类声明中，对于 [!INCLUDE[vbprvb](../../../../includes/vbprvb-md.md)] 应置于 `Class` 关键字之前，对于 [!INCLUDE[csprcs](../../../../includes/csprcs-md.md)] 则应置于类声明之前。  
  
    ```vb  
    ' Specifies the bitmap associated with the Button type.  
    <ToolboxBitmap(GetType(Button))> Class MyControl1  
    ' Specifies a bitmap file.  
    End Class  
    <ToolboxBitmap("C:\Documents and Settings\Joe\MyPics\myImage.bmp")> _  
       Class MyControl2  
    End Class  
    ' Specifies a type that indicates the assembly to search, and the name   
    ' of an image resource to look for.  
    <ToolboxBitmap(GetType(MyControl), "MyControlBitmap")> Class MyControl  
    End Class  
    ```  
  
    ```csharp  
    // Specifies the bitmap associated with the Button type.  
    [ToolboxBitmap(typeof(Button))]  
    class MyControl1 : UserControl  
    {  
    }  
    // Specifies a bitmap file.  
    [ToolboxBitmap(@"C:\Documents and Settings\Joe\MyPics\myImage.bmp")]  
    class MyControl2 : UserControl  
    {  
    }  
    // Specifies a type that indicates the assembly to search, and the name   
    // of an image resource to look for.  
    [ToolboxBitmap(typeof(MyControl), "MyControlBitmap")]  
    class MyControl : UserControl  
    {  
    }  
    ```  
  
2.  重新生成项目。  
  
    > [!NOTE]
    >  对于自动生成的控件和组件，位图将不出现在工具箱中。  若要查看位图，请使用**“选择工具箱项”**对话框重新加载控件。  有关更多信息，请参见[演练：使用自定义组件自动填充工具箱](../../../../docs/framework/winforms/controls/walkthrough-automatically-populating-the-toolbox-with-custom-components.md)。  
  
## 请参阅  
 <xref:System.Drawing.ToolboxBitmapAttribute>   
 [演练：使用自定义组件自动填充工具箱](../../../../docs/framework/winforms/controls/walkthrough-automatically-populating-the-toolbox-with-custom-components.md)   
 [设计时开发 Windows 窗体控件](../../../../docs/framework/winforms/controls/developing-windows-forms-controls-at-design-time.md)   
 [特性](../Topic/Attributes%20\(Visual%20Basic\)1.md)   
 [特性](../Topic/Attributes%20\(C%23%20and%20Visual%20Basic\).md)