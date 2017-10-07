---
title: "кластеры aaaUse hello Azure toocreate портала Azure HDInsight с хранилища Озера данных | Документы Microsoft"
description: "Использовать hello Azure toocreate портала и использовать кластерами HDInsight в хранилище Озера данных Azure"
services: data-lake-store,hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: a8c45a83-a8e3-4227-8b02-1bc1e1de6767
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/14/2017
ms.author: nitinme
ms.openlocfilehash: f23113d444a3c5a01894dba29f75f3621b2d16bd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-hdinsight-clusters-with-data-lake-store-by-using-hello-azure-portal"></a>Создание кластеров HDInsight с хранилища Озера данных с помощью портала Azure hello
> [!div class="op_single_selector"]
> * [Использовать hello портал Azure](data-lake-store-hdinsight-hadoop-use-portal.md)
> * [Использование PowerShell (для хранилища по умолчанию)](data-lake-store-hdinsight-hadoop-use-powershell-for-default-storage.md)
> * [Использование PowerShell (для дополнительного хранилища)](data-lake-store-hdinsight-hadoop-use-powershell.md)
> * [Использование Resource Manager](data-lake-store-hdinsight-hadoop-use-resource-manager-template.md)
>
>

Узнайте, как toouse hello Azure портала toocreate кластера HDInsight с помощью учетной записи хранилища Озера данных Azure как хранилища по умолчанию hello или дополнительное хранилище. Несмотря на то, что дополнительное хранилище является обязательным для кластера HDInsight, рекомендуется toostore бизнес-данных в hello дополнительные учетные записи хранения.

## <a name="prerequisites"></a>Предварительные требования
Прежде чем начать работу с учебником, убедитесь, что соблюдены следующие требования к hello:

* **Подписка Azure**. Go слишком[получить бесплатная пробная версия](https://azure.microsoft.com/pricing/free-trial/).
* **Учетная запись Azure Data Lake Store.** Следуйте инструкциям hello из [Приступая к работе с хранилища Озера данных Azure с помощью портала Azure hello](data-lake-store-get-started-portal.md). Необходимо также создать корневую папку на hello учетной записи.  В этом учебнике используется корневая папка __/clusters__.
* **Субъект-служба Azure Active Directory**. Этот учебник содержит инструкции о том, как toocreate участника службы в Azure Active Directory (Azure AD). Однако toocreate участника службы, необходимо быть администратором Azure AD. Если вы являетесь администратором, можно пропустить это предварительное условие и продолжить работу с учебником hello.

    >[!NOTE]
    >Создать субъект-службу может только администратор Azure AD. Администратор Azure AD должен сначала создать субъект-службу, после чего вы сможете создать кластер HDInsight, использующий Data Lake Store. Кроме того, hello участника-службы должны создаваться с помощью сертификата, как описано в разделе [создании участника службы с сертификатом](../azure-resource-manager/resource-group-authenticate-service-principal.md#create-service-principal-with-self-signed-certificate).
    >

## <a name="create-an-hdinsight-cluster"></a>Создание кластера HDInsight

В этом разделе создается кластер HDInsight с учетными записями хранилища Озера данных по умолчанию hello или hello дополнительное хранилище. В этой статье описываются только hello при настройке учетных записей хранилища Озера данных.  Hello общие кластера создания сведения и процедуры см. в разделе [кластеров создать Hadoop в HDInsight](../hdinsight/hdinsight-hadoop-provision-linux-clusters.md).

### <a name="create-a-cluster-with-data-lake-store-as-default-storage"></a>Создание кластера HDInsight, использующего Data Lake Store в качестве хранилища по умолчанию

**toocreate HDInsight кластера хранилище Озера данных в качестве учетной записи хранения по умолчанию hello**

1. Войдите в toohello [портал Azure](https://portal.azure.com).
2. Выполните [создавать кластеры](../hdinsight/hdinsight-hadoop-create-linux-clusters-portal.md#create-clusters) hello Общие сведения о создании кластеров HDInsight.
3. На hello **хранения** колонки в разделе **тип основного хранилища**выберите **хранилища Озера данных**и введите следующую информацию hello:

    ![Добавить службы основной tooHDInsight кластера](./media/data-lake-store-hdinsight-hadoop-use-portal/hdi.adl.1.adls.storage.png "добавить службы основной tooHDInsight кластера")

    - **Выбрать учетную запись Data Lake Store**: выберите существующую учетную запись Data Lake Store. Требуется существующая учетная запись Data Lake Store.  См. раздел [Предварительные требования](#prereuisites).
    - **Путь к корневому каталогу**: Введите путь, в которых toobe хранимых файлов, относящихся к кластеру hello. На снимке экрана приветствия, это __/кластеры/myhdiadlcluster/__, в какие hello __/кластеры__ папка должна существовать и hello портал создает *myhdicluster* папки.  Hello *myhdicluster* — имя кластера hello.
    - **Доступ к хранилищу Озера данных**: настроить доступ между учетной записи хранилища Озера данных hello и кластера HDInsight. Инструкции см. в разделе [Настройка доступа к Data Lake Store](#configure-data-lake-store-access).
    - **Дополнительные учетные записи хранения**: Добавление учетных записей хранения Azure как дополнительное хранилище учетных записей для hello кластера. tooadd дополнительных хранилища Озера данных выполняется путем предоставления hello кластера разрешения на данные в несколько учетных записей хранилища Озера данных при настройке учетной записи хранилища Озера данных как тип основного хранилища hello. См. раздел [Настройка доступа к Data Lake Store](#configure-data-lake-store-access).

4. На hello **доступ к хранилищу Озера данных**, нажмите кнопку **выберите**, а затем продолжите создание кластера, как описано в [кластеров создать Hadoop в HDInsight](../hdinsight/hdinsight-hadoop-create-linux-clusters-portal.md).


### <a name="create-a-cluster-with-data-lake-store-as-additional-storage"></a>Создание кластера HDInsight, использующего Data Lake Store в качестве дополнительного хранилища

Hello следующие инструкции создание кластера HDInsight с учетная запись хранилища Azure в качестве хранилища по умолчанию hello и учетную запись хранилища Озера данных как дополнительное хранилище.
**toocreate HDInsight кластера хранилище Озера данных в качестве учетной записи хранения по умолчанию hello**

1. Войдите в toohello [портал Azure](https://portal.azure.com).
2. Выполните [создавать кластеры](../hdinsight/hdinsight-hadoop-create-linux-clusters-portal.md#create-clusters) hello Общие сведения о создании кластеров HDInsight.
3. На hello **хранилища** колонки в разделе **тип основного хранилища**выберите **хранилища Azure**и введите hello следующую информацию:

    ![Добавить службы основной tooHDInsight кластера](./media/data-lake-store-hdinsight-hadoop-use-portal/hdi.adl.1.png "добавить службы основной tooHDInsight кластера")

    - **Метод выбора**: используйте один из следующих вариантов hello:

        * Выберите toospecify учетной записи хранилища, который является частью вашей подписке Azure **Мои подписки**, а затем выберите учетную запись хранения hello.
        * toospecify учетной записи хранилища, который находится за пределами вашей подписке Azure, выберите **ключ доступа**, а затем введите данные hello для hello за пределами учетной записи хранилища.

    - **Контейнер по умолчанию**: использовать либо значение по умолчанию hello или задать собственное имя.

    - Дополнительные учетные записи хранения: добавить несколько учетных записей хранилища Azure в качестве дополнительного хранилища hello.
    - Доступ к хранилищу Озера данных: настроить доступ между учетной записи хранилища Озера данных hello и кластера HDInsight. Инструкции см. в разделе [Настройка доступа к Data Lake Store](#configure-data-lake-store-access).

## <a name="configure-data-lake-store-access"></a>Настройка доступа к Data Lake Store 

В этом разделе вы настроите доступ к Data Lake Store из кластеров HDInsight с помощью субъекта-службы Azure Active Directory. 

### <a name="specify-a-service-principal"></a>Указание субъекта-службы

Из hello портал Azure можно использовать существующий субъект-служба или создайте новую.

**toocreate участника службы из hello портал Azure**

1. Нажмите кнопку **доступ к хранилищу Озера данных** из колонки hello хранилища.
2. На hello **доступ к хранилищу Озера данных** колонка, щелкните **создать новый**.
3. Нажмите кнопку **участника-службы**, а затем выполните инструкции hello toocreate участника службы.
4. Загрузите сертификат hello в том случае, если вы решите toouse его снова в будущем hello. Загрузка hello сертификат полезен, если требуется toouse hello же служба участника при создании дополнительных кластеров HDInsight.

    ![Добавить службы основной tooHDInsight кластера](./media/data-lake-store-hdinsight-hadoop-use-portal/hdi.adl.2.png "добавить службы основной tooHDInsight кластера")

4. Нажмите кнопку **доступа** доступ к папке tooconfigure hello.  См. раздел [Настройка разрешений для файлов](#configure-file-permissions).


**toouse существующий субъект-службу из hello портал Azure**

1. Щелкните **Доступ к Data Lake Store**.
1. На hello **доступ к хранилищу Озера данных** колонка, щелкните **использовать существующие**.
2. Щелкните **Субъект-служба**, а затем выберите субъект-службу. 
3. Отправка hello сертификата (PFX-файл), связанной с участниками выбранные службы, а затем введите пароль сертификата hello.

    ![Добавить службы основной tooHDInsight кластера](./media/data-lake-store-hdinsight-hadoop-use-portal/hdi.adl.5.png "добавить службы основной tooHDInsight кластера")

4. Нажмите кнопку **доступа** доступ к папке tooconfigure hello.  См. раздел [Настройка разрешений для файлов](#configure-file-permissions).


### <a name="configure-file-permissions"></a>Настройка разрешений для файлов

Настраивает Hello различаются в зависимости от того, было ли hello будут использоваться в качестве хранилища по умолчанию hello или дополнительная учетная запись хранения:

- В качестве хранилища по умолчанию:

    - разрешение на корневом уровне hello hello хранилища Озера данных
    - разрешение на корневом уровне hello hello хранения данных кластера HDInsight. Например, hello __/кластеры__ папки, используемой ранее в учебнике hello.
- В качестве дополнительного хранилища:

    - Разрешения на папки hello, где вам требуется доступ к файлам.

**разрешение tooassign во hello корневого уровня учетной записи хранилища Озера данных**

1. На hello **доступ к хранилищу Озера данных** колонка, щелкните **доступа**. Hello **выберите разрешения для файлов** открыть колонку. В нем перечислены все учетные записи хранилища Озера данных hello в вашей подписке.
2. Наведите указатель мыши (не выбирайте) hello при наведении hello имя hello toomake hello флажок отображается, а затем выберите hello флажок учетной записи хранилища Озера данных.

    ![Добавить службы основной tooHDInsight кластера](./media/data-lake-store-hdinsight-hadoop-use-portal/hdi.adl.3.png "добавить службы основной tooHDInsight кластера")

  По умолчанию выбраны разрешения __Чтение__, __Запись__ и __Выполнение__.

3. Нажмите кнопку **выберите** hello нижней части страницы приветствия.
4. Нажмите кнопку **запуска** tooassign разрешение.
5. Нажмите кнопку **Done**(Готово).

**tooassign разрешение на уровне корневого кластера HDInsight hello**

1. На hello **доступ к хранилищу Озера данных** колонка, щелкните **доступа**. Hello **выберите разрешения для файлов** открыть колонку. В нем перечислены все учетные записи хранилища Озера данных hello в вашей подписке.
1. Из hello **выберите разрешения для файлов** колонка, щелкните имя tooshow hello хранилища Озера данных его содержимого.
2. Выберите корневого хранилища кластера HDInsight hello, установив флажок hello слева hello hello папки. В соответствии с toohello экрана выше, — корневого хранилища кластера hello __/кластеры__ папки, заданной при выделении хранилища Озера данных hello хранения по умолчанию.
3. Задать hello разрешения на папку hello.  По умолчанию выбраны разрешения на чтение, запись и выполнение.
4. Нажмите кнопку **выберите** hello нижней части страницы приветствия.
5. Щелкните **Выполнить**.
6. Нажмите кнопку **Done**(Готово).

При использовании хранилища Озера данных как дополнительное хранилище, необходимо назначить разрешение только для папок hello, которые должны tooaccess из кластера HDInsight hello. Например, в следующем снимке экрана приветствия, вы предоставляете доступ только слишком**hdiaddonstorage** папки в учетной записи хранилища Озера данных.

![Назначить кластер HDInsight toohello разрешения участника службы](./media/data-lake-store-hdinsight-hadoop-use-portal/hdi.adl.3-1.png "кластера HDInsight toohello разрешения участника службы Assign")


## <a name="verify-cluster-set-up"></a>Проверка настроек кластера

По завершении установки кластера hello в колонке кластера hello, проверьте результаты, выполнив одной или обеих hello следующие шаги:

* tooverify hello хранилища для кластера hello hello хранилища Озера данных указанной учетной записи, нажмите кнопку **учетные записи хранения** hello левой панели.

    ![Добавить службы основной tooHDInsight кластера](./media/data-lake-store-hdinsight-hadoop-use-portal/hdi.adl.6-1.png "добавить службы основной tooHDInsight кластера")

* tooverify, hello участника-службы был правильно связан с кластером HDInsight hello, щелкните **доступ к хранилищу Озера данных** hello левой панели.

    ![Добавить службы основной tooHDInsight кластера](./media/data-lake-store-hdinsight-hadoop-use-portal/hdi.adl.6.png "добавить службы основной tooHDInsight кластера")


## <a name="examples"></a>Примеры

После настройки кластера hello с хранилища Озера данных как жесткие диски, см. Примеры toothese как toouse HDInsight кластера tooanalyze hello данные, которые хранятся в хранилище Озера данных.

### <a name="run-a-hive-query-against-data-in-a-data-lake-store-as-primary-storage"></a>Выполнение запроса Hive к данным, хранящимся в Data Lake Store (основное хранилище)

toorun запрос Hive с помощью интерфейса представления Hive hello hello Ambari портала. Инструкции по способ представления toouse Ambari куста см [hello используйте представление Hive с Hadoop в HDInsight](../hdinsight/hdinsight-hadoop-use-hive-ambari-view.md).

При работе с данными в хранилище Озера данных, существует несколько toochange строк.

При использовании, например, созданный с помощью хранилища Озера данных в качестве основного хранилища, кластер hello hello путь toohello данные являются: *adl: / / < data_lake_store_account_name > /azuredatalakestore.net/path/to/file*. Запрос Hive toocreate таблицу из образца данных, хранящихся в hello хранилища Озера данных выглядит следующим образом hello, следующем за инструкцией.

    CREATE EXTERNAL TABLE websitelog (str string) LOCATION 'adl://hdiadlsstorage.azuredatalakestore.net/clusters/myhdiadlcluster/HdiSamples/HdiSamples/WebsiteLogSampleData/SampleLog/'

Описание
* `adl://hdiadlstorage.azuredatalakestore.net/`— основной hello hello хранилища Озера данных.
* `/clusters/myhdiadlcluster`— основной hello hello данных кластера, указанный при создании кластера hello.
* `/HdiSamples/HdiSamples/WebsiteLogSampleData/SampleLog/`— местоположение hello hello пример файла, который используется в запросе hello.

### <a name="run-a-hive-query-against-data-in-a-data-lake-store-as-additional-storage"></a>Выполнение запроса Hive к данным, хранящимся в Data Lake Store (дополнительное хранилище)

Если созданный hello кластер использует хранилище больших двоичных объектов хранения по умолчанию, образец данных hello не содержится в hello учетной записи хранилища Озера данных Azure, которая используется в качестве дополнительного хранилища. В этом случае сначала перенести данные hello из toohello хранилища больших двоичных объектов хранилища Озера данных и затем выполняются запросы hello, как показано в предшествующих пример hello.

Сведения о как toocopy из BLOB-хранилища Озера данных tooa хранилище данных см. следующие статьи hello:

* [Использовать данные toocopy Distcp между BLOB-объектов хранилища Azure и хранилища Озера данных](data-lake-store-copy-data-wasb-distcp.md)
* [Использовать AdlCopy toocopy данные из хранилища Azure BLOB-объектов хранилища Озера tooData](data-lake-store-copy-data-azure-storage-blob.md)

### <a name="use-data-lake-store-with-a-spark-cluster"></a>Использование Data Lake Store с кластером Spark
Toorun Spark Spark кластерных заданий можно использовать для данных, которые хранятся в хранилище Озера данных. Дополнительные сведения см. в разделе [данные tooanalyze кластера HDInsight Spark использования хранилища Озера данных](../hdinsight/hdinsight-apache-spark-use-with-data-lake-store.md).


### <a name="use-data-lake-store-in-a-storm-topology"></a>Использование хранилища озера данных в топологии Storm
Можно использовать данные toowrite hello хранилища Озера данных из топологии Storm. Инструкции по tooachieve этот сценарий в разделе [использования хранилища Озера данных Azure с помощью Apache Storm с HDInsight](../hdinsight/hdinsight-storm-write-data-lake-store.md).

## <a name="see-also"></a>См. также
* [PowerShell: Создание toouse кластера HDInsight хранилища Озера данных](data-lake-store-hdinsight-hadoop-use-powershell.md)

[makecert]: https://msdn.microsoft.com/library/windows/desktop/ff548309(v=vs.85).aspx
[pvk2pfx]: https://msdn.microsoft.com/library/windows/desktop/ff550672(v=vs.85).aspx
