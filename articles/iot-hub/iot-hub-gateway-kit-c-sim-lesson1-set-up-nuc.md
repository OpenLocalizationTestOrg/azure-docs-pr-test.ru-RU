---
title: "Приступая к работе с имитацией устройства и шлюзом Azure IoT. Урок 1. Настройка NUC | Документация Майкрософт"
description: "Настройка toowork Intel NUC виде шлюза IoT между датчика и данных датчика toocollect центр IoT Azure и отправить его tooIoT концентратора."
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
ms.openlocfilehash: c2146c7cd8ca54adbd0af279364ec8484be1b45b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-intel-nuc-as-an-iot-gateway"></a><span data-ttu-id="947c5-104">Настройка Intel NUC в качестве шлюза Интернета вещей</span><span class="sxs-lookup"><span data-stu-id="947c5-104">Set up Intel NUC as an IoT gateway</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="947c5-105">Выполняемая задача</span><span class="sxs-lookup"><span data-stu-id="947c5-105">What you will do</span></span>

- <span data-ttu-id="947c5-106">Настройте Intel NUC в качестве шлюза Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="947c5-106">Set up Intel NUC as an IoT gateway.</span></span>
- <span data-ttu-id="947c5-107">Установите пакет Azure IoT Edge hello на Intel NUC.</span><span class="sxs-lookup"><span data-stu-id="947c5-107">Install hello Azure IoT Edge package on Intel NUC.</span></span>
- <span data-ttu-id="947c5-108">Запустите пример приложения «hello_world» на функциональность шлюза hello tooverify Intel NUC.</span><span class="sxs-lookup"><span data-stu-id="947c5-108">Run a "hello_world" sample application on Intel NUC tooverify hello gateway functionality.</span></span>
<span data-ttu-id="947c5-109">Если у вас возникнут проблемы, искать решения на hello [страницу устранения неполадок](iot-hub-gateway-kit-c-sim-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="947c5-109">If you have any problems, look for solutions on hello [troubleshooting page](iot-hub-gateway-kit-c-sim-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="947c5-110">Новые знания</span><span class="sxs-lookup"><span data-stu-id="947c5-110">What you will learn</span></span>

<span data-ttu-id="947c5-111">Из этого урока вы узнаете:</span><span class="sxs-lookup"><span data-stu-id="947c5-111">In this lesson, you will learn:</span></span>

- <span data-ttu-id="947c5-112">Как tooconnect Intel NUC с периферийные устройства.</span><span class="sxs-lookup"><span data-stu-id="947c5-112">How tooconnect Intel NUC with peripherals.</span></span>
- <span data-ttu-id="947c5-113">Как пакеты hello необходимые tooinstall и обновления на использование Intel NUC hello смарт-диспетчера пакетов.</span><span class="sxs-lookup"><span data-stu-id="947c5-113">How tooinstall and update hello required packages on Intel NUC using hello Smart Package Manager.</span></span>
- <span data-ttu-id="947c5-114">Как toorun hello» hello_world» образец функциональность шлюза hello tooverify приложения.</span><span class="sxs-lookup"><span data-stu-id="947c5-114">How toorun hello "hello_world" sample application tooverify hello gateway functionality.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="947c5-115">Необходимые элементы</span><span class="sxs-lookup"><span data-stu-id="947c5-115">What you need</span></span>

- <span data-ttu-id="947c5-116">DE3815TYKE комплект Intel NUC с hello шлюза программного обеспечения Intel IoT Suite (р. воздушного Linux * 7.0.0.13) предварительно.</span><span class="sxs-lookup"><span data-stu-id="947c5-116">An Intel NUC Kit DE3815TYKE with hello Intel IoT Gateway Software Suite (Wind River Linux *7.0.0.13) preinstalled.</span></span>
- <span data-ttu-id="947c5-117">Кабель Ethernet.</span><span class="sxs-lookup"><span data-stu-id="947c5-117">An Ethernet cable.</span></span>
- <span data-ttu-id="947c5-118">Клавиатура.</span><span class="sxs-lookup"><span data-stu-id="947c5-118">A keyboard.</span></span>
- <span data-ttu-id="947c5-119">Кабель HDMI или VGA.</span><span class="sxs-lookup"><span data-stu-id="947c5-119">An HDMI or VGA cable.</span></span>
- <span data-ttu-id="947c5-120">Монитор с портом HDMI или VGA.</span><span class="sxs-lookup"><span data-stu-id="947c5-120">A monitor with an HDMI or VGA port.</span></span>

![Комплект для шлюза](media/iot-hub-gateway-kit-lessons/lesson1/kit_without_sensortag.png)

## <a name="connect-intel-nuc-with-hello-peripherals"></a><span data-ttu-id="947c5-122">Подключения Intel NUC hello периферийных устройств</span><span class="sxs-lookup"><span data-stu-id="947c5-122">Connect Intel NUC with hello peripherals</span></span>

<span data-ttu-id="947c5-123">изображение Hello ниже приведен пример NUC Intel, который связан с различными периферийные устройства:</span><span class="sxs-lookup"><span data-stu-id="947c5-123">hello image below is an example of Intel NUC that is connected with various peripherals:</span></span>

1. <span data-ttu-id="947c5-124">Подключенный tooa клавиатуры.</span><span class="sxs-lookup"><span data-stu-id="947c5-124">Connected tooa keyboard.</span></span>
2. <span data-ttu-id="947c5-125">Подключен монитор toohello кабель VGA или HDMI кабель.</span><span class="sxs-lookup"><span data-stu-id="947c5-125">Connected toohello monitor by a VGA cable or HDMI cable.</span></span>
3. <span data-ttu-id="947c5-126">Подключенный tooa проводной сети с помощью кабеля Ethernet.</span><span class="sxs-lookup"><span data-stu-id="947c5-126">Connected tooa wired network by an Ethernet cable.</span></span>
4. <span data-ttu-id="947c5-127">Источник питания подключенных toohello кабеля питания.</span><span class="sxs-lookup"><span data-stu-id="947c5-127">Connected toohello power supply with a power cable.</span></span>

![Tooperipherals подключен NUC Intel](media/iot-hub-gateway-kit-lessons/lesson1/nuc.png)

## <a name="connect-toohello-intel-nuc-system-from-host-computer-via-secure-shell-ssh"></a><span data-ttu-id="947c5-129">Подключение системы Intel NUC toohello от главного компьютера через Secure Shell (SSH)</span><span class="sxs-lookup"><span data-stu-id="947c5-129">Connect toohello Intel NUC system from host computer via Secure Shell (SSH)</span></span>

<span data-ttu-id="947c5-130">Здесь требуется клавиатуру и монитор tooget hello IP-адрес устройства NUC.</span><span class="sxs-lookup"><span data-stu-id="947c5-130">Here you need keyboard and monitor tooget hello IP address of your NUC device.</span></span> <span data-ttu-id="947c5-131">Если вы уже знаете hello IP адрес, можно пропустить toostep 3 в этом разделе.</span><span class="sxs-lookup"><span data-stu-id="947c5-131">If you already know hello IP address, you can skip toostep 3 in this section.</span></span>

1. <span data-ttu-id="947c5-132">Включите Intel NUC, нажав кнопку питания hello и журналов в системе hello.</span><span class="sxs-lookup"><span data-stu-id="947c5-132">Turn on Intel NUC by pressing hello Power button and log in hello system.</span></span>

   <span data-ttu-id="947c5-133">имя пользователя по умолчанию Hello и пароль указаны оба `root`.</span><span class="sxs-lookup"><span data-stu-id="947c5-133">hello default user name and password are both `root`.</span></span>

2. <span data-ttu-id="947c5-134">Получить IP-адрес NUC hello, выполнив hello `ifconfig` команды.</span><span class="sxs-lookup"><span data-stu-id="947c5-134">Get hello IP address of NUC by running hello `ifconfig` command.</span></span> <span data-ttu-id="947c5-135">Эта процедура выполняется на устройстве NUC hello.</span><span class="sxs-lookup"><span data-stu-id="947c5-135">This step is done on hello NUC device.</span></span>

   <span data-ttu-id="947c5-136">Ниже приведен пример выходных данных команды hello.</span><span class="sxs-lookup"><span data-stu-id="947c5-136">Here is an example of hello command output.</span></span>

   ![Выходные данные ifconfig с IP-адресом NUC](media/iot-hub-gateway-kit-lessons/lesson1/ifconfig.png)

   <span data-ttu-id="947c5-138">В этом примере hello значение, следующее за `inet addr:` hello IP-адрес, необходимый при планировании tooconnect удаленно с tooIntel компьютера узла NUC.</span><span class="sxs-lookup"><span data-stu-id="947c5-138">In this example, hello value that follows `inet addr:` is hello IP address that you need when you plan tooconnect remotely from a host computer tooIntel NUC.</span></span>

3. <span data-ttu-id="947c5-139">Используйте одну из следующую SSH клиентов из вашего узла машины tooconnect tooIntel NUC hello.</span><span class="sxs-lookup"><span data-stu-id="947c5-139">Use one of hello following SSH clients from your host machine tooconnect tooIntel NUC.</span></span>

   - <span data-ttu-id="947c5-140">[PuTTY](http://www.putty.org/) для Windows.</span><span class="sxs-lookup"><span data-stu-id="947c5-140">[PuTTY](http://www.putty.org/) for Windows.</span></span>
   - <span data-ttu-id="947c5-141">Hello сборки в клиент SSH на Ubuntu или macOS.</span><span class="sxs-lookup"><span data-stu-id="947c5-141">hello build-in SSH client on Ubuntu or macOS.</span></span>

   <span data-ttu-id="947c5-142">Это обеспечивает более эффективное и продуктивную toooperate на Intel NUC от главного компьютера.</span><span class="sxs-lookup"><span data-stu-id="947c5-142">It is more efficient and productive toooperate on Intel NUC from a host computer.</span></span> <span data-ttu-id="947c5-143">Требуется hello hello IP-адрес, имя пользователя и пароль hello tooconnect NUC через клиент SSH.</span><span class="sxs-lookup"><span data-stu-id="947c5-143">You need hello hello IP address, user name and password tooconnect hello NUC via SSH client.</span></span> <span data-ttu-id="947c5-144">Ниже приведен пример использования hello SSH-клиента на macOS.</span><span class="sxs-lookup"><span data-stu-id="947c5-144">Here is hello example use SSH client on macOS.</span></span>
   <span data-ttu-id="947c5-145">![SSH-клиент, запущенный на macOS](media/iot-hub-gateway-kit-lessons/lesson1/ssh.png)</span><span class="sxs-lookup"><span data-stu-id="947c5-145">![SSH client running on macOS](media/iot-hub-gateway-kit-lessons/lesson1/ssh.png)</span></span>

## <a name="install-hello-azure-iot-edge-package"></a><span data-ttu-id="947c5-146">Установите пакет Azure IoT Edge hello</span><span class="sxs-lookup"><span data-stu-id="947c5-146">Install hello Azure IoT Edge package</span></span>

<span data-ttu-id="947c5-147">пакет Azure IoT Edge Hello содержит hello заранее скомпилированные двоичные файлы hello SDK и его зависимости.</span><span class="sxs-lookup"><span data-stu-id="947c5-147">hello Azure IoT Edge package contains hello pre-compiled binaries of hello SDK and its dependencies.</span></span> <span data-ttu-id="947c5-148">Эти двоичные файлы являются Azure IoT Edge, hello IoT Azure SDK и соответствующих средств hello.</span><span class="sxs-lookup"><span data-stu-id="947c5-148">These binaries are Azure IoT Edge, hello Azure IoT SDK and hello corresponding tools.</span></span> <span data-ttu-id="947c5-149">Hello пакет также содержит пример приложения «hello_world», используется toovalidate функциональность шлюза hello.</span><span class="sxs-lookup"><span data-stu-id="947c5-149">hello package also contains a "hello_world" sample application that is used toovalidate hello gateway functionality.</span></span> <span data-ttu-id="947c5-150">Граница IoT является hello основной частью hello шлюза.</span><span class="sxs-lookup"><span data-stu-id="947c5-150">IoT Edge is hello core part of hello gateway.</span></span> <span data-ttu-id="947c5-151">tooinstall hello пакет, выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="947c5-151">tooinstall hello package, follow these steps:</span></span>

1. <span data-ttu-id="947c5-152">Добавьте репозиторий облака IoT hello, выполнив следующие команды в окне терминала hello:</span><span class="sxs-lookup"><span data-stu-id="947c5-152">Add hello IoT cloud repository by running hello following commands in a terminal window:</span></span>

   ```bash
   rpm --import http://iotdk.intel.com/misc/iot_pub.key
   smart channel --add IoT_Cloud type=rpm-md name="IoT_Cloud" baseurl=http://iotdk.intel.com/repos/iot-cloud/wrlinux7/rcpl13/ -y
   ```

   <span data-ttu-id="947c5-153">Hello `rpm` команда импортирует hello ключ об/мин.</span><span class="sxs-lookup"><span data-stu-id="947c5-153">hello `rpm` command imports hello rpm key.</span></span> <span data-ttu-id="947c5-154">Hello `smart channel` команда добавляет hello rpm канала toohello смарт-диспетчера пакетов.</span><span class="sxs-lookup"><span data-stu-id="947c5-154">hello `smart channel` command adds hello rpm channel toohello Smart Package Manager.</span></span> <span data-ttu-id="947c5-155">Перед запуском hello `smart update` команду, вы видите вывод как ниже.</span><span class="sxs-lookup"><span data-stu-id="947c5-155">Before you run hello `smart update` command, you see an output like below.</span></span>

   ![результаты выполнения команд rpm и smart channel](media/iot-hub-gateway-kit-lessons/lesson1/rpm_smart_channel.png)

   ```bash
   smart update
   ```

2. <span data-ttu-id="947c5-157">Установка пакета hello, выполнив следующую команду hello:</span><span class="sxs-lookup"><span data-stu-id="947c5-157">Install hello package by running hello following command:</span></span>

   ```bash
   smart install packagegroup-cloud-azure -y
   ```

   <span data-ttu-id="947c5-158">`packagegroup-cloud-azure`— Имя пакета hello hello.</span><span class="sxs-lookup"><span data-stu-id="947c5-158">`packagegroup-cloud-azure` is hello name of hello package.</span></span> <span data-ttu-id="947c5-159">Hello `smart install` команды — пакет используется tooinstall hello.</span><span class="sxs-lookup"><span data-stu-id="947c5-159">hello `smart install` command is used tooinstall hello package.</span></span>

   <span data-ttu-id="947c5-160">После установки пакета hello Intel NUC является ожидаемым toowork как шлюз.</span><span class="sxs-lookup"><span data-stu-id="947c5-160">After hello package is installed, Intel NUC is expected toowork as a gateway.</span></span>

## <a name="run-hello-azure-iot-edge-helloworld-sample-application"></a><span data-ttu-id="947c5-161">Запустить hello Azure IoT края «hello_world» образец приложения</span><span class="sxs-lookup"><span data-stu-id="947c5-161">Run hello Azure IoT Edge "hello_world" sample application</span></span>

<span data-ttu-id="947c5-162">Go слишком`azureiotgatewaysdk/samples` и запуск приложения образец «hello_world» образец hello.</span><span class="sxs-lookup"><span data-stu-id="947c5-162">Go too`azureiotgatewaysdk/samples` and run hello sample "hello_world" sample application.</span></span> <span data-ttu-id="947c5-163">В этом образце приложения создает шлюз из hello `hello_world.json` файл и использует базовые компоненты hello Azure IoT Edge архитектура toolog файл tooa сообщение hello world hello каждые 5 секунд.</span><span class="sxs-lookup"><span data-stu-id="947c5-163">This sample application creates a gateway from hello `hello_world.json` file and uses hello fundamental components of hello Azure IoT Edge architecture toolog a hello world message tooa file every 5 seconds.</span></span>

<span data-ttu-id="947c5-164">Можно запустить «hello_world» образец hello образец приложения, запустив hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="947c5-164">You can run hello sample "hello_world" sample application by running hello following command:</span></span>

```bash
cd /usr/share/azureiotgatewaysdk/samples/hello_world/
./hello_world hello_world.json
```

<span data-ttu-id="947c5-165">Пример приложения Hello создает следующие hello, выходные данные при правильной работе функции hello шлюза:</span><span class="sxs-lookup"><span data-stu-id="947c5-165">hello sample application produces hello following output if hello gateway functionality is working correctly:</span></span>

![выходные данные приложения](media/iot-hub-gateway-kit-lessons/lesson1/hello_world.png)

<span data-ttu-id="947c5-167">Если у вас возникнут проблемы, искать решения на hello [страницу устранения неполадок](iot-hub-gateway-kit-c-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="947c5-167">If you have any problems, look for solutions on hello [troubleshooting page](iot-hub-gateway-kit-c-troubleshooting.md).</span></span>

## <a name="summary"></a><span data-ttu-id="947c5-168">Сводка</span><span class="sxs-lookup"><span data-stu-id="947c5-168">Summary</span></span>

<span data-ttu-id="947c5-169">Поздравляем!</span><span class="sxs-lookup"><span data-stu-id="947c5-169">Congratulations!</span></span> <span data-ttu-id="947c5-170">Итак, вы завершили настройку Intel NUC в качестве шлюза.</span><span class="sxs-lookup"><span data-stu-id="947c5-170">You've finished setting up Intel NUC as a gateway.</span></span> <span data-ttu-id="947c5-171">Теперь вы готовы toomove на следующем занятии tooset toohello компьютера узла, создать центр Azure IoT и зарегистрируйте логическое устройство концентратора Azure IoT.</span><span class="sxs-lookup"><span data-stu-id="947c5-171">Now you're ready toomove on toohello next lesson tooset up your host computer, create an Azure IoT hub and register your Azure IoT hub logical device.</span></span>

## <a name="next-steps"></a><span data-ttu-id="947c5-172">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="947c5-172">Next steps</span></span>
[<span data-ttu-id="947c5-173">Подготовка главного компьютера и Центра Интернета вещей Azure</span><span class="sxs-lookup"><span data-stu-id="947c5-173">Get your host computer and Azure IoT hub ready</span></span>](iot-hub-gateway-kit-c-sim-lesson2-get-the-tools-win32.md)
