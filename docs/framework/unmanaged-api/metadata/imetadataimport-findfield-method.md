---
title: "Метод IMetaDataImport::FindField"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-clr
ms.tgt_pltfrm: 
ms.topic: reference
api_name: IMetaDataImport.FindField
api_location: mscoree.dll
api_type: COM
f1_keywords: IMetaDataImport::FindField
helpviewer_keywords:
- IMetaDataImport::FindField method [.NET Framework metadata]
- FindField method [.NET Framework metadata]
ms.assetid: 38cd4e16-fbb2-471c-aa73-ac51a1931ad2
topic_type: apiref
caps.latest.revision: "12"
author: mairaw
ms.author: mairaw
manager: wpickett
ms.openlocfilehash: 2178f8738ca510fb2163c1043dd94ebcb7043904
ms.sourcegitcommit: 4f3fef493080a43e70e951223894768d36ce430a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/21/2017
---
# <a name="imetadataimportfindfield-method"></a><span data-ttu-id="4e31f-102">Метод IMetaDataImport::FindField</span><span class="sxs-lookup"><span data-stu-id="4e31f-102">IMetaDataImport::FindField Method</span></span>
<span data-ttu-id="4e31f-103">Возвращает указатель на FieldDef токен для поля, которое заключено в указанном <xref:System.Type> и имеет имя и метаданные указанной подписи.</span><span class="sxs-lookup"><span data-stu-id="4e31f-103">Gets a pointer to the FieldDef token for the field that is enclosed by the specified <xref:System.Type> and that has the specified name and metadata signature.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="4e31f-104">Синтаксис</span><span class="sxs-lookup"><span data-stu-id="4e31f-104">Syntax</span></span>  
  
```  
HRESULT FindField (  
   [in]  mdTypeDef         td,  
   [in]  LPCWSTR           szName,  
   [in]  PCCOR_SIGNATURE   pvSigBlob,  
   [in]  ULONG             cbSigBlob,  
   [out] mdFieldDef        *pmb  
);  
```  
  
#### <a name="parameters"></a><span data-ttu-id="4e31f-105">Параметры</span><span class="sxs-lookup"><span data-stu-id="4e31f-105">Parameters</span></span>  
 `td`  
 <span data-ttu-id="4e31f-106">[in] Токен TypeDef для класса или интерфейса, содержащего поля для поиска.</span><span class="sxs-lookup"><span data-stu-id="4e31f-106">[in] The TypeDef token for the class or interface that encloses the field to search for.</span></span> <span data-ttu-id="4e31f-107">Если это значение равно `mdTokenNil`, поиск выполняется в глобальной переменной.</span><span class="sxs-lookup"><span data-stu-id="4e31f-107">If this value is `mdTokenNil`, the lookup is done for a global variable.</span></span>  
  
 `szName`  
 <span data-ttu-id="4e31f-108">[in] Имя поля для поиска.</span><span class="sxs-lookup"><span data-stu-id="4e31f-108">[in] The name of the field to search for.</span></span>  
  
 `pvSigBlob`  
 <span data-ttu-id="4e31f-109">[in] Указатель на двоичную подпись метаданных поля.</span><span class="sxs-lookup"><span data-stu-id="4e31f-109">[in] A pointer to the binary metadata signature of the field.</span></span>  
  
 `cbSigBlob`  
 <span data-ttu-id="4e31f-110">[in] Размер в байтах `pvSigBlob`.</span><span class="sxs-lookup"><span data-stu-id="4e31f-110">[in] The size in bytes of `pvSigBlob`.</span></span>  
  
 `pmb`  
 <span data-ttu-id="4e31f-111">[out] Указатель на токен FieldDef сопоставления.</span><span class="sxs-lookup"><span data-stu-id="4e31f-111">[out] A pointer to the matching FieldDef token.</span></span>  
  
## <a name="remarks"></a><span data-ttu-id="4e31f-112">Примечания</span><span class="sxs-lookup"><span data-stu-id="4e31f-112">Remarks</span></span>  
 <span data-ttu-id="4e31f-113">Укажите поля, используя его включающего класса или интерфейса (`td`), его имя (`szName`) и при необходимости его подпись (`pvSigBlob`).</span><span class="sxs-lookup"><span data-stu-id="4e31f-113">You specify the field using its enclosing class or interface (`td`), its name (`szName`), and optionally its signature (`pvSigBlob`).</span></span>  
  
 <span data-ttu-id="4e31f-114">Подпись, передаваемый `FindField` должны были созданы в текущей области, поскольку подписи привязаны к определенным областям.</span><span class="sxs-lookup"><span data-stu-id="4e31f-114">The signature passed to `FindField` must have been generated in the current scope, because signatures are bound to a particular scope.</span></span> <span data-ttu-id="4e31f-115">Подпись можно внедрить токен, который определяет включающего класса или типа значения.</span><span class="sxs-lookup"><span data-stu-id="4e31f-115">A signature can embed a token that identifies the enclosing class or value type.</span></span> <span data-ttu-id="4e31f-116">(Маркер — это индекс в локальной таблице TypeDef).</span><span class="sxs-lookup"><span data-stu-id="4e31f-116">(The token is an index into the local TypeDef table).</span></span> <span data-ttu-id="4e31f-117">Не удается построить во время выполнения вне контекста текущей области и использовать ее в качестве входных данных для `FindField`.</span><span class="sxs-lookup"><span data-stu-id="4e31f-117">You cannot build a run-time signature outside the context of the current scope and use that signature as input to `FindField`.</span></span>  
  
 <span data-ttu-id="4e31f-118">`FindField`находит только поля, которые были определены непосредственно в классе или интерфейсе; наследуемые поля не найден.</span><span class="sxs-lookup"><span data-stu-id="4e31f-118">`FindField` finds only fields that were defined directly in the class or interface; it does not find inherited fields.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="4e31f-119">Требования</span><span class="sxs-lookup"><span data-stu-id="4e31f-119">Requirements</span></span>  
 <span data-ttu-id="4e31f-120">**Платформы:** разделе [требования к системе для](../../../../docs/framework/get-started/system-requirements.md).</span><span class="sxs-lookup"><span data-stu-id="4e31f-120">**Platforms:** See [System Requirements](../../../../docs/framework/get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="4e31f-121">**Заголовок:** Cor.h</span><span class="sxs-lookup"><span data-stu-id="4e31f-121">**Header:** Cor.h</span></span>  
  
 <span data-ttu-id="4e31f-122">**Библиотека:** включена как ресурс в MsCorEE.dll</span><span class="sxs-lookup"><span data-stu-id="4e31f-122">**Library:** Included as a resource in MsCorEE.dll</span></span>  
  
 <span data-ttu-id="4e31f-123">**Версии платформы .NET framework:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="4e31f-123">**.NET Framework Versions:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="4e31f-124">См. также</span><span class="sxs-lookup"><span data-stu-id="4e31f-124">See Also</span></span>  
 [<span data-ttu-id="4e31f-125">IMetaDataImport-интерфейс</span><span class="sxs-lookup"><span data-stu-id="4e31f-125">IMetaDataImport Interface</span></span>](../../../../docs/framework/unmanaged-api/metadata/imetadataimport-interface.md)  
 [<span data-ttu-id="4e31f-126">IMetaDataImport2-интерфейс</span><span class="sxs-lookup"><span data-stu-id="4e31f-126">IMetaDataImport2 Interface</span></span>](../../../../docs/framework/unmanaged-api/metadata/imetadataimport2-interface.md)