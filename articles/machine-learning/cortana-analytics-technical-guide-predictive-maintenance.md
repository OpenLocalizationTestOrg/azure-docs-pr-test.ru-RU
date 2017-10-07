---
title: "обслуживание aaaPredictive аэрокосмическое оборудование с Azure — техническое руководство решения аналитики Cortana | Документы Microsoft"
description: "Техническое руководство по toohello шаблон решения с помощью Cortana аналитики Microsoft для превентивного обслуживания в аэрокосмическое оборудование, программы и транспортировки."
services: cortana-analytics
documentationcenter: 
author: fboylu
manager: jhubbard
editor: cgronlun
ms.assetid: 2c4d2147-0f05-4705-8748-9527c2c1f033
ms.service: cortana-analytics
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/14/2017
ms.author: fboylu
ms.openlocfilehash: 30ddc1c101007546ae1b303bccebae3ecdacb442
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="technical-guide-toohello-cortana-intelligence-solution-template-for-predictive-maintenance-in-aerospace-and-other-businesses"></a>Техническое руководство по toohello шаблон решения аналитики Cortana для превентивного обслуживания в аэрокосмическое оборудование и других организаций

## <a name="important"></a>**Важно!**
Эта статья считается устаревшей. сведения Hello проблема все еще актуальны toohello под рукой, т. е. превентивного обслуживания в аэрокосмическое оборудование, но последней статье hello с hello наиболее вверх toodate сведения можно найти [здесь](https://github.com/Azure/cortana-intelligence-predictive-maintenance-aerospace). 

## <a name="acknowledgements"></a>**Благодарности**
Авторами этой статьи являются специалисты по обработке и анализу данных Ян Цанг (Yan Zhang), Гаухер Шахин (Gauher Shaheen), Фидан Бойлу Юз (Fidan Boylu Uz) и инженер по программному обеспечению в корпорации Майкрософт Дэн Греко (Dan Grecoe).

## <a name="overview"></a>**Обзор**
Шаблоны решений предназначены tooaccelerate hello процесс построения E2E Демонстрация поверх набора аналитики Cortana. Развернутого шаблона будет подготовить подписку с необходимых компонентов Cortana аналитики и построения hello связи между ними. Он также заполняет конвейера данных hello с образцами данных, созданные из приложения генератора данных, который будет загрузить и установить на локальном компьютере, после развертывания шаблона решения hello. Hello данные, созданные из генератора hello будет заполнить конвейера данных hello и приступить к созданию прогнозов машинного обучения, которые можно представить на панели мониторинга Power BI hello. процесс развертывания Hello поможет выполнить несколько шагов tooset копии решения учетные данные. Убедитесь, что записывать эти учетные данные, такие как имя решения, имя пользователя и пароль, предоставленные во время развертывания hello.  

Hello цель данного документа — Эталонная архитектура tooexplain hello и различные компоненты подготовлены в вашей подписке, в рамках этого решения шаблона. Hello документ также рассказывается о том, как tooreplace образец данных с реальными данными аналитики может toosee toobe и прогнозы на основе собственных данных. Кроме того hello документе рассматриваются части решения шаблон, который необходимо изменить, если требуется, чтобы решение hello toocustomize с собственными данными toobe hello. В конце hello приведены инструкции как toobuild hello панели мониторинга Power BI для этого шаблона решения.

> [!TIP]
> Можно скачать и распечатать [PDF-версию этого документа](http://download.microsoft.com/download/F/4/D/F4D7D208-D080-42ED-8813-6030D23329E9/cortana-analytics-technical-guide-predictive-maintenance.pdf).
> 
> 

## <a name="big-picture"></a>**Общая картина**
![Архитектура прогнозируемого обслуживания](media/cortana-analytics-technical-guide-predictive-maintenance/predictive-maintenance-architecture.png)

При развертывании решения hello различных служб Azure в Cortana Analytics Suite активируются (*т. е.* концентратор событий, Stream Analytics, HDInsight, фабрика данных, машинное обучение *и т. д.*). Hello архитектура приведенной выше схеме показаны, в общем, создание hello превентивного обслуживания для Аэрокосмических шаблон решения от начала до конца. Можно будет tooinvestigate этих служб на портале hello azure, щелкнув их hello решения шаблона схемой, созданной с помощью развертывания hello hello решения с исключением hello hdinsight, как данная служба предоставляется по запросу, когда hello связаны действия конвейера являются необходимые toorun и удалены после него.
Вы можете загрузить [полноэкранному hello схемы](http://download.microsoft.com/download/1/9/B/19B815F0-D1B0-4F67-AED3-A40544225FD1/ca-topologies-maintenance-prediction.png).

Hello в следующих разделах описывается каждый из сегментов.

## <a name="data-source-and-ingestion"></a>**Источник данных и прием**
### <a name="synthetic-data-source"></a>Источник искусственных данных
Для этого шаблона, данные hello используемого источника формируется из приложения рабочего стола, который будет загружать и запускать локально, после успешного развертывания. Будет найти toodownload инструкции hello и установить это приложение hello панели свойств при выборе hello первый узел, называемый прогнозной генератора данных обслуживания на схеме шаблона решения hello. Это приложение веб-каналы hello [концентратор событий Azure](#azure-event-hub) службой точек данных или событий, которые будут использоваться hello конца потока hello решения. Этот источник данных состоит из или производным от общедоступные данные из [репозитория данных NASA](http://ti.arc.nasa.gov/tech/dash/pcoe/prognostic-data-repository/) с помощью hello [набор данных имитации снижение ядра Turbofan](http://ti.arc.nasa.gov/tech/dash/pcoe/prognostic-data-repository/#turbofan).

Создание приложения Hello событий будет заполнять hello концентратор событий Azure только при выполнении на компьютере.

### <a name="azure-event-hub"></a>концентратору событий Azure
Hello [концентратор событий Azure](https://azure.microsoft.com/services/event-hubs/) службы — получатель hello hello входных данных, предоставленных hello искусственного источника данных, описанных выше.

## <a name="data-preparation-and-analysis"></a>**Подготовка и анализ данных**
### <a name="azure-stream-analytics"></a>Azure Stream Analytics
Hello [Azure Stream Analytics](https://azure.microsoft.com/services/stream-analytics/) служба является используемым tooprovide рядом с аналитикой в реальном времени на hello входного потока из hello [концентратор событий Azure](#azure-event-hub) службы и опубликовать результаты на [Power BI](https://powerbi.microsoft.com) панели мониторинга, а также архивирование все необработанные входящие события toohello [хранилища Azure](https://azure.microsoft.com/services/storage/) службу для последующей обработки hello [фабрики данных Azure](https://azure.microsoft.com/documentation/services/data-factory/) службы.

### <a name="hd-insights-custom-aggregation"></a>Пользовательская агрегация HD Insights
Hello службы анализ HD Azure — используется toorun [Hive](http://blogs.msdn.com/b/bigdatasupport/archive/2013/11/11/get-started-with-hive-on-hdinsight.aspx) агрегаты tooprovide скриптов (под управлением фабрики данных Azure) на hello необработанные события, которые были архивированы, с помощью службы Azure Stream Analytics hello.

### <a name="azure-machine-learning"></a>Машинное обучение Azure
Hello [машинного обучения Azure](https://azure.microsoft.com/services/machine-learning/) (под управлением фабрики данных Azure) используется служба toomake прогнозов на оставшийся срок службы (RUL) определенного самолет engine, в основе полученных входных данных hello hello.

## <a name="data-publishing"></a>**Публикация данных**
### <a name="azure-sql-database-service"></a>Служба базы данных SQL Azure
Hello [базы данных SQL Azure](https://azure.microsoft.com/services/sql-database/) службы — прогнозы hello используется toostore (управляемые фабрикой данных Azure), полученных hello службы машинного обучения Azure, которая будет использоваться в hello [Power BI](https://powerbi.microsoft.com) панели мониторинга.

## <a name="data-consumption"></a>**Использование данных**
### <a name="power-bi"></a>Power BI
Hello [Power BI](https://powerbi.microsoft.com) служба является tooshow используется панель мониторинга, которая содержит статистические выражения и оповещения, предоставляемые hello [Azure Stream Analytics](https://azure.microsoft.com/services/stream-analytics/) службы, а также RUL прогнозов, хранящиеся в [Azure SQL База данных](https://azure.microsoft.com/services/sql-database/) , полученных с помощью hello [машинного обучения Azure](https://azure.microsoft.com/services/machine-learning/) службы. Инструкции по как toobuild hello панели мониторинга Power BI для этого шаблона решения см. ниже toohello.

## <a name="how-toobring-in-your-own-data"></a>**Как toobring свои данные**
В этом разделе описываются toobring tooAzure собственных данных и области, которые может потребоваться изменение hello данных можно перевести в этой архитектуре.

Маловероятно, что любой набор данных, вставленные будет соответствовать hello набор данных, используемый hello [набор данных имитации снижение ядра Turbofan](http://ti.arc.nasa.gov/tech/dash/pcoe/prognostic-data-repository/#turbofan) используется для этого шаблона решения. Основные сведения о данных и требования будут важны в изменении toowork этого шаблона с собственными данными. Если это ваш первый toohello уязвимость службы машинного обучения Azure, tooit Общие сведения можно получить с помощью пример hello в [как toocreate эксперимента первый](machine-learning-create-experiment.md).

Hello в следующих разделах обсуждаются разделах hello hello шаблона, который потребуется изменить при появился новый набор данных.

### <a name="azure-event-hub"></a>концентратору событий Azure
Hello концентратор событий Azure service является универсальным, таким образом, что данные могут быть разнесены концентратора toohello в формате CSV или JSON. Никакая специальная обработка происходит в hello концентратор событий Azure, но важно понимать hello данных, возвращаемых в него.

В этом документе не описывается, как tooingest данных, но можно легко отправлять события или концентратор событий Azure tooan данных с помощью hello интерфейс API концентратора событий.

### <a name="azure-stream-analytics"></a>Azure Stream Analytics
Hello службой Azure Stream Analytics является чтение из потоков данных и вывода данных tooany количество источников используется tooprovide практически в режиме реального времени.

Для hello превентивного обслуживания для Аэрокосмических шаблон решения Azure Stream Analytics запрос состоит из четырех вложенные запросы, каждый потребитель события из hello концентратор событий Azure service и необходимости выходные данные в четырех различных расположениях. Эти выходные данные состоят из трех наборов данных Power BI и одного места хранения Azure.

запрос Hello Azure Stream Analytics можно найти по:

* Вход в портал Azure hello
* Поиск заданий Stream Analytics hello ![Stream Analytics значок](media/cortana-analytics-technical-guide-predictive-maintenance/icon-stream-analytics.png) , созданные при развертывании решения hello (*например*, **maintenancesa02asapbi** и **maintenancesa02asablob** для решения превентивного обслуживания)
* Выбрать
  
  * ***Входные данные*** tooview входных данных запроса hello
  * ***ЗАПРОС*** сам запрос tooview hello
  * ***ВЫВОДИТ*** tooview hello различные выходы

Сведения о построении запросов Azure Stream Analytics находятся в hello [Справка запросов Stream Analytics](https://msdn.microsoft.com/library/azure/dn834998.aspx) на сайте MSDN.

В этом решении запросы hello вывода трех наборов данных с рядом с аналитикой в реальном времени сведения о hello входящих данных потока tooa панели мониторинга Power BI, предоставляется как часть этого шаблона решения. Поскольку неявные сведения о входящих данных формате hello, эти запросы потребуется изменить toobe на основе вашего формата данных.

запрос Hello в задании Stream Analytics второй hello **maintenancesa02asablob** просто выводит все [концентратора событий](https://azure.microsoft.com/services/event-hubs/) событий для [хранилища Azure](https://azure.microsoft.com/services/storage/) и поэтому требует без изменения независимо от того, в формат данных, что hello сведения событий является потоковым toostorage.

### <a name="azure-data-factory"></a>Фабрика данных Azure
Hello [фабрики данных Azure](https://azure.microsoft.com/documentation/services/data-factory/) управляет служба перемещения hello и обработку данных. Диагностическое обслуживание данных hello Аэрокосмических шаблон решения фабрики состоит из трех [конвейеры](../data-factory/data-factory-create-pipelines.md) , перемещения и обработки данных hello, с использованием различных технологий.  Фабрики данных можно открыть, открыв узел фабрики данных hello hello внизу hello hello решения шаблона схемой, созданной с помощью развертывания hello hello решения. Это займет вы toohello фабрики данных на портале Azure. При обнаружении ошибок в наборах данных, можно пропустить те как из-за toodata фабрики развертывания до запуска генератора данных hello. Эти ошибки не мешают работе фабрики данных.

![Ошибки наборов данных фабрики данных](media/cortana-analytics-technical-guide-predictive-maintenance/data-factory-dataset-error.png)

В этом разделе рассматриваются необходимые hello [конвейеры](../data-factory/data-factory-create-pipelines.md) и [действия](../data-factory/data-factory-create-pipelines.md) содержащихся в hello [фабрики данных Azure](https://azure.microsoft.com/documentation/services/data-factory/). Ниже приведен представление диаграммы hello hello решения.

![Фабрика данных Azure](media/cortana-analytics-technical-guide-predictive-maintenance/azure-data-factory.png)

Содержит два конвейеров hello этой фабрики [Hive](http://blogs.msdn.com/b/bigdatasupport/archive/2013/11/11/get-started-with-hive-on-hdinsight.aspx) скрипты, используемые toopartition и hello статистические данные. Если отмечено, hello скриптов будет находиться в hello [хранилища Azure](https://azure.microsoft.com/services/storage/) учетную запись, созданную во время установки. Их расположение: maintenancesascript\\\\script\\\\hive\\\\ (или https://[имя вашего решения].blob.core.windows.net/maintenancesascript).

Аналогичные toohello [Azure Stream Analytics](#azure-stream-analytics-1) запросы, [Hive](http://blogs.msdn.com/b/bigdatasupport/archive/2013/11/11/get-started-with-hive-on-hdinsight.aspx) скрипты имеют неявные сведения о входящих данных формате hello, эти запросы потребуется изменить toobe на основе формата данных и [компонентов engineering](machine-learning-feature-selection-and-engineering.md) требования.

#### <a name="aggregateflightinfopipeline"></a>*AggregateFlightInfoPipeline*
Это [конвейера](../data-factory/data-factory-create-pipelines.md) содержит одно действие - [HDInsightHive](../data-factory/data-factory-hive-activity.md) действия с помощью [HDInsightLinkedService](https://msdn.microsoft.com/library/azure/dn893526.aspx) , на котором запущена [Hive](http://blogs.msdn.com/b/bigdatasupport/archive/2013/11/11/get-started-with-hive-on-hdinsight.aspx) сценарий toopartition hello данные помещаются в [хранилища Azure](https://azure.microsoft.com/services/storage/) во время [Azure Stream Analytics](https://azure.microsoft.com/services/stream-analytics/) задания.

Сценарий [Hive](http://blogs.msdn.com/b/bigdatasupport/archive/2013/11/11/get-started-with-hive-on-hdinsight.aspx) для этой задачи секционирования — ***AggregateFlightInfo.hql***.

#### <a name="mlscoringpipeline"></a>*MLScoringPipeline*
Это [конвейера](../data-factory/data-factory-create-pipelines.md) содержит несколько действий и которого конечным результатом является hello оцененных прогнозы на основании hello [машинного обучения Azure](https://azure.microsoft.com/services/machine-learning/) эксперимент, связанный с этим шаблоном решения.

Hello действия, содержащиеся в этом являются:

* [HDInsightHive](../data-factory/data-factory-hive-activity.md) действия с помощью [HDInsightLinkedService](https://msdn.microsoft.com/library/azure/dn893526.aspx) , на котором запущена [Hive](http://blogs.msdn.com/b/bigdatasupport/archive/2013/11/11/get-started-with-hive-on-hdinsight.aspx) сценариев tooperform агрегаты и возможностей разработки, необходимые для hello [Azure Машинное Обучение](https://azure.microsoft.com/services/machine-learning/) поэкспериментировать.
  Сценарий [Hive](http://blogs.msdn.com/b/bigdatasupport/archive/2013/11/11/get-started-with-hive-on-hdinsight.aspx) для этой задачи секционирования — ***PrepareMLInput.hql***.
* [Копировать](https://msdn.microsoft.com/library/azure/dn835035.aspx) действие, перемещающее hello результаты из [HDInsightHive](../data-factory/data-factory-hive-activity.md) tooa действия один [хранилища Azure](https://azure.microsoft.com/services/storage/) больших двоичных объектов, которым можно получить доступ по [AzureMLBatchScoring](https://msdn.microsoft.com/library/azure/dn894009.aspx) действия.
* [AzureMLBatchScoring](https://msdn.microsoft.com/library/azure/dn894009.aspx) действия, которое вызывает hello [машинного обучения Azure](https://azure.microsoft.com/services/machine-learning/) эксперимент, что приводит к результаты hello был помещен в одном [хранилища Azure](https://azure.microsoft.com/services/storage/) больших двоичных объектов.

#### <a name="copyscoredresultpipeline"></a>*CopyScoredResultPipeline*
Это [конвейера](../data-factory/data-factory-create-pipelines.md) содержит одно действие - [копирования](https://msdn.microsoft.com/library/azure/dn835035.aspx) действие, перемещающее hello результаты hello [машинного обучения Azure](#azure-machine-learning) поэкспериментировать с *** MLScoringPipeline*** toohello [базы данных SQL Azure](https://azure.microsoft.com/services/sql-database/) , была создана как часть установки шаблона решения.

### <a name="azure-machine-learning"></a>Машинное обучение Azure
Hello [машинного обучения Azure](https://azure.microsoft.com/services/machine-learning/) эксперимента используется для этого шаблона решение обеспечивает hello оставшиеся полезные жизни (RUL) самолет ядра. Hello эксперимента является набор данных конкретного toohello потребляет и потребует изменения или замены определенных toohello данных, получаемых в.

Сведения о создании hello эксперимента машинного обучения Azure см. в разделе [превентивного обслуживания: шаг 1 из 3 подготовки данных и конструируются](http://gallery.cortanaanalytics.com/Experiment/Predictive-Maintenance-Step-1-of-3-data-preparation-and-feature-engineering-2).

## <a name="monitor-progress"></a>**Отслеживание хода выполнения**
 После запуска hello генератора данных hello конвейера начинает tooget структура данных, а hello различные компоненты решения запускать в самом начале, в действие, следующие команды hello выданный hello фабрики данных. Вы можете отслеживать конвейера hello двумя способами.

1. Одно из задания Stream Analytics hello записывает hello необработанные входящие tooblob хранения данных. Если вы щелкните хранилище больших двоичных объектов компонент решения от экрана приветствия вы успешно развернутое приложение hello решения и затем нажмите кнопку "Открыть" в правой панели hello, займет toohello [портала управления](https://portal.azure.com/). На портале щелкните "BLOB-объекты". В следующей панели hello вы увидите список контейнеров. Щелкните **maintenancesadata**. В следующей панели hello, вы увидите hello **rawdata** папки. В папке rawdata hello, вы увидите папки с именами, например час = 17, час = 18 и т. д. При появлении этих папок, он указывает, hello необработанные данные успешно выполняется на компьютере и сохраняется в хранилище больших двоичных объектов. Вы должны увидеть CSV-файлы, которые должны иметь в этих папках ограничение по размерам (в МБ).
2. Последний шаг Hello hello конвейера — toowrite данных (например, прогнозы на основании машинного обучения) в базу данных SQL. Может потребоваться toowait до трех часов hello tooappear данных в базе данных SQL. Одним из способов toomonitor объем данных в базе данных SQL — через [портал azure](https://manage.windowsazure.com/). На левой панели hello найдите баз данных SQL ![значок SQL](media/cortana-analytics-technical-guide-predictive-maintenance/icon-SQL-databases.png) и щелкните его. Затем найдите базу данных **pmaintenancedb** и щелкните ее. На следующей странице hello внизу hello щелкните УПРАВЛЕНИЕ
   
    ![Значок "Управление"](media/cortana-analytics-technical-guide-predictive-maintenance/icon-manage.png).
   
    Здесь можно щелкнуть нового запроса и запрос для hello число строк (например select count(*) из PMResult). По мере роста базы данных, следует увеличить hello количество строк в таблице hello.

## <a name="power-bi-dashboard"></a>**Панель мониторинга Power BI**
### <a name="overview"></a>Обзор
В этом разделе описываются отображением tooset копирование toovisualize панели мониторинга Power BI данные реальном времени, из Azure Stream Analytics (Горячий путь), а также пакетный прогноз результатов из машинного обучения Azure (холодный путь).

### <a name="setup-cold-path-dashboard"></a>Настройка холодного пути панели мониторинга
В конвейере данных hello холодного путь hello essential предназначена tooget прогнозной RUL (оставшегося срока) каждой подсистемы самолет после ее завершения рейса (цикла). результат прогноза Hello обновляется каждые 3 часа для прогнозирования обработчиков самолет hello, после завершения определенного рейса во время hello за последние 3 часа.

Power BI подключается tooan базы данных Azure SQL в качестве источника данных, где хранятся результаты прогноза. Примечание: (1) при развертывании решения, реальные прогноз будет отображаться в hello базы данных в течение 3 часов.
Hello pbix-файл, поставляемый с hello генератор загрузки содержит некоторые данные начальное значение, поэтому может создавать панели мониторинга Power BI hello сразу. (2) на этом шаге условием hello toodownload и установите hello программное обеспечение предоставляется бесплатно [Power BI desktop](https://powerbi.microsoft.com/documentation/powerbi-desktop-get-the-desktop/).

Hello следующие шаги помогут вам в как файл tooconnect hello pbix hello базы данных SQL, зацикливается во время развертывания решения, содержащего данные hello (*например*. результаты прогноза) для визуализации.

1. Получите учетные данные базы данных hello.
   
   Вам потребуется **базы данных, имя сервера, имя базы данных, имя пользователя и пароль** перед перемещением toonext действия. Ниже приведены шаги tooguide hello вы как toofind их.
   
   * Когда элемент **База данных SQL Azure** на схеме шаблона решения станет зеленым, щелкните его и нажмите кнопку **Открыть**.
   * Вы увидите новое вкладка или окно браузера, отображающий hello странице портала Azure. Нажмите кнопку **«Группы ресурсов»** на левой панели hello.
   * Выберите hello подписку, которую вы используете для развертывания решения hello, а затем выберите **"YourSolutionName\_ResourceGroup"**.
   * В hello новый в новом окне панели, щелкните hello ![значок SQL](media/cortana-analytics-technical-guide-predictive-maintenance/icon-sql.png) tooaccess значок базы данных. Имя базы данных является Далее toohello этим значком (*например*, **«pmaintenancedb»**) и hello **имя сервера базы данных** находится в списке hello свойство имени сервера и должен выглядеть аналогичные слишком**YourSoutionName.database.windows.net**.
   * Базы данных **username** и **пароль** : hello так же, как hello имени пользователя и пароля с заранее записанным во время развертывания решения hello.
2. Обновление источника данных hello hello холодного путь отчета файла с Power BI Desktop.
   
   * В папке hello на вашем Компьютере, в которую был загружен и распаковал файл генератора, дважды щелкните **PowerBI\\PredictiveMaintenanceAerospace.pbix** файла. Если вы видите все предупреждающие сообщения, при открытии файла hello, их можно пропустите. В верхней части hello hello файла, нажмите кнопку **изменить запросы**.
     
     ![Изменение запросов](media/cortana-analytics-technical-guide-predictive-maintenance/edit-queries.png)
   * Вы увидите две таблицы — **RemainingUsefulLife** и **PMResult**. Выберите первую таблицу hello и нажмите кнопку ![значок параметров запроса](media/cortana-analytics-technical-guide-predictive-maintenance/icon-query-settings.png) Далее слишком**«Источник»** под **ПРИМЕНЕННЫХ ДЕЙСТВИЙ** на правом hello **«Параметры запроса»**панель. Игнорируйте все предупреждающие сообщения, которые отображаются.
   * В окне pop hello, замените **«Сервер»** и **'Database'** с собственные имена сервера и базы данных, а затем щелкните **«OK»**. Для имени сервера, убедитесь, что указан hello порт 1433 (**YourSoutionName.database.windows.net 1433**). Оставьте поле hello базы данных как **pmaintenancedb**. Игнорируйте hello предупреждающие сообщения, которые отображаются на экране приветствия.
   * В hello далее в новом окне окно, вы увидите два варианта на левой панели hello (**Windows** и **базы данных**). Нажмите кнопку **'Database'**, заполните вашей **«Username»** и **«Пароль»** (это hello имя пользователя и пароль, введенный при развертывании решения hello и создании База данных Azure SQL). В ***выберите которой уровня tooapply эти параметры требуется***, проверьте параметр уровня базы данных. Щелкните **Подключить**.
   * Щелкните вторую таблицу hello **PMResult** нажмите кнопку ![значка навигации](media/cortana-analytics-technical-guide-predictive-maintenance/icon-navigation.png) Далее слишком**«Источник»** под **ПРИМЕНЕННЫЕ действия** на hello вправо **«Параметры запроса»** панели обновления сервера hello и имена баз данных как hello выше действия и нажмите кнопку ОК.
   * После того, как интерактивная задней toohello предыдущую страницу, закройте окно приветствия. В появившемся сообщении нажмите кнопку **Применить**. Наконец, нажмите кнопку hello **Сохранить** кнопку toosave hello изменения. Файл Power BI теперь установил toohello соединения сервера. Если визуализаций пусты, убедитесь, что снимите hello выбранных элементов на toovisualize визуализации hello все данные hello, щелкнув значок ластика hello в верхнем правом углу hello условных обозначений hello. Используйте новые данные кнопки обновления tooreflect hello на визуализации hello. Изначально вы увидите только hello начального значения данных в визуализации как фабрика данных hello запланированных toorefresh каждые 3 часа. После 3 часа будет отображено новые прогнозы, отражаются в визуализации, при обновлении данных hello.
3. (Необязательно) Публикация мониторинга hello холодного путь слишком[Power BI в Интернете](http://www.powerbi.com/). Обратите внимание, что этот шаг требует учетной записи Power BI (или учетной записи Office 365).
   
   * Нажмите кнопку **«Опубликовать»** и несколько секунд позже, появляется окно отображения «Публикация tooPower BI успехов!» Щелкните ссылку "Открыть PredictiveMaintenanceAerospace.pbix в Power BI". Щелкните ссылку hello под «Открыть PredictiveMaintenanceAerospace.pbix в Power BI». toofind подробные инструкции см. в разделе [публикация из Power BI Desktop](https://support.powerbi.com/knowledgebase/articles/461278-publish-from-power-bi-desktop).
   * toocreate новую панель мониторинга: щелкните hello  **+**  входа Далее toothe **панелей мониторинга** раздел в левой области hello. Введите имя hello «Прогнозной Demo обслуживания» для этой новой панели мониторинга.
   * После открытия отчета hello щелкните ![значок БУЛАВКИ](media/cortana-analytics-technical-guide-predictive-maintenance/icon-pin.png) toopin все панели мониторинга tooyour визуализации. toofind подробные инструкции см. в разделе [Закрепление панели мониторинга Power BI tooa плитки из отчета](https://support.powerbi.com/knowledgebase/articles/430323-pin-a-tile-to-a-power-bi-dashboard-from-a-report).
     Переход на страницу панели мониторинга toohello и настроить hello размер и расположение визуализации и изменить их заголовки. toofind подробные инструкции, как tooedit плиток, см. статью [редактирование плитки — изменение размера, перемещение, переименование, ПИН-код, удалить, добавить гиперссылку](https://powerbi.microsoft.com/documentation/powerbi-service-edit-a-tile-in-a-dashboard/#rename). Ниже приведен пример панели мониторинга с помощью некоторых tooit визуализации закрепленные холодного путь.  В зависимости от того, как долго запуске генератора данных может отличаться на визуализации hello эти номера.
     <br/>
     ![Окончательное представление](media/cortana-analytics-technical-guide-predictive-maintenance/final-view.png)
     <br/>
   * Обновление tooschedule hello данных, наведите указатель мыши hello **PredictiveMaintenanceAerospace** набора данных, нажмите кнопку ![значок многоточия](media/cortana-analytics-technical-guide-predictive-maintenance/icon-elipsis.png) и выберите **запланировать обновление**.
     <br/>
     **Примечание:** появление массаже предупреждение, щелкните **изменение учетных данных** и убедитесь, что учетные данные базы данных являются Здравствуйте таким же, как описано в шаге 1.
     <br/>
     ![Планирование обновления](media/cortana-analytics-technical-guide-predictive-maintenance/schedule-refresh.png)
     <br/>
   * Разверните hello **запланировать обновление** раздела. Включите параметр "Поддерживать актуальность данных".
     <br/>
   * Запланировать обновление hello, в соответствии со своими потребностями. toofind Дополнительные сведения см. в разделе [обновление данных в Power BI](https://support.powerbi.com/knowledgebase/articles/474669-data-refresh-in-power-bi).

### <a name="setup-hot-path-dashboard"></a>Настройка панели мониторинга горячего пути
Hello следующие шаги помогут вам как данных реального времени toovisualize выходные данные Stream Analytics заданий, которые были созданы во время развертывания решения hello. Объект [Power BI в Интернете](http://www.powerbi.com/) учетная запись является обязательным tooperform hello следующие шаги. Если у вас нет учетной записи, вы можете [создать ее](https://powerbi.microsoft.com/pricing).

1. Добавьте выходные данные Power BI в Azure Stream Analytics (ASA).
   
   * Вам потребуется toofollow hello инструкциям [Azure Stream Analytics и Power BI: панель мониторинга в режиме реального времени для потоковой передачи данных в реальном](../stream-analytics/stream-analytics-power-bi-dashboard.md) tooset hello выходной файл задания Azure Stream Analytics как Power Бизнес-АНАЛИТИКИ панели мониторинга.
   * Hello ASA запрос имеет три выхода, которые являются **aircraftmonitor**, **aircraftalert**, и **flightsbyhour**. Выберите на вкладке запросов можно просмотреть запрос hello. Соответствующий tooeach из этих таблиц требуется tooadd tooASA выходных данных. При добавлении первого выхода hello (*например* **aircraftmonitor**) убедитесь, что hello **Псевдоним выхода**, **имя набора данных** и  **Имя таблицы** являются одинаковыми hello (**aircraftmonitor**). Выводит tooadd hello повторите шаги для **aircraftalert**, и **flightsbyhour**. После добавления всех трех выходные таблицы и запустил задание ASA hello, вы должны получить сообщение с подтверждением (*например*, «Запуск задания Stream Analytics успешно maintenancesa02asapbi»).
2. Войдите в слишком[Power BI в Интернете](http://www.powerbi.com)
   
   * На левой панели наборов данных в "Мои представления" hello ***DATASET*** имена **aircraftmonitor**, **aircraftalert**, и **flightsbyhour**должны отображаться. Это hello потоковой передачи данных при передаче из Azure Stream Analytics в hello предыдущего набора данных step.hello **flightsbyhour** могут не отображаться в hello же время, как другие два набора данных из-за характера toohello hello SQL-запроса за hello его. Однако он должен появиться через час.
   * Убедитесь, что hello ***визуализации*** области открыт и отображается в правой части экрана приветствия.
3. После получения данных hello, поступающих в Power BI можно запустить, визуализация hello потоковой передачи данных. Ниже приведен пример панели мониторинга с визуализации Горячий путь закрепленные tooit. На основе соответствующих наборов данных можно создать другие плитки панели мониторинга. В зависимости от того, как долго запуске генератора данных может отличаться на визуализации hello эти номера.

    ![Представление панели мониторинга](media\cortana-analytics-technical-guide-predictive-maintenance\dashboard-view.png)

1. Ниже приведены некоторые действия toocreate одной плитки приветствия выше — hello «парк представление датчик 11 vs. Threshold 48.26":
   
   * Выберите набор данных **aircraftmonitor** на hello слева панели наборов данных.
   * Нажмите кнопку hello **график** значок.
   * Нажмите кнопку **обработано** в hello **поля** области, поэтому что он отображается в области «Ось» hello **визуализации** области.
   * Нажмите кнопку s11 и s11alert\_alert, чтобы они отображались в группе "Значения". Щелкните маленькую стрелку hello рядом слишком**s11** и **s11\_предупреждение**, измените «Сумма» слишком «среднее».
   * Нажмите кнопку **Сохранить** на верхней hello и назовите hello отчета «aircraftmonitor». Отчет с именем «aircraftmonitor» будет отображаться в hello **отчеты** раздела hello **Навигатор** hello левую панель.
   * Нажмите кнопку hello **ПИН-кода Visual** значок в верхнем правом углу hello этого графика. Окно «TooDashboard ПИН-код» может отображаться для выбора панели мониторинга. Выберите "Демонстрация прогнозируемого обслуживания", а затем нажмите кнопку "Закрепить".
   * Наведите указатель мыши hello этой плитки на панели мониторинга hello, щелкните значок «edit» hello в правом верхнем углу toochange hello слишком его название «флот представление датчик 11 vs. Пороговое значение 48,26" и подзаголовок слишком «среднее значение между флот во времени».

## <a name="how-toodelete-your-solution"></a>**Как toodelete решения**
Убедитесь, что остановка hello генератора данных при использовании не активно hello решений при запуске генератора данных hello повлечет за собой более высокими затратами. Удалите hello решение, если оно не используется. Удаление решения приведет к удалению всех компонентов hello подготовлены в вашей подписке при развертывании решения hello. решение hello toodelete щелкните свое имя решения в левой панели hello hello шаблон решения и нажмите кнопку Удалить.

## <a name="cost-estimation-tools"></a>**Средства для оценки затрат**
Hello следующие два средства, доступные toohelp лучше понять общее затраты, связанные с запуском hello превентивного обслуживания для Аэрокосмических шаблон решения в вашей подписки:

* [Средство оценки затрат Azure Microsoft (в сети)](https://azure.microsoft.com/pricing/calculator/)
* [Средство оценки затрат Azure Microsoft (на рабочем столе)](http://www.microsoft.com/download/details.aspx?id=43376)

