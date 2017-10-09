---
title: "aaaCreate и восстановление резервной копии в службах BizTalk | Документы Microsoft"
description: "Службы BizTalk включают в себя архивацию и восстановление. Узнайте, как toocreate определить, чего выполняется резервное копирование и восстановление резервной копии. MABS, WABS"
services: biztalk-services
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
ms.assetid: 59f91173-4683-48df-abd5-41262bfce6df
ms.service: biztalk-services
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/07/2016
ms.author: mandia
ms.openlocfilehash: 32356ad870678fa5fd5bbbbf13d9377188f770a1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="biztalk-services-backup-and-restore"></a><span data-ttu-id="cc832-105">Службы BizTalk: резервное копирование и восстановление</span><span class="sxs-lookup"><span data-stu-id="cc832-105">BizTalk Services: Backup and Restore</span></span>

> [!INCLUDE [BizTalk Services is being retired, and replaced with Azure Logic Apps](../../includes/biztalk-services-retirement.md)]

<span data-ttu-id="cc832-106">Службы Azure BizTalk предоставляют функции резервного копирования и восстановления.</span><span class="sxs-lookup"><span data-stu-id="cc832-106">Azure BizTalk Services includes Backup and Restore capabilities.</span></span> <span data-ttu-id="cc832-107">В этом разделе описывается, как toobackup и восстановление службы BizTalk с помощью hello классический портал Azure.</span><span class="sxs-lookup"><span data-stu-id="cc832-107">This topic describes how toobackup and restore BizTalk Services using hello Azure classic portal.</span></span>

<span data-ttu-id="cc832-108">Можно также выполнить резервное копирование службы BizTalk с помощью hello [API REST служб BizTalk](http://go.microsoft.com/fwlink/p/?LinkID=325584).</span><span class="sxs-lookup"><span data-stu-id="cc832-108">You can also back up BizTalk Services using hello [BizTalk Services REST API](http://go.microsoft.com/fwlink/p/?LinkID=325584).</span></span> 

> [!NOTE]
> <span data-ttu-id="cc832-109">Гибридные подключения не резервного копирования, независимо от того, hello выпуска.</span><span class="sxs-lookup"><span data-stu-id="cc832-109">Hybrid Connections are NOT backed up, regardless of hello Edition.</span></span> <span data-ttu-id="cc832-110">Гибридные подключения необходимо создать повторно.</span><span class="sxs-lookup"><span data-stu-id="cc832-110">You must recreate your hybrid connections.</span></span>


## <a name="before-you-begin"></a><span data-ttu-id="cc832-111">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="cc832-111">Before you Begin</span></span>
* <span data-ttu-id="cc832-112">Резервное копирование и восстановление доступны не во всех выпусках.</span><span class="sxs-lookup"><span data-stu-id="cc832-112">Backup and Restore may not be available for all editions.</span></span> <span data-ttu-id="cc832-113">Ознакомьтесь со статьей [Службы BizTalk: диаграмма выпусков](biztalk-editions-feature-chart.md).</span><span class="sxs-lookup"><span data-stu-id="cc832-113">See [BizTalk Services: Editions Chart](biztalk-editions-feature-chart.md).</span></span>
* <span data-ttu-id="cc832-114">Hello классический портал Azure можно создать резервную копию по требованию или архивации по расписанию.</span><span class="sxs-lookup"><span data-stu-id="cc832-114">Using hello Azure classic portal, you can create an On Demand backup or create a scheduled backup.</span></span> 
* <span data-ttu-id="cc832-115">Содержимое резервной копии может быть восстановленной toohello же службы BizTalk или tooa новую службу BizTalk.</span><span class="sxs-lookup"><span data-stu-id="cc832-115">Backup content can be restored toohello same BizTalk Service or tooa new BizTalk Service.</span></span> <span data-ttu-id="cc832-116">toorestore hello службы BizTalk с помощью hello таким же именем, hello существующей службы BizTalk необходимо удалить, и должно быть доступно имя hello.</span><span class="sxs-lookup"><span data-stu-id="cc832-116">toorestore hello BizTalk Service using hello same name, hello existing BizTalk Service must be deleted and hello name must be available.</span></span> <span data-ttu-id="cc832-117">После удаления службы BizTalk, она может занять больше времени, чем требуется для hello таким же именем toobe доступны.</span><span class="sxs-lookup"><span data-stu-id="cc832-117">After you delete a BizTalk Service, it can take longer time than wanted for hello same name toobe available.</span></span> <span data-ttu-id="cc832-118">Если не может ожидать hello же имя toobe доступен, а затем восстановить tooa новую службу BizTalk.</span><span class="sxs-lookup"><span data-stu-id="cc832-118">If you cannot wait for hello same name toobe available, then restore tooa new BizTalk Service.</span></span>
* <span data-ttu-id="cc832-119">Службы BizTalk может быть восстановленной toohello же выпуск и выпуск более высокого уровня.</span><span class="sxs-lookup"><span data-stu-id="cc832-119">BizTalk Services can be restored toohello same edition or a higher edition.</span></span> <span data-ttu-id="cc832-120">Восстановление службы BizTalk tooa выпуск ниже, при создании резервной копии hello использовался, не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="cc832-120">Restoring BizTalk Services tooa lower edition, from when hello backup was taken, is not supported.</span></span>
  
    <span data-ttu-id="cc832-121">Например резервной копии с помощью hello выпуск Basic можно восстановить toohello выпуска Premium.</span><span class="sxs-lookup"><span data-stu-id="cc832-121">For example, a backup using hello Basic Edition can be restored toohello Premium Edition.</span></span> <span data-ttu-id="cc832-122">Восстановление резервной копии с помощью hello Premium Edition не может быть toohello Standard Edition.</span><span class="sxs-lookup"><span data-stu-id="cc832-122">A backup using hello Premium Edition cannot be restored toohello Standard Edition.</span></span>
* <span data-ttu-id="cc832-123">номера управления EDI Hello архивируются toomaintain непрерывность hello контрольных чисел.</span><span class="sxs-lookup"><span data-stu-id="cc832-123">hello EDI Control numbers are backed up toomaintain continuity of hello control numbers.</span></span> <span data-ttu-id="cc832-124">Если сообщения обрабатываются после последнего резервного копирования hello, восстановление этой резервной копии содержимого может привести к повторяющихся контрольных чисел.</span><span class="sxs-lookup"><span data-stu-id="cc832-124">If messages are processed after hello last backup, restoring this backup content can cause duplicate control numbers.</span></span>
* <span data-ttu-id="cc832-125">Если пакет содержит активных сообщений, обработки пакета hello **перед** резервного копирования.</span><span class="sxs-lookup"><span data-stu-id="cc832-125">If a batch has active messages, process hello batch **before** running a backup.</span></span> <span data-ttu-id="cc832-126">При создании резервной копии (запланированной или по требованию) сообщения в пакетах не сохраняются.</span><span class="sxs-lookup"><span data-stu-id="cc832-126">When creating a backup (as needed or scheduled), messages in batches are never stored.</span></span> 
  
    <span data-ttu-id="cc832-127">**Если на момент начала резервного копирования в пакете присутствуют активные сообщения, они не копируются и будут утрачены.**</span><span class="sxs-lookup"><span data-stu-id="cc832-127">**If a backup is taken with active messages in a batch, these messages are not backed up and are therefore lost.**</span></span>
* <span data-ttu-id="cc832-128">Необязательно: В hello портале служб BizTalk, остановите все операции управления.</span><span class="sxs-lookup"><span data-stu-id="cc832-128">Optional: In hello BizTalk Services Portal, stop any management operations.</span></span>

## <a name="create-a-backup"></a><span data-ttu-id="cc832-129">Создание резервной копии</span><span class="sxs-lookup"><span data-stu-id="cc832-129">Create a backup</span></span>
<span data-ttu-id="cc832-130">Резервное копирование может выполняться в любое время — вы полностью управляете этим процессом.</span><span class="sxs-lookup"><span data-stu-id="cc832-130">A backup can be taken at any time and is completely controlled by you.</span></span> <span data-ttu-id="cc832-131">В этом разделе перечислены hello действия toocreate резервные копии с помощью hello Azure классического портала, включая:</span><span class="sxs-lookup"><span data-stu-id="cc832-131">This section lists hello steps toocreate backups using hello Azure classic portal, including:</span></span>

[<span data-ttu-id="cc832-132">Резервное копирование по запросу</span><span class="sxs-lookup"><span data-stu-id="cc832-132">On Demand backup</span></span>](#backupnow)

[<span data-ttu-id="cc832-133">Планирование резервного копирования</span><span class="sxs-lookup"><span data-stu-id="cc832-133">Schedule a backup</span></span>](#backupschedule)

#### <span data-ttu-id="cc832-134"><a name="backupnow"></a>Резервное копирование по запросу</span><span class="sxs-lookup"><span data-stu-id="cc832-134"><a name="backupnow"></a>On Demand backup</span></span>
1. <span data-ttu-id="cc832-135">В hello классический портал Azure, выберите **службы BizTalk**, а затем выберите hello требуется toobackup службы BizTalk.</span><span class="sxs-lookup"><span data-stu-id="cc832-135">In hello Azure classic portal, select **BizTalk Services**, and then select hello BizTalk Service you want toobackup.</span></span>
2. <span data-ttu-id="cc832-136">В hello **мониторинга** выберите **резервное копирование** hello нижней части страницы приветствия.</span><span class="sxs-lookup"><span data-stu-id="cc832-136">In hello **Dashboard** tab, select **Back up** at hello bottom of hello page.</span></span>
3. <span data-ttu-id="cc832-137">Задайте имя резервной копии.</span><span class="sxs-lookup"><span data-stu-id="cc832-137">Enter a backup name.</span></span> <span data-ttu-id="cc832-138">Например, введите *моя_служба_BizTalk*РК*Дата*.</span><span class="sxs-lookup"><span data-stu-id="cc832-138">For example, enter *myBizTalkService*BU*Date*.</span></span>
4. <span data-ttu-id="cc832-139">Выберите учетную запись хранилища больших двоичных объектов и выберите hello флажок toostart hello архивации.</span><span class="sxs-lookup"><span data-stu-id="cc832-139">Choose a blob storage account and select hello checkmark toostart hello backup.</span></span>

<span data-ttu-id="cc832-140">После завершения резервного копирования hello в учетной записи хранения hello создается контейнер с именем резервного копирования Привет вводимых вами.</span><span class="sxs-lookup"><span data-stu-id="cc832-140">Once hello backup completes, a container with hello backup name you enter is created in hello storage account.</span></span> <span data-ttu-id="cc832-141">В этом контейнере содержится резервная копия конфигурации службы BizTalk.</span><span class="sxs-lookup"><span data-stu-id="cc832-141">This container contains your BizTalk Service backup configuration.</span></span>

#### <span data-ttu-id="cc832-142"><a name="backupschedule"></a>Планирование резервного копирования</span><span class="sxs-lookup"><span data-stu-id="cc832-142"><a name="backupschedule"></a>Schedule a backup</span></span>
1. <span data-ttu-id="cc832-143">В hello классический портал Azure, выберите **службы BizTalk**, Здравствуйте, выберите имя службы BizTalk вы tooschedule hello архивация, а затем выберите hello **Настройка** вкладки.</span><span class="sxs-lookup"><span data-stu-id="cc832-143">In hello Azure classic portal, select **BizTalk Services**, select hello BizTalk Service name you want tooschedule hello backup, and then select hello **Configure** tab.</span></span>
2. <span data-ttu-id="cc832-144">Набор hello **состояние архивации** слишком**автоматического**.</span><span class="sxs-lookup"><span data-stu-id="cc832-144">Set hello **Backup Status** too**Automatic**.</span></span> 
3. <span data-ttu-id="cc832-145">Выберите hello **учетной записи хранилища** toostore Здравствуйте резервного копирования, введите hello **частоты** toocreate hello резервных копий и как долго tookeep hello (**дней хранения**):</span><span class="sxs-lookup"><span data-stu-id="cc832-145">Select hello **Storage Account** toostore hello backup, enter hello **Frequency** toocreate hello backups, and how long tookeep hello backups (**Retention Days**):</span></span>
   
    ![][AutomaticBU]
   
    <span data-ttu-id="cc832-146">**Примечания**</span><span class="sxs-lookup"><span data-stu-id="cc832-146">**Notes**</span></span>     
   
   * <span data-ttu-id="cc832-147">В **дней хранения**, срок хранения hello должен быть больше частоты архивации hello.</span><span class="sxs-lookup"><span data-stu-id="cc832-147">In **Retention Days**, hello retention period must be greater than hello backup frequency.</span></span>
   * <span data-ttu-id="cc832-148">Выберите **всегда сохранять по крайней мере один архив**, даже если он находится за пределами срока хранения hello.</span><span class="sxs-lookup"><span data-stu-id="cc832-148">Select **Always keep at least one backup**, even if it is past hello retention period.</span></span>
4. <span data-ttu-id="cc832-149">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="cc832-149">Select **Save**.</span></span>

<span data-ttu-id="cc832-150">При запуске задания архивации, он создает контейнер (toostore резервного копирования данных) в учетной записи хранения hello введенный.</span><span class="sxs-lookup"><span data-stu-id="cc832-150">When a scheduled backup job runs, it creates a container (toostore backup data) in hello storage account you entered.</span></span> <span data-ttu-id="cc832-151">Hello имя контейнера hello называется *имя службы BizTalk-Дата время*.</span><span class="sxs-lookup"><span data-stu-id="cc832-151">hello name of hello container is named *BizTalk Service Name-date-time*.</span></span> 

<span data-ttu-id="cc832-152">Если отображается панель мониторинга службы BizTalk hello **сбой** состояния:</span><span class="sxs-lookup"><span data-stu-id="cc832-152">If hello BizTalk Service dashboard shows a **Failed** status:</span></span>

![Состояние последней запланированной архивации][BackupStatus] 

<span data-ttu-id="cc832-154">будет открыта ссылка Hello hello Устранение toohelp журналы операций службы управления.</span><span class="sxs-lookup"><span data-stu-id="cc832-154">hello link opens hello Management Services Operation Logs toohelp troubleshoot.</span></span> <span data-ttu-id="cc832-155">Ознакомьтесь со статьей [Службы BizTalk: устранение неполадок с помощью журналов операций](http://go.microsoft.com/fwlink/p/?LinkId=391211).</span><span class="sxs-lookup"><span data-stu-id="cc832-155">See [BizTalk Services: Troubleshoot using operation logs](http://go.microsoft.com/fwlink/p/?LinkId=391211).</span></span>

## <a name="restore"></a><span data-ttu-id="cc832-156">восстановление;</span><span class="sxs-lookup"><span data-stu-id="cc832-156">Restore</span></span>
<span data-ttu-id="cc832-157">Можно восстанавливать резервные копии из hello классический портал Azure или hello [восстановить API REST службы BizTalk](http://go.microsoft.com/fwlink/p/?LinkID=325582).</span><span class="sxs-lookup"><span data-stu-id="cc832-157">You can restore backups from hello Azure classic portal or from hello [Restore BizTalk Service REST API](http://go.microsoft.com/fwlink/p/?LinkID=325582).</span></span> <span data-ttu-id="cc832-158">В этом разделе перечислены шаги toorestore hello, с помощью классического портала hello.</span><span class="sxs-lookup"><span data-stu-id="cc832-158">This section lists hello steps toorestore using hello classic portal.</span></span>

#### <a name="before-restoring-a-backup"></a><span data-ttu-id="cc832-159">Подготовка к восстановлению из резервной копии</span><span class="sxs-lookup"><span data-stu-id="cc832-159">Before restoring a backup</span></span>
* <span data-ttu-id="cc832-160">При восстановлении службы BizTalk можно указать новые хранилища отслеживания, архивации и мониторинга.</span><span class="sxs-lookup"><span data-stu-id="cc832-160">New tracking, archiving, and monitoring stores can be entered while restoring a BizTalk Service.</span></span>
* <span data-ttu-id="cc832-161">Здравствуйте, восстанавливается и те же данные среды выполнения EDI.</span><span class="sxs-lookup"><span data-stu-id="cc832-161">hello same EDI Runtime data is restored.</span></span> <span data-ttu-id="cc832-162">резервная копия среды выполнения EDI Hello числа hello элемента управления.</span><span class="sxs-lookup"><span data-stu-id="cc832-162">hello EDI Runtime backup stores hello control numbers.</span></span> <span data-ttu-id="cc832-163">номера управления Hello восстановления находятся в последовательности из hello время резервного копирования hello.</span><span class="sxs-lookup"><span data-stu-id="cc832-163">hello restored control numbers are in sequence from hello time of hello backup.</span></span> <span data-ttu-id="cc832-164">Если сообщения обрабатываются после последнего резервного копирования hello, восстановление этой резервной копии содержимого может привести к повторяющихся контрольных чисел.</span><span class="sxs-lookup"><span data-stu-id="cc832-164">If messages are processed after hello last backup, restoring this backup content can cause duplicate control numbers.</span></span>

#### <a name="restore-a-backup"></a><span data-ttu-id="cc832-165">Восстановление из резервной копии</span><span class="sxs-lookup"><span data-stu-id="cc832-165">Restore a backup</span></span>
1. <span data-ttu-id="cc832-166">В hello классический портал Azure, выберите **New** > **службы приложений** > **службы BizTalk** > **восстановления** :</span><span class="sxs-lookup"><span data-stu-id="cc832-166">In hello Azure classic portal, select **New** > **App Services** > **BizTalk Service** > **Restore**:</span></span>
   
    ![Восстановление из резервной копии][Restore]
2. <span data-ttu-id="cc832-168">В **резервного копирования URL-адрес**, выберите значок папки hello и разверните hello учетной записи хранилища Azure, сохраняет hello архив конфигурации службы BizTalk.</span><span class="sxs-lookup"><span data-stu-id="cc832-168">In **Backup URL**, select hello folder icon and expand hello Azure storage account that stores hello BizTalk Service configuration backup.</span></span> <span data-ttu-id="cc832-169">Разверните контейнер hello и hello правой панели выберите hello, соответствующий резервное копирование txt-файл.</span><span class="sxs-lookup"><span data-stu-id="cc832-169">Expand hello container and in hello right pane, select hello corresponding back up .txt file.</span></span> 
   <br/><br/>
   <span data-ttu-id="cc832-170">Щелкните **Open**(Открыть).</span><span class="sxs-lookup"><span data-stu-id="cc832-170">Select **Open**.</span></span>
3. <span data-ttu-id="cc832-171">На hello **Восстановление службы BizTalk** введите **имя службы BizTalk** и проверьте hello **URL-адрес домена**, **выпуск**и **Регион** для hello восстановить службу BizTalk.</span><span class="sxs-lookup"><span data-stu-id="cc832-171">On hello **Restore BizTalk Service** page, enter a **BizTalk Service Name** and verify hello **Domain URL**, **Edition**, and **Region** for hello restored BizTalk Service.</span></span> <span data-ttu-id="cc832-172">**Создать новый экземпляр базы данных SQL** для hello отслеживания базы данных:</span><span class="sxs-lookup"><span data-stu-id="cc832-172">**Create a new SQL database instance** for hello tracking database:</span></span>
   
    ![][RestoreBizTalkService]
   
    <span data-ttu-id="cc832-173">Выберите стрелку hello.</span><span class="sxs-lookup"><span data-stu-id="cc832-173">Select hello next arrow.</span></span>
4. <span data-ttu-id="cc832-174">Проверьте имя базы данных SQL hello hello, введите hello физическом сервере, где будет создана база данных SQL hello и имя пользователя и пароль для этого сервера.</span><span class="sxs-lookup"><span data-stu-id="cc832-174">Verify hello name of hello SQL database, enter hello physical server where hello SQL database will be created, and a username/password for that server.</span></span>

    <span data-ttu-id="cc832-175">Выпуск базы данных SQL tooconfigure hello, размер и другие свойства, установите **настроить дополнительные параметры базы данных**.</span><span class="sxs-lookup"><span data-stu-id="cc832-175">If you want tooconfigure hello SQL database edition, size, and other properties, select  **Configure Advanced Database Settings**.</span></span> 

    <span data-ttu-id="cc832-176">Выберите стрелку hello.</span><span class="sxs-lookup"><span data-stu-id="cc832-176">Select hello next arrow.</span></span>

1. <span data-ttu-id="cc832-177">Создание учетной записи хранилища или введите существующую учетную запись хранения для hello службы BizTalk.</span><span class="sxs-lookup"><span data-stu-id="cc832-177">Create a new storage account or enter an existing storage account for hello BizTalk Service.</span></span>
2. <span data-ttu-id="cc832-178">Выберите hello флажок toostart hello восстановления.</span><span class="sxs-lookup"><span data-stu-id="cc832-178">Select hello checkmark toostart hello restore.</span></span>

<span data-ttu-id="cc832-179">После успешного завершения восстановления hello новой службы BizTalk указывается в приостановленном состоянии на странице приветствия службы BizTalk в hello классический портал Azure.</span><span class="sxs-lookup"><span data-stu-id="cc832-179">Once hello restoration successfully completes, a new BizTalk Service is listed in a suspended state on hello BizTalk Services page in hello Azure classic portal.</span></span>

### <span data-ttu-id="cc832-180"><a name="postrestore"></a>Действия после восстановления из резервной копии</span><span class="sxs-lookup"><span data-stu-id="cc832-180"><a name="postrestore"></a>After restoring a backup</span></span>
<span data-ttu-id="cc832-181">Hello службы BizTalk всегда восстанавливается в **Suspended** состояния.</span><span class="sxs-lookup"><span data-stu-id="cc832-181">hello BizTalk Service is always restored in a **Suspended** state.</span></span> <span data-ttu-id="cc832-182">В этом состоянии перед hello новую среду работы, включая можно внести изменения в конфигурацию:</span><span class="sxs-lookup"><span data-stu-id="cc832-182">In this state, you can make any configuration changes before hello new environment is functional, including:</span></span>

* <span data-ttu-id="cc832-183">При создании приложения службы BizTalk с помощью пакета SDK служб BizTalk Azure hello, может потребоваться tootooupdate hello управления доступом (ACS) и учетные данные в toowork этих приложений с помощью среды восстановления hello.</span><span class="sxs-lookup"><span data-stu-id="cc832-183">If you created BizTalk Service applications using hello Azure BizTalk Services SDK, you may need tootooupdate hello Access Control (ACS) credentials in those applications toowork with hello restored environment.</span></span>
* <span data-ttu-id="cc832-184">Необходимо восстановить службу BizTalk tooreplicate существующую среду службы BizTalk.</span><span class="sxs-lookup"><span data-stu-id="cc832-184">You restore a BizTalk Service tooreplicate an existing BizTalk Service environment.</span></span> <span data-ttu-id="cc832-185">Если имеются соглашения, настроены на портале служб BizTalk исходного hello, использующих FTP исходной папки, в этом случае может потребоваться tooupdate соглашения hello в среде hello недавно восстановленных toouse другой исходной папки FTP.</span><span class="sxs-lookup"><span data-stu-id="cc832-185">In this situation, if there are agreements configured in hello original BizTalk Services portal that use a source FTP folder, you may need tooupdate hello agreements in hello newly restored environment toouse a different source FTP folder.</span></span> <span data-ttu-id="cc832-186">В противном случае возможны два различных соглашений о попытке toopull hello одного сообщения.</span><span class="sxs-lookup"><span data-stu-id="cc832-186">Otherwise, there may be two different agreements trying toopull hello same message.</span></span>
* <span data-ttu-id="cc832-187">Если восстановить toohave несколько сред службы BizTalk, убедитесь, что целевая среда hello в Visual Studio приложения hello, командлеты PowerShell, API-интерфейс REST или торгового партнера OM API-интерфейсы управления.</span><span class="sxs-lookup"><span data-stu-id="cc832-187">If you restored toohave multiple BizTalk Service environments, make sure you target hello correct environment in hello Visual Studio applications, PowerShell cmdlets, REST APIs, or Trading Partner Management OM APIs.</span></span>
* <span data-ttu-id="cc832-188">Он является хорошей практикой tooconfigure автоматических резервных копий на недавно восстановленных hello среды службы BizTalk.</span><span class="sxs-lookup"><span data-stu-id="cc832-188">It's a good practice tooconfigure automated backups on hello newly restored BizTalk Service environment.</span></span>

<span data-ttu-id="cc832-189">hello toostart службы BizTalk в hello классический портал Azure, выберите hello восстановить службу BizTalk и выберите **Resume** на панели задач hello.</span><span class="sxs-lookup"><span data-stu-id="cc832-189">toostart hello BizTalk Service in hello Azure classic portal, select hello restored BizTalk Service and select **Resume** in hello task bar.</span></span> 

## <a name="what-gets-backed-up"></a><span data-ttu-id="cc832-190">Что входит в резервную копию</span><span class="sxs-lookup"><span data-stu-id="cc832-190">What gets backed up</span></span>
<span data-ttu-id="cc832-191">При создании резервной копии hello следующие элементы создаются резервные копии:</span><span class="sxs-lookup"><span data-stu-id="cc832-191">When a backup is created, hello following items are backed up:</span></span>

<table border="1"> 
<tr bgcolor="FAF9F9">
<th> </th>
<TH><span data-ttu-id="cc832-192">Элементы, включаемые в резервную копию</span><span class="sxs-lookup"><span data-stu-id="cc832-192">Items backed up</span></span></TH> 
</tr> 
<tr>
<td colspan="2"><span data-ttu-id="cc832-193">
 <strong>Портал служб BizTalk Azure</strong></span><span class="sxs-lookup"><span data-stu-id="cc832-193">
 <strong>Azure BizTalk Services Portal</strong></span></span></td>
</tr> 
<tr>
<td><span data-ttu-id="cc832-194">Конфигурация и среда выполнения</span><span class="sxs-lookup"><span data-stu-id="cc832-194">Configuration and Runtime</span></span></td> 
<td>
<ul>
<li><span data-ttu-id="cc832-195">Сведения о партнере и данные профиля</span><span class="sxs-lookup"><span data-stu-id="cc832-195">Partner and profile details</span></span></li>
<li><span data-ttu-id="cc832-196">Партнерские соглашения</span><span class="sxs-lookup"><span data-stu-id="cc832-196">Partner Agreements</span></span></li>
<li><span data-ttu-id="cc832-197">Развернутые пользовательские сборки</span><span class="sxs-lookup"><span data-stu-id="cc832-197">Custom assemblies deployed</span></span></li>
<li><span data-ttu-id="cc832-198">Развернутые мосты</span><span class="sxs-lookup"><span data-stu-id="cc832-198">Bridges deployed</span></span></li>
<li><span data-ttu-id="cc832-199">Сертификаты</span><span class="sxs-lookup"><span data-stu-id="cc832-199">Certificates</span></span></li>
<li><span data-ttu-id="cc832-200">Развернутые преобразования</span><span class="sxs-lookup"><span data-stu-id="cc832-200">Transforms deployed</span></span></li>
<li><span data-ttu-id="cc832-201">Конвейеры</span><span class="sxs-lookup"><span data-stu-id="cc832-201">Pipelines</span></span></li>
<li><span data-ttu-id="cc832-202">Шаблоны, созданные и сохраненные в hello портале служб BizTalk</span><span class="sxs-lookup"><span data-stu-id="cc832-202">Templates created and saved in hello BizTalk Services Portal</span></span></li>
<li><span data-ttu-id="cc832-203">Сопоставления X12 ST01 и GS01</span><span class="sxs-lookup"><span data-stu-id="cc832-203">X12 ST01 and GS01 mappings</span></span></li>
<li><span data-ttu-id="cc832-204">Контрольные номера (EDI)</span><span class="sxs-lookup"><span data-stu-id="cc832-204">Control numbers (EDI)</span></span></li>
<li><span data-ttu-id="cc832-205">Значения MIC сообщения AS2</span><span class="sxs-lookup"><span data-stu-id="cc832-205">AS2 Message MIC values</span></span></li>
</ul>
</td>
</tr> 

<tr>
<td colspan="2"><span data-ttu-id="cc832-206">
 <strong>Служба BizTalk Azure</strong></span><span class="sxs-lookup"><span data-stu-id="cc832-206">
 <strong>Azure BizTalk Service</strong></span></span></td>
</tr> 
<tr>
<td><span data-ttu-id="cc832-207">Сертификат SSL</span><span class="sxs-lookup"><span data-stu-id="cc832-207">SSL Certificate</span></span></td> 
<td>
<ul>
<li><span data-ttu-id="cc832-208">Данные сертификата SSL</span><span class="sxs-lookup"><span data-stu-id="cc832-208">SSL Certificate Data</span></span></li>
<li><span data-ttu-id="cc832-209">Пароль сертификата SSL</span><span class="sxs-lookup"><span data-stu-id="cc832-209">SSL Certificate Password</span></span></li>
</ul>
</td>
</tr> 
<tr>
<td><span data-ttu-id="cc832-210">Параметры службы BizTalk</span><span class="sxs-lookup"><span data-stu-id="cc832-210">BizTalk Service Settings</span></span></td> 
<td>
<ul>
<li><span data-ttu-id="cc832-211">Число модулей масштабирования</span><span class="sxs-lookup"><span data-stu-id="cc832-211">Scale unit count</span></span></li>
<li><span data-ttu-id="cc832-212">Выпуск</span><span class="sxs-lookup"><span data-stu-id="cc832-212">Edition</span></span></li>
<li><span data-ttu-id="cc832-213">Версия продукта</span><span class="sxs-lookup"><span data-stu-id="cc832-213">Product Version</span></span></li>
<li><span data-ttu-id="cc832-214">Регион и центр обработки данных</span><span class="sxs-lookup"><span data-stu-id="cc832-214">Region/Datacenter</span></span></li>
<li><span data-ttu-id="cc832-215">Ключ и пространство имен службы контроля доступа (ACS)</span><span class="sxs-lookup"><span data-stu-id="cc832-215">Access Control Service (ACS) namespace and key</span></span></li>
<li><span data-ttu-id="cc832-216">Строка подключения к базе данных отслеживания</span><span class="sxs-lookup"><span data-stu-id="cc832-216">Tracking database connection string</span></span></li>
<li><span data-ttu-id="cc832-217">Строка подключения учетной записи хранения для архивации</span><span class="sxs-lookup"><span data-stu-id="cc832-217">Archiving Storage account connection string</span></span></li>
<li><span data-ttu-id="cc832-218">Строка подключения учетной записи хранения для мониторинга</span><span class="sxs-lookup"><span data-stu-id="cc832-218">Monitoring storage account connection string</span></span></li>
</ul>
</td>
</tr> 
<tr>
<td colspan="2"><span data-ttu-id="cc832-219">
 <strong>Дополнительные элементы</strong></span><span class="sxs-lookup"><span data-stu-id="cc832-219">
 <strong>Additional Items</strong></span></span></td>
</tr> 
<tr>
<td><span data-ttu-id="cc832-220">База данных отслеживания</span><span class="sxs-lookup"><span data-stu-id="cc832-220">Tracking Database</span></span></td> 
<td><span data-ttu-id="cc832-221">При создании службы BizTalk hello вводятся сведения о базе данных, отслеживание hello, включая hello сервера базы данных SQL Azure и имя базы данных отслеживания hello.</span><span class="sxs-lookup"><span data-stu-id="cc832-221">When hello BizTalk Service is created, hello Tracking Database details are entered, including hello Azure SQL Database Server and hello Tracking Database name.</span></span> <span data-ttu-id="cc832-222">База данных отслеживания Hello не автоматическое резервное копирование.</span><span class="sxs-lookup"><span data-stu-id="cc832-222">hello Tracking Database is not automatically backed up.</span></span>
<br/><br/><span data-ttu-id="cc832-223">
<strong>Важно!</strong></span><span class="sxs-lookup"><span data-stu-id="cc832-223">
<strong>Important</strong></span></span><br/>
<span data-ttu-id="cc832-224">Если hello базы данных отслеживания удаляется и hello требованиям базы данных восстановлена, должны существовать предыдущей резервной копии.</span><span class="sxs-lookup"><span data-stu-id="cc832-224">If hello Tracking Database is deleted and hello database needs recovered, a previous backup must exist.</span></span> <span data-ttu-id="cc832-225">Если резервной копии не существует, hello базы данных отслеживания и его данные, восстановить невозможно.</span><span class="sxs-lookup"><span data-stu-id="cc832-225">If a backup does not exist, hello Tracking Database and its data are not recoverable.</span></span> <span data-ttu-id="cc832-226">В этом случае можно создать новую базу данных отслеживания с hello имя базы данных.</span><span class="sxs-lookup"><span data-stu-id="cc832-226">In this situation, create a new Tracking Database with hello same database name.</span></span> <span data-ttu-id="cc832-227">Рекомендуется использовать георепликацию.</span><span class="sxs-lookup"><span data-stu-id="cc832-227">Geo-Replication is recommended.</span></span></td>
</tr> 
</table>

## <a name="next"></a><span data-ttu-id="cc832-228">Далее</span><span class="sxs-lookup"><span data-stu-id="cc832-228">Next</span></span>
<span data-ttu-id="cc832-229">Службы BizTalk Azure toocreate в hello Azure классического портала, go слишком[службы BizTalk: Подготовка Azure с помощью классического портала](http://go.microsoft.com/fwlink/p/?LinkID=302280).</span><span class="sxs-lookup"><span data-stu-id="cc832-229">toocreate Azure BizTalk Services in hello Azure classic portal, go too[BizTalk Services: Provisioning Using Azure classic portal](http://go.microsoft.com/fwlink/p/?LinkID=302280).</span></span> <span data-ttu-id="cc832-230">Создание приложений, перейдите в слишком toostart[служб Azure BizTalk](http://go.microsoft.com/fwlink/p/?LinkID=235197).</span><span class="sxs-lookup"><span data-stu-id="cc832-230">toostart creating applications, go too[Azure BizTalk Services](http://go.microsoft.com/fwlink/p/?LinkID=235197).</span></span>

## <a name="see-also"></a><span data-ttu-id="cc832-231">См. также</span><span class="sxs-lookup"><span data-stu-id="cc832-231">See Also</span></span>
* [<span data-ttu-id="cc832-232">Резервное копирование службы BizTalk</span><span class="sxs-lookup"><span data-stu-id="cc832-232">Backup BizTalk Service</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=325584)
* [<span data-ttu-id="cc832-233">Восстановление службы BizTalk из резервной копии</span><span class="sxs-lookup"><span data-stu-id="cc832-233">Restore BizTalk Service from Backup</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=325582)
* [<span data-ttu-id="cc832-234">Службы BizTalk. Диаграмма выпусков Developer, Basic, Standard и Premium</span><span class="sxs-lookup"><span data-stu-id="cc832-234">BizTalk Services: Developer, Basic, Standard and Premium Editions Chart</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302279)
* [<span data-ttu-id="cc832-235">Службы BizTalk: подготовка с использованием классического портала Azure</span><span class="sxs-lookup"><span data-stu-id="cc832-235">BizTalk Services: Provisioning Using Azure classic portal</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302280)
* [<span data-ttu-id="cc832-236">Службы BizTalk. Диаграмма состояния подготовки</span><span class="sxs-lookup"><span data-stu-id="cc832-236">BizTalk Services: Provisioning Status Chart</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=329870)
* [<span data-ttu-id="cc832-237">Службы BizTalk: вкладки «Панель мониторинга», «Монитор» и «Масштаб»</span><span class="sxs-lookup"><span data-stu-id="cc832-237">BizTalk Services: Dashboard, Monitor and Scale tabs</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302281)
* [<span data-ttu-id="cc832-238">Службы BizTalk: регулирование</span><span class="sxs-lookup"><span data-stu-id="cc832-238">BizTalk Services: Throttling</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302282)
* [<span data-ttu-id="cc832-239">Службы BizTalk: имя и ключ издателя</span><span class="sxs-lookup"><span data-stu-id="cc832-239">BizTalk Services: Issuer Name and Issuer Key</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=303941)
* [<span data-ttu-id="cc832-240">Как я запустить с помощью hello пакета SDK служб BizTalk Azure</span><span class="sxs-lookup"><span data-stu-id="cc832-240">How do I Start Using hello Azure BizTalk Services SDK</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302335)

[BackupStatus]: ./media/biztalk-backup-restore/status-last-backup.png
[Restore]: ./media/biztalk-backup-restore/restore-ui.png
[AutomaticBU]: ./media/biztalk-backup-restore/AutomaticBU.png
[RestoreBizTalkService]: ./media/biztalk-backup-restore/RestoreBizTalkServiceWindow.png

