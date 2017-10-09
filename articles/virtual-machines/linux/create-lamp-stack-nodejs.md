---
title: "aaaDeploy LAMP на виртуальной машине Linux с hello Azure CLI 1.0 | Документы Microsoft"
description: "Узнайте, как tooinstall hello LAMP стека на виртуальной Машине Linux в Azure"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: jluk
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 6c12603a-e391-4d3e-acce-442dd7ebb2fe
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: NA
ms.topic: article
ms.date: 2/21/2017
ms.author: juluk
ms.openlocfilehash: e78a82d388ce68710933b9b673aa1b2460bdbb14
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-lamp-stack-with-hello-azure-cli-10"></a><span data-ttu-id="07afe-103">Развертывание стек LAMP с hello Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="07afe-103">Deploy LAMP stack with hello Azure CLI 1.0</span></span>
<span data-ttu-id="07afe-104">В этой статье рассматриваются как toodeploy Apache веб-сервера, MySQL и PHP (стек LAMP hello) в Azure.</span><span class="sxs-lookup"><span data-stu-id="07afe-104">This article walks you through how toodeploy an Apache web server, MySQL, and PHP (hello LAMP stack) on Azure.</span></span> <span data-ttu-id="07afe-105">Необходима учетная запись Azure ([получить бесплатную пробную версию](https://azure.microsoft.com/pricing/free-trial/)) и hello [Azure CLI](../../cli-install-nodejs.md) , [подключен tooyour учетная запись Azure](../../xplat-cli-connect.md).</span><span class="sxs-lookup"><span data-stu-id="07afe-105">You need an Azure Account ([get a free trial](https://azure.microsoft.com/pricing/free-trial/)) and hello [Azure CLI](../../cli-install-nodejs.md) that is [connected tooyour Azure account](../../xplat-cli-connect.md).</span></span>

## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="07afe-106">Задача hello toocomplete версии CLI</span><span class="sxs-lookup"><span data-stu-id="07afe-106">CLI versions toocomplete hello task</span></span>
<span data-ttu-id="07afe-107">Можно выполнить с помощью одного из следующих версий CLI hello задачу hello.</span><span class="sxs-lookup"><span data-stu-id="07afe-107">You can complete hello task using one of hello following CLI versions:</span></span>

- <span data-ttu-id="07afe-108">[Azure CLI 1.0] — нашей CLI для hello классический и ресурса управления развертывания моделей (в этой статье)</span><span class="sxs-lookup"><span data-stu-id="07afe-108">[Azure CLI 1.0] – our CLI for hello classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="07afe-109">[Azure CLI 2.0](create-lamp-stack.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) -нашей нового поколения CLI для модели развертывания hello ресурсов управления</span><span class="sxs-lookup"><span data-stu-id="07afe-109">[Azure CLI 2.0](create-lamp-stack.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) - our next generation CLI for hello resource management deployment model</span></span>

```
# One command toocreate a resource group holding a VM with LAMP already on it
$ azure group create -n uniqueResourceGroup -l westus --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/lamp-app/azuredeploy.json
```

* <span data-ttu-id="07afe-110">Развертывание LAMP на существующей виртуальной машине</span><span class="sxs-lookup"><span data-stu-id="07afe-110">Deploy LAMP on existing VM</span></span>

```
# Two commands: one updates packages, hello other installs Apache, MySQL, and PHP
user@ubuntu$ sudo apt-get update
user@ubuntu$ sudo apt-get install apache2 mysql-server php5 php5-mysql
```

## <a name="deploy-lamp-on-new-vm-walkthrough"></a><span data-ttu-id="07afe-111">Пошаговое руководство по развертыванию LAMP на новой виртуальной машине</span><span class="sxs-lookup"><span data-stu-id="07afe-111">Deploy LAMP on new VM walkthrough</span></span>
<span data-ttu-id="07afe-112">Сначала нужно создать [группы ресурсов](../../azure-resource-manager/resource-group-overview.md) , содержащий hello новой виртуальной Машины:</span><span class="sxs-lookup"><span data-stu-id="07afe-112">You can start by creating a [resource group](../../azure-resource-manager/resource-group-overview.md) that will contain hello new VM:</span></span>

    $ azure group create uniqueResourceGroup westus
    info:    Executing command group create
    info:    Getting resource group uniqueResourceGroup
    info:    Creating resource group uniqueResourceGroup
    info:    Created resource group uniqueResourceGroup
    data:    Id:                  /subscriptions/########-####-####-####-############/resourceGroups/uniqueResourceGroup
    data:    Name:                uniqueResourceGroup
    data:    Location:            westus
    data:    Provisioning State:  Succeeded
    data:    Tags: null
    data:
    info:    group create command OK

<span data-ttu-id="07afe-113">toocreate Здравствуйте самой ВМ, уже написанный найден шаблон диспетчера ресурсов Azure можно использовать [здесь на GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/lamp-app).</span><span class="sxs-lookup"><span data-stu-id="07afe-113">toocreate hello VM itself, you can use an already written Azure Resource Manager template found [here on GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/lamp-app).</span></span>

    $ azure group deployment create --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/lamp-app/azuredeploy.json uniqueResourceGroup uniqueLampName

<span data-ttu-id="07afe-114">Вы увидите запрос на ввод дополнительных данных.</span><span class="sxs-lookup"><span data-stu-id="07afe-114">You should see a response prompting some more inputs:</span></span>

    info:    Executing command group deployment create
    info:    Supply values for hello following parameters
    storageAccountNamePrefix: lampprefix
    location: westus
    adminUsername: someUsername
    adminPassword: somePassword
    mySqlPassword: somePassword
    dnsLabelPrefix: azlamptest
    info:    Initializing template configurations and parameters
    info:    Creating a deployment
    info:    Created template deployment "uniqueLampName"
    info:    Waiting for deployment toocomplete
    data:    DeploymentName     : uniqueLampName
    data:    ResourceGroupName  : uniqueResourceGroup
    data:    ProvisioningState  : Succeeded
    data:    Timestamp          :
    data:    Mode               : Incremental
    data:    CorrelationId      : d51bbf3c-88f1-4cf3-a8b3-942c6925f381
    data:    TemplateLink       : https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/lamp-app/azuredeploy.json
    data:    ContentVersion     : 1.0.0.0
    data:    DeploymentParameters :
    data:    Name                      Type          Value
    data:    ------------------------  ------------  -----------
    data:    storageAccountNamePrefix  String        lampprefix
    data:    location                  String        westus
    data:    adminUsername             String        someUsername
    data:    adminPassword             SecureString  undefined
    data:    mySqlPassword             SecureString  undefined
    data:    dnsLabelPrefix            String        azlamptest
    data:    ubuntuOSVersion           String        14.04.2-LTS
    info:    group deployment create command OK

<span data-ttu-id="07afe-115">Вы создали виртуальную машину Linux с установленным стеком LAMP.</span><span class="sxs-lookup"><span data-stu-id="07afe-115">You have now created a Linux VM with LAMP already installed on it.</span></span> <span data-ttu-id="07afe-116">При желании можно проверить hello установки посредством перехода вниз слишком[проверьте ЛАМПОЧКА успешно установлен](#verify-lamp-successfully-installed).</span><span class="sxs-lookup"><span data-stu-id="07afe-116">If you wish, you can verify hello install by jumping down too[Verify LAMP Successfully Installed](#verify-lamp-successfully-installed).</span></span>

## <a name="deploy-lamp-on-existing-vm-walkthrough"></a><span data-ttu-id="07afe-117">Пошаговое руководство по развертыванию LAMP на существующей виртуальной машине</span><span class="sxs-lookup"><span data-stu-id="07afe-117">Deploy LAMP on existing VM walkthrough</span></span>
<span data-ttu-id="07afe-118">Если требуется помощь для создания виртуальной Машины Linux можно head [здесь toolearn как toocreate ВМ Linux](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="07afe-118">If you need help creating a Linux VM, you can head [here toolearn how toocreate a Linux VM](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="07afe-119">Далее необходимо tooSSH в hello виртуальной Машины с Linux.</span><span class="sxs-lookup"><span data-stu-id="07afe-119">Next, you need tooSSH into hello Linux VM.</span></span> <span data-ttu-id="07afe-120">Если вам нужна помощь с созданием SSH-ключ, можно head [здесь toolearn как toocreate ключа SSH в Linux или Mac](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="07afe-120">If you need help with creating an SSH key, you can head [here toolearn how toocreate an SSH key on Linux/Mac](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
<span data-ttu-id="07afe-121">Если у вас же имеется ключ SSH, продолжайте процедуру и, используя командную строку, подключитесь по протоколу SSH к виртуальной машине Linux с помощью команды `ssh exampleUsername@exampleDNS`.</span><span class="sxs-lookup"><span data-stu-id="07afe-121">If you have an SSH key already, go ahead and SSH from your command line into your Linux VM with `ssh exampleUsername@exampleDNS`.</span></span>

<span data-ttu-id="07afe-122">Теперь, когда вы работаете в ВМ Linux, мы пошаговую установку стек LAMP hello на основе Debian распределения.</span><span class="sxs-lookup"><span data-stu-id="07afe-122">Now that you are working within your Linux VM, we can walk through installing hello LAMP stack on Debian-based distributions.</span></span> <span data-ttu-id="07afe-123">конкретные команды Hello могут отличаться в других дистрибутивах Linux.</span><span class="sxs-lookup"><span data-stu-id="07afe-123">hello exact commands might differ for other Linux distros.</span></span>

#### <a name="installing-on-debianubuntu"></a><span data-ttu-id="07afe-124">Установка на Debian или Ubuntu</span><span class="sxs-lookup"><span data-stu-id="07afe-124">Installing on Debian/Ubuntu</span></span>
<span data-ttu-id="07afe-125">Требуются следующие пакеты, установленные hello: `apache2`, `mysql-server`, `php5`, и `php5-mysql`.</span><span class="sxs-lookup"><span data-stu-id="07afe-125">You need hello following packages installed: `apache2`, `mysql-server`, `php5`, and `php5-mysql`.</span></span> <span data-ttu-id="07afe-126">Их можно установить, перетащив вручную или воспользовавшись Tasksel.</span><span class="sxs-lookup"><span data-stu-id="07afe-126">You can install these packages by directly grabbing these packages or using Tasksel.</span></span> <span data-ttu-id="07afe-127">Ниже приведены указания для обоих способов.</span><span class="sxs-lookup"><span data-stu-id="07afe-127">Instructions for both options are listed below.</span></span>
<span data-ttu-id="07afe-128">Перед установкой требуется toodownload и обновление списков пакета.</span><span class="sxs-lookup"><span data-stu-id="07afe-128">Before installing you need toodownload and update package lists.</span></span>

    user@ubuntu$ sudo apt-get update

##### <a name="individual-packages"></a><span data-ttu-id="07afe-129">Установка отдельных пакетов</span><span class="sxs-lookup"><span data-stu-id="07afe-129">Individual packages</span></span>
<span data-ttu-id="07afe-130">Можно использовать apt-get.</span><span class="sxs-lookup"><span data-stu-id="07afe-130">Using apt-get:</span></span>

    user@ubuntu$ sudo apt-get install apache2 mysql-server php5 php5-mysql

##### <a name="using-tasksel"></a><span data-ttu-id="07afe-131">Установка с помощью Tasksel</span><span class="sxs-lookup"><span data-stu-id="07afe-131">Using tasksel</span></span>
<span data-ttu-id="07afe-132">В качестве альтернативы можно скачать Tasksel. Это инструмент Debian и Ubuntu, который устанавливает в систему несколько связанных пакетов в рамках одной скоординированной задачи.</span><span class="sxs-lookup"><span data-stu-id="07afe-132">Alternatively you can download Tasksel, a Debian/Ubuntu tool that installs multiple related packages as a coordinated "task" onto your system.</span></span>

    user@ubuntu$ sudo apt-get install tasksel
    user@ubuntu$ sudo tasksel install lamp-server

<span data-ttu-id="07afe-133">После выполнения любого из предыдущих параметров hello, будет иметь запрашиваемые tooinstall эти пакеты и другие зависимости.</span><span class="sxs-lookup"><span data-stu-id="07afe-133">After running either of hello previous options, you will be prompted tooinstall these packages and various other dependencies.</span></span> <span data-ttu-id="07afe-134">Нажмите «y», а затем toocontinue «Ввод» и выполните любые другие запросы tooset пароля администратора для MySQL.</span><span class="sxs-lookup"><span data-stu-id="07afe-134">Press 'y' and then 'Enter' toocontinue, and follow any other prompts tooset an administrative password for MySQL.</span></span> <span data-ttu-id="07afe-135">При этом устанавливаются hello минимальные необходимые PHP необходимые расширения toouse PHP с MySQL.</span><span class="sxs-lookup"><span data-stu-id="07afe-135">This installs hello minimum required PHP extensions needed toouse PHP with MySQL.</span></span> 

![][1]

<span data-ttu-id="07afe-136">Выполните следующие команды toosee hello другие расширения PHP, которые доступны в виде пакетов.</span><span class="sxs-lookup"><span data-stu-id="07afe-136">Run hello following command toosee other PHP extensions that are available as packages:</span></span>

    user@ubuntu$ apt-cache search php5


#### <a name="create-infophp-document"></a><span data-ttu-id="07afe-137">Создание документа info.php</span><span class="sxs-lookup"><span data-stu-id="07afe-137">Create info.php document</span></span>
<span data-ttu-id="07afe-138">Теперь должен быть доступ toocheck версии Apache, PHP и MySQL имеется через командную строку hello, введя `apache2 -v`, `mysql -v`, или `php -v`.</span><span class="sxs-lookup"><span data-stu-id="07afe-138">You should now be able toocheck what version of Apache, MySQL, and PHP you have through hello command line by typing `apache2 -v`, `mysql -v`, or `php -v`.</span></span>

<span data-ttu-id="07afe-139">Если вы бы как tootest Далее, можно создать быстрый tooview страницы сведения о PHP в браузере.</span><span class="sxs-lookup"><span data-stu-id="07afe-139">If you would like tootest further, you can create a quick PHP info page tooview in a browser.</span></span> <span data-ttu-id="07afe-140">Создайте файл в текстовом редакторе Nano с помощью следующей команды.</span><span class="sxs-lookup"><span data-stu-id="07afe-140">Create a file with Nano text editor with this command:</span></span>

    user@ubuntu$ sudo nano /var/www/html/info.php

<span data-ttu-id="07afe-141">В текстовом редакторе GNU Nano hello добавьте hello следующие строки:</span><span class="sxs-lookup"><span data-stu-id="07afe-141">Within hello GNU Nano text editor, add hello following lines:</span></span>

    <?php
    phpinfo();
    ?>

<span data-ttu-id="07afe-142">Сохраните и закройте редактор текста hello.</span><span class="sxs-lookup"><span data-stu-id="07afe-142">Then save and exit hello text editor.</span></span>

<span data-ttu-id="07afe-143">Перезапустите Apache с помощью следующей команды, чтобы все новые установленные компоненты вступили в действие.</span><span class="sxs-lookup"><span data-stu-id="07afe-143">Restart Apache with this command so all new installs take effect.</span></span>

    user@ubuntu$ sudo service apache2 restart

## <a name="verify-lamp-successfully-installed"></a><span data-ttu-id="07afe-144">Проверка успешности установки LAMP</span><span class="sxs-lookup"><span data-stu-id="07afe-144">Verify LAMP successfully installed</span></span>
<span data-ttu-id="07afe-145">Теперь можно проверить hello PHP info созданная страница, открыв браузер и переходит в toohttp://youruniqueDNS/info.php.</span><span class="sxs-lookup"><span data-stu-id="07afe-145">Now you can check hello PHP info page you created by opening a browser and going toohttp://youruniqueDNS/info.php.</span></span> <span data-ttu-id="07afe-146">Он должен выглядеть примерно toothis изображения.</span><span class="sxs-lookup"><span data-stu-id="07afe-146">It should look similar toothis image.</span></span>

![][2]

<span data-ttu-id="07afe-147">Apache установки можно проверить, просмотрев hello страница по умолчанию Apache2 Ubuntu последовательно выбрав tooyou http://youruniqueDNS/.</span><span class="sxs-lookup"><span data-stu-id="07afe-147">You can check your Apache installation by viewing hello Apache2 Ubuntu Default Page by going tooyou http://youruniqueDNS/.</span></span> <span data-ttu-id="07afe-148">Должна отобразиться страница следующего вида.</span><span class="sxs-lookup"><span data-stu-id="07afe-148">You should see something like this image.</span></span>

![][3]

<span data-ttu-id="07afe-149">Поздравляем! Вы установили стек LAMP на виртуальную машину Azure.</span><span class="sxs-lookup"><span data-stu-id="07afe-149">Congratulations, you have just setup a LAMP stack on your Azure VM!</span></span>

## <a name="next-steps"></a><span data-ttu-id="07afe-150">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="07afe-150">Next steps</span></span>
<span data-ttu-id="07afe-151">Проверьте hello документации Ubuntu стек LAMP hello.</span><span class="sxs-lookup"><span data-stu-id="07afe-151">Check out hello Ubuntu documentation on hello LAMP stack:</span></span>

* [<span data-ttu-id="07afe-152">https://help.ubuntu.com/community/ApacheMySQLPHP</span><span class="sxs-lookup"><span data-stu-id="07afe-152">https://help.ubuntu.com/community/ApacheMySQLPHP</span></span>](https://help.ubuntu.com/community/ApacheMySQLPHP)

[1]: ./media/deploy-lamp-stack/configmysqlpassword-small.png
[2]: ./media/deploy-lamp-stack/phpsuccesspage.png
[3]: ./media/deploy-lamp-stack/apachesuccesspage.png