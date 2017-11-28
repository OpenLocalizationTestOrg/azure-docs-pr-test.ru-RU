# [Документация по Service Fabric](/azure/service-fabric)
# Обзор
## [Что такое Service Fabric?](service-fabric-overview.md)

# Быстрое начало работы
## [Создание приложения .NET](service-fabric-quickstart-dotnet.md)

# Учебники
## Развертывание приложения .NET
### [1. Сборка приложения .NET](service-fabric-tutorial-create-dotnet-app.md)
### [2 — развертывание приложения hello](service-fabric-tutorial-deploy-app-to-party-cluster.md)
### [3. Настройка непрерывной интеграции и доставки](service-fabric-tutorial-deploy-app-with-cicd-vsts.md)

## Репликация приложения по методике lift-and-shift
### [1. Создание защищенного кластера в Azure](service-fabric-tutorial-create-cluster-azure-ps.md)
### [2. Развертывание приложения .NET с помощью Docker Compose](service-fabric-host-app-in-a-container.md)

# Примеры
## [Примеры кода](https://azure.microsoft.com/en-us/resources/samples/?service=service-fabric)
## [PowerShell](service-fabric-powershell-samples.md)
## [Интерфейс командной строки Service Fabric](samples-cli.md)
### [Развертывание образца](scripts/cli-deploy-application.md)
### [Удаление образца](scripts/cli-remove-application.md)
# Основные понятия
## [Основные сведения о микрослужбах](service-fabric-overview-microservices.md)
## [Общая картина](service-fabric-content-roadmap.md)
## [Сценарии приложений](service-fabric-application-scenarios.md)
## [Примеры и сценарии](service-fabric-patterns-and-scenarios.md)
## [Архитектура](service-fabric-architecture.md)
## [Терминология](service-fabric-technical-overview.md)

## Создание приложений и служб
### Поддерживаемые модели программирования
#### [Обзор](service-fabric-choose-framework.md)
#### Контейнеры
##### [Обзор](service-fabric-containers-overview.md)
##### [Docker Compose (предварительная версия)](service-fabric-docker-compose.md)
##### [Управление ресурсами](service-fabric-resource-governance.md)
#### Надежные службы
##### [Обзор](service-fabric-reliable-services-introduction.md)
##### [Жизненный цикл Reliable Services (C#)](service-fabric-reliable-services-lifecycle.md)
##### [Жизненный цикл Reliable Services (Java)](service-fabric-reliable-services-lifecycle-java.md)
##### [Надежные коллекции](service-fabric-reliable-services-reliable-collections.md)
##### [Reliable Collections: инструкции и рекомендации](service-fabric-reliable-services-reliable-collections-guidelines.md)
##### [Работа с Reliable Collections](service-fabric-work-with-reliable-collections.md)
##### [Транзакции и блокировки](service-fabric-reliable-services-reliable-collections-transactions-locks.md)
##### [Надежная параллельная очередь](service-fabric-reliable-services-reliable-concurrent-queue.md)
##### [Сериализация надежной коллекции](service-fabric-reliable-services-reliable-collections-serialization.md)
##### [Внутренние компоненты Reliable State Manager и Reliable Collections](service-fabric-reliable-services-reliable-collections-internals.md)
##### [Расширенное использование](service-fabric-reliable-services-advanced-usage.md)

#### Надежные субъекты
##### [Обзор](service-fabric-reliable-actors-introduction.md)
##### [Архитектура](service-fabric-reliable-actors-platform.md)
##### [Жизненный цикл и сборка мусора](service-fabric-reliable-actors-lifecycle.md)
##### [Управление данными о состоянии](service-fabric-reliable-actors-state-management.md)
##### [Полиморфизм](service-fabric-reliable-actors-polymorphism.md)
##### [Повторный вход](service-fabric-reliable-actors-reentrancy.md)
##### [Сериализация типа](service-fabric-reliable-actors-notes-on-actor-type-serialization.md)

### [Модель приложения](service-fabric-application-model.md)
### [Модель размещения](service-fabric-hosting-model.md)

### Службы
#### [Ресурсы службы](service-fabric-service-manifest-resources.md)
#### [Состояние службы](service-fabric-concepts-state.md)
#### [Секционирование службы](service-fabric-concepts-partitioning.md)
#### [Доступность служб](service-fabric-availability-services.md)
#### Взаимодействие служб
##### [Обзор](service-fabric-connect-and-communicate-with-services.md)
##### [Служба DNS](service-fabric-dnsservice.md)
##### [Обратный прокси-сервер](service-fabric-reverseproxy.md)
##### [Настройка обратного прокси-сервера для безопасного подключения](service-fabric-reverseproxy-configure-secure-communication.md)
##### [Диагностика обратного прокси-сервера](service-fabric-reverse-proxy-diagnostics.md)
### [Масштабируемость приложений](service-fabric-concepts-scalability.md)
### [ASP.NET Core](service-fabric-reliable-services-communication-aspnetcore.md)

### [Планирование емкости приложения](service-fabric-capacity-planning.md)

## Управление приложениями
### [Обзор](service-fabric-application-lifecycle.md)
### [Строка ImageStoreConnectionString приветствия](service-fabric-image-store-connection-string.md)
### Обновление приложения
#### [Обзор](service-fabric-application-upgrade.md)
#### [Конфигурация](service-fabric-visualstudio-configure-upgrade.md)
#### [Параметры обновления приложений](service-fabric-application-upgrade-parameters.md)
#### [Сериализация данных при обновлении приложения](service-fabric-application-upgrade-data-serialization.md)
#### [Обновление приложения: более сложные темы](service-fabric-application-upgrade-advanced.md)
### [Обзор анализа ошибок](service-fabric-testability-overview.md)

## Создание кластеров и управление ими
### [Обзор](service-fabric-deploy-anywhere.md)
### [Service Fabric в Linux](service-fabric-linux-overview.md)
### Планирование и подготовка
#### [Планирование ресурсов](service-fabric-cluster-capacity.md)
#### [Аварийное восстановление](service-fabric-disaster-recovery.md)
### [Описание кластера](service-fabric-cluster-resource-manager-cluster-description.md)
### [Безопасность кластера](service-fabric-cluster-security.md)
### [Различия между функциями Linux и Windows](service-fabric-linux-windows-differences.md)
### Кластеры в Azure
#### [Виды узлов и масштабируемые наборы ВМ](service-fabric-cluster-nodetypes.md)
#### [Шаблоны сети кластера](service-fabric-patterns-networking.md)
### Диспетчер кластерных ресурсов
#### [Обзор](service-fabric-cluster-resource-manager-introduction.md)
#### [Архитектура](service-fabric-cluster-resource-manager-architecture.md)
#### [Описание кластера](service-fabric-cluster-resource-manager-cluster-description.md)
#### [Обзор групп приложений](service-fabric-cluster-resource-manager-application-groups.md)
#### [Настройка параметров диспетчера кластерных ресурсов](service-fabric-cluster-resource-manager-configure-services.md)
#### [Метрики потребления ресурсов](service-fabric-cluster-resource-manager-metrics.md)
#### [Использование сходства служб](service-fabric-cluster-resource-manager-advanced-placement-rules-affinity.md)
#### [Политики размещения служб](service-fabric-cluster-resource-manager-advanced-placement-rules-placement-policies.md)
#### [Управление кластером](service-fabric-cluster-resource-manager-management-integration.md)
#### [Дефрагментация кластера](service-fabric-cluster-resource-manager-defragmentation-metrics.md)
#### [Балансировка кластера](service-fabric-cluster-resource-manager-balancing.md)
#### [Регулирование](service-fabric-cluster-resource-manager-advanced-throttling.md)
#### [Перемещение служб](service-fabric-cluster-resource-manager-movement-cost.md)

## Мониторинг и диагностика
### [Обзор](service-fabric-diagnostics-overview.md)
### [Модель обеспечения работоспособности](service-fabric-health-introduction.md)
### [Диагностика в Reliable Services с отслеживанием состояния](service-fabric-reliable-services-diagnostics.md)
### [Диагностика в Reliable Actors](service-fabric-reliable-actors-diagnostics.md)

# Как tooGuides
## Настройка среды разработки
### [Windows](service-fabric-get-started.md)
### [Linux](service-fabric-get-started-linux.md)
### [Mac OS](service-fabric-get-started-mac.md)

## Создание приложения
### Создание гостевой исполняемой службы
#### [Размещение приложения Node.js в Windows](quickstart-guest-app.md)
#### [Развертывание гостевого исполняемого файла](service-fabric-deploy-existing-app.md)
#### [Развертывание нескольких пользовательских приложений](service-fabric-deploy-multiple-apps.md)
### Создание службы контейнеров
#### [Создание приложения-контейнера Windows](service-fabric-get-started-containers.md)
#### [Создание приложения-контейнера Linux](service-fabric-get-started-containers-linux.md)
#### [Безопасность контейнеров](service-fabric-securing-containers.md)
#### [Docker Compose (предварительная версия)](service-fabric-docker-compose.md)
#### [Управление ресурсами для контейнеров и служб](service-fabric-resource-governance.md)
#### [Драйверы томов и драйверы ведения журналов](service-fabric-containers-volume-logging-drivers.md)
#### [Службы в контейнерах](service-fabric-services-inside-containers.md)
#### [Cетевые режимы контейнеров](service-fabric-networking-modes.md)

### Создание службы Reliable Services
#### [Обзор](service-fabric-reliable-services-introduction.md)
#### Основные понятия
##### [Жизненный цикл Reliable Services (C#)](service-fabric-reliable-services-lifecycle.md)
##### [Жизненный цикл Reliable Services (Java)](service-fabric-reliable-services-lifecycle-java.md)

#### Reliable Collections
##### [Надежные коллекции](service-fabric-reliable-services-reliable-collections.md)
##### [Reliable Collections: инструкции и рекомендации](service-fabric-reliable-services-reliable-collections-guidelines.md)
##### [Работа с Reliable Collections](service-fabric-work-with-reliable-collections.md)
##### [Транзакции и блокировки](service-fabric-reliable-services-reliable-collections-transactions-locks.md)
##### [Надежная параллельная очередь](service-fabric-reliable-services-reliable-concurrent-queue.md)
##### [Сериализация надежной коллекции](service-fabric-reliable-services-reliable-collections-serialization.md)
##### [Внутренние компоненты Reliable State Manager и Reliable Collections](service-fabric-reliable-services-reliable-collections-internals.md)

#### Начало работы
##### [C# в Windows](service-fabric-reliable-services-quick-start.md)
##### [Java в Linux](service-fabric-reliable-services-quick-start-java.md)
##### [Создание приложения C# в Linux](service-fabric-create-your-first-linux-application-with-csharp.md)
#### Обмен данными со службами
##### [Обмен данными с помощью Reliable Services](service-fabric-reliable-services-communication.md)

##### [Удаленное взаимодействие со службой (C#)](service-fabric-reliable-services-communication-remoting.md)
##### [Удаленное взаимодействие со службой (Java)](service-fabric-reliable-services-communication-remoting-java.md)
##### [WCF](service-fabric-reliable-services-communication-wcf.md)
##### [Безопасные подключения — C#](service-fabric-reliable-services-secure-communication.md)
##### [Безопасные подключения — Java](service-fabric-reliable-services-secure-communication-java.md)

#### [Настройка](service-fabric-reliable-services-configuration.md)
#### [Отправка уведомлений](service-fabric-reliable-services-notifications.md)
#### [Резервное копирование и восстановление](service-fabric-reliable-services-backup-restore.md)

### Создание службы Reliable Actors
#### Начало работы
##### [C# в Windows](service-fabric-reliable-actors-get-started.md)
##### [Java в Linux](service-fabric-reliable-actors-get-started-java.md)
##### [Субъект Java в Linux](service-fabric-create-your-first-linux-application-with-java.md)
#### [Отправка уведомлений](service-fabric-reliable-actors-events.md)
#### [Настройка таймеров и напоминаний](service-fabric-reliable-actors-timers-reminders.md)
#### [Настройка KvsActorStateProvider](service-fabric-reliable-actors-kvsactorstateprovider-configuration.md)
#### [Настройка параметров подключения](service-fabric-reliable-actors-fabrictransportsettings.md)
#### [Настройка ReliableDictionaryActorStateProvider](service-fabric-reliable-actors-reliabledictionarystateprovider-configuration.md)

### [Перенос старое приложение Java toosupport Maven](service-fabric-migrate-old-javaapp-to-use-maven.md)

### [Настройка обратного прокси-сервера для безопасного подключения](service-fabric-reverseproxy-configure-secure-communication.md)

### [Создание службы ASP.NET Core](service-fabric-add-a-web-frontend.md)

### Настройка безопасности
#### [Управление секретами приложений](service-fabric-application-secret-management.md)  
#### [Настройка политик безопасности для приложения](service-fabric-application-runas-security.md)

## Работа в среде разработки Windows
### [Управление приложениями в Visual Studio](service-fabric-manage-application-in-visual-studio.md)
### [Настройка безопасных соединений в Visual Studio](service-fabric-visualstudio-configure-secure-connections.md)
### [Настройка приложения для нескольких сред](service-fabric-manage-multiple-environment-app-configuration.md)
### [Отладка службы .NET в VS](service-fabric-debugging-your-application.md)
### [Распространенные ошибки и исключения](service-fabric-errors-and-exceptions.md)
### [Локальный мониторинг и диагностика](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md)

## Работа в среде разработки Linux
### [Начало работы с подключаемым модулем Eclipse для разработки приложений Java](service-fabric-get-started-eclipse.md)
### [Отладка службы на Java в Eclipse](service-fabric-debugging-your-application-java.md)
### [Локальный мониторинг и диагностика](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally-linux.md)

## Интеграция со службой управления API
### [Обзор](service-fabric-api-management-overview.md)
### [Краткое руководство](service-fabric-api-management-quick-start.md)

## Миграция из облачных служб
### [Сравнение облачных служб и Service Fabric](service-fabric-cloud-services-migration-differences.md)
### [Перенос tooService структуры](service-fabric-cloud-services-migration-worker-role-stateless-service.md)
### [Рекомендации](/azure/architecture/service-fabric/migrate-from-cloud-services)

## Управление жизненным циклом приложения
### [Создание пакета приложения](service-fabric-package-apps.md)

### Развертывание или удаление приложений
#### [Развертывание приложений в локальном кластере](service-fabric-get-started-with-a-local-cluster.md)
#### [PowerShell](service-fabric-deploy-remove-applications.md)
#### [Интерфейс командной строки Service Fabric](service-fabric-application-lifecycle-sfctl.md)
#### [Visual Studio](service-fabric-publish-app-remote-cluster.md)
#### [API-интерфейсы FabricClient](service-fabric-deploy-remove-applications-fabricclient.md)

### Обновление приложений
#### [Обновление с помощью PowerShell](service-fabric-application-upgrade-tutorial-powershell.md)
#### [Обновление с помощью Visual Studio](service-fabric-application-upgrade-tutorial.md)
#### [Устранение неполадок при обновлениях приложений](service-fabric-application-upgrade-troubleshooting.md)

### Тестирование приложений и служб
#### [Тестирование связи между службами](service-fabric-testability-scenarios-service-communication.md)
#### Моделирование сбоев
##### [Использование контролируемого хаоса](service-fabric-controlled-chaos.md)
##### [Использование тестовых действий](service-fabric-testability-actions.md)
##### [При выполнении рабочих нагрузок](service-fabric-testability-workload-tests.md)
##### [Использование тестовых сценариев](service-fabric-testability-scenarios.md)
##### [С помощью перехода узла hello API-интерфейсы](service-fabric-node-transition-apis.md)
#### [Нагрузочный тест приложения](service-fabric-vso-load-test.md)

### Настройка непрерывной интеграции
#### [Настройка непрерывной интеграции с помощью VSTS](service-fabric-set-up-continuous-integration.md)
#### [Развертывание приложения Linux на Java с помощью Jenkins](service-fabric-cicd-your-linux-java-application-with-jenkins.md)

## Создание кластеров и управление ими
### Кластеры в Azure
#### Создание
##### [Создание первого кластера в Azure](service-fabric-get-started-azure-cluster.md)
##### [Портал Azure](service-fabric-cluster-creation-via-portal.md)
##### [Диспетчер ресурсов Azure](service-fabric-cluster-creation-via-arm.md)
#### Масштаб
##### [Вручную](service-fabric-cluster-scale-up-down.md)
##### [Программным способом](service-fabric-cluster-programmatic-scaling.md)
#### [Обновление](service-fabric-cluster-upgrade.md)
#### [Настройка управления доступом](service-fabric-cluster-security-roles.md)
#### [Настройка](service-fabric-cluster-fabric-settings.md)
#### [Открытие порта в hello балансировки нагрузки](create-load-balancer-rule.md)
#### [Управление сертификатами кластера](service-fabric-cluster-security-update-certs-azure.md)
#### [Удалить](service-fabric-cluster-delete.md)

### Изолированные кластеры
#### [Планирование и подготовка развертывания](service-fabric-cluster-standalone-deployment-preparation.md)
#### Создание
##### [Создание первого автономного кластера](service-fabric-get-started-standalone-cluster.md)
##### [Создание локальной среды](service-fabric-cluster-creation-for-windows-server.md)
##### [Безопасное использование сертификатов](service-fabric-windows-cluster-x509-security.md)  
##### [Защита кластера с помощью системы безопасности Windows](service-fabric-windows-cluster-windows-security.md)
##### [Содержимое hello автономного пакета](service-fabric-cluster-standalone-package-contents.md)
#### [Масштабирование](service-fabric-cluster-windows-server-add-remove-nodes.md)
#### [Настройка управления доступом](service-fabric-cluster-security-roles.md)
#### [Настройка](service-fabric-cluster-manifest.md)
#### [Обновление](service-fabric-cluster-upgrade-windows-server.md)

### [Визуализация кластера](service-fabric-visualizing-your-cluster.md)
### [Подключите кластер безопасного tooa](service-fabric-connect-to-secure-cluster.md)

### [Управлять кластером с помощью интерфейса командной строки Service Fabric](service-fabric-cli.md)
### [Установка исправлений для узлов кластера](service-fabric-patch-orchestration-application.md)

### Ресурсы кластера: управление и оркестрация
#### [Обзор диспетчера кластерных ресурсов](service-fabric-cluster-resource-manager-introduction.md)
#### [Архитектура диспетчера кластерных ресурсов](service-fabric-cluster-resource-manager-architecture.md)
#### [Описание кластера](service-fabric-cluster-resource-manager-cluster-description.md)
#### [Обзор групп приложений](service-fabric-cluster-resource-manager-application-groups.md)
#### [Настройка параметров диспетчера кластерных ресурсов](service-fabric-cluster-resource-manager-configure-services.md)
#### [Метрики потребления ресурсов](service-fabric-cluster-resource-manager-metrics.md)
#### [Использование сходства служб](service-fabric-cluster-resource-manager-advanced-placement-rules-affinity.md)
#### [Политики размещения служб](service-fabric-cluster-resource-manager-advanced-placement-rules-placement-policies.md)
#### [Управление кластером](service-fabric-cluster-resource-manager-management-integration.md)
#### [Дефрагментация кластера](service-fabric-cluster-resource-manager-defragmentation-metrics.md)
#### [Балансировка кластера](service-fabric-cluster-resource-manager-balancing.md)
#### [Регулирование](service-fabric-cluster-resource-manager-advanced-throttling.md)
#### [Перемещение служб](service-fabric-cluster-resource-manager-movement-cost.md)

## Мониторинг и диагностика
### [Приложения мониторинга и диагностики](service-fabric-diagnostics-overview.md)
### Создание событий
#### [Создание событий на уровне платформы](service-fabric-diagnostics-event-generation-infra.md)
##### [Операционный канал](service-fabric-diagnostics-event-generation-operational.md)
##### [События Reliable Services](service-fabric-reliable-services-diagnostics.md)
##### [События Reliable Actors](service-fabric-reliable-actors-diagnostics.md)
##### [Метрики производительности](service-fabric-diagnostics-event-generation-perf.md)
#### [Создание событий на уровне приложения](service-fabric-diagnostics-event-generation-app.md)
### Проверка работоспособности приложения и кластера
#### [Отслеживание работоспособности Service Fabric](service-fabric-health-introduction.md)
#### [Проверка работоспособности службы и оповещение о проблемах](service-fabric-diagnostics-how-to-report-and-check-service-health.md)
#### [Добавление настраиваемых отчетов о работоспособности](service-fabric-report-health.md)
#### [Устранение неполадок с помощью отчетов о работоспособности системы](service-fabric-understand-and-troubleshoot-with-system-health-reports.md)
#### [Просмотр отчетов о работоспособности](service-fabric-view-entities-aggregated-health.md)
#### [Отслеживание контейнеров Windows Server](service-fabric-diagnostics-containers-windowsserver.md)
### Статистическая обработка событий
#### [Статистическая обработка событий с помощью EventFlow](service-fabric-diagnostics-event-aggregation-eventflow.md)
#### Статистическая обработка событий с помощью системы диагностики Azure
##### [Windows](service-fabric-diagnostics-event-aggregation-wad.md)
##### [Linux](service-fabric-diagnostics-event-aggregation-lad.md)
### Анализ событий
#### [Анализ событий с помощью Application Insights](service-fabric-diagnostics-event-analysis-appinsights.md)
#### [Анализ событий с помощью OMS](service-fabric-diagnostics-event-analysis-oms.md)
### [Устранение неполадок локального кластера](service-fabric-troubleshoot-local-cluster-setup.md)

# Справочные материалы
## [PowerShell (Azure)](/powershell/module/azurerm.servicefabric/)
## [PowerShell](/powershell/module/servicefabric/?view=azureservicefabricps)
## [Интерфейс командной строки Azure](/cli/azure/sf)
## [API Java](/java/api/overview/azure/servicefabric)
## [.NET](/dotnet/api/overview/azure/service-fabric?view=azure-dotnet)
## [REST](/rest/api/servicefabric)

# Ресурсы
## [Стратегия развития Azure](https://azure.microsoft.com/roadmap/)
## [Часто задаваемые вопросы](service-fabric-common-questions.md)
## [Схема обучения](https://azure.microsoft.com/documentation/learning-paths/service-fabric/)
## [Форум MSDN](https://social.msdn.microsoft.com/Forums/home?forum=AzureServiceFabric)
## [Цены](https://azure.microsoft.com/pricing/details/service-fabric/)
## [Калькулятор цен](https://azure.microsoft.com/pricing/calculator/)
## [Пример кода](http://aka.ms/servicefabricsamples)
## [Варианты поддержки](service-fabric-support.md)
## [Обновления службы](https://azure.microsoft.com/updates/?product=service-fabric)
## [Видеоролики](https://azure.microsoft.com/documentation/videos/index/?services=service-fabric)
