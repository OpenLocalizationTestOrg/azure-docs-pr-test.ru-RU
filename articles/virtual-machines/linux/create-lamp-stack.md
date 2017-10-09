---
title: "aaaDeploy LAMP на виртуальной машине Linux в Azure | Документы Microsoft"
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
ms.devlang: azurecli
ms.topic: article
ms.date: 2/21/2017
ms.author: juluk
ms.openlocfilehash: 42d887bb9f78becc02505e336be25fdaaf78df70
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-lamp-stack-on-azure"></a>Развертывание стека LAMP в Azure
В этой статье рассматриваются как toodeploy Apache веб-сервера, MySQL и PHP (стек LAMP hello) в Azure. Необходима учетная запись Azure ([получить бесплатную пробную версию](https://azure.microsoft.com/pricing/free-trial/)) и hello [Azure CLI 2.0](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2). Можно также выполнить следующие действия с hello [Azure CLI 1.0](create-lamp-stack-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

## <a name="quick-command-summary"></a>Краткая сводка по командам

1. Сохранить и продолжить изменение hello [azuredeploy.parameters.json файл](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/lamp-app/azuredeploy.parameters.json) tooyour предпочтения на локальном компьютере.
2. Выполните следующие две команды toocreate hello группу ресурсов и затем развернуть шаблон.

```azurecli
az group create -l westus -n myResourceGroup
az group deployment create -g myResourceGroup \
    --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/lamp-app/azuredeploy.json \
    --parameters @filepathToParameters.json
```

### <a name="deploy-lamp-on-existing-vm"></a>Развертывание LAMP на существующей виртуальной машине
Hello следующие команды пакеты обновления, а затем устанавливает Apache, PHP и MySQL:

```bash
sudo apt-get update
sudo apt-get install apache2 mysql-server php5 php5-mysql
```

## <a name="deploy-lamp-on-new-vm-walkthrough"></a>Пошаговое руководство по развертыванию LAMP на новой виртуальной машине

1. Создание группы ресурсов с [Создание группы az](/cli/azure/group#create) toocontain hello новой виртуальной Машины:

```azurecli
az group create -l westus -n myResourceGroup
```
toocreate Здравствуйте самой ВМ, уже написанный найден шаблон диспетчера ресурсов Azure можно использовать [здесь на GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/lamp-app).

2. Сохранить hello [azuredeploy.parameters.json файл](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/lamp-app/azuredeploy.parameters.json) tooyour локального компьютера.
3. Изменить hello **azuredeploy.parameters.json** tooyour файл предпочитаемый входных данных.
4. Развертывание шаблона hello с [создание развертывания группы az] ссылается hello загрузили файл json:

```azurecli
az group deployment create -g myResourceGroup \
    --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/lamp-app/azuredeploy.json \
    --parameters @filepathToParameters.json
```

Hello вывода будет примерно toohello следующий пример:

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

Вы создали виртуальную машину Linux с установленным стеком LAMP. При желании можно проверить hello установки посредством перехода вниз слишком[проверьте ЛАМПОЧКА успешно установлен](#verify-lamp-successfully-installed).

## <a name="deploy-lamp-on-existing-vm-walkthrough"></a>Пошаговое руководство по развертыванию LAMP на существующей виртуальной машине
Если требуется помощь для создания виртуальной Машины Linux можно head [здесь toolearn как toocreate ВМ Linux](https://docs.microsoft.com/azure/virtual-machines/virtual-machines-linux-quick-create-cli). Далее необходимо tooSSH в hello виртуальной Машины с Linux. Если вам нужна помощь с созданием SSH-ключ, можно head [здесь toolearn как toocreate ключа SSH в Linux или Mac](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
Если у вас же имеется ключ SSH, продолжайте процедуру и, используя командную строку, подключитесь по протоколу SSH к виртуальной машине Linux с помощью команды `ssh azureuser@mypublicdns.westus.cloudapp.azure.com`.

Теперь, когда вы работаете в ВМ Linux, мы пошаговую установку стек LAMP hello на основе Debian распределения. конкретные команды Hello могут отличаться в других дистрибутивах Linux.

#### <a name="installing-on-debianubuntu"></a>Установка на Debian или Ubuntu
Требуются следующие пакеты, установленные hello: `apache2`, `mysql-server`, `php5`, и `php5-mysql`. Их можно установить, перетащив вручную или воспользовавшись Tasksel.
Перед установкой требуется toodownload и обновление списков пакета.

```bash
sudo apt-get update
```

##### <a name="individual-packages"></a>Установка отдельных пакетов
Можно использовать apt-get.

```bash
sudo apt-get install apache2 mysql-server php5 php5-mysql
```

##### <a name="using-tasksel"></a>Установка с помощью Tasksel
В качестве альтернативы можно скачать Tasksel. Это инструмент Debian и Ubuntu, который устанавливает в систему несколько связанных пакетов в рамках одной скоординированной задачи.

```bash
sudo apt-get install tasksel
sudo tasksel install lamp-server
```

После выполнения любого из предыдущих параметров hello, будет иметь запрашиваемые tooinstall эти пакеты и другие зависимости. tooset пароль администратора для MySQL, нажмите «y», а затем toocontinue «Ввод» и следуйте каких-либо других запросов. Этот процесс устанавливает hello минимальные необходимые PHP необходимые расширения toouse PHP MySQL. 

![][1]

Выполните следующие команды toosee hello другие расширения PHP, которые доступны в виде пакетов.

```bash
apt-cache search php5
```

#### <a name="create-infophp-document"></a>Создание документа info.php
Теперь должен быть доступ toocheck версии Apache, PHP и MySQL имеется через командную строку hello, введя `apache2 -v`, `mysql -v`, или `php -v`.

Если вы бы как tootest Далее, можно создать быстрый tooview страницы сведения о PHP в браузере. Создайте файл в текстовом редакторе Nano с помощью следующей команды.

```bash
sudo nano /var/www/html/info.php
```

В текстовом редакторе GNU Nano hello добавьте hello следующие строки:

```php
<?php
phpinfo();
?>
```

Сохраните и закройте редактор текста hello.

Перезапустите Apache с помощью следующей команды, чтобы все новые установленные компоненты вступили в действие.

```bash
sudo service apache2 restart
```

## <a name="verify-lamp-successfully-installed"></a>Проверка успешности установки LAMP
Теперь можно проверить hello PHP info созданная страница, открыв браузер и переходит в toohttp://youruniqueDNS/info.php. Он должен выглядеть примерно toothis изображения.

![][2]

Apache установки можно проверить, просмотрев hello страница по умолчанию Apache2 Ubuntu последовательно выбрав tooyou http://youruniqueDNS/. Hello вывода будет примерно toohello следующий пример:

![][3]

Поздравляем! Вы установили стек LAMP на виртуальную машину Azure.

## <a name="next-steps"></a>Дальнейшие действия
Проверьте hello документации Ubuntu стек LAMP hello.

* [https://help.ubuntu.com/community/ApacheMySQLPHP](https://help.ubuntu.com/community/ApacheMySQLPHP)

[1]: ./media/deploy-lamp-stack/configmysqlpassword-small.png
[2]: ./media/deploy-lamp-stack/phpsuccesspage.png
[3]: ./media/deploy-lamp-stack/apachesuccesspage.png
