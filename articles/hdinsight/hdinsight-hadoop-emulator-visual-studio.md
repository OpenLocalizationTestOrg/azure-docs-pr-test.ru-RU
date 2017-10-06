---
title: "Озеро aaaData средства для Visual Studio с песочницей Hortonworks - Azure HDInsight | Документы Microsoft"
description: "Узнайте, как toouse hello Озера данных Azure tools для Visual Studio с песочницей Hortonworks hello, работе на локальной виртуальной Машине. С помощью этих средств можно создавать и запускать задания Hive и Pig для \"песочницы\" hello и просмотр выходных данных задания и журнал."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: e3434c45-95d1-4b96-ad4c-fb59870e2ff0
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/11/2017
ms.author: larryfr
ms.openlocfilehash: 7a3406b28d87d953e9b5be387faa86268f47b935
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-azure-data-lake-tools-for-visual-studio-with-hello-hortonworks-sandbox"></a><span data-ttu-id="1a75b-104">Использовать средства hello Озера данных Azure для Visual Studio с hello Hortonworks "песочницы"</span><span class="sxs-lookup"><span data-stu-id="1a75b-104">Use hello Azure Data Lake tools for Visual Studio with hello Hortonworks Sandbox</span></span>

<span data-ttu-id="1a75b-105">Azure Data Lake включает в себя средства для работы с универсальными кластерами Hadoop.</span><span class="sxs-lookup"><span data-stu-id="1a75b-105">Azure Data Lake includes tools for working with generic Hadoop clusters.</span></span> <span data-ttu-id="1a75b-106">В этом документе шаги hello необходимые средства Озера данных hello toouse с hello Hortonworks "песочницы", работающих в локальной виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="1a75b-106">This document provides hello steps needed toouse hello Data Lake tools with hello Hortonworks Sandbox running in a local virtual machine.</span></span>

<span data-ttu-id="1a75b-107">Использование hello Hortonworks "песочницы" позволяет toowork с Hadoop локально в среде разработки.</span><span class="sxs-lookup"><span data-stu-id="1a75b-107">Using hello Hortonworks Sandbox allows you toowork with Hadoop locally on your development environment.</span></span> <span data-ttu-id="1a75b-108">После разработки решения и хотите toodeploy его в масштабе, можно переместить tooan кластера HDInsight.</span><span class="sxs-lookup"><span data-stu-id="1a75b-108">After you have developed a solution and want toodeploy it at scale, you can then move tooan HDInsight cluster.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1a75b-109">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="1a75b-109">Prerequisites</span></span>

* <span data-ttu-id="1a75b-110">Здравствуйте, "песочницы" Hortonworks, работающих в виртуальной машине в среде разработки.</span><span class="sxs-lookup"><span data-stu-id="1a75b-110">hello Hortonworks Sandbox, running in a virtual machine on your development environment.</span></span> <span data-ttu-id="1a75b-111">Этот документ был написан и протестирован с "песочницы" hello, работающих в Oracle VirtualBox.</span><span class="sxs-lookup"><span data-stu-id="1a75b-111">This document was written and tested with hello sandbox running in Oracle VirtualBox.</span></span> <span data-ttu-id="1a75b-112">Сведения о настройке hello "песочницы" в разделе hello [Приступая к работе с hello Hortonworks "песочницы".](hdinsight-hadoop-emulator-get-started.md)</span><span class="sxs-lookup"><span data-stu-id="1a75b-112">For information on setting up hello sandbox, see hello [Get started with hello Hortonworks sandbox.](hdinsight-hadoop-emulator-get-started.md)</span></span> <span data-ttu-id="1a75b-113">.</span><span class="sxs-lookup"><span data-stu-id="1a75b-113">document.</span></span>

* <span data-ttu-id="1a75b-114">Visual Studio 2013, Visual Studio 2015 или Visual Studio 2017 (любой выпуск).</span><span class="sxs-lookup"><span data-stu-id="1a75b-114">Visual Studio 2013, Visual Studio 2015, or Visual Studio 2017 (any edition).</span></span>

* <span data-ttu-id="1a75b-115">Hello [Azure SDK для .NET](https://azure.microsoft.com/downloads/) 2.7.1 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="1a75b-115">hello [Azure SDK for .NET](https://azure.microsoft.com/downloads/) 2.7.1 or later.</span></span>

* <span data-ttu-id="1a75b-116">Hello [Озера данных Azure tools для Visual Studio](https://www.microsoft.com/download/details.aspx?id=49504).</span><span class="sxs-lookup"><span data-stu-id="1a75b-116">hello [Azure Data Lake tools for Visual Studio](https://www.microsoft.com/download/details.aspx?id=49504).</span></span>

## <a name="configure-passwords-for-hello-sandbox"></a><span data-ttu-id="1a75b-117">Настройка паролей для "песочницы" hello</span><span class="sxs-lookup"><span data-stu-id="1a75b-117">Configure passwords for hello sandbox</span></span>

<span data-ttu-id="1a75b-118">Убедитесь в том, что hello запущенного Hortonworks "песочницы".</span><span class="sxs-lookup"><span data-stu-id="1a75b-118">Make sure that hello Hortonworks Sandbox is running.</span></span> <span data-ttu-id="1a75b-119">Следуйте указаниям hello hello [Приступая к работе с hello "песочницы" Hortonworks](hdinsight-hadoop-emulator-get-started.md#set-sandbox-passwords) документа.</span><span class="sxs-lookup"><span data-stu-id="1a75b-119">Then follow hello steps in hello [Get started in hello Hortonworks Sandbox](hdinsight-hadoop-emulator-get-started.md#set-sandbox-passwords) document.</span></span> <span data-ttu-id="1a75b-120">Эти шаги помогут вам настроить hello пароль для hello SSH `root` учетную запись, а hello Ambari `admin` учетной записи.</span><span class="sxs-lookup"><span data-stu-id="1a75b-120">These steps configure hello password for hello SSH `root` account, and hello Ambari `admin` account.</span></span> <span data-ttu-id="1a75b-121">Эти пароли используются при подключении "песочницы" toohello из Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="1a75b-121">These passwords are used when you connect toohello sandbox from Visual Studio.</span></span>

## <a name="connect-hello-tools-toohello-sandbox"></a><span data-ttu-id="1a75b-122">Подключения "песочницы" toohello средства hello</span><span class="sxs-lookup"><span data-stu-id="1a75b-122">Connect hello tools toohello sandbox</span></span>

1. <span data-ttu-id="1a75b-123">Откройте Visual Studio и выберите **Вид**, а затем — **Обозреватель серверов**.</span><span class="sxs-lookup"><span data-stu-id="1a75b-123">Open Visual Studio, select **View**, and then select **Server Explorer**.</span></span>

2. <span data-ttu-id="1a75b-124">Из **обозревателя серверов**, щелкните правой кнопкой мыши hello **HDInsight** запись, а затем выберите **подключения tooHDInsight эмулятор**.</span><span class="sxs-lookup"><span data-stu-id="1a75b-124">From **Server Explorer**, right-click hello **HDInsight** entry, and then select **Connect tooHDInsight Emulator**.</span></span>

    ![Снимок экрана из обозревателя серверов, с tooHDInsight подключить эмулятор выделен](./media/hdinsight-hadoop-emulator-visual-studio/connect-emulator.png)

3. <span data-ttu-id="1a75b-126">Из hello **подключения эмулятора tooHDInsight** диалогового окна введите пароль hello, настроенный для Ambari.</span><span class="sxs-lookup"><span data-stu-id="1a75b-126">From hello **Connect tooHDInsight Emulator** dialog box, enter hello password that you configured for Ambari.</span></span>

    ![Снимок экрана: диалоговое окно с выделенным текстовым полем для ввода пароля](./media/hdinsight-hadoop-emulator-visual-studio/enter-ambari-password.png)

    <span data-ttu-id="1a75b-128">Выберите **Далее** toocontinue.</span><span class="sxs-lookup"><span data-stu-id="1a75b-128">Select **Next** toocontinue.</span></span>

4. <span data-ttu-id="1a75b-129">Используйте hello **пароль** поле tooenter hello пароль, настроенные для hello `root` учетной записи.</span><span class="sxs-lookup"><span data-stu-id="1a75b-129">Use hello **Password** field tooenter hello password you configured for hello `root` account.</span></span> <span data-ttu-id="1a75b-130">Оставьте остальные поля на значение по умолчанию hello hello.</span><span class="sxs-lookup"><span data-stu-id="1a75b-130">Leave hello other fields at hello default value.</span></span>

    ![Снимок экрана: диалоговое окно с выделенным текстовым полем для ввода пароля](./media/hdinsight-hadoop-emulator-visual-studio/enter-root-password.png)

    <span data-ttu-id="1a75b-132">Выберите **Далее** toocontinue.</span><span class="sxs-lookup"><span data-stu-id="1a75b-132">Select **Next** toocontinue.</span></span>

5. <span data-ttu-id="1a75b-133">Ожидания для проверки служб toofinish hello.</span><span class="sxs-lookup"><span data-stu-id="1a75b-133">Wait for validation of hello services toofinish.</span></span> <span data-ttu-id="1a75b-134">В некоторых случаях проверка может завершиться ошибкой и запрашивает tooupdate hello конфигурации.</span><span class="sxs-lookup"><span data-stu-id="1a75b-134">In some cases, validation may fail and prompt you tooupdate hello configuration.</span></span> <span data-ttu-id="1a75b-135">Если проверка завершается неудачно, установите **обновление**и дождитесь hello конфигурации и проверки для службы toofinish hello.</span><span class="sxs-lookup"><span data-stu-id="1a75b-135">If validation fails, select **Update**, and wait for hello configuration and verification for hello service toofinish.</span></span>

    ![Снимок экрана: диалоговое окно с выделенной кнопкой "Обновить"](./media/hdinsight-hadoop-emulator-visual-studio/fail-and-update.png)

    > [!NOTE]
    > <span data-ttu-id="1a75b-137">процесс обновления Hello использует Ambari toomodify приветствия ожидаемых toowhat конфигурации Hortonworks "песочницы" hello Озера данных средства для Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="1a75b-137">hello update process uses Ambari toomodify hello Hortonworks Sandbox configuration toowhat is expected by hello Data Lake tools for Visual Studio.</span></span>

6. <span data-ttu-id="1a75b-138">После завершения проверки, выберите **Готово** toocomplete конфигурации.</span><span class="sxs-lookup"><span data-stu-id="1a75b-138">After validation has finished, select **Finish** toocomplete configuration.</span></span>
    <span data-ttu-id="1a75b-139">![Снимок экрана: диалоговое окно с выделенной кнопкой "Готово"](./media/hdinsight-hadoop-emulator-visual-studio/finished-connect.png)</span><span class="sxs-lookup"><span data-stu-id="1a75b-139">![Screenshot of dialog box, with Finish button highlighted](./media/hdinsight-hadoop-emulator-visual-studio/finished-connect.png)</span></span>

     >[!NOTE]
     > <span data-ttu-id="1a75b-140">В зависимости от скорости hello среды разработки и hello объем памяти, выделенной toohello виртуальной машины его можно воспользоваться tooconfigure несколько минут и проверять hello службы.</span><span class="sxs-lookup"><span data-stu-id="1a75b-140">Depending on hello speed of your development environment, and hello amount of memory allocated toohello virtual machine, it can take several minutes tooconfigure and validate hello services.</span></span>

<span data-ttu-id="1a75b-141">После выполнения этих шагов, теперь у вас есть **локального кластера HDInsight** записи в обозревателе серверов hello **HDInsight** раздела.</span><span class="sxs-lookup"><span data-stu-id="1a75b-141">After following these steps, you now have an **HDInsight local cluster** entry in Server Explorer, under hello **HDInsight** section.</span></span>

## <a name="write-a-hive-query"></a><span data-ttu-id="1a75b-142">Написание запроса Hive</span><span class="sxs-lookup"><span data-stu-id="1a75b-142">Write a Hive query</span></span>

<span data-ttu-id="1a75b-143">Hive предоставляет язык запросов по типу SQL (HiveQL) для работы со структурированными данными.</span><span class="sxs-lookup"><span data-stu-id="1a75b-143">Hive provides a SQL-like query language (HiveQL) for working with structured data.</span></span> <span data-ttu-id="1a75b-144">Используйте следующие шаги toolearn как toorun по требованию запросов к локальному кластеру hello hello.</span><span class="sxs-lookup"><span data-stu-id="1a75b-144">Use hello following steps toolearn how toorun on-demand queries against hello local cluster.</span></span>

1. <span data-ttu-id="1a75b-145">В **обозревателя серверов**, щелкните правой кнопкой мыши запись hello для hello локального кластера, который был добавлен ранее и выберите **написать запрос Hive**.</span><span class="sxs-lookup"><span data-stu-id="1a75b-145">In **Server Explorer**, right-click hello entry for hello local cluster that you added previously, and then select **Write a Hive Query**.</span></span>

    ![Снимок экрана: обозреватель сервера с выделенным пунктом "Написать запрос Hive"](./media/hdinsight-hadoop-emulator-visual-studio/write-hive-query.png)

    <span data-ttu-id="1a75b-147">Откроется окно нового запроса.</span><span class="sxs-lookup"><span data-stu-id="1a75b-147">A new query window appears.</span></span> <span data-ttu-id="1a75b-148">Здесь можно быстро писать и отправить запрос toohello локального кластера.</span><span class="sxs-lookup"><span data-stu-id="1a75b-148">Here you can quickly write and submit a query toohello local cluster.</span></span>

2. <span data-ttu-id="1a75b-149">В новом окне запроса hello введите следующую команду hello:</span><span class="sxs-lookup"><span data-stu-id="1a75b-149">In hello new query window, enter hello following command:</span></span>

        select count(*) from sample_08;

    <span data-ttu-id="1a75b-150">toorun hello запроса select **отправить** hello верхней части окна hello.</span><span class="sxs-lookup"><span data-stu-id="1a75b-150">toorun hello query, select **Submit** at hello top of hello window.</span></span> <span data-ttu-id="1a75b-151">Оставьте hello другие значения (**пакета** и имя сервера) в значения по умолчанию hello.</span><span class="sxs-lookup"><span data-stu-id="1a75b-151">Leave hello other values (**Batch** and server name) at hello default values.</span></span>

    ![Снимок экрана окна запроса, с выделенной кнопкой отправки hello](./media/hdinsight-hadoop-emulator-visual-studio/submit-hive.png)

    <span data-ttu-id="1a75b-153">Можно также использовать hello раскрывающееся меню рядом слишком**отправить** tooselect **Дополнительно**.</span><span class="sxs-lookup"><span data-stu-id="1a75b-153">You can also use hello drop-down menu next too**Submit** tooselect **Advanced**.</span></span> <span data-ttu-id="1a75b-154">Дополнительные параметры позволяют tooprovide Дополнительные параметры для отправки задания hello.</span><span class="sxs-lookup"><span data-stu-id="1a75b-154">Advanced options allow you tooprovide additional options when you submit hello job.</span></span>

    ![Снимок экрана: диалоговое окно "Отправить скрипт"](./media/hdinsight-hadoop-emulator-visual-studio/advanced-hive.png)

3. <span data-ttu-id="1a75b-156">После отправки запроса hello отображается состояние задания hello.</span><span class="sxs-lookup"><span data-stu-id="1a75b-156">After you submit hello query, hello job status appears.</span></span> <span data-ttu-id="1a75b-157">состояние задания Hello отображаются сведения о задания hello, обрабатывается Hadoop.</span><span class="sxs-lookup"><span data-stu-id="1a75b-157">hello job status displays information about hello job as it is processed by Hadoop.</span></span> <span data-ttu-id="1a75b-158">**Состояние задания** предоставляет hello состояние задания hello.</span><span class="sxs-lookup"><span data-stu-id="1a75b-158">**Job State** provides hello status of hello job.</span></span> <span data-ttu-id="1a75b-159">периодически обновляется состояние Hello, или можно использовать hello обновление значок toorefresh hello состояния вручную.</span><span class="sxs-lookup"><span data-stu-id="1a75b-159">hello state is updated periodically, or you can use hello refresh icon toorefresh hello state manually.</span></span>

    ![Снимок экрана: диалоговое окно "Представление заданий" с выделенной записью "Состояние задания"](./media/hdinsight-hadoop-emulator-visual-studio/job-state.png)

    <span data-ttu-id="1a75b-161">После hello **состояние задания** изменяет слишком**завершен**, отображается направленный ациклического графа (DAG).</span><span class="sxs-lookup"><span data-stu-id="1a75b-161">After hello **Job State** changes too**Finished**, a Directed Acyclic Graph (DAG) is displayed.</span></span> <span data-ttu-id="1a75b-162">На этой схеме описан hello путь выполнения, который был определяется Tez при обработке запроса Hive hello.</span><span class="sxs-lookup"><span data-stu-id="1a75b-162">This diagram describes hello execution path that was determined by Tez when processing hello Hive query.</span></span> <span data-ttu-id="1a75b-163">Tez — подсистема выполнения по умолчанию hello для куста hello локальном кластере.</span><span class="sxs-lookup"><span data-stu-id="1a75b-163">Tez is hello default execution engine for Hive on hello local cluster.</span></span>

    > [!NOTE]
    > <span data-ttu-id="1a75b-164">Tez будет по умолчанию hello при использовании кластеры HDInsight под управлением Linux.</span><span class="sxs-lookup"><span data-stu-id="1a75b-164">Tez is also hello default when you are using Linux-based HDInsight clusters.</span></span> <span data-ttu-id="1a75b-165">Это не по умолчанию hello в HDInsight под управлением Windows.</span><span class="sxs-lookup"><span data-stu-id="1a75b-165">It is not hello default on Windows-based HDInsight.</span></span> <span data-ttu-id="1a75b-166">toouse его нет, необходимо добавить строку hello `set hive.execution.engine = tez;` toohello Начало запроса Hive.</span><span class="sxs-lookup"><span data-stu-id="1a75b-166">toouse it there, you must add hello line `set hive.execution.engine = tez;` toohello beginning of your Hive query.</span></span>

    <span data-ttu-id="1a75b-167">Используйте hello **выходные данные задания** связать tooview hello вывода.</span><span class="sxs-lookup"><span data-stu-id="1a75b-167">Use hello **Job Output** link tooview hello output.</span></span> <span data-ttu-id="1a75b-168">В этом случае это 823 hello количество строк в таблице sample_08 hello.</span><span class="sxs-lookup"><span data-stu-id="1a75b-168">In this case, it is 823, hello number of rows in hello sample_08 table.</span></span> <span data-ttu-id="1a75b-169">Диагностические данные об hello задания можно просмотреть с помощью hello **журнала задания** и **Загрузка журнала YARN** ссылки.</span><span class="sxs-lookup"><span data-stu-id="1a75b-169">You can view diagnostics information about hello job by using hello **Job Log** and **Download YARN Log** links.</span></span>

4. <span data-ttu-id="1a75b-170">Можно также запустить задания Hive интерактивно, изменив hello **пакета** поле слишком**Interactive**.</span><span class="sxs-lookup"><span data-stu-id="1a75b-170">You can also run Hive jobs interactively by changing hello **Batch** field too**Interactive**.</span></span> <span data-ttu-id="1a75b-171">а затем нажать кнопку **Выполнить**.</span><span class="sxs-lookup"><span data-stu-id="1a75b-171">Then select **Execute**.</span></span>

    ![Снимок экрана с выделенным элементом "Интерактивный" и кнопкой "Выполнить"](./media/hdinsight-hadoop-emulator-visual-studio/interactive-query.png)

    <span data-ttu-id="1a75b-173">Интерактивный запрос, потоки hello выходные данные журнала, созданного во время обработки toohello **HiveServer2 вывода** окна.</span><span class="sxs-lookup"><span data-stu-id="1a75b-173">An interactive query streams hello output log generated during processing toohello **HiveServer2 Output** window.</span></span>

    > [!NOTE]
    > <span data-ttu-id="1a75b-174">Hello сведения hello те же данные, можно получить из hello **журнала задания** связь после завершения задания.</span><span class="sxs-lookup"><span data-stu-id="1a75b-174">hello information is hello same that is available from hello **Job Log** link after a job has finished.</span></span>

    ![Снимок экрана: журнал выходных данных](./media/hdinsight-hadoop-emulator-visual-studio/hiveserver2-output.png)

## <a name="create-a-hive-project"></a><span data-ttu-id="1a75b-176">Создание проекта Hive</span><span class="sxs-lookup"><span data-stu-id="1a75b-176">Create a Hive project</span></span>

<span data-ttu-id="1a75b-177">Вы также можете создать проект, который содержит несколько скриптов Hive.</span><span class="sxs-lookup"><span data-stu-id="1a75b-177">You can also create a project that contains multiple Hive scripts.</span></span> <span data-ttu-id="1a75b-178">Используйте проект, если требуется иметь связанные сценарии или сценарии toostore в системе управления версиями.</span><span class="sxs-lookup"><span data-stu-id="1a75b-178">Use a project when you have related scripts or want toostore scripts in a version control system.</span></span>

1. <span data-ttu-id="1a75b-179">Откройте Visual Studio, выберите **Файл**, **Создать**, а затем **Проект**.</span><span class="sxs-lookup"><span data-stu-id="1a75b-179">In Visual Studio, select **File**, **New**, and then **Project**.</span></span>

2. <span data-ttu-id="1a75b-180">Из списка проектов hello, разверните **шаблоны**, разверните **Озера данных Azure**и выберите **HIVE (HDInsight)**.</span><span class="sxs-lookup"><span data-stu-id="1a75b-180">From hello list of projects, expand **Templates**, expand **Azure Data Lake**, and then select **HIVE (HDInsight)**.</span></span> <span data-ttu-id="1a75b-181">Выберите из списка шаблонов hello **Hive образец**.</span><span class="sxs-lookup"><span data-stu-id="1a75b-181">From hello list of templates, select **Hive Sample**.</span></span> <span data-ttu-id="1a75b-182">Введите имя и расположение, а затем нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="1a75b-182">Enter a name and location, and then select **OK**.</span></span>

    ![Снимок экрана; окно нового проекта с выделенными элементами "Azure Data Lake", "HIVE", "Пример Hive" и "ОК"](./media/hdinsight-hadoop-emulator-visual-studio/new-hive-project.png)

<span data-ttu-id="1a75b-184">Hello **Hive образец** проект содержит два сценария **WebLogAnalysis.hql** и **SensorDataAnalysis.hql**.</span><span class="sxs-lookup"><span data-stu-id="1a75b-184">hello **Hive Sample** project contains two scripts, **WebLogAnalysis.hql** and **SensorDataAnalysis.hql**.</span></span> <span data-ttu-id="1a75b-185">Вы можете отправить эти скрипты с помощью hello же **отправить** кнопку hello верхней части окна hello.</span><span class="sxs-lookup"><span data-stu-id="1a75b-185">You can submit these scripts by using hello same **Submit** button at hello top of hello window.</span></span>

## <a name="create-a-pig-project"></a><span data-ttu-id="1a75b-186">Создание проекта Pig</span><span class="sxs-lookup"><span data-stu-id="1a75b-186">Create a Pig project</span></span>

<span data-ttu-id="1a75b-187">Тогда как Hive предоставляет язык по типу SQL для работы со структурированными данными, Pig работает, преобразуя данные.</span><span class="sxs-lookup"><span data-stu-id="1a75b-187">While Hive provides a SQL-like language for working with structured data, Pig works by performing transformations on data.</span></span> <span data-ttu-id="1a75b-188">Pig предоставляет язык (латиница Pig), который позволяет вам toodevelop конвейера преобразований.</span><span class="sxs-lookup"><span data-stu-id="1a75b-188">Pig provides a language (Pig Latin) that allows you toodevelop a pipeline of transformations.</span></span> <span data-ttu-id="1a75b-189">toouse Pig с hello локального кластера, выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="1a75b-189">toouse Pig with hello local cluster, follow these steps:</span></span>

1. <span data-ttu-id="1a75b-190">Откройте Visual Studio, выберите **Файл**, **Создать**, а затем — **Проект**.</span><span class="sxs-lookup"><span data-stu-id="1a75b-190">Open Visual Studio, and select **File**, **New**, and then **Project**.</span></span> <span data-ttu-id="1a75b-191">Из списка проектов hello, разверните узел **шаблоны**, разверните **Озера данных Azure**, а затем выберите **Pig (HDInsight)**.</span><span class="sxs-lookup"><span data-stu-id="1a75b-191">From hello list of projects, expand **Templates**, expand **Azure Data Lake**, and then select **Pig (HDInsight)**.</span></span> <span data-ttu-id="1a75b-192">Выберите из списка шаблонов hello **Pig приложения**.</span><span class="sxs-lookup"><span data-stu-id="1a75b-192">From hello list of templates, select **Pig Application**.</span></span> <span data-ttu-id="1a75b-193">Введите имя и расположение, а затем нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="1a75b-193">Enter a name, location, and then select **OK**.</span></span>

    ![Снимок экрана; окно нового проекта с выделенными элементами "Azure Data Lake", "Pig", "Приложение Pig" и "ОК"](./media/hdinsight-hadoop-emulator-visual-studio/new-pig.png)

2. <span data-ttu-id="1a75b-195">Введите после текста как содержимое hello hello hello **script.pig** файла, созданного с помощью этого проекта.</span><span class="sxs-lookup"><span data-stu-id="1a75b-195">Enter hello following text as hello contents of hello **script.pig** file that was created with this project.</span></span>

        a = LOAD '/demo/data/Website/Website-Logs' AS (
            log_id:int,
            ip_address:chararray,
            date:chararray,
            time:chararray,
            landing_page:chararray,
            source:chararray);
        b = FILTER a BY (log_id > 100);
        c = GROUP b BY ip_address;
        DUMP c;

    <span data-ttu-id="1a75b-196">А чем Hive, Pig использует другой язык, выполнение задания hello одинаково для обоих языков через hello **отправить** кнопки.</span><span class="sxs-lookup"><span data-stu-id="1a75b-196">While Pig uses a different language than Hive, how you run hello jobs is consistent between both languages, through hello **Submit** button.</span></span> <span data-ttu-id="1a75b-197">Выбор hello раскрывающегося списка рядом с **отправить** выводит диалоговое окно расширенного отправки для Pig.</span><span class="sxs-lookup"><span data-stu-id="1a75b-197">Selecting hello drop-down beside **Submit** displays an advanced submit dialog box for Pig.</span></span>

    ![Снимок экрана: диалоговое окно "Отправить скрипт"](./media/hdinsight-hadoop-emulator-visual-studio/advanced-pig.png)

3. <span data-ttu-id="1a75b-199">также отображается состояние заданий Hello и выходные данные, Здравствуйте таким же, как запрос Hive.</span><span class="sxs-lookup"><span data-stu-id="1a75b-199">hello job status and output is also displayed, hello same as a Hive query.</span></span>

    ![Снимок экрана: завершенное задание Pig](./media/hdinsight-hadoop-emulator-visual-studio/completed-pig.png)

## <a name="view-jobs"></a><span data-ttu-id="1a75b-201">Просмотр заданий</span><span class="sxs-lookup"><span data-stu-id="1a75b-201">View jobs</span></span>

<span data-ttu-id="1a75b-202">Средства Озера данных также позволяют tooeasily Просмотр сведений о заданиях, которые были запущены в Hadoop.</span><span class="sxs-lookup"><span data-stu-id="1a75b-202">Data Lake tools also allow you tooeasily view information about jobs that have been run on Hadoop.</span></span> <span data-ttu-id="1a75b-203">Используйте следующие шаги toosee hello заданий, которые были запущены на локальном кластере hello hello.</span><span class="sxs-lookup"><span data-stu-id="1a75b-203">Use hello following steps toosee hello jobs that have been run on hello local cluster.</span></span>

1. <span data-ttu-id="1a75b-204">Из **обозревателя серверов**, щелкните правой кнопкой мыши локальный кластер hello и выберите **Просмотр заданий**.</span><span class="sxs-lookup"><span data-stu-id="1a75b-204">From **Server Explorer**, right-click hello local cluster, and then select **View Jobs**.</span></span> <span data-ttu-id="1a75b-205">Отображается список заданий, которые были отправленной toohello кластера.</span><span class="sxs-lookup"><span data-stu-id="1a75b-205">A list of jobs that have been submitted toohello cluster is displayed.</span></span>

    ![Снимок экрана: обозреватель сервера с выделенным пунктом "Просмотреть задания"](./media/hdinsight-hadoop-emulator-visual-studio/view-jobs.png)

2. <span data-ttu-id="1a75b-207">Hello список заданий выберите одну tooview сведений о задании hello.</span><span class="sxs-lookup"><span data-stu-id="1a75b-207">From hello list of jobs, select one tooview hello job details.</span></span>

    ![Снимок экрана из задания браузера, с помощью одного из заданий hello выделен](./media/hdinsight-hadoop-emulator-visual-studio/view-job-details.png)

    <span data-ttu-id="1a75b-209">Отображаемые сведения Hello — примерно toowhat, отображаемые после выполнения запроса Hive или Pig, включая ссылки tooview hello выходные данные и сведения журналов.</span><span class="sxs-lookup"><span data-stu-id="1a75b-209">hello information displayed is similar toowhat you see after running a Hive or Pig query, including links tooview hello output and log information.</span></span>

3. <span data-ttu-id="1a75b-210">Можно также изменять и повторно отправить задания hello отсюда.</span><span class="sxs-lookup"><span data-stu-id="1a75b-210">You can also modify and resubmit hello job from here.</span></span>

## <a name="view-hive-databases"></a><span data-ttu-id="1a75b-211">Просмотр баз данных Hive</span><span class="sxs-lookup"><span data-stu-id="1a75b-211">View Hive databases</span></span>

1. <span data-ttu-id="1a75b-212">В **обозревателя серверов**, разверните hello **локального кластера HDInsight** входа и разверните **баз данных Hive**.</span><span class="sxs-lookup"><span data-stu-id="1a75b-212">In **Server Explorer**, expand hello **HDInsight local cluster** entry, and then expand **Hive Databases**.</span></span> <span data-ttu-id="1a75b-213">Hello **по умолчанию** и **xademo** базы данных в локальном кластере hello отображаются.</span><span class="sxs-lookup"><span data-stu-id="1a75b-213">hello **Default** and **xademo** databases on hello local cluster are displayed.</span></span> <span data-ttu-id="1a75b-214">Развертывание базы данных показывает hello таблиц в базе данных hello.</span><span class="sxs-lookup"><span data-stu-id="1a75b-214">Expanding a database shows hello tables within hello database.</span></span>

    ![Снимок экрана: обозреватель сервера с развернутыми базами данных](./media/hdinsight-hadoop-emulator-visual-studio/expanded-databases.png)

2. <span data-ttu-id="1a75b-216">Раскройте таблицу отображает hello столбцы этой таблицы.</span><span class="sxs-lookup"><span data-stu-id="1a75b-216">Expanding a table displays hello columns for that table.</span></span> <span data-ttu-id="1a75b-217">Просмотр hello tooquickly данных, щелкните правой кнопкой мыши таблицу и выберите **представление первые 100 строк**.</span><span class="sxs-lookup"><span data-stu-id="1a75b-217">tooquickly view hello data, right-click a table, and select **View Top 100 Rows**.</span></span>

    ![Снимок экрана: обозреватель сервера с развернутой таблицей и выбранным пунктом "Просмотреть первые 100 строк"](./media/hdinsight-hadoop-emulator-visual-studio/view-100.png)

### <a name="database-and-table-properties"></a><span data-ttu-id="1a75b-219">Свойства базы данных и таблицы</span><span class="sxs-lookup"><span data-stu-id="1a75b-219">Database and table properties</span></span>

<span data-ttu-id="1a75b-220">Можно просмотреть свойства hello базы данных или таблицы.</span><span class="sxs-lookup"><span data-stu-id="1a75b-220">You can view hello properties of a database or table.</span></span> <span data-ttu-id="1a75b-221">При выборе **свойства** отображаются сведения об элементе выбран hello в окне свойств hello.</span><span class="sxs-lookup"><span data-stu-id="1a75b-221">Selecting **Properties** displays details for hello selected item in hello properties window.</span></span> <span data-ttu-id="1a75b-222">Например в разделе hello сведения, отображаемые на следующий снимок экрана приветствия:</span><span class="sxs-lookup"><span data-stu-id="1a75b-222">For example, see hello information shown in hello following screenshot:</span></span>

![Снимок экрана: окно свойств](./media/hdinsight-hadoop-emulator-visual-studio/properties.png)

### <a name="create-a-table"></a><span data-ttu-id="1a75b-224">Создание таблицы</span><span class="sxs-lookup"><span data-stu-id="1a75b-224">Create a table</span></span>

<span data-ttu-id="1a75b-225">toocreate таблицу, щелкните правой кнопкой мыши базу данных, а затем выберите **Create Table**.</span><span class="sxs-lookup"><span data-stu-id="1a75b-225">toocreate a table, right-click a database, and then select **Create Table**.</span></span>

![Снимок экрана: обозреватель сервера с выделенным пунктом "Создать таблицу"](./media/hdinsight-hadoop-emulator-visual-studio/create-table.png)

<span data-ttu-id="1a75b-227">Затем можно создать таблицу hello, с помощью формы.</span><span class="sxs-lookup"><span data-stu-id="1a75b-227">You can then create hello table using a form.</span></span> <span data-ttu-id="1a75b-228">Внизу hello следующий снимок экрана приветствия, можно увидеть hello необработанные HiveQL, используемые toocreate hello таблицы.</span><span class="sxs-lookup"><span data-stu-id="1a75b-228">At hello bottom of hello following screenshot, you can see hello raw HiveQL that is used toocreate hello table.</span></span>

![Снимок экрана: hello форму используется toocreate таблицы](./media/hdinsight-hadoop-emulator-visual-studio/create-table-form.png)

## <a name="next-steps"></a><span data-ttu-id="1a75b-230">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="1a75b-230">Next steps</span></span>

* [<span data-ttu-id="1a75b-231">Изучение ropes hello объекта hello Hortonworks "песочницы"</span><span class="sxs-lookup"><span data-stu-id="1a75b-231">Learning hello ropes of hello Hortonworks Sandbox</span></span>](http://hortonworks.com/hadoop-tutorial/learning-the-ropes-of-the-hortonworks-sandbox/)
* <span data-ttu-id="1a75b-232">[Hadoop tutorial - Getting started with HDP](http://hortonworks.com/hadoop-tutorial/hello-world-an-introduction-to-hadoop-hcatalog-hive-and-pig/) (Руководство по началу работы с Hadoop)</span><span class="sxs-lookup"><span data-stu-id="1a75b-232">[Hadoop tutorial - Getting started with HDP](http://hortonworks.com/hadoop-tutorial/hello-world-an-introduction-to-hadoop-hcatalog-hive-and-pig/)</span></span>
