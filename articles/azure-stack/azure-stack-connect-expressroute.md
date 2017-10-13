---
title: "Подключиться к Azure с помощью ExpressRoute стек Azure"
description: "Способ подключения виртуальных сетей в Azure стека виртуальных сетей в Azure с помощью ExpressRoute."
services: azure-stack
documentationcenter: 
author: victorar
manager: 
editor: 
ms.assetid: 
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 9/25/2017
ms.author: victorh
ms.openlocfilehash: aa6973939c6cfe0688f5781fdcea5d39670249df
ms.sourcegitcommit: 90e2cced6a773b1b52f999ba73cd8877305d270b
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/13/2017
---
# <a name="connect-azure-stack-to-azure-using-expressroute"></a>Подключиться к Azure с помощью ExpressRoute стек Azure

*Применяется к: стек Azure интегрированных систем и пакет средств разработки стек Azure*

Существует два поддерживаемых методов для подключения к виртуальной сети в Azure виртуальные сети в Azure стека:
   * **Сеть-сеть**

     VPN-подключение по IPsec (IKE v1 и IKE v2). Для этого типа подключения требуется VPN-устройство или RRAS. Дополнительные сведения см. в разделе [подключения стек Azure в Azure с помощью VPN](azure-stack-connect-vpn.md).
   * **ExpressRoute**

     Прямое подключение к Azure из развертывания Azure стека. ExpressRoute — **не** VPN-подключения через общедоступный Интернет. Дополнительные сведения об Azure ExpressRoute см. в разделе [Обзор ExpressRoute](../expressroute/expressroute-introduction.md).

В этой статье показан пример использования ExpressRoute для подключения к Azure Azure стека.
## <a name="requirements"></a>Требования
Ниже приведены особые требования для подключения стек Azure и Azure с помощью ExpressRoute.
* Подписка Azure для создания каналов expressroute и виртуальных сетей в Azure.
* Объект подготовить канал ExpressRoute через [поставщика услуг подключения](../expressroute/expressroute-locations.md).
* Маршрутизатор, который был подключен к его WAN портов канал ExpressRoute.
* Мультитенантный шлюз стек Azure связан стороне маршрутизатора локальной сети.
* Маршрутизатор должен поддерживать через виртуальную Частную сеть для подключений между его интерфейса локальной сети и мультитенантный шлюз Azure стека.
* Если более чем одного клиента добавляется в развертывании Azure стека, маршрутизатор необходима для создания нескольких Vrf (виртуальный маршрутизации и пересылки).

На следующей диаграмме показан концептуальное представление сети после завершения настройки:

![Концептуальная схема](media/azure-stack-connect-expressroute/Conceptual.png)

**На рис. 1**

В примере ниже показан архитектура как несколько клиентов соединиться с инфраструктурой Azure стека через маршрутизатор ExpressRoute Azure на границе Microsoft:

![Схема архитектуры](media/azure-stack-connect-expressroute/Architecture.png)

**Схема 2**

Пример, приведенный в этом разделе использует ту же архитектуру для подключения к Azure через частного пиринга ExpressRoute. Это можно сделать с помощью через виртуальную Частную сеть для подключения через шлюз виртуальной сети Azure стека маршрутизатор ExpressRoute. Следующие шаги в этой статье показано, как создание конца в конец соединения между двумя виртуальных сетей от двух разных клиентов в стек Azure для их соответствующих виртуальных сетей в Azure. Можно добавить как многие клиента виртуальных сетей и реплицировать шаги для каждого клиента или использовать этот пример развертывание только одного клиента виртуальной сети.

## <a name="configure-azure-stack"></a>Настройка стек Azure
Теперь можно создать ресурсов, необходимых для настройки среды Azure стека как клиента. Следующие шаги иллюстрируют, вам нужно. Эти инструкции показано, как создать ресурсы с помощью портала Azure стека, но можно также использовать PowerShell.

![Действия сетевых ресурсов](media/azure-stack-connect-expressroute/image2.png)
### <a name="before-you-begin"></a>Перед началом работы
Перед началом настройки необходимо:
* Развертывания служб Azure стека.

   Сведения о развертывании пакета средств разработки стек Azure см. в разделе [краткое руководство для развертывания пакета средств разработки Azure стека](azure-stack-deploy-overview.md).
* Стек Azure, пользователь может подписаться на предложение.

  Инструкции см. в разделе [доступность виртуальных машин для пользователей Azure стека](azure-stack-tutorial-tenant-vm.md).

### <a name="create-network-resources-in-azure-stack"></a>Создание сетевых ресурсов в стек Azure

Используйте следующие процедуры для создания требуемым сетевым ресурсам в Azure стека для каждого клиента:

#### <a name="create-the-virtual-network-and-vm-subnet"></a>Создание виртуальной сети и подсети виртуальной машины
1. Войдите в портал пользователей с учетной записью пользователя (клиента).

2. На портале щелкните **New**.

   ![](media/azure-stack-connect-expressroute/MAS-new.png)

3. В меню Marketplace выберите **Сети**.

4. В меню щелкните **Виртуальная сеть**.

5. Введите значения в соответствующие поля, используйте следующую таблицу:

   |Поле  |Значение  |
   |---------|---------|
   |Имя     |Tenant1VNet1         |
   |Пространство адресов     |10.1.0.0/16|
   |Имя подсети     |Sub1 клиента (1)|
   |Диапазон адресов подсети     |10.1.1.0/24|

6. В поле **Подписка** должна появиться созданная ранее подписка.

    а. Для группы ресурсов, можно создать группу ресурсов или если это уже сделано, установите **использовать существующие**.

    b. Проверьте значение расположения по умолчанию.

    c. Щелкните **Закрепить на панели мониторинга**.

    d. Щелкните **Создать**.



#### <a name="create-the-gateway-subnet"></a>Создание подсети шлюза
1. Откройте ресурс виртуальной сети, вы создали (Tenant1VNet1) на панели мониторинга.
2. В разделе «Параметры» выберите **подсети**.
3. Щелкните **Подсеть шлюза**, чтобы добавить подсеть шлюза в виртуальную сеть.
   
    ![](media/azure-stack-connect-expressroute/gatewaysubnet.png)
4. Подсети присвоено имя **GatewaySubnet** по умолчанию.
   Подсети шлюза являются специальными, и для правильной работы им должно быть присвоено конкретное имя.
5. В **диапазона адресов** поле, убедитесь, что адрес **10.1.0.0/24**.
6. Нажмите кнопку **ОК**, чтобы создать подсеть шлюза.

#### <a name="create-the-virtual-network-gateway"></a>Создание шлюза виртуальной сети
1. На портале Azure стека пользователя щелкните **New**.
   
2. В меню Marketplace выберите **Сети**.
3. В списке сетевых ресурсов выберите **Шлюз виртуальной сети**.
4. В поле **Имя** введите **GW1**.
5. Щелкните пункт **Виртуальная сеть**, чтобы выбрать виртуальную сеть.
   Выберите **Tenant1VNet1** из списка.
6. Щелкните пункт меню **Общедоступный IP-адрес**. Когда **выберите общедоступный IP-адрес** раздел откроется щелкните **создать новый**.
7. В поле **Имя** введите **GW1-PiP** и нажмите кнопку **ОК**.
8. Для параметра **Тип VPN** должно быть установлено значение **Route-based** (На основе маршрутов) по умолчанию.
    Не изменяйте значение этого параметра.
9. Убедитесь, что для параметров **Подписка** и **Расположение** выбраны правильные значения. Если требуется, вы можете закрепить ресурсов на панель мониторинга. Щелкните **Создать**.

#### <a name="create-the-local-network-gateway"></a>Создание шлюза локальной сети

Ресурс шлюза локальной сети предназначена для указания удаленного шлюза на другом конце VPN-подключение. Например удаленная сторона является подчиненный локальной сети, интерфейс маршрутизатора ExpressRoute. Для клиента 1 в этом примере удаленный адрес — 10.60.3.255, как показано на рис. 2.

1. Войдите в систему физического компьютера Azure Stack.
2. Войдите на пользовательский портал с помощью учетной записи пользователя и нажмите кнопку **New**.
3. В меню Marketplace выберите **Сети**.
4. В списке сетевых ресурсов выберите **шлюз локальной сети**.
5. В **имя** тип поля **ER-маршрутизатор-GW**.
6. Для **IP-адрес** полей см. рис. 2. IP-адрес подчиненный интерфейс локальной сети маршрутизатор ExpressRoute для клиента 1 — 10.60.3.255. Для среды введите IP-адрес маршрутизатора соответствующий интерфейс.
7. В **адресное пространство** введите адресное пространство виртуальных сетей, который требуется подключить к Azure. Для этого примера см. рис. 2. Для клиента 1, обратите внимание, что необходимые подсетей **192.168.2.0/24** (это концентратора виртуальной сети в Azure) и **10.100.0.0/16** (это резервный виртуальной сети в Azure). Введите соответствующие подсети для вашей рабочей среде.
   > [!IMPORTANT]
   > В этом примере предполагается, что вы используете статические маршруты для сеть-сеть VPN-подключение между шлюзом стек Azure и маршрутизатор ExpressRoute.

8. Убедитесь, что ваш **подписки**, **группы ресурсов**, и **расположение** заданы правильно и нажмите кнопку **создать**.

#### <a name="create-the-connection"></a>Создание подключения
1. На портале Azure стека пользователя щелкните **New**.
2. В меню Marketplace выберите **Сети**.
3. В списке сетевых ресурсов выберите **Подключение**.
4. В **основы** разделе "Параметры" выберите **-сайтами (IPSec)** как **тип соединения**.
5. Выберите **подписки**, **группы ресурсов**, и **расположение** и нажмите кнопку **ОК**.
6. В **параметры** щелкните **шлюз виртуальной сети** щелкните **GW1**.
7. Нажмите кнопку **шлюз локальной сети**и нажмите кнопку **ER маршрутизатора GW**.
8. В **имя подключения** введите **ConnectToAzure**.
9. В **общий ключ (PSK)** введите **abc123** и нажмите кнопку **ОК**.
10. На **Сводка** щелкните **ОК**.

    После создания соединения, можно увидеть общедоступный IP-адрес, используемый шлюзом виртуальной сети. Чтобы найти адрес на портале Azure стека, перейдите на шлюз виртуальной сети. В **Обзор**, найти **общедоступный IP-адрес**. Запишите этот адрес; используется в качестве *внутренний IP-адрес* в следующем разделе (если применимо, для развертывания).

    ![](media/azure-stack-connect-expressroute/GWPublicIP.png)

#### <a name="create-a-virtual-machine"></a>Создание виртуальной машины
Для проверки данных, проходящих через VPN-подключение, необходимо, чтобы виртуальные машины для отправки и получения данных в стек виртуальной сети Azure. Теперь создайте виртуальную машину и поместить его в вашей подсети виртуальной Машины в виртуальной сети.

1. На портале Azure стека пользователя щелкните **New**.
2. В меню Marketplace выберите **Виртуальные машины**.
3. В списке образов виртуальных машин, выберите **Eval центра обработки данных Windows Server 2016** образ и нажмите кнопку **создать**.
4. На **основы** раздела **имя** тип поля **VM01**.
5. Введите допустимое имя пользователя и пароль. Эта учетная запись будет использоваться для входа в виртуальную машину после ее создания.
6. Укажите **подписки**, **группы ресурсов**, и **расположение** и нажмите кнопку **ОК**.
7. На **размер** щелкните размер виртуальной машины для этого экземпляра и нажмите кнопку **выберите**.
8. На **параметры** раздела, можно принять значения по умолчанию. Но это гарантирует выбранной виртуальной сети **Tenant1VNet1** и подсети **10.1.1.0/24**. Нажмите кнопку **ОК**.
9. Проверьте параметры на **Сводка** и нажмите кнопку **ОК**.

Для каждого клиента для подключения виртуальной сети, повторите предыдущие шаги из **создать виртуальную сеть и подсеть виртуальной Машины** через **Создание виртуальной машины** разделы.

### <a name="configure-the-nat-virtual-machine-for-gateway-traversal"></a>Настройте виртуальную машину NAT для обхода шлюза
> [!IMPORTANT]
> Этот раздел предназначен для развертывания пакета средств разработки Azure стека только. NAT не требуется для развертываний с несколькими узлами.

Пакет средств разработки Azure стека самодостаточны и изолированы от сети, на котором развернута физического узла. Таким образом не является внешним, шлюзы, подключенные к сети «External» виртуальный IP-адрес, но скрыто за маршрутизатором, выполнив сетевых адресов (NAT).
 
Маршрутизатор — это виртуальная машина Windows Server (**AzS BGPNAT01**) под управлением роли маршрутизации и удаленного доступа (RRAS) в инфраструктуре Azure стека Development Kit. Необходимо настроить NAT на виртуальной машине AzS BGPNAT01, чтобы разрешить VPN-подключения сеть-сеть для подключения на обоих концах.

#### <a name="configure-the-nat"></a>Настройка преобразования сетевых адресов

1. Войдите в Azure стека физического компьютера с учетной записью администратора.
2. Скопируйте и измените следующий сценарий PowerShell и выполните в с повышенными привилегиями Windows PowerShell ISE. Замените пароль администратора. Возвращается адрес вашей *BGPNAT внешний адрес*.

   ```
   cd \AzureStack-Tools-master\connect
   Import-Module .\AzureStack.Connect.psm1
   $Password = ConvertTo-SecureString "<your administrator password>" `
    -AsPlainText `
    -Force
   Get-AzureStackNatServerAddress `
    -HostComputer "azs-bgpnat01" `
    -Password $Password
   ```
4. Настройка преобразования сетевых адресов, скопируйте и измените следующий сценарий PowerShell и выполняются в с повышенными привилегиями Windows PowerShell ISE. Измените скрипт, чтобы заменить *BGPNAT внешний адрес* и *внутренний IP-адрес* (ранее определенных на **создания подключения** раздел).

   На примере диаграммах *BGPNAT внешний адрес* — 10.10.0.62 и *внутренний IP-адрес* — 192.168.102.1.

   ```
   # Designate the external NAT address for the ports that use the IKE authentication.
   Invoke-Command `
    -ComputerName azs-bgpnat01 `
     {Add-NetNatExternalAddress `
      -NatName BGPNAT `
      -IPAddress <External BGPNAT address> `
      -PortStart 499 `
      -PortEnd 501}
   Invoke-Command `
    -ComputerName azs-bgpnat01 `
     {Add-NetNatExternalAddress `
      -NatName BGPNAT `
      -IPAddress <External BGPNAT address> `
      -PortStart 4499 `
      -PortEnd 4501}
   # create a static NAT mapping to map the external address to the Gateway
   # Public IP Address to map the ISAKMP port 500 for PHASE 1 of the IPSEC tunnel
   Invoke-Command `
    -ComputerName azs-bgpnat01 `
     {Add-NetNatStaticMapping `
      -NatName BGPNAT `
      -Protocol UDP `
      -ExternalIPAddress <External BGPNAT address> `
      -InternalIPAddress <Internal IP address> `
      -ExternalPort 500 `
      -InternalPort 500}
   # Finally, configure NAT traversal which uses port 4500 to
   # successfully establish the complete IPSEC tunnel over NAT devices
   Invoke-Command `
    -ComputerName azs-bgpnat01 `
     {Add-NetNatStaticMapping `
      -NatName BGPNAT `
      -Protocol UDP `
      -ExternalIPAddress <External BGPNAT address> `
      -InternalIPAddress <Internal IP address> `
      -ExternalPort 4500 `
      -InternalPort 4500}
   ```

## <a name="configure-azure"></a>Настройка Azure
Теперь, после завершения настройки стека Azure, можно развернуть некоторые ресурсы Azure. На следующей диаграмме показан пример клиента виртуальной сети в Azure. Можно использовать любое имя и схему адресации для виртуальной сети в Azure. Однако диапазон адресов для виртуальных сетей в стеке Azure и Azure должны быть уникальными и не перекрываются.

![Виртуальные сети Azure](media/azure-stack-connect-expressroute/AzureArchitecture.png)

**Схема 3**

Ресурсы, развертываемые в Azure похожи на ресурсы, которые развернуты в стек Azure. Аналогичным образом можно развернуть:
* Виртуальные сети и подсети
* Подсеть шлюза
* шлюз виртуальной сети;
* Соединение
* Канал ExpressRoute

Пример сетевой инфраструктуры Azure настраивается следующим образом:
* Используется стандартный (192.168.2.0/24) звездообразной (10.100.0.0./16) модели виртуальной сети.
* Рабочие нагрузки развертываются в резервный виртуальной сети и канал ExpressRoute подключен к концентратору виртуальной сети.
* Два виртуальных сетей связаны с помощью функции пиринга виртуальной сети.

### <a name="configure-vnets"></a>Настройка виртуальных сетей
1. Войдите на портал Azure, используя свои учетные данные Azure.
2. Создание концентратора виртуальной сети с помощью адресное пространство 192.168.2.0/24. Создание с помощью 192.168.2.0/25 диапазон адресов подсети и добавить подсеть шлюза, используя диапазон адресов 192.168.2.128/27.
3. Создание резервного диапазон адресов виртуальной сети и подсети с помощью 10.100.0.0/16.


Дополнительные сведения о создании виртуальных сетей в Azure см. в разделе [создать виртуальную сеть с несколькими подсетями](../virtual-network/virtual-networks-create-vnet-arm-pportal.md).

### <a name="configure-an-expressroute-circuit"></a>Настроить канал ExpressRoute

1. Изучите необходимые компоненты ExpressRoute в [ExpressRoute необходимые компоненты и контрольный список](../expressroute/expressroute-prerequisites.md).
2. Следуйте указаниям в [Создание и изменение канал ExpressRoute](../expressroute/expressroute-howto-circuit-portal-resource-manager.md) для создания канала ExpressRoute с помощью вашей подписки Azure.
3. С помощью поставщика услуг размещения или поставщика для подготовки к каналу ExpressRoute со своей стороны совместно использовать ключ службы из предыдущего шага.
4. Следуйте указаниям в [создания и изменения пиринга за канал ExpressRoute](../expressroute/expressroute-howto-routing-portal-resource-manager.md) настройка частного пиринга на канал ExpressRoute.

### <a name="create-the-virtual-network-gateway"></a>Создание шлюза виртуальной сети

* Следуйте указаниям в [настроить шлюз виртуальной сети для ExpressRoute с помощью PowerShell](../expressroute/expressroute-howto-add-gateway-resource-manager.md) Создание шлюза виртуальной сети для ExpressRoute в концентраторе виртуальной сети.

### <a name="create-the-connection"></a>Создание подключения

* Чтобы связать с expressroute концентратора виртуальной сети, следуйте инструкциям [подключить виртуальную сеть к каналу ExpressRoute](../expressroute/expressroute-howto-linkvnet-portal-resource-manager.md).

### <a name="peer-the-vnets"></a>Одноранговая виртуальных сетей

* Одноранговая основной и резервный виртуальных сетей с помощью действия, описанные в [создать виртуальную сеть пиринга с помощью портала Azure](../virtual-network/virtual-networks-create-vnetpeering-arm-portal.md). При настройке пиринговой виртуальной сети убедитесь, что выбраны следующие параметры:
   * От концентратора для типа «звезда»: **разрешить транспорте шлюза**
   * Из типа «звезда» к концентратору: **использовать удаленный шлюз**

### <a name="create-a-virtual-machine"></a>Создание виртуальной машины

* Развертывание рабочей нагрузки виртуальных машин в резервный виртуальной сети.

Повторите эти действия для всех дополнительных пользователей виртуальных сетей для подключения в Azure через их соответствующие каналы ExpressRoute.

## <a name="configure-the-router"></a>Настройка маршрутизатора

На следующей диаграмме инфраструктуры в целом можно использовать для задач настройки маршрутизатора ExpressRoute. На этой диаграмме показаны двух клиентов (клиента 1 и 2 клиента) их соответствующих цепи Express Route. Каждый связанный для своих собственных VRF (виртуальный маршрутизации и пересылки) в локальной и глобальной сети на стороне ExpressRoute маршрутизатора, чтобы обеспечить изоляцию конца в конец между двух клиентов. Обратите внимание, IP-адреса, используемые в интерфейсах маршрутизатора, как выполните пример конфигурации.

![Полнофункциональный схемы](media/azure-stack-connect-expressroute/EndToEnd.png)

**На рис. 4**

Можно использовать любой маршрутизатор, который поддерживает IKEv2 VPN и BGP разорвать соединение через виртуальную Частную сеть для из стека Azure. Тому же маршрутизатору используется для подключения к Azure, используя канал ExpressRoute. 

Ниже приведен пример конфигурации из 1000 Cisco ASR, который поддерживает инфраструктуру сети, показанный на диаграмме. 4.

```
ip vrf Tenant 1
 description Routing Domain for PRIVATE peering to Azure for Tenant 1
 rd 1:1
!
ip vrf Tenant 2
 description Routing Domain for PRIVATE peering to Azure for Tenant 2
 rd 1:5
!
crypto ikev2 proposal V2-PROPOSAL2 
description IKEv2 proposal for Tenant 1 
encryption aes-cbc-256
 integrity sha256
 group 2
crypto ikev2 proposal V4-PROPOSAL2 
description IKEv2 proposal for Tenant 2 
encryption aes-cbc-256
 integrity sha256
 group 2
!
crypto ikev2 policy V2-POLICY2 
description IKEv2 Policy for Tenant 1 
match fvrf Tenant 1
 match address local 10.60.3.255
 proposal V2-PROPOSAL2
description IKEv2 Policy for Tenant 2
crypto ikev2 policy V4-POLICY2 
 match fvrf Tenant 2
 match address local 10.60.3.251
 proposal V4-PROPOSAL2
!
crypto ikev2 profile V2-PROFILE
description IKEv2 profile for Tenant 1 
match fvrf Tenant 1
 match address local 10.60.3.255
 match identity remote any
 authentication remote pre-share key abc123
 authentication local pre-share key abc123
 ivrf Tenant 1
!
crypto ikev2 profile V4-PROFILE
description IKEv2 profile for Tenant 2
 match fvrf Tenant 2
 match address local 10.60.3.251
 match identity remote any
 authentication remote pre-share key abc123
 authentication local pre-share key abc123
 ivrf Tenant 2
!
crypto ipsec transform-set V2-TRANSFORM2 esp-gcm 256 
 mode tunnel
crypto ipsec transform-set V4-TRANSFORM2 esp-gcm 256 
 mode tunnel
!
crypto ipsec profile V2-PROFILE
 set transform-set V2-TRANSFORM2 
 set ikev2-profile V2-PROFILE
!
crypto ipsec profile V4-PROFILE
 set transform-set V4-TRANSFORM2 
 set ikev2-profile V4-PROFILE
!
interface Tunnel10
description S2S VPN Tunnel for Tenant 1
 ip vrf forwarding Tenant 1
 ip address 11.0.0.2 255.255.255.252
 ip tcp adjust-mss 1350
 tunnel source TenGigabitEthernet0/1/0.211
 tunnel mode ipsec ipv4
 tunnel destination 10.10.0.62
 tunnel vrf Tenant 1
 tunnel protection ipsec profile V2-PROFILE
!
interface Tunnel20
description S2S VPN Tunnel for Tenant 2
 ip vrf forwarding Tenant 2
 ip address 11.0.0.2 255.255.255.252
 ip tcp adjust-mss 1350
 tunnel source TenGigabitEthernet0/1/0.213
 tunnel mode ipsec ipv4
 tunnel destination 10.10.0.62
 tunnel vrf VNET3
 tunnel protection ipsec profile V4-PROFILE
!
interface GigabitEthernet0/0/1
 description PRIMARY Express Route Link to AZURE over Equinix
 no ip address
 negotiation auto
!
interface GigabitEthernet0/0/1.100
description Primary WAN interface of Tenant 1
 description PRIMARY ER link supporting Tenant 1 to Azure
 encapsulation dot1Q 101
 ip vrf forwarding Tenant 1
 ip address 192.168.1.1 255.255.255.252
!
interface GigabitEthernet0/0/1.102
description Primary WAN interface of Tenant 2
 description PRIMARY ER link supporting Tenant 2 to Azure
 encapsulation dot1Q 102
 ip vrf forwarding Tenant 2
 ip address 192.168.1.17 255.255.255.252
!
interface GigabitEthernet0/0/2
 description BACKUP Express Route Link to AZURE over Equinix
 no ip address
 negotiation auto
!
interface GigabitEthernet0/0/2.100
description Secondary WAN interface of Tenant 1
 description BACKUP ER link supporting Tenant 1 to Azure
 encapsulation dot1Q 101
 ip vrf forwarding Tenant 1
 ip address 192.168.1.5 255.255.255.252
!
interface GigabitEthernet0/0/2.102
description Secondary WAN interface of Tenant 2 
description BACKUP ER link supporting Tenant 2 to Azure
 encapsulation dot1Q 102
 ip vrf forwarding Tenant 2
 ip address 192.168.1.21 255.255.255.252
!
interface TenGigabitEthernet0/1/0
 description Downlink to ---Port 1/47
 no ip address
!
interface TenGigabitEthernet0/1/0.211
 description LAN interface of Tenant 1
description Downlink to --- Port 1/47.211
 encapsulation dot1Q 211
 ip vrf forwarding Tenant 1
 ip address 10.60.3.255 255.255.255.254
!
interface TenGigabitEthernet0/1/0.213
description LAN interface of Tenant 2
 description Downlink to --- Port 1/47.213
 encapsulation dot1Q 213
 ip vrf forwarding Tenant 2
 ip address 10.60.3.251 255.255.255.254
!
router bgp 65530
 bgp router-id <removed>
 bgp log-neighbor-changes
 description BGP neighbor config and route advertisement for Tenant 1 VRF 
 address-family ipv4 vrf Tenant 1
  network 10.1.0.0 mask 255.255.0.0
  network 10.60.3.254 mask 255.255.255.254
  network 192.168.1.0 mask 255.255.255.252
  network 192.168.1.4 mask 255.255.255.252
  neighbor 10.10.0.62 remote-as 65100
  neighbor 10.10.0.62 description VPN-BGP-PEER-for-Tenant 1
  neighbor 10.10.0.62 ebgp-multihop 5
  neighbor 10.10.0.62 activate
  neighbor 10.60.3.254 remote-as 4232570301
  neighbor 10.60.3.254 description LAN peer for CPEC:INET:2112 VRF
  neighbor 10.60.3.254 activate
  neighbor 10.60.3.254 route-map BLOCK-ALL out
  neighbor 192.168.1.2 remote-as 12076
  neighbor 192.168.1.2 description PRIMARY ER peer for Tenant 1 to Azure
  neighbor 192.168.1.2 ebgp-multihop 5
  neighbor 192.168.1.2 activate
  neighbor 192.168.1.2 soft-reconfiguration inbound
  neighbor 192.168.1.2 route-map Tenant 1-ONLY out
  neighbor 192.168.1.6 remote-as 12076
  neighbor 192.168.1.6 description BACKUP ER peer for Tenant 1 to Azure
  neighbor 192.168.1.6 ebgp-multihop 5
  neighbor 192.168.1.6 activate
  neighbor 192.168.1.6 soft-reconfiguration inbound
  neighbor 192.168.1.6 route-map Tenant 1-ONLY out
  maximum-paths 8
 exit-address-family
 !
description BGP neighbor config and route advertisement for Tenant 2 VRF 
address-family ipv4 vrf Tenant 2
  network 10.1.0.0 mask 255.255.0.0
  network 10.60.3.250 mask 255.255.255.254
  network 192.168.1.16 mask 255.255.255.252
  network 192.168.1.20 mask 255.255.255.252
  neighbor 10.10.0.62 remote-as 65300
  neighbor 10.10.0.62 description VPN-BGP-PEER-for-Tenant 2
  neighbor 10.10.0.62 ebgp-multihop 5
  neighbor 10.10.0.62 activate
  neighbor 10.60.3.250 remote-as 4232570301
  neighbor 10.60.3.250 description LAN peer for CPEC:INET:2112 VRF
  neighbor 10.60.3.250 activate
  neighbor 10.60.3.250 route-map BLOCK-ALL out
  neighbor 192.168.1.18 remote-as 12076
  neighbor 192.168.1.18 description PRIMARY ER peer for Tenant 2 to Azure
  neighbor 192.168.1.18 ebgp-multihop 5
  neighbor 192.168.1.18 activate
  neighbor 192.168.1.18 soft-reconfiguration inbound
  neighbor 192.168.1.18 route-map VNET-ONLY out
  neighbor 192.168.1.22 remote-as 12076
  neighbor 192.168.1.22 description BACKUP ER peer for Tenant 2 to Azure
  neighbor 192.168.1.22 ebgp-multihop 5
  neighbor 192.168.1.22 activate
  neighbor 192.168.1.22 soft-reconfiguration inbound
  neighbor 192.168.1.22 route-map VNET-ONLY out
  maximum-paths 8
 exit-address-family
!
ip forward-protocol nd
!
ip as-path access-list 1 permit ^$
ip route vrf Tenant 1 10.1.0.0 255.255.0.0 Tunnel10
ip route vrf Tenant 2 10.1.0.0 255.255.0.0 Tunnel20
!
ip prefix-list BLOCK-ALL seq 5 deny 0.0.0.0/0 le 32
!
route-map BLOCK-ALL permit 10
 match ip address prefix-list BLOCK-ALL
!
route-map VNET-ONLY permit 10
 match as-path 1
!
```

## <a name="test-the-connection"></a>Проверка подключения

Проверьте подключение после установления подключения сеть-сеть и канал ExpressRoute. Эта задача является простой.  Выполните вход на одной из виртуальных машин, созданных в виртуальной сети Azure и проверить связь с виртуальной машины, созданной в среде Azure стека, или наоборот. 

Чтобы убедиться, что при отправке трафика через сеть-сеть и подключения ExpressRoute, необходимо проверить связь выделенный адрес IP-адрес (DIP) виртуальной машины на концах одновременно, а не адрес виртуального IP-адреса виртуальной машины. Таким образом необходимо найти и запишите адрес, на другой стороне соединения.

### <a name="allow-icmp-in-through-the-firewall"></a>Разрешить ICMP в через брандмауэр
По умолчанию Windows Server 2016 не разрешают ICMP-пакеты через брандмауэр. Таким образом для каждой виртуальной машины, используемого в тест, в окне PowerShell с повышенными привилегиями выполните следующий командлет:


   ```
   New-NetFirewallRule `
    –DisplayName “Allow ICMPv4-In” `
    –Protocol ICMPv4
   ```

### <a name="ping-the-azure-stack-virtual-machine"></a>Проверить связь с виртуальной машины Azure стека

1. Войдите на пользовательский портал Azure стека с помощью учетной записи клиента.
2. В области навигации слева щелкните **Виртуальные машины**.
3. Найти ранее созданную виртуальную машину и щелкните его.
4. В разделе для виртуальной машины, нажмите кнопку **Connect**.
5. Откройте PowerShell с повышенными правами окно и введите **ipconfig/all**.
6. Найти адрес IPv4 в выходных данных и запишите его. Проверьте связь этого адреса из виртуальной машины в виртуальной сети Azure. В среде примере адрес является из подсети 10.1.1.x/24. В вашей среде адресе может отличаться. Тем не менее следует в подсети, созданной для подсети виртуальной сети клиента.


### <a name="view-data-transfer-statistics"></a>Просмотр статистики передачи данных

Если вы хотите знать, какой объем трафика передается через подключение к, можно найти эти сведения в разделе "подключения" в пользовательском портале Azure стека. Эти сведения также является хороший способ проверить, что ping, который вы только что отправлен на самом деле пошло через подключения VPN и ExpressRoute.

1. Войдите на пользовательский портал стека Microsoft Azure с помощью учетной записи клиента.
2. Перейдите к группе ресурсов, в которой был создан шлюза VPN и выберите **подключений** тип объекта.
3. Нажмите кнопку **ConnectToAzure** подключение в списке.
4. На **подключения** можно просмотреть статистику для **данные в** и **исходящие данные**. Там будут отображаться ненулевые значения.

   ![Данные в исходящие данные](media/azure-stack-connect-expressroute/DataInDataOut.png)

## <a name="next-steps"></a>Дальнейшие действия
[Развертывание приложений для Azure и Azure стека](azure-stack-solution-pipeline.md)