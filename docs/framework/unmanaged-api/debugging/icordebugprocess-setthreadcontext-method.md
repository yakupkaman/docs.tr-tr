---
title: ICorDebugProcess::SetThreadContext Yöntemi
ms.date: 03/30/2017
api_name:
- ICorDebugProcess.SetThreadContext
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugProcess::SetThreadContext
helpviewer_keywords:
- ICorDebugProcess::SetThreadContext method [.NET Framework debugging]
- SetThreadContext method, ICorDebugProcess interface [.NET Framework debugging]
ms.assetid: a7b50175-2bf1-40be-8f65-64aec7aa1247
topic_type:
- apiref
ms.openlocfilehash: 66d544bbc0511ea76565376c8f10294f1758026b
ms.sourcegitcommit: 13e79efdbd589cad6b1de634f5d6b1262b12ab01
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/28/2020
ms.locfileid: "76792567"
---
# <a name="icordebugprocesssetthreadcontext-method"></a>ICorDebugProcess::SetThreadContext Yöntemi
Bu işlemdeki verilen iş parçacığının bağlamını ayarlar.  
  
## <a name="syntax"></a>Sözdizimi  
  
```cpp  
HRESULT SetThreadContext(  
    [in] DWORD threadID,  
    [in] ULONG32 contextSize,  
    [in, length_is(contextSize), size_is(contextSize)]  
    BYTE context[]);  
```  
  
## <a name="parameters"></a>Parametreler  
 `threadID`  
 'ndaki Bağlamını ayarlanacak iş parçacığının KIMLIĞI.  
  
 `contextSize`  
 'ndaki `context` dizisinin boyutu.  
  
 `context`  
 'ndaki İş parçacığının bağlamını tanımlayan bir bayt dizisi.  
  
 Bağlam, iş parçacığının yürütüldüğü işlemcinin mimarisini belirtir.  
  
## <a name="remarks"></a>Açıklamalar  
 İş parçacığı gerçekten, bağlamı geçici olarak değiştirilen bir "ele geçirilmiş" durumda olabileceğinden, hata ayıklayıcı Win32 `SetThreadContext` işlevi yerine bu yöntemi çağırmalıdır. Bu yöntem, yalnızca bir iş parçacığı yerel kodda olduğunda kullanılmalıdır. Yönetilen koddaki iş parçacıkları için [ICorDebugRegisterSet](icordebugregisterset-interface.md) kullanın. Bant dışı (OOB) hata ayıklama olayı sırasında bir iş parçacığının bağlamını hiçbir şekilde değiştirmeniz gerekmez.  
  
 Geçirilen veriler, geçerli platform için bir bağlam yapısı olmalıdır.  
  
 Yanlış kullanılırsa, bu yöntem çalışma zamanını bozabilir.  
  
## <a name="requirements"></a>Gereksinimler  
 **Platformlar:** Bkz. [sistem gereksinimleri](../../../../docs/framework/get-started/system-requirements.md).  
  
 **Üst bilgi:** CorDebug. IDL, CorDebug. h  
  
 **Kitaplık:** Corguid. lib  
  
 **.NET Framework sürümleri:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]
