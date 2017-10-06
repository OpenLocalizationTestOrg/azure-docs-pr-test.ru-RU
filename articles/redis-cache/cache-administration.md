---
title: "aaaHow tooadminister кэша Redis для Azure | Документы Microsoft"
description: "Узнайте, как например перезагрузить tooperform задачи администрирования и Планирование обновлений для кэша Redis для Azure"
services: redis-cache
documentationcenter: na
author: steved0x
manager: douge
editor: tysonn
ms.assetid: 8c915ae6-5322-4046-9938-8f7832403000
ms.service: cache
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: cache-redis
ms.workload: tbd
ms.date: 07/05/2017
ms.author: sdanie
ms.openlocfilehash: eb24668a3f6264444e7d4daf1ac43b41b12dfe66
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooadminister-azure-redis-cache"></a>Как tooadminister Redis для Azure кэша
В этом разделе описывается, как tooperform администрирование таких задач, как [перезагрузку](#reboot) и [Планирование обновлений](#schedule-updates) для экземпляров кэша Redis для Azure.

## <a name="reboot"></a>Reboot
Hello **перезагрузить** колонке позволяет tooreboot один или несколько узлов кэша. Это перезагрузка дает вам tootest приложения для обеспечения устойчивости при наличии сбоя узла кэша.

![Reboot](./media/cache-administration/redis-cache-administration-reboot.png)

Выберите узлы tooreboot hello и нажмите кнопку **перезагрузки**.

![Reboot](./media/cache-administration/redis-cache-reboot.png)

При наличии кэша premium с включенной кластеризацией, можно выбрать какие сегменты кэша tooreboot hello.

![Reboot](./media/cache-administration/redis-cache-reboot-cluster.png)

tooreboot один или несколько узлов кэша, выберите узлы требуемого hello и нажмите кнопку **перезагрузки**. При наличии кэша premium с включенной кластеризацией выберите tooreboot сегментов hello требуемого и нажмите кнопку **перезагрузки**. Через несколько минут hello перезагрузка выбранных узлов и снова подключены к сети через несколько минут.

Hello воздействие на клиентские приложения изменяется в зависимости от того, какие узлы перезагрузить.

* **Образец** — когда главный узел hello превышает узла реплики toohello перезагруженный, Azure Redis Cache завершится ошибкой и повышает ее toomaster. Во время перехода на другой ресурс может быть более короткий интервал, в котором сбои при подключении toohello кэша.
* **Ведомый** — при перезагрузке hello подчиненный узел является обычно нет влияния toocache клиентов.
* **Основной и подчиненный** — при перезагрузке обоих узлов кэша все данные теряются при hello кэша и подключений toohello кэша fail пока hello основной узел становится доступной. Если вы настроили [сохраняемости данных](cache-how-to-premium-persistence.md), самой последней резервной копии hello восстанавливается hello кэша становится доступной, когда запись кэша, произошедших после последней резервной копии hello теряются.
* **Узлы расширенной кэш с включенной кластеризацией** — когда перезагрузить один или несколько узлов кэша premium с кластеризацией включен, hello поведение для hello выбранных узлов hello же, как при перезагрузке hello соответствующий узел или узлы некластеризованный кэш.

> [!IMPORTANT]
> Перезагрузка теперь доступна для всех ценовых категорий.
> 
> 

## <a name="reboot-faq"></a>Часто задаваемые вопросы о перезагрузке
* [Какой из узлов следует перезагрузке tootest Мое приложение?](#which-node-should-i-reboot-to-test-my-application)
* [Можно перезагрузить hello кэша tooclear клиентских подключений](#can-i-reboot-the-cache-to-clear-client-connections)
* [Сохранятся ли данные кэша после перезагрузки?](#will-i-lose-data-from-my-cache-if-i-do-a-reboot)
* [Можно ли перезагрузить кэш с помощью PowerShell, интерфейса командной строки или других средств управления?](#can-i-reboot-my-cache-using-powershell-cli-or-other-management-tools)
* [Какие цены уровней, можно использовать функции hello перезагрузка?](#what-pricing-tiers-can-use-the-reboot-functionality)

### <a name="which-node-should-i-reboot-tootest-my-application"></a>Какой из узлов следует перезагрузке tootest Мое приложение?
tootest hello устойчивости в случае сбоя приложения hello первичного узла кэша, перезагрузка hello **Master** узла. Устойчивость hello tootest приложения в случае сбоя вторичного узла hello, перезагрузка hello **ведомый** узла. Устойчивость hello tootest приложения от сбоя всего кэша hello, перезагрузите **оба** узлов.

### <a name="can-i-reboot-hello-cache-tooclear-client-connections"></a>Можно перезагрузить hello кэша tooclear клиентских подключений
Да, при перезагрузке hello кэша будут очищены все клиентские соединения. Перезагрузка может быть полезно в случае hello, где все клиентские соединения не будут использованы из-за tooa логическая ошибка или ошибка в клиентское приложение hello. Каждая Ценовая категория имеет другие [ограничения на подключения клиентов](cache-configure.md#default-redis-server-configuration) для hello разного размера, а после достижения этих ограничений принимаются дополнительных клиентских подключений. Перезагрузка кэша hello предоставляет tooclear способом все клиентские соединения.

> [!IMPORTANT]
> При перезагрузке подключений tooclear клиента кэша StackExchange.Redis автоматически повторно подключается после узла Redis hello вернется в оперативный режим. Если hello базовой проблема не будет устранена, hello клиентских соединений может продолжаться toobe занята.
> 
> 

### <a name="will-i-lose-data-from-my-cache-if-i-do-a-reboot"></a>Сохранятся ли данные кэша после перезагрузки?
При перезагрузке обоих hello **Master** и **ведомый** узлы, теряются все данные в кэше hello (или своего сегмента при использовании размера кэша premium с включенной кластеризацией). Если вы настроили [сохраняемости данных](cache-how-to-premium-persistence.md), hello самой последней резервной копии будет восстановлена hello кэша становится доступной, когда запись кэша с момента создания hello резервной копии будут потеряны.

Если перезагрузить только одного из узлов hello, данные не обычно теряются, но по-прежнему может быть. Например, при перезагрузке hello главного узла и запись кэша выполняется hello данные из записи кэша hello будет потеряно. Другим случаем потеря данных будет перезагрузить один узел и hello другой узел происходит toogo работу из-за сбоя tooa hello то же время. Дополнительные сведения о возможных причинах потери данных см. в разделе [ошибка toomy данные в Redis?](https://gist.github.com/JonCole/b6354d92a2d51c141490f10142884ea4#file-whathappenedtomydatainredis-md)

### <a name="can-i-reboot-my-cache-using-powershell-cli-or-other-management-tools"></a>Можно ли перезагрузить кэш с помощью PowerShell, интерфейса командной строки или других средств управления?
Да, PowerShell инструкции в разделе [tooreboot кэш Redis](cache-howto-manage-redis-cache-powershell.md#to-reboot-a-redis-cache).

### <a name="what-pricing-tiers-can-use-hello-reboot-functionality"></a>Какие цены уровней, можно использовать функции hello перезагрузка?
Перезагрузка доступна для всех ценовых категорий.

## <a name="schedule-updates"></a>запланировать обновления
Hello **расписание обновления** колонке позволяет toodesignate периода обслуживания для вашего кэша уровня Premium. Если задан период обслуживания hello, все обновления сервера Redis выполняются во время этого периода. 

> [!NOTE] 
> Hello окна обслуживания применяется только tooRedis обновления сервера и не tooany Azure обновлений или обновления операционной системы toohello hello виртуальных машин, которые размещения кэша hello.
> 
> 

![запланировать обновления](./media/cache-administration/redis-schedule-updates.png)

toospecify периода обслуживания, проверьте дни hello требуемого укажите hello час запуска окна обслуживания для каждого дня и нажмите кнопку **ОК**. Обратите внимание, что период обслуживания hello в формате UTC. 

> [!NOTE]
> период обслуживания по умолчанию Hello для обновления составляет пять часов. Это значение не hello портал Azure можно настроить, но его можно настроить в PowerShell с использованием hello `MaintenanceWindow` параметр hello [New AzureRmRedisCacheScheduleEntry](/powershell/module/azurerm.rediscache/new-azurermrediscachescheduleentry) командлета. Дополнительные сведения см. в разделе [Можно ли управлять запланированными обновлениями с помощью PowerShell, интерфейса командной строки или других инструментов управления?](#can-i-manage-scheduled-updates-using-powershell-cli-or-other-management-tools)
> 
> 

## <a name="schedule-updates-faq"></a>Часто задаваемые вопросы о планировании обновлений
* [Когда обновления выполняться режим hello расписание обновлений компонентов?](#when-do-updates-occur-if-i-dont-use-the-schedule-updates-feature)
* [Тип обновления выполняются во время hello запланированного периода обслуживания?](#what-type-of-updates-are-made-during-the-scheduled-maintenance-window)
* [Можно ли управлять запланированными обновлениями с помощью PowerShell, интерфейса командной строки или других средств управления?](#can-i-managed-scheduled-updates-using-powershell-cli-or-other-management-tools)
* [Какие цены уровнями можно с помощью функции обновления hello расписание?](#what-pricing-tiers-can-use-the-schedule-updates-functionality)

### <a name="when-do-updates-occur-if-i-dont-use-hello-schedule-updates-feature"></a>Когда обновления выполняться режим hello расписание обновлений компонентов?
Если период обслуживания не указан, то обновления могут выполняться в любое время.

### <a name="what-type-of-updates-are-made-during-hello-scheduled-maintenance-window"></a>Тип обновления выполняются во время hello запланированного периода обслуживания?
Только Redis обновления выполняются во время hello запланированного периода обслуживания сервера. Hello периода обслуживания не применяется tooAzure обновлений или обновления операционной системы виртуальной Машины toohello.

### <a name="can-i-managed-scheduled-updates-using-powershell-cli-or-other-management-tools"></a>Можно ли управлять запланированными обновлениями с помощью PowerShell, интерфейса командной строки или других средств управления?
Да, вы можете управлять запланированного обновления с помощью hello следующие командлеты PowerShell:

* [Get-AzureRmRedisCachePatchSchedule](/powershell/module/azurerm.rediscache/get-azurermrediscachepatchschedule)
* [New-AzureRmRedisCachePatchSchedule](/powershell/module/azurerm.rediscache/new-azurermrediscachepatchschedule)
* [New-AzureRmRedisCacheScheduleEntry](/powershell/module/azurerm.rediscache/new-azurermrediscachescheduleentry)
* [Remove-AzureRmRedisCachePatchSchedule](/powershell/module/azurerm.rediscache/remove-azurermrediscachepatchschedule)

### <a name="what-pricing-tiers-can-use-hello-schedule-updates-functionality"></a>Какие цены уровнями можно с помощью функции обновления hello расписание?
Hello **расписание обновления** функция доступна только в ценовой категории premium hello.

## <a name="next-steps"></a>Дальнейшие действия
* Узнайте больше о [кэше Redis для Azure уровня "Премиум"](cache-premium-tier-intro.md).

