---
title: "Развертывание существующего исполняемого файла в Azure Service Fabric | Документация Майкрософт"
description: "Пошаговое руководство по упаковке имеющегося приложения в качестве гостевого исполняемого файла для его развертывания в кластере Service Fabric."
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
ms.openlocfilehash: a1db3dda674ffe43587333d88f3816549af3019c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="deploy-a-guest-executable-to-service-fabric"></a><span data-ttu-id="e9cb7-103">Развертывание гостевого исполняемого файла в Service Fabric</span><span class="sxs-lookup"><span data-stu-id="e9cb7-103">Deploy a guest executable to Service Fabric</span></span>
<span data-ttu-id="e9cb7-104">В Azure Service Fabric можно запустить как службу приложение любого типа, в том числе приложения Node.js, Java или C++.</span><span class="sxs-lookup"><span data-stu-id="e9cb7-104">You can run any type of code, such as Node.js, Java, or C++ in Azure Service Fabric as a service.</span></span> <span data-ttu-id="e9cb7-105">В Service Fabric такие типы служб называются гостевыми исполняемыми файлами.</span><span class="sxs-lookup"><span data-stu-id="e9cb7-105">Service Fabric refers to these types of services as guest executables.</span></span>

<span data-ttu-id="e9cb7-106">Гостевые исполняемые файлы обрабатываются в Service Fabric как службы без отслеживания состояния.</span><span class="sxs-lookup"><span data-stu-id="e9cb7-106">Guest executables are treated by Service Fabric like stateless services.</span></span> <span data-ttu-id="e9cb7-107">Это значит, что они будут размещены на узлах кластера на основе доступности и других метрик.</span><span class="sxs-lookup"><span data-stu-id="e9cb7-107">As a result, they are placed on nodes in a cluster, based on availability and other metrics.</span></span> <span data-ttu-id="e9cb7-108">В этой статье описывается, как упаковать и развернуть гостевой исполняемый файл в кластере Service Fabric, используя Visual Studio или служебную программу командной строки.</span><span class="sxs-lookup"><span data-stu-id="e9cb7-108">This article describes how to package and deploy a guest executable to a Service Fabric cluster, by using Visual Studio or a command-line utility.</span></span>

<span data-ttu-id="e9cb7-109">Здесь мы рассмотрим процедуру упаковки гостевого исполняемого файла и его развертывания в Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="e9cb7-109">In this article, we cover the steps to package a guest executable and deploy it to Service Fabric.</span></span>  

## <a name="benefits-of-running-a-guest-executable-in-service-fabric"></a><span data-ttu-id="e9cb7-110">Преимущества запуска гостевого исполняемого файла в Service Fabric</span><span class="sxs-lookup"><span data-stu-id="e9cb7-110">Benefits of running a guest executable in Service Fabric</span></span>
<span data-ttu-id="e9cb7-111">Запуск гостевого исполняемого файла в кластере Service Fabric имеет несколько преимуществ.</span><span class="sxs-lookup"><span data-stu-id="e9cb7-111">There are several advantages to running a guest executable in a Service Fabric cluster:</span></span>

* <span data-ttu-id="e9cb7-112">обеспечение высокой доступности;</span><span class="sxs-lookup"><span data-stu-id="e9cb7-112">High availability.</span></span> <span data-ttu-id="e9cb7-113">Приложения, работающие в среде Service Fabric, отличаются высоким уровнем доступности.</span><span class="sxs-lookup"><span data-stu-id="e9cb7-113">Applications that run in Service Fabric are made highly available.</span></span> <span data-ttu-id="e9cb7-114">Service Fabric обеспечивает выполнение экземпляров приложения.</span><span class="sxs-lookup"><span data-stu-id="e9cb7-114">Service Fabric ensures that instances of an application are running.</span></span>
* <span data-ttu-id="e9cb7-115">Наблюдение за работоспособностью системы.</span><span class="sxs-lookup"><span data-stu-id="e9cb7-115">Health monitoring.</span></span> <span data-ttu-id="e9cb7-116">Service Fabric наблюдает за работоспособностью приложений и в случае сбоя предоставляет диагностические данные.</span><span class="sxs-lookup"><span data-stu-id="e9cb7-116">Service Fabric health monitoring detects if an application is running, and provides diagnostic information if there is a failure.</span></span>   
* <span data-ttu-id="e9cb7-117">Управление жизненным циклом приложений.</span><span class="sxs-lookup"><span data-stu-id="e9cb7-117">Application lifecycle management.</span></span> <span data-ttu-id="e9cb7-118">Service Fabric не только обновляет приложения без ущерба для работы пользователей, но и автоматически откатывает приложение к предыдущей версии, если во время обновления возникло событие ухудшения работоспособности.</span><span class="sxs-lookup"><span data-stu-id="e9cb7-118">Besides providing upgrades with no downtime, Service Fabric provides automatic rollback to the previous version if there is a bad health event reported during an upgrade.</span></span>    
* <span data-ttu-id="e9cb7-119">Плотность.</span><span class="sxs-lookup"><span data-stu-id="e9cb7-119">Density.</span></span> <span data-ttu-id="e9cb7-120">В одном кластере могут работать несколько приложений, что позволяет отказаться от использования отдельного оборудования для каждого приложения.</span><span class="sxs-lookup"><span data-stu-id="e9cb7-120">You can run multiple applications in a cluster, which eliminates the need for each application to run on its own hardware.</span></span>
* <span data-ttu-id="e9cb7-121">Возможность обнаружения: с помощью REST можно вызвать службу именования Service Fabric для поиска других служб в кластере.</span><span class="sxs-lookup"><span data-stu-id="e9cb7-121">Discoverability: Using REST you can call the Service Fabric Naming service to find other services in the cluster.</span></span> 

## <a name="samples"></a><span data-ttu-id="e9cb7-122">Примеры</span><span class="sxs-lookup"><span data-stu-id="e9cb7-122">Samples</span></span>
* [<span data-ttu-id="e9cb7-123">Пример для упаковки и развертывания гостевого исполняемого файла</span><span class="sxs-lookup"><span data-stu-id="e9cb7-123">Sample for packaging and deploying a guest executable</span></span>](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started)
* [<span data-ttu-id="e9cb7-124">Пример двух гостевых исполняемых файлов (C# и Node.js), которые взаимодействуют через службу именования с помощью REST</span><span class="sxs-lookup"><span data-stu-id="e9cb7-124">Sample of two guest executables (C# and nodejs) communicating via the Naming service using REST</span></span>](https://github.com/Azure-Samples/service-fabric-dotnet-containers)

## <a name="overview-of-application-and-service-manifest-files"></a><span data-ttu-id="e9cb7-125">Обзор файлов манифестов приложений и служб</span><span class="sxs-lookup"><span data-stu-id="e9cb7-125">Overview of application and service manifest files</span></span>
<span data-ttu-id="e9cb7-126">При развертывании гостевого исполняемого файла рекомендуем ознакомиться с моделью развертывания и упаковки Service Fabric, которая описана в [этой статье](service-fabric-application-model.md).</span><span class="sxs-lookup"><span data-stu-id="e9cb7-126">As part of deploying a guest executable, it is useful to understand the Service Fabric packaging and deployment model as described in [application model](service-fabric-application-model.md).</span></span> <span data-ttu-id="e9cb7-127">Модель упаковки Service Fabric основана на двух XML-файлах — манифестах приложения и службы.</span><span class="sxs-lookup"><span data-stu-id="e9cb7-127">The Service Fabric packaging model relies on two XML files: the application and service manifests.</span></span> <span data-ttu-id="e9cb7-128">Определение схемы для файла ApplicationManifest.xml и ServiceManifest.xml устанавливается с пакетом SDK в расположении *C:\Program Files\Microsoft SDKs\Service Fabric\schemas\ServiceFabricServiceModel.xsd*.</span><span class="sxs-lookup"><span data-stu-id="e9cb7-128">The schema definition for the ApplicationManifest.xml and ServiceManifest.xml files is installed with the Service Fabric SDK into *C:\Program Files\Microsoft SDKs\Service Fabric\schemas\ServiceFabricServiceModel.xsd*.</span></span>

* <span data-ttu-id="e9cb7-129">**Манифест приложения.** Этот манифест используется для описания приложения.</span><span class="sxs-lookup"><span data-stu-id="e9cb7-129">**Application manifest** The application manifest is used to describe the application.</span></span> <span data-ttu-id="e9cb7-130">В файле указаны службы, из которых состоит приложение, и другие параметры развертывания для одной или нескольких служб (например, число экземпляров).</span><span class="sxs-lookup"><span data-stu-id="e9cb7-130">It lists the services that compose it, and other parameters that are used to define how one or more services should be deployed, such as the number of instances.</span></span>

  <span data-ttu-id="e9cb7-131">В Service Fabric приложение — это единица развертывания и обновления.</span><span class="sxs-lookup"><span data-stu-id="e9cb7-131">In Service Fabric, an application is a unit of deployment and upgrade.</span></span> <span data-ttu-id="e9cb7-132">Приложение может обновляться как одна единица, для которой выполняется управление потенциальными сбоями и откатами.</span><span class="sxs-lookup"><span data-stu-id="e9cb7-132">An application can be upgraded as a single unit where potential failures and potential rollbacks are managed.</span></span> <span data-ttu-id="e9cb7-133">Service Fabric гарантирует, что процесс обновления либо будет выполнен успешно, либо (в случае сбоя) не оставит приложение в неизвестном или нестабильном состоянии.</span><span class="sxs-lookup"><span data-stu-id="e9cb7-133">Service Fabric guarantees that the upgrade process is either successful, or, if the upgrade fails, does not leave the application in an unknown or unstable state.</span></span>
* <span data-ttu-id="e9cb7-134">**Манифест служб.** Манифест служб описывает компоненты службы.</span><span class="sxs-lookup"><span data-stu-id="e9cb7-134">**Service manifest** The service manifest describes the components of a service.</span></span> <span data-ttu-id="e9cb7-135">В этом файле содержится такая информация, как имя и тип службы, ее код и конфигурация.</span><span class="sxs-lookup"><span data-stu-id="e9cb7-135">It includes data, such as the name and type of service, and its code and configuration.</span></span> <span data-ttu-id="e9cb7-136">Манифест службы также включает некоторые дополнительные параметры, которые могут использоваться для настройки службы после ее развертывания.</span><span class="sxs-lookup"><span data-stu-id="e9cb7-136">The service manifest also includes some additional parameters that can be used to configure the service once it is deployed.</span></span>

## <a name="application-package-file-structure"></a><span data-ttu-id="e9cb7-137">Структура файла пакета приложения</span><span class="sxs-lookup"><span data-stu-id="e9cb7-137">Application package file structure</span></span>
<span data-ttu-id="e9cb7-138">Чтобы развернуть приложение в Service Fabric, такое приложение должно соответствовать предопределенной структуре каталогов.</span><span class="sxs-lookup"><span data-stu-id="e9cb7-138">To deploy an application to Service Fabric, the application should follow a predefined directory structure.</span></span> <span data-ttu-id="e9cb7-139">Ниже приведен пример этой структуры.</span><span class="sxs-lookup"><span data-stu-id="e9cb7-139">The following is an example of that structure.</span></span>

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

<span data-ttu-id="e9cb7-140">Каталог ApplicationPackageRoot содержит файл ApplicationManifest.xml, определяющий приложение.</span><span class="sxs-lookup"><span data-stu-id="e9cb7-140">The ApplicationPackageRoot contains the ApplicationManifest.xml file that defines the application.</span></span> <span data-ttu-id="e9cb7-141">Дочерний каталог для каждой службы, включенной в приложение, используется для хранения всех артефактов, необходимых службе.</span><span class="sxs-lookup"><span data-stu-id="e9cb7-141">A subdirectory for each service included in the application is used to contain all the artifacts that the service requires.</span></span> <span data-ttu-id="e9cb7-142">Подкаталоги включают файл ServiceManifest.xml и, как правило, следующие каталоги:</span><span class="sxs-lookup"><span data-stu-id="e9cb7-142">These subdirectories are the ServiceManifest.xml and, typically, the following:</span></span>

* <span data-ttu-id="e9cb7-143">*Code*.</span><span class="sxs-lookup"><span data-stu-id="e9cb7-143">*Code*.</span></span> <span data-ttu-id="e9cb7-144">В этом каталоге содержится код службы.</span><span class="sxs-lookup"><span data-stu-id="e9cb7-144">This directory contains the service code.</span></span>
* <span data-ttu-id="e9cb7-145">*Config*.</span><span class="sxs-lookup"><span data-stu-id="e9cb7-145">*Config*.</span></span> <span data-ttu-id="e9cb7-146">В этом каталоге хранится файл Settings.xml (а также другие файлы, если они нужны), который выполняемая служба может использовать для получения определенных параметров конфигурации.</span><span class="sxs-lookup"><span data-stu-id="e9cb7-146">This directory contains a Settings.xml file (and other files if necessary) that the service can access at runtime to retrieve specific configuration settings.</span></span>
* <span data-ttu-id="e9cb7-147">*Data*.</span><span class="sxs-lookup"><span data-stu-id="e9cb7-147">*Data*.</span></span> <span data-ttu-id="e9cb7-148">Здесь хранятся дополнительные локальные данные, которые могут потребоваться службе.</span><span class="sxs-lookup"><span data-stu-id="e9cb7-148">This is an additional directory to store additional local data that the service may need.</span></span> <span data-ttu-id="e9cb7-149">Обратите внимание, что в этом каталоге могут храниться только временные данные.</span><span class="sxs-lookup"><span data-stu-id="e9cb7-149">Data should be used to store only ephemeral data.</span></span> <span data-ttu-id="e9cb7-150">Service Fabric не копирует и не реплицирует изменения, внесенные в каталог Data, при перемещении службы (например, во время отработки отказа).</span><span class="sxs-lookup"><span data-stu-id="e9cb7-150">Service Fabric does not copy or replicate changes to the data directory if the service needs to be relocated (for example, during failover).</span></span>

> [!NOTE]
> <span data-ttu-id="e9cb7-151">Если каталоги `config` и `data` вам не нужны, не создавайте их.</span><span class="sxs-lookup"><span data-stu-id="e9cb7-151">You don't have to create the `config` and `data` directories if you don't need them.</span></span>
>
>

## <a name="package-an-existing-executable"></a><span data-ttu-id="e9cb7-152">Упаковка существующего исполняемого файла</span><span class="sxs-lookup"><span data-stu-id="e9cb7-152">Package an existing executable</span></span>
<span data-ttu-id="e9cb7-153">При упаковке гостевого исполняемого файла вы можете использовать шаблон проекта Visual Studio или [создать пакет приложения вручную](#manually).</span><span class="sxs-lookup"><span data-stu-id="e9cb7-153">When packaging a guest executable, you can choose either to use a Visual Studio project template or to [create the application package manually](#manually).</span></span> <span data-ttu-id="e9cb7-154">При использовании Visual Studio шаблон проекта создает для вас структуру пакета приложения и файлы манифеста.</span><span class="sxs-lookup"><span data-stu-id="e9cb7-154">Using Visual Studio, the application package structure and manifest files are created by the new project template for you.</span></span>

> [!TIP]
> <span data-ttu-id="e9cb7-155">Упаковать имеющийся исполняемый файл Windows в службу проще всего с помощью Visual Studio. В Linux можно использовать Yeoman.</span><span class="sxs-lookup"><span data-stu-id="e9cb7-155">The easiest way to package an existing Windows executable into a service is to use Visual Studio and on Linux to use Yeoman</span></span>
>

## <a name="use-visual-studio-to-package-and-deploy-an-existing-executable"></a><span data-ttu-id="e9cb7-156">Упаковка и развертывание существующего исполняемого приложения с использованием Visual Studio</span><span class="sxs-lookup"><span data-stu-id="e9cb7-156">Use Visual Studio to package and deploy an existing executable</span></span>
<span data-ttu-id="e9cb7-157">Visual Studio предоставляет шаблон службы Service Fabric для развертывания гостевого исполняемого файла в кластере Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="e9cb7-157">Visual Studio provides a Service Fabric service template to help you deploy a guest executable to a Service Fabric cluster.</span></span>

1. <span data-ttu-id="e9cb7-158">Чтобы создать приложение Service Fabric, выберите **Файл** > **Создать проект**.</span><span class="sxs-lookup"><span data-stu-id="e9cb7-158">Choose **File** > **New Project**, and create a Service Fabric application.</span></span>
2. <span data-ttu-id="e9cb7-159">Выберите **гостевой исполняемый файл** в качестве шаблона службы.</span><span class="sxs-lookup"><span data-stu-id="e9cb7-159">Choose **Guest Executable** as the service template.</span></span>
3. <span data-ttu-id="e9cb7-160">Щелкните **Обзор**, чтобы выбрать папку с исполняемым файлом, и определите остальные параметры, необходимые для создания службы.</span><span class="sxs-lookup"><span data-stu-id="e9cb7-160">Click **Browse** to select the folder with your executable and fill in the rest of the parameters to create the service.</span></span>
   * <span data-ttu-id="e9cb7-161">*Поведение пакета кода*.</span><span class="sxs-lookup"><span data-stu-id="e9cb7-161">*Code Package Behavior*.</span></span> <span data-ttu-id="e9cb7-162">Здесь можно выбрать копирование всего содержимого папки в проект Visual Studio. Это удобно, если исполняемый файл не будет изменяться.</span><span class="sxs-lookup"><span data-stu-id="e9cb7-162">Can be set to copy all the content of your folder to the Visual Studio Project, which is useful if the executable does not change.</span></span> <span data-ttu-id="e9cb7-163">Если исполняемый файл будет изменяться и требуется возможность выбора новых сборок в динамическом режиме, можно задать привязку к папке.</span><span class="sxs-lookup"><span data-stu-id="e9cb7-163">If you expect the executable to change and want the ability to pick up new builds dynamically, you can choose to link to the folder instead.</span></span> <span data-ttu-id="e9cb7-164">При создании проекта приложения в Visual Studio можно использовать связанные папки.</span><span class="sxs-lookup"><span data-stu-id="e9cb7-164">You can use linked folders when creating the application project in Visual Studio.</span></span> <span data-ttu-id="e9cb7-165">С их помощью можно ссылаться на исходное расположение в проекте, что позволяет обновлять гостевой исполняемый файл в источнике.</span><span class="sxs-lookup"><span data-stu-id="e9cb7-165">This links to the source location from within the project, making it possible for you to update the guest executable in its source destination.</span></span> <span data-ttu-id="e9cb7-166">Эти обновления при создании становятся частью пакета приложения.</span><span class="sxs-lookup"><span data-stu-id="e9cb7-166">Those updates become part of the application package on build.</span></span>
   * <span data-ttu-id="e9cb7-167">*Program* обозначает исполняемый файл, который следует выполнить для запуска службы.</span><span class="sxs-lookup"><span data-stu-id="e9cb7-167">*Program* specifies the executable that should be run to start the service.</span></span>
   * <span data-ttu-id="e9cb7-168">*Arguments* позволяет указать аргументы, которые нужно передать в исполняемый файл.</span><span class="sxs-lookup"><span data-stu-id="e9cb7-168">*Arguments* specifies the arguments that should be passed to the executable.</span></span> <span data-ttu-id="e9cb7-169">Здесь можно указать список параметров с аргументами.</span><span class="sxs-lookup"><span data-stu-id="e9cb7-169">It can be a list of parameters with arguments.</span></span>
   * <span data-ttu-id="e9cb7-170">*WorkingFolder* позволяет определить рабочий каталог для процесса, который будет запущен.</span><span class="sxs-lookup"><span data-stu-id="e9cb7-170">*WorkingFolder* specifies the working directory for the process that is going to be started.</span></span> <span data-ttu-id="e9cb7-171">Можно задать три значения:</span><span class="sxs-lookup"><span data-stu-id="e9cb7-171">You can specify three values:</span></span>
     * <span data-ttu-id="e9cb7-172">`CodeBase`. Рабочим каталогом будет каталог Code в пакете приложения (каталог `Code` в показанной выше структуре файлов).</span><span class="sxs-lookup"><span data-stu-id="e9cb7-172">`CodeBase` specifies that the working directory is going to be set to the code directory in the application package (`Code` directory shown in the preceding file structure).</span></span>
     * <span data-ttu-id="e9cb7-173">`CodePackage`. Рабочим каталогом будет корневой каталог в пакете приложения (каталог `GuestService1Pkg` в показанной выше структуре файлов).</span><span class="sxs-lookup"><span data-stu-id="e9cb7-173">`CodePackage` specifies that the working directory is going to be set to the root of the application package    (`GuestService1Pkg` shown in the preceding file structure).</span></span>
     * <span data-ttu-id="e9cb7-174">`Work`. Файлы помещаются в подкаталог, который называется рабочим.</span><span class="sxs-lookup"><span data-stu-id="e9cb7-174">`Work` specifies that the files are placed in a subdirectory called work.</span></span>
4. <span data-ttu-id="e9cb7-175">Присвойте службе имя и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="e9cb7-175">Give your service a name, and click **OK**.</span></span>
5. <span data-ttu-id="e9cb7-176">Если службе нужна конечная точка для обмена данными, можно добавить значения протокола, порта и типа в файл ServiceManifest.xml.</span><span class="sxs-lookup"><span data-stu-id="e9cb7-176">If your service needs an endpoint for communication, you can now add the protocol, port, and type to the ServiceManifest.xml file.</span></span> <span data-ttu-id="e9cb7-177">Например, `<Endpoint Name="NodeAppTypeEndpoint" Protocol="http" Port="3000" UriScheme="http" PathSuffix="myapp/" Type="Input" />`.</span><span class="sxs-lookup"><span data-stu-id="e9cb7-177">For example: `<Endpoint Name="NodeAppTypeEndpoint" Protocol="http" Port="3000" UriScheme="http" PathSuffix="myapp/" Type="Input" />`.</span></span>
6. <span data-ttu-id="e9cb7-178">Теперь можно выполнить упаковку и публикацию на локальном кластере, выполнив отладку решения в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="e9cb7-178">You can now use the package and publish action against your local cluster by debugging the solution in Visual Studio.</span></span> <span data-ttu-id="e9cb7-179">Когда все будет готово, можно опубликовать приложение на удаленном кластере или вернуть решение в систему управления версиями.</span><span class="sxs-lookup"><span data-stu-id="e9cb7-179">When ready, you can publish the application to a remote cluster or check in the solution to source control.</span></span>
7. <span data-ttu-id="e9cb7-180">Перейдите к концу этой статьи, чтобы узнать, как просмотреть данные о работе гостевого исполняемого файла в Service Fabric Explorer.</span><span class="sxs-lookup"><span data-stu-id="e9cb7-180">Go to the end of this article to see how to view your guest executable service running in Service Fabric Explorer.</span></span>

## <a name="use-yoeman-to-package-and-deploy-an-existing-executable-on-linux"></a><span data-ttu-id="e9cb7-181">Упаковка и развертывание существующего исполняемого файла с помощью Yoeman в Linux</span><span class="sxs-lookup"><span data-stu-id="e9cb7-181">Use Yoeman to package and deploy an existing executable on Linux</span></span>

<span data-ttu-id="e9cb7-182">Процедура создания и развертывания гостевого исполняемого файла в Linux совпадает с процедурой развертывания приложения csharp или java.</span><span class="sxs-lookup"><span data-stu-id="e9cb7-182">The procedure for creating and deploying a guest executable on Linux is the same as deploying a csharp or java application.</span></span>

1. <span data-ttu-id="e9cb7-183">В окне терминала введите `yo azuresfguest`.</span><span class="sxs-lookup"><span data-stu-id="e9cb7-183">In a terminal, type `yo azuresfguest`.</span></span>
2. <span data-ttu-id="e9cb7-184">Присвойте имя приложению.</span><span class="sxs-lookup"><span data-stu-id="e9cb7-184">Name your application.</span></span>
3. <span data-ttu-id="e9cb7-185">Введите имя службы и укажите сведения, включая путь к исполняемому файлу и параметры, с которыми он должен вызываться.</span><span class="sxs-lookup"><span data-stu-id="e9cb7-185">Name your service, and provide the details including path of the executable and the parameters it must be invoked with.</span></span>

<span data-ttu-id="e9cb7-186">Yeoman создает пакет приложения с соответствующими файлами приложения и манифеста, а также со сценариями установки и удаления.</span><span class="sxs-lookup"><span data-stu-id="e9cb7-186">Yeoman creates an application package with the appropriate application and manifest files along with install and uninstall scripts.</span></span>

<a id="manually"></a>

## <a name="manually-package-and-deploy-an-existing-executable"></a><span data-ttu-id="e9cb7-187">Упаковка и развертывание имеющегося исполняемого файла вручную</span><span class="sxs-lookup"><span data-stu-id="e9cb7-187">Manually package and deploy an existing executable</span></span>
<span data-ttu-id="e9cb7-188">Процесс упаковки гостевого исполняемого файла вручную включает следующие этапы:</span><span class="sxs-lookup"><span data-stu-id="e9cb7-188">The process of manually packaging a guest executable is based on the following general steps:</span></span>

1. <span data-ttu-id="e9cb7-189">Создание структуры каталогов пакета.</span><span class="sxs-lookup"><span data-stu-id="e9cb7-189">Create the package directory structure.</span></span>
2. <span data-ttu-id="e9cb7-190">Добавление файлов конфигурации и кода приложения.</span><span class="sxs-lookup"><span data-stu-id="e9cb7-190">Add the application's code and configuration files.</span></span>
3. <span data-ttu-id="e9cb7-191">Редактирование файла манифеста службы.</span><span class="sxs-lookup"><span data-stu-id="e9cb7-191">Edit the service manifest file.</span></span>
4. <span data-ttu-id="e9cb7-192">Редактирование файла манифеста приложения.</span><span class="sxs-lookup"><span data-stu-id="e9cb7-192">Edit the application manifest file.</span></span>

<!--
>[AZURE.NOTE] We do provide a packaging tool that allows you to create the ApplicationPackage automatically. The tool is currently in preview. You can download it from [here](http://aka.ms/servicefabricpacktool).
-->

### <a name="create-the-package-directory-structure"></a><span data-ttu-id="e9cb7-193">Создание структуры каталогов пакета</span><span class="sxs-lookup"><span data-stu-id="e9cb7-193">Create the package directory structure</span></span>
<span data-ttu-id="e9cb7-194">Для начала можно создать структуру каталогов, как описано в предыдущем разделе "Структура файлов для пакета приложения".</span><span class="sxs-lookup"><span data-stu-id="e9cb7-194">You can start by creating the directory structure, as described in the preceding section, "Application package file structure."</span></span>

### <a name="add-the-applications-code-and-configuration-files"></a><span data-ttu-id="e9cb7-195">Добавление файлов конфигурации и кода приложения</span><span class="sxs-lookup"><span data-stu-id="e9cb7-195">Add the application's code and configuration files</span></span>
<span data-ttu-id="e9cb7-196">Создав структуру каталогов, добавьте файлы кода и конфигурации приложения в каталоги Code и Config.</span><span class="sxs-lookup"><span data-stu-id="e9cb7-196">After you have created the directory structure, you can add the application's code and configuration files under the code and config directories.</span></span> <span data-ttu-id="e9cb7-197">При необходимости в этих каталогах можно создать дополнительные папки (подкаталоги).</span><span class="sxs-lookup"><span data-stu-id="e9cb7-197">You can also create additional directories or subdirectories under the code or config directories.</span></span>

<span data-ttu-id="e9cb7-198">Service Fabric создает расширенную копию содержимого корневого каталога приложения (выполняется операция `xcopy`), поэтому вам нужно создать только два каталога верхнего уровня: для кода и для параметров.</span><span class="sxs-lookup"><span data-stu-id="e9cb7-198">Service Fabric does an `xcopy` of the content of the application root directory, so there is no predefined structure to use other than creating two top directories, code and settings.</span></span> <span data-ttu-id="e9cb7-199">(Вы можете выбрать любые имена.</span><span class="sxs-lookup"><span data-stu-id="e9cb7-199">(You can pick different names if you want.</span></span> <span data-ttu-id="e9cb7-200">Дополнительные сведения см. в следующем разделе.)</span><span class="sxs-lookup"><span data-stu-id="e9cb7-200">More details are in the next section.)</span></span>

> [!NOTE]
> <span data-ttu-id="e9cb7-201">Обязательно добавьте все файлы и зависимости, необходимые приложению.</span><span class="sxs-lookup"><span data-stu-id="e9cb7-201">Make sure that you include all the files and dependencies that the application needs.</span></span> <span data-ttu-id="e9cb7-202">Service Fabric скопирует содержимое пакета приложения на все узлы кластера, где будут развертываться службы приложения.</span><span class="sxs-lookup"><span data-stu-id="e9cb7-202">Service Fabric copies the content of the application package on all nodes in the cluster where the application's services are going to be deployed.</span></span> <span data-ttu-id="e9cb7-203">Пакет должен содержать весь код, необходимый для работы приложения.</span><span class="sxs-lookup"><span data-stu-id="e9cb7-203">The package should contain all the code that the application needs to run.</span></span> <span data-ttu-id="e9cb7-204">Не рассчитывайте на то, что зависимости уже установлены.</span><span class="sxs-lookup"><span data-stu-id="e9cb7-204">Do not assume that the dependencies are already installed.</span></span>
>
>

### <a name="edit-the-service-manifest-file"></a><span data-ttu-id="e9cb7-205">Редактирование файла манифеста службы</span><span class="sxs-lookup"><span data-stu-id="e9cb7-205">Edit the service manifest file</span></span>
<span data-ttu-id="e9cb7-206">Далее нужно добавить в манифест службы следующие сведения:</span><span class="sxs-lookup"><span data-stu-id="e9cb7-206">The next step is to edit the service manifest file to include the following information:</span></span>

* <span data-ttu-id="e9cb7-207">Имя типа службы.</span><span class="sxs-lookup"><span data-stu-id="e9cb7-207">The name of the service type.</span></span> <span data-ttu-id="e9cb7-208">Это идентификатор, по которому Service Fabric определяет службу.</span><span class="sxs-lookup"><span data-stu-id="e9cb7-208">This is an ID that Service Fabric uses to identify a service.</span></span>
* <span data-ttu-id="e9cb7-209">Команда для запуска приложения (ExeHost).</span><span class="sxs-lookup"><span data-stu-id="e9cb7-209">The command to use to launch the application (ExeHost).</span></span>
* <span data-ttu-id="e9cb7-210">Любой сценарий, который нужно выполнить для установки приложения (SetupEntrypoint).</span><span class="sxs-lookup"><span data-stu-id="e9cb7-210">Any script that needs to be run to set up the application (SetupEntrypoint).</span></span>

<span data-ttu-id="e9cb7-211">Ниже приведен пример файла `ServiceManifest.xml` .</span><span class="sxs-lookup"><span data-stu-id="e9cb7-211">The following is an example of a `ServiceManifest.xml` file:</span></span>

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

<span data-ttu-id="e9cb7-212">В следующих разделах мы рассмотрим те элементы файла, которые вам нужно изменить.</span><span class="sxs-lookup"><span data-stu-id="e9cb7-212">The following sections go over the different parts of the file that you need to update.</span></span>

#### <a name="update-servicetypes"></a><span data-ttu-id="e9cb7-213">Обновление ServiceTypes</span><span class="sxs-lookup"><span data-stu-id="e9cb7-213">Update ServiceTypes</span></span>
```xml
<ServiceTypes>
  <StatelessServiceType ServiceTypeName="NodeApp" UseImplicitHost="true" />
</ServiceTypes>
```

* <span data-ttu-id="e9cb7-214">Выберите для `ServiceTypeName`любое имя.</span><span class="sxs-lookup"><span data-stu-id="e9cb7-214">You can pick any name that you want for `ServiceTypeName`.</span></span> <span data-ttu-id="e9cb7-215">Значение используется в файле `ApplicationManifest.xml` для идентификации службы.</span><span class="sxs-lookup"><span data-stu-id="e9cb7-215">The value is used in the `ApplicationManifest.xml` file to identify the service.</span></span>
* <span data-ttu-id="e9cb7-216">Укажите `UseImplicitHost="true"`.</span><span class="sxs-lookup"><span data-stu-id="e9cb7-216">Specify `UseImplicitHost="true"`.</span></span> <span data-ttu-id="e9cb7-217">Этот атрибут сообщает платформе Service Fabric, что служба использует автономное приложение, поэтому платформе нужно только запустить службу как процесс и следить за ее работоспособностью.</span><span class="sxs-lookup"><span data-stu-id="e9cb7-217">This attribute tells Service Fabric that the service is based on a self-contained app, so all Service Fabric needs to do is to launch it as a process and monitor its health.</span></span>

#### <a name="update-codepackage"></a><span data-ttu-id="e9cb7-218">Обновление CodePackage</span><span class="sxs-lookup"><span data-stu-id="e9cb7-218">Update CodePackage</span></span>
<span data-ttu-id="e9cb7-219">Элемент CodePackage указывает на расположение и версию кода службы.</span><span class="sxs-lookup"><span data-stu-id="e9cb7-219">The CodePackage element specifies the location (and version) of the service's code.</span></span>

```xml
<CodePackage Name="Code" Version="1.0.0.0">
```

<span data-ttu-id="e9cb7-220">Атрибут `Name` определяет имя каталога в пакете приложения, где хранится код службы.</span><span class="sxs-lookup"><span data-stu-id="e9cb7-220">The `Name` element is used to specify the name of the directory in the application package that contains the service's code.</span></span> <span data-ttu-id="e9cb7-221">`CodePackage` также имеет атрибут `version`.</span><span class="sxs-lookup"><span data-stu-id="e9cb7-221">`CodePackage` also has the `version` attribute.</span></span> <span data-ttu-id="e9cb7-222">Он определяет версию кода, а также может использоваться для обновления кода службы с помощью инфраструктуры Service Fabric для управления жизненным циклом приложения.</span><span class="sxs-lookup"><span data-stu-id="e9cb7-222">This can be used to specify the version of the code, and can also potentially be used to upgrade the service's code by using the application lifecycle management infrastructure in Service Fabric.</span></span>

#### <a name="optional-update-setupentrypoint"></a><span data-ttu-id="e9cb7-223">Обновление SetupEntrypoint (необязательно)</span><span class="sxs-lookup"><span data-stu-id="e9cb7-223">Optional: Update SetupEntrypoint</span></span>
```xml
<SetupEntryPoint>
   <ExeHost>
       <Program>scripts\launchConfig.cmd</Program>
   </ExeHost>
</SetupEntryPoint>
```
<span data-ttu-id="e9cb7-224">Элемент SetupEntrypoint позволяет определить исполняемый или пакетный файл, который следует запустить перед выполнением кода службы.</span><span class="sxs-lookup"><span data-stu-id="e9cb7-224">The SetupEntryPoint element is used to specify any executable or batch file that should be executed before the service's code is launched.</span></span> <span data-ttu-id="e9cb7-225">Это необязательный шаг, поэтому этот элемент можно не указывать, если инициализация не требуется.</span><span class="sxs-lookup"><span data-stu-id="e9cb7-225">It is an optional step, so it does not need to be included if there is no initialization required.</span></span> <span data-ttu-id="e9cb7-226">Файл, указанный в SetupEntryPoint, выполняется при каждом перезапуске службы.</span><span class="sxs-lookup"><span data-stu-id="e9cb7-226">The SetupEntryPoint is executed every time the service is restarted.</span></span>

<span data-ttu-id="e9cb7-227">Есть только один элемент SetupEntrypoint, следовательно, если для установки приложения требуется несколько скриптов, эти скрипты необходимо сгруппировать в один пакетный файл.</span><span class="sxs-lookup"><span data-stu-id="e9cb7-227">There is only one SetupEntryPoint, so setup scripts need to be grouped in a single batch file if the application's setup requires multiple scripts.</span></span> <span data-ttu-id="e9cb7-228">SetupEntryPoint может выполнять файлы любого типа, включая исполняемые и пакетные, а также командлеты PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e9cb7-228">The SetupEntryPoint can execute any type of file: executable files, batch files, and PowerShell cmdlets.</span></span> <span data-ttu-id="e9cb7-229">Подробнее см. в статье [Настройка SetupEntryPoint](service-fabric-application-runas-security.md).</span><span class="sxs-lookup"><span data-stu-id="e9cb7-229">For more details, see [Configure SetupEntryPoint](service-fabric-application-runas-security.md).</span></span>

<span data-ttu-id="e9cb7-230">В приведенном выше примере в разделе SetupEntrypoint запускается пакетный файл `LaunchConfig.cmd`, расположенный в подкаталоге `scripts` каталога Code (при условии, что в элементе WorkingFolder указано имя каталога CodeBase).</span><span class="sxs-lookup"><span data-stu-id="e9cb7-230">In the preceding example, the SetupEntryPoint runs a batch file called `LaunchConfig.cmd` that is located in the `scripts` subdirectory of the code directory (assuming the WorkingFolder element is set to CodeBase).</span></span>

#### <a name="update-entrypoint"></a><span data-ttu-id="e9cb7-231">Обновление EntryPoint</span><span class="sxs-lookup"><span data-stu-id="e9cb7-231">Update EntryPoint</span></span>
```xml
<EntryPoint>
  <ExeHost>
    <Program>node.exe</Program>
    <Arguments>bin/www</Arguments>
    <WorkingFolder>CodeBase</WorkingFolder>
  </ExeHost>
</EntryPoint>
```

<span data-ttu-id="e9cb7-232">Элемент `EntryPoint` в файле манифеста службы указывает, как нужно запускать службу.</span><span class="sxs-lookup"><span data-stu-id="e9cb7-232">The `EntryPoint` element in the service manifest file is used to specify how to launch the service.</span></span> <span data-ttu-id="e9cb7-233">В элементе `ExeHost` указывается исполняемый файл (вместе с аргументами), который будет использоваться для запуска службы.</span><span class="sxs-lookup"><span data-stu-id="e9cb7-233">The `ExeHost` element specifies the executable (and arguments) that should be used to launch the service.</span></span>

* <span data-ttu-id="e9cb7-234">`Program` — имя исполняемого файла, который будет запускать службу.</span><span class="sxs-lookup"><span data-stu-id="e9cb7-234">`Program` specifies the name of the executable that should start the service.</span></span>
* <span data-ttu-id="e9cb7-235">`Arguments` — аргументы, которые нужно передать в исполняемый файл.</span><span class="sxs-lookup"><span data-stu-id="e9cb7-235">`Arguments` specifies the arguments that should be passed to the executable.</span></span> <span data-ttu-id="e9cb7-236">Здесь можно указать список параметров с аргументами.</span><span class="sxs-lookup"><span data-stu-id="e9cb7-236">It can be a list of parameters with arguments.</span></span>
* <span data-ttu-id="e9cb7-237">`WorkingFolder` — рабочий каталог запускаемого процесса.</span><span class="sxs-lookup"><span data-stu-id="e9cb7-237">`WorkingFolder` specifies the working directory for the process that is going to be started.</span></span> <span data-ttu-id="e9cb7-238">Можно задать три значения:</span><span class="sxs-lookup"><span data-stu-id="e9cb7-238">You can specify three values:</span></span>
  * <span data-ttu-id="e9cb7-239">`CodeBase`. Рабочим каталогом будет каталог Code в пакете приложения (каталог `Code` в показанной выше структуре файлов).</span><span class="sxs-lookup"><span data-stu-id="e9cb7-239">`CodeBase` specifies that the working directory is going to be set to the code directory in the application package (`Code` directory in the preceding file structure).</span></span>
  * <span data-ttu-id="e9cb7-240">`CodePackage`. Рабочим каталогом будет корневой каталог в пакете приложения (каталог `GuestService1Pkg` в показанной выше структуре файлов).</span><span class="sxs-lookup"><span data-stu-id="e9cb7-240">`CodePackage` specifies that the working directory is going to be set to the root of the application package    (`GuestService1Pkg` in the preceding file structure).</span></span>
    * <span data-ttu-id="e9cb7-241">`Work`. Файлы помещаются в подкаталог, который называется рабочим.</span><span class="sxs-lookup"><span data-stu-id="e9cb7-241">`Work` specifies that the files are placed in a subdirectory called work.</span></span>

<span data-ttu-id="e9cb7-242">Элемент WorkingFolder позволяет задать правильный рабочий каталог, чтобы приложение или сценарии инициализации могли использовать относительные пути.</span><span class="sxs-lookup"><span data-stu-id="e9cb7-242">The WorkingFolder is useful to set the correct working directory so that relative paths can be used by either the application or initialization scripts.</span></span>

#### <a name="update-endpoints-and-register-with-naming-service-for-communication"></a><span data-ttu-id="e9cb7-243">Обновление конечных точек и регистрация в службе именования для обмена данными</span><span class="sxs-lookup"><span data-stu-id="e9cb7-243">Update Endpoints and register with Naming Service for communication</span></span>
```xml
<Endpoints>
   <Endpoint Name="NodeAppTypeEndpoint" Protocol="http" Port="3000" Type="Input" />
</Endpoints>

```
<span data-ttu-id="e9cb7-244">В приведенном выше примере в элементе `Endpoint` указываются конечные точки, через которые приложение может ожидать передачи данных.</span><span class="sxs-lookup"><span data-stu-id="e9cb7-244">In the preceding example, the `Endpoint` element specifies the endpoints that the application can listen on.</span></span> <span data-ttu-id="e9cb7-245">В этом примере приложение Node.js прослушивает HTTP-порт 3000.</span><span class="sxs-lookup"><span data-stu-id="e9cb7-245">In this example, the Node.js application listens on http on port 3000.</span></span>

<span data-ttu-id="e9cb7-246">Кроме того, можно настроить так, чтобы служба Service Fabric опубликовала конечную точку в службе именования.</span><span class="sxs-lookup"><span data-stu-id="e9cb7-246">Furthermore you can ask Service Fabric to publish this endpoint to the Naming Service so other services can discover the endpoint address to this service.</span></span> <span data-ttu-id="e9cb7-247">Таким образом, другие службы смогут обнаружить адрес конечной точки для этой службы.</span><span class="sxs-lookup"><span data-stu-id="e9cb7-247">This enables you to be able to communicate between services that are guest executables.</span></span>
<span data-ttu-id="e9cb7-248">Опубликованный адрес конечной точки имеет вид `UriScheme://IPAddressOrFQDN:Port/PathSuffix`.</span><span class="sxs-lookup"><span data-stu-id="e9cb7-248">The published endpoint address is of the form `UriScheme://IPAddressOrFQDN:Port/PathSuffix`.</span></span> <span data-ttu-id="e9cb7-249">`UriScheme` и `PathSuffix` являются необязательными атрибутами.</span><span class="sxs-lookup"><span data-stu-id="e9cb7-249">`UriScheme` and `PathSuffix` are optional attributes.</span></span> <span data-ttu-id="e9cb7-250">`IPAddressOrFQDN` — IP-адрес или полное доменное имя узла, на котором размещен исполняемый файл. Значение вычисляется автоматически.</span><span class="sxs-lookup"><span data-stu-id="e9cb7-250">`IPAddressOrFQDN` is the IP address or fully qualified domain name of the node this executable gets placed on, and it is calculated for you.</span></span>

<span data-ttu-id="e9cb7-251">В примере ниже после развертывания службы в Service Fabric Explorer появится конечная точка в формате `http://10.1.4.92:3000/myapp/`, опубликованная для экземпляра службы.</span><span class="sxs-lookup"><span data-stu-id="e9cb7-251">In the following example, once the service is deployed, in Service Fabric Explorer you see an endpoint similar to `http://10.1.4.92:3000/myapp/` published for the service instance.</span></span> <span data-ttu-id="e9cb7-252">Если используется локальный компьютер, она будет в формате `http://localhost:3000/myapp/`.</span><span class="sxs-lookup"><span data-stu-id="e9cb7-252">Or if this is a local machine, you see `http://localhost:3000/myapp/`.</span></span>

```xml
<Endpoints>
   <Endpoint Name="NodeAppTypeEndpoint" Protocol="http" Port="3000"  UriScheme="http" PathSuffix="myapp/" Type="Input" />
</Endpoints>
```
<span data-ttu-id="e9cb7-253">Эти адреса можно использовать для обмена данными между службами через [обратный прокси-сервер](service-fabric-reverseproxy.md) .</span><span class="sxs-lookup"><span data-stu-id="e9cb7-253">You can use these addresses with [reverse proxy](service-fabric-reverseproxy.md) to communicate between services.</span></span>

### <a name="edit-the-application-manifest-file"></a><span data-ttu-id="e9cb7-254">Редактирование файла манифеста приложения</span><span class="sxs-lookup"><span data-stu-id="e9cb7-254">Edit the application manifest file</span></span>
<span data-ttu-id="e9cb7-255">Настроив файл `Servicemanifest.xml`, вам нужно внести в файл `ApplicationManifest.xml` изменения, которые позволят использовать правильные тип и имя службы.</span><span class="sxs-lookup"><span data-stu-id="e9cb7-255">Once you have configured the `Servicemanifest.xml` file, you need to make some changes to the `ApplicationManifest.xml` file to ensure that the correct service type and name are used.</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<ApplicationManifest xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" ApplicationTypeName="NodeAppType" ApplicationTypeVersion="1.0" xmlns="http://schemas.microsoft.com/2011/01/fabric">
   <ServiceManifestImport>
      <ServiceManifestRef ServiceManifestName="NodeApp" ServiceManifestVersion="1.0.0.0" />
   </ServiceManifestImport>
</ApplicationManifest>
```

#### <a name="servicemanifestimport"></a><span data-ttu-id="e9cb7-256">ServiceManifestImport</span><span class="sxs-lookup"><span data-stu-id="e9cb7-256">ServiceManifestImport</span></span>
<span data-ttu-id="e9cb7-257">В элементе `ServiceManifestImport` можно указать одну или несколько служб, которые нужно добавить в приложение.</span><span class="sxs-lookup"><span data-stu-id="e9cb7-257">In the `ServiceManifestImport` element, you can specify one or more services that you want to include in the app.</span></span> <span data-ttu-id="e9cb7-258">Службы указываются в атрибуте `ServiceManifestName` в виде имени каталога, в котором хранится файл `ServiceManifest.xml`.</span><span class="sxs-lookup"><span data-stu-id="e9cb7-258">Services are referenced with `ServiceManifestName`, which specifies the name of the directory where the `ServiceManifest.xml` file is located.</span></span>

```xml
<ServiceManifestImport>
  <ServiceManifestRef ServiceManifestName="NodeApp" ServiceManifestVersion="1.0.0.0" />
</ServiceManifestImport>
```

## <a name="set-up-logging"></a><span data-ttu-id="e9cb7-259">Настройка ведения журнала</span><span class="sxs-lookup"><span data-stu-id="e9cb7-259">Set up logging</span></span>
<span data-ttu-id="e9cb7-260">В журналах консоли можно отслеживать работоспособность гостевых исполняемых файлов. В частности, из этих журналов можно узнать, не возвращают ли сценарии приложения и конфигурации какие-либо ошибки.</span><span class="sxs-lookup"><span data-stu-id="e9cb7-260">For guest executables, it is useful to be able to see console logs to find out if the application and configuration scripts show any errors.</span></span>
<span data-ttu-id="e9cb7-261">Перенаправление консоли можно настроить в файле `ServiceManifest.xml` в элементе `ConsoleRedirection`.</span><span class="sxs-lookup"><span data-stu-id="e9cb7-261">Console redirection can be configured in the `ServiceManifest.xml` file using the `ConsoleRedirection` element.</span></span>

> [!WARNING]
> <span data-ttu-id="e9cb7-262">Никогда не используйте политику перенаправления консоли для приложений в рабочей среде, так как она может повлиять на отработку отказа приложения.</span><span class="sxs-lookup"><span data-stu-id="e9cb7-262">Never use the console redirection policy in an application that is deployed in production because this can affect the application failover.</span></span> <span data-ttu-id="e9cb7-263">Используйте ее *только* для локальной разработки и отладки.</span><span class="sxs-lookup"><span data-stu-id="e9cb7-263">*Only* use this for local development and debugging purposes.</span></span>  
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

<span data-ttu-id="e9cb7-264">`ConsoleRedirection` может использоваться для перенаправления выходных данных консоли (stdout и stderr) в рабочий каталог.</span><span class="sxs-lookup"><span data-stu-id="e9cb7-264">`ConsoleRedirection` can be used to redirect console output (both stdout and stderr) to a working directory.</span></span> <span data-ttu-id="e9cb7-265">Это позволяет проверить, не было ли ошибок во время установки или выполнения приложения в кластере Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="e9cb7-265">This provides the ability to verify that there are no errors during the setup or execution of the application in the Service Fabric cluster.</span></span>

<span data-ttu-id="e9cb7-266">`FileRetentionCount` определяет, сколько файлов будет сохраняться в рабочем каталоге.</span><span class="sxs-lookup"><span data-stu-id="e9cb7-266">`FileRetentionCount` determines how many files are saved in the working directory.</span></span> <span data-ttu-id="e9cb7-267">Например, значение 5 означает, что в рабочем каталоге будут храниться файлы журналов для пяти предыдущих запусков.</span><span class="sxs-lookup"><span data-stu-id="e9cb7-267">A value of 5, for example, means that the log files for the previous five executions are stored in the working directory.</span></span>

<span data-ttu-id="e9cb7-268">`FileMaxSizeInKb` определяет максимальный размер файла журнала.</span><span class="sxs-lookup"><span data-stu-id="e9cb7-268">`FileMaxSizeInKb` specifies the maximum size of the log files.</span></span>

<span data-ttu-id="e9cb7-269">Файлы журналов сохраняются в один из рабочих каталогов службы.</span><span class="sxs-lookup"><span data-stu-id="e9cb7-269">Log files are saved in one of the service's working directories.</span></span> <span data-ttu-id="e9cb7-270">Чтобы определить, где находятся файлы, откройте Service Fabric Explorer и посмотрите, на каком узле запущена служба и какой рабочий каталог используется.</span><span class="sxs-lookup"><span data-stu-id="e9cb7-270">To determine where the files are located, use Service Fabric Explorer to determine which node the service is running on, and which working directory is being used.</span></span> <span data-ttu-id="e9cb7-271">Эта процедура рассмотрена далее в этой статье.</span><span class="sxs-lookup"><span data-stu-id="e9cb7-271">This process is covered later in this article.</span></span>

## <a name="deployment"></a><span data-ttu-id="e9cb7-272">Развертывание</span><span class="sxs-lookup"><span data-stu-id="e9cb7-272">Deployment</span></span>
<span data-ttu-id="e9cb7-273">Последним шагом является [развертывание приложения](service-fabric-deploy-remove-applications.md).</span><span class="sxs-lookup"><span data-stu-id="e9cb7-273">The last step is to [deploy your application](service-fabric-deploy-remove-applications.md).</span></span> <span data-ttu-id="e9cb7-274">В приведенном ниже скрипте PowerShell показано, как можно развернуть приложение в локальном кластере разработки и запустить новую службу Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="e9cb7-274">The following PowerShell script shows how to deploy your application to the local development cluster, and start a new Service Fabric service.</span></span>

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
> <span data-ttu-id="e9cb7-275">[Сожмите пакет](service-fabric-package-apps.md#compress-a-package) перед копированием в хранилище образов, если пакет имеет большой размер или содержит много файлов.</span><span class="sxs-lookup"><span data-stu-id="e9cb7-275">[Compress the package](service-fabric-package-apps.md#compress-a-package) before copying to the image store if the package is large or has many files.</span></span> <span data-ttu-id="e9cb7-276">Дополнительные сведения см. [здесь](service-fabric-deploy-remove-applications.md#upload-the-application-package).</span><span class="sxs-lookup"><span data-stu-id="e9cb7-276">Read more [here](service-fabric-deploy-remove-applications.md#upload-the-application-package).</span></span>
>

<span data-ttu-id="e9cb7-277">Службу Service Fabric можно развертывать в разных конфигурациях.</span><span class="sxs-lookup"><span data-stu-id="e9cb7-277">A Service Fabric service can be deployed in various "configurations."</span></span> <span data-ttu-id="e9cb7-278">Например, службу можно развернуть с одним или несколькими экземплярами. Также можно развернуть по одному экземпляру службы на каждом узле кластера Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="e9cb7-278">For example, it can be deployed as single or multiple instances, or it can be deployed in such a way that there is one instance of the service on each node of the Service Fabric cluster.</span></span>

<span data-ttu-id="e9cb7-279">Параметр `InstanceCount` командлета `New-ServiceFabricService` позволяет указать, сколько экземпляров службы следует запускать в кластере Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="e9cb7-279">The `InstanceCount` parameter of the `New-ServiceFabricService` cmdlet is used to specify how many instances of the service should be launched in the Service Fabric cluster.</span></span> <span data-ttu-id="e9cb7-280">Значение `InstanceCount` следует задавать в зависимости от типа развертываемого приложения.</span><span class="sxs-lookup"><span data-stu-id="e9cb7-280">You can set the `InstanceCount` value, depending on the type of application that you are deploying.</span></span> <span data-ttu-id="e9cb7-281">Ниже приводятся два самых распространенных сценария.</span><span class="sxs-lookup"><span data-stu-id="e9cb7-281">The two most common scenarios are:</span></span>

* <span data-ttu-id="e9cb7-282">`InstanceCount = "1"`.</span><span class="sxs-lookup"><span data-stu-id="e9cb7-282">`InstanceCount = "1"`.</span></span> <span data-ttu-id="e9cb7-283">В этом случае в кластере развертывается только один экземпляр службы.</span><span class="sxs-lookup"><span data-stu-id="e9cb7-283">In this case, only one instance of the service is deployed in the cluster.</span></span> <span data-ttu-id="e9cb7-284">На каком именно узле будет развернута служба, определяет планировщик Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="e9cb7-284">Service Fabric's scheduler determines which node the service is going to be deployed on.</span></span>
* <span data-ttu-id="e9cb7-285">`InstanceCount ="-1"`.</span><span class="sxs-lookup"><span data-stu-id="e9cb7-285">`InstanceCount ="-1"`.</span></span> <span data-ttu-id="e9cb7-286">В этом случае на каждом узле кластера Service Fabric будет развернуто по одному экземпляру службы.</span><span class="sxs-lookup"><span data-stu-id="e9cb7-286">In this case, one instance of the service is deployed on every node in the Service Fabric cluster.</span></span> <span data-ttu-id="e9cb7-287">В результате на каждом узле кластера будет по одному (и только одному) экземпляру службы.</span><span class="sxs-lookup"><span data-stu-id="e9cb7-287">The result is having one (and only one) instance of the service for each node in the cluster.</span></span>

<span data-ttu-id="e9cb7-288">Эта конфигурация подходит для клиентских приложений (например, конечной точки REST), ведь для работы с конечной точкой таким приложениям достаточно подключиться к любому узлу кластера.</span><span class="sxs-lookup"><span data-stu-id="e9cb7-288">This is a useful configuration for front-end applications (for example, a REST endpoint), because client applications need to "connect" to any of the nodes in the cluster to use the endpoint.</span></span> <span data-ttu-id="e9cb7-289">Эту конфигурацию можно использовать и в том случае, если все узлы в кластере Service Fabric подключены к подсистеме балансировки нагрузки.</span><span class="sxs-lookup"><span data-stu-id="e9cb7-289">This configuration can also be used when, for example, all nodes of the Service Fabric cluster are connected to a load balancer.</span></span> <span data-ttu-id="e9cb7-290">Тогда клиентский трафик будет распределяться между экземплярами службы, которые запущены на всех узлах кластера.</span><span class="sxs-lookup"><span data-stu-id="e9cb7-290">Client traffic can then be distributed across the service that is running on all nodes in the cluster.</span></span>

## <a name="check-your-running-application"></a><span data-ttu-id="e9cb7-291">Проверка работающего приложения</span><span class="sxs-lookup"><span data-stu-id="e9cb7-291">Check your running application</span></span>
<span data-ttu-id="e9cb7-292">В обозревателе Service Fabric определите узел, где запущена служба.</span><span class="sxs-lookup"><span data-stu-id="e9cb7-292">In Service Fabric Explorer, identify the node where the service is running.</span></span> <span data-ttu-id="e9cb7-293">В этом примере она выполняется на узле Node1.</span><span class="sxs-lookup"><span data-stu-id="e9cb7-293">In this example, it runs on Node1:</span></span>

![Узел, на котором запущена служба](./media/service-fabric-deploy-existing-app/nodeappinsfx.png)

<span data-ttu-id="e9cb7-295">Если вы перейдете к узлу, а затем к приложению, вы увидите основные сведения об узле, включая его расположение на диске.</span><span class="sxs-lookup"><span data-stu-id="e9cb7-295">If you navigate to the node and browse to the application, you see the essential node information, including its location on disk.</span></span>

![Расположение на диске](./media/service-fabric-deploy-existing-app/locationondisk2.png)

<span data-ttu-id="e9cb7-297">Если перейти в этот каталог в обозревателе сервера, вы увидите рабочий каталог и папку журналов службы, как показано на рисунке ниже.</span><span class="sxs-lookup"><span data-stu-id="e9cb7-297">If you browse to the directory by using Server Explorer, you can find the working directory and the service's log folder, as shown in the following screenshot:</span></span> 

![Расположение журнала](./media/service-fabric-deploy-existing-app/loglocation.png)

## <a name="next-steps"></a><span data-ttu-id="e9cb7-299">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="e9cb7-299">Next steps</span></span>
<span data-ttu-id="e9cb7-300">Из этой статьи вы узнали об основной процедуре упаковки гостевого исполняемого файла и его развертывания в Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="e9cb7-300">In this article, you have learned how to package a guest executable and deploy it to Service Fabric.</span></span> <span data-ttu-id="e9cb7-301">В приведенных ниже статьях описаны связанные сведения и задачи.</span><span class="sxs-lookup"><span data-stu-id="e9cb7-301">See the following articles for related information and tasks.</span></span>

* <span data-ttu-id="e9cb7-302">[Пример для упаковки и развертывания гостевого исполняемого файла](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started), включая ссылку на предварительную версию средства упаковки</span><span class="sxs-lookup"><span data-stu-id="e9cb7-302">[Sample for packaging and deploying a guest executable](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started), including a link to the prerelease of the packaging tool</span></span>
* [<span data-ttu-id="e9cb7-303">Пример двух гостевых исполняемых файлов (C# и Node.js), которые взаимодействуют через службу именования с помощью REST</span><span class="sxs-lookup"><span data-stu-id="e9cb7-303">Sample of two guest executables (C# and nodejs) communicating via the Naming service using REST</span></span>](https://github.com/Azure-Samples/service-fabric-dotnet-containers)
* [<span data-ttu-id="e9cb7-304">Развертывание нескольких пользовательских приложений</span><span class="sxs-lookup"><span data-stu-id="e9cb7-304">Deploy multiple guest executables</span></span>](service-fabric-deploy-multiple-apps.md)
* [<span data-ttu-id="e9cb7-305">Создание первого приложения Service Fabric в Visual Studio</span><span class="sxs-lookup"><span data-stu-id="e9cb7-305">Create your first Service Fabric application using Visual Studio</span></span>](service-fabric-create-your-first-application-in-visual-studio.md)
