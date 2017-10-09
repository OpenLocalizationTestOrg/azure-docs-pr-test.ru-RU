---
title: "Разработка действий aaaScript с HDInsight под управлением Linux — в Azure | Документы Microsoft"
description: "Узнайте, как toouse Bash сценарии toocustomize кластеры HDInsight под управлением Linux. Hello скрипт действие hdinsight, позволяет toorun скриптов во время или после создания кластера. Скрипты можно использовать toochange параметры конфигурации кластера или установить дополнительное программное обеспечение."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: cf4c89cd-f7da-4a10-857f-838004965d3e
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/31/2017
ms.author: larryfr
ms.openlocfilehash: 1f504b00365df5f4cfb3ae19ad55ff7630342650
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="script-action-development-with-hdinsight"></a>Разработка действий сценариев с помощью HDInsight

Узнайте, как Bash toocustomize кластера HDInsight с помощью скриптов. Действия сценариев являются способом toocustomize HDInsight во время или после создания кластера.

> [!IMPORTANT]
> Hello в данном пошаговом руководстве требуется кластер HDInsight, использующий Linux. Linux — hello только операционную систему, используемую в HDInsight версии 3.4 или более поздней. Дополнительные сведения см. в разделе [Приближается дата прекращения сопровождения HDI версии 3.3](hdinsight-component-versioning.md#hdinsight-windows-retirement).

## <a name="what-are-script-actions"></a>Что такое действия сценариев?

Действия сценариев Bash скрипты, которые Azure работает на изменения конфигурации toomake узлы кластера hello и устанавливать программное обеспечение. Действие сценария выполняется как корневой и обеспечивает полный доступ узлов кластера toohello права.

Действия сценариев могут применяться через hello следующие методы:

| Используйте этот метод tooapply сценария: | При создании кластера… | В работающем кластере… |
| --- |:---:|:---:|
| Портал Azure |✓  |✓ |
| Azure PowerShell |✓ |✓ |
| Инфраструктура CLI Azure |&nbsp; |✓ |
| Пакет SDK для HDInsight .NET |✓ |✓ |
| Шаблон Azure Resource Manager |✓  |&nbsp; |

Дополнительные сведения об использовании этих действий скрипта tooapply методов см. в разделе [HDInsight настроить кластеры, использующие действия скрипта](hdinsight-hadoop-customize-cluster-linux.md).

## <a name="bestPracticeScripting"></a>Рекомендации по разработке сценариев

При разработке пользовательского скрипта для кластера HDInsight, существует несколько лучшие методики tookeep помнить:

* [Целевая версия Hadoop hello](#bPS1)
* [Hello целевой версии ОС](#bps10)
* [Обеспечить стабильность связывает tooscript ресурсы](#bPS2)
* [Использование предварительно скомпилированных ресурсов](#bPS4)
* [Убедитесь, что скрипт настройки кластера hello идемпотентными](#bPS3)
* [Обеспечить высокий уровень доступности кластера архитектура hello](#bPS5)
* [Настройка хранилища больших двоичных объектов Azure toouse пользовательские компоненты hello](#bPS6)
* [TooSTDOUT сведения о записи и STDERR](#bPS7)
* [Сохранение файлов в формате ASCII с использованием LF в качестве символа завершения строки](#bps8)
* [Использовать toorecover логику повторных попыток от временных ошибок](#bps9)

> [!IMPORTANT]
> Действия скриптов должна быть завершена в течение 60 минут или hello процесс завершается ошибкой. Во время инициализации узла, hello скрипт выполняется параллельно с другими процессами, установки и настройки. Соперничество за ресурсы, такие как ЦП или в сети может вызвать скрипт hello tootake больше toofinish не так, как в среде разработки.

### <a name="bPS1"></a>Целевая версия Hadoop hello

В различных версиях HDInsight используются различные версии служб Hadoop и компонентов. Если сценарий требует определенной версии службы или компонента, hello скрипт следует использовать только с версией hello HDInsight, которая включает hello необходимых компонентов. Можно найти сведения о версии компонентов, включенных в HDInsight с помощью hello [управление версиями компонента HDInsight](hdinsight-component-versioning.md) документа.

### <a name="bps10"></a>Целевая версия ОС hello

HDInsight под управлением Linux основан на hello распространения Ubuntu Linux. Для разных версий HDInsight используются разные версии Ubuntu. Это может изменить поведение сценария. Например, HDInsight версии 3.4 и более ранних версий основан на версии Ubuntu, в которой используется Upstart. Версия 3.5 основана на Ubuntu версии 16.04, в которой используется Systemd. Systemd и Upstart используют различные команды, скрипт должен быть записан toowork с обоими.

Является еще одним важным различием между HDInsight 3.4 и 3.5, `JAVA_HOME` теперь указывает tooJava 8.

Версия ОС hello можно проверить с помощью `lsb_release`. Hello следующий код демонстрирует, как toodetermine Если hello скрипт выполняется на Ubuntu 14 или 16:

```bash
OS_VERSION=$(lsb_release -sr)
if [[ $OS_VERSION == 14* ]]; then
    echo "OS verion is $OS_VERSION. Using hue-binaries-14-04."
    HUE_TARFILE=hue-binaries-14-04.tgz
elif [[ $OS_VERSION == 16* ]]; then
    echo "OS verion is $OS_VERSION. Using hue-binaries-16-04."
    HUE_TARFILE=hue-binaries-16-04.tgz
fi
...
if [[ $OS_VERSION == 16* ]]; then
    echo "Using systemd configuration"
    systemctl daemon-reload
    systemctl stop webwasb.service    
    systemctl start webwasb.service
else
    echo "Using upstart configuration"
    initctl reload-configuration
    stop webwasb
    start webwasb
fi
...
if [[ $OS_VERSION == 14* ]]; then
    export JAVA_HOME=/usr/lib/jvm/java-7-openjdk-amd64
elif [[ $OS_VERSION == 16* ]]; then
    export JAVA_HOME=/usr/lib/jvm/java-8-openjdk-amd64
fi
```

Можно найти hello полный скрипт, содержащий эти фрагменты кода в https://hdiconfigactions.blob.core.windows.net/linuxhueconfigactionv02/install-hue-uber-v02.sh.

Версию hello Ubuntu, используемый HDInsight см. в разделе hello [версия компонента HDInsight](hdinsight-component-versioning.md) документа.

. в разделе toounderstand hello различия между Systemd и Upstart, [Systemd для пользователей Upstart](https://wiki.ubuntu.com/SystemdForUpstartUsers).

### <a name="bPS2"></a>Обеспечить стабильность связывает tooscript ресурсы

Hello скрипта и связанных ресурсов должен оставаться доступными во время существования hello hello кластера. Эти ресурсы являются обязательными при добавлении новых узлов кластера toohello во время операции масштабирования.

Рекомендуется Hello является toodownload и архивировать все данные в учетной записи хранилища Azure для вашей подписки.

> [!IMPORTANT]
> Hello хранилища учетная запись должна быть hello по умолчанию учетной записи хранилища для кластера hello или открытые, только для чтения контейнера на любой другой учетной записи хранилища.

Например, hello образцы, поставляемые корпорацией Майкрософт, хранятся в hello [https://hdiconfigactions.blob.core.windows.net/](https://hdiconfigactions.blob.core.windows.net/) учетной записи хранилища. Это поддерживается командой HDInsight hello контейнер открытым и доступным только для чтения.

### <a name="bPS4"></a>Использование предварительно скомпилированных ресурсов

tooreduce hello время принимает toorun hello скрипт, избежать операций, которые компиляции ресурсов из исходного кода. Например, предварительной компиляции ресурсов и сохранять их в большом двоичном объекте учетной записи хранилища Azure в hello же центре обработки данных с HDInsight.

### <a name="bPS3"></a>Убедитесь, что скрипт настройки кластера hello идемпотентными

Сценарии должны быть идемпотентными. Если сценарий hello запускается несколько раз, он должен возвращать hello же состояния при каждом toohello кластера.

Например, сценарий, который изменяет файлы конфигурации, не должен добавлять повторяющиеся записи в случае многократного выполнения.

### <a name="bPS5"></a>Обеспечить высокий уровень доступности кластера архитектура hello

Кластеры HDInsight под управлением Linux предоставляют два головного узла, которые активны в кластере hello и скрипт действия выполняются на обоих узлах. Если hello компоненты, которые можно установить только один головной узел, не устанавливайте компоненты hello на оба головного узла.

> [!IMPORTANT]
> Службы, предоставляемые в рамках HDInsight превышают спроектированный toofail между двумя узлами головного hello при необходимости. Эта функция не будет продлен toocustom компоненты устанавливаются с помощью действий скрипта. Если требуется высокий уровень доступности пользовательских компонентов, необходимо реализовать собственный механизм отработки отказа.

### <a name="bPS6"></a>Настройка хранилища больших двоичных объектов Azure toouse пользовательские компоненты hello

Возможно, компонентов, установленных на кластер hello конфигурацию по умолчанию, который использует хранилище системы распределенных файла Hadoop (HDFS). HDInsight использует хранилище Azure или хранилища Озера данных в качестве хранилища по умолчанию hello. Они обеспечивают системой совместимый файл HDFS, которая сохраняет данные, даже если удалить кластер hello. Может потребоваться установить toouse WASB или ADL вместо HDFS компонентов tooconfigure.

Для большинства операций не обязательно toospecify hello файловой системы. Например следующие hello копирует файл giraph-examples.jar hello из хранилища toocluster hello локальной файловой системы:

```bash
hdfs dfs -put /usr/hdp/current/giraph/giraph-examples.jar /example/jars/
```

В этом примере hello `hdfs` команда прозрачно использует хранилище кластера по умолчанию hello. Для некоторых операций может потребоваться toospecify hello URI. Например, `adl:///example/jars` для Data Lake Store или `wasb:///example/jars` для хранилища Azure.

### <a name="bPS7"></a>TooSTDOUT сведения о записи и STDERR

HDInsight заносит в журнал выходные данные скрипт, написанный tooSTDOUT и STDERR. Можно просмотреть эти сведения, с помощью Ambari web hello пользовательского интерфейса.

> [!NOTE]
> Ambari доступна только в том случае, если hello кластер успешно создан. Hello, устранении неполадок см. Если вы используете действие сценария во время создания кластера и создание завершается с ошибкой, [HDInsight настроить кластеры, использующие действие сценария](hdinsight-hadoop-customize-cluster-linux.md#troubleshooting) другие способы доступа к записываемых данных.

Большинство программ и пакеты установки уже записи tooSTDOUT сведения и STDERR, однако вы можете tooadd более подробное ведение журнала. tooSTDOUT toosend текста, используйте `echo`. Например:

```bash
echo "Getting ready tooinstall Foo"
```

По умолчанию `echo` отправляет hello tooSTDOUT строки. toodirect его tooSTDERR, добавьте `>&2` перед `echo`. Например:

```bash
>&2 echo "An error occurred installing Foo"
```

Это перенаправляет данные, которые записываются вместо tooSTDOUT tooSTDERR (2). Дополнительные сведения о перенаправлении ввода-вывода см. на странице [http://www.tldp.org/LDP/abs/html/io-redirection.html](http://www.tldp.org/LDP/abs/html/io-redirection.html).

Дополнительные сведения о просмотре журналов, созданных действиями сценариев, см. в статье [Настройка кластеров HDInsight с помощью действия сценария](hdinsight-hadoop-customize-cluster-linux.md#troubleshooting).

### <a name="bps8"></a> Сохранение файлов в формате ASCII с использованием LF в качестве символа завершения строки

Сценарии Bash должны храниться в формате ASCII. Для завершения строк в этом файле используется символ LF. Файлы, которые хранятся в кодировке UTF-8 или использовать в качестве завершения строк hello CRLF могут завершаться со hello следующая ошибка:

```
$'\r': command not found
line 1: #!/usr/bin/env: No such file or directory
```

### <a name="bps9"></a>Использовать toorecover логику повторных попыток от временных ошибок

При загрузке файлов, установки пакетов с помощью apt get или других действий, которые передачи данных через Здравствуйте Интернета, действие hello может завершиться ошибкой из-за ошибки сети tootransient. Например удаленный ресурс hello, которые обмениваются данными с может быть в процессе hello переключения tooa узел резервного копирования.

toomake устойчивым tootransient ошибки скрипта, можно реализовать логику повторных попыток. следующие функции Hello показано, как tooimplement логику повторных попыток. Он пытается выполнить сбойные операции hello трижды до сбоя.

```bash
#retry
MAXATTEMPTS=3

retry() {
    local -r CMD="$@"
    local -i ATTMEPTNUM=1
    local -i RETRYINTERVAL=2

    until $CMD
    do
        if (( ATTMEPTNUM == MAXATTEMPTS ))
        then
                echo "Attempt $ATTMEPTNUM failed. no more attempts left."
                return 1
        else
                echo "Attempt $ATTMEPTNUM failed! Retrying in $RETRYINTERVAL seconds..."
                sleep $(( RETRYINTERVAL ))
                ATTMEPTNUM=$ATTMEPTNUM+1
        fi
    done
}
```

Hello следующие примеры демонстрируют, как toouse эту функцию.

```bash
retry ls -ltr foo

retry wget -O ./tmpfile.sh https://hdiconfigactions.blob.core.windows.net/linuxhueconfigactionv02/install-hue-uber-v02.sh
```

## <a name="helpermethods"></a>Вспомогательные методы для пользовательских сценариев

Вспомогательные методы действий сценариев — это служебные программы, которые можно использовать при создании пользовательских сценариев. Эти методы содержатся в сценарии [https://hdiconfigactions.blob.core.windows.net/linuxconfigactionmodulev01/HDInsightUtilities-v01.sh](https://hdiconfigactions.blob.core.windows.net/linuxconfigactionmodulev01/HDInsightUtilities-v01.sh). Используйте следующие toodownload hello и использовать их как часть сценария:

```bash
# Import hello helper method module.
wget -O /tmp/HDInsightUtilities-v01.sh -q https://hdiconfigactions.blob.core.windows.net/linuxconfigactionmodulev01/HDInsightUtilities-v01.sh && source /tmp/HDInsightUtilities-v01.sh && rm -f /tmp/HDInsightUtilities-v01.sh
```

Hello следующие вспомогательные классы, доступные для использования в скрипте:

| Назначение вспомогательного приложения | Описание |
| --- | --- |
| `download_file SOURCEURL DESTFILEPATH [OVERWRITE]` |Загружает файл из hello исходный URI toohello указанный путь к файлу. По умолчанию существующий файл не перезаписывается. |
| `untar_file TARFILE DESTDIR` |Извлекает tar-файл (с помощью `-xf`) toohello целевой каталог. |
| `test_is_headnode` |При запуске на головном узле кластера возвращает значение 1, в противном случае — 0. |
| `test_is_datanode` |Если hello текущий узел является узлом данных (рабочая), возвращают значение 1; в противном случае — 0. |
| `test_is_first_datanode` |Если hello текущий узел сначала данные hello (рабочая) узла (именованные workernode0) возвращает 1; в противном случае — 0. |
| `get_headnodes` |Полное доменное имя возвращаемого hello headnodes hello в кластере hello. Имена содержат разделители-запятые. При возникновении ошибки возвращается пустая строка. |
| `get_primary_headnode` |Возвращает полное доменное имя hello головному узлу первичной hello. При возникновении ошибки возвращается пустая строка. |
| `get_secondary_headnode` |Возвращает hello полное доменное имя получателя головному узлу hello. При возникновении ошибки возвращается пустая строка. |
| `get_primary_headnode_number` |Возвращает числовой суффикс hello головному узлу первичной hello. При возникновении ошибки возвращается пустая строка. |
| `get_secondary_headnode_number` |Возвращает числовой суффикс hello объекта получателя головному узлу hello. При возникновении ошибки возвращается пустая строка. |

## <a name="commonusage"></a>Общие варианты использования

В этом разделе приводятся рекомендации по реализации некоторых hello распространенных шаблонов использования, вы можете столкнуться при написании пользовательского скрипта.

### <a name="passing-parameters-tooa-script"></a>Передача параметров сценария tooa

В некоторых случаях для сценария требуется указывать параметры. Например может потребоваться пароль администратора hello для hello кластера при использовании Ambari REST API hello.

Параметры, передаваемые toohello сценария известны как *позиционные параметры*и им назначается слишком`$1` для первого параметра hello, `$2` для hello второй и поэтому на. `$0`содержит имя самого сценария hello hello.

Значения, передаваемые toohello сценария в качестве параметров должны быть заключены в одинарные кавычки ('). Это гарантирует, что hello передано значение рассматривается как литерал.

### <a name="setting-environment-variables"></a>Настройка переменных среды

Установив переменную среды осуществляется hello следующей инструкцией:

    VARIABLENAME=value

Где VARIABLENAME — hello имя переменной hello. Использование переменной, hello tooaccess `$VARIABLENAME`. Например tooassign значение, предоставляемые позиционного параметра переменной среды с именем пароль, следует использовать hello, следующем за инструкцией:

    PASSWORD=$1

Затем можно использовать сведения toohello последующий доступ к нему `$PASSWORD`.

Переменные среды, заданные в скриптах hello существуют только в области hello hello скрипта. В некоторых случаях может потребоваться tooadd системные переменные, которые будет сохраняться после hello сценария. переменные среды уровня системы tooadd, добавьте переменную hello слишком`/etc/environment`. Например, добавляет hello, следующем за инструкцией `HADOOP_CONF_DIR`:

```bash
echo "HADOOP_CONF_DIR=/etc/hadoop/conf" | sudo tee -a /etc/environment
```

### <a name="access-toolocations-where-hello-custom-scripts-are-stored"></a>Доступ к toolocations, где хранятся пользовательские сценарии hello

Скрипты, используемые toocustomize кластер должен toobe хранятся в одном из следующих элементов hello:

* __Учетной записи хранилища Azure__ связанное с кластером hello.

* __Дополнительная учетная запись хранения__ связанные с кластером hello.

* __ресурсе с общедоступным URI__. Например URL-адрес toodata хранятся в OneDrive, Dropbox или другой файл размещения службы.

* __Хранилища Озера данных Azure__ связанное с кластером HDInsight hello. Дополнительные сведения об использовании Azure Data Lake Store с HDInsight см. в статье [Создание кластера HDInsight с хранилищем озера данных с помощью портала Azure](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md).

    > [!NOTE]
    > tooaccess Hello службы основной HDInsight использует хранилище Озера данных должен иметь доступ на чтение toohello сценария.

Ресурсы, используемые сценарием hello также необходимо быть общедоступным.

Хранение файлов hello в учетной записи хранилища Azure или хранилища Озера данных Azure предоставляет быстрый доступ, как в пределах hello сети Azure.

> [!NOTE]
> Hello URI формат, используемый tooreference hello сценария зависит от того, использование службы hello. Учетные записи хранения, связанные с кластером HDInsight hello, используйте `wasb://` или `wasbs://`. для общедоступного универсального кода ресурса (URI) — `http://` или `https://`, а для Data Lake Store — `adl://`.

### <a name="checking-hello-operating-system-version"></a>Проверка версии операционной системы hello

Для разных версий HDInsight используются конкретные версии Ubuntu. В сценарии следует проверить различия между версиями ОС. Например может потребоваться tooinstall связанные toohello версия Ubuntu двоичный файл.

toocheck hello ОС версии, используйте `lsb_release`. Например hello следующий сценарий демонстрирует, как файл tooreference конкретных tar-файл в зависимости от версии ОС hello:

```bash
OS_VERSION=$(lsb_release -sr)
if [[ $OS_VERSION == 14* ]]; then
    echo "OS verion is $OS_VERSION. Using hue-binaries-14-04."
    HUE_TARFILE=hue-binaries-14-04.tgz
elif [[ $OS_VERSION == 16* ]]; then
    echo "OS verion is $OS_VERSION. Using hue-binaries-16-04."
    HUE_TARFILE=hue-binaries-16-04.tgz
fi
```

## <a name="deployScript"></a>Контрольный список для развертывания действия сценария

Ниже приведены шаги hello, который мы воспользовались при подготовке toodeploy эти скрипты.

* Поместите файлы hello, содержащие пользовательские скрипты hello в месте, доступном из узлов кластера hello во время развертывания. Например hello хранилища по умолчанию для кластера hello. Файлы также могут храниться в общедоступных службах размещения.
* Убедитесь, что скрипт hello impotent. Это позволит toobe hello сценарий выполняться несколько раз на hello же узла.
* Использование типа hello tookeep временный файл/TMP directory загруженные файлы, используемые сценарии hello и затем очистить их после выполнения скриптов.
* Если изменяются параметры на уровне операционной системы или файлы конфигурации службы Hadoop, вы можете toorestart службы HDInsight.

## <a name="runScriptAction"></a>Как toorun действие сценария

Можно использовать сценарий toocustomize действия HDInsight кластеры, использующие hello следующие методы:

* Портал Azure
* Azure PowerShell
* Шаблоны диспетчера ресурсов Azure
* Здравствуйте, HDInsight .NET SDK.

Дополнительные сведения об использовании каждого метода см. в разделе [как toouse записать действие в скрипт](hdinsight-hadoop-customize-cluster-linux.md).

## <a name="sampleScripts"></a>Примеры пользовательских сценариев

Корпорация Майкрософт предоставляет примеры сценариев tooinstall компонентов в кластере HDInsight. См. следующие ссылки для выполнения сценариев дополнительные пример hello.

* [Установка и использование Hue в кластерах HDInsight](hdinsight-hadoop-hue-linux.md)
* [Установка и использование Solr в кластерах HDInsight](hdinsight-hadoop-solr-install-linux.md)
* [Установка и использование Giraph в кластерах HDInsight](hdinsight-hadoop-giraph-install-linux.md)
* [Установка и обновление Mono в кластерах HDInsight](hdinsight-hadoop-install-mono.md)

## <a name="troubleshooting"></a>Устранение неполадок

Здесь представлены Hello ошибок, которые могут возникнуть при использовании скриптов, разработанным:

**Ошибка**: `$'\r': command not found`. Иногда дополняется фразой `syntax error: unexpected end of file`.

*Причина*: Эта ошибка возникает, когда hello строки в скрипте заканчиваться CRLF. В системах UNIX ожидать только LF как hello завершения строк.

Эта проблема чаще всего происходит, когда hello скрипт создается в среде Windows, CRLF является общей оси конца для многих текстовых редакторах, в Windows.

*Разрешение*: Если этот вариант в текстовом редакторе, выберите формат Unix или LF hello завершения строк. Можно также использовать следующие команды на tooan CRLF hello toochange системы Unix LF hello:

> [!NOTE]
> Hello следующие команды представляют собой примерно соответствует тем, что им следует менять tooLF символ конца строки CRLF hello. Выберите его в соответствии с hello служебных программ, доступных в системе.

| Команда | Примечания |
| --- | --- |
| `unix2dos -b INFILE` |исходный файл Hello резервного копирования с. Расширение BAK |
| `tr -d '\r' < INFILE > OUTFILE` |В файле OUTFILE для окончания строк будут использоваться только символы LF. |
| `perl -pi -e 's/\r\n/\n/g' INFILE` | Изменяет файл hello напрямую |
| ```sed 's/$'"/`echo \\\r`/" INFILE > OUTFILE``` |В файле OUTFILE для окончания строк будут использоваться только символы LF. |

**Ошибка**: `line 1: #!/usr/bin/env: No such file or directory`.

*Причина*: Эта ошибка возникает при hello скрипт был сохранен как с метки порядка байтов (BOM) UTF-8.

*Разрешение*: hello файл в формате ASCII или UTF-8 без метки порядка БАЙТОВ. Можно также использовать следующую команду на Linux или Unix системы toocreate файл без hello Спецификации hello:

    awk 'NR==1{sub(/^\xef\xbb\xbf/,"")}{print}' INFILE > OUTFILE

Замените `INFILE` с файлом hello содержащий hello Спецификации. `OUTFILE`должно быть новое имя файла, содержащего сценарий hello без hello Спецификации.

## <a name="seeAlso"></a>Дальнейшие действия

* Узнайте, каким образом слишком[HDInsight настроить кластеры, использующие действие сценария](hdinsight-hadoop-customize-cluster-linux.md)
* Используйте hello [HDInsight .NET SDK ссылка](https://msdn.microsoft.com/library/mt271028.aspx) toolearn Дополнительные сведения о создании приложений .NET, которые управляют HDInsight
* Используйте hello [HDInsight REST API](https://msdn.microsoft.com/library/azure/mt622197.aspx) toolearn как действия по управлению tooperform toouse REST на HDInsight кластеров.
