---
title: ICorDebugProcess5::EnumerateHeap Yöntemi
ms.date: 03/30/2017
api_name:
- ICorDebugProcess5.EnumerateHeap
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugProcess5::EnumerateHeap
helpviewer_keywords:
- EnumerateHeap method, ICorDebugProcess5 interface [.NET Framework debugging]
- ICorDebugProcess5::EnumerateHeap method [.NET Framework debugging]
ms.assetid: b0192104-6073-4089-a4df-dc29ee033074
topic_type:
- apiref
ms.openlocfilehash: 780f9eb0984e35c4487d770b5e7ff33917cf07ed
ms.sourcegitcommit: 13e79efdbd589cad6b1de634f5d6b1262b12ab01
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/28/2020
ms.locfileid: "76792410"
---
# <a name="icordebugprocess5enumerateheap-method"></a>ICorDebugProcess5::EnumerateHeap Yöntemi
Yönetilen yığındaki nesneler için bir Numaralandırıcı alır.  
  
## <a name="syntax"></a>Sözdizimi  
  
```cpp  
HRESULT EnumerateHeap(  
    [out] ICorDebugHeapEnum **ppObjects  
);  
```  
  
## <a name="parameters"></a>Parametreler  
 `ppObject`  
 dışı Yönetilen yığında bulunan nesneler için bir Numaralandırıcı olan [ICorDebugHeapEnum](icordebugheapenum-interface.md) arabirimi nesnesinin adresine yönelik bir işaretçi.  
  
## <a name="remarks"></a>Açıklamalar  
 `ICorDebugProcess5::EnumerateHeap` yöntemi çağrılmadan önce, [ICorDebugProcess5:: GetGCHeapInformation](icordebugprocess5-getgcheapinformation-method.md) metodunu çağırmanız ve döndürülen [COR_HEAPINFO](cor-heapinfo-structure.md) nesnesinin `areGCStructuresValid` alanının değerini inceleyerek geçerli durumunda çöp toplama yığınının numaralandırılanmış olduğundan emin olmanız gerekir. Ayrıca, `ICorDebugProcess5::EnumerateHeap`, yönetilen yığın için bellekten önce, işlemin kullanım ömrü içinde çok erken bir şekilde iliştiriyorsa `E_FAIL` döndürür.  
  
 [ICorDebugHeapEnum](icordebugheapenum-interface.md) arabirimi nesnesi, [cor_heapobject](cor-heapobject-structure.md) nesneleri Listeletmanızı sağlayan ıcordebugger genum arabiriminden türetilmiş standart bir Numaralandırıcı. Bu yöntem, [ICorDebugHeapEnum](icordebugheapenum-interface.md) toplama nesnesini tüm nesneler hakkında bilgi sağlayan [cor_heapobject](cor-heapobject-structure.md) örneklerle doldurur. Koleksiyon, herhangi bir nesne tarafından kök olmayan ancak henüz atık toplayıcı tarafından toplanmamış nesneler hakkında bilgi sağlayan [cor_heapobject](cor-heapobject-structure.md) örnekleri de içerebilir.  
  
## <a name="requirements"></a>Gereksinimler  
 **Platformlar:** Bkz. [sistem gereksinimleri](../../../../docs/framework/get-started/system-requirements.md).  
  
 **Üst bilgi:** CorDebug. IDL, CorDebug. h  
  
 **Kitaplık:** Corguid. lib  
  
 **.NET Framework sürümleri:** [!INCLUDE[net_current_v45plus](../../../../includes/net-current-v45plus-md.md)]  
  
## <a name="see-also"></a>Ayrıca bkz.

- [ICorDebugProcess5 Arabirimi](icordebugprocess5-interface.md)
- [Hata Ayıklama Arabirimleri](debugging-interfaces.md)
