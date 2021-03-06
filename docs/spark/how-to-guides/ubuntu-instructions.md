---
title: Ubuntu'da Apache Spark uygulaması için bir .NET oluşturma
description: Ubuntu'da Apache Spark uygulaması için .NET'inizi nasıl oluşturacağınız hakkında bilgi edinin
ms.date: 01/29/2020
ms.topic: conceptual
ms.custom: mvc,how-to
ms.openlocfilehash: 6dd6f60bb89a51c47fe17182fc47de818cd00b80
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/15/2020
ms.locfileid: "79187565"
---
# <a name="learn-how-to-build-your-net-for-apache-spark-application-on-ubuntu"></a>Ubuntu'da Apache Spark uygulaması için .NET'inizi nasıl oluşturacağınız hakkında bilgi edinin

Bu makalede, Ubuntu'da Apache Spark uygulamaları için .NET'inizi nasıl oluşturabileceğinizöğretilir.

## <a name="prerequisites"></a>Önkoşullar

Aşağıdaki ön koşulların tümüne zaten sahipseniz, [yapı](#build) adımlarına atlayın.

1. .NET **[Core 2.1 SDK](https://dotnet.microsoft.com/download/dotnet-core/2.1)** veya **[.NET Core 3.1 SDK'yı](https://dotnet.microsoft.com/download/dotnet-core/3.1)** `dotnet` indirin ve kurun - SDK'yı yüklemek araç zincirini yolunuza ekler.  .NET Core 2.1, 2.2 ve 3.1 desteklenir.

2. **[OpenJDK 8'i](https://openjdk.java.net/install/)** yükleyin.

   - Aşağıdaki komutu kullanabilirsiniz:

   ```bash
   sudo apt install openjdk-8-jdk
   ```

   * Komut satırınızdan çalıştırabileceğinizi `java` doğrulayın.

      Örnek java sürüm çıktısı:

      ```bash
      openjdk version "1.8.0_191"
      OpenJDK Runtime Environment (build 1.8.0_191-8u191-b12-2ubuntu0.18.04.1-b12)
      OpenJDK 64-Bit Server VM (build 25.191-b12, mixed mode)
      ```

   * Zaten birden çok OpenJDK sürümü yüklüyse ve OpenJDK 8'i seçmek istiyorsanız, aşağıdaki komutu kullanın:

      ```bash
      sudo update-alternatives --config java
      ```

3. **[Apache Maven 3.6.0+](https://maven.apache.org/download.cgi)** yükleyin.

   * Şu komutu çalıştırın:

      ```bash
      mkdir -p ~/bin/maven
      cd ~/bin/maven
      wget https://www-us.apache.org/dist/maven/maven-3/3.6.0/binaries/apache-maven-3.6.0-bin.tar.gz
      tar -xvzf apache-maven-3.6.0-bin.tar.gz
      ln -s apache-maven-3.6.0 current
      export M2_HOME=~/bin/maven/current
      export PATH=${M2_HOME}/bin:${PATH}
      source ~/.bashrc
      ```

       Terminalinizi kapattığınızda bu ortam değişkenlerinin kaybolacağını unutmayın. Değişikliklerin kalıcı olmasını istiyorsanız, `export` satırları dosyanıza `~/.bashrc` ekleyin.

   * Komut satırınızdan çalıştırabildiğinizi `mvn` doğrulayın

       Örnek mvn-sürüm çıktısı:

       ```
       Apache Maven 3.6.0 (97c98ec64a1fdfee7767ce5ffb20918da4f719f3; 2018-10-24T18:41:47Z)
       Maven home: ~/bin/apache-maven-3.6.0
       Java version: 1.8.0_191, vendor: Oracle Corporation, runtime: /usr/lib/jvm/java-8-openjdk-amd64/jre
       Default locale: en, platform encoding: UTF-8
       OS name: "linux", version: "4.4.0-17763-microsoft", arch: "amd64", family: "unix"
       ```

4. **[Apache Spark 2.3+ yükleyin.](https://spark.apache.org/downloads.html)**
[Apache Spark 2.3+](https://spark.apache.org/downloads.html) indirin ve yerel bir klasöre `~/bin/spark-2.3.2-bin-hadoop2.7`ayıklayın (örn. ). (Desteklenen kıvılcım versiyonları 2.3.*, 2.4.0, 2.4.1, 2.4.3 ve 2.4.4'tür)

   ```bash
   tar -xvzf /path/to/spark-2.3.2-bin-hadoop2.7.tgz -C ~/bin/spark-2.3.2-bin-hadoop2.7
   ```

   * Gerekli [ortam değişkenlerini](https://www.java.com/en/download/help/path.xml) `SPARK_HOME` (örn. `~/bin/spark-2.3.2-bin-hadoop2.7/`) ve `PATH` (örn. `$SPARK_HOME/bin:$PATH`

      ```bash
      export SPARK_HOME=~/bin/spark-2.3.2-hadoop2.7
      export PATH="$SPARK_HOME/bin:$PATH"
      source ~/.bashrc
      ```

      Terminalinizi kapattığınızda bu ortam değişkenlerinin kaybolacağını unutmayın. Değişikliklerin kalıcı olmasını istiyorsanız, `export` satırları dosyanıza `~/.bashrc` ekleyin.

   * Komut satırınızdan çalıştırabileceğinizi `spark-shell` doğrulayın.

      Örnek konsol çıkışı:

      ```
      Welcome to
            ____              __
           / __/__  ___ _____/ /__
          _\ \/ _ \/ _ `/ __/  '_/
         /___/ .__/\_,_/_/ /_/\_\   version 2.3.2
            /_/

      Using Scala version 2.11.8 (Java HotSpot(TM) 64-Bit Server VM, Java 1.8.0_201)
      Type in expressions to have them evaluated.
      Type :help for more information.

      scala> sc
      res0: org.apache.spark.SparkContext = org.apache.spark.SparkContext@6eaa6b0c
      ```

Bir sonraki bölüme `dotnet`geçmeden `java` `mvn`önce `spark-shell` komut satırınızdan , , , çalıştırabildiğinizden emin olun. Daha iyi bir yol olduğunu mu düşünüyorsun? Lütfen [bir sorun açın](https://github.com/dotnet/spark/issues) ve katkıda bulunmakiçin çekinmeyin.

## <a name="build"></a>Oluşturma

Bu kılavuzun geri kalanı için, apache Spark deposu için .NET'i makinenize klonlamış olmanız `~/dotnet.spark/`gerekir.

```bash
git clone https://github.com/dotnet/spark.git ~/dotnet.spark
```

### <a name="build-net-for-spark-scala-extensions-layer"></a>Kıvılcım Scala uzantıları katmanı için .NET oluştur

Bir .NET başvurusu yaptığınızda, .NET for Apache Spark,Scala'da yazılı olan ve Apache Spark'a isteklerinizi nasıl işleyeceğini bildiren gerekli bir mantığa sahiptir (örneğin, yeni bir Kıvılcım Oturumu oluşturma isteği, .NET tarafından JVM tarafına veri aktarımı isteği vb.). Bu mantık [Apache Spark Scala Kaynak Kodu için .NET](https://github.com/dotnet/spark/tree/master/src/scala)bulunabilir.

Bir sonraki adım Apache Spark Scala uzantısı katmanı için .NET oluşturmaktır:

```bash
cd src/scala
mvn clean package
```

Desteklenen Spark sürümleri için oluşturulan JAR'ları görmelisiniz:

* `microsoft-spark-2.3.x/target/microsoft-spark-2.3.x-<version>.jar`
* `microsoft-spark-2.4.x/target/microsoft-spark-2.4.x-<version>.jar`

### <a name="build-net-sample-applications-using-net-core-cli"></a>.NET Core CLI kullanarak .NET örnek uygulamalar oluşturun

Bu bölümde, Apache Spark için .NET [için örnek uygulamaların](https://github.com/dotnet/spark/tree/master/examples) nasıl oluşturulabildiği açıklanmaktadır. Bu adımlar, Kıvılcım uygulaması için herhangi bir .NET için genel oluşturma işlemini anlamada yardımcı olacaktır.

1. İşçiyi oluşturun:

   ```dotnetcli
   cd ~/dotnet.spark/src/csharp/Microsoft.Spark.Worker/
   dotnet publish -f netcoreapp2.1 -r ubuntu.18.04-x64
   ```

   Örnek konsol çıkışı:

   ```bash
   user@machine:/home/user/dotnet.spark/src/csharp/Microsoft.Spark.Worker$ dotnet publish -f netcoreapp2.1 -r ubuntu.18.04-x64
   Microsoft (R) Build Engine version 16.0.462+g62fb89029d for .NET Core
   Copyright (C) Microsoft Corporation. All rights reserved.

      Restore completed in 36.03 ms for /home/user/dotnet.spark/src/csharp/Microsoft.Spark.Worker/Microsoft.Spark.Worker.csproj.
      Restore completed in 35.94 ms for /home/user/dotnet.spark/src/csharp/Microsoft.Spark/Microsoft.Spark.csproj.
      Microsoft.Spark -> /home/user/dotnet.spark/artifacts/bin/Microsoft.Spark/Debug/netstandard2.0/Microsoft.Spark.dll
      Microsoft.Spark.Worker -> /home/user/dotnet.spark/artifacts/bin/Microsoft.Spark.Worker/Debug/netcoreapp2.1/ubuntu.18.04-x64/Microsoft.Spark.Worker.dll
      Microsoft.Spark.Worker -> /home/user/dotnet.spark/artifacts/bin/Microsoft.Spark.Worker/Debug/netcoreapp2.1/ubuntu.18.04-x64/publish/
   ```

2. Örnekleri oluşturun:

   ```dotnetcli
   cd ~/dotnet.spark/examples/Microsoft.Spark.CSharp.Examples/
   dotnet publish -f netcoreapp2.1 -r ubuntu.18.04-x64
   ```

   Örnek konsol çıkışı:

   ```bash
   user@machine:/home/user/dotnet.spark/examples/Microsoft.Spark.CSharp.Examples$ dotnet publish -f netcoreapp2.1 -r ubuntu.18.04-x64
   Microsoft (R) Build Engine version 16.0.462+g62fb89029d for .NET Core
   Copyright (C) Microsoft Corporation. All rights reserved.

      Restore completed in 37.11 ms for /home/user/dotnet.spark/src/csharp/Microsoft.Spark/Microsoft.Spark.csproj.
      Restore completed in 281.63 ms for /home/user/dotnet.spark/examples/Microsoft.Spark.CSharp.Examples/Microsoft.Spark.CSharp.Examples.csproj.
      Microsoft.Spark -> /home/user/dotnet.spark/artifacts/bin/Microsoft.Spark/Debug/netstandard2.0/Microsoft.Spark.dll
      Microsoft.Spark.CSharp.Examples -> /home/user/dotnet.spark/artifacts/bin/Microsoft.Spark.CSharp.Examples/Debug/netcoreapp2.1/ubuntu.18.04-x64/Microsoft.Spark.CSharp.Examples.dll
      Microsoft.Spark.CSharp.Examples -> /home/user/dotnet.spark/artifacts/bin/Microsoft.Spark.CSharp.Examples/Debug/netcoreapp2.1/ubuntu.18.04-x64/publish/
   ```  

## <a name="run-the-net-for-spark-sample-applications"></a>Kıvılcım örnek uygulamaları için .NET'i çalıştırın

Örnekleri oluşturduğunuzda ,.NET `spark-submit` Core uygulamalarınızı göndermek için kullanabilirsiniz. [Önkoşullar](#prerequisites) bölümünü takip ettiğinizden ve Apache Spark'ı yüklediğinizden emin olun.

1. `Microsoft.Spark.Worker` Veya `DOTNET_WORKER_DIR` `PATH` ortam değişkenini ikilinin oluşturulduğu yolu içerecek şekilde ayarlayın `~/dotnet.spark/artifacts/bin/Microsoft.Spark.Worker/Debug/netcoreapp2.1/ubuntu.18.04-x64/publish`(örn.. ).

   ```bash
   export DOTNET_WORKER_DIR=~/dotnet.spark/artifacts/bin/Microsoft.Spark.Worker/Debug/netcoreapp2.1/ubuntu.18.04-x64/publish
   ```

2. Bir terminal açın ve uygulama ikilinizin oluşturulduğu dizine gidin `~/dotnet.spark/artifacts/bin/Microsoft.Spark.CSharp.Examples/Debug/netcoreapp2.1/ubuntu.18.04-x64/publish`(örn.

   ```bash
   cd ~/dotnet.spark/artifacts/bin/Microsoft.Spark.CSharp.Examples/Debug/netcoreapp2.1/ubuntu.18.04-x64/publish
   ```

3. Uygulamanızı çalıştırmak temel yapıyı izler:

   ```bash
   spark-submit \
     [--jars <any-jars-your-app-is-dependent-on>] \
     --class org.apache.spark.deploy.dotnet.DotnetRunner \
     --master local \
     <path-to-microsoft-spark-jar> \
     <path-to-your-app-binary> <argument(s)-to-your-app>
   ```

   Çalıştırabileceğiniz bazı örnekler şunlardır:

   * **[Microsoft.Spark.Examples.Sql.Batch.Basic](https://github.com/dotnet/spark/blob/master/examples/Microsoft.Spark.CSharp.Examples/Sql/Batch/Basic.cs)**

      ```bash
      spark-submit \
      --class org.apache.spark.deploy.dotnet.DotnetRunner \
      --master local \
      ~/dotnet.spark/src/scala/microsoft-spark-<version>/target/microsoft-spark-<version>.jar \
      Microsoft.Spark.CSharp.Examples Sql.Batch.Basic $SPARK_HOME/examples/src/main/resources/people.json
      ```

   * **[Microsoft.Spark.Examples.Sql.Streaming.StructuredNetworkWordCount](https://github.com/dotnet/spark/blob/master/examples/Microsoft.Spark.CSharp.Examples/Sql/Streaming/StructuredNetworkWordCount.cs)**

      ```bash
      spark-submit \
      --class org.apache.spark.deploy.dotnet.DotnetRunner \
      --master local \
      ~/dotnet.spark/src/scala/microsoft-spark-<version>/target/microsoft-spark-<version>.jar \
      Microsoft.Spark.CSharp.Examples Sql.Streaming.StructuredNetworkWordCount localhost 9999
      ```

   * **[Microsoft.Spark.Examples.Sql.Streaming.StructuredKafkaWordCount (maven erişilebilir)](https://github.com/dotnet/spark/blob/master/examples/Microsoft.Spark.CSharp.Examples/Sql/Streaming/StructuredKafkaWordCount.cs)**

      ```bash
      spark-submit \
      --packages org.apache.spark:spark-sql-kafka-0-10_2.11:2.3.2 \
      --class org.apache.spark.deploy.dotnet.DotnetRunner \
      --master local \
      ~/dotnet.spark/src/scala/microsoft-spark-<version>/target/microsoft-spark-<version>.jar \
      Microsoft.Spark.CSharp.Examples Sql.Streaming.StructuredKafkaWordCount localhost:9092 subscribe test
      ```

   * **[Microsoft.Spark.Examples.Sql.Streaming.StructuredKafkaWordCount (kavanoz lar sağlandı)](https://github.com/dotnet/spark/blob/master/examples/Microsoft.Spark.CSharp.Examples/Sql/Streaming/StructuredKafkaWordCount.cs)**

      ```bash
      spark-submit \
      --jars path/to/net.jpountz.lz4/lz4-1.3.0.jar,path/to/org.apache.kafka/kafka-clients-0.10.0.1.jar,path/to/org.apache.spark/spark-sql-kafka-0-10_2.11-2.3.2.jar,`path/to/org.slf4j/slf4j-api-1.7.6.jar,path/to/org.spark-project.spark/unused-1.0.0.jar,path/to/org.xerial.snappy/snappy-java-1.1.2.6.jar \
      --class org.apache.spark.deploy.dotnet.DotnetRunner \
      --master local \
      ~/dotnet.spark/src/scala/microsoft-spark-<version>/target/microsoft-spark-<version>.jar \
      Microsoft.Spark.CSharp.Examples Sql.Streaming.StructuredKafkaWordCount localhost:9092 subscribe test
       ```
