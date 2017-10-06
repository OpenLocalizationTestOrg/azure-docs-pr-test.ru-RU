---
title: "часто задаваемые вопросы о ExpressRoute aaaAzure | Документы Microsoft"
description: "часто задаваемые вопросы о ExpressRoute Hello содержит сведения о поддерживаемых служб Azure, стоимость, данных и подключений, соглашения об уровне ОБСЛУЖИВАНИЯ, поставщиков и расположения, пропускной способности и дополнительные технические сведения."
documentationcenter: na
services: expressroute
author: cherylmc
manager: timlt
editor: 
ms.assetid: 09b17bc4-d0b3-4ab0-8c14-eed730e1446e
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/01/2017
ms.author: cherylmc
ms.openlocfilehash: c01e83f1497103e2fa85251dce6fb41844e46e9a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="expressroute-faq"></a>Вопросы и ответы по ExpressRoute

## <a name="what-is-expressroute"></a>Что такое ExpressRoute?

ExpressRoute — это служба Azure, которая позволяет создавать частные подключения между центрами обработки данных Microsoft и инфраструктурой вашей локальной среды или среды для совместной работы. Подключения ExpressRoute не выходят hello общедоступный Интернет и предложение большую безопасность, надежность и высокую скорость и снизить задержку, чем обычные подключения через Интернет hello.

### <a name="what-are-hello-benefits-of-using-expressroute-and-private-network-connections"></a>Что такое hello преимущества использования ExpressRoute и частных сетевых подключений

Подключения ExpressRoute не выходят hello общедоступный Интернет. Они предоставляют более поздней версии безопасности, надежности и скорости, с нижним и согласованное задержку, чем обычные подключения через Интернет hello. В некоторых случаях с помощью данных tootransfer подключения ExpressRoute между локальными устройствами и Azure может обеспечить существенное сокращение затрат.

### <a name="where-is-hello-service-available"></a>Где доступна служба hello?

Сведения о расположении этой службы и ее доступности см. на странице [Партнеры и расположения ExpressRoute](expressroute-locations.md).

### <a name="how-can-i-use-expressroute-tooconnect-toomicrosoft-if-i-dont-have-partnerships-with-one-of-hello-expressroute-carrier-partners"></a>Как использовать ExpressRoute tooconnect tooMicrosoft Если у меня нет соглашений ни с одним из партнеров-поставщиков ExpressRoute hello?

Можно указать регионального поставщика и перемещаться tooone подключения Ethernet обмена hello поддерживается расположения поставщика. Затем можно равноправное подключение с корпорацией Майкрософт в расположении поставщика hello. Проверьте hello последний раздел [ExpressRoute партнеров и расположения](expressroute-locations.md) toosee, если ваш поставщик услуг присутствует в любом расположении exchange hello. Затем вы можете заказать канал ExpressRoute через поставщик tooconnect hello службы tooAzure.

### <a name="how-much-does-expressroute-cost"></a>Сколько стоит ExpressRoute?

Сведения о ценах см. на [этой странице](https://azure.microsoft.com/pricing/details/expressroute/).

### <a name="if-i-pay-for-an-expressroute-circuit-of-a-given-bandwidth-does-hello-vpn-connection-i-purchase-from-my-network-service-provider-have-toobe-hello-same-speed"></a>Если я плачу для канал ExpressRoute данной пропускной способности hello VPN-подключение, которое я приобретаю у своего поставщика сетевых услуг имеют toobe hello такой же скоростью?

Нет. Вы можете приобрести у своего поставщика услуг VPN-подключение любой скорости. Ваш tooAzure подключения то, ограниченный toohello ExpressRoute цепь пропускной способностью.

### <a name="if-i-pay-for-an-expressroute-circuit-of-a-given-bandwidth-do-i-have-hello-ability-tooburst-up-toohigher-speeds-if-necessary"></a>Если я плачу за канал ExpressRoute данной пропускной способности, есть ли tooburst hello возможность копирования toohigher скорости при необходимости?

Да. Каналы ExpressRoute, настроенных tooallow tooburst времен tootwo hello ограничение пропускной способности превышением без дополнительных затрат. Проверьте у поставщика вашей службы toosee они поддерживают эту возможность.

### <a name="can-i-use-hello-same-private-network-connection-with-virtual-network-and-other-azure-services-simultaneously"></a>Можно ли использовать hello частных сетевых подключений с виртуальной сетью и другими службами Azure одновременно?

Да. Канал ExpressRoute после установки, можно tooaccess в виртуальной сети и другие службы Azure одновременно. Подключаться toovirtual сетей по частным путем пиринга hello и tooother служб по пути открытого пиринга hello.

### <a name="does-expressroute-offer-a-service-level-agreement-sla"></a>Предлагается ли с ExpressRoute соглашение об уровне обслуживания (SLA)?

Сведения см. в разделе hello [ExpressRoute соглашение об уровне ОБСЛУЖИВАНИЯ](https://azure.microsoft.com/support/legal/sla/) страницы.

## <a name="supported-services"></a>Поддерживаемые службы

ExpressRoute поддерживает [три домена маршрутизации](expressroute-circuit-peerings.md) для разных типов служб.

### <a name="private-peering"></a>Частный пиринг

* Виртуальные сети, в том числе все виртуальные машины и облачные службы

### <a name="public-peering"></a>Общедоступный пиринг

* Power BI
* Dynamics 365 for Finance and Operations (ранее — Dynamics AX Online).
* Большая часть hello Azure службы с hello следующие несколько исключений:
  * CDN
  * Нагрузочное тестирование Visual Studio Team Services
  * Многофакторная идентификация
  * Диспетчер трафика

### <a name="microsoft-peering"></a>Пиринг Майкрософт

* [Office 365](http://aka.ms/ExpressRouteOffice365)
* Приложения с участием клиентов Dynamics 365 (ранее — CRM Online):
  * Dynamics 365 for Sales;
  * Dynamics 365 for Customer Service;
  * Dynamics 365 for Field Service;
  * Dynamics 365 for Project Service.

## <a name="data-and-connections"></a>Данные и подключения

### <a name="are-there-limits-on-hello-amount-of-data-that-i-can-transfer-using-expressroute"></a>Существуют ограничения на hello объем данных, передаваемых посредством ExpressRoute?

Мы не устанавливаем ограничений на hello объем передачи данных. См. слишком[сведения о ценах](https://azure.microsoft.com/pricing/details/expressroute/) сведения о стоимости полосы пропускания.

### <a name="what-connection-speeds-are-supported-by-expressroute"></a>Какие скорости подключения поддерживаются в ExpressRoute?

Поддерживаемая пропускная способность:

50 Мбит/с, 100 Мбит/с, 200 Мбит/с, 500 Мбит/с, 1 Гбит/с, 2 Гбит/с, 5 Гбит/с, 10 Гбит/с

### <a name="which-service-providers-are-available"></a>Какие поставщики услуг доступны?

В разделе [ExpressRoute партнеров и расположения](expressroute-locations.md) hello список поставщиков услуг и расположения.

## <a name="technical-details"></a>Технические сведения

### <a name="what-are-hello-technical-requirements-for-connecting-my-on-premises-location-tooazure"></a>Что такое hello технические требования для подключения Мой tooAzure расположения в локальной среде?

Требования см. на [странице предварительных требований ExpressRoute](expressroute-prerequisites.md).

### <a name="are-connections-tooexpressroute-redundant"></a>Избыточны tooExpressRoute подключения?

Да. Каждый канал ExpressRoute имеет резервную пару кросс-подключений, настроенных tooprovide высокого уровня доступности.

### <a name="will-i-lose-connectivity-if-one-of-my-expressroute-links-fail"></a>Будет ли потеряно подключение в случае сбоя одной из моих связей ExpressRoute?

Подключение не будут потеряны, если один из hello кросс-соединений завершается ошибкой. Доступные toosupport hello сетевой нагрузки всегда резервное соединение. Кроме того, можно создать несколько каналов в другой пиринг расположение tooachieve сбоям.

### <a name="onep2plink"></a>Если я не совместно размещенных в облаке exchange и поставщику услуг предлагает точка-точка, нужно ли tooorder два физических соединений между my локальной сети и корпорацией Майкрософт?

Если ваш поставщик услуг могут устанавливать два виртуальных каналов Ethernet через hello физическое соединение, требуется только одно физическое соединение. Hello физическое подключение (например, оптоволоконные) завершается на слое 1 устройство (L1) (см. рисунок hello). виртуальные каналы Hello двумя Ethernet помечены разными ИД виртуальной ЛС, один для hello основной схемы и один для hello получателей. Эти идентификаторы виртуальной ЛС находятся в заголовок hello внешнего 802.1Q Ethernet. Заголовок Ethernet Hello внутреннее 802.1Q (не показано) является сопоставленных tooa конкретных [домен маршрутизации ExpressRoute](expressroute-circuit-peerings.md).

![](./media/expressroute-faqs/expressroute-p2p-ref-arch.png)

### <a name="can-i-extend-one-of-my-vlans-tooazure-using-expressroute"></a>Могу ли я расширить одну tooAzure Мои виртуальные локальные сети, с помощью ExpressRoute?

Нет. Мы не поддерживаем расширения подключений второго уровня до Azure.

### <a name="can-i-have-more-than-one-expressroute-circuit-in-my-subscription"></a>Можно ли получить в своей подписке несколько каналов ExpressRoute?

Да. Вы можете получить в своей подписке несколько каналов ExpressRoute. ограничение по умолчанию Hello устанавливается too10. Ограничение hello tooincrease технической поддержки Майкрософт, можно обратиться в случае необходимости.

### <a name="can-i-have-expressroute-circuits-from-different-service-providers"></a>Можно ли использовать каналы ExpressRoute от разных поставщиков услуг?

Да. Вы можете использовать каналы ExpressRoute от нескольких поставщиков услуг. Каждый канал ExpressRoute связан только с одним поставщиком услуг. 

### <a name="can-i-have-multiple-expressroute-circuits-in-hello-same-location"></a>Можно иметь несколько каналов ExpressRoute в hello местоположения?

Да. Можно иметь несколько каналов ExpressRoute, hello с таким же или разных поставщиков услуг в hello местоположения. Тем не менее, нельзя связать более одного toohello цепь ExpressRoute виртуальных сетевых из hello же расположение.

### <a name="how-do-i-connect-my-virtual-networks-tooan-expressroute-circuit"></a>Как подключаться моих виртуальных сетей tooan канал ExpressRoute

Основные этапы Hello

* Установить канал ExpressRoute и включить поставщик услуг hello.
* Вы или hello поставщика, необходимо настроить hello пиринга BGP (s).
* Свяжите канал ExpressRoute toohello hello виртуальной сети.

Дополнительные сведения см. в статье [Процедуры ExpressRoute для подготовки каналов и состояний каналов](expressroute-workflows.md).

### <a name="are-there-connectivity-boundaries-for-my-expressroute-circuit"></a>Существуют границы подключения к каналу ExpressRoute?

Да. Hello [ExpressRoute партнеров и расположения](expressroute-locations.md) статье представлен обзор границ подключения hello за канал ExpressRoute. Подключение за канал ExpressRoute находится в одной области геополитические ограниченный tooa. Подключение может быть toocross развернутое геополитических регионов путем включения расширенной функции hello ExpressRoute.

### <a name="can-i-link-toomore-than-one-virtual-network-tooan-expressroute-circuit"></a>Можно связать toomore более одной виртуальной сети tooan канал ExpressRoute?

Да. Можно установить настройки соединений too10 виртуальных сетей на стандартный канал ExpressRoute и копирование too100 на [канал ExpressRoute premium](#expressroute-premium). 

### <a name="i-have-multiple-azure-subscriptions-that-contain-virtual-networks-can-i-connect-virtual-networks-that-are-in-separate-subscriptions-tooa-single-expressroute-circuit"></a>У меня есть несколько подписок Azure, содержащих виртуальные сети. Можно ли подключить виртуальные сети, которые находятся в отдельных подписок tooa одного канала ExpressRoute?

Да. Вы можете разрешить копирование too10 других подписок Azure toouse одного канала ExpressRoute. Это ограничение может быть увеличена путем включения расширенной функции hello ExpressRoute.

Дополнительные сведения см. в статье [Подключение виртуальной сети к каналу ExpressRoute](expressroute-howto-linkvnet-arm.md).

### <a name="are-virtual-networks-connected-toohello-same-circuit-isolated-from-each-other"></a>Toohello подключенных виртуальных сетей, одному каналу изолированных друг от друга?

Нет. Из маршрутизации перспективы, все виртуальные сети toohello связанные одним каналом expressroute входят в одном домене маршрутизации hello и не изолированы друг от друга. Если требуется направить изоляции, то необходимо toocreate отдельный канал ExpressRoute.

### <a name="can-i-have-one-virtual-network-connected-toomore-than-one-expressroute-circuit"></a>Может иметь одну виртуальную сеть, подключенную toomore, чем один канал ExpressRoute?

Да. Можно связать одну виртуальную сеть с вверх toofour каналы ExpressRoute. Они должны быть заказаны из четырех разных [расположений ExpressRoute](expressroute-locations.md).

### <a name="can-i-access-hello-internet-from-my-virtual-networks-connected-tooexpressroute-circuits"></a>Получить доступ к Интернету hello из моей цепи tooExpressRoute подключенных виртуальных сетей?

Да. Если вы не разгласили маршруты по умолчанию (0.0.0.0/0) или префиксы Интернет-маршрутов через сеанс BGP hello, toohello Интернета можно подключаться из виртуальной сети, привязанной tooan канал ExpressRoute.

### <a name="can-i-block-internet-connectivity-toovirtual-networks-connected-tooexpressroute-circuits"></a>Можно заблокировать Интернет подключения toovirtual сетей подключенных tooExpressRoute цепи?

Да. Можно объявить о tooblock маршруты (0.0.0.0/0) по умолчанию все машины toovirtual подключения к Интернету, развернутые в виртуальной сети и направлять весь трафик через канал ExpressRoute hello.

При объявлении маршруты по умолчанию выполняется принудительный tooservices трафика по открытого пиринга (например, хранилище Azure и баз данных SQL Server) локальный tooyour назад. Вы должны будете tooconfigure вашей tooAzure маршрутизаторы tooreturn трафика через пути открытого пиринга hello или через Интернет hello.

### <a name="can-virtual-networks-linked-toohello-same-expressroute-circuit-talk-tooeach-other"></a>Связанные toohello виртуальных сетей можно одним каналом expressroute говорить tooeach другие?

Да. Виртуальные машины, развернутые в toohello подключенных виртуальных сетей, которые одним каналом expressroute могут взаимодействовать друг с другом.

### <a name="can-i-use-site-to-site-connectivity-for-virtual-networks-in-conjunction-with-expressroute"></a>Можно ли использовать подключения типа "сеть-сеть" для виртуальных сетей вместе с ExpressRoute?

Да. ExpressRoute может сосуществовать с VPN типа "сеть-сеть".

### <a name="can-i-move-a-virtual-network-from-site-to-site--point-to-site-configuration-toouse-expressroute"></a>Можно изменить виртуальную сеть с конфигурацией сеть сеть "и" точка сеть toouse ExpressRoute?

Да. Будет использовать шлюз ExpressRoute toocreate внутри виртуальной сети. Есть малого времени простоя, связанного с процессом hello.

### <a name="why-is-there-a-public-ip-address-associated-with-hello-expressroute-gateway-on-a-virtual-network"></a>Почему при общедоступный IP-адрес, связанный с hello шлюз ExpressRoute в виртуальной сети?

Hello общедоступный IP-адрес используется для управления только для внутреннего. Этот общедоступный IP-адрес не предоставляется toohello Интернета и не может использоваться нарушения безопасности виртуальной сети.

### <a name="what-do-i-need-tooconnect-tooazure-storage-over-expressroute"></a>Что делать tooconnect tooAzure хранилища требуется по ExpressRoute?

Вы должны установить канал ExpressRoute и настроить маршруты для общедоступного пиринга.

### <a name="are-there-limits-on-hello-number-of-routes-i-can-advertise"></a>Существуют ограничения на количество hello маршруты, которые можно разглашать?

Да. Мы принимаем too4000 префиксов маршрутов для частного пиринга и 200 для общедоступного пиринга и пиринг Майкрософт. Можно увеличить этот too10 000 маршрутов для частного пиринга при включении расширенной функции hello ExpressRoute.

### <a name="are-there-restrictions-on-ip-ranges-i-can-advertise-over-hello-bgp-session"></a>Существуют ограничения на диапазоны IP-адресов, которые можно разглашать hello сеанса BGP?

Мы не принимают частные префиксы (RFC1918) в открытый hello и сеанс пиринга BGP корпорации Майкрософт.

### <a name="what-happens-if-i-exceed-hello-bgp-limits"></a>Что происходит, если превысить ограничения BGP hello?

Сеансы BGP будут удалены. Они будут сброшены после hello число префиксов снизится предел hello.

### <a name="what-is-hello-expressroute-bgp-hold-time-can-it-be-adjusted"></a>Что такое hello времени хранения ExpressRoute BGP? Можно ли его изменить?

время ожидания Hello — 180. Hello активности сообщения отправляются каждые 60 секунд. Они являются фиксированные параметры hello стороны Майкрософт, не может быть изменено. Можно автоматически tooconfigure различных таймеров и параметры сеанса BGP hello будет согласовано соответствующим образом.

### <a name="after-i-advertise-hello-default-route-00000-toomy-virtual-networks-i-cant-activate-windows-running-on-my-azure-vms-how-tooi-fix-this"></a>После я объявления hello по умолчанию (0.0.0.0/0) маршрута toomy виртуальных сетей, не удается активировать Windows на виртуальных машин Azure. Как tooI устранить эту проблему?

Hello следующие шаги помогут распознать запроса активации hello Azure:

1. Установите для своего канала ExpressRoute открытый пиринг hello.
2. Выполнить уточняющий запрос DNS и поиска IP-адреса hello **kms.core.windows.net**
3. Hello службы управления ключами должен распознать запроса активации hello поступают из Azure и честь hello запроса. Выполните одно из следующих трех задач hello.

   * В локальной сети, маршрут hello трафик, поступающий для hello IP-адрес, полученный на задней tooAzure шаг 2 через hello открытого пиринга.
   * У вашей NSP поставщика hello перекрестием pin трафика задней tooAzure через hello открытого пиринга.
   * Создайте маршрут определяемых пользователем этой точки hello IP-адрес с Интернет в качестве следующего прыжка и примените его toohello подсетями, где находятся эти виртуальные машины.

### <a name="can-i-change-hello-bandwidth-of-an-expressroute-circuit"></a>Можно изменить hello пропускной способности канала ExpressRoute?

Да, можно выполнять tooincrease hello пропускной способностью вашего канала ExpressRoute в hello портал Azure или с помощью PowerShell. При наличии емкость hello физического порта, на котором был создан ваш канал, успешно внесенные изменения. 

Если внесенные изменения не удается, это означает, достаточно места, оставшегося на текущий порт hello и необходимо toocreate новый канал ExpressRoute с более высокой пропускной способностью hello, или что не имеет дополнительных мощностей в этом расположении, в этом случае вы не сможете пропускная способность tooincrease hello. 

Вы также будете иметь toofollow с вашей tooensure подключения поставщика обновляют ограничителей hello в пределах их увеличение пропускной способности сети toosupport hello. Уменьшить нельзя Однако hello пропускной способностью вашего канала ExpressRoute. Вы toocreate новый канал ExpressRoute с низкой пропускной способностью и удалить старый цепь hello.

### <a name="how-do-i-change-hello-bandwidth-of-an-expressroute-circuit"></a>Как изменить hello пропускной способности канала ExpressRoute?

Вы можете обновить hello пропускной способности hello каналов expressroute с помощью командлета hello REST API или PowerShell.

## <a name="expressroute-premium"></a>ExpressRoute Premium

### <a name="what-is-expressroute-premium"></a>Что такое ExpressRoute Premium?

ExpressRoute "премиум" — это совокупность hello следующие атрибуты:

* Увеличено маршрутизации таблицы с too10 4000 маршрутов, 000 маршрутов для частного пиринга.
* Увеличить число виртуальных сетей, которое может быть подключенным toohello канал ExpressRoute (по умолчанию — 10). Дополнительные сведения см. в разделе hello [ExpressRoute ограничения](#limits) таблицы.
* Подключение tooOffice 365 и Dynamics 365.
* Глобальный IPv6 по основной сети Microsoft hello. Теперь можно связать виртуальную сеть в одном геополитическом регионе с каналом ExpressRoute в другом регионе.<br>
    **Примеры**

    *  Можно связать виртуальную сеть, созданные в tooan Западная Европа канал ExpressRoute, созданных в Силиконовой долине. 
    *  Для открытого пиринга hello, префиксы из других регионов геополитические объявления таким образом, что можно соединиться, например, SQL Azure Западная Европа от канала в Силиконовой долине.


### <a name="limits"></a>Сколько виртуальных сетей можно связать канал ExpressRoute tooan включения ExpressRoute premium?

Hello следующих таблицах показаны ограничения ExpressRoute hello и hello число виртуальных сетей на канал ExpressRoute:

[!INCLUDE [ExpressRoute limits](../../includes/expressroute-limits.md)]

### <a name="how-do-i-enable-expressroute-premium"></a>Как включить ExpressRoute Premium?

ExpressRoute расширенные функции можно включить, если включена функция hello и завершить работу, обновив состояние канала hello. Можно включить ExpressRoute premium во время создания канала, или можно вызвать hello REST API или командлет PowerShell.

### <a name="how-do-i-disable-expressroute-premium"></a>Как отключить ExpressRoute Premium?

ExpressRoute premium можно отключить путем вызова hello REST API или командлет PowerShell. Необходимо убедиться, что перед отключением ExpressRoute premium масштабируются на ограничения по умолчанию потребностей toomeet подключения hello. Если эффективность использование масштабирует за пределы ограничения по умолчанию hello, hello запроса toodisable ExpressRoute premium завершается ошибкой.

### <a name="can-i-pick-and-choose-hello-features-i-want-from-hello-premium-feature-set"></a>Можно ли выбирать функции hello нужные из набора функций hello premium?

Нет. Не удается выбрать функции hello. При включении ExpressRoute Premium мы включаем все функции.

### <a name="how-much-does-expressroute-premium-cost"></a>Сколько стоит ExpressRoute Premium?

См. слишком[сведения о ценах](https://azure.microsoft.com/pricing/details/expressroute/) стоимость.

### <a name="do-i-pay-for-expressroute-premium-in-addition-toostandard-expressroute-charges"></a>Я плачу за ExpressRoute premium в дополнение к этому toostandard плата ExpressRoute?

Да. Взимается плата за premium ExpressRoute поверх плата за канал ExpressRoute и расходы, предусмотренного hello поставщика услуг подключения.

## <a name="expressroute-for-office-365-and-dynamics-365"></a>ExpressRoute для Office 365 и Dynamics 365

[!INCLUDE [expressroute-office365-include](../../includes/expressroute-office365-include.md)]

### <a name="how-do-i-create-an-expressroute-circuit-tooconnect-toooffice-365-services-and-dynamics-365"></a>Создание tooconnect цепь ExpressRoute служб tooOffice 365 и Dynamics 365?

1. Просмотрите hello [страница предварительных требований к ExpressRoute](expressroute-prerequisites.md) toomake убедиться, что требованиям hello.
2. выполнены tooensure, которая требует подключения, просмотрите список поставщиков услуг и расположения в hello hello [ExpressRoute партнеров и расположения](expressroute-locations.md) статьи.
3. Спланируйте действия по увеличению пропускной способности, просмотрев раздел [Сетевое планирование и настройка производительности для Office 365](http://aka.ms/tune/).
4. Выполните действия hello, перечисленных в tooset рабочие процессы hello копирование подключения [рабочие процессы ExpressRoute на предмет подготовки и состояния каналов](expressroute-workflows.md).

> [!IMPORTANT]
> Убедитесь, что включена ExpressRoute премиальное дополнение, при настройке службы связи tooOffice 365 и Dynamics 365.
> 
> 

### <a name="do-i-need-tooenable-azure-public-peering-tooconnect-toooffice-365-services-and-dynamics-365"></a>Зачем мне tooenable Azure открытый пиринг tooconnect tooOffice 365 services и Dynamics 365?

Нет, достаточно tooenable Пиринга Майкрософт. Проверки подлинности трафика tooAzure AD отправляется через Пиринг Майкрософт. 

### <a name="can-my-existing-expressroute-circuits-support-connectivity-toooffice-365-services-and-dynamics-365"></a>Поддерживает службы 365 tooOffice связи и Dynamics 365 моей существующей цепи ExpressRoute?

Да. К существующей цепи ExpressRoute может быть toosupport настроенное подключение tooOffice 365 служб. Убедитесь, что имеется достаточно мощности tooconnect tooOffice 365 services и включения премиальное дополнение. [Сетевое планирование и настройка производительности для Office 365](http://aka.ms/tune/) помогут вам спланировать потребности подключения. Также ознакомьтесь с разделом [Создание и изменение канала ExpressRoute](expressroute-howto-circuit-classic.md).

### <a name="what-office-365-services-can-be-accessed-over-an-expressroute-connection"></a>К каким службам Office 365 можно получить доступ через подключение ExpressRoute?

См. слишком[Office 365 URL-адреса и IP-адресов](http://aka.ms/o365endpoints) страницы текущий список служб, поддерживаемых через ExpressRoute.

### <a name="how-much-does-expressroute-for-office-365-services-and-dynamics-365-cost"></a>Каковы затраты на использование ExpressRoute для служб Office 365 и Dynamics 365?

Службы Office 365 и Dynamics 365 требуется toobe надстройки premium включена. В разделе hello [страница сведений о ценах](https://azure.microsoft.com/pricing/details/expressroute/) затрат.

### <a name="what-regions-is-expressroute-for-office-365-supported-in"></a>В каких регионах поддерживается ExpressRoute для Office 365?

Дополнительные сведения см. в [этой статье](expressroute-locations.md).

### <a name="can-i-access-office-365-over-hello-internet-even-if-expressroute-was-configured-for-my-organization"></a>Можно пользоваться Office 365 через hello Интернет, даже если был настроен ExpressRoute для моей организации?

Да. Конечные точки Office 365 службы должны быть доступны через Интернет, hello, несмотря на то, что для вашей сети, был настроен ExpressRoute. Если вы находитесь в расположении, которое является настроенным tooconnect tooOffice 365 services через ExpressRoute, нужно будет подключиться через ExpressRoute.

### <a name="can-i-access-office-365-us-government-community-gcc-services-over-an-azure-us-government-expressroute-circuit"></a>Можно ли получать доступ к службам сообщества Office 365 для государственных организаций США (GCC) через канал ExpressRoute Azure для государственных организаций США?

Да. Конечные точки службы Office 365 GCC должны быть доступны через hello Azure нам государственных ExpressRoute. Тем не менее при первой необходимости tooopen поддержка билета на hello предполагается tooadvertise tooMicrosoft префиксы hello Azure tooprovide портала. После устранения hello в службу поддержки вашей службы связи tooOffice 365 GCC будет установлено. 

### <a name="can-dynamics-365-for-operations-formerly-known-as-dynamics-ax-online-be-accessed-over-an-expressroute-connection"></a>Можно ли получить доступ к Dynamics 365 for Operations (ранее — Dynamics AX Online) через подключение ExpressRoute?

Да. [Dynamics 365 for Operations](https://www.microsoft.com/dynamics365/operations) размещается в Azure. Вы можете включить открытого пиринга Azure на ваш tooit tooconnect цепь ExpressRoute.

## <a name="route-filters-for-microsoft-peering"></a>Фильтры маршрутов для пиринга Майкрософт

### <a name="i-am-turning-on-microsoft-peering-for-hello-first-time-what-routes-will-i-see"></a>Я Включение пиринг Майкрософт для hello первый раз, какие маршруты появятся?

Вы не увидите никаких маршрутов. У вас есть tooattach фильтра tooyour цепи toostart префикс объявлений маршрутов. Инструкции см. в статье [Настройка фильтров маршрута для пиринга Майкрософт](how-to-routefilter-powershell.md).

### <a name="i-turned-on-microsoft-peering-and-now-i-am-trying-tooselect-exchange-online-but-it-is-giving-me-an-error-that-i-am-not-authorized-toodo-it"></a>Я включается пиринг Майкрософт и теперь я идет tooselect Exchange Online, но она дает мне ошибку, что я не авторизованные toodo его.

При использовании фильтров маршрутов любой клиент может включить пиринг Майкрософт. Тем не менее, для работы со службами Office 365, вы по-прежнему нужна tooget авторизованы с помощью Office 365.

### <a name="do-i-need-tooget-authorization-for-turning-on-dynamics-365-over-microsoft-peering"></a>Требуется ли для включения Dynamics 365 через пиринг Майкрософт tooget авторизации?

Нет, для этого авторизация Dynamics 365 не нужна. Вы можете создать правило и выбрать сообщество Dynamics 365 без авторизации.

### <a name="i-already-have-microsoft-peering-how-can-i-take-advantage-of-route-filters"></a>У меня уже есть пиринг Майкрософт, как воспользоваться фильтрами маршрутов?

Можно создать фильтр, выберите hello службы вы хотите toouse и подключите hello пиринг Майкрософт tooyour фильтра. Инструкции см. в статье [Настройка фильтров маршрута для пиринга Майкрософт](how-to-routefilter-powershell.md).

### <a name="i-have-microsoft-peering-at-one-location-now-i-am-trying-tooenable-it-at-another-location-and-i-am-not-seeing-any-prefixes"></a>У меня есть Microsoft пиринг в одном месте, теперь удается tooenable его в другом месте и я не вижу префиксы.

* Microsoft пиринг ExpressRoute каналов, которые были настроены предыдущих tooAugust 1, 2017 г. будет иметь все службы префиксов, объявленных через пиринг Майкрософт, даже если не определены фильтры маршрутов.

* Пиринг каналы ExpressRoute, настроенных в течение или после 1 августа 2017 г. Корпорация Майкрософт не будет иметь префиксы объявленных пока фильтр не будет подключено toohello канала. По умолчанию вы не увидите никаких префиксов.
