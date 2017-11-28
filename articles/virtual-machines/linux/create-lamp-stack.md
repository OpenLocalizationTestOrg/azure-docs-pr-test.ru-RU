---
title: "Развертывание LAMP на виртуальной машине Linux в Azure | Документация Майкрософт"
description: "Узнайте, как установить стек LAMP на виртуальную машину Linux в Azure."
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
ms.openlocfilehash: ad69876bfbeba5f948a81e5c48c659fdf2265ae2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="deploy-lamp-stack-on-azure"></a><span data-ttu-id="ff681-103">Развертывание стека LAMP в Azure</span><span class="sxs-lookup"><span data-stu-id="ff681-103">Deploy LAMP stack on Azure</span></span>
<span data-ttu-id="ff681-104">Эта статья содержит указания по развертыванию веб-сервера Apache, MySQL и PHP (стека LAMP) в Azure.</span><span class="sxs-lookup"><span data-stu-id="ff681-104">This article walks you through how to deploy an Apache web server, MySQL, and PHP (the LAMP stack) on Azure.</span></span> <span data-ttu-id="ff681-105">Требуются учетная запись Azure (можно [получить бесплатную пробную версию](https://azure.microsoft.com/pricing/free-trial/)) и [CLI Azure 2.0](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).</span><span class="sxs-lookup"><span data-stu-id="ff681-105">You need an Azure account ([get a free trial](https://azure.microsoft.com/pricing/free-trial/)) and the [Azure CLI 2.0](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).</span></span> <span data-ttu-id="ff681-106">Эти действия можно также выполнить с помощью [Azure CLI 1.0](create-lamp-stack-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="ff681-106">You can also perform these steps with the [Azure CLI 1.0](create-lamp-stack-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

## <a name="quick-command-summary"></a><span data-ttu-id="ff681-107">Краткая сводка по командам</span><span class="sxs-lookup"><span data-stu-id="ff681-107">Quick command summary</span></span>

1. <span data-ttu-id="ff681-108">Сохраните на локальном компьютере [файл azuredeploy.parameters.json](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/lamp-app/azuredeploy.parameters.json) и измените его, указав свои параметры.</span><span class="sxs-lookup"><span data-stu-id="ff681-108">Save and edit the [azuredeploy.parameters.json file](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/lamp-app/azuredeploy.parameters.json) to your preference on your local machine.</span></span>
2. <span data-ttu-id="ff681-109">Выполните следующие две команды, чтобы создать группу ресурсов, а затем развернуть шаблон.</span><span class="sxs-lookup"><span data-stu-id="ff681-109">Run the following two commands to create a resource group and then deploy your template:</span></span>

```azurecli
az group create -l westus -n myResourceGroup
az group deployment create -g myResourceGroup \
    --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/lamp-app/azuredeploy.json \
    --parameters @filepathToParameters.json
```

### <a name="deploy-lamp-on-existing-vm"></a><span data-ttu-id="ff681-110">Развертывание LAMP на существующей виртуальной машине</span><span class="sxs-lookup"><span data-stu-id="ff681-110">Deploy LAMP on existing VM</span></span>
<span data-ttu-id="ff681-111">Следующие команды обновляют пакеты, а затем устанавливают Apache, MySQL и PHP.</span><span class="sxs-lookup"><span data-stu-id="ff681-111">The following commands updates packages, then installs Apache, MySQL, and PHP:</span></span>

```bash
sudo apt-get update
sudo apt-get install apache2 mysql-server php5 php5-mysql
```

## <a name="deploy-lamp-on-new-vm-walkthrough"></a><span data-ttu-id="ff681-112">Пошаговое руководство по развертыванию LAMP на новой виртуальной машине</span><span class="sxs-lookup"><span data-stu-id="ff681-112">Deploy LAMP on new VM walkthrough</span></span>

1. <span data-ttu-id="ff681-113">С помощью команды [az group create](/cli/azure/group#create) создайте группу ресурсов для новой виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="ff681-113">Create a resource group with [az group create](/cli/azure/group#create) to contain the new VM:</span></span>

```azurecli
az group create -l westus -n myResourceGroup
```
<span data-ttu-id="ff681-114">Чтобы создать саму виртуальную машину, можно использовать готовый шаблон Azure Resource Manager [с сайта GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/lamp-app).</span><span class="sxs-lookup"><span data-stu-id="ff681-114">To create the VM itself, you can use an already written Azure Resource Manager template found [here on GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/lamp-app).</span></span>

2. <span data-ttu-id="ff681-115">Сохраните [файл azuredeploy.parameters.json](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/lamp-app/azuredeploy.parameters.json) на локальном компьютере.</span><span class="sxs-lookup"><span data-stu-id="ff681-115">Save the [azuredeploy.parameters.json file](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/lamp-app/azuredeploy.parameters.json) to your local machine.</span></span>
3. <span data-ttu-id="ff681-116">Измените **файл azuredeploy.parameters.json**, указав свои входные параметры.</span><span class="sxs-lookup"><span data-stu-id="ff681-116">Edit the **azuredeploy.parameters.json** file to your preferred inputs.</span></span>
4. <span data-ttu-id="ff681-117">Разверните шаблон с помощью команды [az group deployment create], указав скачанный JSON-файл.</span><span class="sxs-lookup"><span data-stu-id="ff681-117">Deploy the template with [az group deployment create] referencing the downloaded json file:</span></span>

```azurecli
az group deployment create -g myResourceGroup \
    --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/lamp-app/azuredeploy.json \
    --parameters @filepathToParameters.json
```

<span data-ttu-id="ff681-118">Вы должны увидеть результат, аналогичный приведенному ниже.</span><span class="sxs-lookup"><span data-stu-id="ff681-118">The output is similar to the following example:</span></span>

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

<span data-ttu-id="ff681-119">Вы создали виртуальную машину Linux с установленным стеком LAMP.</span><span class="sxs-lookup"><span data-stu-id="ff681-119">You have now created a Linux VM with LAMP already installed on it.</span></span> <span data-ttu-id="ff681-120">При желании можно проверить установку, перейдя к разделу [Проверка успешности установки LAMP](#verify-lamp-successfully-installed).</span><span class="sxs-lookup"><span data-stu-id="ff681-120">If you wish, you can verify the install by jumping down to [Verify LAMP Successfully Installed](#verify-lamp-successfully-installed).</span></span>

## <a name="deploy-lamp-on-existing-vm-walkthrough"></a><span data-ttu-id="ff681-121">Пошаговое руководство по развертыванию LAMP на существующей виртуальной машине</span><span class="sxs-lookup"><span data-stu-id="ff681-121">Deploy LAMP on existing VM walkthrough</span></span>
<span data-ttu-id="ff681-122">Если вам нужна помощь с созданием виртуальной машины Linux, то вы можете перейти [сюда](https://docs.microsoft.com/azure/virtual-machines/virtual-machines-linux-quick-create-cli), чтобы узнать, как создать виртуальную машину Linux.</span><span class="sxs-lookup"><span data-stu-id="ff681-122">If you need help creating a Linux VM, you can head [here to learn how to create a Linux VM](https://docs.microsoft.com/azure/virtual-machines/virtual-machines-linux-quick-create-cli).</span></span> <span data-ttu-id="ff681-123">Далее требуется подключится по протоколу SSH к виртуальной машине Linux.</span><span class="sxs-lookup"><span data-stu-id="ff681-123">Next, you need to SSH into the Linux VM.</span></span> <span data-ttu-id="ff681-124">Если вам нужна помощь с созданием ключа SSH, то вы можете перейти [сюда](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), чтобы узнать, как создать ключ SSH в Linux или Mac.</span><span class="sxs-lookup"><span data-stu-id="ff681-124">If you need help with creating an SSH key, you can head [here to learn how to create an SSH key on Linux/Mac](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
<span data-ttu-id="ff681-125">Если у вас же имеется ключ SSH, продолжайте процедуру и, используя командную строку, подключитесь по протоколу SSH к виртуальной машине Linux с помощью команды `ssh azureuser@mypublicdns.westus.cloudapp.azure.com`.</span><span class="sxs-lookup"><span data-stu-id="ff681-125">If you have an SSH key already, go ahead and SSH from your command line into your Linux VM with `ssh azureuser@mypublicdns.westus.cloudapp.azure.com`.</span></span>

<span data-ttu-id="ff681-126">Теперь, когда вы работаете на своей виртуальной машине Linux, мы можем рассмотреть установку стека LAMP на дистрибутивы на основе Debian.</span><span class="sxs-lookup"><span data-stu-id="ff681-126">Now that you are working within your Linux VM, we can walk through installing the LAMP stack on Debian-based distributions.</span></span> <span data-ttu-id="ff681-127">Конкретные команды могут отличаться для других дистрибутивов Linux.</span><span class="sxs-lookup"><span data-stu-id="ff681-127">The exact commands might differ for other Linux distros.</span></span>

#### <a name="installing-on-debianubuntu"></a><span data-ttu-id="ff681-128">Установка на Debian или Ubuntu</span><span class="sxs-lookup"><span data-stu-id="ff681-128">Installing on Debian/Ubuntu</span></span>
<span data-ttu-id="ff681-129">Необходимо установить следующие пакеты: `apache2`, `mysql-server`, `php5` и `php5-mysql`.</span><span class="sxs-lookup"><span data-stu-id="ff681-129">You need the following packages installed: `apache2`, `mysql-server`, `php5`, and `php5-mysql`.</span></span> <span data-ttu-id="ff681-130">Их можно установить, перетащив вручную или воспользовавшись Tasksel.</span><span class="sxs-lookup"><span data-stu-id="ff681-130">You can install these packages by directly grabbing these packages or using Tasksel.</span></span>
<span data-ttu-id="ff681-131">Перед установкой требуется скачать и обновить списки пакетов.</span><span class="sxs-lookup"><span data-stu-id="ff681-131">Before installing you need to download and update package lists.</span></span>

```bash
sudo apt-get update
```

##### <a name="individual-packages"></a><span data-ttu-id="ff681-132">Установка отдельных пакетов</span><span class="sxs-lookup"><span data-stu-id="ff681-132">Individual packages</span></span>
<span data-ttu-id="ff681-133">Можно использовать apt-get.</span><span class="sxs-lookup"><span data-stu-id="ff681-133">Using apt-get:</span></span>

```bash
sudo apt-get install apache2 mysql-server php5 php5-mysql
```

##### <a name="using-tasksel"></a><span data-ttu-id="ff681-134">Установка с помощью Tasksel</span><span class="sxs-lookup"><span data-stu-id="ff681-134">Using tasksel</span></span>
<span data-ttu-id="ff681-135">В качестве альтернативы можно скачать Tasksel. Это инструмент Debian и Ubuntu, который устанавливает в систему несколько связанных пакетов в рамках одной скоординированной задачи.</span><span class="sxs-lookup"><span data-stu-id="ff681-135">Alternatively you can download Tasksel, a Debian/Ubuntu tool that installs multiple related packages as a coordinated "task" onto your system.</span></span>

```bash
sudo apt-get install tasksel
sudo tasksel install lamp-server
```

<span data-ttu-id="ff681-136">После выполнения одной из приведенных выше команд вам будет предложено установить эти пакеты и некоторые другие зависимости.</span><span class="sxs-lookup"><span data-stu-id="ff681-136">After running either of the previous options, you will be prompted to install these packages and various other dependencies.</span></span> <span data-ttu-id="ff681-137">Нажмите клавишу Y, а затем клавишу ВВОД, чтобы продолжить, и следуйте остальным указаниям по установке административного пароля для MySQL.</span><span class="sxs-lookup"><span data-stu-id="ff681-137">To set an administrative password for MySQL, press 'y' and then 'Enter' to continue, and follow any other prompts.</span></span> <span data-ttu-id="ff681-138">Это позволит установить минимальный набор расширений PHP, необходимый для использования PHP с MySQL.</span><span class="sxs-lookup"><span data-stu-id="ff681-138">This process installs the minimum required PHP extensions needed to use PHP with MySQL.</span></span> 

![][1]

<span data-ttu-id="ff681-139">Выполните следующую команду, чтобы увидеть другие расширения PHP, доступные как пакеты:</span><span class="sxs-lookup"><span data-stu-id="ff681-139">Run the following command to see other PHP extensions that are available as packages:</span></span>

```bash
apt-cache search php5
```

#### <a name="create-infophp-document"></a><span data-ttu-id="ff681-140">Создание документа info.php</span><span class="sxs-lookup"><span data-stu-id="ff681-140">Create info.php document</span></span>
<span data-ttu-id="ff681-141">Теперь можно проверить версию установленных компонентов Apache, MySQL и PHP из командной строки, введя `apache2 -v`, `mysql -v` или `php -v`.</span><span class="sxs-lookup"><span data-stu-id="ff681-141">You should now be able to check what version of Apache, MySQL, and PHP you have through the command line by typing `apache2 -v`, `mysql -v`, or `php -v`.</span></span>

<span data-ttu-id="ff681-142">Если вы хотите расширить тестирование, то можете создать страницу кратких сведений о PHP для просмотра в браузере.</span><span class="sxs-lookup"><span data-stu-id="ff681-142">If you would like to test further, you can create a quick PHP info page to view in a browser.</span></span> <span data-ttu-id="ff681-143">Создайте файл в текстовом редакторе Nano с помощью следующей команды.</span><span class="sxs-lookup"><span data-stu-id="ff681-143">Create a file with Nano text editor with this command:</span></span>

```bash
sudo nano /var/www/html/info.php
```

<span data-ttu-id="ff681-144">В текстовом редакторе Nano GNU добавьте следующие строки.</span><span class="sxs-lookup"><span data-stu-id="ff681-144">Within the GNU Nano text editor, add the following lines:</span></span>

```php
<?php
phpinfo();
?>
```

<span data-ttu-id="ff681-145">Сохраните файл и закройте текстовый редактор.</span><span class="sxs-lookup"><span data-stu-id="ff681-145">Then save and exit the text editor.</span></span>

<span data-ttu-id="ff681-146">Перезапустите Apache с помощью следующей команды, чтобы все новые установленные компоненты вступили в действие.</span><span class="sxs-lookup"><span data-stu-id="ff681-146">Restart Apache with this command so all new installs take effect.</span></span>

```bash
sudo service apache2 restart
```

## <a name="verify-lamp-successfully-installed"></a><span data-ttu-id="ff681-147">Проверка успешности установки LAMP</span><span class="sxs-lookup"><span data-stu-id="ff681-147">Verify LAMP successfully installed</span></span>
<span data-ttu-id="ff681-148">Теперь можно просмотреть созданную страницу сведений о PHP. Откройте браузер и перейдите по адресу http://youruniqueDNS/info.php.</span><span class="sxs-lookup"><span data-stu-id="ff681-148">Now you can check the PHP info page you created by opening a browser and going to http://youruniqueDNS/info.php.</span></span> <span data-ttu-id="ff681-149">Она должна выглядеть, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="ff681-149">It should look similar to this image.</span></span>

![][2]

<span data-ttu-id="ff681-150">Можно проверить установленный экземпляр Apache, просмотрев страницу по умолчанию Apache2 Ubuntu. Для этого перейдите по ссылке http://youruniqueDNS/.</span><span class="sxs-lookup"><span data-stu-id="ff681-150">You can check your Apache installation by viewing the Apache2 Ubuntu Default Page by going to you http://youruniqueDNS/.</span></span> <span data-ttu-id="ff681-151">Вы должны увидеть результат, аналогичный приведенному ниже.</span><span class="sxs-lookup"><span data-stu-id="ff681-151">The output is similar to the following example:</span></span>

![][3]

<span data-ttu-id="ff681-152">Поздравляем! Вы установили стек LAMP на виртуальную машину Azure.</span><span class="sxs-lookup"><span data-stu-id="ff681-152">Congratulations, you have just setup a LAMP stack on your Azure VM!</span></span>

## <a name="next-steps"></a><span data-ttu-id="ff681-153">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="ff681-153">Next steps</span></span>
<span data-ttu-id="ff681-154">Ознакомьтесь с документацией Ubuntu по стеку LAMP.</span><span class="sxs-lookup"><span data-stu-id="ff681-154">Check out the Ubuntu documentation on the LAMP stack:</span></span>

* [<span data-ttu-id="ff681-155">https://help.ubuntu.com/community/ApacheMySQLPHP</span><span class="sxs-lookup"><span data-stu-id="ff681-155">https://help.ubuntu.com/community/ApacheMySQLPHP</span></span>](https://help.ubuntu.com/community/ApacheMySQLPHP)

[1]: ./media/deploy-lamp-stack/configmysqlpassword-small.png
[2]: ./media/deploy-lamp-stack/phpsuccesspage.png
[3]: ./media/deploy-lamp-stack/apachesuccesspage.png
