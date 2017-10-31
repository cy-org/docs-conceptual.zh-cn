---
title: "扩展 Visual Basic 中的我 Namespace |Microsoft 文档"
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-visual-basic
ms.topic: article
f1_keywords:
- vb.AddingMyExtensions
dev_langs:
- VB
helpviewer_keywords:
- My namespace, customizing
- My namespace
- My namespace, extending
ms.assetid: 808e8617-b01c-4135-8b21-babe87389e8e
caps.latest.revision: 13
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
ms.openlocfilehash: 1d1e957536f35b81a9672994c9d4d261afb764ea
ms.lasthandoff: 03/13/2017

---
# <a name="extending-the-my-namespace-in-visual-basic"></a>扩展 Visual Basic 中的 My 命名空间
`My`在 Visual Basic 中的命名空间公开的属性和方法，使您能够轻松地利用.NET Framework 的强大功能。 `My`命名空间简化了常见编程问题，通常为单行代码可将一个困难的任务。 此外，`My`命名空间可完全扩展，以便您可以自定义的行为`My`并将新的服务添加到其层次结构，以适应特定的应用程序需求。 本主题将讨论如何自定义的现有成员`My`命名空间以及如何将添加到您自己自定义类`My`命名空间。  
  
 **主题内容**  
  
-   [自定义现有我 Namespace 成员](#customizing)  
  
-   [将成员添加到 My 对象](#addingtoobjects)  
  
-   [自定义将对象添加到我 Namespace](#addingcustom)  
  
-   [将成员添加到我 Namespace](#addingtonamespace)  
  
-   [将事件添加到自定义 My 对象](#addingevents)  
  
-   [设计指南](#design)  
  
-   [设计的类库我](#designing)  
  
-   [打包和部署扩展](#packaging)  
  
##  <a name="customizing"></a>自定义现有我 Namespace 成员  
 `My`命名空间中 Visual Basic 公开经常使用您的应用程序、 您的计算机，和更多相关信息。 有关中的对象的完整列表`My`命名空间，请参阅[我引用](../../../visual-basic/language-reference/keywords/my-reference.md)。 你可能需要自定义的现有成员`My`命名空间，以便他们更好地匹配您的应用程序的需求。 中的某个对象的任何属性`My`命名空间不是只读的可以设置为自定义值。  
  
 例如，假定您经常使用`My.User`对象来访问当前安全上下文运行您的应用程序的用户。 但是，您的公司使用自定义用户对象公开的其他信息和公司内部用户的功能。 在此方案中，可以将默认值为`My.User.CurrentPrincipal`与您自己自定义主体对象，如下面的示例中所示的一个实例的属性。  
  
 [!code-vb[VbVbcnExtendingMy #&1;](../../../visual-basic/developing-apps/customizing-extending-my/codesnippet/VisualBasic/extending-the-my-namespace_1.vb)]  
  
 设置`CurrentPrincipal`属性`My.User`对象更改应用程序运行所依据的标识。 `My.User`对象，就会返回有关新指定的用户的信息。  
  
##  <a name="addingtoobjects"></a>将成员添加到 My 对象  
 从返回的类型`My.Application`和`My.Computer`被定义为`Partial`类。 因此，您可以扩展`My.Application`和`My.Computer`对象通过创建`Partial`类名为`MyApplication`或`MyComputer`。 此类不能为`Private`类。 如果您指定类的一部分`My`命名空间中，您可以添加属性和方法，将包含在`My.Application`或`My.Computer`对象。  
  
 例如，下面的示例添加一个名为属性`DnsServerIPAddresses`到`My.Computer`对象。  
  
 [!code-vb[VbVbcnExtendingMy #&2;](../../../visual-basic/developing-apps/customizing-extending-my/codesnippet/VisualBasic/extending-the-my-namespace_2.vb)]  
  
##  <a name="addingcustom"></a>自定义将对象添加到我 Namespace  
 尽管`My`命名空间提供了许多常见编程任务的解决方案，您可能会遇到的任务，`My`命名空间不能解决。 例如，您的应用程序可能会访问用户数据的自定义目录服务或应用程序可能会使用默认情况下，使用 Visual Basic 不安装的程序集。 您可以扩展`My`命名空间以包含到一些特定于您的环境的常见任务的自定义解决方案。 `My`命名空间可以轻松地扩展以添加新成员，以满足不断增长的应用程序需求。 此外，您可以将部署您`My`给其他开发人员为 Visual Basic 模板的命名空间扩展。  
  
###  <a name="addingtonamespace"></a>将成员添加到我 Namespace  
 因为`My`是一个命名空间像任何其他命名空间，您可以添加顶级属性它只需添加一个模块，并指定`Namespace`的`My`。 批注与模块`HideModuleName`特性，如下面的示例所示。 `HideModuleName`特性可确保当智能感知显示的成员时，将不显示模块名称`My`命名空间。  
  
 [!code-vb[VbVbcnExtendingMy #&3;](../../../visual-basic/developing-apps/customizing-extending-my/codesnippet/VisualBasic/extending-the-my-namespace_3.vb)]  
  
 若要将成员添加到`My`命名空间，请根据需要向模块添加属性。 每个属性添加到`My`命名空间中，添加类型的私有字段`ThreadSafeObjectProvider(Of T)`，其中类型是由自定义属性返回的类型。 此字段用于创建线程安全对象实例的属性通过调用返回`GetInstance`方法。 因此，每个线程都访问扩展的属性接收自己的返回类型的实例。 下面的示例添加一个名为属性`SampleExtension`类型的指针`SampleExtension`到`My`命名空间︰  
  
 [!code-vb[VbVbcnExtendingMy #&4;](../../../visual-basic/developing-apps/customizing-extending-my/codesnippet/VisualBasic/extending-the-my-namespace_4.vb)]  
  
##  <a name="addingevents"></a>将事件添加到自定义 My 对象  
 您可以使用`My.Application`对象公开您的自定义事件`My`对象通过扩展`MyApplication`分部类中的`My`命名空间。 对于基于 Windows 的项目，您可以双击**我的项目**中为你的项目中的节点**解决方案资源管理器**。 在 Visual Basic 中**项目设计器**，请单击`Application`选项卡，然后单击`View Application Events`按钮。 将创建名为 ApplicationEvents.vb 一个新文件。 它包含以下代码来扩展`MyApplication`类。  
  
 [!code-vb[VbVbcnExtendingMy #&5;](../../../visual-basic/developing-apps/customizing-extending-my/codesnippet/VisualBasic/extending-the-my-namespace_5.vb)]  
  
 您可以为您的自定义添加事件处理程序`My`对象添加到自定义的事件处理程序`MyApplication`类。 自定义事件让您可以添加一个事件处理程序添加、 移除或引发该事件时将执行的代码。 请注意，`AddHandler`代码用于自定义事件而添加了对事件进行处理的用户代码的情况下，才会运行。 例如，考虑`SampleExtension`上一节中的对象具有`Load`您想要添加的自定义事件处理程序的事件。 下面的代码示例显示名为自定义事件处理程序`SampleExtensionLoad`将时调用`My.SampleExtension.Load`事件发生。 当添加代码来处理新`My.SampleExtensionLoad`事件，`AddHandler`执行此自定义事件代码的一部分。 `MyApplication_SampleExtensionLoad`方法包含在要展示一个示例处理一个事件处理程序的代码示例`My.SampleExtensionLoad`事件。 请注意，`SampleExtensionLoad`选择时，可以使用事件**我的应用程序事件**在左侧的下拉列表在代码编辑器上方时您正在编辑 ApplicationEvents.vb 文件的选项。  
  
 [!code-vb[VbVbcnExtendingMy #&6;](../../../visual-basic/developing-apps/customizing-extending-my/codesnippet/VisualBasic/extending-the-my-namespace_6.vb)]  
  
##  <a name="design"></a>设计指南  
 当您开发的扩展`My`命名空间中，使用以下准则来帮助您扩展组件的维护成本降至最低。  
  
-   **包括仅扩展逻辑。** 中包含的逻辑`My`命名空间扩展应包括只公开中的所需的功能所需的代码`My`命名空间。 由于您的扩展插件将以源代码形式驻留在用户项目中，更新扩展组件所产生的高额的维护开销，并应尽可能避免使用。  
  
-   **最小化项目假设。** 当您创建您的扩展的`My`命名空间中，不会假定引用、 导入项目级别或特定的编译器设置一组 (例如，`Option Strict`关闭)。 相反，最小化依赖项，则通过使用完全限定类型的所有引用`Global`关键字。 此外，请确保编译扩展时，`Option Strict`上以最大程度减少扩展中的错误。  
  
-   **隔离的扩展插件代码。** 将代码放在一个文件使您的扩展插件为 Visual Studio 项目模板可以方便地部署。 有关详细信息，请参阅本主题后面的"打包和部署扩展"。 放置所有`My`单个文件中的命名空间扩展代码或在项目中一个单独的文件夹还有助于用户查找`My`命名空间扩展。  
  
##  <a name="designing"></a>设计的类库我  
 对于多数对象模型的情况一样，一些设计模式适用于`My`命名空间和其他人不这样做。 当设计的扩展`My`命名空间，请考虑以下原则︰  
  
-   **无状态方法。** 中的方法`My`命名空间应提供某项特定任务的完整解决方案。 确保传递给方法的参数值提供了完成特定任务所需的所有输入。 应避免创建依赖于以前的状态，如对资源的打开连接的方法。  
  
-   **全局实例。** 只有在中维护的状态`My`命名空间是全局的项目。 例如，`My.Application.Info`封装整个应用程序共享的状态。  
  
-   **简单参数类型。** 为简单起见通过避免复杂的参数类型。 相反，创建不采用任何参数输入的方法或执行简单的输入的类型，如字符串、 基元类型等。  
  
-   **工厂方法。** 某些类型具有一定困难，若要实例化。 提供工厂方法为扩展`My`命名空间能让您更轻松地发现并使用属于此类别的类型。 最适合的工厂方法的一个示例是`My.Computer.FileSystem.OpenTextFileReader`。 .NET Framework 中有几种流类型。 具体而言，指定文本文件`OpenTextFileReader`有助于用户理解要使用的流。  
  
 这些准则不会阻止常规设计原则的类库。 相反，它们是针对开发人员使用的 Visual Basic 进行了优化的建议和`My`命名空间。 创建类库的常规设计原则，请参阅[Framework 设计准则](http://msdn.microsoft.com/library/5fbcaf4f-ea2a-4d20-b0d6-e61dee202b4b)。  
  
##  <a name="packaging"></a>打包和部署扩展  
 您可以包括`My`命名空间扩展 Visual Studio 项目模板，或者您可以打包您的扩展，并将它们部署为 Visual Studio 项模板。 当您打包您`My`用作 Visual Studio 项模板的命名空间扩展，您可以充分利用所提供的 Visual Basic 的其他功能。 这些功能使您能够时项目引用特定的程序集，包含扩展，或使用户可以显式添加您`My`使用的命名空间扩展**My 扩展**Visual Basic 项目设计器的页面。  
  
 有关如何部署的详细信息`My`命名空间的扩展，请参阅[打包和部署自定义 My 扩展](../../../visual-basic/developing-apps/customizing-extending-my/packaging-and-deploying-custom-my-extensions.md)。  
  
## <a name="see-also"></a>另请参阅  
 [打包和部署自定义 My 扩展](../../../visual-basic/developing-apps/customizing-extending-my/packaging-and-deploying-custom-my-extensions.md)   
 [扩展 Visual Basic 应用程序模型](../../../visual-basic/developing-apps/customizing-extending-my/extending-the-visual-basic-application-model.md)   
 [自定义的对象都将在我](../../../visual-basic/developing-apps/customizing-extending-my/customizing-which-objects-are-available-in-my.md)   
 [My 扩展页项目设计器](https://docs.microsoft.com/visualstudio/ide/reference/my-extensions-page-project-designer-visual-basic)   
 [应用程序页、项目设计器 (Visual Basic)](https://docs.microsoft.com/visualstudio/ide/reference/application-page-project-designer-visual-basic)   
 [Partial](../../../visual-basic/language-reference/modifiers/partial.md)
