---
title: COR_PRF_TRANSITION_REASON Numaralandırması
ms.date: 03/30/2017
api_name:
- COR_PRF_TRANSITION_REASON
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- COR_PRF_TRANSITION_REASON
helpviewer_keywords:
- COR_PRF_TRANSITION_REASON enumeration [.NET Framework profiling]
ms.assetid: da941118-01b7-4197-ae5b-9f2f8adcd623
topic_type:
- apiref
ms.openlocfilehash: 1c3c311fd431b6c0b18af3d6516973b2471cfabd
ms.sourcegitcommit: b11efd71c3d5ce3d9449c8d4345481b9f21392c6
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/29/2020
ms.locfileid: "76867069"
---
# <a name="cor_prf_transition_reason-enumeration"></a>COR_PRF_TRANSITION_REASON Numaralandırması
Yönetilmesinin yönetilmeyen koda veya tam tersi bir geçişin sebebini gösterir.  
  
## <a name="syntax"></a>Sözdizimi  
  
```cpp  
typedef enum {  
    COR_PRF_TRANSITION_CALL,  
    COR_PRF_TRANSITION_RETURN  
} COR_PRF_TRANSITION_REASON;  
```  
  
## <a name="members"></a>Üyeler  
  
|Üye|Açıklama|  
|------------|-----------------|  
|`COR_PRF_TRANSITION_CALL`|Geçiş bir işleve yapılan çağrıdır.|  
|`COR_PRF_TRANSITION_RETURN`|Geçiş, bir işlevden geri dönüş nedeniyle yapılır.|  
  
## <a name="remarks"></a>Açıklamalar  
 Bir geçiş gerçekleştiğinde, profil oluşturucu bir [ICorProfilerCallback:: ManagedToUnmanagedTransition](icorprofilercallback-managedtounmanagedtransition-method.md) veya [ICorProfilerCallback:: UnmanagedToManagedTransition](icorprofilercallback-unmanagedtomanagedtransition-method.md) geri çağırması alır, bunlardan biri, geçişin nedenini göstermek için `COR_PRF_TRANSITION_REASON` numaralandırması değeri sağlar.  
  
## <a name="requirements"></a>Gereksinimler  
 **Platformlar:** Bkz. [sistem gereksinimleri](../../../../docs/framework/get-started/system-requirements.md).  
  
 **Üst bilgi:** CorProf. IDL, CorProf. h  
  
 **Kitaplık:** Corguid. lib  
  
 **.NET Framework sürümleri:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]
