---
title: "tooAzure стека образа виртуальной Машины aaaAdding | Документы Microsoft"
description: "Добавить вашей организации Windows или Linux VM образ для toouse клиентов"
services: azure-stack
documentationcenter: 
author: SnehaGunda
manager: byronr
editor: 
ms.assetid: e5a4236b-1b32-4ee6-9aaa-fcde297a020f
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/10/2017
ms.author: sngun
ms.openlocfilehash: 26dd6c289664c4d64d5932f4396ae778f3f1e1f1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="make-a-custom-virtual-machine-image-available-in-azure-stack"></a><span data-ttu-id="a491b-103">Выбрать изображение настраиваемой виртуальной машины, доступные в стек Azure</span><span class="sxs-lookup"><span data-stu-id="a491b-103">Make a custom virtual machine image available in Azure Stack</span></span>

<span data-ttu-id="a491b-104">Azure позволяет стека облака Администраторы toomake настраиваемой виртуальной машины изображения tootheir доступных пользователей.</span><span class="sxs-lookup"><span data-stu-id="a491b-104">Azure Stack enables cloud administrators toomake custom virtual machine images available tootheir users.</span></span> <span data-ttu-id="a491b-105">Эти образы могут ссылаться шаблоны Azure Resource Manager или добавлены toothe пользовательского интерфейса Azure Marketplace с hello создания элемента Marketplace.</span><span class="sxs-lookup"><span data-stu-id="a491b-105">These images can be referenced by Azure Resource Manager templates or added toothe Azure Marketplace UI with hello creation of a Marketplace item.</span></span> 

## <a name="add-a-vm-image-toomarketplace-with-powershell"></a><span data-ttu-id="a491b-106">Добавьте toomarketplace образа виртуальной Машины с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="a491b-106">Add a VM image toomarketplace with PowerShell</span></span>

<span data-ttu-id="a491b-107">Запустите hello следующие необходимые компоненты из hello [пакет средств разработки](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-remote-desktop), или из внешнего клиента Windows в случае [подключен через виртуальную частную сеть](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-vpn)</span><span class="sxs-lookup"><span data-stu-id="a491b-107">Run hello following prerequisites either from hello [development kit](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-remote-desktop), or from a Windows-based external client if you are [connected through VPN](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-vpn)</span></span>

* <span data-ttu-id="a491b-108">[Установите PowerShell для Azure стека](azure-stack-powershell-install.md).</span><span class="sxs-lookup"><span data-stu-id="a491b-108">[Install PowerShell for Azure Stack](azure-stack-powershell-install.md).</span></span>  

* <span data-ttu-id="a491b-109">Загрузите hello [toowork необходимые средства с Azure стека](azure-stack-powershell-download.md).</span><span class="sxs-lookup"><span data-stu-id="a491b-109">Download hello [tools required toowork with Azure Stack](azure-stack-powershell-download.md).</span></span>  

* <span data-ttu-id="a491b-110">Подготовка образа виртуального жесткого диска операционной системы Windows или Linux в формате VHD (не VHDX).</span><span class="sxs-lookup"><span data-stu-id="a491b-110">Prepare a Windows or Linux operating system virtual hard disk image in VHD format (not VHDX).</span></span>
   
   * <span data-ttu-id="a491b-111">Для образов Windows hello статьи [отправить tooAzure образ виртуальной Машины Windows для развертывания диспетчера ресурсов](../virtual-machines/windows/upload-generalized-managed.md) содержит инструкции по подготовке образа в hello **hello подготовки виртуального жесткого диска для передачи** раздела.</span><span class="sxs-lookup"><span data-stu-id="a491b-111">For Windows images, hello article [Upload a Windows VM image tooAzure for Resource Manager deployments](../virtual-machines/windows/upload-generalized-managed.md) contains image preparation instructions in hello **Prepare hello VHD for upload** section.</span></span>
   * <span data-ttu-id="a491b-112">Для образов Linux, выполните действия hello для подготовки образа hello или использовать существующий образ Azure Linux стека, как описано в статье hello [виртуальные машины Linux развертывания в Azure стека](azure-stack-linux.md).</span><span class="sxs-lookup"><span data-stu-id="a491b-112">For Linux images, follow hello steps to prepare hello image or use an existing Azure Stack Linux image as described in hello article [Deploy Linux virtual machines on Azure Stack](azure-stack-linux.md).</span></span>  

<span data-ttu-id="a491b-113">Теперь выполните следующие шаги tooadd hello изображения toohello стека Azure marketplace hello.</span><span class="sxs-lookup"><span data-stu-id="a491b-113">Now run hello following steps tooadd hello image toohello Azure Stack marketplace:</span></span>

1. <span data-ttu-id="a491b-114">Импортируйте модули Connect и ComputeAdmin hello:</span><span class="sxs-lookup"><span data-stu-id="a491b-114">Import hello Connect and ComputeAdmin modules:</span></span>
   
   ```powershell
   Set-ExecutionPolicy RemoteSigned

   # import hello Connect and ComputeAdmin modules
   Import-Module .\Connect\AzureStack.Connect.psm1
   Import-Module .\ComputeAdmin\AzureStack.ComputeAdmin.psm1
   ``` 

2. <span data-ttu-id="a491b-115">Войдите в систему tooyour среды Azure стека.</span><span class="sxs-lookup"><span data-stu-id="a491b-115">Sign in tooyour Azure Stack environment.</span></span> <span data-ttu-id="a491b-116">Выполнения hello следующий скрипт в зависимости от того, при развертывании среды стека Azure с помощью AAD или AD FS (Убедитесь, что tooreplace hello AAD имя клиента):</span><span class="sxs-lookup"><span data-stu-id="a491b-116">Run hello following script depending on if your Azure Stack environment is deployed by using AAD or AD FS (Make sure tooreplace hello AAD tenant name):</span></span> 

   <span data-ttu-id="a491b-117">а.</span><span class="sxs-lookup"><span data-stu-id="a491b-117">a.</span></span> <span data-ttu-id="a491b-118">**Azure Active Directory**, используйте следующий командлет hello:</span><span class="sxs-lookup"><span data-stu-id="a491b-118">**Azure Active Directory**, use hello following cmdlet:</span></span>

   ```PowerShell
   # Create hello Azure Stack cloud administrator's AzureRM environment by using hello following cmdlet:
   Add-AzureRMEnvironment `
     -Name "AzureStackAdmin" `
     -ArmEndpoint "https://adminmanagement.local.azurestack.external" 

   Set-AzureRmEnvironment `
    -Name "AzureStackAdmin" `
    -GraphAudience "https://graph.windows.net/"

   $TenantID = Get-AzsDirectoryTenantId `
     -AADTenantName "<myDirectoryTenantName>.onmicrosoft.com" `
     -EnvironmentName AzureStackAdmin

   Login-AzureRmAccount `
     -EnvironmentName "AzureStackAdmin" `
     -TenantId $TenantID 
   ```

   <span data-ttu-id="a491b-119">b.</span><span class="sxs-lookup"><span data-stu-id="a491b-119">b.</span></span> <span data-ttu-id="a491b-120">**Службы федерации Active Directory**, используйте следующий командлет hello:</span><span class="sxs-lookup"><span data-stu-id="a491b-120">**Active Directory Federation Services**, use hello following cmdlet:</span></span>
    
   ```PowerShell
   # Create hello Azure Stack cloud administrator's AzureRM environment by using hello following cmdlet:
   Add-AzureRMEnvironment `
     -Name "AzureStackAdmin" `
     -ArmEndpoint "https://adminmanagement.local.azurestack.external"

   Set-AzureRmEnvironment `
     -Name "AzureStackAdmin" `
     -GraphAudience "https://graph.local.azurestack.external/" `
     -EnableAdfsAuthentication:$true

   $TenantID = Get-AzsDirectoryTenantId `
     -ADFS 
     -EnvironmentName AzureStackAdmin 

   Login-AzureRmAccount `
     -EnvironmentName "AzureStackAdmin" `
     -TenantId $TenantID 
   ```
    
3. <span data-ttu-id="a491b-121">Добавить образ виртуальной Машины hello путем вызова hello `Add-AzsVMImage` командлета.</span><span class="sxs-lookup"><span data-stu-id="a491b-121">Add hello VM image by invoking hello `Add-AzsVMImage` cmdlet.</span></span> <span data-ttu-id="a491b-122">В командлет Add-AzsVMImage hello укажите hello osType как Windows или Linux.</span><span class="sxs-lookup"><span data-stu-id="a491b-122">In hello Add-AzsVMImage cmdlet, specify hello osType as Windows or Linux.</span></span> <span data-ttu-id="a491b-123">Включить hello издателя, предложение, SKU и версия для hello образа виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="a491b-123">Include hello publisher, offer, SKU, and version for hello VM image.</span></span> <span data-ttu-id="a491b-124">В разделе hello [параметры](#parameters) сведения о hello допускается параметров.</span><span class="sxs-lookup"><span data-stu-id="a491b-124">See hello [Parameters](#parameters) section for information about hello allowed parameters.</span></span> <span data-ttu-id="a491b-125">Эти параметры используются образа виртуальной Машины hello tooreference шаблонов диспетчера ресурсов Azure.</span><span class="sxs-lookup"><span data-stu-id="a491b-125">These parameters are used by Azure Resource Manager templates tooreference hello VM image.</span></span> <span data-ttu-id="a491b-126">Ниже приведен пример вызова скрипта hello.</span><span class="sxs-lookup"><span data-stu-id="a491b-126">Following is an example invocation of hello script:</span></span>
     
     ```powershell
     Add-AzsVMImage `
       -publisher "Canonical" `
       -offer "UbuntuServer" `
       -sku "14.04.3-LTS" `
       -version "1.0.0" `
       -osType Linux `
       -osDiskLocalPath 'C:\Users\AzureStackAdmin\Desktop\UbuntuServer.vhd' `
     ```

<span data-ttu-id="a491b-127">Команда Hello hello следующие:</span><span class="sxs-lookup"><span data-stu-id="a491b-127">hello command does hello following:</span></span>

* <span data-ttu-id="a491b-128">Проверяет подлинность среды toohello стек Azure</span><span class="sxs-lookup"><span data-stu-id="a491b-128">Authenticates toohello Azure Stack environment</span></span>
* <span data-ttu-id="a491b-129">Отправляет локального виртуального жесткого диска tooa hello созданная учетная запись временного хранилища</span><span class="sxs-lookup"><span data-stu-id="a491b-129">Uploads hello local VHD tooa newly created temporary storage account</span></span>
* <span data-ttu-id="a491b-130">Добавляет репозитория образов виртуальных Машин toohello образ виртуальной Машины hello и</span><span class="sxs-lookup"><span data-stu-id="a491b-130">Adds hello VM image toohello VM image repository and</span></span>
* <span data-ttu-id="a491b-131">Создает элемент Marketplace</span><span class="sxs-lookup"><span data-stu-id="a491b-131">Creates a Marketplace item</span></span>

<span data-ttu-id="a491b-132">tooverify, команда hello выполнено успешно, перейдите tooMarketplace hello портала, а затем убедитесь этот образ виртуальной Машины hello доступен в hello **виртуальные машины** категории.</span><span class="sxs-lookup"><span data-stu-id="a491b-132">tooverify that hello command ran successfully, go tooMarketplace in hello portal, and then verify that hello VM image is available in hello **Virtual Machines** category.</span></span>

![Образ виртуальной Машины успешно добавлено](./media/azure-stack-add-vm-image/image5.PNG) 

## <a name="remove-a-vm-image-with-powershell"></a><span data-ttu-id="a491b-134">Удаление образа виртуальной Машины с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="a491b-134">Remove a VM image with PowerShell</span></span>

<span data-ttu-id="a491b-135">При hello образ виртуальной машины, который вы отправили ранее больше не нужна, можно удалить из hello marketplace с помощью hello, выполнив командлет:</span><span class="sxs-lookup"><span data-stu-id="a491b-135">When you no longer need hello virtual machine image that you have uploaded earlier, you can delete it from hello marketplace by using hello following cmdlet:</span></span>

```powershell
Remove-AzsVMImage `
  -publisher "Canonical" `
  -offer "UbuntuServer" `
  -sku "14.04.3-LTS" `
  -version "1.0.0" `
```

## <a name="parameters"></a><span data-ttu-id="a491b-136">Параметры</span><span class="sxs-lookup"><span data-stu-id="a491b-136">Parameters</span></span>

| <span data-ttu-id="a491b-137">Параметр</span><span class="sxs-lookup"><span data-stu-id="a491b-137">Parameter</span></span> | <span data-ttu-id="a491b-138">Описание</span><span class="sxs-lookup"><span data-stu-id="a491b-138">Description</span></span> |
| --- | --- |
| <span data-ttu-id="a491b-139">**Издатель**</span><span class="sxs-lookup"><span data-stu-id="a491b-139">**publisher**</span></span> |<span data-ttu-id="a491b-140">Сегмент имени издателя Hello hello образа виртуальной Машины, который пользователи используют при развертывании образа hello.</span><span class="sxs-lookup"><span data-stu-id="a491b-140">hello publisher name segment of hello VM image that users use when deploying hello image.</span></span> <span data-ttu-id="a491b-141">Например, «Microsoft».</span><span class="sxs-lookup"><span data-stu-id="a491b-141">An example is ‘Microsoft’.</span></span> <span data-ttu-id="a491b-142">Не включайте пробел или другие специальные символы в этом поле.</span><span class="sxs-lookup"><span data-stu-id="a491b-142">Do not include a space or other special characters in this field.</span></span> |
| <span data-ttu-id="a491b-143">**предложение**</span><span class="sxs-lookup"><span data-stu-id="a491b-143">**offer**</span></span> |<span data-ttu-id="a491b-144">Hello сегмент имени предложение hello образа виртуальной Машины, которую пользователи применять при развертывании образа виртуальной Машины hello.</span><span class="sxs-lookup"><span data-stu-id="a491b-144">hello offer name segment of hello VM Image that users use when deploying hello VM image.</span></span> <span data-ttu-id="a491b-145">Пример: 'WindowsServer».</span><span class="sxs-lookup"><span data-stu-id="a491b-145">An example is ‘WindowsServer’.</span></span> <span data-ttu-id="a491b-146">Не включайте пробел или другие специальные символы в этом поле.</span><span class="sxs-lookup"><span data-stu-id="a491b-146">Do not include a space or other special characters in this field.</span></span> |
| <span data-ttu-id="a491b-147">**sku**</span><span class="sxs-lookup"><span data-stu-id="a491b-147">**sku**</span></span> |<span data-ttu-id="a491b-148">Hello сегмент имя SKU hello образа виртуальной Машины, которую пользователи применять при развертывании образа виртуальной Машины hello.</span><span class="sxs-lookup"><span data-stu-id="a491b-148">hello SKU name segment of hello VM Image that users use when deploying hello VM image.</span></span> <span data-ttu-id="a491b-149">Например, «Datacenter2016».</span><span class="sxs-lookup"><span data-stu-id="a491b-149">An example is ‘Datacenter2016’.</span></span> <span data-ttu-id="a491b-150">Не включайте пробел или другие специальные символы в этом поле.</span><span class="sxs-lookup"><span data-stu-id="a491b-150">Do not include a space or other special characters in this field.</span></span> |
| <span data-ttu-id="a491b-151">**version**</span><span class="sxs-lookup"><span data-stu-id="a491b-151">**version**</span></span> |<span data-ttu-id="a491b-152">Версия образа виртуальной Машины, которую пользователи применять при развертывании образа виртуальной Машины hello hello Hello.</span><span class="sxs-lookup"><span data-stu-id="a491b-152">hello version of hello VM Image that users use when deploying hello VM image.</span></span> <span data-ttu-id="a491b-153">Эта версия имеет формат hello  *\#.\#. \#*.</span><span class="sxs-lookup"><span data-stu-id="a491b-153">This version is in hello format *\#.\#.\#*.</span></span> <span data-ttu-id="a491b-154">Например, "1.0.0».</span><span class="sxs-lookup"><span data-stu-id="a491b-154">An example is ‘1.0.0’.</span></span> <span data-ttu-id="a491b-155">Не включайте пробел или другие специальные символы в этом поле.</span><span class="sxs-lookup"><span data-stu-id="a491b-155">Do not include a space or other special characters in this field.</span></span> |
| <span data-ttu-id="a491b-156">**osType**</span><span class="sxs-lookup"><span data-stu-id="a491b-156">**osType**</span></span> |<span data-ttu-id="a491b-157">Hello osType hello изображения должен быть «Windows» или «Linux».</span><span class="sxs-lookup"><span data-stu-id="a491b-157">hello osType of hello image must be either ‘Windows’ or ‘Linux’.</span></span> |
| <span data-ttu-id="a491b-158">**osDiskLocalPath**</span><span class="sxs-lookup"><span data-stu-id="a491b-158">**osDiskLocalPath**</span></span> |<span data-ttu-id="a491b-159">диск toohello ОС Hello локальный путь виртуального жесткого диска, который вы отправляете как tooAzure образ виртуальной Машины стека.</span><span class="sxs-lookup"><span data-stu-id="a491b-159">hello local path toohello OS disk VHD that you are uploading as a VM image tooAzure Stack.</span></span> |
| <span data-ttu-id="a491b-160">**dataDiskLocalPaths**</span><span class="sxs-lookup"><span data-stu-id="a491b-160">**dataDiskLocalPaths**</span></span> |<span data-ttu-id="a491b-161">Необязательный массив hello локальных путей для дисков данных, которые могут быть загружены как часть образа виртуальной Машины hello.</span><span class="sxs-lookup"><span data-stu-id="a491b-161">An optional array of hello local paths for data disks that can be uploaded as part of hello VM image.</span></span> |
| <span data-ttu-id="a491b-162">**CreateGalleryItem**</span><span class="sxs-lookup"><span data-stu-id="a491b-162">**CreateGalleryItem**</span></span> |<span data-ttu-id="a491b-163">Логический флаг, который определяет, является ли toocreate элемент в Marketplace.</span><span class="sxs-lookup"><span data-stu-id="a491b-163">A Boolean flag that determines whether toocreate an item in Marketplace.</span></span> <span data-ttu-id="a491b-164">По умолчанию устанавливается tootrue.</span><span class="sxs-lookup"><span data-stu-id="a491b-164">By default, it is set tootrue.</span></span> |
| <span data-ttu-id="a491b-165">**Заголовок**</span><span class="sxs-lookup"><span data-stu-id="a491b-165">**title**</span></span> |<span data-ttu-id="a491b-166">Hello отображаемое имя элемента Marketplace.</span><span class="sxs-lookup"><span data-stu-id="a491b-166">hello display name of Marketplace item.</span></span> <span data-ttu-id="a491b-167">По умолчанию он имеет значение toohello издателя предложение номера Sku образа ВМ hello.</span><span class="sxs-lookup"><span data-stu-id="a491b-167">By default, it is set toohello Publisher-Offer-Sku of hello VM image.</span></span> |
| <span data-ttu-id="a491b-168">**description**</span><span class="sxs-lookup"><span data-stu-id="a491b-168">**description**</span></span> |<span data-ttu-id="a491b-169">Описание Hello элемента Marketplace hello.</span><span class="sxs-lookup"><span data-stu-id="a491b-169">hello description of hello Marketplace item.</span></span> |
| <span data-ttu-id="a491b-170">**расположение**</span><span class="sxs-lookup"><span data-stu-id="a491b-170">**location**</span></span> |<span data-ttu-id="a491b-171">необходимо опубликовать Hello расположение toowhich hello образ операционной системы.</span><span class="sxs-lookup"><span data-stu-id="a491b-171">hello location toowhich hello VM image should be published.</span></span> <span data-ttu-id="a491b-172">По умолчанию это значение имеет значение toolocal.</span><span class="sxs-lookup"><span data-stu-id="a491b-172">By default, this value is set toolocal.</span></span>|
| <span data-ttu-id="a491b-173">**osDiskBlobURI**</span><span class="sxs-lookup"><span data-stu-id="a491b-173">**osDiskBlobURI**</span></span> |<span data-ttu-id="a491b-174">При необходимости этот сценарий также принимает URI хранилища BLOB-объектов для osDisk.</span><span class="sxs-lookup"><span data-stu-id="a491b-174">Optionally, this script also accepts a Blob storage URI for osDisk.</span></span> |
| <span data-ttu-id="a491b-175">**dataDiskBlobURIs**</span><span class="sxs-lookup"><span data-stu-id="a491b-175">**dataDiskBlobURIs**</span></span> |<span data-ttu-id="a491b-176">При необходимости этот сценарий также принимает массив URI хранилища BLOB-объект для добавления образа toohello дисков данных.</span><span class="sxs-lookup"><span data-stu-id="a491b-176">Optionally, this script also accepts an array of Blob storage URIs for adding data disks toohello image.</span></span> |

## <a name="add-a-vm-image-through-hello-portal"></a><span data-ttu-id="a491b-177">Добавление образа виртуальной Машины через портал hello</span><span class="sxs-lookup"><span data-stu-id="a491b-177">Add a VM image through hello portal</span></span>

> [!NOTE]
> <span data-ttu-id="a491b-178">Этот метод требует создания элементов Marketplace hello отдельно.</span><span class="sxs-lookup"><span data-stu-id="a491b-178">This method requires creating hello Marketplace item separately.</span></span>

<span data-ttu-id="a491b-179">Одно из требований образов заключается в том, что они могут ссылаться URI хранилища BLOB-объектов.</span><span class="sxs-lookup"><span data-stu-id="a491b-179">One requirement of images is that they can be referenced by a Blob storage URI.</span></span> <span data-ttu-id="a491b-180">Подготовка образа операционной системы Windows или Linux в формате VHD (не VHDX), а затем отправьте hello учетная запись хранилища образов tooa в Azure или Azure стека.</span><span class="sxs-lookup"><span data-stu-id="a491b-180">Prepare a Windows or Linux operating system image in VHD format (not VHDX), and then upload hello image tooa storage account in Azure or Azure Stack.</span></span> <span data-ttu-id="a491b-181">Если образ уже отправленного toohello хранилища больших двоичных объектов в Azure или Azure стека, можно пропустить шаг 1.</span><span class="sxs-lookup"><span data-stu-id="a491b-181">If your image is already uploaded toohello Blob storage in Azure or Azure Stack, you can skip step1.</span></span>

1. <span data-ttu-id="a491b-182">[Отправка tooAzure образ виртуальной Машины Windows для развертывания диспетчера ресурсов](https://azure.microsoft.com/documentation/articles/virtual-machines-windows-upload-image/) или для создания образа Linux, следуйте инструкциям hello, описанным в hello [виртуальные машины Linux развертывания в Azure стека](azure-stack-linux.md) статьи.</span><span class="sxs-lookup"><span data-stu-id="a491b-182">[Upload a Windows VM image tooAzure for Resource Manager deployments](https://azure.microsoft.com/documentation/articles/virtual-machines-windows-upload-image/) or for a Linux image, follow hello instructions described in hello [Deploy Linux virtual machines on Azure Stack](azure-stack-linux.md) article.</span></span> <span data-ttu-id="a491b-183">Необходимо учитывать следующие рекомендации, перед отправкой образа hello hello.</span><span class="sxs-lookup"><span data-stu-id="a491b-183">You should understand hello following considerations before you upload hello image:</span></span>

   * <span data-ttu-id="a491b-184">Это более эффективно tooupload tooAzure образа хранилища больших двоичных объектов стека чем tooAzure хранилища больших двоичных объектов, поскольку занимает меньше времени toopush hello toohello стека Azure образ репозитория образов.</span><span class="sxs-lookup"><span data-stu-id="a491b-184">It's more efficient tooupload an image tooAzure Stack Blob storage than tooAzure Blob storage because it takes less time toopush hello image toohello Azure Stack image repository.</span></span> 
   
   * <span data-ttu-id="a491b-185">При передаче hello [образа виртуальной Машины Windows](https://azure.microsoft.com/documentation/articles/virtual-machines-windows-upload-image/), убедитесь, что hello toosubstitute **tooAzure входа** шаг с hello [настройки среды PowerShell hello Azure стека оператор](azure-stack-powershell-configure-admin.md)шаг.</span><span class="sxs-lookup"><span data-stu-id="a491b-185">When uploading hello [Windows VM image](https://azure.microsoft.com/documentation/articles/virtual-machines-windows-upload-image/), make sure toosubstitute hello **Login tooAzure** step with hello [Configure hello Azure Stack operator's PowerShell environment](azure-stack-powershell-configure-admin.md)  step.</span></span>  

   * <span data-ttu-id="a491b-186">Запишите hello URI, где отправить hello изображение, которое является в кодировке hello хранилища больших двоичных объектов:  *&lt;storageAccount&gt;/&lt;blobContainer&gt; / &lt;targetVHDName&gt;*.vhd</span><span class="sxs-lookup"><span data-stu-id="a491b-186">Make a note of hello Blob storage URI where you upload hello image, which is in hello following format: *&lt;storageAccount&gt;/&lt;blobContainer&gt;/&lt;targetVHDName&gt;*.vhd</span></span>

   * <span data-ttu-id="a491b-187">toomake hello большого двоичного объекта toohello применимым для анонимного доступа, перейдите контейнера учетной записи хранилища BLOB-объекта где hello ВМ образа виртуального жесткого диска, отправленному слишком**большого двоичного объекта,** , а затем выберите **политики доступа**.</span><span class="sxs-lookup"><span data-stu-id="a491b-187">toomake hello blob anonymously accessible, go toohello storage account blob container where hello VM image VHD was uploaded too**Blob,** and then select **Access Policy**.</span></span> <span data-ttu-id="a491b-188">Если требуется, можно создать подпись общего доступа для контейнера hello и включить его как часть hello URI большого двоичного объекта.</span><span class="sxs-lookup"><span data-stu-id="a491b-188">If you want, you can instead generate a shared access signature for hello container and include it as part of hello blob URI.</span></span>

   ![Перейдите в BLOB-объектов учетной записи toostorage](./media/azure-stack-add-vm-image/image1.png)

   ![Toopublic доступа набор больших двоичных объектов](./media/azure-stack-add-vm-image/image2.png)

2. <span data-ttu-id="a491b-191">Вход tooAzure стек как администратор облака > меню "hello" щелкните **дополнительные службы** > **поставщиков ресурсов** > выберите **вычислений**  >  **Образов виртуальных Машин** > **добавить**</span><span class="sxs-lookup"><span data-stu-id="a491b-191">Sign in tooAzure Stack as a cloud administrator > From hello menu, click **More services** > **Resource Providers** > select  **Compute** > **VM images** > **Add**</span></span>

3. <span data-ttu-id="a491b-192">На hello **добавить образ виртуальной Машины** колонке введите hello издателя, предложение, SKU и версия образа виртуальной машины hello.</span><span class="sxs-lookup"><span data-stu-id="a491b-192">On hello **Add a VM Image** blade, enter hello publisher, offer, SKU, and version of hello virtual machine image.</span></span> <span data-ttu-id="a491b-193">Эти сегменты имя ссылаться toohello образа виртуальной Машины в шаблоны диспетчера ресурсов.</span><span class="sxs-lookup"><span data-stu-id="a491b-193">These name segments refer toohello VM image in Resource Manager templates.</span></span> <span data-ttu-id="a491b-194">Убедитесь, что tooselect **osType** правильно.</span><span class="sxs-lookup"><span data-stu-id="a491b-194">Make sure tooselect the **osType** correctly.</span></span> <span data-ttu-id="a491b-195">Для **URI большого двоичного объекта диска OD**введите hello URI BLOB-объекта, где был загружен образ и нажмите кнопку **создать** toobegin Создание образа виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="a491b-195">For **OD Disk Blob URI**, enter hello Blob URI where the image was uploaded and click **Create** toobegin creating the VM Image.</span></span>
   
   ![Начать toocreate hello изображения](./media/azure-stack-add-vm-image/image4.png)

   <span data-ttu-id="a491b-197">Когда hello образ успешно создан, hello состояние образа виртуальной Машины изменяется too'Succeeded ".</span><span class="sxs-lookup"><span data-stu-id="a491b-197">When hello image is successfully created, hello VM image status changes too‘Succeeded’.</span></span>

4. <span data-ttu-id="a491b-198">образ виртуальной машины hello toomake повысить его доступность для их потребления пользователями в hello пользовательского интерфейса, то лучше слишком[создать элемент Marketplace](azure-stack-create-and-publish-marketplace-item.md).</span><span class="sxs-lookup"><span data-stu-id="a491b-198">toomake hello virtual machine image more readily available for user consumption in hello UI, it is best too[create a Marketplace item](azure-stack-create-and-publish-marketplace-item.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="a491b-199">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="a491b-199">Next steps</span></span>

[<span data-ttu-id="a491b-200">Подготовка виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="a491b-200">Provision a virtual machine</span></span>](azure-stack-provision-vm.md)