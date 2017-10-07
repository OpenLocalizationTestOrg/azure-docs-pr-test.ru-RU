---
title: "Наборы масштабирования виртуальных машин для Linux в Azure aaaCreate | Документы Microsoft"
description: "Создание и развертывание высокодоступного приложения на виртуальных машинах Linux с помощью масштабируемого набора виртуальных машин."
services: virtual-machine-scale-sets
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: 
ms.assetid: 
ms.service: virtual-machine-scale-sets
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: azurecli
ms.topic: article
ms.date: 08/11/2017
ms.author: iainfou
ms.openlocfilehash: 00dd81043f9be46ef2dc6dfe97eefdb20944ee13
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-machine-scale-set-and-deploy-a-highly-available-app-on-linux"></a>Создание масштабируемого набора виртуальных машин и развертывание высокодоступного приложения на базе Linux
Набор масштабирования виртуальной машины дает toodeploy и управление набором идентичными, автоматического масштабирования виртуальных машин. Можно вручную масштабировать hello число виртуальных машин в наборе масштабирования hello, или определить tooautoscale правила на основе использования ЦП, объем памяти или сетевой трафик. В рамках этого руководства вы развернете масштабируемый набор виртуальных машин в Azure. Вы узнаете, как выполнять следующие задачи:

> [!div class="checklist"]
> * Использовать toocreate init облачные приложения tooscale
> * создавать масштабируемый набор виртуальных машин;
> * Увеличение или уменьшение числа hello экземпляров в наборе масштабирования
> * просматривать сведения о подключении для экземпляров масштабируемого набора;
> * использовать диски данных в масштабируемом наборе.


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

Если выбрать tooinstall и использовать hello CLI локально, упражнений этого учебника требуется, вы используете версию Azure CLI hello 2.0.4 или более поздней версии. Запустите `az --version` версии toofind hello. Если требуется tooinstall или обновления, см. раздел [установить CLI Azure 2.0]( /cli/azure/install-azure-cli). 

## <a name="scale-set-overview"></a>Обзор масштабируемого набора
Набор масштабирования виртуальной машины дает toodeploy и управление набором идентичными, автоматического масштабирования виртуальных машин. Масштаб задает hello используйте же компоненты, как вы узнали о в предыдущем учебнике hello слишком[создать высокодоступные виртуальные машины](tutorial-availability-sets.md). Виртуальные машины в масштабируемом наборе создаются в группе доступности и распределяются по логическим доменам сбоя и обновления.

Виртуальные машины создаются в масштабируемом наборе по мере необходимости. Определение правила toocontrol автомасштабирования как и когда добавляются или удаляются из hello масштабный набор виртуальных машин. Эти правила могут активироваться на основе метрик, таких как использование ЦП, использование памяти или сетевой трафик.

Масштаб задает поддержки вверх too1 000 виртуальных машин при использовании образа платформы Azure. Для рабочих нагрузок, вы можете слишком[создать образ виртуальной Машины](tutorial-custom-images.md). Можно создать too100 виртуальных машин в наборе, при использовании настраиваемого образа масштабирования.


## <a name="create-an-app-tooscale"></a>Создание приложения tooscale
Для использования в рабочей среде вы можете слишком[создать образ виртуальной Машины](tutorial-custom-images.md) , включающего приложения установлен и настроен. В этом учебнике позволяет настроить hello виртуальных машин на первой загрузки tooquickly разделе наборе в действии масштабирования.

В предыдущем учебнике вы узнали [как toocustomize виртуальной машины Linux при первой загрузке](tutorial-automate-vm-deployment.md) с инициализацией облака. Можно использовать hello же tooinstall файл конфигурации облачной init NGINX и выполнение простого приложения Node.js «Hello World». 

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


## <a name="create-a-scale-set"></a>Создание масштабируемого набора
Прежде чем создать масштабируемый набор, выполните команду [az group create](/cli/azure/group#create) для создания группы ресурсов. Hello следующий пример создает группу ресурсов с именем *myResourceGroupScaleSet* в hello *eastus* расположение:

```azurecli-interactive 
az group create --name myResourceGroupScaleSet --location eastus
```

Создайте масштабируемый набор виртуальных машин с помощью команды [az vmss create](/cli/azure/vmss#create). Hello следующий пример создает именованный наборе масштабирования *myScaleSet*, использующее hello облака init файл toocustomize hello виртуальной Машины и создает ключи SSH, если они не существуют:

```azurecli-interactive 
az vmss create \
  --resource-group myResourceGroupScaleSet \
  --name myScaleSet \
  --image UbuntuLTS \
  --upgrade-policy-mode automatic \
  --custom-data cloud-init.txt \
  --admin-username azureuser \
  --generate-ssh-keys      
```

Он занимает несколько минут toocreate и настроить все hello масштабирования набор ресурсов виртуальных машин. Существует фоновых задач, продолжить toorun после hello Azure CLI возвращает toohello строки. Он может быть другой несколько минут, чтобы получить доступ к приложение hello.


## <a name="allow-web-traffic"></a>Разрешение веб-трафика
Подсистема балансировки нагрузки была создана автоматически в составе набора масштабирования виртуальных машин hello. Подсистема балансировки нагрузки Hello распределяет трафик по набор определенных виртуальных машин с помощью правила подсистемы балансировки нагрузки. Дополнительные сведения об основных понятиях подсистемы балансировки нагрузки и конфигурации в следующем учебнике hello [как tooload сбалансировать виртуальных машин в Azure](tutorial-load-balancer.md).

tooallow трафика tooreach hello веб-приложения, создайте правило с [создать правило балансировки нагрузки сети az](/cli/azure/network/lb/rule#create). Hello следующий код создает правило с именем *myLoadBalancerRuleWeb*:

```azurecli-interactive 
az network lb rule create \
  --resource-group myResourceGroupScaleSet \
  --name myLoadBalancerRuleWeb \
  --lb-name myScaleSetLB \
  --backend-pool-name myScaleSetLBBEPool \
  --backend-port 80 \
  --frontend-ip-name loadBalancerFrontEnd \
  --frontend-port 80 \
  --protocol tcp
```

## <a name="test-your-app"></a>Тестирование приложения
toosee приложение Node.js в Интернете hello получить hello общедоступный IP-адрес балансировки нагрузки, с [az сети public-ip show](/cli/azure/network/public-ip#show). Hello следующий пример извлекает hello IP-адрес для *myScaleSetLBPublicIP* создана как часть набора масштабирования hello:

```azurecli-interactive 
az network public-ip show \
    --resource-group myResourceGroupScaleSet \
    --name myScaleSetLBPublicIP \
    --query [ipAddress] \
    --output tsv
```

Введите hello общедоступный IP-адрес в tooa веб-браузера. будут отображены приложение Hello, включая имя узла виртуальной Машины, hello нагрузки трафика балансировки распределенных для hello hello:

![Запуск приложения Node.js](./media/tutorial-create-vmss/running-nodejs-app.png)

набор в действии масштабирования hello toosee, вы может принудительное обновление вашего веб-браузера toosee hello нагрузку балансировки распределения трафика между все виртуальные машины hello, запускающий ваше приложение.


## <a name="management-tasks"></a>Задачи управления
На протяжении жизненного цикла hello набора масштабирования hello, может потребоваться toorun одну или несколько задач управления. Кроме того вы можете toocreate скрипты, автоматизирующие различные жизненного цикла задачи. Hello Azure CLI 2.0 предоставляет toodo быстро этих задач. Ниже приведено несколько распространенных задач.

### <a name="view-vms-in-a-scale-set"></a>Просмотр виртуальных машин в масштабируемом наборе
Список виртуальных машин, работающих в шкалу tooview набора, используйте [экземпляры списка в vmss az](/cli/azure/vmss#list-instances) следующим образом:

```azurecli-interactive 
az vmss list-instances \
  --resource-group myResourceGroupScaleSet \
  --name myScaleSet \
  --output table
```

Hello вывода будет примерно toohello следующий пример:

```azurecli-interactive 
  InstanceId  LatestModelApplied    Location    Name          ProvisioningState    ResourceGroup            VmId
------------  --------------------  ----------  ------------  -------------------  -----------------------  ------------------------------------
           1  True                  eastus      myScaleSet_1  Succeeded            MYRESOURCEGROUPSCALESET  c72ddc34-6c41-4a53-b89e-dd24f27b30ab
           3  True                  eastus      myScaleSet_3  Succeeded            MYRESOURCEGROUPSCALESET  44266022-65c3-49c5-92dd-88ffa64f95da
```


### <a name="increase-or-decrease-vm-instances"></a>Увеличение или уменьшение числа экземпляров виртуальной машины
число экземпляров hello toosee в настоящее время на шкале установки, используйте [az vmss Показать](/cli/azure/vmss#show) и запросов на *sku.capacity*:

```azurecli-interactive 
az vmss show \
    --resource-group myResourceGroupScaleSet \
    --name myScaleSet \
    --query [sku.capacity] \
    --output table
```

Можно затем вручную увеличить или уменьшить hello количество виртуальных машин в наборе с масштабирования hello [vmss шкалы az](/cli/azure/vmss#scale). Hello следующий пример задает hello число виртуальных машин в ваш набор слишком масштабирования*5*:

```azurecli-interactive 
az vmss scale \
    --resource-group myResourceGroupScaleSet \
    --name myScaleSet \
    --new-capacity 5
```

Правила автоматического масштабирования позволяют определить, как задать tooscale вверх или вниз hello число виртуальных машин в шкалу в toodemand ответа, такие как сетевой трафик или использования ЦП. В настоящее время эти правила невозможно задать с помощью Azure CLI 2.0. Используйте hello [портал Azure](https://portal.azure.com) tooconfigure автомасштабирования.

### <a name="get-connection-info"></a>Получение сведений о подключении
сведения о соединении tooobtain около hello в наборы масштабирования виртуальных машин, используйте [списка vmss az-экземпляр соединения info](/cli/azure/vmss#list-instance-connection-info). Эта команда выводит hello общедоступный IP-адрес и порт для каждой виртуальной Машины, который позволяет вам tooconnect с SSH:

```azurecli-interactive 
az vmss list-instance-connection-info \
    --resource-group myResourceGroupScaleSet \
    --name myScaleSet
```


## <a name="use-data-disks-with-scale-sets"></a>Использование дисков данных с масштабируемыми наборами
Можно создавать диски данных и использовать их с масштабируемыми наборами. В предыдущем учебнике вы узнали, каким образом слишком[дисков Azure управление](tutorial-manage-disks.md) hello, кривые рекомендации и производительности приложений для создания приложений на диски с данными, а не hello ОС диска.

### <a name="create-scale-set-with-data-disks"></a>Создание масштабируемого набора с дисками данных
toocreate шкалу установить и диски с данными, добавить hello `--data-disk-sizes-gb` toohello параметр [az vmss создать](/cli/azure/vmss#create) команды. Hello следующем примере создается набор масштабирования с *50*ГБ данных диски подключены tooeach экземпляр:

```azurecli-interactive 
az vmss create \
    --resource-group myResourceGroupScaleSet \
    --name myScaleSetDisks \
    --image UbuntuLTS \
    --upgrade-policy-mode automatic \
    --custom-data cloud-init.txt \
    --admin-username azureuser \
    --generate-ssh-keys \
    --data-disk-sizes-gb 50
```

Когда экземпляры удаляются из масштабируемого набора, также удаляются подключенные к ним диски данных.

### <a name="add-data-disks"></a>Добавление дисков данных
задать tooadd tooinstances диска данных в шкалу, используйте [присоединить диск vmss az](/cli/azure/vmss/disk#attach). Hello следующий пример добавляет *50*экземпляра tooeach ГБ диска:

```azurecli-interactive 
az vmss disk attach \
    --resource-group myResourceGroupScaleSet \
    --name myScaleSet \
    --size-gb 50 \
    --lun 2
```

### <a name="detach-data-disks"></a>Отключение дисков данных
задать tooremove tooinstances диска данных в шкалу, используйте [отсоединить диск vmss az](/cli/azure/vmss/disk#detach). Hello следующий пример удаляет hello диск данных в LUN *2* из каждого экземпляра:

```azurecli-interactive 
az vmss disk detach \
    --resource-group myResourceGroupScaleSet \
    --name myScaleSet \
    --lun 2
```


## <a name="next-steps"></a>Дальнейшие действия
В рамках этого руководства вы создали набор масштабирования виртуальных машин. Вы научились выполнять следующие задачи:

> [!div class="checklist"]
> * Использовать toocreate init облачные приложения tooscale
> * создавать масштабируемый набор виртуальных машин;
> * Увеличение или уменьшение числа hello экземпляров в наборе масштабирования
> * просматривать сведения о подключении для экземпляров масштабируемого набора;
> * использовать диски данных в масштабируемом наборе.

Дополнительные сведения о понятиях и принципах работы виртуальных машин балансировки нагрузки передвинута Далее учебника toolearn toohello.

> [!div class="nextstepaction"]
> [Балансировка нагрузки между виртуальными машинами](tutorial-load-balancer.md)