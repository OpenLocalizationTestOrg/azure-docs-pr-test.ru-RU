---
title: "aaaAutomating развертывания приложений с помощью расширения виртуальных машин | Документы Microsoft"
description: "Руководство по .NET Core для виртуальных машин Azure"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 9fc8b1ba-60f5-410b-8190-9f1ff885e50e
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/12/2017
ms.author: nepeters
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 38a02a4271d6b9ba02a473a51794a7bd90ca3a35
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="application-deployment-with-azure-resource-manager-templates-for-linux-vms"></a>Развертывание приложений с использованием шаблонов Azure Resource Manager для виртуальных машин Linux

После выявления и преобразовать в шаблон развертывания все требования для Azure инфраструктурных развертывания приложения hello должен обращаться toobe. Развертывание приложения в данном ссылается двоичные файлы приложения hello tooinstalling на ресурсах Azure. Образец hello Music Store, .net Core, NGINX и руководителя, потребуется toobe устанавливается и настраивается на каждой виртуальной машине. предварительно создать Hello Music Store двоичные файлы должны toobe установлена на виртуальной машине hello и hello Music Store базы данных.

В этом документе описаны как расширения виртуальных машин можно автоматизировать приложения развертывание и настройку tooAzure виртуальных машин. Здесь будут описаны все зависимости и уникальные настройки. Для получения наилучших результатов hello предварительно разверните экземпляр tooyour решения hello подписки Azure, работают вместе с hello шаблона диспетчера ресурсов Azure. Полный шаблон Hello можно найти здесь — [музыка хранилища развертывания на Ubuntu](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-linux).

## <a name="configuration-script"></a>Скрипт настройки
Расширения виртуальных машин — это специализированные программы, применяемыми автоматизации конфигурации tooprovide виртуальных машин. Расширения используются в различных целях, например для автоматизации антивирусных программ, настройки ведения журнала и конфигурации Docker. Расширение пользовательского скрипта можно использовать toorun любой скрипт от виртуальной машины. Образец hello Music Store она до toohello расширение пользовательского скрипта tooconfigure hello Ubuntu виртуальных машин и установить приложение Music Store hello. 

Перед с подробным описанием объявлены как расширения виртуальных машин в шаблон диспетчера ресурсов Azure, изучите hello скрипт, который выполняется. Этот скрипт настраивает hello Ubuntu виртуальной машины toohost hello приложение Music Store. При запуске hello скрипт устанавливает все необходимое программное обеспечение, установить приложение магазина музыка hello из системы управления версиями и подготовки hello базы данных. 

toolearn Дополнительные сведения о размещении .net Core приложения в Linux, в разделе [публикации tooa Linux рабочей среде](https://docs.asp.net/en/latest/publishing/linuxproduction.html).

> Этот пример предназначен только для демонстрации.
> 
> 

```bash
#!/bin/bash

# install dotnet core
sudo sh -c 'echo "deb [arch=amd64] https://apt-mo.trafficmanager.net/repos/dotnet-release/ trusty main" > /etc/apt/sources.list.d/dotnetdev.list'
sudo apt-key adv --keyserver apt-mo.trafficmanager.net --recv-keys 417A0893
sudo apt-get update
sudo apt-get install -y dotnet-dev-1.0.0-preview2-003121

# download application
sudo wget https://raw.github.com/Microsoft/dotnet-core-sample-templates/master/dotnet-core-music-linux/music-app/music-store-azure-demo-pub.tar /
sudo mkdir /opt/music
sudo tar -xf music-store-azure-demo-pub.tar -C /opt/music

# install nginx, update config file
sudo apt-get install -y nginx
sudo service nginx start
sudo touch /etc/nginx/sites-available/default
sudo wget https://raw.githubusercontent.com/Microsoft/dotnet-core-sample-templates/master/dotnet-core-music-linux/music-app/nginx-config/default -O /etc/nginx/sites-available/default
sudo cp /opt/music/nginx-config/default /etc/nginx/sites-available/
sudo nginx -s reload

# update and secure music config file
sed -i "s/<replaceserver>/$1/g" /opt/music/config.json
sed -i "s/<replaceuser>/$2/g" /opt/music/config.json
sed -i "s/<replacepass>/$3/g" /opt/music/config.json
sudo chown $2 /opt/music/config.json
sudo chmod 0400 /opt/music/config.json

# config supervisor
sudo apt-get install -y supervisor
sudo touch /etc/supervisor/conf.d/music.conf
sudo wget https://raw.githubusercontent.com/Microsoft/dotnet-core-sample-templates/master/dotnet-core-music-linux/music-app/supervisor/music.conf -O /etc/supervisor/conf.d/music.conf
sudo service supervisor stop
sudo service supervisor start

# pre-create music store database
/usr/bin/dotnet /opt/music/MusicStore.dll &
```

## <a name="vm-script-extension"></a>Расширение скриптов виртуальной машины
Расширения ВМ может выполняться от виртуальной машины во время сборки, включая расширения ресурсов hello в hello шаблона диспетчера ресурсов Azure. Hello расширения можно добавить с помощью мастера добавления ресурсов Visual Studio hello, или путем вставки допустимых данных JSON в шаблоне hello. Hello расширение сценария ресурса вложен в hello ресурса виртуальной машины; Это можно заметить в следующий пример hello.

Выполните этот образец ссылку toosee hello JSON в шаблоне hello диспетчера ресурсов — [расширение ВМ сценария](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L359). 

Обратите внимание на hello ниже JSON, hello сценарий хранится в GitHub. Этот скрипт также может храниться в хранилище BLOB-объектов Azure. Кроме того шаблоны Azure Resource Manager разрешить выполнения строку hello сценария tooconstructed таким образом, что значения параметров шаблона, которая может использоваться в качестве параметров для выполнения скриптов. В этом случае данные предоставляются в развертывание шаблонов hello, и эти значения можно затем использовать при выполнении сценария hello.

```json
{
  "apiVersion": "2015-06-15",
  "type": "extensions",
  "name": "config-app",
  "location": "[resourceGroup().location]",
  "dependsOn": [
    "[concat('Microsoft.Compute/virtualMachines/', concat(variables('vmName'),copyindex()))]"
  ],
  "tags": {
    "displayName": "config-app"
  },
  "properties": {
    "publisher": "Microsoft.Azure.Extensions",
    "type": "CustomScript",
    "typeHandlerVersion": "2.0",
    "autoUpgradeMinorVersion": true,
    "settings": {
      "fileUris": [
        "https://raw.githubusercontent.com/Microsoft/dotnet-core-sample-templates/master/dotnet-core-music-linux/scripts/config-music.sh"
      ]
    },
    "protectedSettings": {
      "commandToExecute": "[concat('sudo sh config-music.sh ',variables('musicStoreSqlName'), ' ', parameters('adminUsername'), ' ', parameters('sqlAdminPassword'))]"
    }
  }
}
```

Дополнительные сведения об использовании расширения пользовательского скрипта hello см. в разделе [пользовательских расширений сценария с помощью шаблонов диспетчера ресурсов](extensions-customscript.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

## <a name="next-step"></a>Дальнейшее действие
<hr>

[Ознакомьтесь с другими шаблонами Azure Resource Manager](https://github.com/Azure/azure-quickstart-templates)

