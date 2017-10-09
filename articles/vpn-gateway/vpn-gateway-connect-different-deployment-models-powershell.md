---
title: "Подключение tooAzure классических виртуальных сетей виртуальных сетей диспетчера ресурсов: PowerShell | Документы Microsoft"
description: "Узнайте, как toocreate VPN-подключение между классических виртуальных сетей и виртуальных сетей диспетчера ресурсов с помощью VPN-шлюза и PowerShell"
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager
ms.assetid: f17c3bf0-5cc9-4629-9928-1b72d0c9340b
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/21/2017
ms.author: cherylmc
ms.openlocfilehash: 8b1cf6ae4becf1829fa99961c5dd09a422fcc1fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="connect-virtual-networks-from-different-deployment-models-using-powershell"></a>Подключение виртуальных сетей из различных моделей развертывания с использованием PowerShell



В этой статье показано, как tooconnect классических виртуальных сетей tooResource tooallow диспетчер виртуальных сетей hello ресурсам, расположенным в hello отдельное развертывание моделей toocommunicate друг с другом. Hello действия, описанные в этой статье с помощью PowerShell, но можно также создать этой конфигурации с помощью портала Azure hello, выбрав статьи hello из этого списка.

> [!div class="op_single_selector"]
> * [Портал](vpn-gateway-connect-different-deployment-models-portal.md)
> * [PowerShell](vpn-gateway-connect-different-deployment-models-powershell.md)
> 
> 

Подключение классический tooa виртуальной сети VNet диспетчера ресурсов выполняется аналогично tooconnecting локального сайта виртуальной сети tooan расположения. Оба типа подключения используйте tooprovide шлюза VPN защищенный туннель, с помощью IPsec/IKE. Подключение можно создать между виртуальными сетями, которые находятся в разных подписках и разных регионах. Можно также подключиться, которые уже есть подключения tooon локальные сети, при условии, что шлюз hello, они были настроены: динамический или на основе маршрутов. Дополнительные сведения о подключениях к виртуальной сети для виртуальной сети см. в разделе hello [часто задаваемые вопросы о виртуальной сети для виртуальной сети](#faq) конце hello в этой статье. 

Если ваш виртуальных сетей в hello совпадают, вы можете tooinstead необходимо учитывать их с помощью Пиринг виртуальной сети. При пиринговой связи между виртуальными сетями VPN-шлюз не используется. Дополнительную информацию см. в статье [Пиринговая связь между виртуальными сетями](../virtual-network/virtual-network-peering-overview.md). 

## <a name="before-beginning"></a>Подготовка

Hello следующее пошаговыми руководствами tooconfigure необходимые параметры hello динамические или на основе маршрутов шлюза для каждой виртуальной сети и создания VPN-подключений между шлюзами hello. Эта конфигурация не поддерживает статические шлюзы и шлюзы на основе политик.

### <a name="prerequisites"></a>Предварительные требования

* Обе виртуальные сети уже созданы.
* Hello диапазоны адресов для hello виртуальных сетей не перекрываются друг с другом или перекрываться с любым hello диапазонов для других соединений, hello шлюзов могут быть подключены.
* Установлены новые командлеты PowerShell hello. В разделе [как tooinstall и настройка Azure PowerShell](/powershell/azure/overview) для получения дополнительной информации. Убедитесь в том, что при установке службы управления (SM) hello и hello командлеты диспетчера ресурсов (RM). 

### <a name="exampleref"></a>Примеры настроек

Можно использовать эти значения toocreate тестовой среде, или ссылаться toothem toobetter понять hello примеры в этой статье.

**Параметры классической виртуальной сети**

Имя виртуальной сети = ClassicVNet <br>
Расположение: Западная часть США <br>
Адресные пространства виртуальной сети = 10.0.0.0/24 <br>
Подсеть-1 = 10.0.0.0/27 <br>
Шлюз подсети = 10.0.0.32/29 <br>
Имя локальной сети = RMVNetLocal <br>
Тип шлюза = DynamicRouting

**Параметры виртуальной сети Resource Manager**

Имя виртуальной сети = RMVNet <br>
Группа ресурсов = RG1 <br>
Адресные пространства виртуальной сети = 192.168.0.0/16 <br>
Подсеть-1 = 192.168.1.0/24 <br>
Шлюз подсети = 192.168.0.0/26 <br>
Расположение = восточная часть США <br>
Общедоступное IP-имя шлюза: gwpip <br>
Шлюз локальной сети = ClassicVNetLocal <br>
Имя шлюза виртуальной сети = RMGateway <br>
Конфигурация IP-адресации шлюза = gwipconfig

## <a name="createsmgw"></a>Раздел 1 — Настройка hello классической виртуальной сети
### <a name="part-1---download-your-network-configuration-file"></a>Часть 1. Скачивание файла конфигурации сети
1. Войдите в tooyour учетной записи Azure в hello консоли PowerShell с повышенными правами. Hello следующий командлет запросит hello учетные данные входа для учетной записи Azure. После входа в систему, он загружает параметры учетной записи, чтобы они были доступны tooAzure PowerShell. Используйте hello toocomplete командлеты SM PowerShell этой части конфигурации hello.

  ```powershell
  Add-AzureAccount
  ```
2. Экспортируйте файл конфигурации сети Azure, выполнив следующую команду hello. Можно изменить расположение hello hello tooexport tooa различные расположения файла при необходимости.

  ```powershell
  Get-AzureVNetConfig -ExportToFile C:\AzureNet\NetworkConfig.xml
  ```
3. Привет открыть XML-файл, загруженный tooedit его. Пример файла конфигурации сети hello разделе hello [схема конфигурации сети](https://msdn.microsoft.com/library/jj157100.aspx).

### <a name="part-2--verify-hello-gateway-subnet"></a>Часть 2 - Проверьте hello подсеть шлюза
В hello **VirtualNetworkSites** элемента, добавьте tooyour подсети шлюза виртуальной сети, если оно еще не создано. При работе с файлом конфигурации сети hello hello подсеть шлюза должен называться «GatewaySubnet» или Azure не удается распознать и использовать его как подсеть шлюза.

[!INCLUDE [vpn-gateway-no-nsg-include](../../includes/vpn-gateway-no-nsg-include.md)]

**Пример**

    <VirtualNetworkSites>
      <VirtualNetworkSite name="ClassicVNet" Location="West US">
        <AddressSpace>
          <AddressPrefix>10.0.0.0/24</AddressPrefix>
        </AddressSpace>
        <Subnets>
          <Subnet name="Subnet-1">
            <AddressPrefix>10.0.0.0/27</AddressPrefix>
          </Subnet>
          <Subnet name="GatewaySubnet">
            <AddressPrefix>10.0.0.32/29</AddressPrefix>
          </Subnet>
        </Subnets>
      </VirtualNetworkSite>
    </VirtualNetworkSites>

### <a name="part-3---add-hello-local-network-site"></a>Часть 3 — Добавление hello сайта локальной сети
Hello сайта локальной сети, добавляемые представляет hello требуется tooconnect toowhich RM виртуальной сети. Добавить **LocalNetworkSites** файл toohello элемента, если она еще не создана. На этом этапе в конфигурации hello hello VPNGatewayAddress может быть любой допустимый общедоступный IP-адрес, так как мы еще не создали hello шлюз для hello диспетчера ресурсов виртуальной сети. После создания шлюза hello, мы заменяем этот IP-адрес заполнителя hello открытый IP-адрес, которому назначен toohello RM шлюза.

    <LocalNetworkSites>
      <LocalNetworkSite name="RMVNetLocal">
        <AddressSpace>
          <AddressPrefix>192.168.0.0/16</AddressPrefix>
        </AddressSpace>
        <VPNGatewayAddress>13.68.210.16</VPNGatewayAddress>
      </LocalNetworkSite>
    </LocalNetworkSites>

### <a name="part-4---associate-hello-vnet-with-hello-local-network-site"></a>Часть 4 - hello связывание виртуальной сети с сайта локальной сети hello
В этом разделе мы указываем hello сайта локальной сети, что требуется tooconnect виртуальной сети для hello. В этом случае это hello виртуальную сеть диспетчера ресурсов, ссылки на более ранних версий. Убедитесь, что имена hello соответствует. На этом этапе шлюз еще не создается. Он указывает, что hello локальной сети, hello шлюз будет подключаться к.

        <Gateway>
          <ConnectionsToLocalNetwork>
            <LocalNetworkSiteRef name="RMVNetLocal">
              <Connection type="IPsec" />
            </LocalNetworkSiteRef>
          </ConnectionsToLocalNetwork>
        </Gateway>

### <a name="part-5---save-hello-file-and-upload"></a>Часть 5 - сохранить файл hello и передачи
Сохраните файл hello, а затем импортировать его tooAzure, выполнив следующую команду hello. Убедитесь, что изменение пути файла hello, необходимые для вашей среды.

```powershell
Set-AzureVNetConfig -ConfigurationPath C:\AzureNet\NetworkConfig.xml
```

Вы увидите тот же результат, удовлетворены hello импорта.

        OperationDescription        OperationId                      OperationStatus                                                
        --------------------        -----------                      ---------------                                                
        Set-AzureVNetConfig        e0ee6e66-9167-cfa7-a746-7casb9    Succeeded 

### <a name="part-6---create-hello-gateway"></a>Часть 6 - Создание шлюза hello

Перед запуском этого примера, см. toohello toosee ожидает, что файл конфигурации сети, загруженный для hello точные имена, которые платформа Azure. файл конфигурации сети Hello содержит hello значения для классических виртуальных сетей. Иногда hello имена для виртуальных сетей изменения в файле конфигурации сети hello при создании классического параметры виртуальной сети в классическом hello портал Azure, из-за различия toohello в модели развертывания hello. Например, при использовании Azure портала toocreate классической виртуальной сети с именем «Классической виртуальной сети» и он создан в группе ресурсов с именем «ClassicRG» hello, hello, содержащийся в файле конфигурации сети hello называется преобразованный too'Group ClassicRG классической виртуальной сети ". При указании hello имя виртуальной сети, которая содержит пробелы, используйте кавычки вокруг значение hello.


Используйте следующий пример toocreate шлюза с динамической маршрутизацией hello.

```powershell
New-AzureVNetGateway -VNetName ClassicVNet -GatewayType DynamicRouting
```

Можно проверить состояние hello hello шлюза с помощью hello **Get-AzureVNetGateway** командлета.

## <a name="creatermgw"></a>Раздел 2: Настройка шлюза виртуальной сети RM hello
toocreate VPN-шлюз для hello RM виртуальной сети, следуйте инструкциям hello. Не начинайте hello действия до, после получения hello общедоступный IP-адрес для шлюза hello классической виртуальной сети. 

1. Войдите в систему tooyour учетной записи Azure в консоли PowerShell hello. Hello следующий командлет запросит hello учетные данные входа для учетной записи Azure. После входа в систему, чтобы они были доступны tooAzure PowerShell, загружаются параметры учетной записи.

  ```powershell
  Login-AzureRmAccount
  ``` 
   
  Если у вас есть несколько подписок, запросите их список.

  ```powershell
  Get-AzureRmSubscription
  ```
   
  Укажите требуемый toouse подписки hello.

  ```powershell
  Select-AzureRmSubscription -SubscriptionName "Name of subscription"
  ```
2. Создайте локальный сетевой шлюз. В виртуальной сети шлюз локальной сети hello обычно относится tooyour в локальном расположении. В этом случае шлюз локальной сети hello указывает tooyour классической виртуальной сети. Присвойте ему имя, с помощью которого можно ссылаться tooit Azure, а также указать префикс пространства адресов hello. Azure использует префикс IP-адреса укажите tooidentify tooyour toosend какой трафик локального расположения hello. Для получения tooadjust hello сведений здесь более поздней версии, перед созданием шлюза, можно изменить значения hello и образец hello выполнения снова.
   
   **-Имя** является именем hello, требуется шлюз локальной сети toohello toorefer tooassign.<br>
   **-AddressPrefix** — hello адресное пространство для классической виртуальной сети.<br>
   **-GatewayIpAddress** — hello общедоступный IP-адрес шлюза hello классической виртуальной сети. Убедитесь, что следующие hello toochange пример tooreflect hello правильный IP-адрес.<br>

  ```powershell
  New-AzureRmLocalNetworkGateway -Name ClassicVNetLocal `
  -Location "West US" -AddressPrefix "10.0.0.0/24" `
  -GatewayIpAddress "n.n.n.n" -ResourceGroupName RG1
  ```
3. Запрос открытый IP адрес toobe toohello выделенный шлюз виртуальной сети для hello диспетчера ресурсов виртуальной сети. Нельзя указать hello IP-адреса, которые должны toouse. шлюз виртуальной сети toohello выделяется динамически Hello IP-адрес. Однако это не означает hello изменения IP-адреса. Hello только время изменения IP-адреса шлюза виртуальной сети hello когда hello шлюза будет удалено и создано заново. Изменение размера, сброс или другие внутренние обслуживания или обновления шлюза hello не будет изменена.

  На этом этапе также задается переменная, которая будет использоваться позже.

  ```powershell
  $ipaddress = New-AzureRmPublicIpAddress -Name gwpip `
  -ResourceGroupName RG1 -Location 'EastUS' `
  -AllocationMethod Dynamic
  ```

4. Проверьте наличие подсети шлюза в виртуальной сети. Если подсети шлюза нет, добавьте ее. Убедитесь, что подсеть шлюза hello называется *GatewaySubnet*.
5. Получить подсеть hello, используемая для шлюза hello, выполнив следующую команду hello. На этом шаге мы также настроить переменной toobe используется в следующем шаге hello.
   
   **-Имя** hello имя виртуальной сети диспетчер ресурсов.<br>
   **-ResourceGroupName** является группой ресурсов hello, hello, связанный с виртуальной сети. подсеть шлюза Hello уже должен существовать для этой виртуальной сети и должен называться *GatewaySubnet* toowork должным образом.<br>

  ```powershell
  $subnet = Get-AzureRmVirtualNetworkSubnetConfig -Name GatewaySubnet `
  -VirtualNetwork (Get-AzureRmVirtualNetwork -Name RMVNet -ResourceGroupName RG1)
  ``` 

6. Создайте адресации конфигурации IP-адрес шлюза hello. Конфигурация шлюза Hello определяет подсеть hello и hello открытый IP адрес toouse. Используйте следующие toocreate образец hello конфигурацию шлюза.

  На этом шаге hello **- SubnetId** и **- PublicIpAddressId** параметры должны передаваться свойства id hello hello подсети и IP адрес объектов, соответственно. Нельзя использовать простую строку. Эти переменные задаются в toorequest шаг hello общедоступный IP-адрес и hello шаг tooretrieve hello подсети.

  ```powershell
  $gwipconfig = New-AzureRmVirtualNetworkGatewayIpConfig `
  -Name gwipconfig -SubnetId $subnet.id `
  -PublicIpAddressId $ipaddress.id
  ```
7. Создание шлюза виртуальной сети hello диспетчера ресурсов, выполнив следующую команду hello. Hello `-VpnType` должно быть *routebased*. Может потребоваться 45 минут или больше toocreate hello шлюза.

  ```powershell
  New-AzureRmVirtualNetworkGateway -Name RMGateway -ResourceGroupName RG1 `
  -Location "EastUS" -GatewaySKU Standard -GatewayType Vpn `
  -IpConfigurations $gwipconfig `
  -EnableBgp $false -VpnType RouteBased
  ```
8. Скопируйте hello общедоступный IP-адрес после создания VPN-шлюз hello. Используется при настройке параметров локальной сети hello для классической виртуальной сети. Можно использовать следующий командлет tooretrieve hello открытый IP-адрес hello. Hello общедоступный IP-адрес указан в hello, возвращаемое как *IP-адрес*.

  ```powershell
  Get-AzureRmPublicIpAddress -Name gwpip -ResourceGroupName RG1
  ```

## <a name="section-3-modify-hello-classic-vnet-local-site-settings"></a>Раздел 3: Изменение hello классический параметрами локального сайта виртуальной сети

В этом разделе, работать с hello классической виртуальной сети. Можно заменить hello заполнитель IP-адрес, который использовался при указании параметров hello локального сайта, которая будет toohello tooconnect используется шлюз виртуальной сети диспетчер ресурсов. 

1. Экспортируйте файл конфигурации сети hello.

  ```powershell
  Get-AzureVNetConfig -ExportToFile C:\AzureNet\NetworkConfig.xml
  ```
2. В текстовом редакторе, измените значение hello для VPNGatewayAddress. Замените IP-адрес заполнителя hello hello общедоступный IP-адрес шлюза hello диспетчера ресурсов, а затем сохраните изменения hello.

  ```
  <VPNGatewayAddress>13.68.210.16</VPNGatewayAddress>
  ```
3. Импорт hello изменить tooAzure файла конфигурации сети.

  ```powershell
  Set-AzureVNetConfig -ConfigurationPath C:\AzureNet\NetworkConfig.xml
  ```

## <a name="connect"></a>Раздел 4: Создайте подключение между шлюзами hello
Создание подключения между шлюзами hello требуется PowerShell. Может потребоваться tooadd вашей учетной записи Azure toouse hello классической версии hello командлеты PowerShell. Таким образом, используйте toodo **Add-AzureAccount**.

1. В консоли PowerShell hello задайте общий ключ. Перед выполнением командлетов hello, ссылаться toohello toosee ожидает, что файл конфигурации сети, загруженный для hello точные имена, которые платформа Azure. При указании hello имя виртуальной сети, которая содержит пробелы, используйте одинарные кавычки значение hello.<br><br>В следующем примере **- VNetName** — имя hello hello классической виртуальной сети и **- LocalNetworkSiteName** hello имя сайта локальной сети hello. Hello **- SharedKey** создать и задать значение. В примере hello мы использовали «abc123», но вы можете создавать и использовать более сложной. Hello, важно, что очередь является то значение hello, здесь должно быть приветствия одинаковое значение указывается в hello следующий шаг при создании подключения. должно отображаться Hello возвращаемого **состояния: успешно**.

  ```powershell
  Set-AzureVNetGatewayKey -VNetName ClassicVNet `
  -LocalNetworkSiteName RMVNetLocal -SharedKey abc123
  ```
2. Создайте hello VPN-подключение, выполнив следующие команды hello:
   
  Установка переменных hello.

  ```powershell
  $vnet01gateway = Get-AzureRMLocalNetworkGateway -Name ClassicVNetLocal -ResourceGroupName RG1
  $vnet02gateway = Get-AzureRmVirtualNetworkGateway -Name RMGateway -ResourceGroupName RG1
  ```
   
  Создание подключения hello. Обратите внимание, что hello **- ConnectionType** — IPsec не Vnet2Vnet.

  ```powershell
  New-AzureRmVirtualNetworkGatewayConnection -Name RM-Classic -ResourceGroupName RG1 `
  -Location "East US" -VirtualNetworkGateway1 `
  $vnet02gateway -LocalNetworkGateway2 `
  $vnet01gateway -ConnectionType IPsec -RoutingWeight 10 -SharedKey 'abc123'
  ```

## <a name="section-5-verify-your-connections"></a>Раздел 5. Проверка подключений

### <a name="tooverify-hello-connection-from-your-classic-vnet-tooyour-resource-manager-vnet"></a>tooverify hello подключения из вашей классической виртуальной сети tooyour диспетчера ресурсов виртуальной сети

#### <a name="powershell"></a>PowerShell

[!INCLUDE [vpn-gateway-verify-connection-ps-classic](../../includes/vpn-gateway-verify-connection-ps-classic-include.md)]

#### <a name="azure-portal"></a>Портал Azure

[!INCLUDE [vpn-gateway-verify-connection-azureportal-classic](../../includes/vpn-gateway-verify-connection-azureportal-classic-include.md)]


### <a name="tooverify-hello-connection-from-your-resource-manager-vnet-tooyour-classic-vnet"></a>tooverify hello подключения из вашей виртуальной сети диспетчер ресурсов tooyour классической виртуальной сети

#### <a name="powershell"></a>PowerShell

[!INCLUDE [vpn-gateway-verify-ps-rm](../../includes/vpn-gateway-verify-connection-ps-rm-include.md)]

#### <a name="azure-portal"></a>Портал Azure

[!INCLUDE [vpn-gateway-verify-connection-portal-rm](../../includes/vpn-gateway-verify-connection-portal-rm-include.md)]

## <a name="faq"></a>Часто задаваемые вопросы о подключениях типа "виртуальная сеть — виртуальная сеть"

[!INCLUDE [vpn-gateway-vnet-vnet-faq](../../includes/vpn-gateway-vnet-vnet-faq-include.md)]

