## <a name="prepare-your-raspberry-pi"></a><span data-ttu-id="c403c-101">Подготовка устройства Raspberry Pi</span><span class="sxs-lookup"><span data-stu-id="c403c-101">Prepare your Raspberry Pi</span></span>

### <a name="install-raspbian"></a><span data-ttu-id="c403c-102">Установка Raspbian</span><span class="sxs-lookup"><span data-stu-id="c403c-102">Install Raspbian</span></span>

<span data-ttu-id="c403c-103">Если вы впервые используете устройство Raspberry Pi, необходимо установить операционную систему Raspbian с помощью NOOBS на карте SD, входящей в состав набора.</span><span class="sxs-lookup"><span data-stu-id="c403c-103">If this is the first time you are using your Raspberry Pi, you need to install the Raspbian operating system using NOOBS on the SD card included in the kit.</span></span> <span data-ttu-id="c403c-104">В [руководстве по программному обеспечению Raspberry Pi][lnk-install-raspbian] содержатся сведения об установке операционной системы на устройстве Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="c403c-104">The [Raspberry Pi Software Guide][lnk-install-raspbian] describes how to install an operating system on your Raspberry Pi.</span></span> <span data-ttu-id="c403c-105">В этом руководстве предполагается, что операционная система Raspbian уже установлена на Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="c403c-105">This tutorial assumes you have installed the Raspbian operating system on your Raspberry Pi.</span></span>

> [!NOTE]
> <span data-ttu-id="c403c-106">На картах SD, входящих в [начальный набор Microsoft Azure IoT для Raspberry Pi 3][lnk-starter-kits], уже установлены NOOBS.</span><span class="sxs-lookup"><span data-stu-id="c403c-106">The SD card included in the [Microsoft Azure IoT Starter Kit for Raspberry Pi 3][lnk-starter-kits] already has NOOBS installed.</span></span> <span data-ttu-id="c403c-107">Вы можете установить Raspberry Pi из этой карты, а также другую операционную систему Raspbian.</span><span class="sxs-lookup"><span data-stu-id="c403c-107">You can boot the Raspberry Pi from this card and choose to install the Raspbian OS.</span></span>

### <a name="set-up-the-hardware"></a><span data-ttu-id="c403c-108">Настройка оборудования</span><span class="sxs-lookup"><span data-stu-id="c403c-108">Set up the hardware</span></span>

<span data-ttu-id="c403c-109">Для создания данных телеметрии в этом руководстве используется датчик BME280, который входит в [начальный набор Microsoft Azure IoT для Raspberry Pi 3[lnk-starter-kits]].</span><span class="sxs-lookup"><span data-stu-id="c403c-109">This tutorial uses the BME280 sensor included in the [Microsoft Azure IoT Starter Kit for Raspberry Pi 3][lnk-starter-kits] to generate telemetry data.</span></span> <span data-ttu-id="c403c-110">Для извещения о том, что Raspberry Pi обрабатывает вызов метода из панели мониторинга решений, используется светодиодный индикатор.</span><span class="sxs-lookup"><span data-stu-id="c403c-110">It uses an LED to indicate when the Raspberry Pi processes a method invocation from the solution dashboard.</span></span>

<span data-ttu-id="c403c-111">Компоненты монтажной платы:</span><span class="sxs-lookup"><span data-stu-id="c403c-111">The components on the bread board are:</span></span>

- <span data-ttu-id="c403c-112">красный светодиодный индикатор;</span><span class="sxs-lookup"><span data-stu-id="c403c-112">Red LED</span></span>
- <span data-ttu-id="c403c-113">резистор 220 Ом (красный, красный, коричневый);</span><span class="sxs-lookup"><span data-stu-id="c403c-113">220-Ohm resistor (red, red, brown)</span></span>
- <span data-ttu-id="c403c-114">датчик BME280.</span><span class="sxs-lookup"><span data-stu-id="c403c-114">BME280 sensor</span></span>

<span data-ttu-id="c403c-115">На следующей схеме показано, как подключить оборудование.</span><span class="sxs-lookup"><span data-stu-id="c403c-115">The following diagram shows how to connect your hardware:</span></span>

![Подключение оборудования для Raspberry Pi][img-connection-diagram]

<span data-ttu-id="c403c-117">В следующей таблице перечислены подключения от Raspberry Pi к компонентам монтажной платы.</span><span class="sxs-lookup"><span data-stu-id="c403c-117">The following table summarizes the connections from the Raspberry Pi to the components on the breadboard:</span></span>

| <span data-ttu-id="c403c-118">Raspberry Pi</span><span class="sxs-lookup"><span data-stu-id="c403c-118">Raspberry Pi</span></span>            | <span data-ttu-id="c403c-119">Монтажная плата</span><span class="sxs-lookup"><span data-stu-id="c403c-119">Breadboard</span></span>             |<span data-ttu-id="c403c-120">Цвет</span><span class="sxs-lookup"><span data-stu-id="c403c-120">Color</span></span>         |
| ----------------------- | ---------------------- | ------------- |
| <span data-ttu-id="c403c-121">GND (вывод 14)</span><span class="sxs-lookup"><span data-stu-id="c403c-121">GND (Pin 14)</span></span>            | <span data-ttu-id="c403c-122">Индикатор, -ve (18A)</span><span class="sxs-lookup"><span data-stu-id="c403c-122">LED -ve pin (18A)</span></span>      | <span data-ttu-id="c403c-123">Сиреневый</span><span class="sxs-lookup"><span data-stu-id="c403c-123">Purple</span></span>          |
| <span data-ttu-id="c403c-124">GPCLK0 (вывод 7)</span><span class="sxs-lookup"><span data-stu-id="c403c-124">GPCLK0 (Pin 7)</span></span>          | <span data-ttu-id="c403c-125">Резистор (25A)</span><span class="sxs-lookup"><span data-stu-id="c403c-125">Resistor (25A)</span></span>         | <span data-ttu-id="c403c-126">Оранжевый</span><span class="sxs-lookup"><span data-stu-id="c403c-126">Orange</span></span>          |
| <span data-ttu-id="c403c-127">SPI_CE0 (вывод 24)</span><span class="sxs-lookup"><span data-stu-id="c403c-127">SPI_CE0 (Pin 24)</span></span>        | <span data-ttu-id="c403c-128">CS (39A)</span><span class="sxs-lookup"><span data-stu-id="c403c-128">CS (39A)</span></span>               | <span data-ttu-id="c403c-129">Синий</span><span class="sxs-lookup"><span data-stu-id="c403c-129">Blue</span></span>          |
| <span data-ttu-id="c403c-130">SPI_SCLK (вывод 23)</span><span class="sxs-lookup"><span data-stu-id="c403c-130">SPI_SCLK (Pin 23)</span></span>       | <span data-ttu-id="c403c-131">SCK (36A)</span><span class="sxs-lookup"><span data-stu-id="c403c-131">SCK (36A)</span></span>              | <span data-ttu-id="c403c-132">Желтый</span><span class="sxs-lookup"><span data-stu-id="c403c-132">Yellow</span></span>        |
| <span data-ttu-id="c403c-133">SPI_MISO (вывод 21)</span><span class="sxs-lookup"><span data-stu-id="c403c-133">SPI_MISO (Pin 21)</span></span>       | <span data-ttu-id="c403c-134">SDO (37A)</span><span class="sxs-lookup"><span data-stu-id="c403c-134">SDO (37A)</span></span>              | <span data-ttu-id="c403c-135">Белый</span><span class="sxs-lookup"><span data-stu-id="c403c-135">White</span></span>         |
| <span data-ttu-id="c403c-136">SPI MOSI (вывод 19)</span><span class="sxs-lookup"><span data-stu-id="c403c-136">SPI_MOSI (Pin 19)</span></span>       | <span data-ttu-id="c403c-137">SDI (38A)</span><span class="sxs-lookup"><span data-stu-id="c403c-137">SDI (38A)</span></span>              | <span data-ttu-id="c403c-138">Зеленый</span><span class="sxs-lookup"><span data-stu-id="c403c-138">Green</span></span>         |
| <span data-ttu-id="c403c-139">GND (вывод 6)</span><span class="sxs-lookup"><span data-stu-id="c403c-139">GND (Pin 6)</span></span>             | <span data-ttu-id="c403c-140">GND (35A)</span><span class="sxs-lookup"><span data-stu-id="c403c-140">GND (35A)</span></span>              | <span data-ttu-id="c403c-141">Черный</span><span class="sxs-lookup"><span data-stu-id="c403c-141">Black</span></span>         |
| <span data-ttu-id="c403c-142">3,3 В (вывод 1)</span><span class="sxs-lookup"><span data-stu-id="c403c-142">3.3 V (Pin 1)</span></span>           | <span data-ttu-id="c403c-143">3 В (34A)</span><span class="sxs-lookup"><span data-stu-id="c403c-143">3Vo (34A)</span></span>              | <span data-ttu-id="c403c-144">Красный</span><span class="sxs-lookup"><span data-stu-id="c403c-144">Red</span></span>           |

<span data-ttu-id="c403c-145">Чтобы завершить настройку оборудования, сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="c403c-145">To complete the hardware setup, you need to:</span></span>

- <span data-ttu-id="c403c-146">Подключите Raspberry Pi к источнику питания, входящему в состав набора.</span><span class="sxs-lookup"><span data-stu-id="c403c-146">Connect your Raspberry Pi to the power supply included in the kit.</span></span>
- <span data-ttu-id="c403c-147">Подключите Raspberry Pi к сети с помощью кабеля Ethernet, входящего в состав набора.</span><span class="sxs-lookup"><span data-stu-id="c403c-147">Connect your Raspberry Pi to your network using the Ethernet cable included in your kit.</span></span> <span data-ttu-id="c403c-148">Кроме того, для Raspberry Pi можно настроить [беспроводное подключение][lnk-pi-wireless].</span><span class="sxs-lookup"><span data-stu-id="c403c-148">Alternatively, you can set up [Wireless Connectivity][lnk-pi-wireless] for your Raspberry Pi.</span></span>

<span data-ttu-id="c403c-149">Установка оборудования для Raspberry Pi завершена.</span><span class="sxs-lookup"><span data-stu-id="c403c-149">You have now completed the hardware setup of your Raspberry Pi.</span></span>

### <a name="sign-in-and-access-the-terminal"></a><span data-ttu-id="c403c-150">Вход и доступ к терминалу</span><span class="sxs-lookup"><span data-stu-id="c403c-150">Sign in and access the terminal</span></span>

<span data-ttu-id="c403c-151">Существует два варианта получения доступа к среде терминала на Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="c403c-151">You have two options to access a terminal environment on your Raspberry Pi:</span></span>

- <span data-ttu-id="c403c-152">Если клавиатура и монитор подключены к Raspberry Pi, вы можете использовать графический пользовательский интерфейс Raspbian, чтобы получить доступ к окну терминала.</span><span class="sxs-lookup"><span data-stu-id="c403c-152">If you have a keyboard and monitor connected to your Raspberry Pi, you can use the Raspbian GUI to access a terminal window.</span></span>

- <span data-ttu-id="c403c-153">Получите доступ к командной строке на устройстве Raspberry Pi с настольного компьютера, используя SSH.</span><span class="sxs-lookup"><span data-stu-id="c403c-153">Access the command line on your Raspberry Pi using SSH from your desktop machine.</span></span>

#### <a name="use-a-terminal-window-in-the-gui"></a><span data-ttu-id="c403c-154">Использование окна терминала в графическом пользовательском интерфейсе</span><span class="sxs-lookup"><span data-stu-id="c403c-154">Use a terminal Window in the GUI</span></span>

<span data-ttu-id="c403c-155">По умолчанию в качестве учетных данных для Raspbian используется имя пользователя **pi** и пароль **raspberry**.</span><span class="sxs-lookup"><span data-stu-id="c403c-155">The default credentials for Raspbian are username **pi** and password **raspberry**.</span></span> <span data-ttu-id="c403c-156">На панели задач в графическом пользовательском интерфейсе можно запустить служебную программу **Terminal** с помощью значка в виде монитора.</span><span class="sxs-lookup"><span data-stu-id="c403c-156">In the task bar in the GUI, you can launch the **Terminal** utility using the icon that looks like a monitor.</span></span>

#### <a name="sign-in-with-ssh"></a><span data-ttu-id="c403c-157">Вход с помощью SSH</span><span class="sxs-lookup"><span data-stu-id="c403c-157">Sign in with SSH</span></span>

<span data-ttu-id="c403c-158">Используйте SSH, чтобы получить доступ к Raspberry Pi с помощью командной строки.</span><span class="sxs-lookup"><span data-stu-id="c403c-158">You can use SSH for command-line access to your Raspberry Pi.</span></span> <span data-ttu-id="c403c-159">Сведения о настройке SSH на устройстве Raspberry Pi и о подключении из [Windows][lnk-ssh-windows], [Linux и Mac OS][lnk-ssh-linux] см. в руководстве по [SSH (SECURE SHELL)][lnk-pi-ssh].</span><span class="sxs-lookup"><span data-stu-id="c403c-159">The article [SSH (Secure Shell)][lnk-pi-ssh] describes how to configure SSH on your Raspberry Pi, and how to connect from [Windows][lnk-ssh-windows] or [Linux & Mac OS][lnk-ssh-linux].</span></span>

<span data-ttu-id="c403c-160">Войдите, используя имя пользователя **pi** и пароль **raspberry**.</span><span class="sxs-lookup"><span data-stu-id="c403c-160">Sign in with username **pi** and password **raspberry**.</span></span>

#### <a name="optional-share-a-folder-on-your-raspberry-pi"></a><span data-ttu-id="c403c-161">Совместный доступ к папке на устройстве Raspberry Pi (необязательно)</span><span class="sxs-lookup"><span data-stu-id="c403c-161">Optional: Share a folder on your Raspberry Pi</span></span>

<span data-ttu-id="c403c-162">При необходимости вы можете предоставить общий доступ к папке на устройстве Raspberry Pi для среды рабочего стола.</span><span class="sxs-lookup"><span data-stu-id="c403c-162">Optionally, you may want to share a folder on your Raspberry Pi with your desktop environment.</span></span> <span data-ttu-id="c403c-163">Предоставив общий доступ к папке, вы сможете использовать предпочитаемый классический текстовый редактор (например, [Visual Studio Code](https://code.visualstudio.com/) или [Sublime Text](http://www.sublimetext.com/)), чтобы редактировать файлы на устройстве Raspberry Pi вместо использования `nano` или `vi`.</span><span class="sxs-lookup"><span data-stu-id="c403c-163">Sharing a folder enables you to use your preferred desktop text editor (such as [Visual Studio Code](https://code.visualstudio.com/) or [Sublime Text](http://www.sublimetext.com/)) to edit files on your Raspberry Pi instead of using `nano` or `vi`.</span></span>

<span data-ttu-id="c403c-164">Чтобы предоставить общий доступ к папке в Windows, необходимо настроить сервер Samba на устройстве Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="c403c-164">To share a folder with Windows, configure a Samba server on the Raspberry Pi.</span></span> <span data-ttu-id="c403c-165">Вы также можете использовать встроенный сервер [SFTP](https://www.raspberrypi.org/documentation/remote-access/) с клиентом SFTP на настольном компьютере.</span><span class="sxs-lookup"><span data-stu-id="c403c-165">Alternatively, use the built-in [SFTP](https://www.raspberrypi.org/documentation/remote-access/) server with an SFTP client on your desktop.</span></span>

### <a name="enable-spi"></a><span data-ttu-id="c403c-166">Включение SPI</span><span class="sxs-lookup"><span data-stu-id="c403c-166">Enable SPI</span></span>

<span data-ttu-id="c403c-167">Прежде чем запустить пример приложения, необходимо включить шину последовательного периферийного интерфейса (SPI) на Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="c403c-167">Before you can run the sample application, you must enable the Serial Peripheral Interface (SPI) bus on the Raspberry Pi.</span></span> <span data-ttu-id="c403c-168">Raspberry Pi взаимодействует с датчиком BME280 через шину SPI.</span><span class="sxs-lookup"><span data-stu-id="c403c-168">The Raspberry Pi communicates with the BME280 sensor device over the SPI bus.</span></span> <span data-ttu-id="c403c-169">Выполните следующую команду, чтобы изменить файл конфигурации:</span><span class="sxs-lookup"><span data-stu-id="c403c-169">Use the following command to edit the configuration file:</span></span>

```sh
sudo nano /boot/config.txt
```

<span data-ttu-id="c403c-170">Найдите следующую строку:</span><span class="sxs-lookup"><span data-stu-id="c403c-170">Find the line:</span></span>

`#dtparam=spi=on`

- <span data-ttu-id="c403c-171">Чтобы раскомментировать строку, удалите `#` в начале.</span><span class="sxs-lookup"><span data-stu-id="c403c-171">To uncomment the line, delete the `#` at the start.</span></span>
- <span data-ttu-id="c403c-172">Сохраните изменения (**CTRL+O**, **ВВОД**) и закройте редактор (**CTRL+X**).</span><span class="sxs-lookup"><span data-stu-id="c403c-172">Save your changes (**Ctrl-O**, **Enter**) and exit the editor (**Ctrl-X**).</span></span>
- <span data-ttu-id="c403c-173">Чтобы включить SPI, перезагрузите Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="c403c-173">To enable SPI, reboot the Raspberry Pi.</span></span> <span data-ttu-id="c403c-174">При перезагрузке будет отключен терминал, поэтому после перезапуска Raspberry Pi необходимо будет выполнить повторный вход:</span><span class="sxs-lookup"><span data-stu-id="c403c-174">Rebooting disconnects the terminal, you need to sign in again when the Raspberry Pi restarts:</span></span>

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