---
title: "定义类 (Visual Basic 中) |Microsoft 文档"
ms.custom: 
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
dev_langs:
- VB
helpviewer_keywords:
- execution, ending
- objects [Visual Basic], initializing
- Initialize event
- files, closing
- programs, quitting
- code, exiting
- objects [Visual Basic], creating
- program termination
- classes [Visual Basic], walkthroughs
- class modules, walkthroughs
- Terminate event
- execution, stopping
ms.assetid: 07018828-2d49-4cf5-a44b-19fb15d9efea
caps.latest.revision: 21
author: dotnet-bot
ms.author: dotnetcontent
translation.priority.ht:
- cs-cz
- de-de
- es-es
- fr-fr
- it-it
- ja-jp
- ko-kr
- pl-pl
- pt-br
- ru-ru
- tr-tr
- zh-cn
- zh-tw
translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: aeaa5c2bb85c1a642da15c6a29546cf065380e27
ms.lasthandoff: 03/13/2017

---
# <a name="walkthrough-defining-classes-visual-basic"></a>演练：定义类 (Visual Basic)
本演练演示如何定义类，您可以使用它来创建对象。 它还演示如何将属性和方法添加到新类，并演示如何初始化对象。  
  
[!INCLUDE[note_settings_general](../../../../csharp/language-reference/compiler-messages/includes/note_settings_general_md.md)]  
  
### <a name="to-define-a-class"></a>若要定义一个类  
  
1.  通过单击创建项目**新项目**上**文件**菜单。 此时将出现 **“新建项目”** 对话框。  
  
2.  从列表中选择 Windows 应用程序[!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]项目模板来显示新项目。  
  
3.  将新类添加到项目中，通过单击**添加类**上**项目**菜单。 **添加新项**对话框随即出现。  
  
4.  选择**类**模板。  
  
5.  将新类命名`UserNameInfo.vb`，然后单击**添加**以显示新类的代码。  
  
     [!code-vb[VbVbalrOOP #&5;](../../../../visual-basic/misc/codesnippet/VisualBasic/walkthrough-defining-classes_1.vb)]  
  
    > [!NOTE]
    >  您可以使用[!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]**代码编辑器**将类添加到启动窗体中，通过键入`Class`关键字后跟新类的名称。 **代码编辑器**会提供相应`End Class`为您的语句。  
  
6.  通过添加下面的代码之间定义的类的私有字段`Class`和`End Class`语句︰  
  
     [!code-vb[VbVbalrOOP #&7;](../../../../visual-basic/misc/codesnippet/VisualBasic/walkthrough-defining-classes_2.vb)]  
  
     声明该字段作为`Private`意味着它可以仅在类中使用。 您可以使字段成为可从类外部的通过使用访问修饰符，如`Public`提供更多的权限。 有关详细信息，请参阅[Visual Basic 中的访问级别](../../../../visual-basic/programming-guide/language-features/declared-elements/access-levels.md)。  
  
7.  通过添加下面的代码定义用于类的属性︰  
  
     [!code-vb[VbVbalrOOP #&8;](../../../../visual-basic/misc/codesnippet/VisualBasic/walkthrough-defining-classes_3.vb)]  
  
8.  通过添加下面的代码定义为类的方法︰  
  
     [!code-vb[VbVbalrOOP #&9;](../../../../visual-basic/misc/codesnippet/VisualBasic/walkthrough-defining-classes_4.vb)]  
  
9. 通过添加一个名为过程定义参数化构造函数为新类`Sub New`:  
  
     [!code-vb[VbVbalrOOP #&10;](../../../../visual-basic/misc/codesnippet/VisualBasic/walkthrough-defining-classes_5.vb)]  
  
     `Sub New`创建基于此类对象时自动调用构造函数。 此构造函数设置保存的用户名称的字段的值。  
  
### <a name="to-create-a-button-to-test-the-class"></a>若要创建一个按钮以测试类  
  
1.  通过右键单击在其名称更改为设计模式的启动窗体**解决方案资源管理器**，然后单击**视图设计器**。 默认情况下，Windows 应用程序项目的启动窗体是名为 form1.vb。 然后，主窗体将出现。  
  
2.  向主窗体添加一个按钮并双击它以显示的代码`Button1_Click`事件处理程序。 添加以下代码以调用测试过程︰  
  
     [!code-vb[VbVbalrOOP #&12;](../../../../visual-basic/misc/codesnippet/VisualBasic/walkthrough-defining-classes_6.vb)]  
  
### <a name="to-run-your-application"></a>运行应用程序  
  
1.  通过按 F5 运行应用程序。 单击要调用测试过程的窗体上的按钮。 它将显示一条消息表明原始`UserName`是"MOORE，BOBBY"，因为该过程调用`Capitalize`对象的方法。  
  
2.  单击**确定**关闭消息框。 `Button1 Click`过程将更改的值`UserName`属性，并显示的新值的一条消息表明`UserName`是"Worden，Joe"。  
  
## <a name="see-also"></a>另请参阅  
 [面向对象的编程](http://msdn.microsoft.com/library/1cf6e655-3f30-45f1-9a5d-4a88ca24a1c2)   
 [对象和类](../../../../visual-basic/programming-guide/language-features/objects-and-classes/index.md)

