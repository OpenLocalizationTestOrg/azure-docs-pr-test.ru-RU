---
title: "Быстрый запуск - aaaAzure CLI создания виртуальной Машины | Документы Microsoft"
description: "Быстро Узнайте toocreate виртуальных машин с hello Azure CLI."
services: virtual-machines-linux
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: hero-article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 06/14/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 0d9c686e2f4c7339b29b8c43cd1dd9ee56d7dc6a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-linux-virtual-machine-with-hello-azure-cli"></a>Создание виртуальной машины Linux с hello Azure CLI

Hello Azure CLI — используется toocreate и управления ресурсами Azure hello командной строке или в сценариях. В этом руководстве рассматривается использование виртуальной машины, работающей Ubuntu server toodeploy hello Azure CLI. После развертывания сервера hello SSH-подключения создается и устанавливается веб-сервер NGINX.

Если у вас еще нет подписки Azure, [создайте бесплатную учетную запись Azure](https://azure.microsoft.com/free/?WT.mc_id=A261C142F), прежде чем начинать работу.

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

Если выбрать tooinstall и использовать hello CLI локально, краткого руководства требуется управлением hello Azure CLI версия 2.0.4 или более поздней версии. Запустите `az --version` версии toofind hello. Если требуется tooinstall или обновления, см. раздел [установить CLI Azure 2.0]( /cli/azure/install-azure-cli). 

## <a name="create-a-resource-group"></a>Создание группы ресурсов

Создание группы ресурсов с hello [Создание группы az](/cli/azure/group#create) команды. Группа ресурсов Azure является логическим контейнером, в котором происходит развертывание ресурсов Azure и управление ими. 

Hello следующий пример создает группу ресурсов с именем *myResourceGroup* в hello *eastus* расположение.

```azurecli-interactive 
az group create --name myResourceGroup --location eastus
```

## <a name="create-virtual-machine"></a>Создание виртуальной машины

Создайте виртуальную Машину с hello [создания виртуальной машины az](/cli/azure/vm#create) команды. 

Hello следующий пример создает Виртуальную машину с именем *myVM* и создает ключи SSH, если они еще не существуют в ключевое расположение по умолчанию. toouse конкретный набор ключей, используйте hello `--ssh-key-value` параметр.  

```azurecli-interactive 
az vm create --resource-group myResourceGroup --name myVM --image UbuntuLTS --generate-ssh-keys
```

При создании виртуальной Машины hello hello Azure CLI показано toohello аналогичные сведения, следующий пример. Запишите hello `publicIpAddress`. Этот адрес будет hello используется tooaccess виртуальной Машины.

```azurecli-interactive 
{
  "fqdns": "",
  "id": "/subscriptions/d5b9d4b7-6fc1-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.Compute/virtualMachines/myVM",
  "location": "eastus",
  "macAddress": "00-0D-3A-23-9A-49",
  "powerState": "VM running",
  "privateIpAddress": "10.0.0.4",
  "publicIpAddress": "40.68.254.142",
  "resourceGroup": "myResourceGroup"
}
```

## <a name="open-port-80-for-web-traffic"></a>Открытие порта 80 для веб-трафика 

По умолчанию виртуальные машины Linux, развернутые в Azure, поддерживают только SSH-подключения. Если эта виртуальная машина будет toobe веб-сервере, необходимо tooopen порту 80 из Интернета hello. Используйте hello [az виртуальной машины откройте порт-](/cli/azure/vm#open-port) команда tooopen hello требуемого порта.  
 
 ```azurecli-interactive 
az vm open-port --port 80 --resource-group myResourceGroup --name myVM
```

## <a name="ssh-into-your-vm"></a>SSH-подключение к виртуальной машине

Используйте hello следующая команда toocreate сеанс SSH с виртуальной машиной hello. Убедитесь, что tooreplace  *<publicIpAddress>*  с hello корректировать общедоступный IP-адрес виртуальной машины.  В примере выше виртуальная машина имела следующий IP-адрес: *40.68.254.142*.

```bash 
ssh <publicIpAddress>
```

## <a name="install-nginx"></a>Установка nginx

Используйте hello ниже bash источники пакетов tooupdate сценария и установить последнюю версию пакета NGINX hello. 

```bash 
#!/bin/bash

# update package source
apt-get -y update

# install NGINX
apt-get -y install nginx
```

## <a name="view-hello-nginx-welcome-page"></a>Просмотр hello NGINX начальной страницы

NGINX установлен и порт 80, теперь открыт на ВМ из hello Интернет - можно использовать веб-браузер на выбор tooview hello по умолчанию NGINX начальной страницы. Быть убедиться, что hello toouse *publicIpAddress* приведенной выше toovisit страница по умолчанию hello. 

![Сайт nginx по умолчанию](./media/quick-create-cli/nginx.png) 


## <a name="clean-up-resources"></a>Очистка ресурсов

Если больше не нужны, можно использовать hello [удаление группы az](/cli/azure/group#delete) команд группы ресурсов tooremove hello, виртуальных Машин и все связанные ресурсы.

```azurecli-interactive 
az group delete --name myResourceGroup
```

## <a name="next-steps"></a>Дальнейшие действия

Из этого краткого руководства вы узнали о том, как развернуть простую виртуальную машину, о правилах группы безопасности сети и об установке веб-сервера. toolearn Дополнительные сведения о виртуальных машинах Azure, продолжить toohello учебника для виртуальных машин Linux.


> [!div class="nextstepaction"]
> [Создание виртуальных машин Linux и управление ими с помощью Azure CLI](./tutorial-manage-vm.md)
