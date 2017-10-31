---
title: "演练：在 Visual Studio 中嵌入托管程序集中的类型 (C#)"
ms.custom: 
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-csharp
ms.topic: article
dev_langs:
- CSharp
ms.assetid: 55ed13c9-c5bb-4bc2-bcd8-0587eb568864
caps.latest.revision: 3
author: BillWagner
ms.author: wiwagn
translation.priority.mt:
- cs-cz
- pl-pl
- pt-br
- tr-tr
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: 7b003e76229a06883adc22f933f08663330f0c9d
ms.contentlocale: zh-cn
ms.lasthandoff: 07/28/2017

---
# <a name="walkthrough-embedding-types-from-managed-assemblies-in-visual-studio-c"></a>演练：在 Visual Studio 中嵌入托管程序集中的类型 (C#)
如果嵌入强命名托管程序集中的类型信息，则可以对应用程序中的类型进行松耦合，以实现版本独立性。 也就是说，可以将程序编写为使用多个托管库版本中的类型，而不必对每个版本重新编译程序。  
  
 类型嵌入经常与 COM 互操作一起使用，例如使用 Microsoft Office 中的自动化对象的应用程序。 通过嵌入类型信息，程序的同一个版本可以处理不同计算机上的不同 Microsoft Office 版本。 但也可以在完全托管的解决方案中使用类型嵌入。  
  
 可从具有以下特征的程序集嵌入类型信息：  
  
-   程序集至少公开一个公共接口。  
  
-   嵌入的接口使用 `ComImport` 特性和 `Guid` 特性（及一个唯一 GUID）进行批注。  
  
-   程序集使用 `ImportedFromTypeLib` 特性或 `PrimaryInteropAssembly` 特性和程序集级别的 `Guid` 特性进行批注。 （默认情况下，Visual C# 项目模板包含程序集级别的 `Guid` 特性。）  
  
 指定可嵌入的公共接口后，可以创建实现这些接口的运行时类。 然后，客户端程序可以通过引用包含这些公共接口的程序集，并将该引用的 `Embed Interop Types` 属性设置为 `True`，在设计时嵌入这些接口的类型信息。 这等效于使用命令行编译器和通过 `/link` 编译器选项引用该程序集。 然后，客户端程序可以加载类型化为这些接口的运行时对象的实例。 如果创建新版本的强命名运行时程序集，则不必使用更新的运行时程序集来重新编译客户端程序。 客户端程序将使用公共接口的嵌入类型信息，从而继续使用任何可用的运行时程序集版本。  
  
 由于类型嵌入的主要功能是提供对 COM 互操作程序集中类型信息的嵌入的支持，因此以下限制在将类型信息嵌入完全托管解决方案中时适用：  
  
-   仅嵌入特定于 COM 互操作的特性；忽略其他特性。  
  
-   如果一个类型使用泛型参数且泛型参数的类型是嵌入类型，则不能跨程序集边界使用该类型。 跨程序集边界的示例包括从另一个程序集调用方法或从另一个程序集中定义的类型派生类型。  
  
-   不嵌入常量。  
  
-   <xref:System.Collections.Generic.Dictionary%602?displayProperty=fullName> 类不支持将嵌入类型作为密钥。 可以实现自己的字典类型以支持将嵌入类型作为密钥。  
  
 本演练中将执行以下操作：  
  
-   创建一个强命名程序集，它具有包含可嵌入类型信息的公共接口。  
  
-   创建一个实现该公共接口的强命名运行时程序集。  
  
-   创建一个客户端程序，该程序嵌入公共接口中的类型信息，并创建运行时程序集中的类的实例。  
  
-   修改并重新生成运行时程序集。  
  
-   运行客户端程序，查看正在使用的运行时程序集新版本，而不必重新编译该客户端程序。  
  
[!INCLUDE[note_settings_general](~/includes/note-settings-general-md.md)]  
  
## <a name="creating-an-interface"></a>创建接口  
  
#### <a name="to-create-the-type-equivalence-interface-project"></a>创建类型等效性接口项目  
  
1.  在 Visual Studio 中的“文件”菜单上，选择“新建”，然后单击“项目”。  
  
2.  在“新建项目”对话框的“项目类型”窗格中，确保选中“Windows”。 在“模板”窗格中，选择“类库”。 在“名称”框中，键入 `TypeEquivalenceInterface`，然后单击“确定”。 新项目创建完成。  
  
3.  在“解决方案资源管理器”中，右键单击 Class1.cs 文件，然后单击“重命名”。 将文件重命名为 `ISampleInterface.cs`，然后按 Enter。 重命名文件也会将类重命名为 `ISampleInterface`。 此类将表示类的公共接口。  
  
4.  右键单击 TypeEquivalenceInterface 项目，然后单击“属性”。 单击“生成”选项卡。 将输出路径设置为开发计算机上的有效位置，例如 `C:\TypeEquivalenceSample`。 本演练的后续步骤中也将使用此位置。  
  
5.  在编辑项目属性期间，单击“签名”选项卡。 选择“为程序集签名”选项。 在“选择强名称密钥文件”列表中，单击“<新建…>”。 在“密钥文件名”框中，键入 `key.snk`。 清除“使用密码保护密钥文件”复选框。 单击“确定”。  
  
6.  打开 ISampleInterface.cs 文件。 将以下代码添加到 ISampleInterface 类文件，以创建 ISampleInterface 接口。  
  
    ```csharp  
    using System;  
    using System.Runtime.InteropServices;  
  
    namespace TypeEquivalenceInterface  
    {  
        [ComImport]  
        [Guid("8DA56996-A151-4136-B474-32784559F6DF")]  
        public interface ISampleInterface  
        {  
            void GetUserInput();  
            string UserInput { get; }  
        }  
    }  
    ```  
  
7.  在“工具”菜单上，单击“创建 Guid”。 在“创建 GUID”对话框中，单击“注册表格式”，然后单击“复制”。 单击“退出” 。  
  
8.  在 `Guid` 特性中，删除示例 GUID ，并粘贴从“创建 GUID”对话框复制的 GUID。 删除复制的 GUID 中的大括号 ({})。  
  
9. 在“解决方案资源管理器”中，展开“属性”文件夹。 双击 AssemblyInfo.cs 文件。 向文件中添加以下特性。  
  
    ```csharp  
    [assembly: ImportedFromTypeLib("")]  
    ```  
  
     保存该文件。  
  
10. 保存项目。  
  
11. 右键单击 TypeEquivalenceInterface 项目，然后单击“生成”。 此时将编译类库 .dll 文件，并保存到指定的生成输出路径中（如 C:\TypeEquivalenceSample）。  
  
## <a name="creating-a-runtime-class"></a>创建运行时类  
  
#### <a name="to-create-the-type-equivalence-runtime-project"></a>创建类型等效性运行时项目  
  
1.  在 Visual Studio 中的“文件”菜单上，指向“新建”，然后单击“项目”。  
  
2.  在“新建项目”对话框的“项目类型”窗格中，确保选中“Windows”。 在“模板”窗格中，选择“类库”。 在“名称”框中，键入 `TypeEquivalenceRuntime`，然后单击“确定”。 新项目创建完成。  
  
3.  在“解决方案资源管理器”中，右键单击 Class1.cs 文件，然后单击“重命名”。 将文件重命名为 `SampleClass.cs`，然后按 Enter。 重命名文件也会将类重命名为 `SampleClass`。 此类将实现 `ISampleInterface` 接口。  
  
4.  右键单击 TypeEquivalenceRuntime 项目，然后单击“属性”。 单击“生成”选项卡。 将输出路径设置为 TypeEquivalenceInterface 项目中所用的同一位置，例如，`C:\TypeEquivalenceSample`。  
  
5.  在编辑项目属性期间，单击“签名”选项卡。 选择“为程序集签名”选项。 在“选择强名称密钥文件”列表中，单击“<新建…>”。 在“密钥文件名”框中，键入 `key.snk`。 清除“使用密码保护密钥文件”复选框。 单击“确定”。  
  
6.  右键单击 TypeEquivalenceRuntime 项目，然后单击“添加引用”。 单击“浏览”选项卡，然后浏览到输出路径文件夹。 选择 TypeEquivalenceInterface.dll 文件并单击“确定”。  
  
7.  在“解决方案资源管理器”中，展开“引用”文件夹。 选择 TypeEquivalenceInterface 引用。 在 TypeEquivalenceInterface 引用的“属性”窗口中，将“特定版本”属性设置为“False”。  
  
8.  将以下代码添加到 SampleClass 类文件，以创建 SampleClass 类。  
  
    ```csharp  
    using System;  
    using System.Collections.Generic;  
    using System.Linq;  
    using System.Text;  
    using TypeEquivalenceInterface;  
  
    namespace TypeEquivalenceRuntime  
    {  
        public class SampleClass : ISampleInterface  
        {  
            private string p_UserInput;  
            public string UserInput { get { return p_UserInput; } }  
  
            public void GetUserInput()  
            {  
                Console.WriteLine("Please enter a value:");  
                p_UserInput = Console.ReadLine();  
            }  
        }  
    )  
    ```  
  
9. 保存项目。  
  
10. 右键单击 TypeEquivalenceRuntime 项目，然后单击“生成”。 此时将编译类库 .dll 文件，并保存到指定的生成输出路径中（如 C:\TypeEquivalenceSample）。  
  
## <a name="creating-a-client-project"></a>创建客户端项目  
  
#### <a name="to-create-the-type-equivalence-client-project"></a>创建类型等效性客户端项目  
  
1.  在 Visual Studio 中的“文件”菜单上，指向“新建”，然后单击“项目”。  
  
2.  在“新建项目”对话框的“项目类型”窗格中，确保选中“Windows”。 在“模板”窗格中，选择“控制台应用程序”。 在“名称”框中，键入 `TypeEquivalenceClient`，然后单击“确定”。 新项目创建完成。  
  
3.  右键单击 TypeEquivalenceClient 项目，然后单击“属性”。 单击“生成”选项卡。 将输出路径设置为 TypeEquivalenceInterface 项目中所用的同一位置，例如，`C:\TypeEquivalenceSample`。  
  
4.  右键单击 TypeEquivalenceClient 项目，然后单击“添加引用”。 单击“浏览”选项卡，然后浏览到输出路径文件夹。 选择 TypeEquivalenceInterface.dll 文件（不是 TypeEquivalenceRuntime.dll）并单击“确定”。  
  
5.  在“解决方案资源管理器”中，展开“引用”文件夹。 选择 TypeEquivalenceInterface 引用。 在 TypeEquivalenceInterface 引用的“属性”窗口中，将“嵌入互操作类型”属性设置为“True”。  
  
6.  将以下代码添加到 Program.cs 文件，以创建客户端程序。  
  
    ```csharp  
    using System;  
    using System.Collections.Generic;  
    using System.Linq;  
    using System.Text;  
    using TypeEquivalenceInterface;  
    using System.Reflection;  
  
    namespace TypeEquivalenceClient  
    {  
        class Program  
        {  
            static void Main(string[] args)  
            {  
                Assembly sampleAssembly = Assembly.Load("TypeEquivalenceRuntime");  
                ISampleInterface sampleClass =   
                    (ISampleInterface)sampleAssembly.CreateInstance("TypeEquivalenceRuntime.SampleClass");  
                sampleClass.GetUserInput();  
                Console.WriteLine(sampleClass.UserInput);  
                Console.WriteLine(sampleAssembly.GetName().Version.ToString());  
                Console.ReadLine();  
            }  
        }  
    }  
    ```  
  
7.  按 Ctrl+F5 生成并运行程序。  
  
## <a name="modifying-the-interface"></a>修改接口  
  
#### <a name="to-modify-the-interface"></a>修改接口  
  
1.  在 Visual Studio 中的“文件”菜单上，指向“打开”，然后单击“项目/解决方案”。  
  
2.  在“打开项目”对话框中，右键单击 TypeEquivalenceInterface 项目，然后单击“属性”。 单击“应用程序”  选项卡。 单击“程序集信息”按钮。 将“程序集版本”和“文件版本”的值更改为 `2.0.0.0`。  
  
3.  打开 SampleInterface.cs 文件。 将以下代码行添加到 ISampleInterface 接口。  
  
    ```csharp  
    DateTime GetDate();  
    ```  
  
     保存该文件。  
  
4.  保存项目。  
  
5.  右键单击 TypeEquivalenceInterface 项目，然后单击“生成”。 此时将编译新版本的类库 .dll 文件，并保存到指定的生成输出路径中（如 C:\TypeEquivalenceSample）。  
  
## <a name="modifying-the-runtime-class"></a>修改运行时类  
  
#### <a name="to-modify-the-runtime-class"></a>修改运行时类  
  
1.  在 Visual Studio 中的“文件”菜单上，指向“打开”，然后单击“项目/解决方案”。  
  
2.  在“打开项目”对话框中，右键单击 TypeEquivalenceRuntime 项目，然后单击“属性”。 单击“应用程序”  选项卡。 单击“程序集信息”按钮。 将“程序集版本”和“文件版本”的值更改为 `2.0.0.0`。  
  
3.  打开 SampleClass.cs 文件。 将以下代码行添加到 SampleClass 类。  
  
    ```csharp  
    public DateTime GetDate()  
    {  
        return DateTime.Now;  
    }  
    ```  
  
     保存该文件。  
  
4.  保存项目。  
  
5.  右键单击 TypeEquivalenceRuntime 项目，然后单击“生成”。 此时将编译更新版本的类库 .dll 文件，并保存到之前指定的生成输出路径中（如 C:\TypeEquivalenceSample）。  
  
6.  在文件资源管理器中，打开输出路径文件夹（如 C:\TypeEquivalenceSample）。 双击 TypeEquivalenceClient.exe 运行该程序。 程序将反映 TypeEquivalenceRuntime 程序集的未经重新编译的新版本。  
  
## <a name="see-also"></a>请参阅  
 [/link（C# 编译器选项）](../../../../csharp/language-reference/compiler-options/link-compiler-option.md)   
 [C# 编程指南](../../../../csharp/programming-guide/index.md)   
 [使用程序集编程](../../../../framework/app-domains/programming-with-assemblies.md)   
 [程序集和全局程序集缓存 (C#)](../../../../csharp/programming-guide/concepts/assemblies-gac/index.md)

