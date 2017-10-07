---
title: "Связывание виртуальной сети tooan канал ExpressRoute: PowerShell: классический: Azure | Документы Microsoft"
description: "Этот документ содержит общие сведения о том, как toolink виртуальных сетей (Vnet) tooExpressRoute цепи с помощью hello классической модели развертывания и PowerShell."
services: expressroute
documentationcenter: na
author: ganesr
manager: carmonm
editor: 
tags: azure-service-management
ms.assetid: 9b53fd72-9b6b-4844-80b9-4e1d54fd0c17
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/28/2017
ms.author: ganesr
ms.openlocfilehash: 6b8a01dcd4bbb9618ec3dd438cf0107538fb2a7a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="connect-a-virtual-network-tooan-expressroute-circuit-using-powershell-classic"></a>Подключиться с помощью PowerShell (классические) канал ExpressRoute tooan виртуальной сети
> [!div class="op_single_selector"]
> * [Портал Azure](expressroute-howto-linkvnet-portal-resource-manager.md)
> * [PowerShell](expressroute-howto-linkvnet-arm.md)
> * [Интерфейс командной строки Azure](howto-linkvnet-cli.md)
> * [Видео — портал Azure](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-a-connection-between-your-vpn-gateway-and-expressroute-circuit)
> * [PowerShell (классическая модель)](expressroute-howto-linkvnet-classic.md)
>

Эта статья поможет вам связать каналы ExpressRoute tooAzure виртуальных сетей (Vnet) с помощью hello классической модели развертывания и PowerShell. Виртуальные сети может быть либо в одной подписке hello или может быть частью другой подписки.

[!INCLUDE [expressroute-classic-end-include](../../includes/expressroute-classic-end-include.md)]

**О моделях развертывания Azure**

[!INCLUDE [vpn-gateway-clasic-rm](../../includes/vpn-gateway-classic-rm-include.md)]

## <a name="configuration-prerequisites"></a>Предварительные требования для настройки
1. Требуется последняя версия hello hello модули Azure PowerShell. Hello последнюю модули PowerShell можно загрузить из hello PowerShell раздел hello [страницу загрузок Azure](https://azure.microsoft.com/downloads/). Следуйте инструкциям в разделе hello [как tooinstall и настройка Azure PowerShell](/powershell/azure/overview) пошаговые инструкции о том, как tooconfigure модули Azure PowerShell hello toouse компьютера.
2. Требуется tooreview hello [необходимые компоненты](expressroute-prerequisites.md), [требования к маршрутизации](expressroute-routing.md), и [рабочих процессов](expressroute-workflows.md) перед началом настройки.
3. Вам потребуется активный канал ExpressRoute.
   * Следуйте инструкциям hello слишком[создать канал ExpressRoute](expressroute-howto-circuit-classic.md) и иметь поставщиком соединения включить hello канала.
   * Убедитесь, что для вашего канала настроен частный пиринг Azure. В разделе hello [Настройка маршрутизации](expressroute-howto-routing-classic.md) маршрутизации инструкции.
   * Убедитесь, что настроен открытого пиринга Azure и hello пиринга BGP между вашей сетью и Майкрософт работает так, чтобы можно было включить подключение начала до конца.
   * Вам необходимо иметь созданные и полностью подготовленные виртуальную сеть и шлюз виртуальной сети. Следуйте инструкциям hello слишком[Настройка виртуальной сети для ExpressRoute](expressroute-howto-vnet-portal-classic.md).

Объедините tooan виртуальных сетей too10 канал ExpressRoute. Все виртуальные сети должны быть в hello геополитические совпадают. Можно связать большее количество виртуальных сетей tooyour канал ExpressRoute или связать виртуальных сетей, которые находятся в других геополитических регионов, если вы включили hello ExpressRoute премиальное дополнение. Проверьте hello [часто задаваемые вопросы о](expressroute-faqs.md) Дополнительные сведения о премиальное дополнение hello.

## <a name="connect-a-virtual-network-in-hello-same-subscription-tooa-circuit"></a>Подключить виртуальную сеть в Привет одному каналу tooa подписки
Виртуальная сеть tooan канал ExpressRoute можно связать с помощью hello, выполнив командлет. Убедитесь, что шлюз виртуальной сети, hello создается и готов для связывания перед запуском командлета hello.

    New-AzureDedicatedCircuitLink -ServiceKey "*****************************" -VNetName "MyVNet"
    Provisioned

## <a name="connect-a-virtual-network-in-a-different-subscription-tooa-circuit"></a>Подключить виртуальную сеть в цепи tooa другой подписке
Канал ExpressRoute может совместно использоваться несколькими подписками. Следующий рисунок Hello показана простая схема способ управления доступом подходит для каналов ExpressRoute в нескольких подписках.

Каждый из hello маленькие облака в облако hello является используется toorepresent подписках, которые принадлежат toodifferent отделам в организации. Каждого из отделов hello hello организации можно использовать собственную подписку для развертывания их службы — но hello отделы могут совместно использовать одной ExpressRoute цепи tooconnect tooyour назад в локальной сети. Одному отделу (в этом примере: ИТ) может быть владельцем hello канал ExpressRoute. Другие подписки в hello организации можно использовать канал ExpressRoute hello.

> [!NOTE]
> Плата за подключение и пропускную способность для hello выделенного канала будет применен toohello владельца канала ExpressRoute. Все виртуальные сети совместно использовать hello же пропускной способности.
> 
> 

![Подключение между подписками](./media/expressroute-howto-linkvnet-classic/cross-subscription.png)

### <a name="administration"></a>Администрирование
Hello *владельца канала* — администратор hello/coadministrator hello подписки, в которой hello ExpressRoute создан канал. Hello владелец канала может разрешить администраторам или coadministrators другие подписки, который ссылается tooas *circuit пользователей*, toouse hello выделенный канал, которой они владеют. Цепи пользователям, авторизованным toouse hello организации ExpressRoute канала может связать hello виртуальную сеть в своей подписки toohello канал ExpressRoute после прав.

Владелец канала Hello имеет авторизаций toomodify и revoke power hello в любое время. Отмена авторизации приведет к удалению из hello подписки, доступ к которым был отозван всех ссылок.

### <a name="circuit-owner-operations"></a>Действия владельца канала

**Создание разрешения**

Hello владелец канала авторизует администраторов других подписок hello toouse hello указанного канала. В следующем примере hello Здравствуйте, администратор hello канала (ИТ компании Contoso) позволяет администратору hello из другой подписки (разработки тест) toolink копии схемы toohello tootwo виртуальных сетей. Здравствуйте, администратор Contoso ИТ данная возможность включена, указав идентификатор hello корпорации Майкрософт для разработки и тестирования. командлет Hello не отправляет по электронной почте toohello указанный идентификатор Майкрософт. Владелец канала Hello должен tooexplicitly уведомить hello другого владельца подписки, hello авторизации завершен.

    New-AzureDedicatedCircuitLinkAuthorization -ServiceKey "**************************" -Description "Dev-Test Links" -Limit 2 -MicrosoftIds 'devtest@contoso.com'

    Description         : Dev-Test Links
    Limit               : 2
    LinkAuthorizationId : **********************************
    MicrosoftIds        : devtest@contoso.com
    Used                : 0

**Просмотр разрешений**

Владелец канала Hello, можно просмотреть все разрешения, выданные для конкретного канала, выполнив следующий командлет hello.

    Get-AzureDedicatedCircuitLinkAuthorization -ServiceKey: "**************************"

    Description         : EngineeringTeam
    Limit               : 3
    LinkAuthorizationId : ####################################
    MicrosoftIds        : engadmin@contoso.com
    Used                : 1

    Description         : MarketingTeam
    Limit               : 1
    LinkAuthorizationId : @@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
    MicrosoftIds        : marketingadmin@contoso.com
    Used                : 0

    Description         : Dev-Test Links
    Limit               : 2
    LinkAuthorizationId : &&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&
    MicrosoftIds        : salesadmin@contoso.com
    Used                : 2


**Изменение разрешений**

Владелец канала Hello можно изменить параметры авторизации с помощью hello, выполнив командлет:

    Set-AzureDedicatedCircuitLinkAuthorization -ServiceKey "**************************" -AuthorizationId "&&&&&&&&&&&&&&&&&&&&&&&&&&&&"-Limit 5

    Description         : Dev-Test Links
    Limit               : 5
    LinkAuthorizationId : &&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&
    MicrosoftIds        : devtest@contoso.com
    Used                : 0


**Удаление разрешений**

Владелец канала Hello можно revoke и удаление авторизации пользователя toohello, выполнив следующий командлет hello:

    Remove-AzureDedicatedCircuitLinkAuthorization -ServiceKey "*****************************" -AuthorizationId "###############################"


### <a name="circuit-user-operations"></a>Действия пользователя канала

**Просмотр разрешений**

Hello цепи пользователя можно просмотреть параметры авторизации с помощью hello, выполнив командлет:

    Get-AzureAuthorizedDedicatedCircuit

    Bandwidth                        : 200
    CircuitName                      : ContosoIT
    Location                         : Washington DC
    MaximumAllowedLinks              : 2
    ServiceKey                       : &&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&
    ServiceProviderName              : equinix
    ServiceProviderProvisioningState : Provisioned
    Status                           : Enabled
    UsedLinks                        : 0

**Активация разрешений на связь**

пользователя канала Hello можно выполнить следующий командлет tooredeem hello авторизации:

    New-AzureDedicatedCircuitLink –servicekey "&&&&&&&&&&&&&&&&&&&&&&&&&&" –VnetName 'SalesVNET1'

    State VnetName
    ----- --------
    Provisioned SalesVNET1

В подписке hello связаны вновь для hello виртуальной сети, выполните следующую команду:

    New-AzureDedicatedCircuitLink -ServiceKey "*****************************" -VNetName "MyVNet"

## <a name="next-steps"></a>Дальнейшие действия
Дополнительные сведения об ExpressRoute см. в разделе hello [часто задаваемые вопросы о ExpressRoute](expressroute-faqs.md).

