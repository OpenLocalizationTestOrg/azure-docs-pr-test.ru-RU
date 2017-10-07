---
title: "aaaCustom расширением сценария на виртуальной Машине Windows | Документы Microsoft"
description: "Автоматизировать задачи настройки виртуальной Машины Azure с помощью сценариев PowerShell toorun расширение пользовательского скрипта hello в удаленной виртуальной Машине Windows"
services: virtual-machines-windows
documentationcenter: 
author: neilpeterson
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: ebb7340a-8f61-4d3c-a290-d7bf8de2d0bd
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 01/17/2017
ms.author: nepeters
ms.openlocfilehash: cf7bb895dd211f07fd010dc03b68cd77df1127b2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="custom-script-extension-for-windows-using-hello-classic-deployment-model"></a><span data-ttu-id="686ec-103">Пользовательский скрипт расширения для Windows с помощью hello классической модели развертывания</span><span class="sxs-lookup"><span data-stu-id="686ec-103">Custom Script Extension for Windows using hello classic deployment model</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="686ec-104">В Azure предлагаются две модели развертывания для создания ресурсов и работы с ними: [модель диспетчера ресурсов и классическая модель](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="686ec-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="686ec-105">В этой статье описан с помощью hello классической модели развертывания.</span><span class="sxs-lookup"><span data-stu-id="686ec-105">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="686ec-106">Корпорация Майкрософт рекомендует наиболее новые развертывания модели hello диспетчера ресурсов.</span><span class="sxs-lookup"><span data-stu-id="686ec-106">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="686ec-107">Узнайте, каким образом слишком[выполните следующие действия с помощью диспетчера ресурсов модели hello](../extensions-customscript.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="686ec-107">Learn how too[perform these steps using hello Resource Manager model](../extensions-customscript.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

<span data-ttu-id="686ec-108">Hello настраиваемое расширение скриптов загружает и запускает сценарии на виртуальных машинах Azure.</span><span class="sxs-lookup"><span data-stu-id="686ec-108">hello Custom Script Extension downloads and executes scripts on Azure virtual machines.</span></span> <span data-ttu-id="686ec-109">Это расширение можно использовать для настройки после развертывания, установки программного обеспечения и других задач настройки или управления.</span><span class="sxs-lookup"><span data-stu-id="686ec-109">This extension is useful for post deployment configuration, software installation, or any other configuration / management task.</span></span> <span data-ttu-id="686ec-110">Скрипты можно загружается из хранилища Azure или GitHub, или предоставить toohello портал Azure во время выполнения модуля.</span><span class="sxs-lookup"><span data-stu-id="686ec-110">Scripts can be downloaded from Azure storage or GitHub, or provided toohello Azure portal at extension run time.</span></span> <span data-ttu-id="686ec-111">Hello расширение пользовательского скрипта интегрируется с шаблоны Azure Resource Manager и также можно выполнить с помощью hello Azure CLI, PowerShell, портал Azure или hello API REST Azure виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="686ec-111">hello Custom Script extension integrates with Azure Resource Manager templates, and can also be run using hello Azure CLI, PowerShell, Azure portal, or hello Azure Virtual Machine REST API.</span></span>

<span data-ttu-id="686ec-112">В этом документе описаны как с помощью настраиваемого расширения скриптов hello toouse hello модуля Azure PowerShell, шаблоны диспетчера ресурсов Azure и сведения об устранения неполадок в системах Windows.</span><span class="sxs-lookup"><span data-stu-id="686ec-112">This document details how toouse hello Custom Script Extension using hello Azure PowerShell module, Azure Resource Manager templates, and details troubleshooting steps on Windows systems.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="686ec-113">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="686ec-113">Prerequisites</span></span>

### <a name="operating-system"></a><span data-ttu-id="686ec-114">Операционная система</span><span class="sxs-lookup"><span data-stu-id="686ec-114">Operating System</span></span>

<span data-ttu-id="686ec-115">Hello настраиваемое расширение скриптов для Windows, которые могут выполняться для Windows Server 2008 R2, 2012 и 2012 R2, 2016 освобождает.</span><span class="sxs-lookup"><span data-stu-id="686ec-115">hello Custom Script Extension for Windows can be run against Windows Server 2008 R2, 2012, 2012 R2, and 2016 releases.</span></span>

### <a name="script-location"></a><span data-ttu-id="686ec-116">Расположение сценария</span><span class="sxs-lookup"><span data-stu-id="686ec-116">Script Location</span></span>

<span data-ttu-id="686ec-117">сценарий Hello должен toobe хранятся в хранилище Azure или любом другом месте, доступные через допустимый URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="686ec-117">hello script needs toobe stored in Azure storage, or any other location accessible through a valid URL.</span></span>

### <a name="internet-connectivity"></a><span data-ttu-id="686ec-118">Подключение к Интернету</span><span class="sxs-lookup"><span data-stu-id="686ec-118">Internet Connectivity</span></span>

<span data-ttu-id="686ec-119">Hello пользовательский скрипт расширения для Windows требует hello целевой виртуальной машины подключенных toohello Интернета.</span><span class="sxs-lookup"><span data-stu-id="686ec-119">hello Custom Script Extension for Windows requires that hello target virtual machine is connected toohello internet.</span></span> 

## <a name="extension-schema"></a><span data-ttu-id="686ec-120">Схема расширения</span><span class="sxs-lookup"><span data-stu-id="686ec-120">Extension schema</span></span>

<span data-ttu-id="686ec-121">Hello следующий JSON показана схема hello для hello настраиваемого расширения скриптов.</span><span class="sxs-lookup"><span data-stu-id="686ec-121">hello following JSON shows hello schema for hello Custom Script Extension.</span></span> <span data-ttu-id="686ec-122">модуль Hello требует местоположение скрипта (хранилища Azure или другое местоположение с допустимый URL-адрес) и tooexecute команды.</span><span class="sxs-lookup"><span data-stu-id="686ec-122">hello extension requires a script location (Azure Storage or other location with valid URL), and a command tooexecute.</span></span> <span data-ttu-id="686ec-123">При использовании хранилища Azure в качестве исходного текста сценария hello, требуется ключ учетной записи и имени учетной записи хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="686ec-123">If using Azure Storage as hello script source, an Azure storage account name and account key is required.</span></span> <span data-ttu-id="686ec-124">Эти элементы следует рассматривать как конфиденциальные данные и указанные в конфигурацию защищенных параметров расширения hello.</span><span class="sxs-lookup"><span data-stu-id="686ec-124">These items should be treated as sensitive data and specified in hello extensions protected setting configuration.</span></span> <span data-ttu-id="686ec-125">Данных параметр расширение защищенных виртуальных Машин Azure шифруется и расшифрованы только hello целевой виртуальной машине.</span><span class="sxs-lookup"><span data-stu-id="686ec-125">Azure VM extension protected setting data is encrypted, and only decrypted on hello target virtual machine.</span></span>

```json
{
    "name": "config-app",
    "type": "Microsoft.ClassicCompute/virtualMachines/extensions",
    "location": "[resourceGroup().location]",
    "apiVersion": "2015-06-01",
    "properties": {
        "publisher": "Microsoft.Compute",
        "extension": "CustomScriptExtension",
        "version": "1.8",
        "parameters": {
            "public": {
                "fileUris": "[myScriptLocation]"
            },
            "private": {
                "commandToExecute": "[myExecutionString]"
            }
        }
    }
}
```

### <a name="property-values"></a><span data-ttu-id="686ec-126">Значения свойств</span><span class="sxs-lookup"><span data-stu-id="686ec-126">Property values</span></span>

| <span data-ttu-id="686ec-127">Имя</span><span class="sxs-lookup"><span data-stu-id="686ec-127">Name</span></span> | <span data-ttu-id="686ec-128">Значение и пример</span><span class="sxs-lookup"><span data-stu-id="686ec-128">Value / Example</span></span> |
| ---- | ---- |
| <span data-ttu-id="686ec-129">версия_API</span><span class="sxs-lookup"><span data-stu-id="686ec-129">apiVersion</span></span> | <span data-ttu-id="686ec-130">2015-06-15</span><span class="sxs-lookup"><span data-stu-id="686ec-130">2015-06-15</span></span> |
| <span data-ttu-id="686ec-131">publisher</span><span class="sxs-lookup"><span data-stu-id="686ec-131">publisher</span></span> | <span data-ttu-id="686ec-132">Microsoft.Compute;</span><span class="sxs-lookup"><span data-stu-id="686ec-132">Microsoft.Compute</span></span> |
| <span data-ttu-id="686ec-133">Расширение</span><span class="sxs-lookup"><span data-stu-id="686ec-133">extension</span></span> | <span data-ttu-id="686ec-134">CustomScriptExtension</span><span class="sxs-lookup"><span data-stu-id="686ec-134">CustomScriptExtension</span></span> |
| <span data-ttu-id="686ec-135">typeHandlerVersion</span><span class="sxs-lookup"><span data-stu-id="686ec-135">typeHandlerVersion</span></span> | <span data-ttu-id="686ec-136">1.8</span><span class="sxs-lookup"><span data-stu-id="686ec-136">1.8</span></span> |
| <span data-ttu-id="686ec-137">fileUris (пример)</span><span class="sxs-lookup"><span data-stu-id="686ec-137">fileUris (e.g)</span></span> | <span data-ttu-id="686ec-138">https://raw.githubusercontent.com/Microsoft/dotnet-core-sample-templates/master/dotnet-core-music-windows/scripts/configure-music-app.ps1</span><span class="sxs-lookup"><span data-stu-id="686ec-138">https://raw.githubusercontent.com/Microsoft/dotnet-core-sample-templates/master/dotnet-core-music-windows/scripts/configure-music-app.ps1</span></span> |
| <span data-ttu-id="686ec-139">commandToExecute (пример)</span><span class="sxs-lookup"><span data-stu-id="686ec-139">commandToExecute (e.g)</span></span> | <span data-ttu-id="686ec-140">powershell -ExecutionPolicy Unrestricted -File configure-music-app.ps1</span><span class="sxs-lookup"><span data-stu-id="686ec-140">powershell -ExecutionPolicy Unrestricted -File configure-music-app.ps1</span></span> |

## <a name="template-deployment"></a><span data-ttu-id="686ec-141">Развертывание шаблона</span><span class="sxs-lookup"><span data-stu-id="686ec-141">Template deployment</span></span>

<span data-ttu-id="686ec-142">Расширения виртуальной машины Azure можно развернуть с помощью шаблонов Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="686ec-142">Azure VM extensions can be deployed with Azure Resource Manager templates.</span></span> <span data-ttu-id="686ec-143">можно использовать схему JSON Hello, описанные в предыдущем разделе hello в hello toorun шаблона диспетчера ресурсов Azure настраиваемое расширение скриптов во время развертывания шаблона диспетчера ресурсов Azure.</span><span class="sxs-lookup"><span data-stu-id="686ec-143">hello JSON schema detailed in hello previous section can be used in an Azure Resource Manager template toorun hello Custom Script Extension during an Azure Resource Manager template deployment.</span></span> <span data-ttu-id="686ec-144">Образец шаблона, включает hello настраиваемое расширение скриптов можно найти здесь, [GitHub](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-windows).</span><span class="sxs-lookup"><span data-stu-id="686ec-144">A sample template that includes hello Custom Script Extension can be found here, [GitHub](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-windows).</span></span>

## <a name="powershell-deployment"></a><span data-ttu-id="686ec-145">Развертывание с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="686ec-145">PowerShell deployment</span></span>

<span data-ttu-id="686ec-146">Hello `Set-AzureVMCustomScriptExtension` команду можно использовать tooadd hello пользовательский сценарий расширения tooan существующей виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="686ec-146">hello `Set-AzureVMCustomScriptExtension` command can be used tooadd hello Custom Script extension tooan existing virtual machine.</span></span> <span data-ttu-id="686ec-147">Дополнительные сведения см. в статье о [Set-AzureRmVMCustomScriptExtension](https://docs.microsoft.com/en-us/powershell/resourcemanager/azurerm.compute/v2.1.0/set-azurermvmcustomscriptextension).</span><span class="sxs-lookup"><span data-stu-id="686ec-147">For more information, see [Set-AzureRmVMCustomScriptExtension ](https://docs.microsoft.com/en-us/powershell/resourcemanager/azurerm.compute/v2.1.0/set-azurermvmcustomscriptextension).</span></span>

```powershell
# create vm object
$vm = Get-AzureVM -Name 2016clas -ServiceName 2016clas1313

# set extension
Set-AzureVMCustomScriptExtension -VM $vm -FileUri myFileUri -Run 'create-file.ps1'

# update vm
$vm | Update-AzureVM
```

## <a name="troubleshoot-and-support"></a><span data-ttu-id="686ec-148">Устранение неполадок и поддержка</span><span class="sxs-lookup"><span data-stu-id="686ec-148">Troubleshoot and support</span></span>

### <a name="troubleshoot"></a><span data-ttu-id="686ec-149">Устранение неполадок</span><span class="sxs-lookup"><span data-stu-id="686ec-149">Troubleshoot</span></span>

<span data-ttu-id="686ec-150">Данные о состоянии hello развертываний расширения могут быть получены из hello портал Azure, а также с помощью модуля Azure PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="686ec-150">Data about hello state of extension deployments can be retrieved from hello Azure portal, and by using hello Azure PowerShell module.</span></span> <span data-ttu-id="686ec-151">Состояние развертывания hello toosee расширений для данной виртуальной Машины, запустите следующую команду hello.</span><span class="sxs-lookup"><span data-stu-id="686ec-151">toosee hello deployment state of extensions for a given VM, run hello following command.</span></span>

```powershell
Get-AzureVMExtension -ResourceGroupName myResourceGroup -VMName myVM -Name myExtensionName
```

<span data-ttu-id="686ec-152">Выполнение модуля вывода нам регистрируется toofiles в следующий каталог hello целевой виртуальной машине hello.</span><span class="sxs-lookup"><span data-stu-id="686ec-152">Extension execution output us logged toofiles found in hello following directory on hello target virtual machine.</span></span>

```cmd
C:\WindowsAzure\Logs\Plugins\Microsoft.Compute.CustomScriptExtension
```

<span data-ttu-id="686ec-153">сам скрипт Hello загружается в следующий каталог hello целевой виртуальной машине hello.</span><span class="sxs-lookup"><span data-stu-id="686ec-153">hello script itself is downloaded into hello following directory on hello target virtual machine.</span></span>

```cmd
C:\Packages\Plugins\Microsoft.Compute.CustomScriptExtension\1.*\Downloads
```

### <a name="support"></a><span data-ttu-id="686ec-154">Поддержка</span><span class="sxs-lookup"><span data-stu-id="686ec-154">Support</span></span>

<span data-ttu-id="686ec-155">Если вам нужна дополнительная помощь в любой момент в этой статье, можно обратиться в hello Azure экспертами hello [форумы MSDN Azure и переполнения стека](https://azure.microsoft.com/en-us/support/forums/).</span><span class="sxs-lookup"><span data-stu-id="686ec-155">If you need more help at any point in this article, you can contact hello Azure experts on hello [MSDN Azure and Stack Overflow forums](https://azure.microsoft.com/en-us/support/forums/).</span></span> <span data-ttu-id="686ec-156">Кроме того, можно зарегистрировать обращение в службу поддержки Azure.</span><span class="sxs-lookup"><span data-stu-id="686ec-156">Alternatively, you can file an Azure support incident.</span></span> <span data-ttu-id="686ec-157">Go toohello [сайт поддержки Azure](https://azure.microsoft.com/en-us/support/options/) и выбрать получение поддержки.</span><span class="sxs-lookup"><span data-stu-id="686ec-157">Go toohello [Azure support site](https://azure.microsoft.com/en-us/support/options/) and select Get support.</span></span> <span data-ttu-id="686ec-158">Дополнительные сведения об использовании Azure поддерживает чтение hello [поддержки Microsoft Azure часто задаваемые вопросы о](https://azure.microsoft.com/en-us/support/faq/).</span><span class="sxs-lookup"><span data-stu-id="686ec-158">For information about using Azure Support, read hello [Microsoft Azure support FAQ](https://azure.microsoft.com/en-us/support/faq/).</span></span>
