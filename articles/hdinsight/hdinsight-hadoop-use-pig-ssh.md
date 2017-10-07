---
title: "aaaUse Hadoop Pig с SSH в кластере HDInsight - Azure | Документы Microsoft"
description: "Узнайте, как подключать кластер Hadoop под управлением Linux tooa SSH, и затем использовать hello Pig команды toorun Pig латиница инструкции в интерактивном режиме или в виде пакета задания."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: b646a93b-4c51-4ba4-84da-3275d9124ebe
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/12/2017
ms.author: larryfr
ms.openlocfilehash: 1da303e239b537e6b331b1d33010058582718c90
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="run-pig-jobs-on-a-linux-based-cluster-with-hello-pig-command-ssh"></a>Выполнять задания Pig в кластере под управлением Linux с hello команда Pig (SSH)

[!INCLUDE [pig-selector](../../includes/hdinsight-selector-use-pig.md)]

Узнайте, как toointeractively запуска задания Pig из кластера HDInsight tooyour подключения SSH. Hello латиница Pig язык программирования позволяет toodescribe преобразования, вывод hello требуемого tooproduce примененных toohello входных данных.

> [!IMPORTANT]
> Hello в данном пошаговом руководстве требуется кластер HDInsight под управлением Linux. Linux — hello только операционную систему, используемую в HDInsight версии 3.4 или более поздней. Дополнительные сведения см. в разделе [Приближается дата прекращения сопровождения HDI версии 3.3](hdinsight-component-versioning.md#hdinsight-windows-retirement).

## <a id="ssh"></a>Подключение по SSH

Используйте кластер HDInsight tooyour tooconnect SSH. Hello следующий пример соединяет tooa кластер с именем **myhdinsight** как hello учетной записи с именем **sshuser**:

    ssh sshuser@myhdinsight-ssh.azurehdinsight.net

**При указании ключа сертификата для проверки подлинности SSH** при создании кластера HDInsight hello, может потребоваться toospecify расположение hello hello закрытого ключа на компьютере клиента.

    ssh sshuser@myhdinsight-ssh.azurehdinsight.net -i ~/mykey.key

**Если задан пароль для проверки подлинности SSH** при создании кластера HDInsight hello предоставляют hello пароль при появлении запроса.

Дополнительные сведения об использовании протокола SSH с HDInsight см. в разделе [Подключение к HDInsight (Hadoop) с помощью SSH](hdinsight-hadoop-linux-use-ssh-unix.md).

## <a id="pig"></a>Команда Pig hello

1. После установления соединения, запустите hello Pig командной строки (CLI) с помощью hello следующую команду:

        pig

    Через некоторое время отобразится командная строка `grunt>` .

2. Введите hello следующей инструкцией:

        LOGS = LOAD '/example/data/sample.log';

    Эта команда загружает содержимое файла sample.log hello hello в ЖУРНАЛЫ. Hello содержимое файла hello можно просмотреть с помощью hello следующей инструкцией:

        DUMP LOGS;

3. Затем преобразуйте hello данных путем применения регулярное выражение tooextract только hello уровень ведения журнала из каждой записи с помощью hello следующей инструкцией:

        LEVELS = foreach LOGS generate REGEX_EXTRACT($0, '(TRACE|DEBUG|INFO|WARN|ERROR|FATAL)', 1)  as LOGLEVEL;

    Можно использовать **ДАМПА** tooview hello данных после преобразования «hello». В этом случае используйте `DUMP LEVELS;`.

4. Продолжить применение преобразований с помощью инструкций hello в hello в следующей таблице:

    | Инструкция Pig Latin | Какие оператор hello |
    | ---- | ---- |
    | `FILTEREDLEVELS = FILTER LEVELS by LOGLEVEL is not null;` | Удаляет строки, содержащие значение null для уровня ведения журнала hello и сохраняет результаты hello в `FILTEREDLEVELS`. |
    | `GROUPEDLEVELS = GROUP FILTEREDLEVELS by LOGLEVEL;` | Hello групп строк, уровень ведения журнала и сохраняет результаты hello в `GROUPEDLEVELS`. |
    | `FREQUENCIES = foreach GROUPEDLEVELS generate group as LOGLEVEL, COUNT(FILTEREDLEVELS.LOGLEVEL) as COUNT;` | Создает набор данных, который содержит каждое уникальное значение уровня ведения журнала и количество его вхождений. Hello набор данных хранится в `FREQUENCIES`. |
    | `RESULT = order FREQUENCIES by COUNT desc;` | Упорядочивает уровни журнала hello по количеству (по убыванию) и сохраняет в `RESULT`. |

    > [!TIP]
    > Используйте `DUMP` tooview hello результат преобразования hello после каждого шага.

5. Можно также сохранить результаты hello преобразования с помощью hello `STORE` инструкции. Например, следующем за инструкцией hello сохраняет hello `RESULT` toohello `/example/data/pigout` на hello хранилища по умолчанию для кластера:

        STORE RESULT into '/example/data/pigout';

   > [!NOTE]
   > Hello данные хранятся в указанном каталоге hello в файлах с именем `part-nnnnn`. Если hello каталог уже существует, возникает ошибка.

6. tooexit hello grunt приглашении введите hello следующей инструкцией:

        QUIT;

### <a name="pig-latin-batch-files"></a>Пакетные файлы Pig Latin

Также можно использовать hello Pig команда toorun латиница Pig, содержащиеся в файле.

1. После выхода из строки grunt hello, используйте hello следующая команда toopipe STDIN в файл с именем `pigbatch.pig`. Этот файл создается в корневом каталоге hello для hello учетной записи пользователя SSH.

        cat > ~/pigbatch.pig

2. Введите или вставьте следующие строки hello и затем использовать сочетание клавиш Ctrl + D, после завершения.

        LOGS = LOAD '/example/data/sample.log';
        LEVELS = foreach LOGS generate REGEX_EXTRACT($0, '(TRACE|DEBUG|INFO|WARN|ERROR|FATAL)', 1)  as LOGLEVEL;
        FILTEREDLEVELS = FILTER LEVELS by LOGLEVEL is not null;
        GROUPEDLEVELS = GROUP FILTEREDLEVELS by LOGLEVEL;
        FREQUENCIES = foreach GROUPEDLEVELS generate group as LOGLEVEL, COUNT(FILTEREDLEVELS.LOGLEVEL) as COUNT;
        RESULT = order FREQUENCIES by COUNT desc;
        DUMP RESULT;

3. Используйте hello следующая команда toorun hello `pigbatch.pig` файл с помощью команды Pig hello.

        pig ~/pigbatch.pig

    После завершения выполнения пакетного задания hello, вы видите hello следующие выходные данные:

        (TRACE,816)
        (DEBUG,434)
        (INFO,96)
        (WARN,11)
        (ERROR,6)
        (FATAL,2)


## <a id="nextsteps"></a>Дальнейшие действия

Общие сведения о Pig в HDInsight см. следующий документ hello.

* [Использование Pig с Hadoop в HDInsight](hdinsight-use-pig.md)

Дополнительные сведения о других способах toowork с Hadoop в HDInsight см hello следующие документы:

* [Использование Hive с Hadoop в HDInsight](hdinsight-use-hive.md)
* [Использование MapReduce с Hadoop в HDInsight](hdinsight-use-mapreduce.md)
