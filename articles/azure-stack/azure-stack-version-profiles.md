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
# <a name="manage-api-version-profiles-in-azure-stack"></a>Управление профилями версии API в стек Azure

Профили версии API обеспечивают toomanage способом версии различия между Azure и Azure стека. Профиль версии API — это набор модулей AzureRM PowerShell для определенной версии API. Каждая облачная платформа имеет набор профилей версии поддерживаемых API. Например, стека Azure поддерживает определенный профиль устаревшей версии, например **2017 г. 03-09-профиля**и hello Azure поддерживает **последние** профиля версии API. При установке профиля hello AzureRM PowerShell модули, которые соответствуют toohello указан профиль установлены.

## <a name="install-hello-powershell-module-required-toouse-api-version-profiles"></a>Установка профилей hello API toouse модуля, который требуется PowerShell версии

Hello **AzureRM.Bootstrapper** модуль, который доступен через hello коллекции PowerShell предоставляет командлеты PowerShell, которые требуется toowork с профилями версии API. Используйте следующий командлет tooinstall hello AzureRM.Bootstrapper модуль hello.

```PowerShell
Install-Module -Name AzureRm.BootStrapper
```
Hello AzureRM.Bootstrapper модуль находится в режиме предварительного просмотра; сведения и функциональные возможности могут toochange субъекта. toodownload и установите hello последнюю версию этого модуля из hello коллекции PowerShell, запустите следующий командлет hello:

```PowerShell
Update-Module -Name "AzureRm.BootStrapper"
```

## <a name="install-a-profile"></a>Установка профиля

Используйте hello **установки AzureRmProfile** командлет с hello **2017 г. 03-09-профиля** AzureRM API версии профиль tooinstall hello модулями, необходимыми стеком Azure. Обратите внимание, что с этим профилем версия API не установлены модули администратора облака Azure стека hello, и они должны устанавливаться отдельно, как указано в hello шаг 3 из hello [Установка PowerShell для Azure стека](azure-stack-powershell-install.md) статьи.

```PowerShell 
Install-AzureRMProfile -Profile 2017-03-09-profile
```
## <a name="install-and-import-modules-in-a-profile"></a>Установить и импортировать модули в профиле

Используйте hello **AzureRmProfile используйте** tooinstall и импортируйте модули командлетов, связанных с профилем версии API. В сеансе PowerShell можно импортировать только один профиль версии API. профиль tooimport различных API версии, необходимо открыть новый сеанс PowerShell. Используйте AzureRMProfile Hello выполняет hello следующие задачи:  
1. Проверяет, модули PowerShell hello, связанные с hello указанный профиль версии API устанавливаются в текущей области hello.  
2. Загрузка и установка hello модулей, если они еще не установлены.   
3. Импортирует hello модули в текущий сеанс PowerShell hello. 

```PowerShell
# Installs and imports hello specified API version profile into hello current PowerShell session.
Use-AzureRmProfile -Profile 2017-03-09-profile -Scope CurrentUser

# Installs and imports hello specified API version profile into hello current PowerShell session without any prompts
Use-AzureRmProfile -Profile 2017-03-09-profile -Scope CurrentUser -Force
```

tooinstall и импорта выбранных модулей AzureRM из профиля версии API-интерфейса, необходимо запустить командлет hello используйте AzureRMProfile с hello **модуль** параметр:

```PowerShell
# Installs and imports hello compute, Storage and Network modules from hello specified API version profile into your current PowerShell session.
Use-AzureRmProfile -Profile 2017-03-09-profile -Module AzureRM.Compute, AzureRM.Storage, AzureRM.Network
```

## <a name="get-hello-installed-profiles"></a>Получить профили hello установлен

Используйте hello **Get AzureRmProfile** командлет tooget hello списка доступных профилей версии API: 

```PowerShell
# lists all API version profiles provided by hello AzureRM.BootStrapper module.
Get-AzureRmProfile -ListAvailable 

# lists hello API version profiles which are installed on your machine
Get-AzureRmProfile
```
## <a name="update-profiles"></a>Обновить профили

Используйте hello **AzureRmProfile обновление** модули hello tooupdate командлет в версии профиль toohello последняя версия API модулей, доступных в hello PSGallery. Рекомендуется tooalways запускать hello **AzureRmProfile обновление** командлета в новый tooavoid сеанса PowerShell конфликты при импорте модулей. Hello AzureRmProfile обновления выполняет hello следующие задачи:

1. Проверяет, если последние версии hello модулей устанавливаются в заданный профиль версии API для текущей области hello hello.  
2. Предлагает tooinstall, если они еще не установлены.  
3. Устанавливает и импортирует модули hello обновлены в текущем сеансе PowerShell hello.  

```PowerShell
Update-AzureRmProfile -Profile 2017-03-09-profile
```

tooremove hello ранее установленные версии модулей hello перед обновлением toohello последнюю версию, с помощью командлета Update AzureRmProfile hello вместе с hello **- RemovePreviousVersions** параметр:

```PowerShell 
Update-AzureRmProfile -Profile 2017-03-09-profile -RemovePreviousVersions
```

Этот командлет запускается hello следующие задачи:  

1. Проверяет, если последние версии hello модулей устанавливаются в заданный профиль версии API для текущей области hello hello.  
2. Удаляет старые версии hello модулей из hello текущего профиля версии API и в текущем сеансе PowerShell hello.  
4. предлагает tooinstall hello последнюю версию.  
5. Устанавливает и импортирует модули hello обновлены в текущем сеансе PowerShell hello.  
 
## <a name="uninstall-profiles"></a>Удалять профили

Используйте hello **AzureRmProfile удаления** hello toouninstall командлет указанный профиль версии API.

```PowerShell 
Uninstall-AzureRmProfile -Profile 2017-03-09-profile
```

## <a name="next-steps"></a>Дальнейшие действия
* [Install PowerShell for Azure Stack](azure-stack-powershell-install.md) (Установка PowerShell для Azure Stack)
* [Настройка среды PowerShell hello Azure стека пользователя](azure-stack-powershell-configure-user.md)  
