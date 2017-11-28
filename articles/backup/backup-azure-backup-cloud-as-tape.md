---
title: "Использование службы архивации Azure для замены инфраструктуры ленточных накопителей | Документация Майкрософт"
description: "Узнайте, как служба архивации Azure предоставляет ленточную семантику, которая дает возможность выполнять резервное копирование и восстановление данных в Azure"
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
ms.openlocfilehash: f0f3152daf5f91f7c9e540797bf09b21969d2d33
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="move-your-long-term-storage-from-tape-to-the-azure-cloud"></a><span data-ttu-id="111d6-103">Перенос долгосрочного хранения данных с магнитной ленты в облако Azure</span><span class="sxs-lookup"><span data-stu-id="111d6-103">Move your long-term storage from tape to the Azure cloud</span></span>
<span data-ttu-id="111d6-104">Пользователи службы архивации Azure и System Center Data Protection Manager могут:</span><span class="sxs-lookup"><span data-stu-id="111d6-104">Azure Backup and System Center Data Protection Manager customers can:</span></span>

* <span data-ttu-id="111d6-105">создавать резервные копии данных по расписанию, которое лучше всего соответствует потребностям организации;</span><span class="sxs-lookup"><span data-stu-id="111d6-105">Back up data in schedules which best suit the organizational needs.</span></span>
* <span data-ttu-id="111d6-106">хранить резервные копии данных в течение более длительного времени;</span><span class="sxs-lookup"><span data-stu-id="111d6-106">Retain the backup data for longer periods</span></span>
* <span data-ttu-id="111d6-107">сделать Azure одним из средств длительного хранения данных (вместо магнитных лент).</span><span class="sxs-lookup"><span data-stu-id="111d6-107">Make Azure a part of their long-term retention needs (instead of tape).</span></span>

<span data-ttu-id="111d6-108">В этой статье объясняется, как клиенты могут активировать политики резервного копирования и хранения.</span><span class="sxs-lookup"><span data-stu-id="111d6-108">This article explains how customers can enable backup and retention policies.</span></span> <span data-ttu-id="111d6-109">У клиентов, использующих для длительного хранения магнитные ленты, теперь появилась мощная и эффективная альтернатива.</span><span class="sxs-lookup"><span data-stu-id="111d6-109">Customers who use tapes to address their long-term-retention needs now have a powerful and viable alternative with the availability of this feature.</span></span> <span data-ttu-id="111d6-110">Эта функция активирована в последнем выпуске службы архивации Azure (доступен [здесь](http://aka.ms/azurebackup_agent)).</span><span class="sxs-lookup"><span data-stu-id="111d6-110">The feature is enabled in the latest release of the Azure Backup (which is available [here](http://aka.ms/azurebackup_agent)).</span></span> <span data-ttu-id="111d6-111">Клиентам, использующим решение System Center DPM, необходимо обновить его по крайней мере до DPM 2012 R2 UR5, прежде чем использовать DPM в службе архивации Azure.</span><span class="sxs-lookup"><span data-stu-id="111d6-111">System Center DPM customers must update to, at least, DPM 2012 R2 UR5 before using DPM with the Azure Backup service.</span></span>

## <a name="what-is-the-backup-schedule"></a><span data-ttu-id="111d6-112">Что такое расписание резервного копирования</span><span class="sxs-lookup"><span data-stu-id="111d6-112">What is the Backup Schedule?</span></span>
<span data-ttu-id="111d6-113">Расписание резервного копирования определяет частоту выполнения операции резервного копирования.</span><span class="sxs-lookup"><span data-stu-id="111d6-113">The backup schedule indicates the frequency of the backup operation.</span></span> <span data-ttu-id="111d6-114">Например, параметры на показанном ниже экране означают, что резервные копии будут создаваться каждый день в 18:00 и в полночь.</span><span class="sxs-lookup"><span data-stu-id="111d6-114">For example, the settings in the following screen indicate that backups are taken daily at 6pm and at midnight.</span></span>

![Ежедневное расписание](./media/backup-azure-backup-cloud-as-tape/dailybackupschedule.png)

<span data-ttu-id="111d6-116">Создание резервных копий может быть и еженедельным.</span><span class="sxs-lookup"><span data-stu-id="111d6-116">Customers can also schedule a weekly backup.</span></span> <span data-ttu-id="111d6-117">Например, параметры на показанном ниже экране означают, что резервные копии будут создаваться каждую среду и воскресенье в 09:30 и в 01:00.</span><span class="sxs-lookup"><span data-stu-id="111d6-117">For example, the settings in the following screen indicate that backups are taken every alternate Sunday & Wednesday at 9:30AM and 1:00AM.</span></span>

![Еженедельное расписание](./media/backup-azure-backup-cloud-as-tape/weeklybackupschedule.png)

## <a name="what-is-the-retention-policy"></a><span data-ttu-id="111d6-119">Что такое политика хранения?</span><span class="sxs-lookup"><span data-stu-id="111d6-119">What is the Retention Policy?</span></span>
<span data-ttu-id="111d6-120">Политика хранения определяет время, в течение которого должна храниться резервная копия.</span><span class="sxs-lookup"><span data-stu-id="111d6-120">The retention policy specifies the duration for which the backup must be stored.</span></span> <span data-ttu-id="111d6-121">Вместо того, чтобы настраивать одну политику для всех точек резервного копирования, клиенты могут настроить разные политики хранения на основе времени создания резервной копии.</span><span class="sxs-lookup"><span data-stu-id="111d6-121">Rather than just specifying a “flat policy” for all backup points, customers can specify different retention policies based on when the backup is taken.</span></span> <span data-ttu-id="111d6-122">Например, точка ежедневной архивации (которая служит точкой оперативного восстановления) хранится в течение 90 дней.</span><span class="sxs-lookup"><span data-stu-id="111d6-122">For example, the backup point taken daily, which serves as an operational recovery point, is preserved for 90 days.</span></span> <span data-ttu-id="111d6-123">Точка архивации, создаваемая в конце каждого квартала для аудита, хранится дольше.</span><span class="sxs-lookup"><span data-stu-id="111d6-123">The backup point taken at the end of each quarter for audit purposes is preserved for a longer duration.</span></span>

![Политика хранения](./media/backup-azure-backup-cloud-as-tape/retentionpolicy.png)

<span data-ttu-id="111d6-125">Общее число точек хранения, указанное в этой политике, равно 90 (ежедневные точки) + 40 (одна для каждого квартала в течение 10 лет) = 130.</span><span class="sxs-lookup"><span data-stu-id="111d6-125">The total number of “retention points” specified in this policy is 90 (daily points) + 40 (one each quarter for 10 years) = 130.</span></span>

## <a name="example--putting-both-together"></a><span data-ttu-id="111d6-126">Пример объединения обеих точек восстановления</span><span class="sxs-lookup"><span data-stu-id="111d6-126">Example – Putting both together</span></span>
![Образец экрана](./media/backup-azure-backup-cloud-as-tape/samplescreen.png)

1. <span data-ttu-id="111d6-128">**Ежедневная политика хранения.** Резервные копии, создаваемые ежедневно, хранятся в течение семи дней.</span><span class="sxs-lookup"><span data-stu-id="111d6-128">**Daily retention policy**: Backups taken daily are stored for seven days.</span></span>
2. <span data-ttu-id="111d6-129">**Еженедельная политика хранения.** Резервные копии, создаваемые каждый день в полночь и каждую субботу в 18:00, хранятся в течение четырех недель.</span><span class="sxs-lookup"><span data-stu-id="111d6-129">**Weekly retention policy**: Backups taken every day at midnight and 6PM Saturday are preserved for four weeks</span></span>
3. <span data-ttu-id="111d6-130">**Ежемесячная политика хранения.** Резервные копии, создаваемые в полночь и в 18:00 в последнюю субботу каждого месяца, хранятся в течение 12 месяцев.</span><span class="sxs-lookup"><span data-stu-id="111d6-130">**Monthly retention policy**: Backups taken at midnight and 6pm on the last Saturday of each month are preserved for 12 months</span></span>
4. <span data-ttu-id="111d6-131">**Ежегодная политика хранения.** Резервные копии, создаваемые в полночь в последнюю субботу каждого марта, хранятся в течение 10 лет.</span><span class="sxs-lookup"><span data-stu-id="111d6-131">**Yearly retention policy**: Backups taken at midnight on the last Saturday of every March are preserved for 10 years</span></span>

<span data-ttu-id="111d6-132">Общее число точек хранения (точки, из которых клиент может восстановить данные) в приведенной выше диаграмме вычисляется следующим образом:</span><span class="sxs-lookup"><span data-stu-id="111d6-132">The total number of “retention points” (points from which a customer can restore data) in the preceding diagram is computed as follows:</span></span>

* <span data-ttu-id="111d6-133">две точки в день в течение 7 дней = 14 точек восстановления;</span><span class="sxs-lookup"><span data-stu-id="111d6-133">two points per day for seven days = 14 recovery points</span></span>
* <span data-ttu-id="111d6-134">две точки в неделю в течение 4 недель = 8 точек восстановления;</span><span class="sxs-lookup"><span data-stu-id="111d6-134">two points per week for four weeks = 8 recovery points</span></span>
* <span data-ttu-id="111d6-135">две точки в месяц в течение 12 месяцев = 24 точки восстановления;</span><span class="sxs-lookup"><span data-stu-id="111d6-135">two points per month for 12 months = 24 recovery points</span></span>
* <span data-ttu-id="111d6-136">одна точка в год в течение 10 лет = 10 точек восстановления.</span><span class="sxs-lookup"><span data-stu-id="111d6-136">one point per year per 10 years = 10 recovery points</span></span>

<span data-ttu-id="111d6-137">Общее количество точек восстановления равно 56.</span><span class="sxs-lookup"><span data-stu-id="111d6-137">The total number of recovery points is 56.</span></span>

> [!NOTE]
> <span data-ttu-id="111d6-138">У службы архивации Azure нет ограничений на количество точек восстановления.</span><span class="sxs-lookup"><span data-stu-id="111d6-138">Azure backup doesn't have a restriction on number of recovery points.</span></span>
>
>

## <a name="advanced-configuration"></a><span data-ttu-id="111d6-139">Расширенная конфигурация</span><span class="sxs-lookup"><span data-stu-id="111d6-139">Advanced configuration</span></span>
<span data-ttu-id="111d6-140">Щелкнув элемент **Изменить** на показанном выше экране, клиенты получат доступ к дополнительным возможностям для составления расписаний хранения.</span><span class="sxs-lookup"><span data-stu-id="111d6-140">By clicking **Modify** in the preceding screen, customers have further flexibility in specifying retention schedules.</span></span>

![Изменить](./media/backup-azure-backup-cloud-as-tape/modify.png)

## <a name="next-steps"></a><span data-ttu-id="111d6-142">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="111d6-142">Next Steps</span></span>
<span data-ttu-id="111d6-143">Дополнительные сведения о службе архивации Azure см. в статьях:</span><span class="sxs-lookup"><span data-stu-id="111d6-143">For more information about Azure Backup, see:</span></span>

* [<span data-ttu-id="111d6-144">Общие сведения о службе архивации Azure</span><span class="sxs-lookup"><span data-stu-id="111d6-144">Introduction to Azure Backup</span></span>](backup-introduction-to-azure-backup.md)
* [<span data-ttu-id="111d6-145">Знакомство со службой архивации Azure</span><span class="sxs-lookup"><span data-stu-id="111d6-145">Try Azure Backup</span></span>](backup-try-azure-backup-in-10-mins.md)
