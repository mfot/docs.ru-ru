---
title: "Перечисление CorDebugMappingResult"
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
- CorDebugMappingResult
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- CorDebugMappingResult
helpviewer_keywords:
- CorDebugMappingResult enumeration [.NET Framework debugging]
ms.assetid: 701281dd-2936-45c8-a1f0-3bf7332b093b
topic_type:
- apiref
caps.latest.revision: 
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.workload:
- dotnet
ms.openlocfilehash: 924cfec87b99cba9621af02d4e78e72094060ae8
ms.sourcegitcommit: 16186c34a957fdd52e5db7294f291f7530ac9d24
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/22/2017
---
# <a name="cordebugmappingresult-enumeration"></a>Перечисление CorDebugMappingResult
Предоставляет сведения о том, как было получено значение указателя инструкций.  
  
## <a name="syntax"></a>Синтаксис  
  
```  
typedef enum CorDebugMappingResult {  
    MAPPING_PROLOG              = 0x1,  
    MAPPING_EPILOG              = 0x2,  
    MAPPING_NO_INFO             = 0x4,  
    MAPPING_UNMAPPED_ADDRESS    = 0x8,  
    MAPPING_EXACT               = 0x10,  
    MAPPING_APPROXIMATE         = 0x20,  
} CorDebugMappingResult;  
```  
  
## <a name="members"></a>Участники  
  
|Член|Описание:|  
|------------|-----------------|  
|`MAPPING_PROLOG`|Машинный код находится в прологе, поэтому значение IP равно 0.|  
|`MAPPING_EPILOG`|Машинный код находится в эпилоге, поэтому значение IP-адрес последней инструкции метода.|  
|`MAPPING_NO_INFO`|Нет сведений о сопоставлении для метода, поэтому значение IP равно 0.|  
|`MAPPING_UNMAPPED_ADDRESS`|Хотя сведения о сопоставлении для метода, текущий адрес не может быть сопоставлен код на промежуточном языке (MSIL). IP-адрес равен 0.|  
|`MAPPING_EXACT`|Метод сопоставляет ровно код MSIL, либо была выполнена интерпретация кадра, поэтому значение IP-адреса является точным.|  
|`MAPPING_APPROXIMATE`|Метод успешно сопоставлен, но значение IP-адреса может быть приблизительным.|  
  
## <a name="remarks"></a>Примечания  
 Можно использовать [ICorDebugILFrame::GetIP](../../../../docs/framework/unmanaged-api/debugging/icordebugilframe-getip-method.md) метод получения значения указателя инструкций.  
  
## <a name="requirements"></a>Требования  
 **Платформы:** разделе [требования к системе для](../../../../docs/framework/get-started/system-requirements.md).  
  
 **Заголовок:** CorDebug.idl, CorDebug.h  
  
 **Библиотека:** CorGuids.lib  
  
 **Версии платформы .NET framework:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>См. также  
 [Перечисления отладки](../../../../docs/framework/unmanaged-api/debugging/debugging-enumerations.md)
