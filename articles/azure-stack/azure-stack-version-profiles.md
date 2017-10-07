---
title: "профили aaaUsing API версии в стек Azure | Документы Microsoft"
description: "Сведения о профилях версии API в Azure стека."
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
ms.date: 03/21/2017
ms.author: sngun
ms.openlocfilehash: cb54a683054f08fd123bcb6245d88aaa30c29882
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="manage-api-version-profiles-in-azure-stack"></a><span data-ttu-id="725d0-103">Управление профилями версии API в стек Azure</span><span class="sxs-lookup"><span data-stu-id="725d0-103">Manage API version profiles in Azure Stack</span></span>

<span data-ttu-id="725d0-104">Профили версии API обеспечивают toomanage способом версии различия между Azure и Azure стека.</span><span class="sxs-lookup"><span data-stu-id="725d0-104">API version profiles provide a way toomanage version differences between Azure and Azure Stack.</span></span> <span data-ttu-id="725d0-105">Профиль версии API — это набор модулей AzureRM PowerShell для определенной версии API.</span><span class="sxs-lookup"><span data-stu-id="725d0-105">An API version profile is a set of AzureRM PowerShell modules with specific API versions.</span></span> <span data-ttu-id="725d0-106">Каждая облачная платформа имеет набор профилей версии поддерживаемых API.</span><span class="sxs-lookup"><span data-stu-id="725d0-106">Each cloud platform has a set of supported API version profiles.</span></span> <span data-ttu-id="725d0-107">Например, стека Azure поддерживает определенный профиль устаревшей версии, например **2017 г. 03-09-профиля**и hello Azure поддерживает **последние** профиля версии API.</span><span class="sxs-lookup"><span data-stu-id="725d0-107">For example, Azure Stack supports a specific dated profile version such as  **2017-03-09-profile**, and Azure supports hello **latest** API version profile.</span></span> <span data-ttu-id="725d0-108">При установке профиля hello AzureRM PowerShell модули, которые соответствуют toohello указан профиль установлены.</span><span class="sxs-lookup"><span data-stu-id="725d0-108">When you install a profile, hello AzureRM PowerShell modules that correspond toohello specified profile are installed.</span></span>

## <a name="install-hello-powershell-module-required-toouse-api-version-profiles"></a><span data-ttu-id="725d0-109">Установка профилей hello API toouse модуля, который требуется PowerShell версии</span><span class="sxs-lookup"><span data-stu-id="725d0-109">Install hello PowerShell module required toouse API version profiles</span></span>

<span data-ttu-id="725d0-110">Hello **AzureRM.Bootstrapper** модуль, который доступен через hello коллекции PowerShell предоставляет командлеты PowerShell, которые требуется toowork с профилями версии API.</span><span class="sxs-lookup"><span data-stu-id="725d0-110">hello **AzureRM.Bootstrapper** module that is available through hello PowerShell Gallery provides PowerShell cmdlets that are required toowork with API version profiles.</span></span> <span data-ttu-id="725d0-111">Используйте следующий командлет tooinstall hello AzureRM.Bootstrapper модуль hello.</span><span class="sxs-lookup"><span data-stu-id="725d0-111">Use hello following cmdlet tooinstall hello AzureRM.Bootstrapper module:</span></span>

```PowerShell
Install-Module -Name AzureRm.BootStrapper
```
<span data-ttu-id="725d0-112">Hello AzureRM.Bootstrapper модуль находится в режиме предварительного просмотра; сведения и функциональные возможности могут toochange субъекта.</span><span class="sxs-lookup"><span data-stu-id="725d0-112">hello AzureRM.Bootstrapper module is in preview; details and functionality are subject toochange.</span></span> <span data-ttu-id="725d0-113">toodownload и установите hello последнюю версию этого модуля из hello коллекции PowerShell, запустите следующий командлет hello:</span><span class="sxs-lookup"><span data-stu-id="725d0-113">toodownload and install hello latest version of this module from hello PowerShell Gallery, run hello following cmdlet:</span></span>

```PowerShell
Update-Module -Name "AzureRm.BootStrapper"
```

## <a name="install-a-profile"></a><span data-ttu-id="725d0-114">Установка профиля</span><span class="sxs-lookup"><span data-stu-id="725d0-114">Install a profile</span></span>

<span data-ttu-id="725d0-115">Используйте hello **установки AzureRmProfile** командлет с hello **2017 г. 03-09-профиля** AzureRM API версии профиль tooinstall hello модулями, необходимыми стеком Azure.</span><span class="sxs-lookup"><span data-stu-id="725d0-115">Use hello **Install-AzureRmProfile** cmdlet with hello **2017-03-09-profile** API version profile tooinstall hello AzureRM modules required by Azure Stack.</span></span> <span data-ttu-id="725d0-116">Обратите внимание, что с этим профилем версия API не установлены модули администратора облака Azure стека hello, и они должны устанавливаться отдельно, как указано в hello шаг 3 из hello [Установка PowerShell для Azure стека](azure-stack-powershell-install.md) статьи.</span><span class="sxs-lookup"><span data-stu-id="725d0-116">Note that hello Azure Stack cloud administrator modules are not installed with this API version profile, and they should be installed separately as specified in hello Step 3 of hello [Install PowerShell for Azure Stack](azure-stack-powershell-install.md) article.</span></span>

```PowerShell 
Install-AzureRMProfile -Profile 2017-03-09-profile
```
## <a name="install-and-import-modules-in-a-profile"></a><span data-ttu-id="725d0-117">Установить и импортировать модули в профиле</span><span class="sxs-lookup"><span data-stu-id="725d0-117">Install and import modules in a profile</span></span>

<span data-ttu-id="725d0-118">Используйте hello **AzureRmProfile используйте** tooinstall и импортируйте модули командлетов, связанных с профилем версии API.</span><span class="sxs-lookup"><span data-stu-id="725d0-118">Use hello **Use-AzureRmProfile** cmdlet tooinstall and import modules that are associated with an API version profile.</span></span> <span data-ttu-id="725d0-119">В сеансе PowerShell можно импортировать только один профиль версии API.</span><span class="sxs-lookup"><span data-stu-id="725d0-119">You can import only one API version profile in a PowerShell session.</span></span> <span data-ttu-id="725d0-120">профиль tooimport различных API версии, необходимо открыть новый сеанс PowerShell.</span><span class="sxs-lookup"><span data-stu-id="725d0-120">tooimport a different API version profile, you must open a new PowerShell session.</span></span> <span data-ttu-id="725d0-121">Используйте AzureRMProfile Hello выполняет hello следующие задачи:</span><span class="sxs-lookup"><span data-stu-id="725d0-121">hello Use-AzureRMProfile cmdlet runs hello following tasks:</span></span>  
1. <span data-ttu-id="725d0-122">Проверяет, модули PowerShell hello, связанные с hello указанный профиль версии API устанавливаются в текущей области hello.</span><span class="sxs-lookup"><span data-stu-id="725d0-122">Checks if hello PowerShell modules associated with hello specified API version profile are installed in hello current scope.</span></span>  
2. <span data-ttu-id="725d0-123">Загрузка и установка hello модулей, если они еще не установлены.</span><span class="sxs-lookup"><span data-stu-id="725d0-123">Downloads and installs hello modules if they are not already installed.</span></span>   
3. <span data-ttu-id="725d0-124">Импортирует hello модули в текущий сеанс PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="725d0-124">Imports hello modules into hello current PowerShell session.</span></span> 

```PowerShell
# Installs and imports hello specified API version profile into hello current PowerShell session.
Use-AzureRmProfile -Profile 2017-03-09-profile -Scope CurrentUser

# Installs and imports hello specified API version profile into hello current PowerShell session without any prompts
Use-AzureRmProfile -Profile 2017-03-09-profile -Scope CurrentUser -Force
```

<span data-ttu-id="725d0-125">tooinstall и импорта выбранных модулей AzureRM из профиля версии API-интерфейса, необходимо запустить командлет hello используйте AzureRMProfile с hello **модуль** параметр:</span><span class="sxs-lookup"><span data-stu-id="725d0-125">tooinstall and import selected AzureRM modules from an API version profile, run hello Use-AzureRMProfile cmdlet with hello **Module** parameter:</span></span>

```PowerShell
# Installs and imports hello compute, Storage and Network modules from hello specified API version profile into your current PowerShell session.
Use-AzureRmProfile -Profile 2017-03-09-profile -Module AzureRM.Compute, AzureRM.Storage, AzureRM.Network
```

## <a name="get-hello-installed-profiles"></a><span data-ttu-id="725d0-126">Получить профили hello установлен</span><span class="sxs-lookup"><span data-stu-id="725d0-126">Get hello installed profiles</span></span>

<span data-ttu-id="725d0-127">Используйте hello **Get AzureRmProfile** командлет tooget hello списка доступных профилей версии API:</span><span class="sxs-lookup"><span data-stu-id="725d0-127">Use hello **Get-AzureRmProfile** cmdlet tooget hello list of available API version profiles:</span></span> 

```PowerShell
# lists all API version profiles provided by hello AzureRM.BootStrapper module.
Get-AzureRmProfile -ListAvailable 

# lists hello API version profiles which are installed on your machine
Get-AzureRmProfile
```
## <a name="update-profiles"></a><span data-ttu-id="725d0-128">Обновить профили</span><span class="sxs-lookup"><span data-stu-id="725d0-128">Update profiles</span></span>

<span data-ttu-id="725d0-129">Используйте hello **AzureRmProfile обновление** модули hello tooupdate командлет в версии профиль toohello последняя версия API модулей, доступных в hello PSGallery.</span><span class="sxs-lookup"><span data-stu-id="725d0-129">Use hello **Update-AzureRmProfile** cmdlet tooupdate hello modules in an API version profile toohello latest version of modules that are available in hello PSGallery.</span></span> <span data-ttu-id="725d0-130">Рекомендуется tooalways запускать hello **AzureRmProfile обновление** командлета в новый tooavoid сеанса PowerShell конфликты при импорте модулей.</span><span class="sxs-lookup"><span data-stu-id="725d0-130">It's recommended tooalways run hello **Update-AzureRmProfile** cmdlet in a new PowerShell session tooavoid conflicts when importing modules.</span></span> <span data-ttu-id="725d0-131">Hello AzureRmProfile обновления выполняет hello следующие задачи:</span><span class="sxs-lookup"><span data-stu-id="725d0-131">hello Update-AzureRmProfile cmdlet runs hello following tasks:</span></span>

1. <span data-ttu-id="725d0-132">Проверяет, если последние версии hello модулей устанавливаются в заданный профиль версии API для текущей области hello hello.</span><span class="sxs-lookup"><span data-stu-id="725d0-132">Checks if hello latest versions of modules are installed in hello given API version profile for hello current scope.</span></span>  
2. <span data-ttu-id="725d0-133">Предлагает tooinstall, если они еще не установлены.</span><span class="sxs-lookup"><span data-stu-id="725d0-133">Prompts you tooinstall if they are not already installed.</span></span>  
3. <span data-ttu-id="725d0-134">Устанавливает и импортирует модули hello обновлены в текущем сеансе PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="725d0-134">Installs and imports hello updated modules into hello current PowerShell session.</span></span>  

```PowerShell
Update-AzureRmProfile -Profile 2017-03-09-profile
```

<span data-ttu-id="725d0-135">tooremove hello ранее установленные версии модулей hello перед обновлением toohello последнюю версию, с помощью командлета Update AzureRmProfile hello вместе с hello **- RemovePreviousVersions** параметр:</span><span class="sxs-lookup"><span data-stu-id="725d0-135">tooremove hello previously installed versions of hello modules before updating toohello latest available version, use hello Update-AzureRmProfile cmdlet along with hello **-RemovePreviousVersions** parameter:</span></span>

```PowerShell 
Update-AzureRmProfile -Profile 2017-03-09-profile -RemovePreviousVersions
```

<span data-ttu-id="725d0-136">Этот командлет запускается hello следующие задачи:</span><span class="sxs-lookup"><span data-stu-id="725d0-136">This cmdlet runs hello following tasks:</span></span>  

1. <span data-ttu-id="725d0-137">Проверяет, если последние версии hello модулей устанавливаются в заданный профиль версии API для текущей области hello hello.</span><span class="sxs-lookup"><span data-stu-id="725d0-137">Checks if hello latest versions of modules are installed in hello given API version profile for hello current scope.</span></span>  
2. <span data-ttu-id="725d0-138">Удаляет старые версии hello модулей из hello текущего профиля версии API и в текущем сеансе PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="725d0-138">Removes hello older versions of modules from hello current API version profile and in hello current PowerShell session.</span></span>  
4. <span data-ttu-id="725d0-139">предлагает tooinstall hello последнюю версию.</span><span class="sxs-lookup"><span data-stu-id="725d0-139">prompts you tooinstall hello latest version.</span></span>  
5. <span data-ttu-id="725d0-140">Устанавливает и импортирует модули hello обновлены в текущем сеансе PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="725d0-140">Installs and imports hello updated modules into hello current PowerShell session.</span></span>  
 
## <a name="uninstall-profiles"></a><span data-ttu-id="725d0-141">Удалять профили</span><span class="sxs-lookup"><span data-stu-id="725d0-141">Uninstall profiles</span></span>

<span data-ttu-id="725d0-142">Используйте hello **AzureRmProfile удаления** hello toouninstall командлет указанный профиль версии API.</span><span class="sxs-lookup"><span data-stu-id="725d0-142">Use hello **Uninstall-AzureRmProfile** cmdlet toouninstall hello specified API version profile.</span></span>

```PowerShell 
Uninstall-AzureRmProfile -Profile 2017-03-09-profile
```

## <a name="next-steps"></a><span data-ttu-id="725d0-143">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="725d0-143">Next steps</span></span>
* <span data-ttu-id="725d0-144">[Install PowerShell for Azure Stack](azure-stack-powershell-install.md) (Установка PowerShell для Azure Stack)</span><span class="sxs-lookup"><span data-stu-id="725d0-144">[Install PowerShell for Azure Stack](azure-stack-powershell-install.md)</span></span>
* [<span data-ttu-id="725d0-145">Настройка среды PowerShell hello Azure стека пользователя</span><span class="sxs-lookup"><span data-stu-id="725d0-145">Configure hello Azure Stack user's PowerShell environment</span></span>](azure-stack-powershell-configure-user.md)  
