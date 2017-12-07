---
title: "Функция PutClassWmi (Справочник по неуправляемым API)"
description: "Функция PutClassWmi создает новый класс, или обновляет существующую."
ms.date: 11/06/2017
ms.prod: .net-framework
ms.technology: dotnet-clr
ms.topic: reference
api_name: PutClassWmi
api_location: WMINet_Utils.dll
api_type: DLLExport
f1_keywords: PutClassWmi
helpviewer_keywords: PutClassWmi function [.NET WMI and performance counters]
topic_type: Reference
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.openlocfilehash: dda7dc4d71b65c8b031f2dca459bd282eef1f270
ms.sourcegitcommit: a53799f81351ad9afb3007cd68846ce6aeeb10cb
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/15/2017
---
# <a name="putclasswmi-function"></a>Функция PutClassWmi
Создает новый класс, или обновляет существующую.  

[!INCLUDE[internalonly-unmanaged](../../../../includes/internalonly-unmanaged.md)]
  
## <a name="syntax"></a>Синтаксис  
  
```  
HRESULT PutClassWmi (
   [in] IWbemClassObject*    pObject,
   [in] long                 lFlags,
   [in] IWbemContext*        pCtx,
   [out] IWbemCallResult**   ppCallResult
); 
```  

## <a name="parameters"></a>Параметры

`pObject`    
[in] Указатель является допустимым определением класса. Необходимо правильно инициализировать со всеми значениями обязательное свойство.

`lFlags`   
[in] Сочетание флагов, влияющих на поведение этой функции. Следующие значения определяются в *WbemCli.h* файла заголовка, или их можно определить как константы в коде: 

|Константа  |Значение  |Описание  |
|---------|---------|---------|
| `WBEM_FLAG_USE_AMENDED_QUALIFIERS` | 0x20000 | Если набор WMI не сохраняет любые квалификаторы с измененные версии. </br> В противном случае набор, предполагается этот объект не локализован, что все квалификаторы — storedwith данного экземпляра. |
| `WBEM_FLAG_CREATE_OR_UPDATE` | 0 | Создайте класс, если она не существует, или перезаписать его, если он уже существует. |
| `WBEM_FLAG_UPDATE_ONLY` | 1 | Обновите класс. Класс должен существовать для успешного вызова. |
| `WBEM_FLAG_CREATE_ONLY` | 2 | Создание класса. Вызов завершается неудачей, если класс уже существует. |
| `WBEM_FLAG_RETURN_IMMEDIATELY` | 0x10 | Флаг вызывает полусинхронных вызовов. |
| `WBEM_FLAG_OWNER_UPDATE` | 0x10000 | Принудительная поставщики должны указывать этот флаг, при вызове `PutClassWmi` для указания, что этот класс был изменен. |
| `WBEM_FLAG_UPDATE_COMPATIBLE` | 0 | Позволяет класс обновляться, если не производные классы и экземпляры этого класса не существует. Она также позволяет обновлений во всех случаях, если изменение выполнено лишь в незначительной квалификаторы, например квалификатор описания. Если класс имеет экземпляры или изменения относятся к важным квалификаторы, обновление завершается ошибкой. |
| `WBEM_FLAG_UPDATE_SAFE_MODE` | 0x20 | Обеспечивает обновление классов даже при наличии дочерних классов, при условии, что изменение не вызовет конфликты с дочерними классами. Например этот флаг позволяет новое свойство для добавления базового класса, который не упоминался ранее в любом дочернем классе. Если класс имеет экземпляры, обновление не выполнено. |
| `WBEM_FLAG_UPDATE_FORCE_MODE` | 0x40 | Вызывает принудительное обновление классов при наличии конфликтующих дочерних классов. Например этот флаг принудительное обновление, если квалификатор определена в дочернем классе, и пытается добавить же квалификатор, который конфликтует с существующие один thte базового класса. В принудительном режиме tis конфликт разрешается путем удаления квалификатора в дочернем классе. |

`pCtx`  
[in] Как правило, это значение равно `null`. В противном случае он является указателем на [IWbemContext](https://msdn.microsoft.com/library/aa391465(v=vs.85).aspx) экземпляр, который может использоваться поставщиком, предоставляющего запрошенного классы. 

`ppCallResult`  
[out] Если `null`, этот параметр не используется. Если `lFlags` содержит `WBEM_FLAG_RETURN_IMMEDIATELY`, функция немедленно возвращает `WBEM_S_NO_ERROR`. `ppCallResult` Параметр получает указатель на новый [IWbemCallResult](https://msdn.microsoft.com/library/aa391425(v=vs.85).aspx) объекта.

## <a name="return-value"></a>Возвращаемое значение

Следующие значения, возвращаемые этой функцией, определяются в *WbemCli.h* файла заголовка, или их можно определить как константы в коде:

|Константа  |Значение  |Описание  |
|---------|---------|---------|
| `WBEM_E_ACCESS_DENIED` | 0x80041003 | Пользователь не имеет разрешения на создание или изменение классы. |
| `WBEM_E_FAILED` | 0x80041001 | Произошла неизвестная ошибка. |
| `WBEM_E_INVALID_CLASS` | 0x80041010 | Указанный класс не является допустимым. Как правило, это означает, что `pObject` указывает экземпляр объекта. |
| `WBEM_E_INVALID_PARAMETER` | 0x80041008 | Параметр не является допустимым. |
| `WBEM_E_INVALID OPERATION` | 0x80041016 | Недопустимое имя указанного класса. |
| `WBEM_E_CLASS_HAS_CHILDREN` | 0x80041025 | Попытка сделать изменение, которое аннулирует подкласс. |
| `WBEM_E_ALREADY_EXISTS` | 0x80041019 | `WBEM_FLAG_CREATE_ONLY` Был указан флаг, но класс уже существует. |
| `WBEM_E_NOT_FOUND` | 0x80041002 | `WBEM_FLAG_UPDATE_ONLY`был указан в `lFlags`, и этот класс не найден. |
| `WBEM_E_INCOMPLETE_CLASS` | 0x80041020 | Требуемые свойства для классов, не все заданы. |
| `WBEM_E_OUT_OF_MEMORY` | 0x80041006 | Недостаточно памяти для завершения операции. |
| `WBEM_E_SHUTTING_DOWN` | 0x80041033 | WMI был, скорее всего, остановлен и перезапускать. Вызовите [ConnectServerWmi](connectserverwmi.md) еще раз. |
| `WBEM_E_TRANSPORT_FAILURE` | 0x80041015 | Не удалось выполнить вызов RPC удаленной процедуры связь между текущим процессом и WMI. |
| `WBEM_S_NO_ERROR` | 0 | Успешный вызов функции.  |
  
## <a name="remarks"></a>Примечания

Эта функция создает оболочку для вызова [IWbemServices::PutClass](https://msdn.microsoft.com/library/aa392113(v=vs.85).aspx) метод.

Пользователь не может создать классы, имена которых начинаться или заканчиваться символом подчеркивания chacater

При сбое вызова функции, можно получить дополнительные сведения об ошибке, вызвав [GetErrorInfo](geterrorinfo.md) функции.

## <a name="requirements"></a>Требования  
 **Платформы:** разделе [требования к системе для](../../../../docs/framework/get-started/system-requirements.md).  
  
 **Заголовок:** WMINet_Utils.idl  
  
 **Версии платформы .NET framework:**[!INCLUDE[net_current_v472plus](../../../../includes/net-current-v472plus.md)]  
  
## <a name="see-also"></a>См. также  
[WMI и счетчиков производительности (Справочник по неуправляемым API)](index.md)