---
title: "Использование определяемых пользователем функций Python с Apache Hive и Pig в Azure HDInsight | Документация Майкрософт"
description: "Узнайте, как использовать пользовательские функции (UDF) технологической платформы Hadoop на базе Azure — Python с Hive и Pig в HDInsight."
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
ms.openlocfilehash: 9b67ded05a52f1e68580434667495cf6cf939871
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="use-python-user-defined-functions-udf-with-hive-and-pig-in-hdinsight"></a><span data-ttu-id="907f3-103">Использование пользовательских функций Python с Hive и Pig в Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="907f3-103">Use Python User Defined Functions (UDF) with Hive and Pig in HDInsight</span></span>

<span data-ttu-id="907f3-104">Узнайте, как использовать определяемые пользователем функции (UDF) Python с Apache Hive и Pig в Hadoop на кластерах Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="907f3-104">Learn how to use Python user-defined functions (UDF) with Apache Hive and Pig in Hadoop on Azure HDInsight.</span></span>

## <span data-ttu-id="907f3-105"><a name="python"></a>Python в HDInsight</span><span class="sxs-lookup"><span data-stu-id="907f3-105"><a name="python"></a>Python on HDInsight</span></span>

<span data-ttu-id="907f3-106">По умолчанию на кластерах HDInsight 3.0 и более поздних версиях установлен Python версии 2.7.</span><span class="sxs-lookup"><span data-stu-id="907f3-106">Python2.7 is installed by default on HDInsight 3.0 and later.</span></span> <span data-ttu-id="907f3-107">Apache Hive можно использовать с этой версией Python для потоковой обработки.</span><span class="sxs-lookup"><span data-stu-id="907f3-107">Apache Hive can be used with this version of Python for stream processing.</span></span> <span data-ttu-id="907f3-108">При этом для передачи данных между Hive и определяемой пользователем функцией используется STDOUT и STDIN.</span><span class="sxs-lookup"><span data-stu-id="907f3-108">Stream processing uses STDOUT and STDIN to pass data between Hive and the UDF.</span></span>

<span data-ttu-id="907f3-109">В состав HDInsight также входят Jython, который представляет собой реализацию Python, написанную на Java.</span><span class="sxs-lookup"><span data-stu-id="907f3-109">HDInsight also includes Jython, which is a Python implementation written in Java.</span></span> <span data-ttu-id="907f3-110">Jython выполняется непосредственно на виртуальной машине Java и не использует потоковую передачу.</span><span class="sxs-lookup"><span data-stu-id="907f3-110">Jython runs directly on the Java Virtual Machine and does not use streaming.</span></span> <span data-ttu-id="907f3-111">Jython является рекомендуемым интерпретатором Python при использовании Python с Pig.</span><span class="sxs-lookup"><span data-stu-id="907f3-111">Jython is the recommended Python interpreter when using Python with Pig.</span></span>

> [!WARNING]
> <span data-ttu-id="907f3-112">Шаги в этом документе основаны на следующих предположениях:</span><span class="sxs-lookup"><span data-stu-id="907f3-112">The steps in this document make the following assumptions:</span></span> 
>
> * <span data-ttu-id="907f3-113">Вы создаете скрипты Python в локальной среде разработки.</span><span class="sxs-lookup"><span data-stu-id="907f3-113">You create the Python scripts on your local development environment.</span></span>
> * <span data-ttu-id="907f3-114">Вы отправляете скрипты в HDInsight, используя либо команду `scp` из локального сеанса Bash либо предоставленный сценарий PowerShell.</span><span class="sxs-lookup"><span data-stu-id="907f3-114">You upload the scripts to HDInsight using either the `scp` command from a local Bash session or the provided PowerShell script.</span></span>
>
> <span data-ttu-id="907f3-115">Если вы хотите использовать предварительную версию [Azure Cloud Shell (оболочка)](https://docs.microsoft.com/azure/cloud-shell/overview) для работы с HDInsight, вам необходимо:</span><span class="sxs-lookup"><span data-stu-id="907f3-115">If you want to use the [Azure Cloud Shell (bash)](https://docs.microsoft.com/azure/cloud-shell/overview) preview to work with HDInsight, then you must:</span></span>
>
> * <span data-ttu-id="907f3-116">Создать скрипты в среде Cloud Shell.</span><span class="sxs-lookup"><span data-stu-id="907f3-116">Create the scripts inside the cloud shell environment.</span></span>
> * <span data-ttu-id="907f3-117">Использовать `scp` для отправки файлов из Cloud Shell в HDInsight.</span><span class="sxs-lookup"><span data-stu-id="907f3-117">Use `scp` to upload the files from the cloud shell to HDInsight.</span></span>
> * <span data-ttu-id="907f3-118">Использовать `ssh` из Cloud Shell для подключения к HDInsight и выполнения примеров.</span><span class="sxs-lookup"><span data-stu-id="907f3-118">Use `ssh` from the cloud shell to connect to HDInsight and run the examples.</span></span>

## <span data-ttu-id="907f3-119"><a name="hivepython"></a>Определяемая пользователем функция Hive</span><span class="sxs-lookup"><span data-stu-id="907f3-119"><a name="hivepython"></a>Hive UDF</span></span>

<span data-ttu-id="907f3-120">Скрипт Python можно использовать в качестве определяемой пользователем функции из Hive через HiveQL с помощью инструкции `TRANSFORM`.</span><span class="sxs-lookup"><span data-stu-id="907f3-120">Python can be used as a UDF from Hive through the HiveQL `TRANSFORM` statement.</span></span> <span data-ttu-id="907f3-121">Например, следующий запрос HiveQL вызывает файл `hiveudf.py`, хранящийся в учетной записи хранения Azure по умолчанию для кластера.</span><span class="sxs-lookup"><span data-stu-id="907f3-121">For example, the following HiveQL invokes the `hiveudf.py` file stored in the default Azure Storage account for the cluster.</span></span>

<span data-ttu-id="907f3-122">**HDInsight под управлением Linux**</span><span class="sxs-lookup"><span data-stu-id="907f3-122">**Linux-based HDInsight**</span></span>

```hiveql
add file wasb:///hiveudf.py;

SELECT TRANSFORM (clientid, devicemake, devicemodel)
    USING 'python hiveudf.py' AS
    (clientid string, phoneLable string, phoneHash string)
FROM hivesampletable
ORDER BY clientid LIMIT 50;
```

<span data-ttu-id="907f3-123">**HDInsight под управлением Windows**</span><span class="sxs-lookup"><span data-stu-id="907f3-123">**Windows-based HDInsight**</span></span>

```hiveql
add file wasb:///hiveudf.py;

SELECT TRANSFORM (clientid, devicemake, devicemodel)
    USING 'D:\Python27\python.exe hiveudf.py' AS
    (clientid string, phoneLable string, phoneHash string)
FROM hivesampletable
ORDER BY clientid LIMIT 50;
```

> [!NOTE]
> <span data-ttu-id="907f3-124">В кластерах HDInsight под управлением Windows оператор `USING` должен задавать полный путь к python.exe.</span><span class="sxs-lookup"><span data-stu-id="907f3-124">On Windows-based HDInsight clusters, the `USING` clause must specify the full path to python.exe.</span></span>

<span data-ttu-id="907f3-125">Вот что делает данный пример:</span><span class="sxs-lookup"><span data-stu-id="907f3-125">Here's what this example does:</span></span>

1. <span data-ttu-id="907f3-126">Инструкция `add file` в начале файла добавляет файл `hiveudf.py` в распределенный кэш, и он становится доступен всем узлам кластера.</span><span class="sxs-lookup"><span data-stu-id="907f3-126">The `add file` statement at the beginning of the file adds the `hiveudf.py` file to the distributed cache, so it's accessible by all nodes in the cluster.</span></span>
2. <span data-ttu-id="907f3-127">Инструкция `SELECT TRANSFORM ... USING` выбирает данные из `hivesampletable`.</span><span class="sxs-lookup"><span data-stu-id="907f3-127">The `SELECT TRANSFORM ... USING` statement selects data from the `hivesampletable`.</span></span> <span data-ttu-id="907f3-128">Она также передает параметры clientid, devicemake и devicemodel в скрипт `hiveudf.py`.</span><span class="sxs-lookup"><span data-stu-id="907f3-128">It also passes the clientid, devicemake, and devicemodel values to the `hiveudf.py` script.</span></span>
3. <span data-ttu-id="907f3-129">Предложение `AS` описывает поля, возвращаемые из `hiveudf.py`.</span><span class="sxs-lookup"><span data-stu-id="907f3-129">The `AS` clause describes the fields returned from `hiveudf.py`.</span></span>

<a name="streamingpy"></a>

### <a name="create-the-hiveudfpy-file"></a><span data-ttu-id="907f3-130">Создание файла hiveudf.py</span><span class="sxs-lookup"><span data-stu-id="907f3-130">Create the hiveudf.py file</span></span>


<span data-ttu-id="907f3-131">В среде разработки создайте текстовый файл с именем `hiveudf.py`.</span><span class="sxs-lookup"><span data-stu-id="907f3-131">On your development environment, create a text file named `hiveudf.py`.</span></span> <span data-ttu-id="907f3-132">Используйте следующий код в качестве содержимого файла:</span><span class="sxs-lookup"><span data-stu-id="907f3-132">Use the following code as the contents of the file:</span></span>

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

<span data-ttu-id="907f3-133">Сценарий выполняет следующие действия:</span><span class="sxs-lookup"><span data-stu-id="907f3-133">This script performs the following actions:</span></span>

1. <span data-ttu-id="907f3-134">Чтение данных из STDIN.</span><span class="sxs-lookup"><span data-stu-id="907f3-134">Read a line of data from STDIN.</span></span>
2. <span data-ttu-id="907f3-135">Стоящий в конце знак новой строки удаляется с помощью `string.strip(line, "\n ")`.</span><span class="sxs-lookup"><span data-stu-id="907f3-135">The trailing newline character is removed using `string.strip(line, "\n ")`.</span></span>
3. <span data-ttu-id="907f3-136">При обработке потока в одной строке будут содержаться все значения, разделенные символом табуляции.</span><span class="sxs-lookup"><span data-stu-id="907f3-136">When doing stream processing, a single line contains all the values with a tab character between each value.</span></span> <span data-ttu-id="907f3-137">Поэтому можно использовать `string.split(line, "\t")` для разделения входящих данных при каждой табуляции, возвращая лишь поля.</span><span class="sxs-lookup"><span data-stu-id="907f3-137">So `string.split(line, "\t")` can be used to split the input at each tab, returning just the fields.</span></span>
4. <span data-ttu-id="907f3-138">По завершении обработки результат должен быть записан в поток STDOUT в виде одной строки, с разделенными символами табуляции полями.</span><span class="sxs-lookup"><span data-stu-id="907f3-138">When processing is complete, the output must be written to STDOUT as a single line, with a tab between each field.</span></span> <span data-ttu-id="907f3-139">Пример: `print "\t".join([clientid, phone_label, hashlib.md5(phone_label).hexdigest()])`.</span><span class="sxs-lookup"><span data-stu-id="907f3-139">For example, `print "\t".join([clientid, phone_label, hashlib.md5(phone_label).hexdigest()])`.</span></span>
5. <span data-ttu-id="907f3-140">Цикл `while` повторяется до тех пор, пока считывается `line`.</span><span class="sxs-lookup"><span data-stu-id="907f3-140">The `while` loop repeats until no `line` is read.</span></span>

<span data-ttu-id="907f3-141">Выходные данные скрипта представляют собой объединенные входные значения для `devicemake` и `devicemodel`, а также хэш для объединенного значения.</span><span class="sxs-lookup"><span data-stu-id="907f3-141">The script output is a concatenation of the input values for `devicemake` and `devicemodel`, and a hash of the concatenated value.</span></span>

<span data-ttu-id="907f3-142">Сведения о выполнении этого примера в кластере HDInsight см. в разделе [Выполнение примеров](#running).</span><span class="sxs-lookup"><span data-stu-id="907f3-142">See [Running the examples](#running) for how to run this example on your HDInsight cluster.</span></span>

## <span data-ttu-id="907f3-143"><a name="pigpython"></a>Определяемая пользователем функция Pig</span><span class="sxs-lookup"><span data-stu-id="907f3-143"><a name="pigpython"></a>Pig UDF</span></span>

<span data-ttu-id="907f3-144">Скрипт Python можно использовать в виде определяемой пользователем функции из Pig с использованием инструкции `GENERATE`.</span><span class="sxs-lookup"><span data-stu-id="907f3-144">A Python script can be used as a UDF from Pig through the `GENERATE` statement.</span></span> <span data-ttu-id="907f3-145">Вы можете запустить скрипт с помощью Jython или CPython.</span><span class="sxs-lookup"><span data-stu-id="907f3-145">You can run the script using either Jython or C Python.</span></span>

* <span data-ttu-id="907f3-146">Jython работает на виртуальной машине Java и изначально может вызываться из Pig.</span><span class="sxs-lookup"><span data-stu-id="907f3-146">Jython runs on the JVM, and can natively be called from Pig.</span></span>
* <span data-ttu-id="907f3-147">CPython является внешним процессом, поэтому данные из Pig на JVM отправляются в скрипт, выполняющийся в процессе Python.</span><span class="sxs-lookup"><span data-stu-id="907f3-147">C Python is an external process, so the data from Pig on the JVM is sent out to the script running in a Python process.</span></span> <span data-ttu-id="907f3-148">Выходные данные скрипта Python отправляются обратно в Pig.</span><span class="sxs-lookup"><span data-stu-id="907f3-148">The output of the Python script is sent back into Pig.</span></span>

<span data-ttu-id="907f3-149">Чтобы указать интерпретатор Python, используйте `register` при указании ссылки на скрипт Python.</span><span class="sxs-lookup"><span data-stu-id="907f3-149">To specify the Python interpreter, use `register` when referencing the Python script.</span></span> <span data-ttu-id="907f3-150">Следующие примеры регистрируют скрипты с Pig в качестве `myfuncs`:</span><span class="sxs-lookup"><span data-stu-id="907f3-150">The following examples register scripts with Pig as `myfuncs`:</span></span>

* <span data-ttu-id="907f3-151">**Для использования Jython:** `register '/path/to/pigudf.py' using jython as myfuncs;`</span><span class="sxs-lookup"><span data-stu-id="907f3-151">**To use Jython**: `register '/path/to/pigudf.py' using jython as myfuncs;`</span></span>
* <span data-ttu-id="907f3-152">**Для использования CPython:** `register '/path/to/pigudf.py' using streaming_python as myfuncs;`</span><span class="sxs-lookup"><span data-stu-id="907f3-152">**To use C Python**: `register '/path/to/pigudf.py' using streaming_python as myfuncs;`</span></span>

> [!IMPORTANT]
> <span data-ttu-id="907f3-153">При использовании Jython путь к файлу pig_jython может быть локальным путем или путем WASB://.</span><span class="sxs-lookup"><span data-stu-id="907f3-153">When using Jython, the path to the pig_jython file can be either a local path or a WASB:// path.</span></span> <span data-ttu-id="907f3-154">Но при использовании CPython необходимо указать ссылку на файл в локальной файловой системе узла, который используется для отправки задания Pig.</span><span class="sxs-lookup"><span data-stu-id="907f3-154">However, when using C Python, you must reference a file on the local file system of the node that you are using to submit the Pig job.</span></span>

<span data-ttu-id="907f3-155">После регистрации язык Pig Latin будет одинаковым для обоих примеров:</span><span class="sxs-lookup"><span data-stu-id="907f3-155">Once past registration, the Pig Latin for this example is the same for both:</span></span>

```pig
LOGS = LOAD 'wasb:///example/data/sample.log' as (LINE:chararray);
LOG = FILTER LOGS by LINE is not null;
DETAILS = FOREACH LOG GENERATE myfuncs.create_structure(LINE);
DUMP DETAILS;
```

<span data-ttu-id="907f3-156">Вот что делает данный пример:</span><span class="sxs-lookup"><span data-stu-id="907f3-156">Here's what this example does:</span></span>

1. <span data-ttu-id="907f3-157">Первая строка загружает образец файла данных `sample.log` в `LOGS`.</span><span class="sxs-lookup"><span data-stu-id="907f3-157">The first line loads the sample data file, `sample.log` into `LOGS`.</span></span> <span data-ttu-id="907f3-158">Она также определяет каждую запись как массив символов `chararray`.</span><span class="sxs-lookup"><span data-stu-id="907f3-158">It also defines each record as a `chararray`.</span></span>
2. <span data-ttu-id="907f3-159">Следующая строка отфильтровывает все пустые значения, сохраняя результат работы в `LOG`.</span><span class="sxs-lookup"><span data-stu-id="907f3-159">The next line filters out any null values, storing the result of the operation into `LOG`.</span></span>
3. <span data-ttu-id="907f3-160">Затем выполняется итерация по записям в `LOG` и используется инструкция `GENERATE` для вызова метода `create_structure`, содержащегося в скрипте Python или Jython, загруженном как `myfuncs`.</span><span class="sxs-lookup"><span data-stu-id="907f3-160">Next, it iterates over the records in `LOG` and uses `GENERATE` to invoke the `create_structure` method contained in the Python/Jython script loaded as `myfuncs`.</span></span> <span data-ttu-id="907f3-161">`LINE` используется для передачи текущей записи в функцию.</span><span class="sxs-lookup"><span data-stu-id="907f3-161">`LINE` is used to pass the current record to the function.</span></span>
4. <span data-ttu-id="907f3-162">Наконец, выходные данные сбрасываются в поток STDOUT командой `DUMP`.</span><span class="sxs-lookup"><span data-stu-id="907f3-162">Finally, the outputs are dumped to STDOUT using the `DUMP` command.</span></span> <span data-ttu-id="907f3-163">После завершения операции эта команда выведет результат.</span><span class="sxs-lookup"><span data-stu-id="907f3-163">This command displays the results after the operation completes.</span></span>

### <a name="create-the-pigudfpy-file"></a><span data-ttu-id="907f3-164">Создание файла pigudf.py</span><span class="sxs-lookup"><span data-stu-id="907f3-164">Create the pigudf.py file</span></span>

<span data-ttu-id="907f3-165">В среде разработки создайте текстовый файл с именем `pigudf.py`.</span><span class="sxs-lookup"><span data-stu-id="907f3-165">On your development environment, create a text file named `pigudf.py`.</span></span> <span data-ttu-id="907f3-166">Используйте следующий код в качестве содержимого файла:</span><span class="sxs-lookup"><span data-stu-id="907f3-166">Use the following code as the contents of the file:</span></span>

<a name="streamingpy"></a>

```python
# Uncomment the following if using C Python
#from pig_util import outputSchema

@outputSchema("log: {(date:chararray, time:chararray, classname:chararray, level:chararray, detail:chararray)}")
def create_structure(input):
    if (input.startswith('java.lang.Exception')):
        input = input[21:len(input)] + ' - java.lang.Exception'
    date, time, classname, level, detail = input.split(' ', 4)
    return date, time, classname, level, detail
```

<span data-ttu-id="907f3-167">В примере Pig Latin мы определили вход `LINE` в виде массива строк, потому что для ввода нет согласованной схемы.</span><span class="sxs-lookup"><span data-stu-id="907f3-167">In the Pig Latin example, we defined the `LINE` input as a chararray because there is no consistent schema for the input.</span></span> <span data-ttu-id="907f3-168">Скрипт Python выполняет преобразование данных в согласованную схему на выходе.</span><span class="sxs-lookup"><span data-stu-id="907f3-168">The Python script transforms the data into a consistent schema for output.</span></span>

1. <span data-ttu-id="907f3-169">Инструкция `@outputSchema` задает формат данных, в котором они возвращаются в Pig.</span><span class="sxs-lookup"><span data-stu-id="907f3-169">The `@outputSchema` statement defines the format of the data that is returned to Pig.</span></span> <span data-ttu-id="907f3-170">В данном случае это **data bag**, являющийся типом данных Pig.</span><span class="sxs-lookup"><span data-stu-id="907f3-170">In this case, it's a **data bag**, which is a Pig data type.</span></span> <span data-ttu-id="907f3-171">Корзина содержит следующие поля, все они имеют тип "Массив строк" (строки):</span><span class="sxs-lookup"><span data-stu-id="907f3-171">The bag contains the following fields, all of which are chararray (strings):</span></span>

   * <span data-ttu-id="907f3-172">date — дата создания записи журнала;</span><span class="sxs-lookup"><span data-stu-id="907f3-172">date - the date the log entry was created</span></span>
   * <span data-ttu-id="907f3-173">date — время создания записи журнала;</span><span class="sxs-lookup"><span data-stu-id="907f3-173">time - the time the log entry was created</span></span>
   * <span data-ttu-id="907f3-174">classname — имя класса, для которого создана запись;</span><span class="sxs-lookup"><span data-stu-id="907f3-174">classname - the class name the entry was created for</span></span>
   * <span data-ttu-id="907f3-175">level — уровень журналирования;</span><span class="sxs-lookup"><span data-stu-id="907f3-175">level - the log level</span></span>
   * <span data-ttu-id="907f3-176">detail — подробная информация о записи журнала.</span><span class="sxs-lookup"><span data-stu-id="907f3-176">detail - verbose details for the log entry</span></span>

2. <span data-ttu-id="907f3-177">Затем `def create_structure(input)` определяет функцию, в которую Pig отправляет строковые элементы.</span><span class="sxs-lookup"><span data-stu-id="907f3-177">Next, the `def create_structure(input)` defines the function that Pig passes line items to.</span></span>

3. <span data-ttu-id="907f3-178">Данные для примера, `sample.log`, в основном соответствуют схеме даты, времени, имени класса, уровня и подробной информации, которую мы хотим возвращать.</span><span class="sxs-lookup"><span data-stu-id="907f3-178">The example data, `sample.log`, mostly conforms to the date, time, classname, level, and detail schema we want to return.</span></span> <span data-ttu-id="907f3-179">Однако он содержит несколько строк, начинающихся с `*java.lang.Exception*`.</span><span class="sxs-lookup"><span data-stu-id="907f3-179">However, it contains a few lines that begin with `*java.lang.Exception*`.</span></span> <span data-ttu-id="907f3-180">Эти строки должны быть изменены в соответствии со схемой.</span><span class="sxs-lookup"><span data-stu-id="907f3-180">These lines must be modified to match the schema.</span></span> <span data-ttu-id="907f3-181">Инструкция `if` проверяет на наличие таких строк, затем манипулирует входными данными, переставляя строку `*java.lang.Exception*` в конец, формируя данные в соответствии с ожидаемой схемой.</span><span class="sxs-lookup"><span data-stu-id="907f3-181">The `if` statement checks for those, then massages the input data to move the `*java.lang.Exception*` string to the end, bringing the data in-line with our expected output schema.</span></span>

4. <span data-ttu-id="907f3-182">Затем команда `split` используется для разделения данных по первым четырем символам пробела.</span><span class="sxs-lookup"><span data-stu-id="907f3-182">Next, the `split` command is used to split the data at the first four space characters.</span></span> <span data-ttu-id="907f3-183">Выходным данным присваиваются значения `date`, `time`, `classname`, `level` и `detail`.</span><span class="sxs-lookup"><span data-stu-id="907f3-183">The output is assigned into `date`, `time`, `classname`, `level`, and `detail`.</span></span>

5. <span data-ttu-id="907f3-184">И результаты возвращаются в Pig.</span><span class="sxs-lookup"><span data-stu-id="907f3-184">Finally, the values are returned to Pig.</span></span>

<span data-ttu-id="907f3-185">Когда данные возвращаются в Pig, они имеют согласованную схему, определенную инструкцией `@outputSchema`.</span><span class="sxs-lookup"><span data-stu-id="907f3-185">When the data is returned to Pig, it has a consistent schema as defined in the `@outputSchema` statement.</span></span>

## <span data-ttu-id="907f3-186"><a name="running"></a>Отправка и выполнение примеров</span><span class="sxs-lookup"><span data-stu-id="907f3-186"><a name="running"></a>Upload and run the examples</span></span>

> [!IMPORTANT]
> <span data-ttu-id="907f3-187">Действия с **SSH** работают только с кластером HDInsight на базе Linux.</span><span class="sxs-lookup"><span data-stu-id="907f3-187">The **SSH** steps only work with a Linux-based HDInsight cluster.</span></span> <span data-ttu-id="907f3-188">Действия с **PowerShell** работают с кластером HDInsight на базе Linux и Windows, но требуют клиента Windows.</span><span class="sxs-lookup"><span data-stu-id="907f3-188">The **PowerShell** steps work with either a Linux or Windows-based HDInsight cluster, but require a Windows client.</span></span>

### <a name="ssh"></a><span data-ttu-id="907f3-189">SSH</span><span class="sxs-lookup"><span data-stu-id="907f3-189">SSH</span></span>

<span data-ttu-id="907f3-190">Дополнительные сведения об использовании SSH см. в разделе [Подключение к HDInsight (Hadoop) с помощью SSH](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="907f3-190">For more information on using SSH, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

1. <span data-ttu-id="907f3-191">Используйте `scp` для копирования файлов в кластер HDInsight.</span><span class="sxs-lookup"><span data-stu-id="907f3-191">Use `scp` to copy the files to your HDInsight cluster.</span></span> <span data-ttu-id="907f3-192">Например, следующая команда позволяет скопировать файлы в кластер с именем **mycluster**.</span><span class="sxs-lookup"><span data-stu-id="907f3-192">For example, the following command copies the files to a cluster named **mycluster**.</span></span>

    ```bash
    scp hiveudf.py pigudf.py myuser@mycluster-ssh.azurehdinsight.net:
    ```

2. <span data-ttu-id="907f3-193">Используйте SSH, чтобы подключиться к кластеру.</span><span class="sxs-lookup"><span data-stu-id="907f3-193">Use SSH to connect to the cluster.</span></span>

    ```bash
    ssh myuser@mycluster-ssh.azurehdinsight.net
    ```

3. <span data-ttu-id="907f3-194">В сеансе SSH добавьте переданные ранее файлы Python в хранилище WASB для кластера.</span><span class="sxs-lookup"><span data-stu-id="907f3-194">From the SSH session, add the python files uploaded previously to the WASB storage for the cluster.</span></span>

    ```bash
    hdfs dfs -put hiveudf.py /hiveudf.py
    hdfs dfs -put pigudf.py /pigudf.py
    ```

<span data-ttu-id="907f3-195">После передачи файлов выполните следующие действия для выполнения заданий Hive и Pig.</span><span class="sxs-lookup"><span data-stu-id="907f3-195">After uploading the files, use the following steps to run the Hive and Pig jobs.</span></span>

#### <a name="use-the-hive-udf"></a><span data-ttu-id="907f3-196">Использование определяемой пользователем функции Hive</span><span class="sxs-lookup"><span data-stu-id="907f3-196">Use the Hive UDF</span></span>

1. <span data-ttu-id="907f3-197">Используйте команду `hive` , чтобы запустить оболочку Hive.</span><span class="sxs-lookup"><span data-stu-id="907f3-197">Use the `hive` command to start the hive shell.</span></span> <span data-ttu-id="907f3-198">После загрузки оболочки вы увидите запрос `hive>` .</span><span class="sxs-lookup"><span data-stu-id="907f3-198">You should see a `hive>` prompt once the shell has loaded.</span></span>

2. <span data-ttu-id="907f3-199">Введите следующий запрос `hive>` в командной строке:</span><span class="sxs-lookup"><span data-stu-id="907f3-199">Enter the following query at the `hive>` prompt:</span></span>

   ```hive
   add file wasb:///hiveudf.py;
   SELECT TRANSFORM (clientid, devicemake, devicemodel)
       USING 'python hiveudf.py' AS
       (clientid string, phoneLabel string, phoneHash string)
   FROM hivesampletable
   ORDER BY clientid LIMIT 50;
   ```

3. <span data-ttu-id="907f3-200">После ввода последней строки запустится задание.</span><span class="sxs-lookup"><span data-stu-id="907f3-200">After entering the last line, the job should start.</span></span> <span data-ttu-id="907f3-201">По завершении задания эта команда возвращает выходные данные следующего вида:</span><span class="sxs-lookup"><span data-stu-id="907f3-201">Once the job completes, it returns output similar to the following example:</span></span>

        100041    RIM 9650    d476f3687700442549a83fac4560c51c
        100041    RIM 9650    d476f3687700442549a83fac4560c51c
        100042    Apple iPhone 4.2.x    375ad9a0ddc4351536804f1d5d0ea9b9
        100042    Apple iPhone 4.2.x    375ad9a0ddc4351536804f1d5d0ea9b9
        100042    Apple iPhone 4.2.x    375ad9a0ddc4351536804f1d5d0ea9b9

#### <a name="use-the-pig-udf"></a><span data-ttu-id="907f3-202">Использование определяемой пользователем функции Pig</span><span class="sxs-lookup"><span data-stu-id="907f3-202">Use the Pig UDF</span></span>

1. <span data-ttu-id="907f3-203">Используйте команду `pig` , чтобы запустить оболочку.</span><span class="sxs-lookup"><span data-stu-id="907f3-203">Use the `pig` command to start the shell.</span></span> <span data-ttu-id="907f3-204">После загрузки оболочки вы увидите запрос `grunt>`.</span><span class="sxs-lookup"><span data-stu-id="907f3-204">You see a `grunt>` prompt once the shell has loaded.</span></span>

2. <span data-ttu-id="907f3-205">В окне запроса `grunt>` введите следующие операторы:</span><span class="sxs-lookup"><span data-stu-id="907f3-205">Enter the following statements at the `grunt>` prompt:</span></span>

   ```pig
   Register wasb:///pigudf.py using jython as myfuncs;
   LOGS = LOAD 'wasb:///example/data/sample.log' as (LINE:chararray);
   LOG = FILTER LOGS by LINE is not null;
   DETAILS = foreach LOG generate myfuncs.create_structure(LINE);
   DUMP DETAILS;
   ```

3. <span data-ttu-id="907f3-206">После ввода указанной строки должно запуститься задание.</span><span class="sxs-lookup"><span data-stu-id="907f3-206">After entering the following line, the job should start.</span></span> <span data-ttu-id="907f3-207">По завершении задания эта команда возвращает выходные данные следующего вида:</span><span class="sxs-lookup"><span data-stu-id="907f3-207">Once the job completes, it returns output similar to the following data:</span></span>

        ((2012-02-03,20:11:56,SampleClass5,[TRACE],verbose detail for id 990982084))
        ((2012-02-03,20:11:56,SampleClass7,[TRACE],verbose detail for id 1560323914))
        ((2012-02-03,20:11:56,SampleClass8,[DEBUG],detail for id 2083681507))
        ((2012-02-03,20:11:56,SampleClass3,[TRACE],verbose detail for id 1718828806))
        ((2012-02-03,20:11:56,SampleClass3,[INFO],everything normal for id 530537821))

4. <span data-ttu-id="907f3-208">Используйте `quit` для выхода из оболочки Grunt, а затем следующую команду для изменения файла pigudf.py в локальной файловой системе:</span><span class="sxs-lookup"><span data-stu-id="907f3-208">Use `quit` to exit the Grunt shell, and then use the following to edit the pigudf.py file on the local file system:</span></span>

    ```bash
    nano pigudf.py
    ```

5. <span data-ttu-id="907f3-209">Войдите в редактор и раскомментируйте следующую строку, удалив символ `#` в начале строки.</span><span class="sxs-lookup"><span data-stu-id="907f3-209">Once in the editor, uncomment the following line by removing the `#` character from the beginning of the line:</span></span>

    ```bash
    #from pig_util import outputSchema
    ```

    <span data-ttu-id="907f3-210">Закончив вносить изменения, нажмите сочетание клавиш CTRL+X, чтобы выйти из редактора.</span><span class="sxs-lookup"><span data-stu-id="907f3-210">Once the change has been made, use Ctrl+X to exit the editor.</span></span> <span data-ttu-id="907f3-211">Выберите Y и нажмите ВВОД, чтобы сохранить изменения.</span><span class="sxs-lookup"><span data-stu-id="907f3-211">Select Y, and then enter to save the changes.</span></span>

6. <span data-ttu-id="907f3-212">Используйте команду `pig` , чтобы снова запустить оболочку.</span><span class="sxs-lookup"><span data-stu-id="907f3-212">Use the `pig` command to start the shell again.</span></span> <span data-ttu-id="907f3-213">При появлении запроса `grunt>` введите следующие инструкции, чтобы запустить сценарий Python с помощью интерпретатора CPython.</span><span class="sxs-lookup"><span data-stu-id="907f3-213">Once you are at the `grunt>` prompt, use the following to run the Python script using the C Python interpreter.</span></span>

   ```pig
   Register 'pigudf.py' using streaming_python as myfuncs;
   LOGS = LOAD 'wasb:///example/data/sample.log' as (LINE:chararray);
   LOG = FILTER LOGS by LINE is not null;
   DETAILS = foreach LOG generate myfuncs.create_structure(LINE);
   DUMP DETAILS;
   ```

    <span data-ttu-id="907f3-214">Когда это задание будет выполнено, вы увидите такой же результат, как при запуске сценария с помощью Jython.</span><span class="sxs-lookup"><span data-stu-id="907f3-214">Once this job completes, you should see the same output as when you previously ran the script using Jython.</span></span>

### <a name="powershell-upload-the-files"></a><span data-ttu-id="907f3-215">PowerShell: отправка файлов</span><span class="sxs-lookup"><span data-stu-id="907f3-215">PowerShell: Upload the files</span></span>

<span data-ttu-id="907f3-216">Вы можете использовать PowerShell для отправки файлов на сервер HDInsight.</span><span class="sxs-lookup"><span data-stu-id="907f3-216">You can use PowerShell to upload the files to the HDInsight server.</span></span> <span data-ttu-id="907f3-217">Используйте следующий скрипт для отправки файлов Python:</span><span class="sxs-lookup"><span data-stu-id="907f3-217">Use the following script to upload the Python files:</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="907f3-218">В этом разделе используется Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="907f3-218">The steps in this section use Azure PowerShell.</span></span> <span data-ttu-id="907f3-219">Дополнительные сведения об использовании Azure PowerShell см. в статье [How to install and configure Azure PowerShell](/powershell/azure/overview) (Как установить и настроить Azure PowerShell).</span><span class="sxs-lookup"><span data-stu-id="907f3-219">For more information on using Azure PowerShell, see [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span>

```powershell
# Login to your Azure subscription
# Is there an active Azure subscription?
$sub = Get-AzureRmSubscription -ErrorAction SilentlyContinue
if(-not($sub))
{
    Add-AzureRmAccount
}

# Get cluster info
$clusterName = Read-Host -Prompt "Enter the HDInsight cluster name"
# Change the path to match the file location on your system
$pathToStreamingFile = "C:\path\to\hiveudf.py"
$pathToJythonFile = "C:\path\to\pigudf.py"

$clusterInfo = Get-AzureRmHDInsightCluster -ClusterName $clusterName
$resourceGroup = $clusterInfo.ResourceGroup
$storageAccountName=$clusterInfo.DefaultStorageAccount.split('.')[0]
$container=$clusterInfo.DefaultStorageContainer
$storageAccountKey=(Get-AzureRmStorageAccountKey `
    -Name $storageAccountName `
-ResourceGroupName $resourceGroup)[0].Value

#Create a storage content and upload the file
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
> <span data-ttu-id="907f3-220">Измените значение `C:\path\to` на путь к файлам в среде разработки.</span><span class="sxs-lookup"><span data-stu-id="907f3-220">Change the `C:\path\to` value to the path to the files on your development environment.</span></span>

<span data-ttu-id="907f3-221">Этот скрипт получает информацию для кластера HDInsight, извлекает учетную запись и ключ для учетной записи хранения по умолчанию и загружает файлы в корневую папку контейнера.</span><span class="sxs-lookup"><span data-stu-id="907f3-221">This script retrieves information for your HDInsight cluster, then extracts the account and key for the default storage account, and uploads the files to the root of the container.</span></span>

> [!NOTE]
> <span data-ttu-id="907f3-222">Дополнительные сведения о загрузке файлов см. в статье [Отправка данных для заданий Hadoop в HDInsight](hdinsight-upload-data.md).</span><span class="sxs-lookup"><span data-stu-id="907f3-222">For more information on uploading files, see the [Upload data for Hadoop jobs in HDInsight](hdinsight-upload-data.md) document.</span></span>

#### <a name="powershell-use-the-hive-udf"></a><span data-ttu-id="907f3-223">PowerShell: использование определяемой пользователем функции Hive</span><span class="sxs-lookup"><span data-stu-id="907f3-223">PowerShell: Use the Hive UDF</span></span>

<span data-ttu-id="907f3-224">PowerShell также можно использовать для удаленного запуска запросов на использование Hive.</span><span class="sxs-lookup"><span data-stu-id="907f3-224">PowerShell can also be used to remotely run Hive queries.</span></span> <span data-ttu-id="907f3-225">Используйте следующий сценарий PowerShell для запуска запроса Hive, который использует скрипт **hiveudf.py**:</span><span class="sxs-lookup"><span data-stu-id="907f3-225">Use the following PowerShell script to run a Hive query that uses **hiveudf.py** script:</span></span>

> [!IMPORTANT]
> <span data-ttu-id="907f3-226">Перед запуском он предлагает вам ввести сведения об HTTPS и учетной записи администратора для кластера HDInsight.</span><span class="sxs-lookup"><span data-stu-id="907f3-226">Before running, the script prompts you for the HTTPs/Admin account information for your HDInsight cluster.</span></span>

```powershell
# Login to your Azure subscription
# Is there an active Azure subscription?
$sub = Get-AzureRmSubscription -ErrorAction SilentlyContinue
if(-not($sub))
{
    Add-AzureRmAccount
}

# Get cluster info
$clusterName = Read-Host -Prompt "Enter the HDInsight cluster name"
$creds=Get-Credential -Message "Enter the login for the cluster"

# If using a Windows-based HDInsight cluster, change the USING statement to:
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
Write-Host "Wait for the Hive job to complete ..." -ForegroundColor Green
Wait-AzureRmHDInsightJob `
    -JobId $job.JobId `
    -ClusterName $clusterName `
    -HttpCredential $creds
# Uncomment the following to see stderr output
# Get-AzureRmHDInsightJobOutput `
#   -Clustername $clusterName `
#   -JobId $job.JobId `
#   -HttpCredential $creds `
#   -DisplayOutputType StandardError
Write-Host "Display the standard output ..." -ForegroundColor Green
Get-AzureRmHDInsightJobOutput `
    -Clustername $clusterName `
    -JobId $job.JobId `
    -HttpCredential $creds
```

<span data-ttu-id="907f3-227">Результат выполнения задания **Hive** должен выглядеть аналогично следующему примеру:</span><span class="sxs-lookup"><span data-stu-id="907f3-227">The output for the **Hive** job should appear similar to the following example:</span></span>

    100041    RIM 9650    d476f3687700442549a83fac4560c51c
    100041    RIM 9650    d476f3687700442549a83fac4560c51c
    100042    Apple iPhone 4.2.x    375ad9a0ddc4351536804f1d5d0ea9b9
    100042    Apple iPhone 4.2.x    375ad9a0ddc4351536804f1d5d0ea9b9
    100042    Apple iPhone 4.2.x    375ad9a0ddc4351536804f1d5d0ea9b9

#### <a name="pig-jython"></a><span data-ttu-id="907f3-228">Pig (Jython)</span><span class="sxs-lookup"><span data-stu-id="907f3-228">Pig (Jython)</span></span>

<span data-ttu-id="907f3-229">PowerShell также можно использовать для запуска заданий Pig Latin.</span><span class="sxs-lookup"><span data-stu-id="907f3-229">PowerShell can also be used to run Pig Latin jobs.</span></span> <span data-ttu-id="907f3-230">Для запуска задания Pig Latin, использующего скрипт **pigudf.py**, используйте следующий сценарий PowerShell:</span><span class="sxs-lookup"><span data-stu-id="907f3-230">To run a Pig Latin job that uses the **pigudf.py** script, use the following PowerShell script:</span></span>

> [!NOTE]
> <span data-ttu-id="907f3-231">При удаленной отправке задания с помощью PowerShell нельзя использовать CPython в качестве интерпретатора.</span><span class="sxs-lookup"><span data-stu-id="907f3-231">When remotely submitting a job using PowerShell, it is not possible to use C Python as the interpreter.</span></span>

```powershell
# Login to your Azure subscription
# Is there an active Azure subscription?
$sub = Get-AzureRmSubscription -ErrorAction SilentlyContinue
if(-not($sub))
{
    Add-AzureRmAccount
}

# Get cluster info
$clusterName = Read-Host -Prompt "Enter the HDInsight cluster name"
$creds=Get-Credential -Message "Enter the login for the cluster"

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

Write-Host "Wait for the Pig job to complete ..." -ForegroundColor Green
Wait-AzureRmHDInsightJob `
    -Job $job.JobId `
    -ClusterName $clusterName `
    -HttpCredential $creds
# Uncomment the following to see stderr output
# Get-AzureRmHDInsightJobOutput `
#    -Clustername $clusterName `
#    -JobId $job.JobId `
#    -HttpCredential $creds `
#    -DisplayOutputType StandardError
Write-Host "Display the standard output ..." -ForegroundColor Green
Get-AzureRmHDInsightJobOutput `
    -Clustername $clusterName `
    -JobId $job.JobId `
    -HttpCredential $creds
```

<span data-ttu-id="907f3-232">Результат выполнения задания **Pig** должен выглядеть аналогично следующим данным:</span><span class="sxs-lookup"><span data-stu-id="907f3-232">The output for the **Pig** job should appear similar to the following data:</span></span>

    ((2012-02-03,20:11:56,SampleClass5,[TRACE],verbose detail for id 990982084))
    ((2012-02-03,20:11:56,SampleClass7,[TRACE],verbose detail for id 1560323914))
    ((2012-02-03,20:11:56,SampleClass8,[DEBUG],detail for id 2083681507))
    ((2012-02-03,20:11:56,SampleClass3,[TRACE],verbose detail for id 1718828806))
    ((2012-02-03,20:11:56,SampleClass3,[INFO],everything normal for id 530537821))

## <span data-ttu-id="907f3-233"><a name="troubleshooting"></a>Устранение неполадок</span><span class="sxs-lookup"><span data-stu-id="907f3-233"><a name="troubleshooting"></a>Troubleshooting</span></span>

### <a name="errors-when-running-jobs"></a><span data-ttu-id="907f3-234">Ошибки при выполнении заданий</span><span class="sxs-lookup"><span data-stu-id="907f3-234">Errors when running jobs</span></span>

<span data-ttu-id="907f3-235">При выполнении задания hive может возникнуть ошибка, аналогичная приведенной ниже:</span><span class="sxs-lookup"><span data-stu-id="907f3-235">When running the hive job, you may encounter an error similar to the following text:</span></span>

    Caused by: org.apache.hadoop.hive.ql.metadata.HiveException: [Error 20001]: An error occurred while reading or writing to your custom script. It may have crashed with an error.

<span data-ttu-id="907f3-236">Эта проблема может быть вызвана символами окончания строк в файле Python.</span><span class="sxs-lookup"><span data-stu-id="907f3-236">This problem may be caused by the line endings in the Python file.</span></span> <span data-ttu-id="907f3-237">Многие редакторы Windows по умолчанию используют символы CRLF, но в приложениях Linux обычно ожидается использование символа LF.</span><span class="sxs-lookup"><span data-stu-id="907f3-237">Many Windows editors default to using CRLF as the line ending, but Linux applications usually expect LF.</span></span>

<span data-ttu-id="907f3-238">Вы можете использовать следующие команды PowerShell для удаления символов CR перед передачей файла в HDInsight:</span><span class="sxs-lookup"><span data-stu-id="907f3-238">You can use the following PowerShell statements to remove the CR characters before uploading the file to HDInsight:</span></span>

```powershell
$original_file ='c:\path\to\hiveudf.py'
$text = [IO.File]::ReadAllText($original_file) -replace "`r`n", "`n"
[IO.File]::WriteAllText($original_file, $text)
```

### <a name="powershell-scripts"></a><span data-ttu-id="907f3-239">Сценарии PowerShell</span><span class="sxs-lookup"><span data-stu-id="907f3-239">PowerShell scripts</span></span>

<span data-ttu-id="907f3-240">Оба примера скриптов PowerShell, используемых для запуска примеров, содержат закомментированную строку, которая отображает вывод ошибок для задания.</span><span class="sxs-lookup"><span data-stu-id="907f3-240">Both of the example PowerShell scripts used to run the examples contain a commented line that displays error output for the job.</span></span> <span data-ttu-id="907f3-241">Если вы не видите ожидаемых результатов задания, раскомментируйте следующую строку и просмотрите информацию об ошибках на предмет отображения проблемы.</span><span class="sxs-lookup"><span data-stu-id="907f3-241">If you are not seeing the expected output for the job, uncomment the following line and see if the error information indicates a problem.</span></span>

```powershell
# Get-AzureRmHDInsightJobOutput `
        -Clustername $clusterName `
        -JobId $job.JobId `
        -HttpCredential $creds `
        -DisplayOutputType StandardError
```

<span data-ttu-id="907f3-242">Сведения об ошибках (STDERR) и результат выполнения задания (STDOUT) также записываются в хранилище HDInsight.</span><span class="sxs-lookup"><span data-stu-id="907f3-242">The error information (STDERR) and the result of the job (STDOUT) are also logged to your HDInsight storage.</span></span>

| <span data-ttu-id="907f3-243">Для данного задания...</span><span class="sxs-lookup"><span data-stu-id="907f3-243">For this job...</span></span> | <span data-ttu-id="907f3-244">Смотрите эти файлы в контейнере</span><span class="sxs-lookup"><span data-stu-id="907f3-244">Look at these files in the blob container</span></span> |
| --- | --- |
| <span data-ttu-id="907f3-245">Hive</span><span class="sxs-lookup"><span data-stu-id="907f3-245">Hive</span></span> |<span data-ttu-id="907f3-246">/HivePython/stderr</span><span class="sxs-lookup"><span data-stu-id="907f3-246">/HivePython/stderr</span></span><p><span data-ttu-id="907f3-247">/HivePython/stdout</span><span class="sxs-lookup"><span data-stu-id="907f3-247">/HivePython/stdout</span></span> |
| <span data-ttu-id="907f3-248">Pig,</span><span class="sxs-lookup"><span data-stu-id="907f3-248">Pig</span></span> |<span data-ttu-id="907f3-249">/PigPython/stderr</span><span class="sxs-lookup"><span data-stu-id="907f3-249">/PigPython/stderr</span></span><p><span data-ttu-id="907f3-250">/PigPython/stdout</span><span class="sxs-lookup"><span data-stu-id="907f3-250">/PigPython/stdout</span></span> |

## <span data-ttu-id="907f3-251"><a name="next"></a>Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="907f3-251"><a name="next"></a>Next steps</span></span>

<span data-ttu-id="907f3-252">Если вам нужно загрузить модули Python, которые не поставляются по умолчанию, см. статью [How to deploy a Python module to Windows Azure HDInsight](http://blogs.msdn.com/b/benjguin/archive/2014/03/03/how-to-deploy-a-python-module-to-windows-azure-hdinsight.aspx) (Как развернуть модуль Python в Windows Azure HDInsight).</span><span class="sxs-lookup"><span data-stu-id="907f3-252">If you need to load Python modules that aren't provided by default, see [How to deploy a module to Azure HDInsight](http://blogs.msdn.com/b/benjguin/archive/2014/03/03/how-to-deploy-a-python-module-to-windows-azure-hdinsight.aspx).</span></span>

<span data-ttu-id="907f3-253">Сведения о других способах использования Pig и Hive и дополнительную информацию об использовании MapReduce см. в следующих документах:</span><span class="sxs-lookup"><span data-stu-id="907f3-253">For other ways to use Pig, Hive, and to learn about using MapReduce, see the following documents:</span></span>

* [<span data-ttu-id="907f3-254">Использование Hive с HDInsight</span><span class="sxs-lookup"><span data-stu-id="907f3-254">Use Hive with HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="907f3-255">Использование Pig с HDInsight</span><span class="sxs-lookup"><span data-stu-id="907f3-255">Use Pig with HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="907f3-256">Использование MapReduce с HDInsight</span><span class="sxs-lookup"><span data-stu-id="907f3-256">Use MapReduce with HDInsight</span></span>](hdinsight-use-mapreduce.md)
