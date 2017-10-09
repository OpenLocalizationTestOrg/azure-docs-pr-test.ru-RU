---
title: "aaaDeploy LAMP на виртуальной машине Linux с hello Azure CLI 1.0 | Документы Microsoft"
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
ms.devlang: NA
ms.topic: article
ms.date: 2/21/2017
ms.author: juluk
ms.openlocfilehash: e78a82d388ce68710933b9b673aa1b2460bdbb14
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-lamp-stack-with-hello-azure-cli-10"></a>Развертывание стек LAMP с hello Azure CLI 1.0
В этой статье рассматриваются как toodeploy Apache веб-сервера, MySQL и PHP (стек LAMP hello) в Azure. Необходима учетная запись Azure ([получить бесплатную пробную версию](https://azure.microsoft.com/pricing/free-trial/)) и hello [Azure CLI](../../cli-install-nodejs.md) , [подключен tooyour учетная запись Azure](../../xplat-cli-connect.md).

## <a name="cli-versions-toocomplete-hello-task"></a>Задача hello toocomplete версии CLI
Можно выполнить с помощью одного из следующих версий CLI hello задачу hello.

- [Azure CLI 1.0] — нашей CLI для hello классический и ресурса управления развертывания моделей (в этой статье)
- [Azure CLI 2.0](create-lamp-stack.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) -нашей нового поколения CLI для модели развертывания hello ресурсов управления

```
# One command toocreate a resource group holding a VM with LAMP already on it
$ azure group create -n uniqueResourceGroup -l westus --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/lamp-app/azuredeploy.json
```

* Развертывание LAMP на существующей виртуальной машине

```
# Two commands: one updates packages, hello other installs Apache, MySQL, and PHP
user@ubuntu$ sudo apt-get update
user@ubuntu$ sudo apt-get install apache2 mysql-server php5 php5-mysql
```

## <a name="deploy-lamp-on-new-vm-walkthrough"></a>Пошаговое руководство по развертыванию LAMP на новой виртуальной машине
Сначала нужно создать [группы ресурсов](../../azure-resource-manager/resource-group-overview.md) , содержащий hello новой виртуальной Машины:

    $ azure group create uniqueResourceGroup westus
    info:    Executing command group create
    info:    Getting resource group uniqueResourceGroup
    info:    Creating resource group uniqueResourceGroup
    info:    Created resource group uniqueResourceGroup
    data:    Id:                  /subscriptions/########-####-####-####-############/resourceGroups/uniqueResourceGroup
    data:    Name:                uniqueResourceGroup
    data:    Location:            westus
    data:    Provisioning State:  Succeeded
    data:    Tags: null
    data:
    info:    group create command OK

toocreate Здравствуйте самой ВМ, уже написанный найден шаблон диспетчера ресурсов Azure можно использовать [здесь на GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/lamp-app).

    $ azure group deployment create --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/lamp-app/azuredeploy.json uniqueResourceGroup uniqueLampName

Вы увидите запрос на ввод дополнительных данных.

    info:    Executing command group deployment create
    info:    Supply values for hello following parameters
    storageAccountNamePrefix: lampprefix
    location: westus
    adminUsername: someUsername
    adminPassword: somePassword
    mySqlPassword: somePassword
    dnsLabelPrefix: azlamptest
    info:    Initializing template configurations and parameters
    info:    Creating a deployment
    info:    Created template deployment "uniqueLampName"
    info:    Waiting for deployment toocomplete
    data:    DeploymentName     : uniqueLampName
    data:    ResourceGroupName  : uniqueResourceGroup
    data:    ProvisioningState  : Succeeded
    data:    Timestamp          :
    data:    Mode               : Incremental
    data:    CorrelationId      : d51bbf3c-88f1-4cf3-a8b3-942c6925f381
    data:    TemplateLink       : https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/lamp-app/azuredeploy.json
    data:    ContentVersion     : 1.0.0.0
    data:    DeploymentParameters :
    data:    Name                      Type          Value
    data:    ------------------------  ------------  -----------
    data:    storageAccountNamePrefix  String        lampprefix
    data:    location                  String        westus
    data:    adminUsername             String        someUsername
    data:    adminPassword             SecureString  undefined
    data:    mySqlPassword             SecureString  undefined
    data:    dnsLabelPrefix            String        azlamptest
    data:    ubuntuOSVersion           String        14.04.2-LTS
    info:    group deployment create command OK

Вы создали виртуальную машину Linux с установленным стеком LAMP. При желании можно проверить hello установки посредством перехода вниз слишком[проверьте ЛАМПОЧКА успешно установлен](#verify-lamp-successfully-installed).

## <a name="deploy-lamp-on-existing-vm-walkthrough"></a>Пошаговое руководство по развертыванию LAMP на существующей виртуальной машине
Если требуется помощь для создания виртуальной Машины Linux можно head [здесь toolearn как toocreate ВМ Linux](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). Далее необходимо tooSSH в hello виртуальной Машины с Linux. Если вам нужна помощь с созданием SSH-ключ, можно head [здесь toolearn как toocreate ключа SSH в Linux или Mac](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
Если у вас же имеется ключ SSH, продолжайте процедуру и, используя командную строку, подключитесь по протоколу SSH к виртуальной машине Linux с помощью команды `ssh exampleUsername@exampleDNS`.

Теперь, когда вы работаете в ВМ Linux, мы пошаговую установку стек LAMP hello на основе Debian распределения. конкретные команды Hello могут отличаться в других дистрибутивах Linux.

#### <a name="installing-on-debianubuntu"></a>Установка на Debian или Ubuntu
Требуются следующие пакеты, установленные hello: `apache2`, `mysql-server`, `php5`, и `php5-mysql`. Их можно установить, перетащив вручную или воспользовавшись Tasksel. Ниже приведены указания для обоих способов.
Перед установкой требуется toodownload и обновление списков пакета.

    user@ubuntu$ sudo apt-get update

##### <a name="individual-packages"></a>Установка отдельных пакетов
Можно использовать apt-get.

    user@ubuntu$ sudo apt-get install apache2 mysql-server php5 php5-mysql

##### <a name="using-tasksel"></a>Установка с помощью Tasksel
В качестве альтернативы можно скачать Tasksel. Это инструмент Debian и Ubuntu, который устанавливает в систему несколько связанных пакетов в рамках одной скоординированной задачи.

    user@ubuntu$ sudo apt-get install tasksel
    user@ubuntu$ sudo tasksel install lamp-server

После выполнения любого из предыдущих параметров hello, будет иметь запрашиваемые tooinstall эти пакеты и другие зависимости. Нажмите «y», а затем toocontinue «Ввод» и выполните любые другие запросы tooset пароля администратора для MySQL. При этом устанавливаются hello минимальные необходимые PHP необходимые расширения toouse PHP с MySQL. 

![][1]

Выполните следующие команды toosee hello другие расширения PHP, которые доступны в виде пакетов.

    user@ubuntu$ apt-cache search php5


#### <a name="create-infophp-document"></a>Создание документа info.php
Теперь должен быть доступ toocheck версии Apache, PHP и MySQL имеется через командную строку hello, введя `apache2 -v`, `mysql -v`, или `php -v`.

Если вы бы как tootest Далее, можно создать быстрый tooview страницы сведения о PHP в браузере. Создайте файл в текстовом редакторе Nano с помощью следующей команды.

    user@ubuntu$ sudo nano /var/www/html/info.php

В текстовом редакторе GNU Nano hello добавьте hello следующие строки:

    <?php
    phpinfo();
    ?>

Сохраните и закройте редактор текста hello.

Перезапустите Apache с помощью следующей команды, чтобы все новые установленные компоненты вступили в действие.

    user@ubuntu$ sudo service apache2 restart

## <a name="verify-lamp-successfully-installed"></a>Проверка успешности установки LAMP
Теперь можно проверить hello PHP info созданная страница, открыв браузер и переходит в toohttp://youruniqueDNS/info.php. Он должен выглядеть примерно toothis изображения.

![][2]

Apache установки можно проверить, просмотрев hello страница по умолчанию Apache2 Ubuntu последовательно выбрав tooyou http://youruniqueDNS/. Должна отобразиться страница следующего вида.

![][3]

Поздравляем! Вы установили стек LAMP на виртуальную машину Azure.

## <a name="next-steps"></a>Дальнейшие действия
Проверьте hello документации Ubuntu стек LAMP hello.

* [https://help.ubuntu.com/community/ApacheMySQLPHP](https://help.ubuntu.com/community/ApacheMySQLPHP)

[1]: ./media/deploy-lamp-stack/configmysqlpassword-small.png
[2]: ./media/deploy-lamp-stack/phpsuccesspage.png
[3]: ./media/deploy-lamp-stack/apachesuccesspage.png