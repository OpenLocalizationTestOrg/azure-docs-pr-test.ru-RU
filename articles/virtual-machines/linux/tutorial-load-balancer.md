---
title: "aaaHow tooload сбалансировать виртуальных машин Linux в Azure | Документы Microsoft"
description: "Узнайте, как toouse hello Azure распределять балансировки toocreate высокой доступности и безопасности приложений в трех виртуальных машин Linux"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 08/11/2017
ms.author: iainfou
ms.custom: mvc
ms.openlocfilehash: f01752c3caec3489ee13e63000775769f3236e11
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooload-balance-linux-virtual-machines-in-azure-toocreate-a-highly-available-application"></a>Как tooload сбалансировать виртуальных машин Linux в Azure toocreate приложение с высокой доступностью
Балансировка нагрузки обеспечивает более высокий уровень доступности за счет распределения входящих запросов между несколькими виртуальными машинами. В этом учебнике вы узнаете о hello различных компонентов подсистемы балансировки нагрузки Azure hello, распределения трафика и обеспечения высокого уровня доступности. Вы узнаете, как выполнять следующие задачи:

> [!div class="checklist"]
> * Создание Azure Load Balancer
> * Создание пробы работоспособности балансировщика нагрузки
> * создавать правила трафика подсистемы балансировки нагрузки;
> * Использование облака init toocreate простое приложение Node.js
> * Создание виртуальных машин и присоединения tooa балансировки нагрузки
> * Просмотр балансировщика нагрузки в действии
> * добавлять и удалять виртуальные машины из подсистемы балансировки нагрузки.


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

Если выбрать tooinstall и использовать hello CLI локально, упражнений этого учебника требуется, вы используете версию Azure CLI hello 2.0.4 или более поздней версии. Запустите `az --version` версии toofind hello. Если требуется tooinstall или обновления, см. раздел [установить CLI Azure 2.0]( /cli/azure/install-azure-cli). 

## <a name="azure-load-balancer-overview"></a>Обзор Azure Load Balancer
Azure Load Balancer представляет собой балансировщик нагрузки уровня 4 (TCP, UDP), который обеспечивает высокий уровень доступности, распределяя входящий трафик между работоспособными виртуальными машинами. Отслеживает данный порт на каждой виртуальной Машине зонда работоспособности подсистемы балансировки нагрузки и только распределяет трафик tooan оперативной виртуальной Машины.

Вы определяете интерфейсную конфигурацию IP-адресов, содержащую один или несколько общедоступных IP-адресов. Эту интерфейсный IP-конфигурацию позволяет вашей toobe нагрузки балансировки и приложения доступны через Интернет hello. 

Виртуальные машины подключены tooa подсистемы балансировки нагрузки с помощью их виртуальный сетевой адаптер (NIC). toodistribute toohello трафика виртуальных машин, пул адресов серверной части содержит IP-адреса hello hello виртуальный (NIC) подключенных toohello подсистемы балансировки нагрузки.

toocontrol hello потока трафика, определить правила подсистемы балансировки нагрузки для определенных портов и протоколов, сопоставить виртуальные машины tooyour.

Если вы следовали предыдущим учебником hello слишком[создания набора масштабирования виртуальных машин](tutorial-create-vmss.md), подсистемы балансировки нагрузки будет создан. Все эти компоненты были настроены для вас в качестве части набора масштабирования hello.


## <a name="create-azure-load-balancer"></a>Создание Azure Load Balancer
В этом разделе описаны создание и настройка каждого компонента балансировки нагрузки hello. Прежде чем создать балансировщик нагрузки, выполните команду [az group create](/cli/azure/group#create) для создания группы ресурсов. Hello следующий пример создает группу ресурсов с именем *myResourceGroupLoadBalancer* в hello *eastus* расположение:

```azurecli-interactive 
az group create --name myResourceGroupLoadBalancer --location eastus
```

### <a name="create-a-public-ip-address"></a>Создание общедоступного IP-адреса
tooaccess приложения на Здравствуйте Интернет, необходимые для балансировки нагрузки hello общедоступный IP-адрес. Создайте общедоступный IP-адрес с помощью команды [az network public-ip create](/cli/azure/network/public-ip#create). Hello следующий пример создает общедоступный IP-адрес с именем *myPublicIP* в hello *myResourceGroupLoadBalancer* группа ресурсов:

```azurecli-interactive 
az network public-ip create \
    --resource-group myResourceGroupLoadBalancer \
    --name myPublicIP
```

### <a name="create-a-load-balancer"></a>Создание балансировщика нагрузки
Создайте балансировщик нагрузки с помощью команды [az network lb create](/cli/azure/network/lb#create). Hello следующий пример создает подсистемы балансировки нагрузки с именем *myLoadBalancer* и назначает hello *myPublicIP* адрес toohello интерфейсный IP-конфигурации:

```azurecli-interactive 
az network lb create \
    --resource-group myResourceGroupLoadBalancer \
    --name myLoadBalancer \
    --frontend-ip-name myFrontEndPool \
    --backend-pool-name myBackEndPool \
    --public-ip-address myPublicIP
```

### <a name="create-a-health-probe"></a>Создание пробы работоспособности
tooallow hello балансировки toomonitor hello состояние загрузки приложения, используйте проверки работоспособности. Проверка работоспособности Hello динамически добавляет или удаляет виртуальные машины из ротации подсистемы балансировки нагрузки hello, в зависимости от их проверки toohealth ответа. По умолчанию виртуальная машина удаляется из распределения подсистемы балансировки нагрузки hello после двух последовательных сбоев каждые 15 секунд. Пробу работоспособности можно создать на основе протокола или конкретной страницы проверки работоспособности приложения. 

Следующий пример Hello создает TCP-зонды. Вы также можете создать настраиваемую пробу HTTP для более детальных проверок. При использовании пользовательских проверку HTTP, необходимо создать страницу проверки работоспособности hello, таких как *healthcheck.js*. Hello пробы должен возвращать **HTTP 200 OK** ответа для узла hello tookeep подсистемы балансировки нагрузки hello в поворота.

использовать toocreate TCP-зонды работоспособности [зонд балансировки нагрузки сети az создать](/cli/azure/network/lb/probe#create). Hello следующий пример создает зонда работоспособности с именем *myHealthProbe*:

```azurecli-interactive 
az network lb probe create \
    --resource-group myResourceGroupLoadBalancer \
    --lb-name myLoadBalancer \
    --name myHealthProbe \
    --protocol tcp \
    --port 80
```

### <a name="create-a-load-balancer-rule"></a>Создание правила балансировщика нагрузки
Правило подсистемы балансировки нагрузки — toodefine используется как трафика является распределенной toohello виртуальных машин. Можно определить hello интерфейсный IP-конфигурацию для hello входящий трафик и hello серверной части IP пула tooreceive hello трафика, а также требуемых исходных hello и порт назначения. toomake убедиться, что только работоспособное ВМ получать трафик также определять toouse проверки работоспособности hello.

Создайте правило балансировщика нагрузки с помощью команды [az network lb rule create](/cli/azure/network/lb/rule#create). Hello следующий код создает правило с именем *myLoadBalancerRule*, использует hello *myHealthProbe* проверки работоспособности и сальдо трафик через порт *80*:

```azurecli-interactive 
az network lb rule create \
    --resource-group myResourceGroupLoadBalancer \
    --lb-name myLoadBalancer \
    --name myLoadBalancerRule \
    --protocol tcp \
    --frontend-port 80 \
    --backend-port 80 \
    --frontend-ip-name myFrontEndPool \
    --backend-pool-name myBackEndPool \
    --probe-name myHealthProbe
```


## <a name="configure-virtual-network"></a>Настройка виртуальной сети
Перед развертыванием некоторые виртуальные машины и можно проверить балансировки, создайте hello, поддерживающие ресурсы виртуальной сети. Дополнительные сведения о виртуальных сетях см. в разделе hello [управление виртуальными сетями Azure](tutorial-virtual-network.md) учебника.

### <a name="create-network-resources"></a>Создание сетевых ресурсов
Создайте виртуальную сеть с помощью команды [az network vnet create](/cli/azure/network/vnet#create). Hello следующий пример создает виртуальную сеть с именем *myVnet* с подсеть с именем *mySubnet*:

```azurecli-interactive 
az network vnet create \
    --resource-group myResourceGroupLoadBalancer \
    --name myVnet \
    --subnet-name mySubnet
```

использовать tooadd группы безопасности сети, [создать az сети nsg](/cli/azure/network/nsg#create). Hello следующий пример создает группу безопасности сети с именем *myNetworkSecurityGroup*:

```azurecli-interactive 
az network nsg create \
    --resource-group myResourceGroupLoadBalancer \
    --name myNetworkSecurityGroup
```

Создайте правило группы безопасности сети с помощью команды [az network nsg rule create](/cli/azure/network/nsg/rule#create). Hello следующий пример создает правило группы сетевой безопасности с именем *myNetworkSecurityGroupRule*:

```azurecli-interactive 
az network nsg rule create \
    --resource-group myResourceGroupLoadBalancer \
    --nsg-name myNetworkSecurityGroup \
    --name myNetworkSecurityGroupRule \
    --priority 1001 \
    --protocol tcp \
    --destination-port-range 80
```

Для создания виртуальных сетевых карт используется команда [az network nic create](/cli/azure/network/nic#create). Hello следующий пример создает три виртуальных сетевых адаптеров. (Один виртуальный сетевой Адаптер для каждой виртуальной Машины, создать приложение hello следующих шагов). Можно создать в любое время дополнительных виртуальных сетевых адаптеров и виртуальные машины и добавить их toohello балансировки нагрузки:

```bash
for i in `seq 1 3`; do
    az network nic create \
        --resource-group myResourceGroupLoadBalancer \
        --name myNic$i \
        --vnet-name myVnet \
        --subnet mySubnet \
        --network-security-group myNetworkSecurityGroup \
        --lb-name myLoadBalancer \
        --lb-address-pools myBackEndPool
done
```

## <a name="create-virtual-machines"></a>Создание виртуальных машин

### <a name="create-cloud-init-config"></a>Создание конфигурации cloud-init
В предыдущем учебнике на [как toocustomize виртуальной машины Linux при первой загрузке](tutorial-automate-vm-deployment.md), вы узнали, каким образом tooautomate настройки виртуальной Машины с инициализацией облака. Можно использовать hello же tooinstall файл конфигурации облачной init NGINX и выполнение простого приложения Node.js «Hello World».

В вашей текущей оболочке, создайте файл с именем *init.txt облака* и вставить hello следующая конфигурация. Например можно создайте файл hello в hello облака оболочки не на локальном компьютере. Введите `sensible-editor cloud-init.txt` toocreate hello файла и просмотреть список доступных редакторов. Убедитесь, что этот файл всей облачной init hello скопирован верно, особенно hello первой строки:

```yaml
#cloud-config
package_upgrade: true
packages:
  - nginx
  - nodejs
  - npm
write_files:
  - owner: www-data:www-data
  - path: /etc/nginx/sites-available/default
    content: |
      server {
        listen 80;
        location / {
          proxy_pass http://localhost:3000;
          proxy_http_version 1.1;
          proxy_set_header Upgrade $http_upgrade;
          proxy_set_header Connection keep-alive;
          proxy_set_header Host $host;
          proxy_cache_bypass $http_upgrade;
        }
      }
  - owner: azureuser:azureuser
  - path: /home/azureuser/myapp/index.js
    content: |
      var express = require('express')
      var app = express()
      var os = require('os');
      app.get('/', function (req, res) {
        res.send('Hello World from host ' + os.hostname() + '!')
      })
      app.listen(3000, function () {
        console.log('Hello world app listening on port 3000!')
      })
runcmd:
  - service nginx restart
  - cd "/home/azureuser/myapp"
  - npm init
  - npm install express -y
  - nodejs index.js
```

### <a name="create-virtual-machines"></a>Создание виртуальных машин
tooimprove hello высокий уровень доступности приложения, поместите виртуальные машины в группу доступности. Дополнительные сведения о группах доступности см. в разделе hello предыдущих [как виртуальные машины высокой надежности toocreate](tutorial-availability-sets.md) учебника.

Создайте группу доступности с помощью команды [az vm availability-set create](/cli/azure/vm/availability-set#create). Hello следующий пример создает именованный набор доступности *myAvailabilitySet*:

```azurecli-interactive 
az vm availability-set create \
    --resource-group myResourceGroupLoadBalancer \
    --name myAvailabilitySet
```

Теперь можно создавать виртуальные машины hello с [создания виртуальной машины az](/cli/azure/vm#create). Hello следующий пример создает три виртуальные машины и создает ключи SSH, если они еще не существует:

```bash
for i in `seq 1 3`; do
    az vm create \
        --resource-group myResourceGroupLoadBalancer \
        --name myVM$i \
        --availability-set myAvailabilitySet \
        --nics myNic$i \
        --image UbuntuLTS \
        --admin-username azureuser \
        --generate-ssh-keys \
        --custom-data cloud-init.txt \
        --no-wait
done
```

Существует фоновых задач, продолжить toorun после hello Azure CLI возвращает toohello строки. Hello `--no-wait` параметра не ожидать все hello toocomplete задачи. Он может быть другой несколько минут, чтобы получить доступ к приложение hello. Hello зонда работоспособности подсистемы балансировки нагрузки автоматически определяет, когда приложение hello выполняется на каждой виртуальной Машине. После запуска приложение hello правило подсистемы балансировки нагрузки hello запускает toodistribute трафика.


## <a name="test-load-balancer"></a>Проверка балансировщика нагрузки
Получить hello общедоступный IP-адрес балансировки нагрузки, с [az сети public-ip show](/cli/azure/network/public-ip#show). Hello следующий пример извлекает hello IP-адрес для *myPublicIP* созданную ранее:

```azurecli-interactive 
az network public-ip show \
    --resource-group myResourceGroupLoadBalancer \
    --name myPublicIP \
    --query [ipAddress] \
    --output tsv
```

После этого можно вводить hello общедоступный IP-адрес в tooa веб-браузере. Запомнить - занимает несколько минут hello hello виртуальные машины toobe готовности начала toothem toodistribute трафика подсистемы балансировки нагрузки hello. Откроется приложение Hello, включая имя узла виртуальной Машины hello hello балансировки нагрузки, hello распределенных tooas трафика в следующий пример hello:

![Запуск приложения Node.js](./media/tutorial-load-balancer/running-nodejs-app.png)

Подсистема балансировки нагрузки hello toosee распределять трафик между все три виртуальные машины, запускающий ваше приложение, вы может принудительно обновить веб-браузере.


## <a name="add-and-remove-vms"></a>Добавление и удаление виртуальных машин
Может потребоваться tooperform обслуживания на hello приложения, таких как установка обновления ОС работающих виртуальных машин. toodeal с приложением tooyour большего объема трафика, может потребоваться tooadd дополнительных ВМ. В этом разделе показано, как tooremove или добавить виртуальную Машину из балансировки нагрузки hello.

### <a name="remove-a-vm-from-hello-load-balancer"></a>Удалите виртуальную Машину из балансировки нагрузки hello
Можно удалить виртуальную Машину из hello серверный пул адресов с [удалить az сетевых ip конфигурация пул сетевых адресов-](/cli/azure/network/nic/ip-config/address-pool#remove). Следующий пример удаляет Hello hello виртуальный сетевой Адаптер для **myVM2** из *myLoadBalancer*:

```azurecli-interactive 
az network nic ip-config address-pool remove \
    --resource-group myResourceGroupLoadBalancer \
    --nic-name myNic2 \
    --ip-config-name ipConfig1 \
    --lb-name myLoadBalancer \
    --address-pool myBackEndPool 
```

подсистемы балансировки нагрузки hello toosee распределять трафик между hello остальные две виртуальные машины под управлением приложения вы можно принудительно обновить веб-браузере. Теперь можно выполнить обслуживание на hello виртуальной Машины, таких как установка обновлений операционной системы или перезагрузки виртуальной Машины.

### <a name="add-a-vm-toohello-load-balancer"></a>Добавляет подсистему балансировки нагрузки виртуальной Машины toohello
После выполнения обслуживания виртуальной Машины, или если требуется емкость tooexpand, можно добавить пул адресов серверной части ВМ toohello с [az сетевых ip конфигурация пул сетевых адресов-добавить](/cli/azure/network/nic/ip-config/address-pool#add). Hello следующий пример добавляет hello виртуальный сетевой Адаптер для **myVM2** слишком*myLoadBalancer*:

```azurecli-interactive 
az network nic ip-config address-pool add \
    --resource-group myResourceGroupLoadBalancer \
    --nic-name myNic2 \
    --ip-config-name ipConfig1 \
    --lb-name myLoadBalancer \
    --address-pool myBackEndPool
```


## <a name="next-steps"></a>Дальнейшие действия
В этом учебнике вы создается подсистемы балансировки нагрузки и прикрепляется tooit виртуальных машин. Вы научились выполнять следующие задачи:

> [!div class="checklist"]
> * Создание Azure Load Balancer
> * Создание пробы работоспособности балансировщика нагрузки
> * создавать правила трафика подсистемы балансировки нагрузки;
> * Использование облака init toocreate простое приложение Node.js
> * Создание виртуальных машин и присоединения tooa балансировки нагрузки
> * Просмотр балансировщика нагрузки в действии
> * добавлять и удалять виртуальные машины из подсистемы балансировки нагрузки.

Дополнительные сведения о виртуальной сети Azure компоненты приращения Далее учебника toolearn toohello.

> [!div class="nextstepaction"]
> [Управление виртуальными сетями Azure и виртуальными машинами Linux с помощью Azure CLI](tutorial-virtual-network.md)
