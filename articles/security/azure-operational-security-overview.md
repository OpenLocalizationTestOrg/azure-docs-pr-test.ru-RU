---
title: "Общие сведения о безопасности операций aaaAzure | Документы Microsoft"
description: "В этой статье Обзор hello Azure оперативной безопасности."
services: security
documentationcenter: na
author: unifycloud
manager: swadhwa
editor: tomsh
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/27/2017
ms.author: tomsh
ms.openlocfilehash: b91c7889660b32e4933c305007692bd6e1ded05f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-operational-security-overview"></a>Обзор операционной безопасности Azure
Azure оперативной безопасности ссылается toohello служб, элементы управления и toousers доступных компонентов для защиты своих данных, приложений и другие активы, в Microsoft Azure. [Azure оперативной безопасности](https://docs.microsoft.com/azure/security/azure-operational-security) платформа, которая включает в себя знаний hello полученные в результате широкий набор возможностей, которые являются уникальными tooMicrosoft, включая hello Microsoft Security Development Lifecycle (SDL), Microsoft Security hello Программа Response Center и глубокого осведомленность о угроз безопасности кибер hello.

В этой статье Azure оперативной Общие сведения о безопасности, основное внимание уделяется hello в следующих областях:

- Azure Operations Management Suite;
-   Центр безопасности Azure
-   Azure Monitor
-   Наблюдатель за сетями Azure;
-   аналитика службы хранилища Azure;
-   Azure Active Directory.

## <a name="azure-operations-management-suite"></a>Azure Operations Management Suite;
ИТ-отдел отвечает за управление инфраструктуры центров обработки данных, приложений и данных, включая hello стабильности и безопасности системы. Тем не менее получение аналитики безопасности между часто увеличение сложные ИТ-среды требуется организаций toocobble данные из нескольких систем безопасности и управления.

[Microsoft Operations Management Suite (OMS)](https://docs.microsoft.com/azure/operations-management-suite/operations-management-suite-overview) — это облачное решение корпорации Майкрософт для управления ИТ-средой, которое помогает управлять локальной и облачной инфраструктурой и защищать ее.

OMS является облачным решением по управлению ИТ-инфраструктурой со множеством возможностей, включая автоматизацию ИТ, обеспечение безопасности и соответствия требованиям, службу Log Analytics, архивацию и восстановление. Таким образом, он toomanage точной aid и защитить ИТ-инфраструктуру — на локальном компьютере и в облаке hello.

Hello основные функциональные возможности OMS предоставляется набор служб, работающих в Azure. Каждая служба предоставляет функции управления и сценарии управления tooachieve служб можно объединять. К ним относятся:

-   Служба Log Analytics
-   Автоматизация
-   Резервное копирование
-   Site Recovery

### <a name="log-analytics"></a>Служба Log Analytics
[Log Analytics](http://azure.microsoft.com/documentation/services/log-analytics) предоставляет службы мониторинга для OMS за счет сбора данных из управляемых ресурсов и помещения их в центральный репозиторий. Эти данные могут включать события, данные производительности или пользовательские данные, предоставленные с помощью hello API. После сбора данных hello доступен для предупреждения, анализа и экспорта. Этот метод позволяет tooconsolidate данные из различных источников, можно объединить данные из служб Azure с существующей локальной средой. Он также четко разделяет hello сбор данных hello hello, действий на этих данных, чтобы все действия, доступные tooall типов данных.

### <a name="automation"></a>Служба автоматизации
Microsoft [автоматизации Azure](https://docs.microsoft.com/azure/automation/automation-intro) предоставляет способ для пользователей tooautomate hello вручную, длительные, ошибкам и часто повторяющиеся задачи, которые обычно осуществляются в облачной и корпоративной среде. Он позволяет сэкономить время и повышает надежность hello обычные административные задачи и даже планирует их toobe автоматически выполняется через регулярные интервалы. Можно автоматизировать процессы, используя модули Runbook, или автоматизировать управление конфигурацией, используя службу настройки требуемого состояния (DSC).

### <a name="backup"></a>Резервное копирование
[Резервное копирование Azure](https://docs.microsoft.com/azure/backup/backup-introduction-to-azure-backup) — hello Azure службы на основе можно использовать tooback (или защита) и восстановления данных в облако Microsoft hello. Служба архивации Azure позволяет заменить существующее локальное или автономное решение для резервного копирования на надежное, безопасное и экономичное облачное решение. Служба архивации Azure предлагает несколько компонентов, загрузить и развернуть на соответствующий компьютер с hello server, или в облаке hello. компонент Hello или агент, который развертывается зависит от необходимых tooprotect. Все компоненты службы архивации Azure (независимо от того, защищаете данные локально или в облаке hello) может быть используется tooback копирование хранилище служб восстановления tooa данных в Azure. В разделе hello [таблицы Azure Backup компонентов](https://docs.microsoft.com/azure/backup/backup-introduction-to-azure-backup#which-azure-backup-components-should-i-use).

### <a name="site-recovery"></a>Site Recovery
[Azure Site Recovery](http://azure.microsoft.com/documentation/services/site-recovery) обеспечивает непрерывность бизнеса, управляя операциями репликации локальных виртуальных и физических машин tooAzure или tooa вторичного сайта. В случае недоступности основного сайта переключением toohello вторичного расположения, чтобы пользователи могут сохранить рабочий и обратно в том случае, если возврат систем tooworking. Интеллектуальное и эффективное обнаружение угроз.

## <a name="azure-active-directory"></a>Azure Active Directory
[Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-enable-sso-scenario) — это комплексное решение для идентификации как службы (IDaaS) корпорации Майкрософт, которое:

-   включает IAM как облачную службу;
-   обеспечивает централизованное управление доступом, единый вход (SSO) и формирование отчетов;
-   Поддерживает управление доступом интеграции для [тысяч приложений](https://azure.microsoft.com/marketplace/active-directory/) в галерее приложения hello, включая Salesforce, Google Apps, Box, Concur и многое другое.

Azure AD также включает полный набор [возможностей управления удостоверениями](https://docs.microsoft.com/azure/security/security-identity-management-overview#security-monitoring-alerts-and-machine-learning-based-reports), в том числе [Многофакторную Идентификацию](https://docs.microsoft.com/azure/multi-factor-authentication/multi-factor-authentication), [регистрацию устройств]( https://docs.microsoft.com/azure/active-directory/active-directory-device-registration-overview), [самостоятельное управление паролями](https://azure.microsoft.com/resources/videos/self-service-password-reset-azure-ad/), [самостоятельное управление группами](https://docs.microsoft.com/azure/active-directory/active-directory-passwords-update-your-own-password), [управление привилегированными учетными записями](https://docs.microsoft.com/azure/active-directory/active-directory-privileged-identity-management-configure), [управление доступом на основе ролей](https://docs.microsoft.com/azure/active-directory/role-based-access-control-what-is), [отслеживание использования приложений](https://docs.microsoft.com/azure/active-directory/connect-health/active-directory-aadconnect-health), [расширенный аудит](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-activity-audit-logs), [мониторинг безопасности и предупреждения](https://docs.microsoft.com/azure/operations-management-suite/oms-security-responding-alerts).

С Azure Active Directory, все приложения публикации для ваших партнеров и клиентов (business или потребителя) имеется hello такие же возможности управления удостоверениями и доступом. Это позволяет вам toosignificantly сократить эксплуатационные затраты.

## <a name="azure-security-center"></a>Центр безопасности Azure
[Центр безопасности Azure](https://docs.microsoft.com/azure/security-center/security-center-get-started) помогает предотвратить, обнаружить и вернуть toothreats Повышенная видимость и контроль над hello безопасность ресурсов Azure. Он включает встроенные функции мониторинга безопасности и управления политиками для подписок, помогает выявлять угрозы, которые в противном случае могли бы оказаться незамеченными, и взаимодействует с широким комплексом решений по обеспечению безопасности.

[Центр безопасности](https://docs.microsoft.com/azure/security-center/security-center-linux-virtual-machine) помогает защитить данные виртуальных машин в Azure, обеспечивая представление параметров безопасности и отслеживание угроз. Центр безопасности может отслеживать виртуальные машины для обеспечения следующего:

-   Параметры безопасности операционной системы (ОС) с hello рекомендуемые правила конфигурации
-   Своевременная установка отсутствующих обновлений системы безопасности и критических обновлений.
-   Рекомендации по защите конечных точек.
-   Проверка шифрования диска.
-   Сетевые атаки

Центр безопасности Azure использует [управление доступом на основе ролей (RBAC)](https://docs.microsoft.com/azure/active-directory/role-based-access-control-configure), который предоставляет [встроенных ролей](https://docs.microsoft.com/azure/active-directory/role-based-access-built-in-roles) , можно назначить toousers, групп и служб в Azure.

Центр обеспечения безопасности оценивает конфигурацию hello проблемы безопасности tooidentify ресурсы и уязвимости. В центре безопасности отображается только сведения о связанных ресурсов tooa при назначении роли hello владельца, участника или чтения для hello подписка или группа ресурсов, к которому принадлежит ресурс.

>[!Note]
>В разделе [разрешений в центр безопасности Azure](https://docs.microsoft.com/azure/security-center/security-center-permissions) toolearn Дополнительные сведения о ролях и разрешенные действия в центре безопасности.

Центр обеспечения безопасности использует hello Microsoft Monitoring Agent — это же агент используется службой Operations Management Suite и анализа журналов hello hello. Данные, собранные от этого агента хранится в существующей службе анализа журналов [рабочей](https://docs.microsoft.com/azure/log-analytics/log-analytics-manage-access) связанный с вашей подпиской Azure или новых рабочих областей, учитывая geolocation hello учетной записи из hello виртуальной Машины.

## <a name="azure-monitor"></a>Azure Monitor
Проблемы с производительностью в облачном приложении могут повлиять на работу вашей компании. Несколько взаимосвязанных компонентов и частые выпуски могут в любое время привести к снижению производительности. В разработанном приложении пользователи, как правило, находят проблемы, которые не были обнаружены во время тестирования. Следует немедленно узнать об этих проблемах и средства для диагностики и устранения проблем hello.

[Azure Monitor](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-azure-monitor) — это основное средство для отслеживания служб, выполняемых в Azure. Он предоставляет уровня инфраструктуры данные о пропускной способности hello службы и hello окружающей среды. Если вы управляете приложений в Azure, выбор ли tooscale вверх или вниз ресурсы, затем монитора Azure позволяет вам использовать toostart.

Кроме того можно использовать мониторинга данных toogain полное представление о своем приложении. Эти знания можно помочь tooimprove производительность приложения и удобства поддержки или автоматизации действий, которые в противном случае требуют вмешательства. Сюда входят:

-   Журнал действий Azure
-   Журналы диагностики Azure
-   Метрики
-   Диагностика Azure

### <a name="azure-activity-log"></a>Журнал действий Azure
Это журнал, который позволяет контролировать hello операций, которые были выполнены на ресурсы в вашей подписке. Hello [журнал действий](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-activity-logs) ранее была известна как «Журналы аудита» или «Операционные журналы», так как отчеты события плоскости управления для ваших подписок.

### <a name="azure-diagnostic-logs"></a>Журналы диагностики Azure
[Журналы Azure диагностики](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs) создаваемых ресурса и предоставляет широкие возможности, часто данные об операции hello этого ресурса. Hello содержимое этих журналов зависит от типа ресурса.

Например, системные журналы событий Windows — это одна из категорий журналов диагностики для виртуальных машин, а журналы больших двоичных объектов, таблиц и очередей — категории журналов диагностики для учетных записей хранения.

Журналы диагностики отличаются от hello [журнал действий (прежнее название — журнал аудита или Операционный журнал)](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-activity-logs). журнал действий Hello позволяет контролировать hello операций, которые были выполнены на ресурсы в вашей подписке. Журналы диагностики дают представление об операциях, выполняемых самим ресурсом.

### <a name="metrics"></a>Метрики
Монитор Azure обеспечивает tooconsume телеметрии toogain видимость hello производительности и работоспособности рабочих нагрузок в Azure. наиболее важные тип Hello данные телеметрии Azure — метрики hello (также называемые счетчики производительности), генерируемой ресурсы наиболее Azure. Монитор Azure предоставляет несколько способов tooconfigure и использовать эти [метрики](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-metrics) для мониторинга и устранения неполадок.

### <a name="azure-diagnostics"></a>Диагностика Azure
Это возможность hello в Azure, которая включает hello сбор диагностических данных с развернутым приложением. Можно использовать расширения диагностики hello из различных источников в другой. В настоящее время поддерживаются [веб-роли и рабочие роли облачной службы Azure](https://docs.microsoft.com/azure/vs-azure-tools-configure-roles-for-cloud-service), [виртуальные машины Azure](https://docs.microsoft.com/azure/vs-azure-tools-configure-roles-for-cloud-service) под управлением Microsoft Windows и [Service Fabric](https://docs.microsoft.com/azure/monitoring-and-diagnostics/azure-diagnostics).


## <a name="network-watcher"></a>Наблюдатель за сетями
Клиенты создают комплексную сеть в Azure, администрируя и сочетая различные отдельные сетевые ресурсы, в том числе виртуальные сети, каналы ExpressRoute, шлюзы приложений, подсистемы балансировки нагрузки и многое другое. Наблюдение за доступно на каждом hello сетевых ресурсов.

Hello tooend сеть может иметь сложные конфигурации и взаимодействия между ресурсами, создание в сложных сценариях, требующих сценариям отслеживания с помощью Наблюдатель сети.

[Наблюдатель за сетями](https://docs.microsoft.com/azure/network-watcher/network-watcher-monitoring-overview) упростит мониторинг и диагностику сети Azure. Средств диагностики и визуализации, доступных с помощью значения enable Наблюдатель сети, которые вы tootake удаленный пакет записывает на виртуальную машину Azure, анализировать использование журналов поток сетевого трафика и диагностики шлюза VPN и подключений.

Наблюдатель сети в настоящее время имеет hello следующие возможности:

- [Топология](https://docs.microsoft.com/azure/network-watcher/network-watcher-topology-overview) -предоставляет hello отображение представление уровня сети различных взаимосвязями и ассоциации между сетевым ресурсам в группе ресурсов.
-   [Изменяемая запись пакетов](https://docs.microsoft.com/azure/network-watcher/network-watcher-packet-capture-overview). Позволяет записывать входящие и исходящие пакеты данных для виртуальной машины. Расширенные параметры фильтра и тонкой настройки элементов управления, например, время будет tooset и ограничений на размер обеспечивают гибкость. Hello пакетов данные могут храниться в хранилище BLOB-объектов или на локальном диске hello в формате .cap.
-   [Проверка IP-потока](https://docs.microsoft.com/azure/network-watcher/network-watcher-ip-flow-verify-overview). Позволяет проверить, разрешен или запрещен пакет, на основе информации о пакете, указанной в пяти кортежах (конечный IP-адрес, исходный IP-адрес, конечный порт, исходный порт и протокол). Если пакет приветствия запрещен группой безопасности, hello правил и групп, которым отказано в пакет приветствия возвращается.
-   [Следующий прыжок](https://docs.microsoft.com/azure/network-watcher/network-watcher-next-hop-overview) -определяет hello следующего прыжка для пакетов, направляется в сетевой инфраструктуре Azure, позволяя toodiagnose любое неправильно настроенных определяемых пользователем маршрутов hello.
-   [Представление "Группа безопасности"](https://docs.microsoft.com/azure/network-watcher/network-watcher-security-group-view-overview) -возвращает hello безопасности эффективный и примененные правила, которые применяются на виртуальной Машине.
-   [Ведение журнала потока NSG](https://docs.microsoft.com/azure/network-watcher/network-watcher-nsg-flow-logging-overview) -журналы потока для групп безопасности сети включить связанные tootraffic журналы toocapture, разрешенных или запрещенных правилами безопасности hello в группе hello. Hello потока определяется 5-фрагментному сведения — исходный IP-адрес, конечный IP-адрес, порт источника, конечный порт и протокол.
-   [Шлюз виртуальной сети и устранение неполадок при подключении](https://docs.microsoft.com/azure/network-watcher/network-watcher-troubleshoot-manage-rest) -предоставляет возможность tootroubleshoot hello шлюзах виртуальной сети и подключения.
-   [Сетевые ограничения подписки](https://docs.microsoft.com/azure/network-watcher/network-watcher-monitoring-overview) -позволяет tooview использование ресурсов сети с ограничениями.
-   [Настройка журнала диагностики](https://docs.microsoft.com/azure/network-watcher/network-watcher-monitoring-overview) — предоставляет tooenable одну область, или отключите журналы диагностики сетевых ресурсов в группе ресурсов.

более tooconfigure Наблюдатель сети в статье, toolearn [Настройка Наблюдатель сети](https://docs.microsoft.com/azure/network-watcher/network-watcher-create).

## <a name="developer-operations-devops"></a>Операции разработки (DevOps)
Предыдущий tooDevOps разработки приложений, команды были сбора бизнес-требований программы и написания кода. Отдельная группа QA тестируется программа hello в изолированной среде разработки, если требованиям и выпусках hello код для toodeploy операций. Hello группы развертывания также зависят бессистемного группам, как сетевая поддержка и базы данных. Каждый раз, программное обеспечение» возникает по часам hello» tooan независимых команды, он добавляет узких мест.

[DevOps](https://www.visualstudio.com/learn/what-is-devops/) позволяет командам toodeliver более безопасные более высокого качества решения быстрее и дешевле. Клиенты ожидают динамическое и надежное взаимодействие с программным обеспечением и службами.  Команды необходимо быстро выполнять итерацию обновлений программного обеспечения, оценки влияния обновления hello hello и быстро реагировать с новых проблем tooaddress итераций разработки или обеспечить дополнительные преимущества.  Такие облачные платформы, как Microsoft Azure, лишены традиционных узких мест и помогают упростить инфраструктуру. Программное обеспечение безраздельно в любого бизнеса как hello ключевые преимущества и коэффициент результатов бизнеса. Не организации, developer или ИТ-worker можно или следует избегать перемещения DevOps hello.

Для старшего DevOps специалисты принимают несколько hello, следуя рекомендациям. Эти методы [задействован человек](https://www.visualstudio.com/learn/what-is-devops-culture/) стратегии tooform основании hello бизнес-сценариев.  Инструментарий может помочь автоматизировать hello различные рекомендации:

-   [Agile планирование и управление проектами](https://www.visualstudio.com/learn/what-is-agile/) методы, используемые tooplan и изолировать работы по спринтам, управлять производительности команды и помогают командам быстро применить toochanging бизнес-требованиями.
-   [Управление версиями, обычно с Git](https://www.visualstudio.com/learn/what-is-git/), позволяет командам, расположенных в источнике tooshare hello world и интегрировать программного средства разработки tooautomate hello выпуска конвейера.
-   [Непрерывная интеграция](https://www.visualstudio.com/learn/what-is-continuous-integration/) дисков hello текущее слияние и тестирование кода, который раньше ведет toofinding дефектов.  Еще одно ее преимущество — затрачивается меньше времени на борьбу с проблемами слияния и обеспечивается быстрая обратная связь с командами разработчиков.
-   [Непрерывной поставки](https://www.visualstudio.com/learn/what-is-continuous-delivery/) программных средств tooproduction среды и тестирования организаций, помогающее быстро исправить ошибки и реагировать на изменение tooever бизнеса требования.
-   [Мониторинг](https://www.visualstudio.com/learn/what-is-monitoring/) позволяет отслеживать работоспособность запущенных приложений, включая рабочую среду, а также данные об их использовании клиентами. Это поможет организациям формировать гипотезы и быстро подтверждать или опровергать разработанные стратегии.  Подробные данные собираются и хранятся в различных форматах ведения журнала.
-   [Инфраструктура как код (IaC)](https://www.visualstudio.com/learn/what-is-infrastructure-as-code/) подход, который позволяет hello automation и проверки создания и удаления из сети и виртуальные машины toohelp с реализацией безопасную и надежную размещения платформы приложений.
-   [Микрослужбами](https://www.visualstudio.com/learn/what-are-microservices/) архитектура является tooisolate использовать варианты использования бизнеса в небольших для повторного использования службы.  Эта архитектура обеспечивает масштабируемость и эффективность.

## <a name="next-steps"></a>Дальнейшие действия
toolearn Дополнительные сведения о безопасности OMS и решения аудита, см. следующие статьи hello:

- [Operations Management Suite | Безопасность и соответствие требованиям](https://www.microsoft.com/cloud-platform/security-and-compliance)
- [TooSecurity мониторинга и отвечает на запросы предупреждения в Operations Management Suite безопасности и аудита решение](https://docs.microsoft.com/en-us/azure/operations-management-suite/oms-security-responding-alerts).
- [Мониторинг ресурсов в решении "Безопасность и аудит" Operations Management Suite](https://docs.microsoft.com/en-us/azure/operations-management-suite/oms-security-monitoring-resources)
