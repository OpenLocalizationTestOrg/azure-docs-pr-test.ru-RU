---
title: "Создание и изменение канала ExpressRoute с помощью PowerShell и классического портала Azure | Документация Майкрософт"
description: "В этой статье содержится описание этапов hello для создания и подготовки канал ExpressRoute. В этой статье также показано, как состояние toocheck hello, обновить, или удалить и Отмена подготовки к схемы."
documentationcenter: na
services: expressroute
author: ganesr
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 0134d242-6459-4dec-a2f1-4657c3bc8b23
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/21/2017
ms.author: ganesr;cherylmc
ms.openlocfilehash: 9897c88776a2153ba22aa9ff328becb9f12b660b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-modify-an-expressroute-circuit-using-powershell-classic"></a>Создание и изменение канала ExpressRoute с помощью PowerShell (классическая модель)
> [!div class="op_single_selector"]
> * [Портал Azure](expressroute-howto-circuit-portal-resource-manager.md)
> * [PowerShell](expressroute-howto-circuit-arm.md)
> * [Интерфейс командной строки Azure](howto-circuit-cli.md)
> * [Видео — портал Azure](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-an-expressroute-circuit)
> * [PowerShell (классическая модель)](expressroute-howto-circuit-classic.md)
>

В этой статье описывается toocreate действия hello канал Azure ExpressRoute с помощью PowerShell командлеты и hello классической модели развертывания. В этой статье также показано, как состояние toocheck hello, обновить, или удалить и отзыв канал ExpressRoute.

[!INCLUDE [expressroute-classic-end-include](../../includes/expressroute-classic-end-include.md)]


**О моделях развертывания Azure**

[!INCLUDE [vpn-gateway-clasic-rm](../../includes/vpn-gateway-classic-rm-include.md)]

## <a name="before-you-begin"></a>Перед началом работы
### <a name="step-1-review-hello-prerequisites-and-workflow-articles"></a>Шаг 1. Проверьте предварительные условия hello и статей рабочего процесса
Убедитесь, что вы просмотрели hello [необходимые компоненты](expressroute-prerequisites.md) и [рабочих процессов](expressroute-workflows.md) перед началом настройки.  

### <a name="step-2-install-hello-latest-versions-of-hello-azure-service-management-sm-powershell-modules"></a>Шаг 2. Установить последние версии hello hello модули PowerShell службы управления Azure (SM)
Следуйте инструкциям в разделе hello [Приступая к работе с помощью командлетов Azure PowerShell](/powershell/azure/overview) пошаговые инструкции о том, как tooconfigure модули Azure PowerShell hello toouse компьютера.

### <a name="step-3-log-in-tooyour-azure-account-and-select-a-subscription"></a>Шаг 3. Войдите в tooyour учетная запись Azure и выберите подписку
1. Откройте консоль PowerShell с повышенными правами и подключите tooyour учетную запись. Используйте следующий пример toohelp подключении hello.

        Login-AzureRmAccount

2. Проверьте hello подписки для учетной записи hello.

        Get-AzureRmSubscription

3. При наличии нескольких подписок выберите подписку hello, что требуется toouse.

        Select-AzureRmSubscription -SubscriptionName "Replace_with_your_subscription_name"

4. Затем используйте следующий командлет tooadd hello tooPowerShell вашей подписки Azure для hello классической модели развертывания.

        Add-AzureAccount

## <a name="create-and-provision-an-expressroute-circuit"></a>Создание и предоставление канала ExpressRoute
### <a name="step-1-import-hello-powershell-modules-for-expressroute"></a>Шаг 1. Импортируйте модули PowerShell hello для ExpressRoute
 Если вы еще не сделали необходимо импортировать модули hello Azure и ExpressRoute в сеанс PowerShell hello в toostart заказа с помощью командлетов ExpressRoute hello. Импортируйте модули hello hello расположение, которое они были установлены tooon локального компьютера. В зависимости от метода hello использовалась tooinstall hello модули, hello расположение может отличаться от следующих примере hello. При необходимости измените пример hello.  

    Import-Module 'C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\ServiceManagement\Azure\Azure.psd1'
    Import-Module 'C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\ServiceManagement\Azure\ExpressRoute\ExpressRoute.psd1'

### <a name="step-2-get-hello-list-of-supported-providers-locations-and-bandwidths"></a>Шаг 2. Получить список поддерживаемых поставщиков, расположений и полос пропускания hello
Прежде чем создавать канал ExpressRoute, необходимо hello список поставщиков поддерживаемых соединений, расположений и полосы пропускания.

Здравствуйте, командлета PowerShell `Get-AzureDedicatedCircuitServiceProvider` возвращает эту информацию, которая будет использоваться на последующих этапах:

    Get-AzureDedicatedCircuitServiceProvider

Проверьте toosee, если поставщиком соединения существует в списке. Запишите hello следующую информацию, так как потребуется позднее при создании канала:

* Имя
* PeeringLocations
* BandwidthsOffered

Теперь вы готовы toocreate канал ExpressRoute.         

### <a name="step-3-create-an-expressroute-circuit"></a>Шаг 3. Создание канала ExpressRoute
Привет, в следующем примере показано, как circuit toocreate ExpressRoute 200 Мбит/с до Equinix в Силиконовой долине. Если вы используете другой поставщик и другие параметры, подставьте в запрос соответствующие данные.

> [!IMPORTANT]
> Ваш канал ExpressRoute будет записана с момента hello выдачи ключа службы. Убедитесь, что эта операция при готовности tooprovision hello цепи hello поставщика услуг подключения.
> 
> 

Hello ниже приведен пример запроса нового ключа службы.

    $Bandwidth = 200
    $CircuitName = "MyTestCircuit"
    $ServiceProvider = "Equinix"
    $Location = "Silicon Valley"

    New-AzureDedicatedCircuit -CircuitName $CircuitName -ServiceProviderName $ServiceProvider -Bandwidth $Bandwidth -Location $Location -sku Standard -BillingType MeteredData

Или, если вы хотите toocreate канал ExpressRoute с надстройками "премиум" hello, hello используйте следующий пример. См. toohello [часто задаваемые вопросы о ExpressRoute](expressroute-faqs.md) Дополнительные сведения о премиальное дополнение hello.

    New-AzureDedicatedCircuit -CircuitName $CircuitName -ServiceProviderName $ServiceProvider -Bandwidth $Bandwidth -Location $Location -sku Premium - BillingType MeteredData


Hello ответ будет содержать hello ключа службы. Подробное описание всех параметров hello можно получить, выполнив следующие hello:

    get-help new-azurededicatedcircuit -detailed

### <a name="step-4-list-all-hello-expressroute-circuits"></a>Шаг 4. Перечислены все каналы ExpressRoute hello
Можно запустить hello `Get-AzureDedicatedCircuit` tooget список всех hello каналы ExpressRoute, созданные команды:

    Get-AzureDedicatedCircuit

Hello ответ будет что-нибудь подобное toohello в следующем примере:

    Bandwidth                        : 200
    CircuitName                      : MyTestCircuit
    Location                         : Silicon Valley
    ServiceKey                       : *********************************
    ServiceProviderName              : equinix
    ServiceProviderProvisioningState : NotProvisioned
    Sku                              : Standard
    Status                           : Enabled

Эти сведения в любое время можно получить с помощью hello `Get-AzureDedicatedCircuit` командлета. Делая hello вызова без параметров перечисляет все каналы hello. Ключ службы будут перечислены в hello *ServiceKey* поля.

    Get-AzureDedicatedCircuit

    Bandwidth                        : 200
    CircuitName                      : MyTestCircuit
    Location                         : Silicon Valley
    ServiceKey                       : *********************************
    ServiceProviderName              : equinix
    ServiceProviderProvisioningState : NotProvisioned
    Sku                              : Standard
    Status                           : Enabled

Подробное описание всех параметров hello можно получить, выполнив следующие hello:

    get-help get-azurededicatedcircuit -detailed

### <a name="step-5-send-hello-service-key-tooyour-connectivity-provider-for-provisioning"></a>Шаг 5. Отправка ключа tooyour подключения hello службы поставщика для подготовки
*ServiceProviderProvisioningState* предоставляет сведения о hello текущее состояние подготовки на стороне поставщика услуг hello. *Состояние* предоставляет hello состояния на стороне Microsoft hello. Дополнительные сведения о состояния подготовки схемы см. в разделе hello [рабочих процессов](expressroute-workflows.md#expressroute-circuit-provisioning-states) статьи.

При создании нового канала ExpressRoute hello схемы будут иметь hello следующие состояния:

    ServiceProviderProvisioningState : NotProvisioned
    Status                           : Enabled


Hello канала будет отправлена toohello при поставщика услуг подключения hello находится в процессе hello включить его для вас следующие состояния:

    ServiceProviderProvisioningState : Provisioning
    Status                           : Enabled

Канал ExpressRoute должна иметь следующие состояния для вас toobe может toouse hello его:

    ServiceProviderProvisioningState : Provisioned
    Status                           : Enabled


### <a name="step-6-periodically-check-hello-status-and-hello-state-of-hello-circuit-key"></a>Шаг 6. Периодически Проверьте состояние hello и состояние hello ключа канала hello
Это позволяет узнать, когда поставщик включил ваш канал. После настройки канала hello *ServiceProviderProvisioningState* будет отображаться как *инициализировано* как показано в следующий пример hello:

    Get-AzureDedicatedCircuit

    Bandwidth                        : 200
    CircuitName                      : MyTestCircuit
    Location                         : Silicon Valley
    ServiceKey                       : *********************************
    ServiceProviderName              : equinix
    ServiceProviderProvisioningState : Provisioned
    Sku                              : Standard
    Status                           : Enabled

### <a name="step-7-create-your-routing-configuration"></a>Шаг 7. Создание конфигурации маршрутизации
Ссылки toohello [expressroute в конфигурацию маршрутизации (Создание и изменение схемы пиринги)](expressroute-howto-routing-classic.md) статьи для получения пошаговых инструкций.

> [!IMPORTANT]
> Эти инструкции применяются только toocircuits, созданных с помощью службы поставщиков, предлагающих услуги подключений второго уровня. Если вы работаете с поставщиком, предлагающим услуги третьего уровня (обычно это IPVPN, например MPLS), то ваш поставщик услуг подключения выполнит настройку и управление конфигурацией самостоятельно.
> 
> 

### <a name="step-8-link-a-virtual-network-tooan-expressroute-circuit"></a>Шаг 8. Связывание виртуальной сети tooan канал ExpressRoute
Затем свяжите виртуальной сети tooyour канал ExpressRoute. См. слишком[ExpressRoute связывания каналов сетей toovirtual](expressroute-howto-linkvnet-classic.md) пошаговые инструкции. Получить виртуальные сети с помощью hello классической модели развертывания для ExpressRoute toocreate [Создание виртуальной сети для ExpressRoute](expressroute-howto-vnet-portal-classic.md).

## <a name="getting-hello-status-of-an-expressroute-circuit"></a>Получение состояния hello канал ExpressRoute
Эти сведения в любое время можно получить с помощью hello `Get-AzureCircuit` командлета. Делая hello вызова без параметров перечисляет все каналы hello.

    Get-AzureDedicatedCircuit

    Bandwidth                        : 200
    CircuitName                      : MyTestCircuit
    Location                         : Silicon Valley
    ServiceKey                       : *********************************
    ServiceProviderName              : equinix
    ServiceProviderProvisioningState : Provisioned
    Sku                              : Standard
    Status                           : Enabled

    Bandwidth                        : 1000
    CircuitName                      : MyAsiaCircuit
    Location                         : Singapore
    ServiceKey                       : #################################
    ServiceProviderName              : equinix
    ServiceProviderProvisioningState : Provisioned
    Sku                              : Standard
    Status                           : Enabled

Сведения о конкретных канал ExpressRoute можно получить, передав в качестве параметра вызова toohello hello ключа службы.

    Get-AzureDedicatedCircuit -ServiceKey "*********************************"

    Bandwidth                        : 200
    CircuitName                      : MyTestCircuit
    Location                         : Silicon Valley
    ServiceKey                       : *********************************
    ServiceProviderName              : equinix
    ServiceProviderProvisioningState : Provisioned
    Sku                              : Standard
    Status                           : Enabled


Подробное описание всех параметров hello можно получить, выполнив следующий пример hello:

    get-help get-azurededicatedcircuit -detailed

## <a name="modifying-an-expressroute-circuit"></a>Изменение канала ExpressRoute
Некоторые свойства канала ExpressRoute можно изменить, не повлияв на подключение.

Можно сделать hello без простоев следующие:

* включать и отключать надстройку ExpressRoute "Премиум" для канала ExpressRoute;
* Увеличение hello пропускной способностью вашего канала ExpressRoute при условии, что доступно емкости на порту hello. Обратите внимание, что понижение уровня полосы пропускания канала hello не поддерживается. 
* Изменение плана на основе данных, измеряемые tooUnlimited данных отслеживания использования hello. Обратите внимание, изменяющихся план контроля использования программных продуктов hello из данных tooMetered данных не поддерживается.
* Параметр *Allow Classic Operations*(Разрешить классические операции) можно включать и отключать.

См. toohello [часто задаваемые вопросы о ExpressRoute](expressroute-faqs.md) Дополнительные сведения об ограничениях и ограничениях.

### <a name="tooenable-hello-expressroute-premium-add-on"></a>tooenable hello ExpressRoute премиальное дополнение
Премиальное дополнение hello ExpressRoute можно включить для вашей существующей цепи с помощью hello, выполнив командлет PowerShell:

    Set-AzureDedicatedCircuitProperties -ServiceKey "*********************************" -Sku Premium

    Bandwidth                        : 1000
    CircuitName                      : TestCircuit
    Location                         : Silicon Valley
    ServiceKey                       : *********************************
    ServiceProviderName              : equinix
    ServiceProviderProvisioningState : Provisioned
    Sku                              : Premium
    Status                           : Enabled

Ваш канал получают hello ExpressRoute premium дополнительные возможности. Обратите внимание, что мы начнем выставления счетов для hello premium дополнительные возможности, как только команда hello успешно запущена.

### <a name="toodisable-hello-expressroute-premium-add-on"></a>toodisable hello ExpressRoute премиальное дополнение
> [!IMPORTANT]
> Эта операция может завершиться ошибкой, если вы используете ресурсы, которые больше, чем то, что разрешено для стандартной схемы hello.
> 
> 

#### <a name="considerations"></a>Рекомендации

* Необходимо убедиться, hello число цепи связанных toohello виртуальных сетей находится меньше 10, прежде чем понизить из premium toostandard. Если этого не сделать, ваш запрос на обновление завершится ошибкой, и вы будете по документу hello премиум-уровень.
* Все связи с виртуальными сетями в других геополитических регионах необходимо разорвать. Если этого не сделать, ваш запрос на обновление завершится ошибкой, и вы будете по документу hello премиум-уровень.
* Для частного пиринга таблица маршрутов должна содержать менее 4000 маршрутов. Если размер таблицы маршрутов больше 4000 маршрутов, сеанс BGP hello приведет к удалению и не будет снова включено, пока hello число префиксов, объявленных становится меньше 4 000.

#### <a name="disable-hello-premium-add-on"></a>Отключить надстройку premium hello
Премиальное дополнение hello ExpressRoute для вашей существующей схемы, можно отключить с помощью hello, выполнив командлет PowerShell:

    Set-AzureDedicatedCircuitProperties -ServiceKey "*********************************" -Sku Standard

    Bandwidth                        : 1000
    CircuitName                      : TestCircuit
    Location                         : Silicon Valley
    ServiceKey                       : *********************************
    ServiceProviderName              : equinix
    ServiceProviderProvisioningState : Provisioned
    Sku                              : Standard
    Status                           : Enabled



### <a name="tooupdate-hello-expressroute-circuit-bandwidth"></a>пропускная способность контура tooupdate hello ExpressRoute
Проверьте hello [часто задаваемые вопросы о ExpressRoute](expressroute-faqs.md) для поддерживаемых вариантов пропускной способности для поставщика. Можно выбрать любого размера, больше, чем размер hello вашей существующей цепи при условии, что позволяет физическому порту hello (на котором создается ваш канал).

> [!IMPORTANT]
> Канал ExpressRoute toorecreate hello возможно, если имеется существующий порт hello недостаточной мощности. Обновление схемы hello невозможно, если доступна без дополнительной емкости в этом расположении.
>
> Нельзя уменьшить hello пропускной способности канала ExpressRoute без прерывания. Понижение уровня полосы пропускания необходимо канал ExpressRoute toodeprovision hello и повторной инициализации новый канал ExpressRoute.
> 
> 

#### <a name="resize-a-circuit"></a>Изменение размера канала

После определения размера необходимо, можно использовать следующие команды tooresize hello ваш канал:

    Set-AzureDedicatedCircuitProperties -ServiceKey ********************************* -Bandwidth 1000

    Bandwidth                        : 1000
    CircuitName                      : TestCircuit
    Location                         : Silicon Valley
    ServiceKey                       : *********************************
    ServiceProviderName              : equinix
    ServiceProviderProvisioningState : Provisioned
    Sku                              : Standard
    Status                           : Enabled

Будут, ваш канал был размера на стороне Майкрософт hello. Необходимо обратиться к настройки подключения поставщика tooupdate на своей стороне toomatch это изменение. Обратите внимание, что мы начнем выставления счетов за hello обновлен параметр пропускной способности из этой точки.

Если появится следующая ошибка при увеличении пропускной способности канала hello hello, это означает наличие остается достаточная полоса пропускания hello физического порта, где создается вашей существующей цепи. Вы toodelete этой цепи и создайте новый канал hello размера, что нужно. 

    Set-AzureDedicatedCircuitProperties : InvalidOperation : Insufficient bandwidth available tooperform this circuit
    update operation
    At line:1 char:1
    + Set-AzureDedicatedCircuitProperties -ServiceKey ********************* ...
    + ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
        + CategoryInfo          : CloseError: (:) [Set-AzureDedicatedCircuitProperties], CloudException
        + FullyQualifiedErrorId : Microsoft.WindowsAzure.Commands.ExpressRoute.SetAzureDedicatedCircuitPropertiesCommand


## <a name="deprovisioning-and-deleting-an-expressroute-circuit"></a>Отзыв и удаление канала ExpressRoute

### <a name="considerations"></a>Рекомендации

* Необходимо удалить связь всех виртуальных сетей с каналом expressroute для этой операции toosucceed hello. Проверьте toosee, если у вас есть все виртуальные сети, связанным toohello канала, если операция завершается неудачно.
* Если состояние подготовки службы поставщика hello ExpressRoute канала **Provisioning** или **инициализировано** необходимо работать с ваш канал hello toodeprovision поставщика службы с их стороны. Она будет продолжать tooreserve ресурсы и выставлять вам счет на поставщика услуг hello завершения списания цепи hello и уведомляет нас.
* Если поставщик услуг hello отозваны hello канала (состояние подготовки поставщика услуг hello задано слишком**не инициализировано**) можно удалить цепь hello. Это остановит выставления счетов для hello схемы.

#### <a name="delete-a-circuit"></a>Удаление канала

Ваш канал ExpressRoute можно удалить, выполнив следующую команду hello:

    Remove-AzureDedicatedCircuit -ServiceKey "*********************************"



## <a name="next-steps"></a>Дальнейшие действия
После создания ваш канал, убедитесь, что hello следующие:

* [Создание и изменение маршрутизации для канала ExpressRoute](expressroute-howto-routing-classic.md)
* [Связать вашей виртуальной сети tooyour канал ExpressRoute](expressroute-howto-linkvnet-classic.md)

