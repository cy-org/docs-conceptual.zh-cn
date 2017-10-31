---
title: "My.Resources 对象 |Microsoft 文档"
ms.date: 2015-07-20
ms.prod: .net
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
f1_keywords:
- My.Resources
- My.Resources.MyResources.ResourceManager
- My.Resources.MyResources.Culture
dev_langs:
- VB
helpviewer_keywords:
- My.Resources object
ms.assetid: 34c3f2dc-7b87-432c-9d5f-17ea666bb266
caps.latest.revision: 22
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
ms.openlocfilehash: 6ad5bd4e33438256719b59cb0936cf6bc8525ab1
ms.lasthandoff: 03/13/2017

---
# <a name="myresources-object"></a>My.Resources 对象
提供用于访问应用程序的资源的属性和类。  
  
## <a name="remarks"></a>备注  
 `My.Resources`对象提供了对应用程序的资源的访问，并允许动态应用程序检索资源。 有关详细信息，请参阅[管理应用程序资源 (.NET)](https://docs.microsoft.com/visualstudio/ide/managing-application-resources-dotnet)。  
  
 `My.Resources`对象仅公开全局资源。 它不提供对与窗体关联的资源文件的访问。 必须从该窗体来访问窗体资源。 有关详细信息，请参阅[演练：本地化 Windows 窗体](http://msdn.microsoft.com/en-us/9a96220d-a19b-4de0-9f48-01e5d82679e5)。  
  
 您可以访问应用程序的区域性特定资源文件从`My.Resources`对象。 默认情况下，`My.Resources`对象内查找匹配的区域中的资源文件中的资源<xref:Microsoft.VisualBasic.ApplicationServices.ApplicationBase.UICulture%2A>属性。</xref:Microsoft.VisualBasic.ApplicationServices.ApplicationBase.UICulture%2A> 但是，您可以重写此行为并指定特定区域性使用的资源。 有关详细信息，请参阅[桌面应用中的资源](http://msdn.microsoft.com/library/8ad495d4-2941-40cf-bf64-e82e85825890)。  
  
## <a name="properties"></a>属性  
 属性的`My.Resources`对象提供对应用程序的资源的只读访问。 若要添加或删除资源，请使用**项目设计器**。 有关详细信息，请参阅[如何︰ 添加或移除资源](http://msdn.microsoft.com/en-us/7b77bc06-3952-4799-b029-def3f8f7f88d)。 您可以访问资源通过添加**项目设计器**使用`My.Resources.``resourceName`。  
  
 您还可以添加或移除通过选择你的项目中的资源文件**解决方案资源管理器**，然后单击**添加新项**或**添加现有项**从**项目**菜单。 您可以访问通过这种方式添加的资源`My.Resources.``resourceFileName`。`resourceName`。  
  
 每个资源具有名称、 类别和值，并且这些资源设置决定了用于访问该资源的属性中的显示方式`My.Resources`对象。 在添加的资源**项目设计器**:  
  
-   名称确定该属性的名称  
  
-   资源数据是与属性的值  
  
-   类别确定属性的类型︰  
  
|类别|属性数据类型|  
|---|---|  
|**字符串**|[字符串](../../../visual-basic/language-reference/data-types/string-data-type.md)|  
|**图像**|<xref:System.Drawing.Bitmap></xref:System.Drawing.Bitmap>|  
|**图标**|<xref:System.Drawing.Icon></xref:System.Drawing.Icon>|  
|**音频**|<xref:System.IO.UnmanagedMemoryStream></xref:System.IO.UnmanagedMemoryStream><br /><br /> <xref:System.IO.UnmanagedMemoryStream>类派生自<xref:System.IO.Stream>类，以便它可以用于以流，如方法<xref:Microsoft.VisualBasic.Devices.Audio.Play%2A>方法。</xref:Microsoft.VisualBasic.Devices.Audio.Play%2A> </xref:System.IO.Stream> </xref:System.IO.UnmanagedMemoryStream>|  
|**文件**|-   [字符串](../../../visual-basic/language-reference/data-types/string-data-type.md)为文本文件。<br />-<xref:System.Drawing.Bitmap>图像文件。</xref:System.Drawing.Bitmap><br />-<xref:System.Drawing.Icon>图标文件。</xref:System.Drawing.Icon><br />-<xref:System.IO.UnmanagedMemoryStream>的声音文件。</xref:System.IO.UnmanagedMemoryStream>|  
|**其他**|通过在设计器中的信息确定**类型**列。|  
  
## <a name="classes"></a>类  
 `My.Resources`对象将作为具有共享属性的类公开每个资源文件。 类名是资源文件的名称相同。 如前一部分中所述，资源文件中的资源公开为类中的属性。  
  
## <a name="example"></a>示例  
 此示例将窗体的标题设置为字符串资源名称为`Form1Title`应用程序资源文件中。 对于该示例能工作，该应用程序必须具有一个名为字符串`Form1Title`其资源文件中。 有关详细信息，请参阅[如何︰ 添加或移除资源](http://msdn.microsoft.com/en-us/7b77bc06-3952-4799-b029-def3f8f7f88d)。  
  
 [!code-vb[VbVbalrMyResources #&1;](../../../visual-basic/developing-apps/programming/app-settings/codesnippet/VisualBasic/my-resources-object_1.vb)]  
  
## <a name="example"></a>示例  
 本示例将窗体的图标名为图标为`Form1Icon`存储在应用程序的资源文件。 对于该示例能工作，应用程序必须具有名为图标`Form1Icon`其资源文件中。  
  
 [!code-vb[VbVbalrMyResources #&2;](../../../visual-basic/developing-apps/programming/app-settings/codesnippet/VisualBasic/my-resources-object_2.vb)]  
  
## <a name="example"></a>示例  
 此示例将窗体的背景图像设置到名为的图像资源`Form1Background`，这是应用程序资源文件。 对于此示例正常工作，该应用程序必须具有名为的图像资源`Form1Background`其资源文件中。  
  
 [!code-vb[VbVbalrMyResources #&3;](../../../visual-basic/developing-apps/programming/app-settings/codesnippet/VisualBasic/my-resources-object_3.vb)]  
  
## <a name="example"></a>示例  
 此示例播放的声音，作为名为音频资源存储`Form1Greeting`应用程序的资源文件中。 对于该示例能工作，应用程序必须具有名为音频资源`Form1Greeting`其资源文件中。 `My.Computer.Audio.Play`方法是仅适用于 Windows 窗体应用程序。  
  
 [!code-vb[VbVbalrMyResources #&4;](../../../visual-basic/developing-apps/programming/app-settings/codesnippet/VisualBasic/my-resources-object_4.vb)]  
  
## <a name="example"></a>示例  
 此示例检索字符串资源的应用程序的法语区域性版本。 指定的资源`Message`。 若要更改区域性，`My.Resources`对象使用，该示例使用<xref:Microsoft.VisualBasic.ApplicationServices.ApplicationBase.ChangeUICulture%2A>。</xref:Microsoft.VisualBasic.ApplicationServices.ApplicationBase.ChangeUICulture%2A>  
  
 对于此示例正常工作，该应用程序必须具有一个名为字符串`Message`在其资源文件和应用程序应该有该资源文件中，Resources.fr-fr.resx，该文件的法语区域性版本。 有关详细信息，请参阅[如何︰ 添加或移除资源](http://msdn.microsoft.com/en-us/7b77bc06-3952-4799-b029-def3f8f7f88d)。 如果应用程序不具有资源文件中，法语区域性版本`My.Resource`对象将从默认区域性资源文件中检索资源。  
  
 [!code-vb[VbVbalrMyResources #&10;](../../../visual-basic/developing-apps/programming/app-settings/codesnippet/VisualBasic/my-resources-object_5.vb)]  
  
## <a name="see-also"></a>另请参阅  
 [如何︰ 添加或删除资源](http://msdn.microsoft.com/en-us/7b77bc06-3952-4799-b029-def3f8f7f88d)   
 [管理应用程序资源 (.NET)](https://docs.microsoft.com/visualstudio/ide/managing-application-resources-dotnet)   
 [桌面应用程序中的资源](http://msdn.microsoft.com/library/8ad495d4-2941-40cf-bf64-e82e85825890)   
 [演练︰ 本地化 Windows 窗体](http://msdn.microsoft.com/en-us/9a96220d-a19b-4de0-9f48-01e5d82679e5)
