---
title: "Использование ACR для кластера DC/OS Azure | Документация Майкрософт"
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
ms.openlocfilehash: 618d32ca919e50d41b85c800225fe72c3b94e537
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="use-acr-with-a-dcos-cluster-to-deploy-your-application"></a><span data-ttu-id="5786f-104">Использование ACR в кластере DC/OS для развертывания приложения</span><span class="sxs-lookup"><span data-stu-id="5786f-104">Use ACR with a DC/OS cluster to deploy your application</span></span>

<span data-ttu-id="5786f-105">В этой статье вы узнаете, как использовать реестр контейнеров Azure с кластером DC/OS.</span><span class="sxs-lookup"><span data-stu-id="5786f-105">In this article, we explore how to use Azure Container Registry with a DC/OS cluster.</span></span> <span data-ttu-id="5786f-106">Использование ACR позволяет закрыто хранить образы контейнеров и управлять ими.</span><span class="sxs-lookup"><span data-stu-id="5786f-106">Using ACR allows you to privately store and manage container images.</span></span> <span data-ttu-id="5786f-107">В рамках этого руководства рассматриваются следующие задачи:</span><span class="sxs-lookup"><span data-stu-id="5786f-107">This tutorial covers the following tasks:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="5786f-108">Развертывание реестра контейнеров Azure (при необходимости).</span><span class="sxs-lookup"><span data-stu-id="5786f-108">Deploy Azure Container Registry (if needed)</span></span>
> * <span data-ttu-id="5786f-109">Настройка проверки подлинности ACR в кластере DC/OS.</span><span class="sxs-lookup"><span data-stu-id="5786f-109">Configure ACR authentication on a DC/OS cluster</span></span>
> * <span data-ttu-id="5786f-110">Отправка образа в реестр контейнеров Azure.</span><span class="sxs-lookup"><span data-stu-id="5786f-110">Uploaded an image to the Azure Container Registry</span></span>
> * <span data-ttu-id="5786f-111">Запуск образа контейнера из реестра контейнеров Azure.</span><span class="sxs-lookup"><span data-stu-id="5786f-111">Run a container image from the Azure Container Registry</span></span>

<span data-ttu-id="5786f-112">Для выполнения действий, описанных в этом руководстве, потребуется кластер ACS DC/OS.</span><span class="sxs-lookup"><span data-stu-id="5786f-112">You need an ACS DC/OS cluster to complete the steps in this tutorial.</span></span> <span data-ttu-id="5786f-113">При необходимости его можно создать с помощью следующего [примера сценария](./../kubernetes/scripts/container-service-cli-deploy-dcos.md).</span><span class="sxs-lookup"><span data-stu-id="5786f-113">If needed, [this script sample](./../kubernetes/scripts/container-service-cli-deploy-dcos.md) can create one for you.</span></span>

<span data-ttu-id="5786f-114">Для этого руководства требуется Azure CLI версии 2.0.4 или более поздней.</span><span class="sxs-lookup"><span data-stu-id="5786f-114">This tutorial requires the Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="5786f-115">Чтобы узнать версию, выполните команду `az --version`.</span><span class="sxs-lookup"><span data-stu-id="5786f-115">Run `az --version` to find the version.</span></span> <span data-ttu-id="5786f-116">Если вам необходимо выполнить обновление, см. статью [Установка Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="5786f-116">If you need to upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

## <a name="deploy-azure-container-registry"></a><span data-ttu-id="5786f-117">Развертывание реестра контейнеров Azure</span><span class="sxs-lookup"><span data-stu-id="5786f-117">Deploy Azure Container Registry</span></span>

<span data-ttu-id="5786f-118">При необходимости создайте реестр контейнеров Azure с помощью команды [az acr create](/cli/azure/acr#create).</span><span class="sxs-lookup"><span data-stu-id="5786f-118">If needed, create an Azure Container registry with the [az acr create](/cli/azure/acr#create) command.</span></span> 

<span data-ttu-id="5786f-119">В следующем примере создается реестр со случайно созданным именем.</span><span class="sxs-lookup"><span data-stu-id="5786f-119">The following example creates a registry with a randomly generate name.</span></span> <span data-ttu-id="5786f-120">При этом он настраивается с учетной записью администратора с помощью аргумента `--admin-enabled`.</span><span class="sxs-lookup"><span data-stu-id="5786f-120">The registry is also configured with an admin account using the `--admin-enabled` argument.</span></span>

```azurecli-interactive
az acr create --resource-group myResourceGroup --name myContainerRegistry$RANDOM --sku Basic --admin-enabled true
```

<span data-ttu-id="5786f-121">После создания реестра Azure CLI выводит данные, подобные следующим.</span><span class="sxs-lookup"><span data-stu-id="5786f-121">Once the registry has been created, the Azure CLI outputs data similar to the following.</span></span> <span data-ttu-id="5786f-122">Запишите `name` и `loginServer`, так как они понадобятся на следующих шагах.</span><span class="sxs-lookup"><span data-stu-id="5786f-122">Take note of the `name` and `loginServer`, these are used in later steps.</span></span>

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

<span data-ttu-id="5786f-123">Получите учетные данные реестра контейнеров с помощью команды [az acr credential show](/cli/azure/acr/credential).</span><span class="sxs-lookup"><span data-stu-id="5786f-123">Get the container registry credentials using the [az acr credential show](/cli/azure/acr/credential) command.</span></span> <span data-ttu-id="5786f-124">Замените `--name` значением, записанным на предыдущем шаге.</span><span class="sxs-lookup"><span data-stu-id="5786f-124">Substitute the `--name` with the one noted in the last step.</span></span> <span data-ttu-id="5786f-125">Запишите один пароль, так как он потребуется в дальнейшем.</span><span class="sxs-lookup"><span data-stu-id="5786f-125">Take note of one password, it is needed in a later step.</span></span>

```azurecli-interactive
az acr credential show --name myContainerRegistry23489
```

<span data-ttu-id="5786f-126">Дополнительные сведения о реестре контейнеров Azure см. в статье [Общие сведения о частных реестрах контейнеров Docker](../../container-registry/container-registry-intro.md).</span><span class="sxs-lookup"><span data-stu-id="5786f-126">For more information on Azure Container Registry, see [Introduction to private Docker container registries](../../container-registry/container-registry-intro.md).</span></span> 

## <a name="manage-acr-authentication"></a><span data-ttu-id="5786f-127">Управление проверкой подлинности ACR</span><span class="sxs-lookup"><span data-stu-id="5786f-127">Manage ACR authentication</span></span>

<span data-ttu-id="5786f-128">Обычно, чтобы получить образ из закрытого реестра или передать образ в реестр, вам прежде всего нужно пройти проверку подлинности в реестре.</span><span class="sxs-lookup"><span data-stu-id="5786f-128">The conventional way to push and pull image from a private registry is to first authenticate with the registry.</span></span> <span data-ttu-id="5786f-129">Чтобы сделать это, используйте команду `docker login` на любом клиенте, которому требуется доступ к закрытому реестру.</span><span class="sxs-lookup"><span data-stu-id="5786f-129">To do so, you would use the `docker login` command on any client that needs to access the private registry.</span></span> <span data-ttu-id="5786f-130">Так как кластер DC/OS может содержать множество узлов, которые должны пройти проверку подлинности с помощью ACR, полезно автоматизировать этот процесс для каждого узла.</span><span class="sxs-lookup"><span data-stu-id="5786f-130">Because a DC/OS cluster can contain many nodes, all of which need to be authenticated with the ACR, it is helpful to automate this process across each node.</span></span> 

### <a name="create-shared-storage"></a><span data-ttu-id="5786f-131">Создание общего хранилища</span><span class="sxs-lookup"><span data-stu-id="5786f-131">Create shared storage</span></span>

<span data-ttu-id="5786f-132">Этот процесс использует общую папку Azure, которая была подключена на каждом узле кластера.</span><span class="sxs-lookup"><span data-stu-id="5786f-132">This process uses an Azure file share that has been mounted on each node in the cluster.</span></span> <span data-ttu-id="5786f-133">Если вы еще не настроили общее хранилище, ознакомьтесь со статьей [Создание и подключение файлового ресурса к кластеру DC/OS](container-service-dcos-fileshare.md).</span><span class="sxs-lookup"><span data-stu-id="5786f-133">If you have not already set up shared storage, see [Setup a file share inside a DC/OS cluster](container-service-dcos-fileshare.md).</span></span>

### <a name="configure-acr-authentication"></a><span data-ttu-id="5786f-134">Настройка проверки подлинности ACR</span><span class="sxs-lookup"><span data-stu-id="5786f-134">Configure ACR authentication</span></span>

<span data-ttu-id="5786f-135">Сначала получите полное доменное имя главного кластера DC/OS и сохраните его в переменной.</span><span class="sxs-lookup"><span data-stu-id="5786f-135">First, get the FQDN of the DC/OS master and store it in a variable.</span></span>

```azurecli-interactive
FQDN=$(az acs list --resource-group myResourceGroup --query "[0].masterProfile.fqdn" --output tsv)
```

<span data-ttu-id="5786f-136">Создайте SSH-подключение к главному узлу (или первому главному узлу) кластера DC/OS.</span><span class="sxs-lookup"><span data-stu-id="5786f-136">Create an SSH connection with the master (or the first master) of your DC/OS-based cluster.</span></span> <span data-ttu-id="5786f-137">Измените имя пользователя, если при создании кластера использовалось значение не по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="5786f-137">Update the user name if a non-default value was used when creating the cluster.</span></span>

```azurecli-interactive
ssh azureuser@$FQDN
```

<span data-ttu-id="5786f-138">Выполните следующую команду, чтобы войти в реестр контейнеров Azure.</span><span class="sxs-lookup"><span data-stu-id="5786f-138">Run the following command to login to the Azure Container Registry.</span></span> <span data-ttu-id="5786f-139">Замените `--username` именем реестра контейнеров, а `--password` — одним из предоставленных паролей.</span><span class="sxs-lookup"><span data-stu-id="5786f-139">Replace the `--username` with the name of the container registry, and the `--password` with one of the provided passwords.</span></span> <span data-ttu-id="5786f-140">Замените последний аргумент *mycontainerregistry.azurecr.io* в примере именем loginServer реестра контейнеров.</span><span class="sxs-lookup"><span data-stu-id="5786f-140">Replace the last argument *mycontainerregistry.azurecr.io* in the example with the loginServer name of the container registry.</span></span> 

<span data-ttu-id="5786f-141">Эта команда сохраняет значения для проверки подлинности локально в пути `~/.docker`.</span><span class="sxs-lookup"><span data-stu-id="5786f-141">This command stores the authentication values locally under the `~/.docker` path.</span></span>

```azurecli-interactive
docker -H tcp://localhost:2375 login --username=myContainerRegistry23489 --password=//=ls++q/m+w+pQDb/xCi0OhD=2c/hST mycontainerregistry.azurecr.io
```

<span data-ttu-id="5786f-142">Создайте сжатый файл, который содержит значения проверки подлинности реестра контейнера.</span><span class="sxs-lookup"><span data-stu-id="5786f-142">Create a compressed file that contains the container registry authentication values.</span></span>

```azurecli-interactive
tar czf docker.tar.gz .docker
```

<span data-ttu-id="5786f-143">Скопируйте этот файл в общее хранилище кластера.</span><span class="sxs-lookup"><span data-stu-id="5786f-143">Copy this file to the cluster shared storage.</span></span> <span data-ttu-id="5786f-144">Этот шаг делает файл доступным на всех узлах кластера DC/OS.</span><span class="sxs-lookup"><span data-stu-id="5786f-144">This step makes the file available on all nodes of the DC/OS cluster.</span></span>

```azurecli-interactive
cp docker.tar.gz /mnt/share/dcosshare
```

## <a name="upload-image-to-acr"></a><span data-ttu-id="5786f-145">Отправка образа в ACR</span><span class="sxs-lookup"><span data-stu-id="5786f-145">Upload image to ACR</span></span>

<span data-ttu-id="5786f-146">Теперь из компьютера разработки или любой другой системы с установленным Docker создайте образ и отправьте его в реестр контейнеров Azure.</span><span class="sxs-lookup"><span data-stu-id="5786f-146">Now from a development machine, or any other system with Docker installed, create an image and upload it to the Azure Container Registry.</span></span>

<span data-ttu-id="5786f-147">Создайте контейнер из образа Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="5786f-147">Create a container from the Ubuntu image.</span></span>

```azurecli-interactive
docker run ubunut --name base-image
```

<span data-ttu-id="5786f-148">Теперь добавьте контейнер в новый образ.</span><span class="sxs-lookup"><span data-stu-id="5786f-148">Now capture the container into a new image.</span></span> <span data-ttu-id="5786f-149">Имя образа должно включать имя `loginServer` реестра контейнеров в формате `loginServer/imageName`.</span><span class="sxs-lookup"><span data-stu-id="5786f-149">The image name needs to include the `loginServer` name of the container registrywith a format of `loginServer/imageName`.</span></span>

```azurecli-interactive
docker -H tcp://localhost:2375 commit base-image mycontainerregistry30678.azurecr.io/dcos-demo
````

<span data-ttu-id="5786f-150">Войдите в реестр контейнеров Azure.</span><span class="sxs-lookup"><span data-stu-id="5786f-150">Login into the Azure Container Registry.</span></span> <span data-ttu-id="5786f-151">Замените имя именем loginServer, --username — именем реестра контейнеров, а --password — одним из предоставленных паролей.</span><span class="sxs-lookup"><span data-stu-id="5786f-151">Replace the name with the loginServer name, the --username with the name of the container registry, and the --password with one of the provided passwords.</span></span>

```azurecli-interactive
docker login --username=myContainerRegistry23489 --password=//=ls++q/m+w+pQDb/xCi0OhD=2c/hST mycontainerregistry2675.azurecr.io
```

<span data-ttu-id="5786f-152">Наконец, отправьте образ в реестр ACR.</span><span class="sxs-lookup"><span data-stu-id="5786f-152">Finally, upload the image to the ACR registry.</span></span> <span data-ttu-id="5786f-153">Этот пример отправляет образ с именем dcos-demo.</span><span class="sxs-lookup"><span data-stu-id="5786f-153">This example uploads an image named dcos-demo.</span></span>

```azurecli-interactive
docker push mycontainerregistry30678.azurecr.io/dcos-demo
```

## <a name="run-an-image-from-acr"></a><span data-ttu-id="5786f-154">Запуск образа из ACR</span><span class="sxs-lookup"><span data-stu-id="5786f-154">Run an image from ACR</span></span>

<span data-ttu-id="5786f-155">Чтобы использовать образ из реестра ACR, создайте файл с именем *acrDemo.json* и скопируйте в него следующий текст.</span><span class="sxs-lookup"><span data-stu-id="5786f-155">To use an image from the ACR registry, create a file names *acrDemo.json* and copy the following text into it.</span></span> <span data-ttu-id="5786f-156">Замените имя образа именем loginServer реестра контейнеров и именем образа, например `loginServer/imageName`.</span><span class="sxs-lookup"><span data-stu-id="5786f-156">Replace the image name with the container registry loginServer name and image name, for example `loginServer/imageName`.</span></span> <span data-ttu-id="5786f-157">Обратите внимание на свойство `uris`.</span><span class="sxs-lookup"><span data-stu-id="5786f-157">Take note of the `uris` property.</span></span> <span data-ttu-id="5786f-158">Это свойство содержит расположение файла проверки подлинности реестра контейнеров, который в данном случае является общей папкой Azure, установленной на каждом узле в кластере DC/OS.</span><span class="sxs-lookup"><span data-stu-id="5786f-158">This property holds the location of the container registry authentication file, which in this case is the Azure file share that is mounted on each node in the DC/OS cluster.</span></span>

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

<span data-ttu-id="5786f-159">Разверните приложение с помощью CLI DC/OS.</span><span class="sxs-lookup"><span data-stu-id="5786f-159">Deploy the application with the DC/OC CLI.</span></span>

```azurecli-interactive
dcos marathon app add acrDemo.json
```

## <a name="next-steps"></a><span data-ttu-id="5786f-160">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="5786f-160">Next steps</span></span>

<span data-ttu-id="5786f-161">В этом руководстве вы настроили кластер DC/OS для использования с реестром контейнеров Azure, в частности выполнили следующие задачи:</span><span class="sxs-lookup"><span data-stu-id="5786f-161">In this tutorial you have configure DC/OS to use Azure Container Registry including the following tasks:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="5786f-162">Развертывание реестра контейнеров Azure (при необходимости).</span><span class="sxs-lookup"><span data-stu-id="5786f-162">Deploy Azure Container Registry (if needed)</span></span>
> * <span data-ttu-id="5786f-163">Настройка проверки подлинности ACR в кластере DC/OS.</span><span class="sxs-lookup"><span data-stu-id="5786f-163">Configure ACR authentication on a DC/OS cluster</span></span>
> * <span data-ttu-id="5786f-164">Отправка образа в реестр контейнеров Azure.</span><span class="sxs-lookup"><span data-stu-id="5786f-164">Uploaded an image to the Azure Container Registry</span></span>
> * <span data-ttu-id="5786f-165">Запуск образа контейнера из реестра контейнеров Azure.</span><span class="sxs-lookup"><span data-stu-id="5786f-165">Run a container image from the Azure Container Registry</span></span>
