---
title: "Тестирование и отладка заданий U-SQL с помощью локального выполнения и пакета SDK U-SQL для Azure Data Lake | Документация Майкрософт"
description: "Сведения о том, как с помощью средств Azure Data Lake для Visual Studio и пакета SDK U-SQL для Azure Data Lake выполнять тестирование и отладку заданий U-SQL на локальной рабочей станции."
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
ms.openlocfilehash: 771a96df5cc66bac46e7144785be8cc072b57b31
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="test-and-debug-u-sql-jobs-by-using-local-run-and-the-azure-data-lake-u-sql-sdk"></a><span data-ttu-id="c405f-103">Тестирование и отладка заданий U-SQL с помощью локального выполнения и пакета SDK U-SQL для Azure Data Lake</span><span class="sxs-lookup"><span data-stu-id="c405f-103">Test and debug U-SQL jobs by using local run and the Azure Data Lake U-SQL SDK</span></span>

<span data-ttu-id="c405f-104">Вы можете использовать средства Azure Data Lake для Visual Studio и пакет SDK U-SQL для Azure Data Lake, чтобы запускать задания U-SQL на рабочей станции так же, как в службе Azure Data Lake.</span><span class="sxs-lookup"><span data-stu-id="c405f-104">You can use Azure Data Lake Tools for Visual Studio and the Azure Data Lake U-SQL SDK to run U-SQL jobs on your workstation, just as you can in the Azure Data Lake service.</span></span> <span data-ttu-id="c405f-105">Оба этих компонента для локального выполнения помогут вам быстрее выполнять тестирование и отладку заданий U-SQL.</span><span class="sxs-lookup"><span data-stu-id="c405f-105">These two local-run features save you time in testing and debugging your U-SQL jobs.</span></span>

## <a name="understand-the-data-root-folder-and-the-file-path"></a><span data-ttu-id="c405f-106">Сведения о корневой папке данных и пути к файлу</span><span class="sxs-lookup"><span data-stu-id="c405f-106">Understand the data-root folder and the file path</span></span>

<span data-ttu-id="c405f-107">Для локального выполнения и использования пакетов SDK U-SQL вам потребуется настроить корневую папку данных.</span><span class="sxs-lookup"><span data-stu-id="c405f-107">Both local run and the U-SQL SDK require a data-root folder.</span></span> <span data-ttu-id="c405f-108">Корневая папка данных служит "локальным хранилищем" для локальной учетной записи среды вычислений.</span><span class="sxs-lookup"><span data-stu-id="c405f-108">The data-root folder is a "local store" for the local compute account.</span></span> <span data-ttu-id="c405f-109">Она действует так же, как учетная запись Azure Data Lake Store в учетной записи Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="c405f-109">It's equivalent to the Azure Data Lake Store account of a Data Lake Analytics account.</span></span> <span data-ttu-id="c405f-110">Переход на другую корневую папку данных аналогичен переходу на другую учетную запись хранения.</span><span class="sxs-lookup"><span data-stu-id="c405f-110">Switching to a different data-root folder is just like switching to a different store account.</span></span> <span data-ttu-id="c405f-111">Если вам нужен доступ к данным, которые совместно используются различными корневыми папками данных, следует использовать в скриптах абсолютные пути</span><span class="sxs-lookup"><span data-stu-id="c405f-111">If you want to access commonly shared data with different data-root folders, you must use absolute paths in your scripts.</span></span> <span data-ttu-id="c405f-112">или создать в корневой папке данных символические ссылки файловой системы (например, с помощью команды **mklink** для файловой системы NTFS), указывающие на совместно используемые данные.</span><span class="sxs-lookup"><span data-stu-id="c405f-112">Or, create file system symbolic links (for example, **mklink** on NTFS) under the data-root folder to point to the shared data.</span></span>

<span data-ttu-id="c405f-113">Корневая папка данных используется в следующих целях.</span><span class="sxs-lookup"><span data-stu-id="c405f-113">The data-root folder is used to:</span></span>

- <span data-ttu-id="c405f-114">Хранение метаданных, включая базы данных, таблицы, функции с табличным значением (TVF) и сборки.</span><span class="sxs-lookup"><span data-stu-id="c405f-114">Store metadata, including databases, tables, table-valued functions (TVFs), and assemblies.</span></span>
- <span data-ttu-id="c405f-115">Поиск путей ввода-вывода, которые определяются как относительные пути в U-SQL.</span><span class="sxs-lookup"><span data-stu-id="c405f-115">Look up the input and output paths that are defined as relative paths in U-SQL.</span></span> <span data-ttu-id="c405f-116">Использование относительных путей упрощает развертывание проектов U-SQL в Azure.</span><span class="sxs-lookup"><span data-stu-id="c405f-116">Using relative paths makes it easier to deploy your U-SQL projects to Azure.</span></span>

<span data-ttu-id="c405f-117">В скриптах U-SQL можно использовать как относительные, так и абсолютные локальные пути.</span><span class="sxs-lookup"><span data-stu-id="c405f-117">You can use both a relative path and a local absolute path in U-SQL scripts.</span></span> <span data-ttu-id="c405f-118">Относительный путь задается относительно пути к выбранной корневой папке данных.</span><span class="sxs-lookup"><span data-stu-id="c405f-118">The relative path is relative to the specified data-root folder path.</span></span> <span data-ttu-id="c405f-119">Мы советуем использовать в качестве разделителя пути символ "/", чтобы обеспечить совместимость скриптов с выполнением на стороне сервера.</span><span class="sxs-lookup"><span data-stu-id="c405f-119">We recommend that you use "/" as the path separator to make your scripts compatible with the server side.</span></span> <span data-ttu-id="c405f-120">Ниже приведены некоторые примеры относительных путей и их абсолютные эквиваленты.</span><span class="sxs-lookup"><span data-stu-id="c405f-120">Here are some examples of relative paths and their equivalent absolute paths.</span></span> <span data-ttu-id="c405f-121">В этих примерах предполагается, что мы используем корневую папку данных C:\LocalRunDataRoot.</span><span class="sxs-lookup"><span data-stu-id="c405f-121">In these examples, C:\LocalRunDataRoot is the data-root folder.</span></span>

|<span data-ttu-id="c405f-122">Относительный путь</span><span class="sxs-lookup"><span data-stu-id="c405f-122">Relative path</span></span>|<span data-ttu-id="c405f-123">Абсолютный путь</span><span class="sxs-lookup"><span data-stu-id="c405f-123">Absolute path</span></span>|
|-------------|-------------|
|<span data-ttu-id="c405f-124">/abc/def/input.csv</span><span class="sxs-lookup"><span data-stu-id="c405f-124">/abc/def/input.csv</span></span> |<span data-ttu-id="c405f-125">C:\LocalRunDataRoot\abc\def\input.csv</span><span class="sxs-lookup"><span data-stu-id="c405f-125">C:\LocalRunDataRoot\abc\def\input.csv</span></span>|
|<span data-ttu-id="c405f-126">abc/def/input.csv</span><span class="sxs-lookup"><span data-stu-id="c405f-126">abc/def/input.csv</span></span>  |<span data-ttu-id="c405f-127">C:\LocalRunDataRoot\abc\def\input.csv</span><span class="sxs-lookup"><span data-stu-id="c405f-127">C:\LocalRunDataRoot\abc\def\input.csv</span></span>|
|<span data-ttu-id="c405f-128">D:/abc/def/input.csv</span><span class="sxs-lookup"><span data-stu-id="c405f-128">D:/abc/def/input.csv</span></span> |<span data-ttu-id="c405f-129">D:\abc\def\input.csv</span><span class="sxs-lookup"><span data-stu-id="c405f-129">D:\abc\def\input.csv</span></span>|

## <a name="use-local-run-from-visual-studio"></a><span data-ttu-id="c405f-130">Локальное выполнение из Visual Studio</span><span class="sxs-lookup"><span data-stu-id="c405f-130">Use local run from Visual Studio</span></span>

<span data-ttu-id="c405f-131">Средства Data Lake для Visual Studio предоставляют возможность локального выполнения U-SQL в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="c405f-131">Data Lake Tools for Visual Studio provides a U-SQL local-run experience in Visual Studio.</span></span> <span data-ttu-id="c405f-132">Это позволит вам:</span><span class="sxs-lookup"><span data-stu-id="c405f-132">By using this feature, you can:</span></span>

- <span data-ttu-id="c405f-133">локально запускать скрипты U-SQL вместе со сборками C#;</span><span class="sxs-lookup"><span data-stu-id="c405f-133">Run a U-SQL script locally, along with C# assemblies.</span></span>
- <span data-ttu-id="c405f-134">локально выполнять отладку сборок C#;</span><span class="sxs-lookup"><span data-stu-id="c405f-134">Debug a C# assembly locally.</span></span>
- <span data-ttu-id="c405f-135">создавать, просматривать и удалять каталоги U-SQL (локальные базы данных, сборки, схемы и таблицы) с помощью обозревателя сервера.</span><span class="sxs-lookup"><span data-stu-id="c405f-135">Create, view, and delete U-SQL catalogs (local databases, assemblies, schemas, and tables) from Server Explorer.</span></span> <span data-ttu-id="c405f-136">Локальный каталог также можно найти с помощью обозревателя сервера.</span><span class="sxs-lookup"><span data-stu-id="c405f-136">You can also find the local catalog also from Server Explorer.</span></span>

    ![Локальный каталог для локального выполнения средств Data Lake для Visual Studio](./media/data-lake-analytics-data-lake-tools-local-run/data-lake-tools-for-visual-studio-local-run-local-catalog.png)

<span data-ttu-id="c405f-138">Установщик средств Data Lake создает папку C:\LocalRunRoot, которая по умолчанию используется в качестве корневой папки данных.</span><span class="sxs-lookup"><span data-stu-id="c405f-138">The Data Lake Tools installer creates a C:\LocalRunRoot folder to be used as the default data-root folder.</span></span> <span data-ttu-id="c405f-139">По умолчанию для локального выполнения используется коэффициент параллелизма 1.</span><span class="sxs-lookup"><span data-stu-id="c405f-139">The default local-run parallelism is 1.</span></span>

### <a name="to-configure-local-run-in-visual-studio"></a><span data-ttu-id="c405f-140">Настройка локального выполнения в Visual Studio</span><span class="sxs-lookup"><span data-stu-id="c405f-140">To configure local run in Visual Studio</span></span>

1. <span data-ttu-id="c405f-141">Откройте Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="c405f-141">Open Visual Studio.</span></span>
2. <span data-ttu-id="c405f-142">Откройте **обозреватель сервера**.</span><span class="sxs-lookup"><span data-stu-id="c405f-142">Open **Server Explorer**.</span></span>
3. <span data-ttu-id="c405f-143">Разверните узлы **Azure** > **Data Lake Analytics**.</span><span class="sxs-lookup"><span data-stu-id="c405f-143">Expand **Azure** > **Data Lake Analytics**.</span></span>
4. <span data-ttu-id="c405f-144">Откройте меню **Data Lake** и выберите пункт **Параметры и настройки**.</span><span class="sxs-lookup"><span data-stu-id="c405f-144">Click the **Data Lake** menu, and then click **Options and Settings**.</span></span>
5. <span data-ttu-id="c405f-145">В дереве слева разверните узел **Azure Data Lake**, а затем — **Общие**.</span><span class="sxs-lookup"><span data-stu-id="c405f-145">In the left tree, expand **Azure Data Lake**, and then expand **General**.</span></span>

    ![Настройка параметров для локального выполнения средств Data Lake для Visual Studio](./media/data-lake-analytics-data-lake-tools-local-run/data-lake-tools-for-visual-studio-local-run-configure.png)

<span data-ttu-id="c405f-147">Для локального выполнения требуется создать проект U-SQL для Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="c405f-147">A Visual Studio U-SQL project is required for performing local run.</span></span> <span data-ttu-id="c405f-148">Эта часть выполняется не так, как при запуске скриптов U-SQL в Azure.</span><span class="sxs-lookup"><span data-stu-id="c405f-148">This part is different from running U-SQL scripts from Azure.</span></span>

### <a name="to-run-a-u-sql-script-locally"></a><span data-ttu-id="c405f-149">Локальное выполнение скрипта U-SQL</span><span class="sxs-lookup"><span data-stu-id="c405f-149">To run a U-SQL script locally</span></span>
1. <span data-ttu-id="c405f-150">В Visual Studio откройте нужный проект U-SQL.</span><span class="sxs-lookup"><span data-stu-id="c405f-150">From Visual Studio, open your U-SQL project.</span></span>   
2. <span data-ttu-id="c405f-151">В обозревателе решений щелкните правой кнопкой мыши скрипт U-SQL и выберите команду **Submit Script** (Отправить скрипт).</span><span class="sxs-lookup"><span data-stu-id="c405f-151">Right-click a U-SQL script in Solution Explorer, and then click **Submit Script**.</span></span>
3. <span data-ttu-id="c405f-152">Выберите **(Local)** в качестве учетной записи аналитики для локального выполнения скрипта.</span><span class="sxs-lookup"><span data-stu-id="c405f-152">Select **(Local)** as the Analytics account to run your script locally.</span></span>
<span data-ttu-id="c405f-153">Можно также щелкнуть учетную запись **(Local)** в верхней части окна скрипта, а затем нажать кнопку **Отправить** (или использовать клавиши CTRL+F5).</span><span class="sxs-lookup"><span data-stu-id="c405f-153">You can also click the **(Local)** account on the top of script window, and then click **Submit** (or use the Ctrl + F5 keyboard shortcut).</span></span>

    ![Отправка заданий для локального выполнения средств Data Lake для Visual Studio](./media/data-lake-analytics-data-lake-tools-local-run/data-lake-tools-for-visual-studio-local-run-submit-job.png)

### <a name="debug-scripts-and-c-assemblies-locally"></a><span data-ttu-id="c405f-155">Локальная отладка скриптов и сборок C#</span><span class="sxs-lookup"><span data-stu-id="c405f-155">Debug scripts and C# assemblies locally</span></span>

<span data-ttu-id="c405f-156">Можно выполнять отладку сборок C# без их отправки и регистрации в службе Azure Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="c405f-156">You can debug C# assemblies without submitting and registering it to Azure Data Lake Analytics Service.</span></span> <span data-ttu-id="c405f-157">Точки останова можно установить в файле кода и в ссылочном проекте C#.</span><span class="sxs-lookup"><span data-stu-id="c405f-157">You can set breakpoints in both the code behind file and in a referenced C# project.</span></span>

#### <a name="to-debug-local-code-in-code-behind-file"></a><span data-ttu-id="c405f-158">Отладка локального кода в файле кода</span><span class="sxs-lookup"><span data-stu-id="c405f-158">To debug local code in code behind file</span></span>

1. <span data-ttu-id="c405f-159">Установите точки останова в файле кода.</span><span class="sxs-lookup"><span data-stu-id="c405f-159">Set breakpoints in the code behind file.</span></span>
2. <span data-ttu-id="c405f-160">Нажмите клавишу F5 для запуска локальной отладки сценария.</span><span class="sxs-lookup"><span data-stu-id="c405f-160">Press F5 to debug the script locally.</span></span>

> [!NOTE]
   > <span data-ttu-id="c405f-161">Следующая процедура работает только в Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="c405f-161">The following procedure only works in Visual Studio 2015.</span></span> <span data-ttu-id="c405f-162">В более ранних версиях Visual Studio необходимо вручную добавить PDB-файлы.</span><span class="sxs-lookup"><span data-stu-id="c405f-162">In older Visual Studio you may need to manually add the pdb files.</span></span>  
   >
   >

#### <a name="to-debug-local-code-in-a-referenced-c-project"></a><span data-ttu-id="c405f-163">Отладка локального кода в указанном проекте C#</span><span class="sxs-lookup"><span data-stu-id="c405f-163">To debug local code in a referenced C# project</span></span>

1. <span data-ttu-id="c405f-164">Создайте проект сборки C# и постройте его для создания выходной библиотеки DLL.</span><span class="sxs-lookup"><span data-stu-id="c405f-164">Create a C# Assembly project, and build it to generate the output dll.</span></span>
2. <span data-ttu-id="c405f-165">Зарегистрируйте библиотеку DLL с помощью инструкции U-SQL:</span><span class="sxs-lookup"><span data-stu-id="c405f-165">Register the dll using a U-SQL statement:</span></span>

        CREATE ASSEMBLY assemblyname FROM @"..\..\path\to\output\.dll";
        
3. <span data-ttu-id="c405f-166">Установите точки останова в коде C#.</span><span class="sxs-lookup"><span data-stu-id="c405f-166">Set breakpoints in the C# code.</span></span>
4. <span data-ttu-id="c405f-167">Нажмите клавишу F5 для локальной отладки сценария со ссылками на библиотеку DLL C#.</span><span class="sxs-lookup"><span data-stu-id="c405f-167">Press F5 to debug the script with referencing the C# dll locally.</span></span>

## <a name="use-local-run-from-the-data-lake-u-sql-sdk"></a><span data-ttu-id="c405f-168">Использование локального выполнения из пакета SDK U-SQL для Data Lake</span><span class="sxs-lookup"><span data-stu-id="c405f-168">Use local run from the Data Lake U-SQL SDK</span></span>

<span data-ttu-id="c405f-169">Для локального выполнения скриптов U-SQL можно использовать не только Visual Studio, но и пакет SDK U-SQL для Azure Data Lake. В последнем случае используется интерфейс командной строки или программные интерфейсы.</span><span class="sxs-lookup"><span data-stu-id="c405f-169">In addition to running U-SQL scripts locally by using Visual Studio, you can use the Azure Data Lake U-SQL SDK to run U-SQL scripts locally with command-line and programming interfaces.</span></span> <span data-ttu-id="c405f-170">Это позволяет масштабировать сценарии локального тестирования U-SQL.</span><span class="sxs-lookup"><span data-stu-id="c405f-170">Through these, you can scale your U-SQL local test.</span></span>

<span data-ttu-id="c405f-171">Узнайте больше о [пакете SDK Azure Data Lake для U-SQL](data-lake-analytics-u-sql-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="c405f-171">Learn more about [Azure Data Lake U-SQL SDK](data-lake-analytics-u-sql-sdk.md).</span></span>


## <a name="next-steps"></a><span data-ttu-id="c405f-172">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="c405f-172">Next steps</span></span>

* <span data-ttu-id="c405f-173">Более сложный запрос см. в руководстве [Анализ журналов веб-сайта с помощью службы Azure Data Lake Analytics](data-lake-analytics-analyze-weblogs.md).</span><span class="sxs-lookup"><span data-stu-id="c405f-173">To see a more complex query, see [Analyze website logs using Azure Data Lake Analytics](data-lake-analytics-analyze-weblogs.md).</span></span>
* <span data-ttu-id="c405f-174">Для просмотра сведений о заданиях см. статью [Использование браузера и представления для заданий Azure Data Lake Analytics](data-lake-analytics-data-lake-tools-view-jobs.md).</span><span class="sxs-lookup"><span data-stu-id="c405f-174">To view job details, see [Use Job Browser and Job View for Azure Data Lake Analytics jobs](data-lake-analytics-data-lake-tools-view-jobs.md).</span></span>
* <span data-ttu-id="c405f-175">Дополнительные сведения см. в статье [Использование представления выполнения вершин в инструментах Data Lake для Visual Studio](data-lake-analytics-data-lake-tools-use-vertex-execution-view.md).</span><span class="sxs-lookup"><span data-stu-id="c405f-175">To use the vertex execution view, see [Use the Vertex Execution View in Data Lake Tools for Visual Studio](data-lake-analytics-data-lake-tools-use-vertex-execution-view.md).</span></span>
