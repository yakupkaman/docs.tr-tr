---
title: TensorFlow ile bir ML.NET özel görüntü sınıflandırıcı oluşturma
description: Önceden eğitilmiş bir TensorFlow modeli yeniden kullanarak görüntüleri sınıflandırmak için senaryo bir TensorFlow aktarımlı ML.NET özel görüntü sınıflandırıcıda oluşturma keşfedin.
ms.date: 04/05/2019
ms.topic: tutorial
ms.custom: mvc
ms.openlocfilehash: 7d320135d0d414c2cca934ff3d4cad5152a24ee8
ms.sourcegitcommit: 5b6d778ebb269ee6684fb57ad69a8c28b06235b9
ms.translationtype: HT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/08/2019
ms.locfileid: "59232531"
---
# <a name="tutorial-build-an-mlnet-custom-image-classifier-with-tensorflow"></a><span data-ttu-id="7ecc1-103">Öğretici: TensorFlow ile bir ML.NET özel görüntü sınıflandırıcı oluşturma</span><span class="sxs-lookup"><span data-stu-id="7ecc1-103">Tutorial: Build an ML.NET custom image classifier with TensorFlow</span></span>

<span data-ttu-id="7ecc1-104">Bu örnek öğretici, önceden eğitilen bir görüntü sınıflandırıcı nasıl kullanabileceğinizi gösteren `TensorFlow` görüntüleri birkaç kategoride sınıflandırmak için yeni özel modeli oluşturmak için model.</span><span class="sxs-lookup"><span data-stu-id="7ecc1-104">This sample tutorial illustrates how you can use an already trained Image Classifier `TensorFlow` model to build a new custom model to classify images into a few categories.</span></span>

<span data-ttu-id="7ecc1-105">Ne öncesi zaten bir model kullanabilirsiniz ya da tümünün veya bazılarının, sorununuzu çözmenize yardımcı olmak için bu modelinin katmanlarını yeniden eğitme ve benzer bir sorunu çözmek eğitilen?</span><span class="sxs-lookup"><span data-stu-id="7ecc1-105">What if you could reuse a model that's already been pre trained to solve a similar problem and retrain either all or some of the layers of that model to make it solve your problem?</span></span> <span data-ttu-id="7ecc1-106">Bu teknik yeniden yeni bir model oluşturmak üzere önceden eğitilen bir modelin parçası olarak da bilinen [aktarım öğrenme](https://en.wikipedia.org/wiki/Transfer_learning).</span><span class="sxs-lookup"><span data-stu-id="7ecc1-106">This technique of reusing part of an already trained model to build a new model is known as [transfer learning](https://en.wikipedia.org/wiki/Transfer_learning).</span></span>

<span data-ttu-id="7ecc1-107">Eğitim bir [görüntü sınıflandırması](https://en.wikipedia.org/wiki/Outline_of_object_recognition) sıfırdan modeli, Parametreler, bir sürü etiketli eğitim verilerini ve işlem kaynakları (GPU saat yüzlerce) çok büyük miktarda milyonlarca ayarlama gerektirir.</span><span class="sxs-lookup"><span data-stu-id="7ecc1-107">Training an [Image Classification](https://en.wikipedia.org/wiki/Outline_of_object_recognition) model from scratch requires setting millions of parameters, a ton of labeled training data and a vast amount of compute resources (hundreds of GPU hours).</span></span> <span data-ttu-id="7ecc1-108">Aktarımlı öğrenme kadar etkili olarak sıfırdan özel bir model eğitim olsa da görüntüleri etiketlenmiş resimlerinizi milyonlarca karşılaştırması binlerce birlikte çalışarak bu işlem için kısayol sağlar ve oldukça hızlı bir şekilde özelleştirilmiş model derleme (bir makinede bir saat içinde bir GPU).</span><span class="sxs-lookup"><span data-stu-id="7ecc1-108">While not as effective as training a custom model from scratch, transfer learning allows you to shortcut this process by working with thousands of images vs. millions of labeled images and build a customized model fairly quickly (within an hour on a machine without a GPU).</span></span>

<span data-ttu-id="7ecc1-109">Bu öğreticide şunların nasıl yapıladığını öğreneceksiniz:</span><span class="sxs-lookup"><span data-stu-id="7ecc1-109">In this tutorial, you learn how to:</span></span>
> [!div class="checklist"]
> * <span data-ttu-id="7ecc1-110">Sorunu anlama</span><span class="sxs-lookup"><span data-stu-id="7ecc1-110">Understand the problem</span></span>
> * <span data-ttu-id="7ecc1-111">Yeniden kullanmak ve önceden eğitilmiş bir modeli ayarlama</span><span class="sxs-lookup"><span data-stu-id="7ecc1-111">Reuse and tune the pre-trained model</span></span>
> * <span data-ttu-id="7ecc1-112">Resimleri sınıflandırma</span><span class="sxs-lookup"><span data-stu-id="7ecc1-112">Classify Images</span></span>

> [!NOTE]
> <span data-ttu-id="7ecc1-113">Bu konu şu anda Önizleme aşamasında olan ML.NET ifade eder ve malzeme değişiklik gösterebilir.</span><span class="sxs-lookup"><span data-stu-id="7ecc1-113">This topic refers to ML.NET, which is currently in Preview, and material may be subject to change.</span></span> <span data-ttu-id="7ecc1-114">Daha fazla bilgi için ziyaret [ML.NET giriş](https://www.microsoft.com/net/learn/apps/machine-learning-and-ai/ml-dotnet).</span><span class="sxs-lookup"><span data-stu-id="7ecc1-114">For more information, visit [the ML.NET introduction](https://www.microsoft.com/net/learn/apps/machine-learning-and-ai/ml-dotnet).</span></span>

<span data-ttu-id="7ecc1-115">Bu öğretici ve ilgili örnek şu anda kullandığınız **ML.NET sürüm 0.10**.</span><span class="sxs-lookup"><span data-stu-id="7ecc1-115">This tutorial and related sample are currently using **ML.NET version 0.10**.</span></span> <span data-ttu-id="7ecc1-116">Daha fazla bilgi için bkz: adresindeki sürüm notlarını [dotnet/machinelearning GitHub deposu](https://github.com/dotnet/machinelearning/tree/master/docs/release-notes)</span><span class="sxs-lookup"><span data-stu-id="7ecc1-116">For more information, see the release notes at the [dotnet/machinelearning GitHub repo](https://github.com/dotnet/machinelearning/tree/master/docs/release-notes)</span></span>

## <a name="image-classification-sample-overview"></a><span data-ttu-id="7ecc1-117">Görüntü sınıflandırma örneğine genel bakış</span><span class="sxs-lookup"><span data-stu-id="7ecc1-117">Image classification sample overview</span></span>

<span data-ttu-id="7ecc1-118">Örnek görüntüleri küçük bir eğitim veri miktarı ile sınıflandırmak için önceden eğitilmiş bir modeli yeniden kullanarak bir görüntü sınıflandırıcı oluşturma için ML.NET kullanan bir konsol uygulamasıdır.</span><span class="sxs-lookup"><span data-stu-id="7ecc1-118">The sample is a console application that uses ML.NET to build an image classifier by reusing a pre-trained model to classify images with a small amount of training data.</span></span>

<span data-ttu-id="7ecc1-119">Bu öğreticide kaynak kodunu bulabilirsiniz [dotnet/samples](https://github.com/dotnet/samples/tree/master/machine-learning/tutorials/TransferLearningTF) depo.</span><span class="sxs-lookup"><span data-stu-id="7ecc1-119">You can find the source code for this tutorial at the [dotnet/samples](https://github.com/dotnet/samples/tree/master/machine-learning/tutorials/TransferLearningTF) repository.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7ecc1-120">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="7ecc1-120">Prerequisites</span></span>

* <span data-ttu-id="7ecc1-121">[Visual Studio 2017 15.6 veya üzeri](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017) yüklü ".NET Core çoklu platform geliştirme" iş yüküyle birlikte sağlanır.</span><span class="sxs-lookup"><span data-stu-id="7ecc1-121">[Visual Studio 2017 15.6 or later](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017) with the ".NET Core cross-platform development" workload installed.</span></span>

* <span data-ttu-id="7ecc1-122">Microsoft.ML 0.10.0 Nuget paketi</span><span class="sxs-lookup"><span data-stu-id="7ecc1-122">Microsoft.ML 0.10.0 Nuget package</span></span>
* <span data-ttu-id="7ecc1-123">Microsoft.ML.ImageAnalytics 0.10.0 Nuget paketi</span><span class="sxs-lookup"><span data-stu-id="7ecc1-123">Microsoft.ML.ImageAnalytics 0.10.0 Nuget package</span></span>
* <span data-ttu-id="7ecc1-124">Microsoft.ML.TensorFlow 0.10.0 Nuget paketi</span><span class="sxs-lookup"><span data-stu-id="7ecc1-124">Microsoft.ML.TensorFlow 0.10.0 Nuget package</span></span>

* [<span data-ttu-id="7ecc1-125">Öğretici varlıklar dizin. ZIP dosyası</span><span class="sxs-lookup"><span data-stu-id="7ecc1-125">The tutorial assets directory .ZIP file</span></span>](http://download.microsoft.com/download/0/E/5/0E5E0136-21CE-4C66-AC18-9917DED8A4AD/image-classifier-assets.zip)

* [<span data-ttu-id="7ecc1-126">InceptionV3 machine learning modeli</span><span class="sxs-lookup"><span data-stu-id="7ecc1-126">The InceptionV3 machine learning model</span></span>](https://storage.googleapis.com/download.tensorflow.org/models/inception5h.zip)

## <a name="select-the-appropriate-machine-learning-task"></a><span data-ttu-id="7ecc1-127">Uygun makine öğrenimi görevini seçin</span><span class="sxs-lookup"><span data-stu-id="7ecc1-127">Select the appropriate machine learning task</span></span>

<span data-ttu-id="7ecc1-128">[Derin öğrenme](https://en.wikipedia.org/wiki/Deep_learning) , görüntü işleme ve konuşma tanıma gibi alanları revolutionizing Machine Learning, bir alt kümesidir.</span><span class="sxs-lookup"><span data-stu-id="7ecc1-128">[Deep learning](https://en.wikipedia.org/wiki/Deep_learning) is a subset of Machine Learning, which is revolutionizing areas like Computer Vision and Speech Recognition.</span></span>

<span data-ttu-id="7ecc1-129">Modelleri, büyük kümelerini kullanarak eğitilir derin öğrenme [veri etiketli](https://en.wikipedia.org/wiki/Labeled_data) ve [sinir ağları](https://en.wikipedia.org/wiki/Artificial_neural_network) birden çok öğrenim katmanlarını içerir.</span><span class="sxs-lookup"><span data-stu-id="7ecc1-129">Deep learning models are trained by using large sets of [labeled data](https://en.wikipedia.org/wiki/Labeled_data) and [neural networks](https://en.wikipedia.org/wiki/Artificial_neural_network) that contain multiple learning layers.</span></span> <span data-ttu-id="7ecc1-130">Derin öğrenme:</span><span class="sxs-lookup"><span data-stu-id="7ecc1-130">Deep learning:</span></span>

* <span data-ttu-id="7ecc1-131">Görüntü işleme gibi bazı görevler üzerinde daha iyi gerçekleştirir.</span><span class="sxs-lookup"><span data-stu-id="7ecc1-131">Performs better on some tasks like Computer Vision.</span></span>

* <span data-ttu-id="7ecc1-132">İyi büyük verileri tutarlarını gerçekleştirir.</span><span class="sxs-lookup"><span data-stu-id="7ecc1-132">Performs well on huge data amounts.</span></span>

<span data-ttu-id="7ecc1-133">Görüntü sınıflandırması otomatik olarak gibi birden fazla kategoriye görüntüleri sınıflandırmak olanak sağlayan ortak bir Machine Learning görevidir:</span><span class="sxs-lookup"><span data-stu-id="7ecc1-133">Image Classification is a common Machine Learning task that allows us to automatically classify images into multiple categories such as:</span></span>

* <span data-ttu-id="7ecc1-134">İnsan yüz veya bir görüntüde algılanıyor.</span><span class="sxs-lookup"><span data-stu-id="7ecc1-134">Detecting a human face in an image or not.</span></span>
* <span data-ttu-id="7ecc1-135">Köpek Kedilere algılanıyor.</span><span class="sxs-lookup"><span data-stu-id="7ecc1-135">Detecting Cats vs. dogs.</span></span>

 <span data-ttu-id="7ecc1-136">Veya belirlenmesinde aşağıdaki resimlerde gösterildiği gibi bir görüntü bir yiyecek, çocuğunun veya Gereci:</span><span class="sxs-lookup"><span data-stu-id="7ecc1-136">Or as in the following images determining if an image is a(n)  food, toy, or appliance:</span></span>

![<span data-ttu-id="7ecc1-137">pizza görüntü](./media/image-classification/220px-Pepperoni_pizza.jpg)
![Oyuncak Ayı ayı görüntü](./media/image-classification/119px-Nalle_-_a_small_brown_teddy_bear.jpg)
![toaster görüntüsü</span><span class="sxs-lookup"><span data-stu-id="7ecc1-137">pizza image](./media/image-classification/220px-Pepperoni_pizza.jpg)
![teddy bear image](./media/image-classification/119px-Nalle_-_a_small_brown_teddy_bear.jpg)
![toaster image</span></span>](./media/image-classification/193px-Broodrooster.jpg)

>[!Note]
> <span data-ttu-id="7ecc1-138">Önceki görüntüler için Wikimedia Commons ait ve şu şekilde atanmıştır:</span><span class="sxs-lookup"><span data-stu-id="7ecc1-138">The preceding images belong to Wikimedia Commons and are attributed as follows:</span></span>
>
> * <span data-ttu-id="7ecc1-139">"220px-Pepperoni_pizza.jpg" Public Domain, https://commons.wikimedia.org/w/index.php?curid=79505,</span><span class="sxs-lookup"><span data-stu-id="7ecc1-139">"220px-Pepperoni_pizza.jpg" Public Domain, https://commons.wikimedia.org/w/index.php?curid=79505,</span></span>
> * <span data-ttu-id="7ecc1-140">"119px-Nalle_-_a_small_brown_teddy_bear.jpg" tarafından [Jonik](https://commons.wikimedia.org/wiki/User:Jonik) -, CC BY-SA 2.0, kendi kendine fotoğrafı https://commons.wikimedia.org/w/index.php?curid=48166.</span><span class="sxs-lookup"><span data-stu-id="7ecc1-140">"119px-Nalle_-_a_small_brown_teddy_bear.jpg" By [Jonik](https://commons.wikimedia.org/wiki/User:Jonik) - Self-photographed, CC BY-SA 2.0, https://commons.wikimedia.org/w/index.php?curid=48166.</span></span>
> * <span data-ttu-id="7ecc1-141">"193px-Broodrooster.jpg" tarafından [M.Minderhoud](https://nl.wikipedia.org/wiki/Gebruiker:Michiel1972) -kendi iş, CC BY SA 3.0 https://commons.wikimedia.org/w/index.php?curid=27403</span><span class="sxs-lookup"><span data-stu-id="7ecc1-141">"193px-Broodrooster.jpg" By [M.Minderhoud](https://nl.wikipedia.org/wiki/Gebruiker:Michiel1972) - Own work, CC BY-SA 3.0, https://commons.wikimedia.org/w/index.php?curid=27403</span></span>

<span data-ttu-id="7ecc1-142">Aktarımlı öğrenme içeren birkaç stratejileri gibi *tüm katmanlar yeniden eğitme* ve *sondan katman*.</span><span class="sxs-lookup"><span data-stu-id="7ecc1-142">Transfer learning includes a few strategies, such as *retrain all layers* and *penultimate layer*.</span></span> <span data-ttu-id="7ecc1-143">Bu öğreticide açıklamak ve nasıl kullanabileceğinizi gösteren *sondan katman stratejisi*.</span><span class="sxs-lookup"><span data-stu-id="7ecc1-143">This tutorial will explain and show how to use the *penultimate layer strategy*.</span></span> <span data-ttu-id="7ecc1-144">*Sondan katman stratejisi* zaten belirli bir sorunu çözmek için önceden eğitildi bir model kullanır.</span><span class="sxs-lookup"><span data-stu-id="7ecc1-144">The *penultimate layer strategy* reuses a model that's already been pre-trained to solve a specific problem.</span></span> <span data-ttu-id="7ecc1-145">Strateji, ardından yeni bir sorunu çözmeye sağlamak için bu modelin son katmanı retrains.</span><span class="sxs-lookup"><span data-stu-id="7ecc1-145">The strategy then retrains the final layer of that model to make it solve a new problem.</span></span> <span data-ttu-id="7ecc1-146">Önceden eğitilmiş modelin yeni modelinizin bir parçası olarak yeniden önemli zamandan ve kaynaklardan tasarruf.</span><span class="sxs-lookup"><span data-stu-id="7ecc1-146">Reusing the pre-trained model as part of your new model will save significant time and resources.</span></span>

<span data-ttu-id="7ecc1-147">Görüntü sınıflandırma modelinizi yeniden [başlangıcı modeli](https://storage.googleapis.com/download.tensorflow.org/models/inception5h.zip), üzerinde bir popüler görüntü tanıma modeli eğitilir `ImageNet` TensorFlow modeli nerede çalışırsa tüm sınıflandırmak için veri kümesi, binlerce sınıflara gibi görüntüleri " Genel","Jersey"ve"Dishwasher".</span><span class="sxs-lookup"><span data-stu-id="7ecc1-147">Your image classification model reuses the [Inception model](https://storage.googleapis.com/download.tensorflow.org/models/inception5h.zip), a popular image recognition model trained on the `ImageNet` dataset where the TensorFlow model tries to classify entire images into a thousand classes, like “Umbrella”, “Jersey”, and “Dishwasher”.</span></span>

<span data-ttu-id="7ecc1-148">`Inception v3 model` Olarak sınıflandırılan bir [derin konvolüsyonel sinir ağını](https://en.wikipedia.org/wiki/Convolutional_neural_network) ve eşleşen veya bazı etki alanlarına İnsan performansa aşan sabit visual tanıma görevleri, makul performans elde edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7ecc1-148">The `Inception v3 model` can be classified as a [deep convolutional neural network](https://en.wikipedia.org/wiki/Convolutional_neural_network) and can achieve reasonable performance on hard visual recognition tasks, matching or exceeding human performance in some domains.</span></span> <span data-ttu-id="7ecc1-149">Model/algoritması birden çok Araştırmacıları tarafından geliştirilmiş ve özgün kağıda tabanlı: ["Yeni mimarisi için görüntü işleme tarafından Szegedy yeniden değerlendirme", et. Al.](https://arxiv.org/abs/1512.00567)</span><span class="sxs-lookup"><span data-stu-id="7ecc1-149">The model/algorithm was developed by multiple researchers and based on the original paper: ["Rethinking the Inception Architecture for Computer Vision” by Szegedy, et. al.](https://arxiv.org/abs/1512.00567)</span></span>

<span data-ttu-id="7ecc1-150">Çünkü `Inception model` öncesi zaten içerdiği farklı görüntüleri binlerce üzerinde geliştirilen, [görüntü özellikleri](https://en.wikipedia.org/wiki/Feature_(computer_vision)) resim tanımlama için gerekli.</span><span class="sxs-lookup"><span data-stu-id="7ecc1-150">Because the `Inception model` has already been pre trained on thousands of different images, it contains the [image features](https://en.wikipedia.org/wiki/Feature_(computer_vision)) needed for image identification.</span></span> <span data-ttu-id="7ecc1-151">Basit özellikleri (örneğin, kenarlar) alt görüntü özelliği katmanlarının tanır ve daha yüksek katmanları (şekiller gibi) daha karmaşık özelliklerden tanı.</span><span class="sxs-lookup"><span data-stu-id="7ecc1-151">The lower image feature layers recognize simple features (such as edges) and the higher layers recognize more complex features (such as shapes).</span></span> <span data-ttu-id="7ecc1-152">Son katmanı, zaten nasıl sınıflandırılacağıyla görüntüleri anlayan önceden eğitilen bir modelin ile başlatıyorsanız çünkü çok daha küçük veri kümesi karşı çalıştırılır.</span><span class="sxs-lookup"><span data-stu-id="7ecc1-152">The final layer is trained against a much smaller set of data because you're starting with a pre trained model that already understands how to classify images.</span></span> <span data-ttu-id="7ecc1-153">Modelinizi ikiden fazla kategorileri sınıflandırmak verdiğinden, bu örneği yer almaktadır. bir [çok sınıflı sınıflandırıcı](../resources/tasks.md#multiclass-classification).</span><span class="sxs-lookup"><span data-stu-id="7ecc1-153">As your model allows you to classify more than two categories, this is an example of a [multi-class classifier](../resources/tasks.md#multiclass-classification).</span></span> 

`TensorFlow` <span data-ttu-id="7ecc1-154">popüler derin öğrenme ve eğitim derin sinir ağı (ve genel sayısal hesaplamalar) etkinleştirir ve halinde uygulanır makine öğrenimi araç seti bir `transformer` ML.NET içinde.</span><span class="sxs-lookup"><span data-stu-id="7ecc1-154">is a popular deep learning and machine learning toolkit that enables training deep neural networks (and general numeric computations), and is implemented as a `transformer` in ML.NET.</span></span> <span data-ttu-id="7ecc1-155">Bu öğretici için yeniden kullanıldığı `Inception model`.</span><span class="sxs-lookup"><span data-stu-id="7ecc1-155">For this tutorial, it's used to reuse the `Inception model`.</span></span>

<span data-ttu-id="7ecc1-156">Aşağıdaki diyagramda gösterildiği gibi .NET Core veya .NET Framework uygulamalarınızı ML.NET NuGet paketlerini bir başvuru ekleyin.</span><span class="sxs-lookup"><span data-stu-id="7ecc1-156">As shown in the following diagram, you add a reference to the ML.NET NuGet packages in your .NET Core or .NET Framework applications.</span></span> <span data-ttu-id="7ecc1-157">ML.NET kapsar altında içerir ve yerel başvuruyor `TensorFlow` yükler mevcut bir kod yazmanızı sağlayan kitaplığı eğitilmiş `TensorFlow` Puanlama için model dosyası.</span><span class="sxs-lookup"><span data-stu-id="7ecc1-157">Under the covers, ML.NET includes and references the native `TensorFlow` library that allows you to write code that loads an existing trained `TensorFlow` model file for scoring.</span></span>  

![TensorFlow dönüştürme ML.NET mimarisi diyagramı](./media/image-classification/tensorflow-mlnet.png)

<span data-ttu-id="7ecc1-159">`Inception model` Binlerce kategoriler halinde görüntüleri sınıflandırmak için eğitilen ancak daha küçük bir kategori kümesini ve bu kategorilerin görüntülerde sınıflandırmak gerekir.</span><span class="sxs-lookup"><span data-stu-id="7ecc1-159">The `Inception model` is trained to classify images into a thousand categories, but you need to classify images in a smaller category set, and only those categories.</span></span> <span data-ttu-id="7ecc1-160">Girin `transfer` parçası `transfer learning`.</span><span class="sxs-lookup"><span data-stu-id="7ecc1-160">Enter the `transfer` part of `transfer learning`.</span></span> <span data-ttu-id="7ecc1-161">Aktarabilirsiniz `Inception model`'s tanıması ve özel görüntü sınıflandırıcınızı yeni sınırlı kategorilerini görüntülere sınıflandırma özelliği.</span><span class="sxs-lookup"><span data-stu-id="7ecc1-161">You can transfer the `Inception model`'s ability to recognize and classify images to the new limited categories of your custom image classifier.</span></span>  

 <span data-ttu-id="7ecc1-162">Son üç kategorileri kümesi kullanarak bu modeli katmanı yeniden eğitme oluşturacağız:</span><span class="sxs-lookup"><span data-stu-id="7ecc1-162">You're going to retrain the final layer of that model using a set of three categories:</span></span>

* <span data-ttu-id="7ecc1-163">Yiyecek</span><span class="sxs-lookup"><span data-stu-id="7ecc1-163">Food</span></span>
* <span data-ttu-id="7ecc1-164">Çocuğunun</span><span class="sxs-lookup"><span data-stu-id="7ecc1-164">Toy</span></span>
* <span data-ttu-id="7ecc1-165">Gereç</span><span class="sxs-lookup"><span data-stu-id="7ecc1-165">Appliance</span></span>

<span data-ttu-id="7ecc1-166">Katman kullanan bir [ÇOKTERİMLİ Lojistik regresyon algoritması](https://en.wikipedia.org/wiki/Multinomial_logistic_regression) kategoriyi mümkün olan en kısa sürede bulunacak.</span><span class="sxs-lookup"><span data-stu-id="7ecc1-166">Your layer uses a [multinomial logistic regression algorithm](https://en.wikipedia.org/wiki/Multinomial_logistic_regression) to find the correct category as quickly as possible.</span></span> <span data-ttu-id="7ecc1-167">Bu algoritma, yanıt bir değer ölçeklendirerek kategoriyi ve diğerleri için sıfır değeri belirlemek için olasılıkları kullanma sınıflandırır.</span><span class="sxs-lookup"><span data-stu-id="7ecc1-167">This algorithm classifies using probabilities to determine the answer, giving a one value to the correct category and a zero value to the others.</span></span>  

### <a name="dataset"></a><span data-ttu-id="7ecc1-168">DataSet</span><span class="sxs-lookup"><span data-stu-id="7ecc1-168">DataSet</span></span>

<span data-ttu-id="7ecc1-169">İki veri kaynağı vardır: `.tsv` dosyası ve görüntü dosyaları.</span><span class="sxs-lookup"><span data-stu-id="7ecc1-169">There are two data sources: the `.tsv` file, and the image files.</span></span>  <span data-ttu-id="7ecc1-170">`tags.tsv` Dosyada iki sütun: ilk olarak tanımlanan `ImagePath` ve ikincisi `Label` görüntüsüne karşılık gelen.</span><span class="sxs-lookup"><span data-stu-id="7ecc1-170">The `tags.tsv` file contains two columns: the first one is defined as `ImagePath` and the second one is the `Label` corresponding to the image.</span></span> <span data-ttu-id="7ecc1-171">Aşağıdaki örnek dosyası, bir başlık satırı yok ve şöyle görünür:</span><span class="sxs-lookup"><span data-stu-id="7ecc1-171">The following example file doesn't have a header row, and looks like this:</span></span>

```tsv
broccoli.jpg    food
pizza.jpg   food
pizza2.jpg  food
teddy2.jpg  toy
teddy3.jpg  toy
teddy4.jpg  toy
toaster.jpg appliance
toaster2.png    appliance
```

<span data-ttu-id="7ecc1-172">Eğitim ve test görüntüleri bir ZIP dosyası indireceksiniz varlıklar klasörlerinde yer alır.</span><span class="sxs-lookup"><span data-stu-id="7ecc1-172">The training and testing images are located in the assets folders that you'll download in a zip file.</span></span> <span data-ttu-id="7ecc1-173">Bu görüntüler için Wikimedia Commons ait.</span><span class="sxs-lookup"><span data-stu-id="7ecc1-173">These images belong to Wikimedia Commons.</span></span>
> *<span data-ttu-id="7ecc1-174">[Wikimedia Commons](https://commons.wikimedia.org/w/index.php?title=Main_Page&oldid=313158208), serbest medya depo.</span><span class="sxs-lookup"><span data-stu-id="7ecc1-174">[Wikimedia Commons](https://commons.wikimedia.org/w/index.php?title=Main_Page&oldid=313158208), the free media repository.</span></span>* <span data-ttu-id="7ecc1-175">Alınan 10:48, 17 Ekim 2018 tarihinden sonra:</span><span class="sxs-lookup"><span data-stu-id="7ecc1-175">Retrieved 10:48, October 17, 2018 from:</span></span>  
> https://commons.wikimedia.org/wiki/Pizza  
> https://commons.wikimedia.org/wiki/Toaster  
> https://commons.wikimedia.org/wiki/Teddy_bear  

## <a name="create-a-console-application"></a><span data-ttu-id="7ecc1-176">Konsol uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="7ecc1-176">Create a console application</span></span>

### <a name="create-a-project"></a><span data-ttu-id="7ecc1-177">Proje oluşturma</span><span class="sxs-lookup"><span data-stu-id="7ecc1-177">Create a project</span></span>

1. <span data-ttu-id="7ecc1-178">Visual Studio 2017'yi açın.</span><span class="sxs-lookup"><span data-stu-id="7ecc1-178">Open Visual Studio 2017.</span></span> <span data-ttu-id="7ecc1-179">Seçin **dosya** > **yeni** > **proje** menü çubuğundan.</span><span class="sxs-lookup"><span data-stu-id="7ecc1-179">Select **File** > **New** > **Project** from the menu bar.</span></span> <span data-ttu-id="7ecc1-180">İçinde **yeni proje** iletişim kutusunda **Visual C#** düğümünü ve ardından **.NET Core** düğümü.</span><span class="sxs-lookup"><span data-stu-id="7ecc1-180">In the **New Project** dialog, select the **Visual C#** node followed by the **.NET Core** node.</span></span> <span data-ttu-id="7ecc1-181">Ardından **konsol uygulaması (.NET Core)** proje şablonu.</span><span class="sxs-lookup"><span data-stu-id="7ecc1-181">Then select the **Console App (.NET Core)** project template.</span></span> <span data-ttu-id="7ecc1-182">İçinde **adı** metin kutusuna "TransferLearningTF" yazın ve ardından **Tamam** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="7ecc1-182">In the **Name** text box, type "TransferLearningTF" and then select the **OK** button.</span></span>

2. <span data-ttu-id="7ecc1-183">Yükleme **Microsoft.ML NuGet paketini**:</span><span class="sxs-lookup"><span data-stu-id="7ecc1-183">Install the **Microsoft.ML NuGet Package**:</span></span>

    <span data-ttu-id="7ecc1-184">Çözüm Gezgini'nde seçin ve proje üzerinde sağ **NuGet paketlerini Yönet**.</span><span class="sxs-lookup"><span data-stu-id="7ecc1-184">In Solution Explorer, right-click on your project and select **Manage NuGet Packages**.</span></span> <span data-ttu-id="7ecc1-185">Paket kaynağı olarak "nuget.org" seçin, Gözat sekmesini seçin, arama **Microsoft.ML**.</span><span class="sxs-lookup"><span data-stu-id="7ecc1-185">Choose "nuget.org" as the Package source, select the Browse tab, search for **Microsoft.ML**.</span></span> <span data-ttu-id="7ecc1-186">Tıklayarak **sürüm** açılan listesinde, select **0.10.0** paketini listede bulun ve seçin **yükleme** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="7ecc1-186">Click on the **Version** drop-down, select the **0.10.0** package in the list, and select the **Install** button.</span></span> <span data-ttu-id="7ecc1-187">Seçin **Tamam** düğmesini **Değişiklikleri Önizle** iletişim ve ardından **kabul ediyorum** düğmesini **lisans kabulü** iletişim varsa, listelenen paketlerin lisans koşullarını kabul etmiş olursunuz.</span><span class="sxs-lookup"><span data-stu-id="7ecc1-187">Select the **OK** button on the **Preview Changes** dialog and then select the **I Accept** button on the **License Acceptance** dialog if you agree with the license terms for the packages listed.</span></span> <span data-ttu-id="7ecc1-188">Bu adımı yineleyin **Microsoft.ML.ImageAnalytics v0.10.0** ve **Microsoft.ML.TensorFlow v0.10.0**.</span><span class="sxs-lookup"><span data-stu-id="7ecc1-188">Repeat these steps for **Microsoft.ML.ImageAnalytics v0.10.0** and **Microsoft.ML.TensorFlow v0.10.0**.</span></span>

  > [!NOTE]
  > <span data-ttu-id="7ecc1-189">Bu öğreticide **Microsoft.ML v0.10.0**, **Microsoft.ML.ImageAnalytics v0.10.0**, ve **Microsoft.ML.TensorFlow v0.10.0**.</span><span class="sxs-lookup"><span data-stu-id="7ecc1-189">This tutorial uses **Microsoft.ML v0.10.0**, **Microsoft.ML.ImageAnalytics v0.10.0**, and **Microsoft.ML.TensorFlow v0.10.0**.</span></span>

### <a name="prepare-your-data"></a><span data-ttu-id="7ecc1-190">Verilerinizi hazırlama</span><span class="sxs-lookup"><span data-stu-id="7ecc1-190">Prepare your data</span></span>

1. <span data-ttu-id="7ecc1-191">İndirme [proje varlıklar dizin zip dosyasını](http://download.microsoft.com/download/0/E/5/0E5E0136-21CE-4C66-AC18-9917DED8A4AD/image-classifier-assets.zip)ve sıkıştırmasını açın.</span><span class="sxs-lookup"><span data-stu-id="7ecc1-191">Download [The project assets directory zip file](http://download.microsoft.com/download/0/E/5/0E5E0136-21CE-4C66-AC18-9917DED8A4AD/image-classifier-assets.zip), and unzip.</span></span>

2. <span data-ttu-id="7ecc1-192">Kopyalama `assets` içine dizin, *TransferLearningTF* proje dizini.</span><span class="sxs-lookup"><span data-stu-id="7ecc1-192">Copy the `assets` directory into your *TransferLearningTF* project directory.</span></span> <span data-ttu-id="7ecc1-193">Bu dizin ve alt dizinlerinde (dışında indirme ve bir sonraki adımda ekleme yeni model) verileri ve destek dosyaları içeren Bu öğretici için gerekli.</span><span class="sxs-lookup"><span data-stu-id="7ecc1-193">This directory and its subdirectories contain the data and support files (except for the Inception model, which you'll download and add in the next step) needed for this tutorial.</span></span>

3. <span data-ttu-id="7ecc1-194">İndirme [başlangıcı modeli](https://storage.googleapis.com/download.tensorflow.org/models/inception5h.zip)ve sıkıştırmasını açın.</span><span class="sxs-lookup"><span data-stu-id="7ecc1-194">Download the [Inception model](https://storage.googleapis.com/download.tensorflow.org/models/inception5h.zip), and unzip.</span></span>

4. <span data-ttu-id="7ecc1-195">İçeriğini kopyalayın `inception5h` dizin yalnızca sıkıştırması açılan içine, *TransferLearningTF* proje `assets\inputs-train\inception` dizin.</span><span class="sxs-lookup"><span data-stu-id="7ecc1-195">Copy the contents of the `inception5h` directory just unzipped into your *TransferLearningTF* project `assets\inputs-train\inception` directory.</span></span> <span data-ttu-id="7ecc1-196">Bu dizin, aşağıdaki görüntüde gösterildiği gibi model ve Bu öğretici için gerekli ek destek dosyalarını içerir:</span><span class="sxs-lookup"><span data-stu-id="7ecc1-196">This directory contains the model and additional support files needed for this tutorial, as shown in the following image:</span></span>

   ![Yeni dizin içeriği](./media/image-classification/inception-files.png)

5. <span data-ttu-id="7ecc1-198">Her varlık dizin ve alt dizinleri seçip dosya Çözüm Gezgini'nde sağ **özellikleri**.</span><span class="sxs-lookup"><span data-stu-id="7ecc1-198">In Solution Explorer, right-click each of the files in the asset directory and subdirectories and select **Properties**.</span></span> <span data-ttu-id="7ecc1-199">Altında **Gelişmiş**, değiştirin **çıkış dizinine Kopyala** için **yeniyse Kopyala**.</span><span class="sxs-lookup"><span data-stu-id="7ecc1-199">Under **Advanced**, change the value of **Copy to Output Directory** to **Copy if newer**.</span></span>

### <a name="create-classes-and-define-paths"></a><span data-ttu-id="7ecc1-200">Yollarını tanımlamak ve sınıfları oluşturma</span><span class="sxs-lookup"><span data-stu-id="7ecc1-200">Create classes and define paths</span></span>

<span data-ttu-id="7ecc1-201">Aşağıdaki ek ekleyin `using` üst tarafına deyimlerini *Program.cs* dosyası:</span><span class="sxs-lookup"><span data-stu-id="7ecc1-201">Add the following additional `using` statements to the top of the *Program.cs* file:</span></span>

[!code-csharp[AddUsings](../../../samples/machine-learning/tutorials/TransferLearningTF/Program.cs#AddUsings)]

<span data-ttu-id="7ecc1-202">Yolları çeşitli varlıklar ve genel değişkenleri tutmak için genel alanlar oluşturmak `LabelTokey`,`ImageReal`, ve `PredictedLabelValue`:</span><span class="sxs-lookup"><span data-stu-id="7ecc1-202">Create global fields to hold the paths to the various assets, and global variables for the `LabelTokey`,`ImageReal`, and  `PredictedLabelValue`:</span></span>

* `_assetsPath` <span data-ttu-id="7ecc1-203">varlıkları yolu vardır.</span><span class="sxs-lookup"><span data-stu-id="7ecc1-203">has the path to the assets.</span></span>
* `_trainTagsTsv` <span data-ttu-id="7ecc1-204">yolu için eğitim görüntü veri etiketleri tsv dosyası vardır.</span><span class="sxs-lookup"><span data-stu-id="7ecc1-204">has the path to the training image data tags tsv file.</span></span>
* `_predictTagsTsv` <span data-ttu-id="7ecc1-205">yolu için tahmin görüntü veri etiketleri tsv dosyası vardır.</span><span class="sxs-lookup"><span data-stu-id="7ecc1-205">has the path to the prediction image data tags tsv file.</span></span>
* `_trainImagesFolder` <span data-ttu-id="7ecc1-206">modeli eğitmek için kullanılan görüntülerin yolunu sahiptir.</span><span class="sxs-lookup"><span data-stu-id="7ecc1-206">has the path to the images used to train the model.</span></span>
* `_predictImagesFolder` <span data-ttu-id="7ecc1-207">eğitilen modelin sınıflandırılmaya görüntü sahiptir.</span><span class="sxs-lookup"><span data-stu-id="7ecc1-207">has the path to the images to be classified by the trained model.</span></span>
* `_inceptionPb` <span data-ttu-id="7ecc1-208">Yolun modelinizi yeniden kullanılabilmeleri için önceden eğitilmiş başlangıcı modeline sahiptir.</span><span class="sxs-lookup"><span data-stu-id="7ecc1-208">has the path to the pre-trained Inception model to be reused to retrain your model.</span></span>
* `_inputImageClassifierZip` <span data-ttu-id="7ecc1-209">eğitilen model öğesinden yüklendiği yolu vardır.</span><span class="sxs-lookup"><span data-stu-id="7ecc1-209">has the path where the trained model is loaded from.</span></span>
* `_outputImageClassifierZip` <span data-ttu-id="7ecc1-210">eğitilen modelin kaydedildiği yolu vardır.</span><span class="sxs-lookup"><span data-stu-id="7ecc1-210">has the path where the trained model is saved.</span></span>
* `LabelTokey` <span data-ttu-id="7ecc1-211">olan `Label` bir anahtar ile eşlenen değeri.</span><span class="sxs-lookup"><span data-stu-id="7ecc1-211">is the `Label` value mapped to a key.</span></span>
* `ImageReal`  <span data-ttu-id="7ecc1-212">Tahmin edilen görüntü değeri içeren sütun.</span><span class="sxs-lookup"><span data-stu-id="7ecc1-212">is the column containing the predicted image value.</span></span>
* `PredictedLabelValue` <span data-ttu-id="7ecc1-213">Tahmin edilen etiket değeri içeren sütun.</span><span class="sxs-lookup"><span data-stu-id="7ecc1-213">is the column containing the predicted label value.</span></span>

<span data-ttu-id="7ecc1-214">Aşağıdaki kod satırı hemen üstündeki ekleyin `Main` yöntemi bu yollar ve diğer değişkenlerini belirtmek için:</span><span class="sxs-lookup"><span data-stu-id="7ecc1-214">Add the following code to the line right above the `Main` method to specify those paths and the other variables:</span></span>

[!code-csharp[DeclareGlobalVariables](../../../samples/machine-learning/tutorials/TransferLearningTF/Program.cs#DeclareGlobalVariables)]

<span data-ttu-id="7ecc1-215">Girdi verilerini ve tahminler elde etmek için bazı sınıflar oluşturun.</span><span class="sxs-lookup"><span data-stu-id="7ecc1-215">Create some classes for your input data, and predictions.</span></span> <span data-ttu-id="7ecc1-216">Yeni bir sınıf, projenize ekleyin:</span><span class="sxs-lookup"><span data-stu-id="7ecc1-216">Add a new class to your project:</span></span>

1. <span data-ttu-id="7ecc1-217">İçinde **Çözüm Gezgini**projeye sağ tıklayın ve ardından **Ekle** > **yeni öğe**.</span><span class="sxs-lookup"><span data-stu-id="7ecc1-217">In **Solution Explorer**, right-click the project, and then select **Add** > **New Item**.</span></span>

1. <span data-ttu-id="7ecc1-218">İçinde **Yeni Öğe Ekle** iletişim kutusunda **sınıfı** değiştirip **adı** alanı *ImageData.cs*.</span><span class="sxs-lookup"><span data-stu-id="7ecc1-218">In the **Add New Item** dialog box, select **Class** and change the **Name** field to *ImageData.cs*.</span></span> <span data-ttu-id="7ecc1-219">Ardından, **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="7ecc1-219">Then, select the **Add** button.</span></span>

    <span data-ttu-id="7ecc1-220">*ImageData.cs* dosyası Kod Düzenleyicisi'nde açılır.</span><span class="sxs-lookup"><span data-stu-id="7ecc1-220">The *ImageData.cs* file opens in the code editor.</span></span> <span data-ttu-id="7ecc1-221">Aşağıdaki `using` üstüne deyimi *ImageData.cs*:</span><span class="sxs-lookup"><span data-stu-id="7ecc1-221">Add the following `using` statement to the top of *ImageData.cs*:</span></span>

[!code-csharp[AddUsings](../../../samples/machine-learning/tutorials/TransferLearningTF/ImageData.cs#AddUsings)]

<span data-ttu-id="7ecc1-222">Varolan sınıf tanımına kaldırın ve aşağıdaki kodu ekleyin `ImageData` sınıfının *ImageData.cs* dosyası:</span><span class="sxs-lookup"><span data-stu-id="7ecc1-222">Remove the existing class definition and add the following code for the `ImageData` class to the *ImageData.cs* file:</span></span>

[!code-csharp[DeclareTypes](../../../samples/machine-learning/tutorials/TransferLearningTF/ImageData.cs#DeclareTypes)]

`ImageData` <span data-ttu-id="7ecc1-223">girdi görüntüsünün veri sınıfı ve aşağıdaki <xref:System.String> alanlar:</span><span class="sxs-lookup"><span data-stu-id="7ecc1-223">is the input image data class and has the following <xref:System.String> fields:</span></span>

* `ImagePath` <span data-ttu-id="7ecc1-224">görüntü dosya adı içeriyor.</span><span class="sxs-lookup"><span data-stu-id="7ecc1-224">contains the image file name.</span></span>
* `Label` <span data-ttu-id="7ecc1-225">görüntü etiketi için bir değer içeriyor.</span><span class="sxs-lookup"><span data-stu-id="7ecc1-225">contains a value for the image label.</span></span>

<span data-ttu-id="7ecc1-226">Projeniz için yeni bir sınıf eklemek `ImagePrediction`:</span><span class="sxs-lookup"><span data-stu-id="7ecc1-226">Add a new class to your project for `ImagePrediction`:</span></span>

1. <span data-ttu-id="7ecc1-227">İçinde **Çözüm Gezgini**projeye sağ tıklayın ve ardından **Ekle** > **yeni öğe**.</span><span class="sxs-lookup"><span data-stu-id="7ecc1-227">In **Solution Explorer**, right-click the project, and then select **Add** > **New Item**.</span></span>

1. <span data-ttu-id="7ecc1-228">İçinde **Yeni Öğe Ekle** iletişim kutusunda **sınıfı** değiştirip **adı** alanı *ImagePrediction.cs*.</span><span class="sxs-lookup"><span data-stu-id="7ecc1-228">In the **Add New Item** dialog box, select **Class** and change the **Name** field to *ImagePrediction.cs*.</span></span> <span data-ttu-id="7ecc1-229">Ardından, **Ekle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="7ecc1-229">Then, select the **Add** button.</span></span>

    <span data-ttu-id="7ecc1-230">*ImagePrediction.cs* dosyası Kod Düzenleyicisi'nde açılır.</span><span class="sxs-lookup"><span data-stu-id="7ecc1-230">The *ImagePrediction.cs* file opens in the code editor.</span></span> <span data-ttu-id="7ecc1-231">Hem de kaldırma `System.Collections.Generic` ve `System.Text` `using` deyimleri en üstündeki *ImagePrediction.cs*:</span><span class="sxs-lookup"><span data-stu-id="7ecc1-231">Remove both the `System.Collections.Generic` and the `System.Text` `using` statements at the top of *ImagePrediction.cs*:</span></span>

<span data-ttu-id="7ecc1-232">Varolan sınıf tanımına kaldırın ve olan aşağıdaki kodu ekleyin `ImagePrediction` çok sınıf *ImagePrediction.cs* dosyası:</span><span class="sxs-lookup"><span data-stu-id="7ecc1-232">Remove the existing class definition and add the following code, which has the `ImagePrediction` class, to the *ImagePrediction.cs* file:</span></span>

[!code-csharp[DeclareGlobalVariables](../../../samples/machine-learning/tutorials/TransferLearningTF/ImagePrediction.cs#DeclareTypes)]

`ImagePrediction` <span data-ttu-id="7ecc1-233">Görüntü tahmin sınıftır ve aşağıdaki alanlar vardır:</span><span class="sxs-lookup"><span data-stu-id="7ecc1-233">is the image prediction class and has the following fields:</span></span>

* `Score` <span data-ttu-id="7ecc1-234">güvenle yüzdesi verilen görüntü sınıflandırması içerir.</span><span class="sxs-lookup"><span data-stu-id="7ecc1-234">contains the confidence percentage for a given image classification.</span></span>
* `PredictedLabelValue` <span data-ttu-id="7ecc1-235">Tahmin edilen görüntü sınıflandırma etiketi için bir değer içeriyor.</span><span class="sxs-lookup"><span data-stu-id="7ecc1-235">contains a value for the predicted image classification label.</span></span>

`ImagePrediction` <span data-ttu-id="7ecc1-236">eğitilen modelin sonra sınıf tahmin için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="7ecc1-236">is the class used for prediction after the model has been trained.</span></span> <span data-ttu-id="7ecc1-237">Bunun bir `string` (`ImagePath`) görüntü yolu için.</span><span class="sxs-lookup"><span data-stu-id="7ecc1-237">It has a `string` (`ImagePath`) for the image path.</span></span> <span data-ttu-id="7ecc1-238">`Label` Modeli yeniden eğitme ve yeniden kullanmak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="7ecc1-238">The `Label` is used to reuse and retrain the model.</span></span> <span data-ttu-id="7ecc1-239">`PredictedLabelValue` Tahmin ve değerlendirme sırasında kullanılır.</span><span class="sxs-lookup"><span data-stu-id="7ecc1-239">The `PredictedLabelValue` is used during prediction and evaluation.</span></span> <span data-ttu-id="7ecc1-240">Değerlendirme, bir giriş eğitim verileri, tahmin edilen değerleri ve modeli ile kullanılır.</span><span class="sxs-lookup"><span data-stu-id="7ecc1-240">For evaluation, an input with training data, the predicted values, and the model are used.</span></span>

<span data-ttu-id="7ecc1-241">[MLContext sınıfı](xref:Microsoft.ML.MLContext) bir tüm ML.NET işlemleri için başlangıç noktası ve başlatma `mlContext` modeli oluşturma iş akışı nesneleri arasında paylaşılabilir bir yeni ML.NET ortamı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="7ecc1-241">The [MLContext class](xref:Microsoft.ML.MLContext) is a starting point for all ML.NET operations, and initializing `mlContext` creates a new ML.NET environment that can be shared across the model creation workflow objects.</span></span> <span data-ttu-id="7ecc1-242">Bu, kavramsal olarak, benzer `DBContext` Entity Framework.</span><span class="sxs-lookup"><span data-stu-id="7ecc1-242">It's similar, conceptually, to `DBContext` in Entity Framework.</span></span>

### <a name="initialize-variables-in-main"></a><span data-ttu-id="7ecc1-243">Ana değişkenleri başlatma</span><span class="sxs-lookup"><span data-stu-id="7ecc1-243">Initialize variables in Main</span></span>

<span data-ttu-id="7ecc1-244">Başlatma `mlContext` değişken ile yeni bir örneğini `MLContext`.</span><span class="sxs-lookup"><span data-stu-id="7ecc1-244">Initialize the `mlContext` variable with a new instance of `MLContext`.</span></span>  <span data-ttu-id="7ecc1-245">Değiştirin `Console.WriteLine("Hello World!")` aşağıdaki kod satırıyla `Main` yöntemi:</span><span class="sxs-lookup"><span data-stu-id="7ecc1-245">Replace the `Console.WriteLine("Hello World!")` line with the following code in the `Main` method:</span></span>

[!code-csharp[CreateMLContext](../../../samples/machine-learning/tutorials/TransferLearningTF/Program.cs#CreateMLContext)]

### <a name="create-a-struct-for-default-parameters"></a><span data-ttu-id="7ecc1-246">Varsayılan parametreleri için bir yapı oluşturma</span><span class="sxs-lookup"><span data-stu-id="7ecc1-246">Create a struct for default parameters</span></span>

<span data-ttu-id="7ecc1-247">Yeni modelde birkaç varsayılan parametre olarak geçirmenize gerek yok.</span><span class="sxs-lookup"><span data-stu-id="7ecc1-247">The Inception model has several default parameters you need to pass in.</span></span> <span data-ttu-id="7ecc1-248">Aşağıdaki kod ile kolay adlar için varsayılan parametre değerlerini hemen sonra eşlemek için bir yapı oluşturmak `Main()` yöntemi:</span><span class="sxs-lookup"><span data-stu-id="7ecc1-248">Create a struct to map the default parameter values to friendly names with the following code, just after the `Main()` method:</span></span>

[!code-csharp[InceptionSettings](../../../samples/machine-learning/tutorials/TransferLearningTF/Program.cs#InceptionSettings)]

### <a name="create-a-display-utility-method"></a><span data-ttu-id="7ecc1-249">Görüntü yardımcı programı yöntemi oluşturma</span><span class="sxs-lookup"><span data-stu-id="7ecc1-249">Create a display utility method</span></span>

<span data-ttu-id="7ecc1-250">Daha fazla kez ve görüntü verileri ve ilgili Öngörüler yinelenen kodu istemiyorsanız eşleştirme ve görüntü.</span><span class="sxs-lookup"><span data-stu-id="7ecc1-250">Pair and display the image data and the related predictions more than once, and you don't want to duplicate code.</span></span> <span data-ttu-id="7ecc1-251">Eşleştirme ve görüntü ve tahmin sonuçlarını görüntüleyen işlemek için bir görüntü yardımcı programı yöntemi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="7ecc1-251">Create a display utility method to handle pairing and displaying the image and prediction results.</span></span>

<span data-ttu-id="7ecc1-252">`PairAndDisplayResults()` Yöntemi aşağıdaki görevleri yürütür:</span><span class="sxs-lookup"><span data-stu-id="7ecc1-252">The `PairAndDisplayResults()` method executes the following tasks:</span></span>

* <span data-ttu-id="7ecc1-253">Veri ve raporlama için Öngörüler birleştirir.</span><span class="sxs-lookup"><span data-stu-id="7ecc1-253">Combines data and predictions for reporting.</span></span>
* <span data-ttu-id="7ecc1-254">Tahmin edilen sonuçları görüntüler.</span><span class="sxs-lookup"><span data-stu-id="7ecc1-254">Displays the predicted results.</span></span>

<span data-ttu-id="7ecc1-255">Oluşturma `PairAndDisplayResults()` yöntemi hemen sonrasına `InceptionSettings` yapısı, aşağıdaki kodu kullanarak:</span><span class="sxs-lookup"><span data-stu-id="7ecc1-255">Create the `PairAndDisplayResults()` method, just after the `InceptionSettings` struct, using the following code:</span></span>

```csharp
private static void PairAndDisplayResults(IEnumerable<ImageNetData> imageData, IEnumerable<ImageNetPrediction> imagePredictionData)
{

}
```

<span data-ttu-id="7ecc1-256">Tahmin edilen sonuçlarını görüntülemeden önce birleştirme `imageData` ve `imagePrediction` özgün birlikte görmek için `Image Path` tahmin edilen kategori ile.</span><span class="sxs-lookup"><span data-stu-id="7ecc1-256">Before displaying the predicted results, combine the `imageData` and `imagePrediction` together to see the original `Image Path` with its predicted category.</span></span> <span data-ttu-id="7ecc1-257">Aşağıdaki kod <xref:System.Linq.Enumerable.Zip%2A?displayProperty=nameWithType> yöntemini gerçekleşen, sağlamak için bu nedenle ilk satırı olarak bu ekleyin `PairAndDisplayResults()` yöntemi:</span><span class="sxs-lookup"><span data-stu-id="7ecc1-257">The following code uses the <xref:System.Linq.Enumerable.Zip%2A?displayProperty=nameWithType> method to make that happen, so add it as the first line of the `PairAndDisplayResults()` method:</span></span>

[!code-csharp[BuildImagePredictionPairs](../../../samples/machine-learning/tutorials/TransferLearningTF/Program.cs#BuildImagePredictionPairs)]

<span data-ttu-id="7ecc1-258">Birleştirilmiş göre `imageData` ve `imageData` bir sınıf kullanarak sonuçları görüntüleyebilirsiniz <xref:System.Console.WriteLine?displayProperty=nameWithType> yöntemi:</span><span class="sxs-lookup"><span data-stu-id="7ecc1-258">Now that you've combined the `imageData` and `imageData` into a class, you can display the results using the <xref:System.Console.WriteLine?displayProperty=nameWithType> method:</span></span>

[!code-csharp[DisplayPredictions](../../../samples/machine-learning/tutorials/TransferLearningTF/Program.cs#DisplayPredictions)]

<span data-ttu-id="7ecc1-259">Sizi ararız `PairAndDisplayResults()` sonraki iki yöntemle yöntemi.</span><span class="sxs-lookup"><span data-stu-id="7ecc1-259">You'll call the `PairAndDisplayResults()` method in the next two methods.</span></span>

### <a name="create-a-tsv-file-utility-method"></a><span data-ttu-id="7ecc1-260">.Tsv dosya yardımcı program metodu oluştur</span><span class="sxs-lookup"><span data-stu-id="7ecc1-260">Create a .tsv file utility method</span></span>

<span data-ttu-id="7ecc1-261">`ReadFromTsv()` Yöntemi aşağıdaki görevleri yürütür:</span><span class="sxs-lookup"><span data-stu-id="7ecc1-261">The `ReadFromTsv()` method executes the following tasks:</span></span>

* <span data-ttu-id="7ecc1-262">Görüntü verisini okur `tags.tsv` dosya.</span><span class="sxs-lookup"><span data-stu-id="7ecc1-262">Reads the image data `tags.tsv` file.</span></span>
* <span data-ttu-id="7ecc1-263">Dosya yolu görüntü dosya adına ekler.</span><span class="sxs-lookup"><span data-stu-id="7ecc1-263">Adds the file path to the image file name.</span></span>
* <span data-ttu-id="7ecc1-264">Dosya verilerini bir IEnumerable yükler`ImageData` nesne.</span><span class="sxs-lookup"><span data-stu-id="7ecc1-264">Loads the file data into an IEnumerable`ImageData` object.</span></span>

<span data-ttu-id="7ecc1-265">Oluşturma `ReadFromTsv()` yöntemi hemen sonrasına `PairAndDisplayResults()` yöntemi, aşağıdaki kodu kullanarak:</span><span class="sxs-lookup"><span data-stu-id="7ecc1-265">Create the `ReadFromTsv()` method, just after the `PairAndDisplayResults()` method, using the following code:</span></span>

```csharp
public static IEnumerable<ImageData> ReadFromTsv(string file, string folder)
{

}
```

<span data-ttu-id="7ecc1-266">Aşağıdaki kod aracılığıyla ayrıştırır `tags.tsv` dosya yolu için resim dosya adı eklemek için dosya `ImagePath` özelliği ve yükler ve `Label` içine bir `ImageData` nesne.</span><span class="sxs-lookup"><span data-stu-id="7ecc1-266">The following code parses through the `tags.tsv` file to add the file path to the image file name for the `ImagePath` property and load it and the `Label` into an `ImageData` object.</span></span> <span data-ttu-id="7ecc1-267">İlk satırı olarak ekleyin `ReadFromTsv()` yöntemi.</span><span class="sxs-lookup"><span data-stu-id="7ecc1-267">Add it as the first line of the `ReadFromTsv()` method.</span></span>  <span data-ttu-id="7ecc1-268">Tahmin sonuçlarını görüntülemek için tam dosya yolunu ihtiyacınız vardır.</span><span class="sxs-lookup"><span data-stu-id="7ecc1-268">You need the fully qualified file path to display the prediction results.</span></span>

[!code-csharp[ReadFromTsv](../../../samples/machine-learning/tutorials/TransferLearningTF/Program.cs#ReadFromTsv)]
<span data-ttu-id="7ecc1-269">ML.NET içinde üç ana kavramı vardır: [Veri](../basic-concepts-model-training-in-mldotnet.md#data), [dönüştürücüler](../basic-concepts-model-training-in-mldotnet.md#transformer), ve [Estimators](../basic-concepts-model-training-in-mldotnet.md#estimator).</span><span class="sxs-lookup"><span data-stu-id="7ecc1-269">There are three major concepts in ML.NET: [Data](../basic-concepts-model-training-in-mldotnet.md#data), [Transformers](../basic-concepts-model-training-in-mldotnet.md#transformer), and [Estimators](../basic-concepts-model-training-in-mldotnet.md#estimator).</span></span>

## <a name="reuse-and-tune-pre-trained-model"></a><span data-ttu-id="7ecc1-270">Yeniden kullanmak ve önceden eğitilmiş bir modeli ayarlama</span><span class="sxs-lookup"><span data-stu-id="7ecc1-270">Reuse and tune pre-trained model</span></span>

<span data-ttu-id="7ecc1-271">Aşağıdaki çağrısı ekleyin `ReuseAndTuneInceptionModel()`yöntemi sonraki kod satırı olarak `Main()` yöntemi:</span><span class="sxs-lookup"><span data-stu-id="7ecc1-271">Add the following call to the `ReuseAndTuneInceptionModel()`method as the next line of code in the `Main()` method:</span></span>

[!code-csharp[CallReuseAndTuneInceptionModel](../../../samples/machine-learning/tutorials/TransferLearningTF/Program.cs#CallReuseAndTuneInceptionModel)]

<span data-ttu-id="7ecc1-272">`ReuseAndTuneInceptionModel()` Yöntemi aşağıdaki görevleri yürütür:</span><span class="sxs-lookup"><span data-stu-id="7ecc1-272">The `ReuseAndTuneInceptionModel()` method executes the following tasks:</span></span>

* <span data-ttu-id="7ecc1-273">Verileri yükler</span><span class="sxs-lookup"><span data-stu-id="7ecc1-273">Loads the data</span></span>
* <span data-ttu-id="7ecc1-274">Ayıklar ve verileri dönüştürür.</span><span class="sxs-lookup"><span data-stu-id="7ecc1-274">Extracts and transforms the data.</span></span>
* <span data-ttu-id="7ecc1-275">TensorFlow modelini puanlar.</span><span class="sxs-lookup"><span data-stu-id="7ecc1-275">Scores the TensorFlow model.</span></span>
* <span data-ttu-id="7ecc1-276">(Çağırma sayısı) tabanlarını modeli.</span><span class="sxs-lookup"><span data-stu-id="7ecc1-276">Tunes (retrains) the model.</span></span>
* <span data-ttu-id="7ecc1-277">Model sonuçlarını görüntüler.</span><span class="sxs-lookup"><span data-stu-id="7ecc1-277">Displays model results.</span></span>
* <span data-ttu-id="7ecc1-278">Model değerlendirir.</span><span class="sxs-lookup"><span data-stu-id="7ecc1-278">Evaluates the model.</span></span>
* <span data-ttu-id="7ecc1-279">Model kaydeder.</span><span class="sxs-lookup"><span data-stu-id="7ecc1-279">Saves the model.</span></span>

<span data-ttu-id="7ecc1-280">Oluşturma `ReuseAndTuneInceptionModel()` yöntemi hemen sonrasına `InceptionSettings` yapısı ve hemen önce `PairAndDisplayResults()` yöntemi, aşağıdaki kodu kullanarak:</span><span class="sxs-lookup"><span data-stu-id="7ecc1-280">Create the `ReuseAndTuneInceptionModel()` method, just after the `InceptionSettings` struct and just before the `PairAndDisplayResults()` method, using the following code:</span></span>

```csharp
public static void ReuseAndTuneInceptionModel(MLContext mlContext, string dataLocation, string imagesFolder, string inputModelLocation, string outputModelLocation)
{

}
```

### <a name="load-the-data"></a><span data-ttu-id="7ecc1-281">Verileri yükleme</span><span class="sxs-lookup"><span data-stu-id="7ecc1-281">Load the data</span></span>

<span data-ttu-id="7ecc1-282">ML.NET verilerinde olarak temsil edilir bir [IDataView sınıfı](xref:Microsoft.Data.DataView.IDataView).</span><span class="sxs-lookup"><span data-stu-id="7ecc1-282">Data in ML.NET is represented as an [IDataView class](xref:Microsoft.Data.DataView.IDataView).</span></span> `IDataView` <span data-ttu-id="7ecc1-283">Sekmeli veriler (sayısal ve metin) açıklayan bir esnek ve verimli yoludur.</span><span class="sxs-lookup"><span data-stu-id="7ecc1-283">is a flexible, efficient way of describing tabular data (numeric and text).</span></span> <span data-ttu-id="7ecc1-284">Veri yüklenebilir bir metin dosyasından veya gerçek zamanlı olarak (örneğin, SQL veritabanı veya günlük dosyaları) için bir `IDataView` nesne.</span><span class="sxs-lookup"><span data-stu-id="7ecc1-284">Data can be loaded from a text file or in real time (for example, SQL database or log files) to an `IDataView` object.</span></span>

<span data-ttu-id="7ecc1-285">Kullanarak verileri yüklemek `MLContext.Data.ReadFromTextFile` sarmalayıcı.</span><span class="sxs-lookup"><span data-stu-id="7ecc1-285">Load the data using the `MLContext.Data.ReadFromTextFile` wrapper.</span></span> <span data-ttu-id="7ecc1-286">Sonraki satırda olarak aşağıdaki kodu ekleyin `ReuseAndTuneInceptionModel()` yöntemi:</span><span class="sxs-lookup"><span data-stu-id="7ecc1-286">Add the following code as the next line in the `ReuseAndTuneInceptionModel()` method:</span></span>

[!code-csharp[LoadData](../../../samples/machine-learning/tutorials/TransferLearningTF/Program.cs#LoadData "Load the data")]

### <a name="extract-features-and-transform-the-data"></a><span data-ttu-id="7ecc1-287">Özellikleri ayıklayın ve verileri dönüştürme</span><span class="sxs-lookup"><span data-stu-id="7ecc1-287">Extract Features and transform the data</span></span>

<span data-ttu-id="7ecc1-288">Ön işleme ve verileri temizleme bir veri kümesi, machine learning için etkili bir şekilde kullanılmadan önce gerçekleşen önemli görevlerdir.</span><span class="sxs-lookup"><span data-stu-id="7ecc1-288">Pre-processing and cleaning data are important tasks that occur before a dataset is used effectively for machine learning.</span></span>  <span data-ttu-id="7ecc1-289">Veri modelleme görevleri olmadan kullanarak yanıltıcı sonuçlara neden olabilir.</span><span class="sxs-lookup"><span data-stu-id="7ecc1-289">Using data without these modeling tasks can produce misleading results.</span></span>

<span data-ttu-id="7ecc1-290">Makine öğrenimi algoritmaları anlamak [özellikleri tespit](../resources/glossary.md#feature) verileri ve ne zaman, derin sinir ağları ile ilgilenen gerekir uyarlayabilirsiniz ağ tarafından beklenen biçimde görüntüleri.</span><span class="sxs-lookup"><span data-stu-id="7ecc1-290">Machine learning algorithms understand [featurized](../resources/glossary.md#feature) data, and when dealing with deep neural networks you must adapt the images to the format expected by the network.</span></span> <span data-ttu-id="7ecc1-291">Bu biçim bir [sayısal vektör](../resources/glossary.md#numerical-feature-vector).</span><span class="sxs-lookup"><span data-stu-id="7ecc1-291">That format is a [numeric vector](../resources/glossary.md#numerical-feature-vector).</span></span>

<span data-ttu-id="7ecc1-292">Eğitim ve değerlendirme sonra ile tahmin **etiket** sütun değerleri.</span><span class="sxs-lookup"><span data-stu-id="7ecc1-292">After training and evaluation, predict with the **Label** column values.</span></span> <span data-ttu-id="7ecc1-293">Önceden eğitilmiş bir modeli kullandığınız gibi alanları yeni modeliyle eşlemek [MapValueToKey()](xref:Microsoft.ML.ConversionsExtensionsCatalog.MapValueToKey%2A) yöntemi.</span><span class="sxs-lookup"><span data-stu-id="7ecc1-293">As you're using a pre-trained model, map fields to the new model with the [MapValueToKey()](xref:Microsoft.ML.ConversionsExtensionsCatalog.MapValueToKey%2A) method.</span></span> <span data-ttu-id="7ecc1-294">Bu yöntem dönüştüren `Label` sayısal bir anahtar türü (`LabelTokey`) sütunu ve yeni veri kümesi sütun olarak ekleyin:  Bu ad `estimator` gibi de Eğitmeni kendisine eklemeniz.</span><span class="sxs-lookup"><span data-stu-id="7ecc1-294">This method transforms the `Label` into a numeric key type (`LabelTokey`) column and add it as new dataset column:  Name this `estimator` as you'll also add the trainer to it.</span></span> <span data-ttu-id="7ecc1-295">Sonraki kod satırı ekleyin:</span><span class="sxs-lookup"><span data-stu-id="7ecc1-295">Add the next line of code:</span></span>

[!code-csharp[MapValueToKey1](../../../samples/machine-learning/tutorials/TransferLearningTF/Program.cs#MapValueToKey1)]

<span data-ttu-id="7ecc1-296">Resim estimator kullanan önceden eğitilmiş işleme [derin sinir Network(DNN)](https://en.wikipedia.org/wiki/Deep_learning#Deep_neural_networks) featurizers özelliği ayıklama için.</span><span class="sxs-lookup"><span data-stu-id="7ecc1-296">Your image processing estimator uses pre-trained [Deep Neural Network(DNN)](https://en.wikipedia.org/wiki/Deep_learning#Deep_neural_networks) featurizers for feature extraction.</span></span> <span data-ttu-id="7ecc1-297">Derin sinir ağları ile ilgilenirken, beklenen ağ biçimi görüntülerin uyarlayın.</span><span class="sxs-lookup"><span data-stu-id="7ecc1-297">When dealing with deep neural networks, you  adapt the images to the expected network format.</span></span> <span data-ttu-id="7ecc1-298">Modelin beklenen biçime görüntü verilerini almak için kullandığınız görüntü dönüşümlerden nedeni budur:</span><span class="sxs-lookup"><span data-stu-id="7ecc1-298">This is the reason you use several image transforms to get the image data into the model's expected form:</span></span>

1. <span data-ttu-id="7ecc1-299">`LoadImages`Dönüştürme görüntü bit eşlem türü olarak belleğe yüklenir.</span><span class="sxs-lookup"><span data-stu-id="7ecc1-299">The `LoadImages`transform images are loaded in memory as a Bitmap type.</span></span>
2. <span data-ttu-id="7ecc1-300">`Resize` Dönüştürme olarak önceden eğitilmiş model tanımlı girdi görüntüsü genişliği ve yüksekliği görüntüleri yeniden boyutlandırır.</span><span class="sxs-lookup"><span data-stu-id="7ecc1-300">The `Resize` transform resizes the images as the pre-trained model has a defined input image width and height.</span></span>
3. <span data-ttu-id="7ecc1-301">`ImagePixelExtractingEstimator` Dönüştürme giriş görüntülerden piksel ayıklar ve bunları sayısal vektörü dönüştürür.</span><span class="sxs-lookup"><span data-stu-id="7ecc1-301">The `ImagePixelExtractingEstimator` transform extracts the pixels from the input images and converts them into a numeric vector.</span></span>

<span data-ttu-id="7ecc1-302">Bu görüntü dönüşümler sonraki kod satırı ekleyin:</span><span class="sxs-lookup"><span data-stu-id="7ecc1-302">Add these image transforms as the next lines of code:</span></span>

[!code-csharp[ImageTransforms](../../../samples/machine-learning/tutorials/TransferLearningTF/Program.cs#ImageTransforms)]

<span data-ttu-id="7ecc1-303">`TensorFlowTransform` Ayıklar belirtilen çıkış ( `Inception model`ait görüntü özellikleri `softmax2_pre_activation`) ve önceden eğitilmiş kullanarak bir veri kümesi puanlar `TensorFlow` modeli.</span><span class="sxs-lookup"><span data-stu-id="7ecc1-303">The `TensorFlowTransform` extracts specified outputs (the `Inception model`'s image features `softmax2_pre_activation`), and scores a dataset using the pre-trained `TensorFlow` model.</span></span>

`softmax2_pre_activation` <span data-ttu-id="7ecc1-304">model, görüntüleri sınıfı belirleyen ile ait olduğu yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="7ecc1-304">assists the model with determining which class the images belongs to.</span></span> `softmax2_pre_activation` <span data-ttu-id="7ecc1-305">Görüntü kategorilerin her birine ve tüm bu olasılıklar olasılığını döndürür, en fazla 1 eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="7ecc1-305">returns a probability for each of the categories for an image, and all of those probabilities must add up to 1.</span></span> <span data-ttu-id="7ecc1-306">Bu görüntü tek bir kategoriye ait olacak aşağıdaki örnekte gösterildiği gibi varsayılır:</span><span class="sxs-lookup"><span data-stu-id="7ecc1-306">It assumes that an image will belong to only one category, as shown in the following example:</span></span>

| <span data-ttu-id="7ecc1-307">örneği</span><span class="sxs-lookup"><span data-stu-id="7ecc1-307">Class</span></span>         | <span data-ttu-id="7ecc1-308">Olasılık</span><span class="sxs-lookup"><span data-stu-id="7ecc1-308">Probability</span></span>   |
| ------------- | ------------- |
| `Food`        |  <span data-ttu-id="7ecc1-309">0.001</span><span class="sxs-lookup"><span data-stu-id="7ecc1-309">0.001</span></span>        |
| `Toy`         |  <span data-ttu-id="7ecc1-310">0.95</span><span class="sxs-lookup"><span data-stu-id="7ecc1-310">0.95</span></span>         |
| `Appliance`   |  <span data-ttu-id="7ecc1-311">0,06</span><span class="sxs-lookup"><span data-stu-id="7ecc1-311">0.06</span></span>         |

<span data-ttu-id="7ecc1-312">Append `TensorFlowTransform` için `estimator` aşağıdaki kod satırını ile:</span><span class="sxs-lookup"><span data-stu-id="7ecc1-312">Append the `TensorFlowTransform` to the `estimator` with the following line of code:</span></span>

[!code-csharp[ScoreTensorFlowModel](../../../samples/machine-learning/tutorials/TransferLearningTF/Program.cs#ScoreTensorFlowModel)]

### <a name="choose-a-training-algorithm"></a><span data-ttu-id="7ecc1-313">Eğitim algoritması seçin</span><span class="sxs-lookup"><span data-stu-id="7ecc1-313">Choose a training algorithm</span></span>

<span data-ttu-id="7ecc1-314">Eğitim algoritması eklemek için çağrı `mlContext.MulticlassClassification.Trainers.LogisticRegression()` sarmalayıcı yöntemi.</span><span class="sxs-lookup"><span data-stu-id="7ecc1-314">To add the training algorithm, call the `mlContext.MulticlassClassification.Trainers.LogisticRegression()` wrapper method.</span></span>  <span data-ttu-id="7ecc1-315">`LogisticRegression` Eklenir `estimator` ve yeni görüntü özelliklerini kabul eder (`softmax2_pre_activation`) ve `Label` giriş geçmiş verilerden bilgi edinmek için parametreleri.</span><span class="sxs-lookup"><span data-stu-id="7ecc1-315">The `LogisticRegression` is appended to the `estimator` and accepts the Inception image features (`softmax2_pre_activation`) and the `Label` input parameters to learn from the historic data.</span></span>  <span data-ttu-id="7ecc1-316">Eğitmeni ile aşağıdaki kodu ekleyin:</span><span class="sxs-lookup"><span data-stu-id="7ecc1-316">Add the trainer with the following code:</span></span>

[!code-csharp[AddTrainer](../../../samples/machine-learning/tutorials/TransferLearningTF/Program.cs#AddTrainer)]

<span data-ttu-id="7ecc1-317">Harita gerekir `predictedlabel` için `predictedlabelvalue`:</span><span class="sxs-lookup"><span data-stu-id="7ecc1-317">You also need to map the `predictedlabel` to the `predictedlabelvalue`:</span></span>

[!code-csharp[MapValueToKey2](../../../samples/machine-learning/tutorials/TransferLearningTF/Program.cs#MapValueToKey2)]

<span data-ttu-id="7ecc1-318">`Fit()` Yöntemine sağlanan bir eğitim veri kümesi modelinizi eğitir.</span><span class="sxs-lookup"><span data-stu-id="7ecc1-318">The `Fit()` method trains your model with the provided training dataset.</span></span> <span data-ttu-id="7ecc1-319">Yürütülmeden `Estimator` verileri dönüştürme ve eğitim ve uygulama tanımlarını döndürür geri olan eğitilen model bir `Transformer`.</span><span class="sxs-lookup"><span data-stu-id="7ecc1-319">It executes the `Estimator` definitions by transforming the data and applying the training, and it returns back the trained model, which is a `Transformer`.</span></span> <span data-ttu-id="7ecc1-320">Modele uygun `Train` veri ve sonraki kod satırı olarak aşağıdakileri ekleyerek eğitilen model dönüş `ReuseAndTuneInceptionModel()` yöntemi:</span><span class="sxs-lookup"><span data-stu-id="7ecc1-320">Fit the model to the `Train` data and return the trained model by adding the following as the next line of code in the `ReuseAndTuneInceptionModel()` method:</span></span>

[!code-csharp[TrainModel](../../../samples/machine-learning/tutorials/TransferLearningTF/Program.cs#TrainModel)]

<span data-ttu-id="7ecc1-321">[Transform()](xref:Microsoft.ML.ITransformer.Transform%2A) yöntemi, birden çok test veri kümesini girdi satırları sağlanan için Öngörüler sağlar.</span><span class="sxs-lookup"><span data-stu-id="7ecc1-321">The [Transform()](xref:Microsoft.ML.ITransformer.Transform%2A) method makes predictions for multiple provided input rows of a test dataset.</span></span>  <span data-ttu-id="7ecc1-322">Dönüştürme `Training` aşağıdakileri ekleyerek veri kod için `ReuseAndTuneInceptionModel()`:</span><span class="sxs-lookup"><span data-stu-id="7ecc1-322">Transform the `Training` data by adding the following code to `ReuseAndTuneInceptionModel()`:</span></span>

[!code-csharp[TransformData](../../../samples/machine-learning/tutorials/TransferLearningTF/Program.cs#TransformData)]

<span data-ttu-id="7ecc1-323">Görüntü veri ve öngörü dönüştürme `DataViews` içine kesin türü belirtilmiş `IEnumerables` çiftine daha kolay görüntüleme için.</span><span class="sxs-lookup"><span data-stu-id="7ecc1-323">Convert your image data and prediction `DataViews` into strongly-typed `IEnumerables` to pair for easier display.</span></span> <span data-ttu-id="7ecc1-324">Kullanım `MLContext.CreateEnumerable()` yöntemi, aşağıdaki kodu kullanarak yapmak için:</span><span class="sxs-lookup"><span data-stu-id="7ecc1-324">Use the `MLContext.CreateEnumerable()` method to do that, using the following code:</span></span>

[!code-csharp[EnumerateDataViews](../../../samples/machine-learning/tutorials/TransferLearningTF/Program.cs#EnumerateDataViews)]

<span data-ttu-id="7ecc1-325">Çağrı `PairAndDisplayResults()` eşleştirin ve verilerinizi ve Öngörüler sonraki satırı olarak görüntülemek için yöntem `ReuseAndTuneInceptionModel()` yöntemi:</span><span class="sxs-lookup"><span data-stu-id="7ecc1-325">Call the `PairAndDisplayResults()` method to pair and display your data and predictions as the next line in the `ReuseAndTuneInceptionModel()` method:</span></span>

[!code-csharp[CallPairAndDisplayResults1](../../../samples/machine-learning/tutorials/TransferLearningTF/Program.cs#CallPairAndDisplayResults1)]

<span data-ttu-id="7ecc1-326">Ayarlanırsa, tahmin sonra [Evaluate()](xref:Microsoft.ML.RecommendationCatalog.Evaluate%2A) yöntemi:</span><span class="sxs-lookup"><span data-stu-id="7ecc1-326">Once you have the prediction set, the [Evaluate()](xref:Microsoft.ML.RecommendationCatalog.Evaluate%2A) method:</span></span>

* <span data-ttu-id="7ecc1-327">Model değerlendirir (tahmin edilen değeri ile gerçek veri kümesini karşılaştırır `Labels`).</span><span class="sxs-lookup"><span data-stu-id="7ecc1-327">Assesses the model (compares the predicted values with the actual dataset `Labels`).</span></span>

* <span data-ttu-id="7ecc1-328">Model performansı ölçümlerini döndürür.</span><span class="sxs-lookup"><span data-stu-id="7ecc1-328">Returns the model performance metrics.</span></span> 

<span data-ttu-id="7ecc1-329">Aşağıdaki kodu ekleyin `ReuseAndTuneInceptionModel()` yöntemi sonraki satır olarak:</span><span class="sxs-lookup"><span data-stu-id="7ecc1-329">Add the following code to the `ReuseAndTuneInceptionModel()` method as the next line:</span></span>

[!code-csharp[Evaluate](../../../samples/machine-learning/tutorials/TransferLearningTF/Program.cs#Evaluate)]

<span data-ttu-id="7ecc1-330">Aşağıdaki ölçümler için görüntü sınıflandırması değerlendirilir:</span><span class="sxs-lookup"><span data-stu-id="7ecc1-330">The following metrics are evaluated for image classification:</span></span>

* `Log-loss` <span data-ttu-id="7ecc1-331">-bkz [günlük kaybı](../resources/glossary.md#log-loss).</span><span class="sxs-lookup"><span data-stu-id="7ecc1-331">- see [Log Loss](../resources/glossary.md#log-loss).</span></span> <span data-ttu-id="7ecc1-332">Sıfır olarak mümkün olduğunca yakın olmasını günlük zarar kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="7ecc1-332">You want Log-loss to be as close to zero as possible.</span></span>

* `Per class Log-loss`<span data-ttu-id="7ecc1-333">biçimindeki telefon numarasıdır.</span><span class="sxs-lookup"><span data-stu-id="7ecc1-333">.</span></span> <span data-ttu-id="7ecc1-334">Sınıf günlük kaybı sıfır olarak mümkün olduğunca yakın olmasını istediğiniz.</span><span class="sxs-lookup"><span data-stu-id="7ecc1-334">You want per class Log-loss to be as close to zero as possible.</span></span>

<span data-ttu-id="7ecc1-335">Ölçümleri görüntülemek için sonuçları paylaşıp bunlar üzerinde harekete aşağıdaki kodu kullanın:</span><span class="sxs-lookup"><span data-stu-id="7ecc1-335">Use the following code to display the metrics, share the results, and then act on them:</span></span>

[!code-csharp[DisplayMetrics](../../../samples/machine-learning/tutorials/TransferLearningTF/Program.cs#DisplayMetrics)]

`mlContext.Model.Save` <span data-ttu-id="7ecc1-336">eğitilen model diğer .NET uygulamalarında tahminlerde bulunmak için kullanılabilecek bir .zip dosyası olarak ("varlıklar/çıkışları" klasöründe farklı olarak) kaydeder.</span><span class="sxs-lookup"><span data-stu-id="7ecc1-336">saves your trained model to a .zip file (in the "assets/outputs" folder), which can be used in other .NET applications to make predictions.</span></span> <span data-ttu-id="7ecc1-337">Aşağıdaki kodu ekleyin `ReuseAndTuneInceptionModel()` yöntemi sonraki satır olarak:</span><span class="sxs-lookup"><span data-stu-id="7ecc1-337">Add the following code to the `ReuseAndTuneInceptionModel()` method as the next line:</span></span>

[!code-csharp[SaveModel](../../../samples/machine-learning/tutorials/TransferLearningTF/Program.cs#SaveModel)]

## <a name="classify-images-with-a-loaded-model"></a><span data-ttu-id="7ecc1-338">Yüklenen bir model ile görüntü sınıflandırma</span><span class="sxs-lookup"><span data-stu-id="7ecc1-338">Classify images with a loaded model</span></span>

<span data-ttu-id="7ecc1-339">Aşağıdaki çağrısı ekleyin `ClassifyImages()` yöntemi sonraki kod satırı olarak `Main` yöntemi:</span><span class="sxs-lookup"><span data-stu-id="7ecc1-339">Add the following call to the `ClassifyImages()` method as the next line of code in the `Main` method:</span></span>

[!code-csharp[CallClassifyImages](../../../samples/machine-learning/tutorials/TransferLearningTF/Program.cs#CallClassifyImages)]

<span data-ttu-id="7ecc1-340">`ClassifyImages()` Yöntemi aşağıdaki görevleri yürütür:</span><span class="sxs-lookup"><span data-stu-id="7ecc1-340">The `ClassifyImages()` method executes the following tasks:</span></span>

* <span data-ttu-id="7ecc1-341">Modeli yükler.</span><span class="sxs-lookup"><span data-stu-id="7ecc1-341">Loads the model.</span></span>
* <span data-ttu-id="7ecc1-342">Okur. TSV dosyasına `IEnumerable`.</span><span class="sxs-lookup"><span data-stu-id="7ecc1-342">Reads .TSV file into `IEnumerable`.</span></span>
* <span data-ttu-id="7ecc1-343">Test verileri temel alan görüntü sınıflandırmaları tahmin eder.</span><span class="sxs-lookup"><span data-stu-id="7ecc1-343">Predicts image classifications based on test data.</span></span>

<span data-ttu-id="7ecc1-344">Oluşturma `ClassifyImages()` yöntemi hemen sonrasına `ReuseAndTuneInceptionModel()` yöntemi ve hemen önce `PairAndDisplayResults()` yöntemi, aşağıdaki kodu kullanarak:</span><span class="sxs-lookup"><span data-stu-id="7ecc1-344">Create the `ClassifyImages()` method, just after the `ReuseAndTuneInceptionModel()` method and just before the `PairAndDisplayResults()` method, using the following code:</span></span>

```csharp
public static void ClassifyImages(MLContext mlContext, string dataLocation, string imagesFolder, string outputModelLocation)
{

}
```

<span data-ttu-id="7ecc1-345">İlk olarak, aşağıdaki kod ile daha önce kaydettiğiniz model yüklenemiyor:</span><span class="sxs-lookup"><span data-stu-id="7ecc1-345">First, load the model that you saved previously with the following code:</span></span>

[!code-csharp[LoadModel](../../../samples/machine-learning/tutorials/TransferLearningTF/Program.cs#LoadModel)]

<span data-ttu-id="7ecc1-346">Çağrı `ReadFromTsv()` yöntemi oluşturmak için bir `IEnumerable<ImageData>` her biri için tam yolu içeren sınıf `ImagePath`.</span><span class="sxs-lookup"><span data-stu-id="7ecc1-346">Call the `ReadFromTsv()` method to create an `IEnumerable<ImageData>` class that contains the fully qualified path for each `ImagePath`.</span></span> <span data-ttu-id="7ecc1-347">Bu dosya yolu, veri ve öngörü sonuçlarınızı eşleştirmeye ihtiyacınız vardır.</span><span class="sxs-lookup"><span data-stu-id="7ecc1-347">You need that file path to pair your data and prediction results.</span></span> <span data-ttu-id="7ecc1-348">Dönüştürmeniz gerekir `IEnumerable<ImageData>` sınıfının bir `IDataView` tahmin etmek için kullanacağınız.</span><span class="sxs-lookup"><span data-stu-id="7ecc1-348">You also need to convert the `IEnumerable<ImageData>` class to an `IDataView` that you will use to predict.</span></span> <span data-ttu-id="7ecc1-349">Sonraki iki satırlar halinde aşağıdaki kodu ekleyin `ClassifyImages()` yöntemi:</span><span class="sxs-lookup"><span data-stu-id="7ecc1-349">Add the following code as the next two lines in the `ClassifyImages()` method:</span></span>

[!code-csharp[ReadFromTSV](../../../samples/machine-learning/tutorials/TransferLearningTF/Program.cs#ReadFromTSV)]

<span data-ttu-id="7ecc1-350">Eğitim resmi verilerle daha önce yaptığınız gibi test görüntü kullanarak verileri kategori tahmin [Transform()](xref:Microsoft.ML.ITransformer.Transform%2A) yöntemi.</span><span class="sxs-lookup"><span data-stu-id="7ecc1-350">As you did previously with the training image data, predict the category of the test image data using the [Transform()](xref:Microsoft.ML.ITransformer.Transform%2A) method.</span></span> <span data-ttu-id="7ecc1-351">Aşağıdaki kodu ekleyin `ClassifyImages()` yöntemi tahminler elde etmek için ve dönüştürmek için `predictions` `IDataView` içine bir `IEnumerable` eşleştirme ve görüntüleme için:</span><span class="sxs-lookup"><span data-stu-id="7ecc1-351">Add the following code to the `ClassifyImages()` method for the predictions and to convert the `predictions` `IDataView` into an `IEnumerable` for pairing and display:</span></span>

[!code-csharp[Predict](../../../samples/machine-learning/tutorials/TransferLearningTF/Program.cs#Predict)]

<span data-ttu-id="7ecc1-352">Eşleştirebilir ve Öngörüler ve test görüntü verilerini görüntülemek için çağırmak için aşağıdaki kodu ekleyin. `PairAndDisplayResults()` sonraki satırı olarak daha önce oluşturduğunuz yöntemi `ClassifyImages()` yöntemi:</span><span class="sxs-lookup"><span data-stu-id="7ecc1-352">To pair and display your test image data and predictions, add the following code to call the `PairAndDisplayResults()` method previously created as the next line in the `ClassifyImages()` method:</span></span>

[!code-csharp[CallPairAndDisplayResults2](../../../samples/machine-learning/tutorials/TransferLearningTF/Program.cs#CallPairAndDisplayResults2)]

## <a name="classify-a-single-image-with-a-loaded-model"></a><span data-ttu-id="7ecc1-353">Yüklenen bir model ile tek bir görüntü sınıflandırma</span><span class="sxs-lookup"><span data-stu-id="7ecc1-353">Classify a single image with a loaded model</span></span>

<span data-ttu-id="7ecc1-354">Aşağıdaki çağrısı ekleyin `ClassifySingleImage()` yöntemi sonraki kod satırı olarak `Main` yöntemi:</span><span class="sxs-lookup"><span data-stu-id="7ecc1-354">Add the following call to the `ClassifySingleImage()` method as the next line of code in the `Main` method:</span></span>

[!code-csharp[CallClassifySingleImage](../../../samples/machine-learning/tutorials/TransferLearningTF/Program.cs#CallClassifySingleImage)]

<span data-ttu-id="7ecc1-355">`ClassifyImages()` Yöntemi aşağıdaki görevleri yürütür:</span><span class="sxs-lookup"><span data-stu-id="7ecc1-355">The `ClassifyImages()` method executes the following tasks:</span></span>

* <span data-ttu-id="7ecc1-356">Modeli yükler.</span><span class="sxs-lookup"><span data-stu-id="7ecc1-356">Loads the model.</span></span>
* <span data-ttu-id="7ecc1-357">Yükleri bir `ImageData` örneği.</span><span class="sxs-lookup"><span data-stu-id="7ecc1-357">Loads an `ImageData` instance.</span></span>
* <span data-ttu-id="7ecc1-358">Test verileri temel alan görüntü sınıflandırması tahmin eder.</span><span class="sxs-lookup"><span data-stu-id="7ecc1-358">Predicts image classification based on test data.</span></span>

<span data-ttu-id="7ecc1-359">Oluşturma `ClassifySingleImage()` yöntemi hemen sonrasına `ClassifyImages()` yöntemi ve hemen önce `PairAndDisplayResults()` yöntemi, aşağıdaki kodu kullanarak:</span><span class="sxs-lookup"><span data-stu-id="7ecc1-359">Create the `ClassifySingleImage()` method, just after the `ClassifyImages()` method and just before the `PairAndDisplayResults()` method, using the following code:</span></span>

```csharp
public static void ClassifySingleImage(MLContext mlContext, string imagePath, string outputModelLocation)
{

}
```

<span data-ttu-id="7ecc1-360">İlk olarak, aşağıdaki kod ile daha önce kaydettiğiniz model yüklenemiyor:</span><span class="sxs-lookup"><span data-stu-id="7ecc1-360">First, load the model that you saved previously with the following code:</span></span>

[!code-csharp[LoadModel2](../../../samples/machine-learning/tutorials/TransferLearningTF/Program.cs#LoadModel2)]

<span data-ttu-id="7ecc1-361">Oluşturma bir `ImageData` tek tam yol ve görüntü dosya adı içeren sınıf `ImagePath`.</span><span class="sxs-lookup"><span data-stu-id="7ecc1-361">Create an `ImageData` class that contains the fully qualified path and image file name for the single `ImagePath`.</span></span> <span data-ttu-id="7ecc1-362">Sonraki satırları olarak aşağıdaki kodu ekleyin `ClassifySingleImage()` yöntemi:</span><span class="sxs-lookup"><span data-stu-id="7ecc1-362">Add the following code as the next  lines in the `ClassifySingleImage()` method:</span></span>

[!code-csharp[LoadImageData](../../../samples/machine-learning/tutorials/TransferLearningTF/Program.cs#LoadImageData)]

<span data-ttu-id="7ecc1-363">[PredictionEngine sınıfı](xref:Microsoft.ML.PredictionEngine%602) tahmin verilerini tek bir örneğini gerçekleştirdiği API kolaylığıdır.</span><span class="sxs-lookup"><span data-stu-id="7ecc1-363">The [PredictionEngine class](xref:Microsoft.ML.PredictionEngine%602) is a convenience API that performs a prediction on a single instance of data.</span></span> <span data-ttu-id="7ecc1-364">[Predict()](xref:Microsoft.ML.PredictionEngine%602.Predict%2A) işlevi, tek bir veri sütununu tahmin sağlar.</span><span class="sxs-lookup"><span data-stu-id="7ecc1-364">The [Predict()](xref:Microsoft.ML.PredictionEngine%602.Predict%2A) function makes a prediction on a single column of data.</span></span> <span data-ttu-id="7ecc1-365">Geçirmek `imageData` için `PredictionEngine` resim kategorisi aşağıdaki kodu ekleyerek tahmin etmek için `ClassifySingleImage()`:</span><span class="sxs-lookup"><span data-stu-id="7ecc1-365">Pass `imageData` to the `PredictionEngine` to predict the image category by adding the following code to `ClassifySingleImage()`:</span></span>

[!code-csharp[PredictSingle](../../../samples/machine-learning/tutorials/TransferLearningTF/Program.cs#PredictSingle)]

<span data-ttu-id="7ecc1-366">Sonraki kod satırı olarak tahmin sonucu görüntülemek `ClassifySingleImage()` yöntemi:</span><span class="sxs-lookup"><span data-stu-id="7ecc1-366">Display the prediction result as the next line of code in the `ClassifySingleImage()` method:</span></span>

[!code-csharp[DisplayPrediction](../../../samples/machine-learning/tutorials/TransferLearningTF/Program.cs#DisplayPrediction)]

## <a name="results"></a><span data-ttu-id="7ecc1-367">Sonuçlar</span><span class="sxs-lookup"><span data-stu-id="7ecc1-367">Results</span></span>

<span data-ttu-id="7ecc1-368">Önceki adımları tamamladıktan sonra Konsol uygulamanızı (Ctrl + F5) çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="7ecc1-368">After following the previous steps, run your console app (Ctrl + F5).</span></span> <span data-ttu-id="7ecc1-369">Sonuçlarınız aşağıdaki çıktıya benzer olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="7ecc1-369">Your results should be similar to the following output.</span></span>  <span data-ttu-id="7ecc1-370">Uyarı veya işlem iletileri görebilirsiniz, ancak bu iletiler anlaşılması için aşağıdaki sonuçları kaldırılmış olan.</span><span class="sxs-lookup"><span data-stu-id="7ecc1-370">You may see warnings or processing messages, but these messages have been removed from the following results for clarity.</span></span>

```console
=============== Training classification model ===============
Image: broccoli.jpg predicted as: food with score: 0.976743
Image: pizza.jpg predicted as: food with score: 0.9751652
Image: pizza2.jpg predicted as: food with score: 0.9660203
Image: teddy2.jpg predicted as: toy with score: 0.9748783
Image: teddy3.jpg predicted as: toy with score: 0.9829691
Image: teddy4.jpg predicted as: toy with score: 0.9868168
Image: toaster.jpg predicted as: appliance with score: 0.9769174
Image: toaster2.png predicted as: appliance with score: 0.9800823
=============== Classification metrics ===============
LogLoss is: 0.0228266745633507
PerClassLogLoss is: 0.0277501705149937 , 0.0186303530571291 , 0.0217359128952187
=============== Save model to local file ===============
Model saved: C:\Tutorials\TransferLearningTF\bin\Debug\netcoreapp2.2\assets\outputs\imageClassifier.zip
=============== Loading model ===============
Model loaded: C:\Tutorials\TransferLearningTF\bin\Debug\netcoreapp2.2\assets\outputs\imageClassifier.zip
=============== Making classifications ===============
Image: broccoli.png predicted as: food with score: 0.905548
Image: pizza3.jpg predicted as: food with score: 0.9709008
Image: teddy6.jpg predicted as: toy with score: 0.9750155
=============== Loading model ===============
Model loaded: C:\Tutorials\TransferLearningTF\bin\Debug\netcoreapp2.2\assets\outputs\imageClassifier.zip
=============== Making single image classification ===============
Image: toaster3.jpg predicted as: appliance with score: 0.9625379
Press any key to continue . . .
```

<span data-ttu-id="7ecc1-371">Tebrikler!</span><span class="sxs-lookup"><span data-stu-id="7ecc1-371">Congratulations!</span></span> <span data-ttu-id="7ecc1-372">Şimdi başarıyla bir makine öğrenme modelinin görüntü sınıflandırması için önceden eğitilmiş yeniden kullanarak derlediğiniz `TensorFlow` ML.NET içindeki model.</span><span class="sxs-lookup"><span data-stu-id="7ecc1-372">You've now successfully built a machine learning model for image classification by reusing a pre-trained `TensorFlow` model in ML.NET.</span></span>

<span data-ttu-id="7ecc1-373">Bu öğreticide kaynak kodunu bulabilirsiniz [dotnet/samples](https://github.com/dotnet/samples/tree/master/machine-learning/tutorials/TransferLearningTF) depo.</span><span class="sxs-lookup"><span data-stu-id="7ecc1-373">You can find the source code for this tutorial at the [dotnet/samples](https://github.com/dotnet/samples/tree/master/machine-learning/tutorials/TransferLearningTF) repository.</span></span>

<span data-ttu-id="7ecc1-374">Bu öğreticide, şunların nasıl yapıldığını öğrendiniz:</span><span class="sxs-lookup"><span data-stu-id="7ecc1-374">In this tutorial, you learned how to:</span></span>
> [!div class="checklist"]
> * <span data-ttu-id="7ecc1-375">Sorunu anlama</span><span class="sxs-lookup"><span data-stu-id="7ecc1-375">Understand the problem</span></span>
> * <span data-ttu-id="7ecc1-376">Yeniden kullanmak ve önceden eğitilmiş bir modeli ayarlama</span><span class="sxs-lookup"><span data-stu-id="7ecc1-376">Reuse and tune the pre-trained model</span></span>
> * <span data-ttu-id="7ecc1-377">Yüklenen bir model ile görüntü sınıflandırma</span><span class="sxs-lookup"><span data-stu-id="7ecc1-377">Classify images with a loaded model</span></span>

<span data-ttu-id="7ecc1-378">Bir genişletilmiş görüntü sınıflandırma örnek keşfetmek için Machine Learning örnekleri GitHub havuzuna göz atın.</span><span class="sxs-lookup"><span data-stu-id="7ecc1-378">Check out the Machine Learning samples GitHub repository to explore an expanded image classification sample.</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="7ecc1-379">DotNet/machinelearning-samples GitHub deposu</span><span class="sxs-lookup"><span data-stu-id="7ecc1-379">dotnet/machinelearning-samples GitHub repository</span></span>](https://github.com/dotnet/machinelearning/)