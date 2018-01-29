---
title: "Использование профилей версий API в Azure Stack | Документация Майкрософт"
description: "Сведения о профилях версии API в Azure Stack."
services: azure-stack
documentationcenter: 
author: mattbriggs
manager: femila
editor: 
ms.assetid: EBAEA4D2-098B-4B5A-A197-2CEA631A1882
ms.service: azure-stack
ms.workload: na
pms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/25/2017
ms.author: mabrigg
ms.openlocfilehash: 68f4250c2a2a6bed1a1e21dc444e93cc87b6f59b
ms.sourcegitcommit: a5f16c1e2e0573204581c072cf7d237745ff98dc
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/11/2017
---
# <a name="manage-api-version-profiles-in-azure-stack"></a>Управление профилями версий API в Azure Stack

*Область применения: интегрированные системы Azure Stack и пакет SDK для Azure Stack*

Профили версий API позволяют управлять различиями между версиями Azure и Azure Stack. Профиль версии API — это набор модулей AzureRM PowerShell с определенными версиями API. Каждая облачная платформа имеет набор поддерживаемых профилей версий API. Например, Azure Stack поддерживает версию профиля определенной даты, например **2017-03-09-profile**, а Azure поддерживает профиль API **последней** версии. При установке профиля устанавливается набор модулей AzureRM PowerShell, которые соответствуют выбранному профилю.

## <a name="install-the-powershell-module-required-to-use-api-version-profiles"></a>Установка модуля PowerShell, необходимого для использования профилей версий API

Модуль **AzureRM.Bootstrapper**, доступный в коллекции PowerShell, предоставляет командлеты PowerShell, необходимые для работы с профилями версий API. Чтобы установить модуль AzureRM.Bootstrapper, используйте следующий командлет:

```PowerShell
Install-Module -Name AzureRm.BootStrapper
```
Модуль AzureRM.Bootstrapper доступен в режиме предварительной версии, поэтому некоторые сведения и функции могут измениться. Чтобы скачать и установить последнюю версию этого модуля из коллекции PowerShell, выполните следующий командлет:

```PowerShell
Update-Module -Name "AzureRm.BootStrapper"
```

## <a name="install-a-profile"></a>Установка профиля

Чтобы установить модули AzureRM, необходимые для Azure Stack, используйте командлет **Install-AzureRmProfile** с профилем API версии **2017-03-09-profile**. Обратите внимание, что модули оператора Azure Stack не устанавливаются с этим профилем версии API. Их нужно устанавливать отдельно, как указано на шаге 3 статьи [Установка PowerShell для Azure Stack](azure-stack-powershell-install.md).

```PowerShell 
Install-AzureRMProfile -Profile 2017-03-09-profile
```
## <a name="install-and-import-modules-in-a-profile"></a>Установка и импорт модулей в профиль

Используйте командлет **Use-AzureRmProfile**, чтобы установить и импортировать модули, связанные с профилем версии API. Для сеанса PowerShell можно импортировать только один профиль версии API. Чтобы импортировать другой профиль версии API, необходимо открыть новый сеанс PowerShell. Командлет Use-AzureRMProfile выполняет следующие задачи.  
1. Проверяет в текущей области наличие модулей PowerShell, связанных с определенным профилем версии API.  
2. Скачивает и устанавливает модули, которые еще не установлены.   
3. Импортирует модули для текущего сеанса PowerShell. 

```PowerShell
# Installs and imports the specified API version profile into the current PowerShell session.
Use-AzureRmProfile -Profile 2017-03-09-profile -Scope CurrentUser

# Installs and imports the specified API version profile into the current PowerShell session without any prompts
Use-AzureRmProfile -Profile 2017-03-09-profile -Scope CurrentUser -Force
```

Чтобы установить и импортировать выбранные модули AzureRM из профиля версии API, выполните командлет Use-AzureRMProfile с параметром **Module**:

```PowerShell
# Installs and imports the compute, Storage and Network modules from the specified API version profile into your current PowerShell session.
Use-AzureRmProfile -Profile 2017-03-09-profile -Module AzureRM.Compute, AzureRM.Storage, AzureRM.Network
```

## <a name="get-the-installed-profiles"></a>Получение установленных профилей

Используйте командлет **Get-AzureRmProfile**, чтобы получить список доступных профилей версий API. 

```PowerShell
# lists all API version profiles provided by the AzureRM.BootStrapper module.
Get-AzureRmProfile -ListAvailable 

# lists the API version profiles which are installed on your machine
Get-AzureRmProfile
```
## <a name="update-profiles"></a>Обновление профилей

Используйте командлет **Update-AzureRmProfile** для обновления модулей в профиле версии API до последней версии, доступной в PSGallery. Всегда запускайте командлет **Update-AzureRmProfile** в новом сеансе PowerShell, чтобы избежать конфликтов при импорте модулей. Командлет Update-AzureRmProfile выполняет следующие задачи.

1. Проверяет в текущей области, установлены ли последние версии модулей в определенном профиле версии API.  
2. Предлагает установить их, если они еще не установлены.  
3. Устанавливает и импортирует обновленные модули для текущего сеанса PowerShell.  

```PowerShell
Update-AzureRmProfile -Profile 2017-03-09-profile
```

Чтобы удалить ранее установленные версии модулей перед обновлением до последней версии, при запуске командлета Update-AzureRmProfile укажите параметр **-RemovePreviousVersions**.

```PowerShell 
Update-AzureRmProfile -Profile 2017-03-09-profile -RemovePreviousVersions
```

Этот командлет выполняет следующие задачи.  

1. Проверяет в текущей области, установлены ли последние версии модулей в определенном профиле версии API.  
2. Удаляет устаревшие версии модулей из текущего профиля версии API и текущего сеанса PowerShell.  
4. Предлагает установить последнюю версию.  
5. Устанавливает и импортирует обновленные модули для текущего сеанса PowerShell.  
 
## <a name="uninstall-profiles"></a>Удаление профилей

Чтобы удалить определенный профиль версии API, используйте командлет **Uninstall-AzureRmProfile**.

```PowerShell 
Uninstall-AzureRmProfile -Profile 2017-03-09-profile
```

## <a name="next-steps"></a>Дальнейшие действия
* [Install PowerShell for Azure Stack](azure-stack-powershell-install.md) (Установка PowerShell для Azure Stack)
* [Configure the Azure Stack user's PowerShell environment](user/azure-stack-powershell-configure-user.md) (Настройка пользовательской среды PowerShell в Azure Stack)  
