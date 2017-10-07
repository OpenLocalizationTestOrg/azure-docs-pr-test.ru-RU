---
title: "aaaDesired конфигурации состояния Обзор Azure | Документы Microsoft"
description: "Обзор использования hello обработчик расширений Microsoft Azure для настройки требуемого состояния PowerShell. В ней описаны обязательные требования, архитектура, командлеты и многое другое."
services: virtual-machines-windows
documentationcenter: 
author: zjalexander
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager
keywords: 
ms.assetid: bbacbc93-1e7b-4611-a3ec-e3320641f9ba
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: na
ms.date: 01/09/2017
ms.author: zachal
ms.openlocfilehash: b0337a2f1124f35e5e40c1478bd7530427e59d44
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-toohello-azure-desired-state-configuration-extension-handler"></a><span data-ttu-id="76a32-104">Обработчик расширений Azure настройки требуемого состояния toohello введение</span><span class="sxs-lookup"><span data-stu-id="76a32-104">Introduction toohello Azure Desired State Configuration extension handler</span></span>
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

<span data-ttu-id="76a32-105">Hello агент ВМ и связанные с ним расширения являются частью hello службах инфраструктуры Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="76a32-105">hello Azure VM Agent and associated Extensions are part of hello Microsoft Azure Infrastructure Services.</span></span> <span data-ttu-id="76a32-106">Расширения ВМ — программные компоненты, расширяющие функциональные возможности виртуальной Машины hello и упрощения различные операции управления виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="76a32-106">VM Extensions are software components that extend hello VM functionality and simplify various VM management operations.</span></span> <span data-ttu-id="76a32-107">Например, hello расширения VMAccess можно использовать tooreset пароль администратора или hello пользовательский сценарий используется tooexecute сценария на hello виртуальная машина может иметь расширение.</span><span class="sxs-lookup"><span data-stu-id="76a32-107">For example, hello VMAccess extension can be used tooreset an administrator's password, or hello Custom Script extension can be used tooexecute a script on hello VM.</span></span>

<span data-ttu-id="76a32-108">В этой статье описаны hello расширения конфигурации требуемого состояния PowerShell (DSC) для виртуальных машин Azure в рамках hello Azure PowerShell SDK.</span><span class="sxs-lookup"><span data-stu-id="76a32-108">This article introduces hello PowerShell Desired State Configuration (DSC) Extension for Azure VMs as part of hello Azure PowerShell SDK.</span></span> <span data-ttu-id="76a32-109">Можно использовать новые командлеты tooupload и применение конфигурации PowerShell DSC на виртуальной Машине Azure включено с hello расширение PowerShell DSC.</span><span class="sxs-lookup"><span data-stu-id="76a32-109">You can use new cmdlets tooupload and apply a PowerShell DSC configuration on an Azure VM enabled with hello PowerShell DSC extension.</span></span> <span data-ttu-id="76a32-110">вызовы расширение PowerShell DSC Hello в PowerShell DSC tooenact hello полученную конфигурацию DSC на hello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="76a32-110">hello PowerShell DSC extension calls into PowerShell DSC tooenact hello received DSC configuration on hello VM.</span></span> <span data-ttu-id="76a32-111">Эта функция также доступна через портал Azure hello.</span><span class="sxs-lookup"><span data-stu-id="76a32-111">This functionality is also available through hello Azure portal.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="76a32-112">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="76a32-112">Prerequisites</span></span>
<span data-ttu-id="76a32-113">**Локальный компьютер** toointeract с Здравствуйте расширения виртуальной Машины Windows Azure, необходимо либо hello портал Azure toouse или hello Azure PowerShell SDK.</span><span class="sxs-lookup"><span data-stu-id="76a32-113">**Local machine** toointeract with hello Azure VM extension, you need toouse either hello Azure portal or hello Azure PowerShell SDK.</span></span> 

<span data-ttu-id="76a32-114">**Гостевой агент** hello виртуальной Машине Azure, настроенный в конфигурации hello DSC должен toobe ОС, которая поддерживает либо Windows Management Framework (WMF) 4.0 и 5.0.</span><span class="sxs-lookup"><span data-stu-id="76a32-114">**Guest Agent** hello Azure VM that is configured by hello DSC configuration needs toobe an OS that supports either Windows Management Framework (WMF) 4.0 or 5.0.</span></span> <span data-ttu-id="76a32-115">Hello полный список поддерживаемых версий операционной системы можно найти в hello [журнал версий расширения DSC](https://blogs.msdn.microsoft.com/powershell/2014/11/20/release-history-for-the-azure-dsc-extension/).</span><span class="sxs-lookup"><span data-stu-id="76a32-115">hello full list of supported OS versions can be found at hello [DSC Extension Version History](https://blogs.msdn.microsoft.com/powershell/2014/11/20/release-history-for-the-azure-dsc-extension/).</span></span>

## <a name="terms-and-concepts"></a><span data-ttu-id="76a32-116">Термины и основные понятия</span><span class="sxs-lookup"><span data-stu-id="76a32-116">Terms and concepts</span></span>
<span data-ttu-id="76a32-117">Это руководство предполагает знание hello следующие понятия:</span><span class="sxs-lookup"><span data-stu-id="76a32-117">This guide presumes familiarity with hello following concepts:</span></span>

<span data-ttu-id="76a32-118">Конфигурация — документ конфигурации DSC.</span><span class="sxs-lookup"><span data-stu-id="76a32-118">Configuration - A DSC configuration document.</span></span> 

<span data-ttu-id="76a32-119">Узел — целевой объект для конфигурации DSC.</span><span class="sxs-lookup"><span data-stu-id="76a32-119">Node - A target for a DSC configuration.</span></span> <span data-ttu-id="76a32-120">В этом документе «узел» всегда ссылается tooan виртуальной Машине Azure.</span><span class="sxs-lookup"><span data-stu-id="76a32-120">In this document, "node" always refers tooan Azure VM.</span></span>

<span data-ttu-id="76a32-121">Данные конфигурации — PSD1-файл, содержащий данные среды для конфигурации.</span><span class="sxs-lookup"><span data-stu-id="76a32-121">Configuration Data - A .psd1 file containing environmental data for a configuration</span></span>

## <a name="architectural-overview"></a><span data-ttu-id="76a32-122">Основные сведения об архитектуре</span><span class="sxs-lookup"><span data-stu-id="76a32-122">Architectural overview</span></span>
<span data-ttu-id="76a32-123">Hello расширение Azure DSC использует toodeliver framework hello агента ВМ Azure, применения и отчет о конфигурации DSC, работающих на виртуальных машинах Azure.</span><span class="sxs-lookup"><span data-stu-id="76a32-123">hello Azure DSC extension uses hello Azure VM Agent framework toodeliver, enact, and report on DSC configurations running on Azure VMs.</span></span> <span data-ttu-id="76a32-124">Hello расширение DSC ожидает ZIP-файл, содержащий по крайней мере в документе конфигурации и набор параметров предоставляется посредством hello Azure PowerShell SDK или hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="76a32-124">hello DSC extension expects a .zip file containing at least a configuration document, and a set of parameters provided either through hello Azure PowerShell SDK or through hello Azure portal.</span></span>

<span data-ttu-id="76a32-125">Расширение hello вызывается для hello первый раз, запускается процесс установки.</span><span class="sxs-lookup"><span data-stu-id="76a32-125">When hello extension is called for hello first time, it runs an installation process.</span></span> <span data-ttu-id="76a32-126">Этот процесс устанавливает версию hello Windows Management Framework (WMF) с помощью hello следующая логика:</span><span class="sxs-lookup"><span data-stu-id="76a32-126">This process installs a version of hello Windows Management Framework (WMF) using hello following logic:</span></span>

1. <span data-ttu-id="76a32-127">Если hello Azure ОС виртуальной Машины Windows Server 2016, никакие действия не выполняются.</span><span class="sxs-lookup"><span data-stu-id="76a32-127">If hello Azure VM OS is Windows Server 2016, no action is taken.</span></span> <span data-ttu-id="76a32-128">Windows Server 2016 уже hello последняя установленная версия PowerShell.</span><span class="sxs-lookup"><span data-stu-id="76a32-128">Windows Server 2016 already has hello latest version of PowerShell installed.</span></span>
2. <span data-ttu-id="76a32-129">Если hello `wmfVersion` свойство указано, что hello WMF версии, если только он не совместим с ОС виртуальной Машины hello.</span><span class="sxs-lookup"><span data-stu-id="76a32-129">If hello `wmfVersion` property is specified, that version of hello WMF is installed unless it is incompatible with hello VM's OS.</span></span>
3. <span data-ttu-id="76a32-130">Если не `wmfVersion` свойство указано, hello последние применимые hello WMF версии.</span><span class="sxs-lookup"><span data-stu-id="76a32-130">If no `wmfVersion` property is specified, hello latest applicable version of hello WMF is installed.</span></span>

<span data-ttu-id="76a32-131">Установка hello WMF требуется перезагрузка.</span><span class="sxs-lookup"><span data-stu-id="76a32-131">Installation of hello WMF requires a reboot.</span></span> <span data-ttu-id="76a32-132">После перезагрузки, расширение hello загружает hello ZIP-файл, указанный в hello `modulesUrl` свойство.</span><span class="sxs-lookup"><span data-stu-id="76a32-132">After reboot, hello extension downloads hello .zip file specified in hello `modulesUrl` property.</span></span> <span data-ttu-id="76a32-133">Если это расположение находится в хранилище больших двоичных объектов, маркер SAS может быть указан в hello `sasToken` tooaccess свойство hello файла.</span><span class="sxs-lookup"><span data-stu-id="76a32-133">If this location is in Azure blob storage, a SAS token can be specified in hello `sasToken` property tooaccess hello file.</span></span> <span data-ttu-id="76a32-134">После загрузки и распаковать hello .zip, hello функцию конфигурации, определенные в `configurationFunction` выполняется toogenerate hello MOF-файл.</span><span class="sxs-lookup"><span data-stu-id="76a32-134">After hello .zip is downloaded and unpacked, hello configuration function defined in `configurationFunction` is run toogenerate hello MOF file.</span></span> <span data-ttu-id="76a32-135">расширение Hello запускает `Start-DscConfiguration -Force` on hello созданный MOF-файл.</span><span class="sxs-lookup"><span data-stu-id="76a32-135">hello extension then runs `Start-DscConfiguration -Force` on hello generated MOF file.</span></span> <span data-ttu-id="76a32-136">расширение Hello записывает выходные данные и записывает ее обратно toohello Azure состояние канала.</span><span class="sxs-lookup"><span data-stu-id="76a32-136">hello extension captures output and writes it back out toohello Azure Status Channel.</span></span> <span data-ttu-id="76a32-137">С этого момента, hello DSC LCM обрабатывает мониторинг и исправление обычным образом.</span><span class="sxs-lookup"><span data-stu-id="76a32-137">From this point on, hello DSC LCM handles monitoring and correction as normal.</span></span> 

## <a name="powershell-cmdlets"></a><span data-ttu-id="76a32-138">Командлеты PowerShell</span><span class="sxs-lookup"><span data-stu-id="76a32-138">PowerShell cmdlets</span></span>
<span data-ttu-id="76a32-139">Командлеты PowerShell можно использовать с помощью диспетчера ресурсов Azure или hello toopackage модели классическое развертывание, публикация и отслеживать развертывание расширения DSC.</span><span class="sxs-lookup"><span data-stu-id="76a32-139">PowerShell cmdlets can be used with Azure Resource Manager or hello classic deployment model toopackage, publish, and monitor DSC extension deployments.</span></span> <span data-ttu-id="76a32-140">Hello перечисленные ниже командлеты представляют Привет классическое развертывание модули, но «Azure» можно заменить «AzureRm» toouse hello Azure Resource Manager модели.</span><span class="sxs-lookup"><span data-stu-id="76a32-140">hello following cmdlets listed are hello classic deployment modules, but "Azure" can be replaced with "AzureRm" toouse hello Azure Resource Manager model.</span></span> <span data-ttu-id="76a32-141">Например `Publish-AzureVMDscConfiguration` использует hello классической модели развертывания, где `Publish-AzureRmVMDscConfiguration` использует диспетчера ресурсов Azure.</span><span class="sxs-lookup"><span data-stu-id="76a32-141">For example,  `Publish-AzureVMDscConfiguration` uses hello classic deployment model, where `Publish-AzureRmVMDscConfiguration` uses Azure Resource Manager.</span></span> 

<span data-ttu-id="76a32-142">`Publish-AzureVMDscConfiguration`Вставляет в файл конфигурации, ищет зависимые ресурсы DSC и создает ZIP-файл, содержащий конфигурации hello и конфигурации hello tooenact необходимые ресурсы DSC.</span><span class="sxs-lookup"><span data-stu-id="76a32-142">`Publish-AzureVMDscConfiguration` takes in a configuration file, scans it for dependent DSC resources, and creates a .zip file containing hello configuration and DSC resources needed tooenact hello configuration.</span></span> <span data-ttu-id="76a32-143">Его можно также создать hello локально с помощью hello `-ConfigurationArchivePath` параметра.</span><span class="sxs-lookup"><span data-stu-id="76a32-143">It can also create hello package locally using hello `-ConfigurationArchivePath` parameter.</span></span> <span data-ttu-id="76a32-144">В противном случае публикует хранилища больших двоичных объектов tooAzure файла .zip hello и защищает его с помощью токена SAS.</span><span class="sxs-lookup"><span data-stu-id="76a32-144">Otherwise, it publishes hello .zip file tooAzure blob storage and secures it with a SAS token.</span></span>

<span data-ttu-id="76a32-145">Hello ZIP-файл, созданных этим командлетом имеет hello ps1-скрипт конфигурации на корень hello hello архивной папки.</span><span class="sxs-lookup"><span data-stu-id="76a32-145">hello .zip file created by this cmdlet has hello .ps1 configuration script at hello root of hello archive folder.</span></span> <span data-ttu-id="76a32-146">Ресурсы имеют папке модуля hello помещены в архив hello.</span><span class="sxs-lookup"><span data-stu-id="76a32-146">Resources have hello module folder placed in hello archive folder.</span></span> 

<span data-ttu-id="76a32-147">`Set-AzureVMDscExtension`внедряет hello параметры, необходимые hello расширение PowerShell DSC в объект конфигурации виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="76a32-147">`Set-AzureVMDscExtension` injects hello settings needed by hello PowerShell DSC extension into a VM configuration object.</span></span> <span data-ttu-id="76a32-148">В hello классической модели развертывания, изменения hello ВМ должен быть применен tooan ВМ Azure с `Update-AzureVM`.</span><span class="sxs-lookup"><span data-stu-id="76a32-148">In hello classic deployment model, hello VM changes must be applied tooan Azure VM with `Update-AzureVM`.</span></span> 

<span data-ttu-id="76a32-149">`Get-AzureVMDscExtension`Извлекает состояние расширения DSC hello конкретной виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="76a32-149">`Get-AzureVMDscExtension` retrieves hello DSC extension status of a particular VM.</span></span> 

<span data-ttu-id="76a32-150">`Get-AzureVMDscExtensionStatus`Извлекает состояние hello hello конфигурации DSC, активированная обработчиком расширения DSC hello.</span><span class="sxs-lookup"><span data-stu-id="76a32-150">`Get-AzureVMDscExtensionStatus` retrieves hello status of hello DSC configuration enacted by hello DSC extension handler.</span></span> <span data-ttu-id="76a32-151">Это действие может выполняться с одной виртуальной машиной или с группой виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="76a32-151">This action can be performed on a single VM, or group of VMs.</span></span>

<span data-ttu-id="76a32-152">`Remove-AzureVMDscExtension`Удаляет обработчик расширения hello данной виртуальной машине.</span><span class="sxs-lookup"><span data-stu-id="76a32-152">`Remove-AzureVMDscExtension` removes hello extension handler from a given virtual machine.</span></span> <span data-ttu-id="76a32-153">Этот командлет не **не** удалить конфигурацию hello, удалите hello WMF или изменить параметры hello применения на виртуальной машине hello.</span><span class="sxs-lookup"><span data-stu-id="76a32-153">This cmdlet does **not** remove hello configuration, uninstall hello WMF, or change hello applied settings on hello virtual machine.</span></span> <span data-ttu-id="76a32-154">Удаляет только обработчик расширений hello.</span><span class="sxs-lookup"><span data-stu-id="76a32-154">It only removes hello extension handler.</span></span> 

<span data-ttu-id="76a32-155">**Основные отличия между командлетами для ASM и Azure Resource Manager**</span><span class="sxs-lookup"><span data-stu-id="76a32-155">**Key differences in ASM and Azure Resource Manager cmdlets**</span></span>

* <span data-ttu-id="76a32-156">Командлеты Azure Resource Manager выполняются синхронно.</span><span class="sxs-lookup"><span data-stu-id="76a32-156">Azure Resource Manager cmdlets are synchronous.</span></span> <span data-ttu-id="76a32-157">а командлеты ASM — асинхронными.</span><span class="sxs-lookup"><span data-stu-id="76a32-157">ASM cmdlets are asynchronous.</span></span>
* <span data-ttu-id="76a32-158">ResourceGroupName, VMName, ArchiveStorageAccountName, Version, Location — это обязательные параметры в Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="76a32-158">ResourceGroupName, VMName, ArchiveStorageAccountName, Version, and Location are all required parameters in Azure Resource Manager.</span></span>
* <span data-ttu-id="76a32-159">ArchiveResourceGroupName — новый необязательный параметр для Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="76a32-159">ArchiveResourceGroupName is a new optional parameter for Azure Resource Manager.</span></span> <span data-ttu-id="76a32-160">Этот параметр можно указать, когда учетной записи хранилища относится tooa группы ресурсов, отличной от hello один, где создается виртуальная машина hello.</span><span class="sxs-lookup"><span data-stu-id="76a32-160">You can specify this parameter when your storage account belongs tooa different resource group than hello one where hello virtual machine is created.</span></span>
* <span data-ttu-id="76a32-161">ConfigurationArchive — это ArchiveBlobName в Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="76a32-161">ConfigurationArchive is called ArchiveBlobName in Azure Resource Manager</span></span>
* <span data-ttu-id="76a32-162">ContainerName — это ArchiveContainerName в Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="76a32-162">ContainerName is called ArchiveContainerName in Azure Resource Manager</span></span>
* <span data-ttu-id="76a32-163">StorageEndpointSuffix — это ArchiveStorageEndpointSuffix в Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="76a32-163">StorageEndpointSuffix is called ArchiveStorageEndpointSuffix in Azure Resource Manager</span></span>
* <span data-ttu-id="76a32-164">Hello AutoUpdate добавлен параметр tooAzure tooenable диспетчера ресурсов, автоматическое обновление hello расширение обработчика toohello последнюю версию, что и если оно доступно.</span><span class="sxs-lookup"><span data-stu-id="76a32-164">hello AutoUpdate switch has been added tooAzure Resource Manager tooenable automatic updating of hello extension handler toohello latest version as and when it is available.</span></span> <span data-ttu-id="76a32-165">Обратите внимание, что этот параметр имеет hello возможны перезагрузки toocause hello виртуальной Машины, когда новая версия выпуска WMF hello.</span><span class="sxs-lookup"><span data-stu-id="76a32-165">Note this parameter has hello potential toocause reboots on hello VM when a new version of hello WMF is released.</span></span> 

## <a name="azure-portal-functionality"></a><span data-ttu-id="76a32-166">Использование портала Azure</span><span class="sxs-lookup"><span data-stu-id="76a32-166">Azure portal functionality</span></span>
<span data-ttu-id="76a32-167">Обзор tooa виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="76a32-167">Browse tooa VM.</span></span> <span data-ttu-id="76a32-168">В разделе "Параметры" > "Общие" щелкните "Расширения".</span><span class="sxs-lookup"><span data-stu-id="76a32-168">Under Settings -> General click "Extensions."</span></span> <span data-ttu-id="76a32-169">Будет создана новая панель.</span><span class="sxs-lookup"><span data-stu-id="76a32-169">A new pane is created.</span></span> <span data-ttu-id="76a32-170">Щелкните "Добавить" и выберите DSC PowerShell.</span><span class="sxs-lookup"><span data-stu-id="76a32-170">Click "Add" and select PowerShell DSC.</span></span>

<span data-ttu-id="76a32-171">портал Hello должен входных данных.</span><span class="sxs-lookup"><span data-stu-id="76a32-171">hello portal needs input.</span></span>
<span data-ttu-id="76a32-172">**Configuration Modules or Script**(Модули или сценарий конфигурации) — обязательное поле.</span><span class="sxs-lookup"><span data-stu-id="76a32-172">**Configuration Modules or Script**: This field is mandatory.</span></span> <span data-ttu-id="76a32-173">Требуется ps1-файл, содержащий сценарий конфигурации или ZIP-файл с помощью сценария конфигурации .ps1 корне hello и все зависимые ресурсы в папках модуля в пределах hello .zip.</span><span class="sxs-lookup"><span data-stu-id="76a32-173">Requires a .ps1 file containing a configuration script, or a .zip file with a .ps1 configuration script at hello root, and all dependent resources in module folders within hello .zip.</span></span> <span data-ttu-id="76a32-174">Он может быть создан с hello `Publish-AzureVMDscConfiguration -ConfigurationArchivePath` командлетов, включенных в пакет SDK для Azure PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="76a32-174">It can be created with hello `Publish-AzureVMDscConfiguration -ConfigurationArchivePath` cmdlet included in hello Azure PowerShell SDK.</span></span> <span data-ttu-id="76a32-175">ZIP-файл Hello передаются в хранилище BLOB-объектов пользователя, защищенным с помощью маркера SAS.</span><span class="sxs-lookup"><span data-stu-id="76a32-175">hello .zip file is uploaded into your user blob storage secured by a SAS token.</span></span> 

<span data-ttu-id="76a32-176">**Configuration Data PSD1 File**(PSD1-файл данных конфигурации) — необязательное поле.</span><span class="sxs-lookup"><span data-stu-id="76a32-176">**Configuration Data PSD1 File**: This field is optional.</span></span> <span data-ttu-id="76a32-177">Если конфигурации требуется файл данных конфигурации в .psd1, используйте это поле tooselect его и отправьте его в хранилище больших двоичных объектов tooyour пользователя, где он защищен с помощью маркера SAS.</span><span class="sxs-lookup"><span data-stu-id="76a32-177">If your configuration requires a configuration data file in .psd1, use this field tooselect it and upload it tooyour user blob storage, where it is secured by a SAS token.</span></span> 

<span data-ttu-id="76a32-178">**Module-Qualified Name of Configuration**(Полное имя модуля конфигурации) — PS1-файлы могут включать в себя несколько функций конфигурации.</span><span class="sxs-lookup"><span data-stu-id="76a32-178">**Module-Qualified Name of Configuration**: .ps1 files can have multiple configuration functions.</span></span> <span data-ttu-id="76a32-179">Введите имя hello скрипт .ps1 конфигурации hello, за которым следует "\' и hello имя функции hello конфигурации.</span><span class="sxs-lookup"><span data-stu-id="76a32-179">Enter hello name of hello configuration .ps1 script followed by a  '\' and hello name of hello configuration function.</span></span> <span data-ttu-id="76a32-180">Например если ps1-скрипт имеет hello имя «configuration.ps1», а конфигурация hello — «IisInstall», введите:`configuration.ps1\IisInstall`</span><span class="sxs-lookup"><span data-stu-id="76a32-180">For example, if your .ps1 script has hello name "configuration.ps1", and hello configuration is "IisInstall", you would enter: `configuration.ps1\IisInstall`</span></span>

<span data-ttu-id="76a32-181">**Аргументы конфигурации**: Если функция конфигурации hello принимает аргументы, укажите их здесь в формате hello `argumentName1=value1,argumentName2=value2`.</span><span class="sxs-lookup"><span data-stu-id="76a32-181">**Configuration Arguments**: If hello configuration function takes arguments, enter them in here in hello format `argumentName1=value1,argumentName2=value2`.</span></span> <span data-ttu-id="76a32-182">Обратите внимание, что этот формат отличается от того, в котором аргументы конфигурации принимаются через командлеты PowerShell или шаблоны Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="76a32-182">Note this format is a different format than how configuration arguments are accepted through PowerShell cmdlets or Resource Manager templates.</span></span> 

## <a name="getting-started"></a><span data-ttu-id="76a32-183">Приступая к работе</span><span class="sxs-lookup"><span data-stu-id="76a32-183">Getting started</span></span>
<span data-ttu-id="76a32-184">расширение Azure DSC Hello принимает документы конфигурации DSC и их применения на виртуальных машинах Azure.</span><span class="sxs-lookup"><span data-stu-id="76a32-184">hello Azure DSC extension takes in DSC configuration documents and enacts them on Azure VMs.</span></span> <span data-ttu-id="76a32-185">Ниже приведен простой пример конфигурации.</span><span class="sxs-lookup"><span data-stu-id="76a32-185">A simple example of a configuration follows.</span></span> <span data-ttu-id="76a32-186">Сохраните его локально как файл IisInstall.ps1.</span><span class="sxs-lookup"><span data-stu-id="76a32-186">Save it locally as "IisInstall.ps1":</span></span>

```powershell
configuration IISInstall 
{ 
    node "localhost"
    { 
        WindowsFeature IIS 
        { 
            Ensure = "Present" 
            Name = "Web-Server"                       
        } 
    } 
}
```

<span data-ttu-id="76a32-187">следующие шаги месте hello IisInstall.ps1 скрипт на hello Hello указан виртуальной Машины, выполнить конфигурацию hello и выдавать отчеты о состоянии.</span><span class="sxs-lookup"><span data-stu-id="76a32-187">hello following steps place hello IisInstall.ps1 script on hello specified VM, execute hello configuration, and report back on status.</span></span>
###<a name="classic-model"></a><span data-ttu-id="76a32-188">Классическая модель</span><span class="sxs-lookup"><span data-stu-id="76a32-188">Classic model</span></span>
```powershell
#Azure PowerShell cmdlets are required
Import-Module Azure

#Use an existing Azure Virtual Machine, 'DscDemo1'
$demoVM = Get-AzureVM DscDemo1

#Publish hello configuration script into user storage.
Publish-AzureVMDscConfiguration -ConfigurationPath ".\IisInstall.ps1" -StorageContext $storageContext -Verbose -Force

#Set hello VM toorun hello DSC configuration
Set-AzureVMDscExtension -VM $demoVM -ConfigurationArchive "IisInstall.ps1.zip" -StorageContext $storageContext -ConfigurationName "IisInstall" -Verbose

#Update hello configuration of an Azure Virtual Machine
$demoVM | Update-AzureVM -Verbose

#check on status
Get-AzureVMDscExtensionStatus -VM $demovm -Verbose
```
###<a name="azure-resource-manager-model"></a><span data-ttu-id="76a32-189">Модель Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="76a32-189">Azure Resource Manager model</span></span>

```powershell
$resourceGroup = "dscVmDemo"
$location = "westus"
$vmName = "myVM"
$storageName = "demostorage"
#Publish hello configuration script into user storage
Publish-AzureRmVMDscConfiguration -ConfigurationPath .\iisInstall.ps1 -ResourceGroupName $resourceGroup -StorageAccountName $storageName -force
#Set hello VM toorun hello DSC configuration
Set-AzureRmVmDscExtension -Version 2.21 -ResourceGroupName $resourceGroup -VMName $vmName -ArchiveStorageAccountName $storageName -ArchiveBlobName iisInstall.ps1.zip -AutoUpdate:$true -ConfigurationName "IISInstall"

```

## <a name="logging"></a><span data-ttu-id="76a32-190">Ведение журналов</span><span class="sxs-lookup"><span data-stu-id="76a32-190">Logging</span></span>
<span data-ttu-id="76a32-191">Журналы размещаются в следующем каталоге:</span><span class="sxs-lookup"><span data-stu-id="76a32-191">Logs are placed in:</span></span>

<span data-ttu-id="76a32-192">C:\WindowsAzure\Logs\Plugins\Microsoft.Powershell.DSC\[номер версии]</span><span class="sxs-lookup"><span data-stu-id="76a32-192">C:\WindowsAzure\Logs\Plugins\Microsoft.Powershell.DSC\[Version Number]</span></span>

## <a name="next-steps"></a><span data-ttu-id="76a32-193">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="76a32-193">Next steps</span></span>
<span data-ttu-id="76a32-194">Дополнительные сведения о PowerShell DSC [посетите центр документации PowerShell hello](https://msdn.microsoft.com/powershell/dsc/overview).</span><span class="sxs-lookup"><span data-stu-id="76a32-194">For more information about PowerShell DSC, [visit hello PowerShell documentation center](https://msdn.microsoft.com/powershell/dsc/overview).</span></span> 

<span data-ttu-id="76a32-195">Изучите hello [шаблона Azure Resource Manager для расширения hello DSC](extensions-dsc-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="76a32-195">Examine hello [Azure Resource Manager template for hello DSC extension](extensions-dsc-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> 

<span data-ttu-id="76a32-196">Дополнительные функциональные возможности toofind можно управлять с помощью PowerShell DSC [Обзор коллекции PowerShell hello](https://www.powershellgallery.com/packages?q=DscResource&x=0&y=0) дополнительные ресурсы DSC.</span><span class="sxs-lookup"><span data-stu-id="76a32-196">toofind additional functionality you can manage with PowerShell DSC, [browse hello PowerShell gallery](https://www.powershellgallery.com/packages?q=DscResource&x=0&y=0) for more DSC resources.</span></span>

<span data-ttu-id="76a32-197">Дополнительные сведения о передаче конфиденциальные параметры в конфигурации в разделе [управление учетными данными безопасно с обработчиком расширения hello DSC](extensions-dsc-credentials.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="76a32-197">For details on passing sensitive parameters into configurations, see [Manage credentials securely with hello DSC extension handler](extensions-dsc-credentials.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

