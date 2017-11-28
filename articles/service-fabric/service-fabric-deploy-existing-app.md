---
title: "aaaDeploy существующего исполняемого tooAzure Service Fabric | Документы Microsoft"
description: "Пошаговое руководство по развертыванию кластера Service Fabric tooa toopackage существующее приложение в качестве гостевой исполняемый файл, поэтому он может быть"
services: service-fabric
documentationcenter: .net
author: msfussell
manager: timlt
editor: 
ms.assetid: d799c1c6-75eb-4b8a-9f94-bf4f3dadf4c3
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 07/02/2017
ms.author: mfussell;mikhegn
ms.openlocfilehash: 5599802bdb6bda2407a138d77e12148ccb64f437
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-guest-executable-tooservice-fabric"></a><span data-ttu-id="f7f65-103">Развертывание гостевого исполняемого tooService структуры</span><span class="sxs-lookup"><span data-stu-id="f7f65-103">Deploy a guest executable tooService Fabric</span></span>
<span data-ttu-id="f7f65-104">В Azure Service Fabric можно запустить как службу приложение любого типа, в том числе приложения Node.js, Java или C++.</span><span class="sxs-lookup"><span data-stu-id="f7f65-104">You can run any type of code, such as Node.js, Java, or C++ in Azure Service Fabric as a service.</span></span> <span data-ttu-id="f7f65-105">Service Fabric toothese типов служб называется гостевой исполняемые файлы.</span><span class="sxs-lookup"><span data-stu-id="f7f65-105">Service Fabric refers toothese types of services as guest executables.</span></span>

<span data-ttu-id="f7f65-106">Гостевые исполняемые файлы обрабатываются в Service Fabric как службы без отслеживания состояния.</span><span class="sxs-lookup"><span data-stu-id="f7f65-106">Guest executables are treated by Service Fabric like stateless services.</span></span> <span data-ttu-id="f7f65-107">Это значит, что они будут размещены на узлах кластера на основе доступности и других метрик.</span><span class="sxs-lookup"><span data-stu-id="f7f65-107">As a result, they are placed on nodes in a cluster, based on availability and other metrics.</span></span> <span data-ttu-id="f7f65-108">В этой статье описывается как toopackage и развернуть гостевой кластер Service Fabric tooa исполняемый файл с помощью Visual Studio или программы командной строки.</span><span class="sxs-lookup"><span data-stu-id="f7f65-108">This article describes how toopackage and deploy a guest executable tooa Service Fabric cluster, by using Visual Studio or a command-line utility.</span></span>

<span data-ttu-id="f7f65-109">В этой статье мы охватывают действия hello toopackage гостевой исполняемый файл и разверните его tooService структуры.</span><span class="sxs-lookup"><span data-stu-id="f7f65-109">In this article, we cover hello steps toopackage a guest executable and deploy it tooService Fabric.</span></span>  

## <a name="benefits-of-running-a-guest-executable-in-service-fabric"></a><span data-ttu-id="f7f65-110">Преимущества запуска гостевого исполняемого файла в Service Fabric</span><span class="sxs-lookup"><span data-stu-id="f7f65-110">Benefits of running a guest executable in Service Fabric</span></span>
<span data-ttu-id="f7f65-111">Существует несколько преимуществ toorunning гостевой исполняемый объект в кластер Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="f7f65-111">There are several advantages toorunning a guest executable in a Service Fabric cluster:</span></span>

* <span data-ttu-id="f7f65-112">обеспечение высокой доступности;</span><span class="sxs-lookup"><span data-stu-id="f7f65-112">High availability.</span></span> <span data-ttu-id="f7f65-113">Приложения, работающие в среде Service Fabric, отличаются высоким уровнем доступности.</span><span class="sxs-lookup"><span data-stu-id="f7f65-113">Applications that run in Service Fabric are made highly available.</span></span> <span data-ttu-id="f7f65-114">Service Fabric обеспечивает выполнение экземпляров приложения.</span><span class="sxs-lookup"><span data-stu-id="f7f65-114">Service Fabric ensures that instances of an application are running.</span></span>
* <span data-ttu-id="f7f65-115">Наблюдение за работоспособностью системы.</span><span class="sxs-lookup"><span data-stu-id="f7f65-115">Health monitoring.</span></span> <span data-ttu-id="f7f65-116">Service Fabric наблюдает за работоспособностью приложений и в случае сбоя предоставляет диагностические данные.</span><span class="sxs-lookup"><span data-stu-id="f7f65-116">Service Fabric health monitoring detects if an application is running, and provides diagnostic information if there is a failure.</span></span>   
* <span data-ttu-id="f7f65-117">Управление жизненным циклом приложений.</span><span class="sxs-lookup"><span data-stu-id="f7f65-117">Application lifecycle management.</span></span> <span data-ttu-id="f7f65-118">Помимо обновления без простоев, Service Fabric предоставляет автоматического отката toohello предыдущей версии, если событие работоспособности неправильный отчет во время обновления.</span><span class="sxs-lookup"><span data-stu-id="f7f65-118">Besides providing upgrades with no downtime, Service Fabric provides automatic rollback toohello previous version if there is a bad health event reported during an upgrade.</span></span>    
* <span data-ttu-id="f7f65-119">Плотность.</span><span class="sxs-lookup"><span data-stu-id="f7f65-119">Density.</span></span> <span data-ttu-id="f7f65-120">В кластере, что исключает необходимость hello для каждого приложения toorun на собственное оборудование, можно запускать несколько приложений.</span><span class="sxs-lookup"><span data-stu-id="f7f65-120">You can run multiple applications in a cluster, which eliminates hello need for each application toorun on its own hardware.</span></span>
* <span data-ttu-id="f7f65-121">Возможность обнаружения: С помощью REST можно вызвать toofind служба именования Service Fabric hello другие службы в кластере hello.</span><span class="sxs-lookup"><span data-stu-id="f7f65-121">Discoverability: Using REST you can call hello Service Fabric Naming service toofind other services in hello cluster.</span></span> 

## <a name="samples"></a><span data-ttu-id="f7f65-122">Примеры</span><span class="sxs-lookup"><span data-stu-id="f7f65-122">Samples</span></span>
* [<span data-ttu-id="f7f65-123">Пример для упаковки и развертывания гостевого исполняемого файла</span><span class="sxs-lookup"><span data-stu-id="f7f65-123">Sample for packaging and deploying a guest executable</span></span>](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started)
* [<span data-ttu-id="f7f65-124">Пример двух гостевой исполняемых файлов (C# и nodejs) общения с помощью службы именования hello, с помощью REST</span><span class="sxs-lookup"><span data-stu-id="f7f65-124">Sample of two guest executables (C# and nodejs) communicating via hello Naming service using REST</span></span>](https://github.com/Azure-Samples/service-fabric-dotnet-containers)

## <a name="overview-of-application-and-service-manifest-files"></a><span data-ttu-id="f7f65-125">Обзор файлов манифестов приложений и служб</span><span class="sxs-lookup"><span data-stu-id="f7f65-125">Overview of application and service manifest files</span></span>
<span data-ttu-id="f7f65-126">В рамках развертывания гостевой исполняемый файл, он является полезным toounderstand hello Service Fabric упаковки и развертывания модели как описано в [модель приложения](service-fabric-application-model.md).</span><span class="sxs-lookup"><span data-stu-id="f7f65-126">As part of deploying a guest executable, it is useful toounderstand hello Service Fabric packaging and deployment model as described in [application model](service-fabric-application-model.md).</span></span> <span data-ttu-id="f7f65-127">модель упаковки Service Fabric Hello основывается на двух файлах XML: hello манифесты приложений и служб.</span><span class="sxs-lookup"><span data-stu-id="f7f65-127">hello Service Fabric packaging model relies on two XML files: hello application and service manifests.</span></span> <span data-ttu-id="f7f65-128">Hello определение схемы для hello файлы ApplicationManifest.xml и ServiceManifest.xml должен быть установлен с hello Service Fabric SDK в *C:\Program Files\Microsoft SDKs\Service Fabric\schemas\ServiceFabricServiceModel.xsd*.</span><span class="sxs-lookup"><span data-stu-id="f7f65-128">hello schema definition for hello ApplicationManifest.xml and ServiceManifest.xml files is installed with hello Service Fabric SDK into *C:\Program Files\Microsoft SDKs\Service Fabric\schemas\ServiceFabricServiceModel.xsd*.</span></span>

* <span data-ttu-id="f7f65-129">**Манифест приложения** hello манифест приложения — приложение hello используется toodescribe.</span><span class="sxs-lookup"><span data-stu-id="f7f65-129">**Application manifest** hello application manifest is used toodescribe hello application.</span></span> <span data-ttu-id="f7f65-130">Перечисляются службы hello, составляющих его и другими параметрами, используемые toodefine следует развернуть как одна или несколько служб, например hello число экземпляров.</span><span class="sxs-lookup"><span data-stu-id="f7f65-130">It lists hello services that compose it, and other parameters that are used toodefine how one or more services should be deployed, such as hello number of instances.</span></span>

  <span data-ttu-id="f7f65-131">В Service Fabric приложение — это единица развертывания и обновления.</span><span class="sxs-lookup"><span data-stu-id="f7f65-131">In Service Fabric, an application is a unit of deployment and upgrade.</span></span> <span data-ttu-id="f7f65-132">Приложение может обновляться как одна единица, для которой выполняется управление потенциальными сбоями и откатами.</span><span class="sxs-lookup"><span data-stu-id="f7f65-132">An application can be upgraded as a single unit where potential failures and potential rollbacks are managed.</span></span> <span data-ttu-id="f7f65-133">Service Fabric гарантирует, что процесс обновления hello является либо успешно, или при сбое обновления hello не оставляет приложение hello в неизвестном или работает нестабильно состоянии.</span><span class="sxs-lookup"><span data-stu-id="f7f65-133">Service Fabric guarantees that hello upgrade process is either successful, or, if hello upgrade fails, does not leave hello application in an unknown or unstable state.</span></span>
* <span data-ttu-id="f7f65-134">**Манифест службы** манифест службы hello описывает hello компоненты службы.</span><span class="sxs-lookup"><span data-stu-id="f7f65-134">**Service manifest** hello service manifest describes hello components of a service.</span></span> <span data-ttu-id="f7f65-135">Он включает в себя данные, такие как имя hello и тип службы и его код и конфигурация.</span><span class="sxs-lookup"><span data-stu-id="f7f65-135">It includes data, such as hello name and type of service, and its code and configuration.</span></span> <span data-ttu-id="f7f65-136">Hello манифест службы также содержит некоторые дополнительные параметры, которые можно использовать службу hello tooconfigure после его развертывания.</span><span class="sxs-lookup"><span data-stu-id="f7f65-136">hello service manifest also includes some additional parameters that can be used tooconfigure hello service once it is deployed.</span></span>

## <a name="application-package-file-structure"></a><span data-ttu-id="f7f65-137">Структура файла пакета приложения</span><span class="sxs-lookup"><span data-stu-id="f7f65-137">Application package file structure</span></span>
<span data-ttu-id="f7f65-138">toodeploy приложения tooService структуры приложения hello должны следовать стандартные каталогов.</span><span class="sxs-lookup"><span data-stu-id="f7f65-138">toodeploy an application tooService Fabric, hello application should follow a predefined directory structure.</span></span> <span data-ttu-id="f7f65-139">Hello ниже приведен пример этой структуры.</span><span class="sxs-lookup"><span data-stu-id="f7f65-139">hello following is an example of that structure.</span></span>

```
|-- ApplicationPackageRoot
    |-- GuestService1Pkg
        |-- Code
            |-- existingapp.exe
        |-- Config
            |-- Settings.xml
        |-- Data
        |-- ServiceManifest.xml
    |-- ApplicationManifest.xml
```

<span data-ttu-id="f7f65-140">Hello ApplicationPackageRoot содержит файл ApplicationManifest.xml hello, определяющий приложение hello.</span><span class="sxs-lookup"><span data-stu-id="f7f65-140">hello ApplicationPackageRoot contains hello ApplicationManifest.xml file that defines hello application.</span></span> <span data-ttu-id="f7f65-141">Вложенный каталог для каждой службы в приложение hello — используется toocontain все hello артефакты, необходимые службе hello.</span><span class="sxs-lookup"><span data-stu-id="f7f65-141">A subdirectory for each service included in hello application is used toocontain all hello artifacts that hello service requires.</span></span> <span data-ttu-id="f7f65-142">Эти подкаталоги будут hello ServiceManifest.xml и, как правило, hello следующие:</span><span class="sxs-lookup"><span data-stu-id="f7f65-142">These subdirectories are hello ServiceManifest.xml and, typically, hello following:</span></span>

* <span data-ttu-id="f7f65-143">*Code*.</span><span class="sxs-lookup"><span data-stu-id="f7f65-143">*Code*.</span></span> <span data-ttu-id="f7f65-144">Эта папка содержит код службы hello.</span><span class="sxs-lookup"><span data-stu-id="f7f65-144">This directory contains hello service code.</span></span>
* <span data-ttu-id="f7f65-145">*Config*. Эта папка содержит файл Settings.xml (и другие файлы при необходимости) доступность службы hello во время выполнения tooretrieve определенные параметры конфигурации.</span><span class="sxs-lookup"><span data-stu-id="f7f65-145">*Config*. This directory contains a Settings.xml file (and other files if necessary) that hello service can access at runtime tooretrieve specific configuration settings.</span></span>
* <span data-ttu-id="f7f65-146">*Data*.</span><span class="sxs-lookup"><span data-stu-id="f7f65-146">*Data*.</span></span> <span data-ttu-id="f7f65-147">Это дополнительный каталог toostore Дополнительные локальные данные, может потребоваться hello службы.</span><span class="sxs-lookup"><span data-stu-id="f7f65-147">This is an additional directory toostore additional local data that hello service may need.</span></span> <span data-ttu-id="f7f65-148">Данные должны быть toostore используется только временных данных.</span><span class="sxs-lookup"><span data-stu-id="f7f65-148">Data should be used toostore only ephemeral data.</span></span> <span data-ttu-id="f7f65-149">Если необходимо toobe переместить (например, во время отработки отказа), служба hello Service Fabric не копирует и реплицировать изменения toohello каталог данных.</span><span class="sxs-lookup"><span data-stu-id="f7f65-149">Service Fabric does not copy or replicate changes toohello data directory if hello service needs toobe relocated (for example, during failover).</span></span>

> [!NOTE]
> <span data-ttu-id="f7f65-150">Нет toocreate hello `config` и `data` каталоги, если они не нужны.</span><span class="sxs-lookup"><span data-stu-id="f7f65-150">You don't have toocreate hello `config` and `data` directories if you don't need them.</span></span>
>
>

## <a name="package-an-existing-executable"></a><span data-ttu-id="f7f65-151">Упаковка существующего исполняемого файла</span><span class="sxs-lookup"><span data-stu-id="f7f65-151">Package an existing executable</span></span>
<span data-ttu-id="f7f65-152">При упаковке гостевой исполняемый файл, вы можете либо toouse шаблон проекта Visual Studio или слишком[вручную создать пакет приложения hello](#manually).</span><span class="sxs-lookup"><span data-stu-id="f7f65-152">When packaging a guest executable, you can choose either toouse a Visual Studio project template or too[create hello application package manually](#manually).</span></span> <span data-ttu-id="f7f65-153">С помощью Visual Studio, hello структуры пакета приложения и файлы манифеста создаются hello новый шаблон проекта для вас.</span><span class="sxs-lookup"><span data-stu-id="f7f65-153">Using Visual Studio, hello application package structure and manifest files are created by hello new project template for you.</span></span>

> [!TIP]
> <span data-ttu-id="f7f65-154">toouse Visual Studio — Hello простым способом toopackage существующий исполняемый файл в службу Windows и Linux toouse Yeoman</span><span class="sxs-lookup"><span data-stu-id="f7f65-154">hello easiest way toopackage an existing Windows executable into a service is toouse Visual Studio and on Linux toouse Yeoman</span></span>
>

## <a name="use-visual-studio-toopackage-and-deploy-an-existing-executable"></a><span data-ttu-id="f7f65-155">Использовать toopackage Visual Studio и развертывать существующего исполняемого файла</span><span class="sxs-lookup"><span data-stu-id="f7f65-155">Use Visual Studio toopackage and deploy an existing executable</span></span>
<span data-ttu-id="f7f65-156">Visual Studio предоставляет Service Fabric toohelp шаблона службы, можно развернуть гостевой кластер Service Fabric исполняемый tooa.</span><span class="sxs-lookup"><span data-stu-id="f7f65-156">Visual Studio provides a Service Fabric service template toohelp you deploy a guest executable tooa Service Fabric cluster.</span></span>

1. <span data-ttu-id="f7f65-157">Чтобы создать приложение Service Fabric, выберите **Файл** > **Создать проект**.</span><span class="sxs-lookup"><span data-stu-id="f7f65-157">Choose **File** > **New Project**, and create a Service Fabric application.</span></span>
2. <span data-ttu-id="f7f65-158">Выберите **гостевой исполняемый файл** как hello шаблона службы.</span><span class="sxs-lookup"><span data-stu-id="f7f65-158">Choose **Guest Executable** as hello service template.</span></span>
3. <span data-ttu-id="f7f65-159">Нажмите кнопку **Обзор** tooselect hello папка с исполняемый файл и заполните поля на rest hello toocreate hello hello параметров службы.</span><span class="sxs-lookup"><span data-stu-id="f7f65-159">Click **Browse** tooselect hello folder with your executable and fill in hello rest of hello parameters toocreate hello service.</span></span>
   * <span data-ttu-id="f7f65-160">*Поведение пакета кода*.</span><span class="sxs-lookup"><span data-stu-id="f7f65-160">*Code Package Behavior*.</span></span> <span data-ttu-id="f7f65-161">Может быть набор toocopy все содержимое hello toohello вашей папки проекта Visual Studio, это полезно, если hello исполняемый файл не изменяется.</span><span class="sxs-lookup"><span data-stu-id="f7f65-161">Can be set toocopy all hello content of your folder toohello Visual Studio Project, which is useful if hello executable does not change.</span></span> <span data-ttu-id="f7f65-162">Если ожидается, что исполняемый файл toochange hello и динамически требуется hello toopick возможность копирования новые сборки, вы можете toolink toohello папки.</span><span class="sxs-lookup"><span data-stu-id="f7f65-162">If you expect hello executable toochange and want hello ability toopick up new builds dynamically, you can choose toolink toohello folder instead.</span></span> <span data-ttu-id="f7f65-163">При создании проекта приложения hello в Visual Studio, можно использовать связанные папки.</span><span class="sxs-lookup"><span data-stu-id="f7f65-163">You can use linked folders when creating hello application project in Visual Studio.</span></span> <span data-ttu-id="f7f65-164">Это свяжет toohello источника, откуда в рамках проекта hello, благодаря чему вы tooupdate hello гостевой исполняемый файл в поле назначения источника.</span><span class="sxs-lookup"><span data-stu-id="f7f65-164">This links toohello source location from within hello project, making it possible for you tooupdate hello guest executable in its source destination.</span></span> <span data-ttu-id="f7f65-165">Эти обновления становятся частью пакета приложения hello в сборке.</span><span class="sxs-lookup"><span data-stu-id="f7f65-165">Those updates become part of hello application package on build.</span></span>
   * <span data-ttu-id="f7f65-166">*Программа* указывает hello исполняемый файл, который следует запускать службы toostart hello.</span><span class="sxs-lookup"><span data-stu-id="f7f65-166">*Program* specifies hello executable that should be run toostart hello service.</span></span>
   * <span data-ttu-id="f7f65-167">*Аргументы* указывает hello аргументы, которые должны быть переданы toohello исполняемый файл.</span><span class="sxs-lookup"><span data-stu-id="f7f65-167">*Arguments* specifies hello arguments that should be passed toohello executable.</span></span> <span data-ttu-id="f7f65-168">Здесь можно указать список параметров с аргументами.</span><span class="sxs-lookup"><span data-stu-id="f7f65-168">It can be a list of parameters with arguments.</span></span>
   * <span data-ttu-id="f7f65-169">*WorkingFolder* указывает hello рабочий каталог для hello процесс, который будет запущен toobe.</span><span class="sxs-lookup"><span data-stu-id="f7f65-169">*WorkingFolder* specifies hello working directory for hello process that is going toobe started.</span></span> <span data-ttu-id="f7f65-170">Можно задать три значения:</span><span class="sxs-lookup"><span data-stu-id="f7f65-170">You can specify three values:</span></span>
     * <span data-ttu-id="f7f65-171">`CodeBase`Указывает, что hello рабочий каталог будет toobe задать каталог toohello кода в пакете приложения hello (`Code` directory, показанным в hello предшествующий структура файла).</span><span class="sxs-lookup"><span data-stu-id="f7f65-171">`CodeBase` specifies that hello working directory is going toobe set toohello code directory in hello application package (`Code` directory shown in hello preceding file structure).</span></span>
     * <span data-ttu-id="f7f65-172">`CodePackage`Указывает, что hello рабочий каталог будет toobe задать корень toohello пакета приложения hello (`GuestService1Pkg` показано в предшествующих структура файла hello).</span><span class="sxs-lookup"><span data-stu-id="f7f65-172">`CodePackage` specifies that hello working directory is going toobe set toohello root of hello application package    (`GuestService1Pkg` shown in hello preceding file structure).</span></span>
     * <span data-ttu-id="f7f65-173">`Work`Указывает, что hello файлы помещаются в подкаталог с именем работы.</span><span class="sxs-lookup"><span data-stu-id="f7f65-173">`Work` specifies that hello files are placed in a subdirectory called work.</span></span>
4. <span data-ttu-id="f7f65-174">Присвойте службе имя и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="f7f65-174">Give your service a name, and click **OK**.</span></span>
5. <span data-ttu-id="f7f65-175">Если службе нужна конечную точку для взаимодействия, теперь можно добавить hello протокол, порт и файле ServiceManifest.xml toohello типа.</span><span class="sxs-lookup"><span data-stu-id="f7f65-175">If your service needs an endpoint for communication, you can now add hello protocol, port, and type toohello ServiceManifest.xml file.</span></span> <span data-ttu-id="f7f65-176">Например, `<Endpoint Name="NodeAppTypeEndpoint" Protocol="http" Port="3000" UriScheme="http" PathSuffix="myapp/" Type="Input" />`.</span><span class="sxs-lookup"><span data-stu-id="f7f65-176">For example: `<Endpoint Name="NodeAppTypeEndpoint" Protocol="http" Port="3000" UriScheme="http" PathSuffix="myapp/" Type="Input" />`.</span></span>
6. <span data-ttu-id="f7f65-177">Теперь можно использовать пакет hello и публикации действия для локального кластера. с помощью отладки hello решения в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="f7f65-177">You can now use hello package and publish action against your local cluster by debugging hello solution in Visual Studio.</span></span> <span data-ttu-id="f7f65-178">Когда все будет готово, можно опубликовать hello приложения tooa удаленного кластера или установить в элемент управления toosource решения hello.</span><span class="sxs-lookup"><span data-stu-id="f7f65-178">When ready, you can publish hello application tooa remote cluster or check in hello solution toosource control.</span></span>
7. <span data-ttu-id="f7f65-179">Как перейти toohello конце этой статьи toosee tooview гостевой исполняемый файл службы в обозреватель Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="f7f65-179">Go toohello end of this article toosee how tooview your guest executable service running in Service Fabric Explorer.</span></span>

## <a name="use-yoeman-toopackage-and-deploy-an-existing-executable-on-linux"></a><span data-ttu-id="f7f65-180">Использование Yoeman toopackage и развертывания существующего исполняемого файла в Linux</span><span class="sxs-lookup"><span data-stu-id="f7f65-180">Use Yoeman toopackage and deploy an existing executable on Linux</span></span>

<span data-ttu-id="f7f65-181">Hello процедуры для создания и развертывания гостевой исполняемый файл в Linux hello такой же, как развертывание приложения на c# или java.</span><span class="sxs-lookup"><span data-stu-id="f7f65-181">hello procedure for creating and deploying a guest executable on Linux is hello same as deploying a csharp or java application.</span></span>

1. <span data-ttu-id="f7f65-182">В окне терминала введите `yo azuresfguest`.</span><span class="sxs-lookup"><span data-stu-id="f7f65-182">In a terminal, type `yo azuresfguest`.</span></span>
2. <span data-ttu-id="f7f65-183">Присвойте имя приложению.</span><span class="sxs-lookup"><span data-stu-id="f7f65-183">Name your application.</span></span>
3. <span data-ttu-id="f7f65-184">Службы, введите имя и сведения о hello, включая путь к исполняемому hello и hello параметры, которые должны вызываться с использованием.</span><span class="sxs-lookup"><span data-stu-id="f7f65-184">Name your service, and provide hello details including path of hello executable and hello parameters it must be invoked with.</span></span>

<span data-ttu-id="f7f65-185">Yeoman создает пакет приложения с помощью соответствующего приложения hello и файлы манифеста, наряду с установки и удаления скриптов.</span><span class="sxs-lookup"><span data-stu-id="f7f65-185">Yeoman creates an application package with hello appropriate application and manifest files along with install and uninstall scripts.</span></span>

<a id="manually"></a>

## <a name="manually-package-and-deploy-an-existing-executable"></a><span data-ttu-id="f7f65-186">Упаковка и развертывание имеющегося исполняемого файла вручную</span><span class="sxs-lookup"><span data-stu-id="f7f65-186">Manually package and deploy an existing executable</span></span>
<span data-ttu-id="f7f65-187">процесс Hello вручную упаковки гостевой исполняемый файл основан на hello следующие общие шаги:</span><span class="sxs-lookup"><span data-stu-id="f7f65-187">hello process of manually packaging a guest executable is based on hello following general steps:</span></span>

1. <span data-ttu-id="f7f65-188">Создайте структуру каталогов пакета hello.</span><span class="sxs-lookup"><span data-stu-id="f7f65-188">Create hello package directory structure.</span></span>
2. <span data-ttu-id="f7f65-189">Добавьте приложение hello код и файлы конфигурации.</span><span class="sxs-lookup"><span data-stu-id="f7f65-189">Add hello application's code and configuration files.</span></span>
3. <span data-ttu-id="f7f65-190">Измените файл манифеста службы hello.</span><span class="sxs-lookup"><span data-stu-id="f7f65-190">Edit hello service manifest file.</span></span>
4. <span data-ttu-id="f7f65-191">Измените файл манифеста приложения hello.</span><span class="sxs-lookup"><span data-stu-id="f7f65-191">Edit hello application manifest file.</span></span>

<!--
>[AZURE.NOTE] We do provide a packaging tool that allows you toocreate hello ApplicationPackage automatically. hello tool is currently in preview. You can download it from [here](http://aka.ms/servicefabricpacktool).
-->

### <a name="create-hello-package-directory-structure"></a><span data-ttu-id="f7f65-192">Создать структуру каталогов пакета hello</span><span class="sxs-lookup"><span data-stu-id="f7f65-192">Create hello package directory structure</span></span>
<span data-ttu-id="f7f65-193">Можно запустить, создание hello структуры каталогов, как описано в предыдущих разделов, hello «Структура файла пакета приложения».</span><span class="sxs-lookup"><span data-stu-id="f7f65-193">You can start by creating hello directory structure, as described in hello preceding section, "Application package file structure."</span></span>

### <a name="add-hello-applications-code-and-configuration-files"></a><span data-ttu-id="f7f65-194">Добавление приложения hello код и файлы конфигурации</span><span class="sxs-lookup"><span data-stu-id="f7f65-194">Add hello application's code and configuration files</span></span>
<span data-ttu-id="f7f65-195">После создания структуры каталогов hello, можно добавить приложение hello код и файлы конфигурации в группе кода и конфигурации каталогов hello.</span><span class="sxs-lookup"><span data-stu-id="f7f65-195">After you have created hello directory structure, you can add hello application's code and configuration files under hello code and config directories.</span></span> <span data-ttu-id="f7f65-196">Можно также создать дополнительные каталоги файлов или подкаталогов в каталогах hello кода или конфигурации.</span><span class="sxs-lookup"><span data-stu-id="f7f65-196">You can also create additional directories or subdirectories under hello code or config directories.</span></span>

<span data-ttu-id="f7f65-197">Service Fabric `xcopy` содержимого hello hello корневому каталогу приложения, поэтому нет предопределенных структуры toouse Кроме создание двух каталогов top, код и параметры.</span><span class="sxs-lookup"><span data-stu-id="f7f65-197">Service Fabric does an `xcopy` of hello content of hello application root directory, so there is no predefined structure toouse other than creating two top directories, code and settings.</span></span> <span data-ttu-id="f7f65-198">(Вы можете выбрать любые имена.</span><span class="sxs-lookup"><span data-stu-id="f7f65-198">(You can pick different names if you want.</span></span> <span data-ttu-id="f7f65-199">Дополнительные сведения находятся в следующем разделе hello.)</span><span class="sxs-lookup"><span data-stu-id="f7f65-199">More details are in hello next section.)</span></span>

> [!NOTE]
> <span data-ttu-id="f7f65-200">Убедитесь, что включение всех файлов hello и зависимости, которые hello потребностей приложения.</span><span class="sxs-lookup"><span data-stu-id="f7f65-200">Make sure that you include all hello files and dependencies that hello application needs.</span></span> <span data-ttu-id="f7f65-201">Service Fabric копирует hello содержимого пакета приложения hello на всех узлах в кластере hello, где службы приложения hello находятся toobe будет развернут.</span><span class="sxs-lookup"><span data-stu-id="f7f65-201">Service Fabric copies hello content of hello application package on all nodes in hello cluster where hello application's services are going toobe deployed.</span></span> <span data-ttu-id="f7f65-202">Hello пакет должен содержать все кода hello, что hello приложению toorun.</span><span class="sxs-lookup"><span data-stu-id="f7f65-202">hello package should contain all hello code that hello application needs toorun.</span></span> <span data-ttu-id="f7f65-203">Не следует считать зависимости hello уже установлены.</span><span class="sxs-lookup"><span data-stu-id="f7f65-203">Do not assume that hello dependencies are already installed.</span></span>
>
>

### <a name="edit-hello-service-manifest-file"></a><span data-ttu-id="f7f65-204">Изменить файл манифеста службы hello</span><span class="sxs-lookup"><span data-stu-id="f7f65-204">Edit hello service manifest file</span></span>
<span data-ttu-id="f7f65-205">Hello следующим шагом является tooedit hello службы файл манифеста tooinclude hello следующую информацию:</span><span class="sxs-lookup"><span data-stu-id="f7f65-205">hello next step is tooedit hello service manifest file tooinclude hello following information:</span></span>

* <span data-ttu-id="f7f65-206">Hello имя типа службы hello.</span><span class="sxs-lookup"><span data-stu-id="f7f65-206">hello name of hello service type.</span></span> <span data-ttu-id="f7f65-207">— Это идентификатор, что Service Fabric использует tooidentify службы.</span><span class="sxs-lookup"><span data-stu-id="f7f65-207">This is an ID that Service Fabric uses tooidentify a service.</span></span>
* <span data-ttu-id="f7f65-208">Hello команда toouse toolaunch hello приложения (ExeHost).</span><span class="sxs-lookup"><span data-stu-id="f7f65-208">hello command toouse toolaunch hello application (ExeHost).</span></span>
* <span data-ttu-id="f7f65-209">Любой сценарий, который требуется запустить toobe tooset приложения hello (SetupEntrypoint).</span><span class="sxs-lookup"><span data-stu-id="f7f65-209">Any script that needs toobe run tooset up hello application (SetupEntrypoint).</span></span>

<span data-ttu-id="f7f65-210">Hello ниже приведен пример `ServiceManifest.xml` файла:</span><span class="sxs-lookup"><span data-stu-id="f7f65-210">hello following is an example of a `ServiceManifest.xml` file:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<ServiceManifest xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" Name="NodeApp" Version="1.0.0.0" xmlns="http://schemas.microsoft.com/2011/01/fabric">
   <ServiceTypes>
      <StatelessServiceType ServiceTypeName="NodeApp" UseImplicitHost="true"/>
   </ServiceTypes>
   <CodePackage Name="code" Version="1.0.0.0">
      <SetupEntryPoint>
         <ExeHost>
             <Program>scripts\launchConfig.cmd</Program>
         </ExeHost>
      </SetupEntryPoint>
      <EntryPoint>
         <ExeHost>
            <Program>node.exe</Program>
            <Arguments>bin/www</Arguments>
            <WorkingFolder>CodePackage</WorkingFolder>
         </ExeHost>
      </EntryPoint>
   </CodePackage>
   <Resources>
      <Endpoints>
         <Endpoint Name="NodeAppTypeEndpoint" Protocol="http" Port="3000" Type="Input" />
      </Endpoints>
   </Resources>
</ServiceManifest>
```

<span data-ttu-id="f7f65-211">Hello в следующих разделах рассмотрены различные части файла hello необходимые tooupdate hello.</span><span class="sxs-lookup"><span data-stu-id="f7f65-211">hello following sections go over hello different parts of hello file that you need tooupdate.</span></span>

#### <a name="update-servicetypes"></a><span data-ttu-id="f7f65-212">Обновление ServiceTypes</span><span class="sxs-lookup"><span data-stu-id="f7f65-212">Update ServiceTypes</span></span>
```xml
<ServiceTypes>
  <StatelessServiceType ServiceTypeName="NodeApp" UseImplicitHost="true" />
</ServiceTypes>
```

* <span data-ttu-id="f7f65-213">Выберите для `ServiceTypeName`любое имя.</span><span class="sxs-lookup"><span data-stu-id="f7f65-213">You can pick any name that you want for `ServiceTypeName`.</span></span> <span data-ttu-id="f7f65-214">Hello значение используется в hello `ApplicationManifest.xml` файловой службы tooidentify hello.</span><span class="sxs-lookup"><span data-stu-id="f7f65-214">hello value is used in hello `ApplicationManifest.xml` file tooidentify hello service.</span></span>
* <span data-ttu-id="f7f65-215">Укажите `UseImplicitHost="true"`.</span><span class="sxs-lookup"><span data-stu-id="f7f65-215">Specify `UseImplicitHost="true"`.</span></span> <span data-ttu-id="f7f65-216">Этот атрибут сообщает Service Fabric, что служба hello основывается на автономное приложение, должно все Service Fabric toodo toolaunch его как процесс и осуществлять мониторинг его состояния.</span><span class="sxs-lookup"><span data-stu-id="f7f65-216">This attribute tells Service Fabric that hello service is based on a self-contained app, so all Service Fabric needs toodo is toolaunch it as a process and monitor its health.</span></span>

#### <a name="update-codepackage"></a><span data-ttu-id="f7f65-217">Обновление CodePackage</span><span class="sxs-lookup"><span data-stu-id="f7f65-217">Update CodePackage</span></span>
<span data-ttu-id="f7f65-218">элемент CodePackage Hello указывает расположение hello (и версию) кода hello службы.</span><span class="sxs-lookup"><span data-stu-id="f7f65-218">hello CodePackage element specifies hello location (and version) of hello service's code.</span></span>

```xml
<CodePackage Name="Code" Version="1.0.0.0">
```

<span data-ttu-id="f7f65-219">Hello `Name` элемент — используется toospecify hello имя каталога hello в пакет приложения hello, который содержит код службы hello.</span><span class="sxs-lookup"><span data-stu-id="f7f65-219">hello `Name` element is used toospecify hello name of hello directory in hello application package that contains hello service's code.</span></span> <span data-ttu-id="f7f65-220">`CodePackage`также имеет hello `version` атрибута.</span><span class="sxs-lookup"><span data-stu-id="f7f65-220">`CodePackage` also has hello `version` attribute.</span></span> <span data-ttu-id="f7f65-221">Это может быть используется toospecify hello версию кода hello и потенциально может быть использовано код tooupgrade hello службы с помощью инфраструктуры управления жизненным циклом приложения hello в Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="f7f65-221">This can be used toospecify hello version of hello code, and can also potentially be used tooupgrade hello service's code by using hello application lifecycle management infrastructure in Service Fabric.</span></span>

#### <a name="optional-update-setupentrypoint"></a><span data-ttu-id="f7f65-222">Обновление SetupEntrypoint (необязательно)</span><span class="sxs-lookup"><span data-stu-id="f7f65-222">Optional: Update SetupEntrypoint</span></span>
```xml
<SetupEntryPoint>
   <ExeHost>
       <Program>scripts\launchConfig.cmd</Program>
   </ExeHost>
</SetupEntryPoint>
```
<span data-ttu-id="f7f65-223">элемент SetupEntryPoint Hello является исполняемым или пакетным файлом, которая должна выполняться перед запуском кода hello службы используется toospecify.</span><span class="sxs-lookup"><span data-stu-id="f7f65-223">hello SetupEntryPoint element is used toospecify any executable or batch file that should be executed before hello service's code is launched.</span></span> <span data-ttu-id="f7f65-224">Это необязательный шаг, поэтому она не должна toobe включено, если не требуется инициализация.</span><span class="sxs-lookup"><span data-stu-id="f7f65-224">It is an optional step, so it does not need toobe included if there is no initialization required.</span></span> <span data-ttu-id="f7f65-225">Hello SetupEntryPoint выполняется каждый раз при перезапуске службы hello.</span><span class="sxs-lookup"><span data-stu-id="f7f65-225">hello SetupEntryPoint is executed every time hello service is restarted.</span></span>

<span data-ttu-id="f7f65-226">Имеется только один SetupEntryPoint сценариев установки требуется toobe группируются в одном пакетном файле, если установка приложения hello требует нескольких сценариев.</span><span class="sxs-lookup"><span data-stu-id="f7f65-226">There is only one SetupEntryPoint, so setup scripts need toobe grouped in a single batch file if hello application's setup requires multiple scripts.</span></span> <span data-ttu-id="f7f65-227">Hello SetupEntryPoint могут выполнять все типы файлов: исполняемых файлов, пакетных файлов и командлеты PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f7f65-227">hello SetupEntryPoint can execute any type of file: executable files, batch files, and PowerShell cmdlets.</span></span> <span data-ttu-id="f7f65-228">Подробнее см. в статье [Настройка SetupEntryPoint](service-fabric-application-runas-security.md).</span><span class="sxs-lookup"><span data-stu-id="f7f65-228">For more details, see [Configure SetupEntryPoint](service-fabric-application-runas-security.md).</span></span>

<span data-ttu-id="f7f65-229">В предыдущих пример hello, hello SetupEntryPoint выполнение пакетного файла вызывается `LaunchConfig.cmd` , расположенного в hello `scripts` подкаталоге каталога кода hello (при условии, что hello WorkingFolder имеет значение tooCodeBase).</span><span class="sxs-lookup"><span data-stu-id="f7f65-229">In hello preceding example, hello SetupEntryPoint runs a batch file called `LaunchConfig.cmd` that is located in hello `scripts` subdirectory of hello code directory (assuming hello WorkingFolder element is set tooCodeBase).</span></span>

#### <a name="update-entrypoint"></a><span data-ttu-id="f7f65-230">Обновление EntryPoint</span><span class="sxs-lookup"><span data-stu-id="f7f65-230">Update EntryPoint</span></span>
```xml
<EntryPoint>
  <ExeHost>
    <Program>node.exe</Program>
    <Arguments>bin/www</Arguments>
    <WorkingFolder>CodeBase</WorkingFolder>
  </ExeHost>
</EntryPoint>
```

<span data-ttu-id="f7f65-231">Hello `EntryPoint` элемент в файл манифеста службы hello — toospecify используется как toolaunch hello службы.</span><span class="sxs-lookup"><span data-stu-id="f7f65-231">hello `EntryPoint` element in hello service manifest file is used toospecify how toolaunch hello service.</span></span> <span data-ttu-id="f7f65-232">Hello `ExeHost` элемент указывает hello исполняемый файл (и аргументы), следует использовать toolaunch hello службы.</span><span class="sxs-lookup"><span data-stu-id="f7f65-232">hello `ExeHost` element specifies hello executable (and arguments) that should be used toolaunch hello service.</span></span>

* <span data-ttu-id="f7f65-233">`Program`Указывает имя hello hello исполняемый файл, который необходимо запустить службу hello.</span><span class="sxs-lookup"><span data-stu-id="f7f65-233">`Program` specifies hello name of hello executable that should start hello service.</span></span>
* <span data-ttu-id="f7f65-234">`Arguments`Указывает hello аргументы, которые должны быть переданы toohello исполняемый файл.</span><span class="sxs-lookup"><span data-stu-id="f7f65-234">`Arguments` specifies hello arguments that should be passed toohello executable.</span></span> <span data-ttu-id="f7f65-235">Здесь можно указать список параметров с аргументами.</span><span class="sxs-lookup"><span data-stu-id="f7f65-235">It can be a list of parameters with arguments.</span></span>
* <span data-ttu-id="f7f65-236">`WorkingFolder`Указывает рабочий каталог hello для hello процесс, который будет запущен toobe.</span><span class="sxs-lookup"><span data-stu-id="f7f65-236">`WorkingFolder` specifies hello working directory for hello process that is going toobe started.</span></span> <span data-ttu-id="f7f65-237">Можно задать три значения:</span><span class="sxs-lookup"><span data-stu-id="f7f65-237">You can specify three values:</span></span>
  * <span data-ttu-id="f7f65-238">`CodeBase`Указывает, что hello рабочий каталог будет toobe задать каталог toohello кода в пакете приложения hello (`Code` каталог в hello предшествующий структура файла).</span><span class="sxs-lookup"><span data-stu-id="f7f65-238">`CodeBase` specifies that hello working directory is going toobe set toohello code directory in hello application package (`Code` directory in hello preceding file structure).</span></span>
  * <span data-ttu-id="f7f65-239">`CodePackage`Указывает, что hello рабочий каталог будет toobe задать корень toohello пакета приложения hello (`GuestService1Pkg` в hello предшествующий структура файла).</span><span class="sxs-lookup"><span data-stu-id="f7f65-239">`CodePackage` specifies that hello working directory is going toobe set toohello root of hello application package    (`GuestService1Pkg` in hello preceding file structure).</span></span>
    * <span data-ttu-id="f7f65-240">`Work`Указывает, что hello файлы помещаются в подкаталог с именем работы.</span><span class="sxs-lookup"><span data-stu-id="f7f65-240">`Work` specifies that hello files are placed in a subdirectory called work.</span></span>

<span data-ttu-id="f7f65-241">Hello WorkingFolder является полезным tooset hello правильный рабочий каталог для использования относительных путей скриптами либо hello приложения или инициализации.</span><span class="sxs-lookup"><span data-stu-id="f7f65-241">hello WorkingFolder is useful tooset hello correct working directory so that relative paths can be used by either hello application or initialization scripts.</span></span>

#### <a name="update-endpoints-and-register-with-naming-service-for-communication"></a><span data-ttu-id="f7f65-242">Обновление конечных точек и регистрация в службе именования для обмена данными</span><span class="sxs-lookup"><span data-stu-id="f7f65-242">Update Endpoints and register with Naming Service for communication</span></span>
```xml
<Endpoints>
   <Endpoint Name="NodeAppTypeEndpoint" Protocol="http" Port="3000" Type="Input" />
</Endpoints>

```
<span data-ttu-id="f7f65-243">В предыдущих пример hello, hello `Endpoint` элемент указывает hello конечных точек, которые могут прослушивать приложения hello.</span><span class="sxs-lookup"><span data-stu-id="f7f65-243">In hello preceding example, hello `Endpoint` element specifies hello endpoints that hello application can listen on.</span></span> <span data-ttu-id="f7f65-244">В этом примере hello Node.js приложение прослушивает http через порт 3000.</span><span class="sxs-lookup"><span data-stu-id="f7f65-244">In this example, hello Node.js application listens on http on port 3000.</span></span>

<span data-ttu-id="f7f65-245">Кроме того можно попросить Service Fabric toopublish toohello этой конечной точки службы именования, другие службы может обнаруживать адрес toothis hello конечной точки службы.</span><span class="sxs-lookup"><span data-stu-id="f7f65-245">Furthermore you can ask Service Fabric toopublish this endpoint toohello Naming Service so other services can discover hello endpoint address toothis service.</span></span> <span data-ttu-id="f7f65-246">Это позволит вам может toocommunicate toobe между службами исполняемых гостевой.</span><span class="sxs-lookup"><span data-stu-id="f7f65-246">This enables you toobe able toocommunicate between services that are guest executables.</span></span>
<span data-ttu-id="f7f65-247">Hello опубликованных адрес конечной точки — hello формы `UriScheme://IPAddressOrFQDN:Port/PathSuffix`.</span><span class="sxs-lookup"><span data-stu-id="f7f65-247">hello published endpoint address is of hello form `UriScheme://IPAddressOrFQDN:Port/PathSuffix`.</span></span> <span data-ttu-id="f7f65-248">`UriScheme` и `PathSuffix` являются необязательными атрибутами.</span><span class="sxs-lookup"><span data-stu-id="f7f65-248">`UriScheme` and `PathSuffix` are optional attributes.</span></span> <span data-ttu-id="f7f65-249">`IPAddressOrFQDN`— hello IP-адрес или полное доменное имя узла hello этот исполняемый файл помещается в и вычисляется автоматически.</span><span class="sxs-lookup"><span data-stu-id="f7f65-249">`IPAddressOrFQDN` is hello IP address or fully qualified domain name of hello node this executable gets placed on, and it is calculated for you.</span></span>

<span data-ttu-id="f7f65-250">В hello примере один раз hello служба развернута, в обозреватель Service Fabric см конечной точки аналогично слишком`http://10.1.4.92:3000/myapp/` публикации для экземпляра службы hello.</span><span class="sxs-lookup"><span data-stu-id="f7f65-250">In hello following example, once hello service is deployed, in Service Fabric Explorer you see an endpoint similar too`http://10.1.4.92:3000/myapp/` published for hello service instance.</span></span> <span data-ttu-id="f7f65-251">Если используется локальный компьютер, она будет в формате `http://localhost:3000/myapp/`.</span><span class="sxs-lookup"><span data-stu-id="f7f65-251">Or if this is a local machine, you see `http://localhost:3000/myapp/`.</span></span>

```xml
<Endpoints>
   <Endpoint Name="NodeAppTypeEndpoint" Protocol="http" Port="3000"  UriScheme="http" PathSuffix="myapp/" Type="Input" />
</Endpoints>
```
<span data-ttu-id="f7f65-252">Можно использовать эти адреса с [обратный прокси-сервер](service-fabric-reverseproxy.md) toocommunicate между службами.</span><span class="sxs-lookup"><span data-stu-id="f7f65-252">You can use these addresses with [reverse proxy](service-fabric-reverseproxy.md) toocommunicate between services.</span></span>

### <a name="edit-hello-application-manifest-file"></a><span data-ttu-id="f7f65-253">Изменить файл манифеста приложения hello</span><span class="sxs-lookup"><span data-stu-id="f7f65-253">Edit hello application manifest file</span></span>
<span data-ttu-id="f7f65-254">После настройки hello `Servicemanifest.xml` файл, необходимо toomake некоторые изменения toohello `ApplicationManifest.xml` файл tooensure, hello правильный тип службы и имя используются.</span><span class="sxs-lookup"><span data-stu-id="f7f65-254">Once you have configured hello `Servicemanifest.xml` file, you need toomake some changes toohello `ApplicationManifest.xml` file tooensure that hello correct service type and name are used.</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<ApplicationManifest xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" ApplicationTypeName="NodeAppType" ApplicationTypeVersion="1.0" xmlns="http://schemas.microsoft.com/2011/01/fabric">
   <ServiceManifestImport>
      <ServiceManifestRef ServiceManifestName="NodeApp" ServiceManifestVersion="1.0.0.0" />
   </ServiceManifestImport>
</ApplicationManifest>
```

#### <a name="servicemanifestimport"></a><span data-ttu-id="f7f65-255">ServiceManifestImport</span><span class="sxs-lookup"><span data-stu-id="f7f65-255">ServiceManifestImport</span></span>
<span data-ttu-id="f7f65-256">В hello `ServiceManifestImport` элемента, можно указать одну или несколько служб, которые должны tooinclude в приложение hello.</span><span class="sxs-lookup"><span data-stu-id="f7f65-256">In hello `ServiceManifestImport` element, you can specify one or more services that you want tooinclude in hello app.</span></span> <span data-ttu-id="f7f65-257">Службы указываются с `ServiceManifestName`, который указывает имя hello hello каталога, в которой hello `ServiceManifest.xml` находится файл.</span><span class="sxs-lookup"><span data-stu-id="f7f65-257">Services are referenced with `ServiceManifestName`, which specifies hello name of hello directory where hello `ServiceManifest.xml` file is located.</span></span>

```xml
<ServiceManifestImport>
  <ServiceManifestRef ServiceManifestName="NodeApp" ServiceManifestVersion="1.0.0.0" />
</ServiceManifestImport>
```

## <a name="set-up-logging"></a><span data-ttu-id="f7f65-258">Настройка ведения журнала</span><span class="sxs-lookup"><span data-stu-id="f7f65-258">Set up logging</span></span>
<span data-ttu-id="f7f65-259">Для исполняемых файлов гостя является toofind журналы консоли может toosee полезно toobe out hello сценариев приложения и конфигурации показа ошибок.</span><span class="sxs-lookup"><span data-stu-id="f7f65-259">For guest executables, it is useful toobe able toosee console logs toofind out if hello application and configuration scripts show any errors.</span></span>
<span data-ttu-id="f7f65-260">Перенаправление консоли можно настроить в hello `ServiceManifest.xml` файла с помощью hello `ConsoleRedirection` элемента.</span><span class="sxs-lookup"><span data-stu-id="f7f65-260">Console redirection can be configured in hello `ServiceManifest.xml` file using hello `ConsoleRedirection` element.</span></span>

> [!WARNING]
> <span data-ttu-id="f7f65-261">Никогда не используйте политику перенаправления консоли hello в приложении, которое развертывается в рабочей среде, так как это может повлиять на приложения hello перехода на другой ресурс.</span><span class="sxs-lookup"><span data-stu-id="f7f65-261">Never use hello console redirection policy in an application that is deployed in production because this can affect hello application failover.</span></span> <span data-ttu-id="f7f65-262">Используйте ее *только* для локальной разработки и отладки.</span><span class="sxs-lookup"><span data-stu-id="f7f65-262">*Only* use this for local development and debugging purposes.</span></span>  
>
>

```xml
<EntryPoint>
  <ExeHost>
    <Program>node.exe</Program>
    <Arguments>bin/www</Arguments>
    <WorkingFolder>CodeBase</WorkingFolder>
    <ConsoleRedirection FileRetentionCount="5" FileMaxSizeInKb="2048"/>
  </ExeHost>
</EntryPoint>
```

<span data-ttu-id="f7f65-263">`ConsoleRedirection`можно использовать tooredirect консоли вывода (stdout и stderr) tooa рабочий каталог.</span><span class="sxs-lookup"><span data-stu-id="f7f65-263">`ConsoleRedirection` can be used tooredirect console output (both stdout and stderr) tooa working directory.</span></span> <span data-ttu-id="f7f65-264">Это обеспечивает возможность tooverify hello, нет ли ошибок во время установки hello или выполнение приложения hello в кластер Service Fabric hello.</span><span class="sxs-lookup"><span data-stu-id="f7f65-264">This provides hello ability tooverify that there are no errors during hello setup or execution of hello application in hello Service Fabric cluster.</span></span>

<span data-ttu-id="f7f65-265">`FileRetentionCount`Определяет, сколько файлов сохраняются в рабочем каталоге hello.</span><span class="sxs-lookup"><span data-stu-id="f7f65-265">`FileRetentionCount` determines how many files are saved in hello working directory.</span></span> <span data-ttu-id="f7f65-266">Например, значение 5, означает, что hello для предыдущих выполнений пять hello находятся файлы журналов в рабочем каталоге hello.</span><span class="sxs-lookup"><span data-stu-id="f7f65-266">A value of 5, for example, means that hello log files for hello previous five executions are stored in hello working directory.</span></span>

<span data-ttu-id="f7f65-267">`FileMaxSizeInKb`Указывает максимальный размер файлов журнала hello hello.</span><span class="sxs-lookup"><span data-stu-id="f7f65-267">`FileMaxSizeInKb` specifies hello maximum size of hello log files.</span></span>

<span data-ttu-id="f7f65-268">Файлы журнала сохраняются в одном из рабочих hello службы каталогов.</span><span class="sxs-lookup"><span data-stu-id="f7f65-268">Log files are saved in one of hello service's working directories.</span></span> <span data-ttu-id="f7f65-269">toodetermine, где находятся файлы hello, используйте обозреватель Service Fabric toodetermine службу hello узла, которая выполняется на, и какой рабочий каталог используется.</span><span class="sxs-lookup"><span data-stu-id="f7f65-269">toodetermine where hello files are located, use Service Fabric Explorer toodetermine which node hello service is running on, and which working directory is being used.</span></span> <span data-ttu-id="f7f65-270">Эта процедура рассмотрена далее в этой статье.</span><span class="sxs-lookup"><span data-stu-id="f7f65-270">This process is covered later in this article.</span></span>

## <a name="deployment"></a><span data-ttu-id="f7f65-271">Развертывание</span><span class="sxs-lookup"><span data-stu-id="f7f65-271">Deployment</span></span>
<span data-ttu-id="f7f65-272">Hello последним этапом является слишком[развертывания приложения](service-fabric-deploy-remove-applications.md).</span><span class="sxs-lookup"><span data-stu-id="f7f65-272">hello last step is too[deploy your application](service-fabric-deploy-remove-applications.md).</span></span> <span data-ttu-id="f7f65-273">Здравствуйте, следуя показан сценарий PowerShell как toodeploy вашего приложения toohello локальному кластеру разработки, а также запускать новую службу Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="f7f65-273">hello following PowerShell script shows how toodeploy your application toohello local development cluster, and start a new Service Fabric service.</span></span>

```PowerShell

Connect-ServiceFabricCluster localhost:19000

Write-Host 'Copying application package...'
Copy-ServiceFabricApplicationPackage -ApplicationPackagePath 'C:\Dev\MultipleApplications' -ImageStoreConnectionString 'file:C:\SfDevCluster\Data\ImageStoreShare' -ApplicationPackagePathInImageStore 'nodeapp'

Write-Host 'Registering application type...'
Register-ServiceFabricApplicationType -ApplicationPathInImageStore 'nodeapp'

New-ServiceFabricApplication -ApplicationName 'fabric:/nodeapp' -ApplicationTypeName 'NodeAppType' -ApplicationTypeVersion 1.0

New-ServiceFabricService -ApplicationName 'fabric:/nodeapp' -ServiceName 'fabric:/nodeapp/nodeappservice' -ServiceTypeName 'NodeApp' -Stateless -PartitionSchemeSingleton -InstanceCount 1

```

>[!TIP]
> <span data-ttu-id="f7f65-274">[Сжатие пакета hello](service-fabric-package-apps.md#compress-a-package) перед копированием toohello хранилища образов, если пакет hello большой или имеет много файлов.</span><span class="sxs-lookup"><span data-stu-id="f7f65-274">[Compress hello package](service-fabric-package-apps.md#compress-a-package) before copying toohello image store if hello package is large or has many files.</span></span> <span data-ttu-id="f7f65-275">Дополнительные сведения см. [здесь](service-fabric-deploy-remove-applications.md#upload-the-application-package).</span><span class="sxs-lookup"><span data-stu-id="f7f65-275">Read more [here](service-fabric-deploy-remove-applications.md#upload-the-application-package).</span></span>
>

<span data-ttu-id="f7f65-276">Службу Service Fabric можно развертывать в разных конфигурациях.</span><span class="sxs-lookup"><span data-stu-id="f7f65-276">A Service Fabric service can be deployed in various "configurations."</span></span> <span data-ttu-id="f7f65-277">Например его можно развернуть в качестве одного или нескольких экземпляров, или он может быть развернут таким образом, что имеется один экземпляр службы hello на каждом узле кластера Service Fabric hello.</span><span class="sxs-lookup"><span data-stu-id="f7f65-277">For example, it can be deployed as single or multiple instances, or it can be deployed in such a way that there is one instance of hello service on each node of hello Service Fabric cluster.</span></span>

<span data-ttu-id="f7f65-278">Hello `InstanceCount` параметр hello `New-ServiceFabricService` командлета — используется toospecify, сколько экземпляров hello службы должны запускаться в кластер Service Fabric hello.</span><span class="sxs-lookup"><span data-stu-id="f7f65-278">hello `InstanceCount` parameter of hello `New-ServiceFabricService` cmdlet is used toospecify how many instances of hello service should be launched in hello Service Fabric cluster.</span></span> <span data-ttu-id="f7f65-279">Можно задать hello `InstanceCount` значение в зависимости от типа развертываемого приложения hello.</span><span class="sxs-lookup"><span data-stu-id="f7f65-279">You can set hello `InstanceCount` value, depending on hello type of application that you are deploying.</span></span> <span data-ttu-id="f7f65-280">Ниже приведены Hello два наиболее распространенных сценариев.</span><span class="sxs-lookup"><span data-stu-id="f7f65-280">hello two most common scenarios are:</span></span>

* <span data-ttu-id="f7f65-281">`InstanceCount = "1"`.</span><span class="sxs-lookup"><span data-stu-id="f7f65-281">`InstanceCount = "1"`.</span></span> <span data-ttu-id="f7f65-282">В этом случае в кластере hello развертывается только один экземпляр службы hello.</span><span class="sxs-lookup"><span data-stu-id="f7f65-282">In this case, only one instance of hello service is deployed in hello cluster.</span></span> <span data-ttu-id="f7f65-283">Планировщик Service Fabric определяет, какие службы hello узла будет toobe, развернутой на.</span><span class="sxs-lookup"><span data-stu-id="f7f65-283">Service Fabric's scheduler determines which node hello service is going toobe deployed on.</span></span>
* <span data-ttu-id="f7f65-284">`InstanceCount ="-1"`.</span><span class="sxs-lookup"><span data-stu-id="f7f65-284">`InstanceCount ="-1"`.</span></span> <span data-ttu-id="f7f65-285">В этом случае один экземпляр службы hello развертывается на всех узлах кластера Service Fabric hello.</span><span class="sxs-lookup"><span data-stu-id="f7f65-285">In this case, one instance of hello service is deployed on every node in hello Service Fabric cluster.</span></span> <span data-ttu-id="f7f65-286">результат Hello наличие одного (и только одного) экземпляр службы hello для каждого узла в кластере hello.</span><span class="sxs-lookup"><span data-stu-id="f7f65-286">hello result is having one (and only one) instance of hello service for each node in hello cluster.</span></span>

<span data-ttu-id="f7f65-287">Это полезно конфигурации для клиентских приложений (например, конечную точку REST), так как клиентские приложения должны слишком «подключиться» tooany hello узлов в конечную точку hello toouse кластера hello.</span><span class="sxs-lookup"><span data-stu-id="f7f65-287">This is a useful configuration for front-end applications (for example, a REST endpoint), because client applications need too"connect" tooany of hello nodes in hello cluster toouse hello endpoint.</span></span> <span data-ttu-id="f7f65-288">Эта конфигурация используется также при, например, все узлы кластера Service Fabric hello подключенных tooa подсистемы балансировки нагрузки.</span><span class="sxs-lookup"><span data-stu-id="f7f65-288">This configuration can also be used when, for example, all nodes of hello Service Fabric cluster are connected tooa load balancer.</span></span> <span data-ttu-id="f7f65-289">Затем клиентский трафик можно распределить между hello службу, которая выполняется на всех узлах в кластере hello.</span><span class="sxs-lookup"><span data-stu-id="f7f65-289">Client traffic can then be distributed across hello service that is running on all nodes in hello cluster.</span></span>

## <a name="check-your-running-application"></a><span data-ttu-id="f7f65-290">Проверка работающего приложения</span><span class="sxs-lookup"><span data-stu-id="f7f65-290">Check your running application</span></span>
<span data-ttu-id="f7f65-291">В обозреватель Service Fabric определите узел hello, где запущена служба hello.</span><span class="sxs-lookup"><span data-stu-id="f7f65-291">In Service Fabric Explorer, identify hello node where hello service is running.</span></span> <span data-ttu-id="f7f65-292">В этом примере она выполняется на узле Node1.</span><span class="sxs-lookup"><span data-stu-id="f7f65-292">In this example, it runs on Node1:</span></span>

![Узел, на котором запущена служба](./media/service-fabric-deploy-existing-app/nodeappinsfx.png)

<span data-ttu-id="f7f65-294">Если перехода узла toohello и toohello с приложением можно увидеть hello узел важные сведения, включая ее расположение на диске.</span><span class="sxs-lookup"><span data-stu-id="f7f65-294">If you navigate toohello node and browse toohello application, you see hello essential node information, including its location on disk.</span></span>

![Расположение на диске](./media/service-fabric-deploy-existing-app/locationondisk2.png)

<span data-ttu-id="f7f65-296">При просмотре каталога toohello с помощью обозревателя серверов можно найти hello рабочий каталог и папки журнала hello службы, как показано на следующий снимок экрана приветствия:</span><span class="sxs-lookup"><span data-stu-id="f7f65-296">If you browse toohello directory by using Server Explorer, you can find hello working directory and hello service's log folder, as shown in hello following screenshot:</span></span> 

![Расположение журнала](./media/service-fabric-deploy-existing-app/loglocation.png)

## <a name="next-steps"></a><span data-ttu-id="f7f65-298">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="f7f65-298">Next steps</span></span>
<span data-ttu-id="f7f65-299">В этой статье вы узнали как toopackage гостевой исполняемый файл и развернуть ее tooService структуры.</span><span class="sxs-lookup"><span data-stu-id="f7f65-299">In this article, you have learned how toopackage a guest executable and deploy it tooService Fabric.</span></span> <span data-ttu-id="f7f65-300">См. следующие статьи для связанной информации и задачи hello.</span><span class="sxs-lookup"><span data-stu-id="f7f65-300">See hello following articles for related information and tasks.</span></span>

* <span data-ttu-id="f7f65-301">[Пример для упаковки и развертывания гостевой исполняемый файл](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started), включая предварительный выпуск toohello ссылку средства упаковки hello</span><span class="sxs-lookup"><span data-stu-id="f7f65-301">[Sample for packaging and deploying a guest executable](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started), including a link toohello prerelease of hello packaging tool</span></span>
* [<span data-ttu-id="f7f65-302">Пример двух гостевой исполняемых файлов (C# и nodejs) общения с помощью службы именования hello, с помощью REST</span><span class="sxs-lookup"><span data-stu-id="f7f65-302">Sample of two guest executables (C# and nodejs) communicating via hello Naming service using REST</span></span>](https://github.com/Azure-Samples/service-fabric-dotnet-containers)
* [<span data-ttu-id="f7f65-303">Развертывание нескольких пользовательских приложений</span><span class="sxs-lookup"><span data-stu-id="f7f65-303">Deploy multiple guest executables</span></span>](service-fabric-deploy-multiple-apps.md)
* [<span data-ttu-id="f7f65-304">Создание первого приложения Service Fabric в Visual Studio</span><span class="sxs-lookup"><span data-stu-id="f7f65-304">Create your first Service Fabric application using Visual Studio</span></span>](service-fabric-create-your-first-application-in-visual-studio.md)
