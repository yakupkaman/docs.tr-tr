---
title: ICorProfilerCallback8::DynamicMethodJITCompilationBitmiş Yöntem
ms.date: 04/10/2018
api_name:
- ICorProfilerCallback8.DynamicMethodJITCompilationFinished
api_location:
- mscorwks.dll
- corprof.idl
api_type:
- COM
ms.openlocfilehash: c2e9489654a0fe5fa65ec638ed0f991a6c01415a
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/12/2020
ms.locfileid: "79175115"
---
# <a name="icorprofilercallback8dynamicmethodjitcompilationfinished-method"></a>ICorProfilerCallback8::DynamicMethodJITCompilationBitmiş Yöntem
[.NET Framework 4.7 ve sonraki sürümlerde desteklendi]  
  
Dinamik bir yöntemin JIT derlemesi tamamlandığında profiloluşturucuyu not edin.  
  
## <a name="syntax"></a>Sözdizimi  
  
```cpp  
HRESULT DynamicMethodJITCompilationFinished(  
     [in]  FunctionID  functionId,
     [in]  BOOL        hrStatus,
     [in]  BOOL        fIsSafeToBlock
);  
```  
  
## <a name="parameters"></a>Parametreler  
[içinde]`functionId`  
JIT derlemesinin başlatıldıği bellek içi işlevin tanımlayıcısı.

[içinde] `hrStatus` JIT derlemesinin başarılı olup olmadığını gösteren bir değer.

[içinde] `fIsSafeToBlock` engellemenin çalışma zamanının arama iş parçacığının bu geri aramadan dönmesini beklemesine neden olabileceğini belirtmek 
 `true` için; `false` engellemenin çalışma zamanının çalışmasını etkilemeyeceğini belirtmek için.  

## <a name="remarks"></a>Açıklamalar  

Dinamik bir yöntemin JIT derlemesi tamamlandığında bu geri arama tetiklenir. Bu çeşitli IL saplamaları ve LCG yöntemleri içerir. Amacı, profil oluşturucu yazarlara derlenen yöntemi kullanıcılara tanımlamak için yeterli bilgi sağlamaktır.

> [!NOTE]
> `functionId`dinamik yöntemlerin meta verisi olmadığından, değerler meta veri belirteçlerini gidermek için kullanılamaz.

## <a name="requirements"></a>Gereksinimler  
 **Platformlar:** [Bkz. Sistem Gereksinimleri](../../../../docs/framework/get-started/system-requirements.md).  
  
 **Üstbilgi:** CorProf.idl, CorProf.h  
  
 **Kütüphane:** CorGuids.lib  
  
 **.NET Çerçeve Sürümleri:**[!INCLUDE[net_current_v47plus](../../../../includes/net-current-v47plus.md)]  
  
## <a name="see-also"></a>Ayrıca bkz.

- [DynamicMethodJITCompilationStarted Yöntemi](icorprofilercallback8-dynamicmethodjitcompilationstarted-method.md)
- [ICorProfilerCallback8 Arabirimi](icorprofilercallback8-interface.md)
