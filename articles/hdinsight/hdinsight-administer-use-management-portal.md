---
title: "Здравствуйте, aaaManage кластеров Hadoop под управлением Windows в HDInsight с помощью портала Azure | Документы Microsoft"
description: "Узнайте, как tooadminister службы HDInsight. Создание кластера HDInsight, откройте hello интерактивной консоли JavaScript и Привет открыть Hadoop командной консоли."
services: hdinsight
documentationcenter: 
tags: azure-portal
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 9295a988-bd88-453a-8c8b-55fa103bf39c
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: jgao
ROBOTS: NOINDEX
ms.openlocfilehash: a237726b0e37a08005ce22e96581739e93edb050
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="manage-windows-based-hadoop-clusters-in-hdinsight-by-using-hello-azure-portal"></a>Управление с помощью портала Azure hello кластеров под управлением Windows Hadoop в HDInsight

С помощью hello [портал Azure][azure-portal], можно создавать кластеры Hadoop под управлением Windows в Azure HDInsight, измените пароль пользователя Hadoop и Включение протокола удаленного рабочего стола (RDP), чтобы вы могли использовать hello Hadoop командной консоли в кластере hello.

Hello сведения в этой статье применяется только на основе tooWindow кластеров HDInsight. Сведения об управлении кластерами под управлением Linux см. в разделе [кластеров управление Hadoop в HDInsight с помощью hello портал Azure](hdinsight-administer-use-portal-linux.md).

> [!IMPORTANT]
> Linux — hello только операционную систему, используемую в HDInsight версии 3.4 или более поздней. Дополнительные сведения см. в разделе [Приближается дата прекращения сопровождения HDI версии 3.3](hdinsight-component-versioning.md#hdinsight-windows-retirement).


## <a name="prerequisites"></a>Предварительные требования

Прежде чем приступать к этой статье, необходимо иметь следующие hello:

* **Подписка Azure**. Ознакомьтесь с [бесплатной пробной версией Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).
* **Учетная запись хранения Azure** -кластер HDInsight использует контейнер службы хранилища больших двоичных объектов Azure в качестве файловой системы по умолчанию hello. Дополнительные сведения о том, каким образом хранилище больших двоичных объектов Azure обеспечивает удобную работу с кластерами HDInsight, см. в статье [Использование хранилища BLOB-объектов Azure с HDInsight](hdinsight-hadoop-use-blob-storage.md). Дополнительные сведения о создании учетной записи хранилища Azure см. в разделе [как учетную запись хранения tooCreate](../storage/common/storage-create-storage-account.md).

## <a name="open-hello-portal"></a>Откройте портал hello
1. Войдите в слишком[https://portal.azure.com](https://portal.azure.com).
2. После открытия hello портала можно:

   * Нажмите кнопку **New** из toocreate меню слева hello нового кластера:

       ![Кнопка создания кластера HDInsight](./media/hdinsight-administer-use-management-portal/azure-portal-new-button.png)
   * Нажмите кнопку **кластеров HDInsight** из меню слева hello.

       ![Кнопка кластера HDInsight на портале Azure](./media/hdinsight-administer-use-management-portal/azure-portal-hdinsight-button.png)

     Если **HDInsight** не отображается в левом меню hello, щелкните **Обзор**.

     ![Кнопка обзора кластера на портале Azure](./media/hdinsight-administer-use-management-portal/azure-portal-browse-button.png)

## <a name="create-clusters"></a>Создание кластеров
Hello создания инструкции по использованию hello портала, см. [HDInsight, создания кластеров](hdinsight-hadoop-provision-linux-clusters.md).

HDInsight работает со множеством компонентов Hadoop. Список hello hello компонентов, которые были проверены и поддерживается, в разделе [версии Hadoop — в Azure HDInsight](hdinsight-component-versioning.md). HDInsight можно настроить с помощью одного из следующих вариантов hello:

* Используйте действие скрипта toorun пользовательские скрипты, можно настроить tooeither кластера изменения конфигурации кластера или установить пользовательские компоненты, такие как Giraph или Solr. Дополнительные сведения см. в статье [Настройка кластеров HDInsight под управлением Linux с помощью действия сценария](hdinsight-hadoop-customize-cluster.md).
* Используйте параметры настройки кластера hello в hello HDInsight .NET SDK или Azure PowerShell во время создания кластера. Изменений конфигурации, затем сохраняются через время существования hello hello кластера и не подвержены reimages узел кластера, которые периодически выполняет платформы Azure для обслуживания. Дополнительные сведения об использовании параметров настройки кластера hello см. в разделе [HDInsight, создания кластеров](hdinsight-hadoop-provision-linux-clusters.md).
* Некоторые компоненты собственного Java, например Mahout и каскадных, могут выполняться в кластере hello как JAR-файла. Эти файлы JAR может быть распределенное tooAzure хранилища больших двоичных объектов и передавать tooHDInsight кластеров с помощью механизмов отправки заданий Hadoop. Подробные сведения см. в статье [Отправка заданий Hadoop в HDInsight](hdinsight-submit-hadoop-jobs-programmatically.md).

  > [!NOTE]
  > При наличии проблем развертывание кластеров tooHDInsight файлы JAR или вызов JAR-файлов в кластерах HDInsight, обратитесь к [поддержки Майкрософт](https://azure.microsoft.com/support/options/).
  >
  > Компонент Cascading не поддерживается службой HDInsight и на него не распространяется техническая поддержка Майкрософт. Список поддерживаемых компонентов см [новые возможности, предоставляемые HDInsight версии кластера hello](hdinsight-component-versioning.md).
  >
  >

Установка программного обеспечения в кластере hello с помощью удаленного рабочего стола не поддерживается. Рекомендуется хранить все файлы на дисках hello hello головного узла, как они будут потеряны, если вам требуется toore-создавать кластеры hello. Рекомендуется хранить файлы в хранилище больших двоичных объектов Azure. Хранилище BLOB-объектов остается неизменным.

## <a name="list-and-show-clusters"></a>Отображение кластеров
1. Войдите в слишком[https://portal.azure.com](https://portal.azure.com).
2. Нажмите кнопку **кластеров HDInsight** из меню слева hello.
3. Щелкните имя кластера hello. Если список кластеров hello велик, можно использовать фильтр в hello вверху страницы приветствия.
4. Дважды щелкните кластер из tooshow hello hello список сведений.

    **Меню и основная информация**:

    ![Основная информация о кластере HDInsight на портале Azure](./media/hdinsight-administer-use-management-portal/hdinsight-essentials.png)

   * toocustomize hello меню, щелкните правой кнопкой мыши в меню "hello" и нажмите кнопку **Настройка**.
   * **Параметры** и **все параметры**: отображает hello **параметры** колонке hello кластер, который служит tooaccess подробные сведения о конфигурации для кластера hello.
   * **Панель мониторинга**, **мониторинга кластера** и **URL-адрес: это все способы tooaccess hello кластера панели мониторинга, которая является Ambari Web для кластеров под управлением Linux. -**Безопасный оболочки **: Показывает hello инструкции tooconnect toohello кластера с помощью подключения Secure Shell (SSH).
   * **Масштабировать кластер**: позволяет toochange hello число рабочих узлов для этого кластера.
   * **Удалить**: Удаляет hello кластера.
   * **Быстрый запуск**: отображение сведений, необходимых для начала работы с HDInsight.
   * ** Пользователей: Позволяет tooset разрешения для *портала управления* этого кластера для других пользователей в вашей подписке Azure.

     > [!IMPORTANT]
     > Это *только* влияет на доступ и разрешения toothis кластера в hello портал Azure и не влияет на кто может подключаться tooor отправки заданий toohello HDInsight кластера.
     >
     >
   * **Теги**: теги разрешить вы tooset ключ значение пары toodefine пользовательские таксономии облачных служб. Например, можно создать ключ с именем **project**, а затем использовать общее значение для всех служб, связанных с определенным проектом.
   * **Ambari представления**: связывает tooAmbari Web.

     > [!IMPORTANT]
     > toomanage hello службы, предоставляемые hello кластера HDInsight, необходимо использовать Ambari Web или hello Ambari REST API. Дополнительные сведения об использовании Ambari см. в статье [Управление кластерами HDInsight с помощью веб-интерфейса Ambari](hdinsight-hadoop-manage-ambari.md).
     >
     >

     **Использование**:

     ![Использование кластера HDInsight на портале Azure](./media/hdinsight-administer-use-management-portal/hdinsight-portal-cluster-usage.png)
5. Щелкните **Параметры**.

    ![Использование кластера HDInsight на портале Azure](./media/hdinsight-administer-use-management-portal/hdinsight.portal.cluster.settings.png)

   * **Свойства**: Просмотр свойств кластера hello.
   * **Идентификатор AAD кластера**:
   * **Azure хранилища ключей**: Просмотр учетной записи хранения по умолчанию hello и ее ключа. Hello она конфигурации в процессе создания кластера hello.
   * **Кластер входа**: изменение hello кластера HTTP имя и пароль пользователя.
   * **Внешние Метахранилища**: просмотр hello метахранилища Hive и Oozie. Hello метахранилища можно настроить только во время создания кластера hello.
   * **Масштабировать кластер**: увеличение и уменьшение hello число рабочих узлов кластера.
   * **Удаленный рабочий стол**: включить и отключить доступ для удаленного рабочего стола (RDP), а также указать имя пользователя RDP hello.  имя пользователя RDP Hello должен отличаться от hello имя пользователя HTTP.
   * **Зарегистрированный партнер**:

     > [!NOTE]
     > Это универсальный список доступных параметров; не все из них будут присутствовать для всех типов кластера.
     >
     >
6. Щелкните **Свойства**.

    в разделе свойств Hello перечислены hello следующие:

   * **Имя узла**: имя кластера.
   * **URL-адрес кластера**.
   * **Состояние**: возможны варианты "Прервано", "Принято", "Хранилище кластера подготовлено", "Конфигурация виртуальной машины Azure", "Конфигурация HDInsight", "Оперативный", "Выполняется", "Ошибка", "Удаление", "Удалено", "Время ожидания истекло", "Удаление добавлено в очередь", "Истекло время ожидания удаления", "Ошибка удаления", "Исправление добавлено в очередь", "Смена сертификатов в очереди", "Изменение размера поставлено в очередь" и "Настройка кластера".
   * **Регион**: расположение Azure. Список поддерживаемых местоположений Azure см. в разделе hello **область** раскрывающегося списка на [цены на HDInsight](https://azure.microsoft.com/pricing/details/hdinsight/).
   * **Дата создания**.
   * **Операционная система**: **Windows** или **Linux**.
   * **Тип**: Hadoop, HBase, Storm или Spark.
   * **Версия**. См. раздел [Поддерживаемые версии HDInsight](hdinsight-component-versioning.md).
   * **Подписка**: имя подписки.
   * **Идентификатор подписки**.
   * **Первичный источник данных**. Hello учетной записи хранилища больших двоичных объектов Azure используется по умолчанию hello файловой системы Hadoop.
   * **Ценовая категория рабочих узлов**.
   * **Ценовая категория головного узла**.

## <a name="delete-clusters"></a>Удаление кластеров
Учетная запись хранения по умолчанию hello или связанных учетных записей кластера при удалении не удаляются. Можно повторно создать hello кластера с помощью hello одинаковые учетные записи хранения и hello же метахранилища.

1. Войдите в toohello [портала][azure-portal].
2. Нажмите кнопку **просмотреть все** hello в левом меню, щелкните **кластеров HDInsight**, щелкните имя кластера.
3. Нажмите кнопку **удаление** из hello верхнем меню, а затем выполните инструкции hello.

См. также раздел [Приостановка и завершение работы кластеров](#pauseshut-down-clusters).

## <a name="scale-clusters"></a>Масштабирование кластеров
масштабирование функции кластера Hello позволяет toochange hello число рабочих узлов в кластере, который выполняется в Azure HDInsight без необходимости toore-создать кластер hello.

> [!NOTE]
> Поддерживаются только кластеры HDInsight версии 3.1.3 или более поздней. Если вы не знаете hello версии кластера, можно проверить свойства страницы приветствия.  См. раздел [Отображение кластеров](#list-and-show-clusters).
>
>

Hello последствия изменения hello количество узлов данных для каждого типа поддерживаемых HDInsight кластера:

* Hadoop

    Можно легко увеличить hello число рабочих узлов в кластере Hadoop, на котором выполняется без ущерба для все ожидающие или выполняемые задания. Также можно отправлять новые задания, hello операции во время выполнения. Ошибки в операции масштабирования обрабатываются правильно, чтобы hello кластер всегда оставался в рабочем состоянии.

    Когда кластер Hadoop уменьшено за счет уменьшения hello количество узлов данных, некоторые службы hello в кластере hello перезапускаются. В результате все выполняющиеся и ожидающие задания toofail окончании hello hello операцию масштабирования. Можно Однако повторно отправить задания hello после завершения операции hello.
* HBase

    Можно легко добавить или удалить узлы tooyour HBase кластера при выполнении. Региональные серверы распределяются автоматически через несколько минут после завершения hello операция масштабирования. Тем не менее можно также вручную сбалансировать региональные серверы hello, войдя в hello головному узлу кластера, и выполнение hello, следующие команды из окна командной строки:

        >pushd %HBASE_HOME%\bin
        >hbase shell
        >balancer

    Дополнительные сведения об использовании оболочки HBase hello см. в разделе]
* Storm

    Можно легко добавить или удалить кластер Storm tooyour узлы данных при выполнении. Однако после успешного завершения hello операция масштабирования потребуется toorebalance hello топологии.

    Повторную балансировку можно выполнить двумя способами:

  * с помощью веб-интерфейса Storm;
  * с помощью программы командной строки.

    См. toohello [документации Apache Storm](http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html) для получения дополнительных сведений.

    в кластере HDInsight hello доступен Hello Storm пользовательского веб-интерфейса:

    ![HDInsight, storm, масштабирование, перераспределение](./media/hdinsight-administer-use-management-portal/hdinsight-portal-scale-cluster-storm-rebalance.png)

    Ниже приведен пример как toouse hello CLI команды toorebalance hello Storm топологии:

        ## Reconfigure hello topology "mytopology" toouse 5 worker processes,
        ## hello spout "blue-spout" toouse 3 executors, and
        ## hello bolt "yellow-bolt" toouse 10 executors
        $ storm rebalance mytopology -n 5 -e blue-spout=3 -e yellow-bolt=10

**tooscale кластеров**

1. Войдите в toohello [портала][azure-portal].
2. Нажмите кнопку **просмотреть все** hello в левом меню, щелкните **кластеров HDInsight**, щелкните имя кластера.
3. Нажмите кнопку **параметры** hello верхнем меню, и нажмите кнопку **масштабирования кластера**.
4. В поле **Количество рабочих узлов**укажите нужное количество. Hello лимит hello узла кластера различается для каждой подписки Azure. Вы можете обратиться выставления счетов tooincrease hello допустимое ограничение.  сведения о стоимости Hello отразят hello внесенные вами изменения toohello количество узлов.

    ![HDInsight, Hadoop, HBase, Storm Spark, масштабирование](./media/hdinsight-administer-use-management-portal/hdinsight.portal.scale.cluster.png)

## <a name="pauseshut-down-clusters"></a>Приостановка и завершение работы кластеров
Большинство заданий Hadoop представляют собой пакетные задания, выполняемые от случая к случаю. Для большинства кластеров Hadoop, являются большие промежутки времени hello кластера не используется для обработки. В случае с HDInsight ваши данные хранятся в службе хранилища Azure, что позволяет безопасно удалить неиспользуемый кластер.
Плата за кластеры HDInsight взимается, даже когда они не используются. Поскольку плата hello для кластера hello много раз больше, чем hello плата за хранилище, экономически выгодно toodelete кластеры, когда они не используются.

Вы можете программировать процесса hello разными способами:

* С помощью фабрики данных Azure. Выполняемые по запросу и самоопределяющиеся связанные службы HDInsight описаны в статьях [Связанные службы вычислений](../data-factory/data-factory-compute-linked-services.md) и [Преобразование данных в фабрике данных Azure](../data-factory/data-factory-data-transformation-activities.md).
* С помощью Azure PowerShell.  См. статью [Анализ данных о задержке рейсов с помощью Hive в HDInsight](hdinsight-analyze-flight-delay-data.md).
* С помощью интерфейса командной строки Azure. См. статью [Управление кластерами Hadoop в HDInsight с помощью интерфейса командной строки (CLI) Azure](hdinsight-administer-use-command-line.md).
* С помощью пакета SDK для HDInsight .NET. См. статью [Отправка заданий Hadoop в HDInsight](hdinsight-submit-hadoop-jobs-programmatically.md).

Привет, сведения о ценах, см. [цены на HDInsight](https://azure.microsoft.com/pricing/details/hdinsight/). toodelete кластер из портала hello. в разделе [удалить кластеров](#delete-clusters)

## <a name="change-cluster-username"></a>Изменение имени пользователя кластера
Кластер HDInsight может иметь две учетные записи пользователя. Hello учетной записи пользователя кластеров HDInsight создается во время процесса создания hello. Можно также создать учетную запись пользователя протокола удаленного рабочего СТОЛА для доступа к hello кластер с помощью RDP. См. сведения о [включении удаленного рабочего стола](#connect-to-hdinsight-clusters-by-using-rdp).

**имя пользователя кластера HDInsight toochange hello и пароль**

1. Войдите в toohello [портала][azure-portal].
2. Нажмите кнопку **просмотреть все** hello в левом меню, щелкните **кластеров HDInsight**, щелкните имя кластера.
3. Нажмите кнопку **параметры** hello верхнем меню, и нажмите кнопку **входа кластера**.
4. Если **входа кластера** был включен, необходимо нажать кнопку **отключить**и нажмите кнопку **включить** перед изменением hello имени пользователя и пароля...
5. Изменение hello **имя входа кластера** и/или hello **входа пароль кластера**и нажмите кнопку **Сохранить**.

    ![hdinsight, изменение, пользователь кластера, имя пользователя, пароль, http пользователь](./media/hdinsight-administer-use-management-portal/hdinsight.portal.change.username.password.png)

## <a name="grantrevoke-access"></a>Предоставление и отмена доступа
Кластеры HDInsight имеют hello следующие веб-службы HTTP (все эти службы имеют RESTful конечные точки):

* ODBC
* JDBC
* Ambari
* Oozie
* Templeton

По умолчанию эти службы предоставляются для доступа. Вы можете revoke или предоставления hello доступа из hello портал Azure.

> [!NOTE]
> Предоставление или Отмена доступа hello, восстановится hello кластера имя и пароль пользователя.
>
>

**toogrant или отмены HTTP веб-службы доступа**

1. Войдите в toohello [портала][azure-portal].
2. Нажмите кнопку **просмотреть все** hello в левом меню, щелкните **кластеров HDInsight**, щелкните имя кластера.
3. Нажмите кнопку **параметры** hello верхнем меню, и нажмите кнопку **входа кластера**.
4. Если **входа кластера** был включен, необходимо нажать кнопку **отключить**и нажмите кнопку **включить** перед изменением hello имени пользователя и пароля...
5. Для **пользователя для входа кластер** и **входа пароль кластера**, введите hello новое имя пользователя и пароль (соответственно) для кластера hello.
6. Щелкните **СОХРАНИТЬ**.

    ![hdinsight, предоставление, отмена, http, веб-служба, доступ](./media/hdinsight-administer-use-management-portal/hdinsight.portal.change.username.password.png)

## <a name="find-hello-default-storage-account"></a>Найти учетную запись хранения по умолчанию hello
Каждый кластер HDInsight имеет учетную запись хранения, используемую по умолчанию. Здравствуйте учетной записи хранения по умолчанию и ее ключи, для кластера отображается под **параметры**/**свойства**/**хранилища ключей Azure**. См. раздел [Отображение кластеров](#list-and-show-clusters).

## <a name="find-hello-resource-group"></a>Найти группу ресурсов hello
В режиме Azure Resource Manager hello каждый кластер HDInsight создается с группой ресурсов Azure. группы ресурсов Azure Hello, кластер, к которому относится tooappears в:

* содержит список кластеров Hello **группы ресурсов** столбца.
* на плитке кластера **Основное** .  

Выполняемые по запросу и самоопределяющиеся связанные службы HDInsight описаны в статьях [Отображение кластеров](#list-and-show-clusters).

## <a name="open-hdinsight-query-console"></a>Открытие консоли запросов HDInsight
Hello консоли HDInsight запроса включает hello следующие атрибуты:

* **Редактор кустов**. Графический пользовательский веб-интерфейс для отправки заданий Hive.  В разделе [запуска Hive запросы, использующие hello консоль запросов](hdinsight-hadoop-use-hive-query-console.md).

    ![Редактор кустов на портале HDInsight](./media/hdinsight-administer-use-management-portal/hdinsight-hive-editor.png)
* **Журнал заданий**. Позволяет отслеживать задания Hadoop.  

    ![История заданий на портале HDInsight](./media/hdinsight-administer-use-management-portal/hdinsight-job-history.png)

    Нажмите кнопку **имя запроса** tooshow hello сведения, включая свойства задания **запроса задания**, и ** выходные данные задания. Можно также загрузить запрос hello и рабочей станции tooyour вывода hello.
* **Файл браузера**: Обзор учетной записи хранения по умолчанию hello и hello связанным учетных записей хранения.

    ![Обозреватель файлов на портале HDInsight](./media/hdinsight-administer-use-management-portal/hdinsight-file-browser.png)

    На снимке экрана приветствия hello  **<Account>**  тип указывает hello элемент учетная запись хранилища Azure.  Щелкните файлы hello toobrowse имени учетной записи hello.
* **Пользовательский интерфейс Hadoop:**

    ![Пользовательский интерфейс Hadoop на портале HDInsight](./media/hdinsight-administer-use-management-portal/hdinsight-hadoop-ui.png)

    В **пользовательском интерфейсе Hadoop*можно просматривать файлы и журналы.
* **Пользовательский интерфейс Yarn:**

    ![Пользовательский интерфейс YARN на портале HDInsight](./media/hdinsight-administer-use-management-portal/hdinsight-yarn-ui.png)

## <a name="run-hive-queries"></a>Выполнение запросов Hive
задания Hive tooran из hello портала, нажмите кнопку **редактор Hive** в hello запроса HDInsight консоли. Выполняемые по запросу и самоопределяющиеся связанные службы HDInsight описаны в статьях [Открытие консоли запросов HDInsight](#open-hdinsight-query-console).

## <a name="monitor-jobs"></a>Мониторинг заданий
toomonitor задания из hello портала, нажмите кнопку **журнал заданий** в hello запроса HDInsight консоли. Выполняемые по запросу и самоопределяющиеся связанные службы HDInsight описаны в статьях [Открытие консоли запросов HDInsight](#open-hdinsight-query-console).

## <a name="browse-files"></a>Обзор файлов
toobrowse файлы хранятся в учетной записи хранения по умолчанию hello и hello связанным учетных записей хранения, нажмите кнопку **браузер файла** в hello запроса HDInsight консоли. Выполняемые по запросу и самоопределяющиеся связанные службы HDInsight описаны в статьях [Открытие консоли запросов HDInsight](#open-hdinsight-query-console).

Можно также использовать hello **Обзор файловой системы hello** служебной программы из hello **Hadoop пользовательского интерфейса** в консоли HDInsight hello.  Выполняемые по запросу и самоопределяющиеся связанные службы HDInsight описаны в статьях [Открытие консоли запросов HDInsight](#open-hdinsight-query-console).

## <a name="monitor-cluster-usage"></a>Мониторинг использования кластера
Hello **использование** раздел колонка кластера HDInsight hello отображает сведения о hello число ядер подписки tooyour доступны для использования с HDInsight, а также hello количество ядер, выделенных toothis кластера и как они могут выделить для hello узлов на этом кластере. См. раздел [Отображение кластеров](#list-and-show-clusters).

> [!IMPORTANT]
> toomonitor hello службы, предоставляемые hello кластера HDInsight, необходимо использовать Ambari Web или hello Ambari REST API. Дополнительные сведения об использовании Ambari см. в статье [Управление кластерами HDInsight с помощью веб-интерфейса Ambari](hdinsight-hadoop-manage-ambari.md).
>
>

## <a name="open-hadoop-ui"></a>Открытие пользовательского интерфейса Hadoop
toomonitor hello кластера, обзора hello файловой системы и проверьте журналы, нажмите **пользовательского интерфейса Hadoop** в HDInsight запрос hello консоли. Выполняемые по запросу и самоопределяющиеся связанные службы HDInsight описаны в статьях [Открытие консоли запросов HDInsight](#open-hdinsight-query-console).

## <a name="open-yarn-ui"></a>Открытие пользовательского интерфейса Yarn
Щелкните toouse Yarn пользовательского интерфейса, **Yarn пользовательского интерфейса** в hello запроса HDInsight консоли. Выполняемые по запросу и самоопределяющиеся связанные службы HDInsight описаны в статьях [Открытие консоли запросов HDInsight](#open-hdinsight-query-console).

## <a name="connect-tooclusters-using-rdp"></a>Подключение с использованием протокола удаленного рабочего СТОЛА tooclusters
Hello учетные данные для кластера hello, предоставленные при его создании предоставляют доступ службы toohello на hello кластера, но не toohello самого кластера через удаленный рабочий стол. Вы можете включить доступ к удаленному рабочему столу во время или после подготовки кластера. Hello инструкции о включении удаленного рабочего стола в момент создания см. в разделе [кластера HDInsight, создания](hdinsight-hadoop-provision-linux-clusters.md).

**tooenable удаленного рабочего стола**

1. Войдите в toohello [портала][azure-portal].
2. Нажмите кнопку **просмотреть все** hello в левом меню, щелкните **кластеров HDInsight**, щелкните имя кластера.
3. Нажмите кнопку **параметры** hello верхнем меню, и нажмите кнопку **удаленного рабочего стола**.
4. Заполните поля **Срок действия**, **Имя пользователя удаленного рабочего стола** и **Пароль удаленного рабочего стола**, а затем нажмите кнопку **Включить**.

    ![Hdinsight, включить, отключить, настроить, удаленный рабочий стол](./media/hdinsight-administer-use-management-portal/hdinsight.portal.remote.desktop.png)

    значения по умолчанию Hello для срок действия — час.

   > [!NOTE]
   > Также можно использовать tooenable HDInsight .NET SDK hello удаленного рабочего стола в кластере. Используйте hello **EnableRdp** hello объекта клиента HDInsight в следующие способом hello метод: **клиента. EnableRdp (clustername, расположение, «rdpuser», «rdppassword», DateTime.Now.AddDays(6))**. Аналогично, toodisable удаленного рабочего стола на кластере hello, можно использовать **клиента. DisableRdp (имя_кластера, расположение)**. Дополнительные сведения об этих методах см. в [справочнике по пакету SDK для HDInsight .NET](http://go.microsoft.com/fwlink/?LinkId=529017). Это применимо только для кластеров HDInsight под управлением Windows.
   >
   >

**tooconnect tooa кластера с помощью протокола удаленного рабочего СТОЛА**

1. Войдите в toohello [портала][azure-portal].
2. Нажмите кнопку **просмотреть все** hello в левом меню, щелкните **кластеров HDInsight**, щелкните имя кластера.
3. Нажмите кнопку **параметры** hello верхнем меню, и нажмите кнопку **удаленного рабочего стола**.
4. Нажмите кнопку **Connect** и следуйте инструкциям, hello. Если кнопка «Подключить» неактивна, сначала активируйте ее. Убедитесь, что с помощью hello удаленного рабочего стола пользователя, имя пользователя и пароль.  Не удается использовать учетные данные кластера hello.

## <a name="open-hadoop-command-line"></a>Открытие командной строки Hadoop
tooconnect toohello кластера с помощью удаленного рабочего стола и использовать hello Hadoop командной строки, необходимо сначала включить удаленный рабочий стол доступа toohello кластера как описано в предыдущем разделе hello.

**tooopen командной строки Hadoop**

1. Подключите кластер toohello, с помощью удаленного рабочего стола.
2. С рабочего стола hello, дважды щелкните **командной строки Hadoop**.

    ![HDI.HadoopCommandLine][image-hadoopcommandline]

    Дополнительные сведения о командах Hadoop см. в [справочнике по командам Hadoop](http://hadoop.apache.org/docs/current/hadoop-project-dist/hadoop-common/CommandsManual.html).

В предыдущем снимке экрана hello hello имя папки имеет hello Hadoop номер версии внедрены. номер версии Hello можно версии измененных на основе hello hello компонентов Hadoop, установленных на кластере hello. Можно использовать Hadoop среды переменные toorefer toothose папки. Например:

    cd %hadoop_home%
    cd %hive_home%
    cd %hbase_home%
    cd %pig_home%
    cd %sqoop_home%
    cd %hcatalog_home%

## <a name="next-steps"></a>Дальнейшие действия
В этой статье вы узнали, как toocreate кластер HDInsight с помощью hello портала и как tooopen hello средство командной строки Hadoop. toolearn более, см. следующие статьи hello.

* [Администрирование HDInsight с помощью Azure PowerShell](hdinsight-administer-use-powershell.md)
* [Администрирование HDInsight с помощью CLI Azure](hdinsight-administer-use-command-line.md)
* [Создание кластеров Hadoop в HDInsight](hdinsight-hadoop-provision-linux-clusters.md)
* [Отправка заданий Hadoop в HDInsight](hdinsight-submit-hadoop-jobs-programmatically.md)
* [Начало работы с Azure HDInsight](hdinsight-hadoop-linux-tutorial-get-started.md)
* [Какая версия Hadoop включена в Azure HDInsight?](hdinsight-component-versioning.md)

[azure-portal]: https://portal.azure.com
[image-hadoopcommandline]: ./media/hdinsight-administer-use-management-portal/hdinsight-hadoop-command-line.png "Командная строка Hadoop"
