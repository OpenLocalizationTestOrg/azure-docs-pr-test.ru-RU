---
title: "aaaAzure пользовательский скрипт расширения для Windows | Документы Microsoft"
description: "Автоматизации задач настройки виртуальной Машины Windows с помощью расширения пользовательский сценарий hello"
services: virtual-machines-windows
documentationcenter: 
author: neilpeterson
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: f4181fee-7a9d-4a1c-b517-52956f5b7fa1
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 07/16/2017
ms.author: nepeters
ms.openlocfilehash: 97e065242e9fed116ee20b074f4e302a0cd10585
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="custom-script-extension-for-windows"></a><span data-ttu-id="3424b-103">Расширение Custom Script в ОС Windows</span><span class="sxs-lookup"><span data-stu-id="3424b-103">Custom Script Extension for Windows</span></span>

<span data-ttu-id="3424b-104">Hello настраиваемое расширение скриптов загружает и запускает сценарии на виртуальных машинах Azure.</span><span class="sxs-lookup"><span data-stu-id="3424b-104">hello Custom Script Extension downloads and executes scripts on Azure virtual machines.</span></span> <span data-ttu-id="3424b-105">Это расширение можно использовать для настройки после развертывания, установки программного обеспечения и других задач настройки или управления.</span><span class="sxs-lookup"><span data-stu-id="3424b-105">This extension is useful for post deployment configuration, software installation, or any other configuration / management task.</span></span> <span data-ttu-id="3424b-106">Скрипты можно загружается из хранилища Azure или GitHub, или предоставить toohello портал Azure во время выполнения модуля.</span><span class="sxs-lookup"><span data-stu-id="3424b-106">Scripts can be downloaded from Azure storage or GitHub, or provided toohello Azure portal at extension run time.</span></span> <span data-ttu-id="3424b-107">Hello расширение пользовательского скрипта интегрируется с шаблоны Azure Resource Manager и также можно выполнить с помощью hello Azure CLI, PowerShell, портал Azure или hello API REST Azure виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="3424b-107">hello Custom Script extension integrates with Azure Resource Manager templates, and can also be run using hello Azure CLI, PowerShell, Azure portal, or hello Azure Virtual Machine REST API.</span></span>

<span data-ttu-id="3424b-108">В этом документе описаны как с помощью настраиваемого расширения скриптов hello toouse hello модуля Azure PowerShell, шаблоны диспетчера ресурсов Azure и сведения об устранения неполадок в системах Windows.</span><span class="sxs-lookup"><span data-stu-id="3424b-108">This document details how toouse hello Custom Script Extension using hello Azure PowerShell module, Azure Resource Manager templates, and details troubleshooting steps on Windows systems.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3424b-109">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="3424b-109">Prerequisites</span></span>

### <a name="operating-system"></a><span data-ttu-id="3424b-110">Операционная система</span><span class="sxs-lookup"><span data-stu-id="3424b-110">Operating System</span></span>

<span data-ttu-id="3424b-111">Hello настраиваемое расширение скриптов для Windows, которые могут выполняться для Windows Server 2008 R2, 2012 и 2012 R2, 2016 освобождает.</span><span class="sxs-lookup"><span data-stu-id="3424b-111">hello Custom Script Extension for Windows can be run against Windows Server 2008 R2, 2012, 2012 R2, and 2016 releases.</span></span>

### <a name="script-location"></a><span data-ttu-id="3424b-112">Расположение сценария</span><span class="sxs-lookup"><span data-stu-id="3424b-112">Script Location</span></span>

<span data-ttu-id="3424b-113">сценарий Hello должен toobe хранятся в хранилище больших двоичных объектов Azure или любом другом месте, доступные через допустимый URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="3424b-113">hello script needs toobe stored in Azure Blob storage, or any other location accessible through a valid URL.</span></span>

### <a name="internet-connectivity"></a><span data-ttu-id="3424b-114">Подключение к Интернету</span><span class="sxs-lookup"><span data-stu-id="3424b-114">Internet Connectivity</span></span>

<span data-ttu-id="3424b-115">Hello пользовательский скрипт расширения для Windows требует hello целевой виртуальной машины подключенных toohello Интернета.</span><span class="sxs-lookup"><span data-stu-id="3424b-115">hello Custom Script Extension for Windows requires that hello target virtual machine is connected toohello internet.</span></span> 

## <a name="extension-schema"></a><span data-ttu-id="3424b-116">Схема расширения</span><span class="sxs-lookup"><span data-stu-id="3424b-116">Extension schema</span></span>

<span data-ttu-id="3424b-117">Hello следующий JSON показана схема hello для hello настраиваемого расширения скриптов.</span><span class="sxs-lookup"><span data-stu-id="3424b-117">hello following JSON shows hello schema for hello Custom Script Extension.</span></span> <span data-ttu-id="3424b-118">модуль Hello требует местоположение скрипта (хранилища Azure или другое местоположение с допустимый URL-адрес) и tooexecute команды.</span><span class="sxs-lookup"><span data-stu-id="3424b-118">hello extension requires a script location (Azure Storage or other location with valid URL), and a command tooexecute.</span></span> <span data-ttu-id="3424b-119">При использовании хранилища Azure в качестве исходного текста сценария hello, требуется ключ учетной записи и имени учетной записи хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="3424b-119">If using Azure Storage as hello script source, an Azure storage account name and account key is required.</span></span> <span data-ttu-id="3424b-120">Эти элементы следует рассматривать как конфиденциальные данные и указанные в конфигурацию защищенных параметров расширения hello.</span><span class="sxs-lookup"><span data-stu-id="3424b-120">These items should be treated as sensitive data and specified in hello extensions protected setting configuration.</span></span> <span data-ttu-id="3424b-121">Данных параметр расширение защищенных виртуальных Машин Azure шифруется и расшифрованы только hello целевой виртуальной машине.</span><span class="sxs-lookup"><span data-stu-id="3424b-121">Azure VM extension protected setting data is encrypted, and only decrypted on hello target virtual machine.</span></span>

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
        "typeHandlerVersion": "1.9",
        "autoUpgradeMinorVersion": true,
        "settings": {
            "fileUris": [
                "script location"
            ]
        },
        "protectedSettings": {
            "commandToExecute": "myExecutionCommand",
            "storageAccountName": "myStorageAccountName",
            "storageAccountKey": "myStorageAccountKey"
        }
    }
}
```

### <a name="property-values"></a><span data-ttu-id="3424b-122">Значения свойств</span><span class="sxs-lookup"><span data-stu-id="3424b-122">Property values</span></span>

| <span data-ttu-id="3424b-123">Имя</span><span class="sxs-lookup"><span data-stu-id="3424b-123">Name</span></span> | <span data-ttu-id="3424b-124">Значение и пример</span><span class="sxs-lookup"><span data-stu-id="3424b-124">Value / Example</span></span> |
| ---- | ---- |
| <span data-ttu-id="3424b-125">версия_API</span><span class="sxs-lookup"><span data-stu-id="3424b-125">apiVersion</span></span> | <span data-ttu-id="3424b-126">2015-06-15</span><span class="sxs-lookup"><span data-stu-id="3424b-126">2015-06-15</span></span> |
| <span data-ttu-id="3424b-127">publisher</span><span class="sxs-lookup"><span data-stu-id="3424b-127">publisher</span></span> | <span data-ttu-id="3424b-128">Microsoft.Compute;</span><span class="sxs-lookup"><span data-stu-id="3424b-128">Microsoft.Compute</span></span> |
| <span data-ttu-id="3424b-129">type</span><span class="sxs-lookup"><span data-stu-id="3424b-129">type</span></span> | <span data-ttu-id="3424b-130">extensions</span><span class="sxs-lookup"><span data-stu-id="3424b-130">extensions</span></span> |
| <span data-ttu-id="3424b-131">typeHandlerVersion</span><span class="sxs-lookup"><span data-stu-id="3424b-131">typeHandlerVersion</span></span> | <span data-ttu-id="3424b-132">1.9</span><span class="sxs-lookup"><span data-stu-id="3424b-132">1.9</span></span> |
| <span data-ttu-id="3424b-133">fileUris (пример)</span><span class="sxs-lookup"><span data-stu-id="3424b-133">fileUris (e.g)</span></span> | <span data-ttu-id="3424b-134">https://raw.githubusercontent.com/Microsoft/dotnet-core-sample-templates/master/dotnet-core-music-windows/scripts/configure-music-app.ps1</span><span class="sxs-lookup"><span data-stu-id="3424b-134">https://raw.githubusercontent.com/Microsoft/dotnet-core-sample-templates/master/dotnet-core-music-windows/scripts/configure-music-app.ps1</span></span> |
| <span data-ttu-id="3424b-135">commandToExecute (пример)</span><span class="sxs-lookup"><span data-stu-id="3424b-135">commandToExecute (e.g)</span></span> | <span data-ttu-id="3424b-136">powershell -ExecutionPolicy Unrestricted -File configure-music-app.ps1</span><span class="sxs-lookup"><span data-stu-id="3424b-136">powershell -ExecutionPolicy Unrestricted -File configure-music-app.ps1</span></span> |
| <span data-ttu-id="3424b-137">storageAccountName (пример)</span><span class="sxs-lookup"><span data-stu-id="3424b-137">storageAccountName (e.g)</span></span> | <span data-ttu-id="3424b-138">examplestorageacct</span><span class="sxs-lookup"><span data-stu-id="3424b-138">examplestorageacct</span></span> |
| <span data-ttu-id="3424b-139">storageAccountKey (пример)</span><span class="sxs-lookup"><span data-stu-id="3424b-139">storageAccountKey (e.g)</span></span> | <span data-ttu-id="3424b-140">TmJK/1N3AbAZ3q/+hOXoi/l73zOqsaxXDhqa9Y83/v5UpXQp2DQIBuv2Tifp60cE/OaHsJZmQZ7teQfczQj8hg==</span><span class="sxs-lookup"><span data-stu-id="3424b-140">TmJK/1N3AbAZ3q/+hOXoi/l73zOqsaxXDhqa9Y83/v5UpXQp2DQIBuv2Tifp60cE/OaHsJZmQZ7teQfczQj8hg==</span></span> |

<span data-ttu-id="3424b-141">**Примечание**. В именах свойств учитывается регистр.</span><span class="sxs-lookup"><span data-stu-id="3424b-141">**Note** - these property names are case sensitive.</span></span> <span data-ttu-id="3424b-142">Используйте имена hello, см. выше проблем развертывания tooavoid.</span><span class="sxs-lookup"><span data-stu-id="3424b-142">Use hello names as seen above tooavoid deployment issues.</span></span>

## <a name="template-deployment"></a><span data-ttu-id="3424b-143">Развертывание шаблона</span><span class="sxs-lookup"><span data-stu-id="3424b-143">Template deployment</span></span>

<span data-ttu-id="3424b-144">Расширения виртуальной машины Azure можно развернуть с помощью шаблонов Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="3424b-144">Azure VM extensions can be deployed with Azure Resource Manager templates.</span></span> <span data-ttu-id="3424b-145">можно использовать схему JSON Hello, описанные в предыдущем разделе hello в hello toorun шаблона диспетчера ресурсов Azure настраиваемое расширение скриптов во время развертывания шаблона диспетчера ресурсов Azure.</span><span class="sxs-lookup"><span data-stu-id="3424b-145">hello JSON schema detailed in hello previous section can be used in an Azure Resource Manager template toorun hello Custom Script Extension during an Azure Resource Manager template deployment.</span></span> <span data-ttu-id="3424b-146">Образец шаблона, включает hello настраиваемое расширение скриптов можно найти здесь, [GitHub](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-windows).</span><span class="sxs-lookup"><span data-stu-id="3424b-146">A sample template that includes hello Custom Script Extension can be found here, [GitHub](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-windows).</span></span>

## <a name="powershell-deployment"></a><span data-ttu-id="3424b-147">Развертывание с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="3424b-147">PowerShell deployment</span></span>

<span data-ttu-id="3424b-148">Hello `Set-AzureRmVMCustomScriptExtension` команду можно использовать tooadd hello пользовательский сценарий расширения tooan существующей виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="3424b-148">hello `Set-AzureRmVMCustomScriptExtension` command can be used tooadd hello Custom Script extension tooan existing virtual machine.</span></span> <span data-ttu-id="3424b-149">Дополнительные сведения см. в статье о [Set-AzureRmVMCustomScriptExtension](https://docs.microsoft.com/en-us/powershell/resourcemanager/azurerm.compute/v2.1.0/set-azurermvmcustomscriptextension).</span><span class="sxs-lookup"><span data-stu-id="3424b-149">For more information, see [Set-AzureRmVMCustomScriptExtension ](https://docs.microsoft.com/en-us/powershell/resourcemanager/azurerm.compute/v2.1.0/set-azurermvmcustomscriptextension).</span></span>
```powershell
Set-AzureRmVMCustomScriptExtension -ResourceGroupName myResourceGroup `
    -VMName myVM `
    -Location myLocation `
    -FileUri myURL `
    -Run 'myScript.ps1' `
    -Name DemoScriptExtension
```

## <a name="troubleshoot-and-support"></a><span data-ttu-id="3424b-150">Устранение неполадок и поддержка</span><span class="sxs-lookup"><span data-stu-id="3424b-150">Troubleshoot and support</span></span>

### <a name="troubleshoot"></a><span data-ttu-id="3424b-151">Устранение неполадок</span><span class="sxs-lookup"><span data-stu-id="3424b-151">Troubleshoot</span></span>

<span data-ttu-id="3424b-152">Данные о состоянии hello развертываний расширения могут быть получены из hello портал Azure, а также с помощью модуля Azure PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="3424b-152">Data about hello state of extension deployments can be retrieved from hello Azure portal, and by using hello Azure PowerShell module.</span></span> <span data-ttu-id="3424b-153">Состояние развертывания hello toosee расширений для данной виртуальной Машины, запустите следующую команду hello.</span><span class="sxs-lookup"><span data-stu-id="3424b-153">toosee hello deployment state of extensions for a given VM, run hello following command.</span></span>

```powershell
Get-AzureRmVMExtension -ResourceGroupName myResourceGroup -VMName myVM -Name myExtensionName
```

<span data-ttu-id="3424b-154">Модуль выполнения выходных данных зарегистрированного toofiles вложенной hello следовать directory hello целевой виртуальной машине.</span><span class="sxs-lookup"><span data-stu-id="3424b-154">Extension execution output is logged toofiles found under hello following directory on hello target virtual machine.</span></span>
```cmd
C:\WindowsAzure\Logs\Plugins\Microsoft.Compute.CustomScriptExtension
```

<span data-ttu-id="3424b-155">файлы загружаются в следующий каталог hello целевой виртуальной машине hello указанный Hello.</span><span class="sxs-lookup"><span data-stu-id="3424b-155">hello specified files are downloaded into hello following directory on hello target virtual machine.</span></span>
```cmd
C:\Packages\Plugins\Microsoft.Compute.CustomScriptExtension\1.*\Downloads\<n>
```
<span data-ttu-id="3424b-156">где `<n>` имеет десятичное целое число, которое может измениться между выполнениями hello расширения.</span><span class="sxs-lookup"><span data-stu-id="3424b-156">where `<n>` is a decimal integer which may change between executions of hello extension.</span></span>  <span data-ttu-id="3424b-157">Hello `1.*` значение соответствует фактическую, текущий hello `typeHandlerVersion` значение hello расширения.</span><span class="sxs-lookup"><span data-stu-id="3424b-157">hello `1.*` value matches hello actual, current `typeHandlerVersion` value of hello extension.</span></span>  <span data-ttu-id="3424b-158">Например, может быть действительных папках hello `C:\Packages\Plugins\Microsoft.Compute.CustomScriptExtension\1.8\Downloads\2`.</span><span class="sxs-lookup"><span data-stu-id="3424b-158">For example, hello actual directory could be `C:\Packages\Plugins\Microsoft.Compute.CustomScriptExtension\1.8\Downloads\2`.</span></span>  

<span data-ttu-id="3424b-159">При выполнении hello `commandToExecute` команды расширения hello задаст этот каталог (например, `...\Downloads\2`) как hello текущий рабочий каталог.</span><span class="sxs-lookup"><span data-stu-id="3424b-159">When executing hello `commandToExecute` command, hello extension will have set this directory (e.g., `...\Downloads\2`) as hello current working directory.</span></span> <span data-ttu-id="3424b-160">Это включает использование hello относительные пути toolocate hello файлов загружены через hello `fileURIs` свойство.</span><span class="sxs-lookup"><span data-stu-id="3424b-160">This enables hello use of relative paths toolocate hello files downloaded via hello `fileURIs` property.</span></span> <span data-ttu-id="3424b-161">Приведенной ниже таблице hello, примеры.</span><span class="sxs-lookup"><span data-stu-id="3424b-161">See hello table below for examples.</span></span>

<span data-ttu-id="3424b-162">Поскольку со временем может меняться hello загрузки абсолютный путь, будет лучше tooopt для относительных скрипт или путей к файлам в hello `commandToExecute` строки, когда это возможно.</span><span class="sxs-lookup"><span data-stu-id="3424b-162">Since hello absolute download path may vary over time, it is better tooopt for relative script/file paths in hello `commandToExecute` string, whenever possible.</span></span> <span data-ttu-id="3424b-163">Например:</span><span class="sxs-lookup"><span data-stu-id="3424b-163">For example:</span></span>
```json
    "commandToExecute": "powershell.exe . . . -File './scripts/myscript.ps1'"
```

<span data-ttu-id="3424b-164">Сведения о пути после первого сегмента URI hello сохраняется для файлов загружены через hello `fileUris` списка свойств.</span><span class="sxs-lookup"><span data-stu-id="3424b-164">Path information after hello first URI segment is retained for files downloaded via hello `fileUris` property list.</span></span>  <span data-ttu-id="3424b-165">Как показано в следующей таблице hello, загруженные файлы сопоставляются в подкаталогах загрузки tooreflect структура hello hello `fileUris` значения.</span><span class="sxs-lookup"><span data-stu-id="3424b-165">As shown in hello table below, downloaded files are mapped into download subdirectories tooreflect hello structure of hello `fileUris` values.</span></span>  

#### <a name="examples-of-downloaded-files"></a><span data-ttu-id="3424b-166">Примеры скачанных файлов</span><span class="sxs-lookup"><span data-stu-id="3424b-166">Examples of Downloaded Files</span></span>

| <span data-ttu-id="3424b-167">Универсальный код ресурса (URI) в fileUris</span><span class="sxs-lookup"><span data-stu-id="3424b-167">URI in fileUris</span></span> | <span data-ttu-id="3424b-168">Относительное расположение скачанных файлов</span><span class="sxs-lookup"><span data-stu-id="3424b-168">Relative downloaded location</span></span> | <span data-ttu-id="3424b-169">Абсолютное расположение скачанных файлов*</span><span class="sxs-lookup"><span data-stu-id="3424b-169">Absolute downloaded location *</span></span> |
| ---- | ------- |:--- |
| `https://someAcct.blob.core.windows.net/aContainer/scripts/myscript.ps1` | `./scripts/myscript.ps1` |`C:\Packages\Plugins\Microsoft.Compute.CustomScriptExtension\1.8\Downloads\2\scripts\myscript.ps1`  |
| `https://someAcct.blob.core.windows.net/aContainer/topLevel.ps1` | `./topLevel.ps1` | `C:\Packages\Plugins\Microsoft.Compute.CustomScriptExtension\1.8\Downloads\2\topLevel.ps1` |

<span data-ttu-id="3424b-170">\*Как выше, абсолютные пути hello изменит за время жизни hello hello виртуальной Машины, но не в пределах одного выполнения расширение CustomScript hello.</span><span class="sxs-lookup"><span data-stu-id="3424b-170">\* As above, hello absolute directory paths will change over hello lifetime of hello VM, but not within a single execution of hello CustomScript extension.</span></span>

### <a name="support"></a><span data-ttu-id="3424b-171">Поддержка</span><span class="sxs-lookup"><span data-stu-id="3424b-171">Support</span></span>

<span data-ttu-id="3424b-172">Если вам нужна дополнительная помощь в любой момент в этой статье, можно обратиться в hello Azure экспертами hello [форумы MSDN Azure и переполнения стека] (https://azure.microsoft.com/en-us/support/forums/).</span><span class="sxs-lookup"><span data-stu-id="3424b-172">If you need more help at any point in this article, you can contact hello Azure experts on hello [MSDN Azure and Stack Overflow forums] (https://azure.microsoft.com/en-us/support/forums/).</span></span> <span data-ttu-id="3424b-173">Кроме того, можно зарегистрировать обращение в службу поддержки Azure.</span><span class="sxs-lookup"><span data-stu-id="3424b-173">Alternatively, you can file an Azure support incident.</span></span> <span data-ttu-id="3424b-174">Go toohello [сайт поддержки Azure](https://azure.microsoft.com/en-us/support/options/) и выбрать получение поддержки.</span><span class="sxs-lookup"><span data-stu-id="3424b-174">Go toohello [Azure support site](https://azure.microsoft.com/en-us/support/options/) and select Get support.</span></span> <span data-ttu-id="3424b-175">Дополнительные сведения об использовании Azure поддерживает чтение hello [поддержки Microsoft Azure часто задаваемые вопросы о](https://azure.microsoft.com/en-us/support/faq/).</span><span class="sxs-lookup"><span data-stu-id="3424b-175">For information about using Azure Support, read hello [Microsoft Azure support FAQ](https://azure.microsoft.com/en-us/support/faq/).</span></span>
