---
title: "Развертывание приложения в наборах масштабирования виртуальных машин"
description: "Использование расширений для развертывания приложения в масштабируемом наборе виртуальных машин Azure."
services: virtual-machine-scale-sets
documentationcenter: 
author: thraka
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: f8892199-f2e2-4b82-988a-28ca8a7fd1eb
ms.service: virtual-machine-scale-sets
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/26/2017
ms.author: adegeo
ms.openlocfilehash: fa7d9d3bef4cb326844ede76171e8c566e87116b
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="deploy-your-application-on-virtual-machine-scale-sets"></a><span data-ttu-id="c1e5b-103">Развертывание приложения в масштабируемых наборах виртуальных машин</span><span class="sxs-lookup"><span data-stu-id="c1e5b-103">Deploy your application on virtual machine scale sets</span></span>

<span data-ttu-id="c1e5b-104">В этой статье описываются различные способы установки программного обеспечения во время подготовки масштабируемого набора.</span><span class="sxs-lookup"><span data-stu-id="c1e5b-104">This article describes different ways of how to install software at the time the scale set is provisioned.</span></span>

<span data-ttu-id="c1e5b-105">Возможно, вам потребуется обратиться к статье [Обзор проектов масштабируемых наборов](virtual-machine-scale-sets-design-overview.md), в которой описаны некоторые ограничения, налагаемые масштабируемыми наборами виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="c1e5b-105">You may want to review the [Scale Set Design Overview](virtual-machine-scale-sets-design-overview.md) article, which describes some of the limits imposed by virtual machine scale sets.</span></span>

## <a name="capture-and-reuse-an-image"></a><span data-ttu-id="c1e5b-106">Запись и повторное использование образа</span><span class="sxs-lookup"><span data-stu-id="c1e5b-106">Capture and reuse an image</span></span>

<span data-ttu-id="c1e5b-107">Виртуальную машину, созданную в Azure, можно использовать для подготовки базового образа для масштабируемого набора.</span><span class="sxs-lookup"><span data-stu-id="c1e5b-107">You can use a virtual machine you have in Azure to prepare a base-image for your scale set.</span></span> <span data-ttu-id="c1e5b-108">Этот процесс создает управляемый диск в вашей учетной записи хранения, на который можно ссылаться как на базовый образ для масштабируемого набора.</span><span class="sxs-lookup"><span data-stu-id="c1e5b-108">This process creates a managed disk in your storage account, which you can reference as the base image for your scale set.</span></span> 

<span data-ttu-id="c1e5b-109">Сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="c1e5b-109">Do the following steps:</span></span>

1. <span data-ttu-id="c1e5b-110">Создайте виртуальную машину Azure</span><span class="sxs-lookup"><span data-stu-id="c1e5b-110">Create an Azure Virtual Machine</span></span>
   * <span data-ttu-id="c1e5b-111">[Linux][linux-vm-create]</span><span class="sxs-lookup"><span data-stu-id="c1e5b-111">[Linux][linux-vm-create]</span></span>
   * <span data-ttu-id="c1e5b-112">[Windows][windows-vm-create]</span><span class="sxs-lookup"><span data-stu-id="c1e5b-112">[Windows][windows-vm-create]</span></span>

2. <span data-ttu-id="c1e5b-113">Подключитесь к виртуальной машине и настройте необходимые параметры системы.</span><span class="sxs-lookup"><span data-stu-id="c1e5b-113">Remote into the virtual machine and customize the system to your liking.</span></span>

   <span data-ttu-id="c1e5b-114">Теперь вы можете установить приложение.</span><span class="sxs-lookup"><span data-stu-id="c1e5b-114">If you want, you can install your application now.</span></span> <span data-ttu-id="c1e5b-115">Но учтите, что если вы установите приложение сейчас, обновить его будет сложнее, так как потребуется сначала удалить его.</span><span class="sxs-lookup"><span data-stu-id="c1e5b-115">However, know that by installing your application now, you may make upgrading your application more complicated because you may need to remove it first.</span></span> <span data-ttu-id="c1e5b-116">Вместо этого вы можете использовать этот шаг для установки необходимых компонентов, которые могут потребоваться приложению, таких как определенные компоненты среды выполнения или операционной системы.</span><span class="sxs-lookup"><span data-stu-id="c1e5b-116">Instead, you can use this step to install any prerequisites your application may need, like a specific runtime or operating system feature.</span></span>

3. <span data-ttu-id="c1e5b-117">Выполните процедуру в руководстве по "записи виртуальной машины" для [Linux][linux-vm-capture] или [Windows][windows-vm-capture].</span><span class="sxs-lookup"><span data-stu-id="c1e5b-117">Follow the "capture a machine" tutorial for either [Linux][linux-vm-capture] or [Windows][windows-vm-capture].</span></span>

4. <span data-ttu-id="c1e5b-118">Создайте [масштабируемый набор виртуальных машин][vmss-create], используя URI образа, записанного на предыдущем шаге.</span><span class="sxs-lookup"><span data-stu-id="c1e5b-118">Create a [Virtual Machine Scale Set][vmss-create] with the image URI you captured in the previous step.</span></span>

<span data-ttu-id="c1e5b-119">Дополнительные сведения о дисках см. в статьях [Обзор управляемых дисков](../virtual-machines/windows/managed-disks-overview.md) и [Использование подключенных дисков данных](virtual-machine-scale-sets-attached-disks.md).</span><span class="sxs-lookup"><span data-stu-id="c1e5b-119">For more information about disks, see [Managed Disks Overview](../virtual-machines/windows/managed-disks-overview.md) and [Use Attached Data Disks](virtual-machine-scale-sets-attached-disks.md).</span></span>

## <a name="install-when-the-scale-set-is-provisioned"></a><span data-ttu-id="c1e5b-120">Установка при подготовке масштабируемого набора</span><span class="sxs-lookup"><span data-stu-id="c1e5b-120">Install when the scale set is provisioned</span></span>

<span data-ttu-id="c1e5b-121">Расширения виртуальных машин можно применить к масштабируемому набору виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="c1e5b-121">Virtual machine extensions can be applied to a virtual machine scale set.</span></span> <span data-ttu-id="c1e5b-122">Используя расширение виртуальной машины, можно настроить виртуальные машины в масштабируемом наборе как целую группу.</span><span class="sxs-lookup"><span data-stu-id="c1e5b-122">With a virtual machine extension, you can customize the virtual machines in a scale set as a whole group.</span></span> <span data-ttu-id="c1e5b-123">Дополнительные сведения о расширениях см. в статье, посвященной [расширениям виртуальных машин](../virtual-machines/windows/extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="c1e5b-123">For more information about extensions, see [Virtual Machine Extensions](../virtual-machines/windows/extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

<span data-ttu-id="c1e5b-124">Вы можете использовать три основных расширения в зависимости от типа операционной системы: Linux или Windows.</span><span class="sxs-lookup"><span data-stu-id="c1e5b-124">There are three main extensions you can use, depending on if your operating system is Linux-based or Windows-based.</span></span>

### <a name="windows"></a><span data-ttu-id="c1e5b-125">Windows</span><span class="sxs-lookup"><span data-stu-id="c1e5b-125">Windows</span></span>

<span data-ttu-id="c1e5b-126">Для операционной системы на основе Windows используйте расширение **Custom Script 1.8** или **PowerShell DSC**.</span><span class="sxs-lookup"><span data-stu-id="c1e5b-126">For a Windows-based operating system, use either the **Custom Script v1.8** extension, or the **PowerShell DSC** extension.</span></span>

#### <a name="custom-script"></a><span data-ttu-id="c1e5b-127">Custom Script</span><span class="sxs-lookup"><span data-stu-id="c1e5b-127">Custom Script</span></span>

<span data-ttu-id="c1e5b-128">Расширение Custom Script запускает сценарий на каждом экземпляре виртуальной машины в масштабируемом наборе.</span><span class="sxs-lookup"><span data-stu-id="c1e5b-128">The Custom Script extension runs a script on each virtual machine instance in the scale set.</span></span> <span data-ttu-id="c1e5b-129">В файле конфигурации или переменной указывается, какие файлы скачиваются на виртуальную машину и какие команды затем выполняются.</span><span class="sxs-lookup"><span data-stu-id="c1e5b-129">A config file or variable indicates which files are downloaded to the virtual machine, and then what command runs.</span></span> <span data-ttu-id="c1e5b-130">Таким образом, вы можете запустить, например, программу установки, сценарий, пакетный файл или любой исполняемый файл.</span><span class="sxs-lookup"><span data-stu-id="c1e5b-130">You could use this to run an installer, a script, a batch file, any executable for example.</span></span>

<span data-ttu-id="c1e5b-131">PowerShell использует для параметров хэш-таблицу.</span><span class="sxs-lookup"><span data-stu-id="c1e5b-131">PowerShell uses a hashtable for the settings.</span></span> <span data-ttu-id="c1e5b-132">В этом примере расширение Custom Script настраивается для запуска сценария PowerShell, который устанавливает службы IIS.</span><span class="sxs-lookup"><span data-stu-id="c1e5b-132">This example configures the custom script extension to run a PowerShell script that installs IIS.</span></span>

```powershell
# Setup extension configuration hashtable variable
$customConfig = @{
  "fileUris" = @("https://raw.githubusercontent.com/MicrosoftDocs/azure-cloud-services-files/temp/install-iis.ps1");
  "commandToExecute" = "PowerShell -ExecutionPolicy Unrestricted .\install-iis.ps1 >> `"%TEMP%\StartupLog.txt`" 2>&1";
};

# Add the extension to the config
Add-AzureRmVmssExtension -VirtualMachineScaleSet $vmssConfig -Publisher Microsoft.Compute -Type CustomScriptExtension -TypeHandlerVersion 1.8 -Name "customscript1" -Setting $customConfig

# Send the new config to Azure
Update-AzureRmVmss -ResourceGroupName $rg -Name "MyVmssTest143"  -VirtualMachineScaleSet $vmssConfig
```

>[!IMPORTANT]
><span data-ttu-id="c1e5b-133">Используйте параметр `-ProtectedSetting` для любых параметров, которые могут содержать конфиденциальные сведения.</span><span class="sxs-lookup"><span data-stu-id="c1e5b-133">Use the `-ProtectedSetting` switch for any settings that may contain sensitive information.</span></span>

---------


<span data-ttu-id="c1e5b-134">Интерфейс командной строки Azure использует для параметров JSON-файл.</span><span class="sxs-lookup"><span data-stu-id="c1e5b-134">Azure CLI uses a json file for the settings.</span></span> <span data-ttu-id="c1e5b-135">В этом примере расширение Custom Script настраивается для запуска сценария PowerShell, который устанавливает службы IIS.</span><span class="sxs-lookup"><span data-stu-id="c1e5b-135">This example configures the custom script extension to run a PowerShell script that installs IIS.</span></span> <span data-ttu-id="c1e5b-136">Сохраните следующий JSON-файл с именем _settings.json_.</span><span class="sxs-lookup"><span data-stu-id="c1e5b-136">Save the following json file as _settings.json_.</span></span>

```json
{
  "fileUris": [
    "https://raw.githubusercontent.com/MicrosoftDocs/azure-cloud-services-files/temp/install-iis.ps1"
  ],
  "commandToExecute": "PowerShell -ExecutionPolicy Unrestricted .\install-iis.ps1 >> \"%TEMP%\StartupLog.txt\" 2>&1"
}
```

<span data-ttu-id="c1e5b-137">Затем выполните следующую команду Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="c1e5b-137">Then, run this Azure CLI command.</span></span>

```azurecli
az vmss extension set --publisher Microsoft.Compute --version 1.8 --name CustomScriptExtension --resource-group myResourceGroup --vmss-name myScaleSet --settings @settings.json
```

>[!IMPORTANT]
><span data-ttu-id="c1e5b-138">Используйте параметр `--protected-settings` для любых параметров, которые могут содержать конфиденциальные сведения.</span><span class="sxs-lookup"><span data-stu-id="c1e5b-138">Use the `--protected-settings` switch for any settings that may contain sensitive information.</span></span>

### <a name="powershell-dsc"></a><span data-ttu-id="c1e5b-139">PowerShell DSC</span><span class="sxs-lookup"><span data-stu-id="c1e5b-139">PowerShell DSC</span></span>

<span data-ttu-id="c1e5b-140">PowerShell DSC можно использовать для настройки экземпляров виртуальных машин в масштабируемом наборе.</span><span class="sxs-lookup"><span data-stu-id="c1e5b-140">You can use PowerShell DSC to customize the scale set vm instances.</span></span> <span data-ttu-id="c1e5b-141">Расширение **DSC**, опубликованное **Microsoft.Powershell**, развертывает и запускает предоставленную конфигурацию DSC для каждого экземпляра виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="c1e5b-141">The **DSC** extension published by **Microsoft.Powershell** deploys and runs the provided DSC configuration on each virtual machine instance.</span></span> <span data-ttu-id="c1e5b-142">Файл конфигурации или переменная указывает расширению, где находится *ZIP*-пакет и какую комбинацию _сценария и функции_ использовать.</span><span class="sxs-lookup"><span data-stu-id="c1e5b-142">A config file or variable tells the extension where *.zip* package is, and which _script-function_ combination to run.</span></span>

<span data-ttu-id="c1e5b-143">PowerShell использует для параметров хэш-таблицу.</span><span class="sxs-lookup"><span data-stu-id="c1e5b-143">PowerShell uses a hashtable for the settings.</span></span> <span data-ttu-id="c1e5b-144">В этом примере развертывается пакет DSC, который устанавливает службы IIS.</span><span class="sxs-lookup"><span data-stu-id="c1e5b-144">This example deploys a DSC package that installs IIS.</span></span>

```powershell
# Setup extension configuration hashtable variable
$dscConfig = @{
  "wmfVersion" = "latest";
  "configuration" = @{
    "url" = "https://github.com/MicrosoftDocs/azure-cloud-services-files/raw/temp/dsc.zip";
    "script" = "configure-http.ps1";
    "function" = "WebsiteTest";
  };
}

# Add the extension to the config
Add-AzureRmVmssExtension -VirtualMachineScaleSet $vmssConfig -Publisher Microsoft.Powershell -Type DSC -TypeHandlerVersion 2.24 -Name "dsc1" -Setting $dscConfig

# Send the new config to Azure
Update-AzureRmVmss -ResourceGroupName $rg -Name "myscaleset1"  -VirtualMachineScaleSet $vmssConfig
```

>[!IMPORTANT]
><span data-ttu-id="c1e5b-145">Используйте параметр `-ProtectedSetting` для любых параметров, которые могут содержать конфиденциальные сведения.</span><span class="sxs-lookup"><span data-stu-id="c1e5b-145">Use the `-ProtectedSetting` switch for any settings that may contain sensitive information.</span></span>

-----------

<span data-ttu-id="c1e5b-146">Интерфейс командной строки Azure использует для параметров JSON-файл.</span><span class="sxs-lookup"><span data-stu-id="c1e5b-146">Azure CLI uses a json for the settings.</span></span> <span data-ttu-id="c1e5b-147">В этом примере развертывается пакет DSC, который устанавливает службы IIS.</span><span class="sxs-lookup"><span data-stu-id="c1e5b-147">This example deploys a DSC package that installs IIS.</span></span> <span data-ttu-id="c1e5b-148">Сохраните следующий JSON-файл с именем _settings.json_.</span><span class="sxs-lookup"><span data-stu-id="c1e5b-148">Save the following json file as _settings.json_.</span></span>

```json
{
  "wmfVersion": "latest",
  "configuration": {
    "url": "https://github.com/MicrosoftDocs/azure-cloud-services-files/raw/temp/dsc.zip",
    "script": "configure-http.ps1",
    "function": "WebsiteTest"
  }
}
```

<span data-ttu-id="c1e5b-149">Затем выполните следующую команду Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="c1e5b-149">Then, run this Azure CLI command.</span></span>

```azurecli
az vmss extension set --publisher Microsoft.Powershell --version 2.24 --name DSC --resource-group myResourceGroup --vmss-name myScaleSet --settings @settings.json
```

>[!IMPORTANT]
><span data-ttu-id="c1e5b-150">Используйте параметр `--protected-settings` для любых параметров, которые могут содержать конфиденциальные сведения.</span><span class="sxs-lookup"><span data-stu-id="c1e5b-150">Use the `--protected-settings` switch for any settings that may contain sensitive information.</span></span>

### <a name="linux"></a><span data-ttu-id="c1e5b-151"> Linux</span><span class="sxs-lookup"><span data-stu-id="c1e5b-151">Linux</span></span>

<span data-ttu-id="c1e5b-152">Linux может использовать расширение **Custom Script 2.0** или пакет **cloud-init** во время создания.</span><span class="sxs-lookup"><span data-stu-id="c1e5b-152">Linux can use either the **Custom Script v2.0** extension or use **cloud-init** during creation.</span></span>

<span data-ttu-id="c1e5b-153">Custom Script представляет собой простое расширение, которое загружает файлы в экземпляры виртуальной машины и выполняет команду.</span><span class="sxs-lookup"><span data-stu-id="c1e5b-153">Custom script is a simple extension that downloads files to the virtual machine instances, and runs a command.</span></span>

#### <a name="custom-script"></a><span data-ttu-id="c1e5b-154">Custom Script</span><span class="sxs-lookup"><span data-stu-id="c1e5b-154">Custom Script</span></span>

<span data-ttu-id="c1e5b-155">Сохраните следующий JSON-файл с именем _settings.json_.</span><span class="sxs-lookup"><span data-stu-id="c1e5b-155">Save the following json file as _settings.json_.</span></span>

```json
{
  "fileUris": [
    "https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-vmss-bottle-autoscale/installserver.sh",
    "https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-vmss-bottle-autoscale/workserver.py"
  ],
  "commandToExecute": "bash installserver.sh"
}
```

<span data-ttu-id="c1e5b-156">Используйте Azure CLI для добавления этого расширения в существующий масштабируемый набор виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="c1e5b-156">Use the Azure CLI to add this extension to an existing virtual machine scale set.</span></span> <span data-ttu-id="c1e5b-157">Каждая виртуальная машина в масштабируемом наборе автоматически запускает расширение.</span><span class="sxs-lookup"><span data-stu-id="c1e5b-157">Each virtual machine in the scale set automatically runs the extension.</span></span>

```azurecli
az vmss extension set --publisher Microsoft.Azure.Extensions --version 2.0 --name CustomScript --resource-group myResourceGroup --vmss-name myScaleSet --settings @settings.json
```

>[!IMPORTANT]
><span data-ttu-id="c1e5b-158">Используйте параметр `--protected-settings` для любых параметров, которые могут содержать конфиденциальные сведения.</span><span class="sxs-lookup"><span data-stu-id="c1e5b-158">Use the `--protected-settings` switch for any settings that may contain sensitive information.</span></span>

#### <a name="cloud-init"></a><span data-ttu-id="c1e5b-159">Cloud-Init</span><span class="sxs-lookup"><span data-stu-id="c1e5b-159">Cloud-Init</span></span>

<span data-ttu-id="c1e5b-160">Cloud-Init используется при создании масштабируемого набора.</span><span class="sxs-lookup"><span data-stu-id="c1e5b-160">Cloud-Init is used when the scale set is created.</span></span> <span data-ttu-id="c1e5b-161">Во-первых, создайте локальный файл с именем _cloud-init.txt_ и добавьте в него свою конфигурацию.</span><span class="sxs-lookup"><span data-stu-id="c1e5b-161">First, create a local file named _cloud-init.txt_ and add your configuration to it.</span></span> <span data-ttu-id="c1e5b-162">Например, ознакомьтесь с [этой статьей](https://gist.github.com/Thraka/27bd66b1fb79e11904fb62b7de08a8a6#file-cloud-init-txt).</span><span class="sxs-lookup"><span data-stu-id="c1e5b-162">For example, see [this gist](https://gist.github.com/Thraka/27bd66b1fb79e11904fb62b7de08a8a6#file-cloud-init-txt)</span></span>

<span data-ttu-id="c1e5b-163">Используйте интерфейс командной строки Azure для создания масштабируемого набора.</span><span class="sxs-lookup"><span data-stu-id="c1e5b-163">Use the Azure CLI to create a scale set.</span></span> <span data-ttu-id="c1e5b-164">В поле `--custom-data` можно ввести имя файла сценария cloud-init.</span><span class="sxs-lookup"><span data-stu-id="c1e5b-164">The `--custom-data` field accepts the file name of a cloud-init script.</span></span>

```azurecli
az vmss create \
  --resource-group myResourceGroupScaleSet \
  --name myScaleSet \
  --image Canonical:UbuntuServer:14.04.4-LTS:latest \
  --upgrade-policy-mode automatic \
  --custom-data cloud-init.txt \
  --admin-username azureuser \
  --generate-ssh-keys      
```

## <a name="how-do-i-manage-application-updates"></a><span data-ttu-id="c1e5b-165">Как управлять обновлениями приложений?</span><span class="sxs-lookup"><span data-stu-id="c1e5b-165">How do I manage application updates?</span></span>

<span data-ttu-id="c1e5b-166">При развертывании приложения с помощью расширения измените определение расширения каким-либо образом.</span><span class="sxs-lookup"><span data-stu-id="c1e5b-166">If you deployed your application through an extension, alter the extension definition in some way.</span></span> <span data-ttu-id="c1e5b-167">Это изменение вызовет повторное развертывание расширения для всех экземпляров виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="c1e5b-167">This change causes the extension to be redeployed to all virtual machine instances.</span></span> <span data-ttu-id="c1e5b-168">В расширение **необходимо** внести какие-либо изменения, например переименовать указанный файл, в противном случае Azure не определит расширение как измененное.</span><span class="sxs-lookup"><span data-stu-id="c1e5b-168">Something **must** be changed about the extension, such as renaming a referenced file, otherwise, Azure does not see that the extension has changed.</span></span>

<span data-ttu-id="c1e5b-169">Если приложение встроено в образ операционной системы, используйте для обновления приложения конвейер автоматизированного развертывания.</span><span class="sxs-lookup"><span data-stu-id="c1e5b-169">If you baked the application into your own operating system image, use an automated deployment pipeline for application updates.</span></span> <span data-ttu-id="c1e5b-170">Спроектируйте архитектуру таким образом, чтобы упростить быстрый ввод промежуточного масштабируемого набора в рабочую среду.</span><span class="sxs-lookup"><span data-stu-id="c1e5b-170">Design your architecture to facilitate rapid swapping of a staged scale set into production.</span></span> <span data-ttu-id="c1e5b-171">Хорошим примером этого подхода является [работа драйвера Azure Spinnaker](https://github.com/spinnaker/deck/tree/master/app/scripts/modules/azure) - [http://www.spinnaker.io/](http://www.spinnaker.io/).</span><span class="sxs-lookup"><span data-stu-id="c1e5b-171">A good example of this approach is the [Azure Spinnaker driver work](https://github.com/spinnaker/deck/tree/master/app/scripts/modules/azure) - [http://www.spinnaker.io/](http://www.spinnaker.io/).</span></span>

<span data-ttu-id="c1e5b-172">[Packer](https://www.packer.io/) и [Terraform](https://www.terraform.io/) поддерживают Azure Resource Manager, поэтому можно определить свои образы в виде кода, создать их в Azure и затем использовать виртуальный жесткий диск в масштабируемом наборе.</span><span class="sxs-lookup"><span data-stu-id="c1e5b-172">[Packer](https://www.packer.io/) and [Terraform](https://www.terraform.io/) support Azure Resource Manager, so you can also define your images "as code" and build them in Azure, then use the VHD in your scale set.</span></span> <span data-ttu-id="c1e5b-173">Но такой подход не подходит для образов Marketplace, в которых расширения и пользовательские сценарии более важны, так как вы не оперируете данными из Marketplace напрямую.</span><span class="sxs-lookup"><span data-stu-id="c1e5b-173">However, doing so would become problematic for marketplace images, where extensions/custom scripts become more important since you don’t directly manipulate bits from marketplace.</span></span>

## <a name="what-happens-when-a-scale-set-scales-out"></a><span data-ttu-id="c1e5b-174">Что происходит при расширении масштабируемого набора?</span><span class="sxs-lookup"><span data-stu-id="c1e5b-174">What happens when a scale set scales out?</span></span>
<span data-ttu-id="c1e5b-175">При добавлении одной или нескольких виртуальных машин в масштабируемый набор приложение устанавливается автоматически.</span><span class="sxs-lookup"><span data-stu-id="c1e5b-175">When you add one or more virtual machines to a scale set, the application is automatically installed.</span></span> <span data-ttu-id="c1e5b-176">Например, если в масштабируемом наборе определены расширения, то они будут запускаться на каждой новой виртуальной машине при ее создании.</span><span class="sxs-lookup"><span data-stu-id="c1e5b-176">For example if the scale set has extensions defined, they run on a new virtual machine each time it is created.</span></span> <span data-ttu-id="c1e5b-177">Если масштабируемый набор основан на исходном пользовательском образе, то любая новая виртуальная машина является его копией.</span><span class="sxs-lookup"><span data-stu-id="c1e5b-177">If the scale set is based on a custom image, any new virtual machine is a copy of the source custom image.</span></span> <span data-ttu-id="c1e5b-178">Если виртуальные машины в масштабируемом наборе являются узлами контейнера, возможно, потребуется реализовать загрузку контейнеров кодом запуска в расширение Custom Script.</span><span class="sxs-lookup"><span data-stu-id="c1e5b-178">If the scale set virtual machines are container hosts, then you might have startup code to load the containers in a Custom Script Extension.</span></span> <span data-ttu-id="c1e5b-179">Кроме того, расширение может устанавливать агент, который регистрируется в оркестраторе кластера, например в службе контейнеров Azure.</span><span class="sxs-lookup"><span data-stu-id="c1e5b-179">Or, an extension might install an agent that registers with a cluster orchestrator, such as Azure Container Service.</span></span>


## <a name="how-do-you-roll-out-an-os-update-across-update-domains"></a><span data-ttu-id="c1e5b-180">Как можно развернуть обновление ОС в доменах обновления?</span><span class="sxs-lookup"><span data-stu-id="c1e5b-180">How do you roll out an OS update across update domains?</span></span>
<span data-ttu-id="c1e5b-181">Предположим, вам требуется обновить образ ОС, не прерывая работу масштабируемого набора виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="c1e5b-181">Suppose you want to update your OS image while keeping the virtual machine scale set running.</span></span> <span data-ttu-id="c1e5b-182">PowerShell и Azure CLI могут обновлять образы виртуальных машин, по одной виртуальной машине за раз.</span><span class="sxs-lookup"><span data-stu-id="c1e5b-182">PowerShell and the Azure CLI can update the virtual machine images, one virtual machine at a time.</span></span> <span data-ttu-id="c1e5b-183">В статье [Обновление набора масштабирования виртуальных машин](./virtual-machine-scale-sets-upgrade-scale-set.md) также содержатся сведения о том, какие варианты обновления операционной системы доступны в масштабируемом наборе виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="c1e5b-183">The [Upgrade a Virtual Machine Scale Set](./virtual-machine-scale-sets-upgrade-scale-set.md) article also provides further information on what options are available to perform an operating system upgrade across a virtual machine scale set.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c1e5b-184">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="c1e5b-184">Next steps</span></span>

* [<span data-ttu-id="c1e5b-185">Управление масштабируемым набором с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="c1e5b-185">Use PowerShell to manage your scale set.</span></span>](virtual-machine-scale-sets-windows-manage.md)
* [<span data-ttu-id="c1e5b-186">Создание шаблона масштабируемого набора</span><span class="sxs-lookup"><span data-stu-id="c1e5b-186">Create a scale set template.</span></span>](virtual-machine-scale-sets-mvss-start.md)


[linux-vm-create]: ../virtual-machines/linux/tutorial-manage-vm.md
[windows-vm-create]: ../virtual-machines/windows/tutorial-manage-vm.md
[linux-vm-capture]: ../virtual-machines/linux/capture-image.md
[windows-vm-capture]: ../virtual-machines/windows/capture-image.md 
[vmss-create]: virtual-machine-scale-sets-create.md

