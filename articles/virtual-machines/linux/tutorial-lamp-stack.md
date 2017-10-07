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
# <a name="install-a-lamp-web-server-on-an-azure-vm"></a>Установка веб-сервера LAMP на виртуальной машине Azure
В этой статье рассматриваются как toodeploy Apache веб-сервера, MySQL и PHP (стек LAMP hello) на Виртуальной машине Ubuntu в Azure. При желании веб-сервер NGINX hello. в разделе hello [LEMP стека](tutorial-lemp-stack.md) учебника. сервер LAMP toosee hello в действии, при необходимости можно установить и настроить сайт WordPress. Из этого руководства вы узнаете, как выполнить следующие задачи:

> [!div class="checklist"]
> * Создание Виртуальной машине Ubuntu (hello «L» hello LAMP стека)
> * Открытие порта 80 для веб-трафика
> * Установка Apache, PHP и MySQL
> * Проверка установки и настройки.
> * Установка WordPress на сервере LAMP hello


Дополнительные сведения о стек LAMP hello, включая рекомендации для рабочей среды, в разделе hello [документации Ubuntu](https://help.ubuntu.com/community/ApacheMySQLPHP).

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

Если выбрать tooinstall и использовать hello CLI локально, упражнений этого учебника требуется, вы используете версию Azure CLI hello 2.0.4 или более поздней версии. Запустите `az --version` версии toofind hello. Если требуется tooinstall или обновления, см. раздел [установить CLI Azure 2.0]( /cli/azure/install-azure-cli). 

[!INCLUDE [virtual-machines-linux-tutorial-stack-intro.md](../../../includes/virtual-machines-linux-tutorial-stack-intro.md)]

## <a name="install-apache-mysql-and-php"></a>Установка Apache, PHP и MySQL

Запустите следующие команды tooupdate Ubuntu пакета источники hello и установите Apache, PHP и MySQL. Обратите внимание, hello крышки (^) в конце hello команда hello.


```bash
sudo apt update && sudo apt install lamp-server^
```



Вы являетесь запрашиваемые tooinstall hello пакетов и других зависимостей. При появлении запроса задайте пароль пользователя root для MySQL, а затем toocontinue [Enter]. Выполните оставшиеся приглашения hello. Этот процесс устанавливает hello минимальные необходимые PHP необходимые расширения toouse PHP MySQL. 

![Страница с паролем привилегированного пользователя MySQL][1]

## <a name="verify-installation-and-configuration"></a>Проверка установки и настройки.


### <a name="apache"></a>Apache

Проверьте версию hello Apache hello следующую команду:
```bash
apache2 -v
```

С помощью Apache установлены и порт 80 откройте tooyour виртуальной Машины, hello веб-сервер теперь может осуществляться из hello Интернета. hello tooview страница по умолчанию Ubuntu Apache2 откройте веб-браузер и введите hello общедоступный IP-адрес hello виртуальной Машины. Используйте общедоступный IP-адрес hello используется tooSSH toohello виртуальной Машины:

![Страница Apache по умолчанию][3]


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

Tootest дальнейшей, создайте быстрый tooview страницы сведения о PHP в браузере. Hello, следующая команда создает страница сведений о hello PHP:

```bash
sudo sh -c 'echo "<?php phpinfo(); ?>" > /var/www/html/info.php'
```

Теперь можно проверить hello PHP info созданная страница. Откройте браузер и перейдите в слишком`http://yourPublicIPAddress/info.php`. Замените hello общедоступный IP-адрес виртуальной Машины. Он должен выглядеть примерно toothis изображения.

![Страница сведений о PHP][2]

[!INCLUDE [virtual-machines-linux-tutorial-wordpress.md](../../../includes/virtual-machines-linux-tutorial-wordpress.md)]


## <a name="next-steps"></a>Дальнейшие действия

Из этого руководства вы узнали, как развернуть сервер LAMP в Azure. Вы научились выполнять следующие задачи:

> [!div class="checklist"]
> * Создание виртуальной машины Ubuntu.
> * Открытие порта 80 для веб-трафика
> * Установка Apache, PHP и MySQL
> * Проверка установки и настройки.
> * Установка WordPress на сервере LAMP hello

Как переместить следующий учебник toolearn toohello toosecure веб-серверов с использованием сертификата SSL.

> [!div class="nextstepaction"]
> [Secure a web server with SSL certificates on a Linux virtual machine in Azure](tutorial-secure-web-server.md) (Защита веб-сервера на виртуальной машине Linux в облаке Azure с помощью SSL-сертификата)

[1]: ./media/tutorial-lamp-stack/configmysqlpassword-small.png
[2]: ./media/tutorial-lamp-stack/phpsuccesspage.png
[3]: ./media/tutorial-lamp-stack/apachesuccesspage.png