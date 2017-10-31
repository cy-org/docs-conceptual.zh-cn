---
title: "如何：创建 COM 包装"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology:
- dotnet-clr
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- COM,wrappers creating
- COM,wrappers Visual Studio
ms.assetid: bdf89bea-1623-45ee-a57b-cf7c90395efa
caps.latest.revision: 12
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: e99b084ddb565a8ae00ee917eaf7fca2c659ab64
ms.contentlocale: zh-cn
ms.lasthandoff: 08/21/2017

---
# <a name="how-to-create-com-wrappers"></a>如何：创建 COM 包装
可以通过使用 [!INCLUDE[vsprvsext](../../../includes/vsprvsext-md.md)] 功能或 .NET Framework 工具 Tlbimp.exe 和 Regasm.exe 创建组件对象模型 (COM) 包装器。 这两种方法都会生成两种类型的 COM 包装器：  
  
-   从类型库中生成一个[运行时可调用包装器](../../../docs/framework/interop/runtime-callable-wrapper.md)以在托管代码中运行 COM 对象。  
  
-   生成具有所需注册表设置的一个 [COM 可调用包装器](../../../docs/framework/interop/com-callable-wrapper.md)以在本机应用程序中运行托管对象。  
  
 在 [!INCLUDE[vsprvslong](../../../includes/vsprvslong-md.md)] 中，可以将 COM 包装器作为引用添加到项目中。  
  
## <a name="wrapping-com-objects-in-a-managed-application"></a>在托管应用程序中包装 COM 对象  
  
#### <a name="to-create-a-runtime-callable-wrapper-using-visual-studio"></a>使用 Visual Studio 创建运行时可调用包装器  
  
1.  打开托管应用程序的项目。  
  
2.  在“项目”菜单上，单击“显示所有文件”。  
  
3.  在“项目”菜单上，单击“添加引用”。  
  
4.  在“添加引用”对话框中，单击“COM”选项卡，选择要使用的组件，然后单击“确定”。  
  
     在“解决方案资源管理器”中检查 COM 组件是否已添加到项目的“引用”文件夹中。  
  
 现在可以编写代码以访问 COM 对象。 可以从通过声明对象开始，如使用适用于 [!INCLUDE[vbprvblong](../../../includes/vbprvblong-md.md)] 的 `Imports` 语句或适用于 [!INCLUDE[csprcslong](../../../includes/csprcslong-md.md)] 的 `Using` 语句。  
  
> [!NOTE]
>  如果要编写 Microsoft Office 组件的程序，请首先从 Microsoft 下载中心安装 [Microsoft Office 主互操作程序集](http://go.microsoft.com/fwlink/?LinkId=50479) (PIA)。 在步骤 4 中，为所需的 Office 产品选择可用的最新版本的对象库，如 Microsoft Word 11.0 对象库。  
  
#### <a name="to-create-a-runtime-callable-wrapper-using-net-framework-tools"></a>使用 .NET Framework 工具创建运行时可调用包装器  
  
-   运行 [Tlbimp.exe（类型库导入程序）](../../../docs/framework/tools/tlbimp-exe-type-library-importer.md)工具。  
  
 此工具为在原始类型库中定义的类型创建包含运行时元数据的程序集。  
  
## <a name="wrapping-managed-objects-in-a-native-application"></a>在本机应用程序中包装托管对象  
  
#### <a name="to-create-a-com-callable-wrapper-using-visual-studio"></a>使用 Visual Studio 创建 COM 可调用包装器  
  
1.  为要在本机代码中运行的托管类创建类库项目。 此类必须具有默认的构造函数。  
  
     在 AssemblyInfo 文件中验证程序集是否具有由四部分构成的完整版本号。 在 Windows 注册表中维护版本控制需要此版本号。 有关版本号的详细信息，请参阅[程序集版本控制](../../../docs/framework/app-domains/assembly-versioning.md)。  
  
2.  在“项目”菜单上，单击“属性”。  
  
3.  单击“编译”选项卡。  
  
4.  选择“为 COM 互操作注册”复选框。  
  
 生成项目时，将自动为 COM 互操作注册程序集。 如果要在 [!INCLUDE[vsprvslong](../../../includes/vsprvslong-md.md)] 中生成本机应用程序，可以通过单击“项目”菜单上的“添加引用”来使用此程序集。  
  
#### <a name="to-create-a-com-callable-wrapper-using-net-framework-tools"></a>使用 .NET Framework 工具创建 COM 可调用包装器  
  
-   运行 [Regasm.exe（程序集注册工具）](../../../docs/framework/tools/regasm-exe-assembly-registration-tool.md)工具。  
  
 此工具读取程序集元数据，并向注册表添加所需的项。 这样，使 COM 客户端可以透明方式创建 .NET Framework 类。 可以像使用本机 COM 类一样可以使用此程序集。  
  
 可以在任何目录中的程序集上运行 Regasm.exe，然后运行 [Gacutil.exe（全局程序集缓存工具）](../../../docs/framework/tools/gacutil-exe-gac-tool.md)以将其移动到全局程序集缓存中。 移动此程序集不会使位置注册表项失效，因为如果未在其他位置找到此程序集，则会始终对全局程序集缓存进行检查。  
  
## <a name="see-also"></a>另请参阅  
 [运行时可调用包装器](../../../docs/framework/interop/runtime-callable-wrapper.md)   
 [COM 可调用包装器](../../../docs/framework/interop/com-callable-wrapper.md)

