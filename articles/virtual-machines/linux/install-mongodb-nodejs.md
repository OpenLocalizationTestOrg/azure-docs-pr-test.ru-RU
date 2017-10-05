---
title: "Установка MongoDB на виртуальную машину Linux с помощью Azure CLI 1.0 | Документация Майкрософт"
description: "Узнайте, как установить и настроить MongoDB на виртуальной машине Linux в Azure, используя модель развертывания с помощью Resource Manager."
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
ms.openlocfilehash: c97ade0a3d95824f723aad55776de861fe49441f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-install-and-configure-mongodb-on-a-linux-vm-using-the-azure-cli-10"></a><span data-ttu-id="95ed7-103">Как установить и настроить MongoDB на виртуальную машину Linux с помощью Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="95ed7-103">How to install and configure MongoDB on a Linux VM using the Azure CLI 1.0</span></span>
<span data-ttu-id="95ed7-104">[MongoDB](http://www.mongodb.org) — это популярная высокопроизводительная база данных NoSQL с открытым кодом.</span><span class="sxs-lookup"><span data-stu-id="95ed7-104">[MongoDB](http://www.mongodb.org) is a popular open-source, high-performance NoSQL database.</span></span> <span data-ttu-id="95ed7-105">В этой статье рассматривается, как установить и настроить MongoDB на виртуальной машине Linux в Azure, используя модель развертывания с помощью Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="95ed7-105">This article shows you how to install and configure MongoDB on a Linux VM in Azure using the Resource Manager deployment model.</span></span> <span data-ttu-id="95ed7-106">Изучив представленные примеры, вы узнаете, как:</span><span class="sxs-lookup"><span data-stu-id="95ed7-106">Examples are shown that detail how to:</span></span>

* <span data-ttu-id="95ed7-107">[установить и настроить базовый экземпляр MongoDB вручную](#manually-install-and-configure-mongodb-on-a-vm);</span><span class="sxs-lookup"><span data-stu-id="95ed7-107">[Manually install and configure a basic MongoDB instance](#manually-install-and-configure-mongodb-on-a-vm)</span></span>
* <span data-ttu-id="95ed7-108">[создать базовый экземпляр MongoDB на основе шаблона Resource Manager](#create-basic-mongodb-instance-on-centos-using-a-template);</span><span class="sxs-lookup"><span data-stu-id="95ed7-108">[Create a basic MongoDB instance using a Resource Manager template](#create-basic-mongodb-instance-on-centos-using-a-template)</span></span>
* <span data-ttu-id="95ed7-109">[создать сложный сегментированный кластер MongoDB с набором реплик с использованием шаблона Resource Manager](#create-a-complex-mongodb-sharded-cluster-on-centos-using-a-template).</span><span class="sxs-lookup"><span data-stu-id="95ed7-109">[Create a complex MongoDB sharded cluster with replica sets using a Resource Manager template](#create-a-complex-mongodb-sharded-cluster-on-centos-using-a-template)</span></span>


## <a name="cli-versions-to-complete-the-task"></a><span data-ttu-id="95ed7-110">Версии интерфейса командной строки для выполнения задачи</span><span class="sxs-lookup"><span data-stu-id="95ed7-110">CLI versions to complete the task</span></span>
<span data-ttu-id="95ed7-111">Вы можете выполнить задачу, используя одну из следующих версий интерфейса командной строки.</span><span class="sxs-lookup"><span data-stu-id="95ed7-111">You can complete the task using one of the following CLI versions:</span></span>

- <span data-ttu-id="95ed7-112">Azure CLI 1.0 — интерфейс командной строки для классической модели развертывания и модели развертывания Resource Manager (в этой статье).</span><span class="sxs-lookup"><span data-stu-id="95ed7-112">Azure CLI 1.0 – our CLI for the classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="95ed7-113">[Azure CLI 2.0](create-cli-complete-nodejs.md) — интерфейс командной строки следующего поколения для модели развертывания с помощью Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="95ed7-113">[Azure CLI 2.0](create-cli-complete-nodejs.md) - our next generation CLI for the resource management deployment model</span></span>


## <a name="manually-install-and-configure-mongodb-on-a-vm"></a><span data-ttu-id="95ed7-114">Установка и настройка MongoDB на виртуальной машине вручную</span><span class="sxs-lookup"><span data-stu-id="95ed7-114">Manually install and configure MongoDB on a VM</span></span>
<span data-ttu-id="95ed7-115">База данных MongoDB [содержит инструкции по установке](https://docs.mongodb.com/manual/administration/install-on-linux/) для дистрибутивов Linux, в том числе Red Hat, CentOS, SUSE, Ubuntu и Debian.</span><span class="sxs-lookup"><span data-stu-id="95ed7-115">MongoDB [provide installation instructions](https://docs.mongodb.com/manual/administration/install-on-linux/) for Linux distros including Red Hat / CentOS, SUSE, Ubuntu, and Debian.</span></span> <span data-ttu-id="95ed7-116">В следующем примере создается виртуальная машина *CentOS*, использующая ключ SSH, который хранится в каталоге *~/.ssh/id_rsa.pub*.</span><span class="sxs-lookup"><span data-stu-id="95ed7-116">The following example creates a *CentOS* VM using an SSH key stored at *~/.ssh/id_rsa.pub*.</span></span> <span data-ttu-id="95ed7-117">В ответ на запросы укажите имя учетной записи хранения, DNS-имя и учетные данные администратора:</span><span class="sxs-lookup"><span data-stu-id="95ed7-117">Answer the prompts for storage account name, DNS name, and admin credentials:</span></span>

```azurecli
azure vm quick-create \
    --image-urn CentOS \
    --ssh-publickey-file ~/.ssh/id_rsa.pub 
```

<span data-ttu-id="95ed7-118">Войдите в виртуальную машину, используя общедоступный IP-адрес, полученный на предыдущем шаге создания виртуальной машины:</span><span class="sxs-lookup"><span data-stu-id="95ed7-118">Log on to the VM using the public IP address displayed at the end of the preceding VM creation step:</span></span>

```bash
ssh azureuser@40.78.23.145
```

<span data-ttu-id="95ed7-119">Чтобы добавить источники установки для MongoDB, создайте файл репозитория **yum**, как показано ниже:</span><span class="sxs-lookup"><span data-stu-id="95ed7-119">To add the installation sources for MongoDB, create a **yum** repository file as follows:</span></span>

```bash
sudo touch /etc/yum.repos.d/mongodb-org-3.4.repo
```

<span data-ttu-id="95ed7-120">Откройте файл репозитория MongoDB для редактирования.</span><span class="sxs-lookup"><span data-stu-id="95ed7-120">Open the MongoDB repo file for editing.</span></span> <span data-ttu-id="95ed7-121">Добавьте следующие строки.</span><span class="sxs-lookup"><span data-stu-id="95ed7-121">Add the following lines:</span></span>

```sh
[mongodb-org-3.4]
name=MongoDB Repository
baseurl=https://repo.mongodb.org/yum/redhat/$releasever/mongodb-org/3.4/x86_64/
gpgcheck=1
enabled=1
gpgkey=https://www.mongodb.org/static/pgp/server-3.4.asc
```

<span data-ttu-id="95ed7-122">Установите MongoDB, используя **yum**, как показано ниже:</span><span class="sxs-lookup"><span data-stu-id="95ed7-122">Install MongoDB using **yum** as follows:</span></span>

```bash
sudo yum install -y mongodb-org
```

<span data-ttu-id="95ed7-123">По умолчанию в образах CentOS принудительно используется SELinux. Это препятствует доступу к MongoDB.</span><span class="sxs-lookup"><span data-stu-id="95ed7-123">By default, SELinux is enforced on CentOS images that prevents you from accessing MongoDB.</span></span> <span data-ttu-id="95ed7-124">Установите средства управления политиками и настройте SELinux так, чтобы база данных MongoDB могла использовать TCP-порт 27017 (по умолчанию):</span><span class="sxs-lookup"><span data-stu-id="95ed7-124">Install policy management tools and configure SELinux to allow MongoDB to operate on its default TCP port 27017 as follows.</span></span> 

```bash
sudo yum install -y policycoreutils-python
sudo semanage port -a -t mongod_port_t -p tcp 27017
```

<span data-ttu-id="95ed7-125">Запустите службу MongoDB следующим образом:</span><span class="sxs-lookup"><span data-stu-id="95ed7-125">Start the MongoDB service as follows:</span></span>

```bash
sudo service mongod start
```

<span data-ttu-id="95ed7-126">Проверьте установленную базы данных MongoDB, подключившись к ней с помощью локального клиента `mongo`:</span><span class="sxs-lookup"><span data-stu-id="95ed7-126">Verify the MongoDB installation by connecting using the local `mongo` client:</span></span>

```bash
mongo
```

<span data-ttu-id="95ed7-127">Теперь проверьте экземпляр MongoDB, добавив некоторые данные и выполнив их поиск:</span><span class="sxs-lookup"><span data-stu-id="95ed7-127">Now test the MongoDB instance by adding some data and then searching:</span></span>

```sh
> db
test
> db.foo.insert( { a : 1 } )  
> db.foo.find()  
{ "_id" : ObjectId("57ec477cd639891710b90727"), "a" : 1 }
> exit
```

<span data-ttu-id="95ed7-128">При необходимости настройте автоматический запуск MongoDB при перезагрузке системы:</span><span class="sxs-lookup"><span data-stu-id="95ed7-128">If desired, configure MongoDB to start automatically during a system reboot:</span></span>

```bash
sudo chkconfig mongod on
```


## <a name="create-basic-mongodb-instance-on-centos-using-a-template"></a><span data-ttu-id="95ed7-129">Создание базового экземпляра MongoDB на виртуальной машине CentOS с использованием шаблона</span><span class="sxs-lookup"><span data-stu-id="95ed7-129">Create basic MongoDB instance on CentOS using a template</span></span>
<span data-ttu-id="95ed7-130">На виртуальной машине CentOS можно создать базовый экземпляр MongoDB, используя следующий шаблон быстрого запуска Azure из GitHub.</span><span class="sxs-lookup"><span data-stu-id="95ed7-130">You can create a basic MongoDB instance on a single CentOS VM using the following Azure quickstart template from GitHub.</span></span> <span data-ttu-id="95ed7-131">В этом шаблоне используется расширение настраиваемых скриптов для Linux, что позволяет добавить в созданную виртуальную машину CentOS репозиторий `yum`, а затем установить MongoDB.</span><span class="sxs-lookup"><span data-stu-id="95ed7-131">This template uses the Custom Script extension for Linux to add a `yum` repository to your newly created CentOS VM and then install MongoDB.</span></span>

* <span data-ttu-id="95ed7-132">[Базовый экземпляр MongoDB на виртуальной машине CentOS](https://github.com/Azure/azure-quickstart-templates/tree/master/mongodb-on-centos): https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/mongodb-on-centos/azuredeploy.json.</span><span class="sxs-lookup"><span data-stu-id="95ed7-132">[Basic MongoDB instance on CentOS](https://github.com/Azure/azure-quickstart-templates/tree/master/mongodb-on-centos) - https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/mongodb-on-centos/azuredeploy.json</span></span>

<span data-ttu-id="95ed7-133">В следующем примере создается группа ресурсов с именем `myResourceGroup` в регионе `eastus`.</span><span class="sxs-lookup"><span data-stu-id="95ed7-133">The following example creates a resource group with the name `myResourceGroup` in the `eastus` region.</span></span> <span data-ttu-id="95ed7-134">Введите свои значения следующим образом:</span><span class="sxs-lookup"><span data-stu-id="95ed7-134">Enter your own values as follows:</span></span>

```azurecli
azure group create \
    --name myResourceGroup \
    --location eastus \
    --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/mongodb-on-centos/azuredeploy.json
```

> [!NOTE]
> <span data-ttu-id="95ed7-135">Интерфейс командной строки Azure отобразит строку всего через несколько секунд после начала развертывания, но для завершения установки и настройки может потребоваться несколько минут.</span><span class="sxs-lookup"><span data-stu-id="95ed7-135">The Azure CLI returns you to a prompt within a few seconds of creating the deployment, but the installation and configuration takes a few minutes to complete.</span></span> <span data-ttu-id="95ed7-136">Проверьте состояние развертывания, выполнив команду `azure group deployment show myResourceGroup` и указав соответствующим образом имя группы ресурсов.</span><span class="sxs-lookup"><span data-stu-id="95ed7-136">Check the status of the deployment with `azure group deployment show myResourceGroup`, entering the name of your resource group accordingly.</span></span> <span data-ttu-id="95ed7-137">Подождите, пока для параметра **ProvisioningState** не отобразится значение *Succeeded*, а затем попробуйте подключиться к виртуальной машине по протоколу SSH.</span><span class="sxs-lookup"><span data-stu-id="95ed7-137">Wait until the **ProvisioningState** shows *Succeeded* before trying to SSH to the VM.</span></span>

<span data-ttu-id="95ed7-138">После развертывания подключитесь к виртуальной машине по протоколу SSH.</span><span class="sxs-lookup"><span data-stu-id="95ed7-138">Once the deployment is complete, SSH to the VM.</span></span> <span data-ttu-id="95ed7-139">Получите IP-адрес виртуальной машины, используя команду `azure vm show`, как показано в следующем примере:</span><span class="sxs-lookup"><span data-stu-id="95ed7-139">Obtain the IP address of your VM using the `azure vm show` command as in the following example:</span></span>

```azurecli
azure vm show --resource-group myResourceGroup --name myLinuxVM
```

<span data-ttu-id="95ed7-140">В конце выходных данных будет отображаться общедоступный IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="95ed7-140">Near the end of the output, the public IP address is displayed.</span></span> <span data-ttu-id="95ed7-141">Подключитесь к своей виртуальной машине по протоколу SSH, используя ее IP-адрес:</span><span class="sxs-lookup"><span data-stu-id="95ed7-141">SSH to your VM with the IP address of your VM:</span></span>

```bash
ssh azureuser@138.91.149.74
```

<span data-ttu-id="95ed7-142">Проверьте установку базы данных MongoDB, подключившись к ней с помощью локального клиента `mongo`, как показано ниже:</span><span class="sxs-lookup"><span data-stu-id="95ed7-142">Verify the MongoDB installation by connecting using the local `mongo` client as follows:</span></span>

```bash
mongo
```

<span data-ttu-id="95ed7-143">Теперь проверьте экземпляр, добавив некоторые данные и выполнив их поиск, как показано ниже:</span><span class="sxs-lookup"><span data-stu-id="95ed7-143">Now test the instance by adding some data and searching as follows:</span></span>

```sh
> db
test
> db.foo.insert( { a : 1 } )  
> db.foo.find()  
{ "_id" : ObjectId("57ec477cd639891710b90727"), "a" : 1 }
> exit
```


## <a name="create-a-complex-mongodb-sharded-cluster-on-centos-using-a-template"></a><span data-ttu-id="95ed7-144">Создание сложного сегментированного кластера MongoDB на виртуальной машине CentOS с использованием шаблона</span><span class="sxs-lookup"><span data-stu-id="95ed7-144">Create a complex MongoDB Sharded Cluster on CentOS using a template</span></span>
<span data-ttu-id="95ed7-145">Используя следующий шаблон быстрого запуска Azure из GitHub, можно создать сложный сегментированный кластер MongoDB.</span><span class="sxs-lookup"><span data-stu-id="95ed7-145">You can create a complex MongoDB sharded cluster using the following Azure quickstart template from GitHub.</span></span> <span data-ttu-id="95ed7-146">Этот шаблон соответствует [рекомендациям для сегментированного кластера MongoDB](https://docs.mongodb.com/manual/core/sharded-cluster-components/) в отношении избыточности и высокой доступности.</span><span class="sxs-lookup"><span data-stu-id="95ed7-146">This template follows the [MongoDB sharded cluster best practices](https://docs.mongodb.com/manual/core/sharded-cluster-components/) to provide redundancy and high availability.</span></span> <span data-ttu-id="95ed7-147">Он предусматривает создание двух сегментов с тремя узлами в каждом наборе реплик.</span><span class="sxs-lookup"><span data-stu-id="95ed7-147">The template creates two shards, with three nodes in each replica set.</span></span> <span data-ttu-id="95ed7-148">Кроме того, он создает набор реплик сервера конфигурации и два сервера маршрутизации **mongos**. Это позволяет обеспечить согласованность приложений из разных сегментов.</span><span class="sxs-lookup"><span data-stu-id="95ed7-148">One config server replica set with three nodes is also created, plus two **mongos** router servers to provide consistency to applications from across the shards.</span></span>

* <span data-ttu-id="95ed7-149">[Сегментированный кластер MongoDB на виртуальной машине CentOS](https://github.com/Azure/azure-quickstart-templates/tree/master/mongodb-sharding-centos): https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/mongodb-sharding-centos/azuredeploy.json.</span><span class="sxs-lookup"><span data-stu-id="95ed7-149">[MongoDB Sharding Cluster on CentOS](https://github.com/Azure/azure-quickstart-templates/tree/master/mongodb-sharding-centos) - https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/mongodb-sharding-centos/azuredeploy.json</span></span>

> [!WARNING]
> <span data-ttu-id="95ed7-150">Для развертывания сложного сегментированного кластера MongoDB требуется более 20 ядер. Обычно 20 ядер — это количество по умолчанию для региона, выделяемое на одну подписку.</span><span class="sxs-lookup"><span data-stu-id="95ed7-150">Deploying this complex MongoDB sharded cluster requires more than 20 cores, which is typically the default core count per region for a subscription.</span></span> <span data-ttu-id="95ed7-151">Отправьте запрос в службу поддержки Azure, чтобы увеличить количество ядер.</span><span class="sxs-lookup"><span data-stu-id="95ed7-151">Open an Azure support request to increase your core count.</span></span>

<span data-ttu-id="95ed7-152">В следующем примере создается группа ресурсов с именем *myResourceGroup* в регионе *eastus*.</span><span class="sxs-lookup"><span data-stu-id="95ed7-152">The following example creates a resource group with the name *myResourceGroup* in the *eastus* region.</span></span> <span data-ttu-id="95ed7-153">Введите свои значения следующим образом:</span><span class="sxs-lookup"><span data-stu-id="95ed7-153">Enter your own values as follows:</span></span>

```azurecli
azure group create \
    --name myResourceGroup \
    --location eastus \
    --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/mongodb-sharding-centos/azuredeploy.json
```

> [!NOTE]
> <span data-ttu-id="95ed7-154">Интерфейс командной строки Azure отобразит строку всего через несколько секунд после начала развертывания, но для завершения установки и настройки может потребоваться более одного часа.</span><span class="sxs-lookup"><span data-stu-id="95ed7-154">The Azure CLI returns you to a prompt within a few seconds of creating the deployment, but the installation and configuration can take over an hour to complete.</span></span> <span data-ttu-id="95ed7-155">Проверьте состояние развертывания, выполнив команду `azure group deployment show myResourceGroup` и указав соответствующим образом имя группы ресурсов.</span><span class="sxs-lookup"><span data-stu-id="95ed7-155">Check the status of the deployment with `azure group deployment show myResourceGroup`, adjusting the name of your resource group accordingly.</span></span> <span data-ttu-id="95ed7-156">Подождите, пока для параметра **ProvisioningState** не отобразится значение *Succeeded*, а затем попробуйте подключиться к виртуальным машинам.</span><span class="sxs-lookup"><span data-stu-id="95ed7-156">Wait until the **ProvisioningState** shows *Succeeded* before connecting to the VMs.</span></span>


## <a name="next-steps"></a><span data-ttu-id="95ed7-157">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="95ed7-157">Next steps</span></span>
<span data-ttu-id="95ed7-158">В этих примерах подключение к экземпляру MongoDB выполняется локально с помощью виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="95ed7-158">In these examples, you connect to the MongoDB instance locally from the VM.</span></span> <span data-ttu-id="95ed7-159">Чтобы подключится к экземпляру MongoDB из другой виртуальной машины или сети, [создайте соответствующие правила группы безопасности сети](nsg-quickstart.md).</span><span class="sxs-lookup"><span data-stu-id="95ed7-159">If you want to connect to the MongoDB instance from another VM or network, ensure the appropriate [Network Security Group rules are created](nsg-quickstart.md).</span></span>

<span data-ttu-id="95ed7-160">Дополнительные сведения о создании с использованием шаблонов см. в статье [Общие сведения о диспетчере ресурсов Azure](../../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="95ed7-160">For more information about creating using templates, see the [Azure Resource Manager overview](../../azure-resource-manager/resource-group-overview.md).</span></span>

<span data-ttu-id="95ed7-161">Для скачивания и выполнения скриптов на виртуальных машинах в шаблонах Azure Resource Manager используется расширение настраиваемых скриптов.</span><span class="sxs-lookup"><span data-stu-id="95ed7-161">The Azure Resource Manager templates use the Custom Script Extension to download and execute scripts on your VMs.</span></span> <span data-ttu-id="95ed7-162">Дополнительные сведения см. в статье [Использование расширения пользовательских сценариев Azure на виртуальных машинах Linux](extensions-customscript.md).</span><span class="sxs-lookup"><span data-stu-id="95ed7-162">For more information, see [Using the Azure Custom Script Extension with Linux Virtual Machines](extensions-customscript.md).</span></span>

