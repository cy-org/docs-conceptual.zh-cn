---
title: "如何：异步调用 Web 服务 (Visual Basic)"
ms.date: 2015-07-20
ms.prod: .net
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
dev_langs:
- VB
helpviewer_keywords:
- asynchronous calls
- Web services, accessing
ms.assetid: ff8046f4-f1f2-4d8b-90b7-95e3f7415418
caps.latest.revision: 14
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
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: f191ccb5f42f9cfc5dc4e44e58d2338422207aa1
ms.contentlocale: zh-cn
ms.lasthandoff: 07/28/2017

---
# <a name="how-to-call-a-web-service-asynchronously-visual-basic"></a>如何：异步调用 Web 服务 (Visual Basic)
此示例在 Web 服务的异步处理程序事件中附加了一个处理程序，以便它能检索异步方法调用的结果。 此示例使用了 DemoTemperatureService Web 服务（位于 http://www.xmethods.net。  
  
 当你在 [!INCLUDE[vsprvs](~/includes/vsprvs-md.md)] 集成开发环境 (IDE) 中引用项目中的 Web 服务时，该服务将添加到 `My.WebServices` 对象中，并且 IDE 将生成一个客户端代理类来访问指定的 Web 服务  
  
 使用此代理类可以同步调用 Web 服务方法，而应用程序则在 Web 服务方法内等待函数执行完成。 另外，代理还创建其他成员来协助异步调用方法。 对于每一个 Web 服务函数（*NameOfWebServiceFunction*），代理都会创建一个 *NameOfWebServiceFunction*`Async` 子例程、一个 *NameOfWebServiceFunction*`Completed` 事件和一个 *NameOfWebServiceFunction*`CompletedEventArgs` 类。 此示例演示如何使用异步成员访问 DemoTemperatureService Web 服务的 `getTemp` 函数。  
  
> [!NOTE]
>  因为 ASP.NET 不支持 `My.WebServices` 对象，所以这段代码不适用于 Web 应用程序。  
  
### <a name="to-call-a-web-service-asynchronously"></a>以异步方式调用 Web 服务  
  
1.  请参考 DemoTemperatureService Web 服务（位于 http://www.xmethods.net）。 网址为  
  
    ```  
    http://www.xmethods.net/sd/2001/DemoTemperatureService.wsdl  
    ```  
  
2.  为 `getTempCompleted` 事件添加事件处理程序：  
  
    ```  
    Private Sub getTempCompletedHandler(ByVal sender As Object,   
        ByVal e As net.xmethods.www.getTempCompletedEventArgs)  
  
        MsgBox("Temperature: " & e.Result)  
    End Sub  
    ```  
  
    > [!NOTE]
    >  不能使用 `Handles` 语句将事件处理程序与 `My.WebServices` 对象的事件关联起来。  
  
3.  如果已将事件处理程序添加到 `getTempCompleted` 事件，则添加要跟踪的字段：  
  
    ```  
    Private handlerAttached As Boolean = False  
    ```  
  
4.  添加一个方法，以将事件处理程序添加到 `getTempCompleted` 事件（如有必要）并调用 `getTempAsynch` 方法：  
  
    ```  
    Sub CallGetTempAsync(ByVal zipCode As Integer)  
        If Not handlerAttached Then  
            AddHandler My.WebServices.  
                TemperatureService.getTempCompleted,   
                AddressOf Me.TS_getTempCompleted  
            handlerAttached = True  
        End If  
        My.WebServices.TemperatureService.getTempAsync(zipCode)  
    End Sub  
    ```  
  
     若要以异步方式调用 `getTemp` Web 方法，请调用 `CallGetTempAsync` 方法。 当 Web 方法执行完成后，其返回值将被传递到 `getTempCompletedHandler` 事件处理程序。  
  
## <a name="see-also"></a>请参阅  
 [访问应用程序 Web 服务](../../../visual-basic/developing-apps/programming/accessing-application-web-services.md)   
 [My.WebServices 对象](../../../visual-basic/language-reference/objects/my-webservices-object.md)

