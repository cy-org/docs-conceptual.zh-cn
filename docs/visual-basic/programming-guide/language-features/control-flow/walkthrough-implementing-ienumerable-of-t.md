---
title: "在 Visual Basic 中实现 IEnumerable |Microsoft 文档"
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
- control flow [Visual Basic]
- enumerable interfaces
- loop structures, optimizing performance
- control flow
ms.assetid: c60d7589-51f2-4463-a2d5-22506bbc1554
caps.latest.revision: 15
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
ms.openlocfilehash: 68c37c46cbceb1056d50972cdc58ddb7c7577447
ms.lasthandoff: 03/13/2017

---
# <a name="walkthrough-implementing-ienumerableof-t-in-visual-basic"></a>演练：在 Visual Basic 中实现 IEnumerable(Of T)
<xref:System.Collections.Generic.IEnumerable%601>接口由可以一次返回一系列值的一项的类实现。</xref:System.Collections.Generic.IEnumerable%601> 返回的数据一次一个项目是不需要将整个数据集加载到内存，无法使用它的优势。 只需要足够的内存用于从数据中加载的单个项。 类实现`IEnumerable(T)`接口可与使用`For Each`循环或 LINQ 查询。  
  
 例如，假设一个应用程序必须读取一个大型文本文件并将每一行返回从与特定搜索条件匹配的文件。 应用程序使用 LINQ 查询以从与指定的条件匹配的文件中返回行。 若要使用 LINQ 查询来查询该文件的内容，应用程序可以加载到一个数组或集合的文件的内容。 但是，将整个文件加载到数组或集合会占用比所需的内存比以往更多的内存。 LINQ 查询无法使用 enumerable 类，返回与搜索条件匹配的值改为查询该文件的内容。 返回仅有少数的查询匹配的值会消耗内存更少。  
  
 您可以创建一个类以实现<xref:System.Collections.Generic.IEnumerable%601>接口，以公开为可枚举数据源数据。</xref:System.Collections.Generic.IEnumerable%601> 您实现的类`IEnumerable(T)`接口会需要另一个类，该类实现<xref:System.Collections.Generic.IEnumerator%601>接口以循环访问源数据。</xref:System.Collections.Generic.IEnumerator%601> 这两个类，可以按顺序为特定类型返回的数据的项。  
  
 在本演练中，将创建一个类以实现`IEnumerable(Of String)`接口和实现类`IEnumerator(Of String)`接口，以一次读取文本文件的一行。  
  
[!INCLUDE[note_settings_general](../../../../csharp/language-reference/compiler-messages/includes/note_settings_general_md.md)]  
  
## <a name="creating-the-enumerable-class"></a>创建可枚举类  
  
|若要创建可枚举类项目|  
|---|  
|1.在[!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]，请在**文件**菜单上，指向**新建**，然后单击**项目**。<br />2.在**新项目**对话框中，在**项目类型**窗格中，请确保**Windows**处于选中状态。 选择**类库**中**模板**窗格。 在**名称**框中，键入`StreamReaderEnumerable`，然后单击**确定**。 将显示新项目。<br />3.在**解决方案资源管理器**，用鼠标右键单击 Class1.vb 文件，然后单击**重命名**。 文件重命名为`StreamReaderEnumerable.vb`，然后按 enter 键。 重命名该文件也进行重命名为该类`StreamReaderEnumerable`。 此类将实现`IEnumerable(Of String)`接口。<br />4.右击 StreamReaderEnumerable 项目，指向**添加**，然后单击**新项**。 选择**类**模板。 在**名称**框中，键入`StreamReaderEnumerator.vb`，然后单击**确定**。|  
  
 此项目中的第一个类是可枚举类，将实现`IEnumerable(Of String)`接口。 此泛型接口实现<xref:System.Collections.IEnumerable>接口，并保证此类的使用者可以访问值类型化为`String`。</xref:System.Collections.IEnumerable>  
  
|若要添加代码以实现 IEnumerable|  
|---|  
|1.打开 StreamReaderEnumerable.vb 文件。<br />2.在后面的行上`Public Class StreamReaderEnumerable`，键入以下命令并按 ENTER。<br />     [!code-vb[VbVbalrIteratorWalkthrough #&1;](../../../../visual-basic/programming-guide/language-features/control-flow/codesnippet/VisualBasic/walkthrough-implementing-ienumerable-of-t_1.vb)]<br />     [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]具有所需的成员的类将自动填充`IEnumerable(Of String)`接口。<br />3.一次，此可枚举类将从文本文件的一行读取行。 将以下代码添加到要公开将文件路径作为输入参数的公共构造函数的类。<br />     [!code-vb[VbVbalrIteratorWalkthrough #&2;](../../../../visual-basic/programming-guide/language-features/control-flow/codesnippet/VisualBasic/walkthrough-implementing-ienumerable-of-t_2.vb)]<br />4.实现<xref:System.Collections.Generic.IEnumerable%601.GetEnumerator%2A>方法`IEnumerable(Of String)`接口将返回的新实例`StreamReaderEnumerator`类</xref:System.Collections.Generic.IEnumerable%601.GetEnumerator%2A> 实现`GetEnumerator`方法`IEnumerable`接口可以成为`Private`，这是因为您必须公开只有的成员`IEnumerable(Of String)`接口。 替换的代码，[!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]为生成`GetEnumerator`方法替换为以下代码。<br />     [!code-vb[VbVbalrIteratorWalkthrough #&3;](../../../../visual-basic/programming-guide/language-features/control-flow/codesnippet/VisualBasic/walkthrough-implementing-ienumerable-of-t_3.vb)]|  
  
|若要添加代码以实现 IEnumerator|  
|---|  
|1.打开 StreamReaderEnumerator.vb 文件。<br />2.在后面的行上`Public Class StreamReaderEnumerator`，键入以下命令并按 ENTER。<br />     [!code-vb[VbVbalrIteratorWalkthrough #&4;](../../../../visual-basic/programming-guide/language-features/control-flow/codesnippet/VisualBasic/walkthrough-implementing-ienumerable-of-t_4.vb)]<br />     [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]具有所需的成员的类将自动填充`IEnumerator(Of String)`接口。<br />3.枚举器类打开文本文件，并执行文件 I/O，以从文件读取的行。 将下面的代码添加到类，以公开公共构造函数作为输入参数的文件路径和打开文本文件进行读取。<br />     [!code-vb[VbVbalrIteratorWalkthrough #&5;](../../../../visual-basic/programming-guide/language-features/control-flow/codesnippet/VisualBasic/walkthrough-implementing-ienumerable-of-t_5.vb)]<br />4.`Current`属性都`IEnumerator(Of String)`和`IEnumerator`从文本文件作为接口返回的当前项`String`。 实现`Current`属性`IEnumerator`接口可以成为`Private`，这是因为您必须公开只有的成员`IEnumerator(Of String)`接口。 替换的代码，[!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]为生成`Current`属性替换为以下代码。<br />     [!code-vb[VbVbalrIteratorWalkthrough #&6;](../../../../visual-basic/programming-guide/language-features/control-flow/codesnippet/VisualBasic/walkthrough-implementing-ienumerable-of-t_6.vb)]<br />5.`MoveNext`方法`IEnumerator`界面导航到文本文件中的下一项并更新所返回的值`Current`属性。 如果没有更多的项，若要读取，`MoveNext`方法将返回`False`; 否则为`MoveNext`方法将返回`True`。 将以下代码添加到 `MoveNext` 方法中。<br />     [!code-vb[VbVbalrIteratorWalkthrough #&7;](../../../../visual-basic/programming-guide/language-features/control-flow/codesnippet/VisualBasic/walkthrough-implementing-ienumerable-of-t_7.vb)]<br />6.`Reset`方法`IEnumerator`接口指示迭代器指向该文本文件开始，并清除当前项的值。 将以下代码添加到 `Reset` 方法中。<br />     [!code-vb[VbVbalrIteratorWalkthrough #&8;](../../../../visual-basic/programming-guide/language-features/control-flow/codesnippet/VisualBasic/walkthrough-implementing-ienumerable-of-t_8.vb)]<br />7.`Dispose`方法`IEnumerator`接口可保证在销毁迭代器之前，释放所有非托管的资源。 使用的文件句柄`StreamReader`对象是一个非托管的资源，销毁该迭代器实例之前，必须关闭。 替换的代码，[!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]为生成`Dispose`方法替换为以下代码。<br />     [!code-vb[VbVbalrIteratorWalkthrough #&9;](../../../../visual-basic/programming-guide/language-features/control-flow/codesnippet/VisualBasic/walkthrough-implementing-ienumerable-of-t_9.vb)]|  
  
## <a name="using-the-sample-iterator"></a>使用示例迭代器  
 可以在需要实现的对象的控制结构以及代码中使用 enumerable 类`IEnumerable`，如`For Next`循环或 LINQ 查询。 下面的示例演示`StreamReaderEnumerable`LINQ 查询中。  
  
 [!code-vb[VbVbalrIteratorWalkthrough #&10;](../../../../visual-basic/programming-guide/language-features/control-flow/codesnippet/VisualBasic/walkthrough-implementing-ienumerable-of-t_10.vb)]  
  
## <a name="see-also"></a>另请参阅  
 [在 Visual Basic 中的 LINQ 简介](../../../../visual-basic/programming-guide/language-features/linq/introduction-to-linq.md)   
 [控制流](../../../../visual-basic/programming-guide/language-features/control-flow/index.md)   
 [循环结构](../../../../visual-basic/programming-guide/language-features/control-flow/loop-structures.md)   
 [For Each...Next 语句](../../../../visual-basic/language-reference/statements/for-each-next-statement.md)

