---
title: "задания aaaDebug U-SQL | Документы Microsoft"
description: "Узнайте, как toodebug U-SQL не удалось вершин, с помощью Visual Studio."
services: data-lake-analytics
documentationcenter: 
author: saveenr
manager: jhubbard
editor: cgronlun
ms.assetid: bcd0b01e-1755-4112-8e8a-a5cabdca4df2
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 09/02/2016
ms.author: saveenr
ms.openlocfilehash: 092bffa1a59ed91c5837402d0276447480b923fe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="debug-user-defined-c-code-for-failed-u-sql-jobs"></a><span data-ttu-id="b941f-103">Отладка определяемого пользователем кода C# для заданий U-SQL, завершившихся сбоем</span><span class="sxs-lookup"><span data-stu-id="b941f-103">Debug user-defined C# code for failed U-SQL jobs</span></span>

<span data-ttu-id="b941f-104">U-SQL предоставляет модель расширяемости, с помощью C#, поэтому можно написать код tooadd функциональные возможности по работе как пользовательские средства извлечения или редуктора.</span><span class="sxs-lookup"><span data-stu-id="b941f-104">U-SQL provides an extensibility model using C#, so you can write your code tooadd functionality such as a custom extractor or reducer.</span></span> <span data-ttu-id="b941f-105">toolearn более, в разделе [руководство программирования U-SQL](https://docs.microsoft.com/en-us/azure/data-lake-analytics/data-lake-analytics-u-sql-programmability-guide#use-user-defined-functions-udf).</span><span class="sxs-lookup"><span data-stu-id="b941f-105">toolearn more, see [U-SQL programmability guide](https://docs.microsoft.com/en-us/azure/data-lake-analytics/data-lake-analytics-u-sql-programmability-guide#use-user-defined-functions-udf).</span></span> <span data-ttu-id="b941f-106">Но, как показывает практика, разработка без ошибок невозможна, а отладка в системах больших данных затруднена, так как многие системы предоставляют достаточно ограниченный набор отладочных сведений о среде, таких как журналы.</span><span class="sxs-lookup"><span data-stu-id="b941f-106">In practice any code may need debugging, and big data systems may only provide limited runtime debugging information such as log files.</span></span>

<span data-ttu-id="b941f-107">Средства Озера данных Azure для Visual Studio предоставляет средство, называемое **не удалось выполнить отладку вершин**, которая позволяет клонировать невыполненного задания с локального компьютера hello облака tooyour для отладки.</span><span class="sxs-lookup"><span data-stu-id="b941f-107">Azure Data Lake Tools for Visual Studio provides a feature called **Failed Vertex Debug**, which lets you clone a failed job from hello cloud tooyour local machine for debugging.</span></span> <span data-ttu-id="b941f-108">локальный клон Hello захватывает hello всей облачной среды, включая все входные данные и пользовательского кода.</span><span class="sxs-lookup"><span data-stu-id="b941f-108">hello local clone captures hello entire cloud environment, including any input data and user code.</span></span>

<span data-ttu-id="b941f-109">Hello следующем видео показано, как сбой отладки вершин в средствах Озера данных Azure для Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="b941f-109">hello following video demonstrates Failed Vertex Debug in Azure Data Lake Tools for Visual Studio.</span></span>

> [!VIDEO https://e0d1.wpc.azureedge.net/80E0D1/OfficeMixProdMediaBlobStorage/asset-d3aeab42-6149-4ecc-b044-aa624901ab32/b0fc0373c8f94f1bb8cd39da1310adb8.mp4?sv=2012-02-12&sr=c&si=a91fad76-cfdd-4513-9668-483de39e739c&sig=K%2FR%2FdnIi9S6P%2FBlB3iLAEV5pYu6OJFBDlQy%2FQtZ7E7M%3D&se=2116-07-19T09:27:30Z&rscd=attachment%3B%20filename%3DDebugyourcustomcodeinUSQLADLA.mp4]
>

> [!NOTE]
> <span data-ttu-id="b941f-110">Visual Studio требуется hello, следующие два обновления, если они еще не установлены: [Microsoft Visual C++ 2015 распространяемый пакет обновления 3](https://www.microsoft.com/en-us/download/details.aspx?id=53840) и [универсальных C времени выполнения для приложений Windows](https://www.microsoft.com/download/details.aspx?id=50410).</span><span class="sxs-lookup"><span data-stu-id="b941f-110">Visual Studio requires hello following two updates, if they are not already installed: [Microsoft Visual C++ 2015 Redistributable Update 3](https://www.microsoft.com/en-us/download/details.aspx?id=53840) and the [Universal C Runtime for Windows](https://www.microsoft.com/download/details.aspx?id=50410).</span></span>

## <a name="download-failed-vertex-toolocal-machine"></a><span data-ttu-id="b941f-111">Не удалось загрузить вершин toolocal машины</span><span class="sxs-lookup"><span data-stu-id="b941f-111">Download failed vertex toolocal machine</span></span>

<span data-ttu-id="b941f-112">При открытии сбоя задания в средствах Озера данных Azure для Visual Studio, появится желтая панель оповещений с помощью подробных сообщений об ошибках во вкладке "Ошибка" hello.</span><span class="sxs-lookup"><span data-stu-id="b941f-112">When you open a failed job in Azure Data Lake Tools for Visual Studio, you see a yellow alert bar with detailed error messages in hello error tab.</span></span>

1. <span data-ttu-id="b941f-113">Нажмите кнопку **загрузки** toodownload hello все необходимые ресурсы и входные потоки.</span><span class="sxs-lookup"><span data-stu-id="b941f-113">Click **Download** toodownload all hello required resources and input streams.</span></span> <span data-ttu-id="b941f-114">Если hello загрузка не завершена, нажмите кнопку **повторите**.</span><span class="sxs-lookup"><span data-stu-id="b941f-114">If hello download doesn't complete, click **Retry**.</span></span>

2. <span data-ttu-id="b941f-115">Нажмите кнопку **откройте** после завершения загрузки hello toogenerate локальной среде отладки.</span><span class="sxs-lookup"><span data-stu-id="b941f-115">Click **Open** after hello download completes toogenerate a local debugging environment.</span></span> <span data-ttu-id="b941f-116">Будет создан и автоматически открыт новый экземпляр Visual Studio с решением для отладки.</span><span class="sxs-lookup"><span data-stu-id="b941f-116">A new Visual Studio instance with a debugging solution is automatically created and opened.</span></span>

![Azure Data Lake Analytics U-SQL отладка visual studio скачивание вершины](./media/data-lake-analytics-debug-u-sql-jobs/data-lake-analytics-download-vertex.png)

<span data-ttu-id="b941f-118">Задания могут содержать файлы исходного кода или зарегистрированные сборки, и действия по отладке для этих двух типов различаются.</span><span class="sxs-lookup"><span data-stu-id="b941f-118">Jobs may include code-behind source files or registered assemblies, and these two types have different debugging scenarios.</span></span>

- [<span data-ttu-id="b941f-119">Отладка невыполненного задания с кодом программной части</span><span class="sxs-lookup"><span data-stu-id="b941f-119">Debug a failed job with code-behind</span></span>](#debug-job-failed-with-code-behind)
- [<span data-ttu-id="b941f-120">Отладка невыполненного задания со сборками</span><span class="sxs-lookup"><span data-stu-id="b941f-120">Debug a failed job with assemblies</span></span>](#debug-job-failed-with-assemblies)


## <a name="debug-job-failed-with-code-behind"></a><span data-ttu-id="b941f-121">Отладка невыполненного задания с кодом программной части</span><span class="sxs-lookup"><span data-stu-id="b941f-121">Debug job failed with code-behind</span></span>

<span data-ttu-id="b941f-122">Если U-SQL происходит сбой операции, а задание hello содержится пользовательский код (обычно называется `Script.usql.cs` в проекте U-SQL), что исходный код импортируется в hello при отладке решения.</span><span class="sxs-lookup"><span data-stu-id="b941f-122">If a U-SQL job fails, and hello job includes user code (typically named `Script.usql.cs` in a U-SQL project), that source code is imported into hello debugging solution.</span></span>  <span data-ttu-id="b941f-123">Здесь можно использовать hello hello Visual Studio отладки средства (Контрольные значения, переменные, т. д.) tootroubleshoot проблему.</span><span class="sxs-lookup"><span data-stu-id="b941f-123">From there you can use hello Visual Studio debugging tools (watch, variables, etc.) tootroubleshoot hello problem.</span></span>

> [!NOTE]
> <span data-ttu-id="b941f-124">Перед отладкой, быть убедиться, что toocheck **исключения среды CLR** в параметры исключений окно hello (**Ctrl + Alt + E**).</span><span class="sxs-lookup"><span data-stu-id="b941f-124">Before debugging, be sure toocheck **Common Language Runtime Exceptions** in hello Exception Settings window (**Ctrl + Alt + E**).</span></span>

![Azure Data Lake Analytics U-SQL отладка visual studio настройка](./media/data-lake-analytics-debug-u-sql-jobs/data-lake-analytics-clr-exception-setting.png)

1. <span data-ttu-id="b941f-126">Нажмите клавишу **F5** toorun hello фонового кода.</span><span class="sxs-lookup"><span data-stu-id="b941f-126">Press **F5** toorun hello code-behind code.</span></span> <span data-ttu-id="b941f-127">Он будет выполняться до тех пор, пока не возникнет исключение.</span><span class="sxs-lookup"><span data-stu-id="b941f-127">It will run until it is stopped by an exception.</span></span>

2. <span data-ttu-id="b941f-128">Откройте hello `ADLTool_Codebehind.usql.cs` файла и задавать точки останова, затем нажмите клавишу **F5** кода hello toodebug шаг за шагом.</span><span class="sxs-lookup"><span data-stu-id="b941f-128">Open hello `ADLTool_Codebehind.usql.cs` file and set breakpoints, then press **F5** toodebug hello code step by step.</span></span>

    ![Исключение при отладке U-SQL в Azure Data Lake Analytics](./media/data-lake-analytics-debug-u-sql-jobs/data-lake-analytics-debug-exception.png)

## <a name="debug-job-failed-with-assemblies"></a><span data-ttu-id="b941f-130">Отладка невыполненного задания со сборками</span><span class="sxs-lookup"><span data-stu-id="b941f-130">Debug job failed with assemblies</span></span>

<span data-ttu-id="b941f-131">При использовании зарегистрированных сборок в ваш скрипт U-SQL hello системы не удается получить исходный код hello автоматически.</span><span class="sxs-lookup"><span data-stu-id="b941f-131">If you use registered assemblies in your U-SQL script, hello system can't get hello source code automatically.</span></span> <span data-ttu-id="b941f-132">В этом случае следует вручную добавьте hello сборки исходного кода файлы toohello решения.</span><span class="sxs-lookup"><span data-stu-id="b941f-132">In this case, manually add hello assemblies' source code files toohello solution.</span></span>

### <a name="configure-hello-solution"></a><span data-ttu-id="b941f-133">Настройка решения hello</span><span class="sxs-lookup"><span data-stu-id="b941f-133">Configure hello solution</span></span>

1. <span data-ttu-id="b941f-134">Щелкните правой кнопкой мыши **решения «VertexDebug» > Добавить > существующий проект...**  toofind hello сборок исходного кода и добавьте toohello проекта hello отладки решения.</span><span class="sxs-lookup"><span data-stu-id="b941f-134">Right-click **Solution 'VertexDebug' > Add > Existing Project...** toofind hello assemblies' source code and add hello project toohello debugging solution.</span></span>

    ![Добавление проекта при отладке U-SQL в Azure Data Lake Analytics](./media/data-lake-analytics-debug-u-sql-jobs/data-lake-analytics-add-project-to-debug-solution.png)

2. <span data-ttu-id="b941f-136">Щелкните правой кнопкой мыши **LocalVertexHost > свойства** в решение и скопируйте hello hello **рабочий каталог** пути.</span><span class="sxs-lookup"><span data-stu-id="b941f-136">Right-click **LocalVertexHost > Properties** in hello solution and copy hello **Working Directory** path.</span></span>

3. <span data-ttu-id="b941f-137">Щелкните правой кнопкой мыши **проект исходного кода сборки > свойства**выберите hello **построения** вкладки в левой части и вставьте путь hello копируются как **выходных данных > выходной путь**.</span><span class="sxs-lookup"><span data-stu-id="b941f-137">Right-Click **assembly source code project > Properties**, select hello **Build** tab at left, and paste hello copied path as **Output > Output path**.</span></span>

    ![Настройка пути pdb при отладке U-SQL в Azure Data Lake Analytics](./media/data-lake-analytics-debug-u-sql-jobs/data-lake-analytics-set-pdb-path.png)

4. <span data-ttu-id="b941f-139">Нажмите клавиши **Ctrl+Alt+E** и проверьте **Исключения среды CLR** в окне параметров исключений.</span><span class="sxs-lookup"><span data-stu-id="b941f-139">Press **Ctrl + Alt + E**, check **Common Language Runtime Exceptions** in Exception Settings window.</span></span>

### <a name="start-debug"></a><span data-ttu-id="b941f-140">Запуск отладки</span><span class="sxs-lookup"><span data-stu-id="b941f-140">Start debug</span></span>

1. <span data-ttu-id="b941f-141">Щелкните правой кнопкой мыши **проект исходного кода сборки > Перестроить** toooutput .pdb файлы toohello `LocalVertexHost` рабочий каталог.</span><span class="sxs-lookup"><span data-stu-id="b941f-141">Right-click **assembly source code project > Rebuild** toooutput .pdb files toohello `LocalVertexHost` working directory.</span></span>

2. <span data-ttu-id="b941f-142">Нажмите клавишу **F5** и hello проект будет выполняться, пока она остановлена в результате исключения.</span><span class="sxs-lookup"><span data-stu-id="b941f-142">Press **F5** and hello project will run until it is stopped by an exception.</span></span> <span data-ttu-id="b941f-143">Может появиться следующая предупреждение, можно не обращать внимания hello.</span><span class="sxs-lookup"><span data-stu-id="b941f-143">You may see hello following warning message, which you can safely ignore.</span></span> <span data-ttu-id="b941f-144">Он может занять tooa минут tooget toohello отладки экрана.</span><span class="sxs-lookup"><span data-stu-id="b941f-144">It can take up tooa minute tooget toohello debug screen.</span></span>

    ![Azure Data Lake Analytics U-SQL отладка visual studio предупреждение](./media/data-lake-analytics-debug-u-sql-jobs/data-lake-analytics-visual-studio-u-sql-debug-warning.png)

3. <span data-ttu-id="b941f-146">Откройте исходный код и задавать точки останова, затем нажмите клавишу **F5** кода hello toodebug шаг за шагом.</span><span class="sxs-lookup"><span data-stu-id="b941f-146">Open your source code and set breakpoints, then press **F5** toodebug hello code step by step.</span></span>

<span data-ttu-id="b941f-147">Можно также использовать hello hello Visual Studio отладки средства (Контрольные значения, переменные, т. д.) tootroubleshoot проблему.</span><span class="sxs-lookup"><span data-stu-id="b941f-147">You can also use hello Visual Studio debugging tools (watch, variables, etc.) tootroubleshoot hello problem.</span></span>

> [!NOTE]
> <span data-ttu-id="b941f-148">Перестройте проект исходного кода hello сборки каждый раз после изменения hello кода обновлена toogenerate PDB-файлы.</span><span class="sxs-lookup"><span data-stu-id="b941f-148">Rebuild hello assembly source code project each time after you modify hello code toogenerate updated .pdb files.</span></span>

<span data-ttu-id="b941f-149">После отладки, после успешного выполнения проекта hello hello в окне вывода отображаются hello следующие сообщения:</span><span class="sxs-lookup"><span data-stu-id="b941f-149">After debugging, if hello project completes successfully hello output window shows hello following message:</span></span>

```
hello Program 'LocalVertexHost.exe' has exited with code 0 (0x0).
```

![Успешное завершение отладки U-SQL в Azure Data Lake Analytics](./media/data-lake-analytics-debug-u-sql-jobs/data-lake-analytics-debug-succeed.png)

## <a name="resubmit-hello-job"></a><span data-ttu-id="b941f-151">Повторно отправить задания hello</span><span class="sxs-lookup"><span data-stu-id="b941f-151">Resubmit hello job</span></span>

<span data-ttu-id="b941f-152">После завершения отладки повторно отправьте hello невыполненное задание.</span><span class="sxs-lookup"><span data-stu-id="b941f-152">Once you have completed debugging, resubmit hello failed job.</span></span>

1. <span data-ttu-id="b941f-153">Для заданий с помощью решений для кода, скопируйте код C# в файл исходного кода hello (обычно `Script.usql.cs`).</span><span class="sxs-lookup"><span data-stu-id="b941f-153">For jobs with code-behind solutions, copy your C# code into hello code-behind source file (typically `Script.usql.cs`).</span></span>
2. <span data-ttu-id="b941f-154">Для заданий со сборками зарегистрируйте DLL-сборкам hello обновлен в базе данных ADLA:</span><span class="sxs-lookup"><span data-stu-id="b941f-154">For jobs with assemblies, register hello updated .dll assemblies into your ADLA database:</span></span>
    1. <span data-ttu-id="b941f-155">В обозревателе серверов или Cloud Explorer, разверните hello **ADLA учетной записи > баз данных** узла.</span><span class="sxs-lookup"><span data-stu-id="b941f-155">From Server Explorer or Cloud Explorer, expand hello **ADLA account > Databases** node.</span></span>
    2. <span data-ttu-id="b941f-156">Щелкните правой кнопкой мыши **сборки** и зарегистрировать новый DLL-файл сборки в базе данных ADLA hello: ![отладки Azure аналитика Озера данных U-SQL регистрации сборки](./media/data-lake-analytics-debug-u-sql-jobs/data-lake-analytics-register-assembly.png)</span><span class="sxs-lookup"><span data-stu-id="b941f-156">Right-click **Assemblies** and register your new .dll assemblies with hello ADLA database: ![Azure Data Lake Analytics U-SQL debug register assembly](./media/data-lake-analytics-debug-u-sql-jobs/data-lake-analytics-register-assembly.png)</span></span>
3. <span data-ttu-id="b941f-157">Повторно отправьте задание.</span><span class="sxs-lookup"><span data-stu-id="b941f-157">Resubmit your job.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b941f-158">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="b941f-158">Next steps</span></span>

- [<span data-ttu-id="b941f-159">Руководство по программированию U-SQL</span><span class="sxs-lookup"><span data-stu-id="b941f-159">U-SQL programmability guide</span></span>](data-lake-analytics-u-sql-programmability-guide.md)
- [<span data-ttu-id="b941f-160">Разработка определяемых пользователем операторов U-SQL для заданий аналитики озера данных Azure</span><span class="sxs-lookup"><span data-stu-id="b941f-160">Develop U-SQL User-defined operators for Azure Data Lake Analytics jobs</span></span>](data-lake-analytics-u-sql-develop-user-defined-operators.md)
- [<span data-ttu-id="b941f-161">Учебник. Разработка скриптов U-SQL с помощью средств озера данных для Visual Studio</span><span class="sxs-lookup"><span data-stu-id="b941f-161">Tutorial: develop U-SQL scripts using Data Lake Tools for Visual Studio</span></span>](data-lake-analytics-data-lake-tools-get-started.md)
