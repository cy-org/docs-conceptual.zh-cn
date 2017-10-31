---
title: "多线程过程的参数和返回值 (C#)"
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
ms.assetid: ba63c30c-d9f0-4962-b5c7-9d83ba851e6a
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
ms.openlocfilehash: 5e377a006409dbae49b3c00297f69e8d55a01295
ms.contentlocale: zh-cn
ms.lasthandoff: 07/28/2017

---
# <a name="parameters-and-return-values-for-multithreaded-procedures-c"></a>多线程过程的参数和返回值 (C#)
在多线程应用程序中提供和返回值是很复杂的，因为必须将对某个过程的引用传递给线程类的构造函数，该过程不带参数也不返回值。 下面几节介绍一些提供参数和从不同线程上的过程返回值的简单方法。  
  
## <a name="supplying-parameters-for-multithreaded-procedures"></a>为多线程过程提供参数  
 为多线程方法调用提供参数的最好办法是将目标方法包装在类中，并为该类定义字段，这些字段将用作新线程的参数。 这种方法的优点是，任何时候想要启动新线程，都可以创建类的新实例，该实例带有自身的参数。 例如，假设有一个计算三角形面积的函数，如以下代码所示：  
  
```csharp  
double CalcArea(double Base, double Height)  
{  
    return 0.5 * Base * Height;  
}  
```  
  
 可以编写一个包装 `CalcArea` 函数的类，并创建一些字段来存储输入参数，如以下所示：  
  
```csharp  
class AreaClass  
{  
    public double Base;  
    public double Height;  
    public double Area;  
    public void CalcArea()  
    {  
        Area = 0.5 * Base * Height;  
        MessageBox.Show("The area is: " + Area.ToString());  
    }  
}  
```  
  
 若要使用 `AreaClass`，可以创建一个 `AreaClass` 对象并设置 `Base` 和 `Height` 属性，如以下代码所示：  
  
```csharp  
protected void TestArea()  
{  
    AreaClass AreaObject = new AreaClass();  
  
    System.Threading.Thread Thread =  
        new System.Threading.Thread(AreaObject.CalcArea);  
    AreaObject.Base = 30;  
    AreaObject.Height = 40;  
    Thread.Start();  
}  
```  
  
 请注意，调用 `CalcArea` 方法后，`TestArea` 过程并不检查 `Area` 字段的值。 `CalcArea` 运行于单独的线程，因此，如果在调用 `Thread.Start` 后立即检查，则无法确定 `Area` 字段已被设置。 下一节讨论从多线程过程返回值的更好方法。  
  
## <a name="returning-values-from-multithreaded-procedures"></a>从多线程过程返回值  
 由于这些过程不能为函数也不能使用 `ByRef` 参数，因而从运行于不同线程的过程返回值是很复杂的。 返回值最简单的方法是：使用 <xref:System.ComponentModel.BackgroundWorker> 组件来管理线程，在任务完成时引发事件，然后用事件处理程序处理结果。  
  
 下面的示例通过从运行于单独线程的某过程引发一个事件来返回值：  
  
```csharp  
class AreaClass2  
{  
    public double Base;  
    public double Height;  
    public double CalcArea()  
    {  
        // Calculate the area of a triangle.  
        return 0.5 * Base * Height;  
    }  
}  
  
private System.ComponentModel.BackgroundWorker BackgroundWorker1  
    = new System.ComponentModel.BackgroundWorker();  
  
private void TestArea2()  
{  
    InitializeBackgroundWorker();  
  
    AreaClass2 AreaObject2 = new AreaClass2();  
    AreaObject2.Base = 30;  
    AreaObject2.Height = 40;  
  
    // Start the asynchronous operation.  
    BackgroundWorker1.RunWorkerAsync(AreaObject2);  
}  
  
private void InitializeBackgroundWorker()  
{  
    // Attach event handlers to the BackgroundWorker object.  
    BackgroundWorker1.DoWork +=  
        new System.ComponentModel.DoWorkEventHandler(BackgroundWorker1_DoWork);  
    BackgroundWorker1.RunWorkerCompleted +=  
        new System.ComponentModel.RunWorkerCompletedEventHandler(BackgroundWorker1_RunWorkerCompleted);  
}  
  
private void BackgroundWorker1_DoWork(  
    object sender,  
    System.ComponentModel.DoWorkEventArgs e)  
{  
    AreaClass2 AreaObject2 = (AreaClass2)e.Argument;  
    // Return the value through the Result property.  
    e.Result = AreaObject2.CalcArea();  
}  
  
private void BackgroundWorker1_RunWorkerCompleted(  
    object sender,  
    System.ComponentModel.RunWorkerCompletedEventArgs e)  
{  
    // Access the result through the Result property.  
    double Area = (double)e.Result;  
    MessageBox.Show("The area is: " + Area.ToString());  
}  
```  
  
 可以通过使用 <xref:System.Threading.ThreadPool.QueueUserWorkItem%2A> 方法的可选 `ByVal` 状态对象变量来向线程池线程提供参数并返回值。 线程计时器线程也支持将状态对象用于此目的。 有关线程池和线程计时器的信息，请参阅[线程池 (C#)](../../../../csharp/programming-guide/concepts/threading/thread-pooling.md) 和[线程计时器 (C#)](../../../../csharp/programming-guide/concepts/threading/thread-timers.md)。  
  
## <a name="see-also"></a>请参阅  
 [演练：利用 BackgroundWorker 组件进行多线程处理 (C#)](../../../../csharp/programming-guide/concepts/threading/walkthrough-multithreading-with-the-backgroundworker-component.md)   
 [线程池 (C#)](../../../../csharp/programming-guide/concepts/threading/thread-pooling.md)   
 [线程同步 (C#)](../../../../csharp/programming-guide/concepts/threading/thread-synchronization.md)   
 [事件](../../../../csharp/programming-guide/events/index.md)   
 [多线程应用程序 (C#)](../../../../csharp/programming-guide/concepts/threading/multithreaded-applications.md)   
 [委托](../../../../csharp/programming-guide/delegates/index.md)   
 [组件中的多线程处理](http://msdn.microsoft.com/library/2fc31e68-fb71-4544-b654-0ce720478779)

