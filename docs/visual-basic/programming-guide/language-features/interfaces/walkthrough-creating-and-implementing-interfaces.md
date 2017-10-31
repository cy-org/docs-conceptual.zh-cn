---
title: "创建和实现接口 (Visual Basic 中) |Microsoft 文档"
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
- interfaces, walkthroughs
- interfaces, testing
- interface implementation, walkthrough
- interfaces, creating
ms.assetid: ded82af2-9f52-4232-98ef-fe458180f112
caps.latest.revision: 22
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
ms.openlocfilehash: 076bc8d33e97286c31f27a2016e39a25e9cec22c
ms.lasthandoff: 03/13/2017

---
# <a name="walkthrough-creating-and-implementing-interfaces-visual-basic"></a>演练：创建和实现接口 (Visual Basic)
接口描述特征的属性、 方法和事件，但将留给了结构或类实现的细节。  
  
 本演练演示如何声明和实现接口。  
  
> [!NOTE]
>  本演练并不提供有关如何创建用户界面的信息。  
  
[!INCLUDE[note_settings_general](../../../../csharp/language-reference/compiler-messages/includes/note_settings_general_md.md)]  
  
### <a name="to-define-an-interface"></a>若要定义一个接口  
  
1.  打开一个新[!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]Windows 应用程序项目。  
  
2.  向项目添加一个新模块，通过单击**添加模块**上**项目**菜单。  
  
3.  命名新模块`Module1.vb`，然后单击**添加**。 显示新的模块的代码。  
  
4.  定义一个接口，该接口名为`TestInterface`内`Module1`通过键入`Interface TestInterface`之间`Module`和`End Module`语句，并按 ENTER。 **代码编辑器**缩进`Interface`关键字，并将添加`End Interface`语句来形成一个代码块。  
  
5.  通过将下面的代码之间定义属性、 方法和事件的接口`Interface`和`End Interface`语句︰  
  
     [!code-vb[VbVbalrOOP #&98;](../../../../visual-basic/misc/codesnippet/VisualBasic/walkthrough-creating-and-implementing-interfaces_1.vb)]  
  
## <a name="implementation"></a>实现  
 您可能注意到用来声明接口成员的语法是用来声明类成员声明语法不同。 这一区别反映接口不能包含实现代码的情况。  
  
#### <a name="to-implement-the-interface"></a>若要实现接口  
  
1.  添加一个名为类`ImplementationClass`通过添加下面的语句`Module1`后面`End Interface`语句之前`End Module`语句，并按 ENTER:  
  
     [!code-vb[VbVbalrOOP #&99;](../../../../visual-basic/misc/codesnippet/VisualBasic/walkthrough-creating-and-implementing-interfaces_2.vb)]  
  
     如果您正在在集成的开发环境中，**代码编辑器**提供一条匹配`End Class`语句时按 enter 键。  
  
2.  将以下代码添加`Implements`语句`ImplementationClass`，命名的类接口实现︰  
  
     [!code-vb[VbVbalrOOP #&100;](../../../../visual-basic/misc/codesnippet/VisualBasic/walkthrough-creating-and-implementing-interfaces_3.vb)]  
  
     在顶部的类或结构，其他项分开列出`Implements`语句指示类或结构实现的接口。  
  
     如果您正在在集成的开发环境中，**代码编辑器**实现所需的类成员`TestInterface`时按 enter 键，并且可以跳过下一步。  
  
3.  如果您没有使用使用集成的开发环境中，必须实现该接口的所有成员`MyInterface`。 添加以下代码到`ImplementationClass`实现`Event1`， `Method1`，和`Prop1`:  
  
     [!code-vb[VbVbalrOOP #&101;](../../../../visual-basic/misc/codesnippet/VisualBasic/walkthrough-creating-and-implementing-interfaces_4.vb)]  
  
     `Implements`语句指定的接口和实现的接口成员。  
  
4.  完成的定义`Prop1`通过将一个私有字段添加到存储的属性值的类中︰  
  
     [!code-vb[VbVbalrOOP #&102;](../../../../visual-basic/misc/codesnippet/VisualBasic/walkthrough-creating-and-implementing-interfaces_5.vb)]  
  
     返回的值`pval`从属性 get 访问器。  
  
     [!code-vb[VbVbalrOOP #&103;](../../../../visual-basic/misc/codesnippet/VisualBasic/walkthrough-creating-and-implementing-interfaces_6.vb)]  
  
     值设置`pval`在属性 set 访问器。  
  
     [!code-vb[VbVbalrOOP #&104;](../../../../visual-basic/misc/codesnippet/VisualBasic/walkthrough-creating-and-implementing-interfaces_7.vb)]  
  
5.  完成的定义`Method1`通过添加下面的代码。  
  
     [!code-vb[VbVbalrOOP #&105;](../../../../visual-basic/misc/codesnippet/VisualBasic/walkthrough-creating-and-implementing-interfaces_8.vb)]  
  
#### <a name="to-test-the-implementation-of-the-interface"></a>若要测试该接口实现  
  
1.  用鼠标右键单击你的项目中的启动窗体**解决方案资源管理器**，然后单击**查看代码**。 编辑器会显示启动窗体的类。 默认情况下，启动窗体称为`Form1`。  
  
2.  将以下代码添加`testInstance`字段拖至`Form1`类︰  
  
     [!code-vb[VbVbalrOOP #&120;](../../../../visual-basic/misc/codesnippet/VisualBasic/walkthrough-creating-and-implementing-interfaces_9.vb)]  
  
     通过声明`testInstance`作为`WithEvents`、`Form1`类可以处理其事件。  
  
3.  添加到以下事件处理程序`Form1`类来处理所引发的事件`testInstance`:  
  
     [!code-vb[VbVbalrOOP #&106;](../../../../visual-basic/misc/codesnippet/VisualBasic/walkthrough-creating-and-implementing-interfaces_10.vb)]  
  
4.  添加一个名为子例程`Test`到`Form1`类来测试实现类︰  
  
     [!code-vb[VbVbalrOOP #&107; 页](../../../../visual-basic/misc/codesnippet/VisualBasic/walkthrough-creating-and-implementing-interfaces_11.vb)]  
  
     `Test`过程创建的实现的类实例`MyInterface`，将分配到该实例`testInstance`字段中，设置一个属性，并通过该接口运行一个方法。  
  
5.  添加代码以调用`Test`过程从`Form1 Load`启动窗体的过程︰  
  
     [!code-vb[VbVbalrOOP #&108;](../../../../visual-basic/misc/codesnippet/VisualBasic/walkthrough-creating-and-implementing-interfaces_12.vb)]  
  
6.  运行`Test`过程通过按 F5。 将显示消息"Prop1 已设置为 9"。 之后您单击确定，显示"Method1 X 参数 is 5"的消息。 单击确定，并显示"事件处理程序捕获事件"的消息。  
  
## <a name="see-also"></a>另请参阅  
 [Implements 语句](../../../../visual-basic/language-reference/statements/implements-statement.md)   
 [接口](../../../../visual-basic/programming-guide/language-features/interfaces/index.md)   
 [Interface 语句](../../../../visual-basic/language-reference/statements/interface-statement.md)   
 [Event 语句](../../../../visual-basic/language-reference/statements/event-statement.md)

