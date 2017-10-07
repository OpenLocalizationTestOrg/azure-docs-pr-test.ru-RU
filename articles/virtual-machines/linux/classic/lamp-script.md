---
title: "Расширение CustomScript на виртуальной Машине Linux hello aaaUse | Документы Microsoft"
description: "Узнайте, как toodeploy расширения приложений на виртуальных машин Linux в Azure toouse hello CustomScript созданной hello классической модели развертывания."
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
ms.openlocfilehash: 864a586e70093eefbabc065a3c05e1cf9e315704
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-lamp-app-using-hello-azure-customscript-extension-for-linux"></a>Развертывание приложения ИНДИКАТОРА с помощью hello расширение CustomScript Azure для Linux
> [!IMPORTANT] 
> В Azure предлагаются две модели развертывания для создания ресурсов и работы с ними: [модель диспетчера ресурсов и классическая модель](../../../resource-manager-deployment-model.md). В этой статье описан с помощью hello классической модели развертывания. Корпорация Майкрософт рекомендует наиболее новые развертывания модели hello диспетчера ресурсов. Сведения о развертывании стек LAMP, с помощью модели hello диспетчера ресурсов см. в разделе [здесь](../tutorial-lamp-stack.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

Hello расширения CustomScript Microsoft Azure для Linux обеспечивает toocustomize способом виртуальных машин (ВМ), запустив произвольный код, написанный на любом языке сценариев, поддерживаемых hello виртуальной Машины (например, Python и Bash). Это обеспечивает tooautomate очень гибкий способ машины toomultiple развертывания приложения.

Hello расширение CustomScript можно развернуть с помощью hello портал Azure, Windows PowerShell или hello Azure командной строки (CLI Azure).

В этой статье мы будем использовать toodeploy hello Azure CLI простого приложения tooan LAMP Ubuntu ВМ создан с помощью hello классической модели развертывания.

## <a name="prerequisites"></a>Предварительные требования
Для этого примера создайте две виртуальные машины Azure под управлением Ubuntu 14.04 или более поздней версии. Hello виртуальных машин, называются *ВМ сценарий* и *lamp ВМ*. Используйте уникальные имена для создания виртуальных машин hello. Он используется toorun команды CLI hello и одно является LAMP приложение используется toodeploy hello.

Необходимо также учетную запись хранилища Azure и ключа tooaccess ИТ (это можно получить из hello портал Azure).

Если вам нужна помощь при создании виртуальных машин Linux в Azure см. слишком[создать виртуальную машину под управлением Linux](createportal.md).

команды установки Hello предполагают Ubuntu, но вы можете адаптировать hello установки для любой поддерживаемый дистрибутив Linux.

Hello скрипт виртуальная машина виртуальная машина должна toohave установке Azure CLI, с tooAzure рабочего соединения. См. справку слишком[Установка и настройка интерфейса командной строки Azure hello](../../../cli-install-nodejs.md).

## <a name="upload-a-script"></a>Загрузка сценария
Используется hello расширение CustomScript toorun сценарий в стеке LAMP tooinstall hello удаленной виртуальной Машины и создание страницы PHP. В сценарии hello tooaccess заказа из любого места будет передать как BLOB-объекта Azure.

### <a name="script-overview"></a>Общие сведения о сценариях
Ниже приведен пример сценария Hello устанавливает tooUbuntu стек LAMP (включая настройку автоматической установкой MySQL), записывает простой файл PHP и запускает Apache.

    #!/bin/bash
    # set up a silent install of MySQL
    dbpass="mySQLPassw0rd"

    export DEBIAN_FRONTEND=noninteractive
    echo mysql-server-5.6 mysql-server/root_password password $dbpass | debconf-set-selections
    echo mysql-server-5.6 mysql-server/root_password_again password $dbpass | debconf-set-selections

    # install hello LAMP stack
    apt-get -y install apache2 mysql-server php5 php5-mysql  

    # write some PHP
    echo \<center\>\<h1\>My Demo App\</h1\>\<br/\>\</center\> > /var/www/html/phpinfo.php
    echo \<\?php phpinfo\(\)\; \?\> >> /var/www/html/phpinfo.php

    # restart Apache
    apachectl restart

### <a name="upload-script"></a>Отправка скрипта
Сохраните скрипт hello как текстовый файл, например *install_lamp.sh*, а затем передать его tooAzure хранилища. Это легко сделать с помощью интерфейса CLI Azure. Hello следующий пример передает hello файла tooa хранилища контейнера с именем «скрипты». Если контейнер hello не существует, вам потребуется toocreate его первого.

    azure storage blob upload -a <yourStorageAccountName> -k <yourStorageKey> --container scripts ./install_lamp.sh

Также можно создайте файл JSON, описывающий, как toodownload hello скрипта из хранилища Azure. Сохраните его в виде *public_config.json* (замена «mystorage» с именем hello учетной записи):

    {"fileUris":["https://mystorage.blob.core.windows.net/scripts/install_lamp.sh"], "commandToExecute":"sh install_lamp.sh" }


## <a name="deploy-hello-extension"></a>Развертывание модуля hello
Теперь вы можете использовать hello Далее команда toodeploy hello расширения CustomScript Linux toohello удаленной виртуальной Машины с помощью hello Azure CLI.

    azure vm extension set -c "./public_config.json" lamp-vm CustomScript Microsoft.Azure.Extensions 2.0

Предыдущая команда Hello загружает и запускает hello *install_lamp.sh* скриптов на ВМ называется hello *lamp ВМ*.

Поскольку приложение hello включает веб-сервера, помните, порт прослушивания tooopen HTTP на hello удаленной виртуальной Машины с помощью следующей команды hello.

    azure vm endpoint create -n Apache -o tcp lamp-vm 80 80

## <a name="monitoring-and-troubleshooting"></a>Мониторинг и устранение неполадок
Можно проверить на насколько хорошо выполняется hello пользовательского скрипта, просмотрев файл журнала hello hello удаленной виртуальной Машины. SSH слишком*lamp ВМ* и файл hello по заключительного фрагмента журнала с помощью следующей команды hello.

    cd /var/log/azure/customscript
    tail -f handler.log

После запуска hello расширение CustomScript можно просматривать сведения созданная страница toohello PHP. Страница приветствия PHP hello в этой статье приведен *http://lamp-vm.cloudapp.net/phpinfo.php*.

## <a name="additional-resources"></a>Дополнительные ресурсы
Можно использовать hello же toodeploy основные шаги более сложных приложений. В этом примере сценария установки hello была сохранена как общедоступный BLOB-объект в хранилище Azure. Более безопасный вариант будет сценарий установки hello toostore как безопасный большой двоичный объект с [подписи безопасного доступа](https://msdn.microsoft.com/library/azure/ee395415.aspx) (SAS).

Далее перечислены дополнительные ресурсы для Azure CLI, Linux и hello расширение CustomScript.

[Автоматизация задач настройки виртуальных машин под управлением Linux с помощью расширения CustomScript](https://azure.microsoft.com/blog/2014/08/20/automate-linux-vm-customization-tasks-using-customscript-extension/)

[Расширения Azure для Linux (GitHub)](https://github.com/Azure/azure-linux-extensions)