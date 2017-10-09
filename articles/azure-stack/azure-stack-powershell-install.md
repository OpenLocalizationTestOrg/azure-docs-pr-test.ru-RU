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
# <a name="install-powershell-for-azure-stack"></a>Установите PowerShell для Azure стека  

Совместимые модули Azure PowerShell Azure стека являются обязательным toowork со стеком Azure. В этом руководстве мы рассмотрим tooinstall необходимые шаги hello PowerShell для Azure стека. Можно использовать hello действия, описанные в этой статье из пакета средств разработки Azure стека hello или из внешнего клиента на основе Windows, при подключении через виртуальную частную сеть.

В этой статье содержатся подробные инструкции по tooinstall PowerShell для Azure стека. Тем не менее, tooquickly установить и настроить PowerShell, можно использовать сценарий hello, входящий в hello [приступить к работе с PowerShell](azure-stack-powershell-configure-quickstart.md) раздела. 

> [!NOTE]
> Привет, следующие шаги требуют PowerShell 5.0. toocheck версии, выполнения $PSVersionTable.PSVersion и сравнить hello «основной» версии.

Команды PowerShell для Azure стека устанавливаются через коллекцию PowerShell hello. tooregiser hello PSGallery репозитория, откройте сеанс PowerShell с повышенными привилегиями из пакета средств разработки hello или из внешнего клиента, на основе Windows при подключении через виртуальную частную сеть запуска hello следующую команду:

```powershell
Set-PSRepository `
  -Name "PSGallery" `
  -InstallationPolicy Trusted
```

## <a name="uninstall-existing-versions-of-powershell"></a>Удалите существующие версии PowerShell

Прежде чем устанавливать hello требуемой версии, убедитесь, что удалить все существующие модули Azure PowerShell. Их можно удалить с помощью одного из следующих двух методов hello:

* модули toouninstall hello существующих PowerShell, войдите в пакет средств разработки toohello или внешних toohello клиента на основе Windows, при планировании tooestablish VPN-подключения. Закройте все активные сеансы PowerShell hello и выполнения hello следующую команду: 

   ```powershell
   Get-Module -ListAvailable | where-Object {$_.Name -like “Azure*”} | Uninstall-Module
   ```

* Войдите в пакет средств разработки toohello или внешних toohello клиента на основе Windows, при планировании tooestablish VPN-подключения. Удалить все hello папки, которые начинаются с «Azure» из hello `C:\Program Files (x86)\WindowsPowerShell\Modules` и `C:\Users\AzureStackAdmin\Documents\WindowsPowerShell\Modules` папки. Удаление этих папок удаляет все существующие модули PowerShell из «AzureStackAdmin» hello и области «глобальные» пользователя. 

Hello следующих разделах описаны tooinstall необходимые шаги hello PowerShell для Azure стека. PowerShell можно установить на стек Azure, который выполняется в подключенной, частично подключен, или в сценарии отсоединения. 

## <a name="install-powershell-in-a-connected-scenario"></a>Установите в связанный сценарий PowerShell 

Совместимые модули AzureRM Azure стека устанавливаются через профили версии API. Стек Azure требует hello **2017 г. 03-09-профиля** профиля версии API, который доступен при установке модуля AzureRM.Bootstrapper hello. toolearn о профилях версии API и командлеты hello из них, см. toohello [управления профилями версии API](azure-stack-version-profiles.md). В модулях AzureRM toohello сложения также следует установить модули PowerShell Azure стека конкретного hello. На рабочей станции разработки, выполните эти модули hello, следуя tooinstall сценарий PowerShell:

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

tooconfirm установки hello, перезапустите hello следующую команду:

  ```powershell
  Get-Module `
    -ListAvailable | where-Object {$_.Name -like “Azure*”}
  ```
  При успешном выполнении установки hello hello AzureRM и AzureStack модули отображаются в выходных данных hello.

## <a name="install-powershell-in-a-disconnected-or-in-a-partially-connected-scenario"></a>Установите PowerShell в отключенном или в сценарии с частично подключенным

В сценарии отсоединения необходимо сначала загрузить hello модули PowerShell tooa компьютере с подключением к Интернету и передает их toohello Azure стека Development Kit для установки.

1. Войдите в компьютер tooa которой вы подключены к Интернету и использовать следующий скрипт toodownload hello AzureRM hello и AzureStack пакеты на локальном компьютере.

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

2. Копировать hello загруженных пакетов через tooa USB-устройство.

3. Войдите в пакет средств разработки toohello и скопируйте hello пакетов из расположения tooa устройства USB hello в пакет средств разработки hello. 

4. Теперь необходимо зарегистрировать это расположение в качестве репозитория по умолчанию hello и установить hello AzureRM и AzureStack модули из этого репозитория:

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

## <a name="next-steps"></a>Дальнейшие действия

* [Загрузить набор средств Azure стека из GitHub](azure-stack-powershell-download.md)
* [Настройка среды PowerShell hello Azure стека пользователя](azure-stack-powershell-configure-user.md)  
* [Настройка среды PowerShell оператор hello стек Azure](azure-stack-powershell-configure-admin.md) 
* [Управление профилями версии API в стек Azure](azure-stack-version-profiles.md)  
