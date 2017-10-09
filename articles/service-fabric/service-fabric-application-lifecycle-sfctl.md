---
title: "приложения Azure Service Fabric aaaManage, использующие Azure Service Fabric CLI"
description: "Узнайте, как toodeploy и удаление приложений с Azure Service Fabric кластера с помощью Azure Service Fabric CLI"
services: service-fabric
author: samedder
manager: timlt
ms.service: service-fabric
ms.topic: article
ms.date: 08/22/2017
ms.author: edwardsa
ms.openlocfilehash: d9f98cee1d70f71a2aab68ff556956619910e4fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="manage-an-azure-service-fabric-application-by-using-azure-service-fabric-cli"></a><span data-ttu-id="170f6-103">Управление приложением Azure Service Fabric с помощью интерфейса командной строки Azure Service Fabric</span><span class="sxs-lookup"><span data-stu-id="170f6-103">Manage an Azure Service Fabric application by using Azure Service Fabric CLI</span></span>

<span data-ttu-id="170f6-104">Узнайте, как toocreate и удаление приложений, работающих в кластере Azure Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="170f6-104">Learn how toocreate and delete applications that are running in an Azure Service Fabric cluster.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="170f6-105">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="170f6-105">Prerequisites</span></span>

* <span data-ttu-id="170f6-106">Установите интерфейс командной строки Service Fabric</span><span class="sxs-lookup"><span data-stu-id="170f6-106">Install Service Fabric CLI.</span></span> <span data-ttu-id="170f6-107">и выберите кластер Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="170f6-107">Then, select your Service Fabric cluster.</span></span> <span data-ttu-id="170f6-108">Дополнительные сведения см. в статье [Azure Service Fabric command line](service-fabric-cli.md) (Интерфейс командной строки Azure Service Fabric).</span><span class="sxs-lookup"><span data-stu-id="170f6-108">For more information, see [Get started with Service Fabric CLI](service-fabric-cli.md).</span></span>

* <span data-ttu-id="170f6-109">У Service Fabric приложения пакет готов toobe развертывания.</span><span class="sxs-lookup"><span data-stu-id="170f6-109">Have a Service Fabric application package ready toobe deployed.</span></span> <span data-ttu-id="170f6-110">Дополнительные сведения о том, как tooauthor и пакет приложения, узнайте, как hello [модель приложения Service Fabric](service-fabric-application-model.md).</span><span class="sxs-lookup"><span data-stu-id="170f6-110">For more information about how tooauthor and package an application, read about hello [Service Fabric application model](service-fabric-application-model.md).</span></span>

## <a name="overview"></a><span data-ttu-id="170f6-111">Обзор</span><span class="sxs-lookup"><span data-stu-id="170f6-111">Overview</span></span>

<span data-ttu-id="170f6-112">toodeploy нового приложения, выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="170f6-112">toodeploy a new application, complete these steps:</span></span>

1. <span data-ttu-id="170f6-113">Отправка образа хранилища Service Fabric toohello пакета приложений.</span><span class="sxs-lookup"><span data-stu-id="170f6-113">Upload an application package toohello Service Fabric image store.</span></span>
2. <span data-ttu-id="170f6-114">Подготовьте тип приложения.</span><span class="sxs-lookup"><span data-stu-id="170f6-114">Provision an application type.</span></span>
3. <span data-ttu-id="170f6-115">Укажите приложение и создайте его.</span><span class="sxs-lookup"><span data-stu-id="170f6-115">Specify and create an application.</span></span>
4. <span data-ttu-id="170f6-116">Укажите службы и создайте их.</span><span class="sxs-lookup"><span data-stu-id="170f6-116">Specify and create services.</span></span>

<span data-ttu-id="170f6-117">tooremove существующего приложения, выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="170f6-117">tooremove an existing application, complete these steps:</span></span>

1. <span data-ttu-id="170f6-118">Удаление приложения hello.</span><span class="sxs-lookup"><span data-stu-id="170f6-118">Delete hello application.</span></span>
2. <span data-ttu-id="170f6-119">Отключение hello связанный тип приложения.</span><span class="sxs-lookup"><span data-stu-id="170f6-119">Unprovision hello associated application type.</span></span>
3. <span data-ttu-id="170f6-120">Удаляет содержимое хранилища hello изображения.</span><span class="sxs-lookup"><span data-stu-id="170f6-120">Delete hello image store content.</span></span>

## <a name="deploy-a-new-application"></a><span data-ttu-id="170f6-121">Развертывание нового приложения</span><span class="sxs-lookup"><span data-stu-id="170f6-121">Deploy a new application</span></span>

<span data-ttu-id="170f6-122">toodeploy нового приложения, завершения hello следующие задачи:</span><span class="sxs-lookup"><span data-stu-id="170f6-122">toodeploy a new application, complete hello following tasks:</span></span>

### <a name="upload-a-new-application-package-toohello-image-store"></a><span data-ttu-id="170f6-123">Отправить новый образ хранилище toohello приложения пакета</span><span class="sxs-lookup"><span data-stu-id="170f6-123">Upload a new application package toohello image store</span></span>

<span data-ttu-id="170f6-124">Прежде чем создавать приложения, отправьте изображение хранилище Service Fabric toohello hello приложения пакета.</span><span class="sxs-lookup"><span data-stu-id="170f6-124">Before you create an application, upload hello application package toohello Service Fabric image store.</span></span>

<span data-ttu-id="170f6-125">Например, если пакет приложения hello `app_package_dir` directory hello используйте следующие команды tooupload hello каталога:</span><span class="sxs-lookup"><span data-stu-id="170f6-125">For example, if your application package is in hello `app_package_dir` directory, use hello following commands tooupload hello directory:</span></span>

```azurecli
sfctl application upload --path ~/app_package_dir
```

<span data-ttu-id="170f6-126">Для больших пакетов приложений, вы можете указать hello `--show-progress` параметр toodisplay hello ход выполнения передачи hello.</span><span class="sxs-lookup"><span data-stu-id="170f6-126">For large application packages, you can specify hello `--show-progress` option toodisplay hello progress of hello upload.</span></span>

### <a name="provision-hello-application-type"></a><span data-ttu-id="170f6-127">Тип приложения hello подготовки</span><span class="sxs-lookup"><span data-stu-id="170f6-127">Provision hello application type</span></span>

<span data-ttu-id="170f6-128">После завершения передачи hello подготовить приложение hello.</span><span class="sxs-lookup"><span data-stu-id="170f6-128">When hello upload is finished, provision hello application.</span></span> <span data-ttu-id="170f6-129">приложение hello tooprovision, hello используйте следующую команду:</span><span class="sxs-lookup"><span data-stu-id="170f6-129">tooprovision hello application, use hello following command:</span></span>

```azurecli
sfctl application provision --application-type-build-path app_package_dir
```

<span data-ttu-id="170f6-130">Здравствуйте, значение для `application-type-build-path` — имя hello hello каталога, где загруженный пакет приложения.</span><span class="sxs-lookup"><span data-stu-id="170f6-130">hello value for `application-type-build-path` is hello name of hello directory where you uploaded your application package.</span></span>

### <a name="create-an-application-from-an-application-type"></a><span data-ttu-id="170f6-131">Создание приложения из типа приложения</span><span class="sxs-lookup"><span data-stu-id="170f6-131">Create an application from an application type</span></span>

<span data-ttu-id="170f6-132">После их инициализации приложения hello, используйте следующие команды tooname hello и создания приложения:</span><span class="sxs-lookup"><span data-stu-id="170f6-132">After you provision hello application, use hello following command tooname and create your application:</span></span>

```azurecli
sfctl application create --app-name fabric:/TestApp --app-type TestAppType --app-version 1.0
```

<span data-ttu-id="170f6-133">`app-name`— Имя hello, что требуется toouse для экземпляра приложения hello.</span><span class="sxs-lookup"><span data-stu-id="170f6-133">`app-name` is hello name that you want toouse for hello application instance.</span></span> <span data-ttu-id="170f6-134">Другие параметры можно найти с помощью манифеста приложения, который был подготовлен ранее.</span><span class="sxs-lookup"><span data-stu-id="170f6-134">You can get additional parameters from the previously provisioned application manifest.</span></span>

<span data-ttu-id="170f6-135">Имя приложения Hello должно начинаться с префикса hello `fabric:/`.</span><span class="sxs-lookup"><span data-stu-id="170f6-135">hello application name must start with hello prefix `fabric:/`.</span></span>

### <a name="create-services-for-hello-new-application"></a><span data-ttu-id="170f6-136">Создание служб для нового приложения hello</span><span class="sxs-lookup"><span data-stu-id="170f6-136">Create services for hello new application</span></span>

<span data-ttu-id="170f6-137">После создания приложения можно создайте службы из приложения hello.</span><span class="sxs-lookup"><span data-stu-id="170f6-137">After you have created an application, create services from hello application.</span></span> <span data-ttu-id="170f6-138">В следующем примере hello создадим новый без отслеживания состояния службы из нашего приложения.</span><span class="sxs-lookup"><span data-stu-id="170f6-138">In hello following example, we create a new stateless service from our application.</span></span> <span data-ttu-id="170f6-139">Hello служб, которые можно создать из приложения, определенные в манифест службы в пакет предварительно подготовленные приложения hello.</span><span class="sxs-lookup"><span data-stu-id="170f6-139">hello services that you can create from an application are defined in a service manifest in hello previously provisioned application package.</span></span>

```azurecli
sfctl service create --app-id TestApp --name fabric:/TestApp/TestSvc --service-type TestServiceType \
--stateless --instance-count 1 --singleton-scheme
```

## <a name="verify-application-deployment-and-health"></a><span data-ttu-id="170f6-140">Проверка развертывания и работоспособности приложения</span><span class="sxs-lookup"><span data-stu-id="170f6-140">Verify application deployment and health</span></span>

<span data-ttu-id="170f6-141">tooverify все, что находится в работоспособном состоянии, выполните следующие команды работоспособности hello.</span><span class="sxs-lookup"><span data-stu-id="170f6-141">tooverify everything is healthy, use hello following health commands:</span></span>

```azurecli
sfctl application list
sfctl service list --application-id TestApp
```

<span data-ttu-id="170f6-142">tooverify, что служба hello находится в работоспособном состоянии, используйте аналогичные команды tooretrieve hello работоспособности hello службы и приложения:</span><span class="sxs-lookup"><span data-stu-id="170f6-142">tooverify that hello service is healthy, use similar commands tooretrieve hello health of both hello service and the application:</span></span>

```azurecli
sfctl application health --application-id TestApp
sfctl service health --service-id TestApp/TestSvc
```

<span data-ttu-id="170f6-143">Параметр `HealthState` работоспособных служб и приложений должен иметь значение `Ok`.</span><span class="sxs-lookup"><span data-stu-id="170f6-143">Healthy services and applications have a `HealthState` value of `Ok`.</span></span>

## <a name="remove-an-existing-application"></a><span data-ttu-id="170f6-144">Удаление имеющегося приложения</span><span class="sxs-lookup"><span data-stu-id="170f6-144">Remove an existing application</span></span>

<span data-ttu-id="170f6-145">tooremove приложения, завершения hello следующие задачи:</span><span class="sxs-lookup"><span data-stu-id="170f6-145">tooremove an application, complete hello following tasks:</span></span>

### <a name="delete-hello-application"></a><span data-ttu-id="170f6-146">Удаление приложения hello</span><span class="sxs-lookup"><span data-stu-id="170f6-146">Delete hello application</span></span>

<span data-ttu-id="170f6-147">приложение hello toodelete, hello используйте следующую команду:</span><span class="sxs-lookup"><span data-stu-id="170f6-147">toodelete hello application, use hello following command:</span></span>

```azurecli
sfctl application delete --application-id TestEdApp
```

### <a name="unprovision-hello-application-type"></a><span data-ttu-id="170f6-148">Отменить подготовку типа приложения hello</span><span class="sxs-lookup"><span data-stu-id="170f6-148">Unprovision hello application type</span></span>

<span data-ttu-id="170f6-149">После удаления приложения hello, можно отменить подготовку типа приложения hello, если оно больше не требуется.</span><span class="sxs-lookup"><span data-stu-id="170f6-149">After you delete hello application, you can unprovision hello application type if you no longer need it.</span></span> <span data-ttu-id="170f6-150">Тип приложения hello toounprovision, hello используйте следующую команду:</span><span class="sxs-lookup"><span data-stu-id="170f6-150">toounprovision hello application type, use hello following command:</span></span>

```azurecli
sfctl application unprovision --application-type-name TestAppTye --application-type-version 1.0
```

<span data-ttu-id="170f6-151">версия по имени и типа тип Hello должна соответствовать hello имени и версии в манифесте предварительно подготовленные приложения hello.</span><span class="sxs-lookup"><span data-stu-id="170f6-151">hello type name and type version must match hello name and version in hello previously provisioned application manifest.</span></span>

### <a name="delete-hello-application-package"></a><span data-ttu-id="170f6-152">Удалить пакет приложения hello</span><span class="sxs-lookup"><span data-stu-id="170f6-152">Delete hello application package</span></span>

<span data-ttu-id="170f6-153">После отменил инициализацию типа приложения hello, можно удалить пакет приложения hello из хранилища образов hello, если оно больше не требуется.</span><span class="sxs-lookup"><span data-stu-id="170f6-153">After you have unprovisioned hello application type, you can delete hello application package from hello image store if you no longer need it.</span></span> <span data-ttu-id="170f6-154">Удалите пакеты приложения, чтобы освободить место на диске.</span><span class="sxs-lookup"><span data-stu-id="170f6-154">Deleting application packages helps reclaim disk space.</span></span> 

<span data-ttu-id="170f6-155">пакет приложения hello toodelete из хранилища образов hello, hello используйте следующую команду:</span><span class="sxs-lookup"><span data-stu-id="170f6-155">toodelete hello application package from hello image store, use hello following command:</span></span>

```azurecli
sfctl store delete --content-path app_package_dir
```

<span data-ttu-id="170f6-156">`content-path`должно быть именем hello hello каталога, который загружен при создании приложения hello.</span><span class="sxs-lookup"><span data-stu-id="170f6-156">`content-path` must be hello name of hello directory that you uploaded when you created hello application.</span></span>

## <a name="upgrade-application"></a><span data-ttu-id="170f6-157">Обновление приложения</span><span class="sxs-lookup"><span data-stu-id="170f6-157">Upgrade application</span></span>

<span data-ttu-id="170f6-158">После создания приложения, можно повторить hello одинаковый набор шагов tooprovision второй версии приложения.</span><span class="sxs-lookup"><span data-stu-id="170f6-158">After creating your application, you can repeat hello same set of steps tooprovision a second version of your application.</span></span> <span data-ttu-id="170f6-159">После этого обновления приложения Service Fabric может перевести toorunning hello вторая версия приложения hello.</span><span class="sxs-lookup"><span data-stu-id="170f6-159">Then, with a Service Fabric application upgrade you can transition toorunning hello second version of hello application.</span></span> <span data-ttu-id="170f6-160">Дополнительные сведения см. в разделе документации hello на [обновления приложения Service Fabric](service-fabric-application-upgrade.md).</span><span class="sxs-lookup"><span data-stu-id="170f6-160">For more information, see hello documentation on [Service Fabric application upgrades](service-fabric-application-upgrade.md).</span></span>

<span data-ttu-id="170f6-161">tooperform обновления первого подготовки hello следующей версии приложения с помощью hello как раньше hello же команды:</span><span class="sxs-lookup"><span data-stu-id="170f6-161">tooperform an upgrade, first provision hello next version of hello application using hello same commands as before:</span></span>

```azurecli
sfctl application upload --path ~/app_package_dir_2
sfctl application provision --application-type-build-path app_package_dir_2
```

<span data-ttu-id="170f6-162">Рекомендации и tooperform отслеживаемых автоматического обновления, запустите обновление hello, выполнив следующую команду hello:</span><span class="sxs-lookup"><span data-stu-id="170f6-162">It is recommended then tooperform a monitored automatic upgrade, launch hello upgrade by running hello following command:</span></span>

```azurecli
sfctl application upgrade --app-id TestApp --app-version 2.0.0 --parameters "{\"test\":\"value\"}" --mode Monitored
```

<span data-ttu-id="170f6-163">Обновления переопределяют существующие параметры вне зависимости от способа их задания.</span><span class="sxs-lookup"><span data-stu-id="170f6-163">Upgrades override existing parameters with whatever set is specified.</span></span> <span data-ttu-id="170f6-164">Параметры приложения должен передаваться как аргументы команды обновления toohello, при необходимости.</span><span class="sxs-lookup"><span data-stu-id="170f6-164">Application parameters should be passed as arguments toohello upgrade command, if necessary.</span></span> <span data-ttu-id="170f6-165">Параметры приложения должны быть закодированы в виде объекта JSON.</span><span class="sxs-lookup"><span data-stu-id="170f6-165">Application parameters should be encoded as a JSON object.</span></span>

<span data-ttu-id="170f6-166">указанные параметры tooretrieve, вы можете использовать hello `sfctl application info` команды.</span><span class="sxs-lookup"><span data-stu-id="170f6-166">tooretrieve any parameters previously specified, you can use hello `sfctl application info` command.</span></span>

<span data-ttu-id="170f6-167">Если выполняется обновление приложения, hello состояние может быть получен с помощью `sfctl application upgrade-status` команды.</span><span class="sxs-lookup"><span data-stu-id="170f6-167">When an application upgrade is in progress, hello status can be retrieved using the `sfctl application upgrade-status` command.</span></span>

<span data-ttu-id="170f6-168">Наконец, если обновление выполняется и должен toobe отменено, можно использовать hello `sfctl application upgrade-rollback` tooroll обратно hello обновления.</span><span class="sxs-lookup"><span data-stu-id="170f6-168">Finally, if an upgrade is in progress and needs toobe canceled, you can use hello `sfctl application upgrade-rollback` tooroll back hello upgrade.</span></span>

## <a name="next-steps"></a><span data-ttu-id="170f6-169">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="170f6-169">Next steps</span></span>

* <span data-ttu-id="170f6-170">[Azure Service Fabric command line](service-fabric-cli.md) (Командная строка Azure Service Fabric)</span><span class="sxs-lookup"><span data-stu-id="170f6-170">[Service Fabric CLI basics](service-fabric-cli.md)</span></span>
* [<span data-ttu-id="170f6-171">Подготовка среды разработки в Linux</span><span class="sxs-lookup"><span data-stu-id="170f6-171">Getting started with Service Fabric on Linux</span></span>](service-fabric-get-started-linux.md)
* [<span data-ttu-id="170f6-172">Обновление приложения Service Fabric</span><span class="sxs-lookup"><span data-stu-id="170f6-172">Launching a Service Fabric application upgrade</span></span>](service-fabric-application-upgrade.md)
