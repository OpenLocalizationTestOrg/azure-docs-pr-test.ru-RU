## <a name="prepare-your-raspberry-pi"></a>Подготовка устройства Raspberry Pi

### <a name="install-raspbian"></a>Установка Raspbian

Если это первый раз используете вашей Raspberry Pi hello необходимо tooinstall hello Raspbian операционной системы с помощью NOOBS на SD-карте hello, входящих в пакет средств hello. Hello [руководство по Pi Raspberry] [ lnk-install-raspbian] описывает как tooinstall операционной системы на ваш Raspberry Pi. Учебнике предполагается, что вы установили hello Raspbian операционной системы на ваш Raspberry Pi.

> [!NOTE]
> Hello SD-карту, входящую в hello [Microsoft Azure IoT начальный набор для Raspberry Pi 3] [ lnk-starter-kits] уже установлен NOOBS. Можно загрузки hello Raspberry Pi с этой карты и выберите hello tooinstall Raspbian ОС.

### <a name="set-up-hello-hardware"></a>Настройка оборудования hello

В этом учебнике используется hello BME280 датчика, включенных в hello [Microsoft Azure IoT начальный набор для Raspberry Pi 3] [ lnk-starter-kits] toogenerate данные телеметрии. Она использует Индикатор tooindicate hello Raspberry Pi во время обработки вызова метода с панели мониторинга hello решения.

Существуют компоненты Hello на доске хлеб hello.

- красный светодиодный индикатор;
- резистор 220 Ом (красный, красный, коричневый);
- датчик BME280;

Hello следующей схеме показано tooconnect оборудования:

![Подключение оборудования для Raspberry Pi][img-connection-diagram]

Hello следующей таблице перечислены hello подключения из компонентов toohello Raspberry Pi hello hello breadboard:

| Raspberry Pi            | Монтажная плата             |Цвет         |
| ----------------------- | ---------------------- | ------------- |
| GND (вывод 14)            | Индикатор, -ve (18A)      | Сиреневый          |
| GPCLK0 (вывод 7)          | Резистор (25A)         | Оранжевый          |
| SPI_CE0 (вывод 24)        | CS (39A)               | Синий          |
| SPI_SCLK (вывод 23)       | SCK (36A)              | Желтый        |
| SPI_MISO (вывод 21)       | SDO (37A)              | Белый         |
| SPI MOSI (вывод 19)       | SDI (38A)              | Зеленый         |
| GND (вывод 6)             | GND (35A)              | Черный         |
| 3,3 В (вывод 1)           | 3 В (34A)              | Красный           |

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

### <a name="enable-spi"></a>Включение SPI

Перед запуском образца приложения hello, необходимо включить hello периферийных последовательного интерфейса (SPI) шины на hello Raspberry Pi. Hello Raspberry Pi взаимодействует с hello BME280 сенсорных устройств через hello SPI шины. Используйте следующие команды tooedit hello конфигурации файл hello:

```sh
sudo nano /boot/config.txt
```

Найдите строку hello:

`#dtparam=spi=on`

- Строка hello toouncomment, delete hello `#` в начале hello.
- Сохранить изменения (**Ctrl-O**, **ввод**) и редактор hello выхода (**Ctrl-X**).
- tooenable SPI, перезагрузите hello Raspberry Pi. Перезагрузка отключает терминалов hello, вы должны toosign в снова после hello Raspberry Pi перезагрузки:

  ```sh
  sudo reboot
  ```


[img-connection-diagram]: media/iot-suite-raspberry-pi-kit-prepare-pi/rpi2_remote_monitoring.png

[lnk-install-raspbian]: https://www.raspberrypi.org/learning/software-guide/quickstart/
[lnk-pi-wireless]: https://www.raspberrypi.org/documentation/configuration/wireless/README.md
[lnk-pi-ssh]: https://www.raspberrypi.org/documentation/remote-access/ssh/README.md
[lnk-ssh-windows]: https://www.raspberrypi.org/documentation/remote-access/ssh/windows.md
[lnk-ssh-linux]: https://www.raspberrypi.org/documentation/remote-access/ssh/unix.md
[lnk-starter-kits]: https://azure.microsoft.com/develop/iot/starter-kits/