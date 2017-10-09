---
title: "aaaConnect удаленное устройство StorSimple tooyour | Документы Microsoft"
description: "Объясняет, как tooconfigure устройства для удаленного управления и как tooconnect tooWindows PowerShell для StorSimple через HTTP или HTTPS."
services: storsimple
documentationcenter: 
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 04/07/2017
ms.author: alkohli
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 38b6a6350891b9f6f8fdfc55880b2f47105d947c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="connect-remotely-tooyour-storsimple-8000-series-device"></a>Удаленное подключение устройства серии StorSimple 8000 tooyour

## <a name="overview"></a>Обзор

Вы можете удаленно подключиться tooyour устройство с помощью Windows PowerShell. При таком способе подключения меню не отображается. (Вы увидеть меню только в том случае, если вы используете hello последовательной консоли на устройстве tooconnect hello.) С помощью удаленного взаимодействия Windows PowerShell подключитесь tooa определенной среде выполнения. Можно также указать язык отображения приветствия.

Дополнительные сведения об использовании toomanage удаленного взаимодействия Windows PowerShell устройства go слишком[с помощью Windows PowerShell для StorSimple tooadminister устройства StorSimple](storsimple-8000-windows-powershell-administration.md).

В этом учебнике описано как tooconfigure устройства для удаленного управления и затем как tooconnect tooWindows PowerShell для StorSimple. Можно использовать HTTP или HTTPS tooremotely подключаться с помощью Windows PowerShell. Тем не менее, при определении как tooconnect tooWindows PowerShell для StorSimple, рассмотрим hello следующую информацию:

* Непосредственное подключение toohello последовательной консоли устройства защищено, но подключения последовательной консоли toohello через сетевые коммутаторы не. Тщательно hello угрозу безопасности при соединении через сетевые коммутаторы toohello последовательной консоли устройства.
* Подключение через сеанс HTTP является более безопасным, чем подключение через последовательную консоль hello hello сети. Несмотря на то, что это не самый безопасный метод hello, он допустим для надежных сетей.
* Hello наиболее безопасный и рекомендуемый параметр hello является подключение посредством сеанса HTTPS с самозаверяющим сертификатом.

Можно удаленно подключиться toohello интерфейс Windows PowerShell. Однако устройства StorSimple tooyour удаленного доступа через интерфейс Windows PowerShell hello не включается по умолчанию. Необходимо сначала включить удаленное управление на устройстве hello и затем на hello клиента, который будет использоваться tooaccess устройства.

Hello действия, описанные в этой статье были выполнены в системе узла под управлением Windows Server 2012 R2.

## <a name="connect-through-http"></a>Подключение по протоколу HTTP

Подключение tooWindows PowerShell для StorSimple через сеанс HTTP является более безопасным, чем подключение через последовательную консоль устройства StorSimple hello. Несмотря на то, что это не самый безопасный метод hello, он допустим для надежных сетей.

Можно использовать либо hello Azure portal или hello последовательной консоли tooconfigure удаленного управления. Выберите один из следующих процедур hello.

* [Использовать hello Azure портала tooenable удаленное управление по протоколу HTTP](#use-the-azure-classic-portal-to-enable-remote-management-over-http)
* [Используйте hello последовательной консоли tooenable удаленное управление по протоколу HTTP](#use-the-serial-console-to-enable-remote-management-over-http)

После включения удаленного управления, используйте hello, выполнив процедуру tooprepare hello клиента для удаленного подключения.

* [Подготовка hello клиента для удаленного подключения](#prepare-the-client-for-remote-connection)

### <a name="use-hello-azure-portal-tooenable-remote-management-over-http"></a>Использовать hello Azure портала tooenable удаленное управление по протоколу HTTP

Выполните следующие шаги в hello Azure портала tooenable удаленное управление по протоколу HTTP hello.

#### <a name="tooenable-remote-management-through-hello-azure-portal"></a>удаленное управление tooenable через портал Azure hello

1. Перейдите в службе диспетчера StorSimple устройство tooyour. Выберите **устройств** и затем выберите и щелкните hello устройство tooconfigure для удаленного управления. Go слишком**параметры устройства > безопасности**.
2. В hello **параметры безопасности** колонка, щелкните **удаленного управления**.
3. В hello **удаленного управления** задать колонке **Включение удаленного управления** слишком**Да**.
4. Теперь вы можете tooconnect с помощью протокола HTTP. (по умолчанию hello — tooconnect по протоколу HTTPS). Убедитесь, что выбран HTTP.
   
   > [!NOTE]
   > Подключение по HTTP допустимо только в доверенных сетях.
   
5. Щелкните **Сохранить**, а затем щелкните **Да**, когда появится запрос на подтверждение.

### <a name="use-hello-serial-console-tooenable-remote-management-over-http"></a>Используйте hello последовательной консоли tooenable удаленное управление по протоколу HTTP
Выполните следующие шаги на удаленное управление последовательной консоли устройства tooenable hello hello.

#### <a name="tooenable-remote-management-through-hello-device-serial-console"></a>удаленное управление tooenable через последовательную консоль устройства hello
1. В меню последовательной консоли hello выберите вариант 1. Дополнительные сведения об использовании последовательной консоли hello на устройстве hello go слишком[подключения tooWindows PowerShell для StorSimple через последовательную консоль устройства](storsimple-8000-windows-powershell-administration.md#connect-to-windows-powershell-for-storsimple-via-the-device-serial-console).
2. Привет введите в строке:`Enable-HcsRemoteManagement –AllowHttp`
3. Вы будете оповещены об уязвимостях безопасности с помощью HTTP tooconnect toohello устройства hello. При появлении запроса подтверждения введите **Y**.
4. Убедитесь, что HTTP включен, набрав: `Get-HcsSystem`
5. Убедитесь, что hello **RemoteManagementMode** отображается **HttpsAndHttpEnabled**.hello следующие иллюстрации показаны эти параметры в PuTTY.
   
     ![Последовательный HTTPS и HTTP включены](./media/storsimple-remote-connect/HCS_SerialHttpsAndHttpEnabled.png)

### <a name="prepare-hello-client-for-remote-connection"></a>Подготовка hello клиента для удаленного подключения
Выполните следующие шаги на приветствия клиента tooenable удаленного управления hello.

#### <a name="tooprepare-hello-client-for-remote-connection"></a>tooprepare hello клиента для удаленного подключения
1. Запустите сеанс Windows PowerShell от имени администратора.
2. Тип hello следующая команда tooadd hello IP-адрес устройства toohello hello StorSimple клиента списку доверенных узлов:
   
     `Set-Item wsman:\localhost\Client\TrustedHosts <device_ip> -Concatenate -Force`
   
     Замените <*device_ip*> hello IP-адрес устройства, например: 
   
     `Set-Item wsman:\localhost\Client\TrustedHosts 10.126.173.90 -Concatenate -Force`
3. Тип hello следующая команда toosave hello устройство и учетные данные в переменной: 
   
    ```
    $cred = Get-Credential
    ```
    
4. В диалоговом окне приветствия, которая отображается:
   
   1. Введите имя пользователя hello в следующем формате: *device_ip\SSAdmin*.
   2. Введите пароль администратора устройства hello, который был задан при настройке устройства hello с приветствия мастера установки. пароль по умолчанию Hello — *Password1*.
5. Запустите сеанс Windows PowerShell на устройстве hello, введя следующую команду:
   
     `Enter-PSSession -Credential $cred -ConfigurationName SSAdminConsole -ComputerName <device_ip>`
   
   > [!NOTE]
   > toocreate сеанс Windows PowerShell для использования с виртуального устройства StorSimple hello append hello `–Port` параметра и укажите общий порт hello, настроенные для виртуального устройства StorSimple в системе удаленного взаимодействия.
   
   
На этом этапе необходимо активного устройства toohello удаленного сеанса Windows PowerShell.
   
![Удаленное взаимодействие PowerShell через HTTP](./media/storsimple-remote-connect/HCS_PSRemotingUsingHTTP.png)

## <a name="connect-through-https"></a>Подключение по протоколу HTTPS

Подключение tooWindows PowerShell для StorSimple через сеанс HTTPS — наиболее безопасный hello и рекомендуется использовать метод Microsoft Azure StorSimple устройство удаленно подключения tooyour. Hello следующих процедур объясняется, как tooset копирование hello последовательную консоль и клиентские компьютеры, чтобы можно было использовать HTTPS tooconnect tooWindows PowerShell для StorSimple.

Можно использовать либо hello Azure portal или hello последовательной консоли tooconfigure удаленного управления. Выберите один из следующих процедур hello.

* [Использовать hello Azure портала tooenable удаленное управление по протоколу HTTPS](#use-the-azure-classic-portal-to-enable-remote-management-over-https)
* [Использовать hello последовательной консоли tooenable удаленное управление по протоколу HTTPS](#use-the-serial-console-to-enable-remote-management-over-https)

После включения удаленного управления, используйте следующие процедуры tooprepare hello узлов для удаленного управления hello и подключить устройство toohello от удаленного хоста hello.

* [Подготовка узла hello для удаленного управления](#prepare-the-host-for-remote-management)
* [Подключите устройство toohello от удаленного хоста hello](#connect-to-the-device-from-the-remote-host)

### <a name="use-hello-azure-portal-tooenable-remote-management-over-https"></a>Использовать hello Azure портала tooenable удаленное управление по протоколу HTTPS

Выполните следующие шаги в hello Azure портала tooenable удаленное управление по протоколу HTTPS hello.

#### <a name="tooenable-remote-management-over-https-from-hello-azure-portal"></a>удаленное управление по протоколу HTTPS из портала Azure hello tooenable

1. Перейдите в службе диспетчера StorSimple устройство tooyour. Выберите **устройств** и затем выберите и щелкните hello устройство tooconfigure для удаленного управления. Go слишком**параметры устройства > безопасности**.
2. В hello **параметры безопасности** колонка, щелкните **удаленного управления**.
3. Задать **Включение удаленного управления** слишком**Да**.
4. Теперь вы можете tooconnect с помощью протокола HTTPS. (по умолчанию hello — tooconnect по протоколу HTTPS). Убедитесь, что выбран HTTPS.
5. Щелкните многоточие (…), а затем выберите **Загрузить сертификат удаленного управления**. Укажите toosave расположение этого файла. Необходимо tooinstall этот сертификат на компьютере клиента или узла hello, который будет использоваться tooconnect toohello устройства.
6. Нажмите кнопку **Сохранить**, а затем щелкните **Да**, когда появится запрос на подтверждение.

### <a name="use-hello-serial-console-tooenable-remote-management-over-https"></a>Использовать hello последовательной консоли tooenable удаленное управление по протоколу HTTPS

Выполните следующие шаги на удаленное управление последовательной консоли устройства tooenable hello hello.

#### <a name="tooenable-remote-management-through-hello-device-serial-console"></a>удаленное управление tooenable через последовательную консоль устройства hello
1. В меню последовательной консоли hello выберите вариант 1. Дополнительные сведения об использовании последовательной консоли hello на устройстве hello go слишком[подключения tooWindows PowerShell для StorSimple через последовательную консоль устройства](storsimple-8000-windows-powershell-administration.md#connect-to-windows-powershell-for-storsimple-via-the-device-serial-console).
2. Привет введите в строке:
   
     `Enable-HcsRemoteManagement`
   
    Эта команда должна включить протокол HTTPS на вашем устройстве.
3. Убедитесь, что HTTPS включен, набрав: 
   
     `Get-HcsSystem`
   
    Убедитесь в том, что hello **RemoteManagementMode** отображается **HttpsEnabled**.hello следующие иллюстрации показаны эти параметры в PuTTY.
   
     ![Последовательный HTTPS включен](./media/storsimple-remote-connect/HCS_SerialHttpsEnabled.png)
4. Из вывода hello `Get-HcsSystem`, скопируйте серийный номер устройства hello hello и сохранить его для последующего использования.
   
   > [!NOTE]
   > серийный номер Hello указывает toohello CN-имени в сертификате hello.
   
5. Получите сертификат удаленного управления, набрав: 
   
     `Get-HcsRemoteManagementCert`
   
    Появится сертификат аналогичные toohello следующее.
   
    ![Получение сертификата удаленного управления](./media/storsimple-remote-connect/HCS_GetRemoteManagementCertificate.png)
6. Скопируйте hello сведения в сертификате hello **---BEGIN CERTIFICATE---** слишком**---конечный СЕРТИФИКАТ---** в текстовый редактор, например Блокнот и сохраните его как файл CER. (Необходимо будет скопировать этот файл tooyour удаленного узла при подготовке узла hello.)
   
   > [!NOTE]
   > toogenerate новый сертификат, используйте hello `Set-HcsRemoteManagementCert` командлета.
   
### <a name="prepare-hello-host-for-remote-management"></a>Подготовка узла hello для удаленного управления

tooprepare hello главного компьютера для удаленного подключения, которое использует сеанс HTTPS выполните hello следующих процедур.

* [Импортировать файл .cer hello в корневое хранилище hello hello клиента или удаленного узла](#to-import-the-certificate-on-the-remote-host).
* [Добавьте файл hosts toohello серийные номера устройств hello на удаленном узле](#to-add-device-serial-numbers-to-the-remote-host).

Каждый из предыдущих процедур, hello описан ниже.

#### <a name="tooimport-hello-certificate-on-hello-remote-host"></a>tooimport hello сертификата удаленного узла hello
1. Щелкните правой кнопкой мыши hello CER-файл и выберите **установить сертификат**. Запустится мастер импорта сертификатов hello.
   
    ![Мастер импорта сертификатов 1](./media/storsimple-remote-connect/HCS_CertificateImportWizard1.png)
2. В качестве **Расположения хранилища** выберите **Локальный компьютер**, а затем нажмите кнопку **Далее**.
3. Выберите **поместить все сертификаты в следующие хранилища hello**, а затем нажмите кнопку **Обзор**. Перейдите в удаленный узел toohello корневое хранилище и нажмите кнопку **Далее**.
   
    ![Мастер импорта сертификатов 2](./media/storsimple-remote-connect/HCS_CertificateImportWizard2.png)
4. Нажмите кнопку **Готово** Появится сообщение, информирующее о том, что hello Импорт успешно выполнен.
   
    ![Мастер импорта сертификатов 3](./media/storsimple-remote-connect/HCS_CertificateImportWizard3.png)

#### <a name="tooadd-device-serial-numbers-toohello-remote-host"></a>удаленный узел серийные номера устройств toohello tooadd
1. Откройте Блокнот от имени администратора, а затем откройте файл hosts hello, расположенный в \Windows\System32\Drivers\etc.
2. Добавьте следующие три файла hosts записи tooyour hello: **DATA 0 IP-адрес**, **фиксированный IP-адрес контроллера 0**, и **фиксированный IP-адрес контроллера 1 адрес**.
3. Введите серийный номер устройства hello сохраненный ранее. Сопоставьте этот IP-адрес toohello, как показано в hello после изображения. Для контроллера 0 и 1, добавьте **Controller0** и **Controller1** в конце hello hello серийный номер (CN-имя).
   
    ![Добавление файла toohosts CN-имени](./media/storsimple-remote-connect/HCS_AddingCNNameToHostsFile.png)
4. Сохранить файл hosts hello.

### <a name="connect-toohello-device-from-hello-remote-host"></a>Подключите устройство toohello от удаленного хоста hello

Использование Windows PowerShell и SSL tooenter сеанс SSAdmin на устройстве с удаленного узла или клиента. Hello сеанс SSAdmin сопоставляется toooption 1 в hello [последовательной консоли](storsimple-8000-windows-powershell-administration.md#connect-to-windows-powershell-for-storsimple-via-the-device-serial-console) меню вашего устройства.

Выполните процедуру, приведенную на компьютере hello, с которого будет осуществляться удаленное подключение Windows PowerShell toomake hello hello.

#### <a name="tooenter-an-ssadmin-session-on-hello-device-by-using-windows-powershell-and-ssl"></a>tooenter сеанс SSAdmin на устройстве hello с помощью Windows PowerShell и SSL
1. Запустите сеанс Windows PowerShell от имени администратора.
2. Добавьте hello устройства IP адрес toohello доверенные узлы клиента введя:
   
     `Set-Item wsman:\localhost\Client\TrustedHosts <device_ip> -Concatenate -Force`
   
    Где <*device_ip*> hello IP-адрес устройства, например: 
   
     `Set-Item wsman:\localhost\Client\TrustedHosts 10.126.173.90 -Concatenate -Force`
3. toocreate новые учетные данные, введите следующую команду:
   
     `$cred = New-Object pscredential @("<IP of target device>\SSAdmin", (ConvertTo-SecureString -Force -AsPlainText "<Device Administrator Password>"))`
   
    Где <*IP-адрес целевого устройства*> — hello IP-адрес DATA 0 для устройства, например, **10.126.173.90** как показано в предшествующих образ файла hosts hello hello. Также укажите пароль администратора hello для вашего устройства.
4. Создайте сеанс, набрав:
   
     `$session = New-PSSession -UseSSL -ComputerName <Serial number of target device> -Credential $cred -ConfigurationName "SSAdminConsole"`
   
    Для параметра - ComputerName hello в командлете hello, предоставляют hello <*серийный номер целевого устройства*>. Этот серийный номер был сопоставлен toohello IP-адрес DATA 0 в файле hosts hello на удаленном узле; например **SHX0991003G44MT** как показано в hello после изображения.
5. Тип:
   
     `Enter-PSSession $session`
6. Toowait потребуется несколько минут и затем будет tooyour подключенного устройства через HTTPS по протоколу SSL. Появится сообщение о том, что вы являетесь tooyour подключенных устройств.
   
    ![Удаленное взаимодействие PowerShell через HTTPS и SSL](./media/storsimple-remote-connect/HCS_PSRemotingUsingHTTPSAndSSL.png)

## <a name="next-steps"></a>Дальнейшие действия

* Дополнительные сведения о [с помощью tooadminister Windows PowerShell устройства StorSimple](storsimple-8000-windows-powershell-administration.md).
* Дополнительные сведения о [с помощью hello tooadminister службы диспетчера StorSimple устройство устройства StorSimple](storsimple-8000-manager-service-administration.md).

