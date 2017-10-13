---
title: "Добавление образа виртуальной Машины по умолчанию в стек Azure Marketplace | Документы Microsoft"
description: "Добавьте образ виртуальной Машины Windows Server 2016 по умолчанию в стек Azure Marketplace."
services: azure-stack
documentationcenter: 
author: SnehaGunda
manager: byronr
editor: 
ms.assetid: 
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/10/2017
ms.author: sngun
ms.openlocfilehash: 43781cb025865df1d228376f57412f3d482d3ad0
ms.sourcegitcommit: 90e2cced6a773b1b52f999ba73cd8877305d270b
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/13/2017
---
# <a name="add-the-windows-server-2016-vm-image-to-the-azure-stack-marketplace"></a><span data-ttu-id="8a1cd-103">Добавить образ виртуальной Машины Windows Server 2016 в стек Azure Marketplace</span><span class="sxs-lookup"><span data-stu-id="8a1cd-103">Add the Windows Server 2016 VM image to the Azure Stack marketplace</span></span>

<span data-ttu-id="8a1cd-104">По умолчанию отсутствуют все образы виртуальных машин в стек Azure marketplace.</span><span class="sxs-lookup"><span data-stu-id="8a1cd-104">By default, there aren’t any virtual machine images available in the Azure Stack marketplace.</span></span> <span data-ttu-id="8a1cd-105">Оператор стек Azure необходимо добавить изображение в Marketplace, чтобы пользователи могли использовать их.</span><span class="sxs-lookup"><span data-stu-id="8a1cd-105">The Azure Stack operator must add an image to the marketplace before users can use them.</span></span> <span data-ttu-id="8a1cd-106">Образ Windows Server 2016 в стек Azure Marketplace можно добавить с помощью одного из следующих двух способов:</span><span class="sxs-lookup"><span data-stu-id="8a1cd-106">You can add the Windows Server 2016 image to the Azure Stack marketplace by using one of the following two methods:</span></span>

* <span data-ttu-id="8a1cd-107">[Добавить изображение, загрузив его из Azure Marketplace](#add-the-image-by-downloading-it-from-the-Azure-marketplace) -используйте этот параметр, если вы работаете в сценарии подключенных и если вы зарегистрировали экземпляра Azure стека с помощью Azure.</span><span class="sxs-lookup"><span data-stu-id="8a1cd-107">[Add the image by downloading it from the Azure Marketplace](#add-the-image-by-downloading-it-from-the-Azure-marketplace) - Use this option if you are operating in a connected scenario and if you have registered your Azure Stack instance with Azure.</span></span>

* <span data-ttu-id="8a1cd-108">[Добавление изображения с помощью PowerShell](#add-the-image-by-using-powershell) -используйте этот параметр, если вы развернули стек Azure в сценарии отсоединения, или в сценариях с ограниченной подключением.</span><span class="sxs-lookup"><span data-stu-id="8a1cd-108">[Add the image by using PowerShell](#add-the-image-by-using-powershell) - Use this option if you have deployed Azure Stack in a disconnected scenario or in scenarios with limited connectivity.</span></span>

## <a name="add-the-image-by-downloading-it-from-the-azure-marketplace"></a><span data-ttu-id="8a1cd-109">Добавить изображение, загрузив его из Azure Marketplace</span><span class="sxs-lookup"><span data-stu-id="8a1cd-109">Add the image by downloading it from the Azure Marketplace</span></span>

1. <span data-ttu-id="8a1cd-110">После развертывания Azure стека, войдите в ваш пакет средств разработки Azure стека.</span><span class="sxs-lookup"><span data-stu-id="8a1cd-110">After deploying Azure Stack, sign in to your Azure Stack Development Kit.</span></span>

2. <span data-ttu-id="8a1cd-111">Нажмите кнопку **дополнительные службы** > **управления Marketplace** > **добавить из Azure**</span><span class="sxs-lookup"><span data-stu-id="8a1cd-111">click **More services** > **Marketplace Management** > **Add from Azure**</span></span> 

3. <span data-ttu-id="8a1cd-112">Поиск **Windows Server 2016 центра обработки данных — Eval** изображение > щелкните **загрузки**</span><span class="sxs-lookup"><span data-stu-id="8a1cd-112">Find or search for the **Windows Server 2016 Datacenter – Eval** image > click **Download**</span></span>

   ![Загрузите образ из Azure](media/azure-stack-add-default-image/download-image.png)

<span data-ttu-id="8a1cd-114">После завершения загрузки, изображение будет добавлено к **управления Marketplace** колонки и он также доступен из **виртуальные машины** колонку.</span><span class="sxs-lookup"><span data-stu-id="8a1cd-114">After the download completes, the image is added to the **Marketplace Management** blade and it is also made available from the **Virtual Machines** blade.</span></span>

## <a name="add-the-image-by-using-powershell"></a><span data-ttu-id="8a1cd-115">Добавление изображения с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="8a1cd-115">Add the image by using PowerShell</span></span>

### <a name="prerequisites"></a><span data-ttu-id="8a1cd-116">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="8a1cd-116">Prerequisites</span></span> 

<span data-ttu-id="8a1cd-117">Выполнить следующие предварительные требования, либо из [пакет средств разработки](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-remote-desktop), или из внешнего клиента Windows в случае [подключен через виртуальную частную сеть](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-vpn):</span><span class="sxs-lookup"><span data-stu-id="8a1cd-117">Run the following prerequisites either from the [development kit](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-remote-desktop), or from a Windows-based external client if you are [connected through VPN](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-vpn):</span></span>

* <span data-ttu-id="8a1cd-118">Установка [модули Azure PowerShell Azure стека совместимой](azure-stack-powershell-install.md).</span><span class="sxs-lookup"><span data-stu-id="8a1cd-118">Install [Azure Stack-compatible Azure PowerShell modules](azure-stack-powershell-install.md).</span></span>  

* <span data-ttu-id="8a1cd-119">Загрузить [инструменты, необходимые для работы с Azure стека](azure-stack-powershell-download.md).</span><span class="sxs-lookup"><span data-stu-id="8a1cd-119">Download the [tools required to work with Azure Stack](azure-stack-powershell-download.md).</span></span>  

* <span data-ttu-id="8a1cd-120">Перейдите к https://www.microsoft.com/en-us/evalcenter/evaluate-windows-server-2016 и загрузить ознакомительную версию Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="8a1cd-120">Go to https://www.microsoft.com/en-us/evalcenter/evaluate-windows-server-2016 and download the Windows Server 2016 evaluation.</span></span> <span data-ttu-id="8a1cd-121">При появлении запроса выберите **ISO** версию для загрузки.</span><span class="sxs-lookup"><span data-stu-id="8a1cd-121">When prompted, select the **ISO** version of the download.</span></span> <span data-ttu-id="8a1cd-122">Запишите путь к расположению загрузки, который используется далее в этом пошаговом руководстве.</span><span class="sxs-lookup"><span data-stu-id="8a1cd-122">Record the path to the download location, which is used later in these steps.</span></span> <span data-ttu-id="8a1cd-123">Необходимо подключение к Интернету.</span><span class="sxs-lookup"><span data-stu-id="8a1cd-123">This step requires internet connectivity.</span></span>  

<span data-ttu-id="8a1cd-124">Теперь выполните следующие действия, чтобы добавить изображение в стек Azure marketplace:</span><span class="sxs-lookup"><span data-stu-id="8a1cd-124">Now run the following steps to add the image to the Azure Stack marketplace:</span></span>
   
1. <span data-ttu-id="8a1cd-125">Импортируйте модули Azure Connect стека и ComputeAdmin с помощью следующих команд:</span><span class="sxs-lookup"><span data-stu-id="8a1cd-125">Import the Azure Stack Connect and ComputeAdmin modules by using the following commands:</span></span>

   ```powershell
   Set-ExecutionPolicy RemoteSigned

   # import the Connect and ComputeAdmin modules   
   Import-Module .\Connect\AzureStack.Connect.psm1
   Import-Module .\ComputeAdmin\AzureStack.ComputeAdmin.psm1

   ```

2. <span data-ttu-id="8a1cd-126">Войдите в среду Azure стека.</span><span class="sxs-lookup"><span data-stu-id="8a1cd-126">Sign in to your Azure Stack environment.</span></span> <span data-ttu-id="8a1cd-127">Выполните следующий сценарий, в зависимости от среды стека Azure развертывается с помощью AAD или AD FS (Убедитесь, что для замены AAD tenantName, GraphAudience конечной точки и ArmEndpoint значения в зависимости от конфигурации вашей среды):</span><span class="sxs-lookup"><span data-stu-id="8a1cd-127">Run the following script depending on if your Azure Stack environment is deployed by using AAD or AD FS (Make sure to replace the AAD tenantName, GraphAudience endpoint and ArmEndpoint values as per your environment configuration):</span></span>  

   <span data-ttu-id="8a1cd-128">а.</span><span class="sxs-lookup"><span data-stu-id="8a1cd-128">a.</span></span> <span data-ttu-id="8a1cd-129">**Azure Active Directory**, используйте следующий командлет:</span><span class="sxs-lookup"><span data-stu-id="8a1cd-129">**Azure Active Directory**, use the following cmdlet:</span></span>

   ```PowerShell
   # For Azure Stack development kit, this value is set to https://adminmanagement.local.azurestack.external. To get this value for Azure Stack integrated systems, contact your service provider.
   $ArmEndpoint = "<Resource Manager endpoint for your environment>"

   # For Azure Stack development kit, this value is set to https://graph.windows.net/. To get this value for Azure Stack integrated systems, contact your service provider.
   $GraphAudience = "<GraphAuidence endpoint for your environment>"
   
   # Create the Azure Stack operator's AzureRM environment by using the following cmdlet:
   Add-AzureRMEnvironment `
     -Name "AzureStackAdmin" `
     -ArmEndpoint $ArmEndpoint

   Set-AzureRmEnvironment `
    -Name "AzureStackAdmin" `
    -GraphAudience $GraphAudience

   $TenantID = Get-AzsDirectoryTenantId `
     -AADTenantName "<myDirectoryTenantName>.onmicrosoft.com" `
     -EnvironmentName AzureStackAdmin

   Login-AzureRmAccount `
     -EnvironmentName "AzureStackAdmin" `
     -TenantId $TenantID 
   ```

   <span data-ttu-id="8a1cd-130">b.</span><span class="sxs-lookup"><span data-stu-id="8a1cd-130">b.</span></span> <span data-ttu-id="8a1cd-131">**Службы федерации Active Directory**, используйте следующий командлет:</span><span class="sxs-lookup"><span data-stu-id="8a1cd-131">**Active Directory Federation Services**, use the following cmdlet:</span></span>
    
   ```PowerShell
   # For Azure Stack development kit, this value is set to https://adminmanagement.local.azurestack.external. To get this value for Azure Stack integrated systems, contact your service provider.
   $ArmEndpoint = "<Resource Manager endpoint for your environment>"

   # For Azure Stack development kit, this value is set to https://graph.local.azurestack.external/. To get this value for Azure Stack integrated systems, contact your service provider.
   $GraphAudience = "<GraphAuidence endpoint for your environment>"

   # Create the Azure Stack operator's AzureRM environment by using the following cmdlet:
   Add-AzureRMEnvironment `
     -Name "AzureStackAdmin" `
     -ArmEndpoint $ArmEndpoint

   Set-AzureRmEnvironment `
     -Name "AzureStackAdmin" `
     -GraphAudience $GraphAudience `
     -EnableAdfsAuthentication:$true

   $TenantID = Get-AzsDirectoryTenantId `
     -ADFS 
     -EnvironmentName AzureStackAdmin 

   Login-AzureRmAccount `
     -EnvironmentName "AzureStackAdmin" `
     -TenantId $TenantID 
   ```
   
3. <span data-ttu-id="8a1cd-132">Добавить образ Windows Server 2016 в стек Azure Marketplace (не забудьте заменить *Path_to_ISO* с путем к загруженный ISO WS2016):</span><span class="sxs-lookup"><span data-stu-id="8a1cd-132">Add the Windows Server 2016 image to the Azure Stack marketplace (Make sure to replace the *Path_to_ISO* with the path to the WS2016 ISO you downloaded):</span></span>

   ```PowerShell
   $ISOPath = "<Fully_Qualified_Path_to_ISO>"

   # Add a Windows Server 2016 Evaluation VM Image.
   New-AzsServer2016VMImage `
     -ISOPath $ISOPath

   ```

<span data-ttu-id="8a1cd-133">Чтобы убедиться, что образ виртуальной Машины Windows Server 2016 имеет последний накопительный пакет обновления, включите `IncludeLatestCU` во время выполнения `New-AzsServer2016VMImage` командлета.</span><span class="sxs-lookup"><span data-stu-id="8a1cd-133">To ensure that the Windows Server 2016 VM image has the latest cumulative update, include the `IncludeLatestCU` parameter when running the `New-AzsServer2016VMImage` cmdlet.</span></span> <span data-ttu-id="8a1cd-134">В разделе [параметры](#parameters) сведения о допустимых параметрах `New-AzsServer2016VMImage` командлета.</span><span class="sxs-lookup"><span data-stu-id="8a1cd-134">See the [Parameters](#parameters) section for information about allowed parameters for the `New-AzsServer2016VMImage` cmdlet.</span></span> <span data-ttu-id="8a1cd-135">Опубликовать изображения в магазине Azure стека занимает около часа.</span><span class="sxs-lookup"><span data-stu-id="8a1cd-135">It takes about an hour to publish the image to the Azure Stack marketplace.</span></span> 

## <a name="parameters"></a><span data-ttu-id="8a1cd-136">Параметры</span><span class="sxs-lookup"><span data-stu-id="8a1cd-136">Parameters</span></span>

|<span data-ttu-id="8a1cd-137">Параметры нового AzsServer2016VMImage</span><span class="sxs-lookup"><span data-stu-id="8a1cd-137">New-AzsServer2016VMImage parameters</span></span>|<span data-ttu-id="8a1cd-138">Обязательный?</span><span class="sxs-lookup"><span data-stu-id="8a1cd-138">Required?</span></span>|<span data-ttu-id="8a1cd-139">Описание</span><span class="sxs-lookup"><span data-stu-id="8a1cd-139">Description</span></span>|
|-----|-----|------|
|<span data-ttu-id="8a1cd-140">ISOPath</span><span class="sxs-lookup"><span data-stu-id="8a1cd-140">ISOPath</span></span>|<span data-ttu-id="8a1cd-141">Да</span><span class="sxs-lookup"><span data-stu-id="8a1cd-141">Yes</span></span>|<span data-ttu-id="8a1cd-142">Полный путь к загруженный ISO Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="8a1cd-142">The fully qualified path to the downloaded Windows Server 2016 ISO.</span></span>|
|<span data-ttu-id="8a1cd-143">net35</span><span class="sxs-lookup"><span data-stu-id="8a1cd-143">Net35</span></span>|<span data-ttu-id="8a1cd-144">Нет</span><span class="sxs-lookup"><span data-stu-id="8a1cd-144">No</span></span>|<span data-ttu-id="8a1cd-145">Этот параметр позволяет установить среду выполнения .NET 3.5 в образе Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="8a1cd-145">This parameter allows you to install the .NET 3.5 runtime on the Windows Server 2016 image.</span></span> <span data-ttu-id="8a1cd-146">По умолчанию это значение равным true.</span><span class="sxs-lookup"><span data-stu-id="8a1cd-146">By default, this value is set to true.</span></span>|
|<span data-ttu-id="8a1cd-147">Version (версия)</span><span class="sxs-lookup"><span data-stu-id="8a1cd-147">Version</span></span>|<span data-ttu-id="8a1cd-148">Нет</span><span class="sxs-lookup"><span data-stu-id="8a1cd-148">No</span></span>|<span data-ttu-id="8a1cd-149">Этот параметр позволяет выбрать, следует ли добавить **Core** или **полного** или **оба** образы Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="8a1cd-149">This parameter allows you to choose whether to add a **Core** or **Full** or **Both** Windows Server 2016 images.</span></span> <span data-ttu-id="8a1cd-150">По умолчанию это значение равно «Full».</span><span class="sxs-lookup"><span data-stu-id="8a1cd-150">By default, this value is set to "Full."</span></span>|
|<span data-ttu-id="8a1cd-151">VHDSizeInMB</span><span class="sxs-lookup"><span data-stu-id="8a1cd-151">VHDSizeInMB</span></span>|<span data-ttu-id="8a1cd-152">Нет</span><span class="sxs-lookup"><span data-stu-id="8a1cd-152">No</span></span>|<span data-ttu-id="8a1cd-153">Задает размер образа виртуального жесткого диска для добавления в среду Azure стека (в МБ).</span><span class="sxs-lookup"><span data-stu-id="8a1cd-153">Sets the size (in MB) of the VHD image to be added to your Azure Stack environment.</span></span> <span data-ttu-id="8a1cd-154">По умолчанию это значение будет присвоено 40960 МБ.</span><span class="sxs-lookup"><span data-stu-id="8a1cd-154">By default, this value is set to 40960 MB.</span></span>|
|<span data-ttu-id="8a1cd-155">CreateGalleryItem</span><span class="sxs-lookup"><span data-stu-id="8a1cd-155">CreateGalleryItem</span></span>|<span data-ttu-id="8a1cd-156">Нет</span><span class="sxs-lookup"><span data-stu-id="8a1cd-156">No</span></span>|<span data-ttu-id="8a1cd-157">Указывает, следует ли создать элемент Marketplace для образа Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="8a1cd-157">Specifies if a Marketplace item should be created for the Windows Server 2016 image.</span></span> <span data-ttu-id="8a1cd-158">По умолчанию это значение равным true.</span><span class="sxs-lookup"><span data-stu-id="8a1cd-158">By default, this value is set to true.</span></span>|
|<span data-ttu-id="8a1cd-159">location</span><span class="sxs-lookup"><span data-stu-id="8a1cd-159">location</span></span> |<span data-ttu-id="8a1cd-160">Нет</span><span class="sxs-lookup"><span data-stu-id="8a1cd-160">No</span></span> |<span data-ttu-id="8a1cd-161">Указывает расположение, к которому должны публиковаться образа Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="8a1cd-161">Specifies the location to which the Windows Server 2016 image should be published.</span></span>|
|<span data-ttu-id="8a1cd-162">IncludeLatestCU</span><span class="sxs-lookup"><span data-stu-id="8a1cd-162">IncludeLatestCU</span></span>|<span data-ttu-id="8a1cd-163">Нет</span><span class="sxs-lookup"><span data-stu-id="8a1cd-163">No</span></span>|<span data-ttu-id="8a1cd-164">Установите этот переключатель, чтобы применить последнее накопительное обновление Windows Server 2016 для нового виртуального жесткого диска.</span><span class="sxs-lookup"><span data-stu-id="8a1cd-164">Set this switch to apply the latest Windows Server 2016 cumulative update to the new VHD.</span></span>|
|<span data-ttu-id="8a1cd-165">CUUri</span><span class="sxs-lookup"><span data-stu-id="8a1cd-165">CUUri</span></span> |<span data-ttu-id="8a1cd-166">Нет</span><span class="sxs-lookup"><span data-stu-id="8a1cd-166">No</span></span> |<span data-ttu-id="8a1cd-167">Это значение используется для выбора накопительное обновление Windows Server 2016 из указанного URI.</span><span class="sxs-lookup"><span data-stu-id="8a1cd-167">Set this value to choose the Windows Server 2016 cumulative update from a specific URI.</span></span> |
|<span data-ttu-id="8a1cd-168">CUPath</span><span class="sxs-lookup"><span data-stu-id="8a1cd-168">CUPath</span></span> |<span data-ttu-id="8a1cd-169">Нет</span><span class="sxs-lookup"><span data-stu-id="8a1cd-169">No</span></span> |<span data-ttu-id="8a1cd-170">Это значение используется для выбора накопительное обновление Windows Server 2016 из локального пути.</span><span class="sxs-lookup"><span data-stu-id="8a1cd-170">Set this value to choose the Windows Server 2016 cumulative update from a local path.</span></span> <span data-ttu-id="8a1cd-171">Этот параметр полезен, если вы развернули экземпляра Azure стека в отключенной среде.</span><span class="sxs-lookup"><span data-stu-id="8a1cd-171">This option is helpful if you have deployed the Azure Stack instance in a disconnected environment.</span></span>|

## <a name="next-steps"></a><span data-ttu-id="8a1cd-172">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="8a1cd-172">Next steps</span></span>

[<span data-ttu-id="8a1cd-173">Подготовка виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="8a1cd-173">Provision a virtual machine</span></span>](azure-stack-provision-vm.md)
