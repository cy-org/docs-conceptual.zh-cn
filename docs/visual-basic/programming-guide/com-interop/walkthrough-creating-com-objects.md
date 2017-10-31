---
title: "演练︰ 使用 Visual Basic 创建 COM 对象 |Microsoft 文档"
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
- COM interop, creating COM objects
- COM objects, creating
- COM interop, walkthroughs
- object creation, COM objects
- COM objects, walkthroughs
ms.assetid: 7b07a463-bc72-4392-9ba0-9dfcb697a44f
caps.latest.revision: 30
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
ms.openlocfilehash: cce28e2be5914880107334bf2c4dc4dc645b4793
ms.lasthandoff: 03/13/2017

---
# <a name="walkthrough-creating-com-objects-with-visual-basic"></a>演练：使用 Visual Basic 创建 COM 对象
创建新的应用程序或组件时，则最好创建.NET Framework 程序集。 但是，[!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]还可以轻松地公开 com 是.NET Framework 组件 这使您可以提供新的组件需要 COM 组件的早期应用程序套件。 本演练演示如何使用[!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]公开[!INCLUDE[dnprdnshort](../../../csharp/getting-started/includes/dnprdnshort_md.md)]对象作为 COM 对象，包括使用和不使用 COM 类模板。  
  
 公开 COM 对象的最简单方法是使用 COM 类模板。 COM 类模板创建一个新类，，，然后配置你的项目生成的类和互操作性层作为 COM 对象并将其注册到操作系统。  
  
> [!NOTE]
>  尽管您还可以公开的类中创建[!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]为要使用的非托管代码的 COM 对象，它不是真正的 COM 对象并不能由[!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]。 有关详细信息，请参阅[.NET Framework 应用程序中的 COM 互操作性](../../../visual-basic/programming-guide/com-interop/com-interoperability-in-net-framework-applications.md)。  
  
[!INCLUDE[note_settings_general](../../../csharp/language-reference/compiler-messages/includes/note_settings_general_md.md)]  
  
### <a name="to-create-a-com-object-by-using-the-com-class-template"></a>若要通过使用 COM 类模板创建的 COM 对象  
  
1.  打开一个新的 Windows 应用程序项目，从**文件**菜单上，通过单击**新项目**。  
  
2.  在**新项目**对话框中的下**项目类型**字段中，检查是否选中了 Windows。 选择**类库**从**模板**列表，，然后单击**确定**。 将显示新项目。  
  
3.  选择**添加新项**从**项目**菜单。 **添加新项**中会显示对话框。  
  
4.  选择**COM 类**从**模板**列表，，然后单击**添加**。 [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]添加一个新类并配置 COM 互操作的新项目。  
  
5.  向 COM 类中添加代码，例如属性、 方法和事件。  
  
6.  选择**生成 ClassLibrary1**从**生成**菜单。 [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]生成程序集和随操作系统一起注册的 COM 对象。  
  
## <a name="creating-com-objects-without-the-com-class-template"></a>创建 COM 对象不使用 COM 类模板  
 此外可以创建一个手动而不是使用 COM 类模板的 COM 类。 当您正在从命令行或希望更好地控制如何定义 COM 对象时，此过程是很有帮助。  
  
#### <a name="to-set-up-your-project-to-generate-a-com-object"></a>若要设置你的项目以生成一个 COM 对象  
  
1.  打开一个新的 Windows 应用程序项目，从**文件**菜单上，通过单击**NewProject**。  
  
2.  在**新项目**对话框中的下**项目类型**字段中，检查是否选中了 Windows。 选择**类库**从**模板**列表，，然后单击**确定**。 将显示新项目。  
  
3.  在**解决方案资源管理器**，用鼠标右键单击您的项目，然后单击**属性**。 **项目设计器**显示。  
  
4.  单击“编译”****选项卡。  
  
5.  选择**为 COM 互操作注册**复选框。  
  
#### <a name="to-set-up-the-code-in-your-class-to-create-a-com-object"></a>若要将您的类中的代码设置为创建 COM 对象  
  
1.  在**解决方案资源管理器**，双击**Class1.vb**以显示其代码。  
  
2.  将该类重命名为 `ComClass1`。  
  
3.  添加以下常量`ComClass1`。 它们将存储不需要具有 COM 对象的全局唯一标识符 (GUID) 常量。  
  
     [!code-vb[VbVbalrInterop #&2;](../../../visual-basic/programming-guide/com-interop/codesnippet/VisualBasic/walkthrough-creating-com-objects_1.vb)]  
  
4.  在**工具**菜单上，单击**创建 Guid**。 在**创建 GUID**对话框中，单击**注册表格式**，然后单击**副本**。 单击“退出” ****。  
  
5.  替换空字符串作为`ClassId`guid 的计算机，移除前导空格和尾随大括号内。 例如，如果 Guidgen 由提供的 GUID 是`"{2C8B0AEE-02C9-486e-B809-C780A11530FE}"`，则您的代码应出现，如下所示。  
  
     [!code-vb[VbVbalrInterop #&3;](../../../visual-basic/programming-guide/com-interop/codesnippet/VisualBasic/walkthrough-creating-com-objects_2.vb)]  
  
6.  重复前面的步骤为`InterfaceId`和`EventsId`常量，如以下示例所示。  
  
     [!code-vb[VbVbalrInterop #&4;](../../../visual-basic/programming-guide/com-interop/codesnippet/VisualBasic/walkthrough-creating-com-objects_3.vb)]  
  
    > [!NOTE]
    >  请确保 Guid 是新且唯一的。否则，COM 组件可能与其他 COM 组件。  
  
7.  添加`ComClass`属性设为`ComClass1`，指定的类 ID、 接口 ID 和事件 ID 的 Guid，如以下示例所示︰  
  
     [!code-vb[VbVbalrInterop #&5;](../../../visual-basic/programming-guide/com-interop/codesnippet/VisualBasic/walkthrough-creating-com-objects_4.vb)]  
  
8.  COM 类必须具有无参数`Public Sub New()`构造函数或类无法正确注册。 将无参数构造函数添加到类︰  
  
     [!code-vb[VbVbalrInterop #&6;](../../../visual-basic/programming-guide/com-interop/codesnippet/VisualBasic/walkthrough-creating-com-objects_5.vb)]  
  
9. 将属性、 方法和事件添加到类，它与结束`End Class`语句。 选择**生成解决方案**从**生成**菜单。 [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]生成程序集和随操作系统一起注册的 COM 对象。  
  
    > [!NOTE]
    >  使用生成的 COM 对象[!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]不能由其他使用[!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]应用程序因为它们不是真正的 COM 对象。 尝试添加对此类 COM 对象的引用将引发错误。 有关详细信息，请参阅[.NET Framework 应用程序中的 COM 互操作性](../../../visual-basic/programming-guide/com-interop/com-interoperability-in-net-framework-applications.md)。  
  
## <a name="see-also"></a>另请参阅  
 <xref:Microsoft.VisualBasic.ComClassAttribute></xref:Microsoft.VisualBasic.ComClassAttribute>   
 [COM 互操作](../../../visual-basic/programming-guide/com-interop/index.md)   
 [演练︰ 用 COM 对象实现继承](../../../visual-basic/programming-guide/com-interop/walkthrough-implementing-inheritance-with-com-objects.md)   
 [#Region 指令](../../../visual-basic/language-reference/directives/region-directive.md)   
 [.NET Framework 应用程序中的 COM 互操作性](../../../visual-basic/programming-guide/com-interop/com-interoperability-in-net-framework-applications.md)   
 [互操作性疑难解答](../../../visual-basic/programming-guide/com-interop/troubleshooting-interoperability.md)
