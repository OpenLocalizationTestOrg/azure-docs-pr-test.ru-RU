---
title: "пакет поддержки StorSimple aaaCreate | Документы Microsoft"
description: "Узнайте, как toocreate, расшифровки и изменить пакет поддержки для устройства StorSimple."
services: storsimple
documentationcenter: 
author: alkohli
manager: carmonm
editor: 
ms.assetid: eac76f5f-5db1-4c92-af8c-54053b91e66c
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/17/2016
ms.author: alkohli
ms.openlocfilehash: 209aeee50e823fd2ca96ababd1d0cf3ea9cdad53
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-a-storsimple-support-package"></a>Создание пакетов поддержки StorSimple и управление ими
## <a name="overview"></a>Обзор
Пакет поддержки StorSimple — это простой в использовании механизм, который собирает все журналы tooassist технической поддержки Майкрософт с устранить любые проблемы устройства StorSimple. Hello собирать журналы зашифрованные и сжатые.

Этот учебник включает toocreate пошаговые инструкции и управление ими hello пакет поддержки.

## <a name="create-and-upload-a-support-package-in-hello-azure-classic-portal"></a>Создание и отправка пакета поддержки в hello классический портал Azure
Можно создать и отправить узле поддержки toohello пакета поддержки корпорации Майкрософт с помощью hello **обслуживания** странице службы hello в hello классический портал Azure.

> [!NOTE]
> Отправка Hello требуется ключ доступа поддержки. Специалисту службы поддержки должен предоставить этот tooyou по электронной почте.
> 
> 

Пакет поддержки зашифрованные и сжатые (CAB-файл)-это созданный и загруженный toohello сайт технической поддержки. Сотрудник службы поддержки Hello может найти этот пакет с сайта поддержки hello для устранения проблемы hello.

Выполнение инструкций из классического портала toocreate hello пакет поддержки hello.

#### <a name="toocreate-a-support-package-in-hello-azure-classic-portal"></a>toocreate пакета поддержки в hello классический портал Azure
1. Выберите **Устройства** > **Обслуживание**.
2. В hello **пакет поддержки** выберите **Создание и отправка пакета поддержки**.
3. В hello **Создание и отправка пакета поддержки** диалогового окна поле, hello следующие:
   
    ![Создание пакета поддержки](./media/storsimple-create-manage-support-package/IC740923.png)
   
   * В hello **к поддержке** текста введите ключ доступа hello. Специалисту службы поддержки Майкрософт должна отправлять этот ключ доступа tooyou в сообщении электронной почты.
   * Выберите hello флажок tooprovide согласия tooautomatically передачи поддержки hello пакета toohello сайт технической поддержки Майкрософт.
   * Щелкните значок галочки hello ![значок с изображением флажка](./media/storsimple-create-manage-support-package/IC740895.png).

## <a name="manually-create-a-support-package"></a>Создание пакета поддержки вручную
В некоторых случаях вам потребуется toomanually создать пакет поддержки hello через Windows PowerShell для StorSimple. Например:

* Если необходимо tooremove конфиденциальные сведения из журналов файлы предыдущих toosharing со службой поддержки Майкрософт.
* Если вам трудно Отправка hello пакета из-за проблем с tooconnectivity.

Созданный вручную пакет поддержки можно предоставить службе технической поддержки Майкрософт по электронной почте. Выполните следующие шаги toocreate пакета поддержки в Windows PowerShell для StorSimple hello.

#### <a name="toocreate-a-support-package-in-windows-powershell-for-storsimple"></a>toocreate пакета поддержки в Windows PowerShell для StorSimple
1. toostart сеанс Windows PowerShell с правами администратора на удаленном компьютере hello, который использовал устройства StorSimple tooyour tooconnect, введите следующую команду hello:
   
    `Start PowerShell`
2. В сеансе Windows PowerShell hello подключение toohello консоли SSAdmin на устройстве:
   
   * Hello командной строки введите:
     
       `$MS = New-PSSession -ComputerName <IP address for DATA 0> -Credential SSAdmin -ConfigurationName "SSAdminConsole"`
   * В hello открывшемся диалоговом окне введите пароль администратора устройства. пароль по умолчанию Hello —:
     
      `Password1`
     
      ![Диалоговое окно с учетными данными PowerShell](./media/storsimple-create-manage-support-package/IC740962.png)
   * Нажмите кнопку **ОК**.
   * Hello командной строки введите:
     
      `Enter-PSSession $MS`
3. В открывшемся сеансе hello введите соответствующую команду hello.
   
   * Для сетевых ресурсов, которые защищены паролем, введите:
     
       `Export-HcsSupportPackage –PackageTag "MySupportPackage" –Credential "Username" -Force`
     
       Вам будет выведен на пароль, путь toohello общую сетевую папку и парольную фразу для шифрования (поскольку hello пакет поддержки зашифрован). Затем создается пакет поддержки в указанную папку hello.
   * Для общих папок, которые не защищен паролем, нет необходимости hello `-Credential` параметра. Введите hello следующие данные:
     
       `Export-HcsSupportPackage –PackageTag "MySupportPackage" -Force`
     
       для обоих контроллеров в hello указанной общей сетевой папке создается пакет поддержки Hello. Это зашифрованный, сжатый файл, который может быть отправлен tooMicrosoft поддержки для устранения неполадок. Дополнительные сведения см. в статье [Обращение в службу поддержки Майкрософт](storsimple-contact-microsoft-support.md).

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
> Изменить можно только пакет поддержки, который был создан через Windows PowerShell для StorSimple. Невозможно изменить пакет, созданный на hello классический портал Azure в службе StorSimple Manager.
> 
> 

tooedit пакет поддержки до отправки на сайт технической поддержки Microsoft hello, сначала расшифровать пакет поддержки hello, изменять файлы hello и повторно зашифровать. Выполните следующие шаги hello.

#### <a name="tooedit-a-support-package-in-windows-powershell-for-storsimple"></a>tooedit пакета поддержки в Windows PowerShell для StorSimple
1. Создать пакет поддержки, как описано ранее в [toocreate пакет поддержки в Windows PowerShell для StorSimple](#to-create-a-support-package-in-windows-powershell-for-storsimple).
2. [Загрузка скрипта hello](http://gallery.technet.microsoft.com/scriptcenter/Script-to-decrypt-a-a8d1ed65) локально на клиентском компьютере.
3. Импортируйте модуль Windows PowerShell hello. Укажите hello путь toohello локальной папке в которой был загружен скрипт hello. модуль hello tooimport, введите:
   
    `Import-module <Path toohello folder that contains hello Windows PowerShell script>`
4. Все файлы hello, *.aes* файлы, которые сжаты и зашифрованы. toodecompress и расшифровки файлов, введите:
   
    `Open-HcsSupportPackage <Path toohello folder that contains support package files>`
   
    Обратите внимание, для всех файлов hello теперь отображаются фактические расширения hello.
   
    ![Изменение пакета поддержки](./media/storsimple-create-manage-support-package/IC750706.png)
5. Когда появится для hello парольную фразу для шифрования, введите hello парольную фразу, которая использовалась при создании пакета поддержки hello.
   
        cmdlet Open-HcsSupportPackage at command pipeline position 1
   
        Supply values for hello following parameters:EncryptionPassphrase: ****
6. Обзор toohello папки, содержащей файлы журналов hello. Поскольку файлы журнала hello распакованы и расшифрованы, это будет иметь исходное расширение файла. Изменять эти файлы tooremove сведений о конкретных клиентов, такие как имена томов и IP-адреса устройств и сохранять файлы hello.
7. Закрыть hello файлы toocompress их с помощью gzip и их шифрования с помощью AES-256. Это необходимо для скорости и безопасности при передаче пакета поддержки hello по сети. toocompress и шифрование файлов, введите ниже hello:
   
    `Close-HcsSupportPackage <Path toohello folder that contains support package files>`
   
    ![Изменение пакета поддержки](./media/storsimple-create-manage-support-package/IC750707.png)
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
* Узнайте, каким образом слишком[пакеты поддержки использования и устройства в журналах tootroubleshoot развертывания устройства](storsimple-troubleshoot-deployment.md#support-packages-and-device-logs-available-for-troubleshooting).
* Узнайте, каким образом слишком[используйте hello tooadminister службы диспетчера StorSimple устройство StorSimple](storsimple-manager-service-administration.md).

