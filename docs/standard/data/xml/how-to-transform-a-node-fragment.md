---
title: "Как преобразовать фрагмент узла | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-standard"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
ms.assetid: 73a6c582-b9d7-4fa7-9a05-6d931e1f3de8
caps.latest.revision: 2
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 2
---
# Как преобразовать фрагмент узла
Во время преобразования данных, содержащихся в объекте <xref:System.Xml.XmlDocument> или <xref:System.Xml.XPath.XPathDocument>, преобразования XSLT применяются к документу в целом.  Иными словами, если передать узел, отличный от корневого узла документа, это не помешает процессу преобразования обратиться ко всем узлам загружаемого документа.  Чтобы преобразовать фрагмент узла, необходимо создать отдельный объект, содержащий только этот фрагмент, и передать его методу <xref:System.Xml.Xsl.XslCompiledTransform.Transform%2A>.  
  
## Процедуры  
  
#### Преобразование фрагмента узла  
  
1.  Создайте объект, содержащий исходный документ.  
  
2.  Определите расположение фрагмента узла для преобразования.  
  
3.  Создайте отдельный объект, содержащий только фрагмент узла.  
  
4.  Передайте фрагмент узла методу <xref:System.Xml.Xsl.XslCompiledTransform.Transform%2A>.  
  
## Пример  
 В следующем примере преобразуется фрагмент узла, а результаты выводятся на консоль.  
  
 [!code-csharp[XSLT_NodeFrag#1](../../../../samples/snippets/csharp/VS_Snippets_Data/XSLT_NodeFrag/CS/xslt_frag.cs#1)]
 [!code-vb[XSLT_NodeFrag#1](../../../../samples/snippets/visualbasic/VS_Snippets_Data/XSLT_NodeFrag/VB/xslt_frag.vb#1)]  
  
### Ввод  
  
##### books.xml  
 [!code-xml[XML_Core_Files#1](../../../../samples/snippets/xml/VS_Snippets_Data/XML_Core_Files/XML/books.xml#1)]  
  
##### single.xsl  
 [!code-xml[XSLT_NodeFrag#2](../../../../samples/snippets/xml/VS_Snippets_Data/XSLT_NodeFrag/XML/single.xsl#2)]  
  
### Вывод  
 Заголовок книги — The Confidence Man.  
  
## См. также  
 [Использование класса XslCompiledTransform](../../../../docs/standard/data/xml/using-the-xslcompiledtransform-class.md)