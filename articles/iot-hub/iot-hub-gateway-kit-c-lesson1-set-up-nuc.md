---
title: "Приступая к работе с устройством SensorTag и шлюзом Интернета вещей Azure. Урок 1. Настройка Intel NUC | Документация Майкрософт"
description: "Настройка Intel NUC в качестве шлюза Интернета вещей, который собирает данные из датчиков и передает их в Центр Интернета вещей Azure."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "шлюз Интернета вещей, intel nuc, компьютер nuc, DE3815TYKE"
ms.assetid: 917090d6-35c2-495b-a620-ca6f9c02b317
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 1a3a92ab8d08c6ed6f047208217c46022027157e
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="set-up-intel-nuc-as-an-iot-gateway"></a><span data-ttu-id="2d76b-104">Настройка Intel NUC в качестве шлюза Интернета вещей</span><span class="sxs-lookup"><span data-stu-id="2d76b-104">Set up Intel NUC as an IoT gateway</span></span>
[!INCLUDE [iot-hub-get-started-device-selector](../../includes/iot-hub-get-started-device-selector.md)]

## <a name="what-you-will-do"></a><span data-ttu-id="2d76b-105">Выполняемая задача</span><span class="sxs-lookup"><span data-stu-id="2d76b-105">What you will do</span></span>

- <span data-ttu-id="2d76b-106">Настройте Intel NUC в качестве шлюза Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="2d76b-106">Set up Intel NUC as an IoT gateway.</span></span>
- <span data-ttu-id="2d76b-107">Установите пакет Edge Интернета вещей Azure на Intel NUC.</span><span class="sxs-lookup"><span data-stu-id="2d76b-107">Install the Azure IoT Edge package on the Intel NUC.</span></span>
- <span data-ttu-id="2d76b-108">Запустите пример приложения hello_world на Intel NUC для проверки работоспособности шлюза.</span><span class="sxs-lookup"><span data-stu-id="2d76b-108">Run a "hello_world" sample application on the Intel NUC to verify the gateway functionality.</span></span>

  > <span data-ttu-id="2d76b-109">Если возникнут какие-либо проблемы, то решения можно найти на [странице со сведениями об устранении неполадок](iot-hub-gateway-kit-c-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="2d76b-109">If you have any problems, look for solutions on the [troubleshooting page](iot-hub-gateway-kit-c-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="2d76b-110">Новые знания</span><span class="sxs-lookup"><span data-stu-id="2d76b-110">What you will learn</span></span>

<span data-ttu-id="2d76b-111">Из этого урока вы узнаете:</span><span class="sxs-lookup"><span data-stu-id="2d76b-111">In this lesson, you will learn:</span></span>

- <span data-ttu-id="2d76b-112">как подключить периферийные устройства к Intel NUC;</span><span class="sxs-lookup"><span data-stu-id="2d76b-112">How to connect Intel NUC with peripherals.</span></span>
- <span data-ttu-id="2d76b-113">как установить и обновить требуемые пакеты на Intel NUC с помощью Smart Package Manager;</span><span class="sxs-lookup"><span data-stu-id="2d76b-113">How to install and update the required packages on Intel NUC using the Smart Package Manager.</span></span>
- <span data-ttu-id="2d76b-114">как запустить пример приложения hello_world на Intel NUC для проверки работоспособности шлюза.</span><span class="sxs-lookup"><span data-stu-id="2d76b-114">How to run the "hello_world" sample application to verify the gateway functionality.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="2d76b-115">Необходимые элементы</span><span class="sxs-lookup"><span data-stu-id="2d76b-115">What you need</span></span>

- <span data-ttu-id="2d76b-116">Предварительно установленный пакет DE3815TYKE для Intel NUC с набором программного обеспечения Intel для шлюза Интернета вещей (Wind River Linux *7.0.0.13).</span><span class="sxs-lookup"><span data-stu-id="2d76b-116">An Intel NUC Kit DE3815TYKE with the Intel IoT Gateway Software Suite (Wind River Linux *7.0.0.13) preinstalled.</span></span> <span data-ttu-id="2d76b-117">[Щелкните здесь, чтобы приобрести набор для создания коммерческого шлюза Интернета вещей Grove](https://www.seeedstudio.com/Grove-IoT-Commercial-Gateway-Kit-p-2724.html).</span><span class="sxs-lookup"><span data-stu-id="2d76b-117">[Click here to purchase Grove IoT Commercial Gateway Kit](https://www.seeedstudio.com/Grove-IoT-Commercial-Gateway-Kit-p-2724.html).</span></span>
- <span data-ttu-id="2d76b-118">Кабель Ethernet.</span><span class="sxs-lookup"><span data-stu-id="2d76b-118">An Ethernet cable.</span></span>
- <span data-ttu-id="2d76b-119">Клавиатура.</span><span class="sxs-lookup"><span data-stu-id="2d76b-119">A keyboard.</span></span>
- <span data-ttu-id="2d76b-120">Кабель HDMI или VGA.</span><span class="sxs-lookup"><span data-stu-id="2d76b-120">An HDMI or VGA cable.</span></span>
- <span data-ttu-id="2d76b-121">Монитор с портом HDMI или VGA.</span><span class="sxs-lookup"><span data-stu-id="2d76b-121">A monitor with an HDMI or VGA port.</span></span>
- <span data-ttu-id="2d76b-122">Необязательно: [Texas Instruments Sensor Tag (CC2650STK)](http://www.ti.com/tool/cc2650stk)</span><span class="sxs-lookup"><span data-stu-id="2d76b-122">Optional: [Texas Instruments Sensor Tag (CC2650STK)](http://www.ti.com/tool/cc2650stk)</span></span>

![Комплект для шлюза](media/iot-hub-gateway-kit-lessons/lesson1/kit.png)

## <a name="connect-intel-nuc-with-the-peripherals"></a><span data-ttu-id="2d76b-124">Подключение периферийных устройств к Intel NUC</span><span class="sxs-lookup"><span data-stu-id="2d76b-124">Connect Intel NUC with the peripherals</span></span>

<span data-ttu-id="2d76b-125">На следующем рисунке показана конфигурация Intel NUC с подключением к разным периферийным устройствам.</span><span class="sxs-lookup"><span data-stu-id="2d76b-125">The image below is an example of Intel NUC that is connected with various peripherals:</span></span>

1. <span data-ttu-id="2d76b-126">Подключение к клавиатуре.</span><span class="sxs-lookup"><span data-stu-id="2d76b-126">Connected to a keyboard.</span></span>
2. <span data-ttu-id="2d76b-127">Подключение к монитору через кабель VGA или HDMI.</span><span class="sxs-lookup"><span data-stu-id="2d76b-127">Connected to a monitor with a VGA cable or HDMI cable.</span></span>
3. <span data-ttu-id="2d76b-128">Подключение к проводной сети с помощью кабеля Ethernet.</span><span class="sxs-lookup"><span data-stu-id="2d76b-128">Connected to a wired network with an Ethernet cable.</span></span>
4. <span data-ttu-id="2d76b-129">Подключение питания с помощью кабеля питания.</span><span class="sxs-lookup"><span data-stu-id="2d76b-129">Connected to a power supply with a power cable.</span></span>

![Intel NUC с подключением к периферийным устройствам](media/iot-hub-gateway-kit-lessons/lesson1/nuc.png)

## <a name="connect-to-the-intel-nuc-system-from-host-computer-via-secure-shell-ssh"></a><span data-ttu-id="2d76b-131">Подключение к системе Intel NUC с главного компьютера через Secure Shell (SSH)</span><span class="sxs-lookup"><span data-stu-id="2d76b-131">Connect to the Intel NUC system from host computer via Secure Shell (SSH)</span></span>

<span data-ttu-id="2d76b-132">Вам потребуются клавиатура и монитор, чтобы узнать IP-адрес устройства Intel NUC.</span><span class="sxs-lookup"><span data-stu-id="2d76b-132">You will need a keyboard and a monitor to get the IP address of your Intel NUC device.</span></span> <span data-ttu-id="2d76b-133">Если вы уже знаете IP-адрес, можете сразу перейти к шагу 3 в этом разделе.</span><span class="sxs-lookup"><span data-stu-id="2d76b-133">If you already know the IP address, you can skip ahead to step 3 in this section.</span></span>

1. <span data-ttu-id="2d76b-134">Включите Intel NUC, нажав кнопку питания, и войдите в систему.</span><span class="sxs-lookup"><span data-stu-id="2d76b-134">Turn on the Intel NUC by pressing the power button and then log in.</span></span>

   <span data-ttu-id="2d76b-135">По умолчанию имя пользователя и пароль имеют одинаковые значения: `root`.</span><span class="sxs-lookup"><span data-stu-id="2d76b-135">The default user name and password are both `root`.</span></span>

       > Hit the enter key on your keyboard if you see either of the following errors when you boot: 'A TPM error (7) occurred attempting to read a pcr value.' or 'Timeout, No TPM chip found, activating TPM-bypass!'

2. <span data-ttu-id="2d76b-136">Получите IP-адрес Intel NUC, выполнив команду `ifconfig` на устройстве Intel NUC.</span><span class="sxs-lookup"><span data-stu-id="2d76b-136">Get the IP address of the Intel NUC by running the `ifconfig` command on the Intel NUC device.</span></span>

   <span data-ttu-id="2d76b-137">Вот пример результата выполнения такой команды:</span><span class="sxs-lookup"><span data-stu-id="2d76b-137">Here is an example of the command output.</span></span>

   ![Выходные данные ifconfig с IP-адресом Intel NUC](media/iot-hub-gateway-kit-lessons/lesson1/ifconfig.png)

   <span data-ttu-id="2d76b-139">В этом примере значение IP-адреса указано после символов `inet addr:`. Этот адрес понадобится вам для удаленного подключения к Intel NUC с главного компьютера.</span><span class="sxs-lookup"><span data-stu-id="2d76b-139">In this example, the value that follows `inet addr:` is the IP address that you need when connect to the Intel NUC from a host computer.</span></span>

3. <span data-ttu-id="2d76b-140">Используйте один из следующих SSH-клиентов для подключения к Intel NUC с главного компьютера.</span><span class="sxs-lookup"><span data-stu-id="2d76b-140">Use one of the following SSH clients from your host computer to connect to Intel NUC.</span></span>

    - <span data-ttu-id="2d76b-141">[PuTTY](http://www.putty.org/) для Windows.</span><span class="sxs-lookup"><span data-stu-id="2d76b-141">[PuTTY](http://www.putty.org/) for Windows.</span></span>
    - <span data-ttu-id="2d76b-142">Встроенный SSH-клиент ОС Ubuntu или macOS.</span><span class="sxs-lookup"><span data-stu-id="2d76b-142">The built-in SSH client on Ubuntu or macOS.</span></span>

   <span data-ttu-id="2d76b-143">Работа с Intel NUC будет более эффективной, если подключиться к нему через SSH-клиент с главного компьютера.</span><span class="sxs-lookup"><span data-stu-id="2d76b-143">It is more efficient and productive to operate an Intel NUC from a host computer.</span></span> <span data-ttu-id="2d76b-144">Для этого вам нужны IP-адрес Intel NUC, имя пользователя и пароль.</span><span class="sxs-lookup"><span data-stu-id="2d76b-144">You'll need the Intel NUC's IP address, user name and password to connect to it via an SSH client.</span></span> <span data-ttu-id="2d76b-145">Ниже приведен пример использования SSH-клиента в macOS.</span><span class="sxs-lookup"><span data-stu-id="2d76b-145">Here is an example that uses an SSH client on macOS.</span></span>
   <span data-ttu-id="2d76b-146">![SSH-клиент, запущенный на macOS](media/iot-hub-gateway-kit-lessons/lesson1/ssh.png)</span><span class="sxs-lookup"><span data-stu-id="2d76b-146">![SSH client running on macOS](media/iot-hub-gateway-kit-lessons/lesson1/ssh.png)</span></span>

## <a name="install-the-azure-iot-edge-package"></a><span data-ttu-id="2d76b-147">Установка пакета Edge Интернета вещей Azure</span><span class="sxs-lookup"><span data-stu-id="2d76b-147">Install the Azure IoT Edge package</span></span>

<span data-ttu-id="2d76b-148">Пакет Edge Интернета вещей Azure содержит предварительно скомпилированные двоичные файлы самого пакета Edge Интернета вещей и его зависимостей.</span><span class="sxs-lookup"><span data-stu-id="2d76b-148">The Azure IoT Edge package contains the pre-compiled binaries of IoT Edge and its dependencies.</span></span> <span data-ttu-id="2d76b-149">В список этих файлов входят Edge Интернета вещей Azure, пакет SDK для Интернета вещей Azure и соответствующие средства.</span><span class="sxs-lookup"><span data-stu-id="2d76b-149">These binaries are Azure IoT Edge, the Azure IoT SDK and the corresponding tools.</span></span> <span data-ttu-id="2d76b-150">Пакет также содержит пример приложения hello_world, который используется для проверки работоспособности шлюза.</span><span class="sxs-lookup"><span data-stu-id="2d76b-150">The package also contains a "hello_world" sample application is used to validate the gateway functionality.</span></span> <span data-ttu-id="2d76b-151">Edge Интернета вещей является основой шлюза.</span><span class="sxs-lookup"><span data-stu-id="2d76b-151">IoT Edge is the core part of the gateway.</span></span> 

<span data-ttu-id="2d76b-152">Для установки пакета выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="2d76b-152">Follow these steps to install the package.</span></span>

1. <span data-ttu-id="2d76b-153">Добавьте репозиторий облака Интернета вещей, выполнив в окне терминала следующие команды:</span><span class="sxs-lookup"><span data-stu-id="2d76b-153">Add the IoT Cloud repository by running the following commands in a terminal window:</span></span>

   ```bash
   rpm --import https://iotdk.intel.com/misc/iot_pub2.key
   smart channel --add IoT_Cloud type=rpm-md name="IoT_Cloud" baseurl=http://iotdk.intel.com/repos/iot-cloud/wrlinux7/rcpl13/ -y
   smart channel --add WR_Repo type=rpm-md baseurl=https://distro.windriver.com/release/idp-3-xt/public_feeds/WR-IDP-3-XT-Intel-Baytrail-public-repo/RCPL13/corei7_64/
   ```

   > <span data-ttu-id="2d76b-154">Введите "y", получив запрос "Include this channel?" (Включить этот канал?).</span><span class="sxs-lookup"><span data-stu-id="2d76b-154">Enter 'y', when it prompts you to 'Include this channel?'</span></span>
   
   <span data-ttu-id="2d76b-155">Если произошла ошибка `import read failed(-1)`, можно решить эту проблему, выполнив следующие команды:</span><span class="sxs-lookup"><span data-stu-id="2d76b-155">If you receive an `import read failed(-1)` error, use the following commands to resolve the issue:</span></span>
   ```bash
   wget http://iotdk.intel.com/misc/iot_pub2.key 
   rpm --import iot_pub2.key  
   ```

   <span data-ttu-id="2d76b-156">Команда `rpm` импортирует ключ RPM.</span><span class="sxs-lookup"><span data-stu-id="2d76b-156">The `rpm` command imports the rpm key.</span></span> <span data-ttu-id="2d76b-157">Команда `smart channel` добавляет канал RPM в Smart Package Manager.</span><span class="sxs-lookup"><span data-stu-id="2d76b-157">The `smart channel` command adds the rpm channel to the Smart Package Manager.</span></span> <span data-ttu-id="2d76b-158">Перед запуском команды `smart update` вы должны увидеть примерно такие результаты, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="2d76b-158">Before you run the `smart update` command, you will see an output like below.</span></span>

   ![результаты выполнения команд rpm и smart channel](media/iot-hub-gateway-kit-lessons/lesson1/rpm_smart_channel.png)

2. <span data-ttu-id="2d76b-160">Выполните команду smart update:</span><span class="sxs-lookup"><span data-stu-id="2d76b-160">Execute the smart update command:</span></span>

   ```bash
   smart update
   ```

3. <span data-ttu-id="2d76b-161">Установите пакет для шлюза Интернета вещей Azure, выполнив следующую команду:</span><span class="sxs-lookup"><span data-stu-id="2d76b-161">Install the Azure IoT Gateway package by running the following command:</span></span>

   ```bash
   smart install packagegroup-cloud-azure -y
   ```

   <span data-ttu-id="2d76b-162">Здесь `packagegroup-cloud-azure` — это имя пакета.</span><span class="sxs-lookup"><span data-stu-id="2d76b-162">`packagegroup-cloud-azure` is the name of the package.</span></span> <span data-ttu-id="2d76b-163">Команда `smart install` используется для установки пакета.</span><span class="sxs-lookup"><span data-stu-id="2d76b-163">The `smart install` command is used to install the package.</span></span>

    > <span data-ttu-id="2d76b-164">Если вы увидите ошибку "Открытый ключ недоступен", выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="2d76b-164">Run the following command if you see this error: 'public key not available'</span></span>

    ```bash
    smart config --set rpm-check-signatures=false
    smart install packagegroup-cloud-azure -y
    ```
    > <span data-ttu-id="2d76b-165">Перезагрузите Intel NUC, если отображается сообщение об ошибке "no package provides util-linux-dev" (нет пакета, предоставляющего util-linux-dev)</span><span class="sxs-lookup"><span data-stu-id="2d76b-165">Reboot the Intel NUC if you see this error: 'no package provides util-linux-dev'</span></span>

   <span data-ttu-id="2d76b-166">Когда установка пакета завершится, Intel NUC будет готово выполнять функции шлюза.</span><span class="sxs-lookup"><span data-stu-id="2d76b-166">After the package is installed, Intel NUC is ready to function as a gateway.</span></span>

## <a name="run-the-azure-iot-edge-helloworld-sample-application"></a><span data-ttu-id="2d76b-167">Запуск примера приложения hello_world из Edge Интернета вещей Azure</span><span class="sxs-lookup"><span data-stu-id="2d76b-167">Run the Azure IoT Edge "hello_world" sample application</span></span>

<span data-ttu-id="2d76b-168">Этот пример приложения создает шлюз из файла `hello_world.json` и использует базовые компоненты архитектуры Edge Интернета вещей Azure, чтобы каждые 5 секунд записывать в журнал (log.txt) сообщение Hello World.</span><span class="sxs-lookup"><span data-stu-id="2d76b-168">The following sample application creates a gateway from a `hello_world.json` file and uses the fundamental components of Azure IoT Edge architecture to log a hello world message to a file (log.txt) every 5 seconds.</span></span>

<span data-ttu-id="2d76b-169">Чтобы запустить наш пример "Hello World", выполните следующие команды:</span><span class="sxs-lookup"><span data-stu-id="2d76b-169">You can run the Hello World sample by executing the following commands:</span></span>

```bash
cd /usr/share/azureiotgatewaysdk/samples/hello_world/
./hello_world hello_world.json
```

<span data-ttu-id="2d76b-170">Оставьте приложение "Hello World" работать в течение нескольких минут, а затем остановите его, нажав клавишу ВВОД.</span><span class="sxs-lookup"><span data-stu-id="2d76b-170">Let the Hello World application run for a few minutes and then hit the Enter key to stop it.</span></span>
<span data-ttu-id="2d76b-171">![выходные данные приложения](media/iot-hub-gateway-kit-lessons/lesson1/hello_world.png)</span><span class="sxs-lookup"><span data-stu-id="2d76b-171">![application output](media/iot-hub-gateway-kit-lessons/lesson1/hello_world.png)</span></span>

> <span data-ttu-id="2d76b-172">Вы можете игнорировать любые ошибки "Недопустимый дескриптор аргумента (NULL)", которые появляются после нажатия клавиши ВВОД.</span><span class="sxs-lookup"><span data-stu-id="2d76b-172">You can ignore any 'invalid argument handle(NULL)' errors that appear after you hit Enter.</span></span>

<span data-ttu-id="2d76b-173">Убедитесь, что шлюз успешно работал, открыв файл log.txt, который был создан в папке приложения hello_world. ![Представление каталога с файлом log.txt](media/iot-hub-gateway-kit-lessons/lesson1/logtxtdir.png)</span><span class="sxs-lookup"><span data-stu-id="2d76b-173">You can verify that the gateway ran successfully by opening the log.txt file that is now in your hello_world folder ![log.txt directory view](media/iot-hub-gateway-kit-lessons/lesson1/logtxtdir.png)</span></span>

<span data-ttu-id="2d76b-174">Откройте файл log.txt с помощью следующей команды:</span><span class="sxs-lookup"><span data-stu-id="2d76b-174">Open log.txt using the following command:</span></span>

```bash
vim log.txt
```

<span data-ttu-id="2d76b-175">Вы увидите содержимое log.txt, который содержит сообщения в формате JSON, создаваемые каждые 5 секунд нашим модулем шлюза "Hello World".</span><span class="sxs-lookup"><span data-stu-id="2d76b-175">You will then see the contents of log.txt, which will be a JSON formatted output of the logging messages that were written every 5 seconds by the gateway Hello World module.</span></span>
<span data-ttu-id="2d76b-176">![Представление каталога log.txt](media/iot-hub-gateway-kit-lessons/lesson1/logtxtview.png)</span><span class="sxs-lookup"><span data-stu-id="2d76b-176">![log.txt directory view](media/iot-hub-gateway-kit-lessons/lesson1/logtxtview.png)</span></span>

<span data-ttu-id="2d76b-177">Если возникнут какие-либо проблемы, то решения можно найти на [странице со сведениями об устранении неполадок](iot-hub-gateway-kit-c-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="2d76b-177">If you have any problems, look for solutions on the [troubleshooting page](iot-hub-gateway-kit-c-troubleshooting.md).</span></span>

## <a name="summary"></a><span data-ttu-id="2d76b-178">Сводка</span><span class="sxs-lookup"><span data-stu-id="2d76b-178">Summary</span></span>

<span data-ttu-id="2d76b-179">Поздравляем!</span><span class="sxs-lookup"><span data-stu-id="2d76b-179">Congratulations!</span></span> <span data-ttu-id="2d76b-180">Итак, вы завершили настройку Intel NUC в качестве шлюза.</span><span class="sxs-lookup"><span data-stu-id="2d76b-180">You've finished setting up Intel NUC as a gateway.</span></span> <span data-ttu-id="2d76b-181">Теперь можно переходить к следующему уроку, в котором вы настроите главный компьютер, настроите Центр Интернета вещей Azure и зарегистрируете логическое устройство Центра Интернета вещей Azure.</span><span class="sxs-lookup"><span data-stu-id="2d76b-181">Now you're ready to move on to the next lesson to set up your host computer, create an Azure IoT Hub and register your Azure IoT Hub logical device.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2d76b-182">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="2d76b-182">Next steps</span></span>
[<span data-ttu-id="2d76b-183">Использование шлюза Интернета вещей для подключения устройства к Центру Интернета вещей Azure</span><span class="sxs-lookup"><span data-stu-id="2d76b-183">Use an IoT gateway to connect a device to Azure IoT Hub</span></span>](iot-hub-gateway-kit-c-iot-gateway-connect-device-to-cloud.md)

