---
title: "aaaLog аналитика часто задаваемые вопросы | Документы Microsoft"
description: "Вопросы и ответы о hello службы анализа журналов Azure toofrequently ответы."
services: log-analytics
documentationcenter: 
author: MGoedtel
manager: carmonm
editor: 
ms.assetid: ad536ff7-2c60-4850-a46d-230bc9e1ab45
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/18/2017
ms.author: magoedte
ms.openlocfilehash: 25931f521cbb6ec840184221c6c1a5794b3445f0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="log-analytics-faq"></a>Часто задаваемые вопросы по Log Analytics
В этом списке вопросов и ответов от Майкрософт приведены часто задаваемые вопросы о Log Analytics в Microsoft Operations Management Suite (OMS). Если у вас есть дополнительные вопросы о службе анализа журналов, воспользуйтесь toohello [дискуссионный форум](https://social.msdn.microsoft.com/Forums/azure/home?forum=opinsights) и задайте свои вопросы. Часто вопрос, мы поместить toothis статьи, чтобы можно было найти быстро и легко.

## <a name="general"></a>Общие сведения

### <a name="q-does-log-analytics-use-hello-same-agent-as-azure-security-center"></a>В. Служба аналитики журналов использовать hello же агента как центр безопасности Azure?

О. В начале июня 2017 г. центра безопасности Azure начала с помощью Microsoft Monitoring Agent hello toocollect и хранилища данных. toolearn более, в разделе [безопасности Azure Center миграции платформы часто задаваемые вопросы о](../security-center/security-center-platform-migration-faq.md).

### <a name="q-what-checks-are-performed-by-hello-ad-and-sql-assessment-solutions"></a>В. Какие проверки проводятся по hello AD и решения по оценке SQL?

О. Hello следующий запрос показывает описание всех проверок в настоящее время:

```
(Type=SQLAssessmentRecommendation OR Type=ADAssessmentRecommendation) | dedup RecommendationId | select FocusArea, ActionArea, Recommendation, Description | sort Type, FocusArea,ActionArea, Recommendation
```

Hello результаты затем могут быть экспортированного tooExcel для дальнейшего анализа.

### <a name="q-why-do-i-see-something-different-than-oms-in-system-center-operations-manager-console"></a>В. Почему в консоли System Center Operations Manager отображается другое значение (не *OMS*?)

О. В зависимости от того, какую версию накопительного обновления Operations Manager вы используете, может отображаться узел *System Center Advisor*, *Operational Insights* или *Log Analytics*.

Здравствуйте, обновление строки текста слишком*OMS* включается в пакет управления, который необходимо импортировать вручную toobe. текущий текст hello toosee и функциональные возможности, следуйте инструкциям hello hello последнюю System Center Operations Manager Накопительном пакете обновления статьи и обновить hello консоли.

### <a name="q-is-there-an-on-premises-version-of-log-analytics"></a>В. Существует ли *локальная* версия Log Analytics?

О. Нет. Log Analytics обрабатывает и сохраняет большие объемы данных. Как облачная служба аналитики журналов может tooscale очистки при необходимости и избежать любой среде tooyour влияние производительности.

К преимуществам относятся:
- Майкрософт выполняет hello анализа журналов инфраструктуры, экономит затраты
- Развертывание регулярных обновлений и исправлений.

### <a name="q-how-do-i-troubleshoot-that-log-analytics-is-no-longer-collecting-data"></a>В. Как можно понять, что Log Analytics больше не собирает данные?

Ответ, если вы используете hello бесплатной ценовой категории и отправили более 500 МБ данных в день, hello оставшейся части дня hello останавливает сбор данных. Когда достигается предельное значение ежедневного hello является распространенной причиной, которое служба аналитики журналов останавливает сбор данных или данные появляются toobe отсутствует.

Log Analytics создает событие типа *Операция*, когда сбор данных начинается и останавливается. 

Выполните следующий запрос в toocheck поиска при достижении предельного hello и отсутствующие данные hello.`Type=Operation OperationCategory="Data Collection Status"`

Когда сбор данных прекращается, hello *OperationStatus* — **предупреждение**. После запуска сбора данных hello *OperationStatus* — **успешно**. 

Hello следующей таблице описаны причины, по которым останавливает сбор данных и коллекцию данных tooresume предлагаемое действие:

| Причина прекращения сбора данных                       | Сбор данных tooresume |
| -------------------------------------------------- | ----------------  |
| Достигнут предел ежедневного сбора данных, предоставляемый бесплатно<sup>1</sup>       | Подождите, пока не hello следующий день для перезагрузки tooautomatically коллекции, или<br> Изменение tooa платная ценовой категории |
| Подписка Azure находится в состоянии "Приостановлено" по причине: <br> Период бесплатной пробной версии завершен <br> Истек срок действия Azure Pass <br> Достигнут лимит ежемесячной суммы расходов (например, на подписку MSDN или Visual Studio)                          | Преобразовать tooa платная подписка <br> Преобразовать tooa платная подписка <br> Удалите ограничение или подождите, пока оно сбросится |

<sup>1</sup> Если hello бесплатной ценовой категории рабочей области, вы можете toosending 500 МБ в день toohello службы. По достижении предельного hello, сбор данных останавливается до следующего дня hello. Данные, передаваемые во время остановки сбора данных, не индексируется и не доступны для поиска. Когда сбор данных возобновляется, обработка выполняется только для новых передаваемых данных. 

Log Analytics использует время в формате UTC и каждый день начинается в полночь по времени UTC. Если рабочей hello достигает предельного hello, обработка возобновляется во время первого часа hello следующий день UTC hello.

### <a name="q-how-can-i-be-notified-when-data-collection-stops"></a>В. Как получить уведомление о прекращении сбора данных?

Ответ использовать hello действия, описанные в [создать правило оповещения](log-analytics-alerts-creating.md#create-an-alert-rule) toobe уведомления при остановке сбора данных.

При создании оповещения hello для остановки сбора данных, задать:
- **Имя** слишком*остановки сбора данных*
- **Серьезность** слишком*предупреждение*
- **Запрос поиска** слишком`Type=Operation OperationCategory="Data Collection Status" OperationStatus=Warning`
- **Временное окно** слишком*2 часа*.
- **Предупреждения частоты** toobe один час, так как данные об использовании hello обновляется только один раз в час.
- **Создать предупреждение на основе** toobe *число результатов*
- **Количество результатов** toobe *больше 0*

Используйте hello действия, описанные в [добавить правила tooalert действия](log-analytics-alerts-actions.md) настройку действия электронной почты, веб-перехватчик или runbook для правила оповещения hello.


## <a name="configuration"></a>Конфигурация
### <a name="q-can-i-change-hello-name-of-hello-tableblob-container-used-tooread-from-azure-diagnostics-wad"></a>В. Можно изменить имя hello tooread контейнер, используемый hello таблицы или большого двоичного объекта из Azure Diagnostics (WAD)?

О. Нет, это не поддерживается в настоящее время tooread из произвольных таблиц или контейнеров в хранилище Azure.

### <a name="q-what-ip-addresses-does-hello-log-analytics-service-use-how-do-i-ensure-that-my-firewall-only-allows-traffic-toohello-log-analytics-service"></a>В. IP-адреса hello использование службы анализа журналов? Как убедитесь, что Мой брандмауэр только разрешает трафик toohello анализа журналов службы?

О. Служба аналитики журнала Hello строится на основе Azure. Журнал аналитики IP-адреса находятся в hello [Microsoft Azure Datacenter диапазоны IP-адресов](http://www.microsoft.com/download/details.aspx?id=41653).

При развертывании службы, измените hello фактические IP-адреса hello службы анализа журналов. tooallow имена DNS Hello в брандмауэре, задокументированы в [Настройка параметров прокси-сервера и брандмауэра в службе анализа журналов](log-analytics-proxy-firewall.md).

### <a name="q-i-use-expressroute-for-connecting-tooazure-does-my-log-analytics-traffic-use-my-expressroute-connection"></a>В. Я использую ExpressRoute для подключения tooAzure. Будет ли трафик Log Analytics использовать подключение ExpressRoute?

О. Hello различные типы трафика ExpressRoute описаны в hello [документации по ExpressRoute](../expressroute/expressroute-faqs.md#supported-services).

TooLog трафик аналитики использует схему общедоступного пиринга ExpressRoute hello.

### <a name="q-is-there-a-simple-and-easy-way-toomove-an-existing-log-analytics-workspace-tooanother-log-analytics-workspaceazure-subscription"></a>В. Есть ли toomove простой способ существующей рабочей области аналитики журналов tooanother анализа журналов рабочей области или подписку Azure?

О. Hello `Move-AzureRmResource` командлет позволяет перемещать из одной подписки Azure tooanother рабочей области аналитики журналов, а также учетной записи автоматизации. Дополнительные сведения см. в документации [Move-AzureRmResource](http://msdn.microsoft.com/library/mt652516.aspx).

Это изменение также могут быть созданы в hello портал Azure.

Нельзя перемещать данные из одной tooanother рабочей области аналитики журналов или изменить регион hello, данные аналитики журналов хранятся в.

### <a name="q-how-do-i-add-log-analytics-toosystem-center-operations-manager"></a>Вопрос. как добавить журнала аналитика tooSystem Center Operations Manager?

Ответ. Установка последнего накопительного пакета обновления toohello и импорт пакетов управления позволяет Operations Manager tooconnect tooLog Analytics.

>[!NOTE]
>tooLog подключение Operations Manager Hello Analytics доступна только для System Center Operations Manager 2012 SP1 и более поздних версий.

### <a name="q-how-can-i-confirm-that-an-agent-is-able-toocommunicate-with-log-analytics"></a>Вопрос. как убедиться, что агент является toocommunicate может с помощью аналитики журналов?

Ответ tooensure этот hello агент может взаимодействовать с OMS, перейдите на: панель управления, безопасности и параметров, **Microsoft Monitoring Agent**.

В разделе hello **анализа журналов Azure (OMS)** вкладки, найдите зеленую галочку. Зеленый значок подтверждает, что этот агент hello находится может toocommunicate с hello службой OMS.

Желтый значок предупреждения означает, что агент hello испытывает проблемы связи с OMS. Одна из основных причин — hello службу Microsoft Monitoring Agent остановлена. Используйте hello диспетчер управления toorestart службы.

### <a name="q-how-do-i-stop-an-agent-from-communicating-with-log-analytics"></a>В. Как остановить взаимодействие агента с Log Analytics?

Ответ в System Center Operations Manager, удалите hello компьютера из списка управляемых компьютеров hello помощник по настройке ядра. Operations Manager обновлений hello конфигурацию hello агента toono больше времени отчета tooLog Analytics. Для агентов непосредственно подключен tooLog Analytics, их можно остановить передачу данных через: панель управления, безопасности и параметров, **Microsoft Monitoring Agent**.
В разделе **Azure Log Analytics (OMS)** удалите все рабочие области.

### <a name="q-why-am-i-getting-an-error-when-i-try-toomove-my-workspace-from-one-azure-subscription-tooanother"></a>Вопрос. Почему я получаю ошибку при попытке toomove мою рабочую область из одной подписки Azure tooanother?

Ответ, если вы используете hello портал Azure, убедитесь, что для перемещения hello выбирается только hello рабочую область. Не устанавливайте решений hello--автоматически переместится после перемещения hello рабочей области. 

Убедитесь, что у вас есть разрешение в обеих подписках Azure.

## <a name="agent-data"></a>Данные агента
### <a name="q-how-much-data-can-i-send-through-hello-agent-toolog-analytics-is-there-a-maximum-amount-of-data-per-customer"></a>В. Сколько данных можно отправить через агент hello tooLog аналитика Существует ли максимальный объем данных для одного клиента?
О. план free Hello задает ежедневный лимит в размере 500 МБ в рабочей области. Hello standard и premium планы имеют неограниченно hello объемом данных, который загружается. Как облачная служба, аналитика журналов предназначена tooautomatically масштабирования тома hello toohandle поступающих от клиентов данных — даже если это несколько терабайт в день.

агенту службы анализа журналов Hello не спроектированный tooensure имеет небольшого размера. Один из наших клиентов написал в блог статью о тестах hello от нашего агента и как сильном они находились. тома данных Hello различается в зависимости от hello решений, которые можно включить. Можно найти подробные сведения об объемах данных hello и увидеть разбиение hello решением в hello [использование](log-analytics-usage.md) страницы.

Дополнительные сведения вы найдете [блоге клиента](http://thoughtsonopsmgr.blogspot.com/2015/09/one-small-footprint-for-server-one.html) о небольшом объеме агента OMS hello hello.

### <a name="q-how-much-network-bandwidth-is-used-by-hello-microsoft-management-agent-mma-when-sending-data-toolog-analytics"></a>В. Какую полосу пропускания сети используется hello Microsoft Management Agent (MMA) при отправке данных tooLog Analytics?

О. Пропускная способность — это функция от hello объема отправляемых данных. Данные сжимаются при передаче по сети hello.

### <a name="q-how-much-data-is-sent-per-agent"></a>В. Какой объем данных отправляет каждый агент?

О. зависит от Hello объем данных, отправляемых на каждого агента.

* Hello решений, которые вы выбрали
* Hello числа журналов и счетчиков производительности во время сбора
* Hello объем данных в журналах hello

Hello бесплатной ценовой категории — tooonboard хорошим способом несколько серверов и датчиков hello типичный объем данных. Общее использование отображается на hello [использование](log-analytics-usage.md) страницы.

На компьютерах, где работает агент WireData может toorun hello используйте следующие toosee запроса, какой объем данных, отправляемых hello:

```
Type=WireData (ProcessName="C:\\Program Files\\Microsoft Monitoring Agent\\Agent\\MonitoringHost.exe") (Direction=Outbound) | measure Sum(TotalBytes) by Computer
```



## <a name="next-steps"></a>Дальнейшие действия
* [Начало работы с помощью аналитики журналов](log-analytics-get-started.md) toolearn Дополнительные сведения о службе анализа журналов и получите работающий в минутах.
