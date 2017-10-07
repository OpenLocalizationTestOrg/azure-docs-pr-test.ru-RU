---
title: "Пример сценария CLI - aaaAzure создания виртуальной Машины Linux с NGINX | Документы Microsoft"
description: "Пример скрипта Azure CLI. Создание виртуальной машины Linux с помощью NGINX"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 02/27/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 9166ccfd4f2e6eea731a8dc6956575d9f8f85488
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-vm-with-nginx"></a>Создание виртуальной машины с помощью NGINX

Этот скрипт создает виртуальную машину Azure и использует виртуальную машину Azure настраиваемое расширение скриптов hello tooinstall NGINX. После выполнения сценария hello, можно получить доступ к демонстрационной веб-сайта на общедоступный IP-адрес hello hello виртуальной машины.

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>Пример скрипта

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-vm-nginx/create-vm-nginx.sh "Quick Create VM")]

## <a name="custom-script-extension"></a>Расширение пользовательских сценариев

расширение пользовательского скрипта Hello копирует этот скрипт на виртуальной машине hello. сценарий Hello запустите tooinstall и настроить веб-сервер NGINX. 

```bash
#!/bin/bash

# update package source
apt-get -y update

# install NGINX
apt-get -y install nginx
```

## <a name="clean-up-deployment"></a>Очистка развертывания 

Выполните следующие команды tooremove hello группы ресурсов, виртуальная машина и все связанные ресурсы hello.

```azurecli-interactive 
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a>Описание скрипта

Этот скрипт использует hello, следующие команды toocreate группу ресурсов виртуальной машины, и все связанные ресурсы. Каждая команда в таблице hello связывает toocommand документацию.

| Команда | Примечания |
|---|---|
| [az group create](https://docs.microsoft.com/cli/azure/group#create) | Создает группу ресурсов, в которой хранятся все ресурсы. |
| [az vm create](https://docs.microsoft.com/cli/azure/vm#create) | Создает виртуальную машину hello. Эта команда также указывает hello toobe образа на виртуальной машине используется и учетные данные администратора.  |
| [az vm open-port](https://docs.microsoft.com/cli/azure/network/nsg/rule#create) | Создает tooallow правило группы безопасности сети входящий трафик. В этом примере открывается порт 80 для трафика HTTP. |
| [azure vm extension set](https://docs.microsoft.com/cli/azure/vm/extension#set) | Добавляет и запускает tooa расширения виртуальной машины виртуальной Машины. В этом образце hello расширение пользовательского скрипта является используется tooinstall NGINX.|
| [az group delete](https://docs.microsoft.com/cli/azure/vm/extension#set) | Удаляет группу ресурсов со всеми вложенными ресурсами. |

## <a name="next-steps"></a>Дальнейшие действия

Дополнительные сведения о hello Azure CLI см. в разделе [документации Azure CLI](https://docs.microsoft.com/cli/azure/overview).

Примеры сценариев CLI дополнительную виртуальную машину можно найти в hello [документации виртуальной Машине Linux Azure](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
