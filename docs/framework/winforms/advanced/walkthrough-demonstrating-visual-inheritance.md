---
title: "演练：演示可视化继承 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-winforms"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "jsharp"
helpviewer_keywords: 
  - "窗体继承, 演练"
  - "继承, 演练"
  - "可视继承"
  - "演练 [Windows 窗体], 可视继承"
  - "Windows 窗体, 继承"
ms.assetid: 01966086-3142-450e-8210-3fd4cb33f591
caps.latest.revision: 24
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 24
---
# 演练：演示可视化继承
通过 Visual 继承，可以查看基本表单上的控件和添加新控件。  在本演练中，你将创建基窗体，并将其编译到类库。  将此类库导入另一个项目，并创建一个从基窗体继承的新窗体。  在本演练中，你将学会如何执行以下任务：  
  
-   创建包含基窗体的类库项目。  
  
-   添加具有可修改基窗体的派生类的属性的按钮。  
  
-   添加基窗体的继承者无法修改的按钮。  
  
-   创建包含从 `BaseForm` 继承的窗体的项目。  
  
 最后，本演练将显示继承的窗体上私有控件和受保护控件之间的差异。  
  
> [!NOTE]
>  显示的对话框和菜单命令可能会与“帮助”中的描述不同，具体取决于你现用的设置或版本。  若要更改设置，请在**“工具”**菜单上选择**“导入和导出设置”**。  有关详细信息，请参阅 [Customizing Development Settings in Visual Studio](http://msdn.microsoft.com/zh-cn/22c4debb-4e31-47a8-8f19-16f328d7dcd3)。  
  
> [!CAUTION]
>  并非所有控件都支持从基窗体执行 Visual 继承。  以下控件不支持本演练中描述的情景：  
>   
>  <xref:System.Windows.Forms.WebBrowser>  
>   
>  <xref:System.Windows.Forms.ToolStrip>  
>   
>  <xref:System.Windows.Forms.ToolStripPanel>  
>   
>  <xref:System.Windows.Forms.TableLayoutPanel>  
>   
>  <xref:System.Windows.Forms.FlowLayoutPanel>  
>   
>  <xref:System.Windows.Forms.DataGridView>  
>   
>  无论使用何种修饰符（`private``protected` 或 `public`），继承的窗体中的这些控件始终为只读。  
  
## 方案步骤  
 第一步是创建基窗体。  
  
#### 创建包含基窗体的类库项目  
  
1.  从“文件”菜单上，选择“新建”，然后选择“项目”打开“新建项目”对话框。  
  
2.  创建名为 `BaseFormLibrary` 的 Windows 窗体应用程序。  
  
3.  若要创建类库（而非标准 Windows 窗体应用程序），请在“解决方案资源管理器”中右键单击“BaseFormLibrary”项目节点，然后选择“属性”。  
  
4.  在项目属性中，将“输出类型”从“Windows 应用程序”更改为“类库”。  
  
5.  从“文件”菜单上，选择“全部保存”以将项目和文件保存到默认位置。  
  
 接下来的两步是将按钮添加至基窗体。  为了演示 visual 继承，请通过设置按钮的 `Modifiers` 属性为它们指定不同的访问级别。  
  
#### 添加基窗体的继承者可修改的按钮  
  
1.  在设计器中打开**“Form1”**。  
  
2.  在“工具箱”的“所有 Windows 窗体”选项卡上，双击“按钮”以向窗体添加按钮。  使用鼠标来定位按钮和调整其大小。  
  
3.  在“属性”窗口中，设置按钮的下列属性：  
  
    -   将“Text”属性设置为“Say Hello”。  
  
    -   将 \(Name\) 属性设置为“btnProtected”。  
  
    -   将“Modifiers”**“Modifiers”**属性设置为“Protected”。  这使继承自“Form1”的窗体能够修改“btnProtected”属性。  
  
4.  双击“Say Hello”按钮以为“Click”事件添加事件处理程序。  
  
5.  将以下代码行添加到事件处理程序：  
  
    ```vb  
    MessageBox.Show("Hello, World!")  
    ```  
  
    ```csharp  
    MessageBox.Show("Hello, World!");  
    ```  
  
#### 添加基窗体的继承者不能修改的按钮  
  
1.  通过单击代码编辑器上方的“Form1.vb \[Design\], Form1.cs \[Design\], or Form1.jsl \[Design\]”选项卡或按 F7，切换到设计视图。  
  
2.  按如下方式添加第二个按钮并设置其属性：  
  
    -   将“Text”属性设置为“Say Goodbye”。  
  
    -   将 \(Name\) 属性设置为“btnPrivate”。  
  
    -   将“Modifiers”属性设置为“Private”。  这使继承自“Form1”的窗体无法修改“btnPrivate”属性。  
  
3.  双击“Say Goodbye”按钮以便为“Click”事件添加事件处理程序。  将以下代码行放入事件过程：  
  
    ```vb  
    MessageBox.Show("Goodbye!")  
    ```  
  
    ```csharp  
    MessageBox.Show("Goodbye!");  
    ```  
  
4.  从“构建”菜单上，选择“构建 BaseForm 库”来构建类库。  
  
     构建库后，可创建从刚创建的窗体继承的新项目。  
  
#### 创建包含继承自基窗体的窗体的项目  
  
1.  在“文件”菜单上，选择“添加”，然后选择“新建项目”打开“添加新项目”对话框。  
  
2.  创建名为 `InheritanceTest` 的 Windows 窗体应用程序。  
  
#### 添加继承的窗体  
  
1.  在“解决方案资源管理器”中，右键单击“InheritanceTest”项目，然后依次选择“添加”和“新建项”。  
  
2.  在“添加新项”对话框中，选择“Windows 窗体”类别（若有类别列表），然后选择“继承的窗体”模板。  
  
3.  保留“Form2”的默认名称，然后单击“添加”。  
  
4.  在“继承选择器”对话框中，将“BaseFormLibrary”项目的“Form1”选为要从中继承的窗体并单击“确定”。  
  
     此操作将在“InheritanceTest”项目中创建由“BaseFormLibrary”中的窗体派生的窗体。  
  
5.  如果设计器中继承的窗体 \(**Form2**\) 尚未打开，双击将其打开。  
  
     在设计器中，继承的按钮上角有一个符号 \(![VisualBasicInheritanceSymbol 屏幕快照](../../../../docs/framework/winforms/advanced/media/vbinheritanceglyph.png "vbInheritanceGlyph")\)，指示它们是继承的。  
  
6.  选择“Say Hello”按钮，并查案调整大小图柄。  由于此按钮受保护，继承者可以对其进行移动、调整大小、更改标题和进行其他修改。  
  
7.  选择专有的“Say Goodbye”按钮，请注意它不具有调整大小图柄。  此外，在“属性”窗口中，此按钮的属性呈灰显，指示不能修改。  
  
8.  如果使用 [!INCLUDE[csprcs](../../../../includes/csprcs-md.md)]：  
  
    1.  在“解决方案资源管理器”中，右键单击“InheritanceTest”项目中的“Form1”，然后选择“删除”。  在显示的消息框中，单击“确定”以确认删除。  
  
    2.  打开 Program.cs 文件并将 `Application.Run(new Form1());` 行更改为 `Application.Run(new Form2());`。  
  
9. 在“解决方案资源管理器”中，右键单击“InheritanceTest”项目，然后选择“设为启动项目”。  
  
10. 在“解决方案资源管理器”中，右键单击“InheritanceTest”项目，然后选择“属性”。  
  
11. 在“InheritanceTest”属性页中，将“启动对象”设置为继承的窗体 \(**Form2**\)。  
  
12. 按 F5 运行此应用程序，并观察继承的窗体的行为。  
  
## 后续步骤  
 用户控件的继承方式大致相同。  打开新的类库项目并添加用户控件。  在其上放置构成控件，然后编译项目。  打开另一个新的类库项目，并添加对已编译的类库的引用。  另外，尝试将继承的控件（通过“添加新项”对话框）添加至项目并使用“继承选择器”。  添加用户控件，并更改 `Inherits`（[!INCLUDE[csprcs](../../../../includes/csprcs-md.md)] 中的 `:`）语句。  有关详细信息，请参阅[如何：继承 Windows 窗体](../../../../docs/framework/winforms/advanced/how-to-inherit-windows-forms.md)。  
  
## 请参阅  
 [如何：继承 Windows 窗体](../../../../docs/framework/winforms/advanced/how-to-inherit-windows-forms.md)   
 [Windows 窗体可视化继承](../../../../docs/framework/winforms/advanced/windows-forms-visual-inheritance.md)   
 [Windows 窗体](../../../../docs/framework/winforms/index.md)