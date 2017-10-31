---
title: "如何：使用“继承选择器”对话框继承窗体 | Microsoft Docs"
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
  - "继承，窗体"
  - "“继承选择器”对话框"
  - "继承的窗体，创建"
ms.assetid: 969b4c04-12aa-4297-93a2-0ae747447823
caps.latest.revision: 11
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 11
---
# 如何：使用“继承选择器”对话框继承窗体
继承窗体或其他对象最简单的方法是使用“继承选择器”对话框。  通过该对话框，可以充分利用在其他解决方案中创建的代码或用户界面 \(UI\)。  
  
> [!NOTE]
>  若要使用“继承选择器”对话框继承窗体，必须先将包含该窗体的项目生成到可执行文件或 DLL 中。  若要生成项目，请从“生成”菜单选择“生成解决方案”。  
>   
>  显示的对话框和菜单命令可能会与“帮助”中的描述不同，具体取决于你现用的设置或版本。  若要更改设置，请在**“工具”**菜单上选择**“导入和导出设置”**。  有关详细信息，请参阅 [Customizing Development Settings in Visual Studio](http://msdn.microsoft.com/zh-cn/22c4debb-4e31-47a8-8f19-16f328d7dcd3)。  
  
### 通过使用继承选择器创建继承自现有窗体的 Windows 窗体  
  
1.  从**“项目”**菜单中，选择**“添加 Windows 窗体”**。  
  
     此时将打开“添加新项”对话框。  
  
2.  选择“继承的窗体”模板，并在“名称”框中命名。  单击“添加”按钮继续。  
  
     此时将打开“继承选择器”。  如果当前项目已经包含窗体，则它们将显示在“继承选择器”对话框中。  
  
3.  若要继承另一个程序集中的窗体，请单击“浏览” 按钮。  
  
4.  在“选择包含要继承组件的文件”对话框中，导航到包含所需窗体或模块的项目。  
  
5.  单击 .exe 或 .dll 文件的名称以选中，然后单击“打开”按钮。  
  
     此操作将返回到“继承选择器”对话框，对话框中现在列出了组件及组件所在的项目。  
  
6.  选择组件。  
  
     在“解决方案资源管理器”中，将组件添加到项目。  如果组件具有 UI，将用标志符号 \(![VisualBasicInheritanceSymbol 屏幕快照](../../../../docs/framework/winforms/advanced/media/vbinheritanceglyph.png "vbInheritanceGlyph")\) 标记属于继承窗体一部分的控件，并且选中组件后，超类窗体上将出现一个指示该控件具有的安全级别的边框。  下表中列出了与不同安全级别相对应的行为。  
  
    |控件的安全级别|可以通过设计器和代码编辑器与继承的窗体进行的交互|  
    |-------------|------------------------------|  
    |Public|带有大小调整控点的标准边框：可以调整控件大小和移动控件。  控件可以由声明它的类进行内部访问，也可由其他类进行外部访问。|  
    |Protected|带有大小调整控点的标准边框：可以调整控件大小和移动控件。  可以由声明它的类和任何继承自父类的类进行内部访问，但不能由外部类进行访问。|  
    |Protected Internal（Visual Basic 中为 Protected Friend）|带有大小调整控点的标准边框：可以调整控件大小和移动控件。  可以由声明它的类、任何继承自父类的类以及包含它的程序集的其他成员进行内部访问。|  
    |Internal（Visual Basic 中为 Friend）|窗体上将显示不带有调整大小控点的标准边框，属性在“属性”窗口中可见。  但是，该控件的所有方面都将考虑为只读。  无法对控件进行移动、调整大小或更改其属性。  如果控件是其他控件的容器（例如分组框），则无法添加新控件，也无法移除现有控件，即使那些控件是 public 控件。  此控件只能由包含它的程序集的其他成员进行访问。|  
    |Private|窗体上将显示不带有调整大小控点的标准边框，属性在“属性”窗口中可见。  但是，该控件的所有方面都将考虑为只读。  无法对控件进行移动、调整大小或更改其属性。  如果控件是其他控件的容器（例如分组框），则无法添加新控件，也无法移除现有控件，即使那些控件是 public 控件。  此控件只能由声明它的类进行访问。|  
  
     有关如何更改基窗体外观的详细信息，请参阅[修改基窗体外观的效果](../../../../docs/framework/winforms/advanced/effects-of-modifying-base-form-appearance.md)。  
  
    > [!NOTE]
    >  将继承的控件和组件与 Windows 窗体上的标准控件和组件组合到一起时，可能会与 Z 排序发生冲突。  可以通过修改 Z 排序纠正冲突，做法是单击“格式”菜单，指向“排序”，然后单击“置于顶层”或“置于底层”。  有关对控件进行 Z 排序的详细信息，请参阅[如何：对 Windows 窗体上的对象分层](../../../../docs/framework/winforms/controls/how-to-layer-objects-on-windows-forms.md)。  
  
## 请参阅  
 [Inherits 语句](../../../../ocs/visual-basic/language-reference/statements/inherits-statement.md)   
 [using](../Topic/using%20\(C%23%20Reference\).md)   
 [修改基窗体的外观的效果](../../../../docs/framework/winforms/advanced/effects-of-modifying-base-form-appearance.md)   
 [Windows 窗体可视化继承](../../../../docs/framework/winforms/advanced/windows-forms-visual-inheritance.md)