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
# <a name="use-python-user-defined-functions-udf-with-hive-and-pig-in-hdinsight"></a><span data-ttu-id="cd91a-103">Использование пользовательских функций Python с Hive и Pig в Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="cd91a-103">Use Python User Defined Functions (UDF) with Hive and Pig in HDInsight</span></span>

<span data-ttu-id="cd91a-104">Узнайте, как toouse Python определяемой пользователем функции (UDF) с Apache Hive и Pig в Hadoop в Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="cd91a-104">Learn how toouse Python user-defined functions (UDF) with Apache Hive and Pig in Hadoop on Azure HDInsight.</span></span>

## <span data-ttu-id="cd91a-105"><a name="python"></a>Python в HDInsight</span><span class="sxs-lookup"><span data-stu-id="cd91a-105"><a name="python"></a>Python on HDInsight</span></span>

<span data-ttu-id="cd91a-106">По умолчанию на кластерах HDInsight 3.0 и более поздних версиях установлен Python версии 2.7.</span><span class="sxs-lookup"><span data-stu-id="cd91a-106">Python2.7 is installed by default on HDInsight 3.0 and later.</span></span> <span data-ttu-id="cd91a-107">Apache Hive можно использовать с этой версией Python для потоковой обработки.</span><span class="sxs-lookup"><span data-stu-id="cd91a-107">Apache Hive can be used with this version of Python for stream processing.</span></span> <span data-ttu-id="cd91a-108">STDOUT и STDIN toopass данных Hive и hello определяемой пользователем функции используется для обработки потока.</span><span class="sxs-lookup"><span data-stu-id="cd91a-108">Stream processing uses STDOUT and STDIN toopass data between Hive and hello UDF.</span></span>

<span data-ttu-id="cd91a-109">В состав HDInsight также входят Jython, который представляет собой реализацию Python, написанную на Java.</span><span class="sxs-lookup"><span data-stu-id="cd91a-109">HDInsight also includes Jython, which is a Python implementation written in Java.</span></span> <span data-ttu-id="cd91a-110">Jython запускается непосредственно на виртуальной машине Java hello и не использовать потоковую передачу.</span><span class="sxs-lookup"><span data-stu-id="cd91a-110">Jython runs directly on hello Java Virtual Machine and does not use streaming.</span></span> <span data-ttu-id="cd91a-111">Jython является hello рекомендуется интерпретатор Python при использовании Python с Pig.</span><span class="sxs-lookup"><span data-stu-id="cd91a-111">Jython is hello recommended Python interpreter when using Python with Pig.</span></span>

> [!WARNING]
> <span data-ttu-id="cd91a-112">Hello в данном пошаговом руководстве сделать hello следующие допущения:</span><span class="sxs-lookup"><span data-stu-id="cd91a-112">hello steps in this document make hello following assumptions:</span></span> 
>
> * <span data-ttu-id="cd91a-113">Можно создавать hello сценариев Python в локальной среде разработки.</span><span class="sxs-lookup"><span data-stu-id="cd91a-113">You create hello Python scripts on your local development environment.</span></span>
> * <span data-ttu-id="cd91a-114">Отправка tooHDInsight hello сценарии, с помощью либо hello `scp` из локального сеанса Bash или hello, предоставленный скрипт PowerShell.</span><span class="sxs-lookup"><span data-stu-id="cd91a-114">You upload hello scripts tooHDInsight using either hello `scp` command from a local Bash session or hello provided PowerShell script.</span></span>
>
> <span data-ttu-id="cd91a-115">Если требуется toouse hello [оболочки облако Azure (bash)](https://docs.microsoft.com/azure/cloud-shell/overview) предварительного просмотра toowork с HDInsight, необходимо:</span><span class="sxs-lookup"><span data-stu-id="cd91a-115">If you want toouse hello [Azure Cloud Shell (bash)](https://docs.microsoft.com/azure/cloud-shell/overview) preview toowork with HDInsight, then you must:</span></span>
>
> * <span data-ttu-id="cd91a-116">Создайте скрипты hello внутри hello облачной среде оболочки.</span><span class="sxs-lookup"><span data-stu-id="cd91a-116">Create hello scripts inside hello cloud shell environment.</span></span>
> * <span data-ttu-id="cd91a-117">Используйте `scp` tooupload hello файлы из hello облако tooHDInsight оболочки.</span><span class="sxs-lookup"><span data-stu-id="cd91a-117">Use `scp` tooupload hello files from hello cloud shell tooHDInsight.</span></span>
> * <span data-ttu-id="cd91a-118">Используйте `ssh` из tooHDInsight tooconnect оболочки облака hello и примеры выполнения hello.</span><span class="sxs-lookup"><span data-stu-id="cd91a-118">Use `ssh` from hello cloud shell tooconnect tooHDInsight and run hello examples.</span></span>

## <span data-ttu-id="cd91a-119"><a name="hivepython"></a>Определяемая пользователем функция Hive</span><span class="sxs-lookup"><span data-stu-id="cd91a-119"><a name="hivepython"></a>Hive UDF</span></span>

<span data-ttu-id="cd91a-120">Python можно использовать в качестве определяемой пользователем функции из куста через hello HiveQL `TRANSFORM` инструкции.</span><span class="sxs-lookup"><span data-stu-id="cd91a-120">Python can be used as a UDF from Hive through hello HiveQL `TRANSFORM` statement.</span></span> <span data-ttu-id="cd91a-121">Например, следующая HiveQL hello вызывает hello `hiveudf.py` файлов, хранящихся в учетной записи хранилища Azure по умолчанию hello для hello кластера.</span><span class="sxs-lookup"><span data-stu-id="cd91a-121">For example, hello following HiveQL invokes hello `hiveudf.py` file stored in hello default Azure Storage account for hello cluster.</span></span>

<span data-ttu-id="cd91a-122">**HDInsight под управлением Linux**</span><span class="sxs-lookup"><span data-stu-id="cd91a-122">**Linux-based HDInsight**</span></span>

```hiveql
add file wasb:///hiveudf.py;

SELECT TRANSFORM (clientid, devicemake, devicemodel)
    USING 'python hiveudf.py' AS
    (clientid string, phoneLable string, phoneHash string)
FROM hivesampletable
ORDER BY clientid LIMIT 50;
```

<span data-ttu-id="cd91a-123">**HDInsight под управлением Windows**</span><span class="sxs-lookup"><span data-stu-id="cd91a-123">**Windows-based HDInsight**</span></span>

```hiveql
add file wasb:///hiveudf.py;

SELECT TRANSFORM (clientid, devicemake, devicemodel)
    USING 'D:\Python27\python.exe hiveudf.py' AS
    (clientid string, phoneLable string, phoneHash string)
FROM hivesampletable
ORDER BY clientid LIMIT 50;
```

> [!NOTE]
> <span data-ttu-id="cd91a-124">В кластерах HDInsight под управлением Windows hello `USING` предложение должно содержать полный путь toopython.exe hello.</span><span class="sxs-lookup"><span data-stu-id="cd91a-124">On Windows-based HDInsight clusters, hello `USING` clause must specify hello full path toopython.exe.</span></span>

<span data-ttu-id="cd91a-125">Вот что делает данный пример:</span><span class="sxs-lookup"><span data-stu-id="cd91a-125">Here's what this example does:</span></span>

1. <span data-ttu-id="cd91a-126">Hello `add file` инструкция в начале hello hello файла добавляет hello `hiveudf.py` toohello файл распределенный кэш, поэтому оно доступно для всех узлов в кластере hello.</span><span class="sxs-lookup"><span data-stu-id="cd91a-126">hello `add file` statement at hello beginning of hello file adds hello `hiveudf.py` file toohello distributed cache, so it's accessible by all nodes in hello cluster.</span></span>
2. <span data-ttu-id="cd91a-127">Hello `SELECT TRANSFORM ... USING` инструкция выбирает данные из hello `hivesampletable`.</span><span class="sxs-lookup"><span data-stu-id="cd91a-127">hello `SELECT TRANSFORM ... USING` statement selects data from hello `hivesampletable`.</span></span> <span data-ttu-id="cd91a-128">Он также передает hello clientid, devicemake и toohello значения devicemodel `hiveudf.py` сценария.</span><span class="sxs-lookup"><span data-stu-id="cd91a-128">It also passes hello clientid, devicemake, and devicemodel values toohello `hiveudf.py` script.</span></span>
3. <span data-ttu-id="cd91a-129">Hello `AS` предложение описывает hello полей, возвращенных `hiveudf.py`.</span><span class="sxs-lookup"><span data-stu-id="cd91a-129">hello `AS` clause describes hello fields returned from `hiveudf.py`.</span></span>

<a name="streamingpy"></a>

### <a name="create-hello-hiveudfpy-file"></a><span data-ttu-id="cd91a-130">Создайте файл hiveudf.py hello</span><span class="sxs-lookup"><span data-stu-id="cd91a-130">Create hello hiveudf.py file</span></span>


<span data-ttu-id="cd91a-131">В среде разработки создайте текстовый файл с именем `hiveudf.py`.</span><span class="sxs-lookup"><span data-stu-id="cd91a-131">On your development environment, create a text file named `hiveudf.py`.</span></span> <span data-ttu-id="cd91a-132">Используйте следующий код как hello содержимое файла hello hello.</span><span class="sxs-lookup"><span data-stu-id="cd91a-132">Use hello following code as hello contents of hello file:</span></span>

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

<span data-ttu-id="cd91a-133">Скрипт выполняет следующие действия hello.</span><span class="sxs-lookup"><span data-stu-id="cd91a-133">This script performs hello following actions:</span></span>

1. <span data-ttu-id="cd91a-134">Чтение данных из STDIN.</span><span class="sxs-lookup"><span data-stu-id="cd91a-134">Read a line of data from STDIN.</span></span>
2. <span data-ttu-id="cd91a-135">символ перевода строки в конце Hello удаляется при помощи `string.strip(line, "\n ")`.</span><span class="sxs-lookup"><span data-stu-id="cd91a-135">hello trailing newline character is removed using `string.strip(line, "\n ")`.</span></span>
3. <span data-ttu-id="cd91a-136">При выполнении потока обработки, одна строка содержит все значения hello символом табуляции между значениями.</span><span class="sxs-lookup"><span data-stu-id="cd91a-136">When doing stream processing, a single line contains all hello values with a tab character between each value.</span></span> <span data-ttu-id="cd91a-137">Поэтому `string.split(line, "\t")` может быть hello используется toosplit ввода данных на каждой вкладке, возврат только поля hello.</span><span class="sxs-lookup"><span data-stu-id="cd91a-137">So `string.split(line, "\t")` can be used toosplit hello input at each tab, returning just hello fields.</span></span>
4. <span data-ttu-id="cd91a-138">После завершения обработки hello выходные данные должны записываться tooSTDOUT как одна строка с вкладкой между каждого поля.</span><span class="sxs-lookup"><span data-stu-id="cd91a-138">When processing is complete, hello output must be written tooSTDOUT as a single line, with a tab between each field.</span></span> <span data-ttu-id="cd91a-139">Например, `print "\t".join([clientid, phone_label, hashlib.md5(phone_label).hexdigest()])`.</span><span class="sxs-lookup"><span data-stu-id="cd91a-139">For example, `print "\t".join([clientid, phone_label, hashlib.md5(phone_label).hexdigest()])`.</span></span>
5. <span data-ttu-id="cd91a-140">Hello `while` цикл повторяется, пока нет `line` доступен для чтения.</span><span class="sxs-lookup"><span data-stu-id="cd91a-140">hello `while` loop repeats until no `line` is read.</span></span>

<span data-ttu-id="cd91a-141">выходные данные сценария Hello представляет собой объединение hello входных значений для `devicemake` и `devicemodel`, и хэш hello объединенному значению.</span><span class="sxs-lookup"><span data-stu-id="cd91a-141">hello script output is a concatenation of hello input values for `devicemake` and `devicemodel`, and a hash of hello concatenated value.</span></span>

<span data-ttu-id="cd91a-142">В разделе [выполнением примеров hello](#running) как toorun в этом примере в кластере HDInsight.</span><span class="sxs-lookup"><span data-stu-id="cd91a-142">See [Running hello examples](#running) for how toorun this example on your HDInsight cluster.</span></span>

## <span data-ttu-id="cd91a-143"><a name="pigpython"></a>Определяемая пользователем функция Pig</span><span class="sxs-lookup"><span data-stu-id="cd91a-143"><a name="pigpython"></a>Pig UDF</span></span>

<span data-ttu-id="cd91a-144">Скрипт на Python можно использовать как определяемой пользователем функции из Pig через hello `GENERATE` инструкции.</span><span class="sxs-lookup"><span data-stu-id="cd91a-144">A Python script can be used as a UDF from Pig through hello `GENERATE` statement.</span></span> <span data-ttu-id="cd91a-145">Можно запустить скрипт hello, с помощью Jython или C Python.</span><span class="sxs-lookup"><span data-stu-id="cd91a-145">You can run hello script using either Jython or C Python.</span></span>

* <span data-ttu-id="cd91a-146">Jython выполняется на hello виртуальной машины Java и изначально могут быть вызваны из Pig.</span><span class="sxs-lookup"><span data-stu-id="cd91a-146">Jython runs on hello JVM, and can natively be called from Pig.</span></span>
* <span data-ttu-id="cd91a-147">C Python является внешний процесс, поэтому hello данные из Pig на hello виртуальной машины Java отправляется toohello скрипт, выполняемый в процессе Python.</span><span class="sxs-lookup"><span data-stu-id="cd91a-147">C Python is an external process, so hello data from Pig on hello JVM is sent out toohello script running in a Python process.</span></span> <span data-ttu-id="cd91a-148">выходные данные Hello hello сценарий Python отправляется обратно в Pig.</span><span class="sxs-lookup"><span data-stu-id="cd91a-148">hello output of hello Python script is sent back into Pig.</span></span>

<span data-ttu-id="cd91a-149">интерпретатор Python hello toospecify, используйте `register` при ссылке на сценарий Python hello.</span><span class="sxs-lookup"><span data-stu-id="cd91a-149">toospecify hello Python interpreter, use `register` when referencing hello Python script.</span></span> <span data-ttu-id="cd91a-150">Hello следующие примеры зарегистрировать скрипты Pig как `myfuncs`:</span><span class="sxs-lookup"><span data-stu-id="cd91a-150">hello following examples register scripts with Pig as `myfuncs`:</span></span>

* <span data-ttu-id="cd91a-151">**toouse Jython**:`register '/path/to/pigudf.py' using jython as myfuncs;`</span><span class="sxs-lookup"><span data-stu-id="cd91a-151">**toouse Jython**: `register '/path/to/pigudf.py' using jython as myfuncs;`</span></span>
* <span data-ttu-id="cd91a-152">**toouse C Python**:`register '/path/to/pigudf.py' using streaming_python as myfuncs;`</span><span class="sxs-lookup"><span data-stu-id="cd91a-152">**toouse C Python**: `register '/path/to/pigudf.py' using streaming_python as myfuncs;`</span></span>

> [!IMPORTANT]
> <span data-ttu-id="cd91a-153">При использовании Jython, toohello pig_jython hello путь к файлу может быть локальным путем или WASB: / / path.</span><span class="sxs-lookup"><span data-stu-id="cd91a-153">When using Jython, hello path toohello pig_jython file can be either a local path or a WASB:// path.</span></span> <span data-ttu-id="cd91a-154">Однако при использовании C Python, должны ссылаться на файл hello локальной файловой системе, что вы используете задание Pig toosubmit hello узла hello.</span><span class="sxs-lookup"><span data-stu-id="cd91a-154">However, when using C Python, you must reference a file on hello local file system of hello node that you are using toosubmit hello Pig job.</span></span>

<span data-ttu-id="cd91a-155">После после регистрации, hello латиница Pig в этом примере hello одинаковым для обоих:</span><span class="sxs-lookup"><span data-stu-id="cd91a-155">Once past registration, hello Pig Latin for this example is hello same for both:</span></span>

```pig
LOGS = LOAD 'wasb:///example/data/sample.log' as (LINE:chararray);
LOG = FILTER LOGS by LINE is not null;
DETAILS = FOREACH LOG GENERATE myfuncs.create_structure(LINE);
DUMP DETAILS;
```

<span data-ttu-id="cd91a-156">Вот что делает данный пример:</span><span class="sxs-lookup"><span data-stu-id="cd91a-156">Here's what this example does:</span></span>

1. <span data-ttu-id="cd91a-157">Первая строка Hello загружает hello образец файла данных `sample.log` в `LOGS`.</span><span class="sxs-lookup"><span data-stu-id="cd91a-157">hello first line loads hello sample data file, `sample.log` into `LOGS`.</span></span> <span data-ttu-id="cd91a-158">Она также определяет каждую запись как массив символов `chararray`.</span><span class="sxs-lookup"><span data-stu-id="cd91a-158">It also defines each record as a `chararray`.</span></span>
2. <span data-ttu-id="cd91a-159">Следующая строка Hello отфильтровывает все пустые значения, хранение hello результат операции hello в `LOG`.</span><span class="sxs-lookup"><span data-stu-id="cd91a-159">hello next line filters out any null values, storing hello result of hello operation into `LOG`.</span></span>
3. <span data-ttu-id="cd91a-160">Затем он выполняет перебор записей hello в `LOG` и использует `GENERATE` tooinvoke hello `create_structure` метод, содержащийся в сценарий Python или Jython hello загружен как `myfuncs`.</span><span class="sxs-lookup"><span data-stu-id="cd91a-160">Next, it iterates over hello records in `LOG` and uses `GENERATE` tooinvoke hello `create_structure` method contained in hello Python/Jython script loaded as `myfuncs`.</span></span> <span data-ttu-id="cd91a-161">`LINE`— используется toopass текущей записи toohello функции hello.</span><span class="sxs-lookup"><span data-stu-id="cd91a-161">`LINE` is used toopass hello current record toohello function.</span></span>
4. <span data-ttu-id="cd91a-162">Наконец, результаты hello являются которого был создан дамп tooSTDOUT, с помощью hello `DUMP` команды.</span><span class="sxs-lookup"><span data-stu-id="cd91a-162">Finally, hello outputs are dumped tooSTDOUT using hello `DUMP` command.</span></span> <span data-ttu-id="cd91a-163">Эта команда отображает результаты hello после завершения операции hello.</span><span class="sxs-lookup"><span data-stu-id="cd91a-163">This command displays hello results after hello operation completes.</span></span>

### <a name="create-hello-pigudfpy-file"></a><span data-ttu-id="cd91a-164">Создайте файл pigudf.py hello</span><span class="sxs-lookup"><span data-stu-id="cd91a-164">Create hello pigudf.py file</span></span>

<span data-ttu-id="cd91a-165">В среде разработки создайте текстовый файл с именем `pigudf.py`.</span><span class="sxs-lookup"><span data-stu-id="cd91a-165">On your development environment, create a text file named `pigudf.py`.</span></span> <span data-ttu-id="cd91a-166">Используйте следующий код как hello содержимое файла hello hello.</span><span class="sxs-lookup"><span data-stu-id="cd91a-166">Use hello following code as hello contents of hello file:</span></span>

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

<span data-ttu-id="cd91a-167">В примере hello латиница Pig, мы определили hello `LINE` вводимый в виде chararray, так как нет согласованной схемы для ввода hello.</span><span class="sxs-lookup"><span data-stu-id="cd91a-167">In hello Pig Latin example, we defined hello `LINE` input as a chararray because there is no consistent schema for hello input.</span></span> <span data-ttu-id="cd91a-168">сценарий Python Hello преобразует данные hello в согласованной схеме для выходных данных.</span><span class="sxs-lookup"><span data-stu-id="cd91a-168">hello Python script transforms hello data into a consistent schema for output.</span></span>

1. <span data-ttu-id="cd91a-169">Hello `@outputSchema` инструкция определяет формат hello данные, возвращаемые tooPig hello.</span><span class="sxs-lookup"><span data-stu-id="cd91a-169">hello `@outputSchema` statement defines hello format of hello data that is returned tooPig.</span></span> <span data-ttu-id="cd91a-170">В данном случае это **data bag**, являющийся типом данных Pig.</span><span class="sxs-lookup"><span data-stu-id="cd91a-170">In this case, it's a **data bag**, which is a Pig data type.</span></span> <span data-ttu-id="cd91a-171">Hello контейнер содержит hello следующие поля, являющиеся chararray (строк):</span><span class="sxs-lookup"><span data-stu-id="cd91a-171">hello bag contains hello following fields, all of which are chararray (strings):</span></span>

   * <span data-ttu-id="cd91a-172">Дата — hello даты hello запись журнала была создана</span><span class="sxs-lookup"><span data-stu-id="cd91a-172">date - hello date hello log entry was created</span></span>
   * <span data-ttu-id="cd91a-173">время - hello время создания записи журнала hello</span><span class="sxs-lookup"><span data-stu-id="cd91a-173">time - hello time hello log entry was created</span></span>
   * <span data-ttu-id="cd91a-174">className - была создана запись hello имя класса hello для</span><span class="sxs-lookup"><span data-stu-id="cd91a-174">classname - hello class name hello entry was created for</span></span>
   * <span data-ttu-id="cd91a-175">уровень - hello уровень ведения журнала</span><span class="sxs-lookup"><span data-stu-id="cd91a-175">level - hello log level</span></span>
   * <span data-ttu-id="cd91a-176">Подробные сведения для hello подробности - запись журнала</span><span class="sxs-lookup"><span data-stu-id="cd91a-176">detail - verbose details for hello log entry</span></span>

2. <span data-ttu-id="cd91a-177">Здравствуйте, затем `def create_structure(input)` определяет функцию hello, Pig передает строки элементов.</span><span class="sxs-lookup"><span data-stu-id="cd91a-177">Next, hello `def create_structure(input)` defines hello function that Pig passes line items to.</span></span>

3. <span data-ttu-id="cd91a-178">Hello данные примера `sample.log`, главным образом соответствует toohello даты, времени, classname, уровня и подробные сведения о схеме, мы хотим tooreturn.</span><span class="sxs-lookup"><span data-stu-id="cd91a-178">hello example data, `sample.log`, mostly conforms toohello date, time, classname, level, and detail schema we want tooreturn.</span></span> <span data-ttu-id="cd91a-179">Однако он содержит несколько строк, начинающихся с `*java.lang.Exception*`.</span><span class="sxs-lookup"><span data-stu-id="cd91a-179">However, it contains a few lines that begin with `*java.lang.Exception*`.</span></span> <span data-ttu-id="cd91a-180">Эти строки должны быть измененный toomatch hello схемы.</span><span class="sxs-lookup"><span data-stu-id="cd91a-180">These lines must be modified toomatch hello schema.</span></span> <span data-ttu-id="cd91a-181">Hello `if` проверке инструкцией наличия их, а затем Массаж hello hello toomove входных данных `*java.lang.Exception*` конец toohello строки, переводя hello данных в строках с нашей ожидаемые выходные данные схемы.</span><span class="sxs-lookup"><span data-stu-id="cd91a-181">hello `if` statement checks for those, then massages hello input data toomove hello `*java.lang.Exception*` string toohello end, bringing hello data in-line with our expected output schema.</span></span>

4. <span data-ttu-id="cd91a-182">Здравствуйте, затем `split` команда является данных hello используется toosplit в первых четырех пространства символов hello.</span><span class="sxs-lookup"><span data-stu-id="cd91a-182">Next, hello `split` command is used toosplit hello data at hello first four space characters.</span></span> <span data-ttu-id="cd91a-183">выходные данные Hello назначается в `date`, `time`, `classname`, `level`, и `detail`.</span><span class="sxs-lookup"><span data-stu-id="cd91a-183">hello output is assigned into `date`, `time`, `classname`, `level`, and `detail`.</span></span>

5. <span data-ttu-id="cd91a-184">Наконец tooPig возвращаются значения hello.</span><span class="sxs-lookup"><span data-stu-id="cd91a-184">Finally, hello values are returned tooPig.</span></span>

<span data-ttu-id="cd91a-185">При возврате данных hello tooPig, как определено в hello имеет согласованных схем `@outputSchema` инструкции.</span><span class="sxs-lookup"><span data-stu-id="cd91a-185">When hello data is returned tooPig, it has a consistent schema as defined in hello `@outputSchema` statement.</span></span>

## <span data-ttu-id="cd91a-186"><a name="running"></a>Загрузка и запуск примеров hello</span><span class="sxs-lookup"><span data-stu-id="cd91a-186"><a name="running"></a>Upload and run hello examples</span></span>

> [!IMPORTANT]
> <span data-ttu-id="cd91a-187">Hello **SSH** действия работают только с кластером HDInsight под управлением Linux.</span><span class="sxs-lookup"><span data-stu-id="cd91a-187">hello **SSH** steps only work with a Linux-based HDInsight cluster.</span></span> <span data-ttu-id="cd91a-188">Hello **PowerShell** шаги работы с кластером HDInsight под управлением Windows или Linux, но требуется клиент Windows.</span><span class="sxs-lookup"><span data-stu-id="cd91a-188">hello **PowerShell** steps work with either a Linux or Windows-based HDInsight cluster, but require a Windows client.</span></span>

### <a name="ssh"></a><span data-ttu-id="cd91a-189">SSH</span><span class="sxs-lookup"><span data-stu-id="cd91a-189">SSH</span></span>

<span data-ttu-id="cd91a-190">Дополнительные сведения об использовании SSH см. в разделе [Подключение к HDInsight (Hadoop) с помощью SSH](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="cd91a-190">For more information on using SSH, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

1. <span data-ttu-id="cd91a-191">Используйте `scp` toocopy hello файлы tooyour HDInsight кластера.</span><span class="sxs-lookup"><span data-stu-id="cd91a-191">Use `scp` toocopy hello files tooyour HDInsight cluster.</span></span> <span data-ttu-id="cd91a-192">Например, hello следующую команду, копии hello файлы tooa кластер с именем **mycluster**.</span><span class="sxs-lookup"><span data-stu-id="cd91a-192">For example, hello following command copies hello files tooa cluster named **mycluster**.</span></span>

    ```bash
    scp hiveudf.py pigudf.py myuser@mycluster-ssh.azurehdinsight.net:
    ```

2. <span data-ttu-id="cd91a-193">Использование кластера toohello tooconnect SSH.</span><span class="sxs-lookup"><span data-stu-id="cd91a-193">Use SSH tooconnect toohello cluster.</span></span>

    ```bash
    ssh myuser@mycluster-ssh.azurehdinsight.net
    ```

3. <span data-ttu-id="cd91a-194">Из сеанса SSH hello добавьте файлы python hello предварительно передана toohello WASB хранилища для кластера hello.</span><span class="sxs-lookup"><span data-stu-id="cd91a-194">From hello SSH session, add hello python files uploaded previously toohello WASB storage for hello cluster.</span></span>

    ```bash
    hdfs dfs -put hiveudf.py /hiveudf.py
    hdfs dfs -put pigudf.py /pigudf.py
    ```

<span data-ttu-id="cd91a-195">После отправки файлов hello, используйте hello ниже приведены действия, toorun hello Hive и Pig заданий.</span><span class="sxs-lookup"><span data-stu-id="cd91a-195">After uploading hello files, use hello following steps toorun hello Hive and Pig jobs.</span></span>

#### <a name="use-hello-hive-udf"></a><span data-ttu-id="cd91a-196">Использовать hello Hive определяемой пользователем функции</span><span class="sxs-lookup"><span data-stu-id="cd91a-196">Use hello Hive UDF</span></span>

1. <span data-ttu-id="cd91a-197">Используйте hello `hive` командная оболочка куст toostart hello.</span><span class="sxs-lookup"><span data-stu-id="cd91a-197">Use hello `hive` command toostart hello hive shell.</span></span> <span data-ttu-id="cd91a-198">Вы увидите `hive>` запрашивать сразу после загрузки hello оболочки.</span><span class="sxs-lookup"><span data-stu-id="cd91a-198">You should see a `hive>` prompt once hello shell has loaded.</span></span>

2. <span data-ttu-id="cd91a-199">Введите следующий запрос на hello hello `hive>` строки:</span><span class="sxs-lookup"><span data-stu-id="cd91a-199">Enter hello following query at hello `hive>` prompt:</span></span>

   ```hive
   add file wasb:///hiveudf.py;
   SELECT TRANSFORM (clientid, devicemake, devicemodel)
       USING 'python hiveudf.py' AS
       (clientid string, phoneLabel string, phoneHash string)
   FROM hivesampletable
   ORDER BY clientid LIMIT 50;
   ```

3. <span data-ttu-id="cd91a-200">После ввода последней строкой hello, будет запущено задание hello.</span><span class="sxs-lookup"><span data-stu-id="cd91a-200">After entering hello last line, hello job should start.</span></span> <span data-ttu-id="cd91a-201">После завершения задания hello, он возвращает выходные данные примерно toohello следующий пример:</span><span class="sxs-lookup"><span data-stu-id="cd91a-201">Once hello job completes, it returns output similar toohello following example:</span></span>

        100041    RIM 9650    d476f3687700442549a83fac4560c51c
        100041    RIM 9650    d476f3687700442549a83fac4560c51c
        100042    Apple iPhone 4.2.x    375ad9a0ddc4351536804f1d5d0ea9b9
        100042    Apple iPhone 4.2.x    375ad9a0ddc4351536804f1d5d0ea9b9
        100042    Apple iPhone 4.2.x    375ad9a0ddc4351536804f1d5d0ea9b9

#### <a name="use-hello-pig-udf"></a><span data-ttu-id="cd91a-202">Использовать hello Pig определяемой пользователем функции</span><span class="sxs-lookup"><span data-stu-id="cd91a-202">Use hello Pig UDF</span></span>

1. <span data-ttu-id="cd91a-203">Используйте hello `pig` командная оболочка toostart hello.</span><span class="sxs-lookup"><span data-stu-id="cd91a-203">Use hello `pig` command toostart hello shell.</span></span> <span data-ttu-id="cd91a-204">Вы видите `grunt>` запрашивать сразу после загрузки hello оболочки.</span><span class="sxs-lookup"><span data-stu-id="cd91a-204">You see a `grunt>` prompt once hello shell has loaded.</span></span>

2. <span data-ttu-id="cd91a-205">Введите следующие инструкции на hello hello `grunt>` строки:</span><span class="sxs-lookup"><span data-stu-id="cd91a-205">Enter hello following statements at hello `grunt>` prompt:</span></span>

   ```pig
   Register wasb:///pigudf.py using jython as myfuncs;
   LOGS = LOAD 'wasb:///example/data/sample.log' as (LINE:chararray);
   LOG = FILTER LOGS by LINE is not null;
   DETAILS = foreach LOG generate myfuncs.create_structure(LINE);
   DUMP DETAILS;
   ```

3. <span data-ttu-id="cd91a-206">После ввода следующей строкой hello, будет запущено задание hello.</span><span class="sxs-lookup"><span data-stu-id="cd91a-206">After entering hello following line, hello job should start.</span></span> <span data-ttu-id="cd91a-207">После завершения задания hello, он возвращает выходные данные примерно toohello следующие данные:</span><span class="sxs-lookup"><span data-stu-id="cd91a-207">Once hello job completes, it returns output similar toohello following data:</span></span>

        ((2012-02-03,20:11:56,SampleClass5,[TRACE],verbose detail for id 990982084))
        ((2012-02-03,20:11:56,SampleClass7,[TRACE],verbose detail for id 1560323914))
        ((2012-02-03,20:11:56,SampleClass8,[DEBUG],detail for id 2083681507))
        ((2012-02-03,20:11:56,SampleClass3,[TRACE],verbose detail for id 1718828806))
        ((2012-02-03,20:11:56,SampleClass3,[INFO],everything normal for id 530537821))

4. <span data-ttu-id="cd91a-208">Используйте `quit` tooexit hello Grunt оболочки, а затем используйте следующие tooedit hello pigudf.py файл в локальной файловой системе hello hello:</span><span class="sxs-lookup"><span data-stu-id="cd91a-208">Use `quit` tooexit hello Grunt shell, and then use hello following tooedit hello pigudf.py file on hello local file system:</span></span>

    ```bash
    nano pigudf.py
    ```

5. <span data-ttu-id="cd91a-209">Один раз в редакторе hello раскомментируйте hello, следующей строкой, удалив hello `#` в начале hello hello строки:</span><span class="sxs-lookup"><span data-stu-id="cd91a-209">Once in hello editor, uncomment hello following line by removing hello `#` character from hello beginning of hello line:</span></span>

    ```bash
    #from pig_util import outputSchema
    ```

    <span data-ttu-id="cd91a-210">После изменения hello, используйте редактор hello tooexit Ctrl + X.</span><span class="sxs-lookup"><span data-stu-id="cd91a-210">Once hello change has been made, use Ctrl+X tooexit hello editor.</span></span> <span data-ttu-id="cd91a-211">Выберите Y, а затем введите toosave hello изменения.</span><span class="sxs-lookup"><span data-stu-id="cd91a-211">Select Y, and then enter toosave hello changes.</span></span>

6. <span data-ttu-id="cd91a-212">Используйте hello `pig` командная оболочка hello toostart еще раз.</span><span class="sxs-lookup"><span data-stu-id="cd91a-212">Use hello `pig` command toostart hello shell again.</span></span> <span data-ttu-id="cd91a-213">После перехода на hello `grunt>` запрос, используйте следующий сценарий Python hello toorun, с помощью интерпретатора C Python hello hello.</span><span class="sxs-lookup"><span data-stu-id="cd91a-213">Once you are at hello `grunt>` prompt, use hello following toorun hello Python script using hello C Python interpreter.</span></span>

   ```pig
   Register 'pigudf.py' using streaming_python as myfuncs;
   LOGS = LOAD 'wasb:///example/data/sample.log' as (LINE:chararray);
   LOG = FILTER LOGS by LINE is not null;
   DETAILS = foreach LOG generate myfuncs.create_structure(LINE);
   DUMP DETAILS;
   ```

    <span data-ttu-id="cd91a-214">После завершения этого задания, как при запуске скрипта hello, с помощью Jython должна появиться одинаковые выходные hello.</span><span class="sxs-lookup"><span data-stu-id="cd91a-214">Once this job completes, you should see hello same output as when you previously ran hello script using Jython.</span></span>

### <a name="powershell-upload-hello-files"></a><span data-ttu-id="cd91a-215">PowerShell: Отправка hello файлов</span><span class="sxs-lookup"><span data-stu-id="cd91a-215">PowerShell: Upload hello files</span></span>

<span data-ttu-id="cd91a-216">Можно использовать PowerShell tooupload hello файлы toohello HDInsight сервера.</span><span class="sxs-lookup"><span data-stu-id="cd91a-216">You can use PowerShell tooupload hello files toohello HDInsight server.</span></span> <span data-ttu-id="cd91a-217">Используйте следующие файлы Python hello tooupload сценария hello.</span><span class="sxs-lookup"><span data-stu-id="cd91a-217">Use hello following script tooupload hello Python files:</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="cd91a-218">Hello шаги в этом разделе с помощью Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="cd91a-218">hello steps in this section use Azure PowerShell.</span></span> <span data-ttu-id="cd91a-219">Дополнительные сведения об использовании Azure PowerShell см. в разделе [как tooinstall и настройка Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="cd91a-219">For more information on using Azure PowerShell, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>

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
> <span data-ttu-id="cd91a-220">Изменение hello `C:\path\to` важные файлы toohello toohello пути в среде разработки.</span><span class="sxs-lookup"><span data-stu-id="cd91a-220">Change hello `C:\path\to` value toohello path toohello files on your development environment.</span></span>

<span data-ttu-id="cd91a-221">Этот скрипт возвращает сведения о кластеру HDInsight, а затем извлекает hello учетной записи и ключ учетной записи хранения по умолчанию hello и передачи hello файлы toohello корневого контейнера hello.</span><span class="sxs-lookup"><span data-stu-id="cd91a-221">This script retrieves information for your HDInsight cluster, then extracts hello account and key for hello default storage account, and uploads hello files toohello root of hello container.</span></span>

> [!NOTE]
> <span data-ttu-id="cd91a-222">Дополнительные сведения о передаче файлов см. в разделе hello [передать данные для заданий Hadoop в HDInsight](hdinsight-upload-data.md) документа.</span><span class="sxs-lookup"><span data-stu-id="cd91a-222">For more information on uploading files, see hello [Upload data for Hadoop jobs in HDInsight](hdinsight-upload-data.md) document.</span></span>

#### <a name="powershell-use-hello-hive-udf"></a><span data-ttu-id="cd91a-223">PowerShell: Использование hello Hive определяемой пользователем функции</span><span class="sxs-lookup"><span data-stu-id="cd91a-223">PowerShell: Use hello Hive UDF</span></span>

<span data-ttu-id="cd91a-224">PowerShell можно также используется tooremotely выполнения запросов Hive.</span><span class="sxs-lookup"><span data-stu-id="cd91a-224">PowerShell can also be used tooremotely run Hive queries.</span></span> <span data-ttu-id="cd91a-225">Hello используйте следующий сценарий PowerShell toorun запрос Hive, который использует **hiveudf.py** сценария:</span><span class="sxs-lookup"><span data-stu-id="cd91a-225">Use hello following PowerShell script toorun a Hive query that uses **hiveudf.py** script:</span></span>

> [!IMPORTANT]
> <span data-ttu-id="cd91a-226">Перед запуском, hello сценарий предложит hello HTTPs/Admin сведения об учетной записи для кластера HDInsight.</span><span class="sxs-lookup"><span data-stu-id="cd91a-226">Before running, hello script prompts you for hello HTTPs/Admin account information for your HDInsight cluster.</span></span>

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

<span data-ttu-id="cd91a-227">Здравствуйте, выходные данные для hello **Hive** задания появится примерно toohello в следующем примере:</span><span class="sxs-lookup"><span data-stu-id="cd91a-227">hello output for hello **Hive** job should appear similar toohello following example:</span></span>

    100041    RIM 9650    d476f3687700442549a83fac4560c51c
    100041    RIM 9650    d476f3687700442549a83fac4560c51c
    100042    Apple iPhone 4.2.x    375ad9a0ddc4351536804f1d5d0ea9b9
    100042    Apple iPhone 4.2.x    375ad9a0ddc4351536804f1d5d0ea9b9
    100042    Apple iPhone 4.2.x    375ad9a0ddc4351536804f1d5d0ea9b9

#### <a name="pig-jython"></a><span data-ttu-id="cd91a-228">Pig (Jython)</span><span class="sxs-lookup"><span data-stu-id="cd91a-228">Pig (Jython)</span></span>

<span data-ttu-id="cd91a-229">PowerShell также может быть используется toorun Pig латиница заданий.</span><span class="sxs-lookup"><span data-stu-id="cd91a-229">PowerShell can also be used toorun Pig Latin jobs.</span></span> <span data-ttu-id="cd91a-230">Латинская Pig задания, использующего hello toorun **pigudf.py** сценария, используйте следующий сценарий PowerShell hello:</span><span class="sxs-lookup"><span data-stu-id="cd91a-230">toorun a Pig Latin job that uses hello **pigudf.py** script, use hello following PowerShell script:</span></span>

> [!NOTE]
> <span data-ttu-id="cd91a-231">Когда удаленно отправке задания с помощью PowerShell, не возможные toouse C Python интерпретатора hello.</span><span class="sxs-lookup"><span data-stu-id="cd91a-231">When remotely submitting a job using PowerShell, it is not possible toouse C Python as hello interpreter.</span></span>

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

<span data-ttu-id="cd91a-232">Здравствуйте, выходные данные для hello **Pig** задания появится примерно toohello следующие данные:</span><span class="sxs-lookup"><span data-stu-id="cd91a-232">hello output for hello **Pig** job should appear similar toohello following data:</span></span>

    ((2012-02-03,20:11:56,SampleClass5,[TRACE],verbose detail for id 990982084))
    ((2012-02-03,20:11:56,SampleClass7,[TRACE],verbose detail for id 1560323914))
    ((2012-02-03,20:11:56,SampleClass8,[DEBUG],detail for id 2083681507))
    ((2012-02-03,20:11:56,SampleClass3,[TRACE],verbose detail for id 1718828806))
    ((2012-02-03,20:11:56,SampleClass3,[INFO],everything normal for id 530537821))

## <span data-ttu-id="cd91a-233"><a name="troubleshooting"></a>Устранение неполадок</span><span class="sxs-lookup"><span data-stu-id="cd91a-233"><a name="troubleshooting"></a>Troubleshooting</span></span>

### <a name="errors-when-running-jobs"></a><span data-ttu-id="cd91a-234">Ошибки при выполнении заданий</span><span class="sxs-lookup"><span data-stu-id="cd91a-234">Errors when running jobs</span></span>

<span data-ttu-id="cd91a-235">При запуске задания hive hello, может появиться ошибка примерно toohello после текста:</span><span class="sxs-lookup"><span data-stu-id="cd91a-235">When running hello hive job, you may encounter an error similar toohello following text:</span></span>

    Caused by: org.apache.hadoop.hive.ql.metadata.HiveException: [Error 20001]: An error occurred while reading or writing tooyour custom script. It may have crashed with an error.

<span data-ttu-id="cd91a-236">Это проблема может быть вызвана по hello разрывы строк в файле Python hello.</span><span class="sxs-lookup"><span data-stu-id="cd91a-236">This problem may be caused by hello line endings in hello Python file.</span></span> <span data-ttu-id="cd91a-237">Многие редакторы Windows по умолчанию toousing CRLF конца линии hello, но приложения Linux обычно ожидается, что LF.</span><span class="sxs-lookup"><span data-stu-id="cd91a-237">Many Windows editors default toousing CRLF as hello line ending, but Linux applications usually expect LF.</span></span>

<span data-ttu-id="cd91a-238">Можно использовать следующие PowerShell инструкций tooremove hello CR символы перед отправкой файла tooHDInsight hello hello.</span><span class="sxs-lookup"><span data-stu-id="cd91a-238">You can use hello following PowerShell statements tooremove hello CR characters before uploading hello file tooHDInsight:</span></span>

```powershell
$original_file ='c:\path\to\hiveudf.py'
$text = [IO.File]::ReadAllText($original_file) -replace "`r`n", "`n"
[IO.File]::WriteAllText($original_file, $text)
```

### <a name="powershell-scripts"></a><span data-ttu-id="cd91a-239">Сценарии PowerShell</span><span class="sxs-lookup"><span data-stu-id="cd91a-239">PowerShell scripts</span></span>

<span data-ttu-id="cd91a-240">Оба примера hello сценариев PowerShell, используемых toorun hello примеры содержат соответствующей строки, которая отображает вывод ошибок для задания hello.</span><span class="sxs-lookup"><span data-stu-id="cd91a-240">Both of hello example PowerShell scripts used toorun hello examples contain a commented line that displays error output for hello job.</span></span> <span data-ttu-id="cd91a-241">Если выходные данные hello ожидается для задания hello не видны, раскомментируйте hello следующую команду и если hello сведения об ошибке указывает на проблему в разделе.</span><span class="sxs-lookup"><span data-stu-id="cd91a-241">If you are not seeing hello expected output for hello job, uncomment hello following line and see if hello error information indicates a problem.</span></span>

```powershell
# Get-AzureRmHDInsightJobOutput `
        -Clustername $clusterName `
        -JobId $job.JobId `
        -HttpCredential $creds `
        -DisplayOutputType StandardError
```

<span data-ttu-id="cd91a-242">сведения об ошибке Hello (STDERR) и результат hello hello задания (STDOUT), также регистрируется tooyour HDInsight хранилища.</span><span class="sxs-lookup"><span data-stu-id="cd91a-242">hello error information (STDERR) and hello result of hello job (STDOUT) are also logged tooyour HDInsight storage.</span></span>

| <span data-ttu-id="cd91a-243">Для данного задания...</span><span class="sxs-lookup"><span data-stu-id="cd91a-243">For this job...</span></span> | <span data-ttu-id="cd91a-244">Рассмотрим эти файлы в контейнер больших двоичных объектов hello</span><span class="sxs-lookup"><span data-stu-id="cd91a-244">Look at these files in hello blob container</span></span> |
| --- | --- |
| <span data-ttu-id="cd91a-245">Hive</span><span class="sxs-lookup"><span data-stu-id="cd91a-245">Hive</span></span> |<span data-ttu-id="cd91a-246">/HivePython/stderr</span><span class="sxs-lookup"><span data-stu-id="cd91a-246">/HivePython/stderr</span></span><p><span data-ttu-id="cd91a-247">/HivePython/stdout</span><span class="sxs-lookup"><span data-stu-id="cd91a-247">/HivePython/stdout</span></span> |
| <span data-ttu-id="cd91a-248">Pig,</span><span class="sxs-lookup"><span data-stu-id="cd91a-248">Pig</span></span> |<span data-ttu-id="cd91a-249">/PigPython/stderr</span><span class="sxs-lookup"><span data-stu-id="cd91a-249">/PigPython/stderr</span></span><p><span data-ttu-id="cd91a-250">/PigPython/stdout</span><span class="sxs-lookup"><span data-stu-id="cd91a-250">/PigPython/stdout</span></span> |

## <span data-ttu-id="cd91a-251"><a name="next"></a>Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="cd91a-251"><a name="next"></a>Next steps</span></span>

<span data-ttu-id="cd91a-252">При необходимости tooload Python модули, которые не предоставляются по умолчанию. в разделе [как toodeploy модуль tooAzure HDInsight](http://blogs.msdn.com/b/benjguin/archive/2014/03/03/how-to-deploy-a-python-module-to-windows-azure-hdinsight.aspx).</span><span class="sxs-lookup"><span data-stu-id="cd91a-252">If you need tooload Python modules that aren't provided by default, see [How toodeploy a module tooAzure HDInsight](http://blogs.msdn.com/b/benjguin/archive/2014/03/03/how-to-deploy-a-python-module-to-windows-azure-hdinsight.aspx).</span></span>

<span data-ttu-id="cd91a-253">Другие способы toouse Pig, Hive и toolearn об использовании MapReduce в разделе hello следующие документы:</span><span class="sxs-lookup"><span data-stu-id="cd91a-253">For other ways toouse Pig, Hive, and toolearn about using MapReduce, see hello following documents:</span></span>

* [<span data-ttu-id="cd91a-254">Использование Hive с HDInsight</span><span class="sxs-lookup"><span data-stu-id="cd91a-254">Use Hive with HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="cd91a-255">Использование Pig с HDInsight</span><span class="sxs-lookup"><span data-stu-id="cd91a-255">Use Pig with HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="cd91a-256">Использование MapReduce с HDInsight</span><span class="sxs-lookup"><span data-stu-id="cd91a-256">Use MapReduce with HDInsight</span></span>](hdinsight-use-mapreduce.md)
