---
title: Bellek sızıntısı öğreticisinde hata ayıklama
description: .NET Core 'da Bellek sızıntısını nasıl ayıklayacağınızı öğrenin.
ms.topic: tutorial
ms.date: 12/17/2019
ms.openlocfilehash: cb137503cbc81f5ab9438dadcf1dc1c6750a1ca8
ms.sourcegitcommit: 5f236cd78cf09593c8945a7d753e0850e96a0b80
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/07/2020
ms.locfileid: "75715598"
---
# <a name="tutorial-debug-a-memory-leak-in-net-core"></a><span data-ttu-id="a1d24-103">Öğretici: .NET Core 'da bellek sızıntısı hatalarını ayıklama</span><span class="sxs-lookup"><span data-stu-id="a1d24-103">Tutorial: Debug a memory leak in .NET Core</span></span>

<span data-ttu-id="a1d24-104">**Bu makale şu şekilde geçerlidir: ✓** .net Core 3,0 SDK ve sonraki sürümleri</span><span class="sxs-lookup"><span data-stu-id="a1d24-104">**This article applies to: ✓** .NET Core 3.0 SDK and later versions</span></span>

<span data-ttu-id="a1d24-105">Bu öğreticide, .NET Core Bellek sızıntısını çözümlemek için Araçlar gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="a1d24-105">This tutorial demonstrates the tools to analyze a .NET Core memory leak.</span></span>

<span data-ttu-id="a1d24-106">Bu öğreticide, kasıtlı olarak bellek sızıntısı için tasarlanan örnek bir uygulama kullanılmaktadır.</span><span class="sxs-lookup"><span data-stu-id="a1d24-106">This tutorial uses a sample app, which is designed to intentionally leak memory.</span></span> <span data-ttu-id="a1d24-107">Örnek, bir alıştırma olarak sağlanır.</span><span class="sxs-lookup"><span data-stu-id="a1d24-107">The sample is provided as an exercise.</span></span> <span data-ttu-id="a1d24-108">Yanlışlıkla bellek sızdıran bir uygulamayı analiz edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a1d24-108">You can analyze an app that is unintentionally leaking memory too.</span></span>

<span data-ttu-id="a1d24-109">Bu öğreticide şunları yapacaksınız:</span><span class="sxs-lookup"><span data-stu-id="a1d24-109">In this tutorial, you will:</span></span>

> [!div class="checklist"]
>
> - <span data-ttu-id="a1d24-110">[DotNet-Counters](dotnet-counters.md)ile yönetilen bellek kullanımını inceleyin.</span><span class="sxs-lookup"><span data-stu-id="a1d24-110">Examine managed memory usage with [dotnet-counters](dotnet-counters.md).</span></span>
> - <span data-ttu-id="a1d24-111">Döküm dosyası oluştur.</span><span class="sxs-lookup"><span data-stu-id="a1d24-111">Generate a dump file.</span></span>
> - <span data-ttu-id="a1d24-112">Döküm dosyasını kullanarak bellek kullanımını çözümleyin.</span><span class="sxs-lookup"><span data-stu-id="a1d24-112">Analyze the memory usage using the dump file.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a1d24-113">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="a1d24-113">Prerequisites</span></span>

<span data-ttu-id="a1d24-114">Öğretici şunları kullanır:</span><span class="sxs-lookup"><span data-stu-id="a1d24-114">The tutorial uses:</span></span>

- <span data-ttu-id="a1d24-115">[.NET Core 3,0 SDK](https://dotnet.microsoft.com/download/dotnet-core) veya sonraki bir sürümü.</span><span class="sxs-lookup"><span data-stu-id="a1d24-115">[.NET Core 3.0 SDK](https://dotnet.microsoft.com/download/dotnet-core) or a later version.</span></span>
- <span data-ttu-id="a1d24-116">[DotNet-](dotnet-trace.md) liste süreçlerini izleme.</span><span class="sxs-lookup"><span data-stu-id="a1d24-116">[dotnet-trace](dotnet-trace.md) to list processes.</span></span>
- <span data-ttu-id="a1d24-117">[DotNet-](dotnet-counters.md) yönetilen bellek kullanımını denetlemek için sayaçlar.</span><span class="sxs-lookup"><span data-stu-id="a1d24-117">[dotnet-counters](dotnet-counters.md) to check managed memory usage.</span></span>
- <span data-ttu-id="a1d24-118">[DotNet-](dotnet-dump.md) döküm dosyasını toplamak ve analiz etmek için döküm.</span><span class="sxs-lookup"><span data-stu-id="a1d24-118">[dotnet-dump](dotnet-dump.md) to collect and analyze a dump file.</span></span>
- <span data-ttu-id="a1d24-119">Tanılama için bir [örnek hata ayıklama hedef](https://docs.microsoft.com/samples/dotnet/samples/diagnostic-scenarios/) uygulaması.</span><span class="sxs-lookup"><span data-stu-id="a1d24-119">A [sample debug target](https://docs.microsoft.com/samples/dotnet/samples/diagnostic-scenarios/) app to diagnose.</span></span>

<span data-ttu-id="a1d24-120">Öğretici, örnek ve araçların yüklendiğini ve kullanıma hazırlandığını varsayar.</span><span class="sxs-lookup"><span data-stu-id="a1d24-120">The tutorial assumes the sample and tools are installed and ready to use.</span></span>

## <a name="examine-managed-memory-usage"></a><span data-ttu-id="a1d24-121">Yönetilen bellek kullanımını incele</span><span class="sxs-lookup"><span data-stu-id="a1d24-121">Examine managed memory usage</span></span>

<span data-ttu-id="a1d24-122">Bu senaryonun köke neden olması için tanılama verileri toplamaya başlamadan önce, aslında bir bellek sızıntısı (bellek büyümesi) gördüğünüzü unutmayın.</span><span class="sxs-lookup"><span data-stu-id="a1d24-122">Before you start collecting diagnostics data to help us root cause this scenario, you need to make sure you're actually seeing a memory leak (memory growth).</span></span> <span data-ttu-id="a1d24-123">Doğrulamak için [DotNet-Counters](dotnet-counters.md) aracını kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a1d24-123">You can use the [dotnet-counters](dotnet-counters.md) tool to confirm that.</span></span>

<span data-ttu-id="a1d24-124">Bir konsol penceresi açın ve [örnek hata ayıklama hedefini](https://docs.microsoft.com/samples/dotnet/samples/diagnostic-scenarios/)indirdiğiniz ve sıkıştırmadan indirdiğiniz dizine gidin.</span><span class="sxs-lookup"><span data-stu-id="a1d24-124">Open a console window and navigate to the directory where you downloaded and unzipped the [sample debug target](https://docs.microsoft.com/samples/dotnet/samples/diagnostic-scenarios/).</span></span> <span data-ttu-id="a1d24-125">Hedefi Çalıştır:</span><span class="sxs-lookup"><span data-stu-id="a1d24-125">Run the target:</span></span>

```dotnetcli
dotnet run
```

<span data-ttu-id="a1d24-126">Ayrı bir konsoldan, [DotNet-Trace](dotnet-trace.md) aracını kullanarak işlem kimliğini bulun:</span><span class="sxs-lookup"><span data-stu-id="a1d24-126">From a separate console, find the process ID using the [dotnet-trace](dotnet-trace.md) tool:</span></span>

```console
dotnet-trace ps
```

<span data-ttu-id="a1d24-127">Çıktı aşağıdakine benzer olmalıdır:</span><span class="sxs-lookup"><span data-stu-id="a1d24-127">The output should be similar to:</span></span>

```console
4807 DiagnosticScena /home/user/git/samples/core/diagnostics/DiagnosticScenarios/bin/Debug/netcoreapp3.0/DiagnosticScenarios
```

<span data-ttu-id="a1d24-128">Şimdi, [DotNet-Counters](dotnet-counters.md) aracıyla yönetilen bellek kullanımını kontrol edin.</span><span class="sxs-lookup"><span data-stu-id="a1d24-128">Now, check managed memory usage with the [dotnet-counters](dotnet-counters.md) tool.</span></span> <span data-ttu-id="a1d24-129">`--refresh-interval` yenilemeler arasındaki saniye sayısını belirtir:</span><span class="sxs-lookup"><span data-stu-id="a1d24-129">The `--refresh-interval` specifies the number of seconds between refreshes:</span></span>

```console
dotnet-counters monitor --refresh-interval 1 -p 4807
```

<span data-ttu-id="a1d24-130">Canlı çıktının şuna benzer olması gerekir:</span><span class="sxs-lookup"><span data-stu-id="a1d24-130">The live output should be similar to:</span></span>

```console
Press p to pause, r to resume, q to quit.
    Status: Running

[System.Runtime]
    # of Assemblies Loaded                           118
    % Time in GC (since last GC)                       0
    Allocation Rate (Bytes / sec)                 37,896
    CPU Usage (%)                                      0
    Exceptions / sec                                   0
    GC Heap Size (MB)                                  4
    Gen 0 GC / sec                                     0
    Gen 0 Size (B)                                     0
    Gen 1 GC / sec                                     0
    Gen 1 Size (B)                                     0
    Gen 2 GC / sec                                     0
    Gen 2 Size (B)                                     0
    LOH Size (B)                                       0
    Monitor Lock Contention Count / sec                0
    Number of Active Timers                            1
    ThreadPool Completed Work Items / sec             10
    ThreadPool Queue Length                            0
    ThreadPool Threads Count                           1
    Working Set (MB)                                  83
```

<span data-ttu-id="a1d24-131">Bu satıra odaklanma:</span><span class="sxs-lookup"><span data-stu-id="a1d24-131">Focusing on this line:</span></span>

```console
    GC Heap Size (MB)                                  4
```

<span data-ttu-id="a1d24-132">Yönetilen yığın belleğinin başlangıçtan sonra 4 MB olduğunu görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a1d24-132">You can see that the managed heap memory is 4 MB right after startup.</span></span>

<span data-ttu-id="a1d24-133">Şimdi URL `http://localhost:5000/api/diagscenario/memleak/20000`' a basın.</span><span class="sxs-lookup"><span data-stu-id="a1d24-133">Now, hit the URL `http://localhost:5000/api/diagscenario/memleak/20000`.</span></span>

<span data-ttu-id="a1d24-134">Bellek kullanımının 30 MB 'a kadar büyüdiğini gözlemleyin.</span><span class="sxs-lookup"><span data-stu-id="a1d24-134">Observe that the memory usage has grown to 30 MB.</span></span>

```console
    GC Heap Size (MB)                                 30
```

<span data-ttu-id="a1d24-135">Bellek kullanımını izleyerek belleğin büyüdüğünü veya sızmasını güvenli bir şekilde söyleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a1d24-135">By watching the memory usage, you can safely say that memory is growing or leaking.</span></span> <span data-ttu-id="a1d24-136">Sonraki adım bellek analizine yönelik doğru verileri toplamaktır.</span><span class="sxs-lookup"><span data-stu-id="a1d24-136">The next step is to collect the right data for memory analysis.</span></span>

### <a name="generate-memory-dump"></a><span data-ttu-id="a1d24-137">Bellek dökümü oluştur</span><span class="sxs-lookup"><span data-stu-id="a1d24-137">Generate memory dump</span></span>

<span data-ttu-id="a1d24-138">Olası bellek sızıntılarını analiz edilirken uygulamanın bellek yığınına erişmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="a1d24-138">When analyzing possible memory leaks, you need access to the app's memory heap.</span></span> <span data-ttu-id="a1d24-139">Daha sonra bellek içeriğini çözümleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a1d24-139">Then you can analyze the memory contents.</span></span> <span data-ttu-id="a1d24-140">Nesneler arasındaki ilişkilere bakarak belleğin neden serbest bırakılmadığına ilişkin bir kayıt oluşturursunuz.</span><span class="sxs-lookup"><span data-stu-id="a1d24-140">Looking at relationships between objects, you create theories on why memory isn't being freed.</span></span> <span data-ttu-id="a1d24-141">Ortak bir tanılama veri kaynağı, Windows 'da bellek dökümleridir veya Linux üzerinde eşdeğer çekirdek dökümleridir.</span><span class="sxs-lookup"><span data-stu-id="a1d24-141">A common diagnostics data source is a memory dump on Windows or the equivalent core dump on Linux.</span></span> <span data-ttu-id="a1d24-142">.NET Core uygulamasının bir dökümünü oluşturmak için [DotNet-dump)](dotnet-dump.md) aracını kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a1d24-142">To generate a dump of a .NET Core application, you can use the [dotnet-dump)](dotnet-dump.md) tool.</span></span>

<span data-ttu-id="a1d24-143">Önceden başlatılan [örnek hata ayıklama hedefini](https://docs.microsoft.com/samples/dotnet/samples/diagnostic-scenarios/) kullanarak bir Linux core dökümü oluşturmak için aşağıdaki komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="a1d24-143">Using the [sample debug target](https://docs.microsoft.com/samples/dotnet/samples/diagnostic-scenarios/) previously started, run the following command to generate a Linux core dump:</span></span>

```dotnetcli
dotnet-dump collect -p 4807
```

<span data-ttu-id="a1d24-144">Sonuç, aynı klasörde bulunan temel bir dökümdir.</span><span class="sxs-lookup"><span data-stu-id="a1d24-144">The result is a core dump located in the same folder.</span></span>

```console
Writing minidump with heap to ./core_20190430_185145
Complete
```

### <a name="restart-the-failed-process"></a><span data-ttu-id="a1d24-145">Başarısız olan işlemi yeniden Başlat</span><span class="sxs-lookup"><span data-stu-id="a1d24-145">Restart the failed process</span></span>

<span data-ttu-id="a1d24-146">Döküm toplandıktan sonra, başarısız olan işlemi tanılamak için yeterli bilgiye sahip olmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="a1d24-146">Once the dump is collected, you should have sufficient information to diagnose the failed process.</span></span> <span data-ttu-id="a1d24-147">Başarısız işlem bir üretim sunucusunda çalışıyorsa, artık işlemi yeniden başlatarak kısa süreli düzeltmeye yönelik ideal bir süredir.</span><span class="sxs-lookup"><span data-stu-id="a1d24-147">If the failed process is running on a production server, now it's the ideal time for short-term remediation by restarting the process.</span></span>

<span data-ttu-id="a1d24-148">Bu öğreticide, şimdi [örnek hata ayıklama hedefini](https://docs.microsoft.com/samples/dotnet/samples/diagnostic-scenarios/) tamamladınız ve kapatabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a1d24-148">In this tutorial, you're now done with the [Sample debug target](https://docs.microsoft.com/samples/dotnet/samples/diagnostic-scenarios/) and you can close it.</span></span> <span data-ttu-id="a1d24-149">Sunucuyu başlatan terminale gidin ve `Control-C`' ye basın.</span><span class="sxs-lookup"><span data-stu-id="a1d24-149">Navigate to the terminal that started the server and press `Control-C`.</span></span>

### <a name="analyze-the-core-dump"></a><span data-ttu-id="a1d24-150">Çekirdek dökümünü analiz etme</span><span class="sxs-lookup"><span data-stu-id="a1d24-150">Analyze the core dump</span></span>

<span data-ttu-id="a1d24-151">Oluşturulan temel bir döküm olduğuna göre, dökümü çözümlemek için [DotNet-dump)](dotnet-dump.md) aracını kullanın:</span><span class="sxs-lookup"><span data-stu-id="a1d24-151">Now that you have a core dump generated, use the [dotnet-dump)](dotnet-dump.md) tool to analyze the dump:</span></span>

```dotnetcli
dotnet-dump analyze core_20190430_185145
```

<span data-ttu-id="a1d24-152">Burada `core_20190430_185145` çözümlemek istediğiniz çekirdek döküm adıdır.</span><span class="sxs-lookup"><span data-stu-id="a1d24-152">Where `core_20190430_185145` is the name of the core dump you want to analyze.</span></span>

> [!NOTE]
> <span data-ttu-id="a1d24-153">*Libdl.so* bulunamadığını belirten bir hata görürseniz, *libc6-dev* paketini yüklemek zorunda kalabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a1d24-153">If you see an error complaining that *libdl.so* cannot be found, you may have to install the *libc6-dev* package.</span></span> <span data-ttu-id="a1d24-154">Daha fazla bilgi için bkz. [Linux üzerinde .NET Core önkoşulları](../linux-prerequisites.md).</span><span class="sxs-lookup"><span data-stu-id="a1d24-154">For more information, see [Prerequisites for .NET Core on Linux](../linux-prerequisites.md).</span></span>

<span data-ttu-id="a1d24-155">SOS komutları girebileceğiniz bir istem sunulur.</span><span class="sxs-lookup"><span data-stu-id="a1d24-155">You'll be presented with a prompt where you can enter SOS commands.</span></span> <span data-ttu-id="a1d24-156">Genellikle, bakmak istediğiniz ilk şey, yönetilen yığının genel durumudur:</span><span class="sxs-lookup"><span data-stu-id="a1d24-156">Commonly, the first thing you want to look at is the overall state of the managed heap:</span></span>

```console
> dumpheap -stat

Statistics:
              MT    Count    TotalSize Class Name
...
00007f6c1eeefba8      576        59904 System.Reflection.RuntimeMethodInfo
00007f6c1dc021c8     1749        95696 System.SByte[]
00000000008c9db0     3847       116080      Free
00007f6c1e784a18      175       128640 System.Char[]
00007f6c1dbf5510      217       133504 System.Object[]
00007f6c1dc014c0      467       416464 System.Byte[]
00007f6c21625038        6      4063376 testwebapi.Controllers.Customer[]
00007f6c20a67498   200000      4800000 testwebapi.Controllers.Customer
00007f6c1dc00f90   206770     19494060 System.String
Total 428516 objects
```

<span data-ttu-id="a1d24-157">Burada çoğu nesnenin `String` veya `Customer` nesneleri olduğunu görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a1d24-157">Here you can see that most objects are either `String` or `Customer` objects.</span></span>

<span data-ttu-id="a1d24-158">Tüm `String` örneklerinin bir listesini almak için yöntem tablosu (MT) ile birlikte `dumpheap` komutunu yeniden kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="a1d24-158">You can use the `dumpheap` command again with the method table (MT) to get a list of all the `String` instances:</span></span>

```console
> dumpheap -mt 00007faddaa50f90

         Address               MT     Size
...
00007f6ad09421f8 00007faddaa50f90       94
...
00007f6ad0965b20 00007f6c1dc00f90       80
00007f6ad0965c10 00007f6c1dc00f90       80
00007f6ad0965d00 00007f6c1dc00f90       80
00007f6ad0965df0 00007f6c1dc00f90       80
00007f6ad0965ee0 00007f6c1dc00f90       80

Statistics:
              MT    Count    TotalSize Class Name
00007f6c1dc00f90   206770     19494060 System.String
Total 206770 objects
```

<span data-ttu-id="a1d24-159">Artık nesnenin nasıl ve neden kök olduğunu görmek için bir `System.String` örneğinde `gcroot` komutunu kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a1d24-159">You can now use the `gcroot` command on a `System.String` instance to see how and why the object is rooted.</span></span> <span data-ttu-id="a1d24-160">Bu komutun 30 MB 'lik bir yığın ile birkaç dakika sürdüğü için sabırlı olun:</span><span class="sxs-lookup"><span data-stu-id="a1d24-160">Be patient because this command takes several minutes with a 30-MB heap:</span></span>

```console
> gcroot -all 00007f6ad09421f8

Thread 3f68:
    00007F6795BB58A0 00007F6C1D7D0745 System.Diagnostics.Tracing.CounterGroup.PollForValues() [/_/src/System.Private.CoreLib/shared/System/Diagnostics/Tracing/CounterGroup.cs @ 260]
        rbx:  (interior)
            ->  00007F6BDFFFF038 System.Object[]
            ->  00007F69D0033570 testwebapi.Controllers.Processor
            ->  00007F69D0033588 testwebapi.Controllers.CustomerCache
            ->  00007F69D00335A0 System.Collections.Generic.List`1[[testwebapi.Controllers.Customer, DiagnosticScenarios]]
            ->  00007F6C000148A0 testwebapi.Controllers.Customer[]
            ->  00007F6AD0942258 testwebapi.Controllers.Customer
            ->  00007F6AD09421F8 System.String

HandleTable:
    00007F6C98BB15F8 (pinned handle)
    -> 00007F6BDFFFF038 System.Object[]
    -> 00007F69D0033570 testwebapi.Controllers.Processor
    -> 00007F69D0033588 testwebapi.Controllers.CustomerCache
    -> 00007F69D00335A0 System.Collections.Generic.List`1[[testwebapi.Controllers.Customer, DiagnosticScenarios]]
    -> 00007F6C000148A0 testwebapi.Controllers.Customer[]
    -> 00007F6AD0942258 testwebapi.Controllers.Customer
    -> 00007F6AD09421F8 System.String

Found 2 roots.
```

<span data-ttu-id="a1d24-161">`String`, `Customer` nesne tarafından doğrudan tutulduğundan ve bir `CustomerCache` nesnesi tarafından dolaylı olarak tutulduğundan emin olabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a1d24-161">You can see that the `String` is directly held by the `Customer` object and indirectly held by a `CustomerCache` object.</span></span>

<span data-ttu-id="a1d24-162">Birçok `String` nesnesinin benzer bir düzende izlediğinden emin olmak için nesnelerin dökümünü almaya devam edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a1d24-162">You can continue dumping out objects to see that most `String` objects follow a similar pattern.</span></span> <span data-ttu-id="a1d24-163">Bu noktada, araştırma kodunuzda kök nedenini belirlemek için yeterli bilgi sağladı.</span><span class="sxs-lookup"><span data-stu-id="a1d24-163">At this point, the investigation provided sufficient information to identify the root cause in your code.</span></span>

<span data-ttu-id="a1d24-164">Bu genel yordam, büyük bellek sızıntılarının kaynağını tanımlamanızı sağlar.</span><span class="sxs-lookup"><span data-stu-id="a1d24-164">This general procedure allows you to identify the source of major memory leaks.</span></span>

## <a name="clean-up-resources"></a><span data-ttu-id="a1d24-165">Kaynakları temizleme</span><span class="sxs-lookup"><span data-stu-id="a1d24-165">Clean up resources</span></span>

<span data-ttu-id="a1d24-166">Bu öğreticide, örnek bir Web sunucusu başladıysanız.</span><span class="sxs-lookup"><span data-stu-id="a1d24-166">In this tutorial, you started a sample web server.</span></span> <span data-ttu-id="a1d24-167">Bu sunucu, [başarısız Işlem yeniden başlatma](#restart-the-failed-process) bölümünde açıklandığı gibi kapatılmış olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="a1d24-167">This server should have been shut down as explained in the [Restart the failed process](#restart-the-failed-process) section.</span></span>

<span data-ttu-id="a1d24-168">Oluşturulan döküm dosyasını da silebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a1d24-168">You can also delete the dump file that was created.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a1d24-169">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="a1d24-169">Next steps</span></span>

<span data-ttu-id="a1d24-170">Tebrikler, bu öğreticiyi tamamlama.</span><span class="sxs-lookup"><span data-stu-id="a1d24-170">Congratulations on completing this tutorial.</span></span>

<span data-ttu-id="a1d24-171">Daha fazla tanılama öğreticilerini yayımlamaya devam ediyoruz.</span><span class="sxs-lookup"><span data-stu-id="a1d24-171">We're still publishing more diagnostic tutorials.</span></span> <span data-ttu-id="a1d24-172">[DotNet/Diagnostics](https://github.com/dotnet/diagnostics/tree/master/documentation/tutorial) deposundaki taslak sürümlerini okuyabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a1d24-172">You can read the draft versions on the [dotnet/diagnostics](https://github.com/dotnet/diagnostics/tree/master/documentation/tutorial) repository.</span></span>

<span data-ttu-id="a1d24-173">Bu öğretici, önemli .NET tanılama araçlarının temellerini ele alınmaktadır.</span><span class="sxs-lookup"><span data-stu-id="a1d24-173">This tutorial covered the basics of key .NET diagnostic tools.</span></span> <span data-ttu-id="a1d24-174">Gelişmiş kullanım için aşağıdaki başvuru belgelerine bakın:</span><span class="sxs-lookup"><span data-stu-id="a1d24-174">For advanced usage, see the following reference documentation:</span></span>

* <span data-ttu-id="a1d24-175">[DotNet-](dotnet-trace.md) liste süreçlerini izleme.</span><span class="sxs-lookup"><span data-stu-id="a1d24-175">[dotnet-trace](dotnet-trace.md) to list processes.</span></span>
* <span data-ttu-id="a1d24-176">[DotNet-](dotnet-counters.md) yönetilen bellek kullanımını denetlemek için sayaçlar.</span><span class="sxs-lookup"><span data-stu-id="a1d24-176">[dotnet-counters](dotnet-counters.md) to check managed memory usage.</span></span>
* <span data-ttu-id="a1d24-177">[DotNet-](dotnet-dump.md) döküm dosyasını toplamak ve analiz etmek için döküm.</span><span class="sxs-lookup"><span data-stu-id="a1d24-177">[dotnet-dump](dotnet-dump.md) to collect and analyze a dump file.</span></span>