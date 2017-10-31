---
title: "互操作性 (Visual Basic 中) 疑难解答 |Microsoft 文档"
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
- interop, deploying assemblies
- assemblies [Visual Basic]
- interop, installing assemblies that share components
- COM objects, troubleshooting
- interop, sharing components
- troubleshooting interoperability
- interoperability, troubleshooting
- COM interop, troubleshooting
- assemblies [Visual Basic], deploying
- troubleshooting Visual Basic, interoperability
- interop assemblies
- interoperability, sharing components
- shared components, using with assemblies
ms.assetid: b324cc1e-b03c-4f39-aea6-6a6d5bfd0e37
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
ms.openlocfilehash: cbc37638ed5c57b94356c2d189f36b66202ceba5
ms.lasthandoff: 03/13/2017

---
# <a name="troubleshooting-interoperability-visual-basic"></a>互操作性疑难解答 (Visual Basic)
当 COM 和托管的代码之间互操作[!INCLUDE[dnprdnshort](../../../csharp/getting-started/includes/dnprdnshort_md.md)]，您可能会遇到一个或多个下列常见问题。  
  
##  <a name="vbconinteroperabilitymarshalinganchor1"></a>互操作封送处理  
 有时，您可能需要使用数据类型不属于[!INCLUDE[dnprdnshort](../../../csharp/getting-started/includes/dnprdnshort_md.md)]。 互操作程序集处理的大多数工作对于 COM 对象，但你可能需要控制在向 COM 公开托管的对象时使用的数据类型 例如，类库中的结构必须指定`BStr`非托管字符串发送到由 Visual Basic 6.0 和早期版本创建的 COM 对象的类型。 在这种情况下，你可以使用<xref:System.Runtime.InteropServices.MarshalAsAttribute>若要使作为非托管类型公开的托管的类型的属性。</xref:System.Runtime.InteropServices.MarshalAsAttribute>  
  
##  <a name="vbconinteroperabilitymarshalinganchor2"></a>导出到非托管代码的固定长度的字符串  
 在 Visual Basic 6.0 和早期版本中，字符串至 COM 对象导出为没有 null 终止字符的字节序列。 与其他语言的兼容性[!INCLUDE[vbprvblong](../../../visual-basic/developing-apps/customizing-extending-my/includes/vbprvblong_md.md)]包括终止字符输出字符串时。 若要解决此不兼容性的最佳方式是将字符串作为数组中缺少终止字符导出`Byte`或`Char`。  
  
##  <a name="vbconinteroperabilitymarshalinganchor3"></a>导出继承层次结构  
 托管的类层次结构将平展出，当公开为 COM 对象。 例如，如果定义一个基类的成员，则继承的基类的派生类中公开为 COM 对象时，使用派生的类中的 COM 对象的客户端将不能使用继承的成员。 可以仅作为基类的实例从 COM 对象访问基类成员，然后仅当该基类还创建为 COM 对象。  
  
## <a name="overloaded-methods"></a>重载方法  
 虽然你可以创建重载方法与[!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]，它们不支持由 com 使用。 当包含重载的方法的类公开为 COM 对象时，重载方法会生成新的方法名。  
  
 例如，考虑一个具有两个重载类`Synch`方法。 当类公开为 COM 对象时，可能是新生成的方法名`Synch`和`Synch_2`。  
  
 此重命名操作会导致出现两个问题的 COM 对象的使用者。  
  
1.  客户端可能不希望生成的方法名。  
  
2.  到类或其基本类添加新的重载时，可以更改在类中公开为 COM 对象时生成的方法名。 这会导致版本控制问题。  
  
 若要解决这两个问题，为每个方法提供一个唯一的名称，而不是使用重载，当您开发将公开为 COM 对象的对象。  
  
##  <a name="vbconinteroperabilitymarshalinganchor4"></a>使用通过互操作程序集的 COM 对象  
 几乎好像它们是它们所表示的 COM 对象的托管的代码替换使用互操作程序集。 但是，因为它们是包装并不是实际的 COM 对象，有一些使用互操作程序集和标准程序集之间的差异。 这些不同之处包括公开的类，以及数据类型的参数和返回值。  
  
##  <a name="vbconinteroperabilitymarshalinganchor5"></a>公开为这两个接口的类和类  
 与标准的程序集中的类，不同的 COM 类在互操作程序集作为一个接口和类，表示的 COM 类中公开。 接口的名称是相同的 COM 类。 互操作的类的名称是相同的原始 COM 类，但以单词"类"追加。 例如，假设您的项目必须具有对 COM 对象的互操作程序集的引用。 如果 COM 类命名为`MyComClass`，智能感知和对象浏览器显示名为接口`MyComClass`和一个名为类`MyComClassClass`。  
  
##  <a name="vbconinteroperabilitymarshalinganchor6"></a>创建.NET Framework 类的实例  
 通常情况下，创建的实例[!INCLUDE[dnprdnshort](../../../csharp/getting-started/includes/dnprdnshort_md.md)]类使用`New`语句和类名。 具有互操作程序集所表示的 COM 类是在其中您可以使用的一个例子`New`语句提供的接口。 除非您使用了 COM 类`Inherits`语句，就像类一样，可以使用该接口。 下面的代码演示如何创建`Command`具有对 Microsoft ActiveX 数据对象 2.8 库 COM 对象的引用的项目中的对象︰  
  
 [!code-vb[VbVbalrInterop #&20;](../../../visual-basic/programming-guide/com-interop/codesnippet/VisualBasic/troubleshooting-interoperability_1.vb)]  
  
 但是，如果您使用 COM 类作为基类的派生类，您必须使用互操作表示的类的 COM 类，如以下代码所示︰  
  
 [!code-vb[VbVbalrInterop #&21;](../../../visual-basic/programming-guide/com-interop/codesnippet/VisualBasic/troubleshooting-interoperability_2.vb)]  
  
> [!NOTE]
>  互操作程序集隐式实现接口，用于表示 COM 类。 不应尝试使用`Implements`将导致语句来实现这些接口或错误。  
  
##  <a name="vbconinteroperabilitymarshalinganchor7"></a>参数和返回值的数据类型  
 标准程序集的成员，请与互操作程序集的成员可能具有不同于原始对象声明中使用的数据类型。 尽管互操作程序集将 COM 类型隐式转换为兼容的公共语言运行时类型，但您应注意两面用于防止运行时错误的数据类型。 例如，在 Visual Basic 6.0 和早期版本中，类型的值中创建的 COM 对象`Integer`假定[!INCLUDE[dnprdnshort](../../../csharp/getting-started/includes/dnprdnshort_md.md)]等效类型`Short`。 建议使用对象浏览器来检查导入成员的特征，然后使用它们。  
  
##  <a name="vbconinteroperabilitymarshalinganchor8"></a>模块级别 COM 方法  
 由大多数 COM 对象创建实例的 COM 类使用`New`关键字，然后再调用对象的方法。 此规则的例外涉及 COM 对象，包含`AppObj`或`GlobalMultiUse`COM 类。 这样的类中的模块级方法相似[!INCLUDE[vbprvblong](../../../visual-basic/developing-apps/customizing-extending-my/includes/vbprvblong_md.md)]类。 Visual Basic 6.0 和早期版本隐式创建此类对象的实例为您第一次调用其方法之一。 例如，在 Visual Basic 6.0 中可以添加到 Microsoft DAO 3.6 对象库，并调用的引用`DBEngine`而不必首先创建一个实例的方法︰  
  
```  
Dim db As DAO.Database  
' Open the database.  
Set db = DBEngine.OpenDatabase("C:\nwind.mdb")  
' Use the database object.  
```  
  
 [!INCLUDE[vbprvblong](../../../visual-basic/developing-apps/customizing-extending-my/includes/vbprvblong_md.md)]要求您始终创建 COM 对象的实例，然后才能使用它们的方法。 若要使用这些方法[!INCLUDE[vbprvblong](../../../visual-basic/developing-apps/customizing-extending-my/includes/vbprvblong_md.md)]、 所需的类的变量声明和使用新的关键字来将对象分配给对象变量。 `Shared`时想要确保可以使用关键字创建的类只有一个实例。  
  
 [!code-vb[VbVbalrInterop 第&23;](../../../visual-basic/programming-guide/com-interop/codesnippet/VisualBasic/troubleshooting-interoperability_3.vb)]  
  
##  <a name="vbconinteroperabilitymarshalinganchor9"></a>事件处理程序中未处理的错误  
 一个常见的互操作问题涉及处理由 COM 对象引发的事件的事件处理程序中的错误。 此类错误将被忽略，除非您明确检查使用`On Error`或`Try...Catch...Finally`语句。 例如，下面的示例摘自[!INCLUDE[vbprvblong](../../../visual-basic/developing-apps/customizing-extending-my/includes/vbprvblong_md.md)]具有对 Microsoft ActiveX 数据对象 2.8 库 COM 对象的引用的项目。  
  
 [!code-vb[VbVbalrInterop #&24;](../../../visual-basic/programming-guide/com-interop/codesnippet/VisualBasic/troubleshooting-interoperability_4.vb)]  
  
 此示例将按预期方式引发错误。 但是，如果您尝试相同的示例中而无需`Try...Catch...Finally`块中，错误将忽略就使用`OnError Resume Next`语句。 如果没有错误处理机制，被零除以无提示方式无法正常工作。 因为此类错误永远不会引发未处理的异常错误，很重要使用某种形式的处理从 COM 对象的事件的事件处理程序中的异常处理。  
  
### <a name="understanding-com-interop-errors"></a>了解 COM 互操作错误  
 如果没有错误处理机制，互操作调用通常产生错误时提供非常少的信息。 只要有可能，使用结构化处理，以提供有关问题的详细信息，它们发生的错误。 调试应用程序时可能特别有用。 例如:   
  
 [!code-vb[VbVbalrInterop #&25;](../../../visual-basic/programming-guide/com-interop/codesnippet/VisualBasic/troubleshooting-interoperability_5.vb)]  
  
 可以通过检查异常对象的内容中找到的错误说明、 HRESULT 和 COM 错误的原因等信息。  
  
##  <a name="vbconinteroperabilitymarshalinganchor10"></a>ActiveX 控件问题  
 使用 Visual Basic 6.0 中的大多数 ActiveX 控件使用[!INCLUDE[vbprvblong](../../../visual-basic/developing-apps/customizing-extending-my/includes/vbprvblong_md.md)]顺利。 主要的例外是容器控件中或以可视方式可以包含其他控件的控件。 无法与正常工作的旧控件的一些示例[!INCLUDE[vsprvs](../../../csharp/includes/vsprvs_md.md)]如下︰  
  
-   Microsoft 窗体 2.0 框架控件  
  
-   Up-down 控件，也称为数值调节钮控件  
  
-   Sheridan 选项卡控件  
  
 有的不受支持的 ActiveX 控件问题只有几个解决方法。 你可以迁移现有控件与[!INCLUDE[vsprvs](../../../csharp/includes/vsprvs_md.md)]如果拥有原始源代码。 否则，您可以检查与软件供应商更新。NET 兼容版本的控件来替换不受支持的 ActiveX 控件。  
  
##  <a name="vbconinteroperabilitymarshalinganchor11"></a>传递的控件 ByRef 的 ReadOnly 属性  
 [!INCLUDE[vbprvblong](../../../visual-basic/developing-apps/customizing-extending-my/includes/vbprvblong_md.md)]如果通过，但您有时引发 COM 错误，如"错误 0x800A017F CTL_E_SETNOTSUPPORTED"`ReadOnly`某些较旧的 ActiveX 控件作为属性`ByRef`其他过程的参数。 从 Visual Basic 6.0 中的过程调用不会引发错误，并就像通过值传递，参数的处理方式类似。 请参阅中的错误消息[!INCLUDE[vbprvblong](../../../visual-basic/developing-apps/customizing-extending-my/includes/vbprvblong_md.md)]是 COM 对象的报告您尝试更改一个属性，它不具有属性`Set`过程。  
  
 如果您有权访问所调用的过程，您可以通过使用来防止出现此错误`ByVal`关键字来声明参数接受`ReadOnly`属性。 例如:   
  
 [!code-vb[VbVbalrInterop #&26;](../../../visual-basic/programming-guide/com-interop/codesnippet/VisualBasic/troubleshooting-interoperability_6.vb)]  
  
 如果还没有被调用的过程对源代码的访问，您可以强制要通过添加一组额外的方括号调用过程按值传递的属性。 例如，在项目中包含对 Microsoft ActiveX 数据对象 2.8 库 COM 对象的引用，您可以使用︰  
  
 [!code-vb[VbVbalrInterop #&27;](../../../visual-basic/programming-guide/com-interop/codesnippet/VisualBasic/troubleshooting-interoperability_7.vb)]  
  
##  <a name="vbconinteroperabilitymarshalinganchor12"></a>部署公开互操作的程序集  
 公开 COM 接口的程序集部署了一些独特的挑战。 例如，当单独的应用程序引用同一个 COM 程序集时，将产生潜在的问题。 安装新版本的程序集和另一个应用程序仍在使用旧版本的程序集时，这种情况很常见。 如果您卸载共享某个 DLL 程序集，您可以会无意中使其不可用对其他程序集。  
  
 若要避免此问题，应安装到全局程序集缓存 (GAC) 中的共享程序集和用于该组件的合并模块。 如果您不能在 GAC 中安装应用程序，它应安装到 CommonFilesFolder 特定于版本的子目录中。  
  
 不共享的程序集应并排放置在调用应用程序的目录。  
  
## <a name="see-also"></a>另请参阅  
 <xref:System.Runtime.InteropServices.MarshalAsAttribute></xref:System.Runtime.InteropServices.MarshalAsAttribute>   
 [COM 互操作](../../../visual-basic/programming-guide/com-interop/index.md)   
 [Tlbimp.exe （类型库导入程序）](http://msdn.microsoft.com/library/ec0a8d63-11b3-4acd-b398-da1e37e97382)   
 [Tlbexp.exe （类型库导出程序）](http://msdn.microsoft.com/library/a487d61b-d166-467b-a7ca-d8b52fbff42d)   
 [演练︰ 用 COM 对象实现继承](../../../visual-basic/programming-guide/com-interop/walkthrough-implementing-inheritance-with-com-objects.md)   
 [Inherits 语句](../../../visual-basic/language-reference/statements/inherits-statement.md)   
 [全局程序集缓存](http://msdn.microsoft.com/library/cf5eacd0-d3ec-4879-b6da-5fd5e4372202)
