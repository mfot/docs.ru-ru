---
title: "Интерфейс IAssemblyName"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-clr
ms.tgt_pltfrm: 
ms.topic: reference
api_name: IAssemblyName
api_location: fusion.dll
api_type: COM
f1_keywords: IAssemblyName
helpviewer_keywords: IAssemblyName interface [.NET Framework fusion]
ms.assetid: f7f8e605-6b67-4151-936f-f04ecd671d90
topic_type: apiref
caps.latest.revision: "8"
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.openlocfilehash: 1d11889ab9db408b6e703bbaec17fd0487f142a1
ms.sourcegitcommit: 4f3fef493080a43e70e951223894768d36ce430a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/21/2017
---
# <a name="iassemblyname-interface"></a><span data-ttu-id="c5b58-102">Интерфейс IAssemblyName</span><span class="sxs-lookup"><span data-stu-id="c5b58-102">IAssemblyName Interface</span></span>
<span data-ttu-id="c5b58-103">Предоставляет методы для описания и работы с уникальный идентификатор сборки.</span><span class="sxs-lookup"><span data-stu-id="c5b58-103">Provides methods for describing and working with an assembly's unique identity.</span></span>  
  
## <a name="methods"></a><span data-ttu-id="c5b58-104">Методы</span><span class="sxs-lookup"><span data-stu-id="c5b58-104">Methods</span></span>  
  
|<span data-ttu-id="c5b58-105">Метод</span><span class="sxs-lookup"><span data-stu-id="c5b58-105">Method</span></span>|<span data-ttu-id="c5b58-106">Описание</span><span class="sxs-lookup"><span data-stu-id="c5b58-106">Description</span></span>|  
|------------|-----------------|  
|[<span data-ttu-id="c5b58-107">Метод Clone</span><span class="sxs-lookup"><span data-stu-id="c5b58-107">Clone Method</span></span>](../../../../docs/framework/unmanaged-api/fusion/iassemblyname-clone-method.md)|<span data-ttu-id="c5b58-108">Создает неполную копию `IAssemblyName` объекта.</span><span class="sxs-lookup"><span data-stu-id="c5b58-108">Creates a shallow copy of this `IAssemblyName` object.</span></span>|  
|[<span data-ttu-id="c5b58-109">Метод Finalize</span><span class="sxs-lookup"><span data-stu-id="c5b58-109">Finalize Method</span></span>](../../../../docs/framework/unmanaged-api/fusion/iassemblyname-finalize-method.md)|<span data-ttu-id="c5b58-110">Это позволяет `IAssemblyName` объект освободить ресурсы и выполнить другие операции очистки, перед его деструктора.</span><span class="sxs-lookup"><span data-stu-id="c5b58-110">Allows this `IAssemblyName` object to release resources and perform other cleanup operations before its destructor is called.</span></span>|  
|[<span data-ttu-id="c5b58-111">GetDisplayName-метод</span><span class="sxs-lookup"><span data-stu-id="c5b58-111">GetDisplayName Method</span></span>](../../../../docs/framework/unmanaged-api/fusion/iassemblyname-getdisplayname-method.md)|<span data-ttu-id="c5b58-112">Возвращает понятное имя сборки, упоминаемой в этом `IAssemblyName` объекта.</span><span class="sxs-lookup"><span data-stu-id="c5b58-112">Gets the human-readable name of the assembly referenced by this `IAssemblyName` object.</span></span>|  
|[<span data-ttu-id="c5b58-113">Метод GetName</span><span class="sxs-lookup"><span data-stu-id="c5b58-113">GetName Method</span></span>](../../../../docs/framework/unmanaged-api/fusion/iassemblyname-getname-method.md)|<span data-ttu-id="c5b58-114">Получает простое, нешифрованное имя сборки, упоминаемой в этом `IAssemblyName` объекта.</span><span class="sxs-lookup"><span data-stu-id="c5b58-114">Gets the simple, unencrypted name of the assembly referenced by this `IAssemblyName` object.</span></span>|  
|[<span data-ttu-id="c5b58-115">GetProperty — метод</span><span class="sxs-lookup"><span data-stu-id="c5b58-115">GetProperty Method</span></span>](../../../../docs/framework/unmanaged-api/fusion/iassemblyname-getproperty-method.md)|<span data-ttu-id="c5b58-116">Получает указатель ссылается заданный дескриптор свойства `PropertyId`.</span><span class="sxs-lookup"><span data-stu-id="c5b58-116">Gets a pointer to the property referenced by the specified `PropertyId`.</span></span>|  
|[<span data-ttu-id="c5b58-117">GetVersion-метод</span><span class="sxs-lookup"><span data-stu-id="c5b58-117">GetVersion Method</span></span>](../../../../docs/framework/unmanaged-api/fusion/iassemblyname-getversion-method.md)|<span data-ttu-id="c5b58-118">Возвращает сведения о версии для сборки, упоминаемой в этом `IAssemblyName` объекта.</span><span class="sxs-lookup"><span data-stu-id="c5b58-118">Gets the version information for the assembly referenced by this `IAssemblyName` object.</span></span>|  
|[<span data-ttu-id="c5b58-119">Метод IsEqual</span><span class="sxs-lookup"><span data-stu-id="c5b58-119">IsEqual Method</span></span>](../../../../docs/framework/unmanaged-api/fusion/iassemblyname-isequal-method.md)|<span data-ttu-id="c5b58-120">Определяет, является ли заданное `IAssemblyName` объект равен этому `IAssemblyName`, основываясь на флаги сравнения указанного.</span><span class="sxs-lookup"><span data-stu-id="c5b58-120">Determines whether a specified `IAssemblyName` object is equal to this `IAssemblyName`, based on the specified comparison flags.</span></span>|  
|[<span data-ttu-id="c5b58-121">SetProperty — метод</span><span class="sxs-lookup"><span data-stu-id="c5b58-121">SetProperty Method</span></span>](../../../../docs/framework/unmanaged-api/fusion/iassemblyname-setproperty-method.md)|<span data-ttu-id="c5b58-122">Задает значение свойства, который ссылается заданный дескриптор `PropertyId`.</span><span class="sxs-lookup"><span data-stu-id="c5b58-122">Sets the value of the property referenced by the specified `PropertyId`.</span></span>|  
  
## <a name="requirements"></a><span data-ttu-id="c5b58-123">Требования</span><span class="sxs-lookup"><span data-stu-id="c5b58-123">Requirements</span></span>  
 <span data-ttu-id="c5b58-124">**Платформы:** разделе [требования к системе для](../../../../docs/framework/get-started/system-requirements.md).</span><span class="sxs-lookup"><span data-stu-id="c5b58-124">**Platforms:** See [System Requirements](../../../../docs/framework/get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="c5b58-125">**Заголовок:** Fusion.h</span><span class="sxs-lookup"><span data-stu-id="c5b58-125">**Header:** Fusion.h</span></span>  
  
 <span data-ttu-id="c5b58-126">**Версии платформы .NET framework:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="c5b58-126">**.NET Framework Versions:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="c5b58-127">См. также</span><span class="sxs-lookup"><span data-stu-id="c5b58-127">See Also</span></span>  
 [<span data-ttu-id="c5b58-128">Фьюжн-интерфейсы</span><span class="sxs-lookup"><span data-stu-id="c5b58-128">Fusion Interfaces</span></span>](../../../../docs/framework/unmanaged-api/fusion/fusion-interfaces.md)  
 [<span data-ttu-id="c5b58-129">IAssemblyEnum-интерфейс</span><span class="sxs-lookup"><span data-stu-id="c5b58-129">IAssemblyEnum Interface</span></span>](../../../../docs/framework/unmanaged-api/fusion/iassemblyenum-interface.md)