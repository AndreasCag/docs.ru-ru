---
title: "#warning (справочник по C#) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
f1_keywords: 
  - "#warning"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "#warning - директива [C#]"
ms.assetid: e6fb496d-bb8b-4018-baf6-5b60a0c8902b
caps.latest.revision: 9
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 9
---
# #warning (справочник по C#)
`#warning` позволяет создавать предупреждение первого уровня из определенного места в коде.  Например:  
  
```  
#warning Deprecated code in this method.  
```  
  
## Заметки  
 `#warning` обычно используется в качестве условной директивы.  Кроме того, с помощью [\#error](../../../csharp/language-reference/preprocessor-directives/preprocessor-error.md) можно создать ошибку, определенную пользователем.  
  
## Пример  
  
```  
// preprocessor_warning.cs  
// CS1030 expected  
#define DEBUG  
class MainClass   
{  
    static void Main()   
    {  
#if DEBUG  
#warning DEBUG is defined  
#endif  
    }  
}  
```  
  
## См. также  
 [Справочник по C\#](../../../csharp/language-reference/index.md)   
 [Руководство по программированию на C\#](../../../csharp/programming-guide/index.md)   
 [Директивы препроцессора C\#](../../../csharp/language-reference/preprocessor-directives/index.md)
