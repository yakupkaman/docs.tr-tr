---
title: Hata İletileri
ms.date: 07/20/2015
helpviewer_keywords:
- errors [Visual Basic]
- error messages
- trappable errors
- errors [Visual Basic], trappable
ms.assetid: f2dda05b-baef-41f5-8bb1-598bd7cf239f
ms.openlocfilehash: 15d12802c92e7b9ed99c83885bd38e381c8b687d
ms.sourcegitcommit: 17ee6605e01ef32506f8fdc686954244ba6911de
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/22/2019
ms.locfileid: "74353709"
---
# <a name="error-messages-visual-basic"></a>Hata İletileri (Visual Basic)
Visual Basic bir uygulama yazdığınızda, derlerken veya çalıştırdığınızda aşağıdaki hata türleri meydana gelebilir:  
  
1. Visual Studio 'da bir uygulama yazdığınızda oluşan tasarım zamanı hataları.  
  
2. Visual Studio 'da veya komut isteminde bir uygulama derlerken oluşan derleme zamanı hataları.  
  
3. Visual Studio 'da veya tek başına yürütülebilir dosya olarak bir uygulamayı çalıştırdığınızda oluşan çalışma zamanı hataları.  
  
 Belirli bir hata giderme hakkında daha fazla bilgi için bkz. [Visual Basic programcıları Için ek kaynaklar](../../../visual-basic/getting-started/additional-resources.md).  
  
## <a name="run-time-errors"></a>Çalışma zamanı hataları  
 Visual Basic bir uygulama sistemin yürütemeyeceğini bir eylem gerçekleştirmeye çalışırsa, bir çalışma zamanı hatası oluşur ve Visual Basic bir `Exception` nesnesi oluşturur. Visual Basic, `Throw` ifadesini kullanarak `Exception` nesneleri dahil olmak üzere herhangi bir veri türünde özel hatalar oluşturabilir. Bir uygulama, yakalanan bir özel durumun hata numarasını ve iletisini görüntüleyerek hatayı tanımlayabilir. Bir hata yakalanmazsa, uygulama sonlanır.  
  
 Kod, çalışma zamanı hatalarını yakalayabilir ve inceleyebilir. Hatayı oluşturan kodu bir `Try` bloğunda eklerseniz, eşleşen bir `Catch` bloğunda oluşan herhangi bir hatayı yakalayabilirsiniz. Çalışma zamanında hataları yakalama ve kodunuzda yanıtlama hakkında daha fazla bilgi için bkz [. TRY... Yakala... Finally ekstresi](../../../visual-basic/language-reference/statements/try-catch-finally-statement.md).  
  
## <a name="compile-time-errors"></a>Derleme zamanı hataları  
 Visual Basic Derleyicisi kodda bir sorunla karşılaşırsa, derleme zamanı hatası oluşur. Kod Düzenleyicisi 'nde, bu kod satırının altında dalgalı bir çizgi göründüğünden, hataya neden olan kod satırını kolayca belirleyebilirsiniz. Dalgalı alt çizgiyi işaret ettikten veya **hata listesi**açarsanız, diğer iletileri de gösteren hata iletisi görüntülenir.  
  
 Bir tanımlayıcının altı çizili bir alt çizgi varsa ve en sağdaki karakter altında kısa bir alt çizgi görünürse, sınıf, Oluşturucu, yöntem, özellik, alan veya Enum için bir saplama oluşturabilirsiniz. Daha fazla bilgi için bkz. [kullanımdan oluşturma](/visualstudio/ide/visual-csharp-intellisense#generate-from-usage).
  
 Visual Basic derleyicisinden uyarıları çözümleyerek daha hızlı çalışan ve daha az hata içeren bir kod yazabilirsiniz. Bu uyarılar, uygulama çalıştırıldığında hatalara neden olabilecek kodu belirler. Örneğin derleyici, atanmamış bir nesne değişkeninin bir üyesini çağırmaya çalışırsanız, dönüş değerini ayarlamadan bir işlevden geri dönüş veya özel durumları yakalamak için mantığdaki hatalarla birlikte `Try` bir blok yürütmeye çalıştığınızda sizi uyarır. Bunları açma ve kapatma dahil olmak üzere uyarılar hakkında daha fazla bilgi için bkz. [Visual Basic uyarıları yapılandırma](/visualstudio/ide/configuring-warnings-in-visual-basic).
