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
# <a name="install-a-lemp-web-server-on-an-azure-vm"></a>Установка веб-сервера LEMP на виртуальной машине Azure
В этой статье рассматриваются как toodeploy NGINX веб-сервера, MySQL и PHP (hello LEMP стека) на Виртуальной машине Ubuntu в Azure. стек LEMP Hello — альтернативный популярных toohello [стек LAMP](tutorial-lamp-stack.md), которое также можно установить в Azure. сервер LEMP toosee hello в действии, при необходимости можно установить и настроить сайт WordPress. Из этого руководства вы узнаете, как выполнить следующие задачи:

> [!div class="checklist"]
> * Создание Виртуальной машине Ubuntu (hello «L» hello LEMP стека)
> * Открытие порта 80 для веб-трафика
> * Установка NGINX, MySQL и PHP.
> * Проверка установки и настройки.
> * Установка WordPress на сервере LEMP hello


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

Если выбрать tooinstall и использовать hello CLI локально, упражнений этого учебника требуется, вы используете версию Azure CLI hello 2.0.4 или более поздней версии. Запустите `az --version` версии toofind hello. Если требуется tooinstall или обновления, см. раздел [установить CLI Azure 2.0]( /cli/azure/install-azure-cli). 

[!INCLUDE [virtual-machines-linux-tutorial-stack-intro.md](../../../includes/virtual-machines-linux-tutorial-stack-intro.md)]

## <a name="install-nginx-mysql-and-php"></a>Установка NGINX, MySQL и PHP.

Запустите следующие команды tooupdate Ubuntu пакета источники hello и установите NGINX, PHP и MySQL. 

```bash
sudo apt update && sudo apt install nginx mysql-server php-mysql php php-fpm
```

Вы являетесь запрашиваемые tooinstall hello пакетов и других зависимостей. При появлении запроса задайте пароль пользователя root для MySQL, а затем toocontinue [Enter]. Выполните оставшиеся приглашения hello. Этот процесс устанавливает hello минимальные необходимые PHP необходимые расширения toouse PHP MySQL. 

![Страница с паролем привилегированного пользователя MySQL][1]

## <a name="verify-installation-and-configuration"></a>Проверка установки и настройки.


### <a name="nginx"></a>NGINX

Проверьте версию hello NGINX hello следующую команду:
```bash
nginx -v
```

С NGINX установлены и порт 80 откройте tooyour виртуальных Машин, веб-сервер hello, теперь доступны из hello Интернета. tooview hello NGINX страницы приветствия, откройте браузер и введите hello общедоступный IP-адрес hello виртуальной Машины. Используйте общедоступный IP-адрес hello используется tooSSH toohello виртуальной Машины:

![Страница NGINX по умолчанию][3]


### <a name="mysql"></a>MySQL

Уточните hello версия MySQL hello следующую команду (Обратите внимание, прописная hello `V` параметра):

```bash
msql -V
```

Рекомендуется запускать после установки безопасного hello toohelp сценария MySQL hello:

```bash
mysql_secure_installation
```

Введите пароль MySQL корневой и настройте параметры безопасности hello для вашей среды.

Если вы хотите toocreate базы данных MySQL, добавлять пользователей или изменения параметров конфигурации, tooMySQL входа:

```bash
mysql -u root -p
```

Закончив, выйдите из hello mysql строки, введя `\q`.

### <a name="php"></a>PHP

Проверьте версию PHP hello hello следующую команду:

```bash
php -v
```

Настройте hello toouse NGINX диспетчер процессов FastCGI PHP (PHP-FPM). Выполните следующие команды tooback hello исходный сервер NGINX блокировать файл конфигурации, а затем измените hello исходный файл в редакторе, который предпочитаете hello.

```bash
sudo cp /etc/nginx/sites-available/default /etc/nginx/sites-available/default_backup

sudo sensible-editor /etc/nginx/sites-available/default
```

В редакторе hello, замените содержимое hello `/etc/nginx/sites-available/default` hello следующее. См. комментарии hello объяснение параметров hello. Замените hello общедоступный IP-адрес виртуальной Машины для *yourPublicIPAddress*и оставьте для оставшихся параметров hello. Затем сохраните файл hello.

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

Проверьте конфигурацию NGINX hello наличие синтаксических ошибок.

```bash
sudo nginx -t
```

Если имеет правильный синтаксис hello, перезапустите NGINX с hello следующую команду:

```bash
sudo service nginx restart
```

Tootest дальнейшей, создайте быстрый tooview страницы сведения о PHP в браузере. Hello, следующая команда создает страница сведений о hello PHP:

```bash
sudo sh -c 'echo "<?php phpinfo(); ?>" > /var/www/html/info.php'
```



Теперь можно проверить hello PHP info созданная страница. Откройте браузер и перейдите в слишком`http://yourPublicIPAddress/info.php`. Замените hello общедоступный IP-адрес виртуальной Машины. Он должен выглядеть примерно toothis изображения.

![Страница сведений о PHP][2]


[!INCLUDE [virtual-machines-linux-tutorial-wordpress.md](../../../includes/virtual-machines-linux-tutorial-wordpress.md)]

## <a name="next-steps"></a>Дальнейшие действия

Из этого руководства вы узнали, как развернуть сервер LEMP в Azure. Вы научились выполнять следующие задачи:

> [!div class="checklist"]
> * Создание виртуальной машины Ubuntu.
> * Открытие порта 80 для веб-трафика
> * Установка NGINX, MySQL и PHP.
> * Проверка установки и настройки.
> * Установка WordPress стеке LEMP hello

Как переместить следующий учебник toolearn toohello toosecure веб-серверов с использованием сертификата SSL.

> [!div class="nextstepaction"]
> [Secure a web server with SSL certificates on a Linux virtual machine in Azure](tutorial-secure-web-server.md) (Защита веб-сервера на виртуальной машине Linux в облаке Azure с помощью SSL-сертификата)

[1]: ./media/tutorial-lemp-stack/configmysqlpassword-small.png
[2]: ./media/tutorial-lemp-stack/phpsuccesspage.png
[3]: ./media/tutorial-lemp-stack/nginx.png
