---
title: "перенаправление aaaUsing в Azure RemoteApp | Документы Microsoft"
description: "Узнайте, как tooconfigure и использование перенаправления для удаленных приложений RemoteApp"
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: 2c8c867f-4907-4f2e-9ccd-2eb82bb5b837
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: d5739a75cf606bd971268da67b2c5ff0fe5fe19b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="using-redirection-in-azure-remoteapp"></a>Использование перенаправления в удаленном приложении Azure RemoteApp
> [!IMPORTANT]
> Мы выводим службу Azure RemoteApp из эксплуатации 31 августа 2017 года. Чтение hello [объявления](https://go.microsoft.com/fwlink/?linkid=821148) подробные сведения.
> 
> 

Перенаправление устройств пользователи могут взаимодействовать с удаленными приложениями с помощью hello устройств вложенного tootheir локального компьютера, телефон или планшет. Например при указании Скайп через Azure RemoteApp пользователю необходимо установлен на их ПК toowork с Скайп камеры hello. Это также касается принтеров, динамиков, мониторов и периферийных устройств, подключенных через порт USB.

RemoteApp использует hello удаленного рабочего стола (RDP) и RemoteFX tooprovide перенаправление.

## <a name="what-redirection-is-enabled-by-default"></a>Какое перенаправление включено по умолчанию?
При использовании удаленных приложений RemoteApp, по умолчанию включены следующие перенаправлений hello. сведения Hello в скобках указывают на приветствия протокола удаленного рабочего СТОЛА.

* Воспроизведение звуков на локальном компьютере hello (**проигрывать на этом компьютере**). (audiomode:i:0)
* Запись звука с локального компьютера hello и отправки toohello удаленного компьютера (**записать с этого компьютера**). (audiocapturemode:i:1)
* Печать toolocal принтеры (redirectprinters:i:1)
* COM-порты (redirectcomports:i:1)
* Устройства чтения смарт-карт (redirectsmartcards:i:1)
* Буфер обмена (возможность toocopy и вставить) (redirectclipboard:i:1)
* Очистить сглаживания шрифтов (allow font smoothing:i:1)
* Перенаправление всех поддерживаемых самонастраивающихся устройств. (devicestoredirect:s: *)

## <a name="what-other-redirection-is-available"></a>Какие еще перенаправления доступны?
Два параметра перенаправления по умолчанию отключены:

* Перенаправление дисков (сопоставление дисков): диски локального компьютера становятся подключенные сетевые диски в удаленном сеансе hello. Это позволяет при сохранении или файлы, открытые на локальных дисках, при работе в удаленном сеансе hello.
* USB-перенаправления: hello устройства USB вложенного tooyour локального компьютера можно использовать в рамках удаленного сеанса hello.

## <a name="change-your-redirection-settings-in-remoteapp"></a>Изменение настроек перенаправления в удаленном приложении RemoteApp
Параметры перенаправления hello устройств для коллекции можно изменить с помощью hello Microsoft Azure PowerShell с помощью пакета SDK. После установки hello новый PowerShell и пакет SDK, настроить его toomanage вашей подписки, как описано в [как tooinstall и настройка Azure PowerShell](/powershell/azure/overview).

Выполните команду аналогичные toohello, следующие пользовательские свойства протокола удаленного рабочего СТОЛА tooset hello.

    Set-AzureRemoteAppCollection -CollectionName <collection name>  -CustomRdpProperty "drivestoredirect:s:*`nusbdevicestoredirect:s:*"

(Обратите внимание, что  *`n*  используется в качестве разделителя между отдельными свойствами.)

tooget список настроены какие настраиваемые свойства протокола удаленного рабочего СТОЛА, запустите следующий командлет hello. Обратите внимание, что только пользовательские свойства отображаются в виде выходных результатов не hello свойства по умолчанию:  

    Get-AzureRemoteAppCollection -CollectionName <collection name>

При установке пользовательских свойств необходимо указать все пользовательские свойства каждый раз; в противном случае приветствия возвращается toodisabled.   

### <a name="common-examples"></a>Распространенные примеры
Используйте следующий командлет перенаправление дисков tooenable hello.  

    Set-AzureRemoteAppCollection -CollectionName <collection name>  -CustomRdpProperty "drivestoredirect:s:*"

Используйте этот командлет tooenable USB и диск перенаправление:

    Set-AzureRemoteAppCollection -CollectionName <collection name>  -CustomRdpProperty "drivestoredirect:s:*`nusbdevicestoredirect:s:*"

Используйте этот командлет toodisable совместное использование буфера обмена:  

    Set-AzureRemoteAppCollection -CollectionName <collection name>  -CustomRdpProperty "redirectclipboard:i:0"

> [!IMPORTANT]
> Быть toocompletely убедиться, что выход из системы всех пользователей в коллекции hello (и не только их отключения) перед началом тестирования изменений hello. Пользователи tooensure полностью вышли из системы, последовательно выберите toohello **сеансы** в коллекции hello в hello портал Azure и выйдите из системы все пользователи, не отключены и не выполнил вход. Иногда может потребоваться несколько секунд, tooshow hello локальные диски в проводнике в рамках сеанса hello.
> 
> 

## <a name="change-usb-redirection-settings-on-your-windows-client"></a>Изменение настроек перенаправления USB на клиенте Windows
Следует toouse USB-перенаправления на компьютере, который подключается tooRemoteApp существует 2 действия, которые должны toohappen. 1 — администратор должен tooenable USB-перенаправления на уровне коллекции hello с помощью Azure PowerShell. 2 — на каждом устройстве, где требуется toouse USB-перенаправления необходимо tooenable групповой политики, которая позволяет использовать его. Этот шаг потребуется выполнить для каждого пользователя, который хочет toouse USB-перенаправления toobe.

> [!NOTE]
> Перенаправление USB с помощью удаленного приложения Azure RemoteApp поддерживается только на компьютерах под управлением Windows.
> 
> 

### <a name="enable-usb-redirection-for-hello-remoteapp-collection"></a>Разрешить USB-перенаправления для hello коллекции RemoteApp
Используйте следующий командлет tooenable USB-перенаправления на уровне коллекции hello hello.

    Set-AzureRemoteAppCollection -CollectionName <collection_name> -CustomRdpProperty "nusbdevicestoredirect:s:*"

### <a name="enable-usb-redirection-for-hello-client-computer"></a>Разрешить USB-перенаправления для hello клиентского компьютера
Параметры перенаправления tooconfigure USB на компьютере:

1. Привет открыть редактор локальных групповых политик (GPEDIT. MSC). (Из командной строки запустите команду gpedit.msc.)
2. Откройте папку **Computer Configuration\Policies\Administrative Templates\Windows Components\Remote Desktop Services\Remote Desktop Connection Client\RemoteFX USB Device Redirection**.
3. Дважды щелкните **Разрешить перенаправление RDP других поддерживаемых устройств RemoteFX USB на этом компьютере**.
4. Выберите **включено**, а затем выберите **администраторов и пользователей в hello права доступа для перенаправления USB RemoteFX**.
5. Откройте командную строку с правами администратора и выполните следующую команду hello:
   
        gpupdate /force
6. Перезагрузите компьютер hello.

Можно также использовать toocreate средство управления групповой политикой hello и применить политику перенаправления hello USB для всех компьютеров в домене:

1. Войдите на контроллер домена hello в качестве администратора домена hello.
2. Здравствуйте, откройте консоль управления групповыми политиками. (Щелкните **Пуск > Администрирование > Управление групповой политикой**.)
3. Перейдите toohello домен или подразделение, для которого требуется политика toocreate hello.
4. Щелкните правой кнопкой мыши **Default Domain Policy** (Политика домена по умолчанию), а затем нажмите кнопку **Изменить**.
5. Откройте папку **Computer Configuration\Policies\Administrative Templates\Windows Components\Remote Desktop Services\Remote Desktop Connection Client\RemoteFX USB Device Redirection**.
6. Дважды щелкните **Разрешить перенаправление RDP других поддерживаемых устройств RemoteFX USB на этом компьютере**.
7. Выберите **включено**, а затем выберите **администраторов и пользователей в hello права доступа для перенаправления USB RemoteFX**.
8. Нажмите кнопку **ОК**.  

