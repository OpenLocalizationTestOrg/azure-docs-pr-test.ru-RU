---
title: "aaaWorkflows для настройки канала ExpressRoute | Документы Microsoft"
description: "Эта страница поможет выполнить hello рабочих процессов для настройки канал ExpressRoute и пиринги"
documentationcenter: na
services: expressroute
author: cherylmc
manager: carmonm
editor: 
ms.assetid: 55e0418c-e0bf-44a7-9aa1-720076df9297
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/12/2017
ms.author: cherylmc
ms.openlocfilehash: 8e1dfc137401e0d6d53608ae6c8de0085e182eba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="expressroute-workflows-for-circuit-provisioning-and-circuit-states"></a>Процедуры ExpressRoute для подготовки каналов и состояний каналов
Эта страница поможет выполнить подготовку службы hello и рабочие процессы маршрутизации конфигурации на высоком уровне.

![](./media/expressroute-workflows/expressroute-circuit-workflow.png)

Hello ниже рисунок и соответствующие шаги Показать hello задачи должны следовать в порядке toohave ExpressRoute цепь подготовленных узел узел. 

1. С помощью PowerShell tooconfigure канал ExpressRoute. Следуйте инструкциям hello hello [каналы ExpressRoute создания](expressroute-howto-circuit-classic.md) Дополнительные сведения.
2. Порядок подключения поставщика услуг hello. Порядок действий может варьироваться. Обратитесь к поставщику услуг подключения, Дополнительные сведения о том, как tooorder подключения.
3. Убедитесь, что hello цепь была подготовлена успешно, проверяя состояние через PowerShell подготовки канал ExpressRoute hello. 
4. Настройте домены маршрутизации. Если ваш поставщик услуг подключения выполняет для вас управление третьего уровня, он настроит и маршрутизацию для вашего канала. Если поставщиком соединения только предлагает второго уровня службы, необходимо настроить маршрутизации по инструкциям, описанным в hello [требования к маршрутизации](expressroute-routing.md) и [конфигурации маршрутизации](expressroute-howto-routing-classic.md) страниц.
   
   * Включить открытого пиринга Azure — необходимо включить этот пиринг tooVMs tooconnect / облачных служб, развернутых в виртуальных сетей.
   * Включить частного пиринга Azure — необходимо включить частного пиринга Azure при желании tooconnect tooAzure службами, размещенными на общедоступных IP-адресов. Это требование tooaccess ресурсы Azure, если вы выбрали tooenable Маршрутизация по умолчанию для открытого пиринга Azure.
   * Включить пиринг Майкрософт — это tooaccess Office 365 и Dynamics 365, необходимо включить. 
     
     > [!IMPORTANT]
     > Необходимо убедиться, используется отдельный прокси / edge tooconnect tooMicrosoft, чем то, которое используется для hello hello Интернета. С помощью hello же краю для ExpressRoute и hello Интернет приведут асимметричного маршрутизации и причиной простоев подключения к сети.
     > 
     > 
     
     ![](./media/expressroute-workflows/routing-workflow.png)
5. Связывание виртуальной сети цепи tooExpressRoute - можно связать канал ExpressRoute tooyour виртуальных сетей. Следуйте инструкциям [toolink виртуальных сетей](expressroute-howto-linkvnet-arm.md) tooyour канала. Эти виртуальные сети могут быть либо в ту же подписку Azure канал ExpressRoute hello hello, или может быть в другую подписку.

## <a name="expressroute-circuit-provisioning-states"></a>Состояния подготовки канала ExpressRoute
У каждого канала ExpressRoute имеется два состояния.

* Состояние подготовки поставщика услуг
* Состояние

Состояние указывает на состояние подготовки Майкрософт. Это свойство имеет значение tooEnabled при создании канала Expressroute

состояние подготовки поставщика подключения Hello представляет состояние hello на стороне поставщика услуг подключения hello. Возможные состояния: *NotProvisioned* (Не подготовлен), *Provisioning* (Идет подготовка) и *Provisioned* (Подготовлен). Hello канал ExpressRoute должна находиться в состоянии подготовлена для вас toobe может toouse его.

### <a name="possible-states-of-an-expressroute-circuit"></a>Возможные состояния канала ExpressRoute
В этом разделе перечислены возможные состояния hello за канал ExpressRoute.

**В момент создания**

Вы увидите hello каналов expressroute в hello следующие состояния, как только вы запустите hello hello PowerShell командлет toocreate канал ExpressRoute.

    ServiceProviderProvisioningState : NotProvisioned
    Status                           : Enabled


**Если поставщика услуг подключения находится в процесс подготовки канала hello hello**

Вы увидите hello каналов expressroute в hello, как только вы следующие состояния передачи поставщика услуг подключения ключа toohello службы hello и запуска процесса инициализации hello.

    ServiceProviderProvisioningState : Provisioning
    Status                           : Enabled


**После завершения процесса подготовки hello поставщика услуг подключения**

Вы увидите hello канал ExpressRoute в следующие состояния сразу же после завершения hello процесса инициализации поставщика услуг подключения hello hello.

    ServiceProviderProvisioningState : Provisioned
    Status                           : Enabled

Подготовить и включить — hello цепи hello состояние может быть только в для вас toobe может toouse его. Если ваш поставщик предлагает услуги второго уровня, вы можете настроить маршрутизацию для канала, только если он находится в этом состоянии.

**Если поставщика услуг подключения отзывает hello канала**

Если вы запросили hello службы поставщика toodeprovision hello каналом expressroute, вы увидите цепи hello набора toohello следующие состояния после завершения hello отзыва процесса hello поставщика услуг.

    ServiceProviderProvisioningState : NotProvisioned
    Status                           : Enabled


Вы можете включить toore его при необходимости или запускать командлеты PowerShell toodelete hello канала.  

> [!IMPORTANT]
> При запуске hello toodelete hello командлет PowerShell канала, при операции hello подготовки или инициализировано hello ServiceProviderProvisioningState завершится ошибкой. Обратитесь к каналу ExpressRoute поставщика toodeprovision подключения hello сначала и затем удалить цепь hello. Корпорация Майкрософт будет toobill hello канала до запуска hello цепи hello toodelete командлета PowerShell.
> 
> 

## <a name="routing-session-configuration-state"></a>Состояние конфигурации сеанса маршрутизации
состояние подготовки BGP Hello позволяет узнать, если сеанс BGP hello была включена hello Microsoft edge. Hello состояния должна быть включена для вас toobe может toouse hello пиринга.

Это состояние сеанса BGP hello важные toocheck специально для пиринг Майкрософт. В дополнение toohello BGP состояние подготовки, имеется другое состояние — *объявленных открытых префиксов состояние*. Hello объявленных открытых префиксов состояние должно быть в *настроен* состояния, как для toobe сеанса BGP hello вверх и вашей маршрутизации toowork end-to-end. 

Если hello объявленных состояние открытого префикс имеет tooa *проверки необходимости* состояние сеанса BGP hello не включена, как hello объявленные префиксы не совпали hello как число, в каком-либо маршрутизации реестров hello. 

> [!IMPORTANT]
> Если hello объявленных открытых префиксов состояния находится в *Ручная проверка* состояние, необходимо открыть запрос в службу поддержки с [поддержки Майкрософт](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) и предоставить свидетельство своих IP-адресов hello объявленных вдоль с hello связанный номер автономной системы.
> 
> 

## <a name="next-steps"></a>Дальнейшие действия
* Настройте подключение ExpressRoute.
  
  * [Создайте канал ExpressRoute.](expressroute-howto-circuit-arm.md)
  * [Настройка маршрутизации](expressroute-howto-routing-arm.md)
  * [Связывание виртуальной сети tooan канал ExpressRoute](expressroute-howto-linkvnet-arm.md)

