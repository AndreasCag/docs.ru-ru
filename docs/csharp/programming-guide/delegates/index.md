---
title: "Делегаты (Руководство по программированию на C#) | Документы Майкрософт"
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
dev_langs:
- CSharp
helpviewer_keywords:
- C# language, delegates
- delegates [C#]
ms.assetid: 97de039b-c76b-4b9c-a27d-8c1e1c8d93da
caps.latest.revision: 30
author: BillWagner
ms.author: wiwagn
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
ms.translationtype: Human Translation
ms.sourcegitcommit: 31905a37f09db5f5192123f0118252fbe8b02eff
ms.openlocfilehash: ae5591bcd17a4b7afcdcdfb36717801819f2311f
ms.contentlocale: ru-ru
ms.lasthandoff: 06/26/2017

---
# <a name="delegates-c-programming-guide"></a>Делегаты (Руководство по программированию на C#)
[Делегат](../../../csharp/language-reference/keywords/delegate.md) — это тип, который представляет ссылки на методы с определенным списком параметров и типом возвращаемого значения. При создании экземпляра делегата этот экземпляр можно связать с любым методом с совместимой сигнатурой и типом возвращаемого значения. Метод можно вызвать (активировать) с помощью экземпляра делегата.  
  
 Делегаты используются для передачи методов в качестве аргументов к другим методам. Обработчики событий — это ничто иное, как методы, вызываемые с помощью делегатов. При создании пользовательского метода класс (например, элемент управления Windows) может вызывать этот метод при появлении определенного события. В следующем примере показано объявление делегата:  
  
 [!code-cs[csProgGuideDelegates#20](../../../csharp/programming-guide/delegates/codesnippet/CSharp/index_1.cs)]  
  
 Делегату можно назначить любой метод из любого доступного класса или структуры, соответствующей типу делегата. Этот метод должен быть статическим методом или методом экземпляра. Это позволяет программно изменять вызовы метода, а также включать новый код в существующие классы.  
  
> [!NOTE]
>  В контексте перегрузки метода его сигнатура не содержит возвращаемое значение. Однако в контексте делегатов сигнатура метода содержит возвращаемое значение. Другими словами, метод должен иметь тот же возвращаемый тип, что и делегат.  
  
 Благодаря возможности ссылаться на метод как на параметр делегаты идеально подходят для определения методов обратного вызова. Например, ссылка на метод, сравнивающий два объекта, может быть передана в качестве аргумента алгоритму сортировки. Поскольку код сравнения находится в отдельной процедуре, алгоритм сортировки может быть написан более общим способом.  
  
## <a name="delegates-overview"></a>Общие сведения о делегатах  
 Делегаты имеют следующие свойства.  
  
-   Делегаты похожи на указатели функций в C++, но являются типобезопасными.  
  
-   Делегаты допускают передачу методов в качестве параметров.  
  
-   Делегаты можно использовать для определения методов обратного вызова.  
  
-   Делегаты можно связывать друг с другом; например, при появлении одного события можно вызывать несколько методов.  
  
-   Точное соответствие методов типу делегата не требуется. Дополнительные сведения см. в разделе [Использование вариативности в делегатах](../../../csharp/programming-guide/concepts/covariance-contravariance/using-variance-in-delegates.md).  
  
-   В C# версии 2.0 введена концепция [анонимных методов](../../../csharp/programming-guide/statements-expressions-operators/anonymous-methods.md), которые позволяют передавать блоки кода в виде параметров вместо использования отдельно определенного метода. В C# 3.0 для краткой записи встроенных блоков кода введены лямбда-выражения. В результате компиляции как анонимных методов, так и лямбда-выражений (в определенном контексте) получаются типы делегатов. В настоящее время эти возможности называются анонимными возможностями. Дополнительные сведения о лямбда-выражениях см. в разделе [Анонимные функции](../../../csharp/programming-guide/statements-expressions-operators/anonymous-functions.md).  
  
## <a name="in-this-section"></a>Содержание  
  
-   [Использование делегатов](../../../csharp/programming-guide/delegates/using-delegates.md)  
  
-   [Использование делегатов вместо интерфейсов (руководство по программированию на C#)](http://msdn.microsoft.com/en-us/2e759bdf-7ca4-4005-8597-af92edf6d8f0)  
  
-   [Делегаты с именованными методами и делегаты с анонимными методами](../../../csharp/programming-guide/delegates/delegates-with-named-vs-anonymous-methods.md)  
  
-   [Анонимные методы](../../../csharp/programming-guide/statements-expressions-operators/anonymous-methods.md)  
  
-   [Использование расхождения в делегатах](../../../csharp/programming-guide/concepts/covariance-contravariance/using-variance-in-delegates.md)  
  
-   [Практическое руководство. Объединение делегатов (многоадресные делегаты)](../../../csharp/programming-guide/delegates/how-to-combine-delegates-multicast-delegates.md)  
  
-   [Практическое руководство. Объявление, создание и использование делегата](../../../csharp/programming-guide/delegates/how-to-declare-instantiate-and-use-a-delegate.md)  
  
## <a name="c-language-specification"></a>Спецификация языка C#  
 [!INCLUDE[CSharplangspec](~/includes/csharplangspec-md.md)]  
  
## <a name="featured-book-chapters"></a>Главы в популярных книгах  
 [Делегаты, события и лямбда-выражения](http://go.microsoft.com/fwlink/?LinkId=195395) в [справочном руководстве по C# 3.0, третье издание: более 250 решений для программистов на C# 3.0](http://go.microsoft.com/fwlink/?LinkId=195369)  
  
 [Делегаты и события](http://go.microsoft.com/fwlink/?LinkId=195418) в статье [Изучение C# 3.0: овладение основными понятиями C# 3.0](http://go.microsoft.com/fwlink/?LinkId=195412)  
  
## <a name="see-also"></a>См. также  
 <xref:System.Delegate>   
 [Руководство по программированию на C#](../../../csharp/programming-guide/index.md)   
 [События](../../../csharp/programming-guide/events/index.md)
