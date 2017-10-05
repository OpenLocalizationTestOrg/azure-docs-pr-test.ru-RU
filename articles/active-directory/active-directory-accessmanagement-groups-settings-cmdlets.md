---
title: "Настройка параметров группы с помощью командлетов Azure Active Directory | Документация Майкрософт"
description: "Управление параметрами групп с помощью командлетов Azure Active Directory."
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
ms.openlocfilehash: 0d89f12955b90c7e1a8301b7c3a1a92e7f62d085
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="azure-active-directory-cmdlets-for-configuring-group-settings"></a><span data-ttu-id="51ef3-103">Настройка параметров групп с помощью командлетов Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="51ef3-103">Azure Active Directory cmdlets for configuring group settings</span></span>

> [!IMPORTANT]
> <span data-ttu-id="51ef3-104">Это содержимое применяется только к группам Office 365.</span><span class="sxs-lookup"><span data-stu-id="51ef3-104">This content applies only to Office 365 groups.</span></span> <span data-ttu-id="51ef3-105">Чтобы узнать, как разрешить пользователям создавать группы безопасности, установите `Set-MSOLCompanySettings -UsersPermissionToCreateGroupsEnabled $True`, как описано в статье [Set-MSOLCompanySettings](https://docs.microsoft.com/en-us/powershell/module/msonline/set-msolcompanysettings?view=azureadps-1.0).</span><span class="sxs-lookup"><span data-stu-id="51ef3-105">For more information on how to allow users to create Security groups, set `Set-MSOLCompanySettings -UsersPermissionToCreateGroupsEnabled $True` as described in [Set-MSOLCompanySettings](https://docs.microsoft.com/en-us/powershell/module/msonline/set-msolcompanysettings?view=azureadps-1.0).</span></span> 

<span data-ttu-id="51ef3-106">Параметры групп Office 365 настраиваются с помощью объектов Settings и SettingsTemplate.</span><span class="sxs-lookup"><span data-stu-id="51ef3-106">Office 365 Groups settings are configured using a Settings object and a SettingsTemplate object.</span></span> <span data-ttu-id="51ef3-107">Изначально в каталоге не отображаются все объекты параметров, так как он настроен с параметрами по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="51ef3-107">Initially, you don't see any Settings objects in your directory, because your directory is configured with the default settings.</span></span> <span data-ttu-id="51ef3-108">Чтобы изменить параметры по умолчанию, необходимо с помощью шаблона параметров создать объект параметров.</span><span class="sxs-lookup"><span data-stu-id="51ef3-108">To change the default settings, you must create a new settings object using a settings template.</span></span> <span data-ttu-id="51ef3-109">Шаблоны параметров определены корпорацией Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="51ef3-109">Settings templates are defined by Microsoft.</span></span> <span data-ttu-id="51ef3-110">Поддерживается несколько разных шаблонов параметров.</span><span class="sxs-lookup"><span data-stu-id="51ef3-110">There are several different settings templates.</span></span> <span data-ttu-id="51ef3-111">Чтобы настроить параметры группы Office 365 для каталога, используйте шаблон Group.Unified.</span><span class="sxs-lookup"><span data-stu-id="51ef3-111">To configure Office 365 group settings for your directory, you use the template named "Group.Unified".</span></span> <span data-ttu-id="51ef3-112">Для настройки параметров отдельной группы Office 365 используйте шаблон Group.Unified.Guest.</span><span class="sxs-lookup"><span data-stu-id="51ef3-112">To configure Office 365 group settings on a single group, use the template named "Group.Unified.Guest".</span></span> <span data-ttu-id="51ef3-113">Этот шаблон используется для управления гостевым доступом к группе Office 365.</span><span class="sxs-lookup"><span data-stu-id="51ef3-113">This template is used to manage guest access to an Office 365 group.</span></span> 

<span data-ttu-id="51ef3-114">Командлеты являются частью модуля PowerShell версии 2 для Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="51ef3-114">The cmdlets are part of the Azure Active Directory PowerShell V2 module.</span></span> <span data-ttu-id="51ef3-115">Дополнительные сведения о скачивании и установке модуля на компьютер см. в статье [PowerShell версии 2 для Azure Active Directory](https://docs.microsoft.com/powershell/azuread/).</span><span class="sxs-lookup"><span data-stu-id="51ef3-115">For instructions how to download and install the module on your computer, see the article [Azure Active Directory PowerShell Version 2](https://docs.microsoft.com/powershell/azuread/).</span></span> <span data-ttu-id="51ef3-116">Вы можете установить выпуск версии 2 модуля [из коллекции PowerShell](https://www.powershellgallery.com/packages/AzureAD/).</span><span class="sxs-lookup"><span data-stu-id="51ef3-116">You can install the version 2 release of the module from [the PowerShell gallery](https://www.powershellgallery.com/packages/AzureAD/).</span></span>

## <a name="retrieve-a-specific-settings-value"></a><span data-ttu-id="51ef3-117">Получение определенного значения параметра</span><span class="sxs-lookup"><span data-stu-id="51ef3-117">Retrieve a specific settings value</span></span>
<span data-ttu-id="51ef3-118">Если вам известно имя параметра, которое необходимо получить, можно использовать приведенный ниже командлет.</span><span class="sxs-lookup"><span data-stu-id="51ef3-118">If you know the name of the setting you want to retrieve, you can use the below cmdlet to retrieve the current settings value.</span></span> <span data-ttu-id="51ef3-119">В этом примере показано получение значения для параметра с именем UsageGuidelinesUrl.</span><span class="sxs-lookup"><span data-stu-id="51ef3-119">In this example, we're retrieving the value for a setting named "UsageGuidelinesUrl."</span></span> <span data-ttu-id="51ef3-120">Дополнительные сведения о параметрах каталога и их именах приводятся далее в этой статье.</span><span class="sxs-lookup"><span data-stu-id="51ef3-120">You can read more about directory settings and their names further down in this article.</span></span>

```powershell
(Get-AzureADDirectorySetting).Values | Where-Object -Property Name -Value UsageGuidelinesUrl -EQ
```

## <a name="create-settings-at-the-directory-level"></a><span data-ttu-id="51ef3-121">Создание параметров на уровне каталога</span><span class="sxs-lookup"><span data-stu-id="51ef3-121">Create settings at the directory level</span></span>
<span data-ttu-id="51ef3-122">Далее приведены действия, необходимые для создания параметров на уровне каталога, которые применяются ко всем группам Office 365 в каталоге.</span><span class="sxs-lookup"><span data-stu-id="51ef3-122">These steps create settings at directory level, which apply to all Office 365 groups (Unified groups) in the directory.</span></span>

1. <span data-ttu-id="51ef3-123">В командлетах DirectorySettings необходимо указать идентификатор объекта SettingsTemplate, который вы хотите использовать.</span><span class="sxs-lookup"><span data-stu-id="51ef3-123">In the DirectorySettings cmdlets, you must specify the ID of the SettingsTemplate you want to use.</span></span> <span data-ttu-id="51ef3-124">Если он вам неизвестен, выполните приведенный ниже командлет, чтобы отобразить все шаблоны параметров.</span><span class="sxs-lookup"><span data-stu-id="51ef3-124">If you do not know this ID, this cmdlet returns the list of all settings templates:</span></span>
  
  ```
  PS C:> Get-AzureADDirectorySettingTemplate
  ```
  <span data-ttu-id="51ef3-125">Этот командлет отображает все шаблоны, которые доступны.</span><span class="sxs-lookup"><span data-stu-id="51ef3-125">This cmdlet call returns all templates that are available:</span></span>
  
  ```
  Id                                   DisplayName         Description
  --                                   -----------         -----------
  62375ab9-6b52-47ed-826b-58e47e0e304b Group.Unified       ...
  08d542b9-071f-4e16-94b0-74abb372e3d9 Group.Unified.Guest Settings for a specific Unified Group
  16933506-8a8d-4f0d-ad58-e1db05a5b929 Company.BuiltIn     Setting templates define the different settings that can be used for the associ...
  4bc7f740-180e-4586-adb6-38b2e9024e6b Application...
  898f1161-d651-43d1-805c-3b0b388a9fc2 Custom Policy       Settings ...
  5cf42378-d67d-4f36-ba46-e8b86229381d Password Rule       Settings ...
  ```
2. <span data-ttu-id="51ef3-126">Чтобы добавить URL-адрес правил использования, сначала необходимо получить объект SettingsTemplate, который определяет значение URL-адреса правил использования; это — шаблон Group.Unified:</span><span class="sxs-lookup"><span data-stu-id="51ef3-126">To add a usage guideline URL, first you need to get the SettingsTemplate object that defines the usage guideline URL value; that is, the Group.Unified template:</span></span>
  
  ```
  $Template = Get-AzureADDirectorySettingTemplate -Id 62375ab9-6b52-47ed-826b-58e47e0e304b
  ```
3. <span data-ttu-id="51ef3-127">Затем создайте новый объект параметров на основе этого шаблона:</span><span class="sxs-lookup"><span data-stu-id="51ef3-127">Next, create a new settings object based on that template:</span></span>
  
  ```
  $Setting = $template.CreateDirectorySetting()
  ```  
4. <span data-ttu-id="51ef3-128">Затем обновите значение правил использования:</span><span class="sxs-lookup"><span data-stu-id="51ef3-128">Then update the usage guideline value:</span></span>
  
  ```
  $setting["UsageGuidelinesUrl"] = "<https://guideline.com>"
  ```  
5. <span data-ttu-id="51ef3-129">И, наконец, примените параметры:</span><span class="sxs-lookup"><span data-stu-id="51ef3-129">Finally, apply the settings:</span></span>
  
  ```
  New-AzureADDirectorySetting -DirectorySetting $setting
  ```

<span data-ttu-id="51ef3-130">После успешного выполнения командлет возвращает идентификатор нового объекта Settings.</span><span class="sxs-lookup"><span data-stu-id="51ef3-130">Upon successful completion, the cmdlet returns the ID of the new settings object:</span></span>
  ```
  Id                                   DisplayName TemplateId                           Values
  --                                   ----------- ----------                           ------
  c391b57d-5783-4c53-9236-cefb5c6ef323             62375ab9-6b52-47ed-826b-58e47e0e304b {class SettingValue {...
  ```
<span data-ttu-id="51ef3-131">Ниже приведены параметры, определенные в объекте SettingsTemplate шаблона Group.Unified.</span><span class="sxs-lookup"><span data-stu-id="51ef3-131">Here are the settings defined in the Group.Unified SettingsTemplate.</span></span>

| <span data-ttu-id="51ef3-132">**Параметр**</span><span class="sxs-lookup"><span data-stu-id="51ef3-132">**Setting**</span></span> | <span data-ttu-id="51ef3-133">**Описание**</span><span class="sxs-lookup"><span data-stu-id="51ef3-133">**Description**</span></span> |
| --- | --- |
|  <ul><li><span data-ttu-id="51ef3-134">EnableGroupCreation</span><span class="sxs-lookup"><span data-stu-id="51ef3-134">EnableGroupCreation</span></span><li><span data-ttu-id="51ef3-135">Тип: логический</span><span class="sxs-lookup"><span data-stu-id="51ef3-135">Type: Boolean</span></span><li><span data-ttu-id="51ef3-136">значение по умолчанию: True</span><span class="sxs-lookup"><span data-stu-id="51ef3-136">Default: True</span></span> |<span data-ttu-id="51ef3-137">Флаг, указывающий, разрешено ли создание объединенных групп в каталоге.</span><span class="sxs-lookup"><span data-stu-id="51ef3-137">The flag indicating whether Unified Group creation is allowed in the directory.</span></span> |
|  <ul><li><span data-ttu-id="51ef3-138">GroupCreationAllowedGroupId</span><span class="sxs-lookup"><span data-stu-id="51ef3-138">GroupCreationAllowedGroupId</span></span><li><span data-ttu-id="51ef3-139">Тип: строка</span><span class="sxs-lookup"><span data-stu-id="51ef3-139">Type: String</span></span><li><span data-ttu-id="51ef3-140">Default: “”</span><span class="sxs-lookup"><span data-stu-id="51ef3-140">Default: “”</span></span> |<span data-ttu-id="51ef3-141">Идентификатор GUID группы безопасности, участникам которой разрешено создавать единые группы, даже когда EnableGroupCreation == false.</span><span class="sxs-lookup"><span data-stu-id="51ef3-141">GUID of the security group for which the members are allowed to create Unified Groups even when EnableGroupCreation == false.</span></span> |
|  <ul><li><span data-ttu-id="51ef3-142">UsageGuidelinesUrl</span><span class="sxs-lookup"><span data-stu-id="51ef3-142">UsageGuidelinesUrl</span></span><li><span data-ttu-id="51ef3-143">Тип: строка</span><span class="sxs-lookup"><span data-stu-id="51ef3-143">Type: String</span></span><li><span data-ttu-id="51ef3-144">Default: “”</span><span class="sxs-lookup"><span data-stu-id="51ef3-144">Default: “”</span></span> |<span data-ttu-id="51ef3-145">Ссылка на правила использования группы.</span><span class="sxs-lookup"><span data-stu-id="51ef3-145">A link to the Group Usage Guidelines.</span></span> |
|  <ul><li><span data-ttu-id="51ef3-146">ClassificationDescriptions</span><span class="sxs-lookup"><span data-stu-id="51ef3-146">ClassificationDescriptions</span></span><li><span data-ttu-id="51ef3-147">Тип: строка</span><span class="sxs-lookup"><span data-stu-id="51ef3-147">Type: String</span></span><li><span data-ttu-id="51ef3-148">Default: “”</span><span class="sxs-lookup"><span data-stu-id="51ef3-148">Default: “”</span></span> | <span data-ttu-id="51ef3-149">Разделенный запятыми список описаний классификаций.</span><span class="sxs-lookup"><span data-stu-id="51ef3-149">A comma-delimited list of classification descriptions.</span></span> |
|  <ul><li><span data-ttu-id="51ef3-150">DefaultClassification</span><span class="sxs-lookup"><span data-stu-id="51ef3-150">DefaultClassification</span></span><li><span data-ttu-id="51ef3-151">Тип: строка</span><span class="sxs-lookup"><span data-stu-id="51ef3-151">Type: String</span></span><li><span data-ttu-id="51ef3-152">Default: “”</span><span class="sxs-lookup"><span data-stu-id="51ef3-152">Default: “”</span></span> | <span data-ttu-id="51ef3-153">Классификация, которая должна использоваться по умолчанию для группы, если не была указана иная классификация.</span><span class="sxs-lookup"><span data-stu-id="51ef3-153">The classification that is to be used as the default classification for a group if none was specified.</span></span>|
|  <ul><li><span data-ttu-id="51ef3-154">PrefixSuffixNamingRequirement</span><span class="sxs-lookup"><span data-stu-id="51ef3-154">PrefixSuffixNamingRequirement</span></span><li><span data-ttu-id="51ef3-155">Тип: строка</span><span class="sxs-lookup"><span data-stu-id="51ef3-155">Type: String</span></span><li><span data-ttu-id="51ef3-156">Default: “”</span><span class="sxs-lookup"><span data-stu-id="51ef3-156">Default: “”</span></span> |<span data-ttu-id="51ef3-157">Еще не реализован.</span><span class="sxs-lookup"><span data-stu-id="51ef3-157">Not implemented yet</span></span>
|  <ul><li><span data-ttu-id="51ef3-158">AllowGuestsToBeGroupOwner</span><span class="sxs-lookup"><span data-stu-id="51ef3-158">AllowGuestsToBeGroupOwner</span></span><li><span data-ttu-id="51ef3-159">Тип: логический</span><span class="sxs-lookup"><span data-stu-id="51ef3-159">Type: Boolean</span></span><li><span data-ttu-id="51ef3-160">значение по умолчанию: False</span><span class="sxs-lookup"><span data-stu-id="51ef3-160">Default: False</span></span> | <span data-ttu-id="51ef3-161">Логическое значение, указывающее, может ли гостевой пользователь быть владельцем группы.</span><span class="sxs-lookup"><span data-stu-id="51ef3-161">Boolean indicating whether or not a guest user can be an owner of groups.</span></span> |
|  <ul><li><span data-ttu-id="51ef3-162">AllowGuestsToAccessGroups</span><span class="sxs-lookup"><span data-stu-id="51ef3-162">AllowGuestsToAccessGroups</span></span><li><span data-ttu-id="51ef3-163">Тип: логический</span><span class="sxs-lookup"><span data-stu-id="51ef3-163">Type: Boolean</span></span><li><span data-ttu-id="51ef3-164">значение по умолчанию: True</span><span class="sxs-lookup"><span data-stu-id="51ef3-164">Default: True</span></span> | <span data-ttu-id="51ef3-165">Логическое значение, указывающее, может ли гостевой пользователь иметь доступ к содержимому единой группы.</span><span class="sxs-lookup"><span data-stu-id="51ef3-165">Boolean indicating whether or not a guest user can have access to Unified groups' content.</span></span> |
|  <ul><li><span data-ttu-id="51ef3-166">GuestUsageGuidelinesUrl</span><span class="sxs-lookup"><span data-stu-id="51ef3-166">GuestUsageGuidelinesUrl</span></span><li><span data-ttu-id="51ef3-167">Тип: строка</span><span class="sxs-lookup"><span data-stu-id="51ef3-167">Type: String</span></span><li><span data-ttu-id="51ef3-168">Default: “”</span><span class="sxs-lookup"><span data-stu-id="51ef3-168">Default: “”</span></span> | <span data-ttu-id="51ef3-169">URL-адрес ссылки на правила использования гостя.</span><span class="sxs-lookup"><span data-stu-id="51ef3-169">The url of a link to the guest usage guidelines.</span></span> |
|  <ul><li><span data-ttu-id="51ef3-170">AllowToAddGuests</span><span class="sxs-lookup"><span data-stu-id="51ef3-170">AllowToAddGuests</span></span><li><span data-ttu-id="51ef3-171">Тип: логический</span><span class="sxs-lookup"><span data-stu-id="51ef3-171">Type: Boolean</span></span><li><span data-ttu-id="51ef3-172">значение по умолчанию: True</span><span class="sxs-lookup"><span data-stu-id="51ef3-172">Default: True</span></span> | <span data-ttu-id="51ef3-173">Логическое значение, указывающее, разрешено ли добавлять гостей в этот каталог.</span><span class="sxs-lookup"><span data-stu-id="51ef3-173">A boolean indicating whether or not is allowed to add guests to this directory.</span></span>|
|  <ul><li><span data-ttu-id="51ef3-174">ClassificationList</span><span class="sxs-lookup"><span data-stu-id="51ef3-174">ClassificationList</span></span><li><span data-ttu-id="51ef3-175">Тип: строка</span><span class="sxs-lookup"><span data-stu-id="51ef3-175">Type: String</span></span><li><span data-ttu-id="51ef3-176">Default: “”</span><span class="sxs-lookup"><span data-stu-id="51ef3-176">Default: “”</span></span> |<span data-ttu-id="51ef3-177">Разделенный запятыми список допустимых значений классификации, которые можно применять к объединенным группам.</span><span class="sxs-lookup"><span data-stu-id="51ef3-177">A comma-delimited list of valid classification values that can be applied to Unified Groups.</span></span> |
|  <ul><li><span data-ttu-id="51ef3-178">EnableGroupCreation</span><span class="sxs-lookup"><span data-stu-id="51ef3-178">EnableGroupCreation</span></span><li><span data-ttu-id="51ef3-179">Тип: логический</span><span class="sxs-lookup"><span data-stu-id="51ef3-179">Type: Boolean</span></span><li><span data-ttu-id="51ef3-180">значение по умолчанию: True</span><span class="sxs-lookup"><span data-stu-id="51ef3-180">Default: True</span></span> | <span data-ttu-id="51ef3-181">Логическое значение, указывающее, могут ли пользователи без прав администратора создавать единые группы.</span><span class="sxs-lookup"><span data-stu-id="51ef3-181">A boolean indicating whether or not non-admin users can create new Unified groups.</span></span> |


## <a name="read-settings-at-the-directory-level"></a><span data-ttu-id="51ef3-182">Чтение параметров на уровне каталога</span><span class="sxs-lookup"><span data-stu-id="51ef3-182">Read settings at the directory level</span></span>
<span data-ttu-id="51ef3-183">Далее приведены действия, необходимые для чтения параметров на уровне каталога, применимые ко всем группам Office в каталоге.</span><span class="sxs-lookup"><span data-stu-id="51ef3-183">These steps read settings at directory level, which apply to all Office groups in the directory.</span></span>

1. <span data-ttu-id="51ef3-184">Чтение всех существующих параметров каталога:</span><span class="sxs-lookup"><span data-stu-id="51ef3-184">Read all existing directory settings:</span></span>
  ```
  Get-AzureADDirectorySetting -All $True
  ```
  <span data-ttu-id="51ef3-185">Этот командлет возвращает список всех параметров каталога:</span><span class="sxs-lookup"><span data-stu-id="51ef3-185">This cmdlet returns a list of all directory settings:</span></span>
  ```
  Id                                   DisplayName   TemplateId                           Values
  --                                   -----------   ----------                           ------
  c391b57d-5783-4c53-9236-cefb5c6ef323 Group.Unified 62375ab9-6b52-47ed-826b-58e47e0e304b {class SettingValue {...
  ```

2. <span data-ttu-id="51ef3-186">Чтение всех параметров определенной группы:</span><span class="sxs-lookup"><span data-stu-id="51ef3-186">Read all settings for a specific group:</span></span>
  ```
  Get-AzureADObjectSetting -TargetObjectId ab6a3887-776a-4db7-9da4-ea2b0d63c504 -TargetType Groups
  ```

3. <span data-ttu-id="51ef3-187">Чтение всех значений параметров каталога из объекта Settings конкретного каталога по его идентификатору GUID.</span><span class="sxs-lookup"><span data-stu-id="51ef3-187">Read all directory settings values of a specific directory settings object, using Settings Id GUID:</span></span>
  ```
  (Get-AzureADDirectorySetting -Id c391b57d-5783-4c53-9236-cefb5c6ef323).values
  ```
  <span data-ttu-id="51ef3-188">Этот командлет возвращает имена и значения в объекте Settings для этой конкретной группы:</span><span class="sxs-lookup"><span data-stu-id="51ef3-188">This cmdlet returns the names and values in this settings object for this specific group:</span></span>
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

## <a name="update-settings-for-a-specific-group"></a><span data-ttu-id="51ef3-189">Обновление параметров определенной группы</span><span class="sxs-lookup"><span data-stu-id="51ef3-189">Update settings for a specific group</span></span>

1. <span data-ttu-id="51ef3-190">Найдите шаблон параметров Groups.Unified.Guest.</span><span class="sxs-lookup"><span data-stu-id="51ef3-190">Search for the settings template named "Groups.Unified.Guest"</span></span>
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
2. <span data-ttu-id="51ef3-191">Получите объект SettingTemplate для шаблона Groups.Unified.Guest.</span><span class="sxs-lookup"><span data-stu-id="51ef3-191">Retrieve the template object for the Groups.Unified.Guest template:</span></span>
  ```
  $Template = Get-AzureADDirectorySettingTemplate -Id 08d542b9-071f-4e16-94b0-74abb372e3d9
  ```
3. <span data-ttu-id="51ef3-192">Создайте объект Settings из шаблона.</span><span class="sxs-lookup"><span data-stu-id="51ef3-192">Create a new settings object from the template:</span></span>
  ```
  $Setting = $Template.CreateDirectorySetting()
  ```

4. <span data-ttu-id="51ef3-193">Установите требуемое значение для параметра.</span><span class="sxs-lookup"><span data-stu-id="51ef3-193">Set the setting to the required value:</span></span>
  ```
  $Setting["AllowToAddGuests"]=$False
  ```
5. <span data-ttu-id="51ef3-194">Создайте параметр для требуемой группы в каталоге.</span><span class="sxs-lookup"><span data-stu-id="51ef3-194">Create the new setting for the required group in the directory:</span></span>
  ```
  New-AzureADObjectSetting -TargetType Groups -TargetObjectId ab6a3887-776a-4db7-9da4-ea2b0d63c504 -DirectorySetting $Setting
  
  Id                                   DisplayName TemplateId                           Values
  --                                   ----------- ----------                           ------
  25651479-a26e-4181-afce-ce24111b2cb5             08d542b9-071f-4e16-94b0-74abb372e3d9 {class SettingValue {...
  ```

## <a name="update-settings-at-the-directory-level"></a><span data-ttu-id="51ef3-195">Обновление параметров на уровне каталога</span><span class="sxs-lookup"><span data-stu-id="51ef3-195">Update settings at the directory level</span></span>

<span data-ttu-id="51ef3-196">Далее приведены действия, необходимые для обновления параметров на уровне каталога, которые применяются ко всем единым группам в каталоге.</span><span class="sxs-lookup"><span data-stu-id="51ef3-196">These steps update settings at directory level, which apply to all Unified groups in the directory.</span></span> <span data-ttu-id="51ef3-197">В этих примерах предполагается, что в каталоге уже существует объект Settings.</span><span class="sxs-lookup"><span data-stu-id="51ef3-197">These examples assume there is already a Settings object in your directory.</span></span>

1. <span data-ttu-id="51ef3-198">Найдите существующий объект Settings.</span><span class="sxs-lookup"><span data-stu-id="51ef3-198">Find the existing Settings object:</span></span>
  ```
  Get-AzureADDirectorySetting | Where-object -Property Displayname -Value "Group.Unified" -EQ
  
  Id                                   DisplayName   TemplateId                           Values
  --                                   -----------   ----------                           ------
  c391b57d-5783-4c53-9236-cefb5c6ef323 Group.Unified 62375ab9-6b52-47ed-826b-58e47e0e304b {class SettingValue {...
  
  $setting = Get-AzureADDirectorySetting –Id c391b57d-5783-4c53-9236-cefb5c6ef323
  ```
2. <span data-ttu-id="51ef3-199">Обновление значения:</span><span class="sxs-lookup"><span data-stu-id="51ef3-199">Update the value:</span></span>
  
  ```
  $Setting["AllowToAddGuests"] = "false"
  ```
3. <span data-ttu-id="51ef3-200">Обновление параметра:</span><span class="sxs-lookup"><span data-stu-id="51ef3-200">Update the setting:</span></span>
  
  ```
  Set-AzureADDirectorySetting -Id c391b57d-5783-4c53-9236-cefb5c6ef323 -DirectorySetting $Setting
  ```

## <a name="remove-settings-at-the-directory-level"></a><span data-ttu-id="51ef3-201">Удаление параметров на уровне каталога</span><span class="sxs-lookup"><span data-stu-id="51ef3-201">Remove settings at the directory level</span></span>
<span data-ttu-id="51ef3-202">Далее приведено действие, необходимое для удаления параметров на уровне каталога, применимое ко всем группам Office в каталоге.</span><span class="sxs-lookup"><span data-stu-id="51ef3-202">This step removes settings at directory level, which apply to all Office groups in the directory.</span></span>
  ```
  Remove-AzureADDirectorySetting –Id c391b57d-5783-4c53-9236-cefb5c6ef323c
  ```

## <a name="cmdlet-syntax-reference"></a><span data-ttu-id="51ef3-203">Справочник по синтаксису командлетов</span><span class="sxs-lookup"><span data-stu-id="51ef3-203">Cmdlet syntax reference</span></span>
<span data-ttu-id="51ef3-204">Дополнительную документацию по PowerShell Azure Active Directory см. в разделе [Azure Active Directory Cmdlets](/powershell/azure/install-adv2?view=azureadps-2.0) (Командлеты Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="51ef3-204">You can find more Azure Active Directory PowerShell documentation at [Azure Active Directory Cmdlets](/powershell/azure/install-adv2?view=azureadps-2.0).</span></span>

## <a name="additional-reading"></a><span data-ttu-id="51ef3-205">Дополнительные материалы</span><span class="sxs-lookup"><span data-stu-id="51ef3-205">Additional reading</span></span>

* [<span data-ttu-id="51ef3-206">Управление доступом к ресурсам с помощью групп Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="51ef3-206">Managing access to resources with Azure Active Directory groups</span></span>](active-directory-manage-groups.md)
* [<span data-ttu-id="51ef3-207">Интеграция локальных удостоверений с Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="51ef3-207">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)
