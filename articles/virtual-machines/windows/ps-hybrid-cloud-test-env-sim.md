---
title: "aaaSimulated гибридного облака тестовой среды | Документы Microsoft"
description: "Создание смоделированной гибридной облачной среды для ИТ-специалистов или тестирования разработки с использованием двух виртуальных сетей Azure и подключения тип VNet-to-VNet."
services: virtual-machines-windows
documentationcenter: 
author: JoeDavies-MSFT
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: ca5bf294-8172-44a9-8fed-d6f38d345364
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 09/30/2016
ms.author: josephd
ms.openlocfilehash: 6063022e373c2b3564e040c4fbee122e2438974b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-a-simulated-hybrid-cloud-environment-for-testing"></a>Создание имитации гибридной облачной среды для тестирования
В этом разделе описываются шаги по созданию смоделированной гибридной облачной среды с помощью платформы Microsoft Azure, использующей две виртуальные сети Azure. Здесь представлена конфигурация полученный hello.

![](./media/ps-hybrid-cloud-test-env-sim/virtual-machines-windows-ps-hybrid-cloud-test-env-sim-ph4.png)

Она позволяет смоделировать гибридную облачную рабочую среду и состоит из следующих элементов:

* Имитация и упрощенный локальной сети в виртуальной сети Azure (hello тестовая лаборатория виртуальной сети).
* смоделированная виртуальная сеть с подключением между организациями, размещенная в Azure (TestVNET).
* Подключение виртуальной сети для виртуальной сети между hello двух виртуальных сетей.
* Дополнительный контроллер домена в виртуальной сети TestVNET hello.

Это основа и общая начальная точка, на базе которой можно:

* разрабатывать и тестировать приложения в смоделированной гибридной облачной среде.
* Создание конфигураций тестов из компьютеров, некоторые в hello тестовая лаборатория виртуальной сети, а некоторые в виртуальной сети TestVNET hello, toosimulate гибридной облачной ИТ-задач.

Существует четыре основных этапа toosetting этой тестовой среды гибридного облака:

1. Настройка виртуальной сети hello тестовая лаборатория.
2. Создайте виртуальную сеть между организациями hello.
3. Создание VPN-подключения hello виртуальной сети для виртуальной сети.
4. Настройка DC2. 

Для этой конфигурации требуется подписка Azure. Если у вас есть подписка MSDN или Visual Studio, ознакомьтесь с разделом [Ежемесячная сумма денег на счете в Azure для подписчиков Visual Studio](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/).

> [!NOTE]
> Виртуальные машины и шлюзы виртуальных сетей в Azure создают текущие расходы во время своей работы. На эти затраты выставляется счет при использовании подписки MSDN или платной подписки. Шлюз Azure VPN реализован как набор двух виртуальных машин Azure. toominimize hello затрат, создание тестовой среды hello и как можно быстрее выполнить необходимые попробовать и демонстрацию.
> 
> 

## <a name="phase-1-configure-hello-testlab-virtual-network"></a>Этап 1: Настройка hello тестовая лаборатория виртуальной сети
Используйте инструкции hello в hello [базовая конфигурация тестовой среды](https://technet.microsoft.com/library/mt771177.aspx) разделе tooconfigure hello DC1, APP1 и CLIENT1 компьютеров в виртуальной сети Azure, с именем тестовая лаборатория hello. 

Затем запустите командную строку Azure PowerShell.

> [!NOTE]
> Следующая команда задает Hello использовать Azure PowerShell версии 1.0 и более поздней версии.
> 
> 

Войдите в учетную запись tooyour.

    Login-AzureRMAccount

Получите имя своей подписки, используя следующую команду hello.

    Get-AzureRMSubscription | Sort SubscriptionName | Select SubscriptionName

Настройте свою подписку Azure. Используйте hello же подписку, которая использовалась toobuild базовой конфигурации на этапе 1. Замените весь код внутри кавычек hello, включая hello < и > символы, с правильным именем hello.

    $subscr="<subscription name>"
    Get-AzureRmSubscription –SubscriptionName $subscr | Select-AzureRmSubscription

Далее следует добавьте шлюз подсети toohello тестовая лаборатория виртуальной сети для базовой конфигурации, которой будет hello toohost используется шлюз Azure.

    $rgName="<name of your resource group that you used for your TestLab virtual network>"
    $locName="<Azure location name where you placed hello TestLab virtual network, such as West US>"
    $vnet=Get-AzureRmVirtualNetwork -ResourceGroupName $rgName -Name TestLab
    Add-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -AddressPrefix 10.255.255.248/29 -VirtualNetwork $vnet
    Set-AzureRmVirtualNetwork -VirtualNetwork $vnet

Далее запрос открытый IP адрес tooassign toohello шлюза виртуальной сети hello тестовая лаборатория.

    $gwpip=New-AzureRmPublicIpAddress -Name TestLab_pip -ResourceGroupName $rgName -Location $locName -AllocationMethod Dynamic

Создайте шлюз.

    $vnet=Get-AzureRmVirtualNetwork -Name TestLab -ResourceGroupName $rgName
    $subnet=Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet
    $gwipconfig=New-AzureRmVirtualNetworkGatewayIpConfig -Name TestLab_GWConfig -SubnetId $subnet.Id -PublicIpAddressId $gwpip.Id 
    New-AzureRmVirtualNetworkGateway -Name TestLab_GW -ResourceGroupName $rgName -Location $locName -IpConfigurations $gwipconfig -GatewayType Vpn -VpnType RouteBased

Имейте в виду, что для новых шлюзов может потребоваться 20 минут или более toocreate.

Подключитесь tooDC1 с учетные данные CORP\User1 hello hello портал Azure на локальном компьютере. домен CORP tooconfigure hello, чтобы компьютеры и пользователи используют их локального контроллера домена для проверки подлинности, выполняйте эти команды из командной строки Windows PowerShell с правами администратора на компьютере DC1.

    New-ADReplicationSite -Name "TestLab" 
    New-ADReplicationSite -Name "TestVNET"
    New-ADReplicationSubnet -Name "10.0.0.0/8" -Site "TestLab"
    New-ADReplicationSubnet -Name "192.168.0.0/16" -Site "TestVNET"

Это текущая конфигурация.

![](./media/ps-hybrid-cloud-test-env-sim/virtual-machines-windows-ps-hybrid-cloud-test-env-sim-ph1.png)

## <a name="phase-2-create-hello-testvnet-virtual-network"></a>Этап 2: Создайте виртуальную сеть TestVNET hello
Во-первых создайте виртуальную сеть TestVNET hello и защитите его с сетевой группой безопасности.

    $rgName="<name of hello resource group that you used for your TestLab virtual network>"
    $locName="<Azure location name where you placed hello TestLab virtual network, such as West US>"
    $locShortName="<Azure location name from $locName in all lowercase letters with spaces removed. Example:  westus>"
    $testSubnet=New-AzureRMVirtualNetworkSubnetConfig -Name "TestSubnet" -AddressPrefix 192.168.0.0/24
    $gatewaySubnet=New-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -AddressPrefix 192.168.255.248/29
    New-AzureRMVirtualNetwork -Name "TestVNET" -ResourceGroupName $rgName -Location $locName -AddressPrefix 192.168.0.0/16 -Subnet $testSubnet,$gatewaySubnet –DNSServer 10.0.0.4
    $rule1=New-AzureRMNetworkSecurityRuleConfig -Name "RDPTraffic" -Description "Allow RDP tooall VMs on hello subnet" -Access Allow -Protocol Tcp -Direction Inbound -Priority 100 -SourceAddressPrefix Internet -SourcePortRange * -DestinationAddressPrefix * -DestinationPortRange 3389
    New-AzureRMNetworkSecurityGroup -Name "TestSubnet" -ResourceGroupName $rgName -Location $locShortName -SecurityRules $rule1
    $vnet=Get-AzureRMVirtualNetwork -ResourceGroupName $rgName -Name TestVNET
    $nsg=Get-AzureRMNetworkSecurityGroup -Name "TestSubnet" -ResourceGroupName $rgName
    Set-AzureRMVirtualNetworkSubnetConfig -VirtualNetwork $vnet -Name "TestSubnet" -AddressPrefix 192.168.0.0/24 -NetworkSecurityGroup $nsg

Далее запрос открытый toobe адрес IP выделенный toohello шлюз для виртуальной сети TestVNET hello и создания шлюза.

    $gwpip=New-AzureRmPublicIpAddress -Name TestVNET_pip -ResourceGroupName $rgName -Location $locName -AllocationMethod Dynamic
    $vnet=Get-AzureRmVirtualNetwork -Name TestVNET -ResourceGroupName $rgName
    $subnet=Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet
    $gwipconfig=New-AzureRmVirtualNetworkGatewayIpConfig -Name "TestVNET_GWConfig" -SubnetId $subnet.Id -PublicIpAddressId $gwpip.Id
    New-AzureRmVirtualNetworkGateway -Name "TestVNET_GW" -ResourceGroupName $rgName -Location $locName -IpConfigurations $gwipconfig -GatewayType Vpn -VpnType RouteBased

Это текущая конфигурация.

![](./media/ps-hybrid-cloud-test-env-sim/virtual-machines-windows-ps-hybrid-cloud-test-env-sim-ph2.png)

## <a name="phase-3-create-hello-vnet-to-vnet-connection"></a>Этап 3: Создание подключения hello виртуальной сети для виртуальной сети
Сначала получите случайный, надежно зашифрованный 32-значный общий ключ у администратора сети или администратора безопасности. Можно также использовать информацию hello в [Создание произвольной строки предварительного ключа IPsec](http://social.technet.microsoft.com/wiki/contents/articles/32330.create-a-random-string-for-an-ipsec-preshared-key.aspx) tooobtain общий ключ.

Затем используйте эти команды toocreate hello виртуальная сеть — сеть VPN-подключения, что может занять некоторое время toocomplete.

    $sharedKey="<pre-shared key value>"
    $gwTestLab=Get-AzureRmVirtualNetworkGateway -Name TestLab_GW -ResourceGroupName $rgName
    $gwTestVNET=Get-AzureRmVirtualNetworkGateway -Name TestVNET_GW -ResourceGroupName $rgName
    New-AzureRmVirtualNetworkGatewayConnection -Name TestLab_to_TestVNET -ResourceGroupName $rgName -VirtualNetworkGateway1 $gwTestLab -VirtualNetworkGateway2 $gwTestVNET -Location $locName -ConnectionType Vnet2Vnet -SharedKey $sharedKey
    New-AzureRmVirtualNetworkGatewayConnection -Name TestVNET_to_TestLab -ResourceGroupName $rgName -VirtualNetworkGateway1 $gwTestVNET -VirtualNetworkGateway2 $gwTestLab -Location $locName -ConnectionType Vnet2Vnet -SharedKey $sharedKey

Через несколько минут hello подключение должно быть установлено.

Это текущая конфигурация.

![](./media/ps-hybrid-cloud-test-env-sim/virtual-machines-windows-ps-hybrid-cloud-test-env-sim-ph3.png)

## <a name="phase-4-configure-dc2"></a>Этап 4. Настройка DC2
Прежде всего создайте виртуальную машину для DC2. Выполняйте эти команды в командной строке hello Azure PowerShell на локальном компьютере.

    $rgName="<your resource group name>"
    $locName="<your Azure location, such as West US>"
    $saName="<hello storage account name for hello base configuration>"
    $vnet=Get-AzureRMVirtualNetwork -Name TestVNET -ResourceGroupName $rgName
    $pip=New-AzureRMPublicIpAddress -Name DC2-NIC -ResourceGroupName $rgName -Location $locName -AllocationMethod Dynamic
    $nic=New-AzureRMNetworkInterface -Name DC2-NIC -ResourceGroupName $rgName -Location $locName -SubnetId $vnet.Subnets[0].Id -PublicIpAddressId $pip.Id -PrivateIpAddress 192.168.0.4
    $vm=New-AzureRMVMConfig -VMName DC2 -VMSize Standard_A1
    $storageAcc=Get-AzureRMStorageAccount -ResourceGroupName $rgName -Name $saName
    $vhdURI=$storageAcc.PrimaryEndpoints.Blob.ToString() + "vhds/DC2-TestVNET-ADDSDisk.vhd"
    Add-AzureRMVMDataDisk -VM $vm -Name ADDS-Data -DiskSizeInGB 20 -VhdUri $vhdURI  -CreateOption empty
    $cred=Get-Credential -Message "Type hello name and password of hello local administrator account for DC2."
    $vm=Set-AzureRMVMOperatingSystem -VM $vm -Windows -ComputerName DC2 -Credential $cred -ProvisionVMAgent -EnableAutoUpdate
    $vm=Set-AzureRMVMSourceImage -VM $vm -PublisherName MicrosoftWindowsServer -Offer WindowsServer -Skus 2012-R2-Datacenter -Version "latest"
    $vm=Add-AzureRMVMNetworkInterface -VM $vm -Id $nic.Id
    $osDiskUri=$storageAcc.PrimaryEndpoints.Blob.ToString() + "vhds/DC2-TestLab-OSDisk.vhd"
    $vm=Set-AzureRMVMOSDisk -VM $vm -Name DC2-TestVNET-OSDisk -VhdUri $osDiskUri -CreateOption fromImage
    New-AzureRMVM -ResourceGroupName $rgName -Location $locName -VM $vm

Затем подключитесь toohello Новая виртуальная машина DC2 из hello портал Azure.

Настройте трафика tooallow правило брандмауэра Windows для тестирования связности. Из командной строки Windows PowerShell с правами администратора на DC2 выполните следующие команды.

    Set-NetFirewallRule -DisplayName "File and Printer Sharing (Echo Request - ICMPv4-In)" -enabled True
    ping dc1.corp.contoso.com

команда ping Hello должны появиться четыре успешного ответа от IP-адрес 10.0.0.4. Это тест трафика между hello подключения VNet-VNet.

Добавьте hello дополнительный диск данных на DC2 как новый том с буквой hello диска «f:».

1. Hello левой панели диспетчера сервера щелкните **файловых служб и служб хранилища**, а затем нажмите кнопку **дисков**.
2. В области содержимого hello в hello **дисков** щелкните **диск 2** (с hello **секции** значение слишком**Неизвестный**).
3. Щелкните **Задачи**, а затем **Новый том**.
4. Hello перед началом страница приветствия мастера создания тома, щелкните **Далее**.
5. На сервере выберите hello hello и страницы с диска, нажмите кнопку **диск 2**, а затем нажмите кнопку **Далее**. При появлении запроса нажмите кнопку **OK**.
6. Щелкните hello задать hello размер страницы приветствия тома, **Далее**.
7. На hello Assign tooa диска буква или папка "нажмите" **Далее**.
8. На странице параметров системы hello выберите файл, нажмите кнопку **Далее**.
9. На странице подтверждения выбранных элементов hello щелкните **создать**.
10. После завершения нажмите кнопку **Закрыть**.

Затем настройте DC2 в качестве реплики контроллера домена для домена corp.contoso.com hello. Выполните следующие команды из командной строки Windows PowerShell hello на DC2.

    Install-WindowsFeature AD-Domain-Services -IncludeManagementTools
    Install-ADDSDomainController -Credential (Get-Credential CORP\User1) -DomainName "corp.contoso.com" -InstallDns:$true -DatabasePath "F:\NTDS" -LogPath "F:\Logs" -SysvolPath "F:\SYSVOL"

Обратите внимание, что вы запрашиваемые toosupply оба hello CORP\User1 пароль и пароль режима восстановления служб каталогов (DSRM) и toorestart DC2.

Теперь, когда hello TestVNET виртуальной сети имеет свой собственный DNS-сервер (DC2), необходимо настроить hello TestVNET виртуальной сети toouse этого DNS-сервера.

1. Hello левой части hello портал Azure, щелкните значок hello виртуальные сети и нажмите кнопку **TestVNET**.
2. На hello **параметры** щелкните **DNS-серверы**.
3. В **основной DNS-сервер**, тип **192.168.0.4** tooreplace 10.0.0.4.
4. Щелкните **Сохранить**.

Это текущая конфигурация. 

![](./media/ps-hybrid-cloud-test-env-sim/virtual-machines-windows-ps-hybrid-cloud-test-env-sim-ph4.png)

Смоделированная гибридная облачная среда готова для тестирования.

## <a name="next-step"></a>Дальнейшие действия
* Настройте в этой среде [специализированное веб-приложение](ps-hybrid-cloud-test-env-lob.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

