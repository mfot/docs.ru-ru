---
title: "ICorDebugFunction2 интерфейс1"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-clr
ms.tgt_pltfrm: 
ms.topic: reference
api_name: ICorDebugFunction2
api_location: mscordbi.dll
api_type: COM
f1_keywords: ICorDebugFunction2
helpviewer_keywords: ICorDebugFunction2 interface [.NET Framework debugging]
ms.assetid: 2b936bef-9b75-48bf-859f-42e419c65f1c
topic_type: apiref
caps.latest.revision: "12"
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.openlocfilehash: 4c2806003e06d00a492568d1e2d86add66b5f0ee
ms.sourcegitcommit: bd1ef61f4bb794b25383d3d72e71041a5ced172e
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/18/2017
---
# <a name="icordebugfunction2-interface1"></a><span data-ttu-id="e33e0-102">ICorDebugFunction2 интерфейс1</span><span class="sxs-lookup"><span data-stu-id="e33e0-102">ICorDebugFunction2 Interface1</span></span>
<span data-ttu-id="e33e0-103">Логически расширяет интерфейс ICorDebugFunction для обеспечения поддержки только мой код отладки в пошаговом режиме, который пропускает непользовательском коде.</span><span class="sxs-lookup"><span data-stu-id="e33e0-103">Logically extends the ICorDebugFunction interface to provide support for Just My Code step-through debugging, which skips non-user code.</span></span>  
  
## <a name="methods"></a><span data-ttu-id="e33e0-104">Методы</span><span class="sxs-lookup"><span data-stu-id="e33e0-104">Methods</span></span>  
  
|<span data-ttu-id="e33e0-105">Метод</span><span class="sxs-lookup"><span data-stu-id="e33e0-105">Method</span></span>|<span data-ttu-id="e33e0-106">Описание</span><span class="sxs-lookup"><span data-stu-id="e33e0-106">Description</span></span>|  
|------------|-----------------|  
|[<span data-ttu-id="e33e0-107">Метод EnumerateNativeCode</span><span class="sxs-lookup"><span data-stu-id="e33e0-107">EnumerateNativeCode Method</span></span>](../../../../docs/framework/unmanaged-api/debugging/icordebugfunction2-enumeratenativecode-method.md)|<span data-ttu-id="e33e0-108">(Еще не реализован). Получает указатель на интерфейс ICorDebugCodeEnum, содержащий инструкции машинного кода в функцию, который ссылается данный объект ICorDebugFunction2.</span><span class="sxs-lookup"><span data-stu-id="e33e0-108">(Not yet implemented.) Gets an interface pointer to an ICorDebugCodeEnum that contains the native code statements in the function referenced by this ICorDebugFunction2 object.</span></span>|  
|[<span data-ttu-id="e33e0-109">Метод GetJMCStatus</span><span class="sxs-lookup"><span data-stu-id="e33e0-109">GetJMCStatus Method</span></span>](../../../../docs/framework/unmanaged-api/debugging/icordebugfunction2-getjmcstatus-method.md)|<span data-ttu-id="e33e0-110">Возвращает значение, указывающее, помечена ли данная функция как пользовательский код.</span><span class="sxs-lookup"><span data-stu-id="e33e0-110">Gets a value that indicates whether this function is marked as user code.</span></span>|  
|[<span data-ttu-id="e33e0-111">Метод GetVersionNumber</span><span class="sxs-lookup"><span data-stu-id="e33e0-111">GetVersionNumber Method</span></span>](../../../../docs/framework/unmanaged-api/debugging/icordebugfunction2-getversionnumber-method.md)|<span data-ttu-id="e33e0-112">Возвращает версию этой функции изменить и продолжить.</span><span class="sxs-lookup"><span data-stu-id="e33e0-112">Gets the Edit and Continue version of this function.</span></span>|  
|[<span data-ttu-id="e33e0-113">Метод SetJMCStatus</span><span class="sxs-lookup"><span data-stu-id="e33e0-113">SetJMCStatus Method</span></span>](../../../../docs/framework/unmanaged-api/debugging/icordebugfunction2-setjmcstatus-method.md)|<span data-ttu-id="e33e0-114">Обозначает эту функцию только мой код пошаговое выполнение.</span><span class="sxs-lookup"><span data-stu-id="e33e0-114">Marks this function for Just My Code stepping.</span></span>|  
  
## <a name="remarks"></a><span data-ttu-id="e33e0-115">Примечания</span><span class="sxs-lookup"><span data-stu-id="e33e0-115">Remarks</span></span>  
  
> [!NOTE]
>  <span data-ttu-id="e33e0-116">Этот интерфейс не поддерживает удаленные вызовы между компьютерами или между процессами.</span><span class="sxs-lookup"><span data-stu-id="e33e0-116">This interface does not support being called remotely, either cross-machine or cross-process.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="e33e0-117">Требования</span><span class="sxs-lookup"><span data-stu-id="e33e0-117">Requirements</span></span>  
 <span data-ttu-id="e33e0-118">**Платформы:** разделе [требования к системе для](../../../../docs/framework/get-started/system-requirements.md).</span><span class="sxs-lookup"><span data-stu-id="e33e0-118">**Platforms:** See [System Requirements](../../../../docs/framework/get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="e33e0-119">**Заголовок:** CorDebug.idl, CorDebug.h</span><span class="sxs-lookup"><span data-stu-id="e33e0-119">**Header:** CorDebug.idl, CorDebug.h</span></span>  
  
 <span data-ttu-id="e33e0-120">**Библиотека:** CorGuids.lib</span><span class="sxs-lookup"><span data-stu-id="e33e0-120">**Library:** CorGuids.lib</span></span>  
  
 <span data-ttu-id="e33e0-121">**Версии платформы .NET framework:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="e33e0-121">**.NET Framework Versions:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="e33e0-122">См. также</span><span class="sxs-lookup"><span data-stu-id="e33e0-122">See Also</span></span>  
 [<span data-ttu-id="e33e0-123">Интерфейсы отладки</span><span class="sxs-lookup"><span data-stu-id="e33e0-123">Debugging Interfaces</span></span>](../../../../docs/framework/unmanaged-api/debugging/debugging-interfaces.md)