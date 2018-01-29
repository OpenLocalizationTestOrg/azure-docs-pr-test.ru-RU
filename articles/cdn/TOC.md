# [Обзор](cdn-overview.md)
## [Что такое Azure CDN?](../best-practices-cdn.md?toc=%2fazure%2fcdn%2ftoc.json)

# Начало работы
## [Включение Azure CDN](cdn-create-new-endpoint.md)

# Практическое руководство
## Интеграция
### [Веб-приложения](../app-service/app-service-web-tutorial-content-delivery-network.md?toc=%2fazure%2fcdn%2ftoc.json)
### [Облачные службы](cdn-cloud-service-with-cdn.md)
### Хранилище
#### [Интеграция учетной записи хранения](cdn-create-a-storage-account-with-cdn.md)
#### [Поддержка хранилища SAS](cdn-sas-storage-support.md)
### [Общий доступ к ресурсам независимо от источника](cdn-cors.md)
### [Добавление личного домена к конечной точке CDN](cdn-map-content-to-custom-domain.md)
### [Настройка HTTPS в личном домене](cdn-custom-ssl.md)
## Оптимизация содержимого
### [Общие сведения об оптимизации](cdn-optimization-overview.md)
####[Оптимизация больших файлов](cdn-large-file-optimization.md)
####[Оптимизация потоковой передачи мультимедиа](cdn-media-streaming-optimization.md)
####[Динамическое ускорение сайтов](cdn-dynamic-site-acceleration.md)
 
## управление
### [Управление с помощью Azure PowerShell](cdn-manage-powershell.md)
### [Ограничение доступа в зависимости от страны](cdn-restrict-access-by-country.md)
### [Повышение производительности за счет сжатия файлов](cdn-improve-performance.md)
### Управление поведением кэширования
#### [Как выполняется кэширование](cdn-how-caching-works.md)
#### [Управление поведением кэширования с помощью правил](cdn-caching-rules.md)
#### Кэширование содержимого по строкам запросов
##### [Уровень Standard](cdn-query-string.md)
##### [Уровень Premium](cdn-query-string-premium.md)
#### [Удаление кэшированных ресурсов](cdn-purge-endpoint.md)
#### [Предварительная загрузка кэшированных ресурсов](cdn-preload-endpoint.md)
### Настройка срока жизни
#### [Веб-содержимое Azure](cdn-manage-expiration-of-cloud-service-content.md)
#### [хранилище BLOB-объектов Azure](cdn-manage-expiration-of-blob-content.md)
### [Проверка подлинности по маркерам](cdn-token-auth.md)
### [Мониторинг ресурсов](cdn-resource-health.md)
### [Переопределение поведения с помощью правил](cdn-rules-engine.md)
### [Получение оповещений в реальном времени](cdn-real-time-alerts.md)
### [Поддержка HTTP/2](cdn-http2.md)

## Анализ
### [Анализ вариантов использования CDN Azure](cdn-log-analysis.md)
#### [Журналы диагностики Azure](cdn-azure-diagnostic-logs.md)
#### Средства аналитики для Azure CDN от Verizon
##### [Основные отчеты из Verizon](cdn-analyze-usage-patterns.md)
##### [Настраиваемые отчеты из Verizon](cdn-verizon-custom-reports.md)
#### Средства аналитики для Azure CDN уровня "Премиум" от Verizon
##### [Создание расширенных отчетов HTTP](cdn-advanced-http-reports.md)
##### [Просмотр статистики в реальном времени](cdn-real-time-stats.md)
##### [Анализ производительности граничного узла](cdn-edge-performance.md)

## Разработка
### [.NET](cdn-app-dev-net.md)
### [Node.js](cdn-app-dev-node.md)

## Устранение неполадок
### [Состояние 404](cdn-troubleshoot-endpoint.md)
### [Сжатие файлов](cdn-troubleshoot-compression.md)

# Справочные материалы
## [Примеры кода](https://azure.microsoft.com/en-us/resources/samples/?service=cdn)
## [Azure PowerShell](/powershell/module/azurerm.cdn)
## [.NET](/dotnet/api/microsoft.azure.management.cdn)
## [Java](/java/api/com.microsoft.azure.management.cdn)
## [REST](/rest/api/cdn/)

# Ресурсы
##  [Справочник по обработчику правил](cdn-rules-engine-reference.md)
### [Условные выражения обработчика правил](cdn-rules-engine-reference-conditional-expressions.md)
### [Функции обработчика правил](cdn-rules-engine-reference-features.md)
### [Условия соответствия обработчика правил](cdn-rules-engine-reference-match-conditions.md)
## [Расположение узлов POP сети Azure CDN](cdn-pop-locations.md)
## [Стратегия развития Azure](https://azure.microsoft.com/roadmap/)
## [Форум MSDN](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurecdn)
## [Цены](https://azure.microsoft.com/pricing/details/cdn/)
## [Калькулятор цен](https://azure.microsoft.com/pricing/calculator/)
## [Обновления службы](https://azure.microsoft.com/updates/?product=cdn)
## [Stack Overflow](http://stackoverflow.com/questions/tagged/azure-cdn)
## [Видеоролики](https://azure.microsoft.com/documentation/videos/index/?services=cdn)

