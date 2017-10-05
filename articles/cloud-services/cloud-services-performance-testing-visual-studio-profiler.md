---
title: "Локальное профилирование облачной службы в эмуляторе вычислений | Документация Майкрософт"
services: cloud-services
description: "Анализ проблем производительности в облачных службах с помощью профилировщика Visual Studio"
documentationcenter: 
author: kraigb
manager: ghogen
editor: 
tags: 
ms.assetid: 25e40bf3-eea0-4b0b-9f4a-91ffe797f6c3
ms.service: cloud-services
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 11/18/2016
ms.author: kraigb
ms.openlocfilehash: 51c8192d8312dc5cf546b4c357aeecf6f19d56b8
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="testing-the-performance-of-a-cloud-service-locally-in-the-azure-compute-emulator-using-the-visual-studio-profiler"></a><span data-ttu-id="b39e6-103">Локальное тестирование производительности облачной службы в эмуляторе вычислений Azure с помощью профилировщика Visual Studio</span><span class="sxs-lookup"><span data-stu-id="b39e6-103">Testing the Performance of a Cloud Service Locally in the Azure Compute Emulator Using the Visual Studio Profiler</span></span>
<span data-ttu-id="b39e6-104">Для тестирования производительности облачных служб доступны разнообразные средства и методы.</span><span class="sxs-lookup"><span data-stu-id="b39e6-104">A variety of tools and techniques are available for testing the performance of cloud services.</span></span>
<span data-ttu-id="b39e6-105">При публикации облачной службы в Azure вы можете собрать в Visual Studio данные профилирования и затем проанализировать их локально, как описывается в разделе о [профилировании приложения Azure][1].</span><span class="sxs-lookup"><span data-stu-id="b39e6-105">When you publish a cloud service to Azure, you can have Visual Studio collect profiling data and then analyze it locally, as described in [Profiling an Azure Application][1].</span></span>
<span data-ttu-id="b39e6-106">Кроме того, с помощью системы диагностики можно отслеживать различные счетчики производительности, как описывается в статье [Создание и использование счетчиков производительности в приложении Azure][2].</span><span class="sxs-lookup"><span data-stu-id="b39e6-106">You can also use diagnostics to track a variety of performance counters, as described in [Using performance counters in Azure][2].</span></span>
<span data-ttu-id="b39e6-107">Также может возникнуть необходимость выполнить профилирование приложения локально в эмуляторе вычислений перед развертыванием его в облаке.</span><span class="sxs-lookup"><span data-stu-id="b39e6-107">You might also want to profile your application locally in the compute emulator before deploying it to the cloud.</span></span>

<span data-ttu-id="b39e6-108">В этой статье рассматривается метод профилирования "Выборка ЦП", который может осуществляться локально в эмуляторе.</span><span class="sxs-lookup"><span data-stu-id="b39e6-108">This article covers the CPU Sampling method of profiling, which can be done locally in the emulator.</span></span> <span data-ttu-id="b39e6-109">Выборка из ЦП — это метод профилирования, который не сильно влияет на работу среды.</span><span class="sxs-lookup"><span data-stu-id="b39e6-109">CPU sampling is a method of profiling that is not very intrusive.</span></span> <span data-ttu-id="b39e6-110">С указанным интервалом выборки профилировщик делает снимок стека вызовов.</span><span class="sxs-lookup"><span data-stu-id="b39e6-110">At a designated sampling interval, the profiler takes a snapshot of the call stack.</span></span> <span data-ttu-id="b39e6-111">Данные собираются за период времени и отображаются в отчете.</span><span class="sxs-lookup"><span data-stu-id="b39e6-111">The data is collected over a period of time, and shown in a report.</span></span> <span data-ttu-id="b39e6-112">Данный метод профилирования с высокой вероятностью указывает, где в приложении с интенсивными вычислениями затрачивается большая часть ресурсов ЦП.</span><span class="sxs-lookup"><span data-stu-id="b39e6-112">This method of profiling tends to indicate where in a computationally intensive application most of the CPU work is being done.</span></span>  <span data-ttu-id="b39e6-113">Это дает возможность сосредоточиться на "критическом пути", где приложение тратит большую часть времени.</span><span class="sxs-lookup"><span data-stu-id="b39e6-113">This gives you the opportunity to focus on the "hot path" where your application is spending the most time.</span></span>

## <a name="1-configure-visual-studio-for-profiling"></a><span data-ttu-id="b39e6-114">1. Настройка Visual Studio для профилирования</span><span class="sxs-lookup"><span data-stu-id="b39e6-114">1: Configure Visual Studio for profiling</span></span>
<span data-ttu-id="b39e6-115">Во-первых, есть несколько параметров настройки Visual Studio, которые могут быть полезны при выполнении профилирования.</span><span class="sxs-lookup"><span data-stu-id="b39e6-115">First, there are a few Visual Studio configuration options that might be helpful when profiling.</span></span> <span data-ttu-id="b39e6-116">Для работы с отчетами профилирования потребуются символы (PDB-файлы) для вашего приложения, а также символы для системных библиотек.</span><span class="sxs-lookup"><span data-stu-id="b39e6-116">To make sense of the profiling reports, you'll need symbols (.pdb files) for your application and also symbols for system libraries.</span></span> <span data-ttu-id="b39e6-117">Потребуется убедиться, что указаны доступные серверы символов.</span><span class="sxs-lookup"><span data-stu-id="b39e6-117">You'll want to make sure that you reference the available symbol servers.</span></span> <span data-ttu-id="b39e6-118">Для этого в меню **Средства** в Visual Studio выберите **Параметры**, а затем **Отладка** и **Символы**.</span><span class="sxs-lookup"><span data-stu-id="b39e6-118">To do this, on the **Tools** menu in Visual Studio, choose **Options**, then choose **Debugging**, then **Symbols**.</span></span> <span data-ttu-id="b39e6-119">Убедитесь, что в **Местоположение файла символов (PDB)**указаны серверы символов корпорации Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="b39e6-119">Make sure that Microsoft Symbol Servers is listed under **Symbol file (.pdb) locations**.</span></span>  <span data-ttu-id="b39e6-120">Также можно указать адрес http://referencesource.microsoft.com/symbols, который может содержать дополнительные файлы символов.</span><span class="sxs-lookup"><span data-stu-id="b39e6-120">You can also reference http://referencesource.microsoft.com/symbols, which might have additional symbol files.</span></span>

![Параметры "Символ"][4]

<span data-ttu-id="b39e6-122">При желании можно упростить создаваемые профилировщиком отчеты, установив флажок "Только мой код".</span><span class="sxs-lookup"><span data-stu-id="b39e6-122">If desired, you can simplify the reports that the profiler generates by setting Just My Code.</span></span> <span data-ttu-id="b39e6-123">При включенном параметре "Только мой код" стеки вызова функции упрощаются благодаря скрытию в отчетах вызовов в пределах библиотек и платформы .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="b39e6-123">With Just My Code enabled, function call stacks are simplified so that calls entirely internal to libraries and the .NET Framework are hidden from the reports.</span></span> <span data-ttu-id="b39e6-124">В меню **Средства** выберите **Параметры**.</span><span class="sxs-lookup"><span data-stu-id="b39e6-124">On the **Tools** menu, choose **Options**.</span></span> <span data-ttu-id="b39e6-125">Затем разверните узел **Средства производительности** и выберите команду **Общие**.</span><span class="sxs-lookup"><span data-stu-id="b39e6-125">Then expand the **Performance Tools** node, and choose **General**.</span></span> <span data-ttu-id="b39e6-126">Установите флажок **Включить только мой код для отчетов профилировщика**.</span><span class="sxs-lookup"><span data-stu-id="b39e6-126">Select the checkbox for **Enable Just My Code for profiler reports**.</span></span>

![Параметры "Только мой код"][17]

<span data-ttu-id="b39e6-128">Эти инструкции можно использовать как для нового, так и для существующего проекта.</span><span class="sxs-lookup"><span data-stu-id="b39e6-128">You can use these instructions with an existing project or with a new project.</span></span>  <span data-ttu-id="b39e6-129">Создавая новый проект для методов, описанных ниже, выберите проект **Облачная служба Azure** на C# и выберите **Веб-роль** и **Роль рабочего процесса**.</span><span class="sxs-lookup"><span data-stu-id="b39e6-129">If you create a new project to try the techniques described below, choose a C# **Azure Cloud Service** project, and select a **Web Role** and a **Worker Role**.</span></span>

![Роли проекта облачной службы Azure][5]

<span data-ttu-id="b39e6-131">Для целей примера добавьте в проект код, выполнение которого занимает много времени и демонстрирует очевидные проблемы с производительностью.</span><span class="sxs-lookup"><span data-stu-id="b39e6-131">For example purposes, add some code to your project that takes a lot of time and demonstrates some obvious performance problem.</span></span> <span data-ttu-id="b39e6-132">Например, добавьте в проект роли рабочего процесса следующий код:</span><span class="sxs-lookup"><span data-stu-id="b39e6-132">For example, add the following code to a worker role project:</span></span>

    public class Concatenator
    {
        public static string Concatenate(int number)
        {
            int count;
            string s = "";
            for (count = 0; count < number; count++)
            {
                s += "\n" + count.ToString();
            }
            return s;
        }
    }

<span data-ttu-id="b39e6-133">Вызовите этот код из метода RunAsync класса, производного от рабочей роли RoleEntryPoint.</span><span class="sxs-lookup"><span data-stu-id="b39e6-133">Call this code from the RunAsync method in the worker role's RoleEntryPoint-derived class.</span></span> <span data-ttu-id="b39e6-134">(Игнорируйте предупреждение о том, что метод выполняется синхронно.)</span><span class="sxs-lookup"><span data-stu-id="b39e6-134">(Ignore the warning about the method running synchronously.)</span></span>

        private async Task RunAsync(CancellationToken cancellationToken)
        {
            // TODO: Replace the following with your own logic.
            while (!cancellationToken.IsCancellationRequested)
            {
                Trace.TraceInformation("Working");
                Concatenator.Concatenate(10000);
            }
        }

<span data-ttu-id="b39e6-135">Выполните сборку и запуск облачной службы локально без отладки (Ctrl + F5) и с установленным в конфигурации решения параметром **Выпуск**.</span><span class="sxs-lookup"><span data-stu-id="b39e6-135">Build and run your cloud service locally without debugging (Ctrl+F5), with the solution configuration set to **Release**.</span></span> <span data-ttu-id="b39e6-136">Это гарантирует, что все файлы и папки будут созданы для локального запуска приложения, а также гарантирует, что запущены все эмуляторы.</span><span class="sxs-lookup"><span data-stu-id="b39e6-136">This ensures that all files and folders are created for running the application locally, and ensures that all the emulators are started.</span></span> <span data-ttu-id="b39e6-137">Из панели задач запустите пользовательский интерфейс эмулятора вычислений, чтобы проверить, запускается ли рабочая роль.</span><span class="sxs-lookup"><span data-stu-id="b39e6-137">Start the Compute Emulator UI from the taskbar to verify that your worker role is running.</span></span>

## <a name="2-attach-to-a-process"></a><span data-ttu-id="b39e6-138">2. Присоединение к процессу</span><span class="sxs-lookup"><span data-stu-id="b39e6-138">2: Attach to a process</span></span>
<span data-ttu-id="b39e6-139">Вместо профилирования приложения с помощью его запуска в интегрированной среде разработки Visual Studio 2010 необходимо присоединить профилировщик к выполняющемуся процессу.</span><span class="sxs-lookup"><span data-stu-id="b39e6-139">Instead of profiling the application by starting it from the Visual Studio 2010 IDE, you must attach the profiler to a running process.</span></span> 

<span data-ttu-id="b39e6-140">Чтобы присоединить профилировщик к процессу, в меню **Анализ** выберите **Профилировщик**, а затем — **Присоединить/отсоединить**.</span><span class="sxs-lookup"><span data-stu-id="b39e6-140">To attach the profiler to a process, on the **Analyze** menu, choose **Profiler** and **Attach/Detach**.</span></span>

![Параметр "Присоединить профиль"][6]

<span data-ttu-id="b39e6-142">Для роли рабочего процесса найдите процесс WaWorkerHost.exe.</span><span class="sxs-lookup"><span data-stu-id="b39e6-142">For a worker role, find the WaWorkerHost.exe process.</span></span>

![Процесс WaWorkerHost][7]

<span data-ttu-id="b39e6-144">Если папка проекта находится на сетевом диске, профилировщик попросит указать другое расположение для сохранения отчетов профилирования.</span><span class="sxs-lookup"><span data-stu-id="b39e6-144">If your project folder is on a network drive, the profiler will ask you to provide another location to save the profiling reports.</span></span>

 <span data-ttu-id="b39e6-145">Можно также присоединиться к веб-роли путем присоединения к WaIISHost.exe.</span><span class="sxs-lookup"><span data-stu-id="b39e6-145">You can also attach to a web role by attaching to WaIISHost.exe.</span></span>
<span data-ttu-id="b39e6-146">При наличии в приложении нескольких процессов роли рабочего процесса они идентифицируются по значению processID.</span><span class="sxs-lookup"><span data-stu-id="b39e6-146">If there are multiple worker role processes in your application, you need to use the processID to distinguish them.</span></span> <span data-ttu-id="b39e6-147">Запрос processID можно выполнить в программе путем обращения к объекту Process.</span><span class="sxs-lookup"><span data-stu-id="b39e6-147">You can query the processID programmatically by accessing the Process object.</span></span> <span data-ttu-id="b39e6-148">Например, если вы добавите этот код в метод Run класса, производного от RoleEntryPoint в роли, вы сможете просмотреть журнал в пользовательском интерфейсе эмулятора вычислений, чтобы узнать, к какому процессу подключиться.</span><span class="sxs-lookup"><span data-stu-id="b39e6-148">For example, if you add this code to the Run method of the RoleEntryPoint-derived class in a role, you can look at the log in the Compute Emulator UI to know what process to connect to.</span></span>

    var process = System.Diagnostics.Process.GetCurrentProcess();
    var message = String.Format("Process ID: {0}", process.Id);
    Trace.WriteLine(message, "Information");

<span data-ttu-id="b39e6-149">Чтобы просмотреть журнал, запустите пользовательский интерфейс эмулятора вычислений.</span><span class="sxs-lookup"><span data-stu-id="b39e6-149">To view the log, start the Compute Emulator UI.</span></span>

![Запуск пользовательского интерфейса эмулятора вычислений][8]

<span data-ttu-id="b39e6-151">Откройте окно консоли журнала роли рабочего процесса в пользовательском интерфейсе эмулятора вычислений, щелкнув строку заголовка окна консоли.</span><span class="sxs-lookup"><span data-stu-id="b39e6-151">Open the worker role log console window in the Compute Emulator UI by clicking on the console window's title bar.</span></span> <span data-ttu-id="b39e6-152">Идентификатор процесса можно найти в журнале.</span><span class="sxs-lookup"><span data-stu-id="b39e6-152">You can see the process ID in the log.</span></span>

![Просмотр идентификатора процесса][9]

<span data-ttu-id="b39e6-154">После подсоединения выполните действия в пользовательском интерфейсе приложения (при необходимости), чтобы воспроизвести сценарий.</span><span class="sxs-lookup"><span data-stu-id="b39e6-154">One you've attached, perform the steps in your application's UI (if needed) to reproduce the scenario.</span></span>

<span data-ttu-id="b39e6-155">Чтобы остановить профилирование, щелкните ссылку **Остановить профилирование** .</span><span class="sxs-lookup"><span data-stu-id="b39e6-155">When you want to stop profiling, choose the **Stop Profiling** link.</span></span>

![Параметр "Остановить профилирование"][10]

## <a name="3-view-performance-reports"></a><span data-ttu-id="b39e6-157">3. Просмотр отчетов о производительности</span><span class="sxs-lookup"><span data-stu-id="b39e6-157">3: View performance reports</span></span>
<span data-ttu-id="b39e6-158">Отображается отчет о производительности приложения.</span><span class="sxs-lookup"><span data-stu-id="b39e6-158">The performance report for your application is displayed.</span></span>

<span data-ttu-id="b39e6-159">На этом этапе профилировщик останавливает выполнение, сохраняет данные в VSP-файл и выводит отчет, показывающий анализ этих данных.</span><span class="sxs-lookup"><span data-stu-id="b39e6-159">At this point, the profiler stops executing, saves data in a .vsp file, and displays a report that shows an analysis of this data.</span></span>

![Отчет профилировщика][11]

<span data-ttu-id="b39e6-161">Если в критическом пути отображается String.wstrcpy, щелкните "Только мой код", чтобы переключиться в представление с отображением только пользовательского кода.</span><span class="sxs-lookup"><span data-stu-id="b39e6-161">If you see String.wstrcpy in the Hot Path, click on Just My Code to change the view to show user code only.</span></span>  <span data-ttu-id="b39e6-162">Если отображается String.Concat, попробуйте нажать кнопку "Показать весь код".</span><span class="sxs-lookup"><span data-stu-id="b39e6-162">If you see String.Concat, try pressing the Show All Code button.</span></span>

<span data-ttu-id="b39e6-163">Вы увидите, что метод Concatenate и String.Concat занимают большую часть времени выполнения.</span><span class="sxs-lookup"><span data-stu-id="b39e6-163">You should see the Concatenate method and String.Concat taking up a large portion of the execution time.</span></span>

![Анализ отчета][12]

<span data-ttu-id="b39e6-165">При добавлении кода сцепления строк в этой статье вы должны увидеть соответствующее предупреждение в окне "Список задач".</span><span class="sxs-lookup"><span data-stu-id="b39e6-165">If you added the string concatenation code in this article, you should see a warning in the Task List for this.</span></span> <span data-ttu-id="b39e6-166">Также вы можете увидеть предупреждение об избыточном объеме сбора мусора, что связано с числом создаваемых и подлежащих уничтожению строк.</span><span class="sxs-lookup"><span data-stu-id="b39e6-166">You may also see a warning that there is an excessive amount of garbage collection, which is due to the number of strings that are created and disposed.</span></span>

![Предупреждения о производительности][14]

## <a name="4-make-changes-and-compare-performance"></a><span data-ttu-id="b39e6-168">4. Внесение изменений и сравнение производительности</span><span class="sxs-lookup"><span data-stu-id="b39e6-168">4: Make changes and compare performance</span></span>
<span data-ttu-id="b39e6-169">Можно также сравнить производительность до и после изменения кода.</span><span class="sxs-lookup"><span data-stu-id="b39e6-169">You can also compare the performance before and after a code change.</span></span>  <span data-ttu-id="b39e6-170">Остановите выполняемый процесс и измените код таким образом, чтобы заменить операцию сцепления строк с помощью класса StringBuilder:</span><span class="sxs-lookup"><span data-stu-id="b39e6-170">Stop the running process, and edit the code to replace the string concatenation operation with the use of StringBuilder:</span></span>

    public static string Concatenate(int number)
    {
        int count;
        System.Text.StringBuilder builder = new System.Text.StringBuilder("");
        for (count = 0; count < number; count++)
        {
             builder.Append("\n" + count.ToString());
        }
        return builder.ToString();
    }

<span data-ttu-id="b39e6-171">Выполните еще один прогон, а затем сравните производительность.</span><span class="sxs-lookup"><span data-stu-id="b39e6-171">Do another performance run, and then compare the performance.</span></span> <span data-ttu-id="b39e6-172">В обозревателе производительности, если прогоны находятся в одном сеансе, достаточно выбрать оба отчета, открыть контекстное меню и нажать кнопку **Сравнить отчеты о производительности**.</span><span class="sxs-lookup"><span data-stu-id="b39e6-172">In the Performance Explorer, if the runs are in the same session, you can just select both reports, open the shortcut menu, and choose **Compare Performance Reports**.</span></span> <span data-ttu-id="b39e6-173">Если нужно выполнить сравнение с прогоном, находящимся в другом сеансе проверки производительности, откройте меню **Анализ** и выберите **Сравнить отчеты о производительности**.</span><span class="sxs-lookup"><span data-stu-id="b39e6-173">If you want to compare with a run in another performance session, open the **Analyze** menu, and choose **Compare Performance Reports**.</span></span> <span data-ttu-id="b39e6-174">В открывшемся диалоговом окне укажите оба файла.</span><span class="sxs-lookup"><span data-stu-id="b39e6-174">Specify both files in the dialog box that appears.</span></span>

![Параметр "Сравнить отчеты о производительности"][15]

<span data-ttu-id="b39e6-176">В отчетах выделены различия между двумя прогонами.</span><span class="sxs-lookup"><span data-stu-id="b39e6-176">The reports highlight differences between the two runs.</span></span>

![Сравнительный отчет][16]

<span data-ttu-id="b39e6-178">Поздравляем!</span><span class="sxs-lookup"><span data-stu-id="b39e6-178">Congratulations!</span></span> <span data-ttu-id="b39e6-179">Работа с профилировщиком начата.</span><span class="sxs-lookup"><span data-stu-id="b39e6-179">You've gotten started with the profiler.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="b39e6-180">Устранение неполадок</span><span class="sxs-lookup"><span data-stu-id="b39e6-180">Troubleshooting</span></span>
* <span data-ttu-id="b39e6-181">Убедитесь, что выполняется профилирование сборки для выпуска, и запустите без отладки.</span><span class="sxs-lookup"><span data-stu-id="b39e6-181">Make sure you are profiling a Release build and start without debugging.</span></span>
* <span data-ttu-id="b39e6-182">Если параметр "Присоединить/отсоединить" в меню профилировщика не включен, запустите мастер производительности.</span><span class="sxs-lookup"><span data-stu-id="b39e6-182">If the Attach/Detach option is not enabled on the Profiler menu, run the Performance Wizard.</span></span>
* <span data-ttu-id="b39e6-183">С помощью пользовательского интерфейса эмулятора вычислений просмотрите состояние приложения.</span><span class="sxs-lookup"><span data-stu-id="b39e6-183">Use the Compute Emulator UI to view the status of your application.</span></span> 
* <span data-ttu-id="b39e6-184">В случае возникновения неполадок с запуском приложения в эмуляторе или присоединением профилировщика завершите работу эмулятора вычислений и перезапустите его.</span><span class="sxs-lookup"><span data-stu-id="b39e6-184">If you have problems starting applications in the emulator, or attaching the profiler, shut down the compute emulator and restart it.</span></span> <span data-ttu-id="b39e6-185">Если неполадка не будет устранена, попробуйте перезагрузить компьютер.</span><span class="sxs-lookup"><span data-stu-id="b39e6-185">If that doesn't solve the problem, try rebooting.</span></span> <span data-ttu-id="b39e6-186">Это может происходить, если эмулятор вычислений используется для приостановки и удаления развертываний.</span><span class="sxs-lookup"><span data-stu-id="b39e6-186">This problem can occur if you use the Compute Emulator to suspend and remove running deployments.</span></span>
* <span data-ttu-id="b39e6-187">При использовании команд профилирования из командной строки, особенно глобальных параметров, убедитесь, что вызван VSPerfClrEnv /globaloff и завершена работа VsPerfMon.exe.</span><span class="sxs-lookup"><span data-stu-id="b39e6-187">If you have used any of the profiling commands from the command line, especially the global settings, make sure that VSPerfClrEnv /globaloff has been called and that VsPerfMon.exe has been shut down.</span></span>
* <span data-ttu-id="b39e6-188">Если в ходе выборки будет выведено сообщение "PRF0025: данные не собраны", убедитесь, что в присоединенном процессе есть загрузка ЦП.</span><span class="sxs-lookup"><span data-stu-id="b39e6-188">If when sampling, you see the message "PRF0025: No data was collected," check that the process you attached to has CPU activity.</span></span> <span data-ttu-id="b39e6-189">Приложения, которые не производят вычислений, могут не предоставлять данных для выборки.</span><span class="sxs-lookup"><span data-stu-id="b39e6-189">Applications that are not doing any computational work might not produce any sampling data.</span></span>  <span data-ttu-id="b39e6-190">Это также может быть связано с завершением процесса до начала сбора данных.</span><span class="sxs-lookup"><span data-stu-id="b39e6-190">It's also possible that the process exited before any sampling was done.</span></span> <span data-ttu-id="b39e6-191">Убедитесь, что метод Run для профилируемой роли не завершен.</span><span class="sxs-lookup"><span data-stu-id="b39e6-191">Check to see that the Run method for a role that you are profiling does not terminate.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b39e6-192">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="b39e6-192">Next Steps</span></span>
<span data-ttu-id="b39e6-193">Инструментирование двоичных файлов Azure в эмуляторе не поддерживается в профилировщике Visual Studio, но в случае, если нужно проверить распределение памяти, этот параметр можно выбрать при профилировании.</span><span class="sxs-lookup"><span data-stu-id="b39e6-193">Instrumenting Azure binaries in the emulator is not supported in the Visual Studio profiler, but if you want to test memory allocation, you can choose that option when profiling.</span></span> <span data-ttu-id="b39e6-194">Можно также выбрать параллельное профилирование — это поможет выявить затраты времени на конкурирование потоков за блокировку, или профилирование взаимодействия слоев, что поможет отслеживать проблемы с производительностью в ходе обмена данными между слоями приложения, чаще всего между уровнем данных и ролью рабочего процесса.</span><span class="sxs-lookup"><span data-stu-id="b39e6-194">You can also choose concurrency profiling, which helps you determine whether threads are wasting time competing for locks, or tier interaction profiling, which helps you track down performance problems when interacting between tiers of an application, most frequently between the data tier and a worker role.</span></span>  <span data-ttu-id="b39e6-195">Можно просмотреть запросы к базе данных, создаваемые приложением, и использовать данные профилирования для повышения эффективности работы с базой данных.</span><span class="sxs-lookup"><span data-stu-id="b39e6-195">You can view the database queries that your app generates and use the profiling data to improve your use of the database.</span></span> <span data-ttu-id="b39e6-196">Сведения о профилировании межуровневого взаимодействия см. в записи блога [Walkthrough: Using the Tier Interaction Profiler in Visual Studio Team System 2010][3] (Пошаговое руководство. Использование профилировщика межуровневого взаимодействия в Visual Studio Team System 2010).</span><span class="sxs-lookup"><span data-stu-id="b39e6-196">For information about tier interaction profiling, see the blog post [Walkthrough: Using the Tier Interaction Profiler in Visual Studio Team System 2010][3].</span></span>

[1]: http://msdn.microsoft.com/library/azure/hh369930.aspx
[2]: http://msdn.microsoft.com/library/azure/hh411542.aspx
[3]: http://blogs.msdn.com/b/habibh/archive/2009/06/30/walkthrough-using-the-tier-interaction-profiler-in-visual-studio-team-system-2010.aspx
[4]: ./media/cloud-services-performance-testing-visual-studio-profiler/ProfilingLocally09.png
[5]: ./media/cloud-services-performance-testing-visual-studio-profiler/ProfilingLocally10.png
[6]: ./media/cloud-services-performance-testing-visual-studio-profiler/ProfilingLocally02.png
[7]: ./media/cloud-services-performance-testing-visual-studio-profiler/ProfilingLocally05.png
[8]: ./media/cloud-services-performance-testing-visual-studio-profiler/ProfilingLocally010.png
[9]: ./media/cloud-services-performance-testing-visual-studio-profiler/ProfilingLocally07.png
[10]: ./media/cloud-services-performance-testing-visual-studio-profiler/ProfilingLocally06.png
[11]: ./media/cloud-services-performance-testing-visual-studio-profiler/ProfilingLocally03.png
[12]: ./media/cloud-services-performance-testing-visual-studio-profiler/ProfilingLocally011.png
[14]: ./media/cloud-services-performance-testing-visual-studio-profiler/ProfilingLocally04.png 
[15]: ./media/cloud-services-performance-testing-visual-studio-profiler/ProfilingLocally013.png
[16]: ./media/cloud-services-performance-testing-visual-studio-profiler/ProfilingLocally012.png
[17]: ./media/cloud-services-performance-testing-visual-studio-profiler/ProfilingLocally08.png
