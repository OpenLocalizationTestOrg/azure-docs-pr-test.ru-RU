---
title: "aaaTroubleshoot Сетевые группы безопасности - PowerShell | Документы Microsoft"
description: "Узнайте, как tootroubleshoot сетевых групп безопасности в развертывании диспетчера ресурсов Azure hello модели с помощью Azure PowerShell."
services: virtual-network
documentationcenter: na
author: AnithaAdusumilli
manager: narayan
editor: 
tags: azure-resource-manager
ms.assetid: 4c732bb7-5cb1-40af-9e6d-a2a307c2a9c4
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 09/23/2016
ms.author: anithaa
ms.openlocfilehash: 95fd60fa72cf6d17fa990e3c3eb7d980878f7c15
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-network-security-groups-using-azure-powershell"></a>Устранение неполадок, связанных с группами безопасности сети, с помощью PowerShell
> [!div class="op_single_selector"]
> * [Портал Azure](virtual-network-nsg-troubleshoot-portal.md)
> * [PowerShell](virtual-network-nsg-troubleshoot-powershell.md)
> 
> 

Если вы настроили группы безопасности сети (Nsg) на виртуальной машине (VM) и возникают проблемы с подключением виртуальных Машин, в этой статье Обзор возможностей диагностики для Nsg toohelp дополнительную диагностику.

Группы Nsg позволяют toocontrol hello типов трафика этого потока и из нее виртуальные машины (VM). Nsg может быть применен toosubnets в виртуальной сети Azure (VNet) и сетевых интерфейсов (NIC). Hello действующие правила, применяемые tooa сетевого Адаптера являются агрегата hello правил, которые существуют в hello Nsg применяется tooa сетевого Адаптера и hello подсети, в которой он подключен. Правила в этих NSG иногда конфликтуют друг с другом и влияют на возможность сетевого подключения к виртуальной машине.  

Можно просмотреть все правила hello эффективной защиты от Nsg, применения сетевых адаптеров Виртуальной машины. В этой статье показано, как с помощью этих правил в ВМ неполадок tootroubleshoot hello модели развертывания диспетчера ресурсов Azure. Если вы не знакомы с основными понятиями виртуальной сети и NSG, прочтите hello [виртуальная сеть](virtual-networks-overview.md) и [сетевых групп безопасности](virtual-networks-nsg.md) Обзор статей.

## <a name="using-effective-security-rules-tootroubleshoot-vm-traffic-flow"></a>С помощью поток трафика виртуальных Машин tootroubleshoot действующие правила безопасности
Hello сценарий, который следует за примером может служить распространенная проблема подключения:

Виртуальная машина с именем *VM1* принадлежит к подсети *Subnet1* в виртуальной сети *WestUS-VNet1*. Попытка tooconnect toohello виртуальную Машину с помощью протокола удаленного рабочего СТОЛА через TCP-порт 3389 завершается ошибкой. Nsg применяются на обеих hello Сетевых *VM1 NIC1* и hello подсети *подсети1*. Трафик tooTCP порт 3389 допускается в hello NSG, связанный с сетевым интерфейсом hello *VM1 NIC1*, однако в tooVM1 порт 3389 сбой проверить связь с TCP.

Здравствуйте, хотя в этом примере используется TCP-порт 3389, следующие действия можно используется toodetermine сбоев входящие и исходящие подключения через любой порт.

## <a name="detailed-troubleshooting-steps"></a>Подробные инструкции по устранению неполадок
Выполните следующие шаги tootroubleshoot Nsg для виртуальной Машины hello.

1. Запуск сеанса и имени входа tooAzure Azure PowerShell. Если вы не знакомы с использованием Azure PowerShell, прочтите hello [как tooinstall и настройка Azure PowerShell](/powershell/azure/overview) статьи.
2. Введите следующую команду, tooreturn все правила NSG применяется tooa сетевого Адаптера с именем hello *VM1 NIC1* в группе ресурсов hello *RG1*:
   
        Get-AzureRmEffectiveNetworkSecurityGroup -NetworkInterfaceName VM1-NIC1 -ResourceGroupName RG1
   
   > [!TIP]
   > Если вы не знаете имя hello сетевой карты, введите hello, следующая команда tooretrieve hello имена всех сетевых адаптеров в группе ресурсов: 
   > 
   > `Get-AzureRmNetworkInterface -ResourceGroupName RG1 | Format-Table Name`
   > 
   > 
   
    Hello ниже приведен образец hello действующие правила данные, возвращаемые для hello *VM1 NIC1* сетевого Адаптера:
   
        NetworkSecurityGroup   : {
                                   "Id": "/subscriptions/[Subscription ID]/resourceGroups/RG1/providers/Microsoft.Network/networkSecurityGroups/VM1-NIC1-NSG"
                                 }
        Association            : {
                                   "NetworkInterface": {
                                     "Id": "/subscriptions/[Subscription ID]/resourceGroups/RG1/providers/Microsoft.Network/networkInterfaces/VM1-NIC1"
                                   }
                                 }
        EffectiveSecurityRules : [
                                 {
                                 "Name": "securityRules/allowRDP",
                                 "Protocol": "Tcp",
                                 "SourcePortRange": "0-65535",
                                 "DestinationPortRange": "3389-3389",
                                 "SourceAddressPrefix": "Internet",
                                 "DestinationAddressPrefix": "0.0.0.0/0",
                                 "ExpandedSourceAddressPrefix": [… ],
                                 "ExpandedDestinationAddressPrefix": [],
                                 "Access": "Allow",
                                 "Priority": 1000,
                                 "Direction": "Inbound"
                                 },
                                 {
                                 "Name": "defaultSecurityRules/AllowVnetInBound",
                                 "Protocol": "All",
                                 "SourcePortRange": "0-65535",
                                 "DestinationPortRange": "0-65535",
                                 "SourceAddressPrefix": "VirtualNetwork",
                                 "DestinationAddressPrefix": "VirtualNetwork",
                                 "ExpandedSourceAddressPrefix": [
                                  "10.9.0.0/16",
                                  "168.63.129.16/32",
                                  "10.0.0.0/16",
                                  "10.1.0.0/16"
                                  ],
                                 "ExpandedDestinationAddressPrefix": [
                                  "10.9.0.0/16",
                                  "168.63.129.16/32",
                                  "10.0.0.0/16",
                                  "10.1.0.0/16"
                                  ],
                                  "Access": "Allow",
                                  "Priority": 65000,
                                  "Direction": "Inbound"
                                  },…
                         ]
   
        NetworkSecurityGroup   : {
                                   "Id": 
                                 "/subscriptions/[Subscription ID]/resourceGroups/RG1/providers/Microsoft.Network/networkSecurityGroups/Subnet1-NSG"
                                 }
        Association            : {
                                   "Subnet": {
                                     "Id": 
                                 "/subscriptions/[Subscription ID]/resourceGroups/RG1/providers/Microsoft.Network/virtualNetworks/WestUS-VNet1/subnets/Subnet1"
                                 }
                                 }
        EffectiveSecurityRules : [
                                 {
                                "Name": "securityRules/denyRDP",
                                "Protocol": "Tcp",
                                "SourcePortRange": "0-65535",
                                "DestinationPortRange": "3389-3389",
                                "SourceAddressPrefix": "Internet",
                                "DestinationAddressPrefix": "0.0.0.0/0",
                                "ExpandedSourceAddressPrefix": [
                                   ... ],
                                "ExpandedDestinationAddressPrefix": [],
                                "Access": "Deny",
                                "Priority": 1000,
                                "Direction": "Inbound"
                                },
                                {
                                "Name": "defaultSecurityRules/AllowVnetInBound",
                                "Protocol": "All",
                                "SourcePortRange": "0-65535",
                                "DestinationPortRange": "0-65535",
                                "SourceAddressPrefix": "VirtualNetwork",
                                "DestinationAddressPrefix": "VirtualNetwork",
                                "ExpandedSourceAddressPrefix": [
                                "10.9.0.0/16",
                                "168.63.129.16/32",
                                "10.0.0.0/16",
                                "10.1.0.0/16"
                                ],
                                "ExpandedDestinationAddressPrefix": [
                                "10.9.0.0/16",
                                "168.63.129.16/32",
                                "10.0.0.0/16",
                                "10.1.0.0/16"
                                ],
                                "Access": "Allow",
                                "Priority": 65000,
                                "Direction": "Inbound"
                                },...
                                ]
   
    Обратите внимание следующую информацию в выходных данных hello hello.
   
   * Существует два раздела **NetworkSecurityGroup**: один для подсети (*Subnet1*), а другой для сетевого интерфейса (*VM1-NIC1*). В этом примере NSG был применен tooeach.
   * **Ассоциация** показывает hello ресурсов (подсети или сетевого Адаптера) заданного NSG связана с. Если hello NSG ресурс перемещен часовым непосредственно перед выполнением этой команды, может потребоваться toowait через несколько секунд для hello tooreflect изменение в выходных данных команды hello. 
   * имена правил, которые начинаются с Привет *defaultSecurityRules*: создается при NSG, несколько правил безопасности по умолчанию создаются внутри него. Правила по умолчанию нельзя удалить, но они могут быть переопределены правилами с более высоким приоритетом.
     Чтение hello [NSG Обзор](virtual-networks-nsg.md#default-rules) toolearn статьи о NSG по умолчанию правила безопасности.
   * **ExpandedAddressPrefix** расширяет hello префиксы адресов для тегов по умолчанию NSG. Каждый тег обозначает несколько префиксов адресов. Расширения hello тегов можно использовать при устранении неполадок подключения к виртуальной Машине из конкретного адреса префиксы. Например, тег VIRTUAL_NETWORK с пиринг виртуальной сети, расширяется tooshow одноранговыми префиксы виртуальной сети в предыдущие hello выходные данные.
     
     > [!NOTE]
     > Здравствуйте команды только показаны действующие правила, если NSG связана с подсетью, сетевой Адаптер или оба. Виртуальная машина может иметь несколько сетевых интерфейсов, для которых применяются разные NSG. При устранении неполадок, выполните команду hello для каждого сетевого адаптера.
     > 
     > 
3. Фильтрация по большего количества правила NSG tooease введите следующие команды tootroubleshoot дальнейшей hello: 
   
        $NSGs = Get-AzureRmEffectiveNetworkSecurityGroup -NetworkInterfaceName VM1-NIC1 -ResourceGroupName RG1
        $NSGs.EffectiveSecurityRules | Sort-Object Direction, Access, Priority | Out-GridView
   
    Фильтр для трафика RDP (TCP-порт 3389), применены toohello представление сетки, как показано в следующий рисунок hello:
   
    ![Список правил](./media/virtual-network-nsg-troubleshoot-powershell/rules.png)
4. Как видно в представлении сетки hello, существуют оба разрешающих и запрещающих правил для протокола удаленного рабочего СТОЛА. Hello вывода из шага 2 показывает, что hello *DenyRDP* правило находится в подсети toohello NSG применяется hello. Для входящих правил сначала обрабатываются Nsg применяется toohello подсети. Если соответствие найдено, hello NSG применяется toohello сетевого интерфейса не обрабатывается. В этом случае hello *DenyRDP* правило из подсети hello блокирует toohello протокола удаленного рабочего СТОЛА виртуальной Машины (**VM1**).
   
   > [!NOTE]
   > Виртуальная машина может иметь несколько сетевых адаптеров, подключенных tooit. Каждый может быть подключенным tooa другой подсети. Поскольку команды hello в предыдущих шагах hello выполняются сетевой Адаптер, важно tooensure, указываемое hello возникают hello к сбою подключения к сетевой Адаптер. Если вы не знаете, можно всегда выполнить hello команды для каждого сетевого Адаптера, подключенного toohello виртуальной Машины.
   > 
   > 
5. tooRDP в VM1 изменение hello *запретить RDP (3389)* правила слишком*Разрешить RDP(3389)* в hello **подсети1 NSG** NSG. Убедитесь, что TCP-порт 3389 открыт путем открытия RDP соединение toohello ВМ или с помощью средства PsPing hello. Дополнительные сведения о PsPing при чтении hello [PsPing загрузки страницы](https://technet.microsoft.com/sysinternals/psping.aspx)
   
    Можно или удалить правила из NSG с помощью hello сведения в выходных данных hello hello следующую команду:
   
        Get-Help *-AzureRmNetworkSecurityRuleConfig

## <a name="considerations"></a>Рекомендации
Примите во внимание следующие точки, при устранении неполадок подключения hello.

* Правила NSG по умолчанию будет блокировать входящий доступ из hello Интернета и только разрешения виртуальной сети для входящего трафика. Правила должны быть явно добавлены tooallow входящий доступ из Интернета, при необходимости.
* Если нет правил безопасности NSG вызывает toofail подключения к сети Виртуальной машины, hello возможно, из-за:
  * Программный брандмауэр в операционной системе виртуальной Машины hello
  * Маршруты, настроенные для виртуальных устройств или локального трафика. Интернет-трафик может быть перенаправленный tooon организациями через Принудительное туннелирование. Этот параметр, в зависимости от того, как hello в локальной сети оборудования обрабатывает трафик RDP/SSH-подключения из Интернета hello tooyour виртуальной Машины будут недоступны. Чтение hello [Устранение неполадок маршруты](virtual-network-routes-troubleshoot-powershell.md) статьи toolearn toodiagnose маршрут проблемы, которые могут не задерживают hello поток трафика в и из hello виртуальной Машины. 
* Если одноранговыми виртуальных сетей, по умолчанию, hello VIRTUAL_NETWORK тег автоматически расширяет tooinclude префиксы для одноранговыми виртуальных сетей. Можно просмотреть эти префиксы в hello **ExpandedAddressPrefix** список, tootroubleshoot любые проблемы связанные tooVNet пиринг подключения. 
* Правила безопасности отображаются, только если имеется NSG, связанный с виртуальной Машины hello сетевой Адаптер и или подсети. 
* Если Nsg, не связанные с hello сетевого Адаптера или подсети и имеется открытый IP-адрес, назначенный tooyour виртуальной Машины, все порты будут открыты для входящего и исходящего доступа. Если виртуальная машина hello общедоступный IP-адрес, применение toohello Nsg сетевой Адаптер или подсети настоятельно рекомендуется.  

