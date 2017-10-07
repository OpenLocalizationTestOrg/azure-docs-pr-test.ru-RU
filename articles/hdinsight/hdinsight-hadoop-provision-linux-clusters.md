---
title: "Установка aaaCluster для Hadoop, Spark, Kafka, HBase или R Server - Azure HDInsight | Документы Microsoft"
description: "Настройка кластера Hadoop, Kafka, Spark, HBase, R Server или ураган для HDInsight из браузера, hello Azure CLI, Azure PowerShell, REST или SDK."
keywords: "установка кластера hadoop, установка кластера kafka, установка кластера spark, что такое кластер hadoop"
services: hdinsight
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 23a01938-3fe5-4e2e-8e8b-3368e1bbe2ca
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/06/2017
ms.author: jgao
ms.openlocfilehash: 80ec59d8a39f7fccb940503fd2dc3ae5afee6bcf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-clusters-in-hdinsight-with-hadoop-spark-kafka-and-more"></a>Установка кластеров в HDInsight с использованием Hadoop, Spark, Kafka и других технологий

[!INCLUDE [selector](../../includes/hdinsight-create-linux-cluster-selector.md)]

Узнайте, как tooset и настройке кластеров в HDInsight Hadoop, Spark, Kafka, интерактивный Hive, HBase, R Server, или Storm. Кроме того Узнайте, как кластеры toocustomize и повышают степень безопасности, объединяя их tooa домена.

Кластер Hadoop включает в себя несколько виртуальных машин (узлов), которые используются для распределенной обработки задач. Azure HDInsight обрабатывает сведения о реализации, установки и настройки отдельных узлов, поэтому достаточно tooprovide общих сведений о настройке. 

> [!IMPORTANT]
>Выставление счетов начинается после кластера и останавливается при удалении кластера hello кластера HDInsight. Кластеры оплачиваются поминутно, поэтому всегда следует удалять кластер, когда он больше не нужен. Узнайте, каким образом слишком[удалить кластер.](hdinsight-delete-cluster.md)
>

## <a name="cluster-setup-methods"></a>Способы установки кластера
Hello следующей таблице показаны hello различные методы, которые можно использовать tooset копирование кластера HDInsight.

| Метод создания кластеров | браузер | Команда | Интерфейс REST API | SDK | 
| --- |:---:|:---:|:---:|:---:|
| [Портал Azure](hdinsight-hadoop-create-linux-clusters-portal.md) |✔ |&nbsp; |&nbsp; |&nbsp; |
| [Фабрика данных Azure](hdinsight-hadoop-create-linux-clusters-adf.md) |✔ |✔ |✔ |✔ |
| [Интерфейс командной строки Azure](hdinsight-hadoop-create-linux-clusters-azure-cli.md) |&nbsp; |✔ |&nbsp; |&nbsp; |
| [Azure PowerShell](hdinsight-hadoop-create-linux-clusters-azure-powershell.md) |&nbsp; |✔ |&nbsp; |&nbsp; |
| [cURL](hdinsight-hadoop-create-linux-clusters-curl-rest.md) |&nbsp; |✔ |✔ |&nbsp; |
| [Пакет SDK для .NET](hdinsight-hadoop-create-linux-clusters-dotnet-sdk.md) |&nbsp; |&nbsp; |&nbsp; |✔ |
| [Шаблоны диспетчера ресурсов Azure](hdinsight-hadoop-create-linux-clusters-arm-templates.md) |&nbsp; |✔ |&nbsp; |&nbsp; |

## <a name="quick-create-basic-cluster-setup"></a>Быстрое создание: установка базового кластера
В этой статье описывается настройка в hello [портал Azure](https://portal.azure.com), в котором можно создать кластер HDInsight с помощью *быстрое создание* или *настраиваемый*. 

Следуйте инструкциям на экран приветствия toodo установки базового кластера. Ниже приведены сведения для следующих элементов:

* [Имя группы ресурсов](#resource-group-name)
* [Типы и конфигурация кластеров](#cluster-types) 
* [Имя входа в кластер и имя пользователя SSH](#cluster-login-and-ssh-username)
* [Расположение](#location)

> [!IMPORTANT]
> Linux — hello только операционную систему, используемую в HDInsight версии 3.4 или более поздней. Дополнительные сведения см. в разделе о [прекращении поддержки HDInsight 3.3](hdinsight-component-versioning.md#hdinsight-windows-retirement).
>

## <a name="resource-group-name"></a>Имя группы ресурсов 

[Диспетчер ресурсов Azure](../azure-resource-manager/resource-group-overview.md) упрощает работу с ресурсами hello в приложении как группы, который ссылается tooas группе ресурсов Azure. Можно развернуть, обновления, отслеживания или удалить все ресурсы hello для вашего приложения в рамках одной операции скоординированного.

## <a name="cluster-types"></a> Типы и конфигурация кластеров
Azure HDInsight в настоящее время предоставляют следующие hello кластер типов, каждый ряд компонентов tooprovide определенные функции.

> [!IMPORTANT]
> Доступны различные типы кластеров HDInsight, каждый из которых предназначен для отдельной рабочей нагрузки или технологии. Нет не поддерживаемый метод toocreate кластера, которая объединяет несколько типов, таких как Storm и HBase на один кластер. Если решению требуется технологий, которые распределены по нескольким типам кластера HDInsight, [виртуальной сети Azure](https://docs.microsoft.com/azure/virtual-network) могут подключаться hello необходимые типы кластера. 
>
>

| Тип кластера | Функции |
| --- | --- |
| [Hadoop](hdinsight-hadoop-introduction.md) |Пакетный запрос и анализ хранимых данных |
| [HBase](hdinsight-hbase-overview.md) |Обработка больших объемов данных NoSQL без схемы |
| [Storm](hdinsight-storm-overview.md) |Обработка событий в режиме реального времени |
| [Spark](hdinsight-apache-spark-overview.md) |Обработка в памяти, интерактивные запросы, обработка потоков микро-пакетов |
| [Kafka (предварительная версия)](hdinsight-apache-kafka-introduction.md) | Распределенные потоковой передачи платформу, которая может быть toobuild используется в режиме реального времени потоковой передачи конвейеры данных и приложений |
| [R Server](hdinsight-hadoop-r-server-overview.md) |Разнообразная статистика больших данных, прогнозное моделирование и возможности машинного обучения |
| [Interactive Hive (предварительная версия)](hdinsight-hadoop-use-interactive-hive.md) |Кэширование в памяти для обеспечения интерактивных и ускоренных запросов Hive |

### <a name="number-of-nodes-for-each-cluster-type"></a>Количество узлов для каждого типа кластера
Для каждого типа кластера используется своя терминология. Кроме того, типы отличаются количеством узлов и стандартными размерами виртуальных машин. В следующей таблице hello hello количество узлов для каждого типа узла, указан в скобках.

| Тип | Nodes | Схема |
| --- | --- | --- |
| Hadoop |Головной узел (2), узел данных (от 1) |![Узлы кластера HDInsight Hadoop](./media/hdinsight-hadoop-provision-linux-clusters/hdinsight-hadoop-cluster-type-nodes.png) |
| HBase |Головной сервер (2), региональный сервер (от 1), основной узел или узел Zookeeper (3) |![Узлы кластера HDInsight HBase](./media/hdinsight-hadoop-provision-linux-clusters/hdinsight-hbase-cluster-type-setup.png) |
| Storm |Узел Nimbus (2), сервер супервизора (от 1), узел Zookeeper (3) |![Узлы кластера HDInsight Storm](./media/hdinsight-hadoop-provision-linux-clusters/hdinsight-storm-cluster-type-setup.png) |
| Spark |Головной узел (2), рабочий узел (от 1), узел Zookeeper (3) (кат. "Бесплатный" для размера виртуальной машины Zookeeper A1) |![Узлы кластера HDInsight Spark](./media/hdinsight-hadoop-provision-linux-clusters/hdinsight-spark-cluster-type-setup.png) |

Дополнительные сведения см. в разделе [по умолчанию размеры конфигурации и виртуальной машины узла для кластеров](hdinsight-component-versioning.md#default-node-configuration-and-virtual-machine-sizes-for-clusters) в «Каковы hello Hadoop компоненты и их версии в HDInsight?»

### <a name="hdinsight-version"></a>Версия HDInsight
Выберите версию hello HDInsight для этого кластера. Дополнительные сведения см. в разделе [Поддерживаемые версии HDInsight](hdinsight-component-versioning.md#supported-hdinsight-versions).

### <a name="cluster-tiers"></a>Уровень кластера: уровни обслуживания HDInsight

Azure HDInsight представляет предложения облака hello большие наборы данных на двух уровнях: Standard и Premium.  Дополнительные сведения см. в статье [HDInsight "Стандартный" и HDInsight "Премиум"](hdinsight-component-versioning.md#hdinsight-standard-and-hdinsight-premium).

Hello следующем снимке экрана показано hello Azure портала сведения по выбору типов кластера.

![Конфигурация HDInsight категории "Премиум"](./media/hdinsight-hadoop-provision-linux-clusters/hdinsight-cluster-type-configuration.png)


## <a name="cluster-login-and-ssh-user-name"></a>Имя входа в кластер и имя пользователя SSH
Во время создания кластера HDInsight можно настроить две учетные записи пользователя.

* Пользователь HTTP: имя пользователя по умолчанию hello *администратора*. Основная конфигурация hello используются на hello портал Azure. Иногда его называют "пользователем кластера".
* Пользователь SSH (Linux кластеры): используется tooconnect toohello кластера с помощью SSH. Дополнительные сведения см. в статье [Использование SSH с Hadoop на основе Linux в HDInsight из Linux, Unix или OS X](hdinsight-hadoop-linux-use-ssh-unix.md).

## <a name="location"></a>Расположение (регионы) для кластеров и хранилища

Нет необходимости явно расположение кластера hello toospecify: hello кластер находится в hello местоположения хранения по умолчанию hello. Список поддерживаемых регионов, щелкните hello **область** раскрывающегося списка на [цены на HDInsight](https://go.microsoft.com/fwLink/?LinkID=282635&clcid=0x409).

## <a name="storage-endpoints-for-clusters"></a>Конечные точки хранилища для кластеров

Несмотря на то, что в локальной установке Hadoop используется hello системы распределенных файла Hadoop (HDFS) для хранилища в кластере hello, в облако, использовать конечные точки хранилища в hello подключено toocluster. Для кластеров HDInsight используется [Azure Data Lake Store](hdinsight-hadoop-use-data-lake-store.md) или [BLOB-объекты в службе хранилища Azure](hdinsight-hadoop-use-blob-storage.md). С помощью службы хранилища Azure или хранилища Озера данных означает, что можно безопасно удалить кластеров HDInsight hello, используемый для вычисления, сохранив данные по-прежнему. 

> [!WARNING]
> Использование дополнительная учетная запись хранения в расположении, отличном от hello кластера HDInsight не поддерживается.

Во время настройки для hello конечную точку по умолчанию можно указать контейнер BLOB-объектов учетной записи хранилища Azure или хранилища Озера данных. Hello хранилища по умолчанию содержит узлы приложений и системных журналов. При необходимости можно указать дополнительные связанные учетные записи хранилища Azure и хранилища Озера данных, hello кластера имеет доступ. кластер HDInsight Hello и хранения зависимого приветствия учетные записи должны быть в hello Azure местоположения.

![Параметры хранилища кластера: конечные точки хранилища, совместимые с HDFS](./media/hdinsight-hadoop-provision-linux-clusters/hdinsight-cluster-creation-storage.png)

[!INCLUDE [secure-transfer-enabled-storage-account](../../includes/hdinsight-secure-transfer.md)]


### <a name="optional-metastores"></a>Дополнительные хранилища метаданных
Вы можете создать дополнительные хранилища метаданных Hive или Oozie. Однако не все типы кластеров поддерживают хранилища метаданных, а хранилище данных SQL Azure не совместимо с хранилищами метаданных. 

> [!IMPORTANT]
> При создании пользовательских метахранилище, не используйте дефисы, дефисы и пробелы в имени базы данных hello. Это может привести к toofail процесса создания кластера hello.

### <a name="use-hiveoozie-metastore"></a>Хранилище метаданных Hive

Tooretain таблицах Hive после удаления кластера HDInsight, используйте пользовательские метахранилища. Затем можно присоединить кластер HDInsight tooanother метахранилище hello.

Хранилище метаданных HDInsight, созданное для одной версии кластера HDInsight, не может использоваться в других версиях такого кластера. Список версий HDInsight см. в разделе [Поддерживаемые версии HDInsight](hdinsight-component-versioning.md#supported-hdinsight-versions).

### <a name="oozie-metastore"></a>Хранилище метаданных Oozie

tooincrease производительности при использовании Oozie, используйте пользовательские метахранилища. Метахранилище можно также предоставить доступ к данным задания tooOozie после удаления кластера. 

> [!IMPORTANT]
> Повторно использовать хранилище метаданных Oozie невозможно. toouse пользовательские метахранилище Oozie, укажите пустой базы данных SQL Azure при создании кластера HDInsight hello.

## <a name="configure-cluster-size"></a>Настройка размера кластера

Взимается плата за использование узла, при условии, что существует hello кластера. Выставление счетов начинается сразу после создания кластера и останавливается при удалении кластера hello. Перевести кластер в режим ожидания или отменить его выделение невозможно.

стоимость Hello кластеров HDInsight определяется hello числа узлов и hello размеры виртуальных машин для узлов hello. 

Кластеры разных типов отличаются типами, количеством и размерами узлов.
* Тип кластера Hadoop по умолчанию: 
    * два *головных узла*;  
    * четыре *узла данных*.
* Тип кластера Storm по умолчанию: 
    * два *узла Nimbus*;
    * три *узла ZooKeeper*;
    * четыре *узла супервизора*. 

При пробном использовании HDInsight рекомендуем применять один узел данных. Подробные сведения о ценах на HDInsight см. на [этой странице](https://go.microsoft.com/fwLink/?LinkID=282635&clcid=0x409).

> [!NOTE]
> Hello максимальный размер кластера различается для каждой подписки Azure. Обратитесь к [поддержки по выставлению счетов Azure](https://docs.microsoft.com/azure/azure-supportability/how-to-create-azure-support-request) tooincrease hello ограничение.
>

При использовании кластера hello Azure портала tooconfigure hello размер узла hello доступна через hello **ценовых категорий узла** колонку. На портале hello также видно hello затраты, связанные с размерами hello другой узел. 

![Размеры узла виртуальной машины HDInsight](./media/hdinsight-hadoop-provision-linux-clusters/hdinsight-node-sizes.png)

### <a name="virtual-machine-sizes"></a>Размер виртуальных машин 
При развертывании кластеров выберите вычислительных ресурсов на основе в решение hello планируется toodeploy. Привет, используются следующие виртуальные машины для кластеров HDInsight:
* виртуальные машины серий A и D1–4: [Размеры виртуальных машин Linux общего назначения](https://docs.microsoft.com/azure/virtual-machines/linux/sizes-general);
* виртуальные машины серии D11–14: [Размеры виртуальных машин Linux, оптимизированных для памяти](https://docs.microsoft.com/azure/virtual-machines/linux/sizes-memory).

toofind out значением, которое следует использовать toospecify размер виртуальной Машины при создании кластера с помощью hello разные пакеты SDK, или при использовании Azure PowerShell, в разделе [toouse для кластеров HDInsight размеров виртуальной Машины](../cloud-services/cloud-services-sizes-specs.md#size-tables). В данной статье связанного, используйте значение hello в hello **размер** столбец таблиц hello.

> [!IMPORTANT]
> Если в кластере требуется более 32 рабочих узлов, для головного узла следует выбрать размер с по крайней мере 8 ядрами и 14 ГБ ОЗУ.
>
>

Дополнительные сведения см. в разделе [Размеры виртуальных машин](../virtual-machines/windows/sizes.md). Сведения о стоимости hello разного размера, в разделе [цены на HDInsight](https://azure.microsoft.com/pricing/details/hdinsight).   

## <a name="custom-cluster-setup"></a>Пользовательская установка кластера
Пользовательские кластера установки сборок на hello быстрое создание параметров и добавляет hello следующие параметры:
- [Приложения HDInsight](#hdinsight-applications)
- [Размер кластера](#cluster-size)
- Дополнительные параметры
  - [Действия скриптов](#customize-clusters-using-script-action)
  - [Виртуальная сеть](#use-virtual-network)

## <a name="install-hdinsight-applications-on-clusters"></a>Установка приложений HDInsight в кластерах

Пользователи могут устанавливать приложения HDInsight в кластере HDInsight под управлением Linux. Вы можете использовать приложения, предоставляемые корпорацией Майкрософт, сторонними производителями или разработанные самостоятельно. Дополнительные сведения см. в статье [Установка сторонних приложений Hadoop в Azure HDInsight](hdinsight-apps-install-applications.md).

Большинство приложений HDInsight hello устанавливаются на пустой граничного узла.  Пустой граничного узла — это виртуальная машина Linux с hello же клиентские средства установлен и настроен как hello головного узла. Hello граничного узла можно использовать для доступа к кластеру hello, тестирования клиентские приложения и размещение клиентских приложений. Подробные сведения см. в статье [Использование пустых граничных узлов в HDInsight](hdinsight-apps-use-edge-node.md).

## <a name="advanced-settings-script-actions"></a>Дополнительные параметры: действия скриптов

Можно установить дополнительные компоненты или настроить конфигурацию кластера с помощью сценариев во время создания. Такие сценарии вызываются через **действие сценария**, который имеет параметр конфигурации, который может использоваться с hello портал Azure, командлеты Windows PowerShell для HDInsight или hello HDInsight .NET SDK. Дополнительные сведения см. в статье [Настройка кластеров HDInsight под управлением Linux с помощью действия сценария](hdinsight-hadoop-customize-cluster-linux.md).

Некоторые компоненты собственного Java, например Mahout и каскадных, могут выполняться в кластере hello как файлы архива Java (JAR). Эти файлы JAR может быть распределенное tooAzure хранилища и отправлен tooHDInsight кластеры с механизмами отправки заданий Hadoop. Подробные сведения см. в статье [Отправка заданий Hadoop в HDInsight](hdinsight-submit-hadoop-jobs-programmatically.md).

> [!NOTE]
> При наличии проблем развертывание кластеров tooHDInsight файлы JAR-ФАЙЛ, или вызов JAR-файлов в кластерах HDInsight, обратитесь к [поддержки Майкрософт](https://azure.microsoft.com/support/options/).
>
> Компонент Cascading не поддерживается службой HDInsight и на него не распространяется техническая поддержка Майкрософт. Список поддерживаемых компонентов см [новые возможности, предоставляемые HDInsight версии кластера hello](hdinsight-component-versioning.md).
>
>

В некоторых случаях требуется hello tooconfigure следующие файлы конфигурации во время процесса создания hello:

* clusterIdentity.xml
* core-site.xml
* gateway.xml
* hbase-env.xml
* hbase-site.xml
* hdfs-site.xml
* hive-env.xml
* hive-site.xml
* mapred-site
* oozie-site.xml
* oozie-env.xml
* storm-site.xml
* tez-site.xml
* webhcat-site.xml
* yarn-site.xml

Подробные сведения см. в статье [Настройка кластеров HDInsight с помощью начальной загрузки](hdinsight-hadoop-customize-cluster-bootstrap.md).

## <a name="advanced-settings-extend-clusters-with-a-virtual-network"></a>Дополнительные параметры: расширение кластеров с помощью виртуальной сети
Если решению требуется технологий, которые распределены по нескольким типам кластера HDInsight, [виртуальной сети Azure](https://docs.microsoft.com/azure/virtual-network) могут подключаться hello необходимые типы кластера. Эта конфигурация позволяет кластеров hello и любой код, развертывание toothem, toodirectly взаимодействовать друг с другом.

Подробные сведения об использовании виртуальных сетей Azure в HDInsight см. в статье [Расширение возможностей HDInsight с помощью виртуальной сети Azure](hdinsight-extend-hadoop-virtual-network.md).

Пример использования двух типов кластера в виртуальной сети Azure см. в статье об [анализе данных с датчиков с использованием Storm и HBase](hdinsight-storm-sensor-data-analysis.md). Дополнительные сведения об использовании HDInsight с помощью виртуальной сети, включая требования к конфигурации для hello виртуальной сети, в разделе [HDInsight расширить возможности с помощью виртуальной сети Azure](hdinsight-extend-hadoop-virtual-network.md).

## <a name="troubleshoot-access-control-issues"></a>Устранение неполадок управления доступом

Если при создании кластеров HDInsight возникли проблемы, см. раздел [Создание кластеров](hdinsight-administer-use-portal-linux.md#create-clusters).

## <a name="next-steps"></a>Дальнейшие действия

- [Что такое HDInsight Hadoop экосистема hello и кластеров Hadoop](hdinsight-hadoop-introduction.md)
- [Руководство по Hadoop. Приступая к работе с Hadoop в HDInsight](hdinsight-hadoop-linux-tutorial-get-started.md)
- [Работа в экосистеме Hadoop в HDInsight на компьютере с Windows](hdinsight-hadoop-windows-tools.md)
