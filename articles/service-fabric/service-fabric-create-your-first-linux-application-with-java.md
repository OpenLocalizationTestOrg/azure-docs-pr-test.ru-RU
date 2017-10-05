---
title: "Создание приложения Java Reliable Actors для Linux в Azure Service Fabric | Документация Майкрософт"
description: "Узнайте как создавать приложение Java Reliable Actors Service Fabric в течении пяти минут."
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
ms.openlocfilehash: baf948587ede31fe3d5b4f6f0981269b4cfe4d3d
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="create-your-first-java-service-fabric-reliable-actors-application-on-linux"></a><span data-ttu-id="5516b-103">Создание первого приложения Java Reliable Actors для Linux в Service Fabric</span><span class="sxs-lookup"><span data-stu-id="5516b-103">Create your first Java Service Fabric Reliable Actors application on Linux</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="5516b-104">C# для Windows</span><span class="sxs-lookup"><span data-stu-id="5516b-104">C# - Windows</span></span>](service-fabric-create-your-first-application-in-visual-studio.md)
> * [<span data-ttu-id="5516b-105">Java для Linux</span><span class="sxs-lookup"><span data-stu-id="5516b-105">Java - Linux</span></span>](service-fabric-create-your-first-linux-application-with-java.md)
> * [<span data-ttu-id="5516b-106">C# для Linux</span><span class="sxs-lookup"><span data-stu-id="5516b-106">C# - Linux</span></span>](service-fabric-create-your-first-linux-application-with-csharp.md)
>
>

<span data-ttu-id="5516b-107">Используя это краткое руководство, вы создадите первое Java-приложение Azure Service Fabric в среде разработки Linux всего за несколько минут.</span><span class="sxs-lookup"><span data-stu-id="5516b-107">This quick-start helps you create your first Azure Service Fabric Java application in a Linux development environment in just a few minutes.</span></span>  <span data-ttu-id="5516b-108">В результате вы получите простое приложение Java с одной службой, работающее в кластере локальной разработки.</span><span class="sxs-lookup"><span data-stu-id="5516b-108">When you are finished, you'll have a simple Java single-service application running on the local development cluster.</span></span>  

## <a name="prerequisites"></a><span data-ttu-id="5516b-109">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="5516b-109">Prerequisites</span></span>
<span data-ttu-id="5516b-110">Перед началом работы установите пакет SDK для Service Fabric, интерфейс командной строки Service Fabric и настройте кластер разработки в своей [среде разработки Linux](service-fabric-get-started-linux.md).</span><span class="sxs-lookup"><span data-stu-id="5516b-110">Before you get started, install the Service Fabric SDK, the Service Fabric CLI, and setup a development cluster in your [Linux development environment](service-fabric-get-started-linux.md).</span></span> <span data-ttu-id="5516b-111">Если вы используете Mac OS X, можно [настроить среду разработки Linux на виртуальной машине с помощью Vagrant](service-fabric-get-started-mac.md).</span><span class="sxs-lookup"><span data-stu-id="5516b-111">If you are using Mac OS X, you can [set up a Linux development environment in a virtual machine using Vagrant](service-fabric-get-started-mac.md).</span></span>

<span data-ttu-id="5516b-112">Вам также потребуется установить [интерфейс командной строки Service Fabric](service-fabric-cli.md).</span><span class="sxs-lookup"><span data-stu-id="5516b-112">You will also want to install the [Service Fabric CLI](service-fabric-cli.md).</span></span>

### <a name="install-and-set-up-the-generators-for-java"></a><span data-ttu-id="5516b-113">Установка и настройка генераторов для Java</span><span class="sxs-lookup"><span data-stu-id="5516b-113">Install and set up the generators for Java</span></span>
<span data-ttu-id="5516b-114">Service Fabric предоставляет средства формирования шаблонов, которые позволяют создавать приложения Java в Service Fabric из терминала с помощью генератора шаблонов Yeoman.</span><span class="sxs-lookup"><span data-stu-id="5516b-114">Service Fabric provides scaffolding tools which will help you create a Service Fabric Java application from terminal using Yeoman template generator.</span></span> <span data-ttu-id="5516b-115">Чтобы установить генератор шаблонов Service Fabric Yeoman для Java на компьютере, сделайте следующее.</span><span class="sxs-lookup"><span data-stu-id="5516b-115">Please follow the steps below to ensure you have the Service Fabric yeoman template generator for Java working on your machine.</span></span>
1. <span data-ttu-id="5516b-116">Установите Node.js и NPM на компьютере.</span><span class="sxs-lookup"><span data-stu-id="5516b-116">Install nodejs and NPM on your machine</span></span>

  ```bash
  sudo apt-get install npm
  sudo apt install nodejs-legacy
  ```
2. <span data-ttu-id="5516b-117">Установите на компьютере генератор шаблонов [Yeoman](http://yeoman.io/) из NPM.</span><span class="sxs-lookup"><span data-stu-id="5516b-117">Install [Yeoman](http://yeoman.io/) template generator on your machine from NPM</span></span>

  ```bash
  sudo npm install -g yo
  ```
3. <span data-ttu-id="5516b-118">Установите генератор Java-приложений Service Fabric Yeoman из NPM.</span><span class="sxs-lookup"><span data-stu-id="5516b-118">Install the Service Fabric Yeo Java application generator from NPM</span></span>

  ```bash
  sudo npm install -g generator-azuresfjava
  ```

## <a name="create-the-application"></a><span data-ttu-id="5516b-119">Создание приложения</span><span class="sxs-lookup"><span data-stu-id="5516b-119">Create the application</span></span>
<span data-ttu-id="5516b-120">Приложение Service Fabric содержит одну или несколько служб, каждая из которых выполняет определенную роль в работе приложения.</span><span class="sxs-lookup"><span data-stu-id="5516b-120">A Service Fabric application contains one or more services, each with a specific role in delivering the application's functionality.</span></span> <span data-ttu-id="5516b-121">Генератор, установленный в предыдущем разделе, упрощает создание первой службы и добавление последующих.</span><span class="sxs-lookup"><span data-stu-id="5516b-121">The generator you installed in the last section, makes it easy to create your first service and to add more later.</span></span>  <span data-ttu-id="5516b-122">Кроме того, можно создать, собрать и развернуть Java-приложения Service Fabric с помощью подключаемого модуля для Eclipse.</span><span class="sxs-lookup"><span data-stu-id="5516b-122">You can also create, build, and deploy Service Fabric Java applications using a plugin for Eclipse.</span></span> <span data-ttu-id="5516b-123">См. статью [Подключаемый модуль Service Fabric для разработки приложений Eclipse на Java](service-fabric-get-started-eclipse.md).</span><span class="sxs-lookup"><span data-stu-id="5516b-123">See [Create and deploy your first Java application using Eclipse](service-fabric-get-started-eclipse.md).</span></span> <span data-ttu-id="5516b-124">В этом руководстве используйте Yeoman для создания приложения с одной службой, которая сохраняет и получает значение счетчика.</span><span class="sxs-lookup"><span data-stu-id="5516b-124">For this quick start, use Yeoman to create an application with a single service that stores and gets a counter value.</span></span>

1. <span data-ttu-id="5516b-125">В окне терминала введите ``yo azuresfjava``.</span><span class="sxs-lookup"><span data-stu-id="5516b-125">In a terminal, type ``yo azuresfjava``.</span></span>
2. <span data-ttu-id="5516b-126">Присвойте имя приложению.</span><span class="sxs-lookup"><span data-stu-id="5516b-126">Name your application.</span></span>
3. <span data-ttu-id="5516b-127">Выберите тип первой службы и присвойте ей имя.</span><span class="sxs-lookup"><span data-stu-id="5516b-127">Choose the type of your first service and name it.</span></span> <span data-ttu-id="5516b-128">Для этого примера выберите службу Reliable Actor.</span><span class="sxs-lookup"><span data-stu-id="5516b-128">For this tutorial, choose a Reliable Actor Service.</span></span> <span data-ttu-id="5516b-129">Дополнительные сведения о других типах служб см. в статье [Общие сведения о модели программирования Service Fabric](service-fabric-choose-framework.md).</span><span class="sxs-lookup"><span data-stu-id="5516b-129">For more information about the other types of services, see [Service Fabric programming model overview](service-fabric-choose-framework.md).</span></span>
   <span data-ttu-id="5516b-130">![Генератор Service Fabric Yeoman для Java][sf-yeoman]</span><span class="sxs-lookup"><span data-stu-id="5516b-130">![Service Fabric Yeoman generator for Java][sf-yeoman]</span></span>

## <a name="build-the-application"></a><span data-ttu-id="5516b-131">Создание приложения</span><span class="sxs-lookup"><span data-stu-id="5516b-131">Build the application</span></span>
<span data-ttu-id="5516b-132">Шаблоны Service Fabric для Yeoman включают скрипт сборки для [Gradle](https://gradle.org/), который можно использовать для создания приложения из терминала.</span><span class="sxs-lookup"><span data-stu-id="5516b-132">The Service Fabric Yeoman templates include a build script for [Gradle](https://gradle.org/), which you can use to build the application from the terminal.</span></span>
<span data-ttu-id="5516b-133">Зависимости Java в Service Fabric извлекаются из Maven.</span><span class="sxs-lookup"><span data-stu-id="5516b-133">Service Fabric Java dependencies get fetched from Maven.</span></span> <span data-ttu-id="5516b-134">Чтобы создавать приложения Java в Service Fabric и работать с ними, сначала установите JDK и Gradle.</span><span class="sxs-lookup"><span data-stu-id="5516b-134">To build and work on the Service Fabric Java applications, you need to ensure that you have JDK and Gradle installed.</span></span> <span data-ttu-id="5516b-135">Если эти компоненты еще не установлены, запустите следующие команды для установки JDK (openjdk 8 jdk) и Gradle:</span><span class="sxs-lookup"><span data-stu-id="5516b-135">If not yet installed, you can run the following to install JDK(openjdk-8-jdk) and Gradle -</span></span>

  ```bash
  sudo apt-get install openjdk-8-jdk-headless
  sudo apt-get install gradle
  ```

<span data-ttu-id="5516b-136">Используйте следующую команду, чтобы собрать и упаковать приложение:</span><span class="sxs-lookup"><span data-stu-id="5516b-136">To build and package the application, run the following:</span></span>

  ```bash
  cd myapp
  gradle
  ```

## <a name="deploy-the-application"></a><span data-ttu-id="5516b-137">Развертывание приложения</span><span class="sxs-lookup"><span data-stu-id="5516b-137">Deploy the application</span></span>
<span data-ttu-id="5516b-138">Созданное приложение можно развернуть в локальном кластере.</span><span class="sxs-lookup"><span data-stu-id="5516b-138">Once the application is built, you can deploy it to the local cluster.</span></span>

1. <span data-ttu-id="5516b-139">Подключитесь к удаленному кластеру Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="5516b-139">Connect to the local Service Fabric cluster.</span></span>

    ```bash
    sfctl cluster select --endpoint http://localhost:19080
    ```

2. <span data-ttu-id="5516b-140">С помощью скрипта установки (включен в шаблон) скопируйте пакет приложения в хранилище образов кластера, зарегистрируйте тип приложения и создайте экземпляр приложения.</span><span class="sxs-lookup"><span data-stu-id="5516b-140">Run the install script provided in the template to copy the application package to the cluster's image store, register the application type, and create an instance of the application.</span></span>

    ```bash
    ./install.sh
    ```

<span data-ttu-id="5516b-141">Созданное приложение развертывается так же, как и любое другое приложение Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="5516b-141">Deploying the built application is the same as any other Service Fabric application.</span></span> <span data-ttu-id="5516b-142">Дополнительные сведения см. в документации по [управлению приложениями Service Fabric с помощью интерфейса командной строки Service Fabric](service-fabric-application-lifecycle-sfctl.md).</span><span class="sxs-lookup"><span data-stu-id="5516b-142">See the documentation on [managing a Service Fabric application with the Service Fabric CLI](service-fabric-application-lifecycle-sfctl.md) for detailed instructions.</span></span>

<span data-ttu-id="5516b-143">Параметры для этих команд можно найти в созданном манифесте в пакете приложения.</span><span class="sxs-lookup"><span data-stu-id="5516b-143">Parameters to these commands can be found in the generated manifests inside the application package.</span></span>

<span data-ttu-id="5516b-144">Когда приложение будет развернуто, откройте браузер и перейдите к [Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) по адресу [http://localhost:19080/Explorer](http://localhost:19080/Explorer).</span><span class="sxs-lookup"><span data-stu-id="5516b-144">Once the application has been deployed, open a browser and navigate to [Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) at [http://localhost:19080/Explorer](http://localhost:19080/Explorer).</span></span>
<span data-ttu-id="5516b-145">Затем разверните узел **Приложения**. Вы увидите одну запись для типа приложения и еще одну — для первого экземпляра этого типа.</span><span class="sxs-lookup"><span data-stu-id="5516b-145">Then, expand the **Applications** node and note that there is now an entry for your application type and another for the first instance of that type.</span></span>

## <a name="start-the-test-client-and-perform-a-failover"></a><span data-ttu-id="5516b-146">Запуск тестового клиента и отработка отказа</span><span class="sxs-lookup"><span data-stu-id="5516b-146">Start the test client and perform a failover</span></span>
<span data-ttu-id="5516b-147">Проекты субъекта предполагают использование дополнительных средств. Например, для отправки сообщений им требуется другая служба или клиент.</span><span class="sxs-lookup"><span data-stu-id="5516b-147">Actors do not do anything on their own, they require another service or client to send them messages.</span></span> <span data-ttu-id="5516b-148">Шаблон субъекта включает простой тестовый скрипт, обеспечивающий взаимодействие со службой субъекта.</span><span class="sxs-lookup"><span data-stu-id="5516b-148">The actor template includes a simple test script that you can use to interact with the actor service.</span></span>

1. <span data-ttu-id="5516b-149">Запустите этот скрипт с помощью служебной программы для отслеживания, чтобы просмотреть выходные данные службы субъекта.</span><span class="sxs-lookup"><span data-stu-id="5516b-149">Run the script using the watch utility to see the output of the actor service.</span></span>  <span data-ttu-id="5516b-150">Сценарий теста вызывает для субъекта метод `setCountAsync()`, увеличивающий значение счетчика. Затем для субъекта вызывается метод `getCountAsync()`, чтобы получить новое значение счетчика и вывести его на консоль.</span><span class="sxs-lookup"><span data-stu-id="5516b-150">The test script calls the `setCountAsync()` method on the actor to increment a counter, calls the `getCountAsync()` method on the actor to get the new counter value, and displays that value to the console.</span></span>

    ```bash
    cd myactorsvcTestClient
    watch -n 1 ./testclient.sh
    ```

2. <span data-ttu-id="5516b-151">В Service Fabric Explorer найдите узел, в котором размещена первичная реплика службы субъекта.</span><span class="sxs-lookup"><span data-stu-id="5516b-151">In Service Fabric Explorer, locate the node hosting the primary replica for the actor service.</span></span> <span data-ttu-id="5516b-152">В нашем примере это узел 3.</span><span class="sxs-lookup"><span data-stu-id="5516b-152">In the screenshot below, it is node 3.</span></span> <span data-ttu-id="5516b-153">Первичная реплика службы обрабатывает операции чтения и записи.</span><span class="sxs-lookup"><span data-stu-id="5516b-153">The primary service replica handles read and write operations.</span></span>  <span data-ttu-id="5516b-154">Затем изменения в состоянии службы реплицируются во вторичные реплики, выполняющиеся на узлах 0 и 1, как показано на снимке экрана ниже.</span><span class="sxs-lookup"><span data-stu-id="5516b-154">Changes in service state are then replicated out to the secondary replicas, running on nodes 0 and 1 in the screen shot below.</span></span>

    ![Поиск первичной реплики в Service Fabric Explorer][sfx-primary]

3. <span data-ttu-id="5516b-156">В разделе **Узлы** щелкните найденный узел, а затем выберите в меню "Действия" пункт **Отключить (перезапустить)**.</span><span class="sxs-lookup"><span data-stu-id="5516b-156">In **Nodes**, click the node you found in the previous step, then select **Deactivate (restart)** from the Actions menu.</span></span> <span data-ttu-id="5516b-157">После этого узел, на котором запущена первичная реплика службы, перезапускается и выполняется принудительная отработка отказа с переходом на одну из вторичных реплик, запущенных на другом узле.</span><span class="sxs-lookup"><span data-stu-id="5516b-157">This action restarts the node running the primary service replica and forces a failover to one of the secondary replicas running on another node.</span></span>  <span data-ttu-id="5516b-158">Вторичная реплика повышается до первичной, на другом узле создается еще одна вторичная реплика, и первичная реплика начинает выполнять операции чтения и записи.</span><span class="sxs-lookup"><span data-stu-id="5516b-158">That secondary replica is promoted to primary, another secondary replica is created on a different node, and the primary replica begins to take read/write operations.</span></span> <span data-ttu-id="5516b-159">После перезапуска узла обратите внимание на выходные данные тестового клиента: счетчик будет увеличиваться несмотря на отработку отказа.</span><span class="sxs-lookup"><span data-stu-id="5516b-159">As the node restarts, watch the output from the test client and note that the counter continues to increment despite the failover.</span></span>

## <a name="remove-the-application"></a><span data-ttu-id="5516b-160">Удаление приложения</span><span class="sxs-lookup"><span data-stu-id="5516b-160">Remove the application</span></span>
<span data-ttu-id="5516b-161">С помощью скрипта для удаления экземпляра приложения (включен в шаблон) отмените регистрацию пакета приложения и удалите его из хранилища образов кластера.</span><span class="sxs-lookup"><span data-stu-id="5516b-161">Use the uninstall script provided in the template to delete the application instance, unregister the application package, and remove the application package from the cluster's image store.</span></span>

```bash
./uninstall.sh
```

<span data-ttu-id="5516b-162">В обозревателе Service Fabric вы увидите, что приложение и его тип больше не отображаются в узле **Приложения**.</span><span class="sxs-lookup"><span data-stu-id="5516b-162">In Service Fabric explorer you see that the application and application type no longer appear in the **Applications** node.</span></span>

## <a name="service-fabric-java-libraries-on-maven"></a><span data-ttu-id="5516b-163">Библиотеки Java для Service Fabric в Maven</span><span class="sxs-lookup"><span data-stu-id="5516b-163">Service Fabric Java libraries on Maven</span></span>
<span data-ttu-id="5516b-164">Библиотеки Java для Service Fabric размещены в Maven.</span><span class="sxs-lookup"><span data-stu-id="5516b-164">Service Fabric Java libraries have been hosted in Maven.</span></span> <span data-ttu-id="5516b-165">Чтобы использовать библиотеки Java для Service Fabric из **mavenCentral**, вы можете добавить зависимости в файлы ``pom.xml`` или ``build.gradle`` своих проектов.</span><span class="sxs-lookup"><span data-stu-id="5516b-165">You can add the dependencies in the ``pom.xml`` or ``build.gradle`` of your projects to use Service Fabric Java libraries from **mavenCentral**.</span></span>

### <a name="actors"></a><span data-ttu-id="5516b-166">Субъекты</span><span class="sxs-lookup"><span data-stu-id="5516b-166">Actors</span></span>

<span data-ttu-id="5516b-167">Поддержка субъекта Service Fabric Reliable Actors для приложения.</span><span class="sxs-lookup"><span data-stu-id="5516b-167">Service Fabric Reliable Actor support for your application.</span></span>

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

### <a name="services"></a><span data-ttu-id="5516b-168">Службы</span><span class="sxs-lookup"><span data-stu-id="5516b-168">Services</span></span>

<span data-ttu-id="5516b-169">Поддержка службы без отслеживания состояния Service Fabric для приложения.</span><span class="sxs-lookup"><span data-stu-id="5516b-169">Service Fabric Stateless Service support for your application.</span></span>

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

### <a name="others"></a><span data-ttu-id="5516b-170">Прочее</span><span class="sxs-lookup"><span data-stu-id="5516b-170">Others</span></span>
#### <a name="transport"></a><span data-ttu-id="5516b-171">Транспортировка</span><span class="sxs-lookup"><span data-stu-id="5516b-171">Transport</span></span>

<span data-ttu-id="5516b-172">Поддержка транспортного уровня для приложения Java в Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="5516b-172">Transport layer support for Service Fabric Java application.</span></span> <span data-ttu-id="5516b-173">Вам не нужно явно добавлять эту зависимость в приложения Reliable Actors или Reliable Services, если ваша программа не находится на транспортном уровне.</span><span class="sxs-lookup"><span data-stu-id="5516b-173">You do not need to explicitly add this dependency to your Reliable Actor or Service applications, unless you program at the transport layer.</span></span>

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

#### <a name="fabric-support"></a><span data-ttu-id="5516b-174">Поддержка Service Fabric</span><span class="sxs-lookup"><span data-stu-id="5516b-174">Fabric support</span></span>

<span data-ttu-id="5516b-175">Поддержка на уровне системы для платформы Service Fabric, которая взаимодействует с собственной средой выполнения Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="5516b-175">System level support for Service Fabric, which talks to native Service Fabric runtime.</span></span> <span data-ttu-id="5516b-176">Вам не нужно явно добавлять эту зависимость в приложения Reliable Actors или Reliable Services.</span><span class="sxs-lookup"><span data-stu-id="5516b-176">You do not need to explicitly add this dependency to your Reliable Actor or Service applications.</span></span> <span data-ttu-id="5516b-177">Эта зависимость извлекается автоматически из Maven при включении других зависимостей, описанных выше.</span><span class="sxs-lookup"><span data-stu-id="5516b-177">This gets fetched automatically from Maven, when you include the other dependencies above.</span></span>

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

## <a name="migrating-old-service-fabric-java-applications-to-be-used-with-maven"></a><span data-ttu-id="5516b-178">Перенос устаревших приложений Java из Service Fabric для использования с Maven</span><span class="sxs-lookup"><span data-stu-id="5516b-178">Migrating old Service Fabric Java applications to be used with Maven</span></span>
<span data-ttu-id="5516b-179">Мы недавно переместили библиотеки Java для Service Fabric из пакета SDK для Java Service Fabric в репозиторий Maven.</span><span class="sxs-lookup"><span data-stu-id="5516b-179">We have recently moved Service Fabric Java libraries from Service Fabric Java SDK to Maven repository.</span></span> <span data-ttu-id="5516b-180">Хотя в новых приложениях, созданных с помощью Yeoman или Eclipse, создаются последние обновленные проекты (которые могут работать с Maven), вы можете обновить существующие приложения Service Fabric Java без отслеживания состояния (или приложения Reliable Actors), в которых ранее использовался пакет SDK для Service Fabric Java, чтобы использовать зависимости Java для Service Fabric из Maven.</span><span class="sxs-lookup"><span data-stu-id="5516b-180">While the new applications you generate using Yeoman or Eclipse, will generate latest updated projects (which will be able to work with Maven), you can update your existing Service Fabric stateless or actor Java applications, which were using the Service Fabric Java SDK earlier, to use the Service Fabric Java dependencies from Maven.</span></span> <span data-ttu-id="5516b-181">Выполните [инструкции](service-fabric-migrate-old-javaapp-to-use-maven.md), чтобы устаревшие приложения могли взаимодействовать с Maven.</span><span class="sxs-lookup"><span data-stu-id="5516b-181">Please follow the steps mentioned [here](service-fabric-migrate-old-javaapp-to-use-maven.md) to ensure your older application works with Maven.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5516b-182">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="5516b-182">Next steps</span></span>

* [<span data-ttu-id="5516b-183">Подключаемый модуль Service Fabric для разработки приложений Eclipse на Java</span><span class="sxs-lookup"><span data-stu-id="5516b-183">Create your first Service Fabric Java application on Linux using Eclipse</span></span>](service-fabric-get-started-eclipse.md)
* [<span data-ttu-id="5516b-184">Общие сведения о надежных субъектах Service Fabric</span><span class="sxs-lookup"><span data-stu-id="5516b-184">Learn more about Reliable Actors</span></span>](service-fabric-reliable-actors-introduction.md)
* <span data-ttu-id="5516b-185">[Azure Service Fabric command line](service-fabric-cli.md) (Командная строка Azure Service Fabric)</span><span class="sxs-lookup"><span data-stu-id="5516b-185">[Interact with Service Fabric clusters using the Service Fabric CLI](service-fabric-cli.md)</span></span>
* <span data-ttu-id="5516b-186">[Сведения о вариантах поддержки Service Fabric](service-fabric-support.md)</span><span class="sxs-lookup"><span data-stu-id="5516b-186">Learn about [Service Fabric support options](service-fabric-support.md)</span></span>
* [<span data-ttu-id="5516b-187">Командная строка Azure Service Fabric</span><span class="sxs-lookup"><span data-stu-id="5516b-187">Getting started with Service Fabric CLI</span></span>](service-fabric-cli.md)

<!-- Images -->
[sf-yeoman]: ./media/service-fabric-create-your-first-linux-application-with-java/sf-yeoman.png
[sfx-primary]: ./media/service-fabric-create-your-first-linux-application-with-java/sfx-primary.png
[sf-eclipse-templates]: ./media/service-fabric-create-your-first-linux-application-with-java/sf-eclipse-templates.png
