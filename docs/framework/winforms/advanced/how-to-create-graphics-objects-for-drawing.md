---
title: "如何：创建用于绘制的 Graphics 对象 | Microsoft Docs"
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
  - "GDI+, 创建图像"
  - "图形 [Windows 窗体], 创建"
  - "Graphics 类"
  - "图像 [Windows 窗体], 创建"
ms.assetid: 162861f9-f050-445e-8abb-b2c43a918b8b
caps.latest.revision: 17
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 17
---
# 如何：创建用于绘制的 Graphics 对象
需要先创建 <xref:System.Drawing.Graphics> 对象，然后才可以使用 [!INCLUDE[ndptecgdiplus](../../../../includes/ndptecgdiplus-md.md)] 绘制线条和形状、呈现文本或显示与操作图像。  <xref:System.Drawing.Graphics> 对象表示 [!INCLUDE[ndptecgdiplus](../../../../includes/ndptecgdiplus-md.md)] 绘图表面，并且该对象是用于创建图形图像的对象。  
  
 处理图形包括两个步骤：  
  
1.  创建 <xref:System.Drawing.Graphics> 对象。  
  
2.  使用 <xref:System.Drawing.Graphics> 对象绘制线条和形状、呈现文本或显示与操作图像。  
  
## 创建图形对象  
 可以用各种方法创建图形对象。  
  
#### 创建图形对象  
  
-   在窗体或控件的 <xref:System.Windows.Forms.Control.Paint> 事件中接收对图形对象的引用，作为 <xref:System.Windows.Forms.PaintEventArgs> 的一部分。  在为控件创建绘制代码时，通常会使用此方法来获取对图形对象的引用。  同样，您也可以在处理 <xref:System.Drawing.Printing.PrintDocument> 的 <xref:System.Drawing.Printing.PrintDocument.PrintPage> 事件时获取作为 <xref:System.Drawing.Printing.PrintPageEventArgs> 的属性的图形对象。  
  
     \- 或 \-  
  
-   调用某控件或窗体的 <xref:System.Windows.Forms.Control.CreateGraphics%2A> 方法以获取对 <xref:System.Drawing.Graphics> 对象的引用，该对象表示该控件或窗体的绘图图面。  如果想在已存在的窗体或控件上绘图，请使用此方法。  
  
     \- 或 \-  
  
-   由从 <xref:System.Drawing.Image> 继承的任何对象创建 <xref:System.Drawing.Graphics> 对象。  此方法在您需要更改已存在的图像时十分有用。  
  
     下面的部分给出了有关这些过程的详细信息。  
  
## Paint 事件处理程序中的 PaintEventArgs  
 当对控件的 <xref:System.Windows.Forms.PaintEventHandler> 编程或对 <xref:System.Drawing.Printing.PrintDocument> 的 <xref:System.Drawing.Printing.PrintDocument.PrintPage> 编程时，需提供一个图形对象作为 <xref:System.Windows.Forms.PaintEventArgs> 或 <xref:System.Drawing.Printing.PrintPageEventArgs> 的属性之一。  
  
#### 获取对 Paint 事件的 PaintEventArgs 中 Graphics 对象的引用  
  
1.  声明 <xref:System.Drawing.Graphics> 对象。  
  
2.  分配变量以引用作为 <xref:System.Windows.Forms.PaintEventArgs> 的一部分传递的 <xref:System.Drawing.Graphics> 对象。  
  
3.  插入代码来绘制窗体或控件。  
  
     下面的示例演示了如何从 <xref:System.Windows.Forms.Control.Paint> 事件中的 <xref:System.Windows.Forms.PaintEventArgs> 引用 <xref:System.Drawing.Graphics> 对象：  
  
    ```vb  
    Private Sub Form1_Paint(sender As Object, pe As PaintEventArgs) Handles _  
       MyBase.Paint  
       ' Declares the Graphics object and sets it to the Graphics object  
       ' supplied in the PaintEventArgs.  
       Dim g As Graphics = pe.Graphics  
       ' Insert code to paint the form here.  
    End Sub  
  
    ```  
  
    ```csharp  
    private void Form1_Paint(object sender,   
       System.Windows.Forms.PaintEventArgs pe)   
    {  
       // Declares the Graphics object and sets it to the Graphics object  
       // supplied in the PaintEventArgs.  
       Graphics g = pe.Graphics;  
       // Insert code to paint the form here.  
    }  
  
    ```  
  
    ```cpp  
    private:  
       void Form1_Paint(System::Object ^ sender,  
          System::Windows::Forms::PaintEventArgs ^ pe)  
       {  
          // Declares the Graphics object and sets it to the Graphics object  
          // supplied in the PaintEventArgs.  
          Graphics ^ g = pe->Graphics;  
          // Insert code to paint the form here.  
       }  
    ```  
  
## CreateGraphics 方法  
 也可以使用控件或窗体的 <xref:System.Windows.Forms.Control.CreateGraphics%2A> 方法来获取对 <xref:System.Drawing.Graphics> 对象的引用，该对象表示该控件或窗体的绘图图面。  
  
#### 用 CreateGraphics 方法创建 Graphics 对象  
  
-   调用要用于呈现图形的窗体或控件的 <xref:System.Windows.Forms.Control.CreateGraphics%2A> 方法。  
  
    ```vb  
    Dim g as Graphics  
    ' Sets g to a Graphics object representing the drawing surface of the  
    ' control or form g is a member of.  
    g = Me.CreateGraphics  
  
    ```  
  
    ```csharp  
    Graphics g;  
    // Sets g to a graphics object representing the drawing surface of the  
    // control or form g is a member of.  
    g = this.CreateGraphics();  
  
    ```  
  
    ```cpp  
    Graphics ^ g;  
    // Sets g to a graphics object representing the drawing surface of the  
    // control or form g is a member of.  
    g = this->CreateGraphics();  
    ```  
  
## 从 Image 对象创建  
 另外，可以从 <xref:System.Drawing.Image> 类派生的任何对象创建图形对象。  
  
#### 从 Image 创建 Graphics 对象  
  
-   调用 <xref:System.Drawing.Graphics.FromImage%2A?displayProperty=fullName> 方法，提供要从其创建 <xref:System.Drawing.Graphics> 对象的 Image 变量的名称。  
  
     下面的示例演示如何使用 <xref:System.Drawing.Bitmap> 对象：  
  
    ```vb  
    Dim myBitmap as New Bitmap("C:\Documents and Settings\Joe\Pics\myPic.bmp")  
    Dim g as Graphics = Graphics.FromImage(myBitmap)  
  
    ```  
  
    ```csharp  
    Bitmap myBitmap = new Bitmap(@"C:\Documents and   
       Settings\Joe\Pics\myPic.bmp");  
    Graphics g = Graphics.FromImage(myBitmap);  
  
    ```  
  
    ```cpp  
    Bitmap ^ myBitmap = gcnew  
       Bitmap("D:\\Documents and Settings\\Joe\\Pics\\myPic.bmp");  
    Graphics ^ g = Graphics::FromImage(myBitmap);  
    ```  
  
> [!NOTE]
>  只能从非索引 .bmp 文件（如 16 位、24 位和 32 位的 .bmp 文件）创建 <xref:System.Drawing.Graphics> 对象。  索引 .bmp 文件的像素将索引保存到颜色表中，相比而言，非索引 .bmp 文件的每个像素保存一种颜色。  
  
## 绘制和操作形状与图像  
 <xref:System.Drawing.Graphics> 对象在创建后，可用于绘制线条和形状、呈现文本或显示与操作图像。  与 <xref:System.Drawing.Graphics> 对象一起使用的主要对象有：  
  
-   <xref:System.Drawing.Pen> 类 \-\- 用于绘制线条、勾勒形状轮廓或呈现其他几何表示形式。  
  
-   <xref:System.Drawing.Brush> 类 \-\- 用于填充图形区域，如实心形状、图像或文本。  
  
-   <xref:System.Drawing.Font> 类 \-\- 提供有关在呈现文本时要使用什么形状的说明。  
  
-   <xref:System.Drawing.Color> 结构 \-\- 表示要显示的不同颜色。  
  
#### 使用创建的图形对象  
  
-   使用上面列出的适当对象进行所需的绘制。  
  
     有关更多信息，请参见下列主题：  
  
    |若要呈现|请参见|  
    |----------|---------|  
    |行|[如何：在 Windows 窗体上绘制线条](../../../../docs/framework/winforms/advanced/how-to-draw-a-line-on-a-windows-form.md)|  
    |形状|[如何：绘制空心形状](../../../../docs/framework/winforms/advanced/how-to-draw-an-outlined-shape.md)|  
    |Text|[如何：在 Windows 窗体上绘制文本](../../../../docs/framework/winforms/advanced/how-to-draw-text-on-a-windows-form.md)|  
    |图像|[如何：使用 GDI\+ 呈现图像](../../../../docs/framework/winforms/advanced/how-to-render-images-with-gdi.md)|  
  
## 请参阅  
 [图形编程入门](../../../../docs/framework/winforms/advanced/getting-started-with-graphics-programming.md)   
 [Windows 窗体中的图形和绘制](../../../../docs/framework/winforms/advanced/graphics-and-drawing-in-windows-forms.md)   
 [直线、曲线和图形](../../../../docs/framework/winforms/advanced/lines-curves-and-shapes.md)   
 [如何：使用 GDI\+ 呈现图像](../../../../docs/framework/winforms/advanced/how-to-render-images-with-gdi.md)