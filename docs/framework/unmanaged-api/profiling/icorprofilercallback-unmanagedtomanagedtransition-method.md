---
title: ICorProfilerCallback::UnmanagedToManagedTransition Yöntemi
ms.date: 03/30/2017
api_name:
- ICorProfilerCallback.UnmanagedToManagedTransition
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerCallback::UnmanagedToManagedTransition
helpviewer_keywords:
- ICorProfilerCallback::UnmanagedToManagedTransition method [.NET Framework profiling]
- UnmanagedToManagedTransition method [.NET Framework profiling]
ms.assetid: ade2cc01-9b81-4e09-a5f9-b3b9dda27e96
topic_type:
- apiref
ms.openlocfilehash: c381d4a85a1e836f1972060c8182dd698bb27550
ms.sourcegitcommit: b11efd71c3d5ce3d9449c8d4345481b9f21392c6
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/29/2020
ms.locfileid: "76870558"
---
# <a name="icorprofilercallbackunmanagedtomanagedtransition-method"></a>ICorProfilerCallback::UnmanagedToManagedTransition Yöntemi
Profil oluşturucuyu yönetilmeyen koddan yönetilen koda geçiş olduğunu bildirir.  
  
## <a name="syntax"></a>Sözdizimi  
  
```cpp  
HRESULT UnmanagedToManagedTransition(  
    [in] FunctionID functionId,  
    [in] COR_PRF_TRANSITION_REASON reason);  
```  
  
## <a name="parameters"></a>Parametreler  
 `functionId`  
 'ndaki Çağrılmakta olan işlevin KIMLIĞI.  
  
 `reason`  
 'ndaki Yönetilmeyen koddan yönetilen koda yapılan bir çağrı nedeniyle veya yönetilen bir işlev tarafından çağrılan yönetilmeyen bir işlevden dönüş nedeniyle geçişin yapılıp yapılmayacağını belirten [COR_PRF_TRANSITION_REASON](cor-prf-transition-reason-enumeration.md) numaralandırması değeri.  
  
## <a name="remarks"></a>Açıklamalar  
 `reason` değeri COR_PRF_TRANSITION_RETURN ve `functionId` null değilse, işlev KIMLIĞI yönetilmeyen işlevin olur ve tam zamanında (JıT) derleyici kullanılarak derlenmez. Yönetilmeyen işlevlerde, bunlarla ilişkili bazı temel bilgiler (örneğin, bir ad ve bazı meta veriler) vardır.  
  
 `reason` değeri COR_PRF_TRANSITION_CALL ise, çağrılan işlevin (yani, yönetilen işlev) henüz JıT derlenmemiş olabilir.  
  
## <a name="requirements"></a>Gereksinimler  
 **Platformlar:** Bkz. [sistem gereksinimleri](../../../../docs/framework/get-started/system-requirements.md).  
  
 **Üst bilgi:** CorProf. IDL, CorProf. h  
  
 **Kitaplık:** Corguid. lib  
  
 **.NET Framework sürümleri:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>Ayrıca bkz.

- [ICorProfilerCallback Arabirimi](icorprofilercallback-interface.md)
- [ManagedToUnmanagedTransition Yöntemi](icorprofilercallback-managedtounmanagedtransition-method.md)
- [C++'ta Açık PInvoke Kullanma (DllImport Özniteliği)](/cpp/dotnet/using-explicit-pinvoke-in-cpp-dllimport-attribute)
- [C++ Birlikte Çalışabilirliği Kullanma (Örtük PInvoke)](/cpp/dotnet/using-cpp-interop-implicit-pinvoke)
