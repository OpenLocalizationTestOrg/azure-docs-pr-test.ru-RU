---
title: "aaaEnable подключение к удаленному рабочему столу для роли в облачных службах Azure с помощью PowerShell"
description: "Как tooconfigure azure облачные приложения службы с помощью подключения удаленного рабочего стола tooallow PowerShell"
services: cloud-services
documentationcenter: 
author: thraka
manager: timlt
editor: 
ms.assetid: bf2f70a4-20dc-4302-a91a-38cd7a2baa62
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: adegeo
ms.openlocfilehash: 3f46b014f29f1c0be0e1b485d2f0152424162bb2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="enable-remote-desktop-connection-for-a-role-in-azure-cloud-services-using-powershell"></a>Включение подключения к удаленному рабочему столу для роли в облачных службах Azure с помощью PowerShell
> [!div class="op_single_selector"]
> * [портале Azure](cloud-services-role-enable-remote-desktop-new-portal.md)
> * [Классический портал Azure](cloud-services-role-enable-remote-desktop.md)
> * [PowerShell](cloud-services-role-enable-remote-desktop-powershell.md)
> * [Visual Studio](../vs-azure-tools-remote-desktop-roles.md)
>
>

Удаленный рабочий стол позволяет tooaccess hello системной роли, работающих в Azure. Можно использовать tootroubleshoot подключения удаленного рабочего стола и диагностировать проблемы с приложением во время его выполнения.

В этой статье описывается как tooenable удаленного рабочего стола на роли облачной службы с помощью PowerShell. В разделе [как tooinstall и настройка Azure PowerShell](/powershell/azure/overview) для hello предварительных требований для этой статьи. PowerShell использует hello расширения удаленного рабочего стола, поэтому можно включить удаленный рабочий стол, после развертывания приложения hello.

## <a name="configure-remote-desktop-from-powershell"></a>Настройка удаленного рабочего стола с помощью PowerShell
Hello [AzureServiceRemoteDesktopExtension набор](/powershell/module/azure/set-azureserviceremotedesktopextension?view=azuresmps-3.7.0) командлет позволяет tooenable удаленного рабочего стола на указанные роли или все роли из развертывания облачной службы. Hello командлета вы можете задать hello имя пользователя и пароль для hello пользователя удаленного рабочего стола через hello *учетные данные* параметр, который принимает объект PSCredential.

Если вы используете PowerShell интерактивно, можно легко задавать hello объекта PSCredential, вызывающему Привет [учетные данные Get](https://technet.microsoft.com/library/hh849815.aspx) командлета.

```
$remoteusercredentials = Get-Credential
```

Эта команда отображает диалоговое окно, позволяя вам tooenter hello имя пользователя и пароль для удаленного пользователя hello в безопасном режиме.

Так как в сценариях автоматизации помогает PowerShell, можно также настроить hello **PSCredential** объекта таким образом, не требующее вмешательства пользователя. Во-первых необходимо tooset безопасный пароль. Начать с указанием незашифрованный пароль преобразовать tooa защищенной строки с помощью [ConvertTo-SecureString](https://technet.microsoft.com/library/hh849818.aspx). Затем следует записать tooconvert этой защищенной строки в зашифрованную стандартную строку с помощью [ConvertFrom-SecureString](https://technet.microsoft.com/library/hh849814.aspx). Теперь можно сохранить этот файл tooa зашифрованную стандартную строку с помощью [Set-Content](https://technet.microsoft.com/library/ee176959.aspx).

Также можно создать файл надежный пароль, поэтому, не tootype в hello пароль каждый раз. Кроме того, файл с надежным паролем безопаснее, чем обычный текстовый файл. Используйте следующие toocreate PowerShell файл безопасного пароля hello.

```
ConvertTo-SecureString -String "Password123" -AsPlainText -Force | ConvertFrom-SecureString | Set-Content "password.txt"
```

> [!IMPORTANT]
> При задании пароля hello, убедитесь, что выполнены hello [требованиям сложности](https://technet.microsoft.com/library/cc786468.aspx).
>
>

toocreate hello объекта учетных данных из файла hello надежный пароль, необходимо прочитать содержимое файла hello и преобразовать их назад tooa secure строки с помощью [ConvertTo-SecureString](https://technet.microsoft.com/library/hh849818.aspx).

Hello [набор AzureServiceRemoteDesktopExtension](/powershell/module/azure/set-azureserviceremotedesktopextension?view=azuresmps-3.7.0) командлет также принимает *истечение срока действия* параметр, который задает **DateTime** пользовательских hello срок действия учетной записи. Например можно задать tooexpire hello учетную запись на несколько дней из hello текущую дату и время.

В этом примере PowerShell показано, как tooset hello расширения удаленного рабочего стола в облачной службе:

```
$servicename = "cloudservice"
$username = "RemoteDesktopUser"
$securepassword = Get-Content -Path "password.txt" | ConvertTo-SecureString
$expiry = $(Get-Date).AddDays(1)
$credential = New-Object System.Management.Automation.PSCredential $username,$securepassword
Set-AzureServiceRemoteDesktopExtension -ServiceName $servicename -Credential $credential -Expiration $expiry
```
Также при необходимости можно указать слот развертывания hello и роли, которые вы хотите tooenable удаленного рабочего стола на. Если эти параметры не указаны, hello включает удаленный рабочий стол для всех ролей в hello **рабочей** слот развертывания.

Hello расширения удаленного рабочего стола связанной с развертыванием. Если вы создаете новое развертывание для службы hello, у вас есть удаленного рабочего стола tooenable развертывания. Если требуется всегда toohave включен удаленный рабочий стол, следует рассмотреть, интеграция hello сценариев PowerShell в рабочий процесс развертывания.

## <a name="remote-desktop-into-a-role-instance"></a>Подключение к экземпляру роли по протоколу удаленного рабочего стола
Hello [Get-AzureRemoteDesktopFile](/powershell/module/azure/get-azureremotedesktopfile?view=azuresmps-3.7.0) командлета — используется tooremote рабочего стола к определенного экземпляра роли облачной службы. Можно использовать hello *LocalPath* файл hello toodownload параметр протокола удаленного рабочего СТОЛА на компьютере. Или можно использовать hello *запуска* диалоговое окно параметров toodirectly запуска hello удаленный рабочий стол tooaccess hello экземпляра роли облачной службы.

```
Get-AzureRemoteDesktopFile -ServiceName $servicename -Name "WorkerRole1_IN_0" -Launch
```


## <a name="check-if-remote-desktop-extension-is-enabled-on-a-service"></a>Убедитесь, что расширение удаленного рабочего стола включено в службе.
Hello [Get AzureServiceRemoteDesktopExtension](/powershell/module/azure/get-azureremotedesktopfile?view=azuresmps-3.7.0) показывает, включен или отключен на развертывание службы удаленного рабочего стола. Hello командлет возвращает hello имя пользователя для пользователя удаленного рабочего стола hello и hello роли, которые hello удаленного рабочего стола расширение включено для. По умолчанию это происходит на слот развертывания hello и toouse hello промежуточных слотах, вместо этого можно выбрать.

```
Get-AzureServiceRemoteDesktopExtension -ServiceName $servicename
```

## <a name="remove-remote-desktop-extension-from-a-service"></a>Удаление расширения удаленного рабочего стола из службы
При включении удаленного рабочего стола расширения hello в развертывании, и требуется tooupdate hello настройки удаленного рабочего стола, сначала удалите расширение hello. И снова включите его с новыми настройками hello. Например если требуется, чтобы tooset новый пароль для учетной записи удаленного пользователя hello или hello срок действия истек. Это требуется в существующих развертываниях расширением hello удаленного рабочего стола включена. Для новых развертываний можно просто применить расширения hello напрямую.

tooremove hello удаленного рабочего стола расширения из hello развертывания, можно использовать hello [AzureServiceRemoteDesktopExtension удаление](/powershell/module/azure/remove-azureserviceremotedesktopextension?view=azuresmps-3.7.0) командлета. Также при необходимости можно указать слот развертывания hello и роли, из которого нужно tooremove hello удаленного рабочего стола расширения.

```
Remove-AzureServiceRemoteDesktopExtension -ServiceName $servicename -UninstallConfiguration
```

> [!NOTE]
> hello расширения toocompletely удалить конфигурацию необходимо вызвать hello *удалить* командлет с hello **UninstallConfiguration** параметра.
>
> Hello **UninstallConfiguration** параметр удаляет все конфигурации расширения, примененные toohello службы. Все конфигурации расширения связан с конфигурацией службы hello. Вызов hello *удалить* командлета без **UninstallConfiguration** отсоединяет hello <mark>развертывания</mark> из конфигурации расширения hello, поэтому фактически удаляется расширение Hello. Тем не менее Настройка расширения hello остается связанным с hello службы.
>
>

## <a name="additional-resources"></a>Дополнительные ресурсы

[Как облачные службы tooConfigure](cloud-services-how-to-configure.md)
[облачных служб часто задаваемые вопросы — удаленного рабочего стола](cloud-services-faq.md)
