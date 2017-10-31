---
title: "演练︰ 嵌入的类型的托管 Visual Studio (Visual Basic 中) 中的程序集 |Microsoft 文档"
ms.custom: 
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- VB
ms.assetid: 56ed12ba-adff-4e9c-a668-7fcba80c4795
caps.latest.revision: 3
author: stevehoag
ms.author: shoag
translation.priority.mt:
- cs-cz
- pl-pl
- pt-br
- tr-tr
translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: adc58e081cd9b874a841d84b11d92cbffb6ba6b8
ms.lasthandoff: 03/13/2017

---
# <a name="walkthrough-embedding-types-from-managed-assemblies-in-visual-studio-visual-basic"></a>演练︰ 在 Visual Studio (Visual Basic 中) 中嵌入托管程序集中的类型
如果您嵌入类型信息从强名称的托管程序集，可以松耦合应用程序以实现版本独立性中的类型。 也就是说，您的程序可以编写为使用多个版本中的类型的托管库，而无需为每个版本重新编译。  
  
 用 COM 互操作，例如从 Microsoft Office 中使用自动化对象的应用程序经常使用嵌入类型。 嵌入类型信息，使程序可以使用不同版本的 Microsoft Office 的不同计算机上的相同内部版本。 但是，您还可以使用嵌入了一个完全托管的解决方案的类型。  
  
 可以从具有以下特征的程序集嵌入类型信息︰  
  
-   程序集公开至少一个公共接口。  
  
-   表示嵌入的接口为`ComImport`属性和一个`Guid`属性 （和一个唯一的 GUID）。  
  
-   程序集通过批注`ImportedFromTypeLib`属性或`PrimaryInteropAssembly`属性和程序集级别`Guid`属性。 (默认情况下，Visual Basic 项目模板包含程序集级别`Guid`属性。)  
  
 指定可嵌入的公共接口后，您可以创建实现这些接口的运行时类。 客户端程序然后可以通过引用包含的公共接口和设置的程序集嵌入在设计时这些接口的类型信息`Embed Interop Types`属性的引用的`True`。 这相当于使用命令行编译器，使用引用的程序集`/link`编译器选项。 然后，客户端程序可以加载运行时对象类型化为这些接口的实例。 如果您创建具有强名称的运行时程序集的新版本，客户端程序不必使用更新的运行时的程序集重新编译。 相反，客户端程序将继续使用任何版本的运行时程序集是提供给它，将用于公共接口的嵌入的类型信息。  
  
 由于类型嵌入的主要功能是支持嵌入类型信息从 COM 互操作程序集，以下限制将适用时完全托管的解决方案中嵌入类型信息︰  
  
-   嵌入只有特定于 COM 互操作的属性;其他属性将被忽略。  
  
-   如果某个类型使用的泛型参数的泛型参数的类型为嵌入的类型，不能跨程序集边界使用该类型。 跨程序集边界的示例包括从另一个程序集调用方法或其他程序集中派生类型从一种类型定义。  
  
-   未嵌入常量。  
  
-   <xref:System.Collections.Generic.Dictionary%602?displayProperty=fullName>类不支持嵌入的类型作为密钥。</xref:System.Collections.Generic.Dictionary%602?displayProperty=fullName> 您可以实现您自己的字典类型以支持嵌入的类型作为密钥。  
  
 在本演练中，将执行以下操作︰  
  
-   创建具有强名称程序集具有一个公共接口，其中包含可嵌入类型信息。  
  
-   创建具有强名称的运行时程序集实现该公共接口。  
  
-   创建嵌入的公共接口的类型信息，并创建运行时程序集中类的实例的客户端程序。  
  
-   修改并重新生成运行时程序集。  
  
-   运行客户端程序运行时程序集的新版本正在使用而无需重新编译客户端程序。  
  
[!INCLUDE[note_settings_general](../../../../csharp/language-reference/compiler-messages/includes/note_settings_general_md.md)]  
  
## <a name="creating-an-interface"></a>创建一个接口  
  
#### <a name="to-create-the-type-equivalence-interface-project"></a>若要创建类型等效性接口项目  
  
1.  在 Visual Studio 中，在**文件**菜单上，指向**新建**，然后单击**项目**。  
  
2.  在**新项目**对话框中，在**项目类型**窗格中，请确保**Windows**处于选中状态。 选择**类库**中**模板**窗格。 在**名称**框中，键入`TypeEquivalenceInterface`，然后单击**确定**。 创建新项目。  
  
3.  在**解决方案资源管理器**，用鼠标右键单击 Class1.vb 文件，然后单击**重命名**。 文件重命名为`ISampleInterface.vb`，然后按 enter 键。 重命名该文件也进行重命名为该类`ISampleInterface`。 此类将表示为类的公共接口。  
  
4.  右击 TypeEquivalenceInterface 项目并单击**属性**。 单击“编译”****选项卡。 输出路径设置为您的开发计算机上的有效位置如`C:\TypeEquivalenceSample`。 此外将在本演练中稍后的步骤中使用此位置。  
  
5.  在仍在编辑项目属性，同时单击**签名**选项卡。 选择**为程序集签名**选项。 在**选择强名称密钥文件**列表中，单击** <New...> **。</New...> 在**密钥文件名称**框中，键入`key.snk`。 清除**保护密钥文件使用的密码**复选框。 单击 **“确定”**。  
  
6.  打开 ISampleInterface.vb 文件。 将以下代码添加到 ISampleInterface 类文件以创建 ISampleInterface 界面。  
  
<CodeContentPlaceHolder>0</CodeContentPlaceHolder>  
7.  在**工具**菜单上，单击**创建 Guid**。 在**创建 GUID**对话框中，单击**注册表格式**，然后单击**副本**。 单击“退出” ****。  
  
8.  在`Guid`属性，删除样本 GUID 并粘贴从复制的 GUID**创建 GUID**对话框。 从复制的 GUID 中删除大括号 （{}）。  
  
9. 在**项目**菜单上，单击**显示所有文件**。  
  
10. 在**解决方案资源管理器**，展开**我的项目**文件夹。 双击 AssemblyInfo.vb。 将以下属性添加到该文件。  
  
<CodeContentPlaceHolder>1</CodeContentPlaceHolder>  
     保存该文件。  
  
11. 保存项目。  
  
12. 右击 TypeEquivalenceInterface 项目并单击**生成**。 编译和保存到指定的生成输出路径 (例如，C:\TypeEquivalenceSample) 类库.dll 文件。  
  
## <a name="creating-a-runtime-class"></a>创建运行时类  
  
#### <a name="to-create-the-type-equivalence-runtime-project"></a>若要创建类型等效性运行时项目  
  
1.  在 Visual Studio 中，在**文件**菜单上，指向**新建**，然后单击**项目**。  
  
2.  在**新项目**对话框中，在**项目类型**窗格中，请确保**Windows**处于选中状态。 选择**类库**中**模板**窗格。 在**名称**框中，键入`TypeEquivalenceRuntime`，然后单击**确定**。 创建新项目。  
  
3.  在**解决方案资源管理器**，用鼠标右键单击 Class1.vb 文件，然后单击**重命名**。 文件重命名为`SampleClass.vb`，然后按 enter 键。 此外会重命名该文件重命名为该类`SampleClass`。 此类将实现`ISampleInterface`接口。  
  
4.  右击 TypeEquivalenceRuntime 项目并单击**属性**。 单击“编译”****选项卡。 将输出路径设置到相同的位置在 TypeEquivalenceInterface 项目中，例如，使用`C:\TypeEquivalenceSample`。  
  
5.  在仍在编辑项目属性，同时单击**签名**选项卡。 选择**为程序集签名**选项。 在**选择强名称密钥文件**列表中，单击** <New...> **。</New...> 在**密钥文件名称**框中，键入`key.snk`。 清除**保护密钥文件使用的密码**复选框。 单击 **“确定”**。  
  
6.  右击 TypeEquivalenceRuntime 项目并单击**添加引用**。 单击**浏览**选项卡上，浏览到输出路径文件夹。 选择 TypeEquivalenceInterface.dll 文件并单击**确定**。  
  
7.  在**项目**菜单上，单击**显示所有文件**。  
  
8.  在**解决方案资源管理器**，展开**引用**文件夹。 选择 TypeEquivalenceInterface 引用。 在有关 TypeEquivalenceInterface 参考属性窗口中，设置**特定版本**属性设置为**False**。  
  
9. 将以下代码添加到 SampleClass 类文件以创建 SampleClass 类。  
  
<CodeContentPlaceHolder>2</CodeContentPlaceHolder>  
10. 保存项目。  
  
11. 右击 TypeEquivalenceRuntime 项目并单击**生成**。 编译和保存到指定的生成输出路径 (例如，C:\TypeEquivalenceSample) 类库.dll 文件。  
  
## <a name="creating-a-client-project"></a>创建客户端项目  
  
#### <a name="to-create-the-type-equivalence-client-project"></a>若要创建类型等效性客户端项目  
  
1.  在 Visual Studio 中，在**文件**菜单上，指向**新建**，然后单击**项目**。  
  
2.  在**新项目**对话框中，在**项目类型**窗格中，请确保**Windows**处于选中状态。 选择**控制台应用程序**中**模板**窗格。 在**名称**框中，键入`TypeEquivalenceClient`，然后单击**确定**。 创建新项目。  
  
3.  右击 TypeEquivalenceClient 项目并单击**属性**。 单击“编译”****选项卡。 将输出路径设置到相同的位置在 TypeEquivalenceInterface 项目中，例如，使用`C:\TypeEquivalenceSample`。  
  
4.  右击 TypeEquivalenceClient 项目并单击**添加引用**。 单击**浏览**选项卡上，浏览到输出路径文件夹。 选择 TypeEquivalenceInterface.dll 文件 (不 TypeEquivalenceRuntime.dll) 并单击**确定**。  
  
5.  在**项目**菜单上，单击**显示所有文件**。  
  
6.  在**解决方案资源管理器**，展开**引用**文件夹。 选择 TypeEquivalenceInterface 引用。 在有关 TypeEquivalenceInterface 参考属性窗口中，设置**嵌入互操作类型**属性设置为**True**。  
  
7.  将以下代码添加到 Module1.vb 文件以创建客户端程序。  
  
<CodeContentPlaceHolder>3</CodeContentPlaceHolder>  
8.  按 CTRL + F5 生成并运行该程序。  
  
## <a name="modifying-the-interface"></a>修改界面  
  
#### <a name="to-modify-the-interface"></a>若要修改的界面  
  
1.  在 Visual Studio 中，在**文件**菜单上，指向**打开**，然后单击**项目/解决方案**。  
  
2.  在**打开项目**对话框中，右键单击 TypeEquivalenceInterface 项目，然后单击**属性**。 单击“应用程序” **** 选项卡。 单击**程序集信息**按钮。 更改**程序集版本**和**文件版本**值复制到`2.0.0.0`。  
  
3.  打开 ISampleInterface.vb 文件。 将下面的代码行添加到 ISampleInterface 接口。  
  
<CodeContentPlaceHolder>4</CodeContentPlaceHolder>  
     保存该文件。  
  
4.  保存项目。  
  
5.  右击 TypeEquivalenceInterface 项目并单击**生成**。 编译和保存在指定的生成输出路径 (例如，C:\TypeEquivalenceSample) 类库.dll 文件的新版本。  
  
## <a name="modifying-the-runtime-class"></a>修改运行时类  
  
#### <a name="to-modify-the-runtime-class"></a>若要修改的运行时类  
  
1.  在 Visual Studio 中，在**文件**菜单上，指向**打开**，然后单击**项目/解决方案**。  
  
2.  在**打开项目**对话框框中，右击 TypeEquivalenceRuntime 项目，单击**属性**。 单击“应用程序” **** 选项卡。 单击**程序集信息**按钮。 更改**程序集版本**和**文件版本**值复制到`2.0.0.0`。  
  
3.  打开 SampleClass.vbfile。 将下面的代码行添加到 SampleClass 类。  
  
```vb  
Public Function GetDate() As DateTime Implements ISampleInterface.GetDate  
    Return Now  
End Function  
```  
  
     Save the file.  
  
4.  保存项目。  
  
5.  右击 TypeEquivalenceRuntime 项目并单击**生成**。 编译和保存在以前指定的生成输出路径 (例如，C:\TypeEquivalenceSample) 类库.dll 文件的更新的版本。  
  
6.  在文件资源管理器中，打开输出路径文件夹 (例如，C:\TypeEquivalenceSample)。 双击 TypeEquivalenceClient.exe 以运行该程序。 该程序将反映 TypeEquivalenceRuntime 程序集的新版本，而不具有已重新编译。  
  
## <a name="see-also"></a>另请参阅  
 [/link (Visual Basic)](../../../../visual-basic/reference/command-line-compiler/link.md)   
 [编程概念](../../../../visual-basic/programming-guide/concepts/index.md)   
 [使用程序集编程](http://msdn.microsoft.com/library/25918b15-701d-42c7-95fc-c290d08648d6)   
 [程序集和全局程序集缓存 (Visual Basic)](../../../../visual-basic/programming-guide/concepts/assemblies-gac/index.md)

