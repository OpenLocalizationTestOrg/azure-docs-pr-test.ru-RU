---
title: "Хранение резервных копий базы данных SQL Azure до 10 лет | Документы Майкрософт"
description: "Узнайте, как база данных SQL Azure поддерживает хранение резервных копий в течение 10 лет."
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
ms.openlocfilehash: 25e651203f804fbf32d632b5f83145a3f3f72a7f
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="store-azure-sql-database-backups-for-up-to-10-years"></a><span data-ttu-id="24fa2-103">Хранение резервных копий базы данных SQL Azure до 10 лет</span><span class="sxs-lookup"><span data-stu-id="24fa2-103">Store Azure SQL Database backups for up to 10 years</span></span>
<span data-ttu-id="24fa2-104">В соответствии с нормативными требованиями, стандартами соответствия или бизнес-задачами многие приложения должны хранить резервные копии баз данных более 7–35 дней, то есть дольше, чем при [автоматическом резервном копировании](sql-database-automated-backups.md) базы данных SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="24fa2-104">Many applications have regulatory, compliance, or other business purposes that require you to retain database backups beyond the 7-35 days provided by Azure SQL Database [automatic backups](sql-database-automated-backups.md).</span></span> <span data-ttu-id="24fa2-105">Функция долгосрочного хранения резервных копий позволяет хранить резервные копии базы данных SQL Azure в хранилище служб восстановления Azure до 10 лет.</span><span class="sxs-lookup"><span data-stu-id="24fa2-105">By using the long-term backup retention feature, you can store your SQL database backups in an Azure Recovery Services vault for up to 10 years.</span></span> <span data-ttu-id="24fa2-106">В каждом хранилище можно разместить до 1000 баз данных.</span><span class="sxs-lookup"><span data-stu-id="24fa2-106">You can store up to 1,000 databases per vault.</span></span> <span data-ttu-id="24fa2-107">Вы можете выбрать любую резервную копию из хранилища и восстановить ее как новую базу данных.</span><span class="sxs-lookup"><span data-stu-id="24fa2-107">You then can select any backup in the vault to restore it as a new database.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="24fa2-108">Долгосрочное хранение резервных копий в настоящее время находится на этапе предварительной версии и доступно в следующих регионах: восточная Австралия, юго-восточная Австралия, южная Бразилия, центральная часть США, Восточная Азия, восточная часть США, восточная часть США 2, центральная Индия, южная Индия, восточная Япония, западная Япония, северо-центральный регион США, Северная Европа, юго-центральный регион США, Юго-Восточная Азия, Западная Европа и западная часть США.</span><span class="sxs-lookup"><span data-stu-id="24fa2-108">Long-term backup retention is currently in preview and available in the following regions: Australia East, Australia Southeast, Brazil South, Central US, East Asia, East US, East US 2, India Central, India South, Japan East, Japan West, North Central US, North Europe, South Central US, Southeast Asia, West Europe, and West US.</span></span>
>

> [!NOTE]
> <span data-ttu-id="24fa2-109">В каждом хранилище в течение 24 часов можно включить до 200 баз данных.</span><span class="sxs-lookup"><span data-stu-id="24fa2-109">You can enable up to 200 databases per vault during a 24-hour period.</span></span> <span data-ttu-id="24fa2-110">Мы рекомендуем использовать отдельное хранилище для каждого сервера, чтобы эти ограничения вам не мешали.</span><span class="sxs-lookup"><span data-stu-id="24fa2-110">We recommend that you use a separate vault for each server to minimize the impact of this limit.</span></span> 
> 

## <a name="how-sql-database-long-term-backup-retention-works"></a><span data-ttu-id="24fa2-111">Принципы работы долгосрочного хранения резервных копий базы данных SQL</span><span class="sxs-lookup"><span data-stu-id="24fa2-111">How SQL Database long-term backup retention works</span></span>

<span data-ttu-id="24fa2-112">Благодаря долгосрочному хранению резервных копий можно привязать сервер базы данных SQL Azure к хранилищу служб восстановления Azure.</span><span class="sxs-lookup"><span data-stu-id="24fa2-112">With long-term backup retention, you can associate a SQL database server with an Azure Recovery Services vault.</span></span> 

* <span data-ttu-id="24fa2-113">Это хранилище должно быть создано в той же подписке Azure, что и сервер для базы данных SQL, в том же географическом регионе и в той же группе ресурсов.</span><span class="sxs-lookup"><span data-stu-id="24fa2-113">You must create the vault in the same Azure subscription that created the SQL server and in the same geographic region and resource group.</span></span> 
* <span data-ttu-id="24fa2-114">Затем вы сможете настроить политику хранения для любой базы данных.</span><span class="sxs-lookup"><span data-stu-id="24fa2-114">You then configure a retention policy for any database.</span></span> <span data-ttu-id="24fa2-115">Если эта политика настроена, полная резервная копия базы данных еженедельно копируется в хранилище служб восстановления и хранится там в течение указанного срока (до 10 лет).</span><span class="sxs-lookup"><span data-stu-id="24fa2-115">The policy causes the weekly full database backups to be copied to the Recovery Services vault and retained for the specified retention period (up to 10 years).</span></span> 
* <span data-ttu-id="24fa2-116">Вы сможете восстановить любую из этих резервных копий базы данных, развернув ее в новую базу данных на любом сервере в вашей подписке.</span><span class="sxs-lookup"><span data-stu-id="24fa2-116">You can then restore the database from any of these backups to a new database in any server in the subscription.</span></span> <span data-ttu-id="24fa2-117">Служба хранилища Azure копирует для этой цели существующую резервную копию, и этот процесс никак не влияет на производительность существующей базы данных.</span><span class="sxs-lookup"><span data-stu-id="24fa2-117">Azure storage creates a copy from existing backups, and the copy has no performance impact on the existing database.</span></span>

> [!TIP]
> <span data-ttu-id="24fa2-118">Практическое руководство см. в статье [Настройка долгосрочного хранения резервных копий для базы данных SQL Azure и восстановление из резервной копии](sql-database-long-term-backup-retention-configure.md).</span><span class="sxs-lookup"><span data-stu-id="24fa2-118">For a how-to guide, see [Configure and restore from Azure SQL Database long-term backup retention](sql-database-long-term-backup-retention-configure.md).</span></span>

## <a name="enable-long-term-backup-retention"></a><span data-ttu-id="24fa2-119">Включение долгосрочного хранения резервных копий</span><span class="sxs-lookup"><span data-stu-id="24fa2-119">Enable long-term backup retention</span></span>

<span data-ttu-id="24fa2-120">Чтобы настроить долгосрочное хранение резервной копии для базы данных, выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="24fa2-120">To configure long-term backup retention for a database:</span></span>

1. <span data-ttu-id="24fa2-121">Создайте хранилище служб восстановления Azure в том же регионе, той же подписке и той же группе ресурсов, где был создан сервер базы данных SQL.</span><span class="sxs-lookup"><span data-stu-id="24fa2-121">Create an Azure Recovery Services vault in the same region, subscription, and resource group as your SQL database server.</span></span> 
2. <span data-ttu-id="24fa2-122">Зарегистрируйте сервер в хранилище.</span><span class="sxs-lookup"><span data-stu-id="24fa2-122">Register the server to the vault.</span></span>
3. <span data-ttu-id="24fa2-123">Создайте политику защиты служб восстановления Azure.</span><span class="sxs-lookup"><span data-stu-id="24fa2-123">Create an Azure Recovery Services protection policy.</span></span>
4. <span data-ttu-id="24fa2-124">Примените политику защиты к базе данных, для которой вам требуется долгосрочное хранение резервных копий.</span><span class="sxs-lookup"><span data-stu-id="24fa2-124">Apply the protection policy to the databases that require long-term backup retention.</span></span>

<span data-ttu-id="24fa2-125">Для настройки, управления и восстановления базы данных с помощью долгосрочного хранения создаваемых автоматически резервных копий в хранилище служб восстановления Azure можно использовать один из вариантов.</span><span class="sxs-lookup"><span data-stu-id="24fa2-125">To configure, manage, and restore a database from long-term backup retention of automated backups in an Azure Recovery Services vault, do either of the following:</span></span>

* <span data-ttu-id="24fa2-126">С помощью портала Azure: выберите **Долгосрочное хранение резервных копий**, выберите базу данных и нажмите кнопку **Настроить**.</span><span class="sxs-lookup"><span data-stu-id="24fa2-126">Using the Azure portal: Click **Long-term backup retention**, select a database, and then click **Configure**.</span></span> 

   ![Выбор базы данных для настройки долгосрочного хранения резервных копий](./media/sql-database-get-started-backup-recovery/select-database-for-long-term-backup-retention.png)

* <span data-ttu-id="24fa2-128">С помощью PowerShell: см. статью [Настройка долгосрочного хранения резервных копий для базы данных SQL Azure и восстановление из резервной копии](sql-database-long-term-backup-retention-configure.md).</span><span class="sxs-lookup"><span data-stu-id="24fa2-128">Using PowerShell: Go to [Configure and restore from Azure SQL Database long-term backup retention](sql-database-long-term-backup-retention-configure.md).</span></span>

## <a name="restore-a-database-thats-stored-with-the-long-term-backup-retention-feature"></a><span data-ttu-id="24fa2-129">Восстановление базы данных, сохраненной с помощью функции долгосрочного хранения резервных копий</span><span class="sxs-lookup"><span data-stu-id="24fa2-129">Restore a database that's stored with the long-term backup retention feature</span></span>

<span data-ttu-id="24fa2-130">Для восстановления из резервной копии долгосрочного хранения сделайте следующее.</span><span class="sxs-lookup"><span data-stu-id="24fa2-130">To recover from a long-term backup retention backup:</span></span>

1. <span data-ttu-id="24fa2-131">Получите список содержимого хранилища, в котором хранится резервная копия.</span><span class="sxs-lookup"><span data-stu-id="24fa2-131">List the vault where the backup is stored.</span></span>
2. <span data-ttu-id="24fa2-132">Получите список содержимого контейнера, который сопоставлен с нужным логическим сервером.</span><span class="sxs-lookup"><span data-stu-id="24fa2-132">List the container that is mapped to your logical server.</span></span>
3. <span data-ttu-id="24fa2-133">Получите список содержимого источника данных в хранилище, которое сопоставлено с нужной базой данных.</span><span class="sxs-lookup"><span data-stu-id="24fa2-133">List the data source within the vault that is mapped to your database.</span></span>
4. <span data-ttu-id="24fa2-134">Получите список точек восстановления, доступных для восстановления.</span><span class="sxs-lookup"><span data-stu-id="24fa2-134">List the recovery points that are available to restore.</span></span>
5. <span data-ttu-id="24fa2-135">Выполните восстановление базы данных из подходящей точки восстановления на целевой сервер в вашей подписке.</span><span class="sxs-lookup"><span data-stu-id="24fa2-135">Restore the database from the recovery point to the target server within your subscription.</span></span>

<span data-ttu-id="24fa2-136">Для настройки, управления и восстановления базы данных с помощью долгосрочного хранения создаваемых автоматически резервных копий в хранилище служб восстановления Azure можно использовать один из вариантов.</span><span class="sxs-lookup"><span data-stu-id="24fa2-136">To configure, manage, and restore a database from long-term backup retention of automated backups in an Azure Recovery Services vault, do either of the following:</span></span>

* <span data-ttu-id="24fa2-137">С помощью портала Azure: см. статью [Управление долгосрочным хранением резервных копий с помощью портала Azure](sql-database-long-term-backup-retention-configure.md).</span><span class="sxs-lookup"><span data-stu-id="24fa2-137">Using the Azure portal: Go to [Manage long-term backup retention using the Azure portal](sql-database-long-term-backup-retention-configure.md).</span></span> 

* <span data-ttu-id="24fa2-138">С помощью PowerShell: см. статью [Управление долгосрочным хранением резервных копий с помощью PowerShell](sql-database-long-term-backup-retention-configure.md).</span><span class="sxs-lookup"><span data-stu-id="24fa2-138">Using PowerShell: Go to [Manage long-term backup retention using PowerShell](sql-database-long-term-backup-retention-configure.md).</span></span>

## <a name="get-pricing-for-long-term-backup-retention"></a><span data-ttu-id="24fa2-139">Получение расценок для настройки долгосрочного хранения резервных копий</span><span class="sxs-lookup"><span data-stu-id="24fa2-139">Get pricing for long-term backup retention</span></span>

<span data-ttu-id="24fa2-140">Плата за долгосрочное хранение резервных копий базы данных SQL взимается в соответствии с [ценами на службу архивации Azure](https://azure.microsoft.com/pricing/details/backup/).</span><span class="sxs-lookup"><span data-stu-id="24fa2-140">Long-term backup retention of a SQL database is charged according to the [Azure backup services pricing rates](https://azure.microsoft.com/pricing/details/backup/).</span></span>

<span data-ttu-id="24fa2-141">С момента регистрации сервера базы данных SQL в хранилище с вас будет взиматься плата за общий объем хранилища, используемый для хранения еженедельных резервных копий.</span><span class="sxs-lookup"><span data-stu-id="24fa2-141">After the SQL database server is registered to the vault, you are charged for the total storage that's used by the weekly backups stored in the vault.</span></span>

## <a name="view-available-backups-that-are-stored-in-long-term-backup-retention"></a><span data-ttu-id="24fa2-142">Просмотр доступных резервных копий, хранимых в службе долгосрочного хранения</span><span class="sxs-lookup"><span data-stu-id="24fa2-142">View available backups that are stored in long-term backup retention</span></span>

<span data-ttu-id="24fa2-143">Для настройки, управления и восстановления базы данных с помощью долгосрочного хранения создаваемых автоматически резервных копий в хранилище служб восстановления можно использовать один из вариантов.</span><span class="sxs-lookup"><span data-stu-id="24fa2-143">To configure, manage, and restore a database from long-term backup retention of automated backups in an Azure Recovery Services vault by using the Azure portal, do either of the following:</span></span>

* <span data-ttu-id="24fa2-144">С помощью портала Azure: см. статью [Управление долгосрочным хранением резервных копий с помощью портала Azure](sql-database-long-term-backup-retention-configure.md).</span><span class="sxs-lookup"><span data-stu-id="24fa2-144">Using the Azure portal: Go to [Manage long-term backup retention using the Azure portal](sql-database-long-term-backup-retention-configure.md).</span></span> 

* <span data-ttu-id="24fa2-145">С помощью PowerShell: см. статью [Управление долгосрочным хранением резервных копий с помощью PowerShell](sql-database-long-term-backup-retention-configure.md).</span><span class="sxs-lookup"><span data-stu-id="24fa2-145">Using PowerShell: Go to [Manage long-term backup retention using PowerShell](sql-database-long-term-backup-retention-configure.md).</span></span>

## <a name="disable-long-term-retention"></a><span data-ttu-id="24fa2-146">Отключение долгосрочного хранения</span><span class="sxs-lookup"><span data-stu-id="24fa2-146">Disable long-term retention</span></span>

<span data-ttu-id="24fa2-147">Служба восстановления автоматически очищает резервные копии в соответствии с настроенной политикой хранения.</span><span class="sxs-lookup"><span data-stu-id="24fa2-147">The recovery service automatically handles the cleanup of backups based on the provided retention policy.</span></span> 

<span data-ttu-id="24fa2-148">Чтобы резервные копии определенной базы данных больше не отправлялись в хранилище, удалите политику хранения для этой базы данных.</span><span class="sxs-lookup"><span data-stu-id="24fa2-148">To stop sending the backups for a specific database to the vault, remove the retention policy for that database.</span></span>
  
```
Set-AzureRmSqlDatabaseBackupLongTermRetentionPolicy -ResourceGroupName 'RG1' -ServerName 'Server1' -DatabaseName 'DB1' -State 'Disabled' -ResourceId $policy.Id
```

> [!NOTE]
> <span data-ttu-id="24fa2-149">Резервные копии, которые уже находятся в хранилище, не затрагиваются.</span><span class="sxs-lookup"><span data-stu-id="24fa2-149">The backups that are already in the vault are unaffected.</span></span> <span data-ttu-id="24fa2-150">Они будут автоматически удалены службой восстановления по истечении указанного срока хранения.</span><span class="sxs-lookup"><span data-stu-id="24fa2-150">They are automatically deleted by the recovery service when their retention period expires.</span></span>

## <a name="long-term-backup-retention-faq"></a><span data-ttu-id="24fa2-151">Часто задаваемые вопросы о долгосрочном хранении резервных копий</span><span class="sxs-lookup"><span data-stu-id="24fa2-151">Long-term backup retention FAQ</span></span>

<span data-ttu-id="24fa2-152">**Можно ли вручную удалить из хранилища определенные резервные копии?**</span><span class="sxs-lookup"><span data-stu-id="24fa2-152">**Can I manually delete specific backups in the vault?**</span></span>

<span data-ttu-id="24fa2-153">В настоящее время нет.</span><span class="sxs-lookup"><span data-stu-id="24fa2-153">Not currently.</span></span> <span data-ttu-id="24fa2-154">Хранилище автоматически удаляет резервные копии по истечении периода хранения.</span><span class="sxs-lookup"><span data-stu-id="24fa2-154">The vault automatically cleans up backups when the retention period has expired.</span></span>

<span data-ttu-id="24fa2-155">**Можно ли зарегистрировать сервер в нескольких хранилищах для хранения резервных копий?**</span><span class="sxs-lookup"><span data-stu-id="24fa2-155">**Can I register my server to store backups to more than one vault?**</span></span>

<span data-ttu-id="24fa2-156">Пока нет. Сейчас можно сохранять резервные копии только в одном хранилище.</span><span class="sxs-lookup"><span data-stu-id="24fa2-156">No, you can currently store backups to only one vault at a time.</span></span>

<span data-ttu-id="24fa2-157">**Можно ли использовать хранилище и сервер из разных подписок?**</span><span class="sxs-lookup"><span data-stu-id="24fa2-157">**Can I have a vault and server in different subscriptions?**</span></span>

<span data-ttu-id="24fa2-158">Нет. Сейчас хранилище и сервер должны находиться в одной подписке и в одной группе ресурсов.</span><span class="sxs-lookup"><span data-stu-id="24fa2-158">No, currently the vault and server must be in the same subscription and resource group.</span></span>

<span data-ttu-id="24fa2-159">**Можно ли использовать хранилище, созданное не в том регионе, где расположен мой сервер?**</span><span class="sxs-lookup"><span data-stu-id="24fa2-159">**Can I use a vault that I created in a region that's different from my server’s region?**</span></span>

<span data-ttu-id="24fa2-160">Нет, хранилище и сервер должны находиться в одном регионе, чтобы сократить время копирования и избежать расходов на трафик.</span><span class="sxs-lookup"><span data-stu-id="24fa2-160">No, the vault and server must be in the same region to minimize copy time and avoid traffic charges.</span></span>

<span data-ttu-id="24fa2-161">**Сколько баз данных можно хранить в одном хранилище?**</span><span class="sxs-lookup"><span data-stu-id="24fa2-161">**How many databases can I store in one vault?**</span></span>

<span data-ttu-id="24fa2-162">Сейчас поддерживается не более 1000 баз данных на одно хранилище.</span><span class="sxs-lookup"><span data-stu-id="24fa2-162">Currently, we support up to 1,000 databases per vault.</span></span> 

<span data-ttu-id="24fa2-163">**Сколько хранилищ можно создать в одной подписке?**</span><span class="sxs-lookup"><span data-stu-id="24fa2-163">**How many vaults can I create per subscription?**</span></span>

<span data-ttu-id="24fa2-164">В одной подписке можно создать до 25 хранилищ.</span><span class="sxs-lookup"><span data-stu-id="24fa2-164">You can create up to 25 vaults per subscription.</span></span>

<span data-ttu-id="24fa2-165">**Сколько баз данных можно настроить для одного хранилища в день?**</span><span class="sxs-lookup"><span data-stu-id="24fa2-165">**How many databases can I configure per day per vault?**</span></span>

<span data-ttu-id="24fa2-166">Для одного хранилища можно настроить не более 200 баз данных в день.</span><span class="sxs-lookup"><span data-stu-id="24fa2-166">You can set up 200 databases per day per vault.</span></span>

<span data-ttu-id="24fa2-167">**Работает ли долгосрочное хранение резервных копий с эластичными пулами?**</span><span class="sxs-lookup"><span data-stu-id="24fa2-167">**Does long-term backup retention work with elastic pools?**</span></span>

<span data-ttu-id="24fa2-168">Да.</span><span class="sxs-lookup"><span data-stu-id="24fa2-168">Yes.</span></span> <span data-ttu-id="24fa2-169">Политику хранения можно настроить для любой базы данных в пуле.</span><span class="sxs-lookup"><span data-stu-id="24fa2-169">Any database in the pool can be configured with the retention policy.</span></span>

<span data-ttu-id="24fa2-170">**Можно ли выбрать время создания резервной копии?**</span><span class="sxs-lookup"><span data-stu-id="24fa2-170">**Can I choose the time at which the backup is created?**</span></span>

<span data-ttu-id="24fa2-171">Нет, расписанием архивации управляет база данных SQL. Это нужно для того, чтобы минимизировать влияние на производительность баз данных.</span><span class="sxs-lookup"><span data-stu-id="24fa2-171">No, SQL Database controls the backup schedule to minimize the performance impact on your databases.</span></span>

<span data-ttu-id="24fa2-172">**Для нашей базы данных включено прозрачное шифрование данных. Можно ли использовать для нее хранилище?**</span><span class="sxs-lookup"><span data-stu-id="24fa2-172">**I have transparent data encryption enabled for my database. Can I use it with the vault?**</span></span> 

<span data-ttu-id="24fa2-173">Да, прозрачное шифрование данных поддерживается.</span><span class="sxs-lookup"><span data-stu-id="24fa2-173">Yes, transparent data encryption is supported.</span></span> <span data-ttu-id="24fa2-174">Вы сможете восстановить базу данных из хранилища, даже если исходной базы данных уже не существует.</span><span class="sxs-lookup"><span data-stu-id="24fa2-174">You can restore the database from the vault even if the original database no longer exists.</span></span>

<span data-ttu-id="24fa2-175">**Что произойдет с резервными копиями в хранилище, если моя подписка будет приостановлена?**</span><span class="sxs-lookup"><span data-stu-id="24fa2-175">**What happens with the backups in the vault if my subscription is suspended?**</span></span> 

<span data-ttu-id="24fa2-176">Если подписка приостановлена, мы храним все имеющиеся базы данных и резервные копии.</span><span class="sxs-lookup"><span data-stu-id="24fa2-176">If your subscription is suspended, we retain the existing databases and backups.</span></span> <span data-ttu-id="24fa2-177">Однако новые резервные копии не сохраняются в хранилище.</span><span class="sxs-lookup"><span data-stu-id="24fa2-177">New backups are not copied to the vault.</span></span> <span data-ttu-id="24fa2-178">Когда вы повторно активируете подписку, служба возобновит сохранение резервных копий в хранилище.</span><span class="sxs-lookup"><span data-stu-id="24fa2-178">After you reactivate the subscription, the service resumes copying backups to the vault.</span></span> <span data-ttu-id="24fa2-179">Хранилище станет доступным для операций восстановления с использованием тех резервных копий, которые были созданы до приостановки подписки.</span><span class="sxs-lookup"><span data-stu-id="24fa2-179">Your vault becomes accessible to the restore operations by using the backups that were copied there before the subscription was suspended.</span></span> 

<span data-ttu-id="24fa2-180">**Можно ли получить доступ к файлам резервных копий базы данных SQL, чтобы скачать или восстановить их в экземпляр SQL Server?**</span><span class="sxs-lookup"><span data-stu-id="24fa2-180">**Can I get access to the SQL database backup files so I can download or restore them to the SQL server?**</span></span>

<span data-ttu-id="24fa2-181">В настоящее время это невозможно.</span><span class="sxs-lookup"><span data-stu-id="24fa2-181">No, not currently.</span></span>

<span data-ttu-id="24fa2-182">**Можно ли создать несколько расписаний (ежедневно, еженедельно, ежемесячно, ежегодно) в рамках политики хранения SQL?**</span><span class="sxs-lookup"><span data-stu-id="24fa2-182">**Is it possible to have multiple schedules (daily, weekly, monthly, yearly) within a SQL retention policy.**</span></span>

<span data-ttu-id="24fa2-183">Нет, несколько расписаний пока доступны только для резервных копий виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="24fa2-183">No, multiple schedules are currently available only for virtual machine backups.</span></span>

<span data-ttu-id="24fa2-184">**Мы настроили долгосрочное хранение резервных копий для базы данных, которая является базой данных-получателем с активной георепликацией. Поддерживается ли такая конфигурация?**</span><span class="sxs-lookup"><span data-stu-id="24fa2-184">**What if we set up long-term backup retention on a database that is an active geo-replication secondary database?**</span></span>

<span data-ttu-id="24fa2-185">Поскольку резервное копирование на репликах не выполняется, долгосрочное хранение резервных копий в базах данных-получателях пока не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="24fa2-185">Because we don't take backups on replicas, there is currently no option for long-term backup retention on secondary databases.</span></span> <span data-ttu-id="24fa2-186">Тем не менее пользователям важно настроить долгосрочное хранение резервных копий в базе данных-получателе с активной георепликацией по следующим причинам:</span><span class="sxs-lookup"><span data-stu-id="24fa2-186">However, it is important for users to set up long-term backup retention on an active geo-replication secondary database for these reasons:</span></span>
* <span data-ttu-id="24fa2-187">Если при отработке отказа база данных становится базой данных-источником, создается полная резервная копия, которая будет отправлена в хранилище.</span><span class="sxs-lookup"><span data-stu-id="24fa2-187">When a failover happens and the database becomes a primary database, we take a full backup, which is uploaded to vault.</span></span>
* <span data-ttu-id="24fa2-188">Настройка долгосрочного хранения резервных копий в базе данных-получателе не требует дополнительной оплаты.</span><span class="sxs-lookup"><span data-stu-id="24fa2-188">There is no extra cost to the customer for setting up long-term backup retention on a secondary database.</span></span>

## <a name="next-steps"></a><span data-ttu-id="24fa2-189">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="24fa2-189">Next steps</span></span>
<span data-ttu-id="24fa2-190">Поскольку резервные копии базы данных защищают данные от случайного повреждения или удаления, они являются важной частью любой стратегии непрерывности бизнес-процессов и аварийного восстановления.</span><span class="sxs-lookup"><span data-stu-id="24fa2-190">Because database backups protect data from accidental corruption or deletion, they're an essential part of any business continuity and disaster recovery strategy.</span></span> <span data-ttu-id="24fa2-191">Дополнительные сведения о других решениях для базы данных SQL, обеспечивающих непрерывность бизнес-процессов, см. в статье [Обзор обеспечения непрерывности бизнес-процессов с помощью базы данных SQL Azure](sql-database-business-continuity.md).</span><span class="sxs-lookup"><span data-stu-id="24fa2-191">To learn about the other SQL Database business-continuity solutions, see [Business continuity overview](sql-database-business-continuity.md).</span></span>
