---
title: "aaaAzure службы структуры Docker составления Preview"
description: "Azure Service Fabric принимает Docker Compose toomake формат его проще существующие контейнеры tooorchestrate с помощью Service Fabric. Сейчас эта возможность доступна в предварительной версии."
services: service-fabric
documentationcenter: .net
author: mani-ramaswamy
manager: timlt
editor: 
ms.assetid: ab49c4b9-74a8-4907-b75b-8d2ee84c6d90
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/9/2017
ms.author: subramar
ms.openlocfilehash: a60d1321fd6ef07b241a98c5ab2b8dfe5d441b53
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="docker-compose-application-support-in-azure-service-fabric-preview"></a><span data-ttu-id="99f09-104">Поддержка приложения Docker Compose в Azure Service Fabric (предварительная версия)</span><span class="sxs-lookup"><span data-stu-id="99f09-104">Docker Compose application support in Azure Service Fabric (Preview)</span></span>

<span data-ttu-id="99f09-105">Docker использует hello [docker compose.yml](https://docs.docker.com/compose) файла для определения нескольких контейнера приложений.</span><span class="sxs-lookup"><span data-stu-id="99f09-105">Docker uses hello [docker-compose.yml](https://docs.docker.com/compose) file for defining multi-container applications.</span></span> <span data-ttu-id="99f09-106">toomake он просто для пользователей, знакомых с Docker tooorchestrate существующие контейнера приложения в Azure Service Fabric, мы включили поддержку предварительной версии Docker Compose изначально hello платформы.</span><span class="sxs-lookup"><span data-stu-id="99f09-106">toomake it easy for customers familiar with Docker tooorchestrate existing container applications on Azure Service Fabric, we have included preview support for Docker Compose natively in hello platform.</span></span> <span data-ttu-id="99f09-107">Платформа Service Fabric может принять файлы `docker-compose.yml` версии 3 и более поздней.</span><span class="sxs-lookup"><span data-stu-id="99f09-107">Service Fabric can accept version 3 and later of `docker-compose.yml` files.</span></span> 

<span data-ttu-id="99f09-108">Так как эта поддержка доступна в режиме предварительной версии, поддерживается только подмножество директив Compose.</span><span class="sxs-lookup"><span data-stu-id="99f09-108">Because this support is in preview, only a subset of Compose directives is supported.</span></span> <span data-ttu-id="99f09-109">Например, обновления приложений не поддерживаются.</span><span class="sxs-lookup"><span data-stu-id="99f09-109">For example, application upgrades are not supported.</span></span> <span data-ttu-id="99f09-110">Но вы всегда можете вместо обновления приложений удалить и развернуть их.</span><span class="sxs-lookup"><span data-stu-id="99f09-110">However, you can always remove and deploy applications instead of upgrading them.</span></span>

<span data-ttu-id="99f09-111">toouse это предварительного просмотра, создания кластера с версии 5.7 или более среда выполнения Service Fabric hello через портал Azure, наряду с соответствующего пакета SDK для hello hello.</span><span class="sxs-lookup"><span data-stu-id="99f09-111">toouse this preview, create your cluster with version 5.7 or greater of hello Service Fabric runtime through hello Azure portal along with hello corresponding SDK.</span></span> 

> [!NOTE]
> <span data-ttu-id="99f09-112">Эта функция доступна в режиме предварительной версии и не поддерживается в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="99f09-112">This feature is in preview and is not supported in production.</span></span>

## <a name="deploy-a-docker-compose-file-on-service-fabric"></a><span data-ttu-id="99f09-113">Развертывание файла Docker Compose в Service Fabric</span><span class="sxs-lookup"><span data-stu-id="99f09-113">Deploy a Docker Compose file on Service Fabric</span></span>

<span data-ttu-id="99f09-114">Hello следующие команды создают приложения Service Fabric (с именем `fabric:/TestContainerApp` в предшествующих пример hello), которые можно отслеживать и управлять подобно любому другому приложению Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="99f09-114">hello following commands create a Service Fabric application (named `fabric:/TestContainerApp` in hello preceding example), which you can monitor and manage like any other Service Fabric application.</span></span> <span data-ttu-id="99f09-115">Можно использовать имя указанного приложения hello запросов о работоспособности.</span><span class="sxs-lookup"><span data-stu-id="99f09-115">You can use hello specified application name for health queries.</span></span>

### <a name="use-powershell"></a><span data-ttu-id="99f09-116">Использование PowerShell</span><span class="sxs-lookup"><span data-stu-id="99f09-116">Use PowerShell</span></span>

<span data-ttu-id="99f09-117">Создание приложения составления структуры службы из файла docker compose.yml, выполнив следующую команду в PowerShell hello:</span><span class="sxs-lookup"><span data-stu-id="99f09-117">Create a Service Fabric Compose application from a docker-compose.yml file by running hello following command in PowerShell:</span></span>

```powershell
New-ServiceFabricComposeApplication -ApplicationName fabric:/TestContainerApp -Compose docker-compose.yml [-RegistryUserName <>] [-RegistryPassword <>] [-PasswordEncrypted]
```

<span data-ttu-id="99f09-118">`RegistryUserName`и `RegistryPassword` ссылаться toohello контейнер реестра, имя пользователя и пароль.</span><span class="sxs-lookup"><span data-stu-id="99f09-118">`RegistryUserName` and `RegistryPassword` refer toohello container registry username and password.</span></span> <span data-ttu-id="99f09-119">После завершения приложения hello, можно проверить его состояние с помощью hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="99f09-119">After you've completed hello application, you can check its status by using hello following command:</span></span>

```powershell
Get-ServiceFabricComposeApplicationStatus -ApplicationName fabric:/TestContainerApp -GetAllPages
```

<span data-ttu-id="99f09-120">toodelete hello создания приложения с помощью PowerShell, выполните следующую команду hello.</span><span class="sxs-lookup"><span data-stu-id="99f09-120">toodelete hello Compose application through PowerShell, use hello following command:</span></span>

```powershell
Remove-ServiceFabricComposeApplication  -ApplicationName fabric:/TestContainerApp
```

### <a name="use-azure-service-fabric-cli-sfctl"></a><span data-ttu-id="99f09-121">Использование интерфейса командной строки Service Fabric (sfctl)</span><span class="sxs-lookup"><span data-stu-id="99f09-121">Use Azure Service Fabric CLI (sfctl)</span></span>

<span data-ttu-id="99f09-122">Кроме того можно использовать следующую команду для обновления структуры CLI hello:</span><span class="sxs-lookup"><span data-stu-id="99f09-122">Alternatively, you can use hello following Service Fabric CLI command:</span></span>

```azurecli
sfctl compose create --application-id fabric:/TestContainerApp --compose-file docker-compose.yml [ [ --repo-user --repo-pass --encrypted ] | [ --repo-user ] ] [ --timeout ]
```

<span data-ttu-id="99f09-123">После создания приложения hello, можно проверить его состояние с помощью hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="99f09-123">After you've created hello application, you can check its status by using hello following command:</span></span>

```azurecli
sfctl compose status --application-id TestContainerApp [ --timeout ]
```

<span data-ttu-id="99f09-124">hello toodelete создания приложения, используйте hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="99f09-124">toodelete hello Compose application, use hello following command:</span></span>

```azurecli
sfctl compose remove  --application-id TestContainerApp [ --timeout ]
```

## <a name="supported-compose-directives"></a><span data-ttu-id="99f09-125">Поддерживаемые директивы Compose</span><span class="sxs-lookup"><span data-stu-id="99f09-125">Supported Compose directives</span></span>

<span data-ttu-id="99f09-126">Данная Предварительная версия поддерживает подмножество параметров конфигурации hello в формат версии 3 Создание сообщения hello, включая hello следующих примитивов:</span><span class="sxs-lookup"><span data-stu-id="99f09-126">This preview supports a subset of hello configuration options from hello Compose version 3 format, including hello following primitives:</span></span>

* <span data-ttu-id="99f09-127">Services > Deploy > Replicas</span><span class="sxs-lookup"><span data-stu-id="99f09-127">Services > Deploy > Replicas</span></span>
* <span data-ttu-id="99f09-128">Services > Deploy > Placement > Constraints</span><span class="sxs-lookup"><span data-stu-id="99f09-128">Services > Deploy > Placement > Constraints</span></span>
* <span data-ttu-id="99f09-129">Services > Deploy > Resources > Limits</span><span class="sxs-lookup"><span data-stu-id="99f09-129">Services > Deploy > Resources > Limits</span></span>
    * <span data-ttu-id="99f09-130">-cpu-shares</span><span class="sxs-lookup"><span data-stu-id="99f09-130">-cpu-shares</span></span>
    * <span data-ttu-id="99f09-131">-memory</span><span class="sxs-lookup"><span data-stu-id="99f09-131">-memory</span></span>
    * <span data-ttu-id="99f09-132">-memory-swap</span><span class="sxs-lookup"><span data-stu-id="99f09-132">-memory-swap</span></span>
* <span data-ttu-id="99f09-133">Services > Commands</span><span class="sxs-lookup"><span data-stu-id="99f09-133">Services > Commands</span></span>
* <span data-ttu-id="99f09-134">Services > Environment</span><span class="sxs-lookup"><span data-stu-id="99f09-134">Services > Environment</span></span>
* <span data-ttu-id="99f09-135">Services > Ports</span><span class="sxs-lookup"><span data-stu-id="99f09-135">Services > Ports</span></span>
* <span data-ttu-id="99f09-136">Services > Image</span><span class="sxs-lookup"><span data-stu-id="99f09-136">Services > Image</span></span>
* <span data-ttu-id="99f09-137">Services > Isolation (только для Windows)</span><span class="sxs-lookup"><span data-stu-id="99f09-137">Services > Isolation (only for Windows)</span></span>
* <span data-ttu-id="99f09-138">Services > Logging > Driver</span><span class="sxs-lookup"><span data-stu-id="99f09-138">Services > Logging > Driver</span></span>
* <span data-ttu-id="99f09-139">Services > Logging > Driver > Options</span><span class="sxs-lookup"><span data-stu-id="99f09-139">Services > Logging > Driver > Options</span></span>
* <span data-ttu-id="99f09-140">Volume & Deploy > Volume</span><span class="sxs-lookup"><span data-stu-id="99f09-140">Volume & Deploy > Volume</span></span>

<span data-ttu-id="99f09-141">Настройка кластера hello для принудительного применения ограничения ресурсов, как описано в [ресурсами Service Fabric](service-fabric-resource-governance.md).</span><span class="sxs-lookup"><span data-stu-id="99f09-141">Set up hello cluster for enforcing resource limits, as described in [Service Fabric resource governance](service-fabric-resource-governance.md).</span></span> <span data-ttu-id="99f09-142">Другие директивы Docker Compose не поддерживаются в этой предварительной версии.</span><span class="sxs-lookup"><span data-stu-id="99f09-142">All other Docker Compose directives are unsupported for this preview.</span></span>

## <a name="servicednsname-computation"></a><span data-ttu-id="99f09-143">Вычисление ServiceDnsName</span><span class="sxs-lookup"><span data-stu-id="99f09-143">ServiceDnsName computation</span></span>

<span data-ttu-id="99f09-144">Если задать в файле составление имя службы hello представляет полное доменное имя (то есть, он содержит точкой [.]), DNS-имя hello, зарегистрированные с помощью Service Fabric `<ServiceName>` (включая точку hello).</span><span class="sxs-lookup"><span data-stu-id="99f09-144">If hello service name that you specify in a Compose file is a fully qualified domain name (that is, it contains a dot [.]), hello DNS name registered by Service Fabric is `<ServiceName>` (including hello dot).</span></span> <span data-ttu-id="99f09-145">В противном случае каждый сегмент пути в имени приложения hello становится метка домена в hello DNS-имя службы, с hello становится метка домена верхнего уровня hello первый сегмент пути.</span><span class="sxs-lookup"><span data-stu-id="99f09-145">If not, each path segment in hello application name becomes a domain label in hello service DNS name, with hello first path segment becoming hello top-level domain label.</span></span>

<span data-ttu-id="99f09-146">Например, если hello указано имя приложения — `fabric:/SampleApp/MyComposeApp`, `<ServiceName>.MyComposeApp.SampleApp` бы hello зарегистрированное имя DNS.</span><span class="sxs-lookup"><span data-stu-id="99f09-146">For example, if hello specified application name is `fabric:/SampleApp/MyComposeApp`, `<ServiceName>.MyComposeApp.SampleApp` would be hello registered DNS name.</span></span>

## <a name="differences-between-compose-instance-definition-and-service-fabric-application-model-type-definition"></a><span data-ttu-id="99f09-147">Различия между моделью приложений Compose (определение экземпляра) и Service Fabric (определение типа)</span><span class="sxs-lookup"><span data-stu-id="99f09-147">Differences between Compose (instance definition) and Service Fabric application model (type definition)</span></span>

<span data-ttu-id="99f09-148">Файл docker-compose.yml описывает набор контейнеров, доступных для развертывания, в том числе их свойства и конфигурации.</span><span class="sxs-lookup"><span data-stu-id="99f09-148">A docker-compose.yml file describes a deployable set of containers, including their properties and configurations.</span></span>
<span data-ttu-id="99f09-149">Например файл hello может содержать переменные среды и порты.</span><span class="sxs-lookup"><span data-stu-id="99f09-149">For example, hello file can contain environment variables and ports.</span></span> <span data-ttu-id="99f09-150">Также можно указать параметры развертывания, например ограничения размещения, ограничения ресурсов и DNS-имен в файле docker compose.yml hello.</span><span class="sxs-lookup"><span data-stu-id="99f09-150">You can also specify deployment parameters, such as placement constraints, resource limits, and DNS names, in hello docker-compose.yml file.</span></span>

<span data-ttu-id="99f09-151">Hello [модель приложения Service Fabric](service-fabric-application-model.md) службы использует типы и типы приложений, где можно иметь несколько экземпляров приложения hello того же типа.</span><span class="sxs-lookup"><span data-stu-id="99f09-151">hello [Service Fabric application model](service-fabric-application-model.md) uses service types and application types, where you can have many application instances of hello same type.</span></span> <span data-ttu-id="99f09-152">Например, можно создать по одному экземпляру приложения на клиента.</span><span class="sxs-lookup"><span data-stu-id="99f09-152">For example, you can have one application instance per customer.</span></span> <span data-ttu-id="99f09-153">Эта модель на основе типа поддерживает несколько версий hello одного типа приложения, который регистрируется с помощью среды выполнения hello.</span><span class="sxs-lookup"><span data-stu-id="99f09-153">This type-based model supports multiple versions of hello same application type that's registered with hello runtime.</span></span>

<span data-ttu-id="99f09-154">Например, клиента объект может быть создан с типом 1.0 AppTypeA приложения, а клиент Б может иметь другое приложение, экземпляр которого создается без hello того же типа и версии.</span><span class="sxs-lookup"><span data-stu-id="99f09-154">For example, customer A can have an application instantiated with type 1.0 of AppTypeA, and customer B can have another application instantiated with hello same type and version.</span></span> <span data-ttu-id="99f09-155">Определения типов приложений hello в манифестах приложения hello и укажите имя и развертывания параметров приложения hello, при создании приложения hello.</span><span class="sxs-lookup"><span data-stu-id="99f09-155">You define hello application types in hello application manifests, and you specify hello application name and deployment parameters when you create hello application.</span></span>

<span data-ttu-id="99f09-156">Несмотря на то, что эта модель обеспечивает гибкость, мы также планируете toosupport модель развертывания проще, основанного на экземпляре, где типы являются неявными из файла манифеста hello.</span><span class="sxs-lookup"><span data-stu-id="99f09-156">Although this model offers flexibility, we are also planning toosupport a simpler, instance-based deployment model where types are implicit from hello manifest file.</span></span> <span data-ttu-id="99f09-157">В этой модели каждое приложение получает собственный независимый манифест.</span><span class="sxs-lookup"><span data-stu-id="99f09-157">In this model, each application gets its own independent manifest.</span></span> <span data-ttu-id="99f09-158">Мы предварительно рассматриваем это действие, добавляя поддержку docker-compose.yml, в котором используется формат развертывания на основе экземпляра.</span><span class="sxs-lookup"><span data-stu-id="99f09-158">We are previewing this effort by adding support for docker-compose.yml, which is an instance-based deployment format.</span></span>

## <a name="next-steps"></a><span data-ttu-id="99f09-159">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="99f09-159">Next steps</span></span>

* <span data-ttu-id="99f09-160">Ознакомьтесь со статьей hello [модели приложения Service Fabric](service-fabric-application-model.md)</span><span class="sxs-lookup"><span data-stu-id="99f09-160">Read up on hello [Service Fabric application model](service-fabric-application-model.md)</span></span>
* <span data-ttu-id="99f09-161">[Azure Service Fabric command line](service-fabric-cli.md) (Интерфейс командной строки Azure Service Fabric)</span><span class="sxs-lookup"><span data-stu-id="99f09-161">[Get started with Service Fabric CLI](service-fabric-cli.md)</span></span>
