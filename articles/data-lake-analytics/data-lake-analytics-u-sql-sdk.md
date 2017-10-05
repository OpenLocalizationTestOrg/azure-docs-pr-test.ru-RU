---
title: "Масштабирование локального выполнения и тестирования сценариев U-SQL с помощью пакета SDK U-SQL для Azure Data Lake | Документация Майкрософт"
description: "Узнайте, как использовать пакет SDK Azure Data Lake для U-SQL для масштабирования локального выполнения и тестирования заданий U-SQL с помощью командной строки и программных интерфейсов на локальной рабочей станции."
services: data-lake-analytics
documentationcenter: 
author: 
manager: 
editor: 
ms.assetid: 
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 03/01/2017
ms.author: yanacai
ms.openlocfilehash: 55242bcf644ca0e7f30cfe7eada2130451c36e64
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="scale-u-sql-local-run-and-test-with-azure-data-lake-u-sql-sdk"></a><span data-ttu-id="11840-103">Масштабирование локального выполнения и тестирования сценариев U-SQL с помощью пакета SDK U-SQL для Azure Data Lake</span><span class="sxs-lookup"><span data-stu-id="11840-103">Scale U-SQL local run and test with Azure Data Lake U-SQL SDK</span></span>

<span data-ttu-id="11840-104">При разработке сценария U-SQL, прежде чем он отправляется в облако, как правило, сценарий запускается и тестируется в локальной среде.</span><span class="sxs-lookup"><span data-stu-id="11840-104">When developing U-SQL script, it is common to run and test U-SQL script locally before submit it to cloud.</span></span> <span data-ttu-id="11840-105">Для этого сценария Azure Data Lake предоставляет пакет Nuget, который называется пакетом SDK Azure Data Lake для U-SQL, с помощью которого можно легко масштабировать локальное выполнение и тестирование заданий U-SQL.</span><span class="sxs-lookup"><span data-stu-id="11840-105">Azure Data Lake provides a Nuget package called Azure Data Lake U-SQL SDK for this scenario, through which you can easily scale U-SQL local run and test.</span></span> <span data-ttu-id="11840-106">Можно также интегрировать этот тест U-SQL с системой CI (непрерывная интеграция), чтобы автоматизировать компиляцию и тестирование.</span><span class="sxs-lookup"><span data-stu-id="11840-106">It is also possible to integrate this U-SQL test with CI (Continuous Integration) system to automate the compile and test.</span></span>

<span data-ttu-id="11840-107">Если вас интересует, как вручную выполнить локальный запуск и отладку сценария U-SQL с помощью инструментов с графическим интерфейсом пользователя, то для этого можно использовать средства Azure Data Lake для Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="11840-107">If you care about how to manually local run and debug U-SQL script with GUI tooling, then you can use Azure Data Lake Tools for Visual Studio for that.</span></span> <span data-ttu-id="11840-108">Дополнительные сведения см. [здесь](data-lake-analytics-data-lake-tools-local-run.md).</span><span class="sxs-lookup"><span data-stu-id="11840-108">You can learn more from [here](data-lake-analytics-data-lake-tools-local-run.md).</span></span>

## <a name="install-azure-data-lake-u-sql-sdk"></a><span data-ttu-id="11840-109">Установка пакета SDK Azure Data Lake для U-SQL</span><span class="sxs-lookup"><span data-stu-id="11840-109">Install Azure Data Lake U-SQL SDK</span></span>

<span data-ttu-id="11840-110">Пакет SDK Azure Data Lake для U-SQL можно получить на сайте Nuget.org [здесь](https://www.nuget.org/packages/Microsoft.Azure.DataLake.USQL.SDK/).</span><span class="sxs-lookup"><span data-stu-id="11840-110">You can get the Azure Data Lake U-SQL SDK [here](https://www.nuget.org/packages/Microsoft.Azure.DataLake.USQL.SDK/) on Nuget.org.</span></span> <span data-ttu-id="11840-111">И перед его использованием необходимо убедиться, что у вас установлены приведенные ниже зависимости.</span><span class="sxs-lookup"><span data-stu-id="11840-111">And before using it, you need to make sure you have dependencies as follows.</span></span>

### <a name="dependencies"></a><span data-ttu-id="11840-112">Зависимости</span><span class="sxs-lookup"><span data-stu-id="11840-112">Dependencies</span></span>

<span data-ttu-id="11840-113">Для пакета SDK U-SQL для Data Lake требуются следующие зависимости:</span><span class="sxs-lookup"><span data-stu-id="11840-113">The Data Lake U-SQL SDK requires the following dependencies:</span></span>

- <span data-ttu-id="11840-114">[Microsoft .NET Framework 4.6 или более поздней версии](https://www.microsoft.com/download/details.aspx?id=17851).</span><span class="sxs-lookup"><span data-stu-id="11840-114">[Microsoft .NET Framework 4.6 or newer](https://www.microsoft.com/download/details.aspx?id=17851).</span></span>
- <span data-ttu-id="11840-115">Microsoft Visual C++ 14 и пакет SDK для Windows 10.0.10240.0 или более поздняя версия (в этой статье он называется пакетом CppSDK).</span><span class="sxs-lookup"><span data-stu-id="11840-115">Microsoft Visual C++ 14 and Windows SDK 10.0.10240.0 or newer (which is called CppSDK in this article).</span></span> <span data-ttu-id="11840-116">Пакет CppSDK можно получить двумя способами.</span><span class="sxs-lookup"><span data-stu-id="11840-116">There are two ways to get CppSDK:</span></span>

    - <span data-ttu-id="11840-117">Установка выпуска [Visual Studio Community](https://developer.microsoft.com/downloads/vs-thankyou).</span><span class="sxs-lookup"><span data-stu-id="11840-117">Install [Visual Studio Community Edition](https://developer.microsoft.com/downloads/vs-thankyou).</span></span> <span data-ttu-id="11840-118">В папке Program Files должна существовать папка \Windows Kits\10, например C:\Program Files (x86) \Windows Kits\10\.</span><span class="sxs-lookup"><span data-stu-id="11840-118">You'll have a \Windows Kits\10 folder under the Program Files folder--for example, C:\Program Files (x86)\Windows Kits\10\.</span></span> <span data-ttu-id="11840-119">Кроме того, в папке \Windows Kits\10\Lib находится версия пакета SDK для Windows 10.</span><span class="sxs-lookup"><span data-stu-id="11840-119">You'll also find the Windows 10 SDK version under \Windows Kits\10\Lib.</span></span> <span data-ttu-id="11840-120">Если у вас нет этих папок, переустановите Visual Studio и обязательно выберите пакет SDK для Windows 10 в процессе установки.</span><span class="sxs-lookup"><span data-stu-id="11840-120">If you don’t see these folders, reinstall Visual Studio and be sure to select the Windows 10 SDK during the installation.</span></span> <span data-ttu-id="11840-121">Если он установлен вместе с Visual Studio, локальный компилятор U-SQL обнаружит его автоматически.</span><span class="sxs-lookup"><span data-stu-id="11840-121">If you have this installed with Visual Studio, the U-SQL local compiler will find it automatically.</span></span>

    ![Пакет SDK Windows 10 для локального выполнения средств Data Lake для Visual Studio](./media/data-lake-analytics-data-lake-tools-local-run/data-lake-tools-for-visual-studio-local-run-windows-10-sdk.png)

    - <span data-ttu-id="11840-123">Установка [средств Data Lake для Visual Studio](http://aka.ms/adltoolsvs).</span><span class="sxs-lookup"><span data-stu-id="11840-123">Install [Data Lake Tools for Visual Studio](http://aka.ms/adltoolsvs).</span></span> <span data-ttu-id="11840-124">Предварительно упакованные файлы VC++ и SDK для Windows можно найти в каталоге C:\Program Files (x86)\Microsoft Visual Studio 14.0\Common7\IDE\Extensions\Microsoft\ADL Tools\X.X.XXXX.X\CppSDK.</span><span class="sxs-lookup"><span data-stu-id="11840-124">You can find the prepackaged Visual C++ and Windows SDK files at C:\Program Files (x86)\Microsoft Visual Studio 14.0\Common7\IDE\Extensions\Microsoft\ADL Tools\X.X.XXXX.X\CppSDK.</span></span> <span data-ttu-id="11840-125">В этом случае локальный компилятор U-SQL не сможет найти зависимости автоматически.</span><span class="sxs-lookup"><span data-stu-id="11840-125">In this case, the U-SQL local compiler cannot find the dependencies automatically.</span></span> <span data-ttu-id="11840-126">Вам потребуется указать путь к CppSDK.</span><span class="sxs-lookup"><span data-stu-id="11840-126">You need to specify the CppSDK path for it.</span></span> <span data-ttu-id="11840-127">Можно скопировать файлы в другое место или просто использовать стандартный путь.</span><span class="sxs-lookup"><span data-stu-id="11840-127">You can either copy the files to another location or use it as is.</span></span>

## <a name="understand-basic-concepts"></a><span data-ttu-id="11840-128">Основные понятия</span><span class="sxs-lookup"><span data-stu-id="11840-128">Understand basic concepts</span></span>

### <a name="data-root"></a><span data-ttu-id="11840-129">Корневая папка данных</span><span class="sxs-lookup"><span data-stu-id="11840-129">Data root</span></span>

<span data-ttu-id="11840-130">Корневая папка данных служит "локальным хранилищем" для локальной учетной записи среды вычислений.</span><span class="sxs-lookup"><span data-stu-id="11840-130">The data-root folder is a "local store" for the local compute account.</span></span> <span data-ttu-id="11840-131">Она действует так же, как учетная запись Azure Data Lake Store в учетной записи Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="11840-131">It's equivalent to the Azure Data Lake Store account of a Data Lake Analytics account.</span></span> <span data-ttu-id="11840-132">Переход на другую корневую папку данных аналогичен переходу на другую учетную запись хранения.</span><span class="sxs-lookup"><span data-stu-id="11840-132">Switching to a different data-root folder is just like switching to a different store account.</span></span> <span data-ttu-id="11840-133">Если вам нужен доступ к данным, которые совместно используются различными корневыми папками данных, следует использовать в скриптах абсолютные пути</span><span class="sxs-lookup"><span data-stu-id="11840-133">If you want to access commonly shared data with different data-root folders, you must use absolute paths in your scripts.</span></span> <span data-ttu-id="11840-134">или создать в корневой папке данных символические ссылки файловой системы (например, с помощью команды **mklink** для файловой системы NTFS), указывающие на совместно используемые данные.</span><span class="sxs-lookup"><span data-stu-id="11840-134">Or, create file system symbolic links (for example, **mklink** on NTFS) under the data-root folder to point to the shared data.</span></span>

<span data-ttu-id="11840-135">Корневая папка данных используется в следующих целях.</span><span class="sxs-lookup"><span data-stu-id="11840-135">The data-root folder is used to:</span></span>

- <span data-ttu-id="11840-136">Хранение локальных метаданных, включая базы данных, таблицы, функции с табличным значением (TVF) и сборки.</span><span class="sxs-lookup"><span data-stu-id="11840-136">Store local metadata, including databases, tables, table-valued functions (TVFs), and assemblies.</span></span>
- <span data-ttu-id="11840-137">Поиск путей ввода-вывода, которые определяются как относительные пути в U-SQL.</span><span class="sxs-lookup"><span data-stu-id="11840-137">Look up the input and output paths that are defined as relative paths in U-SQL.</span></span> <span data-ttu-id="11840-138">Использование относительных путей упрощает развертывание проектов U-SQL в Azure.</span><span class="sxs-lookup"><span data-stu-id="11840-138">Using relative paths makes it easier to deploy your U-SQL projects to Azure.</span></span>

### <a name="file-path-in-u-sql"></a><span data-ttu-id="11840-139">Путь к файлу в U-SQL</span><span class="sxs-lookup"><span data-stu-id="11840-139">File path in U-SQL</span></span>

<span data-ttu-id="11840-140">В скриптах U-SQL можно использовать как относительные, так и абсолютные локальные пути.</span><span class="sxs-lookup"><span data-stu-id="11840-140">You can use both a relative path and a local absolute path in U-SQL scripts.</span></span> <span data-ttu-id="11840-141">Относительный путь задается относительно пути к выбранной корневой папке данных.</span><span class="sxs-lookup"><span data-stu-id="11840-141">The relative path is relative to the specified data-root folder path.</span></span> <span data-ttu-id="11840-142">Мы советуем использовать в качестве разделителя пути символ "/", чтобы обеспечить совместимость скриптов с выполнением на стороне сервера.</span><span class="sxs-lookup"><span data-stu-id="11840-142">We recommend that you use "/" as the path separator to make your scripts compatible with the server side.</span></span> <span data-ttu-id="11840-143">Ниже приведены некоторые примеры относительных путей и их абсолютные эквиваленты.</span><span class="sxs-lookup"><span data-stu-id="11840-143">Here are some examples of relative paths and their equivalent absolute paths.</span></span> <span data-ttu-id="11840-144">В этих примерах предполагается, что мы используем корневую папку данных C:\LocalRunDataRoot.</span><span class="sxs-lookup"><span data-stu-id="11840-144">In these examples, C:\LocalRunDataRoot is the data-root folder.</span></span>

|<span data-ttu-id="11840-145">Относительный путь</span><span class="sxs-lookup"><span data-stu-id="11840-145">Relative path</span></span>|<span data-ttu-id="11840-146">Абсолютный путь</span><span class="sxs-lookup"><span data-stu-id="11840-146">Absolute path</span></span>|
|-------------|-------------|
|<span data-ttu-id="11840-147">/abc/def/input.csv</span><span class="sxs-lookup"><span data-stu-id="11840-147">/abc/def/input.csv</span></span> |<span data-ttu-id="11840-148">C:\LocalRunDataRoot\abc\def\input.csv</span><span class="sxs-lookup"><span data-stu-id="11840-148">C:\LocalRunDataRoot\abc\def\input.csv</span></span>|
|<span data-ttu-id="11840-149">abc/def/input.csv</span><span class="sxs-lookup"><span data-stu-id="11840-149">abc/def/input.csv</span></span>  |<span data-ttu-id="11840-150">C:\LocalRunDataRoot\abc\def\input.csv</span><span class="sxs-lookup"><span data-stu-id="11840-150">C:\LocalRunDataRoot\abc\def\input.csv</span></span>|
|<span data-ttu-id="11840-151">D:/abc/def/input.csv</span><span class="sxs-lookup"><span data-stu-id="11840-151">D:/abc/def/input.csv</span></span> |<span data-ttu-id="11840-152">D:\abc\def\input.csv</span><span class="sxs-lookup"><span data-stu-id="11840-152">D:\abc\def\input.csv</span></span>|

### <a name="working-directory"></a><span data-ttu-id="11840-153">Рабочий каталог</span><span class="sxs-lookup"><span data-stu-id="11840-153">Working directory</span></span>

<span data-ttu-id="11840-154">Если сценарий U-SQL выполняется локально, то рабочий каталог создается во время компиляции в текущем каталоге выполнения.</span><span class="sxs-lookup"><span data-stu-id="11840-154">When running the U-SQL script locally, a working directory is created during compilation under current running directory.</span></span> <span data-ttu-id="11840-155">В него записываются выходные данные процесса компиляции, а также здесь создается теневая копия всех файлов среды выполнения, которые требуются для локального выполнения.</span><span class="sxs-lookup"><span data-stu-id="11840-155">In addition to the compilation outputs, the needed runtime files for local execution will be shadow copied to this working directory.</span></span> <span data-ttu-id="11840-156">Корневая папка рабочего каталога называется ScopeWorkDir, и рабочий каталог содержит следующие файлы:</span><span class="sxs-lookup"><span data-stu-id="11840-156">The working directory root folder is called "ScopeWorkDir" and the files under the working directory are as follows:</span></span>

|<span data-ttu-id="11840-157">Каталог/файл</span><span class="sxs-lookup"><span data-stu-id="11840-157">Directory/file</span></span>|<span data-ttu-id="11840-158">Каталог/файл</span><span class="sxs-lookup"><span data-stu-id="11840-158">Directory/file</span></span>|<span data-ttu-id="11840-159">Каталог/файл</span><span class="sxs-lookup"><span data-stu-id="11840-159">Directory/file</span></span>|<span data-ttu-id="11840-160">Определение</span><span class="sxs-lookup"><span data-stu-id="11840-160">Definition</span></span>|<span data-ttu-id="11840-161">Описание</span><span class="sxs-lookup"><span data-stu-id="11840-161">Description</span></span>|
|--------------|--------------|--------------|----------|-----------|
|<span data-ttu-id="11840-162">C6A101DDCB470506</span><span class="sxs-lookup"><span data-stu-id="11840-162">C6A101DDCB470506</span></span>| | |<span data-ttu-id="11840-163">Хэш-строка версии среды выполнения</span><span class="sxs-lookup"><span data-stu-id="11840-163">Hash string of runtime version</span></span>|<span data-ttu-id="11840-164">Теневая копия файлов среды выполнения, необходимых для локального выполнения</span><span class="sxs-lookup"><span data-stu-id="11840-164">Shadow copy of runtime files needed for local execution</span></span>|
| |<span data-ttu-id="11840-165">Script_66AE4909AA0ED06C</span><span class="sxs-lookup"><span data-stu-id="11840-165">Script_66AE4909AA0ED06C</span></span>| |<span data-ttu-id="11840-166">Имя скрипта и хэш-строка пути к скрипту</span><span class="sxs-lookup"><span data-stu-id="11840-166">Script name + hash string of script path</span></span>|<span data-ttu-id="11840-167">Выходные данные компиляции и ведение журнала шагов выполнения</span><span class="sxs-lookup"><span data-stu-id="11840-167">Compilation outputs and execution step logging</span></span>|
| | |<span data-ttu-id="11840-168">\_script\_.abr</span><span class="sxs-lookup"><span data-stu-id="11840-168">\_script\_.abr</span></span>|<span data-ttu-id="11840-169">Выходные данные компилятора</span><span class="sxs-lookup"><span data-stu-id="11840-169">Compiler output</span></span>|<span data-ttu-id="11840-170">Файл Algebra</span><span class="sxs-lookup"><span data-stu-id="11840-170">Algebra file</span></span>|
| | |<span data-ttu-id="11840-171">\_ScopeCodeGen\_.*</span><span class="sxs-lookup"><span data-stu-id="11840-171">\_ScopeCodeGen\_.*</span></span>|<span data-ttu-id="11840-172">Выходные данные компилятора</span><span class="sxs-lookup"><span data-stu-id="11840-172">Compiler output</span></span>|<span data-ttu-id="11840-173">Созданный управляемый код</span><span class="sxs-lookup"><span data-stu-id="11840-173">Generated managed code</span></span>|
| | |<span data-ttu-id="11840-174">\_ScopeCodeGenEngine\_.*</span><span class="sxs-lookup"><span data-stu-id="11840-174">\_ScopeCodeGenEngine\_.*</span></span>|<span data-ttu-id="11840-175">Выходные данные компилятора</span><span class="sxs-lookup"><span data-stu-id="11840-175">Compiler output</span></span>|<span data-ttu-id="11840-176">Созданный собственный код</span><span class="sxs-lookup"><span data-stu-id="11840-176">Generated native code</span></span>|
| | |<span data-ttu-id="11840-177">referenced assemblies</span><span class="sxs-lookup"><span data-stu-id="11840-177">referenced assemblies</span></span>|<span data-ttu-id="11840-178">Ссылка на сборку</span><span class="sxs-lookup"><span data-stu-id="11840-178">Assembly reference</span></span>|<span data-ttu-id="11840-179">Связанные файлы сборок.</span><span class="sxs-lookup"><span data-stu-id="11840-179">Referenced assembly files</span></span>|
| | |<span data-ttu-id="11840-180">deployed_resources</span><span class="sxs-lookup"><span data-stu-id="11840-180">deployed_resources</span></span>|<span data-ttu-id="11840-181">Развертывание ресурсов</span><span class="sxs-lookup"><span data-stu-id="11840-181">Resource deployment</span></span>|<span data-ttu-id="11840-182">Файлы развертывания ресурсов</span><span class="sxs-lookup"><span data-stu-id="11840-182">Resource deployment files</span></span>|
| | |<span data-ttu-id="11840-183">xxxxxxxx.xxx[1..n]\_\*.*</span><span class="sxs-lookup"><span data-stu-id="11840-183">xxxxxxxx.xxx[1..n]\_\*.*</span></span>|<span data-ttu-id="11840-184">Журнал выполнения</span><span class="sxs-lookup"><span data-stu-id="11840-184">Execution log</span></span>|<span data-ttu-id="11840-185">Журнал шагов выполнения</span><span class="sxs-lookup"><span data-stu-id="11840-185">Log of execution steps</span></span>|


## <a name="use-the-sdk-from-the-command-line"></a><span data-ttu-id="11840-186">Использование пакета SDK из командной строки</span><span class="sxs-lookup"><span data-stu-id="11840-186">Use the SDK from the command line</span></span>

### <a name="command-line-interface-of-the-helper-application"></a><span data-ttu-id="11840-187">Интерфейс командной строки вспомогательного приложения</span><span class="sxs-lookup"><span data-stu-id="11840-187">Command-line interface of the helper application</span></span>

<span data-ttu-id="11840-188">Файл LocalRunHelper.exe в каталоге directory\build\runtime пакета SDK содержит вспомогательное приложение командной строки, которое предоставляет интерфейсы для большинства распространенных функций локального выполнения.</span><span class="sxs-lookup"><span data-stu-id="11840-188">Under SDK directory\build\runtime, LocalRunHelper.exe is the command-line helper application that provides interfaces to most of the commonly used local-run functions.</span></span> <span data-ttu-id="11840-189">Обратите внимание, что в командах и параметрах аргументов учитывается регистр.</span><span class="sxs-lookup"><span data-stu-id="11840-189">Note that both the command and the argument switches are case-sensitive.</span></span> <span data-ttu-id="11840-190">Для вызова вспомогательного приложения выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="11840-190">To invoke it:</span></span>

    LocalRunHelper.exe <command> <Required-Command-Arguments> [Optional-Command-Arguments]

<span data-ttu-id="11840-191">Если запустить LocalRunHelper.exe без аргументов или с параметром **help**, отобразятся справочные сведения:</span><span class="sxs-lookup"><span data-stu-id="11840-191">Run LocalRunHelper.exe without arguments or with the **help** switch to show the help information:</span></span>

    > LocalRunHelper.exe help

        Command 'help' :  Show usage information
        Command 'compile' :  Compile the script
        Required Arguments :
            -Script param
                    Script File Path
        Optional Arguments :
            -Shallow [default value 'False']
                    Shallow compile

<span data-ttu-id="11840-192">Эта справочная информация содержит следующие элементы.</span><span class="sxs-lookup"><span data-stu-id="11840-192">In the help information:</span></span>

-  <span data-ttu-id="11840-193">**Command** определяет имя выполняемой команды.</span><span class="sxs-lookup"><span data-stu-id="11840-193">**Command** gives the command’s name.</span></span>  
-  <span data-ttu-id="11840-194">**Required Argument** перечисляет обязательные аргументы.</span><span class="sxs-lookup"><span data-stu-id="11840-194">**Required Argument** lists arguments that must be supplied.</span></span>  
-  <span data-ttu-id="11840-195">**Optional Argument** перечисляет необязательные аргументы и приводит для них значения по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="11840-195">**Optional Argument** lists arguments that are optional, with default values.</span></span>  <span data-ttu-id="11840-196">Если необязательный аргумент имеет тип логического значения, он не принимает дополнительные параметры, и тогда его наличие определяет поведение, противоположное значению по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="11840-196">Optional Boolean arguments don’t have parameters, and their appearances mean negative to their default value.</span></span>

### <a name="return-value-and-logging"></a><span data-ttu-id="11840-197">Возвращаемое значение и ведение журнала</span><span class="sxs-lookup"><span data-stu-id="11840-197">Return value and logging</span></span>

<span data-ttu-id="11840-198">Вспомогательное приложение возвращает значение **0** в случае успешного выполнения или **-1** в случае сбоя.</span><span class="sxs-lookup"><span data-stu-id="11840-198">The helper application returns **0** for success and **-1** for failure.</span></span> <span data-ttu-id="11840-199">По умолчанию вспомогательное приложение отправляет все служебные сообщения в текущую консоль.</span><span class="sxs-lookup"><span data-stu-id="11840-199">By default, the helper sends all messages to the current console.</span></span> <span data-ttu-id="11840-200">Однако большинство команд поддерживает необязательный аргумент **-MessageOut path_to_log_file**, который позволяет перенаправлять выходные данные в файл журнала.</span><span class="sxs-lookup"><span data-stu-id="11840-200">However, most of the commands support the **-MessageOut path_to_log_file** optional argument that redirects the outputs to a log file.</span></span>

### <a name="environment-variable-configuring"></a><span data-ttu-id="11840-201">Настройка переменной среды</span><span class="sxs-lookup"><span data-stu-id="11840-201">Environment variable configuring</span></span>

<span data-ttu-id="11840-202">Для локального выполнения U-SQL требуется указать корневую папку данных в качестве локальной учетной записи хранения, а также указать путь к пакету CppSDK для зависимостей.</span><span class="sxs-lookup"><span data-stu-id="11840-202">U-SQL local run needs a specified data root as local storage account, as well as a specified CppSDK path for dependencies.</span></span> <span data-ttu-id="11840-203">Эти значения можно задать с помощью аргумента в командной строке или переменной среды.</span><span class="sxs-lookup"><span data-stu-id="11840-203">You can both set the argument in command-line or set environment variable for them.</span></span>

- <span data-ttu-id="11840-204">Настройка переменной среды **SCOPE_CPP_SDK**.</span><span class="sxs-lookup"><span data-stu-id="11840-204">Set the **SCOPE_CPP_SDK** environment variable.</span></span>

    <span data-ttu-id="11840-205">Если для получения Microsoft Visual C++ и пакета SDK для Windows вы установили средства Data Lake для Visual Studio, убедитесь в наличии следующей папки:</span><span class="sxs-lookup"><span data-stu-id="11840-205">If you get Microsoft Visual C++ and the Windows SDK by installing Data Lake Tools for Visual Studio, verify that you have the following folder:</span></span>

        C:\Program Files (x86)\Microsoft Visual Studio 14.0\Common7\IDE\Extensions\Microsoft\Microsoft Azure Data Lake Tools for Visual Studio 2015\X.X.XXXX.X\CppSDK

    <span data-ttu-id="11840-206">Определите новую переменную среды с именем **SCOPE_CPP_SDK**, которая будет указывать на этот каталог.</span><span class="sxs-lookup"><span data-stu-id="11840-206">Define a new environment variable called **SCOPE_CPP_SDK** to point to this directory.</span></span> <span data-ttu-id="11840-207">Можно также скопировать эту папку в другое расположение и указать новый путь к ней в переменной среды **SCOPE_CPP_SDK**.</span><span class="sxs-lookup"><span data-stu-id="11840-207">Or copy the folder to the other location and specify **SCOPE_CPP_SDK** as that.</span></span>

    <span data-ttu-id="11840-208">Кроме настройки переменной среды, вы можете использовать аргумент **-CppSDK** в командной строке.</span><span class="sxs-lookup"><span data-stu-id="11840-208">In addition to setting the environment variable, you can specify the **-CppSDK** argument when you're using the command line.</span></span> <span data-ttu-id="11840-209">Этот аргумент переопределяет используемую по умолчанию переменную среды CppSDK.</span><span class="sxs-lookup"><span data-stu-id="11840-209">This argument overwrites your default CppSDK environment variable.</span></span>

- <span data-ttu-id="11840-210">Настройка переменной среды **LOCALRUN_DATAROOT**.</span><span class="sxs-lookup"><span data-stu-id="11840-210">Set the **LOCALRUN_DATAROOT** environment variable.</span></span>

    <span data-ttu-id="11840-211">Определите новую переменную среды с именем **LOCALRUN_DATAROOT**, которая будет указывать на корневую папку данных.</span><span class="sxs-lookup"><span data-stu-id="11840-211">Define a new environment variable called **LOCALRUN_DATAROOT** that points to the data root.</span></span>

    <span data-ttu-id="11840-212">Кроме настройки переменной среды, вы можете использовать аргумент **-DataRoot** в командной строке, который указывает на корневую папку данных.</span><span class="sxs-lookup"><span data-stu-id="11840-212">In addition to setting the environment variable, you can specify the **-DataRoot** argument with the data-root path when you're using a command line.</span></span> <span data-ttu-id="11840-213">Этот аргумент переопределяет используемую по умолчанию переменную среды, задающую путь к корневой папке данных.</span><span class="sxs-lookup"><span data-stu-id="11840-213">This argument overwrites your default data-root environment variable.</span></span> <span data-ttu-id="11840-214">Этот аргумент необходимо добавлять во все выполняемые командные строки, чтобы переопределить используемую по умолчанию переменную среды, задающую путь к корневой папке данных, для всех операций.</span><span class="sxs-lookup"><span data-stu-id="11840-214">You need to add this argument to every command line you're running so that you can overwrite the default data-root environment variable for all operations.</span></span>

### <a name="sdk-command-line-usage-samples"></a><span data-ttu-id="11840-215">Примеры использования командной строки пакета SDK</span><span class="sxs-lookup"><span data-stu-id="11840-215">SDK command line usage samples</span></span>

#### <a name="compile-and-run"></a><span data-ttu-id="11840-216">Компиляция и запуск</span><span class="sxs-lookup"><span data-stu-id="11840-216">Compile and run</span></span>

<span data-ttu-id="11840-217">Команда **run** компилирует скрипт и выполняет программу, полученную в результате компиляции.</span><span class="sxs-lookup"><span data-stu-id="11840-217">The **run** command is used to compile the script and then execute compiled results.</span></span> <span data-ttu-id="11840-218">Эта команда принимает все аргументы командной строки, которые доступны для команд **compile** и **execute**.</span><span class="sxs-lookup"><span data-stu-id="11840-218">Its command-line arguments are a combination of those from **compile** and **execute**.</span></span>

    LocalRunHelper run -Script path_to_usql_script.usql [optional_arguments]

<span data-ttu-id="11840-219">Ниже приведены необязательные аргументы для команды **run**.</span><span class="sxs-lookup"><span data-stu-id="11840-219">The following are optional arguments for **run**:</span></span>


|<span data-ttu-id="11840-220">Аргумент</span><span class="sxs-lookup"><span data-stu-id="11840-220">Argument</span></span>|<span data-ttu-id="11840-221">Значение по умолчанию</span><span class="sxs-lookup"><span data-stu-id="11840-221">Default value</span></span>|<span data-ttu-id="11840-222">Описание</span><span class="sxs-lookup"><span data-stu-id="11840-222">Description</span></span>|
|--------|-------------|-----------|
|<span data-ttu-id="11840-223">-CodeBehind</span><span class="sxs-lookup"><span data-stu-id="11840-223">-CodeBehind</span></span>|<span data-ttu-id="11840-224">Ложь</span><span class="sxs-lookup"><span data-stu-id="11840-224">False</span></span>|<span data-ttu-id="11840-225">Сценарий содержит код программной части .cs.</span><span class="sxs-lookup"><span data-stu-id="11840-225">The script has .cs code behind</span></span>|
|<span data-ttu-id="11840-226">-CppSDK</span><span class="sxs-lookup"><span data-stu-id="11840-226">-CppSDK</span></span>| |<span data-ttu-id="11840-227">Каталог CppSDK.</span><span class="sxs-lookup"><span data-stu-id="11840-227">CppSDK Directory</span></span>|
|<span data-ttu-id="11840-228">-DataRoot</span><span class="sxs-lookup"><span data-stu-id="11840-228">-DataRoot</span></span>| <span data-ttu-id="11840-229">Переменная среды DataRoot</span><span class="sxs-lookup"><span data-stu-id="11840-229">DataRoot environment variable</span></span>|<span data-ttu-id="11840-230">Корневая папка для локального выполнения. По умолчанию используется значение из переменной среды LOCALRUN_DATAROOT.</span><span class="sxs-lookup"><span data-stu-id="11840-230">DataRoot for local run, default to 'LOCALRUN_DATAROOT' environment variable</span></span>|
|<span data-ttu-id="11840-231">-MessageOut</span><span class="sxs-lookup"><span data-stu-id="11840-231">-MessageOut</span></span>| |<span data-ttu-id="11840-232">Сохранение в файл всех сообщений, предназначенных для вывода на консоль.</span><span class="sxs-lookup"><span data-stu-id="11840-232">Dump messages on console to a file</span></span>|
|<span data-ttu-id="11840-233">-Parallel</span><span class="sxs-lookup"><span data-stu-id="11840-233">-Parallel</span></span>|<span data-ttu-id="11840-234">1</span><span class="sxs-lookup"><span data-stu-id="11840-234">1</span></span>|<span data-ttu-id="11840-235">Запуск плана с указанным значением параллелизма.</span><span class="sxs-lookup"><span data-stu-id="11840-235">Run the plan with the specified parallelism</span></span>|
|<span data-ttu-id="11840-236">-References</span><span class="sxs-lookup"><span data-stu-id="11840-236">-References</span></span>| |<span data-ttu-id="11840-237">Список путей к дополнительным справочным сборкам или файлам данных кода программной части с разделителем ";".</span><span class="sxs-lookup"><span data-stu-id="11840-237">List of paths to extra reference assemblies or data files of code behind, separated by ';'</span></span>|
|<span data-ttu-id="11840-238">-UdoRedirect</span><span class="sxs-lookup"><span data-stu-id="11840-238">-UdoRedirect</span></span>|<span data-ttu-id="11840-239">Ложь</span><span class="sxs-lookup"><span data-stu-id="11840-239">False</span></span>|<span data-ttu-id="11840-240">Создание конфигурации перенаправления сборки Udo.</span><span class="sxs-lookup"><span data-stu-id="11840-240">Generate Udo assembly redirect config</span></span>|
|<span data-ttu-id="11840-241">-UseDatabase</span><span class="sxs-lookup"><span data-stu-id="11840-241">-UseDatabase</span></span>|<span data-ttu-id="11840-242">master</span><span class="sxs-lookup"><span data-stu-id="11840-242">master</span></span>|<span data-ttu-id="11840-243">База данных, в которой нужно регистрировать временную сборку кода программной части.</span><span class="sxs-lookup"><span data-stu-id="11840-243">Database to use for code behind temporary assembly registration</span></span>|
|<span data-ttu-id="11840-244">-Verbose</span><span class="sxs-lookup"><span data-stu-id="11840-244">-Verbose</span></span>|<span data-ttu-id="11840-245">Ложь</span><span class="sxs-lookup"><span data-stu-id="11840-245">False</span></span>|<span data-ttu-id="11840-246">Отображение подробных выходных данных среды выполнения.</span><span class="sxs-lookup"><span data-stu-id="11840-246">Show detailed outputs from runtime</span></span>|
|<span data-ttu-id="11840-247">-WorkDir</span><span class="sxs-lookup"><span data-stu-id="11840-247">-WorkDir</span></span>|<span data-ttu-id="11840-248">Текущий каталог</span><span class="sxs-lookup"><span data-stu-id="11840-248">Current Directory</span></span>|<span data-ttu-id="11840-249">Задает каталог для работы и выходных данных компилятора.</span><span class="sxs-lookup"><span data-stu-id="11840-249">Directory for compiler usage and outputs</span></span>|
|<span data-ttu-id="11840-250">-RunScopeCEP</span><span class="sxs-lookup"><span data-stu-id="11840-250">-RunScopeCEP</span></span>|<span data-ttu-id="11840-251">0</span><span class="sxs-lookup"><span data-stu-id="11840-251">0</span></span>|<span data-ttu-id="11840-252">Используемый режим ScopeCEP.</span><span class="sxs-lookup"><span data-stu-id="11840-252">ScopeCEP mode to use</span></span>|
|<span data-ttu-id="11840-253">-ScopeCEPTempPath</span><span class="sxs-lookup"><span data-stu-id="11840-253">-ScopeCEPTempPath</span></span>|<span data-ttu-id="11840-254">temp</span><span class="sxs-lookup"><span data-stu-id="11840-254">temp</span></span>|<span data-ttu-id="11840-255">Временный путь для потоковой передачи данных.</span><span class="sxs-lookup"><span data-stu-id="11840-255">Temp path to use for streaming data</span></span>|
|<span data-ttu-id="11840-256">-OptFlags</span><span class="sxs-lookup"><span data-stu-id="11840-256">-OptFlags</span></span>| |<span data-ttu-id="11840-257">Разделенный запятыми список флагов оптимизатора.</span><span class="sxs-lookup"><span data-stu-id="11840-257">Comma-separated list of optimizer flags</span></span>|


<span data-ttu-id="11840-258">Ниже приведен пример:</span><span class="sxs-lookup"><span data-stu-id="11840-258">Here's an example:</span></span>

    LocalRunHelper run -Script d:\test\test1.usql -WorkDir d:\test\bin -CodeBehind -References "d:\asm\ref1.dll;d:\asm\ref2.dll" -UseDatabase testDB –Parallel 5 -Verbose

<span data-ttu-id="11840-259">Операции **compile** и **execute** можно также выполнять по отдельности.</span><span class="sxs-lookup"><span data-stu-id="11840-259">Besides combining **compile** and **execute**, you can compile and execute the compiled executables separately.</span></span>

#### <a name="compile-a-u-sql-script"></a><span data-ttu-id="11840-260">Компиляция скрипта U-SQL</span><span class="sxs-lookup"><span data-stu-id="11840-260">Compile a U-SQL script</span></span>

<span data-ttu-id="11840-261">Команда **compile** позволяет выполнить компиляцию скрипта U-SQL в исполняемые файлы.</span><span class="sxs-lookup"><span data-stu-id="11840-261">The **compile** command is used to compile a U-SQL script to executables.</span></span>

    LocalRunHelper compile -Script path_to_usql_script.usql [optional_arguments]

<span data-ttu-id="11840-262">Ниже приведены необязательные аргументы для команды **compile**.</span><span class="sxs-lookup"><span data-stu-id="11840-262">The following are optional arguments for **compile**:</span></span>


|<span data-ttu-id="11840-263">Аргумент</span><span class="sxs-lookup"><span data-stu-id="11840-263">Argument</span></span>|<span data-ttu-id="11840-264">Описание</span><span class="sxs-lookup"><span data-stu-id="11840-264">Description</span></span>|
|--------|-----------|
| <span data-ttu-id="11840-265">-CodeBehind [значение по умолчанию False]</span><span class="sxs-lookup"><span data-stu-id="11840-265">-CodeBehind [default value 'False']</span></span>|<span data-ttu-id="11840-266">Сценарий содержит код программной части .cs.</span><span class="sxs-lookup"><span data-stu-id="11840-266">The script has .cs code behind</span></span>|
| <span data-ttu-id="11840-267">-CppSDK [значение по умолчанию "]</span><span class="sxs-lookup"><span data-stu-id="11840-267">-CppSDK [default value '']</span></span>|<span data-ttu-id="11840-268">Каталог CppSDK.</span><span class="sxs-lookup"><span data-stu-id="11840-268">CppSDK Directory</span></span>|
| <span data-ttu-id="11840-269">-DataRoot [значение по умолчанию: переменная среды DataRoot]</span><span class="sxs-lookup"><span data-stu-id="11840-269">-DataRoot [default value 'DataRoot environment variable']</span></span>|<span data-ttu-id="11840-270">Корневая папка для локального выполнения. По умолчанию используется значение из переменной среды LOCALRUN_DATAROOT.</span><span class="sxs-lookup"><span data-stu-id="11840-270">DataRoot for local run, default to 'LOCALRUN_DATAROOT' environment variable</span></span>|
| <span data-ttu-id="11840-271">-MessageOut [значение по умолчанию "]</span><span class="sxs-lookup"><span data-stu-id="11840-271">-MessageOut [default value '']</span></span>|<span data-ttu-id="11840-272">Сохранение в файл всех сообщений, предназначенных для вывода на консоль.</span><span class="sxs-lookup"><span data-stu-id="11840-272">Dump messages on console to a file</span></span>|
| <span data-ttu-id="11840-273">-References [значение по умолчанию "]</span><span class="sxs-lookup"><span data-stu-id="11840-273">-References [default value '']</span></span>|<span data-ttu-id="11840-274">Список путей к дополнительным справочным сборкам или файлам данных кода программной части с разделителем ";".</span><span class="sxs-lookup"><span data-stu-id="11840-274">List of paths to extra reference assemblies or data files of code behind, separated by ';'</span></span>|
| <span data-ttu-id="11840-275">-Shallow [значение по умолчанию False]</span><span class="sxs-lookup"><span data-stu-id="11840-275">-Shallow [default value 'False']</span></span>|<span data-ttu-id="11840-276">Неполная компиляция.</span><span class="sxs-lookup"><span data-stu-id="11840-276">Shallow compile</span></span>|
| <span data-ttu-id="11840-277">-UdoRedirect [значение по умолчанию False]</span><span class="sxs-lookup"><span data-stu-id="11840-277">-UdoRedirect [default value 'False']</span></span>|<span data-ttu-id="11840-278">Создание конфигурации перенаправления сборки Udo.</span><span class="sxs-lookup"><span data-stu-id="11840-278">Generate Udo assembly redirect config</span></span>|
| <span data-ttu-id="11840-279">-UseDatabase [значение по умолчанию master]</span><span class="sxs-lookup"><span data-stu-id="11840-279">-UseDatabase [default value 'master']</span></span>|<span data-ttu-id="11840-280">База данных, в которой нужно регистрировать временную сборку кода программной части.</span><span class="sxs-lookup"><span data-stu-id="11840-280">Database to use for code behind temporary assembly registration</span></span>|
| <span data-ttu-id="11840-281">-WorkDir [значение по умолчанию: текущий каталог]</span><span class="sxs-lookup"><span data-stu-id="11840-281">-WorkDir [default value 'Current Directory']</span></span>|<span data-ttu-id="11840-282">Задает каталог для работы и выходных данных компилятора.</span><span class="sxs-lookup"><span data-stu-id="11840-282">Directory for compiler usage and outputs</span></span>|
| <span data-ttu-id="11840-283">-RunScopeCEP [значение по умолчанию: "0"]</span><span class="sxs-lookup"><span data-stu-id="11840-283">-RunScopeCEP [default value '0']</span></span>|<span data-ttu-id="11840-284">Используемый режим ScopeCEP.</span><span class="sxs-lookup"><span data-stu-id="11840-284">ScopeCEP mode to use</span></span>|
| <span data-ttu-id="11840-285">-ScopeCEPTempPath [значение по умолчанию: "temp"]</span><span class="sxs-lookup"><span data-stu-id="11840-285">-ScopeCEPTempPath [default value 'temp']</span></span>|<span data-ttu-id="11840-286">Временный путь для потоковой передачи данных.</span><span class="sxs-lookup"><span data-stu-id="11840-286">Temp path to use for streaming data</span></span>|
| <span data-ttu-id="11840-287">-OptFlags [значение по умолчанию: "]</span><span class="sxs-lookup"><span data-stu-id="11840-287">-OptFlags [default value '']</span></span>|<span data-ttu-id="11840-288">Разделенный запятыми список флагов оптимизатора.</span><span class="sxs-lookup"><span data-stu-id="11840-288">Comma-separated list of optimizer flags</span></span>|


<span data-ttu-id="11840-289">Вот несколько примеров использования команды.</span><span class="sxs-lookup"><span data-stu-id="11840-289">Here are some usage examples.</span></span>

<span data-ttu-id="11840-290">Компиляция скрипта U-SQL:</span><span class="sxs-lookup"><span data-stu-id="11840-290">Compile a U-SQL script:</span></span>

    LocalRunHelper compile -Script d:\test\test1.usql

<span data-ttu-id="11840-291">Компиляция скрипта U-SQL с определенной корневой папкой данных</span><span class="sxs-lookup"><span data-stu-id="11840-291">Compile a U-SQL script and set the data-root folder.</span></span> <span data-ttu-id="11840-292">(обратите внимание, что этот аргумент переопределяет заданную переменную среды):</span><span class="sxs-lookup"><span data-stu-id="11840-292">Note that this will overwrite the set environment variable.</span></span>

    LocalRunHelper compile -Script d:\test\test1.usql –DataRoot c:\DataRoot

<span data-ttu-id="11840-293">Компиляция скрипта U-SQL с определенным рабочим каталогом и ссылками на сборку и базу данных:</span><span class="sxs-lookup"><span data-stu-id="11840-293">Compile a U-SQL script and set a working directory, reference assembly, and database:</span></span>

    LocalRunHelper compile -Script d:\test\test1.usql -WorkDir d:\test\bin -References "d:\asm\ref1.dll;d:\asm\ref2.dll" -UseDatabase testDB

#### <a name="execute-compiled-results"></a><span data-ttu-id="11840-294">Выполнение скомпилированного результата</span><span class="sxs-lookup"><span data-stu-id="11840-294">Execute compiled results</span></span>

<span data-ttu-id="11840-295">Команда **execute** используется для выполнения скомпилированного результата.</span><span class="sxs-lookup"><span data-stu-id="11840-295">The **execute** command is used to execute compiled results.</span></span>   

    LocalRunHelper execute -Algebra path_to_compiled_algebra_file [optional_arguments]

<span data-ttu-id="11840-296">Ниже приведены необязательные аргументы для команды **execute**.</span><span class="sxs-lookup"><span data-stu-id="11840-296">The following are optional arguments for **execute**:</span></span>

|<span data-ttu-id="11840-297">Аргумент</span><span class="sxs-lookup"><span data-stu-id="11840-297">Argument</span></span>|<span data-ttu-id="11840-298">Описание</span><span class="sxs-lookup"><span data-stu-id="11840-298">Description</span></span>|
|--------|-----------|
|<span data-ttu-id="11840-299">-DataRoot [значение по умолчанию "]</span><span class="sxs-lookup"><span data-stu-id="11840-299">-DataRoot [default value '']</span></span>|<span data-ttu-id="11840-300">Корневая папка для обработки метаданных.</span><span class="sxs-lookup"><span data-stu-id="11840-300">Data root for metadata execution.</span></span> <span data-ttu-id="11840-301">По умолчанию используется переменная среды **LOCALRUN_DATAROOT**.</span><span class="sxs-lookup"><span data-stu-id="11840-301">It defaults to the **LOCALRUN_DATAROOT** environment variable.</span></span>|
|<span data-ttu-id="11840-302">-MessageOut [значение по умолчанию "]</span><span class="sxs-lookup"><span data-stu-id="11840-302">-MessageOut [default value '']</span></span>|<span data-ttu-id="11840-303">Сохранение в файл всех сообщений, предназначенных для вывода на консоль.</span><span class="sxs-lookup"><span data-stu-id="11840-303">Dump messages on the console to a file.</span></span>|
|<span data-ttu-id="11840-304">-Parallel [значение по умолчанию 1]</span><span class="sxs-lookup"><span data-stu-id="11840-304">-Parallel [default value '1']</span></span>|<span data-ttu-id="11840-305">Показатель выполнения созданных шагов локального выполнения на указанном уровне параллелизма.</span><span class="sxs-lookup"><span data-stu-id="11840-305">Indicator to run the generated local-run steps with the specified parallelism level.</span></span>|
|<span data-ttu-id="11840-306">-Verbose [значение по умолчанию False]</span><span class="sxs-lookup"><span data-stu-id="11840-306">-Verbose [default value 'False']</span></span>|<span data-ttu-id="11840-307">Показатель отображения подробных выходных данных среды выполнения.</span><span class="sxs-lookup"><span data-stu-id="11840-307">Indicator to show detailed outputs from runtime.</span></span>|

<span data-ttu-id="11840-308">Пример использования этой команды:</span><span class="sxs-lookup"><span data-stu-id="11840-308">Here's a usage example:</span></span>

    LocalRunHelper execute -Algebra d:\test\workdir\C6A101DDCB470506\Script_66AE4909AA0ED06C\__script__.abr –DataRoot c:\DataRoot –Parallel 5


## <a name="use-the-sdk-with-programming-interfaces"></a><span data-ttu-id="11840-309">Использование пакета SDK с программными интерфейсами</span><span class="sxs-lookup"><span data-stu-id="11840-309">Use the SDK with programming interfaces</span></span>

<span data-ttu-id="11840-310">Все программные интерфейсы размещены в LocalRunHelper.exe.</span><span class="sxs-lookup"><span data-stu-id="11840-310">The programming interfaces are all located in the LocalRunHelper.exe.</span></span> <span data-ttu-id="11840-311">Они позволяют объединить функциональность пакетов SDK U-SQL и тестовой платформы C#, чтобы масштабировать локальное тестирование скрипта U-SQL.</span><span class="sxs-lookup"><span data-stu-id="11840-311">You can use them to integrate the functionality of the U-SQL SDK and the C# test framework to scale your U-SQL script local test.</span></span> <span data-ttu-id="11840-312">В этой статье я буду использовать стандартный проект модульного теста C#, чтобы показать, как использовать эти интерфейсы для тестирования сценария U-SQL.</span><span class="sxs-lookup"><span data-stu-id="11840-312">In this article, I will use the standard C# unit test project to show how to use these interfaces to test your U-SQL script.</span></span>

### <a name="step-1-create-c-unit-test-project-and-configuration"></a><span data-ttu-id="11840-313">Шаг 1. Создание проекта модульного теста C# и его настройка</span><span class="sxs-lookup"><span data-stu-id="11840-313">Step 1: Create C# unit test project and configuration</span></span>

- <span data-ttu-id="11840-314">Создайте проект модульного теста C#, выбрав "Файл" > "Создать" > "Проект" > "Visual C#" > "Тест" > "Проект модульного теста".</span><span class="sxs-lookup"><span data-stu-id="11840-314">Create a C# unit test project through File > New > Project > Visual C# > Test > Unit Test Project.</span></span>
- <span data-ttu-id="11840-315">Добавьте в проект ссылку на LocalRunHelper.exe.</span><span class="sxs-lookup"><span data-stu-id="11840-315">Add LocalRunHelper.exe as a reference for the project.</span></span> <span data-ttu-id="11840-316">LocalRunHelper.exe находится в папке \build\runtime в пакете NuGet.</span><span class="sxs-lookup"><span data-stu-id="11840-316">The LocalRunHelper.exe is located at \build\runtime\LocalRunHelper.exe in Nuget package.</span></span>

    ![Добавление ссылки на пакет SDK Azure Data Lake для U-SQL](./media/data-lake-analytics-u-sql-sdk/data-lake-analytics-u-sql-sdk-add-reference.png)

- <span data-ttu-id="11840-318">Пакет SDK для U-SQL поддерживает **только** среду x64, поэтому обязательно задайте в качестве цели платформу сборки x64.</span><span class="sxs-lookup"><span data-stu-id="11840-318">U-SQL SDK **only** support x64 environment, make sure to set build platform target as x64.</span></span> <span data-ttu-id="11840-319">Это можно сделать, выбрав "Свойство проекта" > "Сборка" > "Целевая платформа".</span><span class="sxs-lookup"><span data-stu-id="11840-319">You can set that through Project Property > Build > Platform target.</span></span>

    ![Настройка платформы x64 в проекте для использования пакета SDK Azure Data Lake для U-SQL](./media/data-lake-analytics-u-sql-sdk/data-lake-analytics-u-sql-sdk-configure-x64.png)

- <span data-ttu-id="11840-321">Обязательно задайте тестовую среду x64.</span><span class="sxs-lookup"><span data-stu-id="11840-321">Make sure to set your test environment as x64.</span></span> <span data-ttu-id="11840-322">В Visual Studio это можно сделать, выбрав "Тест" > "Параметры теста" > " 	Архитектура процессора по умолчанию" > "x64".</span><span class="sxs-lookup"><span data-stu-id="11840-322">In Visual Studio, you can set it through Test > Test Settings > Default Processor Architecture > x64.</span></span>

    ![Настройка тестовой среды x64 для использования пакета SDK Azure Data Lake для U-SQL](./media/data-lake-analytics-u-sql-sdk/data-lake-analytics-u-sql-sdk-configure-test-x64.png)

- <span data-ttu-id="11840-324">Обязательно скопируйте все файлы зависимостей из NugetPackage\build\runtime в рабочий каталог, который обычно находится в каталоге проекта ProjectFolder\bin\x64\Debug.</span><span class="sxs-lookup"><span data-stu-id="11840-324">Make sure to copy all dependency files under NugetPackage\build\runtime\ to project working directory which is usually under ProjectFolder\bin\x64\Debug.</span></span>

### <a name="step-2-create-u-sql-script-test-case"></a><span data-ttu-id="11840-325">Шаг 2. Создание тестового случая сценария U-SQL</span><span class="sxs-lookup"><span data-stu-id="11840-325">Step 2: Create U-SQL script test case</span></span>

<span data-ttu-id="11840-326">Ниже приведен пример кода для теста сценария U-SQL.</span><span class="sxs-lookup"><span data-stu-id="11840-326">Below is the sample code for U-SQL script test.</span></span> <span data-ttu-id="11840-327">Для тестирования необходимо подготовить сценарии, входные файлы и ожидаемые выходные файлы.</span><span class="sxs-lookup"><span data-stu-id="11840-327">For testing, you need to prepare scripts, input files and expected output files.</span></span>

    using System;
    using Microsoft.VisualStudio.TestTools.UnitTesting;
    using System.IO;
    using System.Text;
    using System.Security.Cryptography;
    using Microsoft.Analytics.LocalRun;

    namespace UnitTestProject1
    {
        [TestClass]
        public class USQLUnitTest
        {
            [TestMethod]
            public void TestUSQLScript()
            {
                //Specify the local run message output path
                StreamWriter MessageOutput = new StreamWriter("../../../log.txt");

                LocalRunHelper localrun = new LocalRunHelper(MessageOutput);

                //Configure the DateRoot path, Script Path and CPPSDK path
                localrun.DataRoot = "../../../";
                localrun.ScriptPath = "../../../Script/Script.usql";
                localrun.CppSdkDir = "../../../CppSDK";

                //Run U-SQL script
                localrun.DoRun();

                //Script output 
                string Result = Path.Combine(localrun.DataRoot, "Output/result.csv");

                //Expected script output
                string ExpectedResult = "../../../ExpectedOutput/result.csv";

                Test.Helpers.FileAssert.AreEqual(Result, ExpectedResult);

                //Don't forget to close MessageOutput to get logs into file
                MessageOutput.Close();
            }
        }
    }

    namespace Test.Helpers
    {
        public static class FileAssert
        {
            static string GetFileHash(string filename)
            {
                Assert.IsTrue(File.Exists(filename));

                using (var hash = new SHA1Managed())
                {
                    var clearBytes = File.ReadAllBytes(filename);
                    var hashedBytes = hash.ComputeHash(clearBytes);
                    return ConvertBytesToHex(hashedBytes);
                }
            }

            static string ConvertBytesToHex(byte[] bytes)
            {
                var sb = new StringBuilder();

                for (var i = 0; i < bytes.Length; i++)
                {
                    sb.Append(bytes[i].ToString("x"));
                }
                return sb.ToString();
            }

            public static void AreEqual(string filename1, string filename2)
            {
                string hash1 = GetFileHash(filename1);
                string hash2 = GetFileHash(filename2);

                Assert.AreEqual(hash1, hash2);
            }
        }
    }


### <a name="programming-interfaces-in-localrunhelperexe"></a><span data-ttu-id="11840-328">Программные интерфейсы в LocalRunHelper.exe</span><span class="sxs-lookup"><span data-stu-id="11840-328">Programming interfaces in LocalRunHelper.exe</span></span>

<span data-ttu-id="11840-329">LocalRunHelper.exe предоставляет программные интерфейсы для локальных операций компиляции U-SQL, выполнения U-SQL и т. д. Эти интерфейсы перечислены ниже.</span><span class="sxs-lookup"><span data-stu-id="11840-329">LocalRunHelper.exe provides the programming interfaces for U-SQL local compile, run, etc. The interfaces are listed as follows.</span></span>

<span data-ttu-id="11840-330">**Конструктор**</span><span class="sxs-lookup"><span data-stu-id="11840-330">**Constructor**</span></span>

<span data-ttu-id="11840-331">public LocalRunHelper([System.IO.TextWriter messageOutput = null])</span><span class="sxs-lookup"><span data-stu-id="11840-331">public LocalRunHelper([System.IO.TextWriter messageOutput = null])</span></span>

|<span data-ttu-id="11840-332">Параметр</span><span class="sxs-lookup"><span data-stu-id="11840-332">Parameter</span></span>|<span data-ttu-id="11840-333">Тип</span><span class="sxs-lookup"><span data-stu-id="11840-333">Type</span></span>|<span data-ttu-id="11840-334">Описание</span><span class="sxs-lookup"><span data-stu-id="11840-334">Description</span></span>|
|---------|----|-----------|
|<span data-ttu-id="11840-335">messageOutput</span><span class="sxs-lookup"><span data-stu-id="11840-335">messageOutput</span></span>|<span data-ttu-id="11840-336">System.IO.TextWriter</span><span class="sxs-lookup"><span data-stu-id="11840-336">System.IO.TextWriter</span></span>|<span data-ttu-id="11840-337">Для вывода сообщений задайте значение NULL, чтобы использовать консоль.</span><span class="sxs-lookup"><span data-stu-id="11840-337">for output messages, set to null to use Console</span></span>|

<span data-ttu-id="11840-338">**Свойства**</span><span class="sxs-lookup"><span data-stu-id="11840-338">**Properties**</span></span>

|<span data-ttu-id="11840-339">Свойство</span><span class="sxs-lookup"><span data-stu-id="11840-339">Property</span></span>|<span data-ttu-id="11840-340">Тип</span><span class="sxs-lookup"><span data-stu-id="11840-340">Type</span></span>|<span data-ttu-id="11840-341">Описание</span><span class="sxs-lookup"><span data-stu-id="11840-341">Description</span></span>|
|--------|----|-----------|
|<span data-ttu-id="11840-342">AlgebraPath</span><span class="sxs-lookup"><span data-stu-id="11840-342">AlgebraPath</span></span>|<span data-ttu-id="11840-343">строка</span><span class="sxs-lookup"><span data-stu-id="11840-343">string</span></span>|<span data-ttu-id="11840-344">Путь к файлу алгебры (он является одним из результатов компиляции).</span><span class="sxs-lookup"><span data-stu-id="11840-344">The path to algebra file (algebra file is one of the compilation results)</span></span>|
|<span data-ttu-id="11840-345">CodeBehindReferences</span><span class="sxs-lookup"><span data-stu-id="11840-345">CodeBehindReferences</span></span>|<span data-ttu-id="11840-346">строка</span><span class="sxs-lookup"><span data-stu-id="11840-346">string</span></span>|<span data-ttu-id="11840-347">Если сценарий содержит дополнительные ссылки на код программной части, укажите эти пути, разделенные точкой с запятой ";".</span><span class="sxs-lookup"><span data-stu-id="11840-347">If the script has additional code behind references, specify the paths separated with ';'</span></span>|
|<span data-ttu-id="11840-348">CppSdkDir</span><span class="sxs-lookup"><span data-stu-id="11840-348">CppSdkDir</span></span>|<span data-ttu-id="11840-349">строка</span><span class="sxs-lookup"><span data-stu-id="11840-349">string</span></span>|<span data-ttu-id="11840-350">Каталог пакета CppSDK.</span><span class="sxs-lookup"><span data-stu-id="11840-350">CppSDK directory</span></span>|
|<span data-ttu-id="11840-351">CurrentDir</span><span class="sxs-lookup"><span data-stu-id="11840-351">CurrentDir</span></span>|<span data-ttu-id="11840-352">строка</span><span class="sxs-lookup"><span data-stu-id="11840-352">string</span></span>|<span data-ttu-id="11840-353">Текущий каталог.</span><span class="sxs-lookup"><span data-stu-id="11840-353">Current directory</span></span>|
|<span data-ttu-id="11840-354">DataRoot</span><span class="sxs-lookup"><span data-stu-id="11840-354">DataRoot</span></span>|<span data-ttu-id="11840-355">string</span><span class="sxs-lookup"><span data-stu-id="11840-355">string</span></span>|<span data-ttu-id="11840-356">Путь к корневой папке данных.</span><span class="sxs-lookup"><span data-stu-id="11840-356">Data root path</span></span>|
|<span data-ttu-id="11840-357">DebuggerMailPath</span><span class="sxs-lookup"><span data-stu-id="11840-357">DebuggerMailPath</span></span>|<span data-ttu-id="11840-358">строка</span><span class="sxs-lookup"><span data-stu-id="11840-358">string</span></span>|<span data-ttu-id="11840-359">Путь к почтовому слоту отладчика.</span><span class="sxs-lookup"><span data-stu-id="11840-359">The path to debugger mailslot</span></span>|
|<span data-ttu-id="11840-360">GenerateUdoRedirect</span><span class="sxs-lookup"><span data-stu-id="11840-360">GenerateUdoRedirect</span></span>|<span data-ttu-id="11840-361">bool</span><span class="sxs-lookup"><span data-stu-id="11840-361">bool</span></span>|<span data-ttu-id="11840-362">Указывает, нужно ли создавать конфигурацию, переопределяющую пути перенаправления для загрузки сборки</span><span class="sxs-lookup"><span data-stu-id="11840-362">If we want to generate assembly loading redirection override config</span></span>|
|<span data-ttu-id="11840-363">HasCodeBehind</span><span class="sxs-lookup"><span data-stu-id="11840-363">HasCodeBehind</span></span>|<span data-ttu-id="11840-364">bool</span><span class="sxs-lookup"><span data-stu-id="11840-364">bool</span></span>|<span data-ttu-id="11840-365">Позволяет указать, содержит ли сценарий код программной части.</span><span class="sxs-lookup"><span data-stu-id="11840-365">If the script has code behind</span></span>|
|<span data-ttu-id="11840-366">InputDir</span><span class="sxs-lookup"><span data-stu-id="11840-366">InputDir</span></span>|<span data-ttu-id="11840-367">строка</span><span class="sxs-lookup"><span data-stu-id="11840-367">string</span></span>|<span data-ttu-id="11840-368">Каталог для входных данных.</span><span class="sxs-lookup"><span data-stu-id="11840-368">Directory for input data</span></span>|
|<span data-ttu-id="11840-369">MessagePath</span><span class="sxs-lookup"><span data-stu-id="11840-369">MessagePath</span></span>|<span data-ttu-id="11840-370">строка</span><span class="sxs-lookup"><span data-stu-id="11840-370">string</span></span>|<span data-ttu-id="11840-371">Путь к файлу дампа сообщений.</span><span class="sxs-lookup"><span data-stu-id="11840-371">Message dump file path</span></span>|
|<span data-ttu-id="11840-372">OutputDir</span><span class="sxs-lookup"><span data-stu-id="11840-372">OutputDir</span></span>|<span data-ttu-id="11840-373">строка</span><span class="sxs-lookup"><span data-stu-id="11840-373">string</span></span>|<span data-ttu-id="11840-374">Каталог для выходных данных.</span><span class="sxs-lookup"><span data-stu-id="11840-374">Directory for output data</span></span>|
|<span data-ttu-id="11840-375">Параллелизм</span><span class="sxs-lookup"><span data-stu-id="11840-375">Parallelism</span></span>|<span data-ttu-id="11840-376">int</span><span class="sxs-lookup"><span data-stu-id="11840-376">int</span></span>|<span data-ttu-id="11840-377">Значение параллелизма для вычислений алгебры.</span><span class="sxs-lookup"><span data-stu-id="11840-377">Parallelism to run the algebra</span></span>|
|<span data-ttu-id="11840-378">ParentPid</span><span class="sxs-lookup"><span data-stu-id="11840-378">ParentPid</span></span>|<span data-ttu-id="11840-379">int</span><span class="sxs-lookup"><span data-stu-id="11840-379">int</span></span>|<span data-ttu-id="11840-380">Идентификатор процесса родительского объекта, который отслеживает служба для выполнения выхода. Задайте значение 0 или отрицательное значение, чтобы этот параметр игнорировался.</span><span class="sxs-lookup"><span data-stu-id="11840-380">PID of the parent on which the service monitors to exit, set to 0 or negative to ignore</span></span>|
|<span data-ttu-id="11840-381">ResultPath</span><span class="sxs-lookup"><span data-stu-id="11840-381">ResultPath</span></span>|<span data-ttu-id="11840-382">строка</span><span class="sxs-lookup"><span data-stu-id="11840-382">string</span></span>|<span data-ttu-id="11840-383">Путь к файлу дампа результатов.</span><span class="sxs-lookup"><span data-stu-id="11840-383">Result dump file path</span></span>|
|<span data-ttu-id="11840-384">RuntimeDir</span><span class="sxs-lookup"><span data-stu-id="11840-384">RuntimeDir</span></span>|<span data-ttu-id="11840-385">строка</span><span class="sxs-lookup"><span data-stu-id="11840-385">string</span></span>|<span data-ttu-id="11840-386">Каталог среды выполнения.</span><span class="sxs-lookup"><span data-stu-id="11840-386">Runtime directory</span></span>|
|<span data-ttu-id="11840-387">ScriptPath</span><span class="sxs-lookup"><span data-stu-id="11840-387">ScriptPath</span></span>|<span data-ttu-id="11840-388">string</span><span class="sxs-lookup"><span data-stu-id="11840-388">string</span></span>|<span data-ttu-id="11840-389">Расположение сценария.</span><span class="sxs-lookup"><span data-stu-id="11840-389">Where to find the script</span></span>|
|<span data-ttu-id="11840-390">Shallow</span><span class="sxs-lookup"><span data-stu-id="11840-390">Shallow</span></span>|<span data-ttu-id="11840-391">bool</span><span class="sxs-lookup"><span data-stu-id="11840-391">bool</span></span>|<span data-ttu-id="11840-392">Позволяет задать выполнение неполной компиляции.</span><span class="sxs-lookup"><span data-stu-id="11840-392">Shallow compile or not</span></span>|
|<span data-ttu-id="11840-393">TempDir</span><span class="sxs-lookup"><span data-stu-id="11840-393">TempDir</span></span>|<span data-ttu-id="11840-394">строка</span><span class="sxs-lookup"><span data-stu-id="11840-394">string</span></span>|<span data-ttu-id="11840-395">Каталог временных данных</span><span class="sxs-lookup"><span data-stu-id="11840-395">Temp directory</span></span>|
|<span data-ttu-id="11840-396">UseDataBase</span><span class="sxs-lookup"><span data-stu-id="11840-396">UseDataBase</span></span>|<span data-ttu-id="11840-397">строка</span><span class="sxs-lookup"><span data-stu-id="11840-397">string</span></span>|<span data-ttu-id="11840-398">Укажите базу данных для регистрации временной сборки кода программной части. По умолчанию: база данных master.</span><span class="sxs-lookup"><span data-stu-id="11840-398">Specify the database to use for code behind temporary assembly registration, master by default</span></span>|
|<span data-ttu-id="11840-399">WorkDir</span><span class="sxs-lookup"><span data-stu-id="11840-399">WorkDir</span></span>|<span data-ttu-id="11840-400">строка</span><span class="sxs-lookup"><span data-stu-id="11840-400">string</span></span>|<span data-ttu-id="11840-401">Предпочитаемый рабочий каталог.</span><span class="sxs-lookup"><span data-stu-id="11840-401">Preferred working directory</span></span>|


<span data-ttu-id="11840-402">**Метод**</span><span class="sxs-lookup"><span data-stu-id="11840-402">**Method**</span></span>

|<span data-ttu-id="11840-403">Метод</span><span class="sxs-lookup"><span data-stu-id="11840-403">Method</span></span>|<span data-ttu-id="11840-404">Описание</span><span class="sxs-lookup"><span data-stu-id="11840-404">Description</span></span>|<span data-ttu-id="11840-405">Return</span><span class="sxs-lookup"><span data-stu-id="11840-405">Return</span></span>|<span data-ttu-id="11840-406">Параметр</span><span class="sxs-lookup"><span data-stu-id="11840-406">Parameter</span></span>|
|------|-----------|------|---------|
|<span data-ttu-id="11840-407">public bool DoCompile()</span><span class="sxs-lookup"><span data-stu-id="11840-407">public bool DoCompile()</span></span>|<span data-ttu-id="11840-408">Компиляция сценария U-SQL.</span><span class="sxs-lookup"><span data-stu-id="11840-408">Compile the U-SQL script</span></span>|<span data-ttu-id="11840-409">В случае успешного выполнения возвращает True.</span><span class="sxs-lookup"><span data-stu-id="11840-409">True on success</span></span>| |
|<span data-ttu-id="11840-410">public bool DoExec()</span><span class="sxs-lookup"><span data-stu-id="11840-410">public bool DoExec()</span></span>|<span data-ttu-id="11840-411">Выполнение скомпилированного результата.</span><span class="sxs-lookup"><span data-stu-id="11840-411">Execute the compiled result</span></span>|<span data-ttu-id="11840-412">В случае успешного выполнения возвращает True.</span><span class="sxs-lookup"><span data-stu-id="11840-412">True on success</span></span>| |
|<span data-ttu-id="11840-413">public bool DoRun()</span><span class="sxs-lookup"><span data-stu-id="11840-413">public bool DoRun()</span></span>|<span data-ttu-id="11840-414">Выполнение сценария U-SQL (компиляция и выполнение).</span><span class="sxs-lookup"><span data-stu-id="11840-414">Run the U-SQL script (Compile + Execute)</span></span>|<span data-ttu-id="11840-415">В случае успешного выполнения возвращает True.</span><span class="sxs-lookup"><span data-stu-id="11840-415">True on success</span></span>| |
|<span data-ttu-id="11840-416">public bool IsValidRuntimeDir(string path)</span><span class="sxs-lookup"><span data-stu-id="11840-416">public bool IsValidRuntimeDir(string path)</span></span>|<span data-ttu-id="11840-417">Проверяет, является ли заданный путь допустимым путем среды выполнения.</span><span class="sxs-lookup"><span data-stu-id="11840-417">Check if the given path is valid runtime path</span></span>|<span data-ttu-id="11840-418">Значение True, если путь допустимый.</span><span class="sxs-lookup"><span data-stu-id="11840-418">True for valid</span></span>|<span data-ttu-id="11840-419">Путь к каталогу среды выполнения.</span><span class="sxs-lookup"><span data-stu-id="11840-419">The path of runtime directory</span></span>|


## <a name="faq-about-common-issue"></a><span data-ttu-id="11840-420">Часто задаваемые вопросы о распространенных проблемах</span><span class="sxs-lookup"><span data-stu-id="11840-420">FAQ about common issue</span></span>

### <a name="error-1"></a><span data-ttu-id="11840-421">Ошибка 1</span><span class="sxs-lookup"><span data-stu-id="11840-421">Error 1:</span></span>
<span data-ttu-id="11840-422">E_CSC_SYSTEM_INTERNAL: Внутренняя ошибка!</span><span class="sxs-lookup"><span data-stu-id="11840-422">E_CSC_SYSTEM_INTERNAL: Internal error!</span></span> <span data-ttu-id="11840-423">Не удалось загрузить файл или сборку "ScopeEngineManaged.dll" либо одну из ее зависимостей.</span><span class="sxs-lookup"><span data-stu-id="11840-423">Could not load file or assembly 'ScopeEngineManaged.dll' or one of its dependencies.</span></span> <span data-ttu-id="11840-424">Не найден указанный модуль.</span><span class="sxs-lookup"><span data-stu-id="11840-424">The specified module could not be found.</span></span>

<span data-ttu-id="11840-425">Проверьте следующее:</span><span class="sxs-lookup"><span data-stu-id="11840-425">Please check the following:</span></span>

- <span data-ttu-id="11840-426">Убедитесь, что используется среда x64.</span><span class="sxs-lookup"><span data-stu-id="11840-426">Make sure you have x64 environment.</span></span> <span data-ttu-id="11840-427">Необходимо использовать целевую платформу сборки x64 и тестовую среду x64. Ознакомьтесь с разделом **Шаг 1. Создание проекта модульного теста C# и его настройка** выше.</span><span class="sxs-lookup"><span data-stu-id="11840-427">The build target platform and the test environment should be x64, refer to **Step 1: Create C# unit test project and configuration** above.</span></span>
- <span data-ttu-id="11840-428">Убедитесь, что все файлы зависимостей из NugetPackage\build\runtime были скопированы в рабочий каталог проекта.</span><span class="sxs-lookup"><span data-stu-id="11840-428">Make sure you have copied all dependency files under NugetPackage\build\runtime\ to project working directory.</span></span>


## <a name="next-steps"></a><span data-ttu-id="11840-429">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="11840-429">Next steps</span></span>

* <span data-ttu-id="11840-430">Для знакомства с U-SQL см. статью о [начале работы с языком U-SQL для Azure Data Lake Analytics](data-lake-analytics-u-sql-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="11840-430">To learn U-SQL, see [Get started with Azure Data Lake Analytics U-SQL language](data-lake-analytics-u-sql-get-started.md).</span></span>
* <span data-ttu-id="11840-431">Сведения о том, как записывать диагностические данные в журнал, см. в статье [Доступ к журналам диагностики для Azure Data Lake Analytics](data-lake-analytics-diagnostic-logs.md).</span><span class="sxs-lookup"><span data-stu-id="11840-431">To log diagnostics information, see [Accessing diagnostics logs for Azure Data Lake Analytics](data-lake-analytics-diagnostic-logs.md).</span></span>
* <span data-ttu-id="11840-432">Более сложный запрос см. в руководстве [Анализ журналов веб-сайта с помощью службы Azure Data Lake Analytics](data-lake-analytics-analyze-weblogs.md).</span><span class="sxs-lookup"><span data-stu-id="11840-432">To see a more complex query, see [Analyze website logs using Azure Data Lake Analytics](data-lake-analytics-analyze-weblogs.md).</span></span>
* <span data-ttu-id="11840-433">Для просмотра сведений о заданиях см. статью [Использование браузера и представления для заданий Azure Data Lake Analytics](data-lake-analytics-data-lake-tools-view-jobs.md).</span><span class="sxs-lookup"><span data-stu-id="11840-433">To view job details, see [Use Job Browser and Job View for Azure Data Lake Analytics jobs](data-lake-analytics-data-lake-tools-view-jobs.md).</span></span>
* <span data-ttu-id="11840-434">Дополнительные сведения см. в статье [Использование представления выполнения вершин в инструментах Data Lake для Visual Studio](data-lake-analytics-data-lake-tools-use-vertex-execution-view.md).</span><span class="sxs-lookup"><span data-stu-id="11840-434">To use the vertex execution view, see [Use the Vertex Execution View in Data Lake Tools for Visual Studio](data-lake-analytics-data-lake-tools-use-vertex-execution-view.md).</span></span>
