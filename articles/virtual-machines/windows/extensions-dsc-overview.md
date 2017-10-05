---
title: "Общие сведения о настройке требуемого состояния для Azure | Документация Майкрософт"
description: "Эта статья содержит общие сведения о работе с расширением Desired State Configuration PowerShell с помощью обработчика расширений Microsoft Azure. В ней описаны обязательные требования, архитектура, командлеты и многое другое."
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
ms.openlocfilehash: c05c2d541a5f526f362f9cd72fe6d878374112b6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="introduction-to-the-azure-desired-state-configuration-extension-handler"></a><span data-ttu-id="1833f-104">Общие сведения об обработчике расширения Desired State Configuration в Azure</span><span class="sxs-lookup"><span data-stu-id="1833f-104">Introduction to the Azure Desired State Configuration extension handler</span></span>
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

<span data-ttu-id="1833f-105">Агент VM Azure и связанные расширения являются частью служб инфраструктуры Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="1833f-105">The Azure VM Agent and associated Extensions are part of the Microsoft Azure Infrastructure Services.</span></span> <span data-ttu-id="1833f-106">Расширения виртуальной машины — это программные компоненты, которые расширяют функциональные возможности виртуальной машины и упрощают различные операции управления ею.</span><span class="sxs-lookup"><span data-stu-id="1833f-106">VM Extensions are software components that extend the VM functionality and simplify various VM management operations.</span></span> <span data-ttu-id="1833f-107">Например, расширение VMAccess позволяет сбросить пароль администратора, а расширение пользовательских сценариев можно использовать для выполнения сценария на виртуальной машине.</span><span class="sxs-lookup"><span data-stu-id="1833f-107">For example, the VMAccess extension can be used to reset an administrator's password, or the Custom Script extension can be used to execute a script on the VM.</span></span>

<span data-ttu-id="1833f-108">В этой статье описано расширение PowerShell Desired State Configuration (DSC) для виртуальных машин Azure, которое входит в пакет SDK для Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="1833f-108">This article introduces the PowerShell Desired State Configuration (DSC) Extension for Azure VMs as part of the Azure PowerShell SDK.</span></span> <span data-ttu-id="1833f-109">С помощью новых командлетов вы можете передать и применить конфигурацию DSC PowerShell на виртуальной машине Azure, на которой включено расширение DSC PowerShell.</span><span class="sxs-lookup"><span data-stu-id="1833f-109">You can use new cmdlets to upload and apply a PowerShell DSC configuration on an Azure VM enabled with the PowerShell DSC extension.</span></span> <span data-ttu-id="1833f-110">Расширение DSC PowerShell вызывает DSC PowerShell, чтобы применить полученную конфигурацию DSC к виртуальной машине.</span><span class="sxs-lookup"><span data-stu-id="1833f-110">The PowerShell DSC extension calls into PowerShell DSC to enact the received DSC configuration on the VM.</span></span> <span data-ttu-id="1833f-111">Эта функция доступна также на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="1833f-111">This functionality is also available through the Azure portal.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1833f-112">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="1833f-112">Prerequisites</span></span>
<span data-ttu-id="1833f-113">**Локальный компьютер.** Для взаимодействия с расширением виртуальной машины Azure нужно использовать портал Azure или пакет SDK для Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="1833f-113">**Local machine** To interact with the Azure VM extension, you need to use either the Azure portal or the Azure PowerShell SDK.</span></span> 

<span data-ttu-id="1833f-114">**Гостевой агент.** Виртуальная машина Azure, на которой применяется конфигурация DSC, должна работать под управлением ОС, которая поддерживает Windows Management Framework (WMF) 4.0 или 5.0.</span><span class="sxs-lookup"><span data-stu-id="1833f-114">**Guest Agent** The Azure VM that is configured by the DSC configuration needs to be an OS that supports either Windows Management Framework (WMF) 4.0 or 5.0.</span></span> <span data-ttu-id="1833f-115">Полный список поддерживаемых версий ОС можно найти в [журнале версий расширения DSC](https://blogs.msdn.microsoft.com/powershell/2014/11/20/release-history-for-the-azure-dsc-extension/).</span><span class="sxs-lookup"><span data-stu-id="1833f-115">The full list of supported OS versions can be found at the [DSC Extension Version History](https://blogs.msdn.microsoft.com/powershell/2014/11/20/release-history-for-the-azure-dsc-extension/).</span></span>

## <a name="terms-and-concepts"></a><span data-ttu-id="1833f-116">Термины и основные понятия</span><span class="sxs-lookup"><span data-stu-id="1833f-116">Terms and concepts</span></span>
<span data-ttu-id="1833f-117">Для изучения этого руководства нужно знать приведенные ниже понятия.</span><span class="sxs-lookup"><span data-stu-id="1833f-117">This guide presumes familiarity with the following concepts:</span></span>

<span data-ttu-id="1833f-118">Конфигурация — документ конфигурации DSC.</span><span class="sxs-lookup"><span data-stu-id="1833f-118">Configuration - A DSC configuration document.</span></span> 

<span data-ttu-id="1833f-119">Узел — целевой объект для конфигурации DSC.</span><span class="sxs-lookup"><span data-stu-id="1833f-119">Node - A target for a DSC configuration.</span></span> <span data-ttu-id="1833f-120">Слово "узел" в этом документе всегда означает виртуальную машину Azure.</span><span class="sxs-lookup"><span data-stu-id="1833f-120">In this document, "node" always refers to an Azure VM.</span></span>

<span data-ttu-id="1833f-121">Данные конфигурации — PSD1-файл, содержащий данные среды для конфигурации.</span><span class="sxs-lookup"><span data-stu-id="1833f-121">Configuration Data - A .psd1 file containing environmental data for a configuration</span></span>

## <a name="architectural-overview"></a><span data-ttu-id="1833f-122">Основные сведения об архитектуре</span><span class="sxs-lookup"><span data-stu-id="1833f-122">Architectural overview</span></span>
<span data-ttu-id="1833f-123">Расширение DSC Azure использует платформу агента Azure, чтобы доставлять и применять конфигурации DSC виртуальных машин Azure, а также сообщать об этих конфигурациях.</span><span class="sxs-lookup"><span data-stu-id="1833f-123">The Azure DSC extension uses the Azure VM Agent framework to deliver, enact, and report on DSC configurations running on Azure VMs.</span></span> <span data-ttu-id="1833f-124">Расширению DSC требуется ZIP-файл, содержащий по крайней мере документ конфигурации, а также набор параметров, которые передаются через пакет SDK для Azure PowerShell или портал Azure.</span><span class="sxs-lookup"><span data-stu-id="1833f-124">The DSC extension expects a .zip file containing at least a configuration document, and a set of parameters provided either through the Azure PowerShell SDK or through the Azure portal.</span></span>

<span data-ttu-id="1833f-125">Когда расширение вызывается впервые, оно запускает процесс установки.</span><span class="sxs-lookup"><span data-stu-id="1833f-125">When the extension is called for the first time, it runs an installation process.</span></span> <span data-ttu-id="1833f-126">Этот процесс устанавливает определенную версию Windows Management Framework (WMF), следуя приведенной ниже логике.</span><span class="sxs-lookup"><span data-stu-id="1833f-126">This process installs a version of the Windows Management Framework (WMF) using the following logic:</span></span>

1. <span data-ttu-id="1833f-127">Если виртуальная машина Azure работает под управлением Windows Server 2016, никакие действия не требуются,</span><span class="sxs-lookup"><span data-stu-id="1833f-127">If the Azure VM OS is Windows Server 2016, no action is taken.</span></span> <span data-ttu-id="1833f-128">потому что в Windows Server 2016 уже установлена последняя версия PowerShell.</span><span class="sxs-lookup"><span data-stu-id="1833f-128">Windows Server 2016 already has the latest version of PowerShell installed.</span></span>
2. <span data-ttu-id="1833f-129">Если указано свойство `wmfVersion`, то устанавливается соответствующая версия WMF (за исключением случаев, когда эта версия несовместима с ОС виртуальной машины).</span><span class="sxs-lookup"><span data-stu-id="1833f-129">If the `wmfVersion` property is specified, that version of the WMF is installed unless it is incompatible with the VM's OS.</span></span>
3. <span data-ttu-id="1833f-130">Если свойство `wmfVersion` не указано, то устанавливается последняя применимая версия WMF.</span><span class="sxs-lookup"><span data-stu-id="1833f-130">If no `wmfVersion` property is specified, the latest applicable version of the WMF is installed.</span></span>

<span data-ttu-id="1833f-131">Для установки WMF требуется перезагрузка.</span><span class="sxs-lookup"><span data-stu-id="1833f-131">Installation of the WMF requires a reboot.</span></span> <span data-ttu-id="1833f-132">После перезагрузки расширение скачивает ZIP-файл, указанный в свойстве `modulesUrl` .</span><span class="sxs-lookup"><span data-stu-id="1833f-132">After reboot, the extension downloads the .zip file specified in the `modulesUrl` property.</span></span> <span data-ttu-id="1833f-133">Если это расположение находится в хранилище BLOB-объектов Azure, то для доступа к файлу в свойстве `sasToken` можно указать маркер SAS.</span><span class="sxs-lookup"><span data-stu-id="1833f-133">If this location is in Azure blob storage, a SAS token can be specified in the `sasToken` property to access the file.</span></span> <span data-ttu-id="1833f-134">После скачивания и распаковки ZIP-файла функция конфигурации, определенная в `configurationFunction` , запускается и создает MOF-файл.</span><span class="sxs-lookup"><span data-stu-id="1833f-134">After the .zip is downloaded and unpacked, the configuration function defined in `configurationFunction` is run to generate the MOF file.</span></span> <span data-ttu-id="1833f-135">Затем расширение выполняет командлет `Start-DscConfiguration -Force` с созданным MOF-файлом.</span><span class="sxs-lookup"><span data-stu-id="1833f-135">The extension then runs `Start-DscConfiguration -Force` on the generated MOF file.</span></span> <span data-ttu-id="1833f-136">Расширение фиксирует выходные данные и записывает их в канал состояний Azure.</span><span class="sxs-lookup"><span data-stu-id="1833f-136">The extension captures output and writes it back out to the Azure Status Channel.</span></span> <span data-ttu-id="1833f-137">С этого момента локальный диспетчер конфигураций DSC выполняет мониторинг и обрабатывает исправления в обычном режиме.</span><span class="sxs-lookup"><span data-stu-id="1833f-137">From this point on, the DSC LCM handles monitoring and correction as normal.</span></span> 

## <a name="powershell-cmdlets"></a><span data-ttu-id="1833f-138">Командлеты PowerShell</span><span class="sxs-lookup"><span data-stu-id="1833f-138">PowerShell cmdlets</span></span>
<span data-ttu-id="1833f-139">Командлеты PowerShell можно использовать с классической моделью развертывания или моделью развертывания с помощью Azure Resource Manager, чтобы упаковывать, публиковать и отслеживать развертывания расширений DSC.</span><span class="sxs-lookup"><span data-stu-id="1833f-139">PowerShell cmdlets can be used with Azure Resource Manager or the classic deployment model to package, publish, and monitor DSC extension deployments.</span></span> <span data-ttu-id="1833f-140">Ниже приведены командлеты для классической модели развертывания, но для использования модели Azure Resource Manager часть "Azure" следует заменить на "AzureRM".</span><span class="sxs-lookup"><span data-stu-id="1833f-140">The following cmdlets listed are the classic deployment modules, but "Azure" can be replaced with "AzureRm" to use the Azure Resource Manager model.</span></span> <span data-ttu-id="1833f-141">Например, `Publish-AzureVMDscConfiguration` использует классическую модель развертывания, а `Publish-AzureRmVMDscConfiguration` — модель с Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="1833f-141">For example,  `Publish-AzureVMDscConfiguration` uses the classic deployment model, where `Publish-AzureRmVMDscConfiguration` uses Azure Resource Manager.</span></span> 

<span data-ttu-id="1833f-142">`Publish-AzureVMDscConfiguration` принимает файл конфигурации, проверяет его на наличие зависимых ресурсов DSC и создает ZIP-файл, содержащий ресурсы конфигурации и ресурсы DSC, необходимые для применения конфигурации.</span><span class="sxs-lookup"><span data-stu-id="1833f-142">`Publish-AzureVMDscConfiguration` takes in a configuration file, scans it for dependent DSC resources, and creates a .zip file containing the configuration and DSC resources needed to enact the configuration.</span></span> <span data-ttu-id="1833f-143">Этот командлет может также создать пакет локально с помощью параметра `-ConfigurationArchivePath`</span><span class="sxs-lookup"><span data-stu-id="1833f-143">It can also create the package locally using the `-ConfigurationArchivePath` parameter.</span></span> <span data-ttu-id="1833f-144">или опубликовать ZIP-файл в хранилище BLOB-объектов Azure и защитить его маркером SAS.</span><span class="sxs-lookup"><span data-stu-id="1833f-144">Otherwise, it publishes the .zip file to Azure blob storage and secures it with a SAS token.</span></span>

<span data-ttu-id="1833f-145">На корневом уровне папки архива у ZIP-файла, созданного этим командлетом, есть скрипт конфигурации в формате PS1.</span><span class="sxs-lookup"><span data-stu-id="1833f-145">The .zip file created by this cmdlet has the .ps1 configuration script at the root of the archive folder.</span></span> <span data-ttu-id="1833f-146">Предназначенная для ресурсов папка модуля находится в папке архива.</span><span class="sxs-lookup"><span data-stu-id="1833f-146">Resources have the module folder placed in the archive folder.</span></span> 

<span data-ttu-id="1833f-147">Командлет `Set-AzureVMDscExtension` внедряет параметры, необходимые расширению DSC PowerShell, в объект конфигурации виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="1833f-147">`Set-AzureVMDscExtension` injects the settings needed by the PowerShell DSC extension into a VM configuration object.</span></span> <span data-ttu-id="1833f-148">В классической модели развертывания изменения виртуальной машины применяются к виртуальной машине Azure с помощью `Update-AzureVM`.</span><span class="sxs-lookup"><span data-stu-id="1833f-148">In the classic deployment model, the VM changes must be applied to an Azure VM with `Update-AzureVM`.</span></span> 

<span data-ttu-id="1833f-149">`Get-AzureVMDscExtension` извлекает состояние расширения DSC определенной виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="1833f-149">`Get-AzureVMDscExtension` retrieves the DSC extension status of a particular VM.</span></span> 

<span data-ttu-id="1833f-150">`Get-AzureVMDscExtensionStatus` получает состояние конфигурации DSC, которое применил обработчик расширений DSC.</span><span class="sxs-lookup"><span data-stu-id="1833f-150">`Get-AzureVMDscExtensionStatus` retrieves the status of the DSC configuration enacted by the DSC extension handler.</span></span> <span data-ttu-id="1833f-151">Это действие может выполняться с одной виртуальной машиной или с группой виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="1833f-151">This action can be performed on a single VM, or group of VMs.</span></span>

<span data-ttu-id="1833f-152">`Remove-AzureVMDscExtension` удаляет обработчик расширений из определенной виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="1833f-152">`Remove-AzureVMDscExtension` removes the extension handler from a given virtual machine.</span></span> <span data-ttu-id="1833f-153">Это **не** приводит к удалению конфигурации, удалению WMF или изменению примененных параметров на виртуальной машине.</span><span class="sxs-lookup"><span data-stu-id="1833f-153">This cmdlet does **not** remove the configuration, uninstall the WMF, or change the applied settings on the virtual machine.</span></span> <span data-ttu-id="1833f-154">Удаляется только обработчик расширений.</span><span class="sxs-lookup"><span data-stu-id="1833f-154">It only removes the extension handler.</span></span> 

<span data-ttu-id="1833f-155">**Основные отличия между командлетами для ASM и Azure Resource Manager**</span><span class="sxs-lookup"><span data-stu-id="1833f-155">**Key differences in ASM and Azure Resource Manager cmdlets**</span></span>

* <span data-ttu-id="1833f-156">Командлеты Azure Resource Manager выполняются синхронно.</span><span class="sxs-lookup"><span data-stu-id="1833f-156">Azure Resource Manager cmdlets are synchronous.</span></span> <span data-ttu-id="1833f-157">а командлеты ASM — асинхронными.</span><span class="sxs-lookup"><span data-stu-id="1833f-157">ASM cmdlets are asynchronous.</span></span>
* <span data-ttu-id="1833f-158">ResourceGroupName, VMName, ArchiveStorageAccountName, Version, Location — это обязательные параметры в Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="1833f-158">ResourceGroupName, VMName, ArchiveStorageAccountName, Version, and Location are all required parameters in Azure Resource Manager.</span></span>
* <span data-ttu-id="1833f-159">ArchiveResourceGroupName — новый необязательный параметр для Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="1833f-159">ArchiveResourceGroupName is a new optional parameter for Azure Resource Manager.</span></span> <span data-ttu-id="1833f-160">Этот параметр можно указать, если ваша учетная запись хранения не принадлежит к той группе ресурсов, в которой создана виртуальная машина.</span><span class="sxs-lookup"><span data-stu-id="1833f-160">You can specify this parameter when your storage account belongs to a different resource group than the one where the virtual machine is created.</span></span>
* <span data-ttu-id="1833f-161">ConfigurationArchive — это ArchiveBlobName в Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="1833f-161">ConfigurationArchive is called ArchiveBlobName in Azure Resource Manager</span></span>
* <span data-ttu-id="1833f-162">ContainerName — это ArchiveContainerName в Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="1833f-162">ContainerName is called ArchiveContainerName in Azure Resource Manager</span></span>
* <span data-ttu-id="1833f-163">StorageEndpointSuffix — это ArchiveStorageEndpointSuffix в Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="1833f-163">StorageEndpointSuffix is called ArchiveStorageEndpointSuffix in Azure Resource Manager</span></span>
* <span data-ttu-id="1833f-164">В Azure Resource Manager добавлен параметр AutoUpdate, который позволяет автоматически обновлять обработчик расширений до последней версии сразу, когда она становится доступной.</span><span class="sxs-lookup"><span data-stu-id="1833f-164">The AutoUpdate switch has been added to Azure Resource Manager to enable automatic updating of the extension handler to the latest version as and when it is available.</span></span> <span data-ttu-id="1833f-165">Обратите внимание, что после выпуска новой версии WMF возможна перезагрузка виртуальной машины из-за данного параметра.</span><span class="sxs-lookup"><span data-stu-id="1833f-165">Note this parameter has the potential to cause reboots on the VM when a new version of the WMF is released.</span></span> 

## <a name="azure-portal-functionality"></a><span data-ttu-id="1833f-166">Использование портала Azure</span><span class="sxs-lookup"><span data-stu-id="1833f-166">Azure portal functionality</span></span>
<span data-ttu-id="1833f-167">Перейдите к виртуальной машине.</span><span class="sxs-lookup"><span data-stu-id="1833f-167">Browse to a VM.</span></span> <span data-ttu-id="1833f-168">В разделе "Параметры" > "Общие" щелкните "Расширения".</span><span class="sxs-lookup"><span data-stu-id="1833f-168">Under Settings -> General click "Extensions."</span></span> <span data-ttu-id="1833f-169">Будет создана новая панель.</span><span class="sxs-lookup"><span data-stu-id="1833f-169">A new pane is created.</span></span> <span data-ttu-id="1833f-170">Щелкните "Добавить" и выберите DSC PowerShell.</span><span class="sxs-lookup"><span data-stu-id="1833f-170">Click "Add" and select PowerShell DSC.</span></span>

<span data-ttu-id="1833f-171">Порталу нужны входные данные.</span><span class="sxs-lookup"><span data-stu-id="1833f-171">The portal needs input.</span></span>
<span data-ttu-id="1833f-172">**Configuration Modules or Script**(Модули или сценарий конфигурации) — обязательное поле.</span><span class="sxs-lookup"><span data-stu-id="1833f-172">**Configuration Modules or Script**: This field is mandatory.</span></span> <span data-ttu-id="1833f-173">Здесь следует указать PS1-файл, содержащий сценарий конфигурации, или ZIP-файл со сценарием конфигурации в формате PS1 в корне и всеми зависимыми ресурсами в папках модулей.</span><span class="sxs-lookup"><span data-stu-id="1833f-173">Requires a .ps1 file containing a configuration script, or a .zip file with a .ps1 configuration script at the root, and all dependent resources in module folders within the .zip.</span></span> <span data-ttu-id="1833f-174">Его можно создать с помощью командлета `Publish-AzureVMDscConfiguration -ConfigurationArchivePath` , входящего в пакет SDK для Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="1833f-174">It can be created with the `Publish-AzureVMDscConfiguration -ConfigurationArchivePath` cmdlet included in the Azure PowerShell SDK.</span></span> <span data-ttu-id="1833f-175">Этот ZIP-файл передается в хранилище BLOB-объектов пользователя, защищенный маркером SAS.</span><span class="sxs-lookup"><span data-stu-id="1833f-175">The .zip file is uploaded into your user blob storage secured by a SAS token.</span></span> 

<span data-ttu-id="1833f-176">**Configuration Data PSD1 File**(PSD1-файл данных конфигурации) — необязательное поле.</span><span class="sxs-lookup"><span data-stu-id="1833f-176">**Configuration Data PSD1 File**: This field is optional.</span></span> <span data-ttu-id="1833f-177">Если для вашей конфигурации требуется PSD1-файл данных конфигурации, выберите его с помощью этого поля и передайте в хранилище BLOB-объектов, где он будет защищен маркером SAS.</span><span class="sxs-lookup"><span data-stu-id="1833f-177">If your configuration requires a configuration data file in .psd1, use this field to select it and upload it to your user blob storage, where it is secured by a SAS token.</span></span> 

<span data-ttu-id="1833f-178">**Module-Qualified Name of Configuration**(Полное имя модуля конфигурации) — PS1-файлы могут включать в себя несколько функций конфигурации.</span><span class="sxs-lookup"><span data-stu-id="1833f-178">**Module-Qualified Name of Configuration**: .ps1 files can have multiple configuration functions.</span></span> <span data-ttu-id="1833f-179">Введите имя сценария конфигурации (в формате PS1), символ \', а затем — имя функции конфигурации.</span><span class="sxs-lookup"><span data-stu-id="1833f-179">Enter the name of the configuration .ps1 script followed by a  '\' and the name of the configuration function.</span></span> <span data-ttu-id="1833f-180">Например, если PS1-файл сценария называется configuration.ps1, а имя конфигурации — IisInstall, введите: `configuration.ps1\IisInstall`</span><span class="sxs-lookup"><span data-stu-id="1833f-180">For example, if your .ps1 script has the name "configuration.ps1", and the configuration is "IisInstall", you would enter: `configuration.ps1\IisInstall`</span></span>

<span data-ttu-id="1833f-181">**Configuration Arguments** (Аргументы конфигурации). Если функция конфигурации принимает аргументы, введите их здесь в формате `argumentName1=value1,argumentName2=value2`.</span><span class="sxs-lookup"><span data-stu-id="1833f-181">**Configuration Arguments**: If the configuration function takes arguments, enter them in here in the format `argumentName1=value1,argumentName2=value2`.</span></span> <span data-ttu-id="1833f-182">Обратите внимание, что этот формат отличается от того, в котором аргументы конфигурации принимаются через командлеты PowerShell или шаблоны Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="1833f-182">Note this format is a different format than how configuration arguments are accepted through PowerShell cmdlets or Resource Manager templates.</span></span> 

## <a name="getting-started"></a><span data-ttu-id="1833f-183">Приступая к работе</span><span class="sxs-lookup"><span data-stu-id="1833f-183">Getting started</span></span>
<span data-ttu-id="1833f-184">Расширение DSC Azure получает документы конфигурации DSC и применяет их на виртуальных машинах Azure.</span><span class="sxs-lookup"><span data-stu-id="1833f-184">The Azure DSC extension takes in DSC configuration documents and enacts them on Azure VMs.</span></span> <span data-ttu-id="1833f-185">Ниже приведен простой пример конфигурации.</span><span class="sxs-lookup"><span data-stu-id="1833f-185">A simple example of a configuration follows.</span></span> <span data-ttu-id="1833f-186">Сохраните его локально как файл IisInstall.ps1.</span><span class="sxs-lookup"><span data-stu-id="1833f-186">Save it locally as "IisInstall.ps1":</span></span>

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

<span data-ttu-id="1833f-187">Ниже показано, как разместить сценарий IisInstall.ps1 на указанной виртуальной машине, выполнить конфигурацию и сообщить о статусе.</span><span class="sxs-lookup"><span data-stu-id="1833f-187">The following steps place the IisInstall.ps1 script on the specified VM, execute the configuration, and report back on status.</span></span>
###<a name="classic-model"></a><span data-ttu-id="1833f-188">Классическая модель</span><span class="sxs-lookup"><span data-stu-id="1833f-188">Classic model</span></span>
```powershell
#Azure PowerShell cmdlets are required
Import-Module Azure

#Use an existing Azure Virtual Machine, 'DscDemo1'
$demoVM = Get-AzureVM DscDemo1

#Publish the configuration script into user storage.
Publish-AzureVMDscConfiguration -ConfigurationPath ".\IisInstall.ps1" -StorageContext $storageContext -Verbose -Force

#Set the VM to run the DSC configuration
Set-AzureVMDscExtension -VM $demoVM -ConfigurationArchive "IisInstall.ps1.zip" -StorageContext $storageContext -ConfigurationName "IisInstall" -Verbose

#Update the configuration of an Azure Virtual Machine
$demoVM | Update-AzureVM -Verbose

#check on status
Get-AzureVMDscExtensionStatus -VM $demovm -Verbose
```
###<a name="azure-resource-manager-model"></a><span data-ttu-id="1833f-189">Модель Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="1833f-189">Azure Resource Manager model</span></span>

```powershell
$resourceGroup = "dscVmDemo"
$location = "westus"
$vmName = "myVM"
$storageName = "demostorage"
#Publish the configuration script into user storage
Publish-AzureRmVMDscConfiguration -ConfigurationPath .\iisInstall.ps1 -ResourceGroupName $resourceGroup -StorageAccountName $storageName -force
#Set the VM to run the DSC configuration
Set-AzureRmVmDscExtension -Version 2.21 -ResourceGroupName $resourceGroup -VMName $vmName -ArchiveStorageAccountName $storageName -ArchiveBlobName iisInstall.ps1.zip -AutoUpdate:$true -ConfigurationName "IISInstall"

```

## <a name="logging"></a><span data-ttu-id="1833f-190">Ведение журналов</span><span class="sxs-lookup"><span data-stu-id="1833f-190">Logging</span></span>
<span data-ttu-id="1833f-191">Журналы размещаются в следующем каталоге:</span><span class="sxs-lookup"><span data-stu-id="1833f-191">Logs are placed in:</span></span>

<span data-ttu-id="1833f-192">C:\WindowsAzure\Logs\Plugins\Microsoft.Powershell.DSC\[номер версии]</span><span class="sxs-lookup"><span data-stu-id="1833f-192">C:\WindowsAzure\Logs\Plugins\Microsoft.Powershell.DSC\[Version Number]</span></span>

## <a name="next-steps"></a><span data-ttu-id="1833f-193">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="1833f-193">Next steps</span></span>
<span data-ttu-id="1833f-194">Для получения дополнительных сведений о DSC PowerShell [посетите центр документации PowerShell](https://msdn.microsoft.com/powershell/dsc/overview).</span><span class="sxs-lookup"><span data-stu-id="1833f-194">For more information about PowerShell DSC, [visit the PowerShell documentation center](https://msdn.microsoft.com/powershell/dsc/overview).</span></span> 

<span data-ttu-id="1833f-195">Изучите [шаблон Azure Resource Manager для расширения DSC](extensions-dsc-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="1833f-195">Examine the [Azure Resource Manager template for the DSC extension](extensions-dsc-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> 

<span data-ttu-id="1833f-196">Чтобы получить дополнительные функциональные возможности, которыми можно управлять с помощью DSC PowerShell, [найдите в коллекции PowerShell](https://www.powershellgallery.com/packages?q=DscResource&x=0&y=0) дополнительные материалы по DSC.</span><span class="sxs-lookup"><span data-stu-id="1833f-196">To find additional functionality you can manage with PowerShell DSC, [browse the PowerShell gallery](https://www.powershellgallery.com/packages?q=DscResource&x=0&y=0) for more DSC resources.</span></span>

<span data-ttu-id="1833f-197">Сведения о передаче конфиденциальных параметров в конфигурации см. в статье [Передача учетных данных в обработчик расширений DSC Azure](extensions-dsc-credentials.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="1833f-197">For details on passing sensitive parameters into configurations, see [Manage credentials securely with the DSC extension handler](extensions-dsc-credentials.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

