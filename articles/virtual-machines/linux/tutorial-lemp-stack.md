---
title: "aaaDeploy LEMP на виртуальной машине Linux в Azure | Документы Microsoft"
description: "Учебник - Install hello LEMP стека на виртуальной Машине Linux в Azure"
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
ms.openlocfilehash: d8f9d84c5e9c0df4e9e985c10fe10f63a2f88214
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="install-a-lemp-web-server-on-an-azure-vm"></a><span data-ttu-id="7f543-103">Установка веб-сервера LEMP на виртуальной машине Azure</span><span class="sxs-lookup"><span data-stu-id="7f543-103">Install a LEMP web server on an Azure VM</span></span>
<span data-ttu-id="7f543-104">В этой статье рассматриваются как toodeploy NGINX веб-сервера, MySQL и PHP (hello LEMP стека) на Виртуальной машине Ubuntu в Azure.</span><span class="sxs-lookup"><span data-stu-id="7f543-104">This article walks you through how toodeploy an NGINX web server, MySQL, and PHP (hello LEMP stack) on an Ubuntu VM in Azure.</span></span> <span data-ttu-id="7f543-105">стек LEMP Hello — альтернативный популярных toohello [стек LAMP](tutorial-lamp-stack.md), которое также можно установить в Azure.</span><span class="sxs-lookup"><span data-stu-id="7f543-105">hello LEMP stack is an alternative toohello popular [LAMP stack](tutorial-lamp-stack.md), which you can also install in Azure.</span></span> <span data-ttu-id="7f543-106">сервер LEMP toosee hello в действии, при необходимости можно установить и настроить сайт WordPress.</span><span class="sxs-lookup"><span data-stu-id="7f543-106">toosee hello LEMP server in action, you can optionally install and configure a WordPress site.</span></span> <span data-ttu-id="7f543-107">Из этого руководства вы узнаете, как выполнить следующие задачи:</span><span class="sxs-lookup"><span data-stu-id="7f543-107">In this tutorial you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="7f543-108">Создание Виртуальной машине Ubuntu (hello «L» hello LEMP стека)</span><span class="sxs-lookup"><span data-stu-id="7f543-108">Create an Ubuntu VM (hello 'L' in hello LEMP stack)</span></span>
> * <span data-ttu-id="7f543-109">Открытие порта 80 для веб-трафика</span><span class="sxs-lookup"><span data-stu-id="7f543-109">Open port 80 for web traffic</span></span>
> * <span data-ttu-id="7f543-110">Установка NGINX, MySQL и PHP.</span><span class="sxs-lookup"><span data-stu-id="7f543-110">Install NGINX, MySQL, and PHP</span></span>
> * <span data-ttu-id="7f543-111">Проверка установки и настройки.</span><span class="sxs-lookup"><span data-stu-id="7f543-111">Verify installation and configuration</span></span>
> * <span data-ttu-id="7f543-112">Установка WordPress на сервере LEMP hello</span><span class="sxs-lookup"><span data-stu-id="7f543-112">Install WordPress on hello LEMP server</span></span>


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="7f543-113">Если выбрать tooinstall и использовать hello CLI локально, упражнений этого учебника требуется, вы используете версию Azure CLI hello 2.0.4 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="7f543-113">If you choose tooinstall and use hello CLI locally, this tutorial requires that you are running hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="7f543-114">Запустите `az --version` версии toofind hello.</span><span class="sxs-lookup"><span data-stu-id="7f543-114">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="7f543-115">Если требуется tooinstall или обновления, см. раздел [установить CLI Azure 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="7f543-115">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

[!INCLUDE [virtual-machines-linux-tutorial-stack-intro.md](../../../includes/virtual-machines-linux-tutorial-stack-intro.md)]

## <a name="install-nginx-mysql-and-php"></a><span data-ttu-id="7f543-116">Установка NGINX, MySQL и PHP.</span><span class="sxs-lookup"><span data-stu-id="7f543-116">Install NGINX, MySQL, and PHP</span></span>

<span data-ttu-id="7f543-117">Запустите следующие команды tooupdate Ubuntu пакета источники hello и установите NGINX, PHP и MySQL.</span><span class="sxs-lookup"><span data-stu-id="7f543-117">Run hello following command tooupdate Ubuntu package sources and install NGINX, MySQL, and PHP.</span></span> 

```bash
sudo apt update && sudo apt install nginx mysql-server php-mysql php php-fpm
```

<span data-ttu-id="7f543-118">Вы являетесь запрашиваемые tooinstall hello пакетов и других зависимостей.</span><span class="sxs-lookup"><span data-stu-id="7f543-118">You are prompted tooinstall hello packages and other dependencies.</span></span> <span data-ttu-id="7f543-119">При появлении запроса задайте пароль пользователя root для MySQL, а затем toocontinue [Enter].</span><span class="sxs-lookup"><span data-stu-id="7f543-119">When prompted, set a root password for MySQL, and then [Enter] toocontinue.</span></span> <span data-ttu-id="7f543-120">Выполните оставшиеся приглашения hello.</span><span class="sxs-lookup"><span data-stu-id="7f543-120">Follow hello remaining prompts.</span></span> <span data-ttu-id="7f543-121">Этот процесс устанавливает hello минимальные необходимые PHP необходимые расширения toouse PHP MySQL.</span><span class="sxs-lookup"><span data-stu-id="7f543-121">This process installs hello minimum required PHP extensions needed toouse PHP with MySQL.</span></span> 

![Страница с паролем привилегированного пользователя MySQL][1]

## <a name="verify-installation-and-configuration"></a><span data-ttu-id="7f543-123">Проверка установки и настройки.</span><span class="sxs-lookup"><span data-stu-id="7f543-123">Verify installation and configuration</span></span>


### <a name="nginx"></a><span data-ttu-id="7f543-124">NGINX</span><span class="sxs-lookup"><span data-stu-id="7f543-124">NGINX</span></span>

<span data-ttu-id="7f543-125">Проверьте версию hello NGINX hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="7f543-125">Check hello version of NGINX with hello following command:</span></span>
```bash
nginx -v
```

<span data-ttu-id="7f543-126">С NGINX установлены и порт 80 откройте tooyour виртуальных Машин, веб-сервер hello, теперь доступны из hello Интернета.</span><span class="sxs-lookup"><span data-stu-id="7f543-126">With NGINX installed, and port 80 open tooyour VM, hello web server can now be accessed from hello internet.</span></span> <span data-ttu-id="7f543-127">tooview hello NGINX страницы приветствия, откройте браузер и введите hello общедоступный IP-адрес hello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="7f543-127">tooview hello NGINX welcome page, open a web browser, and enter hello public IP address of hello VM.</span></span> <span data-ttu-id="7f543-128">Используйте общедоступный IP-адрес hello используется tooSSH toohello виртуальной Машины:</span><span class="sxs-lookup"><span data-stu-id="7f543-128">Use hello public IP address you used tooSSH toohello VM:</span></span>

![Страница NGINX по умолчанию][3]


### <a name="mysql"></a><span data-ttu-id="7f543-130">MySQL</span><span class="sxs-lookup"><span data-stu-id="7f543-130">MySQL</span></span>

<span data-ttu-id="7f543-131">Уточните hello версия MySQL hello следующую команду (Обратите внимание, прописная hello `V` параметра):</span><span class="sxs-lookup"><span data-stu-id="7f543-131">Check hello version of MySQL with hello following command (note hello capital `V` parameter):</span></span>

```bash
msql -V
```

<span data-ttu-id="7f543-132">Рекомендуется запускать после установки безопасного hello toohelp сценария MySQL hello:</span><span class="sxs-lookup"><span data-stu-id="7f543-132">We recommend running hello following script toohelp secure hello installation of MySQL:</span></span>

```bash
mysql_secure_installation
```

<span data-ttu-id="7f543-133">Введите пароль MySQL корневой и настройте параметры безопасности hello для вашей среды.</span><span class="sxs-lookup"><span data-stu-id="7f543-133">Enter your MySQL root password, and configure hello security settings for your environment.</span></span>

<span data-ttu-id="7f543-134">Если вы хотите toocreate базы данных MySQL, добавлять пользователей или изменения параметров конфигурации, tooMySQL входа:</span><span class="sxs-lookup"><span data-stu-id="7f543-134">If you want toocreate a MySQL database, add users, or change configuration settings, login tooMySQL:</span></span>

```bash
mysql -u root -p
```

<span data-ttu-id="7f543-135">Закончив, выйдите из hello mysql строки, введя `\q`.</span><span class="sxs-lookup"><span data-stu-id="7f543-135">When done, exit hello mysql prompt by typing `\q`.</span></span>

### <a name="php"></a><span data-ttu-id="7f543-136">PHP</span><span class="sxs-lookup"><span data-stu-id="7f543-136">PHP</span></span>

<span data-ttu-id="7f543-137">Проверьте версию PHP hello hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="7f543-137">Check hello version of PHP with hello following command:</span></span>

```bash
php -v
```

<span data-ttu-id="7f543-138">Настройте hello toouse NGINX диспетчер процессов FastCGI PHP (PHP-FPM).</span><span class="sxs-lookup"><span data-stu-id="7f543-138">Configure NGINX toouse hello PHP FastCGI Process Manager (PHP-FPM).</span></span> <span data-ttu-id="7f543-139">Выполните следующие команды tooback hello исходный сервер NGINX блокировать файл конфигурации, а затем измените hello исходный файл в редакторе, который предпочитаете hello.</span><span class="sxs-lookup"><span data-stu-id="7f543-139">Run hello following commands tooback up hello original NGINX server block config file and then edit hello original file in an editor of your choice:</span></span>

```bash
sudo cp /etc/nginx/sites-available/default /etc/nginx/sites-available/default_backup

sudo sensible-editor /etc/nginx/sites-available/default
```

<span data-ttu-id="7f543-140">В редакторе hello, замените содержимое hello `/etc/nginx/sites-available/default` hello следующее.</span><span class="sxs-lookup"><span data-stu-id="7f543-140">In hello editor, replace hello contents of `/etc/nginx/sites-available/default` with hello following.</span></span> <span data-ttu-id="7f543-141">См. комментарии hello объяснение параметров hello.</span><span class="sxs-lookup"><span data-stu-id="7f543-141">See hello comments for explanation of hello settings.</span></span> <span data-ttu-id="7f543-142">Замените hello общедоступный IP-адрес виртуальной Машины для *yourPublicIPAddress*и оставьте для оставшихся параметров hello.</span><span class="sxs-lookup"><span data-stu-id="7f543-142">Substitute hello public IP address of your VM for *yourPublicIPAddress*, and leave hello remaining settings.</span></span> <span data-ttu-id="7f543-143">Затем сохраните файл hello.</span><span class="sxs-lookup"><span data-stu-id="7f543-143">Then save hello file.</span></span>

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

<span data-ttu-id="7f543-144">Проверьте конфигурацию NGINX hello наличие синтаксических ошибок.</span><span class="sxs-lookup"><span data-stu-id="7f543-144">Check hello NGINX configuration for syntax errors:</span></span>

```bash
sudo nginx -t
```

<span data-ttu-id="7f543-145">Если имеет правильный синтаксис hello, перезапустите NGINX с hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="7f543-145">If hello syntax is correct, restart NGINX with hello following command:</span></span>

```bash
sudo service nginx restart
```

<span data-ttu-id="7f543-146">Tootest дальнейшей, создайте быстрый tooview страницы сведения о PHP в браузере.</span><span class="sxs-lookup"><span data-stu-id="7f543-146">If you want tootest further, create a quick PHP info page tooview in a browser.</span></span> <span data-ttu-id="7f543-147">Hello, следующая команда создает страница сведений о hello PHP:</span><span class="sxs-lookup"><span data-stu-id="7f543-147">hello following command creates hello PHP info page:</span></span>

```bash
sudo sh -c 'echo "<?php phpinfo(); ?>" > /var/www/html/info.php'
```



<span data-ttu-id="7f543-148">Теперь можно проверить hello PHP info созданная страница.</span><span class="sxs-lookup"><span data-stu-id="7f543-148">Now you can check hello PHP info page you created.</span></span> <span data-ttu-id="7f543-149">Откройте браузер и перейдите в слишком`http://yourPublicIPAddress/info.php`.</span><span class="sxs-lookup"><span data-stu-id="7f543-149">Open a browser and go too`http://yourPublicIPAddress/info.php`.</span></span> <span data-ttu-id="7f543-150">Замените hello общедоступный IP-адрес виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="7f543-150">Substitute hello public IP address of your VM.</span></span> <span data-ttu-id="7f543-151">Он должен выглядеть примерно toothis изображения.</span><span class="sxs-lookup"><span data-stu-id="7f543-151">It should look similar toothis image.</span></span>

![Страница сведений о PHP][2]


[!INCLUDE [virtual-machines-linux-tutorial-wordpress.md](../../../includes/virtual-machines-linux-tutorial-wordpress.md)]

## <a name="next-steps"></a><span data-ttu-id="7f543-153">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="7f543-153">Next steps</span></span>

<span data-ttu-id="7f543-154">Из этого руководства вы узнали, как развернуть сервер LEMP в Azure.</span><span class="sxs-lookup"><span data-stu-id="7f543-154">In this tutorial, you deployed a LEMP server in Azure.</span></span> <span data-ttu-id="7f543-155">Вы научились выполнять следующие задачи:</span><span class="sxs-lookup"><span data-stu-id="7f543-155">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="7f543-156">Создание виртуальной машины Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="7f543-156">Create an Ubuntu VM</span></span>
> * <span data-ttu-id="7f543-157">Открытие порта 80 для веб-трафика</span><span class="sxs-lookup"><span data-stu-id="7f543-157">Open port 80 for web traffic</span></span>
> * <span data-ttu-id="7f543-158">Установка NGINX, MySQL и PHP.</span><span class="sxs-lookup"><span data-stu-id="7f543-158">Install NGINX, MySQL, and PHP</span></span>
> * <span data-ttu-id="7f543-159">Проверка установки и настройки.</span><span class="sxs-lookup"><span data-stu-id="7f543-159">Verify installation and configuration</span></span>
> * <span data-ttu-id="7f543-160">Установка WordPress стеке LEMP hello</span><span class="sxs-lookup"><span data-stu-id="7f543-160">Install WordPress on hello LEMP stack</span></span>

<span data-ttu-id="7f543-161">Как переместить следующий учебник toolearn toohello toosecure веб-серверов с использованием сертификата SSL.</span><span class="sxs-lookup"><span data-stu-id="7f543-161">Advance toohello next tutorial toolearn how toosecure web servers with SSL certificates.</span></span>

> [!div class="nextstepaction"]
> <span data-ttu-id="7f543-162">[Secure a web server with SSL certificates on a Linux virtual machine in Azure](tutorial-secure-web-server.md) (Защита веб-сервера на виртуальной машине Linux в облаке Azure с помощью SSL-сертификата)</span><span class="sxs-lookup"><span data-stu-id="7f543-162">[Secure web server with SSL](tutorial-secure-web-server.md)</span></span>

[1]: ./media/tutorial-lemp-stack/configmysqlpassword-small.png
[2]: ./media/tutorial-lemp-stack/phpsuccesspage.png
[3]: ./media/tutorial-lemp-stack/nginx.png
