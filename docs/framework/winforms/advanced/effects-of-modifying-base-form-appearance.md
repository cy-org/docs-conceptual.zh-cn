---
title: "修改基窗体的外观的效果 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-winforms"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "jsharp"
helpviewer_keywords: 
  - "基窗体"
  - "继承, 窗体"
  - "继承的窗体, 对基窗体的修改"
  - "父窗体"
  - "Windows 窗体, 基窗体外观"
ms.assetid: 1c3f2b29-a05c-4c6f-aa1a-4e66b94f343a
caps.latest.revision: 9
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 9
---
# 修改基窗体的外观的效果
在应用程序开发过程中，可能经常需要更改基窗体的外观，该项目（或其他项目）中的其他窗体继承自该基窗体。  
  
 在设计时，当生成包含基窗体的项目时，对基窗体外观所做的更改（属性的设置或控件的增减）将在继承的窗体上反映。  仅将更改保存到基窗体是不够的。  若要生成项目，请从**“生成”**菜单选择**“生成”**。  
  
> [!NOTE]
>  显示的对话框和菜单命令可能会与“帮助”中的描述不同，具体取决于您现用的设置或版本。  若要更改设置，请在**“工具”**菜单上选择**“导入和导出设置”**。  有关更多信息，请参见 [Customizing Development Settings in Visual Studio](http://msdn.microsoft.com/zh-cn/22c4debb-4e31-47a8-8f19-16f328d7dcd3)。  
  
 在运行时对基窗体所作的修改不影响已经实例化的继承的窗体。  
  
## 请参阅  
 [base](../Topic/base%20\(C%23%20Reference\).md)   
 [如何：继承 Windows 窗体](../../../../docs/framework/winforms/advanced/how-to-inherit-windows-forms.md)   
 [Windows 窗体可视化继承](../../../../docs/framework/winforms/advanced/windows-forms-visual-inheritance.md)