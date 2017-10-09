## <a name="prepare-your-raspberry-pi"></a>Подготовка устройства Raspberry Pi

### <a name="install-raspbian"></a>Установка Raspbian

Если это первый раз используете вашей Raspberry Pi hello необходимо tooinstall hello Raspbian операционной системы с помощью NOOBS на SD-карте hello, входящих в пакет средств hello. Hello [руководство по Pi Raspberry] [ lnk-install-raspbian] описывает как tooinstall операционной системы на ваш Raspberry Pi. Учебнике предполагается, что вы установили hello Raspbian операционной системы на ваш Raspberry Pi.

> [!NOTE]
> Hello SD-карту, входящую в hello [Microsoft Azure IoT начальный набор для Raspberry Pi 3] [ lnk-starter-kits] уже установлен NOOBS. Можно загрузки hello Raspberry Pi с этой карты и выберите hello tooinstall Raspbian ОС.

Настройка оборудования toocomplete hello, необходимо:

- Подключите Raspberry Pi toohello питания входят в пакет hello.
- Подключение сети tooyour Raspberry пи с помощью кабеля Ethernet hello, входят в ваш пакет. Кроме того, для Raspberry Pi можно настроить [беспроводное подключение][lnk-pi-wireless].

Теперь завершении настройки оборудования hello вашей Raspberry пи.

### <a name="sign-in-and-access-hello-terminal"></a>Вход и доступ к терминалов hello

У вас есть два tooaccess параметры терминалов среды с вашей пи Raspberry:

- Если клавиатура и отслеживать подключенных tooyour Raspberry Pi, можно использовать tooaccess Raspbian GUI hello окно терминала.

- Командная строка hello доступа на ваш Raspberry Pi, с помощью SSH из настольном компьютере.

#### <a name="use-a-terminal-window-in-hello-gui"></a>Использование окна терминала в hello графического пользовательского интерфейса

имя пользователя, учетные данные по умолчанию Hello для Raspbian **pi** и пароль **raspberry**. На панели задач hello в hello графического пользовательского интерфейса, можно запустить hello **терминалов** hello значок, который выглядит как монитор с помощью служебной программы.

#### <a name="sign-in-with-ssh"></a>Вход с помощью SSH

Можно использовать SSH для командной строки доступ tooyour Raspberry Pi. статья Hello [SSH (Secure Shell)] [ lnk-pi-ssh] описывает как tooconfigure SSH с вашей пи Raspberry и как tooconnect из [Windows] [ lnk-ssh-windows] или [Linux и Mac OS][lnk-ssh-linux].

Войдите, используя имя пользователя **pi** и пароль **raspberry**.

#### <a name="optional-share-a-folder-on-your-raspberry-pi"></a>Совместный доступ к папке на устройстве Raspberry Pi (необязательно)

При необходимости вы можете tooshare папку с вашей Raspberry пи с рабочего стола. Общий доступ к папке позволяет вам toouse предпочтительный рабочего стола текстовый редактор (например, [кода Visual Studio](https://code.visualstudio.com/) или [Sublime текст](http://www.sublimetext.com/)) tooedit файлов на ваш Pi Raspberry вместо использования `nano` или `vi`.

tooshare папка с Windows, Настройка сервера Samba hello Raspberry Pi. Также можно использовать встроенные hello [SFTP](https://www.raspberrypi.org/documentation/remote-access/) сервера с SFTP-клиентом, на рабочем столе.

[lnk-install-raspbian]: https://www.raspberrypi.org/learning/software-guide/quickstart/
[lnk-pi-wireless]: https://www.raspberrypi.org/documentation/configuration/wireless/README.md
[lnk-pi-ssh]: https://www.raspberrypi.org/documentation/remote-access/ssh/README.md
[lnk-ssh-windows]: https://www.raspberrypi.org/documentation/remote-access/ssh/windows.md
[lnk-ssh-linux]: https://www.raspberrypi.org/documentation/remote-access/ssh/unix.md
[lnk-starter-kits]: https://azure.microsoft.com/develop/iot/starter-kits/