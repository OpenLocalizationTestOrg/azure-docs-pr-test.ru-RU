---
title: "решения для анализа сети в службе анализа журналов aaaAzure | Документы Microsoft"
description: "Можно использовать hello решения для анализа сети Azure в журналах шлюза приложения Azure и журналы группы безопасности сети Azure tooreview анализа журналов."
services: log-analytics
documentationcenter: 
author: richrundmsft
manager: ewinner
editor: 
ms.assetid: 66a3b8a1-6c55-4533-9538-cad60c18f28b
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/09/2017
ms.author: richrund
ms.openlocfilehash: 3674189786bacccc82e6708e78f14c92178e6676
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-networking-monitoring-solutions-in-log-analytics"></a>Решения для мониторинга сетей Azure в Log Analytics

Аналитика журналов предлагает следующие решения для мониторинга сети hello.
* Монитор производительности сети (NPM):
 * Монитор работоспособности hello сети
* Tooreview аналитика Azure шлюза приложений
 * журналы шлюза приложений Azure;
 * метрику шлюза приложений Azure.
* Tooreview аналитика сетевой группы безопасности Azure
 * журналы групп безопасности сети Azure.

## <a name="network-performance-monitor-npm"></a>Монитор производительности сети

Hello [сетевой монитор производительности](log-analytics-network-performance-monitor.md) решение по управлению, решения, отслеживающий hello работоспособности, доступности и возможность сетей мониторинга сети.  Это подключение используется toomonitor между:

* общедоступное облако и локальная среда;
* центры обработки данных и расположения пользователей (филиалы);
* подсети, в которых размещены различные уровни многоуровневого приложения.

Дополнительную информацию см. в статье [Решение монитора производительности сети в Azure Log Analytics](log-analytics-network-performance-monitor.md).

## <a name="azure-application-gateway-and-network-security-group-analytics"></a>Шлюз приложений Azure и анализ групп безопасности сети
решения toouse hello.
1. Добавить tooLog решение управления hello аналитика, и
2. Включение анализа журналов диагностики toodirect hello диагностики tooa рабочей. Это не hello журналы необходимые toowrite tooAzure-хранилище больших двоичных объектов.

Можно включить диагностику и hello соответствующее решение для одного или обоих шлюза приложения и группы безопасности сети.

Если не включить сбор данных диагностики для определенного типа ресурсов, но установка решения hello, колонках hello панели мониторинга для этого ресурса пусты и сообщение об ошибке.

> [!NOTE]
> В января 2017 г hello поддерживается способ отправки журналов из шлюзы приложений и группы безопасности сети tooLog Analytics изменено. Если вы видите hello **анализа сети Azure (устарело)** решения, ссылаться слишком[миграция из старого решения сети Analytics hello](#migrating-from-the-old-networking-analytics-solution) для действия необходимы toofollow.
>
>

## <a name="review-azure-networking-data-collection-details"></a>Просмотр сведений о сборе данных о сетях Azure
Шлюз приложений Azure analytics Hello и решений по управлению analytics сетевой группы безопасности hello собирать журналы диагностики непосредственно из шлюзы приложений Azure и группы безопасности сети. Не является tooAzure журналы hello необходимые toowrite хранилища больших двоичных объектов и агент не требуется для сбора данных.

Hello ниже приведены методы сбора данных и другие сведения о сборе данных для анализа шлюза приложения Azure и аналитика hello группы безопасности сети.

| Платформа | Direct Agent | Агент Systems Center Operations Manager | Таблицы Azure | Нужен ли Operations Manager? | Отправка данных агента Operations Manager через группу управления | Частота сбора |
| --- | --- | --- | --- | --- | --- | --- |
| Таблицы Azure |  |  |&#8226; |  |  |при входе |


## <a name="azure-application-gateway-analytics-solution-in-log-analytics"></a>Решение для анализа шлюзов приложений Azure в Log Analytics

![Символ "Аналитика службы приложений Azure"](./media/log-analytics-azure-networking/azure-analytics-symbol.png)

Шлюзы приложений поддерживаются следующие журналы Hello.

* ApplicationGatewayAccessLog
* ApplicationGatewayPerformanceLog
* ApplicationGatewayFirewallLog

Шлюзы приложений поддерживаются следующие метрики Hello.

* пропускная способность за 5 минут.

### <a name="install-and-configure-hello-solution"></a>Установка и настройка решения hello
Используйте следующие инструкции tooinstall hello и настройка решения для анализа hello шлюза приложения Azure:

1. Включить решения для анализа hello шлюза приложения Azure из [Azure marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.AzureAppGatewayAnalyticsOMS?tab=Overview) или с помощью hello процесс, описанный в [решений добавьте анализа журналов из коллекции решений hello](log-analytics-add-solutions.md).
2. Включить ведение журнала диагностики для hello [шлюзы приложений](../application-gateway/application-gateway-diagnostics.md) требуется toomonitor.

#### <a name="enable-azure-application-gateway-diagnostics-in-hello-portal"></a>Включить диагностику шлюза приложения Azure в портале hello

1. Hello портал Azure перейдите toomonitor ресурсов toohello шлюза приложений
2. Выберите *журналы диагностики* после страницы приветствия tooopen

   ![снимок экрана: ресурс шлюза приложений Azure](./media/log-analytics-azure-networking/log-analytics-appgateway-enable-diagnostics01.png)
3. Нажмите кнопку *включить диагностику* после страницы приветствия tooopen

   ![снимок экрана: ресурс шлюза приложений Azure](./media/log-analytics-azure-networking/log-analytics-appgateway-enable-diagnostics02.png)
4. Щелкните tooturn диагностику, *на* под *состояния*
5. Щелкните флажок hello *отправки tooLog аналитика*
6. Выберите существующую рабочую область Log Analytics или создайте новую.
7. Установите флажок hello под **журнала** для каждого из типов toocollect hello журнала
8. Нажмите кнопку *Сохранить* tooenable hello ведение журнала диагностики tooLog аналитика

#### <a name="enable-azure-network-diagnostics-using-powershell"></a>Включение диагностики сети Azure с помощью PowerShell

Hello следующий скрипт PowerShell приведен пример того, как tooenable ведения журналов диагностики для шлюзы приложений.

```powershell
$workspaceId = "/subscriptions/d2e37fee-1234-40b2-5678-0b2199de3b50/resourcegroups/oi-default-east-us/providers/microsoft.operationalinsights/workspaces/rollingbaskets"

$gateway = Get-AzureRmApplicationGateway -Name 'ContosoGateway'

Set-AzureRmDiagnosticSetting -ResourceId $gateway.ResourceId  -WorkspaceId $workspaceId -Enabled $true
```

### <a name="use-azure-application-gateway-analytics"></a>Использование анализа шлюзов приложений Azure
![снимок экрана: элемент "Анализ шлюзов приложений Azure"](./media/log-analytics-azure-networking/log-analytics-appgateway-tile.png)

После нажатия кнопки hello **шлюза приложения Azure analytics** плитки на hello Обзор, можно просмотреть сводные данные журналов и затем можно перейти в toodetails для hello, следующие категории:

* Журналы доступа к шлюзу приложений:
  * ошибки клиента и сервера для журналов доступа шлюза приложений;
  * количество запросов в час для каждого шлюза приложений;
  * количество неудачных запросов в час для каждого шлюза приложений;
  * ошибки агентов пользователя для шлюзов приложений.
* Производительность шлюза приложений:
  * работоспособность узла для шлюза приложений;
  * максимальное количество и 95-й процентиль для неудачных запросов шлюза приложений.

![снимок экрана: панель мониторинга "Анализ шлюзов приложений Azure"](./media/log-analytics-azure-networking/log-analytics-appgateway01.png)

![снимок экрана: панель мониторинга "Анализ шлюзов приложений Azure"](./media/log-analytics-azure-networking/log-analytics-appgateway02.png)

На hello **шлюза приложения Azure analytics** панели мониторинга, просмотрите сводные сведения о hello в одной из колонок hello и выберите один tooview подробные сведения на странице поиска журналов hello.

На любой из страниц поиска журналов hello можно просмотреть результаты по времени, подробные результаты и историю поиска журналов. Можно также фильтровать по результатам hello toonarrow аспектов.


## <a name="azure-network-security-group-analytics-solution-in-log-analytics"></a>Решение для анализа групп безопасности сети Azure в Log Analytics

![Символ "Аналитика групп безопасности сетей Azure"](./media/log-analytics-azure-networking/azure-analytics-symbol.png)

для групп безопасности сети поддерживаются Hello следующие журналы:

* NetworkSecurityGroupEvent
* NetworkSecurityGroupRuleCounter

### <a name="install-and-configure-hello-solution"></a>Установка и настройка решения hello
Используйте следующие инструкции tooinstall hello и настроить решение hello Azure Analytics сети:

1. Включить решения для анализа hello Azure сетевую группу безопасности из [Azure marketplace](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/Microsoft.AzureNSGAnalyticsOMS?tab=Overview) или с помощью hello процесс, описанный в [решений добавьте анализа журналов из коллекции решений hello](log-analytics-add-solutions.md).
2. Включить ведение журнала диагностики для hello [сетевой группы безопасности](../virtual-network/virtual-network-nsg-manage-log.md) toomonitor ресурсов.

### <a name="enable-azure-network-security-group-diagnostics-in-hello-portal"></a>Включение диагностики группы безопасности сети Azure на портале hello

1. Hello портал Azure перейдите toomonitor ресурсов toohello группы безопасности сети
2. Выберите *журналы диагностики* после страницы приветствия tooopen

   ![снимок экрана: ресурс группы безопасности сети Azure](./media/log-analytics-azure-networking/log-analytics-nsg-enable-diagnostics01.png)
3. Нажмите кнопку *включить диагностику* после страницы приветствия tooopen

   ![снимок экрана: ресурс группы безопасности сети Azure](./media/log-analytics-azure-networking/log-analytics-nsg-enable-diagnostics02.png)
4. Щелкните tooturn диагностику, *на* под *состояния*
5. Щелкните флажок hello *отправки tooLog аналитика*
6. Выберите существующую рабочую область Log Analytics или создайте новую.
7. Установите флажок hello под **журнала** для каждого из типов toocollect hello журнала
8. Нажмите кнопку *Сохранить* tooenable hello ведение журнала диагностики tooLog аналитика

### <a name="enable-azure-network-diagnostics-using-powershell"></a>Включение диагностики сети Azure с помощью PowerShell

Hello следующий скрипт PowerShell приведен пример того, как tooenable ведения журналов диагностики для групп безопасности сети
```powershell
$workspaceId = "/subscriptions/d2e37fee-1234-40b2-5678-0b2199de3b50/resourcegroups/oi-default-east-us/providers/microsoft.operationalinsights/workspaces/rollingbaskets"

$nsg = Get-AzureRmNetworkSecurityGroup -Name 'ContosoNSG'

Set-AzureRmDiagnosticSetting -ResourceId $nsg.ResourceId  -WorkspaceId $workspaceId -Enabled $true
```

### <a name="use-azure-network-security-group-analytics"></a>Использование анализа групп безопасности сети Azure
После нажатия кнопки hello **сетевой группы безопасности Azure analytics** плитки на hello Обзор, можно просмотреть сводные данные журналов и затем можно перейти в toodetails для hello, следующие категории:

* Заблокированные потоки группы безопасности сети:
  * правила группы безопасности сети с заблокированными потоками;
  * MAC-адреса c заблокированными потоками.
* Разрешенные потоки группы безопасности сети:
  * правила группы безопасности сети с разрешенными потоками;
  * MAC-адреса c разрешенными потоками.

![снимок экрана: панель мониторинга "Анализ групп безопасности сети Azure"](./media/log-analytics-azure-networking/log-analytics-nsg01.png)

![снимок экрана: панель мониторинга "Анализ групп безопасности сети Azure"](./media/log-analytics-azure-networking/log-analytics-nsg02.png)

На hello **сетевой группы безопасности Azure analytics** панели мониторинга, просмотрите сводные сведения о hello в одной из колонок hello и выберите один tooview подробные сведения на странице поиска журналов hello.

На любой из страниц поиска журналов hello можно просмотреть результаты по времени, подробные результаты и историю поиска журналов. Можно также фильтровать по результатам hello toonarrow аспектов.

## <a name="migrating-from-hello-old-networking-analytics-solution"></a>Миграция из старого решения сети Analytics hello
В января 2017 г hello поддерживается способ отправки журналов из tooLog шлюзы приложений Azure и группы безопасности сети Azure Analytics изменено. Эти изменения обеспечивают hello следующие преимущества:
+ Журналы записываются напрямую tooLog Analytics без hello требуется toouse учетной записи хранения
+ Меньше задержка из hello время, когда журналы, созданные toothem, недоступными в службе анализа журналов
+ Меньше этапов настройки.
+ Общий формат для всех типов системы диагностики Azure.

toouse hello обновление решения:

1. [Настройка диагностики toobe tooLog Analytics отправляется непосредственно из шлюзы приложений Azure](#enable-azure-application-gateway-diagnostics-in-the-portal)
2. [Настройка диагностики toobe tooLog Analytics отправляется непосредственно из групп безопасности сети Azure](#enable-azure-network-security-group-diagnostics-in-the-portal)
2. Включить hello *шлюза приложения Azure Analytics* и hello *аналитика группы безопасности сети Azure* описано решение с помощью процесса hello в [решений добавьте анализа журналов из Hello коллекции решений](log-analytics-add-solutions.md)
3. Обновить все сохраненные запросы, панели мониторинга и новый тип данных оповещения toouse hello
  + Тип — tooAzureDiagnostics. Вы можете использовать сетевые журналы toofilter ResourceType tooAzure hello.

    | Используйте такую замену: | Используйте следующую команду: |
    | --- | --- |
    |`Type=NetworkApplicationgateways OperationName=ApplicationGatewayAccess`| `Type=AzureDiagnostics ResourceType=APPLICATIONGATEWAYS OperationName=ApplicationGatewayAccess` |
    |`Type=NetworkApplicationgateways OperationName=ApplicationGatewayPerformance` | `Type=AzureDiagnostics ResourceType=APPLICATIONGATEWAYS OperationName=ApplicationGatewayPerformance` |
    | `Type=NetworkSecuritygroups` | `Type=AzureDiagnostics ResourceType=NETWORKSECURITYGROUPS` |

   + Для любого поля, имеет суффикс \_s, \_d, или \_g в поле имя hello hello первый символ toolower регистр
   + Для любого поля, имеет суффикс \_«o» в имени hello данных разбивается на отдельные поля на основе имен hello вложенные поля.
4. Удалите hello *анализа сети Azure (не рекомендуется)* решения.
  + Если используется PowerShell, то выполните следующую команду: `Set-AzureOperationalInsightsIntelligencePack -ResourceGroupName <resource group that hello workspace is in> -WorkspaceName <name of hello log analytics workspace> -IntelligencePackName "AzureNetwork" -Enabled $false`

Данные, собранные до вызова hello изменений не отображается в новом решении hello. Вы можете продолжить tooquery для этого данные с помощью hello и старый тип и имена полей.

## <a name="troubleshooting"></a>Устранение неполадок
[!INCLUDE [log-analytics-troubleshoot-azure-diagnostics](../../includes/log-analytics-troubleshoot-azure-diagnostics.md)]

## <a name="next-steps"></a>Дальнейшие действия
* Используйте [входа поиска аналитики журналов](log-analytics-log-searches.md) tooview подробных данных диагностики Azure.
