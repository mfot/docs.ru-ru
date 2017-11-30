---
title: "Интерфейс ISymUnmanagedSourceServerModule"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-clr
ms.tgt_pltfrm: 
ms.topic: reference
api_name: ISymUnmanagedSourceServerModule
api_location: diasymreader.dll
api_type: COM
f1_keywords: ISymUnmanagedSourceServerModule
helpviewer_keywords: ISymUnmanagedSourceServerModule interface [.NET Framework debugging]
ms.assetid: a19b23bd-2061-476e-b67d-252f57404f8b
topic_type: apiref
caps.latest.revision: "6"
author: mairaw
ms.author: mairaw
manager: wpickett
ms.openlocfilehash: 3110be6a42ce68a6a8b3571206244a7fd1d38b8a
ms.sourcegitcommit: bd1ef61f4bb794b25383d3d72e71041a5ced172e
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/18/2017
---
# <a name="isymunmanagedsourceservermodule-interface"></a><span data-ttu-id="679ac-102">Интерфейс ISymUnmanagedSourceServerModule</span><span class="sxs-lookup"><span data-stu-id="679ac-102">ISymUnmanagedSourceServerModule Interface</span></span>
<span data-ttu-id="679ac-103">Предоставляет данные сервера источника для модуля.</span><span class="sxs-lookup"><span data-stu-id="679ac-103">Provides source server data for a module.</span></span> <span data-ttu-id="679ac-104">Получить этот интерфейс, вызвав `QueryInterface` на объект, реализующий интерфейс [ISymUnmanagedReader](../../../../docs/framework/unmanaged-api/diagnostics/isymunmanagedreader-interface.md) интерфейса.</span><span class="sxs-lookup"><span data-stu-id="679ac-104">Obtain this interface by calling `QueryInterface` on an object that implements the [ISymUnmanagedReader](../../../../docs/framework/unmanaged-api/diagnostics/isymunmanagedreader-interface.md) interface.</span></span>  
  
## <a name="methods"></a><span data-ttu-id="679ac-105">Методы</span><span class="sxs-lookup"><span data-stu-id="679ac-105">Methods</span></span>  
  
|<span data-ttu-id="679ac-106">Метод</span><span class="sxs-lookup"><span data-stu-id="679ac-106">Method</span></span>|<span data-ttu-id="679ac-107">Описание</span><span class="sxs-lookup"><span data-stu-id="679ac-107">Description</span></span>|  
|------------|-----------------|  
|[<span data-ttu-id="679ac-108">Метод GetSourceServerData</span><span class="sxs-lookup"><span data-stu-id="679ac-108">GetSourceServerData Method</span></span>](../../../../docs/framework/unmanaged-api/diagnostics/isymunmanagedsourceservermodule-getsourceserverdata-method.md)|<span data-ttu-id="679ac-109">Возвращает данные исходного сервера для модуля.</span><span class="sxs-lookup"><span data-stu-id="679ac-109">Returns the source server data for the module.</span></span>|  
  
## <a name="requirements"></a><span data-ttu-id="679ac-110">Требования</span><span class="sxs-lookup"><span data-stu-id="679ac-110">Requirements</span></span>  
 <span data-ttu-id="679ac-111">**Заголовок:** CorSym.idl, CorSym.h</span><span class="sxs-lookup"><span data-stu-id="679ac-111">**Header:** CorSym.idl, CorSym.h</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="679ac-112">См. также</span><span class="sxs-lookup"><span data-stu-id="679ac-112">See Also</span></span>  
 [<span data-ttu-id="679ac-113">Интерфейсы хранилища символов диагностики</span><span class="sxs-lookup"><span data-stu-id="679ac-113">Diagnostics Symbol Store Interfaces</span></span>](../../../../docs/framework/unmanaged-api/diagnostics/diagnostics-symbol-store-interfaces.md)