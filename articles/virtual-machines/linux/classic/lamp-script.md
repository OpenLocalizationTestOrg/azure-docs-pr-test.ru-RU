---
title: "Расширение CustomScript на виртуальной Машине Linux hello aaaUse | Документы Microsoft"
description: "Узнайте, как toodeploy расширения приложений на виртуальных машин Linux в Azure toouse hello CustomScript созданной hello классической модели развертывания."
editor: tysonn
manager: timlt
documentationcenter: 
services: virtual-machines-linux
author: gbowerman
tags: azure-service-management
ms.assetid: e535241d-feca-4412-b07a-67c936ba88a0
ms.service: virtual-machines-linux
ms.workload: multiple
ms.tgt_pltfrm: linux
ms.devlang: na
ms.topic: article
ms.date: 06/01/2017
ms.author: guybo
ms.openlocfilehash: 864a586e70093eefbabc065a3c05e1cf9e315704
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-lamp-app-using-hello-azure-customscript-extension-for-linux"></a><span data-ttu-id="7a5c6-103">Развертывание приложения ИНДИКАТОРА с помощью hello расширение CustomScript Azure для Linux</span><span class="sxs-lookup"><span data-stu-id="7a5c6-103">Deploy a LAMP app using hello Azure CustomScript Extension for Linux</span></span>
> [!IMPORTANT] 
> <span data-ttu-id="7a5c6-104">В Azure предлагаются две модели развертывания для создания ресурсов и работы с ними: [модель диспетчера ресурсов и классическая модель](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="7a5c6-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="7a5c6-105">В этой статье описан с помощью hello классической модели развертывания.</span><span class="sxs-lookup"><span data-stu-id="7a5c6-105">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="7a5c6-106">Корпорация Майкрософт рекомендует наиболее новые развертывания модели hello диспетчера ресурсов.</span><span class="sxs-lookup"><span data-stu-id="7a5c6-106">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="7a5c6-107">Сведения о развертывании стек LAMP, с помощью модели hello диспетчера ресурсов см. в разделе [здесь](../tutorial-lamp-stack.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="7a5c6-107">For information about deploying a LAMP stack using hello Resource Manager model, see [here](../tutorial-lamp-stack.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="7a5c6-108">Hello расширения CustomScript Microsoft Azure для Linux обеспечивает toocustomize способом виртуальных машин (ВМ), запустив произвольный код, написанный на любом языке сценариев, поддерживаемых hello виртуальной Машины (например, Python и Bash).</span><span class="sxs-lookup"><span data-stu-id="7a5c6-108">hello Microsoft Azure CustomScript Extension for Linux provides a way toocustomize your virtual machines (VMs) by running arbitrary code written in any scripting language supported by hello VM (for example, Python, and Bash).</span></span> <span data-ttu-id="7a5c6-109">Это обеспечивает tooautomate очень гибкий способ машины toomultiple развертывания приложения.</span><span class="sxs-lookup"><span data-stu-id="7a5c6-109">This provides a very flexible way tooautomate application deployment toomultiple machines.</span></span>

<span data-ttu-id="7a5c6-110">Hello расширение CustomScript можно развернуть с помощью hello портал Azure, Windows PowerShell или hello Azure командной строки (CLI Azure).</span><span class="sxs-lookup"><span data-stu-id="7a5c6-110">You can deploy hello CustomScript Extension using hello Azure portal, Windows PowerShell, or hello Azure Command-Line Interface (Azure CLI).</span></span>

<span data-ttu-id="7a5c6-111">В этой статье мы будем использовать toodeploy hello Azure CLI простого приложения tooan LAMP Ubuntu ВМ создан с помощью hello классической модели развертывания.</span><span class="sxs-lookup"><span data-stu-id="7a5c6-111">In this article we'll use hello Azure CLI toodeploy a simple LAMP application tooan Ubuntu VM created using hello classic deployment model.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7a5c6-112">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="7a5c6-112">Prerequisites</span></span>
<span data-ttu-id="7a5c6-113">Для этого примера создайте две виртуальные машины Azure под управлением Ubuntu 14.04 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="7a5c6-113">For this example, first create two Azure VMs running Ubuntu 14.04 or later.</span></span> <span data-ttu-id="7a5c6-114">Hello виртуальных машин, называются *ВМ сценарий* и *lamp ВМ*.</span><span class="sxs-lookup"><span data-stu-id="7a5c6-114">hello VMs are called *script-vm* and *lamp-vm*.</span></span> <span data-ttu-id="7a5c6-115">Используйте уникальные имена для создания виртуальных машин hello.</span><span class="sxs-lookup"><span data-stu-id="7a5c6-115">Use unique names when you create hello VMs.</span></span> <span data-ttu-id="7a5c6-116">Он используется toorun команды CLI hello и одно является LAMP приложение используется toodeploy hello.</span><span class="sxs-lookup"><span data-stu-id="7a5c6-116">One is used toorun hello CLI commands and one is used toodeploy hello LAMP app.</span></span>

<span data-ttu-id="7a5c6-117">Необходимо также учетную запись хранилища Azure и ключа tooaccess ИТ (это можно получить из hello портал Azure).</span><span class="sxs-lookup"><span data-stu-id="7a5c6-117">You also need an Azure Storage account and a key tooaccess it (you can get this from hello Azure portal).</span></span>

<span data-ttu-id="7a5c6-118">Если вам нужна помощь при создании виртуальных машин Linux в Azure см. слишком[создать виртуальную машину под управлением Linux](createportal.md).</span><span class="sxs-lookup"><span data-stu-id="7a5c6-118">If you need help creating Linux VMs on Azure refer too[Create a Virtual Machine Running Linux](createportal.md).</span></span>

<span data-ttu-id="7a5c6-119">команды установки Hello предполагают Ubuntu, но вы можете адаптировать hello установки для любой поддерживаемый дистрибутив Linux.</span><span class="sxs-lookup"><span data-stu-id="7a5c6-119">hello install commands assume Ubuntu, but you can adapt hello installation for any supported Linux distro.</span></span>

<span data-ttu-id="7a5c6-120">Hello скрипт виртуальная машина виртуальная машина должна toohave установке Azure CLI, с tooAzure рабочего соединения.</span><span class="sxs-lookup"><span data-stu-id="7a5c6-120">hello script-vm VM needs toohave Azure CLI installed, with a working connection tooAzure.</span></span> <span data-ttu-id="7a5c6-121">См. справку слишком[Установка и настройка интерфейса командной строки Azure hello](../../../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="7a5c6-121">For help with this refer too[Install and Configure hello Azure Command-Line Interface](../../../cli-install-nodejs.md).</span></span>

## <a name="upload-a-script"></a><span data-ttu-id="7a5c6-122">Загрузка сценария</span><span class="sxs-lookup"><span data-stu-id="7a5c6-122">Upload a script</span></span>
<span data-ttu-id="7a5c6-123">Используется hello расширение CustomScript toorun сценарий в стеке LAMP tooinstall hello удаленной виртуальной Машины и создание страницы PHP.</span><span class="sxs-lookup"><span data-stu-id="7a5c6-123">We'll use hello CustomScript Extension toorun a script on a remote VM tooinstall hello LAMP stack and create a PHP page.</span></span> <span data-ttu-id="7a5c6-124">В сценарии hello tooaccess заказа из любого места будет передать как BLOB-объекта Azure.</span><span class="sxs-lookup"><span data-stu-id="7a5c6-124">In order tooaccess hello script from anywhere we'll upload it as an Azure blob.</span></span>

### <a name="script-overview"></a><span data-ttu-id="7a5c6-125">Общие сведения о сценариях</span><span class="sxs-lookup"><span data-stu-id="7a5c6-125">Script overview</span></span>
<span data-ttu-id="7a5c6-126">Ниже приведен пример сценария Hello устанавливает tooUbuntu стек LAMP (включая настройку автоматической установкой MySQL), записывает простой файл PHP и запускает Apache.</span><span class="sxs-lookup"><span data-stu-id="7a5c6-126">hello script example installs a LAMP stack tooUbuntu (including setting up a silent install of MySQL), writes a simple PHP file, and starts Apache.</span></span>

    #!/bin/bash
    # set up a silent install of MySQL
    dbpass="mySQLPassw0rd"

    export DEBIAN_FRONTEND=noninteractive
    echo mysql-server-5.6 mysql-server/root_password password $dbpass | debconf-set-selections
    echo mysql-server-5.6 mysql-server/root_password_again password $dbpass | debconf-set-selections

    # install hello LAMP stack
    apt-get -y install apache2 mysql-server php5 php5-mysql  

    # write some PHP
    echo \<center\>\<h1\>My Demo App\</h1\>\<br/\>\</center\> > /var/www/html/phpinfo.php
    echo \<\?php phpinfo\(\)\; \?\> >> /var/www/html/phpinfo.php

    # restart Apache
    apachectl restart

### <a name="upload-script"></a><span data-ttu-id="7a5c6-127">Отправка скрипта</span><span class="sxs-lookup"><span data-stu-id="7a5c6-127">Upload script</span></span>
<span data-ttu-id="7a5c6-128">Сохраните скрипт hello как текстовый файл, например *install_lamp.sh*, а затем передать его tooAzure хранилища.</span><span class="sxs-lookup"><span data-stu-id="7a5c6-128">Save hello script as a text file, for example *install_lamp.sh*, and then upload it tooAzure Storage.</span></span> <span data-ttu-id="7a5c6-129">Это легко сделать с помощью интерфейса CLI Azure.</span><span class="sxs-lookup"><span data-stu-id="7a5c6-129">You can do this easily with Azure CLI.</span></span> <span data-ttu-id="7a5c6-130">Hello следующий пример передает hello файла tooa хранилища контейнера с именем «скрипты».</span><span class="sxs-lookup"><span data-stu-id="7a5c6-130">hello following example uploads hello file tooa storage container named "scripts".</span></span> <span data-ttu-id="7a5c6-131">Если контейнер hello не существует, вам потребуется toocreate его первого.</span><span class="sxs-lookup"><span data-stu-id="7a5c6-131">If hello container doesn't exist you'll need toocreate it first.</span></span>

    azure storage blob upload -a <yourStorageAccountName> -k <yourStorageKey> --container scripts ./install_lamp.sh

<span data-ttu-id="7a5c6-132">Также можно создайте файл JSON, описывающий, как toodownload hello скрипта из хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="7a5c6-132">Also create a JSON file that describes how toodownload hello script from Azure Storage.</span></span> <span data-ttu-id="7a5c6-133">Сохраните его в виде *public_config.json* (замена «mystorage» с именем hello учетной записи):</span><span class="sxs-lookup"><span data-stu-id="7a5c6-133">Save this as *public_config.json* (replacing "mystorage" with hello name of your storage account):</span></span>

    {"fileUris":["https://mystorage.blob.core.windows.net/scripts/install_lamp.sh"], "commandToExecute":"sh install_lamp.sh" }


## <a name="deploy-hello-extension"></a><span data-ttu-id="7a5c6-134">Развертывание модуля hello</span><span class="sxs-lookup"><span data-stu-id="7a5c6-134">Deploy hello extension</span></span>
<span data-ttu-id="7a5c6-135">Теперь вы можете использовать hello Далее команда toodeploy hello расширения CustomScript Linux toohello удаленной виртуальной Машины с помощью hello Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="7a5c6-135">Now you can use hello next command toodeploy hello Linux CustomScript Extension toohello remote VM using hello Azure CLI.</span></span>

    azure vm extension set -c "./public_config.json" lamp-vm CustomScript Microsoft.Azure.Extensions 2.0

<span data-ttu-id="7a5c6-136">Предыдущая команда Hello загружает и запускает hello *install_lamp.sh* скриптов на ВМ называется hello *lamp ВМ*.</span><span class="sxs-lookup"><span data-stu-id="7a5c6-136">hello previous command downloads and runs hello *install_lamp.sh* script on hello VM called *lamp-vm*.</span></span>

<span data-ttu-id="7a5c6-137">Поскольку приложение hello включает веб-сервера, помните, порт прослушивания tooopen HTTP на hello удаленной виртуальной Машины с помощью следующей команды hello.</span><span class="sxs-lookup"><span data-stu-id="7a5c6-137">Since hello app includes a web server, remember tooopen an HTTP listening port on hello remote VM with hello next command.</span></span>

    azure vm endpoint create -n Apache -o tcp lamp-vm 80 80

## <a name="monitoring-and-troubleshooting"></a><span data-ttu-id="7a5c6-138">Мониторинг и устранение неполадок</span><span class="sxs-lookup"><span data-stu-id="7a5c6-138">Monitoring and troubleshooting</span></span>
<span data-ttu-id="7a5c6-139">Можно проверить на насколько хорошо выполняется hello пользовательского скрипта, просмотрев файл журнала hello hello удаленной виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="7a5c6-139">You can check on how well hello custom script runs by looking at hello log file on hello remote VM.</span></span> <span data-ttu-id="7a5c6-140">SSH слишком*lamp ВМ* и файл hello по заключительного фрагмента журнала с помощью следующей команды hello.</span><span class="sxs-lookup"><span data-stu-id="7a5c6-140">SSH too*lamp-vm* and tail hello log file with hello next command.</span></span>

    cd /var/log/azure/customscript
    tail -f handler.log

<span data-ttu-id="7a5c6-141">После запуска hello расширение CustomScript можно просматривать сведения созданная страница toohello PHP.</span><span class="sxs-lookup"><span data-stu-id="7a5c6-141">After you run hello CustomScript Extension, you can browse toohello PHP page you created for information.</span></span> <span data-ttu-id="7a5c6-142">Страница приветствия PHP hello в этой статье приведен *http://lamp-vm.cloudapp.net/phpinfo.php*.</span><span class="sxs-lookup"><span data-stu-id="7a5c6-142">hello PHP page for hello example in this article is *http://lamp-vm.cloudapp.net/phpinfo.php*.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="7a5c6-143">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="7a5c6-143">Additional resources</span></span>
<span data-ttu-id="7a5c6-144">Можно использовать hello же toodeploy основные шаги более сложных приложений.</span><span class="sxs-lookup"><span data-stu-id="7a5c6-144">You can use hello same basic steps toodeploy more complex apps.</span></span> <span data-ttu-id="7a5c6-145">В этом примере сценария установки hello была сохранена как общедоступный BLOB-объект в хранилище Azure.</span><span class="sxs-lookup"><span data-stu-id="7a5c6-145">In this example hello install script was saved as a public blob in Azure Storage.</span></span> <span data-ttu-id="7a5c6-146">Более безопасный вариант будет сценарий установки hello toostore как безопасный большой двоичный объект с [подписи безопасного доступа](https://msdn.microsoft.com/library/azure/ee395415.aspx) (SAS).</span><span class="sxs-lookup"><span data-stu-id="7a5c6-146">A more secure option would be toostore hello install script as a secure blob with a [Secure Access Signature](https://msdn.microsoft.com/library/azure/ee395415.aspx) (SAS).</span></span>

<span data-ttu-id="7a5c6-147">Далее перечислены дополнительные ресурсы для Azure CLI, Linux и hello расширение CustomScript.</span><span class="sxs-lookup"><span data-stu-id="7a5c6-147">Additional resources for Azure CLI, Linux and hello CustomScript Extension are listed next.</span></span>

[<span data-ttu-id="7a5c6-148">Автоматизация задач настройки виртуальных машин под управлением Linux с помощью расширения CustomScript</span><span class="sxs-lookup"><span data-stu-id="7a5c6-148">Automate Linux VM Customization Tasks Using CustomScript Extension</span></span>](https://azure.microsoft.com/blog/2014/08/20/automate-linux-vm-customization-tasks-using-customscript-extension/)

[<span data-ttu-id="7a5c6-149">Расширения Azure для Linux (GitHub)</span><span class="sxs-lookup"><span data-stu-id="7a5c6-149">Azure Linux Extensions (GitHub)</span></span>](https://github.com/Azure/azure-linux-extensions)