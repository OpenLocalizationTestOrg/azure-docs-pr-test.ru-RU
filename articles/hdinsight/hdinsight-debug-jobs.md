---
title: "Отладка Hadoop в среде HDInsight: просмотр журналов и интерпретация сообщений об ошибках — Azure | Документы Майкрософт"
description: "Дополнительные сведения о hello сообщений об ошибках, может появиться при администрировании HDInsight с помощью PowerShell, а также действия, которые можно выполнить toorecover."
services: hdinsight
tags: azure-portal
editor: cgronlun
manager: jhubbard
author: mumian
documentationcenter: 
ms.assetid: 7e6ceb0e-8be8-4911-bc80-20714030a3ad
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/06/2017
ms.author: jgao
ms.openlocfilehash: 2f12a40e9dcac32ce2e11d66d60d8b3b212ecb53
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="analyze-hdinsight-logs"></a>Анализ журналов HDInsight
Каждый кластер Hadoop в Azure HDInsight имеет учетную запись хранения Azure, используется в качестве файловой системы по умолчанию hello. Учетная запись хранения Hello называется учетной записи хранения по умолчанию hello. Кластер использует hello хранилище таблиц Azure и hello хранилища BLOB-объектов на toostore учетной записи хранения по умолчанию hello журналов.  toofind hello учетной записи хранения по умолчанию для кластера, в разделе [кластеров управление Hadoop в HDInsight](hdinsight-administer-use-management-portal.md#find-the-default-storage-account). журналы Hello сохраняют в hello учетной записи хранилища даже после удаления кластера hello.

## <a name="logs-written-tooazure-tables"></a>Журналы записываются tooAzure таблиц
Hello журналы записываются tooAzure таблицы обеспечивают один уровень понять, что происходит с кластера HDInsight.

При создании кластера HDInsight, 6 они автоматически создаются для кластеров под управлением Linux в хранилище таблиц по умолчанию hello:

* hdinsightagentlog
* syslog
* daemonlog
* hadoopservicelog
* ambariserverlog
* ambariagentlog

Для кластеров под управлением Windows создается 3 таблицы:

* setuplog: журнал событий и исключений, произошедших во время подготовки и настройки кластеров HDInsight.
* hadoopinstalllog: журнал событий и исключений при установке Hadoop кластере hello. В этой таблице могут оказаться полезными при отладке проблем связанных tooclusters, созданных с помощью настраиваемых параметров.
* hadoopservicelog: журнал событий и исключений, записанных всеми службами Hadoop. Эта таблица может быть полезно при отладке проблем связанных toojob сбоев в кластерах HDInsight.

имена файлов таблицы Hello **u<ClusterName>DDMonYYYYatHHMMSSsss<TableName>**.

Эти таблицы содержит hello следующие поля:

* ClusterDnsName
* ComponentName
* EventTimestamp
* Узел
* MALoggingHash
* Сообщение
* Нет
* PreciseTimeStamp
* Роль
* RowIndex
* Клиент
* TIMESTAMP
* TraceLevel

### <a name="tools-for-accessing-hello-logs"></a>Средства для доступе к журналам hello
Существует множество средств для доступа к данным в этих таблицах:

* Visual Studio
* Обозреватель хранилищ Azure
* Power Query для Excel

#### <a name="use-power-query-for-excel"></a>Использование Power Query для Excel
Power Query можно установить, зайдя на страницу [www.microsoft.com/en-us/download/details.aspx?id=39379](http://www.microsoft.com/en-us/download/details.aspx?id=39379). Страница загрузки для требования к системе для hello hello в разделе

**tooopen toouse Power Query и анализ журналов службы hello**

1. Откройте **Microsoft Excel**.
2. Из hello **Power Query** меню, нажмите кнопку **из Azure**, а затем нажмите кнопку **хранилище из таблиц Microsoft Azure**.
   
    ![Хранилище таблиц Azure для кластера HDInsight Hadoop, открытое в PowerQuery для Excel](./media/hdinsight-debug-jobs/hdinsight-hadoop-analyze-logs-using-excel-power-query-open.png)
3. Введите имя учетной записи хранения hello. Это может быть hello короткое имя или полное доменное имя hello.
4. Введите ключ учетной записи хранения hello. Вы должны увидеть список таблиц:
   
    ![Журналы HDInsight Hadoop, которые хранятся в хранилище таблиц Azure](./media/hdinsight-debug-jobs/hdinsight-hadoop-analyze-logs-table-names.png)
5. Щелкните правой кнопкой мыши таблицу hadoopservicelog hello в hello **Навигатор** области и выберите команду **изменить**. Вы увидите 4 столбца. При необходимости удалить hello **ключ раздела**, **ключ строки**, и **Timestamp** столбцы, выделив их и выбрав **удалить столбцы** Параметры hello на ленте «hello».
6. Нажмите кнопку hello разверните значок на hello содержимого столбца toochoose hello столбцы tooimport в электронную таблицу Excel hello. Для этого примера я выбрал столбцы TraceLevel и ComponentName: они дадут мне базовую информацию о том, на каких компонентах возникли проблемы.
   
    ![Выбор столбцов для журналов HDInsight Hadoop](./media/hdinsight-debug-jobs/hdinsight-hadoop-analyze-logs-using-excel-power-query-filter.png)
7. Нажмите кнопку **ОК** tooimport hello данных.
8. Выберите hello **TraceLevel**, роли, и **ComponentName** столбцы, а затем щелкните **Group By** управления на ленте «hello».
9. Нажмите кнопку **ОК** в hello Group By диалоговое окно
10. Щелкните **Применить и закрыть**.

Теперь можно использовать Excel toofilter и сортировки, при необходимости. Очевидно, что вы можете tooinclude других столбцов (например, сообщение) в порядке toodrill вниз в проблемы они возникают, когда выбора и группировки столбцов hello, описанных выше предоставляет довольно изображение, что происходит со службами Hadoop. Hello же идеи может быть применен toohello setuplog и hadoopinstalllog таблицы.

#### <a name="use-visual-studio"></a>Использование Visual Studio
**toouse Visual Studio**

1. Откройте Visual Studio.
2. Из hello **представление** меню, нажмите кнопку **Cloud Explorer**. Или просто нажмите **CTRL+\,, CTRL+X**.
3. В **Cloud Explorer** выберите **Типы ресурсов**.  Hello других доступный параметр — **групп ресурсов**.
4. Разверните **учетные записи хранения**, hello учетной записи хранения по умолчанию для кластера, а затем **таблиц**.
5. Дважды щелкните **hadoopservicelog**.
6. Добавьте фильтр. Например:
   
        TraceLevel eq 'ERROR'
   
    ![Выбор столбцов для журналов HDInsight Hadoop](./media/hdinsight-debug-jobs/hdinsight-hadoop-analyze-logs-visual-studio-filter.png)
   
    Дополнительные сведения о создании фильтров см. в разделе [создания фильтра строк для hello конструктор таблиц](../vs-azure-tools-table-designer-construct-filter-strings.md).

## <a name="logs-written-tooazure-blob-storage"></a>Регистрирует tooAzure создано хранилище больших двоичных объектов
[Hello журналы таблиц письменного tooAzure](#log-written-to-azure-tables) обеспечивают один уровень понять, что происходит с кластера HDInsight. Тем не менее, эти таблицы не предоставляют журналов уровня задачи, которые могут оказаться полезными при более глубокой детализации возникших проблем. tooprovide этот следующий уровень детализации, HDInsight, кластеры, настроить toowrite журналы задач tooyour учетной записи хранилища больших двоичных объектов для всех заданий, переданных через Templeton. На практике это означает задания отправки с помощью командлетов Microsoft Azure PowerShell hello или hello задания отправки API-интерфейсы .NET, не задания, переданных через RDP/командной-строки toohello кластера доступа. 

см. журналы hello tooview, [журналы приложений YARN доступа на основе Linux HDInsight](hdinsight-hadoop-access-yarn-app-logs-linux.md).

Дополнительные сведения о журналах приложений см. в статье [Simplifying user-logs management and access in YARN](http://hortonworks.com/blog/simplifying-user-logs-management-and-access-in-yarn/) (Упрощенное управление журналами пользователей и доступ в YARN).

## <a name="view-cluster-health-and-job-logs"></a>Просмотр журналов заданий и сведений о работоспособности кластеров
### <a name="access-hadoop-ui"></a>Доступ к пользовательскому интерфейсу Hadoop
Выберите hello портал Azure, HDInsight кластер имя tooopen hello кластера колонки. Из колонки hello кластера, нажмите кнопку **мониторинга**.

![Запуск панели мониторинга кластера](./media/hdinsight-debug-jobs/hdi-debug-launch-dashboard.png)

При появлении запроса введите учетные данные администратора кластера hello. В hello консоль запроса, откроется, щелкните **Hadoop пользовательского интерфейса**.

![Запуск пользовательского интерфейса Hadoop](./media/hdinsight-debug-jobs/hdi-debug-launch-dashboard-hadoop-ui.png)

### <a name="access-hello-yarn-ui"></a>Доступ к hello Yarn пользовательского интерфейса
Выберите hello портал Azure, HDInsight кластер имя tooopen hello кластера колонки. Из колонки hello кластера, нажмите кнопку **мониторинга**. При появлении запроса введите учетные данные администратора кластера hello. В hello консоль запроса, откроется, щелкните **YARN пользовательского интерфейса**.

Можно использовать следующие hello toodo пользовательского интерфейса YARN hello.

* **Получение сведений о состоянии кластера.** Hello левой панели разверните **кластера**и нажмите кнопку **о**. Это отсутствует кластера сведения о состоянии как всего выделено памяти, ядер, используемых, состояние hello диспетчер ресурсов кластера, кластер версии и т. д.
  
    ![Запуск панели мониторинга кластера](./media/hdinsight-debug-jobs/hdi-debug-yarn-cluster-state.png)
* **Получение сведений о состоянии узла.** Hello левой панели разверните **кластера**и нажмите кнопку **узлы**. Перечисляет все узлы hello hello кластером, HTTP-адрес каждого узла, узел tooeach выделенных ресурсов, и т. д.
* **Отслеживание состояния задания.** Hello левой панели разверните **кластера**, а затем нажмите кнопку **приложений** toolist все hello заданий в кластере hello. Если требуется, чтобы toolook заданий в определенном состоянии (например, новый, отправленной, запуска, т. д.), щелкните hello соответствующую ссылку в разделе **приложений**. Дополнительно можно щелкнуть hello toofind имя задания дополнительных сведений о задании hello такие, включая hello выходных данных, журналы и т. д.

### <a name="access-hello-hbase-ui"></a>Доступ к hello HBase пользовательского интерфейса
Выберите hello портал Azure, HDInsight HBase кластера имя tooopen hello кластера колонки. Из колонки hello кластера, нажмите кнопку **мониторинга**. При появлении запроса введите учетные данные администратора кластера hello. В hello консоль запроса, откроется, щелкните **HBase пользовательского интерфейса**.

## <a name="hdinsight-error-codes"></a>Коды ошибок HDInsight
Hello сообщения об ошибках перечислено в этом разделе предоставляются пользователям hello toohelp Hadoop в Azure HDInsight понимания возможных ошибок, возникающих при администрировании службы hello, с помощью Azure PowerShell и tooadvise их на шаги hello который может быть получено toorecover ошибки hello.

Некоторые из этих сообщений об ошибке может также просмотреть в hello портал Azure при используется toomanage кластеров HDInsight. Однако другие сообщения об ошибках могут возникнуть существует менее детализированную из-за ограничений toohello hello предпринять действия в этом контексте невозможно. Другие сообщения об ошибках приведены в hello контекстах, где очевидна hello устранение рисков. 

### <a id="AtleastOneSqlMetastoreMustBeProvided"></a>AtleastOneSqlMetastoreMustBeProvided
* **Описание**: укажите сведения о базе данных Azure SQL для по крайней мере один компонент в порядке toouse настраиваемые параметры для метахранилищ Hive и Oozie, укажите.
* **Устранение рисков**: hello пользователь должен toosupply допустимым SQL Azure метахранилище и повторите попытку hello запросом.  

### <a id="AzureRegionNotSupported"></a>AzureRegionNotSupported
* **Описание.** Не удалось создать кластер в регионе *имя_вашего_региона*. Выберите допустимую область HDInsight и повторите запрос.
* **Устранение рисков**: клиента следует создать область hello кластера, которая в настоящее время поддерживает их: Юго-Восточная Азия, Западная Европа, Северная Европа, восток США или Запад США.  

### <a id="ClusterContainerRecordNotFound"></a>ClusterContainerRecordNotFound
* **Описание**: hello server не удалось найти запись кластера запрошенный hello.  
* **Устранение рисков**: повторите операцию hello.

### <a id="ClusterDnsNameInvalidReservedWord"></a>ClusterDnsNameInvalidReservedWord
* **Описание.** Недопустимое DNS-имя кластера *ваше_DNS_имя*. Убедитесь, что имя начинается и оканчивается цифрой или буквой и не содержит специальных символов отличных от "-"  
* **Устранение рисков**: Убедитесь, что используется допустимое имя DNS для кластера, который начинается и заканчивается буквенно-цифровые и содержит специальные символы, отличные от тире hello "-", а затем повторите операцию hello.

### <a id="ClusterNameUnavailable"></a>ClusterNameUnavailable
* **Описание.** Недоступное имя кластера *имя_вашего_кластера*. Выберите другое имя.  
* **Устранение рисков**: hello пользователя следует указать имя_кластера, которое является уникальным и не существует и повторите. Если пользователь hello использует hello портала, приветствия пользовательского интерфейса будет уведомлять их Если имя кластера уже используется во время hello Создание шагов.

### <a id="ClusterPasswordInvalid"></a>ClusterPasswordInvalid
* **Описание.** Недопустимый пароль кластера. Пароль должен быть по крайней мере 10 символов и должен содержать хотя бы одну цифру, прописные буквы, строчные буквы и специальный символ без пробелов и не должно содержать hello пользователя как часть.  
* **Устранение рисков**: Укажите допустимый кластера пароль и повторите операцию hello.

### <a id="ClusterUserNameInvalid"></a>ClusterUserNameInvalid
* **Описание.** Недопустимое имя пользователя для кластера. Убедитесь, что имя пользователя не содержит специальных символов или пробелов.  
* **Устранение рисков**: Введите имя пользователя действительным кластером и повторите операцию hello.

### <a id="ClusterUserNameInvalidReservedWord"></a>ClusterUserNameInvalidReservedWord
* **Описание.** Недопустимое DNS-имя кластера *ваше_DNS_имя_кластера*. Убедитесь, что имя начинается и оканчивается цифрой или буквой и не содержит специальных символов отличных от "-"  
* **Устранение рисков**: Укажите допустимое имя пользователя кластера DNS и повторите операцию hello.

### <a id="ContainerNameMisMatchWithDnsName"></a>ContainerNameMisMatchWithDnsName
* **Описание**: имя контейнера в URI *yourcontainerURI* и DNS-имя *yourDnsName* в запросе текст должен быть hello таким же.  
* **Устранение рисков**: Убедитесь, что имя контейнера и имя DNS являются одинаковыми hello и повторите операцию hello.

### <a id="DataNodeDefinitionNotFound"></a>DataNodeDefinitionNotFound
* **Описание.** Недопустимая конфигурация кластера. Не удается toofind определений узел данных в размер узла.  
* **Устранение рисков**: повторите операцию hello.

### <a id="DeploymentDeletionFailure"></a>DeploymentDeletionFailure
* **Описание**: не удалось выполнить удаление развертывания hello кластера  
* **Устранение рисков**: повторите операцию удаления hello.

### <a id="DnsMappingNotFound"></a>DnsMappingNotFound
* **Описание.** Ошибка конфигурации службы. Не удалось найти требуемые сведения о сопоставлении DNS.  
* **Устранение.** Удалите кластер и создайте новый.

### <a id="DuplicateClusterContainerRequest"></a>DuplicateClusterContainerRequest
* **Описание.** Попытка создать повторяющийся контейнер кластера. Для контейнера *имя_вашего_контейнера* существует запись, но теги eTag не совпадают.
* **Устранение рисков**: Укажите уникальное имя для контейнера hello и hello повтора операции создания.

### <a id="DuplicateClusterInHostedService"></a>DuplicateClusterInHostedService
* **Описание.** Размещенная служба *имя_вашей_размещенной_службы* уже содержит кластер. Размещенная служба не может содержать несколько кластеров.  
* **Устранение рисков**: hello кластера узлов в другой размещенной службы.

### <a id="FailureToUpdateDeploymentStatus"></a>FailureToUpdateDeploymentStatus
* **Описание**: hello server не удалось обновить состояние развертывания кластера hello hello.  
* **Устранение рисков**: повторите операцию hello. Если ошибка повторится несколько раз, обратитесь в службу поддержки.

### <a id="HdiRestoreClusterAltered"></a>HdiRestoreClusterAltered
* **Описание.** Кластер *имя_вашего_кластера* удален в процессе обслуживания. Создайте кластер hello.
* **Устранение рисков**: повторно создайте hello кластера.

### <a id="HeadNodeConfigNotFound"></a>HeadNodeConfigNotFound
* **Описание.** Недопустимая конфигурация кластера. Требуемые настройки головного узла не найдены в размерах узлов.
* **Устранение рисков**: повторите операцию hello.

### <a id="HostedServiceCreationFailure"></a>HostedServiceCreationFailure
* **Описание**: не удается toocreate размещенной службы *nameOfYourHostedService*. Повторите запрос.  
* **Устранение рисков**: hello повторите попытку.

### <a id="HostedServiceHasProductionDeployment"></a>HostedServiceHasProductionDeployment
* **Описание.** Размещенная служба *имя_вашей_размещенной_службы* уже содержит рабочее развертывание. Размещенная служба не может содержать несколько рабочих развертываний. Повторите запрос hello в другое имя кластера.
* **Устранение рисков**: используйте другое имя кластера и повторите запрос hello.

### <a id="HostedServiceNotFound"></a>HostedServiceNotFound
* **Описание**: службы, размещенной в *nameOfYourHostedService* для hello кластера не найден.  
* **Устранение рисков**: Если hello кластер находится в состоянии ошибки, удалите его, а затем повторите попытку.

### <a id="HostedServiceWithNoDeployment"></a>HostedServiceWithNoDeployment
* **Описание.** Размещенная служба *имя_вашей_размещенной_службы* не имеет связанного развертывания.  
* **Устранение рисков**: Если hello кластер находится в состоянии ошибки, удалите его, а затем повторите попытку.

### <a id="InsufficientResourcesCores"></a>InsufficientResourcesCores
* **Описание**: hello SubscriptionId *yourSubscriptionId* имеет ядра кластера левой toocreate *yourClusterName*. Требуется: *resourcesRequired*. Доступно: *resourcesAvailable*.  
* **Устранение рисков**: высвобождения ресурсов в подписке или увеличить подписки toohello доступные ресурсы hello и повторите попытку toocreate hello кластера.

### <a id="InsufficientResourcesHostedServices"></a>InsufficientResourcesHostedServices
* **Описание**: идентификатор подписки *yourSubscriptionId* не имеет квоты для нового кластера toocreate HostedService *yourClusterName*.  
* **Устранение рисков**: высвобождения ресурсов в подписке или увеличить подписки toohello доступные ресурсы hello и повторите попытку toocreate hello кластера.

### <a id="InternalErrorRetryRequest"></a>InternalErrorRetryRequest
* **Описание**: Произошла внутренняя ошибка сервера hello. Повторите запрос.  
* **Устранение рисков**: hello повторите попытку.

### <a id="InvalidAzureStorageLocation"></a>InvalidAzureStorageLocation
* **Описание.** Недопустимое расположение хранилища Azure *имя_региона_данных*. Убедитесь, что область hello указано правильно и повторите запрос.
* **Устранение рисков**: выберите место хранения, которая поддерживает HDInsight, убедитесь, что кластер является совмещенной и повторите операцию hello.

### <a id="InvalidNodeSizeForDataNode"></a>InvalidNodeSizeForDataNode
* **Описание.** Недопустимый размер виртуальной машины для узлов данных. Для всех узлов данных поддерживается только размер "Большая ВМ".  
* **Устранение рисков**: укажите размер узла hello поддерживается для hello данных узла и повторите операцию hello.

### <a id="InvalidNodeSizeForHeadNode"></a>InvalidNodeSizeForHeadNode
* **Описание.** Недопустимый размер виртуальной машины для головного узла. Для головного узла поддерживается только размер "Виртуальная машина ExtraLarge".  
* **Устранение рисков**: укажите размер узла hello поддерживается hello головного узла и повторите операцию hello

### <a id="InvalidRightsForDeploymentDeletion"></a>InvalidRightsForDeploymentDeletion
* **Описание**: идентификатор подписки *yourSubscriptionId* используется не имеет достаточных разрешений tooexecute операция удаления кластера *yourClusterName*.  
* **Устранение рисков**: Если hello кластер находится в состоянии ошибки, удалите его, а затем повторите попытку.  

### <a id="InvalidStorageAccountBlobContainerName"></a>InvalidStorageAccountBlobContainerName
* **Описание.** Недопустимое имя контейнера двоичных объектов большого размера для внешней учетной записи хранения *имя_вашего_контейнера*. Убедитесь, что имя начинается с буквы и содержит только строчные буквы, цифры и дефис.  
* **Устранение рисков**: укажите имя контейнера BLOB-объектов учетной записи хранения и повторите операцию hello.

### <a id="InvalidStorageAccountConfigurationSecretKey"></a>InvalidStorageAccountConfigurationSecretKey
* **Описание**: конфигурация для учетной записи внешнего хранилища *yourStorageAccountName* , необходимые toohave секретного ключа сведения toobe набор.  
* **Устранение рисков**: Укажите допустимый секретный ключ для учетной записи хранилища hello и повторите операцию hello.

### <a id="InvalidVersionHeaderFormat"></a>InvalidVersionHeaderFormat
* **Описание.** Формат заголовка версии *ваш_заголовок_версии* отличается от допустимого формата гггг-мм-дд.  
* **Устранение рисков**: Укажите допустимый формат для заголовка версии hello и повторите запрос hello.

### <a id="MoreThanOneHeadNode"></a>MoreThanOneHeadNode
* **Описание.** Недопустимая конфигурация кластера. Обнаружена конфигурация с несколькими головными узлами.  
* **Устранение рисков**: изменение конфигурации hello, определяются только для одного головного узла.

### <a id="OperationTimedOutRetryRequest"></a>OperationTimedOutRetryRequest
* **Описание**: не удалось выполнить операцию hello в hello допускается времени или hello максимальное повторные попытки возможно. Повторите запрос.  
* **Устранение рисков**: hello повторите попытку.

### <a id="ParameterNullOrEmpty"></a>ParameterNullOrEmpty
* **Описание.** Параметр *имя_вашего_параметра* не может быть пустым или иметь значение null.  
* **Устранение рисков**: Укажите допустимое значение для параметра hello.

### <a id="PreClusterCreationValidationFailure"></a>PreClusterCreationValidationFailure
* **Описание**: один или несколько входных данных запроса для создания кластера hello не является допустимым. Убедитесь, что входные значения hello указаны правильно и повторите запрос.  
* **Устранение рисков**: Убедитесь, что входные значения hello указаны правильно и повторите запрос.

### <a id="RegionCapabilityNotAvailable"></a>RegionCapabilityNotAvailable
* **Описание.** Недоступна поддержка региона *имя_вашего_региона* и идентификатора подписки *ИД_вашей_подписки*.  
* **Устранение.** Укажите регион, который поддерживает кластеры HDInsight. Hello публично поддерживаемые регионы: Юго-Восточная Азия, Западная Европа, Северная Европа, восток США или Запад США.

### <a id="StorageAccountNotColocated"></a>StorageAccountNotColocated
* **Описание.** Учетная запись хранения *имя_вашей_учетной_записи_хранения* находится в регионе *имя_текущего_региона*. Должно быть то же, что область кластера hello *yourClusterRegionName*.  
* **Устранение рисков**: либо укажите учетную запись хранилища в hello же регионе, что кластер находится в, или если данные уже hello учетной записи хранилища, создание нового кластера в hello же регионе, что hello существующей учетной записи хранения. При использовании портала hello hello пользовательского интерфейса будет уведомлять об этой проблемы заранее.

### <a id="SubscriptionIdNotActive"></a>SubscriptionIdNotActive
* **Описание.** Указанный идентификатор подписки *ИД_вашей_подписки* неактивен.  
* **Устранение.** Повторно активируйте свою подписку или получите новую допустимую подписку.

### <a id="SubscriptionIdNotFound"></a>SubscriptionIdNotFound
* **Описание.** Не удалось найти идентификатор подписки *ИД_вашей_подписки*.  
* **Устранение рисков**: Проверьте, что идентификатор подписки является допустимым и повторите операцию hello.

### <a id="UnableToResolveDNS"></a>UnableToResolveDNS
* **Описание**: не удается tooresolve DNS *yourDnsUrl*. Проверьте hello полный URL-адрес для конечной точки большого двоичного объекта hello предоставляется.  
* **Устранение.** Укажите допустимый URL-адрес большого двоичного объекта. Привет, URL-адрес должен быть полностью допустимыми, включая начиная с *http://* и заканчиваются *.com*.

### <a id="UnableToVerifyLocationOfResource"></a>UnableToVerifyLocationOfResource
* **Описание**: не удается tooverify расположение ресурса *yourDnsUrl*. Проверьте hello полный URL-адрес для конечной точки большого двоичного объекта hello предоставляется.  
* **Устранение.** Укажите допустимый URL-адрес большого двоичного объекта. Привет, URL-адрес должен быть полностью допустимыми, включая начиная с *http://* и заканчиваются *.com*.

### <a id="VersionCapabilityNotAvailable"></a>VersionCapabilityNotAvailable
* **Описание.** Недоступна поддержка версии *указанная_версия* и идентификатора подписки *ИД_вашей_подписки*.  
* **Устранение рисков**: выберите версию, которая доступна и повторите операцию hello.

### <a id="VersionNotSupported"></a>VersionNotSupported
* **Описание.** Версия *указанная_версия* не поддерживается.
* **Устранение рисков**: выберите версию, которая поддерживается и повторите операцию hello.

### <a id="VersionNotSupportedInRegion"></a>VersionNotSupportedInRegion
* **Описание.** Версия *указанная_версия* недоступна в регионе Azure *указанный_регион*.  
* **Устранение рисков**: выберите версию, которая поддерживается в определенной области hello и повторите операцию hello.

### <a id="WasbAccountConfigNotFound"></a>WasbAccountConfigNotFound
* **Описание.** Недопустимая конфигурация кластера. Требуемая конфигурация учетной записи WASB не найдена во внешних учетных записях.  
* **Устранение рисков**: Убедитесь, что учетная запись hello существует и правильно ли указан в конфигурации и повторите попытку операции hello.

## <a name="next-steps"></a>Дальнейшие действия
* [Использование представления Ambari toodebug Tez заданий в HDInsight](hdinsight-debug-ambari-tez-view.md)
* [Включение дампов кучи для служб Hadoop в HDInsight под управлением Linux](hdinsight-hadoop-collect-debug-heap-dump-linux.md)
* [Управление кластерами HDInsight с помощью hello Ambari веб-интерфейса](hdinsight-hadoop-manage-ambari.md)

