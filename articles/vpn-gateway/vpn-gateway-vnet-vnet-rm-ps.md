---
title: "Подключение виртуальной сети Azure tooanother виртуальной сети: PowerShell | Документы Microsoft"
description: "Эта статья описывает этапы настройки подключения между виртуальными сетями с помощью диспетчера ресурсов Azure и PowerShell."
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 0683c664-9c03-40a4-b198-a6529bf1ce8b
ms.service: vpn-gateway
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/02/2017
ms.author: cherylmc
ms.openlocfilehash: 2da30c76867cc3f71d040e63e0dd15d153e15c10
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="configure-a-vnet-to-vnet-vpn-gateway-connection-using-powershell"></a>Настройка подключения VPN-шлюза между виртуальными сетями с помощью PowerShell

В этой статье показано, как toocreate шлюза VPN-подключение между виртуальными сетями. Hello виртуальные сети могут находиться в Здравствуйте, или же в разных регионах, и из hello таким же или разных подписках. При подключении виртуальных сетей из разных подписок, подписки hello не обязательно toobe, связанный с hello того же клиента Active Directory. 

в этой статье инструкциям Hello применяются toohello модели развертывания диспетчера ресурсов и с помощью PowerShell. Можно также создать этой конфигурации с помощью средства развертывания или модель развертывания, выбрав другой вариант из hello после списка.

> [!div class="op_single_selector"]
> * [Портал Azure](vpn-gateway-howto-vnet-vnet-resource-manager-portal.md)
> * [PowerShell](vpn-gateway-vnet-vnet-rm-ps.md)
> * [Интерфейс командной строки Azure](vpn-gateway-howto-vnet-vnet-cli.md)
> * [Портал Azure (классический)](vpn-gateway-howto-vnet-vnet-portal-classic.md)
> * [Подключение с использованием разных моделей развертывания — портал Azure](vpn-gateway-connect-different-deployment-models-portal.md)
> * [Подключение с использованием разных моделей развертывания — PowerShell](vpn-gateway-connect-different-deployment-models-powershell.md)
>
>

Подключение виртуальной сети tooanother виртуальной сети (VNet-VNet) — примерно tooconnecting локального сайта виртуальной сети tooan расположения. Оба типа подключения используйте tooprovide шлюза VPN защищенный туннель, с помощью IPsec/IKE. Если ваш виртуальных сетей в hello совпадают, вы можете tooconsider подключаются с помощью Пиринг виртуальной сети. При пиринговой связи между виртуальными сетями VPN-шлюз не используется. Дополнительную информацию см. в статье [Пиринговая связь между виртуальными сетями](../virtual-network/virtual-network-peering-overview.md).

Подключение типа "виртуальная сеть — виртуальная сеть" можно комбинировать с многосайтовыми конфигурациями. Это дает возможность установления сетевых топологий, которые объединяют подключения между организациями с подключением между виртуальными сетями, как показано в hello, следующая схема:

![Сведения о подключениях](./media/vpn-gateway-vnet-vnet-rm-ps/aboutconnections.png)

### <a name="why-connect-virtual-networks"></a>Что может дать связь между виртуальными сетями

Вы можете tooconnect виртуальных сетей для hello следующих причин:

* **Межрегиональная географическая избыточность и географическое присутствие**

  * Вы можете настроить собственную георепликацию или синхронизацию с безопасной связью без прохождения трафика через конечные точки с выходом в Интернет.
  * С помощью Azure Load Balancer и диспетчера трафика можно настроить высокодоступную рабочую нагрузку с геоизбыточностью в нескольких регионах Azure. Важный пример — tooset копии SQL Always On с группами доступности, распределение по нескольким регионам Azure.
* **Региональные многоуровневые приложения с изоляцией или административной границей**

  * В пределах hello же регионе, можно настроить многоуровневые приложения с несколькими виртуальными сетями, которые соединены друг с другом, из-за tooisolation или требований администрирования.

Дополнительные сведения о подключениях к виртуальной сети для виртуальной сети см. в разделе hello [часто задаваемые вопросы о виртуальной сети для виртуальной сети](#faq) конце hello в этой статье.

## <a name="which-set-of-steps-should-i-use"></a>Каким инструкциям следовать?

В этой статье приведены два разных набора действий. Один набор шагов для [Здравствуйте, виртуальных сетей, которые находятся в одной подписке](#samesub), а другой — [виртуальных сетей, которые находятся в разных подписках](#difsub). Hello ключевое различие между наборами hello — можно создать и настроить все виртуальные ресурсы сети и шлюза hello одного сеанса PowerShell.

Hello действия, описанные в этой статье использовать переменные, объявленные в начале каждого раздела hello. Если вы уже работаете с существующие виртуальные сети, измените параметры hello переменные tooreflect hello в собственной среде. Сведения о разрешении имен виртуальных машин см. в [этой статье](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md).

## <a name="samesub"></a>Как tooconnect виртуальных сетей, находящихся в hello одной подписке

![Схема подключения между виртуальными сетями](./media/vpn-gateway-vnet-vnet-rm-ps/v2vrmps.png)

### <a name="before-you-begin"></a>Перед началом работы

Прежде чем начать, необходимо tooinstall hello последняя версия командлетов Azure PowerShell диспетчера ресурсов hello, по крайней мере версии 4.0 или более поздней версии. Дополнительные сведения об установке hello командлеты PowerShell см. в разделе [как tooinstall и настройка Azure PowerShell](/powershell/azure/overview).

### <a name="Step1"></a>Шаг 1. Планирование диапазонов IP-адресов

В hello, выполнив действия мы создадим два виртуальных сетей вместе с их соответствующими шлюза подсетях и конфигурациях. Затем создадим VPN-подключение между hello двух виртуальных сетей. Это важные tooplan hello IP-адресов для настройки сети. Имейте в виду, необходимо убедиться в том, что ни один из диапазонов виртуальных сетей или диапазонов локальных сетей никак не перекрываются. В этих примерах мы не включаем DNS-сервер. Сведения о разрешении имен виртуальных машин см. в [этой статье](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md).

Мы используем следующие значения в примерах hello hello:

**Значения для TestVNet1:**

* Имя виртуальной сети: TestVNet1
* Группа ресурсов: TestRG1
* Расположение: восточная часть США
* TestVNet1: 10.11.0.0/16 и 10.12.0.0/16
* FrontEnd: 10.11.0.0/24
* BackEnd: 10.12.0.0/24
* GatewaySubnet: 10.12.255.0/27
* Имя шлюза: VNet1GW
* Общедоступный IP-адрес: VNet1GWIP
* Тип VPN: RouteBased
* Подключение (1–4): VNet1toVNet4
* Подключение (1–5): VNet1toVNet5
* Тип подключения: VNet2VNet

**Значения для TestVNet4:**

* Имя виртуальной сети: TestVNet4
* TestVNet2: 10.41.0.0/16 и 10.42.0.0/16
* FrontEnd: 10.41.0.0/24
* BackEnd: 10.42.0.0/24
* GatewaySubnet: 10.42.255.0/27
* Группа ресурсов: TestRG4
* Расположение: Запад США
* Имя шлюза: VNet4GW
* Общедоступный IP-адрес: VNet4GWIP
* Тип VPN: RouteBased
* Подключение: VNet4toVNet1
* Тип подключения: VNet2VNet


### <a name="Step2"></a>Шаг 2. Создание и настройка TestVNet1

1. Объявите переменные. В этом примере hello переменных объявляются с помощью hello значения для этого упражнения. В большинстве случаев следует заменить значения hello свои собственные. Тем не менее эти переменные можно использовать при выполнении через toobecome действия hello знакомы с этим типом конфигурации. Изменение переменных hello, при необходимости, а затем скопируйте и вставьте их в консоль PowerShell.

  ```powershell
  $Sub1 = "Replace_With_Your_Subcription_Name"
  $RG1 = "TestRG1"
  $Location1 = "East US"
  $VNetName1 = "TestVNet1"
  $FESubName1 = "FrontEnd"
  $BESubName1 = "Backend"
  $GWSubName1 = "GatewaySubnet"
  $VNetPrefix11 = "10.11.0.0/16"
  $VNetPrefix12 = "10.12.0.0/16"
  $FESubPrefix1 = "10.11.0.0/24"
  $BESubPrefix1 = "10.12.0.0/24"
  $GWSubPrefix1 = "10.12.255.0/27"
  $GWName1 = "VNet1GW"
  $GWIPName1 = "VNet1GWIP"
  $GWIPconfName1 = "gwipconf1"
  $Connection14 = "VNet1toVNet4"
  $Connection15 = "VNet1toVNet5"
  ```

2. Подключите tooyour учетную запись. Используйте следующий пример toohelp подключении hello.

  ```powershell
  Login-AzureRmAccount
  ```

  Проверьте hello подписки для учетной записи hello.

  ```powershell
  Get-AzureRmSubscription
  ```

  Укажите требуемый toouse подписки hello.

  ```powershell
  Select-AzureRmSubscription -SubscriptionName $Sub1
  ```
3. Создайте новую группу ресурсов.

  ```powershell
  New-AzureRmResourceGroup -Name $RG1 -Location $Location1
  ```
4. Создание конфигурации подсети для TestVNet1 hello. В этом примере создается виртуальная сеть с именем TestVNet1 и три подсети: GatewaySubnet, FrontEnd и Backend. При замене значений важно, чтобы вы назвали подсеть шлюза именем GatewaySubnet. Если вы используете другое имя, создание шлюза завершится сбоем.

  Hello следующий пример использует переменные hello, было установлено ранее. В этом примере hello подсеть шлюза используется /27. Хотя возможных toocreate как /29 подсеть шлюза, рекомендуется создать подсеть большего размера, включающий несколько адресов, выбрав по крайней мере /28 или /27. Это позволит достаточно адреса tooaccommodate возможные дополнительные настройки, вы можете в hello будущих.

  ```powershell
  $fesub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $FESubName1 -AddressPrefix $FESubPrefix1
  $besub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $BESubName1 -AddressPrefix $BESubPrefix1
  $gwsub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $GWSubName1 -AddressPrefix $GWSubPrefix1
  ```
5. Создайте TestVNet1.

  ```powershell
  New-AzureRmVirtualNetwork -Name $VNetName1 -ResourceGroupName $RG1 `
  -Location $Location1 -AddressPrefix $VNetPrefix11,$VNetPrefix12 -Subnet $fesub1,$besub1,$gwsub1
  ```
6. Запрос открытый IP-адрес toobe toohello выделенный шлюз, создаваемых для виртуальной сети. Обратите внимание, что hello AllocationMethod является динамической. Нельзя указать hello IP-адреса, которые должны toouse. Он служит шлюзом динамически выделяемый tooyour. 

  ```powershell
  $gwpip1 = New-AzureRmPublicIpAddress -Name $GWIPName1 -ResourceGroupName $RG1 `
  -Location $Location1 -AllocationMethod Dynamic
  ```
7. Создайте конфигурацию шлюза hello. Конфигурация шлюза Hello определяет подсеть hello и hello открытый IP адрес toouse. Используйте toocreate пример hello конфигурацию шлюза.

  ```powershell
  $vnet1 = Get-AzureRmVirtualNetwork -Name $VNetName1 -ResourceGroupName $RG1
  $subnet1 = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet1
  $gwipconf1 = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GWIPconfName1 `
  -Subnet $subnet1 -PublicIpAddress $gwpip1
  ```
8. Создайте шлюз hello для TestVNet1. На этом шаге создается hello шлюз виртуальной сети для вашего TestVNet1. Для подключений типа VNet-to-VNet необходимо использовать тип VPN RouteBased. Создание шлюза часто занимает 45 минут или более, в зависимости от выбранного шлюза hello SKU.

  ```powershell
  New-AzureRmVirtualNetworkGateway -Name $GWName1 -ResourceGroupName $RG1 `
  -Location $Location1 -IpConfigurations $gwipconf1 -GatewayType Vpn `
  -VpnType RouteBased -GatewaySku VpnGw1
  ```

### <a name="step-3---create-and-configure-testvnet4"></a>Шаг 3. Создание и настройка TestVNet4

После настройки TestVNet1 создайте TestVNet4. Выполните действия hello ниже замена значений hello собственными при необходимости. Этот шаг можно выполнить в hello же сеанс PowerShell, так как он находится в hello же подписки.

1. Объявите переменные. Быть убедиться, что tooreplace hello значениями hello из них требуется toouse для вашей конфигурации.

  ```powershell
  $RG4 = "TestRG4"
  $Location4 = "West US"
  $VnetName4 = "TestVNet4"
  $FESubName4 = "FrontEnd"
  $BESubName4 = "Backend"
  $GWSubName4 = "GatewaySubnet"
  $VnetPrefix41 = "10.41.0.0/16"
  $VnetPrefix42 = "10.42.0.0/16"
  $FESubPrefix4 = "10.41.0.0/24"
  $BESubPrefix4 = "10.42.0.0/24"
  $GWSubPrefix4 = "10.42.255.0/27"
  $GWName4 = "VNet4GW"
  $GWIPName4 = "VNet4GWIP"
  $GWIPconfName4 = "gwipconf4"
  $Connection41 = "VNet4toVNet1"
  ```
2. Создайте новую группу ресурсов.

  ```powershell
  New-AzureRmResourceGroup -Name $RG4 -Location $Location4
  ```
3. Создание конфигурации подсети для TestVNet4 hello.

  ```powershell
  $fesub4 = New-AzureRmVirtualNetworkSubnetConfig -Name $FESubName4 -AddressPrefix $FESubPrefix4
  $besub4 = New-AzureRmVirtualNetworkSubnetConfig -Name $BESubName4 -AddressPrefix $BESubPrefix4
  $gwsub4 = New-AzureRmVirtualNetworkSubnetConfig -Name $GWSubName4 -AddressPrefix $GWSubPrefix4
  ```
4. Создайте TestVNet4.

  ```powershell
  New-AzureRmVirtualNetwork -Name $VnetName4 -ResourceGroupName $RG4 `
  -Location $Location4 -AddressPrefix $VnetPrefix41,$VnetPrefix42 -Subnet $fesub4,$besub4,$gwsub4
  ```
5. Запросите общедоступный IP-адрес.

  ```powershell
  $gwpip4 = New-AzureRmPublicIpAddress -Name $GWIPName4 -ResourceGroupName $RG4 `
  -Location $Location4 -AllocationMethod Dynamic
  ```
6. Создайте конфигурацию шлюза hello.

  ```powershell
  $vnet4 = Get-AzureRmVirtualNetwork -Name $VnetName4 -ResourceGroupName $RG4
  $subnet4 = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet4
  $gwipconf4 = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GWIPconfName4 -Subnet $subnet4 -PublicIpAddress $gwpip4
  ```
7. Создайте шлюз TestVNet4 hello. Создание шлюза часто занимает 45 минут или более, в зависимости от выбранного шлюза hello SKU.

  ```powershell
  New-AzureRmVirtualNetworkGateway -Name $GWName4 -ResourceGroupName $RG4 `
  -Location $Location4 -IpConfigurations $gwipconf4 -GatewayType Vpn `
  -VpnType RouteBased -GatewaySku VpnGw1
  ```

### <a name="step-4---create-hello-connections"></a>Шаг 4 — Создание подключений hello

1. Получите оба шлюза для виртуальных сетей. При выполнении обоих шлюзов hello hello одной подписке, как в примере hello, можно выполнить на этом шаге hello одного сеанса PowerShell.

  ```powershell
  $vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1 -ResourceGroupName $RG1
  $vnet4gw = Get-AzureRmVirtualNetworkGateway -Name $GWName4 -ResourceGroupName $RG4
  ```
2. Создание подключения tooTestVNet4 TestVNet1 hello. На этом этапе можно создать подключение hello TestVNet1 tooTestVNet4. Вы увидите общий ключ, на который ссылается примеры hello. Можно использовать собственные значения для hello общего ключа. Важно, что это общий ключ, hello Hello оба соединения должны совпадать. Создание соединения может занять некоторое время toocomplete.

  ```powershell
  New-AzureRmVirtualNetworkGatewayConnection -Name $Connection14 -ResourceGroupName $RG1 `
  -VirtualNetworkGateway1 $vnet1gw -VirtualNetworkGateway2 $vnet4gw -Location $Location1 `
  -ConnectionType Vnet2Vnet -SharedKey 'AzureA1b2C3'
  ```
3. Создание подключения tooTestVNet1 TestVNet4 hello. Этот шаг является аналогичные toohello показано выше, за исключением того, вы создаете подключение hello из TestVNet4 tooTestVNet1. Убедитесь, что hello общие ключи совпадают. будет установлено подключение Hello через несколько минут.

  ```powershell
  New-AzureRmVirtualNetworkGatewayConnection -Name $Connection41 -ResourceGroupName $RG4 `
  -VirtualNetworkGateway1 $vnet4gw -VirtualNetworkGateway2 $vnet1gw -Location $Location4 `
  -ConnectionType Vnet2Vnet -SharedKey 'AzureA1b2C3'
  ```
4. Проверьте подключение. В разделе hello [как tooverify подключения](#verify).

## <a name="difsub"></a>Как tooconnect виртуальных сетей, находящихся в разных подписках

![Схема подключения между виртуальными сетями](./media/vpn-gateway-vnet-vnet-rm-ps/v2vdiffsub.png)

В этом сценарии мы создадим подключение между TestVNet1 и TestVNet5. TestVNet1 и TestVNet5 находятся в разных подписках. Hello подписки не обязательно toobe, связанный с hello того же клиента Active Directory. Hello эти действия и предыдущий набор hello отличается некоторые шаги настройки hello необходимость toobe выполняется в отдельном сеансе PowerShell, в контексте hello hello второй подписки. Особенно при hello двух подписок принадлежат toodifferent организаций.

### <a name="step-5---create-and-configure-testvnet1"></a>Шаг 5. Создание и настройка TestVNet1

Необходимо выполнить [шаг 1](#Step1) и [шаг 2](#Step2) из hello предыдущей статьи toocreate и настроить TestVNet1 и hello VPN-шлюза для TestVNet1. Для этой конфигурации не требуется toocreate TestVNet4 hello в предыдущем разделе, несмотря на то, что при ее создании, оно не будет конфликтовать с следующие действия. После выполнения шага 1 и 2 шага, выполните шаг 6 toocreate TestVNet5. 

### <a name="step-6---verify-hello-ip-address-ranges"></a>Шаг 6 - проверка hello диапазоны IP-адресов

Это важные toomake в том, что пространство IP-адресов hello hello новой виртуальной сети, TestVNet5, не перекрываются с любым из диапазонов сети VNet или диапазоны шлюза локальной сети. В этом примере hello виртуальных сетей может принадлежать toodifferent организаций. Для этого упражнения можно использовать следующие значения для hello TestVNet5 hello.

**Значения для TestVNet5:**

* Имя виртуальной сети: TestVNet5
* Группа ресурсов: TestRG5
* Расположение: восточная часть Японии
* TestVNet5: 10.51.0.0/16 и 10.52.0.0/16
* FrontEnd: 10.51.0.0/24
* BackEnd: 10.52.0.0/24
* GatewaySubnet: 10.52.255.0.0/27
* Имя шлюза: VNet5GW
* Общедоступный IP-адрес: VNet5GWIP
* Тип VPN: RouteBased
* Подключение: VNet5toVNet1
* Тип подключения: VNet2VNet

### <a name="step-7---create-and-configure-testvnet5"></a>Шаг 7. Создание и настройка TestVNet5

Этот шаг необходимо выполнить в контексте hello hello новую подписку. Эта часть может выполняться Здравствуйте, администратор в другой организации, которой принадлежит подписка hello.

1. Объявите переменные. Быть убедиться, что tooreplace hello значениями hello из них требуется toouse для вашей конфигурации.

  ```powershell
  $Sub5 = "Replace_With_the_New_Subcription_Name"
  $RG5 = "TestRG5"
  $Location5 = "Japan East"
  $VnetName5 = "TestVNet5"
  $FESubName5 = "FrontEnd"
  $BESubName5 = "Backend"
  $GWSubName5 = "GatewaySubnet"
  $VnetPrefix51 = "10.51.0.0/16"
  $VnetPrefix52 = "10.52.0.0/16"
  $FESubPrefix5 = "10.51.0.0/24"
  $BESubPrefix5 = "10.52.0.0/24"
  $GWSubPrefix5 = "10.52.255.0/27"
  $GWName5 = "VNet5GW"
  $GWIPName5 = "VNet5GWIP"
  $GWIPconfName5 = "gwipconf5"
  $Connection51 = "VNet5toVNet1"
  ```
2. Подключите toosubscription 5. Откройте консоль PowerShell и подключить tooyour учетную запись. Используйте следующий пример toohelp подключении hello.

  ```powershell
  Login-AzureRmAccount
  ```

  Проверьте hello подписки для учетной записи hello.

  ```powershell
  Get-AzureRmSubscription
  ```

  Укажите требуемый toouse подписки hello.

  ```powershell
  Select-AzureRmSubscription -SubscriptionName $Sub5
  ```
3. Создайте новую группу ресурсов.

  ```powershell
  New-AzureRmResourceGroup -Name $RG5 -Location $Location5
  ```
4. Создание конфигурации подсети для TestVNet5 hello.

  ```powershell
  $fesub5 = New-AzureRmVirtualNetworkSubnetConfig -Name $FESubName5 -AddressPrefix $FESubPrefix5
  $besub5 = New-AzureRmVirtualNetworkSubnetConfig -Name $BESubName5 -AddressPrefix $BESubPrefix5
  $gwsub5 = New-AzureRmVirtualNetworkSubnetConfig -Name $GWSubName5 -AddressPrefix $GWSubPrefix5
  ```
5. Создайте TestVNet5.

  ```powershell
  New-AzureRmVirtualNetwork -Name $VnetName5 -ResourceGroupName $RG5 -Location $Location5 `
  -AddressPrefix $VnetPrefix51,$VnetPrefix52 -Subnet $fesub5,$besub5,$gwsub5
  ```
6. Запросите общедоступный IP-адрес.

  ```powershell
  $gwpip5 = New-AzureRmPublicIpAddress -Name $GWIPName5 -ResourceGroupName $RG5 `
  -Location $Location5 -AllocationMethod Dynamic
  ```
7. Создайте конфигурацию шлюза hello.

  ```powershell
  $vnet5 = Get-AzureRmVirtualNetwork -Name $VnetName5 -ResourceGroupName $RG5
  $subnet5  = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet5
  $gwipconf5 = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GWIPconfName5 -Subnet $subnet5 -PublicIpAddress $gwpip5
  ```
8. Создайте шлюз TestVNet5 hello.

  ```powershell
  New-AzureRmVirtualNetworkGateway -Name $GWName5 -ResourceGroupName $RG5 -Location $Location5 `
  -IpConfigurations $gwipconf5 -GatewayType Vpn -VpnType RouteBased -GatewaySku VpnGw1
  ```

### <a name="step-8---create-hello-connections"></a>Шаг 8 — Создание подключений hello

В этом примере так как шлюзы hello находятся в разных подписках hello, мы разбить этот шаг двух сеансов PowerShell, помеченный как [подписки 1] и [подписки 5].

1. **[Подписки 1]**  Шлюз виртуальной сети hello get для подписки 1. Вход и подключиться tooSubscription 1 перед запуском hello в следующем примере:

  ```powershell
  $vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1 -ResourceGroupName $RG1
  ```

  Копировать выходные данные hello hello следующие элементы и отправлять эти администратора toohello 5 подписки по электронной почте или другим методом.

  ```powershell
  $vnet1gw.Name
  $vnet1gw.Id
  ```

  Эти два элемента будет иметь примерно toohello значения следующий пример выходных данных:

  ```
  PS D:\> $vnet1gw.Name
  VNet1GW
  PS D:\> $vnet1gw.Id
  /subscriptions/b636ca99-6f88-4df4-a7c3-2f8dc4545509/resourceGroupsTestRG1/providers/Microsoft.Network/virtualNetworkGateways/VNet1GW
  ```
2. **[Подписки 5]**  Шлюз виртуальной сети hello get для 5 подписки. Вход и подключиться tooSubscription 5 перед запуском hello в следующем примере:

  ```powershell
  $vnet5gw = Get-AzureRmVirtualNetworkGateway -Name $GWName5 -ResourceGroupName $RG5
  ```

  Копировать выходные данные hello hello следующие элементы и отправлять эти администратора toohello 1 подписки по электронной почте или другим методом.

  ```powershell
  $vnet5gw.Name
  $vnet5gw.Id
  ```

  Эти два элемента будет иметь примерно toohello значения следующий пример выходных данных:

  ```
  PS C:\> $vnet5gw.Name
  VNet5GW
  PS C:\> $vnet5gw.Id
  /subscriptions/66c8e4f1-ecd6-47ed-9de7-7e530de23994/resourceGroups/TestRG5/providers/Microsoft.Network/virtualNetworkGateways/VNet5GW
  ```
3. **[Подписки 1]**  Создать hello TestVNet1 tooTestVNet5 соединение. На этом этапе можно создать подключение hello TestVNet1 tooTestVNet5. Hello различие — $vnet5gw не удается получить напрямую, так как он находится в другой подписке. Вам потребуется toocreate объекта PowerShell со значениями hello, переданные от подписки 1 в hello описанные выше действия. Используйте hello. пример ниже. Замените собственными значениями hello имя, идентификатор и общего ключа. Важно, что это общий ключ, hello Hello оба соединения должны совпадать. Создание соединения может занять некоторое время toocomplete.

  Перед выполнением следующий пример hello подключите tooSubscription 1:

  ```powershell
  $vnet5gw = New-Object Microsoft.Azure.Commands.Network.Models.PSVirtualNetworkGateway
  $vnet5gw.Name = "VNet5GW"
  $vnet5gw.Id   = "/subscriptions/66c8e4f1-ecd6-47ed-9de7-7e530de23994/resourceGroups/TestRG5/providers/Microsoft.Network/virtualNetworkGateways/VNet5GW"
  $Connection15 = "VNet1toVNet5"
  New-AzureRmVirtualNetworkGatewayConnection -Name $Connection15 -ResourceGroupName $RG1 -VirtualNetworkGateway1 $vnet1gw -VirtualNetworkGateway2 $vnet5gw -Location $Location1 -ConnectionType Vnet2Vnet -SharedKey 'AzureA1b2C3'
  ```
4. **[Подписки 5]**  Создать hello TestVNet5 tooTestVNet1 соединение. Этот шаг является аналогичные toohello показано выше, за исключением того, вы создаете подключение hello из TestVNet5 tooTestVNet1. Hello же процесс создания объекта PowerShell, на основании hello значения, полученные из подписки 1 относится здесь также. На этом шаге убедитесь, что hello общие ключи совпадают.

  Перед выполнением следующий пример hello подключите tooSubscription 5:

  ```powershell
  $vnet1gw = New-Object Microsoft.Azure.Commands.Network.Models.PSVirtualNetworkGateway
  $vnet1gw.Name = "VNet1GW"
  $vnet1gw.Id = "/subscriptions/b636ca99-6f88-4df4-a7c3-2f8dc4545509/resourceGroups/TestRG1/providers/Microsoft.Network/virtualNetworkGateways/VNet1GW "
  New-AzureRmVirtualNetworkGatewayConnection -Name $Connection51 -ResourceGroupName $RG5 -VirtualNetworkGateway1 $vnet5gw -VirtualNetworkGateway2 $vnet1gw -Location $Location5 -ConnectionType Vnet2Vnet -SharedKey 'AzureA1b2C3'
  ```

## <a name="verify"></a>Как tooverify соединение

[!INCLUDE [vpn-gateway-no-nsg-include](../../includes/vpn-gateway-no-nsg-include.md)]

[!INCLUDE [verify connections powershell](../../includes/vpn-gateway-verify-connection-ps-rm-include.md)]

## <a name="faq"></a>Часто задаваемые вопросы о подключениях типа "виртуальная сеть — виртуальная сеть"

[!INCLUDE [vpn-gateway-vnet-vnet-faq](../../includes/vpn-gateway-vnet-vnet-faq-include.md)]

## <a name="next-steps"></a>Дальнейшие действия

* После завершения подключения можно добавить виртуальные машины tooyour виртуальных сетей. В разделе hello [документация по виртуальным машинам](https://docs.microsoft.com/azure/#pivot=services&panel=Compute) для получения дополнительной информации.
* Сведения о BGP см. в разделе hello [Обзор BGP](vpn-gateway-bgp-overview.md) и [как tooconfigure BGP](vpn-gateway-bgp-resource-manager-ps.md).
