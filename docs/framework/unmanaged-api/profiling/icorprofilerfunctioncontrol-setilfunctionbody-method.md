---
title: "Метод ICorProfilerFunctionControl::SetILFunctionBody"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-clr
ms.tgt_pltfrm: 
ms.topic: reference
api_name: ICorProfilerFunctionControl.SetILFunctionBody
api_location: mscorwks.dll
api_type: COM
f1_keywords: ICorProfilerFunctionControl::SetILFunctionBody
helpviewer_keywords:
- ICorProfilerFunctionControl::SetILFunctionBody method [.NET Framework profiling]
- SetILFunctionBody method, ICorProfilerFunctionControl interface [.NET Framework profiling]
ms.assetid: 2c33f0f7-75b2-4c19-b2c7-c94b54997576
topic_type: apiref
caps.latest.revision: "9"
author: mairaw
ms.author: mairaw
manager: wpickett
ms.openlocfilehash: 9469435186a5aef130ca4ebef27a4613afeb921c
ms.sourcegitcommit: bd1ef61f4bb794b25383d3d72e71041a5ced172e
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/18/2017
---
# <a name="icorprofilerfunctioncontrolsetilfunctionbody-method"></a><span data-ttu-id="1159c-102">Метод ICorProfilerFunctionControl::SetILFunctionBody</span><span class="sxs-lookup"><span data-stu-id="1159c-102">ICorProfilerFunctionControl::SetILFunctionBody Method</span></span>
<span data-ttu-id="1159c-103">Заменяет тело метода на языке CIL.</span><span class="sxs-lookup"><span data-stu-id="1159c-103">Replaces the Common Intermediate Language (CIL) body of the method.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="1159c-104">Синтаксис</span><span class="sxs-lookup"><span data-stu-id="1159c-104">Syntax</span></span>  
  
```  
HRESULT SetILFunctionBody(  
    [in]  ULONG   cbNewILMethodHeader,  
    [in, size_is(cbNewILMethodHeader)] LPCBYTE pbNewILMethodHeader);  
```  
  
#### <a name="parameters"></a><span data-ttu-id="1159c-105">Параметры</span><span class="sxs-lookup"><span data-stu-id="1159c-105">Parameters</span></span>  
 `cbNewILMethodHeader`  
 <span data-ttu-id="1159c-106">[in] Общий размер нового кода CIL, включая заголовок и все структуры после тела.</span><span class="sxs-lookup"><span data-stu-id="1159c-106">[in] The total size of the new CIL, including the header and any structures that come after the body.</span></span>  
  
 `pbNewILMethodHeader`  
 <span data-ttu-id="1159c-107">[in] Указатель на новый заголовок на языке CIL.</span><span class="sxs-lookup"><span data-stu-id="1159c-107">[in] A pointer to the new CIL header.</span></span>  
  
## <a name="return-value"></a><span data-ttu-id="1159c-108">Возвращаемое значение</span><span class="sxs-lookup"><span data-stu-id="1159c-108">Return Value</span></span>  
 <span data-ttu-id="1159c-109">Этот метод возвращает следующие специфичные результаты HRESULT.</span><span class="sxs-lookup"><span data-stu-id="1159c-109">This method returns the following specific HRESULTs.</span></span>  
  
|<span data-ttu-id="1159c-110">HRESULT</span><span class="sxs-lookup"><span data-stu-id="1159c-110">HRESULT</span></span>|<span data-ttu-id="1159c-111">Описание</span><span class="sxs-lookup"><span data-stu-id="1159c-111">Description</span></span>|  
|-------------|-----------------|  
|<span data-ttu-id="1159c-112">S_OK</span><span class="sxs-lookup"><span data-stu-id="1159c-112">S_OK</span></span>|<span data-ttu-id="1159c-113">Замена выполнена успешно.</span><span class="sxs-lookup"><span data-stu-id="1159c-113">The replacement was successful.</span></span>|  
  
## <a name="remarks"></a><span data-ttu-id="1159c-114">Примечания</span><span class="sxs-lookup"><span data-stu-id="1159c-114">Remarks</span></span>  
 <span data-ttu-id="1159c-115">В отличие от [ICorProfilerInfo::SetILFunctionBody](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo-setilfunctionbody-method.md) метода `SetILFunctionBody` метод управляет памятью, требуемой для нового тела на языке CIL.</span><span class="sxs-lookup"><span data-stu-id="1159c-115">Unlike the [ICorProfilerInfo::SetILFunctionBody](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo-setilfunctionbody-method.md) method, the `SetILFunctionBody` method manages the memory required for the new CIL body.</span></span> <span data-ttu-id="1159c-116">Это означает, что предоставленное профилировщиком тело на языке CIL не имеет выделенной с помощью [IMethodMalloc](../../../../docs/framework/unmanaged-api/profiling/imethodmalloc-interface.md) интерфейс или в пределах определенного диапазона.</span><span class="sxs-lookup"><span data-stu-id="1159c-116">This means that the CIL body provided by the profiler does not have to be allocated by using the [IMethodMalloc](../../../../docs/framework/unmanaged-api/profiling/imethodmalloc-interface.md) interface or allocated within a particular range.</span></span> <span data-ttu-id="1159c-117">Его можно разместить в любой куче.</span><span class="sxs-lookup"><span data-stu-id="1159c-117">It can be allocated on any heap.</span></span> <span data-ttu-id="1159c-118">Профилировщик может освободить память, используемая для тела на языке CIL после `SetILFunctionBody` возвращает.</span><span class="sxs-lookup"><span data-stu-id="1159c-118">The profiler can free the memory used for its CIL body after `SetILFunctionBody` returns.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="1159c-119">Требования</span><span class="sxs-lookup"><span data-stu-id="1159c-119">Requirements</span></span>  
 <span data-ttu-id="1159c-120">**Платформы:** разделе [требования к системе для](../../../../docs/framework/get-started/system-requirements.md).</span><span class="sxs-lookup"><span data-stu-id="1159c-120">**Platforms:** See [System Requirements](../../../../docs/framework/get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="1159c-121">**Заголовок:** CorProf.idl, CorProf.h</span><span class="sxs-lookup"><span data-stu-id="1159c-121">**Header:** CorProf.idl, CorProf.h</span></span>  
  
 <span data-ttu-id="1159c-122">**Библиотека:** CorGuids.lib</span><span class="sxs-lookup"><span data-stu-id="1159c-122">**Library:** CorGuids.lib</span></span>  
  
 <span data-ttu-id="1159c-123">**Версии платформы .NET framework:**[!INCLUDE[net_current_v45plus](../../../../includes/net-current-v45plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="1159c-123">**.NET Framework Versions:** [!INCLUDE[net_current_v45plus](../../../../includes/net-current-v45plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="1159c-124">См. также</span><span class="sxs-lookup"><span data-stu-id="1159c-124">See Also</span></span>  
 [<span data-ttu-id="1159c-125">Интерфейс ICorProfilerFunctionControl</span><span class="sxs-lookup"><span data-stu-id="1159c-125">ICorProfilerFunctionControl Interface</span></span>](../../../../docs/framework/unmanaged-api/profiling/icorprofilerfunctioncontrol-interface.md)