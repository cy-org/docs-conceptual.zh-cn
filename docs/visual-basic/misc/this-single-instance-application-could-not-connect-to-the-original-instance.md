---
title: "此单实例应用程序无法连接到原始实例 |Microsoft 文档"
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-visual-basic
ms.topic: article
f1_keywords:
- vbrAppModel_SingleInstanceCantConnect
ms.assetid: 7c2c0cee-02a1-4157-be03-39d18e18408f
caps.latest.revision: 12
author: dotnet-bot
ms.author: dotnetcontent
translation.priority.ht:
- de-de
- es-es
- fr-fr
- it-it
- ja-jp
- ko-kr
- ru-ru
- zh-cn
- zh-tw
translation.priority.mt:
- cs-cz
- pl-pl
- pt-br
- tr-tr
translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 17a3ecd69e0e0974b2a8fc50090097b93dc0def3
ms.lasthandoff: 03/13/2017

---
# <a name="this-single-instance-application-could-not-connect-to-the-original-instance"></a>此单实例应用程序未能连接到原始实例
此单实例应用程序未能连接到原始实例。 一些可能导致此问题的原因包括：  
  
-   原始实例停止了响应。  
  
-   应用程序没有创建内核对象的权限。 有关内核对象的详细信息，请参阅[互斥锁](http://msdn.microsoft.com/library/9dd06e25-12c0-4a9e-855a-452dc83803e2)。  
  
     内核对象的基名称是通过串联程序集的 GUID、主版本号和次版本号得到的。 例如，基名称可能是 `3639f15d-9547-43da-8145-60da347829915.1`。  
  
## <a name="to-correct-this-error-when-developing-the-application"></a>在开发应用程序时更正此错误  
  
1.  检查应用程序未进入未响应状态。  
  
2.  检查应用程序是否具有创建内核对象的足够权限。  
  
3.  重启应用程序的原始实例。  
  
4.  重启计算机，以清除可能正在使用连接到原始实例应用程序所需资源的任何进程。  
  
5.  记录发生错误的环境，并与 Microsoft 产品支持服务联系。  
  
## <a name="see-also"></a>另请参阅  
 [NIB︰ 如何︰ 指定应用程序 (Visual Basic 中) 的实例化行为](http://msdn.microsoft.com/en-us/48539ad8-d960-4210-beab-ee65f6c6dc6e)   
 [调试器基础知识](https://docs.microsoft.com/visualstudio/debugger/debugger-basics)   
 [PAVEOVER 产品支持和可访问性](http://msdn.microsoft.com/en-us/14e1d293-7b6d-40a6-bf3e-a92f8ee6c88c)
