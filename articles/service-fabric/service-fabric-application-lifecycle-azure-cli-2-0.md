---
title: "приложения Azure Service Fabric aaaManage, с помощью Azure CLI 2.0"
description: "Узнайте, как toodeploy и удаление приложений с Azure Service Fabric кластера с помощью Azure CLI 2.0."
services: service-fabric
author: samedder
manager: timlt
ms.service: service-fabric
ms.topic: article
ms.date: 06/21/2017
ms.author: edwardsa
ms.openlocfilehash: ae1ba19513978b0f95ffb65d5f1f7a21ed5f2894
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="manage-an-azure-service-fabric-application-by-using-azure-cli-20"></a><span data-ttu-id="d22ae-103">Управление приложением Azure Service Fabric с помощью Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="d22ae-103">Manage an Azure Service Fabric application by using Azure CLI 2.0</span></span>

<span data-ttu-id="d22ae-104">Узнайте, как toocreate и удаление приложений, работающих в кластере Azure Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="d22ae-104">Learn how toocreate and delete applications that are running in an Azure Service Fabric cluster.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d22ae-105">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="d22ae-105">Prerequisites</span></span>

* <span data-ttu-id="d22ae-106">Установите Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="d22ae-106">Install Azure CLI 2.0.</span></span> <span data-ttu-id="d22ae-107">и выберите кластер Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="d22ae-107">Then, select your Service Fabric cluster.</span></span> <span data-ttu-id="d22ae-108">Дополнительные сведения можно найти в документации по [началу работы с Azure CLI 2.0](service-fabric-azure-cli-2-0.md).</span><span class="sxs-lookup"><span data-stu-id="d22ae-108">For more information, see [Get started with Azure CLI 2.0](service-fabric-azure-cli-2-0.md).</span></span>

* <span data-ttu-id="d22ae-109">У Service Fabric приложения пакет готов toobe развертывания.</span><span class="sxs-lookup"><span data-stu-id="d22ae-109">Have a Service Fabric application package ready toobe deployed.</span></span> <span data-ttu-id="d22ae-110">Дополнительные сведения о том, как tooauthor и пакет приложения, узнайте, как hello [модель приложения Service Fabric](service-fabric-application-model.md).</span><span class="sxs-lookup"><span data-stu-id="d22ae-110">For more information about how tooauthor and package an application, read about hello [Service Fabric application model](service-fabric-application-model.md).</span></span>

## <a name="overview"></a><span data-ttu-id="d22ae-111">Обзор</span><span class="sxs-lookup"><span data-stu-id="d22ae-111">Overview</span></span>

<span data-ttu-id="d22ae-112">toodeploy нового приложения, выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="d22ae-112">toodeploy a new application, complete these steps:</span></span>

1. <span data-ttu-id="d22ae-113">Отправка образа хранилища Service Fabric toohello пакета приложений.</span><span class="sxs-lookup"><span data-stu-id="d22ae-113">Upload an application package toohello Service Fabric image store.</span></span>
2. <span data-ttu-id="d22ae-114">Подготовьте тип приложения.</span><span class="sxs-lookup"><span data-stu-id="d22ae-114">Provision an application type.</span></span>
3. <span data-ttu-id="d22ae-115">Укажите приложение и создайте его.</span><span class="sxs-lookup"><span data-stu-id="d22ae-115">Specify and create an application.</span></span>
4. <span data-ttu-id="d22ae-116">Укажите службы и создайте их.</span><span class="sxs-lookup"><span data-stu-id="d22ae-116">Specify and create services.</span></span>

<span data-ttu-id="d22ae-117">tooremove существующего приложения, выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="d22ae-117">tooremove an existing application, complete these steps:</span></span>

1. <span data-ttu-id="d22ae-118">Удаление приложения hello.</span><span class="sxs-lookup"><span data-stu-id="d22ae-118">Delete hello application.</span></span>
2. <span data-ttu-id="d22ae-119">Отключение hello связанный тип приложения.</span><span class="sxs-lookup"><span data-stu-id="d22ae-119">Unprovision hello associated application type.</span></span>
3. <span data-ttu-id="d22ae-120">Удаляет содержимое хранилища hello изображения.</span><span class="sxs-lookup"><span data-stu-id="d22ae-120">Delete hello image store content.</span></span>

## <a name="deploy-a-new-application"></a><span data-ttu-id="d22ae-121">Развертывание нового приложения</span><span class="sxs-lookup"><span data-stu-id="d22ae-121">Deploy a new application</span></span>

<span data-ttu-id="d22ae-122">toodeploy нового приложения, завершения hello следующие задачи.</span><span class="sxs-lookup"><span data-stu-id="d22ae-122">toodeploy a new application, complete hello following tasks.</span></span>

### <a name="upload-a-new-application-package-toohello-image-store"></a><span data-ttu-id="d22ae-123">Отправить новый образ хранилище toohello приложения пакета</span><span class="sxs-lookup"><span data-stu-id="d22ae-123">Upload a new application package toohello image store</span></span>

<span data-ttu-id="d22ae-124">Прежде чем создавать приложения, отправьте изображение хранилище Service Fabric toohello hello приложения пакета.</span><span class="sxs-lookup"><span data-stu-id="d22ae-124">Before you create an application, upload hello application package toohello Service Fabric image store.</span></span> 

<span data-ttu-id="d22ae-125">Например, если пакет приложения hello `app_package_dir` directory hello используйте следующие команды tooupload hello каталога:</span><span class="sxs-lookup"><span data-stu-id="d22ae-125">For example, if your application package is in hello `app_package_dir` directory, use hello following commands tooupload hello directory:</span></span>

```azurecli
az sf application upload --path ~/app_package_dir
```

<span data-ttu-id="d22ae-126">Для больших пакетов приложений, вы можете указать hello `--show-progress` параметр toodisplay hello ход выполнения передачи hello.</span><span class="sxs-lookup"><span data-stu-id="d22ae-126">For large application packages, you can specify hello `--show-progress` option toodisplay hello progress of hello upload.</span></span>

### <a name="provision-hello-application-type"></a><span data-ttu-id="d22ae-127">Тип приложения hello подготовки</span><span class="sxs-lookup"><span data-stu-id="d22ae-127">Provision hello application type</span></span>

<span data-ttu-id="d22ae-128">После завершения передачи hello подготовить приложение hello.</span><span class="sxs-lookup"><span data-stu-id="d22ae-128">When hello upload is finished, provision hello application.</span></span> <span data-ttu-id="d22ae-129">приложение hello tooprovision, hello используйте следующую команду:</span><span class="sxs-lookup"><span data-stu-id="d22ae-129">tooprovision hello application, use hello following command:</span></span>

```azurecli
az sf application provision --application-type-build-path app_package_dir
```

<span data-ttu-id="d22ae-130">Здравствуйте, значение для `application-type-build-path` — имя hello hello каталога, где загруженный пакет приложения.</span><span class="sxs-lookup"><span data-stu-id="d22ae-130">hello value for `application-type-build-path` is hello name of hello directory where you uploaded your application package.</span></span>

### <a name="create-an-application-from-an-application-type"></a><span data-ttu-id="d22ae-131">Создание приложения из типа приложения</span><span class="sxs-lookup"><span data-stu-id="d22ae-131">Create an application from an application type</span></span>

<span data-ttu-id="d22ae-132">После их инициализации приложения hello, используйте следующие команды tooname hello и создания приложения:</span><span class="sxs-lookup"><span data-stu-id="d22ae-132">After you provision hello application, use hello following command tooname and create your application:</span></span>

```azurecli
az sf application create --app-name fabric:/TestApp --app-type TestAppType --app-version 1.0
```

<span data-ttu-id="d22ae-133">`app-name`— Имя hello, что требуется toouse для экземпляра приложения hello.</span><span class="sxs-lookup"><span data-stu-id="d22ae-133">`app-name` is hello name that you want toouse for hello application instance.</span></span> <span data-ttu-id="d22ae-134">Дополнительные параметры можно получить из манифеста предварительно подготовленные приложения hello.</span><span class="sxs-lookup"><span data-stu-id="d22ae-134">You can get additional parameters from hello previously provisioned application manifest.</span></span>

<span data-ttu-id="d22ae-135">Имя приложения Hello должно начинаться с префикса hello `fabric:/`.</span><span class="sxs-lookup"><span data-stu-id="d22ae-135">hello application name must start with hello prefix `fabric:/`.</span></span>

### <a name="create-services-for-hello-new-application"></a><span data-ttu-id="d22ae-136">Создание служб для нового приложения hello</span><span class="sxs-lookup"><span data-stu-id="d22ae-136">Create services for hello new application</span></span>

<span data-ttu-id="d22ae-137">После создания приложения можно создайте службы из приложения hello.</span><span class="sxs-lookup"><span data-stu-id="d22ae-137">After you have created an application, create services from hello application.</span></span> <span data-ttu-id="d22ae-138">В следующем примере hello создадим новый без отслеживания состояния службы из нашего приложения.</span><span class="sxs-lookup"><span data-stu-id="d22ae-138">In hello following example, we create a new stateless service from our application.</span></span> <span data-ttu-id="d22ae-139">Hello служб, которые можно создать из приложения, определенные в манифест службы в пакет предварительно подготовленные приложения hello.</span><span class="sxs-lookup"><span data-stu-id="d22ae-139">hello services that you can create from an application are defined in a service manifest in hello previously provisioned application package.</span></span>

```azurecli
az sf service create --app-id TestApp --name fabric:/TestApp/TestSvc --service-type TestServiceType \
--stateless --instance-count 1 --singleton-scheme
```

## <a name="verify-application-deployment-and-health"></a><span data-ttu-id="d22ae-140">Проверка развертывания и работоспособности приложения</span><span class="sxs-lookup"><span data-stu-id="d22ae-140">Verify application deployment and health</span></span>

<span data-ttu-id="d22ae-141">tooverify, что приложения и службы были успешно развернуты, проверьте, указаны hello приложения и службы:</span><span class="sxs-lookup"><span data-stu-id="d22ae-141">tooverify that an application and service were successfully deployed, check that hello application and service are listed:</span></span>

```azurecli
az sf application list
az sf service list --application-list TestApp
```

<span data-ttu-id="d22ae-142">tooverify, что служба hello находится в работоспособном состоянии, используйте аналогичные команды tooretrieve hello работоспособности hello службы и приложения hello.</span><span class="sxs-lookup"><span data-stu-id="d22ae-142">tooverify that hello service is healthy, use similar commands tooretrieve hello health of both hello service and hello application:</span></span>

```azurecli
az sf application health --application-id TestApp
az sf service health --service-id TestApp/TestSvc
```

<span data-ttu-id="d22ae-143">Параметр `HealthState` работоспособных служб и приложений должен иметь значение `Ok`.</span><span class="sxs-lookup"><span data-stu-id="d22ae-143">Healthy services and applications have a `HealthState` value of `Ok`.</span></span>

## <a name="remove-an-existing-application"></a><span data-ttu-id="d22ae-144">Удаление имеющегося приложения</span><span class="sxs-lookup"><span data-stu-id="d22ae-144">Remove an existing application</span></span>

<span data-ttu-id="d22ae-145">tooremove приложения, завершения hello следующие задачи.</span><span class="sxs-lookup"><span data-stu-id="d22ae-145">tooremove an application, complete hello following tasks.</span></span>

### <a name="delete-hello-application"></a><span data-ttu-id="d22ae-146">Удаление приложения hello</span><span class="sxs-lookup"><span data-stu-id="d22ae-146">Delete hello application</span></span>

<span data-ttu-id="d22ae-147">приложение hello toodelete, hello используйте следующую команду:</span><span class="sxs-lookup"><span data-stu-id="d22ae-147">toodelete hello application, use hello following command:</span></span>

```azurecli
az sf application delete --application-id TestEdApp
```

### <a name="unprovision-hello-application-type"></a><span data-ttu-id="d22ae-148">Отменить подготовку типа приложения hello</span><span class="sxs-lookup"><span data-stu-id="d22ae-148">Unprovision hello application type</span></span>

<span data-ttu-id="d22ae-149">После удаления приложения hello, можно отменить подготовку типа приложения hello, если оно больше не требуется.</span><span class="sxs-lookup"><span data-stu-id="d22ae-149">After you delete hello application, you can unprovision hello application type if you no longer need it.</span></span> <span data-ttu-id="d22ae-150">Тип приложения hello toounprovision, hello используйте следующую команду:</span><span class="sxs-lookup"><span data-stu-id="d22ae-150">toounprovision hello application type, use hello following command:</span></span>

```azurecli
az sf application unprovision --application-type-name TestAppTye --application-type-version 1.0
```

<span data-ttu-id="d22ae-151">версия по имени и типа тип Hello должна соответствовать hello имени и версии в манифесте предварительно подготовленные приложения hello.</span><span class="sxs-lookup"><span data-stu-id="d22ae-151">hello type name and type version must match hello name and version in hello previously provisioned application manifest.</span></span>

### <a name="delete-hello-application-package"></a><span data-ttu-id="d22ae-152">Удалить пакет приложения hello</span><span class="sxs-lookup"><span data-stu-id="d22ae-152">Delete hello application package</span></span>

<span data-ttu-id="d22ae-153">После отменил инициализацию типа приложения hello, можно удалить пакет приложения hello из хранилища образов hello, если оно больше не требуется.</span><span class="sxs-lookup"><span data-stu-id="d22ae-153">After you have unprovisioned hello application type, you can delete hello application package from hello image store if you no longer need it.</span></span> <span data-ttu-id="d22ae-154">Удалите пакеты приложения, чтобы освободить место на диске.</span><span class="sxs-lookup"><span data-stu-id="d22ae-154">Deleting application packages helps reclaim disk space.</span></span> 

<span data-ttu-id="d22ae-155">пакет приложения hello toodelete из хранилища образов hello, hello используйте следующую команду:</span><span class="sxs-lookup"><span data-stu-id="d22ae-155">toodelete hello application package from hello image store, use hello following command:</span></span>

```azurecli
az sf application package-delete --content-path app_package_dir
```

<span data-ttu-id="d22ae-156">`content-path`должно быть именем hello hello каталога, который загружен при создании приложения hello.</span><span class="sxs-lookup"><span data-stu-id="d22ae-156">`content-path` must be hello name of hello directory that you uploaded when you created hello application.</span></span>

## <a name="related-articles"></a><span data-ttu-id="d22ae-157">Связанные статьи</span><span class="sxs-lookup"><span data-stu-id="d22ae-157">Related articles</span></span>

* [<span data-ttu-id="d22ae-158">Service Fabric и Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="d22ae-158">Get started with Service Fabric and Azure CLI 2.0</span></span>](service-fabric-azure-cli-2-0.md)
* [<span data-ttu-id="d22ae-159">Использование интерфейса командной строки Azure для взаимодействия с кластером Service Fabric</span><span class="sxs-lookup"><span data-stu-id="d22ae-159">Get started with Service Fabric XPlat CLI</span></span>](service-fabric-azure-cli.md)
