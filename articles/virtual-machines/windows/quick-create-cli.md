---
title: "Быстрый запуск - aaaAzure создать CLI ВМ Windows | Документы Microsoft"
description: "Быстро Узнайте toocreate виртуальных машинах с hello Azure CLI."
services: virtual-machines-windows
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 05/11/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 029bdecec219b12b80b958ceeedda214f1b13149
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-windows-virtual-machine-with-hello-azure-cli"></a>Создание виртуальной машины Windows с hello Azure CLI

Hello Azure CLI — используется toocreate и управления ресурсами Azure hello командной строке или в сценариях. В этом руководстве рассматривается использование виртуальной машины с ОС Windows Server 2016 toodeploy hello Azure CLI. После завершения развертывания мы подключения toohello сервера и установить службы IIS.

Если у вас еще нет подписки Azure, [создайте бесплатную учетную запись Azure](https://azure.microsoft.com/free/?WT.mc_id=A261C142F), прежде чем начинать работу.


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

Если выбрать tooinstall и использовать hello CLI локально, краткого руководства требуется управлением hello Azure CLI версия 2.0.4 или более поздней версии. Запустите `az --version` версии toofind hello. Если требуется tooinstall или обновления, см. раздел [установить CLI Azure 2.0]( /cli/azure/install-azure-cli). 


## <a name="create-a-resource-group"></a>Создание группы ресурсов

Создайте группу ресурсов с помощью команды [az group create](/cli/azure/group#create). Группа ресурсов Azure является логическим контейнером, в котором происходит развертывание ресурсов Azure и управление ими. 

Hello следующий пример создает группу ресурсов с именем *myResourceGroup* в hello *eastus* расположение.

```azurecli-interactive 
az group create --name myResourceGroup --location eastus
```

## <a name="create-virtual-machine"></a>Создание виртуальной машины

Создайте виртуальную машину с помощью команды [az vm create](/cli/azure/vm#create). 

Hello следующий пример создает Виртуальную машину с именем *myVM*. В этом примере используется *azureuser* имени пользователя с правами администратора и *myPassword12* hello паролем. Обновите эти значения toosomething соответствующие tooyour среду. Эти значения необходимы при создании соединения с виртуальной машиной hello.

```azurecli-interactive 
az vm create --resource-group myResourceGroup --name myVM --image win2016datacenter --admin-username azureuser --admin-password myPassword12
```

При создании виртуальной Машины hello hello Azure CLI показано toohello аналогичные сведения, следующий пример. Запишите hello `publicIpAaddress`. Этот адрес будет hello используется tooaccess виртуальной Машины.

```azurecli-interactive 
{
  "fqdns": "",
  "id": "/subscriptions/d5b9d4b7-6fc1-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.Compute/virtualMachines/myVM",
  "location": "eastus",
  "macAddress": "00-0D-3A-23-9A-49",
  "powerState": "VM running",
  "privateIpAddress": "10.0.0.4",
  "publicIpAddress": "52.174.34.95",
  "resourceGroup": "myResourceGroup"
}
```

## <a name="open-port-80-for-web-traffic"></a>Открытие порта 80 для веб-трафика 

По умолчанию в tooWindows виртуальных машин, развернутых в Azure допускаются только подключений по протоколу RDP. Если эта виртуальная машина будет toobe веб-сервере, необходимо tooopen порту 80 из Интернета hello. Используйте hello [az виртуальной машины откройте порт-](/cli/azure/vm#open-port) команда tooopen hello требуемого порта.  
 
 ```azurecli-interactive  
az vm open-port --port 80 --resource-group myResourceGroup --name myVM
```


## <a name="connect-toovirtual-machine"></a>Подключиться к компьютеру toovirtual

Используйте hello следующая команда toocreate сеанс удаленного рабочего стола с виртуальной машиной hello. Замените hello IP-адрес hello общедоступный IP-адрес виртуальной машины. При появлении запроса введите hello учетные данные, используемые при создании виртуальной машины hello.

```bash 
mstsc /v:<Public IP Address>
```

## <a name="install-iis-using-powershell"></a>Установка IIS с помощью PowerShell

Теперь, когда вы вошли в toohello виртуальной Машине Azure, можно использовать одну строку PowerShell tooinstall IIS и включить hello локальном брандмауэре правило tooallow веб-трафика. Откройте командную строку PowerShell и выполните следующую команду hello:

```powershell
Install-WindowsFeature -name Web-Server -IncludeManagementTools
```

## <a name="view-hello-iis-welcome-page"></a>Представление hello страницу приветствия IIS

С установленными службами IIS и порт 80, теперь открыт на ВМ из hello Интернета можно использовать веб-браузере choice tooview hello по умолчанию службы IIS страницу приветствия. Быть убедиться, что toouse hello общедоступный IP-адрес, описанных выше toovisit страница по умолчанию hello. 

![Сайт IIS по умолчанию](./media/quick-create-powershell/default-iis-website.png) 

## <a name="clean-up-resources"></a>Очистка ресурсов

Если больше не нужны, можно использовать hello [удаление группы az](/cli/azure/group#delete) команд группы ресурсов tooremove hello, виртуальных Машин и все связанные ресурсы.

```azurecli-interactive 
az group delete --name myResourceGroup
```

## <a name="next-steps"></a>Дальнейшие действия

Из этого краткого руководства вы узнали о том, как развернуть простую виртуальную машину, о правилах группы безопасности сети и об установке веб-сервера. toolearn Дополнительные сведения о виртуальных машинах Azure, продолжить toohello учебника для виртуальных машин Windows.

> [!div class="nextstepaction"]
> [Создание виртуальных машин Windows и управление ими с помощью модуля Azure PowerShell](./tutorial-manage-vm.md)
