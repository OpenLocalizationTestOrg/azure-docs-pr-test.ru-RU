---
title: "aaaUsing контроля доступа с кластера с контроллера домена или ОС Azure | Документы Microsoft"
description: "Использование реестра контейнеров Azure с кластером DC/OS в Службе контейнеров Azure"
services: container-service
documentationcenter: 
author: julienstroheker
manager: dcaro
editor: 
tags: acs, azure-container-service, acr, azure-container-registry
keywords: "Docker, контейнеры, микрослужбы, Mesos, Azure, FileShare, cifs"
ms.assetid: 
ms.service: container-service
ms.devlang: na
ms.topic: tutorial
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/23/2017
ms.author: juliens
ms.custom: mvc
ms.openlocfilehash: 9a2802da788b50147d8b4259436bdcdb0c929db8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-acr-with-a-dcos-cluster-toodeploy-your-application"></a><span data-ttu-id="57b19-104">Использовать ACR toodeploy кластера DC/OS приложение</span><span class="sxs-lookup"><span data-stu-id="57b19-104">Use ACR with a DC/OS cluster toodeploy your application</span></span>

<span data-ttu-id="57b19-105">В этой статье мы исследуем как toouse реестра контейнера Azure в кластере DC/OS.</span><span class="sxs-lookup"><span data-stu-id="57b19-105">In this article, we explore how toouse Azure Container Registry with a DC/OS cluster.</span></span> <span data-ttu-id="57b19-106">С помощью контроля доступа позволяет tooprivately хранилище и управление образами контейнеров.</span><span class="sxs-lookup"><span data-stu-id="57b19-106">Using ACR allows you tooprivately store and manage container images.</span></span> <span data-ttu-id="57b19-107">В этом учебнике hello следующие задачи:</span><span class="sxs-lookup"><span data-stu-id="57b19-107">This tutorial covers hello following tasks:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="57b19-108">Развертывание реестра контейнеров Azure (при необходимости).</span><span class="sxs-lookup"><span data-stu-id="57b19-108">Deploy Azure Container Registry (if needed)</span></span>
> * <span data-ttu-id="57b19-109">Настройка проверки подлинности ACR в кластере DC/OS.</span><span class="sxs-lookup"><span data-stu-id="57b19-109">Configure ACR authentication on a DC/OS cluster</span></span>
> * <span data-ttu-id="57b19-110">Загрузить образ toohello реестра контейнера Azure</span><span class="sxs-lookup"><span data-stu-id="57b19-110">Uploaded an image toohello Azure Container Registry</span></span>
> * <span data-ttu-id="57b19-111">Запустите образ контейнера из hello реестра контейнера Azure</span><span class="sxs-lookup"><span data-stu-id="57b19-111">Run a container image from hello Azure Container Registry</span></span>

<span data-ttu-id="57b19-112">Вы должны ACS DC/OS hello toocomplete кластера шаги в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="57b19-112">You need an ACS DC/OS cluster toocomplete hello steps in this tutorial.</span></span> <span data-ttu-id="57b19-113">При необходимости его можно создать с помощью следующего [примера сценария](./../kubernetes/scripts/container-service-cli-deploy-dcos.md).</span><span class="sxs-lookup"><span data-stu-id="57b19-113">If needed, [this script sample](./../kubernetes/scripts/container-service-cli-deploy-dcos.md) can create one for you.</span></span>

<span data-ttu-id="57b19-114">Упражнений этого учебника требуется hello Azure CLI версия 2.0.4 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="57b19-114">This tutorial requires hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="57b19-115">Запустите `az --version` версии toofind hello.</span><span class="sxs-lookup"><span data-stu-id="57b19-115">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="57b19-116">Получить tooupgrade [установить CLI Azure 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="57b19-116">If you need tooupgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

## <a name="deploy-azure-container-registry"></a><span data-ttu-id="57b19-117">Развертывание реестра контейнеров Azure</span><span class="sxs-lookup"><span data-stu-id="57b19-117">Deploy Azure Container Registry</span></span>

<span data-ttu-id="57b19-118">При необходимости создайте в реестре контейнера Azure с hello [создать az acr](/cli/azure/acr#create) команды.</span><span class="sxs-lookup"><span data-stu-id="57b19-118">If needed, create an Azure Container registry with hello [az acr create](/cli/azure/acr#create) command.</span></span> 

<span data-ttu-id="57b19-119">Hello следующий пример создает реестр с помощью создания случайного имени.</span><span class="sxs-lookup"><span data-stu-id="57b19-119">hello following example creates a registry with a randomly generate name.</span></span> <span data-ttu-id="57b19-120">Hello реестра настроен с учетной записью администратора, с использованием hello `--admin-enabled` аргумент.</span><span class="sxs-lookup"><span data-stu-id="57b19-120">hello registry is also configured with an admin account using hello `--admin-enabled` argument.</span></span>

```azurecli-interactive
az acr create --resource-group myResourceGroup --name myContainerRegistry$RANDOM --sku Basic --admin-enabled true
```

<span data-ttu-id="57b19-121">После создания реестра hello hello Azure CLI выводит примерно следующие toohello данных.</span><span class="sxs-lookup"><span data-stu-id="57b19-121">Once hello registry has been created, hello Azure CLI outputs data similar toohello following.</span></span> <span data-ttu-id="57b19-122">Запишите hello `name` и `loginServer`, они используются в последующих шагах.</span><span class="sxs-lookup"><span data-stu-id="57b19-122">Take note of hello `name` and `loginServer`, these are used in later steps.</span></span>

```azurecli
{
  "adminUserEnabled": false,
  "creationDate": "2017-06-06T03:40:56.511597+00:00",
  "id": "/subscriptions/f2799821-a08a-434e-9128-454ec4348b10/resourcegroups/myResourceGroup/providers/Microsoft.ContainerRegistry/registries/myContainerRegistry23489",
  "location": "eastus",
  "loginServer": "mycontainerregistry23489.azurecr.io",
  "name": "myContainerRegistry23489",
  "provisioningState": "Succeeded",
  "sku": {
    "name": "Basic",
    "tier": "Basic"
  },
  "storageAccount": {
    "name": "mycontainerregistr034017"
  },
  "tags": {},
  "type": "Microsoft.ContainerRegistry/registries"
}
```

<span data-ttu-id="57b19-123">Получить учетные данные реестра hello контейнера с помощью hello [Показать учетных данных acr az](/cli/azure/acr/credential) команды.</span><span class="sxs-lookup"><span data-stu-id="57b19-123">Get hello container registry credentials using hello [az acr credential show](/cli/azure/acr/credential) command.</span></span> <span data-ttu-id="57b19-124">Замена hello `--name` с одного указаны в последнем шаге hello hello.</span><span class="sxs-lookup"><span data-stu-id="57b19-124">Substitute hello `--name` with hello one noted in hello last step.</span></span> <span data-ttu-id="57b19-125">Запишите один пароль, так как он потребуется в дальнейшем.</span><span class="sxs-lookup"><span data-stu-id="57b19-125">Take note of one password, it is needed in a later step.</span></span>

```azurecli-interactive
az acr credential show --name myContainerRegistry23489
```

<span data-ttu-id="57b19-126">Дополнительные сведения о реестре контейнера Azure см. в разделе [введение tooprivate Docker контейнера реестры](../../container-registry/container-registry-intro.md).</span><span class="sxs-lookup"><span data-stu-id="57b19-126">For more information on Azure Container Registry, see [Introduction tooprivate Docker container registries](../../container-registry/container-registry-intro.md).</span></span> 

## <a name="manage-acr-authentication"></a><span data-ttu-id="57b19-127">Управление проверкой подлинности ACR</span><span class="sxs-lookup"><span data-stu-id="57b19-127">Manage ACR authentication</span></span>

<span data-ttu-id="57b19-128">проверить подлинность Hello традиционным способом toopush и запросу образа из частной реестра — toofirst реестра hello.</span><span class="sxs-lookup"><span data-stu-id="57b19-128">hello conventional way toopush and pull image from a private registry is toofirst authenticate with hello registry.</span></span> <span data-ttu-id="57b19-129">toodo таким образом, можно использовать hello `docker login` команду на любом клиенте, который должен tooaccess hello частного реестра.</span><span class="sxs-lookup"><span data-stu-id="57b19-129">toodo so, you would use hello `docker login` command on any client that needs tooaccess hello private registry.</span></span> <span data-ttu-id="57b19-130">Поскольку кластера DC/OS может содержать множество узлов, каждый из которых требуется toobe с hello контроля доступа с проверкой подлинности, это полезно tooautomate этот процесс на каждом узле.</span><span class="sxs-lookup"><span data-stu-id="57b19-130">Because a DC/OS cluster can contain many nodes, all of which need toobe authenticated with hello ACR, it is helpful tooautomate this process across each node.</span></span> 

### <a name="create-shared-storage"></a><span data-ttu-id="57b19-131">Создание общего хранилища</span><span class="sxs-lookup"><span data-stu-id="57b19-131">Create shared storage</span></span>

<span data-ttu-id="57b19-132">Этот процесс использует Azure файловый ресурс, который был подключен на каждом узле в кластере hello.</span><span class="sxs-lookup"><span data-stu-id="57b19-132">This process uses an Azure file share that has been mounted on each node in hello cluster.</span></span> <span data-ttu-id="57b19-133">Если вы еще не настроили общее хранилище, ознакомьтесь со статьей [Создание и подключение файлового ресурса к кластеру DC/OS](container-service-dcos-fileshare.md).</span><span class="sxs-lookup"><span data-stu-id="57b19-133">If you have not already set up shared storage, see [Setup a file share inside a DC/OS cluster](container-service-dcos-fileshare.md).</span></span>

### <a name="configure-acr-authentication"></a><span data-ttu-id="57b19-134">Настройка проверки подлинности ACR</span><span class="sxs-lookup"><span data-stu-id="57b19-134">Configure ACR authentication</span></span>

<span data-ttu-id="57b19-135">Сначала необходимо получите hello полное доменное имя hello DC/OS-шаблоны и сохранить его в переменной.</span><span class="sxs-lookup"><span data-stu-id="57b19-135">First, get hello FQDN of hello DC/OS master and store it in a variable.</span></span>

```azurecli-interactive
FQDN=$(az acs list --resource-group myResourceGroup --query "[0].masterProfile.fqdn" --output tsv)
```

<span data-ttu-id="57b19-136">Создайте SSH-подключения с hello master (или первый образец hello) кластера на базе контроллера домена/ОС.</span><span class="sxs-lookup"><span data-stu-id="57b19-136">Create an SSH connection with hello master (or hello first master) of your DC/OS-based cluster.</span></span> <span data-ttu-id="57b19-137">Обновите имя пользователя hello, если значение не по умолчанию использовался при создании кластера hello.</span><span class="sxs-lookup"><span data-stu-id="57b19-137">Update hello user name if a non-default value was used when creating hello cluster.</span></span>

```azurecli-interactive
ssh azureuser@$FQDN
```

<span data-ttu-id="57b19-138">Выполнения hello следующая команда toologin toohello реестра контейнера Azure.</span><span class="sxs-lookup"><span data-stu-id="57b19-138">Run hello following command toologin toohello Azure Container Registry.</span></span> <span data-ttu-id="57b19-139">Замените hello `--username` с именем hello реестра контейнера hello и hello `--password` с одним из предоставленных hello пароли.</span><span class="sxs-lookup"><span data-stu-id="57b19-139">Replace hello `--username` with hello name of hello container registry, and hello `--password` with one of hello provided passwords.</span></span> <span data-ttu-id="57b19-140">Замените hello последний аргумент *mycontainerregistry.azurecr.io* в примере hello именем loginServer hello hello контейнер реестра.</span><span class="sxs-lookup"><span data-stu-id="57b19-140">Replace hello last argument *mycontainerregistry.azurecr.io* in hello example with hello loginServer name of hello container registry.</span></span> 

<span data-ttu-id="57b19-141">Эта команда сохраняет значения для проверки подлинности hello локально под hello `~/.docker` пути.</span><span class="sxs-lookup"><span data-stu-id="57b19-141">This command stores hello authentication values locally under hello `~/.docker` path.</span></span>

```azurecli-interactive
docker -H tcp://localhost:2375 login --username=myContainerRegistry23489 --password=//=ls++q/m+w+pQDb/xCi0OhD=2c/hST mycontainerregistry.azurecr.io
```

<span data-ttu-id="57b19-142">Создайте сжатый файл, содержащий hello контейнер реестра проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="57b19-142">Create a compressed file that contains hello container registry authentication values.</span></span>

```azurecli-interactive
tar czf docker.tar.gz .docker
```

<span data-ttu-id="57b19-143">Скопируйте этот файл toohello общее хранилище кластера.</span><span class="sxs-lookup"><span data-stu-id="57b19-143">Copy this file toohello cluster shared storage.</span></span> <span data-ttu-id="57b19-144">Этот шаг делает файл hello недоступны на всех узлах кластера DC/OS hello.</span><span class="sxs-lookup"><span data-stu-id="57b19-144">This step makes hello file available on all nodes of hello DC/OS cluster.</span></span>

```azurecli-interactive
cp docker.tar.gz /mnt/share/dcosshare
```

## <a name="upload-image-tooacr"></a><span data-ttu-id="57b19-145">Отправка изображения tooACR</span><span class="sxs-lookup"><span data-stu-id="57b19-145">Upload image tooACR</span></span>

<span data-ttu-id="57b19-146">Теперь с компьютера разработки, или любой другой системы с установленным Docker, создать образ и загрузить его toohello реестра контейнера Azure.</span><span class="sxs-lookup"><span data-stu-id="57b19-146">Now from a development machine, or any other system with Docker installed, create an image and upload it toohello Azure Container Registry.</span></span>

<span data-ttu-id="57b19-147">Создание контейнера из образа Ubuntu hello.</span><span class="sxs-lookup"><span data-stu-id="57b19-147">Create a container from hello Ubuntu image.</span></span>

```azurecli-interactive
docker run ubunut --name base-image
```

<span data-ttu-id="57b19-148">Теперь выполните захват hello контейнера в новый образ.</span><span class="sxs-lookup"><span data-stu-id="57b19-148">Now capture hello container into a new image.</span></span> <span data-ttu-id="57b19-149">Имя образа Hello должно tooinclude hello `loginServer` имя registrywith контейнера hello в формат `loginServer/imageName`.</span><span class="sxs-lookup"><span data-stu-id="57b19-149">hello image name needs tooinclude hello `loginServer` name of hello container registrywith a format of `loginServer/imageName`.</span></span>

```azurecli-interactive
docker -H tcp://localhost:2375 commit base-image mycontainerregistry30678.azurecr.io/dcos-demo
````

<span data-ttu-id="57b19-150">Имя входа в hello реестра контейнера Azure.</span><span class="sxs-lookup"><span data-stu-id="57b19-150">Login into hello Azure Container Registry.</span></span> <span data-ttu-id="57b19-151">Замените имя hello имя loginServer hello, hello — имя пользователя с именем hello реестра контейнера hello и hello--пароль с помощью одного из предоставленных hello пароли.</span><span class="sxs-lookup"><span data-stu-id="57b19-151">Replace hello name with hello loginServer name, hello --username with hello name of hello container registry, and hello --password with one of hello provided passwords.</span></span>

```azurecli-interactive
docker login --username=myContainerRegistry23489 --password=//=ls++q/m+w+pQDb/xCi0OhD=2c/hST mycontainerregistry2675.azurecr.io
```

<span data-ttu-id="57b19-152">Наконец отправьте hello изображения toohello ACR реестра.</span><span class="sxs-lookup"><span data-stu-id="57b19-152">Finally, upload hello image toohello ACR registry.</span></span> <span data-ttu-id="57b19-153">Этот пример отправляет образ с именем dcos-demo.</span><span class="sxs-lookup"><span data-stu-id="57b19-153">This example uploads an image named dcos-demo.</span></span>

```azurecli-interactive
docker push mycontainerregistry30678.azurecr.io/dcos-demo
```

## <a name="run-an-image-from-acr"></a><span data-ttu-id="57b19-154">Запуск образа из ACR</span><span class="sxs-lookup"><span data-stu-id="57b19-154">Run an image from ACR</span></span>

<span data-ttu-id="57b19-155">toouse образа из реестра hello контроля доступа, создайте файл имена *acrDemo.json* и копирования hello после текста в него.</span><span class="sxs-lookup"><span data-stu-id="57b19-155">toouse an image from hello ACR registry, create a file names *acrDemo.json* and copy hello following text into it.</span></span> <span data-ttu-id="57b19-156">Замените имя образа hello hello реестра loginServer имени для контейнера и имя изображения, например `loginServer/imageName`.</span><span class="sxs-lookup"><span data-stu-id="57b19-156">Replace hello image name with hello container registry loginServer name and image name, for example `loginServer/imageName`.</span></span> <span data-ttu-id="57b19-157">Запишите hello `uris` свойство.</span><span class="sxs-lookup"><span data-stu-id="57b19-157">Take note of hello `uris` property.</span></span> <span data-ttu-id="57b19-158">Это свойство содержит hello расположение файла реестра проверки подлинности hello контейнера, который в данном случае является hello Azure файловый ресурс, монтируется на каждом узле в кластере DC/OS hello.</span><span class="sxs-lookup"><span data-stu-id="57b19-158">This property holds hello location of hello container registry authentication file, which in this case is hello Azure file share that is mounted on each node in hello DC/OS cluster.</span></span>

```json
{
  "id": "myapp",
  "container": {
    "type": "DOCKER",
    "docker": {
      "image": "mycontainerregistry30678.azurecr.io/dcos-demo",
      "network": "BRIDGE",
      "portMappings": [
        {
          "containerPort": 80,
          "hostPort": 80,
          "protocol": "tcp",
          "name": "80",
          "labels": null
        }
      ],
      "forcePullImage":true
    }
  },
  "instances": 3,
  "cpus": 0.1,
  "mem": 65,
  "healthChecks": [{
      "protocol": "HTTP",
      "path": "/",
      "portIndex": 0,
      "timeoutSeconds": 10,
      "gracePeriodSeconds": 10,
      "intervalSeconds": 2,
      "maxConsecutiveFailures": 10
  }],
  "uris":  [
       "file:///mnt/share/dcosshare/docker.tar.gz"
   ]
}
```

<span data-ttu-id="57b19-159">Развертывание приложения hello с hello DC/OC CLI.</span><span class="sxs-lookup"><span data-stu-id="57b19-159">Deploy hello application with hello DC/OC CLI.</span></span>

```azurecli-interactive
dcos marathon app add acrDemo.json
```

## <a name="next-steps"></a><span data-ttu-id="57b19-160">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="57b19-160">Next steps</span></span>

<span data-ttu-id="57b19-161">В этом учебнике у настройки toouse DC/OS, которое реестра контейнера Azure, включая hello следующие задачи:</span><span class="sxs-lookup"><span data-stu-id="57b19-161">In this tutorial you have configure DC/OS toouse Azure Container Registry including hello following tasks:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="57b19-162">Развертывание реестра контейнеров Azure (при необходимости).</span><span class="sxs-lookup"><span data-stu-id="57b19-162">Deploy Azure Container Registry (if needed)</span></span>
> * <span data-ttu-id="57b19-163">Настройка проверки подлинности ACR в кластере DC/OS.</span><span class="sxs-lookup"><span data-stu-id="57b19-163">Configure ACR authentication on a DC/OS cluster</span></span>
> * <span data-ttu-id="57b19-164">Загрузить образ toohello реестра контейнера Azure</span><span class="sxs-lookup"><span data-stu-id="57b19-164">Uploaded an image toohello Azure Container Registry</span></span>
> * <span data-ttu-id="57b19-165">Запустите образ контейнера из hello реестра контейнера Azure</span><span class="sxs-lookup"><span data-stu-id="57b19-165">Run a container image from hello Azure Container Registry</span></span>
