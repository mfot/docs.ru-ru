---
title: "Функция QualifierSet_Put (Справочник по неуправляемым API)"
description: "Функция QualifierSet_Put записывает именованного квалификатора и его значение."
ms.date: 11/06/2017
ms.prod: .net-framework
ms.technology:
- dotnet-clr
ms.topic: reference
api_name:
- QualifierSet_Put
api_location:
- WMINet_Utils.dll
api_type:
- DLLExport
f1_keywords:
- QualifierSet_Put
helpviewer_keywords:
- QualifierSet_Put function [.NET WMI and performance counters]
topic_type:
- Reference
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.workload:
- dotnet
ms.openlocfilehash: 1bf5c6dbf0f707942d58f4d7cf155636f0532724
ms.sourcegitcommit: 16186c34a957fdd52e5db7294f291f7530ac9d24
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/22/2017
---
# <a name="qualifiersetput-function"></a>Функция QualifierSet_Put
Записывает именованный квалификатор и значение. Новый квалификатор перезаписывает предыдущее значение с тем же именем. Если квалификатор не существует, он создается. 

[!INCLUDE[internalonly-unmanaged](../../../../includes/internalonly-unmanaged.md)]
  
## <a name="syntax"></a>Синтаксис  
  
```  
HRESULT QualifierSet_Put (
   [in] int                  vFunc, 
   [in] IWbemQualifierSet*   ptr, 
   [in] LPCWSTR              wszName,
   [in] VARIANT*             pVal,
   [in] LONG                 lFlavor
); 
```  

## <a name="parameters"></a>Параметры

`vFunc`   
[in] Этот параметр не используется.

`ptr`   
[in] Указатель на [IWbemQualifierSet](https://msdn.microsoft.com/library/aa391860(v=vs.85).aspx) экземпляра.

`wszName`   
[in] Имя квалификатора для записи.

`pVal`[in] Указатель на допустимый `VARIANT` , содержащий квалификатор для записи. Этот параметр не может быть `null`.

`lFlavor`[in] Одно из следующих констант, который определяет требуемый квалификаторов для этого квалификатора. Значение по умолчанию — `WBEM_FLAVOR_OVERRIDABLE` (0).

|Константа  |Значение  |Описание  |
|---------|---------|---------|
| `WBEM_FLAVOR_OVERRIDABLE` | 0 | Квалификатор можно переопределить в производный класс или экземпляр. **Это значение по умолчанию.** |
| `WBEM_FLAVOR_FLAG_PROPAGATE_TO_INSTANCE` | 1 | Квалификатор распространяется в экземпляры. |
| `WBEM_FLAVOR_GLAG_PROPAGATE_TO_DERIVED_CLASS` | 2 | Квалификатор распространяется на производные классы. |
| "WBEM_FLAVOR_NOT_OVERRIDABLE | 0x10 | Квалификатор невозможно переопределить в производном классе или экземпляре. |
| "WBEM_FLAVOR_AMENDED | 0x80 | Квалификатор локализован. |

## <a name="return-value"></a>Возвращаемое значение

Следующие значения, возвращаемые этой функцией, определяются в *WbemCli.h* файла заголовка, или их можно определить как константы в коде:

|Константа  |Значение  |Описание:  |
|---------|---------|---------|
| `WBEM_E_CANNOT_BE_KEY` | 0x8004101f | Возникла Недопустимая попытка задать **ключ** квалификатор для свойства, которое не может быть ключом. Указанные ключи om c; ASS Разрешить определение объекта и не может быть изменены для каждого экземпляра. |
| `WBEM_E_INVALID_PARAMETER` | 0x80041008 | Параметр не является допустимым. |
| `WBEM_E_INVALID_QUALIFIER_TYPE` | 0x80041029 | `pVal` Параметр не является правильным типом квалификатора. |
| `WBEM_E_OVERRIDE_NOT_ALLOWED` | 0x8004101a | Невозможно вызвать `QualifierSet_Put` метод квалификатор, поскольку объект-владелец не разрешает переопределения. |
| `WBEM_S_NO_ERROR` | 0 | Успешный вызов функции.  |
  
## <a name="remarks"></a>Примечания

Эта функция создает оболочку для вызова [IWbemQualifierSet::Put](https://msdn.microsoft.com/library/aa391871(v=vs.85).aspx) метод.

## <a name="requirements"></a>Требования  
 **Платформы:** разделе [требования к системе для](../../../../docs/framework/get-started/system-requirements.md).  
  
 **Заголовок:** WMINet_Utils.idl  
  
 **Версии платформы .NET framework:**[!INCLUDE[net_current_v472plus](../../../../includes/net-current-v472plus.md)]  
  
## <a name="see-also"></a>См. также  
[WMI и счетчиков производительности (Справочник по неуправляемым API)](index.md)
