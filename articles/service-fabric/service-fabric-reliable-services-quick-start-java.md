---
title: "aaaCreate вашего первого надежного микрослужбу Azure в Java | Документы Microsoft"
description: "Введение toocreating приложении Microsoft Azure Service Fabric с служб без отслеживания состояния и с отслеживанием состояния."
services: service-fabric
documentationcenter: java
author: vturecek
manager: timlt
editor: 
ms.assetid: 7831886f-7ec4-4aef-95c5-b2469a5b7b5d
ms.service: service-fabric
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/29/2017
ms.author: vturecek
ms.openlocfilehash: 577d96591797bbfe6be5c1094426b5f1435cca0f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-reliable-services"></a><span data-ttu-id="7b57f-103">Приступая к работе с надежными службами</span><span class="sxs-lookup"><span data-stu-id="7b57f-103">Get started with Reliable Services</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="7b57f-104">C# в Windows</span><span class="sxs-lookup"><span data-stu-id="7b57f-104">C# on Windows</span></span>](service-fabric-reliable-services-quick-start.md)
> * [<span data-ttu-id="7b57f-105">Java в Linux</span><span class="sxs-lookup"><span data-stu-id="7b57f-105">Java on Linux</span></span>](service-fabric-reliable-services-quick-start-java.md)
>
>

<span data-ttu-id="7b57f-106">Эта статья объясняет основы hello служб Azure Service Fabric надежного и содержит инструкции по созданию и развертыванию простого надежной службы приложения, написанные на языке Java.</span><span class="sxs-lookup"><span data-stu-id="7b57f-106">This article explains hello basics of Azure Service Fabric Reliable Services and walks you through creating and deploying a simple Reliable Service application written in Java.</span></span> <span data-ttu-id="7b57f-107">В этом видеоролике Microsoft Virtual Academy также показано, как toocreate без сохранения состояния надежной службы:<center><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=DOX8K86yC_206218965"></span><span class="sxs-lookup"><span data-stu-id="7b57f-107">This Microsoft Virtual Academy video also shows you how toocreate a stateless Reliable service: <center><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=DOX8K86yC_206218965"></span></span>  
<img src="./media/service-fabric-reliable-services-quick-start-java/ReliableServicesJavaVid.png" WIDTH="360" HEIGHT="244">  
</a></center>

## <a name="installation-and-setup"></a><span data-ttu-id="7b57f-108">Установка и настройка</span><span class="sxs-lookup"><span data-stu-id="7b57f-108">Installation and setup</span></span>
<span data-ttu-id="7b57f-109">Прежде чем начать, убедитесь, что у вас есть на компьютере среды разработки Service Fabric hello.</span><span class="sxs-lookup"><span data-stu-id="7b57f-109">Before you start, make sure you have hello Service Fabric development environment set up on your machine.</span></span>
<span data-ttu-id="7b57f-110">Если вам требуется tooset его, перейдите в слишком[Приступая к работе на Mac](service-fabric-get-started-mac.md) или [Приступая к работе в Linux](service-fabric-get-started-linux.md).</span><span class="sxs-lookup"><span data-stu-id="7b57f-110">If you need tooset it up, go too[getting started on Mac](service-fabric-get-started-mac.md) or [getting started on Linux](service-fabric-get-started-linux.md).</span></span>

## <a name="basic-concepts"></a><span data-ttu-id="7b57f-111">Основные понятия</span><span class="sxs-lookup"><span data-stu-id="7b57f-111">Basic concepts</span></span>
<span data-ttu-id="7b57f-112">tooget к работе с надежного обмена, можно только необходимые toounderstand несколько основных понятий.</span><span class="sxs-lookup"><span data-stu-id="7b57f-112">tooget started with Reliable Services, you only need toounderstand a few basic concepts:</span></span>

* <span data-ttu-id="7b57f-113">**Тип службы**. Это ваша реализация службы.</span><span class="sxs-lookup"><span data-stu-id="7b57f-113">**Service type**: This is your service implementation.</span></span> <span data-ttu-id="7b57f-114">Определяется класс hello написании, расширяющий `StatelessService` и любой другой код или зависимости, используемый в этом документе, а также имя и номер версии.</span><span class="sxs-lookup"><span data-stu-id="7b57f-114">It is defined by hello class you write that extends `StatelessService` and any other code or dependencies used therein, along with a name and a version number.</span></span>
* <span data-ttu-id="7b57f-115">**Именованный экземпляр службы**: toorun службы, можно создавать именованные экземпляры типа службы, гораздо как при создании экземпляра объекта типа класса.</span><span class="sxs-lookup"><span data-stu-id="7b57f-115">**Named service instance**: toorun your service, you create named instances of your service type, much like you create object instances of a class type.</span></span> <span data-ttu-id="7b57f-116">Экземпляры службы фактически являются создаваемыми экземплярами объектов написанного вами класса службы.</span><span class="sxs-lookup"><span data-stu-id="7b57f-116">Service instances are in fact object instantiations of your service class that you write.</span></span>
* <span data-ttu-id="7b57f-117">**Узел службы**: hello именованных экземпляров службы, создайте toorun необходимость внутри узла.</span><span class="sxs-lookup"><span data-stu-id="7b57f-117">**Service host**: hello named service instances you create need toorun inside a host.</span></span> <span data-ttu-id="7b57f-118">узел службы Hello — просто процесса, где можно запускать экземпляры службы.</span><span class="sxs-lookup"><span data-stu-id="7b57f-118">hello service host is just a process where instances of your service can run.</span></span>
* <span data-ttu-id="7b57f-119">**Регистрации службы**. Регистрация объединяет все элементы.</span><span class="sxs-lookup"><span data-stu-id="7b57f-119">**Service registration**: Registration brings everything together.</span></span> <span data-ttu-id="7b57f-120">Hello службы тип должен быть зарегистрирован с hello Service Fabric среды выполнения службы размещения tooallow Service Fabric toocreate его экземпляры toorun.</span><span class="sxs-lookup"><span data-stu-id="7b57f-120">hello service type must be registered with hello Service Fabric runtime in a service host tooallow Service Fabric toocreate instances of it toorun.</span></span>  

## <a name="create-a-stateless-service"></a><span data-ttu-id="7b57f-121">Создание службы без отслеживания состояния</span><span class="sxs-lookup"><span data-stu-id="7b57f-121">Create a stateless service</span></span>
<span data-ttu-id="7b57f-122">Для начала создайте приложение Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="7b57f-122">Start by creating a Service Fabric application.</span></span> <span data-ttu-id="7b57f-123">Hello Service Fabric SDK для Linux включает Yeoman генератор tooprovide hello и формирование шаблонов для приложения Service Fabric в службы без отслеживания состояния.</span><span class="sxs-lookup"><span data-stu-id="7b57f-123">hello Service Fabric SDK for Linux includes a Yeoman generator tooprovide hello scaffolding for a Service Fabric application with a stateless service.</span></span> <span data-ttu-id="7b57f-124">Запустить, выполнив hello следующие Yeoman команды:</span><span class="sxs-lookup"><span data-stu-id="7b57f-124">Start by running hello following Yeoman command:</span></span>

```bash
$ yo azuresfjava
```

<span data-ttu-id="7b57f-125">Следуйте инструкциям toocreate hello **надежной службы без сохранения состояния**.</span><span class="sxs-lookup"><span data-stu-id="7b57f-125">Follow hello instructions toocreate a **Reliable Stateless Service**.</span></span> <span data-ttu-id="7b57f-126">В этом учебнике приложения hello имя «HelloWorldApplication» и hello службы «HelloWorld».</span><span class="sxs-lookup"><span data-stu-id="7b57f-126">For this tutorial, name hello application "HelloWorldApplication" and hello service "HelloWorld".</span></span> <span data-ttu-id="7b57f-127">результат Hello включает в себя каталоги для hello `HelloWorldApplication` и `HelloWorld`.</span><span class="sxs-lookup"><span data-stu-id="7b57f-127">hello result includes directories for hello `HelloWorldApplication` and `HelloWorld`.</span></span>

```bash
HelloWorldApplication/
├── build.gradle
├── HelloWorld
│   ├── build.gradle
│   └── src
│       └── statelessservice
│           ├── HelloWorldServiceHost.java
│           └── HelloWorldService.java
├── HelloWorldApplication
│   ├── ApplicationManifest.xml
│   └── HelloWorldPkg
│       ├── Code
│       │   ├── entryPoint.sh
│       │   └── _readme.txt
│       ├── Config
│       │   └── _readme.txt
│       ├── Data
│       │   └── _readme.txt
│       └── ServiceManifest.xml
├── install.sh
├── settings.gradle
└── uninstall.sh
```

## <a name="implement-hello-service"></a><span data-ttu-id="7b57f-128">Реализация службы hello</span><span class="sxs-lookup"><span data-stu-id="7b57f-128">Implement hello service</span></span>
<span data-ttu-id="7b57f-129">Откройте файл **HelloWorldApplication/HelloWorld/src/statelessservice/HelloWorldService.java**.</span><span class="sxs-lookup"><span data-stu-id="7b57f-129">Open **HelloWorldApplication/HelloWorld/src/statelessservice/HelloWorldService.java**.</span></span> <span data-ttu-id="7b57f-130">Этот класс определяет тип службы hello и запускать программный код.</span><span class="sxs-lookup"><span data-stu-id="7b57f-130">This class defines hello service type, and can run any code.</span></span> <span data-ttu-id="7b57f-131">API-Интерфейс службы Hello предоставляет две точки входа для кода:</span><span class="sxs-lookup"><span data-stu-id="7b57f-131">hello service API provides two entry points for your code:</span></span>

* <span data-ttu-id="7b57f-132">Вызывается метод `runAsync()` с открытой точкой входа, в котором можно начать выполнение любой рабочей нагрузки, например длительных вычислений.</span><span class="sxs-lookup"><span data-stu-id="7b57f-132">An open-ended entry point method, called `runAsync()`, where you can begin executing any workloads, including long-running compute workloads.</span></span>

```java
@Override
protected CompletableFuture<?> runAsync(CancellationToken cancellationToken) {
    ...
}
```

* <span data-ttu-id="7b57f-133">Точка входа связи, где можно подключить любой стек связи по выбору.</span><span class="sxs-lookup"><span data-stu-id="7b57f-133">A communication entry point where you can plug in your communication stack of choice.</span></span> <span data-ttu-id="7b57f-134">С ее помощью вы можете получать запросы от пользователей и других служб.</span><span class="sxs-lookup"><span data-stu-id="7b57f-134">This is where you can start receiving requests from users and other services.</span></span>

```java
@Override
protected List<ServiceInstanceListener> createServiceInstanceListeners() {
    ...
}
```

<span data-ttu-id="7b57f-135">В этом учебнике рассматривается hello `runAsync()` метод точки входа.</span><span class="sxs-lookup"><span data-stu-id="7b57f-135">In this tutorial, we focus on hello `runAsync()` entry point method.</span></span> <span data-ttu-id="7b57f-136">Используя его, вы можете сразу же начать выполнение кода.</span><span class="sxs-lookup"><span data-stu-id="7b57f-136">This is where you can immediately start running your code.</span></span>

### <a name="runasync"></a><span data-ttu-id="7b57f-137">RunAsync</span><span class="sxs-lookup"><span data-stu-id="7b57f-137">RunAsync</span></span>
<span data-ttu-id="7b57f-138">Hello платформа вызывает этот метод при помещенных и готов tooexecute является экземпляр службы.</span><span class="sxs-lookup"><span data-stu-id="7b57f-138">hello platform calls this method when an instance of a service is placed and ready tooexecute.</span></span> <span data-ttu-id="7b57f-139">Для службы без отслеживания состояния, это просто означает при открытии hello экземпляр службы.</span><span class="sxs-lookup"><span data-stu-id="7b57f-139">For a stateless service, that simply means when hello service instance is opened.</span></span> <span data-ttu-id="7b57f-140">Токен отмены, который предоставляется toocoordinate при закрытии toobe вашего экземпляра службы.</span><span class="sxs-lookup"><span data-stu-id="7b57f-140">A cancellation token is provided toocoordinate when your service instance needs toobe closed.</span></span> <span data-ttu-id="7b57f-141">В Service Fabric этого цикла открыть/закрыть экземпляра службы может выполняться много раз за время жизни hello hello службы в целом.</span><span class="sxs-lookup"><span data-stu-id="7b57f-141">In Service Fabric, this open/close cycle of a service instance can occur many times over hello lifetime of hello service as a whole.</span></span> <span data-ttu-id="7b57f-142">Это может происходить по ряду причин.</span><span class="sxs-lookup"><span data-stu-id="7b57f-142">This can happen for various reasons, including:</span></span>

* <span data-ttu-id="7b57f-143">система Hello перемещает экземпляров служб для распределения ресурсов.</span><span class="sxs-lookup"><span data-stu-id="7b57f-143">hello system moves your service instances for resource balancing.</span></span>
* <span data-ttu-id="7b57f-144">В коде возникают ошибки.</span><span class="sxs-lookup"><span data-stu-id="7b57f-144">Faults occur in your code.</span></span>
* <span data-ttu-id="7b57f-145">обновляется Hello приложения или системы.</span><span class="sxs-lookup"><span data-stu-id="7b57f-145">hello application or system is upgraded.</span></span>
* <span data-ttu-id="7b57f-146">Базовое оборудование Hello возникает сбой.</span><span class="sxs-lookup"><span data-stu-id="7b57f-146">hello underlying hardware experiences an outage.</span></span>

<span data-ttu-id="7b57f-147">Это согласование управляется tookeep Service Fabric службы высокой доступности и правильно балансировкой.</span><span class="sxs-lookup"><span data-stu-id="7b57f-147">This orchestration is managed by Service Fabric tookeep your service highly available and properly balanced.</span></span>

<span data-ttu-id="7b57f-148">Реализация `runAsync()` не должна использовать синхронную блокировку.</span><span class="sxs-lookup"><span data-stu-id="7b57f-148">`runAsync()` should not block synchronously.</span></span> <span data-ttu-id="7b57f-149">Реализация runAsync должна возвращать CompletableFuture tooallow hello среды выполнения toocontinue.</span><span class="sxs-lookup"><span data-stu-id="7b57f-149">Your implementation of runAsync should return a CompletableFuture tooallow hello runtime toocontinue.</span></span> <span data-ttu-id="7b57f-150">Если рабочая нагрузка должен tooimplement длительная задача, которая должна выполняться внутри hello CompletableFuture.</span><span class="sxs-lookup"><span data-stu-id="7b57f-150">If your workload needs tooimplement a long running task that should be done inside hello CompletableFuture.</span></span>

#### <a name="cancellation"></a><span data-ttu-id="7b57f-151">Отмена</span><span class="sxs-lookup"><span data-stu-id="7b57f-151">Cancellation</span></span>
<span data-ttu-id="7b57f-152">Отмена рабочей нагрузки является совместной усилий под управлением hello, предоставленный токен отмены.</span><span class="sxs-lookup"><span data-stu-id="7b57f-152">Cancellation of your workload is a cooperative effort orchestrated by hello provided cancellation token.</span></span> <span data-ttu-id="7b57f-153">Hello система ожидает от вашей tooend задачи (от успешного завершения, отмены или сбоя) перед переходом.</span><span class="sxs-lookup"><span data-stu-id="7b57f-153">hello system waits for your task tooend (by successful completion, cancellation, or fault) before it moves on.</span></span> <span data-ttu-id="7b57f-154">Это hello важные toohonor отмены маркера, Готово любой работы и завершить работу `runAsync()` максимально быстро при hello система запрашивает отмену.</span><span class="sxs-lookup"><span data-stu-id="7b57f-154">It is important toohonor hello cancellation token, finish any work, and exit `runAsync()` as quickly as possible when hello system requests cancellation.</span></span> <span data-ttu-id="7b57f-155">Hello следующем примере показано, как toohandle событие отмены:</span><span class="sxs-lookup"><span data-stu-id="7b57f-155">hello following example demonstrates how toohandle a cancellation event:</span></span>

```java
    @Override
    protected CompletableFuture<?> runAsync(CancellationToken cancellationToken) {

        // TODO: Replace hello following sample code with your own logic
        // or remove this runAsync override if it's not needed in your service.

        CompletableFuture.runAsync(() -> {
          long iterations = 0;
          while(true)
          {
            cancellationToken.throwIfCancellationRequested();
            logger.log(Level.INFO, "Working-{0}", ++iterations);

            try
            {
              Thread.sleep(1000);
            }
            catch (IOException ex) {}
          }
        });
    }
```

### <a name="service-registration"></a><span data-ttu-id="7b57f-156">Регистрация службы</span><span class="sxs-lookup"><span data-stu-id="7b57f-156">Service registration</span></span>
<span data-ttu-id="7b57f-157">Типы служб должны быть зарегистрированы с помощью среды выполнения Service Fabric hello.</span><span class="sxs-lookup"><span data-stu-id="7b57f-157">Service types must be registered with hello Service Fabric runtime.</span></span> <span data-ttu-id="7b57f-158">Тип службы Hello определен в hello `ServiceManifest.xml` и класс, реализующий службу `StatelessService`.</span><span class="sxs-lookup"><span data-stu-id="7b57f-158">hello service type is defined in hello `ServiceManifest.xml` and your service class that implements `StatelessService`.</span></span> <span data-ttu-id="7b57f-159">Регистрация службы выполняется в hello процесса главную точку входа.</span><span class="sxs-lookup"><span data-stu-id="7b57f-159">Service registration is performed in hello process main entry point.</span></span> <span data-ttu-id="7b57f-160">В этом примере hello процесс является главной точкой входа `HelloWorldServiceHost.java`:</span><span class="sxs-lookup"><span data-stu-id="7b57f-160">In this example, hello process main entry point is `HelloWorldServiceHost.java`:</span></span>

```java
public static void main(String[] args) throws Exception {
    try {
        ServiceRuntime.registerStatelessServiceAsync("HelloWorldType", (context) -> new HelloWorldService(), Duration.ofSeconds(10));
        logger.log(Level.INFO, "Registered stateless service type HelloWorldType.");
        Thread.sleep(Long.MAX_VALUE);
    }
    catch (Exception ex) {
        logger.log(Level.SEVERE, "Exception in registration:", ex);
        throw ex;
    }
}
```

## <a name="run-hello-application"></a><span data-ttu-id="7b57f-161">Запустите приложение hello</span><span class="sxs-lookup"><span data-stu-id="7b57f-161">Run hello application</span></span>

<span data-ttu-id="7b57f-162">Hello Yeoman формирование шаблонов включает gradle сценария toobuild hello приложения и bash сценарии toodeploy и удалить приложение.</span><span class="sxs-lookup"><span data-stu-id="7b57f-162">hello Yeoman scaffolding includes a gradle script toobuild hello application and bash scripts toodeploy and remove the application.</span></span> <span data-ttu-id="7b57f-163">приложение hello toorun, первое приложение hello сборки с gradle:</span><span class="sxs-lookup"><span data-stu-id="7b57f-163">toorun hello application, first build hello application with gradle:</span></span>

```bash
$ gradle
```

<span data-ttu-id="7b57f-164">Этот сценарий создает пакет приложения Service Fabric, который можно развернуть с помощью интерфейса командной строки Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="7b57f-164">This produces a Service Fabric application package that can be deployed using Service Fabric CLI.</span></span>

### <a name="deploy-with-service-fabric-cli"></a><span data-ttu-id="7b57f-165">Развертывание с помощью интерфейса командной строки Service Fabric</span><span class="sxs-lookup"><span data-stu-id="7b57f-165">Deploy with Service Fabric CLI</span></span>

<span data-ttu-id="7b57f-166">сценарий install.sh Hello содержит hello необходимые службы структуры CLI команды toodeploy hello пакета приложения.</span><span class="sxs-lookup"><span data-stu-id="7b57f-166">hello install.sh script contains hello necessary Service Fabric CLI commands toodeploy hello application package.</span></span> <span data-ttu-id="7b57f-167">Запустите приложение hello toodeploy install.sh скрипта.</span><span class="sxs-lookup"><span data-stu-id="7b57f-167">Run the install.sh script toodeploy hello application.</span></span>

```bash
$ ./install.sh
```

## <a name="next-steps"></a><span data-ttu-id="7b57f-168">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="7b57f-168">Next steps</span></span>

* [<span data-ttu-id="7b57f-169">Командная строка Azure Service Fabric</span><span class="sxs-lookup"><span data-stu-id="7b57f-169">Getting started with Service Fabric CLI</span></span>](service-fabric-cli.md)
