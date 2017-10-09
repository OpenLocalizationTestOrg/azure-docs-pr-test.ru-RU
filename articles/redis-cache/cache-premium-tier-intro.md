---
title: "уровень Premium кэша Redis Azure toohello aaaIntroduction | Документы Microsoft"
description: "Узнайте, как toocreate и управление Redis сохраняемости, кластеризация Redis и виртуальной сети поддержки для экземпляров кэша Redis для Azure уровня Premium"
services: redis-cache
documentationcenter: 
author: steved0x
manager: douge
editor: 
ms.assetid: 30f46f9f-e6ec-4c38-a8cc-f9d4444856e5
ms.service: cache
ms.workload: tbd
ms.tgt_pltfrm: cache-redis
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: sdanie
ms.openlocfilehash: 5b58a03647fbf1198509ac6f1acd04f1b682ad95
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-toohello-azure-redis-cache-premium-tier"></a>Уровень Premium кэша Redis Azure toohello введение
Кэш Azure Redis — это распределенное, управляемый кэш, который позволяет создавать быстрые и масштабируемые приложения, обеспечивая супербыстрый доступ к данным tooyour. 

Здравствуйте, новый уровень Premium имеет уровень готовности Enterprise, который включает все функции уровня Standard hello и другие средства, такие как более высокую производительность, более крупных рабочих нагрузок, аварийного восстановления, импорта и экспорта и повышенным уровнем безопасности. Дополнительные сведения о дополнительных функций на уровне кэша Premium hello hello toolearn чтения по-прежнему.

## <a name="better-performance-compared-toostandard-or-basic-tier"></a>Более высокую производительность по сравнению tooStandard или базового уровня
**Повышенная производительность по сравнению с уровнем Стандартный или Базовый.** Кэши в уровня Premium hello развертываются на оборудовании, который имеет более быстрые процессоры и предоставляет более высокую производительность по сравнению toohello Basic или стандартного уровня. Кэши уровня Премиум обладают более высокой пропускной способностью и меньшей задержкой. 

**Пропускная способность для hello того же размера кэша — выше в Premium с уровнем сравниваемых tooStandard.** Например, пропускная способность hello 53 ГБ P4 кэш (расширенная) — 250 КБ запросов в секунду, как сравниваются too150K для C6 (Standard).

Дополнительные сведения о размере, пропускной способности и полосе пропускания для кэшей уровня "Премиум" см. в статье [Кэш Redis для Azure. Вопросы и ответы](cache-faq.md#what-redis-cache-offering-and-size-should-i-use).

## <a name="redis-data-persistence"></a>Сохраняемость данных Redis
Hello уровня Premium позволяет кэшировать данные toopersist hello в учетной записи хранилища Azure. В кэше Basic/Standard все данные hello хранятся только в памяти. При возникновении проблем с базовой инфраструктурой это может привести к потере данных. Рекомендуется использовать функцию сохраняемости данных Redis hello в устойчивости tooincrease уровня Premium hello от потери данных. Кэш Redis для Azure предлагает варианты [сохраняемости данных Redis](http://redis.io/topics/persistence)RDB и AOF (ожидается в ближайшее время). 

Инструкции по настройке сохраняемости см. в разделе [как tooconfigure сохраняемости для кэша Redis Azure Premium](cache-how-to-premium-persistence.md).

## <a name="redis-cluster"></a>Кластер Redis
Если требуется больше, чем 53 ГБ toocreate кэши или хотите tooshard данные по нескольким узлам Redis, можно использовать Redis кластеризации, который доступен на уровне Premium hello. Каждый узел состоит из управляемой Azure пары кэшей (основной кэш и реплика) для обеспечения высокой доступности. 

**Кластеризация Redis обеспечивает максимальные показатели масштабирования и пропускной способности.** Пропускная способность линейно увеличивается по мере увеличения hello число сегментов (узлы) в кластере hello. Например, Если вы создаете кластер P4 10 сегментов, то доступной пропускной способности hello 250 КБ * 10 = 2,5 млн запросов в секунду. См. в разделе hello [Azure Redis кэша часто задаваемые вопросы о](cache-faq.md#what-redis-cache-offering-and-size-should-i-use) Дополнительные сведения о размере, пропускную способность и пропускную способность с кэши premium.

tooget к работе с кластеризацией, в разделе [как tooconfigure кластеризации для кэша Redis Azure Premium](cache-how-to-premium-clustering.md).

## <a name="enhanced-security-and-isolation"></a>Усиленная безопасность и изоляция
Кэшей, созданных в базовом или стандартом уровне hello доступны на hello общедоступный Интернет. Доступ к toohello запрещении кэша на основе ключа доступа hello. С уровня Premium hello дополнительно обеспечивать доступ к hello кэша только для клиентов в указанной сети. Кэш Redis можно развернуть в [виртуальной сети Azure (VNet)](https://azure.microsoft.com/services/virtual-network/). Можно использовать все возможности hello виртуальной сети, такие как подсети, политики управления доступом и другие функции toofurther ограничить доступ tooRedis.

Дополнительные сведения см. в разделе [как поддерживают tooconfigure виртуальной сети для кэша Redis Azure Premium](cache-how-to-premium-vnet.md).

## <a name="importexport"></a>Импорт и экспорт
Импорта и экспорта является операцией управления данных кэша Redis для Azure, позволяющий tooimport данных в кэше Redis для Azure или экспорта данных из кэша Redis для Azure, Импорт и экспорт моментального снимка Redis кэша базы данных (RDB) из premium кэша tooa страничный большой двоичный объект в Azure Учетная запись хранения. Это позволяет toomigrate между различными экземплярами кэша Redis для Azure или заполнения кэша hello с данными, перед использованием.

Импорт может быть используется toobring совместимые файлы RDB Redis с любого сервера Redis под управлением какой-либо облаке или в среде, включая Redis под управлением Linux, Windows или любого поставщика облачных служб, таких как Amazon Web Services и другие. Импорт данных — простой способ toocreate кэша заполнены данными. Во время процесса импорта hello кэша Redis для Azure hello RDB файлы загружаются из хранилища Azure в память и вставляет hello ключи в кэш hello.

Экспорт позволяет tooexport hello данные, хранящиеся в кэш Azure Redis tooRedis совместимый RDB файлов. Можно использовать данные toomove этого компонента из одной tooanother экземпляр кэша Redis для Azure или tooanother сервера Redis. Во время процесса экспорта hello временный файл создается на hello виртуальной Машины, что узлы hello экземпляр сервера кэша Redis для Azure, а hello файл отправленного toohello, назначенные учетной записи хранилища. После завершения операции экспорта hello состояние успеха или сбоя hello временный файл удаляется.

Дополнительные сведения см. в разделе [как tooimport данных и экспортировать данные из кэша Azure Redis](cache-how-to-import-export-data.md).

## <a name="reboot"></a>Reboot
уровень premium Hello позволяет tooreboot один или несколько узлов из вашего кэша по требованию. Это позволяет tootest приложения для обеспечения устойчивости в событии hello сбоя. Можно перезагрузить hello следующие узлы.

* Главный узел кэша.
* Подчиненный узел кэша.
* Главный и подчиненный узлы кэша.
* При использовании размера кэша premium с кластеризации, можно перезагрузить образец hello, ведомый или обоих узлов для отдельных сегментов в кэше hello

Дополнительные сведения см. в разделах [Reboot](cache-administration.md#reboot) (Перезагрузка) и [Часто задаваемые вопросы о перезагрузке](cache-administration.md#reboot-faq).

>[!NOTE]
>Функция перезагрузки теперь включена для всех уровней кэша Redis для Azure.
>
>

## <a name="schedule-updates"></a>запланировать обновления
Hello запланированных обновлений позволяет toodesignate периода обслуживания для вашего кэша. Если задан период обслуживания hello, все обновления сервера Redis выполняются во время этого периода. toodesignate периода обслуживания, выберите требуемого hello дней и укажите hello час запуска окна обслуживания для каждого дня. Обратите внимание, что период обслуживания hello в формате UTC. 

Дополнительные сведения см. в разделах [Планирование обновлений](cache-administration.md#schedule-updates) и [Часто задаваемые вопросы о планировании обновлений](cache-administration.md#schedule-updates-faq).

> [!NOTE]
> Только Redis обновления выполняются во время hello запланированного периода обслуживания сервера. Hello периода обслуживания не применяется tooAzure обновлений или обновления операционной системы виртуальной Машины toohello.
> 
> 

## <a name="geo-replication"></a>Георепликация

**Георепликация** предоставляет механизм связывания двух экземпляров кэша Redis для Azure категории "Премиум". Один кэш используется в качестве основных связанный кэш hello и hello других получателей связанного кэширования hello. Hello дополнительных связанных кэш становится доступным только для чтения и репликации данных, является запись toohello основных кэш toohello дополнительных связанный кэш. Эта возможность может быть используется tooreplicate кэша в разных регионах Azure.

Дополнительные сведения см. в разделе [как tooconfigure географической репликации для кэша Azure Redis](cache-how-to-geo-replication.md).


## <a name="tooscale-toohello-premium-tier"></a>уровень premium toohello tooscale
уровень premium toohello tooscale, просто выберите один из уровней premium hello в hello **изменение ценовой категории** колонку. Также можно масштабировать повышенного уровня toohello кэша с помощью PowerShell и интерфейс командной строки. Пошаговые инструкции см. в разделе [как tooScale Redis для Azure кэшировать](cache-how-to-scale.md) и [как tooautomate операцию масштабирования](cache-how-to-scale.md#how-to-automate-a-scaling-operation).

## <a name="next-steps"></a>Дальнейшие действия
Создание кэша и исследование hello новые возможности уровня premium.

* [Как tooconfigure сохраняемости для кэша Redis Azure Premium](cache-how-to-premium-persistence.md)
* [Как поддерживают tooconfigure виртуальной сети для кэша Redis Azure Premium](cache-how-to-premium-vnet.md)
* [Как tooconfigure кластеризации для кэша Redis Azure Premium](cache-how-to-premium-clustering.md)
* [Как tooimport данных и экспортировать данные из кэша Redis для Azure](cache-how-to-import-export-data.md)
* [Как tooadminister Redis для Azure кэша](cache-administration.md)

