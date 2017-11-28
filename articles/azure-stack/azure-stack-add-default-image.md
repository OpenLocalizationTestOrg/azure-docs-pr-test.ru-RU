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
ms.openlocfilehash: 2953038d45b1bda4aa281ecad91c887dcde90bd0
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="add-the-windows-server-2016-vm-image-to-the-azure-stack-marketplace"></a><span data-ttu-id="f4924-103">Добавить образ виртуальной Машины Windows Server 2016 в стек Azure Marketplace</span><span class="sxs-lookup"><span data-stu-id="f4924-103">Add the Windows Server 2016 VM image to the Azure Stack marketplace</span></span>

<span data-ttu-id="f4924-104">По умолчанию отсутствуют все образы виртуальных машин в стек Azure marketplace.</span><span class="sxs-lookup"><span data-stu-id="f4924-104">By default, there aren’t any virtual machine images available in the Azure Stack marketplace.</span></span> <span data-ttu-id="f4924-105">Стек Azure администратору облака необходимо добавить образ marketplace, чтобы пользователи могли использовать их.</span><span class="sxs-lookup"><span data-stu-id="f4924-105">The Azure Stack cloud administrator must add an image to the marketplace before users can use them.</span></span> <span data-ttu-id="f4924-106">Образ Windows Server 2016 в стек Azure Marketplace можно добавить с помощью одного из следующих двух способов:</span><span class="sxs-lookup"><span data-stu-id="f4924-106">You can add the Windows Server 2016 image to the Azure Stack marketplace by using one of the following two methods:</span></span>

* <span data-ttu-id="f4924-107">[Добавить изображение, загрузив его из Azure Marketplace](#add-the-image-by-downloading-it-from-the-Azure-marketplace) -используйте этот параметр, если вы работаете в сценарии подключенных и если вы зарегистрировали экземпляра Azure стека с помощью Azure.</span><span class="sxs-lookup"><span data-stu-id="f4924-107">[Add the image by downloading it from the Azure Marketplace](#add-the-image-by-downloading-it-from-the-Azure-marketplace) - Use this option if you are operating in a connected scenario and if you have registered your Azure Stack instance with Azure.</span></span>

* <span data-ttu-id="f4924-108">[Добавление изображения с помощью PowerShell](#add-the-image-by-using-powershell) -используйте этот параметр, если вы развернули стек Azure в сценарии отсоединения, или в сценариях с ограниченной подключением.</span><span class="sxs-lookup"><span data-stu-id="f4924-108">[Add the image by using PowerShell](#add-the-image-by-using-powershell) - Use this option if you have deployed Azure Stack in a disconnected scenario or in scenarios with limited connectivity.</span></span>

## <a name="add-the-image-by-downloading-it-from-the-azure-marketplace"></a><span data-ttu-id="f4924-109">Добавить изображение, загрузив его из Azure Marketplace</span><span class="sxs-lookup"><span data-stu-id="f4924-109">Add the image by downloading it from the Azure Marketplace</span></span>

1. <span data-ttu-id="f4924-110">После развертывания Azure стека, войдите в ваш пакет средств разработки Azure стека.</span><span class="sxs-lookup"><span data-stu-id="f4924-110">After deploying Azure Stack, sign in to your Azure Stack Development Kit.</span></span>

2. <span data-ttu-id="f4924-111">Нажмите кнопку **дополнительные службы** > **управления Marketplace** > **добавить из Azure**</span><span class="sxs-lookup"><span data-stu-id="f4924-111">click **More services** > **Marketplace Management** > **Add from Azure**</span></span> 

3. <span data-ttu-id="f4924-112">Поиск **Windows Server 2016 центра обработки данных — Eval** изображение > щелкните **загрузки**</span><span class="sxs-lookup"><span data-stu-id="f4924-112">Find or search for the **Windows Server 2016 Datacenter – Eval** image > click **Download**</span></span>

   ![Загрузите образ из Azure](media/azure-stack-add-default-image/download-image.png)

<span data-ttu-id="f4924-114">После завершения загрузки, изображение будет добавлено к **управления Marketplace** колонки и он также доступен из **виртуальные машины** колонку.</span><span class="sxs-lookup"><span data-stu-id="f4924-114">After the download completes, the image is added to the **Marketplace Management** blade and it is also made available from the **Virtual Machines** blade.</span></span>

## <a name="add-the-image-by-using-powershell"></a><span data-ttu-id="f4924-115">Добавление изображения с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="f4924-115">Add the image by using PowerShell</span></span>

### <a name="prerequisites"></a><span data-ttu-id="f4924-116">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="f4924-116">Prerequisites</span></span> 

<span data-ttu-id="f4924-117">Выполнить следующие предварительные требования, либо из [пакет средств разработки](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-remote-desktop), или из внешнего клиента Windows в случае [подключен через виртуальную частную сеть](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-vpn):</span><span class="sxs-lookup"><span data-stu-id="f4924-117">Run the following prerequisites either from the [development kit](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-remote-desktop), or from a Windows-based external client if you are [connected through VPN](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-vpn):</span></span>

* <span data-ttu-id="f4924-118">Установка [модули Azure PowerShell Azure стека совместимой](azure-stack-powershell-install.md).</span><span class="sxs-lookup"><span data-stu-id="f4924-118">Install [Azure Stack-compatible Azure PowerShell modules](azure-stack-powershell-install.md).</span></span>  

* <span data-ttu-id="f4924-119">Загрузить [инструменты, необходимые для работы с Azure стека](azure-stack-powershell-download.md).</span><span class="sxs-lookup"><span data-stu-id="f4924-119">Download the [tools required to work with Azure Stack](azure-stack-powershell-download.md).</span></span>  

* <span data-ttu-id="f4924-120">Перейдите к https://www.microsoft.com/en-us/evalcenter/evaluate-windows-server-2016 и загрузить ознакомительную версию Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="f4924-120">Go to https://www.microsoft.com/en-us/evalcenter/evaluate-windows-server-2016 and download the Windows Server 2016 evaluation.</span></span> <span data-ttu-id="f4924-121">При появлении запроса выберите **ISO** версию для загрузки.</span><span class="sxs-lookup"><span data-stu-id="f4924-121">When prompted, select the **ISO** version of the download.</span></span> <span data-ttu-id="f4924-122">Запишите путь к расположению загрузки, который используется далее в этом пошаговом руководстве.</span><span class="sxs-lookup"><span data-stu-id="f4924-122">Record the path to the download location, which is used later in these steps.</span></span> <span data-ttu-id="f4924-123">Необходимо подключение к Интернету.</span><span class="sxs-lookup"><span data-stu-id="f4924-123">This step requires internet connectivity.</span></span>  

<span data-ttu-id="f4924-124">Теперь выполните следующие действия, чтобы добавить изображение в стек Azure marketplace:</span><span class="sxs-lookup"><span data-stu-id="f4924-124">Now run the following steps to add the image to the Azure Stack marketplace:</span></span>
   
1. <span data-ttu-id="f4924-125">Импортируйте модули Azure Connect стека и ComputeAdmin с помощью следующих команд:</span><span class="sxs-lookup"><span data-stu-id="f4924-125">Import the Azure Stack Connect and ComputeAdmin modules by using the following commands:</span></span>

   ```powershell
   Set-ExecutionPolicy RemoteSigned

   # import the Connect and ComputeAdmin modules   
   Import-Module .\Connect\AzureStack.Connect.psm1
   Import-Module .\ComputeAdmin\AzureStack.ComputeAdmin.psm1

   ```

2. <span data-ttu-id="f4924-126">Войдите в среду Azure стека.</span><span class="sxs-lookup"><span data-stu-id="f4924-126">Sign in to your Azure Stack environment.</span></span> <span data-ttu-id="f4924-127">Выполните следующий сценарий, в зависимости от среды стека Azure развертывается с помощью AAD или AD FS (Убедитесь, что для замены имени клиента AAD):</span><span class="sxs-lookup"><span data-stu-id="f4924-127">Run the following script depending on if your Azure Stack environment is deployed by using AAD or AD FS (Make sure to replace the AAD tenant name):</span></span>  

   <span data-ttu-id="f4924-128">а.</span><span class="sxs-lookup"><span data-stu-id="f4924-128">a.</span></span> <span data-ttu-id="f4924-129">**Azure Active Directory**, используйте следующий командлет:</span><span class="sxs-lookup"><span data-stu-id="f4924-129">**Azure Active Directory**, use the following cmdlet:</span></span>

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

   <span data-ttu-id="f4924-130">b.</span><span class="sxs-lookup"><span data-stu-id="f4924-130">b.</span></span> <span data-ttu-id="f4924-131">**Службы федерации Active Directory**, используйте следующий командлет:</span><span class="sxs-lookup"><span data-stu-id="f4924-131">**Active Directory Federation Services**, use the following cmdlet:</span></span>
    
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
   
3. <span data-ttu-id="f4924-132">Добавить образ Windows Server 2016 в стек Azure Marketplace (не забудьте заменить *Path_to_ISO* с путем к загруженный ISO WS2016):</span><span class="sxs-lookup"><span data-stu-id="f4924-132">Add the Windows Server 2016 image to the Azure Stack marketplace (Make sure to replace the *Path_to_ISO* with the path to the WS2016 ISO you downloaded):</span></span>

   ```PowerShell
   $ISOPath = "<Fully_Qualified_Path_to_ISO>"

   # Add a Windows Server 2016 Evaluation VM Image.
   New-AzsServer2016VMImage `
     -ISOPath $ISOPath

   ```

<span data-ttu-id="f4924-133">Чтобы убедиться, что образ виртуальной Машины Windows Server 2016 имеет последний накопительный пакет обновления, включите `IncludeLatestCU` во время выполнения `New-AzsServer2016VMImage` командлета.</span><span class="sxs-lookup"><span data-stu-id="f4924-133">To ensure that the Windows Server 2016 VM image has the latest cumulative update, include the `IncludeLatestCU` parameter when running the `New-AzsServer2016VMImage` cmdlet.</span></span> <span data-ttu-id="f4924-134">В разделе [параметры](#parameters) сведения о допустимых параметрах `New-AzsServer2016VMImage` командлета.</span><span class="sxs-lookup"><span data-stu-id="f4924-134">See the [Parameters](#parameters) section for information about allowed parameters for the `New-AzsServer2016VMImage` cmdlet.</span></span> <span data-ttu-id="f4924-135">Опубликовать изображения в магазине Azure стека занимает около часа.</span><span class="sxs-lookup"><span data-stu-id="f4924-135">It takes about an hour to publish the image to the Azure Stack marketplace.</span></span> 

## <a name="parameters"></a><span data-ttu-id="f4924-136">Параметры</span><span class="sxs-lookup"><span data-stu-id="f4924-136">Parameters</span></span>

|<span data-ttu-id="f4924-137">Параметры нового AzsServer2016VMImage</span><span class="sxs-lookup"><span data-stu-id="f4924-137">New-AzsServer2016VMImage parameters</span></span>|<span data-ttu-id="f4924-138">Обязательный?</span><span class="sxs-lookup"><span data-stu-id="f4924-138">Required?</span></span>|<span data-ttu-id="f4924-139">Описание</span><span class="sxs-lookup"><span data-stu-id="f4924-139">Description</span></span>|
|-----|-----|------|
|<span data-ttu-id="f4924-140">ISOPath</span><span class="sxs-lookup"><span data-stu-id="f4924-140">ISOPath</span></span>|<span data-ttu-id="f4924-141">Да</span><span class="sxs-lookup"><span data-stu-id="f4924-141">Yes</span></span>|<span data-ttu-id="f4924-142">Полный путь к загруженный ISO Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="f4924-142">The fully qualified path to the downloaded Windows Server 2016 ISO.</span></span>|
|<span data-ttu-id="f4924-143">net35</span><span class="sxs-lookup"><span data-stu-id="f4924-143">Net35</span></span>|<span data-ttu-id="f4924-144">Нет</span><span class="sxs-lookup"><span data-stu-id="f4924-144">No</span></span>|<span data-ttu-id="f4924-145">Этот параметр позволяет установить среду выполнения .NET 3.5 в образе Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="f4924-145">This parameter allows you to install the .NET 3.5 runtime on the Windows Server 2016 image.</span></span> <span data-ttu-id="f4924-146">По умолчанию это значение равным true.</span><span class="sxs-lookup"><span data-stu-id="f4924-146">By default, this value is set to true.</span></span> <span data-ttu-id="f4924-147">Является обязательным, что образ содержит среду выполнения .NET 3.5 и установить поставщики ресурсов SQL и MYSQL.</span><span class="sxs-lookup"><span data-stu-id="f4924-147">It is mandatory that the image contains the .NET 3.5 runtime to install the SQL and MYSQL resource providers.</span></span> |
|<span data-ttu-id="f4924-148">Version (версия)</span><span class="sxs-lookup"><span data-stu-id="f4924-148">Version</span></span>|<span data-ttu-id="f4924-149">Нет</span><span class="sxs-lookup"><span data-stu-id="f4924-149">No</span></span>|<span data-ttu-id="f4924-150">Этот параметр позволяет выбрать, следует ли добавить **Core** или **полного** или **оба** образы Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="f4924-150">This parameter allows you to choose whether to add a **Core** or **Full** or **Both** Windows Server 2016 images.</span></span> <span data-ttu-id="f4924-151">По умолчанию это значение равно «Full».</span><span class="sxs-lookup"><span data-stu-id="f4924-151">By default, this value is set to "Full."</span></span>|
|<span data-ttu-id="f4924-152">VHDSizeInMB</span><span class="sxs-lookup"><span data-stu-id="f4924-152">VHDSizeInMB</span></span>|<span data-ttu-id="f4924-153">Нет</span><span class="sxs-lookup"><span data-stu-id="f4924-153">No</span></span>|<span data-ttu-id="f4924-154">Задает размер образа виртуального жесткого диска для добавления в среду Azure стека (в МБ).</span><span class="sxs-lookup"><span data-stu-id="f4924-154">Sets the size (in MB) of the VHD image to be added to your Azure Stack environment.</span></span> <span data-ttu-id="f4924-155">По умолчанию это значение будет присвоено 40960 МБ.</span><span class="sxs-lookup"><span data-stu-id="f4924-155">By default, this value is set to 40960 MB.</span></span>|
|<span data-ttu-id="f4924-156">CreateGalleryItem</span><span class="sxs-lookup"><span data-stu-id="f4924-156">CreateGalleryItem</span></span>|<span data-ttu-id="f4924-157">Нет</span><span class="sxs-lookup"><span data-stu-id="f4924-157">No</span></span>|<span data-ttu-id="f4924-158">Указывает, следует ли создать элемент Marketplace для образа Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="f4924-158">Specifies if a Marketplace item should be created for the Windows Server 2016 image.</span></span> <span data-ttu-id="f4924-159">По умолчанию это значение равным true.</span><span class="sxs-lookup"><span data-stu-id="f4924-159">By default, this value is set to true.</span></span>|
|<span data-ttu-id="f4924-160">location</span><span class="sxs-lookup"><span data-stu-id="f4924-160">location</span></span> |<span data-ttu-id="f4924-161">Нет</span><span class="sxs-lookup"><span data-stu-id="f4924-161">No</span></span> |<span data-ttu-id="f4924-162">Указывает расположение, к которому должны публиковаться образа Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="f4924-162">Specifies the location to which the Windows Server 2016 image should be published.</span></span>|
|<span data-ttu-id="f4924-163">IncludeLatestCU</span><span class="sxs-lookup"><span data-stu-id="f4924-163">IncludeLatestCU</span></span>|<span data-ttu-id="f4924-164">Нет</span><span class="sxs-lookup"><span data-stu-id="f4924-164">No</span></span>|<span data-ttu-id="f4924-165">Установите этот переключатель, чтобы применить последнее накопительное обновление Windows Server 2016 для нового виртуального жесткого диска.</span><span class="sxs-lookup"><span data-stu-id="f4924-165">Set this switch to apply the latest Windows Server 2016 cumulative update to the new VHD.</span></span>|
|<span data-ttu-id="f4924-166">CUUri</span><span class="sxs-lookup"><span data-stu-id="f4924-166">CUUri</span></span> |<span data-ttu-id="f4924-167">Нет</span><span class="sxs-lookup"><span data-stu-id="f4924-167">No</span></span> |<span data-ttu-id="f4924-168">Это значение используется для выбора накопительное обновление Windows Server 2016 из указанного URI.</span><span class="sxs-lookup"><span data-stu-id="f4924-168">Set this value to choose the Windows Server 2016 cumulative update from a specific URI.</span></span> |
|<span data-ttu-id="f4924-169">CUPath</span><span class="sxs-lookup"><span data-stu-id="f4924-169">CUPath</span></span> |<span data-ttu-id="f4924-170">Нет</span><span class="sxs-lookup"><span data-stu-id="f4924-170">No</span></span> |<span data-ttu-id="f4924-171">Это значение используется для выбора накопительное обновление Windows Server 2016 из локального пути.</span><span class="sxs-lookup"><span data-stu-id="f4924-171">Set this value to choose the Windows Server 2016 cumulative update from a local path.</span></span> <span data-ttu-id="f4924-172">Этот параметр полезен, если вы развернули экземпляра Azure стека в отключенной среде.</span><span class="sxs-lookup"><span data-stu-id="f4924-172">This option is helpful if you have deployed the Azure Stack instance in a disconnected environment.</span></span>|

## <a name="next-steps"></a><span data-ttu-id="f4924-173">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="f4924-173">Next steps</span></span>

[<span data-ttu-id="f4924-174">Подготовка виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="f4924-174">Provision a virtual machine</span></span>](azure-stack-provision-vm.md)
