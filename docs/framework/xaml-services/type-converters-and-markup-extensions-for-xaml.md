---
title: "Type Converters and Markup Extensions for XAML | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-wpf"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "XAML [XAML Services], type converter services"
  - "XAML [XAML Services], value converters"
  - "XAML [XAML Services], markup extension services"
  - "value converters for XAML [XAML Services]"
  - "XAML [XAML Services], service context"
ms.assetid: db07a952-05ce-4aa4-b6f9-aac7397d0326
caps.latest.revision: 13
author: "wadepickett"
ms.author: "wpickett"
manager: "wpickett"
caps.handback.revision: 12
---
# Type Converters and Markup Extensions for XAML
Преобразователи типов и расширения разметки — это два метода, используемых системами типов XAML и средствами записи XAML для создания компонентов графа объектов. Хотя они обладают общими характеристиками, преобразователи типов и расширения разметки представляются по\-разному в потоке узлов XAML. В этой документации преобразователи типов, расширения разметки и аналогичные конструкции иногда называются преобразователями значений.  
  
<a name="value_converters"></a>   
## Преобразователи значений  
 В XAML преобразователи значений используются для различных сценариев. Ниже перечислены различные типы преобразователей значений в XAML.  
  
-   Преобразователь типов  
  
-   Расширение разметки  
  
-   Сериализатор значений  
  
-   Связанный класс или вспомогательный класс, предоставляющий логику для текстового синтаксиса XAML.  
  
<a name="type_converters"></a>   
## Преобразователи типов  
 Согласно определению служб XAML .NET Framework преобразователи типов — это классы, производные от класса <xref:System.ComponentModel.TypeConverter> среды CLR.<xref:System.ComponentModel.TypeConverter> — это класс, используемый в [!INCLUDE[TLA#tla_netframewk](../../../includes/tlasharptla-netframewk-md.md)] до появления XAML. Его первоначальное назначение заключалось в поддержке окон свойств и аналогичных текстовых метафор для редактирования свойств [!INCLUDE[TLA2#tla_ide](../../../includes/tla2sharptla-ide-md.md)]. После реализации XAML в .NET Framework платформа использует <xref:System.ComponentModel.TypeConverter> для преобразования текстового синтаксиса \(в значении атрибута или в узле значения XAML\) в объект. <xref:System.ComponentModel.TypeConverter> может также использоваться для сериализации значения объекта в текстовый синтаксис.<xref:System.ComponentModel.TypeConverter> также применялся в предыдущих реализациях XAML для отдельных платформ в [!INCLUDE[TLA#tla_wpf](../../../includes/tlasharptla-wpf-md.md)] и [!INCLUDE[vsindigo](../../../includes/vsindigo-md.md)]. Дополнительные сведения о <xref:System.ComponentModel.TypeConverter> в XAML см. в разделе [Type Converters for XAML Overview](../../../docs/framework/xaml-services/type-converters-for-xaml-overview.md).  
  
<a name="markup_extensions"></a>   
## Расширения разметки  
 Согласно определению служб XAML .NET Framework расширения разметки — это классы, производные от класса <xref:System.Windows.Markup.MarkupExtension>. Расширения разметки — это понятие, которое возникло в языке XAML. Расширение разметки можно представить чем\-то вроде расширяемой Escape\-последовательности, вызывающей класс службы для реализации своей логики. С точки зрения разметки обработчики XAML всегда распознают расширение разметки как текстовую последовательность, начинающуюся с открывающей фигурной скобки \({}\) в текстовой строке.  
  
 Расширения разметки отличаются от преобразователей типов. Преобразователи типов обычно связаны с типами или членами. Они вызываются при создании графа объектов или при обнаружении текстового синтаксиса, связанного с этими сущностями, во время сериализации.  
  
 Расширения разметки связаны с отдельным вспомогательным классом службы, но могут применяться к любому значению члена. \(Однако вы можете реализовать расширение разметки, чтобы намеренно ограничить его использование определенными членами или конечными типами с помощью контекста службы.\) Расширения разметки могут переопределять ассоциации преобразователей типов. Кроме того, их можно использовать, чтобы указать значение атрибута для членов, которые в противном случае не поддерживают текстовый синтаксис.  
  
 Дополнительные сведения о реализации шаблона расширения разметки для XAML см. в разделе [Markup Extensions for XAML Overview](../../../docs/framework/xaml-services/markup-extensions-for-xaml-overview.md).  
  
> [!NOTE]
>  Типы <xref:System.Windows.Markup.MarkupExtension> и <xref:System.Windows.Markup.ValueSerializer> находятся в пространстве имен <xref:System.Windows.Markup>, а не в <xref:System.Xaml>. Из этого не следует, что эти типы относятся к технологии WPF или [!INCLUDE[TLA2#tla_winforms](../../../includes/tla2sharptla-winforms-md.md)], которые заполняют пространства имен CLR, содержащие строку `Windows`.<xref:System.Windows.Markup.MarkupExtension> и <xref:System.Windows.Markup.ValueSerializer> находятся в сборке System.Xaml и не зависят от конкретной платформы. Эти типы существовали в пространстве имен среды CLR для [!INCLUDE[net_v30_short](../../../includes/net-v30-short-md.md)] и остаются в нем в [!INCLUDE[net_v40_short](../../../includes/net-v40-short-md.md)] для предотвращения повреждения ссылок в существующих проектах WPF. Для получения дополнительной информации см. [Types Migrated from WPF to System.Xaml](../../../docs/framework/xaml-services/types-migrated-from-wpf-to-system-xaml.md).  
  
<a name="value_serializers"></a>   
## Сериализаторы значений  
 <xref:System.Windows.Markup.ValueSerializer> — это специализированные преобразователь типов, оптимизированный для преобразования объекта в строку. Объект <xref:System.Windows.Markup.ValueSerializer> для XAML не может реализовывать метод `ConvertFrom`. Реализация <xref:System.Windows.Markup.ValueSerializer> получает службы так, будто это реализация <xref:System.ComponentModel.TypeConverter>. Виртуальные методы предоставляют входной параметр `context`. Параметр `context` имеет тип <xref:System.Windows.Markup.IValueSerializerContext>, который наследуется от интерфейса <xref:System.IServiceProvider> и содержит метод <xref:System.IServiceProvider.GetService%2A>.  
  
 В системе типов XAML и реализациях средств записи XAML, которые используют циклическую обработку узлов XAML для сериализации,преобразователь значений, связанный с типом или членом, доступен по собственному свойству <xref:System.Xaml.XamlType.ValueSerializer%2A?displayProperty=fullName>. Для средств записи XAML, выполняющих сериализацию, это значит, что если <xref:System.Xaml.XamlType.TypeConverter%2A?displayProperty=fullName> и <xref:System.Xaml.XamlType.ValueSerializer%2A?displayProperty=fullName> существуют, преобразователь типов можно использовать для пути загрузки, а сериализатор значений — для пути сохранения. Если <xref:System.Xaml.XamlType.TypeConverter%2A?displayProperty=fullName> существует, но <xref:System.Xaml.XamlType.ValueSerializer%2A?displayProperty=fullName> — `null`, преобразователь типов также используется для пути сохранения.  
  
<a name="other_value_converters"></a>   
## Другие преобразователи значений  
 Преобразователь значений можно расширить за границы конкретных шаблонов преобразователя типов или расширения разметки. Однако для такой настройки также потребуется переопределение системы типов XAML, предоставленной службами XAML .NET Framework. Существующая система типов XAML содержит представления и системы отчетности для преобразователей типов, расширений разметки и сериализаторов значений, но не для пользовательских форм преобразования значений. Если вам требуется создать пользовательские преобразователи значений, используйте тип <xref:System.Xaml.Schema.XamlValueConverter%601>.  
  
<a name="type_converters_and_markup_extensions_in_combination"></a>   
## Сочетание преобразователей типов и расширений разметки  
 Расширения разметки и преобразователи типов используются в языке XAML в различных ситуациях. Хотя для расширения разметки контекст доступен, поведение преобразования типов свойств, когда расширение разметки предоставляет значение, обычно не включается в реализацию расширения разметки. Другими словами, даже если расширение разметки возвращает текстовую строку в качестве выходных данных `ProvideValue`, преобразование типа для этой строки относительно конкретного свойства или типа значения свойства не применяется. Как правило, цель расширения разметки — обработать строку и вернуть объект без участия какого\-либо преобразователя типов.  
  
<a name="service_context_for_a_value_converter"></a>   
## Контекст службы для преобразователя значений  
 При реализации преобразователя значений часто требуется доступ к контексту, в котором он применяется. Этот контекст называют контекстом службы. Контекст службы может включать в себя такие сведения, как контекст активной схемы XAML, доступ к системе сопоставления типов, предоставляемый контекстом схемы XAML и средством записи объектов XAML, и т. д. Дополнительные сведения о контекстах служб, доступных для преобразователя значений, и способах доступа к службам, которые могут предоставить контекст службы, см. в разделе [Service Contexts Available to Type Converters and Markup Extensions](../../../docs/framework/xaml-services/service-contexts-available-to-type-converters-and-markup-extensions.md).  
  
## См. также  
 <xref:System.Windows.Markup.MarkupExtension>   
 <xref:System.Xaml.XamlObjectWriter>   
 [Markup Extensions for XAML Overview](../../../docs/framework/xaml-services/markup-extensions-for-xaml-overview.md)   
 [Type Converters for XAML Overview](../../../docs/framework/xaml-services/type-converters-for-xaml-overview.md)   
 [Service Contexts Available to Type Converters and Markup Extensions](../../../docs/framework/xaml-services/service-contexts-available-to-type-converters-and-markup-extensions.md)