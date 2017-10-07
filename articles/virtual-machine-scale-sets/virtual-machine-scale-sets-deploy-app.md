---
title: "Задает aaaDeploy приложения на масштабирования виртуальных машин"
description: "Наборы масштабирования виртуальных машин Azure используйте toodepoy расширения приложения."
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
ms.openlocfilehash: 5f3988b9511d80370a8be1fc042c21fee212506e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-your-application-on-virtual-machine-scale-sets"></a><span data-ttu-id="5da1c-103">Развертывание приложения в масштабируемых наборах виртуальных машин</span><span class="sxs-lookup"><span data-stu-id="5da1c-103">Deploy your application on virtual machine scale sets</span></span>

<span data-ttu-id="5da1c-104">В этой статье описываются различные способы как задать tooinstall программное обеспечение в масштабе hello hello время подготовки.</span><span class="sxs-lookup"><span data-stu-id="5da1c-104">This article describes different ways of how tooinstall software at hello time hello scale set is provisioned.</span></span>

<span data-ttu-id="5da1c-105">Вы можете tooreview hello [Обзор разработки установите масштаб](virtual-machine-scale-sets-design-overview.md) статьи, которая описывает некоторые hello ограничения, накладываемые наборы масштабирования виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="5da1c-105">You may want tooreview hello [Scale Set Design Overview](virtual-machine-scale-sets-design-overview.md) article, which describes some of hello limits imposed by virtual machine scale sets.</span></span>

## <a name="capture-and-reuse-an-image"></a><span data-ttu-id="5da1c-106">Запись и повторное использование образа</span><span class="sxs-lookup"><span data-stu-id="5da1c-106">Capture and reuse an image</span></span>

<span data-ttu-id="5da1c-107">Можно использовать виртуальную машину, заданные в Azure tooprepare базового образа для масштаба.</span><span class="sxs-lookup"><span data-stu-id="5da1c-107">You can use a virtual machine you have in Azure tooprepare a base-image for your scale set.</span></span> <span data-ttu-id="5da1c-108">Этот процесс создает управляемого диска вашей учетной записи хранилища, который может ссылаться в качестве базового образа hello для набора масштабирования.</span><span class="sxs-lookup"><span data-stu-id="5da1c-108">This process creates a managed disk in your storage account, which you can reference as hello base image for your scale set.</span></span> 

<span data-ttu-id="5da1c-109">Здравствуйте, следующие действия:</span><span class="sxs-lookup"><span data-stu-id="5da1c-109">Do hello following steps:</span></span>

1. <span data-ttu-id="5da1c-110">Создайте виртуальную машину Azure</span><span class="sxs-lookup"><span data-stu-id="5da1c-110">Create an Azure Virtual Machine</span></span>
   * <span data-ttu-id="5da1c-111">[Linux][linux-vm-create]</span><span class="sxs-lookup"><span data-stu-id="5da1c-111">[Linux][linux-vm-create]</span></span>
   * <span data-ttu-id="5da1c-112">[Windows][windows-vm-create]</span><span class="sxs-lookup"><span data-stu-id="5da1c-112">[Windows][windows-vm-create]</span></span>

2. <span data-ttu-id="5da1c-113">В удаленном hello виртуальной машины и настроить оформлением tooyour hello системы.</span><span class="sxs-lookup"><span data-stu-id="5da1c-113">Remote into hello virtual machine and customize hello system tooyour liking.</span></span>

   <span data-ttu-id="5da1c-114">Теперь вы можете установить приложение.</span><span class="sxs-lookup"><span data-stu-id="5da1c-114">If you want, you can install your application now.</span></span> <span data-ttu-id="5da1c-115">Однако следует помнить, что путем установки приложения, вы можете сделать обновление более сложные приложения, так как может потребоваться tooremove его первого.</span><span class="sxs-lookup"><span data-stu-id="5da1c-115">However, know that by installing your application now, you may make upgrading your application more complicated because you may need tooremove it first.</span></span> <span data-ttu-id="5da1c-116">Вместо этого можно использовать этот шаг tooinstall все необходимые компоненты, которые могут потребоваться приложение, например определенных компонентов операционной системы или среды выполнения.</span><span class="sxs-lookup"><span data-stu-id="5da1c-116">Instead, you can use this step tooinstall any prerequisites your application may need, like a specific runtime or operating system feature.</span></span>

3. <span data-ttu-id="5da1c-117">Выполните действия из учебника «запись машины» hello либо для [Linux] [ linux-vm-capture] или [Windows][windows-vm-capture].</span><span class="sxs-lookup"><span data-stu-id="5da1c-117">Follow hello "capture a machine" tutorial for either [Linux][linux-vm-capture] or [Windows][windows-vm-capture].</span></span>

4. <span data-ttu-id="5da1c-118">Создание [набора масштабирования виртуальных машин] [ vmss-create] с hello изображения URI, записанный в предыдущем шаге hello.</span><span class="sxs-lookup"><span data-stu-id="5da1c-118">Create a [Virtual Machine Scale Set][vmss-create] with hello image URI you captured in hello previous step.</span></span>

<span data-ttu-id="5da1c-119">Дополнительные сведения о дисках см. в статьях [Обзор управляемых дисков](../virtual-machines/windows/managed-disks-overview.md) и [Использование подключенных дисков данных](virtual-machine-scale-sets-attached-disks.md).</span><span class="sxs-lookup"><span data-stu-id="5da1c-119">For more information about disks, see [Managed Disks Overview](../virtual-machines/windows/managed-disks-overview.md) and [Use Attached Data Disks](virtual-machine-scale-sets-attached-disks.md).</span></span>

## <a name="install-when-hello-scale-set-is-provisioned"></a><span data-ttu-id="5da1c-120">Установка при подготовке набор масштабирования hello</span><span class="sxs-lookup"><span data-stu-id="5da1c-120">Install when hello scale set is provisioned</span></span>

<span data-ttu-id="5da1c-121">Расширения виртуальных машин может быть применен tooa набора масштабирования виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="5da1c-121">Virtual machine extensions can be applied tooa virtual machine scale set.</span></span> <span data-ttu-id="5da1c-122">Расширение виртуальной машины позволяет настраивать hello виртуальных машин в качестве всей группы масштабирования.</span><span class="sxs-lookup"><span data-stu-id="5da1c-122">With a virtual machine extension, you can customize hello virtual machines in a scale set as a whole group.</span></span> <span data-ttu-id="5da1c-123">Дополнительные сведения о расширениях см. в статье, посвященной [расширениям виртуальных машин](../virtual-machines/windows/extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="5da1c-123">For more information about extensions, see [Virtual Machine Extensions](../virtual-machines/windows/extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

<span data-ttu-id="5da1c-124">Вы можете использовать три основных расширения в зависимости от типа операционной системы: Linux или Windows.</span><span class="sxs-lookup"><span data-stu-id="5da1c-124">There are three main extensions you can use, depending on if your operating system is Linux-based or Windows-based.</span></span>

### <a name="windows"></a><span data-ttu-id="5da1c-125">Windows</span><span class="sxs-lookup"><span data-stu-id="5da1c-125">Windows</span></span>

<span data-ttu-id="5da1c-126">Для операционной системы на основе Windows, используйте либо hello **версии 1.8 пользовательский сценарий** расширения или hello **PowerShell DSC** расширения.</span><span class="sxs-lookup"><span data-stu-id="5da1c-126">For a Windows-based operating system, use either hello **Custom Script v1.8** extension, or hello **PowerShell DSC** extension.</span></span>

#### <a name="custom-script"></a><span data-ttu-id="5da1c-127">Custom Script</span><span class="sxs-lookup"><span data-stu-id="5da1c-127">Custom Script</span></span>

<span data-ttu-id="5da1c-128">Hello расширение пользовательского скрипта запускает сценарий на каждом экземпляре виртуальной машины в наборе масштабирования hello.</span><span class="sxs-lookup"><span data-stu-id="5da1c-128">hello Custom Script extension runs a script on each virtual machine instance in hello scale set.</span></span> <span data-ttu-id="5da1c-129">Файл конфигурации или переменная указывает файлы, загруженные toohello виртуальной машины, а затем выполняет команду.</span><span class="sxs-lookup"><span data-stu-id="5da1c-129">A config file or variable indicates which files are downloaded toohello virtual machine, and then what command runs.</span></span> <span data-ttu-id="5da1c-130">Можно использовать этот установщик toorun, сценария, пакетный файл любых исполняемых файлов, например.</span><span class="sxs-lookup"><span data-stu-id="5da1c-130">You could use this toorun an installer, a script, a batch file, any executable for example.</span></span>

<span data-ttu-id="5da1c-131">PowerShell использует хэш-таблицу для параметров hello.</span><span class="sxs-lookup"><span data-stu-id="5da1c-131">PowerShell uses a hashtable for hello settings.</span></span> <span data-ttu-id="5da1c-132">В этом примере настраивается toorun расширение пользовательского скрипта hello сценарий PowerShell, установка служб IIS.</span><span class="sxs-lookup"><span data-stu-id="5da1c-132">This example configures hello custom script extension toorun a PowerShell script that installs IIS.</span></span>

```powershell
# Setup extension configuration hashtable variable
$customConfig = @{
  "fileUris" = @("https://raw.githubusercontent.com/MicrosoftDocs/azure-cloud-services-files/temp/install-iis.ps1");
  "commandToExecute" = "PowerShell -ExecutionPolicy Unrestricted .\install-iis.ps1 >> `"%TEMP%\StartupLog.txt`" 2>&1";
};

# Add hello extension toohello config
Add-AzureRmVmssExtension -VirtualMachineScaleSet $vmssConfig -Publisher Microsoft.Compute -Type CustomScriptExtension -TypeHandlerVersion 1.8 -Name "customscript1" -Setting $customConfig

# Send hello new config tooAzure
Update-AzureRmVmss -ResourceGroupName $rg -Name "MyVmssTest143"  -VirtualMachineScaleSet $vmssConfig
```

>[!IMPORTANT]
><span data-ttu-id="5da1c-133">Используйте hello `-ProtectedSetting` переключения для любых параметров, которые могут содержать конфиденциальные сведения.</span><span class="sxs-lookup"><span data-stu-id="5da1c-133">Use hello `-ProtectedSetting` switch for any settings that may contain sensitive information.</span></span>

---------


<span data-ttu-id="5da1c-134">Azure CLI использует файл json для параметров hello.</span><span class="sxs-lookup"><span data-stu-id="5da1c-134">Azure CLI uses a json file for hello settings.</span></span> <span data-ttu-id="5da1c-135">В этом примере настраивается toorun расширение пользовательского скрипта hello сценарий PowerShell, установка служб IIS.</span><span class="sxs-lookup"><span data-stu-id="5da1c-135">This example configures hello custom script extension toorun a PowerShell script that installs IIS.</span></span> <span data-ttu-id="5da1c-136">Сохранить следующие файл json как hello _settings.json_.</span><span class="sxs-lookup"><span data-stu-id="5da1c-136">Save hello following json file as _settings.json_.</span></span>

```json
{
  "fileUris": [
    "https://raw.githubusercontent.com/MicrosoftDocs/azure-cloud-services-files/temp/install-iis.ps1"
  ],
  "commandToExecute": "PowerShell -ExecutionPolicy Unrestricted .\install-iis.ps1 >> \"%TEMP%\StartupLog.txt\" 2>&1"
}
```

<span data-ttu-id="5da1c-137">Затем выполните следующую команду Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="5da1c-137">Then, run this Azure CLI command.</span></span>

```azurecli
az vmss extension set --publisher Microsoft.Compute --version 1.8 --name CustomScriptExtension --resource-group myResourceGroup --vmss-name myScaleSet --settings @settings.json
```

>[!IMPORTANT]
><span data-ttu-id="5da1c-138">Используйте hello `--protected-settings` переключения для любых параметров, которые могут содержать конфиденциальные сведения.</span><span class="sxs-lookup"><span data-stu-id="5da1c-138">Use hello `--protected-settings` switch for any settings that may contain sensitive information.</span></span>

### <a name="powershell-dsc"></a><span data-ttu-id="5da1c-139">PowerShell DSC</span><span class="sxs-lookup"><span data-stu-id="5da1c-139">PowerShell DSC</span></span>

<span data-ttu-id="5da1c-140">Можно использовать PowerShell DSC toocustomize hello шкалы набор экземпляров виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="5da1c-140">You can use PowerShell DSC toocustomize hello scale set vm instances.</span></span> <span data-ttu-id="5da1c-141">Hello **DSC** опубликованное расширение **Microsoft.Powershell** развертывает и запускает конфигурацию DSC hello указано на каждый экземпляр виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="5da1c-141">hello **DSC** extension published by **Microsoft.Powershell** deploys and runs hello provided DSC configuration on each virtual machine instance.</span></span> <span data-ttu-id="5da1c-142">Файл конфигурации или переменной указывает расширение hello где *.zip* пакета, а какие _функции скрипта_ toorun сочетания.</span><span class="sxs-lookup"><span data-stu-id="5da1c-142">A config file or variable tells hello extension where *.zip* package is, and which _script-function_ combination toorun.</span></span>

<span data-ttu-id="5da1c-143">PowerShell использует хэш-таблицу для параметров hello.</span><span class="sxs-lookup"><span data-stu-id="5da1c-143">PowerShell uses a hashtable for hello settings.</span></span> <span data-ttu-id="5da1c-144">В этом примере развертывается пакет DSC, который устанавливает службы IIS.</span><span class="sxs-lookup"><span data-stu-id="5da1c-144">This example deploys a DSC package that installs IIS.</span></span>

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

# Add hello extension toohello config
Add-AzureRmVmssExtension -VirtualMachineScaleSet $vmssConfig -Publisher Microsoft.Powershell -Type DSC -TypeHandlerVersion 2.24 -Name "dsc1" -Setting $dscConfig

# Send hello new config tooAzure
Update-AzureRmVmss -ResourceGroupName $rg -Name "myscaleset1"  -VirtualMachineScaleSet $vmssConfig
```

>[!IMPORTANT]
><span data-ttu-id="5da1c-145">Используйте hello `-ProtectedSetting` переключения для любых параметров, которые могут содержать конфиденциальные сведения.</span><span class="sxs-lookup"><span data-stu-id="5da1c-145">Use hello `-ProtectedSetting` switch for any settings that may contain sensitive information.</span></span>

-----------

<span data-ttu-id="5da1c-146">Azure CLI использует json для параметров hello.</span><span class="sxs-lookup"><span data-stu-id="5da1c-146">Azure CLI uses a json for hello settings.</span></span> <span data-ttu-id="5da1c-147">В этом примере развертывается пакет DSC, который устанавливает службы IIS.</span><span class="sxs-lookup"><span data-stu-id="5da1c-147">This example deploys a DSC package that installs IIS.</span></span> <span data-ttu-id="5da1c-148">Сохранить следующие файл json как hello _settings.json_.</span><span class="sxs-lookup"><span data-stu-id="5da1c-148">Save hello following json file as _settings.json_.</span></span>

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

<span data-ttu-id="5da1c-149">Затем выполните следующую команду Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="5da1c-149">Then, run this Azure CLI command.</span></span>

```azurecli
az vmss extension set --publisher Microsoft.Powershell --version 2.24 --name DSC --resource-group myResourceGroup --vmss-name myScaleSet --settings @settings.json
```

>[!IMPORTANT]
><span data-ttu-id="5da1c-150">Используйте hello `--protected-settings` переключения для любых параметров, которые могут содержать конфиденциальные сведения.</span><span class="sxs-lookup"><span data-stu-id="5da1c-150">Use hello `--protected-settings` switch for any settings that may contain sensitive information.</span></span>

### <a name="linux"></a><span data-ttu-id="5da1c-151">Linux</span><span class="sxs-lookup"><span data-stu-id="5da1c-151">Linux</span></span>

<span data-ttu-id="5da1c-152">Linux можно использовать либо hello **v2.0 пользовательский сценарий** расширения или используйте **облака init** во время создания.</span><span class="sxs-lookup"><span data-stu-id="5da1c-152">Linux can use either hello **Custom Script v2.0** extension or use **cloud-init** during creation.</span></span>

<span data-ttu-id="5da1c-153">Пользовательский скрипт является простой расширение, которое загружает файлы экземпляров виртуальных машин toohello и выполняет команду.</span><span class="sxs-lookup"><span data-stu-id="5da1c-153">Custom script is a simple extension that downloads files toohello virtual machine instances, and runs a command.</span></span>

#### <a name="custom-script"></a><span data-ttu-id="5da1c-154">Custom Script</span><span class="sxs-lookup"><span data-stu-id="5da1c-154">Custom Script</span></span>

<span data-ttu-id="5da1c-155">Сохранить следующие файл json как hello _settings.json_.</span><span class="sxs-lookup"><span data-stu-id="5da1c-155">Save hello following json file as _settings.json_.</span></span>

```json
{
  "fileUris": [
    "https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-vmss-bottle-autoscale/installserver.sh",
    "https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-vmss-bottle-autoscale/workserver.py"
  ],
  "commandToExecute": "bash installserver.sh"
}
```

<span data-ttu-id="5da1c-156">Используйте этот tooan расширение существующего набора масштабирования виртуальных машин tooadd hello Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="5da1c-156">Use hello Azure CLI tooadd this extension tooan existing virtual machine scale set.</span></span> <span data-ttu-id="5da1c-157">Каждая виртуальная машина в шкале hello автоматически задать расширение hello запусков.</span><span class="sxs-lookup"><span data-stu-id="5da1c-157">Each virtual machine in hello scale set automatically runs hello extension.</span></span>

```azurecli
az vmss extension set --publisher Microsoft.Azure.Extensions --version 2.0 --name CustomScript --resource-group myResourceGroup --vmss-name myScaleSet --settings @settings.json
```

>[!IMPORTANT]
><span data-ttu-id="5da1c-158">Используйте hello `--protected-settings` переключения для любых параметров, которые могут содержать конфиденциальные сведения.</span><span class="sxs-lookup"><span data-stu-id="5da1c-158">Use hello `--protected-settings` switch for any settings that may contain sensitive information.</span></span>

#### <a name="cloud-init"></a><span data-ttu-id="5da1c-159">Cloud-Init</span><span class="sxs-lookup"><span data-stu-id="5da1c-159">Cloud-Init</span></span>

<span data-ttu-id="5da1c-160">Init облако используется при создании набора масштабирования hello.</span><span class="sxs-lookup"><span data-stu-id="5da1c-160">Cloud-Init is used when hello scale set is created.</span></span> <span data-ttu-id="5da1c-161">Сначала создайте локальный файл с именем _init.txt облака_ и добавьте tooit вашей конфигурации.</span><span class="sxs-lookup"><span data-stu-id="5da1c-161">First, create a local file named _cloud-init.txt_ and add your configuration tooit.</span></span> <span data-ttu-id="5da1c-162">Например, ознакомьтесь с [этой статьей](https://gist.github.com/Thraka/27bd66b1fb79e11904fb62b7de08a8a6#file-cloud-init-txt).</span><span class="sxs-lookup"><span data-stu-id="5da1c-162">For example, see [this gist](https://gist.github.com/Thraka/27bd66b1fb79e11904fb62b7de08a8a6#file-cloud-init-txt)</span></span>

<span data-ttu-id="5da1c-163">Задать использование hello Azure CLI toocreate шкалу.</span><span class="sxs-lookup"><span data-stu-id="5da1c-163">Use hello Azure CLI toocreate a scale set.</span></span> <span data-ttu-id="5da1c-164">Hello `--custom-data` hello имя файла скрипта облака init принимает поле.</span><span class="sxs-lookup"><span data-stu-id="5da1c-164">hello `--custom-data` field accepts hello file name of a cloud-init script.</span></span>

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

## <a name="how-do-i-manage-application-updates"></a><span data-ttu-id="5da1c-165">Как управлять обновлениями приложений?</span><span class="sxs-lookup"><span data-stu-id="5da1c-165">How do I manage application updates?</span></span>

<span data-ttu-id="5da1c-166">Если вы развернули приложение через расширение, измените определение расширения hello иным образом.</span><span class="sxs-lookup"><span data-stu-id="5da1c-166">If you deployed your application through an extension, alter hello extension definition in some way.</span></span> <span data-ttu-id="5da1c-167">В результате изменения экземпляров виртуальных машин tooall toobe повторного развертывания расширения hello.</span><span class="sxs-lookup"><span data-stu-id="5da1c-167">This change causes hello extension toobe redeployed tooall virtual machine instances.</span></span> <span data-ttu-id="5da1c-168">Что-то **должен** изменить сведения о расширении hello, таких как переименование указанный файл, в противном случае Azure выполняет не. при этом hello расширение изменилось.</span><span class="sxs-lookup"><span data-stu-id="5da1c-168">Something **must** be changed about hello extension, such as renaming a referenced file, otherwise, Azure does not see that hello extension has changed.</span></span>

<span data-ttu-id="5da1c-169">Если приложение hello помещенного в свой собственный образ операционной системы, используйте конвейер автоматического развертывания для обновлений приложения.</span><span class="sxs-lookup"><span data-stu-id="5da1c-169">If you baked hello application into your own operating system image, use an automated deployment pipeline for application updates.</span></span> <span data-ttu-id="5da1c-170">Разработка вашей архитектуры toofacilitate Быстрая замена промежуточные шкалы набор в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="5da1c-170">Design your architecture toofacilitate rapid swapping of a staged scale set into production.</span></span> <span data-ttu-id="5da1c-171">Хорошим примером такого подхода является hello [работы драйвера Azure Spinnaker](https://github.com/spinnaker/deck/tree/master/app/scripts/modules/azure) - [http://www.spinnaker.io/](http://www.spinnaker.io/).</span><span class="sxs-lookup"><span data-stu-id="5da1c-171">A good example of this approach is hello [Azure Spinnaker driver work](https://github.com/spinnaker/deck/tree/master/app/scripts/modules/azure) - [http://www.spinnaker.io/](http://www.spinnaker.io/).</span></span>

<span data-ttu-id="5da1c-172">[Packer](https://www.packer.io/) и [Terraform](https://www.terraform.io/) поддержки диспетчера ресурсов Azure, поэтому можно определить образы «как код» и создавать их в Azure, затем с помощью hello виртуального жесткого диска в наборе масштабирования.</span><span class="sxs-lookup"><span data-stu-id="5da1c-172">[Packer](https://www.packer.io/) and [Terraform](https://www.terraform.io/) support Azure Resource Manager, so you can also define your images "as code" and build them in Azure, then use hello VHD in your scale set.</span></span> <span data-ttu-id="5da1c-173">Но такой подход не подходит для образов Marketplace, в которых расширения и пользовательские сценарии более важны, так как вы не оперируете данными из Marketplace напрямую.</span><span class="sxs-lookup"><span data-stu-id="5da1c-173">However, doing so would become problematic for marketplace images, where extensions/custom scripts become more important since you don’t directly manipulate bits from marketplace.</span></span>

## <a name="what-happens-when-a-scale-set-scales-out"></a><span data-ttu-id="5da1c-174">Что происходит при расширении масштабируемого набора?</span><span class="sxs-lookup"><span data-stu-id="5da1c-174">What happens when a scale set scales out?</span></span>
<span data-ttu-id="5da1c-175">При добавлении одного или нескольких виртуальных машин tooa набор масштабирования приложения hello устанавливается автоматически.</span><span class="sxs-lookup"><span data-stu-id="5da1c-175">When you add one or more virtual machines tooa scale set, hello application is automatically installed.</span></span> <span data-ttu-id="5da1c-176">Для примера, если задать масштаб hello имеет расширения, определенные, выполняются на новую виртуальную машину при каждом его создания.</span><span class="sxs-lookup"><span data-stu-id="5da1c-176">For example if hello scale set has extensions defined, they run on a new virtual machine each time it is created.</span></span> <span data-ttu-id="5da1c-177">Если набор масштабирования hello основана на пользовательский образ, любой новой виртуальной машины является копией hello источник пользовательского изображения.</span><span class="sxs-lookup"><span data-stu-id="5da1c-177">If hello scale set is based on a custom image, any new virtual machine is a copy of hello source custom image.</span></span> <span data-ttu-id="5da1c-178">Если узлы контейнера hello шкалы набор виртуальных машин, может иметь hello tooload контейнеры для запуска кода в настраиваемое расширение скриптов.</span><span class="sxs-lookup"><span data-stu-id="5da1c-178">If hello scale set virtual machines are container hosts, then you might have startup code tooload hello containers in a Custom Script Extension.</span></span> <span data-ttu-id="5da1c-179">Кроме того, расширение может устанавливать агент, который регистрируется в оркестраторе кластера, например в службе контейнеров Azure.</span><span class="sxs-lookup"><span data-stu-id="5da1c-179">Or, an extension might install an agent that registers with a cluster orchestrator, such as Azure Container Service.</span></span>


## <a name="how-do-you-roll-out-an-os-update-across-update-domains"></a><span data-ttu-id="5da1c-180">Как можно развернуть обновление ОС в доменах обновления?</span><span class="sxs-lookup"><span data-stu-id="5da1c-180">How do you roll out an OS update across update domains?</span></span>
<span data-ttu-id="5da1c-181">Предположим, что нужно tooupdate образа ОС, сохраняя hello масштабирования виртуальных машин установите под управлением.</span><span class="sxs-lookup"><span data-stu-id="5da1c-181">Suppose you want tooupdate your OS image while keeping hello virtual machine scale set running.</span></span> <span data-ttu-id="5da1c-182">PowerShell и hello Azure CLI можно обновить образы виртуальных машин hello, одной виртуальной машине одновременно.</span><span class="sxs-lookup"><span data-stu-id="5da1c-182">PowerShell and hello Azure CLI can update hello virtual machine images, one virtual machine at a time.</span></span> <span data-ttu-id="5da1c-183">Hello [обновление набора масштабирования виртуальных машин](./virtual-machine-scale-sets-upgrade-scale-set.md) статье также приводятся дополнительные сведения на какие параметры будут доступны tooperform обновления операционной системы в наборе масштабирования виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="5da1c-183">hello [Upgrade a Virtual Machine Scale Set](./virtual-machine-scale-sets-upgrade-scale-set.md) article also provides further information on what options are available tooperform an operating system upgrade across a virtual machine scale set.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5da1c-184">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="5da1c-184">Next steps</span></span>

* [<span data-ttu-id="5da1c-185">Используйте PowerShell toomanage набора параметров масштабирования.</span><span class="sxs-lookup"><span data-stu-id="5da1c-185">Use PowerShell toomanage your scale set.</span></span>](virtual-machine-scale-sets-windows-manage.md)
* [<span data-ttu-id="5da1c-186">Создание шаблона масштабируемого набора</span><span class="sxs-lookup"><span data-stu-id="5da1c-186">Create a scale set template.</span></span>](virtual-machine-scale-sets-mvss-start.md)


[linux-vm-create]: ../virtual-machines/linux/tutorial-manage-vm.md
[windows-vm-create]: ../virtual-machines/windows/tutorial-manage-vm.md
[linux-vm-capture]: ../virtual-machines/linux/capture-image.md
[windows-vm-capture]: ../virtual-machines/windows/capture-image.md 
[vmss-create]: virtual-machine-scale-sets-create.md

