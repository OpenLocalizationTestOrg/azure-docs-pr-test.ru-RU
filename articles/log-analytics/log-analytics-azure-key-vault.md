---
title: "решение хранилища ключей в службе анализа журналов aaaAzure | Документы Microsoft"
description: "Можно использовать решение хранилища ключей Azure hello в tooreview аналитики журналов, журналов хранилища ключей Azure."
services: log-analytics
documentationcenter: 
author: richrundmsft
manager: jochan
editor: 
ms.assetid: 5e25e6d6-dd20-4528-9820-6e2958a40dae
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/09/2017
ms.author: richrund
ms.openlocfilehash: 1c6eae26ded7ad55b0159a3be09cdc9901596298
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-key-vault-analytics-solution-in-log-analytics"></a>Решение Azure Key Vault Analytics в Log Analytics

![Символ Key Vault](./media/log-analytics-azure-keyvault/key-vault-analytics-symbol.png)

Можно использовать решение хранилища ключей Azure hello в tooreview аналитики журналов, журналов AuditEvent хранилище ключей Azure.

решение toouse hello, необходимо tooenable ведения журнала диагностики для хранилища ключей Azure и прямой hello диагностики tooa анализа журналов рабочей. Это не hello журналы необходимые toowrite tooAzure-хранилище больших двоичных объектов.

> [!NOTE]
> В января 2017 г hello поддерживается способ отправки журналов из хранилища ключей tooLog Analytics изменено. При использовании решения хранилища ключей hello показывает *(устарело)* в заголовок hello, ссылаетесь слишком[миграция из старого решения хранилища ключей hello](#migrating-from-the-old-key-vault-solution) для действия необходимы toofollow.
>
>

## <a name="install-and-configure-hello-solution"></a>Установка и настройка решения hello
Используйте следующие инструкции tooinstall hello и настроить решение hello хранилище ключей Azure:

1. Включить решение hello хранилище ключей Azure из [Azure marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.KeyVaultAnalyticsOMS?tab=Overview) или с помощью hello процесс, описанный в [решений добавьте анализа журналов из коллекции решений hello](log-analytics-add-solutions.md).
2. Включение диагностики ведения журнала для toomonitor ресурсы hello хранилище ключей, с помощью либо hello [портала](#enable-key-vault-diagnostics-in-the-portal) или [PowerShell](#enable-key-vault-diagnostics-using-powershell)

### <a name="enable-key-vault-diagnostics-in-hello-portal"></a>Включение диагностики хранилища ключей на портале hello

1. Hello портал Azure перейдите toomonitor ресурсов toohello хранилища ключей
2. Выберите *журналы диагностики* после страницы приветствия tooopen

   ![изображение плитки "Хранилище ключей Azure"](./media/log-analytics-azure-keyvault/log-analytics-keyvault-enable-diagnostics01.png)
3. Нажмите кнопку *включить диагностику* после страницы приветствия tooopen

   ![изображение плитки "Хранилище ключей Azure"](./media/log-analytics-azure-keyvault/log-analytics-keyvault-enable-diagnostics02.png)
4. Щелкните tooturn диагностику, *на* под *состояния*
5. Щелкните флажок hello *отправки tooLog аналитика*
6. Выберите существующую рабочую область Log Analytics или создайте новую.
7. tooenable *AuditEvent* журналы, установите флажок hello в журнал
8. Нажмите кнопку *Сохранить* tooenable hello ведение журнала диагностики tooLog аналитика

### <a name="enable-key-vault-diagnostics-using-powershell"></a>Включение диагностики Key Vault с помощью PowerShell
Hello следующий скрипт PowerShell приведен пример того, как toouse `Set-AzureRmDiagnosticSetting` tooenable ведения журналов диагностики для хранилища ключей:
```
$workspaceId = "/subscriptions/d2e37fee-1234-40b2-5678-0b2199de3b50/resourcegroups/oi-default-east-us/providers/microsoft.operationalinsights/workspaces/rollingbaskets"

$kv = Get-AzureRmKeyVault -VaultName 'ContosoKeyVault'

Set-AzureRmDiagnosticSetting -ResourceId $kv.ResourceId  -WorkspaceId $workspaceId -Enabled $true
```



## <a name="review-azure-key-vault-data-collection-details"></a>Просмотр сведений о сборе данных хранилища ключей Azure
Решение хранилища ключей Azure собирает журналы диагностики непосредственно из хранилища ключей hello.
Не является tooAzure журналы hello необходимые toowrite хранилища больших двоичных объектов и агент не требуется для сбора данных.

Hello следующей таблице приведены методы сбора данных и другие сведения о сборе данных для хранилища ключей Azure.

| Платформа | Direct Agent | Агент Systems Center Operations Manager | Таблицы Azure | Нужен ли Operations Manager? | Отправка данных агента Operations Manager через группу управления | Частота сбора |
| --- | --- | --- | --- | --- | --- | --- |
| Таблицы Azure |  |  |&#8226; |  |  | при получении |

## <a name="use-azure-key-vault"></a>Использование хранилища ключей Azure
По окончании [установки решения hello](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.KeyVaultAnalyticsOMS?tab=Overview), просматривать данные хранилища ключей hello, щелкнув hello **хранилище ключей Azure** плитки из hello **Обзор** страницы аналитики журналов.

![изображение плитки "Хранилище ключей Azure"](./media/log-analytics-azure-keyvault/log-analytics-keyvault-tile.png)

После нажатия кнопки hello **Обзор** плитки, можно просмотреть сводные данные журналов и затем в toodetails для hello, следующие категории:

* количество всех операций хранилища ключей за определенный период;
* количество неудавшихся операций за определенный период;
* среднее время задержки для каждой операции;
* Качество обслуживания для операций с hello количество операций, которые занимают более 1 000 мс и список операций, которые занимают более 1 000 мс.

![изображение панели мониторинга хранилища ключей Azure](./media/log-analytics-azure-keyvault/log-analytics-keyvault01.png)

![изображение панели мониторинга хранилища ключей Azure](./media/log-analytics-azure-keyvault/log-analytics-keyvault02.png)

### <a name="tooview-details-for-any-operation"></a>сведения о tooview для любой операции
1. На hello **Обзор** щелкните hello **хранилище ключей Azure** плитки.
2. На hello **хранилище ключей Azure** панели мониторинга, просмотрите сводные сведения о hello в одной из колонок hello и выберите один tooview подробные сведения о нем в hello страницы поиска журналов.

    На любой из страниц поиска журналов hello можно просмотреть результаты по времени, подробные результаты и историю поиска журналов. Можно также фильтровать по результатам hello toonarrow аспектов.

## <a name="log-analytics-records"></a>Записи Log Analytics
Hello решения хранилища ключей Azure анализирует записей, имеющих тип **KeyVaults** , получаемые от [AuditEvent журналы](../key-vault/key-vault-logging.md) в системе диагностики Azure.  В следующей таблице hello имеют свойства для этих записей:  

| Свойство | Описание |
|:--- |:--- |
| Тип |*AzureDiagnostics* |
| SourceSystem |*Таблицы Azure* |
| CallerIpAddress |IP-адрес клиента hello, сделавшего запрос hello |
| Категория | *AuditEvent* |
| CorrelationId |Необязательный идентификатор GUID, который hello клиента можно передать toocorrelate клиентские журналы с журналами (хранилище ключей) на стороне службы. |
| DurationMs |Время, затраченное запроса REST API tooservice hello, в миллисекундах. Это время не включает задержки в сети, поэтому это время может не совпадать с моментом hello мер на стороне клиента hello. |
| HttpStatusCode_d |Код состояния HTTP, возвращаемый запросом hello (например, *200*) |
| id_s |Уникальный идентификатор запроса hello |
| identity_claim_appid_g | Идентификатор GUID для идентификатора приложения hello |
| OperationName |Имя операции hello, как описано в документе [ведение журнала хранилища ключей Azure](../key-vault/key-vault-logging.md) |
| OperationVersion |Версия REST API, необходимая для клиента hello (например *2015-06-01*) |
| requestUri_s |URI запроса hello |
| Ресурс |Имя хранилища ключей hello |
| ResourceGroup |Группа ресурсов хранилища ключей hello |
| ResourceId |Идентификатор ресурса диспетчера ресурсов Azure. Для журналов хранилища ключей это hello хранилище ключей, идентификатор ресурса. |
| ResourceProvider |*MICROSOFT.KEYVAULT* |
| ResourceType | *VAULTS* |
| ResultSignature |Код состояния HTTP (например, *ОК*) |
| ResultType |Результат запроса REST API (например, *Успешно*) |
| SubscriptionId |Идентификатор подписки Azure hello подписку, содержащую hello хранилища ключей |

## <a name="migrating-from-hello-old-key-vault-solution"></a>Миграция из старого решения хранилища ключей hello
В января 2017 г hello поддерживается способ отправки журналов из хранилища ключей tooLog Analytics изменено. Эти изменения обеспечивают hello следующие преимущества:
+ Журналы записываются напрямую tooLog Analytics без hello требуется toouse учетной записи хранения
+ Меньше задержка из hello время, когда журналы, созданные toothem, недоступными в службе анализа журналов
+ Меньше этапов настройки.
+ Общий формат для всех типов системы диагностики Azure.

toouse hello обновление решения:

1. [Настройка диагностики toobe tooLog Analytics отправляется непосредственно из хранилища ключей](#enable-key-vault-diagnostics-in-the-portal)  
2. Включить решение hello хранилище ключей Azure с помощью hello процесс, описанный в [решений добавьте анализа журналов из hello коллекции решений](log-analytics-add-solutions.md)
3. Обновить все сохраненные запросы, панели мониторинга и новый тип данных оповещения toouse hello
  + Тип — изменение с: KeyVaults tooAzureDiagnostics. Можно использовать hello ResourceType toofilter tooKey хранилище журналов.
  - Вместо `Type=KeyVaults` используйте `Type=AzureDiagnostics ResourceType=VAULTS`.
  + Поля (в именах полей учитывается регистр).
  - Для любого поля, имеет суффикс \_s, \_d, или \_g в поле имя hello hello первый символ toolower регистр
  - Для любого поля, имеет суффикс \_«o» в имени hello данных разбивается на отдельные поля на основе имен hello вложенные поля. Например hello UPN вызывающему Привет хранится в поле`identity_claim_http_schemas_xmlsoap_org_ws_2005_05_identity_claims_upn_s`
   - TooCallerIPAddress CallerIpAddress поля изменен
   - Поле RemoteIPCountry больше не используется.
4. Удалите hello *аналитика хранилища ключей (не рекомендуется)* решения. Если используется PowerShell, то выполните следующую команду: `Set-AzureOperationalInsightsIntelligencePack -ResourceGroupName <resource group that hello workspace is in> -WorkspaceName <name of hello log analytics workspace> -IntelligencePackName "KeyVault" -Enabled $false`

Данные, собранные до вызова hello изменений не отображается в новом решении hello. Вы можете продолжить tooquery для этого данные с помощью hello и старый тип и имена полей.

## <a name="troubleshooting"></a>Устранение неполадок
[!INCLUDE [log-analytics-troubleshoot-azure-diagnostics](../../includes/log-analytics-troubleshoot-azure-diagnostics.md)]

## <a name="next-steps"></a>Дальнейшие действия
* Используйте [входа поиска аналитики журналов](log-analytics-log-searches.md) tooview подробных данных хранилища ключей Azure.
