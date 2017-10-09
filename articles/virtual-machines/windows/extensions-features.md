---
title: "aaaVirtual машины расширения и компоненты для Windows в Azure | Документы Microsoft"
description: "Узнайте о расширениях, доступных для виртуальных машин Azure и сгруппированных по предоставляемым функциям или улучшениям."
services: virtual-machines-windows
documentationcenter: 
author: neilpeterson
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager
ms.assetid: 999d63ee-890e-432e-9391-25b3fc6cde28
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 03/06/2017
ms.author: nepeters
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 61ccfd696b38e9be1026d836d5796c2346fd650f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="virtual-machine-extensions-and-features-for-windows"></a><span data-ttu-id="83067-103">Обзор расширений и компонентов виртуальной машины под управлением Windows</span><span class="sxs-lookup"><span data-stu-id="83067-103">Virtual machine extensions and features for Windows</span></span>

<span data-ttu-id="83067-104">Расширения виртуальных машин Azure — это небольшие приложения, которые выполняют задачи настройки и автоматизации после развертывания виртуальных машин Azure.</span><span class="sxs-lookup"><span data-stu-id="83067-104">Azure virtual machine extensions are small applications that provide post-deployment configuration and automation tasks on Azure virtual machines.</span></span> <span data-ttu-id="83067-105">Например, если виртуальная машина требует установки программного обеспечения защиты от вирусов и конфигурации Docker, расширение ВМ может быть используется toocomplete этих задач.</span><span class="sxs-lookup"><span data-stu-id="83067-105">For example, if a virtual machine requires software installation, anti-virus protection, or Docker configuration, a VM extension can be used toocomplete these tasks.</span></span> <span data-ttu-id="83067-106">Расширений ВМ Azure можно выполнять с помощью hello Azure CLI PowerShell шаблоны диспетчера ресурсов Azure и hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="83067-106">Azure VM extensions can be run by using hello Azure CLI, PowerShell, Azure Resource Manager templates, and hello Azure portal.</span></span> <span data-ttu-id="83067-107">Расширения можно использовать при развертывании новой виртуальной машины или запускать на любой из существующих систем.</span><span class="sxs-lookup"><span data-stu-id="83067-107">Extensions can be bundled with a new virtual machine deployment or run against any existing system.</span></span>

<span data-ttu-id="83067-108">В этом документе Обзор расширений виртуальной машины, предварительные условия для использования расширения виртуальных машин, а также рекомендации о предоставлении toodetect, управление и удаление расширений виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="83067-108">This document provides an overview of virtual machine extensions, prerequisites for using virtual machine extensions, and guidance on how toodetect, manage, and remove virtual machine extensions.</span></span> <span data-ttu-id="83067-109">Этот документ содержит только обобщенные сведения, так как существует множество расширений виртуальной машины с разными параметрами настройки.</span><span class="sxs-lookup"><span data-stu-id="83067-109">This document provides generalized information because many VM extensions are available, each with a potentially unique configuration.</span></span> <span data-ttu-id="83067-110">Сведения о различных модулей можно найти в каждое расширение отдельных toohello определенного документа.</span><span class="sxs-lookup"><span data-stu-id="83067-110">Extension-specific details can be found in each document specific toohello individual extension.</span></span>

## <a name="use-cases-and-samples"></a><span data-ttu-id="83067-111">Варианты использования и примеры</span><span class="sxs-lookup"><span data-stu-id="83067-111">Use cases and samples</span></span>

<span data-ttu-id="83067-112">Существует много разных расширений виртуальной машины Azure, каждое из которых используется в определенных случаях.</span><span class="sxs-lookup"><span data-stu-id="83067-112">There are many different Azure VM extensions available, each with a specific use case.</span></span> <span data-ttu-id="83067-113">Вот некоторые варианты использования:</span><span class="sxs-lookup"><span data-stu-id="83067-113">Some example use cases are:</span></span>

- <span data-ttu-id="83067-114">Применение требуемого состояния PowerShell конфигураций tooa виртуальной машины с помощью расширения hello DSC для Windows.</span><span class="sxs-lookup"><span data-stu-id="83067-114">Apply PowerShell Desired State configurations tooa virtual machine by using hello DSC extension for Windows.</span></span> <span data-ttu-id="83067-115">Подробнее см. [Общие сведения об обработчике расширения Desired State Configuration в Azure](extensions-dsc-overview.md);</span><span class="sxs-lookup"><span data-stu-id="83067-115">For more information, see [Azure Desired State configuration extension](extensions-dsc-overview.md).</span></span>
- <span data-ttu-id="83067-116">Настройте наблюдение за виртуальной машины с помощью расширения виртуальной Машине агент наблюдения Microsoft hello.</span><span class="sxs-lookup"><span data-stu-id="83067-116">Configure virtual machine monitoring by using hello Microsoft Monitoring Agent VM extension.</span></span> <span data-ttu-id="83067-117">Дополнительные сведения см. в разделе [tooLog виртуальных машин подключение Azure Analytics](../../log-analytics/log-analytics-azure-vm-extension.md).</span><span class="sxs-lookup"><span data-stu-id="83067-117">For more information, see [Connect Azure virtual machines tooLog Analytics](../../log-analytics/log-analytics-azure-vm-extension.md).</span></span>
- <span data-ttu-id="83067-118">Настройка мониторинга инфраструктуры Azure с hello Datadog расширения.</span><span class="sxs-lookup"><span data-stu-id="83067-118">Configure monitoring of your Azure infrastructure with hello Datadog extension.</span></span> <span data-ttu-id="83067-119">Дополнительные сведения см. в разделе hello [Datadog блог](https://www.datadoghq.com/blog/introducing-azure-monitoring-with-one-click-datadog-deployment/).</span><span class="sxs-lookup"><span data-stu-id="83067-119">For more information, see hello [Datadog blog](https://www.datadoghq.com/blog/introducing-azure-monitoring-with-one-click-datadog-deployment/).</span></span>
- <span data-ttu-id="83067-120">настройка виртуальной машины Azure с помощью Chef.</span><span class="sxs-lookup"><span data-stu-id="83067-120">Configure an Azure virtual machine by using Chef.</span></span> <span data-ttu-id="83067-121">Подробнее см. [Автоматизация развертывания виртуальной машины Azure с помощью Chef](chef-automation.md);</span><span class="sxs-lookup"><span data-stu-id="83067-121">For more information, see [Automating Azure virtual machine deployment with Chef](chef-automation.md).</span></span>

<span data-ttu-id="83067-122">Кроме расширения tooprocess, расширение пользовательского скрипта доступен для виртуальных машин Windows и Linux.</span><span class="sxs-lookup"><span data-stu-id="83067-122">In addition tooprocess-specific extensions, a Custom Script extension is available for both Windows and Linux virtual machines.</span></span> <span data-ttu-id="83067-123">расширение пользовательского скрипта для Windows Hello позволяет любой toobe сценария PowerShell, выполните на виртуальной машине.</span><span class="sxs-lookup"><span data-stu-id="83067-123">hello Custom Script extension for Windows allows any PowerShell script toobe run on a virtual machine.</span></span> <span data-ttu-id="83067-124">Это полезно при разработке развертывания Azure, требующего дополнительной настройки, которую не могут выполнить собственные средства Azure.</span><span class="sxs-lookup"><span data-stu-id="83067-124">This is useful when you're designing Azure deployments that require configuration beyond what native Azure tooling can provide.</span></span> <span data-ttu-id="83067-125">Подробнее см. [Использование расширений пользовательских сценариев для виртуальной машины Windows с шаблонами Azure Resource Manager](extensions-customscript.md).</span><span class="sxs-lookup"><span data-stu-id="83067-125">For more information, see [Windows VM Custom Script extension](extensions-customscript.md).</span></span>


## <a name="prerequisites"></a><span data-ttu-id="83067-126">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="83067-126">Prerequisites</span></span>

<span data-ttu-id="83067-127">Каждое расширение виртуальной машины может иметь собственный набор необходимых компонентов.</span><span class="sxs-lookup"><span data-stu-id="83067-127">Each virtual machine extension may have its own set of prerequisites.</span></span> <span data-ttu-id="83067-128">К примеру hello расширение ВМ Docker обладает необходимым условием поддерживаемые ОС Linux.</span><span class="sxs-lookup"><span data-stu-id="83067-128">For instance, hello Docker VM extension has a prerequisite of a supported Linux distribution.</span></span> <span data-ttu-id="83067-129">Требования отдельных расширений, описаны в документации конкретного расширения hello.</span><span class="sxs-lookup"><span data-stu-id="83067-129">Requirements of individual extensions are detailed in hello extension-specific documentation.</span></span>

### <a name="azure-vm-agent"></a><span data-ttu-id="83067-130">Агент виртуальной машины Azure</span><span class="sxs-lookup"><span data-stu-id="83067-130">Azure VM agent</span></span>
<span data-ttu-id="83067-131">агент ВМ Azure Hello управляет взаимодействием между виртуальной машины Azure и Azure fabric controller hello.</span><span class="sxs-lookup"><span data-stu-id="83067-131">hello Azure VM agent manages interaction between an Azure virtual machine and hello Azure fabric controller.</span></span> <span data-ttu-id="83067-132">агент виртуальной Машины Hello отвечает за многие аспекты работы развертывания и управления Azure виртуальные машины, включая выполнение расширений ВМ.</span><span class="sxs-lookup"><span data-stu-id="83067-132">hello VM agent is responsible for many functional aspects of deploying and managing Azure virtual machines, including running VM extensions.</span></span> <span data-ttu-id="83067-133">агент ВМ Azure Hello предустановлен на Azure Marketplace образов и могут быть установлены на поддерживаемых операционных системах.</span><span class="sxs-lookup"><span data-stu-id="83067-133">hello Azure VM agent is preinstalled on Azure Marketplace images and can be installed on supported operating systems.</span></span>

<span data-ttu-id="83067-134">Сведения о поддерживаемых операционных системах и инструкции по установке см. в статье [Обзор агента и расширений виртуальной машины](agent-user-guide.md).</span><span class="sxs-lookup"><span data-stu-id="83067-134">For information on supported operating systems and installation instructions, see [Azure virtual machine agent](agent-user-guide.md).</span></span>

## <a name="discover-vm-extensions"></a><span data-ttu-id="83067-135">Поиск расширений ВМ</span><span class="sxs-lookup"><span data-stu-id="83067-135">Discover VM extensions</span></span>
<span data-ttu-id="83067-136">Существует множество различных расширений ВМ, которые можно использовать с виртуальными машинами Azure.</span><span class="sxs-lookup"><span data-stu-id="83067-136">Many different VM extensions are available for use with Azure virtual machines.</span></span> <span data-ttu-id="83067-137">toosee полный список, запустите следующую команду с модулем PowerShell диспетчера ресурсов Azure hello hello.</span><span class="sxs-lookup"><span data-stu-id="83067-137">toosee a complete list, run hello following command with hello Azure Resource Manager PowerShell module.</span></span> <span data-ttu-id="83067-138">Убедитесь, что расположение требуемого hello toospecify при запуске этой команды.</span><span class="sxs-lookup"><span data-stu-id="83067-138">Make sure toospecify hello desired location when you're running this command.</span></span>

```powershell
Get-AzureRmVmImagePublisher -Location WestUS | `
Get-AzureRmVMExtensionImageType | `
Get-AzureRmVMExtensionImage | Select Type, Version
```

## <a name="run-vm-extensions"></a><span data-ttu-id="83067-139">Запуск расширений ВМ</span><span class="sxs-lookup"><span data-stu-id="83067-139">Run VM extensions</span></span>

<span data-ttu-id="83067-140">Расширения виртуальных машин Azure может выполняться на существующих виртуальных машин, что полезно при необходимости изменения конфигурации toomake или восстановить подключение на уже развернутой виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="83067-140">Azure virtual machine extensions can be run on existing virtual machines, which is useful when you need toomake configuration changes or recover connectivity on an already deployed VM.</span></span> <span data-ttu-id="83067-141">Также расширения можно использовать при развертывании с помощью шаблонов Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="83067-141">VM extensions can also be bundled with Azure Resource Manager template deployments.</span></span> <span data-ttu-id="83067-142">С помощью расширений с помощью шаблонов диспетчера ресурсов, можно включить toobe виртуальных машин Azure развертывания и настройки без необходимости вмешательства после развертывания hello.</span><span class="sxs-lookup"><span data-stu-id="83067-142">By using extensions with Resource Manager templates, you can enable Azure virtual machines toobe deployed and configured without hello need for post-deployment intervention.</span></span>

<span data-ttu-id="83067-143">Hello следующие методы можно использовать toorun расширение для существующей виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="83067-143">hello following methods can be used toorun an extension against an existing virtual machine.</span></span>

### <a name="powershell"></a><span data-ttu-id="83067-144">PowerShell</span><span class="sxs-lookup"><span data-stu-id="83067-144">PowerShell</span></span>

<span data-ttu-id="83067-145">Есть несколько команд PowerShell, позволяющих выполнять отдельные модули.</span><span class="sxs-lookup"><span data-stu-id="83067-145">Several PowerShell commands exist for running individual extensions.</span></span> <span data-ttu-id="83067-146">toosee список, запустите следующие команды PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="83067-146">toosee a list, run hello following PowerShell commands.</span></span>

```powershell
get-command Set-AzureRM*Extension* -Module AzureRM.Compute
```

<span data-ttu-id="83067-147">Это обеспечивает аналогичную toohello следующие выходные данные:</span><span class="sxs-lookup"><span data-stu-id="83067-147">This provides output similar toohello following:</span></span>

```powershell
CommandType     Name                                               Version    Source
-----------     ----                                               -------    ------
Cmdlet          Set-AzureRmVMAccessExtension                       2.2.0      AzureRM.Compute
Cmdlet          Set-AzureRmVMADDomainExtension                     2.2.0      AzureRM.Compute
Cmdlet          Set-AzureRmVMAEMExtension                          2.2.0      AzureRM.Compute
Cmdlet          Set-AzureRmVMBackupExtension                       2.2.0      AzureRM.Compute
Cmdlet          Set-AzureRmVMBginfoExtension                       2.2.0      AzureRM.Compute
Cmdlet          Set-AzureRmVMChefExtension                         2.2.0      AzureRM.Compute
Cmdlet          Set-AzureRmVMCustomScriptExtension                 2.2.0      AzureRM.Compute
Cmdlet          Set-AzureRmVMDiagnosticsExtension                  2.2.0      AzureRM.Compute
Cmdlet          Set-AzureRmVMDiskEncryptionExtension               2.2.0      AzureRM.Compute
Cmdlet          Set-AzureRmVMDscExtension                          2.2.0      AzureRM.Compute
Cmdlet          Set-AzureRmVMExtension                             2.2.0      AzureRM.Compute
Cmdlet          Set-AzureRmVMSqlServerExtension                    2.2.0      AzureRM.Compute
```

<span data-ttu-id="83067-148">Hello следующий пример использует hello пользовательский сценарий расширения toodownload сценарий из репозитория GitHub hello целевой виртуальной машине и затем запустите скрипт hello.</span><span class="sxs-lookup"><span data-stu-id="83067-148">hello following example uses hello Custom Script extension toodownload a script from a GitHub repository onto hello target virtual machine and then run hello script.</span></span> <span data-ttu-id="83067-149">Дополнительные сведения о hello расширение пользовательского скрипта см. в разделе [Обзор расширения пользовательский сценарий](extensions-customscript.md).</span><span class="sxs-lookup"><span data-stu-id="83067-149">For more information on hello Custom Script extension, see [Custom Script extension overview](extensions-customscript.md).</span></span>

```powershell
Set-AzureRmVMCustomScriptExtension -ResourceGroupName "myResourceGroup" `
    -VMName "myVM" -Name "myCustomScript" `
    -FileUri "https://raw.githubusercontent.com/neilpeterson/nepeters-azure-templates/master/windows-custom-script-simple/support-scripts/Create-File.ps1" `
    -Run "Create-File.ps1" -Location "West US"
```

<span data-ttu-id="83067-150">В этом примере hello расширение виртуальной Машины — используется tooreset hello административный пароль Windows виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="83067-150">In this example, hello VM Access extension is used tooreset hello administrative password of a Windows virtual machine.</span></span> <span data-ttu-id="83067-151">Дополнительные сведения о hello расширение виртуальной Машины в разделе [сброс службы удаленного рабочего стола на виртуальной машине Windows](reset-rdp.md).</span><span class="sxs-lookup"><span data-stu-id="83067-151">For more information on hello VM Access extension, see [Reset Remote Desktop service in a Windows VM](reset-rdp.md).</span></span>

```powershell
$cred=Get-Credential

Set-AzureRmVMAccessExtension -ResourceGroupName "myResourceGroup" -VMName "myVM" -Name "myVMAccess" `
    -Location WestUS -UserName $cred.GetNetworkCredential().Username `
    -Password $cred.GetNetworkCredential().Password -typeHandlerVersion "2.0"
```

<span data-ttu-id="83067-152">Hello `Set-AzureRmVMExtension` команды можно использовать toostart любое расширение виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="83067-152">hello `Set-AzureRmVMExtension` command can be used toostart any VM extension.</span></span> <span data-ttu-id="83067-153">Дополнительные сведения см. в разделе hello [AzureRmVMExtension набор ссылок](https://msdn.microsoft.com/en-us/library/mt603745.aspx).</span><span class="sxs-lookup"><span data-stu-id="83067-153">For more information, see hello [Set-AzureRmVMExtension reference](https://msdn.microsoft.com/en-us/library/mt603745.aspx).</span></span>


### <a name="azure-portal"></a><span data-ttu-id="83067-154">Портал Azure</span><span class="sxs-lookup"><span data-stu-id="83067-154">Azure portal</span></span>

<span data-ttu-id="83067-155">Расширение виртуальной Машины может быть применен tooan существующей виртуальной машины через портал Azure hello.</span><span class="sxs-lookup"><span data-stu-id="83067-155">A VM extension can be applied tooan existing virtual machine through hello Azure portal.</span></span> <span data-ttu-id="83067-156">toodo таким образом, выберите виртуальную машину hello нужны toouse, выберите **расширения**и нажмите кнопку **добавить**.</span><span class="sxs-lookup"><span data-stu-id="83067-156">toodo so, select hello virtual machine you want toouse, choose **Extensions**, and click **Add**.</span></span> <span data-ttu-id="83067-157">Вы увидите список доступных расширений.</span><span class="sxs-lookup"><span data-stu-id="83067-157">This provides a list of available extensions.</span></span> <span data-ttu-id="83067-158">Выберите hello требуется, и следуйте указаниям мастера hello в hello.</span><span class="sxs-lookup"><span data-stu-id="83067-158">Select hello one you want and follow hello steps in hello wizard.</span></span>

<span data-ttu-id="83067-159">Hello следующем рисунке показана установка hello hello модуль защиты от вредоносных программ Майкрософт от hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="83067-159">hello following image shows hello installation of hello Microsoft Antimalware extension from hello Azure portal.</span></span>

![Установка расширения защиты от вредоносных программ](./media/extensions-features/installantimalwareextension.png)

### <a name="azure-resource-manager-templates"></a><span data-ttu-id="83067-161">Шаблоны диспетчера ресурсов Azure</span><span class="sxs-lookup"><span data-stu-id="83067-161">Azure Resource Manager templates</span></span>

<span data-ttu-id="83067-162">Расширения ВМ может быть добавлено tooan шаблона диспетчера ресурсов Azure и выполняться hello развертывания шаблона hello.</span><span class="sxs-lookup"><span data-stu-id="83067-162">VM extensions can be added tooan Azure Resource Manager template and executed with hello deployment of hello template.</span></span> <span data-ttu-id="83067-163">Развертывание расширений с помощью шаблона позволяет создать полностью настроенные развертывания Azure.</span><span class="sxs-lookup"><span data-stu-id="83067-163">Deploying extensions with a template is useful for creating fully configured Azure deployments.</span></span> <span data-ttu-id="83067-164">Например приветствия следующий JSON берется из шаблона диспетчера ресурсов, который развертывает набор с балансировкой нагрузки виртуальные машины и базы данных Azure SQL, а затем устанавливает приложение .NET Core на каждой виртуальной Машине.</span><span class="sxs-lookup"><span data-stu-id="83067-164">For example, hello following JSON is taken from a Resource Manager template that deploys a set of load-balanced virtual machines and an Azure SQL database, and then installs a .NET Core application on each VM.</span></span> <span data-ttu-id="83067-165">Установка программного обеспечения hello обеспечивает Hello расширения виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="83067-165">hello VM extension takes care of hello software installation.</span></span>

<span data-ttu-id="83067-166">Дополнительные сведения см. в разделе hello [полного шаблона диспетчера ресурсов](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-windows).</span><span class="sxs-lookup"><span data-stu-id="83067-166">For more information, see hello [full Resource Manager template](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-windows).</span></span>

```json
{
    "apiVersion": "2015-06-15",
    "type": "extensions",
    "name": "config-app",
    "location": "[resourceGroup().location]",
    "dependsOn": [
    "[concat('Microsoft.Compute/virtualMachines/', variables('vmName'),copyindex())]",
    "[variables('musicstoresqlName')]"
    ],
    "tags": {
    "displayName": "config-app"
    },
    "properties": {
    "publisher": "Microsoft.Compute",
    "type": "CustomScriptExtension",
    "typeHandlerVersion": "1.4",
    "autoUpgradeMinorVersion": true,
    "settings": {
        "fileUris": [
        "https://raw.githubusercontent.com/Microsoft/dotnet-core-sample-templates/master/dotnet-core-music-windows/scripts/configure-music-app.ps1"
        ]
    },
    "protectedSettings": {
        "commandToExecute": "[concat('powershell -ExecutionPolicy Unrestricted -File configure-music-app.ps1 -user ',parameters('adminUsername'),' -password ',parameters('adminPassword'),' -sqlserver ',variables('musicstoresqlName'),'.database.windows.net')]"
    }
    }
}
```

<span data-ttu-id="83067-167">Дополнительные сведения см. в статье [Создание шаблонов Azure Resource Manager с помощью расширений виртуальной машины Windows](template-description.md#extensions).</span><span class="sxs-lookup"><span data-stu-id="83067-167">For more information, see [Authoring Azure Resource Manager templates with Windows VM extensions](template-description.md#extensions).</span></span>

## <a name="secure-vm-extension-data"></a><span data-ttu-id="83067-168">Защита данных в расширениях ВМ</span><span class="sxs-lookup"><span data-stu-id="83067-168">Secure VM extension data</span></span>

<span data-ttu-id="83067-169">При работе с расширением ВМ, может быть необходимо tooinclude конфиденциальные сведения, например учетные данные, имена учетных записей хранилища и ключи доступа к учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="83067-169">When you're running a VM extension, it may be necessary tooinclude sensitive information such as credentials, storage account names, and storage account access keys.</span></span> <span data-ttu-id="83067-170">Множество расширений ВМ включают защищенной конфигурации, который шифрует данные и только расшифровывает его целевой виртуальной машине hello.</span><span class="sxs-lookup"><span data-stu-id="83067-170">Many VM extensions include a protected configuration that encrypts data and only decrypts it inside hello target virtual machine.</span></span> <span data-ttu-id="83067-171">Каждое расширение имеет собственную схему защищенной конфигурации, которая описывается в документации по этим расширениям.</span><span class="sxs-lookup"><span data-stu-id="83067-171">Each extension has a specific protected configuration schema that will be detailed in extension-specific documentation.</span></span>

<span data-ttu-id="83067-172">Привет, в следующем примере показан экземпляр hello расширение пользовательского скрипта для Windows.</span><span class="sxs-lookup"><span data-stu-id="83067-172">hello following example shows an instance of hello Custom Script extension for Windows.</span></span> <span data-ttu-id="83067-173">Обратите внимание, что команды, hello tooexecute включает в себя набор учетных данных.</span><span class="sxs-lookup"><span data-stu-id="83067-173">Notice that hello command tooexecute includes a set of credentials.</span></span> <span data-ttu-id="83067-174">В этом примере команда tooexecute hello не будут зашифрованы.</span><span class="sxs-lookup"><span data-stu-id="83067-174">In this example, hello command tooexecute will not be encrypted.</span></span>


```json
{
    "apiVersion": "2015-06-15",
    "type": "extensions",
    "name": "config-app",
    "location": "[resourceGroup().location]",
    "dependsOn": [
    "[concat('Microsoft.Compute/virtualMachines/', variables('vmName'),copyindex())]",
    "[variables('musicstoresqlName')]"
    ],
    "tags": {
    "displayName": "config-app"
    },
    "properties": {
    "publisher": "Microsoft.Compute",
    "type": "CustomScriptExtension",
    "typeHandlerVersion": "1.4",
    "autoUpgradeMinorVersion": true,
    "settings": {
        "fileUris": [
        "https://raw.githubusercontent.com/Microsoft/dotnet-core-sample-templates/master/dotnet-core-music-windows/scripts/configure-music-app.ps1"
        ],
        "commandToExecute": "[concat('powershell -ExecutionPolicy Unrestricted -File configure-music-app.ps1 -user ',parameters('adminUsername'),' -password ',parameters('adminPassword'),' -sqlserver ',variables('musicstoresqlName'),'.database.windows.net')]"
    }
    }
}
```

<span data-ttu-id="83067-175">Защитить строку hello выполнения путем перемещения hello **tooexecute команда** toohello свойство **защищенных** конфигурации.</span><span class="sxs-lookup"><span data-stu-id="83067-175">Secure hello execution string by moving hello **command tooexecute** property toohello **protected** configuration.</span></span>

```json
{
    "apiVersion": "2015-06-15",
    "type": "extensions",
    "name": "config-app",
    "location": "[resourceGroup().location]",
    "dependsOn": [
    "[concat('Microsoft.Compute/virtualMachines/', variables('vmName'),copyindex())]",
    "[variables('musicstoresqlName')]"
    ],
    "tags": {
    "displayName": "config-app"
    },
    "properties": {
    "publisher": "Microsoft.Compute",
    "type": "CustomScriptExtension",
    "typeHandlerVersion": "1.4",
    "autoUpgradeMinorVersion": true,
    "settings": {
        "fileUris": [
        "https://raw.githubusercontent.com/Microsoft/dotnet-core-sample-templates/master/dotnet-core-music-windows/scripts/configure-music-app.ps1"
        ]
    },
    "protectedSettings": {
        "commandToExecute": "[concat('powershell -ExecutionPolicy Unrestricted -File configure-music-app.ps1 -user ',parameters('adminUsername'),' -password ',parameters('adminPassword'),' -sqlserver ',variables('musicstoresqlName'),'.database.windows.net')]"
    }
    }
}
```

## <a name="troubleshoot-vm-extensions"></a><span data-ttu-id="83067-176">Устранение неполадок с расширениями ВМ</span><span class="sxs-lookup"><span data-stu-id="83067-176">Troubleshoot VM extensions</span></span>

<span data-ttu-id="83067-177">Связанные с каждым расширением виртуальной машины неполадки устраняются определенным образом.</span><span class="sxs-lookup"><span data-stu-id="83067-177">Each VM extension may have specific troubleshooting steps.</span></span> <span data-ttu-id="83067-178">Для экземпляра когда вы используете расширение пользовательского скрипта hello, сведения о выполнении скрипта можно найти локально на hello виртуальной машины, на котором был выполнен hello расширения.</span><span class="sxs-lookup"><span data-stu-id="83067-178">For instance, when you're using hello Custom Script extension, script execution details can be found locally on hello virtual machine on which hello extension was run.</span></span> <span data-ttu-id="83067-179">Действия по устранению неполадок для конкретных расширений описаны в документации по соответствующим расширениям.</span><span class="sxs-lookup"><span data-stu-id="83067-179">Any extension-specific troubleshooting steps are detailed in extension-specific documentation.</span></span>

<span data-ttu-id="83067-180">следующие шаги по устранению неполадок Hello применяются tooall расширения виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="83067-180">hello following troubleshooting steps apply tooall virtual machine extensions.</span></span>

### <a name="view-extension-status"></a><span data-ttu-id="83067-181">Просмотр состояния расширения</span><span class="sxs-lookup"><span data-stu-id="83067-181">View extension status</span></span>

<span data-ttu-id="83067-182">После завершения выполнения расширения виртуальной машины от виртуальной машины, используйте hello следующие состояния расширения tooreturn команды PowerShell.</span><span class="sxs-lookup"><span data-stu-id="83067-182">After a virtual machine extension has been run against a virtual machine, use hello following PowerShell command tooreturn extension status.</span></span> <span data-ttu-id="83067-183">Замените в примере имена-параметры собственными значениями.</span><span class="sxs-lookup"><span data-stu-id="83067-183">Replace example parameter names with your own values.</span></span> <span data-ttu-id="83067-184">Hello `Name` принимает имя hello, данное расширение toohello во время выполнения.</span><span class="sxs-lookup"><span data-stu-id="83067-184">hello `Name` parameter takes hello name given toohello extension at execution time.</span></span>

```PowerShell
Get-AzureRmVMExtension -ResourceGroupName myResourceGroup -VMName myVM -Name myExtensionName
```

<span data-ttu-id="83067-185">Hello вывод выглядит следующим образом следующие hello.</span><span class="sxs-lookup"><span data-stu-id="83067-185">hello output looks like hello following:</span></span>

```json
ResourceGroupName       : myResourceGroup
VMName                  : myVM
Name                    : myExtensionName
Location                : westus
Etag                    : null
Publisher               : Microsoft.Azure.Extensions
ExtensionType           : DockerExtension
TypeHandlerVersion      : 1.0
Id                      : /subscriptions/mySubscriptionIS/resourceGroups/myResourceGroup/providers/Microsoft.Compute/virtualMachines/myVM/extensions/myExtensionName
PublicSettings          :
ProtectedSettings       :
ProvisioningState       : Succeeded
Statuses                :
SubStatuses             :
AutoUpgradeMinorVersion : False
ForceUpdateTag          :
```

<span data-ttu-id="83067-186">Состояние выполнения расширения можно найти также в hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="83067-186">Extension execution status can also be found in hello Azure portal.</span></span> <span data-ttu-id="83067-187">состояние hello tooview расширение, выберите hello виртуальной машины, выберите **расширения**, и выберите hello нужное расширение.</span><span class="sxs-lookup"><span data-stu-id="83067-187">tooview hello status of an extension, select hello virtual machine, choose **Extensions**, and select hello desired extension.</span></span>

### <a name="rerun-vm-extensions"></a><span data-ttu-id="83067-188">Повторный запуск расширений виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="83067-188">Rerun VM extensions</span></span>

<span data-ttu-id="83067-189">Возможны ситуации, в которых расширение виртуальной машины должен toobe повторно.</span><span class="sxs-lookup"><span data-stu-id="83067-189">There may be cases in which a virtual machine extension needs toobe rerun.</span></span> <span data-ttu-id="83067-190">Это можно сделать, удалив расширение hello и повторно запустив hello расширения с помощью метода выполнения по своему усмотрению.</span><span class="sxs-lookup"><span data-stu-id="83067-190">You can do this by removing hello extension and then rerunning hello extension with an execution method of your choice.</span></span> <span data-ttu-id="83067-191">tooremove расширение, запустите следующую команду с помощью модуля Azure PowerShell hello hello.</span><span class="sxs-lookup"><span data-stu-id="83067-191">tooremove an extension, run hello following command with hello Azure PowerShell module.</span></span> <span data-ttu-id="83067-192">Замените в примере имена-параметры собственными значениями.</span><span class="sxs-lookup"><span data-stu-id="83067-192">Replace example parameter names with your own values.</span></span>

```powershell
Remove-AzureRmVMExtension -ResourceGroupName myResourceGroup -VMName myVM -Name myExtensionName
```

<span data-ttu-id="83067-193">Расширения можно также удалить с помощью портала Azure hello.</span><span class="sxs-lookup"><span data-stu-id="83067-193">An extension can also be removed using hello Azure portal.</span></span> <span data-ttu-id="83067-194">toodo так:</span><span class="sxs-lookup"><span data-stu-id="83067-194">toodo so:</span></span>

1. <span data-ttu-id="83067-195">Выберите виртуальную машину.</span><span class="sxs-lookup"><span data-stu-id="83067-195">Select a virtual machine.</span></span>
2. <span data-ttu-id="83067-196">Выберите **Расширения**.</span><span class="sxs-lookup"><span data-stu-id="83067-196">Select **Extensions**.</span></span>
3. <span data-ttu-id="83067-197">Выберите расширение требуемого hello.</span><span class="sxs-lookup"><span data-stu-id="83067-197">Choose hello desired extension.</span></span>
4. <span data-ttu-id="83067-198">Выберите **Удалить**.</span><span class="sxs-lookup"><span data-stu-id="83067-198">Select **Uninstall**.</span></span>

## <a name="common-vm-extensions-reference"></a><span data-ttu-id="83067-199">Справочники по распространенным расширениям виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="83067-199">Common VM extensions reference</span></span>
| <span data-ttu-id="83067-200">Имя расширения</span><span class="sxs-lookup"><span data-stu-id="83067-200">Extension name</span></span> | <span data-ttu-id="83067-201">Описание</span><span class="sxs-lookup"><span data-stu-id="83067-201">Description</span></span> | <span data-ttu-id="83067-202">Дополнительные сведения</span><span class="sxs-lookup"><span data-stu-id="83067-202">More information</span></span> |
| --- | --- | --- |
| <span data-ttu-id="83067-203">Расширение Custom Script в ОС Windows</span><span class="sxs-lookup"><span data-stu-id="83067-203">Custom Script Extension for Windows</span></span> |<span data-ttu-id="83067-204">Выполняет сценарии на виртуальных машинах Azure.</span><span class="sxs-lookup"><span data-stu-id="83067-204">Run scripts against an Azure virtual machine</span></span> |[<span data-ttu-id="83067-205">Расширение Custom Script в ОС Windows</span><span class="sxs-lookup"><span data-stu-id="83067-205">Custom Script Extension for Windows</span></span>](extensions-customscript.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) |
| <span data-ttu-id="83067-206">Расширение DSC в ОС Windows</span><span class="sxs-lookup"><span data-stu-id="83067-206">DSC Extension for Windows</span></span> |<span data-ttu-id="83067-207">Расширение PowerShell DSC (настройка требуемого состояния)</span><span class="sxs-lookup"><span data-stu-id="83067-207">PowerShell DSC (Desired State Configuration) Extension</span></span> |[<span data-ttu-id="83067-208">Общие сведения об обработчике расширения Desired State Configuration в Azure</span><span class="sxs-lookup"><span data-stu-id="83067-208">DSC Extension for Windows</span></span>](extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) |
| <span data-ttu-id="83067-209">Расширение системы диагностики Azure</span><span class="sxs-lookup"><span data-stu-id="83067-209">Azure Diagnostics Extension</span></span> |<span data-ttu-id="83067-210">Управляет системой диагностики Azure</span><span class="sxs-lookup"><span data-stu-id="83067-210">Manage Azure Diagnostics</span></span> |[<span data-ttu-id="83067-211">Расширение системы диагностики Azure</span><span class="sxs-lookup"><span data-stu-id="83067-211">Azure Diagnostics Extension</span></span>](https://azure.microsoft.com/blog/windows-azure-virtual-machine-monitoring-with-wad-extension/) |
| <span data-ttu-id="83067-212">Расширение Azure VM Access</span><span class="sxs-lookup"><span data-stu-id="83067-212">Azure VM Access Extension</span></span> |<span data-ttu-id="83067-213">Управляет пользователями и учетными данными.</span><span class="sxs-lookup"><span data-stu-id="83067-213">Manage users and credentials</span></span> |[<span data-ttu-id="83067-214">Расширение VM Access для Linux</span><span class="sxs-lookup"><span data-stu-id="83067-214">VM Access Extension for Linux</span></span>](https://azure.microsoft.com/en-us/blog/using-vmaccess-extension-to-reset-login-credentials-for-linux-vm/) |
