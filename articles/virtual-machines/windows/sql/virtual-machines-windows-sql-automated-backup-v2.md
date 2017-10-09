---
title: "aaaAutomated v2 резервного копирования для SQL Server 2016 виртуальных машин Azure | Документы Microsoft"
description: "Описывается функция hello автоматического резервного копирования для SQL Server 2016 работающих виртуальных машин в Azure. Эта статья содержит определенные tooVMs, с помощью диспетчера ресурсов hello."
services: virtual-machines-windows
documentationcenter: na
author: rothja
manager: jhubbard
editor: 
tags: azure-resource-manager
ms.assetid: ebd23868-821c-475b-b867-06d4a2e310c7
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 04/05/2017
ms.author: jroth
ms.openlocfilehash: a322792fb22c76bfa74fafb711b8b1927a6e2b3a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="automated-backup-v2-for-sql-server-2016-azure-virtual-machines-resource-manager"></a><span data-ttu-id="dd077-104">Автоматическая архивация версии 2 для виртуальных машин SQL Server 2016 в Azure (Resource Manager)</span><span class="sxs-lookup"><span data-stu-id="dd077-104">Automated Backup v2 for SQL Server 2016 Azure Virtual Machines (Resource Manager)</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="dd077-105">SQL Server 2014</span><span class="sxs-lookup"><span data-stu-id="dd077-105">SQL Server 2014</span></span>](virtual-machines-windows-sql-automated-backup.md)
> * [<span data-ttu-id="dd077-106">SQL Server 2016</span><span class="sxs-lookup"><span data-stu-id="dd077-106">SQL Server 2016</span></span>](virtual-machines-windows-sql-automated-backup-v2.md)

<span data-ttu-id="dd077-107">Автоматическая настройка автоматического резервного копирования v2 [tooMicrosoft управляемого резервного копирования Azure](https://msdn.microsoft.com/library/dn449496.aspx) для всех существующих и новых баз данных на виртуальной Машине Azure под управлением SQL Server 2016 Standard, Enterprise или Developer.</span><span class="sxs-lookup"><span data-stu-id="dd077-107">Automated Backup v2 automatically configures [Managed Backup tooMicrosoft Azure](https://msdn.microsoft.com/library/dn449496.aspx) for all existing and new databases on an Azure VM running SQL Server 2016 Standard, Enterprise, or Developer editions.</span></span> <span data-ttu-id="dd077-108">Это позволяет tooconfigure регулярные резервные копии, использовать устойчивые Azure BLOB-объекта хранилища.</span><span class="sxs-lookup"><span data-stu-id="dd077-108">This enables you tooconfigure regular database backups that utilize durable Azure blob storage.</span></span> <span data-ttu-id="dd077-109">Автоматическое резервное копирование v2 зависит от hello [расширения агента SQL Server IaaS](virtual-machines-windows-sql-server-agent-extension.md).</span><span class="sxs-lookup"><span data-stu-id="dd077-109">Automated Backup v2 depends on hello [SQL Server IaaS Agent Extension](virtual-machines-windows-sql-server-agent-extension.md).</span></span>

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-rm-include.md)]

## <a name="prerequisites"></a><span data-ttu-id="dd077-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="dd077-110">Prerequisites</span></span>
<span data-ttu-id="dd077-111">toouse v2 автоматического резервного копирования, просмотрите hello следующие предварительные требования:</span><span class="sxs-lookup"><span data-stu-id="dd077-111">toouse Automated Backup v2, review hello following prerequisites:</span></span>

<span data-ttu-id="dd077-112">**Операционная система**</span><span class="sxs-lookup"><span data-stu-id="dd077-112">**Operating System**:</span></span>

- <span data-ttu-id="dd077-113">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="dd077-113">Windows Server 2012 R2</span></span>
- <span data-ttu-id="dd077-114">Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="dd077-114">Windows Server 2016</span></span>

<span data-ttu-id="dd077-115">**Версия/выпуск SQL Server**</span><span class="sxs-lookup"><span data-stu-id="dd077-115">**SQL Server version/edition**:</span></span>

- <span data-ttu-id="dd077-116">SQL Server 2016 Standard</span><span class="sxs-lookup"><span data-stu-id="dd077-116">SQL Server 2016 Standard</span></span>
- <span data-ttu-id="dd077-117">SQL Server 2016 Enterprise</span><span class="sxs-lookup"><span data-stu-id="dd077-117">SQL Server 2016 Enterprise</span></span>
- <span data-ttu-id="dd077-118">SQL Server 2016 Developer.</span><span class="sxs-lookup"><span data-stu-id="dd077-118">SQL Server 2016 Developer</span></span>

> [!IMPORTANT]
> <span data-ttu-id="dd077-119">Автоматическая архивация версии 2 работает с SQL Server 2016.</span><span class="sxs-lookup"><span data-stu-id="dd077-119">Automated Backup v2 works with SQL Server 2016.</span></span> <span data-ttu-id="dd077-120">При использовании SQL Server 2014 можно использовать автоматическое резервное копирование v1 tooback копии баз данных.</span><span class="sxs-lookup"><span data-stu-id="dd077-120">If you are using SQL Server 2014, you can use Automated Backup v1 tooback up your databases.</span></span> <span data-ttu-id="dd077-121">Дополнительную информацию см. в статье [Автоматическая архивация для виртуальных машин SQL Server 2014 в Azure](virtual-machines-windows-sql-automated-backup.md).</span><span class="sxs-lookup"><span data-stu-id="dd077-121">For more information, see [Automated Backup for SQL Server 2014 Azure Virtual Machines](virtual-machines-windows-sql-automated-backup.md).</span></span>

<span data-ttu-id="dd077-122">**Конфигурация базы данных**</span><span class="sxs-lookup"><span data-stu-id="dd077-122">**Database configuration**:</span></span>

- <span data-ttu-id="dd077-123">Целевые базы данных должна использовать модель полного восстановления hello.</span><span class="sxs-lookup"><span data-stu-id="dd077-123">Target databases must use hello full recovery model.</span></span> <span data-ttu-id="dd077-124">Дополнительные сведения о влиянии hello hello модель полного восстановления резервных копий см. в разделе [hello резервного копирования в модели полного восстановления](https://technet.microsoft.com/library/ms190217.aspx).</span><span class="sxs-lookup"><span data-stu-id="dd077-124">For more information about hello impact of hello full recovery model on backups, see [Backup Under hello Full Recovery Model](https://technet.microsoft.com/library/ms190217.aspx).</span></span>
- <span data-ttu-id="dd077-125">Системные базы данных имеют toouse модель полного восстановления.</span><span class="sxs-lookup"><span data-stu-id="dd077-125">System databases do not have toouse full recovery model.</span></span> <span data-ttu-id="dd077-126">Тем не менее если требуется toobe резервных копий журнала для модели или базы данных MSDB, необходимо использовать модель полного восстановления.</span><span class="sxs-lookup"><span data-stu-id="dd077-126">However, if you require log backups toobe taken for Model or MSDB, you must use full recovery model.</span></span>
- <span data-ttu-id="dd077-127">Целевые базы данных должен быть на экземпляре SQL Server по умолчанию hello.</span><span class="sxs-lookup"><span data-stu-id="dd077-127">Target databases must be on hello default SQL Server instance.</span></span> <span data-ttu-id="dd077-128">Hello расширения IaaS SQL Server не поддерживает именованные экземпляры.</span><span class="sxs-lookup"><span data-stu-id="dd077-128">hello SQL Server IaaS Extension does not support named instances.</span></span>

<span data-ttu-id="dd077-129">**Модель развертывания Azure**</span><span class="sxs-lookup"><span data-stu-id="dd077-129">**Azure deployment model**:</span></span>

- <span data-ttu-id="dd077-130">Диспетчер ресурсов</span><span class="sxs-lookup"><span data-stu-id="dd077-130">Resource Manager</span></span>

> [!NOTE]
> <span data-ttu-id="dd077-131">Автоматическая архивация зависит hello **расширения агента SQL Server IaaS**.</span><span class="sxs-lookup"><span data-stu-id="dd077-131">Automated Backup relies on hello **SQL Server IaaS Agent Extension**.</span></span> <span data-ttu-id="dd077-132">В текущей коллекции образов виртуальных машин SQL это расширение присутствует по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="dd077-132">Current SQL virtual machine gallery images add this extension by default.</span></span> <span data-ttu-id="dd077-133">Дополнительные сведения см. в статье [SQL Server IaaS Agent Extension](virtual-machines-windows-sql-server-agent-extension.md) (Расширение агента SQL Server IaaS).</span><span class="sxs-lookup"><span data-stu-id="dd077-133">For more information, see [SQL Server IaaS Agent Extension](virtual-machines-windows-sql-server-agent-extension.md).</span></span>

## <a name="settings"></a><span data-ttu-id="dd077-134">данных</span><span class="sxs-lookup"><span data-stu-id="dd077-134">Settings</span></span>
<span data-ttu-id="dd077-135">Hello следующей таблице описаны параметры hello, которые могут быть настроены для автоматического резервного копирования v2.</span><span class="sxs-lookup"><span data-stu-id="dd077-135">hello following table describes hello options that can be configured for Automated Backup v2.</span></span> <span data-ttu-id="dd077-136">Hello фактические шаги настройки отличаются в зависимости от того, используются ли hello портал Azure или команд Windows PowerShell для Azure.</span><span class="sxs-lookup"><span data-stu-id="dd077-136">hello actual configuration steps vary depending on whether you use hello Azure portal or Azure Windows PowerShell commands.</span></span>

### <a name="basic-settings"></a><span data-ttu-id="dd077-137">Основные параметры</span><span class="sxs-lookup"><span data-stu-id="dd077-137">Basic Settings</span></span>

| <span data-ttu-id="dd077-138">Настройка</span><span class="sxs-lookup"><span data-stu-id="dd077-138">Setting</span></span> | <span data-ttu-id="dd077-139">Диапазон (по умолчанию)</span><span class="sxs-lookup"><span data-stu-id="dd077-139">Range (Default)</span></span> | <span data-ttu-id="dd077-140">Описание</span><span class="sxs-lookup"><span data-stu-id="dd077-140">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="dd077-141">**Автоматическая архивация**</span><span class="sxs-lookup"><span data-stu-id="dd077-141">**Automated Backup**</span></span> | <span data-ttu-id="dd077-142">Включено/отключено (отключено)</span><span class="sxs-lookup"><span data-stu-id="dd077-142">Enable/Disable (Disabled)</span></span> | <span data-ttu-id="dd077-143">Включает или отключает автоматическую архивацию для виртуальной машины Azure под управлением SQL Server 2016 Standard или SQL Server 2016 Enterprise.</span><span class="sxs-lookup"><span data-stu-id="dd077-143">Enables or disables Automated Backup for an Azure VM running SQL Server 2016 Standard or Enterprise.</span></span> |
| <span data-ttu-id="dd077-144">**Срок хранения**</span><span class="sxs-lookup"><span data-stu-id="dd077-144">**Retention Period**</span></span> | <span data-ttu-id="dd077-145">1–30 дней (30 дней)</span><span class="sxs-lookup"><span data-stu-id="dd077-145">1-30 days (30 days)</span></span> | <span data-ttu-id="dd077-146">количество резервных копий tooretain дней Hello.</span><span class="sxs-lookup"><span data-stu-id="dd077-146">hello number of days tooretain backups.</span></span> |
| <span data-ttu-id="dd077-147">**Учетная запись хранения**</span><span class="sxs-lookup"><span data-stu-id="dd077-147">**Storage Account**</span></span> | <span data-ttu-id="dd077-148">Учетная запись хранения Azure.</span><span class="sxs-lookup"><span data-stu-id="dd077-148">Azure storage account</span></span> | <span data-ttu-id="dd077-149">Toouse учетной записи хранилища Azure для хранения файлов автоматического резервного копирования в хранилище больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="dd077-149">An Azure storage account toouse for storing Automated Backup files in blob storage.</span></span> <span data-ttu-id="dd077-150">Контейнер создается в этом toostore расположение всех файлов резервных копий.</span><span class="sxs-lookup"><span data-stu-id="dd077-150">A container is created at this location toostore all backup files.</span></span> <span data-ttu-id="dd077-151">файл резервной копии Hello соглашение об именах включает hello даты, времени и идентификатор GUID базы данных.</span><span class="sxs-lookup"><span data-stu-id="dd077-151">hello backup file naming convention includes hello date, time, and database GUID.</span></span> |
| <span data-ttu-id="dd077-152">**Шифрование**</span><span class="sxs-lookup"><span data-stu-id="dd077-152">**Encryption**</span></span> |<span data-ttu-id="dd077-153">Включено/отключено (отключено)</span><span class="sxs-lookup"><span data-stu-id="dd077-153">Enable/Disable (Disabled)</span></span> | <span data-ttu-id="dd077-154">Включает или отключает шифрование.</span><span class="sxs-lookup"><span data-stu-id="dd077-154">Enables or disables encryption.</span></span> <span data-ttu-id="dd077-155">При включено шифрование, сертификаты, используемые toorestore hello hello-резервной копии находятся в hello указан учетную запись хранилища в hello же **automaticbackup** контейнер с помощью hello же соглашение об именовании.</span><span class="sxs-lookup"><span data-stu-id="dd077-155">When encryption is enabled, hello certificates used toorestore hello backup are located in hello specified storage account in hello same **automaticbackup** container using hello same naming convention.</span></span> <span data-ttu-id="dd077-156">При изменении пароля hello, новый сертификат создается с этим паролем, но Здравствуй, старый сертификат остается toorestore предыдущих резервных копий.</span><span class="sxs-lookup"><span data-stu-id="dd077-156">If hello password changes, a new certificate is generated with that password, but hello old certificate remains toorestore prior backups.</span></span> |
| <span data-ttu-id="dd077-157">**Пароль**</span><span class="sxs-lookup"><span data-stu-id="dd077-157">**Password**</span></span> |<span data-ttu-id="dd077-158">Текст пароля</span><span class="sxs-lookup"><span data-stu-id="dd077-158">Password text</span></span> | <span data-ttu-id="dd077-159">Пароль для ключей шифрования.</span><span class="sxs-lookup"><span data-stu-id="dd077-159">A password for encryption keys.</span></span> <span data-ttu-id="dd077-160">Требуется, только если шифрование включено.</span><span class="sxs-lookup"><span data-stu-id="dd077-160">This is only required if encryption is enabled.</span></span> <span data-ttu-id="dd077-161">В порядке toorestore зашифрованной резервной копии, необходимо иметь правильный пароль hello и связанные сертификата, который был использован в hello время, когда была создана резервная копия hello.</span><span class="sxs-lookup"><span data-stu-id="dd077-161">In order toorestore an encrypted backup, you must have hello correct password and related certificate that was used at hello time hello backup was taken.</span></span> |

### <a name="advanced-settings"></a><span data-ttu-id="dd077-162">Дополнительные параметры</span><span class="sxs-lookup"><span data-stu-id="dd077-162">Advanced Settings</span></span>

| <span data-ttu-id="dd077-163">Настройка</span><span class="sxs-lookup"><span data-stu-id="dd077-163">Setting</span></span> | <span data-ttu-id="dd077-164">Диапазон (по умолчанию)</span><span class="sxs-lookup"><span data-stu-id="dd077-164">Range (Default)</span></span> | <span data-ttu-id="dd077-165">Описание</span><span class="sxs-lookup"><span data-stu-id="dd077-165">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="dd077-166">**System Database Backups** (Архивация системных баз данных)</span><span class="sxs-lookup"><span data-stu-id="dd077-166">**System Database Backups**</span></span> | <span data-ttu-id="dd077-167">Включено/отключено (отключено)</span><span class="sxs-lookup"><span data-stu-id="dd077-167">Enable/Disable (Disabled)</span></span> | <span data-ttu-id="dd077-168">При включении этой функции также выполнить резервное копирование hello системных баз данных: Master, MSDB и Model.</span><span class="sxs-lookup"><span data-stu-id="dd077-168">When enabled, this feature will also back up hello system databases: Master, MSDB, and Model.</span></span> <span data-ttu-id="dd077-169">Убедитесь, они находятся в режиме полного восстановления Если выполнены toobe резервных копий журнала для hello MSDB и базы данных модели.</span><span class="sxs-lookup"><span data-stu-id="dd077-169">For hello MSDB and Model databases, verify that they are in full recovery mode if you want log backups toobe taken.</span></span> <span data-ttu-id="dd077-170">Резервные копии журналов для базы данных Master не создаются.</span><span class="sxs-lookup"><span data-stu-id="dd077-170">Log backups are never taken for Master.</span></span> <span data-ttu-id="dd077-171">Кроме того, не создаются и резервные копии базы данных TempDB.</span><span class="sxs-lookup"><span data-stu-id="dd077-171">And no backups are taken for TempDB.</span></span> |
| <span data-ttu-id="dd077-172">**Расписание архивации**</span><span class="sxs-lookup"><span data-stu-id="dd077-172">**Backup Schedule**</span></span> | <span data-ttu-id="dd077-173">Ручная или автоматическая (автоматическая)</span><span class="sxs-lookup"><span data-stu-id="dd077-173">Manual/Automated (Automated)</span></span> | <span data-ttu-id="dd077-174">По умолчанию hello расписание резервного копирования будет автоматически определен на основе рост журнала hello.</span><span class="sxs-lookup"><span data-stu-id="dd077-174">By default, hello backup schedule will be automatically determined based on hello log growth.</span></span> <span data-ttu-id="dd077-175">Вручную расписание резервного копирования позволяет hello пользователя toospecify hello временное окно резервного копирования.</span><span class="sxs-lookup"><span data-stu-id="dd077-175">Manual backup schedule allows hello user toospecify hello time window for backups.</span></span> <span data-ttu-id="dd077-176">В этом случае резервное копирование только занимает место во hello указаны частоты и во время hello временное окно конкретный день.</span><span class="sxs-lookup"><span data-stu-id="dd077-176">In this case, backups will only ever take place at hello specified frequency and during hello specified time window of a given day.</span></span> |
| <span data-ttu-id="dd077-177">**Full backup frequency** (Частота полной архивации)</span><span class="sxs-lookup"><span data-stu-id="dd077-177">**Full backup frequency**</span></span> | <span data-ttu-id="dd077-178">Ежедневно или еженедельно</span><span class="sxs-lookup"><span data-stu-id="dd077-178">Daily/Weekly</span></span> | <span data-ttu-id="dd077-179">Частота создания полных резервных копий.</span><span class="sxs-lookup"><span data-stu-id="dd077-179">Frequency of full backups.</span></span> <span data-ttu-id="dd077-180">В обоих случаях во время следующего запланированного времени периода hello начнется полные резервные копии.</span><span class="sxs-lookup"><span data-stu-id="dd077-180">In both cases, full backups will begin during hello next scheduled time window.</span></span> <span data-ttu-id="dd077-181">Если выбрана еженедельная архивация, то она может охватывать несколько дней, пока не будут успешно созданы резервные копии всех баз данных.</span><span class="sxs-lookup"><span data-stu-id="dd077-181">When weekly is selected, backups could span multiple days until all databases have successfully backed up.</span></span> |
| <span data-ttu-id="dd077-182">**Full backup start time** (Время начала полной архивации)</span><span class="sxs-lookup"><span data-stu-id="dd077-182">**Full backup start time**</span></span> | <span data-ttu-id="dd077-183">00:00–23:00 (01:00)</span><span class="sxs-lookup"><span data-stu-id="dd077-183">00:00 – 23:00 (01:00)</span></span> | <span data-ttu-id="dd077-184">Время начала полной архивации в заданный день.</span><span class="sxs-lookup"><span data-stu-id="dd077-184">Start time of a given day during which full backups can take place.</span></span> |
| <span data-ttu-id="dd077-185">**Full backup time window** (Временное окно полной архивации)</span><span class="sxs-lookup"><span data-stu-id="dd077-185">**Full backup time window**</span></span> | <span data-ttu-id="dd077-186">1–23 ч (1 ч)</span><span class="sxs-lookup"><span data-stu-id="dd077-186">1 – 23 hours (1 hour)</span></span> | <span data-ttu-id="dd077-187">Продолжительность периода времени hello заданного дня, во время которого разрешено выполнение полного резервного копирования.</span><span class="sxs-lookup"><span data-stu-id="dd077-187">Duration of hello time window of a given day during which full backups can take place.</span></span> |
| <span data-ttu-id="dd077-188">**Log backup frequency** (Частота создания резервных копий журналов)</span><span class="sxs-lookup"><span data-stu-id="dd077-188">**Log backup frequency**</span></span> | <span data-ttu-id="dd077-189">5–60 мин (60 мин)</span><span class="sxs-lookup"><span data-stu-id="dd077-189">5 – 60 minutes (60 minutes)</span></span> | <span data-ttu-id="dd077-190">Частота создания резервных копий журналов.</span><span class="sxs-lookup"><span data-stu-id="dd077-190">Frequency of log backups.</span></span> |

## <a name="understanding-full-backup-frequency"></a><span data-ttu-id="dd077-191">Основные сведения о частоте полной архивации</span><span class="sxs-lookup"><span data-stu-id="dd077-191">Understanding full backup frequency</span></span>
<span data-ttu-id="dd077-192">Это важные toounderstand hello различие между ежедневно и еженедельно полные резервные копии.</span><span class="sxs-lookup"><span data-stu-id="dd077-192">It is important toounderstand hello difference between daily and weekly full backups.</span></span> <span data-ttu-id="dd077-193">Для этого мы рассмотрим два примера сценария.</span><span class="sxs-lookup"><span data-stu-id="dd077-193">In this effort, we will walk through two example scenarios.</span></span>

### <a name="scenario-1-weekly-backups"></a><span data-ttu-id="dd077-194">Сценарий 1. Еженедельные резервные копии</span><span class="sxs-lookup"><span data-stu-id="dd077-194">Scenario 1: Weekly backups</span></span>
<span data-ttu-id="dd077-195">У вас есть виртуальная машина SQL Server, которая содержит несколько очень больших баз данных.</span><span class="sxs-lookup"><span data-stu-id="dd077-195">You have a SQL Server VM which contains a number of very large databases.</span></span>

<span data-ttu-id="dd077-196">Понедельник включить автоматическое резервное копирование v2 с hello следующие параметры:</span><span class="sxs-lookup"><span data-stu-id="dd077-196">On Monday, you enable Automated Backup v2 with hello following settings:</span></span>

- <span data-ttu-id="dd077-197">"Расписание архивации": **Ручное**;</span><span class="sxs-lookup"><span data-stu-id="dd077-197">Backup schedule: **Manual**</span></span>
- <span data-ttu-id="dd077-198">"Full backup frequency" (Частота полной архивации): **Еженедельная**;</span><span class="sxs-lookup"><span data-stu-id="dd077-198">Full backup frequency: **Weekly**</span></span>
- <span data-ttu-id="dd077-199">"Full backup start time" (Время начала полной архивации): **01:00**;</span><span class="sxs-lookup"><span data-stu-id="dd077-199">Full backup start time: **01:00**</span></span>
- <span data-ttu-id="dd077-200">"Full backup time window" (Временное окно полной архивации): **1 ч**.</span><span class="sxs-lookup"><span data-stu-id="dd077-200">Full backup time window: **1 hour**</span></span>

<span data-ttu-id="dd077-201">Таким образом, чтобы hello следующей доступной резервной копии, вторник в 13: 00 для 1 час.</span><span class="sxs-lookup"><span data-stu-id="dd077-201">This means that hello next available backup window is Tuesday at 1 AM for 1 hour.</span></span> <span data-ttu-id="dd077-202">В это время служба автоматической архивации начнет по очереди архивировать ваши базы данных.</span><span class="sxs-lookup"><span data-stu-id="dd077-202">At that time, Automated Backup will begin backing up your databases one at a time.</span></span> <span data-ttu-id="dd077-203">В этом сценарии базы данных обладают достаточной будет выполнена, полные резервные копии для баз данных, hello Первая пара.</span><span class="sxs-lookup"><span data-stu-id="dd077-203">In this scenario, your databases are large enough that full backups will complete for hello first couple databases.</span></span> <span data-ttu-id="dd077-204">Однако через час не все базы данных hello не созданы резервные копии.</span><span class="sxs-lookup"><span data-stu-id="dd077-204">However, after one hour not all of hello databases have been backed up.</span></span>

<span data-ttu-id="dd077-205">В этом случае автоматическое резервное копирование начнется резервное копирование hello оставшихся баз данных hello следующего дня, среда, в 13: 00 для 1 час.</span><span class="sxs-lookup"><span data-stu-id="dd077-205">When this happens, Automated Backup will begin backing up hello remaining databases hello next day, Wednesday at 1 AM for 1 hour.</span></span> <span data-ttu-id="dd077-206">Если не все базы данных не созданы резервные копии в это время, он попытается подключиться снова hello следующий день в hello же время.</span><span class="sxs-lookup"><span data-stu-id="dd077-206">If not all databases have been backed up in that time, it will try again hello next day at hello same time.</span></span> <span data-ttu-id="dd077-207">Это будет продолжаться, пока все базы данных не будут заархивированы.</span><span class="sxs-lookup"><span data-stu-id="dd077-207">This will continue until all databases have been successfully backed up.</span></span>

<span data-ttu-id="dd077-208">Как только наступит следующий вторник, служба автоматической архивации снова начнет создавать резервные копии всех баз данных.</span><span class="sxs-lookup"><span data-stu-id="dd077-208">Once it reaches Tuesday again, Automated Backup will begin backing up all databases once again.</span></span>

<span data-ttu-id="dd077-209">Этот сценарий показывает, что автоматическое резервное копирование будет работать только в пределах hello указанного интервала времени, и каждой базы данных будут создаваться резервные копии один раз в неделю.</span><span class="sxs-lookup"><span data-stu-id="dd077-209">This scenario shows that Automated Backup will only operate within hello specified time window, and each database will be backed up once per week.</span></span> <span data-ttu-id="dd077-210">Это также показывает, что возможна для toospan резервные копии нескольких дней в hello случае когда нет возможности toocomplete все резервные копии в течение одного дня.</span><span class="sxs-lookup"><span data-stu-id="dd077-210">This also shows that it is possible for backups toospan multiple days in hello case where it is not possible toocomplete all backups in a single day.</span></span>

### <a name="scenario-2-daily-backups"></a><span data-ttu-id="dd077-211">Сценарий 2. Ежедневные резервные копии</span><span class="sxs-lookup"><span data-stu-id="dd077-211">Scenario 2: Daily backups</span></span>
<span data-ttu-id="dd077-212">У вас есть виртуальная машина SQL Server, которая содержит несколько очень больших баз данных.</span><span class="sxs-lookup"><span data-stu-id="dd077-212">You have a SQL Server VM which contains a number of very large databases.</span></span>

<span data-ttu-id="dd077-213">Понедельник включить автоматическое резервное копирование v2 с hello следующие параметры:</span><span class="sxs-lookup"><span data-stu-id="dd077-213">On Monday, you enable Automated Backup v2 with hello following settings:</span></span>

- <span data-ttu-id="dd077-214">"Расписание архивации": "Ручное";</span><span class="sxs-lookup"><span data-stu-id="dd077-214">Backup schedule: Manual</span></span>
- <span data-ttu-id="dd077-215">"Full backup frequency" (Частота полной архивации): "Ежедневная";</span><span class="sxs-lookup"><span data-stu-id="dd077-215">Full backup frequency: Daily</span></span>
- <span data-ttu-id="dd077-216">"Full backup start time" (Время начала полной архивации): "22:00";</span><span class="sxs-lookup"><span data-stu-id="dd077-216">Full backup start time: 22:00</span></span>
- <span data-ttu-id="dd077-217">"Full backup time window" (Временное окно полной архивации): "6 ч".</span><span class="sxs-lookup"><span data-stu-id="dd077-217">Full backup time window: 6 hours</span></span>

<span data-ttu-id="dd077-218">Таким образом, чтобы hello следующей доступной резервной копии, понедельник в 22: 00 на 6 часов.</span><span class="sxs-lookup"><span data-stu-id="dd077-218">This means that hello next available backup window is Monday at 10 PM for 6 hours.</span></span> <span data-ttu-id="dd077-219">В это время служба автоматической архивации начнет по очереди архивировать ваши базы данных.</span><span class="sxs-lookup"><span data-stu-id="dd077-219">At that time, Automated Backup will begin backing up your databases one at a time.</span></span>

<span data-ttu-id="dd077-220">Затем во вторник в 22:00 снова начнется 6-часовая полная архивация всех баз данных.</span><span class="sxs-lookup"><span data-stu-id="dd077-220">Then, on Tuesday at 10 for 6 hours, full backups of all databases will start again.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="dd077-221">При планировании ежедневного резервного копирования, рекомендуется запланировать tooensure широкий времени окна, скопированы все базы данных в течение этого времени.</span><span class="sxs-lookup"><span data-stu-id="dd077-221">When scheduling daily backups, it is recommended that you schedule a wide time window tooensure all databases can be backed up within this time.</span></span> <span data-ttu-id="dd077-222">Это особенно важно в случае hello, при наличии большого объема данных tooback вверх.</span><span class="sxs-lookup"><span data-stu-id="dd077-222">This is especially important in hello case where you have a large amount of data tooback up.</span></span>

## <a name="configuration-in-hello-portal"></a><span data-ttu-id="dd077-223">Конфигурация в hello портала</span><span class="sxs-lookup"><span data-stu-id="dd077-223">Configuration in hello Portal</span></span>

<span data-ttu-id="dd077-224">Можно использовать v2 автоматического резервного копирования Azure портала tooconfigure hello во время инициализации или для существующих виртуальных машинах SQL Server 2016.</span><span class="sxs-lookup"><span data-stu-id="dd077-224">You can use hello Azure portal tooconfigure Automated Backup v2 during provisioning or for existing SQL Server 2016 VMs.</span></span>

### <a name="new-vms"></a><span data-ttu-id="dd077-225">Новые виртуальные машины</span><span class="sxs-lookup"><span data-stu-id="dd077-225">New VMs</span></span>

<span data-ttu-id="dd077-226">Используйте автоматическое резервное копирование v2 hello Azure портала tooconfigure при создании новой виртуальной машины 2016 SQL Server в модели развертывания диспетчера ресурсов hello.</span><span class="sxs-lookup"><span data-stu-id="dd077-226">Use hello Azure portal tooconfigure Automated Backup v2 when you create a new SQL Server 2016 Virtual Machine in hello Resource Manager deployment model.</span></span> 

<span data-ttu-id="dd077-227">В hello **параметры SQL Server** колонке выберите **автоматическое резервное копирование**.</span><span class="sxs-lookup"><span data-stu-id="dd077-227">In hello **SQL Server settings** blade, select **Automated backup**.</span></span> <span data-ttu-id="dd077-228">Hello следующие Azure портала снимке экрана показано hello **автоматическое резервное копирование SQL** колонку.</span><span class="sxs-lookup"><span data-stu-id="dd077-228">hello following Azure portal screenshot shows hello **SQL Automated Backup** blade.</span></span>

![Настройка автоматической архивации SQL на портале Azure](./media/virtual-machines-windows-sql-automated-backup-v2/automated-backup-blade.png)

> [!NOTE]
> <span data-ttu-id="dd077-230">По умолчанию автоматическая архивация версии 2 отключена.</span><span class="sxs-lookup"><span data-stu-id="dd077-230">Automated Backup v2 is disabled by default.</span></span>

<span data-ttu-id="dd077-231">Контекст, в разделе hello полный на [подготовку виртуальной машины SQL Server в Azure](virtual-machines-windows-portal-sql-server-provision.md).</span><span class="sxs-lookup"><span data-stu-id="dd077-231">For context, see hello complete topic on [provisioning a SQL Server virtual machine in Azure](virtual-machines-windows-portal-sql-server-provision.md).</span></span>

### <a name="existing-vms"></a><span data-ttu-id="dd077-232">Существующие виртуальные машины</span><span class="sxs-lookup"><span data-stu-id="dd077-232">Existing VMs</span></span>

<span data-ttu-id="dd077-233">Выберите существующую виртуальную машину SQL Server.</span><span class="sxs-lookup"><span data-stu-id="dd077-233">For existing SQL Server virtual machines, select your SQL Server virtual machine.</span></span> <span data-ttu-id="dd077-234">Затем выберите hello **конфигурации SQL Server** раздел hello **параметры** колонку.</span><span class="sxs-lookup"><span data-stu-id="dd077-234">Then select hello **SQL Server configuration** section of hello **Settings** blade.</span></span>

![Автоматизированная архивация SQL для существующих виртуальных машин](./media/virtual-machines-windows-sql-automated-backup-v2/sql-server-configuration.png)

<span data-ttu-id="dd077-236">В hello **конфигурации SQL Server** колонка, щелкните hello **изменить** кнопку в hello автоматического резервного копирования раздела.</span><span class="sxs-lookup"><span data-stu-id="dd077-236">In hello **SQL Server configuration** blade, click hello **Edit** button in hello Automated backup section.</span></span>

![Настройка автоматизированной архивации SQL для существующих виртуальных машин](./media/virtual-machines-windows-sql-automated-backup-v2/sql-server-configuration-edit.png)

<span data-ttu-id="dd077-238">По завершении нажмите кнопку hello **ОК** кнопку внизу hello hello **конфигурации SQL Server** toosave колонке изменения.</span><span class="sxs-lookup"><span data-stu-id="dd077-238">When finished, click hello **OK** button on hello bottom of hello **SQL Server configuration** blade toosave your changes.</span></span>

<span data-ttu-id="dd077-239">При включении автоматического резервного копирования для hello первый раз Azure настраивает hello агента SQL Server IaaS в фоновом режиме hello.</span><span class="sxs-lookup"><span data-stu-id="dd077-239">If you are enabling Automated Backup for hello first time, Azure configures hello SQL Server IaaS Agent in hello background.</span></span> <span data-ttu-id="dd077-240">В течение этого времени hello Azure портала может показывать, что автоматическая архивация настроена.</span><span class="sxs-lookup"><span data-stu-id="dd077-240">During this time, hello Azure portal might not show that Automated Backup is configured.</span></span> <span data-ttu-id="dd077-241">Подождите несколько минут для hello агента toobe установлены, настроены.</span><span class="sxs-lookup"><span data-stu-id="dd077-241">Wait several minutes for hello agent toobe installed, configured.</span></span> <span data-ttu-id="dd077-242">После этого hello Azure портале будут отображаться новые параметры hello.</span><span class="sxs-lookup"><span data-stu-id="dd077-242">After that hello Azure portal will reflect hello new settings.</span></span>

## <a name="configuration-with-powershell"></a><span data-ttu-id="dd077-243">Настройка с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="dd077-243">Configuration with PowerShell</span></span>

<span data-ttu-id="dd077-244">Можно использовать PowerShell tooconfigure v2 автоматического резервного копирования.</span><span class="sxs-lookup"><span data-stu-id="dd077-244">You can use PowerShell tooconfigure Automated Backup v2.</span></span> <span data-ttu-id="dd077-245">Предварительно необходимо выполнить следующее.</span><span class="sxs-lookup"><span data-stu-id="dd077-245">Before you begin, you must:</span></span>

- <span data-ttu-id="dd077-246">[Загрузите и установите последнюю версию Azure PowerShell hello](http://aka.ms/webpi-azps).</span><span class="sxs-lookup"><span data-stu-id="dd077-246">[Download and install hello latest Azure PowerShell](http://aka.ms/webpi-azps).</span></span>
- <span data-ttu-id="dd077-247">Откройте компонент Windows PowerShell и свяжите его со своей учетной записью.</span><span class="sxs-lookup"><span data-stu-id="dd077-247">Open Windows PowerShell and associate it with your account.</span></span> <span data-ttu-id="dd077-248">Это можно сделать с помощью инструкции hello в hello [настроить подписку](https://docs.microsoft.com/azure/virtual-machines/windows/sql/virtual-machines-windows-ps-sql-create#configure-your-subscription) раздел hello подготовки раздела.</span><span class="sxs-lookup"><span data-stu-id="dd077-248">You can do this by following hello steps in hello [Configure your subscription](https://docs.microsoft.com/azure/virtual-machines/windows/sql/virtual-machines-windows-ps-sql-create#configure-your-subscription) section of hello provisioning topic.</span></span>

### <a name="install-hello-sql-iaas-extension"></a><span data-ttu-id="dd077-249">Установка расширения SQL IaaS hello</span><span class="sxs-lookup"><span data-stu-id="dd077-249">Install hello SQL IaaS Extension</span></span>
<span data-ttu-id="dd077-250">При подготовке виртуальной машины SQL Server из портала Azure hello hello расширения IaaS SQL Server должны быть уже настроены.</span><span class="sxs-lookup"><span data-stu-id="dd077-250">If you provisioned a SQL Server virtual machine from hello Azure portal, hello SQL Server IaaS Extension should already be installed.</span></span> <span data-ttu-id="dd077-251">Можно определить, если оно устанавливается для виртуальной Машины путем вызова **Get AzureRmVM** и проверив hello **расширения** свойство.</span><span class="sxs-lookup"><span data-stu-id="dd077-251">You can determine if it is installed for your VM by calling **Get-AzureRmVM** command and examining hello **Extensions** property.</span></span>

```powershell
$vmname = "vmname"
$resourcegroupname = "resourcegroupname"

(Get-AzureRmVM -Name $vmname -ResourceGroupName $resourcegroupname).Extensions 
```

<span data-ttu-id="dd077-252">Если установлен hello расширения агента IaaS SQL Server, вы увидите, что оно указано как «SqlIaaSAgent» или «SQLIaaSExtension».</span><span class="sxs-lookup"><span data-stu-id="dd077-252">If hello SQL Server IaaS Agent extension is installed, you should see it listed as “SqlIaaSAgent” or “SQLIaaSExtension”.</span></span> <span data-ttu-id="dd077-253">**ProvisioningState** для расширения hello также должен быть «Succeeded».</span><span class="sxs-lookup"><span data-stu-id="dd077-253">**ProvisioningState** for hello extension should also show “Succeeded”.</span></span> 

<span data-ttu-id="dd077-254">Если он не установлен или не удалось подготовить toobe, его можно установить с hello следующую команду.</span><span class="sxs-lookup"><span data-stu-id="dd077-254">If it is not installed or failed toobe provisioned, you can install it with hello following command.</span></span> <span data-ttu-id="dd077-255">В дополнение toohello ВМ имя и группе ресурсов, необходимо также указать область hello (**$region**), расположенных в ВМ.</span><span class="sxs-lookup"><span data-stu-id="dd077-255">In addition toohello VM name and resource group, you must also specify hello region (**$region**) that your VM is located in.</span></span>

```powershell
$region = “EASTUS2”
Set-AzureRmVMSqlServerExtension -VMName $vmname `
    -ResourceGroupName $resourcegroupname -Name "SQLIaasExtension" `
    -Version "1.2" -Location $region 
```

### <span data-ttu-id="dd077-256"><a id="verifysettings"></a> Проверка текущих параметров</span><span class="sxs-lookup"><span data-stu-id="dd077-256"><a id="verifysettings"></a> Verify current settings</span></span>
<span data-ttu-id="dd077-257">Если вы включили автоматическое резервное копирование во время подготовки, можно использовать PowerShell toocheck текущей конфигурации.</span><span class="sxs-lookup"><span data-stu-id="dd077-257">If you enabled automated backup during provisioning, you can use PowerShell toocheck your current configuration.</span></span> <span data-ttu-id="dd077-258">Запустите hello **Get AzureRmVMSqlServerExtension** команды и изучить hello **AutoBackupSettings** свойства:</span><span class="sxs-lookup"><span data-stu-id="dd077-258">Run hello **Get-AzureRmVMSqlServerExtension** command and examine hello **AutoBackupSettings** property:</span></span>

```powershell
(Get-AzureRmVMSqlServerExtension -VMName $vmname -ResourceGroupName $resourcegroupname).AutoBackupSettings
```

<span data-ttu-id="dd077-259">Вы должны получить аналогичные toohello следующие выходные данные:</span><span class="sxs-lookup"><span data-stu-id="dd077-259">You should get output similar toohello following:</span></span>

```
Enable                      : True
EnableEncryption            : False
RetentionPeriod             : 30
StorageUrl                  : https://test.blob.core.windows.net/
StorageAccessKey            :  
Password                    : 
BackupSystemDbs             : False
BackupScheduleType          : Manual
FullBackupFrequency         : WEEKLY
FullBackupStartTime         : 2
FullBackupWindowHours       : 2
LogBackupFrequency          : 60
```

<span data-ttu-id="dd077-260">Если выходных данных показано, что **включить** задано слишком**False**, то у вас есть tooenable автоматическое резервное копирование.</span><span class="sxs-lookup"><span data-stu-id="dd077-260">If your output shows that **Enable** is set too**False**, then you have tooenable automated backup.</span></span> <span data-ttu-id="dd077-261">Hello хорошие новости — Включение и настройка автоматического резервного копирования в hello таким же образом.</span><span class="sxs-lookup"><span data-stu-id="dd077-261">hello good news is that you enable and configure Automated Backup in hello same way.</span></span> <span data-ttu-id="dd077-262">Hello следующем разделе для получения этих сведений.</span><span class="sxs-lookup"><span data-stu-id="dd077-262">See hello next section for this information.</span></span>

> [!NOTE] 
> <span data-ttu-id="dd077-263">Проверьте параметры hello сразу же после внесения изменений, возможно, вы получите обратно hello старые значения конфигурации.</span><span class="sxs-lookup"><span data-stu-id="dd077-263">If you check hello settings immediately after making a change, it is possible that you will get back hello old configuration values.</span></span> <span data-ttu-id="dd077-264">Подождите несколько минут и проверить параметры hello снова toomake том, что изменения были применены.</span><span class="sxs-lookup"><span data-stu-id="dd077-264">Wait a few minutes and check hello settings again toomake sure that your changes were applied.</span></span>

### <a name="configure-automated-backup-v2"></a><span data-ttu-id="dd077-265">Настройка автоматической архивации версии 2</span><span class="sxs-lookup"><span data-stu-id="dd077-265">Configure Automated Backup v2</span></span>
<span data-ttu-id="dd077-266">PowerShell tooenable автоматическое резервное копирование, а также toomodify можно использовать его параметров и поведения в любое время.</span><span class="sxs-lookup"><span data-stu-id="dd077-266">You can use PowerShell tooenable Automated Backup as well as toomodify its configuration and behavior at any time.</span></span> 

<span data-ttu-id="dd077-267">Во-первых выберите или создайте учетную запись хранения hello файлов резервных копий.</span><span class="sxs-lookup"><span data-stu-id="dd077-267">First, select or create a storage account for hello backup files.</span></span> <span data-ttu-id="dd077-268">Hello следующий скрипт выбирает учетную запись хранения или создает ее, если она не существует.</span><span class="sxs-lookup"><span data-stu-id="dd077-268">hello following script selects a storage account or creates it if it does not exist.</span></span>

```powershell
$storage_accountname = “yourstorageaccount”
$storage_resourcegroupname = $resourcegroupname

$storage = Get-AzureRmStorageAccount -ResourceGroupName $resourcegroupname `
    -Name $storage_accountname -ErrorAction SilentlyContinue
If (-Not $storage)
    { $storage = New-AzureRmStorageAccount -ResourceGroupName $storage_resourcegroupname `
    -Name $storage_accountname -SkuName Standard_GRS -Location $region } 
```

> [!NOTE]
> <span data-ttu-id="dd077-269">Служба автоматической архивации не поддерживает хранение резервных копий в хранилище уровня "Премиум", но может создавать резервные копии дисков виртуальных машин, которые используют хранилище уровня "Премиум".</span><span class="sxs-lookup"><span data-stu-id="dd077-269">Automated Backup does not support storing backups in premium storage, but it can take backups from VM disks which use Premium Storage.</span></span>

<span data-ttu-id="dd077-270">Затем с помощью hello **New AzureRmVMSqlServerAutoBackupConfig** команды tooenable и настройка резервного копирования toostore параметры hello v2 автоматического резервного копирования в учетную запись хранилища Azure hello.</span><span class="sxs-lookup"><span data-stu-id="dd077-270">Then use hello **New-AzureRmVMSqlServerAutoBackupConfig** command tooenable and configure hello Automated Backup v2 settings toostore backups in hello Azure storage account.</span></span> <span data-ttu-id="dd077-271">В этом примере hello копии создаются toobe сохраняются в течение 10 дней.</span><span class="sxs-lookup"><span data-stu-id="dd077-271">In this example, hello backups are set toobe retained for 10 days.</span></span> <span data-ttu-id="dd077-272">Архивация системных баз данных включена.</span><span class="sxs-lookup"><span data-stu-id="dd077-272">System database backups are enabled.</span></span> <span data-ttu-id="dd077-273">Полная архивация выполняется раз в неделю, и для нее выделяется 2-часовое временное окно, начинающееся в 20:00.</span><span class="sxs-lookup"><span data-stu-id="dd077-273">Full backups are scheduled for weekly with a time window starting at 20:00 for two hours.</span></span> <span data-ttu-id="dd077-274">Резервные копии журналов создаются каждые 30 минут.</span><span class="sxs-lookup"><span data-stu-id="dd077-274">Log backups are scheduled for every 30 minutes.</span></span> <span data-ttu-id="dd077-275">Здравствуйте, вторая команда **AzureRmVMSqlServerExtension набор**, hello обновления указано ВМ Azure с помощью этих параметров.</span><span class="sxs-lookup"><span data-stu-id="dd077-275">hello second command, **Set-AzureRmVMSqlServerExtension**, updates hello specified Azure VM with these settings.</span></span>

```powershell
$autobackupconfig = New-AzureRmVMSqlServerAutoBackupConfig -Enable `
    -RetentionPeriodInDays 10 -StorageContext $storage.Context `
    -ResourceGroupName $storage_resourcegroupname -BackupSystemDbs `
    -BackupScheduleType Manual -FullBackupFrequency Weekly `
    -FullBackupStartHour 20 -FullBackupWindowInHours 2 `
    -LogBackupFrequencyInMinutes 30 

Set-AzureRmVMSqlServerExtension -AutoBackupSettings $autobackupconfig `
    -VMName $vmname -ResourceGroupName $resourcegroupname 
```

<span data-ttu-id="dd077-276">Он может занять несколько минут tooinstall и настроить агент SQL Server IaaS hello.</span><span class="sxs-lookup"><span data-stu-id="dd077-276">It could take several minutes tooinstall and configure hello SQL Server IaaS Agent.</span></span> 

<span data-ttu-id="dd077-277">шифрование tooenable изменить hello предыдущего сценария toopass hello **EnableEncryption** параметра вместе с паролем (защищенной строки) для hello **CertificatePassword** параметра.</span><span class="sxs-lookup"><span data-stu-id="dd077-277">tooenable encryption, modify hello previous script toopass hello **EnableEncryption** parameter along with a password (secure string) for hello **CertificatePassword** parameter.</span></span> <span data-ttu-id="dd077-278">Hello следующий сценарий включает параметры автоматической архивации hello в предыдущем примере hello и добавляет шифрование.</span><span class="sxs-lookup"><span data-stu-id="dd077-278">hello following script enables hello Automated Backup settings in hello previous example and adds encryption.</span></span>

```powershell
$password = "P@ssw0rd"
$encryptionpassword = $password | ConvertTo-SecureString -AsPlainText -Force  

$autobackupconfig = New-AzureRmVMSqlServerAutoBackupConfig -Enable `
    -EnableEncryption -CertificatePassword $encryptionpassword `
    -RetentionPeriodInDays 10 -StorageContext $storage.Context `
    -ResourceGroupName $storage_resourcegroupname -BackupSystemDbs `
    -BackupScheduleType Manual -FullBackupFrequency Weekly `
    -FullBackupStartHour 20 -FullBackupWindowInHours 2 `
    -LogBackupFrequencyInMinutes 30 

Set-AzureRmVMSqlServerExtension -AutoBackupSettings $autobackupconfig `
    -VMName $vmname -ResourceGroupName $resourcegroupname
```

<span data-ttu-id="dd077-279">параметры применяются, tooconfirm [Проверка конфигурации автоматического резервного копирования hello](#verifysettings).</span><span class="sxs-lookup"><span data-stu-id="dd077-279">tooconfirm your settings are applied, [verify hello Automated Backup configuration](#verifysettings).</span></span>

### <a name="disable-automated-backup"></a><span data-ttu-id="dd077-280">Отключение автоматической архивации</span><span class="sxs-lookup"><span data-stu-id="dd077-280">Disable Automated Backup</span></span>
<span data-ttu-id="dd077-281">Автоматическое резервное копирование, выполнения hello же сценарий, не hello toodisable **-включить** toohello параметр **New AzureRmVMSqlServerAutoBackupConfig** команды.</span><span class="sxs-lookup"><span data-stu-id="dd077-281">toodisable Automated Backup, run hello same script without hello **-Enable** parameter toohello **New-AzureRmVMSqlServerAutoBackupConfig** command.</span></span> <span data-ttu-id="dd077-282">Здравствуйте, отсутствие hello **-включить** функции hello toodisable команда hello параметров сигналы.</span><span class="sxs-lookup"><span data-stu-id="dd077-282">hello absence of hello **-Enable** parameter signals hello command toodisable hello feature.</span></span> <span data-ttu-id="dd077-283">Как и установка, может занять несколько минут toodisable автоматическое резервное копирование.</span><span class="sxs-lookup"><span data-stu-id="dd077-283">As with installation, it can take several minutes toodisable Automated Backup.</span></span>

```powershell
$autobackupconfig = New-AzureRmVMSqlServerAutoBackupConfig -ResourceGroupName $storage_resourcegroupname

Set-AzureRmVMSqlServerExtension -AutoBackupSettings $autobackupconfig `
    -VMName $vmname -ResourceGroupName $resourcegroupname
```

### <a name="example-script"></a><span data-ttu-id="dd077-284">Пример сценария</span><span class="sxs-lookup"><span data-stu-id="dd077-284">Example script</span></span>
<span data-ttu-id="dd077-285">Hello следующий скрипт предоставляет набор переменных, можно настроить tooenable и настройки автоматического резервного копирования для виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="dd077-285">hello following script provides a set of variables that you can customize tooenable and configure Automated Backup for your VM.</span></span> <span data-ttu-id="dd077-286">В вашем случае может потребоваться toocustomize hello скрипт на основе требований.</span><span class="sxs-lookup"><span data-stu-id="dd077-286">In your case, you might need toocustomize hello script based on your requirements.</span></span> <span data-ttu-id="dd077-287">Например можно иметь toomake изменения, если требуется, чтобы toodisable hello резервное копирование системных баз данных или включить шифрование.</span><span class="sxs-lookup"><span data-stu-id="dd077-287">For example, you would have toomake changes if you wanted toodisable hello backup of system databases or enable encryption.</span></span>

```powershell
$vmname = "yourvmname"
$resourcegroupname = "vmresourcegroupname"
$region = “Azure region name such as EASTUS2”
$storage_accountname = “storageaccountname”
$storage_resourcegroupname = $resourcegroupname
$retentionperiod = 10
$backupscheduletype = "Manual"
$fullbackupfrequency = "Weekly"
$fullbackupstarthour = "20"
$fullbackupwindow = "2"
$logbackupfrequency = "30"

# ResourceGroupName is hello resource group which is hosting hello VM where you are deploying hello SQL IaaS Extension 

Set-AzureRmVMSqlServerExtension -VMName $vmname `
    -ResourceGroupName $resourcegroupname -Name "SQLIaasExtension" `
    -Version "1.2" -Location $region

# Creates/use a storage account toostore hello backups

$storage = Get-AzureRmStorageAccount -ResourceGroupName $resourcegroupname `
    -Name $storage_accountname -ErrorAction SilentlyContinue
If (-Not $storage)
    { $storage = New-AzureRmStorageAccount -ResourceGroupName $storage_resourcegroupname `
    -Name $storage_accountname -SkuName Standard_GRS -Location $region }

# Configure Automated Backup settings

$autobackupconfig = New-AzureRmVMSqlServerAutoBackupConfig -Enable `
    -RetentionPeriodInDays $retentionperiod -StorageContext $storage.Context `
    -ResourceGroupName $storage_resourcegroupname -BackupSystemDbs `
    -BackupScheduleType $backupscheduletype -FullBackupFrequency $fullbackupfrequency `
    -FullBackupStartHour $fullbackupstarthour -FullBackupWindowInHours $fullbackupwindow `
    -LogBackupFrequencyInMinutes $logbackupfrequency

# Apply hello Automated Backup settings toohello VM

Set-AzureRmVMSqlServerExtension -AutoBackupSettings $autobackupconfig `
    -VMName $vmname -ResourceGroupName $resourcegroupname
```

## <a name="next-steps"></a><span data-ttu-id="dd077-288">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="dd077-288">Next steps</span></span>
<span data-ttu-id="dd077-289">Служба автоматической архивации версии 2 позволяет настроить управляемую архивацию на виртуальных машинах Azure.</span><span class="sxs-lookup"><span data-stu-id="dd077-289">Automated Backup v2 configures Managed Backup on Azure VMs.</span></span> <span data-ttu-id="dd077-290">Поэтому важно слишком[документации hello управляемого резервного копирования](https://msdn.microsoft.com/library/dn449496.aspx) toounderstand hello влияние и поведение.</span><span class="sxs-lookup"><span data-stu-id="dd077-290">So it is important too[review hello documentation for Managed Backup](https://msdn.microsoft.com/library/dn449496.aspx) toounderstand hello behavior and implications.</span></span>

<span data-ttu-id="dd077-291">Можно найти созданием резервных копий и восстановление руководство по SQL Server на виртуальных машинах Azure в разделе hello: [резервное копирование и восстановление для SQL Server в виртуальных машинах Azure](virtual-machines-windows-sql-backup-recovery.md).</span><span class="sxs-lookup"><span data-stu-id="dd077-291">You can find additional backup and restore guidance for SQL Server on Azure VMs in hello following topic: [Backup and Restore for SQL Server in Azure Virtual Machines](virtual-machines-windows-sql-backup-recovery.md).</span></span>

<span data-ttu-id="dd077-292">Сведения о других доступных задачах автоматизации см. в разделе [Расширение агента IaaS для SQL Server](virtual-machines-windows-sql-server-agent-extension.md).</span><span class="sxs-lookup"><span data-stu-id="dd077-292">For information about other available automation tasks, see [SQL Server IaaS Agent Extension](virtual-machines-windows-sql-server-agent-extension.md).</span></span>

<span data-ttu-id="dd077-293">Дополнительные сведения о запуске SQL Server на виртуальных машинах Azure см. в [обзоре использования SQL Server на виртуальных машинах Azure](virtual-machines-windows-sql-server-iaas-overview.md).</span><span class="sxs-lookup"><span data-stu-id="dd077-293">For more information about running SQL Server on Azure VMs, see [SQL Server on Azure Virtual Machines overview](virtual-machines-windows-sql-server-iaas-overview.md).</span></span>

