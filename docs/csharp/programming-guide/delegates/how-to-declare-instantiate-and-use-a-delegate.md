---
title: Практическое руководство. Объявление, создание экземпляра и использование делегата (руководство по программированию в C#)
ms.date: 07/20/2015
helpviewer_keywords:
- delegates [C#], declaring and instantiating
ms.assetid: 61c4895f-f785-48f8-8bfe-db73b411c4ae
ms.openlocfilehash: 6c53d7572074db44976494e5eed596bf95aaf456
ms.sourcegitcommit: 3c1c3ba79895335ff3737934e39372555ca7d6d0
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/06/2018
ms.locfileid: "43858864"
---
# <a name="how-to-declare-instantiate-and-use-a-delegate-c-programming-guide"></a>Практическое руководство. Объявление, создание экземпляра и использование делегата (руководство по программированию в C#)
В C# 1.0 и более поздних версий делегаты можно объявлять так, как показано в следующем примере.  
  
 [!code-csharp[csProgGuideDelegates#13](../../../csharp/programming-guide/delegates/codesnippet/CSharp/how-to-declare-instantiate-and-use-a-delegate_1.cs)]  
  
 [!code-csharp[csProgGuideDelegates#14](../../../csharp/programming-guide/delegates/codesnippet/CSharp/how-to-declare-instantiate-and-use-a-delegate_2.cs)]  
  
 В C# 2.0 предоставлен более простой способ для записи предыдущего объявления, который показан в следующем примере.  
  
 [!code-csharp[csProgGuideDelegates#32](../../../csharp/programming-guide/delegates/codesnippet/CSharp/how-to-declare-instantiate-and-use-a-delegate_3.cs)]  
  
 В C# 2.0 и более поздних версиях можно использовать анонимный метод для объявления и инициализации [делегата](../../../csharp/language-reference/keywords/delegate.md), как показано в следующем примере.  
  
 [!code-csharp[csProgGuideDelegates#15](../../../csharp/programming-guide/delegates/codesnippet/CSharp/how-to-declare-instantiate-and-use-a-delegate_4.cs)]  
  
 В C# 3.0 и более поздних версиях можно объявлять делегаты и создавать для них экземпляры с помощью лямбда-выражения, как показано в следующем примере.  
  
 [!code-csharp[csProgGuideDelegates#31](../../../csharp/programming-guide/delegates/codesnippet/CSharp/how-to-declare-instantiate-and-use-a-delegate_5.cs)]  
  
 Дополнительные сведения см. в разделе [Лямбда-выражения](../../../csharp/programming-guide/statements-expressions-operators/lambda-expressions.md).  
  
 Следующий пример демонстрирует объявление, создание экземпляра и использование делегата. Класс `BookDB` инкапсулирует базу данных книжного магазина, в которой хранится информация о книгах. Он предоставляет метод `ProcessPaperbackBooks`, который находит в базе данных все книги в мягкой обложке и вызывает делегат для каждой из них. Используется тип `delegate` с именем `ProcessBookDelegate`. Класс `Test` использует этот класс для печати заголовков и средней цены книг в мягкой обложке.  
  
 Использование делегата помогает правильно разделить функции между базой данных книжного магазина и кодом клиента. Код клиента не имеет сведений о том, как хранятся книги и как код книжного магазина находит книги в мягкой обложке. Код книжного магазина не имеет сведений о том, какая обработка выполняется для найденных книг в мягкой обложке.  
  
## <a name="example"></a>Пример  
 [!code-csharp[csProgGuideDelegates#12](../../../csharp/programming-guide/delegates/codesnippet/CSharp/how-to-declare-instantiate-and-use-a-delegate_6.cs)]  
  
## <a name="robust-programming"></a>Отказоустойчивость  
  
-   Объявление делегата.  
  
     Следующая инструкция объявляет новый тип делегата.  
  
     [!code-csharp[csProgGuideDelegates#16](../../../csharp/programming-guide/delegates/codesnippet/CSharp/how-to-declare-instantiate-and-use-a-delegate_7.cs)]  
  
     Каждый тип делегата описывает количество аргументов и их типы, а также тип возвращаемого значения для всех методов, которые он может инкапсулировать. Каждый раз, когда требуется новый набор типов аргументов или новый тип возвращаемого значения, нужно объявить новый тип делегата.  
  
-   Создания экземпляра делегата.  
  
     После объявления типа делегата нужно создать объект этого делегата и связать его с определенным методом. Продолжая предыдущий пример, вы можете передать метод `PrintTitle` в метод `ProcessPaperbackBooks`, как показано в следующем примере:  
  
     [!code-csharp[csProgGuideDelegates#17](../../../csharp/programming-guide/delegates/codesnippet/CSharp/how-to-declare-instantiate-and-use-a-delegate_8.cs)]  
  
     Будет создан новый объект делегата, связанный со [статическим](../../../csharp/language-reference/keywords/static.md) методом `Test.PrintTitle`. Аналогичным образом, в следующем примере передается нестатический метод `AddBookToTotal` для объекта `totaller`:  
  
     [!code-csharp[csProgGuideDelegates#18](../../../csharp/programming-guide/delegates/codesnippet/CSharp/how-to-declare-instantiate-and-use-a-delegate_9.cs)]  
  
     В обоих случаях новый объект делегата передается в метод `ProcessPaperbackBooks`.  
  
     После создания делегата невозможно изменить метод, с которым он связан. Объекты делегатов являются неизменяемыми.  
  
-   Использование делегатов.  
  
     Обычно после создания объекта делегата он передается в другой код, который будет использовать этот делегат. Для вызова объекта делегата используется имя этого объекта, за которым следуют параметризованные аргументы, которые нужно передать делегату. Ниже показан пример использования делегата.  
  
     [!code-csharp[csProgGuideDelegates#19](../../../csharp/programming-guide/delegates/codesnippet/CSharp/how-to-declare-instantiate-and-use-a-delegate_10.cs)]  
  
     Делегат можно вызвать синхронно, как показано в этом примере, или асинхронно при помощи методов `BeginInvoke` и `EndInvoke`.  
  
## <a name="see-also"></a>См. также

- [Руководство по программированию на C#](../../../csharp/programming-guide/index.md)  
- [События](../../../csharp/programming-guide/events/index.md)  
- [Делегаты](../../../csharp/programming-guide/delegates/index.md)
