---
title: "aaaConnect tooAzure HDInsight с помощью средств Озера данных для Visual Studio | Документы Microsoft"
description: "Узнайте, как tooinstall и использование средств Озера данных для Visual Studio tooconnect tooHadoop кластеров в Azure HDInsight и выполнения запросов Hive."
keywords: "средства hadoop, запрос hive, visual studio, visual studio hadoop"
services: HDInsight
documentationcenter: 
tags: azure-portal
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: ce9c572a-1e98-46bf-9581-13a9767f1fa5
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/23/2017
ms.author: jgao
ms.openlocfilehash: ff5819a64bebe5f4ab3cf763ce6c45c81aa34b19
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="connect-tooazure-hdinsight-and-run-hive-queries-using-data-lake-tools-for-visual-studio"></a>Подключение tooAzure HDInsight и выполнять запросы Hive, с помощью средств Озера данных для Visual Studio

Узнайте, как toouse Озера Data Tools для Visual Studio tooconnect tooHadoop кластеров в [Azure HDInsight](hdinsight-hadoop-introduction.md) и отправки запросов Hive. Дополнительные сведения об использовании HDInsight см. в разделе [tooHDInsight Введение](hdinsight-hadoop-introduction.md) и [Приступая к работе с HDInsight](hdinsight-hadoop-linux-tutorial-get-started.md). Дополнительные сведения о подключении tooa Storm кластера см. в разделе [разработки C# топологии применения Apache Storm на HDInsight с помощью Visual Studio](hdinsight-storm-develop-csharp-visual-studio-topology.md).

Средства Озера данных для Visual Studio может быть используется tooaccess аналитики Озера данных и HDInsight.  Hello сведения о средствах Озера данных см. в разделе [учебника: при разработке скриптов U-SQL, с помощью средств Озера данных для Visual Studio](../data-lake-analytics/data-lake-analytics-data-lake-tools-get-started.md).

**Предварительные требования**

toocomplete Озера данных hello этого учебника и использование средств в Visual Studio, вам потребуется следующее hello.

* Кластер Azure HDInsight: один, см. в разделе toocreate [приступить к работе с HDInsight под управлением Linux](hdinsight-hadoop-linux-tutorial-get-started.md)
* Рабочей станции с hello после программного обеспечения:
  
  * Windows 10, Windows 8.1, Windows 8 или Windows 7.
  * Visual Studio 2013, 2015, 2017.
    
    > [!NOTE]
    > В настоящее время средства Озера данных hello для Visual Studio только поставляются с hello английской версии.
    > 
    > 

## <a name="install-data-lake-tools-for-visual-studio"></a>Установка инструментов Data Lake для Visual Studio

Инструменты Data Lake устанавливаются по умолчанию для Visual Studio 2017. Для более старых версий, его можно установить с помощью hello [Web Platform Installer](https://www.microsoft.com/web/downloads/). Необходимо выбрать hello соответствующий вашей версии Visual Studio. Если у вас нет установленной среды Visual Studio, можно установить hello последние Visual Studio Community и пакета Azure SDK с помощью hello [Web Platform Installer](https://www.microsoft.com/web/downloads/):

![Средства Озера данных для установщика веб-платформы Visual Studio. ] (./media/hdinsight-hadoop-visual-studio-tools-get-started/hdinsight.visual.studio.tools.wpi.png "Tooinstall используйте установщик веб-платформы данных Озера средства для Visual Studio")

## <a name="connect-tooazure-subscriptions"></a>Подключение tooAzure подписки
Средства Озера данных для Visual Studio позволяет кластеров HDInsight tooyour tooconnect, некоторые операции базовую функциональность для управления и выполнения запросов Hive.

> [!NOTE]
> Сведения о подключении кластера Hadoop tooa универсального разделе [записи и отправки запросов Hive, с помощью Visual Studio](http://blogs.msdn.com/b/xiaoyong/archive/2015/05/04/how-to-write-and-submit-hive-queries-using-visual-studio.aspx).
> 
> 

**tooconnect tooyour подписки Azure**

1. Откройте Visual Studio.
2. Из hello **представление** меню, нажмите кнопку **обозревателя серверов** окна обозревателя серверов tooopen hello.
3. Разверните пункт **Azure**, а затем — **HDInsight**.
   
   > [!NOTE]
   > Обратите внимание hello **список задач HDInsight** окна должен быть открыт. Если вы не видите его, нажмите кнопку **другие окна** из hello **представление** меню, а затем нажмите **окно списка задач HDInsight**.  
   > 
   > 
4. Введите учетные данные подписки Azure и нажмите кнопку **Войти**. Это только требуется, если вы никогда не подключены toohello подписки Azure из Visual Studio на этой рабочей станции.
5. В обозревателе сервера отобразится список существующих кластеров HDInsight. Если у вас нет все кластеры, можно создать с помощью hello портал Azure, Azure PowerShell или hello HDInsight SDK. Дополнительные сведения см. в статье [Создание кластеров Hadoop в HDInsight](hdinsight-hadoop-provision-linux-clusters.md).
   
   ![Список кластеров в обозревателе сервера для средств Data Lake для Visual Studio](./media/hdinsight-hadoop-visual-studio-tools-get-started/hdinsight.visual.studio.tools.server.explorer.png "Средства Data Lake для обозревателя серверов в Visual Studio")
6. Разверните кластер HDInsight. Отобразятся **базы данных Hive**, учетная запись хранения по умолчанию, связанные учетные записи хранения и **журнал службы Hadoop**. Далее можно развернуть hello сущностей.

После подключения tooyour подписки Azure, вы будете иметь следующие возможности toodo hello:

**tooconnect toohello портал Azure из Visual Studio**

* В обозревателе сервера разверните **Azure** > **HDInsight**, щелкните правой кнопкой мыши кластер HDInsight и выберите **Manage Cluster in Azure portal** (Управление кластером на портале Azure).

**tooask вопросы и предоставления отзывов в Visual Studio**

* Из hello **средства** меню, нажмите кнопку **HDInsight**, а затем нажмите кнопку **форум MSDN** tooask вопросы, или нажмите кнопку **отправить отзыв**.

## <a name="navigate-hello-linked-resources"></a>Перейдите hello связанные ресурсы
Из обозревателя серверов вы увидите учетной записи хранения по умолчанию hello и связанное хранение учетных записей. При разворачивании учетной записи хранения по умолчанию hello, вы увидите контейнеры hello в учетной записи хранения hello. Учетная запись хранения по умолчанию Hello и контейнер по умолчанию hello помечены. Вы можете щелкнуть правой кнопкой любой hello контейнеры tooview hello содержимое.

![Список связанных ресурсов в обозревателе серверов для средств Data Lake для Visual Studio](./media/hdinsight-hadoop-visual-studio-tools-get-started/hdinsight.visual.studio.tools.linked.resources.png "Список связанных ресурсов")

После открытия контейнера, можно использовать следующие кнопки tooupload, delete и загрузки больших двоичных объектов hello:

![Операции с большими двоичными объектами в обозревателе серверов для средств Data Lake для Visual Studio](./media/hdinsight-hadoop-visual-studio-tools-get-started/hdinsight.visual.studio.tools.blob.operations.png "Передача, удаление и скачивание больших двоичных объектов")

## <a name="run-a-hive-query"></a>Выполнение запроса Hive
[Apache Hive](http://hive.apache.org) — это инфраструктура хранилища данных, созданная на основе Hadoop и обеспечивающая формирование сводных данных, запросов и анализа. Инструменты Data Lake для Visual Studio поддерживают выполнение запросов Hive из Visual Studio. Дополнительные сведения о Hive см. в статье [Использование Hive и HiveQL с Hadoop в HDInsight](hdinsight-use-hive.md).

Это скрипт Hive tootest много времени для кластера HDInsight. Оно может длиться несколько минут или более. Средства Озера данных для Visual Studio способен проверять скрипт Hive локально без подключения tooa динамической кластера.

Средства Озера данных для Visual Studio также позволяет пользователям toosee что находится внутри задания Hive hello путем сбора и распределение результатов журналы YARN hello определенных заданий Hive.

### <a name="view-hello-hivesampletable"></a>Представление hello **hivesampletable**
Все кластеры HDInsight поставляются с примером таблицы Hive, которая называется *hivesampletable*. Мы будем использовать этот tooshow таблицы как таблицы Hive toolist, просмотрите hello схемы таблицы, а также список строк hello в hello Hive таблицы.

**toolist Hive таблицы и представления схемы таблицы Hive**

1. Из **обозревателя серверов**, разверните **Azure** > **HDInsight** > hello кластера по своему усмотрению > **баз данных Hive**  >  **По умолчанию** > **hivesampletable** toosee hello таблицу схемы.
2. Щелкните правой кнопкой мыши **hivesampletable**, а затем нажмите кнопку **представление первые 100 строк** toolist hello строк. Это эквивалент toorunning hello после запроса Hive, с помощью драйвера Hive ODBC:
   
     SELECT * FROM hivesampletable LIMIT 100
   
   Вы можете настроить количество строк hello.
   
   ![Средства Data Lake. Запрос схемы Hive в HDInsight для Visual Studio](./media/hdinsight-hadoop-visual-studio-tools-get-started/hdinsight.visual.studio.tools.hive.schema.png "Результаты запроса Hive")

### <a name="create-hive-tables"></a>Создание таблиц Hive
Можно использовать toocreate графического интерфейса пользователя hello таблицу Hive или использование запросов Hive. Дополнительные сведения об использовании запросов Hive см. в разделе [Выполнение запросов Hive](#run.queries).

**toocreate таблицу Hive**

1. В **обозревателе сервера** разверните **Azure** > **Кластеры HDInsight** > кластер HDInsight > **Базы данных Hive**, щелкните правой кнопкой мыши **По умолчанию** и выберите **Создать таблицу**.
2. Настройте таблицу hello.
3. Нажмите кнопку **Create Table** toosubmit hello toocreate hello новый куст таблицу заданий.
   
    ![Средства Data Lake. Создание таблицы Hive с помощью средств HDInsight для Visual Studio](./media/hdinsight-hadoop-visual-studio-tools-get-started/hdinsight.visual.studio.tools.create.hive.table.png "Создание таблицы Hive")

### <a name="run.queries"></a>Проверка и выполнение запросов Hive
Существует два способа toocreate и выполнения запросов Hive.

* Создание ad-hoc-запросов
* Создание приложения Hive

**toocreate, проверка и выполнение нерегламентированных запросов**

1. В **обозревателе сервера** разверните **Azure**, а затем — **Кластеры HDInsight**.
2. Щелкните правой кнопкой мыши hello кластера, где требуется toorun hello запрос и нажмите кнопку **написать запрос Hive**.
3. Введите запросов Hive hello. Редактор куста hello уведомление поддерживает технологию IntelliSense. Средства Visual Studio поддерживает загрузку Озера данных hello удаленных метаданных во время редактирования скрипта Hive. Например при вводе «SELECT * FROM», hello, IntelliSense выводит списки всех hello предложенные таблицы имен. Если указано имя таблицы, имена столбцов hello перечислены hello IntelliSense. средства Hello поддерживает почти все инструкции Hive DML, вложенные запросы и определяемые пользователем встроенные функции hello.
   
    ![Средства Data Lake. IntelliSense в средствах HDInsight для Visual Studio](./media/hdinsight-hadoop-visual-studio-tools-get-started/hdinsight.visual.studio.tools.intellisense.table.names.png "U-SQL IntelliSense")
   
    ![Средства Data Lake. IntelliSense в средствах HDInsight для Visual Studio](./media/hdinsight-hadoop-visual-studio-tools-get-started/hdinsight.visual.studio.tools.intellisense.column.names.png "U-SQL IntelliSense")
   
   > [!NOTE]
   > Предлагаются только hello метаданные hello кластеров, выбранного в панели инструментов HDInsight.
   > 
   > 
4. (Необязательно): щелкните **скрипт проверки** toocheck hello скрипт синтаксических ошибок.
   
    ![Средства Data Lake. Локальная проверка в средствах Data Lake для Visual Studio](./media/hdinsight-hadoop-visual-studio-tools-get-started/hdinsight.visual.studio.tools.validate.hive.script.png "Проверка сценария")
5. Просто щелкните **Отправить** или выполните **расширенную отправку**. С hello расширенный параметр отправки, следует настроить **имя задания**, **аргументы**, **дополнительных конфигураций**, и **состояние каталога**hello сценария:
   
    ![Запрос Hadoop Hive в HDInsight](./media/hdinsight-hadoop-visual-studio-tools-get-started/hdinsight.visual.studio.tools.submit.jobs.advanced.png "Отправка запросов")
   
    После отправки задания hello разделе **Hive Сводка заданий** окна.
   
    ![Сводка запроса Hadoop Hive в HDInsight](./media/hdinsight-hadoop-visual-studio-tools-get-started/hdinsight.visual.studio.tools.run.hive.job.summary.png "Сводка по заданию Hive")
6. Используйте hello **обновление** кнопку tooupdate hello состояние до изменения состояния задания hello слишком**завершено**.
7. Hello перейти по ссылке ниже hello toosee нижней hello: **запроса задания**, **выходные данные задания**, **журнала задания**, или **Yarn журнала**.

**toocreate и выполнения решения Hive**

1. Из hello **ФАЙЛ** меню, нажмите кнопку **New**, а затем нажмите кнопку **проекта**.
2. Выберите **HDInsight** hello левой панели выберите **Hive приложения** hello средней панели введите свойства hello и нажмите кнопку **ОК**.
   
    ![Средства Data Lake. Создание проекта Hive с помощью средств HDInsight для Visual Studio](./media/hdinsight-hadoop-visual-studio-tools-get-started/hdinsight.visual.studio.tools.new.hive.project.png "Создание приложений Hive с помощью Visual Studio")
3. Из **обозревателе решений**, дважды щелкните **Script.hql** tooopen его.
4. скрипт Hive toovalidate hello, можно щелкнуть hello **скрипт проверки** кнопки, или щелкните правой кнопкой мыши hello скрипт в редакторе hello Hive и нажмите кнопку **скрипт проверки** hello контекстном меню.

### <a name="view-hive-jobs"></a>Просмотр заданий Hive
Для заданий Hive можно просмотреть запросы задания, выходные данные задания, журнал задания и журналы YARN. Дополнительные сведения см. в разделе предыдущего снимка экрана приветствия.

Hello самой последней версии средств hello позволяет toosee, что находится внутри заданиям Hive путем сбора и распределение результатов YARN журналы. Журнал YARN может помочь исследовать проблемы производительности. Дополнительные сведения о том, как HDInsight собирает журналы YARN, см. в статье [Доступ к журналам приложений YARN в HDInsight под управлением Windows](hdinsight-hadoop-access-yarn-app-logs.md).

**задания Hive tooview**

1. В **обозревателе сервера** разверните **Azure**, а затем — **HDInsight**.
2. Щелкните кластер HDInsight правой кнопкой мыши, а затем выберите пункт **Отобразить задания**. Вы увидите список hello Hive задания, работающие в кластере hello.
3. Выберите задание в список tooselect hello задания его, а затем используйте hello **Hive Сводка заданий** tooopen окна **запроса задания**, **выходные данные задания**, **журнала задания**, или **Yarn журнала**.
   
    ![Средства Data Lake. Просмотр заданий Hive с помощью средств HDInsight для Visual Studio](./media/hdinsight-hadoop-visual-studio-tools-get-started/hdinsight.visual.studio.tools.view.hive.jobs.png "Просмотр заданий Hive")

### <a name="faster-path-hive-execution-via-hiveserver2"></a>Быстрый путь выполнения Hive с помощью HiveServer2
> [!NOTE]
> Эта функция работает только с кластером HDInsight 3.2 и более поздних версий.
> 
> 

использовать средства Озера данных Hello задания Hive toosubmit через [WebHCat](https://cwiki.apache.org/confluence/display/Hive/WebHCat) (также известный как Templeton). Потребовалось сведений о задании tooreturn много времени и сведения об ошибках.
В порядке toosolve этой проблемы производительности hello, когда выполняется средствами Озера данных Hive задания непосредственно в кластере hello через HiveServer2, чтобы он пропускает RDP/SSH.
Производительность toobetter сложения пользователей можно также просмотреть Hive в диаграммах Tez и hello сведения о задаче.

При использовании кластера HDInsight 3.2 или более поздней версии будет отображена кнопка **Execute via HiveServer2** (Выполнить через HiveServer2):

![Средства Data Lake для Visual Studio, выполнение через HiveServer2](./media/hdinsight-hadoop-visual-studio-tools-get-started/hdinsight.visual.studio.tools.execute.via.hiveserver2.png "Выполнение запросов Hive с помощью HiveServer2")

Можно и см. в журналах hello потоковой передачи обратно в режиме реального времени при выполнении запроса Hive hello в Tez. в разделе hello задания диаграмм.

![Средства Data Lake для Visual Studio, быстрый путь выполнения Hive](./media/hdinsight-hadoop-visual-studio-tools-get-started/hdinsight.fast.path.hive.execution.png "Просмотр графики заданий")

**Разница между выполнением запросов через HiveServer2 и отправкой запросов через WebHCat**

Выполнение запросов через HiveServer2 имеет множество преимуществ в отношении производительности, однако есть и ряд ограничений. Некоторые ограничения hello не подходит для использования в рабочей среде. Hello следующей таблице показаны различия hello.

|  | Выполнение через HiveServer2 | Отправка через WebHCat |
| --- | --- | --- |
| Выполнение запросов |Исключает такие издержки hello в WebHCat (которая запускает задание MapReduce с именем «TempletonControllerJob»). |Так как запрос выполняется через WebHCat, WebHCat запускает задание MapReduce, что вызывает дополнительную задержку. |
| Потоковая передача журналов |Практически в режиме реального времени. |журналы выполнения задания Hello доступны только по завершении задания hello. |
| Просмотр журнала заданий |Если запрос выполняется через HiveServer2, его журнал заданий (выходные данные заданий) не сохраняется. приложение Hello можно просмотреть в пользовательском Интерфейсе YARN с ограниченные сведения. |Если запрос выполняется через WebHCat, его журнал заданий (выходные данные задания) сохраняется. Его можно просматривать с помощью Visual Studio, SDK HDInsight или PowerShell. |
| Закрытие окна |Выполнение через HiveServer2 является «синхронный» способом, поэтому должен поддерживать Привет открыть windows; Если hello windows закрыты hello выполнения запроса будет отменено. |Отправка через WebHCat способ «асинхронной», можно отправить запрос hello через WebHCat и закрыть Visual Studio. Можно вернуться и просмотреть результаты hello в любое время. |

### <a name="tez-hive-job-performance-graph"></a>Диаграмма выполнения задания Tez Hive
Поддержка средств Озера данных Hello, отображение диаграмм производительности для hello задания Hive выполнялись подсистемой выполнения Tez hello. Сведения о том, как включить Tez, см. в статье [Использование Hive и HiveQL с Hadoop в HDInsight](hdinsight-use-hive.md). После отправки задания в Visual Studio, Visual Studio показывает куст hello graph при завершении задания hello.  Может потребоваться tooclick hello **обновление** кнопку tooget hello последнее состояние задания.

> [!NOTE]
> Эта функция доступна для кластеров HDInsight начиная с версии 3.2.4.593. Она работает только для выполненных заданий (если задание отправлено через WebHCat). Показанная ниже диаграмма будет отображаться, если запрос выполняется через HiveServer2. Она работает для кластеров под управлением Windows и Linux.
> 
> 

![Диаграмма производительности Tez для Hadoop Hive](./media/hdinsight-hadoop-visual-studio-tools-get-started/hdinsight.hive.tez.performance.graph.png "Состояние задания")

запрос лучше понять ваш куст toohelp, средства hello добавить представление оператора, куст hello в этом выпуске. Необходимо просто toodouble, щелкните вершины hello схемы заданий hello и вы увидите все операторы hello внутри hello вершин. Также можно навести на tooview конкретный оператор подробности данного оператора.

### <a name="task-execution-view-for-hive-on-tez-jobs"></a>Представление выполнения задачи для заданий Hive в Tez
Здравствуйте представление выполнения задачи для куста Tez заданий можно использовать tooget структурирования и отображения сведений о заданиях, Hive и получить дополнительные сведения о задании. При наличии проблем с производительностью, можно использовать hello представление tooget подробные сведения. Например, как каждая задача работает hello подробное описание и сведения о каждой задаче (чтение/запись данных, расписание и начальное и конечное время, т. д.), чтобы вы можете настроить задание конфигурации или архитектуры системы на основе сведений hello визуализируются в.

![Средства Data Lake для Visual Studio, представление выполнения заданий](./media/hdinsight-hadoop-visual-studio-tools-get-started/hdinsight.visual.studio.tools.task.execution.view.png "Представление выполнения заданий")

## <a name="run-pig-scripts"></a>Запуск сценариев Pig
Средства Озера данных для Visual Studio поддерживает создание и отправка кластеров tooHDInsight скрипты Pig. Пользователей можно создать проект Pig из шаблона и отправьте hello сценария tooHDInsight кластеров.

## <a name="feedbacks--known-issues"></a>Отзывы и известные проблемы
* Сейчас результаты HiveServer2 отображаются как обычный текст, что не совсем удобно. Мы работаем над решением этой проблемы.
* Если результаты hello запускаются со значениями NULL, в настоящее время hello результаты не отображаются. Мы устранили эту проблему и если блокируются на эту проблему, вы бесплатно toodrop нам электронной почты или обратитесь в службу поддержки.
* в зависимости от настройки локального региона пользователя кодируется Hello HQL сценарий, созданные с помощью Visual Studio. Он может неправильно выполнять при отправке toocluster сценария hello в двоичном виде.

## <a name="next-steps"></a>Дальнейшие действия
В этой статье вы узнали, как tooconnect tooHDInsight кластеры из Visual Studio, с помощью hello Озера данных (HDInsight) пакета средств и как toorun запрос Hive. Дополнительные сведения можно найти в разделе 

* [Использование Hive и HiveQL с Hadoop в HDInsight](hdinsight-use-hive.md)
* [Руководство по Hadoop. Приступая к работе с Hadoop в HDInsight](hdinsight-hadoop-linux-tutorial-get-started.md)
* [Отправка заданий Hadoop в HDInsight](hdinsight-submit-hadoop-jobs-programmatically.md)
* [Анализ данных Twitter с помощью Hive в HDInsight](hdinsight-analyze-twitter-data.md)

