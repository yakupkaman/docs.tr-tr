---
title: Yerel birlikte çalışabilirliği - .NET
description: . NET'te yerel bileşenleriyle arabirim öğrenin.
author: jkoritzinsky
ms.author: jekoritz
ms.date: 01/18/2019
ms.openlocfilehash: 85a22394c8c59f51f462bc0a2ba6a11265682db3
ms.sourcegitcommit: b56d59ad42140d277f2acbd003b74d655fdbc9f1
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/19/2019
ms.locfileid: "54416241"
---
# <a name="native-interoperability"></a><span data-ttu-id="a19fa-103">Yerel birlikte çalışabilirliği</span><span class="sxs-lookup"><span data-stu-id="a19fa-103">Native interoperability</span></span>

<span data-ttu-id="a19fa-104">Aşağıdaki makaleler, "yerel birlikte çalışabilirlik".NET yapmanın çeşitli yollarını göstermektedir.</span><span class="sxs-lookup"><span data-stu-id="a19fa-104">The following articles show the various ways of doing "native interoperability" in .NET.</span></span>

<span data-ttu-id="a19fa-105">Neden yerel kod içine çağırmak istiyorsunuz birkaç nedeni vardır:</span><span class="sxs-lookup"><span data-stu-id="a19fa-105">There are a few reasons why you'd want to call into native code:</span></span>

* <span data-ttu-id="a19fa-106">İşletim sistemleri, büyük hacimli yönetilen sınıf kitaplıklarında bulunmayan API'leri ile gelir.</span><span class="sxs-lookup"><span data-stu-id="a19fa-106">Operating systems come with a large volume of APIs that aren't present in the managed class libraries.</span></span> <span data-ttu-id="a19fa-107">Bu senaryo için birinci bir örnek, donanım veya işletim sistemi yönetim işlevlerine erişimi olacaktır.</span><span class="sxs-lookup"><span data-stu-id="a19fa-107">A prime example for this scenario would be access to hardware or operating system management functions.</span></span>
* <span data-ttu-id="a19fa-108">C stili Abı'ler (yerel Abı'ler) oluşturabilir veya diğer bileşenlerle aracılığıyla gösterilir, Java kodu gibi iletişim kurarak [Java yerel arabirimi (JNI)](https://docs.oracle.com/javase/8/docs/technotes/guides/jni/) veya yerel bir bileşeni oluşturabilecek herhangi bir yönetilen dil.</span><span class="sxs-lookup"><span data-stu-id="a19fa-108">Communicating with other components that have or can produce C-style ABIs (native ABIs), such as Java code that is exposed via [Java Native Interface (JNI)](https://docs.oracle.com/javase/8/docs/technotes/guides/jni/) or any other managed language that could produce a native component.</span></span>
* <span data-ttu-id="a19fa-109">Windows üzerinde çoğu, Microsoft Office suite gibi yüklenen yazılım programlarını temsil eder ve bunları otomatik hale getirmek ya da kullandığınız geliştiricilerin izin veren COM bileşenlerini kaydeder.</span><span class="sxs-lookup"><span data-stu-id="a19fa-109">On Windows, most of the software that gets installed, such as the Microsoft Office suite, registers COM components that represent their programs and allow developers to automate them or use them.</span></span> <span data-ttu-id="a19fa-110">Bu ayrıca yerel birlikte çalışabilirliği gerektirir.</span><span class="sxs-lookup"><span data-stu-id="a19fa-110">This also requires native interoperability.</span></span>

<span data-ttu-id="a19fa-111">Önceki listede tüm olası durumlar ve hangi geliştirici istediğiniz/gibi/yerel bileşenleriyle arabirim oluşturmak için gerekecek senaryoları ele alınmamıştır.</span><span class="sxs-lookup"><span data-stu-id="a19fa-111">The previous list doesn't cover all of the potential situations and scenarios in which the developer would want/like/need to interface with native components.</span></span> <span data-ttu-id="a19fa-112">.NET sınıf kitaplığı, yerel birlikte çalışabilirliği destek adil birkaç Konsolu desteği ve işleme, dosya sistemi erişimini ve diğerleri gibi kendi API uygulamak için örneği için kullanır.</span><span class="sxs-lookup"><span data-stu-id="a19fa-112">.NET class library, for instance, uses the native interoperability support to implement a fair number of its APIs, like console support and manipulation, file system access and others.</span></span> <span data-ttu-id="a19fa-113">Ancak, gerekirse bir seçenek olduğuna dikkat edin önemlidir.</span><span class="sxs-lookup"><span data-stu-id="a19fa-113">However, it's important to note that there's an option if needed.</span></span>

> [!NOTE]
> <span data-ttu-id="a19fa-114">Bu bölümdeki örnekler çoğu için üç tüm desteklenen platformlar için .NET Core (Windows, Linux ve macOS) sunulur.</span><span class="sxs-lookup"><span data-stu-id="a19fa-114">Most of the examples in this section will be presented for all three supported platforms for .NET Core (Windows, Linux and macOS).</span></span> <span data-ttu-id="a19fa-115">Ancak, bazı kısa ve yalnızca tanım örnekler için Windows dosya adları ve uzantıları (diğer bir deyişle, kitaplıkları için "dll") kullanan tek bir örnek gösterilir.</span><span class="sxs-lookup"><span data-stu-id="a19fa-115">However, for some short and illustrative examples, just one sample is shown that uses Windows filenames and extensions (that is, "dll" for libraries).</span></span> <span data-ttu-id="a19fa-116">Bu özelliklerden Linux veya Macos'ta kullanılabilir değil, yalnızca bu çok kolaylık sağlamak için yapılmıştır gelmez.</span><span class="sxs-lookup"><span data-stu-id="a19fa-116">This doesn't mean that those features aren't available on Linux or macOS, it was done merely for convenience sake.</span></span>

## <a name="see-also"></a><span data-ttu-id="a19fa-117">Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="a19fa-117">See also</span></span>

- [<span data-ttu-id="a19fa-118">Platform Çağırma (P/Invoke)</span><span class="sxs-lookup"><span data-stu-id="a19fa-118">Platform Invoke (P/Invoke)</span></span>](pinvoke.md)
- [<span data-ttu-id="a19fa-119">Türü taşıma</span><span class="sxs-lookup"><span data-stu-id="a19fa-119">Type marshalling</span></span>](type-marshalling.md)