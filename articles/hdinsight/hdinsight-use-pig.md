---
title: "aaaUse Pig для Hadoop в HDInsight | Документы Microsoft"
description: "Узнайте, как toouse Pig с Hadoop в HDInsight."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: acfeb52b-4b81-4a7d-af77-3e9908407404
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/15/2017
ms.author: larryfr
ms.openlocfilehash: 90850f2c742b8954c66ce277127e01b14fc3906f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-pig-with-hadoop-on-hdinsight"></a>Использование Pig с Hadoop в HDInsight

Узнайте, как toouse [Apache Pig](http://pig.apache.org/) с HDInsight...

Pig — это платформа, позволяющая создавать программы для Hadoop с помощью процедурного языка, известного как *Pig Latin*. Pig является альтернативным tooJava для создания *MapReduce* решений, который входит в состав Azure HDInsight. Используйте следующие таблицы toodiscover hello различные способы использования Pig с HDInsight hello.

| **Используйте** , если требуется... | ... **интерактивная** оболочка | ...**пакетная** обработка | ...with этим **кластером операционной системы** | ...из этого **кластера операционной системы** |
|:--- |:---:|:---:|:--- |:--- |
| [SSH](hdinsight-hadoop-use-pig-ssh.md) |✔ |✔ |Linux |Linux, Unix, Mac OS X или Windows |
| [REST API](hdinsight-hadoop-use-pig-curl.md) |&nbsp; |✔ |Linux или Windows |Linux, Unix, Mac OS X или Windows |
| [.NET SDK для Hadoop](hdinsight-hadoop-use-pig-dotnet-sdk.md) |&nbsp; |✔ |Linux или Windows |Windows (сейчас) |
| [Windows PowerShell](hdinsight-hadoop-use-pig-powershell.md) |&nbsp; |✔ |Linux или Windows |Windows |
| [Удаленный рабочий стол](hdinsight-hadoop-use-pig-remote-desktop.md) (HDInsight 3.2 и 3.3) |✔ |✔ |Windows |Windows |

> [!IMPORTANT]
> Linux — hello только операционную систему, используемую в HDInsight версии 3.4 или более поздней. Дополнительные сведения см. в разделе [Приближается дата прекращения сопровождения HDI версии 3.3](hdinsight-component-versioning.md#hdinsight-windows-retirement).

## <a id="why"></a>Почему именно Pig?

Одна из проблем hello обработки данных с помощью MapReduce в Hadoop реализует логику обработки, используя только схему и функцию сокращения. Для обработки сложных, вы часто имеют toobreak обработки в нескольких MapReduce операции, которые будут соединены друг с другом tooachieve hello требуемого результата.

Pig позволяет toodefine обработки как набор преобразований, потоки данных через выходной hello требуемого tooproduce hello.

язык Pig латиница Hello позволяет вам toodescribe hello поток данных из необработанные данные ввода через один или несколько преобразования, вывода tooproduce требуемого hello. Программы Pig Latin следуют общему шаблону:

* **Загрузка**: чтение данных toobe с hello файловой системы

* **Преобразование**: манипулировать данными hello

* **Дамп или хранения**: вывод экрана toohello данных или сохранить его для обработки

### <a name="user-defined-functions"></a>Определяемые пользователем функции

Латинская pig также поддерживает определяемые пользователем функции (UDF), позволяющий tooinvoke внешние компоненты, реализующие логику, которая является сложным toomodel в Латинской Pig.

Дополнительные сведения о Pig Latin см. в [справочном руководстве по Pig Latin 1](http://pig.apache.org/docs/r0.7.0/piglatin_ref1.html) и [справочном руководстве по Pig Latin 2](http://pig.apache.org/docs/r0.7.0/piglatin_ref2.html).

Пример использования определяемых пользователем функций с Pig см. следующие документы hello:

* [Использование DataFu с Pig в HDInsight](hdinsight-hadoop-use-pig-datafu-udf.md) — DataFu представляет собой коллекцию полезных определяемых пользователем функций, поддерживаемых Apache
* [Использование Python с Pig и Hive в HDInsight](hdinsight-python.md)
* [Использование C# с Hive и Pig в HDInsight](hdinsight-hadoop-hive-pig-udf-dotnet-csharp.md)

## <a id="data"></a>Демонстрационные данные

HDInsight предоставляет различные пример наборов данных, хранящихся в hello `/example/data` и `/HdiSamples` каталоги. Эти каталоги находятся в хранилище по умолчанию hello для кластера. Hello Pig в этом документе примере hello *log4j* файл из `/example/data/sample.log`.

Каждый журнал в файле hello состоит из полей строку, содержащую `[LOG LEVEL]` поле tooshow hello тип и hello степенью серьезности, например:

    2012-02-03 20:26:41 SampleClass3 [ERROR] verbose detail for id 1527353937

В предыдущем примере hello hello уровень ведения журнала — ошибка.

> [!NOTE]
> Файл log4j можно также создать с помощью hello [Apache Log4j](http://en.wikipedia.org/wiki/Log4j) средство ведения журнала, а затем передать файл tooyour большого двоичного объекта. В разделе [tooHDInsight передача данных](hdinsight-upload-data.md) инструкции. Дополнительные сведения о том, каким образом большие двоичные объекты в службе хранилища Azure используются с HDInsight, см. в статье [Использование хранилища BLOB-объектов Azure с HDInsight](hdinsight-hadoop-use-blob-storage.md).

## <a id="job"></a>Пример задания

Hello следующее задание Pig латиница загружает hello `sample.log` файл из хранилища по умолчанию hello для кластера HDInsight. Затем он выполняет серию преобразований, которые заканчиваются число как много раз входные данные уровня в hello каждого журнала. tooSTDOUT записываются результаты Hello.

    LOGS = LOAD 'wasb:///example/data/sample.log';
    LEVELS = foreach LOGS generate REGEX_EXTRACT($0, '(TRACE|DEBUG|INFO|WARN|ERROR|FATAL)', 1)  as LOGLEVEL;
    FILTEREDLEVELS = FILTER LEVELS by LOGLEVEL is not null;
    GROUPEDLEVELS = GROUP FILTEREDLEVELS by LOGLEVEL;
    FREQUENCIES = foreach GROUPEDLEVELS generate group as LOGLEVEL, COUNT(FILTEREDLEVELS.LOGLEVEL) as COUNT;
    RESULT = order FREQUENCIES by COUNT desc;
    DUMP RESULT;

Hello следующем рисунке показана сводка какие каждое преобразование делает toohello данных.

![Графическое представление преобразований hello][image-hdi-pig-data-transformation]

## <a id="run"></a>Запустить задание Pig латиница hello

HDInsight может запускать задания Pig Latin с помощью различных методов. Используйте следующие таблицы toodecide, какой метод подходит для вас hello, затем по ссылке hello Пошаговое руководство.

| **Используйте** , если требуется... | ... **интерактивная** оболочка | ...**пакетная** обработка | ...with этим **кластером операционной системы** | … в этом **клиенте** |
|:--- |:---:|:---:|:--- |:--- |
| [SSH](hdinsight-hadoop-use-pig-ssh.md) |✔ |✔ |Linux |Linux, Unix, Mac OS X или Windows |
| [Curl](hdinsight-hadoop-use-pig-curl.md) |&nbsp; |✔ |Linux или Windows |Linux, Unix, Mac OS X или Windows |
| [.NET SDK для Hadoop](hdinsight-hadoop-use-pig-dotnet-sdk.md) |&nbsp; |✔ |Linux или Windows |Windows (сейчас) |
| [Windows PowerShell](hdinsight-hadoop-use-pig-powershell.md) |&nbsp; |✔ |Linux или Windows |Windows |
| [Удаленный рабочий стол](hdinsight-hadoop-use-pig-remote-desktop.md) (HDInsight 3.2 и 3.3) |✔ |✔ |Windows |Windows |

> [!IMPORTANT]
> Linux — hello только операционную систему, используемую в HDInsight версии 3.4 или более поздней. Дополнительные сведения см. в разделе [Приближается дата прекращения сопровождения HDI версии 3.3](hdinsight-component-versioning.md#hdinsight-windows-retirement).

## <a name="pig-and-sql-server-integration-services"></a>Использование Pig и SQL Server Integration Services

Можно использовать SQL Server Integration Services (SSIS) toorun задание Pig. пакет дополнительных компонентов Azure для служб SSIS Hello предоставляет следующие компоненты, которые работают с задания Pig в HDInsight hello.

* [Задача Pig в Azure HDInsight][pigtask]

* [Диспетчер подключений по подпискам Azure][connectionmanager]

Дополнительные сведения о hello пакет дополнительных компонентов Azure для служб SSIS [здесь][ssispack].

## <a id="nextsteps"></a>Дальнейшие действия
Теперь, когда вы узнали, как toouse Pig с HDInsight, hello используйте следующие ссылки tooexplore toowork другими способами с Azure HDInsight.

* [Отправка данных tooHDInsight][hdinsight-upload-data]
* [Использование Hive с HDInsight][hdinsight-use-hive]
* [Использование Sqoop с HDInsight](hdinsight-use-sqoop.md)
* [Использование Oozie с HDInsight](hdinsight-use-oozie.md)
* [Использование заданий MapReduce с HDInsight][hdinsight-use-mapreduce]

[apachepig-home]: http://pig.apache.org/
[putty]: http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html
[curl]: http://curl.haxx.se/
[pigtask]: http://msdn.microsoft.com/library/mt146781(v=sql.120).aspx
[connectionmanager]: http://msdn.microsoft.com/library/mt146773(v=sql.120).aspx
[ssispack]: http://msdn.microsoft.com/library/mt146770(v=sql.120).aspx


[hdinsight-upload-data]: hdinsight-upload-data.md

[hdinsight-admin-powershell]: hdinsight-administer-use-powershell.md

[hdinsight-use-hive]: hdinsight-use-hive.md
[hdinsight-use-mapreduce]: hdinsight-use-mapreduce.md

[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-submit-jobs]: hdinsight-submit-hadoop-jobs-programmatically.md#mapreduce-sdk

[Powershell-install-configure]: /powershell/azureps-cmdlets-docs

[powershell-start]: http://technet.microsoft.com/library/hh847889.aspx


[image-hdi-pig-data-transformation]: ./media/hdinsight-use-pig/HDI.DataTransformation.gif
