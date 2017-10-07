---
title: "aaaCreate своего первого приложения Azure микрослужбами Linux с использованием C# | Документы Microsoft"
description: "Создание и развертывание приложения Service Fabric с помощью C#"
services: service-fabric
documentationcenter: csharp
author: mani-ramaswamy
manager: timlt
editor: 
ms.assetid: 5a96d21d-fa4a-4dc2-abe8-a830a3482fb1
ms.service: service-fabric
ms.devlang: csharp
ms.topic: hero-article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/21/2017
ms.author: subramar
ms.openlocfilehash: 68d685e130be338ebcdb2f1af24b66d1e14f580a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-first-azure-service-fabric-application"></a><span data-ttu-id="ea53a-103">Создание первого приложения Azure Service Fabric</span><span class="sxs-lookup"><span data-stu-id="ea53a-103">Create your first Azure Service Fabric application</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="ea53a-104">C# для Windows</span><span class="sxs-lookup"><span data-stu-id="ea53a-104">C# - Windows</span></span>](service-fabric-create-your-first-application-in-visual-studio.md)
> * [<span data-ttu-id="ea53a-105">Java для Linux</span><span class="sxs-lookup"><span data-stu-id="ea53a-105">Java - Linux</span></span>](service-fabric-create-your-first-linux-application-with-java.md)
> * [<span data-ttu-id="ea53a-106">C# для Linux</span><span class="sxs-lookup"><span data-stu-id="ea53a-106">C# - Linux</span></span>](service-fabric-create-your-first-linux-application-with-csharp.md)
>
>

<span data-ttu-id="ea53a-107">Service Fabric предоставляет пакеты SDK для создания служб в среде Linux с помощью .NET Core и Java.</span><span class="sxs-lookup"><span data-stu-id="ea53a-107">Service Fabric provides SDKs for building services on Linux in both .NET Core and Java.</span></span> <span data-ttu-id="ea53a-108">В этом учебнике мы рассмотрим, как toocreate приложения для Linux и построения службы с помощью C# (.NET Core).</span><span class="sxs-lookup"><span data-stu-id="ea53a-108">In this tutorial, we look at how toocreate an application for Linux and build a service using C# (.NET Core).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ea53a-109">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="ea53a-109">Prerequisites</span></span>
<span data-ttu-id="ea53a-110">Перед началом работы [настройте среду разработки Linux](service-fabric-get-started-linux.md).</span><span class="sxs-lookup"><span data-stu-id="ea53a-110">Before you get started, make sure that you have [set up your Linux development environment](service-fabric-get-started-linux.md).</span></span> <span data-ttu-id="ea53a-111">Если вы используете Mac OS X, вы можете [настроить универсальную среду Linux на виртуальной машине с помощью Vagrant](service-fabric-get-started-mac.md).</span><span class="sxs-lookup"><span data-stu-id="ea53a-111">If you are using Mac OS X, you can [set up a Linux one-box environment in a virtual machine using Vagrant](service-fabric-get-started-mac.md).</span></span>

<span data-ttu-id="ea53a-112">Необходимо также tooinstall hello [службы структуры CLI](service-fabric-cli.md)</span><span class="sxs-lookup"><span data-stu-id="ea53a-112">You will also want tooinstall hello [Service Fabric CLI](service-fabric-cli.md)</span></span>

### <a name="install-and-set-up-hello-generators-for-csharp"></a><span data-ttu-id="ea53a-113">Установка и настройка генераторы hello для c#</span><span class="sxs-lookup"><span data-stu-id="ea53a-113">Install and set up hello generators for CSharp</span></span>
<span data-ttu-id="ea53a-114">Service Fabric предоставляет средства формирования шаблонов, которые позволяют создавать приложения CSharp в Service Fabric из терминала с помощью генератора шаблонов Yeoman.</span><span class="sxs-lookup"><span data-stu-id="ea53a-114">Service Fabric provides scaffolding tools which will help you create a Service Fabric CSharp application from terminal using Yeoman template generator.</span></span> <span data-ttu-id="ea53a-115">Выполните шаги hello ниже tooensure, у вас есть генератор yeoman шаблона hello Service Fabric для c# работает на компьютере.</span><span class="sxs-lookup"><span data-stu-id="ea53a-115">Please follow hello steps below tooensure you have hello Service Fabric yeoman template generator for CSharp working on your machine.</span></span>
1. <span data-ttu-id="ea53a-116">Установите Node.js и NPM на компьютере.</span><span class="sxs-lookup"><span data-stu-id="ea53a-116">Install nodejs and NPM on your machine</span></span>

  ```bash
  sudo apt-get install npm
  sudo apt install nodejs-legacy
  ```
2. <span data-ttu-id="ea53a-117">Установите на компьютере генератор шаблонов [Yeoman](http://yeoman.io/) из NPM.</span><span class="sxs-lookup"><span data-stu-id="ea53a-117">Install [Yeoman](http://yeoman.io/) template generator on your machine from NPM</span></span>

  ```bash
  sudo npm install -g yo
  ```
3. <span data-ttu-id="ea53a-118">Установка приложения генератора hello Yeo Java структуры службы из NPM</span><span class="sxs-lookup"><span data-stu-id="ea53a-118">Install hello Service Fabric Yeo Java application generator from NPM</span></span>

  ```bash
  sudo npm install -g generator-azuresfcsharp
  ```

## <a name="create-hello-application"></a><span data-ttu-id="ea53a-119">Создание приложения hello</span><span class="sxs-lookup"><span data-stu-id="ea53a-119">Create hello application</span></span>
<span data-ttu-id="ea53a-120">Приложение Service Fabric может содержать одну или несколько служб, каждый с определенной ролью в предоставлении функциональных возможностей приложения hello.</span><span class="sxs-lookup"><span data-stu-id="ea53a-120">A Service Fabric application can contain one or more services, each with a specific role in delivering hello application's functionality.</span></span> <span data-ttu-id="ea53a-121">Hello Service Fabric [Yeoman](http://yeoman.io/) генератор для c#, который устанавливается на последнем шаге, делает его легко toocreate свою первую службу и tooadd более позднее.</span><span class="sxs-lookup"><span data-stu-id="ea53a-121">hello Service Fabric [Yeoman](http://yeoman.io/) generator for CSharp, which you installed in last step, makes it easy toocreate your first service and tooadd more later.</span></span> <span data-ttu-id="ea53a-122">Воспользуемся Yeoman toocreate приложения с одной службой.</span><span class="sxs-lookup"><span data-stu-id="ea53a-122">Let's use Yeoman toocreate an application with a single service.</span></span>

1. <span data-ttu-id="ea53a-123">В конечном введите hello, следующая команда toostart построение hello формирование шаблонов:`yo azuresfcsharp`</span><span class="sxs-lookup"><span data-stu-id="ea53a-123">In a terminal, type hello following command toostart building hello scaffolding: `yo azuresfcsharp`</span></span>
2. <span data-ttu-id="ea53a-124">Присвойте имя приложению.</span><span class="sxs-lookup"><span data-stu-id="ea53a-124">Name your application.</span></span>
3. <span data-ttu-id="ea53a-125">Выберите тип свою первую службу hello и назовите его.</span><span class="sxs-lookup"><span data-stu-id="ea53a-125">Choose hello type of your first service and name it.</span></span> <span data-ttu-id="ea53a-126">Для целей этого учебника hello следует выбрать вариант надежного службу субъектов.</span><span class="sxs-lookup"><span data-stu-id="ea53a-126">For hello purposes of this tutorial, we choose a Reliable Actor Service.</span></span>

   ![Генератор Service Fabric Yeoman для C#][sf-yeoman]

> [!NOTE]
> <span data-ttu-id="ea53a-128">Дополнительные сведения о параметрах hello см. в разделе [Service Fabric, общие сведения о модели программирования](service-fabric-choose-framework.md).</span><span class="sxs-lookup"><span data-stu-id="ea53a-128">For more information about hello options, see [Service Fabric programming model overview](service-fabric-choose-framework.md).</span></span>
>
>

## <a name="build-hello-application"></a><span data-ttu-id="ea53a-129">Создание приложения hello</span><span class="sxs-lookup"><span data-stu-id="ea53a-129">Build hello application</span></span>
<span data-ttu-id="ea53a-130">шаблоны Yeoman структуры службы Hello содержат сценарий построения, которые можно использовать приложение hello toobuild из hello терминалов (после перехода в папке приложения toohello).</span><span class="sxs-lookup"><span data-stu-id="ea53a-130">hello Service Fabric Yeoman templates include a build script that you can use toobuild hello app from hello terminal (after navigating toohello application folder).</span></span>

  ```sh
 cd myapp
 ./build.sh
  ```

## <a name="deploy-hello-application"></a><span data-ttu-id="ea53a-131">Развертывание приложения hello</span><span class="sxs-lookup"><span data-stu-id="ea53a-131">Deploy hello application</span></span>

<span data-ttu-id="ea53a-132">После построения приложения hello, вы можете развернуть локальный кластер toohello.</span><span class="sxs-lookup"><span data-stu-id="ea53a-132">Once hello application is built, you can deploy it toohello local cluster.</span></span>

1. <span data-ttu-id="ea53a-133">Подключите toohello локальный кластер Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="ea53a-133">Connect toohello local Service Fabric cluster.</span></span>

    ```bash
    sfctl cluster select --endpoint http://localhost:19080
    ```

2. <span data-ttu-id="ea53a-134">Сценарий установки выполнения hello в toocopy шаблона hello hello хранилище образов кластера для приложения пакет toohello, регистрация типа приложения hello и создание экземпляра приложения hello.</span><span class="sxs-lookup"><span data-stu-id="ea53a-134">Run hello install script provided in hello template toocopy hello application package toohello cluster's image store, register hello application type, and create an instance of hello application.</span></span>

    ```bash
    ./install.sh
    ```

<span data-ttu-id="ea53a-135">Развертывание приложения hello построения является Здравствуйте таким же, как любое другое приложение Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="ea53a-135">Deploying hello built application is hello same as any other Service Fabric application.</span></span> <span data-ttu-id="ea53a-136">См. в документации hello [управление приложением Service Fabric с hello службы структуры CLI](service-fabric-application-lifecycle-sfctl.md) подробные инструкции.</span><span class="sxs-lookup"><span data-stu-id="ea53a-136">See hello documentation on [managing a Service Fabric application with hello Service Fabric CLI](service-fabric-application-lifecycle-sfctl.md) for detailed instructions.</span></span>

<span data-ttu-id="ea53a-137">Команды toothese параметры можно найти в манифестах hello создан внутри пакета приложения hello.</span><span class="sxs-lookup"><span data-stu-id="ea53a-137">Parameters toothese commands can be found in hello generated manifests inside hello application package.</span></span>

<span data-ttu-id="ea53a-138">После развертывания приложения hello, откройте браузер и перейдите к [Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) в [http://localhost:19080/обозреватель](http://localhost:19080/Explorer).</span><span class="sxs-lookup"><span data-stu-id="ea53a-138">Once hello application has been deployed, open a browser and navigate to [Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) at [http://localhost:19080/Explorer](http://localhost:19080/Explorer).</span></span> <span data-ttu-id="ea53a-139">Разверните hello **приложений** узел и обратите внимание, что теперь есть запись для типа приложения и другой для hello первого экземпляра этого типа.</span><span class="sxs-lookup"><span data-stu-id="ea53a-139">Then, expand hello **Applications** node and note that there is now an entry for your application type and another for hello first instance of that type.</span></span>

## <a name="start-hello-test-client-and-perform-a-failover"></a><span data-ttu-id="ea53a-140">Запустите тестовый клиент hello и отработка отказа</span><span class="sxs-lookup"><span data-stu-id="ea53a-140">Start hello test client and perform a failover</span></span>
<span data-ttu-id="ea53a-141">Проекты субъекта предполагают использование дополнительных средств.</span><span class="sxs-lookup"><span data-stu-id="ea53a-141">Actor projects do not do anything on their own.</span></span> <span data-ttu-id="ea53a-142">Они требуют другой службой или клиентом toosend их сообщений.</span><span class="sxs-lookup"><span data-stu-id="ea53a-142">They require another service or client toosend them messages.</span></span> <span data-ttu-id="ea53a-143">шаблон субъекта Hello включает простой тестовый скрипт, можно использовать toointeract с службу субъектов hello.</span><span class="sxs-lookup"><span data-stu-id="ea53a-143">hello actor template includes a simple test script that you can use toointeract with hello actor service.</span></span>

1. <span data-ttu-id="ea53a-144">Запустите скрипт hello, используя hello Контрольные значения программа toosee hello выходные данные hello субъекта службы.</span><span class="sxs-lookup"><span data-stu-id="ea53a-144">Run hello script using hello watch utility toosee hello output of hello actor service.</span></span>

    ```bash
    cd myactorsvcTestClient
    watch -n 1 ./testclient.sh
    ```
2. <span data-ttu-id="ea53a-145">В обозреватель Service Fabric найдите узел размещения hello первичной реплики для службы субъекта hello.</span><span class="sxs-lookup"><span data-stu-id="ea53a-145">In Service Fabric Explorer, locate node hosting hello primary replica for hello actor service.</span></span> <span data-ttu-id="ea53a-146">В приведенном далее снимке экрана приветствия это узел 3.</span><span class="sxs-lookup"><span data-stu-id="ea53a-146">In hello screenshot below, it is node 3.</span></span>

    ![Поиск hello первичной реплики в обозреватель Service Fabric][sfx-primary]
3. <span data-ttu-id="ea53a-148">Щелкните узел hello можно найти в предыдущем шаге hello, а затем выберите **деактивировать (перезапустите)** из меню "действия" hello.</span><span class="sxs-lookup"><span data-stu-id="ea53a-148">Click hello node you found in hello previous step, then select **Deactivate (restart)** from hello Actions menu.</span></span> <span data-ttu-id="ea53a-149">Это действие перезапускает один узел в локальном принудительного перехода на другой ресурс tooa вторичной реплики, запущенный на другом узле кластера.</span><span class="sxs-lookup"><span data-stu-id="ea53a-149">This action restarts one node in your local cluster forcing a failover tooa secondary replica running on another node.</span></span> <span data-ttu-id="ea53a-150">При выполнении этого действия, Обратите внимания toohello вывода из тестового клиента hello и обратите внимание, что счетчика hello продолжается tooincrement несмотря на hello перехода на другой ресурс.</span><span class="sxs-lookup"><span data-stu-id="ea53a-150">As you perform this action, pay attention toohello output from hello test client and note that hello counter continues tooincrement despite hello failover.</span></span>

## <a name="adding-more-services-tooan-existing-application"></a><span data-ttu-id="ea53a-151">Добавление существующего приложения tooan дополнительные службы</span><span class="sxs-lookup"><span data-stu-id="ea53a-151">Adding more services tooan existing application</span></span>

<span data-ttu-id="ea53a-152">tooadd другой tooan приложение службы уже созданные с помощью `yo`, выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="ea53a-152">tooadd another service tooan application already created using `yo`, perform hello following steps:</span></span>
1. <span data-ttu-id="ea53a-153">Измените корневой каталог toohello существующее приложение hello.</span><span class="sxs-lookup"><span data-stu-id="ea53a-153">Change directory toohello root of hello existing application.</span></span>  <span data-ttu-id="ea53a-154">Например `cd ~/YeomanSamples/MyApplication`, если `MyApplication` является приложение hello, созданных Yeoman.</span><span class="sxs-lookup"><span data-stu-id="ea53a-154">For example, `cd ~/YeomanSamples/MyApplication`, if `MyApplication` is hello application created by Yeoman.</span></span>
2. <span data-ttu-id="ea53a-155">Запустите `yo azuresfcsharp:AddService`</span><span class="sxs-lookup"><span data-stu-id="ea53a-155">Run `yo azuresfcsharp:AddService`</span></span>

## <a name="migrating-from-projectjson-toocsproj"></a><span data-ttu-id="ea53a-156">Миграция с project.json too.csproj</span><span class="sxs-lookup"><span data-stu-id="ea53a-156">Migrating from project.json too.csproj</span></span>
1. <span data-ttu-id="ea53a-157">Выполнение «перенос dotnet» в корневом каталоге проекта выполнит миграцию всех hello project.json toocsproj формат.</span><span class="sxs-lookup"><span data-stu-id="ea53a-157">Running 'dotnet migrate' in project root directory will migrate all hello project.json toocsproj format.</span></span>
2. <span data-ttu-id="ea53a-158">Обновление hello проект ссылается на соответствующим образом toocsproj файлов проекта.</span><span class="sxs-lookup"><span data-stu-id="ea53a-158">Update hello project references accordingly toocsproj files in project files.</span></span>
3. <span data-ttu-id="ea53a-159">Обновите файлы toocsproj имена файла проекта hello в build.sh.</span><span class="sxs-lookup"><span data-stu-id="ea53a-159">Update hello project file names toocsproj files in build.sh.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ea53a-160">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="ea53a-160">Next steps</span></span>

* [<span data-ttu-id="ea53a-161">Общие сведения о надежных субъектах Service Fabric</span><span class="sxs-lookup"><span data-stu-id="ea53a-161">Learn more about Reliable Actors</span></span>](service-fabric-reliable-actors-introduction.md)
* [<span data-ttu-id="ea53a-162">Взаимодействие с кластерами Service Fabric, с помощью службы структуры CLI hello</span><span class="sxs-lookup"><span data-stu-id="ea53a-162">Interacting with Service Fabric clusters using hello Service Fabric CLI</span></span>](service-fabric-cli.md)
* <span data-ttu-id="ea53a-163">[Сведения о вариантах поддержки Service Fabric](service-fabric-support.md)</span><span class="sxs-lookup"><span data-stu-id="ea53a-163">Learn about [Service Fabric support options](service-fabric-support.md)</span></span>
* [<span data-ttu-id="ea53a-164">Командная строка Azure Service Fabric</span><span class="sxs-lookup"><span data-stu-id="ea53a-164">Getting started with Service Fabric CLI</span></span>](service-fabric-cli.md)

<!-- Images -->
[sf-yeoman]: ./media/service-fabric-create-your-first-linux-application-with-csharp/yeoman-csharp.png
[sfx-primary]: ./media/service-fabric-create-your-first-linux-application-with-csharp/sfx-primary.png
