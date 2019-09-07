---
title: Docker uygulamaları için iç döngü geliştirme iş akışı
description: Docker uygulamalarının geliştirilmesi için "Inner loop" iş akışını öğrenin.
ms.date: 02/15/2019
ms.openlocfilehash: ce573546f61b98c2f93e998203497fa949e9efe8
ms.sourcegitcommit: f20dd18dbcf2275513281f5d9ad7ece6a62644b4
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/30/2019
ms.locfileid: "70295847"
---
# <a name="inner-loop-development-workflow-for-docker-apps"></a><span data-ttu-id="cb766-103">Docker uygulamaları için iç döngü geliştirme iş akışı</span><span class="sxs-lookup"><span data-stu-id="cb766-103">Inner-loop development workflow for Docker apps</span></span>

<span data-ttu-id="cb766-104">Tüm DevOps döngüsünü kapsayan dış döngü iş akışını tetiklemeden önce, hepsi her bir geliştirici makinesinde başlar, tercih edilen dillerini veya platformları kullanarak uygulamanın kendisini kodlayıp yerel olarak test edin (Şekil 4-21).</span><span class="sxs-lookup"><span data-stu-id="cb766-104">Before triggering the outer-loop workflow spanning the entire DevOps cycle, it all begins on each developer's machine, coding the app itself, using their preferred languages or platforms, and testing it locally (Figure 4-21).</span></span> <span data-ttu-id="cb766-105">Ancak her durumda, sizin seçtiğiniz dil, çerçeve veya platformlardan bağımsız olarak, genel olarak önemli bir noktaya sahip olacaksınız.</span><span class="sxs-lookup"><span data-stu-id="cb766-105">But in every case, you'll have an important point in common, no matter what language, framework, or platforms you choose.</span></span> <span data-ttu-id="cb766-106">Bu belirli iş akışında, her zaman Docker kapsayıcılarını geliştirmekte ve test eteceğiz, ancak yerel olarak.</span><span class="sxs-lookup"><span data-stu-id="cb766-106">In this specific workflow, you're always developing and testing Docker containers, but locally.</span></span>

![Adım 1-kod/çalıştırma/hata ayıklama](./media/image18.png)

<span data-ttu-id="cb766-108">**Şekil 4-21**.</span><span class="sxs-lookup"><span data-stu-id="cb766-108">**Figure 4-21**.</span></span> <span data-ttu-id="cb766-109">İç döngü geliştirme bağlamı</span><span class="sxs-lookup"><span data-stu-id="cb766-109">Inner-loop development context</span></span>

<span data-ttu-id="cb766-110">Bir Docker görüntüsünün kapsayıcısı veya örneği şu bileşenleri içerir:</span><span class="sxs-lookup"><span data-stu-id="cb766-110">The container or instance of a Docker image will contain these components:</span></span>

- <span data-ttu-id="cb766-111">Bir işletim sistemi seçimi (örneğin, bir Linux dağıtımı veya Windows)</span><span class="sxs-lookup"><span data-stu-id="cb766-111">An operating system selection (for example, a Linux distribution or Windows)</span></span>

- <span data-ttu-id="cb766-112">Geliştirici tarafından eklenen dosyalar (örneğin, uygulama ikilileri)</span><span class="sxs-lookup"><span data-stu-id="cb766-112">Files added by the developer (for example, app binaries)</span></span>

- <span data-ttu-id="cb766-113">Yapılandırma (örneğin, ortam ayarları ve bağımlılıklar)</span><span class="sxs-lookup"><span data-stu-id="cb766-113">Configuration (for example, environment settings and dependencies)</span></span>

- <span data-ttu-id="cb766-114">Docker tarafından hangi işlemlerin çalıştırılacağını gösteren yönergeler</span><span class="sxs-lookup"><span data-stu-id="cb766-114">Instructions for what processes to run by Docker</span></span>

<span data-ttu-id="cb766-115">İşlem olarak Docker kullanan iç döngü geliştirme iş akışını (sonraki bölümde açıklanmıştır) ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="cb766-115">You can set up the inner-loop development workflow that utilizes Docker as the process (described in the next section).</span></span> <span data-ttu-id="cb766-116">Yalnızca bir kez yapmanız gerektiğinden, ortamı ayarlamaya yönelik ilk adımların dahil edilmediğini göz önünde bulundurun.</span><span class="sxs-lookup"><span data-stu-id="cb766-116">Consider that the initial steps to set up the environment are not included, because you only need to do it once.</span></span>

## <a name="building-a-single-app-within-a-docker-container-using-visual-studio-code-and-docker-cli"></a><span data-ttu-id="cb766-117">Visual Studio Code ve Docker CLı kullanarak bir Docker kapsayıcısı içinde tek bir uygulama oluşturma</span><span class="sxs-lookup"><span data-stu-id="cb766-117">Building a single app within a Docker container using Visual Studio Code and Docker CLI</span></span>

<span data-ttu-id="cb766-118">Uygulamalar, kendi hizmetinizden ve ek kitaplıklardan (bağımlılıklar) oluşur.</span><span class="sxs-lookup"><span data-stu-id="cb766-118">Apps are made up from your own services plus additional libraries (dependencies).</span></span>

<span data-ttu-id="cb766-119">Şekil 4-22, genellikle bir Docker uygulaması oluştururken gerçekleştirmeniz gereken temel adımları gösterir ve ardından her adımın ayrıntılı açıklamalarını izler.</span><span class="sxs-lookup"><span data-stu-id="cb766-119">Figure 4-22 shows the basic steps that you usually need to carry out when building a Docker app, followed by detailed descriptions of each step.</span></span>

![İş akışına genel bakış: Adım 1-kod, adım 2-Dockerfiles 'ı yazma, adım 3-Dockerfiles ile tanımlanmış görüntüleri oluşturma, 4. adım-Docker-Compose ile Hizmetleri tanımlama, 5. adım-kapsayıcıları veya oluşturulan uygulamaları çalıştırın, 6. adım-test uygulamaları, adım 7-gönder-dış döngüyü (CI/CD işlem hatları) başlatın veya devam edin veloping.](./media/image19.png)

<span data-ttu-id="cb766-121">**Şekil 4-22**.</span><span class="sxs-lookup"><span data-stu-id="cb766-121">**Figure 4-22**.</span></span> <span data-ttu-id="cb766-122">Docker CLı kullanan Docker Kapsayıcılı uygulamalar için yaşam döngüsü için üst düzey iş akışı</span><span class="sxs-lookup"><span data-stu-id="cb766-122">High-level workflow for the life cycle for Docker containerized applications using Docker CLI</span></span>

### <a name="step-1-start-coding-in-visual-studio-code-and-create-your-initial-appservice-baseline"></a><span data-ttu-id="cb766-123">1\. Adım: Visual Studio Code kodlama başlatın ve ilk uygulamanızı/hizmet temelinizi oluşturun</span><span class="sxs-lookup"><span data-stu-id="cb766-123">Step 1: Start coding in Visual Studio Code and create your initial app/service baseline</span></span>

<span data-ttu-id="cb766-124">Uygulamanızı geliştirme yönteminiz, Docker olmadan yaptığınız yönteme benzerdir.</span><span class="sxs-lookup"><span data-stu-id="cb766-124">The way you develop your application is similar to the way you do it without Docker.</span></span> <span data-ttu-id="cb766-125">Bu fark, geliştirme sırasında uygulamanızı veya hizmetlerinizi yerel ortamınıza (Linux VM veya Windows gibi) yerleştirilmiş olan Docker Kapsayıcıları içinde çalışan, dağıtmanıza ve test etdiğinize göre yapılır.</span><span class="sxs-lookup"><span data-stu-id="cb766-125">The difference is that while developing, you're deploying and testing your application or services running within Docker containers placed in your local environment (like a Linux VM or Windows).</span></span>

<span data-ttu-id="cb766-126">**Yerel ortamınızı ayarlama**</span><span class="sxs-lookup"><span data-stu-id="cb766-126">**Setting up your local environment**</span></span>

<span data-ttu-id="cb766-127">Mac ve Windows için Docker 'ın en son sürümlerinde, Docker uygulamalarının geliştirilmesi her zamankinden daha kolay olur ve Kurulum basittir.</span><span class="sxs-lookup"><span data-stu-id="cb766-127">With the latest versions of Docker for Mac and Windows, it's easier than ever to develop Docker applications, and the setup is straightforward.</span></span>

> <span data-ttu-id="cb766-128">[! BILGI</span><span class="sxs-lookup"><span data-stu-id="cb766-128">[!INFORMATION]</span></span>
>
> <span data-ttu-id="cb766-129">Docker for Windows ayarlama hakkında yönergeler için bölümüne gidin <https://docs.docker.com/docker-for-windows/>.</span><span class="sxs-lookup"><span data-stu-id="cb766-129">For instructions on setting up Docker for Windows, go to <https://docs.docker.com/docker-for-windows/>.</span></span>
>
><span data-ttu-id="cb766-130">Mac için Docker 'ı ayarlamaya ilişkin yönergeler için adresine gidin <https://docs.docker.com/docker-for-mac/>.</span><span class="sxs-lookup"><span data-stu-id="cb766-130">For instructions on setting up Docker for Mac, go to <https://docs.docker.com/docker-for-mac/>.</span></span>

<span data-ttu-id="cb766-131">Ayrıca, Docker CLı kullanırken uygulamanızı geliştirebilmeniz için bir kod düzenleyicisine gerek duyarsınız.</span><span class="sxs-lookup"><span data-stu-id="cb766-131">In addition, you'll need a code editor so that you can actually develop your application while using Docker CLI.</span></span>

<span data-ttu-id="cb766-132">Microsoft, Mac, Windows ve Linux 'ta desteklenen basit bir kod Düzenleyicisi olan Visual Studio Code sağlar ve IntelliSense 'i [birçok dil](https://code.visualstudio.com/docs/languages/overview) (JavaScript, .net, Go, Java, Ruby, Python ve en modern diller) [için destek sağlar. hata ayıklama](https://code.visualstudio.com/Docs/editor/debugging), git ve uzantılar [ile tümleştirme](https://code.visualstudio.com/Docs/editor/versioncontrol) [desteği](https://code.visualstudio.com/docs/extensions/overview).</span><span class="sxs-lookup"><span data-stu-id="cb766-132">Microsoft provides Visual Studio Code, which is a lightweight code editor that's supported on Mac, Windows, and Linux, and provides IntelliSense with [support for many languages](https://code.visualstudio.com/docs/languages/overview) (JavaScript, .NET, Go, Java, Ruby, Python, and most modern languages), [debugging](https://code.visualstudio.com/Docs/editor/debugging), [integration with Git](https://code.visualstudio.com/Docs/editor/versioncontrol) and [extensions support](https://code.visualstudio.com/docs/extensions/overview).</span></span> <span data-ttu-id="cb766-133">Bu düzenleyici Mac ve Linux geliştiricileri için harika bir uyum.</span><span class="sxs-lookup"><span data-stu-id="cb766-133">This editor is a great fit for Mac and Linux developers.</span></span> <span data-ttu-id="cb766-134">Windows 'da, tam Visual Studio uygulamasını da kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="cb766-134">In Windows, you also can use the full Visual Studio application.</span></span>

> <span data-ttu-id="cb766-135">[! BILGI</span><span class="sxs-lookup"><span data-stu-id="cb766-135">[!INFORMATION]</span></span>
>
> <span data-ttu-id="cb766-136">Windows, Mac veya Linux için Visual Studio Code yükleme yönergeleri için adresine gidin <https://code.visualstudio.com/docs/setup/setup-overview/>.</span><span class="sxs-lookup"><span data-stu-id="cb766-136">For instructions on installing Visual Studio Code for Windows, Mac, or Linux, go to <https://code.visualstudio.com/docs/setup/setup-overview/>.</span></span>
>
> <span data-ttu-id="cb766-137">Mac için Docker 'ı ayarlamaya ilişkin yönergeler için adresine gidin <https://docs.docker.com/docker-for-mac/>.</span><span class="sxs-lookup"><span data-stu-id="cb766-137">For instructions on setting up Docker for Mac, go to <https://docs.docker.com/docker-for-mac/>.</span></span>

<span data-ttu-id="cb766-138">Docker CLI ile çalışabilir ve herhangi bir kod Düzenleyicisi kullanarak kodunuzu yazabilirsiniz, ancak Docker uzantısıyla Visual Studio Code kullanmak, çalışma alanınızdaki yazma `Dockerfile` ve `docker-compose.yml` dosyaları daha kolay hale getirir.</span><span class="sxs-lookup"><span data-stu-id="cb766-138">You can work with Docker CLI and write your code using any code editor, but using Visual Studio Code with the Docker extension makes it easy to author `Dockerfile` and `docker-compose.yml` files in your workspace.</span></span> <span data-ttu-id="cb766-139">Ayrıca, altındaki Docker CLı kullanarak Docker komutlarını yürütmek için Visual Studio Code IDE 'den görevler ve betikler çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="cb766-139">You can also run tasks and scripts from the Visual Studio Code IDE to execute Docker commands using the Docker CLI underneath.</span></span>

<span data-ttu-id="cb766-140">VS Code için Docker uzantısı aşağıdaki özellikleri sağlar:</span><span class="sxs-lookup"><span data-stu-id="cb766-140">The Docker extension for VS Code provides the following features:</span></span>

- <span data-ttu-id="cb766-141">Otomatik `Dockerfile` ve`docker-compose.yml` dosya oluşturma</span><span class="sxs-lookup"><span data-stu-id="cb766-141">Automatic `Dockerfile` and `docker-compose.yml` file generation</span></span>

- <span data-ttu-id="cb766-142">`docker-compose.yml` Ve`Dockerfile` dosyaları için sözdizimi vurgulama ve üzerine gelme ipuçları</span><span class="sxs-lookup"><span data-stu-id="cb766-142">Syntax highlighting and hover tips for `docker-compose.yml` and `Dockerfile` files</span></span>

- <span data-ttu-id="cb766-143">`Dockerfile` Ve`docker-compose.yml` dosyaları için IntelliSense (tamamlama)</span><span class="sxs-lookup"><span data-stu-id="cb766-143">IntelliSense (completions) for `Dockerfile` and `docker-compose.yml` files</span></span>

- <span data-ttu-id="cb766-144">Dosyalar için `Dockerfile` linme (hatalar ve uyarılar)</span><span class="sxs-lookup"><span data-stu-id="cb766-144">Linting (errors and warnings) for `Dockerfile` files</span></span>

- <span data-ttu-id="cb766-145">En yaygın Docker komutları için komut paleti (F1) Tümleştirmesi</span><span class="sxs-lookup"><span data-stu-id="cb766-145">Command Palette (F1) integration for the most common Docker commands</span></span>

- <span data-ttu-id="cb766-146">Görüntüleri ve kapsayıcıları yönetmek için Gezgin tümleştirmesi</span><span class="sxs-lookup"><span data-stu-id="cb766-146">Explorer integration for managing Images and Containers</span></span>

- <span data-ttu-id="cb766-147">DockerHub ve Azure Container kayıt defterlerinden görüntüleri Azure App Service için dağıtma</span><span class="sxs-lookup"><span data-stu-id="cb766-147">Deploy images from DockerHub and Azure Container Registries to Azure App Service</span></span>

<span data-ttu-id="cb766-148">Docker uzantısını yüklemek için CTRL + SHIFT + P tuşlarına basın, yazın `ext install`ve sonra da Market uzantı listesini açmak için uzantı Install komutunu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="cb766-148">To install the Docker extension, press Ctrl+Shift+P, type `ext install`, and then run the Install Extension command to bring up the Marketplace extension list.</span></span> <span data-ttu-id="cb766-149">Sonra, sonuçları filtrelemek için **Docker** yazın ve Şekil 4-23 ' de gösterildiği gibi Docker destek uzantısını seçin.</span><span class="sxs-lookup"><span data-stu-id="cb766-149">Next, type **docker** to filter the results, and then select the Docker Support extension, as depicted in Figure 4-23.</span></span>

![VS Code için Docker uzantısının görünümü.](./media/image20.png)

<span data-ttu-id="cb766-151">**Şekil 4-23**.</span><span class="sxs-lookup"><span data-stu-id="cb766-151">**Figure 4-23**.</span></span> <span data-ttu-id="cb766-152">Visual Studio Code Docker uzantısını yükleme</span><span class="sxs-lookup"><span data-stu-id="cb766-152">Installing the Docker Extension in Visual Studio Code</span></span>

### <a name="step-2-create-a-dockerfile-related-to-an-existing-image-plain-os-or-dev-environments-like-net-core-nodejs-and-ruby"></a><span data-ttu-id="cb766-153">2\. Adım: Var olan bir görüntüyle ilişkili bir DockerFile oluşturma (.NET Core, Node. js ve Ruby gibi basit işletim sistemleri veya geliştirme ortamları)</span><span class="sxs-lookup"><span data-stu-id="cb766-153">Step 2: Create a DockerFile related to an existing image (plain OS or dev environments like .NET Core, Node.js, and Ruby)</span></span>

<span data-ttu-id="cb766-154">Dağıtılması için bir `DockerFile` özel görüntü ve dağıtılacak kapsayıcı başına ihtiyacınız vardır.</span><span class="sxs-lookup"><span data-stu-id="cb766-154">You'll need a `DockerFile` per custom image to be built and per container to be deployed.</span></span> <span data-ttu-id="cb766-155">Uygulamanız tek bir özel hizmetten yapılırsa, tek `DockerFile`yapmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="cb766-155">If your app is made up of a single custom service, you'll need a single `DockerFile`.</span></span> <span data-ttu-id="cb766-156">Ancak uygulamanız birden çok hizmetten oluşuyorsa (bir mikro hizmet mimarisinde olduğu gibi), hizmet başına bir tane `Dockerfile` gerekir.</span><span class="sxs-lookup"><span data-stu-id="cb766-156">But if your app is composed of multiple services (as in a microservices architecture), you'll need one `Dockerfile` per service.</span></span>

<span data-ttu-id="cb766-157">`DockerFile` Genellikle uygulamanızın veya hizmetinizin kök klasörüne yerleştirilir ve Docker 'ın o uygulamayı veya hizmeti nasıl ayarlayacağını ve çalıştıracağını bilmesi için gerekli komutları içerir.</span><span class="sxs-lookup"><span data-stu-id="cb766-157">The `DockerFile` is commonly placed in the root folder of your app or service and contains the required commands so that Docker knows how to set up and run that app or service.</span></span> <span data-ttu-id="cb766-158">Kodunuzu oluşturup `DockerFile` projenize (node. js, .NET Core vb.) birlikte ekleyebilirsiniz, ya da ortama yeni başladıysanız aşağıdaki ipucuna göz atın.</span><span class="sxs-lookup"><span data-stu-id="cb766-158">You can create your `DockerFile` and add it to your project along with your code (node.js, .NET Core, etc.), or, if you're new to the environment, take a look at the following Tip.</span></span>

> [!TIP]
>
> <span data-ttu-id="cb766-159">Docker kapsayıcılarınız `Dockerfile` ile ilgili ve `docker-compose.yml` dosyalarını kullanırken size rehberlik etmek için Docker uzantısını kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="cb766-159">You can use the Docker extension to guide you when using the `Dockerfile` and `docker-compose.yml` files related to your Docker containers.</span></span> <span data-ttu-id="cb766-160">Sonuç olarak, bu tür dosyaları bu araç olmadan yazarsınız, ancak Docker uzantısının kullanılması, öğrenme eğinizi hızlandırmaya yönelik iyi bir başlangıç noktasıdır.</span><span class="sxs-lookup"><span data-stu-id="cb766-160">Eventually, you'll probably write these kinds of files without this tool, but using the Docker extension is a good starting point that will accelerate your learning curve.</span></span>

<span data-ttu-id="cb766-161">Şekil 4-24 ' de, bir Docker-Compose dosyasının VS Code için Docker uzantısını kullanarak nasıl eklendiğini görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="cb766-161">In Figure 4-24, you can see how a docker-compose file is added by using the Docker Extension for VS Code.</span></span>

![VS Code için Docker uzantısının konsol görünümü.](./media/image24.png)

<span data-ttu-id="cb766-163">**Şekil 4-24**.</span><span class="sxs-lookup"><span data-stu-id="cb766-163">**Figure 4-24**.</span></span> <span data-ttu-id="cb766-164">**Çalışma alanına Docker dosyaları Ekle komutu** kullanılarak Docker dosyaları eklendi</span><span class="sxs-lookup"><span data-stu-id="cb766-164">Docker files added using the **Add Docker files to Workspace command**</span></span>

<span data-ttu-id="cb766-165">Bir DockerFile eklediğinizde, kullanacağınız temel Docker görüntüsünü (kullanma `FROM mcr.microsoft.com/dotnet/core/aspnet`gibi) belirtirsiniz.</span><span class="sxs-lookup"><span data-stu-id="cb766-165">When you add a DockerFile, you specify what base Docker image you’ll be using (like using `FROM mcr.microsoft.com/dotnet/core/aspnet`).</span></span> <span data-ttu-id="cb766-166">Genellikle, [Docker Hub kayıt defterindeki](https://hub.docker.com/) ( [.NET Core](https://hub.docker.com/_/microsoft-dotnet-core/) veya [Node. js için](https://hub.docker.com/_/node/)bir görüntü gibi) herhangi bir resmi depodan aldığınız bir temel görüntünün en üstünde özel görüntünüzü oluşturacaksınız.</span><span class="sxs-lookup"><span data-stu-id="cb766-166">You'll usually build your custom image on top of a base image that you get from any official repository at the [Docker Hub registry](https://hub.docker.com/) (like an [image for .NET Core](https://hub.docker.com/_/microsoft-dotnet-core/) or the one [for Node.js](https://hub.docker.com/_/node/)).</span></span>

<span data-ttu-id="cb766-167">***Mevcut bir resmi Docker görüntüsünü kullanma***</span><span class="sxs-lookup"><span data-stu-id="cb766-167">***Use an existing official Docker image***</span></span>

<span data-ttu-id="cb766-168">Sürüm numarasına sahip bir dil yığınının resmi deposunu kullanmak, tüm makinelerde (geliştirme, test ve üretim dahil) aynı dil özelliklerinin kullanılabilir olmasını sağlar.</span><span class="sxs-lookup"><span data-stu-id="cb766-168">Using an official repository of a language stack with a version number ensures that the same language features are available on all machines (including development, testing, and production).</span></span>

<span data-ttu-id="cb766-169">Aşağıda .NET Core kapsayıcısı için örnek bir DockerFile verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="cb766-169">The following is a sample DockerFile for a .NET Core container:</span></span>

```Dockerfile
# Base Docker image to use  
FROM mcr.microsoft.com/dotnet/core/aspnet:2.2
  
# Set the Working Directory and files to be copied to the image  
ARG source  
WORKDIR /app  
COPY ${source:-bin/Release/PublishOutput} .  
  
# Configure the listening port to 80 (Internal/Secured port within Docker host)  
EXPOSE 80  
  
# Application entry point  
ENTRYPOINT ["dotnet", "MyCustomMicroservice.dll"]
```

<span data-ttu-id="cb766-170">Bu durumda, görüntü, satıra `FROM mcr.microsoft.com/dotnet/core/aspnet:2.2`göre resmi ASP.NET Core docker görüntüsünün 2,2 sürümünü (Linux ve Windows için çoklu mimari) temel alır.</span><span class="sxs-lookup"><span data-stu-id="cb766-170">In this case, the image is based on version 2.2 of the official ASP.NET Core Docker image (multi-arch for Linux and Windows), as per the line `FROM mcr.microsoft.com/dotnet/core/aspnet:2.2`.</span></span> <span data-ttu-id="cb766-171">(Bu konu hakkında daha fazla bilgi için, [ASP.NET Core Docker görüntü](https://hub.docker.com/_/microsoft-dotnet-core-aspnet/) sayfasına ve [.NET Core Docker görüntü](https://hub.docker.com/_/microsoft-dotnet-core/) sayfasına bakın).</span><span class="sxs-lookup"><span data-stu-id="cb766-171">(For more information about this topic, see the [ASP.NET Core Docker Image](https://hub.docker.com/_/microsoft-dotnet-core-aspnet/) page and the [.NET Core Docker Image](https://hub.docker.com/_/microsoft-dotnet-core/) page).</span></span>

<span data-ttu-id="cb766-172">DockerFile 'da, Docker 'ı çalışma zamanında kullanacağınız (bağlantı noktası 80 gibi) TCP bağlantı noktasını dinlemek için de talimat verebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="cb766-172">In the DockerFile, you can also instruct Docker to listen to the TCP port that you'll use at runtime (such as port 80).</span></span>

<span data-ttu-id="cb766-173">Kullanmakta olduğunuz dile ve çerçeveye bağlı olarak Dockerfile içinde ek yapılandırma ayarları belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="cb766-173">You can specify additional configuration settings in the Dockerfile, depending on the language and framework you're using.</span></span> <span data-ttu-id="cb766-174">Örneğin, `ENTRYPOINT` `["dotnet", "MySingleContainerWebApp.dll"]` çizgi, Docker 'a .NET Core uygulaması çalıştırmasını söyler.</span><span class="sxs-lookup"><span data-stu-id="cb766-174">For instance, the `ENTRYPOINT` line with `["dotnet", "MySingleContainerWebApp.dll"]` tells Docker to run a .NET Core application.</span></span> <span data-ttu-id="cb766-175">.NET uygulamasını derlemek ve çalıştırmak için SDK ve .NET Core CLI (`dotnet CLI`) kullanıyorsanız, bu ayar farklı olur.</span><span class="sxs-lookup"><span data-stu-id="cb766-175">If you're using the SDK and the .NET Core CLI (`dotnet CLI`) to build and run the .NET application, this setting would be different.</span></span> <span data-ttu-id="cb766-176">Buradaki anahtar noktası, GIRIŞ noktası satırı ve diğer ayarların, uygulamanız için seçtiğiniz dile ve platforma bağlı olmasına bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="cb766-176">The key point here is that the ENTRYPOINT line and other settings depend on the language and platform you choose for your application.</span></span>

> <span data-ttu-id="cb766-177">[! BILGI</span><span class="sxs-lookup"><span data-stu-id="cb766-177">[!INFORMATION]</span></span>
>
> <span data-ttu-id="cb766-178">.NET Core uygulamaları için Docker görüntüleri oluşturma hakkında daha fazla bilgi için adresine gidin <https://docs.microsoft.com/dotnet/core/docker/building-net-docker-images>.</span><span class="sxs-lookup"><span data-stu-id="cb766-178">For more information about building Docker images for .NET Core applications, go to <https://docs.microsoft.com/dotnet/core/docker/building-net-docker-images>.</span></span>
>
> <span data-ttu-id="cb766-179">Kendi görüntülerinizi oluşturma hakkında daha fazla bilgi edinmek için adresine gidin <https://docs.docker.com/engine/tutorials/dockerimages/>.</span><span class="sxs-lookup"><span data-stu-id="cb766-179">To learn more about building your own images, go to <https://docs.docker.com/engine/tutorials/dockerimages/>.</span></span>

<span data-ttu-id="cb766-180">**Çoklu mimari görüntü depoları kullanma**</span><span class="sxs-lookup"><span data-stu-id="cb766-180">**Use multi-arch image repositories**</span></span>

<span data-ttu-id="cb766-181">Depodaki tek bir görüntü adı, Linux görüntüsü ve Windows görüntüsü gibi platform türevlerini içerebilir.</span><span class="sxs-lookup"><span data-stu-id="cb766-181">A single image name in a repo can contain platform variants, such as a Linux image and a Windows image.</span></span> <span data-ttu-id="cb766-182">Bu özellik, Microsoft (temel görüntü oluşturucuları) gibi satıcıların birden çok platformu (yani, Linux ve Windows) kapsayacak şekilde tek bir depo oluşturmasını sağlar.</span><span class="sxs-lookup"><span data-stu-id="cb766-182">This feature allows vendors like Microsoft (base image creators) to create a single repo to cover multiple platforms (that is, Linux and Windows).</span></span> <span data-ttu-id="cb766-183">Örneğin, Docker Hub kayıt defterinde bulunan [DotNet/Core/ASPNET](https://hub.docker.com/_/microsoft-dotnet-core-aspnet/) deposu, aynı görüntü adı kullanılarak Linux ve Windows nano Server için destek sağlar.</span><span class="sxs-lookup"><span data-stu-id="cb766-183">For example, the [dotnet/core/aspnet](https://hub.docker.com/_/microsoft-dotnet-core-aspnet/) repository available in the Docker Hub registry provides support for Linux and Windows Nano Server by using the same image name.</span></span>

<span data-ttu-id="cb766-184">Bir Windows ana bilgisayarının [DotNet/Core/ASPNET](https://hub.docker.com/_/microsoft-dotnet-core-aspnet/) görüntüsünü çekmek, Windows türevini çeker, ancak aynı görüntü adının bir Linux ana bilgisayardan çekmesinde Linux varyantı çekilir.</span><span class="sxs-lookup"><span data-stu-id="cb766-184">Pulling the [dotnet/core/aspnet](https://hub.docker.com/_/microsoft-dotnet-core-aspnet/) image from a Windows host pulls the Windows variant, whereas pulling the same image name from a Linux host pulls the Linux variant.</span></span>

<span data-ttu-id="cb766-185">***Sıfırdan taban görüntünüzü oluşturma***</span><span class="sxs-lookup"><span data-stu-id="cb766-185">***Create your base image from scratch***</span></span>

<span data-ttu-id="cb766-186">Docker 'daki bu [makalede](https://docs.docker.com/engine/userguide/eng-image/baseimages/) açıklandığı gibi, kendi Docker temel görüntünüzü sıfırdan oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="cb766-186">You can create your own Docker base image from scratch as explained in this [article](https://docs.docker.com/engine/userguide/eng-image/baseimages/) from Docker.</span></span> <span data-ttu-id="cb766-187">Bu senaryo muhtemelen yalnızca Docker ile başlıyorsanız sizin için en iyi yöntem değildir, ancak kendi temel görüntünüzün belirli bitlerini ayarlamak istiyorsanız bunu yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="cb766-187">This scenario is probably not the best for you if you're just starting with Docker, but if you want to set the specific bits of your own base image, you can do it.</span></span>

### <a name="step-3-create-your-custom-docker-images-embedding-your-service-in-it"></a><span data-ttu-id="cb766-188">3\. Adım: Hizmetinizi buraya gömmeye yönelik özel Docker görüntülerinizi oluşturun</span><span class="sxs-lookup"><span data-stu-id="cb766-188">Step 3: Create your custom Docker images embedding your service in it</span></span>

<span data-ttu-id="cb766-189">Uygulamanızı içeren her bir özel hizmet için ilgili bir görüntü oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="cb766-189">For each custom service that comprises your app, you'll need to create a related image.</span></span> <span data-ttu-id="cb766-190">Uygulamanız tek bir hizmetten veya Web uygulamasından yapılırsa yalnızca tek bir görüntüye ihtiyacınız vardır.</span><span class="sxs-lookup"><span data-stu-id="cb766-190">If your app is made up of a single service or web app, you'll need just a single image.</span></span>

> [!NOTE]
>
> <span data-ttu-id="cb766-191">"Dış döngü DevOps iş akışını" hesaba katdığınızda,, kaynak kodunuzu bir git deposuna (sürekli tümleştirme) gönderdiğinizde görüntüler otomatik bir yapı işlemi tarafından oluşturulur ve bu sayede, görüntüler bu genel ortamda şu şekilde oluşturulur. kaynak kodu.</span><span class="sxs-lookup"><span data-stu-id="cb766-191">When taking into account the "outer-loop DevOps workflow", the images will be created by an automated build process whenever you push your source code to a Git repository (Continuous Integration), so the images will be created in that global environment from your source code.</span></span>
>
> <span data-ttu-id="cb766-192">Ancak, bu dış döngü rotasına gitmeden önce, Docker uygulamasının doğru şekilde çalıştığından emin olunması gerekir, böylece kaynak denetim sistemine (git, vb.) düzgün çalışmayan bir kod göndermezsiniz.</span><span class="sxs-lookup"><span data-stu-id="cb766-192">But before we consider going to that outer-loop route, we need to ensure that the Docker application is actually working properly so that they don't push code that might not work properly to the source control system (Git, etc.).</span></span>
>
> <span data-ttu-id="cb766-193">Bu nedenle, her geliştiricinin ilk olarak yerel olarak test etmesi için tüm iç döngü sürecini yapması ve tam bir özellik göndermek veya kaynak denetim sistemine geçiş yapmak istemeleriyle geliştirmeye devam etmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="cb766-193">Therefore, each developer first needs to do the entire inner-loop process to test locally and continue developing until they want to push a complete feature or change to the source control system.</span></span>

<span data-ttu-id="cb766-194">Yerel ortamınızda bir görüntü oluşturmak ve dockerfile 'ı kullanmak için, Şekil 4-25 ' de gösterildiği gibi Docker Build komutunu kullanabilirsiniz (birkaç kapsayıcı/hizmet tarafından oluşturulan uygulamalar için de `docker-compose up --build` çalıştırabilirsiniz).</span><span class="sxs-lookup"><span data-stu-id="cb766-194">To create an image in your local environment and using the DockerFile, you can use the docker build command, as demonstrated in Figure 4-25 (you also can run `docker-compose up --build` for applications composed by several containers/services).</span></span>

![İndirme ilerlemesini gösteren Docker-Compose derlemesinin konsol çıktısı.](./media/image25.png)

<span data-ttu-id="cb766-196">**Şekil 4-25**.</span><span class="sxs-lookup"><span data-stu-id="cb766-196">**Figure 4-25**.</span></span> <span data-ttu-id="cb766-197">Docker derlemesini çalıştırma</span><span class="sxs-lookup"><span data-stu-id="cb766-197">Running docker build</span></span>

<span data-ttu-id="cb766-198">İsteğe bağlı olarak, proje klasöründen `docker build` doğrudan çalıştırmak yerine, Çalıştır `dotnet publish` komutunu kullanarak gerekli .NET kitaplıkları ile dağıtılabilir bir klasör oluşturabilir ve sonra öğesini çalıştırabilirsiniz `docker build`.</span><span class="sxs-lookup"><span data-stu-id="cb766-198">Optionally, instead of directly running `docker build` from the project folder, you first can generate a deployable folder with the .NET libraries needed by using the run `dotnet publish` command, and then run `docker build`.</span></span>

<span data-ttu-id="cb766-199">Bu örnek, adıyla `cesardl/netcore-webapi-microservice-docker:first` bir Docker görüntüsü oluşturur (`:first` belirli bir sürüm gibi bir etikettir).</span><span class="sxs-lookup"><span data-stu-id="cb766-199">This example creates a Docker image with the name `cesardl/netcore-webapi-microservice-docker:first` (`:first` is a tag, like a specific version).</span></span> <span data-ttu-id="cb766-200">Bu adımı, çeşitli kapsayıcılarla oluşturulmuş Docker uygulamanız için oluşturmanız gereken her özel görüntü için gerçekleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="cb766-200">You can take this step for each custom image you need to create for your composed Docker application with several containers.</span></span>

<span data-ttu-id="cb766-201">Şekil 4-26 ' de gösterildiği gibi, Docker görüntüleri komutunu kullanarak yerel deponuzda (geliştirme makineniz) mevcut görüntüleri bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="cb766-201">You can find the existing images in your local repository (your development machine) by using the docker images command, as illustrated in Figure 4-26.</span></span>

![Mevcut görüntüleri gösteren komut Docker görüntülerinin konsol çıktısı.](./media/image26.png)

<span data-ttu-id="cb766-203">**Şekil 4-26**.</span><span class="sxs-lookup"><span data-stu-id="cb766-203">**Figure 4-26**.</span></span> <span data-ttu-id="cb766-204">Docker görüntülerini kullanarak mevcut görüntüleri görüntüleme</span><span class="sxs-lookup"><span data-stu-id="cb766-204">Viewing existing images using docker images</span></span>

### <a name="step-4-define-your-services-in-docker-composeyml-when-building-a-composed-docker-app-with-multiple-services"></a><span data-ttu-id="cb766-205">4\. Adım: Birden çok hizmet ile oluşturulmuş bir Docker uygulaması oluştururken Docker-Compose. yıml 'de hizmetlerinizi tanımlama</span><span class="sxs-lookup"><span data-stu-id="cb766-205">Step 4: Define your services in docker-compose.yml when building a composed Docker app with multiple services</span></span>

<span data-ttu-id="cb766-206">`docker-compose.yml` Dosyası ile, bir sonraki adım bölümünde açıklanan dağıtım komutlarıyla oluşturulmuş bir uygulama olarak dağıtılacak bir dizi ilgili hizmet tanımlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="cb766-206">With the `docker-compose.yml` file, you can define a set of related services to be deployed as a composed application with the deployment commands explained in the next step section.</span></span>

<span data-ttu-id="cb766-207">Ana veya kök çözüm klasörünüzde bu dosyayı oluşturun; Bu `docker-compose.yml` dosyada gösterilene benzer içeriğe sahip olmalıdır:</span><span class="sxs-lookup"><span data-stu-id="cb766-207">Create that file in your main or root solution folder; it should have content similar to that shown in this `docker-compose.yml` file:</span></span>

```yml
version: '3.4'
services:
  web:
    build: .
    ports:
     - "81:80"
    volumes:
     - .:/code
    depends_on:
     - redis
  redis:
    image: redis
```

<span data-ttu-id="cb766-208">Bu örnekte bu dosya iki hizmeti tanımlar: Web hizmeti (özel hizmetiniz) ve redsıs hizmeti (popüler önbellek hizmeti).</span><span class="sxs-lookup"><span data-stu-id="cb766-208">In this particular case, this file defines two services: the web service (your custom service) and the redis service (a popular cache service).</span></span> <span data-ttu-id="cb766-209">Her hizmet bir kapsayıcı olarak dağıtılır, bu nedenle her biri için somut bir Docker görüntüsü kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="cb766-209">Each service will be deployed as a container, so we need to use a concrete Docker image for each.</span></span> <span data-ttu-id="cb766-210">Bu özel Web hizmeti için, görüntünün aşağıdakileri yapması gerekir:</span><span class="sxs-lookup"><span data-stu-id="cb766-210">For this particular web service, the image will need to do the following:</span></span>

- <span data-ttu-id="cb766-211">Geçerli dizindeki DockerFile dosyasından derleme</span><span class="sxs-lookup"><span data-stu-id="cb766-211">Build from the DockerFile in the current directory</span></span>

- <span data-ttu-id="cb766-212">Kapsayıcıda açığa çıkarılan 80 numaralı bağlantı noktasını ana makinedeki 81 numaralı bağlantı noktasına iletin</span><span class="sxs-lookup"><span data-stu-id="cb766-212">Forward the exposed port 80 on the container to port 81 on the host machine</span></span>

- <span data-ttu-id="cb766-213">Ana bilgisayardaki proje dizinini kapsayıcıda/Code dizinine bağlayın ve görüntüyü yeniden derlemek zorunda kalmadan kodu değiştirmenize olanak sağlar</span><span class="sxs-lookup"><span data-stu-id="cb766-213">Mount the project directory on the host to /code within the container, making it possible for you to modify the code without having to rebuild the image</span></span>

- <span data-ttu-id="cb766-214">Web hizmetini redsıs hizmetine bağlama</span><span class="sxs-lookup"><span data-stu-id="cb766-214">Link the web service to the redis service</span></span>

<span data-ttu-id="cb766-215">Redsıs hizmeti, Docker Hub kayıt defterinden çekilen [en son ortak redo görüntüsünü](https://hub.docker.com/_/redis/) kullanır.</span><span class="sxs-lookup"><span data-stu-id="cb766-215">The redis service uses the [latest public redis image](https://hub.docker.com/_/redis/) pulled from the Docker Hub registry.</span></span> <span data-ttu-id="cb766-216">[redsıs](https://redis.io/) , sunucu tarafı uygulamalar için popüler bir önbellek sistemidir.</span><span class="sxs-lookup"><span data-stu-id="cb766-216">[redis](https://redis.io/) is a popular cache system for server-side applications.</span></span>

### <a name="step-5-build-and-run-your-docker-app"></a><span data-ttu-id="cb766-217">5\. Adım: Docker uygulamanızı derleyin ve çalıştırın</span><span class="sxs-lookup"><span data-stu-id="cb766-217">Step 5: Build and run your Docker app</span></span>

<span data-ttu-id="cb766-218">Uygulamanızda yalnızca tek bir kapsayıcı varsa, bunu yalnızca Docker konağına (VM veya fiziksel sunucu) dağıtarak çalıştırmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="cb766-218">If your app has only a single container, you just need to run it by deploying it to your Docker Host (VM or physical server).</span></span> <span data-ttu-id="cb766-219">Ancak, uygulamanız birden çok hizmetten yapılırsa, *bunu*da oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="cb766-219">However, if your app is made up of multiple services, you need to *compose it*, too.</span></span> <span data-ttu-id="cb766-220">Farklı seçenekleri görelim.</span><span class="sxs-lookup"><span data-stu-id="cb766-220">Let's see the different options.</span></span>

<span data-ttu-id="cb766-221">***Seçenek A: Tek bir kapsayıcı veya hizmet çalıştırma***</span><span class="sxs-lookup"><span data-stu-id="cb766-221">***Option A: Run a single container or service***</span></span>

<span data-ttu-id="cb766-222">Docker görüntüsünü, burada gösterildiği gibi Docker Run komutunu kullanarak çalıştırabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="cb766-222">You can run the Docker image by using the docker run command, as shown here:</span></span>

```console
docker run -t -d -p 80:5000 cesardl/netcore-webapi-microservice-docker:first
```

<span data-ttu-id="cb766-223">Bu dağıtım için 80 numaralı bağlantı noktasına gönderilen istekleri iç bağlantı noktası 5000 ' e yönlentireceğiz.</span><span class="sxs-lookup"><span data-stu-id="cb766-223">For this particular deployment, we'll be redirecting requests sent to port 80 to the internal port 5000.</span></span> <span data-ttu-id="cb766-224">Uygulama artık ana bilgisayar düzeyindeki 80 numaralı dış bağlantı noktasını dinliyor.</span><span class="sxs-lookup"><span data-stu-id="cb766-224">Now the application is listening on the external port 80 at the host level.</span></span>

<span data-ttu-id="cb766-225">***Seçenek B: Çok kapsayıcılı bir uygulama oluşturma ve çalıştırma***</span><span class="sxs-lookup"><span data-stu-id="cb766-225">***Option B: Compose and run a multiple-container application***</span></span>

<span data-ttu-id="cb766-226">Çoğu kurumsal senaryoda, bir Docker uygulaması birden çok hizmetten oluşur.</span><span class="sxs-lookup"><span data-stu-id="cb766-226">In most enterprise scenarios, a Docker application will be composed of multiple services.</span></span> <span data-ttu-id="cb766-227">Bu gibi durumlarda, daha önce oluşturmuş olabileceğiniz `docker-compose up` Docker-Compose. yıml dosyasını kullanacak olan komutunu (Şekil 4-27) çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="cb766-227">For these cases, you can run the `docker-compose up` command (Figure 4-27), which will use the docker-compose.yml file that you might have created previously.</span></span> <span data-ttu-id="cb766-228">Bu komutun çalıştırılması, tüm ilişkili kapsayıcılarıyla oluşturulmuş bir uygulamayı dağıtır.</span><span class="sxs-lookup"><span data-stu-id="cb766-228">Running this command deploys a composed application with all of its related containers.</span></span>

![Docker-Compose up komutuyla konsol çıktısı.](./media/image27.png)

<span data-ttu-id="cb766-230">**Şekil 4-27**.</span><span class="sxs-lookup"><span data-stu-id="cb766-230">**Figure 4-27**.</span></span> <span data-ttu-id="cb766-231">"Docker-Compose up" komutunun çalıştırılmasının sonuçları</span><span class="sxs-lookup"><span data-stu-id="cb766-231">Results of running the "docker-compose up" command</span></span>

<span data-ttu-id="cb766-232">Çalıştırdıktan sonra, uygulamanızı ve ilgili kapsayıcınızı, Şekil 4-28 ' de gösterildiği gibi, sanal makine gösteriminde, Docker ana bilgisayarınıza dağıtırsınız. `docker-compose up`</span><span class="sxs-lookup"><span data-stu-id="cb766-232">After you run `docker-compose up`, you deploy your application and its related container(s) into your Docker Host, as illustrated in Figure 4-28, in the VM representation.</span></span>

![Çok Kapsayıcılı uygulamaları çalıştıran VM.](./media/image28.png)

<span data-ttu-id="cb766-234">**Şekil 4-28**.</span><span class="sxs-lookup"><span data-stu-id="cb766-234">**Figure 4-28**.</span></span> <span data-ttu-id="cb766-235">Docker Kapsayıcıları dağıtılan VM</span><span class="sxs-lookup"><span data-stu-id="cb766-235">VM with Docker containers deployed</span></span>

### <a name="step-6-test-your-docker-application-locally-in-your-local-cd-vm"></a><span data-ttu-id="cb766-236">6\. Adım: Docker uygulamanızı test edin (yerel CD sanal makinenizde yerel olarak)</span><span class="sxs-lookup"><span data-stu-id="cb766-236">Step 6: Test your Docker application (locally, in your local CD VM)</span></span>

<span data-ttu-id="cb766-237">Bu adım, uygulamanızın yaptığına bağlı olarak farklılık gösterir.</span><span class="sxs-lookup"><span data-stu-id="cb766-237">This step will vary depending on what your app is doing.</span></span>

<span data-ttu-id="cb766-238">Tek bir kapsayıcı veya hizmet olarak dağıtılan basit bir .NET Core Web API 'SI "Merhaba Dünya", yalnızca DockerFile içinde belirtilen TCP bağlantı noktasını sağlayarak hizmete erişmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="cb766-238">In a simple .NET Core Web API "Hello World" deployed as a single container or service, you'd just need to access the service by providing the TCP port specified in the DockerFile.</span></span>

<span data-ttu-id="cb766-239">Localhost açık değilse, hizmetinize gitmek için şu komutu kullanarak makinenin IP adresini bulun:</span><span class="sxs-lookup"><span data-stu-id="cb766-239">If localhost is not turned on, to navigate to your service, find the IP address for the machine by using this command:</span></span>

```console
docker-machine {IP} {YOUR-CONTAINER-NAME}
```

<span data-ttu-id="cb766-240">Docker konağında bir tarayıcı açın ve bu siteye gidin; Şekil 4-29 ' de gösterildiği gibi, uygulamanızı/hizmetinizi çalışır durumda görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="cb766-240">On the Docker host, open a browser and navigate to that site; you should see your app/service running, as demonstrated in Figure 4-29.</span></span>

![Localhost/API/değerlerden alınan yanıtın tarayıcı görünümü.](./media/image29.png)

<span data-ttu-id="cb766-242">**Şekil 4-29**.</span><span class="sxs-lookup"><span data-stu-id="cb766-242">**Figure 4-29**.</span></span> <span data-ttu-id="cb766-243">Localhost kullanarak Docker uygulamanızı yerel olarak test etme</span><span class="sxs-lookup"><span data-stu-id="cb766-243">Testing your Docker application locally using localhost</span></span>

<span data-ttu-id="cb766-244">80 numaralı bağlantı noktasını kullandığını unutmayın, ancak daha önce açıklandığı gibi, ile birlikte `docker run`dağıtılmakta olduğu gibi, dahili olarak bu bağlantı noktası 5000 ' e yönlendirilmekte.</span><span class="sxs-lookup"><span data-stu-id="cb766-244">Note that it's using port 80, but internally it's being redirected to port 5000, because that's how it was deployed with `docker run`, as explained earlier.</span></span>

<span data-ttu-id="cb766-245">Bunu terminalden KıVRıMLı kullanarak test edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="cb766-245">You can test this by using CURL from the terminal.</span></span> <span data-ttu-id="cb766-246">Windows 'daki bir Docker yüklemesinde, Şekil 4-30 ' de gösterildiği gibi varsayılan IP 10.0.75.1 ' dir.</span><span class="sxs-lookup"><span data-stu-id="cb766-246">In a Docker installation on Windows, the default IP is 10.0.75.1, as depicted in Figure 4-30.</span></span>

![Konsol çıkışı, http://10.0.75.1/API/values kıvrımlı ile elde](./media/image30.png)

<span data-ttu-id="cb766-248">**Şekil 4-30**.</span><span class="sxs-lookup"><span data-stu-id="cb766-248">**Figure 4-30**.</span></span> <span data-ttu-id="cb766-249">KıVRıMLı kullanarak Docker uygulamasını yerel olarak test etme</span><span class="sxs-lookup"><span data-stu-id="cb766-249">Testing a Docker application locally by using CURL</span></span>

<span data-ttu-id="cb766-250">**Docker üzerinde çalışan bir kapsayıcıda hata ayıklama**</span><span class="sxs-lookup"><span data-stu-id="cb766-250">**Debugging a container running on Docker**</span></span>

<span data-ttu-id="cb766-251">, Node. js ve .NET Core kapsayıcıları gibi diğer platformları kullanıyorsanız Docker hata ayıklamayı destekler Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="cb766-251">Visual Studio Code supports debugging Docker if you're using Node.js and other platforms like .NET Core containers.</span></span>

<span data-ttu-id="cb766-252">Ayrıca, sonraki bölümde açıklandığı gibi Windows veya Mac için Visual Studio 'Yu kullanırken Docker 'daki .NET Core veya .NET Framework kapsayıcılarında hata ayıklaması yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="cb766-252">You also can debug .NET Core or .NET Framework containers in Docker when using Visual Studio for Windows or Mac, as described in the next section.</span></span>

> <span data-ttu-id="cb766-253">[! BILGI</span><span class="sxs-lookup"><span data-stu-id="cb766-253">[!INFORMATION]</span></span>
>
> <span data-ttu-id="cb766-254">Node. js Docker kapsayıcılarının hatalarını ayıklama hakkında daha fazla bilgi edinmek <https://blog.docker.com/2016/07/live-debugging-docker/> için <https://blogs.msdn.microsoft.com/user_ed/2016/02/27/visual-studio-code-new-features-13-big-debugging-updates-rich-object-hover-conditional-breakpoints-node-js-mono-more/>ve ' a gidin.</span><span class="sxs-lookup"><span data-stu-id="cb766-254">To learn more about debugging Node.js Docker containers, go to <https://blog.docker.com/2016/07/live-debugging-docker/> and <https://blogs.msdn.microsoft.com/user_ed/2016/02/27/visual-studio-code-new-features-13-big-debugging-updates-rich-object-hover-conditional-breakpoints-node-js-mono-more/>.</span></span>

>[!div class="step-by-step"]
><span data-ttu-id="cb766-255">[Önceki](docker-apps-development-environment.md)İleri
>[](visual-studio-tools-for-docker.md)</span><span class="sxs-lookup"><span data-stu-id="cb766-255">[Previous](docker-apps-development-environment.md)
[Next](visual-studio-tools-for-docker.md)</span></span>