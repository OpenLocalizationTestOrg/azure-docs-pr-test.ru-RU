---
title: "aaaPython определяемой пользователем функции с Apache Hive и Pig - Azure HDInsight | Документы Microsoft"
description: "Узнайте, как toouse Python пользовательской функции (UDF) из Hive и Pig в HDInsight Hadoop технологии hello стека в Azure."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: c44d6606-28cd-429b-b535-235e8f34a664
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 07/17/2017
ms.author: larryfr
ms.custom: H1Hack27Feb2017,hdinsightactive
ms.openlocfilehash: 26d8160cc6ed7fc22c3f06f7c1c9954c224b2366
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-python-user-defined-functions-udf-with-hive-and-pig-in-hdinsight"></a>Использование пользовательских функций Python с Hive и Pig в Azure HDInsight

Узнайте, как toouse Python определяемой пользователем функции (UDF) с Apache Hive и Pig в Hadoop в Azure HDInsight.

## <a name="python"></a>Python в HDInsight

По умолчанию на кластерах HDInsight 3.0 и более поздних версиях установлен Python версии 2.7. Apache Hive можно использовать с этой версией Python для потоковой обработки. STDOUT и STDIN toopass данных Hive и hello определяемой пользователем функции используется для обработки потока.

В состав HDInsight также входят Jython, который представляет собой реализацию Python, написанную на Java. Jython запускается непосредственно на виртуальной машине Java hello и не использовать потоковую передачу. Jython является hello рекомендуется интерпретатор Python при использовании Python с Pig.

> [!WARNING]
> Hello в данном пошаговом руководстве сделать hello следующие допущения: 
>
> * Можно создавать hello сценариев Python в локальной среде разработки.
> * Отправка tooHDInsight hello сценарии, с помощью либо hello `scp` из локального сеанса Bash или hello, предоставленный скрипт PowerShell.
>
> Если требуется toouse hello [оболочки облако Azure (bash)](https://docs.microsoft.com/azure/cloud-shell/overview) предварительного просмотра toowork с HDInsight, необходимо:
>
> * Создайте скрипты hello внутри hello облачной среде оболочки.
> * Используйте `scp` tooupload hello файлы из hello облако tooHDInsight оболочки.
> * Используйте `ssh` из tooHDInsight tooconnect оболочки облака hello и примеры выполнения hello.

## <a name="hivepython"></a>Определяемая пользователем функция Hive

Python можно использовать в качестве определяемой пользователем функции из куста через hello HiveQL `TRANSFORM` инструкции. Например, следующая HiveQL hello вызывает hello `hiveudf.py` файлов, хранящихся в учетной записи хранилища Azure по умолчанию hello для hello кластера.

**HDInsight под управлением Linux**

```hiveql
add file wasb:///hiveudf.py;

SELECT TRANSFORM (clientid, devicemake, devicemodel)
    USING 'python hiveudf.py' AS
    (clientid string, phoneLable string, phoneHash string)
FROM hivesampletable
ORDER BY clientid LIMIT 50;
```

**HDInsight под управлением Windows**

```hiveql
add file wasb:///hiveudf.py;

SELECT TRANSFORM (clientid, devicemake, devicemodel)
    USING 'D:\Python27\python.exe hiveudf.py' AS
    (clientid string, phoneLable string, phoneHash string)
FROM hivesampletable
ORDER BY clientid LIMIT 50;
```

> [!NOTE]
> В кластерах HDInsight под управлением Windows hello `USING` предложение должно содержать полный путь toopython.exe hello.

Вот что делает данный пример:

1. Hello `add file` инструкция в начале hello hello файла добавляет hello `hiveudf.py` toohello файл распределенный кэш, поэтому оно доступно для всех узлов в кластере hello.
2. Hello `SELECT TRANSFORM ... USING` инструкция выбирает данные из hello `hivesampletable`. Он также передает hello clientid, devicemake и toohello значения devicemodel `hiveudf.py` сценария.
3. Hello `AS` предложение описывает hello полей, возвращенных `hiveudf.py`.

<a name="streamingpy"></a>

### <a name="create-hello-hiveudfpy-file"></a>Создайте файл hiveudf.py hello


В среде разработки создайте текстовый файл с именем `hiveudf.py`. Используйте следующий код как hello содержимое файла hello hello.

```python
#!/usr/bin/env python
import sys
import string
import hashlib

while True:
    line = sys.stdin.readline()
    if not line:
        break

    line = string.strip(line, "\n ")
    clientid, devicemake, devicemodel = string.split(line, "\t")
    phone_label = devicemake + ' ' + devicemodel
    print "\t".join([clientid, phone_label, hashlib.md5(phone_label).hexdigest()])
```

Скрипт выполняет следующие действия hello.

1. Чтение данных из STDIN.
2. символ перевода строки в конце Hello удаляется при помощи `string.strip(line, "\n ")`.
3. При выполнении потока обработки, одна строка содержит все значения hello символом табуляции между значениями. Поэтому `string.split(line, "\t")` может быть hello используется toosplit ввода данных на каждой вкладке, возврат только поля hello.
4. После завершения обработки hello выходные данные должны записываться tooSTDOUT как одна строка с вкладкой между каждого поля. Например, `print "\t".join([clientid, phone_label, hashlib.md5(phone_label).hexdigest()])`.
5. Hello `while` цикл повторяется, пока нет `line` доступен для чтения.

выходные данные сценария Hello представляет собой объединение hello входных значений для `devicemake` и `devicemodel`, и хэш hello объединенному значению.

В разделе [выполнением примеров hello](#running) как toorun в этом примере в кластере HDInsight.

## <a name="pigpython"></a>Определяемая пользователем функция Pig

Скрипт на Python можно использовать как определяемой пользователем функции из Pig через hello `GENERATE` инструкции. Можно запустить скрипт hello, с помощью Jython или C Python.

* Jython выполняется на hello виртуальной машины Java и изначально могут быть вызваны из Pig.
* C Python является внешний процесс, поэтому hello данные из Pig на hello виртуальной машины Java отправляется toohello скрипт, выполняемый в процессе Python. выходные данные Hello hello сценарий Python отправляется обратно в Pig.

интерпретатор Python hello toospecify, используйте `register` при ссылке на сценарий Python hello. Hello следующие примеры зарегистрировать скрипты Pig как `myfuncs`:

* **toouse Jython**:`register '/path/to/pigudf.py' using jython as myfuncs;`
* **toouse C Python**:`register '/path/to/pigudf.py' using streaming_python as myfuncs;`

> [!IMPORTANT]
> При использовании Jython, toohello pig_jython hello путь к файлу может быть локальным путем или WASB: / / path. Однако при использовании C Python, должны ссылаться на файл hello локальной файловой системе, что вы используете задание Pig toosubmit hello узла hello.

После после регистрации, hello латиница Pig в этом примере hello одинаковым для обоих:

```pig
LOGS = LOAD 'wasb:///example/data/sample.log' as (LINE:chararray);
LOG = FILTER LOGS by LINE is not null;
DETAILS = FOREACH LOG GENERATE myfuncs.create_structure(LINE);
DUMP DETAILS;
```

Вот что делает данный пример:

1. Первая строка Hello загружает hello образец файла данных `sample.log` в `LOGS`. Она также определяет каждую запись как массив символов `chararray`.
2. Следующая строка Hello отфильтровывает все пустые значения, хранение hello результат операции hello в `LOG`.
3. Затем он выполняет перебор записей hello в `LOG` и использует `GENERATE` tooinvoke hello `create_structure` метод, содержащийся в сценарий Python или Jython hello загружен как `myfuncs`. `LINE`— используется toopass текущей записи toohello функции hello.
4. Наконец, результаты hello являются которого был создан дамп tooSTDOUT, с помощью hello `DUMP` команды. Эта команда отображает результаты hello после завершения операции hello.

### <a name="create-hello-pigudfpy-file"></a>Создайте файл pigudf.py hello

В среде разработки создайте текстовый файл с именем `pigudf.py`. Используйте следующий код как hello содержимое файла hello hello.

<a name="streamingpy"></a>

```python
# Uncomment hello following if using C Python
#from pig_util import outputSchema

@outputSchema("log: {(date:chararray, time:chararray, classname:chararray, level:chararray, detail:chararray)}")
def create_structure(input):
    if (input.startswith('java.lang.Exception')):
        input = input[21:len(input)] + ' - java.lang.Exception'
    date, time, classname, level, detail = input.split(' ', 4)
    return date, time, classname, level, detail
```

В примере hello латиница Pig, мы определили hello `LINE` вводимый в виде chararray, так как нет согласованной схемы для ввода hello. сценарий Python Hello преобразует данные hello в согласованной схеме для выходных данных.

1. Hello `@outputSchema` инструкция определяет формат hello данные, возвращаемые tooPig hello. В данном случае это **data bag**, являющийся типом данных Pig. Hello контейнер содержит hello следующие поля, являющиеся chararray (строк):

   * Дата — hello даты hello запись журнала была создана
   * время - hello время создания записи журнала hello
   * className - была создана запись hello имя класса hello для
   * уровень - hello уровень ведения журнала
   * Подробные сведения для hello подробности - запись журнала

2. Здравствуйте, затем `def create_structure(input)` определяет функцию hello, Pig передает строки элементов.

3. Hello данные примера `sample.log`, главным образом соответствует toohello даты, времени, classname, уровня и подробные сведения о схеме, мы хотим tooreturn. Однако он содержит несколько строк, начинающихся с `*java.lang.Exception*`. Эти строки должны быть измененный toomatch hello схемы. Hello `if` проверке инструкцией наличия их, а затем Массаж hello hello toomove входных данных `*java.lang.Exception*` конец toohello строки, переводя hello данных в строках с нашей ожидаемые выходные данные схемы.

4. Здравствуйте, затем `split` команда является данных hello используется toosplit в первых четырех пространства символов hello. выходные данные Hello назначается в `date`, `time`, `classname`, `level`, и `detail`.

5. Наконец tooPig возвращаются значения hello.

При возврате данных hello tooPig, как определено в hello имеет согласованных схем `@outputSchema` инструкции.

## <a name="running"></a>Загрузка и запуск примеров hello

> [!IMPORTANT]
> Hello **SSH** действия работают только с кластером HDInsight под управлением Linux. Hello **PowerShell** шаги работы с кластером HDInsight под управлением Windows или Linux, но требуется клиент Windows.

### <a name="ssh"></a>SSH

Дополнительные сведения об использовании SSH см. в разделе [Подключение к HDInsight (Hadoop) с помощью SSH](hdinsight-hadoop-linux-use-ssh-unix.md).

1. Используйте `scp` toocopy hello файлы tooyour HDInsight кластера. Например, hello следующую команду, копии hello файлы tooa кластер с именем **mycluster**.

    ```bash
    scp hiveudf.py pigudf.py myuser@mycluster-ssh.azurehdinsight.net:
    ```

2. Использование кластера toohello tooconnect SSH.

    ```bash
    ssh myuser@mycluster-ssh.azurehdinsight.net
    ```

3. Из сеанса SSH hello добавьте файлы python hello предварительно передана toohello WASB хранилища для кластера hello.

    ```bash
    hdfs dfs -put hiveudf.py /hiveudf.py
    hdfs dfs -put pigudf.py /pigudf.py
    ```

После отправки файлов hello, используйте hello ниже приведены действия, toorun hello Hive и Pig заданий.

#### <a name="use-hello-hive-udf"></a>Использовать hello Hive определяемой пользователем функции

1. Используйте hello `hive` командная оболочка куст toostart hello. Вы увидите `hive>` запрашивать сразу после загрузки hello оболочки.

2. Введите следующий запрос на hello hello `hive>` строки:

   ```hive
   add file wasb:///hiveudf.py;
   SELECT TRANSFORM (clientid, devicemake, devicemodel)
       USING 'python hiveudf.py' AS
       (clientid string, phoneLabel string, phoneHash string)
   FROM hivesampletable
   ORDER BY clientid LIMIT 50;
   ```

3. После ввода последней строкой hello, будет запущено задание hello. После завершения задания hello, он возвращает выходные данные примерно toohello следующий пример:

        100041    RIM 9650    d476f3687700442549a83fac4560c51c
        100041    RIM 9650    d476f3687700442549a83fac4560c51c
        100042    Apple iPhone 4.2.x    375ad9a0ddc4351536804f1d5d0ea9b9
        100042    Apple iPhone 4.2.x    375ad9a0ddc4351536804f1d5d0ea9b9
        100042    Apple iPhone 4.2.x    375ad9a0ddc4351536804f1d5d0ea9b9

#### <a name="use-hello-pig-udf"></a>Использовать hello Pig определяемой пользователем функции

1. Используйте hello `pig` командная оболочка toostart hello. Вы видите `grunt>` запрашивать сразу после загрузки hello оболочки.

2. Введите следующие инструкции на hello hello `grunt>` строки:

   ```pig
   Register wasb:///pigudf.py using jython as myfuncs;
   LOGS = LOAD 'wasb:///example/data/sample.log' as (LINE:chararray);
   LOG = FILTER LOGS by LINE is not null;
   DETAILS = foreach LOG generate myfuncs.create_structure(LINE);
   DUMP DETAILS;
   ```

3. После ввода следующей строкой hello, будет запущено задание hello. После завершения задания hello, он возвращает выходные данные примерно toohello следующие данные:

        ((2012-02-03,20:11:56,SampleClass5,[TRACE],verbose detail for id 990982084))
        ((2012-02-03,20:11:56,SampleClass7,[TRACE],verbose detail for id 1560323914))
        ((2012-02-03,20:11:56,SampleClass8,[DEBUG],detail for id 2083681507))
        ((2012-02-03,20:11:56,SampleClass3,[TRACE],verbose detail for id 1718828806))
        ((2012-02-03,20:11:56,SampleClass3,[INFO],everything normal for id 530537821))

4. Используйте `quit` tooexit hello Grunt оболочки, а затем используйте следующие tooedit hello pigudf.py файл в локальной файловой системе hello hello:

    ```bash
    nano pigudf.py
    ```

5. Один раз в редакторе hello раскомментируйте hello, следующей строкой, удалив hello `#` в начале hello hello строки:

    ```bash
    #from pig_util import outputSchema
    ```

    После изменения hello, используйте редактор hello tooexit Ctrl + X. Выберите Y, а затем введите toosave hello изменения.

6. Используйте hello `pig` командная оболочка hello toostart еще раз. После перехода на hello `grunt>` запрос, используйте следующий сценарий Python hello toorun, с помощью интерпретатора C Python hello hello.

   ```pig
   Register 'pigudf.py' using streaming_python as myfuncs;
   LOGS = LOAD 'wasb:///example/data/sample.log' as (LINE:chararray);
   LOG = FILTER LOGS by LINE is not null;
   DETAILS = foreach LOG generate myfuncs.create_structure(LINE);
   DUMP DETAILS;
   ```

    После завершения этого задания, как при запуске скрипта hello, с помощью Jython должна появиться одинаковые выходные hello.

### <a name="powershell-upload-hello-files"></a>PowerShell: Отправка hello файлов

Можно использовать PowerShell tooupload hello файлы toohello HDInsight сервера. Используйте следующие файлы Python hello tooupload сценария hello.

> [!IMPORTANT] 
> Hello шаги в этом разделе с помощью Azure PowerShell. Дополнительные сведения об использовании Azure PowerShell см. в разделе [как tooinstall и настройка Azure PowerShell](/powershell/azure/overview).

```powershell
# Login tooyour Azure subscription
# Is there an active Azure subscription?
$sub = Get-AzureRmSubscription -ErrorAction SilentlyContinue
if(-not($sub))
{
    Add-AzureRmAccount
}

# Get cluster info
$clusterName = Read-Host -Prompt "Enter hello HDInsight cluster name"
# Change hello path toomatch hello file location on your system
$pathToStreamingFile = "C:\path\to\hiveudf.py"
$pathToJythonFile = "C:\path\to\pigudf.py"

$clusterInfo = Get-AzureRmHDInsightCluster -ClusterName $clusterName
$resourceGroup = $clusterInfo.ResourceGroup
$storageAccountName=$clusterInfo.DefaultStorageAccount.split('.')[0]
$container=$clusterInfo.DefaultStorageContainer
$storageAccountKey=(Get-AzureRmStorageAccountKey `
    -Name $storageAccountName `
-ResourceGroupName $resourceGroup)[0].Value

#Create a storage content and upload hello file
$context = New-AzureStorageContext `
    -StorageAccountName $storageAccountName `
    -StorageAccountKey $storageAccountKey

Set-AzureStorageBlobContent `
    -File $pathToStreamingFile `
    -Blob "hiveudf.py" `
    -Container $container `
    -Context $context

Set-AzureStorageBlobContent `
    -File $pathToJythonFile `
    -Blob "pigudf.py" `
    -Container $container `
    -Context $context
```
> [!IMPORTANT]
> Изменение hello `C:\path\to` важные файлы toohello toohello пути в среде разработки.

Этот скрипт возвращает сведения о кластеру HDInsight, а затем извлекает hello учетной записи и ключ учетной записи хранения по умолчанию hello и передачи hello файлы toohello корневого контейнера hello.

> [!NOTE]
> Дополнительные сведения о передаче файлов см. в разделе hello [передать данные для заданий Hadoop в HDInsight](hdinsight-upload-data.md) документа.

#### <a name="powershell-use-hello-hive-udf"></a>PowerShell: Использование hello Hive определяемой пользователем функции

PowerShell можно также используется tooremotely выполнения запросов Hive. Hello используйте следующий сценарий PowerShell toorun запрос Hive, который использует **hiveudf.py** сценария:

> [!IMPORTANT]
> Перед запуском, hello сценарий предложит hello HTTPs/Admin сведения об учетной записи для кластера HDInsight.

```powershell
# Login tooyour Azure subscription
# Is there an active Azure subscription?
$sub = Get-AzureRmSubscription -ErrorAction SilentlyContinue
if(-not($sub))
{
    Add-AzureRmAccount
}

# Get cluster info
$clusterName = Read-Host -Prompt "Enter hello HDInsight cluster name"
$creds=Get-Credential -Message "Enter hello login for hello cluster"

# If using a Windows-based HDInsight cluster, change hello USING statement to:
# "USING 'D:\Python27\python.exe hiveudf.py' AS " +
$HiveQuery = "add file wasb:///hiveudf.py;" +
                "SELECT TRANSFORM (clientid, devicemake, devicemodel) " +
                "USING 'python hiveudf.py' AS " +
                "(clientid string, phoneLabel string, phoneHash string) " +
                "FROM hivesampletable " +
                "ORDER BY clientid LIMIT 50;"

$jobDefinition = New-AzureRmHDInsightHiveJobDefinition `
    -Query $HiveQuery

$job = Start-AzureRmHDInsightJob `
    -ClusterName $clusterName `
    -JobDefinition $jobDefinition `
    -HttpCredential $creds
Write-Host "Wait for hello Hive job toocomplete ..." -ForegroundColor Green
Wait-AzureRmHDInsightJob `
    -JobId $job.JobId `
    -ClusterName $clusterName `
    -HttpCredential $creds
# Uncomment hello following toosee stderr output
# Get-AzureRmHDInsightJobOutput `
#   -Clustername $clusterName `
#   -JobId $job.JobId `
#   -HttpCredential $creds `
#   -DisplayOutputType StandardError
Write-Host "Display hello standard output ..." -ForegroundColor Green
Get-AzureRmHDInsightJobOutput `
    -Clustername $clusterName `
    -JobId $job.JobId `
    -HttpCredential $creds
```

Здравствуйте, выходные данные для hello **Hive** задания появится примерно toohello в следующем примере:

    100041    RIM 9650    d476f3687700442549a83fac4560c51c
    100041    RIM 9650    d476f3687700442549a83fac4560c51c
    100042    Apple iPhone 4.2.x    375ad9a0ddc4351536804f1d5d0ea9b9
    100042    Apple iPhone 4.2.x    375ad9a0ddc4351536804f1d5d0ea9b9
    100042    Apple iPhone 4.2.x    375ad9a0ddc4351536804f1d5d0ea9b9

#### <a name="pig-jython"></a>Pig (Jython)

PowerShell также может быть используется toorun Pig латиница заданий. Латинская Pig задания, использующего hello toorun **pigudf.py** сценария, используйте следующий сценарий PowerShell hello:

> [!NOTE]
> Когда удаленно отправке задания с помощью PowerShell, не возможные toouse C Python интерпретатора hello.

```powershell
# Login tooyour Azure subscription
# Is there an active Azure subscription?
$sub = Get-AzureRmSubscription -ErrorAction SilentlyContinue
if(-not($sub))
{
    Add-AzureRmAccount
}

# Get cluster info
$clusterName = Read-Host -Prompt "Enter hello HDInsight cluster name"
$creds=Get-Credential -Message "Enter hello login for hello cluster"

$PigQuery = "Register wasb:///pigudf.py using jython as myfuncs;" +
            "LOGS = LOAD 'wasb:///example/data/sample.log' as (LINE:chararray);" +
            "LOG = FILTER LOGS by LINE is not null;" +
            "DETAILS = foreach LOG generate myfuncs.create_structure(LINE);" +
            "DUMP DETAILS;"

$jobDefinition = New-AzureRmHDInsightPigJobDefinition -Query $PigQuery

$job = Start-AzureRmHDInsightJob `
    -ClusterName $clusterName `
    -JobDefinition $jobDefinition `
    -HttpCredential $creds

Write-Host "Wait for hello Pig job toocomplete ..." -ForegroundColor Green
Wait-AzureRmHDInsightJob `
    -Job $job.JobId `
    -ClusterName $clusterName `
    -HttpCredential $creds
# Uncomment hello following toosee stderr output
# Get-AzureRmHDInsightJobOutput `
#    -Clustername $clusterName `
#    -JobId $job.JobId `
#    -HttpCredential $creds `
#    -DisplayOutputType StandardError
Write-Host "Display hello standard output ..." -ForegroundColor Green
Get-AzureRmHDInsightJobOutput `
    -Clustername $clusterName `
    -JobId $job.JobId `
    -HttpCredential $creds
```

Здравствуйте, выходные данные для hello **Pig** задания появится примерно toohello следующие данные:

    ((2012-02-03,20:11:56,SampleClass5,[TRACE],verbose detail for id 990982084))
    ((2012-02-03,20:11:56,SampleClass7,[TRACE],verbose detail for id 1560323914))
    ((2012-02-03,20:11:56,SampleClass8,[DEBUG],detail for id 2083681507))
    ((2012-02-03,20:11:56,SampleClass3,[TRACE],verbose detail for id 1718828806))
    ((2012-02-03,20:11:56,SampleClass3,[INFO],everything normal for id 530537821))

## <a name="troubleshooting"></a>Устранение неполадок

### <a name="errors-when-running-jobs"></a>Ошибки при выполнении заданий

При запуске задания hive hello, может появиться ошибка примерно toohello после текста:

    Caused by: org.apache.hadoop.hive.ql.metadata.HiveException: [Error 20001]: An error occurred while reading or writing tooyour custom script. It may have crashed with an error.

Это проблема может быть вызвана по hello разрывы строк в файле Python hello. Многие редакторы Windows по умолчанию toousing CRLF конца линии hello, но приложения Linux обычно ожидается, что LF.

Можно использовать следующие PowerShell инструкций tooremove hello CR символы перед отправкой файла tooHDInsight hello hello.

```powershell
$original_file ='c:\path\to\hiveudf.py'
$text = [IO.File]::ReadAllText($original_file) -replace "`r`n", "`n"
[IO.File]::WriteAllText($original_file, $text)
```

### <a name="powershell-scripts"></a>Сценарии PowerShell

Оба примера hello сценариев PowerShell, используемых toorun hello примеры содержат соответствующей строки, которая отображает вывод ошибок для задания hello. Если выходные данные hello ожидается для задания hello не видны, раскомментируйте hello следующую команду и если hello сведения об ошибке указывает на проблему в разделе.

```powershell
# Get-AzureRmHDInsightJobOutput `
        -Clustername $clusterName `
        -JobId $job.JobId `
        -HttpCredential $creds `
        -DisplayOutputType StandardError
```

сведения об ошибке Hello (STDERR) и результат hello hello задания (STDOUT), также регистрируется tooyour HDInsight хранилища.

| Для данного задания... | Рассмотрим эти файлы в контейнер больших двоичных объектов hello |
| --- | --- |
| Hive |/HivePython/stderr<p>/HivePython/stdout |
| Pig, |/PigPython/stderr<p>/PigPython/stdout |

## <a name="next"></a>Дальнейшие действия

При необходимости tooload Python модули, которые не предоставляются по умолчанию. в разделе [как toodeploy модуль tooAzure HDInsight](http://blogs.msdn.com/b/benjguin/archive/2014/03/03/how-to-deploy-a-python-module-to-windows-azure-hdinsight.aspx).

Другие способы toouse Pig, Hive и toolearn об использовании MapReduce в разделе hello следующие документы:

* [Использование Hive с HDInsight](hdinsight-use-hive.md)
* [Использование Pig с HDInsight](hdinsight-use-pig.md)
* [Использование MapReduce с HDInsight](hdinsight-use-mapreduce.md)
