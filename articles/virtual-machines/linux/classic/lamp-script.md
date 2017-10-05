---
title: "Использование расширения CustomScript на виртуальной машине Linux | Документация Майкрософт"
description: "Узнайте, как использовать расширение CustomScript для развертывания приложений на виртуальных машинах под управлением Linux, созданных с помощью классической модели развертывания."
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
ms.openlocfilehash: cb1fc9a44dc9e57d9cc9f1c546ad937d67e63c2f
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="deploy-a-lamp-app-using-the-azure-customscript-extension-for-linux"></a><span data-ttu-id="f3fc3-103">Развертывание приложения LAMP с помощью расширения Azure CustomScript для Linux#</span><span class="sxs-lookup"><span data-stu-id="f3fc3-103">Deploy a LAMP app using the Azure CustomScript Extension for Linux</span></span>
> [!IMPORTANT] 
> <span data-ttu-id="f3fc3-104">В Azure предлагаются две модели развертывания для создания ресурсов и работы с ними: [модель диспетчера ресурсов и классическая модель](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="f3fc3-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="f3fc3-105">В этой статье рассматривается использование классической модели развертывания.</span><span class="sxs-lookup"><span data-stu-id="f3fc3-105">This article covers using the Classic deployment model.</span></span> <span data-ttu-id="f3fc3-106">Для большинства новых развертываний Майкрософт рекомендует использовать модель диспетчера ресурсов.</span><span class="sxs-lookup"><span data-stu-id="f3fc3-106">Microsoft recommends that most new deployments use the Resource Manager model.</span></span> <span data-ttu-id="f3fc3-107">Сведения о развертывании стека LAMP с помощью модели Resource Manager см. [здесь](../tutorial-lamp-stack.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="f3fc3-107">For information about deploying a LAMP stack using the Resource Manager model, see [here](../tutorial-lamp-stack.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="f3fc3-108">Расширение Microsoft Azure CustomScript для Linux позволяет использовать для настройки виртуальных машин произвольный код, написанный на одном из языков сценариев, которые поддерживаются виртуальной машиной (например, Python и Bash).</span><span class="sxs-lookup"><span data-stu-id="f3fc3-108">The Microsoft Azure CustomScript Extension for Linux provides a way to customize your virtual machines (VMs) by running arbitrary code written in any scripting language supported by the VM (for example, Python, and Bash).</span></span> <span data-ttu-id="f3fc3-109">Это обеспечивает гибкую автоматизацию развертывания приложения на нескольких виртуальных машинах.</span><span class="sxs-lookup"><span data-stu-id="f3fc3-109">This provides a very flexible way to automate application deployment to multiple machines.</span></span>

<span data-ttu-id="f3fc3-110">Расширение CustomScript можно развернуть с помощью портала Azure, Windows PowerShell или интерфейса командной строки Azure (Azure CLI).</span><span class="sxs-lookup"><span data-stu-id="f3fc3-110">You can deploy the CustomScript Extension using the Azure portal, Windows PowerShell, or the Azure Command-Line Interface (Azure CLI).</span></span>

<span data-ttu-id="f3fc3-111">В этой статье мы будем использовать интерфейс командной строки Azure для развертывания простого приложения LAMP на виртуальной машине под управлением Ubuntu, созданной с помощью классической модели развертывания.</span><span class="sxs-lookup"><span data-stu-id="f3fc3-111">In this article we'll use the Azure CLI to deploy a simple LAMP application to an Ubuntu VM created using the classic deployment model.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f3fc3-112">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="f3fc3-112">Prerequisites</span></span>
<span data-ttu-id="f3fc3-113">Для этого примера создайте две виртуальные машины Azure под управлением Ubuntu 14.04 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="f3fc3-113">For this example, first create two Azure VMs running Ubuntu 14.04 or later.</span></span> <span data-ttu-id="f3fc3-114">Присвойте им имена *script-vm* и *lamp-vm*.</span><span class="sxs-lookup"><span data-stu-id="f3fc3-114">The VMs are called *script-vm* and *lamp-vm*.</span></span> <span data-ttu-id="f3fc3-115">При создании виртуальных машин используйте уникальные имена.</span><span class="sxs-lookup"><span data-stu-id="f3fc3-115">Use unique names when you create the VMs.</span></span> <span data-ttu-id="f3fc3-116">Одна из этих машин будет использоваться для выполнения команд интерфейса командной строки, а другая — для развертывания приложения LAMP.</span><span class="sxs-lookup"><span data-stu-id="f3fc3-116">One is used to run the CLI commands and one is used to deploy the LAMP app.</span></span>

<span data-ttu-id="f3fc3-117">Вам также потребуется учетная запись службы хранилища Azure и ключ доступа к ней (все это можно получить на портале Azure).</span><span class="sxs-lookup"><span data-stu-id="f3fc3-117">You also need an Azure Storage account and a key to access it (you can get this from the Azure portal).</span></span>

<span data-ttu-id="f3fc3-118">Дополнительные сведения о создании виртуальных машин Linux в Azure см. в статье [Создание настраиваемой виртуальной машины под управлением Linux](createportal.md).</span><span class="sxs-lookup"><span data-stu-id="f3fc3-118">If you need help creating Linux VMs on Azure refer to [Create a Virtual Machine Running Linux](createportal.md).</span></span>

<span data-ttu-id="f3fc3-119">Команды установки рассчитаны на Ubuntu, но могут быть адаптированы для установки любого поддерживаемого дистрибутива Linux.</span><span class="sxs-lookup"><span data-stu-id="f3fc3-119">The install commands assume Ubuntu, but you can adapt the installation for any supported Linux distro.</span></span>

<span data-ttu-id="f3fc3-120">На виртуальной машине script-vm должен быть установлен интерфейс CLI Azure. Кроме того, ее необходимо подключить к Azure.</span><span class="sxs-lookup"><span data-stu-id="f3fc3-120">The script-vm VM needs to have Azure CLI installed, with a working connection to Azure.</span></span> <span data-ttu-id="f3fc3-121">Дополнительную информацию см. в статье [Установка Azure CLI](../../../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="f3fc3-121">For help with this refer to [Install and Configure the Azure Command-Line Interface](../../../cli-install-nodejs.md).</span></span>

## <a name="upload-a-script"></a><span data-ttu-id="f3fc3-122">Загрузка сценария</span><span class="sxs-lookup"><span data-stu-id="f3fc3-122">Upload a script</span></span>
<span data-ttu-id="f3fc3-123">Мы используем расширение CustomScript, чтобы выполнить сценарий на удаленной виртуальной машине для установки стека LAMP и создания PHP-страницы.</span><span class="sxs-lookup"><span data-stu-id="f3fc3-123">We'll use the CustomScript Extension to run a script on a remote VM to install the LAMP stack and create a PHP page.</span></span> <span data-ttu-id="f3fc3-124">Чтобы сценарий был доступен из любого расположения, мы передадим его как большой двоичный объект Azure.</span><span class="sxs-lookup"><span data-stu-id="f3fc3-124">In order to access the script from anywhere we'll upload it as an Azure blob.</span></span>

### <a name="script-overview"></a><span data-ttu-id="f3fc3-125">Общие сведения о сценариях</span><span class="sxs-lookup"><span data-stu-id="f3fc3-125">Script overview</span></span>
<span data-ttu-id="f3fc3-126">Сценарий в примере устанавливает стек LAMP в Ubuntu (включая настройку автоматической установки сервера MySQL), создает простой PHP-файл и запускает сервер Apache:</span><span class="sxs-lookup"><span data-stu-id="f3fc3-126">The script example installs a LAMP stack to Ubuntu (including setting up a silent install of MySQL), writes a simple PHP file, and starts Apache.</span></span>

    #!/bin/bash
    # set up a silent install of MySQL
    dbpass="mySQLPassw0rd"

    export DEBIAN_FRONTEND=noninteractive
    echo mysql-server-5.6 mysql-server/root_password password $dbpass | debconf-set-selections
    echo mysql-server-5.6 mysql-server/root_password_again password $dbpass | debconf-set-selections

    # install the LAMP stack
    apt-get -y install apache2 mysql-server php5 php5-mysql  

    # write some PHP
    echo \<center\>\<h1\>My Demo App\</h1\>\<br/\>\</center\> > /var/www/html/phpinfo.php
    echo \<\?php phpinfo\(\)\; \?\> >> /var/www/html/phpinfo.php

    # restart Apache
    apachectl restart

### <a name="upload-script"></a><span data-ttu-id="f3fc3-127">Отправка скрипта</span><span class="sxs-lookup"><span data-stu-id="f3fc3-127">Upload script</span></span>
<span data-ttu-id="f3fc3-128">Сохраните сценарий как текстовый файл, например *install_lamp.sh*, и отправьте его в службу хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="f3fc3-128">Save the script as a text file, for example *install_lamp.sh*, and then upload it to Azure Storage.</span></span> <span data-ttu-id="f3fc3-129">Это легко сделать с помощью интерфейса CLI Azure.</span><span class="sxs-lookup"><span data-stu-id="f3fc3-129">You can do this easily with Azure CLI.</span></span> <span data-ttu-id="f3fc3-130">Приведенный ниже пример передает файл в контейнер хранилища с именем scripts.</span><span class="sxs-lookup"><span data-stu-id="f3fc3-130">The following example uploads the file to a storage container named "scripts".</span></span> <span data-ttu-id="f3fc3-131">Если контейнер не существует, необходимо сначала его создать.</span><span class="sxs-lookup"><span data-stu-id="f3fc3-131">If the container doesn't exist you'll need to create it first.</span></span>

    azure storage blob upload -a <yourStorageAccountName> -k <yourStorageKey> --container scripts ./install_lamp.sh

<span data-ttu-id="f3fc3-132">Также создайте JSON-файл, в котором будет указан способ скачивания сценария из службы хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="f3fc3-132">Also create a JSON file that describes how to download the script from Azure Storage.</span></span> <span data-ttu-id="f3fc3-133">Сохраните его как *public_config.json* (вместо mystorage укажите имя своей учетной записи хранения):</span><span class="sxs-lookup"><span data-stu-id="f3fc3-133">Save this as *public_config.json* (replacing "mystorage" with the name of your storage account):</span></span>

    {"fileUris":["https://mystorage.blob.core.windows.net/scripts/install_lamp.sh"], "commandToExecute":"sh install_lamp.sh" }


## <a name="deploy-the-extension"></a><span data-ttu-id="f3fc3-134">Развертывание расширения</span><span class="sxs-lookup"><span data-stu-id="f3fc3-134">Deploy the extension</span></span>
<span data-ttu-id="f3fc3-135">Теперь расширение CustomScript для Linux можно развернуть на удаленной виртуальной машине с помощью интерфейса командной строки Azure.</span><span class="sxs-lookup"><span data-stu-id="f3fc3-135">Now you can use the next command to deploy the Linux CustomScript Extension to the remote VM using the Azure CLI.</span></span>

    azure vm extension set -c "./public_config.json" lamp-vm CustomScript Microsoft.Azure.Extensions 2.0

<span data-ttu-id="f3fc3-136">Предыдущая команда скачивает и выполняет сценарий *install_lamp.sh* на виртуальной машине с именем *lamp-vm*.</span><span class="sxs-lookup"><span data-stu-id="f3fc3-136">The previous command downloads and runs the *install_lamp.sh* script on the VM called *lamp-vm*.</span></span>

<span data-ttu-id="f3fc3-137">Так как приложение включает в себя веб-сервер, не забудьте открыть порт прослушивания HTTP на удаленной виртуальной машине с помощью следующей команды:</span><span class="sxs-lookup"><span data-stu-id="f3fc3-137">Since the app includes a web server, remember to open an HTTP listening port on the remote VM with the next command.</span></span>

    azure vm endpoint create -n Apache -o tcp lamp-vm 80 80

## <a name="monitoring-and-troubleshooting"></a><span data-ttu-id="f3fc3-138">Мониторинг и устранение неполадок</span><span class="sxs-lookup"><span data-stu-id="f3fc3-138">Monitoring and troubleshooting</span></span>
<span data-ttu-id="f3fc3-139">Можно проверить правильность выполнения пользовательского скрипта, просмотрите файл журнала на удаленной виртуальной машине.</span><span class="sxs-lookup"><span data-stu-id="f3fc3-139">You can check on how well the custom script runs by looking at the log file on the remote VM.</span></span> <span data-ttu-id="f3fc3-140">Добавьте SSH в *lamp-vm* и добавьте в файл журнала заключительный фрагмент с помощью следующей команды:</span><span class="sxs-lookup"><span data-stu-id="f3fc3-140">SSH to *lamp-vm* and tail the log file with the next command.</span></span>

    cd /var/log/azure/customscript
    tail -f handler.log

<span data-ttu-id="f3fc3-141">После запуска расширения CustomScript вы сможете перейти к созданной PHP-странице и проверить данные.</span><span class="sxs-lookup"><span data-stu-id="f3fc3-141">After you run the CustomScript Extension, you can browse to the PHP page you created for information.</span></span> <span data-ttu-id="f3fc3-142">PHP-страница для примера в этой статье — *http://lamp-vm.cloudapp.net/phpinfo.php*.</span><span class="sxs-lookup"><span data-stu-id="f3fc3-142">The PHP page for the example in this article is *http://lamp-vm.cloudapp.net/phpinfo.php*.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="f3fc3-143">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="f3fc3-143">Additional resources</span></span>
<span data-ttu-id="f3fc3-144">С помощью описанных выше действий можно выполнять развертывание и более сложных приложений.</span><span class="sxs-lookup"><span data-stu-id="f3fc3-144">You can use the same basic steps to deploy more complex apps.</span></span> <span data-ttu-id="f3fc3-145">В приведенном примере сценарий установки был сохранен в службе хранилища Azure как общедоступный большой двоичный объект.</span><span class="sxs-lookup"><span data-stu-id="f3fc3-145">In this example the install script was saved as a public blob in Azure Storage.</span></span> <span data-ttu-id="f3fc3-146">Чтобы обеспечить больший уровень защиты, сценарий установки можно сохранить как защищенный большой двоичный объект, для доступа к которому будет использоваться [подписанный URL-адрес](https://msdn.microsoft.com/library/azure/ee395415.aspx) (SAS).</span><span class="sxs-lookup"><span data-stu-id="f3fc3-146">A more secure option would be to store the install script as a secure blob with a [Secure Access Signature](https://msdn.microsoft.com/library/azure/ee395415.aspx) (SAS).</span></span>

<span data-ttu-id="f3fc3-147">Дополнительную информацию об интерфейсе командной строки Azure, Linux и расширении CustomScript см. в следующих статьях.</span><span class="sxs-lookup"><span data-stu-id="f3fc3-147">Additional resources for Azure CLI, Linux and the CustomScript Extension are listed next.</span></span>

[<span data-ttu-id="f3fc3-148">Автоматизация задач настройки виртуальных машин под управлением Linux с помощью расширения CustomScript</span><span class="sxs-lookup"><span data-stu-id="f3fc3-148">Automate Linux VM Customization Tasks Using CustomScript Extension</span></span>](https://azure.microsoft.com/blog/2014/08/20/automate-linux-vm-customization-tasks-using-customscript-extension/)

[<span data-ttu-id="f3fc3-149">Расширения Azure для Linux (GitHub)</span><span class="sxs-lookup"><span data-stu-id="f3fc3-149">Azure Linux Extensions (GitHub)</span></span>](https://github.com/Azure/azure-linux-extensions)