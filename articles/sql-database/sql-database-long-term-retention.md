---
title: "aaaStore резервные копии базы данных SQL Azure для копирования лет too10 | Документы Microsoft"
description: "Узнайте, как база данных SQL Azure позволяет хранить резервные копии для копирования too10 лет."
keywords: 
services: sql-database
documentationcenter: 
author: anosov1960
manager: jhubbard
editor: 
ms.assetid: 66fdb8b8-5903-4d3a-802e-af08d204566e
ms.service: sql-database
ms.custom: business continuity
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 12/22/2016
ms.author: sashan
ms.openlocfilehash: 5825ebd4e3bd66b59b13aea603d377ef814a1df3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="store-azure-sql-database-backups-for-up-too10-years"></a><span data-ttu-id="63d13-103">Хранить резервные копии базы данных SQL Azure для копирования too10 лет</span><span class="sxs-lookup"><span data-stu-id="63d13-103">Store Azure SQL Database backups for up too10 years</span></span>
<span data-ttu-id="63d13-104">Многие приложения имеют нормативным, соответствия или другие бизнес-целей, на которых требуют tooretain резервные копии баз данных за пределы hello 7 35 дней, предоставляемые базой данных SQL Azure [автоматического резервного копирования](sql-database-automated-backups.md).</span><span class="sxs-lookup"><span data-stu-id="63d13-104">Many applications have regulatory, compliance, or other business purposes that require you tooretain database backups beyond hello 7-35 days provided by Azure SQL Database [automatic backups](sql-database-automated-backups.md).</span></span> <span data-ttu-id="63d13-105">Средство hello долгосрочного хранения резервных копий, можно хранить резервные копии базы данных SQL в хранилище служб восстановления Azure для копирования too10 лет.</span><span class="sxs-lookup"><span data-stu-id="63d13-105">By using hello long-term backup retention feature, you can store your SQL database backups in an Azure Recovery Services vault for up too10 years.</span></span> <span data-ttu-id="63d13-106">Вы можете хранить копии too1 000 баз данных на хранилище.</span><span class="sxs-lookup"><span data-stu-id="63d13-106">You can store up too1,000 databases per vault.</span></span> <span data-ttu-id="63d13-107">Затем можно выбрать любой резервной копии toorestore хранилище hello его как новую базу данных.</span><span class="sxs-lookup"><span data-stu-id="63d13-107">You then can select any backup in hello vault toorestore it as a new database.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="63d13-108">Долгосрочного хранения резервных копий является в настоящее время в предварительной версии и доступен в следующих регионах hello: Восточная Австралия, Юго-Восточная Австралия, Южной Бразилии, центральной части США, Восточная Азия, восточная часть США, восточная часть США 2, центральной Индии, Южной Индии, восток Японии, Запад Японии, северо-центральный регион США, Северная Европа, центральный Юг США, Юго-Восточной Азии, Западной Европе и Запад США.</span><span class="sxs-lookup"><span data-stu-id="63d13-108">Long-term backup retention is currently in preview and available in hello following regions: Australia East, Australia Southeast, Brazil South, Central US, East Asia, East US, East US 2, India Central, India South, Japan East, Japan West, North Central US, North Europe, South Central US, Southeast Asia, West Europe, and West US.</span></span>
>

> [!NOTE]
> <span data-ttu-id="63d13-109">Копирование баз данных too200 каждое хранилище можно включить в 24-часовой период.</span><span class="sxs-lookup"><span data-stu-id="63d13-109">You can enable up too200 databases per vault during a 24-hour period.</span></span> <span data-ttu-id="63d13-110">Рекомендуется использовать отдельные хранилища для каждого сервера toominimize hello влияние этого предела.</span><span class="sxs-lookup"><span data-stu-id="63d13-110">We recommend that you use a separate vault for each server toominimize hello impact of this limit.</span></span> 
> 

## <a name="how-sql-database-long-term-backup-retention-works"></a><span data-ttu-id="63d13-111">Принципы работы долгосрочного хранения резервных копий базы данных SQL</span><span class="sxs-lookup"><span data-stu-id="63d13-111">How SQL Database long-term backup retention works</span></span>

<span data-ttu-id="63d13-112">Благодаря долгосрочному хранению резервных копий можно привязать сервер базы данных SQL Azure к хранилищу служб восстановления Azure.</span><span class="sxs-lookup"><span data-stu-id="63d13-112">With long-term backup retention, you can associate a SQL database server with an Azure Recovery Services vault.</span></span> 

* <span data-ttu-id="63d13-113">Необходимо создать хранилище hello в hello одной подписке, который создан hello SQL server и в hello же географического региона и группе ресурсов.</span><span class="sxs-lookup"><span data-stu-id="63d13-113">You must create hello vault in hello same Azure subscription that created hello SQL server and in hello same geographic region and resource group.</span></span> 
* <span data-ttu-id="63d13-114">Затем вы сможете настроить политику хранения для любой базы данных.</span><span class="sxs-lookup"><span data-stu-id="63d13-114">You then configure a retention policy for any database.</span></span> <span data-ttu-id="63d13-115">Hello политики причины hello еженедельно всей базы данных резервных копий toobe копируются toohello хранилище служб восстановления и сохранить для hello заданного срока хранения (вверх too10 лет).</span><span class="sxs-lookup"><span data-stu-id="63d13-115">hello policy causes hello weekly full database backups toobe copied toohello Recovery Services vault and retained for hello specified retention period (up too10 years).</span></span> 
* <span data-ttu-id="63d13-116">Затем можно восстановить hello базы данных из любого из этих резервных копий tooa новой базы данных в любой сервер в подписке hello.</span><span class="sxs-lookup"><span data-stu-id="63d13-116">You can then restore hello database from any of these backups tooa new database in any server in hello subscription.</span></span> <span data-ttu-id="63d13-117">Хранилище Azure создает копию с существующие резервные копии и копии hello имеет не влияет на производительность hello существующей базы данных.</span><span class="sxs-lookup"><span data-stu-id="63d13-117">Azure storage creates a copy from existing backups, and hello copy has no performance impact on hello existing database.</span></span>

> [!TIP]
> <span data-ttu-id="63d13-118">Как tooguide разделе [Настройка и восстановление из долгосрочного хранения резервной копии базы данных SQL Azure](sql-database-long-term-backup-retention-configure.md).</span><span class="sxs-lookup"><span data-stu-id="63d13-118">For a how-tooguide, see [Configure and restore from Azure SQL Database long-term backup retention](sql-database-long-term-backup-retention-configure.md).</span></span>

## <a name="enable-long-term-backup-retention"></a><span data-ttu-id="63d13-119">Включение долгосрочного хранения резервных копий</span><span class="sxs-lookup"><span data-stu-id="63d13-119">Enable long-term backup retention</span></span>

<span data-ttu-id="63d13-120">tooconfigure долгосрочного хранения резервной копии для базы данных:</span><span class="sxs-lookup"><span data-stu-id="63d13-120">tooconfigure long-term backup retention for a database:</span></span>

1. <span data-ttu-id="63d13-121">Создание хранилища служб восстановления Azure в hello одной группе ресурса, региона и подписки с сервером баз данных SQL.</span><span class="sxs-lookup"><span data-stu-id="63d13-121">Create an Azure Recovery Services vault in hello same region, subscription, and resource group as your SQL database server.</span></span> 
2. <span data-ttu-id="63d13-122">Зарегистрируйте хранилище toohello сервера hello.</span><span class="sxs-lookup"><span data-stu-id="63d13-122">Register hello server toohello vault.</span></span>
3. <span data-ttu-id="63d13-123">Создайте политику защиты служб восстановления Azure.</span><span class="sxs-lookup"><span data-stu-id="63d13-123">Create an Azure Recovery Services protection policy.</span></span>
4. <span data-ttu-id="63d13-124">Примените hello защиты политики toohello баз данных, которые требуют долгосрочного хранения резервной копии.</span><span class="sxs-lookup"><span data-stu-id="63d13-124">Apply hello protection policy toohello databases that require long-term backup retention.</span></span>

<span data-ttu-id="63d13-125">tooconfigure, управлять и восстановите базу данных из долгосрочного хранения резервных копий для автоматического создания резервных копий в хранилище служб восстановления Azure, выполните одно из следующих hello.</span><span class="sxs-lookup"><span data-stu-id="63d13-125">tooconfigure, manage, and restore a database from long-term backup retention of automated backups in an Azure Recovery Services vault, do either of hello following:</span></span>

* <span data-ttu-id="63d13-126">Здравствуйте, с помощью портала Azure: щелкните **долгосрочного хранения резервной копии**, выберите базу данных и нажмите кнопку **Настройка**.</span><span class="sxs-lookup"><span data-stu-id="63d13-126">Using hello Azure portal: Click **Long-term backup retention**, select a database, and then click **Configure**.</span></span> 

   ![Выбор базы данных для настройки долгосрочного хранения резервных копий](./media/sql-database-get-started-backup-recovery/select-database-for-long-term-backup-retention.png)

* <span data-ttu-id="63d13-128">С помощью PowerShell: Перейти слишком[Настройка и восстановление из долгосрочного хранения резервной копии базы данных SQL Azure](sql-database-long-term-backup-retention-configure.md).</span><span class="sxs-lookup"><span data-stu-id="63d13-128">Using PowerShell: Go too[Configure and restore from Azure SQL Database long-term backup retention](sql-database-long-term-backup-retention-configure.md).</span></span>

## <a name="restore-a-database-thats-stored-with-hello-long-term-backup-retention-feature"></a><span data-ttu-id="63d13-129">Восстановление базы данных, который хранится вместе с долгосрочного хранения резервной копии функция hello</span><span class="sxs-lookup"><span data-stu-id="63d13-129">Restore a database that's stored with hello long-term backup retention feature</span></span>

<span data-ttu-id="63d13-130">toorecover из резервной копии долгосрочного хранения резервной копии:</span><span class="sxs-lookup"><span data-stu-id="63d13-130">toorecover from a long-term backup retention backup:</span></span>

1. <span data-ttu-id="63d13-131">Список hello хранилища, где хранится резервная копия hello.</span><span class="sxs-lookup"><span data-stu-id="63d13-131">List hello vault where hello backup is stored.</span></span>
2. <span data-ttu-id="63d13-132">Контейнер списка hello, сопоставленные tooyour логического сервера.</span><span class="sxs-lookup"><span data-stu-id="63d13-132">List hello container that is mapped tooyour logical server.</span></span>
3. <span data-ttu-id="63d13-133">Список hello источник данных в хранилище hello, сопоставленные tooyour базы данных.</span><span class="sxs-lookup"><span data-stu-id="63d13-133">List hello data source within hello vault that is mapped tooyour database.</span></span>
4. <span data-ttu-id="63d13-134">Список точек восстановления hello, доступных toorestore.</span><span class="sxs-lookup"><span data-stu-id="63d13-134">List hello recovery points that are available toorestore.</span></span>
5. <span data-ttu-id="63d13-135">Восстановление базы данных hello hello восстановления toohello точка целевого сервера в рамках вашей подписки.</span><span class="sxs-lookup"><span data-stu-id="63d13-135">Restore hello database from hello recovery point toohello target server within your subscription.</span></span>

<span data-ttu-id="63d13-136">tooconfigure, управлять и восстановите базу данных из долгосрочного хранения резервных копий для автоматического создания резервных копий в хранилище служб восстановления Azure, выполните одно из следующих hello.</span><span class="sxs-lookup"><span data-stu-id="63d13-136">tooconfigure, manage, and restore a database from long-term backup retention of automated backups in an Azure Recovery Services vault, do either of hello following:</span></span>

* <span data-ttu-id="63d13-137">С помощью портала Azure "hello": слишком Go[управление долгосрочного хранения резервных копий использование hello портал Azure](sql-database-long-term-backup-retention-configure.md).</span><span class="sxs-lookup"><span data-stu-id="63d13-137">Using hello Azure portal: Go too[Manage long-term backup retention using hello Azure portal](sql-database-long-term-backup-retention-configure.md).</span></span> 

* <span data-ttu-id="63d13-138">С помощью PowerShell: Перейти слишком[управление долгосрочного хранения резервной копии с помощью PowerShell](sql-database-long-term-backup-retention-configure.md).</span><span class="sxs-lookup"><span data-stu-id="63d13-138">Using PowerShell: Go too[Manage long-term backup retention using PowerShell](sql-database-long-term-backup-retention-configure.md).</span></span>

## <a name="get-pricing-for-long-term-backup-retention"></a><span data-ttu-id="63d13-139">Получение расценок для настройки долгосрочного хранения резервных копий</span><span class="sxs-lookup"><span data-stu-id="63d13-139">Get pricing for long-term backup retention</span></span>

<span data-ttu-id="63d13-140">Взимается плата долгосрочного хранения резервной копии базы данных SQL в соответствии с toohello [резервные службы Azure, ценах курсы](https://azure.microsoft.com/pricing/details/backup/).</span><span class="sxs-lookup"><span data-stu-id="63d13-140">Long-term backup retention of a SQL database is charged according toohello [Azure backup services pricing rates](https://azure.microsoft.com/pricing/details/backup/).</span></span>

<span data-ttu-id="63d13-141">После hello сервера базы данных SQL хранилище зарегистрированного toohello, назначается цена hello общий объем хранилища, используемый hello еженедельного резервного копирования, хранящихся в хранилище hello.</span><span class="sxs-lookup"><span data-stu-id="63d13-141">After hello SQL database server is registered toohello vault, you are charged for hello total storage that's used by hello weekly backups stored in hello vault.</span></span>

## <a name="view-available-backups-that-are-stored-in-long-term-backup-retention"></a><span data-ttu-id="63d13-142">Просмотр доступных резервных копий, хранимых в службе долгосрочного хранения</span><span class="sxs-lookup"><span data-stu-id="63d13-142">View available backups that are stored in long-term backup retention</span></span>

<span data-ttu-id="63d13-143">tooconfigure, управлять и восстановите базу данных из долгосрочного хранения резервных копий для автоматического создания резервных копий в хранилище служб восстановления Azure с помощью hello портал Azure, выполните одно из следующих hello:</span><span class="sxs-lookup"><span data-stu-id="63d13-143">tooconfigure, manage, and restore a database from long-term backup retention of automated backups in an Azure Recovery Services vault by using hello Azure portal, do either of hello following:</span></span>

* <span data-ttu-id="63d13-144">С помощью портала Azure "hello": слишком Go[управление долгосрочного хранения резервных копий использование hello портал Azure](sql-database-long-term-backup-retention-configure.md).</span><span class="sxs-lookup"><span data-stu-id="63d13-144">Using hello Azure portal: Go too[Manage long-term backup retention using hello Azure portal](sql-database-long-term-backup-retention-configure.md).</span></span> 

* <span data-ttu-id="63d13-145">С помощью PowerShell: Перейти слишком[управление долгосрочного хранения резервной копии с помощью PowerShell](sql-database-long-term-backup-retention-configure.md).</span><span class="sxs-lookup"><span data-stu-id="63d13-145">Using PowerShell: Go too[Manage long-term backup retention using PowerShell](sql-database-long-term-backup-retention-configure.md).</span></span>

## <a name="disable-long-term-retention"></a><span data-ttu-id="63d13-146">Отключение долгосрочного хранения</span><span class="sxs-lookup"><span data-stu-id="63d13-146">Disable long-term retention</span></span>

<span data-ttu-id="63d13-147">службы восстановления Hello автоматически обрабатывает очистки hello основании hello, предоставляемые политики хранения резервных копий.</span><span class="sxs-lookup"><span data-stu-id="63d13-147">hello recovery service automatically handles hello cleanup of backups based on hello provided retention policy.</span></span> 

<span data-ttu-id="63d13-148">toostop отправку резервные копии hello для конкретной базы данных хранилища toohello, удалите hello политику хранения для этой базы данных.</span><span class="sxs-lookup"><span data-stu-id="63d13-148">toostop sending hello backups for a specific database toohello vault, remove hello retention policy for that database.</span></span>
  
```
Set-AzureRmSqlDatabaseBackupLongTermRetentionPolicy -ResourceGroupName 'RG1' -ServerName 'Server1' -DatabaseName 'DB1' -State 'Disabled' -ResourceId $policy.Id
```

> [!NOTE]
> <span data-ttu-id="63d13-149">Hello резервных копий, которые уже находятся в хранилище hello не затрагиваются.</span><span class="sxs-lookup"><span data-stu-id="63d13-149">hello backups that are already in hello vault are unaffected.</span></span> <span data-ttu-id="63d13-150">Они автоматически удалено службой восстановления hello, по истечении их срока хранения.</span><span class="sxs-lookup"><span data-stu-id="63d13-150">They are automatically deleted by hello recovery service when their retention period expires.</span></span>

## <a name="long-term-backup-retention-faq"></a><span data-ttu-id="63d13-151">Часто задаваемые вопросы о долгосрочном хранении резервных копий</span><span class="sxs-lookup"><span data-stu-id="63d13-151">Long-term backup retention FAQ</span></span>

<span data-ttu-id="63d13-152">**Можно вручную удалить конкретных резервных копий в хранилище hello?**</span><span class="sxs-lookup"><span data-stu-id="63d13-152">**Can I manually delete specific backups in hello vault?**</span></span>

<span data-ttu-id="63d13-153">В настоящее время нет.</span><span class="sxs-lookup"><span data-stu-id="63d13-153">Not currently.</span></span> <span data-ttu-id="63d13-154">хранилище Hello автоматически очищает резервных копий при истечении срока хранения hello.</span><span class="sxs-lookup"><span data-stu-id="63d13-154">hello vault automatically cleans up backups when hello retention period has expired.</span></span>

<span data-ttu-id="63d13-155">**Можно зарегистрировать toomore резервные копии toostore my server, чем одно хранилище**</span><span class="sxs-lookup"><span data-stu-id="63d13-155">**Can I register my server toostore backups toomore than one vault?**</span></span>

<span data-ttu-id="63d13-156">Нет, можно хранить в настоящее время один хранилище резервных копий tooonly одновременно.</span><span class="sxs-lookup"><span data-stu-id="63d13-156">No, you can currently store backups tooonly one vault at a time.</span></span>

<span data-ttu-id="63d13-157">**Можно ли использовать хранилище и сервер из разных подписок?**</span><span class="sxs-lookup"><span data-stu-id="63d13-157">**Can I have a vault and server in different subscriptions?**</span></span>

<span data-ttu-id="63d13-158">Нет, в настоящее время хранилище hello и сервер должны быть в hello же подписке и группе ресурсов.</span><span class="sxs-lookup"><span data-stu-id="63d13-158">No, currently hello vault and server must be in hello same subscription and resource group.</span></span>

<span data-ttu-id="63d13-159">**Можно ли использовать хранилище, созданное не в том регионе, где расположен мой сервер?**</span><span class="sxs-lookup"><span data-stu-id="63d13-159">**Can I use a vault that I created in a region that's different from my server’s region?**</span></span>

<span data-ttu-id="63d13-160">Нет, хранилище hello и сервер должны находиться в hello toominimize же регионе, скопируйте времени и избежать расходов трафика.</span><span class="sxs-lookup"><span data-stu-id="63d13-160">No, hello vault and server must be in hello same region toominimize copy time and avoid traffic charges.</span></span>

<span data-ttu-id="63d13-161">**Сколько баз данных можно хранить в одном хранилище?**</span><span class="sxs-lookup"><span data-stu-id="63d13-161">**How many databases can I store in one vault?**</span></span>

<span data-ttu-id="63d13-162">В настоящее время мы поддерживаем вверх too1 000 баз данных на хранилище.</span><span class="sxs-lookup"><span data-stu-id="63d13-162">Currently, we support up too1,000 databases per vault.</span></span> 

<span data-ttu-id="63d13-163">**Сколько хранилищ можно создать в одной подписке?**</span><span class="sxs-lookup"><span data-stu-id="63d13-163">**How many vaults can I create per subscription?**</span></span>

<span data-ttu-id="63d13-164">Можно создать копию too25 хранилищ для каждой подписки.</span><span class="sxs-lookup"><span data-stu-id="63d13-164">You can create up too25 vaults per subscription.</span></span>

<span data-ttu-id="63d13-165">**Сколько баз данных можно настроить для одного хранилища в день?**</span><span class="sxs-lookup"><span data-stu-id="63d13-165">**How many databases can I configure per day per vault?**</span></span>

<span data-ttu-id="63d13-166">Для одного хранилища можно настроить не более 200 баз данных в день.</span><span class="sxs-lookup"><span data-stu-id="63d13-166">You can set up 200 databases per day per vault.</span></span>

<span data-ttu-id="63d13-167">**Работает ли долгосрочное хранение резервных копий с эластичными пулами?**</span><span class="sxs-lookup"><span data-stu-id="63d13-167">**Does long-term backup retention work with elastic pools?**</span></span>

<span data-ttu-id="63d13-168">Да.</span><span class="sxs-lookup"><span data-stu-id="63d13-168">Yes.</span></span> <span data-ttu-id="63d13-169">Можно настроить любой базы данных в пуле hello с политикой хранения hello.</span><span class="sxs-lookup"><span data-stu-id="63d13-169">Any database in hello pool can be configured with hello retention policy.</span></span>

<span data-ttu-id="63d13-170">**Можно выбрать hello времени, в которое создана резервная копия hello**</span><span class="sxs-lookup"><span data-stu-id="63d13-170">**Can I choose hello time at which hello backup is created?**</span></span>

<span data-ttu-id="63d13-171">Нет, база данных SQL управляет hello расписание резервного копирования toominimize hello влияние на производительность базы данных.</span><span class="sxs-lookup"><span data-stu-id="63d13-171">No, SQL Database controls hello backup schedule toominimize hello performance impact on your databases.</span></span>

<span data-ttu-id="63d13-172">**Для нашей базы данных включено прозрачное шифрование данных. Можно ли использовать его с хранилищем hello?**</span><span class="sxs-lookup"><span data-stu-id="63d13-172">**I have transparent data encryption enabled for my database. Can I use it with hello vault?**</span></span> 

<span data-ttu-id="63d13-173">Да, прозрачное шифрование данных поддерживается.</span><span class="sxs-lookup"><span data-stu-id="63d13-173">Yes, transparent data encryption is supported.</span></span> <span data-ttu-id="63d13-174">Hello базу данных можно восстановить из хранилища hello, даже если hello исходная база данных больше не существует.</span><span class="sxs-lookup"><span data-stu-id="63d13-174">You can restore hello database from hello vault even if hello original database no longer exists.</span></span>

<span data-ttu-id="63d13-175">**Если подписка приостановлена, что происходит с резервными копиями hello в хранилище hello?**</span><span class="sxs-lookup"><span data-stu-id="63d13-175">**What happens with hello backups in hello vault if my subscription is suspended?**</span></span> 

<span data-ttu-id="63d13-176">Если подписка приостановлена, мы сохранить hello существующих баз данных и резервных копий.</span><span class="sxs-lookup"><span data-stu-id="63d13-176">If your subscription is suspended, we retain hello existing databases and backups.</span></span> <span data-ttu-id="63d13-177">Новые резервные копии не копируются toohello хранилища.</span><span class="sxs-lookup"><span data-stu-id="63d13-177">New backups are not copied toohello vault.</span></span> <span data-ttu-id="63d13-178">После повторной активации подписки hello, служба hello возобновляет копирование toohello хранилище резервных копий.</span><span class="sxs-lookup"><span data-stu-id="63d13-178">After you reactivate hello subscription, hello service resumes copying backups toohello vault.</span></span> <span data-ttu-id="63d13-179">Ваше хранилище становится доступен toohello операции восстановления с помощью hello резервных копий, которые были скопированы существует до приостановки подписки hello.</span><span class="sxs-lookup"><span data-stu-id="63d13-179">Your vault becomes accessible toohello restore operations by using hello backups that were copied there before hello subscription was suspended.</span></span> 

<span data-ttu-id="63d13-180">**Можно получить доступ файлы резервной копии базы данных SQL toohello, можно загрузить или восстановить их toohello SQL server?**</span><span class="sxs-lookup"><span data-stu-id="63d13-180">**Can I get access toohello SQL database backup files so I can download or restore them toohello SQL server?**</span></span>

<span data-ttu-id="63d13-181">В настоящее время это невозможно.</span><span class="sxs-lookup"><span data-stu-id="63d13-181">No, not currently.</span></span>

<span data-ttu-id="63d13-182">**Это возможно toohave несколько расписаний (день, неделю, раз в месяц, раз в год) в политику хранения SQL.**</span><span class="sxs-lookup"><span data-stu-id="63d13-182">**Is it possible toohave multiple schedules (daily, weekly, monthly, yearly) within a SQL retention policy.**</span></span>

<span data-ttu-id="63d13-183">Нет, несколько расписаний пока доступны только для резервных копий виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="63d13-183">No, multiple schedules are currently available only for virtual machine backups.</span></span>

<span data-ttu-id="63d13-184">**Мы настроили долгосрочное хранение резервных копий для базы данных, которая является базой данных-получателем с активной георепликацией. Поддерживается ли такая конфигурация?**</span><span class="sxs-lookup"><span data-stu-id="63d13-184">**What if we set up long-term backup retention on a database that is an active geo-replication secondary database?**</span></span>

<span data-ttu-id="63d13-185">Поскольку резервное копирование на репликах не выполняется, долгосрочное хранение резервных копий в базах данных-получателях пока не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="63d13-185">Because we don't take backups on replicas, there is currently no option for long-term backup retention on secondary databases.</span></span> <span data-ttu-id="63d13-186">Тем не менее очень важно для пользователей tooset копирование долгосрочного хранения резервной копии базы данных-получателя активной георепликации по следующим причинам:</span><span class="sxs-lookup"><span data-stu-id="63d13-186">However, it is important for users tooset up long-term backup retention on an active geo-replication secondary database for these reasons:</span></span>
* <span data-ttu-id="63d13-187">Когда происходит отработка отказа и hello база данных становится основной базы данных, мы выполнить полное резервное копирование, являющееся отправленного toovault.</span><span class="sxs-lookup"><span data-stu-id="63d13-187">When a failover happens and hello database becomes a primary database, we take a full backup, which is uploaded toovault.</span></span>
* <span data-ttu-id="63d13-188">Нет без дополнительных затрат toohello клиента для настройки долгосрочного хранения резервной копии базы данных-получателя.</span><span class="sxs-lookup"><span data-stu-id="63d13-188">There is no extra cost toohello customer for setting up long-term backup retention on a secondary database.</span></span>

## <a name="next-steps"></a><span data-ttu-id="63d13-189">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="63d13-189">Next steps</span></span>
<span data-ttu-id="63d13-190">Поскольку резервные копии базы данных защищают данные от случайного повреждения или удаления, они являются важной частью любой стратегии непрерывности бизнес-процессов и аварийного восстановления.</span><span class="sxs-lookup"><span data-stu-id="63d13-190">Because database backups protect data from accidental corruption or deletion, they're an essential part of any business continuity and disaster recovery strategy.</span></span> <span data-ttu-id="63d13-191">toolearn около hello другим решениям непрерывности базы данных SQL см. в разделе [непрерывности бизнес-обзора](sql-database-business-continuity.md).</span><span class="sxs-lookup"><span data-stu-id="63d13-191">toolearn about hello other SQL Database business-continuity solutions, see [Business continuity overview](sql-database-business-continuity.md).</span></span>
