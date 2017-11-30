---
title: "Метод IMetaDataImport::EnumModuleRefs"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-clr
ms.tgt_pltfrm: 
ms.topic: reference
api_name: IMetaDataImport.EnumModuleRefs
api_location: mscoree.dll
api_type: COM
f1_keywords: IMetaDataImport::EnumModuleRefs
helpviewer_keywords:
- EnumModuleRefs method [.NET Framework metadata]
- IMetaDataImport::EnumModuleRefs method [.NET Framework metadata]
ms.assetid: 53441f3a-68d2-477c-906e-37c55dfcfb4d
topic_type: apiref
caps.latest.revision: "11"
author: mairaw
ms.author: mairaw
manager: wpickett
ms.openlocfilehash: ebba448881b934220f0eb46c392ab0909ae37f68
ms.sourcegitcommit: 4f3fef493080a43e70e951223894768d36ce430a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/21/2017
---
# <a name="imetadataimportenummodulerefs-method"></a><span data-ttu-id="7d4c3-102">Метод IMetaDataImport::EnumModuleRefs</span><span class="sxs-lookup"><span data-stu-id="7d4c3-102">IMetaDataImport::EnumModuleRefs Method</span></span>
<span data-ttu-id="7d4c3-103">Перечисляет токены ModuleRef, представляющие импортируемые модули.</span><span class="sxs-lookup"><span data-stu-id="7d4c3-103">Enumerates ModuleRef tokens that represent imported modules.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="7d4c3-104">Синтаксис</span><span class="sxs-lookup"><span data-stu-id="7d4c3-104">Syntax</span></span>  
  
```  
HRESULT EnumModuleRefs (  
   [in, out] HCORENUM     *phEnum,  
   [out]     mdModuleRef  rModuleRefs[],  
   [in]      ULONG        cMax,  
   [out]     ULONG        *pcModuleRefs  
);  
```  
  
#### <a name="parameters"></a><span data-ttu-id="7d4c3-105">Параметры</span><span class="sxs-lookup"><span data-stu-id="7d4c3-105">Parameters</span></span>  
 `phEnum`  
 <span data-ttu-id="7d4c3-106">[in, out] Указатель на перечислитель.</span><span class="sxs-lookup"><span data-stu-id="7d4c3-106">[in, out] A pointer to the enumerator.</span></span> <span data-ttu-id="7d4c3-107">Это должно быть NULL при первом вызове этого метода.</span><span class="sxs-lookup"><span data-stu-id="7d4c3-107">This must be NULL for the first call of this method.</span></span>  
  
 `rModuleRefs`  
 <span data-ttu-id="7d4c3-108">[out] Массив, используемый для хранения токены ModuleRef.</span><span class="sxs-lookup"><span data-stu-id="7d4c3-108">[out] The array used to store the ModuleRef tokens.</span></span>  
  
 `cMax`  
 <span data-ttu-id="7d4c3-109">[in] Максимальный размер массива `rModuleRefs`.</span><span class="sxs-lookup"><span data-stu-id="7d4c3-109">[in] The maximum size of the `rModuleRefs` array.</span></span>  
  
 `pcModuleRefs`  
 <span data-ttu-id="7d4c3-110">[out] Число токены ModuleRef, возвращаемых в `rModuleRefs`.</span><span class="sxs-lookup"><span data-stu-id="7d4c3-110">[out] The number of ModuleRef tokens returned in `rModuleRefs`.</span></span>  
  
## <a name="return-value"></a><span data-ttu-id="7d4c3-111">Возвращаемое значение</span><span class="sxs-lookup"><span data-stu-id="7d4c3-111">Return Value</span></span>  
  
|<span data-ttu-id="7d4c3-112">HRESULT</span><span class="sxs-lookup"><span data-stu-id="7d4c3-112">HRESULT</span></span>|<span data-ttu-id="7d4c3-113">Описание</span><span class="sxs-lookup"><span data-stu-id="7d4c3-113">Description</span></span>|  
|-------------|-----------------|  
|`S_OK`|<span data-ttu-id="7d4c3-114">`EnumModuleRefs`успешно возвращен.</span><span class="sxs-lookup"><span data-stu-id="7d4c3-114">`EnumModuleRefs` returned successfully.</span></span>|  
|`S_FALSE`|<span data-ttu-id="7d4c3-115">Существуют маркеры для перечисления отсутствуют.</span><span class="sxs-lookup"><span data-stu-id="7d4c3-115">There are no tokens to enumerate.</span></span> <span data-ttu-id="7d4c3-116">В этом случае `pcModuleRefs` равно нулю.</span><span class="sxs-lookup"><span data-stu-id="7d4c3-116">In that case, `pcModuleRefs` is zero.</span></span>|  
  
## <a name="requirements"></a><span data-ttu-id="7d4c3-117">Требования</span><span class="sxs-lookup"><span data-stu-id="7d4c3-117">Requirements</span></span>  
 <span data-ttu-id="7d4c3-118">**Платформы:** разделе [требования к системе для](../../../../docs/framework/get-started/system-requirements.md).</span><span class="sxs-lookup"><span data-stu-id="7d4c3-118">**Platforms:** See [System Requirements](../../../../docs/framework/get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="7d4c3-119">**Заголовок:** Cor.h</span><span class="sxs-lookup"><span data-stu-id="7d4c3-119">**Header:** Cor.h</span></span>  
  
 <span data-ttu-id="7d4c3-120">**Библиотека:** включена как ресурс в MsCorEE.dll</span><span class="sxs-lookup"><span data-stu-id="7d4c3-120">**Library:** Included as a resource in MsCorEE.dll</span></span>  
  
 <span data-ttu-id="7d4c3-121">**Версии платформы .NET framework:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="7d4c3-121">**.NET Framework Versions:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="7d4c3-122">См. также</span><span class="sxs-lookup"><span data-stu-id="7d4c3-122">See Also</span></span>  
 [<span data-ttu-id="7d4c3-123">IMetaDataImport-интерфейс</span><span class="sxs-lookup"><span data-stu-id="7d4c3-123">IMetaDataImport Interface</span></span>](../../../../docs/framework/unmanaged-api/metadata/imetadataimport-interface.md)  
 [<span data-ttu-id="7d4c3-124">IMetaDataImport2-интерфейс</span><span class="sxs-lookup"><span data-stu-id="7d4c3-124">IMetaDataImport2 Interface</span></span>](../../../../docs/framework/unmanaged-api/metadata/imetadataimport2-interface.md)