---
title: "如何：定义工具栏按钮的图标 | Microsoft Docs"
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
  - "按钮 [Windows 窗体], 图标"
  - "示例 [Windows 窗体], 工具栏"
  - "图标 [Windows 窗体], 工具栏按钮"
  - "图像 [Windows 窗体], 工具栏按钮"
  - "ToolBar 控件 [Windows 窗体], 向按钮添加图标"
  - "工具栏 [Windows 窗体], 向按钮添加图标"
ms.assetid: 84db98b4-8566-49ce-b2c8-1fd66a5eb3a0
caps.latest.revision: 14
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 14
---
# 如何：定义工具栏按钮的图标
> [!NOTE]
>  <xref:System.Windows.Forms.ToolStrip> 控件取代了 <xref:System.Windows.Forms.ToolBar> 控件并添加了功能；但是，可以选择保留 <xref:System.Windows.Forms.ToolBar> 控件以实现向后兼容并供将来使用。  
  
 <xref:System.Windows.Forms.ToolBar> 按钮能自身中显示图标，以便用户识别。  具体的实现方法是，向 [ImageList 组件](../../../../docs/framework/winforms/controls/imagelist-component-windows-forms.md) 组件添加图像，然后将 <xref:System.Windows.Forms.ImageList> 组件与 <xref:System.Windows.Forms.ToolBar> 控件关联起来。  
  
### 以编程方式设置工具栏按钮的图标  
  
1.  在过程中，实例化 <xref:System.Windows.Forms.ImageList> 组件和 <xref:System.Windows.Forms.ToolBar> 控件。  
  
2.  在同一过程中，向 <xref:System.Windows.Forms.ImageList> 组件分配一个图像。  
  
3.  在同一过程中，向 <xref:System.Windows.Forms.ToolBar> 控件分配 <xref:System.Windows.Forms.ImageList> 控件，然后分配各个工具栏按钮的 <xref:System.Windows.Forms.ToolBarButton.ImageIndex%2A> 属性。  
  
     在下面的代码示例中，图标位置的路径设置是**“My Documents”**文件夹。  这样做是因为可假定大多数运行 Windows 操作系统的计算机都包含此目录。  这还将允许具有最低系统访问级别的用户安全地运行应用程序。  下面的示例假定一个已添加了 <xref:System.Windows.Forms.PictureBox> 控件的窗体。  
  
     按照上述步骤，您应该已经编写出类似于下面显示的代码。  
  
    ```vb  
    Public Sub InitializeMyToolBar()  
    ' Instantiate an ImageList component and a ToolBar control.  
       Dim ToolBar1 as New ToolBar  
       Dim ImageList1 as New ImageList  
    ' Assign an image to the ImageList component.  
    ' You should replace the bold image  
    ' in the sample below with an icon of your own choosing.  
       Dim myImage As System.Drawing.Image = _   
          Image.FromFile Image.FromFile _  
          (System.Environment.GetFolderPath _  
          (System.Environment.SpecialFolder.Personal) _  
          & "\Image.gif")  
       ImageList1.Images.Add(myImage)  
    ' Create a ToolBarButton.  
       Dim ToolBarButton1 As New ToolBarButton()  
    ' Add the ToolBarButton to the ToolBar.  
       ToolBar1.Buttons.Add(toolBarButton1)  
    ' Assign an ImageList to the ToolBar.  
       ToolBar1.ImageList = ImageList1  
    ' Assign the ImageIndex property of the ToolBarButton.  
       ToolBarButton1.ImageIndex = 0  
    End Sub  
  
    ```  
  
    ```csharp  
    public void InitializeMyToolBar()  
    {  
       // Instantiate an ImageList component and a ToolBar control.  
       ToolBar toolBar1 = new  ToolBar();   
       ImageList imageList1 = new ImageList();  
       // Assign an image to the ImageList component.  
       // You should replace the bold image   
       // in the sample below with an icon of your own choosing.  
       // Note the escape character used (@) when specifying the path.  
       Image myImage = Image.FromFile  
       (System.Environment.GetFolderPath  
       (System.Environment.SpecialFolder.Personal)  
       + @"\Image.gif");  
       imageList1.Images.Add(myImage);  
       // Create a ToolBarButton.  
       ToolBarButton toolBarButton1 = new ToolBarButton();  
       // Add the ToolBarButton to the ToolBar.  
       toolBar1.Buttons.Add(toolBarButton1);  
       // Assign an ImageList to the ToolBar.  
       toolBar1.ImageList = imageList1;  
       // Assign ImageIndex property of the ToolBarButton.  
       toolBarButton1.ImageIndex = 0;  
    }  
  
    ```  
  
    ```cpp  
    public:  
       void InitializeMyToolBar()  
       {  
          // Instantiate an ImageList component and a ToolBar control.  
          ToolBar ^ toolBar1 = gcnew  ToolBar();   
          ImageList ^ imageList1 = gcnew ImageList();  
          // Assign an image to the ImageList component.  
          // You should replace the bold image   
          // in the sample below with an icon of your own choosing.  
          Image ^ myImage = Image::FromFile(String::Concat  
             (System::Environment::GetFolderPath  
             (System::Environment::SpecialFolder::Personal),  
             "\\Image.gif"));  
          imageList1->Images->Add(myImage);  
          // Create a ToolBarButton.  
          ToolBarButton ^ toolBarButton1 = gcnew ToolBarButton();  
          // Add the ToolBarButton to the ToolBar.  
          toolBar1->Buttons->Add(toolBarButton1);  
          // Assign an ImageList to the ToolBar.  
          toolBar1->ImageList = imageList1;  
          // Assign ImageIndex property of the ToolBarButton.  
          toolBarButton1->ImageIndex = 0;  
       }  
    ```  
  
## 请参阅  
 <xref:System.Windows.Forms.ToolBar>   
 [如何：触发工具栏按钮的菜单事件](../../../../docs/framework/winforms/controls/how-to-trigger-menu-events-for-toolbar-buttons.md)   
 [ToolBar 控件](../../../../docs/framework/winforms/controls/toolbar-control-windows-forms.md)   
 [ImageList 组件](../../../../docs/framework/winforms/controls/imagelist-component-windows-forms.md)