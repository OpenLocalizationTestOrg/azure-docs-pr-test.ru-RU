---
title: "aaaTips по использованию Hadoop в HDInsight под управлением Linux — в Azure | Документы Microsoft"
description: "Реализация советы по использованию кластеров под управлением Linux HDInsight (Hadoop) в знакомой среде Linux, работающих в облаке Azure hello."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: c41c611c-5798-4c14-81cc-bed1e26b5609
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/12/2017
ms.author: larryfr
ms.openlocfilehash: a555622605079c9beae88ece872042e36d540c7d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="information-about-using-hdinsight-on-linux"></a>Сведения об использовании HDInsight в Linux

Кластеры HDInsight Azure предоставляют Hadoop в знакомой среде Linux, работающих в облаке Azure hello. Для большинства задач они должны работать так же, как и любые другие установки Hadoop в Linux. В этом документе рассматриваются определенные отличия, которые при этом следует учитывать.

> [!IMPORTANT]
> Linux — hello только операционную систему, используемую в HDInsight версии 3.4 или более поздней. Дополнительные сведения см. в разделе [Приближается дата прекращения сопровождения HDI версии 3.3](hdinsight-component-versioning.md#hdinsight-windows-retirement).

## <a name="prerequisites"></a>Предварительные требования

Во многих hello в данном пошаговом руководстве используется hello следующие служебные программы, которые может потребоваться toobe, установленного в системе.

* [cURL](https://curl.haxx.se/) -toocommunicate при использовании веб-служб
* [jq](https://stedolan.github.io/jq/) -использовавшиеся документы JSON tooparse
* [Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-az-cli2) (Предварительная версия) — используется tooremotely управления службами Azure

## <a name="users"></a>Пользователи

Если кластер HDInsight не [присоединен к домену](hdinsight-domain-joined-introduction.md), его нужно рассматривать как **однопользовательскую** систему. Одной учетной записи пользователя SSH создается с кластером hello, с правами администратора. Можно создать дополнительные учетные записи SSH, однако они обладают кластера toohello доступа администратора.

Присоединенный к домену кластер HDInsight поддерживает несколько пользователей, а также более детализированные параметры разрешений и ролей. Дополнительные сведения см. в статье [Manage Domain-joined HDInsight clusters](hdinsight-domain-joined-manage.md) (Управление присоединенными к домену кластерами HDInsight).

## <a name="domain-names"></a>Имена доменов

Hello полное toouse имя (FQDN) домена, при подключении из Интернет-это hello кластера toohello  **&lt;имя_кластера >. azurehdinsight.net** или (для SSH)  **&lt;имя_кластера-ssh >. azurehdinsight.net**.

На внутреннем уровне каждого узла в кластере hello имеет имя, назначаемое при конфигурации кластера. имена кластеров toofind hello, в разделе hello **узлов** страницы приветствия Ambari веб-интерфейса. Можно также использовать следующие tooreturn список узлов из API-интерфейса REST Ambari hello hello:

    curl -u admin:PASSWORD -G "https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/hosts" | jq '.items[].Hosts.host_name'

Замените **пароль** с паролем hello hello учетной записи администратора, и **ИМЯ_КЛАСТЕРА** с hello имя кластера. Эта команда возвращает документ JSON, содержащий список hello узлами в кластере hello. Jq — используется tooextract hello `host_name` значение элемента для каждого узла.

Если требуется имя hello toofind hello узла для конкретной службы, можно запросить Ambari для этого компонента. Например узлы hello toofind hello HDFS имя узла, используйте hello следующую команду:

    curl -u admin:PASSWORD -G "https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/services/HDFS/components/NAMENODE" | jq '.host_components[].HostRoles.host_name'

Эта команда возвращает документ JSON, описывающий hello службы, а затем извлекает jq ожидания только hello `host_name` значение для узлов hello.

## <a name="remote-access-tooservices"></a>Tooservices удаленного доступа

* **Ambari (Интернет)** — https://&lt;имя_кластера>.azurehdinsight.net.

    Проверка подлинности с помощью администратора кластера hello и пароль и снова войдите в tooAmbari.

    Проверка подлинности является открытым текстом - всегда используйте HTTPS toohelp обеспечить подключение hello безопасность.

    > [!IMPORTANT]
    > Некоторые веб-hello пользовательские интерфейсы, доступные через Ambari доступ к узлам, с помощью внутреннее имя домена. Внутренний домен имена не доступен из Интернета через hello Интернета. Может появиться ошибки «сервер не найден» при попытке tooaccess некоторые функции через Интернет hello.
    >
    > toouse hello полный набор функций hello Ambari web пользовательского интерфейса, используйте SSH туннеля tooproxy web трафика toohello головного узла кластера. В разделе [использование SSH туннелирование tooaccess Ambari веб-интерфейса пользователя, диспетчер ресурсов, JobHistory, NameNode, Oozie и других сетевых интерфейсов](hdinsight-linux-ambari-ssh-tunnel.md)

* **Ambari (REST)** —https://&lt;имя_кластера>.azurehdinsight.net/ambari.

    > [!NOTE]
    > Проверка подлинности с помощью администратора кластера hello и пароль.
    >
    > Проверка подлинности является открытым текстом - всегда используйте HTTPS toohelp обеспечить подключение hello безопасность.

* **WebHCat (Templeton)** —https://&lt;имя_кластера>.azurehdinsight.net/templeton.

    > [!NOTE]
    > Проверка подлинности с помощью администратора кластера hello и пароль.
    >
    > Проверка подлинности является открытым текстом - всегда используйте HTTPS toohelp обеспечить подключение hello безопасность.

* **SSH** - &lt;имя_кластера>-ssh.azurehdinsight.net через порт 22 или 23. Порт 22 — toohello головному используется tooconnect для основной узлу, а 23 — используется tooconnect toohello получателя. Дополнительные сведения о hello головного узла см. в разделе [кластеры доступности и надежности Hadoop в HDInsight](hdinsight-high-availability-linux.md).

    > [!NOTE]
    > Доступны только головного узла кластера hello через SSH с клиентского компьютера. После подключения можно затем получить hello рабочих узлов с помощью SSH из головному узлу.

## <a name="file-locations"></a>Местоположения файлов

Файлы, относящиеся к Hadoop можно найти на узлах кластера hello `/usr/hdp`. В этом каталоге содержатся hello следующие вложенные папки:

* **2.2.4.9-1**: hello имя каталога — версия hello hello платформы Hortonworks Data Platform, используемые HDInsight. Номер Hello в кластере может отличаться от hello один перечисленные здесь.
* **текущий**: Эта папка содержит ссылки toosubdirectories под hello **2.2.4.9-1** каталога. Этот каталог существует, поэтому не нужно, чтобы номер версии tooremember hello.

Примеры данных и JAR-файлы можно найти в распределенной файловой системе Hadoop в папках `/example` и `/HdiSamples`.

## <a name="hdfs-azure-storage-and-data-lake-store"></a>HDFS, служба хранилища Azure и Data Lake Store

В большинстве типа распределений HDFS поддерживаемый локального хранилища на машинах hello в кластере hello. Использование локального хранилища в случае облачного решения с почасовой или поминутной платой за вычислительные ресурсы может оказаться весьма затратным.

HDInsight использует либо больших двоичных объектов в хранилище Azure или хранилища Озера данных Azure в качестве хранилища по умолчанию hello. Эти службы обеспечивают hello следующие преимущества:

* недорогое долговременное хранение;
* доступность из внешних служб, например веб-сайтов, служебных программ для отправки или скачивания файлов, пакетов SDK для различных языков и веб-браузеров.

> [!WARNING]
> HDInsight поддерживает только учетные записи хранения Azure __общего назначения__. Он не поддерживает hello __хранилище больших двоичных объектов__ тип учетной записи.

Учетная запись хранилища Azure может быть установлено too4.75 ТБ, хотя отдельные большие двоичные объекты (или файлов с точки зрения HDInsight) может только перейти вверх too195 ГБ. Хранилище Озера данных Azure могут динамически увеличиваться toohold trillions файлов, с отдельными файлами больше петабайт. Подробные сведения см. в [статье о больших двоичных объектах](https://docs.microsoft.com/rest/api/storageservices/understanding-block-blobs--append-blobs--and-page-blobs) и в описании [Data Lake Store](https://azure.microsoft.com/services/data-lake-store/).

При использовании хранилища Azure или хранилища Озера данных, не нужно toodo ничего особенного из данных hello tooaccess HDInsight. Например, следующая команда hello список файлов в hello `/example/data` папки независимо от того, он хранится в хранилище Azure или хранилища Озера данных:

    hdfs dfs -ls /example/data

### <a name="uri-and-scheme"></a>Схема и URI

Некоторые команды могут потребовать toospecify hello схемы как часть hello URI при доступе к файлу. Например hello Storm HDFS компонента требуется схема toospecify hello. При использовании нестандартных хранилище (добавлен в качестве кластера toohello «Дополнительные» хранилища), необходимо всегда использовать схему hello как часть hello URI.

При использовании __хранилища Azure__, используйте один из следующих схем URI hello:

* `wasb:///`: хранилище по умолчанию без шифрования обмена данными.

* `wasbs:///`: хранилище по умолчанию с шифрованием обмена данными.  Схема wasbs Hello поддерживается только из HDInsight начиная с версии 3.6.

* `wasb://<container-name>@<account-name>.blob.core.windows.net/`: при взаимодействии с учетной записью хранения, кроме используемой по умолчанию. Например, используется для дополнительной учетной записи хранения или при доступе к данным в общедоступной учетной записи хранения.

При использовании __хранилища Озера данных__, используйте один из следующих схем URI hello:

* `adl:///`: Доступ к hello хранилища Озера данных по умолчанию для кластера hello.

* `adl://<storage-name>.azuredatalakestore.net/`: используется при взаимодействии с Data Lake Store, отличным от используемого по умолчанию. Также используется tooaccess данных за пределами корневого каталога hello кластера HDInsight.

> [!IMPORTANT]
> При использовании хранилища Озера данных в качестве хранилища по умолчанию hello для HDInsight, необходимо указать путь в хранилище toouse hello как корень hello HDInsight хранилища. путь по умолчанию Hello `/clusters/<cluster-name>/`.
>
> При использовании `/` или `adl:///` tooaccess данных, доступны только данные, хранящиеся в корневом hello (например, `/clusters/<cluster-name>/`) hello кластера. использовать tooaccess данных в любом месте хранилища hello hello `adl://<storage-name>.azuredatalakestore.net/` формат.

### <a name="what-storage-is-hello-cluster-using"></a>Какое хранилище использует hello кластера

Конфигурация хранилища по умолчанию hello tooretrieve Ambari можно использовать для кластера hello. Используйте hello следующую команду tooretrieve HDFS информацию о конфигурации, перелистывания и фильтрация с помощью [jq](https://stedolan.github.io/jq/):

```curl -u admin:PASSWORD -G "https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/configurations/service_config_versions?service_name=HDFS&service_config_version=1" | jq '.items[].configurations[].properties["fs.defaultFS"] | select(. != null)'```

> [!NOTE]
> Возвращает hello первого применения конфигурации toohello сервера (`service_config_version=1`), который содержит эти сведения. Может потребоваться toolist toofind hello последнюю версию всех версий конфигурации.

Эта команда возвращает значение аналогичные toohello, следующие идентификаторы URI:

* `wasb://<container-name>@<account-name>.blob.core.windows.net`, если используется учетная запись хранения Azure.

    Hello имя учетной записи hello имя учетной записи хранения Azure hello, имя контейнера hello hello контейнер больших двоичных объектов, это корневой hello hello хранения данных кластера.

* `adl://home`, если используется Azure Data Lake Store. Имя хранилища Озера данных hello tooget, используйте hello после вызова REST

    ```curl -u admin:PASSWORD -G "https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/configurations/service_config_versions?service_name=HDFS&service_config_version=1" | jq '.items[].configurations[].properties["dfs.adls.home.hostname"] | select(. != null)'```

    Эта команда возвращает hello, за которым следует имя узла: `<data-lake-store-account-name>.azuredatalakestore.net`.

    каталог tooget hello в хранилище hello, являющегося корневым hello для HDInsight, используйте hello после вызова REST:

    ```curl -u admin:PASSWORD -G "https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/configurations/service_config_versions?service_name=HDFS&service_config_version=1" | jq '.items[].configurations[].properties["dfs.adls.home.mountpoint"] | select(. != null)'```

    Эта команда возвращает аналогичные toohello пути, следующие пути: `/clusters/<hdinsight-cluster-name>/`.

Также можно найти сведения хранилища hello, с помощью hello портал Azure с помощью hello следующие шаги:

1. В hello [портал Azure](https://portal.azure.com/), выберите кластер HDInsight.

2. Из hello **свойства** выберите **учетные записи хранения**. отображается информация Hello хранилища для кластера hello.

### <a name="how-do-i-access-files-from-outside-hdinsight"></a>Доступ к файлам за пределами HDInsight

Существует несколько способов tooaccess данные из внешних hello кластера HDInsight. Hello ниже приведены несколько tooutilities ссылки и пакеты SDK, которые можно использовать toowork с данными.

При использовании __хранилища Azure__, см. следующие ссылки для способа получить данные hello:

* [Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-az-cli2) — это набор команд интерфейса командной строки для работы с Azure. После установки, используйте hello `az storage` команду для получения справки по использованию хранилища, или `az storage blob` для команд, больших двоичных объектов.
* [blobxfer.py](https://github.com/Azure/azure-batch-samples/tree/master/Python/Storage)— cценарий Python для работы с большими двоичными объектами в хранилище Azure.
* Различные пакеты SDK:

    * [Java](https://github.com/Azure/azure-sdk-for-java)
    * [Node.js](https://github.com/Azure/azure-sdk-for-node)
    * [PHP](https://github.com/Azure/azure-sdk-for-php)
    * [Python](https://github.com/Azure/azure-sdk-for-python)
    * [Ruby](https://github.com/Azure/azure-sdk-for-ruby)
    * [.NET](https://github.com/Azure/azure-sdk-for-net)
    * [REST API службы хранилища](https://msdn.microsoft.com/library/azure/dd135733.aspx)

При использовании __хранилища Озера данных Azure__, см. следующие ссылки для способа получить данные hello:

* [веб-браузер](../data-lake-store/data-lake-store-get-started-portal.md);
* [PowerShell](../data-lake-store/data-lake-store-get-started-powershell.md)
* [Azure CLI 2.0](../data-lake-store/data-lake-store-get-started-cli-2.0.md)
* [REST API WebHDFS](../data-lake-store/data-lake-store-get-started-rest-api.md);
* [средства Data Lake для Visual Studio](https://www.microsoft.com/download/details.aspx?id=49504);
* [.NET](../data-lake-store/data-lake-store-get-started-net-sdk.md)
* [Java](../data-lake-store/data-lake-store-get-started-java-sdk.md)
* [Python](../data-lake-store/data-lake-store-get-started-python.md)

## <a name="scaling"></a>Масштабирование кластера

масштабирование функции кластера Hello позволяет toodynamically изменение hello количество узлов данных, используемый в кластере. Операции масштабирования можно выполнять параллельно с другими заданиями и процессами, выполняющимися в кластере.

типы другой кластер Hello затронутые масштабирование следующим образом:

* **Hadoop**: при масштабировании с уменьшением hello количество узлов в кластере, некоторые службы hello в кластере hello перезапускаются. Масштабирование операций может привести к задания, выполняющиеся или ожидающие toofail окончании hello hello операция масштабирования. После завершения операции hello можно повторно отправить задания hello.
* **HBase**: региональные серверы распределяются автоматически через несколько минут после завершения hello операция масштабирования. toomanually балансировки региональных серверов, используйте hello следующие шаги:

    1. Подключите кластер HDInsight toohello с помощью SSH. Дополнительные сведения см. в статье [Использование SSH с Hadoop на основе Linux в HDInsight из Linux, Unix или OS X](hdinsight-hadoop-linux-use-ssh-unix.md).

    2. Используйте следующие оболочки HBase toostart hello hello.

            hbase shell

    3. После загрузки hello оболочки HBase используйте hello следующие toomanually баланс hello региональных серверов:

            balancer

* **Storm.** После завершения операции масштабирования следует запустить повторную балансировку для всех запущенных топологий Storm. Перераспределения поддерживает hello топологии tooreadjust параллелизма на основе нового числа узлов в кластере hello hello. toorebalance под управлением топологии, используйте один из следующих вариантов hello:

    * **SSH**: подключение toohello сервера и используйте hello следующая команда toorebalance топологии:

            storm rebalance TOPOLOGYNAME

        Можно также указать параметры toooverride hello параллелизма указания изначально предоставлен hello топологии. Например `storm rebalance mytopology -n 5 -e blue-spout=3 -e yellow-bolt=10` перенастройка hello топологии too5 рабочих процессов, 3 исполнитель для компонента blue spout hello и 10 исполнитель для компонента желтый молнии hello.

    * **Storm пользовательского интерфейса**: используйте hello описанных ниже действий toorebalance топологии с помощью пользовательского интерфейса Storm hello.

        1. Откройте **https://CLUSTERNAME.azurehdinsight.net/stormui** веб-браузера, где ИМЯ_КЛАСТЕРА — имя кластера Storm hello. При появлении соответствующего запроса, введите имя администратора (администратора) кластера HDInsight hello и пароль, указанный при создании кластера hello.
        2. Выберите топологию hello вы хотите toorebalance, а затем выберите hello **Перебалансировка** кнопки. Введите задержку hello, перед выполнением операции измените баланс hello.

Подробные сведения о масштабировании кластера HDInsight см. в следующих статьях.

* [Управление кластерами Hadoop в HDInsight с помощью портала Azure hello](hdinsight-administer-use-portal-linux.md#scale-clusters)
* [Управление кластерами Hadoop в HDInsight с помощью интерфейса командной строки (CLI) Azure](hdinsight-administer-use-command-line.md#scale-clusters)

## <a name="how-do-i-install-hue-or-other-hadoop-component"></a>Как установить Hue (или другой компонент Hadoop)?

HDInsight является управляемой службой. Если Azure обнаруживает проблему с кластером hello, он может удалить hello, сбои узла и создать tooreplace узла его. При установке вручную действия на кластере hello, они не сохраняются при этой операции. Вместо этого используйте [действия скрипта HDInsight](hdinsight-hadoop-customize-cluster.md). Действие сценария может быть hello используется toomake следующие изменения:

* Установка и настройка службы или веб-сайта, например Spark или Hue.
* Установите и настройте компонент, который требует изменения конфигурации на нескольких узлах в кластере hello. Например, обязательная переменная среды, создание каталога ведения журналов или создание файла конфигурации.

Действия сценариев — это сценарии Bash. Hello сценариев запуска во время подготовки кластера и могут используется tooinstall и настроить дополнительные компоненты в кластере hello. Образцы скриптов, предоставляемые для установки hello следующие компоненты:

* [Hue](hdinsight-hadoop-hue-linux.md)
* [Giraph](hdinsight-hadoop-giraph-install-linux.md)
* [Solr](hdinsight-hadoop-solr-install-linux.md)

Сведения о разработке собственных действий скриптов см. в статье [Разработка действий сценариев с помощью HDInsight](hdinsight-hadoop-script-actions-linux.md).

### <a name="jar-files"></a>JAR-файлы

Некоторые технологии Hadoop предоставляются в автономных JAR-файлах, которые содержат функции, используемые в рамках задания MapReduce, либо из Pig или Hive. Хотя их можно устанавливать с помощью действия сценариев, они часто не требуют каких-либо настроек и может быть загруженного toohello кластера после подготовки и предназначен для непосредственного использования. Если вы хотите убедиться, что компонент hello toomake нечувствительным к повторным созданием образа hello кластера, можно хранить в хранилище по умолчанию hello hello jar-файл для кластера (WASB или ADL).

Например, если требуется toouse hello последнюю версию [DataFu](http://datafu.incubator.apache.org/), можно загрузить JAR-файл, содержащий проект hello и отправьте его toohello кластера HDInsight. Затем выполните hello DataFu документации о том, как toouse Pig или Hive.

> [!IMPORTANT]
> Некоторые компоненты, которые являются jar отдельных файлов, предоставляемых с HDInsight, но не в пути hello. Если вам нужны для конкретного компонента, можно использовать для него toosearch выполните hello в кластере:
>
> ```find / -name *componentname*.jar 2>/dev/null```
>
> Эта команда возвращает путь hello соответствующий jar-файла.

toouse другой версии компонента, версия hello передачи требуется и использовать его в заданиях.

> [!WARNING]
> Компоненты, предоставляемые с кластером HDInsight hello полностью поддерживаются и поддержки Майкрософт помогает tooisolate и разрешить проблемы toothese связанные компоненты.
>
> Пользовательские компоненты получают toohelp ограниченную техническую поддержку вы toofurther устранить проблему hello. Это может привести к устранению проблемы hello и без tooengage доступных каналов для hello открытии источника технологий, которых находится глубокие знания для данной технологии. Можно использовать ряд сайтов сообществ, например [форум MSDN по HDInsight](https://social.msdn.microsoft.com/Forums/azure/en-US/home?forum=hdinsight) или [http://stackoverflow.com](http://stackoverflow.com). Кроме того, проекты Apache можно просмотреть на соответствующих сайтах по адресу [http://apache.org](http://apache.org), например для [Hadoop](http://hadoop.apache.org/) и [Spark](http://spark.apache.org/).

## <a name="next-steps"></a>Дальнейшие действия

* [Миграция с HDInsight, на основе Windows и на основе tooLinux](hdinsight-migrate-from-windows-to-linux.md)
* [Использование Hive с HDInsight](hdinsight-use-hive.md)
* [Использование Pig с HDInsight](hdinsight-use-pig.md)
* [Использование заданий MapReduce с HDInsight](hdinsight-use-mapreduce.md)
