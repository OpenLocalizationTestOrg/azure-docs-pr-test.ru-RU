---
title: "aaaIntroduction tooApp среды службы v1"
description: "Дополнительные сведения о функции hello v1 среды службы приложений, которая предоставляет единицы масштабирования безопасную, присоединенных к виртуальной сети, выделенных для выполнения всех приложений."
services: app-service
documentationcenter: 
author: stefsch
manager: erikre
editor: 
ms.assetid: 78e6d4f5-da46-4eb5-a632-b5fdc17d2394
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: ccompy
ms.openlocfilehash: 6e3cd1909b241887b5ec19412b9f7884d870cc3d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooapp-service-environment-v1"></a>Введение tooApp среды службы v1

> [!NOTE]
> Эта статья является о hello v1 среды службы приложений.  Имеется более новая версия hello среды службы приложений, удобнее toouse и выполняется на более мощный инфраструктуры. Дополнительные сведения о новой версии hello начинаться с hello toolearn [toohello введение среды службы приложений](../app-service/app-service-environment/intro.md).
> 

## <a name="overview"></a>Обзор
Среда службы приложений — это план обслуживания [Премиум][PremiumTier] в службе приложений Azure. Она обеспечивает полностью изолированную и выделенную среду для безопасного выполнения приложений службы приложений Azure в большом масштабе, включая [веб-приложения][WebApps], [мобильные приложения][MobileApps] и [приложения API][APIApps].  

Среда службы приложений идеально подходит для рабочих нагрузок приложений, требующих выполнения указанных ниже условий.

* Очень большой масштаб
* Изоляция и безопасный доступ к сети

Клиенты могут создавать несколько сред службы приложений как в одном, так и в нескольких регионах Azure.  Благодаря этому среды службы приложений идеально подходят для горизонтально масштабируемых уровней приложений без учета состояний, поддерживающих большие рабочие нагрузки RPS.

Среды службы приложений — это изолированное toorunning только одного клиента приложения и всегда развертываются в виртуальной сети.  Клиенты имеют возможность точного управления оба приложения входящий и исходящий сетевой трафик и приложений может устанавливать высокоскоростной безопасные соединения по корпоративным ресурсам локальной tooon виртуальных сетей.

Все статьи и как-для пользователя о среды службы приложений теперь доступны в hello [файл README для среды службы приложения](../app-service/app-service-app-service-environments-readme.md).

Обзор того, как включить высокий уровень масштабирования среды службы приложения и защиты доступа к сети см. в разделе hello [глубокое погружение AzureCon] [ AzureConDeepDive] на среды службы приложений!

Глубокое погружение в горизонтальное масштабирование с использованием нескольких средах службы приложения в статье hello о том, как toosetup [объем географически распределенных приложений][GeodistributedAppFootprint].

toosee, как показано в hello AzureCon подробная архитектура безопасности hello был настроен, см. в статье hello в первую очередь реализация [многоуровневая архитектура безопасности](app-service-app-service-environment-layered-security.md) с среды службы приложения.

Приложения, работающие в средах службы приложений, могут получать доступ через такие устройства, как брандмауэр веб-приложений (WAF).  Hello статьи на [Настройка WAF для среды службы приложения](app-service-app-service-environment-web-application-firewall.md) рассматриваются в этом сценарии. 

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="dedicated-compute-resources"></a>Выделенные вычислительные ресурсы
Все hello вычислительных ресурсов в среде службы приложений выделенных исключительно tooa одной подписке, и среды службы приложений можно настроить с помощью копирования (50) toofifty вычислительные ресурсы для монопольного использования одним приложением.

Среды службы приложений состоит из пула ресурсов вычислений переднего плана, а также вычислительных ресурсов один toothree рабочих пулов. 

внешний пул Hello содержит вычислительные ресурсы, ответственные за завершение запросов SSL как Балансировка нагрузки также автоматического запросов приложения в среде службы приложений. 

Каждый пул рабочих содержит вычислительные ресурсы, выделенные слишком[планы службы приложений][AppServicePlan], который в свою очередь содержать одно или несколько приложений службы приложений Azure.  Поскольку может существовать вверх toothree различных рабочих пулов в среде службы приложений, у вас есть hello гибкость toochoose различных вычислительных ресурсов для каждого рабочего пула.  

Например это позволяет toocreate пул один рабочий процесс с менее мощных вычислительных ресурсов для приложения службы планы предназначен для разработки и тестирования приложений.  Второй (или даже третий) рабочий пул может использовать более мощные вычислительные ресурсы, предназначенные для планов службы приложений с запущенными производственными приложениями.

Дополнительные сведения о hello количество вычислительных ресурсов доступны toohello переднего плана и рабочих пулов см. в разделе [как tooConfigure среды службы приложений][HowToConfigureanAppServiceEnvironment].  

Для сведения о доступных hello вычислений ресурсов размеры, поддерживаемые в среде службы приложений, обратитесь к hello [цены на службу приложения] [ AppServicePricing] страницы и просмотрите доступные параметры среды службы приложения hello в ценовой категории "премиум" hello.

## <a name="virtual-network-support"></a>Поддержка виртуальной сети
Среду службы приложений можно создать **либо** в виртуальной сети Azure Resource Manager, **либо** в виртуальной сети, использующей классическую модель развертывания. Вы можете [узнать больше о виртуальных сетях][MoreInfoOnVirtualNetworks].  Поскольку всегда существует среды службы приложений в виртуальной сети и точнее в подсети виртуальной сети, можно использовать оба входящего и исходящего сетевого взаимодействия технологии безопасности hello toocontrol виртуальных сетей.  

Среда службы приложений может быть доступной из Интернета с использованием общедоступного IP-адреса или из внутренней системы с использованием адреса внутренней подсистемы балансировки нагрузки.

Можно использовать [сетевых групп безопасности] [ NetworkSecurityGroups] toorestrict входящие связи toohello подсети, к которой находится среды службы приложений.  Это позволяет toorun приложения за вышестоящего устройств и служб, таких как брандмауэры приложения web и поставщики SaaS сети.

Приложения, должны также часто tooaccess корпоративным ресурсам, например внутренними базами данных и веб-службы.  Наиболее распространенный подход является toomake эти конечные точки доступны только toointernal сетевой трафик в виртуальной сети Azure.  После среды службы приложений присоединены к домену toohello одной виртуальной сети как hello внутренней службы, приложения, выполняющиеся в среде hello могли обращаться к ним, включая конечные точки с помощью [сайт-сайт] [ SiteToSite]и [Azure ExpressRoute] [ ExpressRoute] подключений.

Дополнительную информацию о работе с виртуальными сетями и локальными сетями среды службы приложений можно найти следующие статьи hello [архитектура сети][NetworkArchitectureOverview], [управление входящих подключений Трафик][ControllingInboundTraffic], и [безопасного соединения tooBackends][SecurelyConnectingToBackends]. 

## <a name="getting-started"></a>Приступая к работе
tooget к работе с среды службы приложения, в разделе [как tooCreate среды службы приложений][HowToCreateAnAppServiceEnvironment]

Все статьи и как-для пользователя для среды службы приложений теперь доступны в hello [файл README для среды службы приложения](../app-service/app-service-app-service-environments-readme.md).

Дополнительные сведения о платформе hello службе приложений Azure см. в разделе [службе приложений Azure][AzureAppService].

Обзор hello архитектура сети среды службы приложений см. в разделе hello [Обзор архитектуры сети] [ NetworkArchitectureOverview] статьи.

Сведения об использовании среды службы приложений при помощи ExpressRoute см. в следующей статьей hello [Express Route и среды службы приложения][NetworkConfigDetailsForExpressRoute].

[!INCLUDE [app-service-web-whats-changed](../../includes/app-service-web-whats-changed.md)]

[!INCLUDE [app-service-web-try-app-service](../../includes/app-service-web-try-app-service.md)]

<!-- LINKS -->
[PremiumTier]: http://azure.microsoft.com/pricing/details/app-service/
[MoreInfoOnVirtualNetworks]: https://azure.microsoft.com/documentation/articles/virtual-networks-faq/
[AppServicePlan]: http://azure.microsoft.com/documentation/articles/azure-web-sites-web-hosting-plans-in-depth-overview/
[HowToCreateAnAppServiceEnvironment]: http://azure.microsoft.com/documentation/articles/app-service-web-how-to-create-an-app-service-environment/
[AzureAppService]: http://azure.microsoft.com/documentation/articles/app-service-value-prop-what-is/
[WebApps]: http://azure.microsoft.com/documentation/articles/app-service-web-overview/
[MobileApps]: http://azure.microsoft.com/documentation/articles/app-service-mobile-value-prop-preview/
[APIApps]: http://azure.microsoft.com/documentation/articles/app-service-api-apps-why-best-platform/
[LogicApps]: http://azure.microsoft.com/documentation/articles/app-service-logic-what-are-logic-apps/
[AzureConDeepDive]:  https://azure.microsoft.com/documentation/videos/azurecon-2015-deploying-highly-scalable-and-secure-web-and-mobile-apps/
[GeodistributedAppFootprint]:  https://azure.microsoft.com/documentation/articles/app-service-app-service-environment-geo-distributed-scale/
[NetworkSecurityGroups]: https://azure.microsoft.com/documentation/articles/virtual-networks-nsg/
[SiteToSite]: https://azure.microsoft.com/documentation/articles/vpn-gateway-site-to-site-create/
[ExpressRoute]: http://azure.microsoft.com/services/expressroute/
[HowToConfigureanAppServiceEnvironment]:  http://azure.microsoft.com/documentation/articles/app-service-web-configure-an-app-service-environment/
[ControllingInboundTraffic]:  https://azure.microsoft.com/documentation/articles/app-service-app-service-environment-control-inbound-traffic/
[SecurelyConnectingToBackends]:  https://azure.microsoft.com/documentation/articles/app-service-app-service-environment-securely-connecting-to-backend-resources/
[NetworkArchitectureOverview]:  https://azure.microsoft.com/documentation/articles/app-service-app-service-environment-network-architecture-overview/
[NetworkConfigDetailsForExpressRoute]:  https://azure.microsoft.com/documentation/articles/app-service-app-service-environment-network-configuration-expressroute/
[AppServicePricing]: http://azure.microsoft.com/pricing/details/app-service/ 

<!-- IMAGES -->


