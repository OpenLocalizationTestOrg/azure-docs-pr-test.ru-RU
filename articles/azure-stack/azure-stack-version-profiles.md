---
title: "С помощью профилей версии API стека Azure | Документы Microsoft"
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
ms.openlocfilehash: b70f8a392fdddade31383fc5cc9496cb39d73fd4
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="manage-api-version-profiles-in-azure-stack"></a><span data-ttu-id="d41c5-103">Управление профилями версии API в стек Azure</span><span class="sxs-lookup"><span data-stu-id="d41c5-103">Manage API version profiles in Azure Stack</span></span>

<span data-ttu-id="d41c5-104">Профили версии API-Интерфейс предоставляют способ управления версии различия между Azure и Azure стека.</span><span class="sxs-lookup"><span data-stu-id="d41c5-104">API version profiles provide a way to manage version differences between Azure and Azure Stack.</span></span> <span data-ttu-id="d41c5-105">Профиль версии API — это набор модулей AzureRM PowerShell для определенной версии API.</span><span class="sxs-lookup"><span data-stu-id="d41c5-105">An API version profile is a set of AzureRM PowerShell modules with specific API versions.</span></span> <span data-ttu-id="d41c5-106">Каждая облачная платформа имеет набор профилей версии поддерживаемых API.</span><span class="sxs-lookup"><span data-stu-id="d41c5-106">Each cloud platform has a set of supported API version profiles.</span></span> <span data-ttu-id="d41c5-107">Например, стека Azure поддерживает определенный профиль устаревшей версии, например **2017 г. 03-09-профиля**, и Azure поддерживает **последние** профиля версии API.</span><span class="sxs-lookup"><span data-stu-id="d41c5-107">For example, Azure Stack supports a specific dated profile version such as  **2017-03-09-profile**, and Azure supports the **latest** API version profile.</span></span> <span data-ttu-id="d41c5-108">При установке профиля установлены модули AzureRM PowerShell, которые соответствуют выбранному профилю.</span><span class="sxs-lookup"><span data-stu-id="d41c5-108">When you install a profile, the AzureRM PowerShell modules that correspond to the specified profile are installed.</span></span>

## <a name="install-the-powershell-module-required-to-use-api-version-profiles"></a><span data-ttu-id="d41c5-109">Установка модуля PowerShell, необходимые для использования профилей версия API</span><span class="sxs-lookup"><span data-stu-id="d41c5-109">Install the PowerShell module required to use API version profiles</span></span>

<span data-ttu-id="d41c5-110">**AzureRM.Bootstrapper** модуля, доступных в коллекции PowerShell предоставляет командлеты PowerShell, необходимых для работы с профилями версии API.</span><span class="sxs-lookup"><span data-stu-id="d41c5-110">The **AzureRM.Bootstrapper** module that is available through the PowerShell Gallery provides PowerShell cmdlets that are required to work with API version profiles.</span></span> <span data-ttu-id="d41c5-111">Чтобы установить модуль AzureRM.Bootstrapper, используйте следующий командлет:</span><span class="sxs-lookup"><span data-stu-id="d41c5-111">Use the following cmdlet to install the AzureRM.Bootstrapper module:</span></span>

```PowerShell
Install-Module -Name AzureRm.BootStrapper
```
<span data-ttu-id="d41c5-112">Модуль AzureRM.Bootstrapper — в режиме предварительного просмотра; Подробные сведения и функциональные возможности могут быть изменены.</span><span class="sxs-lookup"><span data-stu-id="d41c5-112">The AzureRM.Bootstrapper module is in preview; details and functionality are subject to change.</span></span> <span data-ttu-id="d41c5-113">Чтобы загрузить и установить последнюю версию этого модуля из коллекции PowerShell, выполните следующий командлет:</span><span class="sxs-lookup"><span data-stu-id="d41c5-113">To download and install the latest version of this module from the PowerShell Gallery, run the following cmdlet:</span></span>

```PowerShell
Update-Module -Name "AzureRm.BootStrapper"
```

## <a name="install-a-profile"></a><span data-ttu-id="d41c5-114">Установка профиля</span><span class="sxs-lookup"><span data-stu-id="d41c5-114">Install a profile</span></span>

<span data-ttu-id="d41c5-115">Используйте **установки AzureRmProfile** командлет с **2017 г. 03-09-профиля** профиля версии API для установки AzureRM модулями, необходимыми стеком Azure.</span><span class="sxs-lookup"><span data-stu-id="d41c5-115">Use the **Install-AzureRmProfile** cmdlet with the **2017-03-09-profile** API version profile to install the AzureRM modules required by Azure Stack.</span></span> <span data-ttu-id="d41c5-116">Обратите внимание, что с этим профилем версия API не установлены модули администратора облака Azure стека, и они должны устанавливаться отдельно, как указано в шаге 3 [Установка PowerShell для Azure стека](azure-stack-powershell-install.md) статьи.</span><span class="sxs-lookup"><span data-stu-id="d41c5-116">Note that the Azure Stack cloud administrator modules are not installed with this API version profile, and they should be installed separately as specified in the Step 3 of the [Install PowerShell for Azure Stack](azure-stack-powershell-install.md) article.</span></span>

```PowerShell 
Install-AzureRMProfile -Profile 2017-03-09-profile
```
## <a name="install-and-import-modules-in-a-profile"></a><span data-ttu-id="d41c5-117">Установить и импортировать модули в профиле</span><span class="sxs-lookup"><span data-stu-id="d41c5-117">Install and import modules in a profile</span></span>

<span data-ttu-id="d41c5-118">Используйте **AzureRmProfile используйте** командлет, чтобы установить и импортировать модули, связанные с профилем версии API.</span><span class="sxs-lookup"><span data-stu-id="d41c5-118">Use the **Use-AzureRmProfile** cmdlet to install and import modules that are associated with an API version profile.</span></span> <span data-ttu-id="d41c5-119">В сеансе PowerShell можно импортировать только один профиль версии API.</span><span class="sxs-lookup"><span data-stu-id="d41c5-119">You can import only one API version profile in a PowerShell session.</span></span> <span data-ttu-id="d41c5-120">Чтобы импортировать другой профиль версии API, необходимо открыть новый сеанс PowerShell.</span><span class="sxs-lookup"><span data-stu-id="d41c5-120">To import a different API version profile, you must open a new PowerShell session.</span></span> <span data-ttu-id="d41c5-121">Используйте AzureRMProfile выполняет следующие задачи:</span><span class="sxs-lookup"><span data-stu-id="d41c5-121">The Use-AzureRMProfile cmdlet runs the following tasks:</span></span>  
1. <span data-ttu-id="d41c5-122">Проверяет наличие модули PowerShell, связанные с конкретным профилем версии API в текущей области.</span><span class="sxs-lookup"><span data-stu-id="d41c5-122">Checks if the PowerShell modules associated with the specified API version profile are installed in the current scope.</span></span>  
2. <span data-ttu-id="d41c5-123">Загрузка и Установка модулей, если они еще не установлены.</span><span class="sxs-lookup"><span data-stu-id="d41c5-123">Downloads and installs the modules if they are not already installed.</span></span>   
3. <span data-ttu-id="d41c5-124">Импортирует модули в текущий сеанс PowerShell.</span><span class="sxs-lookup"><span data-stu-id="d41c5-124">Imports the modules into the current PowerShell session.</span></span> 

```PowerShell
# Installs and imports the specified API version profile into the current PowerShell session.
Use-AzureRmProfile -Profile 2017-03-09-profile -Scope CurrentUser

# Installs and imports the specified API version profile into the current PowerShell session without any prompts
Use-AzureRmProfile -Profile 2017-03-09-profile -Scope CurrentUser -Force
```

<span data-ttu-id="d41c5-125">Для установки и импорта выбранных модулей AzureRM из профиля версии API-Интерфейс, запустить командлет используйте AzureRMProfile с **модуль** параметр:</span><span class="sxs-lookup"><span data-stu-id="d41c5-125">To install and import selected AzureRM modules from an API version profile, run the Use-AzureRMProfile cmdlet with the **Module** parameter:</span></span>

```PowerShell
# Installs and imports the compute, Storage and Network modules from the specified API version profile into your current PowerShell session.
Use-AzureRmProfile -Profile 2017-03-09-profile -Module AzureRM.Compute, AzureRM.Storage, AzureRM.Network
```

## <a name="get-the-installed-profiles"></a><span data-ttu-id="d41c5-126">Получение установленных профилей</span><span class="sxs-lookup"><span data-stu-id="d41c5-126">Get the installed profiles</span></span>

<span data-ttu-id="d41c5-127">Используйте **Get AzureRmProfile** для получения списка доступных профилей версии API:</span><span class="sxs-lookup"><span data-stu-id="d41c5-127">Use the **Get-AzureRmProfile** cmdlet to get the list of available API version profiles:</span></span> 

```PowerShell
# lists all API version profiles provided by the AzureRM.BootStrapper module.
Get-AzureRmProfile -ListAvailable 

# lists the API version profiles which are installed on your machine
Get-AzureRmProfile
```
## <a name="update-profiles"></a><span data-ttu-id="d41c5-128">Обновить профили</span><span class="sxs-lookup"><span data-stu-id="d41c5-128">Update profiles</span></span>

<span data-ttu-id="d41c5-129">Используйте **AzureRmProfile обновление** командлет для обновления до последней версии модулей, доступных в PSGallery модули в профиле версии API.</span><span class="sxs-lookup"><span data-stu-id="d41c5-129">Use the **Update-AzureRmProfile** cmdlet to update the modules in an API version profile to the latest version of modules that are available in the PSGallery.</span></span> <span data-ttu-id="d41c5-130">Рекомендуется всегда запускать **AzureRmProfile обновление** командлет в сеансе PowerShell во избежание конфликтов при импорте модулей.</span><span class="sxs-lookup"><span data-stu-id="d41c5-130">It's recommended to always run the **Update-AzureRmProfile** cmdlet in a new PowerShell session to avoid conflicts when importing modules.</span></span> <span data-ttu-id="d41c5-131">Командлет Update-AzureRmProfile выполняет следующие задачи:</span><span class="sxs-lookup"><span data-stu-id="d41c5-131">The Update-AzureRmProfile cmdlet runs the following tasks:</span></span>

1. <span data-ttu-id="d41c5-132">Проверяет, если установлены последние версии модулей в заданного профиля версии API для текущей области.</span><span class="sxs-lookup"><span data-stu-id="d41c5-132">Checks if the latest versions of modules are installed in the given API version profile for the current scope.</span></span>  
2. <span data-ttu-id="d41c5-133">Предлагает установить, если они еще не установлены.</span><span class="sxs-lookup"><span data-stu-id="d41c5-133">Prompts you to install if they are not already installed.</span></span>  
3. <span data-ttu-id="d41c5-134">Устанавливает и импортирует обновленные модули в текущий сеанс PowerShell.</span><span class="sxs-lookup"><span data-stu-id="d41c5-134">Installs and imports the updated modules into the current PowerShell session.</span></span>  

```PowerShell
Update-AzureRmProfile -Profile 2017-03-09-profile
```

<span data-ttu-id="d41c5-135">Чтобы удалить ранее установленные модули перед обновлением до версии, с помощью командлета Update AzureRmProfile вместе с **- RemovePreviousVersions** параметр:</span><span class="sxs-lookup"><span data-stu-id="d41c5-135">To remove the previously installed versions of the modules before updating to the latest available version, use the Update-AzureRmProfile cmdlet along with the **-RemovePreviousVersions** parameter:</span></span>

```PowerShell 
Update-AzureRmProfile -Profile 2017-03-09-profile -RemovePreviousVersions
```

<span data-ttu-id="d41c5-136">Этот командлет выполняет следующие задачи:</span><span class="sxs-lookup"><span data-stu-id="d41c5-136">This cmdlet runs the following tasks:</span></span>  

1. <span data-ttu-id="d41c5-137">Проверяет, если установлены последние версии модулей в заданного профиля версии API для текущей области.</span><span class="sxs-lookup"><span data-stu-id="d41c5-137">Checks if the latest versions of modules are installed in the given API version profile for the current scope.</span></span>  
2. <span data-ttu-id="d41c5-138">Удаляет старые версии модули из текущего профиля версии API и в текущем сеансе PowerShell.</span><span class="sxs-lookup"><span data-stu-id="d41c5-138">Removes the older versions of modules from the current API version profile and in the current PowerShell session.</span></span>  
4. <span data-ttu-id="d41c5-139">выводит приглашение установить последнюю версию.</span><span class="sxs-lookup"><span data-stu-id="d41c5-139">prompts you to install the latest version.</span></span>  
5. <span data-ttu-id="d41c5-140">Устанавливает и импортирует обновленные модули в текущий сеанс PowerShell.</span><span class="sxs-lookup"><span data-stu-id="d41c5-140">Installs and imports the updated modules into the current PowerShell session.</span></span>  
 
## <a name="uninstall-profiles"></a><span data-ttu-id="d41c5-141">Удалять профили</span><span class="sxs-lookup"><span data-stu-id="d41c5-141">Uninstall profiles</span></span>

<span data-ttu-id="d41c5-142">Используйте **AzureRmProfile удаления** командлет для удаления указанного профиля версии API.</span><span class="sxs-lookup"><span data-stu-id="d41c5-142">Use the **Uninstall-AzureRmProfile** cmdlet to uninstall the specified API version profile.</span></span>

```PowerShell 
Uninstall-AzureRmProfile -Profile 2017-03-09-profile
```

## <a name="next-steps"></a><span data-ttu-id="d41c5-143">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="d41c5-143">Next steps</span></span>
* <span data-ttu-id="d41c5-144">[Install PowerShell for Azure Stack](azure-stack-powershell-install.md) (Установка PowerShell для Azure Stack)</span><span class="sxs-lookup"><span data-stu-id="d41c5-144">[Install PowerShell for Azure Stack](azure-stack-powershell-install.md)</span></span>
* [<span data-ttu-id="d41c5-145">Настройка среды PowerShell пользователя стек Azure</span><span class="sxs-lookup"><span data-stu-id="d41c5-145">Configure the Azure Stack user's PowerShell environment</span></span>](azure-stack-powershell-configure-user.md)  
