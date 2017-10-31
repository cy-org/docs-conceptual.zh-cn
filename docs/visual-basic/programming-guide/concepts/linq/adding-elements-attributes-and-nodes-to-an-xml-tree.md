---
title: "将元素、 特性和节点添加到 XML 树 (Visual Basic 中) |Microsoft 文档"
ms.custom: 
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- VB
ms.assetid: e243e694-c987-43aa-8b22-1e33dace582c
caps.latest.revision: 3
author: dotnet-bot
ms.author: dotnetcontent
translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: b8a1644757fb4ce9f1498e79b16d1077e412346b
ms.lasthandoff: 03/13/2017


---
# <a name="adding-elements-attributes-and-nodes-to-an-xml-tree-visual-basic"></a>将元素、 特性和节点添加到 XML 树 (Visual Basic)
可以向现有的 XML 树中添加内容（包括元素、属性、注释、处理指令、文本和 CDATA）。  
  
## <a name="methods-for-adding-content"></a>添加内容的方法  
 以下方法将子内容添加到<xref:System.Xml.Linq.XElement>或<xref:System.Xml.Linq.XDocument>::</xref:System.Xml.Linq.XDocument> </xref:System.Xml.Linq.XElement>  
  
|方法|说明|  
|------------|-----------------|  
|<xref:System.Xml.Linq.XContainer.Add%2A></xref:System.Xml.Linq.XContainer.Add%2A>|<xref:System.Xml.Linq.XContainer>。</xref:System.Xml.Linq.XContainer>的子内容的末尾添加内容|  
|<xref:System.Xml.Linq.XContainer.AddFirst%2A></xref:System.Xml.Linq.XContainer.AddFirst%2A>|<xref:System.Xml.Linq.XContainer>。</xref:System.Xml.Linq.XContainer>的子内容的开头添加内容|  
  
 以下方法将内容添加为<xref:System.Xml.Linq.XNode>。</xref:System.Xml.Linq.XNode>的同级节点 向其中添加同级内容的最常见的节点是<xref:System.Xml.Linq.XElement>，尽管您可以添加到其他类型的节点<xref:System.Xml.Linq.XText>或<xref:System.Xml.Linq.XComment>。</xref:System.Xml.Linq.XComment></xref:System.Xml.Linq.XText>等的有效的同级内容</xref:System.Xml.Linq.XElement>  
  
|方法|说明|  
|------------|-----------------|  
|<xref:System.Xml.Linq.XNode.AddAfterSelf%2A></xref:System.Xml.Linq.XNode.AddAfterSelf%2A>|在<xref:System.Xml.Linq.XNode>。</xref:System.Xml.Linq.XNode>之后添加内容|  
|<xref:System.Xml.Linq.XNode.AddBeforeSelf%2A></xref:System.Xml.Linq.XNode.AddBeforeSelf%2A>|<xref:System.Xml.Linq.XNode>。</xref:System.Xml.Linq.XNode>之前添加的内容|  
  
## <a name="example"></a>示例  
  
### <a name="description"></a>描述  
 下面的示例创建两个 XML 树，然后修改其中一个树。  
  
### <a name="code"></a>代码  
  
```vb  
Dim srcTree As XElement = _  
    <Root>  
        <Element1>1</Element1>  
        <Element2>2</Element2>  
        <Element3>3</Element3>  
        <Element4>4</Element4>  
        <Element5>5</Element5>  
    </Root>  
Dim xmlTree As XElement = _  
    <Root>  
        <Child1>1</Child1>  
        <Child2>2</Child2>  
        <Child3>3</Child3>  
        <Child4>4</Child4>  
        <Child5>5</Child5>  
    </Root>  
  
xmlTree.Add(<NewChild>new content</NewChild>)  
xmlTree.Add( _  
    From el In srcTree.Elements() _  
    Where CInt(el) > 3 _  
    Select el)  
  
' Even though Child9 does not exist in srcTree, the following statement  
' will not throw an exception, and nothing will be added to xmlTree.  
xmlTree.Add(srcTree.Element("Child9"))  
Console.WriteLine(xmlTree)  
  
```  
  
### <a name="comments"></a>注释  
 此代码生成以下输出：  
  
```xml  
<Root>  
  <Child1>1</Child1>  
  <Child2>2</Child2>  
  <Child3>3</Child3>  
  <Child4>4</Child4>  
  <Child5>5</Child5>  
  <NewChild>new content</NewChild>  
  <Element4>4</Element4>  
  <Element5>5</Element5>  
</Root>  
```  
  
## <a name="see-also"></a>另请参阅  
 [修改 XML 树 (LINQ to XML) (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/modifying-xml-trees-linq-to-xml.md)
