---
title: "因为无法获得单个实例启动所需的操作系统资源出现意外的错误 |Microsoft 文档"
ms.date: 2015-07-20
ms.prod: .net
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
f1_keywords:
- vbrAppModel_CantGetMemoryMappedFile
dev_langs:
- VB
ms.assetid: 0d9f2a30-ff72-4355-8060-744f22339359
caps.latest.revision: 10
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
ms.openlocfilehash: 44432a2c393abb01141d09cf5f28c6fd29c5bc43
ms.lasthandoff: 03/13/2017

---
# <a name="an-unexpected-error-has-occurred-because-an-operating-system-resource-required-for-single-instance-startup-cannot-be-acquired"></a>发生错误，因为无法获得单个实例启动所需的操作系统资源
应用程序未能获取所需的操作系统资源。 一些可能导致此问题的原因是：  
  
-   应用程序不具备创建命名操作系统对象的权限。  
  
-   公共语言运行时不具备创建内存映射文件的权限。  
  
-   应用程序需要访问某个操作系统对象，但另一个进程正在使用该对象。  
  
## <a name="to-correct-this-error"></a>更正此错误  
  
1.  检查该应用程序具有创建命名操作系统对象的足够权限。  
  
2.  检查公共语言运行时具有创建内存映射文件的足够权限。  
  
3.  重新启动计算机以清除可能正使用连接到原始实例应用程序所需的资源的任何进程。  
  
4.  记录发生错误的环境，并与 Microsoft 产品支持服务联系  
  
## <a name="see-also"></a>另请参阅  
 [应用程序页、项目设计器 (Visual Basic)](https://docs.microsoft.com/visualstudio/ide/reference/application-page-project-designer-visual-basic)   
 [调试器基础知识](https://docs.microsoft.com/visualstudio/debugger/debugger-basics)   
 [与我们交流](https://docs.microsoft.com/visualstudio/ide/talk-to-us)
