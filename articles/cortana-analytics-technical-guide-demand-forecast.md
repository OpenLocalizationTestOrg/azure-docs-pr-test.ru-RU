---
title: "Прогноз в энергии техническое руководство по aaaDemand | Документы Microsoft"
description: "Техническое руководство по toohello шаблон решения с помощью Cortana аналитики Microsoft для прогноз продаж в энергии."
services: cortana-analytics
documentationcenter: 
author: yijichen
manager: ilanr9
editor: yijichen
ms.assetid: 7f1a866b-79b7-4b97-ae3e-bc6bebe8c756
ms.service: cortana-analytics
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2016
ms.author: inqiu;yijichen;ilanr9
ms.openlocfilehash: c97b7c19c9e3a317aecc329e61a0692d2f1ec53e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="technical-guide-toohello-cortana-intelligence-solution-template-for-demand-forecast-in-energy"></a>Техническое руководство по toohello шаблон решения аналитики Cortana для прогноз продаж энергия
## <a name="overview"></a>**Обзор**
Шаблоны решений предназначены tooaccelerate hello процесс построения E2E Демонстрация поверх набора аналитики Cortana. Развернутого шаблона будет подготовить подписку с необходимым компонентом Cortana аналитики и построения hello связи между. Он также заполняет конвейера данных hello с образцами данных, получение создан из приложения моделирования данных. Имитатор hello данные по ссылке hello и установить его на локальном компьютере, см. в файле readme.txt toohello инструкции по использованию симулятор hello. Данные, созданные из hello симулятора будет заполнить hello конвейера данных и начала создания машины предсказания обучения можно представить на панели мониторинга Power BI hello.

шаблон Hello решения можно найти [здесь](https://gallery.cortanaintelligence.com/SolutionTemplate/Demand-Forecasting-for-Energy-1)

процесс развертывания Hello поможет выполнить несколько шагов tooset копии решения учетные данные. Убедитесь, что записывать эти учетные данные, такие как имя решения, имя пользователя и пароль, предоставленные во время развертывания hello.

Hello цель данного документа — Эталонная архитектура tooexplain hello и различные компоненты подготовлены в вашей подписке, в рамках этого решения шаблона. Hello документ также рассмотрен как tooreplace hello образец данных с реальными данными собственные toobe может toosee аналитики и прогнозы от вас выиграл данных. Кроме того hello документе рассказывается о hello части решения шаблон, который необходимо изменить, если требуется решение hello toocustomize с собственными данными toobe hello. В конце hello приведены инструкции как toobuild hello панели мониторинга Power BI для этого шаблона решения.

## <a name="big-picture"></a>**Общая картина**
![](media/cortana-analytics-technical-guide-demand-forecast/ca-topologies-energy-forecasting.png)

### <a name="architecture-explained"></a>Описание архитектуры
При развертывании решения hello различных служб Azure в Cortana Analytics Suite активируются (*т. е.* концентратор событий, Stream Analytics, HDInsight, фабрика данных, машинное обучение *и т. д.*). Hello архитектура приведенной выше схеме показаны, в общем, создание hello прогноз спроса для шаблона решения энергии от начала до конца. Будет может tooinvestigate эти службы, щелкнув на них hello диаграмма шаблон решения, созданных с помощью развертывания hello hello решения. Hello в следующих разделах описывается каждый из сегментов.

## <a name="data-source-and-ingestion"></a>**Источник данных и прием**
### <a name="synthetic-data-source"></a>Источник искусственных данных
Для этого шаблона, данные hello используемого источника формируется из приложения рабочего стола, который будет загружать и запускать локально, после успешного развертывания. Будет найти toodownload инструкции hello и установить это приложение hello панели свойств при выборе hello первый узел, называемый симулятор данных прогнозирования энергии на схеме шаблона решения hello. Это приложение веб-каналы hello [концентратор событий Azure](#azure-event-hub) службой точек данных или событий, которые будут использоваться hello конца потока hello решения.

Создание приложения Hello событий будет заполнять hello концентратор событий Azure только при выполнении на компьютере.

### <a name="azure-event-hub"></a>концентратору событий Azure
Hello [концентратор событий Azure](https://azure.microsoft.com/services/event-hubs/) службы — получатель hello hello входных данных, предоставленных hello искусственного источника данных, описанных выше.

## <a name="data-preparation-and-analysis"></a>**Подготовка и анализ данных**
### <a name="azure-stream-analytics"></a>Azure Stream Analytics
Hello [Azure Stream Analytics](https://azure.microsoft.com/services/stream-analytics/) служба является используемым tooprovide рядом с аналитикой в реальном времени на hello входного потока из hello [концентратор событий Azure](#azure-event-hub) службы и опубликовать результаты на [Power BI](https://powerbi.microsoft.com) панели мониторинга, а также архивирование все необработанные входящие события toohello [хранилища Azure](https://azure.microsoft.com/services/storage/) службу для последующей обработки hello [фабрики данных Azure](https://azure.microsoft.com/documentation/services/data-factory/) службы.

### <a name="hd-insights-custom-aggregation"></a>Пользовательская агрегация HD Insights
Hello службы анализ HD Azure — используется toorun [Hive](http://blogs.msdn.com/b/bigdatasupport/archive/2013/11/11/get-started-with-hive-on-hdinsight.aspx) агрегаты tooprovide скриптов (под управлением фабрики данных Azure) на hello необработанные события, которые были архивированы, с помощью службы Azure Stream Analytics hello.

### <a name="azure-machine-learning"></a>Машинное обучение Azure
Hello [машинного обучения Azure](https://azure.microsoft.com/services/machine-learning/) (под управлением фабрики данных Azure) используется служба toomake прогноз на будущие энергопотребление в выбранном регионе, на основе полученных входных данных hello.

## <a name="data-publishing"></a>**Публикация данных**
### <a name="azure-sql-database-service"></a>Служба базы данных SQL Azure
Hello [базы данных SQL Azure](https://azure.microsoft.com/services/sql-database/) службы — прогнозы hello используется toostore (управляемые фабрикой данных Azure), полученных hello службы машинного обучения Azure, которая будет использоваться в hello [Power BI](https://powerbi.microsoft.com) панели мониторинга.

## <a name="data-consumption"></a>**Использование данных**
### <a name="power-bi"></a>Power BI
Hello [Power BI](https://powerbi.microsoft.com) служба является tooshow используется панель мониторинга, которая содержит статистические вычисления, предоставляемые hello [Azure Stream Analytics](https://azure.microsoft.com/services/stream-analytics/) службы, а также запросу прогноз результаты, сохраненные в [Azure SQL База данных](https://azure.microsoft.com/services/sql-database/) , полученных с помощью hello [машинного обучения Azure](https://azure.microsoft.com/services/machine-learning/) службы. Инструкции по как toobuild hello панели мониторинга Power BI для этого шаблона решения см. ниже toohello.

## <a name="how-toobring-in-your-own-data"></a>**Как toobring свои данные**
В этом разделе описываются toobring tooAzure собственных данных и области, которые может потребоваться изменение hello данных можно перевести в этой архитектуре.

Маловероятно, что любой набор данных, которые вы переносите будет соответствовать hello набор данных, используемый для этого шаблона решения. Основные сведения о данных и требования будут важны в изменении toowork этого шаблона с собственными данными. Если это ваш первый toohello уязвимость службы машинного обучения Azure, tooit Общие сведения можно получить с помощью пример hello в [как toocreate эксперимента первый](machine-learning/machine-learning-create-experiment.md).

Hello в следующих разделах обсуждаются разделах hello hello шаблона, который потребуется изменить при появился новый набор данных.

### <a name="azure-event-hub"></a>концентратору событий Azure
Hello [концентратор событий Azure](https://azure.microsoft.com/services/event-hubs/) служба является универсальным, таким образом, что данные могут быть разнесены концентратора toohello в формате CSV или JSON. Никакая специальная обработка происходит в концентратор событий Azure hello, но очень важно, что вы понимаете hello данных, возвращаемых в него.

В этом документе не описывается, как tooingest данных, но одна может легко отправлять события или tooan данных концентратор событий Azure, с помощью hello [интерфейс API концентратора событий](event-hubs/event-hubs-programming-guide.md).

### <a name="azure-stream-analytics"></a>Azure Stream Analytics
Hello [Azure Stream Analytics](https://azure.microsoft.com/services/stream-analytics/) службы используется tooprovide практически в режиме реального времени является чтение из потоков данных и вывода данных tooany количество источников.

Для прогноза спроса для шаблона решения энергии hello hello Azure Stream Analytics запрос состоит из двух вложенных запросов, каждый получению событий из hello концентратор событий Azure service в качестве входных данных и различных местах tootwo выходные данные с. Эти выходные данные состоят из одного набора данных Power BI и одного места хранения Azure.

Hello [Azure Stream Analytics](https://azure.microsoft.com/services/stream-analytics/) запроса можно найти по:

* Вход в hello [портала управления Azure](https://manage.windowsazure.com/)
* Поиск заданий stream analytics hello ![](media/cortana-analytics-technical-guide-demand-forecast/icon-stream-analytics.png) , созданные при развертывании решения hello. Один — для помещения tooblob хранения данных (например, mytest1streaming432822asablob) и hello другая половина — один для помещения tooPower данных бизнес-Аналитики (например mytest1streaming432822asapbi).
* Выбрать

  * ***Входные данные*** tooview входных данных запроса hello
  * ***ЗАПРОС*** сам запрос tooview hello
  * ***ВЫВОДИТ*** tooview hello различные выходы

Сведения о построении запросов Azure Stream Analytics находятся в hello [Справка запросов Stream Analytics](https://msdn.microsoft.com/library/azure/dn834998.aspx) на сайте MSDN.

В этом решении hello задание Azure Stream Analytics, которое выводит набор данных с рядом с аналитикой в реальном времени сведения о hello входящих данных потока tooa панели мониторинга Power BI, если в рамках этого решения шаблона. Поскольку неявные сведения о входящих данных формате hello, эти запросы потребуется изменить toobe на основе вашего формата данных.

Hello другое задание Azure Stream Analytics выводит все [концентратора событий](https://azure.microsoft.com/services/event-hubs/) событий для [хранилища Azure](https://azure.microsoft.com/services/storage/) и требующий без изменения независимо от вашего формата данных как потоковый hello событий сведения toostorage.

### <a name="azure-data-factory"></a>Фабрика данных Azure
Hello [фабрики данных Azure](https://azure.microsoft.com/documentation/services/data-factory/) управляет служба перемещения hello и обработку данных. В hello прогноз спроса для данных hello шаблон решения энергии фабрики состоит из двенадцати [конвейеры](data-factory/data-factory-create-pipelines.md) , перемещения и обработки данных hello, с использованием различных технологий.

  Фабрики данных можно открыть, открыв узел фабрики данных hello внизу hello hello решения шаблона схемой, созданной с помощью развертывания hello hello решения. Это займет вы toohello фабрики данных на портале управления Azure. При обнаружении ошибок в наборах данных, можно пропустить те как из-за toodata фабрики развертывания до запуска генератора данных hello. Эти ошибки не мешают работе фабрики данных.

В этом разделе рассматриваются необходимые hello [конвейеры](data-factory/data-factory-create-pipelines.md) и [действия](data-factory/data-factory-create-pipelines.md) содержащихся в hello [фабрики данных Azure](https://azure.microsoft.com/documentation/services/data-factory/). Ниже приведен представление диаграммы hello hello решения.

![](media/cortana-analytics-technical-guide-demand-forecast/ADF2.png)

Содержит пять конвейеров hello этой фабрики [Hive](http://blogs.msdn.com/b/bigdatasupport/archive/2013/11/11/get-started-with-hive-on-hdinsight.aspx) скрипты, используемые toopartition и hello статистические данные. Если отмечено, hello скриптов будет находиться в hello [хранилища Azure](https://azure.microsoft.com/services/storage/) учетную запись, созданную во время установки. Их расположение: demandforecasting\\\\script\\\\hive\\\\ (или https://[имя вашего решения].blob.core.windows.net/demandforecasting).

Аналогичные toohello [Azure Stream Analytics](#azure-stream-analytics-1) запросы, [Hive](http://blogs.msdn.com/b/bigdatasupport/archive/2013/11/11/get-started-with-hive-on-hdinsight.aspx) скрипты имеют неявные сведения о входящих данных формате hello, эти запросы потребуется изменить toobe на основе формата данных и [компонентов engineering](machine-learning/machine-learning-feature-selection-and-engineering.md) требования.

#### <a name="aggregatedemanddatato1hrpipeline"></a>*AggregateDemandDataTo1HrPipeline*
Это [конвейера](data-factory/data-factory-create-pipelines.md) конвейера содержит одно действие - [HDInsightHive](data-factory/data-factory-hive-activity.md) действия с помощью [HDInsightLinkedService](https://msdn.microsoft.com/library/azure/dn893526.aspx) , на котором запущена [Hive](http://blogs.msdn.com/b/bigdatasupport/archive/2013/11/11/get-started-with-hive-on-hdinsight.aspx)сценарий tooaggregate hello каждые 10 секунд потоковый в данных по запросу на уровне области подстанции уровня toohourly и поместить в [хранилища Azure](https://azure.microsoft.com/services/storage/) через задание Azure Stream Analytics hello.

Скрипт [Hive](http://blogs.msdn.com/b/bigdatasupport/archive/2013/11/11/get-started-with-hive-on-hdinsight.aspx) для этой задачи секционирования — ***AggregateDemandRegion1Hr.hql***.

#### <a name="loadhistorydemanddatapipeline"></a>*LoadHistoryDemandDataPipeline*
Этот [конвейер](data-factory/data-factory-create-pipelines.md) содержит два действия:

* [HDInsightHive](data-factory/data-factory-hive-activity.md) действия с помощью [HDInsightLinkedService](https://msdn.microsoft.com/library/azure/dn893526.aspx) , выполняет куст сценарий данных запросу tooaggregate hello почасовой журнала на уровне области подстанции уровня toohourly и поместить в хранилище Azure во время hello Azure Задание Stream Analytics
* [Копировать](https://msdn.microsoft.com/library/azure/dn835035.aspx) действие, перемещающее hello статистические данные из хранилища Azure blob toohello базы данных SQL Azure, которая была создана как часть установки шаблона решения hello.

Hello [Hive](http://blogs.msdn.com/b/bigdatasupport/archive/2013/11/11/get-started-with-hive-on-hdinsight.aspx) скрипт для этой задачи является ***AggregateDemandHistoryRegion.hql***.

#### <a name="mlscoringregionxpipeline"></a>*MLScoringRegionXPipeline*
Эти [конвейеры](data-factory/data-factory-create-pipelines.md) содержит несколько действий и которого конечным результатом является hello оцененных прогнозы на основании hello эксперимента машинного обучения Azure, связанный с этим шаблоном решения. Они практически идентичны за исключением того, каждый из них обрабатывает только hello различные области, которая осуществляется другой RegionID передается в конвейер ADF hello и скрипт hive hello для каждого региона.  
Hello действия, содержащиеся в этом являются:

* [HDInsightHive](data-factory/data-factory-hive-activity.md) действия с помощью [HDInsightLinkedService](https://msdn.microsoft.com/library/azure/dn893526.aspx) , выполняет куст сценарий tooperform агрегаты и возможностей разработки, необходимые для hello эксперимента машинного обучения Azure. Hello скрипты Hive для выполнения этой задачи соответствующих ***PrepareMLInputRegionX.hql***.
* [Копировать](https://msdn.microsoft.com/library/azure/dn835035.aspx) действия, которое перемещает hello результаты из hello [HDInsightHive](data-factory/data-factory-hive-activity.md) действия tooa один BLOB-хранилища Azure, можно получить доступ по hello [AzureMLBatchScoring](https://msdn.microsoft.com/library/azure/dn894009.aspx) действия.
* [AzureMLBatchScoring](https://msdn.microsoft.com/library/azure/dn894009.aspx) действия, которое вызывает hello эксперимента машинного обучения Azure, что приводит к hello приводит был помещен в один большой двоичный объект хранилища Azure.

#### <a name="copyscoredresultregionxpipeline"></a>*CopyScoredResultRegionXPipeline*
Эти [конвейеры](data-factory/data-factory-create-pipelines.md) содержал единственное действие - [копирования](https://msdn.microsoft.com/library/azure/dn835035.aspx) действия, которое перемещает hello hello эксперимента машинного обучения Azure результаты из соответствующих hello ***MLScoringRegionXPipeline *** toohello базы данных SQL Azure, которая была создана как часть установки шаблона решения hello.

#### <a name="copyaggdemandpipeline"></a>*CopyAggDemandPipeline*
Это [конвейеры](data-factory/data-factory-create-pipelines.md) содержал единственное действие - [копирования](https://msdn.microsoft.com/library/azure/dn835035.aspx) действие, перемещающее hello суммарный запросу текущих данных от ***LoadHistoryDemandDataPipeline*** toohello Azure База данных SQL, была создана как часть установки шаблона решения hello.

#### <a name="copyregiondatapipeline-copysubstationdatapipeline-copytopologydatapipeline"></a>*CopyRegionDataPipeline, CopySubstationDataPipeline, CopyTopologyDataPipeline*
Эти [конвейеры](data-factory/data-factory-create-pipelines.md) содержал единственное действие - [копирования](https://msdn.microsoft.com/library/azure/dn835035.aspx) действие, перемещающее hello ссылочных данных из области, подстанции/Topologygeo, которые загружены tooAzure хранилища BLOB-объектов как часть решения hello toohello установки шаблона базы данных SQL Azure, которая была создана как часть установки шаблона решения hello.

### <a name="azure-machine-learning"></a>Машинное обучение Azure
Hello [машинного обучения Azure](https://azure.microsoft.com/services/machine-learning/) поэкспериментировать используется для этого шаблона решение обеспечивает hello прогноза спроса области. Hello эксперимента является набор данных конкретного toohello потребляет и потребует изменения или замены определенных toohello данных, получаемых в.

## <a name="monitor-progress"></a>**Отслеживание хода выполнения**
После запуска hello генератора данных hello конвейера начинает tooget структура данных, а hello различные компоненты решения запускать в самом начале, в действие, следующие команды hello выданный hello фабрики данных. Вы можете отслеживать конвейера hello двумя способами.

1. Проверьте hello данные из хранилища больших двоичных объектов.

    Одно из задания Stream Analytics hello записывает hello необработанные входящие tooblob хранения данных. При нажатии на **хранилища больших двоичных объектов** компонент решения от hello экране вы успешно развернутое приложение hello решения, а затем нажмите кнопку **откройте** в правой панели hello займет toohello [Портала управления azure](https://portal.azure.com). На портале щелкните **BLOB-объекты**. В следующей панели hello вы увидите список контейнеров. Щелкните **energysadata**. В следующей панели hello, вы увидите hello **«demandongoing»** папки. В папке rawdata hello, вы увидите папки с именами, например по дате = 2016-01-28 и т. д. При появлении этих папок, он указывает, hello необработанные данные успешно выполняется на компьютере и сохраняется в хранилище больших двоичных объектов. Вы увидите файлы, которые должны иметь в этих папках ограничение по размерам (в МБ).
2. Проверьте hello данные из базы данных SQL Azure.

    Последний шаг Hello hello конвейера — toowrite данных (например, прогнозы на основании машинного обучения) в базу данных SQL. Может потребоваться toowait до 2 часов hello tooappear данных в базе данных SQL. Одним из способов toomonitor объем данных в базе данных SQL — через [портала управления Azure](https://manage.windowsazure.com/). На левой панели hello найдите баз данных SQL![](media/cortana-analytics-technical-guide-demand-forecast/SQLicon2.png) и щелкните его. Затем найдите свою базу данных (например demo123456db) и щелкните ее. На следующей странице hello под **«Connect tooyour базы данных»** щелкните **«Запросы выполнения Transact-SQL к базе данных SQL»**.

    Здесь можно щелкнуть нового запроса и запрос для hello число строк (например «select count(*) из DemandRealHourly)» по мере роста базы данных hello количество строк в таблице hello должно увеличиваться.)
3. Проверьте данные hello из панели мониторинга Power BI.

    Можно настроить Power BI Горячий путь мониторинга toomonitor hello необработанные входящие данные. Следуйте инструкциям hello hello «Панели мониторинга Power BI» раздела.

## <a name="power-bi-dashboard"></a>**Панель мониторинга Power BI**
### <a name="overview"></a>Обзор
В этом разделе описывается, как tooset копирование toovisualize панели мониторинга Power BI данные реальном времени от Azure потоковой аналитики (Горячий путь), как также как прогноза результатов из машинного обучения Azure (холодный путь).

### <a name="setup-hot-path-dashboard"></a>Настройка панели мониторинга горячего пути
Hello следующие шаги помогут вам как данных реального времени toovisualize выходные данные Stream Analytics заданий, которые были созданы во время развертывания решения hello. Объект [Power BI в Интернете](http://www.powerbi.com/) учетная запись является обязательным tooperform hello следующие шаги. Если у вас нет учетной записи, вы можете [создать ее](https://powerbi.microsoft.com/pricing).

1. Добавьте выходные данные Power BI в Azure Stream Analytics (ASA).

   * Вам потребуется toofollow hello инструкциям [Azure Stream Analytics и Power BI: панель мониторинга в режиме реального времени для потоковой передачи данных в реальном](stream-analytics/stream-analytics-power-bi-dashboard.md) tooset hello выходной файл задания Azure Stream Analytics как Power Бизнес-АНАЛИТИКИ панели мониторинга.
   * Найдите задание stream analytics hello в вашей [портала управления Azure](https://manage.windowsazure.com). должно быть имя Hello задания hello: YourSolutionName + streamingjob «» + случайное число + «asapbi» (т. е. demostreamingjob123456asapbi).
   * Добавление выходных данных PowerBI для задания ASA hello. Набор hello **Псевдоним выхода** как **«PBIoutput»**. Для параметров **Имя набора данных** и **Имя таблицы** укажите **EnergyStreamData**. После добавления вывода приветствия щелкните **«Start»** внизу hello задания Stream Analytics hello toostart страницу приветствия. Должно появиться сообщение с подтверждением (*например*, "Запуск задания Stream Analytics myteststreamingjob12345asablob выполнен успешно").
2. Войдите в слишком[Power BI в Интернете](http://www.powerbi.com)

   * На левой панели наборов данных в "Мои представления" hello можно будет toosee новый отображение набора данных на левой панели Power BI hello. Это hello потоковой передачи данных, которые можно отправить из Azure Stream Analytics в предыдущем шаге hello.
   * Убедитесь, что hello ***визуализации*** области открыт и отображается в правой части экрана приветствия.
3. Создайте плитку «Запросу, отметка времени» hello:

   * Выберите набор данных **«EnergyStreamData»** на hello слева панели наборов данных.
   * Щелкните значок **График** ![](media/cortana-analytics-technical-guide-demand-forecast/PowerBIpic8.png).
   * Щелкните EnergyStreamData в панели **Поля** .
   * Щелкните **Отметка времени** и убедитесь, что она отображается в разделе "Ось". Щелкните **Нагрузка** и убедитесь, что она отображается в разделе "Ось".
   * Нажмите кнопку **Сохранить** на верхней hello и назовите hello отчет в виде «EnergyStreamDataReport». Hello отчет с именем «EnergyStreamDataReport» будет отображаться в разделе "Отчеты" в области навигатора hello слева.
   * Нажмите кнопку **«Visual ПИН-код»** ![](media/cortana-analytics-technical-guide-demand-forecast/PowerBIpic6.png) значок в правом верхнем углу этого графика, окно «TooDashboard ПИН-код» может отображаться для вас toochoose панели мониторинга. Выберите "EnergyStreamDataReport" и щелкните "Закрепить".
   * Наведите указатель мыши hello через эту плитку на панели мониторинга hello, нажмите кнопку «Изменить» значок в правом верхнем углу toochange его название, как «Запросу, отметка времени»
4. Создайте плитки других панелей мониторинга на основе соответствующих наборов данных. Ниже приведен представление Hello окончательного панели мониторинга.
     ![](media/cortana-analytics-technical-guide-demand-forecast/PBIFullScreen.png)

### <a name="setup-cold-path-dashboard"></a>Настройка панели мониторинга холодного пути
В конвейере данных холодного путь hello essential предназначена прогноза спроса hello tooget каждой области. Power BI подключается tooan базы данных Azure SQL в качестве источника данных, где хранятся результаты прогноза hello.

> [!NOTE]
> 1) Он принимает несколько часов toocollect достаточно прогноза результатов для мониторинга "hello". Мы рекомендуем начать этот процесс 2-3 часа после обед hello генератора данных. (2) на этом шаге условием hello toodownload и установите hello программное обеспечение предоставляется бесплатно [Power BI desktop](https://powerbi.microsoft.com/desktop).
>
>

1. Получите учетные данные базы данных hello.

   Вам потребуется **базы данных, имя сервера, имя базы данных, имя пользователя и пароль** перед перемещением toonext действия. Ниже приведены шаги tooguide hello вы как toofind их.

   * Когда **База данных SQL Azure** на схеме шаблона решения станет зеленой, щелкните ее и нажмите кнопку **Открыть**. Будет интерактивная tooAzure портала управления, а также открывается страница сведений о вашей базы данных.
   * На странице приветствия можно найти раздел «Database». В нем перечислены помещает hello базу данных, который был создан. Hello имя базы данных должно быть **«На имя решения + случайное число + «db»»** (например «mytest12345db»).
   * Выберите базу данных, в новый, разверните панель, можно найти имя сервера базы данных в верхней части hello hello. Имя сервера базы данных должно иметь формат: **имя_решения + случайное число + database.windows.net,1433** (например, mytest12345.database.windows.net,1433).
   * Базы данных **username** и **пароль** : hello так же, как hello имени пользователя и пароля с заранее записанным во время развертывания решения hello.
2. Обновление источника данных hello hello холодного пути файла Power BI

   * Убедитесь, что вы установили hello последнюю версию [Power BI desktop](https://powerbi.microsoft.com/desktop).
   * В hello **«DemandForecastingDataGeneratorv1.0»** загруженный папки, дважды щелкните hello **«Power BI Template\DemandForecastPowerBI.pbix»** файла. Начальный визуализации Hello основаны на фиктивные данные. **Примечание:** Если появляется ошибка передать, убедитесь, что вы установили последнюю версию Power BI Desktop hello.

     После его открытии, в верхней части hello hello файла, нажмите кнопку **изменить запросы**. В окне pop hello, дважды щелкните **«Источник»** на правой панели hello.
     ![](media/cortana-analytics-technical-guide-demand-forecast/PowerBIpic1.png)
   * В окне pop hello, замените **«Server»** и **«Database»** с собственные имена сервера и базы данных, а затем щелкните **«OK»**. Для имени сервера, убедитесь, что указан hello порт 1433 (**YourSolutionName.database.windows.net 1433**). Игнорируйте hello предупреждающие сообщения, которые отображаются на экране приветствия.
   * В hello далее в новом окне окно, вы увидите два варианта на левой панели hello (**Windows** и **базы данных**). Нажмите кнопку **«Database»**, заполните вашей **«Username»** и **«Password»** (это hello имя пользователя и пароль, введенный при развертывании решения hello и создании База данных Azure SQL). В ***выберите которой уровня tooapply эти параметры требуется***, проверьте параметр уровня базы данных. Щелкните **Подключить**.
   * После того, как интерактивная задней toohello предыдущую страницу, закройте окно приветствия. В появившемся сообщении нажмите кнопку **Применить**. Наконец, нажмите кнопку hello **Сохранить** кнопку toosave hello изменения. Файл Power BI теперь установил toohello соединения сервера. Если визуализаций пусты, убедитесь, что снимите hello выбранных элементов на toovisualize визуализации hello все данные hello, щелкнув значок ластика hello в верхнем правом углу hello условных обозначений hello. Используйте новые данные кнопки обновления tooreflect hello на визуализации hello. Изначально вы увидите только hello начального значения данных в визуализации как фабрика данных hello запланированных toorefresh каждые 3 часа. После 3 часа будет отображено новые прогнозы, отражаются в визуализации, при обновлении данных hello.
3. (Необязательно) Публикация мониторинга hello холодного путь слишком[Power BI в Интернете](http://www.powerbi.com/). Обратите внимание, что этот шаг требует учетной записи Power BI (или учетной записи Office 365).

   * Нажмите кнопку **«Опубликовать»** и несколько секунд позже, появляется окно отображения «Публикация tooPower BI успехов!» Щелкните ссылку "Открыть PredictiveMaintenanceAerospace.pbix в Power BI". Щелкните ссылку hello под «Открыть demoprediction.pbix в Power BI». toofind подробные инструкции см. в разделе [публикация из Power BI Desktop](https://support.powerbi.com/knowledgebase/articles/461278-publish-from-power-bi-desktop).
   * toocreate новую панель мониторинга: щелкните hello  **+**  входа Далее toothe **панелей мониторинга** раздел в левой области hello. Введите имя hello «Demo прогноз спроса» для этой новой панели мониторинга.
   * После открытия отчета hello щелкните ![](media/cortana-analytics-technical-guide-demand-forecast/PowerBIpic6.png) toopin все панели мониторинга tooyour визуализации. toofind подробные инструкции см. в разделе [Закрепление панели мониторинга Power BI tooa плитки из отчета](https://support.powerbi.com/knowledgebase/articles/430323-pin-a-tile-to-a-power-bi-dashboard-from-a-report).
     Переход на страницу панели мониторинга toohello и настроить hello размер и расположение визуализации и изменить их заголовки. toofind подробные инструкции, как tooedit плиток, см. статью [редактирование плитки — изменение размера, перемещение, переименование, ПИН-код, удалить, добавить гиперссылку](https://powerbi.microsoft.com/documentation/powerbi-service-edit-a-tile-in-a-dashboard/#rename). Ниже приведен пример панели мониторинга с помощью некоторых tooit визуализации закрепленные холодного путь.

     ![](media/cortana-analytics-technical-guide-demand-forecast/PowerBIpic7.png)
4. (Необязательно) Запланировать обновление источника данных hello.

   * Обновление tooschedule hello данных, наведите указатель мыши hello **EnergyBPI Final** набора данных, нажмите кнопку ![](media/cortana-analytics-technical-guide-demand-forecast/PowerBIpic3.png) и выберите **запланировать обновление**.
     **Примечание:** появление массаже предупреждение, щелкните **изменение учетных данных** и убедитесь, что учетные данные базы данных являются Здравствуйте таким же, как описано в шаге 1.

     ![](media/cortana-analytics-technical-guide-demand-forecast/PowerBIpic4.png)
   * Разверните hello **запланировать обновление** раздела. Включите параметр "Поддерживать актуальность данных".
   * Запланировать обновление hello, в соответствии со своими потребностями. toofind Дополнительные сведения см. в разделе [обновление данных в Power BI](https://powerbi.microsoft.com/documentation/powerbi-refresh-data/).

## <a name="how-toodelete-your-solution"></a>**Как toodelete решения**
Убедитесь, что остановка hello генератора данных при использовании не активно hello решений при запуске генератора данных hello повлечет за собой более высокими затратами. Удалите hello решение, если оно не используется. Удаление решения приведет к удалению всех компонентов hello подготовлены в вашей подписке при развертывании решения hello. решение hello toodelete щелкните свое имя решения в левой панели hello hello шаблон решения и нажмите кнопку Удалить.

## <a name="cost-estimation-tools"></a>**Средства для оценки затрат**
Hello следующие два средства, доступные toohelp лучше понять общие затраты, задействованных в выполнении прогноза спроса hello для шаблона решения энергии в подписке:

* [Средство оценки затрат Azure Microsoft (в сети)](https://azure.microsoft.com/pricing/calculator/)
* [Средство оценки затрат Azure Microsoft (на рабочем столе)](http://www.microsoft.com/download/details.aspx?id=43376)

## <a name="acknowledgements"></a>**Благодарности**
Авторы этой статьи: специалист по обработке данных Ицзин Чен (Yijing Chen) и инженер по программному обеспечению Цю Мин (Qiu Min); оба автора работают в корпорации Майкрософт.
