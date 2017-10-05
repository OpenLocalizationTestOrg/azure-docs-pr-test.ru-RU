---
title: "Добавление образа виртуальной Машины Azure стек | Документы Microsoft"
description: "Добавить организации Windows или Linux VM образ для клиентов на использование"
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
ms.openlocfilehash: 793f6c0f1ad92cec4cbb56662685ca151f90b48c
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="make-a-custom-virtual-machine-image-available-in-azure-stack"></a><span data-ttu-id="adaaf-103">Выбрать изображение настраиваемой виртуальной машины, доступные в стек Azure</span><span class="sxs-lookup"><span data-stu-id="adaaf-103">Make a custom virtual machine image available in Azure Stack</span></span>

<span data-ttu-id="adaaf-104">Стек Azure позволяет администраторам облака образы настраиваемой виртуальной машины сделать доступными для пользователей.</span><span class="sxs-lookup"><span data-stu-id="adaaf-104">Azure Stack enables cloud administrators to make custom virtual machine images available to their users.</span></span> <span data-ttu-id="adaaf-105">Эти образы можно ссылаться на шаблоны Azure Resource Manager или добавлен к пользовательскому Интерфейсу Azure Marketplace с созданием элементов Marketplace.</span><span class="sxs-lookup"><span data-stu-id="adaaf-105">These images can be referenced by Azure Resource Manager templates or added to the Azure Marketplace UI with the creation of a Marketplace item.</span></span> 

## <a name="add-a-vm-image-to-marketplace-with-powershell"></a><span data-ttu-id="adaaf-106">Добавление образа виртуальной Машины для магазина с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="adaaf-106">Add a VM image to marketplace with PowerShell</span></span>

<span data-ttu-id="adaaf-107">Выполнить следующие предварительные требования, либо из [пакет средств разработки](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-remote-desktop), или из внешнего клиента Windows в случае [подключен через виртуальную частную сеть](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-vpn)</span><span class="sxs-lookup"><span data-stu-id="adaaf-107">Run the following prerequisites either from the [development kit](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-remote-desktop), or from a Windows-based external client if you are [connected through VPN](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-vpn)</span></span>

* <span data-ttu-id="adaaf-108">[Установите PowerShell для Azure стека](azure-stack-powershell-install.md).</span><span class="sxs-lookup"><span data-stu-id="adaaf-108">[Install PowerShell for Azure Stack](azure-stack-powershell-install.md).</span></span>  

* <span data-ttu-id="adaaf-109">Загрузить [инструменты, необходимые для работы с Azure стека](azure-stack-powershell-download.md).</span><span class="sxs-lookup"><span data-stu-id="adaaf-109">Download the [tools required to work with Azure Stack](azure-stack-powershell-download.md).</span></span>  

* <span data-ttu-id="adaaf-110">Подготовка образа виртуального жесткого диска операционной системы Windows или Linux в формате VHD (не VHDX).</span><span class="sxs-lookup"><span data-stu-id="adaaf-110">Prepare a Windows or Linux operating system virtual hard disk image in VHD format (not VHDX).</span></span>
   
   * <span data-ttu-id="adaaf-111">Для образов Windows, статьи [загрузить образ виртуальной Машины Windows Azure для развертывания диспетчера ресурсов](../virtual-machines/windows/upload-generalized-managed.md) содержит инструкции по подготовке образа в **Подготовка виртуального жесткого диска для передачи** раздела.</span><span class="sxs-lookup"><span data-stu-id="adaaf-111">For Windows images, the article [Upload a Windows VM image to Azure for Resource Manager deployments](../virtual-machines/windows/upload-generalized-managed.md) contains image preparation instructions in the **Prepare the VHD for upload** section.</span></span>
   * <span data-ttu-id="adaaf-112">Для образов Linux, выполните шаги, чтобы подготовить образ или использовать существующий образ Azure Linux стека, как описано в статье [виртуальные машины Linux развертывания в Azure стека](azure-stack-linux.md).</span><span class="sxs-lookup"><span data-stu-id="adaaf-112">For Linux images, follow the steps to prepare the image or use an existing Azure Stack Linux image as described in the article [Deploy Linux virtual machines on Azure Stack](azure-stack-linux.md).</span></span>  

<span data-ttu-id="adaaf-113">Теперь выполните следующие действия, чтобы добавить изображение в стек Azure marketplace:</span><span class="sxs-lookup"><span data-stu-id="adaaf-113">Now run the following steps to add the image to the Azure Stack marketplace:</span></span>

1. <span data-ttu-id="adaaf-114">Импортируйте модули Connect и ComputeAdmin:</span><span class="sxs-lookup"><span data-stu-id="adaaf-114">Import the Connect and ComputeAdmin modules:</span></span>
   
   ```powershell
   Set-ExecutionPolicy RemoteSigned

   # import the Connect and ComputeAdmin modules
   Import-Module .\Connect\AzureStack.Connect.psm1
   Import-Module .\ComputeAdmin\AzureStack.ComputeAdmin.psm1
   ``` 

2. <span data-ttu-id="adaaf-115">Войдите в среду Azure стека.</span><span class="sxs-lookup"><span data-stu-id="adaaf-115">Sign in to your Azure Stack environment.</span></span> <span data-ttu-id="adaaf-116">Выполните следующий сценарий, в зависимости от среды стека Azure развертывается с помощью AAD или AD FS (Убедитесь, что для замены имени клиента AAD):</span><span class="sxs-lookup"><span data-stu-id="adaaf-116">Run the following script depending on if your Azure Stack environment is deployed by using AAD or AD FS (Make sure to replace the AAD tenant name):</span></span> 

   <span data-ttu-id="adaaf-117">а.</span><span class="sxs-lookup"><span data-stu-id="adaaf-117">a.</span></span> <span data-ttu-id="adaaf-118">**Azure Active Directory**, используйте следующий командлет:</span><span class="sxs-lookup"><span data-stu-id="adaaf-118">**Azure Active Directory**, use the following cmdlet:</span></span>

   ```PowerShell
   # Create the Azure Stack cloud administrator's AzureRM environment by using the following cmdlet:
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

   <span data-ttu-id="adaaf-119">b.</span><span class="sxs-lookup"><span data-stu-id="adaaf-119">b.</span></span> <span data-ttu-id="adaaf-120">**Службы федерации Active Directory**, используйте следующий командлет:</span><span class="sxs-lookup"><span data-stu-id="adaaf-120">**Active Directory Federation Services**, use the following cmdlet:</span></span>
    
   ```PowerShell
   # Create the Azure Stack cloud administrator's AzureRM environment by using the following cmdlet:
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
    
3. <span data-ttu-id="adaaf-121">Добавить образ виртуальной Машины путем вызова `Add-AzsVMImage` командлета.</span><span class="sxs-lookup"><span data-stu-id="adaaf-121">Add the VM image by invoking the `Add-AzsVMImage` cmdlet.</span></span> <span data-ttu-id="adaaf-122">В командлет Add-AzsVMImage укажите osType как Windows или Linux.</span><span class="sxs-lookup"><span data-stu-id="adaaf-122">In the Add-AzsVMImage cmdlet, specify the osType as Windows or Linux.</span></span> <span data-ttu-id="adaaf-123">Включают издатель, предложение, SKU и версия для образа виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="adaaf-123">Include the publisher, offer, SKU, and version for the VM image.</span></span> <span data-ttu-id="adaaf-124">В разделе [параметры](#parameters) сведения о допустимых параметров.</span><span class="sxs-lookup"><span data-stu-id="adaaf-124">See the [Parameters](#parameters) section for information about the allowed parameters.</span></span> <span data-ttu-id="adaaf-125">Эти параметры используются шаблоны Azure Resource Manager для ссылки на образ виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="adaaf-125">These parameters are used by Azure Resource Manager templates to reference the VM image.</span></span> <span data-ttu-id="adaaf-126">Ниже приведен пример вызова скрипта.</span><span class="sxs-lookup"><span data-stu-id="adaaf-126">Following is an example invocation of the script:</span></span>
     
     ```powershell
     Add-AzsVMImage `
       -publisher "Canonical" `
       -offer "UbuntuServer" `
       -sku "14.04.3-LTS" `
       -version "1.0.0" `
       -osType Linux `
       -osDiskLocalPath 'C:\Users\AzureStackAdmin\Desktop\UbuntuServer.vhd' `
     ```

<span data-ttu-id="adaaf-127">Команда выполняет следующие задачи.</span><span class="sxs-lookup"><span data-stu-id="adaaf-127">The command does the following:</span></span>

* <span data-ttu-id="adaaf-128">Выполняет проверку подлинности в среде Azure стека</span><span class="sxs-lookup"><span data-stu-id="adaaf-128">Authenticates to the Azure Stack environment</span></span>
* <span data-ttu-id="adaaf-129">Отправляет локального VHD в учетную запись только что созданный временного хранилища</span><span class="sxs-lookup"><span data-stu-id="adaaf-129">Uploads the local VHD to a newly created temporary storage account</span></span>
* <span data-ttu-id="adaaf-130">Добавляет образ виртуальной Машины в репозиторий образов виртуальных Машин и</span><span class="sxs-lookup"><span data-stu-id="adaaf-130">Adds the VM image to the VM image repository and</span></span>
* <span data-ttu-id="adaaf-131">Создает элемент Marketplace</span><span class="sxs-lookup"><span data-stu-id="adaaf-131">Creates a Marketplace item</span></span>

<span data-ttu-id="adaaf-132">Убедитесь, что команда успешно выполнена, перейдите в Marketplace на портале и убедитесь, что образ виртуальной Машины доступен в **виртуальные машины** категории.</span><span class="sxs-lookup"><span data-stu-id="adaaf-132">To verify that the command ran successfully, go to Marketplace in the portal, and then verify that the VM image is available in the **Virtual Machines** category.</span></span>

![Образ виртуальной Машины успешно добавлено](./media/azure-stack-add-vm-image/image5.PNG) 

## <a name="remove-a-vm-image-with-powershell"></a><span data-ttu-id="adaaf-134">Удаление образа виртуальной Машины с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="adaaf-134">Remove a VM image with PowerShell</span></span>

<span data-ttu-id="adaaf-135">Если вам больше не требуется образ виртуальной машины, который вы отправили ранее, можно удалить его из marketplace, с помощью следующего командлета:</span><span class="sxs-lookup"><span data-stu-id="adaaf-135">When you no longer need the virtual machine image that you have uploaded earlier, you can delete it from the marketplace by using the following cmdlet:</span></span>

```powershell
Remove-AzsVMImage `
  -publisher "Canonical" `
  -offer "UbuntuServer" `
  -sku "14.04.3-LTS" `
  -version "1.0.0" `
```

## <a name="parameters"></a><span data-ttu-id="adaaf-136">Параметры</span><span class="sxs-lookup"><span data-stu-id="adaaf-136">Parameters</span></span>

| <span data-ttu-id="adaaf-137">Параметр</span><span class="sxs-lookup"><span data-stu-id="adaaf-137">Parameter</span></span> | <span data-ttu-id="adaaf-138">Описание</span><span class="sxs-lookup"><span data-stu-id="adaaf-138">Description</span></span> |
| --- | --- |
| <span data-ttu-id="adaaf-139">**Издатель**</span><span class="sxs-lookup"><span data-stu-id="adaaf-139">**publisher**</span></span> |<span data-ttu-id="adaaf-140">Сегмент имени издателя образа виртуальной Машины, которую пользователи применять при развертывании образа.</span><span class="sxs-lookup"><span data-stu-id="adaaf-140">The publisher name segment of the VM image that users use when deploying the image.</span></span> <span data-ttu-id="adaaf-141">Например, «Microsoft».</span><span class="sxs-lookup"><span data-stu-id="adaaf-141">An example is ‘Microsoft’.</span></span> <span data-ttu-id="adaaf-142">Не включайте пробел или другие специальные символы в этом поле.</span><span class="sxs-lookup"><span data-stu-id="adaaf-142">Do not include a space or other special characters in this field.</span></span> |
| <span data-ttu-id="adaaf-143">**предложение**</span><span class="sxs-lookup"><span data-stu-id="adaaf-143">**offer**</span></span> |<span data-ttu-id="adaaf-144">Сегмент предложение имя образа виртуальной Машины, которую пользователи применять при развертывании образа виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="adaaf-144">The offer name segment of the VM Image that users use when deploying the VM image.</span></span> <span data-ttu-id="adaaf-145">Пример: 'WindowsServer».</span><span class="sxs-lookup"><span data-stu-id="adaaf-145">An example is ‘WindowsServer’.</span></span> <span data-ttu-id="adaaf-146">Не включайте пробел или другие специальные символы в этом поле.</span><span class="sxs-lookup"><span data-stu-id="adaaf-146">Do not include a space or other special characters in this field.</span></span> |
| <span data-ttu-id="adaaf-147">**sku**</span><span class="sxs-lookup"><span data-stu-id="adaaf-147">**sku**</span></span> |<span data-ttu-id="adaaf-148">Сегмент имя SKU образа виртуальной Машины, которую пользователи применять при развертывании образа виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="adaaf-148">The SKU name segment of the VM Image that users use when deploying the VM image.</span></span> <span data-ttu-id="adaaf-149">Например, «Datacenter2016».</span><span class="sxs-lookup"><span data-stu-id="adaaf-149">An example is ‘Datacenter2016’.</span></span> <span data-ttu-id="adaaf-150">Не включайте пробел или другие специальные символы в этом поле.</span><span class="sxs-lookup"><span data-stu-id="adaaf-150">Do not include a space or other special characters in this field.</span></span> |
| <span data-ttu-id="adaaf-151">**Версия**</span><span class="sxs-lookup"><span data-stu-id="adaaf-151">**version**</span></span> |<span data-ttu-id="adaaf-152">Версия образа виртуальной Машины, которую пользователи применять при развертывании образа виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="adaaf-152">The version of the VM Image that users use when deploying the VM image.</span></span> <span data-ttu-id="adaaf-153">Эта версия имеет формат  *\#.\#. \#*.</span><span class="sxs-lookup"><span data-stu-id="adaaf-153">This version is in the format *\#.\#.\#*.</span></span> <span data-ttu-id="adaaf-154">Например, "1.0.0».</span><span class="sxs-lookup"><span data-stu-id="adaaf-154">An example is ‘1.0.0’.</span></span> <span data-ttu-id="adaaf-155">Не включайте пробел или другие специальные символы в этом поле.</span><span class="sxs-lookup"><span data-stu-id="adaaf-155">Do not include a space or other special characters in this field.</span></span> |
| <span data-ttu-id="adaaf-156">**osType**</span><span class="sxs-lookup"><span data-stu-id="adaaf-156">**osType**</span></span> |<span data-ttu-id="adaaf-157">OsType изображения должен быть «Windows» или «Linux».</span><span class="sxs-lookup"><span data-stu-id="adaaf-157">The osType of the image must be either ‘Windows’ or ‘Linux’.</span></span> |
| <span data-ttu-id="adaaf-158">**osDiskLocalPath**</span><span class="sxs-lookup"><span data-stu-id="adaaf-158">**osDiskLocalPath**</span></span> |<span data-ttu-id="adaaf-159">Локальный путь для виртуального жесткого диска, который загружается как образ виртуальной Машины в Azure стек диск операционной системы.</span><span class="sxs-lookup"><span data-stu-id="adaaf-159">The local path to the OS disk VHD that you are uploading as a VM image to Azure Stack.</span></span> |
| <span data-ttu-id="adaaf-160">**dataDiskLocalPaths**</span><span class="sxs-lookup"><span data-stu-id="adaaf-160">**dataDiskLocalPaths**</span></span> |<span data-ttu-id="adaaf-161">Необязательный массив локальных путей для дисков данных, которые могут быть загружены как часть образа виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="adaaf-161">An optional array of the local paths for data disks that can be uploaded as part of the VM image.</span></span> |
| <span data-ttu-id="adaaf-162">**CreateGalleryItem**</span><span class="sxs-lookup"><span data-stu-id="adaaf-162">**CreateGalleryItem**</span></span> |<span data-ttu-id="adaaf-163">Логический флаг, который определяет, следует ли создать элемент в Marketplace.</span><span class="sxs-lookup"><span data-stu-id="adaaf-163">A Boolean flag that determines whether to create an item in Marketplace.</span></span> <span data-ttu-id="adaaf-164">По умолчанию установлено значение true.</span><span class="sxs-lookup"><span data-stu-id="adaaf-164">By default, it is set to true.</span></span> |
| <span data-ttu-id="adaaf-165">**Заголовок**</span><span class="sxs-lookup"><span data-stu-id="adaaf-165">**title**</span></span> |<span data-ttu-id="adaaf-166">Отображаемое имя элемента Marketplace.</span><span class="sxs-lookup"><span data-stu-id="adaaf-166">The display name of Marketplace item.</span></span> <span data-ttu-id="adaaf-167">По умолчанию он имеет значение издателя-предложение-Sku образа виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="adaaf-167">By default, it is set to the Publisher-Offer-Sku of the VM image.</span></span> |
| <span data-ttu-id="adaaf-168">**description**</span><span class="sxs-lookup"><span data-stu-id="adaaf-168">**description**</span></span> |<span data-ttu-id="adaaf-169">Описание элемента Marketplace.</span><span class="sxs-lookup"><span data-stu-id="adaaf-169">The description of the Marketplace item.</span></span> |
| <span data-ttu-id="adaaf-170">**расположение**</span><span class="sxs-lookup"><span data-stu-id="adaaf-170">**location**</span></span> |<span data-ttu-id="adaaf-171">Расположение, к которому должны публиковаться образа виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="adaaf-171">The location to which the VM image should be published.</span></span> <span data-ttu-id="adaaf-172">По умолчанию это значение задано для локальных.</span><span class="sxs-lookup"><span data-stu-id="adaaf-172">By default, this value is set to local.</span></span>|
| <span data-ttu-id="adaaf-173">**osDiskBlobURI**</span><span class="sxs-lookup"><span data-stu-id="adaaf-173">**osDiskBlobURI**</span></span> |<span data-ttu-id="adaaf-174">При необходимости этот сценарий также принимает URI хранилища BLOB-объектов для osDisk.</span><span class="sxs-lookup"><span data-stu-id="adaaf-174">Optionally, this script also accepts a Blob storage URI for osDisk.</span></span> |
| <span data-ttu-id="adaaf-175">**dataDiskBlobURIs**</span><span class="sxs-lookup"><span data-stu-id="adaaf-175">**dataDiskBlobURIs**</span></span> |<span data-ttu-id="adaaf-176">При необходимости этот сценарий также принимает массив URI хранилища BLOB-объект для добавления дисков с данными в образе.</span><span class="sxs-lookup"><span data-stu-id="adaaf-176">Optionally, this script also accepts an array of Blob storage URIs for adding data disks to the image.</span></span> |

## <a name="add-a-vm-image-through-the-portal"></a><span data-ttu-id="adaaf-177">Добавление образа виртуальной Машины на портале</span><span class="sxs-lookup"><span data-stu-id="adaaf-177">Add a VM image through the portal</span></span>

> [!NOTE]
> <span data-ttu-id="adaaf-178">Этот метод требует создания элемент Marketplace отдельно.</span><span class="sxs-lookup"><span data-stu-id="adaaf-178">This method requires creating the Marketplace item separately.</span></span>

<span data-ttu-id="adaaf-179">Одно из требований образов заключается в том, что они могут ссылаться URI хранилища BLOB-объектов.</span><span class="sxs-lookup"><span data-stu-id="adaaf-179">One requirement of images is that they can be referenced by a Blob storage URI.</span></span> <span data-ttu-id="adaaf-180">Подготовка образа операционной системы Windows или Linux в формате VHD (не VHDX), а затем отправьте образ в учетную запись хранения в Azure или Azure стека.</span><span class="sxs-lookup"><span data-stu-id="adaaf-180">Prepare a Windows or Linux operating system image in VHD format (not VHDX), and then upload the image to a storage account in Azure or Azure Stack.</span></span> <span data-ttu-id="adaaf-181">Если образ уже отправлено в хранилище больших двоичных объектов в Azure или Azure стека, можно пропустить шаг 1.</span><span class="sxs-lookup"><span data-stu-id="adaaf-181">If your image is already uploaded to the Blob storage in Azure or Azure Stack, you can skip step1.</span></span>

1. <span data-ttu-id="adaaf-182">[Загрузить образ виртуальной Машины Windows Azure для развертывания диспетчера ресурсов](https://azure.microsoft.com/documentation/articles/virtual-machines-windows-upload-image/) или для создания образа Linux, следуйте инструкциям, описанным в [виртуальные машины Linux развертывания в Azure стека](azure-stack-linux.md) статьи.</span><span class="sxs-lookup"><span data-stu-id="adaaf-182">[Upload a Windows VM image to Azure for Resource Manager deployments](https://azure.microsoft.com/documentation/articles/virtual-machines-windows-upload-image/) or for a Linux image, follow the instructions described in the [Deploy Linux virtual machines on Azure Stack](azure-stack-linux.md) article.</span></span> <span data-ttu-id="adaaf-183">Перед отправкой образа необходимо учитывать следующие моменты.</span><span class="sxs-lookup"><span data-stu-id="adaaf-183">You should understand the following considerations before you upload the image:</span></span>

   * <span data-ttu-id="adaaf-184">Это более эффективно будет передать изображение в хранилище больших двоичных объектов Azure стека, чем хранилище больших двоичных объектов Azure, поскольку требуется меньше времени для передачи образа в репозиторий образов Azure стека.</span><span class="sxs-lookup"><span data-stu-id="adaaf-184">It's more efficient to upload an image to Azure Stack Blob storage than to Azure Blob storage because it takes less time to push the image to the Azure Stack image repository.</span></span> 
   
   * <span data-ttu-id="adaaf-185">При передаче [образа виртуальной Машины Windows](https://azure.microsoft.com/documentation/articles/virtual-machines-windows-upload-image/), не забудьте подставить **входа в Azure** пошаговое с [настройки среды PowerShell оператор стек Azure](azure-stack-powershell-configure-admin.md) шаг.</span><span class="sxs-lookup"><span data-stu-id="adaaf-185">When uploading the [Windows VM image](https://azure.microsoft.com/documentation/articles/virtual-machines-windows-upload-image/), make sure to substitute the **Login to Azure** step with the [Configure the Azure Stack operator's PowerShell environment](azure-stack-powershell-configure-admin.md)  step.</span></span>  

   * <span data-ttu-id="adaaf-186">Запишите хранилище больших двоичных объектов URI, где загруженный образ, который находится в следующем формате:  *&lt;storageAccount&gt;/&lt;blobContainer&gt; / &lt;targetVHDName&gt;*.vhd</span><span class="sxs-lookup"><span data-stu-id="adaaf-186">Make a note of the Blob storage URI where you upload the image, which is in the following format: *&lt;storageAccount&gt;/&lt;blobContainer&gt;/&lt;targetVHDName&gt;*.vhd</span></span>

   * <span data-ttu-id="adaaf-187">Чтобы сделать BLOB-объект применимым для анонимного доступа, перейдите в контейнер BLOB-объектов учетной записи хранилища, где ВМ образа виртуального жесткого диска, отправленному в **большого двоичного объекта,** , а затем выберите **политики доступа**.</span><span class="sxs-lookup"><span data-stu-id="adaaf-187">To make the blob anonymously accessible, go to the storage account blob container where the VM image VHD was uploaded to **Blob,** and then select **Access Policy**.</span></span> <span data-ttu-id="adaaf-188">Если требуется, можно создать подпись общего доступа для контейнера и включить его как часть URI большого двоичного объекта.</span><span class="sxs-lookup"><span data-stu-id="adaaf-188">If you want, you can instead generate a shared access signature for the container and include it as part of the blob URI.</span></span>

   ![Перейдите к учетной записи хранилища больших двоичных объектов](./media/azure-stack-add-vm-image/image1.png)

   ![Набор больших двоичных объектов доступ к открытым](./media/azure-stack-add-vm-image/image2.png)

2. <span data-ttu-id="adaaf-191">Войдите в стеке Azure как администратор облака > в меню пункт **дополнительные службы** > **поставщиков ресурсов** > выберите **вычислений**  >  **Образов виртуальных Машин** > **добавить**</span><span class="sxs-lookup"><span data-stu-id="adaaf-191">Sign in to Azure Stack as a cloud administrator > From the menu, click **More services** > **Resource Providers** > select  **Compute** > **VM images** > **Add**</span></span>

3. <span data-ttu-id="adaaf-192">На **добавить образ виртуальной Машины** колонке введите издателя, предложение, SKU и версия образа виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="adaaf-192">On the **Add a VM Image** blade, enter the publisher, offer, SKU, and version of the virtual machine image.</span></span> <span data-ttu-id="adaaf-193">См. Эти сегменты имя образа виртуальной Машины в шаблоны диспетчера ресурсов.</span><span class="sxs-lookup"><span data-stu-id="adaaf-193">These name segments refer to the VM image in Resource Manager templates.</span></span> <span data-ttu-id="adaaf-194">Убедитесь в том выбрать **osType** правильно.</span><span class="sxs-lookup"><span data-stu-id="adaaf-194">Make sure to select the **osType** correctly.</span></span> <span data-ttu-id="adaaf-195">Для **URI большого двоичного объекта диска OD**введите URI BLOB-объекта, где был загружен образ и нажмите кнопку **создать** Чтобы приступить к созданию образа виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="adaaf-195">For **OD Disk Blob URI**, enter the Blob URI where the image was uploaded and click **Create** to begin creating the VM Image.</span></span>
   
   ![Начало для создания образа](./media/azure-stack-add-vm-image/image4.png)

   <span data-ttu-id="adaaf-197">При успешно создан образ, меняется состояние образа виртуальной Машины «Выполнено».</span><span class="sxs-lookup"><span data-stu-id="adaaf-197">When the image is successfully created, the VM image status changes to ‘Succeeded’.</span></span>

4. <span data-ttu-id="adaaf-198">Чтобы сделать более легко доступны для потребления пользователями образ виртуальной машины в пользовательском Интерфейсе, лучше всего [создать элемент Marketplace](azure-stack-create-and-publish-marketplace-item.md).</span><span class="sxs-lookup"><span data-stu-id="adaaf-198">To make the virtual machine image more readily available for user consumption in the UI, it is best to [create a Marketplace item](azure-stack-create-and-publish-marketplace-item.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="adaaf-199">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="adaaf-199">Next steps</span></span>

[<span data-ttu-id="adaaf-200">Подготовка виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="adaaf-200">Provision a virtual machine</span></span>](azure-stack-provision-vm.md)