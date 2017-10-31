---
title: "如何：更改 Windows 窗体 ToolTip 组件的延迟 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-winforms"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "jsharp"
helpviewer_keywords: 
  - "示例 [Windows 窗体], 工具提示"
  - "ToolTip 组件 [Windows 窗体], 延迟值"
  - "工具提示 [Windows 窗体], 延迟值"
ms.assetid: 08979ba7-dd84-477b-ab17-8d06e759be99
caps.latest.revision: 12
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 12
---
# 如何：更改 Windows 窗体 ToolTip 组件的延迟
可以为 Windows 窗体 <xref:System.Windows.Forms.ToolTip> 组件设置多个延迟值。  所有这些属性的度量单位都是毫秒。  <xref:System.Windows.Forms.ToolTip.InitialDelay%2A> 属性确定用户必须指向关联控件多长时间工具提示字符串才会出现。  当鼠标从与工具提示关联的一个控件移到另一个控件时，<xref:System.Windows.Forms.ToolTip.ReshowDelay%2A> 属性用于设置出现后面的工具提示字符串所需的毫秒数。  <xref:System.Windows.Forms.ToolTip.AutoPopDelay%2A> 属性确定工具提示字符串显示多长时间。  您可以逐个设置这些值，或者通过设置 <xref:System.Windows.Forms.ToolTip.AutomaticDelay%2A> 属性的值进行设置；其他延迟属性是根据分配给 <xref:System.Windows.Forms.ToolTip.AutomaticDelay%2A> 属性的值设置的。  例如，当 <xref:System.Windows.Forms.ToolTip.AutomaticDelay%2A> 的值为 N 时，<xref:System.Windows.Forms.ToolTip.InitialDelay%2A> 被设置为 N，<xref:System.Windows.Forms.ToolTip.ReshowDelay%2A> 被设置为 <xref:System.Windows.Forms.ToolTip.AutomaticDelay%2A> 除以 5（即 N\/5）的值，而 <xref:System.Windows.Forms.ToolTip.AutoPopDelay%2A> 被设置为 5 倍于 <xref:System.Windows.Forms.ToolTip.AutomaticDelay%2A> 属性值的值（即 5N）。  
  
### 设置延迟  
  
1.  如下例所示设置下列属性。  
  
    ```vb  
    ToolTip1.InitialDelay = 500  
    ToolTip1.ReshowDelay = 100  
    ToolTip1.AutoPopDelay = 5000  
  
    ```  
  
    ```csharp  
    ToolTip1.InitialDelay = 500;  
    ToolTip1.ReshowDelay = 100;  
    ToolTip1.AutoPopDelay = 5000;  
  
    ```  
  
    ```cpp  
    toolTip1->InitialDelay = 500;  
    toolTip1->ReshowDelay = 100;  
    toolTip1->AutoPopDelay = 5000;  
    ```  
  
## 请参阅  
 [ToolTip 组件概述](../../../../docs/framework/winforms/controls/tooltip-component-overview-windows-forms.md)   
 [如何：在设计时为 Windows 窗体上的控件设置工具提示](../../../../docs/framework/winforms/controls/how-to-set-tooltips-for-controls-on-a-windows-form-at-design-time.md)   
 [ToolTip 组件](../../../../docs/framework/winforms/controls/tooltip-component-windows-forms.md)