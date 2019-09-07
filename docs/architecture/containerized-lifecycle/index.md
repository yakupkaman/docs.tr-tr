---
title: Kapsayıcılar ve Docker’a Giriş
description: Docker kullanmanın başlıca avantajlarından yüksek düzeyde bir genel bakış elde edin.
ms.date: 02/15/2019
ms.openlocfilehash: a03c67ed4fbc55c84e69fba5b7978863c8305e00
ms.sourcegitcommit: f20dd18dbcf2275513281f5d9ad7ece6a62644b4
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/30/2019
ms.locfileid: "70295674"
---
# <a name="introduction-to-containers-and-docker"></a><span data-ttu-id="c5692-103">Kapsayıcılara ve Docker 'a giriş</span><span class="sxs-lookup"><span data-stu-id="c5692-103">Introduction to containers and Docker</span></span>

<span data-ttu-id="c5692-104">*Kapsayıcılama, bir uygulama veya hizmetin, bağımlılıklarının ve yapılandırma (dağıtım bildirim dosyaları olarak soyut) bir kapsayıcı görüntüsü olarak birlikte paketlenmekte olan yazılım geliştirme yaklaşımına yönelik bir yaklaşımdır. Daha sonra kapsayıcılı uygulamayı bir birim olarak test edebilir ve onu konak işletim sistemine (OS) bir kapsayıcı görüntüsü örneği olarak dağıtabilirsiniz.*</span><span class="sxs-lookup"><span data-stu-id="c5692-104">*Containerization is an approach to software development in which an application or service, its dependencies, and its configuration (abstracted as deployment manifest files) are packaged together as a container image. You then can test the containerized application as a unit and deploy it as a container image instance to the host operating system (OS).*</span></span>

<span data-ttu-id="c5692-105">Sevkiyat kapsayıcıları, malların içeri, eğitim veya kamyonu içinde yüzden bağımsız olarak aktarıldığına, yazılım kapsayıcıları farklı kod ve bağımlılıklar içerebilen standart bir yazılım dağıtımı birimi görevi görür.</span><span class="sxs-lookup"><span data-stu-id="c5692-105">Just as shipping containers allow goods to be transported by ship, train, or truck regardless of the cargo inside, software containers act as a standard unit of software deployment that can contain different code and dependencies.</span></span> <span data-ttu-id="c5692-106">Yazılımın bu şekilde kapsayıcısız olması, geliştiricilerin ve BT uzmanlarının bunları çok az veya hiç değişiklik yapmadan ortamlar arasında dağıtmasını sağlar.</span><span class="sxs-lookup"><span data-stu-id="c5692-106">Containerizing software this way enables developers and IT professionals to deploy them across environments with little or no modification.</span></span>

<span data-ttu-id="c5692-107">Kapsayıcılar Ayrıca paylaşılan bir işletim sisteminde bulunan uygulamaları birbirinden ayırır.</span><span class="sxs-lookup"><span data-stu-id="c5692-107">Containers also isolate applications from each other on a shared OS.</span></span> <span data-ttu-id="c5692-108">Kapsayıcılı uygulamalar, işletim sistemi üzerinde çalışan bir kapsayıcı konağın üzerinde çalışır (Linux veya Windows).</span><span class="sxs-lookup"><span data-stu-id="c5692-108">Containerized applications run on top of a container host that in turn runs on the OS (Linux or Windows).</span></span> <span data-ttu-id="c5692-109">Bu nedenle kapsayıcılar, sanal makine (VM) görüntülerinden çok daha küçük bir parmak izine sahiptir.</span><span class="sxs-lookup"><span data-stu-id="c5692-109">Containers therefore have a much smaller footprint than virtual machine (VM) images.</span></span>

<span data-ttu-id="c5692-110">Her kapsayıcı Şekil 1-1 ' de gösterildiği gibi bir Web uygulamasını veya bir hizmeti çalıştırabilir.</span><span class="sxs-lookup"><span data-stu-id="c5692-110">Each container can run a whole web application or a service, as shown in Figure 1-1.</span></span> <span data-ttu-id="c5692-111">Bu örnekte, Docker ana bilgisayarı bir kapsayıcı ana bilgisayarı ve APP1, app2, Svc1 ve Svc2 Kapsayıcılı uygulamalar veya hizmetlerdir.</span><span class="sxs-lookup"><span data-stu-id="c5692-111">In this example, Docker host is a container host, and App1, App2, Svc1, and Svc2 are containerized applications or services.</span></span>

![VM 'de veya fiziksel sunucuda işletim sisteminde çalışan iki uygulama ve iki hizmet](./media/image1.png)

<span data-ttu-id="c5692-113">**Şekil 1-1**.</span><span class="sxs-lookup"><span data-stu-id="c5692-113">**Figure 1-1**.</span></span> <span data-ttu-id="c5692-114">Kapsayıcı ana bilgisayarında çalışan birden çok kapsayıcı</span><span class="sxs-lookup"><span data-stu-id="c5692-114">Multiple containers running on a container host</span></span>

<span data-ttu-id="c5692-115">Kapsayıcılardan türetebilmeniz için başka bir avantaj de ölçeklenebilirlik.</span><span class="sxs-lookup"><span data-stu-id="c5692-115">Another benefit you can derive from containerization is scalability.</span></span> <span data-ttu-id="c5692-116">Kısa süreli görevler için yeni kapsayıcılar oluşturarak ölçeği hızla değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c5692-116">You can scale out quickly by creating new containers for short-term tasks.</span></span> <span data-ttu-id="c5692-117">Bir görünüm uygulama noktasından, bir görüntüyü (kapsayıcı oluşturma) başlatmak, hizmet veya Web uygulaması gibi bir işlemi başlatmak için benzerdir.</span><span class="sxs-lookup"><span data-stu-id="c5692-117">From an application point of view, instantiating an image (creating a container) is similar to instantiating a process like a service or web app.</span></span> <span data-ttu-id="c5692-118">Bununla birlikte, aynı görüntünün birden çok konak sunucusunda birden fazla örneğini çalıştırdığınızda, genellikle her kapsayıcının (görüntü örneği) farklı hata etki alanlarında farklı bir konak sunucusunda veya VM 'de çalıştırılmasını istersiniz.</span><span class="sxs-lookup"><span data-stu-id="c5692-118">For reliability, however, when you run multiple instances of the same image across multiple host servers, you typically want each container (image instance) to run in a different host server or VM in different fault domains.</span></span>

<span data-ttu-id="c5692-119">Kısacası, kapsayıcılar tüm uygulama yaşam döngüsü iş akışı genelinde yalıtım, taşınabilirlik, çeviklik, ölçeklenebilirlik ve denetimin avantajlarını sunmaktadır.</span><span class="sxs-lookup"><span data-stu-id="c5692-119">In short, containers offer the benefits of isolation, portability, agility, scalability, and control across the entire application lifecycle workflow.</span></span> <span data-ttu-id="c5692-120">En önemli avantaj geliştirme ve Ops arasında sunulan ortam yalıtımına sahiptir.</span><span class="sxs-lookup"><span data-stu-id="c5692-120">The most important benefit is the environment isolation provided between Dev and Ops.</span></span>

>[!div class="step-by-step"]
>[<span data-ttu-id="c5692-121">Next</span><span class="sxs-lookup"><span data-stu-id="c5692-121">Next</span></span>](what-is-docker.md)