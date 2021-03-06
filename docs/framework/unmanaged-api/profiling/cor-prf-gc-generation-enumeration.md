---
title: COR_PRF_GC_GENERATION Numaralandırması
ms.date: 03/30/2017
api_name:
- COR_PRF_GC_GENERATION
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- COR_PRF_GC_GENERATION
helpviewer_keywords:
- COR_GC_GENERATION_FLAGS enumeration [.NET Framework profiling]
ms.assetid: d6ece160-26ad-4d39-abd7-05acd6f78c48
topic_type:
- apiref
ms.openlocfilehash: 4eff8472e353c4e5fd2505b281cc9efc89f013fc
ms.sourcegitcommit: b11efd71c3d5ce3d9449c8d4345481b9f21392c6
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/29/2020
ms.locfileid: "76867223"
---
# <a name="cor_prf_gc_generation-enumeration"></a>COR_PRF_GC_GENERATION Numaralandırması
Çöp toplama oluşturmayı tanımlar.  
  
## <a name="syntax"></a>Sözdizimi  
  
```cpp  
typedef enum {  
    COR_PRF_GC_GEN_0 = 0,  
    COR_PRF_GC_GEN_1 = 1,  
    COR_PRF_GC_GEN_2 = 2,  
    COR_PRF_GC_LARGE_OBJECT_HEAP = 3  
} COR_PRF_GC_GENERATION;  
```  
  
## <a name="members"></a>Üyeler  
  
|Üye|Açıklama|  
|------------|-----------------|  
|`COR_PRF_GC_GEN_0`|Nesne, oluşturma 0 olarak depolanır.|  
|`COR_PRF_GC_GEN_1`|Nesnesi 1. nesil olarak depolanır.|  
|`COR_PRF_GC_GEN_2`|Nesne 2. nesil olarak depolanır.|  
|`COR_PRF_GC_LARGE_OBJECT_HEAP`|Nesne büyük nesne yığınında depolanır.|  
  
## <a name="remarks"></a>Açıklamalar  
 Çöp toplayıcı, nesneleri yaşa göre nesslerde ayırarak bellek yönetimi performansını geliştirir. Çöp toplayıcı Şu anda üç nesil, numaralandırılmış 0, 1 ve 2 ' yi ve büyük nesneler için kullanılan özel bir yığın kesimini kullanmaktadır. Boyutu belirli bir değerden daha büyük olan nesneler büyük nesne yığınında depolanır. Ayrılan diğer nesneler 0 oluşturmaya ait. Atık toplama sonrasında var olan tüm nesneler 1. kuşak ' e yükseltilir. Çöp toplama işleminden sonra var olan nesneler 2. kuşak ' e taşınır.  
  
 Nesin kullanımı, çöp toplayıcının herhangi bir anda yalnızca ayrılmış nesnelerin bir alt kümesiyle çalışması gerektiği anlamına gelir.  
  
 `COR_PRF_GC_GENERATION` numaralandırması [COR_PRF_GC_GENERATION_RANGE](cor-prf-gc-generation-range-structure.md) yapısı tarafından kullanılır.  
  
## <a name="requirements"></a>Gereksinimler  
 **Platformlar:** Bkz. [sistem gereksinimleri](../../../../docs/framework/get-started/system-requirements.md).  
  
 **Üst bilgi:** CorProf. IDL, CorProf. h  
  
 **Kitaplık:** Corguid. lib  
  
 **.NET Framework sürümleri:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>Ayrıca bkz.

- [Profil Oluşturma Sabit Listeleri](profiling-enumerations.md)
