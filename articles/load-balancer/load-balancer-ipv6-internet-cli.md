---
title: "Подсистема балансировки нагрузки aaaCreate с выходом в Интернет с IPv6 - Azure CLI | Документы Microsoft"
description: "Узнайте, как toocreate Интернета с выходом подсистемы балансировки нагрузки с IPv6 с помощью диспетчера ресурсов Azure hello Azure CLI"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
tags: azure-resource-manager
keywords: "IPv6, Azure Load Balancer, двойной стек, общедоступный IP-адрес, встроенная поддержка Ipv6, мобильное устройство, Интернет вещей"
ms.assetid: a1957c9c-9c1d-423e-9d5c-d71449bc1f37
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: kumud
ms.openlocfilehash: 7ff75ac90d74a74e3d0c27672b36fbd955a086a3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-internet-facing-load-balancer-with-ipv6-in-azure-resource-manager-using-hello-azure-cli"></a>Создание подсистемы балансировки нагрузки с IPv6 в диспетчере ресурсов Azure с помощью hello Azure CLI с выходом в Интернет

> [!div class="op_single_selector"]
> * [PowerShell](load-balancer-ipv6-internet-ps.md)
> * [Интерфейс командной строки Azure](load-balancer-ipv6-internet-cli.md)
> * [Шаблон](load-balancer-ipv6-internet-template.md)

Azure Load Balancer является балансировщиком нагрузки 4-го уровня (TCP, UDP). Подсистема балансировки нагрузки Hello обеспечивает высокую доступность путем распределения входящего трафика между экземплярами службы работоспособности в облачных службах или виртуальных машин в набор балансировки нагрузки. Azure Load Balancer может также представить данные службы на нескольких портах, нескольких IP-адресах или обоими этими способами.

## <a name="example-deployment-scenario"></a>Пример сценария развертывания

Hello следующей схеме показано решение по балансировке нагрузки hello развертываемого с помощью шаблона пример hello, описанных в этой статье.

![Сценарий использования балансировщика нагрузки](./media/load-balancer-ipv6-internet-cli/lb-ipv6-scenario-cli.png)

В этом случае будут созданы следующие ресурсы Azure hello:

* две виртуальные машины;
* виртуальный сетевой интерфейс для каждой виртуальной машины с назначенными IPv4 и IPv6-адресами;
* балансировщик нагрузки для Интернета с общедоступными IPv4- и IPv6-адресами;
* Группа доступности toothat содержит hello две виртуальные машины
* два загрузить балансировки правила toomap hello открытые виртуальные IP-адреса toohello закрытый конечные точки

## <a name="deploying-hello-solution-using-hello-azure-cli"></a>Развертывание решения hello, с помощью hello Azure CLI

Привет, следующие шаги показывают, как с помощью диспетчера ресурсов Azure с CLI подсистемы балансировки нагрузки, toocreate из Интернета. С помощью диспетчера ресурсов Azure каждый ресурс создается и настроить отдельно и затем поместить toocreate ресурса.

toodeploy подсистемы балансировки нагрузки, создания и настройки hello следующие объекты:

* Конфигурация интерфейсных IP-адресов. Содержит общедоступные IP-адреса для входящего сетевого трафика.
* Пул адресов серверной части - содержит сетевых интерфейсов (NIC) для hello виртуальные машины tooreceive сетевой трафик от подсистемы балансировки нагрузки hello.
* Правила балансировки нагрузки — содержит правила сопоставления открытый порт hello tooport подсистемы балансировки нагрузки в пул адресов серверной части hello.
* Правила NAT для входящих подключений — содержит правила, сопоставление порта открытый порт tooa подсистемы балансировки нагрузки hello для конкретной виртуальной машины в пул адресов серверной части hello.
* Проверяет — содержит доступность toocheck проверки, используемые работоспособности экземпляров виртуальных машин в пул адресов серверной части hello.

Дополнительные сведения см. в статье [Поддержка диспетчера ресурсов Azure для подсистемы балансировки нагрузки](load-balancer-arm.md).

## <a name="set-up-your-cli-environment-toouse-azure-resource-manager"></a>Настройка вашей toouse среды интерфейс командной строки диспетчера ресурсов Azure

В этом примере мы запущены средства CLI hello в окне команд PowerShell. Командлеты Azure PowerShell hello не используются, но мы используем PowerShell сценариев возможности tooimprove удобочитаемость и повторного использования.

1. Если ранее не пользовались Azure CLI, см. раздел [Установка и настройка hello Azure CLI](../cli-install-nodejs.md) и следуйте инструкциям hello toohello точку, где выбирается учетная запись Azure и подписки.
2. Запустите hello **azure конфигурации режима** режим Manager tooResource tooswitch команд.

    ```azurecli
    azure config mode arm
    ```

    Ожидаемые выходные данные:

        info:    New mode is arm

3. Войдите в tooAzure и получить список подписок.

    ```azurecli
    azure login
    ```

    При появлении запроса введите свои учетные данные Azure.

    ```azurecli
    azure account list
    ```

    Выберите подписку hello toouse. Запишите идентификатор hello подписки для следующего шага hello.

4. Настройка переменных PowerShell для использования с командами CLI hello.

    ```powershell
    $subscriptionid = "########-####-####-####-############"  # enter subscription id
    $location = "southcentralus"
    $rgName = "pscontosorg1southctrlus09152016"
    $vnetName = "contosoIPv4Vnet"
    $vnetPrefix = "10.0.0.0/16"
    $subnet1Name = "clicontosoIPv4Subnet1"
    $subnet1Prefix = "10.0.0.0/24"
    $subnet2Name = "clicontosoIPv4Subnet2"
    $subnet2Prefix = "10.0.1.0/24"
    $dnsLabel = "contoso09152016"
    $lbName = "myIPv4IPv6Lb"
    ```

## <a name="create-a-resource-group-a-load-balancer-a-virtual-network-and-subnets"></a>Создание группы ресурсов, балансировщика нагрузки, виртуальной сети и подсетей

1. Создание группы ресурсов

    ```azurecli
    azure group create $rgName $location
    ```

2. Создание балансировщика нагрузки

    ```azurecli
    $lb = azure network lb create --resource-group $rgname --location $location --name $lbName
    ```

3. Создайте виртуальную сеть.

    ```azurecli
    $vnet = azure network vnet create  --resource-group $rgname --name $vnetName --location $location --address-prefixes $vnetPrefix
    ```

    Создайте две подсети в этой виртуальной сети.

    ```azurecli
    $subnet1 = azure network vnet subnet create --resource-group $rgname --name $subnet1Name --address-prefix $subnet1Prefix --vnet-name $vnetName
    $subnet2 = azure network vnet subnet create --resource-group $rgname --name $subnet2Name --address-prefix $subnet2Prefix --vnet-name $vnetName
    ```

## <a name="create-public-ip-addresses-for-hello-front-end-pool"></a>Создание общих IP-адресов для пула переднего плана hello

1. Настройка переменных PowerShell hello

    ```powershell
    $publicIpv4Name = "myIPv4Vip"
    $publicIpv6Name = "myIPv6Vip"
    ```

2. Создайте открытый пул IP-адресов hello интерфейсный IP.

    ```azurecli
    $publicipV4 = azure network public-ip create --resource-group $rgname --name $publicIpv4Name --location $location --ip-version IPv4 --allocation-method Dynamic --domain-name-label $dnsLabel
    $publicipV6 = azure network public-ip create --resource-group $rgname --name $publicIpv6Name --location $location --ip-version IPv6 --allocation-method Dynamic --domain-name-label $dnsLabel
    ```

    > [!IMPORTANT]
    > Hello балансировки нагрузки использует метку домена hello hello общедоступный IP-адрес в качестве его полное доменное имя. Это изменение по сравнению с классической развертывания с использованием имени облачной службы hello как hello балансировки нагрузки полное доменное имя.
    > В этом примере hello полное доменное имя — *contoso09152016.southcentralus.cloudapp.azure.com*.

## <a name="create-front-end-and-back-end-pools"></a>Создание интерфейсного и внутреннего пулов

Этот пример создает hello переднего плана пула IP-адресов, получающий hello входящего сетевого трафика в подсистеме балансировки нагрузки hello и hello серверной части пула IP-адресов где переднего плана пула hello отправляет hello балансировки нагрузки сетевого трафика.

1. Настройка переменных PowerShell hello

    ```powershell
    $frontendV4Name = "FrontendVipIPv4"
    $frontendV6Name = "FrontendVipIPv6"
    $backendAddressPoolV4Name = "BackendPoolIPv4"
    $backendAddressPoolV6Name = "BackendPoolIPv6"
    ```

2. Создайте пул IP переднего плана, связывание hello общедоступный IP-адрес создан в предыдущем шаге hello и Подсистема балансировки нагрузки hello.

    ```azurecli
    $frontendV4 = azure network lb frontend-ip create --resource-group $rgname --name $frontendV4Name --public-ip-name $publicIpv4Name --lb-name $lbName
    $frontendV6 = azure network lb frontend-ip create --resource-group $rgname --name $frontendV6Name --public-ip-name $publicIpv6Name --lb-name $lbName
    $backendAddressPoolV4 = azure network lb address-pool create --resource-group $rgname --name $backendAddressPoolV4Name --lb-name $lbName
    $backendAddressPoolV6 = azure network lb address-pool create --resource-group $rgname --name $backendAddressPoolV6Name --lb-name $lbName
    ```

## <a name="create-hello-probe-nat-rules-and-lb-rules"></a>Создание hello пробы, правил NAT и правила балансировки Нагрузки

В этом примере создается hello следующих элементов:

* toocheck правила проверки для подключения к tooTCP порта 80
* преобразование сетевых адресов правила tootranslate весь входящий трафик на порт 3389 tooport 3389 для протокола удаленного рабочего СТОЛА<sup>1</sup>
* преобразование сетевых адресов правила tootranslate весь входящий трафик на tooport 3391 порт 3389 для протокола удаленного рабочего СТОЛА<sup>1</sup>
* toobalance правило балансировки нагрузки весь входящий трафик на порт 80 tooport 80 на hello адресов серверной части пула hello.

<sup>1</sup> NAT правила, связанные tooa конкретного экземпляра виртуальной машины за подсистемой балансировки нагрузки hello. Hello сетевой трафик, поступающий на порт 3389 отправляется toohello отдельную виртуальную машину и порт, связанный с правилом NAT hello. Для правила NAT необходимо указать протокол (UDP или TCP). Оба эти протокола не может быть назначен toohello тот же порт.

1. Настройка переменных PowerShell hello

    ```powershell
    $probeV4V6Name = "ProbeForIPv4AndIPv6"
    $natRule1V4Name = "NatRule-For-Rdp-VM1"
    $natRule2V4Name = "NatRule-For-Rdp-VM2"
    $lbRule1V4Name = "LBRuleForIPv4-Port80"
    $lbRule1V6Name = "LBRuleForIPv6-Port80"
    ```

2. Создать пробу hello

    Hello следующий пример создает проверки зонда TCP для подключения к конечным tooback TCP-порт 80 каждые 15 секунд. Он помечает hello внутренний ресурс недоступен после двух последовательных сбоев.

    ```azurecli
    $probeV4V6 = azure network lb probe create --resource-group $rgname --name $probeV4V6Name --protocol tcp --port 80 --interval 15 --count 2 --lb-name $lbName
    ```

3. Создание правила для входящих подключений NAT, поддерживающих соединения протокола удаленного рабочего СТОЛА toohello серверным ресурсам

    ```azurecli
    $inboundNatRuleRdp1 = azure network lb inbound-nat-rule create --resource-group $rgname --name $natRule1V4Name --frontend-ip-name $frontendV4Name --protocol Tcp --frontend-port 3389 --backend-port 3389 --lb-name $lbName
    $inboundNatRuleRdp2 = azure network lb inbound-nat-rule create --resource-group $rgname --name $natRule2V4Name --frontend-ip-name $frontendV4Name --protocol Tcp --frontend-port 3391 --backend-port 3389 --lb-name $lbName
    ```

4. Создание правил, которые отправлять трафик порты внутренней toodifferent в зависимости от того, какой запрос hello полученных переднего плана подсистемы балансировки нагрузки

    ```azurecli
    $lbruleIPv4 = azure network lb rule create --resource-group $rgname --name $lbRule1V4Name --frontend-ip-name $frontendV4Name --backend-address-pool-name $backendAddressPoolV4Name --probe-name $probeV4V6Name --protocol Tcp --frontend-port 80 --backend-port 80 --lb-name $lbName
    $lbruleIPv6 = azure network lb rule create --resource-group $rgname --name $lbRule1V6Name --frontend-ip-name $frontendV6Name --backend-address-pool-name $backendAddressPoolV6Name --probe-name $probeV4V6Name --protocol Tcp --frontend-port 80 --backend-port 8080 --lb-name $lbName
    ```

5. Проверьте параметры.

    ```azurecli
    azure network lb show --resource-group $rgName --name $lbName
    ```

    Ожидаемые выходные данные:

        info:    Executing command network lb show
        info:    Looking up hello load balancer "myIPv4IPv6Lb"
        data:    Id                              : /subscriptions/########-####-####-####-############/resourceGroups/pscontosorg1southctrlus09152016/providers/Microsoft.Network/loadBalancers/myIPv4IPv6Lb
        data:    Name                            : myIPv4IPv6Lb
        data:    Type                            : Microsoft.Network/loadBalancers
        data:    Location                        : southcentralus
        data:    Provisioning state              : Succeeded
        data:
        data:    Frontend IP configurations:
        data:    Name             Provisioning state  Private IP allocation  Private IP   Subnet  Public IP
        data:    ---------------  ------------------  ---------------------  -----------  ------  ---------
        data:    FrontendVipIPv4  Succeeded           Dynamic                                     myIPv4Vip
        data:    FrontendVipIPv6  Succeeded           Dynamic                                     myIPv6Vip
        data:
        data:    Probes:
        data:    Name                 Provisioning state  Protocol  Port  Path  Interval  Count
        data:    -------------------  ------------------  --------  ----  ----  --------  -----
        data:    ProbeForIPv4AndIPv6  Succeeded           Tcp       80          15        2
        data:
        data:    Backend Address Pools:
        data:    Name             Provisioning state
        data:    ---------------  ------------------
        data:    BackendPoolIPv4  Succeeded
        data:    BackendPoolIPv6  Succeeded
        data:
        data:    Load Balancing Rules:
        data:    Name                  Provisioning state  Load distribution  Protocol  Frontend port  Backend port  Enable floating IP  Idle timeout in minutes
        data:    --------------------  ------------------  -----------------  --------  -------------  ------------  ------------------  -----------------------
        data:    LBRuleForIPv4-Port80  Succeeded           Default            Tcp       80             80            false               4
        data:    LBRuleForIPv6-Port80  Succeeded           Default            Tcp       80             8080          false               4
        data:
        data:    Inbound NAT Rules:
        data:    Name                 Provisioning state  Protocol  Frontend port  Backend port  Enable floating IP  Idle timeout in minutes
        data:    -------------------  ------------------  --------  -------------  ------------  ------------------  -----------------------
        data:    NatRule-For-Rdp-VM1  Succeeded           Tcp       3389           3389          false               4
        data:    NatRule-For-Rdp-VM2  Succeeded           Tcp       3391           3389          false               4
        info:    network lb show

## <a name="create-nics"></a>Создание сетевых адаптеров

Создать сетевые адаптеры и связать их tooNAT правила, правила подсистемы балансировки нагрузки и зонды.

1. Настройка переменных PowerShell hello

    ```powershell
    $nic1Name = "myIPv4IPv6Nic1"
    $nic2Name = "myIPv4IPv6Nic2"
    $subnet1Id = "/subscriptions/$subscriptionid/resourceGroups/$rgName/providers/Microsoft.Network/VirtualNetworks/$vnetName/subnets/$subnet1Name"
    $subnet2Id = "/subscriptions/$subscriptionid/resourceGroups/$rgName/providers/Microsoft.Network/VirtualNetworks/$vnetName/subnets/$subnet2Name"
    $backendAddressPoolV4Id = "/subscriptions/$subscriptionid/resourceGroups/$rgname/providers/Microsoft.Network/loadbalancers/$lbName/backendAddressPools/$backendAddressPoolV4Name"
    $backendAddressPoolV6Id = "/subscriptions/$subscriptionid/resourceGroups/$rgname/providers/Microsoft.Network/loadbalancers/$lbName/backendAddressPools/$backendAddressPoolV6Name"
    $natRule1V4Id = "/subscriptions/$subscriptionid/resourceGroups/$rgname/providers/Microsoft.Network/loadbalancers/$lbName/inboundNatRules/$natRule1V4Name"
    $natRule2V4Id = "/subscriptions/$subscriptionid/resourceGroups/$rgname/providers/Microsoft.Network/loadbalancers/$lbName/inboundNatRules/$natRule2V4Name"
    ```

2. Создайте сетевую карту для каждой серверной части и добавьте конфигурацию IPv6.

    ```azurecli
    $nic1 = azure network nic create --name $nic1Name --resource-group $rgname --location $location --private-ip-version "IPv4" --subnet-id $subnet1Id --lb-address-pool-ids $backendAddressPoolV4Id --lb-inbound-nat-rule-ids $natRule1V4Id
    $nic1IPv6 = azure network nic ip-config create --resource-group $rgname --name "IPv6IPConfig" --private-ip-version "IPv6" --lb-address-pool-ids $backendAddressPoolV6Id --nic-name $nic1Name

    $nic2 = azure network nic create --name $nic2Name --resource-group $rgname --location $location --subnet-id $subnet1Id --lb-address-pool-ids $backendAddressPoolV4Id --lb-inbound-nat-rule-ids $natRule2V4Id
    $nic2IPv6 = azure network nic ip-config create --resource-group $rgname --name "IPv6IPConfig" --private-ip-version "IPv6" --lb-address-pool-ids $backendAddressPoolV6Id --nic-name $nic2Name
    ```

## <a name="create-hello-back-end-vm-resources-and-attach-each-nic"></a>Создать ресурсы виртуальной Машины сервера hello и присоединить каждый сетевой Адаптер

toocreate виртуальные машины, необходимо иметь учетную запись хранилища. Для балансировки нагрузки, hello виртуальные машины должны toobe члены группы доступности. Дополнительные сведения о создании виртуальных машин см. в статье [Создание виртуальной машины в Azure с помощью PowerShell](../virtual-machines/virtual-machines-windows-ps-create.md?toc=%2fazure%2fload-balancer%2ftoc.json).

1. Настройка переменных PowerShell hello

    ```powershell
    $storageAccountName = "ps08092016v6sa0"
    $availabilitySetName = "myIPv4IPv6AvailabilitySet"
    $vm1Name = "myIPv4IPv6VM1"
    $vm2Name = "myIPv4IPv6VM2"
    $nic1Id = "/subscriptions/$subscriptionid/resourceGroups/$rgname/providers/Microsoft.Network/networkInterfaces/$nic1Name"
    $nic2Id = "/subscriptions/$subscriptionid/resourceGroups/$rgname/providers/Microsoft.Network/networkInterfaces/$nic2Name"
    $disk1Name = "WindowsVMosDisk1"
    $disk2Name = "WindowsVMosDisk2"
    $osDisk1Uri = "https://$storageAccountName.blob.core.windows.net/vhds/$disk1Name.vhd"
    $osDisk2Uri = "https://$storageAccountName.blob.core.windows.net/vhds/$disk2Name.vhd"
    $imageurn "MicrosoftWindowsServer:WindowsServer:2012-R2-Datacenter:latest"
    $vmUserName = "vmUser"
    $mySecurePassword = "PlainTextPassword*1"
    ```

    > [!WARNING]
    > В этом примере используется hello имя пользователя и пароль для виртуальных машин hello в виде открытого текста. При с помощью учетные данные в hello снимите следует принять соответствующие меры. Это более безопасный способ обработки учетных данных в PowerShell, в разделе hello [Get-Credential](https://technet.microsoft.com/library/hh849815.aspx) командлета.

2. Создание учетной записи и доступности набора hello хранилища

    Вы можете использовать существующую учетную запись хранилища при создании hello виртуальных машин. Привет, следующая команда создает новую учетную запись хранения.

    ```azurecli
    $storageAcc = azure storage account create $storageAccountName --resource-group $rgName --location $location --sku-name "LRS" --kind "Storage"
    ```

    Создайте группу доступности hello.

    ```azurecli
    $availabilitySet = azure availset create --name $availabilitySetName --resource-group $rgName --location $location
    ```

3. Создание виртуальных машин hello с сетевыми адаптерами связанные hello

    ```azurecli
    $vm1 = azure vm create --resource-group $rgname --location $location --availset-name $availabilitySetName --name $vm1Name --nic-id $nic1Id --os-disk-vhd $osDisk1Uri --os-type "Windows" --admin-username $vmUserName --admin-password $mySecurePassword --vm-size "Standard_A1" --image-urn $imageurn --storage-account-name $storageAccountName --disable-bginfo-extension

    $vm2 = azure vm create --resource-group $rgname --location $location --availset-name $availabilitySetName --name $vm2Name --nic-id $nic2Id --os-disk-vhd $osDisk2Uri --os-type "Windows" --admin-username $vmUserName --admin-password $mySecurePassword --vm-size "Standard_A1" --image-urn $imageurn --storage-account-name $storageAccountName --disable-bginfo-extension
    ```

## <a name="next-steps"></a>Дальнейшие действия

[Приступая к настройке внутренней подсистемы балансировки нагрузки](load-balancer-get-started-ilb-arm-cli.md)

[Настройка режима распределения подсистемы балансировки нагрузки](load-balancer-distribution-mode.md)

[Настройка параметров времени ожидания простоя TCP для подсистемы балансировки нагрузки](load-balancer-tcp-idle-timeout.md)
