---
title: "aaaTest и отладки U-SQL заданий с помощью локального запуска и hello U Озера данных Azure SQL пакета SDK | Документы Microsoft"
description: "Узнайте, как toouse средства Озера данных Azure для Visual Studio и SDK U Озера данных Azure SQL tootest hello и отладки U-SQL заданий на локальной рабочей станции."
services: data-lake-analytics
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 66dd58b1-0b28-46d1-aaae-43ee2739ae0a
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 11/15/2016
ms.author: yanacai
ms.openlocfilehash: be04558a504acf6a088e207608ee2d4a011d3ffc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="test-and-debug-u-sql-jobs-by-using-local-run-and-hello-azure-data-lake-u-sql-sdk"></a><span data-ttu-id="46b49-103">Тестирование и отладку заданий U-SQL с помощью локального запуска и hello SDK U Озера данных Azure SQL</span><span class="sxs-lookup"><span data-stu-id="46b49-103">Test and debug U-SQL jobs by using local run and hello Azure Data Lake U-SQL SDK</span></span>

<span data-ttu-id="46b49-104">Так же, как в службе hello Озера данных Azure, можно использовать средства Озера данных Azure для Visual Studio и hello SDK U Озера данных Azure SQL toorun U-SQL заданий на рабочей станции.</span><span class="sxs-lookup"><span data-stu-id="46b49-104">You can use Azure Data Lake Tools for Visual Studio and hello Azure Data Lake U-SQL SDK toorun U-SQL jobs on your workstation, just as you can in hello Azure Data Lake service.</span></span> <span data-ttu-id="46b49-105">Оба этих компонента для локального выполнения помогут вам быстрее выполнять тестирование и отладку заданий U-SQL.</span><span class="sxs-lookup"><span data-stu-id="46b49-105">These two local-run features save you time in testing and debugging your U-SQL jobs.</span></span>

## <a name="understand-hello-data-root-folder-and-hello-file-path"></a><span data-ttu-id="46b49-106">Понимать hello данных корневой папки и путь к файлу hello</span><span class="sxs-lookup"><span data-stu-id="46b49-106">Understand hello data-root folder and hello file path</span></span>

<span data-ttu-id="46b49-107">Локального запуска и hello SDK U-SQL требуют данных корневую папку.</span><span class="sxs-lookup"><span data-stu-id="46b49-107">Both local run and hello U-SQL SDK require a data-root folder.</span></span> <span data-ttu-id="46b49-108">Папка Hello корневой каталог данных является «локальное хранилище» для учетной записи локального вычислений hello.</span><span class="sxs-lookup"><span data-stu-id="46b49-108">hello data-root folder is a "local store" for hello local compute account.</span></span> <span data-ttu-id="46b49-109">Это учетная запись хранилища Озера данных Azure эквивалентные toohello учетной записи аналитики Озера данных.</span><span class="sxs-lookup"><span data-stu-id="46b49-109">It's equivalent toohello Azure Data Lake Store account of a Data Lake Analytics account.</span></span> <span data-ttu-id="46b49-110">Переключение tooa папку другой корневой каталог данных является так же, как переключения учетной записи tooa другое хранилище.</span><span class="sxs-lookup"><span data-stu-id="46b49-110">Switching tooa different data-root folder is just like switching tooa different store account.</span></span> <span data-ttu-id="46b49-111">Если вы хотите tooaccess часто общих данных с папками другой корневой каталог данных, необходимо использовать абсолютные пути в скриптах.</span><span class="sxs-lookup"><span data-stu-id="46b49-111">If you want tooaccess commonly shared data with different data-root folders, you must use absolute paths in your scripts.</span></span> <span data-ttu-id="46b49-112">Или Создание символических ссылок системных файлов (например, **mklink** в файловой системе NTFS) в папку toopoint hello корневой каталог данных toohello общих данных.</span><span class="sxs-lookup"><span data-stu-id="46b49-112">Or, create file system symbolic links (for example, **mklink** on NTFS) under hello data-root folder toopoint toohello shared data.</span></span>

<span data-ttu-id="46b49-113">Папка Hello корневой каталог данных используется для:</span><span class="sxs-lookup"><span data-stu-id="46b49-113">hello data-root folder is used to:</span></span>

- <span data-ttu-id="46b49-114">Хранение метаданных, включая базы данных, таблицы, функции с табличным значением (TVF) и сборки.</span><span class="sxs-lookup"><span data-stu-id="46b49-114">Store metadata, including databases, tables, table-valued functions (TVFs), and assemblies.</span></span>
- <span data-ttu-id="46b49-115">Поиск hello входного и выходного пути, которые определяются как относительные пути в U-SQL.</span><span class="sxs-lookup"><span data-stu-id="46b49-115">Look up hello input and output paths that are defined as relative paths in U-SQL.</span></span> <span data-ttu-id="46b49-116">Использование относительных путей делает проще toodeploy вашей tooAzure проекты U-SQL.</span><span class="sxs-lookup"><span data-stu-id="46b49-116">Using relative paths makes it easier toodeploy your U-SQL projects tooAzure.</span></span>

<span data-ttu-id="46b49-117">В скриптах U-SQL можно использовать как относительные, так и абсолютные локальные пути.</span><span class="sxs-lookup"><span data-stu-id="46b49-117">You can use both a relative path and a local absolute path in U-SQL scripts.</span></span> <span data-ttu-id="46b49-118">относительный путь Hello — toohello относительный путь к папке указанный корневой каталог данных.</span><span class="sxs-lookup"><span data-stu-id="46b49-118">hello relative path is relative toohello specified data-root folder path.</span></span> <span data-ttu-id="46b49-119">Рекомендуется, можно использовать «/» как hello toomake разделителя пути скрипты, совместимые со стороны сервера hello.</span><span class="sxs-lookup"><span data-stu-id="46b49-119">We recommend that you use "/" as hello path separator toomake your scripts compatible with hello server side.</span></span> <span data-ttu-id="46b49-120">Ниже приведены некоторые примеры относительных путей и их абсолютные эквиваленты.</span><span class="sxs-lookup"><span data-stu-id="46b49-120">Here are some examples of relative paths and their equivalent absolute paths.</span></span> <span data-ttu-id="46b49-121">В этих примерах C:\LocalRunDataRoot — папка hello корневой каталог данных.</span><span class="sxs-lookup"><span data-stu-id="46b49-121">In these examples, C:\LocalRunDataRoot is hello data-root folder.</span></span>

|<span data-ttu-id="46b49-122">Относительный путь</span><span class="sxs-lookup"><span data-stu-id="46b49-122">Relative path</span></span>|<span data-ttu-id="46b49-123">Абсолютный путь</span><span class="sxs-lookup"><span data-stu-id="46b49-123">Absolute path</span></span>|
|-------------|-------------|
|<span data-ttu-id="46b49-124">/abc/def/input.csv</span><span class="sxs-lookup"><span data-stu-id="46b49-124">/abc/def/input.csv</span></span> |<span data-ttu-id="46b49-125">C:\LocalRunDataRoot\abc\def\input.csv</span><span class="sxs-lookup"><span data-stu-id="46b49-125">C:\LocalRunDataRoot\abc\def\input.csv</span></span>|
|<span data-ttu-id="46b49-126">abc/def/input.csv</span><span class="sxs-lookup"><span data-stu-id="46b49-126">abc/def/input.csv</span></span>  |<span data-ttu-id="46b49-127">C:\LocalRunDataRoot\abc\def\input.csv</span><span class="sxs-lookup"><span data-stu-id="46b49-127">C:\LocalRunDataRoot\abc\def\input.csv</span></span>|
|<span data-ttu-id="46b49-128">D:/abc/def/input.csv</span><span class="sxs-lookup"><span data-stu-id="46b49-128">D:/abc/def/input.csv</span></span> |<span data-ttu-id="46b49-129">D:\abc\def\input.csv</span><span class="sxs-lookup"><span data-stu-id="46b49-129">D:\abc\def\input.csv</span></span>|

## <a name="use-local-run-from-visual-studio"></a><span data-ttu-id="46b49-130">Локальное выполнение из Visual Studio</span><span class="sxs-lookup"><span data-stu-id="46b49-130">Use local run from Visual Studio</span></span>

<span data-ttu-id="46b49-131">Средства Data Lake для Visual Studio предоставляют возможность локального выполнения U-SQL в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="46b49-131">Data Lake Tools for Visual Studio provides a U-SQL local-run experience in Visual Studio.</span></span> <span data-ttu-id="46b49-132">Это позволит вам:</span><span class="sxs-lookup"><span data-stu-id="46b49-132">By using this feature, you can:</span></span>

- <span data-ttu-id="46b49-133">локально запускать скрипты U-SQL вместе со сборками C#;</span><span class="sxs-lookup"><span data-stu-id="46b49-133">Run a U-SQL script locally, along with C# assemblies.</span></span>
- <span data-ttu-id="46b49-134">локально выполнять отладку сборок C#;</span><span class="sxs-lookup"><span data-stu-id="46b49-134">Debug a C# assembly locally.</span></span>
- <span data-ttu-id="46b49-135">создавать, просматривать и удалять каталоги U-SQL (локальные базы данных, сборки, схемы и таблицы) с помощью обозревателя сервера.</span><span class="sxs-lookup"><span data-stu-id="46b49-135">Create, view, and delete U-SQL catalogs (local databases, assemblies, schemas, and tables) from Server Explorer.</span></span> <span data-ttu-id="46b49-136">Также можно также найти hello локального каталога из обозревателя серверов.</span><span class="sxs-lookup"><span data-stu-id="46b49-136">You can also find hello local catalog also from Server Explorer.</span></span>

    ![Локальный каталог для локального выполнения средств Data Lake для Visual Studio](./media/data-lake-analytics-data-lake-tools-local-run/data-lake-tools-for-visual-studio-local-run-local-catalog.png)

<span data-ttu-id="46b49-138">Установщик инструментов Озера данных Hello создает C:\LocalRunRoot toobe папки, используемые как папка корневой каталог данных по умолчанию hello.</span><span class="sxs-lookup"><span data-stu-id="46b49-138">hello Data Lake Tools installer creates a C:\LocalRunRoot folder toobe used as hello default data-root folder.</span></span> <span data-ttu-id="46b49-139">параллелизм локального выполнения Hello по умолчанию — 1.</span><span class="sxs-lookup"><span data-stu-id="46b49-139">hello default local-run parallelism is 1.</span></span>

### <a name="tooconfigure-local-run-in-visual-studio"></a><span data-ttu-id="46b49-140">tooconfigure локальном запуске в Visual Studio</span><span class="sxs-lookup"><span data-stu-id="46b49-140">tooconfigure local run in Visual Studio</span></span>

1. <span data-ttu-id="46b49-141">Откройте Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="46b49-141">Open Visual Studio.</span></span>
2. <span data-ttu-id="46b49-142">Откройте **обозреватель сервера**.</span><span class="sxs-lookup"><span data-stu-id="46b49-142">Open **Server Explorer**.</span></span>
3. <span data-ttu-id="46b49-143">Разверните узлы **Azure** > **Data Lake Analytics**.</span><span class="sxs-lookup"><span data-stu-id="46b49-143">Expand **Azure** > **Data Lake Analytics**.</span></span>
4. <span data-ttu-id="46b49-144">Нажмите кнопку hello **Озера данных** меню, а затем нажмите **параметры и настройки**.</span><span class="sxs-lookup"><span data-stu-id="46b49-144">Click hello **Data Lake** menu, and then click **Options and Settings**.</span></span>
5. <span data-ttu-id="46b49-145">В дереве слева hello разверните **Озера данных Azure**, а затем разверните **Общие**.</span><span class="sxs-lookup"><span data-stu-id="46b49-145">In hello left tree, expand **Azure Data Lake**, and then expand **General**.</span></span>

    ![Настройка параметров для локального выполнения средств Data Lake для Visual Studio](./media/data-lake-analytics-data-lake-tools-local-run/data-lake-tools-for-visual-studio-local-run-configure.png)

<span data-ttu-id="46b49-147">Для локального выполнения требуется создать проект U-SQL для Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="46b49-147">A Visual Studio U-SQL project is required for performing local run.</span></span> <span data-ttu-id="46b49-148">Эта часть выполняется не так, как при запуске скриптов U-SQL в Azure.</span><span class="sxs-lookup"><span data-stu-id="46b49-148">This part is different from running U-SQL scripts from Azure.</span></span>

### <a name="toorun-a-u-sql-script-locally"></a><span data-ttu-id="46b49-149">скрипт U-SQL toorun локально</span><span class="sxs-lookup"><span data-stu-id="46b49-149">toorun a U-SQL script locally</span></span>
1. <span data-ttu-id="46b49-150">В Visual Studio откройте нужный проект U-SQL.</span><span class="sxs-lookup"><span data-stu-id="46b49-150">From Visual Studio, open your U-SQL project.</span></span>   
2. <span data-ttu-id="46b49-151">В обозревателе решений щелкните правой кнопкой мыши скрипт U-SQL и выберите команду **Submit Script** (Отправить скрипт).</span><span class="sxs-lookup"><span data-stu-id="46b49-151">Right-click a U-SQL script in Solution Explorer, and then click **Submit Script**.</span></span>
3. <span data-ttu-id="46b49-152">Выберите **(Local)** как hello учетной записи в аналитике toorun сценарий локально.</span><span class="sxs-lookup"><span data-stu-id="46b49-152">Select **(Local)** as hello Analytics account toorun your script locally.</span></span>
<span data-ttu-id="46b49-153">Можно также щелкнуть hello **(Local)** учетную запись на hello верхней части окна «сценарий», а затем нажмите кнопку **отправить** (или используйте Здравствуйте, Ctrl + клавиша F5).</span><span class="sxs-lookup"><span data-stu-id="46b49-153">You can also click hello **(Local)** account on hello top of script window, and then click **Submit** (or use hello Ctrl + F5 keyboard shortcut).</span></span>

    ![Отправка заданий для локального выполнения средств Data Lake для Visual Studio](./media/data-lake-analytics-data-lake-tools-local-run/data-lake-tools-for-visual-studio-local-run-submit-job.png)

### <a name="debug-scripts-and-c-assemblies-locally"></a><span data-ttu-id="46b49-155">Локальная отладка скриптов и сборок C#</span><span class="sxs-lookup"><span data-stu-id="46b49-155">Debug scripts and C# assemblies locally</span></span>

<span data-ttu-id="46b49-156">Можно отлаживать C# сборки без отправки и зарегистрировав его tooAzure Служба аналитики Озера данных.</span><span class="sxs-lookup"><span data-stu-id="46b49-156">You can debug C# assemblies without submitting and registering it tooAzure Data Lake Analytics Service.</span></span> <span data-ttu-id="46b49-157">Можно установить точки останова в обоих hello файл кода программной части и на которую указывает ссылка проекта C#.</span><span class="sxs-lookup"><span data-stu-id="46b49-157">You can set breakpoints in both hello code behind file and in a referenced C# project.</span></span>

#### <a name="toodebug-local-code-in-code-behind-file"></a><span data-ttu-id="46b49-158">toodebug локальный код в файл кода программной части</span><span class="sxs-lookup"><span data-stu-id="46b49-158">toodebug local code in code behind file</span></span>

1. <span data-ttu-id="46b49-159">Установите точки останова в файл с выделенным кодом hello.</span><span class="sxs-lookup"><span data-stu-id="46b49-159">Set breakpoints in hello code behind file.</span></span>
2. <span data-ttu-id="46b49-160">Нажмите клавишу скрипт hello toodebug F5 локально.</span><span class="sxs-lookup"><span data-stu-id="46b49-160">Press F5 toodebug hello script locally.</span></span>

> [!NOTE]
   > <span data-ttu-id="46b49-161">Следующая процедура работает только в Visual Studio 2015 Hello.</span><span class="sxs-lookup"><span data-stu-id="46b49-161">hello following procedure only works in Visual Studio 2015.</span></span> <span data-ttu-id="46b49-162">В более старых Visual Studio может потребоваться toomanually добавьте hello PDB-файлы.</span><span class="sxs-lookup"><span data-stu-id="46b49-162">In older Visual Studio you may need toomanually add hello pdb files.</span></span>  
   >
   >

#### <a name="toodebug-local-code-in-a-referenced-c-project"></a><span data-ttu-id="46b49-163">Локальный код toodebug в ссылке проекта C#</span><span class="sxs-lookup"><span data-stu-id="46b49-163">toodebug local code in a referenced C# project</span></span>

1. <span data-ttu-id="46b49-164">Создание проекта C# сборки и постройте его toogenerate hello вывода dll.</span><span class="sxs-lookup"><span data-stu-id="46b49-164">Create a C# Assembly project, and build it toogenerate hello output dll.</span></span>
2. <span data-ttu-id="46b49-165">Зарегистрируйте библиотеку dll hello, с помощью инструкции U-SQL:</span><span class="sxs-lookup"><span data-stu-id="46b49-165">Register hello dll using a U-SQL statement:</span></span>

        CREATE ASSEMBLY assemblyname FROM @"..\..\path\to\output\.dll";
        
3. <span data-ttu-id="46b49-166">Установите точки останова в hello кода C#.</span><span class="sxs-lookup"><span data-stu-id="46b49-166">Set breakpoints in hello C# code.</span></span>
4. <span data-ttu-id="46b49-167">Нажмите клавишу F5 toodebug hello скрипт при создании ссылок на библиотеки dll hello C# локально.</span><span class="sxs-lookup"><span data-stu-id="46b49-167">Press F5 toodebug hello script with referencing hello C# dll locally.</span></span>

## <a name="use-local-run-from-hello-data-lake-u-sql-sdk"></a><span data-ttu-id="46b49-168">Использование локального запуска из hello SDK данных Озера U-SQL</span><span class="sxs-lookup"><span data-stu-id="46b49-168">Use local run from hello Data Lake U-SQL SDK</span></span>

<span data-ttu-id="46b49-169">Кроме toorunning U-SQL скрипты локально с помощью Visual Studio, можно использовать сценарии U-SQL toorun SDK U Озера данных Azure SQL hello локально с помощью интерфейсов командной строки и программирования.</span><span class="sxs-lookup"><span data-stu-id="46b49-169">In addition toorunning U-SQL scripts locally by using Visual Studio, you can use hello Azure Data Lake U-SQL SDK toorun U-SQL scripts locally with command-line and programming interfaces.</span></span> <span data-ttu-id="46b49-170">Это позволяет масштабировать сценарии локального тестирования U-SQL.</span><span class="sxs-lookup"><span data-stu-id="46b49-170">Through these, you can scale your U-SQL local test.</span></span>

<span data-ttu-id="46b49-171">Узнайте больше о [пакете SDK Azure Data Lake для U-SQL](data-lake-analytics-u-sql-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="46b49-171">Learn more about [Azure Data Lake U-SQL SDK](data-lake-analytics-u-sql-sdk.md).</span></span>


## <a name="next-steps"></a><span data-ttu-id="46b49-172">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="46b49-172">Next steps</span></span>

* <span data-ttu-id="46b49-173">в разделе toosee более сложный запрос, [анализа журналов веб-сайта с помощью аналитики Озера данных Azure](data-lake-analytics-analyze-weblogs.md).</span><span class="sxs-lookup"><span data-stu-id="46b49-173">toosee a more complex query, see [Analyze website logs using Azure Data Lake Analytics](data-lake-analytics-analyze-weblogs.md).</span></span>
* <span data-ttu-id="46b49-174">см. сведения о задании tooview, [используйте браузер задания и представление заданий для задания аналитики Озера данных Azure](data-lake-analytics-data-lake-tools-view-jobs.md).</span><span class="sxs-lookup"><span data-stu-id="46b49-174">tooview job details, see [Use Job Browser and Job View for Azure Data Lake Analytics jobs](data-lake-analytics-data-lake-tools-view-jobs.md).</span></span>
* <span data-ttu-id="46b49-175">представление выполнения вершин toouse hello, в разделе [hello используйте представление выполнения вершин в средствах Озера данных для Visual Studio](data-lake-analytics-data-lake-tools-use-vertex-execution-view.md).</span><span class="sxs-lookup"><span data-stu-id="46b49-175">toouse hello vertex execution view, see [Use hello Vertex Execution View in Data Lake Tools for Visual Studio](data-lake-analytics-data-lake-tools-use-vertex-execution-view.md).</span></span>
