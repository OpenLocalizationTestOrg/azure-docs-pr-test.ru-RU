---
title: "пакет поддержки серии StorSimple 8000 aaaCreate | Документы Microsoft"
description: "Узнайте, как toocreate, расшифровки и изменить пакет поддержки для вашего устройства серии StorSimple 8000."
services: storsimple
documentationcenter: 
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/05/2017
ms.author: alkohli
ms.openlocfilehash: 857555b6ba31b1527f8f00d19818ebbec6005d0e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-a-support-package-for-storsimple-8000-series"></a>Создание пакета поддержки StorSimple для устройства StorSimple серии 8000 и управление им

## <a name="overview"></a>Обзор

Пакет поддержки StorSimple — это простой в использовании механизм, который собирает все журналы tooassist технической поддержки Майкрософт с устранить любые проблемы устройства StorSimple. Hello собирать журналы зашифрованные и сжатые.

Этот учебник включает toocreate пошаговые инструкции и управление ими hello пакет поддержки для вашего устройства серии StorSimple 8000. При работе с StorSimple Virtual Array go слишком[создания пакета журналов](storsimple-ova-web-ui-admin.md#generate-a-log-package).

## <a name="create-a-support-package"></a>Создать пакет поддержки.

В некоторых случаях вам потребуется toomanually создать пакет поддержки hello через Windows PowerShell для StorSimple. Например:

* Если необходимо tooremove конфиденциальные сведения из журналов файлы предыдущих toosharing со службой поддержки Майкрософт.
* Если вам трудно Отправка hello пакета из-за проблем с tooconnectivity.

Созданный вручную пакет поддержки можно предоставить службе технической поддержки Майкрософт по электронной почте. Выполните следующие шаги toocreate пакета поддержки в Windows PowerShell для StorSimple hello.

#### <a name="toocreate-a-support-package-in-windows-powershell-for-storsimple"></a>toocreate пакета поддержки в Windows PowerShell для StorSimple

1. toostart сеанс Windows PowerShell с правами администратора на удаленном компьютере hello, который использовал устройства StorSimple tooyour tooconnect, введите следующую команду hello:
   
    `Start PowerShell`
2. В сеансе Windows PowerShell hello подключение toohello консоли SSAdmin на устройстве:
   
   1. Hello командной строки введите:
     
       `$MS = New-PSSession -ComputerName <IP address for DATA 0> -Credential SSAdmin -ConfigurationName "SSAdminConsole"`
   2. В hello открывшемся диалоговом окне введите пароль администратора устройства. пароль по умолчанию Hello — _Password1_.
     
      ![Диалоговое окно с учетными данными PowerShell](./media/storsimple-8000-create-manage-support-package/IC740962.png)
   3. Нажмите кнопку **ОК**.
   4. Hello командной строки введите:
     
      `Enter-PSSession $MS`
3. В открывшемся сеансе hello введите соответствующую команду hello.
   
   * Для сетевых ресурсов, которые защищены паролем, введите:
     
       `Export-HcsSupportPackage –PackageTag "MySupportPackage" –Credential "Username" -Force`
     
       Вам будет выведен на пароль, путь toohello общую сетевую папку и парольную фразу для шифрования (поскольку hello пакет поддержки зашифрован). Затем создается пакет поддержки в указанную папку hello.
   * Для общих папок, которые не защищен паролем, нет необходимости hello `-Credential` параметра. Введите hello следующие данные:
     
       `Export-HcsSupportPackage –PackageTag "MySupportPackage" -Force`
     
       для обоих контроллеров в hello указанной общей сетевой папке создается пакет поддержки Hello. Это зашифрованный, сжатый файл, который может быть отправлен tooMicrosoft поддержки для устранения неполадок. Дополнительные сведения см. в статье [Обращение в службу поддержки Майкрософт](storsimple-8000-contact-microsoft-support.md).

### <a name="hello-export-hcssupportpackage-cmdlet-parameters"></a>параметры командлета Export-HcsSupportPackage Hello

Можно использовать следующие параметры с помощью командлета Export-HcsSupportPackage hello hello.

| Параметр | Обязательный/необязательный | Description (Описание) |
| --- | --- | --- |
| `-Path` |Обязательно |Используйте расположение hello tooprovide hello общей сетевой папке в какой hello помещен пакет поддержки. |
| `-EncryptionPassphrase` |Обязательно |Используйте tooprovide toohelp парольной фразы шифрования пакета поддержки hello. |
| `-Credential` |Необязательно |Использование учетных данных доступа toosupply для hello общей сетевой папке. |
| `-Force` |Необязательно |Используйте шага подтверждения парольной фразы шифрования tooskip hello. |
| `-PackageTag` |Необязательно |Используйте в каталоге toospecify *путь* помещают пакет поддержки какие hello. по умолчанию Hello — [имя устройства]-[Текущая дата и время:ГГГГ-MM-дд-чч-мм-сс]. |
| `-Scope` |Необязательно |Укажите в качестве **кластера** toocreate (по умолчанию) пакет поддержки для обоих контроллеров. Toocreate пакета только для текущего контроллера hello, укажите **контроллера**. |

## <a name="edit-a-support-package"></a>Изменение пакета поддержки

После создания пакета поддержки может понадобиться tooedit hello tooremove конфиденциальных сведений о пакете. Это может включать имена томов, IP-адреса устройств и имена резервных копий из файлов журнала hello.

> [!IMPORTANT]
> Изменить можно только пакет поддержки, который был создан через Windows PowerShell для StorSimple. Невозможно изменить пакет, созданный на портал Azure в службе диспетчера StorSimple устройство hello.

tooedit пакет поддержки до отправки на сайт технической поддержки Microsoft hello, сначала расшифровать пакет поддержки hello, изменять файлы hello и повторно зашифровать. Выполните следующие шаги hello.

#### <a name="tooedit-a-support-package-in-windows-powershell-for-storsimple"></a>tooedit пакета поддержки в Windows PowerShell для StorSimple

1. Создать пакет поддержки, как описано ранее в [toocreate пакет поддержки в Windows PowerShell для StorSimple](#to-create-a-support-package-in-windows-powershell-for-storsimple).
2. [Загрузка скрипта hello](http://gallery.technet.microsoft.com/scriptcenter/Script-to-decrypt-a-a8d1ed65) локально на клиентском компьютере.
3. Импортируйте модуль Windows PowerShell hello. Укажите hello путь toohello локальной папке в которой был загружен скрипт hello. модуль hello tooimport, введите:
   
    `Import-module <Path toohello folder that contains hello Windows PowerShell script>`
4. Все файлы hello, *.aes* файлы, которые сжаты и зашифрованы. toodecompress и расшифровки файлов, введите:
   
    `Open-HcsSupportPackage <Path toohello folder that contains support package files>`
   
    Обратите внимание, для всех файлов hello теперь отображаются фактические расширения hello.
   
    ![Изменение пакета поддержки](./media/storsimple-8000-create-manage-support-package/IC750706.png)
5. Когда появится для hello парольную фразу для шифрования, введите hello парольную фразу, которая использовалась при создании пакета поддержки hello.
   
        cmdlet Open-HcsSupportPackage at command pipeline position 1
   
        Supply values for hello following parameters:EncryptionPassphrase: ****
6. Обзор toohello папки, содержащей файлы журналов hello. Поскольку файлы журнала hello распакованы и расшифрованы, это будет иметь исходное расширение файла. Изменять эти файлы tooremove сведений о конкретных клиентов, такие как имена томов и IP-адреса устройств и сохранять файлы hello.
7. Закрыть hello файлы toocompress их с помощью gzip и их шифрования с помощью AES-256. Это необходимо для скорости и безопасности при передаче пакета поддержки hello по сети. toocompress и шифрование файлов, введите ниже hello:
   
    `Close-HcsSupportPackage <Path toohello folder that contains support package files>`
   
    ![Изменение пакета поддержки](./media/storsimple-8000-create-manage-support-package/IC750707.png)
8. При появлении запроса введите парольную фразу для hello измененного пакета поддержки.
   
        cmdlet Close-HcsSupportPackage at command pipeline position 1
        Supply values for hello following parameters:EncryptionPassphrase: ****
9. Запишите hello новую парольную фразу, чтобы совместно использовать его службе технической поддержки Майкрософт по запросу.

### <a name="example-editing-files-in-a-support-package-on-a-password-protected-share"></a>Пример: изменение файлов в пакете поддержки на ресурсе, защищенном паролем

Привет, в следующем примере показано, как toodecrypt, изменения и повторного шифрования пакета поддержки.

        PS C:\WINDOWS\system32> Import-module C:\Users\Default\StorSimple\SupportPackage\HCSSupportPackageTools.psm1

        PS C:\WINDOWS\system32> Open-HcsSupportPackage \\hcsfs\Logs\TD48\TD48Logs\C0-A\etw

        cmdlet Open-HcsSupportPackage at command pipeline position 1

        Supply values for hello following parameters:

        EncryptionPassphrase: ****

        PS C:\WINDOWS\system32> Close-HcsSupportPackage \\hcsfs\Logs\TD48\TD48Logs\C0-A\etw

        cmdlet Close-HcsSupportPackage at command pipeline position 1

        Supply values for hello following parameters:

        EncryptionPassphrase: ****

        PS C:\WINDOWS\system32>

## <a name="next-steps"></a>Дальнейшие действия

* Дополнительные сведения о hello [данные, полученные из пакета поддержки hello](https://support.microsoft.com/help/3193606/storsimple-support-packages-and-device-logs)
* Узнайте, каким образом слишком[пакеты поддержки использования и устройства в журналах tootroubleshoot развертывания устройства](storsimple-troubleshoot-deployment.md#support-packages-and-device-logs-available-for-troubleshooting).
* Узнайте, каким образом слишком[используйте hello tooadminister службы диспетчера StorSimple устройство устройства StorSimple](storsimple-8000-manager-service-administration.md).

