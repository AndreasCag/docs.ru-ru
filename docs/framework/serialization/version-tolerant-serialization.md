---
title: "Независимая от версий сериализация | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
helpviewer_keywords: 
  - "класс BinaryFormatter, образцы"
  - "сериализация, атрибуты"
  - "сериализация, управление"
  - "сериализация, пользовательская сериализация"
  - "сериализация, независимая от версий"
  - "независимая от версий сериализация"
  - "версии и сериализация"
ms.assetid: bea0ffe3-2708-4a16-ac7d-e586ed6b8e8d
caps.latest.revision: 9
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 9
---
# Независимая от версий сериализация
В платформе .NET Framework версий 1.0 и 1.1 создание сериализуемых типов, которые можно повторно использовать от одной версии приложения к другой, было проблематичным.Если тип был изменен путем добавления дополнительных полей, возникала следующая проблема:  
  
-   Приложения старых версий выдадут исключения при запросе десериализации новых версий старого типа.  
  
-   Приложения более новых версий выдадут исключения при десериализации старых версий типа с отсутствующими данными.  
  
 Независимая от версий сериализация \(VTS\) является набором функций, представленных в платформе .NET Framework 2.0, которые со временем упрощают изменение сериализуемых типов.В частности, функции VTS доступны для классов, к которым применен атрибут <xref:System.SerializableAttribute>, включая универсальные типы.VTS позволяет добавлять новые поля для таких классов, не нарушая совместимости с другими версиями типа.Пример образца работающего приложения см. в разделе [Образец технологии сериализации, независимой от версии](../../../docs/framework/serialization/version-tolerant-serialization-technology-sample.md).  
  
 Функции VTS доступны при использовании <xref:System.Runtime.Serialization.Formatters.Binary.BinaryFormatter>.Кроме того, при использовании <xref:System.Runtime.Serialization.Formatters.Soap.SoapFormatter> доступны все функции, за исключением допустимости лишних данных.Дополнительные сведения об использовании этих классов для сериализации см. в разделе [Двоичная сериализация](../../../docs/framework/serialization/binary-serialization.md).  
  
## Список функций  
 Набор функций включает в себя следующие:  
  
-   Допустимость лишних или непредвиденных данных.Это позволяет новым версиям типа отправлять данные в старые версии.  
  
-   Допустимость отсутствующих необязательных данных.Это позволяет старым версиям отправлять данные в новые версии.  
  
-   Обратные вызовы сериализации.Это обеспечивает интеллектуальную настройку значения по умолчанию в случае отсутствия данных.  
  
 Кроме того, существует функция объявления при добавлении нового необязательного поля.Это свойство <xref:System.Runtime.Serialization.OptionalFieldAttribute.VersionAdded%2A> атрибута <xref:System.Runtime.Serialization.OptionalFieldAttribute>.  
  
 Подробное описание этих функций см. ниже.  
  
## Допустимость лишних или непредвиденных данных  
 В прошлом при десериализации наличие каких\-либо лишних или непредвиденных данных приводило к выводу исключения.С использованием VTS в такой же ситуации какие\-либо лишние или непредвиденные данные игнорируются, и исключения не выводятся.Благодаря этому приложения, использующие более новые версии типа \(т.е. версию с большим числом полей\), могут отправлять информацию в приложения, ожидающие старые версии этого же типа.  
  
 В следующем примере дополнительные данные в `CountryField` версии 2.0 класса `Address` игнорируются, когда более старое приложение десериализует новую версию.  
  
```csharp  
// Version 1 of the Address class.  
[Serializable]  
public class Address  
{  
    public string Street;  
    public string City;  
}  
// Version 2.0 of the Address class.  
[Serializable]  
public class Address  
{  
    public string Street;  
    public string City;  
    // The older application ignores this data.  
    public string CountryField;  
}  
```  
  
```vb  
' Version 1 of the Address class.  
<Serializable> _  
Public Class Address  
    Public Street As String  
    Public City As String  
End Class  
  
' Version 2.0 of the Address class.  
<Serializable> _  
Public Class Address  
    Public Street As String  
    Public City As String  
    ' The older application ignores this data.  
    Public CountryField As String  
End Class  
```  
  
## Допустимость отсутствующих данных  
 Поля можно отметить как необязательные, применив к ним атрибут <xref:System.Runtime.Serialization.OptionalFieldAttribute>.При отсутствии во время десериализации необязательных данных модуль сериализации игнорирует такое отсутствие и не выводит исключение.Поэтому приложения, ожидающие старые версии типа, могут отправлять данные в приложения, ожидающие новые версии этого же типа.  
  
 В следующем примере показана версия 2.0 класса `Address` с полем `CountryField`, отмеченным как необязательное.Если приложение более старой версии отправляет версию 1 в новое приложение, ожидающее версии 2.0, отсутствие данных игнорируется.  
  
```csharp  
[Serializable]  
public class Address  
{  
    public string Street;  
    public string City;  
  
    [OptionalField]  
    public string CountryField;  
}  
```  
  
```vb  
<Serializable> _  
Public Class Address  
    Public Street As String  
    Public City As String  
  
    <OptionalField> _  
    Public CountryField As String  
End Class  
```  
  
## Обратные вызовы сериализации  
 Обратные вызовы сериализации являются механизмом, который предоставляет обработчики для процесса сериализации и десериализации в четырех точках.  
  
|Атрибут|Когда вызывается связанный метод|Типичные случаи использования|  
|-------------|--------------------------------------|-----------------------------------|  
|<xref:System.Runtime.Serialization.OnDeserializingAttribute>|Перед десериализацией.\*|Инициализация значений по умолчанию для необязательных полей.|  
|<xref:System.Runtime.Serialization.OnDeserializedAttribute>|После десериализации.|Исправление значений необязательных полей на основании содержимого других полей.|  
|<xref:System.Runtime.Serialization.OnSerializingAttribute>|Перед сериализацией.|Подготовка к сериализации.Например, создание структур необязательных данных.|  
|<xref:System.Runtime.Serialization.OnSerializedAttribute>|После сериализации.|Регистрация событий сериализации в журнале.|  
  
 \* Этот обратный вызов осуществляется перед конструктором десериализации, если такой имеется.  
  
### Использование обратных вызовов  
 Чтобы использовать обратные вызовы, примените соответствующий атрибут к методу, который принимает параметр <xref:System.Runtime.Serialization.StreamingContext>.Для каждого из этих атрибутов можно отметить только один метод для класса.Например:  
  
```csharp  
[OnDeserializing]  
private void SetCountryRegionDefault(StreamingContext sc)  
{  
    CountryField = "Japan";  
}  
  
```  
  
```vb  
<OnDeserializing>  
Private Sub SetCountryRegionDefault(StreamingContext sc)  
    CountryField = "Japan";  
End Sub  
```  
  
 Эти методы предназначены для управления версиями.Во время десериализации возможна неправильная инициализация необязательного поля, если данные для него отсутствуют.Это можно исправить, создав метод, который назначает правильное значение, а затем применяет к методу атрибут **OnDeserializingAttribute** или **OnDeserializedAttribute**.  
  
 В следующем примере показан метод в контексте типа.Если приложение более ранней версии отправляет экземпляр класса `Address` в приложение более поздней версии, данные поля `CountryField` будут отсутствовать.Но после десериализации полю будет присвоено значение по умолчанию "Japan".  
  
```csharp  
[Serializable]  
public class Address  
{  
    public string Street;  
    public string City;  
    [OptionalField]  
    public string CountryField;  
  
    [OnDeserializing]  
    private void SetCountryRegionDefault (StreamingContext sc)  
    {  
        CountryField = "Japan";  
    }  
}  
  
```  
  
```vb  
<Serializable> _  
Public Class Address  
    Public Street As String  
    Public City As String  
    <OptionalField> _  
    Public CountryField As String  
  
    <OnDeserializing> _  
    Private Sub SetCountryRegionDefault(StreamingContext sc)  
        CountryField = "Japan";  
    End Sub  
End Class  
```  
  
## Свойство VersionAdded  
 **OptionalFieldAttribute** присвоено свойство **VersionAdded**.В платформе .NET Framework версии 2.0 это свойство не используется.Однако важно правильно задать это свойство, чтобы обеспечить совместимость типа с будущими модулями сериализации.  
  
 Свойство содержит сведения о том, какую версию типа добавило указанное поле.Увеличение должно осуществляться точно по одному \(начиная с 2\) при каждом изменении типа, см. следующий пример:  
  
```csharp  
// Version 1.0  
[Serializable]  
public class Person  
{  
    public string FullName;  
}  
  
// Version 2.0  
[Serializable]  
public class Person  
{  
    public string FullName;  
  
    [OptionalField(VersionAdded = 2)]  
    public string NickName;  
    [OptionalField(VersionAdded = 2)]  
    public DateTime BirthDate;  
}  
  
// Version 3.0  
[Serializable]  
public class Person  
{  
    public string FullName;  
  
    [OptionalField(VersionAdded=2)]  
    public string NickName;  
    [OptionalField(VersionAdded=2)]  
    public DateTime BirthDate;  
  
    [OptionalField(VersionAdded=3)]  
    public int Weight;  
}  
```  
  
```vb  
' Version 1.0  
<Serializable> _  
Public Class Person  
    Public FullName  
End Class  
  
' Version 2.0  
<Serializable> _  
Public Class Person  
    Public FullName As String  
  
    <OptionalField(VersionAdded := 2)> _  
    Public NickName As String  
    <OptionalField(VersionAdded := 2)> _  
    Public BirthDate As DateTime  
End Class  
  
' Version 3.0  
<Serializable> _  
Public Class Person  
    Public FullName As String  
  
    <OptionalField(VersionAdded := 2)> _  
    Public NickName As String  
    <OptionalField(VersionAdded := 2)> _  
    Public BirthDate As DateTime  
  
    <OptionalField(VersionAdded := 3)> _  
    Public Weight As Integer  
End Class  
```  
  
## SerializationBinder  
 Некоторым пользователям может понадобиться возможность выбирать классы для сериализации и десериализации, поскольку на сервере и клиенте требуются разные версии класса.Класс <xref:System.RuntimeSerialization.SerializationBinder> является абстрактным классом, который используется для управления фактическими типами, применяемыми при сериализации и десериализации.Чтобы использовать этот класс, создайте класс, производный от <xref:System.RuntimeSerialization.SerializationBinder>, и переопределите методы <xref:System.Runtime.Serialization.SerializationBinder.BindToName%2A> System.String, System.String)?qualifyHint=False&autoUpgrade=True и <xref:System.Runtime.Serialization.SerializationBinder.BindToType%2A> System.String)?qualifyHint=False&autoUpgrade=True.[!INCLUDE[crdefault](../../../includes/crdefault-md.md)][Управление сериализацией и десериализацией с помощью SerializationBinder](../../../docs/framework/wcf/feature-details/controlling-serialization-and-deserialization-with-serializationbinder.md).  
  
## Рекомендации  
 Чтобы обеспечить правильное управление версиями, соблюдайте следующие правила при изменении типа от версии к версии:  
  
-   Никогда не удаляйте сериализованное поле.  
  
-   Никогда не применяйте атрибут <xref:System.NonSerializedAttribute> к полю, если атрибут не был применен к полю в предыдущей версии.  
  
-   Никогда не изменяйте имя или тип сериализованного поля.  
  
-   При добавлении нового сериализованного поля применяйте атрибут **OptionalFieldAttribute**.  
  
-   При удалении атрибута **NonSerializedAttribute** из поля \(которое было несериализуемым в предыдущей версии\) примените атрибут **OptionalFieldAttribute**.  
  
-   Для всех необязательных полей присвойте значимые значения по умолчанию с помощью обратных вызовов сериализации, если 0 или **null** приемлемы в качестве значений по умолчанию.  
  
 Чтобы гарантировать совместимость типа с будущими модулями сериализации, соблюдайте следующие правила:  
  
-   Всегда правильно задавайте свойство **VersionAdded** для атрибута **OptionalFieldAttribute**.  
  
-   Избегайте ветвления версий.  
  
## См. также  
 <xref:System.SerializableAttribute>   
 <xref:System.Runtime.Serialization.Formatters.Binary.BinaryFormatter>   
 <xref:System.Runtime.Serialization.Formatters.Soap.SoapFormatter>   
 <xref:System.Runtime.Serialization.OptionalFieldAttribute.VersionAdded%2A>   
 <xref:System.Runtime.Serialization.OptionalFieldAttribute>   
 <xref:System.Runtime.Serialization.OnDeserializingAttribute>   
 <xref:System.Runtime.Serialization.OnDeserializedAttribute>   
 <xref:System.Runtime.Serialization.OnDeserializingAttribute>   
 <xref:System.Runtime.Serialization.OnSerializedAttribute>   
 <xref:System.Runtime.Serialization.StreamingContext>   
 <xref:System.NonSerializedAttribute>   
 [Двоичная сериализация](../../../docs/framework/serialization/binary-serialization.md)