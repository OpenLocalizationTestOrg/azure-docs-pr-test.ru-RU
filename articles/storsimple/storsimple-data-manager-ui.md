---
title: "aaaMicrosoft пользовательского интерфейса диспетчера StorSimple данных Azure | Документы Microsoft"
description: "Описывает способ toouse службы диспетчера StorSimple данных пользовательского интерфейса (личной предварительной версии)"
services: storsimple
documentationcenter: NA
author: vidarmsft
manager: syadav
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 11/22/2016
ms.author: vidarmsft
ms.openlocfilehash: b0ee12b3e495400b54e48eb1a98c68b1af2e5f7a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="manage-using-hello-storsimple-data-manager-service-ui-private-preview"></a><span data-ttu-id="a0d12-103">Управление с помощью службы диспетчера StorSimple данных hello пользовательского интерфейса (личной предварительной версии)</span><span class="sxs-lookup"><span data-stu-id="a0d12-103">Manage using hello StorSimple Data Manager service UI (Private Preview)</span></span>

<span data-ttu-id="a0d12-104">В этой статье объясняется, как можно использовать преобразование данных пользовательского интерфейса диспетчера данных StorSimple tooperform hello на данных, располагающихся на устройства серии StorSimple 8000 hello.</span><span class="sxs-lookup"><span data-stu-id="a0d12-104">This article explains how you can use hello StorSimple Data Manager UI tooperform data transformation on data residing on hello StorSimple 8000 series devices.</span></span> <span data-ttu-id="a0d12-105">Hello преобразованные данные могут быть впоследствии использованы другими службами Azure, такие как службы мультимедиа Azure, Azure HDInsight, машинного обучения Azure и поиска Azure.</span><span class="sxs-lookup"><span data-stu-id="a0d12-105">hello transformed data can then be consumed by other Azure services such as Azure Media Services, Azure HDInsight, Azure Machine Learning, and Azure Search.</span></span> 


## <a name="use-storsimple-data-transformation"></a><span data-ttu-id="a0d12-106">Использование преобразования данных StorSimple</span><span class="sxs-lookup"><span data-stu-id="a0d12-106">Use StorSimple Data Transformation</span></span>

<span data-ttu-id="a0d12-107">Hello данных StorSimple Manager — ресурс hello, в течение которого может быть создан, преобразование данных.</span><span class="sxs-lookup"><span data-stu-id="a0d12-107">hello StorSimple Data Manager is hello resource within which Data Transformation can be instantiated.</span></span> <span data-ttu-id="a0d12-108">Hello службы преобразования данных позволяет перемещать данные из вашей локальной для StorSimple устройство tooblobs в хранилище Azure.</span><span class="sxs-lookup"><span data-stu-id="a0d12-108">hello Data Transformation service lets you move data from your StorSimple on-premises device tooblobs in Azure storage.</span></span> <span data-ttu-id="a0d12-109">Таким образом в рабочем процессе необходимо toospecify hello сведения о StorSimple данных устройства и hello, требуется учетная запись хранения toohello toomove интерес.</span><span class="sxs-lookup"><span data-stu-id="a0d12-109">Hence, in workflow you need toospecify hello details about your StorSimple device and hello data of interest that you want toomove toohello storage account.</span></span>

### <a name="create-a-storsimple-data-manager-service"></a><span data-ttu-id="a0d12-110">Создание новой службы диспетчера данных StorSimple</span><span class="sxs-lookup"><span data-stu-id="a0d12-110">Create a StorSimple Data Manager service</span></span>

<span data-ttu-id="a0d12-111">Выполните следующие шаги toocreate службу диспетчера StorSimple данных hello.</span><span class="sxs-lookup"><span data-stu-id="a0d12-111">Perform hello following steps toocreate a StorSimple Data Manager service.</span></span>

1. <span data-ttu-id="a0d12-112">toocreate службу диспетчера StorSimple данных, слишком go[https://aka.ms/HybridDataManager](https://aka.ms/HybridDataManager)</span><span class="sxs-lookup"><span data-stu-id="a0d12-112">toocreate a StorSimple Data Manager service, go too[https://aka.ms/HybridDataManager](https://aka.ms/HybridDataManager)</span></span>

2. <span data-ttu-id="a0d12-113">Нажмите кнопку hello  **+**  значок и поиска для диспетчера StorSimple данных.</span><span class="sxs-lookup"><span data-stu-id="a0d12-113">Click hello **+** icon and search for StorSimple Data Manager.</span></span> <span data-ttu-id="a0d12-114">Выберите нужную службу диспетчера данных StorSimple и нажмите кнопку **Создать**.</span><span class="sxs-lookup"><span data-stu-id="a0d12-114">Click your StorSimple Data Manager service and then click **Create**.</span></span>

3. <span data-ttu-id="a0d12-115">Подписки включена для создания этой службы, вы увидите следующие колонке hello.</span><span class="sxs-lookup"><span data-stu-id="a0d12-115">If your subscription is enabled for creating this service, you see hello following blade.</span></span>

    ![Создание ресурса диспетчера данных StorSimple](./media/storsimple-data-manager-ui/create-new-data-manager-service.png)

4. <span data-ttu-id="a0d12-117">Введите hello входные данные и нажмите кнопку **создать**.</span><span class="sxs-lookup"><span data-stu-id="a0d12-117">Enter hello inputs and click **Create**.</span></span> <span data-ttu-id="a0d12-118">Hello определенное расположение должно быть hello, содержащий учетные записи хранения и службе StorSimple Manager.</span><span class="sxs-lookup"><span data-stu-id="a0d12-118">hello specified location should be hello one that houses your storage accounts and your StorSimple Manager service.</span></span> <span data-ttu-id="a0d12-119">В настоящее время поддерживаются только регионы "Западная часть США" и "Западная Европа".</span><span class="sxs-lookup"><span data-stu-id="a0d12-119">Currently, only West US and West Europe regions are supported.</span></span> <span data-ttu-id="a0d12-120">Таким образом диспетчер данных службы, hello и службой диспетчера StorSimple связанные учетной записи хранения должны быть в предыдущем hello поддерживается регионах.</span><span class="sxs-lookup"><span data-stu-id="a0d12-120">Hence, your StorSimple Manager service, Data Manager service, and hello associated storage account should all be in hello preceding supported regions.</span></span> <span data-ttu-id="a0d12-121">Это занимает около минуты toocreate hello службы.</span><span class="sxs-lookup"><span data-stu-id="a0d12-121">It takes about a minute toocreate hello service.</span></span>

### <a name="create-a-data-transformation-job-definition"></a><span data-ttu-id="a0d12-122">Создание определения задания для преобразования данных</span><span class="sxs-lookup"><span data-stu-id="a0d12-122">Create a data transformation job definition</span></span>

<span data-ttu-id="a0d12-123">В службе диспетчера StorSimple данных необходимо toocreate определение задания преобразования данных.</span><span class="sxs-lookup"><span data-stu-id="a0d12-123">Within a StorSimple Data Manager service, you need toocreate a data transformation job definition.</span></span> <span data-ttu-id="a0d12-124">Определение задания задает подробные сведения о данных hello, которые вас интересуют перемещение в учетной записи хранения в собственном формате hello.</span><span class="sxs-lookup"><span data-stu-id="a0d12-124">A job definition specifies details of hello data that you are interested in moving into a storage account in hello native format.</span></span> 

<span data-ttu-id="a0d12-125">Выполните следующие шаги toocreate новое определение задания преобразования данных hello.</span><span class="sxs-lookup"><span data-stu-id="a0d12-125">Perform hello following steps toocreate a new data transformation job definition.</span></span>

1.  <span data-ttu-id="a0d12-126">Перейдите toohello службу, созданную.</span><span class="sxs-lookup"><span data-stu-id="a0d12-126">Navigate toohello service that you created.</span></span> <span data-ttu-id="a0d12-127">Щелкните **+ Определение задания**.</span><span class="sxs-lookup"><span data-stu-id="a0d12-127">Click **+ Job Definition**.</span></span>

    ![Кнопка "+ Определение задания".](./media/storsimple-data-manager-ui/click-add-job-definition.png)

2. <span data-ttu-id="a0d12-129">Открывает Hello Новая колонка определения задания.</span><span class="sxs-lookup"><span data-stu-id="a0d12-129">hello new job definition blade opens up.</span></span> <span data-ttu-id="a0d12-130">Присвойте заданию имя и нажмите кнопку **Источник**.</span><span class="sxs-lookup"><span data-stu-id="a0d12-130">Give your job definition a name and click **Source**.</span></span> <span data-ttu-id="a0d12-131">В hello **Настройка источника данных** колонке подробно описывают hello устройства StorSimple и hello интересующие его данные.</span><span class="sxs-lookup"><span data-stu-id="a0d12-131">In hello **Configure data source** blade, specify hello details of your StorSimple device and hello data of interest.</span></span>

    ![Создание определения задания](./media/storsimple-data-manager-ui//create-new-job-deifnition.png)

3. <span data-ttu-id="a0d12-133">Так как это новая служба диспетчера данных, репозитории данных еще не настроены.</span><span class="sxs-lookup"><span data-stu-id="a0d12-133">Since this is a new Data Manager service, no data repositories are configured.</span></span> <span data-ttu-id="a0d12-134">щелкните Диспетчер StorSimple Manager как хранилище данных, tooadd **добавить новый** в hello раскрывающемся списке репозиторий данных, а затем нажмите кнопку **добавить хранилище данных**.</span><span class="sxs-lookup"><span data-stu-id="a0d12-134">tooadd your StorSimple Manager as a data repository, click **Add new** in hello data repository dropdown and then click **Add Data Repository**.</span></span>

4. <span data-ttu-id="a0d12-135">Выберите **StorSimple серии 8000 Manager** функции hello репозитория введите свойства hello и вашей **StorSimple Manager**.</span><span class="sxs-lookup"><span data-stu-id="a0d12-135">Choose **StorSimple 8000 series Manager** as hello repository type and enter hello properties of your **StorSimple Manager**.</span></span> <span data-ttu-id="a0d12-136">Для hello **идентификатор ресурса** поля требуется число hello tooenter перед hello **:** в ключ регистрации hello диспетчера StorSimple.</span><span class="sxs-lookup"><span data-stu-id="a0d12-136">For hello **Resource Id** field, you need tooenter hello number before hello **:** in hello registration key of your StorSimple manager.</span></span>

    ![Создание источника данных](./media/storsimple-data-manager-ui/create-new-data-source.png)

5.  <span data-ttu-id="a0d12-138">Когда закончите, нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="a0d12-138">Click **OK** when done.</span></span> <span data-ttu-id="a0d12-139">Репозиторий данных будет сохранен, и позднее этот диспетчер StorSimple можно будет использовать в других определениях заданий, эти параметры не нужно будет вводить повторно.</span><span class="sxs-lookup"><span data-stu-id="a0d12-139">This saves your data repository and this StorSimple Manager can be reused in other job definitions without entering these parameters again.</span></span> <span data-ttu-id="a0d12-140">Он занимает несколько секунд после нажатия **ОК** для hello tooshow StorSimple Manager вверх в раскрывающемся списке hello.</span><span class="sxs-lookup"><span data-stu-id="a0d12-140">It takes a few seconds after you click **OK** for hello StorSimple Manager tooshow up in hello dropdown.</span></span>

6.  <span data-ttu-id="a0d12-141">В hello **Настройка источника данных** колонки, введите имя устройства hello и hello имя тома, которое содержит данные, представляющие интерес.</span><span class="sxs-lookup"><span data-stu-id="a0d12-141">In hello **Configure data source** blade, enter hello device name and hello volume name that has your data of interest.</span></span>

7.  <span data-ttu-id="a0d12-142">В hello **фильтра** подраздела, введите hello корневого каталога, содержащего данные, представляющие интерес (в этом поле должно начинаться с `\`).</span><span class="sxs-lookup"><span data-stu-id="a0d12-142">In hello **Filter** subsection, enter hello root directory that contains your data of interest (this field should start with a `\`).</span></span> <span data-ttu-id="a0d12-143">Здесь можно также добавить фильтры файлов.</span><span class="sxs-lookup"><span data-stu-id="a0d12-143">You can also add any file filters here.</span></span>

8.  <span data-ttu-id="a0d12-144">службы DTS Hello занимается hello данные, которые вытесняются вверх toohello Azure через моментальные снимки.</span><span class="sxs-lookup"><span data-stu-id="a0d12-144">hello data transformation service works on hello data that is pushed up toohello Azure via snapshots.</span></span> <span data-ttu-id="a0d12-145">При выполнении этого задания, вы можете tootake резервной копии каждый раз, это задание выполняется (toowork на последних данных) или toouse hello последней существующей резервной копии в облаке hello (Если вы работаете на некоторых архивированных данных).</span><span class="sxs-lookup"><span data-stu-id="a0d12-145">When running this job, you can choose tootake a backup every time this job is run (toowork on latest data) or toouse hello last existing backup in hello cloud (if you are working on some archived data).</span></span>

    ![Сведения о новом источнике данных](./media/storsimple-data-manager-ui/new-data-source-details.png)

9. <span data-ttu-id="a0d12-147">Теперь параметры цели hello нужны toobe настроен.</span><span class="sxs-lookup"><span data-stu-id="a0d12-147">Next, hello Target settings need toobe configured.</span></span> <span data-ttu-id="a0d12-148">Поддерживаются два типа целевых объектов —учетные записи хранения Azure и учетные записи служб мультимедиа Azure.</span><span class="sxs-lookup"><span data-stu-id="a0d12-148">There are 2 types of supported targets – Azure Storage accounts and Azure Media Services accounts.</span></span> <span data-ttu-id="a0d12-149">Выберите учетные записи хранения файлы tooput в большие двоичные объекты в этой учетной записи.</span><span class="sxs-lookup"><span data-stu-id="a0d12-149">Choose storage accounts tooput files into blobs in that account.</span></span> <span data-ttu-id="a0d12-150">Выберите файлы tooput учетной записи службы мультимедиа на средств в этой учетной записи.</span><span class="sxs-lookup"><span data-stu-id="a0d12-150">Choose media services account tooput files into assets in that account.</span></span> <span data-ttu-id="a0d12-151">Опять же мы должны tooadd репозитория.</span><span class="sxs-lookup"><span data-stu-id="a0d12-151">Again, we need tooadd a repository.</span></span> <span data-ttu-id="a0d12-152">Выберите в раскрывающемся списке hello, **добавить новую** и затем **настройки**.</span><span class="sxs-lookup"><span data-stu-id="a0d12-152">In hello dropdown, select **Add new** and then **Configure settings**.</span></span>

    ![Создание приемника данных](./media/storsimple-data-manager-ui/create-new-data-sink.png)

10. <span data-ttu-id="a0d12-154">Здесь можно выбрать тип hello требуется tooadd и hello другие параметры, связанные с репозиторием hello репозитория.</span><span class="sxs-lookup"><span data-stu-id="a0d12-154">Here, you can select hello type of repository you want tooadd and hello other parameters associated with hello repository.</span></span> <span data-ttu-id="a0d12-155">В обоих случаях очередь хранилища создается при запуске задания hello.</span><span class="sxs-lookup"><span data-stu-id="a0d12-155">In both cases, a storage queue is created when hello job runs.</span></span> <span data-ttu-id="a0d12-156">Эта очередь по мере готовности заполняется сообщениями о преобразованных больших двоичных объектах.</span><span class="sxs-lookup"><span data-stu-id="a0d12-156">This queue is populated with messages about transformed blobs as they are ready.</span></span> <span data-ttu-id="a0d12-157">имя этой очереди Hello hello совпадает с именем hello hello определения задания.</span><span class="sxs-lookup"><span data-stu-id="a0d12-157">hello name of this queue is hello same as hello name of hello job definition.</span></span> <span data-ttu-id="a0d12-158">При выборе **Media Services** как тип репозитория hello, затем можно ввести учетные данные учетной записи хранения которых создается очередь hello.</span><span class="sxs-lookup"><span data-stu-id="a0d12-158">If you select **Media Services** as hello repo type, then you can also enter storage account credentials where hello queue is created.</span></span>

    ![Сведения о новом приемнике данных](./media/storsimple-data-manager-ui/new-data-sink-details.png)

11. <span data-ttu-id="a0d12-160">После добавления репозитория данных hello (которая занимает несколько секунд), вы найдете hello репозитория в раскрывающемся списке hello в hello **имя учетной записи целевой**.</span><span class="sxs-lookup"><span data-stu-id="a0d12-160">After adding hello data repository (which takes a few seconds), you will find hello repo in hello dropdown in hello **Target account name**.</span></span>  <span data-ttu-id="a0d12-161">Выберите целевой объект hello нужны.</span><span class="sxs-lookup"><span data-stu-id="a0d12-161">Choose hello target that you need.</span></span>

12. <span data-ttu-id="a0d12-162">Нажмите кнопку **ОК** определение задания toocreate hello.</span><span class="sxs-lookup"><span data-stu-id="a0d12-162">Click **OK** toocreate hello job definition.</span></span> <span data-ttu-id="a0d12-163">Определение задания готово.</span><span class="sxs-lookup"><span data-stu-id="a0d12-163">Your job definition is now set up.</span></span> <span data-ttu-id="a0d12-164">Можно использовать это определение задания несколько раз через hello пользовательского интерфейса.</span><span class="sxs-lookup"><span data-stu-id="a0d12-164">You can use this job definition multiple times via hello UI.</span></span>

    ![Добавление определения задания](./media/storsimple-data-manager-ui/add-new-job-definition.png)

### <a name="run-hello-job-definition"></a><span data-ttu-id="a0d12-166">Запуск определения задания hello</span><span class="sxs-lookup"><span data-stu-id="a0d12-166">Run hello job definition</span></span>

<span data-ttu-id="a0d12-167">Каждый раз, когда требуются toomove данные из учетной записи хранилища StorSimple toohello, который указан в определении задания hello, вам потребуется tooinvoke его.</span><span class="sxs-lookup"><span data-stu-id="a0d12-167">Whenever you need toomove data from StorSimple toohello storage account that you have specified in hello job definition, you will need tooinvoke it.</span></span> <span data-ttu-id="a0d12-168">При изменении параметров hello каждый раз при вызове задания hello возможна определенная гибкость.</span><span class="sxs-lookup"><span data-stu-id="a0d12-168">There is some flexibility in changing hello parameters every time you invoke hello job.</span></span> <span data-ttu-id="a0d12-169">Ниже приведены шаги Hello.</span><span class="sxs-lookup"><span data-stu-id="a0d12-169">hello steps are as follows:</span></span>

1. <span data-ttu-id="a0d12-170">Выберите службы диспетчера StorSimple данных и щелкните слишком**мониторинг**.</span><span class="sxs-lookup"><span data-stu-id="a0d12-170">Select your StorSimple Data Manager service and go too**Monitoring**.</span></span> <span data-ttu-id="a0d12-171">Щелкните **Запустить сейчас**.</span><span class="sxs-lookup"><span data-stu-id="a0d12-171">Click **Run Now**.</span></span>

    ![Запуск определения задания](./media/storsimple-data-manager-ui/run-now.png)

2. <span data-ttu-id="a0d12-173">Выберите определение hello задания, которые должны toorun.</span><span class="sxs-lookup"><span data-stu-id="a0d12-173">Choose hello job definition that you want toorun.</span></span> <span data-ttu-id="a0d12-174">Нажмите кнопку **параметры запуска** toomodify все параметры, которые может потребоваться toochange для запуска этого задания.</span><span class="sxs-lookup"><span data-stu-id="a0d12-174">Click **Run settings** toomodify any settings that you might want toochange for this job run.</span></span>

    ![Параметры выполнения задания](./media/storsimple-data-manager-ui/run-settings.png)

3. <span data-ttu-id="a0d12-176">Нажмите кнопку **ОК** и нажмите кнопку **запуска** toolaunch вашу работу.</span><span class="sxs-lookup"><span data-stu-id="a0d12-176">Click **OK** and then click **Run** toolaunch your job.</span></span> <span data-ttu-id="a0d12-177">toomonitor этого задания, последовательно выберите toohello **заданий** страницы в диспетчер StorSimple данных.</span><span class="sxs-lookup"><span data-stu-id="a0d12-177">toomonitor this job, go toohello **Jobs** page in your StorSimple Data Manager.</span></span>

    ![Список заданий и состояние](./media/storsimple-data-manager-ui/jobs-list-and-status.png)

4. <span data-ttu-id="a0d12-179">В дополнение toomonitoring в hello **заданий** колонке воспроизведение также hello очереди хранилища, где добавляется сообщение каждый раз при перемещении файла из учетной записи хранения toohello StorSimple.</span><span class="sxs-lookup"><span data-stu-id="a0d12-179">In addition toomonitoring in hello **Jobs** blade, you can also listen on hello storage queue where a message is added every time a file is moved from StorSimple toohello storage account.</span></span>


## <a name="next-steps"></a><span data-ttu-id="a0d12-180">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="a0d12-180">Next steps</span></span>

<span data-ttu-id="a0d12-181">[Используйте диспетчер StorSimple данных задания .NET SDK toolaunch](storsimple-data-manager-dotnet-jobs.md).</span><span class="sxs-lookup"><span data-stu-id="a0d12-181">[Use .NET SDK toolaunch StorSimple Data Manager jobs](storsimple-data-manager-dotnet-jobs.md).</span></span>
