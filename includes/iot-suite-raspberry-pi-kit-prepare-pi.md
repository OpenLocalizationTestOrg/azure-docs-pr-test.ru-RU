## <a name="prepare-your-raspberry-pi"></a><span data-ttu-id="e4668-101">Подготовка устройства Raspberry Pi</span><span class="sxs-lookup"><span data-stu-id="e4668-101">Prepare your Raspberry Pi</span></span>

### <a name="install-raspbian"></a><span data-ttu-id="e4668-102">Установка Raspbian</span><span class="sxs-lookup"><span data-stu-id="e4668-102">Install Raspbian</span></span>

<span data-ttu-id="e4668-103">Если это первый раз используете вашей Raspberry Pi hello необходимо tooinstall hello Raspbian операционной системы с помощью NOOBS на SD-карте hello, входящих в пакет средств hello.</span><span class="sxs-lookup"><span data-stu-id="e4668-103">If this is hello first time you are using your Raspberry Pi, you need tooinstall hello Raspbian operating system using NOOBS on hello SD card included in hello kit.</span></span> <span data-ttu-id="e4668-104">Hello [руководство по Pi Raspberry] [ lnk-install-raspbian] описывает как tooinstall операционной системы на ваш Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="e4668-104">hello [Raspberry Pi Software Guide][lnk-install-raspbian] describes how tooinstall an operating system on your Raspberry Pi.</span></span> <span data-ttu-id="e4668-105">Учебнике предполагается, что вы установили hello Raspbian операционной системы на ваш Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="e4668-105">This tutorial assumes you have installed hello Raspbian operating system on your Raspberry Pi.</span></span>

> [!NOTE]
> <span data-ttu-id="e4668-106">Hello SD-карту, входящую в hello [Microsoft Azure IoT начальный набор для Raspberry Pi 3] [ lnk-starter-kits] уже установлен NOOBS.</span><span class="sxs-lookup"><span data-stu-id="e4668-106">hello SD card included in hello [Microsoft Azure IoT Starter Kit for Raspberry Pi 3][lnk-starter-kits] already has NOOBS installed.</span></span> <span data-ttu-id="e4668-107">Можно загрузки hello Raspberry Pi с этой карты и выберите hello tooinstall Raspbian ОС.</span><span class="sxs-lookup"><span data-stu-id="e4668-107">You can boot hello Raspberry Pi from this card and choose tooinstall hello Raspbian OS.</span></span>

### <a name="set-up-hello-hardware"></a><span data-ttu-id="e4668-108">Настройка оборудования hello</span><span class="sxs-lookup"><span data-stu-id="e4668-108">Set up hello hardware</span></span>

<span data-ttu-id="e4668-109">В этом учебнике используется hello BME280 датчика, включенных в hello [Microsoft Azure IoT начальный набор для Raspberry Pi 3] [ lnk-starter-kits] toogenerate данные телеметрии.</span><span class="sxs-lookup"><span data-stu-id="e4668-109">This tutorial uses hello BME280 sensor included in hello [Microsoft Azure IoT Starter Kit for Raspberry Pi 3][lnk-starter-kits] toogenerate telemetry data.</span></span> <span data-ttu-id="e4668-110">Она использует Индикатор tooindicate hello Raspberry Pi во время обработки вызова метода с панели мониторинга hello решения.</span><span class="sxs-lookup"><span data-stu-id="e4668-110">It uses an LED tooindicate when hello Raspberry Pi processes a method invocation from hello solution dashboard.</span></span>

<span data-ttu-id="e4668-111">Существуют компоненты Hello на доске хлеб hello.</span><span class="sxs-lookup"><span data-stu-id="e4668-111">hello components on hello bread board are:</span></span>

- <span data-ttu-id="e4668-112">красный светодиодный индикатор;</span><span class="sxs-lookup"><span data-stu-id="e4668-112">Red LED</span></span>
- <span data-ttu-id="e4668-113">резистор 220 Ом (красный, красный, коричневый);</span><span class="sxs-lookup"><span data-stu-id="e4668-113">220-Ohm resistor (red, red, brown)</span></span>
- <span data-ttu-id="e4668-114">датчик BME280;</span><span class="sxs-lookup"><span data-stu-id="e4668-114">BME280 sensor</span></span>

<span data-ttu-id="e4668-115">Hello следующей схеме показано tooconnect оборудования:</span><span class="sxs-lookup"><span data-stu-id="e4668-115">hello following diagram shows how tooconnect your hardware:</span></span>

![Подключение оборудования для Raspberry Pi][img-connection-diagram]

<span data-ttu-id="e4668-117">Hello следующей таблице перечислены hello подключения из компонентов toohello Raspberry Pi hello hello breadboard:</span><span class="sxs-lookup"><span data-stu-id="e4668-117">hello following table summarizes hello connections from hello Raspberry Pi toohello components on hello breadboard:</span></span>

| <span data-ttu-id="e4668-118">Raspberry Pi</span><span class="sxs-lookup"><span data-stu-id="e4668-118">Raspberry Pi</span></span>            | <span data-ttu-id="e4668-119">Монтажная плата</span><span class="sxs-lookup"><span data-stu-id="e4668-119">Breadboard</span></span>             |<span data-ttu-id="e4668-120">Цвет</span><span class="sxs-lookup"><span data-stu-id="e4668-120">Color</span></span>         |
| ----------------------- | ---------------------- | ------------- |
| <span data-ttu-id="e4668-121">GND (вывод 14)</span><span class="sxs-lookup"><span data-stu-id="e4668-121">GND (Pin 14)</span></span>            | <span data-ttu-id="e4668-122">Индикатор, -ve (18A)</span><span class="sxs-lookup"><span data-stu-id="e4668-122">LED -ve pin (18A)</span></span>      | <span data-ttu-id="e4668-123">Сиреневый</span><span class="sxs-lookup"><span data-stu-id="e4668-123">Purple</span></span>          |
| <span data-ttu-id="e4668-124">GPCLK0 (вывод 7)</span><span class="sxs-lookup"><span data-stu-id="e4668-124">GPCLK0 (Pin 7)</span></span>          | <span data-ttu-id="e4668-125">Резистор (25A)</span><span class="sxs-lookup"><span data-stu-id="e4668-125">Resistor (25A)</span></span>         | <span data-ttu-id="e4668-126">Оранжевый</span><span class="sxs-lookup"><span data-stu-id="e4668-126">Orange</span></span>          |
| <span data-ttu-id="e4668-127">SPI_CE0 (вывод 24)</span><span class="sxs-lookup"><span data-stu-id="e4668-127">SPI_CE0 (Pin 24)</span></span>        | <span data-ttu-id="e4668-128">CS (39A)</span><span class="sxs-lookup"><span data-stu-id="e4668-128">CS (39A)</span></span>               | <span data-ttu-id="e4668-129">Синий</span><span class="sxs-lookup"><span data-stu-id="e4668-129">Blue</span></span>          |
| <span data-ttu-id="e4668-130">SPI_SCLK (вывод 23)</span><span class="sxs-lookup"><span data-stu-id="e4668-130">SPI_SCLK (Pin 23)</span></span>       | <span data-ttu-id="e4668-131">SCK (36A)</span><span class="sxs-lookup"><span data-stu-id="e4668-131">SCK (36A)</span></span>              | <span data-ttu-id="e4668-132">Желтый</span><span class="sxs-lookup"><span data-stu-id="e4668-132">Yellow</span></span>        |
| <span data-ttu-id="e4668-133">SPI_MISO (вывод 21)</span><span class="sxs-lookup"><span data-stu-id="e4668-133">SPI_MISO (Pin 21)</span></span>       | <span data-ttu-id="e4668-134">SDO (37A)</span><span class="sxs-lookup"><span data-stu-id="e4668-134">SDO (37A)</span></span>              | <span data-ttu-id="e4668-135">Белый</span><span class="sxs-lookup"><span data-stu-id="e4668-135">White</span></span>         |
| <span data-ttu-id="e4668-136">SPI MOSI (вывод 19)</span><span class="sxs-lookup"><span data-stu-id="e4668-136">SPI_MOSI (Pin 19)</span></span>       | <span data-ttu-id="e4668-137">SDI (38A)</span><span class="sxs-lookup"><span data-stu-id="e4668-137">SDI (38A)</span></span>              | <span data-ttu-id="e4668-138">Зеленый</span><span class="sxs-lookup"><span data-stu-id="e4668-138">Green</span></span>         |
| <span data-ttu-id="e4668-139">GND (вывод 6)</span><span class="sxs-lookup"><span data-stu-id="e4668-139">GND (Pin 6)</span></span>             | <span data-ttu-id="e4668-140">GND (35A)</span><span class="sxs-lookup"><span data-stu-id="e4668-140">GND (35A)</span></span>              | <span data-ttu-id="e4668-141">Черный</span><span class="sxs-lookup"><span data-stu-id="e4668-141">Black</span></span>         |
| <span data-ttu-id="e4668-142">3,3 В (вывод 1)</span><span class="sxs-lookup"><span data-stu-id="e4668-142">3.3 V (Pin 1)</span></span>           | <span data-ttu-id="e4668-143">3 В (34A)</span><span class="sxs-lookup"><span data-stu-id="e4668-143">3Vo (34A)</span></span>              | <span data-ttu-id="e4668-144">Красный</span><span class="sxs-lookup"><span data-stu-id="e4668-144">Red</span></span>           |

<span data-ttu-id="e4668-145">Настройка оборудования toocomplete hello, необходимо:</span><span class="sxs-lookup"><span data-stu-id="e4668-145">toocomplete hello hardware setup, you need to:</span></span>

- <span data-ttu-id="e4668-146">Подключите Raspberry Pi toohello питания входят в пакет hello.</span><span class="sxs-lookup"><span data-stu-id="e4668-146">Connect your Raspberry Pi toohello power supply included in hello kit.</span></span>
- <span data-ttu-id="e4668-147">Подключение сети tooyour Raspberry пи с помощью кабеля Ethernet hello, входят в ваш пакет.</span><span class="sxs-lookup"><span data-stu-id="e4668-147">Connect your Raspberry Pi tooyour network using hello Ethernet cable included in your kit.</span></span> <span data-ttu-id="e4668-148">Кроме того, для Raspberry Pi можно настроить [беспроводное подключение][lnk-pi-wireless].</span><span class="sxs-lookup"><span data-stu-id="e4668-148">Alternatively, you can set up [Wireless Connectivity][lnk-pi-wireless] for your Raspberry Pi.</span></span>

<span data-ttu-id="e4668-149">Теперь завершении настройки оборудования hello вашей Raspberry пи.</span><span class="sxs-lookup"><span data-stu-id="e4668-149">You have now completed hello hardware setup of your Raspberry Pi.</span></span>

### <a name="sign-in-and-access-hello-terminal"></a><span data-ttu-id="e4668-150">Вход и доступ к терминалов hello</span><span class="sxs-lookup"><span data-stu-id="e4668-150">Sign in and access hello terminal</span></span>

<span data-ttu-id="e4668-151">У вас есть два tooaccess параметры терминалов среды с вашей пи Raspberry:</span><span class="sxs-lookup"><span data-stu-id="e4668-151">You have two options tooaccess a terminal environment on your Raspberry Pi:</span></span>

- <span data-ttu-id="e4668-152">Если клавиатура и отслеживать подключенных tooyour Raspberry Pi, можно использовать tooaccess Raspbian GUI hello окно терминала.</span><span class="sxs-lookup"><span data-stu-id="e4668-152">If you have a keyboard and monitor connected tooyour Raspberry Pi, you can use hello Raspbian GUI tooaccess a terminal window.</span></span>

- <span data-ttu-id="e4668-153">Командная строка hello доступа на ваш Raspberry Pi, с помощью SSH из настольном компьютере.</span><span class="sxs-lookup"><span data-stu-id="e4668-153">Access hello command line on your Raspberry Pi using SSH from your desktop machine.</span></span>

#### <a name="use-a-terminal-window-in-hello-gui"></a><span data-ttu-id="e4668-154">Использование окна терминала в hello графического пользовательского интерфейса</span><span class="sxs-lookup"><span data-stu-id="e4668-154">Use a terminal Window in hello GUI</span></span>

<span data-ttu-id="e4668-155">имя пользователя, учетные данные по умолчанию Hello для Raspbian **pi** и пароль **raspberry**.</span><span class="sxs-lookup"><span data-stu-id="e4668-155">hello default credentials for Raspbian are username **pi** and password **raspberry**.</span></span> <span data-ttu-id="e4668-156">На панели задач hello в hello графического пользовательского интерфейса, можно запустить hello **терминалов** hello значок, который выглядит как монитор с помощью служебной программы.</span><span class="sxs-lookup"><span data-stu-id="e4668-156">In hello task bar in hello GUI, you can launch hello **Terminal** utility using hello icon that looks like a monitor.</span></span>

#### <a name="sign-in-with-ssh"></a><span data-ttu-id="e4668-157">Вход с помощью SSH</span><span class="sxs-lookup"><span data-stu-id="e4668-157">Sign in with SSH</span></span>

<span data-ttu-id="e4668-158">Можно использовать SSH для командной строки доступ tooyour Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="e4668-158">You can use SSH for command-line access tooyour Raspberry Pi.</span></span> <span data-ttu-id="e4668-159">статья Hello [SSH (Secure Shell)] [ lnk-pi-ssh] описывает как tooconfigure SSH с вашей пи Raspberry и как tooconnect из [Windows] [ lnk-ssh-windows] или [Linux и Mac OS][lnk-ssh-linux].</span><span class="sxs-lookup"><span data-stu-id="e4668-159">hello article [SSH (Secure Shell)][lnk-pi-ssh] describes how tooconfigure SSH on your Raspberry Pi, and how tooconnect from [Windows][lnk-ssh-windows] or [Linux & Mac OS][lnk-ssh-linux].</span></span>

<span data-ttu-id="e4668-160">Войдите, используя имя пользователя **pi** и пароль **raspberry**.</span><span class="sxs-lookup"><span data-stu-id="e4668-160">Sign in with username **pi** and password **raspberry**.</span></span>

#### <a name="optional-share-a-folder-on-your-raspberry-pi"></a><span data-ttu-id="e4668-161">Совместный доступ к папке на устройстве Raspberry Pi (необязательно)</span><span class="sxs-lookup"><span data-stu-id="e4668-161">Optional: Share a folder on your Raspberry Pi</span></span>

<span data-ttu-id="e4668-162">При необходимости вы можете tooshare папку с вашей Raspberry пи с рабочего стола.</span><span class="sxs-lookup"><span data-stu-id="e4668-162">Optionally, you may want tooshare a folder on your Raspberry Pi with your desktop environment.</span></span> <span data-ttu-id="e4668-163">Общий доступ к папке позволяет вам toouse предпочтительный рабочего стола текстовый редактор (например, [кода Visual Studio](https://code.visualstudio.com/) или [Sublime текст](http://www.sublimetext.com/)) tooedit файлов на ваш Pi Raspberry вместо использования `nano` или `vi`.</span><span class="sxs-lookup"><span data-stu-id="e4668-163">Sharing a folder enables you toouse your preferred desktop text editor (such as [Visual Studio Code](https://code.visualstudio.com/) or [Sublime Text](http://www.sublimetext.com/)) tooedit files on your Raspberry Pi instead of using `nano` or `vi`.</span></span>

<span data-ttu-id="e4668-164">tooshare папка с Windows, Настройка сервера Samba hello Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="e4668-164">tooshare a folder with Windows, configure a Samba server on hello Raspberry Pi.</span></span> <span data-ttu-id="e4668-165">Также можно использовать встроенные hello [SFTP](https://www.raspberrypi.org/documentation/remote-access/) сервера с SFTP-клиентом, на рабочем столе.</span><span class="sxs-lookup"><span data-stu-id="e4668-165">Alternatively, use hello built-in [SFTP](https://www.raspberrypi.org/documentation/remote-access/) server with an SFTP client on your desktop.</span></span>

### <a name="enable-spi"></a><span data-ttu-id="e4668-166">Включение SPI</span><span class="sxs-lookup"><span data-stu-id="e4668-166">Enable SPI</span></span>

<span data-ttu-id="e4668-167">Перед запуском образца приложения hello, необходимо включить hello периферийных последовательного интерфейса (SPI) шины на hello Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="e4668-167">Before you can run hello sample application, you must enable hello Serial Peripheral Interface (SPI) bus on hello Raspberry Pi.</span></span> <span data-ttu-id="e4668-168">Hello Raspberry Pi взаимодействует с hello BME280 сенсорных устройств через hello SPI шины.</span><span class="sxs-lookup"><span data-stu-id="e4668-168">hello Raspberry Pi communicates with hello BME280 sensor device over hello SPI bus.</span></span> <span data-ttu-id="e4668-169">Используйте следующие команды tooedit hello конфигурации файл hello:</span><span class="sxs-lookup"><span data-stu-id="e4668-169">Use hello following command tooedit hello configuration file:</span></span>

```sh
sudo nano /boot/config.txt
```

<span data-ttu-id="e4668-170">Найдите строку hello:</span><span class="sxs-lookup"><span data-stu-id="e4668-170">Find hello line:</span></span>

`#dtparam=spi=on`

- <span data-ttu-id="e4668-171">Строка hello toouncomment, delete hello `#` в начале hello.</span><span class="sxs-lookup"><span data-stu-id="e4668-171">toouncomment hello line, delete hello `#` at hello start.</span></span>
- <span data-ttu-id="e4668-172">Сохранить изменения (**Ctrl-O**, **ввод**) и редактор hello выхода (**Ctrl-X**).</span><span class="sxs-lookup"><span data-stu-id="e4668-172">Save your changes (**Ctrl-O**, **Enter**) and exit hello editor (**Ctrl-X**).</span></span>
- <span data-ttu-id="e4668-173">tooenable SPI, перезагрузите hello Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="e4668-173">tooenable SPI, reboot hello Raspberry Pi.</span></span> <span data-ttu-id="e4668-174">Перезагрузка отключает терминалов hello, вы должны toosign в снова после hello Raspberry Pi перезагрузки:</span><span class="sxs-lookup"><span data-stu-id="e4668-174">Rebooting disconnects hello terminal, you need toosign in again when hello Raspberry Pi restarts:</span></span>

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