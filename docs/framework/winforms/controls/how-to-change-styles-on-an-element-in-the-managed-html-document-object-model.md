---
title: "如何：在托管 HTML 文档对象模型中更改元素的样式 | Microsoft Docs"
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
  - "托管 HTML DOM, 更改元素的样式"
ms.assetid: 154e8d9f-3e2d-4e8b-a6f3-c85a070e9cc1
caps.latest.revision: 7
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 7
---
# 如何：在托管 HTML 文档对象模型中更改元素的样式
可以使用 HTML 中的样式控制文档及其元素的外观。  <xref:System.Windows.Forms.HtmlDocument> 和 <xref:System.Windows.Forms.HtmlElement> 支持接受以下格式的样式字符串的 <xref:System.Windows.Forms.HtmlElement.Style%2A> 属性：  
  
 `name1:value1;...;nameN:valueN;`  
  
 这里是一个 `DIV`，所带的样式字符串的字体设置为 Arial，所有文本均设置为粗体：  
  
 `<DIV style="font-face:arial;font-weight:bold;">`  
  
 `Hello, world!`  
  
 `</DIV>`  
  
 使用 <xref:System.Windows.Forms.HtmlElement.Style%2A> 属性操作样式的问题是，添加到单个样式设置和从字符串移除单个样式设置比较麻烦。  例如，当用户将光标放置在 `DIV` 上时以斜体呈现以前的文本，以及当光标离开 `DIV` 时去掉斜体，都会成为很复杂的过程。  如果您需要用这种方式操作大量样式，时间将成为一个问题。  
  
 下面的过程包含的代码可用于在 HTML 文档和元素上轻松操作样式。  此过程要求您知道如何在 Windows 窗体中执行基本任务，例如创建新项目和将控件添加到窗体。  
  
### 在 Windows 窗体应用程序中处理样式更改  
  
1.  创建新的 Windows 窗体项目。  
  
2.  创建一个新的类文件，结尾是适合您的编程语言的扩展名。  
  
3.  将本主题中“示例”部分的 `StyleGenerator` 类代码复制到类文件中，并保存该代码。  
  
4.  将下面的 HTML 保存到名为 Test.htm 的文件中。  
  
    ```  
    <HTML>  
        <BODY>  
  
            <DIV style="font-face:arial;font-weight:bold;">  
                Hello, world!  
            </DIV><P>  
  
            <DIV>  
                Hello again, world!  
            </DIV><P>  
  
        </BODY>  
    </HTML>  
    ```  
  
5.  将名为 `webBrowser1` 的 <xref:System.Windows.Forms.WebBrowser> 控件添加到您的项目的主窗体中。  
  
6.  将下面的代码添加到项目的代码文件中。  
  
    > [!IMPORTANT]
    >  确保 `webBrowser1_DocumentCompleted` 事件处理程序配置为 <xref:System.Windows.Forms.WebBrowser.DocumentCompleted> 事件的侦听器。  在 [!INCLUDE[vsprvs](../../../../includes/vsprvs-md.md)] 中，双击 <xref:System.Windows.Forms.WebBrowser> 控件；在文本编辑器中，以编程方式配置侦听器。  
  
     [!code-csharp[ManagedDOMStyles#2](../../../../samples/snippets/csharp/VS_Snippets_Winforms/ManagedDOMStyles/CS/Form1.cs#2)]
     [!code-vb[ManagedDOMStyles#2](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/ManagedDOMStyles/VB/Form1.vb#2)]  
  
7.  运行该项目。  在第一个 `DIV` 上移动光标，以观测代码效果。  
  
## 示例  
 下面的代码示例演示 `StyleGenerator` 类的完整代码，该代码分析现有样式值，支持添加、更改和移除样式，并返回包含所请求的更改的新样式值。  
  
 [!code-csharp[ManagedDOMStyles#1](../../../../samples/snippets/csharp/VS_Snippets_Winforms/ManagedDOMStyles/CS/StyleGenerator.cs#1)]
 [!code-vb[ManagedDOMStyles#1](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/ManagedDOMStyles/VB/StyleGenerator.vb#1)]  
  
## 请参阅  
 <xref:System.Windows.Forms.HtmlElement>