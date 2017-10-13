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
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/11/2017
---
# <a name="deploy-a-lamp-app-using-the-azure-customscript-extension-for-linux"></a>Развертывание приложения LAMP с помощью расширения Azure CustomScript для Linux#
> [!IMPORTANT] 
> В Azure предлагаются две модели развертывания для создания ресурсов и работы с ними: [модель диспетчера ресурсов и классическая модель](../../../resource-manager-deployment-model.md). В этой статье рассматривается использование классической модели развертывания. Для большинства новых развертываний Майкрософт рекомендует использовать модель диспетчера ресурсов. Сведения о развертывании стека LAMP с помощью модели Resource Manager см. [здесь](../tutorial-lamp-stack.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

Расширение Microsoft Azure CustomScript для Linux позволяет использовать для настройки виртуальных машин произвольный код, написанный на одном из языков сценариев, которые поддерживаются виртуальной машиной (например, Python и Bash). Это обеспечивает гибкую автоматизацию развертывания приложения на нескольких виртуальных машинах.

Расширение CustomScript можно развернуть с помощью портала Azure, Windows PowerShell или интерфейса командной строки Azure (Azure CLI).

В этой статье мы будем использовать интерфейс командной строки Azure для развертывания простого приложения LAMP на виртуальной машине под управлением Ubuntu, созданной с помощью классической модели развертывания.

## <a name="prerequisites"></a>Предварительные требования
Для этого примера создайте две виртуальные машины Azure под управлением Ubuntu 14.04 или более поздней версии. Присвойте им имена *script-vm* и *lamp-vm*. При создании виртуальных машин используйте уникальные имена. Одна из этих машин будет использоваться для выполнения команд интерфейса командной строки, а другая — для развертывания приложения LAMP.

Вам также потребуется учетная запись службы хранилища Azure и ключ доступа к ней (все это можно получить на портале Azure).

Дополнительные сведения о создании виртуальных машин Linux в Azure см. в статье [Создание настраиваемой виртуальной машины под управлением Linux](createportal.md).

Команды установки рассчитаны на Ubuntu, но могут быть адаптированы для установки любого поддерживаемого дистрибутива Linux.

На виртуальной машине script-vm должен быть установлен интерфейс CLI Azure. Кроме того, ее необходимо подключить к Azure. Дополнительную информацию см. в статье [Установка Azure CLI](../../../cli-install-nodejs.md).

## <a name="upload-a-script"></a>Загрузка сценария
Мы используем расширение CustomScript, чтобы выполнить сценарий на удаленной виртуальной машине для установки стека LAMP и создания PHP-страницы. Чтобы сценарий был доступен из любого расположения, мы передадим его как большой двоичный объект Azure.

### <a name="script-overview"></a>Общие сведения о сценариях
Сценарий в примере устанавливает стек LAMP в Ubuntu (включая настройку автоматической установки сервера MySQL), создает простой PHP-файл и запускает сервер Apache:

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

### <a name="upload-script"></a>Отправка скрипта
Сохраните сценарий как текстовый файл, например *install_lamp.sh*, и отправьте его в службу хранилища Azure. Это легко сделать с помощью интерфейса CLI Azure. Приведенный ниже пример передает файл в контейнер хранилища с именем scripts. Если контейнер не существует, необходимо сначала его создать.

    azure storage blob upload -a <yourStorageAccountName> -k <yourStorageKey> --container scripts ./install_lamp.sh

Также создайте JSON-файл, в котором будет указан способ скачивания сценария из службы хранилища Azure. Сохраните его как *public_config.json* (вместо mystorage укажите имя своей учетной записи хранения):

    {"fileUris":["https://mystorage.blob.core.windows.net/scripts/install_lamp.sh"], "commandToExecute":"sh install_lamp.sh" }


## <a name="deploy-the-extension"></a>Развертывание расширения
Теперь расширение CustomScript для Linux можно развернуть на удаленной виртуальной машине с помощью интерфейса командной строки Azure.

    azure vm extension set -c "./public_config.json" lamp-vm CustomScript Microsoft.Azure.Extensions 2.0

Предыдущая команда скачивает и выполняет сценарий *install_lamp.sh* на виртуальной машине с именем *lamp-vm*.

Так как приложение включает в себя веб-сервер, не забудьте открыть порт прослушивания HTTP на удаленной виртуальной машине с помощью следующей команды:

    azure vm endpoint create -n Apache -o tcp lamp-vm 80 80

## <a name="monitoring-and-troubleshooting"></a>Мониторинг и устранение неполадок
Можно проверить правильность выполнения пользовательского скрипта, просмотрите файл журнала на удаленной виртуальной машине. Добавьте SSH в *lamp-vm* и добавьте в файл журнала заключительный фрагмент с помощью следующей команды:

    cd /var/log/azure/customscript
    tail -f handler.log

После запуска расширения CustomScript вы сможете перейти к созданной PHP-странице и проверить данные. PHP-страница для примера в этой статье — *http://lamp-vm.cloudapp.net/phpinfo.php*.

## <a name="additional-resources"></a>Дополнительные ресурсы
С помощью описанных выше действий можно выполнять развертывание и более сложных приложений. В приведенном примере сценарий установки был сохранен в службе хранилища Azure как общедоступный большой двоичный объект. Чтобы обеспечить больший уровень защиты, сценарий установки можно сохранить как защищенный большой двоичный объект, для доступа к которому будет использоваться [подписанный URL-адрес](https://msdn.microsoft.com/library/azure/ee395415.aspx) (SAS).

Дополнительную информацию об интерфейсе командной строки Azure, Linux и расширении CustomScript см. в следующих статьях.

[Автоматизация задач настройки виртуальных машин под управлением Linux с помощью расширения CustomScript](https://azure.microsoft.com/blog/2014/08/20/automate-linux-vm-customization-tasks-using-customscript-extension/)

[Расширения Azure для Linux (GitHub)](https://github.com/Azure/azure-linux-extensions)