---
title: "aaaIntroduction tooAzure безопасности | Документы Microsoft"
description: "Узнайте о системе безопасности Azure, ее службах и принципах работы."
services: security
documentationcenter: na
author: UnifyCloud
manager: swadhwa
editor: TomSh
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/03/2017
ms.author: TomSh
ms.openlocfilehash: 2d42057e9586a0b6ce16a1582db3b3af842297af
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooazure-security"></a>Введение tooAzure безопасности
## <a name="overview"></a>Обзор
Мы знаем, что безопасность обеспечивается одно задание в облаке hello и насколько важно что вам точные и актуальную информацию о безопасности в Azure. Одна из hello наиболее причин toouse Azure для приложений и служб — tootake преимуществами широком наборе средств обеспечения безопасности и возможностей. Эти средства и возможности повышения его возможных toocreate надежные решения для безопасной платформы Azure hello. Microsoft Azure обеспечивает конфиденциальность, целостность и доступность данных клиента, а также прозрачный учет.

лучше понять hello коллекции элементов управления безопасностью в Microsoft Azure реализован hello клиента и Microsoft operations различными способами, в этом техническом документе «Введение tooAzure безопасности», toohelp записывается tooprovide Подробный обзор безопасности hello, доступные с помощью Microsoft Azure.

### <a name="azure-platform"></a>Платформа Azure
Azure — общедоступная облачная платформа, которая поддерживает широкий выбор операционных систем, языков программирования, платформ, инструментов, баз данных и устройств. В ней можно запускать контейнеры Linux с интеграцией Docker, создавать приложения на языках JavaScript, Python, .NET, PHP, Java и Node.js, разрабатывать серверные решения для устройств под управлением iOS, Android и Windows.

Общедоступное облако Azure службы поддерживают hello уже зависит от одной технологии миллионам разработчиков и ИТ-специалистов и доверия. При выполнении сборки или миграции ИТ-ресурсы, общедоступное облако поставщика услуг, зависит от возможности tooprotect этой организации приложений и данных со службами hello и элементы управления hello, они предоставляют toomanage hello безопасность на основе облака активы.

Инфраструктуры Azure разработан из tooapplications средство для размещения миллионы клиентов одновременно, а также trustworthy основу, на которой предприятий могут требования к безопасности.

Кроме того, Azure предоставляет широкий набор toocontrol возможности безопасности можно настроить параметры и hello их, чтобы вы могли изменять toomeet hello уникальные требования к безопасности вашей организации развертываний. Данный документ поможет вам понять, каким образом функции безопасности Azure позволяют удовлетворить эти требования.

> [!Note]
> Основная цель Hello этого документа — в элементе управления, ориентированных на клиента, можно использовать toocustomize и повышения уровня безопасности для приложений и служб.
>
> Мы предоставляем некоторые общие сведения, но Дополнительные сведения о том, как корпорация Майкрософт защищает hello платформы Azure, см. сведения в hello [Центр управления безопасностью Microsoft](https://www.microsoft.com/TrustCenter/default.aspx).

### <a name="abstract"></a>Аннотация
Изначально миграции общедоступное облако было определялось tooinnovate динамично и экономии затрат. Некоторое время безопасность считалась серьезной проблемой и даже непреодолимым препятствием для миграции в общедоступное облако. Тем не менее общедоступного облака безопасности была переведена с основной tooone проблемой hello драйверов для миграции в облако. Hello обоснованием это — hello превосходит возможности приложений tooprotect поставщики больших общедоступных облачных служб и данных hello облачных ресурсов.

Из tooapplications территории hello для размещения миллионы клиентов одновременно предназначен инфраструктуры Azure и предоставляет trustworthy основу, на которой предприятия требованиям их безопасности. Кроме того, Azure предоставляет широкий набор toocontrol возможности безопасности можно настроить параметры и hello их, чтобы вы могли изменять toomeet hello уникальные требования к безопасности вашего toomeet развертывания ЕГО политики управления и соответствуют tooexternal правила.

В этом документе описаны toosecurity подход корпорации Майкрософт в рамках облачной платформы Microsoft Azure hello.
* Средства безопасности, реализованный Microsoft hello toosecure инфраструктуры Azure данные клиентов и приложений.
* Azure служб и безопасности компоненты доступны tooyou toomanage hello безопасности служб hello и ваши данные в ваших подписок Azure.

## <a name="summary-azure-security-capabilities"></a>Сводка возможностей системы безопасности Azure
следующие таблицы Hello укажите краткое описание функций безопасности hello корпорацией Майкрософт toosecure hello инфраструктуры Azure, данные клиентов и безопасных приложений.
### <a name="security-features-implemented-toosecure-hello-azure-platform"></a>Безопасность компоненты, реализованные tooSecure hello платформы Azure:
Hello компоненты в списке следующие, возможности, можно просмотреть Software assurance hello tooprovide приветствия, платформа Azure осуществляется в безопасном режиме. Вы можете воспользоваться предоставленными ссылками, чтобы подробнее узнать, как корпорация Майкрософт учитывает вопросы доверия клиентов в четырех областях: безопасная платформа, конфиденциальность и контроль, соответствие и прозрачность.


| [Безопасная платформа](https://www.microsoft.com/en-us/trustcenter/Security/default.aspx)  | [Конфиденциальность и контроль](https://www.microsoft.com/en-us/trustcenter/Privacy/default.aspx)  |[Соответствие требованиям](https://www.microsoft.com/en-us/trustcenter/Compliance/default.aspx)   | [Прозрачность](https://www.microsoft.com/en-us/trustcenter/Transparency/default.aspx) |
| :-- | :-- | :-- | :-- |
| [Цикл разработки средств безопасности](https://www.microsoft.com/en-us/sdl/), внутренний аудит | [Управлять данными на все время hello](https://www.microsoft.com/en-us/trustcenter/Privacy/You-own-your-data) | [Центр управления безопасностью](https://www.microsoft.com/en-us/trustcenter/default.aspx) |[Как корпорация Майкрософт защищает данные клиентов в службах Azure](https://www.microsoft.com/en-us/trustcenter/Transparency/default.aspx) |
| [Обязательное обучение безопасности, проверки данных](https://www.google.com/url?sa=t&rct=j&q=&esrc=s&source=web&cd=2&cad=rja&uact=8&ved=0ahUKEwiwsOCpganRAhWqxVQKHUdiDsMQFghAMAE&url=https%3A%2F%2Fdownloads.cloudsecurityalliance.org%2Fstar%2Fself-assessment%2FStandardResponsetoRequestforInformationWindowsAzureSecurityPrivacy.docx&usg=AFQjCNEYvBky4zNeDQPN6YJGPFRZA7eeZg&sig2=2kkw1lOCP_kzLzgE9RS2Tg&bvm=bv.142059868,d.amc) |  [Управление расположением данных](https://www.microsoft.com/en-us/trustcenter/Privacy/Where-your-data-is-located) |  [Common Controls Hub](https://www.microsoft.com/en-us/trustcenter/Common-Controls-Hub) |[Как корпорация Майкрософт управляет расположением данных в службах Azure](http://azuredatacentermap.azurewebsites.net/)|
| [Выполнение тестов на проникновение](https://www.google.com/url?sa=t&rct=j&q=&esrc=s&source=web&cd=2&cad=rja&uact=8&ved=0ahUKEwiwsOCpganRAhWqxVQKHUdiDsMQFghAMAE&url=https%3A%2F%2Fdownloads.cloudsecurityalliance.org%2Fstar%2Fself-assessment%2FStandardResponsetoRequestforInformationWindowsAzureSecurityPrivacy.docx&usg=AFQjCNEYvBky4zNeDQPN6YJGPFRZA7eeZg&sig2=2kkw1lOCP_kzLzgE9RS2Tg&bvm=bv.142059868,d.amc), [обнаружение вторжений и атак DDoS](https://www.microsoft.com/en-us/trustcenter/Security/ThreatManagemen), [аудит и ведение журнала](https://www.microsoft.com/en-us/trustcenter/Security/AuditingAndLogging) | [Предоставление доступа к данным на ваших условиях](https://www.microsoft.com/en-us/trustcenter/Privacy/Who-can-access-your-data-and-on-what-terms) |  [Контрольный список облачных служб из-за экспертизы Hello](https://www.microsoft.com/en-us/trustcenter/Compliance/Due-Diligence-Checklist) |[Кто в корпорации Майкрософт имеет доступ к вашим данным и на каких условиях](https://www.microsoft.com/en-us/trustcenter/Privacy/Who-can-access-your-data-and-on-what-terms)|
| [Современный центр обработки данных](https://www.microsoft.com/en-us/cloud-platform/global-datacenters), физическая безопасность, [безопасная сеть](https://docs.microsoft.com/en-us/azure/security/security-network-overview) | [Отвечать на запросы toolaw применения](https://www.microsoft.com/en-us/trustcenter/Privacy/Responding-to-govt-agency-requests-for-customer-data) |  [Соответствие служб, расположений и отрасли](https://www.microsoft.com/en-us/trustcenter/Compliance/default.aspx) |[Как корпорация Майкрософт защищает данные клиентов в службах Azure](https://www.microsoft.com/en-us/trustcenter/Transparency/default.aspx)|
|  [Реагирование на инциденты безопасности](http://aka.ms/SecurityResponsepaper), [разделение ответственности](http://aka.ms/sharedresponsibility) |[Строгие стандарты конфиденциальности](https://www.microsoft.com/en-us/TrustCenter/Privacy/We-set-and-adhere-to-stringent-standards) |  | [Проверка сертификации для служб Azure, центр обеспечения прозрачности](https://www.microsoft.com/en-us/trustcenter/Compliance/default.aspx)|



### <a name="security-features-offered-by-azure-toosecure-data-and-application"></a>Безопасность функции предложенное Azure tooSecure данных и приложений
В зависимости от модели hello облачной службы нет переменных ответственность за кто отвечает за управление безопасностью hello hello приложения или службы. Возможности доступны в tooassist hello платформы Azure, вы удовлетворения эти обязанности через встроенные функции и решения, которые могут быть развернуты в подписку Azure партнеров.

встроенные функции Hello организованы в шесть (6) функциональных областей: Operations, приложения, хранилища, сети, вычислений и удостоверений. Дополнительные сведения о функции hello и возможности, доступные в hello платформы Azure в этих областях шести (6), предоставляются через сводные данные.

## <a name="operations"></a>Операции
Этот раздел содержит дополнительные сведения о ключевых функциях операций безопасности, а также сводные сведения об этих функциях.

### <a name="operations-management-suite-security-and-audit-dashboard"></a>Панель мониторинга "Безопасность и аудит" в Operations Management Suite
Hello [решения OMS безопасность и аудит](https://docs.microsoft.com/azure/operations-management-suite/oms-security-getting-started) дает полное представление в вашей организации и информационной безопасности [встроенные поисковые запросы](https://blogs.technet.microsoft.com/msoms/2016/01/21/easy-microsoft-operations-management-suite-search-queries/) важных моментов, требующих вашего внимания. Hello [безопасность и аудит](https://technet.microsoft.com/library/mt484091.aspx) мониторинга связана с начального экрана приветствия для всего toosecurity в OMS. Он предоставляет высокоуровневый анализ hello состояние безопасности компьютеров. Она также включает возможность tooview hello все события hello за последние 24 часа, 7 дней или другие пользовательские промежуток времени.

Кроме того, можно настроить OMS безопасность и соответствие требованиям слишком[автоматически выполнять определенные действия](https://blogs.technet.microsoft.com/robdavies/2016/04/20/simple-look-at-oms-alert-remediation-with-runbooks-part-1/) при обнаружении определенного события.

### <a name="azure-resource-manager"></a>Диспетчер ресурсов Azure
[Диспетчер ресурсов Azure ](https://docs.microsoft.com/azure/azure-resource-manager/resource-manager-deployment-model) позволяет toowork с ресурсами hello в ваше решение как группу. Можно развернуть, обновить или удалить все ресурсы hello для вашего решения, в один, согласованной операции. Развертывание осуществляется на основе [шаблона Azure Resource Manager](https://blogs.technet.microsoft.com/canitpro/2015/06/29/devops-basics-infrastructure-as-code-arm-templates/), используемого для разных сред, в том числе для тестовой, промежуточной и рабочей. Диспетчер ресурсов обеспечивает безопасность, аудит и тегов toohelp возможности управления ресурсами после развертывания.

Развертываний на базе шаблона диспетчера ресурсов Azure для повышения безопасности hello решений для развертывания в Azure, так как стандартной безопасности, управления параметрами и может быть интегрирован в стандартизированном развертывания на основе шаблона. Это снижает риск hello ошибок конфигурации безопасности, которые могут происходить во время развертывания вручную.

### <a name="application-insights"></a>Application Insights
[Application Insights](https://docs.microsoft.com/azure/application-insights/) — это расширяемая служба управления производительностью приложений (APM) для веб-разработчиков. С помощью Application Insights можно отслеживать динамические веб-приложения и автоматически обнаруживать аномалии производительности. Он включает toohelp средств гибкой аналитической диагностировать проблемы и toounderstand, какие пользователи фактически выполняют вместе со своими приложениями. Он отслеживает все hello время ее работы, во время тестирования и после развертывания или публикации приложения.

Application Insights создает диаграммы и таблицы, которые показывают, например, какое время суток, вы получаете большинству пользователей является приложение hello отвечать на запросы, а также и контейнер, который обслуживается любого внешнего служб, он зависит.

В случае сбоев, ошибок или проблем с производительностью, можно выполнить поиск по данным телеметрии hello причина hello toodiagnose детализации. И службы hello отправит сообщения электронной почты, если были внесены изменения в hello доступность и производительность вашего приложения. Таким образом Application Insight становится средство ценные безопасности, так как он помогает обеспечивать доступность hello в hello конфиденциальность, целостность и доступность тройки безопасности.

### <a name="azure-monitor"></a>Azure Monitor
[Монитор Azure](https://docs.microsoft.com/azure/monitoring-and-diagnostics/) предлагает визуализации, запрос, маршрутизации, предупреждения, Автомасштабирование и автоматизации на обоих данных от hello инфраструктуры Azure ([журнал действий](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-activity-logs)) и каждый отдельный ресурс Azure ([ Журналы диагностики](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs)). Можно использовать монитор Azure tooalert на события, связанные с безопасностью, которые в журналы Azure.

### <a name="log-analytics"></a>Служба Log Analytics
[Аналитика журналов](https://azure.microsoft.com/documentation/services/log-analytics/) частью [Operations Management Suite](https://www.microsoft.com/cloud-platform/operations-management-suite) — предоставляет решение для управления ИТ для локальной и облачной инфраструктуры сторонних разработчиков (например, AWS) в дополнение к этому tooAzure ресурсов. Данные из монитора Azure могут быть направлены непосредственно tooLog Analytics, чтобы можно было видеть метрики и журналов для всей среды в одном месте.

Служба аналитики журналов может быть полезным инструментом аналитические и других видов анализа безопасности, hello позволяет tooquickly поиска больших объемов связанных с безопасностью операции с подходом гибкого запроса. Кроме того, локальные [журналы брандмауэра и прокси-сервера можно экспортировать в Azure для анализа с помощью Log Analytics.](https://docs.microsoft.com/azure/log-analytics/log-analytics-proxy-firewall)

### <a name="azure-advisor"></a>Azure Advisor
[Помощник по настройке ядра Azure](https://docs.microsoft.com/azure/advisor/) — консультант персонализированной облака, помогающая toooptimize развертыванием Azure. Он анализирует конфигурацию и данные телеметрии использования ресурсов. Затем он рекомендует решения toohelp улучшить hello [производительности](https://docs.microsoft.com/azure/advisor/advisor-performance-recommendations), [безопасности](https://docs.microsoft.com/azure/advisor/advisor-security-recommendations), и [высокий уровень доступности](https://docs.microsoft.com/azure/advisor/advisor-high-availability-recommendations) ресурсов при поиске возможных сделок слишком[уменьшить общую Azure тратить](https://docs.microsoft.com/azure/advisor/advisor-cost-recommendations). Помощник по Azure предоставляет рекомендации по безопасности, которые могут значительно повысить общий уровень безопасности решений, развертываемых в Azure. Эти рекомендации составляются на основе анализа безопасности, выполненного [центром безопасности Azure](https://docs.microsoft.com/azure/security-center/security-center-intro)

### <a name="azure-security-center"></a>Центр безопасности Azure
[Центр безопасности Azure](https://docs.microsoft.com/azure/security-center/security-center-intro) помогает предотвратить, обнаружить и вернуть toothreats Повышенная видимость и контроль над hello безопасность ресурсов Azure. Она включает встроенные функции мониторинга безопасности и управления политиками для подписок Azure, помогает выявлять угрозы, которые в противном случае могли бы оказаться незамеченными, и взаимодействует с широким комплексом решений по обеспечению безопасности.

Кроме того, центр безопасности Azure упрощает операции безопасности, обеспечивая единую панель мониторинга, содержащую оповещения и рекомендации, в соответствии с которыми можно предпринять немедленные действия. Часто можно устранять проблемы в консоли центра безопасности Azure hello одним щелчком.
## <a name="applications"></a>Приложения
Дополнительные сведения об основных функций в приложение безопасности и сводные сведения об этих возможностях Hello раздела.

### <a name="web-application-vulnerability-scanning"></a>Сканирование уязвимостей веб-приложений
Одним из простых способов tooget hello работы с проверка на наличие уязвимостей на ваш [приложением служб приложений](https://docs.microsoft.com/azure/app-service/app-service-value-prop-what-is) — toouse hello [интеграция с Tinfoil Security](https://azure.microsoft.com/blog/web-vulnerability-scanning-for-azure-app-service-powered-by-tinfoil-security/) уязвимость одним щелчком tooperform сканирование на приложение. Можно просматривать результаты теста hello в отчете легко понять и узнайте, как toofix Каждая уязвимость с пошаговыми инструкциями.

### <a name="penetration-testing"></a>Выполнение тестов на проникновение
Если вы предпочитаете tooperform собственные проникновения тестов или хотите toouse другой набор сканер или поставщика, следует выполнить hello [Azure преодоление процесс утверждения](https://security-forms.azure.com/penetration-testing/terms) и получить предварительное согласие tooperform hello требуемого проникновения тесты.

### <a name="web-application-firewall"></a>Брандмауэр веб-приложения
Hello брандмауэр веб-приложения (WAF) в [шлюза приложения Azure](https://azure.microsoft.com/services/application-gateway/) помогает защитить веб-приложений из распространенных веб-атак, например путем внедрения кода SQL, атак с использованием межсайтовых сценариев и перехват сеансов. Он поступает предварительно настроенные с защитой от угроз, обозначенную hello [открыть Web приложения безопасности проекта (OWASP) как hello top 10 распространенных уязвимостей](https://msdn.microsoft.com/library/).

### <a name="authentication-and-authorization-in-azure-app-service"></a>Проверка подлинности и авторизация в службе приложений Azure
[Проверка подлинности службы для приложения / авторизации](https://docs.microsoft.com/azure/app-service/app-service-authentication-overview) — это компонент, который предоставляет способ для вашего приложения toosign пользователей, чтобы не нужно toochange код на внутреннем сервере приложения hello. Он предоставляет простой способ tooprotect приложения и рабочие данные для каждого пользователя.

### <a name="layered-security-architecture"></a>Многоуровневая архитектура безопасности
[Среды службы приложений](https://docs.microsoft.com/azure/app-service-web/app-service-app-service-environment-intro) предоставляют изолированную среду выполнения, развернутую в [виртуальной сети Azure](https://docs.microsoft.com/azure/virtual-network/virtual-networks-overview). Поэтому разработчики могут создавать многоуровневую архитектуру безопасности, предусматривающую разные уровни доступа к сети для каждого уровня приложения. Общие желания toohide API назад интерфейсов из общего доступа к Интернету и только позволяет toobe API-интерфейсы, вызванных вышестоящего веб-приложений. [Сетевые группы безопасности (Nsg)](https://azure.microsoft.com/documentation/articles/virtual-networks-nsg/) может использоваться в подсети виртуальной сети Azure, содержащую приложения tooAPI общего доступа toorestrict среды службы приложения.

### <a name="web-server-diagnostics-and-application-diagnostics"></a>Диагностика веб-сервера и приложений
Веб-приложения служб приложений предоставляют диагностических функций для записи в журнал из hello веб-сервер и веб-приложения hello. Используется следующее логическое разделение: [диагностика веб-сервера](https://docs.microsoft.com/azure/app-service-web/web-sites-enable-diagnostic-log) и [диагностика приложений](https://technet.microsoft.com/library/hh530058(v=sc.12).aspx). Веб-серверы включают в себя два основных достижения в диагностике и устранении неполадок сайтов и приложений.

Hello первый новая возможность — состояние в реальном времени сведения о пулов приложений, рабочих процессов, сайты, домены приложений и запросы. Второй новый преимущества Hello hello события подробные трассировки, отслеживающие запроса в процессе hello завершения запросов и ответов.

Коллекция hello tooenable этих событий трассировки, IIS 7 можно журналы полной трассировки записи настроенные tooautomatically в формате XML, для любого конкретного запроса, основанного на времени или ответа коды ошибок.

#### <a name="web-server-diagnostics"></a>Диагностика веб-сервера
Можно включить или отключить hello следующие виды журналы:

-   Подробное ведение журнала ошибок — регистрация подробной информации об ошибке для кодов состояния HTTP, которые указывают на сбой (код состояния 400 и выше). Это может содержать сведения, которые могут помочь определить, почему hello сервер вернул код ошибки hello.

-   Трассировка сбоев запросов - подробные сведения о невыполненных запросов, включая трассировки запрос hello tooprocess компоненты, используемые IIS hello и hello время, затраченное в каждом компоненте. Это может быть полезно, если пытаетесь tooincrease производительность сайта или выявить причину вернул конкретных toobe ошибки HTTP.

-   Веб-сервера регистрации – сведения о транзакций HTTP с использованием расширенного формата файла журнала hello W3C. Это полезно при определении общей сайта метрик, таких как количество hello запросы обрабатываются или сколько запросы отправляются определенный IP-адрес.

#### <a name="application-diagnostics"></a>диагностика приложений
[Диагностика приложений](https://docs.microsoft.com/azure/app-service-web/web-sites-enable-diagnostic-log) позволяет toocapture данные, созданные веб-приложением. Приложения ASP.NET могут использовать hello [System.Diagnostics.Trace](https://msdn.microsoft.com/library/system.diagnostics.trace) консоли диагностики приложений toohello класса toolog сведения журнала. В консоли диагностики приложений существует два основных типа событий, связанных с ними tooapplication производительности и связанных с ними tooapplication сбоев и ошибок. Hello сбоев и ошибок можно разделить дальше в проблем с подключением, безопасностью и сбоями. Сбои, обычно связанные tooa проблема с кодом приложения hello.

В окне диагностики приложений можно просмотреть события, сгруппированные следующим образом:

-   "Все" (отображаются все события);
-   "Ошибки приложения" (отображаются события исключений);
-   "Производительность" (отображаются события производительности).

## <a name="storage"></a>Хранилище
Дополнительные сведения об основных функций в хранилище Azure безопасности и сводные сведения об этих возможностях Hello раздела.

### <a name="role-based-access-control-rbac"></a>Управление доступа на основе ролей
Вы можете защитить учетную запись хранения с помощью управления доступом на основе ролей (RBAC). Ограничение доступа на основании hello [требуется tooknow](https://en.wikipedia.org/wiki/Need_to_know) и [наименьших прав доступа](https://en.wikipedia.org/wiki/Principle_of_least_privilege) принципы безопасности важно для организаций, которые планируют tooenforce политики безопасности для доступа к данным. Эти права доступа предоставляются путем назначения hello соответствующие RBAC роли toogroups и приложения в определенной области. Можно использовать [встроенные роли RBAC](https://docs.microsoft.com/azure/active-directory/role-based-access-built-in-roles), например участника учетной записи хранилища, tooassign привилегии toousers. Доступ к разделам toohello хранилища для учетной записи хранилища с помощью hello [диспетчера ресурсов Azure](https://docs.microsoft.com/azure/storage/storage-security-guide) модели можно управлять через управление доступом на основе ролей (RBAC).

### <a name="shared-access-signature"></a>Подписанный URL-адрес
Объект [подписанного URL-адреса (SAS)](https://docs.microsoft.com/azure/storage/storage-dotnet-shared-access-signature-part-1) предоставляет tooresources делегированный доступ в вашей учетной записи хранилища. Hello SAS означает предоставить клиент ограниченную tooobjects разрешения вашей учетной записи хранилища для указанного периода и с указанным набором разрешений. Можно предоставить эти ограниченные разрешения без необходимости tooshare ключей доступа к учетной записи.

### <a name="encryption-in-transit"></a>Шифрование при передаче
Шифрование при передаче — это механизм защиты данных, передаваемых по сетям. Служба хранилища Azure позволяет применять для защиты данных:
-   [шифрование транспортного уровня](https://docs.microsoft.com/azure/storage/storage-security-guide#encryption-in-transit), например протокол HTTPS, при передаче данных в службу хранилища Azure или из нее;

-   [шифрование подключения](https://docs.microsoft.com/azure/storage/storage-security-guide#using-encryption-during-transit-with-azure-file-shares), например [шифрование SMB 3.0](https://docs.microsoft.com/azure/storage/storage-security-guide) для [общей папки Azure](https://docs.microsoft.com/azure/storage/storage-dotnet-how-to-use-files);

-   Шифрование на стороне клиента, tooencrypt hello данные до их передачи в хранилище и toodecrypt hello данных после передачи из хранилища.

### <a name="encryption-at-rest"></a>Шифрование при хранении
Для многих организаций шифрование неактивных данных является обязательным шагом для защиты данных, соблюдения стандартов и обеспечения конфиденциальности данных. В службе хранилища Azure есть три функции, обеспечивающие шифрование неактивных данных.

-   [Шифрование службы хранилища](https://docs.microsoft.com/azure/storage/storage-service-encryption) позволяет toorequest, что службы хранилища hello автоматически шифровать данные при записи tooAzure хранилища.

-   [Шифрование на стороне клиента](https://docs.microsoft.com/azure/storage/storage-client-side-encryption) также обеспечивает возможность hello шифрования при хранении.

-   [Azure шифрование диска](https://docs.microsoft.com/azure/security/azure-security-disk-encryption) позволяет tooencrypt hello ОС дисков и дисков данных, используемый виртуальной машиной IaaS.

### <a name="storage-analytics"></a>аналитики хранилища
[Azure Storage Analytics](https://docs.microsoft.com/rest/api/storageservices/fileservices/storage-analytics) ведет журнал и предоставляет данные метрик для учетной записи хранения. Можно использовать этот tootrace запросы данных, анализа тенденций использования и диагностики проблем с вашей учетной записи хранилища. Аналитика хранилища заносит в журнал подробные сведения о службе хранилища tooa успешных и неудачных запросах. Эти сведения можно использовать toomonitor отдельных запросов и toodiagnose проблем со службой хранилища. Запросы вносятся в журнал наилучшим возможным образом. регистрируются следующие типы запросов на проверку подлинности Hello:
-   успешные запросы;

-   неудачные запросы, в том числе из-за ошибок, связанных с временем ожидания, регулированием, сетью, авторизацией и др.;

-   запросы, в которых используется подписанный URL-адрес (SAS), в том числе неудачные и успешные запросы;

-   Данные tooanalytics запросов.

### <a name="enabling-browser-based-clients-using-cors"></a>Поддержка браузерных клиентов с помощью CORS
[Общий доступ к ресурсам независимо от источника (CORS)](https://docs.microsoft.com/rest/api/storageservices/fileservices/cross-origin-resource-sharing--cors--support-for-the-azure-storage-services) — это механизм, позволяющий домены toogive друг с другом разрешение для доступа к ресурсам друг друга. Hello агент пользователя отправляет дополнительные заголовки tooensure разрешенным hello кода JavaScript, загруженного из определенного домена tooaccess ресурсам, находящимся в другом домене. домен Hello отправляет в ответ дополнительные заголовки, разрешение или запрет hello исходного домена доступ tooits ресурсов.

Теперь поддерживают CORS службы хранилища Azure, таким образом, задав hello правил CORS для службы hello, прошедший проверку подлинности запроса к службе hello из другого домена вычисленное toodetermine ли это разрешено в соответствии с правилами toohello вами указано.
## <a name="networking"></a>Сеть
Дополнительные сведения о ключевых возможностях Azure сетевой безопасности и сводные сведения об этих возможностях Hello раздела.

### <a name="network-layer-controls"></a>Контроль сетевого уровня
Управление доступом к сети — операция hello ограничение tooand подключения от конкретных устройств и подсетей и представляет hello core безопасности сети. Задача Hello управления доступом к сети — toomake виртуальных машин и служб пользователей доступен tooonly и toowhich устройства необходимо разрешить им доступ.

#### <a name="network-security-groups"></a>группы сетевой безопасности;
Объект [группы безопасности сети (NSG)](https://docs.microsoft.com/azure/virtual-network/virtual-networks-nsg) основных пакетов с отслеживанием состояния, фильтрации брандмауэра и позволяет toocontrol доступ на основе [5-фрагментному](https://www.techopedia.com/definition/28190/5-tuple). Группы безопасности сети не обеспечивают проверку на прикладном уровне или механизмы контроля доступа с проверкой подлинности. Они могут использоваться трафика toocontrol перемещение между подсетями в виртуальной сети Azure и трафик между виртуальной сетью Azure и hello Интернета.

#### <a name="route-control-and-forced-tunneling"></a>Управление маршрутами и принудительное туннелирование
Hello возможность toocontrol поведения маршрутизации в виртуальных сетях Azure — возможность управления безопасностью и доступом критической. Например следует убедиться, что все tooand трафика из виртуальной сети Azure проходит этого безопасности виртуального устройства toomake требуется может toocontrol toobe и настройка поведения маршрутизации. Это можно сделать, настроив в Azure определяемые пользователем маршруты.

[Определяемые пользователем маршруты](https://docs.microsoft.com/azure/virtual-network/virtual-networks-udr-overview) позволяют toocustomize входящий и исходящий пути для трафика, переход в отдельных виртуальных машин или подсети tooinsure hello наиболее безопасный возможных маршрутов. [Принудительное туннелирование](https://www.petri.com/azure-forced-tunneling) является механизмом, можно использовать tooensure, служб, которые не являются допускается tooinitiate toodevices соединения на hello Интернет.

Это поведение отличается от может tooaccept входящих подключений и затем отвечает toothem. Интерфейсный веб-серверов требуется toorequests toorespond от Интернет-узлов, и не сможет ответить, точкой Интернет-трафика toothese входящего веб-серверов и hello веб-серверов.

Принудительное туннелирование — toogo Internet toohello часто используемые tooforce исходящего трафика через прокси-серверы в локальной безопасности и брандмауэры.

#### <a name="virtual-network-security-appliances"></a>Виртуальные устройства сетевой безопасности
Сетевые группы безопасности, определяемые пользователем маршруты и Принудительное туннелирование предоставляют вам уровень безопасности hello сети и транспорта уровнями hello [модели OSI](https://en.wikipedia.org/wiki/OSI_model), могут возникнуть ситуации, когда требуется tooenable безопасности на более высоких уровнях стек Hello. Воспользоваться этими улучшенными функциям сетевой безопасности можно с помощью устройства сетевой безопасности от партнера Azure. Hello можно найти самые последние решения по обеспечению безопасности сети Azure партнера, перейдя по адресу hello [Azure Marketplace](https://azure.microsoft.com/marketplace/) и поиск «безопасность» и «сетевая безопасность».

### <a name="azure-virtual-network"></a>Виртуальная сеть Azure

Azure виртуальной сети (VNet) — это представление сети в облаке hello. Это логический изоляции hello сети Azure fabric выделенного tooyour подписки. Кроме того, можно полностью настраивать hello блоки IP-адресов, параметры DNS, политики безопасности и таблицы маршрутов в этой сети. Кроме того, вы можете дополнительно разделить виртуальную сеть на подсети и запускать виртуальные машины Azure IaaS и (или) [облачные службы (экземпляры роли PaaS)](https://docs.microsoft.com/azure/cloud-services/cloud-services-choose-me) в виртуальных сетях Azure.

Кроме того, можно подключить hello виртуальной сети tooyour локальной сети с помощью одного из hello [варианты подключения](https://docs.microsoft.com/azure/vpn-gateway/) доступны в Azure. По сути вы можете развернуть tooAzure вашей сети, с полный контроль над блоки IP-адресов с преимуществами hello корпоративного уровня, предоставляемые Azure.

Сети Azure поддерживают различные сценарии безопасного удаленного доступа. Ниже перечислены некоторые из них.

-   [Подключение отдельных рабочих станциях tooan виртуальной сети Azure](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-howto-point-to-site-rm-ps)

-   [Подключение локальной сети tooan виртуальной сети Azure VPN-подключение](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-plan-design)

-   [Подключение локальной сети tooan виртуальной сети Azure с выделенную линию](https://docs.microsoft.com/azure/expressroute/expressroute-introduction)

-   [Подключения других виртуальных сетях Azure tooeach](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-vnet-vnet-rm-ps)

### <a name="vpn-gateway"></a>VPN-шлюз
toosend сетевой трафик между виртуальной сети Azure и локальным узлом, необходимо создать VPN-шлюза для виртуальной сети Azure. [VPN-шлюз](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-about-vpngateways) — это разновидность шлюза виртуальной сети, который отправляет зашифрованный трафик через общедоступное подключение. Также можно использовать VPN-шлюзы toosend трафика между виртуальными сетями Azure через hello структуры сети Azure.

### <a name="express-route"></a>ExpressRoute
Microsoft Azure [ExpressRoute](https://docs.microsoft.com/azure/expressroute/expressroute-introduction) является выделенную линию, позволяет расширять свои локальные сети в облако Microsoft hello по выделенному соединению закрытый добиться с помощью поставщика услуг подключения.

![ExpressRoute](./media/azure-security/azure-security-fig1.png)

При помощи ExpressRoute можно устанавливать подключения tooMicrosoft облачные службы, такие как Microsoft Azure, Office 365 и CRM Online. Это может быть подключение типа "любой к любому" (IP VPN), подключение Ethernet типа "точка-точка" или виртуальное кросс-подключение через поставщика услуг подключения на совместно используемом сервере.

Подключения ExpressRoute не выходят hello общедоступный Интернет и таким образом можно считать более безопасны, чем решения на основе VPN. Это позволяет toooffer подключения ExpressRoute дополнительные надежность, высокую скорость, меньшую задержку и большую безопасность по сравнению с обычными подключениями через Интернет hello.


### <a name="application-gateway"></a>Шлюз приложений
[Шлюз приложений Microsoft Azure](https://docs.microsoft.com/azure/application-gateway/application-gateway-introduction) предоставляет [контроллер доставки приложений (ADC)](https://en.wikipedia.org/wiki/Application_delivery_controller) как услугу, предлагая для приложения множество функций балансировки нагрузки уровня 7.

![Шлюз приложений](./media/azure-security/azure-security-fig2.png)

Можно toooptimize web фермы производительность за счет разгрузки toohello завершения служб с интенсивными вычислениями SSL для ЦП шлюза приложений (также называется «Разгрузка SSL» или «Мост SSL»). Он также предоставляет другие возможности маршрутизации уровня 7, включая циклическое распределение входящего трафика, сходство сеансов на основе файлов cookie, маршрутизация URL-адрес на основе пути и toohost возможность hello несколько веб-сайтов за один шлюз приложений. Шлюз приложений — это балансировщик нагрузки уровня 7.

Он обеспечивает отработку отказа, маршрутизации производительности HTTP-запросы между различными серверами, являются ли они на hello облачной или локальной.

Шлюз приложений выполняет многие функции контроллера доставки приложений (ADC), включая балансировку нагрузки HTTP, определение сходства сеансов на основе файлов cookie, разгрузку [SSL](https://docs.microsoft.com/azure/application-gateway/application-gateway-web-application-firewall-powershell), пользовательские пробы работоспособности, поддержку нескольких сайтов и т. д.

### <a name="web-application-firewall"></a>Брандмауэр веб-приложения
Брандмауэр веб-приложения — это функция [шлюза приложения Azure](https://docs.microsoft.com/azure/application-gateway/application-gateway-introduction) , обеспечивает защиту tooweb приложений, использующих шлюз приложений для стандартных функций управления доставки приложений (ADC). Брандмауэр веб-приложения выполняется путем защищая их от большинства hello OWASP top 10 распространенных web уязвимостей.

![Брандмауэр веб-приложения](./media/azure-security/azure-security-fig1.png)

-   Защита от внедрения кода SQL.

-   Защита от распространенных сетевых атак, в том числе от внедрения команд, несанкционированных HTTP-запросов, разделения HTTP-запросов и атак с включением удаленного файла.

-   Защита от нарушений протокола HTTP.

-   Защита от аномалий протокола HTTP, например отсутствия агента пользователя узла и заголовков accept.

-   Защита от программ-роботов, программ-обходчиков и сканеров.

-   Обнаружение распространенных неправильных конфигураций приложений (Apache, IIS и т. д.).


Tooprotect брандмауэра централизованного веб приложения от атак веб значительно упрощает управление безопасностью, а также лучше приложения toohello Software assurance от угроз hello объекта вторжения. Решение WAF также реагировать угрозу безопасности tooa быстрее путем применения исправлений известные уязвимости в центральном расположении и обеспечения безопасности каждого отдельного веб-приложений. Существующее приложение шлюзы можно легко преобразовать tooan шлюз приложений с брандмауэр веб-приложения.
### <a name="traffic-manager"></a>Диспетчер трафика
Microsoft [диспетчера трафика Azure](https://docs.microsoft.com/azure/traffic-manager/traffic-manager-overview) позволяет toocontrol hello распределением пользовательского трафика для конечных точек службы в разных центрах обработки данных. К конечным точкам службы, поддерживаемым диспетчером трафика Azure, относятся виртуальные машины, веб-приложения и облачные службы Azure. Можно также использовать диспетчер трафика Azure для внешних конечных точек, не относящихся к среде Azure. Диспетчер трафика использует hello доменных имен (DNS) toodirect клиент запрашивает toohello наиболее соответствующую конечную точку, на основе [метод маршрутизации трафика](https://docs.microsoft.com/azure/traffic-manager/traffic-manager-routing-methods) и работоспособности hello hello конечных точек.

Диспетчер трафика предоставляет широкий набор маршрутизации трафика методы toosuit требованиям приложений, исправности конечной точки [мониторинг](https://docs.microsoft.com/azure/traffic-manager/traffic-manager-monitoring)и автоматической отработки отказа. Диспетчер трафика является устойчивым toofailure, включая hello сбое всего региона Azure.
### <a name="azure-load-balancer"></a>Azure Load Balancer
[Подсистема балансировки нагрузки Azure](https://docs.microsoft.com/azure/load-balancer/load-balancer-overview) обеспечивает высокий уровень доступности и сетевой производительности tooyour приложений. Это балансировщик нагрузки уровня 4 (TCP, UDP), распределяющий входящий трафик между работоспособными экземплярами служб, определенных в наборе балансировки нагрузки. Вот какие функции можно настроить в службе Azure Load Balancer:

-   Балансировку нагрузки входящего Интернет трафика toovirtual машин. Такая конфигурация называется [балансировкой нагрузки для Интернета](https://docs.microsoft.com/azure/load-balancer/load-balancer-internet-overview).

-   Балансировка нагрузки трафика между виртуальными машинами в виртуальной сети, между виртуальными машинами в облачных службах или между локальными компьютерами и виртуальными машинами в распределенной виртуальной сети. Такая конфигурация называется [внутренней балансировкой нагрузки](https://docs.microsoft.com/azure/load-balancer/load-balancer-internal-overview). 

- Прямой внешнего трафика tooa отдельную виртуальную машину

### <a name="internal-dns"></a>Внутренняя служба DNS
Вы можете управлять hello список DNS-серверов, используемых в виртуальной сети в hello портала управления или в файл конфигурации сети hello. Клиент может сложить too12 DNS-серверов для каждой виртуальной сети. При указании DNS-серверы, это важно tooverify перечисляются клиента DNS-серверы в правильном порядке hello для среды клиента. Списки DNS-серверов не работают по принципу циклического перебора. Они используются, в котором они были указаны порядке hello. При возможности toobe достигнут hello первый DNS-сервер в список hello hello клиент использует этот DNS-сервер независимо от того, функционирует hello DNS-сервера неправильно или не. hello toochange порядок серверов DNS для виртуальной сети клиента, удалите hello DNS-серверы из списка hello и добавьте их обратно в порядке hello клиента хочет. Служба DNS поддерживает hello доступности аспектом тройки безопасности «CIA» hello.

### <a name="azure-dns"></a>Azure DNS
Hello [доменных имен](https://technet.microsoft.com/library/bb629410.aspx), или DNS, отвечает за преобразование (или разрешение) веб-сайта или службы имя tooits IP-адрес. [Azure DNS](https://docs.microsoft.com/azure/dns/dns-overview) является службой размещения для доменов DNS, предоставляющей разрешение имен с помощью инфраструктуры Microsoft Azure. При размещении ваших доменов в Azure, вы можете управлять DNS hello записей с помощью учетных данных, API-интерфейсы, средства и выставление счетов как других служб Azure. Служба DNS поддерживает hello доступности аспектом тройки безопасности «CIA» hello.
### <a name="log-analytics-nsgs"></a>Группы безопасности сети Log Analytics
Можно включить следующие категории журнала диагностики для Nsg hello:
-   Событие: Содержит записи, для какой NSG правила, примененных tooVMs и экземпляр роли, на основе MAC-адреса. Сбор сведений о состоянии Hello для этих правил каждые 60 секунд.

-   Счетчик правил: содержит записи для каждого правила NSG будет применен toodeny сколько раз или разрешить трафик.

### <a name="azure-security-center"></a>Центр безопасности Azure
Центр обеспечения безопасности помогает предотвратить, обнаружение и ответ toothreats и предоставляет вам увеличить видимость и контроль над, hello безопасность ресурсов Azure. Он содержит встроенные функции мониторинга безопасности и управления политиками для подписок Azure, помогает выявлять угрозы, которые в противном случае могли бы оказаться незамеченными, и взаимодействует с широким комплексом решений по обеспечению безопасности. Основное внимание в рекомендациях для сети уделено брандмауэрам, группам безопасности сети, настройке правил входящего трафика и другим аспектам.

Доступные рекомендации для сети представлены ниже.

-   [Добавление следующего поколения брандмауэр](https://docs.microsoft.com/azure/security-center/security-center-add-next-generation-firewall) рекомендует добавить брандмауэра следующего поколения (NGFW) от партнера Майкрософт tooincrease мер по обеспечению безопасности

-   [Направить трафик только через NGFW](https://docs.microsoft.com/azure/security-center/security-center-add-next-generation-firewall#route-traffic-through-ngfw-only) рекомендует настраивать сетевые правила безопасности группы (NSG), которые принудительно tooyour входящий трафик ВМ с помощью вашей NGFW.

-   [Включить группы безопасности сети для подсетей или виртуальных машин](https://docs.microsoft.com/azure/security-center/security-center-enable-network-security-groups). Рекомендует включить группы безопасности сети для подсетей или виртуальных машин.

-   [Ограничить доступ через конечную веб-точку](https://docs.microsoft.com/azure/security-center/security-center-restrict-access-through-internet-facing-endpoints). Рекомендует настроить правила входящего трафика для групп безопасности сети.


## <a name="compute"></a>Среда выполнения приложений

Дополнительные сведения об основных функций в этой области и сводные сведения об этих возможностях Hello раздела.

### <a name="antimalware--antivirus"></a>Антивредоносная программа и антивирусная программа
С помощью Azure IaaS можно использовать антивирусное программное обеспечение безопасности поставщиков, как Майкрософт, Symantec, Trend Micro, McAfee и Касперского tooprotect виртуальных машин с вредоносных файлов, программ для показа рекламы и других угроз. [Антивредоносная программа](https://docs.microsoft.com/azure/security/azure-security-antimalware) (Майкрософт) для облачных служб и виртуальных машин предоставляет защиту, которая помогает обнаруживать и устранять вирусы, шпионское ПО и другие вредоносные программы. Microsoft Antimalware предоставляет можно настроить оповещения, когда известен tooinstall попыток вредоносного или нежелательного программного обеспечения, сам или запуска на Azure систем. Антивредоносную программу (Майкрософт) можно также развертывать с помощью центра безопасности Azure.

### <a name="hardware-security-module"></a>Аппаратные модули безопасности.
Шифрование и проверка подлинности не повышения безопасности, если не защищены сами ключи hello. Можно упростить управление hello и безопасность критических секреты и ключей, сохранив их в [хранилище ключей Azure](https://docs.microsoft.com/azure/key-vault/key-vault-whatis). Хранилище ключей предоставляет toostore параметр hello ключи в оборудования безопасности сертифицированных tooFIPS модулей (HSM) 140-2 уровня 2 стандарты. Ваши ключи шифрования SQL Server для резервного копирования или [прозрачного шифрования данных](https://msdn.microsoft.com/library/bb934049.aspx) могут храниться в хранилище ключей вместе с любыми ключами или секретными кодами приложений. Разрешения и доступ к элементам toothese защищенных управляются с помощью [Azure Active Directory](https://azure.microsoft.com/documentation/services/active-directory/).

### <a name="virtual-machine-backup"></a>Резервное копирование виртуальной машины
[Служба архивации Azure](https://docs.microsoft.com/azure/backup/backup-introduction-to-azure-backup) — это решение, которое защищает данные приложений при нулевых капитальных вложениях и минимальных эксплуатационных затратах. Ошибки приложения может привести к повреждению данных, а человеческой ошибки могут вызвать ошибки в приложения, которое может привести к toosecurity проблем. Служба архивации Azure защитит виртуальные машины Windows и Linux.

### <a name="azure-site-recovery"></a>Azure Site Recovery
Важной частью вашей организации [бизнеса непрерывности и аварийного восстановления (BCDR)](https://docs.microsoft.com/azure/best-practices-availability-paired-regions) стратегией является нахождение способа выполнения tookeep корпоративных рабочих нагрузок и приложений, копирование и запуск спланированные незапланированных простоев. [Служба Azure Site Recovery](https://docs.microsoft.com/azure/site-recovery/site-recovery-overview) помогает координировать процессы репликации, отработки отказа и восстановления рабочих нагрузок и приложений. Кроме того, она обеспечивает доступность этих ресурсов в дополнительном расположении, когда основное выходит из строя.

### <a name="sql-vm-tde"></a>Прозрачное шифрование данных виртуальных машин SQL
Существует несколько функций шифрования SQL Server, например [прозрачное шифрование данных (TDE)](https://docs.microsoft.com/azure/virtual-machines/windows/sqlclassic/virtual-machines-windows-classic-ps-sql-keyvault) и шифрование на уровне столбцов (CLE). Эта форма шифрования требуется toomanage клиентов и хранилище hello криптографических ключей, используемого для шифрования.

Hello службы хранилища ключей Azure (AKV) — спроектированный tooimprove hello безопасности и управления из этих ключей в расположении высокой надежности и безопасности. Hello соединителя SQL Server позволяет SQL Server toouse эти ключи из хранилища ключей Azure.

При запуске SQL Server с локальных компьютеров существуют шагов, можно выполнить tooaccess хранилище ключей Azure с локального компьютера SQL Server. Однако для SQL Server в виртуальных машинах Azure, вы можете сэкономить время при помощи функции hello интеграция хранилища ключей Azure. С несколько tooenable командлеты Azure PowerShell эту функцию, можно автоматизировать hello хранилища ключей конфигурации, необходимые для tooaccess SQL виртуальной Машины.

### <a name="vm-disk-encryption"></a>Шифрование дисков виртуальных машин
[Шифрование дисков Azure](https://docs.microsoft.com/azure/security/azure-security-disk-encryption) — это новая функция, которая помогает шифровать диски виртуальных машин IaaS под управлением Windows и Linux. Он применяется функции отрасли стандартные hello BitLocker для Windows и DM Crypt hello шифрования тома tooprovide Linux для hello ОС и дисков данных hello. решение Hello интегрировано в хранилище ключей Azure toohelp управления и управление ключами шифрования диска hello и секретные данные в вашей подписке хранилища ключей. Hello решение также обеспечивает шифрование всех данных на диски виртуальной машины hello хранятся в службе хранилища Azure.

### <a name="virtual-networking"></a>Виртуальная сеть
Виртуальным машинам требуется осуществлять взаимодействие по сети. toosupport этого требования Azure требует toobe виртуальных машин подключен tooan виртуальной сети Azure. Виртуальная сеть Azure — это логическая конструкция, построена на базе hello структуры физической сети Azure. Каждая логическая [виртуальная сеть Azure](https://docs.microsoft.com/azure/virtual-network/virtual-networks-overview) изолирована от всех прочих виртуальных сетей Azure. Эта изоляция помогает убедиться, что сетевой трафик в развертываниях не доступен tooother Microsoft Azure вопросам.

### <a name="patch-updates"></a>Обновление исправлений
Исправление обновлений представляют Привет основу для поиска и устранения потенциальных проблем и упрощают процесс управления обновлениями программного обеспечения hello, как за счет сокращения числа hello обновлений программного обеспечения, которые необходимо развернуть в организации, так и путем увеличения вашего toomonitor возможности соответствие.

### <a name="security-policy-management-and-reporting"></a>Управление политикой безопасности и отчеты.
[Центр безопасности Azure](https://docs.microsoft.com/azure/security-center/security-center-intro) помогает предотвратить, обнаружение и ответ toothreats и предоставляет увеличить видимость и контролировать, безопасность hello ресурсам Azure. Он содержит встроенные функции мониторинга безопасности и управления политиками для подписок Azure, помогает выявлять угрозы, которые в противном случае могли бы оказаться незамеченными, и взаимодействует с широким комплексом решений по обеспечению безопасности.

### <a name="azure-security-center"></a>Центр безопасности Azure
Центр обеспечения безопасности помогает предотвратить, обнаружения и вернуть toothreats Повышенная видимость и контроль над безопасностью hello Azure ресурсов. Она включает встроенные функции мониторинга безопасности и управления политиками для подписок Azure, помогает выявлять угрозы, которые в противном случае могли бы оказаться незамеченными, и взаимодействует с широким комплексом решений по обеспечению безопасности.

## <a name="identify-and-access-management"></a>Управление удостоверениями и доступом

Защита систем, приложений и данных начинается со средств управления доступом на основе удостоверений. Hello удостоверениями и доступом функции управления, встроенные в Microsoft business продуктов и служб защиты вашей организации и личные сведения от несанкционированного доступа при делая доступных toolegitimate пользователей каждый раз, когда и где они им понадобятся.

### <a name="secure-identity"></a>Защита удостоверения
Корпорация Майкрософт использует несколько рекомендации по обеспечению безопасности и технологии в своих продуктов и служб toomanage удостоверений и доступа.
-   [Многофакторная проверка подлинности](https://azure.microsoft.com/services/multi-factor-authentication/) требует пользователей toouse несколько методов доступа в локальной среде и в облаке hello. Обеспечивается строгая проверка подлинности с рядом простых вариантов проверки, в то же время пользователям предлагается простой процесс входа в систему.

-   [Microsoft Authenticator](https://aka.ms/authenticator) предоставляет удобный пользовательский интерфейс Многофакторной идентификации, который работает с учетными записями Microsoft Azure Active Directory и учетными записями Майкрософт, а также поддерживает проверки с помощью нательных устройств и отпечатков пальцев.

-   [Принудительного применения политики паролей](https://azure.microsoft.com/documentation/articles/active-directory-passwords-policy/) увеличивается hello безопасности традиционных паролей, поскольку требования длину и сложность, принудительно периодической смены и блокировки учетных записей после неудачной проверки подлинности попыток.

-   [Аутентификация на основе маркера](https://azure.microsoft.com/documentation/articles/active-directory-authentication-scenarios/) позволяет выполнять аутентификацию через службы федерации Active Directory (AD FS) или сторонние системы безопасных маркеров.

-   [Управление доступом на основе ролей (RBAC)](https://azure.microsoft.com/documentation/articles/role-based-access-built-in-roles/) включает toogrant доступ по hello пользователю назначена роль, чтобы легко toogive пользователей только hello объем доступа они tooperform их рабочих обязанностей. Параметры RBAC можно настроить в соответствии с бизнес-моделью организации и допустимыми рисками.

-   [Интегрированное управление идентификаторов (гибридное удостоверение)](https://azure.microsoft.com/documentation/articles/active-directory-hybrid-identity-design-considerations-overview/) предоставляет toomaintain управление доступом пользователей между внутренней центрами обработки данных и облачной платформы, создание единого пользовательского удостоверения для проверки подлинности и авторизации tooall ресурсов.

### <a name="secure-apps-and-data"></a>Защита приложений и данных
[Azure Active Directory](https://azure.microsoft.com/services/active-directory/), комплексный удостоверениями и доступом Облачное решение для управления, помогает toodata безопасного доступа в приложениях на сайте и в облаке hello и упрощает управление hello пользователей и групп. Он объединяет основные службы каталогов, дополнительные Управление удостоверениями, безопасность и управление доступом к приложениям и упрощает управление на основе политики идентификаторов toobuild разработчики в свои приложения. tooenhance в Azure Active Directory, можно добавить платный возможности с помощью Azure Active Directory Basic Premium P1 и Premium P2 выпуски hello.

| Бесплатные или стандартные функции     | Функции уровня "Базовый"    |Функции уровня Premium P1 |Функции уровня Premium P2 | Присоединение к Azure Active Directory — только функции Windows 10|
| :------------- | :------------- |:------------- |:------------- |:------------- |
|   [Объекты каталога](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-editions#directory-objects), [пользователя или группы управления (Добавление, обновление и удаление) или на основе пользователя подготовки регистрацию устройств](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-editions#usergroup-management-addupdatedelete-user-based-provisioning-device-registration), [единый вход (SSO)](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-editions#single-sign-on-sso), [самообслуживания Изменение пароля для облачных пользователей](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-editions#self-service-password-change-for-cloud-users), [Connect (модуль синхронизации, который расширяет tooAzure каталогов в локальной среде Active Directory)](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-editions#connect-sync-engine-that-extends-on-premises-directories-to-azure-active-directory), [безопасности / отчеты об использовании](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-editions#securityusage-reports)       |     [Управление доступом и подготовка на основе групп](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-editions#group-based-access-managementprovisioning), [самостоятельный сброс паролей для облачных пользователей](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-editions#self-service-password-reset-for-cloud-users), [фирменная символика организации (настройка страниц входа в систему и панели доступа)](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-editions#company-branding-logon-pagesaccess-panel-customization), [прокси приложения](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-editions#application-proxy), [соглашение об уровне обслуживания 99,9 %](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-editions#sla-999). |  [Самостоятельное управление группами и приложениями, самостоятельное добавление приложений и динамические группы](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-editions#self-service-group), [самостоятельный сброс, изменение и разблокирование паролей с обратной записью в локальную среду](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-editions#self-service-password-resetchangeunlock-with-on-premises-write-back), [Многофакторная идентификация (в облаке и локальной среде (сервер MFA))](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-editions#multi-factor-authentication-cloud-and-on-premises-mfa-server), [клиентская лицензия MIM + сервер MIM](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-editions#mim-cal-mim-server), [Cloud App Discovery](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-editions#cloud-app-discovery), [Connect Health](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-editions#connect-health), [автоматическая смена паролей для учетных записей групп](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-editions#automatic-password-rollover-for-group-accounts).|     [Защита идентификации](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-identityprotection), [управление привилегированными пользователями](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-privileged-identity-management-configure).|    [Присоединение устройства tooAzure AD SSO рабочего стола Microsoft Passport для Azure AD, восстановления Bitlocker администратора](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-editions#join-a-device-to-azure-ad-desktop-sso-microsoft-passport-for-azure-ad-administrator-bitlocker-recovery), [MDM автоматической регистрации, восстановления Bitlocker самообслуживания, устройствам tooWindows 10 дополнительных локальных администраторов в Azure Соединения AD](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-editions#mdm-auto-enrollment)|


- [Обнаружение облачных приложений](https://docs.microsoft.com/azure/active-directory/active-directory-cloudappdiscovery-whatis) — это расширенная функция Azure Active Directory, позволяющая tooidentify облачных приложений, используемых сотрудниками hello в вашей организации.

- [Azure Active Directory Identity Protection](https://azure.microsoft.com/documentation/articles/active-directory-identityprotection/) — служба безопасности, которая использует Azure Active Directory аномалий обнаружения возможности tooprovide консолидированное представление сведений о событиях риска и потенциальных уязвимостей, которые могут повлиять на ваш удостоверения организации.

- [Azure доменных служб Active Directory](https://azure.microsoft.com/services/active-directory-ds/) позволяет toojoin виртуальных машинах Azure tooa домена без hello необходимы toodeploy контроллеры домена. Пользователи войти в toothese виртуальные машины, используя свои корпоративные учетные данные Active Directory и непрерывный доступ к ресурсам.

- [Azure Active Directory B2C](https://azure.microsoft.com/services/active-directory-b2c/) — это служба управления высокой надежности, глобальных идентификаторов потребительском приложениям, которые можно масштабировать toohundreds миллионов идентификаторов и интегрировать на различных мобильных и веб-платформы. Клиентам можно войти tooall приложений через настраиваемый взаимодействия, использовать существующие учетные записи социальных сетей, или можно создать новые учетные данные для автономного.

- [Azure Active Directory B2B совместной работы](https://aka.ms/aad-b2b-collaboration) является безопасной partner интеграции заметного связей между компаниями, включив партнерам tooaccess корпоративным приложениям и данным выборочно с помощью своей самоуправляемых удостоверения.

- [Azure Active Directory Join](https://azure.microsoft.com/documentation/articles/active-directory-azureadjoin-overview/) позволяет tooextend облачные возможности tooWindows 10 устройств для централизованного управления. Он дает возможность пользователям tooconnect toohello корпоративной или организации облака через Azure Active Directory и упрощает доступ tooapps и ресурсы.

- [Прокси приложения Azure Active Directory](https://azure.microsoft.com/documentation/articles/active-directory-application-proxy-get-started/) обеспечивает единый вход и безопасный удаленный доступ для веб-приложений, размещенных в локальной среде.

## <a name="next-steps"></a>Дальнейшие действия
- [Приступая к работе с безопасностью Microsoft Azure](https://docs.microsoft.com/azure/security/azure-security-getting-started)

Службы Azure и возможностях, которые можно использовать toohelp безопасности служб и данных в Azure

- [Центр безопасности Azure](https://azure.microsoft.com/services/security-center/)

Запретить, обнаружения и вернуть toothreats Повышенная видимость и контроль над безопасностью hello Azure ресурсов

- [Наблюдение за работоспособностью системы безопасности в Центре безопасности Azure](https://docs.microsoft.com/azure/security-center/security-center-monitoring)

Здравствуйте, возможности мониторинга в центр безопасности Azure toomonitor соответствия политикам.
