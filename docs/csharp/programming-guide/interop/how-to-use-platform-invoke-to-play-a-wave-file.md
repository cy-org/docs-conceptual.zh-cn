---
title: "如何：使用平台调用播放波形文件（C# 编程指南）"
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
dev_langs:
- CSharp
helpviewer_keywords:
- platform invoke, sound files
- interoperability [C#], playing WAV files using pinvoke
- wav files
- .wav files
ms.assetid: f7f62f53-e026-4c40-b221-3a26adb0c2c5
caps.latest.revision: 30
author: BillWagner
ms.author: wiwagn
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
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: 001236392d2b3d3c70dbd0faf2a899929dfe8625
ms.contentlocale: zh-cn
ms.lasthandoff: 07/28/2017

---
# <a name="how-to-use-platform-invoke-to-play-a-wave-file-c-programming-guide"></a>如何：使用平台调用播放波形文件（C# 编程指南）
下面的 C# 代码示例说明了如何使用平台调用服务在 Windows 操作系统中播放波形声音文件。  
  
## <a name="example"></a>示例  
 此示例代码使用 `DllImport` 将 `winmm.dll` 的 `PlaySound` 方法入口点导入为 `Form1 PlaySound()`。 本示例具有一个带按钮的简单 Windows 窗体。 单击该按钮将打开一个标准的 Windows <xref:System.Windows.Forms.OpenFileDialog> 对话框，以便你可以打开要播放的文件。 选中波形文件后，该文件将使用 winmm.DLL 程序集方法的 `PlaySound()` 方法播放。 有关 winmm.dll 的 `PlaySound` 方法的详细信息，请参阅[使用 PlaySound 功能处理波形音频文件](http://go.microsoft.com/fwlink/?LinkId=148553)。 浏览并选择具有 .wav 扩展名的文件，然后单击“打开”以使用平台调用播放波形文件。 文本框中显示所选文件的完整路径。  
  
 通过筛选器设置对“打开文件”对话框进行筛选，以仅显示扩展名为 .wav 的文件：  
  
 [!code-cs[csProgGuideInterop#5](../../../csharp/programming-guide/interop/codesnippet/CSharp/how-to-use-platform-invoke-to-play-a-wave-file_1.cs)]  
  
 [!code-cs[csProgGuideInterop#3](../../../csharp/programming-guide/interop/codesnippet/CSharp/how-to-use-platform-invoke-to-play-a-wave-file_2.cs)]  
  
## <a name="compiling-the-code"></a>编译代码  
  
### <a name="to-compile-the-code"></a>编译代码  
  
1.  在 Visual Studio 中创建新的 C# Windows 应用程序项目，然后将其命名为“WinSound”。  
  
2.  复制上面的代码，然后将其粘贴到 `Form1.cs` 文件的内容上。  
  
3.  复制以下代码，然后用 `InitializeComponent()` 方法将其粘贴到 `Form1.Designer.cs` 文件中任何现有代码之后。  
  
     [!code-cs[csProgGuideInterop#4](../../../csharp/programming-guide/interop/codesnippet/CSharp/how-to-use-platform-invoke-to-play-a-wave-file_3.cs)]  
  
4.  编译并运行该代码。  
  
## <a name="net-framework-security"></a>.NET Framework 安全性  
 有关详细信息，请参阅 [.NET Framework 安全性](http://go.microsoft.com/fwlink/?LinkId=37122)。  
  
## <a name="see-also"></a>另请参阅  
 [C# 编程指南](../../../csharp/programming-guide/index.md)   
 [互操作性概述](../../../csharp/programming-guide/interop/interoperability-overview.md)   
 [互操作性概述](../../../csharp/programming-guide/interop/interoperability-overview.md)   
 [平台调用详解](http://msdn.microsoft.com/en-us/ba9dd55b-2eaa-45cd-8afd-75cb8d64d243)   
 [用平台调用封送数据](../../../framework/interop/marshaling-data-with-platform-invoke.md)

