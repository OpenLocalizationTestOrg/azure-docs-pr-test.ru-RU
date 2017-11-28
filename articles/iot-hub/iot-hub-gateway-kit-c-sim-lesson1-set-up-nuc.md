---
title: "Приступая к работе с имитацией устройства и шлюзом Azure IoT. Урок 1. Настройка NUC | Документация Майкрософт"
description: "Настройка Intel NUC в качестве шлюза Интернета вещей, который собирает данные из датчиков и передает их в Центр Интернета вещей Azure."
services: iot-hub
documentationcenter: 
author: shizn
manager: yjianfeng
tags: 
keywords: "шлюз Интернета вещей, intel nuc, компьютер nuc, DE3815TYKE"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: f41d6b2e-9b00-40df-90eb-17d824bea883
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: b87974be9570f7d03fe84ae0a1d1fa7e346ff189
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="set-up-intel-nuc-as-an-iot-gateway"></a><span data-ttu-id="5551e-104">Настройка Intel NUC в качестве шлюза Интернета вещей</span><span class="sxs-lookup"><span data-stu-id="5551e-104">Set up Intel NUC as an IoT gateway</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="5551e-105">Выполняемая задача</span><span class="sxs-lookup"><span data-stu-id="5551e-105">What you will do</span></span>

- <span data-ttu-id="5551e-106">Настройте Intel NUC в качестве шлюза Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="5551e-106">Set up Intel NUC as an IoT gateway.</span></span>
- <span data-ttu-id="5551e-107">Установите пакет Edge Интернета вещей Azure на Intel NUC.</span><span class="sxs-lookup"><span data-stu-id="5551e-107">Install the Azure IoT Edge package on Intel NUC.</span></span>
- <span data-ttu-id="5551e-108">Запустите пример приложения hello_world на Intel NUC для проверки работоспособности шлюза.</span><span class="sxs-lookup"><span data-stu-id="5551e-108">Run a "hello_world" sample application on Intel NUC to verify the gateway functionality.</span></span>
<span data-ttu-id="5551e-109">Если возникнут какие-либо проблемы, то решения можно найти на [странице со сведениями об устранении неполадок](iot-hub-gateway-kit-c-sim-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="5551e-109">If you have any problems, look for solutions on the [troubleshooting page](iot-hub-gateway-kit-c-sim-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="5551e-110">Новые знания</span><span class="sxs-lookup"><span data-stu-id="5551e-110">What you will learn</span></span>

<span data-ttu-id="5551e-111">Из этого урока вы узнаете:</span><span class="sxs-lookup"><span data-stu-id="5551e-111">In this lesson, you will learn:</span></span>

- <span data-ttu-id="5551e-112">как подключить периферийные устройства к Intel NUC;</span><span class="sxs-lookup"><span data-stu-id="5551e-112">How to connect Intel NUC with peripherals.</span></span>
- <span data-ttu-id="5551e-113">как установить и обновить требуемые пакеты на Intel NUC с помощью Smart Package Manager;</span><span class="sxs-lookup"><span data-stu-id="5551e-113">How to install and update the required packages on Intel NUC using the Smart Package Manager.</span></span>
- <span data-ttu-id="5551e-114">как запустить пример приложения hello_world на Intel NUC для проверки работоспособности шлюза.</span><span class="sxs-lookup"><span data-stu-id="5551e-114">How to run the "hello_world" sample application to verify the gateway functionality.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="5551e-115">Необходимые элементы</span><span class="sxs-lookup"><span data-stu-id="5551e-115">What you need</span></span>

- <span data-ttu-id="5551e-116">Предварительно установленный пакет DE3815TYKE для Intel NUC с набором программного обеспечения Intel для шлюза Интернета вещей (Wind River Linux *7.0.0.13).</span><span class="sxs-lookup"><span data-stu-id="5551e-116">An Intel NUC Kit DE3815TYKE with the Intel IoT Gateway Software Suite (Wind River Linux *7.0.0.13) preinstalled.</span></span>
- <span data-ttu-id="5551e-117">Кабель Ethernet.</span><span class="sxs-lookup"><span data-stu-id="5551e-117">An Ethernet cable.</span></span>
- <span data-ttu-id="5551e-118">Клавиатура.</span><span class="sxs-lookup"><span data-stu-id="5551e-118">A keyboard.</span></span>
- <span data-ttu-id="5551e-119">Кабель HDMI или VGA.</span><span class="sxs-lookup"><span data-stu-id="5551e-119">An HDMI or VGA cable.</span></span>
- <span data-ttu-id="5551e-120">Монитор с портом HDMI или VGA.</span><span class="sxs-lookup"><span data-stu-id="5551e-120">A monitor with an HDMI or VGA port.</span></span>

![Комплект для шлюза](media/iot-hub-gateway-kit-lessons/lesson1/kit_without_sensortag.png)

## <a name="connect-intel-nuc-with-the-peripherals"></a><span data-ttu-id="5551e-122">Подключение периферийных устройств к Intel NUC</span><span class="sxs-lookup"><span data-stu-id="5551e-122">Connect Intel NUC with the peripherals</span></span>

<span data-ttu-id="5551e-123">На следующем рисунке показана конфигурация Intel NUC с подключением к разным периферийным устройствам.</span><span class="sxs-lookup"><span data-stu-id="5551e-123">The image below is an example of Intel NUC that is connected with various peripherals:</span></span>

1. <span data-ttu-id="5551e-124">Подключение к клавиатуре.</span><span class="sxs-lookup"><span data-stu-id="5551e-124">Connected to a keyboard.</span></span>
2. <span data-ttu-id="5551e-125">Подключение к монитору через кабель VGA или HDMI.</span><span class="sxs-lookup"><span data-stu-id="5551e-125">Connected to the monitor by a VGA cable or HDMI cable.</span></span>
3. <span data-ttu-id="5551e-126">Подключение к проводной сети с помощью кабеля Ethernet.</span><span class="sxs-lookup"><span data-stu-id="5551e-126">Connected to a wired network by an Ethernet cable.</span></span>
4. <span data-ttu-id="5551e-127">Подключение питания с помощью кабеля питания.</span><span class="sxs-lookup"><span data-stu-id="5551e-127">Connected to the power supply with a power cable.</span></span>

![Intel NUC с подключением к периферийным устройствам](media/iot-hub-gateway-kit-lessons/lesson1/nuc.png)

## <a name="connect-to-the-intel-nuc-system-from-host-computer-via-secure-shell-ssh"></a><span data-ttu-id="5551e-129">Подключение к системе Intel NUC с главного компьютера через Secure Shell (SSH)</span><span class="sxs-lookup"><span data-stu-id="5551e-129">Connect to the Intel NUC system from host computer via Secure Shell (SSH)</span></span>

<span data-ttu-id="5551e-130">На этом этапе вам потребуются клавиатура и монитор, чтобы узнать IP-адрес устройства NUC.</span><span class="sxs-lookup"><span data-stu-id="5551e-130">Here you need keyboard and monitor to get the IP address of your NUC device.</span></span> <span data-ttu-id="5551e-131">Если вы уже знаете IP-адрес, можете сразу перейти к шагу 3 в этом разделе.</span><span class="sxs-lookup"><span data-stu-id="5551e-131">If you already know the IP address, you can skip to step 3 in this section.</span></span>

1. <span data-ttu-id="5551e-132">Включите Intel NUC, нажав кнопку питания, и войдите в систему.</span><span class="sxs-lookup"><span data-stu-id="5551e-132">Turn on Intel NUC by pressing the Power button and log in the system.</span></span>

   <span data-ttu-id="5551e-133">По умолчанию имя пользователя и пароль имеют одинаковые значения: `root`.</span><span class="sxs-lookup"><span data-stu-id="5551e-133">The default user name and password are both `root`.</span></span>

2. <span data-ttu-id="5551e-134">Получите IP-адрес устройства NUC, выполнив команду `ifconfig`.</span><span class="sxs-lookup"><span data-stu-id="5551e-134">Get the IP address of NUC by running the `ifconfig` command.</span></span> <span data-ttu-id="5551e-135">Этот шаг выполняется на устройстве NUC.</span><span class="sxs-lookup"><span data-stu-id="5551e-135">This step is done on the NUC device.</span></span>

   <span data-ttu-id="5551e-136">Вот пример результата выполнения такой команды:</span><span class="sxs-lookup"><span data-stu-id="5551e-136">Here is an example of the command output.</span></span>

   ![Выходные данные ifconfig с IP-адресом NUC](media/iot-hub-gateway-kit-lessons/lesson1/ifconfig.png)

   <span data-ttu-id="5551e-138">В этом примере значение IP-адреса указано после символов `inet addr:`. Этот адрес понадобится вам для удаленного подключения к Intel NUC с главного компьютера.</span><span class="sxs-lookup"><span data-stu-id="5551e-138">In this example, the value that follows `inet addr:` is the IP address that you need when you plan to connect remotely from a host computer to Intel NUC.</span></span>

3. <span data-ttu-id="5551e-139">Используйте один из следующих SSH-клиентов для подключения к Intel NUC с главного компьютера.</span><span class="sxs-lookup"><span data-stu-id="5551e-139">Use one of the following SSH clients from your host machine to connect to Intel NUC.</span></span>

   - <span data-ttu-id="5551e-140">[PuTTY](http://www.putty.org/) для Windows.</span><span class="sxs-lookup"><span data-stu-id="5551e-140">[PuTTY](http://www.putty.org/) for Windows.</span></span>
   - <span data-ttu-id="5551e-141">Встроенный SSH-клиент ОС Ubuntu или macOS.</span><span class="sxs-lookup"><span data-stu-id="5551e-141">The build-in SSH client on Ubuntu or macOS.</span></span>

   <span data-ttu-id="5551e-142">Работа с Intel NUC выполняется более эффективно, если подключиться к нему через SSH-клиент с главного компьютера.</span><span class="sxs-lookup"><span data-stu-id="5551e-142">It is more efficient and productive to operate on Intel NUC from a host computer.</span></span> <span data-ttu-id="5551e-143">Для этого вам нужны IP-адрес, имя пользователя и пароль.</span><span class="sxs-lookup"><span data-stu-id="5551e-143">You need the the IP address, user name and password to connect the NUC via SSH client.</span></span> <span data-ttu-id="5551e-144">Вот пример использования SSH-клиента на macOS.</span><span class="sxs-lookup"><span data-stu-id="5551e-144">Here is the example use SSH client on macOS.</span></span>
   <span data-ttu-id="5551e-145">![SSH-клиент, запущенный на macOS](media/iot-hub-gateway-kit-lessons/lesson1/ssh.png)</span><span class="sxs-lookup"><span data-stu-id="5551e-145">![SSH client running on macOS](media/iot-hub-gateway-kit-lessons/lesson1/ssh.png)</span></span>

## <a name="install-the-azure-iot-edge-package"></a><span data-ttu-id="5551e-146">Установка пакета Edge Интернета вещей Azure</span><span class="sxs-lookup"><span data-stu-id="5551e-146">Install the Azure IoT Edge package</span></span>

<span data-ttu-id="5551e-147">Пакет Edge Интернета вещей Azure содержит предварительно скомпилированные двоичные файлы самого пакета SDK и его зависимостей.</span><span class="sxs-lookup"><span data-stu-id="5551e-147">The Azure IoT Edge package contains the pre-compiled binaries of the SDK and its dependencies.</span></span> <span data-ttu-id="5551e-148">В список этих файлов входят Edge Интернета вещей Azure, пакет SDK для Интернета вещей Azure и соответствующие средства.</span><span class="sxs-lookup"><span data-stu-id="5551e-148">These binaries are Azure IoT Edge, the Azure IoT SDK and the corresponding tools.</span></span> <span data-ttu-id="5551e-149">Пакет также содержит пример приложения hello_world, который используется для проверки работоспособности шлюза.</span><span class="sxs-lookup"><span data-stu-id="5551e-149">The package also contains a "hello_world" sample application that is used to validate the gateway functionality.</span></span> <span data-ttu-id="5551e-150">Edge Интернета вещей является основой шлюза.</span><span class="sxs-lookup"><span data-stu-id="5551e-150">IoT Edge is the core part of the gateway.</span></span> <span data-ttu-id="5551e-151">Для установки пакета выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="5551e-151">To install the package, follow these steps:</span></span>

1. <span data-ttu-id="5551e-152">Добавьте репозиторий облака Интернета вещей, выполнив в окне терминала следующие команды:</span><span class="sxs-lookup"><span data-stu-id="5551e-152">Add the IoT cloud repository by running the following commands in a terminal window:</span></span>

   ```bash
   rpm --import http://iotdk.intel.com/misc/iot_pub.key
   smart channel --add IoT_Cloud type=rpm-md name="IoT_Cloud" baseurl=http://iotdk.intel.com/repos/iot-cloud/wrlinux7/rcpl13/ -y
   ```

   <span data-ttu-id="5551e-153">Команда `rpm` импортирует ключ RPM.</span><span class="sxs-lookup"><span data-stu-id="5551e-153">The `rpm` command imports the rpm key.</span></span> <span data-ttu-id="5551e-154">Команда `smart channel` добавляет канал RPM в Smart Package Manager.</span><span class="sxs-lookup"><span data-stu-id="5551e-154">The `smart channel` command adds the rpm channel to the Smart Package Manager.</span></span> <span data-ttu-id="5551e-155">Перед запуском команды `smart update` вы должны увидеть примерно такие результаты, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="5551e-155">Before you run the `smart update` command, you see an output like below.</span></span>

   ![результаты выполнения команд rpm и smart channel](media/iot-hub-gateway-kit-lessons/lesson1/rpm_smart_channel.png)

   ```bash
   smart update
   ```

2. <span data-ttu-id="5551e-157">Установите пакет, выполнив следующую команду:</span><span class="sxs-lookup"><span data-stu-id="5551e-157">Install the package by running the following command:</span></span>

   ```bash
   smart install packagegroup-cloud-azure -y
   ```

   <span data-ttu-id="5551e-158">Здесь `packagegroup-cloud-azure` — это имя пакета.</span><span class="sxs-lookup"><span data-stu-id="5551e-158">`packagegroup-cloud-azure` is the name of the package.</span></span> <span data-ttu-id="5551e-159">Команда `smart install` используется для установки пакета.</span><span class="sxs-lookup"><span data-stu-id="5551e-159">The `smart install` command is used to install the package.</span></span>

   <span data-ttu-id="5551e-160">Когда установка пакета завершится, Intel NUC должен выполнять функции шлюза.</span><span class="sxs-lookup"><span data-stu-id="5551e-160">After the package is installed, Intel NUC is expected to work as a gateway.</span></span>

## <a name="run-the-azure-iot-edge-helloworld-sample-application"></a><span data-ttu-id="5551e-161">Запуск примера приложения hello_world из Edge Интернета вещей Azure</span><span class="sxs-lookup"><span data-stu-id="5551e-161">Run the Azure IoT Edge "hello_world" sample application</span></span>

<span data-ttu-id="5551e-162">Перейдите в каталог `azureiotgatewaysdk/samples` и запустите пример приложения hello_world.</span><span class="sxs-lookup"><span data-stu-id="5551e-162">Go to `azureiotgatewaysdk/samples` and run the sample "hello_world" sample application.</span></span> <span data-ttu-id="5551e-163">Этот пример приложения создает шлюз из файла `hello_world.json` и использует базовые компоненты архитектуры Edge Интернета вещей Azure, чтобы каждые 5 секунд записывать в журнал сообщение Hello World.</span><span class="sxs-lookup"><span data-stu-id="5551e-163">This sample application creates a gateway from the `hello_world.json` file and uses the fundamental components of the Azure IoT Edge architecture to log a hello world message to a file every 5 seconds.</span></span>

<span data-ttu-id="5551e-164">Чтобы запустить пример приложения hello_world, выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="5551e-164">You can run the sample "hello_world" sample application by running the following command:</span></span>

```bash
cd /usr/share/azureiotgatewaysdk/samples/hello_world/
./hello_world hello_world.json
```

<span data-ttu-id="5551e-165">При правильной работе шлюза этот пример приложения должен возвращать следующие данные:</span><span class="sxs-lookup"><span data-stu-id="5551e-165">The sample application produces the following output if the gateway functionality is working correctly:</span></span>

![выходные данные приложения](media/iot-hub-gateway-kit-lessons/lesson1/hello_world.png)

<span data-ttu-id="5551e-167">Если возникнут какие-либо проблемы, то решения можно найти на [странице со сведениями об устранении неполадок](iot-hub-gateway-kit-c-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="5551e-167">If you have any problems, look for solutions on the [troubleshooting page](iot-hub-gateway-kit-c-troubleshooting.md).</span></span>

## <a name="summary"></a><span data-ttu-id="5551e-168">Сводка</span><span class="sxs-lookup"><span data-stu-id="5551e-168">Summary</span></span>

<span data-ttu-id="5551e-169">Поздравляем!</span><span class="sxs-lookup"><span data-stu-id="5551e-169">Congratulations!</span></span> <span data-ttu-id="5551e-170">Итак, вы завершили настройку Intel NUC в качестве шлюза.</span><span class="sxs-lookup"><span data-stu-id="5551e-170">You've finished setting up Intel NUC as a gateway.</span></span> <span data-ttu-id="5551e-171">Теперь можно переходить к следующему уроку, в котором вы настроите главный компьютер, настроите Центр Интернета вещей Azure и зарегистрируете логическое устройство Центра Интернета вещей Azure.</span><span class="sxs-lookup"><span data-stu-id="5551e-171">Now you're ready to move on to the next lesson to set up your host computer, create an Azure IoT hub and register your Azure IoT hub logical device.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5551e-172">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="5551e-172">Next steps</span></span>
[<span data-ttu-id="5551e-173">Подготовка главного компьютера и Центра Интернета вещей Azure</span><span class="sxs-lookup"><span data-stu-id="5551e-173">Get your host computer and Azure IoT hub ready</span></span>](iot-hub-gateway-kit-c-sim-lesson2-get-the-tools-win32.md)
