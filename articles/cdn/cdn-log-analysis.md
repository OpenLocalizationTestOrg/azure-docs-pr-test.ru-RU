---
title: "Анализ aaaLog для Azure CDN | Документы Microsoft"
description: "Клиент может включить анализ журналов для Azure CDN."
services: cdn
documentationcenter: 
author: smcevoy
manager: erikre
editor: 
ms.assetid: 95e18b3c-b987-46c2-baa8-a27a029e3076
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/03/2017
ms.author: v-semcev
ms.openlocfilehash: 56e5a4fec46fd156cf38252732afb4522741d009
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="diagnostics-logs-for-azure-cdn"></a>Журналы диагностики для Azure CDN

После включения CDN для вашего приложения, будет скорее всего требуется использование CDN toomonitor hello, проверьте работоспособность вашей доставки hello и устранения возможных проблем. Azure CDN предоставляет эти возможности с помощью [CDN Core Analytics](cdn-analyze-usage-patterns.md) и [журналов диагностики](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs).

## <a name="cdn-core-analytics"></a>CDN Core Analytics
Именем текущего пользователя сети доставки Содержимого Azure Verizon standard или premium профиля уже analytics основные возможности tooview hello дополнительный портал через параметр «Управление» hello из hello портал Azure. 

## <a name="azure-diagnostic-logs"></a>Журналы диагностики Azure

Эта новая функция Azure позволяет просматривать основную аналитику и сохранять ее в одно или несколько целевых расположений:

 - Учетная запись хранения Azure
 - Концентраторы событий Azure
 - [репозиторий OMS Log Analytics](https://docs.microsoft.com/azure/log-analytics/log-analytics-get-started).
 
 Эта функция доступна для всех конечных точек CDN, принадлежащий tooVerizon (Standard и Premium) и профили CDN Akamai (стандартный).

Журналы диагностики разрешить показателей tooexport базовые способы использования вашей CDN конечную точку tooa различных источников, что позволяет обрабатывать настраиваемым способом. Например, можно сделать hello следующие типы данных экспорта:

- Экспорт данных tooblob хранилища, экспорт tooCSV и создание диаграмм в excel.
- Экспорт данных tooevent концентраторов и согласования с данными из других служб azure.
- Экспорт данных toolog аналитики и просмотра данных в собственных рабочей области OMS

Hello на этом рисунке показано типичное представление Analytics CDN основных данных.

![Портал — журналы диагностики](./media/cdn-diagnostics-log/01_OMS-workspace.png)

*Рисунок 1. Представление CDN Core Analytics*

Пошаговое руководство Hello проходит через hello схемы данных аналитики core hello, шаги, необходимые для включения функции hello и их доставку toovarious назначения из указанных целей.

## <a name="enable-logging-with-azure-portal"></a>Включение ведения журнала с помощью портала Azure

> [!NOTE]
> Hello журналы диагностики включены **off** по умолчанию. 

Выполните действия hello ниже tooenable ведения журнала с помощью CDN Core аналитики.

Войдите в toohello [портал Azure](http://portal.azure.com). Если в вашем рабочем процессе еще не включена служба CDN, [включите Azure CDN](cdn-create-new-endpoint.md), прежде чем продолжить.

1. На портале hello перейдите слишком**профиля CDN**.
2. Выберите профиль CDN, а затем hello конечной точки CDN, которые должны tooenable **журналы диагностики**.

    ![Портал — журналы диагностики](./media/cdn-diagnostics-log/02_Browse-to-Diagnostics-logs.png)

3. Go слишком**журналы диагностики** колонке под **мониторинг** , а затем изменить состояние hello слишком**на**.

    ![Портал — журналы диагностики](./media/cdn-diagnostics-log/03_Diagnostics-logs-options.png)

### <a name="enable-logging-with-azure-storage"></a>Включение ведения журнала с помощью службы хранилища Azure
    
журналы hello toostore toouse хранилища Azure, выберите **архивировать учетной записи хранилища tooa**выберите количество дней хранения и нажмите кнопку **CoreAnalytics** под **журнала**.

![Портал — журналы диагностики](./media/cdn-diagnostics-log/04_Diagnostics-logs-storage.png)

*Рисунок 2. Ведение журнала с помощью службы хранилища Azure*

### <a name="logging-with-oms-log-analytics"></a>Ведение журнала с помощью OMS Log Analytics

журналы hello toostore toouse анализа журналов OMS, выполните следующие действия.

1. Из hello **журналы диагностики** колонке под **мониторинг**выберите **отправки tooLog Analytics** из 

    ![Портал — журналы диагностики](./media/cdn-diagnostics-log/05_Ready-to-Configure.png)    

2. Настройка ведения журнала для анализа журналов hello, щелкнув на настройки. Откроется диалоговое окно tooa, где можно выбрать предыдущей рабочей областью или создайте новую.

    ![Портал — журналы диагностики](./media/cdn-diagnostics-log/06_Choose-workspace.png)

3. Щелкните **Create New Workspace** (Создание рабочей области).

    ![Портал — журналы диагностики](./media/cdn-diagnostics-log/07_Create-new.png)

4. Далее необходимо выбрать имя новой рабочей области, имеющуюся подписку, группу ресурсов (новую или имеющуюся), расположение и ценовую категорию. Предусмотрена возможность hello закрепление этой панели мониторинга tooyour конфигурации. Нажмите кнопку ОК toocomplete hello конфигурации.

    Далее для рабочей области отобразятся имена рабочей области OMS и группы ресурсов. Имена должны быть уникальными. В них могут использоваться только буквы, цифры и дефисы. Запрещено использовать пробелы и знаки подчеркивания. 

    ![Портал — журналы диагностики](./media/cdn-diagnostics-log/08_Workspace-resource.png)

5. Далее вы получаете короткое сообщение о том, что рабочей области будет создана и возвращаются tooyour окно конфигурации ведения журнала. Чтобы проверить hello имя рабочей области аналитики журналов.

    ![Портал — журналы диагностики](./media/cdn-diagnostics-log/09_Return-to-logging.png)

    После настройки конфигурации службы анализа журналов hello убедитесь, что вы также установите флажок CoreAnalytics hello CDN ведения журнала.

6. Если все tooyour оформлением, щелкните hello **Сохранить** кнопку hello верхней части диалогового окна настройки hello.

    ![Портал — журналы диагностики](./media/cdn-diagnostics-log/10_Save-me.png)

    Hello **Сохранить** кнопка больше не активно и что hello на/кнопки теперь является ON, но синего цвета вместо сиреневый.

7. Следует toosee новой рабочей областью OMS перейдите tooyour портал Azure панели мониторинга, щелкните имя hello рабочей области аналитики журналов. Далее вы увидите рабочей области (Убедитесь, что рабочая область OMS выделяется слева hello). Щелкните рабочую область в репозиторий OMS hello toosee плитки приветствия портал OMS. 

    ![Портал — журналы диагностики](./media/cdn-diagnostics-log/11_OMS-dashboard.png) 

    Репозиторий OMS получаются данные готовы toolog. Чтобы tooconsume эти данные, необходимо использовать [решений OMS](#consuming-oms-log-analytics-data), охватываемого далее в этой статье.

Дополнительные сведения о задержках данных журнала см. [здесь](#log-data-delays).

## <a name="enable-logging-with-powershell"></a>Включение ведения журнала с помощью PowerShell

Ниже приведен пример на как tooenable и get журналы диагностики через hello командлетов Azure PowerShell.

###<a name="enabling-diagnostic-logs-in-a-storage-account"></a>Включение журналов диагностики в учетной записи хранения

Сначала войдите в систему и выберите подписку:

    Login-AzureRmAccount 

    Select-AzureSubscription -SubscriptionId 


tooEnable в журналах диагностики в учетную запись хранилища, используйте следующую команду:

```powershell
    Set-AzureRmDiagnosticSetting -ResourceId "/subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/Microsoft.Cdn/profiles/{profileName}/endpoints/{endpointName}" -StorageAccountId "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ClassicStorage/storageAccounts/{storageAccountName}" -Enabled $true -Categories CoreAnalytics
```
tooEnable журналов диагностики в рабочей области OMS, используйте следующую команду:

```powershell
    Set-AzureRmDiagnosticSetting -ResourceId "/subscriptions/`{subscriptionId}<subscriptionId>
    .<subscriptionName>" -WorkspaceId "/subscriptions/<workspaceId>.<workspaceName>" -Enabled $true -Categories CoreAnalytics 
```



## <a name="consuming-diagnostics-logs-from-azure-storage"></a>Использование журналов диагностики из службы хранилища Azure
В этом разделе описываются схемы hello hello CDN core аналитики, как они организованы в учетную запись хранилища Azure и предоставляет образец кода toodownload hello входит в tooa CSV-файла.

### <a name="using-microsoft-azure-storage-explorer"></a>Использование обозревателя хранилищ Microsoft Azure
Перед обращением к hello core аналитические данные из hello учетной записи хранилища Azure, необходимо сначала hello содержимое средство tooaccess учетной записи хранилища. Хотя существует несколько средств на рынке hello, hello, рекомендуется — hello обозреватель хранилищ Microsoft Azure. Можно загрузить средство hello из [здесь](http://storageexplorer.com/). После загрузки и установки программного обеспечения hello, настройте его toouse hello одной учетной записи хранилища Azure, был настроен в качестве назначения toohello CDN журналы диагностики.

1.  Откройте **обозреватель хранилищ Microsoft Azure**.
2.  Найдите учетную запись хранилища hello
3.  Go toohello **«Контейнеров больших двоичных объектов»** узел в группе хранения учетной записи, а затем раскройте узел hello
4.  Выберите hello контейнер с именем **«аналитика журналов coreanalytics»** и дважды щелкните его
5.  Результаты Показать вверх на hello правой панели начиная с hello уровня, который выглядит как **«resourceId =»**. Продолжайте нажимать кнопку все hello способом, пока не появится файл hello **PT1H.json**. См. следующее примечание объяснение пути hello hello.
6.  Каждый BLOB-объект **PT1H.json** представляет hello журналы аналитики один час для конкретной конечной точки CDN или его пользовательский домен.
7.  Схема Hello hello содержимое этого файла JSON описан в разделе hello схемы из hello журналы аналитики Core


> [!NOTE]
> **Формат пути к BLOB-объекту**
> 
> Журналы основной аналитики создаются каждый час. Все данные за час собираются и сохраняются в одном большом двоичном объекте Azure в виде полезных данных JSON. toothis Hello пути больших двоичных объектов Azure отображается, как если бы — это иерархическая структура. Это так, как средства обозревателя хранилищ hello интерпретирует «/» в качестве разделителя каталогов, показана иерархия hello для удобства. На самом деле полный путь hello лишь представляет hello имя большого двоичного объекта. Это имя BLOB-объектов hello следует hello следующее соглашение об именовании 
    
    resourceId=/SUBSCRIPTIONS/{Subscription Id}/RESOURCEGROUPS/{Resource Group Name}/PROVIDERS/MICROSOFT.CDN/PROFILES/{Profile Name}/ENDPOINTS/{Endpoint Name}/ y={Year}/m={Month}/d={Day}/h={Hour}/m={Minutes}/PT1H.json

**Описание полей**

|value|description|
|-------|---------|
|Идентификатор подписки    |Идентификатор подписки Azure hello. Это формат Guid hello.|
|Ресурс |Имя группы ресурсов hello ресурсов группы toowhich hello CDN принадлежат.|
|Имя профиля |Имя профиля CDN hello|
|Имя конечной точки |Имя конечной точки CDN hello|
|Год|  представление 4-значный номер года hello 2017 г. Например,|
|Месяц| 2-разрядное представление числа месяца hello. 01 — январь, 12 — декабрь.|
|День|   представление 2 цифры hello день месяца hello|
|PT1H.json| Фактический файл JSON, где хранятся данные аналитики hello|

### <a name="exporting-hello-core-analytics-data-tooa-csv-file"></a>Экспорт tooa hello Core аналитические данные CSV-файла

toomake ИТ легко tooaccess hello Core Analytics мы предоставляем образец кода для средства, которое пользователи могут загрузить файлы hello JSON в формат плоской CSV-файл, который можно использовать tooeasily создания диаграмм или других агрегатов.

Вот, как можно использовать средство hello.

1.  Посетите ссылки hello github: [https://github.com/Azure-Samples/azure-cdn-samples/tree/master/CoreAnalytics-ExportToCsv](https://github.com/Azure-Samples/azure-cdn-samples/tree/master/CoreAnalytics-ExportToCsv )
2.  Загрузка кода hello
3.  Следуйте инструкциям toocompile и настройка
4.  Запустите средство hello
5.  Полученный CSV-файл отображает данные hello analytics в простых Плоская иерархия.

## <a name="consuming-diagnostics-logs-from-an-oms-log-analytics-repository"></a>Использование журналов диагностики из репозитория OMS Log Analytics
Аналитика журналов представляет собой службу в Operations Management Suite (OMS), отслеживающий вашего облака и локальных сред toomaintain их доступности и производительности. Он собирает данные, созданные ресурсы в облачных и локальных сред и других мониторинга анализа tooprovide средства в нескольких источниках. 

toouse аналитики журналов должна [включить ведение журнала](#enable-logging-with-azure-storage) toohello анализа журналов OMS Azure репозитория, описанная ранее в этой статье.

### <a name="using-hello-oms-repository"></a>С помощью hello репозиторий OMS

 Hello, следующая диаграмма показывает архитектура hello hello входов и выходов hello репозитория:

![Репозиторий OMS Log Analytics](./media/cdn-diagnostics-log/12_Repo-overview.png)

*Рисунок 3. Репозиторий OMS Log Analytics*.

Можно отобразить hello данных различными способами с помощью решения для управления. Решения для управления можно получить из hello [Azure Marketplace](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/category/monitoring-management?page=1&subcategories=management-solutions).

Решения для управления можно установить из Azure marketplace, щелкнув hello **компания** ссылку внизу hello каждого решения.

### <a name="adding-an-oms-cdn-management-solution"></a>Добавление решения по управлению OMS CDN

Выполните эти шаги tooadd решением по управлению.

1.   Если это еще не сделано, вход toohello портал Azure с помощью вашей подписки Azure и перейдите tooyour панели мониторинга.
    ![Панель мониторинга Azure](./media/cdn-diagnostics-log/13_Azure-dashboard.png)

2. В hello **New** колонке под **Marketplace**выберите **мониторинг + управления**.

    ![Marketplace](./media/cdn-diagnostics-log/14_Marketplace.png)

3. В hello **мониторинг + управления** колонка, щелкните **все**.

    ![Смотреть все](./media/cdn-diagnostics-log/15_See-all.png)

4.  Поиск CDN в поле поиска hello.

    ![Смотреть все](./media/cdn-diagnostics-log/16_Search-for.png)

5.  Выберите **Azure CDN Core Analytics**. 

    ![Смотреть все](./media/cdn-diagnostics-log/17_Core-analytics.png)

6.  После нажатия кнопки **создать**, появится запрос toocreate новую рабочую область OMS или используйте существующую. 

    ![Смотреть все](./media/cdn-diagnostics-log/18_Adding-solution.png)

7.  Выберите рабочую область hello создается до. Необходимо tooadd учетной записи автоматизации.

    ![Смотреть все](./media/cdn-diagnostics-log/19_Add-automation.png)

8. Hello следующий экран показывает форму hello автоматизации учетной записи, которую необходимо заполнить. 

    ![Смотреть все](./media/cdn-diagnostics-log/20_Automation.png)

9. После создания учетной записи автоматизации hello вы являетесь готов tooadd решения. Нажмите кнопку hello **создать** кнопки.

    ![Смотреть все](./media/cdn-diagnostics-log/21_Ready.png)

10. Решение теперь добавлено tooyour рабочей области. Вы можете вернуться tooyour портал Azure панели мониторинга.

    ![Смотреть все](./media/cdn-diagnostics-log/22_Dashboard.png)

    Щелкните рабочую область службы анализа журналов hello, вы создали toogo tooyour область. 

11. Нажмите кнопку hello **портал OMS** плитки toosee нового решения на портале OMS hello.

    ![Смотреть все](./media/cdn-diagnostics-log/23_workspace.png)

12. На портале OMS теперь должен выглядеть после экрана приветствия:

    ![Смотреть все](./media/cdn-diagnostics-log/24_OMS-solution.png)

    Выберите один из toosee плитки приветствия несколько представлений данных.

    ![Смотреть все](./media/cdn-diagnostics-log/25_Interior-view.png)

    Таблицу можно прокрутить влево или вправо toosee дальнейшей плитки, представляющих отдельных представлений данных hello. 

    Выбрав одну из плиток hello содержатся дополнительные сведения о данных.

     ![Смотреть все](./media/cdn-diagnostics-log/26_Further-detail.png)

### <a name="offers-and-pricing-tiers"></a>Предложения и ценовые категории

Предложения и ценовые категории для решений по управлению OMS см. [здесь](https://docs.microsoft.com/en-us/azure/log-analytics/log-analytics-add-solutions#offers-and-pricing-tiers).

### <a name="customizing-views"></a>Настройка представлений

Можно настроить hello представление о ваших данных с помощью hello **конструктор представлений**. Перейдите в рабочую область OMS tooyour и начинает разрабатывать, щелкнув hello **конструктор представлений** плитки.

![«Просмотреть конструктор»](./media/cdn-diagnostics-log/27_Designer.png)

Можно перетаскивать и удалять типы диаграмм слева hello и заполните сведения о данных hello требуется tooanalyze на hello слева.

![«Просмотреть конструктор»](./media/cdn-diagnostics-log/28_Designer.png)

    
## <a name="log-data-delays"></a>Задержка данных журнала

Задержка данных журнала Verizon | Задержка данных журнала Akamai
--- | ---
Данные журнала Verizon откладывается 1 час и занимают toostart too2 часы, появляющиеся после завершения распространения конечной точки. | Данные журнала Akamai отложенной 24 часа и занимает toostart too2 часы, появляется ли она создана более 24 часов назад. Если он был создан недавно, может занять too25 часов для появления toostart журналы hello.

## <a name="diagnostic-log-types-for-cdn-core-analytics"></a>Типы журналов диагностики для CDN Core Analytics

В настоящее время мы предлагаем только журналы аналитики основных компонентов, которые содержат метрики, показывающий статистику ответа HTTP и исходящих отображающееся hello CDN извлекает и линии.

### <a name="core-analytics-metrics-details"></a>Сведения о метриках основной аналитики
Hello в следующей таблице содержится перечень метрики недоступны в журналы аналитики Core hello. Не все метрики доступны у всех поставщиков, хотя различия минимальны. в следующей таблице также Hello указывает данная метрика доступно у поставщика. Обратите внимание на то, что hello метрики доступны для только конечные точки CDN на которых установлена трафика.


|Метрика                     | Описание   | Verizon  | Akamai 
|---------------------------|---------------|---|---|
| RequestCountTotal         |Общее количество запросов за этот период.| Да  |Да   |
| RequestCountHttpStatus2xx |Количество всех запросов, в результате которых вернулся код HTTP 2xx (например, 200, 202).              | Да  |Да   |
| RequestCountHttpStatus3xx | Количество всех запросов, в результате которых вернулся код HTTP 3xx (например, 300, 302).              | Да  |Да   |
| RequestCountHttpStatus4xx |Количество всех запросов, в результате которых вернулся код HTTP 4xx (например, 400, 404).               | Да   |Да   |
| RequestCountHttpStatus5xx | Количество всех запросов, в результате которых вернулся код HTTP 5xx (например, 500, 504).              | Да  |Да   |
| RequestCountHttpStatusOthers |  Количество всех остальных кодов HTTP (кроме 2xx–5xx). | Да  |Да   |
| RequestCountHttpStatus200 | Количество всех запросов, в результате которых вернулся код HTTP 200.              |Нет   |Да   |
| RequestCountHttpStatus206 | Количество всех запросов, в результате которых вернулся код HTTP 206.              |Нет   |Да   |
| RequestCountHttpStatus302 | Количество всех запросов, в результате которых вернулся код HTTP 302.              |Нет   |Да   |
| RequestCountHttpStatus304 |  Количество всех запросов, в результате которых вернулся код HTTP 304.             |Нет   |Да   |
| RequestCountHttpStatus404 | Количество всех запросов, в результате которых вернулся код HTTP 404.              |Нет   |Да   |
| RequestCountCacheHit |Количество всех запросов, в результате которых произошло попадание в кэш. Это означает, что был обработан активов hello непосредственно из toohello POP hello клиента.               | Да  |Нет   |
| RequestCountCacheMiss | Количество всех запросов, в результате которых произошел промах кэша. Это означает, что активов hello не найден на клиенте toohello ближайший POP hello и поэтому был извлечен из hello источника.              |Да   | Нет  |
| RequestCountCacheNoCache | Количество всех запросов tooan активов, препятствующая кэшируемого из-за конфигурации пользователя tooa на границе hello.              |Да   | Нет  |
| RequestCountCacheUncacheable | Количество всех запросов tooassets, препятствующая кэширования hello активов Cache-Control и истечения срока действия заголовки, которые указывают, что его не следует кэшировать POP или клиентом hello HTTP                |Да   |Нет   |
| RequestCountCacheOthers | Количество всех запросов с состоянием кэша, не указанным выше.              |Да   | Нет  |
| EgressTotal | Объем передачи исходящих данных в ГБ.              |Да   |Да   |
| EgressHttpStatus2xx | Объем передачи исходящих данных* для ответов с кодами состояния HTTP 2xx в ГБ.            |Да   |Нет   |
| EgressHttpStatus3xx | Объем передачи исходящих данных для ответов с кодами состояния HTTP 3xx в ГБ.              |Да   |Нет   |
| EgressHttpStatus4xx | Объем передачи исходящих данных для ответов с кодами состояния HTTP 4xx в ГБ.               |Да   | Нет  |
| EgressHttpStatus5xx | Объем передачи исходящих данных для ответов с кодами состояния HTTP 5xx в ГБ.               |Да   |  Нет |
| EgressHttpStatusOthers | Объем передачи исходящих данных для ответов с другими кодами состояния HTTP в ГБ.                |Да   |Нет   |
| EgressCacheHit |  Исходящие передачи данных для ответов, которые были доставлены непосредственно из кэша CDN hello на hello CDN извлекает и линии  |Да   |  Нет |
| EgressCacheMiss | Передача исходящих данных для ответов, не найден на hello ближайшего POP-сервер и полученные от исходного сервера hello              |Да   |  Нет |
| EgressCacheNoCache | Для средств, которые предотвращаются кэширования из-за конфигурации пользователя tooa на границе hello передачи исходящих данных.                |Да   |Нет   |
| EgressCacheUncacheable | Передача исходящих данных для средств, которые запрещено кэш Cache-Control и Expires заголовки, которые указывают, что его не следует кэшировать POP или клиентом hello HTTP hello активов                    |Да   | Нет  |
| EgressCacheOthers |  Объем передачи исходящих данных для других сценариев с использованием кэша.             |Да   | Нет  |

* Исходящие данные передачи ссылается tootraffic доставлен из CDN POP серверов toohello клиента.


### <a name="schema-of-hello-core-analytics-logs"></a>Схема Core журналы аналитики hello 

Все журналы хранятся в формате JSON, и каждая запись содержит строковые поля после hello ниже схемой:

```json
    "records": [
        {
            "time": "2017-04-27T01:00:00",
            "resourceId": "<ARM Resource Id of hello CDN Endpoint>",
            "operationName": "Microsoft.Cdn/profiles/endpoints/contentDelivery",
            "category": "CoreAnalytics",
            "properties": {
                "DomainName": "<Name of hello domain for which hello statistics is reported>",
                "RequestCountTotal": integer value,
                "RequestCountHttpStatus2xx": integer value,
                "RequestCountHttpStatus3xx": integer value,
                "RequestCountHttpStatus4xx": integer value,
                "RequestCountHttpStatus5xx": integer value,
                "RequestCountHttpStatusOthers": integer value,
                "RequestCountHttpStatus200": integer value,
                "RequestCountHttpStatus206": integer value,
                "RequestCountHttpStatus302": integer value,
                "RequestCountHttpStatus304": integer value,
                "RequestCountHttpStatus404": integer value,
                "RequestCountCacheHit": integer value,
                "RequestCountCacheMiss": integer value,
                "RequestCountCacheNoCache": integer value,
                "RequestCountCacheUncacheable": integer value,
                "RequestCountCacheOthers": integer value,
                "EgressTotal": double value,
                "EgressHttpStatus2xx": double value,
                "EgressHttpStatus3xx": double value,
                "EgressHttpStatus4xx": double value,
                "EgressHttpStatus5xx": double value,
                "EgressHttpStatusOthers": double value,
                "EgressCacheHit": double value,
                "EgressCacheMiss": double value,
                "EgressCacheNoCache": double value,
                "EgressCacheUncacheable": double value,
                "EgressCacheOthers": double value,
            }
        }

    ]
}
```

Где hello «время» представляет время начала hello границы час hello, для которой сообщается hello статистики. Если метрика не поддерживается поставщиком CDN, вместо значения типа double или целого числа используется значение NULL. Нулевое значение указывает отсутствие hello метрики, и оно отличается от значения 0. Также Обратите внимание, что будет один набор показателей в домене, настроенный на конечной hello.

Примеры свойств приведены ниже

```json
{
     "DomainName": "manlingakamaitest2.azureedge.net",
     "RequestCountTotal": 480,
     "RequestCountHttpStatus2xx": 480,
     "RequestCountHttpStatus3xx": 0,
     "RequestCountHttpStatus4xx": 0,
     "RequestCountHttpStatus5xx": 0,
     "RequestCountHttpStatusOthers": 0,
     "RequestCountHttpStatus200": 480,
     "RequestCountHttpStatus206": 0,
     "RequestCountHttpStatus302": 0,
     "RequestCountHttpStatus304": 0,
     "RequestCountHttpStatus404": 0,
     "RequestCountCacheHit": null,
     "RequestCountCacheMiss": null,
     "RequestCountCacheNoCache": null,
     "RequestCountCacheUncacheable": null,
     "RequestCountCacheOthers": null,
     "EgressTotal": 0.09,
     "EgressHttpStatus2xx": null,
     "EgressHttpStatus3xx": null,
     "EgressHttpStatus4xx": null,
     "EgressHttpStatus5xx": null,
     "EgressHttpStatusOthers": null,
     "EgressCacheHit": null,
     "EgressCacheMiss": null,
     "EgressCacheNoCache": null,
     "EgressCacheUncacheable": null,
     "EgressCacheOthers": null
}

```

## <a name="additional-resources"></a>Дополнительные ресурсы

* [Сбор и использование диагностических данных из ресурсов Azure](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs)
* [Анализ вариантов использования CDN Azure](https://docs.microsoft.com/azure/cdn/cdn-analyze-usage-patterns)
* [Что такое Log Analytics?](https://docs.microsoft.com/en-us/azure/log-analytics/log-analytics-overview)
* [Log Analytics REST API Reference](https://docs.microsoft.com/en-us/rest/api/loganalytics) (Справочник по REST API Log Analytics)







