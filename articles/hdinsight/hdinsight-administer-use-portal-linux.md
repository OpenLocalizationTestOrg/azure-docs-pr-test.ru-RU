---
title: "кластеры aaaManage Hadoop в HDInsight с помощью портала Azure | Документы Microsoft"
description: "Узнайте, как toocreate hello портал Azure с помощью кластеров HDInsight и управления ими."
services: hdinsight
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 5a76f897-02e8-4437-8f2b-4fb12225854a
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/15/2017
ms.author: jgao
ms.openlocfilehash: c242d43d4ccea7cf1e7be19c3f3d7ed3c4f50918
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="manage-hadoop-clusters-in-hdinsight-by-using-hello-azure-portal"></a>Управление кластерами Hadoop в HDInsight с помощью портала Azure hello
[!INCLUDE [selector](../../includes/hdinsight-portal-management-selector.md)]

С помощью hello [портал Azure][azure-portal], вы можете управлять кластеров Hadoop в Azure HDInsight. Используйте выбора вкладки hello сведения об управлении кластерами Hadoop в HDInsight с помощью других средств.

**Предварительные требования**

Прежде чем приступать к этой статье, необходимо иметь hello следующих элементов:

* **Подписка Azure**. Ознакомьтесь с [бесплатной пробной версией Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).

## <a name="open-hello-portal"></a>Привет открыть портал
1. Войдите в слишком[https://portal.azure.com](https://portal.azure.com).
2. После открытия hello портала можно:

   * Нажмите кнопку **New** из toocreate меню слева hello нового кластера:

       ![Кнопка создания кластера HDInsight](./media/hdinsight-administer-use-portal-linux/azure-portal-new-button.png)
   * Нажмите кнопку **кластеров HDInsight** из hello toolist меню слева hello существующих кластеров

       ![Кнопка кластера HDInsight на портале Azure](./media/hdinsight-administer-use-portal-linux/azure-portal-hdinsight-button.png)

       Если вы не видите кластера HDInsight, нажмите кнопку **дополнительные службы** в нижней части списка hello hello и нажмите кнопку **кластеров HDInsight** под hello **аналитики + аналитика** раздел.


## <a name="create-clusters"></a>Создание кластеров
[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

HDInsight работает со множеством компонентов Hadoop. Список hello hello компонентов, которые были проверены и поддерживается, в разделе [версии Hadoop — в Azure HDInsight](hdinsight-component-versioning.md). Hello общие кластера создания Подробнее [кластеров создать Hadoop в HDInsight](hdinsight-hadoop-provision-linux-clusters.md).

### <a name="access-control-requirements"></a>Требования к контролю доступа

При создании кластера HDInsight необходимо указать подписку Azure. Этот кластер может быть создан как новая или существующая группа ресурсов Azure. Можно использовать следующие шаги tooverify hello ваши разрешения для создания кластеров HDInsight:

- toouse существующую группу ресурсов.

    1. Войдите в toohello [портал Azure](https://portal.azure.com).
    2. Нажмите кнопку **групп ресурсов** из групп ресурсов hello toolist меню слева hello.
    3. Щелкните группу ресурсов hello требуется toouse для создания кластера HDInsight.
    4. Нажмите кнопку **(IAM) управления доступом к**и убедитесь, что вы (или группа, к которой принадлежит) имеют по крайней мере hello группы ресурсов toohello доступа участника.

- toocreate новую группу ресурсов

    1. Войдите в toohello [портал Azure](https://portal.azure.com).
    2. Нажмите кнопку **подписки** из меню слева hello. (вы увидите значок ключа желтого цвета). Отобразится список подписок.
    3. Щелкните подписку hello использовать toocreate кластеров. 
    4. Щелкните **Мои разрешения**.  Он показывает вашей [роли](../active-directory/role-based-access-control-what-is.md#built-in-roles) в подписке hello. Требуется по крайней мере кластера HDInsight toocreate доступа участника.

Если появляется ошибка NoRegisteredProviderFound hello или MissingSubscriptionRegistration hello, см. раздел [Устранение общих ошибок развертывания Azure с помощью диспетчера ресурсов Azure](../azure-resource-manager/resource-manager-common-deployment-errors.md).

## <a name="list-and-show-clusters"></a>Отображение кластеров
1. Войдите в слишком[https://portal.azure.com](https://portal.azure.com).
2. Нажмите кнопку **кластеров HDInsight** из hello toolist меню слева hello существующих кластеров.
3. Щелкните имя кластера hello. Если список кластеров hello велик, можно использовать фильтр в hello вверху страницы приветствия.
4. Выберите кластер из списка toosee hello hello-страница обзора:

    ![Основная информация о кластере HDInsight на портале Azure](./media/hdinsight-administer-use-portal-linux/hdinsight-essentials.png)

    * **Панель мониторинга**: кластера hello откроется панель, которая является Ambari Web для кластеров под управлением Linux.
    * **Secure Shell**: отображает hello инструкции tooconnect toohello кластера с помощью подключения Secure Shell (SSH).
    * **Масштабировать кластер**: позволяет toochange hello число рабочих узлов для этого кластера.
    * **Удалить**: Удаляет hello кластера.
    * **Журналы действий.** Отображайте и запрашивайте журналы действий.
    * **Управление доступом (IAM).** Используйте назначение ролей.  В разделе [использовать tooyour роли назначения toomanage доступ к ресурсам подписки Azure](../active-directory/role-based-access-control-configure.md).
    * **Теги**: позволяет вам tooset ключ значение пары toodefine пользовательские таксономии облачных служб. Например, можно создать ключ с именем **project**, а затем использовать общее значение для всех служб, связанных с определенным проектом.
    * **Диагностика и решение проблем.** Отображайте сведения об устранении неполадок.
    * **Блокирует**: Добавление блокировки tooprevent hello кластера, был изменен или удален.
    * **Сценарий автоматизации**: отображение и Экспорт шаблона Azure Resource Manager hello для hello кластера. В настоящее время можно экспортировать только hello зависимых учетная запись хранения Azure. Ознакомьтесь со статьей [Создание кластеров Hadoop под управлением Linux в HDInsight с помощью шаблонов Azure Resource Manager](hdinsight-hadoop-create-linux-clusters-arm-templates.md).
    * **Быстрое начало работы.** Отображение сведений, необходимых для начала работы с HDInsight.
    * **Средства для HDInsight.** Справочные сведения об инструментах, связанных с HDInsight.
    * **Кластер входа**: отображать сведения об имени входа hello кластера.
    * **Использование основных подписки**: отображение hello используемых и доступных ядер для подписки.
    * **Масштабировать кластер**: увеличение и уменьшение hello число рабочих узлов кластера. Ознакомьтесь с разделом [Масштабирование кластеров](hdinsight-administer-use-management-portal.md#scale-clusters).
    * **Secure Shell**: отображает hello инструкции tooconnect toohello кластера с помощью подключения Secure Shell (SSH). Дополнительные сведения см. в статье [Использование SSH с Hadoop на основе Linux в HDInsight из Linux, Unix или OS X](hdinsight-hadoop-linux-use-ssh-unix.md).
    * **Партнера HDInsight**: Добавление или удаление hello текущего партнера HDInsight.
    * **Внешние Метахранилища**: просмотр hello метахранилища Hive и Oozie. Hello метахранилища можно настроить только во время создания кластера hello. Ознакомьтесь с разделом [Использование метахранилища Hive/Oozie](hdinsight-hadoop-provision-linux-clusters.md#use-hiveoozie-metastore).
    * **Скрипт действия**: Bash запуска сценариев на кластере hello. См. статью [Настройка кластеров HDInsight под управлением Linux с помощью действия сценария](hdinsight-hadoop-customize-cluster-linux.md).
    * **Приложения.** Добавляйте и удаляйте приложения HDInsight.  Ознакомьтесь со статьей [Установка пользовательских приложений HDInsight](hdinsight-apps-install-custom-applications.md).
    * **Свойства**: Просмотр свойств кластера hello.
    * **Учетные записи хранения**: просмотр учетных записей хранения hello и ключи hello. учетные записи хранения Hello настраиваются во время создания кластера hello.
    * **Идентификатор AAD кластера**:
    * **Новый запрос на поддержку**: позволяет toocreate обращение в службу поддержки со службой поддержки Майкрософт.
    
6. Щелкните **Свойства**.

    Существуют следующие свойства Hello

   * **Имя узла**: имя кластера.
   * **URL-адрес кластера**. URL-адрес Hello hello Ambari веб-интерфейса.
   * **Состояние**: возможны варианты "Прервано", "Принято", "Хранилище кластера подготовлено", "Конфигурация виртуальной машины Azure", "Конфигурация HDInsight", "Оперативный", "Выполняется", "Ошибка", "Удаление", "Удалено", "Время ожидания истекло", "Удаление добавлено в очередь", "Истекло время ожидания удаления", "Ошибка удаления", "Исправление добавлено в очередь", "Смена сертификатов в очереди", "Изменение размера поставлено в очередь" и "Настройка кластера".
   * **Регион**: расположение Azure. Список поддерживаемых местоположений Azure см. в разделе hello **область** раскрывающегося списка на [цены на HDInsight](https://azure.microsoft.com/pricing/details/hdinsight/).
   * **Дата создания.**
   * **Операционная система**: **Windows** или **Linux**.
   * **Тип**: Hadoop, HBase, Storm или Spark.
   * **Версия**. См. раздел [Поддерживаемые версии HDInsight](hdinsight-component-versioning.md).
   * **Подписка**: имя подписки.
   * **Источник данных по умолчанию**: hello по умолчанию кластера файловой системы.
   * **Worker nodes size** (Размер рабочих узлов).
   * **Размер головного узла.**

## <a name="delete-clusters"></a>Удаление кластеров
Удаление кластера не приводит к удалению учетной записи хранения по умолчанию hello или связанных учетных записей. Можно повторно создать hello кластера с помощью hello одинаковые учетные записи хранения и hello же метахранилища. Это рекомендуется toouse новый контейнер больших двоичных объектов по умолчанию, при повторном создании кластера hello.

1. Войдите в toohello [портала][azure-portal].
2. Нажмите кнопку **кластеров HDInsight** из меню слева hello. Если вы не видите **кластеры HDInsight**, сначала щелкните **Больше служб**.
3. Щелкните кластер hello, которое следует toodelete.
4. Нажмите кнопку **удаление** из hello верхнем меню, а затем выполните инструкции hello.

См. также раздел [Приостановка и завершение работы кластеров](#pauseshut-down-clusters).

## <a name="add-additional-storage-accounts"></a>Добавление дополнительных учетных записей хранения

После создания кластера можно добавить дополнительные учетные записи службы хранилища Azure и учетные записи Azure Data Lake Store. Дополнительные сведения см. в разделе [добавить дополнительное хранилище учетных записей tooHDInsight](./hdinsight-hadoop-add-storage.md).

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

    Можно легко добавить или удалить узлы tooyour HBase кластера при выполнении. Региональные серверы распределяются автоматически через несколько минут после завершения hello операция масштабирования. Тем не менее можно также вручную сбалансировать региональные серверы hello войдите в систему в toohello головному узлу кластера, и выполнение hello, следующие команды из окна командной строки:

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

    ![HDInsight, Storm, масштабирование, перераспределение](./media/hdinsight-administer-use-portal-linux/hdinsight-portal-scale-cluster-storm-rebalance.png)

    Ниже приведен пример как toouse hello CLI команды toorebalance hello Storm топологии:

        ## Reconfigure hello topology "mytopology" toouse 5 worker processes,
        ## hello spout "blue-spout" toouse 3 executors, and
        ## hello bolt "yellow-bolt" toouse 10 executors
        $ storm rebalance mytopology -n 5 -e blue-spout=3 -e yellow-bolt=10

**tooscale кластеров**

1. Войдите в toohello [портала][azure-portal].
2. Нажмите кнопку **кластеров HDInsight** из меню слева hello.
3. Щелкните hello кластер tooscale.
3. Щелкните **Изменить масштаб кластера**.
4. В поле **Количество рабочих узлов**укажите нужное количество. максимально Hello hello количество узлов кластера различается для каждой подписки Azure. Вы можете обратиться выставления счетов tooincrease hello допустимое ограничение.  сведения о стоимости Hello отражает hello внесенные вами изменения toohello количество узлов.

    ![HDInsight, Hadoop, HBase, Storm, Spark, масштабирование](./media/hdinsight-administer-use-portal-linux/hdinsight-portal-scale-cluster.png)

## <a name="pauseshut-down-clusters"></a>Приостановка и завершение работы кластеров

Большинство заданий Hadoop представляют собой пакетные задания, выполняемые от случая к случаю. Для большинства кластеров Hadoop, являются большие промежутки времени hello кластера не используется для обработки. В случае с HDInsight ваши данные хранятся в службе хранилища Azure, что позволяет безопасно удалить неиспользуемый кластер.
Плата за кластеры HDInsight взимается, даже когда они не используются. Поскольку плата hello для кластера hello много раз больше, чем hello плата за хранилище, экономически выгодно toodelete кластеры, когда они не используются.

Вы можете программировать процесса hello разными способами:

* С помощью фабрики данных Azure. Дополнительные сведения о создании связанных служб HDInsight по запросу см. в статье [Создание кластеров Hadoop под управлением Linux в HDInsight по запросу с помощью фабрики данных Azure](hdinsight-hadoop-create-linux-clusters-adf.md).
* С помощью Azure PowerShell.  См. статью [Анализ данных о задержке рейсов с помощью Hive в HDInsight](hdinsight-analyze-flight-delay-data.md).
* С помощью интерфейса командной строки Azure. См. статью [Управление кластерами Hadoop в HDInsight с помощью интерфейса командной строки (CLI) Azure](hdinsight-administer-use-command-line.md).
* С помощью пакета SDK для HDInsight .NET. См. статью [Отправка заданий Hadoop в HDInsight](hdinsight-submit-hadoop-jobs-programmatically.md).

Привет, сведения о ценах, см. [цены на HDInsight](https://azure.microsoft.com/pricing/details/hdinsight/). toodelete кластер из портала hello. в разделе [удалить кластеров](#delete-clusters)


## <a name="upgrade-clusters"></a>Установка новых версий кластеров

В разделе [HDInsight обновление кластера tooa новой версии](./hdinsight-upgrade-cluster.md).

## <a name="change-passwords"></a>Изменение паролей
Кластер HDInsight может иметь две учетные записи пользователя. (так называемый Hello учетной записи пользователя кластеров HDInsight Учетная запись пользователя HTTP) и hello SSH учетной записи пользователя создаются во время процесса создания hello. Можно использовать hello Ambari web пользовательского интерфейса toochange hello кластера учетной записи пользователя и пароль и hello toochange сценария действия учетной записи пользователя SSH

### <a name="change-hello-cluster-user-password"></a>Изменить пароль пользователя кластера hello
Можно использовать пароль пользователя кластера hello toochange hello Ambari веб-интерфейса. toolog в tooAmbari необходимо использовать hello существующего кластера, имя пользователя и пароль.

> [!NOTE]
> При смене hello кластера пароля пользователя (администратор) может привести к выполняли действия для этого кластера toofail сценария. Если у вас есть все сохраненные действия скриптов, предназначенных для рабочих узлов, эти сценарии может завершиться ошибкой при добавлении кластера узлов toohello с помощью операции изменения размера. Дополнительные сведения о действиях сценариев см. в статье [Настройка кластеров HDInsight под управлением Linux с помощью действия сценария](hdinsight-hadoop-customize-cluster-linux.md).
>
>

1. Вход с помощью пользовательского интерфейса Ambari Web toohello hello учетные данные кластера HDInsight. имя пользователя по умолчанию Hello **администратора**. URL-адрес является hello **https://&lt;имя кластера HDInsight > azurehdinsight.net**.
2. Нажмите кнопку **администратора** hello в верхнем меню, а затем нажмите кнопку «Управление Ambari».
3. Hello в левом меню, щелкните **пользователей**.
4. Щелкните **Администратор**.
5. Щелкните **Change Password**(Изменить пароль).

Ambari затем изменяет пароль hello на всех узлах в кластере hello.

### <a name="change-hello-ssh-user-password"></a>Смена пароля пользователя SSH hello
1. В текстовом редакторе, сохраните следующий текст в файл с именем hello **changepassword.sh**.

   > [!IMPORTANT]
   > Необходимо использовать редактор, который используется как конечная строка hello LF. Если редактор hello использует CRLF, скрипт hello не работает.
   >
   >

        #! /bin/bash
        USER=$1
        PASS=$2

        usermod --password $(echo $PASS | openssl passwd -1 -stdin) $USER
2. Отправьте hello tooa расположение хранилища, доступный из HDInsight с помощью адреса HTTP или HTTPS. Например, в такое общедоступное хранилище файлов, как OneDrive или хранилище BLOB-объектов Azure. Сохраните файл toohello hello URI (адрес HTTP или HTTPS), при этом требуется этот URI в следующем шаге hello.
3. Hello портал Azure, щелкните **кластеров HDInsight**.
4. Щелкните свой кластер HDInsight.
4. Щелкните **Действия скрипта**.
4. Из hello **действия скрипта** колонке выберите **отправить новый**. Здравствуйте, когда **отправить действие скрипта** появится в колонке, введите hello следующую информацию:

   | Поле | Значение |
   | --- | --- |
   | Имя |Измените пароль SSH |
   | URI bash-скрипта |файл changepassword.sh toohello URI Hello |
   | Узлы (головные, рабочие, Nimbus, супервизора, Zookeeper и т. д.). |✓ для всех перечисленных типов узлов. |
   | Параметры |Введите имя пользователя SSH hello, а затем hello новый пароль. Должен быть хотя бы один пробел между hello имя пользователя и пароль hello. |
   | Сохранить этот скрипт… |Оставьте это поле без изменений. |
5. Выберите **создать** tooapply hello скрипта. После завершения выполнения сценария hello, вы являетесь может tooconnect toohello кластера с помощью SSH с hello нового пароля.

## <a name="grantrevoke-access"></a>Предоставление и отмена доступа
Кластеры HDInsight имеют hello следующие веб-службы HTTP (все эти службы имеют RESTful конечные точки):

* ODBC
* JDBC
* Ambari
* Oozie
* Templeton

По умолчанию эти службы предоставляются для доступа. Вы можете revoke или предоставления hello доступа с помощью [Azure CLI](hdinsight-administer-use-command-line.md#enabledisable-http-access-for-a-cluster) и [Azure PowerShell](hdinsight-administer-use-powershell.md#grantrevoke-access).

## <a name="find-hello-subscription-id"></a>Найти идентификатор подписки hello

**toofind подписки Azure идентификаторы**

1. Войдите в toohello [портала][azure-portal].
2. Щелкните **Подписки**. У всех подписок есть имя и идентификатор.

Каждый кластер имеет связанные tooan подписки Azure. Здравствуйте, на кластере hello отображается идентификатор подписки **Essential** плитки. См. раздел [Отображение кластеров](#list-and-show-clusters).

## <a name="find-hello-resource-group"></a>Найти группу ресурсов hello
В режиме Azure Resource Manager hello каждый кластер HDInsight создается с группой диспетчера ресурсов Azure. Группа диспетчера ресурсов Hello, кластер, к которому относится tooappears в:

* содержит список кластеров Hello **группы ресурсов** столбца.
* на плитке кластера **Основное** .  

См. раздел [Отображение кластеров](#list-and-show-clusters).

## <a name="find-hello-default-storage-account"></a>Найти учетную запись хранения по умолчанию hello
Каждый кластер HDInsight имеет учетную запись хранения, используемую по умолчанию. Здравствуйте учетной записи хранения по умолчанию и ее ключи, для кластера отображается под **учетные записи хранения**. См. раздел [Отображение кластеров](#list-and-show-clusters).

## <a name="run-hive-queries"></a>Выполнение запросов Hive
Не удалось запустить задание куста непосредственно из hello портал Azure, но можно использовать hello Hive представление Ambari веб-интерфейса.

**с помощью Ambari Hive представления запросов Hive toorun**

1. Вход с помощью пользовательского интерфейса Ambari Web toohello hello учетные данные кластера HDInsight. имя пользователя по умолчанию Hello **администратора**. URL-адрес является hello **https://&lt;имя кластера HDInsight > azurehdinsight.net**.
2. Открыть представление Hive, как показано на следующий снимок экрана приветствия:  

    ![Представление Hive в HDInsight](./media/hdinsight-administer-use-portal-linux/hdinsight-hive-view.png)
3. Нажмите кнопку **запроса** hello верхнем меню.
4. Введите запрос Hive в **редактор запросов**, а затем нажмите кнопку **Execute** (Выполнить).

## <a name="monitor-jobs"></a>Мониторинг заданий
В разделе [кластеры HDInsight управление с помощью веб-интерфейса Ambari hello](hdinsight-hadoop-manage-ambari.md#monitoring).

## <a name="browse-files"></a>Обзор файлов
С помощью hello портал Azure, можно просмотреть содержимое hello контейнера по умолчанию hello.

1. Войдите в слишком[https://portal.azure.com](https://portal.azure.com).
2. Нажмите кнопку **кластеров HDInsight** из hello toolist меню слева hello существующих кластеров.
3. Щелкните имя кластера hello. Если список кластеров hello велик, можно использовать фильтр в hello вверху страницы приветствия.
4. Нажмите кнопку **учетные записи хранения** из меню слева hello кластера.
5. Щелкните учетную запись хранения.
7. Нажмите кнопку hello **большие двоичные объекты** плитки.
8. Щелкните имя контейнера по умолчанию hello.

## <a name="monitor-cluster-usage"></a>Мониторинг использования кластера
Hello **использование** раздел колонка кластера HDInsight hello отображает сведения о hello число ядер подписки tooyour доступны для использования с HDInsight, а также hello количество ядер, выделенных toothis кластера и как они могут выделить для hello узлов на этом кластере. См. раздел [Отображение кластеров](#list-and-show-clusters).

> [!IMPORTANT]
> toomonitor hello службы, предоставляемые hello кластера HDInsight, необходимо использовать Ambari Web или hello Ambari REST API. Дополнительные сведения об использовании Ambari см. в статье [Управление кластерами HDInsight с помощью веб-интерфейса Ambari](hdinsight-hadoop-manage-ambari.md).
>
>

## <a name="connect-tooa-cluster"></a>Подключите кластер tooa

* [Использование Hive с HDInsight](hdinsight-hadoop-use-hive-ambari-view.md)
* [Использование SSH с HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md)

## <a name="next-steps"></a>Дальнейшие действия
Из этой статьи вы узнали о некоторых основных функциях администрирования. toolearn более, см. следующие статьи hello.

* [Администрирование HDInsight с помощью Azure PowerShell](hdinsight-administer-use-powershell.md)
* [Администрирование HDInsight с помощью CLI Azure](hdinsight-administer-use-command-line.md)
* [Создание кластеров HDInsight](hdinsight-hadoop-provision-linux-clusters.md)
* [Использование Hive в HDInsight](hdinsight-use-hive.md)
* [Использование Pig в HDInsight](hdinsight-use-pig.md)
* [Использование Hadoop Sqoop в HDInsight](hdinsight-use-sqoop.md)
* [Начало работы с Azure HDInsight](hdinsight-hadoop-linux-tutorial-get-started.md)
* [Какая версия Hadoop включена в Azure HDInsight?](hdinsight-component-versioning.md)

[azure-portal]: https://portal.azure.com
[image-hadoopcommandline]: ./media/hdinsight-administer-use-portal-linux/hdinsight-hadoop-command-line.png "Командная строка Hadoop"
