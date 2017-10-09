---
title: "aaaConfigure виртуальной сети для кэша Redis Azure Premium | Документы Microsoft"
description: "Узнайте, как toocreate и управления ими поддержки виртуальной сети для экземпляров кэша Redis для Azure уровня Premium"
services: redis-cache
documentationcenter: 
author: steved0x
manager: douge
editor: 
ms.assetid: 8b1e43a0-a70e-41e6-8994-0ac246d8bf7f
ms.service: cache
ms.workload: tbd
ms.tgt_pltfrm: cache-redis
ms.devlang: na
ms.topic: article
ms.date: 05/15/2017
ms.author: sdanie
ms.openlocfilehash: fab715f4d9365ee4c2f8b89d2e2e58768c25b671
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-virtual-network-support-for-a-premium-azure-redis-cache"></a>Как tooconfigure виртуальная сеть поддерживает для кэша Redis Azure Premium
Кэш Azure Redis имеет разные предложения кэша, которые обеспечивают гибкость при hello Выбор размера кэша и функций, включая возможности уровня Premium кластеризации, сохраняемости и поддержки виртуальной сети. Виртуальная сеть — это частная сеть в облаке hello. При настройке экземпляра кэша Redis для Azure с виртуальной сетью, он не общедоступный и может осуществляться только из виртуальных машин и приложений в пределах hello виртуальной сети. В этой статье описано, как tooconfigure виртуальной сети поддерживают для экземпляра кэша Redis для Azure premium.

> [!NOTE]
> Кэш Redis для Azure поддерживает классические виртуальные сети и виртуальные сети Resource Manager.
> 
> 

Сведения о других функций кэша premium см. в разделе [уровня Premium кэша Redis Azure введение toohello](cache-premium-tier-intro.md).

## <a name="why-vnet"></a>Зачем использовать виртуальные сети?
[Виртуальной сети (VNet) Azure](https://azure.microsoft.com/services/virtual-network/) развертывание обеспечивает улучшенную защиту и изоляции для кэша Redis для Azure, а также подсетей, политики управления доступом, и другие функции toofurther ограничения доступа.

## <a name="virtual-network-support"></a>Поддержка виртуальной сети
Поддержка виртуальной сети (VNet) настраивается на hello **новый кэш Redis** колонке во время создания кэша. 

[!INCLUDE [redis-cache-create](../../includes/redis-cache-premium-create.md)]

После выбора ценовой категории premium можно настроить интеграцию Redis виртуальной сети, выбрав виртуальную сеть, которая находится в hello же подписке и расположении с кэшем. toouse новой виртуальной сети, создайте его, следуя указаниям hello [создать виртуальную сеть с помощью портала Azure hello](../virtual-network/virtual-networks-create-vnet-arm-pportal.md) или [Создание виртуальной сети (классические) с помощью портала Azure hello](../virtual-network/virtual-networks-create-vnet-classic-pportal.md) , а затем возвращают toohello **Новый кэш Redis** toocreate колонки и настроить кэш premium.

hello tooconfigure виртуальной сети для вашего нового кэша щелкните **виртуальной сети** на hello **новый кэш Redis** и, при необходимости выберите hello требуемого виртуальной сети из раскрывающегося списка hello.

![Виртуальная сеть][redis-cache-vnet]

Здравствуйте, выберите нужный подсети из hello **подсети** раскрывающегося списка и укажите hello требуемого **статический IP-адрес**. При использовании классического hello виртуальной сети **статический IP-адрес** поле является необязательным, и если не указано, одна выбирается из hello выбранные подсети.

> [!IMPORTANT]
> При развертывании tooa кэша Redis для Azure Resource Manager виртуальной сети, hello кэша должен быть в выделенной подсетью, не содержит другие ресурсы, за исключением экземпляров кэша Redis для Azure. Если попытка toodeploy кэш Azure Redis tooa подсети tooa диспетчера ресурсов виртуальной сети, которая содержит другие ресурсы, hello развертывания завершается ошибкой.
> 
> 

![Виртуальная сеть][redis-cache-vnet-ip]

> [!IMPORTANT]
> Azure резервирует некоторые IP-адреса в каждой подсети, которые нельзя использовать. Hello первый и последний IP-адреса подсетей hello зарезервированы для соответствия протоколу, а также три дополнительные адреса, используемые для служб Azure. Дополнительные сведения см. в разделе [Существуют ли ограничения на использование IP-адресов в пределах этих подсетей?](../virtual-network/virtual-networks-faq.md#are-there-any-restrictions-on-using-ip-addresses-within-these-subnets)
> 
> В добавление toohello IP-адреса виртуальной сети Azure инфраструктурой hello Redis для каждого экземпляра в hello подсети использует два IP-адреса на сегмент и один дополнительный IP-адрес для подсистемы балансировки нагрузки hello. Кэш некластеризованных считается toohave один сегмент.
> 
> 

После создания кэша hello hello конфигурации для hello виртуальной сети можно просмотреть, щелкнув **виртуальной сети** из hello **ресурсов меню**.

![Виртуальная сеть][redis-cache-vnet-info]

tooconnect tooyour redis для Azure — экземпляр кэша при использовании виртуальной сети, укажите имя узла hello кэша в строке подключения hello, как показано в следующий пример hello:

    private static Lazy<ConnectionMultiplexer> lazyConnection = new Lazy<ConnectionMultiplexer>(() =>
    {
        return ConnectionMultiplexer.Connect("contoso5premium.redis.cache.windows.net,abortConnect=false,ssl=true,password=password");
    });

    public static ConnectionMultiplexer Connection
    {
        get
        {
            return lazyConnection.Value;
        }
    }

## <a name="azure-redis-cache-vnet-faq"></a>Часто задаваемые вопросы о виртуальных сетях кэша Redis для Azure
После списка Hello содержит toocommonly ответы, вопросы и ответы о масштабировании кэша Redis для Azure hello.

* [Каковы распространенные ошибки конфигурации кэша Redis для Azure и виртуальных сетей?](#what-are-some-common-misconfiguration-issues-with-azure-redis-cache-and-vnets)
* [Как проверить, что кэш работает в виртуальной сети?](#how-can-i-verify-that-my-cache-is-working-in-a-vnet)
* [Можно ли использовать виртуальные сети в кэше уровня "Стандартный" или "Базовый"?](#can-i-use-vnets-with-a-standard-or-basic-cache)
* [Почему в одних подсетях не удается создать кэш Redis, а в других удается?](#why-does-creating-a-redis-cache-fail-in-some-subnets-but-not-others)
* [Каковы требования к свободному месту адрес подсети hello](#what-are-the-subnet-address-space-requirements)
* [Do all cache features work when hosting a cache in a VNET? (Все ли функции кэша работают, когда он размещен в виртуальной сети?)](#do-all-cache-features-work-when-hosting-a-cache-in-a-vnet)

## <a name="what-are-some-common-misconfiguration-issues-with-azure-redis-cache-and-vnets"></a>Каковы распространенные ошибки конфигурации кэша Redis для Azure и виртуальных сетей?
При размещении кэша Redis для Azure в виртуальной сети используются порты hello в следующей таблице hello. 

>[!IMPORTANT]
>Если порты hello в следующей таблице hello заблокированы, hello кэша может работать неправильно. При использовании кэш Azure Redis в виртуальной сети с одним или несколькими из этих портов заблокированных является наиболее распространенная проблема неправильной настройкой hello.
> 
> 

- [Обязательные порты для исходящего трафика](#outbound-port-requirements)
- [Обязательные порты для входящего трафика](#inbound-port-requirements)

### <a name="outbound-port-requirements"></a>Обязательные порты для исходящего трафика

Существует семь обязательных портов для исходящего трафика.

- При желании все исходящие подключения toohello Интернета можно сделать через клиент локального аудита устройства.
- Три из портов hello маршрутизацию трафика конечные точки tooAzure обслуживания хранилища Azure и Azure DNS.
- Hello оставшихся диапазоны портов и для внутренней связи подсети Redis. Для внутреннего обмена данными в подсети Redis не требуются правила группы безопасности сети в подсети.

| Порты | Направление | Транспортный протокол | Назначение | Локальный IP-адрес | Удаленный IP-адрес |
| --- | --- | --- | --- | --- | --- |
| 80, 443 |Исходящие |TCP |Зависимости Redis в службе хранилища Azure или PKI (Интернет) | (Подсеть Redis) |* |
| 53 |Исходящие |TCP/UDP |Зависимости Redis в DNS (Интернет/виртуальная сеть) | (Подсеть Redis) |* |
| 8443 |Исходящие |TCP |Внутренний обмен данными для Redis | (Подсеть Redis) | (Подсеть Redis) |
| 10221-10231 |Исходящие |TCP |Внутренний обмен данными для Redis | (Подсеть Redis) | (Подсеть Redis) |
| 20226 |Исходящие |TCP |Внутренний обмен данными для Redis | (Подсеть Redis) |(Подсеть Redis) |
| 13000-13999 |Исходящие |TCP |Внутренний обмен данными для Redis | (Подсеть Redis) |(Подсеть Redis) |
| 15000-15999 |Исходящие |TCP |Внутренний обмен данными для Redis | (Подсеть Redis) |(Подсеть Redis) |


### <a name="inbound-port-requirements"></a>Обязательные порты для входящего трафика

Существует восемь обязательных диапазонов портов для входящего трафика. Входящие запросы в этих диапазонов либо являются входящие данные от других служб, размещенных в hello одной виртуальной сети или внутренней toohello связь подсети Redis.

| Порты | Направление | Транспортный протокол | Назначение | Локальный IP-адрес | Удаленный IP-адрес |
| --- | --- | --- | --- | --- | --- |
| 6379, 6380 |Входящий трафик |TCP |Балансировка нагрузки Azure в tooRedis связи клиента, | (Подсеть Redis) |Виртуальная сеть, Azure Load Balancer |
| 8443 |Входящий трафик |TCP |Внутренний обмен данными для Redis | (Подсеть Redis) |(Подсеть Redis) |
| 8500 |Входящий трафик |TCP/UDP |Балансировка нагрузки Azure | (Подсеть Redis) |Azure Load Balancer |
| 10221-10231 |Входящий трафик |TCP |Внутренний обмен данными для Redis | (Подсеть Redis) |(Подсеть Redis) Azure Load Balancer |
| 13000-13999 |Входящий трафик |TCP |Обмен данными клиента tooRedis кластеры балансировки нагрузки Azure | (Подсеть Redis) |Виртуальная сеть, Azure Load Balancer |
| 15000-15999 |Входящий трафик |TCP |Балансировка нагрузки кластеры Azure в tooRedis связи клиента | (Подсеть Redis) |Виртуальная сеть, Azure Load Balancer |
| 16001 |Входящий трафик |TCP/UDP |Балансировка нагрузки Azure | (Подсеть Redis) |Azure Load Balancer |
| 20226 |Входящий трафик |TCP |Внутренний обмен данными для Redis | (Подсеть Redis) |(Подсеть Redis) |

### <a name="additional-vnet-network-connectivity-requirements"></a>Дополнительные требования к подключению к виртуальной сети

Существуют требования к сетевому подключению кэша Redis для Azure, которым виртуальная сеть изначально может не соответствовать. Кэш Azure Redis требует наличия всех hello следующие элементы toofunction должным образом в том случае, при использовании в виртуальной сети.

* Исходящее сетевое подключение tooAzure конечные точки хранилища по всему миру. Сюда входят конечных точках, найденных в hello hello экземпляр кэша Redis для Azure, а также конечные точки хранилища, расположенных в одном регионе **других** регионах Azure. Разрешить конечные точки хранилища Azure в следующих доменов DNS hello: *table.core.windows.net*, *blob.core.windows.net*, *queue.core.windows.net*и *file.core.windows.net*. 
* Исходящие сетевое подключение слишком*ocsp.msocsp.com*, *mscrl.microsoft.com*, и *crl.microsoft.com*. Подключение будет функциональность необходимые toosupport SSL.
* Hello конфигурацию DNS для виртуальной сети hello должны быть способны все конечные точки hello и домены упомянутые в более ранних точек hello. Эти требования DNS может выполняться за счет того, настроен и поддерживается для виртуальной сети hello допустимым инфраструктуры DNS.
* Исходящее сетевое подключение toohello следующие мониторинга Azure конечных точек, то разрешения в группе hello следующие домены DNS: shoebox2 black.shoebox2.metrics.nsatc.net, северо prod2.prod2.metrics.nsatc.net azglobal-black.azglobal.metrics.nsatc.net, azglobal восточно prod2.prod2.metrics.nsatc.net shoebox2-red.shoebox2.metrics.nsatc.net-red.azglobal.metrics.nsatc.net.

### <a name="how-can-i-verify-that-my-cache-is-working-in-a-vnet"></a>Как проверить, что кэш работает в виртуальной сети?

>[!IMPORTANT]
>При подключении экземпляра tooan кэш Azure Redis, размещенном в виртуальной сети, ваш кэш, который клиенты должны находиться в hello одной виртуальной сети, включая любые проверить работу приложений и средств диагностики обмен пакетами.
>
>

После настройки требований порта hello как описано в предыдущем разделе hello можно проверить, что кэш работает, выполнив следующие шаги hello.

- [Перезагрузите](cache-administration.md#reboot) все hello кэшировать узлов. Если все hello необходимые зависимости кэша становится недоступной (задокументированного в [входящего трафика требования к портам](cache-how-to-premium-vnet.md#inbound-port-requirements) и [требования исходящий порт](cache-how-to-premium-vnet.md#outbound-port-requirements)), hello кэша не будет возможности toorestart успешно.
- После узлов кэша hello были перезагружены (по данным состояние кэша hello в hello портал Azure), можно выполнить следующие тесты hello:
  - проверить связь с hello конечную точку кэша (через порт 6380) с компьютера, который находится в пределах hello одной виртуальной сети как hello кэшировать, с помощью [tcping](https://www.elifulkerson.com/projects/tcping.php). Например:
    
    `tcping.exe contosocache.redis.cache.windows.net 6380`
    
    Если hello `tcping` средство сообщает, что открыт порт hello, hello кэша для подключения от клиентов в hello виртуальной сети.

  - Tootest другим способом является toocreate тестового клиента кэша (который может быть простой консольного приложения с использованием StackExchange.Redis), подключается toohello кэша и добавляет и извлекает некоторые элементы из кэша hello. Установка hello образец клиентского приложения на виртуальной Машины, которая находится в одной виртуальной сети в качестве кэша hello hello и запустите его tooverify подключение toohello кэша.


### <a name="can-i-use-vnets-with-a-standard-or-basic-cache"></a>Можно ли использовать виртуальные сети в кэше уровня "Стандартный" или "Базовый"?
Виртуальные сети доступны только для кэшей уровня "Премиум".

### <a name="why-does-creating-a-redis-cache-fail-in-some-subnets-but-not-others"></a>Почему в одних подсетях не удается создать кэш Redis, а в других удается?
При развертывании tooa кэша Redis для Azure Resource Manager виртуальной сети hello кэша необходимо в выделенной подсетью, содержит никакой другой тип ресурса. Если попытаться сделать это toodeploy кэш Azure Redis tooa подсети виртуальной сети диспетчер ресурсов, которая содержит другие ресурсы, hello развертывания завершается ошибкой. Hello существующих ресурсов внутри hello подсети необходимо удалить, прежде чем создавать новый кэш Redis.

Можно развернуть несколько типов из ресурсов tooa классической виртуальной сети, пока у вас недостаточно IP доступных адресов.

### <a name="what-are-hello-subnet-address-space-requirements"></a>Каковы требования к свободному месту адрес подсети hello
Azure резервирует некоторые IP-адреса в каждой подсети, которые нельзя использовать. Hello первый и последний IP-адреса подсетей hello зарезервированы для соответствия протоколу, а также три дополнительные адреса, используемые для служб Azure. Дополнительные сведения см. в разделе [Существуют ли ограничения на использование IP-адресов в пределах этих подсетей?](../virtual-network/virtual-networks-faq.md#are-there-any-restrictions-on-using-ip-addresses-within-these-subnets)

В добавление toohello IP-адреса виртуальной сети Azure инфраструктурой hello Redis для каждого экземпляра в hello подсети использует два IP-адреса на сегмент и один дополнительный IP-адрес для подсистемы балансировки нагрузки hello. Кэш некластеризованных считается toohave один сегмент.

### <a name="do-all-cache-features-work-when-hosting-a-cache-in-a-vnet"></a>Do all cache features work when hosting a cache in a VNET? (Все ли функции кэша работают, когда он размещен в виртуальной сети?)
Когда кэш является частью виртуальной сети, только клиенты в hello виртуальной сети можно обращается к кэшу hello. В результате hello следующие возможности управления кэша не работают в данный момент.

* Консоль redis — поскольку консоль Redis выполняется в вашей локальной браузера, который находится за пределами hello виртуальной сети, она не может подключиться tooyour кэша.

## <a name="use-expressroute-with-azure-redis-cache"></a>Использование ExpressRoute с кэшем Redis для Azure
Клиенты могут подключаться [Azure ExpressRoute](https://azure.microsoft.com/services/expressroute/) цепь tootheir виртуальная сетевая инфраструктура, расширяя их tooAzure в локальной сети. 

По умолчанию только что созданный канал ExpressRoute не выполняет принудительное туннелирование (объявление маршрута по умолчанию, 0.0.0.0/0) в виртуальной сети. В результате исходящие подключения к Интернету может быть непосредственно из hello виртуальной сети и клиентских приложений, могут tooconnect tooother Azure конечных точек, включая кэша Redis для Azure.

Однако общая конфигурация клиента является toouse принудительного туннелирования (объявление маршрута по умолчанию) что вызывает исходящего Интернет трафика tooinstead потока в локальной среде. Этот поток трафика разбивает подключение с помощью кэша Azure Redis, если является hello исходящего трафика, а затем заблокировано в локальной, так, чтобы hello экземпляр кэша Redis для Azure не может toocommunicate с зависимостями.

Hello решением является toodefine один (или более) определяемых пользователем маршрутов (UDRs) на hello подсети, содержащей hello кэша Redis для Azure. UDR определяет маршруты конкретной подсети, которые будут соблюдаться вместо маршрут по умолчанию hello.

Если это возможно рекомендуется следующая конфигурация hello toouse:

* Конфигурация ExpressRoute Hello объявляет 0.0.0.0/0 и по умолчанию force туннелей всех исходящего трафика в локальной.
* Hello UDR применения toohello подсеть содержащий hello кэша Redis для Azure определяет 0.0.0.0/0 на работе маршрут для toohello трафик TCP/IP общедоступный Интернет; Например, установка hello следующего прыжка too'Internet тип ".

Hello воздействии этих шагов — что уровне подсети hello UDR имеет приоритет над hello ExpressRoute принудительного туннелирования, обеспечивая исходящие подключения к Интернету из hello кэша Redis для Azure.

Типичное использование сценарий из-за причин tooperformance не подключении экземпляра tooan кэша Redis для Azure из локального приложения, с помощью ExpressRoute (для достижения оптимальной производительности кэша Redis для Azure клиенты должны находиться в hello же регионе, что кэш Azure Redis hello).

>[!IMPORTANT] 
>Здравствуйте маршрутов, указанных в UDR **должен** быть достаточно точным, tootake приоритет через все маршруты, объявленные hello ExpressRoute конфигурацией. Hello следующий пример использует диапазон адресов широкий 0.0.0.0/0 hello и таким образом могут быть случайно переписаны объявлений маршрутов с помощью более конкретных диапазонов адресов.

>[!WARNING]  
>Кэш Azure Redis не поддерживается с конфигурациями ExpressRoute, **неправильно кросс объявлять маршруты из hello открытого пиринга путь toohello частным путем пиринга**. Конфигурации ExpressRoute, для которых настроен общедоступный пиринг, будут получать объявления маршрутов от корпорации Майкрософт для большого набора диапазонов IP-адресов Microsoft Azure. Если эти диапазоны адресов — это неправильно кросс объявляемых частным путем пиринга hello, hello происходит, все исходящие сетевые пакеты из экземпляра кэша Redis для Azure hello подсети локальной сети клиента tooa неправильно принудительного туннелирования инфраструктура. Этот сетевой поток нарушает работу кэша Redis для Azure. Hello решения toothis проблема заключается в toostop маршруты между рекламу от hello открытого пиринга путь toohello частным путем пиринга.


Справочные сведения об определяемых пользователем маршрутах см. в этом [обзоре](../virtual-network/virtual-networks-udr-overview.md).

Дополнительные сведения об ExpressRoute см. в статье [Технический обзор ExpressRoute](../expressroute/expressroute-introduction.md).

## <a name="next-steps"></a>Дальнейшие действия
Узнайте, как toouse более "премиум" кэша функции.

* [Уровень Premium кэша Redis Azure toohello введение](cache-premium-tier-intro.md)

<!-- IMAGES -->

[redis-cache-vnet]: ./media/cache-how-to-premium-vnet/redis-cache-vnet.png

[redis-cache-vnet-ip]: ./media/cache-how-to-premium-vnet/redis-cache-vnet-ip.png

[redis-cache-vnet-info]: ./media/cache-how-to-premium-vnet/redis-cache-vnet-info.png

