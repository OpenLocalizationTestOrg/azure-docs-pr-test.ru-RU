---
title: "aaaCreate приложения Java службы reliable Actor Azure Service Fabric для Linux | Документы Microsoft"
description: "Узнайте, как toocreate и развертывать приложения Java Service Fabric службы reliable Actor в течение пяти минут."
services: service-fabric
documentationcenter: java
author: rwike77
manager: timlt
editor: 
ms.assetid: 02b51f11-5d78-4c54-bb68-8e128677783e
ms.service: service-fabric
ms.devlang: java
ms.topic: hero-article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/23/2017
ms.author: ryanwi
ms.openlocfilehash: 11496b767811c89969c65d1682d843448eb6a922
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-first-java-service-fabric-reliable-actors-application-on-linux"></a><span data-ttu-id="7dc09-103">Создание первого приложения Java Reliable Actors для Linux в Service Fabric</span><span class="sxs-lookup"><span data-stu-id="7dc09-103">Create your first Java Service Fabric Reliable Actors application on Linux</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="7dc09-104">C# для Windows</span><span class="sxs-lookup"><span data-stu-id="7dc09-104">C# - Windows</span></span>](service-fabric-create-your-first-application-in-visual-studio.md)
> * [<span data-ttu-id="7dc09-105">Java для Linux</span><span class="sxs-lookup"><span data-stu-id="7dc09-105">Java - Linux</span></span>](service-fabric-create-your-first-linux-application-with-java.md)
> * [<span data-ttu-id="7dc09-106">C# для Linux</span><span class="sxs-lookup"><span data-stu-id="7dc09-106">C# - Linux</span></span>](service-fabric-create-your-first-linux-application-with-csharp.md)
>
>

<span data-ttu-id="7dc09-107">Используя это краткое руководство, вы создадите первое Java-приложение Azure Service Fabric в среде разработки Linux всего за несколько минут.</span><span class="sxs-lookup"><span data-stu-id="7dc09-107">This quick-start helps you create your first Azure Service Fabric Java application in a Linux development environment in just a few minutes.</span></span>  <span data-ttu-id="7dc09-108">По завершении вы получите простое приложение Java одна служба запущена на кластере локальная разработка hello.</span><span class="sxs-lookup"><span data-stu-id="7dc09-108">When you are finished, you'll have a simple Java single-service application running on hello local development cluster.</span></span>  

## <a name="prerequisites"></a><span data-ttu-id="7dc09-109">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="7dc09-109">Prerequisites</span></span>
<span data-ttu-id="7dc09-110">Перед началом работы установки hello Service Fabric SDK, hello CLI структуры службы и настроить кластер разработки в вашей [среды разработки Linux](service-fabric-get-started-linux.md).</span><span class="sxs-lookup"><span data-stu-id="7dc09-110">Before you get started, install hello Service Fabric SDK, hello Service Fabric CLI, and setup a development cluster in your [Linux development environment](service-fabric-get-started-linux.md).</span></span> <span data-ttu-id="7dc09-111">Если вы используете Mac OS X, можно [настроить среду разработки Linux на виртуальной машине с помощью Vagrant](service-fabric-get-started-mac.md).</span><span class="sxs-lookup"><span data-stu-id="7dc09-111">If you are using Mac OS X, you can [set up a Linux development environment in a virtual machine using Vagrant](service-fabric-get-started-mac.md).</span></span>

<span data-ttu-id="7dc09-112">Необходимо также tooinstall hello [службы структуры CLI](service-fabric-cli.md).</span><span class="sxs-lookup"><span data-stu-id="7dc09-112">You will also want tooinstall hello [Service Fabric CLI](service-fabric-cli.md).</span></span>

### <a name="install-and-set-up-hello-generators-for-java"></a><span data-ttu-id="7dc09-113">Установка и настройка генераторы hello для Java</span><span class="sxs-lookup"><span data-stu-id="7dc09-113">Install and set up hello generators for Java</span></span>
<span data-ttu-id="7dc09-114">Service Fabric предоставляет средства формирования шаблонов, которые позволяют создавать приложения Java в Service Fabric из терминала с помощью генератора шаблонов Yeoman.</span><span class="sxs-lookup"><span data-stu-id="7dc09-114">Service Fabric provides scaffolding tools which will help you create a Service Fabric Java application from terminal using Yeoman template generator.</span></span> <span data-ttu-id="7dc09-115">Выполните шаги hello ниже tooensure, у вас есть генератор yeoman шаблона hello Service Fabric для Java работа на компьютере.</span><span class="sxs-lookup"><span data-stu-id="7dc09-115">Please follow hello steps below tooensure you have hello Service Fabric yeoman template generator for Java working on your machine.</span></span>
1. <span data-ttu-id="7dc09-116">Установите Node.js и NPM на компьютере.</span><span class="sxs-lookup"><span data-stu-id="7dc09-116">Install nodejs and NPM on your machine</span></span>

  ```bash
  sudo apt-get install npm
  sudo apt install nodejs-legacy
  ```
2. <span data-ttu-id="7dc09-117">Установите на компьютере генератор шаблонов [Yeoman](http://yeoman.io/) из NPM.</span><span class="sxs-lookup"><span data-stu-id="7dc09-117">Install [Yeoman](http://yeoman.io/) template generator on your machine from NPM</span></span>

  ```bash
  sudo npm install -g yo
  ```
3. <span data-ttu-id="7dc09-118">Установка приложения генератора hello Yeo Java структуры службы из NPM</span><span class="sxs-lookup"><span data-stu-id="7dc09-118">Install hello Service Fabric Yeo Java application generator from NPM</span></span>

  ```bash
  sudo npm install -g generator-azuresfjava
  ```

## <a name="create-hello-application"></a><span data-ttu-id="7dc09-119">Создание приложения hello</span><span class="sxs-lookup"><span data-stu-id="7dc09-119">Create hello application</span></span>
<span data-ttu-id="7dc09-120">Приложение Service Fabric содержит одну или несколько служб, каждый с определенной ролью в предоставлении функциональных возможностей приложения hello.</span><span class="sxs-lookup"><span data-stu-id="7dc09-120">A Service Fabric application contains one or more services, each with a specific role in delivering hello application's functionality.</span></span> <span data-ttu-id="7dc09-121">Генератор Hello установлены в последнем разделе hello, делает его легко toocreate свою первую службу и tooadd более позднее.</span><span class="sxs-lookup"><span data-stu-id="7dc09-121">hello generator you installed in hello last section, makes it easy toocreate your first service and tooadd more later.</span></span>  <span data-ttu-id="7dc09-122">Кроме того, можно создать, собрать и развернуть Java-приложения Service Fabric с помощью подключаемого модуля для Eclipse.</span><span class="sxs-lookup"><span data-stu-id="7dc09-122">You can also create, build, and deploy Service Fabric Java applications using a plugin for Eclipse.</span></span> <span data-ttu-id="7dc09-123">См. статью [Подключаемый модуль Service Fabric для разработки приложений Eclipse на Java](service-fabric-get-started-eclipse.md).</span><span class="sxs-lookup"><span data-stu-id="7dc09-123">See [Create and deploy your first Java application using Eclipse](service-fabric-get-started-eclipse.md).</span></span> <span data-ttu-id="7dc09-124">В этом кратком руководстве используйте Yeoman toocreate приложения с одной службы, который сохраняет и возвращает значение счетчика.</span><span class="sxs-lookup"><span data-stu-id="7dc09-124">For this quick start, use Yeoman toocreate an application with a single service that stores and gets a counter value.</span></span>

1. <span data-ttu-id="7dc09-125">В окне терминала введите ``yo azuresfjava``.</span><span class="sxs-lookup"><span data-stu-id="7dc09-125">In a terminal, type ``yo azuresfjava``.</span></span>
2. <span data-ttu-id="7dc09-126">Присвойте имя приложению.</span><span class="sxs-lookup"><span data-stu-id="7dc09-126">Name your application.</span></span>
3. <span data-ttu-id="7dc09-127">Выберите тип свою первую службу hello и назовите его.</span><span class="sxs-lookup"><span data-stu-id="7dc09-127">Choose hello type of your first service and name it.</span></span> <span data-ttu-id="7dc09-128">Для этого примера выберите службу Reliable Actor.</span><span class="sxs-lookup"><span data-stu-id="7dc09-128">For this tutorial, choose a Reliable Actor Service.</span></span> <span data-ttu-id="7dc09-129">Дополнительные сведения о hello других типов служб, в разделе [Service Fabric, общие сведения о модели программирования](service-fabric-choose-framework.md).</span><span class="sxs-lookup"><span data-stu-id="7dc09-129">For more information about hello other types of services, see [Service Fabric programming model overview](service-fabric-choose-framework.md).</span></span>
   <span data-ttu-id="7dc09-130">![Генератор Service Fabric Yeoman для Java][sf-yeoman]</span><span class="sxs-lookup"><span data-stu-id="7dc09-130">![Service Fabric Yeoman generator for Java][sf-yeoman]</span></span>

## <a name="build-hello-application"></a><span data-ttu-id="7dc09-131">Создание приложения hello</span><span class="sxs-lookup"><span data-stu-id="7dc09-131">Build hello application</span></span>
<span data-ttu-id="7dc09-132">шаблоны Hello Yeoman структуры службы включают сценарий построения для [Gradle](https://gradle.org/), который можно использовать приложение hello toobuild из hello терминалов.</span><span class="sxs-lookup"><span data-stu-id="7dc09-132">hello Service Fabric Yeoman templates include a build script for [Gradle](https://gradle.org/), which you can use toobuild hello application from hello terminal.</span></span>
<span data-ttu-id="7dc09-133">Зависимости Java в Service Fabric извлекаются из Maven.</span><span class="sxs-lookup"><span data-stu-id="7dc09-133">Service Fabric Java dependencies get fetched from Maven.</span></span> <span data-ttu-id="7dc09-134">toobuild и hello приложений Java структуры службы, необходимо tooensure, что у вас есть JDK и установлены Gradle.</span><span class="sxs-lookup"><span data-stu-id="7dc09-134">toobuild and work on hello Service Fabric Java applications, you need tooensure that you have JDK and Gradle installed.</span></span> <span data-ttu-id="7dc09-135">Если еще не установлен, можно запустить hello tooinstall JDK(openjdk-8-jdk) и Gradle -</span><span class="sxs-lookup"><span data-stu-id="7dc09-135">If not yet installed, you can run hello following tooinstall JDK(openjdk-8-jdk) and Gradle -</span></span>

  ```bash
  sudo apt-get install openjdk-8-jdk-headless
  sudo apt-get install gradle
  ```

<span data-ttu-id="7dc09-136">пакет и toobuild hello, выполнения приложения hello следующее:</span><span class="sxs-lookup"><span data-stu-id="7dc09-136">toobuild and package hello application, run hello following:</span></span>

  ```bash
  cd myapp
  gradle
  ```

## <a name="deploy-hello-application"></a><span data-ttu-id="7dc09-137">Развертывание приложения hello</span><span class="sxs-lookup"><span data-stu-id="7dc09-137">Deploy hello application</span></span>
<span data-ttu-id="7dc09-138">После построения приложения hello, вы можете развернуть локальный кластер toohello.</span><span class="sxs-lookup"><span data-stu-id="7dc09-138">Once hello application is built, you can deploy it toohello local cluster.</span></span>

1. <span data-ttu-id="7dc09-139">Подключите toohello локальный кластер Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="7dc09-139">Connect toohello local Service Fabric cluster.</span></span>

    ```bash
    sfctl cluster select --endpoint http://localhost:19080
    ```

2. <span data-ttu-id="7dc09-140">Сценарий установки выполнения hello в toocopy шаблона hello hello хранилище образов кластера для приложения пакет toohello, регистрация типа приложения hello и создание экземпляра приложения hello.</span><span class="sxs-lookup"><span data-stu-id="7dc09-140">Run hello install script provided in hello template toocopy hello application package toohello cluster's image store, register hello application type, and create an instance of hello application.</span></span>

    ```bash
    ./install.sh
    ```

<span data-ttu-id="7dc09-141">Развертывание приложения hello построения является Здравствуйте таким же, как любое другое приложение Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="7dc09-141">Deploying hello built application is hello same as any other Service Fabric application.</span></span> <span data-ttu-id="7dc09-142">См. в документации hello [управление приложением Service Fabric с hello службы структуры CLI](service-fabric-application-lifecycle-sfctl.md) подробные инструкции.</span><span class="sxs-lookup"><span data-stu-id="7dc09-142">See hello documentation on [managing a Service Fabric application with hello Service Fabric CLI](service-fabric-application-lifecycle-sfctl.md) for detailed instructions.</span></span>

<span data-ttu-id="7dc09-143">Команды toothese параметры можно найти в манифестах hello создан внутри пакета приложения hello.</span><span class="sxs-lookup"><span data-stu-id="7dc09-143">Parameters toothese commands can be found in hello generated manifests inside hello application package.</span></span>

<span data-ttu-id="7dc09-144">После развертывания приложения hello, откройте браузер и перейдите к [Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) в [http://localhost:19080/обозреватель](http://localhost:19080/Explorer).</span><span class="sxs-lookup"><span data-stu-id="7dc09-144">Once hello application has been deployed, open a browser and navigate to [Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) at [http://localhost:19080/Explorer](http://localhost:19080/Explorer).</span></span>
<span data-ttu-id="7dc09-145">Разверните hello **приложений** узел и обратите внимание, что теперь есть запись для типа приложения и другой для hello первого экземпляра этого типа.</span><span class="sxs-lookup"><span data-stu-id="7dc09-145">Then, expand hello **Applications** node and note that there is now an entry for your application type and another for hello first instance of that type.</span></span>

## <a name="start-hello-test-client-and-perform-a-failover"></a><span data-ttu-id="7dc09-146">Запустите тестовый клиент hello и отработка отказа</span><span class="sxs-lookup"><span data-stu-id="7dc09-146">Start hello test client and perform a failover</span></span>
<span data-ttu-id="7dc09-147">Субъекты никакие действия выполняться не сами по себе, они требуют другой службой или клиентом toosend их сообщений.</span><span class="sxs-lookup"><span data-stu-id="7dc09-147">Actors do not do anything on their own, they require another service or client toosend them messages.</span></span> <span data-ttu-id="7dc09-148">шаблон субъекта Hello включает простой тестовый скрипт, можно использовать toointeract с службу субъектов hello.</span><span class="sxs-lookup"><span data-stu-id="7dc09-148">hello actor template includes a simple test script that you can use toointeract with hello actor service.</span></span>

1. <span data-ttu-id="7dc09-149">Запустите скрипт hello, используя hello Контрольные значения программа toosee hello выходные данные hello субъекта службы.</span><span class="sxs-lookup"><span data-stu-id="7dc09-149">Run hello script using hello watch utility toosee hello output of hello actor service.</span></span>  <span data-ttu-id="7dc09-150">Hello тестовый скрипт вызывает hello `setCountAsync()` tooincrement субъекта hello счетчик, метод вызывает hello `getCountAsync()` метод hello субъекта tooget hello новое значение счетчика и отображает это значение toohello консоли.</span><span class="sxs-lookup"><span data-stu-id="7dc09-150">hello test script calls hello `setCountAsync()` method on hello actor tooincrement a counter, calls hello `getCountAsync()` method on hello actor tooget hello new counter value, and displays that value toohello console.</span></span>

    ```bash
    cd myactorsvcTestClient
    watch -n 1 ./testclient.sh
    ```

2. <span data-ttu-id="7dc09-151">Найдите hello узла размещения hello первичной реплики для службы hello субъекта Service Fabric Explorer.</span><span class="sxs-lookup"><span data-stu-id="7dc09-151">In Service Fabric Explorer, locate hello node hosting hello primary replica for hello actor service.</span></span> <span data-ttu-id="7dc09-152">В приведенном далее снимке экрана приветствия это узел 3.</span><span class="sxs-lookup"><span data-stu-id="7dc09-152">In hello screenshot below, it is node 3.</span></span> <span data-ttu-id="7dc09-153">дескрипторы реплики основной службы Hello операций чтения и записи.</span><span class="sxs-lookup"><span data-stu-id="7dc09-153">hello primary service replica handles read and write operations.</span></span>  <span data-ttu-id="7dc09-154">Изменения в состоянии ожидания toohello вторичных реплик, работающих на узлах, 0 и 1 в приведенном ниже снимке экрана приветствия затем реплицируются.</span><span class="sxs-lookup"><span data-stu-id="7dc09-154">Changes in service state are then replicated out toohello secondary replicas, running on nodes 0 and 1 in hello screen shot below.</span></span>

    ![Поиск hello первичной реплики в обозреватель Service Fabric][sfx-primary]

3. <span data-ttu-id="7dc09-156">В **узлы**, щелкните узел hello можно найти в предыдущем шаге hello, а затем выберите **деактивировать (перезапустите)** из меню "действия" hello.</span><span class="sxs-lookup"><span data-stu-id="7dc09-156">In **Nodes**, click hello node you found in hello previous step, then select **Deactivate (restart)** from hello Actions menu.</span></span> <span data-ttu-id="7dc09-157">Это действие перезапускает hello узла, под управлением реплики основной службы hello и инициирует переход на другой ресурс tooone hello вторичных реплик, запущенный на другом узле.</span><span class="sxs-lookup"><span data-stu-id="7dc09-157">This action restarts hello node running hello primary service replica and forces a failover tooone of hello secondary replicas running on another node.</span></span>  <span data-ttu-id="7dc09-158">Вторичная реплика — унаследованная tooprimary, другой дополнительной реплике создается на другом узле, и первичная реплика hello запускает tootake операций чтения и записи.</span><span class="sxs-lookup"><span data-stu-id="7dc09-158">That secondary replica is promoted tooprimary, another secondary replica is created on a different node, and hello primary replica begins tootake read/write operations.</span></span> <span data-ttu-id="7dc09-159">Как перезапуска узла hello, просмотр выходных данных hello hello тестового клиента и обратите внимание, что счетчика hello продолжается tooincrement несмотря на hello перехода на другой ресурс.</span><span class="sxs-lookup"><span data-stu-id="7dc09-159">As hello node restarts, watch hello output from hello test client and note that hello counter continues tooincrement despite hello failover.</span></span>

## <a name="remove-hello-application"></a><span data-ttu-id="7dc09-160">Удалить приложение hello</span><span class="sxs-lookup"><span data-stu-id="7dc09-160">Remove hello application</span></span>
<span data-ttu-id="7dc09-161">Использовать сценарий удаления hello в экземпляр приложения hello toodelete шаблона hello, отмените регистрацию пакета приложения hello и удаления пакета приложения hello хранилище образов кластера hello.</span><span class="sxs-lookup"><span data-stu-id="7dc09-161">Use hello uninstall script provided in hello template toodelete hello application instance, unregister hello application package, and remove hello application package from hello cluster's image store.</span></span>

```bash
./uninstall.sh
```

<span data-ttu-id="7dc09-162">В обозреватель Service Fabric видно, что приложение hello и тип приложения больше не отображались в hello **приложений** узла.</span><span class="sxs-lookup"><span data-stu-id="7dc09-162">In Service Fabric explorer you see that hello application and application type no longer appear in hello **Applications** node.</span></span>

## <a name="service-fabric-java-libraries-on-maven"></a><span data-ttu-id="7dc09-163">Библиотеки Java для Service Fabric в Maven</span><span class="sxs-lookup"><span data-stu-id="7dc09-163">Service Fabric Java libraries on Maven</span></span>
<span data-ttu-id="7dc09-164">Библиотеки Java для Service Fabric размещены в Maven.</span><span class="sxs-lookup"><span data-stu-id="7dc09-164">Service Fabric Java libraries have been hosted in Maven.</span></span> <span data-ttu-id="7dc09-165">Можно добавить зависимости hello в hello ``pom.xml`` или ``build.gradle`` библиотеки Service Fabric Java toouse проекты из **mavenCentral**.</span><span class="sxs-lookup"><span data-stu-id="7dc09-165">You can add hello dependencies in hello ``pom.xml`` or ``build.gradle`` of your projects toouse Service Fabric Java libraries from **mavenCentral**.</span></span>

### <a name="actors"></a><span data-ttu-id="7dc09-166">Субъекты</span><span class="sxs-lookup"><span data-stu-id="7dc09-166">Actors</span></span>

<span data-ttu-id="7dc09-167">Поддержка субъекта Service Fabric Reliable Actors для приложения.</span><span class="sxs-lookup"><span data-stu-id="7dc09-167">Service Fabric Reliable Actor support for your application.</span></span>

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

### <a name="services"></a><span data-ttu-id="7dc09-168">Службы</span><span class="sxs-lookup"><span data-stu-id="7dc09-168">Services</span></span>

<span data-ttu-id="7dc09-169">Поддержка службы без отслеживания состояния Service Fabric для приложения.</span><span class="sxs-lookup"><span data-stu-id="7dc09-169">Service Fabric Stateless Service support for your application.</span></span>

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

### <a name="others"></a><span data-ttu-id="7dc09-170">Прочее</span><span class="sxs-lookup"><span data-stu-id="7dc09-170">Others</span></span>
#### <a name="transport"></a><span data-ttu-id="7dc09-171">Транспортировка</span><span class="sxs-lookup"><span data-stu-id="7dc09-171">Transport</span></span>

<span data-ttu-id="7dc09-172">Поддержка транспортного уровня для приложения Java в Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="7dc09-172">Transport layer support for Service Fabric Java application.</span></span> <span data-ttu-id="7dc09-173">Не обязательно tooexplicitly добавлять этот tooyour зависимостей Reliable Actor и приложения служб, без программирования на уровне транспорта hello.</span><span class="sxs-lookup"><span data-stu-id="7dc09-173">You do not need tooexplicitly add this dependency tooyour Reliable Actor or Service applications, unless you program at hello transport layer.</span></span>

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

#### <a name="fabric-support"></a><span data-ttu-id="7dc09-174">Поддержка Service Fabric</span><span class="sxs-lookup"><span data-stu-id="7dc09-174">Fabric support</span></span>

<span data-ttu-id="7dc09-175">Поддержка уровня системы для службы структуры, говорящий toonative среда выполнения Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="7dc09-175">System level support for Service Fabric, which talks toonative Service Fabric runtime.</span></span> <span data-ttu-id="7dc09-176">Нет необходимости tooexplicitly добавьте эту зависимость tooyour Reliable Actor или приложений службы.</span><span class="sxs-lookup"><span data-stu-id="7dc09-176">You do not need tooexplicitly add this dependency tooyour Reliable Actor or Service applications.</span></span> <span data-ttu-id="7dc09-177">Это возвращает автоматически получены из Maven, при включении hello другие зависимости выше.</span><span class="sxs-lookup"><span data-stu-id="7dc09-177">This gets fetched automatically from Maven, when you include hello other dependencies above.</span></span>

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

## <a name="migrating-old-service-fabric-java-applications-toobe-used-with-maven"></a><span data-ttu-id="7dc09-178">Миграция старый toobe приложений Java структуры службы, используемые с Maven</span><span class="sxs-lookup"><span data-stu-id="7dc09-178">Migrating old Service Fabric Java applications toobe used with Maven</span></span>
<span data-ttu-id="7dc09-179">Служба Fabric Java библиотеки недавно были удалены из репозитория tooMaven Service Fabric Java SDK.</span><span class="sxs-lookup"><span data-stu-id="7dc09-179">We have recently moved Service Fabric Java libraries from Service Fabric Java SDK tooMaven repository.</span></span> <span data-ttu-id="7dc09-180">Хотя hello новые приложения, созданные с помощью Yeoman или Eclipse, создаст последних измененных проектов (которые будут может toowork с Maven), необходимо обновить существующие структуры службы без сохранения состояния и приложения Java субъектов, которые использовали hello службы Структуры пакета Java SDK более ранних версиях зависимости службы структуры Java hello toouse из Maven.</span><span class="sxs-lookup"><span data-stu-id="7dc09-180">While hello new applications you generate using Yeoman or Eclipse, will generate latest updated projects (which will be able toowork with Maven), you can update your existing Service Fabric stateless or actor Java applications, which were using hello Service Fabric Java SDK earlier, toouse hello Service Fabric Java dependencies from Maven.</span></span> <span data-ttu-id="7dc09-181">Выполните шаги hello упомянутые [здесь](service-fabric-migrate-old-javaapp-to-use-maven.md) tooensure старые приложения работает с Maven.</span><span class="sxs-lookup"><span data-stu-id="7dc09-181">Please follow hello steps mentioned [here](service-fabric-migrate-old-javaapp-to-use-maven.md) tooensure your older application works with Maven.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7dc09-182">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="7dc09-182">Next steps</span></span>

* [<span data-ttu-id="7dc09-183">Подключаемый модуль Service Fabric для разработки приложений Eclipse на Java</span><span class="sxs-lookup"><span data-stu-id="7dc09-183">Create your first Service Fabric Java application on Linux using Eclipse</span></span>](service-fabric-get-started-eclipse.md)
* [<span data-ttu-id="7dc09-184">Общие сведения о надежных субъектах Service Fabric</span><span class="sxs-lookup"><span data-stu-id="7dc09-184">Learn more about Reliable Actors</span></span>](service-fabric-reliable-actors-introduction.md)
* [<span data-ttu-id="7dc09-185">Взаимодействовать с помощью hello CLI структуры службы кластеров Service Fabric</span><span class="sxs-lookup"><span data-stu-id="7dc09-185">Interact with Service Fabric clusters using hello Service Fabric CLI</span></span>](service-fabric-cli.md)
* <span data-ttu-id="7dc09-186">[Сведения о вариантах поддержки Service Fabric](service-fabric-support.md)</span><span class="sxs-lookup"><span data-stu-id="7dc09-186">Learn about [Service Fabric support options](service-fabric-support.md)</span></span>
* [<span data-ttu-id="7dc09-187">Командная строка Azure Service Fabric</span><span class="sxs-lookup"><span data-stu-id="7dc09-187">Getting started with Service Fabric CLI</span></span>](service-fabric-cli.md)

<!-- Images -->
[sf-yeoman]: ./media/service-fabric-create-your-first-linux-application-with-java/sf-yeoman.png
[sfx-primary]: ./media/service-fabric-create-your-first-linux-application-with-java/sfx-primary.png
[sf-eclipse-templates]: ./media/service-fabric-create-your-first-linux-application-with-java/sf-eclipse-templates.png
