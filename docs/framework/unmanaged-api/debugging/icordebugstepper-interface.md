---
title: ICorDebugStepper Arabirimi
ms.date: 03/30/2017
api_name:
- ICorDebugStepper
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugStepper
helpviewer_keywords:
- ICorDebugStepper interface [.NET Framework debugging]
ms.assetid: ed8364eb-f01b-46f6-b5e3-5dda9cae2dfe
topic_type:
- apiref
ms.openlocfilehash: e9bb69567a247472af42efb08b609d3474c87ed2
ms.sourcegitcommit: 13e79efdbd589cad6b1de634f5d6b1262b12ab01
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/28/2020
ms.locfileid: "76791785"
---
# <a name="icordebugstepper-interface"></a>ICorDebugStepper Arabirimi
Bir hata ayıklayıcının gerçekleştirdiği kod yürütmedeki bir adımı temsil eder, bir komutun çıkarılması ve tamamlanması arasında bir tanımlayıcı görevi görür ve bir adımı iptal etmek için bir yol sağlar.  
  
## <a name="methods"></a>Yöntemler  
  
|Yöntem|Açıklama|  
|------------|-----------------|  
|[Deactivate Yöntemi](icordebugstepper-deactivate-method.md)|Bu `ICorDebugStepper`, aldığı son adım komutunu iptal etmesine neden olur.|  
|[IsActive Yöntemi](icordebugstepper-isactive-method.md)|Bu `ICorDebugStepper` Şu anda bir adım yürütüp yürütümeyeceğini belirten bir değer alır.|  
|[SetInterceptMask Yöntemi](icordebugstepper-setinterceptmask-method.md)|İçine eklenen kod türlerini belirten bir Cordebugkesmenoktası değeri ayarlar.|  
|[SetRangeIL Yöntemi](icordebugstepper-setrangeil-method.md)|[ICorDebugStepper:: StepRange](icordebugstepper-steprange-method.md) öğesine yapılan çağrıların, yerel koda göreli bağımsız değişken değerlerini veya bir şekilde ele alınan metodun Microsoft ara DILI (MSIL) kodunu geçirip geçirmediğini belirten bir değer ayarlar.|  
|[SetUnmappedStopMask Yöntemi](icordebugstepper-setunmappedstopmask-method.md)|Yürütmenin durdurulacağı eşlenmemiş kodun türünü belirten bir CorDebugUnmappedStop değeri ayarlar.|  
|[Step Yöntemi](icordebugstepper-step-method.md)|Bu `ICorDebugStepper`, kendisini kapsayan iş parçacığı aracılığıyla tek adımlı ve isteğe bağlı olarak, iş parçacığı içinde çağrılan işlevler aracılığıyla tek adımla devam etmek için sağlar.|  
|[StepOut Yöntemi](icordebugstepper-stepout-method.md)|Bu `ICorDebugStepper`, kendisini kapsayan iş parçacığı aracılığıyla tek adımlı ve geçerli çerçeve çağıran çerçeveye denetim döndürdüğünde tamamlanmasına neden olur.|  
|[StepRange Yöntemi](icordebugstepper-steprange-method.md)|Bu `ICorDebugStepper`, kendisini kapsayan iş parçacığı aracılığıyla tek adımlı ve belirtilen aralıkların en son ötesinde koda ulaştığında geri dönüşmesine neden olur.|  
  
## <a name="remarks"></a>Açıklamalar  
 `ICorDebugStepper` arabirimi aşağıdaki amaçlara hizmet eder:  
  
- Verilen bir step komutu ve bu komutun tamamlanması arasında bir tanımlayıcı görevi görür.  
  
- Gerçekleştirilebilecek tüm adımlamayı kapsüllemek için merkezi bir arabirim sağlar.  
  
- Bir atlama işlemini erken iptal etmek için bir yol sağlar.  
  
 İş parçacığı başına birden fazla Stepper olabilir. Örneğin, bir işlev üzerinde atlama sırasında bir kesme noktası isabet edebilir ve Kullanıcı bu işlevin içinde yeni bir Adımlama işlemi başlatmak isteyebilir. Bu durumun nasıl işleneceğini belirleme, hata ayıklayıcıya yöneliktir. Hata ayıklayıcı orijinal atlama işlemini iptal etmek veya iki işlemi iç içe aktarmak isteyebilir. `ICorDebugStepper` arabirimi her iki seçeneği de destekler.  
  
 Ortak dil çalışma zamanı (CLR), çapraz iş parçacıklı, sıralanmış bir çağrı yapıyorsa, iş parçacıkları arasında Stepper bir geçiş olabilir.  
  
> [!NOTE]
> Bu arabirim, çapraz makine ya da çapraz işlem için uzaktan çağrılmakta değil.  
  
## <a name="requirements"></a>Gereksinimler  
 **Platformlar:** Bkz. [sistem gereksinimleri](../../../../docs/framework/get-started/system-requirements.md).  
  
 **Üst bilgi:** CorDebug. IDL, CorDebug. h  
  
 **Kitaplık:** Corguid. lib  
  
 **.NET Framework sürümleri:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>Ayrıca bkz.

- [Hata Ayıklama Arabirimleri](debugging-interfaces.md)
