---
title: "aaaCreate Hadoop кластеры, использующие веб-браузер - Azure HDInsight | Документы Microsoft"
description: "Узнайте, как toocreate Hadoop, HBase, ураган или Spark кластеров в Linux для HDInsight с помощью веб-браузер и hello портал предварительной версии Azure."
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 697278cf-0032-4f7c-b9b2-a84c4347659e
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: 63027e35e2d66dd76218aff3e0c085fc811736ec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-linux-based-clusters-in-hdinsight-using-hello-azure-portal"></a>Создавать кластеры под управлением Linux в HDInsight с помощью портала Azure hello
[!INCLUDE [selector](../../includes/hdinsight-create-linux-cluster-selector.md)]

Hello портал Azure — это средство управления веб-служб и приложений, размещенных в облаке Microsoft Azure hello. В этой статье вы узнаете, как кластеры с помощью портала hello toocreate HDInsight под управлением Linux.

## <a name="prerequisites"></a>Предварительные требования
[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

* **Подписка Azure**. Ознакомьтесь с [бесплатной пробной версией Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).
* **Современный браузер**. Здравствуйте портал Azure использует HTML5 и Javascript и может работать неправильно в старых браузерах.

## <a name="create-clusters"></a>Создание кластеров
Hello портал Azure предоставляет доступ к большинству hello свойства кластера. С помощью шаблона Azure Resource Manager можно скрыть много сведений. Дополнительные сведения см. в статье [Создание кластеров Hadoop под управлением Linux в HDInsight с помощью шаблонов Azure Resource Manager](hdinsight-hadoop-create-linux-clusters-arm-templates.md).

[!INCLUDE [secure-transfer-enabled-storage-account](../../includes/hdinsight-secure-transfer.md)]


1. Войдите в toohello [портал Azure](https://portal.azure.com).
2. Щелкните **+**, **Аналитика**, а затем — **HDInsight**.
   
    ![Создание нового кластера в hello портал Azure](./media/hdinsight-hadoop-create-linux-cluster-portal/hdinsight-create-cluster.png "для создания нового кластера в hello портал Azure")

3. В hello **HDInsight** колонка, щелкните **Custom (размер, параметры, приложения)**, нажмите кнопку **основы**и введите следующую информацию hello.

    ![Создание нового кластера в hello портал Azure](./media/hdinsight-hadoop-create-linux-cluster-portal/hdinsight-create-cluster-basics.png "для создания нового кластера в hello портал Azure")

    * Введите **имя кластера**: оно должно быть глобально уникальным.

    * Из hello **подписки** hello раскрывающийся список, выберите подписку Azure, которая будет использоваться для кластера hello.

    * Щелкните **Тип кластера**, а затем выберите следующие значения:
   
        * **Тип кластера**: Если вы не знаете, какие toochoose, выберите **Hadoop**. Это наиболее популярных кластера типа hello.
     
            > [!IMPORTANT]
            > HDInsight кластеров поставляются в различных типов, которые соответствуют toohello рабочей нагрузки или технология, которая hello кластера настроена для работы. Нет не поддерживаемый метод toocreate кластера, которая объединяет несколько типов, таких как Storm и HBase на один кластер. 
            > 
            > 
        
        * **Операционная система**: выберите значение **Linux**.
        
        * **Версия**: использовать версию по умолчанию hello, если вы не знаете, какие toochoose. Дополнительные сведения см. в статье [Что представляют собой различные компоненты Hadoop, доступные в HDInsight?](hdinsight-component-versioning.md)
        * **Кластер уровня**: Azure HDInsight представляет предложения облака hello большие наборы данных в двух категориях: уровней Standard и Premium. Дополнительные сведения см. в разделе [Уровни кластера](hdinsight-hadoop-provision-linux-clusters.md#cluster-tiers).

    * Для **пользователя для входа кластер** и **входа пароль кластера**, укажите имя пользователя hello и пароль для пользователя с правами администратора hello.

    * Введите **имя пользователя SSH** и toohave hello SSH пароля, аналогично hello пароль администратора, указанный ранее, установите hello **использовать одинаковый пароль в качестве учетной записи кластера** флажок. Если нет, можно задать только одно **пароль** или **ОТКРЫТЫЙ ключ**, который будет использоваться tooauthenticate hello SSH пользователь. С помощью открытого ключа — hello рекомендованный подход. Нажмите кнопку **выберите** в hello нижней toosave hello учетные данные конфигурации.
   
        См. дополнительные сведения об [использовании SSH в HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).

    * Для **группы ресурсов**, укажите ли вы, чтобы toocreate новую группу ресурсов или используйте существующую.

    * Укажите центр обработки данных **расположение** где будет создан кластер hello.

    * Щелкните **Далее**.

4. На hello **хранения** колонки, укажите, должен ли хранилища Azure (WASB) или хранилища Озера данных в хранилище по умолчанию. Рассмотрим таблицу hello ниже для получения дополнительной информации.

    ![Создание нового кластера в hello портал Azure](./media/hdinsight-hadoop-create-linux-cluster-portal/hdinsight-create-cluster-storage.png "для создания нового кластера в hello портал Azure")

    | Хранилище                                      | Описание |
    |----------------------------------------------|-------------|
    | **Большие двоичные объекты службы хранилища Azure как хранилище по умолчанию**   | <ul><li>В разделе **Тип первичного хранилища** выберите **Служба хранилища Azure**. После этого для **метод выбора**, вы можете **Мои подписки** следует toospecify учетной записи хранилища, который является частью вашей подписке Azure и hello, а затем выберите учетную запись хранения. В противном случае нажмите кнопку **ключ доступа** и заполнить hello hello хранилища учетной записи, которую toochoose из за пределами вашей подписке Azure.</li><li>Для **контейнер по умолчанию**, можно выбрать toogo с именем контейнера по умолчанию hello, предложенными hello портала или указать собственный.</li><li>При использовании WASB хранения по умолчанию (необязательно) можно щелкнуть **дополнительных учетных записей хранилища** toospecify дополнительных учетных записей хранения tooassociate с кластером hello. В hello **хранилища ключей Azure** колонка, щелкните **добавить ключ хранилища**, и затем можно задать учетную запись хранилища в подписках Azure или из других подписок (за счет hello учетной записи хранилища ключ доступа).</li><li>При использовании WASB хранения по умолчанию (необязательно) можно щелкнуть **доступ к хранилищу Озера данных** toospecify хранилища Озера данных Azure как дополнительное хранилище. Подробные сведения см. в статье [Создание кластера HDInsight с хранилищем озера данных с помощью портала Azure](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md).</li></ul> |
    | **Azure Data Lake Store как хранилище по умолчанию** | Для **тип основного хранилища**выберите **хранилища Озера данных** и затем см. в статье toohello [создать кластер HDInsight в хранилище Озера данных с помощью портала Azure](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md) для инструкции. |
    | **Внешние хранилища метаданных**                      | Кроме того можно указать SQL базы данных toosave Hive и Oozie метаданные, связанные с кластером hello. Для **выберите базу данных SQL для куста** выберите базу данных SQL, а затем укажите hello имя пользователя и пароль для базы данных hello. Повторите эти действия для метаданных Oozie.<br><br>Важные особенности при использовании базы данных Azure SQL для хранилищ метаданных. <ul><li>базы данных Azure SQL Hello, используемой для hello метахранилище должны разрешать подключения tooother служб Azure, включая Azure HDInsight. На мониторинга базы данных Azure SQL hello hello правой стороны щелкните имя сервера hello. Это hello сервер, на какие hello SQL выполняется экземпляр базы данных. После установки на представление hello server нажмите кнопку **Настройка**, а затем для **служб Azure**, нажмите кнопку **Да**и нажмите кнопку **Сохранить**.</li><li>При создании метахранилище, не следует использовать имя базы данных, содержащую тире или дефиса, как это может привести к toofail процесса создания кластера hello.</li></ul>                                                                                                                                                                       |

    Щелкните **Далее**. 

    > [!WARNING]
    > С использованием учетной записи дополнительный объем хранилища в другом месте, чем hello кластера HDInsight не поддерживается.

5. При необходимости щелкните **приложений** tooinstall приложений, работающих с кластерами HDInsight. Разработчиками этих приложений могут быть корпорация Майкрософт, независимые поставщики программного обеспечения или вы сами. Дополнительные сведения см. в разделе [Установка приложений HDInsight](hdinsight-apps-install-applications.md#install-applications-during-cluster-creation).


6. Нажмите кнопку **размер кластера** toodisplay сведения об узлах hello, которые будут созданы для этого кластера. Задайте hello количество рабочих узлов, необходимое для hello кластера. Hello оценочная стоимость hello кластера будет отображаться в колонке hello.
   
    ![Колонка "Ценовые категории узлов"](./media/hdinsight-hadoop-create-linux-cluster-portal/hdinsight-create-cluster-nodes.png "Указание количества узлов кластера")
   
   > [!IMPORTANT]
   > Если вы планируете более 32 рабочих узлов в момент создания кластера или масштабирование hello кластера после ее создания, то необходимо выбрать размер головного узла с по крайней мере 8 ядер, 14 ГБ ОЗУ.
   > 
   > Дополнительные сведения о размерах узлов и их стоимости см. на странице с [ценами на HDInsight](https://azure.microsoft.com/pricing/details/hdinsight/).
   > 
   > 
   
   Нажмите кнопку **Далее** toosave hello узел цены конфигурации.

7. Нажмите кнопку **Дополнительные параметры** tooconfigure другие необязательные параметры, такие как с помощью **действия скрипта** toocustomize tooinstall кластера пользовательские компоненты или присоединив **виртуальной сети**. Рассмотрим таблицу hello ниже для получения дополнительной информации.

    ![Колонка "Ценовые категории узлов"](./media/hdinsight-hadoop-create-linux-cluster-portal/hdinsight-create-cluster-advanced.png "Указание количества узлов кластера")

    | Параметр | Описание |
    |--------|-------------|
    | **Действия сценариев** | Используйте этот параметр, если требуется toouse пользовательского скрипта toocustomize кластера, как идет создание кластера hello. Дополнительную информацию о действиях скриптов см. в статье [Настройка кластеров HDInsight под управлением Linux с помощью действия сценария](hdinsight-hadoop-customize-cluster-linux.md). |
    | **Виртуальная сеть** | Выберите виртуальные сети и hello подсеть Azure, если требуется tooplace hello кластера в виртуальной сети. Дополнительные сведения об использовании HDInsight с помощью виртуальной сети, включая требования к конфигурации для hello виртуальной сети в разделе [HDInsight расширить возможности с помощью виртуальной сети Azure](hdinsight-extend-hadoop-virtual-network.md). |

    Щелкните **Далее**.

8. На hello **Сводка** колонки, проверьте сведения о hello, заданное ранее, а затем нажмите кнопку **создать**.

    ![Колонка "Ценовые категории узлов"](./media/hdinsight-hadoop-create-linux-cluster-portal/hdinsight-create-cluster-summary.png "Указание количества узлов кластера")
    
    > [!NOTE]
    > Он может потребоваться некоторое время для hello кластера toobe создана, обычно около 15 минут. Используйте плитки приветствия на начальной панели hello или hello **уведомления** входа на hello слева от toocheck страницы приветствия на процесс подготовки hello.
    > 
    > 
12. После завершения процесса создания приветствия щелкните плитку hello для кластера hello из hello начальной панели toolaunch hello кластера колонки. Hello кластера колонки предоставляет hello следующую информацию.
    
    ![Колонка "Кластер"](./media/hdinsight-hadoop-create-linux-cluster-portal/hdinsight-create-cluster-completed.png "Свойства кластера")
    
    Используйте следующие значки hello toounderstand вверху hello эту колонку hello.
    
    * **Общие сведения о** вкладка предоставляет все hello важные сведения о кластере hello, такие как имя hello, группа ресурсов hello, он принадлежит, расположение hello, hello операционной системы, URL-адрес для мониторинга кластера hello и т. д.
    * **Панель мониторинга** направляет вас toohello Ambari портала, связанные с кластером hello.
    * **Secure Shell**: сведения, необходимые tooaccess hello кластера с помощью SSH.
    * **Масштаб кластера** позволяет увеличить hello число рабочих узлов, связанные с кластером hello.
    * **Удалить**: Удаление кластера HDInsight hello.
    

## <a name="customize-clusters"></a>Настройка кластеров
* Ознакомьтесь с разделом [Настройка кластеров HDInsight с помощью службы начальной загрузки](hdinsight-hadoop-customize-cluster-bootstrap.md).
* См. статью [Настройка кластеров HDInsight под управлением Windows с помощью действия сценария](hdinsight-hadoop-customize-cluster-linux.md).

## <a name="delete-hello-cluster"></a>Удалить кластер hello
[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="troubleshoot"></a>Устранение неполадок

Если при создании кластеров HDInsight возникли проблемы, см. раздел [Создание кластеров](hdinsight-administer-use-portal-linux.md#create-clusters).

## <a name="next-steps"></a>Дальнейшие действия
Теперь, когда вы успешно создали кластер HDInsight, используйте следующие toolearn как hello toowork с кластером:

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

### <a name="spark-clusters"></a>Кластеры Spark
* [Создание автономного приложения с использованием Scala](hdinsight-apache-spark-create-standalone-application.md)
* [Удаленный запуск заданий с помощью Livy в кластере Spark](hdinsight-apache-spark-livy-rest-interface.md)
* [Использование Spark со средствами бизнес-аналитики. Выполнение интерактивного анализа данных с использованием Spark в HDInsight с помощью средств бизнес-аналитики](hdinsight-apache-spark-use-bi-tools.md)
* [Spark с машинного обучения: используйте Spark в HDInsight toopredict food проверки результатов](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [Потоковая передача Spark. Использование Spark в HDInsight для сборки приложений потоковой передачи данных в режиме реального времени](hdinsight-apache-spark-eventhub-streaming.md)

