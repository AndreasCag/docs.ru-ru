---
title: "Ни один из доступных перегруженных &quot;&lt;имя_метода&gt;&quot; не может вызываться с этими аргументами без преобразования с сужением: &lt;список&gt; | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vbrAmbiguousCall2"
ms.assetid: 13b20ffa-9f02-4971-a3cb-e08b402fd971
caps.latest.revision: 9
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 9
---
# Ни один из доступных перегруженных &quot;&lt;имя_метода&gt;&quot; не может вызываться с этими аргументами без преобразования с сужением: &lt;список&gt;
Вызван перегруженный метод, однако он не может быть сопоставлен со списком указанных аргументов без сужающего преобразования.  
  
### Исправление ошибки  
  
1.  Укажите `Option``Strict` `Off`.  
  
2.  Измените аргументы таким образом, чтобы они соответствовали сигнатуре перегруженного метода.  
  
## См. также  
 [Передача аргументов по значению и по ссылке](../../visual-basic/programming-guide/language-features/procedures/passing-arguments-by-value-and-by-reference.md)   
 [Расширяющие и сужающие преобразования](../../visual-basic/programming-guide/language-features/data-types/widening-and-narrowing-conversions.md)