---
title: "aaaAzure операций поставщика для диспетчера ресурсов | Документы Microsoft"
description: "Сведения о hello операций, доступных в hello поставщиков ресурсов Microsoft Azure Resource Manager"
services: active-directory
documentationcenter: 
author: jboeshart
manager: 
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 04/28/2017
ms.author: jaboes
ms.openlocfilehash: 2d2f912ecbade335667d68fdc42ce03a2930a0eb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-resource-manager-resource-provider-operations"></a>Операции поставщиков ресурсов Azure Resource Manager

В этом документе перечислены операции hello, доступные для каждого поставщика ресурсов Microsoft Azure Resource Manager. Их можно использовать в tooresources разрешения пользовательскими ролями tooprovide детального контроля доступа на основе ролей (RBAC) в Azure. Обратите внимание на то, что это не полный список, и операции могут добавляться или удаляться по мере обновления поставщиков. Формат hello выполните операцию строки `Microsoft.<ProviderName>/<ChildResourceType>/<action>`. Полный список текущего использования `Get-AzureRmProviderOperation` (в PowerShell) или `azure provider operations show` (в Azure CLI) toolist операций поставщиков ресурсов Azure.

## <a name="microsoftadhybridhealthservice"></a>Microsoft.ADHybridHealthService

| Операция | Описание |
|---|---|
|/configuration/action|Обновляет конфигурацию клиента.|
|/services/action|Обновляет экземпляр службы в клиенте hello.|
|/configuration/write|Создает конфигурацию клиента.|
|/configuration/read|Считывает hello настройки конфигурации клиента.|
|/services/write|Создает экземпляр службы в клиенте hello.|
|/services/read|Считывает hello экземпляров службы в клиенте hello.|
|/services/delete|Удаляет экземпляр службы в клиенте hello.|
|/services/servicemembers/action|Создает экземпляр элемента службы в службе hello.|
|/services/servicemembers/read|Считывает hello экземпляр элемента службы в службе hello.|
|/services/servicemembers/delete|Удаляет член экземпляра службы в службе hello.|
|/services/servicemembers/alerts/read|Считывает hello оповещения для участника службы.|
|/services/alerts/read|Считывает hello оповещения для службы.|
|/services/alerts/read|Считывает hello оповещения для службы.|

## <a name="microsoftadvisor"></a>Microsoft.Advisor

| Операция | Описание |
|---|---|
|/generateRecommendations/action|Создает рекомендации.|
|/suppressions/action|Создает или обновляет подавления.|
|/register/action|Регистрирует hello подписки для hello Microsoft Advisor|
|/generateRecommendations/read|Возвращает состояние создания рекомендаций.|
|/recommendations/read|Считывает рекомендации.|
|/suppressions/read|Возвращает подавления.|
|/suppressions/delete|Удаляет подавления.|

## <a name="microsoftanalysisservices"></a>Microsoft.AnalysisServices

| Операция | Описание |
|---|---|
|/servers/read|Получает сведения о hello объекта hello указан сервер анализа данных.|
|/servers/write|Создает или обновляет hello указан сервер анализа данных.|
|/servers/delete|Удаляет hello сервера анализа данных.|
|/servers/suspend/action|Приостанавливает hello сервера анализа данных.|
|/servers/resume/action|Резюме hello сервера анализа данных.|
|/servers/checkNameAvailability<br>/action|Проверяет, является ли данное имя сервера анализа данных допустимым и неиспользуемым.|

## <a name="microsoftapimanagement"></a>Microsoft.ApiManagement

| Операция | Описание |
|---|---|
|/checkNameAvailability/action|Проверяет, доступно ли указанное имя службы.|
|/register/action|Регистрирует подписку для поставщика ресурсов Microsoft.ApiManagement.|
|/unregister/action|Отменяет регистрацию подписки для поставщика ресурсов Microsoft.ApiManagement.|
|/service/write|Создает экземпляр службы управления API.|
|/service/read|Считывает метаданные для экземпляра службы управления API.|
|/service/delete|Удаляет экземпляр службы управления API.|
|/service/updatehostname/action|Позволяет настроить, обновить или удалить имена личных доменов для службы управления API.|
|/service/uploadcertificate/action|Передает SSL-сертификата для службы управления API.|
|/service/backup/action|Резервной копии службы управления API toohello контейнера, заданного в пользователя предоставлен учетной записи хранилища|
|/service/restore/action|Восстановление службы управления API из указанного контейнера hello в пользователя, предоставленных учетной записи хранилища|
|/service/managedeployments/action|Позволяет изменить номер SKU или единицы, а также добавить или удалить региональные развертывания службы управления API.|
|/service/getssotoken/action|Получает токен единого входа, который можно использовать toologin портал прежних версий службы управления API от имени администратора|
|/service/applynetworkconfigurationupdates/action|Ресурсов Microsoft.ApiManagement hello обновлений, выполняемых в виртуальной сети toopick обновить параметры сети.|
|/service/operationresults/read|Возвращает текущее состояние длительной операции.|
|/service/networkStatus/read|Возвращает состояние доступа hello сетевых ресурсов.|
|/service/loggers/read|Возвращает список средств ведения журнала или сведения о средстве ведения журнала.|
|/service/loggers/write|Добавляет новое средство ведения журнала или обновляет существующее.|
|/service/loggers/delete|Удаляет существующее средство ведения журнала.|
|/service/users/read|Возвращает список зарегистрированных пользователей или сведения об учетной записи пользователя.|
|/service/users/write|Регистрирует нового пользователя или обновляет данные учетной записи существующего пользователя.|
|/service/users/delete|Удаляет учетную запись пользователя.|
|/service/users/generateSsoUrl/action|Создает URL-адрес единого входа. Hello URL-адрес может быть tooaccess используется портал администрирования|
|/service/users/subscriptions/read|Возвращает список подписок пользователя.|
|/service/users/keys/read|Возвращает список ключей пользователя.|
|/service/users/groups/read|Возвращает список групп пользователя.|
|/service/tenant/operationResults/read|Возвращает список результатов операций или результат определенной операции.|
|/service/tenant/policy/read|Получить конфигурацию политики для клиента hello|
|/service/tenant/policy/write|Задать конфигурацию политики для клиента hello|
|/service/tenant/policy/delete|Удалить конфигурацию политики для клиента hello|
|/service/tenant/configuration/save/action|Создает фиксации с конфигурации моментального снимка toohello указанную ветвь в репозитории hello|
|/service/tenant/configuration/deploy/action|Запускает задачу развертывания tooapply изменения из конфигурации toohello ветви git указанного hello в базе данных.|
|/service/tenant/configuration/validate/action|Проверяет изменений из ветви git указанного hello|
|/service/tenant/configuration/operationResults/read|Возвращает список результатов операций или результат определенной операции.|
|/service/tenant/configuration/syncState/read|Возвращает состояние последней синхронизации с Git.|
|/service/tenant/access/read|Возвращает сведения о доступе клиента.|
|/service/tenant/access/write|Обновляет сведения о доступе клиента.|
|/service/tenant/access/regeneratePrimaryKey/action|Повторно создает первичный ключ доступа.|
|/service/tenant/access/regenerateSecondaryKey/action|Повторно создает вторичный ключ доступа.|
|/service/identityProviders/read|Возвращает список поставщиков удостоверений или сведения о поставщике удостоверений.|
|/service/identityProviders/write|Создает новый поставщик удостоверений или обновляет данные существующего.|
|/service/identityProviders/delete|Удаляет существующий поставщик удостоверений.|
|/service/subscriptions/read|Возвращает список подписок на продукт или сведения о подписке на продукт.|
|/service/subscriptions/write|Подписка существующего пользователя tooan существующий продукт или обновить существующие сведения о подписке. Эта операция может быть используется toorenew подписки|
|/service/subscriptions/delete|Удаляет подписку. Эта операция может быть используется toodelete подписки|
|/service/subscriptions/regeneratePrimaryKey/action|Повторно создает первичный ключ подписки.|
|/service/subscriptions/regenerateSecondaryKey/action|Повторно создает вторичный ключ подписки.|
|/service/backends/read|Возвращает список серверных частей или сведения о серверной части.|
|/service/backends/write|Добавляет новую серверную часть или обновляет данные существующей.|
|/service/backends/delete|Удаляет существующую серверную часть.|
|/service/apis/read|Возвращает список всех зарегистрированных интерфейсов API или сведения об API.|
|/service/apis/write|Создает новый API или обновляет данные существующего API.|
|/service/apis/delete|Удаляет существующий API.|
|/service/apis/policy/read|Возвращает сведения о конфигурации политики для API.|
|/service/apis/policy/write|Задает сведения о конфигурации политики для API.|
|/service/apis/policy/delete|Удаляет конфигурацию политики из API.|
|/service/apis/operations/read|Возвращает список существующих операций API или сведения о конкретной операции API.|
|/service/apis/operations/write|Создает новую операцию API или обновляет существующую.|
|/service/apis/operations/delete|Удаляет существующую операцию API.|
|/service/apis/operations/policy/read|Возвращает сведения о конфигурации политики для операции.|
|/service/apis/operations/policy/write|Задает сведения о конфигурации политики для операции.|
|/service/apis/operations/policy/delete|Удаляет конфигурацию политики из операции.|
|/service/products/read|Возвращает список продуктов или сведения о продукте.|
|/service/products/write|Создает новый продукт или обновляет данные существующего.|
|/service/products/delete|Удаляет существующий продукт.|
|/service/products/subscriptions/read|Возвращает список подписок на продукт.|
|/service/products/apis/read|Получение списка интерфейсов API добавлены tooexisting продукта|
|/service/products/apis/write|Добавить существующий товар tooexisting API|
|/service/products/apis/delete|Удаляет API из существующего продукта.|
|/service/products/policy/read|Возвращает конфигурацию политики существующего продукта.|
|/service/products/policy/write|Задает конфигурацию политики существующего продукта.|
|/service/products/policy/delete|Удаляет конфигурацию политики из существующего продукта.|
|/service/products/groups/read|Возвращает список групп разработчиков, связанных с продуктом.|
|/service/products/groups/write|Устанавливает связь между существующими продуктом и группой разработчиков.|
|/service/products/groups/delete|Удаляет связь между существующими продуктом и группой разработчиков.|
|/service/openidConnectProviders/read|Возвращает список поставщиков OpenID Connect или сведения о поставщике OpenID Connect.|
|/service/openidConnectProviders/write|Создает новый поставщик OpenID Connect или обновляет данные существующего.|
|/service/openidConnectProviders/delete|Удаляет существующий поставщик OpenID Connect.|
|/service/certificates/read|Возвращает список сертификатов или сведения о сертификате.|
|/service/certificates/write|Добавляет новый сертификат.|
|/service/certificates/delete|Удаляет существующий сертификат.|
|/service/properties/read|Возвращает список всех свойств или сведения об указанном свойстве.|
|/service/properties/write|Создает новое свойство или обновляет значение указанного свойства.|
|/service/properties/delete|Удаляет существующее свойство.|
|/service/groups/read|Возвращает список групп или сведения о группе.|
|/service/groups/write|Создает новую группу или обновляет данные существующей.|
|/service/groups/delete|Удаляет существующую группу.|
|/service/groups/users/read|Возвращает список пользователей группы.|
|/service/groups/users/write|Добавить существующую группу tooexisting пользователя|
|/service/groups/users/delete|Удаляет пользователя из существующей группы.|
|/service/authorizationServers/read|Возвращает список серверов авторизации или сведения о сервере авторизации.|
|/service/authorizationServers/write|Создает новый сервер авторизации или обновляет данные существующего.|
|/service/authorizationServers/delete|Удаляет существующий сервер авторизации.|
|/service/reports/bySubscription/read|Возвращает отчет, объединенный по подписке.|
|/service/reports/byRequest/read|Возвращает запросы, передающие данные.|
|/service/reports/byOperation/read|Возвращает отчет, объединенный по операциям.|
|/service/reports/byGeo/read|Возвращает отчет, объединенный по географическому региону.|
|/service/reports/byUser/read|Возвращает отчет, объединенный по разработчикам.|
|/service/reports/byTime/read|Возвращает отчет, объединенный по временным периодам.|
|/service/reports/byApi/read|Возвращает отчет, объединенный по интерфейсам API.|
|/service/reports/byProduct/read|Возвращает отчет, объединенный по продуктам.|

## <a name="microsoftappservice"></a>Microsoft.AppService

| Операция | Описание |
|---|---|
|/appidentities/Read|Возвращает hello ресурс (веб-узел), зарегистрированный hello шлюза.|
|/appidentities/Write|Создает удостоверение приложения.|
|/appidentities/Delete|Удаляет существующее удостоверение приложения.|
|/deploymenttemplates/listMetadata/Action|Перечисляются метаданные пользовательского интерфейса, связанный с hello пакет приложения API.|
|/deploymenttemplates/generate/Action|Возвращает шаблон развертывания tooprovision экземпляры приложения API.|
|/gateways/Read|Экземпляр шлюза возвращает hello.|
|/gateways/Write|Создает новый шлюз или обновляет существующий.|
|/gateways/Delete|Удаляет существующий экземпляр шлюза.|
|/gateways/listLoginUris/Action|Заполняет хранилище маркеров и возвращает универсальные коды ресурса (URI) имени для входа OAuth.|
|/gateways/listKeys/Action|Возвращает секреты шлюза.|
|/gateways/tokens/Write|Создает новый маркер Zumo с заданным именем hello.|
|/gateways/registrations/Read|Возвращает hello ресурс (веб-узел), зарегистрированный hello шлюза.|
|/gateways/registrations/Write|Регистрирует hello шлюза ресурсов (веб-сайт).|
|/gateways/registrations/Delete|Отменяет регистрацию ресурс (веб-сайт) из hello шлюза.|
|/apiapps/Read|Возвращает hello экземпляр приложения API.|
|/apiapps/Write|Создает новое приложение API или обновляет существующее.|
|/apiapps/Delete|Удаляет существующий экземпляр приложения API.|
|/apiapps/listStatus/Action|Возвращает состояние приложения API.|
|/apiapps/listKeys/Action|Возвращает секреты приложения API.|
|/apiapps/apidefinitions/Read|Возвращает определение API для приложения API.|

## <a name="microsoftauthorization"></a>Microsoft.Authorization

| Операция | Описание |
|---|---|
|/elevateAccess/action|Предоставляет hello вызывающий объект доступа администратор доступа пользователя в области приветствия клиента|
|/classicAdministrators/read|Считывает hello администраторов для подписки hello.|
|/classicAdministrators/write|Добавление или изменение подписки tooa администратора.|
|/classicAdministrators/delete|Здравствуйте, администратор удаляет из подписки hello.|
|/locks/read|Получает блокировки на hello указана область.|
|/locks/write|Добавление блокировок в указанный hello области.|
|/locks/delete|Удаление блокировок в hello указана область.|
|/policyAssignments/read|Возвращает сведения о назначении политики.|
|/policyAssignments/write|Создать политику назначения на hello указан области.|
|/policyAssignments/delete|Удаление назначения политики в hello указана область.|
|/permissions/read|Список всех разрешений hello, которые у вызывающего объекта hello в заданной области.|
|/roleDefinitions/read|Возвращает сведения об определении роли.|
|/roleDefinitions/write|Создает или обновляет определение настраиваемой роли с помощью указанных разрешений и назначаемых областей.|
|/roleDefinitions/delete|Удалить hello указанного определения пользовательской роли.|
|/providerOperations/read|Возвращает операции для всех поставщиков ресурсов, которые могут быть использованы в определениях ролей.|
|/policyDefinitions/read|Возвращает сведения об определении политики.|
|/policyDefinitions/write|Создает определение настраиваемой политики.|
|/policyDefinitions/delete|Удаляет определение политики.|
|/roleAssignments/read|Возвращает сведения о назначении роли.|
|/roleAssignments/write|Создание роли назначения на hello указан области.|
|/roleAssignments/delete|Удалить назначение роли в hello указана область.|

## <a name="microsoftautomation"></a>Microsoft.Automation

| Операция | Описание |
|---|---|
|/automationAccounts/read|Возвращает учетную запись службы автоматизации Azure.|
|/automationAccounts/write|Создает или обновляет учетную запись службы автоматизации Azure.|
|/automationAccounts/delete|Удаляет учетную запись службы автоматизации Azure.|
|/automationAccounts/configurations/readContent/action|Возвращает содержимое Azure Automation DSC.|
|/automationAccounts/hybridRunbookWorkerGroups/read|Считывает ресурсы гибридной рабочей роли Runbook.|
|/automationAccounts/hybridRunbookWorkerGroups/delete|Удаляет ресурсы гибридной рабочей роли Runbook.|
|/automationAccounts/jobSchedules/read|Возвращает расписание заданий службы автоматизации Azure.|
|/automationAccounts/jobSchedules/write|Создает расписание заданий службы автоматизации Azure.|
|/automationAccounts/jobSchedules/delete|Удаляет расписание заданий службы автоматизации Azure.|
|/automationAccounts/connectionTypes/read|Возвращает ресурс типа подключения службы автоматизации Azure.|
|/automationAccounts/connectionTypes/write|Создает ресурс типа подключения службы автоматизации Azure.|
|/automationAccounts/connectionTypes/delete|Удаляет ресурс типа подключения службы автоматизации Azure.|
|/automationAccounts/modules/read|Возвращает модуль службы автоматизации Azure.|
|/automationAccounts/modules/write|Создает или обновляет модуль службы автоматизации Azure.|
|/automationAccounts/modules/delete|Удаляет модуль службы автоматизации Azure.|
|/automationAccounts/credentials/read|Возвращает ресурс учетных данных службы автоматизации Azure.|
|/automationAccounts/credentials/write|Создает или обновляет ресурс учетных данных службы автоматизации Azure.|
|/automationAccounts/credentials/delete|Удаляет ресурс учетных данных службы автоматизации Azure.|
|/automationAccounts/certificates/read|Возвращает ресурс сертификата службы автоматизации Azure.|
|/automationAccounts/certificates/write|Создает или обновляет ресурс сертификата службы автоматизации Azure.|
|/automationAccounts/certificates/delete|Удаляет ресурс сертификата службы автоматизации Azure.|
|/automationAccounts/schedules/read|Возвращает ресурс расписания службы автоматизации Azure.|
|/automationAccounts/schedules/write|Создает или обновляет ресурс расписания службы автоматизации Azure.|
|/automationAccounts/schedules/delete|Удаляет ресурс расписания службы автоматизации Azure.|
|/automationAccounts/jobs/read|Возвращает задание службы автоматизации Azure.|
|/automationAccounts/jobs/write|Создает задание службы автоматизации Azure.|
|/automationAccounts/jobs/stop/action|Останавливает задание службы автоматизации Azure.|
|/automationAccounts/jobs/suspend/action|Приостанавливает задание службы автоматизации Azure.|
|/automationAccounts/jobs/resume/action|Возобновляет выполнение задания службы автоматизации Azure.|
|/automationAccounts/jobs/runbookContent/action|Получает содержимое runbook службы автоматизации Azure hello hello во время выполнения задания hello hello|
|/automationAccounts/jobs/output/action|Получает выходные данные задания hello|
|/automationAccounts/jobs/read|Возвращает задание службы автоматизации Azure.|
|/automationAccounts/jobs/write|Создает задание службы автоматизации Azure.|
|/automationAccounts/jobs/stop/action|Останавливает задание службы автоматизации Azure.|
|/automationAccounts/jobs/suspend/action|Приостанавливает задание службы автоматизации Azure.|
|/automationAccounts/jobs/resume/action|Возобновляет выполнение задания службы автоматизации Azure.|
|/automationAccounts/jobs/streams/read|Возвращает поток задания службы автоматизации Azure.|
|/automationAccounts/connections/read|Возвращает ресурс подключения службы автоматизации Azure.|
|/automationAccounts/connections/write|Создает или обновляет ресурс подключения службы автоматизации Azure.|
|/automationAccounts/connections/delete|Удаляет ресурс подключения службы автоматизации Azure.|
|/automationAccounts/variables/read|Считывает ресурс переменной службы автоматизации Azure.|
|/automationAccounts/variables/write|Создает или обновляет ресурс переменной службы автоматизации Azure.|
|/automationAccounts/variables/delete|Удаляет ресурс переменной службы автоматизации Azure.|
|/automationAccounts/runbooks/readContent/action|Получает содержимое runbook службы автоматизации Azure hello|
|/automationAccounts/runbooks/read|Возвращает runbook службы автоматизации Azure.|
|/automationAccounts/runbooks/write|Создает или обновляет runbook службы автоматизации Azure.|
|/automationAccounts/runbooks/delete|Удаляет runbook службы автоматизации Azure.|
|/automationAccounts/runbooks/draft/readContent/action|Получает hello содержимое черновика runbook службы автоматизации Azure|
|/automationAccounts/runbooks/draft/writeContent/action|Создает hello содержимое черновика runbook службы автоматизации Azure|
|/automationAccounts/runbooks/draft/read|Возвращает черновик runbook службы автоматизации Azure.|
|/automationAccounts/runbooks/draft/publish/action|Публикует черновик runbook службы автоматизации Azure.|
|/automationAccounts/runbooks/draft/undoEdit/action|Отменить черновик runbook службы автоматизации Azure tooan изменения|
|/automationAccounts/runbooks/draft/testJob/read|Возвращает тестовое задание черновика runbook службы автоматизации Azure.|
|/automationAccounts/runbooks/draft/testJob/write|Создает тестовое задание черновика runbook службы автоматизации Azure.|
|/automationAccounts/runbooks/draft/testJob/stop/action|Останавливает тестовое задание черновика runbook службы автоматизации Azure.|
|/automationAccounts/runbooks/draft/testJob/suspend/action|Приостанавливает тестовое задание черновика runbook службы автоматизации Azure.|
|/automationAccounts/runbooks/draft/testJob/resume/action|Возобновляет выполнение тестового задания черновика runbook службы автоматизации Azure.|
|/automationAccounts/webhooks/read|Считывает runbook службы автоматизации Azure.|
|/automationAccounts/webhooks/write|Создает или обновляет webhook службы автоматизации Azure.|
|/automationAccounts/webhooks/delete|Удаляет webhook службы автоматизации Azure. |
|/automationAccounts/webhooks/generateUri/action|Создает универсальный код ресурса (URI) для webhook службы автоматизации Azure.|

## <a name="microsoftazureactivedirectory"></a>Microsoft.AzureActiveDirectory

Это не полный поставщик ARM, и он не предоставляет какие-либо операции ARM.

## <a name="microsoftbatch"></a>Microsoft.Batch

| Операция | Описание |
|---|---|
|/register/action|Регистрирует hello подписки для hello поставщика ресурсов пакета и обеспечивает создание учетных записей пакетного hello|
|/batchAccounts/write|Создает новую учетную запись пакетной службы или обновляет существующую.|
|/batchAccounts/read|Перечисляет учетные записи пакетного или получает свойства hello пакетной учетной записи|
|/batchAccounts/delete|Удаляет учетную запись пакетной службы.|
|/batchAccounts/listkeys/action|Отображает ключи доступа для учетной записи пакетной службы.|
|/batchAccounts/regeneratekeys/action|Повторно создает ключи доступа для учетной записи пакетной службы.|
|/batchAccounts/syncAutoStorageKeys/action|Синхронизирует ключи доступа для hello автоматического хранения данных учетной записи, настроенной для пакетной учетной записи|
|/batchAccounts/applications/read|Получает свойства приложения hello или список приложений|
|/batchAccounts/applications/write|Создает новое приложение или обновляет существующее.|
|/batchAccounts/applications/delete|Удаляет приложение.|
|/batchAccounts/applications/versions/read|Возвращает свойства hello для пакета приложения|
|/batchAccounts/applications/versions/write|Создает новый пакет приложения или обновляет существующий.|
|/batchAccounts/applications/versions/activate/action|Активирует пакет приложения.|
|/batchAccounts/applications/versions/delete|Удаляет пакет приложения.|
|/locations/quotas/read|Возвращает квоты пакета hello указан подписки в указанном регионе Azure hello|

## <a name="microsoftbilling"></a>Microsoft.Billing

| Операция | Описание |
|---|---|
|/invoices/read|Выводит список доступных счетов.|

## <a name="microsoftbingmaps"></a>Microsoft.BingMaps

| Операция | Описание |
|---|---|
|/mapApis/Read|Операция чтения.|
|/mapApis/Write|Операции записи.|
|/mapApis/Delete|Операция удаления.|
|/mapApis/regenerateKey/action|Повторно создает ключ hello|
|/mapApis/listSecrets/action|Hello список секретов|
|/mapApis/listSingleSignOnToken/action|Hello чтения единого входа на авторизации маркеров для ресурсов|
|/Operations/read|Описание операции hello.|

## <a name="microsoftcache"></a>Microsoft.Cache

| Операция | Описание |
|---|---|
|/checknameavailability/action|Проверяет, доступно ли имя для нового кэша Redis.|
|/register/action|Регистрирует поставщика ресурсов «Microsoft.Cache» hello с подпиской|
|/unregister/action|Отменяет регистрацию поставщика ресурсов «Microsoft.Cache» hello с подпиской|
|/redis/write|Изменение hello параметры и конфигурации кэша Redis на портале управления hello|
|/redis/read|Просмотр hello параметры и конфигурации кэша Redis на портале управления hello|
|/redis/delete|Удаление hello весь кэш Redis|
|/redis/listKeys/action|Представление hello значение ключей доступа к кэшу Redis на портале управления hello|
|/redis/regenerateKey/action|Измените значение hello ключи доступа кэша Redis на портале управления hello|
|/redis/import/action|Импортирует в Redis данные в указанном формате из нескольких больших двоичных объектов.|
|/redis/export/action|Экспорт Redis данных tooprefixed хранилища больших двоичных объектов в указанном формате|
|/redis/forceReboot/action|Принудительно перезапускает экземпляр кэша. При этом возможна потеря данных.|
|/redis/stop/action|Останавливает экземпляр кэша.|
|/redis/start/action|Запускает экземпляр кэша.|
|/redis/metricDefinitions/read|Возвращает hello доступные метрики для кэша Redis|
|/redis/firewallRules/read|Получить правила брандмауэра IP hello кэша Redis|
|/redis/firewallRules/write|Изменение правил брандмауэра IP hello кэша Redis|
|/redis/firewallRules/delete|Удаляет правила IP-адресов брандмауэра для кэша Redis.|
|/redis/listUpgradeNotifications/read|Список hello последние обновления уведомления для кэша клиента hello.|
|/redis/linkedservers/read|Возвращает связанные серверы для кэша Redis.|
|/redis/linkedservers/write|Добавление связанного сервера tooa кэша Redis|
|/redis/linkedservers/delete|Удаляет связанный сервер из кэша Redis.|
|/redis/patchSchedules/read|Возвращает hello исправления расписание кэша Redis|
|/redis/patchSchedules/write|Изменение hello исправления расписание кэша Redis|
|/redis/patchSchedules/delete|Удаление расписания обновления hello кэша Redis|

## <a name="microsoftcertificateregistration"></a>Microsoft.CertificateRegistration

| Операция | Описание |
|---|---|
|/provisionGlobalAppServicePrincipalInUserTenant/Action|Подготавливает субъект-службу для субъекта приложения-службы.|
|/validateCertificateRegistrationInformation/Action|Проверяет объект покупки сертификата без его отправки.|
|/register/action|Регистрация поставщика ресурсов hello сертификатов Майкрософт для подписки hello|
|/certificateOrders/Write|Добавляет новый заказ сертификата или обновляет существующий.|
|/certificateOrders/Delete|Удаляет существующий сертификат службы приложений.|
|/certificateOrders/Read|Получить список hello CertificateOrders|
|/certificateOrders/reissue/Action|Повторно отправляет существующий заказ сертификата.|
|/certificateOrders/renew/Action|Обновляет существующий заказ сертификата.|
|/certificateOrders/retrieveCertificateActions/Action|Получить список hello действия сертификата|
|/certificateOrders/retrieveEmailHistory/Action|Извлекает журнал электронных сообщений для сертификата.|
|/certificateOrders/resendEmail/Action|Повторно отправляет сообщение сертификата.|
|/certificateOrders/verifyDomainOwnership/Action|проверка принадлежности домена;|
|/certificateOrders/resendRequestEmails/Action|Запрос на повторную отправку tooanother адрес электронной почты, отправляется сообщение электронной почты|
|/certificateOrders/resendRequestEmails/Action|Извлекает печать сайта для выданного сертификата службы приложений.|
|/certificateOrders/certificates/Write|Добавляет новый сертификат или обновляет существующий.|
|/certificateOrders/certificates/Delete|Удаляет существующий сертификат.|
|/certificateOrders/certificates/Read|Получить список сертификатов hello|

## <a name="microsoftclassiccompute"></a>Microsoft.ClassicCompute

| Операция | Описание |
|---|---|
|/register/action|Зарегистрировать tooClassic вычислений|
|/checkDomainNameAvailability/action|Проверяет доступность заданного доменного имени hello.|
|/moveSubscriptionResources/action|Перемещение всех классических ресурсов tooa другую подписку.|
|/validateSubscriptionMoveAvailability/action|Проверьте доступность hello подписки для операции перемещения классический.|
|/operatingSystemFamilies/read|Перечисляет семейства гостевой операционной системы hello в Microsoft Azure, а также hello версии операционной системы для каждого f
|/capabilities/read|Показывает возможности hello|
|/operatingSystems/read|Список версий hello hello гостевой операционной системы, доступных в Microsoft Azure.|
|/resourceTypes/skus/read|Получает список hello Sku для поддерживаемых типов ресурсов.|
|/domainNames/read|Возвращать hello доменных имен для ресурсов.|
|/domainNames/write|Добавление или изменение hello доменных имен для ресурсов.|
|/domainNames/delete|Удалите hello доменных имен для ресурсов.|
|/domainNames/swap/action|Меняет местами hello промежуточного слота toohello производственный слот.|
|/domainNames/serviceCertificates/read|Возвращает hello использованных сертификатов службы.|
|/domainNames/serviceCertificates/write|Добавление или изменение использованных сертификатов службы hello.|
|/domainNames/serviceCertificates/delete|Удаление использованных сертификатов службы hello.|
|/domainNames/serviceCertificates/operationStatuses/read|Читает состояние операции hello для сертификатов службы hello доменных имен.|
|/domainNames/capabilities/read|Показывает возможности имя домена hello|
|/domainNames/extensions/read|Возвращает hello расширения доменных имен.|
|/domainNames/extensions/write|Добавление расширения доменных имен hello.|
|/domainNames/extensions/delete|Удалите hello расширения доменных имен.|
|/domainNames/extensions/operationStatuses/read|Читает состояние операции hello для hello доменные имена расширения.|
|/domainNames/active/write|Задает имя активного домена hello.|
|/domainNames/slots/read|Отображает hello слотов развертывания.|
|/domainNames/slots/write|Создает или обновляет развертывание hello.|
|/domainNames/slots/delete|Удаляет заданный слот развертывания.|
|/domainNames/slots/start/action|Запускает слот развертывания.|
|/domainNames/slots/stop/action|Приостанавливает hello слот развертывания.|
|/domainNames/slots/operationStatuses/read|Читает состояние операции hello для слотов имена домена hello.|
|/domainNames/slots/roles/read|Получение hello роли для слота развертывания hello.|
|/domainNames/slots/roles/extensionReferences/read|Возвращает hello ссылки на расширение для роли слота развертывания hello.|
|/domainNames/slots/roles/extensionReferences/write|Добавление или изменение hello ссылки на расширение для роли слота развертывания hello.|
|/domainNames/slots/roles/extensionReferences/delete|Удалите ссылку hello расширение для роли слота развертывания hello.|
|/domainNames/slots/roles/extensionReferences/operationStatuses/read|Читает состояние операции hello для ссылок на расширение ролей слотов в имена домена hello.|
|/domainNames/slots/roles/roleInstances/read|Получение экземпляра роли hello.|
|/domainNames/slots/roles/roleInstances/restart/action|Перезапускает экземпляры роли.|
|/domainNames/slots/roles/roleInstances/reimage/action|Экземпляр роли reimages hello.|
|/domainNames/slots/roles/roleInstances/operationStatuses/read|Читает состояние операции hello для экземпляров роли ролей слотов имена hello домена.|
|/domainNames/slots/state/start/write|Изменения hello toostopped состояние слота развертывания.|
|/domainNames/slots/state/stop/write|Изменения hello toostarted состояние слота развертывания.|
|/domainNames/slots/upgradeDomain/write|Показывает, как домен обновления hello.|
|/domainNames/internalLoadBalancers/read|Возвращает hello внутренних подсистем балансировки нагрузки.|
|/domainNames/internalLoadBalancers/write|Создает внутреннюю подсистему балансировки нагрузки.|
|/domainNames/internalLoadBalancers/delete|Удаляет внутреннюю подсистему балансировки нагрузки.|
|/domainNames/internalLoadBalancers/operationStatuses/read|Читает состояние операции hello для внутренних подсистем балансировки нагрузки имен доменов hello.|
|/domainNames/loadBalancedEndpointSets/read|Показывает наборы конечных точек с балансировкой нагрузки hello|
|/domainNames/loadBalancedEndpointSets/operationStatuses/read|Читает состояние операции hello для hello доменных имен наборы конечных точек с балансировкой нагрузки.|
|/domainNames/availabilitySets/read|Показать hello набор доступности для ресурса hello.|
|/quotas/read|Получите hello квоты для подписки hello.|
|/virtualMachines/read|Извлекает список виртуальных машин.|
|/virtualMachines/write|Добавляет или изменяет виртуальные машины.|
|/virtualMachines/delete|Удаляет виртуальные машины.|
|/virtualMachines/start/action|Запустите виртуальную машину hello.|
|/virtualMachines/redeploy/action|Повторно развертывает hello виртуальной машины.|
|/virtualMachines/restart/action|Перезапускает виртуальные машины.|
|/virtualMachines/stop/action|Останавливает hello виртуальной машины.|
|/virtualMachines/shutdown/action|Завершить работу виртуальной машины hello.|
|/virtualMachines/attachDisk/action|Присоединяет виртуальная машина tooa диска данных.|
|/virtualMachines/detachDisk/action|Отключает диск данных от виртуальной машины.|
|/virtualMachines/downloadRemoteDesktopConnectionFile/action|Загружает hello RDP-файл для виртуальной машины.|
|/virtualMachines/networkInterfaces/<br>associatedNetworkSecurityGroups/read|Получение группы безопасности сети hello, связанный с сетевым интерфейсом hello.|
|/virtualMachines/networkInterfaces/<br>associatedNetworkSecurityGroups/write|Добавляет группу безопасности сети, связанный с сетевым интерфейсом hello.|
|/virtualMachines/networkInterfaces/<br>associatedNetworkSecurityGroups/delete|Удаляет группу безопасности сети hello, связанный с сетевым интерфейсом hello.|
|/virtualMachines/networkInterfaces/<br>associatedNetworkSecurityGroups/operationStatuses/read|Читает состояние операции hello для виртуальных машин hello групп безопасности связанной сети.|
|/virtualMachines/providers/Microsoft.Insights/metricDefinitions/read|Возвращает определения показателей hello.|
|/virtualMachines/providers/Microsoft.Insights/diagnosticSettings/read|Получение параметров диагностики hello.|
|/virtualMachines/providers/Microsoft.Insights/diagnosticSettings/write|Добавляет или изменяет параметры диагностики.|
|/virtualMachines/metrics/read|Возвращает метрику hello.|
|/virtualMachines/operationStatuses/read|Читает состояние операции hello hello виртуальных машин.|
|/virtualMachines/extensions/read|Получает расширение виртуальной машины hello.|
|/virtualMachines/extensions/write|Помещает hello расширение виртуальной машины.|
|/virtualMachines/extensions/operationStatuses/read|Читает состояние операции hello для hello расширений виртуальных машин.|
|/virtualMachines/asyncOperations/read|Получает возможные асинхронные операции hello|
|/virtualMachines/disks/read|Извлекает список дисков данных.|
|/virtualMachines/associatedNetworkSecurityGroups/read|Получение группы безопасности сети hello, связанных с виртуальной машиной hello.|
|/virtualMachines/associatedNetworkSecurityGroups/write|Добавляет группу безопасности сети, связанной с виртуальной машиной hello.|
|/virtualMachines/associatedNetworkSecurityGroups/delete|Удаляет группу безопасности сети hello, связанных с виртуальной машиной hello.|
|/virtualMachines/associatedNetworkSecurityGroups/operationStatuses/read|Читает состояние операции hello для виртуальных машин hello групп безопасности связанной сети.|

## <a name="microsoftclassicnetwork"></a>Microsoft.ClassicNetwork

| Операция | Описание |
|---|---|
|/register/action|Зарегистрировать tooClassic сети|
|/gatewaySupportedDevices/read|Возвращает список поддерживаемых устройств hello.|
|/reservedIps/read|Возвращает hello зарезервированных IP-адресов|
|/reservedIps/write|Добавляет новый зарезервированный IP-адрес.|
|/reservedIps/delete|Удаляет зарезервированный IP-адрес.|
|/reservedIps/link/action|Привязывает зарезервированный IP-адрес.|
|/reservedIps/join/action|Присоединяет зарезервированный IP-адрес.|
|/reservedIps/operationStatuses/read|Читает состояние операции hello hello зарезервированных IP-адресов.|
|/virtualNetworks/read|Получение hello виртуальной сети.|
|/virtualNetworks/write|Добавляет новую виртуальную сеть.|
|/virtualNetworks/delete|Удаляет hello виртуальной сети.|
|/virtualNetworks/peer/action|Создает пиринг между виртуальными сетями.|
|/virtualNetworks/join/action|Присоединяет hello виртуальной сети.|
|/virtualNetworks/checkIPAddressAvailability/action|Проверяет доступность hello данного IP-адреса в виртуальной сети.|
|/virtualNetworks/capabilities/read|Показывает возможности hello|
|/virtualNetworks/subnets/<br>associatedNetworkSecurityGroups/read|Возвращает hello сетевой группы безопасности, связанный с подсетью hello.|
|/virtualNetworks/subnets/<br>associatedNetworkSecurityGroups/write|Добавляет группу безопасности сети, связанный с подсетью hello.|
|/virtualNetworks/subnets/<br>associatedNetworkSecurityGroups/delete|Удаляет группу безопасности сети hello, связанный с подсетью hello.|
|/virtualNetworks/subnets/<br>associatedNetworkSecurityGroups/operationStatuses/read|Читает состояние операции hello для группы безопасности связанной сети hello виртуальной сети подсети.|
|/virtualNetworks/operationStatuses/read|Читает состояние операции hello hello виртуальных сетей.|
|/virtualNetworks/gateways/read|Получает шлюзы виртуальной сети hello.|
|/virtualNetworks/gateways/write|Добавляет шлюз виртуальной сети.|
|/virtualNetworks/gateways/delete|Удаление шлюза виртуальной сети hello.|
|/virtualNetworks/gateways/startDiagnostics/action|Запускает диагностику шлюза виртуальной сети hello.|
|/virtualNetworks/gateways/stopDiagnostics/action|Останавливает hello диагностику шлюза виртуальной сети hello.|
|/virtualNetworks/gateways/downloadDiagnostics/action|Загружает hello диагностику шлюза.|
|/virtualNetworks/gateways/listCircuitServiceKey/action|Извлекает ключ службы канала hello.|
|/virtualNetworks/gateways/downloadDeviceConfigurationScript/action|Загрузка скрипта конфигурации устройства hello.|
|/virtualNetworks/gateways/listPackage/action|Список hello пакет шлюза виртуальной сети.|
|/virtualNetworks/gateways/operationStatuses/read|Читает состояние операции hello для шлюзов виртуальных сетей hello.|
|/virtualNetworks/gateways/packages/read|Получает пакет шлюза виртуальной сети hello.|
|/virtualNetworks/gateways/connections/read|Извлекает список подключений hello.|
|/virtualNetworks/gateways/connections/connect/action|Подключает соединение toosite шлюза сайта.|
|/virtualNetworks/gateways/connections/disconnect/action|Отключает соединение toosite шлюза сайта.|
|/virtualNetworks/gateways/connections/test/action|Проверяет подключение к шлюзу toosite сайта.|
|/virtualNetworks/gateways/clientRevokedCertificates/read|Hello чтение отозванных сертификатов клиента.|
|/virtualNetworks/gateways/clientRevokedCertificates/write|Отменяет сертификат клиента.|
|/virtualNetworks/gateways/clientRevokedCertificates/delete|Отменяет отмену сертификата клиента.|
|/virtualNetworks/gateways/clientRootCertificates/read|Найти hello клиентских корневых сертификатов.|
|/virtualNetworks/gateways/clientRootCertificates/write|Передает новый корневой сертификат клиента.|
|/virtualNetworks/gateways/clientRootCertificates/delete|Удаляет сертификат клиента шлюза виртуальной сети hello.|
|/virtualNetworks/gateways/clientRootCertificates/download/action|Скачивает сертификат по отпечатку.|
|/virtualNetworks/gateways/clientRootCertificates/listPackage/action|Перечисляет пакеты сертификатов шлюза виртуальной сети hello.|
|/networkSecurityGroups/read|Получение группы безопасности сети hello.|
|/networkSecurityGroups/write|Добавляет новую группу безопасности сети.|
|/networkSecurityGroups/delete|Удаляет группу безопасности сети hello.|
|/networkSecurityGroups/operationStatuses/read|Читает состояние операции hello для hello сетевой группы безопасности.|
|/networkSecurityGroups/securityRules/read|Получает правила безопасности hello.|
|/networkSecurityGroups/securityRules/write|Добавляет или обновляет правило безопасности.|
|/networkSecurityGroups/securityRules/delete|Удаляет правило безопасности hello.|
|/networkSecurityGroups/securityRules/operationStatuses/read|Читает состояние операции hello для правил безопасности группы безопасности сети hello.|
|/quotas/read|Получите hello квоты для подписки hello.|

## <a name="microsoftclassicstorage"></a>Microsoft.ClassicStorage

| Операция | Описание |
|---|---|
|/register/action|Зарегистрировать tooClassic хранилища|
|/checkStorageAccountAvailability/action|Проверка доступности hello учетной записи хранения.|
|/capabilities/read|Показывает возможности hello|
|/publicImages/read|Возвращает hello открытого образа виртуальной машины.|
|/images/read|Возвращает изображение hello.|
|/storageAccounts/read|Возвращать hello учетной записи хранилища с hello, учитывая учетной записи.|
|/storageAccounts/write|Добавляет новую учетную запись хранения.|
|/storageAccounts/delete|Удалите учетную запись хранения hello.|
|/storageAccounts/listKeys/action|Список hello клавиши доступа для учетных записей хранения hello.|
|/storageAccounts/regenerateKey/action|Повторно создает hello ключи доступа для учетной записи хранилища hello.|
|/storageAccounts/operationStatuses/read|Читает состояние операции hello для ресурса hello.|
|/storageAccounts/images/read|Возвращает hello образ учетной записи хранения.|
|/storageAccounts/images/delete|Удаляет заданный образ из учетной записи хранения.|
|/storageAccounts/disks/read|Возвращает hello диска учетной записи хранилища.|
|/storageAccounts/disks/write|Добавляет диск учетной записи хранения.|
|/storageAccounts/disks/delete|Удаляет заданный диск из учетной записи хранения.|
|/storageAccounts/disks/operationStatuses/read|Читает состояние операции hello для ресурса hello.|
|/storageAccounts/osImages/read|Возвращает hello образ операционной системы учетной записи хранения.|
|/storageAccounts/osImages/delete|Удаляет заданный образ операционной системы из учетной записи хранения.|
|/storageAccounts/services/read|Получение доступных служб hello.|
|/storageAccounts/services/metricDefinitions/read|Возвращает определения показателей hello.|
|/storageAccounts/services/metrics/read|Возвращает метрику hello.|
|/storageAccounts/services/diagnosticSettings/read|Получение параметров диагностики hello.|
|/storageAccounts/services/diagnosticSettings/write|Добавляет или изменяет параметры диагностики.|
|/disks/read|Возвращает hello диска учетной записи хранилища.|
|/osImages/read|Образ операционной системы возвращает hello.|
|/quotas/read|Получите hello квоты для подписки hello.|

## <a name="microsoftcognitiveservices"></a>Microsoft.CognitiveServices

| Операция | Описание |
|---|---|
|/accounts/read|Считывает учетные записи API.|
|/accounts/write|Записывает учетные записи API.|
|/accounts/delete|Удаляет учетные записи API.|
|/accounts/listKeys/action|Отображает ключи.|
|/accounts/regenerateKey/action|Повторно создает ключ.|
|/accounts/skus/read|Считывает доступные номера SKU для существующего ресурса.|
|/accounts/usages/read|Получение hello использования квоты для существующего ресурса.|
|/Operations/read|Описание операции hello.|

## <a name="microsoftcommerce"></a>Microsoft.Commerce

| Операция | Описание |
|---|---|
|/RateCard/read|Возвращает предоставляют данные, индикатор ресурсов и метаданных и скорости для hello указанной подписки.|
|/UsageAggregates/read|Извлекает данные о потреблении ресурсов Microsoft Azure по подписке. результат Hello содержит статистические выражения данные об использовании, ресурса и подписки, связанные с сведения о определенного интервала времени.|

## <a name="microsoftcompute"></a>Microsoft.Compute;

| Операция | Описание |
|---|---|
|/register/action|Регистрирует подписку в поставщике ресурсов Microsoft.Compute.|
|/restorePointCollections/read|Получение свойств hello коллекции точек восстановления|
|/restorePointCollections/write|Создает новую коллекцию точек восстановления или обновляет существующую.|
|/restorePointCollections/delete|Удаляет hello коллекция точек восстановления, а также содержится точки восстановления|
|/restorePointCollections/restorePoints/read|Получение свойств hello точки восстановления|
|/restorePointCollections/restorePoints/write|Создает точку восстановления.|
|/restorePointCollections/restorePoints/delete|Удаляет точку восстановления hello|
|/restorePointCollections/restorePoints/retrieveSasUris/action|Получение свойств hello точки восстановления, а также идентификаторы URI SAS blob|
|/virtualMachineScaleSets/read|Получение свойств hello набора масштабирования виртуальных машин|
|/virtualMachineScaleSets/write|Создает новый масштабируемый набор виртуальных машин или обновляет существующий.|
|/virtualMachineScaleSets/delete|Удаление набора масштабирования виртуальных машин hello|
|/virtualMachineScaleSets/start/action|Запускает hello экземпляров масштабного набора виртуальных машин hello|
|/virtualMachineScaleSets/powerOff/action|Отключение питания экземпляров масштабного набора виртуальных машин hello hello|
|/virtualMachineScaleSets/restart/action|Перезапуск экземпляров масштабного набора виртуальных машин hello hello|
|/virtualMachineScaleSets/deallocate/action|Отключение питания и освобождает hello вычислительные ресурсы для hello экземпляров масштабного набора виртуальных машин hello |
|/virtualMachineScaleSets/manualUpgrade/action|Обновляет модель toolatest экземпляров масштабного набора виртуальных машин hello вручную|
|/virtualMachineScaleSets/scale/action|Уменьшает или увеличивает количество экземпляров в существующем масштабируемом наборе виртуальных машин.|
|/virtualMachineScaleSets/instanceView/read|Возвращает представление hello экземпляров масштабного набора виртуальных машин hello|
|/virtualMachineScaleSets/skus/read|Списки hello действительных номеров SKU для существующего набора масштабирования виртуальной машины|
|/virtualMachineScaleSets/virtualMachines/read|Извлекает свойства hello виртуальной машины в наборе масштабирования виртуальных Машин|
|/virtualMachineScaleSets/virtualMachines/delete|Удаляет конкретную виртуальную машину в масштабируемом наборе виртуальных машин.|
|/virtualMachineScaleSets/virtualMachines/start/action|Запускает экземпляр виртуальной машины в масштабируемом наборе виртуальных машин.|
|/virtualMachineScaleSets/virtualMachines/powerOff/action|Завершает работу экземпляра виртуальной машины в масштабируемом наборе виртуальных машин.|
|/virtualMachineScaleSets/virtualMachines/restart/action|Перезапускает экземпляр виртуальной машины в масштабируемом наборе виртуальных машин.|
|/virtualMachineScaleSets/virtualMachines/deallocate/action|Отключение питания и освобождает hello вычислительные ресурсы для виртуальной машины в наборе масштабирования виртуальных Машин.|
|/virtualMachineScaleSets/virtualMachines/instanceView/read|Возвращает представление экземпляра hello виртуальной машины в наборе масштабирования виртуальных Машин.|
|/images/read|Получение свойств hello hello изображения|
|/images/write|Создает новый образ или обновляет существующий.|
|/images/delete|Удаляет образ hello|
|/operations/read|Выводит список операций, доступных в поставщике ресурсов Microsoft.Compute.|
|/disks/read|Получение свойств hello диска|
|/disks/write|Создает новый диск или обновляет существующий.|
|/disks/delete|Удаляет hello диска|
|/disks/beginGetAccess/action|Получить универсальный код Ресурса SAS диска hello hello для доступа к BLOB-объект|
|/disks/endGetAccess/action|Отменить URI SAS диска hello hello|
|/snapshots/read|Получение свойств hello моментального снимка|
|/snapshots/write|Создает новый моментальный снимок или обновляет существующий.|
|/snapshots/delete|Удаляет моментальный снимок.|
|/availabilitySets/read|Получение свойств hello группы доступности|
|/availabilitySets/write|Создает новую группу доступности или обновляет существующую.|
|/availabilitySets/delete|Удаляет группу доступности hello|
|/availabilitySets/vmSizes/read|Список доступных размеров для создания или обновления виртуальной машины в наборе доступности hello|
|/virtualMachines/read|Получение свойств hello виртуальной машины.|
|/virtualMachines/write|Создает новую виртуальную машину или обновляет существующую.|
|/virtualMachines/delete|Удаляет виртуальную машину hello|
|/virtualMachines/start/action|Запускает hello виртуальной машины|
|/virtualMachines/powerOff/action|Отключение питания виртуальной машины hello. Обратите внимание, что hello виртуальной машины по-прежнему toobe выставлен счет.|
|/virtualMachines/redeploy/action|Повторно развертывает виртуальную машину.|
|/virtualMachines/restart/action|Перезапускает виртуальную машину hello|
|/virtualMachines/deallocate/action|Отключение питания hello виртуальной машины и освобождение hello вычислительных ресурсов|
|/virtualMachines/generalize/action|Задает состояние tooGeneralized hello виртуальной машины и подготавливает hello виртуальной машины для записи|
|/virtualMachines/capture/action|Захватывает hello виртуальной машины путем копирования виртуальных жестких дисков и создание шаблона, который может быть используется toocreate подобных виртуальных машин|
|/virtualMachines/convertToManagedDisks/action|Преобразует hello BLOB-объектов на основе дисков, дисков toomanaged hello виртуальной машины|
|/virtualMachines/vmSizes/read|Получение списка доступных размеров hello виртуальной машины можно произвести обновление до|
|/virtualMachines/instanceView/read|Возвращает hello подробного состояния среды выполнения виртуальной машины hello и его ресурсы|
|/virtualMachines/extensions/read|Получение свойств hello расширения виртуальной машины|
|/virtualMachines/extensions/write|Создает новое расширение виртуальной машины или обновляет существующее.|
|/virtualMachines/extensions/delete|Удаляет расширение виртуальной машины hello|
|/locations/vmSizes/read|Выводит список доступных размеров виртуальных машин в расположении.|
|/locations/usages/read|Получает ограничения служб и текущих показателях использования для вычислительных ресурсов hello подписки в расположении|
|/locations/operations/read|Возвращает состояние hello асинхронной операции|

## <a name="microsoftcontainerregistry"></a>Microsoft.ContainerRegistry

| Операция | Описание |
|---|---|
|/register/action|Регистрирует подписку hello для поставщика ресурсов реестра контейнера hello и обеспечивает создание контейнера реестры hello.|
|/checknameavailability/read|Проверяет, является ли имя реестра допустимым и неиспользуемым.|
|/registries/read|Возвращает список контейнера реестры Здравствуйте, или возвращает hello свойства для указанного контейнера реестра hello.|
|/registries/write|Создает в реестре контейнеров с hello заданным параметрам или обновить свойства hello или теги для указанного контейнера реестра hello.|
|/registries/delete|Удаляет существующий реестр контейнеров.|
|/registries/listCredentials/action|Список hello учетные данные входа для указанного контейнера реестра hello.|
|/registries/regenerateCredential/action|Повторно создает hello учетные данные входа для указанного контейнера реестра hello.|

## <a name="microsoftcontainerservice"></a>Microsoft.ContainerService

| Операция | Описание |
|---|---|
|/containerServices/subscriptions/read|Get hello указанных служб контейнеров на основе подписки|
|/containerServices/resourceGroups/read|Get hello указанных служб контейнеров на основе группы ресурсов|
|/containerServices/resourceGroups/ContainerServiceName/read|Hello возвращает указанный контейнер службы|
|/containerServices/resourceGroups/ContainerServiceName/write|Помещает или обновления hello указаны службы контейнеров|
|/containerServices/resourceGroups/ContainerServiceName/delete|Hello Удаляет указанный контейнер службы|

## <a name="microsoftcontentmoderator"></a>Microsoft.ContentModerator

| Операция | Описание |
|---|---|
|/updateCommunicationPreference/action|Обновляет параметры связи.|
|/listCommunicationPreference/action|Отображает параметры связи.|
|/applications/read|Операция чтения.|
|/applications/write|Операции записи.|
|/applications/write|Операции записи.|
|/applications/delete|Операция удаления.|
|/applications/listSecrets/action|Выводит список секретов.|
|/applications/listSingleSignOnToken/action|Считывает маркеры единого входа.|
|/operations/read|Считывает операции.|

## <a name="microsoftcustomerinsights"></a>Microsoft.CustomerInsights

| Операция | Описание |
|---|---|
|/hubs/read|Считывает концентратор Azure Customer Insights.|
|/hubs/write|Создает или обновляет концентратор Azure Customer Insights.|
|/hubs/delete|Удаляет концентратор Azure Customer Insights.|
|/hubs/providers/Microsoft.Insights/metricDefinitions/read|Получает доступные метрики hello для ресурсов|
|/hubs/providers/Microsoft.Insights/diagnosticSettings/read|Возвращает приветствия диагностики для ресурса hello|
|/hubs/providers/Microsoft.Insights/diagnosticSettings/write|Создает или обновляет приветствия диагностики для ресурса hello|
|/hubs/providers/Microsoft.Insights/logDefinitions/read|Получает доступные журналы hello для ресурсов|
|/hubs/authorizationPolicies/read|Считывает политику подписанного URL-адреса Azure Customer Insights.|
|/hubs/authorizationPolicies/write|Создает или обновляет политику подписанного URL-адреса Azure Customer Insights.|
|/hubs/authorizationPolicies/delete|Удаляет политику подписанного URL-адреса Azure Customer Insights.|
|/hubs/authorizationPolicies/regeneratePrimaryKey/action|Повторно создает первичный ключ политики подписанного URL-адреса Azure Customer Insights.|
|/hubs/authorizationPolicies/regenerateSecondaryKey/action|Повторно создает вторичный ключ политики подписанного URL-адреса Azure Customer Insights.|
|/hubs/profiles/read|Считывает профиль Azure Customer Insights.|
|/hubs/profiles/write|Записывает профиль Azure Customer Insights.|
|/hubs/kpi/read|Считывает ключевой показатель эффективности Azure Customer Insights.|
|/hubs/kpi/write|Создает или обновляет ключевой показатель эффективности Azure Customer Insights.|
|/hubs/kpi/delete|Удаляет ключевой показатель эффективности Azure Customer Insights.|
|/hubs/views/read|Считывает представление приложений Azure Customer Insights.|
|/hubs/views/write|Создает или обновляет представление приложений Azure Customer Insights.|
|/hubs/views/delete|Удаляет представление приложений Azure Customer Insights.|
|/hubs/interactions/read|Считывает взаимодействие Azure Customer Insights.|
|/hubs/interactions/write|Создает или обновляет взаимодействие Azure Customer Insights.|
|/hubs/roleAssignments/read|Считывает назначение RBAC для Azure Customer Insights.|
|/hubs/roleAssignments/write|Создает или обновляет назначение RBAC для Azure Customer Insights.|
|/hubs/roleAssignments/delete|Удаляет назначение RBAC для Azure Customer Insights.|
|/hubs/connectors/read|Считывает соединитель Azure Customer Insights.|
|/hubs/connectors/write|Создает или обновляет соединитель Azure Customer Insights.|
|/hubs/connectors/delete|Удаляет соединитель Azure Customer Insights.|
|/hubs/connectors/mappings/read|Считывает сопоставление соединителя Azure Customer Insights.|
|/hubs/connectors/mappings/write|Создает или обновляет сопоставление соединителя Azure Customer Insights.|
|/hubs/connectors/mappings/delete|Удаляет сопоставление соединителя Azure Customer Insights.|

## <a name="microsoftdatacatalog"></a>Microsoft.DataCatalog

| Операция | Описание |
|---|---|
|/checkNameAvailability/action|Проверяет доступность имени каталога для клиента.|
|/catalogs/read|Возвращает свойства каталога или каталогов в подписке или группе ресурсов.|
|/catalogs/write|Создает каталог или обновления hello теги и свойства каталога hello.|
|/catalogs/delete|Удаляет каталог hello.|

## <a name="microsoftdatafactory"></a>Microsoft.DataFactory

| Операция | Описание |
|---|---|
|/datafactories/read|Считывает фабрику данных.|
|/datafactories/write|Создает или обновляет фабрику данных.|
|/datafactories/delete|Удаляет фабрику данных.|
|/datafactories/datapipelines/read|Считывает конвейер.|
|/datafactories/datapipelines/delete|Удаляет конвейер.|
|/datafactories/datapipelines/pause/action|Приостанавливает конвейер.|
|/datafactories/datapipelines/resume/action|Возобновляет работу конвейера.|
|/datafactories/datapipelines/update/action|Обновляет конвейер.|
|/datafactories/datapipelines/write|Создает или обновляет конвейер.|
|/datafactories/linkedServices/read|Считывает связанную службу.|
|/datafactories/linkedServices/delete|Удаляет связанную службу.|
|/datafactories/linkedServices/write|Создает или обновляет связанную службу.|
|/datafactories/tables/read|Считывает таблицу.|
|/datafactories/tables/delete|Удаляет таблицу.|
|/datafactories/tables/write|Создает или обновляет таблицу.|

## <a name="microsoftdatalakeanalytics"></a>Microsoft.DataLakeAnalytics

| Операция | Описание |
|---|---|
|/accounts/read|Получение сведений об учетной записи DataLakeAnalytics hello.|
|/accounts/write|Создать или обновить учетную запись DataLakeAnalytics hello.|
|/accounts/delete|Удаление учетной записи DataLakeAnalytics hello.|
|/accounts/firewallRules/read|Возвращает сведения о правиле брандмауэра.|
|/accounts/firewallRules/write|Создает или обновляет правило брандмауэра.|
|/accounts/firewallRules/delete|Удаляет правило брандмауэра.|
|/accounts/storageAccounts/read|Получение связанной учетной записи хранилища для hello DataLakeAnalytics учетной записи.|
|/accounts/storageAccounts/write|Свяжите toohello учетной записи хранилища DataLakeAnalytics учетной записи.|
|/accounts/storageAccounts/delete|Отменить привязку учетной записи хранения из hello DataLakeAnalytics учетной записи.|
|/accounts/storageAccounts/Containers/read|Получить контейнеры в учетной записи хранилища hello|
|/accounts/storageAccounts/Containers/listSasTokens/action|Список токенов SAS для контейнера хранилища hello|
|/accounts/dataLakeStoreAccounts/read|Получение связанной учетной записи DataLakeStore для hello DataLakeAnalytics учетной записи.|
|/accounts/dataLakeStoreAccounts/write|Свяжите toohello учетной записи DataLakeStore DataLakeAnalytics учетной записи.|
|/accounts/dataLakeStoreAccounts/delete|Удалить связь с учетной записью DataLakeStore из hello DataLakeAnalytics учетной записи.|

## <a name="microsoftdatalakestore"></a>Microsoft.DataLakeStore

| Операция | Описание |
|---|---|
|/accounts/read|Возвращает сведения о существовавшей учетной записи Data Lake Store.|
|/accounts/write|Создает новую учетную запись Data Lake Store или обновляет существующую.|
|/accounts/delete|Удаляет существующую учетную запись Data Lake Store.|
|/accounts/firewallRules/read|Возвращает сведения о правиле брандмауэра.|
|/accounts/firewallRules/write|Создает или обновляет правило брандмауэра.|
|/accounts/firewallRules/delete|Удаляет правило брандмауэра.|
|/accounts/trustedIdProviders/read|Возвращает сведения о доверенном поставщике удостоверений.|
|/accounts/trustedIdProviders/write|Создает или обновляет доверенный поставщик удостоверений.|
|/accounts/trustedIdProviders/delete|Удаляет доверенный поставщик удостоверений.|

## <a name="microsoftdevices"></a>Microsoft.Devices

| Операция | Описание |
|---|---|
|/register/action|Зарегистрировать подписку hello для hello центром IOT поставщика и позволяет hello создания ресурса ресурсов центром IOT|
|/checkNameAvailability/Action|Проверяет, доступно ли имя Центра Интернета вещей.|
|/usages/Read|Возвращает данные об использовании подписки для данного поставщика.|
|/operations/Read|Возвращает все операции поставщика ресурсов.|
|/iotHubs/Read|Возвращает ресурсы hello центром IOT|
|/iotHubs/Write|Создает или обновляет ресурс Центра Интернета вещей.|
|/iotHubs/Delete|Удаляет ресурс Центра Интернета вещей.|
|/iotHubs/listkeys/Action|Возвращает все ключи Центра Интернета вещей.|
|/iotHubs/exportDevices/Action|Экспортирует устройства.|
|/iotHubs/importDevices/Action|Импортирует устройства.|
|/IotHubs/metricDefinitions/read|Получает доступные метрики hello для hello службы центром IOT|
|/iotHubs/iotHubKeys/listkeys/Action|Получить ключ с центром IOT для указанного имени hello|
|/iotHubs/iotHubStats/Read|Возвращает статистику Центра Интернета вещей.|
|/iotHubs/quotaMetrics/Read|Возвращает метрики квоты.|
|/iotHubs/eventHubEndpoints/consumerGroups/Write|Создает группу потребителей концентратора событий.|
|/iotHubs/eventHubEndpoints/consumerGroups/Read|Возвращает группы потребителей концентратора событий.|
|/iotHubs/eventHubEndpoints/consumerGroups/Delete|Удаляет группу потребителей концентратора событий.|
|/iotHubs/routing/routes/$testall/Action|Тестирует сообщение с помощью всех существующих маршрутов.|
|/iotHubs/routing/routes/$testnew/Action|Тестирует сообщение с помощью предоставленного тестового маршрута.|
|/IotHubs/diagnosticSettings/read|Возвращает приветствия диагностики для ресурса hello|
|/IotHubs/diagnosticSettings/write|Создает или обновляет приветствия диагностики для ресурса hello|
|/iotHubs/skus/Read|Возвращает допустимые номера SKU Центра Интернета вещей.|
|/iotHubs/jobs/Read|Возвращает сведения о заданиях, отправленных в заданный Центр Интернета вещей.|
|/iotHubs/routingEndpointsHealth/Read|Возвращает hello работоспособности всех конечных точек маршрутизации для центром IOT|

## <a name="microsoftdevtestlab"></a>Microsoft.DevTestLab

| Операция | Описание |
|---|---|
|/Subscription/register/action|Регистрирует подписку hello|
|/labs/delete|Удаляет лаборатории.|
|/labs/read|Считывает лаборатории.|
|/labs/write|Добавляет или изменяет лаборатории.|
|/labs/ListVhds/action|Выводит список образов дисков, доступных для создания пользовательского образа.|
|/labs/GenerateUploadUri/action|Создайте URI для отправки пользовательского диска изображения tooa лаборатории.|
|/labs/CreateEnvironment/action|Создает виртуальные машины в лаборатории.|
|/labs/ClaimAnyVm/action|Утверждения случайных claimable виртуальной машине в лаборатории hello.|
|/labs/ExportResourceUsage/action|Экспорты hello использование ресурсов лаборатории в учетную запись хранилища|
|/labs/users/delete|Удаляет профили пользователей.|
|/labs/users/read|Считывает профили пользователей.|
|/labs/users/write|Добавляет или изменяет профили пользователей.|
|/labs/users/secrets/delete|Удаляет секреты.|
|/labs/users/secrets/read|Считывает секреты.|
|/labs/users/secrets/write|Добавляет или изменяет секреты.|
|/labs/users/environments/delete|Удаляет среды.|
|/labs/users/environments/read|Считывает среды.|
|/labs/users/environments/write|Добавляет или изменяет среды.|
|/labs/users/disks/delete|Удаляет диски.|
|/labs/users/disks/read|Считывает диски.|
|/labs/users/disks/write|Добавляет или изменяет диски.|
|/labs/users/disks/Attach/action|Присоединить и создать аренды hello hello диск toohello виртуальной машины.|
|/labs/users/disks/Detach/action|Присоединение и отсоединение аренды hello разрыв диска hello присоединенного toohello виртуальной машины.|
|/labs/customImages/delete|Удаляет пользовательские образы.|
|/labs/customImages/read|Считывает пользовательские образы.|
|/labs/customImages/write|Добавляет или изменяет пользовательские образы.|
|/labs/serviceRunners/delete|Удаляет средства выполнения служб.|
|/labs/serviceRunners/read|Считывает средства выполнения служб.|
|/labs/serviceRunners/write|Добавляет или изменяет средства выполнения служб.|
|/labs/artifactSources/delete|Удаляет источники артефактов.|
|/labs/artifactSources/read|Считывает источники артефактов.|
|/labs/artifactSources/write|Добавляет или изменяет источники артефактов.|
|/labs/artifactSources/artifacts/read|Считывает артефакты.|
|/labs/artifactSources/artifacts/GenerateArmTemplate/action|Создает шаблон ARM для hello, учитывая артефакта, передает учетной записи хранилища hello необходимые файлы tooa и проверяет созданный hello артефакта.|
|/labs/artifactSources/armTemplates/read|Считывает шаблоны Azure Resource Manager.|
|/labs/costs/read|Считывает затраты.|
|/labs/costs/write|Добавляет или изменяет затраты.|
|/labs/virtualNetworks/delete|Удаляет виртуальные сети.|
|/labs/virtualNetworks/read|Считывает виртуальные сети.|
|/labs/virtualNetworks/write|Добавляет или изменяет виртуальные сети.|
|/labs/formulas/delete|Удаляет формулы.|
|/labs/formulas/read|Считывает формулы.|
|/labs/formulas/write|Добавляет или изменяет формулы.|
|/labs/schedules/delete|Удаляет расписания.|
|/labs/schedules/read|Считывает расписания.|
|/labs/schedules/write|Добавляет или изменяет расписания.|
|/labs/schedules/Execute/action|Выполняет расписание.|
|/labs/schedules/ListApplicable/action|Выводит список всех применимых расписаний.|
|/labs/galleryImages/read|Считывает образы из коллекции.|
|/labs/policySets/EvaluatePolicies/action|Оценивает политику лаборатории.|
|/labs/policySets/policies/delete|Удаляет политики.|
|/labs/policySets/policies/read|Считывает политики.|
|/labs/policySets/policies/write|Добавляет или изменяет политики.|
|/labs/virtualMachines/delete|Удаляет виртуальные машины.|
|/labs/virtualMachines/read|Считывает виртуальные машины.|
|/labs/virtualMachines/write|Добавляет или изменяет виртуальные машины.|
|/labs/virtualMachines/Start/action|Запускает виртуальную машину.|
|/labs/virtualMachines/Stop/action|Остановка виртуальной машины|
|/labs/virtualMachines/ApplyArtifacts/action|Примените машины toovirtual артефакты.|
|/labs/virtualMachines/AddDataDisk/action|Присоедините к машине toovirtual диска новых или существующих данных.|
|/labs/virtualMachines/DetachDataDisk/action|Отсоедините hello указанный диск из виртуальной машины hello.|
|/labs/virtualMachines/Claim/action|Присваивает владение существующей виртуальной машиной.|
|/labs/virtualMachines/ListApplicableSchedules/action|Выводит список всех применимых расписаний.|
|/labs/virtualMachines/schedules/delete|Удаляет расписания.|
|/labs/virtualMachines/schedules/read|Считывает расписания.|
|/labs/virtualMachines/schedules/write|Добавляет или изменяет расписания.|
|/labs/virtualMachines/schedules/Execute/action|Выполняет расписание.|
|/labs/notificationChannels/delete|Удаляет каналы уведомлений.|
|/labs/notificationChannels/read|Считывает каналы уведомлений.|
|/labs/notificationChannels/write|Добавляет или изменяет каналы уведомлений.|
|/labs/notificationChannels/Notify/action|Отправьте уведомления tooprovided канала.|
|/schedules/delete|Удаляет расписания.|
|/schedules/read|Считывает расписания.|
|/schedules/write|Добавляет или изменяет расписания.|
|/schedules/Execute/action|Выполняет расписание.|
|/schedules/Retarget/action|Обновляет идентификатор целевого ресурса расписания.|
|/locations/operations/read|Считывает операции.|

## <a name="microsoftdocumentdb"></a>Microsoft.DocumentDB

| Операция | Описание |
|---|---|
|/databaseAccountNames/read|Проверяет доступность имени.|
|/databaseAccounts/read|Считывает учетную запись базы данных.|
|/databaseAccounts/write|Обновляет учетные записи базы данных.|
|/databaseAccounts/listKeys/action|Выводит список ключей учетной записи базы данных.|
|/databaseAccounts/regenerateKey/action|Выполняет ротацию ключей учетной записи базы данных.|
|/databaseAccounts/listConnectionStrings/action|Получить hello строки подключения для учетной записи базы данных|
|/databaseAccounts/changeResourceGroup/action|Изменяет группу ресурсов для учетной записи базы данных.|
|/databaseAccounts/failoverPriorityChange/action|Изменяет приоритеты отработки отказа для регионов учетной записи базы данных. Это операция перехода на другой ресурс вручную используется tooperform|
|/databaseAccounts/delete|Удаляет учетные записи hello базы данных.|
|/databaseAccounts/metricDefinitions/read|Считывает определения метрик hello учетной записи базы данных.|
|/databaseAccounts/metrics/read|Считывает hello метрики учетной записи базы данных.|
|/databaseAccounts/usages/read|Считывает использования учетной записи базы данных hello.|
|/databaseAccounts/databases/collections/metricDefinitions/read|Считывает hello коллекцию определения метрик.|
|/databaseAccounts/databases/collections/metrics/read|Считывает hello сбора метрик.|
|/databaseAccounts/databases/collections/usages/read|Считывает hello использования коллекции.|
|/databaseAccounts/databases/metricDefinitions/read|Выполняет чтение определения показателей hello базы данных|
|/databaseAccounts/databases/metrics/read|Считывает hello метрики базы данных.|
|/databaseAccounts/databases/usages/read|Считывает hello использования базы данных.|
|/databaseAccounts/readonlykeys/read|Считывает учетной записи базы данных hello ключей только для чтения.|

## <a name="microsoftdomainregistration"></a>Microsoft.DomainRegistration

| Операция | Описание |
|---|---|
|/generateSsoRequest/Action|Создает запрос на вход в центр управления доменами.|
|/validateDomainRegistrationInformation/Action|Проверяет объект покупки домена без его отправки.|
|/checkDomainAvailability/Action|Проверяет, доступен ли домен для приобретения.|
|/listDomainRecommendations/Action|Получить hello список домена рекомендации на основе ключевых слов|
|/register/action|Регистрация поставщика ресурсов доменов Microsoft hello для hello подписки|
|/domains/Read|Получить список доменов hello|
|/domains/Write|Добавляет новый домен или обновляет существующий.|
|/domains/Delete|Удаляет существующий домен.|
|/domains/operationresults/Read|Возвращает операцию домена.|

## <a name="microsoftdynamicslcs"></a>Microsoft.DynamicsLcs

| Операция | Описание |
|---|---|
|/lcsprojects/read|Отобразить проекты службы жизненного цикла Microsoft Dynamics, принадлежащих пользователю tooa|
|/lcsprojects/write|Создание и обновление проектов службы жизненного цикла Microsoft Dynamics, принадлежащих toohello пользователя. Можно обновить только hello имя и описание свойства. не удается обновить после создания Hello подписке и расположении, связанные с проектом hello|
|/lcsprojects/delete|Удаление службы жизненного цикла Microsoft Dynamics проектов, принадлежащих пользователю toohello|
|/lcsprojects/clouddeployments/read|Отображение развертывания Microsoft Dynamics AX 2012 R3 Evaluation в проекте службы жизненного цикла Microsoft Dynamics, принадлежат tooa пользователя|
|/lcsprojects/clouddeployments/write|Создание развертывания Microsoft Dynamics AX 2012 R3 Evaluation в проекте службы жизненного цикла Microsoft Dynamics, принадлежат tooa пользователя. Развертываниями можно управлять на портале управления Azure.|
|/lcsprojects/connectors/read|Чтение соединителей, которые принадлежат tooa службы жизненного цикла Microsoft Dynamics проекта|
|/lcsprojects/connectors/write|Создание и обновление соединителей, которые принадлежат tooa службы жизненного цикла Microsoft Dynamics проекта|

## <a name="microsofteventhub"></a>Microsoft.EventHub

| Операция | Описание |
|---|---|
|/checkNameAvailability/action|Проверяет доступность пространства имен в заданной подписке.|
|/register/action|Регистрирует hello подписку для поставщика ресурсов EventHub hello и разрешает создание ресурсов EventHub hello|
|/namespaces/write|Создает ресурс пространства имен и обновляет его свойства. Теги и состояние hello пространства имен являются hello свойства, которые могут быть обновлены.|
|/namespaces/read|Получить hello список описаний ресурса пространства имен|
|/namespaces/Delete|Удаляет ресурс пространства имен.|
|/namespaces/metricDefinitions/read|Возвращает список описаний ресурсов метрик пространства имен.|
|/namespaces/authorizationRules/read|Получите список hello описание правил авторизации пространства имен.|
|/namespaces/authorizationRules/write|Создает правила авторизации уровня пространства имен и обновляет его свойства. Права доступа к правилам авторизации Hello, hello основные и вторичные ключи могут обновляться.|
|/namespaces/authorizationRules/delete|Удаляет правило авторизации для пространства имен. не удается удалить правило авторизации пространства имен по умолчанию Hello. |
|/namespaces/authorizationRules/listkeys/action|Получение строки подключения hello toohello пространство имен|
|/namespaces/authorizationRules/regenerateKeys/action|Повторное создание hello основных или дополнительных ключей toohello ресурсов|
|/namespaces/eventhubs/write|Создает или обновляет свойства концентратора событий.|
|/namespaces/eventhubs/read|Возвращает список описаний ресурсов концентратора событий.|
|/namespaces/eventhubs/Delete|Операция toodelete ресурсов EventHub|
|/namespaces/eventHubs/consumergroups/write|Создает или обновляет свойства группы потребителей.|
|/namespaces/eventHubs/consumergroups/read|Возвращает список описаний ресурсов группы потребителей.|
|/namespaces/eventHubs/consumergroups/Delete|Операция toodelete ConsumerGroup ресурсов|
|/namespaces/eventhubs/authorizationRules/read| Получить список правил авторизации EventHub hello|
|/namespaces/eventhubs/authorizationRules/write|Создает правила авторизации концентратора событий и обновляет его свойства. Права доступа к правилам авторизации Hello, hello основные и вторичные ключи могут обновляться.|
|/namespaces/eventhubs/authorizationRules/delete|Операция toodelete EventHub правила авторизации|
|/namespaces/eventhubs/authorizationRules/listkeys/action|Получить строку подключения tooEventHub hello|
|/namespaces/eventhubs/authorizationRules/regenerateKeys/action|Повторное создание hello основных или дополнительных ключей toohello ресурсов|
|/namespaces/diagnosticSettings/read|Возвращает список описаний параметров диагностики пространства имен.|
|/namespaces/diagnosticSettings/write|Возвращает список описаний параметров диагностики пространства имен.|
|/namespaces/logDefinitions/read|Возвращает список описаний ресурсов журналов пространства имен.|

## <a name="microsoftfeatures"></a>Microsoft.Features

| Операция | Описание |
|---|---|
|/providers/features/read|Возвращает функцию hello подписки в заданном поставщике ресурсов.|
|/providers/features/register/action|Регистрирует функцию hello для подписки в заданном поставщике ресурсов.|
|/features/read|Возвращает функции hello подписки.|

## <a name="microsofthdinsight"></a>Microsoft.HDInsight

| Операция | Описание |
|---|---|
|/clusters/write|Создает или обновляет кластер HDInsight.|
|/clusters/read|Возвращает сведения о кластере HDInsight.|
|/clusters/delete|Удаляет кластер HDInsight.|
|/clusters/changerdpsetting/action|Изменяет параметры RDP для кластера HDInsight.|
|/clusters/configurations/action|Обновляет конфигурацию кластера HDInsight.|
|/clusters/configurations/read|Возвращает конфигурации кластеров HDInsight.|
|/clusters/roles/resize/action|Изменяет размер кластера HDInsight.|
|/locations/capabilities/read|Возвращает возможности подписки.|
|/locations/checkNameAvailability/read|Проверяет доступность имени.|

## <a name="microsoftimportexport"></a>Microsoft.ImportExport

| Операция | Описание |
|---|---|
|/register/action|Регистрирует hello подписку для поставщика ресурсов импорта и экспорта hello и разрешает hello создание заданий импорта и экспорта.|
|/jobs/write|Создает задание с hello заданным параметрам или обновить свойства hello или теги для указанного задания hello.|
|/jobs/read|Возвращает свойства hello для указанного задания hello или возвращает список заданий hello.|
|/jobs/listBitLockerKeys/action|Возвращает ключи BitLocker hello для указанного задания hello.|
|/jobs/delete|Удаляет существующее задание.|
|/locations/read|Возвращает свойства hello hello указанного расположения или возвращает hello список расположений.|

## <a name="microsoftinsights"></a>Microsoft.Insights

| Операция | Описание |
|---|---|
|/Register/Action|Регистрация поставщика аналитики microsoft hello|
|/AlertRules/Write|Запись tooan правило оповещения конфигурации|
|/AlertRules/Delete|Удаляет конфигурацию правила генерации оповещений.|
|/AlertRules/Read|Считывает конфигурацию правила генерации оповещений.|
|/AlertRules/Activated/Action|Правило генерации оповещений активировано.|
|/AlertRules/Resolved/Action|Правило генерации оповещений разрешено.|
|/AlertRules/Throttled/Action|Правило генерации оповещений отрегулировано.|
|/AlertRules/Incidents/Read|Считывает конфигурацию инцидентов правила генерации оповещений.|
|/MetricDefinitions/Read|Считывает определения метрик.|
|/eventtypes/values/Read|Считывает значения типов событий управления.|
|/eventtypes/digestevents/Read|Считывает дайджест типов событий управления.|
|/Metrics/Read|Считывает метрики.|
|/LogProfiles/Write|Записи tooa журнала профиля конфигурации|
|/LogProfiles/Delete|Удаляет конфигурацию профилей журнала.|
|/LogProfiles/Read|Считывает профили журналов.|
|/AutoscaleSettings/Write|Написание tooan конфигурацию параметров автоматического масштабирования|
|/AutoscaleSettings/Delete|Удаляет конфигурацию параметров автомасштабирования.|
|/AutoscaleSettings/Read|Считывает конфигурацию параметров автомасштабирования.|
|/AutoscaleSettings/Scaleup/Action|Операция автоматического увеличения масштаба.|
|/AutoscaleSettings/Scaledown/Action|Операция автоматического уменьшения масштаба.|
|/AutoscaleSettings/providers/Microsoft.Insights/MetricDefinitions/Read|Считывает определения метрик.|
|/ActivityLogAlerts/Activated/Action|Предупреждение журналов действий триггера hello|
|/DiagnosticSettings/Write|Запись toodiagnostic параметры конфигурации|
|/DiagnosticSettings/Delete|Удаляет конфигурацию параметров диагностики.|
|/DiagnosticSettings/Read|Считывает конфигурацию параметров диагностики.|
|/LogDefinitions/Read|Считывает определения журналов.|
|/ExtendedDiagnosticSettings/Write|Запись tooextended диагностические параметры конфигурации|
|/ExtendedDiagnosticSettings/Delete|Удаляет конфигурацию дополнительных параметров диагностики.|
|/ExtendedDiagnosticSettings/Read|Считывает конфигурацию дополнительных параметров диагностики.|

## <a name="microsoftkeyvault"></a>Microsoft.KeyVault

| Операция | Описание |
|---|---|
|/register/action|Регистрирует подписку.|
|/checkNameAvailability/read|Проверяет, является ли имя Key Vault допустимым и неиспользуемым.|
|/vaults/read|Просмотр свойств hello хранилища ключей|
|/vaults/write|Создание нового ключа хранилища или обновление hello свойства существующего хранилища ключей|
|/vaults/delete|Удаляет Key Vault.|
|/vaults/deploy/action|Разрешает доступ toosecrets в хранилище ключей при развертывании ресурсов Azure|
|/vaults/secrets/read|Просмотр свойств hello секрета, но его значения|
|/vaults/secrets/write|Создайте новое значение секрет или обновление hello существующих секрета|
|/vaults/accessPolicies/write|Обновить существующую политику доступа, объединение или замена или добавьте новое хранилище tooa политики доступа.|
|/deletedVaults/read|Просмотр свойств hello мягкий удаленных хранилищ ключей|
|/locations/operationResults/read|Проверьте результат hello долго выполнения операции|
|/locations/deletedVaults/read|Просмотр свойств hello мягкий удалить хранилище ключей|
|/locations/deletedVaults/purge/action|Очищает обратимо удаленное хранилище Key Vault.|

## <a name="microsoftlogic"></a>Microsoft.Logic

| Операция | Описание |
|---|---|
|/workflows/read|Считывает hello рабочего процесса.|
|/workflows/write|Создает или обновляет рабочий процесс hello.|
|/workflows/delete|Удаляет hello рабочего процесса.|
|/workflows/run/action|Запуск выполнения рабочего процесса hello.|
|/workflows/disable/action|Отключает hello рабочего процесса.|
|/workflows/enable/action|Позволяет процессу hello.|
|/workflows/validate/action|Проверяет hello рабочего процесса.|
|/workflows/move/action|Перемещает рабочего процесса из его существующий идентификатор подписки, группы ресурсов и/или имя tooa другой идентификатор подписки, который группы ресурсов и/или имя.|
|/workflows/listSwagger/action|Возвращает определения swagger hello рабочего процесса.|
|/workflows/regenerateAccessKey/action|Выполняется повторное создание ключа секреты hello доступа.|
|/workflows/listCallbackUrl/action|Возвращает URL-адрес обратного вызова hello рабочего процесса.|
|/workflows/versions/read|Считывает hello версии рабочего процесса.|
|/workflows/versions/triggers/listCallbackUrl/action|Получает URL-адрес обратного вызова hello триггера.|
|/workflows/runs/read|Считывает hello рабочего процесса.|
|/workflows/runs/cancel/action|Отменяет hello выполнения рабочего процесса.|
|/workflows/runs/actions/read|Считывает hello рабочего процесса, выполните действие.|
|/workflows/runs/operations/read|Читает состояние операции выполнения рабочего процесса hello.|
|/workflows/triggers/read|Считывает hello триггера.|
|/workflows/triggers/run/action|Выполняет hello триггера.|
|/workflows/triggers/listCallbackUrl/action|Получает URL-адрес обратного вызова hello триггера.|
|/workflows/triggers/histories/read|Считывает журналы hello триггера.|
|/workflows/triggers/histories/resubmit/action|Повторяет отправку hello триггера рабочего процесса.|
|/workflows/accessKeys/read|Считывает hello ключ доступа.|
|/workflows/accessKeys/write|Создает или обновляет ключ доступа hello.|
|/workflows/accessKeys/delete|Удаляет ключ доступа hello.|
|/workflows/accessKeys/list/action|Список секретов ключа доступа hello.|
|/workflows/accessKeys/regenerate/action|Выполняется повторное создание ключа секреты hello доступа.|
|/locations/workflows/validate/action|Проверяет hello рабочего процесса.|

## <a name="microsoftmachinelearning"></a>Microsoft.MachineLearning

| Операция | Описание |
|---|---|
|/register/action|Регистрирует hello подписки для hello машинного обучения поставщики ресурсов веб-служб и разрешает создание hello веб-служб.|
|/webServices/action|Создает свойства региональной веб-службы для поддерживаемых регионов.|
|/commitmentPlans/read|Считывает план предложения машинного обучения.|
|/commitmentPlans/write|Создает или обновляет план предложения машинного обучения.|
|/commitmentPlans/delete|Удаляет план предложения машинного обучения.|
|/commitmentPlans/join/action|Присоединяет план предложения машинного обучения.|
|/commitmentPlans/commitmentAssociations/read|Считывает связь плана предложения машинного обучения.|
|/commitmentPlans/commitmentAssociations/move/action|Перемещает связь плана предложения машинного обучения.|
|/Workspaces/read|Считывает рабочую область машинного обучения.|
|/Workspaces/write|Создает или обновляет рабочую область машинного обучения.|
|/Workspaces/delete|Удаляет рабочую область машинного обучения.|
|/Workspaces/listworkspacekeys/action|Выводит список ключей для рабочей области машинного обучения.|
|/Workspaces/resyncstoragekeys/action|Повторно синхронизирует ключи учетной записи хранения, настроенной для рабочей области машинного обучения.|
|/webServices/read|Считывает веб-службу машинного обучения.|
|/webServices/write|Создает или обновляет веб-службу машинного обучения.|
|/webServices/delete|Удаляет веб-службу машинного обучения.|

## <a name="microsoftmarketplaceordering"></a>Microsoft.MarketplaceOrdering

| Операция | Описание |
|---|---|
|/agreements/offers/plans/read|Возвращает соглашение для заданного элемента Marketplace.|
|/agreements/offers/plans/sign/action|Подписывает соглашение для заданного элемента Marketplace.|
|/agreements/offers/plans/cancel/action|Отменяет соглашение для заданного элемента Marketplace.|

## <a name="microsoftmedia"></a>Microsoft.Media

| Операция | Описание |
|---|---|
|/mediaservices/read||
|/mediaservices/write||
|/mediaservices/delete||
|/mediaservices/regenerateKey/action||
|/mediaservices/listKeys/action||
|/mediaservices/syncStorageKeys/action||

## <a name="microsoftnetwork"></a>Microsoft.Network.

| Операция | Описание |
|---|---|
|/register/action|Регистрирует подписку hello|
|/unregister/action|Отменяет регистрацию подписки hello|
|/checkTrafficManagerNameAvailability/action|Проверяет доступность имени DNS диспетчера трафика относительно hello.|
|/dnszones/read|Получение зоны DNS hello, в формате JSON. Hello свойства зоны включают теги, etag, numberOfRecordSets и maxNumberOfRecordSets. Обратите внимание, что эта команда не извлекает наборы записей hello, содержащихся в зоне hello.|
|/dnszones/write|Создает или обновляет зону DNS в группе ресурсов.  Используется tooupdate hello тегов в ресурсе зоны DNS. Обратите внимание, что эта команда не может быть используется toocreate или обновления наборов записей в зоне hello.|
|/dnszones/delete|Удалите зону DNS hello, в формате JSON. Hello свойства зоны включают теги, etag, numberOfRecordSets и maxNumberOfRecordSets.|
|/dnszones/MX/read|Получение набора записей hello типа «MX» в формате JSON. Hello набор записей содержит список записей, а также hello срок ЖИЗНИ, теги и etag.|
|/dnszones/MX/write|Создает или обновляет набора записей типа MX в зоне DNS. Привет, прописанных заменит hello текущие записи в наборе записей hello.|
|/dnszones/MX/delete|Удаление набора записей hello с указанным именем и типом «MX» из зоны DNS.|
|/dnszones/NS/read|Возвращает набор записей DNS типа NS.|
|/dnszones/NS/write|Создает или обновляет набор записей DNS типа NS.|
|/dnszones/NS/delete|Удаляет hello DNS набора записей типа NS|
|/dnszones/AAAA/read|Получение набора записей hello типа «AAAA» в формате JSON. Hello набор записей содержит список записей, а также hello срок ЖИЗНИ, теги и etag.|
|/dnszones/AAAA/write|Создает или обновляет набора записей типа AAAA в зоне DNS. Привет, прописанных заменит hello текущие записи в наборе записей hello.|
|/dnszones/AAAA/delete|Удаление набора записей hello с указанным именем и типом «AAAA» из зоны DNS.|
|/dnszones/CNAME/read|Получение набора записей hello типа «CNAME» в формате JSON. набор записей Hello содержит hello срок ЖИЗНИ, теги и etag.|
|/dnszones/CNAME/write|Создает или обновляет набора записей типа CNAME в зоне DNS. Привет, прописанных заменит hello текущие записи в наборе записей hello.|
|/dnszones/CNAME/delete|Удаление набора записей hello с указанным именем и типом «CNAME» из зоны DNS.|
|/dnszones/SOA/read|Возвращает набор записей DNS типа SOA.|
|/dnszones/SOA/write|Создает или обновляет набор записей DNS типа SOA.|
|/dnszones/SRV/read|Получение набора записей hello типа «SRV» в формате JSON. Hello набор записей содержит список записей, а также hello срок ЖИЗНИ, теги и etag.|
|/dnszones/SRV/write|Создает или обновляет набор записей типа SRV.|
|/dnszones/SRV/delete|Удаление набора записей hello с указанным именем и типом «SRV» из зоны DNS.|
|/dnszones/PTR/read|Получите hello набор записей типа «Указатель», в формате JSON. Hello набор записей содержит список записей, а также hello срок ЖИЗНИ, теги и etag.|
|/dnszones/PTR/write|Создает или обновляет набора записей типа PTR в зоне DNS. Привет, прописанных заменит hello текущие записи в наборе записей hello.|
|/dnszones/PTR/delete|Удаление набора записей hello с указанным именем и типом «PTR» из зоны DNS.|
|/dnszones/A/read|Получите hello набор записей типа «A» в формате JSON. Hello набор записей содержит список записей, а также hello срок ЖИЗНИ, теги и etag.|
|/dnszones/A/write|Создает или обновляет набора записей типа A в зоне DNS. Привет, прописанных заменит hello текущие записи в наборе записей hello.|
|/dnszones/A/delete|Удаление набора записей hello с указанным именем и типом «A» из зоны DNS.|
|/dnszones/TXT/read|Получение набора записей hello типа «TXT», в формате JSON. Hello набор записей содержит список записей, а также hello срок ЖИЗНИ, теги и etag.|
|/dnszones/TXT/write|Создает или обновляет набора записей типа TXT в зоне DNS. Привет, прописанных заменит hello текущие записи в наборе записей hello.|
|/dnszones/TXT/delete|Удаление набора записей hello с указанным именем и типом «TXT» из зоны DNS.|
|/dnszones/recordsets/read|Возвращает набор записей DNS разного типа.|
|/networkInterfaces/read|Возвращает определение сетевого интерфейса. |
|/networkInterfaces/write|Создает новый сетевой интерфейс или обновляет существующий. |
|/networkInterfaces/join/action|Присоединяет tooa сетевого интерфейса виртуальной машины|
|/networkInterfaces/delete|Удаляет сетевой интерфейс.|
|/networkInterfaces/effectiveRouteTable/action|Получение таблицы маршрутов, настроенный в сетевом интерфейсе из hello виртуальной машины|
|/networkInterfaces/effectiveNetworkSecurityGroups/action|Получение группы безопасности сети настроенного на сетевой интерфейс из hello виртуальной машины|
|/networkInterfaces/loadBalancers/read|Возвращает все подсистемы балансировки нагрузки hello, hello сетевой интерфейс является частью|
|/networkInterfaces/ipconfigurations/read|Возвращает определение IP-конфигурации сетевого интерфейса. |
|/publicIPAddresses/read|Возвращает определение общедоступного IP-адреса.|
|/publicIPAddresses/write|Создает новый общедоступный IP-адрес или обновляет существующий. |
|/publicIPAddresses/delete|Удаляет общедоступный IP-адрес.|
|/publicIPAddresses/join/action|Присоединяет общедоступный IP-адрес.|
|/routeFilters/read|Возвращает определение фильтра маршрутов.|
|/routeFilters/join/action|Присоединяет фильтр маршрутов.|
|/routeFilters/delete|Удаляет определение фильтра маршрутов.|
|/routeFilters/write|Создает новый фильтр маршрутов или обновляет существующий.|
|/routeFilters/rules/read|Возвращает определение правила фильтра маршрутов.|
|/routeFilters/rules/write|Создает новое правило фильтра маршрутов или обновляет существующее.|
|/routeFilters/rules/delete|Удаляет определение правила фильтра маршрутов.|
|/networkWatchers/read|Получить определение Наблюдатель сети hello|
|/networkWatchers/write|Создает новый Наблюдатель за сетями или обновляет существующий.|
|/networkWatchers/delete|Удаляет Наблюдатель за сетями.|
|/networkWatchers/configureFlowLog/action|Настраивает ведение журнала потоков для целевого ресурса.|
|/networkWatchers/ipFlowVerify/action|Возвращает ли пакет приветствия разрешен или запрещен tooor из конкретного места назначения.|
|/networkWatchers/nextHop/action|Указанный целевой объект и конечный IP-адрес возвращают тип следующего прыжка hello и далее надеемся, что IP-адрес.|
|/networkWatchers/queryFlowLogStatus/action|Возвращает состояние hello потока, ведение журнала для ресурса.|
|/networkWatchers/queryTroubleshootResult/action|Возвращает hello, устранение неполадок результат hello ранее не выполнялась или в настоящее время запуска операции устранения неполадок.|
|/networkWatchers/securityGroupView/action|Просмотр настройки hello и действующие сетевой безопасности группы правил, применяемых на виртуальной Машине.|
|/networkWatchers/topology/action|Возвращает представление уровня сети для ресурсов и их связей в группе ресурсов.|
|/networkWatchers/troubleshoot/action|Начинает устранение неполадок сетевого ресурса в Azure.|
|/networkWatchers/packetCaptures/queryStatus/action|Возвращает сведения о свойствах и состоянии ресурса записи пакетов.|
|/networkWatchers/packetCaptures/stop/action|Остановите hello для запуска сеанса записи пакета.|
|/networkWatchers/packetCaptures/read|Получить определение захват пакетов hello|
|/networkWatchers/packetCaptures/write|Создает запись пакетов.|
|/networkWatchers/packetCaptures/delete|Удаляет запись пакетов.|
|/loadBalancers/read|Возвращает определение подсистемы балансировки нагрузки.|
|/loadBalancers/write|Создает новую подсистему балансировки нагрузки или обновляет существующую.|
|/loadBalancers/delete|Удаляет подсистему балансировки нагрузки.|
|/loadBalancers/networkInterfaces/read|Возвращает ссылки на tooall hello сетевые интерфейсы в рамках подсистемы балансировки нагрузки|
|/loadBalancers/loadBalancingRules/read|Возвращает определение правила подсистемы балансировки нагрузки.|
|/loadBalancers/backendAddressPools/read|Возвращает определение внутреннего пула адресов подсистемы балансировки нагрузки.|
|/loadBalancers/backendAddressPools/join/action|Выполняет присоединение к внутреннему пулу адресов подсистемы балансировки нагрузки.|
|/loadBalancers/inboundNatPools/read|Возвращает определение пула входящих подключений NAT подсистемы балансировки нагрузки.|
|/loadBalancers/inboundNatPools/join/action|Присоединяет пул входящих подключений NAT подсистемы балансировки нагрузки.|
|/loadBalancers/inboundNatRules/read|Возвращает определение правила NAT для входящего трафика подсистемы балансировки нагрузки.|
|/loadBalancers/inboundNatRules/write|Создает новое правило NAT для входящего трафика подсистемы балансировки нагрузки или обновляет существующее.|
|/loadBalancers/inboundNatRules/delete|Удаляет правило NAT для входящего трафика подсистемы балансировки нагрузки.|
|/loadBalancers/inboundNatRules/join/action|Присоединяет правило NAT для входящего трафика подсистемы балансировки нагрузки.|
|/loadBalancers/outboundNatRules/read|Возвращает определение правила пула исходящих подключений NAT подсистемы балансировки нагрузки.|
|/loadBalancers/probes/read|Возвращает пробу подсистемы балансировки нагрузки.|
|/loadBalancers/virtualMachines/read|Возвращает ссылки на tooall hello виртуальных машин в группе балансировки нагрузки|
|/loadBalancers/frontendIPConfigurations/read|Возвращает определение внешней IP-конфигурации подсистемы балансировки нагрузки.|
|/trafficManagerGeographicHierarchies/read|Возвращает hello иерархии географическая диспетчера трафика, содержащий областей, которые могут быть использованы с hello метод маршрутизации трафика географической|
|/bgpServiceCommunities/read|Возвращает сообщества службы BGP.|
|/applicationGatewayAvailableWafRuleSets/read|Возвращает доступные наборы правил WAF шлюза приложений.|
|/virtualNetworks/read|Получить определение виртуальной сети hello|
|/virtualNetworks/write|Создает новую виртуальную сеть или обновляет существующую.|
|/virtualNetworks/delete|Удаляет виртуальную сеть.|
|/virtualNetworks/peer/action|Создает пиринг между виртуальными сетями.|
|/virtualNetworks/virtualNetworkPeerings/read|Возвращает определение пиринга виртуальной сети.|
|/virtualNetworks/virtualNetworkPeerings/write|Создает новый пиринг виртуальной сети или обновляет существующий.|
|/virtualNetworks/virtualNetworkPeerings/delete|Удаляет пиринг виртуальной сети.|
|/virtualNetworks/subnets/read|Возвращает определение подсети виртуальной сети.|
|/virtualNetworks/subnets/write|Создает новую подсеть пиринг виртуальной сети или обновляет существующую.|
|/virtualNetworks/subnets/delete|Удаляет подсеть виртуальной сети.|
|/virtualNetworks/subnets/join/action|Присоединяет виртуальную сеть.|
|/virtualNetworks/subnets/joinViaServiceTunnel/action|Присоединяет ресурсов, такие как учетная запись хранения или SQL базы данных включено туннелирование службы подсети tooa.|
|/virtualNetworks/subnets/virtualMachines/read|Возвращает ссылки на tooall hello виртуальные машины в подсети виртуальной сети|
|/virtualNetworks/checkIpAddressAvailability/read|Проверьте, если IP-адрес находится в указанной виртуальной сети hello|
|/virtualNetworks/virtualMachines/read|Возвращает ссылки на tooall hello виртуальных машин в виртуальной сети|
|/expressRouteServiceProviders/read|Возвращает поставщики службы ExpressRoute.|
|/dnsoperationresults/read|Возвращает результаты операции DNS.|
|/localnetworkgateways/read|Возвращает шлюз локальной сети.|
|/localnetworkgateways/write|Создает новый шлюз локальной сети или обновляет существующий.|
|/localnetworkgateways/delete|Удаляет шлюз локальной сети.|
|/trafficManagerProfiles/read|Получение конфигурации профиля диспетчера трафика hello. Сюда входят параметры DNS, параметры маршрутизации трафика, параметры мониторинга конечной точки и hello список конечных точек, маршрутизируемых этим профилем диспетчера трафика.|
|/trafficManagerProfiles/write|Создание профиля диспетчера трафика или изменение конфигурации hello существующего профиля диспетчера трафика. Сюда входит включение или отключение профиля и изменение параметров DNS, параметров маршрутизации трафика или параметров мониторинга конечных точек. Конечных точек, маршрутизируемых hello профиля диспетчера трафика можно добавить, удалить, включить или отключить.|
|/trafficManagerProfiles/delete|Удаление профиля диспетчера трафика hello. Все параметры, связанные с hello профиля диспетчера трафика, будут потеряны и больше не может быть hello профиль используется tooroute трафика.|
|/dnsoperationstatuses/read|Возвращает состояние операции DNS. |
|/operations/read|Возвращает доступные операции.|
|/expressRouteCircuits/read|Возвращает канал ExpressRoute.|
|/expressRouteCircuits/write|Создает новый канал ExpressRoute или обновляет существующий.|
|/expressRouteCircuits/delete|Удаляет канал ExpressRoute.|
|/expressRouteCircuits/stats/read|Возвращает статистику канала ExpressRoute.|
|/expressRouteCircuits/peerings/read|Возвращает пиринг канала ExpressRoute.|
|/expressRouteCircuits/peerings/write|Создает новый пиринг канала ExpressRoute или обновляет существующий.|
|/expressRouteCircuits/peerings/delete|Удаляет пиринг канала ExpressRoute.|
|/expressRouteCircuits/peerings/arpTables/action|Возвращает таблицу ARP для пиринга канала ExpressRoute.|
|/expressRouteCircuits/peerings/routeTables/action|Возвращает таблицу маршрутов для пиринга канала ExpressRoute.|
|/expressRouteCircuits/peerings/<br>routeTablesSummary/action|Возвращает сводку по таблице маршрутов для пиринга канала ExpressRoute.|
|/expressRouteCircuits/peerings/stats/read|Возвращает статистику пиринга канала ExpressRoute.|
|/expressRouteCircuits/authorizations/read|Возвращает данные авторизации канала ExpressRoute.|
|/expressRouteCircuits/authorizations/write|Создает новые данные авторизации канала ExpressRoute или обновляет существующие.|
|/expressRouteCircuits/authorizations/delete|Удаляет данные авторизации канала ExpressRoute.|
|/connections/read|Возвращает подключение шлюза виртуальной сети.|
|/connections/write|Создает новое подключение шлюза виртуальной сети или обновляет существующее.|
|/connections/delete|Удаляет подключение шлюза виртуальной сети.|
|/connections/sharedKey/read|Возвращает общий ключ для подключения шлюза виртуальной сети.|
|/connections/sharedKey/write|Создает новый общий ключ для подключения шлюза виртуальной сети или обновляет существующий.|
|/networkSecurityGroups/read|Возвращает определение группы безопасности сети.|
|/networkSecurityGroups/write|Создает новую группу безопасности сети или обновляет существующую.|
|/networkSecurityGroups/delete|Удаляет группу безопасности сети.|
|/networkSecurityGroups/join/action|Присоединяет группу безопасности сети.|
|/networkSecurityGroups/defaultSecurityRules/read|Возвращает определение правила безопасности по умолчанию.|
|/networkSecurityGroups/securityRules/read|Возвращает определение правила безопасности.|
|/networkSecurityGroups/securityRules/write|Создает новое правило безопасности или обновляет существующее.|
|/networkSecurityGroups/securityRules/delete|Удаляет правило безопасности.|
|/applicationGateways/read|Возвращает шлюз приложений.|
|/applicationGateways/write|Создает новый шлюз приложений или обновляет существующий.|
|/applicationGateways/delete|Удаляет шлюз приложений.|
|/applicationGateways/backendhealth/action|Возвращает сведения о работоспособности серверной части шлюза приложений.|
|/applicationGateways/start/action|Запускает шлюз приложений.|
|/applicationGateways/stop/action|Останавливает шлюз приложений.|
|/applicationGateways/backendAddressPools/join/action|Выполняет присоединение к внутреннему пулу адресов шлюза приложений.|
|/routeTables/read|Возвращает определение таблицы маршрутов.|
|/routeTables/write|Создает новую таблицу маршрутов или обновляет существующую.|
|/routeTables/delete|Удаляет определение таблицы маршрутов.|
|/routeTables/join/action|Присоединяет таблицу маршрутов.|
|/routeTables/routes/read|Возвращает определение маршрута.|
|/routeTables/routes/write|Создает новый маршрут или обновляет существующий.|
|/routeTables/routes/delete|Удаляет определение маршрута.|
|/locations/operationResults/read|Возвращает результат асинхронной операции POST или DELETE.|
|/locations/checkDnsNameAvailability/read|Проверяет, доступен метка dns на hello определенное место|
|/locations/usages/read|Возвращает показатели использования ресурсов hello|
|/locations/operations/read|Возвращает ресурс операции, представляющий состояние асинхронной операции.|

## <a name="microsoftnotificationhubs"></a>Microsoft.NotificationHubs

| Операция | Описание |
|---|---|
|/register/action|Регистрирует hello подписку для поставщика ресурсов NotifciationHubs hello и обеспечивает создание hello и Notificationhub|
|/CheckNamespaceAvailability/action|Проверяет, доступно ли имя данного ресурса пространства имен в пределах hello концентратора уведомлений службы.|
|/Namespaces/write|Создает ресурс пространства имен и обновляет его свойства. Теги и состояние hello пространства имен являются hello свойства, которые могут быть обновлены.|
|/Namespaces/read|Получить hello список описаний ресурса пространства имен|
|/Namespaces/Delete|Удаляет ресурс пространства имен.|
|/Namespaces/authorizationRules/action|Получите список hello описание правил авторизации пространства имен.|
|/Namespaces/CheckNotificationHubAvailability/action|Проверяет, доступно ли заданное имя центра уведомлений в пространстве имен.|
|/Namespaces/authorizationRules/write|Создает правила авторизации уровня пространства имен и обновляет его свойства. Права доступа к правилам авторизации Hello, hello основные и вторичные ключи могут обновляться.|
|/Namespaces/authorizationRules/read|Получите список hello описание правил авторизации пространства имен.|
|/Namespaces/authorizationRules/delete|Удаляет правило авторизации для пространства имен. не удается удалить правило авторизации пространства имен по умолчанию Hello. |
|/Namespaces/authorizationRules/listkeys/action|Получение строки подключения hello toohello пространство имен|
|/Namespaces/authorizationRules/regenerateKeys/action|Пространство имен авторизации правило повторно создать первичный и SecondaryKey, hello укажите ключ, который требуется повторно toobe|
|/Namespaces/NotificationHubs/write|Создает центр уведомлений и обновляет его свойства. К этим свойствам в основном относятся учетные данные PNS. Правила авторизации и срок жизни.|
|/Namespaces/NotificationHubs/read|Возвращает список описаний ресурсов центра уведомлений.|
|/Namespaces/NotificationHubs/Delete|Удаляет ресурс центра уведомлений.|
|/Namespaces/NotificationHubs/authorizationRules/action|Получить список hello правила авторизации концентратора уведомлений|
|/Namespaces/NotificationHubs/pnsCredentials/action|Возвращает все учетные данные PNS центра уведомлений. Сюда входят учетные данные WNS, MPNS, APNS, GCM и Baidu.|
|/Namespaces/NotificationHubs/debugSend/action|Отправляет тестовое push-уведомление.|
|/Namespaces/NotificationHubs/metricDefinitions/read|Возвращает список описаний ресурсов метрик пространства имен.|
|/Namespaces/NotificationHubs/<br>authorizationRules/write|Создает правила авторизации центра уведомлений и обновляет его свойства. Права доступа к правилам авторизации Hello, hello основные и вторичные ключи могут обновляться.|
|/Namespaces/NotificationHubs/<br>authorizationRules/read|Получить список hello правила авторизации концентратора уведомлений|
|/Namespaces/NotificationHubs/<br>authorizationRules/delete|Удаляет правила авторизации центра уведомлений.|
|/Namespaces/NotificationHubs/<br>authorizationRules/listkeys/action|Получить строку подключения hello toohello концентратора уведомлений|
|/Namespaces/NotificationHubs/<br>authorizationRules/regenerateKeys/action|Заново уведомлений концентратора авторизации правило повторно создать первичный и SecondaryKey, hello укажите ключ, который должен toobe|

## <a name="microsoftoperationalinsights"></a>Microsoft.OperationalInsights

| Операция | Описание |
|---|---|
|/register/action|Регистрация поставщика ресурсов tooa подписки.|
|/linkTargets/read|Выводит список существующих учетных записей, которые не связаны с подпиской Azure. toolink этой рабочей области tooa подписки Azure, используйте идентификатор клиента возвращаемые этой операцией в свойство идентификатора клиента hello hello операции создать рабочую область.|
|/workspaces/write|Создает новую рабочую область или существующей рабочей области tooan ссылки, предоставляя идентификатор клиента hello из hello существующую рабочую область.|
|/workspaces/read|Возвращает существующую рабочую область.|
|/workspaces/delete|Удаляет рабочую область. Если был связан hello рабочей tooan существующей рабочей области во время создания затем hello рабочей области, которое было связанного toois не удаляется.|
|/workspaces/generateregistrationcertificate/action|Приводит к возникновению ошибки регистрации сертификатов для рабочей области hello. Этот сертификат является рабочей toohello tooconnect используется Microsoft System Center Operation Manager.|
|/workspaces/sharedKeys/action|Извлекает hello общие ключи для hello рабочей области. Эти ключи, используемые tooconnect Microsoft агенты toohello рабочая область оперативной аналитики.|
|/workspaces/search/action|Выполняет поисковый запрос.|
|/workspaces/datasources/read|Возвращает источники данных в рабочей области.|
|/workspaces/datasources/write|Создает или обновляет источники данных в рабочей области.|
|/workspaces/datasources/delete|Удаляет источники данных в рабочей области.|
|/workspaces/managementGroups/read|Возвращает имена hello и метаданные для рабочей toothis подключенных групп управления System Center Operations Manager.|
|/workspaces/schema/read|Возвращает схему поиска hello для hello рабочей области.  Схема поиска включает hello предоставляется полей и их типы.|
|/workspaces/usages/read|Возвращает данные об использовании для рабочей области, включая hello объем данных, считываемых hello рабочей области.|
|/workspaces/intelligencepacks/read|Перечислены все пакеты аналитики, которые являются видимыми для заданной worksapce, а также пакет hello включена или отключена для данной рабочей области.|
|/workspaces/intelligencepacks/enable/action|Включает пакет аналитики для заданной рабочей области.|
|/workspaces/intelligencepacks/disable/action|Отключает пакет аналитики для заданной рабочей области.|
|/workspaces/sharedKeys/read|Извлекает hello общие ключи для hello рабочей области. Эти ключи, используемые tooconnect Microsoft агенты toohello рабочая область оперативной аналитики.|
|/workspaces/savedSearches/read|Возвращает сохраненный поисковый запрос.|
|/workspaces/savedSearches/write|Создает сохраненный поисковый запрос.|
|/workspaces/savedSearches/delete|Удаляет сохраненный поисковый запрос.|
|/workspaces/storageinsightconfigs/write|Создает конфигурацию учетной записи хранения. Эти конфигурации, используемые toopull данных из расположения в существующую учетную запись хранения.|
|/workspaces/storageinsightconfigs/read|Возвращает конфигурацию хранилища.|
|/workspaces/storageinsightconfigs/delete|Удаляет конфигурацию хранилища. Это остановит оперативной аналитики Microsoft считывать данные из учетной записи хранения hello.|
|/workspaces/configurationScopes/read|Возвращает область конфигурации.|
|/workspaces/configurationScopes/write|Задает область конфигурации.|
|/workspaces/configurationScopes/delete|Удаляет область конфигурации.|

## <a name="microsoftoperationsmanagement"></a>Microsoft.OperationsManagement

| Операция | Описание |
|---|---|
|/register/action|Регистрация поставщика ресурсов tooa подписки.|
|/solutions/write|Создает решение OMS.|
|/solutions/read|Возвращает существующее решение OMS.|
|/solutions/delete|Удаляет существующее решение OMS.|

## <a name="microsoftrecoveryservices"></a>Microsoft.RecoveryServices

| Операция | Описание |
|---|---|
|/Vaults/backupJobsExport/action|Экспортирует задания.|
|/Vaults/write|Создает операцию создания хранилища, которая создает ресурс Azure типа "хранилище".|
|/Vaults/read|Hello получить хранилище операция возвращает объект, представляющий ресурс Azure типа «vault» hello|
|/Vaults/delete|Операция удаления Hello удалить хранилище hello указанный ресурс Azure типа «vault»|
|/Vaults/refreshContainers/read|Обновляет список контейнеров hello|
|/Vaults/backupJobsExport/operationResults/read|Здравствуйте, возвращает результат экспорта операции задания.|
|/Vaults/backupOperationResults/read|Возвращает результат операции архивации для хранилища служб восстановления.|
|/Vaults/monitoringAlerts/read|Получает хранилище служб восстановления hello hello предупреждения.|
|/Vaults/monitoringAlerts/{уникальный_ИД_оповещения}/read|Возвращает сведения о hello hello предупреждения.|
|/Vaults/backupSecurityPIN/read|Возвращает данные ПИН-кода безопасности для хранилища служб восстановления.|
|/vaults/replicationEvents/read|Считывает события.|
|/Vaults/backupProtectableItems/read|Возвращает список всех защищаемых элементов.|
|/vaults/replicationFabrics/read|Считывает структуры.|
|/vaults/replicationFabrics/write|Создает или обновляет структуры.|
|/vaults/replicationFabrics/remove/action|Удаляет структуру.|
|/vaults/replicationFabrics/checkConsistency/action|Проверяет согласованность hello структуры|
|/vaults/replicationFabrics/delete|Удаляет структуры.|
|/vaults/replicationFabrics/renewcertificate/action||
|/vaults/replicationFabrics/deployProcessServerImage/action|Развертывает образ сервера обработки.|
|/vaults/replicationFabrics/reassociateGateway/action|Повторно задает связь шлюза.|
|/vaults/replicationFabrics/replicationRecoveryServicesProviders/<br>read|Считывает поставщики служб восстановления.|
|/vaults/replicationFabrics/replicationRecoveryServicesProviders/<br>remove/action|Удаляет поставщик служб восстановления.|
|/vaults/replicationFabrics/replicationRecoveryServicesProviders/<br>удалить|Удаляет поставщики служб восстановления.|
|/vaults/replicationFabrics/replicationRecoveryServicesProviders/<br>refreshProvider/action|Обновляет поставщик.|
|/vaults/replicationFabrics/replicationStorageClassifications/read|Считывает классификации хранилища.|
|/vaults/replicationFabrics/replicationStorageClassifications/<br>replicationStorageClassificationMappings/read|Считывает сопоставления классификаций хранилища.|
|/vaults/replicationFabrics/replicationStorageClassifications/<br>replicationStorageClassificationMappings/write|Создает или обновляет сопоставления классификаций хранилища.|
|/vaults/replicationFabrics/replicationStorageClassifications/<br>replicationStorageClassificationMappings/delete|Удаляет сопоставления классификаций хранилища.|
|/vaults/replicationFabrics/replicationvCenters/read|Считывает задания.|
|/vaults/replicationFabrics/replicationvCenters/write|Создает или обновляет задания.|
|/vaults/replicationFabrics/replicationvCenters/delete|Удаляет задания.|
|/vaults/replicationFabrics/replicationNetworks/read|Считывает сети.|
|/vaults/replicationFabrics/replicationNetworks/<br>replicationNetworkMappings/read|Считывает сетевые сопоставления.|
|/vaults/replicationFabrics/replicationNetworks/<br>/write|Создает или обновляет сетевые сопоставления.|
|/vaults/replicationFabrics/replicationNetworks/<br>replicationNetworkMappings/delete|Удаляет сетевые сопоставления.|
|/vaults/replicationFabrics/replicationProtectionContainers/<br>read|Считывает контейнеры защиты.|
|/vaults/replicationFabrics/replicationProtectionContainers/<br>discoverProtectableItem/action|Обнаруживает защищаемый элемент.|
|/vaults/replicationFabrics/replicationProtectionContainers/<br>write|Создает или обновляет контейнеры защиты.|
|/vaults/replicationFabrics/replicationProtectionContainers/<br>remove/action|Удаляет контейнер защиты.|
|/vaults/replicationFabrics/replicationProtectionContainers/<br>switchprotection/action|Переключает контейнер защиты.|
|/vaults/replicationFabrics/replicationProtectionContainers/<br>replicationProtectableItems/read|Считывает защищаемые элементы.|
|/vaults/replicationFabrics/replicationProtectionContainers/<br>replicationProtectionContainerMappings/read|Считывает сопоставления контейнера защиты.|
|/vaults/replicationFabrics/replicationProtectionContainers/<br>replicationProtectionContainerMappings/write|Создает или обновляет сопоставления контейнера защиты.|
|/vaults/replicationFabrics/replicationProtectionContainers/<br>replicationProtectionContainerMappings/remove/action|Удаляет сопоставление контейнера защиты.|
|/vaults/replicationFabrics/replicationProtectionContainers/<br>replicationProtectionContainerMappings/delete|Удаляет сопоставления контейнера защиты.|
|/vaults/replicationFabrics/replicationProtectionContainers/<br>replicationProtectedItems/read|Считывает защищенные элементы.|
|/vaults/replicationFabrics/replicationProtectionContainers/<br>replicationProtectedItems/write|Создает или обновляет защищенные элементы.|
|/vaults/replicationFabrics/replicationProtectionContainers/<br>replicationProtectedItems/delete|Удаляет защищенные элементы.|
|/vaults/replicationFabrics/replicationProtectionContainers/<br>replicationProtectedItems/remove/action|Удаляет защищенный элемент.|
|/vaults/replicationFabrics/replicationProtectionContainers/<br>replicationProtectedItems/plannedFailover/action|Выполняет плановую отработку отказа.|
|/vaults/replicationFabrics/replicationProtectionContainers/<br>replicationProtectedItems/unplannedFailover/action|Отработка отказа|
|/vaults/replicationFabrics/replicationProtectionContainers/<br>replicationProtectedItems/testFailover/action|Тестирование отработки отказа|
|/vaults/replicationFabrics/replicationProtectionContainers/<br>replicationProtectedItems/testFailoverCleanup/action|Тестирует очистку отработки отказа.|
|/vaults/replicationFabrics/replicationProtectionContainers/<br>replicationProtectedItems/failoverCommit/action|Выполняет отработку отказа с фиксацией.|
|/vaults/replicationFabrics/replicationProtectionContainers/<br>replicationProtectedItems/reProtect/action|Повторно защищает защищенный элемент.|
|/vaults/replicationFabrics/replicationProtectionContainers/<br>replicationProtectedItems/updateMobilityService/action|Обновляет службу Mobility Service.|
|/vaults/replicationFabrics/replicationProtectionContainers/<br>replicationProtectedItems/repairReplication/action|Исправляет репликацию.|
|/vaults/replicationFabrics/replicationProtectionContainers/<br>replicationProtectedItems/applyRecoveryPoint/action|Применяет точку восстановления.|
|/vaults/replicationFabrics/replicationProtectionContainers/<br>replicationProtectedItems/recoveryPoints/read|Считывает точки восстановления для репликации.|
|/vaults/replicationPolicies/read|Считывает политики.|
|/vaults/replicationPolicies/write|Создает или обновляет политики.|
|/vaults/replicationPolicies/delete|Удаляет политики.|
|/vaults/replicationRecoveryPlans/read|Считывает планы восстановления.|
|/vaults/replicationRecoveryPlans/write|Создает или обновляет планы восстановления.|
|/vaults/replicationRecoveryPlans/delete|Удаляет планы восстановления.|
|/vaults/replicationRecoveryPlans/plannedFailover/action|Выполняет плановую отработку отказа для плана восстановления.|
|/vaults/replicationRecoveryPlans/unplannedFailover/action|Выполняет отработку отказа для плана восстановления.|
|/vaults/replicationRecoveryPlans/testFailover/action|Тестирует отработку отказа для плана восстановления.|
|/vaults/replicationRecoveryPlans/testFailoverCleanup/action|Тестирует очистку отработки отказа для плана восстановления.|
|/vaults/replicationRecoveryPlans/failoverCommit/action|Выполняет отработку отказа с фиксацией для плана восстановления.|
|/vaults/replicationRecoveryPlans/reProtect/action|Повторно защищает план восстановления.|
|/Vaults/extendedInformation/read|Hello получить расширенные сведения операция возвращает расширенные сведения объекта представляющий ресурс Azure типа hello? хранилища?|
|/Vaults/extendedInformation/write|Hello получить расширенные сведения операция возвращает расширенные сведения объекта представляющий ресурс Azure типа hello? хранилища?|
|/Vaults/extendedInformation/delete|Hello получить расширенные сведения операция возвращает расширенные сведения объекта представляющий ресурс Azure типа hello? хранилища?|
|/Vaults/backupManagementMetaData/read|Возвращает метаданные управления архивацией для хранилища служб восстановления.|
|/Vaults/backupProtectionContainers/read|Возвращает все контейнеры, принадлежащий toohello подписки|
|/Vaults/backupFabrics/operationResults/read|Возвращает состояние операции hello|
|/Vaults/backupFabrics/protectionContainers/read|Возвращает все зарегистрированные контейнеры.|
|/Vaults/backupFabrics/protectionContainers/<br>operationResults/read|Возвращает результат операции, выполненной с контейнером защиты.|
|/Vaults/backupFabrics/protectionContainers/<br>protectedItems/read|Возвращает сведения об hello защищенному элементу объекте|
|/Vaults/backupFabrics/protectionContainers/<br>protectedItems/write|Создает элемент, защищенный службой архивации.|
|/Vaults/backupFabrics/protectionContainers/<br>protectedItems/delete|Удаляет защищенный элемент.|
|/Vaults/backupFabrics/protectionContainers/<br>protectedItems/backup/action|Архивирует защищенный элемент.|
|/Vaults/backupFabrics/protectionContainers/<br>protectedItems/operationResults/read|Возвращает результат операции, выполненной с защищенными элементами.|
|/Vaults/backupFabrics/protectionContainers/<br>protectedItems/operationStatus/read|Возвращает состояние hello операции для защищенные элементы.|
|/Vaults/backupFabrics/protectionContainers/<br>protectedItems/recoveryPoints/read|Возвращает точки восстановления для защищенных элементов.|
|/Vaults/backupFabrics/protectionContainers/<br>protectedItems/recoveryPoints/<br>restore/action|Восстанавливает точки восстановления для защищенных элементов.|
|/Vaults/backupFabrics/protectionContainers/<br>protectedItems/recoveryPoints/<br>provisionInstantItemRecovery/action|Подготавливает мгновенное восстановление для защищенного элемента.|
|/Vaults/backupFabrics/protectionContainers/<br>protectedItems/recoveryPoints/<br>revokeInstantItemRecovery/action|Отменяет мгновенное восстановление для защищенного элемента.|
|/Vaults/usages/read|Возвращает данные об использовании хранилища служб восстановления.|
|/vaults/usages/read|Считывает данные об использовании хранилищ.|
|/Vaults/certificates/write|Операция обновления ресурса сертификата Hello обновляет сертификат учетных данных ресурсов или хранилища hello.|
|/Vaults/tokenInfo/read|Возвращает сведения о маркере для хранилища служб восстановления.|
|/vaults/replicationAlertSettings/read|Считывает параметры оповещений.|
|/vaults/replicationAlertSettings/write|Создает или обновляет параметры оповещений.|
|/Vaults/backupOperations/read|Возвращает состояние операции архивации для хранилища служб восстановления.|
|/Vaults/storageConfig/read|Возвращает конфигурацию службы хранилища для хранилища служб восстановления.|
|/Vaults/storageConfig/write|Обновляет конфигурацию службы хранилища для хранилища служб восстановления.|
|/Vaults/backupUsageSummaries/read|Возвращает сводки по защищенным элементам и защищенным серверам для служб восстановления.|
|/Vaults/backupProtectedItems/read|Возвращает список hello все защищенные элементы.|
|/Vaults/backupconfig/vaultconfig/read|Возвращает конфигурацию хранилища служб восстановления.|
|/Vaults/backupconfig/vaultconfig/write|Обновляет конфигурацию хранилища служб восстановления.|
|/Vaults/registeredIdentities/write|Hello операции зарегистрировать контейнер службы может быть используется tooregister контейнера в службе восстановления.|
|/Vaults/registeredIdentities/read|Hello получить контейнеры можно использовать операцию получить контейнеры hello, зарегистрированные для ресурса.|
|/Vaults/registeredIdentities/delete|Hello операции отмены регистрации контейнера может быть используется toounregister контейнера.|
|/Vaults/registeredIdentities/operationResults/read|Операция отправки Hello результаты операции получения операции можно использовать для получения состояния операции hello и привести hello асинхронно|
|/vaults/replicationJobs/read|Считывает задания.|
|/vaults/replicationJobs/cancel/action|Отменяет задание.|
|/vaults/replicationJobs/restart/action|Перезапускает задание.|
|/vaults/replicationJobs/resume/action|Возобновляет выполнение задания.|
|/Vaults/backupPolicies/read|Возвращает все политики защиты.|
|/Vaults/backupPolicies/write|Создает политику защиты.|
|/Vaults/backupPolicies/delete|Удаляет политику защиты.|
|/Vaults/backupPolicies/operationResults/read|Возвращает результаты операции политики.|
|/Vaults/backupPolicies/operationStatus/read|Возвращает состояние операции политики.|
|/Vaults/vaultTokens/read|Hello токен хранилища операции можно использовать tooget токен хранилища для внутренних операций уровня хранилища.|
|/Vaults/monitoringConfigurations/notificationConfiguration/read|Получает конфигурацию уведомлений хранилище служб восстановления hello.|
|/Vaults/backupJobs/read|Возвращает все объекты заданий.|
|/Vaults/backupJobs/cancel/action|Отмена задания hello|
|/Vaults/backupJobs/operationResults/read|Здравствуйте, возвращает результат операции задания.|
|/locations/allocateStamp/action|AllocatedStamp является внутренней операцией, используемой службой.|
|/locations/allocatedStamp/read|GetAllocatedStamp является внутренней операцией, используемой службой.|

## <a name="microsoftrelay"></a>Microsoft.Relay

| Операция | Описание |
|---|---|
|/checkNamespaceAvailability/action|Проверяет доступность пространства имен в заданной подписке.|
|/register/action|Регистрирует hello подписку для поставщика ресурсов ретрансляции hello и разрешает создание hello ресурсов ретрансляции|
|/namespaces/write|Создает ресурс пространства имен и обновляет его свойства. Теги и состояние hello пространства имен являются hello свойства, которые могут быть обновлены.|
|/namespaces/read|Получить hello список описаний ресурса пространства имен|
|/namespaces/Delete|Удаляет ресурс пространства имен.|
|/namespaces/authorizationRules/write|Создает правила авторизации уровня пространства имен и обновляет его свойства. Права доступа к правилам авторизации Hello, hello основные и вторичные ключи могут обновляться.|
|/namespaces/authorizationRules/delete|Удаляет правило авторизации для пространства имен. не удается удалить правило авторизации пространства имен по умолчанию Hello. |
|/namespaces/authorizationRules/listkeys/action|Получение строки подключения hello toohello пространство имен|
|/namespaces/HybridConnections/write|Создает или обновляет свойства гибридного подключения.|
|/namespaces/HybridConnections/read|Возвращает список описаний ресурсов гибридного подключения.|
|/namespaces/HybridConnections/Delete|Операция toodelete HybridConnection ресурсов|
|/namespaces/HybridConnections/authorizationRules/write|Создает правила авторизации гибридного подключения и обновляет его свойства. Права доступа к правилам авторизации Hello, hello основные и вторичные ключи могут обновляться.|
|/namespaces/HybridConnections/authorizationRules/delete|Операция toodelete HybridConnection правила авторизации|
|/namespaces/HybridConnections/authorizationRules/listkeys/action|Получить строку подключения tooHybridConnection hello|
|/namespaces/WcfRelays/write|Создает или обновляет свойства ретранслятора WCF.|
|/namespaces/WcfRelays/read|Возвращает список описаний ресурсов ретранслятора WCF.|
|/namespaces/WcfRelays/Delete|Операция toodelete WcfRelay ресурсов|
|/namespaces/WcfRelays/authorizationRules/write|Создает правила авторизации ретранслятора WCF и обновляет его свойства. Права доступа к правилам авторизации Hello, hello основные и вторичные ключи могут обновляться.|
|/namespaces/WcfRelays/authorizationRules/delete|Операция toodelete WcfRelay правила авторизации|
|/namespaces/WcfRelays/authorizationRules/listkeys/action|Получить строку подключения tooWcfRelay hello|

## <a name="microsoftresourcehealth"></a>Microsoft.ResourceHealth

| Операция | Описание |
|---|---|
|/AvailabilityStatuses/read|Получает состояния доступности hello для всех ресурсов в hello указан области|
|/AvailabilityStatuses/current/read|Получает состояние доступности hello для hello указанный ресурс|

## <a name="microsoftresources"></a>Microsoft.Resources

| Операция | Описание |
|---|---|
|/checkResourceName/action|Проверьте правильность имени ресурса hello.|
|/providers/read|Получите список поставщиков hello.|
|/subscriptions/read|Получает список подписок hello.|
|/subscriptions/operationresults/read|Получите подписку hello результаты операции.|
|/subscriptions/providers/read|Возвращает поставщики ресурсов или выводит их список.|
|/subscriptions/tagNames/read|Возвращает теги подписки или выводит их список.|
|/subscriptions/tagNames/write|Добавляет тег подписки.|
|/subscriptions/tagNames/delete|Удаляет тег подписки.|
|/subscriptions/tagNames/tagValues/read|Возвращает значения тегов подписки или выводит их список.|
|/subscriptions/tagNames/tagValues/write|Добавляет значение тега подписки.|
|/subscriptions/tagNames/tagValues/delete|Удаляет значение тега подписки.|
|/subscriptions/resources/read|Возвращает ресурсы подписки.|
|/subscriptions/resourceGroups/read|Возвращает группы ресурсов или выводит их список.|
|/subscriptions/resourceGroups/write|Создает или обновляет группу ресурсов.|
|/subscriptions/resourceGroups/delete|Удаляет группу ресурсов со всеми ресурсами.|
|/subscriptions/resourceGroups/moveResources/action|Перемещает ресурсы из группы tooanother один ресурс.|
|/subscriptions/resourceGroups/validateMoveResources/action|Проверка перемещения ресурсов из группы tooanother один ресурс.|
|/subscriptions/resourcegroups/resources/read|Получает ресурсы hello hello группы ресурсов.|
|/subscriptions/resourcegroups/deployments/read|Возвращает развернутые службы или выводит их список.|
|/subscriptions/resourcegroups/deployments/write|Создает или обновляет развертывание.|
|/subscriptions/resourcegroups/deployments/operationstatuses/read|Возвращает состояния операций развертывания или выводит их список.|
|/subscriptions/resourcegroups/deployments/operations/read|Возвращает операции развертывания или выводит их список.|
|/subscriptions/locations/read|Возвращает список поддерживаемых расположений hello.|
|/links/read|Возвращает ссылки на ресурсы или выводит их список.|
|/links/write|Создает или обновляет ссылку на ресурс.|
|/links/delete|Удаляет ссылку на ресурс.|
|/tenants/read|Возвращает список клиентов hello.|
|/resources/read|Получите список ресурсов на основе фильтров hello.|
|/deployments/read|Возвращает развернутые службы или выводит их список.|
|/deployments/write|Создает или обновляет развертывание.|
|/deployments/delete|Удаляет развертывание.|
|/deployments/cancel/action|Отменяет развертывание.|
|/deployments/validate/action|Проверяет развертывание.|
|/deployments/operations/read|Возвращает операции развертывания или выводит их список.|

## <a name="microsoftscheduler"></a>Microsoft.Scheduler

| Операция | Описание |
|---|---|
|/jobcollections/read|Возвращает коллекцию заданий.|
|/jobcollections/write|Создает или обновляет коллекцию заданий.|
|/jobcollections/delete|Удаляет коллекцию заданий.|
|/jobcollections/enable/action|Включает коллекцию заданий.|
|/jobcollections/disable/action|Отключает коллекцию заданий.|
|/jobcollections/jobs/read|Возвращает задание.|
|/jobcollections/jobs/write|Создает или обновляет задание.|
|/jobcollections/jobs/delete|Удаляет задание.|
|/jobcollections/jobs/run/action|Выполняет задание.|
|/jobcollections/jobs/generateLogicAppDefinition/action|Создает определение приложения логики на основе задания планировщика.|
|/jobcollections/jobs/jobhistories/read|Получает журнал заданий.|

## <a name="microsoftsearch"></a>Microsoft.Search

| Операция | Описание |
|---|---|
|/register/action|Регистрирует hello подписку для поставщика ресурсов поиска hello и обеспечивает создание hello службы поиска.|
|/checkNameAvailability/action|Проверяет доступность hello имя службы.|
|/searchServices/write|Создает или обновляет hello службы поиска.|
|/searchServices/read|Считывает hello службы поиска.|
|/searchServices/delete|Удаление службы поиска hello.|
|/searchServices/start/action|Запуск службы поиска hello.|
|/searchServices/stop/action|Останавливает службу поиска hello.|
|/searchServices/listAdminKeys/action|Считывает ключи администратора hello.|
|/searchServices/regenerateAdminKey/action|Повторно создает ключ администратора hello.|
|/searchServices/createQueryKey/action|Создает ключ запроса hello.|
|/searchServices/queryKey/read|Считывает ключей запроса hello.|
|/searchServices/queryKey/delete|Удаляет ключ запроса hello.|

## <a name="microsoftsecurity"></a>Microsoft.Security

| Операция | Описание |
|---|---|
|/jitNetworkAccessPolicies/read|Возвращает политик доступа к сети на момент hello|
|/jitNetworkAccessPolicies/write|Создает новую политику JIT-доступа к сети или обновляет существующую.|
|/jitNetworkAccessPolicies/initiate/action|Инициирует политику JIT-доступа к сети.|
|/securitySolutionsReferenceData/read|Возвращает решения по обеспечению безопасности hello ссылочных данных|
|/securityStatuses/read|Получает параметры защиты hello состояния работоспособности для ресурсов Azure|
|/webApplicationFirewalls/read|Возвращает брандмауэры приложения hello web|
|/webApplicationFirewalls/write|Создает новый брандмауэр веб-приложения или обновляет существующий.|
|/webApplicationFirewalls/delete|Удаляет брандмауэр веб-приложения.|
|/securitySolutions/read|Возвращает hello решения по обеспечению безопасности|
|/securitySolutions/write|Создает новое решение безопасности или обновляет существующее.|
|/securitySolutions/delete|Удаляет решение безопасности.|
|/tasks/read|Возвращает все доступные рекомендации по безопасности.|
|/tasks/dismiss/action|Закрывает рекомендацию по безопасности.|
|/tasks/activate/action|Активирует рекомендацию по безопасности.|
|/policies/read|Получает политику безопасности hello|
|/policies/write|Здравствуйте, обновления политики безопасности|
|/applicationWhitelistings/read|Возвращает whitelistings приложения hello|
|/applicationWhitelistings/write|Создает новый список разрешений приложения или обновляет существующий.|

## <a name="microsoftservermanagement"></a>Microsoft.ServerManagement

| Операция | Описание |
|---|---|
|/subscriptions/write|Создает или обновляет подписку.|
|/gateways/write|Создает или обновляет шлюз.|
|/gateways/delete|Удаляет шлюз.|
|/gateways/read|Возвращает шлюз.|
|/gateways/regenerateprofile/action|Повторно создает профиль шлюза hello|
|/gateways/upgradetolatest/action|Последнюю версию шлюза hello toohello обновления|
|/nodes/write|Создает или обновляет узел.|
|/nodes/delete|Удаляет узел.|
|/nodes/read|Возвращает узел.|
|/sessions/write|Создает или обновляет сеанс.|
|/sessions/read|Возвращает сеанс.|
|/sessions/delete|Удаляет сеанс.|

## <a name="microsoftservicebus"></a>Microsoft.ServiceBus

| Операция | Описание |
|---|---|
|/checkNameAvailability/action|Проверяет доступность пространства имен в заданной подписке.|
|/register/action|Регистрирует hello подписку для поставщика ресурсов служебной шины hello и разрешает создание ресурсов служебной шины hello|
|/namespaces/write|Создает ресурс пространства имен и обновляет его свойства. Теги и состояние hello пространства имен являются hello свойства, которые могут быть обновлены.|
|/namespaces/read|Получить hello список описаний ресурса пространства имен|
|/namespaces/Delete|Удаляет ресурс пространства имен.|
|/namespaces/metricDefinitions/read|Возвращает список описаний ресурсов метрик пространства имен.|
|/namespaces/authorizationRules/write|Создает правила авторизации уровня пространства имен и обновляет его свойства. Права доступа к правилам авторизации Hello, hello основные и вторичные ключи могут обновляться.|
|/namespaces/authorizationRules/read|Получите список hello описание правил авторизации пространства имен.|
|/namespaces/authorizationRules/delete|Удаляет правило авторизации для пространства имен. не удается удалить правило авторизации пространства имен по умолчанию Hello. |
|/namespaces/authorizationRules/listkeys/action|Получение строки подключения hello toohello пространство имен|
|/namespaces/authorizationRules/regenerateKeys/action|Повторное создание hello основных или дополнительных ключей toohello ресурсов|
|/namespaces/diagnosticSettings/read|Возвращает список описаний параметров диагностики пространства имен.|
|/namespaces/diagnosticSettings/write|Возвращает список описаний параметров диагностики пространства имен.|
|/namespaces/queues/write|Создает или обновляет свойства очереди.|
|/namespaces/queues/read|Возвращает список описаний ресурсов очереди.|
|/namespaces/queues/Delete|Операция toodelete ресурса очереди|
|/namespaces/queues/authorizationRules/write|Создает правила авторизации очереди и обновляет ее свойства. Права доступа к правилам авторизации Hello, hello основные и вторичные ключи могут обновляться.|
|/namespaces/queues/authorizationRules/read| Получить список правил авторизации очереди hello|
|/namespaces/queues/authorizationRules/delete|Операция toodelete правила авторизации в очереди|
|/namespaces/queues/authorizationRules/listkeys/action|Получить строку подключения tooQueue hello|
|/namespaces/queues/authorizationRules/regenerateKeys/action|Повторное создание hello основных или дополнительных ключей toohello ресурсов|
|/namespaces/logDefinitions/read|Возвращает список описаний ресурсов журналов пространства имен.|
|/namespaces/topics/write|Создает или обновляет свойства раздела.|
|/namespaces/topics/read|Возвращает список описаний ресурсов раздела.|
|/namespaces/topics/Delete|Операция toodelete раздел ресурсов|
|/namespaces/topics/authorizationRules/write|Создает правила авторизации раздела и обновляет его свойства. Права доступа к правилам авторизации Hello, hello основные и вторичные ключи могут обновляться.|
|/namespaces/topics/authorizationRules/read| Получить список правил авторизации разделе hello|
|/namespaces/topics/authorizationRules/delete|Операция toodelete разделе правила авторизации|
|/namespaces/topics/authorizationRules/listkeys/action|Получить строку подключения tooTopic hello|
|/namespaces/topics/authorizationRules/regenerateKeys/action|Повторное создание hello основных или дополнительных ключей toohello ресурсов|
|/namespaces/topics/subscriptions/write|Создает или обновляет свойства подписки на раздел.|
|/namespaces/topics/subscriptions/read|Возвращает список описаний ресурсов подписки на раздел.|
|/namespaces/topics/subscriptions/Delete|Операция toodelete TopicSubscription ресурсов|
|/namespaces/topics/subscriptions/rules/write|Создает или обновляет свойства правила.|
|/namespaces/topics/subscriptions/rules/read|Возвращает список описаний ресурсов правила.|
|/namespaces/topics/subscriptions/rules/Delete|Операция toodelete ресурс правила|

## <a name="microsoftsql"></a>Microsoft.Sql

| Операция | Описание |
|---|---|
|/servers/read|Возвращает список серверов в группе ресурсов для подписки.|
|/servers/write|Создает новый сервер или изменяет свойства существующего сервера в группе ресурсов в подписке.|
|/servers/delete|Удаляет сервер и все содержащиеся в нем базы данных и эластичные пулы.|
|/servers/import/action|Создать новую базу данных на сервере hello и развертывание схемы и данных из DacPac-пакет|
|/servers/upgrade/action|Включение новых функций, доступных на последнюю версию сервера hello и укажите схема преобразования для выпуска базы данных|
|/servers/VulnerabilityAssessmentScans/action|Выполняет поиск уязвимостей сервера.|
|/servers/operationResults/read|Операция используется tootrack ход обновления сервера из нижнего toohigher версии|
|/servers/operationResults/delete|Прерывает выполняемое обновление версии сервера.|
|/servers/securityAlertPolicies/read|Получить сведения о hello server угроз обнаружения политики настроены на данном сервере|
|/servers/securityAlertPolicies/write|Изменение обнаружения угроз hello server для данного сервера|
|/servers/securityAlertPolicies/operationResults/read|Получить результаты hello сервера политики обнаружения угроз операции Set|
|/servers/administrators/read|Извлекает сведения об администраторе сервера.|
|/servers/administrators/write|Создает или обновляет учетные данные администратора сервера.|
|/servers/administrators/delete|Удалить администратора сервера с сервера hello|
|/servers/recoverableDatabases/read|Эта операция используется для аварийного восстановления, действующей базы данных toorestore базы данных toolast известного хорошо точки резервного копирования. Возвращает сведения о последней удачной резервной hello, но он не восстанавливает фактически hello базы данных.|
|/servers/serviceObjectives/read|Извлекает список целей уровня обслуживания (также известных как уровни производительности), доступных на данном сервере.|
|/servers/firewallRules/read|Извлекает сведения о правиле брандмауэра для сервера.|
|/servers/firewallRules/write|Создать или обновить правила брандмауэра для сервера, управляющий допускается tooconnect toohello server диапазон IP-адресов|
|/servers/firewallRules/delete|Удалить правило брандмауэра с сервера hello|
|/servers/administratorOperationResults/read|Извлекает сведения об операции администратора сервера.|
|/servers/recommendedElasticPools/read|Получить рекомендации по стоимости tooreduce пулы эластичных баз данных и повышения производительности в зависимости от использования ресурсов historica|
|/servers/recommendedElasticPools/metrics/read|Извлекает метрики для рекомендуемых пулов эластичных баз данных для заданного сервера.|
|/servers/recommendedElasticPools/databases/read|Извлекает базы данных, которые следует добавить в рекомендуемые пулы эластичных баз данных для заданного сервера.|
|/servers/elasticPools/read|Извлекает сведения о пуле эластичных баз данных для заданного сервера.|
|/servers/elasticPools/write|Создает новый пул эластичных баз данных или изменяет свойства существующего.|
|/servers/elasticPools/delete|Удаляет существующий пул эластичных баз данных.|
|/servers/elasticPools/operationResults/read|Извлекает сведения о заданной операции пула эластичных баз данных.|
|/servers/elasticPools/providers/Microsoft.Insights/<br>metricDefinitions/read|Возвращает типы метрик, доступных для пулов эластичных баз данных.|
|/servers/elasticPools/providers/Microsoft.Insights/<br>diagnosticSettings/read|Возвращает приветствия диагностики для ресурса hello|
|/servers/elasticPools/providers/Microsoft.Insights/<br>diagnosticSettings/write|Создает или обновляет приветствия диагностики для ресурса hello|
|/servers/elasticPools/metrics/read|Возвращает метрики использования ресурсов пула эластичных баз данных.|
|/servers/elasticPools/elasticPoolDatabaseActivity/read|Извлекает действия заданной базы данных, входящей в пул эластичных баз данных, а также сведения о ней.|
|/servers/elasticPools/advisors/read|Возвращает список помощников, доступные для эластичного пула hello|
|/servers/elasticPools/advisors/write|Обновляет состояние автовыполнения Помощника на уровне эластичного пула.|
|/servers/elasticPools/advisors/recommendedActions/read|Возвращает список рекомендуемые действия для указанного помощника для эластичного пула hello|
|/servers/elasticPools/advisors/recommendedActions/write|Применить hello Рекомендуемое действие для эластичного пула hello|
|/servers/elasticPools/elasticPoolActivity/read|Извлекает действия и сведения о заданном пуле эластичных баз данных.|
|/servers/elasticPools/databases/read|Извлекает список баз данных, которые входят в пул эластичных баз данных на заданном сервере, а также сведения о них.|
|/servers/auditingPolicies/read|Получить сведения о на данном сервере настроена политика аудита таблицы server по умолчанию hello|
|/servers/auditingPolicies/write|Изменить таблицу сервера по умолчанию hello, аудит для данного сервера|
|/servers/disasterRecoveryConfiguration/operationResults/read|Возвращает результаты операции настройки аварийного восстановления.|
|/servers/advisors/read|Возвращает список помощников, доступный для сервера hello|
|/servers/advisors/write|Обновляет состояние автовыполнения Помощника на уровне сервера.|
|/servers/advisors/recommendedActions/read|Возвращает список рекомендуемые действия для указанного помощника по настройке ядра сервера hello|
|/servers/advisors/recommendedActions/write|Применить hello Рекомендуемое действие на сервере hello|
|/servers/usages/read|Квота DTU возврата сервера и текущего consuption DTU используется всеми базами данных в пределах сервера hello|
|/servers/elasticPoolEstimates/read|Возвращает список оценок эластичных пулов, уже созданных на этом сервере.|
|/servers/elasticPoolEstimates/write|Создает оценку эластичного пула для указанных баз данных.|
|/servers/auditingSettings/read|Получить сведения о сервере hello большого двоичного объекта, на данном сервере настроена политика аудита|
|/servers/auditingSettings/write|Изменить параметры сервера hello BLOB-объект аудита для данного сервера|
|/servers/auditingSettings/operationResults/read|Извлечь результат операции задания политики аудита большого двоичного объекта сервера hello|
|/servers/backupLongTermRetentionVaults/read|Эта операция является tooget используется хранилище архивации долговременного хранения. Она возвращает сведения о hello хранилище toothis зарегистрированного сервера.|
|/servers/backupLongTermRetentionVaults/write|Регистрирует хранилище резервных копий долгосрочного хранения.|
|/servers/restorableDroppedDatabases/read|Извлекает список баз данных, которые были удалены на заданном сервере, но остались в политике хранения. С помощью этой операции можно получить список баз данных и связанные метаданные, например даты удаления.|
|/servers/databases/read|Возвращает список серверов в группе ресурсов для подписки.|
|/servers/databases/write|Создает новый сервер или изменяет свойства существующего сервера в группе ресурсов в подписке.|
|/servers/databases/delete|Удаляет сервер и все содержащиеся в нем базы данных и эластичные пулы.|
|/servers/databases/export/action|Создать новую базу данных на сервере hello и развертывание схемы и данных из DacPac-пакет|
|/servers/databases/VulnerabilityAssessmentScans/action|Выполняет поиск уязвимостей базы данных.|
|/servers/databases/pause/action|Приостанавливает базу данных выпуска хранилища данных.|
|/servers/databases/resume/action|Возобновляет работу базы данных выпуска хранилища данных.|
|/servers/databases/operationResults/read|Операция используется tootrack ход выполнения длительных операций базы данных, например масштаб.|
|/servers/databases/replicationLinks/read|Возвращает сведения о каналах репликации, установленных для определенной базы данных.|
|/servers/databases/replicationLinks/delete|Завершение связи репликации hello принудительно и при этом возможна потеря данных|
|/servers/databases/replicationLinks/unlink/action|Завершение связи репликации hello принудительно или после синхронизации с партнером hello|
|/servers/databases/replicationLinks/failover/action|Переход на другой ресурс после синхронизации всех изменений из первичной, hello превращение этой базы данных в удаленной первичный отношение репликации hello hello основной и внесения в дополнительный|
|/servers/databases/replicationLinks/forceFailoverAllowDataLoss/action|Переход на другой ресурс немедленно с возможной потерей данных, делая этой базы данных в отношение репликации hello основной и позволяя hello удаленного основного на дополнительный|
|/servers/databases/replicationLinks/updateReplicationMode/action|Обновление режима репликации для связи toosynchronous или асинхронном режиме|
|/servers/databases/replicationLinks/operationResults/read|Возвращает состояние длительных операций с каналами репликации базы данных.|
|/servers/databases/dataMaskingPolicies/read|Получить сведения о данных hello маскировки политика, настроенная в данной базе данных|
|/servers/databases/dataMaskingPolicies/write|Изменяет политику маскирования данных для заданной базы данных.|
|/servers/databases/dataMaskingPolicies/rules/read|Получить сведения о данных hello маскировки правила политики, которые настроены в данной базе данных|
|/servers/databases/dataMaskingPolicies/rules/write|Изменяет правило политики маскирования данных для заданной базы данных.|
|/servers/databases/securityAlertPolicies/read|Получить сведения о данной базы данных настроен политика обнаружения угроз hello|
|/servers/databases/securityAlertPolicies/write|Изменение политики обнаружения hello угроз для базы данных|
|/servers/databases/providers/Microsoft.Insights/<br>metricDefinitions/read|Возвращает типы метрик, доступных для баз данных.|
|/servers/databases/providers/Microsoft.Insights/<br>diagnosticSettings/read|Возвращает приветствия диагностики для ресурса hello|
|/servers/databases/providers/Microsoft.Insights/<br>diagnosticSettings/write|Создает или обновляет приветствия диагностики для ресурса hello|
|/servers/databases/providers/Microsoft.Insights/<br>logDefinitions/read|Получает доступные журналы hello для баз данных|
|/servers/databases/topQueries/read|Возвращает статистические данные среды выполнения для выбранного запроса в указанный временной период.|
|/servers/databases/topQueries/queryText/read|Возвращает текст hello Transact-SQL для идентификатора выбранного запроса|
|/servers/databases/topQueries/statistics/read|Возвращает статистические данные среды выполнения для выбранного запроса в указанный временной период.|
|/servers/databases/connectionPolicies/read|Получить сведения о политики подключение hello настроен в данной базе данных|
|/servers/databases/connectionPolicies/write|Изменяет политику подключений для заданной базы данных.|
|/servers/databases/metrics/read|Возвращает метрики использования ресурсов базы данных.|
|/servers/databases/auditRecords/read|Получить записи аудита hello базы данных больших двоичных объектов|
|/servers/databases/transparentDataEncryption/read|Извлекает состояние и сведения о функции безопасности "прозрачное шифрование данных" для заданной базы данных.|
|/servers/databases/transparentDataEncryption/write|Включает или отключает прозрачное шифрование данных для заданной базы данных.|
|/servers/databases/transparentDataEncryption/operationResults/read|Извлекает состояние и сведения о функции безопасности "прозрачное шифрование данных" для заданной базы данных.|
|/servers/databases/auditingPolicies/read|Получить сведения о политики аудита таблицы hello настроен в данной базе данных|
|/servers/databases/auditingPolicies/write|Изменение политики аудита hello таблицы для базы данных|
|/servers/databases/dataWarehouseQueries/read|Возвращает hello хранилища распределения запросов данных для идентификатора выбранного запроса|
|/servers/databases/dataWarehouseQueries/<br>dataWarehouseQuerySteps/read|Возвращает hello распределенного запроса сведений о шаге запроса хранилища данных для идентификатора выбранного шага|
|/servers/databases/serviceTierAdvisors/read|Возвращают предложение по поводу масштабирование базы данных, в зависимости от быстродействия tooimprove статистику выполнения запросов или снизить затраты на|
|/servers/databases/advisors/read|Возвращает список помощников, доступные для hello базы данных|
|/servers/databases/advisors/write|Обновляет состояние автовыполнения Помощника на уровне базы данных.|
|/servers/databases/advisors/recommendedActions/read|Возвращает список рекомендуемые действия для указанного помощника по настройке ядра базы данных hello|
|/servers/databases/advisors/recommendedActions/write|Применить hello Рекомендуемое действие hello базы данных|
|/servers/databases/usages/read|Возвращает максимальный размер базы данных, который может быть достигнут, и текущую емкость, занимаемую данными.|
|/servers/databases/queryStore/read|Возвращает текущие значения параметров хранилища запросов базы данных hello|
|/servers/databases/queryStore/write|Обновляет параметр хранилища запросов для базы данных hello|
|/servers/databases/auditingSettings/read|Получить сведения о hello BLOB-объект аудита политика, настроенная в данной базе данных|
|/servers/databases/auditingSettings/write|Изменение политики аудита hello большого двоичного объекта для базы данных|
|/servers/databases/schemas/tables/recommendedIndexes/read|Извлекает список рекомендаций по индексам для базы данных.|
|/servers/databases/schemas/tables/recommendedIndexes/write|Применяет рекомендацию по индексу.|
|/servers/databases/schemas/tables/columns/read|Извлекает список столбцов таблицы.|
|/servers/databases/missingindexes/read|Возвращает предложения о toocreate индексов базы данных, изменить или удалить в производительности запросов tooimprove заказа|
|/servers/databases/missingindexes/write|Применяет рекомендацию по индексу базы данных к определенной базе данных.|
|/servers/databases/importExportOperationResults/read|Возвращает сведения об операции импорта или экспорта базы данных с использованием пакета DACPAC, расположенного в учетной записи хранения.|
|/servers/importExportOperationResults/read|Получить список hello со сведениями для операций импорта базы данных из учетной записи хранилища на данном сервере|

## <a name="microsoftstorage"></a>Microsoft.Storage;

| Операция | Описание |
|---|---|
|/register/action|Регистрирует hello подписку для поставщика ресурсов хранилища hello и обеспечивает создание учетных записей хранения hello.|
|/checknameavailability/read|Проверяет, является ли имя учетной записи допустимым и неиспользуемым.|
|/storageAccounts/write|Создает учетную запись хранения с hello указанный параметрами или обновляет hello свойства или теги или добавляет пользовательский домен для hello указана учетная запись хранения.|
|/storageAccounts/delete|Удаляет существующую учетную запись хранения.|
|/storageAccounts/listkeys/action|Возвращает ключи доступа hello hello указана учетная запись хранения.|
|/storageAccounts/regeneratekey/action|Повторно создает ключи доступа hello для hello указана учетная запись хранения.|
|/storageAccounts/read|Здравствуйте, возвращает список учетных записей хранения или получает свойства hello hello указана учетная запись хранилища.|
|/storageAccounts/listAccountSas/action|Возвращает маркер SAS для учетной записи hello для hello указана учетная запись хранения.|
|/storageAccounts/listServiceSas/action|Маркер SAS службы хранилища.|
|/storageAccounts/services/diagnosticSettings/write|Создает или обновляет параметры диагностики учетной записи хранения.|
|/skus/read|Список номеров SKU, поддерживаемые хранилища Майкрософт hello.|
|/usages/read|Возвращает hello ограничение с указанием hello текущий счетчик использования ресурсов в hello подписки|
|/operations/read|Опрашивает hello состояние асинхронной операции.|
|/locations/deleteVirtualNetworkOrSubnets/action|Уведомляет поставщик ресурсов Microsoft.Storage о том, что удаляется виртуальная сеть или подсеть.|

## <a name="microsoftstorsimple"></a>Microsoft.StorSimple

| Операция | Описание |
|---|---|
|/managers/clearAlerts/action|Отменить все оповещения hello, связанный с диспетчером устройств hello.|
|/managers/getActivationKey/action|Получите ключ активации для hello диспетчера устройств.|
|/managers/regenerateActivationKey/action|Повторное создание ключа активации для hello диспетчера устройств.|
|/managers/regenarateRegistationCertificate/action|Повторно создать сертификат регистрации для диспетчеров hello устройств.|
|/managers/getEncryptionKey/action|Получение ключа шифрования для hello диспетчера устройств.|
|/managers/read|Возвращает диспетчеры устройств hello или список|
|/managers/delete|Удаляет диспетчеры устройств hello|
|/managers/write|Создать или обновить диспетчеры устройств hello|
|/managers/configureDevice/action|Настраивает устройство.|
|/managers/listActivationKey/action|Возвращает ключ активации hello hello устройства StorSimple.|
|/managers/listPublicEncryptionKey/action|Выводит список открытых ключей шифрования для диспетчера устройств StorSimple.|
|/managers/listPrivateEncryptionKey/action|Возвращает ключ шифрования для диспетчера устройств StorSimple.|
|/managers/provisionCloudAppliance/action|Создает облачное устройство.|
|/Managers/write|Создает операцию создания хранилища, которая создает ресурс Azure типа "хранилище".|
|/Managers/read|Hello получить хранилище операция возвращает объект, представляющий ресурс Azure типа «vault» hello|
|/Managers/delete|Операция удаления Hello удалить хранилище hello указанный ресурс Azure типа «vault»|
|/managers/storageAccountCredentials/write|Создать или обновить учетные данные хранилища hello|
|/managers/storageAccountCredentials/read|Получает учетные данные хранилища hello или список|
|/managers/storageAccountCredentials/delete|Удаляет учетные данные хранилища hello|
|/managers/storageAccountCredentials/listAccessKey/action|Выводит список ключей доступа для данных учетной записи хранения.|
|/managers/accessControlRecords/read|Возвращает записи управления доступом hello или список|
|/managers/accessControlRecords/write|Создание и редактирование записи управления доступом hello|
|/managers/accessControlRecords/delete|Удаляет записи управления доступом hello|
|/managers/metrics/read|Выводит список или получает hello метрики|
|/managers/bandwidthSettings/read|Список параметров пропускной способности hello (серии 8000 только)|
|/managers/bandwidthSettings/write|Создает или обновляет параметры пропускной способности (только для серии 8000).|
|/managers/bandwidthSettings/delete|Удаляет существующие параметры пропускной способности (только для серии 8000).|
|/Managers/extendedInformation/read|Hello получить расширенные сведения операция возвращает расширенные сведения объекта представляющий ресурс Azure типа hello? хранилища?|
|/Managers/extendedInformation/write|Hello получить расширенные сведения операция возвращает расширенные сведения объекта представляющий ресурс Azure типа hello? хранилища?|
|/Managers/extendedInformation/delete|Hello получить расширенные сведения операция возвращает расширенные сведения объекта представляющий ресурс Azure типа hello? хранилища?|
|/managers/alerts/read|Возвращает предупреждения hello или список|
|/managers/storageDomains/read|Получает домены hello хранилища или список|
|/managers/storageDomains/write|Создание или обновление доменов хранилища hello|
|/managers/storageDomains/delete|Удаление доменов хранилища hello|
|/managers/devices/scanForUpdates/action|Выполняет поиск обновлений в устройстве.|
|/managers/devices/download/action|Скачивает обновления для устройства.|
|/managers/devices/install/action|Устанавливает обновления на устройство.|
|/managers/devices/read|Выводит список или получает hello устройства|
|/managers/devices/write|Создание или обновление устройств hello|
|/managers/devices/delete|Удаляет hello устройства|
|/managers/devices/deactivate/action|Деактивирует устройство.|
|/managers/devices/publishSupportPackage/action|Публикует пакет поддержки устройства для устранения неполадок службой поддержки Майкрософт.|
|/managers/devices/failover/action|Отработка отказа устройства hello.|
|/managers/devices/sendTestAlertEmail/action|Отправьте оповещение по электронной почте теста tooconfigured получателей электронной почты.|
|/managers/devices/installUpdates/action|Устанавливает обновления на устройствах hello|
|/managers/devices/listFailoverSets/action|Для существующего устройства задает список hello перехода на другой ресурс.|
|/managers/devices/listFailoverTargets/action|Список целей hello устройств|
|/managers/devices/publicEncryptionKey/action|Список общедоступный ключ шифрования hello диспетчера устройств|
|/managers/devices/hardwareComponentGroups/<br>read|Список hello группы компонентов оборудования|
|/managers/devices/hardwareComponentGroups/<br>changeControllerPowerState/action|Изменяет состояние питания контроллера для групп компонентов оборудования.|
|/managers/devices/metrics/read|Выводит список или получает hello метрики|
|/managers/devices/chapSettings/write|Создать или обновить параметры Chap hello|
|/managers/devices/chapSettings/read|Получает параметры Chap hello или список|
|/managers/devices/chapSettings/delete|Удаляет параметры Chap hello|
|/managers/devices/backupScheduleGroups/read|Получает группы расписаний резервного копирования hello или список|
|/managers/devices/backupScheduleGroups/write|Создание или обновление групп расписаний резервного копирования hello|
|/managers/devices/backupScheduleGroups/delete|Удаление групп расписаний резервного копирования hello|
|/managers/devices/updateSummary/read|Получает hello сводки обновлений или список|
|/managers/devices/migrationSourceConfigurations/<br>import/action|Импортирует конфигурации источников для переноса.|
|/managers/devices/migrationSourceConfigurations/<br>startMigrationEstimate/action|Запустите задание tooestimate hello длительность процесса миграции hello.|
|/managers/devices/migrationSourceConfigurations/<br>startMigration/action|Начинает перенос с использованием конфигураций источников.|
|/managers/devices/migrationSourceConfigurations/<br>confirmMigration/action|Подтверждает успешный перенос и фиксирует его.|
|/managers/devices/migrationSourceConfigurations/<br>fetchMigrationEstimate/action|Получить статус hello hello миграции оценки задания.|
|/managers/devices/migrationSourceConfigurations/<br>fetchMigrationStatus/action|Получить состояние hello для миграции hello.|
|/managers/devices/migrationSourceConfigurations/<br>fetchConfirmMigrationStatus/action|FETCH hello подтвердить состояние миграции.|
|/managers/devices/alertSettings/read|Получает параметры оповещений hello или список|
|/managers/devices/alertSettings/write|Создать или обновить параметры оповещений hello|
|/managers/devices/networkSettings/read|Получает параметры сети hello или список|
|/managers/devices/networkSettings/write|Создает или обновляет параметры сети.|
|/managers/devices/jobs/read|Выводит список или возвращает задания hello|
|/managers/devices/jobs/cancel/action|Отменяет выполнение задания.|
|/managers/devices/metricsDefinitions/read|Возвращает определения показателей hello или список|
|/managers/devices/volumeContainers/write|Создает или обновляет контейнеры томов (только для серии 8000).|
|/managers/devices/volumeContainers/read|Список контейнеров томов hello (серии 8000 только)|
|/managers/devices/volumeContainers/delete|Удаляет существующие контейнеры томов (только для серии 8000).|
|/managers/devices/volumeContainers/listEncryptionKeys/action|Выводит список ключей шифрования контейнеров томов.|
|/managers/devices/volumeContainers/rolloverEncryptionKey/action|Переключает ключи шифрования контейнеров томов.|
|/managers/devices/volumeContainers/metrics/read|Список hello метрики|
|/managers/devices/volumeContainers/volumes/read|Hello список томов|
|/managers/devices/volumeContainers/volumes/write|Создает или обновляет тома.|
|/managers/devices/volumeContainers/volumes/delete|Удаляет существующие тома.|
|/managers/devices/volumeContainers/volumes/metrics/read|Список hello метрики|
|/managers/devices/volumeContainers/volumes/metricsDefinitions/read|Hello список определений метрик|
|/managers/devices/volumeContainers/metricsDefinitions/read|Hello список определений метрик|
|/managers/devices/iscsiservers/read|Получает hello iSCSI серверов или список|
|/managers/devices/iscsiservers/write|Создать или обновить hello iSCSI серверов|
|/managers/devices/iscsiservers/delete|Удаляет hello iSCSI серверов|
|/managers/devices/iscsiservers/backup/action|Архивирует сервер iSCSI.|
|/managers/devices/iscsiservers/metrics/read|Выводит список или получает hello метрики|
|/managers/devices/iscsiservers/disks/read|Выводит список или возвращает диски hello|
|/managers/devices/iscsiservers/disks/write|Создать или обновить диски hello|
|/managers/devices/iscsiservers/disks/delete|Удаление дисков hello|
|/managers/devices/iscsiservers/disks/metrics/read|Выводит список или получает hello метрики|
|/managers/devices/iscsiservers/disks/metricsDefinitions/read|Возвращает определения показателей hello или список|
|/managers/devices/iscsiservers/metricsDefinitions/read|Возвращает определения показателей hello или список|
|/managers/devices/backups/read|Получает hello резервного набора данных или список|
|/managers/devices/backups/delete|Удаляет hello резервного набора данных|
|/managers/devices/backups/restore/action|Восстановление всех томов hello из резервной копии.|
|/managers/devices/backups/elements/clone/action|Клонирует общедоступный ресурс или том с помощью элемента архива.|
|/managers/devices/backupPolicies/write|Создает или обновляет политики архивации (только для серии 8000).|
|/managers/devices/backupPolicies/read|Hello список политик резервного копирования (серии 8000 только)|
|/managers/devices/backupPolicies/delete|Удаляет существующие политики архивации (только для серии 8000).|
|/managers/devices/backupPolicies/backup/action|Выполнить резервное копирование всех томов hello защищена политикой hello toocreate вручную резервного копирования по запросу.|
|/managers/devices/backupPolicies/schedules/write|Создает или обновляет расписания.|
|/managers/devices/backupPolicies/schedules/read|Список расписаний hello|
|/managers/devices/backupPolicies/schedules/delete|Удаляет существующие расписания.|
|/managers/devices/securitySettings/update/action|Обновите параметры безопасности hello.|
|/managers/devices/securitySettings/read|Список hello параметры безопасности|
|/managers/devices/securitySettings/<br>syncRemoteManagementCertificate/action|Синхронизируйте hello сертификат удаленного управления для устройства.|
|/managers/devices/securitySettings/write|Создает или обновляет параметры безопасности.|
|/managers/devices/fileservers/read|Получает hello файловых серверов или список|
|/managers/devices/fileservers/write|Создать или обновить hello файловых серверов|
|/managers/devices/fileservers/delete|Удаляет hello файловых серверов|
|/managers/devices/fileservers/backup/action|Архивирует файловый сервер.|
|/managers/devices/fileservers/metrics/read|Выводит список или получает hello метрики|
|/managers/devices/fileservers/shares/write|Создать или обновить общие ресурсы hello|
|/managers/devices/fileservers/shares/read|Получает hello общих папок или список|
|/managers/devices/fileservers/shares/delete|Удаляет hello общих папок|
|/managers/devices/fileservers/shares/metrics/read|Выводит список или получает hello метрики|
|/managers/devices/fileservers/shares/metricsDefinitions/read|Возвращает определения показателей hello или список|
|/managers/devices/fileservers/metricsDefinitions/read|Возвращает определения показателей hello или список|
|/managers/devices/timeSettings/read|Возвращает параметры времени hello или список|
|/managers/devices/timeSettings/write|Создает или обновляет параметры времени.|
|/Managers/certificates/write|Операция обновления ресурса сертификата Hello обновляет сертификат учетных данных ресурсов или хранилища hello.|
|/managers/cloudApplianceConfigurations/read|Список hello облака Appliance поддерживаемые конфигурации|
|/managers/metricsDefinitions/read|Возвращает определения показателей hello или список|
|/managers/encryptionSettings/read|Получает параметры шифрования hello или список|

## <a name="microsoftstreamanalytics"></a>Microsoft.StreamAnalytics

| Операция | Описание |
|---|---|
|/streamingjobs/Start/action|Запускает задание Stream Analytics.|
|/streamingjobs/Stop/action|Останавливает задание Stream Analytics.|
|/streamingjobs/Read|Считывает задание Stream Analytics.|
|/streamingjobs/Write|Записывает задание Stream Analytics.|
|/streamingjobs/Delete|Удаляет задание Stream Analytics.|
|/streamingjobs/providers/Microsoft.Insights/metricDefinitions/read|Получает доступные метрики hello для streamingjobs|
|/streamingjobs/providers/Microsoft.Insights/diagnosticSettings/read|Считывает параметр диагностики.|
|/streamingjobs/providers/Microsoft.Insights/diagnosticSettings/write|Записывает параметр диагностики.|
|/streamingjobs/providers/Microsoft.Insights/logDefinitions/read|Получает доступные журналы hello для streamingjobs|
|/streamingjobs/transformations/Read|Считывает преобразование задания Stream Analytics.|
|/streamingjobs/transformations/Write|Записывает преобразование задания Stream Analytics.|
|/streamingjobs/transformations/Delete|Удаляет преобразование задания Stream Analytics.|
|/streamingjobs/inputs/Read|Считывает входные данные задания Stream Analytics.|
|/streamingjobs/inputs/Write|Записывает входные данные задания Stream Analytics.|
|/streamingjobs/inputs/Delete|Удаляет входные данные задания Stream Analytics.|
|/streamingjobs/outputs/Read|Считывает выходные данные задания Stream Analytics.|
|/streamingjobs/outputs/Write|Записывает выходные данные задания Stream Analytics.|
|/streamingjobs/outputs/Delete|Удаляет выходные данные задания Stream Analytics.|

## <a name="microsoftsupport"></a>Microsoft.Support

| Операция | Описание |
|---|---|
|/register/action|Регистрирует поставщика ресурсов tooSupport|
|/supportTickets/read|Возвращает подробные сведения в службу поддержки (включая состояние, серьезности, контактные сведения и сообщения) или получает список hello запросов в службу поддержки между подписками.|
|/supportTickets/write|Создает или обновляет запрос в службу поддержки. Можно создавать запросы в службу поддержки по техническим проблемам, а также проблемам, связанным с выставлением счетов, квотами или управлением подписками. Вы можете изменить уровень серьезности, контактную информацию и сообщения для существующих запросов в службу поддержки.|

## <a name="microsoftweb"></a>Microsoft.Web

| Операция | Описание |
|---|---|
|/unregister/action|Отмена регистрации поставщика ресурсов Microsoft.Web для hello подписки.|
|/validate/action|Выполняет проверку.|
|/register/action|Регистрация поставщика ресурсов Microsoft.Web для hello подписки.|
|/hostingEnvironments/Read|Получение свойств hello среды службы приложений|
|/hostingEnvironments/Write|Создает новую среду службы приложений или обновляет существующую.|
|/hostingEnvironments/Delete|Удаляет среду службы приложений.|
|/hostingEnvironments/reboot/Action|Перезагружает все компьютеры в среде службы приложений.|
|/hostingenvironments/resume/action|Возобновляет работу сред внешнего размещения.|
|/hostingenvironments/suspend/action|Приостанавливает работу сред внешнего размещения.|
|/hostingenvironments/metricdefinitions/read|Возвращает определения метрик сред внешнего размещения.|
|/hostingEnvironments/workerPools/Read|Получение свойств hello пула Worker в среде службы приложений|
|/hostingEnvironments/workerPools/Write|Создает новый рабочий пул в среде службы приложений или обновляет существующий.|
|/hostingenvironments/workerpools/metricdefinitions/read|Возвращает определения метрик рабочих пулов в средах внешнего размещения.|
|/hostingenvironments/workerpools/metrics/read|Возвращает метрики рабочих пулов в средах внешнего размещения.|
|/hostingenvironments/workerpools/skus/read|Возвращает номера SKU рабочих пулов в средах внешнего размещения.|
|/hostingenvironments/workerpools/usages/read|Возвращает данные об использовании рабочих пулов в средах внешнего размещения.|
|/hostingenvironments/sites/read|Возвращает веб-приложения в средах внешнего размещения.|
|/hostingenvironments/serverfarms/read|Возвращает планы службы приложений в средах внешнего размещения.|
|/hostingenvironments/usages/read|Возвращает данные об использовании сред внешнего размещения.|
|/hostingenvironments/capacities/read|Возвращает емкости сред внешнего размещения.|
|/hostingenvironments/operations/read|Возвращает операции сред внешнего размещения.|
|/hostingEnvironments/multiRolePools/Read|Получение свойств hello пула переднего плана в среде службы приложений|
|/hostingEnvironments/multiRolePools/Write|Создает новый интерфейсный пул в среде службы приложений или обновляет существующий.|
|/hostingenvironments/multirolepools/metricdefinitions/read|Возвращает определения метрик пулов множественных ролей в средах внешнего размещения.|
|/hostingenvironments/multirolepools/metrics/read|Возвращает метрики пулов множественных ролей в средах внешнего размещения.|
|/hostingenvironments/multirolepools/skus/read|Возвращает номера SKU пулов множественных ролей в средах внешнего размещения.|
|/hostingenvironments/multirolepools/usages/read|Возвращает данные об использовании пулов множественных ролей в средах внешнего размещения.|
|/hostingenvironments/diagnostics/read|Возвращает данные диагностики сред внешнего размещения.|
|/publishingusers/read|Возвращает публикующих пользователей.|
|/publishingusers/write|Обновляет публикующих пользователей.|
|/checknameavailability/read|Проверяет, доступно ли имя ресурса.|
|/geoRegions/Read|Получите список hello географических регионов.|
|/sites/Read|Получение свойств hello веб-приложения|
|/sites/Write|Создает новое веб-приложение или обновляет существующее.|
|/sites/Delete|Удаление существующего веб-приложения|
|/sites/backup/Action|Создает резервную копию веб-приложения.|
|/sites/publishxml/Action|Возвращает XML-файл профиля публикации для веб-приложения.|
|/sites/publish/Action|Публикует веб-приложение.|
|/sites/restart/Action|Перезапускает веб-приложение.|
|/sites/start/Action|Запускает веб-приложение.|
|/sites/stop/Action|Останавливает веб-приложение.|
|/sites/slotsswap/Action|Переключает слоты развертывания веб-приложения.|
|/sites/slotsdiffs/Action|Возвращает различия конфигураций веб-приложения и слотов.|
|/sites/applySlotConfig/Action|Применить конфигурацию веб-приложения слот, из целевого слота toohello текущего веб-приложения|
|/sites/resetSlotConfig/Action|Сбрасывает конфигурацию веб-приложения.|
|/sites/functions/action|Выполняет функции веб-приложений.|
|/sites/listsyncfunctiontriggerstatus/action|Отображает состояние триггера функции синхронизации для веб-приложений.|
|/sites/networktrace/action|Трассирует сеть для веб-приложений.|
|/sites/newpassword/action|Задает новый пароль для веб-приложений.|
|/sites/sync/action|Синхронизирует веб-приложения.|
|/sites/operationresults/read|Возвращает результаты операций веб-приложений.|
|/sites/webjobs/read|Возвращает веб-задания веб-приложений.|
|/sites/backup/read|Возвращает резервную копию веб-приложений.|
|/sites/backup/write|Обновляет резервную копию веб-приложений.|
|/sites/metricdefinitions/read|Возвращает определения метрик веб-приложений.|
|/sites/metrics/read|Возвращает метрики веб-приложений.|
|/sites/continuouswebjobs/delete|Удаляет непрерывные веб-задания веб-приложений.|
|/sites/continuouswebjobs/read|Возвращает непрерывные веб-задания веб-приложений.|
|/sites/continuouswebjobs/start/action|Запускает непрерывные веб-задания веб-приложений.|
|/sites/continuouswebjobs/stop/action|Останавливает непрерывные веб-задания веб-приложений.|
|/sites/domainownershipidentifiers/read|Возвращает идентификаторы владения доменом веб-приложений.|
|/sites/domainownershipidentifiers/write|Обновляет идентификаторы владения доменом веб-приложений.|
|/sites/premieraddons/delete|Удаляет надстройки Premier для веб-приложений.|
|/sites/premieraddons/read|Возвращает надстройки Premier для веб-приложений.|
|/sites/premieraddons/write|Обновляет надстройки Premier для веб-приложений.|
|/sites/triggeredwebjobs/delete|Удаляет активированные веб-задания веб-приложений.|
|/sites/triggeredwebjobs/read|Возвращает активированные веб-задания веб-приложений.|
|/sites/triggeredwebjobs/run/action|Выполняет активированные веб-задания веб-приложений.|
|/sites/hostnamebindings/delete|Удаляет привязки имен узлов для веб-приложений.|
|/sites/hostnamebindings/read|Возвращает привязки имен узлов для веб-приложений.|
|/sites/hostnamebindings/write|Обновляет привязки имен узлов для веб-приложений.|
|/sites/virtualnetworkconnections/delete|Удаляет подключения виртуальных сетей веб-приложений.|
|/sites/virtualnetworkconnections/read|Возвращает подключения виртуальных сетей веб-приложений.|
|/sites/virtualnetworkconnections/write|Обновляет подключения виртуальных сетей веб-приложений.|
|/sites/virtualnetworkconnections/gateways/read|Возвращает шлюзы подключений виртуальных сетей веб-приложений.|
|/sites/virtualnetworkconnections/gateways/write|Обновляет шлюзы подключений виртуальных сетей веб-приложений.|
|/sites/publishxml/read|Возвращает XML-файл профиля публикации для веб-приложений.|
|/sites/hybridconnectionrelays/read|Возвращает ретрансляторы гибридных подключений для веб-приложений.|
|/sites/perfcounters/read|Возвращает счетчики производительности веб-приложений.|
|/sites/usages/read|Возвращает данные об использовании веб-приложений.|
|/sites/slots/Write|Создает новый слот веб-приложения или обновляет существующий.|
|/sites/slots/Delete|Удаляет существующий слот веб-приложения.|
|/sites/slots/backup/Action|Создает резервную копию слота веб-приложения.|
|/sites/slots/publishxml/Action|Возвращает XML-файл профиля публикации для слота веб-приложения.|
|/sites/slots/publish/Action|Публикует слот веб-приложения.|
|/sites/slots/restart/Action|Перезапускает слот веб-приложения.|
|/sites/slots/start/Action|Запускает слот веб-приложения.|
|/sites/slots/stop/Action|Останавливает слот веб-приложения.|
|/sites/slots/slotsswap/Action|Переключает слоты развертывания веб-приложения.|
|/sites/slots/slotsdiffs/Action|Возвращает различия конфигураций веб-приложения и слотов.|
|/sites/slots/applySlotConfig/Action|Примените конфигурацию веб-приложения слот, из целевой слот toohello текущей области.|
|/sites/slots/resetSlotConfig/Action|Сбрасывает конфигурацию слота веб-приложения.|
|/sites/slots/Read|Получение свойств hello слота развертывания веб-приложения|
|/sites/slots/newpassword/action|Задает новый пароль для слотов веб-приложений.|
|/sites/slots/sync/action|Синхронизирует слоты веб-приложений.|
|/sites/slots/operationresults/read|Возвращает результаты операций слотов веб-приложений.|
|/sites/slots/webjobs/read|Возвращает веб-задания слотов веб-приложений.|
|/sites/slots/backup/write|Обновляет резервную копию слотов веб-приложений.|
|/sites/slots/metricdefinitions/read|Возвращает определения метрик слотов веб-приложений.|
|/sites/slots/metrics/read|Возвращает метрики слотов веб-приложений.|
|/sites/slots/continuouswebjobs/delete|Удаляет непрерывные веб-задания слотов веб-приложений.|
|/sites/slots/continuouswebjobs/read|Возвращает непрерывные веб-задания слотов веб-приложений.|
|/sites/slots/continuouswebjobs/start/action|Запускает непрерывные веб-задания слотов веб-приложений.|
|/sites/slots/continuouswebjobs/stop/action|Останавливает непрерывные веб-задания слотов веб-приложений.|
|/sites/slots/premieraddons/delete|Удаляет надстройки Premier для слотов веб-приложений.|
|/sites/slots/premieraddons/read|Возвращает надстройки Premier для слотов веб-приложений.|
|/sites/slots/premieraddons/write|Обновляет надстройки Premier для слотов веб-приложений.|
|/sites/slots/triggeredwebjobs/delete|Удаляет активированные веб-задания слотов веб-приложений.|
|/sites/slots/triggeredwebjobs/read|Возвращает активированные веб-задания слотов веб-приложений.|
|/sites/slots/triggeredwebjobs/run/action|Выполняет активированные веб-задания слотов веб-приложений.|
|/sites/slots/hostnamebindings/delete|Удаляет привязки имен узлов для слотов веб-приложений.|
|/sites/slots/hostnamebindings/read|Возвращает привязки имен узлов для слотов веб-приложений.|
|/sites/slots/hostnamebindings/write|Обновляет привязки имен узлов для слотов веб-приложений.|
|/sites/slots/phplogging/read|Возвращает сведения о ведении журнала PHP для слотов веб-приложений.|
|/sites/slots/virtualnetworkconnections/delete|Удаляет подключения виртуальных сетей для слотов веб-приложений.|
|/sites/slots/virtualnetworkconnections/read|Возвращает подключения виртуальных сетей для слотов веб-приложений.|
|/sites/slots/virtualnetworkconnections/write|Обновляет подключения виртуальных сетей для слотов веб-приложений.|
|/sites/slots/virtualnetworkconnections/gateways/write|Обновляет шлюзы подключений виртуальных сетей для слотов веб-приложений.|
|/sites/slots/usages/read|Возвращает данные об использовании слотов веб-приложений.|
|/sites/slots/hybridconnection/delete|Удаляет гибридное подключение для слотов веб-приложений.|
|/sites/slots/hybridconnection/read|Возвращает гибридное подключение для слотов веб-приложений.|
|/sites/slots/hybridconnection/write|Обновляет гибридное подключение для слотов веб-приложений.|
|/sites/slots/config/Read|Возвращает параметры конфигурации слота веб-приложения.|
|/sites/slots/config/list/Action|Отображает влияющие на безопасность параметры слота веб-приложения, такие как учетные данные для публикации, параметры приложения и строки подключения.|
|/sites/slots/config/Write|Обновляет параметры конфигурации слота веб-приложения.|
|/sites/slots/config/delete|Удаляет конфигурацию слотов веб-приложений.|
|/sites/slots/instances/read|Возвращает экземпляры слотов веб-приложений.|
|/sites/slots/instances/processes/read|Возвращает процессы экземпляры слотов веб-приложений.|
|/sites/slots/instances/deployments/read|Возвращает развертывания экземпляры слотов веб-приложений.|
|/sites/slots/sourcecontrols/Read|Возвращает параметры конфигурации системы управления версиями для слота веб-приложения.|
|/sites/slots/sourcecontrols/Write|Обновляет параметры конфигурации системы управления версиями для слота веб-приложения.|
|/sites/slots/sourcecontrols/Delete|Удаляет параметры конфигурации системы управления версиями для слота веб-приложения.|
|/sites/slots/restore/read|Возвращает данные о восстановлении слотов веб-приложений.|
|/sites/slots/analyzecustomhostname/read|Возвращает результаты анализа пользовательского имени узла для слотов веб-приложений.|
|/sites/slots/backups/Read|Получение свойств hello резервного копирования слоты веб-приложения|
|/sites/slots/backups/list/action|Выводит список резервных копий слотов веб-приложений.|
|/sites/slots/backups/restore/action|Восстанавливает резервные копии слотов веб-приложений.|
|/sites/slots/deployments/delete|Удаляет развертывания слотов веб-приложений.|
|/sites/slots/deployments/read|Возвращает развертывания слотов веб-приложений.|
|/sites/slots/deployments/write|Обновляет развертывания слотов веб-приложений.|
|/sites/slots/deployments/log/read|Возвращает журнал развертываний слотов веб-приложений.|
|/sites/hybridconnection/delete|Удаляет гибридное подключение для веб-приложений.|
|/sites/hybridconnection/read|Возвращает гибридное подключение для веб-приложений.|
|/sites/hybridconnection/write|Обновляет гибридное подключение для веб-приложений.|
|/sites/recommendationhistory/read|Возвращает журнал рекомендаций для веб-приложения.|
|/sites/recommendations/Read|Получите список hello рекомендаций для веб-приложения.|
|/sites/recommendations/disable/action|Отключает рекомендации для веб-приложений.|
|/sites/config/Read|Возвращает параметры конфигурации веб-приложения.|
|/sites/config/list/Action|Отображает влияющие на безопасность параметры веб-приложения, такие как учетные данные для публикации, параметры приложения и строки подключения.|
|/sites/config/Write|Обновляет параметры конфигурации веб-приложения.|
|/sites/config/delete|Удаляет конфигурацию веб-приложений.|
|/sites/instances/read|Возвращает экземпляры веб-приложений.|
|/sites/instances/processes/delete|Удаляет процессы экземпляров веб-приложений.|
|/sites/instances/processes/read|Возвращает процессы экземпляров веб-приложений.|
|/sites/instances/deployments/read|Возвращает развертывания экземпляров веб-приложений.|
|/sites/sourcecontrols/Read|Возвращает параметры конфигурации системы управления версиями веб-приложения.|
|/sites/sourcecontrols/Write|Обновляет параметры конфигурации системы управления версиями веб-приложения.|
|/sites/sourcecontrols/Delete|Удаляет параметры конфигурации системы управления версиями веб-приложения.|
|/sites/restore/read|Возвращает данные о восстановлении веб-приложений.|
|/sites/analyzecustomhostname/read|Анализирует пользовательское имя узла.|
|/sites/backups/Read|Получение свойств hello резервного копирования веб-приложения|
|/sites/backups/list/action|Выводит список резервных копий веб-приложений.|
|/sites/backups/restore/action|Восстанавливает резервные копии веб-приложений.|
|/sites/snapshots/read|Возвращает моментальные снимки веб-приложений.|
|/sites/functions/delete|Удаляет функции веб-приложений.|
|/sites/functions/listsecrets/action|Выводит список секретов для функций веб-приложений.|
|/sites/functions/read|Возвращает функции веб-приложений.|
|/sites/functions/write|Обновляет функции веб-приложений.|
|/sites/deployments/delete|Удаляет развертывания веб-приложений.|
|/sites/deployments/read|Возвращает развертывания веб-приложений.|
|/sites/deployments/write|Обновляет развертывания веб-приложений.|
|/sites/deployments/log/read|Возвращает журнал развертываний веб-приложений.|
|/sites/diagnostics/read|Возвращает данные диагностики веб-приложений.|
|/sites/diagnostics/workerprocessrecycle/read|Возвращает данные диагностики перезапуска рабочих процессов для веб-приложений.|
|/sites/diagnostics/workeravailability/read|Возвращает данные диагностики о доступности рабочих процессов для веб-приложений.|
|/sites/diagnostics/runtimeavailability/read|Возвращает данные диагностики о доступности среды выполнения для веб-приложений.|
|/sites/diagnostics/cpuanalysis/read|Возвращает данные диагностики об анализе ЦП для веб-приложений.|
|/sites/diagnostics/servicehealth/read|Возвращает данные диагностики о работоспособности служб для веб-приложений.|
|/sites/diagnostics/frebanalysis/read|Возвращает данные диагностики об анализе FREB для веб-приложений.|
|/availablestacks/read|Возвращает доступные стеки.|
|/isusernameavailable/read|Проверяет, доступно ли имя пользователя.|
|/Microsoft.Web/apiManagementAccounts/<br>apis/Read|Получите список hello API.|
|/Microsoft.Web/apiManagementAccounts/<br>apis/Write|Добавляет новый API или обновляет существующий.|
|/Microsoft.Web/apiManagementAccounts/<br>apis/Delete|Удаляет существующий API.|
|/Microsoft.Web/apiManagementAccounts/<br>apis/connections/Read|Получите список соединений hello.|
|/Microsoft.Web/apiManagementAccounts/<br>apis/connections/Write|Сохраняет новое подключение или обновляет существующее.|
|/Microsoft.Web/apiManagementAccounts/<br>apis/connections/Delete|Удаляет существующее подключение.|
|/Microsoft.Web/apiManagementAccounts/<br>apis/connections/connectionAcls/Read|Считывает списки управления доступом подключения.|
|/Microsoft.Web/apiManagementAccounts/<br>apis/connections/connectionAcls/Write|Добавляет или обновляет список управления доступом подключения.|
|/Microsoft.Web/apiManagementAccounts/<br>apis/connections/connectionAcls/Delete|Удаляет список управления доступом подключения.|
|/Microsoft.Web/apiManagementAccounts/<br>apis/connectionAcls/Read|Считывает списки управления доступом подключения для API.|
|/Microsoft.Web/apiManagementAccounts/<br>apis/apiAcls/Read|Считывает списки управления доступом подключения.|
|/Microsoft.Web/apiManagementAccounts/<br>apis/apiAcls/Write|Создает или обновляет списки управления доступом API.|
|/Microsoft.Web/apiManagementAccounts/<br>apis/apiAcls/Delete|Удаляет списки управления доступом API.|
|/serverfarms/Read|Получение свойств hello на план служб приложений|
|/serverfarms/Write|Создает новый план службы приложений или обновляет существующий.|
|/serverfarms/Delete|Удаление существующего плана службы приложений|
|/serverfarms/restartSites/Action|Перезапустите все веб-приложения в плане службы приложений.|
|/serverfarms/operationresults/read|Возвращает результаты операций планов службы приложений.|
|/serverfarms/capabilities/read|Возвращает возможности планов службы приложений.|
|/serverfarms/metricdefinitions/read|Возвращает определения метрик планов службы приложений.|
|/serverfarms/metrics/read|Возвращает метрики планов службы приложений.|
|/serverfarms/hybridconnectionplanlimits/read|Возвращает ограничения плана гибридных подключений для плана службы приложений.|
|/serverfarms/virtualnetworkconnections/read|Возвращает подключения виртуальной сети для планов службы приложений.|
|/serverfarms/virtualnetworkconnections/routes/delete|Удаляет маршруты подключений виртуальной сети для планов службы приложений.|
|/serverfarms/virtualnetworkconnections/routes/read|Возвращает маршруты подключений виртуальной сети для планов службы приложений.|
|/serverfarms/virtualnetworkconnections/routes/write|Обновляет маршруты подключений виртуальной сети для планов службы приложений.|
|/serverfarms/virtualnetworkconnections/gateways/write|Обновляет шлюзы подключений виртуальной сети для планов службы приложений.|
|/serverfarms/firstpartyapps/settings/delete|Удаляет параметры основных приложений в планах службы приложений.|
|/serverfarms/firstpartyapps/settings/read|Возвращает параметры основных приложений в планах службы приложений.|
|/serverfarms/firstpartyapps/settings/write|Обновляет параметры основных приложений в планах службы приложений.|
|/serverfarms/sites/read|Возвращает веб-приложения в планах службы приложений.|
|/serverfarms/workers/reboot/action|Перезапускает рабочие роли планов службы приложений.|
|/serverfarms/hybridconnectionrelays/read|Возвращает ретрансляторы гибридных подключений для планов службы приложений.|
|/serverfarms/skus/read|Возвращает номера SKU в планах службы приложений.|
|/serverfarms/usages/read|Возвращает данные об использовании для планов службы приложений.|
|/serverfarms/hybridconnectionnamespaces/relays/sites/read|Возвращает веб-приложения ретрансляторов в пространствах имен гибридных подключений для плана службы приложений.|
|/ishostnameavailable/read|Проверяет, доступно ли имя узла.|
|/connectionGateways/Read|Получите список соединений шлюзы hello.|
|/connectionGateways/Write|Создает или обновляет шлюз для подключения.|
|/connectionGateways/Delete|Удаляет шлюз подключения.|
|/connectionGateways/Join/Action|Присоединяет шлюз подключения.|
|/classicmobileservices/read|Возвращает классические мобильные службы.|
|/skus/read|Возвращает номера SKU.|
|/certificates/Read|Получите список сертификатов hello.|
|/certificates/Write|Добавляет новый сертификат или обновляет существующий.|
|/certificates/Delete|Удаляет существующий сертификат.|
|/operations/read|Возвращает операции.|
|/recommendations/Read|Получите список hello рекомендаций для подписок.|
|/ishostingenvironmentnameavailable/read|Проверяет, доступно ли имя среды внешнего размещения.|
|/apiManagementAccounts/Read|Получите список ApiManagementAccounts hello.|
|/apiManagementAccounts/Write|Добавляет новую учетную запись управления API или обновляет существующую.|
|/apiManagementAccounts/Delete|Удаляет существующую учетную запись управления API.|
|/apiManagementAccounts/connectionAcls/Read|Получите список hello списков управления доступом для подключения.|
|/apiManagementAccounts/apiAcls/Read|Считывает списки управления доступом подключения.|
|/connections/Read|Получите список соединений hello.|
|/connections/Write|Создает или обновляет подключение.|
|/connections/Delete|Удаляет подключение.|
|/connections/Join/Action|Присоединяет подключение.|
|/connections/confirmconsentcode/action|Подтверждает код согласия на подключение.|
|/connections/listconsentlinks/action|Выводит список ссылок на согласие для подключений.|
|/deploymentlocations/read|Возвращает расположения развертываний.|
|/sourcecontrols/read|Возвращает систему управления версиями.|
|/sourcecontrols/write|Обновляет системы управления версиями.|
|/managedhostingenvironments/read|Возвращает управляемые среды внешнего размещения.|
|/managedhostingenvironments/sites/read|Возвращает веб-приложения в управляемых средах внешнего размещения.|
|/managedhostingenvironments/serverfarms/read|Возвращает планы службы приложений в управляемых средах внешнего размещения.|
|/locations/managedapis/read|Возвращает расположения управляемых интерфейсов API.|
|/locations/apioperations/read|Возвращает операции API расположений.|
|/locations/connectiongatewayinstallations/read|Возвращает данные об установленных шлюзах подключений в расположениях.|
|/listSitesAssignedToHostName/Read|Получите имена узлов, назначенных toohostname.|

## <a name="next-steps"></a>Дальнейшие действия

- Узнайте, каким образом слишком[создайте пользовательскую роль](role-based-access-control-custom-roles.md).

- Просмотрите hello [встроенные роли RBAC](role-based-access-built-in-roles.md).

- Узнайте, как toomanage доступ к назначения [пользователем](role-based-access-control-manage-assignments.md) или [по ресурсам](role-based-access-control-configure.md) 
