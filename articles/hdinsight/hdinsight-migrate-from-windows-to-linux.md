---
title: "aaaMigrate с HDInsight под управлением Windows на основе tooLinux HDInsight — Azure | Документы Microsoft"
description: "Узнайте, как toomigrate с HDInsight, на основе Windows кластера tooa кластера HDInsight под управлением Linux."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: ff35be59-bae3-42fd-9edc-77f0041bab93
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/12/2017
ms.author: larryfr
ms.openlocfilehash: 7e5e536e8672d7e7c3086c6860cec062d05eda65
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-from-a-windows-based-hdinsight-cluster-tooa-linux-based-cluster"></a>Миграция с кластера под управлением Linux tooa кластера HDInsight под управлением Windows

Этот документ содержит сведения о hello различия между HDInsight в Windows и Linux, а также рекомендации о том, как toomigrate существующих рабочих нагрузок tooa под управлением Linux кластера.

HDInsight под управлением Windows обеспечивает простой способ toouse Hadoop в облаке hello, может понадобиться кластера под управлением Linux toomigrate tooa. Например tootake преимуществами под управлением Linux инструменты и технологии, которые необходимы для вашего решения. Часто в экосистеме Hadoop hello разрабатываются в системах под управлением Linux и не могут быть доступны для использования с HDInsight под управлением Windows. Кроме того, во многих книгах, видеороликах и других учебных материалах предполагается, что при работе с Hadoop вы используете Linux.

> [!NOTE]
> Кластеры HDInsight использовать долгосрочной поддержка Ubuntu (LTS) в качестве hello операционной системы для hello узлов в кластере hello. Сведения о версии hello Ubuntu с HDInsight, вместе с другими данными управления версиями компонента см. в разделе [версий компонента HDInsight](hdinsight-component-versioning.md).

## <a name="migration-tasks"></a>Задачи миграции

Ниже приведен Hello общий рабочий процесс для миграции.

![Схема рабочего процесса миграции](./media/hdinsight-migrate-from-windows-to-linux/workflow.png)

1. Прочитайте каждый раздел этого документа toounderstand изменения, которые могут потребоваться при миграции существующего рабочего процесса, заданий, кластер под управлением Linux и т.д. tooa.

2. Создайте кластер под управлением Linux как среду тестирования и контроля качества. Дополнительные сведения о создании кластера под управлением Linux см. в статье [Создание кластеров под управлением Linux в HDInsight](hdinsight-hadoop-provision-linux-clusters.md).

3. Копирование существующих заданий, источники данных и приемники toohello новой среды.

4. Выполните Проверочное тестирование toomake убедиться, что заданиям работать должным образом на новый кластер hello.

После проверки того, что все работает правильно, необходимо запланируйте время простоя для миграции hello. В это время простоя выполните hello, следующие действия:

1. Создайте резервную копию временные данные, хранящиеся локально на узлах кластера hello. Например, к ним могут относиться данные, которые хранятся непосредственно на головном узле.

2. Удаление кластера под управлением Windows hello.

3. Создайте кластер под управлением Linux с помощью hello же по умолчанию hello кластера под управлением Windows, используемого хранилище данных. Hello кластера под управлением Linux могут продолжать работать с существующие рабочих данных.

4. Импортируйте все временные данные из резервной копии.

5. Запуск заданий и продолжить обработку с помощью нового кластера hello.

### <a name="copy-data-toohello-test-environment"></a>Копирование данных toohello тестовой среды

Существует множество методов toocopy hello данных и заданий, однако в этом разделе описываются два hello hello простой методы toodirectly перемещения файлов tooa проверка кластера.

#### <a name="hdfs-copy"></a>Копирование HDFS

Используйте hello следующие действия toocopy данные из hello производственного кластера toohello проверка кластера. Эти шаги используют hello `hdfs dfs` служебную программу, которая входит в состав HDInsight.

1. Найти hello хранилища учетной записи и по умолчанию сведения о контейнере для существующего кластера. Следующий пример Hello использует эти сведения, PowerShell tooretrieve:

    ```powershell
    $clusterName="Your existing HDInsight cluster name"
    $clusterInfo = Get-AzureRmHDInsightCluster -ClusterName $clusterName
    write-host "Storage account name: $clusterInfo.DefaultStorageAccount.split('.')[0]"
    write-host "Default container: $clusterInfo.DefaultStorageContainer"
    ```

2. toocreate тестовой среды, выполните действия hello hello кластеров на основе Linux, создайте в документе HDInsight. Остановить перед созданием кластера hello, а вместо этого выберите **необязательная конфигурация**.

3. Hello необязательная конфигурация колонке выберите **связанные учетные записи хранения**.

4. Выберите **добавить ключ хранилища**и при появлении запроса выберите учетную запись хранения hello, возвращенный hello сценарий PowerShell на шаге 1. Щелкните **Выбрать** на каждой колонке. Наконец Создайте кластер hello.

5. После создания кластера hello подключиться с помощью tooit **SSH.** Дополнительные сведения см. в статье [Использование SSH с Hadoop на основе Linux в HDInsight из Linux, Unix или OS X](hdinsight-hadoop-linux-use-ssh-unix.md).

6. Из сеанса SSH hello используйте следующую toocopy командные файлы из hello связаны хранилища учетной записи toohello новой по умолчанию учетной записи хранения hello. Замените КОНТЕЙНЕРА hello контейнера сведения, возвращенные PowerShell. Замените __учетной записи__ с именем учетной записи hello. Замените toodata путь hello tooa данных hello путь к файлу.

    ```bash
    hdfs dfs -cp wasb://CONTAINER@ACCOUNT.blob.core.windows.net/path/to/old/data /path/to/new/location
    ```

    > [!NOTE]
    > Если структура каталогов hello, содержащий данные hello не существует на hello тестовой среды, можно создать его с помощью hello следующую команду:

    ```bash
    hdfs dfs -mkdir -p /new/path/to/create
    ```

    Hello `-p` коммутатор обеспечивает создание hello все каталоги в пути hello.

#### <a name="direct-copy-between-blobs-in-azure-storage"></a>Прямое копирование между большими двоичными объектами в службе хранилища Azure

Кроме того, может потребоваться toouse hello `Start-AzureStorageBlobCopy` Azure PowerShell командлет toocopy BLOB-объектов между учетными записями хранения за пределами HDInsight. Дополнительные сведения см. в разделе hello как toomanage раздел больших двоичных объектов Azure с помощью Azure PowerShell со службой хранилища Azure.

## <a name="client-side-technologies"></a>Технологии на стороне клиента

Клиентские технологии, такие как [командлетов Azure PowerShell](/powershell/azureps-cmdlets-docs), [Azure CLI](../cli-install-nodejs.md), или hello [.NET SDK для Hadoop](https://hadoopsdk.codeplex.com/) продолжить toowork кластеры под управлением Linux. Эти технологии основаны на REST API, которые являются hello одинаково на обоих типах кластера ОС.

## <a name="server-side-technologies"></a>Технологии на стороне сервера

Привет, в следующей таблице приведены инструкции по миграции серверных компонентов, связанных с Windows.

| Если вы используете эту технологию... | Выполните это действие... |
| --- | --- |
| **PowerShell** (сценарии на стороне сервера, включая действия сценариев, используемые во время создания кластера) |Перепишите эти сценарии как скрипты Bash. Сведения о действиях сценариев см. в разделах [Настройка кластеров HDInsight под управлением Linux с помощью действия сценария](hdinsight-hadoop-customize-cluster-linux.md) и [Разработка действий сценариев с помощью HDInsight](hdinsight-hadoop-script-actions-linux.md). |
| **Azure CLI** (сценарии на стороне сервера) |Пока hello Azure CLI доступна в Linux, он не предустановлены на hello HDInsight кластер головного узла. Дополнительные сведения об установке hello Azure CLI см. в разделе [Приступая к работе с Azure CLI 2.0](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli). |
| **Компоненты .NET** |.NET поддерживается в кластерах HDInsight под управлением Linux посредством [Mono](https://mono-project.com). Дополнительные сведения см. в разделе [миграции .NET решений на базе tooLinux HDInsight](hdinsight-hadoop-migrate-dotnet-to-linux.md). |
| **Компоненты Win32 или другая технология, которая существует только для Windows** |Руководство по зависит от компонента hello или технологии. Может быть может toofind версии, совместимой с Linux или могут необходима toofind альтернативное решение или перепишите данный компонент. |

> [!IMPORTANT]
> Hello управления HDInsight SDK не полностью совместим с моно. Он не можно использовать как часть решения развертывания кластера HDInsight toohello в данный момент.

## <a name="cluster-creation"></a>Создание кластера

В этом разделе приведены сведения о различиях при создании кластера.

### <a name="ssh-user"></a>Пользователь SSH

Кластеры HDInsight под управлением Linux используйте hello **Secure Shell (SSH)** протокола узлы кластера toohello tooprovide удаленного доступа. В отличие клиентов удаленного рабочего стола для кластеров Windows, большинство SSH-клиентов не обеспечивает графический пользовательский интерфейс. Вместо этого клиенты SSH предоставляют командную строку, которая позволяет toorun команды на кластере hello. Некоторые клиенты (например, [MobaXterm](http://mobaxterm.mobatek.net/)) предоставляют графический файл системы браузер в дополнение tooa удаленной командной строки.

Во время создания кластера необходимо указать имя пользователя SSH и **пароль** или **сертификат открытого ключа** для аутентификации.

Мы рекомендуем использовать сертификат открытого ключа, так как он более безопасен по сравнению с паролем. Сертификат проверки подлинности осуществляется посредством создания знаком пару открытого и закрытого ключа, а затем указав hello открытый ключ при создании кластера hello. При подключении сервера toohello, с помощью SSH, hello закрытый ключ на клиенте hello обеспечивает проверку подлинности для подключения hello.

Дополнительные сведения см. в статье [Использование SSH с Hadoop на основе Linux в HDInsight из Linux, Unix или OS X](hdinsight-hadoop-linux-use-ssh-unix.md).

### <a name="cluster-customization"></a>Настройка кластера

**Действия сценария**, используемые в кластерах под управлением Linux, должны быть записаны в сценарий Bash. Во время действия скрипта можно использовать во время создания кластера для кластеров под управлением Linux, их также можно использовать tooperform настройки после копирования кластера и работает. Дополнительные сведения см. в разделах [Настройка кластеров HDInsight под управлением Linux с помощью действия сценария](hdinsight-hadoop-customize-cluster-linux.md) и [Разработка действий сценариев с помощью HDInsight](hdinsight-hadoop-script-actions-linux.md).

Еще одна возможность настройки — **начальная загрузка**. Для кластеров Windows эта функция позволяет расположение hello toospecify дополнительные библиотеки для использования с Hive. После создания кластера эти библиотеки автоматически станут доступны для использования с запросов Hive без необходимости toouse hello `ADD JAR`.

Hello начальной загрузки для кластеров под управлением Linux не обеспечивают эту функциональность. Вместо этого используйте действие сценария, указанное в статье [Добавление библиотек Hive во время создания кластера HDInsight](hdinsight-hadoop-add-hive-libraries.md).

### <a name="virtual-networks"></a>Виртуальные сети

Кластеры HDInsight под управлением Windows работают только с классическими виртуальными сетями, а для кластеров HDInsight под управлением Linux требуются виртуальные сети Resource Manager. Если имеются ресурсы классической виртуальной сети, которая hello кластера Linux HDInsight необходимо подключиться к см. в разделе [подключение tooa классической виртуальной сети виртуальная сеть диспетчера ресурсов](../vpn-gateway/vpn-gateway-connect-different-deployment-models-portal.md).

Дополнительные сведения о требованиях к конфигурации при использовании виртуальных сетей Azure в HDInsight см. в статье [Расширение возможностей HDInsight с помощью виртуальной сети Azure](hdinsight-extend-hadoop-virtual-network.md).

## <a name="management-and-monitoring"></a>Управление и мониторинг

Многие веб-hello пользовательских интерфейсов использовался с HDInsight под управлением Windows, такие как журнал заданий или Yarn пользовательского интерфейса, доступны через Ambari. Кроме того hello Ambari Hive представление предоставляет toorun способом запросов Hive, с помощью веб-браузере. Hello Ambari веб-интерфейса можно найти в кластеры под управлением Linux на https://CLUSTERNAME.azurehdinsight.net.

Дополнительные сведения о работе с Ambari см. в разделе hello следующие документы:

* [Веб-интерфейс Ambari](hdinsight-hadoop-manage-ambari.md)
* [Ambari REST API](hdinsight-hadoop-manage-ambari-rest-api.md)

### <a name="ambari-alerts"></a>Предупреждения Ambari

Ambari установлена система предупреждений, позволяющего однозначно судить о потенциальных проблемах с hello кластера. Отображаются в виде красного или желтого значка записей в hello Ambari веб-интерфейса, однако их также можно получить через API-Интерфейс REST hello.

> [!IMPORTANT]
> Предупреждения Ambari указывают на то, что проблема *возможна*, а не на то, что она уже *присутствует*. Например, может появиться предупреждение о том, что сервер HiveServer2 недоступен. При этом вы можете обратиться к нему обычным образом.
>
> Многие предупреждения реализованы в качестве запросов к службе и ожидают ответа в течение определенного промежутка времени. Поэтому предупреждение hello не обязательно означает, что служба hello не работает, только что он не вернул результаты в течение промежутка времени hello ожидается.

Перед выполнением каких-либо действий с оповещением следует оценить, появлялось ли оно в течение продолжительного периода времени или отражает проблемы в работе пользователей, о которых уже сообщалось.

## <a name="file-system-locations"></a>Структура файловой системы

Hello Linux кластера файловой системы выстраивается иначе, чем кластеры HDInsight под управлением Windows. Используйте следующие файлы toofind часто используемые таблицы hello.

| Мне нужна toofind... | Это находится в папке... |
| --- | --- |
| Конфигурация |`/etc`. Например, `/etc/hadoop/conf/core-site.xml` |
| Файлы журналов |`/var/logs` |
| Платформа данных Hortonworks Data Platform (HDP) |`/usr/hdp`. Существует два каталога находится здесь, это текущая версия HDP hello и `current`. Hello `current` каталог содержит toofiles символические ссылки и папки, размещенные в каталоге номера версии hello. Hello `current` каталога предоставляется для удобного доступа к файлам HDP с момента hello номер версии станет как hello HDP обновляется версия. |
| hadoop-streaming.jar |`/usr/hdp/current/hadoop-mapreduce-client/hadoop-streaming.jar` |

Вообще Если известно имя hello файла hello, можно использовать следующую команду из SSH toofind hello путь к файлу сеанса hello:

    find / -name FILENAME 2>/dev/null

Также можно использовать подстановочные знаки с именем файла hello. Например `find / -name *streaming*.jar 2>/dev/null` возвращает tooany путь hello jar-файлы, содержащие слово hello, «потоковая передача» как часть имени файла hello.

## <a name="hive-pig-and-mapreduce"></a>Hive, Pig и MapReduce

Рабочие нагрузки Pig и MapReduce на кластерах Linux похожи. Однако кластеры HDInsight под управлением Linux можно создать с помощью более новых версий Hadoop, Hive и Pig. Эти отличия версий могут повлиять на функционирование существующих решений. Дополнительные сведения о версиях hello компоненты, включенные в HDInsight см. в разделе [управление версиями компонента HDInsight](hdinsight-component-versioning.md).

Кластеры HDInsight под управлением Linux не предоставляют функцию удаленного рабочего стола. Вместо этого можно использовать SSH tooremotely подключения toohello кластер головного узла. Дополнительные сведения см. в разделе hello следующие документы:

* [Использование Hive с Hadoop в HDInsight с применением Beeline](hdinsight-hadoop-use-hive-ssh.md)
* [Использование Pig с SSH](hdinsight-hadoop-use-pig-ssh.md)
* [Использование MapReduce с SSH](hdinsight-hadoop-use-mapreduce-ssh.md)

### <a name="hive"></a>Hive

> [!IMPORTANT]
> Если вы используете внешние метахранилища Hive, вы резервную копию метахранилище hello перед его использованием с HDInsight под управлением Linux. В HDInsight под управлением Linux используются более новые версии Hive, что может привести к проблемам совместимости с хранилищами метаданных, созданными с использованием предыдущих версий.

Следующая диаграмма Hello содержатся рекомендации по переносу рабочих нагрузок Hive.

| В кластерах под управлением Windows я пользуюсь... | В кластерах под управлением Linux... |
| --- | --- |
| **редактор Hive;** |[используйте представление Hive в Ambari](hdinsight-hadoop-use-hive-ambari-view.md) |
| `set hive.execution.engine=tez;`tooenable Tez |Подсистема выполнения по умолчанию hello для кластеров под управлением Linux, больше не используется, чтобы hello задать инструкции Tez. |
| Определяемые пользователем функции C# | Сведения о проверке компонентов C# с HDInsight под управлением Linux см. в разделе [миграции .NET решений на базе tooLinux HDInsight](hdinsight-hadoop-migrate-dotnet-to-linux.md) |
| CMD файлы или сценарии на сервере hello вызывается как часть задания Hive |используйте скрипты Bash |
| `hive` из удаленного рабочего стола. |используйте [Beeline](hdinsight-hadoop-use-hive-beeline.md) или [Hive из сеанса SSH](hdinsight-hadoop-use-hive-ssh.md). |

### <a name="pig"></a>Pig,

| В кластерах под управлением Windows я пользуюсь... | В кластерах под управлением Linux... |
| --- | --- |
| Определяемые пользователем функции C# | Сведения о проверке компонентов C# с HDInsight под управлением Linux см. в разделе [миграции .NET решений на базе tooLinux HDInsight](hdinsight-hadoop-migrate-dotnet-to-linux.md) |
| CMD файлы или сценарии на сервере hello вызывается как часть задания Pig |используйте скрипты Bash |

### <a name="mapreduce"></a>MapReduce

| В кластерах под управлением Windows я пользуюсь... | В кластерах под управлением Linux... |
| --- | --- |
| Компоненты C# для сопоставления и редукции | Сведения о проверке компонентов C# с HDInsight под управлением Linux см. в разделе [миграции .NET решений на базе tooLinux HDInsight](hdinsight-hadoop-migrate-dotnet-to-linux.md) |
| CMD файлы или сценарии на сервере hello вызывается как часть задания Hive |используйте скрипты Bash |

## <a name="oozie"></a>Oozie,

> [!IMPORTANT]
> При использовании внешних метахранилище Oozie вы резервную копию метахранилище hello перед его использованием с HDInsight под управлением Linux. В HDInsight под управлением Linux используются более новые версии Oozie, что может привести к проблемам совместимости с хранилищами метаданных, созданными с использованием предыдущих версий.

Рабочие процессы Oozie позволяют использовать действия оболочки. Оболочки действия используйте оболочки по умолчанию hello для hello операционной системы toorun командной строки. Если у вас есть Oozie рабочие процессы, зависящие от оболочки Windows hello, необходимо переписать hello toorely рабочих процессов на оболочку среды Linux hello (Bash). Дополнительные сведения об использовании действий оболочки с Oozie см. в разделе [Oozie shell action extension](http://oozie.apache.org/docs/3.3.0/DG_ShellActionExtension.html) (Расширение действий оболочки Oozie).

Если имеются рабочие процессы Oozie, зависящие от приложений C#, вызываемых с помощью действий оболочки, необходимо проверить эти приложения в среде Linux. Дополнительные сведения см. в разделе [миграции .NET решений на базе tooLinux HDInsight](hdinsight-hadoop-migrate-dotnet-to-linux.md).

## <a name="storm"></a>Storm

| В кластерах под управлением Windows я пользуюсь... | В кластерах под управлением Linux... |
| --- | --- |
| Панель мониторинга Storm |Hello Storm мониторинга недоступна. В разделе [развертывание и управление Storm топологии на основе Linux HDInsight](hdinsight-storm-deploy-monitor-topology-linux.md) для способов toosubmit топологий |
| Пользовательский интерфейс Storm |найти по адресу https://CLUSTERNAME.azurehdinsight.net/stormui Hello Storm пользовательского интерфейса |
| Visual Studio toocreate, развертывания и управления C# или гибридной топологии |Visual Studio может быть используется toocreate, развертывание и управление C# (SCP.NET) или гибридной топологии, на основе Linux ураган в кластерах HDInsight, созданные после 10/28/2016. |

## <a name="hbase"></a>HBase

Для кластеров под управлением Linux, является родителем hello znode HBase `/hbase-unsecure`. Это значение в конфигурации hello для клиентских приложений Java, использовать собственный API Java HBase.

Пример клиента, который устанавливает это значение, см. в разделе [Использование Maven для сборки приложений Java, которые используют HBase с HDInsight (Hadoop)](hdinsight-hbase-build-java-maven.md).

## <a name="spark"></a>Spark

Кластеры Spark были доступны в кластерах Windows на этапе предварительной версии. Общедоступная версия Spark доступна только в кластерах Linux. Отсутствует путь миграции в кластере Spark под управлением Windows версии tooa предварительного просмотра кластера Spark под управлением Linux.

## <a name="known-issues"></a>Известные проблемы

### <a name="azure-data-factory-custom-net-activities"></a>Пользовательские действия .NET фабрики данных Azure

Пользовательские действия .NET фабрики данных Azure в настоящее время не поддерживаются в кластерах HDInsight под управлением Linux. Вместо этого следует использовать один из hello следующие методы tooimplement настраиваемые действия в рамках конвейера ADF.

* Выполните действия .NET в пуле пакетной службы Azure. В разделе hello связанной пакетной Azure используйте службу [использовать настраиваемые действия в конвейере фабрики данных Azure](../data-factory/data-factory-use-custom-activities.md)
* Реализуйте hello действие как действие MapReduce. Дополнительные сведения см. в разделе [Вызов программы MapReduce из фабрики данных](../data-factory/data-factory-map-reduce.md).

### <a name="line-endings"></a>Символы конца строки

Как правило, в качестве символов конца строки в Windows используется CRLF, а в Linux — LF. Если при формировании или ожидать данных с помощью окончаниях CRLF, может потребоваться toomodify hello производители и потребители toowork с конца строки LF hello.

Например HDInsight в кластере под управлением Windows с помощью Azure PowerShell tooquery возвращает данные с CRLF. Hello того же запроса в кластере под управлением Linux возвращает LF. Если конечная строка hello вызывает проблемы с вашей solutuion перед выполнением миграции следует протестировать toosee tooa кластера под управлением Linux.

При наличии скриптов, которые выполняются непосредственно на узлах кластера Linux hello, следует всегда использовать LF как hello завершения строк. Если вы используете CRLF, регистрируются сообщения об ошибках при выполнении скриптов hello в кластере под управлением Linux.

Если вы знаете, что hello скрипты не содержат строк с использованием внедренных символов CR, можно с помощью одного из следующих методов hello hello окончаниях изменений:

* **Перед отправкой кластера toohello**: hello используйте следующую PowerShell инструкций toochange hello завершениях из CRLF tooLF перед отправкой hello сценария toohello кластера.

    ```powershell
    $original_file ='c:\path\to\script.py'
    $text = [IO.File]::ReadAllText($original_file) -replace "`r`n", "`n"
    [IO.File]::WriteAllText($original_file, $text)
    ```

* **После отправки toohello кластера**: используйте hello следующие команды из toohello сеансу SSH скрипт hello toomodify кластера под управлением Linux.

    ```bash
    hdfs dfs -get wasb:///path/to/script.py oldscript.py
    tr -d '\r' < oldscript.py > script.py
    hdfs dfs -put -f script.py wasb:///path/to/script.py
    ```

## <a name="next-steps"></a>Дальнейшие действия

* [Узнайте, как toocreate HDInsight под управлением Linux кластеров](hdinsight-hadoop-provision-linux-clusters.md)
* [Используйте SSH tooconnect tooHDInsight](hdinsight-hadoop-linux-use-ssh-unix.md)
* [Выполняйте управление кластером под управлением Linux с помощью Ambari](hdinsight-hadoop-manage-ambari.md)
