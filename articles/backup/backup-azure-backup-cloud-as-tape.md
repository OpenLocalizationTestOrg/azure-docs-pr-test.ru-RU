---
title: "резервное копирование Azure tooreplace aaaUse инфраструктуры ленты | Документы Microsoft"
description: "Узнайте, как резервное копирование Azure обеспечивает семантику like ленту, которая позволяет toobackup и восстановления данных в Azure"
services: backup
documentationcenter: 
author: trinadhk
manager: vijayts
editor: 
ms.assetid: 2e1bb67d-986c-4437-8056-3a63169b4214
ms.service: backup
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 1/10/2017
ms.author: saurse;trinadhk;markgal
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 4c5b095d95d39267c54b1eed9427bda09658bb94
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="move-your-long-term-storage-from-tape-toohello-azure-cloud"></a><span data-ttu-id="a7e45-103">Переместить в долговременном хранилище из ленты toohello облако Azure</span><span class="sxs-lookup"><span data-stu-id="a7e45-103">Move your long-term storage from tape toohello Azure cloud</span></span>
<span data-ttu-id="a7e45-104">Пользователи службы архивации Azure и System Center Data Protection Manager могут:</span><span class="sxs-lookup"><span data-stu-id="a7e45-104">Azure Backup and System Center Data Protection Manager customers can:</span></span>

* <span data-ttu-id="a7e45-105">Резервное копирование данных в отчетах, которые лучше всего соответствует требованиям организации hello.</span><span class="sxs-lookup"><span data-stu-id="a7e45-105">Back up data in schedules which best suit hello organizational needs.</span></span>
* <span data-ttu-id="a7e45-106">Hello резервной копии данные сохраняются в течение более длительного</span><span class="sxs-lookup"><span data-stu-id="a7e45-106">Retain hello backup data for longer periods</span></span>
* <span data-ttu-id="a7e45-107">сделать Azure одним из средств длительного хранения данных (вместо магнитных лент).</span><span class="sxs-lookup"><span data-stu-id="a7e45-107">Make Azure a part of their long-term retention needs (instead of tape).</span></span>

<span data-ttu-id="a7e45-108">В этой статье объясняется, как клиенты могут активировать политики резервного копирования и хранения.</span><span class="sxs-lookup"><span data-stu-id="a7e45-108">This article explains how customers can enable backup and retention policies.</span></span> <span data-ttu-id="a7e45-109">Пользователи, использующие tooaddress лент их полном-term хранения должен теперь имеют мощные и жизнеспособности вариант с доступностью hello этой функции.</span><span class="sxs-lookup"><span data-stu-id="a7e45-109">Customers who use tapes tooaddress their long-term-retention needs now have a powerful and viable alternative with hello availability of this feature.</span></span> <span data-ttu-id="a7e45-110">Hello включена в последнем выпуске hello hello Azure Backup (доступный [здесь](http://aka.ms/azurebackup_agent)).</span><span class="sxs-lookup"><span data-stu-id="a7e45-110">hello feature is enabled in hello latest release of hello Azure Backup (which is available [here](http://aka.ms/azurebackup_agent)).</span></span> <span data-ttu-id="a7e45-111">Необходимо выполнить обновление до System Center DPM клиентов, по крайней мере, DPM 2012 R2 UR5 перед использованием DPM с hello службы архивации Azure.</span><span class="sxs-lookup"><span data-stu-id="a7e45-111">System Center DPM customers must update to, at least, DPM 2012 R2 UR5 before using DPM with hello Azure Backup service.</span></span>

## <a name="what-is-hello-backup-schedule"></a><span data-ttu-id="a7e45-112">Что такое hello расписания архивации</span><span class="sxs-lookup"><span data-stu-id="a7e45-112">What is hello Backup Schedule?</span></span>
<span data-ttu-id="a7e45-113">расписание резервного копирования Hello указывает частоту hello hello операции резервного копирования.</span><span class="sxs-lookup"><span data-stu-id="a7e45-113">hello backup schedule indicates hello frequency of hello backup operation.</span></span> <span data-ttu-id="a7e45-114">Например параметры hello в следующий экран приветствия указывают, что резервные копии создаются ежедневно в 18: 00 и в полночь.</span><span class="sxs-lookup"><span data-stu-id="a7e45-114">For example, hello settings in hello following screen indicate that backups are taken daily at 6pm and at midnight.</span></span>

![Ежедневное расписание](./media/backup-azure-backup-cloud-as-tape/dailybackupschedule.png)

<span data-ttu-id="a7e45-116">Создание резервных копий может быть и еженедельным.</span><span class="sxs-lookup"><span data-stu-id="a7e45-116">Customers can also schedule a weekly backup.</span></span> <span data-ttu-id="a7e45-117">Например hello параметры в следующий экран приветствия указывают, что резервные копии создаются каждый вариант воскресенье & среду в 9:30:00 и 1:00 AM.</span><span class="sxs-lookup"><span data-stu-id="a7e45-117">For example, hello settings in hello following screen indicate that backups are taken every alternate Sunday & Wednesday at 9:30AM and 1:00AM.</span></span>

![Еженедельное расписание](./media/backup-azure-backup-cloud-as-tape/weeklybackupschedule.png)

## <a name="what-is-hello-retention-policy"></a><span data-ttu-id="a7e45-119">Что такое hello политики хранения?</span><span class="sxs-lookup"><span data-stu-id="a7e45-119">What is hello Retention Policy?</span></span>
<span data-ttu-id="a7e45-120">Политика хранения Hello указывает длительность hello, для которого должны храниться hello резервного копирования.</span><span class="sxs-lookup"><span data-stu-id="a7e45-120">hello retention policy specifies hello duration for which hello backup must be stored.</span></span> <span data-ttu-id="a7e45-121">Вместо того чтобы просто задавать «плоский политика» для всех точек резервного копирования, клиенты могут указывать на основе политик хранения различных при hello резервная копия.</span><span class="sxs-lookup"><span data-stu-id="a7e45-121">Rather than just specifying a “flat policy” for all backup points, customers can specify different retention policies based on when hello backup is taken.</span></span> <span data-ttu-id="a7e45-122">Например hello точки резервного копирования копии ежедневно, который служит в качестве точки оперативного восстановления сохраняется 90 дней.</span><span class="sxs-lookup"><span data-stu-id="a7e45-122">For example, hello backup point taken daily, which serves as an operational recovery point, is preserved for 90 days.</span></span> <span data-ttu-id="a7e45-123">Hello точки резервного копирования, которое выполняется в конце каждого квартала для целей аудита в hello сохраняется длительный срок.</span><span class="sxs-lookup"><span data-stu-id="a7e45-123">hello backup point taken at hello end of each quarter for audit purposes is preserved for a longer duration.</span></span>

![Политика хранения](./media/backup-azure-backup-cloud-as-tape/retentionpolicy.png)

<span data-ttu-id="a7e45-125">Hello общее число «хранения точек» этой политики — 90 (ежедневных точек) + 40 (одному для каждого квартала для 10 лет) = 130.</span><span class="sxs-lookup"><span data-stu-id="a7e45-125">hello total number of “retention points” specified in this policy is 90 (daily points) + 40 (one each quarter for 10 years) = 130.</span></span>

## <a name="example--putting-both-together"></a><span data-ttu-id="a7e45-126">Пример объединения обеих точек восстановления</span><span class="sxs-lookup"><span data-stu-id="a7e45-126">Example – Putting both together</span></span>
![Образец экрана](./media/backup-azure-backup-cloud-as-tape/samplescreen.png)

1. <span data-ttu-id="a7e45-128">**Ежедневная политика хранения.** Резервные копии, создаваемые ежедневно, хранятся в течение семи дней.</span><span class="sxs-lookup"><span data-stu-id="a7e45-128">**Daily retention policy**: Backups taken daily are stored for seven days.</span></span>
2. <span data-ttu-id="a7e45-129">**Еженедельная политика хранения.** Резервные копии, создаваемые каждый день в полночь и каждую субботу в 18:00, хранятся в течение четырех недель.</span><span class="sxs-lookup"><span data-stu-id="a7e45-129">**Weekly retention policy**: Backups taken every day at midnight and 6PM Saturday are preserved for four weeks</span></span>
3. <span data-ttu-id="a7e45-130">**Ежемесячные политики хранения**: резервные копии, созданные в полночь и 18: 00 на hello суббота Последний день каждого месяца, сохраняются за 12 месяцев</span><span class="sxs-lookup"><span data-stu-id="a7e45-130">**Monthly retention policy**: Backups taken at midnight and 6pm on hello last Saturday of each month are preserved for 12 months</span></span>
4. <span data-ttu-id="a7e45-131">**Ежегодно политики хранения**: резервные копии, созданные в полночь hello Последняя суббота марта каждого сохраняются 10 лет</span><span class="sxs-lookup"><span data-stu-id="a7e45-131">**Yearly retention policy**: Backups taken at midnight on hello last Saturday of every March are preserved for 10 years</span></span>

<span data-ttu-id="a7e45-132">Здравствуйте, «точки сохранения» общее количество (точки, из которых клиент может восстановить данные) в hello предыдущей диаграмме вычисляется следующим образом:</span><span class="sxs-lookup"><span data-stu-id="a7e45-132">hello total number of “retention points” (points from which a customer can restore data) in hello preceding diagram is computed as follows:</span></span>

* <span data-ttu-id="a7e45-133">две точки в день в течение 7 дней = 14 точек восстановления;</span><span class="sxs-lookup"><span data-stu-id="a7e45-133">two points per day for seven days = 14 recovery points</span></span>
* <span data-ttu-id="a7e45-134">две точки в неделю в течение 4 недель = 8 точек восстановления;</span><span class="sxs-lookup"><span data-stu-id="a7e45-134">two points per week for four weeks = 8 recovery points</span></span>
* <span data-ttu-id="a7e45-135">две точки в месяц в течение 12 месяцев = 24 точки восстановления;</span><span class="sxs-lookup"><span data-stu-id="a7e45-135">two points per month for 12 months = 24 recovery points</span></span>
* <span data-ttu-id="a7e45-136">одна точка в год в течение 10 лет = 10 точек восстановления.</span><span class="sxs-lookup"><span data-stu-id="a7e45-136">one point per year per 10 years = 10 recovery points</span></span>

<span data-ttu-id="a7e45-137">Общее количество точек восстановления для Hello равно 56.</span><span class="sxs-lookup"><span data-stu-id="a7e45-137">hello total number of recovery points is 56.</span></span>

> [!NOTE]
> <span data-ttu-id="a7e45-138">У службы архивации Azure нет ограничений на количество точек восстановления.</span><span class="sxs-lookup"><span data-stu-id="a7e45-138">Azure backup doesn't have a restriction on number of recovery points.</span></span>
>
>

## <a name="advanced-configuration"></a><span data-ttu-id="a7e45-139">Расширенная конфигурация</span><span class="sxs-lookup"><span data-stu-id="a7e45-139">Advanced configuration</span></span>
<span data-ttu-id="a7e45-140">Щелкнув **изменить** в предшествующих экрана приветствия, клиенты имеют дополнительные гибкость при определении расписания хранения.</span><span class="sxs-lookup"><span data-stu-id="a7e45-140">By clicking **Modify** in hello preceding screen, customers have further flexibility in specifying retention schedules.</span></span>

![Изменить](./media/backup-azure-backup-cloud-as-tape/modify.png)

## <a name="next-steps"></a><span data-ttu-id="a7e45-142">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="a7e45-142">Next Steps</span></span>
<span data-ttu-id="a7e45-143">Дополнительные сведения о службе архивации Azure см. в статьях:</span><span class="sxs-lookup"><span data-stu-id="a7e45-143">For more information about Azure Backup, see:</span></span>

* [<span data-ttu-id="a7e45-144">Введение tooAzure резервной копии</span><span class="sxs-lookup"><span data-stu-id="a7e45-144">Introduction tooAzure Backup</span></span>](backup-introduction-to-azure-backup.md)
* [<span data-ttu-id="a7e45-145">Знакомство со службой архивации Azure</span><span class="sxs-lookup"><span data-stu-id="a7e45-145">Try Azure Backup</span></span>](backup-try-azure-backup-in-10-mins.md)
