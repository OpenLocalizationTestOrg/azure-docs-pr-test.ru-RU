---
title: "Общие сведения об ExpressRoute: Расширить вашей локальной сети tooAzure через подключение к частной | Документы Microsoft"
description: "Этот технический обзор ExpressRoute объясняет, как подключение ExpressRoute работает tooextend вашей локальной сети tooAzure через частного подключения."
documentationcenter: na
services: expressroute
author: cherylmc
manager: timlt
editor: 
ms.assetid: fd95dcd5-df1d-41d6-85dd-e91d0091af05
ms.service: expressroute
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/03/2017
ms.author: cherylmc
ms.openlocfilehash: 01301e1205c12ecdab34dc9d9b92bc7489e7826c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="expressroute-overview"></a>Обзор ExpressRoute
Microsoft Azure ExpressRoute позволяет расширять свои локальные сети в облако Microsoft hello через подключение к частной добиться с помощью поставщика услуг подключения. При помощи ExpressRoute можно устанавливать подключения tooMicrosoft облачные службы, такие как Microsoft Azure, Office 365 и Dynamics 365.

Это может быть подключение типа "любой к любому" (IP VPN), подключение Ethernet типа "точка-точка" или виртуальное кросс-подключение через поставщика услуг подключения на совместно используемом сервере. Подключения ExpressRoute не выходят hello общедоступный Интернет. Это позволяет toooffer подключения ExpressRoute дополнительные надежность, высокую скорость, меньшую задержку и большую безопасность по сравнению с обычными подключениями через Интернет hello. Сведения о том, как tooconnect tooMicrosoft вашей сети, с помощью ExpressRoute, в разделе [модели подключения к ExpressRoute](expressroute-connectivity-models.md).

![](./media/expressroute-introduction/expressroute-connection-overview.png)

## <a name="key-benefits"></a>Основные преимущества

* Подключении уровня 3 между вашей локальной сети и hello Microsoft Cloud через поставщика услуг подключения. Это может быть подключение типа "любой к любому" (IP VPN), подключение Ethernet типа "точка-точка" или виртуальное кросс-подключение через Ethernet Exchange.
* Облачные службы tooMicrosoft подключения по всем регионам в регионе геополитические hello.
* Службы tooMicrosoft глобальной связи по всем регионам с надстройками premium ExpressRoute.
* Динамическая маршрутизация между вашей сетью и Майкрософт по стандартным протоколам (BGP).
* Встроенная избыточность в каждом расположении пиринга для более высокой надежности.
* [Соглашения об уровне обслуживания](https://azure.microsoft.com/support/legal/sla/), обеспечивающие бесперебойное подключение.
* Поддержка QoS для Skype для бизнеса.

Дополнительные сведения см. в разделе hello [часто задаваемые вопросы о ExpressRoute](expressroute-faqs.md).

## <a name="features"></a>Функции

### <a name="layer-3-connectivity"></a>Подключение третьего уровня
Microsoft использует отраслевых стандартных динамической маршрутизации протокола BGP tooexchange маршруты между локальной сети, ваших экземпляров в Azure, а также Microsoft общедоступных адресов.  Мы устанавливаем несколько сеансов связи с вашей сетью по протоколу BGP для различных профилей трафика. Дополнительные сведения можно найти в hello [ExpressRoute цепи и домены маршрутизации](expressroute-circuit-peerings.md) статьи.

### <a name="redundancy"></a>Избыточность
Каждый канал ExpressRoute состоит из двух подключений tootwo Microsoft Enterprise edge маршрутизаторы (MSEEs) от поставщика услуг подключения hello / вашей сети edge. Корпорация Майкрософт требует двустороннего BGP соединения с поставщиком услуг подключения hello / стороны — один tooeach MSEE. Вы можете не toodeploy избыточных устройств или каналов Ethernet с вашей стороны. Тем не менее поставщиков услуг подключения используйте tooensure избыточных устройств, подключениями передаются tooMicrosoft избыточных способом. Конфигурации с резервированием подключение уровня 3 является обязательным для наших [соглашения об уровне ОБСЛУЖИВАНИЯ](https://azure.microsoft.com/support/legal/sla/) toobe допустимым.

### <a name="connectivity-toomicrosoft-cloud-services"></a>Облачные службы связи tooMicrosoft
[!INCLUDE [expressroute-office365-include](../../includes/expressroute-office365-include.md)]

Подключения ExpressRoute включить доступ toohello следующие службы:

* Службы Microsoft Azure
* Службы Microsoft Office 365
* Microsoft Dynamics 365

Вы можете посетить hello [часто задаваемые вопросы о ExpressRoute](expressroute-faqs.md) страницы подробный список служб, поддерживаемых через ExpressRoute.

### <a name="connectivity-tooall-regions-within-a-geopolitical-region"></a>Подключение tooall регионами геополитические области
Можно подключить tooMicrosoft в одном из наших [пиринга расположения](expressroute-locations.md) и получить доступ tooall области внутри области геополитические hello. 

Например если tooMicrosoft в Амстердам подключен через ExpressRoute, имеют доступ Microsoft tooall облачных служб, размещенных в Европе, Северной и Западной Европе. . В разделе hello [ExpressRoute партнеров и расположение пиринга](expressroute-locations.md) статье Обзор hello геополитических регионов, связанные регионы облака Майкрософт и соответствующими расположениями пиринга ExpressRoute.

### <a name="global-connectivity-with-expressroute-premium-add-on"></a>Глобальные подключения с надстройкой ExpressRoute Premium
Вы можете включить tooextend hello ExpressRoute premium надстройку возможность подключения геополитические за пределами границ. Например, если подключенный tooMicrosoft в Амстердам через ExpressRoute, будет иметь доступа Microsoft tooall облачные службы, размещенные во всех регионах в Здравствуй, мир! (исключаются national облаков). Получить доступ к службам, развернутым в Южной Америке и Австралии hello, так же, как можно получить доступ к Север hello и Западной Европе областей.

### <a name="rich-connectivity-partner-ecosystem"></a>Широкая экосистема партнеров по подключению
ExpressRoute обладает постоянно растущей экосистемой поставщиков услуг подключения и партнеров по SI. Можно ссылаться toohello [ExpressRoute поставщики и расположения](expressroute-locations.md) статьи для получения последних сведений hello.

### <a name="connectivity-toonational-clouds"></a>Подключение toonational облака
Корпорация Майкрософт управляет изолированными облачными средами для особых геополитических регионов и клиентских сегментов. См. toohello [ExpressRoute поставщики и расположения](expressroute-locations.md) страницы список национальных облака и поставщики.

### <a name="bandwidth-options"></a>Поддерживаемая пропускная способность
Каналы ExpressRoute можно приобрести для различной пропускной способности. Поддерживаемые значения пропускной способности перечислены в списке ниже. Убедиться, что toocheck быть со списком поддерживаемых вариантов пропускной способности, которым они предоставляют подключения toodetermine поставщика hello.

* 50 Мбит/с
* 100 Мбит/с
* 200 Мбит/с
* 500 Мбит/с
* 1 Гбит/с
* 2 Гбит/с
* 5 Гбит/с
* 10 Гбит/с

### <a name="dynamic-scaling-of-bandwidth"></a>Динамическое масштабирование пропускной способности
Можно увеличить hello пропускной способности канала ExpressRoute (на наилучшим возможным образом) без необходимости tootear работы подключений. 

### <a name="flexible-billing-models"></a>Гибкие модели тарификации
Вы можете выбрать оптимальную модель тарификации. Выбор между моделями hello выставления счетов, перечисленные ниже. Дополнительные сведения см. в разделе hello [часто задаваемые вопросы о ExpressRoute](expressroute-faqs.md).

* **Безлимитный тарифный план**. канал ExpressRoute Hello взимается по ежемесячную плату и передача всех входящих и исходящих данных не включены бесплатно бесплатно. 
* **Тарифный план с оплатой за трафик**. канал ExpressRoute Hello взимается по ежемесячную плату. Передача входящих данных предоставляется бесплатно. Передача исходящих данных оплачивается за каждый гигабайт исходящих данных. Скорость передачи данных зависит от региона.
* **Надстройка ExpressRoute Premium**. Hello ExpressRoute premium представляет собой надстройку над hello канал ExpressRoute. премиальное дополнение Hello ExpressRoute предоставляет hello следующие возможности: 
  * Для открытых и Azure открытого пиринга Azure из too10 4000 маршрутов, 000 маршрутов ограничивает увеличение маршрута.
  * глобальные подключения для служб. Канал ExpressRoute, созданные в любой области (за исключением national облаков) будет иметь tooresources доступ по какой другой области Здравствуй, мир!. Например, доступ к виртуальной сети, созданной в Западной Европе, может осуществляться через канал ExpressRoute, подготовленный в Кремниевой долине.
  * Повышенная число ссылок виртуальной сети в канал ExpressRoute из 10 tooa увеличить это предельное значение, в зависимости от пропускной способности hello hello канала.

## <a name="faq"></a>Часто задаваемые вопросы

Часто задаваемые вопросы о ExpressRoute см hello [часто задаваемые вопросы о ExpressRoute](expressroute-faqs.md).

## <a name="next-steps"></a>Дальнейшие действия

* Узнайте о [моделях подключения ExpressRoute](expressroute-connectivity-models.md).
* Узнайте больше о подключениях ExpressRoute и доменах маршрутизации. См. статью [Каналы ExpressRoute и домены маршрутизации](expressroute-circuit-peerings.md).
* Найти поставщика услуг. См. статью [Партнеры и одноранговые расположения ExpressRoute](expressroute-locations.md).
* Убедитесь, что выполнены все необходимые условия. См. статью [Предварительные требования и контрольный список для ExpressRoute](expressroute-prerequisites.md).
* См. требования к toohello для [маршрутизации](expressroute-routing.md), [NAT](expressroute-nat.md), и [QoS](expressroute-qos.md).
* Настройте подключение ExpressRoute.
  * [Создание канала ExpressRoute](expressroute-howto-circuit-portal-resource-manager.md)
  * [Настройка пиринга для канала ExpressRoute](expressroute-howto-routing-portal-resource-manager.md)
  * [Подключение виртуальной сети tooan канал ExpressRoute](expressroute-howto-linkvnet-portal-resource-manager.md)
* Дополнительные сведения о некоторых hello другой ключ [сетевые возможности](../networking/networking-overview.md) платформы Azure.
