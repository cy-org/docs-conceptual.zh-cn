---
title: "如何：实现接口事件（C# 编程指南）"
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
dev_langs:
- CSharp
helpviewer_keywords:
- interfaces [C#], event implementation in classes
- events [C#], in interfaces
ms.assetid: 63527447-9535-4880-8e95-35e2075827df
caps.latest.revision: 21
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
ms.openlocfilehash: 8f8460674aa59170cf75eb2fa93e9d232df07e5e
ms.contentlocale: zh-cn
ms.lasthandoff: 07/28/2017

---
# <a name="how-to-implement-interface-events-c-programming-guide"></a>如何：实现接口事件（C# 编程指南）
[接口](../../../csharp/language-reference/keywords/interface.md)可以声明[事件](../../../csharp/language-reference/keywords/event.md)。 下面的示例演示如何在类中实现接口事件。 这些规则基本上都与实现任何接口方法或属性时的相同。  
  
### <a name="to-implement-interface-events-in-a-class"></a>在类中实现接口事件  
  
-   在类中声明事件，然后在相应区域中调用它。  
  
    ```  
    namespace ImplementInterfaceEvents  
    {  
        public interface IDrawingObject  
        {  
            event EventHandler ShapeChanged;  
        }  
        public class MyEventArgs : EventArgs   
        {  
            // class members  
        }  
        public class Shape : IDrawingObject  
        {  
            public event EventHandler ShapeChanged;  
            void ChangeShape()  
            {  
                // Do something here before the event…  
  
                OnShapeChanged(new MyEventArgs(/*arguments*/));  
  
                // or do something here after the event.   
            }  
            protected virtual void OnShapeChanged(MyEventArgs e)  
            {  
                if(ShapeChanged != null)  
                {  
                   ShapeChanged(this, e);  
                }  
            }  
        }  
  
    }  
    ```  
  
## <a name="example"></a>示例  
 下面的示例演示如何处理不太常见的情况：类继承自两个或多个接口，且每个接口都具有相同名称的事件。 在这种情况下，你必须为至少其中一个事件提供显式接口实现。 为事件编写显式接口实现时，还必须编写 `add` 和 `remove` 事件访问器。 通常这些访问器由编译器提供，但在这种情况下编译器不提供它们。  
  
 通过提供自己的访问器，可以指定两个事件是由类中的同一个事件表示，还是由不同事件表示。 例如，如果根据接口规范应在不同时间引发事件，可以在类中将每个事件与单独实现关联。 在下面的示例中，订阅服务器确定它们通过将形状引用转换为 `IShape` 或 `IDrawingObject` 接收哪个 `OnDraw` 事件。  
  
 [!code-cs[csProgGuideEvents#10](../../../csharp/programming-guide/events/codesnippet/CSharp/how-to-implement-interface-events_1.cs)]  
  
## <a name="see-also"></a>另请参阅  
 [C# 编程指南](../../../csharp/programming-guide/index.md)   
 [事件](../../../csharp/programming-guide/events/index.md)   
 [委托](../../../csharp/programming-guide/delegates/index.md)   
 [显式接口实现](../../../csharp/programming-guide/interfaces/explicit-interface-implementation.md)   
 [如何：在派生类中引发基类事件](../../../csharp/programming-guide/events/how-to-raise-base-class-events-in-derived-classes.md)

