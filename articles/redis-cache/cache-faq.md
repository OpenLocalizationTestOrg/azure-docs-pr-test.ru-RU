---
title: "вопросы и ответы кэша Redis aaaAzure | Документы Microsoft"
description: "Узнайте, что hello ответы на вопросы toocommon, шаблоны и практические рекомендации для кэша Redis для Azure"
services: redis-cache
documentationcenter: 
author: steved0x
manager: douge
editor: 
ms.assetid: c2c52b7d-b2d1-433a-b635-c20180e5cab2
ms.service: cache
ms.workload: tbd
ms.tgt_pltfrm: cache-redis
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: sdanie
ms.openlocfilehash: 2c6ed2f65f755bd08f04857b7af31f520cf4f158
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-redis-cache-faq"></a>Кэш Redis для Azure. Вопросы и ответы
Дополнительные сведения hello ответы на вопросы toocommon, шаблоны и рекомендации для кэша Redis для Azure.

## <a name="what-if-my-question-isnt-answered-here"></a>Мне не удалось найти ответ на свой вопрос. Что делать?
Если вашего вопроса нет в списке, сообщите нам об этом, и мы поможем найти ответ.

* Можно разместить вопрос на комментарии hello в конце hello вопросы и ответы и связаться с team hello кэша Azure и другими участниками сообщества о в этой статье.
* tooreach различных пользователей, можно разместить вопрос на hello [форум MSDN кэша Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=azurecache) и связаться с team hello кэша Azure и другими членами сообщества hello.
* Если вы хотите toomake запрос функции, вы можете отправить запросы и идеи слишком[Azure Redis кэша User Voice](https://feedback.azure.com/forums/169382-cache).
* Можно также отправить сообщение электронной почты в toous [отзывы внешний кэш Azure](mailto:azurecache@microsoft.com).

## <a name="azure-redis-cache-basics"></a>Основные сведения о кэше Redis для Azure
Hello вопросы и ответы в этом разделе рассказывается о hello основы кэша Redis для Azure.

* [Описание кэша Redis для Azure](#what-is-azure-redis-cache)
* [Как приступить к работе с кэшем Redis для Azure?](#how-can-i-get-started-with-azure-redis-cache)

Hello следующие часто задаваемые вопросы о рассматриваются основные понятия и вопросы о кэше Redis для Azure и обработаны в одном из hello другие разделы часто задаваемые вопросы.

* [Какое предложение и размер кэша Redis мне следует использовать?](#what-redis-cache-offering-and-size-should-i-use)
* [Какие клиенты кэша Redis можно использовать?](#what-redis-cache-clients-can-i-use)
* [Существует локальный эмулятор кэша Redis для Azure?](#is-there-a-local-emulator-for-azure-redis-cache)
* [Как отслеживать hello работоспособность и производительность моих кэша?](#how-do-i-monitor-the-health-and-performance-of-my-cache)

## <a name="planning-faqs"></a>Часто задаваемые вопросы о планировании
* [Какое предложение и размер кэша Redis мне следует использовать?](#what-redis-cache-offering-and-size-should-i-use)
* [Производительность кэша Redis для Azure](#azure-redis-cache-performance)
* [В каком регионе следует размещать мой кэш?](#in-what-region-should-i-locate-my-cache)
* [Как выставляются счета за использование кэша Redis для Azure?](#how-am-i-billed-for-azure-redis-cache)
* [Могу ли я использовать кэш Redis для Azure с облаком Azure для государственных организаций, Azure China или Microsoft Azure для Германии?](#can-i-use-azure-redis-cache-with-azure-government-cloud-azure-china-cloud-or-microsoft-azure-germany)

## <a name="development-faqs"></a>Часто задаваемые вопросы о разработке
* [Что делать параметры конфигурации StackExchange.Redis hello](#what-do-the-stackexchangeredis-configuration-options-do)
* [Какие клиенты кэша Redis можно использовать?](#what-redis-cache-clients-can-i-use)
* [Существует локальный эмулятор кэша Redis для Azure?](#is-there-a-local-emulator-for-azure-redis-cache)
* [Как выполнять команды Redis?](#how-can-i-run-redis-commands)
* [Почему отсутствует кэша Redis для Azure MSDN Справочник по библиотеке классов как часть hello другими службами Azure?](#why-doesnt-azure-redis-cache-have-an-msdn-class-library-reference-like-some-of-the-other-azure-services)
* [Можно ли использовать кэш Redis для Azure как кэш сеанса PHP?](#can-i-use-azure-redis-cache-as-a-php-session-cache)
* [Что такое базы данных Redis?](#what-are-redis-databases)

## <a name="security-faqs"></a>Часто задаваемые вопросы о безопасности
* [Если включить hello не SSL-порт для подключения tooRedis](#when-should-i-enable-the-non-ssl-port-for-connecting-to-redis)

## <a name="production-faqs"></a>Часто задаваемые вопросы о рабочей среде
* [Какие рекомендации следует учитывать для рабочей среды?](#what-are-some-production-best-practices)
* [Каковы некоторые особенности hello, при использовании общих команд Redis?](#what-are-some-of-the-considerations-when-using-common-redis-commands)
* [Как сравнить и протестировать hello производительность моих кэша?](#how-can-i-benchmark-and-test-the-performance-of-my-cache)
* [Важные сведения о росте пула потоков ThreadPool](#important-details-about-threadpool-growth)
* [Включить tooget сборщик Мусора сервера при использовании StackExchange.Redis большую нагрузку на приветствия клиента](#enable-server-gc-to-get-more-throughput-on-the-client-when-using-stackexchangeredis)
* [Рекомендации по производительности для подключений](#performance-considerations-around-connections)

## <a name="monitoring-and-troubleshooting-faqs"></a>Часто задаваемые вопросы о мониторинге и устранении неполадок
часто задаваемые вопросы о Hello в этот раздел титульных общих мониторинга и вопросы по устранению неполадок. Дополнительные сведения о мониторинге и устранение неполадок своих экземпляров кэша Redis для Azure см. в разделе [как toomonitor Redis для Azure кэшировать](cache-how-to-monitor.md) и [как tootroubleshoot Redis для Azure кэшировать](cache-how-to-troubleshoot.md).

* [Как отслеживать hello работоспособность и производительность моих кэша?](#how-do-i-monitor-the-health-and-performance-of-my-cache)
* [Почему я наблюдаю простои?](#why-am-i-seeing-timeouts)
* [Почему мой клиент был отключен от hello кэша?](#why-was-my-client-disconnected-from-the-cache)

## <a name="prior-cache-offering-faqs"></a>Часто задаваемые вопросы о предыдущих предложениях кэша
* [Какой кэш Azure подходит мне?](#which-azure-cache-offering-is-right-for-me)

### <a name="what-is-azure-redis-cache"></a>Описание кэша Redis для Azure
Кэш Azure Redis основан на hello популярных открытая [кэша Redis](http://redis.io). Он предоставляет доступ к tooa безопасного выделенному кэшу Redis, управляемых корпорацией Майкрософт и доступен из любого приложения в Azure. Более подробные сведения см. в разделе hello [кэш Azure Redis](https://azure.microsoft.com/services/cache/) страница продукта на Azure.com.

### <a name="how-can-i-get-started-with-azure-redis-cache"></a>Как приступить к работе с кэшем Redis для Azure?
Существует несколько способов приступить к работе с кэшем Redis для Azure.

* Вы можете ознакомиться с одним из наших руководств, доступных для [.NET](cache-dotnet-how-to-use-azure-redis-cache.md), [ASP.NET](cache-web-app-howto.md), [Java](cache-java-get-started.md), [Node.js](cache-nodejs-get-started.md) и [Python](cache-python-get-started.md).
* Вы можете ознакомиться с [как tooBuild высокопроизводительных приложений с помощью Microsoft Azure кэша Redis](https://azure.microsoft.com/documentation/videos/how-to-build-high-performance-apps-using-microsoft-azure-cache/).
* Можно извлечь hello документации клиента для клиентов hello, соответствующих языке разработки hello toosee ваш проект, как toouse Redis. Существует множество клиентов Redis, которые можно использовать с кэшем Redis для Azure. Список клиентов Redis доступен на странице [http://redis.io/clients](http://redis.io/clients).

Если у вас нет учетной записи Azure, то вы можете сделать следующее.

* [Открыть бесплатную учетную запись Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=redis_cache_hero). Вы получаете кредиты, которые могут быть используется tootry out платных служб Azure. Даже после израсходования кредитов hello, можно защитить учетную запись hello и использования бесплатной службы Azure и возможностей.
* [Активировать преимущества подписчика Visual Studio](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=redis_cache_hero). Ваша подписка MSDN каждый месяц приносит вам кредиты, которые можно использовать для оплаты использования служб Azure.

<a name="cache-size"></a>

### <a name="what-redis-cache-offering-and-size-should-i-use"></a>Какое предложение и размер кэша Redis мне следует использовать?
Все предложения кэша Redis для Azure обеспечивают разные уровни параметров **размера**, **пропускной способности**, **высокой доступности** и **соглашения об уровне обслуживания**.

Hello ниже приведены рекомендации по выбору размера кэша.

* **Память**: hello простом и стандартном уровни предлагают 250 МБ — 53 ГБ. Hello уровня Premium обеспечивает too530 ГБ. Подробные сведения см. на странице [Цены на кэш Redis для Azure](https://azure.microsoft.com/pricing/details/cache/).
* **Производительность сети**: Если имеется рабочая нагрузка, которая требует высокой пропускной способностью, hello уровня Premium предлагает дополнительные tooStandard пропускной способности по сравнению или Basic. Также в рамках каждого уровня кэши большего размера имеют большую полосу пропускания из-за hello основной виртуальной Машины, на котором размещена hello кэша. В разделе hello [следующие таблицы](#cache-performance) для получения дополнительной информации.
* **Пропускная способность**: hello уровня Premium предлагает hello максимальной доступной пропускной способности. Если hello кэша сервера или клиента достигает ограничения пропускной способности hello, может появиться времени ожидания на стороне клиента hello. Дополнительные сведения см. в следующей таблице hello.
* **Высокий уровень доступности и соглашения об уровне ОБСЛУЖИВАНИЯ**: кэша Redis для Azure гарантирует, что кэша Standard и Premium доступен по крайней мере 99,9% времени hello. toolearn Дополнительные сведения о СОГЛАШЕНИИ, в разделе [Azure Redis стоимость кэша](https://azure.microsoft.com/support/legal/sla/cache/v1_0/). соглашения об уровне ОБСЛУЖИВАНИЯ Hello охватывает только конечные точки кэша toohello подключения. Hello соглашения об уровне ОБСЛУЖИВАНИЯ не охватывает защиты от потери данных. Рекомендуется использовать функцию сохраняемости данных Redis hello в устойчивости tooincrease уровня Premium hello от потери данных.
* **Сохраняемость данных redis**: hello уровня Premium позволяет кэшировать данные toopersist hello в учетной записи хранилища Azure. В кэше Basic/Standard все данные hello хранятся только в памяти. При возникновении проблем с базовой инфраструктурой это может привести к потере данных. Рекомендуется использовать функцию сохраняемости данных Redis hello в устойчивости tooincrease уровня Premium hello от потери данных. Кэш Redis для Azure предлагает варианты постоянного хранения данных RDB и AOF (ожидается в ближайшее время). Дополнительные сведения см. в разделе [как tooconfigure сохраняемости для кэша Redis Azure Premium](cache-how-to-premium-persistence.md).
* **Redis кластера**: toocreate кэширует больше, чем 53 ГБ или tooshard данных на нескольких узлах Redis, можно использовать Redis кластеризации, который доступен на уровне Premium hello. Каждый узел состоит из пары кэшей (основной кэш и реплика) для обеспечения высокой доступности. Дополнительные сведения см. в разделе [как tooconfigure кластеризации для кэша Redis Azure Premium](cache-how-to-premium-clustering.md).
* **Усиленной безопасности и сетевой изоляции**: развертывание Azure виртуальная сеть (VNET) обеспечивает улучшенную защиту и изоляции для кэша Redis для Azure, а также подсетей, политики управления доступом, и другие функции toofurther ограничения доступа. Дополнительные сведения см. в разделе [как поддерживают tooconfigure виртуальной сети для кэша Redis Azure Premium](cache-how-to-premium-vnet.md).
* **Настройка Redis**: hello Standard и Premium уровней можно настроить уведомления Keyspace Redis.
* **Максимальное число клиентских подключений**: hello уровня Premium предлагает hello максимальное число клиентов, которые могут подключаться tooRedis, с более высоким номером подключений для большего размера кэша. Дополнительные сведения см. на странице [цены на кэш Redis для Azure](https://azure.microsoft.com/pricing/details/cache/).
* **Выделенные основных компонентов сервера Redis**: hello уровня Premium, все размеры кэша имеют выделенное ядро для Redis. На уровнях Basic/Standard hello hello C1 размер и выше имеют выделенное ядро сервера Redis.
* **Redis является однопоточным** , поэтому наличие более двух ядер не предоставляет дополнительных преимуществ по сравнению с двумя ядрами, но виртуальные машины большего размера обычно имеют большую пропускную способность, чем виртуальные машины меньшего размера. Если hello кэша сервера или клиента достигает ограничения пропускной способности hello, вы получите значения времени ожидания на стороне клиента hello.
* **Повышение производительности**: кэши в уровня Premium hello развертываются на оборудовании с более быстрые процессоры, что дает более высокую производительность по сравнению toohello базового или стандартного уровня. Кэши уровня Премиум обладают более высокой пропускной способностью и меньшей задержкой.

<a name="cache-performance"></a>

### <a name="azure-redis-cache-performance"></a>Производительность кэша Redis для Azure
Hello следующей таблице показаны значений hello максимальную пропускную способность при тестировании различных размеров Standard и Premium кэширует с помощью `redis-benchmark.exe` из ВМ Iaas для конечной точки кэша Redis для Azure hello. 

>[!NOTE] 
>Эти значения не гарантируются и для них не предусмотрено соглашение об уровне обслуживания, однако они должны быть типичными. Следует загружать тестирования собственного приложения toodetermine hello нужного размера кэша для вашего приложения.
>
>

Из этой таблицы можно сделать следующие выводы hello:

* Пропускная способность для кэшей hello, приветствия одинакового размера более высокого уровня в hello уровня Premium как сравниваемых toohello стандартного уровня. Например с кэшем 6 ГБ, пропускной способности P1 — 180 000 RPS как сравниваемых too49, 000 для C3.
* В Redis кластеризации пропускную способность линейно возрастает по мере увеличения hello число сегментов (узлы) в кластере hello. Например, при создании кластера P4 10 сегментов, затем hello доступных пропускная способность — 400 000 * 10 = 4 миллионов RPS.
* Пропускная способность для увеличить размеры ключа — выше уровня Premium hello как сравниваемых toohello стандартного уровня.

| Ценовая категория  | Размер | Ядра ЦП | Доступная пропускная способность | Единица измерения — 1 КБ |
| --- | --- | --- | --- | --- |
| **Размеры кэша уровня Стандартный** | | |**Мегабит в секунду (Мбит/с) или Мегабайт в секунду (МБ/с)** |**Запросов в секунду** |
| C0 |250 МБ |Совмещаемая блокировка |5 / 0,625 |600 |
| C1 |1 GB |1 |100 / 12,5 |12,200 |
| C2 |2,5 ГБ |2 |200 / 25 |24,000 |
| C3 |6 ГБ |4. |400 / 50 |49,000 |
| C4 |13 ГБ |2 |500 / 62,5 |61,000 |
| C5 |26 ГБ |4 |1,000 / 125 |115,000 |
| C6 |53 ГБ |8 |2,000 / 250 |150 000 |
| **Размеры кэша уровня Премиум** | |**Число ядер ЦП на сегмент** | **Мегабит в секунду (Мбит/с) или Мегабайт в секунду (МБ/с)** |**Запросов в секунду для каждого сегмента** |
| P1 |6 ГБ |2 |1,500 / 187.5 |180,000 |
| P2 |13 ГБ |4 |3,000 / 375 |360,000 |
| P3 |26 ГБ |4. |3,000 / 375 |360,000 |
| P4 |53 ГБ |8 |6,000 / 750 |400 000 |

Для инструкции по загрузке hello Redis средств, таких как `redis-benchmark.exe`, в разделе hello [как можно выполнить команды Redis?](#cache-commands) раздела.

<a name="cache-region"></a>

### <a name="in-what-region-should-i-locate-my-cache"></a>В каком регионе следует размещать мой кэш?
Для максимальной производительности и минимальной задержке, найдите кэша Azure Redis Cache в hello же регионе, что клиентское приложение для кэша.

<a name="cache-billing"></a>

### <a name="how-am-i-billed-for-azure-redis-cache"></a>Как выставляются счета за использование кэша Redis для Azure?
Цены на кэш Redis для Azure можно просмотреть [здесь](https://azure.microsoft.com/pricing/details/cache/). страница с ценами Hello приведены цены на почасовой. Кэши выставляются на основе поминутной с момента hello hello кэш создается до времени hello, кэш удаляется. Нет возможности для остановки или приостановки выставления счетов hello кэша.

### <a name="can-i-use-azure-redis-cache-with-azure-government-cloud-azure-china-cloud-or-microsoft-azure-germany"></a>Могу ли я использовать кэш Redis для Azure с облаком Azure для государственных организаций, Azure China или Microsoft Azure для Германии?
Да, кэш Redis для Azure доступен в облаках Azure для государственных организаций, Azure China и Microsoft Azure для Германии. в этих облаках, по сравнению с общедоступное облако Azure отличаются Hello URL-адреса для доступа и управления кэша Redis для Azure. 

| Облако   | DNS-суффикс для кэша Redis            |
|---------|---------------------------------|
| Общедоступные  | *.redis.cache.windows.net       |
| Штат в США (для обслуживания государственных организаций США)  | *.redis.cache.usgovcloudapi.net |
| Германия | *.redis.cache.cloudapi.de       |
| Китай   | *.redis.cache.chinacloudapi.cn  |

Дополнительные сведения о вопросах, при использовании других облаков кэша Redis для Azure см. hello ссылкам.

- [Azure Government Databases — Azure Redis Cache](../azure-government/documentation-government-services-database.md#azure-redis-cache) (Базы данных Azure для государственных организаций — кэш Redis для Azure)
- [Azure China Cloud — Azure Redis Cache](https://www.azure.cn/documentation/services/redis-cache/) (Облако Azure China — кэш Redis для Azure)
- [Microsoft Azure для Германии](https://azure.microsoft.com/overview/clouds/germany/)

Сведения об использовании кэша Redis для Azure с помощью PowerShell в облако Azure государственных организаций, Китай облако Azure и Германии Microsoft Azure см. в разделе [как tooconnect tooother облаков — PowerShell кэша Redis Azure](cache-howto-manage-redis-cache-powershell.md#how-to-connect-to-other-clouds).

<a name="cache-configuration"></a>

### <a name="what-do-hello-stackexchangeredis-configuration-options-do"></a>Что делать параметры конфигурации StackExchange.Redis hello
StackExchange.Redis имеет много параметров. Этот раздел рассказывает о hello общих настроек. Более подробные сведения о параметрах StackExchange.Redis см. в статье [StackExchange.Redis configuration](https://stackexchange.github.io/StackExchange.Redis/Configuration) (Конфигурация StackExchange.Redis).

| Параметры конфигурации | Описание | Рекомендации |
| --- | --- | --- |
| AbortOnConnectFail |Если значение tootrue, hello подключение не будет восстановиться после сбоя в сети. |Задайте toofalse и позволить StackExchange.Redis повторное соединение производится автоматически. |
| ConnectRetry |Hello число попыток подключения toorepeat во время начального подключения. |См. следующие примечания рекомендации hello. |
| ConnectTimeout |Время ожидания в миллисекундах для операций подключения. |См. следующие примечания рекомендации hello. |

Обычно достаточны значения по умолчанию hello hello клиента. Можно выполнить тонкую настройку hello вариантов в зависимости от рабочей нагрузки.

* **Повторы**
  * ConnectRetry и ConnectTimeout hello Общие рекомендации — toofail быстрого и повторите попытку. В этом руководстве зависит от рабочей нагрузки и сколько времени на среднее значение принимает для вашего клиента tooissue команды Redis и получить ответ.
  * Вам не нужно проверять состояние и подключаться самостоятельно — StackExchange.Redis переподключается автоматически. **Старайтесь не использовать свойство ConnectionMultiplexer.IsConnected hello**.
  * Snowballing - иногда может возникать проблема, где повтором и повторяет snowball hello и никогда не восстанавливает. В случае snowballing следует использовать алгоритм повтора экспоненциально растущим, как описано в [повторите Общие рекомендации](../best-practices-retry-general.md) опубликованных группой шаблонов и практик Майкрософт hello.
* **Значения времени ожидания**
  * Рассмотрим рабочей нагрузки и задание значений hello соответствующим образом. При сохранении больших значений, значение hello время ожидания tooa выше.
  * Задать `AbortOnConnectFail` toofalse и позволить StackExchange.Redis повторного подключения для вас.
  * Используйте один экземпляр ConnectionMultiplexer для приложения hello. Можно использовать LazyConnection toocreate отдельного экземпляра, который возвращается свойством соединения, как показано в [подключиться с использованием класса ConnectionMultiplexer hello кэша toohello](cache-dotnet-how-to-use-azure-redis-cache.md#connect-to-the-cache).
  * Набор hello `ConnectionMultiplexer.ClientName` свойство tooan приложения уникальное имя экземпляра в целях диагностики.
  * Используйте несколько экземпляров `ConnectionMultiplexer` для пользовательских рабочих нагрузок.
      * Вы можете следовать этой модели, если в приложении имеется меняющаяся нагрузка. Например:
      * можно иметь один мультиплексор для работы с большими ключами;
      * можно иметь один мультиплексор для работы с небольшими ключами;
      * можно задать разные значения времени ожидания подключения и логики повторов для каждого используемого ConnectionMultiplexer.
      * Набор hello `ClientName` свойства на каждой мультиплексор toohelp с диагностикой.
      * Это руководство может привести toomore упрощенную задержка на `ConnectionMultiplexer`.

### <a name="what-redis-cache-clients-can-i-use"></a>Какие клиенты кэша Redis можно использовать?
Одно из интересных черт Redis hello является многие клиенты с поддержкой многих языков разработки. Текущий список клиентов Redis см. [здесь](http://redis.io/clients). Руководства, охватывающие несколько разных языков и клиентов см. [как toouse Redis для Azure кэшировать](cache-dotnet-how-to-use-azure-redis-cache.md) и нажмите кнопку hello требуемого языка из переключателя языка hello вверху hello hello статьи.

[!INCLUDE [redis-cache-create](../../includes/redis-cache-access-keys.md)]

<a name="cache-emulator"></a>

### <a name="is-there-a-local-emulator-for-azure-redis-cache"></a>Существует локальный эмулятор кэша Redis для Azure?
Нет не локальный эмулятор для кэша Redis для Azure, но можно запустить из hello hello версии MSOpenTech redis server.exe [Redis средства командной строки](https://github.com/MSOpenTech/redis/releases/) на локальном компьютер и подключите tooit tooget аналогичные возможности tooa локального кэша эмулятор, как показано в следующий пример hello:

    private static Lazy<ConnectionMultiplexer>
          lazyConnection = new Lazy<ConnectionMultiplexer>
        (() =>
        {
            // Connect tooa locally running instance of Redis toosimulate a local cache emulator experience.
            return ConnectionMultiplexer.Connect("127.0.0.1:6379");
        });

        public static ConnectionMultiplexer Connection
        {
            get
            {
                return lazyConnection.Value;
            }
        }


При необходимости можно настроить [redis.conf](http://redis.io/topics/config) toomore файла точно соответствуют hello [параметры кэша по умолчанию](cache-configure.md#default-redis-server-configuration) для вашей сети кэша Azure Redis при необходимости.

<a name="cache-commands"></a>

### <a name="how-can-i-run-redis-commands"></a>Как выполнять команды Redis?
Можно использовать любой из команд hello, перечисленных в [команды Redis](http://redis.io/commands#) за исключением hello команд, перечисленных в [команды не поддерживается в кэше Redis для Azure Redis](cache-configure.md#redis-commands-not-supported-in-azure-redis-cache). У вас есть несколько вариантов toorun Redis команд.

* Если у вас есть кэша Standard или Premium, можно запускать команды Redis с помощью hello [Redis консоли](cache-configure.md#redis-console). консоль Redis Hello предоставляет toorun безопасным способом команды Redis в hello портал Azure.
* Также можно использовать программы командной строки Redis hello. toouse их, выполните следующие действия hello:
* Загрузите hello [Redis средства командной строки](https://github.com/MSOpenTech/redis/releases/).
* Подключение с использованием кэша toohello `redis-cli.exe`. Передайте конечную точку кэша hello, используя параметр -h hello и hello ключа с помощью как показано в следующий пример hello:
* `redis-cli -h <your cache="" name="">
  .redis.cache.windows.net -a <key>
  `

> [!NOTE]
> Hello Redis средства командной строки не работают с hello порт SSL, но можно использовать программу, например `stunnel` toosecurely подключения порт SSL toohello средства hello, следуя указаниям hello в hello [объявление поставщика состояний сеансов ASP.NET для Предварительная версия redis](http://blogs.msdn.com/b/webdev/archive/2014/05/12/announcing-asp-net-session-state-provider-for-redis-preview-release.aspx) записи блога.
>
>

<a name="cache-reference"></a>

### <a name="why-doesnt-azure-redis-cache-have-an-msdn-class-library-reference-like-some-of-hello-other-azure-services"></a>Почему отсутствует кэша Redis для Azure MSDN Справочник по библиотеке классов как часть hello другими службами Azure?
Кэш Microsoft Azure Redis на основании hello открытым исходным кодом кэша Redis и может осуществляться разнообразных [клиентов Redis](http://redis.io/clients) для множества языков программирования. Каждый клиент имеет свой собственный API, что делает вызывает toohello Redis кэш экземпляра с помощью [команды Redis](http://redis.io/commands).

Поскольку все клиенты разные, отсутствует одна централизованная ссылка на классы в MSDN, а каждый клиент поддерживает свою собственную справочную документацию. Кроме того, toohello справочная документация, есть несколько учебников, показывающий, как tooget работу с на разных языках и клиентов кэша кэш Azure Redis. tooaccess этих учебников см [как toouse Redis для Azure кэшировать](cache-dotnet-how-to-use-azure-redis-cache.md) и нажмите кнопку hello требуемого языка из переключателя языка hello вверху hello hello статьи.

### <a name="can-i-use-azure-redis-cache-as-a-php-session-cache"></a>Можно ли использовать кэш Redis для Azure как кэш сеанса PHP?
Да, toouse кэша Redis для Azure как кэш сеанса PHP, укажите экземпляр кэша Azure Redis tooyour строки подключения hello в `session.save_path`.

> [!IMPORTANT]
> При использовании в качестве PHP кэш сеанса кэша Redis для Azure, необходимо, чтобы URL-адрес кодирования hello кэша toohello ключа используется tooconnect безопасности, как показано в следующий пример hello:
>
> `session.save_path = "tcp://mycache.redis.cache.windows.net:6379?auth=<url encoded primary or secondary key here>";`
>
> Если ключ hello не является URL-кодированием, появляется исключение с сообщением, например:`Failed tooparse session.save_path`
>
>

Дополнительные сведения об использовании кэша Redis в качестве кэш сеанса PHP с клиентом PhpRedis hello см. в разделе [обработчик сеанса PHP](https://github.com/phpredis/phpredis#php-session-handler).

### <a name="what-are-redis-databases"></a>Что такое базы данных Redis?

Базы данных redis, просто логическое разделение данных в рамках hello же экземпляре Redis. Hello кэш-память распределяется между всеми базами данных hello и потребление памяти фактическое базы данных зависит от hello ключей и значений, хранящихся в этой базе данных. Например, объем кэша C6 составляет 53 ГБ. Вы можете tooput все 53 ГБ в одну базу данных или его можно разделить между несколькими базами данных. 

> [!NOTE]
> При использовании кэша Redis для Azure уровня "Премиум" с включенной кластеризацией доступна только база данных 0. Это ограничение внутреннее ограничение Redis и не определенного tooAzure кэша Redis. Дополнительные сведения см. в разделе [необходимо toomake любые изменения toomy клиентского приложения toouse кластеризации?](cache-how-to-premium-clustering.md#do-i-need-to-make-any-changes-to-my-client-application-to-use-clustering)
> 
> 


<a name="cache-ssl"></a>

### <a name="when-should-i-enable-hello-non-ssl-port-for-connecting-tooredis"></a>Если включить hello не SSL-порт для подключения tooRedis
Сервер Redis не имеет встроенной поддержки SSL, но кэш Redis для Azure имеет. Если вы подключаетесь tooAzure кэша Redis и клиент поддерживает SSL, например StackExchange.Redis, следует использовать SSL.

>[!NOTE]
>Hello не SSL-порт отключен по умолчанию для новых экземпляров кэша Redis для Azure. Если клиент не поддерживает SSL, то необходимо включить порт без поддержки SSL hello, следуя указаниям hello в hello [доступа к портам](cache-configure.md#access-ports) раздел hello [Настройка кэша в кэше Redis для Azure](cache-configure.md) статьи.
>
>

Redis средств, таких как `redis-cli` не работают с hello порт SSL, но можно использовать программу, например `stunnel` toosecurely подключения порт SSL toohello средства hello, следуя указаниям hello в hello [объявление поставщика состояний сеансов ASP.NET Redis предварительной версии](http://blogs.msdn.com/b/webdev/archive/2014/05/12/announcing-asp-net-session-state-provider-for-redis-preview-release.aspx) записи блога.

Инструкции по загрузке hello Redis средств, см. в разделе hello [как можно выполнить команды Redis?](#cache-commands) раздела.

### <a name="what-are-some-production-best-practices"></a>Какие рекомендации следует учитывать для рабочей среды?
* [Рекомендации для StackExchange.Redis](#stackexchangeredis-best-practices)
* [Конфигурация и основные понятия](#configuration-and-concepts)
* [Тестирование производительности](#performance-testing)

#### <a name="stackexchangeredis-best-practices"></a>Рекомендации для StackExchange.Redis
* Задать `AbortConnect` toofalse, подождите, пока hello ConnectionMultiplexer повторное соединение производится автоматически. [Щелкните здесь, чтобы узнать больше](https://gist.github.com/JonCole/36ba6f60c274e89014dd#file-se-redis-setabortconnecttofalse-md).
* Повторное использование hello ConnectionMultiplexer - не создайте новую для каждого запроса. Hello `Lazy<ConnectionMultiplexer>` шаблон [показанный здесь](cache-dotnet-how-to-use-azure-redis-cache.md#connect-to-the-cache) рекомендуется.
* Лучше всего Redis работает с меньшими значениями, поэтому рассмотрите возможность разделения больших данных на несколько ключей. В [этом обсуждении Redis](https://groups.google.com/forum/#!searchin/redis-db/size/redis-db/n7aa2A4DZDs/3OeEPHSQBAAJ) размер в 100 КБ признан "большим". Прочитайте [эту статью](https://gist.github.com/JonCole/db0e90bedeb3fc4823c2#large-requestresponse-size) , чтобы ознакомиться с примером проблемы, вызванной большими значениями.
* Настройка вашего [параметры пула потоков](#important-details-about-threadpool-growth) tooavoid значения времени ожидания.
* Используйте по крайней мере hello connectTimeout по умолчанию 5 секунд. Этот интервал будет достаточно времени toore StackExchange.Redis-установить подключение hello, в случае использовать сети.
* Имейте в виду hello расходов производительности, связанных с другой операции, которые вы используете. Здравствуйте, например, `KEYS` команда является операцией O(n), поэтому следует избегать. Hello [redis.io сайта](http://redis.io/commands/) содержит подробности о сложности hello время для каждой операции, которые его поддерживают. Щелкните сложности hello toosee каждой команды, для каждой операции.

#### <a name="configuration-and-concepts"></a>Конфигурация и основные понятия
* Для систем в рабочей среде используйте уровень "Стандартный" или "Премиум". Hello базового уровня — это система один узел с нет данных репликации и без соглашения об уровне ОБСЛУЖИВАНИЯ. Кроме того, используйте по крайней мере кэш C1. Как правило, кэши C0 используются в простых сценариях разработки и тестирования.
* Помните, что Redis — это хранилище данных **в памяти** . Прочитайте [эту статью](https://gist.github.com/JonCole/b6354d92a2d51c141490f10142884ea4#file-whathappenedtomydatainredis-md) , чтобы ознакомиться со случаями, в которых может произойти потеря данных.
* Разрабатывать системы, таким образом, что он может обрабатывать звуковые сигналы подключения [из-за toopatching и отработки отказа](https://gist.github.com/JonCole/317fe03805d5802e31cfa37e646e419d#file-azureredis-patchingexplained-md).

#### <a name="performance-testing"></a>Тестирование производительности
* Запустить с помощью `redis-benchmark.exe` tooget вид возможных пропускной способности, прежде чем писать тесты производительности. Поскольку `redis-benchmark` не поддерживает SSL, необходимо [включить порт hello без SSL через портал Azure hello](cache-configure.md#access-ports) перед запуском теста hello. Примеры см. в разделе [как оценки производительности и протестировать hello производительность моих кэша?](#how-can-i-benchmark-and-test-the-performance-of-my-cache)
* Клиент Hello виртуальных Машин, используемых для тестирования должен быть в hello же регионе, что экземпляра кэша Redis.
* Мы рекомендуем использовать Dv2 Серия виртуальных Машин для клиентских, как они имеют более высокую оборудования и hello наилучших результатов, следует предоставить.
* Убедитесь, что у виртуальной Машины, выбрать по крайней мере столько возможностями вычислений и пропускной способности кэша hello, которое тестируется клиента.
* Включите VRSS на клиентском компьютере hello, если вы работаете с Windows. [Щелкните здесь, чтобы узнать больше](https://technet.microsoft.com/library/dn383582.aspx).
* Экземпляры Redis уровня "Премиум" обеспечивают меньшие сетевые задержки и большую пропускную способность, так как используют более производительные ЦП и сетевое оборудование.

<a name="cache-redis-commands"></a>

### <a name="what-are-some-of-hello-considerations-when-using-common-redis-commands"></a>Каковы некоторые особенности hello, при использовании общих команд Redis?
* Не следует запускать определенные команды Redis, принимающих toocomplete длительное время без понимание влияния hello этих команд.
  * Например, не запускайте hello [КЛЮЧЕЙ](http://redis.io/commands/keys) команда в рабочей среде, как это может занять tooreturn длительное время в зависимости от числа hello ключи. Redis является однопотоковым сервером и обрабатывает команды по одной. Если у вас есть другие команды, выданные после ключи, они обрабатываться не будут до Redis выполняет команду ключи hello. Hello [redis.io сайта](http://redis.io/commands/) содержит подробности о сложности hello время для каждой операции, которые его поддерживают. Щелкните сложности hello toosee каждой команды, для каждой операции.
* Размеры ключей — следует использовать пары "ключ-значение" небольшого или большого размера? Как правило он зависит от hello сценария. Если сценарий требует длинными ключами, можно настроить hello ConnectionTimeout и повторите значения и измените логику повторных попыток. С точки зрения сервера Redis меньшие значения наблюдаются toohave более высокую производительность.
* Эти вопросы не означает, что нельзя хранить большие значения в Redis; необходимо учитывать следующие соображения hello. Задержки будут выше. Если у вас есть один набор данных, который больше и один, меньший по размеру, можно использовать несколько экземпляров ConnectionMultiplexer, каждый из которых настроен с другим набором значений времени ожидания и повторных попыток, как описано в предыдущем hello [что hello Параметры конфигурации StackExchange.Redis сделать](#cache-configuration) раздела.

<a name="cache-benchmarking"></a>

### <a name="how-can-i-benchmark-and-test-hello-performance-of-my-cache"></a>Как сравнить и протестировать hello производительность моих кэша?
* [Включить диагностику кэша](cache-how-to-monitor.md#enable-cache-diagnostics) так, чтобы [монитор](cache-how-to-monitor.md) hello работоспособности кэша. Можно просмотреть метрики в hello портал Azure и вы также можете hello [Загрузите и прочтите](https://github.com/rustd/RedisSamples/tree/master/CustomMonitoring) их с помощью средств hello по своему усмотрению.
* Можно использовать redis benchmark.exe tooload тестового сервера Redis.
* Убедитесь, что клиент тестирования нагрузки hello и кэш Redis hello в hello одного региона.
* Redis cli.exe и отслеживайте hello кэша, с помощью команды INFO hello.
* Если нагрузки вызывает фрагментацию большого объема памяти, чем масштабировать tooa размер кэш-памяти.
* Инструкции по загрузке hello Redis средств, см. в разделе hello [как можно выполнить команды Redis?](#cache-commands) раздела.

Hello следующие команды показывают пример использования redis benchmark.exe. Для получения точных результатов выполните следующие команды из виртуальной Машины в hello же регионе, что ваш кэш.

* Тестирование конвейерных запросов SET с полезными данными размером в 1 КБ.

  `redis-benchmark.exe -h **yourcache**.redis.cache.windows.net -a **yourAccesskey** -t SET -n 1000000 -d 1024 -P 50`
* Тестирование конвейерных запросов GET с полезными данными размером в 1 КБ.
  Примечание: Выполнение теста hello НАБОР, показанный выше первого toopopulate кэша

  `redis-benchmark.exe -h **yourcache**.redis.cache.windows.net -a **yourAccesskey** -t GET -n 1000000 -d 1024 -P 50`

<a name="threadpool"></a>

### <a name="important-details-about-threadpool-growth"></a>Важные сведения о росте пула потоков ThreadPool
Hello пула потоков CLR имеет два типа потоков — «Рабочих» и «Порт завершения ввода-вывода» (также называемого IOCP) потоки.

* Рабочие потоки используются, например, для обработки методов `Task.Run(…)` или `ThreadPool.QueueUserWorkItem(…)`. Эти потоки также используются различными компонентами в hello CLR необходимости рабочих toohappen в фоновом потоке.
* IOCP потоков используются в случае асинхронного ввода-ВЫВОДА (например, чтение из сети hello).

Hello пул потоков предоставляет новые рабочие потоки или потоки завершения ввода-вывода по требованию (без любой регулирования) до его достигло приветствия «Минимум» для каждого типа потока. По умолчанию hello минимальное количество потоков задано toohello числу процессоров в системе.

Один раз hello количество существующих потоков (занят) попаданий hello «Минимальная» число потоков hello ThreadPool ограничим hello скорость, с которой он вставляет новый поток tooone потоков на 500 миллисекунд. Как правило, если нагрузка системы достигает величины, для которой необходим поток IOCP, то эта работа будет сделана очень быстро. Однако если hello пакетного режима работы больше, чем параметр «Минимум» hello, будет существовать некоторая задержка при обработке некоторых рабочих hello как hello ThreadPool ожидает один из toohappen две вещи.

1. Существующий поток становится рабочих свободного tooprocess hello.
2. Создание нового потока из-за того, что ни один из существующих потоков не стал доступным в течение 500 мс.

По сути это означает, что при hello число занятых потоков больше, чем потоков Min, скорее всего оплате задержки 500 мс перед обработкой сетевого трафика, приложение hello. Кроме того является важным toonote, что если в имеющемся поток остается простоя в течение более 15 секунд (с учетом я запомнить), он будут очищены и можно повторять этот цикл роста и возможность сжатия.

Если взглянуть на пример сообщения об ошибке от StackExchange.Redis (сборка 1.0.450 или более поздней версии), вы увидите, что теперь оно содержит статистику ThreadPool (подробности о рабочих потоках и потоках IOCP см. ниже).

    System.TimeoutException: Timeout performing GET MyKey, inst: 2, mgr: Inactive,
    queue: 6, qu: 0, qs: 6, qc: 0, wr: 0, wq: 0, in: 0, ar: 0,
    IOCP: (Busy=6,Free=994,Min=4,Max=1000),
    WORKER: (Busy=3,Free=997,Min=4,Max=1000)

В предыдущем примере hello вы увидите, что для потока IOCP 6 занятых потоков, а системы hello менее потоков настроенных tooallow 4. В этом случае клиента hello бы скорее всего видимой два 500 мс задержки из-за 6 > 4.

Обратите внимание, что StackExchange.Redis может достигнуть времени ожидания, если происходит регулирование количества рабочих потоков или потоков IOCP.

### <a name="recommendation"></a>Рекомендации
Имея эту информацию, мы настоятельно рекомендуется клиентов hello значение минимальной конфигурации для IOCP и РАБОЧИЕ потоки toosomething больше, чем значение по умолчанию hello. Мы не может дать универсальными указания на то, что это значение должно быть поскольку hello надлежащее значение для одного приложения будет слишком высокой и низкой для другого приложения. Также этот параметр может повлиять на производительность hello других частей сложных приложений, поэтому каждого заказчика должен toofine настройки, необходимые для этого конкретного параметра tootheir. Хорошей отправной точкой является 200 или 300, после чего нужно проверить и изменить этот параметр в соответствии с результатом.

Как tooconfigure этот параметр:

* В ASP.NET, используйте hello [параметр конфигурации «minIoThreads»] [ "minIoThreads" configuration setting] под hello `<processModel>` элемента конфигурации в файле web.config. При выполнении внутри веб-сайтов Azure, этот параметр не предоставляется с помощью параметров конфигурации hello. Тем не менее, все равно следует быть может tooconfigure этот параметр, программно (см. ниже) в global.asax.cs метод Application_Start.

  > [!NOTE] 
  > Hello значение, указанное в этом элементе конфигурации, *-core* параметр. Например, если имеется 4-ядерный компьютер и хотите вашей toobe параметр minIOThreads 200 во время выполнения, можно использовать `<processModel minIoThreads="50"/>`.
  >

* За пределами ASP.NET, используйте hello [ThreadPool.SetMinThreads(...) ](https://msdn.microsoft.com/library/system.threading.threadpool.setminthreads.aspx) API.

<a name="server-gc"></a>

### <a name="enable-server-gc-tooget-more-throughput-on-hello-client-when-using-stackexchangeredis"></a>Включить tooget сборщик Мусора сервера при использовании StackExchange.Redis большую нагрузку на приветствия клиента
Включение сервера глобального Каталога можно оптимизировать клиента hello и обеспечивают более высокую производительность и пропускную способность, при использовании StackExchange.Redis. Дополнительные сведения о сервере глобального Каталога и как tooenable, см. следующие статьи hello:

* [сборщик Мусора сервера tooenable](https://msdn.microsoft.com/library/ms229357.aspx)
* [Основные сведения о сборке мусора](https://msdn.microsoft.com/library/ee787088.aspx)
* [Сборка мусора и производительность](https://msdn.microsoft.com/library/ee851764.aspx)


### <a name="performance-considerations-around-connections"></a>Рекомендации по производительности для подключений

Каждая ценовая категория имеет различные ограничения для количества клиентских подключений, памяти и пропускной способности. Хотя каждый размер кэша позволяет *до* определенное количество соединений, каждого подключения tooRedis издержки связан. Примером таких накладных расходов могут служить загрузка ЦП и использование памяти в результате шифрования TLS/SSL. Hello максимальное количество подключений для размера кэша предполагается со слабой загрузкой кэша. Если загрузить из соединения издержки *, а также* нагрузки от операции клиента превышает лимит, определенный для системы hello, hello кэша могут возникать проблемы производительности, даже если не превышено ограничение числа подключений hello для hello текущий размер кэша.

Дополнительные сведения об ограничениях hello разных подключений для каждого уровня см. в разделе [стоимость кэша Redis Azure](https://azure.microsoft.com/pricing/details/cache/). Дополнительные сведения о подключениях и других конфигурациях по умолчанию см. в статье [Конфигурация сервера Redis по умолчанию](cache-configure.md#default-redis-server-configuration).

<a name="cache-monitor"></a>

### <a name="how-do-i-monitor-hello-health-and-performance-of-my-cache"></a>Как отслеживать hello работоспособность и производительность моих кэша?
Экземпляры кэша Microsoft Azure Redis можно наблюдать в hello [портал Azure](https://portal.azure.com). Можно просмотреть метрики, закрепить диаграммы метрик toohello начальной панели, настроить hello диапазон дат и времени диаграмм мониторинга, добавить и удалить метрики из диаграмм hello и настроить оповещения при выполнении определенных условий. Дополнительные сведения см. в статье [Как отслеживать кэш Redis для Azure](cache-how-to-monitor.md).

Hello кэша Redis **ресурсов меню** также содержит несколько средств для наблюдения и устранения неполадок ваших кэшей.

* **Диагностика и решение проблем** предоставляет сведения об основных проблемах и способах их устранения.
* Служба **работоспособности ресурсов** отслеживает ресурс и сообщает, работает ли он как ожидалось. Дополнительные сведения о hello службы работоспособности ресурсов Azure см. в разделе [Обзор работоспособности ресурсов Azure](../resource-health/resource-health-overview.md).
* **Новый запрос на поддержку** предоставляет параметры tooopen запрос на техническую поддержку для кэша.

Эти средства включите вы toomonitor hello работоспособности экземпляров кэша Redis для Azure и сведения об управлении приложениями кэширования. Дополнительные сведения см. в разделе hello «поддержка параметры устранения неполадок» в разделе & [как tooconfigure Redis для Azure кэшировать](cache-configure.md).

<a name="cache-timeouts"></a>

### <a name="why-am-i-seeing-timeouts"></a>Почему я наблюдаю простои?
Время ожидания произойдет hello клиента используется tootalk tooRedis. При отправке команды серверу Redis toohello помещено команда hello и со временем сервера Redis выбирает команду hello и выполняет его. Тем не менее можно hello клиента время ожидания в ходе этого процесса и если это происходит исключение возникает на вызов стороны hello. Дополнительные сведения об устранении проблем со временем ожидания см. в разделах [Устранение проблем на стороне клиента](cache-how-to-troubleshoot.md#client-side-troubleshooting) и [Исключения времени ожидания StackExchange.Redis](cache-how-to-troubleshoot.md#stackexchangeredis-timeout-exceptions).

<a name="cache-disconnect"></a>

### <a name="why-was-my-client-disconnected-from-hello-cache"></a>Почему мой клиент был отключен от hello кэша?
Hello ниже приведены некоторые распространенная причина отключения кэша.

* Причины на стороне клиента
  * клиентское приложение Hello был повторного развертывания.
  * клиентское приложение Hello выполняется операция масштабирования.
    * В случае hello облачных служб или веб-приложений, это может быть обусловлено tooauto масштабирования.
  * сетевой уровень Hello на стороне клиента hello изменен.
  * Временные ошибки в клиенте hello или в узлы сети hello между hello клиентом и сервером hello.
  * были Достигнуто пороговое значение ограничения Hello пропускной способности.
  * ЦП привязан операций заняло слишком много времени toocomplete.
* Причины на стороне сервера
  * На hello предложение кэша standard hello службы кэша Azure Redis инициировать отработку отказа из hello основного узла toohello дополнительного узла.
  * Azure исправления hello экземпляра, где был развернут hello кэша
    * Это могли быть обновления сервера Redis или обычное обслуживание ВМ.

### <a name="which-azure-cache-offering-is-right-for-me"></a>Какой кэш Azure подходит мне?
> [!IMPORTANT]
> Согласно прошлогоднему [объявлению](https://azure.microsoft.com/blog/azure-managed-cache-and-in-role-cache-services-to-be-retired-on-11-30-2016/), использование управляемой службы кэша Azure и службы кэша роли Azure **было прекращено** 30 ноября 2016 г. Рекомендуется toouse [кэш Azure Redis](https://azure.microsoft.com/services/cache/). Сведения о миграции см. в разделе [миграция из управляемой службы кэша tooAzure кэша Redis](cache-migrate-to-redis.md).
>
>

### <a name="azure-redis-cache"></a>кэш Azure Redis
Кэш Azure Redis имеет доступно в размерах too53 Гбайт и доступность по SLA до 99,9%. новый Hello [уровня premium](cache-premium-tier-intro.md) предлагает размеры too530 ГБ и поддержка кластеризации виртуальной сети и сохраняемости с 99,9% SLA.

Azure кэша Redis дает клиентам hello возможность toouse безопасным, выделенному кэшу Redis под управлением Майкрософт. Это предложение позволяет получить tooleverage hello богатый набор функций и экосистему Redis и надежного размещения и мониторинга Майкрософт.

В отличие от обычных кэшей, работающих только с парами «ключ — значение», Redis популярен благодаря его высокоэффективным типам данных. Redis также поддерживает выполнение атомарных операций на эти типы, такие как добавление tooa строку. значение приращения hello в хэш-кода; Опубликуйте список tooa; Вычисление пересечения наборов, объединения и отличием: или получении hello элемент с наивысшим рейтингом в отсортированном наборе. Другие возможности включают поддержку транзакций, pub/sub, сценарии Lua, ключи с ограниченным срока жизни и toomake параметры конфигурации Redis ведут себя как традиционные кэш.

Другим ключевым аспектом tooRedis успех — hello открытым исходным кодом жизнеспособная экосистема возникшая вокруг него. Это отражено в различных наборов hello клиенты Redis, доступные для нескольких языков. Это экосистемы и широкий спектр клиентов позволяют toobe кэша Redis для Azure, используемые практически любой рабочей нагрузки, создаваемой в Azure.

Дополнительные сведения о начале работы с кэша Redis для Azure см. в разделе [как tooUse Redis для Azure кэшировать](cache-dotnet-how-to-use-azure-redis-cache.md) и [документации кэш Azure Redis](index.md).

### <a name="managed-cache-service"></a>Управляемая служба кэша
[Использование управляемой службы кэша было прекращено 30 ноября 2016 г.](https://azure.microsoft.com/blog/azure-managed-cache-and-in-role-cache-services-to-be-retired-on-11-30-2016/)

tooview архивировать документации, в разделе [архивированные управляемый кэш документации по службе](https://msdn.microsoft.com/library/azure/dn386094.aspx).

### <a name="in-role-cache"></a>Кэш в роли
[Использование службы кэша роли было прекращено 30 ноября 2016 г.](https://azure.microsoft.com/blog/azure-managed-cache-and-in-role-cache-services-to-be-retired-on-11-30-2016/)

tooview архивировать документации, в разделе [архивированные документации кэша в роли](https://msdn.microsoft.com/library/azure/dn386103.aspx).

["minIoThreads" configuration setting]: https://msdn.microsoft.com/library/vstudio/7w2sway1(v=vs.100).aspx
