---
title: "Пример сценария CLI - aaaAzure Создание ВМ с виртуального жесткого диска | Документы Microsoft"
description: "Пример скрипта Azure CLI. Создание виртуальной машины с помощью виртуального жесткого диска."
services: virtual-machines-linux
documentationcenter: virtual-machines
author: allclark
manager: douge
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 03/09/2017
ms.author: allclark
ms.custom: mvc
ms.openlocfilehash: ce39092697a51e4e8a8e59ba8eb919955f616458
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-vm-with-a-virtual-hard-disk"></a>Создание виртуальной машины с помощью виртуального жесткого диска

Этот пример создает виртуальную машину с помощью виртуального жесткого диска.
Он создает группу ресурсов, учетной записи хранилища и контейнер, а затем создает виртуальную Машину путем загрузки контейнера toohello hello виртуального жесткого диска.
Он заменяет hello ssh открытого ключа с помощью открытого ключа, чтобы получить доступ toohello виртуальной Машины.

Потребуется загрузочный виртуальный жесткий диск.
Можно загрузить VHD, который мы использовали hello https://azclisamples.blob.core.windows.net/vhds/sample.vhd или использовать собственный VHD-ФАЙЛ. ищет скрипт Hello `~/sample.vhd`.

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>Пример скрипта

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-vm-vhd/create-vm-vhd.sh "Create VM using a VHD")]

## <a name="clean-up-deployment"></a>Очистка развертывания 

Выполните следующие команды tooremove hello группы ресурсов, виртуальная машина и все связанные ресурсы hello.

```azurecli-interactive 
az group delete -n az-cli-vhd
```

## <a name="script-explanation"></a>Описание скрипта

Этот скрипт использует hello следующие команды toocreate группы ресурсов, виртуальная машина, группа доступности, балансировки нагрузки и все связанные ресурсы. Каждая команда в таблице hello связывает toocommand документацию.

| Команда | Примечания |
|---|---|
| [az group create](https://docs.microsoft.com/cli/azure/group#create) | Создает группу ресурсов, в которой хранятся все ресурсы. |
| [az storage account list](https://docs.microsoft.com/cli/azure/storage/account#list) | Выводит список учетных записей хранения. |
| [az storage account check-name](https://docs.microsoft.com/cli/azure/storage/account#check-name) | Проверяет допустимость имени учетной записи хранения и что она еще не существует. |
| [az storage account keys list](https://docs.microsoft.com/cli/azure/storage/account/keys#list) | Выводит список ключей для учетных записей хранения hello |
| [az storage blob exists](https://docs.microsoft.com/cli/azure/storage/blob#exists) | Проверяет, существует ли hello больших двоичных объектов |
| [az storage container create](https://docs.microsoft.com/cli/azure/storage/container#create) | Создает контейнер в учетной записи хранения. |
| [az storage blob upload](https://docs.microsoft.com/cli/azure/storage/blob#upload) | Создает большой двоичный объект в контейнере hello, отправка hello виртуального жесткого диска. |
| [az vm list](https://docs.microsoft.com/cli/azure/vm#list) | При использовании `--query` проверки, является ли имя виртуальной Машины hello используется. | 
| [az vm create](https://docs.microsoft.com/cli/azure/vm/availability-set#create) | Создает hello виртуальных машин. |
| [az vm access set-linux-user](https://docs.microsoft.com/cli/azure/vm/access#set-linux-user) | Сбрасывает hello SSH ключа toogive hello текущий пользователь доступ toohello виртуальной Машины. |
| [az vm list-ip-addresses](https://docs.microsoft.com/cli/azure/vm#list-ip-addresses) | Получает IP-адрес hello hello виртуальной Машины, который был создан. |

## <a name="next-steps"></a>Дальнейшие действия

Дополнительные сведения о hello Azure CLI см. в разделе [документации Azure CLI](https://docs.microsoft.com/cli/azure/overview).

Примеры сценариев CLI дополнительную виртуальную машину можно найти в hello [документации виртуальной Машине Linux Azure](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
