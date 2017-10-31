---
title: "用 COM 互操作对数据进行封送处理"
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
- COM interop, data marshaling
- marshaling data, COM interop
ms.assetid: 0bcdd7bf-5026-43eb-b08b-f03f90db9df9
caps.latest.revision: 12
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: 7e798f41f7c770fb0db0abf4a07e53cbaa6ccb40
ms.contentlocale: zh-cn
ms.lasthandoff: 08/21/2017

---
# <a name="marshaling-data-with-com-interop"></a>用 COM 互操作对数据进行封送处理
COM 互操作同时对在托管代码中使用 COM 对象和向 COM 公开托管对象提供支持。 对于将数据封送到 COM 和从 COM 中封送数据的支持是广泛的，并几乎总是提供正确的封送行为。  
  
 [!INCLUDE[winsdklong](../../../includes/winsdklong-md.md)] 包括以下 COM 互操作工具：  
  
-   [类型库导入程序 (Tlbimp.exe)](../../../docs/framework/tools/tlbimp-exe-type-library-importer.md)，它将 COM 类型库转换为互操作程序集。 从该程序集中，互操作封送处理服务生成包装器，该包装器在托管内存和非托管内存之间执行数据封送。  
  
-   [类型库导出程序 (Tlbexp.exe)](../../../docs/framework/tools/tlbexp-exe-type-library-exporter.md)，它从程序集产生 COM 类型库，并生成在方法调用期间执行封送的包装器。  
  
 本节描述在能够（或必须）为封送拆收器提供附加类型信息时自定义互操作包装器的过程。  
  
## <a name="in-this-section"></a>本节内容  
 [COM 数据类型](http://msdn.microsoft.com/en-us/f93ae35d-a416-4218-8700-c8218cc90061)  
 提供相应的托管和非托管数据类型。  
  
 [自定义 COM 可调用包装器](http://msdn.microsoft.com/en-us/825177d3-4b2c-4723-82be-ce6ca2c34ace)  
 描述如何在设计时使用 MarshalAsAttribute 属性显式封送数据类型。  
  
 [自定义运行时可调用包装器](http://msdn.microsoft.com/en-us/4652beaf-77d0-4f37-9687-ca193288c0be)  
 描述如何调整互操作程序集中类型的封送行为以及如何以手动方式定义 COM 类型。  
  
 [如何：将托管代码 DCOM 迁移到 WCF](../../../docs/framework/interop/how-to-migrate-managed-code-dcom-to-wcf.md)  
 描述如何将托管 DCOM 代码迁移到 WCF，得到最安全的解决方案。  
  
## <a name="related-sections"></a>相关章节  
 [高级 COM 互操作性](http://msdn.microsoft.com/en-us/3ada36e5-2390-4d70-b490-6ad8de92f2fb)  
 提供一些链接，指向关于将 COM 组件并入 .NET Framework 应用程序中的详细信息。  
  
 [有关从程序集转换到类型库的摘要](http://msdn.microsoft.com/en-us/3a37eefb-a76c-4000-9080-7dbbf66a4896)  
 描述从程序集到类型库的导出转换过程。  
  
 [有关从类型库转换到程序集的摘要](http://msdn.microsoft.com/en-us/bf3f90c5-4770-4ab8-895c-3ba1055cc958)  
 描述从类型库到程序集的导入转换过程。  
  
 [使用泛型类型进行交互操作](http://msdn.microsoft.com/en-us/26b88e03-085b-4b53-94ba-a5a9c709ce58)  
 描述在使用用于 COM 互操作性的泛型类型时，哪些操作受支持。

