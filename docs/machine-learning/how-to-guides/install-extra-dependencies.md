---
title: Ek ML.NET bağımlılıkları yükleyin
description: ML.NET paketlerinin bağımlı olduğu ancak NuGet paketleriyle yüklü olmayan yerel kitaplıkları nasıl yükleyebilirsiniz öğrenin
ms.date: 04/02/2020
author: natke
ms.author: nakersha
ms.custom: how-to
ms.openlocfilehash: 0b870542706c065295d48205b7780e568e267ab6
ms.sourcegitcommit: 2b3b2d684259463ddfc76ad680e5e09fdc1984d2
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80888304"
---
# <a name="install-extra-mlnet-dependencies"></a><span data-ttu-id="0ae83-103">Ek ML.NET bağımlılıkları yükleyin</span><span class="sxs-lookup"><span data-stu-id="0ae83-103">Install extra ML.NET dependencies</span></span>

<span data-ttu-id="0ae83-104">Çoğu durumda, tüm işletim sistemlerinde, ML.NET yüklemek, uygun NuGet paketine başvurmak kadar basittir.</span><span class="sxs-lookup"><span data-stu-id="0ae83-104">In most cases, on all operating systems, installing ML.NET is as simple as referencing the appropriate NuGet package.</span></span>

```bash
dotnet add package Microsoft.ML
```

<span data-ttu-id="0ae83-105">Ancak bazı durumlarda, özellikle yerel bileşenler gerektiğinde ek yükleme gereksinimleri vardır.</span><span class="sxs-lookup"><span data-stu-id="0ae83-105">In some cases though, there are additional installation requirements, particularly when native components are required.</span></span> <span data-ttu-id="0ae83-106">Bu belge, bu servis talepleri için yükleme gereksinimlerini açıklar.</span><span class="sxs-lookup"><span data-stu-id="0ae83-106">This document describes the installation requirements for those cases.</span></span> <span data-ttu-id="0ae83-107">Bölümler, ek bağımlılık `Microsoft.ML.*` olan belirli NuGet paketi tarafından ayrılmıştır.</span><span class="sxs-lookup"><span data-stu-id="0ae83-107">The sections are broken down by the specific `Microsoft.ML.*` NuGet package that has the additional dependency.</span></span>

## <a name="microsoftmltimeseries-microsoftmlautoml"></a><span data-ttu-id="0ae83-108">Microsoft.ML.TimeSeries, Microsoft.ML.AutoML</span><span class="sxs-lookup"><span data-stu-id="0ae83-108">Microsoft.ML.TimeSeries, Microsoft.ML.AutoML</span></span>

<span data-ttu-id="0ae83-109">Bu paketlerin her ikisi `Microsoft.ML.MKL.Redist`de bir bağımlılık var `libiomp`, hangi bir bağımlılığı vardır.</span><span class="sxs-lookup"><span data-stu-id="0ae83-109">Both of these packages have a dependency on `Microsoft.ML.MKL.Redist`, which has a dependency on `libiomp`.</span></span>

### <a name="windows"></a><span data-ttu-id="0ae83-110">Windows</span><span class="sxs-lookup"><span data-stu-id="0ae83-110">Windows</span></span>

<span data-ttu-id="0ae83-111">Ek yükleme adımları gerekmez.</span><span class="sxs-lookup"><span data-stu-id="0ae83-111">No extra installation steps required.</span></span> <span data-ttu-id="0ae83-112">NuGet paketi projeye eklendiğinde kitaplık yüklenir.</span><span class="sxs-lookup"><span data-stu-id="0ae83-112">The library is installed when the NuGet package is added to the project.</span></span>

### <a name="linux"></a><span data-ttu-id="0ae83-113">Linux</span><span class="sxs-lookup"><span data-stu-id="0ae83-113">Linux</span></span>

1. <span data-ttu-id="0ae83-114">Depo için GPG tuşunu yükleyin</span><span class="sxs-lookup"><span data-stu-id="0ae83-114">Install the GPG key for the repository</span></span>

    ```bash
    sudo bash
    # <type your user password when prompted.  this will put you in a root shell>
    # cd to /tmp where this shell has write permission
    cd /tmp
    # now get the key:
    wget https://apt.repos.intel.com/intel-gpg-keys/GPG-PUB-KEY-INTEL-SW-PRODUCTS-2019.PUB
    # now install that key
    apt-key add GPG-PUB-KEY-INTEL-SW-PRODUCTS-2019.PUB
    # now remove the public key file exit the root shell
    rm GPG-PUB-KEY-INTEL-SW-PRODUCTS-2019.PUB
    exit
    ```

2. <span data-ttu-id="0ae83-115">MKL için APT Deposu ekle</span><span class="sxs-lookup"><span data-stu-id="0ae83-115">Add the APT Repository for MKL</span></span>

    ```bash
    sudo sh -c 'echo deb https://apt.repos.intel.com/mkl all main > /etc/apt/sources.list.d/intel-mkl.list'
    ```

3. <span data-ttu-id="0ae83-116">Paketleri güncelleştirin</span><span class="sxs-lookup"><span data-stu-id="0ae83-116">Update packages</span></span>

    ```bash
    sudo apt-get update
    ```

4. <span data-ttu-id="0ae83-117">MKL'yi yükle</span><span class="sxs-lookup"><span data-stu-id="0ae83-117">Install MKL</span></span>

    ```bash
    sudo apt-get install <COMPONENT>-<VERSION>.<UPDATE>-<BUILD_NUMBER>
    ```

    <span data-ttu-id="0ae83-118">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="0ae83-118">For example:</span></span>

    ```bash
    sudo apt-get install intel-mkl-64bit-2020.0-088
    ```

    <span data-ttu-id="0ae83-119">Konumu belirleyin`libiomp.so`</span><span class="sxs-lookup"><span data-stu-id="0ae83-119">Determine the location of `libiomp.so`</span></span>

    ```bash
    find /opt -name "libiomp5.so"
    ```

    <span data-ttu-id="0ae83-120">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="0ae83-120">For example:</span></span>

    ```output
    /opt/intel/compilers_and_libraries_2020.0.166/linux/compiler/lib/intel64_lin/libiomp5.so
    ```

5. <span data-ttu-id="0ae83-121">Bu konumu yük kitaplığı yoluna ekleyin:</span><span class="sxs-lookup"><span data-stu-id="0ae83-121">Add this location to the load library path:</span></span>

    ```bash
    sudo ldconfig /opt/intel/compilers_and_libraries_2020.0.166/linux/compiler/lib/intel64_li
    ```

### <a name="mac"></a><span data-ttu-id="0ae83-122">Mac</span><span class="sxs-lookup"><span data-stu-id="0ae83-122">Mac</span></span>

1. <span data-ttu-id="0ae83-123">Kitaplığı`Homebrew`</span><span class="sxs-lookup"><span data-stu-id="0ae83-123">Install the library with `Homebrew`</span></span>

    ```bash
    brew update && brew install https://raw.githubusercontent.com/Homebrew/homebrew-core/f5b1ac99a7fba27c19cee0bc4f036775c889b359/Formula/libomp.rb && brew link libomp --force
    ```