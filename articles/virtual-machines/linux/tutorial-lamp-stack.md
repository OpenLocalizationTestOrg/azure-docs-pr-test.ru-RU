---
title: "aaaDeploy LAMP на виртуальной машине Linux в Azure | Документы Microsoft"
description: "Учебник - стек LAMP hello установки на виртуальной Машине Linux в Azure"
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
ms.openlocfilehash: a3d0ecb3277f15bd0a2fdc0d85b738a760e68865
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="install-a-lamp-web-server-on-an-azure-vm"></a><span data-ttu-id="030af-103">Установка веб-сервера LAMP на виртуальной машине Azure</span><span class="sxs-lookup"><span data-stu-id="030af-103">Install a LAMP web server on an Azure VM</span></span>
<span data-ttu-id="030af-104">В этой статье рассматриваются как toodeploy Apache веб-сервера, MySQL и PHP (стек LAMP hello) на Виртуальной машине Ubuntu в Azure.</span><span class="sxs-lookup"><span data-stu-id="030af-104">This article walks you through how toodeploy an Apache web server, MySQL, and PHP (hello LAMP stack) on an Ubuntu VM in Azure.</span></span> <span data-ttu-id="030af-105">При желании веб-сервер NGINX hello. в разделе hello [LEMP стека](tutorial-lemp-stack.md) учебника.</span><span class="sxs-lookup"><span data-stu-id="030af-105">If you prefer hello NGINX web server, see hello [LEMP stack](tutorial-lemp-stack.md) tutorial.</span></span> <span data-ttu-id="030af-106">сервер LAMP toosee hello в действии, при необходимости можно установить и настроить сайт WordPress.</span><span class="sxs-lookup"><span data-stu-id="030af-106">toosee hello LAMP server in action, you can optionally install and configure a WordPress site.</span></span> <span data-ttu-id="030af-107">Из этого руководства вы узнаете, как выполнить следующие задачи:</span><span class="sxs-lookup"><span data-stu-id="030af-107">In this tutorial you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="030af-108">Создание Виртуальной машине Ubuntu (hello «L» hello LAMP стека)</span><span class="sxs-lookup"><span data-stu-id="030af-108">Create an Ubuntu VM (hello 'L' in hello LAMP stack)</span></span>
> * <span data-ttu-id="030af-109">Открытие порта 80 для веб-трафика</span><span class="sxs-lookup"><span data-stu-id="030af-109">Open port 80 for web traffic</span></span>
> * <span data-ttu-id="030af-110">Установка Apache, PHP и MySQL</span><span class="sxs-lookup"><span data-stu-id="030af-110">Install Apache, MySQL, and PHP</span></span>
> * <span data-ttu-id="030af-111">Проверка установки и настройки.</span><span class="sxs-lookup"><span data-stu-id="030af-111">Verify installation and configuration</span></span>
> * <span data-ttu-id="030af-112">Установка WordPress на сервере LAMP hello</span><span class="sxs-lookup"><span data-stu-id="030af-112">Install WordPress on hello LAMP server</span></span>


<span data-ttu-id="030af-113">Дополнительные сведения о стек LAMP hello, включая рекомендации для рабочей среды, в разделе hello [документации Ubuntu](https://help.ubuntu.com/community/ApacheMySQLPHP).</span><span class="sxs-lookup"><span data-stu-id="030af-113">For more on hello LAMP stack, including recommendations for a production environment, see hello [Ubuntu documentation](https://help.ubuntu.com/community/ApacheMySQLPHP).</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="030af-114">Если выбрать tooinstall и использовать hello CLI локально, упражнений этого учебника требуется, вы используете версию Azure CLI hello 2.0.4 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="030af-114">If you choose tooinstall and use hello CLI locally, this tutorial requires that you are running hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="030af-115">Запустите `az --version` версии toofind hello.</span><span class="sxs-lookup"><span data-stu-id="030af-115">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="030af-116">Если требуется tooinstall или обновления, см. раздел [установить CLI Azure 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="030af-116">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

[!INCLUDE [virtual-machines-linux-tutorial-stack-intro.md](../../../includes/virtual-machines-linux-tutorial-stack-intro.md)]

## <a name="install-apache-mysql-and-php"></a><span data-ttu-id="030af-117">Установка Apache, PHP и MySQL</span><span class="sxs-lookup"><span data-stu-id="030af-117">Install Apache, MySQL, and PHP</span></span>

<span data-ttu-id="030af-118">Запустите следующие команды tooupdate Ubuntu пакета источники hello и установите Apache, PHP и MySQL.</span><span class="sxs-lookup"><span data-stu-id="030af-118">Run hello following command tooupdate Ubuntu package sources and install Apache, MySQL, and PHP.</span></span> <span data-ttu-id="030af-119">Обратите внимание, hello крышки (^) в конце hello команда hello.</span><span class="sxs-lookup"><span data-stu-id="030af-119">Note hello caret (^) at hello end of hello command.</span></span>


```bash
sudo apt update && sudo apt install lamp-server^
```



<span data-ttu-id="030af-120">Вы являетесь запрашиваемые tooinstall hello пакетов и других зависимостей.</span><span class="sxs-lookup"><span data-stu-id="030af-120">You are prompted tooinstall hello packages and other dependencies.</span></span> <span data-ttu-id="030af-121">При появлении запроса задайте пароль пользователя root для MySQL, а затем toocontinue [Enter].</span><span class="sxs-lookup"><span data-stu-id="030af-121">When prompted, set a root password for MySQL, and then [Enter] toocontinue.</span></span> <span data-ttu-id="030af-122">Выполните оставшиеся приглашения hello.</span><span class="sxs-lookup"><span data-stu-id="030af-122">Follow hello remaining prompts.</span></span> <span data-ttu-id="030af-123">Этот процесс устанавливает hello минимальные необходимые PHP необходимые расширения toouse PHP MySQL.</span><span class="sxs-lookup"><span data-stu-id="030af-123">This process installs hello minimum required PHP extensions needed toouse PHP with MySQL.</span></span> 

![Страница с паролем привилегированного пользователя MySQL][1]

## <a name="verify-installation-and-configuration"></a><span data-ttu-id="030af-125">Проверка установки и настройки.</span><span class="sxs-lookup"><span data-stu-id="030af-125">Verify installation and configuration</span></span>


### <a name="apache"></a><span data-ttu-id="030af-126">Apache</span><span class="sxs-lookup"><span data-stu-id="030af-126">Apache</span></span>

<span data-ttu-id="030af-127">Проверьте версию hello Apache hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="030af-127">Check hello version of Apache with hello following command:</span></span>
```bash
apache2 -v
```

<span data-ttu-id="030af-128">С помощью Apache установлены и порт 80 откройте tooyour виртуальной Машины, hello веб-сервер теперь может осуществляться из hello Интернета.</span><span class="sxs-lookup"><span data-stu-id="030af-128">With Apache installed, and port 80 open tooyour VM, hello web server can now be accessed from hello internet.</span></span> <span data-ttu-id="030af-129">hello tooview страница по умолчанию Ubuntu Apache2 откройте веб-браузер и введите hello общедоступный IP-адрес hello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="030af-129">tooview hello Apache2 Ubuntu Default Page, open a web browser, and enter hello public IP address of hello VM.</span></span> <span data-ttu-id="030af-130">Используйте общедоступный IP-адрес hello используется tooSSH toohello виртуальной Машины:</span><span class="sxs-lookup"><span data-stu-id="030af-130">Use hello public IP address you used tooSSH toohello VM:</span></span>

![Страница Apache по умолчанию][3]


### <a name="mysql"></a><span data-ttu-id="030af-132">MySQL</span><span class="sxs-lookup"><span data-stu-id="030af-132">MySQL</span></span>

<span data-ttu-id="030af-133">Уточните hello версия MySQL hello следующую команду (Обратите внимание, прописная hello `V` параметра):</span><span class="sxs-lookup"><span data-stu-id="030af-133">Check hello version of MySQL with hello following command (note hello capital `V` parameter):</span></span>

```bash
msql -V
```

<span data-ttu-id="030af-134">Рекомендуется запускать после установки безопасного hello toohelp сценария MySQL hello:</span><span class="sxs-lookup"><span data-stu-id="030af-134">We recommend running hello following script toohelp secure hello installation of MySQL:</span></span>

```bash
mysql_secure_installation
```

<span data-ttu-id="030af-135">Введите пароль MySQL корневой и настройте параметры безопасности hello для вашей среды.</span><span class="sxs-lookup"><span data-stu-id="030af-135">Enter your MySQL root password, and configure hello security settings for your environment.</span></span>

<span data-ttu-id="030af-136">Если вы хотите toocreate базы данных MySQL, добавлять пользователей или изменения параметров конфигурации, tooMySQL входа:</span><span class="sxs-lookup"><span data-stu-id="030af-136">If you want toocreate a MySQL database, add users, or change configuration settings, login tooMySQL:</span></span>

```bash
mysql -u root -p
```

<span data-ttu-id="030af-137">Закончив, выйдите из hello mysql строки, введя `\q`.</span><span class="sxs-lookup"><span data-stu-id="030af-137">When done, exit hello mysql prompt by typing `\q`.</span></span>

### <a name="php"></a><span data-ttu-id="030af-138">PHP</span><span class="sxs-lookup"><span data-stu-id="030af-138">PHP</span></span>

<span data-ttu-id="030af-139">Проверьте версию PHP hello hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="030af-139">Check hello version of PHP with hello following command:</span></span>

```bash
php -v
```

<span data-ttu-id="030af-140">Tootest дальнейшей, создайте быстрый tooview страницы сведения о PHP в браузере.</span><span class="sxs-lookup"><span data-stu-id="030af-140">If you want tootest further, create a quick PHP info page tooview in a browser.</span></span> <span data-ttu-id="030af-141">Hello, следующая команда создает страница сведений о hello PHP:</span><span class="sxs-lookup"><span data-stu-id="030af-141">hello following command creates hello PHP info page:</span></span>

```bash
sudo sh -c 'echo "<?php phpinfo(); ?>" > /var/www/html/info.php'
```

<span data-ttu-id="030af-142">Теперь можно проверить hello PHP info созданная страница.</span><span class="sxs-lookup"><span data-stu-id="030af-142">Now you can check hello PHP info page you created.</span></span> <span data-ttu-id="030af-143">Откройте браузер и перейдите в слишком`http://yourPublicIPAddress/info.php`.</span><span class="sxs-lookup"><span data-stu-id="030af-143">Open a browser and go too`http://yourPublicIPAddress/info.php`.</span></span> <span data-ttu-id="030af-144">Замените hello общедоступный IP-адрес виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="030af-144">Substitute hello public IP address of your VM.</span></span> <span data-ttu-id="030af-145">Он должен выглядеть примерно toothis изображения.</span><span class="sxs-lookup"><span data-stu-id="030af-145">It should look similar toothis image.</span></span>

![Страница сведений о PHP][2]

[!INCLUDE [virtual-machines-linux-tutorial-wordpress.md](../../../includes/virtual-machines-linux-tutorial-wordpress.md)]


## <a name="next-steps"></a><span data-ttu-id="030af-147">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="030af-147">Next steps</span></span>

<span data-ttu-id="030af-148">Из этого руководства вы узнали, как развернуть сервер LAMP в Azure.</span><span class="sxs-lookup"><span data-stu-id="030af-148">In this tutorial, you deployed a LAMP server in Azure.</span></span> <span data-ttu-id="030af-149">Вы научились выполнять следующие задачи:</span><span class="sxs-lookup"><span data-stu-id="030af-149">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="030af-150">Создание виртуальной машины Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="030af-150">Create an Ubuntu VM</span></span>
> * <span data-ttu-id="030af-151">Открытие порта 80 для веб-трафика</span><span class="sxs-lookup"><span data-stu-id="030af-151">Open port 80 for web traffic</span></span>
> * <span data-ttu-id="030af-152">Установка Apache, PHP и MySQL</span><span class="sxs-lookup"><span data-stu-id="030af-152">Install Apache, MySQL, and PHP</span></span>
> * <span data-ttu-id="030af-153">Проверка установки и настройки.</span><span class="sxs-lookup"><span data-stu-id="030af-153">Verify installation and configuration</span></span>
> * <span data-ttu-id="030af-154">Установка WordPress на сервере LAMP hello</span><span class="sxs-lookup"><span data-stu-id="030af-154">Install WordPress on hello LAMP server</span></span>

<span data-ttu-id="030af-155">Как переместить следующий учебник toolearn toohello toosecure веб-серверов с использованием сертификата SSL.</span><span class="sxs-lookup"><span data-stu-id="030af-155">Advance toohello next tutorial toolearn how toosecure web servers with SSL certificates.</span></span>

> [!div class="nextstepaction"]
> <span data-ttu-id="030af-156">[Secure a web server with SSL certificates on a Linux virtual machine in Azure](tutorial-secure-web-server.md) (Защита веб-сервера на виртуальной машине Linux в облаке Azure с помощью SSL-сертификата)</span><span class="sxs-lookup"><span data-stu-id="030af-156">[Secure web server with SSL](tutorial-secure-web-server.md)</span></span>

[1]: ./media/tutorial-lamp-stack/configmysqlpassword-small.png
[2]: ./media/tutorial-lamp-stack/phpsuccesspage.png
[3]: ./media/tutorial-lamp-stack/apachesuccesspage.png