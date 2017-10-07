---
title: "hello aaaUse расширения виртуальной Машины Azure Docker | Документы Microsoft"
description: "Узнайте, как toouse hello tooquickly расширение ВМ Docker и безопасное развертывание среды Docker в Azure с помощью шаблонов диспетчера ресурсов и hello Azure CLI 2.0"
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
ms.openlocfilehash: 8e43adc594192773466ccd2d3e455105f14c1a61
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-docker-environment-in-azure-using-hello-docker-vm-extension"></a><span data-ttu-id="953b2-103">Создание среды Docker в Azure с помощью расширения виртуальной Машины Docker hello</span><span class="sxs-lookup"><span data-stu-id="953b2-103">Create a Docker environment in Azure using hello Docker VM extension</span></span>
<span data-ttu-id="953b2-104">Docker — это популярный контейнер управления и работы с образами платформу, которая позволяет tooquickly работы с контейнерами в Linux.</span><span class="sxs-lookup"><span data-stu-id="953b2-104">Docker is a popular container management and imaging platform that allows you tooquickly work with containers on Linux.</span></span> <span data-ttu-id="953b2-105">В Azure существует несколько способов, которые можно развернуть в соответствии с потребностями tooyour Docker.</span><span class="sxs-lookup"><span data-stu-id="953b2-105">In Azure, there are various ways you can deploy Docker according tooyour needs.</span></span> <span data-ttu-id="953b2-106">В этой статье описывается использование расширение ВМ Docker hello и шаблоны Azure Resource Manager с hello Azure CLI 2.0.</span><span class="sxs-lookup"><span data-stu-id="953b2-106">This article focuses on using hello Docker VM extension and Azure Resource Manager templates with hello Azure CLI 2.0.</span></span> <span data-ttu-id="953b2-107">Можно также выполнить следующие действия с hello [Azure CLI 1.0](dockerextension-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="953b2-107">You can also perform these steps with hello [Azure CLI 1.0](dockerextension-nodejs.md).</span></span>

## <a name="azure-docker-vm-extension-overview"></a><span data-ttu-id="953b2-108">Общие сведения о расширении виртуальных машин Docker для Azure</span><span class="sxs-lookup"><span data-stu-id="953b2-108">Azure Docker VM extension overview</span></span>
<span data-ttu-id="953b2-109">Hello расширение ВМ Docker Azure устанавливает и настраивает управляющую программу Docker hello, клиент Docker и Docker Compose в Linux виртуальной машины (VM).</span><span class="sxs-lookup"><span data-stu-id="953b2-109">hello Azure Docker VM extension installs and configures hello Docker daemon, Docker client, and Docker Compose in your Linux virtual machine (VM).</span></span> <span data-ttu-id="953b2-110">С помощью расширения виртуальной Машины Azure Docker hello, имеют больший контроль и возможностей, чем просто с помощью машины Docker или создании узла Docker hello самостоятельно.</span><span class="sxs-lookup"><span data-stu-id="953b2-110">By using hello Azure Docker VM extension, you have more control and features than simply using Docker Machine or creating hello Docker host yourself.</span></span> <span data-ttu-id="953b2-111">Эти дополнительные возможности, например [Docker Compose](https://docs.docker.com/compose/overview/), подготовить расширение виртуальной Машины Azure Docker hello подходит для более надежной разработчика или рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="953b2-111">These additional features, such as [Docker Compose](https://docs.docker.com/compose/overview/), make hello Azure Docker VM extension suited for more robust developer or production environments.</span></span>

<span data-ttu-id="953b2-112">Дополнительные сведения о hello различных способов развертывания, включая использование машины Docker и контейнер служб Azure см. следующие статьи hello:</span><span class="sxs-lookup"><span data-stu-id="953b2-112">For more information about hello different deployment methods, including using Docker Machine and Azure Container Services, see hello following articles:</span></span>

* <span data-ttu-id="953b2-113">прототип tooquickly приложения, можно создать с помощью одного узла Docker [машины Docker](docker-machine.md).</span><span class="sxs-lookup"><span data-stu-id="953b2-113">tooquickly prototype an app, you can create a single Docker host using [Docker Machine](docker-machine.md).</span></span>
* <span data-ttu-id="953b2-114">toobuild рабочей среде, масштабируемых средах, предоставляющих дополнительные средства планирования и управления развертыванием [кластера с помощью Docker Swarm на контейнер служб Azure](../../container-service/dcos-swarm/container-service-deployment.md).</span><span class="sxs-lookup"><span data-stu-id="953b2-114">toobuild production-ready, scalable environments that provide additional scheduling and management tools, you can deploy a [Docker Swarm cluster on Azure Container Services](../../container-service/dcos-swarm/container-service-deployment.md).</span></span>

## <a name="deploy-a-template-with-hello-azure-docker-vm-extension"></a><span data-ttu-id="953b2-115">Развертывание шаблона с hello расширения виртуальной Машины Azure Docker</span><span class="sxs-lookup"><span data-stu-id="953b2-115">Deploy a template with hello Azure Docker VM extension</span></span>
<span data-ttu-id="953b2-116">Позволяет использовать существующий шаблон краткого руководства toocreate Виртуальной машине Ubuntu, использующий tooinstall расширения виртуальной Машины Azure Docker hello и настройка узла Docker hello.</span><span class="sxs-lookup"><span data-stu-id="953b2-116">Let's use an existing quickstart template toocreate an Ubuntu VM that uses hello Azure Docker VM extension tooinstall and configure hello Docker host.</span></span> <span data-ttu-id="953b2-117">Можно просмотреть здесь шаблон hello: [простое развертывание Виртуальной машине Ubuntu с помощью Docker](https://github.com/Azure/azure-quickstart-templates/tree/master/docker-simple-on-ubuntu).</span><span class="sxs-lookup"><span data-stu-id="953b2-117">You can view hello template here: [Simple deployment of an Ubuntu VM with Docker](https://github.com/Azure/azure-quickstart-templates/tree/master/docker-simple-on-ubuntu).</span></span> <span data-ttu-id="953b2-118">Hello требуется последняя версия [Azure CLI 2.0](/cli/azure/install-az-cli2) установлен и войти в систему с учетной записью Azure tooan [входа az](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="953b2-118">You need hello latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in tooan Azure account using [az login](/cli/azure/#login).</span></span>

<span data-ttu-id="953b2-119">Сначала создайте группу ресурсов с помощью команды [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="953b2-119">First, create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="953b2-120">Hello следующий пример создает группу ресурсов с именем *myResourceGroup* в hello *westus* расположение:</span><span class="sxs-lookup"><span data-stu-id="953b2-120">hello following example creates a resource group named *myResourceGroup* in hello *westus* location:</span></span>

```azurecli
az group create --name myResourceGroup --location westus
```

<span data-ttu-id="953b2-121">Затем разверните виртуальную Машину с [создания развертывания группы az](/cli/azure/group/deployment#create) , включает в себя расширение виртуальной Машины Azure Docker hello из [этого шаблона диспетчера ресурсов Azure на GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/docker-simple-on-ubuntu).</span><span class="sxs-lookup"><span data-stu-id="953b2-121">Next, deploy a VM with [az group deployment create](/cli/azure/group/deployment#create) that includes hello Azure Docker VM extension from [this Azure Resource Manager template on GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/docker-simple-on-ubuntu).</span></span> <span data-ttu-id="953b2-122">Укажите собственные значения для параметров *newStorageAccountName*, *adminUsername*, *adminPassword* и *dnsNameForPublicIP*, как показано ниже:</span><span class="sxs-lookup"><span data-stu-id="953b2-122">Provide your own values for *newStorageAccountName*, *adminUsername*, *adminPassword*, and *dnsNameForPublicIP* as follows:</span></span>

```azurecli
az group deployment create --resource-group myResourceGroup \
  --parameters '{"newStorageAccountName": {"value": "mystorageaccount"},
    "adminUsername": {"value": "azureuser"},
    "adminPassword": {"value": "P@ssw0rd!"},
    "dnsNameForPublicIP": {"value": "mypublicdns"}}' \
  --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/docker-simple-on-ubuntu/azuredeploy.json
```

<span data-ttu-id="953b2-123">Он занимает несколько минут для развертывания toofinish hello.</span><span class="sxs-lookup"><span data-stu-id="953b2-123">It takes a few minutes for hello deployment toofinish.</span></span> <span data-ttu-id="953b2-124">После завершения развертывания hello [переместить шаг toonext](#deploy-your-first-nginx-container) tooSSH tooyour виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="953b2-124">Once hello deployment is finished, [move toonext step](#deploy-your-first-nginx-container) tooSSH tooyour VM.</span></span> 

<span data-ttu-id="953b2-125">При необходимости строки toohello tooinstead возвращаемого элемента управления и позволяют hello развертывания по-прежнему в фоновом режиме hello, добавьте hello `--no-wait` флаг toohello предшествующий команды.</span><span class="sxs-lookup"><span data-stu-id="953b2-125">Optionally, tooinstead return control toohello prompt and let hello deployment continue in hello background, add hello `--no-wait` flag toohello preceding command.</span></span> <span data-ttu-id="953b2-126">Этот процесс позволяет tooperform другие действия в hello CLI во время развертывания hello продолжается несколько минут.</span><span class="sxs-lookup"><span data-stu-id="953b2-126">This process allows you tooperform other work in hello CLI while hello deployment continues for a few minutes.</span></span> 

<span data-ttu-id="953b2-127">Затем можно просмотреть подробные сведения о состоянии узла Docker hello с [Показать ВМ az](/cli/azure/vm#show).</span><span class="sxs-lookup"><span data-stu-id="953b2-127">You can then view details about hello Docker host status with [az vm show](/cli/azure/vm#show).</span></span> <span data-ttu-id="953b2-128">Hello следующий пример проверяет состояние виртуальной Машины с именем hello hello *myDockerVM* (имя по умолчанию на основе шаблона hello hello — не изменять это имя) в группе ресурсов hello с именем *myResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="953b2-128">hello following example checks hello status of hello VM named *myDockerVM* (hello default name from hello template - don't change this name) in hello resource group named *myResourceGroup*:</span></span>

```azurecli
az vm show \
    --resource-group myResourceGroup \
    --name myDockerVM \
    --query [provisioningState] \
    --output tsv
```

<span data-ttu-id="953b2-129">Если эта команда возвращает *успешно*, завершения развертывания hello и вы можете toohello SSH виртуальной Машины в даст hello.</span><span class="sxs-lookup"><span data-stu-id="953b2-129">When this command returns *Succeeded*, hello deployment has finished and you can SSH toohello VM in hello following step.</span></span>

## <a name="deploy-your-first-nginx-container"></a><span data-ttu-id="953b2-130">Развертывание первого контейнера nginx</span><span class="sxs-lookup"><span data-stu-id="953b2-130">Deploy your first nginx container</span></span>
<span data-ttu-id="953b2-131">использовать сведения о tooview виртуальной машины, включая hello DNS-имя `az vm show -g myResourceGroup -n myDockerVM -d --query [fqdns] -o tsv`.</span><span class="sxs-lookup"><span data-stu-id="953b2-131">tooview details of your VM, including hello DNS name, use `az vm show -g myResourceGroup -n myDockerVM -d --query [fqdns] -o tsv`.</span></span> <span data-ttu-id="953b2-132">SSH tooyour новый Docker размещения с локального компьютера следующим образом:</span><span class="sxs-lookup"><span data-stu-id="953b2-132">SSH tooyour new Docker host from your local computer as follows:</span></span>

```bash
ssh azureuser@mypublicdns.westus.cloudapp.azure.com
```

<span data-ttu-id="953b2-133">После входа в toohello узел Docker, запустим контейнер nginx:</span><span class="sxs-lookup"><span data-stu-id="953b2-133">Once logged in toohello Docker host, let's run an nginx container:</span></span>

```bash
sudo docker run -d -p 80:80 nginx
```

<span data-ttu-id="953b2-134">выходные данные Hello выглядят примерно toohello следующий пример, как загружается образ nginx hello и контейнер к работе:</span><span class="sxs-lookup"><span data-stu-id="953b2-134">hello output is similar toohello following example as hello nginx image is downloaded and a container started:</span></span>

```bash
Unable toofind image 'nginx:latest' locally
latest: Pulling from library/nginx
efd26ecc9548: Pull complete
a3ed95caeb02: Pull complete
a48df1751a97: Pull complete
8ddc2d7beb91: Pull complete
Digest: sha256:2ca2638e55319b7bc0c7d028209ea69b1368e95b01383e66dfe7e4f43780926d
Status: Downloaded newer image for nginx:latest
b6ed109fb743a762ff21a4606dd38d3e5d35aff43fa7f12e8d4ed1d920b0cd74
```

<span data-ttu-id="953b2-135">Проверьте состояние hello hello контейнеров, работающих на узле Docker следующим образом:</span><span class="sxs-lookup"><span data-stu-id="953b2-135">Check hello status of hello containers running on your Docker host as follows:</span></span>

```bash
sudo docker ps
```

<span data-ttu-id="953b2-136">выходные данные Hello аналогичные toohello следующий пример, отображение этого контейнера nginx hello запущена и TCP-порты 80 и 443 и пересылки:</span><span class="sxs-lookup"><span data-stu-id="953b2-136">hello output is similar toohello following example, showing that hello nginx container is running and TCP ports 80 and 443 and being forwarded:</span></span>

```bash
CONTAINER ID        IMAGE               COMMAND                  CREATED              STATUS              PORTS                         NAMES
b6ed109fb743        nginx               "nginx -g 'daemon off"   About a minute ago   Up About a minute   0.0.0.0:80->80/tcp, 443/tcp   adoring_payne
```

<span data-ttu-id="953b2-137">toosee контейнера в действие, откройте веб-обозреватель и введите hello DNS-имя узла Docker:</span><span class="sxs-lookup"><span data-stu-id="953b2-137">toosee your container in action, open up a web browser and enter hello DNS name of your Docker host:</span></span>

![Запущенный контейнер nginx](./media/dockerextension/nginxrunning.png)

## <a name="azure-docker-vm-extension-template-reference"></a><span data-ttu-id="953b2-139">Пример шаблона расширения виртуальной машины Docker для Azure</span><span class="sxs-lookup"><span data-stu-id="953b2-139">Azure Docker VM extension template reference</span></span>
<span data-ttu-id="953b2-140">Hello в предыдущем примере существующий шаблон краткого руководства.</span><span class="sxs-lookup"><span data-stu-id="953b2-140">hello previous example uses an existing quickstart template.</span></span> <span data-ttu-id="953b2-141">Можно также развернуть hello расширения виртуальной Машины Azure Docker с помощью собственных шаблонов диспетчера ресурсов.</span><span class="sxs-lookup"><span data-stu-id="953b2-141">You can also deploy hello Azure Docker VM extension with your own Resource Manager templates.</span></span> <span data-ttu-id="953b2-142">toodo таким образом, добавить hello следующие шаблоны диспетчера ресурсов tooyour, определение hello `vmName` вашей виртуальной машины соответствующим образом:</span><span class="sxs-lookup"><span data-stu-id="953b2-142">toodo so, add hello following tooyour Resource Manager templates, defining hello `vmName` of your VM appropriately:</span></span>

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

<span data-ttu-id="953b2-143">Подробное пошаговое руководство по использованию шаблонов Resource Manager см. в статье [Общие сведения об Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="953b2-143">You can find more detailed walkthrough on using Resource Manager templates by reading [Azure Resource Manager overview](../../azure-resource-manager/resource-group-overview.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="953b2-144">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="953b2-144">Next steps</span></span>
<span data-ttu-id="953b2-145">Вы можете слишком[настроить hello Docker daemon TCP-порт](https://docs.docker.com/engine/reference/commandline/dockerd/#/bind-docker-to-another-hostport-or-a-unix-socket), понять [безопасности Docker](https://docs.docker.com/engine/security/security/), или развернуть контейнеры с помощью [Docker Compose](https://docs.docker.com/compose/overview/).</span><span class="sxs-lookup"><span data-stu-id="953b2-145">You may wish too[configure hello Docker daemon TCP port](https://docs.docker.com/engine/reference/commandline/dockerd/#/bind-docker-to-another-hostport-or-a-unix-socket), understand [Docker security](https://docs.docker.com/engine/security/security/), or deploy containers using [Docker Compose](https://docs.docker.com/compose/overview/).</span></span> <span data-ttu-id="953b2-146">Дополнительные сведения о hello расширение ВМ Docker Azure сама разделе hello [GitHub проекта](https://github.com/Azure/azure-docker-extension/).</span><span class="sxs-lookup"><span data-stu-id="953b2-146">For more information on hello Azure Docker VM Extension itself, see hello [GitHub project](https://github.com/Azure/azure-docker-extension/).</span></span>

<span data-ttu-id="953b2-147">Прочтите Дополнительные сведения о дополнительных параметрах развертывания Docker hello в Azure:</span><span class="sxs-lookup"><span data-stu-id="953b2-147">Read more information about hello additional Docker deployment options in Azure:</span></span>

* [<span data-ttu-id="953b2-148">Использовать компьютер Docker с hello Azure драйвера</span><span class="sxs-lookup"><span data-stu-id="953b2-148">Use Docker Machine with hello Azure driver</span></span>](docker-machine.md)  
* <span data-ttu-id="953b2-149">[Начало работы с Docker и составлять toodefine и запустите приложение контейнера несколькими на виртуальной машине Azure](docker-compose-quickstart.md).</span><span class="sxs-lookup"><span data-stu-id="953b2-149">[Get Started with Docker and Compose toodefine and run a multi-container application on an Azure virtual machine](docker-compose-quickstart.md).</span></span>
* [<span data-ttu-id="953b2-150">Развертывание кластера службы контейнеров Azure</span><span class="sxs-lookup"><span data-stu-id="953b2-150">Deploy an Azure Container Service cluster</span></span>](../../container-service/dcos-swarm/container-service-deployment.md)

