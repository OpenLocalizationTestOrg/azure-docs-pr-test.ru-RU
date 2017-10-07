---
title: "Создание и изменение канала ExpressRoute с помощью PowerShell и Azure Resource Manager | Документация Майкрософт"
description: "В этой статье описывается, как toocreate, подготовки, проверьте, обновление, удаление и отзыв канал ExpressRoute."
documentationcenter: na
services: expressroute
author: ganesr
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: f997182e-9b25-4a7a-b079-b004221dadcc
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/12/2017
ms.author: ganesr;cherylmc
ms.openlocfilehash: 8d76c577a9cffdd393abac1b76cccc27d92e9e62
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-modify-an-expressroute-circuit-using-powershell"></a>Создание и изменение канала ExpressRoute с помощью PowerShell
> [!div class="op_single_selector"]
> * [Портал Azure](expressroute-howto-circuit-portal-resource-manager.md)
> * [PowerShell](expressroute-howto-circuit-arm.md)
> * [Интерфейс командной строки Azure](howto-circuit-cli.md)
> * [Видео — портал Azure](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-an-expressroute-circuit)
> * [PowerShell (классическая модель)](expressroute-howto-circuit-classic.md)
>

В этой статье описывается, как circuit toocreate Azure ExpressRoute с помощью PowerShell командлеты и hello Azure модели развертывания диспетчера ресурсов. В этой статье также рассказывается, как toocheck hello состояние канала hello, обновления или удаления и сделать.

## <a name="before-you-begin"></a>Перед началом работы
* Установите последнюю версию hello hello командлеты PowerShell диспетчера ресурсов Azure. Дополнительные сведения см. в [обзоре Azure PowerShell](/powershell/azure/overview).
* Просмотрите hello [необходимые компоненты](expressroute-prerequisites.md) и [рабочих процессов](expressroute-workflows.md) перед началом настройки.


## <a name="create-and-provision-an-expressroute-circuit"></a>Создание и предоставление канала ExpressRoute
### <a name="1-sign-in-tooyour-azure-account-and-select-your-subscription"></a>1. Войдите в tooyour учетная запись Azure и выберите подписку
toobegin конфигурацию входа tooyour учетная запись Azure. Используйте следующие примеры toohelp подключении hello.

```powershell
Login-AzureRmAccount
```

Проверьте hello подписки для учетной записи hello.

```powershell
Get-AzureRmSubscription
```

Выберите подписку hello toocreate expressroute в для:

```powershell
Select-AzureRmSubscription -SubscriptionId "<subscription ID>"
```

### <a name="2-get-hello-list-of-supported-providers-locations-and-bandwidths"></a>2. Получить список поддерживаемых поставщиков, расположений и полос пропускания hello
Прежде чем создавать канал ExpressRoute, необходимо hello список поставщиков поддерживаемых соединений, расположений и полосы пропускания.

Здравствуйте, командлета PowerShell **Get AzureRmExpressRouteServiceProvider** возвращает эту информацию, которая будет использоваться на последующих этапах:

```powershell
Get-AzureRmExpressRouteServiceProvider
```

Проверьте toosee, если поставщиком соединения существует в списке. Запишите hello следующую информацию. Они потребуется позже при создании канала.

* Имя
* PeeringLocations
* BandwidthsOffered

Теперь вы готовы toocreate канал ExpressRoute.   

### <a name="3-create-an-expressroute-circuit"></a>3. Создание канала ExpressRoute
Перед созданием канала ExpressRoute необходимо создать группу ресурсов (если вы этого еще не сделали) Это можно сделать, запустив hello следующую команду:

```powershell
New-AzureRmResourceGroup -Name "ExpressRouteResourceGroup" -Location "West US"
```


Привет, в следующем примере показано, как circuit toocreate ExpressRoute 200 Мбит/с до Equinix в Силиконовой долине. Если вы используете другой поставщик и другие параметры, подставьте в запрос соответствующие данные. Hello ниже приведен пример запроса нового ключа службы.

```powershell
New-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup" -Location "West US" -SkuTier Standard -SkuFamily MeteredData -ServiceProviderName "Equinix" -PeeringLocation "Silicon Valley" -BandwidthInMbps 200
```

Убедитесь, что указан правильный уровень номера SKU hello и семейство номеров SKU:

* Уровень SKU определяет, какая надстройка включена — ExpressRoute Standard или ExpressRoute Premium. Можно указать *Стандартная* tooget hello стандартном номере SKU или *Premium* hello premium надстройки.
* Семейство номеров SKU определяет hello выставления счетов с типом. Выберите *Metereddata* для тарифного плана с оплатой за трафик или *Unlimiteddata* для безлимитного тарифного плана. Можно изменить тип выставления счетов hello из *Metereddata* слишком*Unlimiteddata*, но не может изменить тип hello из *Unlimiteddata* слишком*Metereddata* .

> [!IMPORTANT]
> Ваш канал ExpressRoute будет записана с момента hello выдачи ключа службы. Убедитесь, что эта операция при готовности tooprovision hello цепи hello поставщика услуг подключения.
> 
> 

Hello ответ содержит ключ службы hello. Подробное описание всех параметров hello можно получить, выполнив следующую команду hello:

```powershell
get-help New-AzureRmExpressRouteCircuit -detailed
```


### <a name="4-list-all-expressroute-circuits"></a>4. Получение списка всех каналов ExpressRoute
список всех hello каналы ExpressRoute, которые были созданы tooget запуска hello **Get AzureRmExpressRouteCircuit** команды:

```powershell
Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"
```

Hello ответа будет выглядеть аналогично toohello в следующем примере:

    Name                             : ExpressRouteARMCircuit
    ResourceGroupName                : ExpressRouteResourceGroup
    Location                         : westus
    Id                               : /subscriptions/***************************/resourceGroups/ExpressRouteResourceGroup/providers/Microsoft.Network/expressRouteCircuits/ExpressRouteARMCircuit
    Etag                             : W/"################################"
    ProvisioningState                : Succeeded
    Sku                              : {
                                         "Name": "Standard_MeteredData",
                                         "Tier": "Standard",
                                         "Family": "MeteredData"
                                          }
    CircuitProvisioningState          : Enabled
    ServiceProviderProvisioningState  : NotProvisioned
    ServiceProviderNotes              :
    ServiceProviderProperties         : {
                                          "ServiceProviderName": "Equinix",
                                          "PeeringLocation": "Silicon Valley",
                                          "BandwidthInMbps": 200
                                        }
    ServiceKey                        : **************************************
    Peerings                          : []

Эти сведения в любое время можно получить с помощью hello `Get-AzureRmExpressRouteCircuit` командлета. Делая hello вызова без параметров перечисляет все каналы hello. Ключ службы будут перечислены в hello *ServiceKey* поля:

```powershell
Get-AzureRmExpressRouteCircuit
```


Hello ответа будет выглядеть аналогично toohello в следующем примере:

    Name                             : ExpressRouteARMCircuit
    ResourceGroupName                : ExpressRouteResourceGroup
    Location                         : westus
    Id                               : /subscriptions/***************************/resourceGroups/ExpressRouteResourceGroup/providers/Microsoft.Network/expressRouteCircuits/ExpressRouteARMCircuit
    Etag                             : W/"################################"
    ProvisioningState                : Succeeded
    Sku                              : {
                                         "Name": "Standard_MeteredData",
                                         "Tier": "Standard",
                                         "Family": "MeteredData"
                                          }
    CircuitProvisioningState         : Enabled
    ServiceProviderProvisioningState : NotProvisioned
    ServiceProviderNotes             :
    ServiceProviderProperties        : {
                                         "ServiceProviderName": "Equinix",
                                         "PeeringLocation": "Silicon Valley",
                                         "BandwidthInMbps": 200
                                          }
    ServiceKey                       : **************************************
    Peerings                         : []


Подробное описание всех параметров hello можно получить, выполнив следующую команду hello:

```powershell
get-help Get-AzureRmExpressRouteCircuit -detailed
```

### <a name="5-send-hello-service-key-tooyour-connectivity-provider-for-provisioning"></a>5. Отправка ключа tooyour подключения hello службы поставщика для подготовки
*ServiceProviderProvisioningState* предоставляет сведения о текущем состоянии hello подготовки на стороне поставщика услуг hello. Состояния содержит состояние hello hello стороны Майкрософт. Дополнительные сведения о состояния подготовки схемы см. в разделе hello [рабочих процессов](expressroute-workflows.md#expressroute-circuit-provisioning-states) статьи.

При создании нового канала ExpressRoute hello схемы будут иметь hello следующие состояния:

    ServiceProviderProvisioningState : NotProvisioned
    CircuitProvisioningState         : Enabled



цепь Hello приведет к изменению toohello при поставщика услуг подключения hello находится в процессе hello включить его для вас следующие состояния:

    ServiceProviderProvisioningState : Provisioning
    Status                           : Enabled

Для вас toobe может toouse канал ExpressRoute он должен быть в hello следующие состояния:

    ServiceProviderProvisioningState : Provisioned
    CircuitProvisioningState         : Enabled

### <a name="6-periodically-check-hello-status-and-hello-state-of-hello-circuit-key"></a>6. Периодически Проверьте состояние hello и состояние hello ключа канала hello
Проверка состояния hello и состояние hello hello ключа канала позволяет узнать, когда поставщик подключит ваш канал. После настройки канала hello *ServiceProviderProvisioningState* отображается как *инициализировано*, как показано в следующий пример hello:

```powershell
Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"
```


Hello ответа будет выглядеть аналогично toohello в следующем примере:

    Name                             : ExpressRouteARMCircuit
    ResourceGroupName                : ExpressRouteResourceGroup
    Location                         : westus
    Id                               : /subscriptions/***************************/resourceGroups/ExpressRouteResourceGroup/providers/Microsoft.Network/expressRouteCircuits/ExpressRouteARMCircuit
    Etag                             : W/"################################"
    ProvisioningState                : Succeeded
    Sku                              : {
                                         "Name": "Standard_MeteredData",
                                         "Tier": "Standard",
                                         "Family": "MeteredData"
                                       }
    CircuitProvisioningState         : Enabled
    ServiceProviderProvisioningState : Provisioned
    ServiceProviderNotes             :
    ServiceProviderProperties        : {
                                         "ServiceProviderName": "Equinix",
                                         "PeeringLocation": "Silicon Valley",
                                         "BandwidthInMbps": 200
                                       }
    ServiceKey                       : **************************************
    Peerings                         : []

### <a name="7-create-your-routing-configuration"></a>7. Создание конфигурации маршрутизации
Пошаговые инструкции см. в разделе hello [expressroute в конфигурацию маршрутизации](expressroute-howto-routing-arm.md) статью toocreate и изменения пиринги в цепи.

> [!IMPORTANT]
> Эти инструкции применяются только toocircuits, созданных с помощью службы поставщиков, предлагающих услуги подключений второго уровня. Если вы работаете с поставщиком, предлагающим услуги третьего уровня (обычно это IPVPN, например MPLS), то ваш поставщик услуг подключения выполнит настройку и управление конфигурацией самостоятельно.
> 
> 

### <a name="8-link-a-virtual-network-tooan-expressroute-circuit"></a>8. Связывание виртуальной сети tooan канал ExpressRoute
Затем свяжите виртуальной сети tooyour канал ExpressRoute. Используйте hello [связывание виртуальной сети цепи tooExpressRoute](expressroute-howto-linkvnet-arm.md) статьи при работе с моделью развертывания диспетчера ресурсов hello.

## <a name="getting-hello-status-of-an-expressroute-circuit"></a>Получение состояния hello канал ExpressRoute
Эти сведения в любое время можно получить с помощью hello **Get AzureRmExpressRouteCircuit** командлета. Делая hello вызова без параметров перечисляет все каналы hello.

```powershell
Get-AzureRmExpressRouteCircuit
```


Hello ответ будет иметь примерно toohello в следующем примере:

    Name                             : ExpressRouteARMCircuit
    ResourceGroupName                : ExpressRouteResourceGroup
    Location                         : westus
    Id                               : /subscriptions/***************************/resourceGroups/ExpressRouteResourceGroup/providers/Microsoft.Network/expressRouteCircuits/ExpressRouteARMCircuit
    Etag                             : W/"################################"
    ProvisioningState                : Succeeded
    Sku                              : {
                                         "Name": "Standard_MeteredData",
                                         "Tier": "Standard",
                                         "Family": "MeteredData"
                                       }
    CircuitProvisioningState         : Enabled
    ServiceProviderProvisioningState : Provisioned
    ServiceProviderNotes             :
    ServiceProviderProperties        : {
                                            "ServiceProviderName": "Equinix",
                                            "PeeringLocation": "Silicon Valley",
                                            "BandwidthInMbps": 200
                                          }
    ServiceKey                       : **************************************
    Peerings                         : []


Сведения о конкретных канал ExpressRoute можно получить, передав имя группы ресурсов hello и имя схемы как вызов toohello параметр:

```powershell
Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"
```


Hello ответа будет выглядеть аналогично toohello в следующем примере:

    Name                             : ExpressRouteARMCircuit
    ResourceGroupName                : ExpressRouteResourceGroup
    Location                         : westus
    Id                               : /subscriptions/***************************/resourceGroups/ExpressRouteResourceGroup/providers/Microsoft.Network/expressRouteCircuits/ExpressRouteARMCircuit
    Etag                             : W/"################################"
    ProvisioningState                : Succeeded
    Sku                              : {
                                         "Name": "Standard_MeteredData",
                                            "Tier": "Standard",
                                            "Family": "MeteredData"
                                          }
    CircuitProvisioningState         : Enabled
    ServiceProviderProvisioningState : Provisioned
    ServiceProviderNotes             :
    ServiceProviderProperties        : {
                                         "ServiceProviderName": "Equinix",
                                         "PeeringLocation": "Silicon Valley",
                                         "BandwidthInMbps": 200
                                          }
    ServiceKey                       : **************************************
    Peerings                         : []


Подробное описание всех параметров hello можно получить, выполнив следующую команду hello:

```powershell
get-help get-azurededicatedcircuit -detailed
```

## <a name="modify"></a>Изменение канала ExpressRoute
Некоторые свойства канала ExpressRoute можно изменить, не повлияв на подключение.

Можно сделать hello без простоев следующие:

* включать и отключать надстройку ExpressRoute "Премиум" для канала ExpressRoute;
* Увеличение hello пропускной способностью вашего канала ExpressRoute при условии, что доступно емкости на порту hello. Понижение уровня полосы пропускания канала hello не поддерживается. 
* Изменение плана на основе данных, измеряемые tooUnlimited данных отслеживания использования hello. Изменение hello измерения план из данных tooMetered данных не поддерживается.
* Параметр *Allow Classic Operations*(Разрешить классические операции) можно включать и отключать.

Дополнительные сведения об ограничениях и ограничениях см. в разделе toohello [часто задаваемые вопросы о ExpressRoute](expressroute-faqs.md).

### <a name="tooenable-hello-expressroute-premium-add-on"></a>tooenable hello ExpressRoute премиальное дополнение
Премиальное дополнение hello ExpressRoute можно включить для вашей существующей цепи с помощью hello, следующий фрагмент команды PowerShell:

```powershell
$ckt = Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"

$ckt.Sku.Tier = "Premium"
$ckt.sku.Name = "Premium_MeteredData"

Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```

цепь Hello получают hello ExpressRoute premium дополнительные возможности. Мы начнем выставления счетов для hello premium дополнительные возможности, как только команда hello успешно запущена.

### <a name="toodisable-hello-expressroute-premium-add-on"></a>toodisable hello ExpressRoute премиальное дополнение
> [!IMPORTANT]
> Эта операция может завершиться ошибкой, если вы используете ресурсы, которые больше, чем то, что разрешено для стандартной схемы hello.
> 
> 

Обратите внимание hello следующие:

* Прежде чем понизить из premium toostandard, необходимо убедиться, hello количество виртуальных сетей, которые связаны toohello канала — меньше 10. Если этого не сделать, запрос на обновление завершится ошибкой и мы будем выставлять вам счета по тарифам ценовой категории "Премиум".
* Все связи с виртуальными сетями в других геополитических регионах необходимо разорвать. Если этого не сделать, запрос на обновление завершится ошибкой и мы будем выставлять вам счета по тарифам ценовой категории "Премиум".
* Для частного пиринга таблица маршрутов должна содержать менее 4000 маршрутов. Если размер таблицы маршрутов больше 4000 маршрутов, сеанс BGP hello удаляется и не будет снова включено, пока hello число префиксов, объявленных становится меньше 4 000.

Надстройка premium hello ExpressRoute для существующей цепи hello можно отключить с помощью hello, выполнив командлет PowerShell:

```powershell
$ckt = Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"

$ckt.Sku.Tier = "Standard"
$ckt.sku.Name = "Standard_MeteredData"

Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```

### <a name="tooupdate-hello-expressroute-circuit-bandwidth"></a>пропускная способность контура tooupdate hello ExpressRoute
Поддерживаемые полосы пропускания для поставщика, проверьте hello [часто задаваемые вопросы о ExpressRoute](expressroute-faqs.md). Можно выбрать любой большего размера, чем размер hello вашей существующей цепи.

> [!IMPORTANT]
> Канал ExpressRoute toorecreate hello возможно, если имеется существующий порт hello недостаточной мощности. Обновление схемы hello невозможно, если доступна без дополнительной емкости в этом расположении.
>
> Нельзя уменьшить hello пропускной способности канала ExpressRoute без прерывания. Понижение уровня полосы пропускания необходимо канал ExpressRoute toodeprovision hello и повторной инициализации новый канал ExpressRoute.
> 

После определения размера необходимо, используйте следующие команды tooresize hello ваш канал:

```powershell
$ckt = Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"

$ckt.ServiceProviderProperties.BandwidthInMbps = 1000

Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```


Ваш канал будет изменяться размер на стороне Майкрософт hello. Затем необходимо обратиться к настройки подключения поставщика tooupdate на своей стороне toomatch это изменение. После внесения этого уведомления, мы начнем выставления счетов за hello обновить параметр пропускной способности.

### <a name="toomove-hello-sku-from-metered-toounlimited"></a>hello toomove SKU из отслеживаемых toounlimited
Hello SKU канал ExpressRoute можно изменить с помощью hello, следующий фрагмент команды PowerShell:

```powershell
$ckt = Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"

$ckt.Sku.Family = "UnlimitedData"
$ckt.sku.Name = "Premium_UnlimitedData"

Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```

### <a name="toocontrol-access-toohello-classic-and-resource-manager-environments"></a>Классический toohello toocontrol доступа и диспетчер ресурсов среды
Ознакомьтесь с инструкциями hello в [каналы ExpressRoute переместить из модели развертывания диспетчера ресурсов hello классический toohello](expressroute-howto-move-arm.md).  

## <a name="deprovisioning-and-deleting-an-expressroute-circuit"></a>Отзыв и удаление канала ExpressRoute
Обратите внимание hello следующие:

* Необходимо удалить связь всех виртуальных сетей с каналом expressroute hello. Если операция завершается неудачно, убедитесь, что цепь toohello связанные toosee, если все виртуальные сети.
* Если состояние подготовки службы поставщика hello ExpressRoute канала **Provisioning** или **инициализировано** необходимо работать с ваш канал hello toodeprovision поставщика службы с их стороны. Она будет продолжать tooreserve ресурсы и выставлять вам счет на поставщика услуг hello завершения списания цепи hello и уведомляет нас.
* Если поставщик услуг hello отозваны hello канала (состояние подготовки поставщика услуг hello задано слишком**не инициализировано**) можно удалить цепь hello. Это приведет к остановке выставления счетов для схемы hello

Ваш канал ExpressRoute можно удалить, выполнив следующую команду hello:

```powershell
Remove-AzureRmExpressRouteCircuit -ResourceGroupName "ExpressRouteResourceGroup" -Name "ExpressRouteARMCircuit"
```

## <a name="next-steps"></a>Дальнейшие действия

После создания ваш канал, убедитесь, что hello следующие:

* [Создание и изменение маршрутизации для канала ExpressRoute](expressroute-howto-routing-arm.md)
* [Связать вашей виртуальной сети tooyour канал ExpressRoute](expressroute-howto-linkvnet-arm.md)
