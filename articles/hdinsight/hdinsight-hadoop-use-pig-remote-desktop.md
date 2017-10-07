---
title: "aaaUse Pig для Hadoop с помощью удаленного рабочего стола в HDInsight — Azure | Документы Microsoft"
description: "Узнайте, как toouse hello инструкций латиница Pig toorun Pig команд из кластера под управлением Windows Hadoop tooa подключения удаленного рабочего стола в HDInsight."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: e034a286-de0f-465f-8bf1-3d085ca6abed
ms.service: hdinsight
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 01/17/2017
ms.author: larryfr
ROBOTS: NOINDEX
ms.openlocfilehash: 2a4565fa827cd45fdbe6194b0486df93a6561084
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="run-pig-jobs-from-a-remote-desktop-connection"></a>Выполнение заданий Pig через подключение к удаленному рабочему столу
[!INCLUDE [pig-selector](../../includes/hdinsight-selector-use-pig.md)]

Этот документ содержит пошаговое руководство по использованию инструкций hello Pig команд toorun латиница Pig с кластера HDInsight под управлением Windows tooa подключения удаленного рабочего стола. Латинская pig позволяет приложениям toocreate MapReduce, описав преобразования данных, вместо сопоставления и уменьшения функции.

> [!IMPORTANT]
> Удаленный рабочий стол доступен только в кластерах HDInsight, использование в качестве hello операционной системы Windows. Linux — hello только операционную систему, используемую в HDInsight версии 3.4 или более поздней. Дополнительные сведения см. в разделе [Приближается дата прекращения сопровождения HDI версии 3.3](hdinsight-component-versioning.md#hdinsight-windows-retirement).
>
> Для HDInsight 3.4 или выше в разделе [использование Pig с HDInsight и SSH](hdinsight-hadoop-use-pig-ssh.md) сведения о запуске Pig интерактивного задания непосредственно на hello кластера из командной строки.

## <a id="prereq"></a>Предварительные требования
в этой статье инструкциям toocomplete hello, необходимо будет ниже hello.

* Кластер HDInsight на платформе Windows (Hadoop в HDInsight).
* Клиентский компьютер под управлением Windows 10, Windows 8 или Windows 7.

## <a id="connect"></a>Подключение к удаленному рабочему столу
Включить удаленный рабочий стол для кластера HDInsight hello, а затем соедините tooit в соответствии с инструкциями hello в [tooHDInsight кластерами, с помощью протокола удаленного рабочего СТОЛА подключиться](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp).

## <a id="pig"></a>Команда Pig hello
1. После подключения удаленного рабочего стола, запустите hello **командной строки Hadoop** с помощью hello значка на рабочем столе hello.
2. Используйте следующую команду Pig toostart hello hello.

        %pig_home%\bin\pig

    Откроется командная строка `grunt>` .
3. Введите hello следующей инструкцией:

        LOGS = LOAD 'wasb:///example/data/sample.log';

    Эта команда загружает содержимое файла sample.log hello hello в файл ЖУРНАЛЫ hello. Можно просмотреть содержимое hello hello файла с помощью hello следующую команду:

        DUMP LOGS;
4. Преобразования данных hello, применяя регулярное выражение tooextract только hello уровень ведения журнала из каждой записи:

        LEVELS = foreach LOGS generate REGEX_EXTRACT($0, '(TRACE|DEBUG|INFO|WARN|ERROR|FATAL)', 1)  as LOGLEVEL;

    Можно использовать **ДАМПА** tooview hello данных после преобразования «hello». В этом случае — `DUMP LEVELS;`.
5. Продолжайте применение преобразований с помощью hello, следующие инструкции. Используйте `DUMP` tooview hello результат преобразования hello после каждого шага.

    <table>
    <tr>
    <th>Инструкция</th><th>Действие</th>
    </tr>
    <tr>
    <td>FILTEREDLEVELS = FILTER LEVELS by LOGLEVEL is not null;</td><td>Удаляет строки, содержащие значение null для уровня ведения журнала hello и сохраняет результаты hello в FILTEREDLEVELS.</td>
    </tr>
    <tr>
    <td>GROUPEDLEVELS = GROUP FILTEREDLEVELS by LOGLEVEL;</td><td>Hello групп строк, уровень ведения журнала и сохраняет результаты hello в GROUPEDLEVELS.</td>
    </tr>
    <tr>
    <td>FREQUENCIES = foreach GROUPEDLEVELS generate group as LOGLEVEL, COUNT(FILTEREDLEVELS.LOGLEVEL) as COUNT;</td><td>Создает новый набор данных, который содержит каждое уникальное значение уровня ведения журнала и количество его вхождений. Он сохраняется в FREQUENCIES.</td>
    </tr>
    <tr>
    <td>RESULT = order FREQUENCIES by COUNT desc;</td><td>Упорядочивает уровни журнала hello, count (по убыванию) и сохраняет в РЕЗУЛЬТАТ</td>
    </tr>
    </table>
6.Можно также сохранить результаты hello преобразования с помощью hello `STORE` инструкции. Например, следующая команда hello сохраняет hello `RESULT` toohello **/example/data/pigout** каталог в контейнере хранилища по умолчанию hello для кластера:

        STORE RESULT into 'wasb:///example/data/pigout'

   > [!NOTE]
   > Hello данные хранятся в указанном каталоге hello в файлах с именем **nnnnn часть**. Если hello каталог уже существует, появится сообщение об ошибке.
   >
   >
7. tooexit hello grunt приглашении введите hello, следующем за инструкцией.

        QUIT;

### <a name="pig-latin-batch-files"></a>Пакетные файлы Pig Latin
Также можно использовать hello Pig команда toorun латиница Pig, содержащийся в файле.

1. После выхода из строки grunt hello, откройте **Блокнот** и создайте новый файл с именем **pigbatch.pig** в hello **% PIG_HOME %** каталога.
2. Тип или вставить hello следующие строки в hello **pigbatch.pig** файл и сохраните его:

        LOGS = LOAD 'wasb:///example/data/sample.log';
        LEVELS = foreach LOGS generate REGEX_EXTRACT($0, '(TRACE|DEBUG|INFO|WARN|ERROR|FATAL)', 1)  as LOGLEVEL;
        FILTEREDLEVELS = FILTER LEVELS by LOGLEVEL is not null;
        GROUPEDLEVELS = GROUP FILTEREDLEVELS by LOGLEVEL;
        FREQUENCIES = foreach GROUPEDLEVELS generate group as LOGLEVEL, COUNT(FILTEREDLEVELS.LOGLEVEL) as COUNT;
        RESULT = order FREQUENCIES by COUNT desc;
        DUMP RESULT;
3. Используйте hello, следуя toorun hello **pigbatch.pig** файла с помощью команды pig hello.

        pig %PIG_HOME%\pigbatch.pig

    После завершения пакетного задания hello, вы увидите hello после выходных данных, который должен быть hello же, как при использовании `DUMP RESULT;` в предыдущих шагах hello:

        (TRACE,816)
        (DEBUG,434)
        (INFO,96)
        (WARN,11)
        (ERROR,6)
        (FATAL,2)

## <a id="summary"></a>Сводка
Как видите, hello Pig команда позволяет toointeractively выполнения операций MapReduce или выполнение заданий латиница Pig, которые хранятся в пакетном файле.

## <a id="nextsteps"></a>Дальнейшие действия
Общая информация о Pig в HDInsight:

* [Использование Pig с Hadoop в HDInsight](hdinsight-use-pig.md)

Дополнительная информация о других способах работы с Hadoop в HDInsight:

* [Использование Hive с Hadoop в HDInsight](hdinsight-use-hive.md)
* [Использование MapReduce с Hadoop в HDInsight](hdinsight-use-mapreduce.md)
