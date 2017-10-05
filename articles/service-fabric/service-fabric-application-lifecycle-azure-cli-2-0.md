---
title: "Управление приложениями Azure Service Fabric с помощью Azure CLI 2.0"
description: "Узнайте, как развертывать приложения и удалить их из кластера с Azure Service Fabric с помощью Azure CLI 2.0."
services: service-fabric
author: samedder
manager: timlt
ms.service: service-fabric
ms.topic: article
ms.date: 06/21/2017
ms.author: edwardsa
ms.openlocfilehash: 5728339236e3819b301e428f9d7a8add08f02b3e
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="manage-an-azure-service-fabric-application-by-using-azure-cli-20"></a><span data-ttu-id="16b50-103">Управление приложением Azure Service Fabric с помощью Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="16b50-103">Manage an Azure Service Fabric application by using Azure CLI 2.0</span></span>

<span data-ttu-id="16b50-104">Узнайте, как создавать и удалять приложения, выполняющиеся в кластере Azure Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="16b50-104">Learn how to create and delete applications that are running in an Azure Service Fabric cluster.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="16b50-105">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="16b50-105">Prerequisites</span></span>

* <span data-ttu-id="16b50-106">Установите Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="16b50-106">Install Azure CLI 2.0.</span></span> <span data-ttu-id="16b50-107">и выберите кластер Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="16b50-107">Then, select your Service Fabric cluster.</span></span> <span data-ttu-id="16b50-108">Дополнительные сведения можно найти в документации по [началу работы с Azure CLI 2.0](service-fabric-azure-cli-2-0.md).</span><span class="sxs-lookup"><span data-stu-id="16b50-108">For more information, see [Get started with Azure CLI 2.0](service-fabric-azure-cli-2-0.md).</span></span>

* <span data-ttu-id="16b50-109">Также требуется готовый к развертыванию пакет приложения Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="16b50-109">Have a Service Fabric application package ready to be deployed.</span></span> <span data-ttu-id="16b50-110">Дополнительные сведения о том, как создавать и упаковывать приложения, представлены в [документации по модели приложения Service Fabric](service-fabric-application-model.md).</span><span class="sxs-lookup"><span data-stu-id="16b50-110">For more information about how to author and package an application, read about the [Service Fabric application model](service-fabric-application-model.md).</span></span>

## <a name="overview"></a><span data-ttu-id="16b50-111">Обзор</span><span class="sxs-lookup"><span data-stu-id="16b50-111">Overview</span></span>

<span data-ttu-id="16b50-112">Чтобы развернуть новое приложение, выполните указанные ниже действия.</span><span class="sxs-lookup"><span data-stu-id="16b50-112">To deploy a new application, complete these steps:</span></span>

1. <span data-ttu-id="16b50-113">Отправьте пакет приложения в хранилище образов Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="16b50-113">Upload an application package to the Service Fabric image store.</span></span>
2. <span data-ttu-id="16b50-114">Подготовьте тип приложения.</span><span class="sxs-lookup"><span data-stu-id="16b50-114">Provision an application type.</span></span>
3. <span data-ttu-id="16b50-115">Укажите приложение и создайте его.</span><span class="sxs-lookup"><span data-stu-id="16b50-115">Specify and create an application.</span></span>
4. <span data-ttu-id="16b50-116">Укажите службы и создайте их.</span><span class="sxs-lookup"><span data-stu-id="16b50-116">Specify and create services.</span></span>

<span data-ttu-id="16b50-117">Чтобы удалить существующее приложение, выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="16b50-117">To remove an existing application, complete these steps:</span></span>

1. <span data-ttu-id="16b50-118">Удалите приложение.</span><span class="sxs-lookup"><span data-stu-id="16b50-118">Delete the application.</span></span>
2. <span data-ttu-id="16b50-119">Отмените подготовку связанного типа приложения.</span><span class="sxs-lookup"><span data-stu-id="16b50-119">Unprovision the associated application type.</span></span>
3. <span data-ttu-id="16b50-120">Удалите содержимое из хранилища образов.</span><span class="sxs-lookup"><span data-stu-id="16b50-120">Delete the image store content.</span></span>

## <a name="deploy-a-new-application"></a><span data-ttu-id="16b50-121">Развертывание нового приложения</span><span class="sxs-lookup"><span data-stu-id="16b50-121">Deploy a new application</span></span>

<span data-ttu-id="16b50-122">Чтобы развернуть новое приложение, выполните указанные ниже действия.</span><span class="sxs-lookup"><span data-stu-id="16b50-122">To deploy a new application, complete the following tasks.</span></span>

### <a name="upload-a-new-application-package-to-the-image-store"></a><span data-ttu-id="16b50-123">Передача нового пакета приложения в хранилище образов</span><span class="sxs-lookup"><span data-stu-id="16b50-123">Upload a new application package to the image store</span></span>

<span data-ttu-id="16b50-124">Прежде чем создавать приложение, необходимо отправить пакет приложения в хранилище образов Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="16b50-124">Before you create an application, upload the application package to the Service Fabric image store.</span></span> 

<span data-ttu-id="16b50-125">Предположим, что пакет приложения существует в каталоге `app_package_dir`. Чтобы отправить каталог, выполните следующие команды:</span><span class="sxs-lookup"><span data-stu-id="16b50-125">For example, if your application package is in the `app_package_dir` directory, use the following commands to upload the directory:</span></span>

```azurecli
az sf application upload --path ~/app_package_dir
```

<span data-ttu-id="16b50-126">Для больших пакетов приложений вы можете указать параметр `--show-progress`, чтобы отобразить ход передачи.</span><span class="sxs-lookup"><span data-stu-id="16b50-126">For large application packages, you can specify the `--show-progress` option to display the progress of the upload.</span></span>

### <a name="provision-the-application-type"></a><span data-ttu-id="16b50-127">Подготовка типа приложения</span><span class="sxs-lookup"><span data-stu-id="16b50-127">Provision the application type</span></span>

<span data-ttu-id="16b50-128">По завершении отправки необходимо подготовить приложение.</span><span class="sxs-lookup"><span data-stu-id="16b50-128">When the upload is finished, provision the application.</span></span> <span data-ttu-id="16b50-129">Чтобы подготовить приложение, выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="16b50-129">To provision the application, use the following command:</span></span>

```azurecli
az sf application provision --application-type-build-path app_package_dir
```

<span data-ttu-id="16b50-130">Параметр `application-type-build-path` должен совпадать с именем каталога, содержащего пакет приложения, который был отправлен ранее.</span><span class="sxs-lookup"><span data-stu-id="16b50-130">The value for `application-type-build-path` is the name of the directory where you uploaded your application package.</span></span>

### <a name="create-an-application-from-an-application-type"></a><span data-ttu-id="16b50-131">Создание приложения из типа приложения</span><span class="sxs-lookup"><span data-stu-id="16b50-131">Create an application from an application type</span></span>

<span data-ttu-id="16b50-132">После подготовки приложения можно присвоить ему имя и создать приложение, выполнив следующую команду:</span><span class="sxs-lookup"><span data-stu-id="16b50-132">After you provision the application, use the following command to name and create your application:</span></span>

```azurecli
az sf application create --app-name fabric:/TestApp --app-type TestAppType --app-version 1.0
```

<span data-ttu-id="16b50-133">`app-name` — это имя, которое получит экземпляр приложения.</span><span class="sxs-lookup"><span data-stu-id="16b50-133">`app-name` is the name that you want to use for the application instance.</span></span> <span data-ttu-id="16b50-134">Другие параметры можно найти с помощью манифеста приложения, который был подготовлен ранее.</span><span class="sxs-lookup"><span data-stu-id="16b50-134">You can get additional parameters from the previously provisioned application manifest.</span></span>

<span data-ttu-id="16b50-135">Имя приложения должно начинаться с префикса `fabric:/`.</span><span class="sxs-lookup"><span data-stu-id="16b50-135">The application name must start with the prefix `fabric:/`.</span></span>

### <a name="create-services-for-the-new-application"></a><span data-ttu-id="16b50-136">Создание служб для нового приложения</span><span class="sxs-lookup"><span data-stu-id="16b50-136">Create services for the new application</span></span>

<span data-ttu-id="16b50-137">После создания приложения из него можно создавать службы.</span><span class="sxs-lookup"><span data-stu-id="16b50-137">After you have created an application, create services from the application.</span></span> <span data-ttu-id="16b50-138">В этом примере мы создадим из приложения службу без отслеживания состояния.</span><span class="sxs-lookup"><span data-stu-id="16b50-138">In the following example, we create a new stateless service from our application.</span></span> <span data-ttu-id="16b50-139">Службы, которые можно создать из приложения, определены в манифесте службы внутри подготовленного ранее пакета приложения.</span><span class="sxs-lookup"><span data-stu-id="16b50-139">The services that you can create from an application are defined in a service manifest in the previously provisioned application package.</span></span>

```azurecli
az sf service create --app-id TestApp --name fabric:/TestApp/TestSvc --service-type TestServiceType \
--stateless --instance-count 1 --singleton-scheme
```

## <a name="verify-application-deployment-and-health"></a><span data-ttu-id="16b50-140">Проверка развертывания и работоспособности приложения</span><span class="sxs-lookup"><span data-stu-id="16b50-140">Verify application deployment and health</span></span>

<span data-ttu-id="16b50-141">Чтобы проверить, что приложение и служба были успешно развернуты, убедитесь, что они отображаются:</span><span class="sxs-lookup"><span data-stu-id="16b50-141">To verify that an application and service were successfully deployed, check that the application and service are listed:</span></span>

```azurecli
az sf application list
az sf service list --application-list TestApp
```

<span data-ttu-id="16b50-142">Чтобы проверить, что служба работоспособна, выполните аналогичные команды, чтобы получить сведения о работоспособности службы и приложения.</span><span class="sxs-lookup"><span data-stu-id="16b50-142">To verify that the service is healthy, use similar commands to retrieve the health of both the service and the application:</span></span>

```azurecli
az sf application health --application-id TestApp
az sf service health --service-id TestApp/TestSvc
```

<span data-ttu-id="16b50-143">Параметр `HealthState` работоспособных служб и приложений должен иметь значение `Ok`.</span><span class="sxs-lookup"><span data-stu-id="16b50-143">Healthy services and applications have a `HealthState` value of `Ok`.</span></span>

## <a name="remove-an-existing-application"></a><span data-ttu-id="16b50-144">Удаление имеющегося приложения</span><span class="sxs-lookup"><span data-stu-id="16b50-144">Remove an existing application</span></span>

<span data-ttu-id="16b50-145">Чтобы удалить приложение, выполните указанные ниже действия.</span><span class="sxs-lookup"><span data-stu-id="16b50-145">To remove an application, complete the following tasks.</span></span>

### <a name="delete-the-application"></a><span data-ttu-id="16b50-146">Удаление приложения</span><span class="sxs-lookup"><span data-stu-id="16b50-146">Delete the application</span></span>

<span data-ttu-id="16b50-147">Удалите приложение, выполнив следующую команду:</span><span class="sxs-lookup"><span data-stu-id="16b50-147">To delete the application, use the following command:</span></span>

```azurecli
az sf application delete --application-id TestEdApp
```

### <a name="unprovision-the-application-type"></a><span data-ttu-id="16b50-148">Отмена подготовки типа приложения</span><span class="sxs-lookup"><span data-stu-id="16b50-148">Unprovision the application type</span></span>

<span data-ttu-id="16b50-149">После удаления приложения можно также отменить подготовку типа приложения (если он больше не требуется).</span><span class="sxs-lookup"><span data-stu-id="16b50-149">After you delete the application, you can unprovision the application type if you no longer need it.</span></span> <span data-ttu-id="16b50-150">Для этого выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="16b50-150">To unprovision the application type, use the following command:</span></span>

```azurecli
az sf application unprovision --application-type-name TestAppTye --application-type-version 1.0
```

<span data-ttu-id="16b50-151">Имя и версия типа должны соответствовать имени и версии в манифесте приложения, который был подготовлен ранее.</span><span class="sxs-lookup"><span data-stu-id="16b50-151">The type name and type version must match the name and version in the previously provisioned application manifest.</span></span>

### <a name="delete-the-application-package"></a><span data-ttu-id="16b50-152">Удаление пакета приложения</span><span class="sxs-lookup"><span data-stu-id="16b50-152">Delete the application package</span></span>

<span data-ttu-id="16b50-153">После того как подготовка типа приложения была отменена, пакет приложения можно удалить из хранилища образов (если он больше не требуется).</span><span class="sxs-lookup"><span data-stu-id="16b50-153">After you have unprovisioned the application type, you can delete the application package from the image store if you no longer need it.</span></span> <span data-ttu-id="16b50-154">Удалите пакеты приложения, чтобы освободить место на диске.</span><span class="sxs-lookup"><span data-stu-id="16b50-154">Deleting application packages helps reclaim disk space.</span></span> 

<span data-ttu-id="16b50-155">Чтобы удалить пакет приложения из хранилища образов, выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="16b50-155">To delete the application package from the image store, use the following command:</span></span>

```azurecli
az sf application package-delete --content-path app_package_dir
```

<span data-ttu-id="16b50-156">Параметр `content-path` должен совпадать с именем каталога, загруженного при создании приложения.</span><span class="sxs-lookup"><span data-stu-id="16b50-156">`content-path` must be the name of the directory that you uploaded when you created the application.</span></span>

## <a name="related-articles"></a><span data-ttu-id="16b50-157">Связанные статьи</span><span class="sxs-lookup"><span data-stu-id="16b50-157">Related articles</span></span>

* [<span data-ttu-id="16b50-158">Service Fabric и Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="16b50-158">Get started with Service Fabric and Azure CLI 2.0</span></span>](service-fabric-azure-cli-2-0.md)
* [<span data-ttu-id="16b50-159">Использование интерфейса командной строки Azure для взаимодействия с кластером Service Fabric</span><span class="sxs-lookup"><span data-stu-id="16b50-159">Get started with Service Fabric XPlat CLI</span></span>](service-fabric-azure-cli.md)
