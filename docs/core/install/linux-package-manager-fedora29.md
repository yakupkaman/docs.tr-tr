---
title: Fedora 29-Package Manager-.NET Core 'a .NET Core 'u yükler
description: .NET Core SDK ve çalışma zamanını Fedora 29 ' a yüklemek için bir paket Yöneticisi kullanın.
author: thraka
ms.author: adegeo
ms.date: 11/06/2019
ms.openlocfilehash: 1507687359adaca41465c82541a079f8eac465df
ms.sourcegitcommit: 9a39f2a06f110c9c7ca54ba216900d038aa14ef3
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/23/2019
ms.locfileid: "74451005"
---
# <a name="fedora-29-package-manager---install-net-core"></a><span data-ttu-id="28d14-103">Fedora 29 Paket Yöneticisi-.NET Core 'ı yükler</span><span class="sxs-lookup"><span data-stu-id="28d14-103">Fedora 29 Package Manager - Install .NET Core</span></span>

[!INCLUDE [package-manager-switcher](./includes/package-manager-switcher.md)]

<span data-ttu-id="28d14-104">Bu makalede, Fedora 29 ' da .NET Core yüklemek için bir paket yöneticisi 'nin nasıl kullanılacağı açıklanır.</span><span class="sxs-lookup"><span data-stu-id="28d14-104">This article describes how to use a package manager to install .NET Core on Fedora 29.</span></span> <span data-ttu-id="28d14-105">Çalışma zamanını yüklüyorsanız, hem .NET Core 'u hem de ASP.NET Core çalışma zamanlarını içerdiğinden [ASP.NET Core çalışma zamanını](#install-the-aspnet-core-runtime)yüklemenizi öneririz.</span><span class="sxs-lookup"><span data-stu-id="28d14-105">If you're installing the runtime, we suggest you install the [ASP.NET Core runtime](#install-the-aspnet-core-runtime), as it includes both .NET Core and ASP.NET Core runtimes.</span></span>

## <a name="register-microsoft-key-and-feed"></a><span data-ttu-id="28d14-106">Microsoft anahtar ve akışını Kaydet</span><span class="sxs-lookup"><span data-stu-id="28d14-106">Register Microsoft key and feed</span></span>

<span data-ttu-id="28d14-107">.NET yüklemeden önce şunları yapmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="28d14-107">Before installing .NET, you'll need to:</span></span>

- <span data-ttu-id="28d14-108">Microsoft anahtarını kaydetme</span><span class="sxs-lookup"><span data-stu-id="28d14-108">Register the Microsoft key</span></span>
- <span data-ttu-id="28d14-109">Ürün deposunu kaydetme</span><span class="sxs-lookup"><span data-stu-id="28d14-109">register the product repository</span></span>
- <span data-ttu-id="28d14-110">Gerekli bağımlılıkları yükler</span><span class="sxs-lookup"><span data-stu-id="28d14-110">Install required dependencies</span></span>

<span data-ttu-id="28d14-111">Bu, makine başına yalnızca bir kez yapılmalıdır.</span><span class="sxs-lookup"><span data-stu-id="28d14-111">This only needs to be done once per machine.</span></span>

<span data-ttu-id="28d14-112">Bir Terminal açın ve aşağıdaki komutları çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="28d14-112">Open a terminal and run the following commands.</span></span>

```bash
sudo rpm --import https://packages.microsoft.com/keys/microsoft.asc
sudo wget -q -O /etc/yum.repos.d/microsoft-prod.repo https://packages.microsoft.com/config/fedora/29/prod.repo
```

## <a name="install-the-net-core-sdk"></a><span data-ttu-id="28d14-113">.NET Core SDK 'i yükler</span><span class="sxs-lookup"><span data-stu-id="28d14-113">Install the .NET Core SDK</span></span>

<span data-ttu-id="28d14-114">Yükleme için kullanılabilen ürünleri güncelleştirin, ardından .NET Core SDK yükleme.</span><span class="sxs-lookup"><span data-stu-id="28d14-114">Update the products available for installation, then install the .NET Core SDK.</span></span> <span data-ttu-id="28d14-115">Terminalinizde aşağıdaki komutu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="28d14-115">In your terminal, run the following command.</span></span>

```bash
sudo dnf install dotnet-sdk-3.0
```

## <a name="install-the-aspnet-core-runtime"></a><span data-ttu-id="28d14-116">ASP.NET Core çalışma zamanını yükler</span><span class="sxs-lookup"><span data-stu-id="28d14-116">Install the ASP.NET Core runtime</span></span>

<span data-ttu-id="28d14-117">Yükleme için kullanılabilen ürünleri güncelleştirin, sonra ASP.NET çalışma zamanını yükleme.</span><span class="sxs-lookup"><span data-stu-id="28d14-117">Update the products available for installation, then install the ASP.NET runtime.</span></span> <span data-ttu-id="28d14-118">Terminalinizde aşağıdaki komutu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="28d14-118">In your terminal, run the following command.</span></span>

```bash
sudo dnf install aspnetcore-runtime-3.0
```

## <a name="install-the-net-core-runtime"></a><span data-ttu-id="28d14-119">.NET Core çalışma zamanını yükler</span><span class="sxs-lookup"><span data-stu-id="28d14-119">Install the .NET Core runtime</span></span>

<span data-ttu-id="28d14-120">Yükleme için kullanılabilen ürünleri güncelleştirin ve ardından .NET Core çalışma zamanı 'nı yükleme.</span><span class="sxs-lookup"><span data-stu-id="28d14-120">Update the products available for installation, then install the .NET Core runtime.</span></span> <span data-ttu-id="28d14-121">Terminalinizde aşağıdaki komutu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="28d14-121">In your terminal, run the following command.</span></span>

```bash
sudo dnf install dotnet-runtime-3.0
```

## <a name="how-to-install-other-versions"></a><span data-ttu-id="28d14-122">Diğer sürümleri nasıl yüklenir</span><span class="sxs-lookup"><span data-stu-id="28d14-122">How to install other versions</span></span>

[!INCLUDE [package-manager-switcher](./includes/package-manager-heading-hack-pkgname.md)]