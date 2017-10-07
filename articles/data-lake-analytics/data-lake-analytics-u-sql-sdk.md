---
title: "локальный aaaScale U-SQL, запуск и тестирование с помощью пакета SDK U Озера данных Azure SQL | Документы Microsoft"
description: "Узнайте, как toouse SDK U Озера данных Azure SQL tooscale U-SQL заданий локальный запуск и тестирование с помощью командной строки и интерфейсы программирования на локальной рабочей станции."
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
ms.openlocfilehash: 2b0a16229789268e333f723ff6fc2c3efdc29905
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="scale-u-sql-local-run-and-test-with-azure-data-lake-u-sql-sdk"></a><span data-ttu-id="64e98-103">Масштабирование локального выполнения и тестирования сценариев U-SQL с помощью пакета SDK U-SQL для Azure Data Lake</span><span class="sxs-lookup"><span data-stu-id="64e98-103">Scale U-SQL local run and test with Azure Data Lake U-SQL SDK</span></span>

<span data-ttu-id="64e98-104">При разработке скрипт U-SQL, это общие toorun и локально скрипт теста U-SQL перед отправкой toocloud.</span><span class="sxs-lookup"><span data-stu-id="64e98-104">When developing U-SQL script, it is common toorun and test U-SQL script locally before submit it toocloud.</span></span> <span data-ttu-id="64e98-105">Для этого сценария Azure Data Lake предоставляет пакет Nuget, который называется пакетом SDK Azure Data Lake для U-SQL, с помощью которого можно легко масштабировать локальное выполнение и тестирование заданий U-SQL.</span><span class="sxs-lookup"><span data-stu-id="64e98-105">Azure Data Lake provides a Nuget package called Azure Data Lake U-SQL SDK for this scenario, through which you can easily scale U-SQL local run and test.</span></span> <span data-ttu-id="64e98-106">Это также возможно toointegrate U-SQL тестирование с помощью элемента конфигурации (непрерывной интеграции) системы tooautomate hello компиляции и тестирования.</span><span class="sxs-lookup"><span data-stu-id="64e98-106">It is also possible toointegrate this U-SQL test with CI (Continuous Integration) system tooautomate hello compile and test.</span></span>

<span data-ttu-id="64e98-107">Если вас интересует как toomanually локального запустить и отладить скрипт U-SQL с помощью средства графического пользовательского интерфейса средства Озера данных Azure для Visual Studio можно использовать для этого.</span><span class="sxs-lookup"><span data-stu-id="64e98-107">If you care about how toomanually local run and debug U-SQL script with GUI tooling, then you can use Azure Data Lake Tools for Visual Studio for that.</span></span> <span data-ttu-id="64e98-108">Дополнительные сведения см. [здесь](data-lake-analytics-data-lake-tools-local-run.md).</span><span class="sxs-lookup"><span data-stu-id="64e98-108">You can learn more from [here](data-lake-analytics-data-lake-tools-local-run.md).</span></span>

## <a name="install-azure-data-lake-u-sql-sdk"></a><span data-ttu-id="64e98-109">Установка пакета SDK Azure Data Lake для U-SQL</span><span class="sxs-lookup"><span data-stu-id="64e98-109">Install Azure Data Lake U-SQL SDK</span></span>

<span data-ttu-id="64e98-110">Вы можете получить hello SDK U Озера данных Azure SQL [здесь](https://www.nuget.org/packages/Microsoft.Azure.DataLake.USQL.SDK/) на Nuget.org. И перед его использованием необходимо toomake том, что зависимости следующим образом.</span><span class="sxs-lookup"><span data-stu-id="64e98-110">You can get hello Azure Data Lake U-SQL SDK [here](https://www.nuget.org/packages/Microsoft.Azure.DataLake.USQL.SDK/) on Nuget.org. And before using it, you need toomake sure you have dependencies as follows.</span></span>

### <a name="dependencies"></a><span data-ttu-id="64e98-111">Зависимости</span><span class="sxs-lookup"><span data-stu-id="64e98-111">Dependencies</span></span>

<span data-ttu-id="64e98-112">Hello SDK U Озера данных SQL требуется hello следующие зависимости:</span><span class="sxs-lookup"><span data-stu-id="64e98-112">hello Data Lake U-SQL SDK requires hello following dependencies:</span></span>

- <span data-ttu-id="64e98-113">[Microsoft .NET Framework 4.6 или более поздней версии](https://www.microsoft.com/download/details.aspx?id=17851).</span><span class="sxs-lookup"><span data-stu-id="64e98-113">[Microsoft .NET Framework 4.6 or newer](https://www.microsoft.com/download/details.aspx?id=17851).</span></span>
- <span data-ttu-id="64e98-114">Microsoft Visual C++ 14 и пакет SDK для Windows 10.0.10240.0 или более поздняя версия (в этой статье он называется пакетом CppSDK).</span><span class="sxs-lookup"><span data-stu-id="64e98-114">Microsoft Visual C++ 14 and Windows SDK 10.0.10240.0 or newer (which is called CppSDK in this article).</span></span> <span data-ttu-id="64e98-115">Существует два способа tooget CppSDK:</span><span class="sxs-lookup"><span data-stu-id="64e98-115">There are two ways tooget CppSDK:</span></span>

    - <span data-ttu-id="64e98-116">Установка выпуска [Visual Studio Community](https://developer.microsoft.com/downloads/vs-thankyou).</span><span class="sxs-lookup"><span data-stu-id="64e98-116">Install [Visual Studio Community Edition](https://developer.microsoft.com/downloads/vs-thankyou).</span></span> <span data-ttu-id="64e98-117">Вы получите \Windows Kits\10 папку в папке Program Files hello — например, C:\Program Files (x86) \Windows Kits\10\.</span><span class="sxs-lookup"><span data-stu-id="64e98-117">You'll have a \Windows Kits\10 folder under hello Program Files folder--for example, C:\Program Files (x86)\Windows Kits\10\.</span></span> <span data-ttu-id="64e98-118">Вы также найдете hello версию пакета SDK Windows 10 в \Windows Kits\10\Lib.</span><span class="sxs-lookup"><span data-stu-id="64e98-118">You'll also find hello Windows 10 SDK version under \Windows Kits\10\Lib.</span></span> <span data-ttu-id="64e98-119">Если вы не видите эти папки, переустановите Visual Studio и убедиться, что tooselect hello пакета SDK Windows 10 во время установки hello.</span><span class="sxs-lookup"><span data-stu-id="64e98-119">If you don’t see these folders, reinstall Visual Studio and be sure tooselect hello Windows 10 SDK during hello installation.</span></span> <span data-ttu-id="64e98-120">Если это устанавливается вместе с Visual Studio, hello U-SQL локального компилятор будет искать его автоматически.</span><span class="sxs-lookup"><span data-stu-id="64e98-120">If you have this installed with Visual Studio, hello U-SQL local compiler will find it automatically.</span></span>

    ![Пакет SDK Windows 10 для локального выполнения средств Data Lake для Visual Studio](./media/data-lake-analytics-data-lake-tools-local-run/data-lake-tools-for-visual-studio-local-run-windows-10-sdk.png)

    - <span data-ttu-id="64e98-122">Установка [средств Data Lake для Visual Studio](http://aka.ms/adltoolsvs).</span><span class="sxs-lookup"><span data-stu-id="64e98-122">Install [Data Lake Tools for Visual Studio](http://aka.ms/adltoolsvs).</span></span> <span data-ttu-id="64e98-123">Можно найти предварительно пакетированных hello файлов Visual C++ и пакет SDK для Windows в C:\Program Files (x86) \Microsoft Visual Studio 14.0\Common7\IDE\Extensions\Microsoft\ADL Tools\X.X.XXXX.X\CppSDK.</span><span class="sxs-lookup"><span data-stu-id="64e98-123">You can find hello prepackaged Visual C++ and Windows SDK files at C:\Program Files (x86)\Microsoft Visual Studio 14.0\Common7\IDE\Extensions\Microsoft\ADL Tools\X.X.XXXX.X\CppSDK.</span></span> <span data-ttu-id="64e98-124">В этом случае локальные компилятора hello U-SQL не удается найти зависимости hello автоматически.</span><span class="sxs-lookup"><span data-stu-id="64e98-124">In this case, hello U-SQL local compiler cannot find hello dependencies automatically.</span></span> <span data-ttu-id="64e98-125">Необходимо toospecify hello CppSDK путь для него.</span><span class="sxs-lookup"><span data-stu-id="64e98-125">You need toospecify hello CppSDK path for it.</span></span> <span data-ttu-id="64e98-126">Можно скопировать расположение tooanother hello файлы или использовать ее как есть.</span><span class="sxs-lookup"><span data-stu-id="64e98-126">You can either copy hello files tooanother location or use it as is.</span></span>

## <a name="understand-basic-concepts"></a><span data-ttu-id="64e98-127">Основные понятия</span><span class="sxs-lookup"><span data-stu-id="64e98-127">Understand basic concepts</span></span>

### <a name="data-root"></a><span data-ttu-id="64e98-128">Корневая папка данных</span><span class="sxs-lookup"><span data-stu-id="64e98-128">Data root</span></span>

<span data-ttu-id="64e98-129">Папка Hello корневой каталог данных является «локальное хранилище» для учетной записи локального вычислений hello.</span><span class="sxs-lookup"><span data-stu-id="64e98-129">hello data-root folder is a "local store" for hello local compute account.</span></span> <span data-ttu-id="64e98-130">Это учетная запись хранилища Озера данных Azure эквивалентные toohello учетной записи аналитики Озера данных.</span><span class="sxs-lookup"><span data-stu-id="64e98-130">It's equivalent toohello Azure Data Lake Store account of a Data Lake Analytics account.</span></span> <span data-ttu-id="64e98-131">Переключение tooa папку другой корневой каталог данных является так же, как переключения учетной записи tooa другое хранилище.</span><span class="sxs-lookup"><span data-stu-id="64e98-131">Switching tooa different data-root folder is just like switching tooa different store account.</span></span> <span data-ttu-id="64e98-132">Если вы хотите tooaccess часто общих данных с папками другой корневой каталог данных, необходимо использовать абсолютные пути в скриптах.</span><span class="sxs-lookup"><span data-stu-id="64e98-132">If you want tooaccess commonly shared data with different data-root folders, you must use absolute paths in your scripts.</span></span> <span data-ttu-id="64e98-133">Или Создание символических ссылок системных файлов (например, **mklink** в файловой системе NTFS) в папку toopoint hello корневой каталог данных toohello общих данных.</span><span class="sxs-lookup"><span data-stu-id="64e98-133">Or, create file system symbolic links (for example, **mklink** on NTFS) under hello data-root folder toopoint toohello shared data.</span></span>

<span data-ttu-id="64e98-134">Папка Hello корневой каталог данных используется для:</span><span class="sxs-lookup"><span data-stu-id="64e98-134">hello data-root folder is used to:</span></span>

- <span data-ttu-id="64e98-135">Хранение локальных метаданных, включая базы данных, таблицы, функции с табличным значением (TVF) и сборки.</span><span class="sxs-lookup"><span data-stu-id="64e98-135">Store local metadata, including databases, tables, table-valued functions (TVFs), and assemblies.</span></span>
- <span data-ttu-id="64e98-136">Поиск hello входного и выходного пути, которые определяются как относительные пути в U-SQL.</span><span class="sxs-lookup"><span data-stu-id="64e98-136">Look up hello input and output paths that are defined as relative paths in U-SQL.</span></span> <span data-ttu-id="64e98-137">Использование относительных путей делает проще toodeploy вашей tooAzure проекты U-SQL.</span><span class="sxs-lookup"><span data-stu-id="64e98-137">Using relative paths makes it easier toodeploy your U-SQL projects tooAzure.</span></span>

### <a name="file-path-in-u-sql"></a><span data-ttu-id="64e98-138">Путь к файлу в U-SQL</span><span class="sxs-lookup"><span data-stu-id="64e98-138">File path in U-SQL</span></span>

<span data-ttu-id="64e98-139">В скриптах U-SQL можно использовать как относительные, так и абсолютные локальные пути.</span><span class="sxs-lookup"><span data-stu-id="64e98-139">You can use both a relative path and a local absolute path in U-SQL scripts.</span></span> <span data-ttu-id="64e98-140">относительный путь Hello — toohello относительный путь к папке указанный корневой каталог данных.</span><span class="sxs-lookup"><span data-stu-id="64e98-140">hello relative path is relative toohello specified data-root folder path.</span></span> <span data-ttu-id="64e98-141">Рекомендуется, можно использовать «/» как hello toomake разделителя пути скрипты, совместимые со стороны сервера hello.</span><span class="sxs-lookup"><span data-stu-id="64e98-141">We recommend that you use "/" as hello path separator toomake your scripts compatible with hello server side.</span></span> <span data-ttu-id="64e98-142">Ниже приведены некоторые примеры относительных путей и их абсолютные эквиваленты.</span><span class="sxs-lookup"><span data-stu-id="64e98-142">Here are some examples of relative paths and their equivalent absolute paths.</span></span> <span data-ttu-id="64e98-143">В этих примерах C:\LocalRunDataRoot — папка hello корневой каталог данных.</span><span class="sxs-lookup"><span data-stu-id="64e98-143">In these examples, C:\LocalRunDataRoot is hello data-root folder.</span></span>

|<span data-ttu-id="64e98-144">Относительный путь</span><span class="sxs-lookup"><span data-stu-id="64e98-144">Relative path</span></span>|<span data-ttu-id="64e98-145">Абсолютный путь</span><span class="sxs-lookup"><span data-stu-id="64e98-145">Absolute path</span></span>|
|-------------|-------------|
|<span data-ttu-id="64e98-146">/abc/def/input.csv</span><span class="sxs-lookup"><span data-stu-id="64e98-146">/abc/def/input.csv</span></span> |<span data-ttu-id="64e98-147">C:\LocalRunDataRoot\abc\def\input.csv</span><span class="sxs-lookup"><span data-stu-id="64e98-147">C:\LocalRunDataRoot\abc\def\input.csv</span></span>|
|<span data-ttu-id="64e98-148">abc/def/input.csv</span><span class="sxs-lookup"><span data-stu-id="64e98-148">abc/def/input.csv</span></span>  |<span data-ttu-id="64e98-149">C:\LocalRunDataRoot\abc\def\input.csv</span><span class="sxs-lookup"><span data-stu-id="64e98-149">C:\LocalRunDataRoot\abc\def\input.csv</span></span>|
|<span data-ttu-id="64e98-150">D:/abc/def/input.csv</span><span class="sxs-lookup"><span data-stu-id="64e98-150">D:/abc/def/input.csv</span></span> |<span data-ttu-id="64e98-151">D:\abc\def\input.csv</span><span class="sxs-lookup"><span data-stu-id="64e98-151">D:\abc\def\input.csv</span></span>|

### <a name="working-directory"></a><span data-ttu-id="64e98-152">Рабочий каталог</span><span class="sxs-lookup"><span data-stu-id="64e98-152">Working directory</span></span>

<span data-ttu-id="64e98-153">При запуске сценария hello U-SQL локально, при компиляции в текущем каталоге выполнения создается рабочий каталог.</span><span class="sxs-lookup"><span data-stu-id="64e98-153">When running hello U-SQL script locally, a working directory is created during compilation under current running directory.</span></span> <span data-ttu-id="64e98-154">Кроме выводит toohello компиляции, hello необходимые файлы среды выполнения для локального выполнения будет тени скопированный toothis рабочий каталог.</span><span class="sxs-lookup"><span data-stu-id="64e98-154">In addition toohello compilation outputs, hello needed runtime files for local execution will be shadow copied toothis working directory.</span></span> <span data-ttu-id="64e98-155">Hello рабочей папки корневой каталог называется «ScopeWorkDir» и hello файлы в рабочий каталог hello, следующим образом:</span><span class="sxs-lookup"><span data-stu-id="64e98-155">hello working directory root folder is called "ScopeWorkDir" and hello files under hello working directory are as follows:</span></span>

|<span data-ttu-id="64e98-156">Каталог/файл</span><span class="sxs-lookup"><span data-stu-id="64e98-156">Directory/file</span></span>|<span data-ttu-id="64e98-157">Каталог/файл</span><span class="sxs-lookup"><span data-stu-id="64e98-157">Directory/file</span></span>|<span data-ttu-id="64e98-158">Каталог/файл</span><span class="sxs-lookup"><span data-stu-id="64e98-158">Directory/file</span></span>|<span data-ttu-id="64e98-159">Определение</span><span class="sxs-lookup"><span data-stu-id="64e98-159">Definition</span></span>|<span data-ttu-id="64e98-160">Описание</span><span class="sxs-lookup"><span data-stu-id="64e98-160">Description</span></span>|
|--------------|--------------|--------------|----------|-----------|
|<span data-ttu-id="64e98-161">C6A101DDCB470506</span><span class="sxs-lookup"><span data-stu-id="64e98-161">C6A101DDCB470506</span></span>| | |<span data-ttu-id="64e98-162">Хэш-строка версии среды выполнения</span><span class="sxs-lookup"><span data-stu-id="64e98-162">Hash string of runtime version</span></span>|<span data-ttu-id="64e98-163">Теневая копия файлов среды выполнения, необходимых для локального выполнения</span><span class="sxs-lookup"><span data-stu-id="64e98-163">Shadow copy of runtime files needed for local execution</span></span>|
| |<span data-ttu-id="64e98-164">Script_66AE4909AA0ED06C</span><span class="sxs-lookup"><span data-stu-id="64e98-164">Script_66AE4909AA0ED06C</span></span>| |<span data-ttu-id="64e98-165">Имя скрипта и хэш-строка пути к скрипту</span><span class="sxs-lookup"><span data-stu-id="64e98-165">Script name + hash string of script path</span></span>|<span data-ttu-id="64e98-166">Выходные данные компиляции и ведение журнала шагов выполнения</span><span class="sxs-lookup"><span data-stu-id="64e98-166">Compilation outputs and execution step logging</span></span>|
| | |<span data-ttu-id="64e98-167">\_script\_.abr</span><span class="sxs-lookup"><span data-stu-id="64e98-167">\_script\_.abr</span></span>|<span data-ttu-id="64e98-168">Выходные данные компилятора</span><span class="sxs-lookup"><span data-stu-id="64e98-168">Compiler output</span></span>|<span data-ttu-id="64e98-169">Файл Algebra</span><span class="sxs-lookup"><span data-stu-id="64e98-169">Algebra file</span></span>|
| | |<span data-ttu-id="64e98-170">\_ScopeCodeGen\_.*</span><span class="sxs-lookup"><span data-stu-id="64e98-170">\_ScopeCodeGen\_.*</span></span>|<span data-ttu-id="64e98-171">Выходные данные компилятора</span><span class="sxs-lookup"><span data-stu-id="64e98-171">Compiler output</span></span>|<span data-ttu-id="64e98-172">Созданный управляемый код</span><span class="sxs-lookup"><span data-stu-id="64e98-172">Generated managed code</span></span>|
| | |<span data-ttu-id="64e98-173">\_ScopeCodeGenEngine\_.*</span><span class="sxs-lookup"><span data-stu-id="64e98-173">\_ScopeCodeGenEngine\_.*</span></span>|<span data-ttu-id="64e98-174">Выходные данные компилятора</span><span class="sxs-lookup"><span data-stu-id="64e98-174">Compiler output</span></span>|<span data-ttu-id="64e98-175">Созданный собственный код</span><span class="sxs-lookup"><span data-stu-id="64e98-175">Generated native code</span></span>|
| | |<span data-ttu-id="64e98-176">referenced assemblies</span><span class="sxs-lookup"><span data-stu-id="64e98-176">referenced assemblies</span></span>|<span data-ttu-id="64e98-177">Ссылка на сборку</span><span class="sxs-lookup"><span data-stu-id="64e98-177">Assembly reference</span></span>|<span data-ttu-id="64e98-178">Связанные файлы сборок.</span><span class="sxs-lookup"><span data-stu-id="64e98-178">Referenced assembly files</span></span>|
| | |<span data-ttu-id="64e98-179">deployed_resources</span><span class="sxs-lookup"><span data-stu-id="64e98-179">deployed_resources</span></span>|<span data-ttu-id="64e98-180">Развертывание ресурсов</span><span class="sxs-lookup"><span data-stu-id="64e98-180">Resource deployment</span></span>|<span data-ttu-id="64e98-181">Файлы развертывания ресурсов</span><span class="sxs-lookup"><span data-stu-id="64e98-181">Resource deployment files</span></span>|
| | |<span data-ttu-id="64e98-182">xxxxxxxx.xxx[1..n]\_\*.*</span><span class="sxs-lookup"><span data-stu-id="64e98-182">xxxxxxxx.xxx[1..n]\_\*.*</span></span>|<span data-ttu-id="64e98-183">Журнал выполнения</span><span class="sxs-lookup"><span data-stu-id="64e98-183">Execution log</span></span>|<span data-ttu-id="64e98-184">Журнал шагов выполнения</span><span class="sxs-lookup"><span data-stu-id="64e98-184">Log of execution steps</span></span>|


## <a name="use-hello-sdk-from-hello-command-line"></a><span data-ttu-id="64e98-185">Использовать hello SDK из командной строки hello</span><span class="sxs-lookup"><span data-stu-id="64e98-185">Use hello SDK from hello command line</span></span>

### <a name="command-line-interface-of-hello-helper-application"></a><span data-ttu-id="64e98-186">Интерфейс командной строки вспомогательное приложение hello</span><span class="sxs-lookup"><span data-stu-id="64e98-186">Command-line interface of hello helper application</span></span>

<span data-ttu-id="64e98-187">В разделе SDK directory\build\runtime LocalRunHelper.exe — hello командной строки приложение, которое предоставляет интерфейсы toomost часто используемые hello локального выполнения функции.</span><span class="sxs-lookup"><span data-stu-id="64e98-187">Under SDK directory\build\runtime, LocalRunHelper.exe is hello command-line helper application that provides interfaces toomost of hello commonly used local-run functions.</span></span> <span data-ttu-id="64e98-188">Обратите внимание, что оба hello команда hello параметры зависят от регистра.</span><span class="sxs-lookup"><span data-stu-id="64e98-188">Note that both hello command and hello argument switches are case-sensitive.</span></span> <span data-ttu-id="64e98-189">tooinvoke его:</span><span class="sxs-lookup"><span data-stu-id="64e98-189">tooinvoke it:</span></span>

    LocalRunHelper.exe <command> <Required-Command-Arguments> [Optional-Command-Arguments]

<span data-ttu-id="64e98-190">Запустите LocalRunHelper.exe без аргументов или с hello **справки** переключения tooshow hello справочной информации:</span><span class="sxs-lookup"><span data-stu-id="64e98-190">Run LocalRunHelper.exe without arguments or with hello **help** switch tooshow hello help information:</span></span>

    > LocalRunHelper.exe help

        Command 'help' :  Show usage information
        Command 'compile' :  Compile hello script
        Required Arguments :
            -Script param
                    Script File Path
        Optional Arguments :
            -Shallow [default value 'False']
                    Shallow compile

<span data-ttu-id="64e98-191">В hello справочная информация:</span><span class="sxs-lookup"><span data-stu-id="64e98-191">In hello help information:</span></span>

-  <span data-ttu-id="64e98-192">**Команда** дает hello имя команды.</span><span class="sxs-lookup"><span data-stu-id="64e98-192">**Command** gives hello command’s name.</span></span>  
-  <span data-ttu-id="64e98-193">**Required Argument** перечисляет обязательные аргументы.</span><span class="sxs-lookup"><span data-stu-id="64e98-193">**Required Argument** lists arguments that must be supplied.</span></span>  
-  <span data-ttu-id="64e98-194">**Optional Argument** перечисляет необязательные аргументы и приводит для них значения по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="64e98-194">**Optional Argument** lists arguments that are optional, with default values.</span></span>  <span data-ttu-id="64e98-195">Необязательные аргументы логическое не принимают параметры, и их отображение указывать tootheir отрицательное значение по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="64e98-195">Optional Boolean arguments don’t have parameters, and their appearances mean negative tootheir default value.</span></span>

### <a name="return-value-and-logging"></a><span data-ttu-id="64e98-196">Возвращаемое значение и ведение журнала</span><span class="sxs-lookup"><span data-stu-id="64e98-196">Return value and logging</span></span>

<span data-ttu-id="64e98-197">Возвращает вспомогательное приложение Hello **0** успеха и **-1** сбоя.</span><span class="sxs-lookup"><span data-stu-id="64e98-197">hello helper application returns **0** for success and **-1** for failure.</span></span> <span data-ttu-id="64e98-198">По умолчанию hello вспомогательный отправляет все сообщения toohello текущей консоли.</span><span class="sxs-lookup"><span data-stu-id="64e98-198">By default, hello helper sends all messages toohello current console.</span></span> <span data-ttu-id="64e98-199">Однако большинство команд hello поддерживают hello **path_to_log_file - MessageOut** дополнительный аргумент, который перенаправляет hello выводит tooa файла журнала.</span><span class="sxs-lookup"><span data-stu-id="64e98-199">However, most of hello commands support hello **-MessageOut path_to_log_file** optional argument that redirects hello outputs tooa log file.</span></span>

### <a name="environment-variable-configuring"></a><span data-ttu-id="64e98-200">Настройка переменной среды</span><span class="sxs-lookup"><span data-stu-id="64e98-200">Environment variable configuring</span></span>

<span data-ttu-id="64e98-201">Для локального выполнения U-SQL требуется указать корневую папку данных в качестве локальной учетной записи хранения, а также указать путь к пакету CppSDK для зависимостей.</span><span class="sxs-lookup"><span data-stu-id="64e98-201">U-SQL local run needs a specified data root as local storage account, as well as a specified CppSDK path for dependencies.</span></span> <span data-ttu-id="64e98-202">Вы можете оба аргумента набора hello в переменной среды командной строки, и для них.</span><span class="sxs-lookup"><span data-stu-id="64e98-202">You can both set hello argument in command-line or set environment variable for them.</span></span>

- <span data-ttu-id="64e98-203">Набор hello **SCOPE_CPP_SDK** переменной среды.</span><span class="sxs-lookup"><span data-stu-id="64e98-203">Set hello **SCOPE_CPP_SDK** environment variable.</span></span>

    <span data-ttu-id="64e98-204">Если Microsoft Visual C++ и пакет SDK для Windows hello, установив Озера Data Tools для Visual Studio, следует проверьте hello следующие папки:</span><span class="sxs-lookup"><span data-stu-id="64e98-204">If you get Microsoft Visual C++ and hello Windows SDK by installing Data Lake Tools for Visual Studio, verify that you have hello following folder:</span></span>

        C:\Program Files (x86)\Microsoft Visual Studio 14.0\Common7\IDE\Extensions\Microsoft\Microsoft Azure Data Lake Tools for Visual Studio 2015\X.X.XXXX.X\CppSDK

    <span data-ttu-id="64e98-205">Определите новую переменную среды с именем **SCOPE_CPP_SDK** toopoint toothis каталога.</span><span class="sxs-lookup"><span data-stu-id="64e98-205">Define a new environment variable called **SCOPE_CPP_SDK** toopoint toothis directory.</span></span> <span data-ttu-id="64e98-206">Или скопируйте папку toohello hello другое местоположение и указать **SCOPE_CPP_SDK** , что.</span><span class="sxs-lookup"><span data-stu-id="64e98-206">Or copy hello folder toohello other location and specify **SCOPE_CPP_SDK** as that.</span></span>

    <span data-ttu-id="64e98-207">В переменной среды hello toosetting сложения, можно указать hello **- CppSDK** аргумента при использовании hello командной строки.</span><span class="sxs-lookup"><span data-stu-id="64e98-207">In addition toosetting hello environment variable, you can specify hello **-CppSDK** argument when you're using hello command line.</span></span> <span data-ttu-id="64e98-208">Этот аргумент переопределяет используемую по умолчанию переменную среды CppSDK.</span><span class="sxs-lookup"><span data-stu-id="64e98-208">This argument overwrites your default CppSDK environment variable.</span></span>

- <span data-ttu-id="64e98-209">Набор hello **LOCALRUN_DATAROOT** переменной среды.</span><span class="sxs-lookup"><span data-stu-id="64e98-209">Set hello **LOCALRUN_DATAROOT** environment variable.</span></span>

    <span data-ttu-id="64e98-210">Определите новую переменную среды с именем **LOCALRUN_DATAROOT** , указывающий корневой каталог данных toohello.</span><span class="sxs-lookup"><span data-stu-id="64e98-210">Define a new environment variable called **LOCALRUN_DATAROOT** that points toohello data root.</span></span>

    <span data-ttu-id="64e98-211">В переменной среды hello toosetting сложения, можно указать hello **- DataRoot** аргумент с hello путь от корня данных при работе с командной строки.</span><span class="sxs-lookup"><span data-stu-id="64e98-211">In addition toosetting hello environment variable, you can specify hello **-DataRoot** argument with hello data-root path when you're using a command line.</span></span> <span data-ttu-id="64e98-212">Этот аргумент переопределяет используемую по умолчанию переменную среды, задающую путь к корневой папке данных.</span><span class="sxs-lookup"><span data-stu-id="64e98-212">This argument overwrites your default data-root environment variable.</span></span> <span data-ttu-id="64e98-213">Необходимо tooadd этот аргумент командной строки tooevery которого был осуществлен запуск, чтобы переменная среды корневой каталог данных по умолчанию hello для всех операций, можно перезаписать.</span><span class="sxs-lookup"><span data-stu-id="64e98-213">You need tooadd this argument tooevery command line you're running so that you can overwrite hello default data-root environment variable for all operations.</span></span>

### <a name="sdk-command-line-usage-samples"></a><span data-ttu-id="64e98-214">Примеры использования командной строки пакета SDK</span><span class="sxs-lookup"><span data-stu-id="64e98-214">SDK command line usage samples</span></span>

#### <a name="compile-and-run"></a><span data-ttu-id="64e98-215">Компиляция и запуск</span><span class="sxs-lookup"><span data-stu-id="64e98-215">Compile and run</span></span>

<span data-ttu-id="64e98-216">Hello **запуска** используется команда toocompile hello сценария, а затем выполните скомпилированных результаты.</span><span class="sxs-lookup"><span data-stu-id="64e98-216">hello **run** command is used toocompile hello script and then execute compiled results.</span></span> <span data-ttu-id="64e98-217">Эта команда принимает все аргументы командной строки, которые доступны для команд **compile** и **execute**.</span><span class="sxs-lookup"><span data-stu-id="64e98-217">Its command-line arguments are a combination of those from **compile** and **execute**.</span></span>

    LocalRunHelper run -Script path_to_usql_script.usql [optional_arguments]

<span data-ttu-id="64e98-218">Hello ниже приведены необязательные аргументы для **запуска**:</span><span class="sxs-lookup"><span data-stu-id="64e98-218">hello following are optional arguments for **run**:</span></span>


|<span data-ttu-id="64e98-219">Аргумент</span><span class="sxs-lookup"><span data-stu-id="64e98-219">Argument</span></span>|<span data-ttu-id="64e98-220">Значение по умолчанию</span><span class="sxs-lookup"><span data-stu-id="64e98-220">Default value</span></span>|<span data-ttu-id="64e98-221">Описание</span><span class="sxs-lookup"><span data-stu-id="64e98-221">Description</span></span>|
|--------|-------------|-----------|
|<span data-ttu-id="64e98-222">-CodeBehind</span><span class="sxs-lookup"><span data-stu-id="64e98-222">-CodeBehind</span></span>|<span data-ttu-id="64e98-223">Ложь</span><span class="sxs-lookup"><span data-stu-id="64e98-223">False</span></span>|<span data-ttu-id="64e98-224">сценарий Hello имеет .cs кода программной части</span><span class="sxs-lookup"><span data-stu-id="64e98-224">hello script has .cs code behind</span></span>|
|<span data-ttu-id="64e98-225">-CppSDK</span><span class="sxs-lookup"><span data-stu-id="64e98-225">-CppSDK</span></span>| |<span data-ttu-id="64e98-226">Каталог CppSDK.</span><span class="sxs-lookup"><span data-stu-id="64e98-226">CppSDK Directory</span></span>|
|<span data-ttu-id="64e98-227">-DataRoot</span><span class="sxs-lookup"><span data-stu-id="64e98-227">-DataRoot</span></span>| <span data-ttu-id="64e98-228">Переменная среды DataRoot</span><span class="sxs-lookup"><span data-stu-id="64e98-228">DataRoot environment variable</span></span>|<span data-ttu-id="64e98-229">Слишком DataRoot для локального запуска по умолчанию переменная среды «LOCALRUN_DATAROOT»</span><span class="sxs-lookup"><span data-stu-id="64e98-229">DataRoot for local run, default too'LOCALRUN_DATAROOT' environment variable</span></span>|
|<span data-ttu-id="64e98-230">-MessageOut</span><span class="sxs-lookup"><span data-stu-id="64e98-230">-MessageOut</span></span>| |<span data-ttu-id="64e98-231">Сообщения на консоль tooa файла дампа</span><span class="sxs-lookup"><span data-stu-id="64e98-231">Dump messages on console tooa file</span></span>|
|<span data-ttu-id="64e98-232">-Parallel</span><span class="sxs-lookup"><span data-stu-id="64e98-232">-Parallel</span></span>|<span data-ttu-id="64e98-233">1</span><span class="sxs-lookup"><span data-stu-id="64e98-233">1</span></span>|<span data-ttu-id="64e98-234">Запустите hello план с hello указан параллелизма</span><span class="sxs-lookup"><span data-stu-id="64e98-234">Run hello plan with hello specified parallelism</span></span>|
|<span data-ttu-id="64e98-235">-References</span><span class="sxs-lookup"><span data-stu-id="64e98-235">-References</span></span>| |<span data-ttu-id="64e98-236">Список путей tooextra ссылочных сборок или файлов данных кода программной части, разделенных «;»</span><span class="sxs-lookup"><span data-stu-id="64e98-236">List of paths tooextra reference assemblies or data files of code behind, separated by ';'</span></span>|
|<span data-ttu-id="64e98-237">-UdoRedirect</span><span class="sxs-lookup"><span data-stu-id="64e98-237">-UdoRedirect</span></span>|<span data-ttu-id="64e98-238">Ложь</span><span class="sxs-lookup"><span data-stu-id="64e98-238">False</span></span>|<span data-ttu-id="64e98-239">Создание конфигурации перенаправления сборки Udo.</span><span class="sxs-lookup"><span data-stu-id="64e98-239">Generate Udo assembly redirect config</span></span>|
|<span data-ttu-id="64e98-240">-UseDatabase</span><span class="sxs-lookup"><span data-stu-id="64e98-240">-UseDatabase</span></span>|<span data-ttu-id="64e98-241">master</span><span class="sxs-lookup"><span data-stu-id="64e98-241">master</span></span>|<span data-ttu-id="64e98-242">Toouse базы данных для кода за пределами временную сборку регистрации</span><span class="sxs-lookup"><span data-stu-id="64e98-242">Database toouse for code behind temporary assembly registration</span></span>|
|<span data-ttu-id="64e98-243">-Verbose</span><span class="sxs-lookup"><span data-stu-id="64e98-243">-Verbose</span></span>|<span data-ttu-id="64e98-244">Ложь</span><span class="sxs-lookup"><span data-stu-id="64e98-244">False</span></span>|<span data-ttu-id="64e98-245">Отображение подробных выходных данных среды выполнения.</span><span class="sxs-lookup"><span data-stu-id="64e98-245">Show detailed outputs from runtime</span></span>|
|<span data-ttu-id="64e98-246">-WorkDir</span><span class="sxs-lookup"><span data-stu-id="64e98-246">-WorkDir</span></span>|<span data-ttu-id="64e98-247">Текущий каталог</span><span class="sxs-lookup"><span data-stu-id="64e98-247">Current Directory</span></span>|<span data-ttu-id="64e98-248">Задает каталог для работы и выходных данных компилятора.</span><span class="sxs-lookup"><span data-stu-id="64e98-248">Directory for compiler usage and outputs</span></span>|
|<span data-ttu-id="64e98-249">-RunScopeCEP</span><span class="sxs-lookup"><span data-stu-id="64e98-249">-RunScopeCEP</span></span>|<span data-ttu-id="64e98-250">0</span><span class="sxs-lookup"><span data-stu-id="64e98-250">0</span></span>|<span data-ttu-id="64e98-251">Режим toouse ScopeCEP</span><span class="sxs-lookup"><span data-stu-id="64e98-251">ScopeCEP mode toouse</span></span>|
|<span data-ttu-id="64e98-252">-ScopeCEPTempPath</span><span class="sxs-lookup"><span data-stu-id="64e98-252">-ScopeCEPTempPath</span></span>|<span data-ttu-id="64e98-253">temp</span><span class="sxs-lookup"><span data-stu-id="64e98-253">temp</span></span>|<span data-ttu-id="64e98-254">Путь к временной toouse для потоковой передачи данных</span><span class="sxs-lookup"><span data-stu-id="64e98-254">Temp path toouse for streaming data</span></span>|
|<span data-ttu-id="64e98-255">-OptFlags</span><span class="sxs-lookup"><span data-stu-id="64e98-255">-OptFlags</span></span>| |<span data-ttu-id="64e98-256">Разделенный запятыми список флагов оптимизатора.</span><span class="sxs-lookup"><span data-stu-id="64e98-256">Comma-separated list of optimizer flags</span></span>|


<span data-ttu-id="64e98-257">Ниже приведен пример:</span><span class="sxs-lookup"><span data-stu-id="64e98-257">Here's an example:</span></span>

    LocalRunHelper run -Script d:\test\test1.usql -WorkDir d:\test\bin -CodeBehind -References "d:\asm\ref1.dll;d:\asm\ref2.dll" -UseDatabase testDB –Parallel 5 -Verbose

<span data-ttu-id="64e98-258">Помимо объединения **компиляции** и **выполнение**, можно компилировать и выполнять отдельно hello скомпилированных исполняемых файлов.</span><span class="sxs-lookup"><span data-stu-id="64e98-258">Besides combining **compile** and **execute**, you can compile and execute hello compiled executables separately.</span></span>

#### <a name="compile-a-u-sql-script"></a><span data-ttu-id="64e98-259">Компиляция скрипта U-SQL</span><span class="sxs-lookup"><span data-stu-id="64e98-259">Compile a U-SQL script</span></span>

<span data-ttu-id="64e98-260">Hello **компиляции** команда является tooexecutables сценария используется toocompile U-SQL.</span><span class="sxs-lookup"><span data-stu-id="64e98-260">hello **compile** command is used toocompile a U-SQL script tooexecutables.</span></span>

    LocalRunHelper compile -Script path_to_usql_script.usql [optional_arguments]

<span data-ttu-id="64e98-261">Hello ниже приведены необязательные аргументы для **компиляции**:</span><span class="sxs-lookup"><span data-stu-id="64e98-261">hello following are optional arguments for **compile**:</span></span>


|<span data-ttu-id="64e98-262">Аргумент</span><span class="sxs-lookup"><span data-stu-id="64e98-262">Argument</span></span>|<span data-ttu-id="64e98-263">Описание</span><span class="sxs-lookup"><span data-stu-id="64e98-263">Description</span></span>|
|--------|-----------|
| <span data-ttu-id="64e98-264">-CodeBehind [значение по умолчанию False]</span><span class="sxs-lookup"><span data-stu-id="64e98-264">-CodeBehind [default value 'False']</span></span>|<span data-ttu-id="64e98-265">сценарий Hello имеет .cs кода программной части</span><span class="sxs-lookup"><span data-stu-id="64e98-265">hello script has .cs code behind</span></span>|
| <span data-ttu-id="64e98-266">-CppSDK [значение по умолчанию "]</span><span class="sxs-lookup"><span data-stu-id="64e98-266">-CppSDK [default value '']</span></span>|<span data-ttu-id="64e98-267">Каталог CppSDK.</span><span class="sxs-lookup"><span data-stu-id="64e98-267">CppSDK Directory</span></span>|
| <span data-ttu-id="64e98-268">-DataRoot [значение по умолчанию: переменная среды DataRoot]</span><span class="sxs-lookup"><span data-stu-id="64e98-268">-DataRoot [default value 'DataRoot environment variable']</span></span>|<span data-ttu-id="64e98-269">Слишком DataRoot для локального запуска по умолчанию переменная среды «LOCALRUN_DATAROOT»</span><span class="sxs-lookup"><span data-stu-id="64e98-269">DataRoot for local run, default too'LOCALRUN_DATAROOT' environment variable</span></span>|
| <span data-ttu-id="64e98-270">-MessageOut [значение по умолчанию "]</span><span class="sxs-lookup"><span data-stu-id="64e98-270">-MessageOut [default value '']</span></span>|<span data-ttu-id="64e98-271">Сообщения на консоль tooa файла дампа</span><span class="sxs-lookup"><span data-stu-id="64e98-271">Dump messages on console tooa file</span></span>|
| <span data-ttu-id="64e98-272">-References [значение по умолчанию "]</span><span class="sxs-lookup"><span data-stu-id="64e98-272">-References [default value '']</span></span>|<span data-ttu-id="64e98-273">Список путей tooextra ссылочных сборок или файлов данных кода программной части, разделенных «;»</span><span class="sxs-lookup"><span data-stu-id="64e98-273">List of paths tooextra reference assemblies or data files of code behind, separated by ';'</span></span>|
| <span data-ttu-id="64e98-274">-Shallow [значение по умолчанию False]</span><span class="sxs-lookup"><span data-stu-id="64e98-274">-Shallow [default value 'False']</span></span>|<span data-ttu-id="64e98-275">Неполная компиляция.</span><span class="sxs-lookup"><span data-stu-id="64e98-275">Shallow compile</span></span>|
| <span data-ttu-id="64e98-276">-UdoRedirect [значение по умолчанию False]</span><span class="sxs-lookup"><span data-stu-id="64e98-276">-UdoRedirect [default value 'False']</span></span>|<span data-ttu-id="64e98-277">Создание конфигурации перенаправления сборки Udo.</span><span class="sxs-lookup"><span data-stu-id="64e98-277">Generate Udo assembly redirect config</span></span>|
| <span data-ttu-id="64e98-278">-UseDatabase [значение по умолчанию master]</span><span class="sxs-lookup"><span data-stu-id="64e98-278">-UseDatabase [default value 'master']</span></span>|<span data-ttu-id="64e98-279">Toouse базы данных для кода за пределами временную сборку регистрации</span><span class="sxs-lookup"><span data-stu-id="64e98-279">Database toouse for code behind temporary assembly registration</span></span>|
| <span data-ttu-id="64e98-280">-WorkDir [значение по умолчанию: текущий каталог]</span><span class="sxs-lookup"><span data-stu-id="64e98-280">-WorkDir [default value 'Current Directory']</span></span>|<span data-ttu-id="64e98-281">Задает каталог для работы и выходных данных компилятора.</span><span class="sxs-lookup"><span data-stu-id="64e98-281">Directory for compiler usage and outputs</span></span>|
| <span data-ttu-id="64e98-282">-RunScopeCEP [значение по умолчанию: "0"]</span><span class="sxs-lookup"><span data-stu-id="64e98-282">-RunScopeCEP [default value '0']</span></span>|<span data-ttu-id="64e98-283">Режим toouse ScopeCEP</span><span class="sxs-lookup"><span data-stu-id="64e98-283">ScopeCEP mode toouse</span></span>|
| <span data-ttu-id="64e98-284">-ScopeCEPTempPath [значение по умолчанию: "temp"]</span><span class="sxs-lookup"><span data-stu-id="64e98-284">-ScopeCEPTempPath [default value 'temp']</span></span>|<span data-ttu-id="64e98-285">Путь к временной toouse для потоковой передачи данных</span><span class="sxs-lookup"><span data-stu-id="64e98-285">Temp path toouse for streaming data</span></span>|
| <span data-ttu-id="64e98-286">-OptFlags [значение по умолчанию: "]</span><span class="sxs-lookup"><span data-stu-id="64e98-286">-OptFlags [default value '']</span></span>|<span data-ttu-id="64e98-287">Разделенный запятыми список флагов оптимизатора.</span><span class="sxs-lookup"><span data-stu-id="64e98-287">Comma-separated list of optimizer flags</span></span>|


<span data-ttu-id="64e98-288">Вот несколько примеров использования команды.</span><span class="sxs-lookup"><span data-stu-id="64e98-288">Here are some usage examples.</span></span>

<span data-ttu-id="64e98-289">Компиляция скрипта U-SQL:</span><span class="sxs-lookup"><span data-stu-id="64e98-289">Compile a U-SQL script:</span></span>

    LocalRunHelper compile -Script d:\test\test1.usql

<span data-ttu-id="64e98-290">Скомпилируйте скрипт U-SQL и назначение папки hello корневой каталог данных.</span><span class="sxs-lookup"><span data-stu-id="64e98-290">Compile a U-SQL script and set hello data-root folder.</span></span> <span data-ttu-id="64e98-291">Обратите внимание, что это перезапишет hello задать переменную среды.</span><span class="sxs-lookup"><span data-stu-id="64e98-291">Note that this will overwrite hello set environment variable.</span></span>

    LocalRunHelper compile -Script d:\test\test1.usql –DataRoot c:\DataRoot

<span data-ttu-id="64e98-292">Компиляция скрипта U-SQL с определенным рабочим каталогом и ссылками на сборку и базу данных:</span><span class="sxs-lookup"><span data-stu-id="64e98-292">Compile a U-SQL script and set a working directory, reference assembly, and database:</span></span>

    LocalRunHelper compile -Script d:\test\test1.usql -WorkDir d:\test\bin -References "d:\asm\ref1.dll;d:\asm\ref2.dll" -UseDatabase testDB

#### <a name="execute-compiled-results"></a><span data-ttu-id="64e98-293">Выполнение скомпилированного результата</span><span class="sxs-lookup"><span data-stu-id="64e98-293">Execute compiled results</span></span>

<span data-ttu-id="64e98-294">Hello **выполнение** команда является результатов используется tooexecute компиляции.</span><span class="sxs-lookup"><span data-stu-id="64e98-294">hello **execute** command is used tooexecute compiled results.</span></span>   

    LocalRunHelper execute -Algebra path_to_compiled_algebra_file [optional_arguments]

<span data-ttu-id="64e98-295">Hello ниже приведены необязательные аргументы для **выполнение**:</span><span class="sxs-lookup"><span data-stu-id="64e98-295">hello following are optional arguments for **execute**:</span></span>

|<span data-ttu-id="64e98-296">Аргумент</span><span class="sxs-lookup"><span data-stu-id="64e98-296">Argument</span></span>|<span data-ttu-id="64e98-297">Описание</span><span class="sxs-lookup"><span data-stu-id="64e98-297">Description</span></span>|
|--------|-----------|
|<span data-ttu-id="64e98-298">-DataRoot [значение по умолчанию "]</span><span class="sxs-lookup"><span data-stu-id="64e98-298">-DataRoot [default value '']</span></span>|<span data-ttu-id="64e98-299">Корневая папка для обработки метаданных.</span><span class="sxs-lookup"><span data-stu-id="64e98-299">Data root for metadata execution.</span></span> <span data-ttu-id="64e98-300">По умолчанию используется toohello **LOCALRUN_DATAROOT** переменной среды.</span><span class="sxs-lookup"><span data-stu-id="64e98-300">It defaults toohello **LOCALRUN_DATAROOT** environment variable.</span></span>|
|<span data-ttu-id="64e98-301">-MessageOut [значение по умолчанию "]</span><span class="sxs-lookup"><span data-stu-id="64e98-301">-MessageOut [default value '']</span></span>|<span data-ttu-id="64e98-302">Выведите сообщения в файл tooa hello консоли.</span><span class="sxs-lookup"><span data-stu-id="64e98-302">Dump messages on hello console tooa file.</span></span>|
|<span data-ttu-id="64e98-303">-Parallel [значение по умолчанию 1]</span><span class="sxs-lookup"><span data-stu-id="64e98-303">-Parallel [default value '1']</span></span>|<span data-ttu-id="64e98-304">Индикатор toorun hello созданный локального выполнения действия с hello указан уровень параллелизма.</span><span class="sxs-lookup"><span data-stu-id="64e98-304">Indicator toorun hello generated local-run steps with hello specified parallelism level.</span></span>|
|<span data-ttu-id="64e98-305">-Verbose [значение по умолчанию False]</span><span class="sxs-lookup"><span data-stu-id="64e98-305">-Verbose [default value 'False']</span></span>|<span data-ttu-id="64e98-306">Индикатор tooshow подробные выходные данные из среды выполнения.</span><span class="sxs-lookup"><span data-stu-id="64e98-306">Indicator tooshow detailed outputs from runtime.</span></span>|

<span data-ttu-id="64e98-307">Пример использования этой команды:</span><span class="sxs-lookup"><span data-stu-id="64e98-307">Here's a usage example:</span></span>

    LocalRunHelper execute -Algebra d:\test\workdir\C6A101DDCB470506\Script_66AE4909AA0ED06C\__script__.abr –DataRoot c:\DataRoot –Parallel 5


## <a name="use-hello-sdk-with-programming-interfaces"></a><span data-ttu-id="64e98-308">Использование hello SDK с интерфейсами программирования</span><span class="sxs-lookup"><span data-stu-id="64e98-308">Use hello SDK with programming interfaces</span></span>

<span data-ttu-id="64e98-309">программные интерфейсы Hello расположены в hello LocalRunHelper.exe.</span><span class="sxs-lookup"><span data-stu-id="64e98-309">hello programming interfaces are all located in hello LocalRunHelper.exe.</span></span> <span data-ttu-id="64e98-310">Можно использовать их функции hello toointegrate hello SDK U-SQL и hello tooscale framework теста C# локального тестового скрипт U-SQL.</span><span class="sxs-lookup"><span data-stu-id="64e98-310">You can use them toointegrate hello functionality of hello U-SQL SDK and hello C# test framework tooscale your U-SQL script local test.</span></span> <span data-ttu-id="64e98-311">В этой статье я буду использовать hello standard C# модульного тестирования проекта tooshow как toouse эти интерфейсы tootest скрипту U-SQL.</span><span class="sxs-lookup"><span data-stu-id="64e98-311">In this article, I will use hello standard C# unit test project tooshow how toouse these interfaces tootest your U-SQL script.</span></span>

### <a name="step-1-create-c-unit-test-project-and-configuration"></a><span data-ttu-id="64e98-312">Шаг 1. Создание проекта модульного теста C# и его настройка</span><span class="sxs-lookup"><span data-stu-id="64e98-312">Step 1: Create C# unit test project and configuration</span></span>

- <span data-ttu-id="64e98-313">Создайте проект модульного теста C#, выбрав "Файл" > "Создать" > "Проект" > "Visual C#" > "Тест" > "Проект модульного теста".</span><span class="sxs-lookup"><span data-stu-id="64e98-313">Create a C# unit test project through File > New > Project > Visual C# > Test > Unit Test Project.</span></span>
- <span data-ttu-id="64e98-314">Добавьте LocalRunHelper.exe в качестве ссылки для проекта hello.</span><span class="sxs-lookup"><span data-stu-id="64e98-314">Add LocalRunHelper.exe as a reference for hello project.</span></span> <span data-ttu-id="64e98-315">Hello LocalRunHelper.exe находится в \build\runtime\LocalRunHelper.exe в пакет Nuget.</span><span class="sxs-lookup"><span data-stu-id="64e98-315">hello LocalRunHelper.exe is located at \build\runtime\LocalRunHelper.exe in Nuget package.</span></span>

    ![Добавление ссылки на пакет SDK Azure Data Lake для U-SQL](./media/data-lake-analytics-u-sql-sdk/data-lake-analytics-u-sql-sdk-add-reference.png)

- <span data-ttu-id="64e98-317">Пакет SDK U-SQL **только** поддержки x64 среде, убедитесь что tooset целевой платформы сборки как x64.</span><span class="sxs-lookup"><span data-stu-id="64e98-317">U-SQL SDK **only** support x64 environment, make sure tooset build platform target as x64.</span></span> <span data-ttu-id="64e98-318">Это можно сделать, выбрав "Свойство проекта" > "Сборка" > "Целевая платформа".</span><span class="sxs-lookup"><span data-stu-id="64e98-318">You can set that through Project Property > Build > Platform target.</span></span>

    ![Настройка платформы x64 в проекте для использования пакета SDK Azure Data Lake для U-SQL](./media/data-lake-analytics-u-sql-sdk/data-lake-analytics-u-sql-sdk-configure-x64.png)

- <span data-ttu-id="64e98-320">Убедитесь, что tooset тестовой среды как x64.</span><span class="sxs-lookup"><span data-stu-id="64e98-320">Make sure tooset your test environment as x64.</span></span> <span data-ttu-id="64e98-321">В Visual Studio это можно сделать, выбрав "Тест" > "Параметры теста" > " 	Архитектура процессора по умолчанию" > "x64".</span><span class="sxs-lookup"><span data-stu-id="64e98-321">In Visual Studio, you can set it through Test > Test Settings > Default Processor Architecture > x64.</span></span>

    ![Настройка тестовой среды x64 для использования пакета SDK Azure Data Lake для U-SQL](./media/data-lake-analytics-u-sql-sdk/data-lake-analytics-u-sql-sdk-configure-test-x64.png)

- <span data-ttu-id="64e98-323">Убедитесь, что toocopy все файлы зависимостей в рабочем каталоге NugetPackage\build\runtime\ tooproject, которая обычно находится в стадии ProjectFolder\bin\x64\Debug.</span><span class="sxs-lookup"><span data-stu-id="64e98-323">Make sure toocopy all dependency files under NugetPackage\build\runtime\ tooproject working directory which is usually under ProjectFolder\bin\x64\Debug.</span></span>

### <a name="step-2-create-u-sql-script-test-case"></a><span data-ttu-id="64e98-324">Шаг 2. Создание тестового случая сценария U-SQL</span><span class="sxs-lookup"><span data-stu-id="64e98-324">Step 2: Create U-SQL script test case</span></span>

<span data-ttu-id="64e98-325">Ниже приведен пример кода hello для теста скрипт U-SQL.</span><span class="sxs-lookup"><span data-stu-id="64e98-325">Below is hello sample code for U-SQL script test.</span></span> <span data-ttu-id="64e98-326">Для тестирования, необходимо сценарии tooprepare входных и выходных файлов.</span><span class="sxs-lookup"><span data-stu-id="64e98-326">For testing, you need tooprepare scripts, input files and expected output files.</span></span>

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
                //Specify hello local run message output path
                StreamWriter MessageOutput = new StreamWriter("../../../log.txt");

                LocalRunHelper localrun = new LocalRunHelper(MessageOutput);

                //Configure hello DateRoot path, Script Path and CPPSDK path
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

                //Don't forget tooclose MessageOutput tooget logs into file
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


### <a name="programming-interfaces-in-localrunhelperexe"></a><span data-ttu-id="64e98-327">Программные интерфейсы в LocalRunHelper.exe</span><span class="sxs-lookup"><span data-stu-id="64e98-327">Programming interfaces in LocalRunHelper.exe</span></span>

<span data-ttu-id="64e98-328">LocalRunHelper.exe предоставляет программные интерфейсы для локального компиляции U-SQL, запустите hello, интерфейсы hello и т.д., перечислены ниже.</span><span class="sxs-lookup"><span data-stu-id="64e98-328">LocalRunHelper.exe provides hello programming interfaces for U-SQL local compile, run, etc. hello interfaces are listed as follows.</span></span>

<span data-ttu-id="64e98-329">**Конструктор**</span><span class="sxs-lookup"><span data-stu-id="64e98-329">**Constructor**</span></span>

<span data-ttu-id="64e98-330">public LocalRunHelper([System.IO.TextWriter messageOutput = null])</span><span class="sxs-lookup"><span data-stu-id="64e98-330">public LocalRunHelper([System.IO.TextWriter messageOutput = null])</span></span>

|<span data-ttu-id="64e98-331">Параметр</span><span class="sxs-lookup"><span data-stu-id="64e98-331">Parameter</span></span>|<span data-ttu-id="64e98-332">Тип</span><span class="sxs-lookup"><span data-stu-id="64e98-332">Type</span></span>|<span data-ttu-id="64e98-333">Описание</span><span class="sxs-lookup"><span data-stu-id="64e98-333">Description</span></span>|
|---------|----|-----------|
|<span data-ttu-id="64e98-334">messageOutput</span><span class="sxs-lookup"><span data-stu-id="64e98-334">messageOutput</span></span>|<span data-ttu-id="64e98-335">System.IO.TextWriter</span><span class="sxs-lookup"><span data-stu-id="64e98-335">System.IO.TextWriter</span></span>|<span data-ttu-id="64e98-336">для выходных сообщений задайте toonull toouse консоли</span><span class="sxs-lookup"><span data-stu-id="64e98-336">for output messages, set toonull toouse Console</span></span>|

<span data-ttu-id="64e98-337">**Свойства**</span><span class="sxs-lookup"><span data-stu-id="64e98-337">**Properties**</span></span>

|<span data-ttu-id="64e98-338">Свойство</span><span class="sxs-lookup"><span data-stu-id="64e98-338">Property</span></span>|<span data-ttu-id="64e98-339">Тип</span><span class="sxs-lookup"><span data-stu-id="64e98-339">Type</span></span>|<span data-ttu-id="64e98-340">Описание</span><span class="sxs-lookup"><span data-stu-id="64e98-340">Description</span></span>|
|--------|----|-----------|
|<span data-ttu-id="64e98-341">AlgebraPath</span><span class="sxs-lookup"><span data-stu-id="64e98-341">AlgebraPath</span></span>|<span data-ttu-id="64e98-342">string</span><span class="sxs-lookup"><span data-stu-id="64e98-342">string</span></span>|<span data-ttu-id="64e98-343">Hello путь к файлу tooalgebra (алгебры файл является одним из результатов компиляции hello)</span><span class="sxs-lookup"><span data-stu-id="64e98-343">hello path tooalgebra file (algebra file is one of hello compilation results)</span></span>|
|<span data-ttu-id="64e98-344">CodeBehindReferences</span><span class="sxs-lookup"><span data-stu-id="64e98-344">CodeBehindReferences</span></span>|<span data-ttu-id="64e98-345">string</span><span class="sxs-lookup"><span data-stu-id="64e98-345">string</span></span>|<span data-ttu-id="64e98-346">Если скрипт hello дополнительный код программной части ссылки, укажите hello путей, разделенные «;»</span><span class="sxs-lookup"><span data-stu-id="64e98-346">If hello script has additional code behind references, specify hello paths separated with ';'</span></span>|
|<span data-ttu-id="64e98-347">CppSdkDir</span><span class="sxs-lookup"><span data-stu-id="64e98-347">CppSdkDir</span></span>|<span data-ttu-id="64e98-348">строка</span><span class="sxs-lookup"><span data-stu-id="64e98-348">string</span></span>|<span data-ttu-id="64e98-349">Каталог пакета CppSDK.</span><span class="sxs-lookup"><span data-stu-id="64e98-349">CppSDK directory</span></span>|
|<span data-ttu-id="64e98-350">CurrentDir</span><span class="sxs-lookup"><span data-stu-id="64e98-350">CurrentDir</span></span>|<span data-ttu-id="64e98-351">строка</span><span class="sxs-lookup"><span data-stu-id="64e98-351">string</span></span>|<span data-ttu-id="64e98-352">Текущий каталог.</span><span class="sxs-lookup"><span data-stu-id="64e98-352">Current directory</span></span>|
|<span data-ttu-id="64e98-353">DataRoot</span><span class="sxs-lookup"><span data-stu-id="64e98-353">DataRoot</span></span>|<span data-ttu-id="64e98-354">string</span><span class="sxs-lookup"><span data-stu-id="64e98-354">string</span></span>|<span data-ttu-id="64e98-355">Путь к корневой папке данных.</span><span class="sxs-lookup"><span data-stu-id="64e98-355">Data root path</span></span>|
|<span data-ttu-id="64e98-356">DebuggerMailPath</span><span class="sxs-lookup"><span data-stu-id="64e98-356">DebuggerMailPath</span></span>|<span data-ttu-id="64e98-357">string</span><span class="sxs-lookup"><span data-stu-id="64e98-357">string</span></span>|<span data-ttu-id="64e98-358">почтовый слот toodebugger путь Hello</span><span class="sxs-lookup"><span data-stu-id="64e98-358">hello path toodebugger mailslot</span></span>|
|<span data-ttu-id="64e98-359">GenerateUdoRedirect</span><span class="sxs-lookup"><span data-stu-id="64e98-359">GenerateUdoRedirect</span></span>|<span data-ttu-id="64e98-360">bool</span><span class="sxs-lookup"><span data-stu-id="64e98-360">bool</span></span>|<span data-ttu-id="64e98-361">Если мы хотим загрузки сборки toogenerate перенаправления переопределения конфигурации</span><span class="sxs-lookup"><span data-stu-id="64e98-361">If we want toogenerate assembly loading redirection override config</span></span>|
|<span data-ttu-id="64e98-362">HasCodeBehind</span><span class="sxs-lookup"><span data-stu-id="64e98-362">HasCodeBehind</span></span>|<span data-ttu-id="64e98-363">bool</span><span class="sxs-lookup"><span data-stu-id="64e98-363">bool</span></span>|<span data-ttu-id="64e98-364">Если скрипт hello содержит код программной части</span><span class="sxs-lookup"><span data-stu-id="64e98-364">If hello script has code behind</span></span>|
|<span data-ttu-id="64e98-365">InputDir</span><span class="sxs-lookup"><span data-stu-id="64e98-365">InputDir</span></span>|<span data-ttu-id="64e98-366">строка</span><span class="sxs-lookup"><span data-stu-id="64e98-366">string</span></span>|<span data-ttu-id="64e98-367">Каталог для входных данных.</span><span class="sxs-lookup"><span data-stu-id="64e98-367">Directory for input data</span></span>|
|<span data-ttu-id="64e98-368">MessagePath</span><span class="sxs-lookup"><span data-stu-id="64e98-368">MessagePath</span></span>|<span data-ttu-id="64e98-369">строка</span><span class="sxs-lookup"><span data-stu-id="64e98-369">string</span></span>|<span data-ttu-id="64e98-370">Путь к файлу дампа сообщений.</span><span class="sxs-lookup"><span data-stu-id="64e98-370">Message dump file path</span></span>|
|<span data-ttu-id="64e98-371">OutputDir</span><span class="sxs-lookup"><span data-stu-id="64e98-371">OutputDir</span></span>|<span data-ttu-id="64e98-372">строка</span><span class="sxs-lookup"><span data-stu-id="64e98-372">string</span></span>|<span data-ttu-id="64e98-373">Каталог для выходных данных.</span><span class="sxs-lookup"><span data-stu-id="64e98-373">Directory for output data</span></span>|
|<span data-ttu-id="64e98-374">Параллелизм</span><span class="sxs-lookup"><span data-stu-id="64e98-374">Parallelism</span></span>|<span data-ttu-id="64e98-375">int</span><span class="sxs-lookup"><span data-stu-id="64e98-375">int</span></span>|<span data-ttu-id="64e98-376">Алгебраические hello toorun параллелизма</span><span class="sxs-lookup"><span data-stu-id="64e98-376">Parallelism toorun hello algebra</span></span>|
|<span data-ttu-id="64e98-377">ParentPid</span><span class="sxs-lookup"><span data-stu-id="64e98-377">ParentPid</span></span>|<span data-ttu-id="64e98-378">int</span><span class="sxs-lookup"><span data-stu-id="64e98-378">int</span></span>|<span data-ttu-id="64e98-379">Идентификатор Процесса, на какие hello служба отслеживает tooexit, too0 набор или отрицательным tooignore родителя hello</span><span class="sxs-lookup"><span data-stu-id="64e98-379">PID of hello parent on which hello service monitors tooexit, set too0 or negative tooignore</span></span>|
|<span data-ttu-id="64e98-380">ResultPath</span><span class="sxs-lookup"><span data-stu-id="64e98-380">ResultPath</span></span>|<span data-ttu-id="64e98-381">строка</span><span class="sxs-lookup"><span data-stu-id="64e98-381">string</span></span>|<span data-ttu-id="64e98-382">Путь к файлу дампа результатов.</span><span class="sxs-lookup"><span data-stu-id="64e98-382">Result dump file path</span></span>|
|<span data-ttu-id="64e98-383">RuntimeDir</span><span class="sxs-lookup"><span data-stu-id="64e98-383">RuntimeDir</span></span>|<span data-ttu-id="64e98-384">строка</span><span class="sxs-lookup"><span data-stu-id="64e98-384">string</span></span>|<span data-ttu-id="64e98-385">Каталог среды выполнения.</span><span class="sxs-lookup"><span data-stu-id="64e98-385">Runtime directory</span></span>|
|<span data-ttu-id="64e98-386">ScriptPath</span><span class="sxs-lookup"><span data-stu-id="64e98-386">ScriptPath</span></span>|<span data-ttu-id="64e98-387">string</span><span class="sxs-lookup"><span data-stu-id="64e98-387">string</span></span>|<span data-ttu-id="64e98-388">Где toofind hello сценария</span><span class="sxs-lookup"><span data-stu-id="64e98-388">Where toofind hello script</span></span>|
|<span data-ttu-id="64e98-389">Shallow</span><span class="sxs-lookup"><span data-stu-id="64e98-389">Shallow</span></span>|<span data-ttu-id="64e98-390">bool</span><span class="sxs-lookup"><span data-stu-id="64e98-390">bool</span></span>|<span data-ttu-id="64e98-391">Позволяет задать выполнение неполной компиляции.</span><span class="sxs-lookup"><span data-stu-id="64e98-391">Shallow compile or not</span></span>|
|<span data-ttu-id="64e98-392">TempDir</span><span class="sxs-lookup"><span data-stu-id="64e98-392">TempDir</span></span>|<span data-ttu-id="64e98-393">строка</span><span class="sxs-lookup"><span data-stu-id="64e98-393">string</span></span>|<span data-ttu-id="64e98-394">Каталог временных данных</span><span class="sxs-lookup"><span data-stu-id="64e98-394">Temp directory</span></span>|
|<span data-ttu-id="64e98-395">UseDataBase</span><span class="sxs-lookup"><span data-stu-id="64e98-395">UseDataBase</span></span>|<span data-ttu-id="64e98-396">string</span><span class="sxs-lookup"><span data-stu-id="64e98-396">string</span></span>|<span data-ttu-id="64e98-397">Укажите hello toouse базы данных для кода за пределами временную сборку регистрации master по умолчанию</span><span class="sxs-lookup"><span data-stu-id="64e98-397">Specify hello database toouse for code behind temporary assembly registration, master by default</span></span>|
|<span data-ttu-id="64e98-398">WorkDir</span><span class="sxs-lookup"><span data-stu-id="64e98-398">WorkDir</span></span>|<span data-ttu-id="64e98-399">строка</span><span class="sxs-lookup"><span data-stu-id="64e98-399">string</span></span>|<span data-ttu-id="64e98-400">Предпочитаемый рабочий каталог.</span><span class="sxs-lookup"><span data-stu-id="64e98-400">Preferred working directory</span></span>|


<span data-ttu-id="64e98-401">**Метод**</span><span class="sxs-lookup"><span data-stu-id="64e98-401">**Method**</span></span>

|<span data-ttu-id="64e98-402">Метод</span><span class="sxs-lookup"><span data-stu-id="64e98-402">Method</span></span>|<span data-ttu-id="64e98-403">Описание</span><span class="sxs-lookup"><span data-stu-id="64e98-403">Description</span></span>|<span data-ttu-id="64e98-404">Return</span><span class="sxs-lookup"><span data-stu-id="64e98-404">Return</span></span>|<span data-ttu-id="64e98-405">Параметр</span><span class="sxs-lookup"><span data-stu-id="64e98-405">Parameter</span></span>|
|------|-----------|------|---------|
|<span data-ttu-id="64e98-406">public bool DoCompile()</span><span class="sxs-lookup"><span data-stu-id="64e98-406">public bool DoCompile()</span></span>|<span data-ttu-id="64e98-407">Компиляции сценария hello U-SQL</span><span class="sxs-lookup"><span data-stu-id="64e98-407">Compile hello U-SQL script</span></span>|<span data-ttu-id="64e98-408">В случае успешного выполнения возвращает True.</span><span class="sxs-lookup"><span data-stu-id="64e98-408">True on success</span></span>| |
|<span data-ttu-id="64e98-409">public bool DoExec()</span><span class="sxs-lookup"><span data-stu-id="64e98-409">public bool DoExec()</span></span>|<span data-ttu-id="64e98-410">Выполнение результата hello компиляции</span><span class="sxs-lookup"><span data-stu-id="64e98-410">Execute hello compiled result</span></span>|<span data-ttu-id="64e98-411">В случае успешного выполнения возвращает True.</span><span class="sxs-lookup"><span data-stu-id="64e98-411">True on success</span></span>| |
|<span data-ttu-id="64e98-412">public bool DoRun()</span><span class="sxs-lookup"><span data-stu-id="64e98-412">public bool DoRun()</span></span>|<span data-ttu-id="64e98-413">Запустите сценарий hello U-SQL (компиляции + Execute)</span><span class="sxs-lookup"><span data-stu-id="64e98-413">Run hello U-SQL script (Compile + Execute)</span></span>|<span data-ttu-id="64e98-414">В случае успешного выполнения возвращает True.</span><span class="sxs-lookup"><span data-stu-id="64e98-414">True on success</span></span>| |
|<span data-ttu-id="64e98-415">public bool IsValidRuntimeDir(string path)</span><span class="sxs-lookup"><span data-stu-id="64e98-415">public bool IsValidRuntimeDir(string path)</span></span>|<span data-ttu-id="64e98-416">Проверьте, является ли заданный путь hello путь допустимое время выполнения</span><span class="sxs-lookup"><span data-stu-id="64e98-416">Check if hello given path is valid runtime path</span></span>|<span data-ttu-id="64e98-417">Значение True, если путь допустимый.</span><span class="sxs-lookup"><span data-stu-id="64e98-417">True for valid</span></span>|<span data-ttu-id="64e98-418">Hello путь от каталога среды выполнения</span><span class="sxs-lookup"><span data-stu-id="64e98-418">hello path of runtime directory</span></span>|


## <a name="faq-about-common-issue"></a><span data-ttu-id="64e98-419">Часто задаваемые вопросы о распространенных проблемах</span><span class="sxs-lookup"><span data-stu-id="64e98-419">FAQ about common issue</span></span>

### <a name="error-1"></a><span data-ttu-id="64e98-420">Ошибка 1</span><span class="sxs-lookup"><span data-stu-id="64e98-420">Error 1:</span></span>
<span data-ttu-id="64e98-421">E_CSC_SYSTEM_INTERNAL: Внутренняя ошибка!</span><span class="sxs-lookup"><span data-stu-id="64e98-421">E_CSC_SYSTEM_INTERNAL: Internal error!</span></span> <span data-ttu-id="64e98-422">Не удалось загрузить файл или сборку "ScopeEngineManaged.dll" либо одну из ее зависимостей.</span><span class="sxs-lookup"><span data-stu-id="64e98-422">Could not load file or assembly 'ScopeEngineManaged.dll' or one of its dependencies.</span></span> <span data-ttu-id="64e98-423">не удалось найти указанный модуль Hello.</span><span class="sxs-lookup"><span data-stu-id="64e98-423">hello specified module could not be found.</span></span>

<span data-ttu-id="64e98-424">Проверьте hello следующее:</span><span class="sxs-lookup"><span data-stu-id="64e98-424">Please check hello following:</span></span>

- <span data-ttu-id="64e98-425">Убедитесь, что используется среда x64.</span><span class="sxs-lookup"><span data-stu-id="64e98-425">Make sure you have x64 environment.</span></span> <span data-ttu-id="64e98-426">Целевая платформа для построения Hello и hello тестовой среде следует x64 см. в слишком**шаг 1: создание C# модульного тестирования проекта и конфигурация** выше.</span><span class="sxs-lookup"><span data-stu-id="64e98-426">hello build target platform and hello test environment should be x64, refer too**Step 1: Create C# unit test project and configuration** above.</span></span>
- <span data-ttu-id="64e98-427">Убедитесь, что вы скопировали все файлы зависимостей в NugetPackage\build\runtime\ tooproject рабочий каталог.</span><span class="sxs-lookup"><span data-stu-id="64e98-427">Make sure you have copied all dependency files under NugetPackage\build\runtime\ tooproject working directory.</span></span>


## <a name="next-steps"></a><span data-ttu-id="64e98-428">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="64e98-428">Next steps</span></span>

* <span data-ttu-id="64e98-429">в разделе toolearn U-SQL [Приступая к работе с Azure аналитика Озера данных U-SQL языка](data-lake-analytics-u-sql-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="64e98-429">toolearn U-SQL, see [Get started with Azure Data Lake Analytics U-SQL language](data-lake-analytics-u-sql-get-started.md).</span></span>
* <span data-ttu-id="64e98-430">сведения диагностики toolog см. в разделе [доступ к журналов диагностики для аналитики Озера данных Azure](data-lake-analytics-diagnostic-logs.md).</span><span class="sxs-lookup"><span data-stu-id="64e98-430">toolog diagnostics information, see [Accessing diagnostics logs for Azure Data Lake Analytics](data-lake-analytics-diagnostic-logs.md).</span></span>
* <span data-ttu-id="64e98-431">в разделе toosee более сложный запрос, [анализа журналов веб-сайта с помощью аналитики Озера данных Azure](data-lake-analytics-analyze-weblogs.md).</span><span class="sxs-lookup"><span data-stu-id="64e98-431">toosee a more complex query, see [Analyze website logs using Azure Data Lake Analytics](data-lake-analytics-analyze-weblogs.md).</span></span>
* <span data-ttu-id="64e98-432">см. сведения о задании tooview, [используйте браузер задания и представление заданий для задания аналитики Озера данных Azure](data-lake-analytics-data-lake-tools-view-jobs.md).</span><span class="sxs-lookup"><span data-stu-id="64e98-432">tooview job details, see [Use Job Browser and Job View for Azure Data Lake Analytics jobs](data-lake-analytics-data-lake-tools-view-jobs.md).</span></span>
* <span data-ttu-id="64e98-433">представление выполнения вершин toouse hello, в разделе [hello используйте представление выполнения вершин в средствах Озера данных для Visual Studio](data-lake-analytics-data-lake-tools-use-vertex-execution-view.md).</span><span class="sxs-lookup"><span data-stu-id="64e98-433">toouse hello vertex execution view, see [Use hello Vertex Execution View in Data Lake Tools for Visual Studio](data-lake-analytics-data-lake-tools-use-vertex-execution-view.md).</span></span>
