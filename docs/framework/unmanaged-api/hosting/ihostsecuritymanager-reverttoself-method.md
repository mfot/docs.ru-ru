---
title: "Метод IHostSecurityManager::RevertToSelf"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-clr
ms.tgt_pltfrm: 
ms.topic: reference
api_name: IHostSecurityManager.RevertToSelf
api_location: mscoree.dll
api_type: COM
f1_keywords: IHostSecurityManager::RevertToSelf
helpviewer_keywords:
- RevertToSelf method [.NET Framework hosting]
- IHostSecurityManager::RevertToSelf method [.NET Framework hosting]
ms.assetid: 189f28f8-f9a1-4192-aedc-91084e4f8b99
topic_type: apiref
caps.latest.revision: "10"
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.openlocfilehash: 0fad325bc3df54f412a797e9944f5b1f38615786
ms.sourcegitcommit: 4f3fef493080a43e70e951223894768d36ce430a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/21/2017
---
# <a name="ihostsecuritymanagerreverttoself-method"></a><span data-ttu-id="6455d-102">Метод IHostSecurityManager::RevertToSelf</span><span class="sxs-lookup"><span data-stu-id="6455d-102">IHostSecurityManager::RevertToSelf Method</span></span>
<span data-ttu-id="6455d-103">Завершает олицетворение удостоверения текущего пользователя и возвращает исходный маркер потока.</span><span class="sxs-lookup"><span data-stu-id="6455d-103">Terminates impersonation of the current user identity and returns the original thread token.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="6455d-104">Синтаксис</span><span class="sxs-lookup"><span data-stu-id="6455d-104">Syntax</span></span>  
  
```  
HRESULT RevertToSelf ();  
```  
  
## <a name="return-value"></a><span data-ttu-id="6455d-105">Возвращаемое значение</span><span class="sxs-lookup"><span data-stu-id="6455d-105">Return Value</span></span>  
  
|<span data-ttu-id="6455d-106">HRESULT</span><span class="sxs-lookup"><span data-stu-id="6455d-106">HRESULT</span></span>|<span data-ttu-id="6455d-107">Описание</span><span class="sxs-lookup"><span data-stu-id="6455d-107">Description</span></span>|  
|-------------|-----------------|  
|<span data-ttu-id="6455d-108">S_OK</span><span class="sxs-lookup"><span data-stu-id="6455d-108">S_OK</span></span>|<span data-ttu-id="6455d-109">`RevertToSelf`успешно возвращен.</span><span class="sxs-lookup"><span data-stu-id="6455d-109">`RevertToSelf` returned successfully.</span></span>|  
|<span data-ttu-id="6455d-110">ЗНАЧЕНИЕ HOST_E_CLRNOTAVAILABLE</span><span class="sxs-lookup"><span data-stu-id="6455d-110">HOST_E_CLRNOTAVAILABLE</span></span>|<span data-ttu-id="6455d-111">Общеязыковая среда выполнения (CLR) не был загружен в процесс или находится в состоянии, в котором не может выполнять управляемый код или успешно обработать вызов.</span><span class="sxs-lookup"><span data-stu-id="6455d-111">The common language runtime (CLR) has not been loaded into a process, or the CLR is in a state in which it cannot run managed code or process the call successfully.</span></span>|  
|<span data-ttu-id="6455d-112">HOST_E_TIMEOUT</span><span class="sxs-lookup"><span data-stu-id="6455d-112">HOST_E_TIMEOUT</span></span>|<span data-ttu-id="6455d-113">Истекло время ожидания вызова.</span><span class="sxs-lookup"><span data-stu-id="6455d-113">The call timed out.</span></span>|  
|<span data-ttu-id="6455d-114">HOST_E_NOT_OWNER</span><span class="sxs-lookup"><span data-stu-id="6455d-114">HOST_E_NOT_OWNER</span></span>|<span data-ttu-id="6455d-115">Вызывающий объект не является владельцем блокировки.</span><span class="sxs-lookup"><span data-stu-id="6455d-115">The caller does not own the lock.</span></span>|  
|<span data-ttu-id="6455d-116">HOST_E_ABANDONED</span><span class="sxs-lookup"><span data-stu-id="6455d-116">HOST_E_ABANDONED</span></span>|<span data-ttu-id="6455d-117">Событие было отменено заблокированный поток или ожидал волокон.</span><span class="sxs-lookup"><span data-stu-id="6455d-117">An event was canceled while a blocked thread or fiber was waiting on it.</span></span>|  
|<span data-ttu-id="6455d-118">E_FAIL</span><span class="sxs-lookup"><span data-stu-id="6455d-118">E_FAIL</span></span>|<span data-ttu-id="6455d-119">Неизвестная Неустранимая ошибка.</span><span class="sxs-lookup"><span data-stu-id="6455d-119">An unknown catastrophic failure occurred.</span></span> <span data-ttu-id="6455d-120">Если метод вернет значение E_FAIL, среда CLR больше не может использоваться в процессе.</span><span class="sxs-lookup"><span data-stu-id="6455d-120">When a method returns E_FAIL, the CLR is no longer usable within the process.</span></span> <span data-ttu-id="6455d-121">Последующие вызовы размещение методы возвращают значение HOST_E_CLRNOTAVAILABLE.</span><span class="sxs-lookup"><span data-stu-id="6455d-121">Subsequent calls to hosting methods return HOST_E_CLRNOTAVAILABLE.</span></span>|  
  
## <a name="remarks"></a><span data-ttu-id="6455d-122">Примечания</span><span class="sxs-lookup"><span data-stu-id="6455d-122">Remarks</span></span>  
 <span data-ttu-id="6455d-123">`RevertToSelf`вызывается для возврата исходный маркер потока после предыдущего вызова [ImpersonateLoggedOnUser](../../../../docs/framework/unmanaged-api/hosting/ihostsecuritymanager-impersonateloggedonuser-method.md) метод.</span><span class="sxs-lookup"><span data-stu-id="6455d-123">`RevertToSelf` is called to return to the original thread token, after an earlier call to the [ImpersonateLoggedOnUser](../../../../docs/framework/unmanaged-api/hosting/ihostsecuritymanager-impersonateloggedonuser-method.md) method.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="6455d-124">Требования</span><span class="sxs-lookup"><span data-stu-id="6455d-124">Requirements</span></span>  
 <span data-ttu-id="6455d-125">**Платформы:** разделе [требования к системе для](../../../../docs/framework/get-started/system-requirements.md).</span><span class="sxs-lookup"><span data-stu-id="6455d-125">**Platforms:** See [System Requirements](../../../../docs/framework/get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="6455d-126">**Заголовок:** MSCorEE.h</span><span class="sxs-lookup"><span data-stu-id="6455d-126">**Header:** MSCorEE.h</span></span>  
  
 <span data-ttu-id="6455d-127">**Библиотека:** включена как ресурс в MSCorEE.dll</span><span class="sxs-lookup"><span data-stu-id="6455d-127">**Library:** Included as a resource in MSCorEE.dll</span></span>  
  
 <span data-ttu-id="6455d-128">**Версии платформы .NET framework:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="6455d-128">**.NET Framework Versions:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="6455d-129">См. также</span><span class="sxs-lookup"><span data-stu-id="6455d-129">See Also</span></span>  
 [<span data-ttu-id="6455d-130">IHostSecurityContext-интерфейс</span><span class="sxs-lookup"><span data-stu-id="6455d-130">IHostSecurityContext Interface</span></span>](../../../../docs/framework/unmanaged-api/hosting/ihostsecuritycontext-interface.md)  
 [<span data-ttu-id="6455d-131">IHostSecurityManager-интерфейс</span><span class="sxs-lookup"><span data-stu-id="6455d-131">IHostSecurityManager Interface</span></span>](../../../../docs/framework/unmanaged-api/hosting/ihostsecuritymanager-interface.md)  
 [<span data-ttu-id="6455d-132">Impersonateloggedonuser-метод</span><span class="sxs-lookup"><span data-stu-id="6455d-132">ImpersonateLoggedOnUser Method</span></span>](../../../../docs/framework/unmanaged-api/hosting/ihostsecuritymanager-impersonateloggedonuser-method.md)