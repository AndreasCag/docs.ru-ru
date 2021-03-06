---
title: "Подробные сведения о поведении регулярных выражений | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-standard"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "регулярные выражения, поведение"
  - "регулярные выражения .NET Framework, поведение"
ms.assetid: 0ee1a6b8-caac-41d2-917f-d35570021b10
caps.latest.revision: 27
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 27
---
# Подробные сведения о поведении регулярных выражений
Обработчик регулярных выражений .NET Framework выполняет поиск с возвратом для регулярных выражений и является реализацией традиционной NFA\-машины \(недетерминированного конечного автомата\), аналогично тем, которые используются в Perl, Python, Emacs и Tcl.  Это отличает его от более быстрых, но и более ограниченных DFA\-машин \(детерминированный конечный автомат\), предназначенных только для регулярных выражений и используемых в awk, egrep или lex.  Это также отличает его от типовых, но более медленных POSIX NFA\-машин.  В следующем разделе представлено описание трех типов обработчиков регулярных выражений и объясняется причина реализации регулярных выражений в .NET Framework с помощью обычной NFA\-машины.  
  
## Преимущества NFA\-машины  
 Когда DFA\-машины выполняют сопоставление шаблонов, порядок обработки определяется входной строкой.  Машина начинает обработку с начала входной строки и продолжает последовательную обработку для определения соответствия следующего символа шаблону регулярного выражения.  С их помощью можно обнаружить соответствия максимальной длины.  Поскольку DFA\-машины не проверяют один и тот же знак дважды, они не поддерживают поиск с возвратом.  Но поскольку DFA\-машина поддерживает только ограниченный режим работы, она не способна выполнять поиск соответствий по шаблону с обратными ссылками. Кроме того, она не создает явные выражения и не способна выделять части выражения.  
  
 В отличие от DFA\-машин обычные NFA\-машины выполняют поиск соответствий по шаблонам, и порядок обработки определяется шаблоном регулярных выражений.  По мере обработки определенного элемента языка машина использует жадное сопоставление: она выполняет сопоставление как можно большей части входной строки.  И кроме того, она сохраняет свое состояние после успешного поиска соответствия части выражения.  Если поиск соответствия в конечном счете завершился с ошибкой, машина может вернуться в сохраненное состояние, поэтому она может попытаться найти дополнительные соответствия.  Такой процесс оставления успешного соответствия части выражения, при котором последующие элементы языка также могут привести к соответствию, называется *поиск с возвратом*.  NFA\-машины используют поиск с возвратом, проверяя все возможные расширения регулярного выражения в определенном порядке и принимая первое соответствие.  Поскольку обычная NFA\-машина создает определенное расширение регулярного выражения для успешного сопоставления, она способна находить соответствия для частей выражений и обратных ссылок.  Но поскольку обычная NFA\-машина выполняет поиск с возвратом, она может анализировать одно и то же состояние несколько раз, если к нему ведут несколько разных путей.  В результате в наихудшем случае работа может замедляться по экспоненте.  Поскольку обычная NFA\-машина принимает первое найденное соответствие, другие \(возможно, более длинные\) соответствия могут остаться необнаруженными.  
  
 POSIX NFA\-машины похожи на обычные NFA\-машины, за исключением того, что они продолжают поиск с возвратом до тех пор, пока не будет найдено наиболее длинное совпадение.  В результате POSIX NFA\-машина работает медленнее обычной NFA\-машины, и при использовании POSIX NFA\-машины, изменив порядок поиска с возвратом, невозможно задать предпочтение короткому совпадению вместо более длинного.  
  
 Программисты предпочитают обычные NFA\-машины, поскольку они превосходят по возможностям управления строковыми соответствиями обычные DFA\-машины или POSIX NFA\-машины.  Несмотря на то что в наихудшем случае быстродействие NFA\-машин снижается, ими можно управлять так, что поиск соответствий будет проходить по линейному или полиномиальному времени. Добиться этого можно с помощью шаблонов, уменьшающих неоднозначности и ограничивающих количество возвратов.  Другими словами, несмотря на то что NFA\-машины жертвуют производительностью в обмен на мощность и гибкость, в большинстве случаев они обеспечивают хорошую \(или хотя бы приемлемую\) производительность, если регулярное выражение грамотно написано и позволяет избежать ситуаций, при которых производительность поиска с возвратом снижается экспоненциально.  
  
> [!NOTE]
>  Информацию о том, как излишнее использование поиска с возвратом может повлиять на производительность и как избежать проблем, см. в разделе [Поиск с возвратом](../../../docs/standard/base-types/backtracking-in-regular-expressions.md).  
  
## Возможности обработчика .NET Framework  
 В обработчик регулярных выражений .NET Framework были включены лучшие функции NFA\-машины, а также полный набор структурных элементов, позволяющий программистам управлять процессом поиска с возвратом.  Эти структуры можно использовать для ускорения поиска или для выбора предпочтительных расширений.  
  
 Ниже представлены другие возможности обработчика регулярных выражений .NET Framework.  
  
-   Ленивые кванторы: `??`, `*?`, `+?`, `{`*n*`,`*m*`}?`.  Они указывают обработчику вести поиск минимального числа повторений в первую очередь.  Обычные "жадные" кванторы наоборот пытаются в первую очередь найти наибольшее число повторений.  В следующем примере кода демонстрируется различие между двумя кванторами.  Регулярное выражение соответствует предложению, оканчивающемуся на число, и захваченная группа должна извлечь это число.  Регулярное выражение `.+(\d+)\.` содержит жадный квантор `.+`, под влиянием которого обработчик регулярных выражений захватывает только последнюю цифру числа.  И наоборот, регулярное выражение `.+?(\d+)\.` содержит ленивый квантор `.+?`, под влиянием которого обработчик регулярных выражений захватывает все число.  
  
     [!code-csharp[Conceptual.RegularExpressions.Design#1](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.regularexpressions.design/cs/lazy1.cs#1)]
     [!code-vb[Conceptual.RegularExpressions.Design#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.regularexpressions.design/vb/lazy1.vb#1)]  
  
     Определение жадных и ленивых версий этого регулярного выражения представлено в следующей таблице.  
  
    |Шаблон|Описание|  
    |------------|--------------|  
    |`.+` \(жадный квантор\)|Соответствие как минимум одному вхождению любого символа.  Это дает обработчику регулярных выражений команду на сопоставление всей строки и выполнение поиска с возвратом, который требуется для сопоставления оставшейся части шаблона.|  
    |`.+?` \(ленивый квантор\)|Соответствие как минимум одному вхождению любого символа, но как можно меньшему количеству.|  
    |`(\d+)`|Соответствие как минимум одной цифре и назначение ее для первой захваченной группы.|  
    |`\.`|Совпадение с точкой.|  
  
     Дополнительные сведения о ленивых кванторах см. в разделе [Кванторы](../../../docs/standard/base-types/quantifiers-in-regular-expressions.md).  
  
-   Положительный поиск: `(?=`*subexpression*`)`.  Эта функция позволяет обработчику с поиском с возвратом возвращаться в начальное место в тексте после сопоставления части выражения.  Эта функция полезна при осуществлении поиска с одной позиции с помощью нескольких шаблонов.  Она также позволяет обработчику проверять существование части строки в конце соответствия, не включая при этом часть строки в сопоставленный текст.  В следующем примере используется положительный поиск вперед для извлечения слов в предложении, после которых нет знаков препинания.  
  
     [!code-csharp[Conceptual.RegularExpressions.Design#2](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.regularexpressions.design/cs/lookahead1.cs#2)]
     [!code-vb[Conceptual.RegularExpressions.Design#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.regularexpressions.design/vb/lookahead1.vb#2)]  
  
     В таблице ниже представлено определение регулярного выражения `\b[A-Z]+\b(?=\P{P})`.  
  
    |Шаблон|Описание|  
    |------------|--------------|  
    |`\b`|Совпадение должно начинаться на границе слова.|  
    |`[A-Z]+`|Соответствие любой букве, повторяющейся один или несколько раз.  Поскольку метод <xref:System.Text.RegularExpressions.Regex.Matches%2A?displayProperty=fullName> вызывается с помощью параметра <xref:System.Text.RegularExpressions.RegexOptions?displayProperty=fullName>, сравнение зависит от регистра символов.|  
    |`\b`|Совпадение должно заканчиваться на границе слова.|  
    |`(?=\P{P})`|Поиск для определения, является ли следующий символ знаком препинания.  Если не является, соответствие считается успешным.|  
  
     Дополнительные сведения об утверждениях положительного поиска вперед см. в разделе [Конструкции группирования](../../../docs/standard/base-types/grouping-constructs-in-regular-expressions.md).  
  
-   Отрицательный поиск: `(?!`*subexpression*`)`.  Сопоставление выражения выполняется только в том случае, когда не было обнаружено соответствия подвыражения.  Это существенно упрощает поиск, поскольку часто бывает проще описать выражения, не соответствующие правилу, чем само правило.  Например, трудно написать выражение для поиска слов, которые не начинаются с "не".  В следующем примере для их исключения используется отрицательный поиск вперед.  
  
     [!code-csharp[Conceptual.RegularExpressions.Design#3](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.regularexpressions.design/cs/lookahead2.cs#3)]
     [!code-vb[Conceptual.RegularExpressions.Design#3](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.regularexpressions.design/vb/lookahead2.vb#3)]  
  
     Шаблон регулярного выражения `\b(?!non)\w+\b` определяется, как показано в следующей таблице.  
  
    |Шаблон|Описание|  
    |------------|--------------|  
    |`\b`|Совпадение должно начинаться на границе слова.|  
    |`(?!non)`|Поиск вперед для определения, не начинается ли текущая строка с "не".  Если начинается, соответствие считается неудачным.|  
    |`(\w+)`|Совпадение с одним или несколькими символами слова.|  
    |`\b`|Совпадение должно заканчиваться на границе слова.|  
  
     Дополнительные сведения об утверждениях отрицательного поиска вперед см. в разделе [Конструкции группирования](../../../docs/standard/base-types/grouping-constructs-in-regular-expressions.md).  
  
-   Условная оценка: `(?(`*expression*`)`*yes* `|` *no* `)` и `(?(`*name*`)`*yes*.             `|` *no* `)`, где *expression* — сопоставляемая часть выражения, *name* — имя захваченной группы, *yes* — сопоставляемая строка, если *expression* имеет соответствие или *name* является допустимой непустой захваченной группой; а *no* — сопоставляемая часть выражения, если *expression* не имеет соответствия или *name* не является допустимой непустой захваченной группой.  Эта функция позволяет обработчику вести поиск с использованием нескольких альтернативных шаблонов в зависимости от результатов сопоставлений предыдущей части выражения или утверждения нулевой ширины.  Это более действенный вид обратной ссылки, позволяющий, например, искать соответствия части выражения в зависимости от соответствия предыдущей части выражения.  Регулярное выражение в следующем примере соответствует абзацам, предназначенным для общего и внутреннего использования.  Абзацы, предназначенные только для внутреннего использования, начинаются с тега `<PRIVATE>`.  Шаблон регулярного выражения `^(?<Pvt>\<PRIVATE\>\s)?(?(Pvt)((\w+\p{P}?\s)+)|((\w+\p{P}?\s)+))\r?$` использует условную оценку для назначения содержимого абзацев, предназначенных для общего и внутреннего использования, для отдельных захваченных групп.  Поэтому эти абзацы можно обработать по\-разному.  
  
     [!code-csharp[Conceptual.RegularExpressions.Design#4](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.regularexpressions.design/cs/conditional1.cs#4)]
     [!code-vb[Conceptual.RegularExpressions.Design#4](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.regularexpressions.design/vb/conditional1.vb#4)]  
  
     В следующей таблице представлено определение шаблона регулярных выражений.  
  
    |Шаблон|Описание|  
    |------------|--------------|  
    |`^`|Начало совпадения в начале строки.|  
    |`(?<Pvt>\<PRIVATE\>\s)?`|Соответствует вхождениям в количестве 0 или 1 строки `<PRIVATE>`, за которым следует любой знак пробела.  Назначение соответствия для захваченной группы с именем `Pvt`.|  
    |`(?(Pvt)((\w+\p{P}?\s)+)`|Если захваченная группа `Pvt` существует, сопоставление одного или нескольких вхождений одного или нескольких вхождений символов слов, за которыми следует 0 или 1 пунктуационный разделитель с последующим любым пробелом.  Назначение части строки для первой захваченной группы.|  
    |`&#124;((\w+\p{P}?\s)+))`|Если захваченная группа `Pvt` не существует, сопоставление одного или нескольких вхождений одного или нескольких вхождений символов слов, за которыми следует 0 или 1 пунктуационный разделитель с последующим любым пробелом.  Назначение части строки для третьей захваченной группы.|  
    |`\r?$`|Соответствует концу строки.|  
  
     Дополнительные сведения об условной оценке см. в разделе [Конструкции изменения](../../../docs/standard/base-types/alternation-constructs-in-regular-expressions.md).  
  
-   Сбалансированные определения групп: `(?<`*name1*`-`*name2*`>` *subexpression*`)`.  Эта функция позволяет обработчику регулярных выражений отслеживать вложенные конструкции, такие как скобки или открывающие и закрывающие круглые скобки.  Пример см. в разделе [Конструкции группирования](../../../docs/standard/base-types/grouping-constructs-in-regular-expressions.md).  
  
-   Не возвращающаяся \("жадная"\) часть выражения: `(?>`*subexpression*`)`.  Эта функция обеспечивает для подвыражения верность только первого соответствия, как будто выражение запускалось независимо от содержащего его выражения.  Без этой конструкции поиск в большом выражении с использованием поиска с возвратом может изменить поведение части выражения.  Например, регулярное выражение `(a+)\w` соответствует одному или нескольким символам "a" наряду с буквой, после которой идет последовательность символов "a", и назначает последовательность символов "a" для первой захваченной группы. Однако если последний символ входной строки также является символом "a", он соответствует элементу языка `\w` и не входит в захваченную группу.  
  
     [!code-csharp[Conceptual.RegularExpressions.Design#7](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.regularexpressions.design/cs/nonbacktracking2.cs#7)]
     [!code-vb[Conceptual.RegularExpressions.Design#7](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.regularexpressions.design/vb/nonbacktracking2.vb#7)]  
  
     Регулярное выражение `((?>a+))\w` предотвращает такое поведение.  Поскольку все последовательные символы "a" имеют соответствия без поиска с возвратом, первая захваченная группа содержит все последовательные символы "a".  Если после символов "a" не следует ни один символ, отличный от "a", соответствие считается неудачным.  
  
     [!code-csharp[Conceptual.RegularExpressions.Design#8](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.regularexpressions.design/cs/nonbacktracking1.cs#8)]
     [!code-vb[Conceptual.RegularExpressions.Design#8](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.regularexpressions.design/vb/nonbacktracking1.vb#8)]  
  
     Дополнительные сведения о невозвращающихся частях выражений см. в разделе [Конструкции группирования](../../../docs/standard/base-types/grouping-constructs-in-regular-expressions.md).  
  
-   Поиск совпадений справа налево, задаваемый путем передачи параметра <xref:System.Text.RegularExpressions.RegexOptions?displayProperty=fullName> конструктору класса <xref:System.Text.RegularExpressions.Regex> или методу сопоставления статических экземпляров.  Эта функция полезна при поиске справа налево вместо обычного поиска слева направо, а также бывает более эффективно начинать поиск с правой части шаблона, а не с левой.  Как показано в примере ниже, использование поиска соответствий справа налево может изменить поведение жадных кванторов.  В примере выполняется два поисковых запроса предложения, оканчивающегося на число.  При поиске слева направо с использованием жадного квантора `+` имеется соответствие одной из шести цифр в предложении, тогда как при поиске справа налево — всем шести цифрам.  Описание шаблона регулярного выражения см. в примере с ленивыми кванторами выше в этом разделе.  
  
     [!code-csharp[Conceptual.RegularExpressions.Design#6](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.regularexpressions.design/cs/rtl1.cs#6)]
     [!code-vb[Conceptual.RegularExpressions.Design#6](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.regularexpressions.design/vb/rtl1.vb#6)]  
  
     Дополнительные сведения о поиске соответствий справа налево см. в разделе [Параметры регулярных выражений](../../../docs/standard/base-types/regular-expression-options.md).  
  
-   Положительный и отрицательный поиск назад: `(?<=`*subexpression*`)` для положительного поиска назад и `(?<!`*subexpression*`)` для отрицательного поиска назад.  Эта функция аналогична поиску вперед, рассмотренному ранее в этом разделе.  Поскольку обработчик регулярных выражений позволяет выполнять поиск справа налево, к регулярным выражениям можно применять поиск назад без каких\-либо ограничений.  С помощью положительного и отрицательного поиска назад также можно избегать вложенных кванторов, когда вложенная часть выражения является супермножеством внешнего выражения.  Регулярные выражения с такими вложенными кванторами часто являются причиной низкой производительности.  В следующем примере выполняется проверка, начинается ли и оканчивается ли строка с буквы или цифры, и что любой другой символ в строке является символом большего подмножества.  В результате формируется часть регулярного выражения, используемая для проверки адресов электронной почты. Дополнительные сведения см. в разделе [Практическое руководство. Проверка строк на соответствие формату электронной почты](../../../docs/standard/base-types/how-to-verify-that-strings-are-in-valid-email-format.md).  
  
     [!code-csharp[Conceptual.RegularExpressions.Design#5](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.regularexpressions.design/cs/lookbehind1.cs#5)]
     [!code-vb[Conceptual.RegularExpressions.Design#5](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.regularexpressions.design/vb/lookbehind1.vb#5)]  
  
     В таблице ниже представлено определение регулярного выражения `^[A-Z0-9]([-!#$%&'.*+/=?^`{}|~\w])*(?<=[A-Z0-9])$`.  
  
    |Шаблон|Описание|  
    |------------|--------------|  
    |`^`|Начало совпадения в начале строки.|  
    |`[A-Z0-9]`|Поиск какой\-либо цифры или буквы. \(При сравнении регистр учитывается.\)|  
    |`([-!#$%&'.*+/=?^`{}&#124;~\w])*`|Соответствие 0 или нескольким вхождениям любого символа слова или любого следующего символа: \-, \!, \#, $, %, &, ', ., \*, \+, \/, \=, ?, ^, \`, {, }, &#124; или ~.|  
    |`(?<=[A-Z0-9])`|Поиск назад предыдущего символа, который должен являться числом или буквенно\-цифровым символом. \(При сравнении регистр учитывается.\)|  
    |`$`|Совпадение должно заканчиваться в конце строки.|  
  
     Дополнительные сведения о положительном и отрицательном поиске назад см. в разделе [Конструкции группирования](../../../docs/standard/base-types/grouping-constructs-in-regular-expressions.md).  
  
## Связанные разделы  
  
|Название|Описание|  
|--------------|--------------|  
|[Поиск с возвратом](../../../docs/standard/base-types/backtracking-in-regular-expressions.md)|Сведения об использовании поиска с возвратом для поиска альтернативных соответствий.|  
|[Компиляция и многократное использование](../../../docs/standard/base-types/compilation-and-reuse-in-regular-expressions.md)|Сведения о компиляции и многократном использовании регулярных выражений для повышения производительности.|  
|[Потокобезопасность](../../../docs/standard/base-types/thread-safety-in-regular-expressions.md)|Сведения о потокобезопасности регулярных выражений и времени синхронизации доступа к объектам регулярных выражений.|  
|[Регулярные выражения в .NET Framework](../../../docs/standard/base-types/regular-expressions.md)|Общие сведения о регулярных выражениях в контексте языка программирования.|  
|[Объектная модель регулярных выражений](../../../docs/standard/base-types/the-regular-expression-object-model.md)|Примеры кода и сведения по использованию классов регулярных выражений.|  
|[Примеры регулярных выражений](../../../docs/standard/base-types/regular-expression-examples.md)|Примеры кодов, иллюстрирующих использование регулярных выражений в обычных приложениях.|  
|[Элементы языка регулярных выражений — краткий справочник](../../../docs/standard/base-types/regular-expression-language-quick-reference.md)|Сведения о символах, операторах и конструкциях, используемых для определения регулярных выражений.|  
  
## Справочные сведения  
 <xref:System.Text.RegularExpressions?displayProperty=fullName>