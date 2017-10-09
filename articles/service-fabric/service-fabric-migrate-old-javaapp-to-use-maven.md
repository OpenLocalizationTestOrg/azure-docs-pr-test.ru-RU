---
title: "aaaMigrate из пакета SDK для Java tooMaven - обновление старых приложений Java Azure Service Fabric toouse Maven | Документы Microsoft"
description: "Обновление hello старых приложений Java используемых hello toouse пакет Service Fabric Java SDK зависимости службы структуры Java toofetch из Maven. После завершения этой установки имеющиеся приложения Java будет может toobuild."
services: service-fabric
documentationcenter: java
author: sayantancs
manager: timlt
editor: 
ms.assetid: bf84458f-4b87-4de1-9844-19909e368deb
ms.service: service-fabric
ms.devlang: java
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/23/2017
ms.author: saysa
ms.openlocfilehash: 11b979facd7b3865141a6d3a035a6021dd06ca0c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="update-your-previous-java-service-fabric-application-toofetch-java-libraries-from-maven"></a><span data-ttu-id="c2cba-104">Обновление предыдущих Java Service Fabric приложения toofetch Java библиотеками Maven</span><span class="sxs-lookup"><span data-stu-id="c2cba-104">Update your previous Java Service Fabric application toofetch Java libraries from Maven</span></span>
<span data-ttu-id="c2cba-105">Недавно были удалены двоичных файлов службы структуры Java hello Service Fabric Java SDK tooMaven, на котором размещается.</span><span class="sxs-lookup"><span data-stu-id="c2cba-105">We have recently moved Service Fabric Java binaries from hello Service Fabric Java SDK tooMaven hosting.</span></span> <span data-ttu-id="c2cba-106">Теперь вы можете использовать **mavencentral** toofetch hello последнюю Java структуры службы зависимостей.</span><span class="sxs-lookup"><span data-stu-id="c2cba-106">Now you can use **mavencentral** toofetch hello latest Service Fabric Java dependencies.</span></span> <span data-ttu-id="c2cba-107">Это краткое позволяет обновить существующие приложения Java, ранее созданные toobe используются Service Fabric Java SDK, с помощью либо Yeoman шаблона или Eclipse, совместимы с hello построения на основе Maven toobe.</span><span class="sxs-lookup"><span data-stu-id="c2cba-107">This quick-start helps you update your existing Java applications, which you earlier created toobe used with Service Fabric Java SDK, using either Yeoman template or Eclipse, toobe compatible with hello Maven based build.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c2cba-108">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="c2cba-108">Prerequisites</span></span>
1. <span data-ttu-id="c2cba-109">Сначала необходимо toouninstall hello существующего пакета SDK для Java.</span><span class="sxs-lookup"><span data-stu-id="c2cba-109">First you need toouninstall hello existing Java SDK.</span></span>

  ```bash
  sudo dpkg -r servicefabricsdkjava
  ```
2. <span data-ttu-id="c2cba-110">Следующие службы структуры CLI последней установки hello hello действия, упомянутые [здесь](service-fabric-cli.md).</span><span class="sxs-lookup"><span data-stu-id="c2cba-110">Install hello latest Service Fabric CLI following hello steps mentioned [here](service-fabric-cli.md).</span></span>

3. <span data-ttu-id="c2cba-111">toobuild и hello приложений Java структуры службы, необходимо tooensure наличии JDK 1.8 и установить Gradle.</span><span class="sxs-lookup"><span data-stu-id="c2cba-111">toobuild and work on hello Service Fabric Java applications, you need tooensure that you have JDK 1.8 and Gradle installed.</span></span> <span data-ttu-id="c2cba-112">Если еще не установлен, можно запустить hello следующие tooinstall JDK 1.8 (openjdk 8 jdk) и Gradle -</span><span class="sxs-lookup"><span data-stu-id="c2cba-112">If not yet installed, you can run hello following tooinstall JDK 1.8 (openjdk-8-jdk) and Gradle -</span></span>

 ```bash
 sudo apt-get install openjdk-8-jdk-headless
 sudo apt-get install gradle
 ```
4. <span data-ttu-id="c2cba-113">Сценарии установки и удаления обновления hello из вашего приложения toouse hello новый CLI структуры службы, упомянутых действий hello [здесь](service-fabric-application-lifecycle-sfctl.md).</span><span class="sxs-lookup"><span data-stu-id="c2cba-113">Update hello install/uninstall scripts of your application toouse hello new Service Fabric CLI following hello steps mentioned [here](service-fabric-application-lifecycle-sfctl.md).</span></span> <span data-ttu-id="c2cba-114">Можно ссылаться Приступая к работе tooour [примеры](https://github.com/Azure-Samples/service-fabric-java-getting-started) для ссылки.</span><span class="sxs-lookup"><span data-stu-id="c2cba-114">You can refer tooour getting-started [examples](https://github.com/Azure-Samples/service-fabric-java-getting-started) for reference.</span></span>

>[!TIP]
> <span data-ttu-id="c2cba-115">После удаления hello Service Fabric Java SDK Yeoman не будет работать.</span><span class="sxs-lookup"><span data-stu-id="c2cba-115">After uninstalling hello Service Fabric Java SDK, Yeoman will not work.</span></span> <span data-ttu-id="c2cba-116">Выполните hello предварительным [здесь](service-fabric-create-your-first-linux-application-with-java.md) toohave Yeoman структуры службы Java генератор шаблона вверх и работа.</span><span class="sxs-lookup"><span data-stu-id="c2cba-116">Follow hello Prerequisites mentioned [here](service-fabric-create-your-first-linux-application-with-java.md) toohave Service Fabric Yeoman Java template generator up and working.</span></span>

## <a name="service-fabric-java-libraries-on-maven"></a><span data-ttu-id="c2cba-117">Библиотеки Java для Service Fabric в Maven</span><span class="sxs-lookup"><span data-stu-id="c2cba-117">Service Fabric Java libraries on Maven</span></span>
<span data-ttu-id="c2cba-118">Библиотеки Java для Service Fabric размещены в Maven.</span><span class="sxs-lookup"><span data-stu-id="c2cba-118">Service Fabric Java libraries have been hosted in Maven.</span></span> <span data-ttu-id="c2cba-119">Можно добавить зависимости hello в hello ``pom.xml`` или ``build.gradle`` библиотеки Service Fabric Java toouse проекты из **mavenCentral**.</span><span class="sxs-lookup"><span data-stu-id="c2cba-119">You can add hello dependencies in hello ``pom.xml`` or ``build.gradle`` of your projects toouse Service Fabric Java libraries from **mavenCentral**.</span></span>

### <a name="actors"></a><span data-ttu-id="c2cba-120">Субъекты</span><span class="sxs-lookup"><span data-stu-id="c2cba-120">Actors</span></span>

<span data-ttu-id="c2cba-121">Поддержка субъекта Service Fabric Reliable Actors для приложения.</span><span class="sxs-lookup"><span data-stu-id="c2cba-121">Service Fabric Reliable Actor support for your application.</span></span>

  ```XML
  <dependency>
      <groupId>com.microsoft.servicefabric</groupId>
      <artifactId>sf-actors-preview</artifactId>
      <version>0.10.0</version>
  </dependency>
  ```

  ```gradle
  repositories {
      mavenCentral()
  }
  dependencies {
      compile 'com.microsoft.servicefabric:sf-actors-preview:0.10.0'
  }
  ```

### <a name="services"></a><span data-ttu-id="c2cba-122">Службы</span><span class="sxs-lookup"><span data-stu-id="c2cba-122">Services</span></span>

<span data-ttu-id="c2cba-123">Поддержка службы без отслеживания состояния Service Fabric для приложения.</span><span class="sxs-lookup"><span data-stu-id="c2cba-123">Service Fabric Stateless Service support for your application.</span></span>

  ```XML
  <dependency>
      <groupId>com.microsoft.servicefabric</groupId>
      <artifactId>sf-services-preview</artifactId>
      <version>0.10.0</version>
  </dependency>
  ```

  ```gradle
  repositories {
      mavenCentral()
  }
  dependencies {
      compile 'com.microsoft.servicefabric:sf-services-preview:0.10.0'
  }
  ```

### <a name="others"></a><span data-ttu-id="c2cba-124">Прочее</span><span class="sxs-lookup"><span data-stu-id="c2cba-124">Others</span></span>
#### <a name="transport"></a><span data-ttu-id="c2cba-125">Транспортировка</span><span class="sxs-lookup"><span data-stu-id="c2cba-125">Transport</span></span>

<span data-ttu-id="c2cba-126">Поддержка транспортного уровня для приложения Java в Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="c2cba-126">Transport layer support for Service Fabric Java application.</span></span> <span data-ttu-id="c2cba-127">Не обязательно tooexplicitly добавлять этот tooyour зависимостей Reliable Actor и приложения служб, без программирования на уровне транспорта hello.</span><span class="sxs-lookup"><span data-stu-id="c2cba-127">You do not need tooexplicitly add this dependency tooyour Reliable Actor or Service applications, unless you program at hello transport layer.</span></span>

  ```XML
  <dependency>
      <groupId>com.microsoft.servicefabric</groupId>
      <artifactId>sf-transport-preview</artifactId>
      <version>0.10.0</version>
  </dependency>
  ```

  ```gradle
  repositories {
      mavenCentral()
  }
  dependencies {
      compile 'com.microsoft.servicefabric:sf-transport-preview:0.10.0'
  }
  ```

#### <a name="fabric-support"></a><span data-ttu-id="c2cba-128">Поддержка Service Fabric</span><span class="sxs-lookup"><span data-stu-id="c2cba-128">Fabric support</span></span>

<span data-ttu-id="c2cba-129">Поддержка уровня системы для службы структуры, говорящий toonative среда выполнения Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="c2cba-129">System level support for Service Fabric, which talks toonative Service Fabric runtime.</span></span> <span data-ttu-id="c2cba-130">Нет необходимости tooexplicitly добавьте эту зависимость tooyour Reliable Actor или приложений службы.</span><span class="sxs-lookup"><span data-stu-id="c2cba-130">You do not need tooexplicitly add this dependency tooyour Reliable Actor or Service applications.</span></span> <span data-ttu-id="c2cba-131">Это возвращает автоматически получены из Maven, при включении hello другие зависимости выше.</span><span class="sxs-lookup"><span data-stu-id="c2cba-131">This gets fetched automatically from Maven, when you include hello other dependencies above.</span></span>

  ```XML
  <dependency>
      <groupId>com.microsoft.servicefabric</groupId>
      <artifactId>sf-preview</artifactId>
      <version>0.10.0</version>
  </dependency>
  ```

  ```gradle
  repositories {
      mavenCentral()
  }
  dependencies {
      compile 'com.microsoft.servicefabric:sf-preview:0.10.0'
  }
  ```


## <a name="migrating-service-fabric-stateless-service"></a><span data-ttu-id="c2cba-132">Миграция службы без отслеживания состояния Service Fabric</span><span class="sxs-lookup"><span data-stu-id="c2cba-132">Migrating Service Fabric Stateless Service</span></span>

<span data-ttu-id="c2cba-133">возможности toobuild toobe существующие Service Fabric без сохранения состояния Java службы с помощью Service Fabric зависимостей, выбранные из Maven, требуется tooupdate hello ``build.gradle`` файла внутри hello службы.</span><span class="sxs-lookup"><span data-stu-id="c2cba-133">toobe able toobuild your existing Service Fabric stateless Java service using Service Fabric dependencies fetched from Maven, you need tooupdate hello ``build.gradle`` file inside hello Service.</span></span> <span data-ttu-id="c2cba-134">Ранее он использовать toobe как следующим образом —</span><span class="sxs-lookup"><span data-stu-id="c2cba-134">Previously it used toobe like as follows -</span></span>
```
dependencies {
    compile fileTree(dir: '/opt/microsoft/sdk/servicefabric/java/packages/lib', include: ['*.jar'])
    compile project(':Interface')
}
.
.
.
jar {
    manifest {
    attributes(
                'Main-Class': 'statelessservice.MyStatelessServiceHost',
                "Class-Path": configurations.compile.collect { 'lib/' + it.getName() }.join(' '))
    baseName "MyStateless"
    destinationDir = file('./../MyStatelessApplication/MyStatelessPkg/Code')
}
.
.
.
task copyDeps <<{
    copy {
        from("/opt/microsoft/sdk/servicefabric/java/packages/lib")
        into("./../MyStatelessApplication/MyStatelessPkg/Code/lib")
        include('*.jar')
    }
    copy {
        from("/opt/microsoft/sdk/servicefabric/java/packages/lib")
        into("./../MyStatelessApplication/MyStatelessPkg/Code/lib")
        include('libj*.so')
    }
}
```
<span data-ttu-id="c2cba-135">Теперь hello зависимости hello toofetch из Maven, **обновление** ``build.gradle`` будет иметь соответствующий частей hello следующим -</span><span class="sxs-lookup"><span data-stu-id="c2cba-135">Now, toofetch hello dependencies from Maven, hello **updated** ``build.gradle`` would have hello corresponding parts as follows -</span></span>
```
repositories {
        mavenCentral()
}

configurations {
    azuresf
}

dependencies {
    compile project(':Interface')
    azuresf ('com.microsoft.servicefabric:sf-services-preview:0.10.0')
    compile fileTree(dir: 'lib', include: '*.jar')
}

task explodeDeps(type: Copy, dependsOn:configurations.azuresf) { task ->
    configurations.azuresf.filter { it.toString().contains("native-preview") }.each{
        from zipTree(it)
    }
    configurations.azuresf.filter { !it.toString().contains("native-preview") }.each {
        from it
    }
    into "lib"
    include "libj*.so", "*.jar"
}

compileJava.dependsOn(explodeDeps)
.
.
.
jar {
    manifest {
        def mpath = configurations.compile.collect {'lib/'+it.getName()}.join (' ')
        mpath = mpath + ' ' + configurations.azuresf.collect {'lib/'+it.getName()}.join (' ')
        attributes(
                'Main-Class': 'statelessservice.MyStatelessServiceHost',
                "Class-Path": mpath)
    baseName "MyStateless"
    destinationDir = file('./../MyStatelessApplication/MyStatelessPkg/Code')
   }
}
.
.
.
task copyDeps <<{
    copy {
        from("lib/")
        into("./../MyStatelessApplication/MyStatelessPkg/Code/lib")
        include('*')
    }
}
```
<span data-ttu-id="c2cba-136">Как правило tooget общее представление о как hello создания скрипта выглядит следующим образом для Java службы без отслеживания состояния Service Fabric, образец tooany можно ссылаться из наших примерах, Приступая к работе.</span><span class="sxs-lookup"><span data-stu-id="c2cba-136">In general, tooget an overall idea about how hello build script would look like for a Service Fabric stateless Java service, you can refer tooany sample from our getting-started examples.</span></span> <span data-ttu-id="c2cba-137">Вот hello [build.gradle](https://github.com/Azure-Samples/service-fabric-java-getting-started/blob/master/Services/EchoServer/EchoServer1.0/EchoServerService/build.gradle) EchoServer образец hello.</span><span class="sxs-lookup"><span data-stu-id="c2cba-137">Here is hello [build.gradle](https://github.com/Azure-Samples/service-fabric-java-getting-started/blob/master/Services/EchoServer/EchoServer1.0/EchoServerService/build.gradle) for hello EchoServer sample.</span></span>

## <a name="migrating-service-fabric-actor-service"></a><span data-ttu-id="c2cba-138">Миграция службы субъекта в Service Fabric</span><span class="sxs-lookup"><span data-stu-id="c2cba-138">Migrating Service Fabric Actor Service</span></span>

<span data-ttu-id="c2cba-139">возможности toobuild toobe существующего приложения Java субъекта Service Fabric с помощью Service Fabric зависимостей, выбранные из Maven, требуется tooupdate hello ``build.gradle`` файла внутри пакета интерфейса hello и в пакет службы hello.</span><span class="sxs-lookup"><span data-stu-id="c2cba-139">toobe able toobuild your existing Service Fabric Actor Java application using Service Fabric dependencies fetched from Maven, you need tooupdate hello ``build.gradle`` file inside hello interface package and in hello Service package.</span></span> <span data-ttu-id="c2cba-140">При наличии пакета TestClient необходимо, а также tooupdate.</span><span class="sxs-lookup"><span data-stu-id="c2cba-140">If you have a TestClient package, you need tooupdate that as well.</span></span> <span data-ttu-id="c2cba-141">В этом случае для вашего субъекта ``Myactor``, следующие hello бы hello местах, где требуется tooupdate -</span><span class="sxs-lookup"><span data-stu-id="c2cba-141">So, for your actor ``Myactor``, hello following would be hello places where you need tooupdate -</span></span>
```
./Myactor/build.gradle
./MyactorInterface/build.gradle
./MyactorTestClient/build.gradle
```

#### <a name="updating-build-script-for-hello-interface-project"></a><span data-ttu-id="c2cba-142">Обновление скрипт построения для проекта интерфейса hello</span><span class="sxs-lookup"><span data-stu-id="c2cba-142">Updating build script for hello interface project</span></span>

<span data-ttu-id="c2cba-143">Ранее он использовать toobe как следующим образом —</span><span class="sxs-lookup"><span data-stu-id="c2cba-143">Previously it used toobe like as follows -</span></span>
```
dependencies {
    compile fileTree(dir: '/opt/microsoft/sdk/servicefabric/java/packages/lib', include: ['*.jar'])
}
.
.
```
<span data-ttu-id="c2cba-144">Теперь hello зависимости hello toofetch из Maven, **обновление** ``build.gradle`` будет иметь соответствующий частей hello следующим -</span><span class="sxs-lookup"><span data-stu-id="c2cba-144">Now, toofetch hello dependencies from Maven, hello **updated** ``build.gradle`` would have hello corresponding parts as follows -</span></span>
```
repositories {
    mavenCentral()
}

configurations {
    azuresf
}

dependencies {
    azuresf ('com.microsoft.servicefabric:sf-actors-preview:0.10.0')
    compile fileTree(dir: 'lib', include: '*.jar')
}

task explodeDeps(type: Copy, dependsOn:configurations.azuresf) { task ->
    configurations.azuresf.filter { it.toString().contains("native-preview") }.each{
        from zipTree(it)
    }
    configurations.azuresf.filter { !it.toString().contains("native-preview") }.each {
        from it
    }
    into "lib"
    include "libj*.so", "*.jar"
}

compileJava.dependsOn(explodeDeps)
.
.
```

#### <a name="updating-build-script-for-hello-actor-project"></a><span data-ttu-id="c2cba-145">Обновление скрипт построения для проекта субъекта hello</span><span class="sxs-lookup"><span data-stu-id="c2cba-145">Updating build script for hello actor project</span></span>

<span data-ttu-id="c2cba-146">Ранее он использовать toobe как следующим образом —</span><span class="sxs-lookup"><span data-stu-id="c2cba-146">Previously it used toobe like as follows -</span></span>
```
dependencies {
    compile fileTree(dir: '/opt/microsoft/sdk/servicefabric/java/packages/lib', include: ['*.jar'])
    compile project(':MyactorInterface')
}
.
.
.
jar {
    manifest {
    attributes(
                'Main-Class': 'reliableactor.MyactorHost',
                "Class-Path": configurations.compile.collect { 'lib/' + it.getName() }.join(' '))
      baseName "myactor"
    destinationDir = file('./../myjavaapp/MyactorPkg/Code')
    }
}
.
.
.
task copyDeps<< {
    copy {
        from("/opt/microsoft/sdk/servicefabric/java/packages/lib")
        into("./../myjavaapp/MyactorPkg/Code/lib")
        include('*.jar')
    }
    copy {
        from("/opt/microsoft/sdk/servicefabric/java/packages/lib")
        into("./../myjavaapp/MyactorPkg/Code/lib")
        include('libj*.so')
    }
    copy {
        from("../MyactorInterface/out/lib")
        into("./../myjavaapp/MyactorPkg/Code/lib")
        include('*.jar')
    }
}
```
<span data-ttu-id="c2cba-147">Теперь hello зависимости hello toofetch из Maven, **обновление** ``build.gradle`` будет иметь соответствующий частей hello следующим -</span><span class="sxs-lookup"><span data-stu-id="c2cba-147">Now, toofetch hello dependencies from Maven, hello **updated** ``build.gradle`` would have hello corresponding parts as follows -</span></span>
```
repositories {
    mavenCentral()
}

configurations {
    azuresf
}

dependencies {
    compile project(':MyactorInterface')
    azuresf ('com.microsoft.servicefabric:sf-actors-preview:0.10.0')
    compile fileTree(dir: 'lib', include: '*.jar')
}

task explodeDeps(type: Copy, dependsOn:configurations.azuresf) { task ->
    configurations.azuresf.filter { it.toString().contains("native-preview") }.each{
        from zipTree(it)
    }
    configurations.azuresf.filter { !it.toString().contains("native-preview") }.each {
        from it
    }
    into "lib"
    include "libj*.so", "*.jar"
}

compileJava.dependsOn(explodeDeps)
.
.
.
jar {
    manifest {
        def mpath = configurations.compile.collect {'lib/'+it.getName()}.join (' ')
        mpath = mpath + ' ' + configurations.azuresf.collect {'lib/'+it.getName()}.join (' ')
        attributes(
                'Main-Class': 'reliableactor.MyactorHost',
                "Class-Path": mpath)
    baseName "myactor"
    destinationDir = file('../myjavaapp/MyactorPkg/Code')}
 }
.
.
.
task copyDeps<< {
      copy {
              from("lib/")
              into("../myjavaapp/MyactorPkg/Code/lib")
              include('*')
      }
      copy {
              from("../MyactorInterface/out/lib")
              into("../myjavaapp/MyactorPkg/Code/lib")
              include('*.jar')
      }
}
```

#### <a name="updating-build-script-for-hello-test-client-project"></a><span data-ttu-id="c2cba-148">Обновление скрипт построения для проекта клиента hello теста</span><span class="sxs-lookup"><span data-stu-id="c2cba-148">Updating build script for hello test client project</span></span>

<span data-ttu-id="c2cba-149">Здесь изменения, аналогичные toohello изменения, описанные в предыдущем разделе, то есть проект hello субъекта.</span><span class="sxs-lookup"><span data-stu-id="c2cba-149">Changes here are similar toohello changes discussed in previous section, that is, hello actor project.</span></span> <span data-ttu-id="c2cba-150">Ранее hello toobe сценарий, используемый как следующим - Gradle</span><span class="sxs-lookup"><span data-stu-id="c2cba-150">Previously hello Gradle script used toobe like as follows -</span></span>
```
dependencies {
    compile fileTree(dir: '/opt/microsoft/sdk/servicefabric/java/packages/lib', include: ['*.jar'])
      compile project(':MyactorInterface')
}
.
.
.
jar
{
    manifest {
    attributes(
        'Main-Class': 'reliableactor.test.MyactorTestClient',
        "Class-Path": configurations.compile.collect { 'lib/' + it.getName() }.join(' '))
    }
    baseName "myactor-test"
  destinationDir = file('out/lib')
}
.
.
.
task copyDeps<< {
        copy {
                from("/opt/microsoft/sdk/servicefabric/java/packages/lib")
                into("./out/lib/lib")
                include('*.jar')
        }
        copy {
                from("/opt/microsoft/sdk/servicefabric/java/packages/lib")
                into("./out/lib/lib")
                include('libj*.so')
        }
        copy {
                from("../MyactorInterface/out/lib")
                into("./out/lib/lib")
                include('*.jar')
        }
}
```
<span data-ttu-id="c2cba-151">Теперь hello зависимости hello toofetch из Maven, **обновление** ``build.gradle`` будет иметь соответствующий частей hello следующим -</span><span class="sxs-lookup"><span data-stu-id="c2cba-151">Now, toofetch hello dependencies from Maven, hello **updated** ``build.gradle`` would have hello corresponding parts as follows -</span></span>
```
repositories {
    mavenCentral()
}

configurations {
    azuresf
}

dependencies {
    compile project(':MyactorInterface')
    azuresf ('com.microsoft.servicefabric:sf-actors-preview:0.10.0')
    compile fileTree(dir: 'lib', include: '*.jar')
}

task explodeDeps(type: Copy, dependsOn:configurations.azuresf) { task ->
    configurations.azuresf.filter { it.toString().contains("native-preview") }.each{
        from zipTree(it)
    }
    configurations.azuresf.filter { !it.toString().contains("native-preview") }.each {
        from it
    }
    into "lib"
    include "libj*.so", "*.jar"
}

compileJava.dependsOn(explodeDeps)
.
.
.
jar
{
    manifest {
        def mpath = configurations.compile.collect {'lib/'+it.getName()}.join (' ')
        mpath = mpath + ' ' + configurations.azuresf.collect {'lib/'+it.getName()}.join (' ')
    attributes(
                'Main-Class': 'reliableactor.test.MyactorTestClient',
                "Class-Path": mpath)
    baseName "myactor-test"
    destinationDir = file('./out/lib')
        }
}
.
.
.
task copyDeps<< {
        copy {
                from("lib/")
                into("./out/lib/lib")
                include('*')
        }
        copy {
                from("../MyactorInterface/out/lib")
                into("./out/lib/lib")
                include('*.jar')
        }
}
```

## <a name="next-steps"></a><span data-ttu-id="c2cba-152">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="c2cba-152">Next steps</span></span>

* [<span data-ttu-id="c2cba-153">Создание первого Java-приложения Service Fabric в Linux</span><span class="sxs-lookup"><span data-stu-id="c2cba-153">Create and deploy your first Service Fabric Java application on Linux by using Yeoman</span></span>](service-fabric-create-your-first-linux-application-with-java.md)
* [<span data-ttu-id="c2cba-154">Подключаемый модуль Service Fabric для разработки приложений Eclipse на Java</span><span class="sxs-lookup"><span data-stu-id="c2cba-154">Create and deploy your first Service Fabric Java application on Linux by using Service Fabric Plugin for Eclipse</span></span>](service-fabric-get-started-eclipse.md)
* [<span data-ttu-id="c2cba-155">Взаимодействовать с помощью hello CLI структуры службы кластеров Service Fabric</span><span class="sxs-lookup"><span data-stu-id="c2cba-155">Interact with Service Fabric clusters using hello Service Fabric CLI</span></span>](service-fabric-cli.md)
