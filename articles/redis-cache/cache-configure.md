---
title: "aaaHow tooconfigure кэша Redis для Azure | Документы Microsoft"
description: "Обзор конфигурации Redis по умолчанию hello для кэша Redis для Azure и узнайте, как tooconfigure Azure Redis кэш экземпляров"
services: redis-cache
documentationcenter: na
author: steved0x
manager: douge
editor: tysonn
ms.assetid: d0bf2e1f-6a26-4e62-85ba-d82b35fc5aa6
ms.service: cache
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: cache-redis
ms.workload: tbd
ms.date: 08/22/2017
ms.author: sdanie
ms.openlocfilehash: 46bffb74cdf40e0e0a99c3a83dbe06d6fe1ea65b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-azure-redis-cache"></a>Как tooconfigure Redis для Azure кэша
В этом разделе описывается, как tooreview и обновление hello конфигурации для экземпляров кэша Redis для Azure и конфигурация сервера Redis по умолчанию hello обложки для экземпляров кэша Redis для Azure.

> [!NOTE]
> Дополнительные сведения о настройке и использовании функции кэша premium см. в разделе [как сохраняемости tooconfigure](cache-how-to-premium-persistence.md), [как кластеризация tooconfigure](cache-how-to-premium-clustering.md), и [как поддерживают tooconfigure виртуальной сети ](cache-how-to-premium-vnet.md).
> 
> 

## <a name="configure-redis-cache-settings"></a>Настройка параметров кэша Redis
[!INCLUDE [redis-cache-create](../../includes/redis-cache-browse.md)]

Параметры кэша Redis для Azure просмотреть и настроить на hello **кэша Redis** колонке с помощью hello **ресурсов меню**.

![Параметры кэша Redis](./media/cache-configure/redis-cache-settings.png)

Можно просмотреть и настроить следующие параметры с помощью hello hello **ресурсов меню**.

* [Обзор](#overview)
* [Журнал действий](#activity-log)
* [Управление доступом (IAM)](#access-control-iam)
* [Теги](#tags)
* [Диагностика и решение проблем](#diagnose-and-solve-problems)
* [Параметры](#settings)
    * [Ключи доступа](#access-keys)
    * [Дополнительные параметры](#advanced-settings)
    * [Помощник по кэшу Redis](#redis-cache-advisor)
    * [Масштабирование](#scale)
    * [Размер кластера Redis](#cluster-size)
    * [Сохраняемость данных Redis](#redis-data-persistence)
    * [Планирование обновлений](#schedule-updates)
    * [Георепликация](#geo-replication)
    * [Виртуальная сеть](#virtual-network)
    * [Брандмауэр](#firewall)
    * [Свойства](#properties)
    * [Блокировки](#locks)
    * [Сценарий автоматизации](#automation-script)
* [Администрирование](#administration)
    * [Импорт данных](#importexport)
    * [Экспорт данных](#importexport)
    * [Reboot](#reboot)
* [Мониторинг](#monitoring)
    * [Метрики Redis](#redis-metrics)
    * [Правила оповещения](#alert-rules)
    * [Диагностика](#diagnostics)
* [Настройки поддержки и устранения неполадок](#support-amp-troubleshooting-settings)
    * [Работоспособность ресурса](#resource-health)
    * [Новый запрос в службу поддержки](#new-support-request)


## <a name="overview"></a>Обзор

В разделе **Обзор** содержатся основные сведения о кэше, такие как имя, порты, ценовая категория, и выбранные метрики кэша.

### <a name="activity-log"></a>Журнал действий

Нажмите кнопку **журнал действий** tooview действия, выполняемые с вашего кэша. Можно также использовать tooexpand фильтрации этого представления tooinclude другие ресурсы. Дополнительные сведения об использовании журналов аудита см. в статье [Просмотр журналов действий для аудита действий с ресурсами](../azure-resource-manager/resource-group-audit.md). Дополнительные сведения о мониторинге событий кэша Redis для Azure см. в разделе [Операции и оповещения](cache-how-to-monitor.md#operations-and-alerts).

### <a name="access-control-iam"></a>Управление доступом (IAM)

Hello **(IAM) управления доступом к** раздел предоставляет поддержку для управления доступом на основе ролей (RBAC) в hello Azure toohelp портала организации соответствуют свои требования к управлению доступом просто и точно выполнять. Дополнительные сведения см. в разделе [управление доступом на основе ролей в hello портал Azure](../active-directory/role-based-access-control-configure.md).

### <a name="tags"></a>Теги

Hello **теги** раздел помогает организовать ресурсы. Дополнительные сведения см. в разделе [использование теги tooorganize ресурсам Azure](../azure-resource-manager/resource-group-using-tags.md).


### <a name="diagnose-and-solve-problems"></a>Диагностика и решение проблем

Нажмите кнопку **диагностики и устранения неполадок** toobe предоставлены общие проблемы и стратегии по их устранению.



## <a name="settings"></a>данных
Hello **параметры** раздел позволяет вам tooaccess и настройте следующие параметры кэша hello.

* [Ключи доступа](#access-keys)
* [Дополнительные параметры](#advanced-settings)
* [Помощник по кэшу Redis](#redis-cache-advisor)
* [Масштабирование](#scale)
* [Размер кластера Redis](#cluster-size)
* [Сохраняемость данных Redis](#redis-data-persistence)
* [Планирование обновлений](#schedule-updates)
* [Георепликация](#geo-replication)
* [Виртуальная сеть](#virtual-network)
* [Брандмауэр](#firewall)
* [Свойства](#properties)
* [Блокировки](#locks)
* [Сценарий автоматизации](#automation-script)



### <a name="access-keys"></a>Ключи доступа
Нажмите кнопку **ключи доступа** tooview или повторно создайте доступ hello ключи для вашего кэша. Эти ключи используются hello клиенты, подключающиеся tooyour кэша.

![Ключи доступа кэша Redis](./media/cache-configure/redis-cache-manage-keys.png)

### <a name="advanced-settings"></a>Дополнительные параметры
Hello следующие параметры настраиваются на hello **Дополнительные параметры** колонку.

* [Порты доступа](#access-ports)
* [Политики памяти](#memory-policies)
* [Уведомления пространства ключей (дополнительные параметры)](#keyspace-notifications-advanced-settings)

#### <a name="access-ports"></a>Порты доступа
Для новых кэшей без SSL порт по умолчанию отключен. tooenable hello не SSL порт, щелкните **нет** для **разрешить доступ только через SSL** на hello **Дополнительные параметры** колонку и нажмите кнопку **Сохранить**.

![Порты доступа кэша Redis](./media/cache-configure/redis-cache-access-ports.png)

<a name="maxmemory-policy-and-maxmemory-reserved"></a>
#### <a name="memory-policies"></a>Политики памяти
Hello **политику Maxmemory**, **зарезервировано maxmemory**, и **зарезервировано maxfragmentationmemory** параметры на hello **Дополнительные параметры**колонку настройки политик памяти hello для кэша hello.

![Политика максимальной памяти кэша Redis](./media/cache-configure/redis-cache-maxmemory-policy.png)

**Политика максимальной памяти** настраивает политику кэша hello вытеснения hello и позволяет toochoose из hello следующие политики вытеснения:

* `volatile-lru`-Это по умолчанию hello.
* `allkeys-lru`
* `volatile-random`
* `allkeys-random`
* `volatile-ttl`
* `noeviction`

Дополнительные сведения о политиках `maxmemory` см. в разделе [Eviction policies](http://redis.io/topics/lru-cache#eviction-policies) (Политики вытеснения) на сайте Redis.

Hello **maxmemory зарезервировано** параметр настраивает hello объем памяти в Мегабайтах, который зарезервирован для операции не из кэша, такие как репликации во время отработки отказа. Установка этого значения можно toohave более согласованной работы сервера Redis при зависит от нагрузки. Это значение должно быть выше при рабочих нагрузках с преобладанием записи. При резервировании памяти для таких операций она недоступна для хранения кэшированных данных.

Hello **maxfragmentationmemory зарезервировано** параметр настраивает hello объем памяти в Мегабайтах, который является зарезервированным tooaccommodate для фрагментации памяти. Установка этого значения можно toohave более согласованной работы сервера Redis при hello кэш не заполнится или закрыть соотношение фрагментации toofull и hello также высокого уровня. При резервировании памяти для таких операций она недоступна для хранения кэшированных данных.

Единственное tooconsider при выборе нового значения резервирование памяти (**зарезервировано maxmemory** или **maxfragmentationmemory зарезервировано**) является, как это изменение может повлиять на кэш, который уже выполняется с большие объемы данных в ней. Например если кэш 53 ГБ с 49 ГБ данных, а затем измените значение too8 hello резервирования ГБ, это будет удалена hello max доступной памяти для системы hello вниз too45 ГБ. Если ваши текущие `used_memory` или `used_memory_rss` значения выше, чем новый предел hello 45 ГБ, а затем hello система будет иметь tooevict данных, пока оба `used_memory` и `used_memory_rss` ниже 45 ГБ. Вытеснение может увеличить нагрузку на сервер и фрагментацию памяти. Дополнительные сведения о доступных метриках кэша, таких как `used_memory` и `used_memory_rss`, см. в разделе [Доступные метрики и интервалы отчетности](cache-how-to-monitor.md#available-metrics-and-reporting-intervals).

> [!IMPORTANT]
> Hello **зарезервировано maxmemory** и **maxfragmentationmemory зарезервировано** параметры доступны только для Standard и Premium кэширует.
> 
> 

#### <a name="keyspace-notifications-advanced-settings"></a>Уведомления пространства ключей (дополнительные параметры)
Redis на hello настраиваются уведомления keyspace **Дополнительные параметры** колонку. Уведомления Keyspace позволяют клиентам tooreceive уведомления при возникновении определенных событий.

![Дополнительные параметры кэша Redis](./media/cache-configure/redis-cache-advanced-settings.png)

> [!IMPORTANT]
> Пространство ключей уведомлений и hello **уведомления keyspace событий** параметра доступны только для кэша Standard и Premium.
> 
> 

Дополнительные сведения см. в статье [Redis Keyspace Notifications](http://redis.io/topics/notifications) (Уведомления пространства ключей Redis). Пример кода, в разделе hello [KeySpaceNotifications.cs](https://github.com/rustd/RedisSamples/blob/master/HelloWorld/KeySpaceNotifications.cs) файла в hello [Hello world](https://github.com/rustd/RedisSamples/tree/master/HelloWorld) образца.


<a name="recommendations"></a>
## <a name="redis-cache-advisor"></a>Помощник по кэшу Redis
Hello **Advisor кэша Redis** колонке приводятся рекомендации для кэша. Во время обычной работы не отображается никаких рекомендаций. 

![Рекомендации](./media/cache-configure/redis-cache-no-recommendations.png)

При любых условиях происходят во время операций hello вашего кэша, например использовании большого объема памяти, пропускной способности сети или нагрузки на сервер, на hello отображаются оповещение **кэша Redis** колонку.

![Рекомендации](./media/cache-configure/redis-cache-recommendations-alert.png)

Дополнительные сведения можно найти на hello **рекомендации** колонку.

![Рекомендации](./media/cache-configure/redis-cache-recommendations.png)

Вы можете отслеживать эти метрики на hello [диаграммы мониторинга](cache-how-to-monitor.md#monitoring-charts) и [диаграммы использования](cache-how-to-monitor.md#usage-charts) разделы hello **кэша Redis** колонку.

Каждая ценовая категория имеет различные ограничения для количества клиентских подключений, памяти и пропускной способности. Если в течение продолжительного периода времени кэш приближается к максимальной емкости для этих метрик, создается рекомендация. Дополнительные сведения о метрики hello и проверены hello ограничения **рекомендации** , см. в следующей таблице hello:

| Метрика "Кэш Redis" | Дополнительные сведения |
| --- | --- |
| Пропускная способность сети |[Производительность кэша — доступная пропускная способность](cache-faq.md#cache-performance) |
| Подключенные клиенты |[Конфигурация сервера Redis по умолчанию — максимальное количество клиентов](#maxclients) |
| Загрузка сервера |[Диаграммы использования — загрузка сервера Redis](cache-how-to-monitor.md#usage-charts) |
| Использование памяти |[Производительность кэша — размер](cache-faq.md#cache-performance) |

tooupgrade кэша, нажмите кнопку **обновление** toochange hello ценовой категории и [шкалы](#scale) кэша. Дополнительные сведения о выборе ценовой категории кэша см. в разделе [Какое предложение и размер кэша Redis мне следует использовать?](cache-faq.md#what-redis-cache-offering-and-size-should-i-use)


### <a name="scale"></a>Масштаб
Нажмите кнопку **шкалы** hello tooview или измените ценовую категорию для вашего кэша. Дополнительные сведения о масштабировании см. в разделе [как tooScale Redis для Azure кэшировать](cache-how-to-scale.md).

![Ценовая категория кэша Redis](./media/cache-configure/pricing-tier.png)

<a name="cluster-size"></a>

### <a name="redis-cluster-size"></a>Размер кластера Redis
Нажмите кнопку **размер кластера Redis (Предварительная версия)** размер кластера hello toochange для выполнения расширенной кэш с включенной кластеризацией.

> [!NOTE]
> Обратите внимание, что при hello Azure Redis кэша Premium уровня был выпущен tooGeneral доступности функции hello Redis размер кластера в настоящее время находится в предварительной версии.
> 
> 

![Размер кластера Redis](./media/cache-configure/redis-cache-redis-cluster-size.png)

размер кластера toochange hello, используйте ползунок hello, или введите число от 1 до 10 в hello **количества сегментов** текстовое поле и нажмите кнопку **ОК** toosave.

> [!IMPORTANT]
> Кластеризация Redis доступна только для кэша категории «Премиум». Дополнительные сведения см. в разделе [как tooconfigure кластеризации для кэша Redis Azure Premium](cache-how-to-premium-clustering.md).
> 
> 


### <a name="redis-data-persistence"></a>Сохраняемость данных Redis
Нажмите кнопку **сохраняемости данных Redis** tooenable, отключить или настроить сохранение данных кэша premium. Кэш Redis для Azure обеспечивает сохраняемость Redis на основе [RDB](cache-how-to-premium-persistence.md#configure-rdb-persistence) или [AOF](cache-how-to-premium-persistence.md#configure-aof-persistence).

Дополнительные сведения см. в разделе [как tooconfigure сохраняемости для кэша Redis Azure Premium](cache-how-to-premium-persistence.md).


> [!IMPORTANT]
> Сохраняемость данных Redis доступна только для кэшей категории «Премиум». 
> 
> 

### <a name="schedule-updates"></a>запланировать обновления
Hello **расписание обновления** колонке позволяет toodesignate периода обслуживания для обновления сервера Redis своего кэша. 

> [!IMPORTANT]
> Hello окна обслуживания применяется только tooRedis обновления сервера и не tooany Azure обновлений или обновления операционной системы toohello hello виртуальных машин, которые размещения кэша hello.
> 
> 

![запланировать обновления](./media/cache-configure/redis-schedule-updates.png)

toospecify периода обслуживания, проверьте дни hello требуемого укажите hello час запуска окна обслуживания для каждого дня и нажмите кнопку **ОК**. Обратите внимание, что период обслуживания hello в формате UTC. 

> [!IMPORTANT]
> Hello **расписание обновления** функция доступна только для кэши уровня Premium. Дополнительные сведения и указания см. в разделе о [планировании обновлений](cache-administration.md#schedule-updates) статьи, посвященной администрированию кэша Redis для Azure.
> 
> 

### <a name="geo-replication"></a>Георепликация

Hello **георепликации** колонке предоставляет механизм для связывания двух экземпляров кэша Redis для Azure уровня Premium. Один кэш используется в качестве основных связанный кэш hello и hello других получателей связанного кэширования hello. Hello дополнительных связанных кэш становится доступным только для чтения и репликации данных, является запись toohello основных кэш toohello дополнительных связанный кэш. Эта возможность может быть используется tooreplicate кэша в разных регионах Azure.

> [!IMPORTANT]
> **Георепликация** доступна только для кэшей категории "Премиум". Дополнительные сведения и инструкции см. в разделе [как tooconfigure географической репликации для кэша Azure Redis](cache-how-to-geo-replication.md).
> 
> 

### <a name="virtual-network"></a>Виртуальная сеть
Hello **виртуальной сети** раздел позволяет вам tooconfigure hello виртуальной сети настроек для кэша. Сведения о создании кэша premium с помощью виртуальной сети поддержки и обновления ее параметров, в разделе [как tooconfigure виртуальная сеть поддерживает для кэша Redis Azure Premium](cache-how-to-premium-vnet.md).

> [!IMPORTANT]
> Параметры виртуальной сети доступны только для кэшей уровня Премиум, которые были настроены с поддержкой виртуальной сети во время создания кэша. 
> 
> 

### <a name="firewall"></a>Брандмауэр

Нажмите кнопку **брандмауэра** tooview и настройка правил брандмауэра для кэша Redis Azure Premium.

![Брандмауэр](./media/cache-configure/redis-firewall-rules.png)

В правилах брандмауэра можно указать начало и конец диапазона IP-адресов. Если настроены правила брандмауэра, подключений клиентов только из hello указано диапазоны IP-адресов можно подключиться toohello кэша. При сохранении правила брандмауэра нет небольшая задержка перед hello правило вступает в силу. Обычно эта задержка не длится более одной минуты.

> [!IMPORTANT]
> Подключения из систем мониторинга кэша Redis для Azure всегда разрешены, даже если настроены правила брандмауэра.
> 
> Правила брандмауэра доступны только для кэшей уровня "Премиум".
> 
> 

### <a name="properties"></a>Свойства
Нажмите кнопку **свойства** tooview сведения о кэше, включая конечную точку кэша hello и порты.

![Свойства кэша Redis](./media/cache-configure/redis-cache-properties.png)

### <a name="locks"></a>Блокировки
Hello **блокирует** раздел позволяет вам toolock подписки, группы ресурсов или ресурсов tooprevent другим пользователям в организации от случайного удаления или изменения критическим ресурсам. Дополнительные сведения см. в статье [Блокировка ресурсов с помощью диспетчера ресурсов Azure](../azure-resource-manager/resource-group-lock-resources.md).

### <a name="automation-script"></a>Сценарий автоматизации

Нажмите кнопку **сценарий автоматизации** toobuild и экспортировать шаблон развернутых ресурсов для будущих развертываний. Дополнительные сведения о работе с шаблонами см. в статье [Развертывание ресурсов с использованием шаблонов Azure Resource Manager](../azure-resource-manager/resource-group-template-deploy.md).

## <a name="administration-settings"></a>Параметры администрирования
Здравствуйте, параметры в hello **администрирования** раздел разрешить hello tooperform следующие административные задачи для кэша. 

![Администрирование](./media/cache-configure/redis-cache-administration.png)

* [Импорт данных](#importexport)
* [Экспорт данных](#importexport)
* [Reboot](#reboot)


### <a name="importexport"></a>Импорт и экспорт
Импорт и экспорт является операцией управления данных кэша Redis для Azure, позволяющий tooimport и экспорт данных в кэше hello, Импорт и экспорт моментального снимка Redis кэша базы данных (RDB) из premium кэша tooa страничный большой двоичный объект в учетной записи хранилища Azure. Импорт и экспорт позволяет toomigrate между различными экземплярами кэша Redis для Azure или заполнения кэша hello с данными, перед использованием.

Импорт может быть используется toobring Redis совместимые RDB файлы с любого сервера Redis под управлением какой-либо облаке или в среде, включая Redis под управлением Linux, Windows или любого поставщика облачных служб, таких как Amazon Web Services и другие. Импорт данных — простой способ toocreate кэша заполнены данными. Во время процесса импорта hello кэша Redis для Azure hello RDB файлы загружаются из хранилища Azure в память и затем вставляет hello ключи в кэш hello.

Экспорт позволяет tooexport hello данные, хранящиеся в кэш Azure Redis tooRedis совместимые файлы RDB. Можно использовать данные toomove этого компонента из одной tooanother экземпляр кэша Redis для Azure или tooanother сервера Redis. Во время процесса экспорта hello временный файл создается на hello виртуальной Машины, что узлы hello экземпляр сервера кэша Redis для Azure, а hello файл отправленного toohello, назначенные учетной записи хранилища. После завершения операции экспорта hello состояние успеха или сбоя hello временный файл удаляется.

> [!IMPORTANT]
> Функция импорта и экспорта доступна только для кэшей категории "Премиум". Дополнительные сведения и указания см. в статье [Импорт и экспорт данных в кэше Redis для Azure](cache-how-to-import-export-data.md).
> 
> 

### <a name="reboot"></a>Reboot
Hello **перезагрузить** колонке позволяет tooreboot hello узлов кэша. Это перезагрузка дает вам tootest приложения для обеспечения устойчивости при наличии сбоя узла кэша.

![Reboot](./media/cache-configure/redis-cache-reboot.png)

При наличии кэша premium с включенной кластеризацией, можно выбрать какие сегменты кэша tooreboot hello.

![Reboot](./media/cache-configure/redis-cache-reboot-cluster.png)

tooreboot один или несколько узлов кэша, выберите узлы требуемого hello и нажмите кнопку **перезагрузки**. При наличии кэша premium с включенной кластеризацией выберите tooreboot сегментам hello и нажмите кнопку **перезагрузки**. Через несколько минут hello выбранные узлы перезагрузку и снова подключены к сети через несколько минут.

> [!IMPORTANT]
> Перезагрузка теперь доступна для всех ценовых категорий. Дополнительные сведения и указания см. в разделе о [перезагрузке](cache-administration.md#reboot) статьи, посвященной администрированию кэша Redis для Azure.
> 
> 


## <a name="monitoring"></a>Мониторинг

Hello **мониторинг** раздел позволяет вам tooconfigure диагностики и мониторинга для кэша Redis. Дополнительные сведения о кэше Redis для Azure наблюдение и диагностику см. в разделе [как toomonitor Redis для Azure кэшировать](cache-how-to-monitor.md).

![Диагностика](./media/cache-configure/redis-cache-diagnostics.png)

* [Метрики Redis](#redis-metrics)
* [Правила оповещения](#alert-rules)
* [Диагностика](#diagnostics)

### <a name="redis-metrics"></a>Метрики Redis
Нажмите кнопку **Redis метрики** слишком[Просмотр метрик](cache-how-to-monitor.md#view-cache-metrics) своего кэша.

### <a name="alert-rules"></a>Правила оповещения

Нажмите кнопку **предупреждения правила** tooconfigure оповещения на основе кэша Redis. Дополнительные сведения см. в статье [Как отслеживать кэш Redis для Azure](cache-how-to-monitor.md#alerts).

### <a name="diagnostics"></a>Диагностика

По умолчанию в Azure Monitor метрики кэша [хранятся в течение 30 дней](../monitoring-and-diagnostics/monitoring-overview-azure-monitor.md#store-and-archive), а затем удаляются. Щелкните toopersist показатели кэша более 30 дней **диагностики** слишком[Настройка учетной записи хранения hello](cache-how-to-monitor.md#export-cache-metrics) используется toostore диагностики кэша.

>[!NOTE]
>В дополнение tooarchiving toostorage метрик вашего кэша, вы также можете [поток их tooan концентратора событий или отправлять их tooLog Analytics](../monitoring-and-diagnostics/monitoring-overview-metrics.md#export-metrics).
>
>

## <a name="support--troubleshooting-settings"></a>Настройки поддержки и устранения неполадок
Здравствуйте, параметры в hello **поддержки + Устранение неполадок** раздела предоставляют параметры для устранения проблем с кэшем.

![Поддержка и устранение неполадок](./media/cache-configure/redis-cache-support-troubleshooting.png)

* [Работоспособность ресурса](#resource-health)
* [Новый запрос в службу поддержки](#new-support-request)

### <a name="resource-health"></a>Работоспособность ресурса
Служба **работоспособности ресурсов** отслеживает ресурс и сообщает, работает ли он как ожидалось. Дополнительные сведения о hello службы работоспособности ресурсов Azure см. в разделе [Обзор работоспособности ресурсов Azure](../resource-health/resource-health-overview.md).

> [!NOTE]
> Состояние ресурса — в настоящее время не удается tooreport о работоспособности hello экземплярами кэша Redis для Azure, размещенными в виртуальной сети. Дополнительные сведения см. в разделе [Все ли функции кэша работают, когда он размещен в виртуальной сети?](cache-how-to-premium-vnet.md#do-all-cache-features-work-when-hosting-a-cache-in-a-vnet).
> 
> 

### <a name="new-support-request"></a>Новый запрос на техническую поддержку
Нажмите кнопку **New поддержки запроса** tooopen запрос на поддержку своего кэша.





## <a name="default-redis-server-configuration"></a>Конфигурация сервера Redis по умолчанию
Новые экземпляры кэша Redis для Azure настроены следующие значения конфигурации Redis по умолчанию hello.

> [!NOTE]
> Параметры Hello в данном разделе нельзя изменить при помощи hello `StackExchange.Redis.IServer.ConfigSet` метод. Если этот метод вызывается с одним hello команды в этом разделе, выдается исключение аналогичные toohello следующие:  
> 
> `StackExchange.Redis.RedisServerException: ERR unknown command 'CONFIG'`
> 
> Все значения, которые можно настроить, например **максимум памяти политики**, настраиваемых с помощью hello портал Azure и управление из командной строки, таких как Azure CLI или PowerShell.
> 
> 

| Настройка | Значение по умолчанию | Описание |
| --- | --- | --- |
| `databases` |16 |количество баз данных по умолчанию Hello равно 16, но можно настроить разные номера на основе hello ценовой категории. <sup>1</sup> база данных по умолчанию hello-DB 0, можно выбрать его для подключения с помощью `connection.GetDatabase(dbid)` где `dbid` является числом в диапазоне от `0` и `databases - 1`. |
| `maxclients` |Зависит от ценового уровня hello<sup>2</sup> |Это максимальное количество подключенных клиентов, одновременно hello же hello времени. После достижения предела hello Redis закрывает все новые соединения hello вернуть ошибку «максимальное количество клиентов достигнут». |
| `maxmemory-policy` |`volatile-lru` |Политика Maxmemory является приветствия для как Redis выбирает, какие tooremove при `maxmemory` достигается (hello размер предложения, выбранный при создании кэша hello hello кэша). По умолчанию hello кэша Redis для Azure — параметр `volatile-lru`, который удаляет hello ключи со сроком действия, заданные с помощью алгоритма LRU. Этот параметр можно настроить в hello портал Azure. Дополнительные сведения см. в разделе [Политики памяти](#memory-policies). |
| `maxmemory-samples` |3 |toosave памяти, LRU и минимальный TTL алгоритмы являются примерные алгоритмы вместо точными. По умолчанию Redis проверок три ключей и получает hello один менее недавно использованного. |
| `lua-time-limit` |5 000 |Максимальное время выполнения сценария Lua в миллисекундах. При достижении максимального времени выполнения hello Redis регистрирует скрипт по-прежнему выполнения после hello максимально допустимое время, которое запускает tooreply tooqueries с ошибкой. |
| `lua-event-limit` |500 |Максимальный размер очереди событий сценариев. |
| `client-output-buffer-limit` `normalclient-output-buffer-limit` `pubsub` |0 0 032mb 8mb 60 |Hello ограничения буферов вывода клиентов можно использовать tooforce отключения клиентов, не считываются данные с сервера hello достаточно быстро для какой-либо причине (как правило, причиной является клиента Pub/Sub не могут использовать столь же быстро, как их производит издатель hello сообщения). Дополнительные сведения см. по ссылке [http://redis.io/topics/clients](http://redis.io/topics/clients). |

<a name="databases"></a>
<sup>1</sup>ограничение hello `databases` отличается для каждого кэша Azure Redis ценовой категории и может быть задано при создании кэша. Если не `databases` указан параметр во время создания кэша по умолчанию hello — 16.

* Кэши уровней Basic и Standard
  * C0 (250 МБ) кэша — копирование баз данных too16
  * C1 кэша (1 ГБ) — копирование баз данных too16
  * C2 кэша (2,5 ГБ) — копирование баз данных too16
  * C3 кэша (6 ГБ) — копирование баз данных too16
  * C4 кэша (13 ГБ) — копирование баз данных too32
  * C5 кэша (26 ГБ) — копирование баз данных too48
  * C6 кэша (53 ГБ) — копирование баз данных too64
* Кэши уровня Premium
  * P1 (6 ГБ — 60 ГБ) — копирование баз данных too16
  * P2 (13-130 ГБ) — копирование баз данных too32
  * P3 (26 ГБ — 260 ГБ) — копирование баз данных too48
  * P4 (53-530 ГБ) — копирование баз данных too64
  * Все кэши premium с кластером Redis enabled - Redis кластера поддерживает только использование базы данных 0, поэтому hello `databases` для любого кэша premium с кластером Redis включена равняется 1 и hello предела [выберите](http://redis.io/commands/select) команды не разрешено. Дополнительные сведения см. в разделе [необходимо toomake любые изменения toomy клиентского приложения toouse кластеризации?](cache-how-to-premium-clustering.md#do-i-need-to-make-any-changes-to-my-client-application-to-use-clustering)

Дополнительные сведения о базах данных см. в разделе [Что такое базы данных Redis?](cache-faq.md#what-are-redis-databases)

> [!NOTE]
> Hello `databases` параметр может быть настроена только во время создания кэша и только с помощью PowerShell, CLI или других клиентов управления. Пример настройки `databases` во время создания кэша с помощью PowerShell см. в разделе о командлете [New-AzureRmRedisCache](cache-howto-manage-redis-cache-powershell.md#databases).
> 
> 

<a name="maxclients"></a>
<sup>2</sup>`maxclients` отличается для каждой ценовой категории кэша Redis для Azure.

* Кэши уровней Basic и Standard
  * C0 (250 МБ) кэша - too256 подключения
  * C1 кэш (1 ГБ) — копирование too1, 000 подключений
  * C2 кэш (2,5 ГБ) — копирование too2, 000 подключений
  * C3 кэш (6 ГБ) — копирование too5, 000 подключений
  * C4 кэш (13 ГБ) — копирование too10, 000 подключений
  * C5 кэш (26 ГБ) — копирование too15, 000 подключений
  * C6 кэш (53 ГБ) — копирование too20, 000 подключений
* Кэши уровня Premium
  * P1 (6 ГБ — 60 ГБ) — копирование too7 подключения на скорости 500
  * P2 (13-130 ГБ) — копирование too15 000 подключений
  * P3 (26 ГБ — 260 ГБ) — копирование too30 000 подключений
  * P4 (53-530 ГБ) — копирование too40 000 подключений

> [!NOTE]
> Хотя каждый размер кэша позволяет *до* определенное количество соединений, каждого подключения tooRedis издержки связан. Примером таких накладных расходов могут служить загрузка ЦП и использование памяти в результате шифрования TLS/SSL. Hello максимальное количество подключений для размера кэша предполагается со слабой загрузкой кэша. Если загрузить из соединения издержки *, а также* нагрузки от операции клиента превышает лимит, определенный для системы hello, hello кэша могут возникать проблемы производительности, даже если не превышено ограничение числа подключений hello для hello текущий размер кэша.
> 
> 



## <a name="redis-commands-not-supported-in-azure-redis-cache"></a>Команды Redis не поддерживаются в кэше Redis для Azure
> [!IMPORTANT]
> Поскольку конфигурации и управления экземплярами кэша Redis для Azure управляется корпорацией Майкрософт, hello отключаются следующие команды. Если при попытке tooinvoke их, появляется сообщение об ошибке слишком`"(error) ERR unknown command"`.
> 
> * BGREWRITEAOF
> * BGSAVE
> * CONFIG
> * DEBUG
> * MIGRATE
> * Сохранить
> * SHUTDOWN
> * SLAVEOF
> * CLUSTER — команды записи для кластера отключены, однако допускается использование кластерных команд только для чтения.
> 
> 

Дополнительные сведения о командах Redis см. по ссылке [http://redis.io/commands](http://redis.io/commands).

## <a name="redis-console"></a>Консоль Redis
Можно безопасно выполнить команды tooyour экземпляров кэша Redis для Azure, с помощью hello **Redis консоли**, который доступен в hello портал Azure для всех уровней кэша.

> [!IMPORTANT]
> - Hello Redis консоль не работает с [VNET](cache-how-to-premium-vnet.md). Когда кэш является частью виртуальной сети, только клиенты в hello виртуальной сети можно обращается к кэшу hello. Поскольку консоль Redis выполняется в вашей локальной браузера, который находится за пределами hello виртуальной сети, она не может подключиться tooyour кэша.
> - В кэше Redis для Azure поддерживаются не все команды Redis. Список команд Redis, отключены для кэша Redis для Azure см. в разделе hello предыдущих [команды не поддерживается в кэше Redis для Azure Redis](#redis-commands-not-supported-in-azure-redis-cache) раздела. Дополнительные сведения о командах Redis см. по ссылке [http://redis.io/commands](http://redis.io/commands).
> 
> 

hello tooaccess Redis консоли, нажмите кнопку **консоли** из hello **кэша Redis** колонку.

![Консоль Redis](./media/cache-configure/redis-console-menu.png)

tooissue команды для экземпляра кэша, просто hello тип требуемой команды в консоль hello.

![Консоль Redis](./media/cache-configure/redis-console.png)


### <a name="using-hello-redis-console-with-a-premium-clustered-cache"></a>С помощью hello консоль Redis с расширенной кэш кластера

Когда кэш с помощью hello консоль Redis с расширенной кластера, могут выдавать команды tooa hello кэша в одном сегменте. tooissue конкретным сегментом tooa команды, сначала подключиться toohello нужному сегменту, щелкнув его в выбора сегментов hello.

![Консоль Redis](./media/cache-configure/redis-console-premium-cluster.png)

При попытке tooaccess ключ, который хранится в другой сегмент, чем hello подключенных сегментов, появляется ошибка сообщение аналогичные toohello следующие сообщения.

```
shard1>get myKey
(error) MOVED 866 13.90.202.154:13000 (shard 0)
```

В предыдущем примере hello сегмент 1 — hello выбранного сегментов, но `myKey` находится в сегмент 0, как указано в hello `(shard 0)` часть сообщение hello. В этом примере tooaccess `myKey`выберите сегмент 0 с помощью hello выбора сегментов, а затем команду hello требуемого проблему.


## <a name="move-your-cache-tooa-new-subscription"></a>Переместить в новую подписку tooa кэша
Можно переместить в новую подписку tooa кэша, щелкнув **переместить**.

![Перемещение кэша Redis](./media/cache-configure/redis-cache-move.png)

Сведения о перемещении ресурсов от одного ресурса группы tooanother и из одной подписки tooanother см. в разделе [переместить группу ресурсов toonew ресурсов или подписку](../azure-resource-manager/resource-group-move-resources.md).

## <a name="next-steps"></a>Дальнейшие действия
* Дополнительные сведения о работе с командами Redis см. в разделе [Как выполнять команды Redis?](cache-faq.md#how-can-i-run-redis-commands)

