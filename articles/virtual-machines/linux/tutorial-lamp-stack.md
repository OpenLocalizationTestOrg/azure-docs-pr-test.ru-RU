---
title: "Развертывание LAMP на виртуальной машине Linux в Azure | Документация Майкрософт"
description: "Руководство по установке стека LAMP на виртуальной машине Linux в Azure"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: dlepow
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 6c12603a-e391-4d3e-acce-442dd7ebb2fe
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: azurecli
ms.topic: article
ms.date: 08/03/2017
ms.author: danlep
ms.openlocfilehash: 9148ac9646e4e1cfeff8f20c096e390499437e78
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="install-a-lamp-web-server-on-an-azure-vm"></a><span data-ttu-id="eef93-103">Установка веб-сервера LAMP на виртуальной машине Azure</span><span class="sxs-lookup"><span data-stu-id="eef93-103">Install a LAMP web server on an Azure VM</span></span>
<span data-ttu-id="eef93-104">Эта статья содержит указания по развертыванию веб-сервера Apache, MySQL и PHP (стека LAMP) на виртуальной машине Ubuntu в Azure.</span><span class="sxs-lookup"><span data-stu-id="eef93-104">This article walks you through how to deploy an Apache web server, MySQL, and PHP (the LAMP stack) on an Ubuntu VM in Azure.</span></span> <span data-ttu-id="eef93-105">Если вы хотите использовать веб-сервер NGINX, ознакомьтесь с руководством [Install a LEMP web server on an Azure VM](tutorial-lemp-stack.md) (Установка веб-сервера LEMP на виртуальной машине Azure).</span><span class="sxs-lookup"><span data-stu-id="eef93-105">If you prefer the NGINX web server, see the [LEMP stack](tutorial-lemp-stack.md) tutorial.</span></span> <span data-ttu-id="eef93-106">Если необходимо оценить работу сервера LAMP в действии, вы можете установить и настроить сайт WordPress.</span><span class="sxs-lookup"><span data-stu-id="eef93-106">To see the LAMP server in action, you can optionally install and configure a WordPress site.</span></span> <span data-ttu-id="eef93-107">Из этого руководства вы узнаете, как выполнить следующие задачи:</span><span class="sxs-lookup"><span data-stu-id="eef93-107">In this tutorial you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="eef93-108">создание виртуальной машины Ubuntu (L в названии стека LAMP);</span><span class="sxs-lookup"><span data-stu-id="eef93-108">Create an Ubuntu VM (the 'L' in the LAMP stack)</span></span>
> * <span data-ttu-id="eef93-109">Открытие порта 80 для веб-трафика</span><span class="sxs-lookup"><span data-stu-id="eef93-109">Open port 80 for web traffic</span></span>
> * <span data-ttu-id="eef93-110">Установка Apache, PHP и MySQL</span><span class="sxs-lookup"><span data-stu-id="eef93-110">Install Apache, MySQL, and PHP</span></span>
> * <span data-ttu-id="eef93-111">проверка установки и настройки;</span><span class="sxs-lookup"><span data-stu-id="eef93-111">Verify installation and configuration</span></span>
> * <span data-ttu-id="eef93-112">установка WordPress на сервере LAMP.</span><span class="sxs-lookup"><span data-stu-id="eef93-112">Install WordPress on the LAMP server</span></span>


<span data-ttu-id="eef93-113">Дополнительные сведения о стеке LAMP, включая рекомендации для рабочей среды, см. в [документации Ubuntu](https://help.ubuntu.com/community/ApacheMySQLPHP).</span><span class="sxs-lookup"><span data-stu-id="eef93-113">For more on the LAMP stack, including recommendations for a production environment, see the [Ubuntu documentation](https://help.ubuntu.com/community/ApacheMySQLPHP).</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="eef93-114">Если вы решили установить и использовать интерфейс командной строки локально, то для работы с этим руководством вам понадобится Azure CLI 2.0.4 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="eef93-114">If you choose to install and use the CLI locally, this tutorial requires that you are running the Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="eef93-115">Чтобы узнать версию, выполните команду `az --version`.</span><span class="sxs-lookup"><span data-stu-id="eef93-115">Run `az --version` to find the version.</span></span> <span data-ttu-id="eef93-116">Если вам необходимо выполнить установку или обновление, см. статью [Установка Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="eef93-116">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

[!INCLUDE [virtual-machines-linux-tutorial-stack-intro.md](../../../includes/virtual-machines-linux-tutorial-stack-intro.md)]

## <a name="install-apache-mysql-and-php"></a><span data-ttu-id="eef93-117">Установка Apache, PHP и MySQL</span><span class="sxs-lookup"><span data-stu-id="eef93-117">Install Apache, MySQL, and PHP</span></span>

<span data-ttu-id="eef93-118">Чтобы обновить источники пакетов Ubuntu и установить Apache, PHP и MySQL, выполните указанную ниже команду.</span><span class="sxs-lookup"><span data-stu-id="eef93-118">Run the following command to update Ubuntu package sources and install Apache, MySQL, and PHP.</span></span> <span data-ttu-id="eef93-119">Обратите внимание на символ крышки (^) в конце команды.</span><span class="sxs-lookup"><span data-stu-id="eef93-119">Note the caret (^) at the end of the command.</span></span>


```bash
sudo apt update && sudo apt install lamp-server^
```



<span data-ttu-id="eef93-120">Отобразится запрос на установку пакетов и других зависимостей.</span><span class="sxs-lookup"><span data-stu-id="eef93-120">You are prompted to install the packages and other dependencies.</span></span> <span data-ttu-id="eef93-121">При появлении запроса укажите пароль привилегированного пользователя для MySQL, а затем нажмите клавишу ВВОД для продолжения.</span><span class="sxs-lookup"><span data-stu-id="eef93-121">When prompted, set a root password for MySQL, and then [Enter] to continue.</span></span> <span data-ttu-id="eef93-122">Выполните оставшиеся инструкции на экране.</span><span class="sxs-lookup"><span data-stu-id="eef93-122">Follow the remaining prompts.</span></span> <span data-ttu-id="eef93-123">Это позволит установить минимальный набор расширений PHP, необходимый для использования PHP с MySQL.</span><span class="sxs-lookup"><span data-stu-id="eef93-123">This process installs the minimum required PHP extensions needed to use PHP with MySQL.</span></span> 

![Страница с паролем привилегированного пользователя MySQL][1]

## <a name="verify-installation-and-configuration"></a><span data-ttu-id="eef93-125">Проверка установки и настройки.</span><span class="sxs-lookup"><span data-stu-id="eef93-125">Verify installation and configuration</span></span>


### <a name="apache"></a><span data-ttu-id="eef93-126">Apache</span><span class="sxs-lookup"><span data-stu-id="eef93-126">Apache</span></span>

<span data-ttu-id="eef93-127">Проверьте версию Apache, выполнив следующую команду:</span><span class="sxs-lookup"><span data-stu-id="eef93-127">Check the version of Apache with the following command:</span></span>
```bash
apache2 -v
```

<span data-ttu-id="eef93-128">Установив Apache и открыв порт 80 для виртуальной машины, вы можете получить доступ к веб-серверу через Интернет.</span><span class="sxs-lookup"><span data-stu-id="eef93-128">With Apache installed, and port 80 open to your VM, the web server can now be accessed from the internet.</span></span> <span data-ttu-id="eef93-129">Чтобы просмотреть страницу по умолчанию Apache2 Ubuntu, откройте веб-браузер и введите общедоступный IP-адрес виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="eef93-129">To view the Apache2 Ubuntu Default Page, open a web browser, and enter the public IP address of the VM.</span></span> <span data-ttu-id="eef93-130">Укажите общедоступный IP-адрес, используемый для подключения по протоколу SSH к виртуальной машине.</span><span class="sxs-lookup"><span data-stu-id="eef93-130">Use the public IP address you used to SSH to the VM:</span></span>

![Страница Apache по умолчанию][3]


### <a name="mysql"></a><span data-ttu-id="eef93-132">MySQL</span><span class="sxs-lookup"><span data-stu-id="eef93-132">MySQL</span></span>

<span data-ttu-id="eef93-133">Узнайте версию MySQL, выполнив указанную ниже команду. Обратите внимание, что параметр `V` указан с заглавной буквы.</span><span class="sxs-lookup"><span data-stu-id="eef93-133">Check the version of MySQL with the following command (note the capital `V` parameter):</span></span>

```bash
msql -V
```

<span data-ttu-id="eef93-134">Чтобы обеспечить безопасную установку MySQL, мы рекомендуем выполнить следующий скрипт:</span><span class="sxs-lookup"><span data-stu-id="eef93-134">We recommend running the following script to help secure the installation of MySQL:</span></span>

```bash
mysql_secure_installation
```

<span data-ttu-id="eef93-135">Введите пароль привилегированного пользователя MySQL и настройте параметры безопасности для своей среды.</span><span class="sxs-lookup"><span data-stu-id="eef93-135">Enter your MySQL root password, and configure the security settings for your environment.</span></span>

<span data-ttu-id="eef93-136">Чтобы создать базу данных MySQL, добавить пользователей или изменить параметры конфигурации, войдите в MySQL.</span><span class="sxs-lookup"><span data-stu-id="eef93-136">If you want to create a MySQL database, add users, or change configuration settings, login to MySQL:</span></span>

```bash
mysql -u root -p
```

<span data-ttu-id="eef93-137">По окончании выйдите из командной строки MySQL, введя `\q`.</span><span class="sxs-lookup"><span data-stu-id="eef93-137">When done, exit the mysql prompt by typing `\q`.</span></span>

### <a name="php"></a><span data-ttu-id="eef93-138">PHP</span><span class="sxs-lookup"><span data-stu-id="eef93-138">PHP</span></span>

<span data-ttu-id="eef93-139">Узнайте версию PHP, выполнив следующую команду:</span><span class="sxs-lookup"><span data-stu-id="eef93-139">Check the version of PHP with the following command:</span></span>

```bash
php -v
```

<span data-ttu-id="eef93-140">Для дальнейшего тестирования создайте страницу кратких сведений о PHP для просмотра в браузере.</span><span class="sxs-lookup"><span data-stu-id="eef93-140">If you want to test further, create a quick PHP info page to view in a browser.</span></span> <span data-ttu-id="eef93-141">Следующая команда создает страницу сведений о PHP:</span><span class="sxs-lookup"><span data-stu-id="eef93-141">The following command creates the PHP info page:</span></span>

```bash
sudo sh -c 'echo "<?php phpinfo(); ?>" > /var/www/html/info.php'
```

<span data-ttu-id="eef93-142">Теперь можно просмотреть созданную страницу сведений о PHP.</span><span class="sxs-lookup"><span data-stu-id="eef93-142">Now you can check the PHP info page you created.</span></span> <span data-ttu-id="eef93-143">Откройте браузер и перейдите на страницу `http://yourPublicIPAddress/info.php`.</span><span class="sxs-lookup"><span data-stu-id="eef93-143">Open a browser and go to `http://yourPublicIPAddress/info.php`.</span></span> <span data-ttu-id="eef93-144">Замените общедоступный IP-адрес своей виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="eef93-144">Substitute the public IP address of your VM.</span></span> <span data-ttu-id="eef93-145">Она должна выглядеть, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="eef93-145">It should look similar to this image.</span></span>

![Страница сведений о PHP][2]

[!INCLUDE [virtual-machines-linux-tutorial-wordpress.md](../../../includes/virtual-machines-linux-tutorial-wordpress.md)]


## <a name="next-steps"></a><span data-ttu-id="eef93-147">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="eef93-147">Next steps</span></span>

<span data-ttu-id="eef93-148">Из этого руководства вы узнали, как развернуть сервер LAMP в Azure.</span><span class="sxs-lookup"><span data-stu-id="eef93-148">In this tutorial, you deployed a LAMP server in Azure.</span></span> <span data-ttu-id="eef93-149">Вы научились выполнять следующие задачи:</span><span class="sxs-lookup"><span data-stu-id="eef93-149">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="eef93-150">Создание виртуальной машины Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="eef93-150">Create an Ubuntu VM</span></span>
> * <span data-ttu-id="eef93-151">Открытие порта 80 для веб-трафика</span><span class="sxs-lookup"><span data-stu-id="eef93-151">Open port 80 for web traffic</span></span>
> * <span data-ttu-id="eef93-152">Установка Apache, PHP и MySQL</span><span class="sxs-lookup"><span data-stu-id="eef93-152">Install Apache, MySQL, and PHP</span></span>
> * <span data-ttu-id="eef93-153">проверка установки и настройки;</span><span class="sxs-lookup"><span data-stu-id="eef93-153">Verify installation and configuration</span></span>
> * <span data-ttu-id="eef93-154">установка WordPress на сервере LAMP.</span><span class="sxs-lookup"><span data-stu-id="eef93-154">Install WordPress on the LAMP server</span></span>

<span data-ttu-id="eef93-155">Перейдите к следующему руководству, чтобы узнать, как защитить веб-серверы с помощью SSL-сертификатов.</span><span class="sxs-lookup"><span data-stu-id="eef93-155">Advance to the next tutorial to learn how to secure web servers with SSL certificates.</span></span>

> [!div class="nextstepaction"]
> <span data-ttu-id="eef93-156">[Secure a web server with SSL certificates on a Linux virtual machine in Azure](tutorial-secure-web-server.md) (Защита веб-сервера на виртуальной машине Linux в облаке Azure с помощью SSL-сертификата)</span><span class="sxs-lookup"><span data-stu-id="eef93-156">[Secure web server with SSL](tutorial-secure-web-server.md)</span></span>

[1]: ./media/tutorial-lamp-stack/configmysqlpassword-small.png
[2]: ./media/tutorial-lamp-stack/phpsuccesspage.png
[3]: ./media/tutorial-lamp-stack/apachesuccesspage.png