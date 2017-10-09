---
title: "aaaCreate вашего первого на основе субъектов Azure микрослужбу в Java | Документы Microsoft"
description: "Этот учебник поможет выполнить шаги создания, отладки и развертывания простой службы на основе субъектов, с помощью службы структуры службы Reliable Actor hello."
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: 
ms.assetid: d31dc8ab-9760-4619-a641-facb8324c759
ms.service: service-fabric
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 01/04/2017
ms.author: vturecek
ms.openlocfilehash: 24718a8d7034360c53597f139169580f1a6ce732
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-reliable-actors"></a><span data-ttu-id="69788-103">Приступая к работе с Reliable Actors</span><span class="sxs-lookup"><span data-stu-id="69788-103">Getting started with Reliable Actors</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="69788-104">C# в Windows</span><span class="sxs-lookup"><span data-stu-id="69788-104">C# on Windows</span></span>](service-fabric-reliable-actors-get-started.md)
> * [<span data-ttu-id="69788-105">Java в Linux</span><span class="sxs-lookup"><span data-stu-id="69788-105">Java on Linux</span></span>](service-fabric-reliable-actors-get-started-java.md)
> 
> 

<span data-ttu-id="69788-106">Эта статья объясняет основы hello Azure Service Fabric Reliable Actors и содержит инструкции по созданию и развертыванию простого приложения Reliable Actor в Java.</span><span class="sxs-lookup"><span data-stu-id="69788-106">This article explains hello basics of Azure Service Fabric Reliable Actors and walks you through creating and deploying a simple Reliable Actor application in Java.</span></span>

## <a name="installation-and-setup"></a><span data-ttu-id="69788-107">Установка и настройка</span><span class="sxs-lookup"><span data-stu-id="69788-107">Installation and setup</span></span>
<span data-ttu-id="69788-108">Прежде чем начать, убедитесь, что у вас есть на компьютере среды разработки Service Fabric hello.</span><span class="sxs-lookup"><span data-stu-id="69788-108">Before you start, make sure you have hello Service Fabric development environment set up on your machine.</span></span>
<span data-ttu-id="69788-109">Если вам требуется tooset его, перейдите в слишком[Приступая к работе на Mac](service-fabric-get-started-mac.md) или [Приступая к работе в Linux](service-fabric-get-started-linux.md).</span><span class="sxs-lookup"><span data-stu-id="69788-109">If you need tooset it up, go too[getting started on Mac](service-fabric-get-started-mac.md) or [getting started on Linux](service-fabric-get-started-linux.md).</span></span>

## <a name="basic-concepts"></a><span data-ttu-id="69788-110">Основные понятия</span><span class="sxs-lookup"><span data-stu-id="69788-110">Basic concepts</span></span>
<span data-ttu-id="69788-111">tooget выполнению службы Reliable Actor, нужно только необходимые toounderstand несколько основных понятий.</span><span class="sxs-lookup"><span data-stu-id="69788-111">tooget started with Reliable Actors, you only need toounderstand a few basic concepts:</span></span>

* <span data-ttu-id="69788-112">**Служба субъекта**.</span><span class="sxs-lookup"><span data-stu-id="69788-112">**Actor service**.</span></span> <span data-ttu-id="69788-113">Службы Reliable Actor упакованы в надежные службы, которая может быть развернута в инфраструктуре Service Fabric hello.</span><span class="sxs-lookup"><span data-stu-id="69788-113">Reliable Actors are packaged in Reliable Services that can be deployed in hello Service Fabric infrastructure.</span></span> <span data-ttu-id="69788-114">Экземпляры субъектов активируются в именованном экземпляре службы.</span><span class="sxs-lookup"><span data-stu-id="69788-114">Actor instances are activated in a named service instance.</span></span>
* <span data-ttu-id="69788-115">**Регистрация субъекта**.</span><span class="sxs-lookup"><span data-stu-id="69788-115">**Actor registration**.</span></span> <span data-ttu-id="69788-116">Как с помощью надежного обмена службы Reliable Actor должен toobe зарегистрирована среда выполнения Service Fabric hello.</span><span class="sxs-lookup"><span data-stu-id="69788-116">As with Reliable Services, a Reliable Actor service needs toobe registered with hello Service Fabric runtime.</span></span> <span data-ttu-id="69788-117">Кроме того тип субъекта hello должен toobe зарегистрирован со средой выполнения hello субъекта.</span><span class="sxs-lookup"><span data-stu-id="69788-117">In addition, hello actor type needs toobe registered with hello Actor runtime.</span></span>
* <span data-ttu-id="69788-118">**Интерфейс субъекта**.</span><span class="sxs-lookup"><span data-stu-id="69788-118">**Actor interface**.</span></span> <span data-ttu-id="69788-119">интерфейс Hello субъекта является toodefine используется строго типизированный открытый интерфейс субъекта.</span><span class="sxs-lookup"><span data-stu-id="69788-119">hello actor interface is used toodefine a strongly typed public interface of an actor.</span></span> <span data-ttu-id="69788-120">В hello терминологии модели Reliable Actor hello субъекта интерфейс определяет hello может понять и обрабатывать типы сообщений, которые hello субъекта.</span><span class="sxs-lookup"><span data-stu-id="69788-120">In hello Reliable Actor model terminology, hello actor interface defines hello types of messages that hello actor can understand and process.</span></span> <span data-ttu-id="69788-121">интерфейс Hello субъекта используется другим субъектам и клиентские приложения слишком «отправить» (асинхронно) субъекта toohello сообщений.</span><span class="sxs-lookup"><span data-stu-id="69788-121">hello actor interface is used by other actors and client applications too"send" (asynchronously) messages toohello actor.</span></span> <span data-ttu-id="69788-122">Субъекты Reliable Actors могут реализовывать несколько интерфейсов.</span><span class="sxs-lookup"><span data-stu-id="69788-122">Reliable Actors can implement multiple interfaces.</span></span>
* <span data-ttu-id="69788-123">**Класс ActorProxy**.</span><span class="sxs-lookup"><span data-stu-id="69788-123">**ActorProxy class**.</span></span> <span data-ttu-id="69788-124">Hello класс ActorProxy используется tooinvoke клиентского приложения hello методы, предоставляемые через интерфейс hello субъекта.</span><span class="sxs-lookup"><span data-stu-id="69788-124">hello ActorProxy class is used by client applications tooinvoke hello methods exposed through hello actor interface.</span></span> <span data-ttu-id="69788-125">Hello ActorProxy класс предоставляет две важные функции:</span><span class="sxs-lookup"><span data-stu-id="69788-125">hello ActorProxy class provides two important functionalities:</span></span>
  
  * <span data-ttu-id="69788-126">Разрешение имен: это может toolocate hello субъекта в кластере hello (поиск hello узел кластера hello, где размещается).</span><span class="sxs-lookup"><span data-stu-id="69788-126">Name resolution: It is able toolocate hello actor in hello cluster (find hello node of hello cluster where it is hosted).</span></span>
  * <span data-ttu-id="69788-127">Обработка сбоев: он повторите вызовы методов и повторно разрешить расположение субъекта hello после, например, сбой, который требует toobe субъекта hello переместить tooanother узел в кластере hello.</span><span class="sxs-lookup"><span data-stu-id="69788-127">Failure handling: It can retry method invocations and re-resolve hello actor location after, for example, a failure that requires hello actor toobe relocated tooanother node in hello cluster.</span></span>

<span data-ttu-id="69788-128">следующие правила, которые относятся интерфейсы tooactor Hello, следует отметить:</span><span class="sxs-lookup"><span data-stu-id="69788-128">hello following rules that pertain tooactor interfaces are worth mentioning:</span></span>

* <span data-ttu-id="69788-129">методы интерфейса субъекта не могут быть перегружены;</span><span class="sxs-lookup"><span data-stu-id="69788-129">Actor interface methods cannot be overloaded.</span></span>
* <span data-ttu-id="69788-130">методы интерфейса субъекта не должны иметь выходных, ссылочных или необязательных параметров.</span><span class="sxs-lookup"><span data-stu-id="69788-130">Actor interface methods must not have out, ref, or optional parameters.</span></span>
* <span data-ttu-id="69788-131">универсальные интерфейсы не поддерживаются.</span><span class="sxs-lookup"><span data-stu-id="69788-131">Generic interfaces are not supported.</span></span>

## <a name="create-an-actor-service"></a><span data-ttu-id="69788-132">Создание службы субъекта</span><span class="sxs-lookup"><span data-stu-id="69788-132">Create an actor service</span></span>
<span data-ttu-id="69788-133">Сначала создайте приложение Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="69788-133">Start by creating a new Service Fabric application.</span></span> <span data-ttu-id="69788-134">Hello Service Fabric SDK для Linux включает Yeoman генератор tooprovide hello и формирование шаблонов для приложения Service Fabric в службы без отслеживания состояния.</span><span class="sxs-lookup"><span data-stu-id="69788-134">hello Service Fabric SDK for Linux includes a Yeoman generator tooprovide hello scaffolding for a Service Fabric application with a stateless service.</span></span> <span data-ttu-id="69788-135">Запустить, выполнив hello следующие Yeoman команды:</span><span class="sxs-lookup"><span data-stu-id="69788-135">Start by running hello following Yeoman command:</span></span>

```bash
$ yo azuresfjava
```

<span data-ttu-id="69788-136">Следуйте инструкциям toocreate hello **надежной службы субъекта**.</span><span class="sxs-lookup"><span data-stu-id="69788-136">Follow hello instructions toocreate a **Reliable Actor Service**.</span></span> <span data-ttu-id="69788-137">Для этого учебника назовите hello приложения «HelloWorldActorApplication» и hello субъект «HelloWorldActor».</span><span class="sxs-lookup"><span data-stu-id="69788-137">For this tutorial, name hello application "HelloWorldActorApplication" and hello actor "HelloWorldActor."</span></span> <span data-ttu-id="69788-138">будет создана Hello после формирования шаблонов:</span><span class="sxs-lookup"><span data-stu-id="69788-138">hello following scaffolding will be created:</span></span>

```bash
HelloWorldActorApplication/
├── build.gradle
├── HelloWorldActor
│   ├── build.gradle
│   ├── settings.gradle
│   └── src
│       └── reliableactor
│           ├── HelloWorldActorHost.java
│           └── HelloWorldActorImpl.java
├── HelloWorldActorApplication
│   ├── ApplicationManifest.xml
│   └── HelloWorldActorPkg
│       ├── Code
│       │   ├── entryPoint.sh
│       │   └── _readme.txt
│       ├── Config
│       │   ├── _readme.txt
│       │   └── Settings.xml
│       ├── Data
│       │   └── _readme.txt
│       └── ServiceManifest.xml
├── HelloWorldActorInterface
│   ├── build.gradle
│   └── src
│       └── reliableactor
│           └── HelloWorldActor.java
├── HelloWorldActorTestClient
│   ├── build.gradle
│   ├── settings.gradle
│   ├── src
│   │   └── reliableactor
│   │       └── test
│   │           └── HelloWorldActorTestClient.java
│   └── testclient.sh
├── install.sh
├── settings.gradle
└── uninstall.sh
```

## <a name="reliable-actors-basic-building-blocks"></a><span data-ttu-id="69788-139">Простые стандартные блоки в решении на базе надежных субъектов</span><span class="sxs-lookup"><span data-stu-id="69788-139">Reliable Actors basic building blocks</span></span>
<span data-ttu-id="69788-140">описанные выше основные понятия Hello переводиться hello основные стандартные блоки службы Reliable Actor.</span><span class="sxs-lookup"><span data-stu-id="69788-140">hello basic concepts described earlier translate into hello basic building blocks of a Reliable Actor service.</span></span>

### <a name="actor-interface"></a><span data-ttu-id="69788-141">Интерфейс субъекта</span><span class="sxs-lookup"><span data-stu-id="69788-141">Actor interface</span></span>
<span data-ttu-id="69788-142">Содержит определение интерфейса hello для субъекта hello.</span><span class="sxs-lookup"><span data-stu-id="69788-142">This contains hello interface definition for hello actor.</span></span> <span data-ttu-id="69788-143">Этот интерфейс определяет контракт hello субъект, который является общим для hello субъекта реализация и вызов hello субъект, поэтому он обычно смысле toodefine его в месте, которое отделить от реализации субъекта hello и могут использоваться в нескольких других клиентов hello службы или клиентского приложения.</span><span class="sxs-lookup"><span data-stu-id="69788-143">This interface defines hello actor contract that is shared by hello actor implementation and hello clients calling hello actor, so it typically makes sense toodefine it in a place that is separate from hello actor implementation and can be shared by multiple other services or client applications.</span></span>

<span data-ttu-id="69788-144">`HelloWorldActorInterface/src/reliableactor/HelloWorldActor.java`:</span><span class="sxs-lookup"><span data-stu-id="69788-144">`HelloWorldActorInterface/src/reliableactor/HelloWorldActor.java`:</span></span>

```java
public interface HelloWorldActor extends Actor {
    @Readonly   
    CompletableFuture<Integer> getCountAsync();

    CompletableFuture<?> setCountAsync(int count);
}
```

### <a name="actor-service"></a><span data-ttu-id="69788-145">Служба субъекта</span><span class="sxs-lookup"><span data-stu-id="69788-145">Actor service</span></span>
<span data-ttu-id="69788-146">Служба субъекта содержит реализацию и код регистрации субъекта.</span><span class="sxs-lookup"><span data-stu-id="69788-146">This contains your actor implementation and actor registration code.</span></span> <span data-ttu-id="69788-147">Hello субъекта класс реализует интерфейс hello субъекта.</span><span class="sxs-lookup"><span data-stu-id="69788-147">hello actor class implements hello actor interface.</span></span> <span data-ttu-id="69788-148">Здесь субъект выполняет свою работу.</span><span class="sxs-lookup"><span data-stu-id="69788-148">This is where your actor does its work.</span></span>

<span data-ttu-id="69788-149">`HelloWorldActor/src/reliableactor/HelloWorldActorImpl`:</span><span class="sxs-lookup"><span data-stu-id="69788-149">`HelloWorldActor/src/reliableactor/HelloWorldActorImpl`:</span></span>

```java
@ActorServiceAttribute(name = "HelloWorldActor.HelloWorldActorService")
@StatePersistenceAttribute(statePersistence = StatePersistence.Persisted)
public class HelloWorldActorImpl extends ReliableActor implements HelloWorldActor {
    Logger logger = Logger.getLogger(this.getClass().getName());

    protected CompletableFuture<?> onActivateAsync() {
        logger.log(Level.INFO, "onActivateAsync");

        return this.stateManager().tryAddStateAsync("count", 0);
    }

    @Override
    public CompletableFuture<Integer> getCountAsync() {
        logger.log(Level.INFO, "Getting current count value");
        return this.stateManager().getStateAsync("count");
    }

    @Override
    public CompletableFuture<?> setCountAsync(int count) {
        logger.log(Level.INFO, "Setting current count value {0}", count);
        return this.stateManager().addOrUpdateStateAsync("count", count, (key, value) -> count > value ? count : value);
    }
}
```

### <a name="actor-registration"></a><span data-ttu-id="69788-150">Регистрация субъекта</span><span class="sxs-lookup"><span data-stu-id="69788-150">Actor registration</span></span>
<span data-ttu-id="69788-151">необходимо зарегистрировать службу Hello субъекта с типом службы в среде выполнения Service Fabric hello.</span><span class="sxs-lookup"><span data-stu-id="69788-151">hello actor service must be registered with a service type in hello Service Fabric runtime.</span></span> <span data-ttu-id="69788-152">В порядок hello toorun службу субъектов субъекта экземпляры, тип субъекта также должен быть зарегистрирован с hello службу субъектов.</span><span class="sxs-lookup"><span data-stu-id="69788-152">In order for hello Actor Service toorun your actor instances, your actor type must also be registered with hello Actor Service.</span></span> <span data-ttu-id="69788-153">Hello `ActorRuntime` метод регистрации выполняет это действие для субъектов.</span><span class="sxs-lookup"><span data-stu-id="69788-153">hello `ActorRuntime` registration method performs this work for actors.</span></span>

<span data-ttu-id="69788-154">`HelloWorldActor/src/reliableactor/HelloWorldActorHost`:</span><span class="sxs-lookup"><span data-stu-id="69788-154">`HelloWorldActor/src/reliableactor/HelloWorldActorHost`:</span></span>

```java
public class HelloWorldActorHost {

    public static void main(String[] args) throws Exception {

        try {
            ActorRuntime.registerActorAsync(HelloWorldActorImpl.class, (context, actorType) -> new ActorServiceImpl(context, actorType, ()-> new HelloWorldActorImpl()), Duration.ofSeconds(10));

            Thread.sleep(Long.MAX_VALUE);

        } catch (Exception e) {
            e.printStackTrace();
            throw e;
        }
    }
}
```

### <a name="test-client"></a><span data-ttu-id="69788-155">Тестовый клиент</span><span class="sxs-lookup"><span data-stu-id="69788-155">Test client</span></span>
<span data-ttu-id="69788-156">Это простое тестовое приложение клиента можно запускать отдельно от tootest приложения Service Fabric hello службы субъекта.</span><span class="sxs-lookup"><span data-stu-id="69788-156">This is a simple test client application you can run separately from hello Service Fabric application tootest your actor service.</span></span> <span data-ttu-id="69788-157">Это пример из где hello ActorProxy можно использовать tooactivate и взаимодействия с экземплярами субъекта.</span><span class="sxs-lookup"><span data-stu-id="69788-157">This is an example of where hello ActorProxy can be used tooactivate and communicate with actor instances.</span></span> <span data-ttu-id="69788-158">Он не развертывается с вашей службой.</span><span class="sxs-lookup"><span data-stu-id="69788-158">It does not get deployed with your service.</span></span>

### <a name="hello-application"></a><span data-ttu-id="69788-159">приложение Hello</span><span class="sxs-lookup"><span data-stu-id="69788-159">hello application</span></span>
<span data-ttu-id="69788-160">Наконец пакеты приложения hello hello субъекта-службы и другие службы, который может быть добавлена в hello будущих вместе для развертывания.</span><span class="sxs-lookup"><span data-stu-id="69788-160">Finally, hello application packages hello actor service and any other services you might add in hello future together for deployment.</span></span> <span data-ttu-id="69788-161">Он содержит hello *ApplicationManifest.xml* и заполнителями для пакета службы субъекта hello.</span><span class="sxs-lookup"><span data-stu-id="69788-161">It contains hello *ApplicationManifest.xml* and place holders for hello actor service package.</span></span>

## <a name="run-hello-application"></a><span data-ttu-id="69788-162">Запустите приложение hello</span><span class="sxs-lookup"><span data-stu-id="69788-162">Run hello application</span></span>

<span data-ttu-id="69788-163">Hello Yeoman формирование шаблонов включает gradle сценария toobuild hello приложения и bash сценарии toodeploy и удалить приложение.</span><span class="sxs-lookup"><span data-stu-id="69788-163">hello Yeoman scaffolding includes a gradle script toobuild hello application and bash scripts toodeploy and remove the application.</span></span> <span data-ttu-id="69788-164">приложение hello toodeploy, первое приложение hello сборки с gradle:</span><span class="sxs-lookup"><span data-stu-id="69788-164">toodeploy hello application, first build hello application with gradle:</span></span>

```bash
$ gradle
```

<span data-ttu-id="69788-165">Этот сценарий создаст пакет приложения Service Fabric, который можно развернуть с помощью инструментов интерфейса командной строки Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="69788-165">This will produce a Service Fabric application package that can be deployed using Service Fabric CLI tools.</span></span>

### <a name="deploy-service-fabric-cli"></a><span data-ttu-id="69788-166">Развертывание интерфейса командной строки Service Fabric</span><span class="sxs-lookup"><span data-stu-id="69788-166">Deploy Service Fabric CLI</span></span>

<span data-ttu-id="69788-167">сценарий install.sh Hello содержит hello необходимые службы структуры CLI (sfctl) команды toodeploy hello пакета приложения.</span><span class="sxs-lookup"><span data-stu-id="69788-167">hello install.sh script contains hello necessary Service Fabric CLI (sfctl) commands toodeploy hello application package.</span></span>
<span data-ttu-id="69788-168">Запустите приложение hello install.sh сценария toodeploy hello.</span><span class="sxs-lookup"><span data-stu-id="69788-168">Run hello install.sh script toodeploy hello application.</span></span>

```bash
$ ./install.sh
```

## <a name="next-steps"></a><span data-ttu-id="69788-169">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="69788-169">Next steps</span></span>

* [<span data-ttu-id="69788-170">Командная строка Azure Service Fabric</span><span class="sxs-lookup"><span data-stu-id="69788-170">Getting started with Service Fabric CLI</span></span>](service-fabric-cli.md)
