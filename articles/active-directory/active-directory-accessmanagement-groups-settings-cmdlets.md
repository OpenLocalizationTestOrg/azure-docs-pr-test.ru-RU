---
title: "Параметры группы aaaConfigure, с помощью командлетов Azure Active Directory | Документы Microsoft"
description: "Как управлять параметрами hello для групп с помощью командлетов Azure Active Directory"
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 9f2090e6-3af4-4f07-bbb2-1d18dae89b73
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: curtand
ms.reviewer: kairaz.contractor
ms.custom: it-pro;
ms.openlocfilehash: 46db49d9dec3eaa41c97ca74c57854189eddc16d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-cmdlets-for-configuring-group-settings"></a><span data-ttu-id="fd898-103">Настройка параметров групп с помощью командлетов Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="fd898-103">Azure Active Directory cmdlets for configuring group settings</span></span>

> [!IMPORTANT]
> <span data-ttu-id="fd898-104">Эти материалы относятся группы tooOffice 365.</span><span class="sxs-lookup"><span data-stu-id="fd898-104">This content applies only tooOffice 365 groups.</span></span> <span data-ttu-id="fd898-105">Дополнительные сведения о том, как задать tooallow группы безопасности пользователей toocreate, `Set-MSOLCompanySettings -UsersPermissionToCreateGroupsEnabled $True` как описано в [Set-MSOLCompanySettings](https://docs.microsoft.com/en-us/powershell/module/msonline/set-msolcompanysettings?view=azureadps-1.0).</span><span class="sxs-lookup"><span data-stu-id="fd898-105">For more information on how tooallow users toocreate Security groups, set `Set-MSOLCompanySettings -UsersPermissionToCreateGroupsEnabled $True` as described in [Set-MSOLCompanySettings](https://docs.microsoft.com/en-us/powershell/module/msonline/set-msolcompanysettings?view=azureadps-1.0).</span></span> 

<span data-ttu-id="fd898-106">Параметры групп Office 365 настраиваются с помощью объектов Settings и SettingsTemplate.</span><span class="sxs-lookup"><span data-stu-id="fd898-106">Office 365 Groups settings are configured using a Settings object and a SettingsTemplate object.</span></span> <span data-ttu-id="fd898-107">Изначально вы не видите все объекты параметров в вашем каталоге, так как ваш каталог настроен с параметрами по умолчанию hello.</span><span class="sxs-lookup"><span data-stu-id="fd898-107">Initially, you don't see any Settings objects in your directory, because your directory is configured with hello default settings.</span></span> <span data-ttu-id="fd898-108">параметры по умолчанию hello toochange, необходимо создать новый объект параметров с помощью параметров шаблона.</span><span class="sxs-lookup"><span data-stu-id="fd898-108">toochange hello default settings, you must create a new settings object using a settings template.</span></span> <span data-ttu-id="fd898-109">Шаблоны параметров определены корпорацией Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="fd898-109">Settings templates are defined by Microsoft.</span></span> <span data-ttu-id="fd898-110">Поддерживается несколько разных шаблонов параметров.</span><span class="sxs-lookup"><span data-stu-id="fd898-110">There are several different settings templates.</span></span> <span data-ttu-id="fd898-111">Параметры группы tooconfigure Office 365 для вашего каталога, используйте hello шаблона с именем «Group.Unified».</span><span class="sxs-lookup"><span data-stu-id="fd898-111">tooconfigure Office 365 group settings for your directory, you use hello template named "Group.Unified".</span></span> <span data-ttu-id="fd898-112">Параметры группы tooconfigure Office 365 на одну группу, используйте шаблон hello, с именем «Group.Unified.Guest».</span><span class="sxs-lookup"><span data-stu-id="fd898-112">tooconfigure Office 365 group settings on a single group, use hello template named "Group.Unified.Guest".</span></span> <span data-ttu-id="fd898-113">Этот шаблон является группа tooan Office 365 используется toomanage гостевого доступа.</span><span class="sxs-lookup"><span data-stu-id="fd898-113">This template is used toomanage guest access tooan Office 365 group.</span></span> 

<span data-ttu-id="fd898-114">командлеты Hello являются частью модуля hello Azure Active Directory PowerShell V2.</span><span class="sxs-lookup"><span data-stu-id="fd898-114">hello cmdlets are part of hello Azure Active Directory PowerShell V2 module.</span></span> <span data-ttu-id="fd898-115">Инструкции как toodownload и установки hello модуля на компьютере, в статье hello [Azure Active Directory PowerShell версии 2](https://docs.microsoft.com/powershell/azuread/).</span><span class="sxs-lookup"><span data-stu-id="fd898-115">For instructions how toodownload and install hello module on your computer, see hello article [Azure Active Directory PowerShell Version 2](https://docs.microsoft.com/powershell/azuread/).</span></span> <span data-ttu-id="fd898-116">Вы можете установить выпуск версии 2 hello hello модуля из [коллекции PowerShell hello](https://www.powershellgallery.com/packages/AzureAD/).</span><span class="sxs-lookup"><span data-stu-id="fd898-116">You can install hello version 2 release of hello module from [hello PowerShell gallery](https://www.powershellgallery.com/packages/AzureAD/).</span></span>

## <a name="retrieve-a-specific-settings-value"></a><span data-ttu-id="fd898-117">Получение определенного значения параметра</span><span class="sxs-lookup"><span data-stu-id="fd898-117">Retrieve a specific settings value</span></span>
<span data-ttu-id="fd898-118">Если известно имя hello hello параметр tooretrieve, можно использовать hello ниже текущего значения параметров командлета tooretrieve hello.</span><span class="sxs-lookup"><span data-stu-id="fd898-118">If you know hello name of hello setting you want tooretrieve, you can use hello below cmdlet tooretrieve hello current settings value.</span></span> <span data-ttu-id="fd898-119">В этом примере извлекаются hello значение для параметра с именем «UsageGuidelinesUrl.»</span><span class="sxs-lookup"><span data-stu-id="fd898-119">In this example, we're retrieving hello value for a setting named "UsageGuidelinesUrl."</span></span> <span data-ttu-id="fd898-120">Дополнительные сведения о параметрах каталога и их именах приводятся далее в этой статье.</span><span class="sxs-lookup"><span data-stu-id="fd898-120">You can read more about directory settings and their names further down in this article.</span></span>

```powershell
(Get-AzureADDirectorySetting).Values | Where-Object -Property Name -Value UsageGuidelinesUrl -EQ
```

## <a name="create-settings-at-hello-directory-level"></a><span data-ttu-id="fd898-121">Создание параметров на уровне папки hello</span><span class="sxs-lookup"><span data-stu-id="fd898-121">Create settings at hello directory level</span></span>
<span data-ttu-id="fd898-122">Эти шаги создают параметры на уровне папки применимые группы Office 365 tooall (единой группы) в каталоге hello.</span><span class="sxs-lookup"><span data-stu-id="fd898-122">These steps create settings at directory level, which apply tooall Office 365 groups (Unified groups) in hello directory.</span></span>

1. <span data-ttu-id="fd898-123">В hello DirectorySettings командлеты необходимо указать идентификатор hello hello требуется toouse SettingsTemplate.</span><span class="sxs-lookup"><span data-stu-id="fd898-123">In hello DirectorySettings cmdlets, you must specify hello ID of hello SettingsTemplate you want toouse.</span></span> <span data-ttu-id="fd898-124">Если вы не знаете этот идентификатор, этот командлет возвращает список всех параметров шаблонов hello:</span><span class="sxs-lookup"><span data-stu-id="fd898-124">If you do not know this ID, this cmdlet returns hello list of all settings templates:</span></span>
  
  ```
  PS C:> Get-AzureADDirectorySettingTemplate
  ```
  <span data-ttu-id="fd898-125">Этот командлет отображает все шаблоны, которые доступны.</span><span class="sxs-lookup"><span data-stu-id="fd898-125">This cmdlet call returns all templates that are available:</span></span>
  
  ```
  Id                                   DisplayName         Description
  --                                   -----------         -----------
  62375ab9-6b52-47ed-826b-58e47e0e304b Group.Unified       ...
  08d542b9-071f-4e16-94b0-74abb372e3d9 Group.Unified.Guest Settings for a specific Unified Group
  16933506-8a8d-4f0d-ad58-e1db05a5b929 Company.BuiltIn     Setting templates define hello different settings that can be used for hello associ...
  4bc7f740-180e-4586-adb6-38b2e9024e6b Application...
  898f1161-d651-43d1-805c-3b0b388a9fc2 Custom Policy       Settings ...
  5cf42378-d67d-4f36-ba46-e8b86229381d Password Rule       Settings ...
  ```
2. <span data-ttu-id="fd898-126">tooadd URL-адрес правила использования, сначала необходимо tooget hello SettingsTemplate объект, который определяет значение URL-адреса направляющих hello использования; то есть hello Group.Unified шаблона:</span><span class="sxs-lookup"><span data-stu-id="fd898-126">tooadd a usage guideline URL, first you need tooget hello SettingsTemplate object that defines hello usage guideline URL value; that is, hello Group.Unified template:</span></span>
  
  ```
  $Template = Get-AzureADDirectorySettingTemplate -Id 62375ab9-6b52-47ed-826b-58e47e0e304b
  ```
3. <span data-ttu-id="fd898-127">Затем создайте новый объект параметров на основе этого шаблона:</span><span class="sxs-lookup"><span data-stu-id="fd898-127">Next, create a new settings object based on that template:</span></span>
  
  ```
  $Setting = $template.CreateDirectorySetting()
  ```  
4. <span data-ttu-id="fd898-128">Обновите значение направляющих hello использования:</span><span class="sxs-lookup"><span data-stu-id="fd898-128">Then update hello usage guideline value:</span></span>
  
  ```
  $setting["UsageGuidelinesUrl"] = "<https://guideline.com>"
  ```  
5. <span data-ttu-id="fd898-129">Наконец примените параметры hello:</span><span class="sxs-lookup"><span data-stu-id="fd898-129">Finally, apply hello settings:</span></span>
  
  ```
  New-AzureADDirectorySetting -DirectorySetting $setting
  ```

<span data-ttu-id="fd898-130">После успешного завершения hello командлет возвращает идентификатор hello объекта hello новые параметры:</span><span class="sxs-lookup"><span data-stu-id="fd898-130">Upon successful completion, hello cmdlet returns hello ID of hello new settings object:</span></span>
  ```
  Id                                   DisplayName TemplateId                           Values
  --                                   ----------- ----------                           ------
  c391b57d-5783-4c53-9236-cefb5c6ef323             62375ab9-6b52-47ed-826b-58e47e0e304b {class SettingValue {...
  ```
<span data-ttu-id="fd898-131">Ниже приведены параметры hello, определенные в Group.Unified SettingsTemplate hello.</span><span class="sxs-lookup"><span data-stu-id="fd898-131">Here are hello settings defined in hello Group.Unified SettingsTemplate.</span></span>

| <span data-ttu-id="fd898-132">**Параметр**</span><span class="sxs-lookup"><span data-stu-id="fd898-132">**Setting**</span></span> | <span data-ttu-id="fd898-133">**Описание**</span><span class="sxs-lookup"><span data-stu-id="fd898-133">**Description**</span></span> |
| --- | --- |
|  <ul><li><span data-ttu-id="fd898-134">EnableGroupCreation</span><span class="sxs-lookup"><span data-stu-id="fd898-134">EnableGroupCreation</span></span><li><span data-ttu-id="fd898-135">Тип: логический</span><span class="sxs-lookup"><span data-stu-id="fd898-135">Type: Boolean</span></span><li><span data-ttu-id="fd898-136">значение по умолчанию: True</span><span class="sxs-lookup"><span data-stu-id="fd898-136">Default: True</span></span> |<span data-ttu-id="fd898-137">Hello флаг, указывающий, разрешено ли создание единой группы в каталоге hello.</span><span class="sxs-lookup"><span data-stu-id="fd898-137">hello flag indicating whether Unified Group creation is allowed in hello directory.</span></span> |
|  <ul><li><span data-ttu-id="fd898-138">GroupCreationAllowedGroupId</span><span class="sxs-lookup"><span data-stu-id="fd898-138">GroupCreationAllowedGroupId</span></span><li><span data-ttu-id="fd898-139">Тип: строка</span><span class="sxs-lookup"><span data-stu-id="fd898-139">Type: String</span></span><li><span data-ttu-id="fd898-140">Default: “”</span><span class="sxs-lookup"><span data-stu-id="fd898-140">Default: “”</span></span> |<span data-ttu-id="fd898-141">Идентификатор GUID группы безопасности hello, какие hello участники могут toocreate объединенные группы, даже когда EnableGroupCreation == false.</span><span class="sxs-lookup"><span data-stu-id="fd898-141">GUID of hello security group for which hello members are allowed toocreate Unified Groups even when EnableGroupCreation == false.</span></span> |
|  <ul><li><span data-ttu-id="fd898-142">UsageGuidelinesUrl</span><span class="sxs-lookup"><span data-stu-id="fd898-142">UsageGuidelinesUrl</span></span><li><span data-ttu-id="fd898-143">Тип: строка</span><span class="sxs-lookup"><span data-stu-id="fd898-143">Type: String</span></span><li><span data-ttu-id="fd898-144">Default: “”</span><span class="sxs-lookup"><span data-stu-id="fd898-144">Default: “”</span></span> |<span data-ttu-id="fd898-145">Ссылка toohello правила использования группы.</span><span class="sxs-lookup"><span data-stu-id="fd898-145">A link toohello Group Usage Guidelines.</span></span> |
|  <ul><li><span data-ttu-id="fd898-146">ClassificationDescriptions</span><span class="sxs-lookup"><span data-stu-id="fd898-146">ClassificationDescriptions</span></span><li><span data-ttu-id="fd898-147">Тип: строка</span><span class="sxs-lookup"><span data-stu-id="fd898-147">Type: String</span></span><li><span data-ttu-id="fd898-148">Default: “”</span><span class="sxs-lookup"><span data-stu-id="fd898-148">Default: “”</span></span> | <span data-ttu-id="fd898-149">Разделенный запятыми список описаний классификаций.</span><span class="sxs-lookup"><span data-stu-id="fd898-149">A comma-delimited list of classification descriptions.</span></span> |
|  <ul><li><span data-ttu-id="fd898-150">DefaultClassification</span><span class="sxs-lookup"><span data-stu-id="fd898-150">DefaultClassification</span></span><li><span data-ttu-id="fd898-151">Тип: строка</span><span class="sxs-lookup"><span data-stu-id="fd898-151">Type: String</span></span><li><span data-ttu-id="fd898-152">Default: “”</span><span class="sxs-lookup"><span data-stu-id="fd898-152">Default: “”</span></span> | <span data-ttu-id="fd898-153">Классификация Hello, toobe использовать в качестве hello классификации по умолчанию для группы, если ничего не было указано.</span><span class="sxs-lookup"><span data-stu-id="fd898-153">hello classification that is toobe used as hello default classification for a group if none was specified.</span></span>|
|  <ul><li><span data-ttu-id="fd898-154">PrefixSuffixNamingRequirement</span><span class="sxs-lookup"><span data-stu-id="fd898-154">PrefixSuffixNamingRequirement</span></span><li><span data-ttu-id="fd898-155">Тип: строка</span><span class="sxs-lookup"><span data-stu-id="fd898-155">Type: String</span></span><li><span data-ttu-id="fd898-156">Default: “”</span><span class="sxs-lookup"><span data-stu-id="fd898-156">Default: “”</span></span> |<span data-ttu-id="fd898-157">Еще не реализован.</span><span class="sxs-lookup"><span data-stu-id="fd898-157">Not implemented yet</span></span>
|  <ul><li><span data-ttu-id="fd898-158">AllowGuestsToBeGroupOwner</span><span class="sxs-lookup"><span data-stu-id="fd898-158">AllowGuestsToBeGroupOwner</span></span><li><span data-ttu-id="fd898-159">Тип: логический</span><span class="sxs-lookup"><span data-stu-id="fd898-159">Type: Boolean</span></span><li><span data-ttu-id="fd898-160">значение по умолчанию: False</span><span class="sxs-lookup"><span data-stu-id="fd898-160">Default: False</span></span> | <span data-ttu-id="fd898-161">Логическое значение, указывающее, может ли гостевой пользователь быть владельцем группы.</span><span class="sxs-lookup"><span data-stu-id="fd898-161">Boolean indicating whether or not a guest user can be an owner of groups.</span></span> |
|  <ul><li><span data-ttu-id="fd898-162">AllowGuestsToAccessGroups</span><span class="sxs-lookup"><span data-stu-id="fd898-162">AllowGuestsToAccessGroups</span></span><li><span data-ttu-id="fd898-163">Тип: логический</span><span class="sxs-lookup"><span data-stu-id="fd898-163">Type: Boolean</span></span><li><span data-ttu-id="fd898-164">значение по умолчанию: True</span><span class="sxs-lookup"><span data-stu-id="fd898-164">Default: True</span></span> | <span data-ttu-id="fd898-165">Логическое значение, указывающее, можно ли существование пользователя guest имеют содержимое группы tooUnified доступа.</span><span class="sxs-lookup"><span data-stu-id="fd898-165">Boolean indicating whether or not a guest user can have access tooUnified groups' content.</span></span> |
|  <ul><li><span data-ttu-id="fd898-166">GuestUsageGuidelinesUrl</span><span class="sxs-lookup"><span data-stu-id="fd898-166">GuestUsageGuidelinesUrl</span></span><li><span data-ttu-id="fd898-167">Тип: строка</span><span class="sxs-lookup"><span data-stu-id="fd898-167">Type: String</span></span><li><span data-ttu-id="fd898-168">Default: “”</span><span class="sxs-lookup"><span data-stu-id="fd898-168">Default: “”</span></span> | <span data-ttu-id="fd898-169">URL-адрес Hello toohello ссылку гостевой рекомендации по использованию.</span><span class="sxs-lookup"><span data-stu-id="fd898-169">hello url of a link toohello guest usage guidelines.</span></span> |
|  <ul><li><span data-ttu-id="fd898-170">AllowToAddGuests</span><span class="sxs-lookup"><span data-stu-id="fd898-170">AllowToAddGuests</span></span><li><span data-ttu-id="fd898-171">Тип: логический</span><span class="sxs-lookup"><span data-stu-id="fd898-171">Type: Boolean</span></span><li><span data-ttu-id="fd898-172">значение по умолчанию: True</span><span class="sxs-lookup"><span data-stu-id="fd898-172">Default: True</span></span> | <span data-ttu-id="fd898-173">Логическое значение, указывающее, доступен ли каталог toothis разрешенных tooadd гостей.</span><span class="sxs-lookup"><span data-stu-id="fd898-173">A boolean indicating whether or not is allowed tooadd guests toothis directory.</span></span>|
|  <ul><li><span data-ttu-id="fd898-174">ClassificationList</span><span class="sxs-lookup"><span data-stu-id="fd898-174">ClassificationList</span></span><li><span data-ttu-id="fd898-175">Тип: строка</span><span class="sxs-lookup"><span data-stu-id="fd898-175">Type: String</span></span><li><span data-ttu-id="fd898-176">Default: “”</span><span class="sxs-lookup"><span data-stu-id="fd898-176">Default: “”</span></span> |<span data-ttu-id="fd898-177">Список с разделителями запятыми допустимого значения, которые может быть применен tooUnified групп.</span><span class="sxs-lookup"><span data-stu-id="fd898-177">A comma-delimited list of valid classification values that can be applied tooUnified Groups.</span></span> |
|  <ul><li><span data-ttu-id="fd898-178">EnableGroupCreation</span><span class="sxs-lookup"><span data-stu-id="fd898-178">EnableGroupCreation</span></span><li><span data-ttu-id="fd898-179">Тип: логический</span><span class="sxs-lookup"><span data-stu-id="fd898-179">Type: Boolean</span></span><li><span data-ttu-id="fd898-180">значение по умолчанию: True</span><span class="sxs-lookup"><span data-stu-id="fd898-180">Default: True</span></span> | <span data-ttu-id="fd898-181">Логическое значение, указывающее, могут ли пользователи без прав администратора создавать единые группы.</span><span class="sxs-lookup"><span data-stu-id="fd898-181">A boolean indicating whether or not non-admin users can create new Unified groups.</span></span> |


## <a name="read-settings-at-hello-directory-level"></a><span data-ttu-id="fd898-182">Чтение параметров на уровне папки hello</span><span class="sxs-lookup"><span data-stu-id="fd898-182">Read settings at hello directory level</span></span>
<span data-ttu-id="fd898-183">Эти шаги чтение параметров на уровне папки, которые применены tooall Office групп в каталоге hello.</span><span class="sxs-lookup"><span data-stu-id="fd898-183">These steps read settings at directory level, which apply tooall Office groups in hello directory.</span></span>

1. <span data-ttu-id="fd898-184">Чтение всех существующих параметров каталога:</span><span class="sxs-lookup"><span data-stu-id="fd898-184">Read all existing directory settings:</span></span>
  ```
  Get-AzureADDirectorySetting -All $True
  ```
  <span data-ttu-id="fd898-185">Этот командлет возвращает список всех параметров каталога:</span><span class="sxs-lookup"><span data-stu-id="fd898-185">This cmdlet returns a list of all directory settings:</span></span>
  ```
  Id                                   DisplayName   TemplateId                           Values
  --                                   -----------   ----------                           ------
  c391b57d-5783-4c53-9236-cefb5c6ef323 Group.Unified 62375ab9-6b52-47ed-826b-58e47e0e304b {class SettingValue {...
  ```

2. <span data-ttu-id="fd898-186">Чтение всех параметров определенной группы:</span><span class="sxs-lookup"><span data-stu-id="fd898-186">Read all settings for a specific group:</span></span>
  ```
  Get-AzureADObjectSetting -TargetObjectId ab6a3887-776a-4db7-9da4-ea2b0d63c504 -TargetType Groups
  ```

3. <span data-ttu-id="fd898-187">Чтение всех значений параметров каталога из объекта Settings конкретного каталога по его идентификатору GUID.</span><span class="sxs-lookup"><span data-stu-id="fd898-187">Read all directory settings values of a specific directory settings object, using Settings Id GUID:</span></span>
  ```
  (Get-AzureADDirectorySetting -Id c391b57d-5783-4c53-9236-cefb5c6ef323).values
  ```
  <span data-ttu-id="fd898-188">Этот командлет возвращает hello имена и значения в этом объекте параметры для этой конкретной группы:</span><span class="sxs-lookup"><span data-stu-id="fd898-188">This cmdlet returns hello names and values in this settings object for this specific group:</span></span>
  ```
  Name                          Value
  ----                          -----
  ClassificationDescriptions
  DefaultClassification
  PrefixSuffixNamingRequirement
  AllowGuestsToBeGroupOwner     False 
  AllowGuestsToAccessGroups     True
  GuestUsageGuidelinesUrl
  GroupCreationAllowedGroupId
  AllowToAddGuests              True
  UsageGuidelinesUrl            <https://guideline.com>
  ClassificationList
  EnableGroupCreation           True
  ```

## <a name="update-settings-for-a-specific-group"></a><span data-ttu-id="fd898-189">Обновление параметров определенной группы</span><span class="sxs-lookup"><span data-stu-id="fd898-189">Update settings for a specific group</span></span>

1. <span data-ttu-id="fd898-190">Поиск hello параметры шаблона с именем «Groups.Unified.Guest»</span><span class="sxs-lookup"><span data-stu-id="fd898-190">Search for hello settings template named "Groups.Unified.Guest"</span></span>
  ```
  Get-AzureADDirectorySettingTemplate
  
  Id                                   DisplayName            Description
  --                                   -----------            -----------
  62375ab9-6b52-47ed-826b-58e47e0e304b Group.Unified          ...
  08d542b9-071f-4e16-94b0-74abb372e3d9 Group.Unified.Guest    Settings for a specific Unified Group
  4bc7f740-180e-4586-adb6-38b2e9024e6b Application            ...
  898f1161-d651-43d1-805c-3b0b388a9fc2 Custom Policy Settings ...
  5cf42378-d67d-4f36-ba46-e8b86229381d Password Rule Settings ...
  ```
2. <span data-ttu-id="fd898-191">Получите hello объекта шаблона для шаблона Groups.Unified.Guest hello:</span><span class="sxs-lookup"><span data-stu-id="fd898-191">Retrieve hello template object for hello Groups.Unified.Guest template:</span></span>
  ```
  $Template = Get-AzureADDirectorySettingTemplate -Id 08d542b9-071f-4e16-94b0-74abb372e3d9
  ```
3. <span data-ttu-id="fd898-192">Создание объекта параметров из шаблона hello:</span><span class="sxs-lookup"><span data-stu-id="fd898-192">Create a new settings object from hello template:</span></span>
  ```
  $Setting = $Template.CreateDirectorySetting()
  ```

4. <span data-ttu-id="fd898-193">Задайте значение toohello требуется параметр hello:</span><span class="sxs-lookup"><span data-stu-id="fd898-193">Set hello setting toohello required value:</span></span>
  ```
  $Setting["AllowToAddGuests"]=$False
  ```
5. <span data-ttu-id="fd898-194">Создайте новый параметр hello для hello нужную группу в каталоге hello:</span><span class="sxs-lookup"><span data-stu-id="fd898-194">Create hello new setting for hello required group in hello directory:</span></span>
  ```
  New-AzureADObjectSetting -TargetType Groups -TargetObjectId ab6a3887-776a-4db7-9da4-ea2b0d63c504 -DirectorySetting $Setting
  
  Id                                   DisplayName TemplateId                           Values
  --                                   ----------- ----------                           ------
  25651479-a26e-4181-afce-ce24111b2cb5             08d542b9-071f-4e16-94b0-74abb372e3d9 {class SettingValue {...
  ```

## <a name="update-settings-at-hello-directory-level"></a><span data-ttu-id="fd898-195">Обновить параметры на уровне папки hello</span><span class="sxs-lookup"><span data-stu-id="fd898-195">Update settings at hello directory level</span></span>

<span data-ttu-id="fd898-196">Эти действия обновления параметров на уровне папки, которые применены tooall единой группы в каталоге hello.</span><span class="sxs-lookup"><span data-stu-id="fd898-196">These steps update settings at directory level, which apply tooall Unified groups in hello directory.</span></span> <span data-ttu-id="fd898-197">В этих примерах предполагается, что в каталоге уже существует объект Settings.</span><span class="sxs-lookup"><span data-stu-id="fd898-197">These examples assume there is already a Settings object in your directory.</span></span>

1. <span data-ttu-id="fd898-198">Найти существующий объект параметров hello:</span><span class="sxs-lookup"><span data-stu-id="fd898-198">Find hello existing Settings object:</span></span>
  ```
  Get-AzureADDirectorySetting | Where-object -Property Displayname -Value "Group.Unified" -EQ
  
  Id                                   DisplayName   TemplateId                           Values
  --                                   -----------   ----------                           ------
  c391b57d-5783-4c53-9236-cefb5c6ef323 Group.Unified 62375ab9-6b52-47ed-826b-58e47e0e304b {class SettingValue {...
  
  $setting = Get-AzureADDirectorySetting –Id c391b57d-5783-4c53-9236-cefb5c6ef323
  ```
2. <span data-ttu-id="fd898-199">Обновите значение hello:</span><span class="sxs-lookup"><span data-stu-id="fd898-199">Update hello value:</span></span>
  
  ```
  $Setting["AllowToAddGuests"] = "false"
  ```
3. <span data-ttu-id="fd898-200">Обновление параметра hello:</span><span class="sxs-lookup"><span data-stu-id="fd898-200">Update hello setting:</span></span>
  
  ```
  Set-AzureADDirectorySetting -Id c391b57d-5783-4c53-9236-cefb5c6ef323 -DirectorySetting $Setting
  ```

## <a name="remove-settings-at-hello-directory-level"></a><span data-ttu-id="fd898-201">Удалить параметры на уровне папки hello</span><span class="sxs-lookup"><span data-stu-id="fd898-201">Remove settings at hello directory level</span></span>
<span data-ttu-id="fd898-202">Этот шаг удаляет параметры на уровне папки, применяемые tooall Office групп в каталоге hello.</span><span class="sxs-lookup"><span data-stu-id="fd898-202">This step removes settings at directory level, which apply tooall Office groups in hello directory.</span></span>
  ```
  Remove-AzureADDirectorySetting –Id c391b57d-5783-4c53-9236-cefb5c6ef323c
  ```

## <a name="cmdlet-syntax-reference"></a><span data-ttu-id="fd898-203">Справочник по синтаксису командлетов</span><span class="sxs-lookup"><span data-stu-id="fd898-203">Cmdlet syntax reference</span></span>
<span data-ttu-id="fd898-204">Дополнительную документацию по PowerShell Azure Active Directory см. в разделе [Azure Active Directory Cmdlets](/powershell/azure/install-adv2?view=azureadps-2.0) (Командлеты Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="fd898-204">You can find more Azure Active Directory PowerShell documentation at [Azure Active Directory Cmdlets](/powershell/azure/install-adv2?view=azureadps-2.0).</span></span>

## <a name="additional-reading"></a><span data-ttu-id="fd898-205">Дополнительные материалы</span><span class="sxs-lookup"><span data-stu-id="fd898-205">Additional reading</span></span>

* [<span data-ttu-id="fd898-206">Управление tooresources доступ с помощью групп Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="fd898-206">Managing access tooresources with Azure Active Directory groups</span></span>](active-directory-manage-groups.md)
* [<span data-ttu-id="fd898-207">Интеграция локальных удостоверений с Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="fd898-207">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)
