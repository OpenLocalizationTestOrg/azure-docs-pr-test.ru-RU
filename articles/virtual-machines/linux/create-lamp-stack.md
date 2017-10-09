---
title: "aaaDeploy LAMP на виртуальной машине Linux в Azure | Документы Microsoft"
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
ms.devlang: azurecli
ms.topic: article
ms.date: 2/21/2017
ms.author: juluk
ms.openlocfilehash: 42d887bb9f78becc02505e336be25fdaaf78df70
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-lamp-stack-on-azure"></a><span data-ttu-id="ac5d8-103">Развертывание стека LAMP в Azure</span><span class="sxs-lookup"><span data-stu-id="ac5d8-103">Deploy LAMP stack on Azure</span></span>
<span data-ttu-id="ac5d8-104">В этой статье рассматриваются как toodeploy Apache веб-сервера, MySQL и PHP (стек LAMP hello) в Azure.</span><span class="sxs-lookup"><span data-stu-id="ac5d8-104">This article walks you through how toodeploy an Apache web server, MySQL, and PHP (hello LAMP stack) on Azure.</span></span> <span data-ttu-id="ac5d8-105">Необходима учетная запись Azure ([получить бесплатную пробную версию](https://azure.microsoft.com/pricing/free-trial/)) и hello [Azure CLI 2.0](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).</span><span class="sxs-lookup"><span data-stu-id="ac5d8-105">You need an Azure account ([get a free trial](https://azure.microsoft.com/pricing/free-trial/)) and hello [Azure CLI 2.0](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).</span></span> <span data-ttu-id="ac5d8-106">Можно также выполнить следующие действия с hello [Azure CLI 1.0](create-lamp-stack-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="ac5d8-106">You can also perform these steps with hello [Azure CLI 1.0](create-lamp-stack-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

## <a name="quick-command-summary"></a><span data-ttu-id="ac5d8-107">Краткая сводка по командам</span><span class="sxs-lookup"><span data-stu-id="ac5d8-107">Quick command summary</span></span>

1. <span data-ttu-id="ac5d8-108">Сохранить и продолжить изменение hello [azuredeploy.parameters.json файл](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/lamp-app/azuredeploy.parameters.json) tooyour предпочтения на локальном компьютере.</span><span class="sxs-lookup"><span data-stu-id="ac5d8-108">Save and edit hello [azuredeploy.parameters.json file](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/lamp-app/azuredeploy.parameters.json) tooyour preference on your local machine.</span></span>
2. <span data-ttu-id="ac5d8-109">Выполните следующие две команды toocreate hello группу ресурсов и затем развернуть шаблон.</span><span class="sxs-lookup"><span data-stu-id="ac5d8-109">Run hello following two commands toocreate a resource group and then deploy your template:</span></span>

```azurecli
az group create -l westus -n myResourceGroup
az group deployment create -g myResourceGroup \
    --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/lamp-app/azuredeploy.json \
    --parameters @filepathToParameters.json
```

### <a name="deploy-lamp-on-existing-vm"></a><span data-ttu-id="ac5d8-110">Развертывание LAMP на существующей виртуальной машине</span><span class="sxs-lookup"><span data-stu-id="ac5d8-110">Deploy LAMP on existing VM</span></span>
<span data-ttu-id="ac5d8-111">Hello следующие команды пакеты обновления, а затем устанавливает Apache, PHP и MySQL:</span><span class="sxs-lookup"><span data-stu-id="ac5d8-111">hello following commands updates packages, then installs Apache, MySQL, and PHP:</span></span>

```bash
sudo apt-get update
sudo apt-get install apache2 mysql-server php5 php5-mysql
```

## <a name="deploy-lamp-on-new-vm-walkthrough"></a><span data-ttu-id="ac5d8-112">Пошаговое руководство по развертыванию LAMP на новой виртуальной машине</span><span class="sxs-lookup"><span data-stu-id="ac5d8-112">Deploy LAMP on new VM walkthrough</span></span>

1. <span data-ttu-id="ac5d8-113">Создание группы ресурсов с [Создание группы az](/cli/azure/group#create) toocontain hello новой виртуальной Машины:</span><span class="sxs-lookup"><span data-stu-id="ac5d8-113">Create a resource group with [az group create](/cli/azure/group#create) toocontain hello new VM:</span></span>

```azurecli
az group create -l westus -n myResourceGroup
```
<span data-ttu-id="ac5d8-114">toocreate Здравствуйте самой ВМ, уже написанный найден шаблон диспетчера ресурсов Azure можно использовать [здесь на GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/lamp-app).</span><span class="sxs-lookup"><span data-stu-id="ac5d8-114">toocreate hello VM itself, you can use an already written Azure Resource Manager template found [here on GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/lamp-app).</span></span>

2. <span data-ttu-id="ac5d8-115">Сохранить hello [azuredeploy.parameters.json файл](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/lamp-app/azuredeploy.parameters.json) tooyour локального компьютера.</span><span class="sxs-lookup"><span data-stu-id="ac5d8-115">Save hello [azuredeploy.parameters.json file](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/lamp-app/azuredeploy.parameters.json) tooyour local machine.</span></span>
3. <span data-ttu-id="ac5d8-116">Изменить hello **azuredeploy.parameters.json** tooyour файл предпочитаемый входных данных.</span><span class="sxs-lookup"><span data-stu-id="ac5d8-116">Edit hello **azuredeploy.parameters.json** file tooyour preferred inputs.</span></span>
4. <span data-ttu-id="ac5d8-117">Развертывание шаблона hello с [создание развертывания группы az] ссылается hello загрузили файл json:</span><span class="sxs-lookup"><span data-stu-id="ac5d8-117">Deploy hello template with [az group deployment create] referencing hello downloaded json file:</span></span>

```azurecli
az group deployment create -g myResourceGroup \
    --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/lamp-app/azuredeploy.json \
    --parameters @filepathToParameters.json
```

<span data-ttu-id="ac5d8-118">Hello вывода будет примерно toohello следующий пример:</span><span class="sxs-lookup"><span data-stu-id="ac5d8-118">hello output is similar toohello following example:</span></span>

```json
{
"id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/myResourceGroup/providers/Microsoft.Resources/deployments/azuredeploy",
"name": "azuredeploy",
"properties": {
    "correlationId": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
    "debugSetting": null,
}
...
"provisioningState": "Succeeded",
"template": null,
"templateLink": {
    "contentVersion": "1.0.0.0",
    "uri": "https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/lamp-app/azuredeploy.json"
    },
    "timestamp": "2017-02-22T00:05:51.860411+00:00"
},
"resourceGroup": "myResourceGroup"
}
```

<span data-ttu-id="ac5d8-119">Вы создали виртуальную машину Linux с установленным стеком LAMP.</span><span class="sxs-lookup"><span data-stu-id="ac5d8-119">You have now created a Linux VM with LAMP already installed on it.</span></span> <span data-ttu-id="ac5d8-120">При желании можно проверить hello установки посредством перехода вниз слишком[проверьте ЛАМПОЧКА успешно установлен](#verify-lamp-successfully-installed).</span><span class="sxs-lookup"><span data-stu-id="ac5d8-120">If you wish, you can verify hello install by jumping down too[Verify LAMP Successfully Installed](#verify-lamp-successfully-installed).</span></span>

## <a name="deploy-lamp-on-existing-vm-walkthrough"></a><span data-ttu-id="ac5d8-121">Пошаговое руководство по развертыванию LAMP на существующей виртуальной машине</span><span class="sxs-lookup"><span data-stu-id="ac5d8-121">Deploy LAMP on existing VM walkthrough</span></span>
<span data-ttu-id="ac5d8-122">Если требуется помощь для создания виртуальной Машины Linux можно head [здесь toolearn как toocreate ВМ Linux](https://docs.microsoft.com/azure/virtual-machines/virtual-machines-linux-quick-create-cli).</span><span class="sxs-lookup"><span data-stu-id="ac5d8-122">If you need help creating a Linux VM, you can head [here toolearn how toocreate a Linux VM](https://docs.microsoft.com/azure/virtual-machines/virtual-machines-linux-quick-create-cli).</span></span> <span data-ttu-id="ac5d8-123">Далее необходимо tooSSH в hello виртуальной Машины с Linux.</span><span class="sxs-lookup"><span data-stu-id="ac5d8-123">Next, you need tooSSH into hello Linux VM.</span></span> <span data-ttu-id="ac5d8-124">Если вам нужна помощь с созданием SSH-ключ, можно head [здесь toolearn как toocreate ключа SSH в Linux или Mac](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="ac5d8-124">If you need help with creating an SSH key, you can head [here toolearn how toocreate an SSH key on Linux/Mac](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
<span data-ttu-id="ac5d8-125">Если у вас же имеется ключ SSH, продолжайте процедуру и, используя командную строку, подключитесь по протоколу SSH к виртуальной машине Linux с помощью команды `ssh azureuser@mypublicdns.westus.cloudapp.azure.com`.</span><span class="sxs-lookup"><span data-stu-id="ac5d8-125">If you have an SSH key already, go ahead and SSH from your command line into your Linux VM with `ssh azureuser@mypublicdns.westus.cloudapp.azure.com`.</span></span>

<span data-ttu-id="ac5d8-126">Теперь, когда вы работаете в ВМ Linux, мы пошаговую установку стек LAMP hello на основе Debian распределения.</span><span class="sxs-lookup"><span data-stu-id="ac5d8-126">Now that you are working within your Linux VM, we can walk through installing hello LAMP stack on Debian-based distributions.</span></span> <span data-ttu-id="ac5d8-127">конкретные команды Hello могут отличаться в других дистрибутивах Linux.</span><span class="sxs-lookup"><span data-stu-id="ac5d8-127">hello exact commands might differ for other Linux distros.</span></span>

#### <a name="installing-on-debianubuntu"></a><span data-ttu-id="ac5d8-128">Установка на Debian или Ubuntu</span><span class="sxs-lookup"><span data-stu-id="ac5d8-128">Installing on Debian/Ubuntu</span></span>
<span data-ttu-id="ac5d8-129">Требуются следующие пакеты, установленные hello: `apache2`, `mysql-server`, `php5`, и `php5-mysql`.</span><span class="sxs-lookup"><span data-stu-id="ac5d8-129">You need hello following packages installed: `apache2`, `mysql-server`, `php5`, and `php5-mysql`.</span></span> <span data-ttu-id="ac5d8-130">Их можно установить, перетащив вручную или воспользовавшись Tasksel.</span><span class="sxs-lookup"><span data-stu-id="ac5d8-130">You can install these packages by directly grabbing these packages or using Tasksel.</span></span>
<span data-ttu-id="ac5d8-131">Перед установкой требуется toodownload и обновление списков пакета.</span><span class="sxs-lookup"><span data-stu-id="ac5d8-131">Before installing you need toodownload and update package lists.</span></span>

```bash
sudo apt-get update
```

##### <a name="individual-packages"></a><span data-ttu-id="ac5d8-132">Установка отдельных пакетов</span><span class="sxs-lookup"><span data-stu-id="ac5d8-132">Individual packages</span></span>
<span data-ttu-id="ac5d8-133">Можно использовать apt-get.</span><span class="sxs-lookup"><span data-stu-id="ac5d8-133">Using apt-get:</span></span>

```bash
sudo apt-get install apache2 mysql-server php5 php5-mysql
```

##### <a name="using-tasksel"></a><span data-ttu-id="ac5d8-134">Установка с помощью Tasksel</span><span class="sxs-lookup"><span data-stu-id="ac5d8-134">Using tasksel</span></span>
<span data-ttu-id="ac5d8-135">В качестве альтернативы можно скачать Tasksel. Это инструмент Debian и Ubuntu, который устанавливает в систему несколько связанных пакетов в рамках одной скоординированной задачи.</span><span class="sxs-lookup"><span data-stu-id="ac5d8-135">Alternatively you can download Tasksel, a Debian/Ubuntu tool that installs multiple related packages as a coordinated "task" onto your system.</span></span>

```bash
sudo apt-get install tasksel
sudo tasksel install lamp-server
```

<span data-ttu-id="ac5d8-136">После выполнения любого из предыдущих параметров hello, будет иметь запрашиваемые tooinstall эти пакеты и другие зависимости.</span><span class="sxs-lookup"><span data-stu-id="ac5d8-136">After running either of hello previous options, you will be prompted tooinstall these packages and various other dependencies.</span></span> <span data-ttu-id="ac5d8-137">tooset пароль администратора для MySQL, нажмите «y», а затем toocontinue «Ввод» и следуйте каких-либо других запросов.</span><span class="sxs-lookup"><span data-stu-id="ac5d8-137">tooset an administrative password for MySQL, press 'y' and then 'Enter' toocontinue, and follow any other prompts.</span></span> <span data-ttu-id="ac5d8-138">Этот процесс устанавливает hello минимальные необходимые PHP необходимые расширения toouse PHP MySQL.</span><span class="sxs-lookup"><span data-stu-id="ac5d8-138">This process installs hello minimum required PHP extensions needed toouse PHP with MySQL.</span></span> 

![][1]

<span data-ttu-id="ac5d8-139">Выполните следующие команды toosee hello другие расширения PHP, которые доступны в виде пакетов.</span><span class="sxs-lookup"><span data-stu-id="ac5d8-139">Run hello following command toosee other PHP extensions that are available as packages:</span></span>

```bash
apt-cache search php5
```

#### <a name="create-infophp-document"></a><span data-ttu-id="ac5d8-140">Создание документа info.php</span><span class="sxs-lookup"><span data-stu-id="ac5d8-140">Create info.php document</span></span>
<span data-ttu-id="ac5d8-141">Теперь должен быть доступ toocheck версии Apache, PHP и MySQL имеется через командную строку hello, введя `apache2 -v`, `mysql -v`, или `php -v`.</span><span class="sxs-lookup"><span data-stu-id="ac5d8-141">You should now be able toocheck what version of Apache, MySQL, and PHP you have through hello command line by typing `apache2 -v`, `mysql -v`, or `php -v`.</span></span>

<span data-ttu-id="ac5d8-142">Если вы бы как tootest Далее, можно создать быстрый tooview страницы сведения о PHP в браузере.</span><span class="sxs-lookup"><span data-stu-id="ac5d8-142">If you would like tootest further, you can create a quick PHP info page tooview in a browser.</span></span> <span data-ttu-id="ac5d8-143">Создайте файл в текстовом редакторе Nano с помощью следующей команды.</span><span class="sxs-lookup"><span data-stu-id="ac5d8-143">Create a file with Nano text editor with this command:</span></span>

```bash
sudo nano /var/www/html/info.php
```

<span data-ttu-id="ac5d8-144">В текстовом редакторе GNU Nano hello добавьте hello следующие строки:</span><span class="sxs-lookup"><span data-stu-id="ac5d8-144">Within hello GNU Nano text editor, add hello following lines:</span></span>

```php
<?php
phpinfo();
?>
```

<span data-ttu-id="ac5d8-145">Сохраните и закройте редактор текста hello.</span><span class="sxs-lookup"><span data-stu-id="ac5d8-145">Then save and exit hello text editor.</span></span>

<span data-ttu-id="ac5d8-146">Перезапустите Apache с помощью следующей команды, чтобы все новые установленные компоненты вступили в действие.</span><span class="sxs-lookup"><span data-stu-id="ac5d8-146">Restart Apache with this command so all new installs take effect.</span></span>

```bash
sudo service apache2 restart
```

## <a name="verify-lamp-successfully-installed"></a><span data-ttu-id="ac5d8-147">Проверка успешности установки LAMP</span><span class="sxs-lookup"><span data-stu-id="ac5d8-147">Verify LAMP successfully installed</span></span>
<span data-ttu-id="ac5d8-148">Теперь можно проверить hello PHP info созданная страница, открыв браузер и переходит в toohttp://youruniqueDNS/info.php.</span><span class="sxs-lookup"><span data-stu-id="ac5d8-148">Now you can check hello PHP info page you created by opening a browser and going toohttp://youruniqueDNS/info.php.</span></span> <span data-ttu-id="ac5d8-149">Он должен выглядеть примерно toothis изображения.</span><span class="sxs-lookup"><span data-stu-id="ac5d8-149">It should look similar toothis image.</span></span>

![][2]

<span data-ttu-id="ac5d8-150">Apache установки можно проверить, просмотрев hello страница по умолчанию Apache2 Ubuntu последовательно выбрав tooyou http://youruniqueDNS/.</span><span class="sxs-lookup"><span data-stu-id="ac5d8-150">You can check your Apache installation by viewing hello Apache2 Ubuntu Default Page by going tooyou http://youruniqueDNS/.</span></span> <span data-ttu-id="ac5d8-151">Hello вывода будет примерно toohello следующий пример:</span><span class="sxs-lookup"><span data-stu-id="ac5d8-151">hello output is similar toohello following example:</span></span>

![][3]

<span data-ttu-id="ac5d8-152">Поздравляем! Вы установили стек LAMP на виртуальную машину Azure.</span><span class="sxs-lookup"><span data-stu-id="ac5d8-152">Congratulations, you have just setup a LAMP stack on your Azure VM!</span></span>

## <a name="next-steps"></a><span data-ttu-id="ac5d8-153">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="ac5d8-153">Next steps</span></span>
<span data-ttu-id="ac5d8-154">Проверьте hello документации Ubuntu стек LAMP hello.</span><span class="sxs-lookup"><span data-stu-id="ac5d8-154">Check out hello Ubuntu documentation on hello LAMP stack:</span></span>

* [<span data-ttu-id="ac5d8-155">https://help.ubuntu.com/community/ApacheMySQLPHP</span><span class="sxs-lookup"><span data-stu-id="ac5d8-155">https://help.ubuntu.com/community/ApacheMySQLPHP</span></span>](https://help.ubuntu.com/community/ApacheMySQLPHP)

[1]: ./media/deploy-lamp-stack/configmysqlpassword-small.png
[2]: ./media/deploy-lamp-stack/phpsuccesspage.png
[3]: ./media/deploy-lamp-stack/apachesuccesspage.png
