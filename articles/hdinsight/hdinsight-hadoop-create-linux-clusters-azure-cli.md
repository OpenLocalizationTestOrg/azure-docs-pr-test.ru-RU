---
title: "с помощью командной строки - hello Azure HDInsight кластеров Hadoop aaaCreate | Документы Microsoft"
description: "Узнайте, как с помощью кластеров HDInsight toocreate hello кросс платформенных Azure CLI 1.0."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 50b01483-455c-4d87-b754-2229005a8ab9
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/26/2017
ms.author: larryfr
ms.openlocfilehash: 5295b01054b8c23df0e3b75a3e0e8c933ac48b3c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-hdinsight-clusters-using-hello-azure-cli"></a>Создать кластеры HDInsight с помощью hello Azure CLI

[!INCLUDE [selector](../../includes/hdinsight-create-linux-cluster-selector.md)]

Hello шагов этого пошагового руководства документа, для создания кластера HDInsight 3.5 с помощью hello Azure CLI 1.0.

> [!IMPORTANT]
> Linux — hello только операционную систему, используемую в HDInsight версии 3.4 или более поздней. Дополнительные сведения см. в разделе [Приближается дата прекращения сопровождения HDI версии 3.3](hdinsight-component-versioning.md#hdinsight-windows-retirement).


## <a name="prerequisites"></a>Предварительные требования

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

* **Подписка Azure**. См. страницу [бесплатной пробной версии Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).

* **Azure CLI**. Hello в данном пошаговом руководстве последнего были протестированы с Azure CLI версии 0.10.14.

    > [!IMPORTANT]
    > Hello в данном пошаговом руководстве не работают с Azure CLI версии 2.0. Azure CLI 2.0 не поддерживает создание кластера HDInsight.

## <a name="log-in-tooyour-azure-subscription"></a>Войдите в tooyour подписки Azure

Выполните hello шагов, описанных в [подключение tooan подписки Azure из hello Azure командной строки (CLI Azure)](../xplat-cli-connect.md) и подключите tooyour подписку, используя hello **входа** метод.

## <a name="create-a-cluster"></a>Создание кластера

Привет, следующие шаги необходимо выполнить из командной строки, например PowerShell или Bash.

1. Используйте hello следующая команда tooauthenticate tooyour подписки Azure:

        azure login

    Вы являются запрашиваемые tooprovide свое имя и пароль. Если у вас несколько подписок Azure, используйте `azure account set <subscriptionname>` tooset hello подписку, которая hello Azure CLI команды используют.

2. Переключение режима tooAzure диспетчера ресурсов, с помощью hello следующую команду:

        azure config mode arm

3. Создайте группу ресурсов. Эта группа ресурсов содержит кластер HDInsight hello и соответствующие учетной записи хранилища.

        azure group create groupname location

    * Замените `groupname` уникальное имя для группы hello.

    * Замените `location` с hello географический регион, вы должны быть toocreate hello группы.

       Список допустимых местах, использовать hello `azure location list` команды, а затем использовать одно из местоположений hello из hello `Name` столбца.

4. Создайте учетную запись хранения. Эта учетная запись хранения служит hello хранилища по умолчанию для кластера HDInsight hello.

        azure storage account create -g groupname --sku-name RAGRS -l location --kind Storage storagename

    * Замените `groupname` с именем hello hello группы, созданной в предыдущем шаге hello.

    * Замените `location` с hello местоположения, используемый в предыдущем шаге hello.

    * Замените `storagename` уникальное имя для учетной записи хранения hello.

        > [!NOTE]
        > Дополнительные сведения о параметрах hello, использованный в этой команде используется `azure storage account create -h` tooview справку для этой команды.

5. Получить учетную запись хранения hello ключа используется tooaccess hello.

        azure storage account keys list -g groupname storagename

    * Замените `groupname` с hello имя группы ресурсов.
    * Замените `storagename` с именем hello hello учетной записи хранения.

     В возвращаемых данных hello, сохранить hello `key` значение `key1`.

6. Создание кластера HDInsight.

        azure hdinsight cluster create -g groupname -l location -y Linux --clusterType Hadoop --defaultStorageAccountName storagename.blob.core.windows.net --defaultStorageAccountKey storagekey --defaultStorageContainer clustername --workerNodeCount 3 --userName admin --password httppassword --sshUserName sshuser --sshPassword sshuserpassword clustername

    * Замените `groupname` с hello имя группы ресурсов.

    * Замените `Hadoop` с типом кластера hello, что вы хотите toocreate. Примеры: `Hadoop`, `HBase`, `Kafka`, `Spark` или `Storm`.

     > [!IMPORTANT]
     > HDInsight кластеров поставляются в различных типов, которые соответствуют toohello рабочей нагрузки или технология, которая hello кластера настроена для работы. Нет не поддерживаемый метод toocreate кластера, которая объединяет несколько типов, таких как Storm и HBase на один кластер.

    * Замените `location` с hello местоположения, используемый в предыдущих шагах.

    * Замените `storagename` на имя учетной записи хранения hello.

    * Замените `storagekey` с hello ключ, полученный в предыдущем шаге hello.

    * Для hello `--defaultStorageContainer` параметр, используйте hello точно такое же имя, как вы используете для кластера hello.

    * Замените `admin` и `httppassword` hello имя и пароль вы хотите toouse при доступе к hello кластера по протоколу HTTPS.

    * Замените `sshuser` и `sshuserpassword` hello имя пользователя и пароль при доступе к hello кластера с помощью SSH требуется toouse

    > [!IMPORTANT]
    > Этот пример создает кластер с 2 рабочими узлами. После создания кластера можно также изменить hello число рабочих узлов, выполняя операции масштабирования. Если вы планируете использовать более 32 рабочих узлов, для головного узла необходимо выбрать по крайней мере 8-ядерный процессор и 14 ГБ ОЗУ. Можно задать размер hello головного узла с помощью hello `--headNodeSize` параметра во время создания кластера.
    >
    > Дополнительные сведения о размерах узлов и их стоимости см. на странице с [ценами на HDInsight](https://azure.microsoft.com/pricing/details/hdinsight/).

    Он может занять несколько минут для toofinish процесса создания кластера hello. обычно около 15 минут.

## <a name="troubleshoot"></a>Устранение неполадок

Если при создании кластеров HDInsight возникли проблемы, см. раздел [Создание кластеров](hdinsight-administer-use-portal-linux.md#create-clusters).

## <a name="next-steps"></a>Дальнейшие действия

Теперь, когда кластер HDInsight с помощью Azure CLI hello успешно создана, использовать как следующая toolearn hello toowork с кластером:

### <a name="hadoop-clusters"></a>Кластеры Hadoop

* [Использование Hive с HDInsight](hdinsight-use-hive.md)
* [Использование Pig с HDInsight](hdinsight-use-pig.md)
* [Использование MapReduce с HDInsight](hdinsight-use-mapreduce.md)

### <a name="hbase-clusters"></a>Кластеры HBase

* [Начало работы с HBase в HDInsight](hdinsight-hbase-tutorial-get-started-linux.md)
* [Разработка приложений Java для HBase в HDInsight](hdinsight-hbase-build-java-maven-linux.md)

### <a name="storm-clusters"></a>Кластеры Storm

* [Разработка приложений Java для Storm в HDInsight](hdinsight-storm-develop-java-topology.md)
* [Использование компонентов Python в Storm в HDInsight](hdinsight-storm-develop-python-topology.md)
* [Развертывание и мониторинг топологий с помощью Storm в HDInsight](hdinsight-storm-deploy-monitor-topology-linux.md)
