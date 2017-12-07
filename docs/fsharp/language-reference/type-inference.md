---
title: "Вывод типа (F#)"
description: "Узнайте, как компилятор F # определяет типы значений, переменных, параметров и возвращаемых значений."
keywords: "visual f#, f#, функциональное программирование"
author: cartermp
ms.author: phcart
ms.date: 05/16/2016
ms.topic: language-reference
ms.prod: .net
ms.technology: devlang-fsharp
ms.devlang: fsharp
ms.assetid: 2d5fa4b1-732a-4d71-a62d-07f7ee79fe06
ms.openlocfilehash: c23954c0a0828cc7d2aae0553d37d5ee1dfbe152
ms.sourcegitcommit: bd1ef61f4bb794b25383d3d72e71041a5ced172e
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/18/2017
---
# <a name="type-inference"></a>Вывод типа

В этом разделе описывается, как компилятор F # определяет типы значений, переменных, параметров и возвращаемых значений.

## <a name="type-inference-in-general"></a>Определение типа в целом
Концепция вывода типа является не имеют для указания типов конструкций F #, за исключением случаев, когда компилятор не может определить тип. Пропуск сведения явный тип означает, что F # — это динамически типизированный язык или что значения в языке F # слабо типизированы. F # — это статически типизированный язык, это означает, что компилятор выводит точный тип, для каждой конструкции во время компиляции. Если имеется достаточно сведений, чтобы компилятор мог вывести типы каждой конструкции, вы должны предоставить дополнительные сведения о типе, обычно путем добавления заметок явный тип, где-либо в коде.


## <a name="inference-of-parameter-and-return-types"></a>Вывод параметров и возвращаемые типы
В списке параметров не нужно указать тип каждого параметра. И еще, F # — это статически типизированный язык, и поэтому каждое значение и выражение имеют определенный тип во время компиляции. Для этих типов, которые явно не указан компилятор выводит тип, в зависимости от контекста. Если тип не указана иным образом, он определяется как универсальные. Если код использует значение несогласованно, так что нет единственного выведенного типа, который удовлетворяет всем вариантам использования значения, компилятор сообщает об ошибке.

Тип возвращаемого значения функции определяется по типу последнего выражения в функции.

Например, в следующем коде, типы параметров `a` и `b` и тип возвращаемого значения выводятся быть `int` так как литерал `100` относится к типу `int`.

[!code-fsharp[Main](../../../samples/snippets/fsharp/lang-ref-3/snippet301.fs)]

Может повлиять на вывод типа, изменив литералы. При внесении `100` `uint32` путем добавления суффикса `u`, типы `a`, `b`, и имеют тип возвращаемого значения `uint32`.

Также могут повлиять на определение типа, используя другие конструкции, которые подразумевают ограничения на типы, такие как функции и методы, работающие с определенным типом.

Кроме того можно применить явный тип заметки для параметров функции или метода или переменные в выражениях, как показано в следующих примерах. Если возникают конфликты между различными ограничениями возникать ошибки.

[!code-fsharp[Main](../../../samples/snippets/fsharp/lang-ref-3/snippet302.fs)]

Вы также можно явно указать возвращаемое значение функции, предоставляя аннотацию типа после того как все параметры.

[!code-fsharp[Main](../../../samples/snippets/fsharp/lang-ref-3/snippet303.fs)]

Распространенный случай, когда полезно аннотации типа для параметра — параметр не является типом объекта, если необходимо использовать член.

[!code-fsharp[Main](../../../samples/snippets/fsharp/lang-ref-3/snippet304.fs)]
    
## <a name="automatic-generalization"></a>Автоматическое обобщение
Если код функции не зависит от типа параметра, компилятор считает, что параметр является универсальным. Это называется *Автоматическое обобщение*, и он может быть помогать при написании универсального кода без повышения сложности.

Например следующая функция объединяет два параметра любого типа в кортеж.

[!code-fsharp[Main](../../../samples/snippets/fsharp/lang-ref-3/snippet305.fs)]

Тип определяется как

```fsharp
'a -> 'b -> 'a * 'b
```

## <a name="additional-information"></a>Дополнительные сведения
Определение типа является более подробно в спецификации языка F #.


## <a name="see-also"></a>См. также
[Автоматическое обобщение](generics/automatic-generalization.md)