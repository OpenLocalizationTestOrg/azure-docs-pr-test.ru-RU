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
# <a name="azure-active-directory-cmdlets-for-configuring-group-settings"></a>Настройка параметров групп с помощью командлетов Azure Active Directory

> [!IMPORTANT]
> Эти материалы относятся группы tooOffice 365. Дополнительные сведения о том, как задать tooallow группы безопасности пользователей toocreate, `Set-MSOLCompanySettings -UsersPermissionToCreateGroupsEnabled $True` как описано в [Set-MSOLCompanySettings](https://docs.microsoft.com/en-us/powershell/module/msonline/set-msolcompanysettings?view=azureadps-1.0). 

Параметры групп Office 365 настраиваются с помощью объектов Settings и SettingsTemplate. Изначально вы не видите все объекты параметров в вашем каталоге, так как ваш каталог настроен с параметрами по умолчанию hello. параметры по умолчанию hello toochange, необходимо создать новый объект параметров с помощью параметров шаблона. Шаблоны параметров определены корпорацией Майкрософт. Поддерживается несколько разных шаблонов параметров. Параметры группы tooconfigure Office 365 для вашего каталога, используйте hello шаблона с именем «Group.Unified». Параметры группы tooconfigure Office 365 на одну группу, используйте шаблон hello, с именем «Group.Unified.Guest». Этот шаблон является группа tooan Office 365 используется toomanage гостевого доступа. 

командлеты Hello являются частью модуля hello Azure Active Directory PowerShell V2. Инструкции как toodownload и установки hello модуля на компьютере, в статье hello [Azure Active Directory PowerShell версии 2](https://docs.microsoft.com/powershell/azuread/). Вы можете установить выпуск версии 2 hello hello модуля из [коллекции PowerShell hello](https://www.powershellgallery.com/packages/AzureAD/).

## <a name="retrieve-a-specific-settings-value"></a>Получение определенного значения параметра
Если известно имя hello hello параметр tooretrieve, можно использовать hello ниже текущего значения параметров командлета tooretrieve hello. В этом примере извлекаются hello значение для параметра с именем «UsageGuidelinesUrl.» Дополнительные сведения о параметрах каталога и их именах приводятся далее в этой статье.

```powershell
(Get-AzureADDirectorySetting).Values | Where-Object -Property Name -Value UsageGuidelinesUrl -EQ
```

## <a name="create-settings-at-hello-directory-level"></a>Создание параметров на уровне папки hello
Эти шаги создают параметры на уровне папки применимые группы Office 365 tooall (единой группы) в каталоге hello.

1. В hello DirectorySettings командлеты необходимо указать идентификатор hello hello требуется toouse SettingsTemplate. Если вы не знаете этот идентификатор, этот командлет возвращает список всех параметров шаблонов hello:
  
  ```
  PS C:> Get-AzureADDirectorySettingTemplate
  ```
  Этот командлет отображает все шаблоны, которые доступны.
  
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
2. tooadd URL-адрес правила использования, сначала необходимо tooget hello SettingsTemplate объект, который определяет значение URL-адреса направляющих hello использования; то есть hello Group.Unified шаблона:
  
  ```
  $Template = Get-AzureADDirectorySettingTemplate -Id 62375ab9-6b52-47ed-826b-58e47e0e304b
  ```
3. Затем создайте новый объект параметров на основе этого шаблона:
  
  ```
  $Setting = $template.CreateDirectorySetting()
  ```  
4. Обновите значение направляющих hello использования:
  
  ```
  $setting["UsageGuidelinesUrl"] = "<https://guideline.com>"
  ```  
5. Наконец примените параметры hello:
  
  ```
  New-AzureADDirectorySetting -DirectorySetting $setting
  ```

После успешного завершения hello командлет возвращает идентификатор hello объекта hello новые параметры:
  ```
  Id                                   DisplayName TemplateId                           Values
  --                                   ----------- ----------                           ------
  c391b57d-5783-4c53-9236-cefb5c6ef323             62375ab9-6b52-47ed-826b-58e47e0e304b {class SettingValue {...
  ```
Ниже приведены параметры hello, определенные в Group.Unified SettingsTemplate hello.

| **Параметр** | **Описание** |
| --- | --- |
|  <ul><li>EnableGroupCreation<li>Тип: логический<li>значение по умолчанию: True |Hello флаг, указывающий, разрешено ли создание единой группы в каталоге hello. |
|  <ul><li>GroupCreationAllowedGroupId<li>Тип: строка<li>Default: “” |Идентификатор GUID группы безопасности hello, какие hello участники могут toocreate объединенные группы, даже когда EnableGroupCreation == false. |
|  <ul><li>UsageGuidelinesUrl<li>Тип: строка<li>Default: “” |Ссылка toohello правила использования группы. |
|  <ul><li>ClassificationDescriptions<li>Тип: строка<li>Default: “” | Разделенный запятыми список описаний классификаций. |
|  <ul><li>DefaultClassification<li>Тип: строка<li>Default: “” | Классификация Hello, toobe использовать в качестве hello классификации по умолчанию для группы, если ничего не было указано.|
|  <ul><li>PrefixSuffixNamingRequirement<li>Тип: строка<li>Default: “” |Еще не реализован.
|  <ul><li>AllowGuestsToBeGroupOwner<li>Тип: логический<li>значение по умолчанию: False | Логическое значение, указывающее, может ли гостевой пользователь быть владельцем группы. |
|  <ul><li>AllowGuestsToAccessGroups<li>Тип: логический<li>значение по умолчанию: True | Логическое значение, указывающее, можно ли существование пользователя guest имеют содержимое группы tooUnified доступа. |
|  <ul><li>GuestUsageGuidelinesUrl<li>Тип: строка<li>Default: “” | URL-адрес Hello toohello ссылку гостевой рекомендации по использованию. |
|  <ul><li>AllowToAddGuests<li>Тип: логический<li>значение по умолчанию: True | Логическое значение, указывающее, доступен ли каталог toothis разрешенных tooadd гостей.|
|  <ul><li>ClassificationList<li>Тип: строка<li>Default: “” |Список с разделителями запятыми допустимого значения, которые может быть применен tooUnified групп. |
|  <ul><li>EnableGroupCreation<li>Тип: логический<li>значение по умолчанию: True | Логическое значение, указывающее, могут ли пользователи без прав администратора создавать единые группы. |


## <a name="read-settings-at-hello-directory-level"></a>Чтение параметров на уровне папки hello
Эти шаги чтение параметров на уровне папки, которые применены tooall Office групп в каталоге hello.

1. Чтение всех существующих параметров каталога:
  ```
  Get-AzureADDirectorySetting -All $True
  ```
  Этот командлет возвращает список всех параметров каталога:
  ```
  Id                                   DisplayName   TemplateId                           Values
  --                                   -----------   ----------                           ------
  c391b57d-5783-4c53-9236-cefb5c6ef323 Group.Unified 62375ab9-6b52-47ed-826b-58e47e0e304b {class SettingValue {...
  ```

2. Чтение всех параметров определенной группы:
  ```
  Get-AzureADObjectSetting -TargetObjectId ab6a3887-776a-4db7-9da4-ea2b0d63c504 -TargetType Groups
  ```

3. Чтение всех значений параметров каталога из объекта Settings конкретного каталога по его идентификатору GUID.
  ```
  (Get-AzureADDirectorySetting -Id c391b57d-5783-4c53-9236-cefb5c6ef323).values
  ```
  Этот командлет возвращает hello имена и значения в этом объекте параметры для этой конкретной группы:
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

## <a name="update-settings-for-a-specific-group"></a>Обновление параметров определенной группы

1. Поиск hello параметры шаблона с именем «Groups.Unified.Guest»
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
2. Получите hello объекта шаблона для шаблона Groups.Unified.Guest hello:
  ```
  $Template = Get-AzureADDirectorySettingTemplate -Id 08d542b9-071f-4e16-94b0-74abb372e3d9
  ```
3. Создание объекта параметров из шаблона hello:
  ```
  $Setting = $Template.CreateDirectorySetting()
  ```

4. Задайте значение toohello требуется параметр hello:
  ```
  $Setting["AllowToAddGuests"]=$False
  ```
5. Создайте новый параметр hello для hello нужную группу в каталоге hello:
  ```
  New-AzureADObjectSetting -TargetType Groups -TargetObjectId ab6a3887-776a-4db7-9da4-ea2b0d63c504 -DirectorySetting $Setting
  
  Id                                   DisplayName TemplateId                           Values
  --                                   ----------- ----------                           ------
  25651479-a26e-4181-afce-ce24111b2cb5             08d542b9-071f-4e16-94b0-74abb372e3d9 {class SettingValue {...
  ```

## <a name="update-settings-at-hello-directory-level"></a>Обновить параметры на уровне папки hello

Эти действия обновления параметров на уровне папки, которые применены tooall единой группы в каталоге hello. В этих примерах предполагается, что в каталоге уже существует объект Settings.

1. Найти существующий объект параметров hello:
  ```
  Get-AzureADDirectorySetting | Where-object -Property Displayname -Value "Group.Unified" -EQ
  
  Id                                   DisplayName   TemplateId                           Values
  --                                   -----------   ----------                           ------
  c391b57d-5783-4c53-9236-cefb5c6ef323 Group.Unified 62375ab9-6b52-47ed-826b-58e47e0e304b {class SettingValue {...
  
  $setting = Get-AzureADDirectorySetting –Id c391b57d-5783-4c53-9236-cefb5c6ef323
  ```
2. Обновите значение hello:
  
  ```
  $Setting["AllowToAddGuests"] = "false"
  ```
3. Обновление параметра hello:
  
  ```
  Set-AzureADDirectorySetting -Id c391b57d-5783-4c53-9236-cefb5c6ef323 -DirectorySetting $Setting
  ```

## <a name="remove-settings-at-hello-directory-level"></a>Удалить параметры на уровне папки hello
Этот шаг удаляет параметры на уровне папки, применяемые tooall Office групп в каталоге hello.
  ```
  Remove-AzureADDirectorySetting –Id c391b57d-5783-4c53-9236-cefb5c6ef323c
  ```

## <a name="cmdlet-syntax-reference"></a>Справочник по синтаксису командлетов
Дополнительную документацию по PowerShell Azure Active Directory см. в разделе [Azure Active Directory Cmdlets](/powershell/azure/install-adv2?view=azureadps-2.0) (Командлеты Azure Active Directory).

## <a name="additional-reading"></a>Дополнительные материалы

* [Управление tooresources доступ с помощью групп Azure Active Directory](active-directory-manage-groups.md)
* [Интеграция локальных удостоверений с Azure Active Directory](active-directory-aadconnect.md)
