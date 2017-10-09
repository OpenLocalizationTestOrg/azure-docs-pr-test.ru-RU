---
title: "aaaHow tooScale кэша Redis для Azure | Документы Microsoft"
description: "Узнайте, как tooscale Azure Redis кэш экземпляров"
services: redis-cache
documentationcenter: 
author: steved0x
manager: douge
editor: 
ms.assetid: 350db214-3b7c-4877-bd43-fef6df2db96c
ms.service: cache
ms.workload: tbd
ms.tgt_pltfrm: cache-redis
ms.devlang: na
ms.topic: article
ms.date: 04/11/2017
ms.author: sdanie
ms.openlocfilehash: 8d7c015a539f872913056392aa080bf3f445bd03
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooscale-azure-redis-cache"></a>Как tooScale Redis для Azure кэша
Кэш Azure Redis имеет разные предложения кэша, которые обеспечивают гибкость при hello Выбор размера кэша и компоненты. После создания кэша можно масштабировать размер hello и hello в ценовой категории hello кэша при изменении требований hello приложения. В этой статье показано, как tooscale кэша как hello портал Azure, так и с помощью средств, таких как Azure PowerShell и Azure CLI.

## <a name="when-tooscale"></a>Когда tooscale
Можно использовать hello [мониторинг](cache-how-to-monitor.md) функции кэша Azure Redis toomonitor hello работоспособность и производительность кэша и определить, когда tooscale hello кэша. 

Вы можете отслеживать следующие hello toohelp метрик выяснения того, требуются tooscale.

* Загрузка сервера Redis
* Использование памяти
* Пропускная способность сети
* Загрузка ЦП

Если выяснилось, что ваш кэш больше не удовлетворяет требованиям приложения, можно масштабировать tooa увеличить или уменьшить размер кэша, ценовой категории, которая подходит для вашего приложения. Дополнительные сведения об определении кэширования ценовой уровень toouse см. в разделе [какие Redis размер кэша и использовать](cache-faq.md#what-redis-cache-offering-and-size-should-i-use).

## <a name="scale-a-cache"></a>Масштабирование кэша
tooscale кэша, [Обзор кэша toohello](cache-configure.md#configure-redis-cache-settings) в hello [портал Azure](https://portal.azure.com) и нажмите кнопку **шкалы** из hello **ресурсов меню**.

![Масштаб](./media/cache-how-to-scale/redis-cache-scale-menu.png)

Выберите hello требуемого категория hello **выберите ценовую категорию** колонку и нажмите кнопку **выберите**.

![Ценовая категория ][redis-cache-pricing-tier-blade]


Можно масштабировать tooa различных ценовой категории с hello следующие ограничения:

* Нельзя масштабировать из выше ценовой уровень tooa ниже ценовой категории.
  * Нельзя масштабировать из **Premium** кэша вниз tooa **Стандартная** или **основные** кэша.
  * Нельзя масштабировать из **Стандартная** кэша вниз tooa **основные** кэша.
* Можно масштабировать от **основные** кэшировать tooa **Стандартная** кэш, но не может изменить размер hello в hello то же время. Если требуется другой размер, можно сделать последующих размер toohello требуемой операции масштабирования.
* Нельзя масштабировать из **основные** кэшировать непосредственно tooa **Premium** кэша. Требуется расширение из **основные** слишком**Стандартная** за одну операцию масштабирования, а затем с **Стандартная** слишком**Premium** последующих масштабирования операция.
* Нельзя масштабировать от большего вниз toohello **C0 (250 МБ)** размер.
 
Хотя hello кэша выполняется масштабирование toohello новые ценовой категории, **масштабирование** состояние отображается в hello **кэша Redis** колонку.

![Масштабирование][redis-cache-scaling]

По завершении масштабирование hello состояние меняется с **масштабирование** слишком**под управлением**.

## <a name="how-tooautomate-a-scaling-operation"></a>Как tooautomate операцию масштабирования
В дополнение tooscaling экземпляров кэша в Здравствуйте портал Azure, можно масштабировать, используя командлеты PowerShell Azure CLI и с помощью hello библиотеки управления Microsoft Azure (MAML). 

* [Масштабирование с помощью PowerShell](#scale-using-powershell)
* [Масштабирование с помощью интерфейса командной строки Azure](#scale-using-azure-cli)
* [Масштабирование с помощью MAML](#scale-using-maml)

### <a name="scale-using-powershell"></a>Масштабирование с помощью PowerShell
Можно масштабировать экземпляров кэша Redis Azure с помощью PowerShell с помощью hello [набор AzureRmRedisCache](https://msdn.microsoft.com/library/azure/mt634518.aspx) в случае, если hello `Size`, `Sku`, или `ShardCount` свойства изменяются. Hello следующем примере показано, как tooscale кэш именоваться `myCache` tooa 2,5 ГБ кэша. 

    Set-AzureRmRedisCache -ResourceGroupName myGroup -Name myCache -Size 2.5GB

Дополнительные сведения о масштабировании с помощью PowerShell см. в разделе [tooscale Redis кэша с помощью Powershell](cache-howto-manage-redis-cache-powershell.md#scale).

### <a name="scale-using-azure-cli"></a>Масштабирование с помощью интерфейса командной строки Azure
вызывается с помощью Azure CLI экземплярами кэша Azure Redis tooscale hello `azure rediscache set` команды и передать hello необходимости изменения конфигурации, которые включают новый размер, sku или размер кластера, в зависимости от hello требуемого операцию масштабирования.

Дополнительные сведения о масштабировании с помощью интерфейса командной строки Azure см. в разделе [Изменение параметров существующего кэша Redis](cache-manage-cli.md#scale).

### <a name="scale-using-maml"></a>Масштабирование с помощью MAML
tooscale экземпляров кэша Redis Azure с помощью hello [библиотеки управления Microsoft Azure (MAML)](http://azure.microsoft.com/updates/management-libraries-for-net-release-announcement/), вызов hello `IRedisOperations.CreateOrUpdate` метод и передайте его в новый размер hello hello `RedisProperties.SKU.Capacity`.

    static void Main(string[] args)
    {
        // For instructions on getting hello access token, see
        // https://azure.microsoft.com/documentation/articles/cache-configure/#access-keys
        string token = GetAuthorizationHeader();

        TokenCloudCredentials creds = new TokenCloudCredentials(subscriptionId,token);

        RedisManagementClient client = new RedisManagementClient(creds);
        var redisProperties = new RedisProperties();

        // tooscale, set a new size for hello redisSKUCapacity parameter.
        redisProperties.Sku = new Sku(redisSKUName,redisSKUFamily,redisSKUCapacity);
        redisProperties.RedisVersion = redisVersion;
        var redisParams = new RedisCreateOrUpdateParameters(redisProperties, redisCacheRegion);
        client.Redis.CreateOrUpdate(resourceGroupName,cacheName, redisParams);
    }

Дополнительные сведения см. в разделе hello [управления кэша Redis с помощью MAML](https://github.com/rustd/RedisSamples/tree/master/ManageCacheUsingMAML) образца.

## <a name="scaling-faq"></a>Масштабирование: часто задаваемые вопросы
Hello следующий список содержит toocommonly ответы, вопросы и ответы о масштабировании кэша Redis для Azure.

* [Можно ли выполнять масштабирование кэша до уровня Премиум, с уровня Премиум до другого уровня или в пределах уровня Премиум?](#can-i-scale-to-from-or-within-a-premium-cache)
* [После масштабирования, нужно ли toochange ключи кэша имени или доступа?](#after-scaling-do-i-have-to-change-my-cache-name-or-access-keys)
* [Как работает масштабирование?](#how-does-scaling-work)
* [Сохранятся ли данные кэша при масштабировании?](#will-i-lose-data-from-my-cache-during-scaling)
* [Что происходит с пользовательским параметром databases при масштабировании?](#is-my-custom-databases-setting-affected-during-scaling)
* [Будет ли кэш доступен во время масштабирования?](#will-my-cache-be-available-during-scaling)
* [Какие операции не поддерживаются?](#operations-that-are-not-supported)
* [Сколько времени занимает масштабирование?](#how-long-does-scaling-take)
* [Как узнать, когда масштабирование завершено?](#how-can-i-tell-when-scaling-is-complete)

### <a name="can-i-scale-to-from-or-within-a-premium-cache"></a>Можно ли выполнять масштабирование кэша до уровня Премиум, с уровня Премиум до другого уровня или в пределах уровня Премиум?
* Нельзя масштабировать из **Premium** кэша вниз tooa **основные** или **Стандартная** ценовой категории.
* Можно масштабировать от одного **Premium** цены tooanother уровня кэша.
* Нельзя масштабировать из **основные** кэшировать непосредственно tooa **Premium** кэша. Сначала необходимо масштабирование из **основные** слишком**стандартные** за одну операцию масштабирования, а затем от **стандартные** слишком**Premium** в последующем Операция масштабирования.
* Если включена кластеризация при создании вашего **Premium** кэша, вы можете [изменить размер кластера hello](cache-how-to-premium-clustering.md#cluster-size). Если кэш был создан без включенной кластеризации, ее нельзя будет настроить позже.
  
  Дополнительные сведения см. в разделе [как tooconfigure кластеризации для кэша Redis Azure Premium](cache-how-to-premium-clustering.md).

### <a name="after-scaling-do-i-have-toochange-my-cache-name-or-access-keys"></a>После масштабирования, нужно ли toochange ключи кэша имени или доступа?
Нет, имя кэша и ключи не изменяются во время операции масштабирования.

### <a name="how-does-scaling-work"></a>Как работает масштабирование?
* Когда **основные** кэш масштабируется tooa другого размера, она завершает работу, а новый кэш, предоставляется с помощью нового размера hello. В течение этого времени hello кэша недоступна и все данные в кэше hello, будут потеряны.
* При **основные** кэш является масштабированный tooa **Стандартная** кэш, Подготовка кэша-реплики и hello данные копируются из hello основной toohello реплики кэша. во время процесса масштабирование hello Hello кэш остается доступным.
* При **Стандартная** кэш является другой длины масштабированные tooa или tooa **Premium** кэша, одна из реплик hello завершает работу и повторно подготовить toohello новый размер и hello передача данных по и других hello реплика выполнит переход на другой ресурс перед его повторно инициализировать, аналогичный процесс toohello, возникающее при сбое одного из узлов кэша hello.

### <a name="will-i-lose-data-from-my-cache-during-scaling"></a>Сохранятся ли данные кэша при масштабировании?
* Когда **основные** кэша находится новый размер масштабированный tooa, все данные теряются и hello кэша недоступна во время операция масштабирования hello.
* При **основные** кэш является масштабированный tooa **Стандартная** кэша, hello кэша hello обычно сохраняются данные.
* При **Стандартная** кэш является масштабированный tooa большего размера или уровень, или **Premium** кэш масштабируется tooa больший размер, все данные, обычно сохраняются. При масштабировании **Стандартная** или **Premium** кэша вниз tooa меньшего размера, данные могут быть потеряны в зависимости от того, сколько данных находится в кэше hello связанных новый размер toohello при масштабировании. При потере данных при масштабировании с уменьшением, ключи извлекаются с помощью hello [allkeys lru](http://redis.io/topics/lru-cache) политики вытеснения. 

### <a name="is-my-custom-databases-setting-affected-during-scaling"></a>Что происходит с пользовательским параметром databases при масштабировании?
Некоторые ценовые категории имеют различные [баз данных ограничения](cache-configure.md#databases), поэтому существуют определенные рекомендации, если масштабирование Если настроено пользовательское значение hello `databases` можно задать во время создания кэша.

* При масштабировании tooa ценовой категории с более низким `databases` предел от текущего уровня hello:
  * Если вы используете hello количество по умолчанию `databases` которого составляет 16 для всех ценовых категорий, данные не потеряны.
  * Если вы используете настраиваемое число `databases` , находящееся в пределах hello toowhich уровня hello, будет произведено масштабирование, это `databases` настройки сохраняются, и данные не теряются.
  * При использовании настраиваемое число `databases` , размер которого превышает ограничения hello hello новый уровень, hello `databases` параметр задается для ограничений снижения toohello на новый уровень hello и потере всех данных в базах данных удалены hello.
* При масштабировании же или более поздней версии в ценовой категории с hello tooa `databases` предел от текущего уровня hello вашей `databases` настройки сохраняются, и данные не теряются.

Обратите внимание, что, хотя кэш "Стандартный" и "Премиум" имеет соглашение об уровне обслуживания с показателем доступности 99,9 %, для потери данных соглашение об уровне обслуживания отсутствует.

### <a name="will-my-cache-be-available-during-scaling"></a>Будет ли кэш доступен во время масштабирования?
* **Стандартная** и **Premium** кэши остаются доступными во время операция масштабирования hello.
* **Основные** кэши находятся в автономном режиме во время масштабирования операций tooa разного размера, но остаются доступными при масштабировании с **основные** слишком**Standard**.

### <a name="operations-that-are-not-supported"></a>Какие операции не поддерживаются?
* Нельзя масштабировать из выше ценовой уровень tooa ниже ценовой категории.
  * Нельзя масштабировать из **Premium** кэша вниз tooa **Стандартная** или **основные** кэша.
  * Нельзя масштабировать из **Стандартная** кэша вниз tooa **основные** кэша.
* Можно масштабировать от **основные** кэшировать tooa **Стандартная** кэш, но не может изменить размер hello в hello то же время. Если требуется другой размер, можно сделать последующих размер toohello требуемой операции масштабирования.
* Нельзя масштабировать из **основные** кэшировать непосредственно tooa **Premium** кэша. Сначала необходимо масштабирование из **основные** слишком**стандартные** за одну операцию масштабирования, а затем от **стандартные** слишком**Premium** в последующем Операция масштабирования.
* Нельзя масштабировать от большего вниз toohello **C0 (250 МБ)** размер.

Если происходит сбой операции масштабирования, hello служба попытается toorevert hello операции и кэша hello вернется toohello исходный размер.

### <a name="how-long-does-scaling-take"></a>Сколько времени занимает масштабирование?
Масштабирование занимает приблизительно 20 минут, в зависимости от того, сколько данных находится в кэше hello.

### <a name="how-can-i-tell-when-scaling-is-complete"></a>Как узнать, когда масштабирование завершено?
Hello портала Azure вы увидите hello операцию масштабирования в данный момент. По завершении масштабирование hello hello состояния кэша слишком**под управлением**.

<!-- IMAGES -->

[redis-cache-pricing-tier-blade]: ./media/cache-how-to-scale/redis-cache-pricing-tier-blade.png

[redis-cache-scaling]: ./media/cache-how-to-scale/redis-cache-scaling.png



