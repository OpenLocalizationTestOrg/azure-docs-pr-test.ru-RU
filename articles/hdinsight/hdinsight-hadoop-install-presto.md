---
title: "кластеры Presto в Azure HDInsight Linux aaaInstall | Документы Microsoft"
description: "Узнайте, как tooinstall Presto и Airpal на основе Linux HDInsight Hadoop кластеры, использующие действий скрипта."
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/17/2017
ms.author: nitinme
ms.openlocfilehash: 5d54d0efc3e5fdc6f5a8d3a94ad2f61d16df24c2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="install-and-use-presto-on-hdinsight-hadoop-clusters"></a>Установка и использование Presto в кластерах HDInsight Hadoop

В этом разделе вы узнаете, как кластеры tooinstall Presto на HDInsight Hadoop с помощью действия сценария. Вы также узнаете, как tooinstall Airpal в существующем кластере Presto HDInsight.

> [!IMPORTANT]
> Hello в данном пошаговом руководстве требуется **кластера HDInsight 3.5 Hadoop** , использующий Linux. Linux — hello только операционную систему, используемую в HDInsight версии 3.4 или более поздней. Дополнительные сведения см. в статье [Что представляют собой различные компоненты и версии Hadoop, доступные в HDInsight?](hdinsight-component-versioning.md)

## <a name="what-is-presto"></a>Что такое Presto?
[Presto](https://prestodb.io/overview.html) представляет собой быстрый распределенный модуль SQL-запросов для больших данных. Presto подходит для интерактивных запросов петабайт данных. Дополнительные сведения о компонентах hello Presto и как они работают вместе. в разделе [появится понятия](https://github.com/prestodb/presto/blob/master/presto-docs/src/main/sphinx/overview/concepts.rst).

> [!WARNING]
> Компоненты, предоставляемые с кластером HDInsight hello полностью поддерживаются и поддержки Майкрософт способствуют tooisolate и разрешить проблемы toothese связанные компоненты.
> 
> Пользовательские компоненты, такие как Presto получать toohelp ограниченную техническую поддержку вы toofurther устранить проблему hello. Это может привести к устранению проблемы hello и без tooengage доступных каналов для hello открытии источника технологий, которых находится глубокие знания для данной технологии. Можно использовать ряд сайтов сообществ, например [форум MSDN по HDInsight](https://social.msdn.microsoft.com/Forums/azure/home?forum=hdinsight) или [http://stackoverflow.com](http://stackoverflow.com). Кроме того, для проектов Apache есть соответствующие сайты, например [Hadoop](http://hadoop.apache.org/) на сайте [http://apache.org](http://apache.org).
> 
> 


## <a name="install-presto-using-script-action"></a>Установка Presto с помощью действия скрипта

В этом разделе описано, как toouse hello образец скрипта при создании нового кластера с помощью hello портал Azure. 

1. Запуск подготовки кластера с помощью действия hello в [кластеры HDInsight под управлением Linux подготовки](hdinsight-hadoop-create-linux-clusters-portal.md). Убедитесь, что вы создаете с помощью hello кластер hello **настраиваемый** кластера создания потока. Необходимо убедиться, что при создании кластера hello соответствует hello следующие требования.

    а. Это должен быть кластер Hadoop в HDInsight версии 3.5.

    b. Оно должно использовать хранилище Azure как hello хранилища данных. С помощью Presto на кластер, использующий в качестве варианта хранилища hello хранилища Озера данных Azure пока не поддерживается. 

    ![Создание кластера HDInsight с использованием настраиваемых параметров](./media/hdinsight-hadoop-install-presto/hdinsight-install-custom.png)

2. На hello **Дополнительные параметры** колонке выберите **действия скрипта**и укажите следующие сведения hello:
   
   * **ИМЯ**: Введите понятное имя для действия сценария hello.
   * **URI bash-скрипта**: `https://raw.githubusercontent.com/hdinsight/presto-hdinsight/master/installpresto.sh`
   * **ГОЛОВНОЙ**: установите флажок.
   * **Рабочая роль**: установите флажок.
   * **ZOOKEEPER**: снимите этот флажок.
   * **ПАРАМЕТРЫ**: оставьте это поле пустым.


3. Внизу hello hello **действия скрипта** колонке щелкните hello **выберите** конфигурация hello toosave кнопок. Щелкните hello **выберите** кнопку внизу hello hello **Дополнительные параметры** сведения о конфигурации hello toosave колонку.

4. Продолжить подготовки кластера hello, как описано в [кластеры HDInsight под управлением Linux подготовки](hdinsight-hadoop-create-linux-clusters-portal.md).

    > [!NOTE]
    > Действия сценариев используется tooapply также может быть Azure PowerShell, hello Azure CLI, hello HDInsight .NET SDK или шаблоны Azure Resource Manager. Можно также применить tooalready действия сценария работающие кластеры. Дополнительные сведения см. в статье [Настройка кластеров HDInsight под управлением Linux с помощью действия сценария](hdinsight-hadoop-customize-cluster-linux.md).
    > 
    > 

## <a name="use-presto-with-hdinsight"></a>Использование Presto с HDInsight

Выполните следующие шаги toouse Presto в кластер HDInsight после установки с помощью hello действия, описанные выше hello.

1. Подключите кластер HDInsight toohello с помощью SSH:
   
        ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net
   
    Дополнительные сведения см. в статье [Использование SSH с Hadoop на основе Linux в HDInsight из Linux, Unix или OS X](hdinsight-hadoop-linux-use-ssh-unix.md).
     

2. Запустите консоль появится hello, используя следующую команду hello.
   
        presto --schema default

3. Выполните запрос в примере таблицы **hivesampletable**, которая доступна во всех кластерах HDInsight по умолчанию.
   
        select count (*) from hivesampletable;
   
    По умолчанию соединители [Hive](https://prestodb.io/docs/current/connector/hive.html) и [TPCH](https://prestodb.io/docs/current/connector/tpch.html) для Presto уже настроены. Соединитель куст — настроенное toouse hello установки по умолчанию установлен Hive, таким образом, все таблицы hello из куста автоматически отображается на Presto.

    Подробное описание использования Presto см. в [документации по Presto](https://prestodb.io/docs/current/index.html).

## <a name="use-airpal-with-presto"></a>Использование Airpal с Presto

[Airpal](https://github.com/airbnb/airpal#airpal) является веб-интерфейсом запросов с открытым кодом для Presto. Дополнительные сведения об Airpal см. в [документации по Airpal](https://github.com/airbnb/airpal#airpal).

В этом разделе мы рассмотрим действия hello слишком**установить Airpal на hello edgenode** кластер HDInsight Hadoop, уже содержит Presto установлена. Это гарантирует, что запрос, hello Airpal веб-интерфейс доступна через Интернет hello.

1. С помощью SSH, подключиться к головному узлу кластера HDInsight hello, если оно Presto toohello:
   
        ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net
   
    Дополнительные сведения см. в статье [Использование SSH с Hadoop на основе Linux в HDInsight из Linux, Unix или OS X](hdinsight-hadoop-linux-use-ssh-unix.md).

2. После подключения, выполните следующую команду hello.

        sudo slider registry  --name presto1 --getexp presto 
   
    Вы должны увидеть результаты hello следующим образом:

        {
            "coordinator_address" : [ {
                "value" : "10.0.0.12:9090",
                "level" : "application",
                "updatedTime" : "Mon Apr 03 20:13:41 UTC 2017"
        } ]

3. Hello в выходных данных, отметьте значение hello hello **значение** свойства. Он потребуется при установке Airpal на edgenode hello кластера. Из выходных данных hello выше значение hello, вам потребуется — **10.0.0.12:9090**.

4. Использовать шаблон hello  **[здесь](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fhdinsight%2Fpresto-hdinsight%2Fmaster%2Fairpal-deploy.json)**  toocreate HDInsight кластера edgenode и предоставления значения hello, как показано в следующий снимок экрана приветствия.

    ![Установка HDInsight Airpal в кластер Presto](./media/hdinsight-hadoop-install-presto/hdinsight-install-airpal.png)

5. Щелкните **Приобрести**.

6. После изменений hello примененных toohello конфигурации кластера, доступны hello Airpal веб-интерфейса с помощью hello следующие шаги.

    а. Из колонки hello кластера, нажмите кнопку **приложений**.

    ![Запуск HDInsight Airpal в кластере Presto](./media/hdinsight-hadoop-install-presto/hdinsight-presto-launch-airpal.png)

    b. Из hello **установленные приложения** колонка, щелкните **портала** от airpal.

    ![Запуск HDInsight Airpal в кластере Presto](./media/hdinsight-hadoop-install-presto/hdinsight-presto-launch-airpal-1.png)

    c. При появлении запроса введите учетные данные администратора hello, указанный при создании hello кластера HDInsight Hadoop.

## <a name="customize-a-presto-installation-on-hdinsight-cluster"></a>Настройка установки Presto в кластере HDInsight

После установки Presto в кластере HDInsight Hadoop, можно настроить hello установки toomake изменения, такие как параметры памяти обновления, измените соединителей, и т. д. Выполните hello, поэтому следующие шаги toodo.

1. С помощью SSH, подключиться к головному узлу кластера HDInsight hello, если оно Presto toohello:
   
        ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net
   
    Дополнительные сведения см. в статье [Использование SSH с Hadoop на основе Linux в HDInsight из Linux, Unix или OS X](hdinsight-hadoop-linux-use-ssh-unix.md).

2. Внесите изменения в конфигурацию в файле hello `/var/lib/presto/presto-hdinsight-master/appConfig-default.json`. Дополнительные сведения о конфигурации см. в статье [Presto configuration for YARN-based clusters](https://prestodb.io/presto-yarn/installation-yarn-configuration-options.html) (Конфигурация Presto для кластеров на базе YARN).

3. Остановите и завершения текущего выполняемого экземпляра hello Presto.

        sudo slider stop presto1 --force
        sudo slider destroy presto1 --force

4. Запустите новый экземпляр Presto с настройкой hello.

       sudo slider create presto1 --template /var/lib/presto/presto-hdinsight-master/appConfig-default.json --resources /var/lib/presto/presto-hdinsight-master/resources-default.json

5. Дождитесь hello новый экземпляр toobe готовности и запишите адрес появится координатора.


       sudo slider registry --name presto1 --getexp presto

## <a name="generate-benchmark-data-for-hdinsight-clusters-that-run-presto"></a>Создание тестовых данных для кластеров HDInsight под управлением Presto

TPC-доменных служб Active Directory — hello стандартный для измерения производительности hello многих систем поддержки принятия решений, включая систем большие наборы данных. Можно использовать Presto данных toogenerate кластеров HDInsight и оценить, сравнивает его с данными тестирования HDInsight. Дополнительные сведения см. [здесь](https://github.com/hdinsight/tpcds-datagen-as-hive-query/blob/master/README.md).



## <a name="see-also"></a>См. также
* [Установка и использование Hue в кластерах HDInsight](hdinsight-hadoop-hue-linux.md). Цветовым тоном является веб-интерфейса, который позволяет легко toocreate, запустите и сохраните задания Pig и Hive, также как и в случае найдите hello хранилища по умолчанию для кластера HDInsight.

* [Установка Giraph в кластерах HDInsight](hdinsight-hadoop-giraph-install-linux.md). Используйте tooinstall настройки кластера кластеров Giraph на HDInsight Hadoop. Giraph дает graph tooperform обработки с помощью Hadoop и может использоваться с Azure HDInsight.

* [Установка Solr в кластерах HDInsight](hdinsight-hadoop-solr-install-linux.md). Используйте tooinstall настройки кластера кластеров Solr на HDInsight Hadoop. Solr позволяет выполнять операции поиска мощные tooperform хранимых данных.

[hdinsight-install-r]: hdinsight-hadoop-r-scripts-linux.md
[hdinsight-cluster-customize]: hdinsight-hadoop-customize-cluster-linux.md
