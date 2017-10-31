---
title: "如何︰ 从 Visual Basic 中引用 COM 对象 |Microsoft 文档"
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
- COM interop, referencing COM objects
- referencing objects, COM objects from Visual Basic
- objects [Visual Basic], referencing
- COM objects, referencing
- interop assemblies
ms.assetid: 9c518fb4-27d9-4112-9e6a-5a7d0210af6f
caps.latest.revision: 13
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
ms.openlocfilehash: 97c132bcbd36ba7810acadb2aebddc5e84f0b44d
ms.lasthandoff: 03/13/2017

---
# <a name="how-to-reference-com-objects-from-visual-basic"></a>如何：从 Visual Basic 中引用 COM 对象
在[!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]，添加对具有类型库 COM 对象的引用需要互操作程序集创建一个 COM 库。 对成员的 COM 对象引用都路由到互操作程序集，然后将转发给实际的 COM 对象。 从 COM 对象的响应路由到互操作程序集，并将其转发到您[!INCLUDE[dnprdnshort](../../../csharp/getting-started/includes/dnprdnshort_md.md)]应用程序。  
  
 使用互操作程序集在.NET 程序集中嵌入的 COM 对象的类型信息的情况下，可以引用 COM 对象。 若要嵌入类型信息，请设置`Embed Interop Types`属性设置为`True`为对 COM 对象的引用。 如果您使用命令行编译器进行编译，请使用`/link`选项来引用 COM 库。 有关详细信息，请参阅[/link (Visual Basic 中)](../../../visual-basic/reference/command-line-compiler/link.md)。  
  
 [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]添加对类型库中的集成的开发环境 (IDE) 的引用时，会自动创建互操作程序集。 在从命令行处理时，可以使用 Tlbimp 实用程序来手动创建互操作程序集。  
  
### <a name="to-add-references-to-com-objects"></a>若要添加对 COM 对象的引用  
  
1.  在**项目**菜单上，选择**添加引用**，然后单击**COM**对话框中的选项卡。  
  
2.  选择你想要从 COM 对象的列表中使用的组件。  
  
3.  若要简化对互操作程序集的访问，将添加`Imports`到顶部的类或模块将在其中使用的 COM 对象的语句。 例如，下面的代码示例导入命名空间`INKEDLib`中所引用对象`Microsoft InkEdit Control 1.0`库。  
  
     [!code-vb[VbVbalrInterop #&40;](../../../visual-basic/programming-guide/com-interop/codesnippet/VisualBasic/how-to-reference-com-objects_1.vb)]  
  
### <a name="to-create-an-interop-assembly-using-tlbimp"></a>若要创建使用 Tlbimp 互操作程序集  
  
1.  如果尚不搜索路径的一部分，并且您目前不所在的目录，请将 Tlbimp 的位置添加到搜索路径。  
  
2.  调用 Tlbimp 命令提示符下，提供以下信息︰  
  
    -   包含类型库的 DLL 的名称和位置  
  
    -   名称和命名空间的位置信息的放置位置  
  
    -   目标互操作程序集的名称和位置  
  
     以下代码提供了一个示例：  
  
    ```  
    Tlbimp test3.dll /out:NameSpace1 /out:Interop1.dll  
    ```  
  
     可以使用 Tlbimp 来创建互操作程序集的类型库，即使对于未注册的 COM 对象。 但是，由互操作程序集引用的 COM 对象必须正确注册它们是要使用的计算机上。 可以通过使用 Regsvr32 实用程序随 Windows 操作系统附带注册 COM 对象。  
  
## <a name="see-also"></a>另请参阅  
 [COM 互操作](../../../visual-basic/programming-guide/com-interop/index.md)   
 [Tlbimp.exe （类型库导入程序）](http://msdn.microsoft.com/library/ec0a8d63-11b3-4acd-b398-da1e37e97382)   
 [Tlbexp.exe （类型库导出程序）](http://msdn.microsoft.com/library/a487d61b-d166-467b-a7ca-d8b52fbff42d)   
 [演练︰ 用 COM 对象实现继承](../../../visual-basic/programming-guide/com-interop/walkthrough-implementing-inheritance-with-com-objects.md)   
 [互操作性疑难解答](../../../visual-basic/programming-guide/com-interop/troubleshooting-interoperability.md)   
 [Imports 语句（.NET 命名空间和类型）](../../../visual-basic/language-reference/statements/imports-statement-net-namespace-and-type.md)
