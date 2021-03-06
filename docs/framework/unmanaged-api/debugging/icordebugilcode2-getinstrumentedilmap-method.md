---
title: ICorDebugILCode2::GetInstrumentedILMap Yöntemi
ms.date: 03/30/2017
dev_langs:
- cpp
api_name:
- ICorDebugILCode2.GetInstrumentedILMap
api_location:
- mscordbi.dll
api_type:
- COM
ms.assetid: 7a4e3085-8f95-40ef-a4be-7d6146f47ce2
topic_type:
- apiref
ms.openlocfilehash: 728a6c83dc321fa28dc4ff84c4e874d886524b36
ms.sourcegitcommit: 13e79efdbd589cad6b1de634f5d6b1262b12ab01
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/28/2020
ms.locfileid: "76788566"
---
# <a name="icordebugilcode2getinstrumentedilmap-method"></a>ICorDebugILCode2::GetInstrumentedILMap Yöntemi
[.NET Framework 4.5.2 ve sonraki sürümlerde desteklenir]  
  
 Bu örnek için profil oluşturucu tarafından işaretlenmiş ara dil (IL) uzaklıklarını orijinal Yöntem Il uzaklıklarından bir eşleme döndürür.  
  
## <a name="syntax"></a>Sözdizimi  
  
```cpp
HRESULT GetInstrumentedILMap(  
   [in] ULONG32 cMap,  
   [out] ULONG32 *pcMap,  
   [out, size_is(cMap), length_is(*pcMap)] COR_IL_MAP map[]  
);  
```  
  
## <a name="parameters"></a>Parametreler  
 cMap  
 'ndaki `map` dizisinin depolama kapasitesi. Daha fazla bilgi için Açıklamalar bölümüne bakın.  
  
 pcMap  
 dışı Harita dizisine yazılan COR_IL_MAP değerlerinin sayısı.  
  
 map  
 dışı Profil Oluşturucu tarafından izlenen Il 'den özgün yöntemin Il 'ye eşlemeler hakkında bilgi sağlayan COR_IL_MAP değerleri dizisi.  
  
## <a name="remarks"></a>Açıklamalar  
 Profil Oluşturucu [ICorProfilerInfo:: SetILInstrumentedCodeMap](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo-setilinstrumentedcodemap-method.md) metodunu çağırarak eşlemeyi ayarlarsa, hata ayıklayıcı eşlemeyi almak için bu yöntemi çağırabilir ve yığın izlemeleri ve değişken yaşam SÜRELERI için Il farklarını hesaplarken dahili eşlemeyi kullanır.  
  
 `cMap` 0 ise ve `pcMap`**null**değilse `pcMap` kullanılabilir COR_IL_MAP değer sayısına ayarlanır. Sıfır olmayan `cMap`, `map` dizisinin depolama kapasitesini temsil eder. Yöntemi döndürüldüğünde, `map` en fazla `cMap` öğesi içerir ve `pcMap` aslında `map` dizisine yazılmış COR_IL_MAP değerlerinin sayısına ayarlanır.  
  
 Il düzenlenmemişse veya eşleme bir profil oluşturucu tarafından sağlanmamışsa, bu yöntem `S_OK` döndürür ve `pcMap` 0 olarak ayarlar.  
  
## <a name="requirements"></a>Gereksinimler  
 **Platformlar:** Bkz. [sistem gereksinimleri](../../../../docs/framework/get-started/system-requirements.md).  
  
 **Üst bilgi:** CorDebug. IDL, CorDebug. h  
  
 **Kitaplık:** Corguid. lib  
  
 **.NET Framework sürümleri:** [!INCLUDE[net_current_v452plus](../../../../includes/net-current-v452plus-md.md)]  
  
## <a name="see-also"></a>Ayrıca bkz.

- [ICorProfilerInfo:: Setilınstrumentedcodemap](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo-setilinstrumentedcodemap-method.md)
- [ICorDebugILCode2 Arabirimi](icordebugilcode2-interface.md)
- [Hata Ayıklama Arabirimleri](debugging-interfaces.md)
