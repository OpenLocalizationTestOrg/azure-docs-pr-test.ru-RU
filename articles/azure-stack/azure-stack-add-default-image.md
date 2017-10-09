---
title: "aaaAdd ВМ по умолчанию hello образа marketplace стек Azure toohello | Документы Microsoft"
description: "Добавьте hello виртуальной Машины Windows Server 2016 по умолчанию изображение toohello стека Azure marketplace."
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
ms.openlocfilehash: 9b5a6f4e4c73c706b059e3c3622a968b5eef9a27
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="add-hello-windows-server-2016-vm-image-toohello-azure-stack-marketplace"></a><span data-ttu-id="bc1b2-103">Добавить hello виртуальной Машины Windows Server 2016 изображения toohello стека Azure marketplace</span><span class="sxs-lookup"><span data-stu-id="bc1b2-103">Add hello Windows Server 2016 VM image toohello Azure Stack marketplace</span></span>

<span data-ttu-id="bc1b2-104">По умолчанию отсутствуют все образы виртуальных машин в hello стек Azure marketplace.</span><span class="sxs-lookup"><span data-stu-id="bc1b2-104">By default, there aren’t any virtual machine images available in hello Azure Stack marketplace.</span></span> <span data-ttu-id="bc1b2-105">администратору облака Azure стека Hello необходимо добавить toohello образа marketplace, чтобы пользователи могли использовать их.</span><span class="sxs-lookup"><span data-stu-id="bc1b2-105">hello Azure Stack cloud administrator must add an image toohello marketplace before users can use them.</span></span> <span data-ttu-id="bc1b2-106">Windows Server 2016 hello изображения toohello стека Azure marketplace можно добавить с помощью одного из следующих двух методов hello:</span><span class="sxs-lookup"><span data-stu-id="bc1b2-106">You can add hello Windows Server 2016 image toohello Azure Stack marketplace by using one of hello following two methods:</span></span>

* <span data-ttu-id="bc1b2-107">[Добавить изображение hello, загрузив его с hello Azure Marketplace](#add-the-image-by-downloading-it-from-the-Azure-marketplace) -используйте этот параметр, если вы работаете в сценарии подключенных и если вы зарегистрировали экземпляра Azure стека с помощью Azure.</span><span class="sxs-lookup"><span data-stu-id="bc1b2-107">[Add hello image by downloading it from hello Azure Marketplace](#add-the-image-by-downloading-it-from-the-Azure-marketplace) - Use this option if you are operating in a connected scenario and if you have registered your Azure Stack instance with Azure.</span></span>

* <span data-ttu-id="bc1b2-108">[Добавить изображение hello с помощью PowerShell](#add-the-image-by-using-powershell) -используйте этот параметр, если вы развернули стек Azure в сценарии отсоединения, или в сценариях с ограниченной подключением.</span><span class="sxs-lookup"><span data-stu-id="bc1b2-108">[Add hello image by using PowerShell](#add-the-image-by-using-powershell) - Use this option if you have deployed Azure Stack in a disconnected scenario or in scenarios with limited connectivity.</span></span>

## <a name="add-hello-image-by-downloading-it-from-hello-azure-marketplace"></a><span data-ttu-id="bc1b2-109">Добавить изображение hello, загрузив его с hello Azure Marketplace</span><span class="sxs-lookup"><span data-stu-id="bc1b2-109">Add hello image by downloading it from hello Azure Marketplace</span></span>

1. <span data-ttu-id="bc1b2-110">После развертывания Azure стека, войдите в tooyour пакет средств разработки Azure стека.</span><span class="sxs-lookup"><span data-stu-id="bc1b2-110">After deploying Azure Stack, sign in tooyour Azure Stack Development Kit.</span></span>

2. <span data-ttu-id="bc1b2-111">Нажмите кнопку **дополнительные службы** > **управления Marketplace** > **добавить из Azure**</span><span class="sxs-lookup"><span data-stu-id="bc1b2-111">click **More services** > **Marketplace Management** > **Add from Azure**</span></span> 

3. <span data-ttu-id="bc1b2-112">Поиск или поиск hello **Windows Server 2016 центра обработки данных — Eval** изображение > щелкните **загрузки**</span><span class="sxs-lookup"><span data-stu-id="bc1b2-112">Find or search for hello **Windows Server 2016 Datacenter – Eval** image > click **Download**</span></span>

   ![Загрузите образ из Azure](media/azure-stack-add-default-image/download-image.png)

<span data-ttu-id="bc1b2-114">После завершения загрузки hello hello изображение будет добавлено toohello **управления Marketplace** колонки и он также доступен из hello **виртуальные машины** колонку.</span><span class="sxs-lookup"><span data-stu-id="bc1b2-114">After hello download completes, hello image is added toohello **Marketplace Management** blade and it is also made available from hello **Virtual Machines** blade.</span></span>

## <a name="add-hello-image-by-using-powershell"></a><span data-ttu-id="bc1b2-115">Добавить изображение hello с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="bc1b2-115">Add hello image by using PowerShell</span></span>

### <a name="prerequisites"></a><span data-ttu-id="bc1b2-116">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="bc1b2-116">Prerequisites</span></span> 

<span data-ttu-id="bc1b2-117">Запустите hello следующие необходимые компоненты из hello [пакет средств разработки](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-remote-desktop), или из внешнего клиента Windows в случае [подключен через виртуальную частную сеть](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-vpn):</span><span class="sxs-lookup"><span data-stu-id="bc1b2-117">Run hello following prerequisites either from hello [development kit](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-remote-desktop), or from a Windows-based external client if you are [connected through VPN](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-vpn):</span></span>

* <span data-ttu-id="bc1b2-118">Установка [модули Azure PowerShell Azure стека совместимой](azure-stack-powershell-install.md).</span><span class="sxs-lookup"><span data-stu-id="bc1b2-118">Install [Azure Stack-compatible Azure PowerShell modules](azure-stack-powershell-install.md).</span></span>  

* <span data-ttu-id="bc1b2-119">Загрузите hello [toowork необходимые средства с Azure стека](azure-stack-powershell-download.md).</span><span class="sxs-lookup"><span data-stu-id="bc1b2-119">Download hello [tools required toowork with Azure Stack](azure-stack-powershell-download.md).</span></span>  

* <span data-ttu-id="bc1b2-120">Go toohttps://www.microsoft.com/en-us/evalcenter/evaluate-windows-server-2016 и загрузка пробной версии Windows Server 2016 hello.</span><span class="sxs-lookup"><span data-stu-id="bc1b2-120">Go toohttps://www.microsoft.com/en-us/evalcenter/evaluate-windows-server-2016 and download hello Windows Server 2016 evaluation.</span></span> <span data-ttu-id="bc1b2-121">При появлении запроса выберите hello **ISO** версии hello загрузки.</span><span class="sxs-lookup"><span data-stu-id="bc1b2-121">When prompted, select hello **ISO** version of hello download.</span></span> <span data-ttu-id="bc1b2-122">Путь toohello записей hello загрузите расположение, которое будет использоваться в дальнейшем эти действия.</span><span class="sxs-lookup"><span data-stu-id="bc1b2-122">Record hello path toohello download location, which is used later in these steps.</span></span> <span data-ttu-id="bc1b2-123">Необходимо подключение к Интернету.</span><span class="sxs-lookup"><span data-stu-id="bc1b2-123">This step requires internet connectivity.</span></span>  

<span data-ttu-id="bc1b2-124">Теперь выполните следующие шаги tooadd hello изображения toohello стека Azure marketplace hello.</span><span class="sxs-lookup"><span data-stu-id="bc1b2-124">Now run hello following steps tooadd hello image toohello Azure Stack marketplace:</span></span>
   
1. <span data-ttu-id="bc1b2-125">Импортируйте модули Azure Connect стека и ComputeAdmin hello с помощью hello, следующие команды:</span><span class="sxs-lookup"><span data-stu-id="bc1b2-125">Import hello Azure Stack Connect and ComputeAdmin modules by using hello following commands:</span></span>

   ```powershell
   Set-ExecutionPolicy RemoteSigned

   # import hello Connect and ComputeAdmin modules   
   Import-Module .\Connect\AzureStack.Connect.psm1
   Import-Module .\ComputeAdmin\AzureStack.ComputeAdmin.psm1

   ```

2. <span data-ttu-id="bc1b2-126">Войдите в систему tooyour среды Azure стека.</span><span class="sxs-lookup"><span data-stu-id="bc1b2-126">Sign in tooyour Azure Stack environment.</span></span> <span data-ttu-id="bc1b2-127">Выполнения hello следующий скрипт в зависимости от того, при развертывании среды стека Azure с помощью AAD или AD FS (Убедитесь, что tooreplace hello AAD имя клиента):</span><span class="sxs-lookup"><span data-stu-id="bc1b2-127">Run hello following script depending on if your Azure Stack environment is deployed by using AAD or AD FS (Make sure tooreplace hello AAD tenant name):</span></span>  

   <span data-ttu-id="bc1b2-128">а.</span><span class="sxs-lookup"><span data-stu-id="bc1b2-128">a.</span></span> <span data-ttu-id="bc1b2-129">**Azure Active Directory**, используйте следующий командлет hello:</span><span class="sxs-lookup"><span data-stu-id="bc1b2-129">**Azure Active Directory**, use hello following cmdlet:</span></span>

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

   <span data-ttu-id="bc1b2-130">b.</span><span class="sxs-lookup"><span data-stu-id="bc1b2-130">b.</span></span> <span data-ttu-id="bc1b2-131">**Службы федерации Active Directory**, используйте следующий командлет hello:</span><span class="sxs-lookup"><span data-stu-id="bc1b2-131">**Active Directory Federation Services**, use hello following cmdlet:</span></span>
    
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
   
3. <span data-ttu-id="bc1b2-132">Добавьте Windows Server 2016 hello изображения toohello стека Azure marketplace (Убедитесь, что hello tooreplace *Path_to_ISO* с toohello путь hello загруженный ISO WS2016):</span><span class="sxs-lookup"><span data-stu-id="bc1b2-132">Add hello Windows Server 2016 image toohello Azure Stack marketplace (Make sure tooreplace hello *Path_to_ISO* with hello path toohello WS2016 ISO you downloaded):</span></span>

   ```PowerShell
   $ISOPath = "<Fully_Qualified_Path_to_ISO>"

   # Add a Windows Server 2016 Evaluation VM Image.
   New-AzsServer2016VMImage `
     -ISOPath $ISOPath

   ```

<span data-ttu-id="bc1b2-133">tooensure, hello образ виртуальной Машины Windows Server 2016 имеет hello последний накопительный пакет обновления, включают hello `IncludeLatestCU` при выполнении hello `New-AzsServer2016VMImage` командлета.</span><span class="sxs-lookup"><span data-stu-id="bc1b2-133">tooensure that hello Windows Server 2016 VM image has hello latest cumulative update, include hello `IncludeLatestCU` parameter when running hello `New-AzsServer2016VMImage` cmdlet.</span></span> <span data-ttu-id="bc1b2-134">В разделе hello [параметры](#parameters) сведения о допустимых параметрах hello `New-AzsServer2016VMImage` командлет.</span><span class="sxs-lookup"><span data-stu-id="bc1b2-134">See hello [Parameters](#parameters) section for information about allowed parameters for hello `New-AzsServer2016VMImage` cmdlet.</span></span> <span data-ttu-id="bc1b2-135">Это занимает около часа toopublish hello изображения toohello стека Azure marketplace.</span><span class="sxs-lookup"><span data-stu-id="bc1b2-135">It takes about an hour toopublish hello image toohello Azure Stack marketplace.</span></span> 

## <a name="parameters"></a><span data-ttu-id="bc1b2-136">Параметры</span><span class="sxs-lookup"><span data-stu-id="bc1b2-136">Parameters</span></span>

|<span data-ttu-id="bc1b2-137">Параметры нового AzsServer2016VMImage</span><span class="sxs-lookup"><span data-stu-id="bc1b2-137">New-AzsServer2016VMImage parameters</span></span>|<span data-ttu-id="bc1b2-138">Обязательный?</span><span class="sxs-lookup"><span data-stu-id="bc1b2-138">Required?</span></span>|<span data-ttu-id="bc1b2-139">Описание</span><span class="sxs-lookup"><span data-stu-id="bc1b2-139">Description</span></span>|
|-----|-----|------|
|<span data-ttu-id="bc1b2-140">ISOPath</span><span class="sxs-lookup"><span data-stu-id="bc1b2-140">ISOPath</span></span>|<span data-ttu-id="bc1b2-141">Да</span><span class="sxs-lookup"><span data-stu-id="bc1b2-141">Yes</span></span>|<span data-ttu-id="bc1b2-142">Hello toohello полный путь загрузки Windows Server 2016 ISO.</span><span class="sxs-lookup"><span data-stu-id="bc1b2-142">hello fully qualified path toohello downloaded Windows Server 2016 ISO.</span></span>|
|<span data-ttu-id="bc1b2-143">net35</span><span class="sxs-lookup"><span data-stu-id="bc1b2-143">Net35</span></span>|<span data-ttu-id="bc1b2-144">Нет</span><span class="sxs-lookup"><span data-stu-id="bc1b2-144">No</span></span>|<span data-ttu-id="bc1b2-145">Этот параметр позволяет среды выполнения .NET 3.5 hello tooinstall в образ Windows Server 2016 hello.</span><span class="sxs-lookup"><span data-stu-id="bc1b2-145">This parameter allows you tooinstall hello .NET 3.5 runtime on hello Windows Server 2016 image.</span></span> <span data-ttu-id="bc1b2-146">По умолчанию это значение имеет значение tootrue.</span><span class="sxs-lookup"><span data-stu-id="bc1b2-146">By default, this value is set tootrue.</span></span> <span data-ttu-id="bc1b2-147">Является обязательным, что это изображение hello содержит hello .NET 3.5 среды выполнения tooinstall hello SQL и MYSQL поставщиков ресурсов.</span><span class="sxs-lookup"><span data-stu-id="bc1b2-147">It is mandatory that hello image contains hello .NET 3.5 runtime tooinstall hello SQL and MYSQL resource providers.</span></span> |
|<span data-ttu-id="bc1b2-148">Version (версия)</span><span class="sxs-lookup"><span data-stu-id="bc1b2-148">Version</span></span>|<span data-ttu-id="bc1b2-149">Нет</span><span class="sxs-lookup"><span data-stu-id="bc1b2-149">No</span></span>|<span data-ttu-id="bc1b2-150">Этот параметр позволяет вам toochoose ли tooadd **Core** или **полного** или **оба** образы Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="bc1b2-150">This parameter allows you toochoose whether tooadd a **Core** or **Full** or **Both** Windows Server 2016 images.</span></span> <span data-ttu-id="bc1b2-151">По умолчанию это значение «Переполнен.»</span><span class="sxs-lookup"><span data-stu-id="bc1b2-151">By default, this value is set too"Full."</span></span>|
|<span data-ttu-id="bc1b2-152">VHDSizeInMB</span><span class="sxs-lookup"><span data-stu-id="bc1b2-152">VHDSizeInMB</span></span>|<span data-ttu-id="bc1b2-153">Нет</span><span class="sxs-lookup"><span data-stu-id="bc1b2-153">No</span></span>|<span data-ttu-id="bc1b2-154">Задает hello объем (в МБ) toobe образа виртуального жесткого диска hello добавлен tooyour среду стека Azure.</span><span class="sxs-lookup"><span data-stu-id="bc1b2-154">Sets hello size (in MB) of hello VHD image toobe added tooyour Azure Stack environment.</span></span> <span data-ttu-id="bc1b2-155">По умолчанию это значение задано too40960 МБ.</span><span class="sxs-lookup"><span data-stu-id="bc1b2-155">By default, this value is set too40960 MB.</span></span>|
|<span data-ttu-id="bc1b2-156">CreateGalleryItem</span><span class="sxs-lookup"><span data-stu-id="bc1b2-156">CreateGalleryItem</span></span>|<span data-ttu-id="bc1b2-157">Нет</span><span class="sxs-lookup"><span data-stu-id="bc1b2-157">No</span></span>|<span data-ttu-id="bc1b2-158">Указывает, следует ли создать элемент Marketplace для образа Windows Server 2016 hello.</span><span class="sxs-lookup"><span data-stu-id="bc1b2-158">Specifies if a Marketplace item should be created for hello Windows Server 2016 image.</span></span> <span data-ttu-id="bc1b2-159">По умолчанию это значение имеет значение tootrue.</span><span class="sxs-lookup"><span data-stu-id="bc1b2-159">By default, this value is set tootrue.</span></span>|
|<span data-ttu-id="bc1b2-160">location</span><span class="sxs-lookup"><span data-stu-id="bc1b2-160">location</span></span> |<span data-ttu-id="bc1b2-161">Нет</span><span class="sxs-lookup"><span data-stu-id="bc1b2-161">No</span></span> |<span data-ttu-id="bc1b2-162">Указывает расположение toowhich hello hello-образ Windows Server 2016 должна быть опубликована.</span><span class="sxs-lookup"><span data-stu-id="bc1b2-162">Specifies hello location toowhich hello Windows Server 2016 image should be published.</span></span>|
|<span data-ttu-id="bc1b2-163">IncludeLatestCU</span><span class="sxs-lookup"><span data-stu-id="bc1b2-163">IncludeLatestCU</span></span>|<span data-ttu-id="bc1b2-164">Нет</span><span class="sxs-lookup"><span data-stu-id="bc1b2-164">No</span></span>|<span data-ttu-id="bc1b2-165">Установите этот переключатель tooapply hello последнюю Windows Server 2016 накопительное обновление toohello нового виртуального жесткого диска.</span><span class="sxs-lookup"><span data-stu-id="bc1b2-165">Set this switch tooapply hello latest Windows Server 2016 cumulative update toohello new VHD.</span></span>|
|<span data-ttu-id="bc1b2-166">CUUri</span><span class="sxs-lookup"><span data-stu-id="bc1b2-166">CUUri</span></span> |<span data-ttu-id="bc1b2-167">Нет</span><span class="sxs-lookup"><span data-stu-id="bc1b2-167">No</span></span> |<span data-ttu-id="bc1b2-168">Задайте значение toochoose hello Windows Server 2016 накопительного обновления от указанного URI.</span><span class="sxs-lookup"><span data-stu-id="bc1b2-168">Set this value toochoose hello Windows Server 2016 cumulative update from a specific URI.</span></span> |
|<span data-ttu-id="bc1b2-169">CUPath</span><span class="sxs-lookup"><span data-stu-id="bc1b2-169">CUPath</span></span> |<span data-ttu-id="bc1b2-170">Нет</span><span class="sxs-lookup"><span data-stu-id="bc1b2-170">No</span></span> |<span data-ttu-id="bc1b2-171">Задайте значение toochoose hello Windows Server 2016 накопительного обновления из локального пути.</span><span class="sxs-lookup"><span data-stu-id="bc1b2-171">Set this value toochoose hello Windows Server 2016 cumulative update from a local path.</span></span> <span data-ttu-id="bc1b2-172">Этот параметр полезен, если вы развернули экземпляр hello Azure стека в отключенной среде.</span><span class="sxs-lookup"><span data-stu-id="bc1b2-172">This option is helpful if you have deployed hello Azure Stack instance in a disconnected environment.</span></span>|

## <a name="next-steps"></a><span data-ttu-id="bc1b2-173">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="bc1b2-173">Next steps</span></span>

[<span data-ttu-id="bc1b2-174">Подготовка виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="bc1b2-174">Provision a virtual machine</span></span>](azure-stack-provision-vm.md)
