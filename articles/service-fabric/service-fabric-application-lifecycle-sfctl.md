---
title: "Управление приложениями Azure Service Fabric с помощью интерфейса командной строки Azure Service Fabric"
description: "Узнайте, как развертывать приложения в кластере Azure Service Fabric и удалять их из него с помощью интерфейса командной строки Azure Service Fabric."
services: service-fabric
author: samedder
manager: timlt
ms.service: service-fabric
ms.topic: article
ms.date: 08/22/2017
ms.author: edwardsa
ms.openlocfilehash: c3a2eb3e6e54f952ef963bb2a0292d9ad7b53bc5
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="manage-an-azure-service-fabric-application-by-using-azure-service-fabric-cli"></a><span data-ttu-id="810ee-103">Управление приложением Azure Service Fabric с помощью интерфейса командной строки Azure Service Fabric</span><span class="sxs-lookup"><span data-stu-id="810ee-103">Manage an Azure Service Fabric application by using Azure Service Fabric CLI</span></span>

<span data-ttu-id="810ee-104">Узнайте, как создавать и удалять приложения, выполняющиеся в кластере Azure Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="810ee-104">Learn how to create and delete applications that are running in an Azure Service Fabric cluster.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="810ee-105">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="810ee-105">Prerequisites</span></span>

* <span data-ttu-id="810ee-106">Установите интерфейс командной строки Service Fabric</span><span class="sxs-lookup"><span data-stu-id="810ee-106">Install Service Fabric CLI.</span></span> <span data-ttu-id="810ee-107">и выберите кластер Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="810ee-107">Then, select your Service Fabric cluster.</span></span> <span data-ttu-id="810ee-108">Дополнительные сведения см. в статье [Azure Service Fabric command line](service-fabric-cli.md) (Интерфейс командной строки Azure Service Fabric).</span><span class="sxs-lookup"><span data-stu-id="810ee-108">For more information, see [Get started with Service Fabric CLI](service-fabric-cli.md).</span></span>

* <span data-ttu-id="810ee-109">Также требуется готовый к развертыванию пакет приложения Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="810ee-109">Have a Service Fabric application package ready to be deployed.</span></span> <span data-ttu-id="810ee-110">Дополнительные сведения о том, как создавать и упаковывать приложения, представлены в [документации по модели приложения Service Fabric](service-fabric-application-model.md).</span><span class="sxs-lookup"><span data-stu-id="810ee-110">For more information about how to author and package an application, read about the [Service Fabric application model](service-fabric-application-model.md).</span></span>

## <a name="overview"></a><span data-ttu-id="810ee-111">Обзор</span><span class="sxs-lookup"><span data-stu-id="810ee-111">Overview</span></span>

<span data-ttu-id="810ee-112">Чтобы развернуть новое приложение, выполните указанные ниже действия.</span><span class="sxs-lookup"><span data-stu-id="810ee-112">To deploy a new application, complete these steps:</span></span>

1. <span data-ttu-id="810ee-113">Отправьте пакет приложения в хранилище образов Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="810ee-113">Upload an application package to the Service Fabric image store.</span></span>
2. <span data-ttu-id="810ee-114">Подготовьте тип приложения.</span><span class="sxs-lookup"><span data-stu-id="810ee-114">Provision an application type.</span></span>
3. <span data-ttu-id="810ee-115">Укажите приложение и создайте его.</span><span class="sxs-lookup"><span data-stu-id="810ee-115">Specify and create an application.</span></span>
4. <span data-ttu-id="810ee-116">Укажите службы и создайте их.</span><span class="sxs-lookup"><span data-stu-id="810ee-116">Specify and create services.</span></span>

<span data-ttu-id="810ee-117">Чтобы удалить существующее приложение, выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="810ee-117">To remove an existing application, complete these steps:</span></span>

1. <span data-ttu-id="810ee-118">Удалите приложение.</span><span class="sxs-lookup"><span data-stu-id="810ee-118">Delete the application.</span></span>
2. <span data-ttu-id="810ee-119">Отмените подготовку связанного типа приложения.</span><span class="sxs-lookup"><span data-stu-id="810ee-119">Unprovision the associated application type.</span></span>
3. <span data-ttu-id="810ee-120">Удалите содержимое из хранилища образов.</span><span class="sxs-lookup"><span data-stu-id="810ee-120">Delete the image store content.</span></span>

## <a name="deploy-a-new-application"></a><span data-ttu-id="810ee-121">Развертывание нового приложения</span><span class="sxs-lookup"><span data-stu-id="810ee-121">Deploy a new application</span></span>

<span data-ttu-id="810ee-122">Чтобы развернуть новое приложение, выполните указанные ниже действия.</span><span class="sxs-lookup"><span data-stu-id="810ee-122">To deploy a new application, complete the following tasks:</span></span>

### <a name="upload-a-new-application-package-to-the-image-store"></a><span data-ttu-id="810ee-123">Передача нового пакета приложения в хранилище образов</span><span class="sxs-lookup"><span data-stu-id="810ee-123">Upload a new application package to the image store</span></span>

<span data-ttu-id="810ee-124">Прежде чем создавать приложение, необходимо отправить пакет приложения в хранилище образов Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="810ee-124">Before you create an application, upload the application package to the Service Fabric image store.</span></span>

<span data-ttu-id="810ee-125">Предположим, что пакет приложения существует в каталоге `app_package_dir`. Чтобы отправить каталог, выполните следующие команды:</span><span class="sxs-lookup"><span data-stu-id="810ee-125">For example, if your application package is in the `app_package_dir` directory, use the following commands to upload the directory:</span></span>

```azurecli
sfctl application upload --path ~/app_package_dir
```

<span data-ttu-id="810ee-126">Для больших пакетов приложений вы можете указать параметр `--show-progress`, чтобы отобразить ход передачи.</span><span class="sxs-lookup"><span data-stu-id="810ee-126">For large application packages, you can specify the `--show-progress` option to display the progress of the upload.</span></span>

### <a name="provision-the-application-type"></a><span data-ttu-id="810ee-127">Подготовка типа приложения</span><span class="sxs-lookup"><span data-stu-id="810ee-127">Provision the application type</span></span>

<span data-ttu-id="810ee-128">По завершении отправки необходимо подготовить приложение.</span><span class="sxs-lookup"><span data-stu-id="810ee-128">When the upload is finished, provision the application.</span></span> <span data-ttu-id="810ee-129">Чтобы подготовить приложение, выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="810ee-129">To provision the application, use the following command:</span></span>

```azurecli
sfctl application provision --application-type-build-path app_package_dir
```

<span data-ttu-id="810ee-130">Параметр `application-type-build-path` должен совпадать с именем каталога, содержащего пакет приложения, который был отправлен ранее.</span><span class="sxs-lookup"><span data-stu-id="810ee-130">The value for `application-type-build-path` is the name of the directory where you uploaded your application package.</span></span>

### <a name="create-an-application-from-an-application-type"></a><span data-ttu-id="810ee-131">Создание приложения из типа приложения</span><span class="sxs-lookup"><span data-stu-id="810ee-131">Create an application from an application type</span></span>

<span data-ttu-id="810ee-132">После подготовки приложения можно присвоить ему имя и создать приложение, выполнив следующую команду:</span><span class="sxs-lookup"><span data-stu-id="810ee-132">After you provision the application, use the following command to name and create your application:</span></span>

```azurecli
sfctl application create --app-name fabric:/TestApp --app-type TestAppType --app-version 1.0
```

<span data-ttu-id="810ee-133">`app-name` — это имя, которое получит экземпляр приложения.</span><span class="sxs-lookup"><span data-stu-id="810ee-133">`app-name` is the name that you want to use for the application instance.</span></span> <span data-ttu-id="810ee-134">Другие параметры можно найти с помощью манифеста приложения, который был подготовлен ранее.</span><span class="sxs-lookup"><span data-stu-id="810ee-134">You can get additional parameters from the previously provisioned application manifest.</span></span>

<span data-ttu-id="810ee-135">Имя приложения должно начинаться с префикса `fabric:/`.</span><span class="sxs-lookup"><span data-stu-id="810ee-135">The application name must start with the prefix `fabric:/`.</span></span>

### <a name="create-services-for-the-new-application"></a><span data-ttu-id="810ee-136">Создание служб для нового приложения</span><span class="sxs-lookup"><span data-stu-id="810ee-136">Create services for the new application</span></span>

<span data-ttu-id="810ee-137">После создания приложения из него можно создавать службы.</span><span class="sxs-lookup"><span data-stu-id="810ee-137">After you have created an application, create services from the application.</span></span> <span data-ttu-id="810ee-138">В этом примере мы создадим из приложения службу без отслеживания состояния.</span><span class="sxs-lookup"><span data-stu-id="810ee-138">In the following example, we create a new stateless service from our application.</span></span> <span data-ttu-id="810ee-139">Службы, которые можно создать из приложения, определены в манифесте службы внутри подготовленного ранее пакета приложения.</span><span class="sxs-lookup"><span data-stu-id="810ee-139">The services that you can create from an application are defined in a service manifest in the previously provisioned application package.</span></span>

```azurecli
sfctl service create --app-id TestApp --name fabric:/TestApp/TestSvc --service-type TestServiceType \
--stateless --instance-count 1 --singleton-scheme
```

## <a name="verify-application-deployment-and-health"></a><span data-ttu-id="810ee-140">Проверка развертывания и работоспособности приложения</span><span class="sxs-lookup"><span data-stu-id="810ee-140">Verify application deployment and health</span></span>

<span data-ttu-id="810ee-141">Чтобы убедиться, что все находится в работоспособном состоянии, выполните приведенные ниже команды.</span><span class="sxs-lookup"><span data-stu-id="810ee-141">To verify everything is healthy, use the following health commands:</span></span>

```azurecli
sfctl application list
sfctl service list --application-id TestApp
```

<span data-ttu-id="810ee-142">Чтобы проверить, что служба работоспособна, выполните аналогичные команды, чтобы получить сведения о работоспособности службы и приложения.</span><span class="sxs-lookup"><span data-stu-id="810ee-142">To verify that the service is healthy, use similar commands to retrieve the health of both the service and the application:</span></span>

```azurecli
sfctl application health --application-id TestApp
sfctl service health --service-id TestApp/TestSvc
```

<span data-ttu-id="810ee-143">Параметр `HealthState` работоспособных служб и приложений должен иметь значение `Ok`.</span><span class="sxs-lookup"><span data-stu-id="810ee-143">Healthy services and applications have a `HealthState` value of `Ok`.</span></span>

## <a name="remove-an-existing-application"></a><span data-ttu-id="810ee-144">Удаление имеющегося приложения</span><span class="sxs-lookup"><span data-stu-id="810ee-144">Remove an existing application</span></span>

<span data-ttu-id="810ee-145">Чтобы удалить приложение, выполните указанные ниже действия.</span><span class="sxs-lookup"><span data-stu-id="810ee-145">To remove an application, complete the following tasks:</span></span>

### <a name="delete-the-application"></a><span data-ttu-id="810ee-146">Удаление приложения</span><span class="sxs-lookup"><span data-stu-id="810ee-146">Delete the application</span></span>

<span data-ttu-id="810ee-147">Удалите приложение, выполнив следующую команду:</span><span class="sxs-lookup"><span data-stu-id="810ee-147">To delete the application, use the following command:</span></span>

```azurecli
sfctl application delete --application-id TestEdApp
```

### <a name="unprovision-the-application-type"></a><span data-ttu-id="810ee-148">Отмена подготовки типа приложения</span><span class="sxs-lookup"><span data-stu-id="810ee-148">Unprovision the application type</span></span>

<span data-ttu-id="810ee-149">После удаления приложения можно также отменить подготовку типа приложения (если он больше не требуется).</span><span class="sxs-lookup"><span data-stu-id="810ee-149">After you delete the application, you can unprovision the application type if you no longer need it.</span></span> <span data-ttu-id="810ee-150">Для этого выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="810ee-150">To unprovision the application type, use the following command:</span></span>

```azurecli
sfctl application unprovision --application-type-name TestAppTye --application-type-version 1.0
```

<span data-ttu-id="810ee-151">Имя и версия типа должны соответствовать имени и версии в манифесте приложения, который был подготовлен ранее.</span><span class="sxs-lookup"><span data-stu-id="810ee-151">The type name and type version must match the name and version in the previously provisioned application manifest.</span></span>

### <a name="delete-the-application-package"></a><span data-ttu-id="810ee-152">Удаление пакета приложения</span><span class="sxs-lookup"><span data-stu-id="810ee-152">Delete the application package</span></span>

<span data-ttu-id="810ee-153">После того как подготовка типа приложения была отменена, пакет приложения можно удалить из хранилища образов (если он больше не требуется).</span><span class="sxs-lookup"><span data-stu-id="810ee-153">After you have unprovisioned the application type, you can delete the application package from the image store if you no longer need it.</span></span> <span data-ttu-id="810ee-154">Удалите пакеты приложения, чтобы освободить место на диске.</span><span class="sxs-lookup"><span data-stu-id="810ee-154">Deleting application packages helps reclaim disk space.</span></span> 

<span data-ttu-id="810ee-155">Чтобы удалить пакет приложения из хранилища образов, выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="810ee-155">To delete the application package from the image store, use the following command:</span></span>

```azurecli
sfctl store delete --content-path app_package_dir
```

<span data-ttu-id="810ee-156">Параметр `content-path` должен совпадать с именем каталога, загруженного при создании приложения.</span><span class="sxs-lookup"><span data-stu-id="810ee-156">`content-path` must be the name of the directory that you uploaded when you created the application.</span></span>

## <a name="upgrade-application"></a><span data-ttu-id="810ee-157">Обновление приложения</span><span class="sxs-lookup"><span data-stu-id="810ee-157">Upgrade application</span></span>

<span data-ttu-id="810ee-158">После создания приложения можно повторить тот же набор шагов, чтобы подготовить вторую версию приложения.</span><span class="sxs-lookup"><span data-stu-id="810ee-158">After creating your application, you can repeat the same set of steps to provision a second version of your application.</span></span> <span data-ttu-id="810ee-159">Затем с помощью функции обновления приложения Service Fabric можно перейти к использованию второй версии приложения.</span><span class="sxs-lookup"><span data-stu-id="810ee-159">Then, with a Service Fabric application upgrade you can transition to running the second version of the application.</span></span> <span data-ttu-id="810ee-160">Дополнительные сведения см. в документации по [обновлению приложения Service Fabric](service-fabric-application-upgrade.md).</span><span class="sxs-lookup"><span data-stu-id="810ee-160">For more information, see the documentation on [Service Fabric application upgrades](service-fabric-application-upgrade.md).</span></span>

<span data-ttu-id="810ee-161">Чтобы выполнить обновление, необходимо сначала подготовить следующую версию приложения, используя ту же команду, что и раньше.</span><span class="sxs-lookup"><span data-stu-id="810ee-161">To perform an upgrade, first provision the next version of the application using the same commands as before:</span></span>

```azurecli
sfctl application upload --path ~/app_package_dir_2
sfctl application provision --application-type-build-path app_package_dir_2
```

<span data-ttu-id="810ee-162">Затем рекомендуется выполнить отслеживаемое автоматическое обновление. Запустите обновление, выполнив следующую команду.</span><span class="sxs-lookup"><span data-stu-id="810ee-162">It is recommended then to perform a monitored automatic upgrade, launch the upgrade by running the following command:</span></span>

```azurecli
sfctl application upgrade --app-id TestApp --app-version 2.0.0 --parameters "{\"test\":\"value\"}" --mode Monitored
```

<span data-ttu-id="810ee-163">Обновления переопределяют существующие параметры вне зависимости от способа их задания.</span><span class="sxs-lookup"><span data-stu-id="810ee-163">Upgrades override existing parameters with whatever set is specified.</span></span> <span data-ttu-id="810ee-164">При необходимости параметры приложения можно передать как аргументы команды обновления.</span><span class="sxs-lookup"><span data-stu-id="810ee-164">Application parameters should be passed as arguments to the upgrade command, if necessary.</span></span> <span data-ttu-id="810ee-165">Параметры приложения должны быть закодированы в виде объекта JSON.</span><span class="sxs-lookup"><span data-stu-id="810ee-165">Application parameters should be encoded as a JSON object.</span></span>

<span data-ttu-id="810ee-166">Чтобы получить какие-либо указанные ранее параметры, можно использовать команду `sfctl application info`.</span><span class="sxs-lookup"><span data-stu-id="810ee-166">To retrieve any parameters previously specified, you can use the `sfctl application info` command.</span></span>

<span data-ttu-id="810ee-167">Если выполняется обновление приложения, его состояние можно получить с помощью команды `sfctl application upgrade-status`.</span><span class="sxs-lookup"><span data-stu-id="810ee-167">When an application upgrade is in progress, the status can be retrieved using the `sfctl application upgrade-status` command.</span></span>

<span data-ttu-id="810ee-168">Наконец, если идет обновление и его необходимо отменить, можно использовать команду `sfctl application upgrade-rollback`, чтобы выполнить откат обновления.</span><span class="sxs-lookup"><span data-stu-id="810ee-168">Finally, if an upgrade is in progress and needs to be canceled, you can use the `sfctl application upgrade-rollback` to roll back the upgrade.</span></span>

## <a name="next-steps"></a><span data-ttu-id="810ee-169">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="810ee-169">Next steps</span></span>

* <span data-ttu-id="810ee-170">[Azure Service Fabric command line](service-fabric-cli.md) (Командная строка Azure Service Fabric)</span><span class="sxs-lookup"><span data-stu-id="810ee-170">[Service Fabric CLI basics](service-fabric-cli.md)</span></span>
* [<span data-ttu-id="810ee-171">Подготовка среды разработки в Linux</span><span class="sxs-lookup"><span data-stu-id="810ee-171">Getting started with Service Fabric on Linux</span></span>](service-fabric-get-started-linux.md)
* [<span data-ttu-id="810ee-172">Обновление приложения Service Fabric</span><span class="sxs-lookup"><span data-stu-id="810ee-172">Launching a Service Fabric application upgrade</span></span>](service-fabric-application-upgrade.md)
