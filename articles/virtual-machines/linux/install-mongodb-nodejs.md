---
title: "Здравствуйте, aaaInstall MongoDB на виртуальной Машине Linux с помощью Azure CLI 1.0 | Документы Microsoft"
description: "Узнайте, как tooinstall и настройте на виртуальной машине Linux в Azure с помощью модели развертывания диспетчера ресурсов hello MongoDB."
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
ms.assetid: 3f55b546-86df-4442-9ef4-8a25fae7b96e
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/11/2017
ms.author: iainfou
ms.openlocfilehash: 4ce21a2c63da7d00a4422e0a6766e2103e7f12d7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooinstall-and-configure-mongodb-on-a-linux-vm-using-hello-azure-cli-10"></a><span data-ttu-id="096a4-103">Как tooinstall и настройте MongoDB на ВМ Linux с помощью hello Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="096a4-103">How tooinstall and configure MongoDB on a Linux VM using hello Azure CLI 1.0</span></span>
<span data-ttu-id="096a4-104">[MongoDB](http://www.mongodb.org) — это популярная высокопроизводительная база данных NoSQL с открытым кодом.</span><span class="sxs-lookup"><span data-stu-id="096a4-104">[MongoDB](http://www.mongodb.org) is a popular open-source, high-performance NoSQL database.</span></span> <span data-ttu-id="096a4-105">В этой статье показано, как tooinstall и настройте на виртуальной Машине Linux в Azure с помощью модели развертывания диспетчера ресурсов hello MongoDB.</span><span class="sxs-lookup"><span data-stu-id="096a4-105">This article shows you how tooinstall and configure MongoDB on a Linux VM in Azure using hello Resource Manager deployment model.</span></span> <span data-ttu-id="096a4-106">Изучив представленные примеры, вы узнаете, как:</span><span class="sxs-lookup"><span data-stu-id="096a4-106">Examples are shown that detail how to:</span></span>

* <span data-ttu-id="096a4-107">[установить и настроить базовый экземпляр MongoDB вручную](#manually-install-and-configure-mongodb-on-a-vm);</span><span class="sxs-lookup"><span data-stu-id="096a4-107">[Manually install and configure a basic MongoDB instance](#manually-install-and-configure-mongodb-on-a-vm)</span></span>
* <span data-ttu-id="096a4-108">[создать базовый экземпляр MongoDB на основе шаблона Resource Manager](#create-basic-mongodb-instance-on-centos-using-a-template);</span><span class="sxs-lookup"><span data-stu-id="096a4-108">[Create a basic MongoDB instance using a Resource Manager template](#create-basic-mongodb-instance-on-centos-using-a-template)</span></span>
* <span data-ttu-id="096a4-109">[создать сложный сегментированный кластер MongoDB с набором реплик с использованием шаблона Resource Manager](#create-a-complex-mongodb-sharded-cluster-on-centos-using-a-template).</span><span class="sxs-lookup"><span data-stu-id="096a4-109">[Create a complex MongoDB sharded cluster with replica sets using a Resource Manager template](#create-a-complex-mongodb-sharded-cluster-on-centos-using-a-template)</span></span>


## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="096a4-110">Задача hello toocomplete версии CLI</span><span class="sxs-lookup"><span data-stu-id="096a4-110">CLI versions toocomplete hello task</span></span>
<span data-ttu-id="096a4-111">Можно выполнить с помощью одного из следующих версий CLI hello задачу hello.</span><span class="sxs-lookup"><span data-stu-id="096a4-111">You can complete hello task using one of hello following CLI versions:</span></span>

- <span data-ttu-id="096a4-112">Azure CLI 1.0 — нашей CLI для hello классический и ресурса управления развертывания моделей (в этой статье)</span><span class="sxs-lookup"><span data-stu-id="096a4-112">Azure CLI 1.0 – our CLI for hello classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="096a4-113">[Azure CLI 2.0](create-cli-complete-nodejs.md) -нашей нового поколения CLI для модели развертывания hello ресурсов управления</span><span class="sxs-lookup"><span data-stu-id="096a4-113">[Azure CLI 2.0](create-cli-complete-nodejs.md) - our next generation CLI for hello resource management deployment model</span></span>


## <a name="manually-install-and-configure-mongodb-on-a-vm"></a><span data-ttu-id="096a4-114">Установка и настройка MongoDB на виртуальной машине вручную</span><span class="sxs-lookup"><span data-stu-id="096a4-114">Manually install and configure MongoDB on a VM</span></span>
<span data-ttu-id="096a4-115">База данных MongoDB [содержит инструкции по установке](https://docs.mongodb.com/manual/administration/install-on-linux/) для дистрибутивов Linux, в том числе Red Hat, CentOS, SUSE, Ubuntu и Debian.</span><span class="sxs-lookup"><span data-stu-id="096a4-115">MongoDB [provide installation instructions](https://docs.mongodb.com/manual/administration/install-on-linux/) for Linux distros including Red Hat / CentOS, SUSE, Ubuntu, and Debian.</span></span> <span data-ttu-id="096a4-116">Hello следующий пример создает *CentOS* виртуальную Машину с помощью ключа SSH, хранящиеся в *~/.ssh/id_rsa.pub*.</span><span class="sxs-lookup"><span data-stu-id="096a4-116">hello following example creates a *CentOS* VM using an SSH key stored at *~/.ssh/id_rsa.pub*.</span></span> <span data-ttu-id="096a4-117">Hello ответов запрашивает имя учетной записи хранения, DNS-имя и учетные данные администратора:</span><span class="sxs-lookup"><span data-stu-id="096a4-117">Answer hello prompts for storage account name, DNS name, and admin credentials:</span></span>

```azurecli
azure vm quick-create \
    --image-urn CentOS \
    --ssh-publickey-file ~/.ssh/id_rsa.pub 
```

<span data-ttu-id="096a4-118">Войдите на toohello виртуальной Машины с помощью hello общедоступный IP-адрес отображается в конце hello hello предшествующий этап создания виртуальной Машины:</span><span class="sxs-lookup"><span data-stu-id="096a4-118">Log on toohello VM using hello public IP address displayed at hello end of hello preceding VM creation step:</span></span>

```bash
ssh azureuser@40.78.23.145
```

<span data-ttu-id="096a4-119">создать источник установки hello tooadd MongoDB, **yum** файл репозитория следующим образом:</span><span class="sxs-lookup"><span data-stu-id="096a4-119">tooadd hello installation sources for MongoDB, create a **yum** repository file as follows:</span></span>

```bash
sudo touch /etc/yum.repos.d/mongodb-org-3.4.repo
```

<span data-ttu-id="096a4-120">Откройте для редактирования файл репозитория hello MongoDB.</span><span class="sxs-lookup"><span data-stu-id="096a4-120">Open hello MongoDB repo file for editing.</span></span> <span data-ttu-id="096a4-121">Добавьте следующие строки hello:</span><span class="sxs-lookup"><span data-stu-id="096a4-121">Add hello following lines:</span></span>

```sh
[mongodb-org-3.4]
name=MongoDB Repository
baseurl=https://repo.mongodb.org/yum/redhat/$releasever/mongodb-org/3.4/x86_64/
gpgcheck=1
enabled=1
gpgkey=https://www.mongodb.org/static/pgp/server-3.4.asc
```

<span data-ttu-id="096a4-122">Установите MongoDB, используя **yum**, как показано ниже:</span><span class="sxs-lookup"><span data-stu-id="096a4-122">Install MongoDB using **yum** as follows:</span></span>

```bash
sudo yum install -y mongodb-org
```

<span data-ttu-id="096a4-123">По умолчанию в образах CentOS принудительно используется SELinux. Это препятствует доступу к MongoDB.</span><span class="sxs-lookup"><span data-stu-id="096a4-123">By default, SELinux is enforced on CentOS images that prevents you from accessing MongoDB.</span></span> <span data-ttu-id="096a4-124">Установка средств управления политиками и настройка SELinux tooallow MongoDB toooperate на порт TCP по умолчанию 27017 следующим образом.</span><span class="sxs-lookup"><span data-stu-id="096a4-124">Install policy management tools and configure SELinux tooallow MongoDB toooperate on its default TCP port 27017 as follows.</span></span> 

```bash
sudo yum install -y policycoreutils-python
sudo semanage port -a -t mongod_port_t -p tcp 27017
```

<span data-ttu-id="096a4-125">Запуск службы MongoDB hello следующим образом:</span><span class="sxs-lookup"><span data-stu-id="096a4-125">Start hello MongoDB service as follows:</span></span>

```bash
sudo service mongod start
```

<span data-ttu-id="096a4-126">Проверка установки MongoDB hello при подключении с использованием локального hello `mongo` клиента:</span><span class="sxs-lookup"><span data-stu-id="096a4-126">Verify hello MongoDB installation by connecting using hello local `mongo` client:</span></span>

```bash
mongo
```

<span data-ttu-id="096a4-127">Теперь можно проверьте экземпляр MongoDB hello, добавив некоторые данные и затем найти:</span><span class="sxs-lookup"><span data-stu-id="096a4-127">Now test hello MongoDB instance by adding some data and then searching:</span></span>

```sh
> db
test
> db.foo.insert( { a : 1 } )  
> db.foo.find()  
{ "_id" : ObjectId("57ec477cd639891710b90727"), "a" : 1 }
> exit
```

<span data-ttu-id="096a4-128">При необходимости настройте MongoDB toostart автоматически во время перезагрузки системы.</span><span class="sxs-lookup"><span data-stu-id="096a4-128">If desired, configure MongoDB toostart automatically during a system reboot:</span></span>

```bash
sudo chkconfig mongod on
```


## <a name="create-basic-mongodb-instance-on-centos-using-a-template"></a><span data-ttu-id="096a4-129">Создание базового экземпляра MongoDB на виртуальной машине CentOS с использованием шаблона</span><span class="sxs-lookup"><span data-stu-id="096a4-129">Create basic MongoDB instance on CentOS using a template</span></span>
<span data-ttu-id="096a4-130">Можно создать базовый экземпляр MongoDB на одной виртуальной Машины CentOS с помощью hello следующую Azure примеры использования шаблона из GitHub.</span><span class="sxs-lookup"><span data-stu-id="096a4-130">You can create a basic MongoDB instance on a single CentOS VM using hello following Azure quickstart template from GitHub.</span></span> <span data-ttu-id="096a4-131">Этот шаблон использует расширение hello пользовательский сценарий для Linux tooadd `yum` tooyour репозитория вновь созданные ВМ CentOS, а затем установите MongoDB.</span><span class="sxs-lookup"><span data-stu-id="096a4-131">This template uses hello Custom Script extension for Linux tooadd a `yum` repository tooyour newly created CentOS VM and then install MongoDB.</span></span>

* <span data-ttu-id="096a4-132">[Базовый экземпляр MongoDB на виртуальной машине CentOS](https://github.com/Azure/azure-quickstart-templates/tree/master/mongodb-on-centos): https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/mongodb-on-centos/azuredeploy.json.</span><span class="sxs-lookup"><span data-stu-id="096a4-132">[Basic MongoDB instance on CentOS](https://github.com/Azure/azure-quickstart-templates/tree/master/mongodb-on-centos) - https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/mongodb-on-centos/azuredeploy.json</span></span>

<span data-ttu-id="096a4-133">Hello следующий пример создает группу ресурсов с именем hello `myResourceGroup` в hello `eastus` области.</span><span class="sxs-lookup"><span data-stu-id="096a4-133">hello following example creates a resource group with hello name `myResourceGroup` in hello `eastus` region.</span></span> <span data-ttu-id="096a4-134">Введите свои значения следующим образом:</span><span class="sxs-lookup"><span data-stu-id="096a4-134">Enter your own values as follows:</span></span>

```azurecli
azure group create \
    --name myResourceGroup \
    --location eastus \
    --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/mongodb-on-centos/azuredeploy.json
```

> [!NOTE]
> <span data-ttu-id="096a4-135">Hello Azure CLI возвращает строки tooa через несколько секунд создания hello развертывания, но попытка установки hello и конфигурация принимает toocomplete несколько минут.</span><span class="sxs-lookup"><span data-stu-id="096a4-135">hello Azure CLI returns you tooa prompt within a few seconds of creating hello deployment, but hello installation and configuration takes a few minutes toocomplete.</span></span> <span data-ttu-id="096a4-136">Проверьте состояние развертывания hello с hello `azure group deployment show myResourceGroup`, введя hello имя группы ресурсов соответствующим образом.</span><span class="sxs-lookup"><span data-stu-id="096a4-136">Check hello status of hello deployment with `azure group deployment show myResourceGroup`, entering hello name of your resource group accordingly.</span></span> <span data-ttu-id="096a4-137">Подождите, пока hello **ProvisioningState** показывает *успешно* перед идет tooSSH toohello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="096a4-137">Wait until hello **ProvisioningState** shows *Succeeded* before trying tooSSH toohello VM.</span></span>

<span data-ttu-id="096a4-138">После развертывания hello завершить, toohello SSH виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="096a4-138">Once hello deployment is complete, SSH toohello VM.</span></span> <span data-ttu-id="096a4-139">Получить IP-адрес виртуальной Машины с помощью hello hello `azure vm show` команду как hello в следующем примере:</span><span class="sxs-lookup"><span data-stu-id="096a4-139">Obtain hello IP address of your VM using hello `azure vm show` command as in hello following example:</span></span>

```azurecli
azure vm show --resource-group myResourceGroup --name myLinuxVM
```

<span data-ttu-id="096a4-140">Конец hello hello выходные данные отображается hello общедоступный IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="096a4-140">Near hello end of hello output, hello public IP address is displayed.</span></span> <span data-ttu-id="096a4-141">Tooyour SSH виртуальной Машины с IP-адресом hello вашей виртуальной машины:</span><span class="sxs-lookup"><span data-stu-id="096a4-141">SSH tooyour VM with hello IP address of your VM:</span></span>

```bash
ssh azureuser@138.91.149.74
```

<span data-ttu-id="096a4-142">Проверка установки MongoDB hello при подключении с использованием локального hello `mongo` клиента следующим образом:</span><span class="sxs-lookup"><span data-stu-id="096a4-142">Verify hello MongoDB installation by connecting using hello local `mongo` client as follows:</span></span>

```bash
mongo
```

<span data-ttu-id="096a4-143">Теперь тест hello экземпляр с помощью добавления данных и поиска следующим образом:</span><span class="sxs-lookup"><span data-stu-id="096a4-143">Now test hello instance by adding some data and searching as follows:</span></span>

```sh
> db
test
> db.foo.insert( { a : 1 } )  
> db.foo.find()  
{ "_id" : ObjectId("57ec477cd639891710b90727"), "a" : 1 }
> exit
```


## <a name="create-a-complex-mongodb-sharded-cluster-on-centos-using-a-template"></a><span data-ttu-id="096a4-144">Создание сложного сегментированного кластера MongoDB на виртуальной машине CentOS с использованием шаблона</span><span class="sxs-lookup"><span data-stu-id="096a4-144">Create a complex MongoDB Sharded Cluster on CentOS using a template</span></span>
<span data-ttu-id="096a4-145">Можно создать сложные MongoDB сегментированных кластер, использующий hello следующую Azure примеры использования шаблона из GitHub.</span><span class="sxs-lookup"><span data-stu-id="096a4-145">You can create a complex MongoDB sharded cluster using hello following Azure quickstart template from GitHub.</span></span> <span data-ttu-id="096a4-146">В этом шаблоне описываются hello [рекомендации сегментированных кластера MongoDB](https://docs.mongodb.com/manual/core/sharded-cluster-components/) tooprovide избыточность и высокий уровень доступности.</span><span class="sxs-lookup"><span data-stu-id="096a4-146">This template follows hello [MongoDB sharded cluster best practices](https://docs.mongodb.com/manual/core/sharded-cluster-components/) tooprovide redundancy and high availability.</span></span> <span data-ttu-id="096a4-147">шаблон Hello создает два сегментов с тремя узлами в каждом наборе реплик.</span><span class="sxs-lookup"><span data-stu-id="096a4-147">hello template creates two shards, with three nodes in each replica set.</span></span> <span data-ttu-id="096a4-148">Также создается одно конфигурации сервера реплику с тремя узлами, плюс два **mongos** маршрутизатора серверов tooprovide согласованности tooapplications из по сегментам hello.</span><span class="sxs-lookup"><span data-stu-id="096a4-148">One config server replica set with three nodes is also created, plus two **mongos** router servers tooprovide consistency tooapplications from across hello shards.</span></span>

* <span data-ttu-id="096a4-149">[Сегментированный кластер MongoDB на виртуальной машине CentOS](https://github.com/Azure/azure-quickstart-templates/tree/master/mongodb-sharding-centos): https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/mongodb-sharding-centos/azuredeploy.json.</span><span class="sxs-lookup"><span data-stu-id="096a4-149">[MongoDB Sharding Cluster on CentOS](https://github.com/Azure/azure-quickstart-templates/tree/master/mongodb-sharding-centos) - https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/mongodb-sharding-centos/azuredeploy.json</span></span>

> [!WARNING]
> <span data-ttu-id="096a4-150">Развертывание этого сложного MongoDB сегментированных кластера требуется более чем 20 ядер, которой обычно является число ядер по умолчанию hello в одном регионе для подписки.</span><span class="sxs-lookup"><span data-stu-id="096a4-150">Deploying this complex MongoDB sharded cluster requires more than 20 cores, which is typically hello default core count per region for a subscription.</span></span> <span data-ttu-id="096a4-151">Откройте запрос поддержки Azure tooincrease на число ядер.</span><span class="sxs-lookup"><span data-stu-id="096a4-151">Open an Azure support request tooincrease your core count.</span></span>

<span data-ttu-id="096a4-152">Hello следующий пример создает группу ресурсов с именем hello *myResourceGroup* в hello *eastus* области.</span><span class="sxs-lookup"><span data-stu-id="096a4-152">hello following example creates a resource group with hello name *myResourceGroup* in hello *eastus* region.</span></span> <span data-ttu-id="096a4-153">Введите свои значения следующим образом:</span><span class="sxs-lookup"><span data-stu-id="096a4-153">Enter your own values as follows:</span></span>

```azurecli
azure group create \
    --name myResourceGroup \
    --location eastus \
    --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/mongodb-sharding-centos/azuredeploy.json
```

> [!NOTE]
> <span data-ttu-id="096a4-154">Hello Azure CLI возвращает строки tooa через несколько секунд создания hello развертывания, но hello установки и настройки может взять на себя toocomplete час.</span><span class="sxs-lookup"><span data-stu-id="096a4-154">hello Azure CLI returns you tooa prompt within a few seconds of creating hello deployment, but hello installation and configuration can take over an hour toocomplete.</span></span> <span data-ttu-id="096a4-155">Проверьте состояние развертывания hello с hello `azure group deployment show myResourceGroup`, соответственно изменив hello имя группы ресурсов.</span><span class="sxs-lookup"><span data-stu-id="096a4-155">Check hello status of hello deployment with `azure group deployment show myResourceGroup`, adjusting hello name of your resource group accordingly.</span></span> <span data-ttu-id="096a4-156">Подождите, пока hello **ProvisioningState** показывает *успешно* перед подключением toohello виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="096a4-156">Wait until hello **ProvisioningState** shows *Succeeded* before connecting toohello VMs.</span></span>


## <a name="next-steps"></a><span data-ttu-id="096a4-157">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="096a4-157">Next steps</span></span>
<span data-ttu-id="096a4-158">В этих примерах подключения toohello MongoDB экземпляра локально из hello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="096a4-158">In these examples, you connect toohello MongoDB instance locally from hello VM.</span></span> <span data-ttu-id="096a4-159">Если экземпляр MongoDB toohello tooconnect из другой виртуальной Машины или сети, убедитесь, соответствующие hello [создаются правила группы безопасности сети](nsg-quickstart.md).</span><span class="sxs-lookup"><span data-stu-id="096a4-159">If you want tooconnect toohello MongoDB instance from another VM or network, ensure hello appropriate [Network Security Group rules are created](nsg-quickstart.md).</span></span>

<span data-ttu-id="096a4-160">Дополнительные сведения о создании с помощью шаблонов см. в разделе hello [Обзор диспетчера ресурсов Azure](../../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="096a4-160">For more information about creating using templates, see hello [Azure Resource Manager overview](../../azure-resource-manager/resource-group-overview.md).</span></span>

<span data-ttu-id="096a4-161">шаблоны Azure Resource Manager Hello использовать toodownload hello настраиваемое расширение скриптов и выполнения скриптов на ВМ.</span><span class="sxs-lookup"><span data-stu-id="096a4-161">hello Azure Resource Manager templates use hello Custom Script Extension toodownload and execute scripts on your VMs.</span></span> <span data-ttu-id="096a4-162">Дополнительные сведения см. в разделе [использование hello Azure настраиваемое расширение скриптов с виртуальных машин Linux](extensions-customscript.md).</span><span class="sxs-lookup"><span data-stu-id="096a4-162">For more information, see [Using hello Azure Custom Script Extension with Linux Virtual Machines](extensions-customscript.md).</span></span>

