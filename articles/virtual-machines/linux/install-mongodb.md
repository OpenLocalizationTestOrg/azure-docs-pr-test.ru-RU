---
title: "aaaInstall MongoDB на виртуальной Машине Linux с hello Azure CLI | Документы Microsoft"
description: "Узнайте, как tooinstall и настройте MongoDB на hello iusing виртуальной машине Linux Azure CLI 2.0"
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
ms.assetid: 3f55b546-86df-4442-9ef4-8a25fae7b96e
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 06/23/2017
ms.author: iainfou
ms.openlocfilehash: 97a4d9913f0eeaf7b8bf15d7fc81befe538cdc8d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooinstall-and-configure-mongodb-on-a-linux-vm"></a><span data-ttu-id="065ca-103">Как tooinstall и настройте MongoDB на виртуальной Машине Linux</span><span class="sxs-lookup"><span data-stu-id="065ca-103">How tooinstall and configure MongoDB on a Linux VM</span></span>
<span data-ttu-id="065ca-104">[MongoDB](http://www.mongodb.org) — это популярная высокопроизводительная база данных NoSQL с открытым кодом.</span><span class="sxs-lookup"><span data-stu-id="065ca-104">[MongoDB](http://www.mongodb.org) is a popular open-source, high-performance NoSQL database.</span></span> <span data-ttu-id="065ca-105">В этой статье показано, как tooinstall и настройте на виртуальной Машине Linux с hello Azure CLI 2.0 MongoDB.</span><span class="sxs-lookup"><span data-stu-id="065ca-105">This article shows you how tooinstall and configure MongoDB on a Linux VM with hello Azure CLI 2.0.</span></span> <span data-ttu-id="065ca-106">Можно также выполнить следующие действия с hello [Azure CLI 1.0](install-mongodb-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="065ca-106">You can also perform these steps with hello [Azure CLI 1.0](install-mongodb-nodejs.md).</span></span> <span data-ttu-id="065ca-107">Изучив представленные примеры, вы узнаете, как:</span><span class="sxs-lookup"><span data-stu-id="065ca-107">Examples are shown that detail how to:</span></span>

* <span data-ttu-id="065ca-108">[установить и настроить базовый экземпляр MongoDB вручную](#manually-install-and-configure-mongodb-on-a-vm);</span><span class="sxs-lookup"><span data-stu-id="065ca-108">[Manually install and configure a basic MongoDB instance](#manually-install-and-configure-mongodb-on-a-vm)</span></span>
* <span data-ttu-id="065ca-109">[создать базовый экземпляр MongoDB на основе шаблона Resource Manager](#create-basic-mongodb-instance-on-centos-using-a-template);</span><span class="sxs-lookup"><span data-stu-id="065ca-109">[Create a basic MongoDB instance using a Resource Manager template](#create-basic-mongodb-instance-on-centos-using-a-template)</span></span>
* <span data-ttu-id="065ca-110">[создать сложный сегментированный кластер MongoDB с набором реплик с использованием шаблона Resource Manager](#create-a-complex-mongodb-sharded-cluster-on-centos-using-a-template).</span><span class="sxs-lookup"><span data-stu-id="065ca-110">[Create a complex MongoDB sharded cluster with replica sets using a Resource Manager template](#create-a-complex-mongodb-sharded-cluster-on-centos-using-a-template)</span></span>


## <a name="manually-install-and-configure-mongodb-on-a-vm"></a><span data-ttu-id="065ca-111">Установка и настройка MongoDB на виртуальной машине вручную</span><span class="sxs-lookup"><span data-stu-id="065ca-111">Manually install and configure MongoDB on a VM</span></span>
<span data-ttu-id="065ca-112">База данных MongoDB [содержит инструкции по установке](https://docs.mongodb.com/manual/administration/install-on-linux/) для дистрибутивов Linux, в том числе Red Hat, CentOS, SUSE, Ubuntu и Debian.</span><span class="sxs-lookup"><span data-stu-id="065ca-112">MongoDB [provide installation instructions](https://docs.mongodb.com/manual/administration/install-on-linux/) for Linux distros including Red Hat / CentOS, SUSE, Ubuntu, and Debian.</span></span> <span data-ttu-id="065ca-113">Hello следующий пример создает *CentOS* виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="065ca-113">hello following example creates a *CentOS* VM.</span></span> <span data-ttu-id="065ca-114">toocreate этой среды hello требуется последняя версия [Azure CLI 2.0](/cli/azure/install-az-cli2) установлен и войти в систему с учетной записью Azure tooan [входа az](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="065ca-114">toocreate this environment, you need hello latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in tooan Azure account using [az login](/cli/azure/#login).</span></span>

<span data-ttu-id="065ca-115">Создайте группу ресурсов с помощью команды [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="065ca-115">Create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="065ca-116">Hello следующий пример создает группу ресурсов с именем *myResourceGroup* в hello *eastus* расположение:</span><span class="sxs-lookup"><span data-stu-id="065ca-116">hello following example creates a resource group named *myResourceGroup* in hello *eastus* location:</span></span>

```azurecli
az group create --name myResourceGroup --location eastus
```

<span data-ttu-id="065ca-117">Создайте виртуальную машину с помощью команды [az vm create](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="065ca-117">Create a VM with [az vm create](/cli/azure/vm#create).</span></span> <span data-ttu-id="065ca-118">Hello следующий пример создает Виртуальную машину с именем *myVM* с именем пользователя *azureuser* с использованием открытого ключа проверки подлинности SSH</span><span class="sxs-lookup"><span data-stu-id="065ca-118">hello following example creates a VM named *myVM* with a user named *azureuser* using SSH public key authentication</span></span>

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image CentOS \
    --admin-username azureuser \
    --generate-ssh-keys
```

<span data-ttu-id="065ca-119">Toohello SSH виртуальную Машину с помощью имени пользователя и hello `publicIpAddress` перечисленные в выходных данных hello из предыдущего шага hello:</span><span class="sxs-lookup"><span data-stu-id="065ca-119">SSH toohello VM using your own username and hello `publicIpAddress` listed in hello output from hello previous step:</span></span>

```bash
ssh azureuser@<publicIpAddress>
```

<span data-ttu-id="065ca-120">создать источник установки hello tooadd MongoDB, **yum** файл репозитория следующим образом:</span><span class="sxs-lookup"><span data-stu-id="065ca-120">tooadd hello installation sources for MongoDB, create a **yum** repository file as follows:</span></span>

```bash
sudo touch /etc/yum.repos.d/mongodb-org-3.4.repo
```

<span data-ttu-id="065ca-121">Откройте для редактирования файл репозитория hello MongoDB.</span><span class="sxs-lookup"><span data-stu-id="065ca-121">Open hello MongoDB repo file for editing.</span></span> <span data-ttu-id="065ca-122">Добавьте следующие строки hello:</span><span class="sxs-lookup"><span data-stu-id="065ca-122">Add hello following lines:</span></span>

```sh
[mongodb-org-3.4]
name=MongoDB Repository
baseurl=https://repo.mongodb.org/yum/redhat/$releasever/mongodb-org/3.4/x86_64/
gpgcheck=1
enabled=1
gpgkey=https://www.mongodb.org/static/pgp/server-3.4.asc
```

<span data-ttu-id="065ca-123">Установите MongoDB, используя **yum**, как показано ниже:</span><span class="sxs-lookup"><span data-stu-id="065ca-123">Install MongoDB using **yum** as follows:</span></span>

```bash
sudo yum install -y mongodb-org
```

<span data-ttu-id="065ca-124">По умолчанию в образах CentOS принудительно используется SELinux. Это препятствует доступу к MongoDB.</span><span class="sxs-lookup"><span data-stu-id="065ca-124">By default, SELinux is enforced on CentOS images that prevents you from accessing MongoDB.</span></span> <span data-ttu-id="065ca-125">Установка средств управления политиками и настройка SELinux tooallow MongoDB toooperate на порт TCP по умолчанию 27017 следующим образом:</span><span class="sxs-lookup"><span data-stu-id="065ca-125">Install policy management tools and configure SELinux tooallow MongoDB toooperate on its default TCP port 27017 as follows:</span></span>

```bash
sudo yum install -y policycoreutils-python
sudo semanage port -a -t mongod_port_t -p tcp 27017
```

<span data-ttu-id="065ca-126">Запуск службы MongoDB hello следующим образом:</span><span class="sxs-lookup"><span data-stu-id="065ca-126">Start hello MongoDB service as follows:</span></span>

```bash
sudo service mongod start
```

<span data-ttu-id="065ca-127">Проверка установки MongoDB hello при подключении с использованием локального hello `mongo` клиента:</span><span class="sxs-lookup"><span data-stu-id="065ca-127">Verify hello MongoDB installation by connecting using hello local `mongo` client:</span></span>

```bash
mongo
```

<span data-ttu-id="065ca-128">Теперь можно проверьте экземпляр MongoDB hello, добавив некоторые данные и затем найти:</span><span class="sxs-lookup"><span data-stu-id="065ca-128">Now test hello MongoDB instance by adding some data and then searching:</span></span>

```sh
> db
test
> db.foo.insert( { a : 1 } )  
> db.foo.find()  
{ "_id" : ObjectId("57ec477cd639891710b90727"), "a" : 1 }
> exit
```

<span data-ttu-id="065ca-129">При необходимости настройте MongoDB toostart автоматически во время перезагрузки системы.</span><span class="sxs-lookup"><span data-stu-id="065ca-129">If desired, configure MongoDB toostart automatically during a system reboot:</span></span>

```bash
sudo chkconfig mongod on
```


## <a name="create-basic-mongodb-instance-on-centos-using-a-template"></a><span data-ttu-id="065ca-130">Создание базового экземпляра MongoDB на виртуальной машине CentOS с использованием шаблона</span><span class="sxs-lookup"><span data-stu-id="065ca-130">Create basic MongoDB instance on CentOS using a template</span></span>
<span data-ttu-id="065ca-131">Можно создать базовый экземпляр MongoDB на одной виртуальной Машины CentOS с помощью hello следующую Azure примеры использования шаблона из GitHub.</span><span class="sxs-lookup"><span data-stu-id="065ca-131">You can create a basic MongoDB instance on a single CentOS VM using hello following Azure quickstart template from GitHub.</span></span> <span data-ttu-id="065ca-132">Этот шаблон использует расширение hello пользовательский сценарий для Linux tooadd **yum** tooyour репозитория вновь созданные ВМ CentOS, а затем установите MongoDB.</span><span class="sxs-lookup"><span data-stu-id="065ca-132">This template uses hello Custom Script extension for Linux tooadd a **yum** repository tooyour newly created CentOS VM and then install MongoDB.</span></span>

* <span data-ttu-id="065ca-133">[Базовый экземпляр MongoDB на виртуальной машине CentOS](https://github.com/Azure/azure-quickstart-templates/tree/master/mongodb-on-centos): https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/mongodb-on-centos/azuredeploy.json.</span><span class="sxs-lookup"><span data-stu-id="065ca-133">[Basic MongoDB instance on CentOS](https://github.com/Azure/azure-quickstart-templates/tree/master/mongodb-on-centos) - https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/mongodb-on-centos/azuredeploy.json</span></span>

<span data-ttu-id="065ca-134">toocreate этой среды hello требуется последняя версия [Azure CLI 2.0](/cli/azure/install-az-cli2) установлен и войти в систему с учетной записью Azure tooan [входа az](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="065ca-134">toocreate this environment, you need hello latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in tooan Azure account using [az login](/cli/azure/#login).</span></span> <span data-ttu-id="065ca-135">Сначала создайте группу ресурсов с помощью команды [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="065ca-135">First, create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="065ca-136">Hello следующий пример создает группу ресурсов с именем *myResourceGroup* в hello *eastus* расположение:</span><span class="sxs-lookup"><span data-stu-id="065ca-136">hello following example creates a resource group named *myResourceGroup* in hello *eastus* location:</span></span>

```azurecli
az group create --name myResourceGroup --location eastus
```

<span data-ttu-id="065ca-137">Затем разверните шаблон hello MongoDB с [создания развертывания группы az](/cli/azure/group/deployment#create).</span><span class="sxs-lookup"><span data-stu-id="065ca-137">Next, deploy hello MongoDB template with [az group deployment create](/cli/azure/group/deployment#create).</span></span> <span data-ttu-id="065ca-138">Определите необходимые имена и размеры ресурсов, например *newStorageAccountName*, *virtualNetworkName* и *vmSize*:</span><span class="sxs-lookup"><span data-stu-id="065ca-138">Define your own resource names and sizes where needed such as for *newStorageAccountName*, *virtualNetworkName*, and *vmSize*:</span></span>

```azurecli
az group deployment create --resource-group myResourceGroup \
  --parameters '{"newStorageAccountName": {"value": "mystorageaccount"},
    "adminUsername": {"value": "azureuser"},
    "adminPassword": {"value": "P@ssw0rd!"},
    "dnsNameForPublicIP": {"value": "mypublicdns"},
    "virtualNetworkName": {"value": "myVnet"},
    "vmSize": {"value": "Standard_DS2_v2"},
    "vmName": {"value": "myVM"},
    "publicIPAddressName": {"value": "myPublicIP"},
    "nicName": {"value": "myNic"}}' \
  --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/mongodb-on-centos/azuredeploy.json
```

<span data-ttu-id="065ca-139">Вход toohello виртуальной Машины с помощью hello общедоступный адрес DNS вашей виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="065ca-139">Log on toohello VM using hello public DNS address of your VM.</span></span> <span data-ttu-id="065ca-140">Можно просмотреть hello общедоступный адрес DNS с [Показать ВМ az](/cli/azure/vm#show):</span><span class="sxs-lookup"><span data-stu-id="065ca-140">You can view hello public DNS address with [az vm show](/cli/azure/vm#show):</span></span>

```azurecli
az vm show -g myResourceGroup -n myVM -d --query [fqdns] -o tsv
```

<span data-ttu-id="065ca-141">Tooyour SSH ВМ, используя имя пользователя и общедоступный адрес DNS:</span><span class="sxs-lookup"><span data-stu-id="065ca-141">SSH tooyour VM using your own username and public DNS address:</span></span>

```bash
ssh azureuser@mypublicdns.eastus.cloudapp.azure.com
```

<span data-ttu-id="065ca-142">Проверка установки MongoDB hello при подключении с использованием локального hello `mongo` клиента следующим образом:</span><span class="sxs-lookup"><span data-stu-id="065ca-142">Verify hello MongoDB installation by connecting using hello local `mongo` client as follows:</span></span>

```bash
mongo
```

<span data-ttu-id="065ca-143">Теперь тест hello экземпляр с помощью добавления данных и поиска следующим образом:</span><span class="sxs-lookup"><span data-stu-id="065ca-143">Now test hello instance by adding some data and searching as follows:</span></span>

```sh
> db
test
> db.foo.insert( { a : 1 } )  
> db.foo.find()  
{ "_id" : ObjectId("57ec477cd639891710b90727"), "a" : 1 }
> exit
```


## <a name="create-a-complex-mongodb-sharded-cluster-on-centos-using-a-template"></a><span data-ttu-id="065ca-144">Создание сложного сегментированного кластера MongoDB на виртуальной машине CentOS с использованием шаблона</span><span class="sxs-lookup"><span data-stu-id="065ca-144">Create a complex MongoDB Sharded Cluster on CentOS using a template</span></span>
<span data-ttu-id="065ca-145">Можно создать сложные MongoDB сегментированных кластер, использующий hello следующую Azure примеры использования шаблона из GitHub.</span><span class="sxs-lookup"><span data-stu-id="065ca-145">You can create a complex MongoDB sharded cluster using hello following Azure quickstart template from GitHub.</span></span> <span data-ttu-id="065ca-146">В этом шаблоне описываются hello [рекомендации сегментированных кластера MongoDB](https://docs.mongodb.com/manual/core/sharded-cluster-components/) tooprovide избыточность и высокий уровень доступности.</span><span class="sxs-lookup"><span data-stu-id="065ca-146">This template follows hello [MongoDB sharded cluster best practices](https://docs.mongodb.com/manual/core/sharded-cluster-components/) tooprovide redundancy and high availability.</span></span> <span data-ttu-id="065ca-147">шаблон Hello создает два сегментов с тремя узлами в каждом наборе реплик.</span><span class="sxs-lookup"><span data-stu-id="065ca-147">hello template creates two shards, with three nodes in each replica set.</span></span> <span data-ttu-id="065ca-148">Также создается одно конфигурации сервера реплику с тремя узлами, плюс два **mongos** маршрутизатора серверов tooprovide согласованности tooapplications из по сегментам hello.</span><span class="sxs-lookup"><span data-stu-id="065ca-148">One config server replica set with three nodes is also created, plus two **mongos** router servers tooprovide consistency tooapplications from across hello shards.</span></span>

* <span data-ttu-id="065ca-149">[Сегментированный кластер MongoDB на виртуальной машине CentOS](https://github.com/Azure/azure-quickstart-templates/tree/master/mongodb-sharding-centos): https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/mongodb-sharding-centos/azuredeploy.json.</span><span class="sxs-lookup"><span data-stu-id="065ca-149">[MongoDB Sharding Cluster on CentOS](https://github.com/Azure/azure-quickstart-templates/tree/master/mongodb-sharding-centos) - https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/mongodb-sharding-centos/azuredeploy.json</span></span>

> [!WARNING]
> <span data-ttu-id="065ca-150">Развертывание этого сложного MongoDB сегментированных кластера требуется более чем 20 ядер, которой обычно является число ядер по умолчанию hello в одном регионе для подписки.</span><span class="sxs-lookup"><span data-stu-id="065ca-150">Deploying this complex MongoDB sharded cluster requires more than 20 cores, which is typically hello default core count per region for a subscription.</span></span> <span data-ttu-id="065ca-151">Откройте запрос поддержки Azure tooincrease на число ядер.</span><span class="sxs-lookup"><span data-stu-id="065ca-151">Open an Azure support request tooincrease your core count.</span></span>

<span data-ttu-id="065ca-152">toocreate этой среды hello требуется последняя версия [Azure CLI 2.0](/cli/azure/install-az-cli2) установлен и войти в систему с учетной записью Azure tooan [входа az](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="065ca-152">toocreate this environment, you need hello latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in tooan Azure account using [az login](/cli/azure/#login).</span></span> <span data-ttu-id="065ca-153">Сначала создайте группу ресурсов с помощью команды [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="065ca-153">First, create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="065ca-154">Hello следующий пример создает группу ресурсов с именем *myResourceGroup* в hello *eastus* расположение:</span><span class="sxs-lookup"><span data-stu-id="065ca-154">hello following example creates a resource group named *myResourceGroup* in hello *eastus* location:</span></span>

```azurecli
az group create --name myResourceGroup --location eastus
```

<span data-ttu-id="065ca-155">Затем разверните шаблон hello MongoDB с [создания развертывания группы az](/cli/azure/group/deployment#create).</span><span class="sxs-lookup"><span data-stu-id="065ca-155">Next, deploy hello MongoDB template with [az group deployment create](/cli/azure/group/deployment#create).</span></span> <span data-ttu-id="065ca-156">Определите необходимые имена и размеры ресурсов, например *mongoAdminUsername*, *sizeOfDataDiskInGB* и *configNodeVmSize*:</span><span class="sxs-lookup"><span data-stu-id="065ca-156">Define your own resource names and sizes where needed such as for *mongoAdminUsername*, *sizeOfDataDiskInGB*, and *configNodeVmSize*:</span></span>

```azurecli
az group deployment create --resource-group myResourceGroup \
  --parameters '{"adminUsername": {"value": "azureuser"},
    "adminPassword": {"value": "P@ssw0rd!"},
    "mongoAdminUsername": {"value": "mongoadmin"},
    "mongoAdminPassword": {"value": "P@ssw0rd!"},
    "dnsNamePrefix": {"value": "mypublicdns"},
    "environment": {"value": "AzureCloud"},
    "numDataDisks": {"value": "4"},
    "sizeOfDataDiskInGB": {"value": 20},
    "centOsVersion": {"value": "7.0"},
    "routerNodeVmSize": {"value": "Standard_DS3_v2"},
    "configNodeVmSize": {"value": "Standard_DS3_v2"},
    "replicaNodeVmSize": {"value": "Standard_DS3_v2"},
    "zabbixServerIPAddress": {"value": "Null"}}' \
  --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/mongodb-sharding-centos/azuredeploy.json \
  --name myMongoDBCluster \
  --no-wait
```

<span data-ttu-id="065ca-157">Это развертывание может перехватить toodeploy час и настройте все экземпляры виртуальной Машины hello.</span><span class="sxs-lookup"><span data-stu-id="065ca-157">This deployment can take over an hour toodeploy and configure all hello VM instances.</span></span> <span data-ttu-id="065ca-158">Hello `--no-wait` флаг используется в конце hello hello предшествующий команда tooreturn управления toohello командной строки после развертывания шаблона hello после принятия hello платформы Azure.</span><span class="sxs-lookup"><span data-stu-id="065ca-158">hello `--no-wait` flag is used at hello end of hello preceding command tooreturn control toohello command prompt once hello template deployment has been accepted by hello Azure platform.</span></span> <span data-ttu-id="065ca-159">Затем можно просмотреть состояние развертывания hello с [Показать развертывания группы az](/cli/azure/group/deployment#show).</span><span class="sxs-lookup"><span data-stu-id="065ca-159">You can then view hello deployment status with [az group deployment show](/cli/azure/group/deployment#show).</span></span> <span data-ttu-id="065ca-160">Hello следующие представления пример hello состояние для hello *myMongoDBCluster* развертывания в hello *myResourceGroup* группа ресурсов:</span><span class="sxs-lookup"><span data-stu-id="065ca-160">hello following example views hello status for hello *myMongoDBCluster* deployment in hello *myResourceGroup* resource group:</span></span>

```azurecli
az group deployment show \
    --resource-group myResourceGroup \
    --name myMongoDBCluster \
    --query [properties.provisioningState] \
    --output tsv
```

## <a name="next-steps"></a><span data-ttu-id="065ca-161">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="065ca-161">Next steps</span></span>
<span data-ttu-id="065ca-162">В этих примерах подключения toohello MongoDB экземпляра локально из hello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="065ca-162">In these examples, you connect toohello MongoDB instance locally from hello VM.</span></span> <span data-ttu-id="065ca-163">Если экземпляр MongoDB toohello tooconnect из другой виртуальной Машины или сети, убедитесь, соответствующие hello [создаются правила группы безопасности сети](nsg-quickstart.md).</span><span class="sxs-lookup"><span data-stu-id="065ca-163">If you want tooconnect toohello MongoDB instance from another VM or network, ensure hello appropriate [Network Security Group rules are created](nsg-quickstart.md).</span></span>

<span data-ttu-id="065ca-164">Эти примеры развертывания среды MongoDB core hello в целях разработки.</span><span class="sxs-lookup"><span data-stu-id="065ca-164">These examples deploy hello core MongoDB environment for development purposes.</span></span> <span data-ttu-id="065ca-165">Примените hello необходимые параметры конфигурации безопасности для вашей среды.</span><span class="sxs-lookup"><span data-stu-id="065ca-165">Apply hello required security configuration options for your environment.</span></span> <span data-ttu-id="065ca-166">Дополнительные сведения см. в разделе hello [docs безопасности MongoDB](https://docs.mongodb.com/manual/security/).</span><span class="sxs-lookup"><span data-stu-id="065ca-166">For more information, see hello [MongoDB security docs](https://docs.mongodb.com/manual/security/).</span></span>

<span data-ttu-id="065ca-167">Дополнительные сведения о создании с помощью шаблонов см. в разделе hello [Обзор диспетчера ресурсов Azure](../../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="065ca-167">For more information about creating using templates, see hello [Azure Resource Manager overview](../../azure-resource-manager/resource-group-overview.md).</span></span>

<span data-ttu-id="065ca-168">шаблоны Azure Resource Manager Hello использовать toodownload hello настраиваемое расширение скриптов и выполнения скриптов на ВМ.</span><span class="sxs-lookup"><span data-stu-id="065ca-168">hello Azure Resource Manager templates use hello Custom Script Extension toodownload and execute scripts on your VMs.</span></span> <span data-ttu-id="065ca-169">Дополнительные сведения см. в разделе [использование hello Azure настраиваемое расширение скриптов с виртуальных машин Linux](extensions-customscript.md).</span><span class="sxs-lookup"><span data-stu-id="065ca-169">For more information, see [Using hello Azure Custom Script Extension with Linux Virtual Machines](extensions-customscript.md).</span></span>

