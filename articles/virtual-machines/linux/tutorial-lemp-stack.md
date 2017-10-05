---
title: "Развертывание LEMP на виртуальной машине Linux в Azure | Документация Майкрософт"
description: "Руководство по установке стека LEMP на виртуальной машине Linux в Azure"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: dlepow
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: azurecli
ms.topic: article
ms.date: 08/03/2017
ms.author: danlep
ms.openlocfilehash: 653af144eb12cacf955f96a5442efd73add38e88
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="install-a-lemp-web-server-on-an-azure-vm"></a><span data-ttu-id="e839b-103">Установка веб-сервера LEMP на виртуальной машине Azure</span><span class="sxs-lookup"><span data-stu-id="e839b-103">Install a LEMP web server on an Azure VM</span></span>
<span data-ttu-id="e839b-104">Эта статья содержит указания по развертыванию веб-сервера NGINX, MySQL и PHP (стека LEMP) на виртуальной машине Ubuntu в Azure.</span><span class="sxs-lookup"><span data-stu-id="e839b-104">This article walks you through how to deploy an NGINX web server, MySQL, and PHP (the LEMP stack) on an Ubuntu VM in Azure.</span></span> <span data-ttu-id="e839b-105">Стек LEMP является альтернативой известному [стеку LAMP](tutorial-lamp-stack.md), который также можно установить в Azure.</span><span class="sxs-lookup"><span data-stu-id="e839b-105">The LEMP stack is an alternative to the popular [LAMP stack](tutorial-lamp-stack.md), which you can also install in Azure.</span></span> <span data-ttu-id="e839b-106">Чтобы оценить работу сервера LEMP в действии, вы можете установить и настроить сайт WordPress.</span><span class="sxs-lookup"><span data-stu-id="e839b-106">To see the LEMP server in action, you can optionally install and configure a WordPress site.</span></span> <span data-ttu-id="e839b-107">Из этого руководства вы узнаете, как выполнить следующие задачи:</span><span class="sxs-lookup"><span data-stu-id="e839b-107">In this tutorial you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="e839b-108">Создание виртуальной машины Ubuntu ("L" в названии стека LEMP).</span><span class="sxs-lookup"><span data-stu-id="e839b-108">Create an Ubuntu VM (the 'L' in the LEMP stack)</span></span>
> * <span data-ttu-id="e839b-109">Открытие порта 80 для веб-трафика</span><span class="sxs-lookup"><span data-stu-id="e839b-109">Open port 80 for web traffic</span></span>
> * <span data-ttu-id="e839b-110">Установка NGINX, MySQL и PHP.</span><span class="sxs-lookup"><span data-stu-id="e839b-110">Install NGINX, MySQL, and PHP</span></span>
> * <span data-ttu-id="e839b-111">Проверка установки и настройки.</span><span class="sxs-lookup"><span data-stu-id="e839b-111">Verify installation and configuration</span></span>
> * <span data-ttu-id="e839b-112">Установка WordPress на сервере LEMP.</span><span class="sxs-lookup"><span data-stu-id="e839b-112">Install WordPress on the LEMP server</span></span>


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="e839b-113">Если вы решили установить и использовать интерфейс командной строки локально, то для работы с этим руководством вам понадобится Azure CLI 2.0.4 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="e839b-113">If you choose to install and use the CLI locally, this tutorial requires that you are running the Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="e839b-114">Чтобы узнать версию, выполните команду `az --version`.</span><span class="sxs-lookup"><span data-stu-id="e839b-114">Run `az --version` to find the version.</span></span> <span data-ttu-id="e839b-115">Если вам необходимо выполнить установку или обновление, см. статью [Установка Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="e839b-115">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

[!INCLUDE [virtual-machines-linux-tutorial-stack-intro.md](../../../includes/virtual-machines-linux-tutorial-stack-intro.md)]

## <a name="install-nginx-mysql-and-php"></a><span data-ttu-id="e839b-116">Установка NGINX, MySQL и PHP.</span><span class="sxs-lookup"><span data-stu-id="e839b-116">Install NGINX, MySQL, and PHP</span></span>

<span data-ttu-id="e839b-117">Чтобы обновить источники пакетов Ubuntu и установить NGINX, PHP и MySQL, выполните команду ниже.</span><span class="sxs-lookup"><span data-stu-id="e839b-117">Run the following command to update Ubuntu package sources and install NGINX, MySQL, and PHP.</span></span> 

```bash
sudo apt update && sudo apt install nginx mysql-server php-mysql php php-fpm
```

<span data-ttu-id="e839b-118">Отобразится запрос на установку пакетов и других зависимостей.</span><span class="sxs-lookup"><span data-stu-id="e839b-118">You are prompted to install the packages and other dependencies.</span></span> <span data-ttu-id="e839b-119">При появлении запроса укажите пароль привилегированного пользователя для MySQL, а затем нажмите клавишу ВВОД для продолжения.</span><span class="sxs-lookup"><span data-stu-id="e839b-119">When prompted, set a root password for MySQL, and then [Enter] to continue.</span></span> <span data-ttu-id="e839b-120">Выполните оставшиеся инструкции на экране.</span><span class="sxs-lookup"><span data-stu-id="e839b-120">Follow the remaining prompts.</span></span> <span data-ttu-id="e839b-121">Это позволит установить минимальный набор расширений PHP, необходимый для использования PHP с MySQL.</span><span class="sxs-lookup"><span data-stu-id="e839b-121">This process installs the minimum required PHP extensions needed to use PHP with MySQL.</span></span> 

![Страница с паролем привилегированного пользователя MySQL][1]

## <a name="verify-installation-and-configuration"></a><span data-ttu-id="e839b-123">Проверка установки и настройки.</span><span class="sxs-lookup"><span data-stu-id="e839b-123">Verify installation and configuration</span></span>


### <a name="nginx"></a><span data-ttu-id="e839b-124">NGINX</span><span class="sxs-lookup"><span data-stu-id="e839b-124">NGINX</span></span>

<span data-ttu-id="e839b-125">Узнайте версию NGINX с помощью следующей команды:</span><span class="sxs-lookup"><span data-stu-id="e839b-125">Check the version of NGINX with the following command:</span></span>
```bash
nginx -v
```

<span data-ttu-id="e839b-126">Установив NGINX и открыв порт 80 для виртуальной машины, вы можете получить доступ к веб-серверу через Интернет.</span><span class="sxs-lookup"><span data-stu-id="e839b-126">With NGINX installed, and port 80 open to your VM, the web server can now be accessed from the internet.</span></span> <span data-ttu-id="e839b-127">Откройте веб-браузер и введите общедоступный IP-адрес виртуальной машины, чтобы перейти на страницу приветствия NGINX.</span><span class="sxs-lookup"><span data-stu-id="e839b-127">To view the NGINX welcome page, open a web browser, and enter the public IP address of the VM.</span></span> <span data-ttu-id="e839b-128">Укажите общедоступный IP-адрес, используемый для подключения по протоколу SSH к виртуальной машине.</span><span class="sxs-lookup"><span data-stu-id="e839b-128">Use the public IP address you used to SSH to the VM:</span></span>

![Страница NGINX по умолчанию][3]


### <a name="mysql"></a><span data-ttu-id="e839b-130">MySQL</span><span class="sxs-lookup"><span data-stu-id="e839b-130">MySQL</span></span>

<span data-ttu-id="e839b-131">Узнайте версию MySQL, выполнив указанную ниже команду. Обратите внимание, что параметр `V` указан с заглавной буквы.</span><span class="sxs-lookup"><span data-stu-id="e839b-131">Check the version of MySQL with the following command (note the capital `V` parameter):</span></span>

```bash
msql -V
```

<span data-ttu-id="e839b-132">Чтобы обеспечить безопасную установку MySQL, мы рекомендуем выполнить следующий скрипт:</span><span class="sxs-lookup"><span data-stu-id="e839b-132">We recommend running the following script to help secure the installation of MySQL:</span></span>

```bash
mysql_secure_installation
```

<span data-ttu-id="e839b-133">Введите пароль привилегированного пользователя MySQL и настройте параметры безопасности для своей среды.</span><span class="sxs-lookup"><span data-stu-id="e839b-133">Enter your MySQL root password, and configure the security settings for your environment.</span></span>

<span data-ttu-id="e839b-134">Чтобы создать базу данных MySQL, добавить пользователей или изменить параметры конфигурации, войдите в MySQL.</span><span class="sxs-lookup"><span data-stu-id="e839b-134">If you want to create a MySQL database, add users, or change configuration settings, login to MySQL:</span></span>

```bash
mysql -u root -p
```

<span data-ttu-id="e839b-135">По окончании выйдите из командной строки MySQL, введя `\q`.</span><span class="sxs-lookup"><span data-stu-id="e839b-135">When done, exit the mysql prompt by typing `\q`.</span></span>

### <a name="php"></a><span data-ttu-id="e839b-136">PHP</span><span class="sxs-lookup"><span data-stu-id="e839b-136">PHP</span></span>

<span data-ttu-id="e839b-137">Узнайте версию PHP, выполнив следующую команду:</span><span class="sxs-lookup"><span data-stu-id="e839b-137">Check the version of PHP with the following command:</span></span>

```bash
php -v
```

<span data-ttu-id="e839b-138">Настройте NGINX, чтобы использовать менеджер процессов FastCGI PHP (PHP-FPM).</span><span class="sxs-lookup"><span data-stu-id="e839b-138">Configure NGINX to use the PHP FastCGI Process Manager (PHP-FPM).</span></span> <span data-ttu-id="e839b-139">Чтобы создать резервную копию исходного файла конфигурации для блока сервера NGINX, а затем изменить этот файл в текстовом редакторе, выполните следующие команды:</span><span class="sxs-lookup"><span data-stu-id="e839b-139">Run the following commands to back up the original NGINX server block config file and then edit the original file in an editor of your choice:</span></span>

```bash
sudo cp /etc/nginx/sites-available/default /etc/nginx/sites-available/default_backup

sudo sensible-editor /etc/nginx/sites-available/default
```

<span data-ttu-id="e839b-140">В редакторе замените содержимое `/etc/nginx/sites-available/default` кодом ниже.</span><span class="sxs-lookup"><span data-stu-id="e839b-140">In the editor, replace the contents of `/etc/nginx/sites-available/default` with the following.</span></span> <span data-ttu-id="e839b-141">Описания параметров см. в комментариях.</span><span class="sxs-lookup"><span data-stu-id="e839b-141">See the comments for explanation of the settings.</span></span> <span data-ttu-id="e839b-142">Замените общедоступный IP-адрес виртуальной машины на *свой_общедоступный_IP-адрес*, а остальные параметры оставьте без изменений.</span><span class="sxs-lookup"><span data-stu-id="e839b-142">Substitute the public IP address of your VM for *yourPublicIPAddress*, and leave the remaining settings.</span></span> <span data-ttu-id="e839b-143">Затем сохраните файл.</span><span class="sxs-lookup"><span data-stu-id="e839b-143">Then save the file.</span></span>

```
server {
    listen 80 default_server;
    listen [::]:80 default_server;

    root /var/www/html;
    # Homepage of website is index.php
    index index.php;

    server_name yourPublicIPAddress;

    location / {
        try_files $uri $uri/ =404;
    }

    # Include FastCGI configuration for NGINX
    location ~ \.php$ {
        include snippets/fastcgi-php.conf;
        fastcgi_pass unix:/run/php/php7.0-fpm.sock;
    }
}
```

<span data-ttu-id="e839b-144">Проверьте наличие синтаксических ошибок в конфигурации NGINX.</span><span class="sxs-lookup"><span data-stu-id="e839b-144">Check the NGINX configuration for syntax errors:</span></span>

```bash
sudo nginx -t
```

<span data-ttu-id="e839b-145">Если синтаксис правильный, перезапустите NGINX с помощью следующей команды:</span><span class="sxs-lookup"><span data-stu-id="e839b-145">If the syntax is correct, restart NGINX with the following command:</span></span>

```bash
sudo service nginx restart
```

<span data-ttu-id="e839b-146">Для дальнейшего тестирования создайте страницу кратких сведений о PHP для просмотра в браузере.</span><span class="sxs-lookup"><span data-stu-id="e839b-146">If you want to test further, create a quick PHP info page to view in a browser.</span></span> <span data-ttu-id="e839b-147">Следующая команда создает страницу сведений о PHP:</span><span class="sxs-lookup"><span data-stu-id="e839b-147">The following command creates the PHP info page:</span></span>

```bash
sudo sh -c 'echo "<?php phpinfo(); ?>" > /var/www/html/info.php'
```



<span data-ttu-id="e839b-148">Теперь можно просмотреть созданную страницу сведений о PHP.</span><span class="sxs-lookup"><span data-stu-id="e839b-148">Now you can check the PHP info page you created.</span></span> <span data-ttu-id="e839b-149">Откройте браузер и перейдите на страницу `http://yourPublicIPAddress/info.php`.</span><span class="sxs-lookup"><span data-stu-id="e839b-149">Open a browser and go to `http://yourPublicIPAddress/info.php`.</span></span> <span data-ttu-id="e839b-150">Замените общедоступный IP-адрес своей виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="e839b-150">Substitute the public IP address of your VM.</span></span> <span data-ttu-id="e839b-151">Она должна выглядеть, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="e839b-151">It should look similar to this image.</span></span>

![Страница сведений о PHP][2]


[!INCLUDE [virtual-machines-linux-tutorial-wordpress.md](../../../includes/virtual-machines-linux-tutorial-wordpress.md)]

## <a name="next-steps"></a><span data-ttu-id="e839b-153">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="e839b-153">Next steps</span></span>

<span data-ttu-id="e839b-154">Из этого руководства вы узнали, как развернуть сервер LEMP в Azure.</span><span class="sxs-lookup"><span data-stu-id="e839b-154">In this tutorial, you deployed a LEMP server in Azure.</span></span> <span data-ttu-id="e839b-155">Вы научились выполнять следующие задачи:</span><span class="sxs-lookup"><span data-stu-id="e839b-155">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="e839b-156">Создание виртуальной машины Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="e839b-156">Create an Ubuntu VM</span></span>
> * <span data-ttu-id="e839b-157">Открытие порта 80 для веб-трафика</span><span class="sxs-lookup"><span data-stu-id="e839b-157">Open port 80 for web traffic</span></span>
> * <span data-ttu-id="e839b-158">Установка NGINX, MySQL и PHP.</span><span class="sxs-lookup"><span data-stu-id="e839b-158">Install NGINX, MySQL, and PHP</span></span>
> * <span data-ttu-id="e839b-159">Проверка установки и настройки.</span><span class="sxs-lookup"><span data-stu-id="e839b-159">Verify installation and configuration</span></span>
> * <span data-ttu-id="e839b-160">Установка WordPress в стеке LEMP.</span><span class="sxs-lookup"><span data-stu-id="e839b-160">Install WordPress on the LEMP stack</span></span>

<span data-ttu-id="e839b-161">Перейдите к следующему руководству, чтобы узнать, как защитить веб-серверы с помощью SSL-сертификатов.</span><span class="sxs-lookup"><span data-stu-id="e839b-161">Advance to the next tutorial to learn how to secure web servers with SSL certificates.</span></span>

> [!div class="nextstepaction"]
> <span data-ttu-id="e839b-162">[Secure a web server with SSL certificates on a Linux virtual machine in Azure](tutorial-secure-web-server.md) (Защита веб-сервера на виртуальной машине Linux в облаке Azure с помощью SSL-сертификата)</span><span class="sxs-lookup"><span data-stu-id="e839b-162">[Secure web server with SSL](tutorial-secure-web-server.md)</span></span>

[1]: ./media/tutorial-lemp-stack/configmysqlpassword-small.png
[2]: ./media/tutorial-lemp-stack/phpsuccesspage.png
[3]: ./media/tutorial-lemp-stack/nginx.png
