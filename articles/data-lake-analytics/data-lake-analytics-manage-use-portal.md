---
title: "Управление Azure Data Lake Analytics с помощью портала Azure | Документация Майкрософт"
description: "Узнайте, как управлять учетными записями аналитики озера данных, источниками данных, пользователями и заданиями."
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
ms.openlocfilehash: e49d1a0e0ccc6567d0a6841817667717ff5dba76
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="manage-azure-data-lake-analytics-by-using-the-azure-portal"></a><span data-ttu-id="4f3c8-103">Управление Azure Data Lake Analytics с помощью портала Azure</span><span class="sxs-lookup"><span data-stu-id="4f3c8-103">Manage Azure Data Lake Analytics by using the Azure portal</span></span>
[!INCLUDE [manage-selector](../../includes/data-lake-analytics-selector-manage.md)]

<span data-ttu-id="4f3c8-104">Узнайте, как управлять учетными записями, источниками данных учетной записи, пользователями и заданиями Azure Data Lake Analytics с помощью портала Azure.</span><span class="sxs-lookup"><span data-stu-id="4f3c8-104">Learn how to manage Azure Data Lake Analytics accounts, account data sources, users, and jobs by using the Azure portal.</span></span> <span data-ttu-id="4f3c8-105">Для просмотра разделов, посвященных управлению с помощью других инструментов, воспользуйтесь вкладкой вверху страницы.</span><span class="sxs-lookup"><span data-stu-id="4f3c8-105">To see management topics about using other tools, click a tab at the top of the page.</span></span>

<!-- ################################ -->
<!-- ################################ -->

## <a name="manage-data-lake-analytics-accounts"></a><span data-ttu-id="4f3c8-106">Управление учетными записями Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="4f3c8-106">Manage Data Lake Analytics accounts</span></span>

### <a name="create-an-account"></a><span data-ttu-id="4f3c8-107">Создание учетной записи</span><span class="sxs-lookup"><span data-stu-id="4f3c8-107">Create an account</span></span>

1. <span data-ttu-id="4f3c8-108">Войдите на [портал Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="4f3c8-108">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="4f3c8-109">Щелкните **Создать** > **Аналитика** > **Data Lake Analytics**.</span><span class="sxs-lookup"><span data-stu-id="4f3c8-109">Click **New** > **Intelligence + analytics** > **Data Lake Analytics**.</span></span>
3. <span data-ttu-id="4f3c8-110">Выберите значения для следующих параметров:</span><span class="sxs-lookup"><span data-stu-id="4f3c8-110">Select values for the following items:</span></span> 
   1. <span data-ttu-id="4f3c8-111">**Имя**: имя учетной записи Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="4f3c8-111">**Name**: The name of the Data Lake Analytics account.</span></span>
   2. <span data-ttu-id="4f3c8-112">**Подписка**: подписка Azure, которая используется для учетной записи.</span><span class="sxs-lookup"><span data-stu-id="4f3c8-112">**Subscription**: The Azure subscription used for the account.</span></span>
   3. <span data-ttu-id="4f3c8-113">**Группа ресурсов**: группа ресурсов Azure, в которой создается учетная запись.</span><span class="sxs-lookup"><span data-stu-id="4f3c8-113">**Resource Group**: The Azure resource group in which to create the account.</span></span> 
   4. <span data-ttu-id="4f3c8-114">**Расположение**: центр обработки данных Azure для учетной записи Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="4f3c8-114">**Location**: The Azure datacenter for the Data Lake Analytics account.</span></span> 
   5. <span data-ttu-id="4f3c8-115">**Data Lake Store**: хранилище по умолчанию для учетной записи Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="4f3c8-115">**Data Lake Store**: The default store to be used for the Data Lake Analytics account.</span></span> <span data-ttu-id="4f3c8-116">Учетная запись Azure Data Lake Store и учетная запись Data Lake Analytics должны находиться в одном расположении.</span><span class="sxs-lookup"><span data-stu-id="4f3c8-116">The Azure Data Lake Store account and the Data Lake Analytics account must be in the same location.</span></span>
4. <span data-ttu-id="4f3c8-117">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="4f3c8-117">Click **Create**.</span></span> 

### <a name="delete-a-data-lake-analytics-account"></a><span data-ttu-id="4f3c8-118">Удаление учетной записи Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="4f3c8-118">Delete a Data Lake Analytics account</span></span>

<span data-ttu-id="4f3c8-119">Перед удалением учетной записи Data Lake Analytics необходимо удалить учетную запись Data Lake Store по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="4f3c8-119">Before you delete a Data Lake Analytics account, delete its default Data Lake Store account.</span></span>

1. <span data-ttu-id="4f3c8-120">На портале Azure выберите свою учетную запись Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="4f3c8-120">In the Azure portal, go to your Data Lake Analytics account.</span></span>
2. <span data-ttu-id="4f3c8-121">Нажмите кнопку **Delete**(Удалить).</span><span class="sxs-lookup"><span data-stu-id="4f3c8-121">Click **Delete**.</span></span>
3. <span data-ttu-id="4f3c8-122">Введите имя учетной записи.</span><span class="sxs-lookup"><span data-stu-id="4f3c8-122">Type the account name.</span></span>
4. <span data-ttu-id="4f3c8-123">Нажмите кнопку **Delete**(Удалить).</span><span class="sxs-lookup"><span data-stu-id="4f3c8-123">Click **Delete**.</span></span>

<!-- ################################ -->
<!-- ################################ -->

## <a name="manage-data-sources"></a><span data-ttu-id="4f3c8-124">Управление источниками данных</span><span class="sxs-lookup"><span data-stu-id="4f3c8-124">Manage data sources</span></span>

<span data-ttu-id="4f3c8-125">Data Lake Analytics в настоящее время поддерживает следующие источники данных:</span><span class="sxs-lookup"><span data-stu-id="4f3c8-125">Data Lake Analytics supports the following data sources:</span></span>

* <span data-ttu-id="4f3c8-126">Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="4f3c8-126">Data Lake Store</span></span>
* <span data-ttu-id="4f3c8-127">Хранилище Azure</span><span class="sxs-lookup"><span data-stu-id="4f3c8-127">Azure Storage</span></span>

<span data-ttu-id="4f3c8-128">Вы можете использовать обозреватель данных для просмотра источников данных и выполнения основных операций управления файлами.</span><span class="sxs-lookup"><span data-stu-id="4f3c8-128">You can use Data Explorer to browse data sources and perform basic file management operations.</span></span> 

### <a name="add-a-data-source"></a><span data-ttu-id="4f3c8-129">Добавление источника данных</span><span class="sxs-lookup"><span data-stu-id="4f3c8-129">Add a data source</span></span>

1. <span data-ttu-id="4f3c8-130">На портале Azure выберите свою учетную запись Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="4f3c8-130">In the Azure portal, go to your Data Lake Analytics account.</span></span>
2. <span data-ttu-id="4f3c8-131">Щелкните **Источники данных**.</span><span class="sxs-lookup"><span data-stu-id="4f3c8-131">Click **Data Sources**.</span></span>
3. <span data-ttu-id="4f3c8-132">Щелкните **Добавить источник данных**.</span><span class="sxs-lookup"><span data-stu-id="4f3c8-132">Click **Add Data Source**.</span></span>
    
   * <span data-ttu-id="4f3c8-133">Чтобы добавить учетную запись Data Lake Store, требуется имя учетной записи и доступ к учетной записи, чтобы отправить ей запрос.</span><span class="sxs-lookup"><span data-stu-id="4f3c8-133">To add a Data Lake Store account, you need the account name and access to the account to be able to query it.</span></span>
   * <span data-ttu-id="4f3c8-134">Чтобы добавить хранилище BLOB-объектов Azure, требуется учетная запись хранения и ключ учетной записи.</span><span class="sxs-lookup"><span data-stu-id="4f3c8-134">To add Azure Blob storage, you need the storage account and the account key.</span></span> <span data-ttu-id="4f3c8-135">Чтобы найти их, перейдите к учетной записи хранения на портале.</span><span class="sxs-lookup"><span data-stu-id="4f3c8-135">To find them, go to the storage account in the portal.</span></span>

## <a name="set-up-firewall-rules"></a><span data-ttu-id="4f3c8-136">Настройка правил брандмауэра</span><span class="sxs-lookup"><span data-stu-id="4f3c8-136">Set up firewall rules</span></span>

<span data-ttu-id="4f3c8-137">Data Lake Analytics позволяет дополнительно блокировать доступ к учетной записи Data Lake Analytics на уровне сети.</span><span class="sxs-lookup"><span data-stu-id="4f3c8-137">You can use Data Lake Analytics to further lock down access to your Data Lake Analytics account at the network level.</span></span> <span data-ttu-id="4f3c8-138">Вы можете включить брандмауэр, указать IP-адрес или определить диапазон IP-адресов для доверенных клиентов.</span><span class="sxs-lookup"><span data-stu-id="4f3c8-138">You can enable a firewall, specify an IP address, or define an IP address range for your trusted clients.</span></span> <span data-ttu-id="4f3c8-139">После этого к хранилищу смогут подключаться только клиенты с IP-адресами из определенного диапазона.</span><span class="sxs-lookup"><span data-stu-id="4f3c8-139">After you enable these measures, only clients that have the IP addresses within the defined range can connect to the store.</span></span>

<span data-ttu-id="4f3c8-140">Если другие службы Azure, например Azure Data Factory или виртуальные машины, будут подключаться к учетной записи Data Lake Analytics, убедитесь, что для параметра **Разрешить использование служб Azure** установлено значение **Вкл**.</span><span class="sxs-lookup"><span data-stu-id="4f3c8-140">If other Azure services, like Azure Data Factory or VMs, connect to the Data Lake Analytics account, make sure that **Allow Azure Services** is turned **On**.</span></span> 

### <a name="set-up-a-firewall-rule"></a><span data-ttu-id="4f3c8-141">Настройка правила брандмауэра.</span><span class="sxs-lookup"><span data-stu-id="4f3c8-141">Set up a firewall rule</span></span>

1. <span data-ttu-id="4f3c8-142">На портале Azure выберите свою учетную запись Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="4f3c8-142">In the Azure portal, go to your Data Lake Analytics account.</span></span>
2. <span data-ttu-id="4f3c8-143">В меню слева щелкните **Брандмауэр**.</span><span class="sxs-lookup"><span data-stu-id="4f3c8-143">On the menu on the left, click **Firewall**.</span></span>

## <a name="add-a-new-user"></a><span data-ttu-id="4f3c8-144">Добавление нового пользователя</span><span class="sxs-lookup"><span data-stu-id="4f3c8-144">Add a new user</span></span>

<span data-ttu-id="4f3c8-145">Чтобы быстро подготовить новых пользователей Data Lake, используйте **мастер добавления пользователей**.</span><span class="sxs-lookup"><span data-stu-id="4f3c8-145">You can use the **Add User Wizard** to easily provision new Data Lake users.</span></span>

1. <span data-ttu-id="4f3c8-146">На портале Azure выберите свою учетную запись Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="4f3c8-146">In the Azure portal, go to your Data Lake Analytics account.</span></span>
2. <span data-ttu-id="4f3c8-147">В левой части экрана в разделе **Приступая к работе** щелкните **Мастер добавления пользователей**.</span><span class="sxs-lookup"><span data-stu-id="4f3c8-147">On the left, under **Getting Started**, click **Add User Wizard**.</span></span>
3. <span data-ttu-id="4f3c8-148">Выберите пользователя и нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="4f3c8-148">Select a user, and then click **Select**.</span></span>
4. <span data-ttu-id="4f3c8-149">Выберите роль и нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="4f3c8-149">Select a role, and then click **Select**.</span></span> <span data-ttu-id="4f3c8-150">Чтобы добавить нового разработчика в Azure Data Lake, выберите роль **Разработчик Data Lake Analytics**.</span><span class="sxs-lookup"><span data-stu-id="4f3c8-150">To set up a new developer to use Azure Data Lake, select the **Data Lake Analytics Developer** role.</span></span>
5. <span data-ttu-id="4f3c8-151">Выберите списки управления доступом для баз данных U-SQL.</span><span class="sxs-lookup"><span data-stu-id="4f3c8-151">Select the access control lists (ACLs) for the U-SQL databases.</span></span> <span data-ttu-id="4f3c8-152">Когда нужные параметры настроены, нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="4f3c8-152">When you're satisfied with your choices, click **Select**.</span></span>
6. <span data-ttu-id="4f3c8-153">Выберите списки управления доступом для файлов.</span><span class="sxs-lookup"><span data-stu-id="4f3c8-153">Select the ACLs for files.</span></span> <span data-ttu-id="4f3c8-154">Чтобы использовать хранилище по умолчанию, не изменяйте списки управления доступом для корневой папки "/" и для папки /system.</span><span class="sxs-lookup"><span data-stu-id="4f3c8-154">For the default store, don't change the ACLs for the root folder "/" and for the /system folder.</span></span> <span data-ttu-id="4f3c8-155">Нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="4f3c8-155">Click **Select**.</span></span>
7. <span data-ttu-id="4f3c8-156">Просмотрите выбранные изменения и нажмите кнопку **Выполнить**.</span><span class="sxs-lookup"><span data-stu-id="4f3c8-156">Review all your selected changes, and then click **Run**.</span></span>
8. <span data-ttu-id="4f3c8-157">После завершения работы мастера нажмите кнопку **Готово**.</span><span class="sxs-lookup"><span data-stu-id="4f3c8-157">When the wizard is finished, click **Done**.</span></span>

## <a name="manage-role-based-access-control"></a><span data-ttu-id="4f3c8-158">Управление доступом на основе ролей</span><span class="sxs-lookup"><span data-stu-id="4f3c8-158">Manage Role-Based Access Control</span></span>

<span data-ttu-id="4f3c8-159">Подобно другим службам Azure, можно использовать управление доступом на основе ролей (RBAC), чтобы управлять взаимодействием пользователей со службой.</span><span class="sxs-lookup"><span data-stu-id="4f3c8-159">Like other Azure services, you can use Role-Based Access Control (RBAC) to control how users interact with the service.</span></span>

<span data-ttu-id="4f3c8-160">Стандартные роли RBAC имеют следующие возможности:</span><span class="sxs-lookup"><span data-stu-id="4f3c8-160">The standard RBAC roles have the following capabilities:</span></span>
* <span data-ttu-id="4f3c8-161">**Владелец**: может отправлять и отслеживать задания, отменять задания от любого пользователя, а также настраивать учетные записи.</span><span class="sxs-lookup"><span data-stu-id="4f3c8-161">**Owner**: Can submit jobs, monitor jobs, cancel jobs from any user, and configure the account.</span></span>
* <span data-ttu-id="4f3c8-162">**Участник**: может отправлять и отслеживать задания, отменять задания для любого пользователя, а также настраивать учетные записи.</span><span class="sxs-lookup"><span data-stu-id="4f3c8-162">**Contributor**: Can submit jobs, monitor jobs, cancel jobs from any user, and configure the account.</span></span>
* <span data-ttu-id="4f3c8-163">**Читатель**: может отслеживать задания.</span><span class="sxs-lookup"><span data-stu-id="4f3c8-163">**Reader**: Can monitor jobs.</span></span>

<span data-ttu-id="4f3c8-164">Чтобы предоставить разработчикам доступ к U-SQL для использования службы Data Lake Analytics, используйте роль "Разработчик Data Lake Analytics".</span><span class="sxs-lookup"><span data-stu-id="4f3c8-164">Use the Data Lake Analytics Developer role to enable U-SQL developers to use the Data Lake Analytics service.</span></span> <span data-ttu-id="4f3c8-165">Роль "Разработчик Data Lake Analytics" можно использовать для:</span><span class="sxs-lookup"><span data-stu-id="4f3c8-165">You can use the Data Lake Analytics Developer role to:</span></span>
* <span data-ttu-id="4f3c8-166">отправки заданий;</span><span class="sxs-lookup"><span data-stu-id="4f3c8-166">Submit jobs.</span></span>
* <span data-ttu-id="4f3c8-167">отслеживания состояния и хода выполнения отправленных пользователями заданий;</span><span class="sxs-lookup"><span data-stu-id="4f3c8-167">Monitor job status and the progress of jobs submitted by any user.</span></span>
* <span data-ttu-id="4f3c8-168">просмотра скриптов U-SQL в отправленных пользователями заданиях;</span><span class="sxs-lookup"><span data-stu-id="4f3c8-168">See the U-SQL scripts from jobs submitted by any user.</span></span>
* <span data-ttu-id="4f3c8-169">отмены собственных заданий.</span><span class="sxs-lookup"><span data-stu-id="4f3c8-169">Cancel only your own jobs.</span></span>

### <a name="add-users-or-security-groups-to-a-data-lake-analytics-account"></a><span data-ttu-id="4f3c8-170">Добавление пользователей или групп безопасности к учетной записи Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="4f3c8-170">Add users or security groups to a Data Lake Analytics account</span></span>

1. <span data-ttu-id="4f3c8-171">На портале Azure выберите свою учетную запись Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="4f3c8-171">In the Azure portal, go to your Data Lake Analytics account.</span></span>
2. <span data-ttu-id="4f3c8-172">Щелкните **Управление доступом (IAM)** > **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="4f3c8-172">Click **Access control (IAM)** > **Add**.</span></span>
3. <span data-ttu-id="4f3c8-173">Выберите роль.</span><span class="sxs-lookup"><span data-stu-id="4f3c8-173">Select a role.</span></span>
4. <span data-ttu-id="4f3c8-174">Добавьте пользователя.</span><span class="sxs-lookup"><span data-stu-id="4f3c8-174">Add a user.</span></span>
5. <span data-ttu-id="4f3c8-175">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="4f3c8-175">Click **OK**.</span></span>

>[!NOTE]
><span data-ttu-id="4f3c8-176">Если пользователю или группе безопасности требуется отправлять задания, они также должны иметь разрешение в учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="4f3c8-176">If a user or a security group needs to submit jobs, they also need permission on the store account.</span></span> <span data-ttu-id="4f3c8-177">Дополнительные сведения см. в статье [Защита данных, хранимых в Azure Data Lake Store](../data-lake-store/data-lake-store-secure-data.md).</span><span class="sxs-lookup"><span data-stu-id="4f3c8-177">For more information, see [Secure data stored in Data Lake Store](../data-lake-store/data-lake-store-secure-data.md).</span></span>
>

<!-- ################################ -->
<!-- ################################ -->

## <a name="manage-jobs"></a><span data-ttu-id="4f3c8-178">Управление заданиями</span><span class="sxs-lookup"><span data-stu-id="4f3c8-178">Manage jobs</span></span>

### <a name="submit-a-job"></a><span data-ttu-id="4f3c8-179">Отправка задания</span><span class="sxs-lookup"><span data-stu-id="4f3c8-179">Submit a job</span></span>

1. <span data-ttu-id="4f3c8-180">На портале Azure выберите свою учетную запись Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="4f3c8-180">In the Azure portal, go to your Data Lake Analytics account.</span></span>

2. <span data-ttu-id="4f3c8-181">Нажмите кнопку **Создать задание**.</span><span class="sxs-lookup"><span data-stu-id="4f3c8-181">Click **New Job**.</span></span> <span data-ttu-id="4f3c8-182">Настройте для каждого задания:</span><span class="sxs-lookup"><span data-stu-id="4f3c8-182">For each job,  configure:</span></span>

    1. <span data-ttu-id="4f3c8-183">**Имя задания**: имя задания.</span><span class="sxs-lookup"><span data-stu-id="4f3c8-183">**Job Name**: The name of the job.</span></span>
    2. <span data-ttu-id="4f3c8-184">**Приоритет**: чем меньше число, тем выше приоритет.</span><span class="sxs-lookup"><span data-stu-id="4f3c8-184">**Priority**: Lower numbers have higher priority.</span></span> <span data-ttu-id="4f3c8-185">Если два задания поставлены в очередь, первым выполняется задание с более низким приоритетом.</span><span class="sxs-lookup"><span data-stu-id="4f3c8-185">If two jobs are queued, the one with lower priority value runs first.</span></span>
    3. <span data-ttu-id="4f3c8-186">**Параллелизм**: максимальное число вычислительных процессов, зарезервированных для этого задания.</span><span class="sxs-lookup"><span data-stu-id="4f3c8-186">**Parallelism**: The maximum number of compute processes to reserve for this job.</span></span>

3. <span data-ttu-id="4f3c8-187">Щелкните **Отправить задание**.</span><span class="sxs-lookup"><span data-stu-id="4f3c8-187">Click **Submit Job**.</span></span>

### <a name="monitor-jobs"></a><span data-ttu-id="4f3c8-188">Мониторинг заданий</span><span class="sxs-lookup"><span data-stu-id="4f3c8-188">Monitor jobs</span></span>

1. <span data-ttu-id="4f3c8-189">На портале Azure выберите свою учетную запись Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="4f3c8-189">In the Azure portal, go to your Data Lake Analytics account.</span></span>
2. <span data-ttu-id="4f3c8-190">Щелкните **Просмотр всех заданий**.</span><span class="sxs-lookup"><span data-stu-id="4f3c8-190">Click **View All Jobs**.</span></span> <span data-ttu-id="4f3c8-191">Отобразится список всех активных и недавно завершенных заданий в учетной записи.</span><span class="sxs-lookup"><span data-stu-id="4f3c8-191">A list of all the active and recently finished jobs in the account is shown.</span></span>
3. <span data-ttu-id="4f3c8-192">При необходимости щелкните **Фильтр** для поиска заданий по значениям **Диапазон времени**, **Имя задания** и **Автор**.</span><span class="sxs-lookup"><span data-stu-id="4f3c8-192">Optionally, click **Filter** to help you find the jobs by **Time Range**, **Job Name**, and **Author** values.</span></span> 

### <a name="monitoring-pipeline-jobs"></a><span data-ttu-id="4f3c8-193">Отслеживание заданий конвейера</span><span class="sxs-lookup"><span data-stu-id="4f3c8-193">Monitoring pipeline jobs</span></span>
<span data-ttu-id="4f3c8-194">Задания конвейера определенного сценария выполнятся совместно в последовательном порядке.</span><span class="sxs-lookup"><span data-stu-id="4f3c8-194">Jobs that are part of a pipeline work together, usually sequentially, to accomplish a specific scenario.</span></span> <span data-ttu-id="4f3c8-195">Например, вы можете иметь конвейер, который очищает, извлекает, преобразует и содержит статистические данные, используемые при работе с клиентами.</span><span class="sxs-lookup"><span data-stu-id="4f3c8-195">For example, you can have a pipeline that cleans, extracts, transforms, aggregates usage for customer insights.</span></span> <span data-ttu-id="4f3c8-196">Задания конвейера определяются с помощью свойства Pipeline при отправке задания.</span><span class="sxs-lookup"><span data-stu-id="4f3c8-196">Pipeline jobs are identified using the "Pipeline" property when the job was submitted.</span></span> <span data-ttu-id="4f3c8-197">В заданиях, запланированных с помощью ADF V2, эти свойства заполняются автоматически.</span><span class="sxs-lookup"><span data-stu-id="4f3c8-197">Jobs scheduled using ADF V2 will automatically have this property populated.</span></span> 

<span data-ttu-id="4f3c8-198">Чтобы просмотреть список заданий U-SQL конвейера, сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="4f3c8-198">To view a list of U-SQL jobs that are part of pipelines:</span></span> 

1. <span data-ttu-id="4f3c8-199">На портале Azure перейдите к своим учетным записям Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="4f3c8-199">In the Azure portal, go to your Data Lake Analytics accounts.</span></span>
2. <span data-ttu-id="4f3c8-200">Выберите **Подробные сведения о заданиях**.</span><span class="sxs-lookup"><span data-stu-id="4f3c8-200">Click **Job Insights**.</span></span> <span data-ttu-id="4f3c8-201">По умолчанию на вкладке "Все задания" можно просмотреть список выполняющихся и завершенных заданий, а также заданий, поставленных в очередь.</span><span class="sxs-lookup"><span data-stu-id="4f3c8-201">The "All Jobs" tab will be defaulted, showing a list of running, queued, and ended jobs.</span></span>
3. <span data-ttu-id="4f3c8-202">Перейдите на вкладку **Задания конвейера**. Список заданий конвейера будет отображаться со сводными статистическими данными по каждому конвейеру.</span><span class="sxs-lookup"><span data-stu-id="4f3c8-202">Click the **Pipeline Jobs** tab. A list of pipeline jobs will be shown along with aggregated statistics for each pipeline.</span></span>

### <a name="monitoring-recurring-jobs"></a><span data-ttu-id="4f3c8-203">Отслеживание повторяющихся заданий</span><span class="sxs-lookup"><span data-stu-id="4f3c8-203">Monitoring recurring jobs</span></span>
<span data-ttu-id="4f3c8-204">Повторяющиеся задания — это задания, которые имеют одинаковую бизнес-логику, но используют разные входные данные при каждом запуске.</span><span class="sxs-lookup"><span data-stu-id="4f3c8-204">A recurring job is one that has the same business logic but uses different input data every time it runs.</span></span> <span data-ttu-id="4f3c8-205">В идеале повторяющиеся задания должны всегда выполняться успешно и иметь относительно стабильное время выполнения. Отслеживание этого поведения поможет обеспечить работоспособность задания.</span><span class="sxs-lookup"><span data-stu-id="4f3c8-205">Ideally, recurring jobs should always succeed, and have relatively stable execution time; monitoring these behaviors will help ensure the job is healthy.</span></span> <span data-ttu-id="4f3c8-206">Повторяющиеся задания определяются с помощью свойства Recurrence.</span><span class="sxs-lookup"><span data-stu-id="4f3c8-206">Recurring jobs are identified using the "Recurrence" property.</span></span> <span data-ttu-id="4f3c8-207">В заданиях, запланированных с помощью ADF V2, эти свойства заполняются автоматически.</span><span class="sxs-lookup"><span data-stu-id="4f3c8-207">Jobs scheduled using ADF V2 will automatically have this property populated.</span></span>

<span data-ttu-id="4f3c8-208">Чтобы просмотреть список повторяющихся заданий U-SQL, сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="4f3c8-208">To view a list of U-SQL jobs that are recurring:</span></span> 

1. <span data-ttu-id="4f3c8-209">На портале Azure перейдите к своим учетным записям Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="4f3c8-209">In the Azure portal, go to your Data Lake Analytics accounts.</span></span>
2. <span data-ttu-id="4f3c8-210">Выберите **Подробные сведения о заданиях**.</span><span class="sxs-lookup"><span data-stu-id="4f3c8-210">Click **Job Insights**.</span></span> <span data-ttu-id="4f3c8-211">По умолчанию на вкладке "Все задания" можно просмотреть список выполняющихся и завершенных заданий, а также заданий, поставленных в очередь.</span><span class="sxs-lookup"><span data-stu-id="4f3c8-211">The "All Jobs" tab will be defaulted, showing a list of running, queued, and ended jobs.</span></span>
3. <span data-ttu-id="4f3c8-212">Откройте вкладку **Повторяющиеся задания**. Список повторяющихся заданий будет отображаться со сводными статистическими данными по повторяющемуся заданию.</span><span class="sxs-lookup"><span data-stu-id="4f3c8-212">Click the **Recurring Jobs** tab. A list of recurring jobs will be shown along with aggregated statistics for each recurring job.</span></span>

## <a name="manage-policies"></a><span data-ttu-id="4f3c8-213">Управление политиками</span><span class="sxs-lookup"><span data-stu-id="4f3c8-213">Manage policies</span></span>

### <a name="account-level-policies"></a><span data-ttu-id="4f3c8-214">Политики на уровне учетной записи</span><span class="sxs-lookup"><span data-stu-id="4f3c8-214">Account-level policies</span></span>

<span data-ttu-id="4f3c8-215">Эти политики применяются для всех заданий в учетной записи Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="4f3c8-215">These policies apply to all jobs in a Data Lake Analytics account.</span></span>

#### <a name="maximum-number-of-aus-in-a-data-lake-analytics-account"></a><span data-ttu-id="4f3c8-216">Максимальное число единиц использования аналитики в учетной записи Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="4f3c8-216">Maximum number of AUs in a Data Lake Analytics account</span></span>
<span data-ttu-id="4f3c8-217">Общее число единиц использования аналитики (AU), которые может использовать учетная запись Data Lake Analytics, контролируется политикой.</span><span class="sxs-lookup"><span data-stu-id="4f3c8-217">A policy controls the total number of Analytics Units (AUs) your Data Lake Analytics account can use.</span></span> <span data-ttu-id="4f3c8-218">По умолчанию установлено значение 250.</span><span class="sxs-lookup"><span data-stu-id="4f3c8-218">By default, the value is set to 250.</span></span> <span data-ttu-id="4f3c8-219">Например, если это значение равно 250 единицам, можно выполнять одно задание с 250 единицами или 10 заданий с 25 единицами.</span><span class="sxs-lookup"><span data-stu-id="4f3c8-219">For example, if this value is set to 250 AUs, you can have one job running with 250 AUs assigned to it, or 10 jobs running with 25 AUs each.</span></span> <span data-ttu-id="4f3c8-220">Дополнительные задания, которые передаются, помещаются в очередь до завершения выполняющихся заданий.</span><span class="sxs-lookup"><span data-stu-id="4f3c8-220">Additional jobs that are submitted are queued until the running jobs are finished.</span></span> <span data-ttu-id="4f3c8-221">После завершения выполняющихся заданий единицы использования аналитики освобождаются и могут использоваться для выполнения заданий в очереди.</span><span class="sxs-lookup"><span data-stu-id="4f3c8-221">When running jobs are finished, AUs are freed up for the queued jobs to run.</span></span>

<span data-ttu-id="4f3c8-222">Чтобы изменить количество единиц использования аналитики для вашей учетной записи Data Lake Analytics, выполните следующее:</span><span class="sxs-lookup"><span data-stu-id="4f3c8-222">To change the number of AUs for your Data Lake Analytics account:</span></span>

1. <span data-ttu-id="4f3c8-223">На портале Azure выберите свою учетную запись Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="4f3c8-223">In the Azure portal, go to your Data Lake Analytics account.</span></span>
2. <span data-ttu-id="4f3c8-224">Щелкните **Свойства**.</span><span class="sxs-lookup"><span data-stu-id="4f3c8-224">Click **Properties**.</span></span>
3. <span data-ttu-id="4f3c8-225">В разделе **Максимум единиц аналитики (AU) на задание** передвиньте ползунок, чтобы выбрать значение, или введите значение в текстовом поле.</span><span class="sxs-lookup"><span data-stu-id="4f3c8-225">Under **Maximum AUs**, move the slider to select a value, or enter the value in the text box.</span></span> 
4. <span data-ttu-id="4f3c8-226">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="4f3c8-226">Click **Save**.</span></span>

> [!NOTE]
> <span data-ttu-id="4f3c8-227">Если требуется больше единиц использования аналитики, чем значение по умолчанию (250), на портале щелкните **Справка и поддержка**, чтобы отправить запрос в службу технической поддержки.</span><span class="sxs-lookup"><span data-stu-id="4f3c8-227">If you need more than the default (250) AUs, in the portal, click **Help+Support** to submit a support request.</span></span> <span data-ttu-id="4f3c8-228">Количество единиц использования аналитики, доступных в вашей учетной записи Data Lake Analytics, можно увеличить.</span><span class="sxs-lookup"><span data-stu-id="4f3c8-228">The number of AUs available in your Data Lake Analytics account can be increased.</span></span>
>

#### <a name="maximum-number-of-jobs-that-can-run-simultaneously"></a><span data-ttu-id="4f3c8-229">Максимальное количество одновременно выполняемых заданий</span><span class="sxs-lookup"><span data-stu-id="4f3c8-229">Maximum number of jobs that can run simultaneously</span></span>
<span data-ttu-id="4f3c8-230">Политика определяет количество заданий, которые могут выполняться одновременно.</span><span class="sxs-lookup"><span data-stu-id="4f3c8-230">A policy controls how many jobs can run at the same time.</span></span> <span data-ttu-id="4f3c8-231">По умолчанию установлено значение 20.</span><span class="sxs-lookup"><span data-stu-id="4f3c8-231">By default, this value is set to 20.</span></span> <span data-ttu-id="4f3c8-232">Если в вашей учетной записи Data Lake Analytics есть доступные единицы использования аналитики, новые задания будут запускаться немедленно до тех пор, пока общее количество выполняемых заданий не достигнет значения этой политики.</span><span class="sxs-lookup"><span data-stu-id="4f3c8-232">If your Data Lake Analytics has AUs available, new jobs are scheduled to run immediately until the total number of running jobs reaches the value of this policy.</span></span> <span data-ttu-id="4f3c8-233">По достижении максимального количества одновременно выполняемых заданий, последующие задания помещаются в очередь в порядке приоритета, пока не будет завершено одно или несколько запущенных заданий (в зависимости от доступности единиц использования аналитики).</span><span class="sxs-lookup"><span data-stu-id="4f3c8-233">When you reach the maximum number of jobs that can run simultaneously, subsequent jobs are queued in priority order until one or more running jobs complete (depending on AU availability).</span></span>

<span data-ttu-id="4f3c8-234">Чтобы изменить количество одновременно выполняемых заданий:</span><span class="sxs-lookup"><span data-stu-id="4f3c8-234">To change the number of jobs that can run simultaneously:</span></span>

1. <span data-ttu-id="4f3c8-235">На портале Azure выберите свою учетную запись Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="4f3c8-235">In the Azure portal, go to your Data Lake Analytics account.</span></span>
2. <span data-ttu-id="4f3c8-236">Щелкните **Свойства**.</span><span class="sxs-lookup"><span data-stu-id="4f3c8-236">Click **Properties**.</span></span>
3. <span data-ttu-id="4f3c8-237">В разделе **Максимальное число выполняемых заданий** передвиньте ползунок, чтобы выбрать значение, или введите значение в текстовом поле.</span><span class="sxs-lookup"><span data-stu-id="4f3c8-237">Under **Maximum Number of Running Jobs**, move the slider to select a value, or enter the value in the text box.</span></span> 
4. <span data-ttu-id="4f3c8-238">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="4f3c8-238">Click **Save**.</span></span>

> [!NOTE]
> <span data-ttu-id="4f3c8-239">Если требуется запустить больше заданий, чем значение по умолчанию (20), на портале щелкните **Справка и поддержка**, чтобы отправить запрос в службу технической поддержки.</span><span class="sxs-lookup"><span data-stu-id="4f3c8-239">If you need to run more than the default (20) number of jobs, in the portal, click **Help+Support** to submit a support request.</span></span> <span data-ttu-id="4f3c8-240">Количество одновременно выполняемых заданий, доступных в вашей учетной записи Data Lake Analytics, можно увеличить.</span><span class="sxs-lookup"><span data-stu-id="4f3c8-240">The number of jobs that can run simultaneously in your Data Lake Analytics account can be increased.</span></span>
>

#### <a name="how-long-to-keep-job-metadata-and-resources"></a><span data-ttu-id="4f3c8-241">Как долго следует хранить метаданные и ресурсы задания</span><span class="sxs-lookup"><span data-stu-id="4f3c8-241">How long to keep job metadata and resources</span></span> 
<span data-ttu-id="4f3c8-242">При запуске заданий U-SQL служба Data Lake Analytics сохраняет все связанные файлы.</span><span class="sxs-lookup"><span data-stu-id="4f3c8-242">When your users run U-SQL jobs, the Data Lake Analytics service retains all related files.</span></span> <span data-ttu-id="4f3c8-243">Связанные файлы включают в себя скрипт U-SQL, DLL-файлы, на которые ссылается скрипт U-SQL, скомпилированные ресурсы и статистику.</span><span class="sxs-lookup"><span data-stu-id="4f3c8-243">Related files include the U-SQL script, the DLL files referenced in the U-SQL script, compiled resources, and statistics.</span></span> <span data-ttu-id="4f3c8-244">Файлы находятся в папке /system/ учетной записи Azure Data Lake Storage по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="4f3c8-244">The files are in the /system/ folder of the default Azure Data Lake Storage account.</span></span> <span data-ttu-id="4f3c8-245">Эта политика определяет, как долго хранятся эти ресурсы, прежде чем они будут удалены автоматически (по умолчанию — 30 дней).</span><span class="sxs-lookup"><span data-stu-id="4f3c8-245">This policy controls how long these resources are stored before they are automatically deleted (the default is 30 days).</span></span> <span data-ttu-id="4f3c8-246">Эти файлы можно использовать для отладки, а также для настройки производительности заданий, которые будут повторно выполнятся в будущем.</span><span class="sxs-lookup"><span data-stu-id="4f3c8-246">You can use these files for debugging, and for performance-tuning of jobs that you'll rerun in the future.</span></span>

<span data-ttu-id="4f3c8-247">Чтобы изменить срок хранения метаданных и ресурсов задания:</span><span class="sxs-lookup"><span data-stu-id="4f3c8-247">To change how long to keep job metadata and resources:</span></span>

1. <span data-ttu-id="4f3c8-248">На портале Azure выберите свою учетную запись Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="4f3c8-248">In the Azure portal, go to your Data Lake Analytics account.</span></span>
2. <span data-ttu-id="4f3c8-249">Щелкните **Свойства**.</span><span class="sxs-lookup"><span data-stu-id="4f3c8-249">Click **Properties**.</span></span>
3. <span data-ttu-id="4f3c8-250">В разделе **Срок хранения запросов заданий в днях** передвиньте ползунок, чтобы выбрать значение, или введите значение в текстовом поле.</span><span class="sxs-lookup"><span data-stu-id="4f3c8-250">Under **Days to Retain Job Queries**, move the slider to select a value, or enter the value in the text box.</span></span>  
4. <span data-ttu-id="4f3c8-251">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="4f3c8-251">Click **Save**.</span></span>

### <a name="job-level-policies"></a><span data-ttu-id="4f3c8-252">Политики на уровне задания</span><span class="sxs-lookup"><span data-stu-id="4f3c8-252">Job-level policies</span></span>
<span data-ttu-id="4f3c8-253">С помощью политик на уровне задания можно управлять максимальным количеством единиц использования аналитики и максимальным приоритетом, который отдельные пользователи (или участники групп безопасности) могут устанавливать в заданиях, которые они отправляют.</span><span class="sxs-lookup"><span data-stu-id="4f3c8-253">With job-level policies, you can control the maximum AUs and the maximum priority that individual users (or members of specific security groups) can set on jobs that they submit.</span></span> <span data-ttu-id="4f3c8-254">Это позволит контролировать затраты, которые несут пользователи.</span><span class="sxs-lookup"><span data-stu-id="4f3c8-254">This lets you control the costs incurred by users.</span></span> <span data-ttu-id="4f3c8-255">Политики также позволяют контролировать эффект, который запланированные задания могу оказать на рабочие задания с высоким приоритетом, запущенные в одной учетной записи Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="4f3c8-255">It also lets you control the effect that scheduled jobs might have on high-priority production jobs that are running in the same Data Lake Analytics account.</span></span>

<span data-ttu-id="4f3c8-256">Служба Data Lake Analytics имеет две политики, которые могут быть установлены на уровне задания.</span><span class="sxs-lookup"><span data-stu-id="4f3c8-256">Data Lake Analytics has two policies that you can set at the job level:</span></span>

* <span data-ttu-id="4f3c8-257">**Ограничение единиц использования аналитики для задания**: пользователи могут отправлять только те задания, которые содержат это число единиц использования аналитики.</span><span class="sxs-lookup"><span data-stu-id="4f3c8-257">**AU limit per job**: Users can only submit jobs that have up to this number of AUs.</span></span> <span data-ttu-id="4f3c8-258">По умолчанию это ограничение аналогично максимальному значению единиц использования аналитики для учетной записи.</span><span class="sxs-lookup"><span data-stu-id="4f3c8-258">By default, this limit is the same as the maximum AU limit for the account.</span></span>
* <span data-ttu-id="4f3c8-259">**Приоритет**: пользователи могут отправлять только те задания, приоритет которых меньше или равен этому значению.</span><span class="sxs-lookup"><span data-stu-id="4f3c8-259">**Priority**: Users can only submit jobs that have a priority lower than or equal to this value.</span></span> <span data-ttu-id="4f3c8-260">Обратите внимание, что большее значение означает более низкий приоритет.</span><span class="sxs-lookup"><span data-stu-id="4f3c8-260">Note that a higher number means a lower priority.</span></span> <span data-ttu-id="4f3c8-261">По умолчанию устанавливается значение 1, которое означает максимально возможный приоритет.</span><span class="sxs-lookup"><span data-stu-id="4f3c8-261">By default, this is set to 1, which is the highest possible priority.</span></span>

<span data-ttu-id="4f3c8-262">Для каждой учетной записи назначается политика по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="4f3c8-262">There is a default policy set on every account.</span></span> <span data-ttu-id="4f3c8-263">Она применяется ко всем пользователям учетной записи.</span><span class="sxs-lookup"><span data-stu-id="4f3c8-263">The default policy applies to all users of the account.</span></span> <span data-ttu-id="4f3c8-264">Можно установить дополнительные политики для отдельных пользователей и групп.</span><span class="sxs-lookup"><span data-stu-id="4f3c8-264">You can set additional policies for specific users and groups.</span></span> 

> [!NOTE]
> <span data-ttu-id="4f3c8-265">Политики на уровне учетной записи и политики на уровне задания применяются одновременно.</span><span class="sxs-lookup"><span data-stu-id="4f3c8-265">Account-level policies and job-level policies apply simultaneously.</span></span>
>

#### <a name="add-a-policy-for-a-specific-user-or-group"></a><span data-ttu-id="4f3c8-266">Добавление политики для конкретного пользователя или группы</span><span class="sxs-lookup"><span data-stu-id="4f3c8-266">Add a policy for a specific user or group</span></span>

1. <span data-ttu-id="4f3c8-267">На портале Azure выберите свою учетную запись Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="4f3c8-267">In the Azure portal, go to your Data Lake Analytics account.</span></span>
2. <span data-ttu-id="4f3c8-268">Щелкните **Свойства**.</span><span class="sxs-lookup"><span data-stu-id="4f3c8-268">Click **Properties**.</span></span>
3. <span data-ttu-id="4f3c8-269">В разделе **Пределы отправки заданий** нажмите кнопку **Добавить политику**.</span><span class="sxs-lookup"><span data-stu-id="4f3c8-269">Under **Job Submission Limits**, click the **Add Policy** button.</span></span> <span data-ttu-id="4f3c8-270">Затем выберите или введите следующие параметры.</span><span class="sxs-lookup"><span data-stu-id="4f3c8-270">Then, select or enter the following settings:</span></span>
    1. <span data-ttu-id="4f3c8-271">**Имя политики вычислений**: введите имя политики для напоминания о назначении политики.</span><span class="sxs-lookup"><span data-stu-id="4f3c8-271">**Compute Policy Name**: Enter a policy name, to remind you of the purpose of the policy.</span></span>
    2. <span data-ttu-id="4f3c8-272">**Выберите пользователя или группу**: выберите пользователя или группу, к которым будет применяться эта политика.</span><span class="sxs-lookup"><span data-stu-id="4f3c8-272">**Select User or Group**: Select the user or group this policy applies to.</span></span>
    3. <span data-ttu-id="4f3c8-273">**Задайте предел AU для задания**: установите предел единиц использования аналитики, который будет применяться для выбранного пользователя или группы.</span><span class="sxs-lookup"><span data-stu-id="4f3c8-273">**Set the Job AU Limit**: Set the AU limit that applies to the selected user or group.</span></span>
    4. <span data-ttu-id="4f3c8-274">**Set the Priority Limit** (Задайте предел приоритета): установите предел приоритета, который будет применяться для выбранного пользователя или группы.</span><span class="sxs-lookup"><span data-stu-id="4f3c8-274">**Set the Priority Limit**: Set the priority limit that applies to the selected user or group.</span></span>

4. <span data-ttu-id="4f3c8-275">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="4f3c8-275">Click **Ok**.</span></span>

5. <span data-ttu-id="4f3c8-276">Новая политика отобразится в таблице политик **По умолчанию** в разделе **Пределы отправки заданий**.</span><span class="sxs-lookup"><span data-stu-id="4f3c8-276">The new policy is listed in the **Default** policy table, under **Job Submission Limits**.</span></span> 

#### <a name="delete-or-edit-an-existing-policy"></a><span data-ttu-id="4f3c8-277">Удаление или изменение существующей политики</span><span class="sxs-lookup"><span data-stu-id="4f3c8-277">Delete or edit an existing policy</span></span>

1. <span data-ttu-id="4f3c8-278">На портале Azure выберите свою учетную запись Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="4f3c8-278">In the Azure portal, go to your Data Lake Analytics account.</span></span>
2. <span data-ttu-id="4f3c8-279">Щелкните **Свойства**.</span><span class="sxs-lookup"><span data-stu-id="4f3c8-279">Click **Properties**.</span></span>
3. <span data-ttu-id="4f3c8-280">В разделе **Пределы отправки заданий** найдите политику, которую требуется изменить.</span><span class="sxs-lookup"><span data-stu-id="4f3c8-280">Under **Job Submission Limits**, find the policy you want to edit.</span></span>
4.  <span data-ttu-id="4f3c8-281">Чтобы увидеть параметры **Удалить** и **Изменить**, в правом столбце таблицы щелкните **…**.</span><span class="sxs-lookup"><span data-stu-id="4f3c8-281">To see the **Delete** and **Edit** options, in the rightmost column of the table, click **...**.</span></span>

### <a name="additional-resources-for-job-policies"></a><span data-ttu-id="4f3c8-282">Дополнительные ресурсы политики заданий</span><span class="sxs-lookup"><span data-stu-id="4f3c8-282">Additional resources for job policies</span></span>
* [<span data-ttu-id="4f3c8-283">Запись блога с обзором политик</span><span class="sxs-lookup"><span data-stu-id="4f3c8-283">Policy overview blog post</span></span>](https://blogs.msdn.microsoft.com/azuredatalake/2017/06/08/managing-your-azure-data-lake-analytics-compute-resources-overview/)
* [<span data-ttu-id="4f3c8-284">Запись блога о политиках на уровне учетной записи</span><span class="sxs-lookup"><span data-stu-id="4f3c8-284">Account-level policies blog post</span></span>](https://blogs.msdn.microsoft.com/azuredatalake/2017/06/08/managing-your-azure-data-lake-analytics-compute-resources-account-level-policy/)
* [<span data-ttu-id="4f3c8-285">Запись блога о политиках на уровне задания</span><span class="sxs-lookup"><span data-stu-id="4f3c8-285">Job-level policies blog post</span></span>](https://blogs.msdn.microsoft.com/azuredatalake/2017/06/08/managing-your-azure-data-lake-analytics-compute-resources-job-level-policy/)

## <a name="next-steps"></a><span data-ttu-id="4f3c8-286">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="4f3c8-286">Next steps</span></span>

* [<span data-ttu-id="4f3c8-287">Обзор аналитики озера данных Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="4f3c8-287">Overview of Azure Data Lake Analytics</span></span>](data-lake-analytics-overview.md)
* [<span data-ttu-id="4f3c8-288">Начало работы с Azure Data Lake Analytics с помощью портала Azure</span><span class="sxs-lookup"><span data-stu-id="4f3c8-288">Get started with Data Lake Analytics by using the Azure portal</span></span>](data-lake-analytics-get-started-portal.md)
* [<span data-ttu-id="4f3c8-289">Управление Azure Data Lake Analytics с помощью Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="4f3c8-289">Manage Azure Data Lake Analytics by using Azure PowerShell</span></span>](data-lake-analytics-manage-use-powershell.md)

