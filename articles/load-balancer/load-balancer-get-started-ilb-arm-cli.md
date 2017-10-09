---
title: "Внутренний aaaCreate загрузить балансировки - Azure CLI | Документы Microsoft"
description: "Узнайте, как toocreate внутренняя Подсистема балансировки нагрузки с помощью hello Azure CLI в диспетчере ресурсов"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
tags: azure-resource-manager
ms.assetid: c7a24e92-b4da-43c0-90f2-841c1b7ce489
ms.service: load-balancer
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: kumud
ms.openlocfilehash: 3aea6fdb07600f0d661ec6b8ffc784b03380a127
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-internal-load-balancer-by-using-hello-azure-cli"></a>Создание внутренней подсистемы балансировки нагрузки с помощью hello Azure CLI

> [!div class="op_single_selector"]
> * [Портал Azure](../load-balancer/load-balancer-get-started-ilb-arm-portal.md)
> * [PowerShell](../load-balancer/load-balancer-get-started-ilb-arm-ps.md)
> * [Интерфейс командной строки Azure](../load-balancer/load-balancer-get-started-ilb-arm-cli.md)
> * [Шаблон](../load-balancer/load-balancer-get-started-ilb-arm-template.md)

[!INCLUDE [load-balancer-get-started-ilb-intro-include.md](../../includes/load-balancer-get-started-ilb-intro-include.md)]

> [!NOTE]
> В Azure предлагаются две модели развертывания для создания ресурсов и работы с ними: [модель Resource Manager и классическая модель](../azure-resource-manager/resource-manager-deployment-model.md).  В этой статье описывается использование модели развертывания диспетчера ресурсов hello, который рекомендуется в большинстве случаев новый вместо hello [классической модели развертывания](load-balancer-get-started-ilb-classic-cli.md).

[!INCLUDE [load-balancer-get-started-ilb-scenario-include.md](../../includes/load-balancer-get-started-ilb-scenario-include.md)]

## <a name="deploy-hello-solution-by-using-hello-azure-cli"></a>Развертывание решения hello с помощью hello Azure CLI

Привет, следующие шаги показывают, как toocreate из Интернета подсистемы балансировки нагрузки с помощью диспетчера ресурсов Azure с CLI. С помощью диспетчера ресурсов Azure каждый ресурс создается и настроить отдельно и затем поместить toocreate ресурса.

Требуется toocreate и настроить hello следующие объекты toodeploy подсистемы балансировки нагрузки:

* **Конфигурация интерфейсных IP-адресов**: содержит общедоступные IP-адреса для входящего сетевого трафика.
* **Пул адресов серверной части**: содержит сетевых интерфейсов (NIC), позволяющие hello виртуальные машины tooreceive сетевой трафик от подсистемы балансировки нагрузки hello
* **Правила балансировки нагрузки**: содержит правила, которые сопоставляют открытый порт hello tooport подсистемы балансировки нагрузки в пул адресов серверной части hello
* **Правила NAT для входящих подключений**: содержит правила, которые сопоставляют открытый порт на порт tooa подсистемы балансировки нагрузки hello для конкретной виртуальной машины в пул адресов серверной части hello
* **Проверяет**: содержит проверках работоспособности, доступности hello используется toocheck экземпляров виртуальных машин в пул адресов серверной части hello

Дополнительные сведения см. в статье [Поддержка диспетчера ресурсов Azure для подсистемы балансировки нагрузки](load-balancer-arm.md).

## <a name="set-up-cli-toouse-resource-manager"></a>Настройка toouse интерфейс командной строки диспетчера ресурсов

1. Если ранее не пользовались Azure CLI, см. раздел [установить и настроить hello Azure CLI](../cli-install-nodejs.md). Следуйте инструкциям hello toohello точку, где выбирается учетная запись Azure и подписки.
2. Запустите hello **azure конфигурации режима** команды режим Manager tooResource tooswitch, следующим образом:

    ```azurecli
    azure config mode arm
    ```

    Ожидаемые выходные данные:

        info:    New mode is arm

## <a name="create-an-internal-load-balancer-step-by-step"></a>Пошаговая инструкция по созданию внутреннего балансировщика нагрузки

1. Войдите в tooAzure.

    ```azurecli
    azure login
    ```

    При появлении запроса введите свои учетные данные Azure.

2. Изменение режима средства tooAzure диспетчера ресурсов для hello команды.

    ```azurecli
    azure config mode arm
    ```

## <a name="create-a-resource-group"></a>Создание группы ресурсов

Все ресурсы в Azure Resource Manager связаны с группой ресурсов. Если вы еще этого не сделали, создайте группу ресурсов.

```azurecli
azure group create <resource group name> <location>
```

## <a name="create-an-internal-load-balancer-set"></a>Создание набора внутренних балансировщиков нагрузки

1. Создание внутреннего балансировщика нагрузки

    В следующие сценарии hello группу ресурсов с именем nrprg создается в регионе Восток США.

    ```azurecli
    azure network lb create --name nrprg --location eastus
    ```

   > [!NOTE]
   > Все ресурсы для внутренних подсистем балансировки нагрузки, таких как виртуальные сети и подсети виртуальной сети должен быть в hello одну группу ресурсов и в hello же области.

2. Создание внешнего IP-адреса для hello внутренней подсистемы балансировки нагрузки.

    Hello IP-адреса, используемого должно быть в диапазоне подсети hello виртуальной сети.

    ```azurecli
    azure network lb frontend-ip create --resource-group nrprg --lb-name ilbset --name feilb --private-ip-address 10.0.0.7 --subnet-name nrpvnetsubnet --subnet-vnet-name nrpvnet
    ```

3. Создайте пул адресов серверной части hello.

    ```azurecli
    azure network lb address-pool create --resource-group nrprg --lb-name ilbset --name beilb
    ```

    После определения интерфейсного IP-адреса и пула внутренних адресов можно создать правила балансировщика нагрузки, правила NAT для входящего трафика и настроенные пробы работоспособности.

4. Создайте правило подсистемы балансировки нагрузки для hello внутренней подсистемы балансировки нагрузки.

    При выполнении предыдущего действия hello hello команда создает правило балансировки нагрузки для прослушивания tooport 1433 в пуле переднего плана hello и отправки балансировки нагрузки трафика toohello внутренней пул сетевых адресов, также использует порт 1433.

    ```azurecli
    azure network lb rule create --resource-group nrprg --lb-name ilbset --name ilbrule --protocol tcp --frontend-port 1433 --backend-port 1433 --frontend-ip-name feilb --backend-address-pool-name beilb
    ```

5. Создайте правило NAT для входящих подключений.

    Правила для входящих подключений NAT, используется toocreate конечные точки в подсистему балансировки нагрузки, go tooa конкретного экземпляра виртуальной машины. предыдущие шаги Hello создать два правила NAT для удаленного рабочего стола.

    ```azurecli
    azure network lb inbound-nat-rule create --resource-group nrprg --lb-name ilbset --name NATrule1 --protocol TCP --frontend-port 5432 --backend-port 3389

    azure network lb inbound-nat-rule create --resource-group nrprg --lb-name ilbset --name NATrule2 --protocol TCP --frontend-port 5433 --backend-port 3389
    ```

6. Создайте пробы работоспособности подсистемы балансировки нагрузки hello.

    Проверка работоспособности проверяет все toomake экземпляров виртуальной машины, убедиться, что они могут отправлять сетевой трафик. Hello экземпляр виртуальной машины с проверками сбоя проверки удаляется из hello балансировки нагрузки, пока не переходит в оперативный режим и проверку выборки определяет, что он исправен.

    ```azurecli
    azure network lb probe create --resource-group nrprg --lb-name ilbset --name ilbprobe --protocol tcp --interval 300 --count 4
    ```

    > [!NOTE]
    > Hello платформы Microsoft Azure использует статические публично маршрутизируемый IPv4-адрес для различных сценариев администрирования. Hello IP-адрес — 168.63.129.16. Не блокируйте этот IP-адрес брандмауэрами, поскольку это может привести к непредвиденному поведению.
    > С учетом tooAzure внутренней балансировки нагрузки, отслеживая проб из состояние работоспособности hello toodetermine подсистемы балансировки нагрузки hello для виртуальных машин в набор балансировки нагрузки используется этот IP-адрес. Если группа безопасности сети является используется toorestrict трафика tooAzure виртуальные машины в наборе внутренне балансировки нагрузки или примененных tooa подсети виртуальной сети, убедитесь, что правило сетевой безопасности добавлен tooallow трафика из 168.63.129.16.

## <a name="create-nics"></a>Создание сетевых адаптеров

Необходима toocreate сетевые адаптеры (или изменить существующие) и связать их tooNAT правила, правила подсистемы балансировки нагрузки и зонды.

1. Создание сетевого Адаптера с именем *быть балансировки нагрузки сетевого адаптера 1*и затем связать его с hello *rdp1* NAT правило и hello *beilb* пул адресов серверной части.

    ```azurecli
    azure network nic create --resource-group nrprg --name lb-nic1-be --subnet-name nrpvnetsubnet --subnet-vnet-name nrpvnet --lb-address-pool-ids "/subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/backendAddressPools/beilb" --lb-inbound-nat-rule-ids "/subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/inboundNatRules/rdp1" --location eastus
    ```

    Ожидаемые выходные данные:

        info:    Executing command network nic create
        + Looking up hello network interface "lb-nic1-be"
        + Looking up hello subnet "nrpvnetsubnet"
        + Creating network interface "lb-nic1-be"
        + Looking up hello network interface "lb-nic1-be"
        data:    Id                              : /subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/networkInterfaces/lb-nic1-be
        data:    Name                            : lb-nic1-be
        data:    Type                            : Microsoft.Network/networkInterfaces
        data:    Location                        : eastus
        data:    Provisioning state              : Succeeded
        data:    Enable IP forwarding            : false
        data:    IP configurations:
        data:      Name                          : NIC-config
        data:      Provisioning state            : Succeeded
        data:      Private IP address            : 10.0.0.4
        data:      Private IP Allocation Method  : Dynamic
        data:      Subnet                        : /subscriptions/####################################/resourceGroups/NRPRG/providers/Microsoft.Network/virtualNetworks/NRPVnet/subnets/NRPVnetSubnet
        data:      Load balancer backend address pools
        data:        Id                          : /subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/backendAddressPools/NRPbackendpool
        data:      Load balancer inbound NAT rules:
        data:        Id                          : /subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/inboundNatRules/rdp1
        data:
        info:    network nic create command OK

2. Создание сетевого Адаптера с именем *балансировки нагрузки nic2 быть*и затем связать его с hello *rdp2* NAT правило и hello *beilb* пул адресов серверной части.

    ```azurecli
    azure network nic create --resource-group nrprg --name lb-nic2-be --subnet-name nrpvnetsubnet --subnet-vnet-name nrpvnet --lb-address-pool-ids "/subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/backendAddressPools/beilb" --lb-inbound-nat-rule-ids "/subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/inboundNatRules/rdp2" --location eastus
    ```

3. Создание виртуальной машины с именем *DB1*и затем связать его с сетевого Адаптера с именем hello *быть балансировки нагрузки сетевого адаптера 1*. Вызывается учетной записи хранилища *web1nrp* создан, прежде чем hello, следующая команда запускает:

    ```azurecli
    azure vm create --resource--resource-grouproup nrprg --name DB1 --location eastus --vnet-name nrpvnet --vnet-subnet-name nrpvnetsubnet --nic-name lb-nic1-be --availset-name nrp-avset --storage-account-name web1nrp --os-type Windows --image-urn MicrosoftWindowsServer:WindowsServer:2012-R2-Datacenter:4.0.20150825
    ```
    > [!IMPORTANT]
    > Виртуальные машины в toobe необходимость подсистемы балансировки нагрузки, в hello одной группе доступности. Используйте `azure availset create` toocreate набор доступности.

4. Создание виртуальной машины (VM) с именем *DB2*и затем связать его с сетевого Адаптера с именем hello *балансировки нагрузки nic2 быть*. Вызывается учетной записи хранилища *web1nrp* была создана перед запуском hello следующую команду.

    ```azurecli
    azure vm create --resource--resource-grouproup nrprg --name DB2 --location eastus --vnet-name nrpvnet --vnet-subnet-name nrpvnetsubnet --nic-name lb-nic2-be --availset-name nrp-avset --storage-account-name web2nrp --os-type Windows --image-urn MicrosoftWindowsServer:WindowsServer:2012-R2-Datacenter:4.0.20150825
    ```

## <a name="delete-a-load-balancer"></a>Удаление балансировщика нагрузки

tooremove балансировщик нагрузки hello используйте следующую команду:

```azurecli
azure network lb delete --resource-group nrprg --name ilbset
```

## <a name="next-steps"></a>Дальнейшие действия

[Настройка режима распределения балансировщика нагрузки с помощью соответствия исходному IP-адресу](load-balancer-distribution-mode.md)

[Настройка параметров времени ожидания простоя TCP для подсистемы балансировки нагрузки](load-balancer-tcp-idle-timeout.md)

