---
title: "Подключение сайтов toomultiple виртуальной сети, с помощью VPN-шлюза и PowerShell: классический | Документы Microsoft"
description: "В этой статье описывается подключение нескольких локальных сайтов tooa виртуальной сети с помощью VPN-шлюза для hello классической модели развертывания."
services: vpn-gateway
documentationcenter: na
author: yushwang
manager: rossort
editor: 
tags: azure-service-management
ms.assetid: b043df6e-f1e8-4a4d-8467-c06079e2c093
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/20/2017
ms.author: yushwang
ms.openlocfilehash: 5404b1c55ed3453b4dbc94dfd93e47c0812025f4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="add-a-site-to-site-connection-tooa-vnet-with-an-existing-vpn-gateway-connection-classic"></a>Добавить tooa подключения сайта для сайта виртуальной сети с помощью существующего VPN-шлюза подключения (классические)

[!INCLUDE [deployment models](../../includes/vpn-gateway-classic-deployment-model-include.md)]

> [!div class="op_single_selector"]
> * [Портал Azure](vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md)
> * [PowerShell (классическая модель)](vpn-gateway-multi-site.md)
>
>

В этой статье описывается с помощью PowerShell tooadd-сайтами (S2S) подключений tooa VPN-шлюз, имеется существующее подключение. Этот тип подключения чаще всего ссылка tooas конфигурации «нескольких сайтов». Hello действия в этой статье, относятся toovirtual сетей, созданных с помощью hello классической модели развертывания (также известные как службы управления). Эти действия не относятся существующих конфигураций подключений tooExpressRoute/сайт-сайт.

### <a name="deployment-models-and-methods"></a>Модели и методы развертывания

[!INCLUDE [vpn-gateway-clasic-rm](../../includes/vpn-gateway-classic-rm-include.md)]

Мы обновляем эту таблицу по мере выпуска новых статей и дополнительных инструментов для этой конфигурации. Если статья доступен, непосредственно свяжем tooit из этой таблицы.

[!INCLUDE [vpn-gateway-table-multi-site](../../includes/vpn-gateway-table-multisite-include.md)]

## <a name="about-connecting"></a>О подключении

Можно подключить несколько локальных сайтов tooa одной виртуальной сети. Это особенно привлекательно для создания гибридных облачных решений. Создание шлюза виртуальной сети Azure подключение нескольких сайтов tooyour составляет примерно toocreating других подключений сайт-сайт. На самом деле можно использовать существующий шлюз Azure VPN, при условии, что шлюз hello является динамическим (на основе маршрутов).

При наличии подключенных tooyour статический шлюз виртуальной сети можно изменить toodynamic типа hello шлюза, не перестраивая toorebuild hello виртуальной сети в порядке tooaccommodate несколькими сайтами. Перед изменением типа маршрутизации hello, убедитесь, что шлюза VPN локальной поддерживает конфигурации VPN на основе маршрута.

![Схема многосайтового подключения](./media/vpn-gateway-multi-site/multisite.png "Многосайтовое подключение")

## <a name="points-tooconsider"></a>Tooconsider точек

**Его нельзя будет toouse hello портала toomake изменения toothis виртуальной сети.** Требуется файл конфигурации сети toohello изменения toomake вместо использования портала hello. При внесении изменений в портале hello они заменят параметры несколькими сайтами ссылку для этой виртуальной сети.

Вы уверены, что справитесь с помощью файла конфигурации сети hello, hello времени после завершения процедуры hello несколькими сайтами. Тем не менее при наличии нескольких работающим по конфигурации сети, необходимо убедиться, что все знает об этом ограничении toomake. Это не значит, что нельзя использовать портал hello во всех. Можно использовать для всех остальных объектов, за исключением того, делая конфигурации изменения toothis конкретной виртуальной сети.

## <a name="before-you-begin"></a>Перед началом работы

Перед началом настройки убедитесь, что hello следующее:

* Совместимое оборудование VPN для каждого местного расположения. Проверьте [сведения об устройствах VPN для подключения к виртуальной сети](vpn-gateway-about-vpn-devices.md) tooverify Если hello устройства, которые должны toouse, известный toobe совместимы.
* Внешний общедоступный IPv4-адрес для каждого VPN-устройства. Hello IP-адрес не может располагаться за устройством NAT. Это обязательное требование.
* Вам потребуется tooinstall hello последняя версия командлетов Azure PowerShell hello. Убедитесь, что установки службы управления (SM) версии hello в версии диспетчера ресурсов toohello сложения. В разделе [как tooinstall и настройка Azure PowerShell](/powershell/azure/overview) для получения дополнительной информации.
* Пользователь, имеющий опыт в настройке вашего оборудования VPN. Вы получите toohave хорошо понимать процесс tooconfigure VPN-устройство или работают с специалистом.
* диапазоны IP-адресов Hello требуется toouse для виртуальной сети (Если вы еще не созданы).
* Hello диапазоны IP-адресов для каждого из сайтов локальной сети hello, которые вы будете подключаться. Необходимо убедиться, что диапазоны hello IP-адресов для каждого из сайтов локальной сети hello, что требуется tooconnect toodo не перекрываются toomake. В противном случае hello портала или hello REST API отклонит загружаемую конфигурацию hello.<br>Например если у вас есть два сайта локальной сети, что оба содержат 10.2.3.0/24 диапазон адресов IP hello и у вас есть пакет с адресом назначения 10.2.3.3, Azure не сможет определить сайт, который требуется toosend hello пакета toobecause hello диапазоны адресов — перекрывающиеся. tooprevent проблем с маршрутизацией, Azure не позволяет tooupload файл конфигурации, который имеет пересекающиеся диапазоны адресов.

## <a name="1-create-a-site-to-site-vpn"></a>1. Создание подключения VPN типа "сеть — сеть"
Это отлично, если у вас уже есть подключение VPN типа "сеть — сеть" со шлюзом с динамической маршрутизацией. Можно продолжить слишком[экспорт параметров конфигурации виртуальной сети hello](#export). В противном случае hello следующие:

### <a name="if-you-already-have-a-site-to-site-virtual-network-but-it-has-a-static-policy-based-routing-gateway"></a>Если у вас уже есть виртуальная сеть типа "сеть — сеть", но со шлюзом со статической маршрутизацией (на основе политики)
1. Изменение маршрута toodynamic тип шлюза. Для многосайтового подключения VPN требуется шлюз с динамической маршрутизацией (также известный как шлюз на основе маршрутов). Введите toochange шлюз, вы добавите требуется toofirst delete hello существующий шлюз, а затем создайте новую. Инструкции см. в разделе [как toochange hello VPN тип маршрутизации шлюза](vpn-gateway-configure-vpn-gateway-mp.md).  
2. Настройте новый шлюз и создайте VPN-туннель. Инструкции см. в разделе [настроить VPN-шлюза в классический портал Azure hello](vpn-gateway-configure-vpn-gateway-mp.md). Во-первых измените маршрут toodynamic тип шлюза.

### <a name="if-you-dont-have-a-site-to-site-virtual-network"></a>Если у вас нет виртуальной сети типа "сеть — сеть"
1. Создание виртуальной сети сайт-сайт с помощью следующей процедуры: [создайте виртуальную сеть с VPN-подключения сеть-сеть в классический портал Azure hello](vpn-gateway-site-to-site-create.md).  
2. Настройте шлюз с динамической маршрутизацией с помощью следующей процедуры: [Настройка VPN-шлюза](vpn-gateway-configure-vpn-gateway-mp.md). Быть убедиться, что tooselect **динамической маршрутизации** применительно к типу шлюза.

## <a name="export"></a>2. Экспортируйте файл конфигурации сети hello
Экспортируйте файл конфигурации сети Azure, выполнив следующую команду hello. Можно изменить расположение hello hello tooexport tooa различные расположения файла при необходимости.

```powershell
Get-AzureVNetConfig -ExportToFile C:\AzureNet\NetworkConfig.xml
```

## <a name="3-open-hello-network-configuration-file"></a>3. Привет открыть файл конфигурации сети
Откройте файл конфигурации сети hello, загруженный на последнем шаге hello. Используйте любой редактор XML. файл Hello должен выглядеть примерно toohello следующее:

        <NetworkConfiguration xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/ServiceHosting/2011/07/NetworkConfiguration">
          <VirtualNetworkConfiguration>
            <LocalNetworkSites>
              <LocalNetworkSite name="Site1">
                <AddressSpace>
                  <AddressPrefix>10.0.0.0/16</AddressPrefix>
                  <AddressPrefix>10.1.0.0/16</AddressPrefix>
                </AddressSpace>
                <VPNGatewayAddress>131.2.3.4</VPNGatewayAddress>
              </LocalNetworkSite>
              <LocalNetworkSite name="Site2">
                <AddressSpace>
                  <AddressPrefix>10.2.0.0/16</AddressPrefix>
                  <AddressPrefix>10.3.0.0/16</AddressPrefix>
                </AddressSpace>
                <VPNGatewayAddress>131.4.5.6</VPNGatewayAddress>
              </LocalNetworkSite>
            </LocalNetworkSites>
            <VirtualNetworkSites>
              <VirtualNetworkSite name="VNet1" AffinityGroup="USWest">
                <AddressSpace>
                  <AddressPrefix>10.20.0.0/16</AddressPrefix>
                  <AddressPrefix>10.21.0.0/16</AddressPrefix>
                </AddressSpace>
                <Subnets>
                  <Subnet name="FE">
                    <AddressPrefix>10.20.0.0/24</AddressPrefix>
                  </Subnet>
                  <Subnet name="BE">
                    <AddressPrefix>10.20.1.0/24</AddressPrefix>
                  </Subnet>
                  <Subnet name="GatewaySubnet">
                    <AddressPrefix>10.20.2.0/29</AddressPrefix>
                  </Subnet>
                </Subnets>
                <Gateway>
                  <ConnectionsToLocalNetwork>
                    <LocalNetworkSiteRef name="Site1">
                      <Connection type="IPsec" />
                    </LocalNetworkSiteRef>
                  </ConnectionsToLocalNetwork>
                </Gateway>
              </VirtualNetworkSite>
            </VirtualNetworkSites>
          </VirtualNetworkConfiguration>
        </NetworkConfiguration>

## <a name="4-add-multiple-site-references"></a>4. Добавление ссылок на несколько сайтов
При добавлении или удалении будет вносить изменения toohello элемент ConnectionsToLocalNetwork/LocalNetworkSiteRef. Добавление новой ссылки на локальный сайт Azure toocreate запускает новый туннель. В следующем примере hello hello сеть настроена для подключения одного сайта. Сохраните файл hello, после внесения изменений.

```
  <Gateway>
    <ConnectionsToLocalNetwork>
      <LocalNetworkSiteRef name="Site1"><Connection type="IPsec" /></LocalNetworkSiteRef>
    </ConnectionsToLocalNetwork>
  </Gateway>
```

tooadd дополнительных ссылок на сайты (создать конфигурации нескольких сайтов), достаточно добавить строки дополнительных «LocalNetworkSiteRef», как показано в приведенном ниже примере hello.

```
  <Gateway>
    <ConnectionsToLocalNetwork>
      <LocalNetworkSiteRef name="Site1"><Connection type="IPsec" /></LocalNetworkSiteRef>
      <LocalNetworkSiteRef name="Site2"><Connection type="IPsec" /></LocalNetworkSiteRef>
    </ConnectionsToLocalNetwork>
  </Gateway>
```

## <a name="5-import-hello-network-configuration-file"></a>5. Импорт файла конфигурации сети hello
Импорт файла конфигурации сети hello. При импорте этого файла с изменениями hello, будут добавлены новые туннели hello. Привет туннели будут использовать шлюз с динамической hello, созданного ранее. Можно использовать либо hello классического портала или файл hello tooimport PowerShell.

## <a name="6-download-keys"></a>6. Скачивание ключей
После добавления новых туннелей используйте hello PowerShell командлет «Get-AzureVNetGatewayKey» tooget hello IPsec/IKE предварительные общие ключи для каждого туннеля.

Например:

```powershell
Get-AzureVNetGatewayKey –VNetName "VNet1" –LocalNetworkSiteName "Site1"
Get-AzureVNetGatewayKey –VNetName "VNet1" –LocalNetworkSiteName "Site2"
```

При желании можно также использовать hello *получения шлюза общего ключа виртуальной сети* tooget API-интерфейса REST hello предварительные общие ключи.

## <a name="7-verify-your-connections"></a>7. Проверка подключений
Проверьте состояние многосайтового туннеля hello. После загрузки hello ключей для каждого туннеля, будет необходимо tooverify подключений. Используйте «Get-AzureVnetConnection» tooget туннели список виртуальных сетей, как показано в приведенном ниже примере hello. VNet1 — имя hello hello виртуальной сети.

```powershell
Get-AzureVnetConnection -VNetName VNET1
```

Пример возвращаемых данных:

```
    ConnectivityState         : Connected
    EgressBytesTransferred    : 661530
    IngressBytesTransferred   : 519207
    LastConnectionEstablished : 5/2/2014 2:51:40 PM
    LastEventID               : 23401
    LastEventMessage          : hello connectivity state for hello local network site 'Site1' changed from Not Connected tooConnected.
    LastEventTimeStamp        : 5/2/2014 2:51:40 PM
    LocalNetworkSiteName      : Site1
    OperationDescription      : Get-AzureVNetConnection
    OperationId               : 7f68a8e6-51e9-9db4-88c2-16b8067fed7f
    OperationStatus           : Succeeded

    ConnectivityState         : Connected
    EgressBytesTransferred    : 789398
    IngressBytesTransferred   : 143908
    LastConnectionEstablished : 5/2/2014 3:20:40 PM
    LastEventID               : 23401
    LastEventMessage          : hello connectivity state for hello local network site 'Site2' changed from Not Connected tooConnected.
    LastEventTimeStamp        : 5/2/2014 2:51:40 PM
    LocalNetworkSiteName      : Site2
    OperationDescription      : Get-AzureVNetConnection
    OperationId               : 7893b329-51e9-9db4-88c2-16b8067fed7f
    OperationStatus           : Succeeded
```

## <a name="next-steps"></a>Дальнейшие действия

toolearn Дополнительные сведения о шлюзах VPN в разделе [о шлюзах VPN](vpn-gateway-about-vpngateways.md).
