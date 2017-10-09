---
title: "aaaDeploy Deis 3-узловой кластер | Документы Microsoft"
description: "В этой статье описывается как toocreate 3-узловой Deis кластера в Azure с помощью шаблона диспетчера ресурсов Azure"
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
ms.openlocfilehash: a4c0fb8cbb849264e64b433540157c9afecd184e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-and-configure-a-3-node-deis-cluster-in-azure"></a><span data-ttu-id="53a8f-103">Развертывание и настройка 3-узлового кластера Deis в Azure</span><span class="sxs-lookup"><span data-stu-id="53a8f-103">Deploy and configure a 3-node Deis cluster in Azure</span></span>
<span data-ttu-id="53a8f-104">В этой статье пошагово описана подготовка кластера [Deis](http://deis.io/) в Azure.</span><span class="sxs-lookup"><span data-stu-id="53a8f-104">This article walks you through provisioning a [Deis](http://deis.io/) cluster on Azure.</span></span> <span data-ttu-id="53a8f-105">Она охватывает все действия hello на создание сертификатов, необходимых toodeploying hello и масштабирование образец **Go** приложение hello нового кластера.</span><span class="sxs-lookup"><span data-stu-id="53a8f-105">It covers all hello steps from creating hello necessary certificates toodeploying and scaling a sample **Go** application on hello newly provisioned cluster.</span></span>

<span data-ttu-id="53a8f-106">Hello следующей схеме показана архитектура hello hello развертывания системы.</span><span class="sxs-lookup"><span data-stu-id="53a8f-106">hello following diagram shows hello architecture of hello deployed system.</span></span> <span data-ttu-id="53a8f-107">Системный администратор управляет hello кластера с помощью Deis средств, таких как **deis** и **deisctl**.</span><span class="sxs-lookup"><span data-stu-id="53a8f-107">A system administrator manages hello cluster using Deis tools such as **deis** and **deisctl**.</span></span> <span data-ttu-id="53a8f-108">Соединения устанавливаются с помощью балансировки нагрузки Azure, направляет tooone подключений hello члена hello узлы в кластере hello.</span><span class="sxs-lookup"><span data-stu-id="53a8f-108">Connections are established through an Azure load balancer, which forwards hello connections tooone of hello member nodes on hello cluster.</span></span> <span data-ttu-id="53a8f-109">доступ клиентов Hello развернутых приложений через hello также балансировки нагрузки.</span><span class="sxs-lookup"><span data-stu-id="53a8f-109">hello clients access deployed applications through hello load balancer as well.</span></span> <span data-ttu-id="53a8f-110">В этом случае балансировки нагрузки hello перенаправляет трафик tooa hello Deis сетки маршрутизатор, который дальнейшей перенаправляет вызвавший контейнеры Docker toocorresponding трафика, размещенных в кластере hello.</span><span class="sxs-lookup"><span data-stu-id="53a8f-110">In this case, hello load balancer forwards hello traffic tooa Deis router mesh, which further routs traffic toocorresponding Docker containers hosted on hello cluster.</span></span>

  ![Схема архитектуры развернутого кластера Deis](./media/deis-cluster/architecture-overview.png)

<span data-ttu-id="53a8f-112">Порядок toorun через hello, выполнив действия вам потребуется:</span><span class="sxs-lookup"><span data-stu-id="53a8f-112">In order toorun through hello following steps, you'll need:</span></span>

* <span data-ttu-id="53a8f-113">Активная подписка Azure.</span><span class="sxs-lookup"><span data-stu-id="53a8f-113">An active Azure subscription.</span></span> <span data-ttu-id="53a8f-114">Если у вас ее нет, можно получить бесплатную ознакомительную версию на сайте [azure.com](https://azure.microsoft.com/).</span><span class="sxs-lookup"><span data-stu-id="53a8f-114">If you don't have one, you can get a free trail on [azure.com](https://azure.microsoft.com/).</span></span>
* <span data-ttu-id="53a8f-115">Рабочий или группы ресурсов Azure toouse идентификатор учебного заведения.</span><span class="sxs-lookup"><span data-stu-id="53a8f-115">A work or school id toouse Azure resource groups.</span></span> <span data-ttu-id="53a8f-116">Если имеется личная учетная запись и войти в систему с Microsoft id, необходимо слишком[создать из вашего личного один идентификатор рабочего](../windows/create-aad-work-id.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="53a8f-116">If you have a personal account and log in with a Microsoft id, you need too[create a work id from your personal one](../windows/create-aad-work-id.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
* <span data-ttu-id="53a8f-117">Либо — в зависимости от операционной системы клиента--hello [Azure PowerShell](/powershell/azureps-cmdlets-docs) или hello [Azure CLI для Mac, Linux и Windows](../../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="53a8f-117">Either -- depending on your client operating system -- hello [Azure PowerShell](/powershell/azureps-cmdlets-docs) or hello [Azure CLI for Mac, Linux, and Windows](../../cli-install-nodejs.md).</span></span>
* <span data-ttu-id="53a8f-118">[OpenSSL](https://www.openssl.org/).</span><span class="sxs-lookup"><span data-stu-id="53a8f-118">[OpenSSL](https://www.openssl.org/).</span></span> <span data-ttu-id="53a8f-119">OpenSSL — используется toogenerate hello необходимые сертификаты.</span><span class="sxs-lookup"><span data-stu-id="53a8f-119">OpenSSL is used toogenerate hello necessary certificates.</span></span>
* <span data-ttu-id="53a8f-120">Клиент Git, например [Git Bash](https://git-scm.com/).</span><span class="sxs-lookup"><span data-stu-id="53a8f-120">A Git client such as [Git Bash](https://git-scm.com/).</span></span>
* <span data-ttu-id="53a8f-121">Пример приложения hello tootest, кроме того, потребуется DNS-сервера.</span><span class="sxs-lookup"><span data-stu-id="53a8f-121">tootest hello sample application, you'll also need a DNS server.</span></span> <span data-ttu-id="53a8f-122">Можно использовать любые DNS-серверы или службы, которые поддерживают записи A с подстановочным знаком.</span><span class="sxs-lookup"><span data-stu-id="53a8f-122">You can use any DNS servers or services that support wildcard A records.</span></span>
* <span data-ttu-id="53a8f-123">Toorun компьютер Deis клиентских средств.</span><span class="sxs-lookup"><span data-stu-id="53a8f-123">A computer toorun Deis client tools.</span></span> <span data-ttu-id="53a8f-124">Можно использовать локальный компьютер или виртуальную машину.</span><span class="sxs-lookup"><span data-stu-id="53a8f-124">You can use either a local machine or a virtual machine.</span></span> <span data-ttu-id="53a8f-125">Эти инструменты можно использовать на любой дистрибутив Linux, но hello следующие инструкции используют Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="53a8f-125">You can run these tools on almost any Linux distribution, but hello following instructions use Ubuntu.</span></span>

## <a name="provision-hello-cluster"></a><span data-ttu-id="53a8f-126">Подготовка кластера hello</span><span class="sxs-lookup"><span data-stu-id="53a8f-126">Provision hello cluster</span></span>
<span data-ttu-id="53a8f-127">В этом разделе мы используем [диспетчера ресурсов Azure](../../azure-resource-manager/resource-group-overview.md) шаблона из открытого репозитория hello [azure — начало работы — шаблоны](https://github.com/Azure/azure-quickstart-templates).</span><span class="sxs-lookup"><span data-stu-id="53a8f-127">In this section, you'll use an [Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md) template from hello open source repository [azure-quickstart-templates](https://github.com/Azure/azure-quickstart-templates).</span></span> <span data-ttu-id="53a8f-128">Во-первых будет копировать вниз hello шаблона.</span><span class="sxs-lookup"><span data-stu-id="53a8f-128">First, you'll copy down hello template.</span></span> <span data-ttu-id="53a8f-129">Затем создадите новую пару ключей SSH для аутентификации.</span><span class="sxs-lookup"><span data-stu-id="53a8f-129">Then, you'll create a new SSH key pair for authentication.</span></span> <span data-ttu-id="53a8f-130">После этого вы настроите новый идентификатор для кластера.</span><span class="sxs-lookup"><span data-stu-id="53a8f-130">And then, you'll configure a new identifier for you cluster.</span></span> <span data-ttu-id="53a8f-131">И наконец, используйте сценарий hello или hello PowerShell скрипт tooprovision hello кластера.</span><span class="sxs-lookup"><span data-stu-id="53a8f-131">And finally, you'll use either hello Shell script or hello PowerShell script tooprovision hello cluster.</span></span>

1. <span data-ttu-id="53a8f-132">Репозиторий hello клона: [https://github.com/Azure/azure-quickstart-templates](https://github.com/Azure/azure-quickstart-templates).</span><span class="sxs-lookup"><span data-stu-id="53a8f-132">Clone hello repository: [https://github.com/Azure/azure-quickstart-templates](https://github.com/Azure/azure-quickstart-templates).</span></span>
   
        git clone https://github.com/Azure/azure-quickstart-templates
2. <span data-ttu-id="53a8f-133">Перейдите в папку toohello шаблона:</span><span class="sxs-lookup"><span data-stu-id="53a8f-133">Go toohello template folder:</span></span>
   
        cd azure-quickstart-templates\deis-cluster-coreos
3. <span data-ttu-id="53a8f-134">Создайте новую пару ключей SSH, используя ssh-keygen:</span><span class="sxs-lookup"><span data-stu-id="53a8f-134">Create a new SSH key pair using ssh-keygen:</span></span>
   
        ssh-keygen -t rsa -b 4096 -c "[your_email@domain.com]"
4. <span data-ttu-id="53a8f-135">Создайте сертификат с помощью hello выше закрытого ключа:</span><span class="sxs-lookup"><span data-stu-id="53a8f-135">Generate a certificate using hello above private key:</span></span>
   
        openssl req -x509 -days 365 -new -key [your private key file] -out [cert file toobe generated]
5. <span data-ttu-id="53a8f-136">Go слишком[https://discovery.etcd.io/new](https://discovery.etcd.io/new) toogenerate новый маркер кластера, который выглядит примерно:</span><span class="sxs-lookup"><span data-stu-id="53a8f-136">Go too[https://discovery.etcd.io/new](https://discovery.etcd.io/new) toogenerate a new cluster token, which looks something like:</span></span>
   
        https://discovery.etcd.io/6a28e078895c5ec737174db2419bb2f3
   <br />
   <span data-ttu-id="53a8f-137">Для каждого кластера CoreOS должен toohave уникального токена из этой бесплатной службой.</span><span class="sxs-lookup"><span data-stu-id="53a8f-137">Each CoreOS cluster needs toohave a unique token from this free service.</span></span> <span data-ttu-id="53a8f-138">Дополнительные сведения см. в [документации по CoreOS](https://coreos.com/docs/cluster-management/setup/cluster-discovery/).</span><span class="sxs-lookup"><span data-stu-id="53a8f-138">Please see [CoreOS documentation](https://coreos.com/docs/cluster-management/setup/cluster-discovery/) for more details.</span></span>
6. <span data-ttu-id="53a8f-139">Изменить hello **облака config.yaml** файла существующие hello tooreplace **обнаружения** токена с hello новый маркер:</span><span class="sxs-lookup"><span data-stu-id="53a8f-139">Modify hello **cloud-config.yaml** file tooreplace hello existing  **discovery** token with hello new token:</span></span>
   
        #cloud-config
        ---
        coreos:
          etcd:
            # generate a new token for each unique cluster from https://discovery.etcd.io/new
            # uncomment hello following line and replace it with your discovery URL
            discovery: https://discovery.etcd.io/3973057f670770a7628f917d58c2208a
        ...
7. <span data-ttu-id="53a8f-140">Изменение hello **azuredeploy parameters.json** файла: hello откройте сертификат, созданный на шаге 4, в текстовом редакторе.</span><span class="sxs-lookup"><span data-stu-id="53a8f-140">Modify hello **azuredeploy-parameters.json** file: Open hello certificate you created in step 4 in a text editor.</span></span> <span data-ttu-id="53a8f-141">Скопируйте весь текст между `----BEGIN CERTIFICATE-----` и `-----END CERTIFICATE-----` в hello **sshKeyData** параметра (потребуется tooremove все символы новой строки).</span><span class="sxs-lookup"><span data-stu-id="53a8f-141">Copy all text between `----BEGIN CERTIFICATE-----` and `-----END CERTIFICATE-----` into hello **sshKeyData** parameter (you'll need tooremove all newline characters).</span></span>
8. <span data-ttu-id="53a8f-142">Изменение hello **newStorageAccountName** параметра.</span><span class="sxs-lookup"><span data-stu-id="53a8f-142">Modify hello **newStorageAccountName** parameter.</span></span> <span data-ttu-id="53a8f-143">Это учетная запись хранения hello для дисков операционной системы виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="53a8f-143">This is hello storage account for VM OS disks.</span></span> <span data-ttu-id="53a8f-144">Это имя учетной записи имеет toobe глобально уникальным.</span><span class="sxs-lookup"><span data-stu-id="53a8f-144">This account name has toobe globally unique.</span></span>
9. <span data-ttu-id="53a8f-145">Изменение hello **publicDomainName** параметра.</span><span class="sxs-lookup"><span data-stu-id="53a8f-145">Modify hello **publicDomainName** parameter.</span></span> <span data-ttu-id="53a8f-146">Это значение станет частью hello DNS-имя, связанное с общедоступным IP-подсистемы балансировки нагрузки hello.</span><span class="sxs-lookup"><span data-stu-id="53a8f-146">This will become part of hello DNS name associated with hello load balancer public IP.</span></span> <span data-ttu-id="53a8f-147">Hello окончательного полное доменное имя будет иметь формат hello *[значение этого параметра]*. *[region]* . cloudapp.azure.com. Например если указать имя hello как deishbai32 и группы ресурсов hello toohello развернутой области Запад США, а затем hello окончательного deishbai32.westus.cloudapp.azure.com будет балансировки нагрузки tooyour полное доменное имя.</span><span class="sxs-lookup"><span data-stu-id="53a8f-147">hello final FQDN will have hello format of *[value of this parameter]*.*[region]*.cloudapp.azure.com. For example, if you specify hello name as deishbai32, and hello resource group is deployed toohello West US region, then hello final FQDN tooyour load balancer will be deishbai32.westus.cloudapp.azure.com.</span></span>
10. <span data-ttu-id="53a8f-148">Сохраните файл параметров hello.</span><span class="sxs-lookup"><span data-stu-id="53a8f-148">Save hello parameter file.</span></span> <span data-ttu-id="53a8f-149">И затем можно подготовить hello кластера с помощью Azure PowerShell:</span><span class="sxs-lookup"><span data-stu-id="53a8f-149">And then you can provision hello cluster using Azure PowerShell:</span></span>
    
        .\deploy-deis.ps1 -ResourceGroupName [resource group name] -ResourceGroupLocation "West US" -TemplateFile
        .\azuredeploy.json -ParametersFile .\azuredeploy-parameters.json -CloudInitFile .\cloud-config.yaml
    
    <span data-ttu-id="53a8f-150">Или с помощью Azure CLI:</span><span class="sxs-lookup"><span data-stu-id="53a8f-150">or Azure CLI:</span></span>
    
        ./deploy-deis.sh -n "[resource group name]" -l "West US" -f ./azuredeploy.json -e ./azuredeploy-parameters.json
        -c ./cloud-config.yaml  
11. <span data-ttu-id="53a8f-151">После подготовки hello группы ресурсов, можно просмотреть все ресурсы hello в группе hello на классический портал Azure.</span><span class="sxs-lookup"><span data-stu-id="53a8f-151">Once hello resource group is provisioned, you can see all hello resources in hello group on Azure classic portal.</span></span> <span data-ttu-id="53a8f-152">Как показано на следующий снимок экрана, hello hello, группа ресурсов содержит виртуальную сеть с трех виртуальных машин, которые являются объединить toohello одной группе доступности.</span><span class="sxs-lookup"><span data-stu-id="53a8f-152">As shown in hello following screenshot, hello resource group contains a virtual network with three VMs, which are joined toohello same availability set.</span></span> <span data-ttu-id="53a8f-153">Группа Hello также содержит подсистему балансировки нагрузки, имеющая связанный общедоступный IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="53a8f-153">hello group also contains a load balancer, which has an associated public IP.</span></span>
    
    ![Группа ресурсов на классический портал Azure подготовлена Hello](./media/deis-cluster/resource-group.png)

## <a name="install-hello-client"></a><span data-ttu-id="53a8f-155">Установка клиента на приветствия</span><span class="sxs-lookup"><span data-stu-id="53a8f-155">Install hello client</span></span>
<span data-ttu-id="53a8f-156">Требуется **deisctl** toocontrol вашей Deis кластера.</span><span class="sxs-lookup"><span data-stu-id="53a8f-156">You need **deisctl** toocontrol your Deis cluster.</span></span> <span data-ttu-id="53a8f-157">Несмотря на то, что deisctl автоматически устанавливается на всех узлах кластера hello, это deisctl toouse рекомендаций на отдельном компьютере правами администратора.</span><span class="sxs-lookup"><span data-stu-id="53a8f-157">Although deisctl is automatically installed in all hello cluster nodes, it's a good practice toouse deisctl on a separate administrative machine.</span></span> <span data-ttu-id="53a8f-158">Кроме того так как все узлы должны быть настроены только частные IP-адреса, вам потребуется toouse туннелирования SSH с помощью подсистемы балансировки нагрузки hello, имеющая общедоступный IP-адрес, узел машины tooconnect toohello.</span><span class="sxs-lookup"><span data-stu-id="53a8f-158">Furthermore, because all nodes are configured with only private IP addresses, you'll need toouse SSH tunneling through hello load balancer, which has a public IP, tooconnect toohello node machines.</span></span> <span data-ttu-id="53a8f-159">Hello ниже приведены hello шаги по настройке deisctl на отдельном Ubuntu физической или виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="53a8f-159">hello following are hello steps of setting up deisctl on a separate Ubuntu physical or virtual machine.</span></span>

1. <span data-ttu-id="53a8f-160">Установите deisctl:mkdir deis:</span><span class="sxs-lookup"><span data-stu-id="53a8f-160">Install deisctl:mkdir deis</span></span>
   
        cd deis
        curl -sSL http://deis.io/deisctl/install.sh | sh -s 1.6.1
        sudo ln -fs $PWD/deisctl /usr/local/bin/deisctl
2. <span data-ttu-id="53a8f-161">Добавление агента toossh закрытого ключа:</span><span class="sxs-lookup"><span data-stu-id="53a8f-161">Add your private key toossh agent:</span></span>
   
        eval `ssh-agent -s`
        ssh-add [path toohello private key file, see step 1 in hello previous section]
3. <span data-ttu-id="53a8f-162">Настройте deisctl:</span><span class="sxs-lookup"><span data-stu-id="53a8f-162">Configure deisctl:</span></span>
   
        export DEISCTL_TUNNEL=[public ip of hello load balancer]:2223

<span data-ttu-id="53a8f-163">Hello шаблон определяет NAT правила для входящих подключений, которые сопоставляют 2223 tooinstance 1, 2224 tooinstance 2 и 2225 tooinstance 3.</span><span class="sxs-lookup"><span data-stu-id="53a8f-163">hello template defines inbound NAT rules that map 2223 tooinstance 1, 2224 tooinstance 2, and 2225 tooinstance 3.</span></span> <span data-ttu-id="53a8f-164">Это обеспечивает избыточность для использования инструмента deisctl hello.</span><span class="sxs-lookup"><span data-stu-id="53a8f-164">This provides redundancy for using hello deisctl tool.</span></span> <span data-ttu-id="53a8f-165">Можно просмотреть эти правила на классическом портале Azure.</span><span class="sxs-lookup"><span data-stu-id="53a8f-165">You can examine these rules on Azure classic portal:</span></span>

![Подсистема балансировки нагрузки правила NAT на hello](./media/deis-cluster/nat-rules.png)

> [!NOTE]
> <span data-ttu-id="53a8f-167">В настоящее время шаблона hello поддерживает только 3 узлов кластеров.</span><span class="sxs-lookup"><span data-stu-id="53a8f-167">Currently hello template only supports 3-node clusters.</span></span> <span data-ttu-id="53a8f-168">Это связано с ограничением в определении правил NAT шаблона диспетчера ресурсов Azure, которое не позволяет использовать синтаксис цикла.</span><span class="sxs-lookup"><span data-stu-id="53a8f-168">This is because of a limitation in Azure Resource Manager template NAT rule definition, which doesn’t support loop syntax.</span></span>
> 
> 

## <a name="install-and-start-hello-deis-platform"></a><span data-ttu-id="53a8f-169">Установка и запуск hello Deis платформы</span><span class="sxs-lookup"><span data-stu-id="53a8f-169">Install and start hello Deis platform</span></span>
<span data-ttu-id="53a8f-170">Теперь можно использовать deisctl tooinstall и запустить hello Deis платформа:</span><span class="sxs-lookup"><span data-stu-id="53a8f-170">Now you can use deisctl tooinstall and start hello Deis platform:</span></span>

    deisctl config platform set domain=[some domain]
    deisctl config platform set sshPrivateKey=[path toohello private key file]
    deisctl install platform
    deisctl start platform

> [!NOTE]
> <span data-ttu-id="53a8f-171">Начальный платформы hello занимает некоторое время (до 10 минут).</span><span class="sxs-lookup"><span data-stu-id="53a8f-171">Starting hello platform takes a while (as much as 10 minutes).</span></span> <span data-ttu-id="53a8f-172">Особенно запуск hello построитель службы может занять много времени.</span><span class="sxs-lookup"><span data-stu-id="53a8f-172">Especially, starting hello builder service can take a long time.</span></span> <span data-ttu-id="53a8f-173">Иногда занимает несколько попыток toosucceed: Если hello операции toohang, попробуйте ввести `ctrl+c` toobreak выполнения команды hello и повторите попытку.</span><span class="sxs-lookup"><span data-stu-id="53a8f-173">And sometimes it takes a few tries toosucceed: If hello operation seems toohang, try typing `ctrl+c` toobreak execution of hello command and retry.</span></span>
> 
> 

<span data-ttu-id="53a8f-174">Можно использовать `deisctl list` tooverify, если все службы запущены:</span><span class="sxs-lookup"><span data-stu-id="53a8f-174">You can use `deisctl list` tooverify if all services are running:</span></span>

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

<span data-ttu-id="53a8f-175">Поздравляем!</span><span class="sxs-lookup"><span data-stu-id="53a8f-175">Congratulations!</span></span> <span data-ttu-id="53a8f-176">Теперь у вас есть работающий кластер Deis в Azure!</span><span class="sxs-lookup"><span data-stu-id="53a8f-176">Now you've got a running Deis clsuter on Azure!</span></span> <span data-ttu-id="53a8f-177">Теперь давайте развернуть пример Go приложения toosee hello кластера в действии.</span><span class="sxs-lookup"><span data-stu-id="53a8f-177">Next, let's deploy a sample Go application toosee hello cluster in action.</span></span>

## <a name="deploy-and-scale-a-hello-world-application"></a><span data-ttu-id="53a8f-178">Развертывание и масштабирование приложения Hello World</span><span class="sxs-lookup"><span data-stu-id="53a8f-178">Deploy and scale a Hello World application</span></span>
<span data-ttu-id="53a8f-179">Hello следующие шаги показывают, как toodeploy «Hello World» Go кластера toohello приложения.</span><span class="sxs-lookup"><span data-stu-id="53a8f-179">hello following steps show how toodeploy a "Hello World" Go application toohello cluster.</span></span> <span data-ttu-id="53a8f-180">на основе действия Hello [Deis документации](http://docs.deis.io/en/latest/using_deis/using-dockerfiles/#using-dockerfiles).</span><span class="sxs-lookup"><span data-stu-id="53a8f-180">hello steps are based on [Deis documentation](http://docs.deis.io/en/latest/using_deis/using-dockerfiles/#using-dockerfiles).</span></span>

1. <span data-ttu-id="53a8f-181">Для маршрутизации toowork сетки hello надлежащим образом, вам потребуется toohave запись A подстановочный знак для вашего домена, указывающий toohello общедоступный IP-адрес подсистемы балансировки нагрузки hello.</span><span class="sxs-lookup"><span data-stu-id="53a8f-181">For hello routing mesh toowork properly, you’ll need toohave a wildcard A record for your domain pointing toohello public IP of hello load balancer.</span></span> <span data-ttu-id="53a8f-182">Hello следующем снимке экрана показана запись hello A для регистрации домена образец на GoDaddy:</span><span class="sxs-lookup"><span data-stu-id="53a8f-182">hello following screenshot shows hello A record for a sample domain registration on GoDaddy:</span></span>
   
    ![Запись A Godaddy](./media/deis-cluster/go-daddy.png)
   
   <p />
2. <span data-ttu-id="53a8f-184">Установите deis:</span><span class="sxs-lookup"><span data-stu-id="53a8f-184">Install deis:</span></span>
   
        mkdir deis
        cd deis
        curl -sSL http://deis.io/deis-cli/install.sh | sh
        ln -fs $PWD/deis /usr/local/bin/deis
3. <span data-ttu-id="53a8f-185">Создание нового ключа SSH, а затем добавьте открытого ключа tooGitHub hello (Конечно, можно также повторно использовать существующие ключи).</span><span class="sxs-lookup"><span data-stu-id="53a8f-185">Create a new SSH key, and then add hello public key tooGitHub (of course, you can also reuse your existing keys).</span></span> <span data-ttu-id="53a8f-186">toocreate новую пару ключей SSH, используйте:</span><span class="sxs-lookup"><span data-stu-id="53a8f-186">toocreate a new SSH key pair, use:</span></span>
   
        cd ~/.ssh
        ssh-keygen (press [Enter]s toouse default file names and empty passcode)
4. <span data-ttu-id="53a8f-187">Добавьте id_rsa.pub или открытый ключ hello по своему усмотрению, tooGitHub.</span><span class="sxs-lookup"><span data-stu-id="53a8f-187">Add id_rsa.pub, or hello public key of your choice, tooGitHub.</span></span> <span data-ttu-id="53a8f-188">Это можно сделать с помощью hello добавить SSH ключа кнопки на экране настройки ключей SSH:</span><span class="sxs-lookup"><span data-stu-id="53a8f-188">You can do this by using hello Add SSH key button in your SSH keys configuration screen:</span></span>
   
   ![Ключ GitHub](./media/deis-cluster/github-key.png)
   
   <p />
5. <span data-ttu-id="53a8f-190">Зарегистрируйте нового пользователя:</span><span class="sxs-lookup"><span data-stu-id="53a8f-190">Register a new user:</span></span>
   
        deis register http://deis.[your domain]
   <p />
6. <span data-ttu-id="53a8f-191">Добавьте hello SSH-ключ:</span><span class="sxs-lookup"><span data-stu-id="53a8f-191">Add hello SSH key:</span></span>
   
        deis keys:add [path tooyour SSH public key]
   <p />      
7. <span data-ttu-id="53a8f-192">Создайте приложение:</span><span class="sxs-lookup"><span data-stu-id="53a8f-192">Create an application.</span></span>
   
        git clone https://github.com/deis/helloworld.git
        cd helloworld
        deis create
        git push deis master
   <p /><span data-ttu-id="53a8f-193">
8.Отправка git Hello активируют Docker изображения toobe построения и развертывания, который может занять несколько минут.</span><span class="sxs-lookup"><span data-stu-id="53a8f-193">
8. hello git push will trigger Docker images toobe built and deployed, which will take a few minutes.</span></span> <span data-ttu-id="53a8f-194">Из Мои возможности в некоторых случаях шаг 10 (Pushing tooprivate репозитория образов) может зависнуть.</span><span class="sxs-lookup"><span data-stu-id="53a8f-194">From my experience, occasionally, Step 10 (Pushing image tooprivate repository) may hang.</span></span> <span data-ttu-id="53a8f-195">В этом случае вы можете остановить процесс hello приложения hello удалить с помощью "deis приложений: уничтожить <application name> ` tooremove hello application and try again. You can use `deis apps:list" toofind hello имя приложения.</span><span class="sxs-lookup"><span data-stu-id="53a8f-195">When this happens, you can stop hello process, remove hello application using `deis apps:destroy –a <application name>` tooremove hello application and try again. You can use `deis apps:list` toofind out hello name of your application.</span></span> <span data-ttu-id="53a8f-196">Если все работает, вы увидите нечто похожее на следующее hello в конце hello выходные данные команды:</span><span class="sxs-lookup"><span data-stu-id="53a8f-196">If everything works out, you should see something like hello following at hello end of command outputs:</span></span>
   
        -----> Launching...
               done, lambda-underdog:v2 deployed tooDeis
               http://lambda-underdog.artitrack.com
               toolearn more, use `deis help` or visit http://deis.io
        toossh://git@deis.artitrack.com:2222/lambda-underdog.git
         * [new branch]      master -> master
   <p />
9. <span data-ttu-id="53a8f-197">Проверьте, работает ли приложение hello.</span><span class="sxs-lookup"><span data-stu-id="53a8f-197">Verify if hello application is working:</span></span>
   
        curl -S http://[your application name].[your domain]
   <span data-ttu-id="53a8f-198">Вы должны увидеть следующее:</span><span class="sxs-lookup"><span data-stu-id="53a8f-198">You should see:</span></span>
   
        Welcome tooDeis!
        See hello documentation at http://docs.deis.io/ for more information.
        (you can use geis apps:list tooget hello name of your application).
   <p />
10. <span data-ttu-id="53a8f-199">Масштабирование экземпляров too3 приложения hello:</span><span class="sxs-lookup"><span data-stu-id="53a8f-199">Scale hello application too3 instances:</span></span>
    
        deis scale cmd=3
    <p />
11. <span data-ttu-id="53a8f-200">При необходимости можно использовать deis сведения подробности tooexamine приложения.</span><span class="sxs-lookup"><span data-stu-id="53a8f-200">Optionally, you can use deis info tooexamine details of your application.</span></span> <span data-ttu-id="53a8f-201">Hello следующие выходные данные приведены из моей развертывания приложения.</span><span class="sxs-lookup"><span data-stu-id="53a8f-201">hello following outputs are from my application deployment:</span></span>
    
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

## <a name="next-steps"></a><span data-ttu-id="53a8f-202">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="53a8f-202">Next Steps</span></span>
<span data-ttu-id="53a8f-203">В этой статье подробно описан все tooprovision действия hello Deis новый кластер в Azure с помощью шаблона диспетчера ресурсов Azure.</span><span class="sxs-lookup"><span data-stu-id="53a8f-203">This article walked you through all hello steps tooprovision a new Deis cluster on Azure using an Azure Resource Manager template.</span></span> <span data-ttu-id="53a8f-204">шаблон Hello поддерживает избыточность подключений, а также балансировку нагрузки для развернутых приложений для работы с проектами.</span><span class="sxs-lookup"><span data-stu-id="53a8f-204">hello template supports redundancy in tooling connections as well as load balancing for deployed applications.</span></span> <span data-ttu-id="53a8f-205">шаблон Hello также позволяет избежать с помощью общедоступных IP-адресов на узлы элементов, которые обеспечивает экономию ценное открытый IP и предоставляет более безопасной среде toohost приложений.</span><span class="sxs-lookup"><span data-stu-id="53a8f-205">hello template also avoids using public IPs on member nodes, which saves precious public IP resources and provides a more secured environment toohost applications.</span></span> <span data-ttu-id="53a8f-206">toolearn более, см. следующие статьи hello.</span><span class="sxs-lookup"><span data-stu-id="53a8f-206">toolearn more, see hello following articles:</span></span>

<span data-ttu-id="53a8f-207">[Общие сведения о диспетчере ресурсов Azure][resource-group-overview]</span><span class="sxs-lookup"><span data-stu-id="53a8f-207">[Azure Resource Manager Overview][resource-group-overview]</span></span>  
<span data-ttu-id="53a8f-208">[Как toouse hello Azure CLI][azure-command-line-tools]</span><span class="sxs-lookup"><span data-stu-id="53a8f-208">[How toouse hello Azure CLI][azure-command-line-tools]</span></span>  
<span data-ttu-id="53a8f-209">[Использование Azure PowerShell с Azure Resource Manager][powershell-azure-resource-manager]</span><span class="sxs-lookup"><span data-stu-id="53a8f-209">[Using Azure PowerShell with Azure Resource Manager][powershell-azure-resource-manager]</span></span>  

[azure-command-line-tools]: ../../cli-install-nodejs.md
[resource-group-overview]: ../../azure-resource-manager/resource-group-overview.md
[powershell-azure-resource-manager]: ../../azure-resource-manager/powershell-azure-resource-manager.md
