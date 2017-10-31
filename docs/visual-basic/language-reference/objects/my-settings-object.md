---
title: "My.Settings 对象 |Microsoft 文档"
ms.date: 2015-07-20
ms.prod: .net
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
f1_keywords:
- My.MySettingsProperty.Settings
- My.Settings
dev_langs:
- VB
helpviewer_keywords:
- My.Settings object
ms.assetid: 41f30dc1-202a-4273-b9b7-5728941f996c
caps.latest.revision: 16
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
ms.openlocfilehash: d48d3556f55ef286e2f501e2df5bf5035d3aff90
ms.lasthandoff: 03/13/2017

---
# <a name="mysettings-object"></a>My.Settings 对象
提供属性和方法来访问应用程序的设置。  
  
## <a name="remarks"></a>备注  
 `My.Settings`对象提供对应用程序的设置的访问，并允许您动态地存储和检索属性设置和您的应用程序的其他信息。 有关详细信息，请参阅[管理应用程序设置 (.NET)](https://docs.microsoft.com/visualstudio/ide/managing-application-settings-dotnet)。  
  
## <a name="properties"></a>属性  
 属性的`My.Settings`对象提供对应用程序的设置的访问。 若要添加或删除设置，请使用**设置设计器**。  
  
 每个设置具有**名称**，**类型**，**范围**，和**值**，并且这些设置确定用于访问每个设置的属性中的显示方式`My.Settings`对象︰  
  
-   **名称**确定该属性的名称。  
  
-   **类型**确定该属性的类型。  
  
-   **作用域**指示属性是否是只读的。 如果值为**应用程序**，该属性是只读的; 如果值为**用户**，该属性是可读写。  
  
-   **值**是属性的默认值。  
  
## <a name="methods"></a>方法  
  
|方法|描述|  
|---|---|  
|`Reload`|重新加载上次保存的值中的用户设置。|  
|`Save`|将保存当前的用户设置。|  
  
 `My.Settings`对象还提供了高级的属性和方法，继承<xref:System.Configuration.ApplicationSettingsBase>类。</xref:System.Configuration.ApplicationSettingsBase>  
  
## <a name="tasks"></a>任务  
 下表列出了所涉及的任务的示例`My.Settings`对象。  
  
|到|请参阅|  
|---|---|  
|读取应用程序设置|[如何︰ 读取在 Visual Basic 中的应用程序设置](../../../visual-basic/developing-apps/programming/app-settings/how-to-read-application-settings.md)|  
|更改用户设置|[如何︰ 在 Visual Basic 中的用户设置更改](../../../visual-basic/developing-apps/programming/app-settings/how-to-change-user-settings.md)|  
|保持用户设置|[如何︰ 保存在 Visual Basic 中的用户设置](../../../visual-basic/developing-apps/programming/app-settings/how-to-persist-user-settings.md)|  
|创建用户设置的属性网格|[如何︰ 创建在 Visual Basic 中的用户设置的属性网格](../../../visual-basic/developing-apps/programming/app-settings/how-to-create-property-grids-for-user-settings.md)|  
  
## <a name="example"></a>示例  
 此示例中显示的值`Nickname`设置。  
  
 [!code-vb[VbVbalrMyResources #&14;](../../../visual-basic/developing-apps/programming/app-settings/codesnippet/VisualBasic/my-settings-object_1.vb)]  
  
 对于此示例正常工作，您的应用程序必须具有`Nickname`类型设置`String`。  
  
## <a name="see-also"></a>另请参阅  
 <xref:System.Configuration.ApplicationSettingsBase></xref:System.Configuration.ApplicationSettingsBase>   
 [如何︰ 读取在 Visual Basic 中的应用程序设置](../../../visual-basic/developing-apps/programming/app-settings/how-to-read-application-settings.md)   
 [如何︰ 在 Visual Basic 中的用户设置更改](../../../visual-basic/developing-apps/programming/app-settings/how-to-change-user-settings.md)   
 [如何︰ 保存在 Visual Basic 中的用户设置](../../../visual-basic/developing-apps/programming/app-settings/how-to-persist-user-settings.md)   
 [如何︰ 创建在 Visual Basic 中的用户设置的属性网格](../../../visual-basic/developing-apps/programming/app-settings/how-to-create-property-grids-for-user-settings.md)   
 [管理应用程序设置 (.NET)](https://docs.microsoft.com/visualstudio/ide/managing-application-settings-dotnet)
