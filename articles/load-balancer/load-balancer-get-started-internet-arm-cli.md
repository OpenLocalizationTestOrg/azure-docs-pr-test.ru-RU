---
title: "Подсистема балансировки - нагрузки на aaaCreate из Интернета, Azure CLI | Документы Microsoft"
description: "Узнайте, как toocreate с выходом подсистемы балансировки нагрузки Интернета с помощью диспетчера ресурсов hello Azure CLI"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: a8bcdd88-f94c-4537-8143-c710eaa86818
ms.service: load-balancer
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: kumud
ms.openlocfilehash: cadb5edb3b4a4e2f0813109d027eaafdc7ef7303
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="creating-an-internet-load-balancer-using-hello-azure-cli"></a>Создание Интернет подсистемы балансировки нагрузки, с помощью hello Azure CLI

> [!div class="op_single_selector"]
> * [Портал](../load-balancer/load-balancer-get-started-internet-portal.md)
> * [PowerShell](../load-balancer/load-balancer-get-started-internet-arm-ps.md)
> * [Интерфейс командной строки Azure](../load-balancer/load-balancer-get-started-internet-arm-cli.md)
> * [Шаблон](../load-balancer/load-balancer-get-started-internet-arm-template.md)

[!INCLUDE [load-balancer-get-started-internet-intro-include.md](../../includes/load-balancer-get-started-internet-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

В этой статье рассматриваются hello модели развертывания диспетчера ресурсов. Вы также можете [Узнайте, как с помощью классического развертывания подсистемы балансировки нагрузки, toocreate из Интернета](load-balancer-get-started-internet-classic-portal.md)

[!INCLUDE [load-balancer-get-started-internet-scenario-include.md](../../includes/load-balancer-get-started-internet-scenario-include.md)]

## <a name="deploying-hello-solution-using-hello-azure-cli"></a>Развертывание решения hello, с помощью hello Azure CLI

Привет, следующие шаги показывают, как с помощью диспетчера ресурсов Azure с CLI подсистемы балансировки нагрузки, toocreate из Интернета. С помощью диспетчера ресурсов Azure создается и настраивается по отдельности каждого ресурса, затем объединить toocreate ресурса.

Необходимо создать и настроить hello следующие объекты toodeploy подсистемы балансировки нагрузки:

* Конфигурация интерфейсных IP-адресов. Содержит общедоступные IP-адреса для входящего сетевого трафика.
* Пул адресов серверной части - содержит сетевых интерфейсов (NIC) для hello виртуальные машины tooreceive сетевой трафик от подсистемы балансировки нагрузки hello.
* Правила балансировки нагрузки — содержит правила сопоставления открытый порт hello tooport подсистемы балансировки нагрузки в пул адресов серверной части hello.
* Правила NAT для входящих подключений — содержит правила, сопоставление порта открытый порт tooa подсистемы балансировки нагрузки hello для конкретной виртуальной машины в пул адресов серверной части hello.
* Проверяет — содержит доступность toocheck проверки, используемые работоспособности экземпляров виртуальных машин в пул адресов серверной части hello.

Дополнительные сведения см. в статье о [поддержке Azure Resource Manage для подсистемы балансировки нагрузки](load-balancer-arm.md).

## <a name="set-up-cli-toouse-resource-manager"></a>Настройка toouse интерфейс командной строки диспетчера ресурсов

1. Если ранее не пользовались Azure CLI, см. раздел [Установка и настройка hello Azure CLI](../cli-install-nodejs.md) и следуйте инструкциям hello toohello точку, где выбирается учетная запись Azure и подписки.
2. Запустите hello **azure конфигурации режима** tooswitch tooResource Manager режим команд, как показано ниже.

    ```azurecli
        azure config mode arm
    ```

    Ожидаемые выходные данные:

        info:    New mode is arm

## <a name="create-a-virtual-network-and-a-public-ip-address-for-hello-front-end-ip-pool"></a>Создайте виртуальную сеть и общедоступный IP-адрес пула IP-интерфейса hello

1. Создание виртуальной сети (VNet) с именем *NRPVnet* Восток США там hello группу ресурсов с именем *NRPRG*.

    ```azurecli
        azure network vnet create NRPRG NRPVnet eastUS -a 10.0.0.0/16
    ```

    Создайте подсеть *NRPVnetSubnet* с блоком CIDR 10.0.0.0/24 в виртуальной сети *NRPVnet*.

    ```azurecli
        azure network vnet subnet create NRPRG NRPVnet NRPVnetSubnet -a 10.0.0.0/24
    ```

2. Создать общедоступный IP-адрес с именем *NRPPublicIP* toobe, используемый пулом IP-интерфейса с именем DNS *loadbalancernrp.eastus.cloudapp.azure.com*. hello ниже используется тип статического выделения hello и тайм-аут простоя 4 минуты.

    ```azurecli
        azure network public-ip create -g NRPRG -n NRPPublicIP -l eastus -d loadbalancernrp -a static -i 4
    ```

   > [!IMPORTANT]
   > Hello балансировки нагрузки будет использовать метку hello общедоступный IP-адрес домена hello по полным доменным ИМЕНЕМ. Это изменение по сравнению с классической развертывания с использованием hello облачной службы как hello балансировки нагрузки полное доменное имя (FQDN).
   > В этом примере hello полное доменное имя — *loadbalancernrp.eastus.cloudapp.azure.com*.

## <a name="create-a-load-balancer"></a>Создание балансировщика нагрузки

Hello следующая команда создает подсистемы балансировки нагрузки с именем *NRPlb* в hello *NRPRG* группы ресурсов в hello *Восток США* расположение Azure.

    ```azurecli
    azure network lb create NRPRG NRPlb eastus
    ```

## <a name="create-a-front-end-ip-pool-and-a-backend-address-pool"></a>Создание пула интерфейсных IP-адресов и пула внутренних адресов
В этом примере демонстрируется toocreate hello переднего плана пула IP-адресов, получающий hello входящего сетевого трафика на hello подсистемы балансировки нагрузки и hello внутреннего пула IP-адресов, где переднего плана пула hello отправляет hello балансировки нагрузки сетевого трафика.

1. Создайте пул IP переднего плана, связывание hello общедоступный IP-адрес создан в предыдущем шаге hello и Подсистема балансировки нагрузки hello.

    ```azurecli
        azure network lb frontend-ip create nrpRG NRPlb NRPfrontendpool -i nrppublicip
    ```

2. Настройте пул адресов серверной части используется tooreceive входящего трафика из пула IP-интерфейса hello.

    ```azurecli
        azure network lb address-pool create NRPRG NRPlb NRPbackendpool
    ```

## <a name="create-lb-rules-nat-rules-and-probe"></a>Создание правил балансировки нагрузки, правил NAT и пробы

В этом примере создается hello следующих элементов.

* правило NAT для tootranslate весь входящий трафик на порт 21 tooport 22<sup>1</sup>
* правило NAT для tootranslate весь входящий трафик на порт 23 tooport 22
* toobalance правило балансировки нагрузки весь входящий трафик на порт 80 tooport 80 на hello адресов серверной части пула hello.
* состояние проверки правила toocheck hello работоспособности на страницу с именем *HealthProbe.aspx*.

<sup>1</sup> NAT правила, связанные tooa конкретного экземпляра виртуальной машины за подсистемой балансировки нагрузки hello. Hello сетевой трафик, поступающий на порт 21 отправляется tooa отдельную виртуальную машину на порт, связанный с этим правилом NAT 22. Для правила NAT необходимо указать протокол (UDP или TCP). Оба эти протокола не может быть назначен toohello тот же порт.

1. Создание правил NAT hello.

    ```azurecli
        azure network lb inbound-nat-rule create --resource-group nrprg --lb-name nrplb --name ssh1 --protocol tcp --frontend-port 21 --backend-port 22
        azure network lb inbound-nat-rule create --resource-group nrprg --lb-name nrplb --name ssh2 --protocol tcp --frontend-port 23 --backend-port 22
    ```

2. Создайте правило балансировщика нагрузки.

    ```azurecli
        azure network lb rule create --resource-group nrprg --lb-name nrplb --name lbrule --protocol tcp --frontend-port 80 --backend-port 80 --frontend-ip-name NRPfrontendpool --backend-address-pool-name NRPbackendpool
    ```

3. Создайте пробу работоспособности.

    ```azurecli
        azure network lb probe create --resource-group nrprg --lb-name nrplb --name healthprobe --protocol "http" --port 80 --path healthprobe.aspx --interval 15 --count 4
    ```

4. Проверьте параметры.

    ```azurecli
        azure network lb show nrprg nrplb
    ```

    Ожидаемые выходные данные:

        info:    Executing command network lb show
        + Looking up hello load balancer "nrplb"
        + Looking up hello public ip "NRPPublicIP"
        data:    Id                              : /subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb
        data:    Name                            : nrplb
        data:    Type                            : Microsoft.Network/loadBalancers
        data:    Location                        : eastus
        data:    Provisioning State              : Succeeded
        data:    Frontend IP configurations:
        data:      Name                          : NRPfrontendpool
        data:      Provisioning state            : Succeeded
        data:      Public IP address id          : /subscriptions/####################################/resourceGroups/NRPRG/providers/Microsoft.Network/publicIPAddresses/NRPPublicIP
        data:      Public IP allocation method   : Static
        data:      Public IP address             : 40.114.13.145
        data:
        data:    Backend address pools:
        data:      Name                          : NRPbackendpool
        data:      Provisioning state            : Succeeded
        data:
        data:    Load balancing rules:
        data:      Name                          : HTTP
        data:      Provisioning state            : Succeeded
        data:      Protocol                      : Tcp
        data:      Frontend port                 : 80
        data:      Backend port                  : 80
        data:      Enable floating IP            : false
        data:      Idle timeout in minutes       : 4
        data:      Frontend IP configuration     : /subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/frontendIPConfigurations/NRPfrontendpool
        data:      Backend address pool          : /subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/backendAddressPools/NRPbackendpool
        data:
        data:    Inbound NAT rules:
        data:      Name                          : ssh1
        data:      Provisioning state            : Succeeded
        data:      Protocol                      : Tcp
        data:      Frontend port                 : 21
        data:      Backend port                  : 22
        data:      Enable floating IP            : false
        data:      Idle timeout in minutes       : 4
        data:      Frontend IP configuration     : /subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/frontendIPConfigurations/NRPfrontendpool
        data:
        data:      Name                          : ssh2
        data:      Provisioning state            : Succeeded
        data:      Protocol                      : Tcp
        data:      Frontend port                 : 23
        data:      Backend port                  : 22
        data:      Enable floating IP            : false
        data:      Idle timeout in minutes       : 4
        data:      Frontend IP configuration     : /subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/frontendIPConfigurations/NRPfrontendpool
        data:
        data:    Probes:
        data:      Name                          : healthprobe
        data:      Provisioning state            : Succeeded
        data:      Protocol                      : Http
        data:      Port                          : 80
        data:      Interval in seconds           : 15
        data:      Number of probes              : 4
        data:
        info:    network lb show command OK

## <a name="create-nics"></a>Создание сетевых адаптеров

Необходима toocreate сетевые адаптеры (или изменить существующие) и связать их tooNAT правила, правила подсистемы балансировки нагрузки и зонды.

1. Создайте сетевую КАРТУ с именем *быть балансировки нагрузки сетевого адаптера 1*и связать его с hello *rdp1* NAT правило и hello *NRPbackendpool* пул адресов серверной части.

    ```azurecli
        azure network nic create --resource-group nrprg --name lb-nic1-be --subnet-name nrpvnetsubnet --subnet-vnet-name nrpvnet --lb-address-pool-ids "/subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/backendAddressPools/NRPbackendpool" --lb-inbound-nat-rule-ids "/subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/inboundNatRules/rdp1" eastus
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

2. Создайте сетевую КАРТУ с именем *балансировки нагрузки nic2 быть*и связать его с hello *rdp2* NAT правило и hello *NRPbackendpool* пул адресов серверной части.

    ```azurecli
        azure network nic create --resource-group nrprg --name lb-nic2-be --subnet-name nrpvnetsubnet --subnet-vnet-name nrpvnet --lb-address-pool-ids "/subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/backendAddressPools/NRPbackendpool" --lb-inbound-nat-rule-ids "/subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/inboundNatRules/rdp2" eastus
    ```

3. Создание виртуальной машины (VM) с именем *web1*и связать его с сетевого Адаптера с именем hello *быть балансировки нагрузки сетевого адаптера 1*. Вызывается учетной записи хранилища *web1nrp* была создана перед выполнением команды hello ниже.

    ```azurecli
        azure vm create --resource-group nrprg --name web1 --location eastus --vnet-name nrpvnet --vnet-subnet-name nrpvnetsubnet --nic-name lb-nic1-be --availset-name nrp-avset --storage-account-name web1nrp --os-type Windows --image-urn MicrosoftWindowsServer:WindowsServer:2012-R2-Datacenter:4.0.20150825
    ```

    > [!IMPORTANT]
    > Виртуальные машины в toobe необходимость подсистемы балансировки нагрузки, в hello одной группе доступности. Используйте `azure availset create` toocreate набор доступности.

    Hello выходные данные должны быть примерно toohello следующее:

        info:    Executing command vm create
        + Looking up hello VM "web1"
        Enter username: azureuser
        Enter password for azureuser: *********
        Confirm password: *********
        info:    Using hello VM Size "Standard_A1"
        info:    hello [OS, Data] Disk or image configuration requires storage account
        + Looking up hello storage account web1nrp
        + Looking up hello availability set "nrp-avset"
        info:    Found an Availability set "nrp-avset"
        + Looking up hello NIC "lb-nic1-be"
        info:    Found an existing NIC "lb-nic1-be"
        info:    Found an IP configuration with virtual network subnet id "/subscriptions/####################################/resourceGroups/NRPRG/providers/Microsoft.Network/virtualNetworks/NRPVnet/subnets/NRPVnetSubnet" in hello NIC "lb-nic1-be"
        info:    This is a NIC without publicIP configured
        + Creating VM "web1"
        info:    vm create command OK

    > [!NOTE]
    > Информационное сообщение Hello **это сетевой Адаптер без общедоступный IP-адрес настроен** ожидается с момента создания hello сетевой Адаптер для подключения tooInternet hello нагрузки балансировки общедоступный IP-адрес с помощью подсистемы балансировки нагрузки hello.

    С момента hello *быть балансировки нагрузки сетевого адаптера 1* сетевой Адаптер связан с hello *rdp1* правила NAT, можно подключить слишком*web1* с помощью протокола удаленного рабочего СТОЛА через порт 3441 в подсистеме балансировки нагрузки hello.

4. Создание виртуальной машины (VM) с именем *web2*и связать его с сетевого Адаптера с именем hello *балансировки нагрузки nic2 быть*. Вызывается учетной записи хранилища *web1nrp* была создана перед выполнением команды hello ниже.

    ```azurecli
        azure vm create --resource-group nrprg --name web2 --location eastus --vnet-name nrpvnet --vnet-subnet-name nrpvnetsubnet --nic-name lb-nic2-be --availset-name nrp-avset --storage-account-name web2nrp --os-type Windows --image-urn MicrosoftWindowsServer:WindowsServer:2012-R2-Datacenter:4.0.20150825
    ```

## <a name="update-an-existing-load-balancer"></a>Обновление существующего балансировщика нагрузки
Вы можете добавить правила, ссылающиеся на существующий балансировщик нагрузки. В следующем примере hello новое правило балансировки нагрузки добавляется существующей подсистемы балансировки нагрузки tooan **NRPlb**

```azurecli
azure network lb rule create --resource-group nrprg --lb-name nrplb --name lbrule2 --protocol tcp --frontend-port 8080 --backend-port 8051 --frontend-ip-name frontendnrppool --backend-address-pool-name NRPbackendpool
```

## <a name="delete-a-load-balancer"></a>Удаление балансировщика нагрузки
Используйте hello, следующая команда tooremove подсистемы балансировки нагрузки:

```azurecli
azure network lb delete --resource-group nrprg --name nrplb
```

## <a name="next-steps"></a>Дальнейшие действия
[Приступая к настройке внутренней подсистемы балансировки нагрузки](load-balancer-get-started-ilb-arm-cli.md)

[Настройка режима распределения подсистемы балансировки нагрузки](load-balancer-distribution-mode.md)

[Настройка параметров времени ожидания простоя TCP для подсистемы балансировки нагрузки](load-balancer-tcp-idle-timeout.md)
