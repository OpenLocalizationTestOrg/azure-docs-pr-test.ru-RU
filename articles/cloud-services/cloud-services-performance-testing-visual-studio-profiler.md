---
title: "Облачные службы локально в эмуляторе вычислений hello aaaProfiling | Документы Microsoft"
services: cloud-services
description: "Анализа проблем с производительностью в облачные службы с помощью профилировщика Visual Studio hello"
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
ms.openlocfilehash: fc37c85dad4db4cc0310f73afad56fc0fe5f3963
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="testing-hello-performance-of-a-cloud-service-locally-in-hello-azure-compute-emulator-using-hello-visual-studio-profiler"></a><span data-ttu-id="65db3-103">Тестирование производительности облачной службы локально hello в hello hello Azure эмуляторе вычислений с помощью профилировщика Visual Studio</span><span class="sxs-lookup"><span data-stu-id="65db3-103">Testing hello Performance of a Cloud Service Locally in hello Azure Compute Emulator Using hello Visual Studio Profiler</span></span>
<span data-ttu-id="65db3-104">Широкий набор средств и приемов доступны для тестирования производительности hello облачных служб.</span><span class="sxs-lookup"><span data-stu-id="65db3-104">A variety of tools and techniques are available for testing hello performance of cloud services.</span></span>
<span data-ttu-id="65db3-105">При публикации облачной службы tooAzure, что Visual Studio сбора данных профилирования, а затем анализировать эти данные локально, как описано в [профилирование приложения Azure][1].</span><span class="sxs-lookup"><span data-stu-id="65db3-105">When you publish a cloud service tooAzure, you can have Visual Studio collect profiling data and then analyze it locally, as described in [Profiling an Azure Application][1].</span></span>
<span data-ttu-id="65db3-106">Можно также использовать tootrack диагностики производительности широкий набор счетчиков, как описано в [использование счетчиков производительности в Azure][2].</span><span class="sxs-lookup"><span data-stu-id="65db3-106">You can also use diagnostics tootrack a variety of performance counters, as described in [Using performance counters in Azure][2].</span></span>
<span data-ttu-id="65db3-107">Можно также tooprofile перед его развертыванием toohello облачные приложения локально в эмуляторе вычислений hello.</span><span class="sxs-lookup"><span data-stu-id="65db3-107">You might also want tooprofile your application locally in hello compute emulator before deploying it toohello cloud.</span></span>

<span data-ttu-id="65db3-108">В этой статье описан метод выборки циклов ЦП hello профилирования, это можно сделать локально в эмуляторе hello.</span><span class="sxs-lookup"><span data-stu-id="65db3-108">This article covers hello CPU Sampling method of profiling, which can be done locally in hello emulator.</span></span> <span data-ttu-id="65db3-109">Выборка из ЦП — это метод профилирования, который не сильно влияет на работу среды.</span><span class="sxs-lookup"><span data-stu-id="65db3-109">CPU sampling is a method of profiling that is not very intrusive.</span></span> <span data-ttu-id="65db3-110">С интервалом выборки указанный профилировщик hello делает моментальный снимок стека вызовов hello.</span><span class="sxs-lookup"><span data-stu-id="65db3-110">At a designated sampling interval, hello profiler takes a snapshot of hello call stack.</span></span> <span data-ttu-id="65db3-111">Hello данные собираются за период времени и отображаемых в отчете.</span><span class="sxs-lookup"><span data-stu-id="65db3-111">hello data is collected over a period of time, and shown in a report.</span></span> <span data-ttu-id="65db3-112">Этот метод профилирования обычно tooindicate, где в приложении с большим объемом вычислений большую часть работы hello ЦП, проводится.</span><span class="sxs-lookup"><span data-stu-id="65db3-112">This method of profiling tends tooindicate where in a computationally intensive application most of hello CPU work is being done.</span></span>  <span data-ttu-id="65db3-113">Это дает hello toofocus возможных сделок на hello «Горячий путь», где приложение тратит hello большая часть времени.</span><span class="sxs-lookup"><span data-stu-id="65db3-113">This gives you hello opportunity toofocus on hello "hot path" where your application is spending hello most time.</span></span>

## <a name="1-configure-visual-studio-for-profiling"></a><span data-ttu-id="65db3-114">1. Настройка Visual Studio для профилирования</span><span class="sxs-lookup"><span data-stu-id="65db3-114">1: Configure Visual Studio for profiling</span></span>
<span data-ttu-id="65db3-115">Во-первых, есть несколько параметров настройки Visual Studio, которые могут быть полезны при выполнении профилирования.</span><span class="sxs-lookup"><span data-stu-id="65db3-115">First, there are a few Visual Studio configuration options that might be helpful when profiling.</span></span> <span data-ttu-id="65db3-116">Суть toomake Здравствуйте отчетов профилирования, вам потребуется символов (PDB-файлов) для вашего приложения, а также символы для системных библиотек.</span><span class="sxs-lookup"><span data-stu-id="65db3-116">toomake sense of hello profiling reports, you'll need symbols (.pdb files) for your application and also symbols for system libraries.</span></span> <span data-ttu-id="65db3-117">Будет необходимо убедиться, что ссылаться на серверы доступных символов hello toomake.</span><span class="sxs-lookup"><span data-stu-id="65db3-117">You'll want toomake sure that you reference hello available symbol servers.</span></span> <span data-ttu-id="65db3-118">toodo это на hello **средства** меню в Visual Studio выберите **параметры**, выберите **Отладка**, затем **символы**.</span><span class="sxs-lookup"><span data-stu-id="65db3-118">toodo this, on hello **Tools** menu in Visual Studio, choose **Options**, then choose **Debugging**, then **Symbols**.</span></span> <span data-ttu-id="65db3-119">Убедитесь, что в **Местоположение файла символов (PDB)**указаны серверы символов корпорации Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="65db3-119">Make sure that Microsoft Symbol Servers is listed under **Symbol file (.pdb) locations**.</span></span>  <span data-ttu-id="65db3-120">Также можно указать адрес http://referencesource.microsoft.com/symbols, который может содержать дополнительные файлы символов.</span><span class="sxs-lookup"><span data-stu-id="65db3-120">You can also reference http://referencesource.microsoft.com/symbols, which might have additional symbol files.</span></span>

![Параметры "Символ"][4]

<span data-ttu-id="65db3-122">При желании можно упростить hello сообщает создает этот профилировщик hello, задав только мой код.</span><span class="sxs-lookup"><span data-stu-id="65db3-122">If desired, you can simplify hello reports that hello profiler generates by setting Just My Code.</span></span> <span data-ttu-id="65db3-123">Только мой код стеки вызовов функции упрощены, полностью внутренней toolibraries, которая вызывает и hello .NET Framework, скрыты от hello отчеты.</span><span class="sxs-lookup"><span data-stu-id="65db3-123">With Just My Code enabled, function call stacks are simplified so that calls entirely internal toolibraries and hello .NET Framework are hidden from hello reports.</span></span> <span data-ttu-id="65db3-124">На hello **средства** меню, выберите **параметры**.</span><span class="sxs-lookup"><span data-stu-id="65db3-124">On hello **Tools** menu, choose **Options**.</span></span> <span data-ttu-id="65db3-125">Разверните hello **средства повышения производительности** узел и выберите **Общие**.</span><span class="sxs-lookup"><span data-stu-id="65db3-125">Then expand hello **Performance Tools** node, and choose **General**.</span></span> <span data-ttu-id="65db3-126">Установите флажок hello для **включить только мой код для отчетов профилировщика**.</span><span class="sxs-lookup"><span data-stu-id="65db3-126">Select hello checkbox for **Enable Just My Code for profiler reports**.</span></span>

![Параметры "Только мой код"][17]

<span data-ttu-id="65db3-128">Эти инструкции можно использовать как для нового, так и для существующего проекта.</span><span class="sxs-lookup"><span data-stu-id="65db3-128">You can use these instructions with an existing project or with a new project.</span></span>  <span data-ttu-id="65db3-129">При создании нового hello tootry проекта методик, описанных ниже, выберите C# **облачной службы Azure** проекта, а затем выберите **веб-роли** и **рабочей роли**.</span><span class="sxs-lookup"><span data-stu-id="65db3-129">If you create a new project tootry hello techniques described below, choose a C# **Azure Cloud Service** project, and select a **Web Role** and a **Worker Role**.</span></span>

![Роли проекта облачной службы Azure][5]

<span data-ttu-id="65db3-131">Например целей, добавить некоторые tooyour проекта кода, который занимает много времени и демонстрируются некоторые проблемы производительности очевидно.</span><span class="sxs-lookup"><span data-stu-id="65db3-131">For example purposes, add some code tooyour project that takes a lot of time and demonstrates some obvious performance problem.</span></span> <span data-ttu-id="65db3-132">Например добавьте следующий проект рабочей роли код tooa hello:</span><span class="sxs-lookup"><span data-stu-id="65db3-132">For example, add hello following code tooa worker role project:</span></span>

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

<span data-ttu-id="65db3-133">Этот код можно вызовите из hello RunAsync метод класса, производного от RoleEntryPoint hello рабочей роли.</span><span class="sxs-lookup"><span data-stu-id="65db3-133">Call this code from hello RunAsync method in hello worker role's RoleEntryPoint-derived class.</span></span> <span data-ttu-id="65db3-134">(Не учитывать hello предупреждение о методе hello синхронное выполнение).</span><span class="sxs-lookup"><span data-stu-id="65db3-134">(Ignore hello warning about hello method running synchronously.)</span></span>

        private async Task RunAsync(CancellationToken cancellationToken)
        {
            // TODO: Replace hello following with your own logic.
            while (!cancellationToken.IsCancellationRequested)
            {
                Trace.TraceInformation("Working");
                Concatenator.Concatenate(10000);
            }
        }

<span data-ttu-id="65db3-135">Построение и запуск облачной службы локально без отладки (Ctrl + F5), задайте слишком конфигурации решения hello**выпуска**.</span><span class="sxs-lookup"><span data-stu-id="65db3-135">Build and run your cloud service locally without debugging (Ctrl+F5), with hello solution configuration set too**Release**.</span></span> <span data-ttu-id="65db3-136">Это гарантирует, что все файлы и папки создаются для выполнения приложения hello локально и гарантирует, что запущены все Привет эмуляторы.</span><span class="sxs-lookup"><span data-stu-id="65db3-136">This ensures that all files and folders are created for running hello application locally, and ensures that all hello emulators are started.</span></span> <span data-ttu-id="65db3-137">Запустите пользовательский Интерфейс эмулятора вычислений hello из tooverify hello задач, на котором выполняется рабочей роли.</span><span class="sxs-lookup"><span data-stu-id="65db3-137">Start hello Compute Emulator UI from hello taskbar tooverify that your worker role is running.</span></span>

## <a name="2-attach-tooa-process"></a><span data-ttu-id="65db3-138">2: присоединение процесса tooa</span><span class="sxs-lookup"><span data-stu-id="65db3-138">2: Attach tooa process</span></span>
<span data-ttu-id="65db3-139">Вместо профилирования приложения hello, запустите его из hello интерфейса IDE Visual Studio 2010, необходимо присоединить hello профилировщик tooa выполнения процесса.</span><span class="sxs-lookup"><span data-stu-id="65db3-139">Instead of profiling hello application by starting it from hello Visual Studio 2010 IDE, you must attach hello profiler tooa running process.</span></span> 

<span data-ttu-id="65db3-140">tooattach hello профилировщик tooa процесса на hello **анализ** меню, выберите **профилировщик** и **подключение/отключение**.</span><span class="sxs-lookup"><span data-stu-id="65db3-140">tooattach hello profiler tooa process, on hello **Analyze** menu, choose **Profiler** and **Attach/Detach**.</span></span>

![Параметр "Присоединить профиль"][6]

<span data-ttu-id="65db3-142">Для рабочей роли найдите процесс WaWorkerHost.exe hello.</span><span class="sxs-lookup"><span data-stu-id="65db3-142">For a worker role, find hello WaWorkerHost.exe process.</span></span>

![Процесс WaWorkerHost][7]

<span data-ttu-id="65db3-144">Если вашей папки проекта находится на сетевом диске, профилировщик hello запросит tooprovide toosave hello другое расположение, отчеты профилирования.</span><span class="sxs-lookup"><span data-stu-id="65db3-144">If your project folder is on a network drive, hello profiler will ask you tooprovide another location toosave hello profiling reports.</span></span>

 <span data-ttu-id="65db3-145">Можно также присоединить tooa веб-роли путем присоединения tooWaIISHost.exe.</span><span class="sxs-lookup"><span data-stu-id="65db3-145">You can also attach tooa web role by attaching tooWaIISHost.exe.</span></span>
<span data-ttu-id="65db3-146">Если существует несколько рабочих процессов для роли в приложении, необходимо toouse hello processID toodistinguish их.</span><span class="sxs-lookup"><span data-stu-id="65db3-146">If there are multiple worker role processes in your application, you need toouse hello processID toodistinguish them.</span></span> <span data-ttu-id="65db3-147">Вы можете запрашивать hello processID программным путем при доступе к объекту процесса hello.</span><span class="sxs-lookup"><span data-stu-id="65db3-147">You can query hello processID programmatically by accessing hello Process object.</span></span> <span data-ttu-id="65db3-148">Например если добавить этот код toohello выполнения метод класса, производного от RoleEntryPoint hello в роли, можно взглянуть на журнала в пользовательский Интерфейс эмулятора вычислений tooknow hello какие tooconnect процесса для.</span><span class="sxs-lookup"><span data-stu-id="65db3-148">For example, if you add this code toohello Run method of hello RoleEntryPoint-derived class in a role, you can look at the log in hello Compute Emulator UI tooknow what process tooconnect to.</span></span>

    var process = System.Diagnostics.Process.GetCurrentProcess();
    var message = String.Format("Process ID: {0}", process.Id);
    Trace.WriteLine(message, "Information");

<span data-ttu-id="65db3-149">Журнал tooview hello, hello начала пользовательский Интерфейс эмулятора вычислений.</span><span class="sxs-lookup"><span data-stu-id="65db3-149">tooview hello log, start hello Compute Emulator UI.</span></span>

![Запустить пользовательский Интерфейс эмулятора вычислений hello][8]

<span data-ttu-id="65db3-151">Откройте окно hello рабочей роли журнала консоли в hello пользовательский Интерфейс эмулятора вычислений, щелкнув на панели заголовка окна консоли hello.</span><span class="sxs-lookup"><span data-stu-id="65db3-151">Open hello worker role log console window in hello Compute Emulator UI by clicking on hello console window's title bar.</span></span> <span data-ttu-id="65db3-152">Вы увидите идентификатор процесса hello в журнале hello.</span><span class="sxs-lookup"><span data-stu-id="65db3-152">You can see hello process ID in hello log.</span></span>

![Просмотр идентификатора процесса][9]

<span data-ttu-id="65db3-154">Который присоединен, выполните действия hello в сценарий hello tooreproduce приложения пользовательского интерфейса (при необходимости).</span><span class="sxs-lookup"><span data-stu-id="65db3-154">One you've attached, perform hello steps in your application's UI (if needed) tooreproduce hello scenario.</span></span>

<span data-ttu-id="65db3-155">При необходимости toostop профилирования выберите hello **остановить профилирование** ссылку.</span><span class="sxs-lookup"><span data-stu-id="65db3-155">When you want toostop profiling, choose hello **Stop Profiling** link.</span></span>

![Параметр "Остановить профилирование"][10]

## <a name="3-view-performance-reports"></a><span data-ttu-id="65db3-157">3. Просмотр отчетов о производительности</span><span class="sxs-lookup"><span data-stu-id="65db3-157">3: View performance reports</span></span>
<span data-ttu-id="65db3-158">отображается отчет о производительности Hello для вашего приложения.</span><span class="sxs-lookup"><span data-stu-id="65db3-158">hello performance report for your application is displayed.</span></span>

<span data-ttu-id="65db3-159">На этом этапе hello профилировщик прекращает выполнение, сохраняет данные в VSP-файл и отображает отчет, показывающий анализ этих данных.</span><span class="sxs-lookup"><span data-stu-id="65db3-159">At this point, hello profiler stops executing, saves data in a .vsp file, and displays a report that shows an analysis of this data.</span></span>

![Отчет профилировщика][11]

<span data-ttu-id="65db3-161">Если вы видите String.wstrcpy в hello критический путь, щелкнув только мой код toochange hello представление tooshow только код пользователя.</span><span class="sxs-lookup"><span data-stu-id="65db3-161">If you see String.wstrcpy in hello Hot Path, click on Just My Code toochange hello view tooshow user code only.</span></span>  <span data-ttu-id="65db3-162">Если вы видите String.Concat, попробуйте нажав кнопку "Показать все код hello".</span><span class="sxs-lookup"><span data-stu-id="65db3-162">If you see String.Concat, try pressing hello Show All Code button.</span></span>

<span data-ttu-id="65db3-163">Вы увидите метод СЦЕПИТЬ hello и String.Concat занимают большую часть времени выполнения hello.</span><span class="sxs-lookup"><span data-stu-id="65db3-163">You should see hello Concatenate method and String.Concat taking up a large portion of hello execution time.</span></span>

![Анализ отчета][12]

<span data-ttu-id="65db3-165">При добавлении кода объединения строку hello в этой статье вы увидите предупреждение в hello список задач для этого.</span><span class="sxs-lookup"><span data-stu-id="65db3-165">If you added hello string concatenation code in this article, you should see a warning in hello Task List for this.</span></span> <span data-ttu-id="65db3-166">Может также появиться предупреждение, что имеется слишком много мусора, которая наступает toohello число строк, которые создаются и удален.</span><span class="sxs-lookup"><span data-stu-id="65db3-166">You may also see a warning that there is an excessive amount of garbage collection, which is due toohello number of strings that are created and disposed.</span></span>

![Предупреждения о производительности][14]

## <a name="4-make-changes-and-compare-performance"></a><span data-ttu-id="65db3-168">4. Внесение изменений и сравнение производительности</span><span class="sxs-lookup"><span data-stu-id="65db3-168">4: Make changes and compare performance</span></span>
<span data-ttu-id="65db3-169">Вы также можете сравнить производительность hello до и после изменения кода.</span><span class="sxs-lookup"><span data-stu-id="65db3-169">You can also compare hello performance before and after a code change.</span></span>  <span data-ttu-id="65db3-170">Остановить процесс hello и изменить hello кода tooreplace hello сцепление строк с использованием hello объекта StringBuilder:</span><span class="sxs-lookup"><span data-stu-id="65db3-170">Stop hello running process, and edit hello code tooreplace hello string concatenation operation with hello use of StringBuilder:</span></span>

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

<span data-ttu-id="65db3-171">Выполните запуск другой производительности, а затем сравнить производительность hello.</span><span class="sxs-lookup"><span data-stu-id="65db3-171">Do another performance run, and then compare hello performance.</span></span> <span data-ttu-id="65db3-172">В hello Обозреватель производительности, если hello запусков находятся в hello же сеансе, просто выберите оба отчета, откройте контекстное меню hello и выберите **Сравнить отчеты о производительности**.</span><span class="sxs-lookup"><span data-stu-id="65db3-172">In hello Performance Explorer, if hello runs are in hello same session, you can just select both reports, open hello shortcut menu, and choose **Compare Performance Reports**.</span></span> <span data-ttu-id="65db3-173">Toocompare с выполнения во время другого сеанса производительности, откройте hello **анализ** меню и выберите **Сравнить отчеты о производительности**.</span><span class="sxs-lookup"><span data-stu-id="65db3-173">If you want toocompare with a run in another performance session, open hello **Analyze** menu, and choose **Compare Performance Reports**.</span></span> <span data-ttu-id="65db3-174">Укажите оба файла в диалоговом окне приветствия, отображается.</span><span class="sxs-lookup"><span data-stu-id="65db3-174">Specify both files in hello dialog box that appears.</span></span>

![Параметр "Сравнить отчеты о производительности"][15]

<span data-ttu-id="65db3-176">отчеты Hello подчеркивают различия между двумя выполнениями hello.</span><span class="sxs-lookup"><span data-stu-id="65db3-176">hello reports highlight differences between hello two runs.</span></span>

![Сравнительный отчет][16]

<span data-ttu-id="65db3-178">Поздравляем!</span><span class="sxs-lookup"><span data-stu-id="65db3-178">Congratulations!</span></span> <span data-ttu-id="65db3-179">Начала работы с профилировщиком hello.</span><span class="sxs-lookup"><span data-stu-id="65db3-179">You've gotten started with hello profiler.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="65db3-180">Устранение неполадок</span><span class="sxs-lookup"><span data-stu-id="65db3-180">Troubleshooting</span></span>
* <span data-ttu-id="65db3-181">Убедитесь, что выполняется профилирование сборки для выпуска, и запустите без отладки.</span><span class="sxs-lookup"><span data-stu-id="65db3-181">Make sure you are profiling a Release build and start without debugging.</span></span>
* <span data-ttu-id="65db3-182">Если hello присоединение и отсоединение профилировщика меню hello не включена, запустите мастер производительности hello.</span><span class="sxs-lookup"><span data-stu-id="65db3-182">If hello Attach/Detach option is not enabled on hello Profiler menu, run hello Performance Wizard.</span></span>
* <span data-ttu-id="65db3-183">Используйте пользовательский Интерфейс эмулятора вычислений hello tooview состояние hello приложения.</span><span class="sxs-lookup"><span data-stu-id="65db3-183">Use hello Compute Emulator UI tooview hello status of your application.</span></span> 
* <span data-ttu-id="65db3-184">Если возникают проблемы при запуске приложения в эмуляторе hello или присоединение hello профилировщика, завершение работы эмулятора вычислений hello и перезапустите ее.</span><span class="sxs-lookup"><span data-stu-id="65db3-184">If you have problems starting applications in hello emulator, or attaching hello profiler, shut down hello compute emulator and restart it.</span></span> <span data-ttu-id="65db3-185">Если это не устранит проблему hello, попробуйте перезагрузить.</span><span class="sxs-lookup"><span data-stu-id="65db3-185">If that doesn't solve hello problem, try rebooting.</span></span> <span data-ttu-id="65db3-186">Это может происходить, если использовать эмулятор вычислений toosuspend hello и удалить выполняемых развертываниях.</span><span class="sxs-lookup"><span data-stu-id="65db3-186">This problem can occur if you use hello Compute Emulator toosuspend and remove running deployments.</span></span>
* <span data-ttu-id="65db3-187">При использовании любого из hello профилирование команды из командной строки, особенно Здравствуйте глобальные параметры, убедитесь, что вызван VSPerfClrEnv/globaloff и что VsPerfMon.exe была завершена.</span><span class="sxs-lookup"><span data-stu-id="65db3-187">If you have used any of hello profiling commands from the command line, especially hello global settings, make sure that VSPerfClrEnv /globaloff has been called and that VsPerfMon.exe has been shut down.</span></span>
* <span data-ttu-id="65db3-188">Если при выборке данных, вы увидите сообщение hello» PRF0025: данные не собраны,» убедитесь, что процесс присоединенный toohas ЦП действие hello.</span><span class="sxs-lookup"><span data-stu-id="65db3-188">If when sampling, you see hello message "PRF0025: No data was collected," check that hello process you attached toohas CPU activity.</span></span> <span data-ttu-id="65db3-189">Приложения, которые не производят вычислений, могут не предоставлять данных для выборки.</span><span class="sxs-lookup"><span data-stu-id="65db3-189">Applications that are not doing any computational work might not produce any sampling data.</span></span>  <span data-ttu-id="65db3-190">Можно также, hello процесс завершился до любой выборки, выполненной.</span><span class="sxs-lookup"><span data-stu-id="65db3-190">It's also possible that hello process exited before any sampling was done.</span></span> <span data-ttu-id="65db3-191">Проверьте toosee, которые не прерывают hello метод Run для роли, которая выполняется профилирование.</span><span class="sxs-lookup"><span data-stu-id="65db3-191">Check toosee that hello Run method for a role that you are profiling does not terminate.</span></span>

## <a name="next-steps"></a><span data-ttu-id="65db3-192">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="65db3-192">Next Steps</span></span>
<span data-ttu-id="65db3-193">Инструментирование Azure двоичные файлы в эмуляторе hello в профилировщик Visual Studio hello не поддерживается, но если вы хотите tootest выделения памяти, можно выбрать этот параметр при профилировании.</span><span class="sxs-lookup"><span data-stu-id="65db3-193">Instrumenting Azure binaries in hello emulator is not supported in hello Visual Studio profiler, but if you want tootest memory allocation, you can choose that option when profiling.</span></span> <span data-ttu-id="65db3-194">Вы также можете профилирования с параллелизмом, которая помогает определить, ли потоков тратит время конкурирующие за блокировки или профилирование уровневого взаимодействия, что помогает отслеживать проблемы с производительностью при взаимодействии между уровнями приложения, наиболее часто между уровнем данных hello и рабочей роли.</span><span class="sxs-lookup"><span data-stu-id="65db3-194">You can also choose concurrency profiling, which helps you determine whether threads are wasting time competing for locks, or tier interaction profiling, which helps you track down performance problems when interacting between tiers of an application, most frequently between hello data tier and a worker role.</span></span>  <span data-ttu-id="65db3-195">Могут просматривать hello запросы к базе данных, приложение создает и использовать hello профилирования данных tooimprove использование hello базы данных.</span><span class="sxs-lookup"><span data-stu-id="65db3-195">You can view hello database queries that your app generates and use hello profiling data tooimprove your use of hello database.</span></span> <span data-ttu-id="65db3-196">Сведения о профилировании взаимодействия уровней см. в разделе hello записи блога [Пошаговое руководство: использование hello профилировщик уровня взаимодействия в Visual Studio Team System 2010][3].</span><span class="sxs-lookup"><span data-stu-id="65db3-196">For information about tier interaction profiling, see hello blog post [Walkthrough: Using hello Tier Interaction Profiler in Visual Studio Team System 2010][3].</span></span>

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
