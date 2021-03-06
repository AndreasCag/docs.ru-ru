---
title: "#error (справочник по C#) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
f1_keywords: 
  - "#error"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "#error - директива [C#]"
ms.assetid: f2a7f3af-4cf9-4111-b369-70204d24b26b
caps.latest.revision: 10
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 10
---
# #error (справочник по C#)
`#error` позволяет создавать ошибку первого уровня из определенного места в коде.  Примеры.  
  
```  
#error Deprecated code in this method.  
```  
  
## Заметки  
 `#error` обычно используется в качестве условной директивы.  
  
 Кроме того, с помощью [\#warning](../../../csharp/language-reference/preprocessor-directives/preprocessor-warning.md) можно создать предупреждение, определенное пользователем.  
  
## Пример  
  
```  
// preprocessor_error.cs  
// CS1029 expected  
#define DEBUG  
class MainClass   
{  
    static void Main()   
    {  
#if DEBUG  
#error DEBUG is defined  
#endif  
    }  
}  
```  
  
## См. также  
 [Справочник по C\#](../../../csharp/language-reference/index.md)   
 [Руководство по программированию на C\#](../../../csharp/programming-guide/index.md)   
 [Директивы препроцессора C\#](../../../csharp/language-reference/preprocessor-directives/index.md)