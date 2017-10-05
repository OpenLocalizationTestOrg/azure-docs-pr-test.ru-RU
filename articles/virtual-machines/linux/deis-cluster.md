---
title: "Развертывание 3-узлового кластера Deis | Документация Майкрософт"
description: "В этой статье описывается создание 3-узлового кластера Deis в Azure с помощью шаблона диспетчера ресурсов Azure."
services: virtual-machines-linux
documentationcenter: 
author: HaishiBai
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 5eb67eb7-95d4-461d-8eac-44925224ba5f
ms.service: virtual-machines-linux
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 06/24/2015
ms.author: hbai
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 9a0c3dd7562dfb5ce54c2ebfd4665109f59cd8fd
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="deploy-and-configure-a-3-node-deis-cluster-in-azure"></a><span data-ttu-id="51c93-103">Развертывание и настройка 3-узлового кластера Deis в Azure</span><span class="sxs-lookup"><span data-stu-id="51c93-103">Deploy and configure a 3-node Deis cluster in Azure</span></span>
<span data-ttu-id="51c93-104">В этой статье пошагово описана подготовка кластера [Deis](http://deis.io/) в Azure.</span><span class="sxs-lookup"><span data-stu-id="51c93-104">This article walks you through provisioning a [Deis](http://deis.io/) cluster on Azure.</span></span> <span data-ttu-id="51c93-105">Она охватывает все действия, от создания необходимых сертификатов до развертывания и масштабирования примера приложения **Go** на новом подготовленном кластере.</span><span class="sxs-lookup"><span data-stu-id="51c93-105">It covers all the steps from creating the necessary certificates to deploying and scaling a sample **Go** application on the newly provisioned cluster.</span></span>

<span data-ttu-id="51c93-106">На следующей схеме показана архитектура развернутой системы.</span><span class="sxs-lookup"><span data-stu-id="51c93-106">The following diagram shows the architecture of the deployed system.</span></span> <span data-ttu-id="51c93-107">Системный администратор управляет кластером с помощью инструментов Deis, таких как **deis** и **deisctl**.</span><span class="sxs-lookup"><span data-stu-id="51c93-107">A system administrator manages the cluster using Deis tools such as **deis** and **deisctl**.</span></span> <span data-ttu-id="51c93-108">Подключения устанавливаются через посредством подсистемы балансировки нагрузки Azure, переадресовывающей подключения одному из узлов, участвующих в кластере.</span><span class="sxs-lookup"><span data-stu-id="51c93-108">Connections are established through an Azure load balancer, which forwards the connections to one of the member nodes on the cluster.</span></span> <span data-ttu-id="51c93-109">Кроме того, доступ клиентов к развернутым приложениям также осуществляется через подсистему балансировки нагрузки.</span><span class="sxs-lookup"><span data-stu-id="51c93-109">The clients access deployed applications through the load balancer as well.</span></span> <span data-ttu-id="51c93-110">В этом случае подсистема балансировки нагрузки переадресовывает трафик в сеть маршрутизатора Deis, который, в свою очередь, перенаправляет трафик в соответствующие контейнеры Docker, размещенные в кластере.</span><span class="sxs-lookup"><span data-stu-id="51c93-110">In this case, the load balancer forwards the traffic to a Deis router mesh, which further routs traffic to corresponding Docker containers hosted on the cluster.</span></span>

  ![Схема архитектуры развернутого кластера Deis](./media/deis-cluster/architecture-overview.png)

<span data-ttu-id="51c93-112">Вот что требуется, чтобы выполнить следующие действия:</span><span class="sxs-lookup"><span data-stu-id="51c93-112">In order to run through the following steps, you'll need:</span></span>

* <span data-ttu-id="51c93-113">Активная подписка Azure.</span><span class="sxs-lookup"><span data-stu-id="51c93-113">An active Azure subscription.</span></span> <span data-ttu-id="51c93-114">Если у вас ее нет, можно получить бесплатную ознакомительную версию на сайте [azure.com](https://azure.microsoft.com/).</span><span class="sxs-lookup"><span data-stu-id="51c93-114">If you don't have one, you can get a free trail on [azure.com](https://azure.microsoft.com/).</span></span>
* <span data-ttu-id="51c93-115">Рабочий или учебный идентификатор для использования групп ресурсов Azure.</span><span class="sxs-lookup"><span data-stu-id="51c93-115">A work or school id to use Azure resource groups.</span></span> <span data-ttu-id="51c93-116">Если у вас имеется личная учетная запись и для входа вы используете идентификатор Майкрософт, необходимо [создать рабочий идентификатор на основе вашего личного идентификатора](../windows/create-aad-work-id.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="51c93-116">If you have a personal account and log in with a Microsoft id, you need to [create a work id from your personal one](../windows/create-aad-work-id.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
* <span data-ttu-id="51c93-117">Либо, в зависимости от клиентской операционной системы, [Azure PowerShell](/powershell/azureps-cmdlets-docs) или [Azure CLI для Mac, Linux и Windows](../../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="51c93-117">Either -- depending on your client operating system -- the [Azure PowerShell](/powershell/azureps-cmdlets-docs) or the [Azure CLI for Mac, Linux, and Windows](../../cli-install-nodejs.md).</span></span>
* <span data-ttu-id="51c93-118">[OpenSSL](https://www.openssl.org/).</span><span class="sxs-lookup"><span data-stu-id="51c93-118">[OpenSSL](https://www.openssl.org/).</span></span> <span data-ttu-id="51c93-119">OpenSSL используется для создания необходимых сертификатов.</span><span class="sxs-lookup"><span data-stu-id="51c93-119">OpenSSL is used to generate the necessary certificates.</span></span>
* <span data-ttu-id="51c93-120">Клиент Git, например [Git Bash](https://git-scm.com/).</span><span class="sxs-lookup"><span data-stu-id="51c93-120">A Git client such as [Git Bash](https://git-scm.com/).</span></span>
* <span data-ttu-id="51c93-121">Чтобы протестировать пример приложения, также необходим DNS-сервер.</span><span class="sxs-lookup"><span data-stu-id="51c93-121">To test the sample application, you'll also need a DNS server.</span></span> <span data-ttu-id="51c93-122">Можно использовать любые DNS-серверы или службы, которые поддерживают записи A с подстановочным знаком.</span><span class="sxs-lookup"><span data-stu-id="51c93-122">You can use any DNS servers or services that support wildcard A records.</span></span>
* <span data-ttu-id="51c93-123">Компьютер для запуска клиентских инструментов Deis.</span><span class="sxs-lookup"><span data-stu-id="51c93-123">A computer to run Deis client tools.</span></span> <span data-ttu-id="51c93-124">Можно использовать локальный компьютер или виртуальную машину.</span><span class="sxs-lookup"><span data-stu-id="51c93-124">You can use either a local machine or a virtual machine.</span></span> <span data-ttu-id="51c93-125">Эти инструменты можно запустить практически на любом дистрибутиве Linux, но приведенные указания относятся к Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="51c93-125">You can run these tools on almost any Linux distribution, but the following instructions use Ubuntu.</span></span>

## <a name="provision-the-cluster"></a><span data-ttu-id="51c93-126">Подготовка кластера</span><span class="sxs-lookup"><span data-stu-id="51c93-126">Provision the cluster</span></span>
<span data-ttu-id="51c93-127">В этом разделе вы будете использовать шаблон [Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md) из репозитория открытого кода [azure-quickstart-templates](https://github.com/Azure/azure-quickstart-templates).</span><span class="sxs-lookup"><span data-stu-id="51c93-127">In this section, you'll use an [Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md) template from the open source repository [azure-quickstart-templates](https://github.com/Azure/azure-quickstart-templates).</span></span> <span data-ttu-id="51c93-128">Сначала вы скопируете шаблон.</span><span class="sxs-lookup"><span data-stu-id="51c93-128">First, you'll copy down the template.</span></span> <span data-ttu-id="51c93-129">Затем создадите новую пару ключей SSH для аутентификации.</span><span class="sxs-lookup"><span data-stu-id="51c93-129">Then, you'll create a new SSH key pair for authentication.</span></span> <span data-ttu-id="51c93-130">После этого вы настроите новый идентификатор для кластера.</span><span class="sxs-lookup"><span data-stu-id="51c93-130">And then, you'll configure a new identifier for you cluster.</span></span> <span data-ttu-id="51c93-131">И, наконец, вы используете сценарий оболочки или сценарий PowerShell для подготовки кластера.</span><span class="sxs-lookup"><span data-stu-id="51c93-131">And finally, you'll use either the Shell script or the PowerShell script to provision the cluster.</span></span>

1. <span data-ttu-id="51c93-132">Клонируйте репозиторий: [https://github.com/Azure/azure-quickstart-templates](https://github.com/Azure/azure-quickstart-templates).</span><span class="sxs-lookup"><span data-stu-id="51c93-132">Clone the repository: [https://github.com/Azure/azure-quickstart-templates](https://github.com/Azure/azure-quickstart-templates).</span></span>
   
        git clone https://github.com/Azure/azure-quickstart-templates
2. <span data-ttu-id="51c93-133">Перейдите в папку шаблона:</span><span class="sxs-lookup"><span data-stu-id="51c93-133">Go to the template folder:</span></span>
   
        cd azure-quickstart-templates\deis-cluster-coreos
3. <span data-ttu-id="51c93-134">Создайте новую пару ключей SSH, используя ssh-keygen:</span><span class="sxs-lookup"><span data-stu-id="51c93-134">Create a new SSH key pair using ssh-keygen:</span></span>
   
        ssh-keygen -t rsa -b 4096 -c "[your_email@domain.com]"
4. <span data-ttu-id="51c93-135">Создайте сертификат с помощью полученного выше закрытого ключа:</span><span class="sxs-lookup"><span data-stu-id="51c93-135">Generate a certificate using the above private key:</span></span>
   
        openssl req -x509 -days 365 -new -key [your private key file] -out [cert file to be generated]
5. <span data-ttu-id="51c93-136">Перейдите по адресу [https://discovery.etcd.io/new](https://discovery.etcd.io/new) , чтобы создать новый токен кластера, который имеет следующий вид:</span><span class="sxs-lookup"><span data-stu-id="51c93-136">Go to [https://discovery.etcd.io/new](https://discovery.etcd.io/new) to generate a new cluster token, which looks something like:</span></span>
   
        https://discovery.etcd.io/6a28e078895c5ec737174db2419bb2f3
   <br />
   <span data-ttu-id="51c93-137">У каждого кластера CoreOS должен быть уникальный токен от этой бесплатной службы.</span><span class="sxs-lookup"><span data-stu-id="51c93-137">Each CoreOS cluster needs to have a unique token from this free service.</span></span> <span data-ttu-id="51c93-138">Дополнительные сведения см. в [документации по CoreOS](https://coreos.com/docs/cluster-management/setup/cluster-discovery/).</span><span class="sxs-lookup"><span data-stu-id="51c93-138">Please see [CoreOS documentation](https://coreos.com/docs/cluster-management/setup/cluster-discovery/) for more details.</span></span>
6. <span data-ttu-id="51c93-139">Измените файл **cloud-config.yaml**, чтобы заменить существующий токен **discovery** новым.</span><span class="sxs-lookup"><span data-stu-id="51c93-139">Modify the **cloud-config.yaml** file to replace the existing  **discovery** token with the new token:</span></span>
   
        #cloud-config
        ---
        coreos:
          etcd:
            # generate a new token for each unique cluster from https://discovery.etcd.io/new
            # uncomment the following line and replace it with your discovery URL
            discovery: https://discovery.etcd.io/3973057f670770a7628f917d58c2208a
        ...
7. <span data-ttu-id="51c93-140">Измените файл **azuredeploy-parameters.json** : откройте сертификат, созданный на шаге 4, в текстовом редакторе.</span><span class="sxs-lookup"><span data-stu-id="51c93-140">Modify the **azuredeploy-parameters.json** file: Open the certificate you created in step 4 in a text editor.</span></span> <span data-ttu-id="51c93-141">Скопируйте весь текст между `----BEGIN CERTIFICATE-----` и `-----END CERTIFICATE-----` в параметр **sshKeyData** (необходимо удалить все знаки новой строки).</span><span class="sxs-lookup"><span data-stu-id="51c93-141">Copy all text between `----BEGIN CERTIFICATE-----` and `-----END CERTIFICATE-----` into the **sshKeyData** parameter (you'll need to remove all newline characters).</span></span>
8. <span data-ttu-id="51c93-142">Измените параметр **newStorageAccountName** .</span><span class="sxs-lookup"><span data-stu-id="51c93-142">Modify the **newStorageAccountName** parameter.</span></span> <span data-ttu-id="51c93-143">Это учетная запись хранения для дисков операционной системы виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="51c93-143">This is the storage account for VM OS disks.</span></span> <span data-ttu-id="51c93-144">Это имя учетной записи должно быть глобально уникальным.</span><span class="sxs-lookup"><span data-stu-id="51c93-144">This account name has to be globally unique.</span></span>
9. <span data-ttu-id="51c93-145">Измените параметр **publicDomainName** .</span><span class="sxs-lookup"><span data-stu-id="51c93-145">Modify the **publicDomainName** parameter.</span></span> <span data-ttu-id="51c93-146">Это значение станет частью DNS-имени, связанного с общедоступным IP-адресом подсистемы балансировки нагрузки.</span><span class="sxs-lookup"><span data-stu-id="51c93-146">This will become part of the DNS name associated with the load balancer public IP.</span></span> <span data-ttu-id="51c93-147">У окончательного полного доменного имени будет такой формат: *[значение этого параметра]*.*[регион]*.cloudapp.azure.com.</span><span class="sxs-lookup"><span data-stu-id="51c93-147">The final FQDN will have the format of *[value of this parameter]*.*[region]*.cloudapp.azure.com.</span></span> <span data-ttu-id="51c93-148">Например, если указать имя deishbai32, и группа ресурсов развернута в западной части США, окончательным полным доменным именем вашей подсистемы балансировки нагрузки будет deishbai32.westus.cloudapp.azure.com.</span><span class="sxs-lookup"><span data-stu-id="51c93-148">For example, if you specify the name as deishbai32, and the resource group is deployed to the West US region, then the final FQDN to your load balancer will be deishbai32.westus.cloudapp.azure.com.</span></span>
10. <span data-ttu-id="51c93-149">Сохраните файл параметров.</span><span class="sxs-lookup"><span data-stu-id="51c93-149">Save the parameter file.</span></span> <span data-ttu-id="51c93-150">После этого можно подготовить кластер с помощью Azure PowerShell:</span><span class="sxs-lookup"><span data-stu-id="51c93-150">And then you can provision the cluster using Azure PowerShell:</span></span>
    
        .\deploy-deis.ps1 -ResourceGroupName [resource group name] -ResourceGroupLocation "West US" -TemplateFile
        .\azuredeploy.json -ParametersFile .\azuredeploy-parameters.json -CloudInitFile .\cloud-config.yaml
    
    <span data-ttu-id="51c93-151">Или с помощью Azure CLI:</span><span class="sxs-lookup"><span data-stu-id="51c93-151">or Azure CLI:</span></span>
    
        ./deploy-deis.sh -n "[resource group name]" -l "West US" -f ./azuredeploy.json -e ./azuredeploy-parameters.json
        -c ./cloud-config.yaml  
11. <span data-ttu-id="51c93-152">После подготовки группы ресурсов вы увидите все эти ресурсы в данной группе на классическом портале Azure.</span><span class="sxs-lookup"><span data-stu-id="51c93-152">Once the resource group is provisioned, you can see all the resources in the group on Azure classic portal.</span></span> <span data-ttu-id="51c93-153">Как показано на следующем снимке экрана, группа ресурсов содержит виртуальную сеть с тремя виртуальными машинами, которые присоединены к одной группе доступности.</span><span class="sxs-lookup"><span data-stu-id="51c93-153">As shown in the following screenshot, the resource group contains a virtual network with three VMs, which are joined to the same availability set.</span></span> <span data-ttu-id="51c93-154">Группа также содержит подсистему балансировки нагрузки, имеющую связанный общедоступный IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="51c93-154">The group also contains a load balancer, which has an associated public IP.</span></span>
    
    ![Подготовленная группа ресурсов на классическом портале Azure](./media/deis-cluster/resource-group.png)

## <a name="install-the-client"></a><span data-ttu-id="51c93-156">Установка клиента</span><span class="sxs-lookup"><span data-stu-id="51c93-156">Install the client</span></span>
<span data-ttu-id="51c93-157">Для управления кластером Deis необходим **deisctl** .</span><span class="sxs-lookup"><span data-stu-id="51c93-157">You need **deisctl** to control your Deis cluster.</span></span> <span data-ttu-id="51c93-158">Хотя deisctl автоматически устанавливается на всех узлах кластера, рекомендуется использовать deisctl на отдельном компьютере администрирования.</span><span class="sxs-lookup"><span data-stu-id="51c93-158">Although deisctl is automatically installed in all the cluster nodes, it's a good practice to use deisctl on a separate administrative machine.</span></span> <span data-ttu-id="51c93-159">Более того, так как для всех узлов настроены только частные IP-адреса, для подключения к компьютерам узлов необходимо использовать туннелирование SSH через подсистему балансировки нагрузки, имеющую общедоступный IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="51c93-159">Furthermore, because all nodes are configured with only private IP addresses, you'll need to use SSH tunneling through the load balancer, which has a public IP, to connect to the node machines.</span></span> <span data-ttu-id="51c93-160">Ниже приведены шаги по настройке deisctl на отдельном физическом компьютере или виртуальной машине Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="51c93-160">The following are the steps of setting up deisctl on a separate Ubuntu physical or virtual machine.</span></span>

1. <span data-ttu-id="51c93-161">Установите deisctl:mkdir deis:</span><span class="sxs-lookup"><span data-stu-id="51c93-161">Install deisctl:mkdir deis</span></span>
   
        cd deis
        curl -sSL http://deis.io/deisctl/install.sh | sh -s 1.6.1
        sudo ln -fs $PWD/deisctl /usr/local/bin/deisctl
2. <span data-ttu-id="51c93-162">Добавьте закрытый ключ в агент ssh:</span><span class="sxs-lookup"><span data-stu-id="51c93-162">Add your private key to ssh agent:</span></span>
   
        eval `ssh-agent -s`
        ssh-add [path to the private key file, see step 1 in the previous section]
3. <span data-ttu-id="51c93-163">Настройте deisctl:</span><span class="sxs-lookup"><span data-stu-id="51c93-163">Configure deisctl:</span></span>
   
        export DEISCTL_TUNNEL=[public ip of the load balancer]:2223

<span data-ttu-id="51c93-164">Шаблон определяет правила для входящих подключений NAT, сопоставляющие 2223 с экземпляром 1, 2224 с экземпляром 2 и 2225 с экземпляром 3.</span><span class="sxs-lookup"><span data-stu-id="51c93-164">The template defines inbound NAT rules that map 2223 to instance 1, 2224 to instance 2, and 2225 to instance 3.</span></span> <span data-ttu-id="51c93-165">Это обеспечивает избыточность при использовании инструмента deisctl.</span><span class="sxs-lookup"><span data-stu-id="51c93-165">This provides redundancy for using the deisctl tool.</span></span> <span data-ttu-id="51c93-166">Можно просмотреть эти правила на классическом портале Azure.</span><span class="sxs-lookup"><span data-stu-id="51c93-166">You can examine these rules on Azure classic portal:</span></span>

![Правила NAT в подсистеме балансировки нагрузки](./media/deis-cluster/nat-rules.png)

> [!NOTE]
> <span data-ttu-id="51c93-168">Сейчас шаблон поддерживает только 3-узловые кластеры.</span><span class="sxs-lookup"><span data-stu-id="51c93-168">Currently the template only supports 3-node clusters.</span></span> <span data-ttu-id="51c93-169">Это связано с ограничением в определении правил NAT шаблона диспетчера ресурсов Azure, которое не позволяет использовать синтаксис цикла.</span><span class="sxs-lookup"><span data-stu-id="51c93-169">This is because of a limitation in Azure Resource Manager template NAT rule definition, which doesn’t support loop syntax.</span></span>
> 
> 

## <a name="install-and-start-the-deis-platform"></a><span data-ttu-id="51c93-170">Установка и запуск платформы Deis</span><span class="sxs-lookup"><span data-stu-id="51c93-170">Install and start the Deis platform</span></span>
<span data-ttu-id="51c93-171">Теперь можно использовать deisctl для установки и запуска платформы Deis:</span><span class="sxs-lookup"><span data-stu-id="51c93-171">Now you can use deisctl to install and start the Deis platform:</span></span>

    deisctl config platform set domain=[some domain]
    deisctl config platform set sshPrivateKey=[path to the private key file]
    deisctl install platform
    deisctl start platform

> [!NOTE]
> <span data-ttu-id="51c93-172">Запуск платформы занимает некоторое время (до 10 минут).</span><span class="sxs-lookup"><span data-stu-id="51c93-172">Starting the platform takes a while (as much as 10 minutes).</span></span> <span data-ttu-id="51c93-173">Особенно долго запускается служба builder.</span><span class="sxs-lookup"><span data-stu-id="51c93-173">Especially, starting the builder service can take a long time.</span></span> <span data-ttu-id="51c93-174">Иногда требуется несколько попыток: если операция перестает отвечать на запросы, попробуйте ввести `ctrl+c`, чтобы прервать выполнение команды и повторить попытку.</span><span class="sxs-lookup"><span data-stu-id="51c93-174">And sometimes it takes a few tries to succeed: If the operation seems to hang, try typing `ctrl+c` to break execution of the command and retry.</span></span>
> 
> 

<span data-ttu-id="51c93-175">Можно использовать `deisctl list`, чтобы проверить, все ли службы запущены:</span><span class="sxs-lookup"><span data-stu-id="51c93-175">You can use `deisctl list` to verify if all services are running:</span></span>

    deisctl list
    UNIT                            MACHINE                 LOAD    ACTIVE          SUB
    deis-builder.service            ebe3005e.../10.0.0.6    loaded  active          running
    deis-controller.service         ebe3005e.../10.0.0.6    loaded  active          running
    deis-database.service           9c79bbdd.../10.0.0.5    loaded  active          running
    deis-logger.service             9c79bbdd.../10.0.0.5    loaded  active          running
    deis-logspout.service           8d658d5a.../10.0.0.4    loaded  active          running
    deis-logspout.service           9c79bbdd.../10.0.0.5    loaded  active          running
    deis-logspout.service           ebe3005e.../10.0.0.6    loaded  active          running
    deis-publisher.service          8d658d5a.../10.0.0.4    loaded  active          running
    deis-publisher.service          9c79bbdd.../10.0.0.5    loaded  active          running
    deis-publisher.service          ebe3005e.../10.0.0.6    loaded  active          running
    deis-registry@1.service         ebe3005e.../10.0.0.6    loaded  active          running
    deis-router@1.service           ebe3005e.../10.0.0.6    loaded  active          running
    deis-router@2.service           8d658d5a.../10.0.0.4    loaded  active          running
    deis-router@3.service           9c79bbdd.../10.0.0.5    loaded  active          running
    deis-store-daemon.service       8d658d5a.../10.0.0.4    loaded  active          running
    deis-store-daemon.service       9c79bbdd.../10.0.0.5    loaded  active          running
    deis-store-daemon.service       ebe3005e.../10.0.0.6    loaded  active          running
    deis-store-gateway@1.service    9c79bbdd.../10.0.0.5    loaded  active          running
    deis-store-metadata.service     8d658d5a.../10.0.0.4    loaded  active          running
    deis-store-metadata.service     9c79bbdd.../10.0.0.5    loaded  active          running
    deis-store-metadata.service     ebe3005e.../10.0.0.6    loaded  active          running
    deis-store-monitor.service      8d658d5a.../10.0.0.4    loaded  active          running
    deis-store-monitor.service      9c79bbdd.../10.0.0.5    loaded  active          running
    deis-store-monitor.service      ebe3005e.../10.0.0.6    loaded  active          running
    deis-store-volume.service       8d658d5a.../10.0.0.4    loaded  active          running
    deis-store-volume.service       9c79bbdd.../10.0.0.5    loaded  active          running
    deis-store-volume.service       ebe3005e.../10.0.0.6    loaded  active          running

<span data-ttu-id="51c93-176">Поздравляем!</span><span class="sxs-lookup"><span data-stu-id="51c93-176">Congratulations!</span></span> <span data-ttu-id="51c93-177">Теперь у вас есть работающий кластер Deis в Azure!</span><span class="sxs-lookup"><span data-stu-id="51c93-177">Now you've got a running Deis clsuter on Azure!</span></span> <span data-ttu-id="51c93-178">Теперь давайте развернем пример приложения Go, чтобы просмотреть, как работает кластер.</span><span class="sxs-lookup"><span data-stu-id="51c93-178">Next, let's deploy a sample Go application to see the cluster in action.</span></span>

## <a name="deploy-and-scale-a-hello-world-application"></a><span data-ttu-id="51c93-179">Развертывание и масштабирование приложения Hello World</span><span class="sxs-lookup"><span data-stu-id="51c93-179">Deploy and scale a Hello World application</span></span>
<span data-ttu-id="51c93-180">Ниже показано, как развернуть приложение Go «Hello World» в кластере.</span><span class="sxs-lookup"><span data-stu-id="51c93-180">The following steps show how to deploy a "Hello World" Go application to the cluster.</span></span> <span data-ttu-id="51c93-181">Шаги основаны на [документации по Deis](http://docs.deis.io/en/latest/using_deis/using-dockerfiles/#using-dockerfiles).</span><span class="sxs-lookup"><span data-stu-id="51c93-181">The steps are based on [Deis documentation](http://docs.deis.io/en/latest/using_deis/using-dockerfiles/#using-dockerfiles).</span></span>

1. <span data-ttu-id="51c93-182">Чтобы сеть маршрутизации работала правильно, необходимо иметь запись A с подстановочным знаком для домена, указывающую на общедоступный IP-адрес подсистемы балансировки нагрузки.</span><span class="sxs-lookup"><span data-stu-id="51c93-182">For the routing mesh to work properly, you’ll need to have a wildcard A record for your domain pointing to the public IP of the load balancer.</span></span> <span data-ttu-id="51c93-183">На следующем снимке экрана показана запись A для примера регистрации домена на GoDaddy:</span><span class="sxs-lookup"><span data-stu-id="51c93-183">The following screenshot shows the A record for a sample domain registration on GoDaddy:</span></span>
   
    ![Запись A Godaddy](./media/deis-cluster/go-daddy.png)
   
   <p />
2. <span data-ttu-id="51c93-185">Установите deis:</span><span class="sxs-lookup"><span data-stu-id="51c93-185">Install deis:</span></span>
   
        mkdir deis
        cd deis
        curl -sSL http://deis.io/deis-cli/install.sh | sh
        ln -fs $PWD/deis /usr/local/bin/deis
3. <span data-ttu-id="51c93-186">Создайте новый ключ SSH, а затем добавьте открытый ключ в GitHub (конечно, можно также повторно использовать существующие ключи).</span><span class="sxs-lookup"><span data-stu-id="51c93-186">Create a new SSH key, and then add the public key to GitHub (of course, you can also reuse your existing keys).</span></span> <span data-ttu-id="51c93-187">Чтобы создать новую пару ключей SSH, используйте:</span><span class="sxs-lookup"><span data-stu-id="51c93-187">To create a new SSH key pair, use:</span></span>
   
        cd ~/.ssh
        ssh-keygen (press [Enter]s to use default file names and empty passcode)
4. <span data-ttu-id="51c93-188">Добавьте в GitHub id_rsa.pub или открытый ключ (по своему усмотрению).</span><span class="sxs-lookup"><span data-stu-id="51c93-188">Add id_rsa.pub, or the public key of your choice, to GitHub.</span></span> <span data-ttu-id="51c93-189">Это можно сделать с помощью кнопки «Add SSH key» (Добавить ключ SSH) на экране настройки ключей SSH:</span><span class="sxs-lookup"><span data-stu-id="51c93-189">You can do this by using the Add SSH key button in your SSH keys configuration screen:</span></span>
   
   ![Ключ GitHub](./media/deis-cluster/github-key.png)
   
   <p />
5. <span data-ttu-id="51c93-191">Зарегистрируйте нового пользователя:</span><span class="sxs-lookup"><span data-stu-id="51c93-191">Register a new user:</span></span>
   
        deis register http://deis.[your domain]
   <p />
6. <span data-ttu-id="51c93-192">Добавьте ключ SSH:</span><span class="sxs-lookup"><span data-stu-id="51c93-192">Add the SSH key:</span></span>
   
        deis keys:add [path to your SSH public key]
   <p />      
7. <span data-ttu-id="51c93-193">Создайте приложение:</span><span class="sxs-lookup"><span data-stu-id="51c93-193">Create an application.</span></span>
   
        git clone https://github.com/deis/helloworld.git
        cd helloworld
        deis create
        git push deis master
   <p /><span data-ttu-id="51c93-194">
8. Отправка git инициирует сборку и развертывание образов Docker, что может занять несколько минут.</span><span class="sxs-lookup"><span data-stu-id="51c93-194">
8. The git push will trigger Docker images to be built and deployed, which will take a few minutes.</span></span> <span data-ttu-id="51c93-195">Из личного опыта: иногда на шаге 10 (при отправке образа в частный репозиторий) система может перестать отвечать на запросы.</span><span class="sxs-lookup"><span data-stu-id="51c93-195">From my experience, occasionally, Step 10 (Pushing image to private repository) may hang.</span></span> <span data-ttu-id="51c93-196">В этом случае можно остановить процесс и удалить приложение с помощью команды deis apps:destroy –a <application name>` to remove the application and try again. You can use `deis apps:list, чтобы узнать имя приложения.</span><span class="sxs-lookup"><span data-stu-id="51c93-196">When this happens, you can stop the process, remove the application using `deis apps:destroy –a <application name>` to remove the application and try again. You can use `deis apps:list` to find out the name of your application.</span></span> <span data-ttu-id="51c93-197">Если все работает, по завершении вывода команды вы увидите примерно следующее:</span><span class="sxs-lookup"><span data-stu-id="51c93-197">If everything works out, you should see something like the following at the end of command outputs:</span></span>
   
        -----> Launching...
               done, lambda-underdog:v2 deployed to Deis
               http://lambda-underdog.artitrack.com
               To learn more, use `deis help` or visit http://deis.io
        To ssh://git@deis.artitrack.com:2222/lambda-underdog.git
         * [new branch]      master -> master
   <p />
9. <span data-ttu-id="51c93-198">Проверьте, работает ли приложение:</span><span class="sxs-lookup"><span data-stu-id="51c93-198">Verify if the application is working:</span></span>
   
        curl -S http://[your application name].[your domain]
   <span data-ttu-id="51c93-199">Вы должны увидеть следующее:</span><span class="sxs-lookup"><span data-stu-id="51c93-199">You should see:</span></span>
   
        Welcome to Deis!
        See the documentation at http://docs.deis.io/ for more information.
        (you can use geis apps:list to get the name of your application).
   <p />
10. <span data-ttu-id="51c93-200">Масштабируйте приложение на 3 экземпляра:</span><span class="sxs-lookup"><span data-stu-id="51c93-200">Scale the application to 3 instances:</span></span>
    
        deis scale cmd=3
    <p />
11. <span data-ttu-id="51c93-201">Кроме того, можно использовать deis info, чтобы просмотреть сведения о приложении.</span><span class="sxs-lookup"><span data-stu-id="51c93-201">Optionally, you can use deis info to examine details of your application.</span></span> <span data-ttu-id="51c93-202">Ниже приведены выходные данные моего развертывания приложения:</span><span class="sxs-lookup"><span data-stu-id="51c93-202">The following outputs are from my application deployment:</span></span>
    
        deis info
        === lambda-underdog Application
        {
          "updated": "2015-05-22T06:14:10UTC",
          "uuid": "10c74ee7-b7ff-4786-967a-7e65af7eabc3",
          "created": "2015-05-22T06:07:55UTC",
          "url": "lambda-underdog.artitrack.com",
          "owner": "haishi",
          "id": "lambda-underdog",
          "structure": {
            "cmd": 3
          }
        }
    
        === lambda-underdog Processes
        --- cmd:
        cmd.1 up (v2)
        cmd.2 up (v2)
        cmd.3 up (v2)
    
        === lambda-underdog Domains
        No domains

## <a name="next-steps"></a><span data-ttu-id="51c93-203">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="51c93-203">Next Steps</span></span>
<span data-ttu-id="51c93-204">В этой статье подробно описаны все шаги по подготовке нового кластера Deis в Azure с помощью шаблона диспетчера ресурсов Azure.</span><span class="sxs-lookup"><span data-stu-id="51c93-204">This article walked you through all the steps to provision a new Deis cluster on Azure using an Azure Resource Manager template.</span></span> <span data-ttu-id="51c93-205">Шаблон поддерживает избыточность подключений инструментов, а также балансировку нагрузки для развернутых приложений.</span><span class="sxs-lookup"><span data-stu-id="51c93-205">The template supports redundancy in tooling connections as well as load balancing for deployed applications.</span></span> <span data-ttu-id="51c93-206">Шаблон также позволяет избежать использования общедоступных IP-адресов на узлах кластера, что позволяет экономить ценные ресурсы общедоступных IP-адресов и обеспечивает более защищенную среду для размещения приложений.</span><span class="sxs-lookup"><span data-stu-id="51c93-206">The template also avoids using public IPs on member nodes, which saves precious public IP resources and provides a more secured environment to host applications.</span></span> <span data-ttu-id="51c93-207">Для получения дополнительных сведений ознакомьтесь со следующими статьями:</span><span class="sxs-lookup"><span data-stu-id="51c93-207">To learn more, see the following articles:</span></span>

<span data-ttu-id="51c93-208">[Общие сведения о диспетчере ресурсов Azure][resource-group-overview]</span><span class="sxs-lookup"><span data-stu-id="51c93-208">[Azure Resource Manager Overview][resource-group-overview]</span></span>  
<span data-ttu-id="51c93-209">[Установка Azure CLI][azure-command-line-tools]</span><span class="sxs-lookup"><span data-stu-id="51c93-209">[How to use the Azure CLI][azure-command-line-tools]</span></span>  
<span data-ttu-id="51c93-210">[Использование Azure PowerShell с Azure Resource Manager][powershell-azure-resource-manager]</span><span class="sxs-lookup"><span data-stu-id="51c93-210">[Using Azure PowerShell with Azure Resource Manager][powershell-azure-resource-manager]</span></span>  

[azure-command-line-tools]: ../../cli-install-nodejs.md
[resource-group-overview]: ../../azure-resource-manager/resource-group-overview.md
[powershell-azure-resource-manager]: ../../azure-resource-manager/powershell-azure-resource-manager.md
