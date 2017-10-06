---
title: "подписки aaaAzure ограничения и квоты | Документы Microsoft"
description: "В этой статье приводится перечень наиболее распространенных ограничений, относящихся к подписке Azure и различным службам, квот и границ. Сюда входят сведения на как tooincrease ограничивает вместе с максимальные значения."
services: 
documentationcenter: 
author: rothja
manager: jeffreyg
editor: 
tags: billing
ms.assetid: 60d848f9-ff26-496e-a5ec-ccf92ad7d125
ms.service: billing
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/21/2017
ms.author: byvinyal
ms.openlocfilehash: a754d56124520791254ab8f1729808f0750ff222
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-subscription-and-service-limits-quotas-and-constraints"></a>Подписка Azure, границы, квоты и ограничения службы
В этом документе перечислены некоторые наиболее распространенные Microsoft Azure пределы hello, которые иногда называются квоты. Этот документ на текущий момент охватывает не все службы Azure. Со временем hello будут развертываться и обновлении списков toocover дополнительные платформы hello.

Перейдите на страницу [расценкам Azure](https://azure.microsoft.com/pricing/) toolearn Дополнительные сведения о ценах. Нет, можно оценить затраты с помощью hello [калькулятор цен](https://azure.microsoft.com/pricing/calculator/) или посетив hello цены страница сведений для службы (например, [виртуальных машин Windows](https://azure.microsoft.com/pricing/details/virtual-machines/#Windows)). Затраты на управление toohelp советы см. в разделе [предотвратить непредвиденные затраты на управление затрат и выставлению счетов Azure](billing/billing-getting-started.md).

> [!NOTE]
> Если хотите tooraise hello ограничение или квоту выше hello **ограничение по умолчанию**, [откройте запрос поддержки сети клиента без платы](azure-supportability/resource-manager-core-quotas-request.md). Hello ограничения не может быть изменен выше hello **максимальный предел** значение, показанное в следующей таблице hello. При наличии не **максимальный предел** столбец, затем hello ресурса не имеет настраиваться ограничения. 
> 
> Бесплатная пробная версия подписки не предусматривает возможность увеличения ограничения и квоты. Если у вас есть бесплатная пробная версия, можно обновить tooa [Оплата по мере использования](https://azure.microsoft.com/offers/ms-azr-0003p/) подписки. Дополнительные сведения см. в разделе [обновление бесплатная пробная версия tooPay как-то-Go](billing/billing-upgrade-azure-subscription.md).
> 

## <a name="limits-and-hello-azure-resource-manager"></a>Ограничения и hello диспетчера ресурсов Azure
Теперь стало возможно toocombine несколько ресурсов Azure в tooa одной группы ресурсов Azure. При использовании групп ресурсов перейдет под управление ограничениями, один раз были глобальными на региональном уровне с hello диспетчера ресурсов Azure. Дополнительные сведения о группах ресурсов Azure см. в статье [Общие сведения о диспетчере ресурсов Azure](azure-resource-manager/resource-group-overview.md).

В пределах hello ниже новой таблицы был добавлен tooreflect любые различия в пределах при использовании hello диспетчера ресурсов Azure. Например, имеется таблица **Ограничения подписки** и таблица **Ограничения подписки — Azure Resource Manager**. Если ограничение применяется tooboth сценариев, только отображается в первой таблице hello. Если не указано иное, ограничения глобальны во всех областях.

> [!NOTE]
> Он является tooemphasize важные квоты для ресурсов в группах ресурсов Azure в регионе доступных по подписке что находятся не каждой подписки, как hello службы управления квоты. В качестве примера используем квоты ядер ЦП. Если необходимо увеличить квоту с поддержкой ядер toorequest toodecide необходимо как число ядер, которые вы хотите toouse в определенных регионах, а затем внесите конкретный запрос для группы ресурсов Azure основные квоты суммы hello и области, которые вы хотите. Таким образом Если вам требуется toouse 30 ядер в Западной Европе toorun приложения существует; в частности, следует запросить 30 ядер в Западной Европе. Но не нужно увеличить в какой другой области Основные квоты — только Западной Европе будет иметь hello 30-core квоты.
> <!-- -->
> В результате может оказаться полезным tooconsider решить, какие группы ресурсов Azure квот должен toobe для рабочей нагрузки в любом одной области и запрос, сумма в каждом регионе, в который вы собираетесь развертывания. Подробные сведения об определении текущих квот для конкретных регионов см. в разделе [Устранение неполадок развертывания](resource-manager-common-deployment-errors.md).
> 
> 

## <a name="service-specific-limits"></a>Ограничения определенных служб
* [Active Directory](#active-directory-limits)
* [Управление API](#api-management-limits)
* [Служба приложений](#app-service-limits)
* [Шлюз приложений](#application-gateway-limits)
* [Application Insights](#application-insights-limits)
* [Автоматизация](#automation-limits)
* [База данных Azure Cosmos](#azure-cosmos-db-limits)
* [Сетка событий Azure](#azure-event-grid-limits)
* [кэш Azure Redis](#azure-redis-cache-limits)
* [Azure RemoteApp](#azure-remoteapp-limits)
* [Архивация](#backup-limits)
* [Пакетная служба](#batch-limits)
* [Службы BizTalk](#biztalk-services-limits)
* [CDN](#cdn-limits)
* [Облачные службы](#cloud-services-limits)
* [Экземпляры контейнеров](#container-instances-limits)
* [Фабрика данных](#data-factory-limits)
* [Аналитика озера данных](#data-lake-analytics-limits)
* [Data Lake Store](#data-lake-store-limits)
* [DNS](#dns-limits)
* [Концентраторы событий](#event-hubs-limits)
* [Центр Интернета вещей](#iot-hub-limits)
* [хранилище ключей;](#key-vault-limits)
* [Log Analytics или Operational Insights](#log-analytics-limits)
* [Службы мультимедиа](#media-services-limits)
* [Службы мобильного взаимодействия;](#mobile-engagement-limits)
* [Мобильные службы](#mobile-services-limits)
* [Мониторинг](#monitor-limits)
* [Многофакторная идентификация](#multi-factor-authentication)
* [Сеть](#networking-limits)
* [Наблюдатель за сетями](#network-watcher-limits)
* [Служба концентратора уведомлений](#notification-hub-service-limits)
* [Группа ресурсов](#resource-group-limits)
* [Планировщик](#scheduler-limits)
* [Поиск](#search-limits)
* [Служебная шина](#service-bus-limits)
* [Site Recovery](#site-recovery-limits)
* [База данных SQL](#sql-database-limits)
* [Хранилище](#storage-limits)
* [StorSimple System](#storsimple-system-limits)
* [Анализ потока](#stream-analytics-limits)
* [Подписка](#subscription-limits)
* [Диспетчер трафика](#traffic-manager-limits)
* [Виртуальные машины](#virtual-machines-limits)
* [Наборы для масштабирования виртуальных машин](#virtual-machine-scale-sets-limits)

### <a name="subscription-limits"></a>Ограничения подписки
#### <a name="subscription-limits"></a>Ограничения подписки
[!INCLUDE [azure-subscription-limits](../includes/azure-subscription-limits.md)]

#### <a name="subscription-limits---azure-resource-manager"></a>Ограничения подписки — Azure Resource Manager
Hello следующие ограничения применяются при использовании hello диспетчера ресурсов Azure и группы ресурсов Azure. Ограничения, которые не были изменены с помощью диспетчера ресурсов Azure hello не перечислены ниже. Для этих ограничений см toohello предыдущей таблице.

Сведения о работе с ограничениями на запросы Resource Manager см. в разделе [Throttling Resource Manager requests](resource-manager-request-limits.md) (Регулирование запросов Resource Manager).

[!INCLUDE [azure-subscription-limits-azure-resource-manager](../includes/azure-subscription-limits-azure-resource-manager.md)]

### <a name="resource-group-limits"></a>Ограничения группы ресурсов
[!INCLUDE [azure-resource-groups-limits](../includes/azure-resource-groups-limits.md)]

### <a name="virtual-machines-limits"></a>Ограничения виртуальных машин
#### <a name="virtual-machine-limits"></a>Ограничения виртуальной машины
[!INCLUDE [azure-virtual-machines-limits](../includes/azure-virtual-machines-limits.md)]

#### <a name="virtual-machines-limits---azure-resource-manager"></a>Ограничения виртуальных машин — диспетчер ресурсов Azure
Hello следующие ограничения применяются при использовании hello диспетчера ресурсов Azure и группы ресурсов Azure. Ограничения, которые не были изменены с помощью диспетчера ресурсов Azure hello не перечислены ниже. Для этих ограничений см toohello предыдущей таблице.

[!INCLUDE [azure-virtual-machines-limits-azure-resource-manager](../includes/azure-virtual-machines-limits-azure-resource-manager.md)]

### <a name="virtual-machine-scale-sets-limits"></a>Ограничения для масштабируемых наборов виртуальных машин
[!INCLUDE [virtual-machine-scale-sets-limits](../includes/azure-virtual-machine-scale-sets-limits.md)]

### <a name="container-instances-limits"></a>Ограничения для экземпляров контейнеров
[!INCLUDE [container-instances-limits](../includes/container-instances-limits.md)]

### <a name="networking-limits"></a>Ограничения сети
[!INCLUDE [expressroute-limits](../includes/expressroute-limits.md)]

#### <a name="networking-limits"></a>Ограничения сети
[!INCLUDE [azure-virtual-network-limits](../includes/azure-virtual-network-limits.md)]

#### <a name="application-gateway-limits"></a>Ограничения шлюза приложений
[!INCLUDE [application-gateway-limits](../includes/application-gateway-limits.md)]

#### <a name="network-watcher-limits"></a>Пределы наблюдателя за сетями
[!INCLUDE [network-watcher-limits](../includes/network-watcher-limits.md)]

#### <a name="traffic-manager-limits"></a>Ограничения диспетчера трафика
[!INCLUDE [traffic-manager-limits](../includes/traffic-manager-limits.md)]

#### <a name="dns-limits"></a>Ограничения DNS
[!INCLUDE [dns-limits](../includes/dns-limits.md)]

### <a name="storage-limits"></a>Ограничения хранилища
Дополнительные сведения об ограничениях учетных записей хранения см. в статье [Целевые показатели по производительности и масштабируемости для хранилища Azure](storage/common/storage-scalability-targets.md).
<!--like # storage accts --> 
#### <a name="storage-service-limits"></a>Ограничения службы хранения
[!INCLUDE [azure-storage-limits](../includes/azure-storage-limits.md)]

<!-- conceptual info about disk limits -- applies toounmanaged and managed -->
#### <a name="virtual-machine-disk-limits"></a>Ограничения для дисков виртуальной машины 
[!INCLUDE [azure-storage-limits-vm-disks](../includes/azure-storage-limits-vm-disks.md)]

Дополнительные сведения см. в статье [Размеры виртуальных машин](virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

#### <a name="managed-virtual-machine-disks"></a>Управляемые диски виртуальной машины

[!INCLUDE [azure-storage-limits-vm-disks-managed](../includes/azure-storage-limits-vm-disks-managed.md)]

#### <a name="unmanaged-virtual-machine-disks"></a>Неуправляемые диски виртуальной машины

[!INCLUDE [azure-storage-limits-vm-disks-standard](../includes/azure-storage-limits-vm-disks-standard.md)]

[!INCLUDE [azure-storage-limits-vm-disks-premium](../includes/azure-storage-limits-vm-disks-premium.md)]

#### <a name="storage-resource-provider-limits"></a>Ограничения поставщика ресурсов хранилища
[!INCLUDE [azure-storage-limits-azure-resource-manager](../includes/azure-storage-limits-azure-resource-manager.md)]

### <a name="cloud-services-limits"></a>Ограничения облачных служб
[!INCLUDE [azure-cloud-services-limits](../includes/azure-cloud-services-limits.md)]

### <a name="app-service-limits"></a>Ограничения службы приложений
Hello вслед за службы приложений ограничивает включают ограничений для веб-приложения, мобильные приложения, приложения API и логику приложения.

[!INCLUDE [azure-websites-limits](../includes/azure-websites-limits.md)]

### <a name="scheduler-limits"></a>Ограничения планировщика
[!INCLUDE [scheduler-limits-table](../includes/scheduler-limits-table.md)]

### <a name="batch-limits"></a>Ограничения пакета
[!INCLUDE [azure-batch-limits](../includes/azure-batch-limits.md)]

### <a name="biztalk-services-limits"></a>Ограничения служб BizTalk
Hello следующей таблице показаны hello ограничения для служб Azure Biztalk.

[!INCLUDE [biztalk-services-service-limits](../includes/biztalk-services-service-limits.md)]

### <a name="azure-cosmos-db-limits"></a>Ограничения Azure Cosmos DB
Azure Cosmos DB — это база данных масштабе, какая пропускная способность и хранением данных может быть масштабированный toohandle независимо от используемой приложением. Если у вас есть вопросы по Azure Cosmos DB обеспечивает масштаб hello, отправьте по электронной почте tooaskcosmosdb@microsoft.com.

### <a name="mobile-engagement-limits"></a>Ограничения Служб мобильного взаимодействия
[!INCLUDE [azure-mobile-engagement-limits](../includes/azure-mobile-engagement-limits.md)]

### <a name="search-limits"></a>Ограничения поиска
Ценовые категории определяют емкости hello и ограничения службы поиска. Существуют следующие категории:

* *Бесплатный* : мультитенантная служба, используемая совместно с другими подписчиками Azure и предназначенная для оценки и разработки небольших проектов.
* *Основные* предоставляет выделенные вычислительные ресурсы для рабочих нагрузок на меньшем масштабе toothree реплик для рабочих нагрузок запросов высокой доступности.
* *Стандартный (S1, S2, S3, S3 с высокой плотностью)* предназначена для больших рабочих нагрузок в рабочей среде. Несколько уровней существовать внутри стандартного уровня hello, чтобы вы могли выбрать конфигурацию ресурсов, который наилучшим образом соответствует профиль рабочей нагрузки.

**Ограничения на одну подписку**

[!INCLUDE [azure-search-limits-per-subscription](../includes/azure-search-limits-per-subscription.md)]

**Ограничения на одну службу поиска**

[!INCLUDE [azure-search-limits-per-service](../includes/azure-search-limits-per-service.md)]

toolearn более об ограничениях на более детальном уровне, такие как размер документа, количество запросов в секунду, ключи, запросов и ответов в разделе [службы ограничения в поиске Azure](search/search-limits-quotas-capacity.md).

### <a name="media-services-limits"></a>Ограничения служб мультимедиа
[!INCLUDE [azure-mediaservices-limits](../includes/azure-mediaservices-limits.md)]

### <a name="cdn-limits"></a>Ограничения CDN
[!INCLUDE [cdn-limits](../includes/cdn-limits.md)]

### <a name="mobile-services-limits"></a>Ограничения мобильных служб
[!INCLUDE [mobile-services-limits](../includes/mobile-services-limits.md)]

### <a name="monitor-limits"></a>Пределы монитора
[!INCLUDE [monitoring-limits](../includes/monitoring-limits.md)]

### <a name="notification-hub-service-limits"></a>Ограничения служб концентратора уведомлений
[!INCLUDE [notification-hub-limits](../includes/notification-hub-limits.md)]

### <a name="event-hubs-limits"></a>Ограничения концентраторов событий
[!INCLUDE [azure-servicebus-limits](../includes/event-hubs-limits.md)]

### <a name="service-bus-limits"></a>Ограничения служебной шины
[!INCLUDE [azure-servicebus-limits](../includes/service-bus-quotas-table.md)]

### <a name="iot-hub-limits"></a>Пределы для Центра Интернета вещей
[!INCLUDE [azure-iothub-limits](../includes/iot-hub-limits.md)]

### <a name="data-factory-limits"></a>Ограничения фабрики данных
[!INCLUDE [azure-data-factory-limits](../includes/azure-data-factory-limits.md)]

### <a name="data-lake-analytics-limits"></a>Ограничения Data Lake Analytics
[!INCLUDE [azure-data-lake-analytics-limits](../includes/azure-data-lake-analytics-limits.md)]

### <a name="data-lake-store-limits"></a>Ограничения Data Lake Store
[!INCLUDE [azure-data-lake-store-limits](../includes/azure-data-lake-store-limits.md)]

### <a name="stream-analytics-limits"></a>Ограничения Stream Analytics
[!INCLUDE [stream-analytics-limits-table](../includes/stream-analytics-limits-table.md)]

### <a name="active-directory-limits"></a>Ограничения Active Directory
[!INCLUDE [AAD-service-limits](../includes/active-directory-service-limits-include.md)]

### <a name="azure-event-grid-limits"></a>Ограничения сетки событий Azure
[!INCLUDE [event-grid-limits](../includes/event-grid-limits.md)]

### <a name="azure-remoteapp-limits"></a>Ограничения Azure RemoteApp
[!INCLUDE [azure-remoteapp-limits](../includes/azure-remoteapp-limits.md)]

### <a name="storsimple-system-limits"></a>Ограничения системы StorSimple
[!INCLUDE [storsimple-limits-table](../includes/storsimple-limits-table.md)]

### <a name="log-analytics-limits"></a>Ограничения Log Analytics
[!INCLUDE [operational-insights-limits](../includes/operational-insights-limits.md)]

### <a name="backup-limits"></a>Ограничения резервного копирования
[!INCLUDE [azure-backup-limits](../includes/azure-backup-limits.md)]

### <a name="site-recovery-limits"></a>Ограничения Site Recovery
[!INCLUDE [site-recovery-limits](../includes/site-recovery-limits.md)]

### <a name="application-insights-limits"></a>Ограничения Application Insights
[!INCLUDE [application-insights-limits](../includes/application-insights-limits.md)]

### <a name="api-management-limits"></a>Ограничения управления API
[!INCLUDE [api-management-service-limits](../includes/api-management-service-limits.md)]

### <a name="azure-redis-cache-limits"></a>Ограничения кэша Redis для Azure
[!INCLUDE [redis-cache-service-limits](../includes/redis-cache-service-limits.md)]

### <a name="key-vault-limits"></a>Ограничения хранилища ключей
[!INCLUDE [key-vault-limits](../includes/key-vault-limits.md)]

### <a name="multi-factor-authentication"></a>Многофакторная идентификация
[!INCLUDE [azure-mfa-service-limits](../includes/azure-mfa-service-limits.md)]

### <a name="automation-limits"></a>Ограничения автоматизации
[!INCLUDE [automation-limits](../includes/azure-automation-service-limits.md)]

### <a name="sql-database-limits"></a>Ограничения базы данных SQL
Ограничения базы данных SQL описаны в разделе [Ограничения ресурсов базы данных SQL](sql-database/sql-database-resource-limits.md).

## <a name="see-also"></a>Дополнительные материалы
[Основные сведения о лимитах Azure и их увеличении](https://azure.microsoft.com/blog/2014/06/04/azure-limits-quotas-increase-requests/)

[Размеры виртуальных машин и облачных служб для Azure](virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

[Размеры для облачных служб](cloud-services/cloud-services-sizes-specs.md)

