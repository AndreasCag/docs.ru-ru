---
title: "Типы значений и ссылочные типы | Документы Microsoft"
ms.custom: 
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
dev_langs:
- VB
helpviewer_keywords:
- reference data types
- reference types
- value types
- value data types
- types [Visual Basic]
- data types [Visual Basic], value types
- data types [Visual Basic], reference types
ms.assetid: fc82ce15-5a40-4c5c-a1e1-a556830e7391
caps.latest.revision: 14
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
ms.openlocfilehash: de8016b4b2a5550b32373a41c89a484fa996c596
ms.lasthandoff: 03/13/2017

---
# <a name="value-types-and-reference-types"></a>Value Types and Reference Types
В Visual Basic типы данных реализуются на основе их классификации. [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] Типы данных могут классифицироваться в соответствии с переменной определенного типа, хранит ли собственные данные или указатель на данные. Если переменная хранит собственные данные — *тип значения*; если он содержит указатель на данные в другом месте в памяти, это *ссылочный тип*.  
  
## <a name="value-types"></a>Типы значений  
 Тип данных является *тип значения* , если он содержит данные в пределах своей собственной памяти. Следующие типы значений:  
  
-   Все числовые типы данных  
  
-   `Boolean`, `Char` и `Date`  
  
-   Все структуры, даже если их члены являются ссылочными типами  
  
-   Перечисления, поскольку их базовый тип всегда является `SByte`, `Short`, `Integer`, `Long`, `Byte`, `UShort`, `UInteger`, или`ULong`  
  
 Каждая структура является типом значения, даже если он содержит члены ссылочного типа. По этой причине типы значения, такие как `Char` и `Integer` , реализуются посредством структуры .NET Framework.  
  
 Можно объявить тип значения с помощью зарезервированного ключевого слова, `Decimal`. Можно также использовать `New` ключевое слово для инициализации типа значений. Это особенно полезно, если тип имеет конструктор, принимающий параметры. Примером этого является <xref:System.Decimal.%23ctor%28System.Int32%2CSystem.Int32%2CSystem.Int32%2CSystem.Boolean%2CSystem.Byte%29>конструктор, который создает новый `Decimal` значение из предоставленных частей.</xref:System.Decimal.%23ctor%28System.Int32%2CSystem.Int32%2CSystem.Int32%2CSystem.Boolean%2CSystem.Byte%29>  
  
## <a name="reference-types"></a>Ссылочные типы  
 Объект *ссылочный тип* содержит указатель на другую область памяти, содержащую данные. Ссылочные типы включают следующие:  
  
-   `String`  
  
-   Все массивы, даже если их элементы являются типами значений  
  
-   Типы классов, таких как<xref:System.Windows.Forms.Form></xref:System.Windows.Forms.Form>  
  
-   Делегаты  
  
 Класс *ссылочный тип*. По этой причине ссылочные типы, такие как `Object` и `String` поддерживаемых [!INCLUDE[dnprdnshort](../../../../csharp/getting-started/includes/dnprdnshort_md.md)] классы. Обратите внимание, что каждый массив является ссылочным типом, даже если его члены являются типами значений.  
  
 Поскольку каждый ссылочный тип представляет собой соответствующий класс .NET Framework, следует использовать [оператор New](../../../../visual-basic/language-reference/operators/new-operator.md) ключевое слово для его инициализации. Следующий оператор инициализирует массив.  
  
```  
Dim totals() As Single = New Single(8) {}  
```  
  
## <a name="elements-that-are-not-types"></a>Элементы, которые не являются типами  
 Следующие элементы программирования не квалифицируются как типы, так как нельзя указывать ни один из них как тип данных для объявленного элемента:  
  
-   Пространства имен  
  
-   Модули  
  
-   События  
  
-   Свойства и процедуры  
  
-   Переменные, константы и поля  
  
## <a name="working-with-the-object-data-type"></a>Работа с типом данных объекта  
 Можно назначить переменной ссылочного типа или типа значения `Object` тип данных. `Object` Переменная всегда содержит указатель на данные, а не сами данные. Однако если присвоить тип значений для `Object` переменной, он ведет себя так, как если бы она содержала свои собственные данные. Дополнительные сведения см. в разделе [тип данных объекта](../../../../visual-basic/language-reference/data-types/object-data-type.md).  
  
 Вы можете выяснить, был ли `Object` переменная используется в качестве ссылочного типа или типа значения, передайте ее в <xref:Microsoft.VisualBasic.Information.IsReference%2A>метод <xref:Microsoft.VisualBasic.Information>класса <xref:Microsoft.VisualBasic?displayProperty=fullName>имен.</xref:Microsoft.VisualBasic?displayProperty=fullName> </xref:Microsoft.VisualBasic.Information> </xref:Microsoft.VisualBasic.Information.IsReference%2A> <xref:Microsoft.VisualBasic.Information.IsReference%2A?displayProperty=fullName>Возвращает `True` Если содержимое `Object` переменная представляет ссылочный тип.</xref:Microsoft.VisualBasic.Information.IsReference%2A?displayProperty=fullName>  
  
## <a name="see-also"></a>См. также  
 [Обнуляемые типы значений](../../../../visual-basic/programming-guide/language-features/data-types/nullable-value-types.md)   
 [Преобразования типов в Visual Basic](../../../../visual-basic/programming-guide/language-features/data-types/type-conversions.md)   
 [Оператор Structure](../../../../visual-basic/language-reference/statements/structure-statement.md)   
 [Эффективное использование типов данных](../../../../visual-basic/programming-guide/language-features/data-types/efficient-use-of-data-types.md)   
 [Тип данных Object](../../../../visual-basic/language-reference/data-types/object-data-type.md)   
 [Типы данных](../../../../visual-basic/programming-guide/language-features/data-types/index.md)
