---
title: "Здравствуйте, aaaManage аналитики Озера данных Azure с помощью портала Azure | Документы Microsoft"
description: "Дополнительные сведения о том, как toomanage учебных аналитики Озера данных, данных источники, пользователей и заданий."
services: data-lake-analytics
documentationcenter: 
author: saveenr
manager: jhubbard
editor: cgronlun
ms.assetid: a0e045f1-73d6-427f-868d-7b55c10f811b
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 12/05/2016
ms.author: edmaca
ms.openlocfilehash: f63ccdfae79772c92e92462194e8cdc636a73dc6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-data-lake-analytics-by-using-hello-azure-portal"></a><span data-ttu-id="189e0-103">Управление аналитики Озера данных Azure с помощью портала Azure hello</span><span class="sxs-lookup"><span data-stu-id="189e0-103">Manage Azure Data Lake Analytics by using hello Azure portal</span></span>
[!INCLUDE [manage-selector](../../includes/data-lake-analytics-selector-manage.md)]

<span data-ttu-id="189e0-104">Узнайте, как учетные записи toomanage аналитики Озера данных Azure, учетная запись источников данных, пользователей и заданий с помощью hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="189e0-104">Learn how toomanage Azure Data Lake Analytics accounts, account data sources, users, and jobs by using hello Azure portal.</span></span> <span data-ttu-id="189e0-105">статьи, посвященные управлению toosee об использовании других средств вкладку вверху hello страницы приветствия.</span><span class="sxs-lookup"><span data-stu-id="189e0-105">toosee management topics about using other tools, click a tab at hello top of hello page.</span></span>

<!-- ################################ -->
<!-- ################################ -->

## <a name="manage-data-lake-analytics-accounts"></a><span data-ttu-id="189e0-106">Управление учетными записями Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="189e0-106">Manage Data Lake Analytics accounts</span></span>

### <a name="create-an-account"></a><span data-ttu-id="189e0-107">Создание учетной записи</span><span class="sxs-lookup"><span data-stu-id="189e0-107">Create an account</span></span>

1. <span data-ttu-id="189e0-108">Войдите в toohello [портал Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="189e0-108">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="189e0-109">Щелкните **Создать** > **Аналитика** > **Data Lake Analytics**.</span><span class="sxs-lookup"><span data-stu-id="189e0-109">Click **New** > **Intelligence + analytics** > **Data Lake Analytics**.</span></span>
3. <span data-ttu-id="189e0-110">Выберите значения для hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="189e0-110">Select values for hello following items:</span></span> 
   1. <span data-ttu-id="189e0-111">**Имя**: hello имя hello учетной записи аналитики Озера данных.</span><span class="sxs-lookup"><span data-stu-id="189e0-111">**Name**: hello name of hello Data Lake Analytics account.</span></span>
   2. <span data-ttu-id="189e0-112">**Подписки**: hello подписки Azure для использования учетной записи hello.</span><span class="sxs-lookup"><span data-stu-id="189e0-112">**Subscription**: hello Azure subscription used for hello account.</span></span>
   3. <span data-ttu-id="189e0-113">**Группа ресурсов**: hello группы ресурсов Azure в учетную запись, которая hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="189e0-113">**Resource Group**: hello Azure resource group in which toocreate hello account.</span></span> 
   4. <span data-ttu-id="189e0-114">**Расположение**: hello центра обработки данных Azure для учетной записи аналитики Озера данных hello.</span><span class="sxs-lookup"><span data-stu-id="189e0-114">**Location**: hello Azure datacenter for hello Data Lake Analytics account.</span></span> 
   5. <span data-ttu-id="189e0-115">**Хранилище Озера данных**: hello toobe хранилища по умолчанию для использования учетной записи аналитики Озера данных hello.</span><span class="sxs-lookup"><span data-stu-id="189e0-115">**Data Lake Store**: hello default store toobe used for hello Data Lake Analytics account.</span></span> <span data-ttu-id="189e0-116">Учетная запись хранилища Озера данных Azure Hello и hello учетная запись должна быть в аналитике Озера данных hello местоположения.</span><span class="sxs-lookup"><span data-stu-id="189e0-116">hello Azure Data Lake Store account and hello Data Lake Analytics account must be in hello same location.</span></span>
4. <span data-ttu-id="189e0-117">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="189e0-117">Click **Create**.</span></span> 

### <a name="delete-a-data-lake-analytics-account"></a><span data-ttu-id="189e0-118">Удаление учетной записи Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="189e0-118">Delete a Data Lake Analytics account</span></span>

<span data-ttu-id="189e0-119">Перед удалением учетной записи Data Lake Analytics необходимо удалить учетную запись Data Lake Store по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="189e0-119">Before you delete a Data Lake Analytics account, delete its default Data Lake Store account.</span></span>

1. <span data-ttu-id="189e0-120">В hello портал Azure выберите учетную запись аналитики Озера данных tooyour.</span><span class="sxs-lookup"><span data-stu-id="189e0-120">In hello Azure portal, go tooyour Data Lake Analytics account.</span></span>
2. <span data-ttu-id="189e0-121">Нажмите кнопку **Delete**(Удалить).</span><span class="sxs-lookup"><span data-stu-id="189e0-121">Click **Delete**.</span></span>
3. <span data-ttu-id="189e0-122">Имя учетной записи типа hello.</span><span class="sxs-lookup"><span data-stu-id="189e0-122">Type hello account name.</span></span>
4. <span data-ttu-id="189e0-123">Нажмите кнопку **Delete**(Удалить).</span><span class="sxs-lookup"><span data-stu-id="189e0-123">Click **Delete**.</span></span>

<!-- ################################ -->
<!-- ################################ -->

## <a name="manage-data-sources"></a><span data-ttu-id="189e0-124">Управление источниками данных</span><span class="sxs-lookup"><span data-stu-id="189e0-124">Manage data sources</span></span>

<span data-ttu-id="189e0-125">Аналитика Озера данных поддерживает следующие источники данных hello:</span><span class="sxs-lookup"><span data-stu-id="189e0-125">Data Lake Analytics supports hello following data sources:</span></span>

* <span data-ttu-id="189e0-126">Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="189e0-126">Data Lake Store</span></span>
* <span data-ttu-id="189e0-127">Хранилище Azure</span><span class="sxs-lookup"><span data-stu-id="189e0-127">Azure Storage</span></span>

<span data-ttu-id="189e0-128">Можно использовать источники данных toobrowse обозреватель данных и выполнения операций управления базовый файл.</span><span class="sxs-lookup"><span data-stu-id="189e0-128">You can use Data Explorer toobrowse data sources and perform basic file management operations.</span></span> 

### <a name="add-a-data-source"></a><span data-ttu-id="189e0-129">Добавление источника данных</span><span class="sxs-lookup"><span data-stu-id="189e0-129">Add a data source</span></span>

1. <span data-ttu-id="189e0-130">В hello портал Azure выберите учетную запись аналитики Озера данных tooyour.</span><span class="sxs-lookup"><span data-stu-id="189e0-130">In hello Azure portal, go tooyour Data Lake Analytics account.</span></span>
2. <span data-ttu-id="189e0-131">Щелкните **Источники данных**.</span><span class="sxs-lookup"><span data-stu-id="189e0-131">Click **Data Sources**.</span></span>
3. <span data-ttu-id="189e0-132">Щелкните **Добавить источник данных**.</span><span class="sxs-lookup"><span data-stu-id="189e0-132">Click **Add Data Source**.</span></span>
    
   * <span data-ttu-id="189e0-133">tooadd учетной записи хранилища Озера данных необходима учетная запись hello toohello имя и доступа к учетной записи может tooquery toobe его.</span><span class="sxs-lookup"><span data-stu-id="189e0-133">tooadd a Data Lake Store account, you need hello account name and access toohello account toobe able tooquery it.</span></span>
   * <span data-ttu-id="189e0-134">tooadd хранилища больших двоичных объектов Azure, необходимо hello учетной записи хранилища и ключ учетной записи hello.</span><span class="sxs-lookup"><span data-stu-id="189e0-134">tooadd Azure Blob storage, you need hello storage account and hello account key.</span></span> <span data-ttu-id="189e0-135">toofind учетной записи toohello их, перейдите на портал hello.</span><span class="sxs-lookup"><span data-stu-id="189e0-135">toofind them, go toohello storage account in hello portal.</span></span>

## <a name="set-up-firewall-rules"></a><span data-ttu-id="189e0-136">Настройка правил брандмауэра</span><span class="sxs-lookup"><span data-stu-id="189e0-136">Set up firewall rules</span></span>

<span data-ttu-id="189e0-137">Аналитика Озера данных toofurther блокировка tooyour доступа учетной записи аналитики Озера данных можно использовать на уровне сети hello.</span><span class="sxs-lookup"><span data-stu-id="189e0-137">You can use Data Lake Analytics toofurther lock down access tooyour Data Lake Analytics account at hello network level.</span></span> <span data-ttu-id="189e0-138">Вы можете включить брандмауэр, указать IP-адрес или определить диапазон IP-адресов для доверенных клиентов.</span><span class="sxs-lookup"><span data-stu-id="189e0-138">You can enable a firewall, specify an IP address, or define an IP address range for your trusted clients.</span></span> <span data-ttu-id="189e0-139">После включения этих мер только клиенты, hello IP-адреса в диапазоне определенных hello можно подключить хранилище toohello.</span><span class="sxs-lookup"><span data-stu-id="189e0-139">After you enable these measures, only clients that have hello IP addresses within hello defined range can connect toohello store.</span></span>

<span data-ttu-id="189e0-140">Если другие службы Azure, например фабрики данных Azure или виртуальные машины, подключить учетную запись аналитики Озера данных toohello, убедитесь, что **разрешить службам Azure** включена **на**.</span><span class="sxs-lookup"><span data-stu-id="189e0-140">If other Azure services, like Azure Data Factory or VMs, connect toohello Data Lake Analytics account, make sure that **Allow Azure Services** is turned **On**.</span></span> 

### <a name="set-up-a-firewall-rule"></a><span data-ttu-id="189e0-141">Настройка правила брандмауэра.</span><span class="sxs-lookup"><span data-stu-id="189e0-141">Set up a firewall rule</span></span>

1. <span data-ttu-id="189e0-142">В hello портал Azure выберите учетную запись аналитики Озера данных tooyour.</span><span class="sxs-lookup"><span data-stu-id="189e0-142">In hello Azure portal, go tooyour Data Lake Analytics account.</span></span>
2. <span data-ttu-id="189e0-143">Hello слева hello меню **брандмауэра**.</span><span class="sxs-lookup"><span data-stu-id="189e0-143">On hello menu on hello left, click **Firewall**.</span></span>

## <a name="add-a-new-user"></a><span data-ttu-id="189e0-144">Добавление нового пользователя</span><span class="sxs-lookup"><span data-stu-id="189e0-144">Add a new user</span></span>

<span data-ttu-id="189e0-145">Можно использовать hello **мастера добавления пользователей** tooeasily при появлении новых пользователей Озера данных.</span><span class="sxs-lookup"><span data-stu-id="189e0-145">You can use hello **Add User Wizard** tooeasily provision new Data Lake users.</span></span>

1. <span data-ttu-id="189e0-146">В hello портал Azure выберите учетную запись аналитики Озера данных tooyour.</span><span class="sxs-lookup"><span data-stu-id="189e0-146">In hello Azure portal, go tooyour Data Lake Analytics account.</span></span>
2. <span data-ttu-id="189e0-147">На hello слева в разделе **Приступая к работе**, нажмите кнопку **мастера добавления пользователей**.</span><span class="sxs-lookup"><span data-stu-id="189e0-147">On hello left, under **Getting Started**, click **Add User Wizard**.</span></span>
3. <span data-ttu-id="189e0-148">Выберите пользователя и нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="189e0-148">Select a user, and then click **Select**.</span></span>
4. <span data-ttu-id="189e0-149">Выберите роль и нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="189e0-149">Select a role, and then click **Select**.</span></span> <span data-ttu-id="189e0-150">tooset копирование новых toouse разработчика Озера данных Azure, выберите hello **разработчика аналитика Озера данных** роли.</span><span class="sxs-lookup"><span data-stu-id="189e0-150">tooset up a new developer toouse Azure Data Lake, select hello **Data Lake Analytics Developer** role.</span></span>
5. <span data-ttu-id="189e0-151">Выберите hello управления доступом (ACL) для баз данных hello U-SQL.</span><span class="sxs-lookup"><span data-stu-id="189e0-151">Select hello access control lists (ACLs) for hello U-SQL databases.</span></span> <span data-ttu-id="189e0-152">Когда нужные параметры настроены, нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="189e0-152">When you're satisfied with your choices, click **Select**.</span></span>
6. <span data-ttu-id="189e0-153">Выберите hello списки управления доступом для файлов.</span><span class="sxs-lookup"><span data-stu-id="189e0-153">Select hello ACLs for files.</span></span> <span data-ttu-id="189e0-154">Не изменяйте hello ACL для hello корневая папка для хранилища по умолчанию hello, «/» и для папки/System hello.</span><span class="sxs-lookup"><span data-stu-id="189e0-154">For hello default store, don't change hello ACLs for hello root folder "/" and for hello /system folder.</span></span> <span data-ttu-id="189e0-155">Нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="189e0-155">Click **Select**.</span></span>
7. <span data-ttu-id="189e0-156">Просмотрите выбранные изменения и нажмите кнопку **Выполнить**.</span><span class="sxs-lookup"><span data-stu-id="189e0-156">Review all your selected changes, and then click **Run**.</span></span>
8. <span data-ttu-id="189e0-157">После завершения работы мастера hello, нажмите кнопку **сделать**.</span><span class="sxs-lookup"><span data-stu-id="189e0-157">When hello wizard is finished, click **Done**.</span></span>

## <a name="manage-role-based-access-control"></a><span data-ttu-id="189e0-158">Управление доступом на основе ролей</span><span class="sxs-lookup"><span data-stu-id="189e0-158">Manage Role-Based Access Control</span></span>

<span data-ttu-id="189e0-159">Как и другие службы Azure можно использовать toocontrol управление доступом на основе ролей (RBAC), как пользователи взаимодействуют со службой hello.</span><span class="sxs-lookup"><span data-stu-id="189e0-159">Like other Azure services, you can use Role-Based Access Control (RBAC) toocontrol how users interact with hello service.</span></span>

<span data-ttu-id="189e0-160">стандартные роли RBAC Hello имеют hello следующие возможности:</span><span class="sxs-lookup"><span data-stu-id="189e0-160">hello standard RBAC roles have hello following capabilities:</span></span>
* <span data-ttu-id="189e0-161">**Владелец**: можно отправлять задания, отслеживайте задания, отмена заданий из любой пользователь и настроить учетную запись hello.</span><span class="sxs-lookup"><span data-stu-id="189e0-161">**Owner**: Can submit jobs, monitor jobs, cancel jobs from any user, and configure hello account.</span></span>
* <span data-ttu-id="189e0-162">**Участник**: можно отправлять задания, отслеживайте задания, отмена заданий из любой пользователь и настроить учетную запись hello.</span><span class="sxs-lookup"><span data-stu-id="189e0-162">**Contributor**: Can submit jobs, monitor jobs, cancel jobs from any user, and configure hello account.</span></span>
* <span data-ttu-id="189e0-163">**Читатель**: может отслеживать задания.</span><span class="sxs-lookup"><span data-stu-id="189e0-163">**Reader**: Can monitor jobs.</span></span>

<span data-ttu-id="189e0-164">Использование hello разработчика аналитика Озера данных роли tooenable U-SQL разработчики toouse hello аналитики Озера данных службы.</span><span class="sxs-lookup"><span data-stu-id="189e0-164">Use hello Data Lake Analytics Developer role tooenable U-SQL developers toouse hello Data Lake Analytics service.</span></span> <span data-ttu-id="189e0-165">Вы можете использовать роль разработчика аналитика Озера данных hello для:</span><span class="sxs-lookup"><span data-stu-id="189e0-165">You can use hello Data Lake Analytics Developer role to:</span></span>
* <span data-ttu-id="189e0-166">отправки заданий;</span><span class="sxs-lookup"><span data-stu-id="189e0-166">Submit jobs.</span></span>
* <span data-ttu-id="189e0-167">Отслеживать ход выполнения состояние и hello задания отправленного заданий.</span><span class="sxs-lookup"><span data-stu-id="189e0-167">Monitor job status and hello progress of jobs submitted by any user.</span></span>
* <span data-ttu-id="189e0-168">См. в сценарии hello U-SQL из отправленного задания.</span><span class="sxs-lookup"><span data-stu-id="189e0-168">See hello U-SQL scripts from jobs submitted by any user.</span></span>
* <span data-ttu-id="189e0-169">отмены собственных заданий.</span><span class="sxs-lookup"><span data-stu-id="189e0-169">Cancel only your own jobs.</span></span>

### <a name="add-users-or-security-groups-tooa-data-lake-analytics-account"></a><span data-ttu-id="189e0-170">Добавление пользователей или групп безопасности tooa учетной записи аналитики Озера данных</span><span class="sxs-lookup"><span data-stu-id="189e0-170">Add users or security groups tooa Data Lake Analytics account</span></span>

1. <span data-ttu-id="189e0-171">В hello портал Azure выберите учетную запись аналитики Озера данных tooyour.</span><span class="sxs-lookup"><span data-stu-id="189e0-171">In hello Azure portal, go tooyour Data Lake Analytics account.</span></span>
2. <span data-ttu-id="189e0-172">Щелкните **Управление доступом (IAM)** > **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="189e0-172">Click **Access control (IAM)** > **Add**.</span></span>
3. <span data-ttu-id="189e0-173">Выберите роль.</span><span class="sxs-lookup"><span data-stu-id="189e0-173">Select a role.</span></span>
4. <span data-ttu-id="189e0-174">Добавьте пользователя.</span><span class="sxs-lookup"><span data-stu-id="189e0-174">Add a user.</span></span>
5. <span data-ttu-id="189e0-175">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="189e0-175">Click **OK**.</span></span>

>[!NOTE]
><span data-ttu-id="189e0-176">Если пользователь или группа безопасности должна toosubmit заданий, они также требуется разрешение на учетную запись хранилища hello.</span><span class="sxs-lookup"><span data-stu-id="189e0-176">If a user or a security group needs toosubmit jobs, they also need permission on hello store account.</span></span> <span data-ttu-id="189e0-177">Дополнительные сведения см. в статье [Защита данных, хранимых в Azure Data Lake Store](../data-lake-store/data-lake-store-secure-data.md).</span><span class="sxs-lookup"><span data-stu-id="189e0-177">For more information, see [Secure data stored in Data Lake Store](../data-lake-store/data-lake-store-secure-data.md).</span></span>
>

<!-- ################################ -->
<!-- ################################ -->

## <a name="manage-jobs"></a><span data-ttu-id="189e0-178">Управление заданиями</span><span class="sxs-lookup"><span data-stu-id="189e0-178">Manage jobs</span></span>

### <a name="submit-a-job"></a><span data-ttu-id="189e0-179">Отправка задания</span><span class="sxs-lookup"><span data-stu-id="189e0-179">Submit a job</span></span>

1. <span data-ttu-id="189e0-180">В hello портал Azure выберите учетную запись аналитики Озера данных tooyour.</span><span class="sxs-lookup"><span data-stu-id="189e0-180">In hello Azure portal, go tooyour Data Lake Analytics account.</span></span>

2. <span data-ttu-id="189e0-181">Нажмите кнопку **Создать задание**.</span><span class="sxs-lookup"><span data-stu-id="189e0-181">Click **New Job**.</span></span> <span data-ttu-id="189e0-182">Настройте для каждого задания:</span><span class="sxs-lookup"><span data-stu-id="189e0-182">For each job,  configure:</span></span>

    1. <span data-ttu-id="189e0-183">**Имя задания**: hello имя задания hello.</span><span class="sxs-lookup"><span data-stu-id="189e0-183">**Job Name**: hello name of hello job.</span></span>
    2. <span data-ttu-id="189e0-184">**Приоритет**: чем меньше число, тем выше приоритет.</span><span class="sxs-lookup"><span data-stu-id="189e0-184">**Priority**: Lower numbers have higher priority.</span></span> <span data-ttu-id="189e0-185">Если два задания помещаются в очередь, в первую очередь выполняется hello один меньшее значение приоритета.</span><span class="sxs-lookup"><span data-stu-id="189e0-185">If two jobs are queued, hello one with lower priority value runs first.</span></span>
    3. <span data-ttu-id="189e0-186">**Параллелизм**: hello максимальное число вычислительных процессов tooreserve для этого задания.</span><span class="sxs-lookup"><span data-stu-id="189e0-186">**Parallelism**: hello maximum number of compute processes tooreserve for this job.</span></span>

3. <span data-ttu-id="189e0-187">Щелкните **Отправить задание**.</span><span class="sxs-lookup"><span data-stu-id="189e0-187">Click **Submit Job**.</span></span>

### <a name="monitor-jobs"></a><span data-ttu-id="189e0-188">Мониторинг заданий</span><span class="sxs-lookup"><span data-stu-id="189e0-188">Monitor jobs</span></span>

1. <span data-ttu-id="189e0-189">В hello портал Azure выберите учетную запись аналитики Озера данных tooyour.</span><span class="sxs-lookup"><span data-stu-id="189e0-189">In hello Azure portal, go tooyour Data Lake Analytics account.</span></span>
2. <span data-ttu-id="189e0-190">Щелкните **Просмотр всех заданий**.</span><span class="sxs-lookup"><span data-stu-id="189e0-190">Click **View All Jobs**.</span></span> <span data-ttu-id="189e0-191">Отображается список всех hello active и недавно завершенных заданий в учетной записи hello.</span><span class="sxs-lookup"><span data-stu-id="189e0-191">A list of all hello active and recently finished jobs in hello account is shown.</span></span>
3. <span data-ttu-id="189e0-192">При необходимости щелкните **фильтра** toohelp найти hello заданий по **диапазон времени**, **имя задания**, и **автор** значения.</span><span class="sxs-lookup"><span data-stu-id="189e0-192">Optionally, click **Filter** toohelp you find hello jobs by **Time Range**, **Job Name**, and **Author** values.</span></span> 

### <a name="monitoring-pipeline-jobs"></a><span data-ttu-id="189e0-193">Отслеживание заданий конвейера</span><span class="sxs-lookup"><span data-stu-id="189e0-193">Monitoring pipeline jobs</span></span>
<span data-ttu-id="189e0-194">Задания, которые являются частью конвейера работают вместе, обычно последовательно tooaccomplish конкретного сценария.</span><span class="sxs-lookup"><span data-stu-id="189e0-194">Jobs that are part of a pipeline work together, usually sequentially, tooaccomplish a specific scenario.</span></span> <span data-ttu-id="189e0-195">Например, вы можете иметь конвейер, который очищает, извлекает, преобразует и содержит статистические данные, используемые при работе с клиентами.</span><span class="sxs-lookup"><span data-stu-id="189e0-195">For example, you can have a pipeline that cleans, extracts, transforms, aggregates usage for customer insights.</span></span> <span data-ttu-id="189e0-196">Конвейер задания устанавливаются с помощью свойства «Конвейер» hello, когда задания hello.</span><span class="sxs-lookup"><span data-stu-id="189e0-196">Pipeline jobs are identified using hello "Pipeline" property when hello job was submitted.</span></span> <span data-ttu-id="189e0-197">В заданиях, запланированных с помощью ADF V2, эти свойства заполняются автоматически.</span><span class="sxs-lookup"><span data-stu-id="189e0-197">Jobs scheduled using ADF V2 will automatically have this property populated.</span></span> 

<span data-ttu-id="189e0-198">tooview список заданий U-SQL, которые являются частью конвейеры:</span><span class="sxs-lookup"><span data-stu-id="189e0-198">tooview a list of U-SQL jobs that are part of pipelines:</span></span> 

1. <span data-ttu-id="189e0-199">В hello портал Azure перейдите на учетные записи tooyour аналитики Озера данных.</span><span class="sxs-lookup"><span data-stu-id="189e0-199">In hello Azure portal, go tooyour Data Lake Analytics accounts.</span></span>
2. <span data-ttu-id="189e0-200">Выберите **Подробные сведения о заданиях**.</span><span class="sxs-lookup"><span data-stu-id="189e0-200">Click **Job Insights**.</span></span> <span data-ttu-id="189e0-201">Привет, вкладка «Все заданий» будет установлено значение по умолчанию, отображая список запущена, в очередь и окончания задания.</span><span class="sxs-lookup"><span data-stu-id="189e0-201">hello "All Jobs" tab will be defaulted, showing a list of running, queued, and ended jobs.</span></span>
3. <span data-ttu-id="189e0-202">Нажмите кнопку hello **заданий конвейера** вкладки. Список заданий конвейера будет отображаться со сводными статистическими данными по каждому конвейеру.</span><span class="sxs-lookup"><span data-stu-id="189e0-202">Click hello **Pipeline Jobs** tab. A list of pipeline jobs will be shown along with aggregated statistics for each pipeline.</span></span>

### <a name="monitoring-recurring-jobs"></a><span data-ttu-id="189e0-203">Отслеживание повторяющихся заданий</span><span class="sxs-lookup"><span data-stu-id="189e0-203">Monitoring recurring jobs</span></span>
<span data-ttu-id="189e0-204">Повторяющееся задание должна иметь hello же бизнес-логика, но использует другой входных данных, при каждом запуске.</span><span class="sxs-lookup"><span data-stu-id="189e0-204">A recurring job is one that has hello same business logic but uses different input data every time it runs.</span></span> <span data-ttu-id="189e0-205">В идеальном случае повторяющихся заданий всегда должна завершиться успешно и имеют относительно устойчивой времени выполнения; отслеживание этих поведения поможет обеспечить успешную hello задание находится в работоспособном состоянии.</span><span class="sxs-lookup"><span data-stu-id="189e0-205">Ideally, recurring jobs should always succeed, and have relatively stable execution time; monitoring these behaviors will help ensure hello job is healthy.</span></span> <span data-ttu-id="189e0-206">Повторяющиеся задания идентифицируются с помощью свойства «Повторение» hello.</span><span class="sxs-lookup"><span data-stu-id="189e0-206">Recurring jobs are identified using hello "Recurrence" property.</span></span> <span data-ttu-id="189e0-207">В заданиях, запланированных с помощью ADF V2, эти свойства заполняются автоматически.</span><span class="sxs-lookup"><span data-stu-id="189e0-207">Jobs scheduled using ADF V2 will automatically have this property populated.</span></span>

<span data-ttu-id="189e0-208">tooview список заданий U-SQL, которые являются:</span><span class="sxs-lookup"><span data-stu-id="189e0-208">tooview a list of U-SQL jobs that are recurring:</span></span> 

1. <span data-ttu-id="189e0-209">В hello портал Azure перейдите на учетные записи tooyour аналитики Озера данных.</span><span class="sxs-lookup"><span data-stu-id="189e0-209">In hello Azure portal, go tooyour Data Lake Analytics accounts.</span></span>
2. <span data-ttu-id="189e0-210">Выберите **Подробные сведения о заданиях**.</span><span class="sxs-lookup"><span data-stu-id="189e0-210">Click **Job Insights**.</span></span> <span data-ttu-id="189e0-211">Привет, вкладка «Все заданий» будет установлено значение по умолчанию, отображая список запущена, в очередь и окончания задания.</span><span class="sxs-lookup"><span data-stu-id="189e0-211">hello "All Jobs" tab will be defaulted, showing a list of running, queued, and ended jobs.</span></span>
3. <span data-ttu-id="189e0-212">Нажмите кнопку hello **повторяющихся заданий** вкладки. Список повторяющихся заданий будет отображаться со сводными статистическими данными по повторяющемуся заданию.</span><span class="sxs-lookup"><span data-stu-id="189e0-212">Click hello **Recurring Jobs** tab. A list of recurring jobs will be shown along with aggregated statistics for each recurring job.</span></span>

## <a name="manage-policies"></a><span data-ttu-id="189e0-213">Управление политиками</span><span class="sxs-lookup"><span data-stu-id="189e0-213">Manage policies</span></span>

### <a name="account-level-policies"></a><span data-ttu-id="189e0-214">Политики на уровне учетной записи</span><span class="sxs-lookup"><span data-stu-id="189e0-214">Account-level policies</span></span>

<span data-ttu-id="189e0-215">Эти политики применяются tooall заданий в учетной записи аналитики Озера данных.</span><span class="sxs-lookup"><span data-stu-id="189e0-215">These policies apply tooall jobs in a Data Lake Analytics account.</span></span>

#### <a name="maximum-number-of-aus-in-a-data-lake-analytics-account"></a><span data-ttu-id="189e0-216">Максимальное число единиц использования аналитики в учетной записи Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="189e0-216">Maximum number of AUs in a Data Lake Analytics account</span></span>
<span data-ttu-id="189e0-217">Политика управляет hello общее число единиц аналитика (AUs) можно использовать учетную запись аналитики Озера данных.</span><span class="sxs-lookup"><span data-stu-id="189e0-217">A policy controls hello total number of Analytics Units (AUs) your Data Lake Analytics account can use.</span></span> <span data-ttu-id="189e0-218">По умолчанию hello устанавливается too250.</span><span class="sxs-lookup"><span data-stu-id="189e0-218">By default, hello value is set too250.</span></span> <span data-ttu-id="189e0-219">Например, если имеет значение too250 AUs, может иметь одно задание, выполнив 250 Сиднейское назначенный tooit или 10 заданий, выполняемых с 25 Сиднейское каждого.</span><span class="sxs-lookup"><span data-stu-id="189e0-219">For example, if this value is set too250 AUs, you can have one job running with 250 AUs assigned tooit, or 10 jobs running with 25 AUs each.</span></span> <span data-ttu-id="189e0-220">Дополнительные задания, которые передаются помещаются в очередь завершения выполняющихся заданий hello.</span><span class="sxs-lookup"><span data-stu-id="189e0-220">Additional jobs that are submitted are queued until hello running jobs are finished.</span></span> <span data-ttu-id="189e0-221">После завершения выполняющихся заданий Сиднейское освобождаются для использования hello toorun заданий в очереди.</span><span class="sxs-lookup"><span data-stu-id="189e0-221">When running jobs are finished, AUs are freed up for hello queued jobs toorun.</span></span>

<span data-ttu-id="189e0-222">toochange hello число AUs для вашей учетной записи аналитики Озера данных:</span><span class="sxs-lookup"><span data-stu-id="189e0-222">toochange hello number of AUs for your Data Lake Analytics account:</span></span>

1. <span data-ttu-id="189e0-223">В hello портал Azure выберите учетную запись аналитики Озера данных tooyour.</span><span class="sxs-lookup"><span data-stu-id="189e0-223">In hello Azure portal, go tooyour Data Lake Analytics account.</span></span>
2. <span data-ttu-id="189e0-224">Щелкните **Свойства**.</span><span class="sxs-lookup"><span data-stu-id="189e0-224">Click **Properties**.</span></span>
3. <span data-ttu-id="189e0-225">В разделе **максимальное Сиднейское**, переместите ползунок hello tooselect значение или введите значение hello в текстовом поле hello.</span><span class="sxs-lookup"><span data-stu-id="189e0-225">Under **Maximum AUs**, move hello slider tooselect a value, or enter hello value in hello text box.</span></span> 
4. <span data-ttu-id="189e0-226">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="189e0-226">Click **Save**.</span></span>

> [!NOTE]
> <span data-ttu-id="189e0-227">Если вам требуется больше, чем hello по умолчанию (250) Сиднейское, hello портале щелкните **Справка + поддержка** toosubmit запрос на техническую поддержку.</span><span class="sxs-lookup"><span data-stu-id="189e0-227">If you need more than hello default (250) AUs, in hello portal, click **Help+Support** toosubmit a support request.</span></span> <span data-ttu-id="189e0-228">можно увеличить количество Hello Сиднейское, доступные в вашей учетной записи аналитики Озера данных.</span><span class="sxs-lookup"><span data-stu-id="189e0-228">hello number of AUs available in your Data Lake Analytics account can be increased.</span></span>
>

#### <a name="maximum-number-of-jobs-that-can-run-simultaneously"></a><span data-ttu-id="189e0-229">Максимальное количество одновременно выполняемых заданий</span><span class="sxs-lookup"><span data-stu-id="189e0-229">Maximum number of jobs that can run simultaneously</span></span>
<span data-ttu-id="189e0-230">Политики определяет, сколько могут выполняться в hello то же время.</span><span class="sxs-lookup"><span data-stu-id="189e0-230">A policy controls how many jobs can run at hello same time.</span></span> <span data-ttu-id="189e0-231">По умолчанию это значение имеет значение too20.</span><span class="sxs-lookup"><span data-stu-id="189e0-231">By default, this value is set too20.</span></span> <span data-ttu-id="189e0-232">Если аналитики Озера данных Сиднейское доступны, новые задания, запланированные toorun немедленно в том случае, пока не достигнет hello общего количества выполняемых заданий hello значение этой политики.</span><span class="sxs-lookup"><span data-stu-id="189e0-232">If your Data Lake Analytics has AUs available, new jobs are scheduled toorun immediately until hello total number of running jobs reaches hello value of this policy.</span></span> <span data-ttu-id="189e0-233">По достижении hello максимальное количество одновременно выполняемых заданий, последующие задания помещаются в очередь в порядке приоритета, пока не выполнено одно или несколько запущенных заданий (в зависимости от доступности Австралия).</span><span class="sxs-lookup"><span data-stu-id="189e0-233">When you reach hello maximum number of jobs that can run simultaneously, subsequent jobs are queued in priority order until one or more running jobs complete (depending on AU availability).</span></span>

<span data-ttu-id="189e0-234">toochange число hello одновременно выполняемых заданий:</span><span class="sxs-lookup"><span data-stu-id="189e0-234">toochange hello number of jobs that can run simultaneously:</span></span>

1. <span data-ttu-id="189e0-235">В hello портал Azure выберите учетную запись аналитики Озера данных tooyour.</span><span class="sxs-lookup"><span data-stu-id="189e0-235">In hello Azure portal, go tooyour Data Lake Analytics account.</span></span>
2. <span data-ttu-id="189e0-236">Щелкните **Свойства**.</span><span class="sxs-lookup"><span data-stu-id="189e0-236">Click **Properties**.</span></span>
3. <span data-ttu-id="189e0-237">В разделе **максимальное число выполнение задания**, переместите ползунок hello tooselect значение или введите значение hello в текстовом поле hello.</span><span class="sxs-lookup"><span data-stu-id="189e0-237">Under **Maximum Number of Running Jobs**, move hello slider tooselect a value, or enter hello value in hello text box.</span></span> 
4. <span data-ttu-id="189e0-238">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="189e0-238">Click **Save**.</span></span>

> [!NOTE]
> <span data-ttu-id="189e0-239">Если вам требуется более чем hello по умолчанию (20) количество заданий, hello портала щелкните toorun **Справка + поддержка** toosubmit запрос на техническую поддержку.</span><span class="sxs-lookup"><span data-stu-id="189e0-239">If you need toorun more than hello default (20) number of jobs, in hello portal, click **Help+Support** toosubmit a support request.</span></span> <span data-ttu-id="189e0-240">можно увеличить Hello количество заданий, которые могут выполняться одновременно в вашей учетной записи аналитики Озера данных.</span><span class="sxs-lookup"><span data-stu-id="189e0-240">hello number of jobs that can run simultaneously in your Data Lake Analytics account can be increased.</span></span>
>

#### <a name="how-long-tookeep-job-metadata-and-resources"></a><span data-ttu-id="189e0-241">Как долго tookeep задания метаданных и ресурсы</span><span class="sxs-lookup"><span data-stu-id="189e0-241">How long tookeep job metadata and resources</span></span> 
<span data-ttu-id="189e0-242">При запуске задания U-SQL пользователей hello Служба аналитики Озера данных сохраняет все связанные файлы.</span><span class="sxs-lookup"><span data-stu-id="189e0-242">When your users run U-SQL jobs, hello Data Lake Analytics service retains all related files.</span></span> <span data-ttu-id="189e0-243">Связанные файлы содержат сценарий hello U-SQL, на которые ссылается скрипт U-SQL hello, скомпилированных ресурсах и статистику hello DLL-файлы.</span><span class="sxs-lookup"><span data-stu-id="189e0-243">Related files include hello U-SQL script, hello DLL files referenced in hello U-SQL script, compiled resources, and statistics.</span></span> <span data-ttu-id="189e0-244">Hello файлы находятся в папке /system/ hello учетной записи хранилища Озера данных Azure по умолчанию hello.</span><span class="sxs-lookup"><span data-stu-id="189e0-244">hello files are in hello /system/ folder of hello default Azure Data Lake Storage account.</span></span> <span data-ttu-id="189e0-245">Эта политика определяет, как долго хранятся эти ресурсы, прежде чем они будут удалены автоматически (по умолчанию hello — 30 дней).</span><span class="sxs-lookup"><span data-stu-id="189e0-245">This policy controls how long these resources are stored before they are automatically deleted (hello default is 30 days).</span></span> <span data-ttu-id="189e0-246">Эти файлы можно использовать для отладки, а также для настройки производительности заданий, которые будут повторно в будущем hello.</span><span class="sxs-lookup"><span data-stu-id="189e0-246">You can use these files for debugging, and for performance-tuning of jobs that you'll rerun in hello future.</span></span>

<span data-ttu-id="189e0-247">toochange продолжительность метаданные задания tookeep и ресурсы:</span><span class="sxs-lookup"><span data-stu-id="189e0-247">toochange how long tookeep job metadata and resources:</span></span>

1. <span data-ttu-id="189e0-248">В hello портал Azure выберите учетную запись аналитики Озера данных tooyour.</span><span class="sxs-lookup"><span data-stu-id="189e0-248">In hello Azure portal, go tooyour Data Lake Analytics account.</span></span>
2. <span data-ttu-id="189e0-249">Щелкните **Свойства**.</span><span class="sxs-lookup"><span data-stu-id="189e0-249">Click **Properties**.</span></span>
3. <span data-ttu-id="189e0-250">В разделе **tooRetain дней задания запросов**, переместите ползунок hello tooselect значение или введите значение hello в текстовом поле hello.</span><span class="sxs-lookup"><span data-stu-id="189e0-250">Under **Days tooRetain Job Queries**, move hello slider tooselect a value, or enter hello value in hello text box.</span></span>  
4. <span data-ttu-id="189e0-251">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="189e0-251">Click **Save**.</span></span>

### <a name="job-level-policies"></a><span data-ttu-id="189e0-252">Политики на уровне задания</span><span class="sxs-lookup"><span data-stu-id="189e0-252">Job-level policies</span></span>
<span data-ttu-id="189e0-253">С помощью политик на уровне задания, можно управлять hello максимальное Сиднейское и hello максимальный приоритет, отдельных пользователей (или участники групп безопасности) можно задать на задания, которые они отправляют.</span><span class="sxs-lookup"><span data-stu-id="189e0-253">With job-level policies, you can control hello maximum AUs and hello maximum priority that individual users (or members of specific security groups) can set on jobs that they submit.</span></span> <span data-ttu-id="189e0-254">Это позволяет контролировать затраты hello пользователями.</span><span class="sxs-lookup"><span data-stu-id="189e0-254">This lets you control hello costs incurred by users.</span></span> <span data-ttu-id="189e0-255">Он также позволяет эффект управления hello, запланированные задания должен обладать высоким приоритетом производственных заданий, выполняющихся в hello учетную запись аналитики Озера данных.</span><span class="sxs-lookup"><span data-stu-id="189e0-255">It also lets you control hello effect that scheduled jobs might have on high-priority production jobs that are running in hello same Data Lake Analytics account.</span></span>

<span data-ttu-id="189e0-256">Аналитика Озера данных имеет две политики, которые могут быть установлены на уровне задания hello.</span><span class="sxs-lookup"><span data-stu-id="189e0-256">Data Lake Analytics has two policies that you can set at hello job level:</span></span>

* <span data-ttu-id="189e0-257">**Ограничение Австралия задания**: пользователи могут только отправлять задания, имеющие toothis число Сиднейское вверх.</span><span class="sxs-lookup"><span data-stu-id="189e0-257">**AU limit per job**: Users can only submit jobs that have up toothis number of AUs.</span></span> <span data-ttu-id="189e0-258">По умолчанию это ограничение является hello аналогично hello Австралия максимальное значение для учетной записи hello.</span><span class="sxs-lookup"><span data-stu-id="189e0-258">By default, this limit is hello same as hello maximum AU limit for hello account.</span></span>
* <span data-ttu-id="189e0-259">**Приоритет**: пользователи могут только отправлять задания, которые имеют значение меньше или равна toothis приоритета.</span><span class="sxs-lookup"><span data-stu-id="189e0-259">**Priority**: Users can only submit jobs that have a priority lower than or equal toothis value.</span></span> <span data-ttu-id="189e0-260">Обратите внимание, что большее значение означает более низкий приоритет.</span><span class="sxs-lookup"><span data-stu-id="189e0-260">Note that a higher number means a lower priority.</span></span> <span data-ttu-id="189e0-261">По умолчанию это устанавливается too1, что является максимально возможный приоритет hello.</span><span class="sxs-lookup"><span data-stu-id="189e0-261">By default, this is set too1, which is hello highest possible priority.</span></span>

<span data-ttu-id="189e0-262">Для каждой учетной записи назначается политика по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="189e0-262">There is a default policy set on every account.</span></span> <span data-ttu-id="189e0-263">Политика по умолчанию Hello применяется пользователей tooall hello учетной записи.</span><span class="sxs-lookup"><span data-stu-id="189e0-263">hello default policy applies tooall users of hello account.</span></span> <span data-ttu-id="189e0-264">Можно установить дополнительные политики для отдельных пользователей и групп.</span><span class="sxs-lookup"><span data-stu-id="189e0-264">You can set additional policies for specific users and groups.</span></span> 

> [!NOTE]
> <span data-ttu-id="189e0-265">Политики на уровне учетной записи и политики на уровне задания применяются одновременно.</span><span class="sxs-lookup"><span data-stu-id="189e0-265">Account-level policies and job-level policies apply simultaneously.</span></span>
>

#### <a name="add-a-policy-for-a-specific-user-or-group"></a><span data-ttu-id="189e0-266">Добавление политики для конкретного пользователя или группы</span><span class="sxs-lookup"><span data-stu-id="189e0-266">Add a policy for a specific user or group</span></span>

1. <span data-ttu-id="189e0-267">В hello портал Azure выберите учетную запись аналитики Озера данных tooyour.</span><span class="sxs-lookup"><span data-stu-id="189e0-267">In hello Azure portal, go tooyour Data Lake Analytics account.</span></span>
2. <span data-ttu-id="189e0-268">Щелкните **Свойства**.</span><span class="sxs-lookup"><span data-stu-id="189e0-268">Click **Properties**.</span></span>
3. <span data-ttu-id="189e0-269">В разделе **предел отправки заданий**, нажмите кнопку hello **добавить политику** кнопки.</span><span class="sxs-lookup"><span data-stu-id="189e0-269">Under **Job Submission Limits**, click hello **Add Policy** button.</span></span> <span data-ttu-id="189e0-270">Затем выберите или введите hello следующие параметры:</span><span class="sxs-lookup"><span data-stu-id="189e0-270">Then, select or enter hello following settings:</span></span>
    1. <span data-ttu-id="189e0-271">**Имя политики вычислений**: Введите имя политики, tooremind вы hello цель политики hello.</span><span class="sxs-lookup"><span data-stu-id="189e0-271">**Compute Policy Name**: Enter a policy name, tooremind you of hello purpose of hello policy.</span></span>
    2. <span data-ttu-id="189e0-272">**Выберите пользователя или группу**: Выбор приветствия пользователя или группы, эта политика применяется к.</span><span class="sxs-lookup"><span data-stu-id="189e0-272">**Select User or Group**: Select hello user or group this policy applies to.</span></span>
    3. <span data-ttu-id="189e0-273">**Задать ограничение Австралия hello**: установленного лимита hello Австралия, применяющий toohello выбранного пользователя или группы.</span><span class="sxs-lookup"><span data-stu-id="189e0-273">**Set hello Job AU Limit**: Set hello AU limit that applies toohello selected user or group.</span></span>
    4. <span data-ttu-id="189e0-274">**Задать ограничение приоритета hello**: установленного лимита hello приоритет применения toohello выбранного пользователя или группы.</span><span class="sxs-lookup"><span data-stu-id="189e0-274">**Set hello Priority Limit**: Set hello priority limit that applies toohello selected user or group.</span></span>

4. <span data-ttu-id="189e0-275">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="189e0-275">Click **Ok**.</span></span>

5. <span data-ttu-id="189e0-276">Hello новая политика отображается в hello **по умолчанию** политики таблицы в разделе **предел отправки заданий**.</span><span class="sxs-lookup"><span data-stu-id="189e0-276">hello new policy is listed in hello **Default** policy table, under **Job Submission Limits**.</span></span> 

#### <a name="delete-or-edit-an-existing-policy"></a><span data-ttu-id="189e0-277">Удаление или изменение существующей политики</span><span class="sxs-lookup"><span data-stu-id="189e0-277">Delete or edit an existing policy</span></span>

1. <span data-ttu-id="189e0-278">В hello портал Azure выберите учетную запись аналитики Озера данных tooyour.</span><span class="sxs-lookup"><span data-stu-id="189e0-278">In hello Azure portal, go tooyour Data Lake Analytics account.</span></span>
2. <span data-ttu-id="189e0-279">Щелкните **Свойства**.</span><span class="sxs-lookup"><span data-stu-id="189e0-279">Click **Properties**.</span></span>
3. <span data-ttu-id="189e0-280">В разделе **предел отправки заданий**, найти hello политику tooedit.</span><span class="sxs-lookup"><span data-stu-id="189e0-280">Under **Job Submission Limits**, find hello policy you want tooedit.</span></span>
4.  <span data-ttu-id="189e0-281">toosee hello **удаление** и **изменить** параметров в правом столбце hello hello таблицы, выберите пункт **...** .</span><span class="sxs-lookup"><span data-stu-id="189e0-281">toosee hello **Delete** and **Edit** options, in hello rightmost column of hello table, click **...**.</span></span>

### <a name="additional-resources-for-job-policies"></a><span data-ttu-id="189e0-282">Дополнительные ресурсы политики заданий</span><span class="sxs-lookup"><span data-stu-id="189e0-282">Additional resources for job policies</span></span>
* [<span data-ttu-id="189e0-283">Запись блога с обзором политик</span><span class="sxs-lookup"><span data-stu-id="189e0-283">Policy overview blog post</span></span>](https://blogs.msdn.microsoft.com/azuredatalake/2017/06/08/managing-your-azure-data-lake-analytics-compute-resources-overview/)
* [<span data-ttu-id="189e0-284">Запись блога о политиках на уровне учетной записи</span><span class="sxs-lookup"><span data-stu-id="189e0-284">Account-level policies blog post</span></span>](https://blogs.msdn.microsoft.com/azuredatalake/2017/06/08/managing-your-azure-data-lake-analytics-compute-resources-account-level-policy/)
* [<span data-ttu-id="189e0-285">Запись блога о политиках на уровне задания</span><span class="sxs-lookup"><span data-stu-id="189e0-285">Job-level policies blog post</span></span>](https://blogs.msdn.microsoft.com/azuredatalake/2017/06/08/managing-your-azure-data-lake-analytics-compute-resources-job-level-policy/)

## <a name="next-steps"></a><span data-ttu-id="189e0-286">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="189e0-286">Next steps</span></span>

* [<span data-ttu-id="189e0-287">Обзор аналитики озера данных Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="189e0-287">Overview of Azure Data Lake Analytics</span></span>](data-lake-analytics-overview.md)
* [<span data-ttu-id="189e0-288">Начало работы с аналитики Озера данных с помощью портала Azure hello</span><span class="sxs-lookup"><span data-stu-id="189e0-288">Get started with Data Lake Analytics by using hello Azure portal</span></span>](data-lake-analytics-get-started-portal.md)
* [<span data-ttu-id="189e0-289">Управление Azure Data Lake Analytics с помощью Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="189e0-289">Manage Azure Data Lake Analytics by using Azure PowerShell</span></span>](data-lake-analytics-manage-use-powershell.md)

