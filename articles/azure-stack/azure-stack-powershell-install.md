---
title: "PowerShell для Azure стека aaaInstall | Документы Microsoft"
description: "Узнайте, как tooinstall PowerShell для Azure стека."
services: azure-stack
documentationcenter: 
author: SnehaGunda
manager: byronr
editor: 
ms.assetid: 
ms.service: azure-stack
ms.workload: na
pms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/03/2017
ms.author: sngun
ms.openlocfilehash: 60995af2168348638e2513ab941a4125ca5c624a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="install-powershell-for-azure-stack"></a><span data-ttu-id="c189a-103">Установите PowerShell для Azure стека</span><span class="sxs-lookup"><span data-stu-id="c189a-103">Install PowerShell for Azure Stack</span></span>  

<span data-ttu-id="c189a-104">Совместимые модули Azure PowerShell Azure стека являются обязательным toowork со стеком Azure.</span><span class="sxs-lookup"><span data-stu-id="c189a-104">Azure Stack compatible Azure PowerShell modules are required toowork with Azure Stack.</span></span> <span data-ttu-id="c189a-105">В этом руководстве мы рассмотрим tooinstall необходимые шаги hello PowerShell для Azure стека.</span><span class="sxs-lookup"><span data-stu-id="c189a-105">In this guide, we walk you through hello steps required tooinstall PowerShell for Azure Stack.</span></span> <span data-ttu-id="c189a-106">Можно использовать hello действия, описанные в этой статье из пакета средств разработки Azure стека hello или из внешнего клиента на основе Windows, при подключении через виртуальную частную сеть.</span><span class="sxs-lookup"><span data-stu-id="c189a-106">You can use hello steps described in this article either from hello Azure Stack Development Kit, or from a Windows-based external client if you are connected through VPN.</span></span>

<span data-ttu-id="c189a-107">В этой статье содержатся подробные инструкции по tooinstall PowerShell для Azure стека.</span><span class="sxs-lookup"><span data-stu-id="c189a-107">This article has detailed instructions tooinstall PowerShell for Azure Stack.</span></span> <span data-ttu-id="c189a-108">Тем не менее, tooquickly установить и настроить PowerShell, можно использовать сценарий hello, входящий в hello [приступить к работе с PowerShell](azure-stack-powershell-configure-quickstart.md) раздела.</span><span class="sxs-lookup"><span data-stu-id="c189a-108">However, if you want tooquickly install and configure PowerShell, you can use hello script that is provided in hello [Get up and running with PowerShell](azure-stack-powershell-configure-quickstart.md) topic.</span></span> 

> [!NOTE]
> <span data-ttu-id="c189a-109">Привет, следующие шаги требуют PowerShell 5.0.</span><span class="sxs-lookup"><span data-stu-id="c189a-109">hello following steps require PowerShell 5.0.</span></span> <span data-ttu-id="c189a-110">toocheck версии, выполнения $PSVersionTable.PSVersion и сравнить hello «основной» версии.</span><span class="sxs-lookup"><span data-stu-id="c189a-110">toocheck your version, run $PSVersionTable.PSVersion and compare hello "Major" version.</span></span>

<span data-ttu-id="c189a-111">Команды PowerShell для Azure стека устанавливаются через коллекцию PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="c189a-111">PowerShell commands for Azure Stack are installed through hello PowerShell gallery.</span></span> <span data-ttu-id="c189a-112">tooregiser hello PSGallery репозитория, откройте сеанс PowerShell с повышенными привилегиями из пакета средств разработки hello или из внешнего клиента, на основе Windows при подключении через виртуальную частную сеть запуска hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="c189a-112">tooregiser hello PSGallery repository, open an elevated PowerShell session from hello development kit or from a Windows-based external client if you are connected through VPN and run hello following command:</span></span>

```powershell
Set-PSRepository `
  -Name "PSGallery" `
  -InstallationPolicy Trusted
```

## <a name="uninstall-existing-versions-of-powershell"></a><span data-ttu-id="c189a-113">Удалите существующие версии PowerShell</span><span class="sxs-lookup"><span data-stu-id="c189a-113">Uninstall existing versions of PowerShell</span></span>

<span data-ttu-id="c189a-114">Прежде чем устанавливать hello требуемой версии, убедитесь, что удалить все существующие модули Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c189a-114">Before installing hello required version, make sure that you uninstall any existing Azure PowerShell modules.</span></span> <span data-ttu-id="c189a-115">Их можно удалить с помощью одного из следующих двух методов hello:</span><span class="sxs-lookup"><span data-stu-id="c189a-115">You can uninstall them by using one of hello following two methods:</span></span>

* <span data-ttu-id="c189a-116">модули toouninstall hello существующих PowerShell, войдите в пакет средств разработки toohello или внешних toohello клиента на основе Windows, при планировании tooestablish VPN-подключения.</span><span class="sxs-lookup"><span data-stu-id="c189a-116">toouninstall hello existing PowerShell modules, sign in toohello development kit, or toohello Windows-based external client if you are planning tooestablish a VPN connection.</span></span> <span data-ttu-id="c189a-117">Закройте все активные сеансы PowerShell hello и выполнения hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="c189a-117">Close all hello active PowerShell sessions and run hello following command:</span></span> 

   ```powershell
   Get-Module -ListAvailable | where-Object {$_.Name -like “Azure*”} | Uninstall-Module
   ```

* <span data-ttu-id="c189a-118">Войдите в пакет средств разработки toohello или внешних toohello клиента на основе Windows, при планировании tooestablish VPN-подключения.</span><span class="sxs-lookup"><span data-stu-id="c189a-118">Sign in toohello development kit, or toohello Windows-based external client if you are planning tooestablish a VPN connection.</span></span> <span data-ttu-id="c189a-119">Удалить все hello папки, которые начинаются с «Azure» из hello `C:\Program Files (x86)\WindowsPowerShell\Modules` и `C:\Users\AzureStackAdmin\Documents\WindowsPowerShell\Modules` папки.</span><span class="sxs-lookup"><span data-stu-id="c189a-119">Delete all hello folders that start with "Azure" from hello `C:\Program Files (x86)\WindowsPowerShell\Modules` and `C:\Users\AzureStackAdmin\Documents\WindowsPowerShell\Modules` folders.</span></span> <span data-ttu-id="c189a-120">Удаление этих папок удаляет все существующие модули PowerShell из «AzureStackAdmin» hello и области «глобальные» пользователя.</span><span class="sxs-lookup"><span data-stu-id="c189a-120">Deleting these folders removes any existing PowerShell modules from hello "AzureStackAdmin" and "global" user scopes.</span></span> 

<span data-ttu-id="c189a-121">Hello следующих разделах описаны tooinstall необходимые шаги hello PowerShell для Azure стека.</span><span class="sxs-lookup"><span data-stu-id="c189a-121">hello following sections describe hello steps required tooinstall PowerShell for Azure Stack.</span></span> <span data-ttu-id="c189a-122">PowerShell можно установить на стек Azure, который выполняется в подключенной, частично подключен, или в сценарии отсоединения.</span><span class="sxs-lookup"><span data-stu-id="c189a-122">PowerShell can be installed on Azure Stack that is operated in connected, partially connected, or in a disconnected scenario.</span></span> 

## <a name="install-powershell-in-a-connected-scenario"></a><span data-ttu-id="c189a-123">Установите в связанный сценарий PowerShell</span><span class="sxs-lookup"><span data-stu-id="c189a-123">Install PowerShell in a connected scenario</span></span> 

<span data-ttu-id="c189a-124">Совместимые модули AzureRM Azure стека устанавливаются через профили версии API.</span><span class="sxs-lookup"><span data-stu-id="c189a-124">Azure Stack compatible AzureRM modules are installed through API version profiles.</span></span> <span data-ttu-id="c189a-125">Стек Azure требует hello **2017 г. 03-09-профиля** профиля версии API, который доступен при установке модуля AzureRM.Bootstrapper hello.</span><span class="sxs-lookup"><span data-stu-id="c189a-125">Azure Stack requires hello **2017-03-09-profile** API version profile, which is available by installing hello AzureRM.Bootstrapper module.</span></span> <span data-ttu-id="c189a-126">toolearn о профилях версии API и командлеты hello из них, см. toohello [управления профилями версии API](azure-stack-version-profiles.md).</span><span class="sxs-lookup"><span data-stu-id="c189a-126">toolearn about API version profiles and hello cmdlets provided by them, refer toohello [manage API version profiles](azure-stack-version-profiles.md).</span></span> <span data-ttu-id="c189a-127">В модулях AzureRM toohello сложения также следует установить модули PowerShell Azure стека конкретного hello.</span><span class="sxs-lookup"><span data-stu-id="c189a-127">In addition toohello AzureRM modules, you should also install hello Azure Stack-specific PowerShell modules.</span></span> <span data-ttu-id="c189a-128">На рабочей станции разработки, выполните эти модули hello, следуя tooinstall сценарий PowerShell:</span><span class="sxs-lookup"><span data-stu-id="c189a-128">Run hello following PowerShell script tooinstall these modules on your development workstation:</span></span>

  ```powershell
  # Install hello AzureRM.Bootstrapper module. Select Yes when prompted tooinstall NuGet 
  Install-Module `
    -Name AzureRm.BootStrapper

  # Install and import hello API Version Profile required by Azure Stack into hello current PowerShell session.
  Use-AzureRmProfile `
    -Profile 2017-03-09-profile -Force

  Install-Module `
    -Name AzureStack `
    -RequiredVersion 1.2.10
  ```

<span data-ttu-id="c189a-129">tooconfirm установки hello, перезапустите hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="c189a-129">tooconfirm hello installation, run hello following command:</span></span>

  ```powershell
  Get-Module `
    -ListAvailable | where-Object {$_.Name -like “Azure*”}
  ```
  <span data-ttu-id="c189a-130">При успешном выполнении установки hello hello AzureRM и AzureStack модули отображаются в выходных данных hello.</span><span class="sxs-lookup"><span data-stu-id="c189a-130">If hello installation is successful, hello AzureRM and AzureStack modules are displayed in hello output.</span></span>

## <a name="install-powershell-in-a-disconnected-or-in-a-partially-connected-scenario"></a><span data-ttu-id="c189a-131">Установите PowerShell в отключенном или в сценарии с частично подключенным</span><span class="sxs-lookup"><span data-stu-id="c189a-131">Install PowerShell in a disconnected or in a partially connected scenario</span></span>

<span data-ttu-id="c189a-132">В сценарии отсоединения необходимо сначала загрузить hello модули PowerShell tooa компьютере с подключением к Интернету и передает их toohello Azure стека Development Kit для установки.</span><span class="sxs-lookup"><span data-stu-id="c189a-132">In a disconnected scenario, you must first download hello PowerShell modules tooa machine that has internet connectivity, and then transfer them toohello Azure Stack Development Kit for installation.</span></span>

1. <span data-ttu-id="c189a-133">Войдите в компьютер tooa которой вы подключены к Интернету и использовать следующий скрипт toodownload hello AzureRM hello и AzureStack пакеты на локальном компьютере.</span><span class="sxs-lookup"><span data-stu-id="c189a-133">Sign in tooa computer where you have internet connectivity and use hello following script toodownload hello AzureRM, and AzureStack packages onto your local computer:</span></span>

   ```powershell
   $Path = "<Path that is used toosave hello packages>"

   Save-Package `
     -ProviderName NuGet `
     -Source https://www.powershellgallery.com/api/v2 `
     -Name AzureRM `
     -Path $Path `
     -Force `
     -RequiredVersion 1.2.10

   Save-Package `
     -ProviderName NuGet `
     -Source https://www.powershellgallery.com/api/v2 `
     -Name AzureStack `
     -Path $Path `
     -Force `
     -RequiredVersion 1.2.10 
   ```

2. <span data-ttu-id="c189a-134">Копировать hello загруженных пакетов через tooa USB-устройство.</span><span class="sxs-lookup"><span data-stu-id="c189a-134">Copy hello downloaded packages over tooa USB device.</span></span>

3. <span data-ttu-id="c189a-135">Войдите в пакет средств разработки toohello и скопируйте hello пакетов из расположения tooa устройства USB hello в пакет средств разработки hello.</span><span class="sxs-lookup"><span data-stu-id="c189a-135">Sign in toohello development kit and copy hello packages from hello USB device tooa location on hello development kit.</span></span> 

4. <span data-ttu-id="c189a-136">Теперь необходимо зарегистрировать это расположение в качестве репозитория по умолчанию hello и установить hello AzureRM и AzureStack модули из этого репозитория:</span><span class="sxs-lookup"><span data-stu-id="c189a-136">Now you must register this location as hello default repository and install hello AzureRM and AzureStack modules from this repository:</span></span>

   ```powershell
   $SourceLocation = "<Location on hello development kit that contains hello PowerShell packages>"
   $RepoName = "MyNuGetSource"

   Register-PSRepository `
     -Name $RepoName `
     -SourceLocation $SourceLocation `
     -InstallationPolicy Trusted

   ```powershell
   Install-Module AzureRM `
     -Repository $RepoName

   Install-Module AzureStack `
     -Repository $RepoName 
   ```

## <a name="next-steps"></a><span data-ttu-id="c189a-137">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="c189a-137">Next steps</span></span>

* [<span data-ttu-id="c189a-138">Загрузить набор средств Azure стека из GitHub</span><span class="sxs-lookup"><span data-stu-id="c189a-138">Download Azure Stack tools from GitHub</span></span>](azure-stack-powershell-download.md)
* [<span data-ttu-id="c189a-139">Настройка среды PowerShell hello Azure стека пользователя</span><span class="sxs-lookup"><span data-stu-id="c189a-139">Configure hello Azure Stack user's PowerShell environment</span></span>](azure-stack-powershell-configure-user.md)  
* [<span data-ttu-id="c189a-140">Настройка среды PowerShell оператор hello стек Azure</span><span class="sxs-lookup"><span data-stu-id="c189a-140">Configure hello Azure Stack operator's PowerShell environment</span></span>](azure-stack-powershell-configure-admin.md) 
* [<span data-ttu-id="c189a-141">Управление профилями версии API в стек Azure</span><span class="sxs-lookup"><span data-stu-id="c189a-141">Manage API version profiles in Azure Stack</span></span>](azure-stack-version-profiles.md)  
