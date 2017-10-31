---
title: "演练︰ 用 COM 对象 (Visual Basic 中) 实现继承 |Microsoft 文档"
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
- inheritance, COM reusability
- base classes, COM reusability
- inheritance, walkthroughs
- derived classes, COM reusability
ms.assetid: f8e7263a-de13-48d1-b67c-ca1adf3544d9
caps.latest.revision: 16
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
ms.openlocfilehash: fa7753847619f14600c924cba01e55651c4f17c2
ms.lasthandoff: 03/13/2017

---
# <a name="walkthrough-implementing-inheritance-with-com-objects-visual-basic"></a>演练：用 COM 对象实现继承 (Visual Basic)
您可以派生从 Visual Basic 类`Public`中 COM 对象，即使他们的早期版本中创建的类[!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]。 属性和方法从 COM 对象继承的类可以重写或重载只是作为属性和方法的任何其他基类可以重写或重载。 从 COM 对象的继承具有不希望重新编译现有类库时很有帮助。  
  
 下面的过程演示如何使用 Visual Basic 6.0 中创建 COM 对象，其中包含一个类，并将其作为基类。  
  
[!INCLUDE[note_settings_general](../../../csharp/language-reference/compiler-messages/includes/note_settings_general_md.md)]  
  
### <a name="to-build-the-com-object-that-is-used-in-this-walkthrough"></a>若要生成在本演练中使用的 COM 对象  
  
1.  在 Visual Basic 6.0 中，打开一个新的 ActiveX DLL 项目。 一个名为项目`Project1`创建。 它具有一个名为类`Class1`。  
  
2.  在**项目资源管理器**，用鼠标右键单击**Project1**，然后单击**Project1 属性**。 **项目属性**中会显示对话框。  
  
3.  在**常规**的选项卡上**项目属性**对话框框中，键入更改项目名称`ComObject1`中**项目名称**字段。  
  
4.  在**项目资源管理器**，用鼠标右键单击`Class1`，然后单击**属性**。 **属性**显示为类的窗口。  
  
5.  更改`Name`属性设置为`MathFunctions`。  
  
6.  在**项目资源管理器**，用鼠标右键单击`MathFunctions`，然后单击**查看代码**。 **代码编辑器**显示。  
  
7.  添加一个本地变量来保存属性值︰  
  
    ```  
    ' Local variable to hold property value  
    Private mvarProp1 As Integer  
    ```  
  
8.  将属性添加`Let`和属性`Get`属性过程︰  
  
    ```  
    Public Property Let Prop1(ByVal vData As Integer)  
       'Used when assigning a value to the property.  
       mvarProp1 = vData  
    End Property  
    Public Property Get Prop1() As Integer  
       'Used when retrieving a property's value.  
       Prop1 = mvarProp1  
    End Property  
    ```  
  
9. 添加一个函数︰  
  
    ```  
    Function AddNumbers(   
       ByVal SomeNumber As Integer,   
       ByVal AnotherNumber As Integer) As Integer  
  
       AddNumbers = SomeNumber + AnotherNumber  
    End Function  
    ```  
  
10. 创建和注册的 COM 对象，通过单击**使 ComObject1.dll**上**文件**菜单。  
  
    > [!NOTE]
    >  尽管您还可以公开与所创建的类[!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]作为 COM 对象，它不是真正的 COM 对象，不能在本演练中使用。 有关详细信息，请参阅[.NET Framework 应用程序中的 COM 互操作性](../../../visual-basic/programming-guide/com-interop/com-interoperability-in-net-framework-applications.md)。  
  
## <a name="interop-assemblies"></a>互操作程序集  
 在以下过程中，您将创建一个互操作程序集，它将作为非托管的代码 （如 COM 对象） 和托管的代码之间的桥梁[!INCLUDE[vsprvs](../../../csharp/includes/vsprvs_md.md)]使用。 互操作程序集，[!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]创建句柄对象的许多使用 COM 的详细信息，如*互操作封送处理*，包装参数和返回值转换为等效的数据的进程类型标记为它们移动到和从 COM 对象。 中的引用[!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]互操作程序集，而不是实际的 COM 对象的应用程序指向。  
  
#### <a name="to-use-a-com-object-with-visual-basic-2005-and-later-versions"></a>若要使用 Visual Basic 2005 和更高版本的 COM 对象  
  
1.  打开一个新[!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]Windows 应用程序项目。  
  
2.  在**项目**菜单上，单击**添加引用**。  
  
     **添加引用**中会显示对话框。  
  
3.  在**COM**选项卡上，双击`ComObject1`中**组件名称**列表，然后单击**确定**。  
  
4.  在 **“项目”** 菜单上，单击 **“添加新项”**。  
  
     **添加新项**中会显示对话框。  
  
5.  在**模板**窗格中，单击**类**。  
  
     默认文件名， `Class1.vb`，将出现在**名称**字段。 将此字段更改为 MathClass.vb，然后单击**添加**。 这将创建一个名为类`MathClass`，并显示其代码。  
  
6.  将以下代码添加到顶部`MathClass`从 COM 类继承。  
  
     [!code-vb[VbVbalrInterop #&31;](../../../visual-basic/programming-guide/com-interop/codesnippet/VisualBasic/walkthrough-implementing-inheritance-with-com-objects_1.vb)]  
  
7.  通过添加以下代码到重载的基类的公共方法`MathClass`:  
  
     [!code-vb[VbVbalrInterop #&32;](../../../visual-basic/programming-guide/com-interop/codesnippet/VisualBasic/walkthrough-implementing-inheritance-with-com-objects_2.vb)]  
  
8.  通过添加下面的代码来扩展继承的类`MathClass`:  
  
     [!code-vb[VbVbalrInterop 第&33;](../../../visual-basic/programming-guide/com-interop/codesnippet/VisualBasic/walkthrough-implementing-inheritance-with-com-objects_3.vb)]  
  
 新类继承的属性中的 COM 对象的基类，重载方法，并定义要扩展类的新方法。  
  
#### <a name="to-test-the-inherited-class"></a>若要测试继承的类  
  
1.  向启动窗体中，添加一个按钮，然后双击它以查看其代码。  
  
2.  在按钮的`Click`事件处理程序，添加以下代码以创建的实例`MathClass`并调用重载的方法︰  
  
     [!code-vb[VbVbalrInterop #&34;](../../../visual-basic/programming-guide/com-interop/codesnippet/VisualBasic/walkthrough-implementing-inheritance-with-com-objects_4.vb)]  
  
3.  通过按 F5 运行项目。  
  
 当您单击在表单上，按钮时`AddNumbers`方法首先调用的`Short`数据类型的数字，和[!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]选择适当的方法从基类。 第二次调用`AddNumbers`定向到的重载方法`MathClass`。 第三个调用调用`SubtractNumbers`方法，扩展类。 设置了基类中的属性，并且显示的值。  
  
## <a name="next-steps"></a>后续步骤  
 您可能已经注意到，重载`AddNumbers`函数起来都具有相同的数据类型为继承自基类的 COM 对象的方法。 这是因为参数和参数的基类方法被定义为 16 位整数，在 Visual Basic 6.0 中，但它们公开为 16 位整数类型的`Short`更高版本的 Visual Basic 中。 新函数接受 32 位整数，并重载基类函数。  
  
 当使用 COM 对象，请确保验证参数的大小和数据类型。 例如，当使用接受 Visual Basic 6.0 集合对象作为参数的 COM 对象时，不能提供更高版本的 Visual Basic 中的集合。  
  
 属性和从 COM 类继承的方法可以重写，意味着您可以声明本地属性或方法来代替一个属性或方法继承自基类的 COM 类。 重写继承的 COM 属性的规则是相似的规则重写其他属性和方法有以下例外︰  
  
-   如果重写任何属性或方法从 COM 类继承时，必须重写所有其他继承的属性和方法。  
  
-   使用属性`ByRef`参数不能重写。  
  
## <a name="see-also"></a>另请参阅  
 [.NET Framework 应用程序中的 COM 互操作性](../../../visual-basic/programming-guide/com-interop/com-interoperability-in-net-framework-applications.md)   
 [Inherits 语句](../../../visual-basic/language-reference/statements/inherits-statement.md)   
 [Short 数据类型](../../../visual-basic/language-reference/data-types/short-data-type.md)
