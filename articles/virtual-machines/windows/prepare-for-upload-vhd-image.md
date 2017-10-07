---
title: "aaaPrepare tooAzure tooupload виртуального жесткого диска Windows | Документы Microsoft"
description: "Как tooprepare Windows VHD или VHDX, перед отправкой tooAzure"
services: virtual-machines-windows
documentationcenter: 
author: glimoli
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 7802489d-33ec-4302-82a4-91463d03887a
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 08/01/2017
ms.author: genli
ms.openlocfilehash: 530390e4c6a4f66ddfd4da23338f9bb3708c299f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="prepare-a-windows-vhd-or-vhdx-tooupload-tooazure"></a>Подготовка виртуального жесткого диска Windows или VHDX tooAzure tooupload
Перед отправкой виртуальных машинах (VM) из локальной tooMicrosoft Azure, необходимо подготовить hello виртуального жесткого диска (VHD или VHDX). Azure поддерживает только первого поколения виртуальных машин, которые находятся в формате VHD hello и фиксированного размера диска. Максимальный размер Hello разрешена для hello виртуального жесткого диска — 1023 ГБ. Вы можете преобразовать поколение 1 виртуальной Машины из hello VHDX файла tooVHD системы и с динамически расширяемый диска toofixed нулевого размера. Но вы не можете изменить поколение виртуальной машины. Дополнительные сведения см. в статье о том, [как выбрать поколение для виртуальной машины в Hyper-V](https://technet.microsoft.com/windows-server-docs/compute/hyper-v/plan/should-i-create-a-generation-1-or-2-virtual-machine-in-hyper-v).

Дополнительные сведения о политике поддержки hello для виртуальной Машины Azure см. в разделе [поддержка по Microsoft server для виртуальных машин Microsoft Azure](https://support.microsoft.com/help/2721672/microsoft-server-software-support-for-microsoft-azure-virtual-machines).

> [!Note]
> инструкции Hello в данной статье применимы toohello 64-разрядной версии Windows Server 2008 R2 и более поздних версий ОС Windows server. Сведения о запуске 32-разрядной версии операционной системы в Azure см. в статье [Support for 32-bit operating systems in Azure virtual machines](https://support.microsoft.com/help/4021388/support-for-32-bit-operating-systems-in-azure-virtual-machines) (Поддержка 32-разрядных операционных систем на виртуальных машинах Azure).

## <a name="convert-hello-virtual-disk-toovhd-and-fixed-size-disk"></a>Преобразовать диск фиксированного размера и tooVHD hello виртуального диска 
Если вам требуется tooconvert вашей toohello виртуальный диск требуется формат для Azure, воспользуйтесь одним из способов hello в этом разделе. Создайте резервную копию hello виртуальной Машины перед запуском процесса преобразования виртуального диска hello и убедитесь в том, что hello виртуального жесткого диска Windows правильно работает на локальном сервере hello. Устраните все ошибки в самой ВМ hello, прежде чем повторите tooconvert или передать его tooAzure.

После преобразования диска hello, создание виртуальной Машины, которая использует hello преобразовать диск. Запустите и выполните вход toofinish ВМ toohello Подготовка hello виртуальной Машины для передачи.

### <a name="convert-disk-using-hyper-v-manager"></a>Преобразование диска с помощью диспетчера Hyper-V
1. Откройте диспетчер Hyper-V и выберите локального компьютера в левой hello. В меню над списком компьютера hello hello выберите **действия** > **изменить диск**.
2. На hello **поиск виртуального жесткого диска** экране, найдите и выберите виртуальный диск.
3. На hello **выбрать действие** экрана, а затем выберите **преобразовать** и **Далее**.
4. Если вам требуется tooconvert из формата VHDX, выберите **VHD** и нажмите кнопку **Далее**
5. Если вам требуется tooconvert с динамически расширяемые диска, выберите **фиксированный размер** и нажмите кнопку **Далее**
6. Найдите и выберите путь toosave hello виртуального жесткого диска в новый файл.
7. Нажмите кнопку **Готово**

>[!NOTE]
>команды Hello в этой статье, должны выполняться в сеансе PowerShell с повышенными привилегиями.

### <a name="convert-disk-by-using-powershell"></a>Преобразование диска с помощью PowerShell
Виртуальный диск можно преобразовать с помощью hello [Convert-VHD](http://technet.microsoft.com/library/hh848454.aspx) команды в Windows PowerShell. При запуске PowerShell выберите **Запуск от имени администратора**. 

Hello следующая команда преобразует VHDX tooVHD и динамически расширяемые toofixed размер диска:

```Powershell
Convert-VHD –Path c:\test\MY-VM.vhdx –DestinationPath c:\test\MY-NEW-VM.vhd -VHDType Fixed
```
В этой команде замените значение hello для «-путь» с hello путь toohello виртуальный жесткий диск, необходимо tooconvert и hello значение для «-DestinationPath» hello новый путь и имя hello преобразовать диск.

### <a name="convert-from-vmware-vmdk-disk-format"></a>Преобразование диска VMware в формате VMDK
При наличии образ виртуальной Машины Windows в hello [формате VMDK](https://en.wikipedia.org/wiki/VMDK), преобразуйте его tooa виртуального жесткого диска с помощью hello [преобразователь виртуальной Машины Microsoft](https://www.microsoft.com/download/details.aspx?id=42497). Дополнительные сведения см. в статье hello блог [как tooConvert tooHyper-V VHD VMDK для VMware](http://blogs.msdn.com/b/timomta/archive/2015/06/11/how-to-convert-a-vmware-vmdk-to-hyper-v-vhd.aspx).

## <a name="set-windows-configurations-for-azure"></a>Настройка конфигурации Windows для Azure

Для виртуальной Машины, которая планируется hello tooAzure tooupload, выполнить все команды в hello ниже шагов из [окно командной строки с повышенными привилегиями](https://technet.microsoft.com/library/cc947813.aspx):

1. Удалите все статические постоянный маршрут в таблице маршрутизации hello:
   
   * таблицы маршрутов tooview hello, запустите `route print` hello командной строки.
   * Проверьте hello **маршруты сохраняемости** разделы. При наличии постоянный маршрут, воспользуйтесь [удаление маршрута](https://technet.microsoft.com/library/cc739598.apx) tooremove его.
2. Удалите прокси-сервера WinHTTP hello:
   
    ```PowerShell
    netsh winhttp reset proxy
    ```
3. Задать политику SAN диска hello слишком[Onlineall](https://technet.microsoft.com/library/gg252636.aspx). 
   
    ```PowerShell
    diskpart 
    ```
    Привет открыть окно командной строки введите следующие команды hello:

     ```DISKPART
    san policy=onlineall
    exit   
    ```

4. Задать время по Гринвичу (UTC) для Windows и hello тип запуска службы времени Windows (w32time) hello слишком**автоматически**:
   
    ```PowerShell
    Set-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\Control\TimeZoneInformation' -name "RealTimeIsUniversal" 1 -Type DWord

    Set-Service -Name w32time -StartupType Auto
    ```
5. Задайте профиль toohello hello power **высокая производительность**:

    ```PowerShell
    powercfg /setactive SCHEME_MIN
    ```

## <a name="check-hello-windows-services"></a>Проверка служб Windows hello
Убедитесь, что каждый из следующих служб Windows hello задано toohello **значения по умолчанию Windows**. Ниже приведены минимальные номера hello служб, которые должны настраиваться toomake том, что этой hello виртуальная машина подключена. tooreset hello параметры запуска, запустите hello, следующие команды:
   
```PowerShell
Set-Service -Name bfe -StartupType Auto
Set-Service -Name dhcp -StartupType Auto
Set-Service -Name dnscache -StartupType Auto
Set-Service -Name IKEEXT -StartupType Auto
Set-Service -Name iphlpsvc -StartupType Auto
Set-Service -Name netlogon -StartupType Manual
Set-Service -Name netman -StartupType Manual
Set-Service -Name nsi -StartupType Auto
Set-Service -Name termService -StartupType Manual
Set-Service -Name MpsSvc -StartupType Auto
Set-Service -Name RemoteRegistry -StartupType Auto
```

## <a name="update-remote-desktop-registry-settings"></a>Обновление параметров реестра для удаленного рабочего стола
Убедитесь, что hello следующие параметры настроены правильно для подключения удаленного рабочего стола:

>[!Note] 
>Может появиться сообщение об ошибке при запуске hello **Set-ItemProperty-Path "HKLM:\SOFTWARE\Policies\Microsoft\Windows NT\Terminal службы — имя &lt;имя объекта&gt; &lt;значение&gt;** в этом пошаговом руководстве. сообщение об ошибке Hello можно спокойно проигнорировать. Это означает, что домен hello не внедряет этой конфигурации с помощью объекта групповой политики.
>
>

1. Включите протокол удаленного рабочего стола (RDP):
   
    ```PowerShell
    Set-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\Control\Terminal Server' -name "fDenyTSConnections" -Value 0 -Type DWord

    Set-ItemProperty -Path 'HKLM:\SOFTWARE\Policies\Microsoft\Windows NT\Terminal Services' -name "fDenyTSConnections" -Value 0 -Type DWord
    ```
   
2. Hello RDP-порту настроены правильно (по умолчанию порт 3389):
   
    ```PowerShell
   Set-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\Control\Terminal Server\Winstations\RDP-Tcp' -name "PortNumber" 3389 -Type DWord
    ```
    При развертывании виртуальной Машины к порту 3389 создаются правила по умолчанию hello. Номер порта toochange hello следует сделайте после развертывания hello ВМ в Azure.

3. Hello прослушиватель в каждом сетевой интерфейс:
   
    ```PowerShell
    Set-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\Control\Terminal Server\Winstations\RDP-Tcp' -name "LanAdapter" 0 -Type DWord
   ```
4. Настройка режима проверки подлинности на уровне сети hello для подключений по протоколу RDP hello:
   
    ```PowerShell
   Set-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\Control\Terminal Server\WinStations\RDP-Tcp' -name "UserAuthentication" 1 -Type DWord

    Set-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\Control\Terminal Server\WinStations\RDP-Tcp' -name "SecurityLayer" 1 -Type DWord

    Set-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\Control\Terminal Server\WinStations\RDP-Tcp' -name "fAllowSecProtocolNegotiation" 1 -Type DWord
     ```

5. Установите значение keep-alive hello:
    
    ```PowerShell
    Set-ItemProperty -Path 'HKLM:\SOFTWARE\Policies\Microsoft\Windows NT\Terminal Services' -name "KeepAliveEnable" 1 -Type DWord
    Set-ItemProperty -Path 'HKLM:\SOFTWARE\Policies\Microsoft\Windows NT\Terminal Services' -name "KeepAliveInterval" 1 -Type DWord
    Set-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\Control\Terminal Server\Winstations\RDP-Tcp' -name "KeepAliveTimeout" 1 -Type DWord
    ```
6. Выполните повторное подключение:
    
    ```PowerShell
    Set-ItemProperty -Path 'HKLM:\SOFTWARE\Policies\Microsoft\Windows NT\Terminal Services' -name "fDisableAutoReconnect" 0 -Type DWord
    Set-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\Control\Terminal Server\Winstations\RDP-Tcp' -name "fInheritReconnectSame" 1 -Type DWord
    Set-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\Control\Terminal Server\Winstations\RDP-Tcp' -name "fReconnectSame" 0 -Type DWord
    ```
7. Максимальное число одновременных подключений в hello:
    
    ```PowerShell
    Set-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\Control\Terminal Server\Winstations\RDP-Tcp' -name "MaxInstanceCount" 4294967295 -Type DWord
    ```
8. При наличии любого самозаверяющие сертификаты привязаны toohello RDP-прослушиватель, удалить их:
    
    ```PowerShell
    Remove-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\Control\Terminal Server\WinStations\RDP-Tcp' -name "SSLCertificateSHA1Hash"
    ```
    Это toomake том, что можно подключиться в начале hello при развертывании виртуальной Машины hello. Можно также просмотреть это на следующем этапе после развертывания ВМ в Azure, при необходимости приветствия.

9. Если hello виртуальной Машины будет входить в состав домена, убедитесь, что все hello следующие параметры toomake убедиться, что hello прежние параметры, не будут возвращены. Hello политики, которые должны быть проверены, hello следующее:
    
    - Включите RDP:

         Computer Configuration\Policies\Windows Settings\Administrative Templates\ Components\Remote Desktop Services\Remote Desktop Session Host\Connections:
         
         **Разрешить пользователям tooconnect удаленно с помощью удаленного рабочего стола**

    - Групповая политика с проверкой подлинности на уровне сети:

        Settings\Administrative Templates\Components\Remote Desktop Services\Remote Desktop Session Host\Security: 
        
        **Требовать проверку подлинности пользователя для удаленных подключений путем проверки подлинности на уровне сети**
    
    - Параметры проверки активности:

        Computer Configuration\Policies\Windows Settings\Administrative Templates\Windows Components\Remote Desktop Services\Remote Desktop Session Host\Connections: 
        
        **Настроить интервал проверяемых на активность подключений**

    - Параметры повторного подключения:

        Computer Configuration\Policies\Windows Settings\Administrative Templates\Windows Components\Remote Desktop Services\Remote Desktop Session Host\Connections: 
        
        **Автоматическое переподключение**

    - Максимальное число подключений в hello:

        Computer Configuration\Policies\Windows Settings\Administrative Templates\Windows Components\Remote Desktop Services\Remote Desktop Session Host\Connections: 
        
        **Ограничить количество подключений**

## <a name="configure-windows-firewall-rules"></a>Настройка правил брандмауэра Windows
1. Включите брандмауэр Windows hello трех профилей (домен, Standard и Public):

   ```PowerShell
    Set-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\services\SharedAccess\Parameters\FirewallPolicy\DomainProfile' -name "EnableFirewall" -Value 1 -Type DWord
    Set-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\services\SharedAccess\Parameters\FirewallPolicy\PublicProfile' -name "EnableFirewall" -Value 1 -Type DWord
    Set-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\services\SharedAccess\Parameters\FirewallPolicy\Standardprofile' -name "EnableFirewall" -Value 1 -Type DWord
   ```

2. Запустите следующую команду в PowerShell tooallow WinRM через hello трех профилей брандмауэра (домен, частные и Общие) hello и включение hello служба PowerShell Remote.
   
   ```PowerShell
    Enable-PSRemoting -force
    netsh advfirewall firewall set rule dir=in name="Windows Remote Management (HTTP-In)" new enable=yes
    netsh advfirewall firewall set rule dir=in name="Windows Remote Management (HTTP-In)" new enable=yes
   ```
3. Включить hello следующий трафик RDP hello tooallow правила брандмауэра 

   ```PowerShell
    netsh advfirewall firewall set rule group="Remote Desktop" new enable=yes
   ```   
4. Включите hello файла и общий доступ к принтеру правила, чтобы hello виртуальной Машины может отвечать команду ping tooa внутри hello виртуальной сети:

   ```PowerShell
    netsh advfirewall firewall set rule dir=in name="File and Printer Sharing (Echo Request - ICMPv4-In)" new enable=yes
   ``` 
5. Если hello виртуальной Машины будет входить в состав домена, проверьте следующие параметры toomake убедиться, что не будут возвращены hello прежние параметры hello. Hello AD политики, которые необходимо проверить, hello следующее:

    - Включить профили брандмауэра Windows hello

        Computer Configuration\Policies\Windows Settings\Administrative Templates\Network\Network Connection\Windows Firewall\Domain Profile\Windows Firewall: **Защита всех сетевых подключений**

       Computer Configuration\Policies\Windows Settings\Administrative Templates\Network\Network Connection\Windows Firewall\Standard Profile\Windows Firewall: **Защита всех сетевых подключений**

    - Включите RDP: 

        Computer Configuration\Policies\Windows Settings\Administrative Templates\Network\Network Connection\Windows Firewall\Domain Profile\Windows Firewall: **Разрешить исключения для входящих сообщений удаленного управления рабочим столом**

        Computer Configuration\Policies\Windows Settings\Administrative Templates\Network\Network Connection\Windows Firewall\Standard Profile\Windows Firewall: **Разрешить исключения для входящих сообщений удаленного управления рабочим столом**

    - Включите ICMP-V4:

        Computer Configuration\Policies\Windows Settings\Administrative Templates\Network\Network Connection\Windows Firewall\Domain Profile\Windows Firewall: **Разрешить исключения ICMP**

        Computer Configuration\Policies\Windows Settings\Administrative Templates\Network\Network Connection\Windows Firewall\Standard Profile\Windows Firewall: **Разрешить исключения ICMP**

## <a name="verify-vm-is-healthy-secure-and-accessible-with-rdp"></a>Проверка виртуальной машины: работоспособность, защищенность и доступ по протоколу RDP 
1. toomake убедиться, что hello диск находится в работоспособном состоянии и согласованного, запустите операцию проверки диска hello при следующей перезагрузке виртуальной Машины:

    ```PowerShell
    Chkdsk /f
    ```
    Убедитесь, что отчет hello показывает исправна и очистки диска.

2. Чтобы задайте параметры данных конфигурации загрузки (BCD) hello. 

    > [!Note]
    > Обязательно выполните следующие команды в окне командной строки с повышенными привилегиями, а **НЕ** в PowerShell:
   
   ```CMD
   bcdedit /set {bootmgr} integrityservices enable
   
   bcdedit /set {default} device partition=C:
   
   bcdedit /set {default} integrityservices enable
   
   bcdedit /set {default} recoveryenabled Off
   
   bcdedit /set {default} osdevice partition=C:
   
   bcdedit /set {default} bootstatuspolicy IgnoreAllFailures
   ```
3. Проверьте согласованность репозитория правильно Windows hello. tooperform, выполнения hello следующую команду:

    ```PowerShell
    winmgmt /verifyrepository
    ```
    См. в случае повреждения репозитория hello [WMI: повреждение базы данных или не](https://blogs.technet.microsoft.com/askperf/2014/08/08/wmi-repository-corruption-or-not).

4. Убедитесь, что любое другое приложение не использует hello порт 3389. Этот порт используется для hello службы протокола удаленного рабочего СТОЛА в Azure. Можно запустить **netstat - anob** toosee, какие порты в используются на hello виртуальной Машины:

    ```PowerShell
    netstat -anob
    ```

5. Если hello виртуального жесткого диска Windows, которые должны tooupload является контроллером домена, выполните следующие действия:

    О. Выполните [этих дополнительных шагов](https://support.microsoft.com/kb/2904015) tooprepare hello диска.

    B. Убедитесь, что вы знаете пароль DSRM hello случаю, когда toostart hello виртуальной Машины в режиме DSRM в определенный момент. Вы можете toorefer toothis связать tooset hello [Пароль DSRM](https://technet.microsoft.com/library/cc754363(v=ws.11).aspx).

6. Убедитесь, что hello встроенной учетной записи администратора и пароль являются известными tooyou. Можно tooreset hello текущий пароль локального администратора и убедитесь в том, что toosign этой учетной записи можно использовать в tooWindows через hello RDP-подключение. Это разрешение доступа управляется hello объекта групповой политики «Локальный вход на через службу удаленных рабочих столов». Этот объект можно просмотреть в hello редактор локальной групповой политики в разделе:

    Computer Configuration\Windows Settings\Security Settings\Local Policies\User Rights Assignment

7. Убедитесь, что следующие AD hello политики toomake убедиться, что не блокируют RDP-доступ через протокола удаленного рабочего СТОЛА или из сети hello:

    - Компьютер Configuration\Windows Settings\Security безопасности\Локальные политики\Назначение прав Assignment\Deny доступа toothis компьютер от сети hello

    - Computer Configuration\Windows Settings\Security Settings\Local Policies\User Rights Assignment\Запретить вход в систему через службу удаленных рабочих столов.


8. Перезапуск hello ВМ toomake том, что Windows по-прежнему работоспособна можно получить с помощью hello RDP-подключение. На этом этапе можно toocreate виртуальной Машины в вашей локальной Hyper-V toomake убедиться, что приветствия полностью выполняется запуск виртуальной Машины и затем проверьте, является ли он доступным протокола удаленного рабочего СТОЛА.

9. Удалите все дополнительные фильтры TDI, например программное обеспечение, которое анализирует пакеты TCP, или дополнительные брандмауэры. Можно также просмотреть это на следующем этапе после развертывания ВМ в Azure, при необходимости приветствия.

10. Удалите другие стороннего программного обеспечения и драйвер, toophysical связанные компоненты или любой другой технологии виртуализации.

### <a name="install-windows-updates"></a>Установка обновлений Windows
Лучшая конфигурация Hello является слишком**имеют уровень исправления hello машины hello в последней hello**. Если это невозможно, убедитесь, что hello, после обновления установлены:

|                       |                   |           |                                       Минимальная версия файла для 64-разрядной системы       |                                      |                                      |                            |
|-------------------------|-------------------|------------------------------------|---------------------------------------------|--------------------------------------|--------------------------------------|----------------------------|
| Компонент               | Binary            | Windows 7 и Windows Server 2008 R2 | Windows 8 и Windows Server 2012             | Windows 8.1 и Windows Server 2012 R2 | Windows 10 и Windows Server 2016 RS1 | Windows 10 RS2             |
| Хранилище                 | disk.sys          | 6.1.7601.23403 — KB3125574         | 6.2.9200.17638 / 6.2.9200.21757 — KB3137061 | 6.3.9600.18203 — KB3137061           | -                                    | -                          |
|                         | storport.sys      | 6.1.7601.23403 — KB3125574         | 6.2.9200.17188 / 6.2.9200.21306 — KB3018489 | 6.3.9600.18573 — KB4022726           | 10.0.14393.1358 — KB4022715          | 10.0.15063.332             |
|                         | ntfs.sys          | 6.1.7601.23403 — KB3125574         | 6.2.9200.17623 / 6.2.9200.21743 — KB3121255 | 6.3.9600.18654 — KB4022726           | 10.0.14393.1198 — KB4022715          | 10.0.15063.447             |
|                         | Iologmsg.dll      | 6.1.7601.23403 — KB3125574         | 6.2.9200.16384 — KB2995387                  | -                                    | -                                    | -                          |
|                         | Classpnp.sys      | 6.1.7601.23403 — KB3125574         | 6.2.9200.17061 / 6.2.9200.21180 — KB2995387 | 6.3.9600.18334 — KB3172614           | 10.0.14393.953 — KB4022715           | -                          |
|                         | Volsnap.sys       | 6.1.7601.23403 — KB3125574         | 6.2.9200.17047 / 6.2.9200.21165 — KB2975331 | 6.3.9600.18265 — KB3145384           | -                                    | 10.0.15063.0               |
|                         | partmgr.sys       | 6.1.7601.23403 — KB3125574         | 6.2.9200.16681 — KB2877114                  | 6.3.9600.17401 — KB3000850           | 10.0.14393.953 — KB4022715           | 10.0.15063.0               |
|                         | volmgr.sys        |                                    |                                             |                                      |                                      | 10.0.15063.0               |
|                         | Volmgrx.sys       | 6.1.7601.23403 — KB3125574         | -                                           | -                                    | -                                    | 10.0.15063.0               |
|                         | Msiscsi.sys       | 6.1.7601.23403 — KB3125574         | 6.2.9200.21006 — KB2955163                  | 6.3.9600.18624 — KB4022726           | 10.0.14393.1066 — KB4022715          | 10.0.15063.447             |
|                         | Msdsm.sys         | 6.1.7601.23403 — KB3125574         | 6.2.9200.21474 — KB3046101                  | 6.3.9600.18592 — KB4022726           | -                                    | -                          |
|                         | Mpio.sys          | 6.1.7601.23403 — KB3125574         | 6.2.9200.21190 — KB3046101                  | 6.3.9600.18616 — KB4022726           | 10.0.14393.1198 — KB4022715          | -                          |
|                         | Fveapi.dll        | 6.1.7601.23311 — KB3125574         | 6.2.9200.20930 — KB2930244                  | 6.3.9600.18294 — KB3172614           | 10.0.14393.576 — KB4022715           | -                          |
|                         | Fveapibase.dll    | 6.1.7601.23403 — KB3125574         | 6.2.9200.20930 — KB2930244                  | 6.3.9600.17415 — KB3172614           | 10.0.14393.206 — KB4022715           | -                          |
| Сеть                 | netvsc.sys        | -                                  | -                                           | -                                    | 10.0.14393.1198 — KB4022715          | 10.0.15063.250 — KB4020001 |
|                         | mrxsmb10.sys      | 6.1.7601.23816 — KB4022722         | 6.2.9200.22108 — KB4022724                  | 6.3.9600.18603 — KB4022726           | 10.0.14393.479 — KB4022715           | 10.0.15063.483             |
|                         | mrxsmb20.sys      | 6.1.7601.23816 — KB4022722         | 6.2.9200.21548 — KB4022724                  | 6.3.9600.18586 — KB4022726           | 10.0.14393.953 — KB4022715           | 10.0.15063.483             |
|                         | mrxsmb.sys        | 6.1.7601.23816 — KB4022722         | 6.2.9200.22074 — KB4022724                  | 6.3.9600.18586 — KB4022726           | 10.0.14393.953 — KB4022715           | 10.0.15063.0               |
|                         | tcpip.sys         | 6.1.7601.23761 — KB4022722         | 6.2.9200.22070 — KB4022724                  | 6.3.9600.18478 — KB4022726           | 10.0.14393.1358 — KB4022715          | 10.0.15063.447             |
|                         | http.sys          | 6.1.7601.23403 — KB3125574         | 6.2.9200.17285 — KB3042553                  | 6.3.9600.18574 — KB4022726           | 10.0.14393.251 — KB4022715           | 10.0.15063.483             |
|                         | vmswitch.sys      | 6.1.7601.23727 — KB4022719         | 6.2.9200.22117 — KB4022724                  | 6.3.9600.18654 — KB4022726           | 10.0.14393.1358 — KB4022715          | 10.0.15063.138             |
| Core                    | ntoskrnl.exe      | 6.1.7601.23807 — KB4022719         | 6.2.9200.22170 — KB4022718                  | 6.3.9600.18696 — KB4022726           | 10.0.14393.1358 — KB4022715          | 10.0.15063.483             |
| Службы удаленных рабочих столов | rdpcorets.dll     | 6.2.9200.21506 — KB4022719         | 6.2.9200.22104 — KB4022724                  | 6.3.9600.18619 — KB4022726           | 10.0.14393.1198 — KB4022715          | 10.0.15063.0               |
|                         | termsrv.dll       | 6.1.7601.23403 — KB3125574         | 6.2.9200.17048 — KB2973501                  | 6.3.9600.17415 — KB3000850           | 10.0.14393.0 — KB4022715             | 10.0.15063.0               |
|                         | termdd.sys        | 6.1.7601.23403 — KB3125574         | -                                           | -                                    | -                                    | -                          |
|                         | win32k.sys        | 6.1.7601.23807 — KB4022719         | 6.2.9200.22168 — KB4022718                  | 6.3.9600.18698 — KB4022726           | 10.0.14393.594 — KB4022715           | -                          |
|                         | rdpdd.dll         | 6.1.7601.23403 — KB3125574         | -                                           | -                                    | -                                    | -                          |
|                         | rdpwd.sys         | 6.1.7601.23403 — KB3125574         | -                                           | -                                    | -                                    | -                          |
| Безопасность                | Из-за tooWannaCrypt | KB4012212                          | KB4012213                                   | KB4012213                            | KB4012606                            | KB4012606                  |
|                         |                   |                                    | KB4012216                                   |                                      | KB4013198                            | KB4013198                  |
|                         |                   | KB4012215                          | KB4012214                                   | KB4012216                            | KB4013429                            | KB4013429                  |
|                         |                   |                                    | KB4012217                                   |                                      | KB4013429                            | KB4013429                  |
       
### Когда toouse sysprep<a id="step23"></a>    

Sysprep — это процесс, могут возникнуть в версии windows, приведет к сбросу hello установки системы hello и предоставит «out of hello box experience», удаляя все личные данные и сброс несколько компонентов. Обычно это делается, если вы хотите toocreate шаблон, из которого можно развернуть несколько виртуальных машин, имеющих определенную конфигурацию. Этот шаблон называется **универсальным образом**.

Если вместо этого необходимо только toocreate одной виртуальной Машины с одного диска нет toouse sysprep. В этом случае можно просто создать hello виртуальной Машины в том, что известно как **специализированный образ**.

Дополнительные сведения о том, как toocreate ВМ из специализированного диска отображается:

- [Создание виртуальной машины Windows из специализированного диска](create-vm-specialized.md)
- [Create a VM from a specialized VHD disk](https://azure.microsoft.com/resources/templates/201-vm-specialized-vhd/) (Создание виртуальной машины из специализированного VHD-диска)

Если вы хотите toocreate обобщенный образ, необходимо toorun sysprep. Дополнительные сведения о программе Sysprep см. в разделе [как tooUse Sysprep: введение](http://technet.microsoft.com/library/bb457073.aspx). 

Не все роли или приложения, установленные на компьютере с Windows, поддерживают этот образ. Поэтому перед выполнять эту процедуру, см. Убедитесь, что следующие статьи toomake toohello этой роли "hello" этого компьютера поддерживается sysprep. [Sysprep Support for Server Roles](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles) (Поддержка серверных ролей в Sysprep).

### <a name="steps-toogeneralize-a-vhd"></a>Действия toogeneralize виртуального жесткого диска

>[!NOTE]
> После запуска sysprep.exe, как указано в hello, выполнив действия, выключите hello виртуальной Машины и не включить его снова до создания образа из него в Azure.

1. Войдите в toohello виртуальной Машины Windows.
2. Запустите **командную строку** от имени администратора. 
3. Перейдите в каталог hello для: **%windir%\system32\sysprep**, а затем запустите **sysprep.exe**.
3. В hello **средство подготовки системы** выберите **Enter System Out-of-Box Experience (OOBE)**и убедитесь, что hello **Generalize** установлен флажок.

    ![Средство SysPrep](media/prepare-for-upload-vhd-image/syspre.png)
4. В разделе **Параметры завершения работы** выберите **Завершение работы**.
5. Нажмите кнопку **ОК**.
6. По завершении работы программы Sysprep завершите работу виртуальной Машины hello. Не используйте **перезапустите** tooshut вниз hello виртуальной Машины.
7. Теперь hello виртуального жесткого диска — Готово toobe отправлен. Дополнительные сведения о том, как toocreate ВМ с общего диска, на экране [Отправка обобщенный виртуальный жесткий ДИСК и использовать toocreate новые виртуальные машины в Azure](sa-upload-generalized.md).


## <a name="complete-recommended-configurations"></a>Рекомендуемые настройки
Привет, следующие параметры не влияют на Отправка виртуального жесткого диска. Тем не менее, мы настоятельно рекомендуем их настроить.

* Установка hello [агента ВМ Azure](http://go.microsoft.com/fwlink/?LinkID=394789&clcid=0x409). Затем можно включить расширения виртуальной машины. Hello расширения ВМ реализуют значительную часть важных функций hello, возможно требуется toouse в ВМ, таких как сброс паролей, Настройка RDP и так далее. Дополнительные сведения можно найти в разделе 

    - [VM Agent and Extensions – Part 1](https://azure.microsoft.com/blog/vm-agent-and-extensions-part-1/) (Расширения и агент виртуальной машины. Часть 1)
    - [VM Agent and Extensions – Part 2](https://azure.microsoft.com/blog/vm-agent-and-extensions-part-2/) (Расширения и агент виртуальной машины. Часть 2)
* Hello дампа журнала может оказаться полезным при устранении неполадок Windows аварийного завершения. Включите сбор журналов hello дампа:
  
    ```PowerShell
    Set-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\Control\CrashControl' -name "CrashDumpEnable" -Value "2" -Type DWord
    Set-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\Control\CrashControl' -name "DumpFile" -Value "%SystemRoot%\MEMORY.DMP"
    Set-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\Control\CrashControl' -name "AutoReboot" -Value 0 -Type DWord
    New-Item -Path 'HKLM:\SOFTWARE\Microsoft\Windows\Windows Error Reporting\LocalDumps'
    New-ItemProperty -Path 'HKLM:\SOFTWARE\Microsoft\Windows\Windows Error Reporting\LocalDumps' -name "DumpFolder" -Value "c:\CrashDumps"
    New-ItemProperty -Path 'HKLM:\SOFTWARE\Microsoft\Windows\Windows Error Reporting\LocalDumps' -name "DumpCount" -Value 10 -Type DWord
    New-ItemProperty -Path 'HKLM:\SOFTWARE\Microsoft\Windows\Windows Error Reporting\LocalDumps' -name "DumpType" -Value 2 -Type DWord
    Set-Service -Name WerSvc -StartupType Manual
    ```
    При получении ошибки во время выполнения любой hello практические шаги в этой статье, это означает, что разделы реестра hello уже существует. В этом случае используйте hello вместо следующие команды:

    ```PowerShell
    Set-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\Control\CrashControl' -name "CrashDumpEnable" -Value "2" -Type DWord
    Set-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\Control\CrashControl' -name "DumpFile" -Value "%SystemRoot%\MEMORY.DMP"
    Set-ItemProperty -Path 'HKLM:\SOFTWARE\Microsoft\Windows\Windows Error Reporting\LocalDumps' -name "DumpFolder" -Value "c:\CrashDumps"
    Set-ItemProperty -Path 'HKLM:\SOFTWARE\Microsoft\Windows\Windows Error Reporting\LocalDumps' -name "DumpCount" -Value 10 -Type DWord
    Set-ItemProperty -Path 'HKLM:\SOFTWARE\Microsoft\Windows\Windows Error Reporting\LocalDumps' -name "DumpType" -Value 2 -Type DWord
    Set-Service -Name WerSvc -StartupType Manual
    ```
*  После создания hello ВМ в Azure рекомендуется поместить файл подкачки hello производительность tooimprove тома hello «Temporal водить». Вы можете это сделать, как показано ниже:

    ```PowerShell
    Set-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\Control\Session Manager\Memory Management' -name "PagingFiles" -Value "D:\pagefile"
    ```
Если любой диск, который является toohello подключенных виртуальных Машин, букву диска тома временных дисков hello обычно является «Г.» Это назначение может отличаться, в зависимости от числа доступных дисков и hello настройки, выполненные hello.

## <a name="next-steps"></a>Дальнейшие действия
* [Отправка tooAzure образ виртуальной Машины Windows для развертывания диспетчера ресурсов](upload-generalized-managed.md)

