---
title: "Резервное копирование фермы SharePoint с помощью сервера резервного копирования Azure | Документация Майкрософт"
description: "Резервное копирование данных SharePoint с помощью сервера резервного копирования Azure. Эта статья содержит информацию о настройке фермы SharePoint для сохранения нужных данных в Azure. Защищенные данные SharePoint можно восстановить с диска или из Azure."
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
ms.openlocfilehash: 3ed000affd326eb1bd7c99773ec021ad6e03cc3b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="back-up-a-sharepoint-farm-to-azure"></a><span data-ttu-id="50563-105">Архивация фермы SharePoint в Azure</span><span class="sxs-lookup"><span data-stu-id="50563-105">Back up a SharePoint farm to Azure</span></span>
<span data-ttu-id="50563-106">Архивация SharePoint в Microsoft Azure с помощью сервера службы архивации Microsoft Azure во многом напоминает архивацию других источников данных.</span><span class="sxs-lookup"><span data-stu-id="50563-106">You back up a SharePoint farm to Microsoft Azure by using Microsoft Azure Backup Server (MABS) in much the same way that you back up other data sources.</span></span> <span data-ttu-id="50563-107">Служба архивации Azure позволяет гибко планировать архивацию, задавая ежедневные, еженедельные, ежемесячные или ежегодные точки архивации, и предоставляет параметры политики хранения для любой из этих точек.</span><span class="sxs-lookup"><span data-stu-id="50563-107">Azure Backup provides flexibility in the backup schedule to create daily, weekly, monthly, or yearly backup points and gives you retention policy options for various backup points.</span></span> <span data-ttu-id="50563-108">Также она позволяет сохранять копии локальных дисков для краткосрочных целей времени восстановления, а также сохранять копии в Azure для экономичного и длительного хранения.</span><span class="sxs-lookup"><span data-stu-id="50563-108">It also provides the capability to store local disk copies for quick recovery-time objectives (RTO) and to store copies to Azure for economical, long-term retention.</span></span>

## <a name="sharepoint-supported-versions-and-related-protection-scenarios"></a><span data-ttu-id="50563-109">Поддерживаемые версии SharePoint и соответствующие сценарии защиты</span><span class="sxs-lookup"><span data-stu-id="50563-109">SharePoint supported versions and related protection scenarios</span></span>
<span data-ttu-id="50563-110">Служба архивации Azure для DPM поддерживает следующие сценарии:</span><span class="sxs-lookup"><span data-stu-id="50563-110">Azure Backup for DPM supports the following scenarios:</span></span>

| <span data-ttu-id="50563-111">Рабочая нагрузка</span><span class="sxs-lookup"><span data-stu-id="50563-111">Workload</span></span> | <span data-ttu-id="50563-112">Версия</span><span class="sxs-lookup"><span data-stu-id="50563-112">Version</span></span> | <span data-ttu-id="50563-113">Развертывание SharePoint</span><span class="sxs-lookup"><span data-stu-id="50563-113">SharePoint deployment</span></span> | <span data-ttu-id="50563-114">Защита и восстановление</span><span class="sxs-lookup"><span data-stu-id="50563-114">Protection and recovery</span></span> |
| --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="50563-115">SharePoint</span><span class="sxs-lookup"><span data-stu-id="50563-115">SharePoint</span></span> |<span data-ttu-id="50563-116">SharePoint 2013, SharePoint 2010, SharePoint 2007, SharePoint 3.0</span><span class="sxs-lookup"><span data-stu-id="50563-116">SharePoint 2013, SharePoint 2010, SharePoint 2007, SharePoint 3.0</span></span> |<span data-ttu-id="50563-117">SharePoint разворачивается как физический сервер или виртуальная машина Hyper-V/VMware </span><span class="sxs-lookup"><span data-stu-id="50563-117">SharePoint deployed as a physical server or Hyper-V/VMware virtual machine</span></span> <br> -------------- <br> <span data-ttu-id="50563-118">SQL AlwaysOn</span><span class="sxs-lookup"><span data-stu-id="50563-118">SQL AlwaysOn</span></span> | <span data-ttu-id="50563-119">Параметры восстановления фермы SharePoint: ферма, база данных, файл или элемент списка для восстановления из точек восстановления диска.</span><span class="sxs-lookup"><span data-stu-id="50563-119">Protect SharePoint Farm recovery options: Recovery farm, database, and file or list item from disk recovery points.</span></span>  <span data-ttu-id="50563-120">Восстановление фермы и базы данных из точек восстановления Azure.</span><span class="sxs-lookup"><span data-stu-id="50563-120">Farm and database recovery from Azure recovery points.</span></span> |

## <a name="before-you-start"></a><span data-ttu-id="50563-121">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="50563-121">Before you start</span></span>
<span data-ttu-id="50563-122">Перед архивацией фермы SharePoint в Azure необходимо выполнить некоторые действия.</span><span class="sxs-lookup"><span data-stu-id="50563-122">There are a few things you need to confirm before you back up a SharePoint farm to Azure.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="50563-123">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="50563-123">Prerequisites</span></span>
<span data-ttu-id="50563-124">Прежде чем продолжить, убедитесь, что у вас [установлен и подготовлен сервер резервного копирования Azure](backup-azure-microsoft-azure-backup.md) для защиты рабочих нагрузок.</span><span class="sxs-lookup"><span data-stu-id="50563-124">Before you proceed, make sure that you have [installed and prepared the Azure Backup Server](backup-azure-microsoft-azure-backup.md) to protect workloads.</span></span>

### <a name="protection-agent"></a><span data-ttu-id="50563-125">Агент защиты</span><span class="sxs-lookup"><span data-stu-id="50563-125">Protection agent</span></span>
<span data-ttu-id="50563-126">Агент защиты необходимо установить на все серверы, где работает SharePoint или SQL Server, и на все остальные серверы, входящие в ферму SharePoint.</span><span class="sxs-lookup"><span data-stu-id="50563-126">The Protection agent must be installed on the server that's running SharePoint, the servers that are running SQL Server, and all other servers that are part of the SharePoint farm.</span></span> <span data-ttu-id="50563-127">Дополнительные сведения о настройке агента защиты см. в статье [Настройка защиты для SharePoint](https://technet.microsoft.com/library/hh758034\(v=sc.12\).aspx).</span><span class="sxs-lookup"><span data-stu-id="50563-127">For more information about how to set up the protection agent, see [Setup Protection Agent](https://technet.microsoft.com/library/hh758034\(v=sc.12\).aspx).</span></span>  <span data-ttu-id="50563-128">Единственное исключение состоит в том, что агент устанавливается только на один интерфейсный веб-сервер.</span><span class="sxs-lookup"><span data-stu-id="50563-128">The one exception is that you install the agent only on a single web front end (WFE) server.</span></span> <span data-ttu-id="50563-129">DPM требует установки агента только на один интерфейсный веб-сервер, который будет служить точкой входа для защиты.</span><span class="sxs-lookup"><span data-stu-id="50563-129">DPM needs the agent on one WFE server only to serve as the entry point for protection.</span></span>

### <a name="sharepoint-farm"></a><span data-ttu-id="50563-130">Ферма SharePoint</span><span class="sxs-lookup"><span data-stu-id="50563-130">SharePoint farm</span></span>
<span data-ttu-id="50563-131">На каждые 10 млн элементов, содержащихся в ферме, требуется не менее 2 ГБ памяти в томе, где находится папка MABS.</span><span class="sxs-lookup"><span data-stu-id="50563-131">For every 10 million items in the farm, there must be at least 2 GB of space on the volume where the MABS folder is located.</span></span> <span data-ttu-id="50563-132">Эта память нужна для создания каталога.</span><span class="sxs-lookup"><span data-stu-id="50563-132">This space is required for catalog generation.</span></span> <span data-ttu-id="50563-133">Чтобы сервер MABS мог восстанавливать определенные элементы (семейства веб-сайтов, сайты, списки, библиотеки документов, папки, документов или элементы списков), операция создания каталога формирует список URL-адресов, сохраняемых в каждой базе данных контента.</span><span class="sxs-lookup"><span data-stu-id="50563-133">For MABS to recover specific items (site collections, sites, lists, document libraries, folders, individual documents, and list items), catalog generation creates a list of the URLs that are contained within each content database.</span></span> <span data-ttu-id="50563-134">Этот список URL-адресов можно просмотреть в консоли администратора MABS, открыв панель восстанавливаемых элементов в области задач **Восстановление**.</span><span class="sxs-lookup"><span data-stu-id="50563-134">You can view the list of URLs in the recoverable item pane in the **Recovery** task area of MABS Administrator Console.</span></span>

### <a name="sql-server"></a><span data-ttu-id="50563-135">SQL Server</span><span class="sxs-lookup"><span data-stu-id="50563-135">SQL Server</span></span>
<span data-ttu-id="50563-136">MABS запускается от имени учетной записи LocalSystem.</span><span class="sxs-lookup"><span data-stu-id="50563-136">MABS runs as a LocalSystem account.</span></span> <span data-ttu-id="50563-137">Чтобы сервер MABS мог создавать резервные копии баз данных SQL Server, эта учетная запись должна иметь права системного администратора для того сервера, на котором выполняется SQL Server.</span><span class="sxs-lookup"><span data-stu-id="50563-137">To back up SQL Server databases, MABS needs sysadmin privileges on that account for the server that's running SQL Server.</span></span> <span data-ttu-id="50563-138">Установите для параметра NT AUTHORITY\SYSTEM значение *sysadmin* на сервере под управлением SQL Server, для которого нужно создать резервную копию.</span><span class="sxs-lookup"><span data-stu-id="50563-138">Set NT AUTHORITY\SYSTEM to *sysadmin* on the server that's running SQL Server before you back it up.</span></span>

<span data-ttu-id="50563-139">Если в ферме SharePoint есть базы данных SQL Server, настроенные с псевдонимами SQL Server, установите клиентские компоненты SQL Server на интерфейсный веб-сервер, защищаемый MABS.</span><span class="sxs-lookup"><span data-stu-id="50563-139">If the SharePoint farm has SQL Server databases that are configured with SQL Server aliases, install the SQL Server client components on the front-end Web server that MABS will protect.</span></span>

### <a name="sharepoint-server"></a><span data-ttu-id="50563-140">SharePoint Server</span><span class="sxs-lookup"><span data-stu-id="50563-140">SharePoint Server</span></span>
<span data-ttu-id="50563-141">Производительность системы зависит от многих факторов, включая размер фермы SharePoint. Как правило, для защиты фермы SharePoint объемом 25 ТБ используется один сервер MABS.</span><span class="sxs-lookup"><span data-stu-id="50563-141">While performance depends on many factors such as size of SharePoint farm, as general guidance one MABS can protect a 25 TB SharePoint farm.</span></span>

### <a name="whats-not-supported"></a><span data-ttu-id="50563-142">Что не поддерживается</span><span class="sxs-lookup"><span data-stu-id="50563-142">What's not supported</span></span>
* <span data-ttu-id="50563-143">Защита фермы SharePoint с помощью MABS не охватывает индексы поиска или базы данных службы приложений.</span><span class="sxs-lookup"><span data-stu-id="50563-143">MABS that protects a SharePoint farm does not protect search indexes or application service databases.</span></span> <span data-ttu-id="50563-144">Защиту этих баз данных необходимо настраивать отдельно.</span><span class="sxs-lookup"><span data-stu-id="50563-144">You will need to configure the protection of these databases separately.</span></span>
* <span data-ttu-id="50563-145">MABS не поддерживает резервное копирование баз данных SharePoint SQL Server, размещенных в общих хранилищах на масштабируемом файловом сервере.</span><span class="sxs-lookup"><span data-stu-id="50563-145">MABS does not provide backup of SharePoint SQL Server databases that are hosted on scale-out file server (SOFS) shares.</span></span>

## <a name="configure-sharepoint-protection"></a><span data-ttu-id="50563-146">Настройка защиты SharePoint</span><span class="sxs-lookup"><span data-stu-id="50563-146">Configure SharePoint protection</span></span>
<span data-ttu-id="50563-147">Чтобы использовать MABS для защиты SharePoint, сначала нужно настроить службу модуля записи VSS SharePoint (службу модуля записи WSS) с помощью файла **ConfigureSharePoint.exe**.</span><span class="sxs-lookup"><span data-stu-id="50563-147">Before you can use MABS to protect SharePoint, you must configure the SharePoint VSS Writer service (WSS Writer service) by using **ConfigureSharePoint.exe**.</span></span>

<span data-ttu-id="50563-148">Файл **ConfigureSharePoint.exe** находится в папке [путь_установки_MABS]\bin на интерфейсном веб-сервере.</span><span class="sxs-lookup"><span data-stu-id="50563-148">You can find **ConfigureSharePoint.exe** in the [MABS Installation Path]\bin folder on the front-end web server.</span></span> <span data-ttu-id="50563-149">Он позволяет установить агент защиты с учетными данными для фермы SharePoint.</span><span class="sxs-lookup"><span data-stu-id="50563-149">This tool provides the protection agent with the credentials for the SharePoint farm.</span></span> <span data-ttu-id="50563-150">Файл нужно распаковать на одном интерфейсном веб-сервере.</span><span class="sxs-lookup"><span data-stu-id="50563-150">You run it on a single WFE server.</span></span> <span data-ttu-id="50563-151">Если у вас таких серверов несколько, выберите один из них для настройки группы защиты.</span><span class="sxs-lookup"><span data-stu-id="50563-151">If you have multiple WFE servers, select just one when you configure a protection group.</span></span>

### <a name="to-configure-the-sharepoint-vss-writer-service"></a><span data-ttu-id="50563-152">Настройка службы модуля записи VSS SharePoint</span><span class="sxs-lookup"><span data-stu-id="50563-152">To configure the SharePoint VSS Writer service</span></span>
1. <span data-ttu-id="50563-153">На интерфейсном веб-сервере откройте командную строку и перейдите в папку [путь установки MABS]\bin\.</span><span class="sxs-lookup"><span data-stu-id="50563-153">On the WFE server, at a command prompt, go to [MABS installation location]\bin\\</span></span>
2. <span data-ttu-id="50563-154">Введите ConfigureSharePoint -EnableSharePointProtection.</span><span class="sxs-lookup"><span data-stu-id="50563-154">Enter ConfigureSharePoint -EnableSharePointProtection.</span></span>
3. <span data-ttu-id="50563-155">Введите учетные данные администратора фермы.</span><span class="sxs-lookup"><span data-stu-id="50563-155">Enter the farm administrator credentials.</span></span> <span data-ttu-id="50563-156">Эта учетная запись должна быть членом локальной группы администраторов на интерфейсном веб-сервере.</span><span class="sxs-lookup"><span data-stu-id="50563-156">This account should be a member of the local Administrator group on the WFE server.</span></span> <span data-ttu-id="50563-157">Если администратор фермы не является локальным администратором, предоставьте на интерфейсном веб-сервере следующие разрешения:</span><span class="sxs-lookup"><span data-stu-id="50563-157">If the farm administrator isn’t a local admin grant the following permissions on the WFE server:</span></span>
   * <span data-ttu-id="50563-158">Предоставьте группе WSS_Admin_WPG полный доступ к папке DPM (%Program Files%\Microsoft Azure Backup\DPM).</span><span class="sxs-lookup"><span data-stu-id="50563-158">Grant the WSS_Admin_WPG group full control to the DPM folder (%Program Files%\Microsoft Azure Backup\DPM).</span></span>
   * <span data-ttu-id="50563-159">Предоставьте группе WSS_Admin_WPG право чтения реестра DPM (HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft Data Protection Manager).</span><span class="sxs-lookup"><span data-stu-id="50563-159">Grant the WSS_Admin_WPG group read access to the DPM Registry key (HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft Data Protection Manager).</span></span>

> [!NOTE]
> <span data-ttu-id="50563-160">После каждого изменения в учетных данных администратора фермы SharePoint файл ConfigureSharePoint.exe необходимо перезапускать.</span><span class="sxs-lookup"><span data-stu-id="50563-160">You’ll need to rerun ConfigureSharePoint.exe whenever there’s a change in the SharePoint farm administrator credentials.</span></span>
>
>

## <a name="back-up-a-sharepoint-farm-by-using-mabs"></a><span data-ttu-id="50563-161">Архивация фермы SharePoint с помощью MABS</span><span class="sxs-lookup"><span data-stu-id="50563-161">Back up a SharePoint farm by using MABS</span></span>
<span data-ttu-id="50563-162">Когда вы примените для DPM и фермы SharePoint все указанные выше настройки, можно развернуть защиту SharePoint с помощью MABS.</span><span class="sxs-lookup"><span data-stu-id="50563-162">After you have configured MABS and the SharePoint farm as explained previously, SharePoint can be protected by MABS.</span></span>

### <a name="to-protect-a-sharepoint-farm"></a><span data-ttu-id="50563-163">Защита фермы SharePoint</span><span class="sxs-lookup"><span data-stu-id="50563-163">To protect a SharePoint farm</span></span>
1. <span data-ttu-id="50563-164">На вкладке **Защита** консоли администратора MABS нажмите кнопку **Создать**.</span><span class="sxs-lookup"><span data-stu-id="50563-164">From the **Protection** tab of the MABS Administrator Console, click **New**.</span></span>
    <span data-ttu-id="50563-165">![Вкладка создания защиты](./media/backup-azure-backup-sharepoint/dpm-new-protection-tab.png)</span><span class="sxs-lookup"><span data-stu-id="50563-165">![New Protection Tab](./media/backup-azure-backup-sharepoint/dpm-new-protection-tab.png)</span></span>
2. <span data-ttu-id="50563-166">На странице **Выбор типа группы защиты** мастера **создания группы защиты** выберите **Серверы** и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="50563-166">On the **Select Protection Group Type** page of the **Create New Protection Group** wizard, select **Servers**, and then click **Next**.</span></span>

    ![Выберите тип группы защиты](./media/backup-azure-backup-sharepoint/select-protection-group-type.png)
3. <span data-ttu-id="50563-168">На экране **Выбор элементов группы** установите флажок для сервера SharePoint, который нужно защитить, и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="50563-168">On the **Select Group Members** screen, select the check box for the SharePoint server you want to protect and click **Next**.</span></span>

    ![Выберите членов группы](./media/backup-azure-backup-sharepoint/select-group-members2.png)

   > [!NOTE]
   > <span data-ttu-id="50563-170">Если агент защиты установлен, сервер виден в мастере.</span><span class="sxs-lookup"><span data-stu-id="50563-170">With the protection agent installed, you can see the server in the wizard.</span></span> <span data-ttu-id="50563-171">Также сервер MABS отображает его структуру.</span><span class="sxs-lookup"><span data-stu-id="50563-171">MABS also shows its structure.</span></span> <span data-ttu-id="50563-172">Так как файл ConfigureSharePoint.exe запущен, MABS обменивается данными со службой модуля записи VSS SharePoint и соответствующими базами данных SQL Server, а также распознает структуру фермы SharePoint, связанные базы данных контента и все соответствующие элементы.</span><span class="sxs-lookup"><span data-stu-id="50563-172">Because you ran ConfigureSharePoint.exe, MABS communicates with the SharePoint VSS Writer service and its corresponding SQL Server databases and recognizes the SharePoint farm structure, the associated content databases, and any corresponding items.</span></span>
   >
   >
4. <span data-ttu-id="50563-173">На странице **Выбор метода защиты данных** введите имя группы защиты в поле **Имя группы защиты** и выберите желаемые *методы защиты*.</span><span class="sxs-lookup"><span data-stu-id="50563-173">On the **Select Data Protection Method** page, enter the name of the **Protection Group**, and select your preferred *protection methods*.</span></span> <span data-ttu-id="50563-174">Щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="50563-174">Click **Next**.</span></span>

    ![Выберите метод защиты данных](./media/backup-azure-backup-sharepoint/select-data-protection-method1.png)

   > [!NOTE]
   > <span data-ttu-id="50563-176">С помощью метода защиты диска можно удовлетворить краткосрочные цели времени восстановления.</span><span class="sxs-lookup"><span data-stu-id="50563-176">The disk protection method helps to meet short recovery-time objectives.</span></span>
   >
   >
5. <span data-ttu-id="50563-177">На странице **Выбор краткосрочных целей** выберите желаемый диапазон хранения в поле **Диапазон хранения** и укажите время создания резервных копий.</span><span class="sxs-lookup"><span data-stu-id="50563-177">On the **Specify Short-Term Goals** page, select your preferred **Retention range** and identify when you want backups to occur.</span></span>

    ![Выберите краткосрочные цели](./media/backup-azure-backup-sharepoint/specify-short-term-goals2.png)

   > [!NOTE]
   > <span data-ttu-id="50563-179">Так как восстановления обычно требуют данные менее чем за пять последних дней, в данном примере выбран пятидневный диапазон хранения на диске и назначена архивация на нерабочее время.</span><span class="sxs-lookup"><span data-stu-id="50563-179">Because recovery is most often required for data that's less than five days old, we selected a retention range of five days on disk and ensured that the backup happens during non-production hours, for this example.</span></span>
   >
   >
6. <span data-ttu-id="50563-180">Проверьте, какой объем дискового пространства в пуле носителей выделен для группы защиты, и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="50563-180">Review the storage pool disk space allocated for the protection group, and click then **Next**.</span></span>
7. <span data-ttu-id="50563-181">Для каждой группы защиты MABS выделяет дисковую память для хранения и администрирования реплик.</span><span class="sxs-lookup"><span data-stu-id="50563-181">For every protection group, MABS allocates disk space to store and manage replicas.</span></span> <span data-ttu-id="50563-182">На этом этапе MABS должен создать копию выбранных данных.</span><span class="sxs-lookup"><span data-stu-id="50563-182">At this point, MABS must create a copy of the selected data.</span></span> <span data-ttu-id="50563-183">Выберите способ и время создания реплики и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="50563-183">Select how and when you want the replica created, and then click **Next**.</span></span>

    ![Выберите метод создания реплики](./media/backup-azure-backup-sharepoint/choose-replica-creation-method.png)

   > [!NOTE]
   > <span data-ttu-id="50563-185">Чтобы не мешать сетевому трафику, выбирайте нерабочее время.</span><span class="sxs-lookup"><span data-stu-id="50563-185">To make sure that network traffic is not effected, select a time outside production hours.</span></span>
   >
   >
8. <span data-ttu-id="50563-186">MABS обеспечивает целостность данных за счет проверки реплик на согласованность.</span><span class="sxs-lookup"><span data-stu-id="50563-186">MABS ensures data integrity by performing consistency checks on the replica.</span></span> <span data-ttu-id="50563-187">Доступны два параметра.</span><span class="sxs-lookup"><span data-stu-id="50563-187">There are two available options.</span></span> <span data-ttu-id="50563-188">Вы можете установить расписание проверок согласованности или DPM может выполнять такие проверки в реплике автоматически, как только она становится несогласованной.</span><span class="sxs-lookup"><span data-stu-id="50563-188">You can define a schedule to run consistency checks, or DPM can run consistency checks automatically on the replica whenever it becomes inconsistent.</span></span> <span data-ttu-id="50563-189">Выберите желаемый параметр и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="50563-189">Select your preferred option, and then click **Next**.</span></span>

    ![Проверка согласованности](./media/backup-azure-backup-sharepoint/consistency-check.png)
9. <span data-ttu-id="50563-191">На странице **Указание данных для оперативной защиты** выберите ферму SharePoint, которую нужно защитить, и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="50563-191">On the **Specify Online Protection Data** page, select the SharePoint farm that you want to protect, and then click **Next**.</span></span>

    ![DPM SharePoint Protection1](./media/backup-azure-backup-sharepoint/select-online-protection1.png)
10. <span data-ttu-id="50563-193">На странице **Указание данных для оперативной защиты** выберите желаемое расписание и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="50563-193">On the **Specify Online Backup Schedule** page, select your preferred schedule, and then click **Next**.</span></span>

    ![Online_backup_schedule](./media/backup-azure-backup-sharepoint/specify-online-backup-schedule.png)

    > [!NOTE]
    > <span data-ttu-id="50563-195">MABS поддерживает не более двух резервных копий в Azure за день на основе последней доступной точки резервного копирования диска.</span><span class="sxs-lookup"><span data-stu-id="50563-195">MABS provides a maximum of two daily backups to Azure from the then available latest disk backup point.</span></span> <span data-ttu-id="50563-196">Служба архивации Azure также может контролировать объем пропускной способности глобальной сети, который может использоваться для архивации в пиковые и непиковые часы, с помощью [регулирования сети службы архивации Azure](https://azure.microsoft.com/documentation/articles/backup-configure-vault/#enable-network-throttling).</span><span class="sxs-lookup"><span data-stu-id="50563-196">Azure Backup can also control the amount of WAN bandwidth that can be used for backups in peak and off-peak hours by using [Azure Backup Network Throttling](https://azure.microsoft.com/documentation/articles/backup-configure-vault/#enable-network-throttling).</span></span>
    >
    >
11. <span data-ttu-id="50563-197">В зависимости от выбранного расписания архивации на странице **Укажите политику хранения в сети** выберите политику хранения для ежедневных, еженедельных, ежемесячных и ежегодных точек архивации.</span><span class="sxs-lookup"><span data-stu-id="50563-197">Depending on the backup schedule that you selected, on the **Specify Online Retention Policy** page, select the retention policy for daily, weekly, monthly, and yearly backup points.</span></span>

    ![Online_retention_policy](./media/backup-azure-backup-sharepoint/specify-online-retention.png)

    > [!NOTE]
    > <span data-ttu-id="50563-199">MABS использует трехуровневую схему хранения, которая позволяет выбирать разную политику хранения для разных точек резервного копирования.</span><span class="sxs-lookup"><span data-stu-id="50563-199">MABS uses a grandfather-father-son retention scheme in which a different retention policy can be chosen for different backup points.</span></span>
    >
    >
12. <span data-ttu-id="50563-200">Как и диск, реплика начальной контрольной точки должна быть создана в Azure.</span><span class="sxs-lookup"><span data-stu-id="50563-200">Similar to disk, an initial reference point replica needs to be created in Azure.</span></span> <span data-ttu-id="50563-201">Выберите желаемый параметр для создания начальной резервной копии в Azure и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="50563-201">Select your preferred option to create an initial backup copy to Azure, and then click **Next**.</span></span>

    ![Online_replica](./media/backup-azure-backup-sharepoint/online-replication.png)
13. <span data-ttu-id="50563-203">Просмотрите выбранные параметры на странице **Сводка** и нажмите кнопку **Создать группу**.</span><span class="sxs-lookup"><span data-stu-id="50563-203">Review your selected settings on the **Summary** page, and then click **Create Group**.</span></span> <span data-ttu-id="50563-204">После создания группы защиты появится сообщение об успешном выполнении операции.</span><span class="sxs-lookup"><span data-stu-id="50563-204">You will see a success message after the protection group has been created.</span></span>

    ![Сводка](./media/backup-azure-backup-sharepoint/summary.png)

## <a name="restore-a-sharepoint-item-from-disk-by-using-mabs"></a><span data-ttu-id="50563-206">Восстановление элемента SharePoint с диска с помощью MABS</span><span class="sxs-lookup"><span data-stu-id="50563-206">Restore a SharePoint item from disk by using MABS</span></span>
<span data-ttu-id="50563-207">В приведенном ниже примере *элемент восстановления SharePoint* был случайно удален и должен быть восстановлен.</span><span class="sxs-lookup"><span data-stu-id="50563-207">In the following example, the *Recovering SharePoint item* has been accidentally deleted and needs to be recovered.</span></span>
<span data-ttu-id="50563-208">![DPM SharePoint Protection4](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection5.png)</span><span class="sxs-lookup"><span data-stu-id="50563-208">![MABS SharePoint Protection4](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection5.png)</span></span>

1. <span data-ttu-id="50563-209">Откройте **консоль администратора DPM**.</span><span class="sxs-lookup"><span data-stu-id="50563-209">Open the **DPM Administrator Console**.</span></span> <span data-ttu-id="50563-210">На вкладке **Защита** отображаются все фермы SharePoint, защищаемые DPM.</span><span class="sxs-lookup"><span data-stu-id="50563-210">All SharePoint farms that are protected by DPM are shown in the **Protection** tab.</span></span>

    ![MABS SharePoint Protection3](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection4.png)
2. <span data-ttu-id="50563-212">Чтобы начать восстановление элемента, откройте вкладку **Восстановление** .</span><span class="sxs-lookup"><span data-stu-id="50563-212">To begin to recover the item, select the **Recovery** tab.</span></span>

    ![MABS SharePoint Protection5](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection6.png)
3. <span data-ttu-id="50563-214">Чтобы найти *элемент восстановления SharePoint* , можно использовать поиск на основе подстановки в пределах диапазона точек восстановления.</span><span class="sxs-lookup"><span data-stu-id="50563-214">You can search SharePoint for *Recovering SharePoint item* by using a wildcard-based search within a recovery point range.</span></span>

    ![MABS SharePoint Protection6](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection7.png)
4. <span data-ttu-id="50563-216">Найдите в результатах поиска нужную точку восстановления, щелкните элемент правой кнопкой мыши и выберите пункт **Восстановить**.</span><span class="sxs-lookup"><span data-stu-id="50563-216">Select the appropriate recovery point from the search results, right-click the item, and then select **Recover**.</span></span>
5. <span data-ttu-id="50563-217">Вы можете просмотреть разные точки восстановления и выбрать базу данных или элементы для восстановления.</span><span class="sxs-lookup"><span data-stu-id="50563-217">You can also browse through various recovery points and select a database or item to recover.</span></span> <span data-ttu-id="50563-218">Выберите **дату и время восстановления**, а затем выберите **базу данных, ферму SharePoint, точку восстановления и элемент** в соответствующих полях.</span><span class="sxs-lookup"><span data-stu-id="50563-218">Select **Date > Recovery time**, and then select the correct **Database > SharePoint farm > Recovery point > Item**.</span></span>

    ![MABS SharePoint Protection7](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection8.png)
6. <span data-ttu-id="50563-220">Щелкните элемент правой кнопкой мыши и выберите параметр **Восстановить**, чтобы открыть **мастер восстановления**.</span><span class="sxs-lookup"><span data-stu-id="50563-220">Right-click the item, and then select **Recover** to open the **Recovery Wizard**.</span></span> <span data-ttu-id="50563-221">Щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="50563-221">Click **Next**.</span></span>

    ![Просмотр выбранных параметров восстановления](./media/backup-azure-backup-sharepoint/review-recovery-selection.png)
7. <span data-ttu-id="50563-223">Выберите желаемый тип восстановления и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="50563-223">Select the type of recovery that you want to perform, and then click **Next**.</span></span>

    ![Тип восстановления](./media/backup-azure-backup-sharepoint/select-recovery-type.png)

   > [!NOTE]
   > <span data-ttu-id="50563-225">Выбранный в примере параметр **Восстановить в исходное местоположение** восстанавливает элемент на исходный сайт SharePoint.</span><span class="sxs-lookup"><span data-stu-id="50563-225">The selection of **Recover to original** in the example recovers the item to the original SharePoint site.</span></span>
   >
   >
8. <span data-ttu-id="50563-226">Выберите желаемый **процесс восстановления** на соответствующей странице мастера.</span><span class="sxs-lookup"><span data-stu-id="50563-226">Select the **Recovery Process** that you want to use.</span></span>

   * <span data-ttu-id="50563-227">Если ферма SharePoint не изменилась и находится в том же состоянии, что и в указанной точке восстановления, выберите **Восстановить без фермы восстановления** .</span><span class="sxs-lookup"><span data-stu-id="50563-227">Select **Recover without using a recovery farm** if the SharePoint farm has not changed and is the same as the recovery point that is being restored.</span></span>
   * <span data-ttu-id="50563-228">Если с момента создания точки восстановления ферма SharePoint изменилась, выберите вариант **Восстановление с использованием фермы восстановления** .</span><span class="sxs-lookup"><span data-stu-id="50563-228">Select **Recover using a recovery farm** if the SharePoint farm has changed since the recovery point was created.</span></span>

     ![процесс восстановления](./media/backup-azure-backup-sharepoint/recovery-process.png)
9. <span data-ttu-id="50563-230">Укажите размещение промежуточного экземпляра SQL Server для временного восстановления базы данных, а также промежуточную общую папку на сервере MABS и на сервере, где выполняется SharePoint, для восстановления элемента.</span><span class="sxs-lookup"><span data-stu-id="50563-230">Provide a staging SQL Server instance location to recover the database temporarily, and provide a staging file share on MABS and the server that's running SharePoint to recover the item.</span></span>

    ![Расположение промежуточного хранения 1](./media/backup-azure-backup-sharepoint/staging-location1.png)

    <span data-ttu-id="50563-232">Сервер MABS присоединяет базу данных контента, в которой размещается элемент SharePoint, к временному экземпляру SQL Server.</span><span class="sxs-lookup"><span data-stu-id="50563-232">MABS attaches the content database that is hosting the SharePoint item to the temporary SQL Server instance.</span></span> <span data-ttu-id="50563-233">Затем он восстанавливает элемент из базы данных контента и помещает его в промежуточную папку на сервере MABS.</span><span class="sxs-lookup"><span data-stu-id="50563-233">From the content database, it recovers the item and puts it on the staging file location on MABS.</span></span> <span data-ttu-id="50563-234">Теперь элемент, восстановленный в папке промежуточного хранения, нужно экспортировать в папку промежуточного хранения на ферме SharePoint.</span><span class="sxs-lookup"><span data-stu-id="50563-234">The recovered item that's on the staging location now needs to be exported to the staging location on the SharePoint farm.</span></span>

    ![Расположение промежуточного хранения 2](./media/backup-azure-backup-sharepoint/staging-location2.png)
10. <span data-ttu-id="50563-236">Откройте страницу **Указание параметров восстановления**и примените параметры безопасности к ферме SharePoint или к точке восстановления.</span><span class="sxs-lookup"><span data-stu-id="50563-236">Select **Specify recovery options**, and apply security settings to the SharePoint farm or apply the security settings of the recovery point.</span></span> <span data-ttu-id="50563-237">Щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="50563-237">Click **Next**.</span></span>

    ![Варианты восстановления](./media/backup-azure-backup-sharepoint/recovery-options.png)

    > [!NOTE]
    > <span data-ttu-id="50563-239">Здесь же можно отрегулировать использование пропускной способности сети.</span><span class="sxs-lookup"><span data-stu-id="50563-239">You can choose to throttle the network bandwidth usage.</span></span> <span data-ttu-id="50563-240">Это позволит сократить нежелательную нагрузку на сервер в рабочие часы.</span><span class="sxs-lookup"><span data-stu-id="50563-240">This minimizes impact to the production server during production hours.</span></span>
    >
    >
11. <span data-ttu-id="50563-241">Просмотрите сводные данные и нажмите кнопку **Восстановить** , чтобы начать восстановление файла.</span><span class="sxs-lookup"><span data-stu-id="50563-241">Review the summary information, and then click **Recover** to begin recovery of the file.</span></span>

    ![Сводка параметров восстановления](./media/backup-azure-backup-sharepoint/recovery-summary.png)
12. <span data-ttu-id="50563-243">Теперь откройте вкладку **Мониторинг** в **консоли администратора MABS** и проверьте **состояние** восстановления.</span><span class="sxs-lookup"><span data-stu-id="50563-243">Now select the **Monitoring** tab in the **MABS Administrator Console** to view the **Status** of the recovery.</span></span>

    ![Состояние восстановления](./media/backup-azure-backup-sharepoint/recovery-monitoring.png)

    > [!NOTE]
    > <span data-ttu-id="50563-245">Файл восстановлен.</span><span class="sxs-lookup"><span data-stu-id="50563-245">The file is now restored.</span></span> <span data-ttu-id="50563-246">Обновите сайт SharePoint, чтобы проверить восстановленный файл.</span><span class="sxs-lookup"><span data-stu-id="50563-246">You can refresh the SharePoint site to check the restored file.</span></span>
    >
    >

## <a name="restore-a-sharepoint-database-from-azure-by-using-dpm"></a><span data-ttu-id="50563-247">Восстановление базы данных SharePoint из Azure с помощью DPM</span><span class="sxs-lookup"><span data-stu-id="50563-247">Restore a SharePoint database from Azure by using DPM</span></span>
1. <span data-ttu-id="50563-248">Чтобы восстановить базу данных контента SharePoint, просмотрите различные точки восстановления (как было показано ранее) и выберите желаемую точку восстановления.</span><span class="sxs-lookup"><span data-stu-id="50563-248">To recover a SharePoint content database, browse through various recovery points (as shown previously), and select the recovery point that you want to restore.</span></span>

    ![MABS SharePoint Protection8](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection9.png)
2. <span data-ttu-id="50563-250">Дважды щелкните точку восстановления SharePoint, чтобы отобразить доступные регистрационные сведения SharePoint.</span><span class="sxs-lookup"><span data-stu-id="50563-250">Double-click the SharePoint recovery point to show the available SharePoint catalog information.</span></span>

   > [!NOTE]
   > <span data-ttu-id="50563-251">Так как длительное хранение фермы SharePoint выполняется в Azure, на сервере MABS нет доступных сведений (метаданных) для каталога.</span><span class="sxs-lookup"><span data-stu-id="50563-251">Because the SharePoint farm is protected for long-term retention in Azure, no catalog information (metadata) is available on MABS.</span></span> <span data-ttu-id="50563-252">В результате каждый раз, когда базу данных контента SharePoint требуется вернуть в состояние на определенный момент, необходимо каталогизировать ферму SharePoint заново.</span><span class="sxs-lookup"><span data-stu-id="50563-252">As a result, whenever a point-in-time SharePoint content database needs to be recovered, you need to catalog the SharePoint farm again.</span></span>
   >
   >
3. <span data-ttu-id="50563-253">Нажмите кнопку **Повторить каталогизацию**.</span><span class="sxs-lookup"><span data-stu-id="50563-253">Click **Re-catalog**.</span></span>

    ![MABS SharePoint Protection10](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection12.png)

    <span data-ttu-id="50563-255">Откроется окно состояния **Повторная каталогизация облака** .</span><span class="sxs-lookup"><span data-stu-id="50563-255">The **Cloud Recatalog** status window opens.</span></span>

    ![MABS SharePoint Protection11](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection13.png)

    <span data-ttu-id="50563-257">После завершения каталогизации состояние изменится на *Успешно*.</span><span class="sxs-lookup"><span data-stu-id="50563-257">After cataloging is finished, the status changes to *Success*.</span></span> <span data-ttu-id="50563-258">Нажмите кнопку **Закрыть**</span><span class="sxs-lookup"><span data-stu-id="50563-258">Click **Close**.</span></span>

    ![MABS SharePoint Protection12](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection14.png)
4. <span data-ttu-id="50563-260">Щелкните объект SharePoint на вкладке MABS **Восстановление**, чтобы получить структуру базы данных контента.</span><span class="sxs-lookup"><span data-stu-id="50563-260">Click the SharePoint object shown in the MABS **Recovery** tab to get the content database structure.</span></span> <span data-ttu-id="50563-261">Щелкните элемент правой кнопкой мыши и выберите **Восстановить**.</span><span class="sxs-lookup"><span data-stu-id="50563-261">Right-click the item, and then click **Recover**.</span></span>

    ![MABS SharePoint Protection13](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection15.png)
5. <span data-ttu-id="50563-263">Выполните [процедуру восстановления, описанную ранее в этой статье](#restore-a-sharepoint-item-from-disk-using-dpm) , чтобы восстановить базу данных контента SharePoint с диска.</span><span class="sxs-lookup"><span data-stu-id="50563-263">At this point, follow the [recovery steps earlier in this article](#restore-a-sharepoint-item-from-disk-using-dpm) to recover a SharePoint content database from disk.</span></span>

## <a name="faqs"></a><span data-ttu-id="50563-264">Часто задаваемые вопросы</span><span class="sxs-lookup"><span data-stu-id="50563-264">FAQs</span></span>
<span data-ttu-id="50563-265">В. Можно ли восстановить элемент SharePoint в исходное расположение, если SharePoint настроен с использованием SQL AlwaysOn (с защитой на диске)?</span><span class="sxs-lookup"><span data-stu-id="50563-265">Q: Can I recover a SharePoint item to the original location if SharePoint is configured by using SQL AlwaysOn (with protection on disk)?</span></span><br>
<span data-ttu-id="50563-266">О. Да, элемент можно восстановить на исходный сайт SharePoint.</span><span class="sxs-lookup"><span data-stu-id="50563-266">A: Yes, the item can be recovered to the original SharePoint site.</span></span>

<span data-ttu-id="50563-267">В. Можно ли восстановить базу данных SharePoint в исходное расположение, если SharePoint настроен с использованием SQL AlwaysOn?</span><span class="sxs-lookup"><span data-stu-id="50563-267">Q: Can I recover a SharePoint database to the original location if SharePoint is configured by using SQL AlwaysOn?</span></span><br>
<span data-ttu-id="50563-268">О. Так как базы данных SharePoint настраиваются в SQL AlwaysOn, их нельзя изменить, не удалив группу доступности.</span><span class="sxs-lookup"><span data-stu-id="50563-268">A: Because SharePoint databases are configured in SQL AlwaysOn, they cannot be modified unless the availability group is removed.</span></span> <span data-ttu-id="50563-269">В связи с этим сервер MABS не может восстанавливать базы данных в исходное расположение.</span><span class="sxs-lookup"><span data-stu-id="50563-269">As a result, MABS cannot restore a database to the original location.</span></span> <span data-ttu-id="50563-270">Вы можете восстановить базу данных SQL Server в другой экземпляр SQL Server.</span><span class="sxs-lookup"><span data-stu-id="50563-270">You can recover a SQL Server database to another SQL Server instance.</span></span>

## <a name="next-steps"></a><span data-ttu-id="50563-271">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="50563-271">Next steps</span></span>
* <span data-ttu-id="50563-272">Дополнительные сведения о защите SharePoint с помощью MABS см. в [этой серии видеоматериалов](http://channel9.msdn.com/Series/Azure-Backup/Microsoft-SCDPM-Protection-of-SharePoint-1-of-2-How-to-create-a-SharePoint-Protection-Group).</span><span class="sxs-lookup"><span data-stu-id="50563-272">Learn more about MABS Protection of SharePoint - see [Video Series - DPM Protection of SharePoint](http://channel9.msdn.com/Series/Azure-Backup/Microsoft-SCDPM-Protection-of-SharePoint-1-of-2-How-to-create-a-SharePoint-Protection-Group)</span></span>
