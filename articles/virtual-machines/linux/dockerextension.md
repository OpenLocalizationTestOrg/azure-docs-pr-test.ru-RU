---
title: "Использование расширения виртуальной машины Docker для Azure | Документация Майкрософт"
description: "Узнайте, как использовать расширение виртуальной машины Docker для быстрого и безопасного развертывания среды Docker в Azure с помощью шаблонов Resource Manager и Azure CLI 2.0."
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
ms.assetid: 936d67d7-6921-4275-bf11-1e0115e66b7f
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/11/2017
ms.author: iainfou
ms.openlocfilehash: 63d0d80999fd57d014c74d5c6aef3733ec2afe85
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="create-a-docker-environment-in-azure-using-the-docker-vm-extension"></a><span data-ttu-id="186a3-103">Создание среды Docker в Azure с помощью расширения виртуальной машины Docker</span><span class="sxs-lookup"><span data-stu-id="186a3-103">Create a Docker environment in Azure using the Docker VM extension</span></span>
<span data-ttu-id="186a3-104">Docker — это популярная платформа для управления контейнерами и работы с образами, которая позволяет быстро работать с контейнерами в Linux.</span><span class="sxs-lookup"><span data-stu-id="186a3-104">Docker is a popular container management and imaging platform that allows you to quickly work with containers on Linux.</span></span> <span data-ttu-id="186a3-105">В Azure развертывание Docker можно выполнить несколькими разными способами в соответствии с конкретными потребностями.</span><span class="sxs-lookup"><span data-stu-id="186a3-105">In Azure, there are various ways you can deploy Docker according to your needs.</span></span> <span data-ttu-id="186a3-106">В этой статье рассматривается использование расширения виртуальной машины Docker и шаблонов Azure Resource Manager с помощью Azure CLI 2.0.</span><span class="sxs-lookup"><span data-stu-id="186a3-106">This article focuses on using the Docker VM extension and Azure Resource Manager templates with the Azure CLI 2.0.</span></span> <span data-ttu-id="186a3-107">Эти действия можно также выполнить с помощью [Azure CLI 1.0](dockerextension-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="186a3-107">You can also perform these steps with the [Azure CLI 1.0](dockerextension-nodejs.md).</span></span>

## <a name="azure-docker-vm-extension-overview"></a><span data-ttu-id="186a3-108">Общие сведения о расширении виртуальных машин Docker для Azure</span><span class="sxs-lookup"><span data-stu-id="186a3-108">Azure Docker VM extension overview</span></span>
<span data-ttu-id="186a3-109">Расширение виртуальных машин Docker для Azure устанавливает и настраивает управляющую программу Docker, клиент Docker и Docker Compose на виртуальной машине Linux.</span><span class="sxs-lookup"><span data-stu-id="186a3-109">The Azure Docker VM extension installs and configures the Docker daemon, Docker client, and Docker Compose in your Linux virtual machine (VM).</span></span> <span data-ttu-id="186a3-110">В отличие от использования только машины Docker или самостоятельного создания узла Docker с этим расширением вы получаете дополнительные элементы управления и компоненты.</span><span class="sxs-lookup"><span data-stu-id="186a3-110">By using the Azure Docker VM extension, you have more control and features than simply using Docker Machine or creating the Docker host yourself.</span></span> <span data-ttu-id="186a3-111">Благодаря этим дополнительным компонентам, таким как [Docker Compose](https://docs.docker.com/compose/overview/), расширение виртуальных машин Docker для Azure подходит для более надежных сред разработки или рабочих сред.</span><span class="sxs-lookup"><span data-stu-id="186a3-111">These additional features, such as [Docker Compose](https://docs.docker.com/compose/overview/), make the Azure Docker VM extension suited for more robust developer or production environments.</span></span>

<span data-ttu-id="186a3-112">Дополнительные сведения о различных методах развертывания, в том числе с помощью Docker Machine и служб контейнеров Azure, см. в следующих статьях:</span><span class="sxs-lookup"><span data-stu-id="186a3-112">For more information about the different deployment methods, including using Docker Machine and Azure Container Services, see the following articles:</span></span>

* <span data-ttu-id="186a3-113">Чтобы быстро создать прототип приложения, можно создать один узел Docker с помощью [машины Docker](docker-machine.md).</span><span class="sxs-lookup"><span data-stu-id="186a3-113">To quickly prototype an app, you can create a single Docker host using [Docker Machine](docker-machine.md).</span></span>
* <span data-ttu-id="186a3-114">Чтобы создать готовые к работе, масштабируемые среды с дополнительными средствами планирования и управления, можно развернуть [кластер Docker Swarm в службах контейнеров Azure](../../container-service/dcos-swarm/container-service-deployment.md).</span><span class="sxs-lookup"><span data-stu-id="186a3-114">To build production-ready, scalable environments that provide additional scheduling and management tools, you can deploy a [Docker Swarm cluster on Azure Container Services](../../container-service/dcos-swarm/container-service-deployment.md).</span></span>

## <a name="deploy-a-template-with-the-azure-docker-vm-extension"></a><span data-ttu-id="186a3-115">Развертывание шаблона с помощью расширения виртуальных машин Docker для Azure</span><span class="sxs-lookup"><span data-stu-id="186a3-115">Deploy a template with the Azure Docker VM extension</span></span>
<span data-ttu-id="186a3-116">Чтобы создать виртуальную машину Ubuntu, на которой установлено расширение виртуальной машины Docker для Azure (для установки и настройки узла Docker), мы используем готовый шаблон быстрого запуска.</span><span class="sxs-lookup"><span data-stu-id="186a3-116">Let's use an existing quickstart template to create an Ubuntu VM that uses the Azure Docker VM extension to install and configure the Docker host.</span></span> <span data-ttu-id="186a3-117">Шаблон можно найти в разделе [Simple deployment of an Ubuntu VM with Docker](https://github.com/Azure/azure-quickstart-templates/tree/master/docker-simple-on-ubuntu)(Простое развертывание виртуальной машины Ubuntu с Docker).</span><span class="sxs-lookup"><span data-stu-id="186a3-117">You can view the template here: [Simple deployment of an Ubuntu VM with Docker](https://github.com/Azure/azure-quickstart-templates/tree/master/docker-simple-on-ubuntu).</span></span> <span data-ttu-id="186a3-118">Вам нужно установить последнюю версию [Azure CLI 2.0](/cli/azure/install-az-cli2) и войти в учетную запись Azure с помощью команды [az login](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="186a3-118">You need the latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in to an Azure account using [az login](/cli/azure/#login).</span></span>

<span data-ttu-id="186a3-119">Сначала создайте группу ресурсов с помощью команды [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="186a3-119">First, create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="186a3-120">В следующем примере создается группа ресурсов с именем *myResourceGroup* в расположении *westus*.</span><span class="sxs-lookup"><span data-stu-id="186a3-120">The following example creates a resource group named *myResourceGroup* in the *westus* location:</span></span>

```azurecli
az group create --name myResourceGroup --location westus
```

<span data-ttu-id="186a3-121">Затем, выполнив команду [az group deployment create](/cli/azure/group/deployment#create), разверните виртуальную машину с расширением виртуальной машины Docker для Azure с помощью [этого шаблона Azure Resource Manager из репозитория GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/docker-simple-on-ubuntu).</span><span class="sxs-lookup"><span data-stu-id="186a3-121">Next, deploy a VM with [az group deployment create](/cli/azure/group/deployment#create) that includes the Azure Docker VM extension from [this Azure Resource Manager template on GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/docker-simple-on-ubuntu).</span></span> <span data-ttu-id="186a3-122">Укажите собственные значения для параметров *newStorageAccountName*, *adminUsername*, *adminPassword* и *dnsNameForPublicIP*, как показано ниже:</span><span class="sxs-lookup"><span data-stu-id="186a3-122">Provide your own values for *newStorageAccountName*, *adminUsername*, *adminPassword*, and *dnsNameForPublicIP* as follows:</span></span>

```azurecli
az group deployment create --resource-group myResourceGroup \
  --parameters '{"newStorageAccountName": {"value": "mystorageaccount"},
    "adminUsername": {"value": "azureuser"},
    "adminPassword": {"value": "P@ssw0rd!"},
    "dnsNameForPublicIP": {"value": "mypublicdns"}}' \
  --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/docker-simple-on-ubuntu/azuredeploy.json
```

<span data-ttu-id="186a3-123">Подождите несколько минут до завершения развертывания.</span><span class="sxs-lookup"><span data-stu-id="186a3-123">It takes a few minutes for the deployment to finish.</span></span> <span data-ttu-id="186a3-124">После завершения развертывания [перейдите к следующему шагу](#deploy-your-first-nginx-container), чтобы подключиться к виртуальной машине по протоколу SSH.</span><span class="sxs-lookup"><span data-stu-id="186a3-124">Once the deployment is finished, [move to next step](#deploy-your-first-nginx-container) to SSH to your VM.</span></span> 

<span data-ttu-id="186a3-125">При необходимости, чтобы вернуть управление командной строке и позволить развертыванию работать в фоновом режиме, добавьте в предыдущую команду флаг `--no-wait`.</span><span class="sxs-lookup"><span data-stu-id="186a3-125">Optionally, to instead return control to the prompt and let the deployment continue in the background, add the `--no-wait` flag to the preceding command.</span></span> <span data-ttu-id="186a3-126">Этот процесс позволит выполнять другую работу в интерфейсе командной строки, пока в течение нескольких минут будет продолжаться развертывание.</span><span class="sxs-lookup"><span data-stu-id="186a3-126">This process allows you to perform other work in the CLI while the deployment continues for a few minutes.</span></span> 

<span data-ttu-id="186a3-127">После этого можно будет просмотреть сведения о состоянии узла Docker с помощью команды [az vm show](/cli/azure/vm#show).</span><span class="sxs-lookup"><span data-stu-id="186a3-127">You can then view details about the Docker host status with [az vm show](/cli/azure/vm#show).</span></span> <span data-ttu-id="186a3-128">В следующем примере проверяется состояние виртуальной машины с именем *myDockerVM* (имя по умолчанию, указанное в шаблоне; не изменяйте его) в группе ресурсов *myResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="186a3-128">The following example checks the status of the VM named *myDockerVM* (the default name from the template - don't change this name) in the resource group named *myResourceGroup*:</span></span>

```azurecli
az vm show \
    --resource-group myResourceGroup \
    --name myDockerVM \
    --query [provisioningState] \
    --output tsv
```

<span data-ttu-id="186a3-129">Если эта команда возвращает состояние *Succeeded*, значит, развертывание завершено, и вы сможете установить подключение SSH к виртуальной машине на следующем шаге.</span><span class="sxs-lookup"><span data-stu-id="186a3-129">When this command returns *Succeeded*, the deployment has finished and you can SSH to the VM in the following step.</span></span>

## <a name="deploy-your-first-nginx-container"></a><span data-ttu-id="186a3-130">Развертывание первого контейнера nginx</span><span class="sxs-lookup"><span data-stu-id="186a3-130">Deploy your first nginx container</span></span>
<span data-ttu-id="186a3-131">Для просмотра сведений о виртуальной машине, включая DNS-имя, можно использовать команду `az vm show -g myResourceGroup -n myDockerVM -d --query [fqdns] -o tsv`.</span><span class="sxs-lookup"><span data-stu-id="186a3-131">To view details of your VM, including the DNS name, use `az vm show -g myResourceGroup -n myDockerVM -d --query [fqdns] -o tsv`.</span></span> <span data-ttu-id="186a3-132">Установите подключение по протоколу SSH к новому узлу Docker с локального компьютера, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="186a3-132">SSH to your new Docker host from your local computer as follows:</span></span>

```bash
ssh azureuser@mypublicdns.westus.cloudapp.azure.com
```

<span data-ttu-id="186a3-133">После входа в систему узла Docker запустите контейнер nginx.</span><span class="sxs-lookup"><span data-stu-id="186a3-133">Once logged in to the Docker host, let's run an nginx container:</span></span>

```bash
sudo docker run -d -p 80:80 nginx
```

<span data-ttu-id="186a3-134">После скачивания образа nginx и запуска контейнера результаты должны выглядеть примерно так, как показано в следующем примере.</span><span class="sxs-lookup"><span data-stu-id="186a3-134">The output is similar to the following example as the nginx image is downloaded and a container started:</span></span>

```bash
Unable to find image 'nginx:latest' locally
latest: Pulling from library/nginx
efd26ecc9548: Pull complete
a3ed95caeb02: Pull complete
a48df1751a97: Pull complete
8ddc2d7beb91: Pull complete
Digest: sha256:2ca2638e55319b7bc0c7d028209ea69b1368e95b01383e66dfe7e4f43780926d
Status: Downloaded newer image for nginx:latest
b6ed109fb743a762ff21a4606dd38d3e5d35aff43fa7f12e8d4ed1d920b0cd74
```

<span data-ttu-id="186a3-135">Проверьте состояние контейнеров, запущенных на узле Docker, следующим образом.</span><span class="sxs-lookup"><span data-stu-id="186a3-135">Check the status of the containers running on your Docker host as follows:</span></span>

```bash
sudo docker ps
```

<span data-ttu-id="186a3-136">Результаты должны выглядеть примерно так, как показано ниже. В них должно быть указано, что контейнер nginx запущен, а TCP-порты 80 и 443 перенаправлены.</span><span class="sxs-lookup"><span data-stu-id="186a3-136">The output is similar to the following example, showing that the nginx container is running and TCP ports 80 and 443 and being forwarded:</span></span>

```bash
CONTAINER ID        IMAGE               COMMAND                  CREATED              STATUS              PORTS                         NAMES
b6ed109fb743        nginx               "nginx -g 'daemon off"   About a minute ago   Up About a minute   0.0.0.0:80->80/tcp, 443/tcp   adoring_payne
```

<span data-ttu-id="186a3-137">Чтобы увидеть контейнер в действии, откройте веб-браузер и введите DNS-имя узла Docker.</span><span class="sxs-lookup"><span data-stu-id="186a3-137">To see your container in action, open up a web browser and enter the DNS name of your Docker host:</span></span>

![Запущенный контейнер nginx](./media/dockerextension/nginxrunning.png)

## <a name="azure-docker-vm-extension-template-reference"></a><span data-ttu-id="186a3-139">Пример шаблона расширения виртуальной машины Docker для Azure</span><span class="sxs-lookup"><span data-stu-id="186a3-139">Azure Docker VM extension template reference</span></span>
<span data-ttu-id="186a3-140">В предыдущем примере использовался готовый шаблон быстрого запуска.</span><span class="sxs-lookup"><span data-stu-id="186a3-140">The previous example uses an existing quickstart template.</span></span> <span data-ttu-id="186a3-141">Расширение виртуальной машины Docker для Azure можно также развернуть с помощью собственных шаблонов Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="186a3-141">You can also deploy the Azure Docker VM extension with your own Resource Manager templates.</span></span> <span data-ttu-id="186a3-142">Для этого добавьте следующий код в свои шаблоны Resource Manager, задав вместо `vmName` имя своей виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="186a3-142">To do so, add the following to your Resource Manager templates, defining the `vmName` of your VM appropriately:</span></span>

```json
{
  "type": "Microsoft.Compute/virtualMachines/extensions",
  "name": "[concat(variables('vmName'), '/DockerExtension'))]",
  "apiVersion": "2015-05-01-preview",
  "location": "[parameters('location')]",
  "dependsOn": [
    "[concat('Microsoft.Compute/virtualMachines/', variables('vmName'))]"
  ],
  "properties": {
    "publisher": "Microsoft.Azure.Extensions",
    "type": "DockerExtension",
    "typeHandlerVersion": "1.*",
    "autoUpgradeMinorVersion": true,
    "settings": {},
    "protectedSettings": {}
  }
}
```

<span data-ttu-id="186a3-143">Подробное пошаговое руководство по использованию шаблонов Resource Manager см. в статье [Общие сведения об Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="186a3-143">You can find more detailed walkthrough on using Resource Manager templates by reading [Azure Resource Manager overview](../../azure-resource-manager/resource-group-overview.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="186a3-144">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="186a3-144">Next steps</span></span>
<span data-ttu-id="186a3-145">Возможно, вам потребуется [настроить TCP-порт управляющей программы Docker](https://docs.docker.com/engine/reference/commandline/dockerd/#/bind-docker-to-another-hostport-or-a-unix-socket), [ознакомиться с параметрами безопасности Docker](https://docs.docker.com/engine/security/security/) или развернуть контейнеры с помощью [Docker Compose](https://docs.docker.com/compose/overview/).</span><span class="sxs-lookup"><span data-stu-id="186a3-145">You may wish to [configure the Docker daemon TCP port](https://docs.docker.com/engine/reference/commandline/dockerd/#/bind-docker-to-another-hostport-or-a-unix-socket), understand [Docker security](https://docs.docker.com/engine/security/security/), or deploy containers using [Docker Compose](https://docs.docker.com/compose/overview/).</span></span> <span data-ttu-id="186a3-146">Дополнительные сведения о расширении виртуальных машин Docker для Azure см. в [репозитории GitHub](https://github.com/Azure/azure-docker-extension/).</span><span class="sxs-lookup"><span data-stu-id="186a3-146">For more information on the Azure Docker VM Extension itself, see the [GitHub project](https://github.com/Azure/azure-docker-extension/).</span></span>

<span data-ttu-id="186a3-147">Дополнительные сведения о вариантах развертывания Docker в Azure см. в следующих источниках:</span><span class="sxs-lookup"><span data-stu-id="186a3-147">Read more information about the additional Docker deployment options in Azure:</span></span>

* [<span data-ttu-id="186a3-148">Использование машины Docker с драйвером Azure</span><span class="sxs-lookup"><span data-stu-id="186a3-148">Use Docker Machine with the Azure driver</span></span>](docker-machine.md)  
* <span data-ttu-id="186a3-149">[Приступая к работе с решениями Docker и Compose для определения и запуска многоконтейнерного приложения на виртуальной машине Azure](docker-compose-quickstart.md)</span><span class="sxs-lookup"><span data-stu-id="186a3-149">[Get Started with Docker and Compose to define and run a multi-container application on an Azure virtual machine](docker-compose-quickstart.md).</span></span>
* [<span data-ttu-id="186a3-150">Развертывание кластера службы контейнеров Azure</span><span class="sxs-lookup"><span data-stu-id="186a3-150">Deploy an Azure Container Service cluster</span></span>](../../container-service/dcos-swarm/container-service-deployment.md)

