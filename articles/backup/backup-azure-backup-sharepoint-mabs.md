---
title: "tooback сервера aaaUse резервное копирование фермы SharePoint tooAzure | Документы Microsoft"
description: "Используйте tooback Azure резервное копирование и восстановление данных SharePoint. Эта статья содержит сведения tooconfigure hello фермы SharePoint, чтобы необходимые данные могут храниться в Azure. Защищенные данные SharePoint можно восстановить с диска или из Azure."
services: backup
documentationcenter: 
author: pvrk
manager: shivamg
editor: 
ms.assetid: 34ba87a4-91f1-4054-a4a1-272af1e15496
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: pullabhk
ms.openlocfilehash: 350c1ac0f3518f400062f3b586bbe9710a79915a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="back-up-a-sharepoint-farm-tooazure"></a><span data-ttu-id="28b05-105">Резервное копирование фермы SharePoint tooAzure</span><span class="sxs-lookup"><span data-stu-id="28b05-105">Back up a SharePoint farm tooAzure</span></span>
<span data-ttu-id="28b05-106">Резервное копирование SharePoint фермы tooMicrosoft Azure с помощью сервера архивации Microsoft Azure (MABS) в много hello так же, резервное копирование других источников данных.</span><span class="sxs-lookup"><span data-stu-id="28b05-106">You back up a SharePoint farm tooMicrosoft Azure by using Microsoft Azure Backup Server (MABS) in much hello same way that you back up other data sources.</span></span> <span data-ttu-id="28b05-107">Резервное копирование Azure обеспечивает гибкость в toocreate hello расписание резервного копирования ежедневно, еженедельно, ежемесячно или ежегодно точки резервного копирования и предоставляет параметры политики хранения для различных точках рабочего процесса резервного копирования.</span><span class="sxs-lookup"><span data-stu-id="28b05-107">Azure Backup provides flexibility in hello backup schedule toocreate daily, weekly, monthly, or yearly backup points and gives you retention policy options for various backup points.</span></span> <span data-ttu-id="28b05-108">Он также предоставляет hello возможность toostore локальный диск копий для целей быстрое время восстановления (RTO) и toostore копирует tooAzure экономичной, долгосрочного хранения.</span><span class="sxs-lookup"><span data-stu-id="28b05-108">It also provides hello capability toostore local disk copies for quick recovery-time objectives (RTO) and toostore copies tooAzure for economical, long-term retention.</span></span>

## <a name="sharepoint-supported-versions-and-related-protection-scenarios"></a><span data-ttu-id="28b05-109">Поддерживаемые версии SharePoint и соответствующие сценарии защиты</span><span class="sxs-lookup"><span data-stu-id="28b05-109">SharePoint supported versions and related protection scenarios</span></span>
<span data-ttu-id="28b05-110">Azure Backup для DPM поддерживает следующие сценарии hello:</span><span class="sxs-lookup"><span data-stu-id="28b05-110">Azure Backup for DPM supports hello following scenarios:</span></span>

| <span data-ttu-id="28b05-111">Рабочая нагрузка</span><span class="sxs-lookup"><span data-stu-id="28b05-111">Workload</span></span> | <span data-ttu-id="28b05-112">Версия</span><span class="sxs-lookup"><span data-stu-id="28b05-112">Version</span></span> | <span data-ttu-id="28b05-113">Развертывание SharePoint</span><span class="sxs-lookup"><span data-stu-id="28b05-113">SharePoint deployment</span></span> | <span data-ttu-id="28b05-114">Защита и восстановление</span><span class="sxs-lookup"><span data-stu-id="28b05-114">Protection and recovery</span></span> |
| --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="28b05-115">SharePoint</span><span class="sxs-lookup"><span data-stu-id="28b05-115">SharePoint</span></span> |<span data-ttu-id="28b05-116">SharePoint 2013, SharePoint 2010, SharePoint 2007, SharePoint 3.0</span><span class="sxs-lookup"><span data-stu-id="28b05-116">SharePoint 2013, SharePoint 2010, SharePoint 2007, SharePoint 3.0</span></span> |<span data-ttu-id="28b05-117">SharePoint разворачивается как физический сервер или виртуальная машина Hyper-V/VMware </span><span class="sxs-lookup"><span data-stu-id="28b05-117">SharePoint deployed as a physical server or Hyper-V/VMware virtual machine</span></span> <br> -------------- <br> <span data-ttu-id="28b05-118">SQL AlwaysOn</span><span class="sxs-lookup"><span data-stu-id="28b05-118">SQL AlwaysOn</span></span> | <span data-ttu-id="28b05-119">Параметры восстановления фермы SharePoint: ферма, база данных, файл или элемент списка для восстановления из точек восстановления диска.</span><span class="sxs-lookup"><span data-stu-id="28b05-119">Protect SharePoint Farm recovery options: Recovery farm, database, and file or list item from disk recovery points.</span></span>  <span data-ttu-id="28b05-120">Восстановление фермы и базы данных из точек восстановления Azure.</span><span class="sxs-lookup"><span data-stu-id="28b05-120">Farm and database recovery from Azure recovery points.</span></span> |

## <a name="before-you-start"></a><span data-ttu-id="28b05-121">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="28b05-121">Before you start</span></span>
<span data-ttu-id="28b05-122">Существует несколько моментов, которые необходимо tooconfirm перед выполнением резервного копирования tooAzure фермы SharePoint.</span><span class="sxs-lookup"><span data-stu-id="28b05-122">There are a few things you need tooconfirm before you back up a SharePoint farm tooAzure.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="28b05-123">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="28b05-123">Prerequisites</span></span>
<span data-ttu-id="28b05-124">Прежде чем продолжить, убедитесь, что [установлен и подготовленные hello Azure Backup Server](backup-azure-microsoft-azure-backup.md) tooprotect рабочих нагрузок.</span><span class="sxs-lookup"><span data-stu-id="28b05-124">Before you proceed, make sure that you have [installed and prepared hello Azure Backup Server](backup-azure-microsoft-azure-backup.md) tooprotect workloads.</span></span>

### <a name="protection-agent"></a><span data-ttu-id="28b05-125">Агент защиты</span><span class="sxs-lookup"><span data-stu-id="28b05-125">Protection agent</span></span>
<span data-ttu-id="28b05-126">агент защиты Hello должен устанавливаться на сервере hello, на котором выполняется SharePoint, hello серверов, работающих под управлением SQL Server и другие серверы, которые являются частью фермы SharePoint hello.</span><span class="sxs-lookup"><span data-stu-id="28b05-126">hello Protection agent must be installed on hello server that's running SharePoint, hello servers that are running SQL Server, and all other servers that are part of hello SharePoint farm.</span></span> <span data-ttu-id="28b05-127">Дополнительные сведения о том, как tooset hello агента защиты, в разделе [установки агента защиты](https://technet.microsoft.com/library/hh758034\(v=sc.12\).aspx).</span><span class="sxs-lookup"><span data-stu-id="28b05-127">For more information about how tooset up hello protection agent, see [Setup Protection Agent](https://technet.microsoft.com/library/hh758034\(v=sc.12\).aspx).</span></span>  <span data-ttu-id="28b05-128">Hello одно исключение — установить агент hello только на одном веб-сервере переднего плана (WFE).</span><span class="sxs-lookup"><span data-stu-id="28b05-128">hello one exception is that you install hello agent only on a single web front end (WFE) server.</span></span> <span data-ttu-id="28b05-129">DPM требуется агент hello на один tooserve сервера WFE только в качестве точки входа hello для защиты.</span><span class="sxs-lookup"><span data-stu-id="28b05-129">DPM needs hello agent on one WFE server only tooserve as hello entry point for protection.</span></span>

### <a name="sharepoint-farm"></a><span data-ttu-id="28b05-130">Ферма SharePoint</span><span class="sxs-lookup"><span data-stu-id="28b05-130">SharePoint farm</span></span>
<span data-ttu-id="28b05-131">Для каждых 10 млн элементов в ферме hello должен быть по крайней мере 2 ГБ дискового пространства на томе hello, где находится папка MABS hello.</span><span class="sxs-lookup"><span data-stu-id="28b05-131">For every 10 million items in hello farm, there must be at least 2 GB of space on hello volume where hello MABS folder is located.</span></span> <span data-ttu-id="28b05-132">Эта память нужна для создания каталога.</span><span class="sxs-lookup"><span data-stu-id="28b05-132">This space is required for catalog generation.</span></span> <span data-ttu-id="28b05-133">MABS toorecover определенных элементов (семейств веб-сайтов, сайты, списки, библиотеки документов, папки, отдельные документы и элементы списка) создания каталогов создает список hello URL-адресов, которые содержатся в каждой базе данных контента.</span><span class="sxs-lookup"><span data-stu-id="28b05-133">For MABS toorecover specific items (site collections, sites, lists, document libraries, folders, individual documents, and list items), catalog generation creates a list of hello URLs that are contained within each content database.</span></span> <span data-ttu-id="28b05-134">Можно просмотреть список hello URL-адреса в hello hello восстанавливаемый элемент области **восстановления** области консоли администратора MABS задач.</span><span class="sxs-lookup"><span data-stu-id="28b05-134">You can view hello list of URLs in hello recoverable item pane in hello **Recovery** task area of MABS Administrator Console.</span></span>

### <a name="sql-server"></a><span data-ttu-id="28b05-135">SQL Server</span><span class="sxs-lookup"><span data-stu-id="28b05-135">SQL Server</span></span>
<span data-ttu-id="28b05-136">MABS запускается от имени учетной записи LocalSystem.</span><span class="sxs-lookup"><span data-stu-id="28b05-136">MABS runs as a LocalSystem account.</span></span> <span data-ttu-id="28b05-137">tooback копирование баз данных SQL Server MABS должен прав системного администратора для этой учетной записи для hello сервера, на котором выполняется SQL Server.</span><span class="sxs-lookup"><span data-stu-id="28b05-137">tooback up SQL Server databases, MABS needs sysadmin privileges on that account for hello server that's running SQL Server.</span></span> <span data-ttu-id="28b05-138">Задать NT AUTHORITY\SYSTEM слишком*sysadmin* hello сервера, на котором выполняется SQL Server, прежде чем создать его резервную копию.</span><span class="sxs-lookup"><span data-stu-id="28b05-138">Set NT AUTHORITY\SYSTEM too*sysadmin* on hello server that's running SQL Server before you back it up.</span></span>

<span data-ttu-id="28b05-139">Если ферма SharePoint hello баз данных SQL Server, которые настроены с псевдонимами SQL Server, установите клиентские компоненты SQL Server hello на hello интерфейсный веб-сервер, который будет защищать MABS.</span><span class="sxs-lookup"><span data-stu-id="28b05-139">If hello SharePoint farm has SQL Server databases that are configured with SQL Server aliases, install hello SQL Server client components on hello front-end Web server that MABS will protect.</span></span>

### <a name="sharepoint-server"></a><span data-ttu-id="28b05-140">SharePoint Server</span><span class="sxs-lookup"><span data-stu-id="28b05-140">SharePoint Server</span></span>
<span data-ttu-id="28b05-141">Производительность системы зависит от многих факторов, включая размер фермы SharePoint. Как правило, для защиты фермы SharePoint объемом 25 ТБ используется один сервер MABS.</span><span class="sxs-lookup"><span data-stu-id="28b05-141">While performance depends on many factors such as size of SharePoint farm, as general guidance one MABS can protect a 25 TB SharePoint farm.</span></span>

### <a name="whats-not-supported"></a><span data-ttu-id="28b05-142">Что не поддерживается</span><span class="sxs-lookup"><span data-stu-id="28b05-142">What's not supported</span></span>
* <span data-ttu-id="28b05-143">Защита фермы SharePoint с помощью MABS не охватывает индексы поиска или базы данных службы приложений.</span><span class="sxs-lookup"><span data-stu-id="28b05-143">MABS that protects a SharePoint farm does not protect search indexes or application service databases.</span></span> <span data-ttu-id="28b05-144">Необходимо будет tooconfigure hello защиты этих баз данных отдельно.</span><span class="sxs-lookup"><span data-stu-id="28b05-144">You will need tooconfigure hello protection of these databases separately.</span></span>
* <span data-ttu-id="28b05-145">MABS не поддерживает резервное копирование баз данных SharePoint SQL Server, размещенных в общих хранилищах на масштабируемом файловом сервере.</span><span class="sxs-lookup"><span data-stu-id="28b05-145">MABS does not provide backup of SharePoint SQL Server databases that are hosted on scale-out file server (SOFS) shares.</span></span>

## <a name="configure-sharepoint-protection"></a><span data-ttu-id="28b05-146">Настройка защиты SharePoint</span><span class="sxs-lookup"><span data-stu-id="28b05-146">Configure SharePoint protection</span></span>
<span data-ttu-id="28b05-147">Прежде чем использовать MABS tooprotect SharePoint, необходимо настроить hello модуля записи VSS SharePoint (службы модуля записи WSS) с помощью **ConfigureSharePoint.exe**.</span><span class="sxs-lookup"><span data-stu-id="28b05-147">Before you can use MABS tooprotect SharePoint, you must configure hello SharePoint VSS Writer service (WSS Writer service) by using **ConfigureSharePoint.exe**.</span></span>

<span data-ttu-id="28b05-148">Можно найти **ConfigureSharePoint.exe** в папке \bin hello [путь установки MABS] на интерфейсном веб-сервере hello.</span><span class="sxs-lookup"><span data-stu-id="28b05-148">You can find **ConfigureSharePoint.exe** in hello [MABS Installation Path]\bin folder on hello front-end web server.</span></span> <span data-ttu-id="28b05-149">Это средство предоставляет hello агент защиты с hello учетные данные для фермы SharePoint hello.</span><span class="sxs-lookup"><span data-stu-id="28b05-149">This tool provides hello protection agent with hello credentials for hello SharePoint farm.</span></span> <span data-ttu-id="28b05-150">Файл нужно распаковать на одном интерфейсном веб-сервере.</span><span class="sxs-lookup"><span data-stu-id="28b05-150">You run it on a single WFE server.</span></span> <span data-ttu-id="28b05-151">Если у вас таких серверов несколько, выберите один из них для настройки группы защиты.</span><span class="sxs-lookup"><span data-stu-id="28b05-151">If you have multiple WFE servers, select just one when you configure a protection group.</span></span>

### <a name="tooconfigure-hello-sharepoint-vss-writer-service"></a><span data-ttu-id="28b05-152">hello tooconfigure служба модуля записи VSS SharePoint</span><span class="sxs-lookup"><span data-stu-id="28b05-152">tooconfigure hello SharePoint VSS Writer service</span></span>
1. <span data-ttu-id="28b05-153">На сервере WFE hello, в командной строке перейти слишком \bin\ [расположение установки MABS]</span><span class="sxs-lookup"><span data-stu-id="28b05-153">On hello WFE server, at a command prompt, go too[MABS installation location]\bin\\</span></span>
2. <span data-ttu-id="28b05-154">Введите ConfigureSharePoint -EnableSharePointProtection.</span><span class="sxs-lookup"><span data-stu-id="28b05-154">Enter ConfigureSharePoint -EnableSharePointProtection.</span></span>
3. <span data-ttu-id="28b05-155">Введите учетные данные администратора фермы hello.</span><span class="sxs-lookup"><span data-stu-id="28b05-155">Enter hello farm administrator credentials.</span></span> <span data-ttu-id="28b05-156">Эта учетная запись должна быть членом hello локальной группы администраторов на сервере WFE hello.</span><span class="sxs-lookup"><span data-stu-id="28b05-156">This account should be a member of hello local Administrator group on hello WFE server.</span></span> <span data-ttu-id="28b05-157">Если администратор фермы hello не hello grant локального администратора, следующие разрешения на сервере WFE hello:</span><span class="sxs-lookup"><span data-stu-id="28b05-157">If hello farm administrator isn’t a local admin grant hello following permissions on hello WFE server:</span></span>
   * <span data-ttu-id="28b05-158">Предоставление hello WSS_Admin_WPG полный доступ toohello DPM папку группы (% Program Files%\Microsoft Azure Backup\DPM).</span><span class="sxs-lookup"><span data-stu-id="28b05-158">Grant hello WSS_Admin_WPG group full control toohello DPM folder (%Program Files%\Microsoft Azure Backup\DPM).</span></span>
   * <span data-ttu-id="28b05-159">Предоставьте hello WSS_Admin_WPG группы доступа на чтение toohello DPM реестра (HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft Data Protection Manager).</span><span class="sxs-lookup"><span data-stu-id="28b05-159">Grant hello WSS_Admin_WPG group read access toohello DPM Registry key (HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft Data Protection Manager).</span></span>

> [!NOTE]
> <span data-ttu-id="28b05-160">Вам потребуется toorerun ConfigureSharePoint.exe при каждом изменении в hello учетные данные администратора фермы SharePoint.</span><span class="sxs-lookup"><span data-stu-id="28b05-160">You’ll need toorerun ConfigureSharePoint.exe whenever there’s a change in hello SharePoint farm administrator credentials.</span></span>
>
>

## <a name="back-up-a-sharepoint-farm-by-using-mabs"></a><span data-ttu-id="28b05-161">Архивация фермы SharePoint с помощью MABS</span><span class="sxs-lookup"><span data-stu-id="28b05-161">Back up a SharePoint farm by using MABS</span></span>
<span data-ttu-id="28b05-162">После настройки MABS и hello фермы SharePoint, как описано ранее SharePoint может быть защищен MABS.</span><span class="sxs-lookup"><span data-stu-id="28b05-162">After you have configured MABS and hello SharePoint farm as explained previously, SharePoint can be protected by MABS.</span></span>

### <a name="tooprotect-a-sharepoint-farm"></a><span data-ttu-id="28b05-163">tooprotect фермы SharePoint</span><span class="sxs-lookup"><span data-stu-id="28b05-163">tooprotect a SharePoint farm</span></span>
1. <span data-ttu-id="28b05-164">Из hello **защиты** щелкните вкладку hello консоли администратора MABS **New**.</span><span class="sxs-lookup"><span data-stu-id="28b05-164">From hello **Protection** tab of hello MABS Administrator Console, click **New**.</span></span>
    <span data-ttu-id="28b05-165">![Вкладка создания защиты](./media/backup-azure-backup-sharepoint/dpm-new-protection-tab.png)</span><span class="sxs-lookup"><span data-stu-id="28b05-165">![New Protection Tab](./media/backup-azure-backup-sharepoint/dpm-new-protection-tab.png)</span></span>
2. <span data-ttu-id="28b05-166">На hello **Выбор типа группы защиты** страница hello **создания новой группы защиты** мастера, выберите **серверы**, а затем нажмите кнопку **Далее** .</span><span class="sxs-lookup"><span data-stu-id="28b05-166">On hello **Select Protection Group Type** page of hello **Create New Protection Group** wizard, select **Servers**, and then click **Next**.</span></span>

    ![Выберите тип группы защиты](./media/backup-azure-backup-sharepoint/select-protection-group-type.png)
3. <span data-ttu-id="28b05-168">На hello **Выбор членов группы** экрана, выберите hello флажок для сервера SharePoint hello tooprotect и щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="28b05-168">On hello **Select Group Members** screen, select hello check box for hello SharePoint server you want tooprotect and click **Next**.</span></span>

    ![Выберите членов группы](./media/backup-azure-backup-sharepoint/select-group-members2.png)

   > [!NOTE]
   > <span data-ttu-id="28b05-170">С установленным агентом защиты hello вы увидите hello сервера в мастере hello.</span><span class="sxs-lookup"><span data-stu-id="28b05-170">With hello protection agent installed, you can see hello server in hello wizard.</span></span> <span data-ttu-id="28b05-171">Также сервер MABS отображает его структуру.</span><span class="sxs-lookup"><span data-stu-id="28b05-171">MABS also shows its structure.</span></span> <span data-ttu-id="28b05-172">Поскольку вы запустили ConfigureSharePoint.exe, MABS взаимодействует со службой модуля записи VSS SharePoint hello и все соответствующие базы данных SQL Server и распознает hello структура фермы SharePoint, hello связанных баз данных содержимого и все соответствующие элементы.</span><span class="sxs-lookup"><span data-stu-id="28b05-172">Because you ran ConfigureSharePoint.exe, MABS communicates with hello SharePoint VSS Writer service and its corresponding SQL Server databases and recognizes hello SharePoint farm structure, hello associated content databases, and any corresponding items.</span></span>
   >
   >
4. <span data-ttu-id="28b05-173">На hello **Выбор метода защиты данных** введите имя hello hello **группы защиты**и выберите предпочитаемом *методы защиты*.</span><span class="sxs-lookup"><span data-stu-id="28b05-173">On hello **Select Data Protection Method** page, enter hello name of hello **Protection Group**, and select your preferred *protection methods*.</span></span> <span data-ttu-id="28b05-174">Щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="28b05-174">Click **Next**.</span></span>

    ![Выберите метод защиты данных](./media/backup-azure-backup-sharepoint/select-data-protection-method1.png)

   > [!NOTE]
   > <span data-ttu-id="28b05-176">метод защиты диска Hello помогает toomeet короткое время восстановления целей.</span><span class="sxs-lookup"><span data-stu-id="28b05-176">hello disk protection method helps toomeet short recovery-time objectives.</span></span>
   >
   >
5. <span data-ttu-id="28b05-177">На hello **Выбор краткосрочных целей** выберите предпочитаемом **диапазон хранения** и определить, когда требуется toooccur резервных копий.</span><span class="sxs-lookup"><span data-stu-id="28b05-177">On hello **Specify Short-Term Goals** page, select your preferred **Retention range** and identify when you want backups toooccur.</span></span>

    ![Выберите краткосрочные цели](./media/backup-azure-backup-sharepoint/specify-short-term-goals2.png)

   > [!NOTE]
   > <span data-ttu-id="28b05-179">Так как восстановление чаще всего требуется для данных, которые меньше пяти дней, мы выбранные диапазон хранения равен пяти дней на диске и гарантирует, что эта резервная копия hello происходит в непроизводственной часы, в этом примере.</span><span class="sxs-lookup"><span data-stu-id="28b05-179">Because recovery is most often required for data that's less than five days old, we selected a retention range of five days on disk and ensured that hello backup happens during non-production hours, for this example.</span></span>
   >
   >
6. <span data-ttu-id="28b05-180">Просмотрите hello пула хранения дискового пространства, выделенного для группы защиты hello, а затем нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="28b05-180">Review hello storage pool disk space allocated for hello protection group, and click then **Next**.</span></span>
7. <span data-ttu-id="28b05-181">Для каждой группы защиты MABS выделяет toostore места на диске и управление репликами.</span><span class="sxs-lookup"><span data-stu-id="28b05-181">For every protection group, MABS allocates disk space toostore and manage replicas.</span></span> <span data-ttu-id="28b05-182">На этом этапе MABS необходимо создать копию hello выбранных данных.</span><span class="sxs-lookup"><span data-stu-id="28b05-182">At this point, MABS must create a copy of hello selected data.</span></span> <span data-ttu-id="28b05-183">Выберите способ и время создания реплика hello и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="28b05-183">Select how and when you want hello replica created, and then click **Next**.</span></span>

    ![Выберите метод создания реплики](./media/backup-azure-backup-sharepoint/choose-replica-creation-method.png)

   > [!NOTE]
   > <span data-ttu-id="28b05-185">убедиться, что сетевой трафик не устаревший toomake выберите время вне рабочих часов.</span><span class="sxs-lookup"><span data-stu-id="28b05-185">toomake sure that network traffic is not effected, select a time outside production hours.</span></span>
   >
   >
8. <span data-ttu-id="28b05-186">MABS гарантирует целостность данных путем выполнения проверки согласованности в реплике hello.</span><span class="sxs-lookup"><span data-stu-id="28b05-186">MABS ensures data integrity by performing consistency checks on hello replica.</span></span> <span data-ttu-id="28b05-187">Доступны два параметра.</span><span class="sxs-lookup"><span data-stu-id="28b05-187">There are two available options.</span></span> <span data-ttu-id="28b05-188">Можно определить проверяет согласованность toorun расписание или DPM запустить проверку согласованности автоматически hello реплики всякий раз, когда он становится несогласованной.</span><span class="sxs-lookup"><span data-stu-id="28b05-188">You can define a schedule toorun consistency checks, or DPM can run consistency checks automatically on hello replica whenever it becomes inconsistent.</span></span> <span data-ttu-id="28b05-189">Выберите желаемый параметр и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="28b05-189">Select your preferred option, and then click **Next**.</span></span>

    ![Проверка согласованности](./media/backup-azure-backup-sharepoint/consistency-check.png)
9. <span data-ttu-id="28b05-191">На hello **укажите оперативной защиты данных** выберите hello фермы SharePoint будет tooprotect и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="28b05-191">On hello **Specify Online Protection Data** page, select hello SharePoint farm that you want tooprotect, and then click **Next**.</span></span>

    ![DPM SharePoint Protection1](./media/backup-azure-backup-sharepoint/select-online-protection1.png)
10. <span data-ttu-id="28b05-193">На hello **укажите расписание оперативной архивации** выберите предпочтительное расписание и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="28b05-193">On hello **Specify Online Backup Schedule** page, select your preferred schedule, and then click **Next**.</span></span>

    ![Online_backup_schedule](./media/backup-azure-backup-sharepoint/specify-online-backup-schedule.png)

    > [!NOTE]
    > <span data-ttu-id="28b05-195">MABS обеспечивает максимальную два tooAzure ежедневных резервных копий из hello, а затем доступны последние точки для резервного копирования диска.</span><span class="sxs-lookup"><span data-stu-id="28b05-195">MABS provides a maximum of two daily backups tooAzure from hello then available latest disk backup point.</span></span> <span data-ttu-id="28b05-196">Резервное копирование Azure можно также управлять hello объем пропускной способности глобальной сети, который может использоваться для архивации в пиковые и непиковые часы с помощью [регулирование сети резервного копирования Azure](https://azure.microsoft.com/documentation/articles/backup-configure-vault/#enable-network-throttling).</span><span class="sxs-lookup"><span data-stu-id="28b05-196">Azure Backup can also control hello amount of WAN bandwidth that can be used for backups in peak and off-peak hours by using [Azure Backup Network Throttling](https://azure.microsoft.com/documentation/articles/backup-configure-vault/#enable-network-throttling).</span></span>
    >
    >
11. <span data-ttu-id="28b05-197">В зависимости от расписания архивации hello, выбранного на hello **указание политики оперативного хранения** страницы выберите hello политику хранения для резервного копирования точек ежедневно, еженедельно, ежемесячно и ежегодно.</span><span class="sxs-lookup"><span data-stu-id="28b05-197">Depending on hello backup schedule that you selected, on hello **Specify Online Retention Policy** page, select hello retention policy for daily, weekly, monthly, and yearly backup points.</span></span>

    ![Online_retention_policy](./media/backup-azure-backup-sharepoint/specify-online-retention.png)

    > [!NOTE]
    > <span data-ttu-id="28b05-199">MABS использует трехуровневую схему хранения, которая позволяет выбирать разную политику хранения для разных точек резервного копирования.</span><span class="sxs-lookup"><span data-stu-id="28b05-199">MABS uses a grandfather-father-son retention scheme in which a different retention policy can be chosen for different backup points.</span></span>
    >
    >
12. <span data-ttu-id="28b05-200">Аналогичные toodisk реплики точки начальную ссылку должен toobe, созданные в Azure.</span><span class="sxs-lookup"><span data-stu-id="28b05-200">Similar toodisk, an initial reference point replica needs toobe created in Azure.</span></span> <span data-ttu-id="28b05-201">Выберите ваш предпочтительный вариант toocreate tooAzure начальной резервной копии и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="28b05-201">Select your preferred option toocreate an initial backup copy tooAzure, and then click **Next**.</span></span>

    ![Online_replica](./media/backup-azure-backup-sharepoint/online-replication.png)
13. <span data-ttu-id="28b05-203">Просмотрите выбранные параметры на hello **Сводка** и нажмите кнопку **создать группу**.</span><span class="sxs-lookup"><span data-stu-id="28b05-203">Review your selected settings on hello **Summary** page, and then click **Create Group**.</span></span> <span data-ttu-id="28b05-204">После создания группы защиты hello, вы увидите сообщение об успешном выполнении.</span><span class="sxs-lookup"><span data-stu-id="28b05-204">You will see a success message after hello protection group has been created.</span></span>

    ![Сводка](./media/backup-azure-backup-sharepoint/summary.png)

## <a name="restore-a-sharepoint-item-from-disk-by-using-mabs"></a><span data-ttu-id="28b05-206">Восстановление элемента SharePoint с диска с помощью MABS</span><span class="sxs-lookup"><span data-stu-id="28b05-206">Restore a SharePoint item from disk by using MABS</span></span>
<span data-ttu-id="28b05-207">В следующем примере hello, hello *элемент восстановление SharePoint* был случайно удален и требуется восстановить toobe.</span><span class="sxs-lookup"><span data-stu-id="28b05-207">In hello following example, hello *Recovering SharePoint item* has been accidentally deleted and needs toobe recovered.</span></span>
<span data-ttu-id="28b05-208">![DPM SharePoint Protection4](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection5.png)</span><span class="sxs-lookup"><span data-stu-id="28b05-208">![MABS SharePoint Protection4](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection5.png)</span></span>

1. <span data-ttu-id="28b05-209">Откройте hello **консоли администрирования DPM**.</span><span class="sxs-lookup"><span data-stu-id="28b05-209">Open hello **DPM Administrator Console**.</span></span> <span data-ttu-id="28b05-210">Показаны все ферм SharePoint, которые защищены с помощью DPM в hello **защиты** вкладки.</span><span class="sxs-lookup"><span data-stu-id="28b05-210">All SharePoint farms that are protected by DPM are shown in hello **Protection** tab.</span></span>

    ![MABS SharePoint Protection3](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection4.png)
2. <span data-ttu-id="28b05-212">toorecover hello toobegin элемента, выберите hello **восстановления** вкладки.</span><span class="sxs-lookup"><span data-stu-id="28b05-212">toobegin toorecover hello item, select hello **Recovery** tab.</span></span>

    ![MABS SharePoint Protection5](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection6.png)
3. <span data-ttu-id="28b05-214">Чтобы найти *элемент восстановления SharePoint* , можно использовать поиск на основе подстановки в пределах диапазона точек восстановления.</span><span class="sxs-lookup"><span data-stu-id="28b05-214">You can search SharePoint for *Recovering SharePoint item* by using a wildcard-based search within a recovery point range.</span></span>

    ![MABS SharePoint Protection6](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection7.png)
4. <span data-ttu-id="28b05-216">Выберите точку восстановления, соответствующих hello из результатов поиска hello, щелкните правой кнопкой мыши элемент hello и выберите **восстановить**.</span><span class="sxs-lookup"><span data-stu-id="28b05-216">Select hello appropriate recovery point from hello search results, right-click hello item, and then select **Recover**.</span></span>
5. <span data-ttu-id="28b05-217">Также можно просматривать различные точки восстановления и выбрать базу данных или элемент toorecover.</span><span class="sxs-lookup"><span data-stu-id="28b05-217">You can also browse through various recovery points and select a database or item toorecover.</span></span> <span data-ttu-id="28b05-218">Выберите **даты > времени восстановления**и выберите правильный hello **базы данных > фермы SharePoint > точка восстановления > элемент**.</span><span class="sxs-lookup"><span data-stu-id="28b05-218">Select **Date > Recovery time**, and then select hello correct **Database > SharePoint farm > Recovery point > Item**.</span></span>

    ![MABS SharePoint Protection7](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection8.png)
6. <span data-ttu-id="28b05-220">Щелкните правой кнопкой мыши элемент hello, а затем выберите **восстановить** tooopen hello **мастер восстановления**.</span><span class="sxs-lookup"><span data-stu-id="28b05-220">Right-click hello item, and then select **Recover** tooopen hello **Recovery Wizard**.</span></span> <span data-ttu-id="28b05-221">Щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="28b05-221">Click **Next**.</span></span>

    ![Просмотр выбранных параметров восстановления](./media/backup-azure-backup-sharepoint/review-recovery-selection.png)
7. <span data-ttu-id="28b05-223">Выберите тип восстановления требуется tooperform и нажмите кнопку hello **Далее**.</span><span class="sxs-lookup"><span data-stu-id="28b05-223">Select hello type of recovery that you want tooperform, and then click **Next**.</span></span>

    ![Тип восстановления](./media/backup-azure-backup-sharepoint/select-recovery-type.png)

   > [!NOTE]
   > <span data-ttu-id="28b05-225">Здравствуйте, выбор **восстановить toooriginal** в hello производится восстановление исходного узла SharePoint hello элемента toohello.</span><span class="sxs-lookup"><span data-stu-id="28b05-225">hello selection of **Recover toooriginal** in hello example recovers hello item toohello original SharePoint site.</span></span>
   >
   >
8. <span data-ttu-id="28b05-226">Выберите hello **процесса восстановления** нужных toouse.</span><span class="sxs-lookup"><span data-stu-id="28b05-226">Select hello **Recovery Process** that you want toouse.</span></span>

   * <span data-ttu-id="28b05-227">Выберите **восстановление без использования фермы восстановления** Если ферма SharePoint hello не изменилась и hello таким же, как hello восстановления точка, которая является время восстановления.</span><span class="sxs-lookup"><span data-stu-id="28b05-227">Select **Recover without using a recovery farm** if hello SharePoint farm has not changed and is hello same as hello recovery point that is being restored.</span></span>
   * <span data-ttu-id="28b05-228">Выберите **восстановления с использованием фермы восстановления** hello фермы SharePoint изменился с момента создания точки восстановления hello.</span><span class="sxs-lookup"><span data-stu-id="28b05-228">Select **Recover using a recovery farm** if hello SharePoint farm has changed since hello recovery point was created.</span></span>

     ![процесс восстановления](./media/backup-azure-backup-sharepoint/recovery-process.png)
9. <span data-ttu-id="28b05-230">Временно обеспечивают промежуточного экземпляра расположение toorecover hello базы данных SQL Server, а также в промежуточной папке MABS и hello сервера, на котором выполняется SharePoint toorecover hello элемента.</span><span class="sxs-lookup"><span data-stu-id="28b05-230">Provide a staging SQL Server instance location toorecover hello database temporarily, and provide a staging file share on MABS and hello server that's running SharePoint toorecover hello item.</span></span>

    ![Расположение промежуточного хранения 1](./media/backup-azure-backup-sharepoint/staging-location1.png)

    <span data-ttu-id="28b05-232">MABS присоединяет hello базы данных содержимого, на котором размещается hello SharePoint элемент toohello временный экземпляр SQL Server.</span><span class="sxs-lookup"><span data-stu-id="28b05-232">MABS attaches hello content database that is hosting hello SharePoint item toohello temporary SQL Server instance.</span></span> <span data-ttu-id="28b05-233">Из базы данных контента hello он восстанавливает элемент hello и помещает его в промежуточное расположение файла в MABS hello.</span><span class="sxs-lookup"><span data-stu-id="28b05-233">From hello content database, it recovers hello item and puts it on hello staging file location on MABS.</span></span> <span data-ttu-id="28b05-234">Hello восстановить элемент, на hello, теперь промежуточное расположение toohello toobe экспортировать потребностей промежуточное расположение на ферме SharePoint hello.</span><span class="sxs-lookup"><span data-stu-id="28b05-234">hello recovered item that's on hello staging location now needs toobe exported toohello staging location on hello SharePoint farm.</span></span>

    ![Расположение промежуточного хранения 2](./media/backup-azure-backup-sharepoint/staging-location2.png)
10. <span data-ttu-id="28b05-236">Выберите **задание параметров восстановления**и применить параметры безопасности toohello фермы SharePoint или применить настройки безопасности hello hello точки восстановления.</span><span class="sxs-lookup"><span data-stu-id="28b05-236">Select **Specify recovery options**, and apply security settings toohello SharePoint farm or apply hello security settings of hello recovery point.</span></span> <span data-ttu-id="28b05-237">Щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="28b05-237">Click **Next**.</span></span>

    ![Варианты восстановления](./media/backup-azure-backup-sharepoint/recovery-options.png)

    > [!NOTE]
    > <span data-ttu-id="28b05-239">Можно выбрать использование полосы пропускания сети toothrottle hello.</span><span class="sxs-lookup"><span data-stu-id="28b05-239">You can choose toothrottle hello network bandwidth usage.</span></span> <span data-ttu-id="28b05-240">Это сводит к минимуму влияние toohello рабочего сервера во время рабочих часов.</span><span class="sxs-lookup"><span data-stu-id="28b05-240">This minimizes impact toohello production server during production hours.</span></span>
    >
    >
11. <span data-ttu-id="28b05-241">Просмотрите сводные данные hello и нажмите кнопку **восстановить** toobegin восстановления файла hello.</span><span class="sxs-lookup"><span data-stu-id="28b05-241">Review hello summary information, and then click **Recover** toobegin recovery of hello file.</span></span>

    ![Сводка параметров восстановления](./media/backup-azure-backup-sharepoint/recovery-summary.png)
12. <span data-ttu-id="28b05-243">Теперь выберите hello **мониторинг** на вкладке hello **консоли администрирования MABS** tooview hello **состояние** hello восстановления.</span><span class="sxs-lookup"><span data-stu-id="28b05-243">Now select hello **Monitoring** tab in hello **MABS Administrator Console** tooview hello **Status** of hello recovery.</span></span>

    ![Состояние восстановления](./media/backup-azure-backup-sharepoint/recovery-monitoring.png)

    > [!NOTE]
    > <span data-ttu-id="28b05-245">восстановлен файл Hello.</span><span class="sxs-lookup"><span data-stu-id="28b05-245">hello file is now restored.</span></span> <span data-ttu-id="28b05-246">Вы можете обновить файл hello восстановить toocheck сайта SharePoint hello.</span><span class="sxs-lookup"><span data-stu-id="28b05-246">You can refresh hello SharePoint site toocheck hello restored file.</span></span>
    >
    >

## <a name="restore-a-sharepoint-database-from-azure-by-using-dpm"></a><span data-ttu-id="28b05-247">Восстановление базы данных SharePoint из Azure с помощью DPM</span><span class="sxs-lookup"><span data-stu-id="28b05-247">Restore a SharePoint database from Azure by using DPM</span></span>
1. <span data-ttu-id="28b05-248">toorecover базы данных содержимого SharePoint, просмотрите различные точки восстановления (как показано выше) и выберите точку восстановления hello, которая будет toorestore.</span><span class="sxs-lookup"><span data-stu-id="28b05-248">toorecover a SharePoint content database, browse through various recovery points (as shown previously), and select hello recovery point that you want toorestore.</span></span>

    ![MABS SharePoint Protection8](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection9.png)
2. <span data-ttu-id="28b05-250">Дважды щелкните hello SharePoint tooshow точки hello доступных SharePoint каталог данных для восстановления.</span><span class="sxs-lookup"><span data-stu-id="28b05-250">Double-click hello SharePoint recovery point tooshow hello available SharePoint catalog information.</span></span>

   > [!NOTE]
   > <span data-ttu-id="28b05-251">Так как ферма SharePoint hello защищен для долгосрочного хранения в Azure, можно найти в MABS никаких сведений каталога (метаданные).</span><span class="sxs-lookup"><span data-stu-id="28b05-251">Because hello SharePoint farm is protected for long-term retention in Azure, no catalog information (metadata) is available on MABS.</span></span> <span data-ttu-id="28b05-252">В результате каждый раз, когда в момент базы данных содержимого SharePoint должен восстановить toobe, понадобятся toocatalog hello веб-фермы SharePoint.</span><span class="sxs-lookup"><span data-stu-id="28b05-252">As a result, whenever a point-in-time SharePoint content database needs toobe recovered, you need toocatalog hello SharePoint farm again.</span></span>
   >
   >
3. <span data-ttu-id="28b05-253">Нажмите кнопку **Повторить каталогизацию**.</span><span class="sxs-lookup"><span data-stu-id="28b05-253">Click **Re-catalog**.</span></span>

    ![MABS SharePoint Protection10](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection12.png)

    <span data-ttu-id="28b05-255">Hello **повторная Каталогизация облака** откроется окно состояния.</span><span class="sxs-lookup"><span data-stu-id="28b05-255">hello **Cloud Recatalog** status window opens.</span></span>

    ![MABS SharePoint Protection11](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection13.png)

    <span data-ttu-id="28b05-257">После завершения создания каталога hello состояние изменяется слишком*успешно*.</span><span class="sxs-lookup"><span data-stu-id="28b05-257">After cataloging is finished, hello status changes too*Success*.</span></span> <span data-ttu-id="28b05-258">Нажмите кнопку **Закрыть**</span><span class="sxs-lookup"><span data-stu-id="28b05-258">Click **Close**.</span></span>

    ![MABS SharePoint Protection12](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection14.png)
4. <span data-ttu-id="28b05-260">Щелкните объект SharePoint hello показано hello MABS **восстановления** вкладке Структура базы данных контента tooget hello.</span><span class="sxs-lookup"><span data-stu-id="28b05-260">Click hello SharePoint object shown in hello MABS **Recovery** tab tooget hello content database structure.</span></span> <span data-ttu-id="28b05-261">Щелкните правой кнопкой мыши элемент hello и нажмите кнопку **восстановить**.</span><span class="sxs-lookup"><span data-stu-id="28b05-261">Right-click hello item, and then click **Recover**.</span></span>

    ![MABS SharePoint Protection13](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection15.png)
5. <span data-ttu-id="28b05-263">На этом этапе выполните hello [шаги восстановления ранее в этой статье](#restore-a-sharepoint-item-from-disk-using-dpm) toorecover базы данных содержимого SharePoint с диска.</span><span class="sxs-lookup"><span data-stu-id="28b05-263">At this point, follow hello [recovery steps earlier in this article](#restore-a-sharepoint-item-from-disk-using-dpm) toorecover a SharePoint content database from disk.</span></span>

## <a name="faqs"></a><span data-ttu-id="28b05-264">Часто задаваемые вопросы</span><span class="sxs-lookup"><span data-stu-id="28b05-264">FAQs</span></span>
<span data-ttu-id="28b05-265">Вопрос. можно ли восстановить исходное расположение элемента toohello SharePoint, если SharePoint настраивается с помощью SQL AlwaysOn (с защитой на диске)?</span><span class="sxs-lookup"><span data-stu-id="28b05-265">Q: Can I recover a SharePoint item toohello original location if SharePoint is configured by using SQL AlwaysOn (with protection on disk)?</span></span><br>
<span data-ttu-id="28b05-266">Ответ Да, hello элемент может быть восстановленные toohello исходного сайта SharePoint.</span><span class="sxs-lookup"><span data-stu-id="28b05-266">A: Yes, hello item can be recovered toohello original SharePoint site.</span></span>

<span data-ttu-id="28b05-267">Вопрос. можно ли восстановить исходное расположение toohello базы данных SharePoint, если SharePoint настраивается с помощью SQL AlwaysOn?</span><span class="sxs-lookup"><span data-stu-id="28b05-267">Q: Can I recover a SharePoint database toohello original location if SharePoint is configured by using SQL AlwaysOn?</span></span><br>
<span data-ttu-id="28b05-268">Ответ, так как базы данных SharePoint настраиваются в SQL AlwaysOn, их нельзя изменить, если удаляется группа доступности hello.</span><span class="sxs-lookup"><span data-stu-id="28b05-268">A: Because SharePoint databases are configured in SQL AlwaysOn, they cannot be modified unless hello availability group is removed.</span></span> <span data-ttu-id="28b05-269">В результате MABS нельзя восстановить в исходное расположение toohello базы данных.</span><span class="sxs-lookup"><span data-stu-id="28b05-269">As a result, MABS cannot restore a database toohello original location.</span></span> <span data-ttu-id="28b05-270">Можно восстановить экземпляр SQL Server tooanother базы данных SQL Server.</span><span class="sxs-lookup"><span data-stu-id="28b05-270">You can recover a SQL Server database tooanother SQL Server instance.</span></span>

## <a name="next-steps"></a><span data-ttu-id="28b05-271">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="28b05-271">Next steps</span></span>
* <span data-ttu-id="28b05-272">Дополнительные сведения о защите SharePoint с помощью MABS см. в [этой серии видеоматериалов](http://channel9.msdn.com/Series/Azure-Backup/Microsoft-SCDPM-Protection-of-SharePoint-1-of-2-How-to-create-a-SharePoint-Protection-Group).</span><span class="sxs-lookup"><span data-stu-id="28b05-272">Learn more about MABS Protection of SharePoint - see [Video Series - DPM Protection of SharePoint](http://channel9.msdn.com/Series/Azure-Backup/Microsoft-SCDPM-Protection-of-SharePoint-1-of-2-How-to-create-a-SharePoint-Protection-Group)</span></span>
