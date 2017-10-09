---
title: "hello aaaUse расширения виртуальной Машины Azure Docker с hello Azure CLI 1.0 | Документы Microsoft"
description: "Узнайте, как toouse hello tooquickly расширение ВМ Docker и безопасного развертывания в среде Docker в Azure с помощью шаблонов диспетчера ресурсов."
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/11/2017
ms.author: iainfou
ms.openlocfilehash: 2133cdb1af741fe30093910fae5c3b2c91e8d5fe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-docker-environment-in-azure-using-hello-docker-vm-extension-with-hello-azure-cli-10"></a><span data-ttu-id="a843b-103">Создание среды Docker в Azure с помощью расширения виртуальной Машины Docker hello с hello Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="a843b-103">Create a Docker environment in Azure using hello Docker VM extension with hello Azure CLI 1.0</span></span>
<span data-ttu-id="a843b-104">Docker — это популярный контейнер управления и работы с образами платформу, которая позволяет вам tooquickly работы с контейнерами Linux (а также Windows).</span><span class="sxs-lookup"><span data-stu-id="a843b-104">Docker is a popular container management and imaging platform that allows you tooquickly work with containers on Linux (and Windows as well).</span></span> <span data-ttu-id="a843b-105">В Azure существует несколько способов, которые можно развернуть в соответствии с потребностями tooyour Docker.</span><span class="sxs-lookup"><span data-stu-id="a843b-105">In Azure, there are various ways you can deploy Docker according tooyour needs.</span></span> <span data-ttu-id="a843b-106">В этой статье описывается использование расширение ВМ Docker hello и шаблоны Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="a843b-106">This article focuses on using hello Docker VM extension and Azure Resource Manager templates.</span></span> 

<span data-ttu-id="a843b-107">Дополнительные сведения о hello различных способов развертывания, включая использование машины Docker и контейнер служб Azure см. следующие статьи hello:</span><span class="sxs-lookup"><span data-stu-id="a843b-107">For more information about hello different deployment methods, including using Docker Machine and Azure Container Services, see hello following articles:</span></span>

* <span data-ttu-id="a843b-108">прототип tooquickly приложения, можно создать с помощью одного узла Docker [машины Docker](docker-machine.md).</span><span class="sxs-lookup"><span data-stu-id="a843b-108">tooquickly prototype an app, you can create a single Docker host using [Docker Machine](docker-machine.md).</span></span>
* <span data-ttu-id="a843b-109">Для крупных и более стабильные средах, можно использовать расширения виртуальной Машины Azure Docker hello, которое также поддерживает [Docker Compose](https://docs.docker.com/compose/overview/) развертывания toogenerate согласованное контейнера.</span><span class="sxs-lookup"><span data-stu-id="a843b-109">For larger, more stable environments, you can use hello Azure Docker VM extension, which also supports [Docker Compose](https://docs.docker.com/compose/overview/) toogenerate consistent container deployments.</span></span> <span data-ttu-id="a843b-110">Этой статьи описаны с помощью расширения виртуальной Машины Azure Docker hello.</span><span class="sxs-lookup"><span data-stu-id="a843b-110">This article details using hello Azure Docker VM extension.</span></span>
* <span data-ttu-id="a843b-111">toobuild рабочей среде, масштабируемых средах, предоставляющих дополнительные средства планирования и управления развертыванием [кластера с помощью Docker Swarm на контейнер служб Azure](../../container-service/dcos-swarm/container-service-deployment.md).</span><span class="sxs-lookup"><span data-stu-id="a843b-111">toobuild production-ready, scalable environments that provide additional scheduling and management tools, you can deploy a [Docker Swarm cluster on Azure Container Services](../../container-service/dcos-swarm/container-service-deployment.md).</span></span>

## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="a843b-112">Задача hello toocomplete версии CLI</span><span class="sxs-lookup"><span data-stu-id="a843b-112">CLI versions toocomplete hello task</span></span>
<span data-ttu-id="a843b-113">Можно выполнить с помощью одного из следующих версий CLI hello задачу hello.</span><span class="sxs-lookup"><span data-stu-id="a843b-113">You can complete hello task using one of hello following CLI versions:</span></span>

- <span data-ttu-id="a843b-114">[Azure CLI 1.0](#azure-docker-vm-extension-overview) — нашей CLI для hello классический и ресурса управления развертывания моделей (в этой статье)</span><span class="sxs-lookup"><span data-stu-id="a843b-114">[Azure CLI 1.0](#azure-docker-vm-extension-overview) – our CLI for hello classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="a843b-115">[Azure CLI 2.0](dockerextension.md) -нашей нового поколения CLI для модели развертывания hello ресурсов управления</span><span class="sxs-lookup"><span data-stu-id="a843b-115">[Azure CLI 2.0](dockerextension.md) - our next generation CLI for hello resource management deployment model</span></span> 

## <a name="azure-docker-vm-extension-overview"></a><span data-ttu-id="a843b-116">Общие сведения о расширении виртуальных машин Docker для Azure</span><span class="sxs-lookup"><span data-stu-id="a843b-116">Azure Docker VM extension overview</span></span>
<span data-ttu-id="a843b-117">Hello расширение ВМ Docker Azure устанавливает и настраивает управляющую программу Docker hello, клиент Docker и Docker Compose в Linux виртуальной машины (VM).</span><span class="sxs-lookup"><span data-stu-id="a843b-117">hello Azure Docker VM extension installs and configures hello Docker daemon, Docker client, and Docker Compose in your Linux virtual machine (VM).</span></span> <span data-ttu-id="a843b-118">С помощью расширения виртуальной Машины Azure Docker hello, имеют больший контроль и возможностей, чем просто с помощью машины Docker или создании узла Docker hello самостоятельно.</span><span class="sxs-lookup"><span data-stu-id="a843b-118">By using hello Azure Docker VM extension, you have more control and features than simply using Docker Machine or creating hello Docker host yourself.</span></span> <span data-ttu-id="a843b-119">Эти дополнительные возможности, например [Docker Compose](https://docs.docker.com/compose/overview/), подготовить расширение виртуальной Машины Azure Docker hello подходит для более надежной разработчика или рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="a843b-119">These additional features, such as [Docker Compose](https://docs.docker.com/compose/overview/), make hello Azure Docker VM extension suited for more robust developer or production environments.</span></span>

<span data-ttu-id="a843b-120">Шаблоны Azure Resource Manager определить структуру в целом hello среды.</span><span class="sxs-lookup"><span data-stu-id="a843b-120">Azure Resource Manager templates define hello entire structure of your environment.</span></span> <span data-ttu-id="a843b-121">Шаблоны позволяют toocreate и настроить ресурсы, такие как узел Docker hello виртуальных машин, хранилища, средства управления доступом на основе ролей (RBAC) и диагностики.</span><span class="sxs-lookup"><span data-stu-id="a843b-121">Templates allow you toocreate and configure resources such as hello Docker host VMs, storage, Role-Based Access Controls (RBAC), and diagnostics.</span></span> <span data-ttu-id="a843b-122">Можно повторно использовать эти шаблоны toocreate дополнительные развертывания согласованным образом.</span><span class="sxs-lookup"><span data-stu-id="a843b-122">You can reuse these templates toocreate additional deployments in a consistent manner.</span></span> <span data-ttu-id="a843b-123">Дополнительные сведения об Azure Resource Manager и шаблонах см. в статье [Общие сведения об Azure Resource Manager ](../../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="a843b-123">For more information about Azure Resource Manager and templates, see [Resource Manager overview](../../azure-resource-manager/resource-group-overview.md).</span></span> 

## <a name="deploy-a-template-with-hello-azure-docker-vm-extension"></a><span data-ttu-id="a843b-124">Развертывание шаблона с hello расширения виртуальной Машины Azure Docker</span><span class="sxs-lookup"><span data-stu-id="a843b-124">Deploy a template with hello Azure Docker VM extension</span></span>
<span data-ttu-id="a843b-125">Позволяет использовать существующий шаблон краткого руководства toocreate Виртуальной машине Ubuntu, использующий tooinstall расширения виртуальной Машины Azure Docker hello и настройка узла Docker hello.</span><span class="sxs-lookup"><span data-stu-id="a843b-125">Let's use an existing quickstart template toocreate an Ubuntu VM that uses hello Azure Docker VM extension tooinstall and configure hello Docker host.</span></span> <span data-ttu-id="a843b-126">Можно просмотреть здесь шаблон hello: [простое развертывание Виртуальной машине Ubuntu с помощью Docker](https://github.com/Azure/azure-quickstart-templates/tree/master/docker-simple-on-ubuntu).</span><span class="sxs-lookup"><span data-stu-id="a843b-126">You can view hello template here: [Simple deployment of an Ubuntu VM with Docker](https://github.com/Azure/azure-quickstart-templates/tree/master/docker-simple-on-ubuntu).</span></span> 

<span data-ttu-id="a843b-127">Требуется hello [последние Azure CLI](../../cli-install-nodejs.md) установлен и вход с помощью режима диспетчера ресурсов hello следующим образом:</span><span class="sxs-lookup"><span data-stu-id="a843b-127">You need hello [latest Azure CLI](../../cli-install-nodejs.md) installed and logged in using hello Resource Manager mode as follows:</span></span>

```azurecli
azure config mode arm
```

<span data-ttu-id="a843b-128">Развертывание шаблона hello, с помощью hello Azure CLI, указав hello шаблон URI.</span><span class="sxs-lookup"><span data-stu-id="a843b-128">Deploy hello template using hello Azure CLI, specifying hello template URI.</span></span> <span data-ttu-id="a843b-129">Hello следующий пример создает группу ресурсов с именем *myResourceGroup* в hello *westus* расположение.</span><span class="sxs-lookup"><span data-stu-id="a843b-129">hello following example creates a resource group named *myResourceGroup* in hello *westus* location.</span></span> <span data-ttu-id="a843b-130">Укажите собственное имя группы ресурсов и расположение, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="a843b-130">Use your own resource group name and location as follows:</span></span>

```azurecli
azure group create \
    --name myResourceGroup \
    --location westus \
    --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/docker-simple-on-ubuntu/azuredeploy.json
```

<span data-ttu-id="a843b-131">Ответить на запрос tooname hello вашей учетной записи хранилища, укажите имя пользователя и пароль и укажите DNS-имя.</span><span class="sxs-lookup"><span data-stu-id="a843b-131">Answer hello prompts tooname your storage account, provide a username and password, and provide a DNS name.</span></span> <span data-ttu-id="a843b-132">Hello вывода будет примерно toohello следующий пример:</span><span class="sxs-lookup"><span data-stu-id="a843b-132">hello output is similar toohello following example:</span></span>

```azurecli
info:    Executing command group create
+ Getting resource group myResourceGroup
+ Updating resource group myResourceGroup
info:    Updated resource group myResourceGroup
info:    Supply values for hello following parameters
newStorageAccountName: mystorageaccount
adminUsername: azureuser
adminPassword: P@ssword!
dnsNameForPublicIP: mypublicidns
+ Initializing template configurations and parameters
+ Creating a deployment
info:    Created template deployment "azuredeploy"
data:    Id:                  /subscriptions/guid/resourceGroups/myResourceGroup
data:    Name:                myResourceGroup
data:    Location:            westus
data:    Provisioning State:  Succeeded
data:    Tags: null
data:
info:    group create command OK
```

<span data-ttu-id="a843b-133">Hello Azure CLI возвращает строки toohello только через несколько секунд, но узла Docker находится в процессе создания и настроить hello расширение ВМ Docker в Azure.</span><span class="sxs-lookup"><span data-stu-id="a843b-133">hello Azure CLI returns you toohello prompt after only a few seconds, but your Docker host is still being created and configured by hello Azure Docker VM extension.</span></span> <span data-ttu-id="a843b-134">Он занимает несколько минут для развертывания toofinish hello.</span><span class="sxs-lookup"><span data-stu-id="a843b-134">It takes a few minutes for hello deployment toofinish.</span></span> <span data-ttu-id="a843b-135">Для просмотра сведений о состоянии узла Docker hello, с помощью hello `azure vm show` команды.</span><span class="sxs-lookup"><span data-stu-id="a843b-135">You can view details about hello Docker host status using hello `azure vm show` command.</span></span>

<span data-ttu-id="a843b-136">Hello следующий пример проверяет состояние виртуальной Машины с именем hello hello *myDockerVM* (имя по умолчанию на основе шаблона hello hello — не изменять это имя) в группе ресурсов hello с именем *myResourceGroup*.</span><span class="sxs-lookup"><span data-stu-id="a843b-136">hello following example checks hello status of hello VM named *myDockerVM* (hello default name from hello template - don't change this name) in hello resource group named *myResourceGroup*.</span></span> <span data-ttu-id="a843b-137">Введите имя группы ресурсов hello, созданный на предыдущих шага hello hello:</span><span class="sxs-lookup"><span data-stu-id="a843b-137">Enter hello name of hello resource group you created in hello preceding step:</span></span>

```azurecli
azure vm show --resource-group myResourceGroup --name myDockerVM
```

<span data-ttu-id="a843b-138">Здравствуйте, выходные данные hello `azure vm show` команды будет примерно toohello следующий пример:</span><span class="sxs-lookup"><span data-stu-id="a843b-138">hello output of hello `azure vm show` command is similar toohello following example:</span></span>

```azurecli
info:    Executing command vm show
+ Looking up hello VM "myDockerVM"
+ Looking up hello NIC "myVMNicD"
+ Looking up hello public ip "myPublicIPD"
data:    Id                              :/subscriptions/guid/resourceGroups/myresourcegroup/providers/Microsoft.Compute/virtualMachines/MyDockerVM
data:    ProvisioningState               :Succeeded
data:    Name                            :MyDockerVM
data:    Location                        :westus
data:    Type                            :Microsoft.Compute/virtualMachines
[...]
data:
data:    Network Profile:
data:      Network Interfaces:
data:        Network Interface #1:
data:          Primary                   :true
data:          MAC Address               :00-0D-3A-33-D3-95
data:          Provisioning State        :Succeeded
data:          Name                      :myVMNicD
data:          Location                  :westus
data:            Public IP address       :13.91.107.235
data:            FQDN                    :mypublicdns.westus.cloudapp.azure.com
data:
data:    Diagnostics Instance View:
info:    vm show command OK
```

<span data-ttu-id="a843b-139">Верхней hello hello выходных данных вы видите hello **ProvisioningState** из hello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="a843b-139">Near hello top of hello output, you see hello **ProvisioningState** of hello VM.</span></span> <span data-ttu-id="a843b-140">При этом выводится *успешно*, завершения развертывания hello и вы можете toohello SSH виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="a843b-140">When this displays *Succeeded*, hello deployment has finished and you can SSH toohello VM.</span></span>

<span data-ttu-id="a843b-141">Концу hello вывода hello *полное доменное имя* отображает hello полное доменное имя узла Docker.</span><span class="sxs-lookup"><span data-stu-id="a843b-141">Towards hello end of hello output, *FQDN* displays hello fully qualified domain name of your Docker host.</span></span> <span data-ttu-id="a843b-142">Это полное доменное имя является то, что используется узел Docker tooyour tooSSH в hello, оставшиеся шаги.</span><span class="sxs-lookup"><span data-stu-id="a843b-142">This FQDN is what you use tooSSH tooyour Docker host in hello remaining steps.</span></span>

## <a name="deploy-your-first-nginx-container"></a><span data-ttu-id="a843b-143">Развертывание первого контейнера nginx</span><span class="sxs-lookup"><span data-stu-id="a843b-143">Deploy your first nginx container</span></span>
<span data-ttu-id="a843b-144">После завершения развертывания hello SSH tooyour новый узел Docker с локального компьютера.</span><span class="sxs-lookup"><span data-stu-id="a843b-144">Once hello deployment has finished, SSH tooyour new Docker host from your local computer.</span></span> <span data-ttu-id="a843b-145">Введите собственное имя пользователя и полное доменное имя, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="a843b-145">Enter your own username and FQDN as follows:</span></span>

```bash
ssh ops@mypublicdns.westus.cloudapp.azure.com
```

<span data-ttu-id="a843b-146">После входа в toohello узел Docker, запустим контейнер nginx:</span><span class="sxs-lookup"><span data-stu-id="a843b-146">Once logged in toohello Docker host, let's run an nginx container:</span></span>

```bash
sudo docker run -d -p 80:80 nginx
```

<span data-ttu-id="a843b-147">выходные данные Hello выглядят примерно toohello следующий пример, как загружается образ nginx hello и контейнер к работе:</span><span class="sxs-lookup"><span data-stu-id="a843b-147">hello output is similar toohello following example as hello nginx image is downloaded and a container started:</span></span>

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

<span data-ttu-id="a843b-148">Проверьте состояние hello hello контейнеров, работающих на узле Docker следующим образом:</span><span class="sxs-lookup"><span data-stu-id="a843b-148">Check hello status of hello containers running on your Docker host as follows:</span></span>

```bash
sudo docker ps
```

<span data-ttu-id="a843b-149">выходные данные Hello аналогичные toohello следующий пример, отображение этого контейнера nginx hello запущена и TCP-порты 80 и 443 и пересылки:</span><span class="sxs-lookup"><span data-stu-id="a843b-149">hello output is similar toohello following example, showing that hello nginx container is running and TCP ports 80 and 443 and being forwarded:</span></span>

```bash
CONTAINER ID        IMAGE               COMMAND                  CREATED              STATUS              PORTS                         NAMES
b6ed109fb743        nginx               "nginx -g 'daemon off"   About a minute ago   Up About a minute   0.0.0.0:80->80/tcp, 443/tcp   adoring_payne
```

<span data-ttu-id="a843b-150">toosee контейнера в действие, откройте веб-обозреватель и введите полное ДОМЕННОЕ имя узла Docker hello:</span><span class="sxs-lookup"><span data-stu-id="a843b-150">toosee your container in action, open up a web browser and enter hello FQDN name of your Docker host:</span></span>

![Запущенный контейнер nginx](./media/dockerextension/nginxrunning.png)

## <a name="azure-docker-vm-extension-template-reference"></a><span data-ttu-id="a843b-152">Пример шаблона расширения виртуальной машины Docker для Azure</span><span class="sxs-lookup"><span data-stu-id="a843b-152">Azure Docker VM extension template reference</span></span>
<span data-ttu-id="a843b-153">Hello в предыдущем примере существующий шаблон краткого руководства.</span><span class="sxs-lookup"><span data-stu-id="a843b-153">hello previous example uses an existing quickstart template.</span></span> <span data-ttu-id="a843b-154">Можно также развернуть hello расширения виртуальной Машины Azure Docker с помощью собственных шаблонов диспетчера ресурсов.</span><span class="sxs-lookup"><span data-stu-id="a843b-154">You can also deploy hello Azure Docker VM extension with your own Resource Manager templates.</span></span> <span data-ttu-id="a843b-155">toodo таким образом, добавить hello следующие шаблоны диспетчера ресурсов tooyour, определение hello *vmName* вашей виртуальной машины соответствующим образом:</span><span class="sxs-lookup"><span data-stu-id="a843b-155">toodo so, add hello following tooyour Resource Manager templates, defining hello *vmName* of your VM appropriately:</span></span>

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
    "typeHandlerVersion": "1.1",
    "autoUpgradeMinorVersion": true,
    "settings": {},
    "protectedSettings": {}
  }
}
```

<span data-ttu-id="a843b-156">Подробное пошаговое руководство по использованию шаблонов Resource Manager см. в статье [Общие сведения об Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="a843b-156">You can find more detailed walkthrough on using Resource Manager templates by reading [Azure Resource Manager overview](../../azure-resource-manager/resource-group-overview.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="a843b-157">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="a843b-157">Next steps</span></span>
<span data-ttu-id="a843b-158">Вы можете слишком[настроить hello Docker daemon TCP-порт](https://docs.docker.com/engine/reference/commandline/dockerd/#/bind-docker-to-another-hostport-or-a-unix-socket), понять [безопасности Docker](https://docs.docker.com/engine/security/security/), или развернуть контейнеры с помощью [Docker Compose](https://docs.docker.com/compose/overview/).</span><span class="sxs-lookup"><span data-stu-id="a843b-158">You may wish too[configure hello Docker daemon TCP port](https://docs.docker.com/engine/reference/commandline/dockerd/#/bind-docker-to-another-hostport-or-a-unix-socket), understand [Docker security](https://docs.docker.com/engine/security/security/), or deploy containers using [Docker Compose](https://docs.docker.com/compose/overview/).</span></span> <span data-ttu-id="a843b-159">Дополнительные сведения о hello расширение ВМ Docker Azure сама разделе hello [GitHub проекта](https://github.com/Azure/azure-docker-extension/).</span><span class="sxs-lookup"><span data-stu-id="a843b-159">For more information on hello Azure Docker VM Extension itself, see hello [GitHub project](https://github.com/Azure/azure-docker-extension/).</span></span>

<span data-ttu-id="a843b-160">Прочтите Дополнительные сведения о дополнительных параметрах развертывания Docker hello в Azure:</span><span class="sxs-lookup"><span data-stu-id="a843b-160">Read more information about hello additional Docker deployment options in Azure:</span></span>

* [<span data-ttu-id="a843b-161">Использовать компьютер Docker с hello Azure драйвера</span><span class="sxs-lookup"><span data-stu-id="a843b-161">Use Docker Machine with hello Azure driver</span></span>](docker-machine.md)  
* <span data-ttu-id="a843b-162">[Начало работы с Docker и составлять toodefine и запустите приложение контейнера несколькими на виртуальной машине Azure](docker-compose-quickstart.md).</span><span class="sxs-lookup"><span data-stu-id="a843b-162">[Get Started with Docker and Compose toodefine and run a multi-container application on an Azure virtual machine](docker-compose-quickstart.md).</span></span>
* [<span data-ttu-id="a843b-163">Развертывание кластера службы контейнеров Azure</span><span class="sxs-lookup"><span data-stu-id="a843b-163">Deploy an Azure Container Service cluster</span></span>](../../container-service/dcos-swarm/container-service-deployment.md)

