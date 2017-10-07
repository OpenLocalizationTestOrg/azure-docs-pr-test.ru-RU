---
title: "aaaMonitor доступ к журналов, журналов производительности, работоспособности серверной части и метрики для шлюза приложения | Документы Microsoft"
description: "Узнайте, как tooenable и управление журналы событий и журналы производительности для шлюза приложений"
services: application-gateway
documentationcenter: na
author: amitsriva
manager: rossort
editor: tysonn
tags: azure-resource-manager
ms.assetid: 300628b8-8e3d-40ab-b294-3ecc5e48ef98
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/17/2017
ms.author: amitsriva
ms.openlocfilehash: 36ebf15c28f776158350ef8e73d617ef68e09266
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="back-end-health-diagnostic-logs-and-metrics-for-application-gateway"></a>Работоспособность серверной части, журналы диагностики и метрики для шлюза приложений

С помощью шлюза приложения Azure, можно отслеживать ресурсы hello следующих способов:

* [Тыловой работоспособности](#back-end-health): использование шлюза приложений предоставляет hello toomonitor возможность hello работоспособности серверов hello в hello пулы серверной части через портал Azure hello и PowerShell. Также можно найти работоспособности hello hello пулов серверной части через журналы диагностики производительности hello.

* [Журналы](#diagnostic-logs): разрешить журналы для доступа, производительности и других данных toobe сохранения или извлечена из ресурса в целях мониторинга.

* [Метрики.](#metrics) Сейчас в шлюзе приложений используется одна метрика. Этот показатель измеряет hello пропускная способность шлюза приложения hello в байтах в секунду.

## <a name="back-end-health"></a>Работоспособность серверной части

Шлюз приложений предоставляет возможность hello toomonitor работоспособности hello отдельных членов hello пулов серверной части через портал hello, PowerShell и hello командной строки (CLI). Можно также найти сводной работоспособности сводки пулов серверной части через журналы диагностики производительности hello. 

отчет о работоспособности серверной части Hello отражает hello выходные данные экземпляров hello шлюз приложений работоспособности проверки toohello серверной части. Если проверка прошла успешно и обратно hello end могут получать трафик, считается исправной. В противном случае серверная часть считается неработоспособной.

> [!IMPORTANT]
> Если имеется группа безопасности сети (NSG) в подсети шлюза приложений, откройте диапазоны портов 65503 65534 в подсети шлюза приложения hello для входящего трафика. Эти порты являются обязательными для API toowork hello работоспособности серверной части.


### <a name="view-back-end-health-through-hello-portal"></a>Просмотр состояния работоспособности серверной части через портал hello

На портале hello работоспособности серверной части предоставляется автоматически. В существующем шлюзе приложений выберите **Мониторинг** > **Оценка работоспособности серверной части**. 

Каждый член пула внутренней hello значится на этой странице (будь то, что сетевой Адаптер, IP или полное доменное имя). На ней показаны имя внутреннего пула, порт, параметры HTTP внутреннего пула и его состояние работоспособности. Допустимые значения состояния работоспособности: **Работоспособен**, **Неработоспособен** и **Неизвестно**.

> [!NOTE]
> Если вы видите состояние работоспособности серверной части **Неизвестный**, серверной части toohello доступ, не заблокирован, правило NSG, определяемых пользователем маршрутов (UDR) или пользовательского DNS-сервер в виртуальной сети hello.

![Работоспособность серверной части][10]

### <a name="view-back-end-health-through-powershell"></a>Просмотр данных о работоспособности серверной части с помощью PowerShell

Привет, следующий код PowerShell показано, как hello tooview работоспособности серверной части с помощью `Get-AzureRmApplicationGatewayBackendHealth` командлета:

```powershell
Get-AzureRmApplicationGatewayBackendHealth -Name ApplicationGateway1 -ResourceGroupName Contoso
```

### <a name="view-back-end-health-through-azure-cli-20"></a>Просмотр данных о работоспособности серверной части с помощью Azure CLI 2.0

```azurecli
az network application-gateway show-backend-health --resource-group AdatumAppGatewayRG --name AdatumAppGateway
```

### <a name="results"></a>Результаты

Следующий фрагмент кода Hello показан пример hello ответа.

```json
{
"BackendAddressPool": {
    "Id": "/subscriptions/00000000-0000-0000-000000000000/resourceGroups/ContosoRG/providers/Microsoft.Network/applicationGateways/applicationGateway1/backendAddressPools/appGatewayBackendPool"
},
"BackendHttpSettingsCollection": [
    {
    "BackendHttpSettings": {
        "Id": "/00000000-0000-0000-000000000000/resourceGroups/ContosoRG/providers/Microsoft.Network/applicationGateways/applicationGateway1/backendHttpSettingsCollection/appGatewayBackendHttpSettings"
    },
    "Servers": [
        {
        "Address": "hostname.westus.cloudapp.azure.com",
        "Health": "Healthy"
        },
        {
        "Address": "hostname.westus.cloudapp.azure.com",
        "Health": "Healthy"
        }
    ]
    }
]
}
```

## <a name="diagnostic-logging"></a>Журналы диагностики

Можно использовать различные типы журналов в Azure toomanage и устранение неполадок шлюзы приложений. Некоторые из этих журналах доступны через портал hello. Также можно извлечь все журналы из хранилища BLOB-объектов Azure и просматривать их с помощью таких средств, как [Log Analytics](../log-analytics/log-analytics-azure-networking-analytics.md), Excel и Power BI. Дополнительные сведения о различных типах hello журналов из hello после списка.

* **Журнал действий**: можно использовать [журналы действий Azure](../monitoring-and-diagnostics/insights-debugging-with-events.md) (ранее называвшейся операционные журналы и журналы аудита) tooview все операции, которые будут отправлены tooyour подписки Azure и их состояние. По умолчанию собираются записи журнала действий и их можно просмотреть в hello портал Azure.
* **Журнал доступа**: можно использовать шаблоны доступа к шлюз приложений этот журнал tooview и проанализировать важные сведения, включая hello вызывающего IP, запрошенного URL-адреса, задержка отклика, код возврата и байт и выхода из системы. Данные для журнала доступа собираются каждые 300 секунд. Этот журнал содержит одну запись для каждого экземпляра шлюза приложений. экземпляр шлюза приложения Hello определяться свойство instanceId hello.
* **Журнал производительности**: можно использовать этот tooview журнала, как выполняются экземпляры шлюз приложений. В этот журнал записываются сведения о производительности каждого экземпляра, включая общее число обработанных запросов, пропускную способность в байтах, число неудачных запросов, а также число работоспособных и неработоспособных серверных экземпляров. Данные для журнала производительности собираются каждые 60 секунд.
* **Журнал брандмауэра**: можно использовать этот протокол tooview hello запросов, регистрируются через режим обнаружения или Предотвращение шлюза приложения, настроенного с hello брандмауэр веб-приложения.

> [!NOTE]
> Журналы доступны только для ресурсов, развернутых в модели развертывания диспетчера ресурсов Azure hello. Нельзя использовать журналы для ресурсов в hello классической модели развертывания. Для лучшего понимания hello двух моделей, в разделе hello [сведения о диспетчере ресурсов и классического развертывания](../azure-resource-manager/resource-manager-deployment-model.md) статьи.

Существует три способа хранения журналов:

* **Учетная запись хранения** лучше всего подходит для длительного хранения журналов и их просмотра по мере необходимости.
* **Концентраторы событий**: концентраторы событий являются прекрасно подходит для интеграции с другими данными, безопасности и управления событиями (SEIM) средств tooget оповещения на ресурсы.
* **Log Analytics** лучше всего подходит для общего мониторинга приложения в реальном времени и изучения тенденций.

### <a name="enable-logging-through-powershell"></a>Включение ведения журнала с помощью PowerShell

Ведение журнала действий автоматически включается для каждого ресурса Resource Manager. Необходимо включить доступа и toostart ведения журнала производительности, сбор данных hello, доступные через эти журналы. tooenable входа hello используйте следующие шаги:

1. Обратите внимание, идентификатор ресурса вашей учетной записи хранилища, где хранятся данные журнала hello. Это значение имеет вид hello: /subscriptions/\<subscriptionId\>/resourceGroups/\<имя группы ресурсов\>/providers/Microsoft.Storage/storageAccounts/\<имя учетной записи хранения\>. Можно использовать любую учетную запись хранения в подписке. Эти сведения можно использовать hello Azure toofind портала.

    ![ИД ресурса для учетной записи хранения на портале](./media/application-gateway-diagnostics/diagnostics1.png)

2. Запишите или запомните идентификатор ресурса шлюза приложений, для которого нужно включить ведение журнала. Это значение имеет вид hello: /subscriptions/\<subscriptionId\>/resourceGroups/\<имя группы ресурсов\>/providers/Microsoft.Network/applicationGateways/\<шлюза приложений имя\>. Эти сведения можно использовать портала toofind hello.

    ![ИД ресурса для шлюза приложений на портале](./media/application-gateway-diagnostics/diagnostics2.png)

3. Включите ведение журнала диагностики с помощью hello, выполнив командлет PowerShell:

    ```powershell
    Set-AzureRmDiagnosticSetting  -ResourceId /subscriptions/<subscriptionId>/resourceGroups/<resource group name>/providers/Microsoft.Network/applicationGateways/<application gateway name> -StorageAccountId /subscriptions/<subscriptionId>/resourceGroups/<resource group name>/providers/Microsoft.Storage/storageAccounts/<storage account name> -Enabled $true     
    ```
    
> [!TIP] 
>Для журналов действий отдельная учетная запись хранения не требуется. Использование Hello хранилища для доступа и ведение журнала производительности влечет за собой службы оплаты.

### <a name="enable-logging-through-hello-azure-portal"></a>Включить ведение журнала через hello портал Azure

1. В hello портал Azure, ресурс и нажмите кнопку **журналы диагностики**.

   Для шлюза приложений доступны три журнала:

   * журнал доступа;
   * журнал производительности;
   * журнал брандмауэра.

2. Сбор данных о toostart, нажмите кнопку **включить диагностику**.

   ![Включение диагностики][1]

3. Hello **параметры диагностики** колонке предоставляет параметры hello для hello журналы диагностики. В этом примере служба аналитики журналов хранятся журналы hello. Нажмите кнопку **Настройка** под **анализа журналов** tooconfigure рабочей области. Можно также использовать концентраторов событий и журналы учетной записи хранения toosave hello диагностики.

   ![При запуске процесса конфигурации hello][2]

4. Выберите существующую рабочую область Operations Management Suite (OMS) или создайте новую. В этом примере используется существующая рабочая область.

   ![Параметры для рабочих областей OMS][3]

5. Подтверждение параметров hello и нажмите кнопку **Сохранить**.

   ![Колонка "Параметры диагностики" с выбранными значениями][4]

### <a name="activity-log"></a>Журнал действий

Azure создает hello журнал действий по умолчанию. журналы Hello сохраняются в течение 90 дней в хранилище Azure журналы событий hello. Дополнительные сведения об этих журналов, считывая hello [просматривать события и журнал действий](../monitoring-and-diagnostics/insights-debugging-with-events.md) статьи.

### <a name="access-log"></a>журнал доступа;

Журнал доступа Hello создается только в том случае, если он включен на каждом экземпляре шлюза приложения, как описано в предыдущих шагах hello. Hello данные хранятся в учетной записи хранения hello, указанного при включении ведения журнала hello. Каждый доступа шлюза приложение регистрируется в формате JSON, как показано в следующий пример hello:


|Значение  |Описание  |
|---------|---------|
|instanceId     | Шлюз приложений экземпляра запроса обслуживаются hello.        |
|clientIP     | IP-адреса для запроса hello.        |
|clientPort     | Исходный порт для запроса hello.       |
|httpMethod     | Метод HTTP, используемый запросом hello.       |
|requestUri     | URI hello получен запрос.        |
|RequestQuery     | **Сервер маршрутизации**: экземпляр пула серверной части, отправленного запроса hello. </br> **X-AzureApplicationGateway-ЖУРНАЛА-ID**: идентификатор корреляции, используемый для запроса hello. Это может быть используется tootroubleshoot проблемы трафика на внутренних серверах hello. </br>**Состояние сервера**: код ответа HTTP, полученные шлюз приложений от hello серверной части.       |
|UserAgent     | Агент пользователя из заголовка запроса hello HTTP.        |
|httpStatus     | Код состояния HTTP, возвращаемый клиента toohello шлюз приложений.       |
|httpVersion     | Версия HTTP запроса hello.        |
|receivedBytes     | Размер полученного пакета (в байтах).        |
|sentBytes| Размер отправленного пакета (в байтах).|
|timeTaken| Интервал времени (в миллисекундах), необходимое для запроса toobe обработки и его toobe ответа отправлены. Рассчитывается как интервал приветствия hello время, когда шлюз приложений получает первый байт hello HTTP время toohello запроса, когда ответ hello отправки по завершении операции. Очень важно, что toonote, обычно hello поле затраченное время включает время hello приветственных пакетов запросов и ответов передаваемых по сети hello. |
|sslEnabled| Используется ли пулы внутренней связи toohello SSL. Допустимые значения: on и off.|
```json
{
    "resourceId": "/SUBSCRIPTIONS/{subscriptionId}/RESOURCEGROUPS/PEERINGTEST/PROVIDERS/MICROSOFT.NETWORK/APPLICATIONGATEWAYS/{applicationGatewayName}",
    "operationName": "ApplicationGatewayAccess",
    "time": "2017-04-26T19:27:38Z",
    "category": "ApplicationGatewayAccessLog",
    "properties": {
        "instanceId": "ApplicationGatewayRole_IN_0",
        "clientIP": "191.96.249.97",
        "clientPort": 46886,
        "httpMethod": "GET",
        "requestUri": "/phpmyadmin/scripts/setup.php",
        "requestQuery": "X-AzureApplicationGateway-CACHE-HIT=0&SERVER-ROUTED=10.4.0.4&X-AzureApplicationGateway-LOG-ID=874f1f0f-6807-41c9-b7bc-f3cfa74aa0b1&SERVER-STATUS=404",
        "userAgent": "-",
        "httpStatus": 404,
        "httpVersion": "HTTP/1.0",
        "receivedBytes": 65,
        "sentBytes": 553,
        "timeTaken": 205,
        "sslEnabled": "off"
    }
}
```

### <a name="performance-log"></a>журнал производительности;

Журнал производительности Hello создается только в том случае, если она включена на каждом экземпляре шлюза приложения, как описано в предыдущих шагах hello. Hello данные хранятся в учетной записи хранения hello, указанного при включении ведения журнала hello. данные журнала производительности Hello создается с интервалом в 1 минуту. регистрируется Hello следующие данные:


|Значение  |Описание  |
|---------|---------|
|instanceId     |  Экземпляр шлюза приложений, для которого формируются данные о производительности. Если экземпляров шлюза приложений несколько, каждому экземпляру будет соответствовать определенная строка.        |
|healthyHostCount     | Номер работоспособное узлов в пуле hello серверной части.        |
|unHealthyHostCount     | Номер неработоспособное узлов в пуле hello серверной части.        |
|requestCount     | Число обрабатываемых запросов.        |
|latency | Задержка (в миллисекундах) запросов от экземпляра toohello hello серверный компонент, выполняющий запросы hello. |
|failedRequestCount| Количество невыполненных запросов.|
|throughput| Средняя пропускная способность с момента последнего входа hello, измеряемое в байтах в секунду.|

```json
{
    "resourceId": "/SUBSCRIPTIONS/{subscriptionId}/RESOURCEGROUPS/{resourceGroupName}/PROVIDERS/MICROSOFT.NETWORK/APPLICATIONGATEWAYS/{applicationGatewayName}",
    "operationName": "ApplicationGatewayPerformance",
    "time": "2016-04-09T00:00:00Z",
    "category": "ApplicationGatewayPerformanceLog",
    "properties":
    {
        "instanceId":"ApplicationGatewayRole_IN_1",
        "healthyHostCount":"4",
        "unHealthyHostCount":"0",
        "requestCount":"185",
        "latency":"0",
        "failedRequestCount":"0",
        "throughput":"119427"
    }
}
```

> [!NOTE]
> Задержка вычисляется на основе hello время, когда первый байт hello hello HTTP-запрос получен toohello время отправки последнего байта hello hello HTTP-ответа. Его hello сумма hello шлюза приложения, время обработки, а также hello toohello стоимости сети обратно завершить, плюс время hello hello tooprocess hello серверной части принимает запрос.

### <a name="firewall-log"></a>журнал брандмауэра.

Журнал брандмауэра Hello создается только в том случае, если она включена для всех шлюзов, приложения, как описано в предыдущих шагах hello. Этот журнал также требует, что брандмауэр веб-приложения, hello настроен на использование шлюза приложений. Hello данные хранятся в учетной записи хранения hello, указанного при включении ведения журнала hello. регистрируется Hello следующие данные:


|Значение  |Описание  |
|---------|---------|
|instanceId     | Экземпляр шлюза приложений, для которого формируются данные о брандмауэре. Если экземпляров шлюза приложений несколько, каждому экземпляру будет соответствовать определенная строка.         |
|clientIp     |   IP-адреса для запроса hello.      |
|clientPort     |  Исходный порт для запроса hello.       |
|requestUri     | URL-адрес hello получила запрос.       |
|ruleSetType     | Тип набора правил. доступное значение Hello — OWASP.        |
|ruleSetVersion     | Используемая версия набора правил. Возможные значения: 2.2.9 и 3.0.     |
|ruleId     | Код правила hello инициации события.        |
|Message     | Понятное сообщение hello инициации события. Дополнительные сведения приведены в разделе "Сведения" hello.        |
|action     |  Действие, выполняемое при запросе hello. Возможные значения: Blocked и Allowed.      |
|site     | Сайт, для которого hello журнала была создана. В нашем случае возможно только значение Global, так как применяются глобальные правила.|
|сведения     | Сведения об активации события hello.        |
|details.message     | Описание правила hello.        |
|details.data     | В запросе данных найдены правила соответствия hello.         |
|details.file     | Файл конфигурации, содержащий правило hello.        |
|details.line     | Номер строки в файле конфигурации hello, вызвавшей событие hello.       |

```json
{
  "resourceId": "/SUBSCRIPTIONS/{subscriptionId}/RESOURCEGROUPS/{resourceGroupName}/PROVIDERS/MICROSOFT.NETWORK/APPLICATIONGATEWAYS/{applicationGatewayName}",
  "operationName": "ApplicationGatewayFirewall",
  "time": "2017-03-20T15:52:09.1494499Z",
  "category": "ApplicationGatewayFirewallLog",
  "properties": {
    "instanceId": "ApplicationGatewayRole_IN_0",
    "clientIp": "104.210.252.3",
    "clientPort": "4835",
    "requestUri": "/?a=%3Cscript%3Ealert(%22Hello%22);%3C/script%3E",
    "ruleSetType": "OWASP",
    "ruleSetVersion": "3.0",
    "ruleId": "941320",
    "message": "Possible XSS Attack Detected - HTML Tag Handler",
    "action": "Blocked",
    "site": "Global",
    "details": {
      "message": "Warning. Pattern match \"<(a|abbr|acronym|address|applet|area|audioscope|b|base|basefront|bdo|bgsound|big|blackface|blink|blockquote|body|bq|br|button|caption|center|cite|code|col|colgroup|comment|dd|del|dfn|dir|div|dl|dt|em|embed|fieldset|fn|font|form|frame|frameset|h1|head|h ...\" at ARGS:a.",
      "data": "Matched Data: <script> found within ARGS:a: <script>alert(\\x22hello\\x22);</script>",
      "file": "rules/REQUEST-941-APPLICATION-ATTACK-XSS.conf",
      "line": "865"
    }
  }
} 

```

### <a name="view-and-analyze-hello-activity-log"></a>Просмотр и анализ журнала активности hello

Можно просматривать и анализировать данные журнала действий с помощью любого из следующих методов hello.

* **Инструменты Azure**: получать сведения из журнала активности hello через Azure PowerShell, hello Azure CLI, hello Azure REST API или hello портал Azure. Пошаговые инструкции для каждого метода описаны в hello [действия операции с помощью диспетчера ресурсов](../azure-resource-manager/resource-group-audit.md) статьи.
* **Power BI.** Если у вас еще нет учетной записи [Power BI](https://powerbi.microsoft.com/pricing), вы можете использовать бесплатную пробную версию. С помощью hello [журналы действий Azure пакет содержимого для Power BI](https://powerbi.microsoft.com/en-us/documentation/powerbi-content-pack-azure-audit-logs/), можно анализировать данные с помощью предварительно настроенных панелей мониторинга, которые можно использовать как есть или настроить.

### <a name="view-and-analyze-hello-access-performance-and-firewall-logs"></a>Просмотр и анализ hello доступ, производительность и журналы брандмауэра

Azure [анализа журналов](../log-analytics/log-analytics-azure-networking-analytics.md) можно собирать hello счетчика и событие файлы журнала из вашей учетной записи хранилища больших двоичных объектов. Он включает визуализации и возможности tooanalyze мощное средство поиска журналов.

Можно также подключиться tooyour учетной записи хранения и получения записей журнала hello JSON для доступа и производительности журналов. После загрузки файлов hello JSON можно преобразовать tooCSV и просматривать их в Excel, Power BI или любом другом средстве визуализации данных.

> [!TIP]
> Если вы знакомы с Visual Studio и основные понятия, связанные изменения значений константы и переменные в C#, можно использовать hello [входа преобразователь средства](https://github.com/Azure-Samples/networking-dotnet-log-converter) GitHub доступны.
> 
> 

## <a name="metrics"></a>Метрики

Метрики поддерживаются только для определенных ресурсов Azure, где можно просмотреть счетчики производительности в портале hello. Сейчас для шлюза приложений доступна одна метрика. Эта метрика пропускной способности, и вы увидите это на портале hello. Обзор шлюза tooan приложения и нажмите кнопку **метрики**. значения tooview hello, выберите пропускную способность в hello **доступные метрики** раздела. Hello после изображения вы увидите пример с фильтрами hello, toodisplay hello данных можно использовать в различных временных интервалов.

![Представление метрик с фильтрами][5]

toosee текущий список метрик, в разделе [поддерживаемых метрик с помощью монитора Azure](../monitoring-and-diagnostics/monitoring-supported-metrics.md).

### <a name="alert-rules"></a>Правила оповещения

Вы можете запустить правила генерации оповещений на основе метрик для ресурса. Например предупреждение можно вызвать веб-перехватчик или электронной почты администратора, если пропускная способность шлюза приложения hello hello выше, ниже или в порогового значения за указанный период.

Следующий пример Hello описывается создание правила оповещения, отправляющий администратор tooan электронной почты после нарушений пропускной способности a пороговое значение:

1. Нажмите кнопку **добавить оповещение метрики** tooopen hello **добавить правило** колонку. Можно также получить доступ из колонки метрики hello эту колонку.

   ![Кнопка "Добавить оповещение метрики"][6]

2. На hello **добавить правило** колонки, введите имя hello, условие и уведомить разделы и нажмите кнопку **ОК**.

   * В hello **условие** селектора, выберите одно из значений hello четырех: **больше**, **больше или равно**, **меньше, чем**, или  **Меньше или равно**.

   * В hello **период** селектора, выберите период в 5 минут too6 часов.

   * При выборе **электронной почты, владельцы, участники и читатели**, hello электронной почты может быть динамическим основании hello пользователям, имеющим доступ toothat ресурсов. В противном случае можно указать список разделенных запятыми пользователей в hello **email(s) дополнительного администратора** поле.

   ![Колонка "Добавление правила"][7]

Если пороговое значение hello, нарушена, прибывает сообщение электронной почты, аналогичные toohello один в hello после изображения:

![Сообщение электронной почты о нарушении порога][8]

После создания оповещения метрики появится список оповещений. Он предоставляет общие сведения о всех правил генерации оповещений hello.

![Список оповещений и правил][9]

. в разделе toolearn более уведомлений об предупреждениях, [получать уведомления об оповещениях](../monitoring-and-diagnostics/insights-receive-alert-notifications.md).

Посетите toounderstand Дополнительные сведения о веб-привязок и их использовании с оповещениями, [настроить веб-перехватчика на оповещение Azure метрики](../monitoring-and-diagnostics/insights-webhooks-alerts.md).

## <a name="next-steps"></a>Дальнейшие действия

* См. сведения о визуализации журналов счетчиков и событий с помощью [Log Analytics](../log-analytics/log-analytics-azure-networking-analytics.md).
* Прочтите запись блога [Visualize your Azure Activity Log with Power BI](http://blogs.msdn.com/b/powerbi/archive/2015/09/30/monitor-azure-audit-logs-with-power-bi.aspx) (Визуализация журналов действий Azure с помощью Power BI).
* Прочтите запись блога [View and analyze Azure Audit Logs in Power BI and more](https://azure.microsoft.com/blog/analyze-azure-audit-logs-in-powerbi-more/) (Просмотр и анализ журналов аудита Azure с помощью Power BI и других средств).

[1]: ./media/application-gateway-diagnostics/figure1.png
[2]: ./media/application-gateway-diagnostics/figure2.png
[3]: ./media/application-gateway-diagnostics/figure3.png
[4]: ./media/application-gateway-diagnostics/figure4.png
[5]: ./media/application-gateway-diagnostics/figure5.png
[6]: ./media/application-gateway-diagnostics/figure6.png
[7]: ./media/application-gateway-diagnostics/figure7.png
[8]: ./media/application-gateway-diagnostics/figure8.png
[9]: ./media/application-gateway-diagnostics/figure9.png
[10]: ./media/application-gateway-diagnostics/figure10.png
