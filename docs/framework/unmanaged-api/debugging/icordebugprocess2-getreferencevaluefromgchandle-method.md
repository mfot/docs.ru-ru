---
title: "Метод ICorDebugProcess2::GetReferenceValueFromGCHandle"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology:
- dotnet-clr
ms.tgt_pltfrm: 
ms.topic: reference
api_name:
- ICorDebugProcess2.GetReferenceValueFromGCHandle
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugProcess2::GetReferenceValueFromGCHandle
helpviewer_keywords:
- GetReferenceValueFromGCHandle method [.NET Framework debugging]
- ICorDebugProcess2::GetReferenceValueFromGCHandle method [.NET Framework debugging]
ms.assetid: 8bdd7f4c-19f2-4ede-875e-603773e8c128
topic_type:
- apiref
caps.latest.revision: 
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.workload:
- dotnet
ms.openlocfilehash: 0ac4cc32be6914ea858d32b8699a695588f0a1e0
ms.sourcegitcommit: 16186c34a957fdd52e5db7294f291f7530ac9d24
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/22/2017
---
# <a name="icordebugprocess2getreferencevaluefromgchandle-method"></a>Метод ICorDebugProcess2::GetReferenceValueFromGCHandle
Получает указатель ссылки на указанный управляемый объект, с дескриптором сборки мусора.  
  
## <a name="syntax"></a>Синтаксис  
  
```  
HRESULT GetReferenceValueFromGCHandle (  
    [in]  UINT_PTR                 handle,  
    [out] ICorDebugReferenceValue  **pOutValue  
);  
```  
  
#### <a name="parameters"></a>Параметры  
 `handle`  
 [in] Указатель на управляемый объект, который имеет дескриптор сборки мусора. Это значение является <xref:System.IntPtr> объекта и может быть извлечен из <xref:System.Runtime.InteropServices.GCHandle> для управляемого объекта.  
  
 `pOutValue`  
 [out] Указатель на адрес объекта ICorDebugReferenceValue, представляющий ссылку на указанный управляемый объект.  
  
## <a name="remarks"></a>Примечания  
 Не следует путать возвращенное значение ссылки со значением коллекции ссылка сборки мусора.  
  
 Возвращаемая ссылка ведет себя как обычной ссылки. Этот параметр отключен, когда выполнение кода продолжается после точки останова. Время существования целевого объекта не зависит от времени существования значения ссылки.  
  
> [!NOTE]
>  `GetReferenceValueFromGCHandle` Метод не проверяет дескриптор. Таким образом `GetReferenceValueFromGCHandle` метода может привести к повреждению отладчика и отлаживаемого, если передается недопустимый дескриптор кода.  
  
## <a name="requirements"></a>Требования  
 **Платформы:** разделе [требования к системе для](../../../../docs/framework/get-started/system-requirements.md).  
  
 **Заголовок:** CorDebug.idl, CorDebug.h  
  
 **Библиотека:** CorGuids.lib  
  
 **Версии платформы .NET framework:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]
