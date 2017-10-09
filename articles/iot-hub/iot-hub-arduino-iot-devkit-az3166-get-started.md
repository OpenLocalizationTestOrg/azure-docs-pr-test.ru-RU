---
title: "toocloud набор разработки aaaIoT - tooAzure подключения AZ3166 набор разработки IoT центр IoT | Документы Microsoft"
description: "Узнайте, как toosetup и подключите набор разработки AZ3166 IoT tooAzure центр IoT для него toosend данных toohello Azure облачной платформы в этом учебнике."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: 
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/11/2017
ms.author: xshi
ms.openlocfilehash: fd36abaed1fd9f73028b84312bca9e900fb9c004
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="connect-iot-devkit-az3166-tooazure-iot-hub-in-hello-cloud"></a><span data-ttu-id="aafc8-103">Подключение AZ3166 набор разработки IoT tooAzure центр IoT в облаке hello</span><span class="sxs-lookup"><span data-stu-id="aafc8-103">Connect IoT DevKit AZ3166 tooAzure IoT Hub in hello cloud</span></span>

[!INCLUDE [iot-hub-get-started-device-selector](../../includes/iot-hub-get-started-device-selector.md)]

<span data-ttu-id="aafc8-104">Hello [набор разработки IoT MXChip](https://microsoft.github.io/azure-iot-developer-kit/) можно использовать toodevelop и прототип Интернета вещей (IoT) решения, использующие службы Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="aafc8-104">hello [MXChip IoT DevKit](https://microsoft.github.io/azure-iot-developer-kit/) can be used toodevelop and prototype Internet of Things (IoT) solutions leveraging Microsoft Azure services.</span></span> <span data-ttu-id="aafc8-105">Он содержит совместимую с Arduino плату со множеством периферийных устройств и датчиков, пакет ПО для платы с открытым кодом и расширяющийся [каталог проектов](https://microsoft.github.io/azure-iot-developer-kit/docs/projects/).</span><span class="sxs-lookup"><span data-stu-id="aafc8-105">It includes an Arduino compatible board with rich peripherals and sensors, an open-source board package and a growing [projects catalog](https://microsoft.github.io/azure-iot-developer-kit/docs/projects/).</span></span>

## <a name="what-you-do"></a><span data-ttu-id="aafc8-106">В рамках этого руководства мы:</span><span class="sxs-lookup"><span data-stu-id="aafc8-106">What you do</span></span>
<span data-ttu-id="aafc8-107">Подключение [набор разработки](https://microsoft.github.io/azure-iot-developer-kit/) центр Azure IoT tooan создать сбор hello датчиков температуры и влажности данных и отправки hello данных tooIoT концентратора.</span><span class="sxs-lookup"><span data-stu-id="aafc8-107">Connect [DevKit](https://microsoft.github.io/azure-iot-developer-kit/) tooan Azure IoT hub that you create, collect hello temperature and humidity data from sensors and send hello data tooIoT hub.</span></span>

<span data-ttu-id="aafc8-108">У вас еще нет платы DevKit?</span><span class="sxs-lookup"><span data-stu-id="aafc8-108">Don't have a DevKit yet?</span></span> <span data-ttu-id="aafc8-109">Вы можете новую плату DevKit [здесь](https://aka.ms/iot-devkit-purchase).</span><span class="sxs-lookup"><span data-stu-id="aafc8-109">Get a new one [here](https://aka.ms/iot-devkit-purchase).</span></span>

## <a name="what-you-learn"></a><span data-ttu-id="aafc8-110">Что вы узнаете</span><span class="sxs-lookup"><span data-stu-id="aafc8-110">What you learn</span></span>

* <span data-ttu-id="aafc8-111">Как tooconnect доступа tooWireless набор разработки IoT пункт и подготовить среду разработки.</span><span class="sxs-lookup"><span data-stu-id="aafc8-111">How tooconnect IoT DevKit tooWireless access point and prepare your development environment.</span></span>
* <span data-ttu-id="aafc8-112">Как toocreate центр IoT и регистрация устройства для набор разработки MXChip IoT.</span><span class="sxs-lookup"><span data-stu-id="aafc8-112">How toocreate an IoT hub and register a device for MXChip IoT DevKit.</span></span>
* <span data-ttu-id="aafc8-113">Как toocollect датчиков, выполнив пример приложения на набор разработки MXChip IoT.</span><span class="sxs-lookup"><span data-stu-id="aafc8-113">How toocollect sensor data by running a sample application on MXChip IoT DevKit.</span></span>
* <span data-ttu-id="aafc8-114">Как toosend hello центра IoT tooyour данных датчика.</span><span class="sxs-lookup"><span data-stu-id="aafc8-114">How toosend hello sensor data tooyour IoT hub.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="aafc8-115">Необходимые элементы</span><span class="sxs-lookup"><span data-stu-id="aafc8-115">What you need</span></span>

* <span data-ttu-id="aafc8-116">Плата MXChip IoT DevKit с кабелем micro USB.</span><span class="sxs-lookup"><span data-stu-id="aafc8-116">An MXChip IoT DevKit board with a micro USB cable.</span></span> <span data-ttu-id="aafc8-117">Вы можете [получить ее прямо сейчас](https://aka.ms/iot-devkit-purchase).</span><span class="sxs-lookup"><span data-stu-id="aafc8-117">[Get it now](https://aka.ms/iot-devkit-purchase)</span></span>
* <span data-ttu-id="aafc8-118">Компьютер под управлением Windows 10 или macOS 10.10 (или более поздней версии).</span><span class="sxs-lookup"><span data-stu-id="aafc8-118">A computer running Windows 10 or macOS 10.10+</span></span>
* <span data-ttu-id="aafc8-119">активная подписка Azure;</span><span class="sxs-lookup"><span data-stu-id="aafc8-119">An active Azure subscription</span></span>
  * <span data-ttu-id="aafc8-120">Вы можете активировать [бесплатную 30-дневную пробную учетную запись Microsoft Azure](https://azureinfo.microsoft.com/us-freetrial.html).</span><span class="sxs-lookup"><span data-stu-id="aafc8-120">Activate a [free 30-day trial Microsoft Azure account](https://azureinfo.microsoft.com/us-freetrial.html)</span></span>

## <a name="prepare-your-hardware"></a><span data-ttu-id="aafc8-121">Подготовка оборудования</span><span class="sxs-lookup"><span data-stu-id="aafc8-121">Prepare your hardware</span></span>

<span data-ttu-id="aafc8-122">Подключить компьютер tooyour hello оборудования.</span><span class="sxs-lookup"><span data-stu-id="aafc8-122">Hook up hello hardware tooyour computer.</span></span>

### <a name="hardware-you-need"></a><span data-ttu-id="aafc8-123">Необходимое оборудование</span><span class="sxs-lookup"><span data-stu-id="aafc8-123">Hardware you need</span></span>

* <span data-ttu-id="aafc8-124">Плата DevKit.</span><span class="sxs-lookup"><span data-stu-id="aafc8-124">DevKit board</span></span>
* <span data-ttu-id="aafc8-125">Кабель micro USB.</span><span class="sxs-lookup"><span data-stu-id="aafc8-125">Micro USB cable</span></span>

![Приступая к работе: оборудование](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/hardware.jpg)

### <a name="connect-devkit-tooyour-computer"></a><span data-ttu-id="aafc8-127">Подключите компьютер tooyour набор разработки</span><span class="sxs-lookup"><span data-stu-id="aafc8-127">Connect DevKit tooyour computer</span></span>

1. <span data-ttu-id="aafc8-128">Подключение USB окончания tooyour ПК</span><span class="sxs-lookup"><span data-stu-id="aafc8-128">Connect USB end tooyour PC</span></span>
2. <span data-ttu-id="aafc8-129">Подключение Micro USB окончания toohello набор разработки</span><span class="sxs-lookup"><span data-stu-id="aafc8-129">Connect Micro USB end toohello DevKit</span></span>
3. <span data-ttu-id="aafc8-130">Далее toopower Hello зеленый Индикатор подтверждает подключения</span><span class="sxs-lookup"><span data-stu-id="aafc8-130">hello green LED next toopower confirms connection</span></span>

![Приступая к работе: подключение](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/connect.jpg)

## <a name="configure-wifi"></a><span data-ttu-id="aafc8-132">Настройка Wi-Fi</span><span class="sxs-lookup"><span data-stu-id="aafc8-132">Configure WiFi</span></span>

<span data-ttu-id="aafc8-133">Для работы проектов Центра Интернета вещей требуется подключение к Интернету.</span><span class="sxs-lookup"><span data-stu-id="aafc8-133">IoT projects rely on Internet connectivity.</span></span> <span data-ttu-id="aafc8-134">Используйте следующие инструкции tooconfigure hello набор разработки tooconnect tooWiFi hello.</span><span class="sxs-lookup"><span data-stu-id="aafc8-134">Use hello following instructions tooconfigure hello DevKit tooconnect tooWiFi.</span></span>

### <a name="enter-ap-mode"></a><span data-ttu-id="aafc8-135">Переключение в режим точки беспроводного доступа</span><span class="sxs-lookup"><span data-stu-id="aafc8-135">Enter AP Mode</span></span>

<span data-ttu-id="aafc8-136">Удерживая нажатой кнопку B, то push и отпустите кнопку "сбросить" hello, а затем кнопку выпуск б. Ваш набор разработки входит в режим доступа для настройки Wi-Fi.</span><span class="sxs-lookup"><span data-stu-id="aafc8-136">Hold down button B, then push and release hello reset button, then release button B. Your DevKit will enter AP Mode for configuring WiFi.</span></span> <span data-ttu-id="aafc8-137">Hello отобразится экран приветствия Identifier(SSID) установите службы из hello набор разработки, а также hello конфигурации портала IP-адрес:</span><span class="sxs-lookup"><span data-stu-id="aafc8-137">hello screen will display hello Service Set Identifier(SSID) of hello DevKit as well as hello configuration portal IP address:</span></span>

![Приступая к работе: настройка Wi-Fi](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/wifi-ap.jpg)

### <a name="connect-toodevkit-ap"></a><span data-ttu-id="aafc8-139">Подключение tooDevKit AP</span><span class="sxs-lookup"><span data-stu-id="aafc8-139">Connect tooDevKit AP</span></span>

<span data-ttu-id="aafc8-140">Теперь использование другого Wi-Fi включена устройств (ПК или мобильный телефон) tooconnect toohello набор разработки SSID (выделены hello экрана выше), оставьте пустым паролем hello.</span><span class="sxs-lookup"><span data-stu-id="aafc8-140">Now, use another WiFi enabled device (PC or mobile phone) tooconnect toohello DevKit SSID (highlighted in hello screenshot above), leave hello password empty.</span></span>

![Приступая к работе: идентификатор SSID](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/connect-ssid.png)

### <a name="configure-wifi-for-devkit"></a><span data-ttu-id="aafc8-142">Настройка Wi-Fi для платы DevKit</span><span class="sxs-lookup"><span data-stu-id="aafc8-142">Configure WiFi for DevKit</span></span>

<span data-ttu-id="aafc8-143">Откройте hello IP-адрес, на экране приветствия набор разработки на ПК или в браузере мобильного телефона, выберите сеть Wi-Fi hello нужные hello tooconnect набор разработки для, а затем введите пароль hello.</span><span class="sxs-lookup"><span data-stu-id="aafc8-143">Open hello IP address shown on hello DevKit screen on your PC or mobile phone browser, select hello WiFi network you want hello DevKit tooconnect to, then type hello password.</span></span> <span data-ttu-id="aafc8-144">Нажмите кнопку **Connect** toocomplete:</span><span class="sxs-lookup"><span data-stu-id="aafc8-144">Click **Connect** toocomplete:</span></span>

![Приступая к работе: портал настройки Wi-Fi](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/wifi-portal.png)

<span data-ttu-id="aafc8-146">После успешного соединения hello hello набор разработки перезагрузится через несколько секунд.</span><span class="sxs-lookup"><span data-stu-id="aafc8-146">Once hello connection succeeds, hello DevKit will reboot in a few seconds.</span></span> <span data-ttu-id="aafc8-147">Если выполнено успешно, на экране приветствия появится hello Wi-Fi имя и IP-адрес:</span><span class="sxs-lookup"><span data-stu-id="aafc8-147">If succeeded, you will see hello WiFi name and IP address on hello screen:</span></span>

![Приступая к работе: IP-адрес для Wi-Fi](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/wifi-ip.jpg)

> [!NOTE] 
<span data-ttu-id="aafc8-149">отображаемый в фото hello Hello IP-адрес может не соответствовать hello фактических IP назначается и отображается на экране приветствия набор разработки.</span><span class="sxs-lookup"><span data-stu-id="aafc8-149">hello IP address displayed in hello photo may not match hello actual IP assigned and displayed on hello DevKit screen.</span></span> <span data-ttu-id="aafc8-150">Это нормально, как Wi-Fi использует DHCP toodynamically назначение IP-адресов.</span><span class="sxs-lookup"><span data-stu-id="aafc8-150">This is normal as WiFi uses DHCP toodynamically assign IPs.</span></span>

<span data-ttu-id="aafc8-151">После настройки Wi-Fi учетные данные останутся на hello устройства для этого соединения, даже если не подключен.</span><span class="sxs-lookup"><span data-stu-id="aafc8-151">After WiFi is configured, your credentials will be persisted on hello device for that connection, even if unplugged.</span></span> <span data-ttu-id="aafc8-152">Например, если вы настроили hello набор разработки для Wi-Fi дома и затем потребовалось hello набор разработки toohello office, необходимо будет tooreconfigure AP режим (начиная с шага **войти в режим AP**) tooconnect hello office tooyour набор разработки Wi-Fi.</span><span class="sxs-lookup"><span data-stu-id="aafc8-152">For example, if you configured hello DevKit for WiFi in your home and then took hello DevKit toohello office, you will need tooreconfigure AP mode (starting at step **Enter AP Mode**) tooconnect hello DevKit tooyour office WiFi.</span></span> 

## <a name="start-using-devkit"></a><span data-ttu-id="aafc8-153">Начало использования платы DevKit</span><span class="sxs-lookup"><span data-stu-id="aafc8-153">Start using DevKit</span></span>

<span data-ttu-id="aafc8-154">приложение по умолчанию Hello, работающих на набор разработки проверка hello последняя версия встроенного по hello и выводится некоторые данные диагностики датчика для вас.</span><span class="sxs-lookup"><span data-stu-id="aafc8-154">hello default app running on DevKit will check hello latest version of hello firmware and display some sensor diagnosis data for you.</span></span>

### <a name="upgrade-toohello-latest-firmware"></a><span data-ttu-id="aafc8-155">Обновление toohello последняя версия встроенного по</span><span class="sxs-lookup"><span data-stu-id="aafc8-155">Upgrade toohello latest firmware</span></span>

<span data-ttu-id="aafc8-156">Появится на экране приветствия, обе версии встроенного по последняя hello, при необходимости обновления.</span><span class="sxs-lookup"><span data-stu-id="aafc8-156">You will be prompted on hello screen both hello current and latest firmware version if there is an upgrade needed.</span></span> <span data-ttu-id="aafc8-157">Выполните [обновления микропрограммы](https://microsoft.github.io/azure-iot-developer-kit/docs/upgrading/) руководство tooupgrade его.</span><span class="sxs-lookup"><span data-stu-id="aafc8-157">Follow [Upgrade firmware](https://microsoft.github.io/azure-iot-developer-kit/docs/upgrading/) guide tooupgrade it.</span></span>

![Приступая к работе: встроенное ПО](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/firmware.jpg)

> [!NOTE] 
<span data-ttu-id="aafc8-159">Это однократное усилия, после начала разработки на hello набор разработки и отправить приложение, вы получите последнюю версию встроенного по hello поставляются вместе с приложением.</span><span class="sxs-lookup"><span data-stu-id="aafc8-159">This is a one-time effort, once you start developing on hello DevKit and upload your app, you will have hello latest firmware come with your app.</span></span>

### <a name="test-various-sensors"></a><span data-ttu-id="aafc8-160">Тестирование различных датчиков</span><span class="sxs-lookup"><span data-stu-id="aafc8-160">Test various sensors</span></span>

<span data-ttu-id="aafc8-161">Нажмите кнопку B tootest датчиков, продолжать, нажатие и отпускание кнопки toocycle hello B через каждого датчика.</span><span class="sxs-lookup"><span data-stu-id="aafc8-161">Press button B tootest sensors, continue pressing and releasing hello B button toocycle through each sensor.</span></span>

![Приступая к работе: датчики](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/sensors.jpg)

## <a name="prepare-development-environment"></a><span data-ttu-id="aafc8-163">Подготовка среды разработки</span><span class="sxs-lookup"><span data-stu-id="aafc8-163">Prepare development environment</span></span>

<span data-ttu-id="aafc8-164">Теперь настало время tooset hello среды разработки: средства и пакеты для toobuild привлекательных приложений IoT.</span><span class="sxs-lookup"><span data-stu-id="aafc8-164">Now it's time tooset up hello development environment: tools and packages for you toobuild stunning IoT applications.</span></span> <span data-ttu-id="aafc8-165">Можно выбрать Windows или tooyour операционной системы в соответствии с версией macOS.</span><span class="sxs-lookup"><span data-stu-id="aafc8-165">You can choose Windows or macOS version according tooyour operating system.</span></span>


### <a name="windows"></a><span data-ttu-id="aafc8-166">Windows</span><span class="sxs-lookup"><span data-stu-id="aafc8-166">Windows</span></span>

<span data-ttu-id="aafc8-167">Мы рекомендуем вам toouse hello установки пакета tooprepare hello среды разработки.</span><span class="sxs-lookup"><span data-stu-id="aafc8-167">We encourage you toouse hello installation package tooprepare hello development environment.</span></span> <span data-ttu-id="aafc8-168">Если возникли проблемы, можно выполнить hello [действия вручную](https://microsoft.github.io/azure-iot-developer-kit/docs/installation/) tooget своей работы.</span><span class="sxs-lookup"><span data-stu-id="aafc8-168">If you encounter any issues, you can follow hello [manual steps](https://microsoft.github.io/azure-iot-developer-kit/docs/installation/) tooget it done.</span></span>

#### <a name="download-latest-package"></a><span data-ttu-id="aafc8-169">Скачивание последней версии пакета</span><span class="sxs-lookup"><span data-stu-id="aafc8-169">Download latest package</span></span>

<span data-ttu-id="aafc8-170">Hello `.zip` загрузке файл содержит все необходимые средства и пакеты, необходимые для разработки набор разработки.</span><span class="sxs-lookup"><span data-stu-id="aafc8-170">hello `.zip` file you download contains all necessary tools and packages required for DevKit development.</span></span>

> [!div class="button"]
[<span data-ttu-id="aafc8-171">Загрузить</span><span class="sxs-lookup"><span data-stu-id="aafc8-171">Download</span></span>](https://azureboard.azureedge.net/prod/installpackage/devkit_install_1.0.2.zip)


> [!NOTE] 
> <span data-ttu-id="aafc8-172">Hello `.zip` файл содержит hello следующие средства и пакеты.</span><span class="sxs-lookup"><span data-stu-id="aafc8-172">hello `.zip` file contains hello following tools and packages.</span></span> <span data-ttu-id="aafc8-173">Если уже установлены некоторые компоненты, скрипт hello обнаружит и пропустить их.</span><span class="sxs-lookup"><span data-stu-id="aafc8-173">If you already have some components installed, hello script will detect and skip them.</span></span>
> * <span data-ttu-id="aafc8-174">Node.js и Yarn: среда выполнения для сценария установки hello и автоматизированных задач</span><span class="sxs-lookup"><span data-stu-id="aafc8-174">Node.js and Yarn: Runtime for hello setup script and automated tasks</span></span>
> * <span data-ttu-id="aafc8-175">[Azure CLI 2.0 MSI](https://docs.microsoft.com//cli/azure/install-azure-cli#windows) -кросс платформенных взаимодействие с командной строки для управления ресурсами Azure, hello MSI-ФАЙЛ содержит зависимые Python и PIP-адрес.</span><span class="sxs-lookup"><span data-stu-id="aafc8-175">[Azure CLI 2.0 MSI](https://docs.microsoft.com//cli/azure/install-azure-cli#windows) - Cross-platform command-line experience for managing Azure resources, hello MSI contains dependent Python and pip.</span></span>
> * <span data-ttu-id="aafc8-176">[Visual Studio Code](https://code.visualstudio.com/): упрощенный редактор кода для разработки для платы DevKit.</span><span class="sxs-lookup"><span data-stu-id="aafc8-176">[Visual Studio Code](https://code.visualstudio.com/): Lightweight code editor for DevKit development</span></span>
> * <span data-ttu-id="aafc8-177">[Расширение Visual Studio Code для Arduino](https://marketplace.visualstudio.com/items?itemName=vsciot-vscode.vscode-arduino): обеспечивает разработку для Arduino в VS Code.</span><span class="sxs-lookup"><span data-stu-id="aafc8-177">[Visual Studio Code extension for Arduino](https://marketplace.visualstudio.com/items?itemName=vsciot-vscode.vscode-arduino): Enables Arduino development in VS Code</span></span>
> * <span data-ttu-id="aafc8-178">[Интегрированная среда разработки Arduino](https://www.arduino.cc/en/Main/Software): hello расширение для Arduino зависит от этого средства</span><span class="sxs-lookup"><span data-stu-id="aafc8-178">[Arduino IDE](https://www.arduino.cc/en/Main/Software): hello extension for Arduino relies on this tool</span></span>
> * <span data-ttu-id="aafc8-179">Пакет платы набор разработки: Средства цепочки, библиотеки и проекты для hello набор разработки</span><span class="sxs-lookup"><span data-stu-id="aafc8-179">DevKit Board Package: Tool chains, libraries and projects for hello DevKit</span></span>
> * <span data-ttu-id="aafc8-180">Служебная программа ST-Link: необходимые служебные программы и драйверы.</span><span class="sxs-lookup"><span data-stu-id="aafc8-180">ST-Link Utility: Essential utilities and drivers</span></span>

#### <a name="run-installation-script"></a><span data-ttu-id="aafc8-181">Запуск сценария установки</span><span class="sxs-lookup"><span data-stu-id="aafc8-181">Run installation script</span></span>

<span data-ttu-id="aafc8-182">В проводнике Windows найдите hello `.zip` и извлеките его, найдите `install.cmd`, щелкните правой кнопкой мыши и выберите **«Запуск от имени администратора»** toostart.</span><span class="sxs-lookup"><span data-stu-id="aafc8-182">In Windows File Explorer, locate hello `.zip` and extract it, find `install.cmd`, right-click and select **"Run as administrator"** toostart.</span></span>

![Приступая к работе: запуск от имени администратора](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/run-admin.png)

<span data-ttu-id="aafc8-184">Во время установки вы увидите ход hello каждый инструмент или пакета.</span><span class="sxs-lookup"><span data-stu-id="aafc8-184">During installation, you will see hello progress of each tool or package.</span></span>

![Приступая к работе: установка](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/install.png)

#### <a name="confirm-tooinstall-drivers"></a><span data-ttu-id="aafc8-186">Подтвердите tooinstall драйверы</span><span class="sxs-lookup"><span data-stu-id="aafc8-186">Confirm tooinstall drivers</span></span>

<span data-ttu-id="aafc8-187">Hello VS Code для расширения Arduino использует hello Arduino интегрированной среды разработки.</span><span class="sxs-lookup"><span data-stu-id="aafc8-187">hello VS Code for Arduino extension relies on hello Arduino IDE.</span></span> <span data-ttu-id="aafc8-188">Если это hello впервые устанавливаете hello Arduino IDE, будут использоваться запрашиваемые tooinstall соответствующие драйверы:</span><span class="sxs-lookup"><span data-stu-id="aafc8-188">If this is hello first time you are installing hello Arduino IDE, you will be prompted tooinstall relevant drivers:</span></span>

![Приступая к работе: драйвер](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/driver.png)

<span data-ttu-id="aafc8-190">Может потребоваться установка toofinish около 10 минут в зависимости от быстродействия Internet.</span><span class="sxs-lookup"><span data-stu-id="aafc8-190">It should take around 10 minutes toofinish installation depending on your Internet speed.</span></span> <span data-ttu-id="aafc8-191">После завершения установки hello, вы увидите кода Visual Studio и интегрированной среды разработки Arduino ярлыки на рабочем столе.</span><span class="sxs-lookup"><span data-stu-id="aafc8-191">Once hello installation is complete, you should see Visual Studio Code and Arduino IDE shortcuts on your desktop.</span></span>

> [!NOTE] 
<span data-ttu-id="aafc8-192">В некоторых случаях при запуске VS Code появляется сообщение об ошибке. В нем сообщается, что не удается найти интегрированную среду разработки Arduino или связанный пакет ПО для платы.</span><span class="sxs-lookup"><span data-stu-id="aafc8-192">Occasionally, when you launch VS Code, you will be prompted with an error that cannot find Arduino IDE or related board package.</span></span> <span data-ttu-id="aafc8-193">toosolve его закрыть VS Code Arduino IDE запустить один раз и VS Code должна правильно определить путь Arduino IDE.</span><span class="sxs-lookup"><span data-stu-id="aafc8-193">toosolve it, close VS Code, launch Arduino IDE once and VS Code should locate Arduino IDE path correctly.</span></span>


### <a name="macos-preview"></a><span data-ttu-id="aafc8-194">macOS (предварительная версия)</span><span class="sxs-lookup"><span data-stu-id="aafc8-194">macOS (Preview)</span></span>

<span data-ttu-id="aafc8-195">Выполните эти среды разработки tooprepare действия на macOS.</span><span class="sxs-lookup"><span data-stu-id="aafc8-195">Follow these steps tooprepare development environment on macOS.</span></span>

#### <a name="install-azure-cli-20"></a><span data-ttu-id="aafc8-196">Установка Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="aafc8-196">Install Azure CLI 2.0</span></span>

<span data-ttu-id="aafc8-197">Выполните hello [официальный руководство](https://docs.microsoft.com//cli/azure/install-azure-cli) tooinstall Azure CLI 2.0:</span><span class="sxs-lookup"><span data-stu-id="aafc8-197">Follow hello [official guide](https://docs.microsoft.com//cli/azure/install-azure-cli) tooinstall Azure CLI 2.0:</span></span>

<span data-ttu-id="aafc8-198">Azure CLI 2.0 можно установить с помощью одной команды `curl`.</span><span class="sxs-lookup"><span data-stu-id="aafc8-198">Install Azure CLI 2.0 with one `curl` command:</span></span>

```bash
curl -L https://aka.ms/InstallAzureCli | bash
```

<span data-ttu-id="aafc8-199">И перезапустите вашей командной оболочки для изменения эффекта tootake:</span><span class="sxs-lookup"><span data-stu-id="aafc8-199">And restart your command shell for changes tootake effect:</span></span>

```bash
exec -l $SHELL
```

#### <a name="install-arduino-ide"></a><span data-ttu-id="aafc8-200">Установка интегрированной среды разработки Arduino</span><span class="sxs-lookup"><span data-stu-id="aafc8-200">Install Arduino IDE</span></span>

<span data-ttu-id="aafc8-201">Hello расширения Arduino кода Visual Studio использует hello Arduino интегрированной среды разработки.</span><span class="sxs-lookup"><span data-stu-id="aafc8-201">hello Visual Studio Code Arduino extension relies on hello Arduino IDE.</span></span> <span data-ttu-id="aafc8-202">Загрузите и установите hello [Arduino интегрированную среду разработки для macOS](https://www.arduino.cc/en/Main/Software).</span><span class="sxs-lookup"><span data-stu-id="aafc8-202">Download and install hello [Arduino IDE for macOS](https://www.arduino.cc/en/Main/Software).</span></span>

#### <a name="install-visual-studio-code"></a><span data-ttu-id="aafc8-203">Установка Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="aafc8-203">Install Visual Studio Code</span></span>

<span data-ttu-id="aafc8-204">Скачайте и установите [Visual Studio Code для macOS](https://code.visualstudio.com/).</span><span class="sxs-lookup"><span data-stu-id="aafc8-204">Download and install [Visual Studio Code for macOS](https://code.visualstudio.com/).</span></span> <span data-ttu-id="aafc8-205">Это будет hello средство первичной разработки для создания IoT набор разработки приложений.</span><span class="sxs-lookup"><span data-stu-id="aafc8-205">This will be hello primary development tool for building DevKit IoT applications.</span></span>

####  <a name="download-latest-package"></a><span data-ttu-id="aafc8-206">Скачивание последней версии пакета</span><span class="sxs-lookup"><span data-stu-id="aafc8-206">Download latest package</span></span>

1. <span data-ttu-id="aafc8-207">Установите Node.js.</span><span class="sxs-lookup"><span data-stu-id="aafc8-207">Install Node.js.</span></span> <span data-ttu-id="aafc8-208">Можно использовать диспетчер пакетов популярных macOS [Homebrew](https://brew.sh/) или [готовые установщика](https://nodejs.org/en/download/) tooinstall его.</span><span class="sxs-lookup"><span data-stu-id="aafc8-208">You can use popular macOS package manager [Homebrew](https://brew.sh/) or [pre-built installer](https://nodejs.org/en/download/) tooinstall it.</span></span>

2. <span data-ttu-id="aafc8-209">Скачайте файл с расширением `.zip`, содержащий сценарии задач, необходимые для разработки для DevKit в VS Code.</span><span class="sxs-lookup"><span data-stu-id="aafc8-209">Download `.zip` file containing task scripts required for DevKit development in VS Code.</span></span>

   > [!div class="button"]
   [<span data-ttu-id="aafc8-210">Загрузить</span><span class="sxs-lookup"><span data-stu-id="aafc8-210">Download</span></span>](https://azureboard.azureedge.net/installpackage/devkit_tasks_1.0.2.zip)

   <span data-ttu-id="aafc8-211">Найдите hello `.zip` и извлеките его.</span><span class="sxs-lookup"><span data-stu-id="aafc8-211">Locate hello `.zip` and extract it.</span></span> <span data-ttu-id="aafc8-212">Затем запустите **терминалов** приложения и выполнения hello, следуя tooconfigure команды:</span><span class="sxs-lookup"><span data-stu-id="aafc8-212">Then launch **Terminal** app and run hello following commands tooconfigure:</span></span>

   <span data-ttu-id="aafc8-213">Переместите папку пользователя macOS tooyour извлеченную папку:</span><span class="sxs-lookup"><span data-stu-id="aafc8-213">Move extracted folder tooyour macOS user folder:</span></span>
   ```bash
   mv [.zip extracted folder]/azure-board-cli ~/. ; cd ~/azure-board-cli
   ```
  
   <span data-ttu-id="aafc8-214">Установите пакеты `npm`.</span><span class="sxs-lookup"><span data-stu-id="aafc8-214">Install `npm` packages:</span></span>
   ```
   npm install
   ```

#### <a name="install-vs-code-extension-for-arduino"></a><span data-ttu-id="aafc8-215">Расширение VS Code для Arduino</span><span class="sxs-lookup"><span data-stu-id="aafc8-215">Install VS Code extension for Arduino</span></span>

<span data-ttu-id="aafc8-216">Код Visual Studio позволяет tooinstall Marketplace расширений непосредственно в средстве hello, просто щелкните значок расширения hello в левом меню области hello и найдите `Arduino` tooinstall:</span><span class="sxs-lookup"><span data-stu-id="aafc8-216">Visual Studio Code allows you tooinstall Marketplace extensions directly in hello tool, simply click hello extensions icon in hello left menu pane and then search `Arduino` tooinstall:</span></span>

![Установка: расширения](media/iot-hub-arduino-devkit-az3166-get-started/installation-extensions-mac.png)

#### <a name="install-devkit-board-package"></a><span data-ttu-id="aafc8-218">Установка пакета ПО для платы DevKit</span><span class="sxs-lookup"><span data-stu-id="aafc8-218">Install DevKit board package</span></span>

<span data-ttu-id="aafc8-219">Вам потребуется tooadd hello набор разработки доски с помощью hello Manager доски в коде Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="aafc8-219">You will need tooadd hello DevKit board using hello Board Manager in Visual Studio Code.</span></span>

1. <span data-ttu-id="aafc8-220">Используйте `Cmd+Shift+P` tooinvoke команд палитры и тип **Arduino** затем найдите и выберите **Arduino: диспетчер плата**.</span><span class="sxs-lookup"><span data-stu-id="aafc8-220">Use `Cmd+Shift+P` tooinvoke command palette and type **Arduino** then find and select **Arduino: Board Manager**.</span></span>

2. <span data-ttu-id="aafc8-221">Нажмите кнопку **«Дополнительные URL-адреса»** внизу hello справа.</span><span class="sxs-lookup"><span data-stu-id="aafc8-221">Click **'Additional URLs'** at hello bottom right.</span></span>
   <span data-ttu-id="aafc8-222">![Установка: дополнительные URL-адреса](media/iot-hub-arduino-devkit-az3166-get-started/installation-additional-urls-mac.png)</span><span class="sxs-lookup"><span data-stu-id="aafc8-222">![installation-additional-urls](media/iot-hub-arduino-devkit-az3166-get-started/installation-additional-urls-mac.png)</span></span>

3. <span data-ttu-id="aafc8-223">В hello `settings.json` файл, добавьте строку внизу hello `USER SETTINGS` области и сохранить.</span><span class="sxs-lookup"><span data-stu-id="aafc8-223">In hello `settings.json` file, add a line at hello bottom of `USER SETTINGS` pane and save.</span></span>
   ```json
   "arduino.additionalUrls": "https://raw.githubusercontent.com/VSChina/azureiotdevkit_tools/master/package_azureboard_index.json"
   ```
   ![Установка: JSON-файл параметров](media/iot-hub-arduino-devkit-az3166-get-started/installation-settings-json-mac.png)

4. <span data-ttu-id="aafc8-225">Теперь hello плата Manager для поиска «az3166» и установите последнюю версию hello.</span><span class="sxs-lookup"><span data-stu-id="aafc8-225">Now in hello Board Manager search for 'az3166' and install hello latest version.</span></span>
   <span data-ttu-id="aafc8-226">![Установка: az3166](media/iot-hub-arduino-devkit-az3166-get-started/installation-az3166-mac.png)</span><span class="sxs-lookup"><span data-stu-id="aafc8-226">![installation-az3166](media/iot-hub-arduino-devkit-az3166-get-started/installation-az3166-mac.png)</span></span>

<span data-ttu-id="aafc8-227">Теперь у вас есть все необходимые средства hello и пакеты, установленные для macOS.</span><span class="sxs-lookup"><span data-stu-id="aafc8-227">You now have all hello necessary tools and packages installed for macOS.</span></span>


## <a name="open-project-folder"></a><span data-ttu-id="aafc8-228">Открытие папки проекта</span><span class="sxs-lookup"><span data-stu-id="aafc8-228">Open project folder</span></span>

### <a name="launch-vs-code"></a><span data-ttu-id="aafc8-229">Запустите VSCode.</span><span class="sxs-lookup"><span data-stu-id="aafc8-229">Launch VS Code</span></span>

<span data-ttu-id="aafc8-230">Убедитесь, что плата DevKit не подключена.</span><span class="sxs-lookup"><span data-stu-id="aafc8-230">Make sure your DevKit is not connected.</span></span> <span data-ttu-id="aafc8-231">Сначала запустите VS Code и подключите компьютер tooyour набор разработки hello.</span><span class="sxs-lookup"><span data-stu-id="aafc8-231">Launch VS Code first and connect hello DevKit tooyour computer.</span></span> <span data-ttu-id="aafc8-232">VS Code автоматически найдет ее, и отобразится вводная страница.</span><span class="sxs-lookup"><span data-stu-id="aafc8-232">VS Code will automatically find it and pop up an introduction page:</span></span>

![Минирешение: VS Code](media/iot-hub-arduino-devkit-az3166-get-started/mini-solution-vscode.png)

> [!NOTE] 
<span data-ttu-id="aafc8-234">В некоторых случаях при запуске VS Code появляется сообщение об ошибке. В нем сообщается, что не удается найти интегрированную среду разработки Arduino или связанный пакет ПО для платы.</span><span class="sxs-lookup"><span data-stu-id="aafc8-234">Occasionally, when you launch VS Code, you will be prompted with error that cannot find Arduino IDE or related board package.</span></span> <span data-ttu-id="aafc8-235">toosolve его закрыть VS Code еще раз запустите Arduino интегрированной среды разработки и VS Code должна правильно определить путь Arduino IDE.</span><span class="sxs-lookup"><span data-stu-id="aafc8-235">toosolve it, close VS Code, launch Arduino IDE once again and VS Code should locate Arduino IDE path correctly.</span></span>

### <a name="open-arduino-examples-folder"></a><span data-ttu-id="aafc8-236">Открытие папки с примерами Arduino</span><span class="sxs-lookup"><span data-stu-id="aafc8-236">Open Arduino Examples folder</span></span>

<span data-ttu-id="aafc8-237">Переключение слишком**«Примеры Arduino»** вкладки, переходы слишком`Examples for MXCHIP AZ3166 > AzureIoT` и выберите команду `GetStarted`.</span><span class="sxs-lookup"><span data-stu-id="aafc8-237">Switch too**'Arduino Examples'** tab, navigate too`Examples for MXCHIP AZ3166 > AzureIoT` and click on `GetStarted`.</span></span>

![Минирешение: примеры](media/iot-hub-arduino-devkit-az3166-get-started/mini-solution-examples.png)

<span data-ttu-id="aafc8-239">Если вы столкнулись tooclose hello области tooreload его, используйте `Ctrl+Shift+P` (macOS: `Cmd+Shift+P`) tooinvoke команд палитры и тип **Arduino** toofind и выберите **Arduino: примеры**.</span><span class="sxs-lookup"><span data-stu-id="aafc8-239">If you happen tooclose hello pane, tooreload it, use `Ctrl+Shift+P` (macOS: `Cmd+Shift+P`) tooinvoke command palette and type **Arduino** toofind and select **Arduino: Examples**.</span></span>

## <a name="provision-azure-services"></a><span data-ttu-id="aafc8-240">Подготовка служб Azure</span><span class="sxs-lookup"><span data-stu-id="aafc8-240">Provision Azure services</span></span>

<span data-ttu-id="aafc8-241">Запустите задачу в окне решения hello, `Ctrl+P` (macOS: `Cmd+P`), введя «задача подготовки облако»:</span><span class="sxs-lookup"><span data-stu-id="aafc8-241">In hello solution window, run your task through `Ctrl+P` (macOS: `Cmd+P`) by typing 'task cloud-provision':</span></span>

<span data-ttu-id="aafc8-242">В hello VS Code терминалов интерактивной командной строки поможет hello подготовки необходимых служб Azure:</span><span class="sxs-lookup"><span data-stu-id="aafc8-242">In hello VS Code terminal, an interactive command line will guide you through provisioning hello required Azure services:</span></span>

![Минирешение: подготовка облачных служб](media/iot-hub-arduino-devkit-az3166-get-started/mini-solution/connect-iothub/cloud-provision.png)

## <a name="build-and-upload-arduino-sketch"></a><span data-ttu-id="aafc8-244">Создание и передача эскиза Arduino</span><span class="sxs-lookup"><span data-stu-id="aafc8-244">Build and upload Arduino sketch</span></span>

### <a name="install-required-library"></a><span data-ttu-id="aafc8-245">Установка необходимой библиотеки</span><span class="sxs-lookup"><span data-stu-id="aafc8-245">Install required library</span></span>

1. <span data-ttu-id="aafc8-246">Нажмите клавишу `F1` или `Ctrl+Shift+P` (macOS: `Cmd+Shift+P`) tooinvoke команд палитры и тип **Arduino** затем найдите и выберите **Arduino: диспетчер библиотек**.</span><span class="sxs-lookup"><span data-stu-id="aafc8-246">Press `F1` or `Ctrl+Shift+P` (macOS: `Cmd+Shift+P`) tooinvoke command palette and type **Arduino** then find and select **Arduino: Library Manager**.</span></span>

2. <span data-ttu-id="aafc8-247">Найдите библиотеку `ArduinoJson` и щелкните **Install** (Установить).</span><span class="sxs-lookup"><span data-stu-id="aafc8-247">Search for `ArduinoJson` library and click **Install**</span></span>

### <a name="build-and-upload-hello-device-code"></a><span data-ttu-id="aafc8-248">Построение и загружать код устройства hello</span><span class="sxs-lookup"><span data-stu-id="aafc8-248">Build and upload hello device code</span></span>

<span data-ttu-id="aafc8-249">Используйте `Ctrl+P` (macOS: `Cmd+P`) toorun «задачи устройства загрузки».</span><span class="sxs-lookup"><span data-stu-id="aafc8-249">Use `Ctrl+P` (macOS: `Cmd+P`) toorun 'task device-upload'.</span></span> <span data-ttu-id="aafc8-250">Hello терминалов предложит вам tooenter режим конфигурации.</span><span class="sxs-lookup"><span data-stu-id="aafc8-250">hello terminal will prompt you tooenter configuration mode.</span></span> <span data-ttu-id="aafc8-251">toodo таким образом, удерживая нажатой кнопку A, а затем кнопки сброса hello принудительной отправки и выпуска.</span><span class="sxs-lookup"><span data-stu-id="aafc8-251">toodo so, hold down button A, then push and release hello reset button.</span></span> <span data-ttu-id="aafc8-252">Hello отобразится экран «Конфигурация».</span><span class="sxs-lookup"><span data-stu-id="aafc8-252">hello screen will display 'Configuration'.</span></span> <span data-ttu-id="aafc8-253">Это строка подключения tooset hello, извлекает из шага «задачи облака подготовку к работе».</span><span class="sxs-lookup"><span data-stu-id="aafc8-253">This is tooset hello connection string that retrieves from 'task cloud-provision' step.</span></span>

<span data-ttu-id="aafc8-254">Затем он будет запущен, проверка и отправка эскиз Arduino hello:</span><span class="sxs-lookup"><span data-stu-id="aafc8-254">Then it will start verifying and uploading hello Arduino sketch:</span></span>

![Минирешение: передача кода устройства](media/iot-hub-arduino-devkit-az3166-get-started/mini-solution/connect-iothub/device-upload.png)

<span data-ttu-id="aafc8-256">Hello набор разработки будет перезагрузить и начать выполнение кода hello.</span><span class="sxs-lookup"><span data-stu-id="aafc8-256">hello DevKit will reboot and start running hello code.</span></span>

## <a name="test-hello-project"></a><span data-ttu-id="aafc8-257">Hello тестовый проект</span><span class="sxs-lookup"><span data-stu-id="aafc8-257">Test hello project</span></span>

<span data-ttu-id="aafc8-258">В VS Code щелкните значок подключаемых power hello строку hello tooopen последовательного монитор состояния hello.</span><span class="sxs-lookup"><span data-stu-id="aafc8-258">In VS Code, click hello power plug icon on hello status bar tooopen hello Serial Monitor.</span></span>

<span data-ttu-id="aafc8-259">Пример приложения Hello выполняется успешно при появлении hello следующие результаты:</span><span class="sxs-lookup"><span data-stu-id="aafc8-259">hello sample application is running successfully when you see hello following results:</span></span>

* <span data-ttu-id="aafc8-260">Hello последовательного монитор отображает hello же сведения, что содержимое hello hello снимке экрана ниже.</span><span class="sxs-lookup"><span data-stu-id="aafc8-260">hello Serial Monitor displays hello same information as hello content in hello screenshot below.</span></span>
* <span data-ttu-id="aafc8-261">мигает Hello Светодиод на набор разработки MXChip IoT.</span><span class="sxs-lookup"><span data-stu-id="aafc8-261">hello LED on MXChip IoT DevKit is blinking.</span></span>

![Окончательный результат в VS Code](media/iot-hub-arduino-devkit-az3166-get-started/mini-solution/connect-iothub/result-serial-output.png)

## <a name="problems-and-feedback"></a><span data-ttu-id="aafc8-263">Проблемы и обратная связь</span><span class="sxs-lookup"><span data-stu-id="aafc8-263">Problems and feedback</span></span>

<span data-ttu-id="aafc8-264">Можно найти [часто задаваемые вопросы о](https://microsoft.github.io/azure-iot-developer-kit/docs/faq/) при возникновении проблем или достижения toous из каналов hello ниже.</span><span class="sxs-lookup"><span data-stu-id="aafc8-264">You can find [FAQs](https://microsoft.github.io/azure-iot-developer-kit/docs/faq/) if you encounter problems or reach out toous from hello channels below.</span></span>

## <a name="next-steps"></a><span data-ttu-id="aafc8-265">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="aafc8-265">Next steps</span></span>

<span data-ttu-id="aafc8-266">Вы успешно подключились набор разработки IoT MXChip tooyour центр IoT и отправленных hello захвачен центра IoT tooyour данных датчика.</span><span class="sxs-lookup"><span data-stu-id="aafc8-266">You have successfully connected an MXChip IoT DevKit tooyour IoT Hub, and sent hello captured sensor data tooyour IoT hub.</span></span>

<span data-ttu-id="aafc8-267">Приступая к работе toocontinue центр IoT и tooexplore других сценариев IoT просмотреть:</span><span class="sxs-lookup"><span data-stu-id="aafc8-267">toocontinue getting started with IoT Hub and tooexplore other IoT scenarios, see:</span></span>

- [<span data-ttu-id="aafc8-268">Управление обменом сообщениями между устройством и облаком с помощью обозревателя Центра Интернета вещей</span><span class="sxs-lookup"><span data-stu-id="aafc8-268">Manage cloud device messaging with iothub-explorer</span></span>](https://docs.microsoft.com/azure/iot-hub/iot-hub-explorer-cloud-device-messaging)
- [<span data-ttu-id="aafc8-269">Сохранять сообщения центр IoT tooAzure хранилища данных</span><span class="sxs-lookup"><span data-stu-id="aafc8-269">Save IoT Hub messages tooAzure data storage</span></span>](https://docs.microsoft.com//azure/iot-hub/iot-hub-store-data-in-azure-table-storage)
- [<span data-ttu-id="aafc8-270">Использовать данные в режиме реального времени датчика toovisualize Power BI из центра IoT Azure</span><span class="sxs-lookup"><span data-stu-id="aafc8-270">Use Power BI toovisualize real-time sensor data from Azure IoT Hub</span></span>](https://docs.microsoft.com//azure/iot-hub/iot-hub-live-data-visualization-in-power-bi)
- [<span data-ttu-id="aafc8-271">Использовать данные в режиме реального времени датчика toovisualize веб-приложения Azure из центр IoT Azure</span><span class="sxs-lookup"><span data-stu-id="aafc8-271">Use Azure Web Apps toovisualize real-time sensor data from Azure IoT Hub</span></span>](https://docs.microsoft.com//azure/iot-hub/iot-hub-live-data-visualization-in-web-apps)
- [<span data-ttu-id="aafc8-272">Прогноз погоды, используя данные датчика hello из вашего центра IoT в машинном обучении Azure</span><span class="sxs-lookup"><span data-stu-id="aafc8-272">Weather forecast using hello sensor data from your IoT hub in Azure Machine Learning</span></span>](https://docs.microsoft.com/azure/iot-hub/iot-hub-weather-forecast-machine-learning)
- [<span data-ttu-id="aafc8-273">Управление устройствами с помощью средства iothub-explorer</span><span class="sxs-lookup"><span data-stu-id="aafc8-273">Device management with iothub-explorer</span></span>](https://docs.microsoft.com/azure/iot-hub/iot-hub-device-management-iothub-explorer)
- <span data-ttu-id="aafc8-274">[Remote monitoring and notifications with Logic Apps](https://docs.microsoft.com/azure/iot-hub/iot-hub-monitoring-notifications-with-azure-logic-apps) (Удаленный мониторинг и уведомления Logic Apps)</span><span class="sxs-lookup"><span data-stu-id="aafc8-274">[Remote monitoring and notifications with Logic Apps](https://docs.microsoft.com/azure/iot-hub/iot-hub-monitoring-notifications-with-azure-logic-apps)</span></span>