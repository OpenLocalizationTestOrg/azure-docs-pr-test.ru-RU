---
title: "Приступая к работе с устройством SensorTag и шлюзом Интернета вещей Azure. Урок 1. Настройка Intel NUC | Документация Майкрософт"
description: "Настройка toowork Intel NUC виде шлюза IoT между датчика и данных датчика toocollect центр IoT Azure и отправить его tooIoT концентратора."
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
ms.openlocfilehash: 7c3ab3b014713c7facb86b8e8622d70e60a960e6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-intel-nuc-as-an-iot-gateway"></a><span data-ttu-id="f5c5b-104">Настройка Intel NUC в качестве шлюза Интернета вещей</span><span class="sxs-lookup"><span data-stu-id="f5c5b-104">Set up Intel NUC as an IoT gateway</span></span>
[!INCLUDE [iot-hub-get-started-device-selector](../../includes/iot-hub-get-started-device-selector.md)]

## <a name="what-you-will-do"></a><span data-ttu-id="f5c5b-105">Выполняемая задача</span><span class="sxs-lookup"><span data-stu-id="f5c5b-105">What you will do</span></span>

- <span data-ttu-id="f5c5b-106">Настройте Intel NUC в качестве шлюза Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="f5c5b-106">Set up Intel NUC as an IoT gateway.</span></span>
- <span data-ttu-id="f5c5b-107">Установите пакет Azure IoT Edge hello на hello Intel NUC.</span><span class="sxs-lookup"><span data-stu-id="f5c5b-107">Install hello Azure IoT Edge package on hello Intel NUC.</span></span>
- <span data-ttu-id="f5c5b-108">Запустите пример приложения «hello_world» на hello функциональность шлюза hello tooverify Intel NUC.</span><span class="sxs-lookup"><span data-stu-id="f5c5b-108">Run a "hello_world" sample application on hello Intel NUC tooverify hello gateway functionality.</span></span>

  > <span data-ttu-id="f5c5b-109">Если у вас возникнут проблемы, искать решения на hello [страницу устранения неполадок](iot-hub-gateway-kit-c-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="f5c5b-109">If you have any problems, look for solutions on hello [troubleshooting page](iot-hub-gateway-kit-c-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="f5c5b-110">Новые знания</span><span class="sxs-lookup"><span data-stu-id="f5c5b-110">What you will learn</span></span>

<span data-ttu-id="f5c5b-111">Из этого урока вы узнаете:</span><span class="sxs-lookup"><span data-stu-id="f5c5b-111">In this lesson, you will learn:</span></span>

- <span data-ttu-id="f5c5b-112">Как tooconnect Intel NUC с периферийные устройства.</span><span class="sxs-lookup"><span data-stu-id="f5c5b-112">How tooconnect Intel NUC with peripherals.</span></span>
- <span data-ttu-id="f5c5b-113">Как пакеты hello необходимые tooinstall и обновления на использование Intel NUC hello смарт-диспетчера пакетов.</span><span class="sxs-lookup"><span data-stu-id="f5c5b-113">How tooinstall and update hello required packages on Intel NUC using hello Smart Package Manager.</span></span>
- <span data-ttu-id="f5c5b-114">Как toorun hello» hello_world» образец функциональность шлюза hello tooverify приложения.</span><span class="sxs-lookup"><span data-stu-id="f5c5b-114">How toorun hello "hello_world" sample application tooverify hello gateway functionality.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="f5c5b-115">Необходимые элементы</span><span class="sxs-lookup"><span data-stu-id="f5c5b-115">What you need</span></span>

- <span data-ttu-id="f5c5b-116">DE3815TYKE комплект Intel NUC с hello шлюза программного обеспечения Intel IoT Suite (р. воздушного Linux * 7.0.0.13) предварительно.</span><span class="sxs-lookup"><span data-stu-id="f5c5b-116">An Intel NUC Kit DE3815TYKE with hello Intel IoT Gateway Software Suite (Wind River Linux *7.0.0.13) preinstalled.</span></span> <span data-ttu-id="f5c5b-117">[Щелкните здесь toopurchase Grove IoT коммерческих шлюза комплект](https://www.seeedstudio.com/Grove-IoT-Commercial-Gateway-Kit-p-2724.html).</span><span class="sxs-lookup"><span data-stu-id="f5c5b-117">[Click here toopurchase Grove IoT Commercial Gateway Kit](https://www.seeedstudio.com/Grove-IoT-Commercial-Gateway-Kit-p-2724.html).</span></span>
- <span data-ttu-id="f5c5b-118">Кабель Ethernet.</span><span class="sxs-lookup"><span data-stu-id="f5c5b-118">An Ethernet cable.</span></span>
- <span data-ttu-id="f5c5b-119">Клавиатура.</span><span class="sxs-lookup"><span data-stu-id="f5c5b-119">A keyboard.</span></span>
- <span data-ttu-id="f5c5b-120">Кабель HDMI или VGA.</span><span class="sxs-lookup"><span data-stu-id="f5c5b-120">An HDMI or VGA cable.</span></span>
- <span data-ttu-id="f5c5b-121">Монитор с портом HDMI или VGA.</span><span class="sxs-lookup"><span data-stu-id="f5c5b-121">A monitor with an HDMI or VGA port.</span></span>
- <span data-ttu-id="f5c5b-122">Необязательно: [Texas Instruments Sensor Tag (CC2650STK)](http://www.ti.com/tool/cc2650stk)</span><span class="sxs-lookup"><span data-stu-id="f5c5b-122">Optional: [Texas Instruments Sensor Tag (CC2650STK)](http://www.ti.com/tool/cc2650stk)</span></span>

![Комплект для шлюза](media/iot-hub-gateway-kit-lessons/lesson1/kit.png)

## <a name="connect-intel-nuc-with-hello-peripherals"></a><span data-ttu-id="f5c5b-124">Подключения Intel NUC hello периферийных устройств</span><span class="sxs-lookup"><span data-stu-id="f5c5b-124">Connect Intel NUC with hello peripherals</span></span>

<span data-ttu-id="f5c5b-125">изображение Hello ниже приведен пример NUC Intel, который связан с различными периферийные устройства:</span><span class="sxs-lookup"><span data-stu-id="f5c5b-125">hello image below is an example of Intel NUC that is connected with various peripherals:</span></span>

1. <span data-ttu-id="f5c5b-126">Подключенный tooa клавиатуры.</span><span class="sxs-lookup"><span data-stu-id="f5c5b-126">Connected tooa keyboard.</span></span>
2. <span data-ttu-id="f5c5b-127">Подключен монитор tooa кабель VGA или HDMI кабель.</span><span class="sxs-lookup"><span data-stu-id="f5c5b-127">Connected tooa monitor with a VGA cable or HDMI cable.</span></span>
3. <span data-ttu-id="f5c5b-128">Подключенный tooa проводной сети с помощью кабеля Ethernet.</span><span class="sxs-lookup"><span data-stu-id="f5c5b-128">Connected tooa wired network with an Ethernet cable.</span></span>
4. <span data-ttu-id="f5c5b-129">Источник питания подключенных tooa кабеля питания.</span><span class="sxs-lookup"><span data-stu-id="f5c5b-129">Connected tooa power supply with a power cable.</span></span>

![Tooperipherals подключен NUC Intel](media/iot-hub-gateway-kit-lessons/lesson1/nuc.png)

## <a name="connect-toohello-intel-nuc-system-from-host-computer-via-secure-shell-ssh"></a><span data-ttu-id="f5c5b-131">Подключение системы Intel NUC toohello от главного компьютера через Secure Shell (SSH)</span><span class="sxs-lookup"><span data-stu-id="f5c5b-131">Connect toohello Intel NUC system from host computer via Secure Shell (SSH)</span></span>

<span data-ttu-id="f5c5b-132">Необходимо будет клавиатуру и монитор tooget hello IP-адрес устройства Intel NUC.</span><span class="sxs-lookup"><span data-stu-id="f5c5b-132">You will need a keyboard and a monitor tooget hello IP address of your Intel NUC device.</span></span> <span data-ttu-id="f5c5b-133">Если вы уже знаете hello IP адрес, можно пропустить упреждающего toostep 3 в этом разделе.</span><span class="sxs-lookup"><span data-stu-id="f5c5b-133">If you already know hello IP address, you can skip ahead toostep 3 in this section.</span></span>

1. <span data-ttu-id="f5c5b-134">Включите hello Intel NUC, нажав кнопку питания hello и войдите в систему.</span><span class="sxs-lookup"><span data-stu-id="f5c5b-134">Turn on hello Intel NUC by pressing hello power button and then log in.</span></span>

   <span data-ttu-id="f5c5b-135">имя пользователя по умолчанию Hello и пароль указаны оба `root`.</span><span class="sxs-lookup"><span data-stu-id="f5c5b-135">hello default user name and password are both `root`.</span></span>

       > Hit hello enter key on your keyboard if you see either of hello following errors when you boot: 'A TPM error (7) occurred attempting tooread a pcr value.' or 'Timeout, No TPM chip found, activating TPM-bypass!'

2. <span data-ttu-id="f5c5b-136">Получить IP-адрес hello hello Intel NUC, выполнив hello `ifconfig` команду на устройстве Intel NUC hello.</span><span class="sxs-lookup"><span data-stu-id="f5c5b-136">Get hello IP address of hello Intel NUC by running hello `ifconfig` command on hello Intel NUC device.</span></span>

   <span data-ttu-id="f5c5b-137">Ниже приведен пример выходных данных команды hello.</span><span class="sxs-lookup"><span data-stu-id="f5c5b-137">Here is an example of hello command output.</span></span>

   ![Выходные данные ifconfig с IP-адресом Intel NUC](media/iot-hub-gateway-kit-lessons/lesson1/ifconfig.png)

   <span data-ttu-id="f5c5b-139">В этом примере hello значение, следующее за `inet addr:` hello IP-адрес, необходимый при подключении toohello Intel NUC от главного компьютера.</span><span class="sxs-lookup"><span data-stu-id="f5c5b-139">In this example, hello value that follows `inet addr:` is hello IP address that you need when connect toohello Intel NUC from a host computer.</span></span>

3. <span data-ttu-id="f5c5b-140">Используйте одну из следующую SSH клиентов из вашего узла компьютера tooconnect tooIntel NUC hello.</span><span class="sxs-lookup"><span data-stu-id="f5c5b-140">Use one of hello following SSH clients from your host computer tooconnect tooIntel NUC.</span></span>

    - <span data-ttu-id="f5c5b-141">[PuTTY](http://www.putty.org/) для Windows.</span><span class="sxs-lookup"><span data-stu-id="f5c5b-141">[PuTTY](http://www.putty.org/) for Windows.</span></span>
    - <span data-ttu-id="f5c5b-142">Hello встроенный клиент SSH на Ubuntu или macOS.</span><span class="sxs-lookup"><span data-stu-id="f5c5b-142">hello built-in SSH client on Ubuntu or macOS.</span></span>

   <span data-ttu-id="f5c5b-143">Это обеспечивает более эффективное и продуктивную toooperate NUC Intel от главного компьютера.</span><span class="sxs-lookup"><span data-stu-id="f5c5b-143">It is more efficient and productive toooperate an Intel NUC from a host computer.</span></span> <span data-ttu-id="f5c5b-144">Будет необходимо hello Intel NUC IP-адрес, пользователь имя и пароль tooit tooconnect через клиент SSH.</span><span class="sxs-lookup"><span data-stu-id="f5c5b-144">You'll need hello Intel NUC's IP address, user name and password tooconnect tooit via an SSH client.</span></span> <span data-ttu-id="f5c5b-145">Ниже приведен пример использования SSH-клиента в macOS.</span><span class="sxs-lookup"><span data-stu-id="f5c5b-145">Here is an example that uses an SSH client on macOS.</span></span>
   <span data-ttu-id="f5c5b-146">![SSH-клиент, запущенный на macOS](media/iot-hub-gateway-kit-lessons/lesson1/ssh.png)</span><span class="sxs-lookup"><span data-stu-id="f5c5b-146">![SSH client running on macOS](media/iot-hub-gateway-kit-lessons/lesson1/ssh.png)</span></span>

## <a name="install-hello-azure-iot-edge-package"></a><span data-ttu-id="f5c5b-147">Установите пакет Azure IoT Edge hello</span><span class="sxs-lookup"><span data-stu-id="f5c5b-147">Install hello Azure IoT Edge package</span></span>

<span data-ttu-id="f5c5b-148">пакет Azure IoT Edge Hello содержит hello заранее скомпилированные двоичные файлы IoT границей и его зависимости.</span><span class="sxs-lookup"><span data-stu-id="f5c5b-148">hello Azure IoT Edge package contains hello pre-compiled binaries of IoT Edge and its dependencies.</span></span> <span data-ttu-id="f5c5b-149">Эти двоичные файлы являются Azure IoT Edge, hello IoT Azure SDK и соответствующих средств hello.</span><span class="sxs-lookup"><span data-stu-id="f5c5b-149">These binaries are Azure IoT Edge, hello Azure IoT SDK and hello corresponding tools.</span></span> <span data-ttu-id="f5c5b-150">Hello пакет также содержит «hello_world» приложение представляет функциональность шлюза используется toovalidate hello.</span><span class="sxs-lookup"><span data-stu-id="f5c5b-150">hello package also contains a "hello_world" sample application is used toovalidate hello gateway functionality.</span></span> <span data-ttu-id="f5c5b-151">Граница IoT является hello основной частью hello шлюза.</span><span class="sxs-lookup"><span data-stu-id="f5c5b-151">IoT Edge is hello core part of hello gateway.</span></span> 

<span data-ttu-id="f5c5b-152">Выполните эти шаги tooinstall hello пакета.</span><span class="sxs-lookup"><span data-stu-id="f5c5b-152">Follow these steps tooinstall hello package.</span></span>

1. <span data-ttu-id="f5c5b-153">Добавьте hello облака IoT репозиторий, выполнив следующие команды в окне терминала hello:</span><span class="sxs-lookup"><span data-stu-id="f5c5b-153">Add hello IoT Cloud repository by running hello following commands in a terminal window:</span></span>

   ```bash
   rpm --import https://iotdk.intel.com/misc/iot_pub2.key
   smart channel --add IoT_Cloud type=rpm-md name="IoT_Cloud" baseurl=http://iotdk.intel.com/repos/iot-cloud/wrlinux7/rcpl13/ -y
   smart channel --add WR_Repo type=rpm-md baseurl=https://distro.windriver.com/release/idp-3-xt/public_feeds/WR-IDP-3-XT-Intel-Baytrail-public-repo/RCPL13/corei7_64/
   ```

   > <span data-ttu-id="f5c5b-154">Введите «y», при запросе too'Include этот канал? "</span><span class="sxs-lookup"><span data-stu-id="f5c5b-154">Enter 'y', when it prompts you too'Include this channel?'</span></span>
   
   <span data-ttu-id="f5c5b-155">При получении `import read failed(-1)` ошибку, используйте hello следующая проблема hello tooresolve команды:</span><span class="sxs-lookup"><span data-stu-id="f5c5b-155">If you receive an `import read failed(-1)` error, use hello following commands tooresolve hello issue:</span></span>
   ```bash
   wget http://iotdk.intel.com/misc/iot_pub2.key 
   rpm --import iot_pub2.key  
   ```

   <span data-ttu-id="f5c5b-156">Hello `rpm` команда импортирует hello ключ об/мин.</span><span class="sxs-lookup"><span data-stu-id="f5c5b-156">hello `rpm` command imports hello rpm key.</span></span> <span data-ttu-id="f5c5b-157">Hello `smart channel` команда добавляет hello rpm канала toohello смарт-диспетчера пакетов.</span><span class="sxs-lookup"><span data-stu-id="f5c5b-157">hello `smart channel` command adds hello rpm channel toohello Smart Package Manager.</span></span> <span data-ttu-id="f5c5b-158">Перед запуском hello `smart update` команды, вы увидите выходные данные, аналогичные показанным ниже.</span><span class="sxs-lookup"><span data-stu-id="f5c5b-158">Before you run hello `smart update` command, you will see an output like below.</span></span>

   ![результаты выполнения команд rpm и smart channel](media/iot-hub-gateway-kit-lessons/lesson1/rpm_smart_channel.png)

2. <span data-ttu-id="f5c5b-160">Выполните команду hello смарт-обновления:</span><span class="sxs-lookup"><span data-stu-id="f5c5b-160">Execute hello smart update command:</span></span>

   ```bash
   smart update
   ```

3. <span data-ttu-id="f5c5b-161">Установите пакет шлюза Azure IoT hello, выполнив hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="f5c5b-161">Install hello Azure IoT Gateway package by running hello following command:</span></span>

   ```bash
   smart install packagegroup-cloud-azure -y
   ```

   <span data-ttu-id="f5c5b-162">`packagegroup-cloud-azure`— Имя пакета hello hello.</span><span class="sxs-lookup"><span data-stu-id="f5c5b-162">`packagegroup-cloud-azure` is hello name of hello package.</span></span> <span data-ttu-id="f5c5b-163">Hello `smart install` команды — пакет используется tooinstall hello.</span><span class="sxs-lookup"><span data-stu-id="f5c5b-163">hello `smart install` command is used tooinstall hello package.</span></span>

    > <span data-ttu-id="f5c5b-164">Выполнения hello следующая команда, если вы видите эту ошибку: «открытый ключ недоступен»</span><span class="sxs-lookup"><span data-stu-id="f5c5b-164">Run hello following command if you see this error: 'public key not available'</span></span>

    ```bash
    smart config --set rpm-check-signatures=false
    smart install packagegroup-cloud-azure -y
    ```
    > <span data-ttu-id="f5c5b-165">Перезагрузить hello Intel NUC, если вы видите эту ошибку: «нет пакет предоставляет util-linux-dev»</span><span class="sxs-lookup"><span data-stu-id="f5c5b-165">Reboot hello Intel NUC if you see this error: 'no package provides util-linux-dev'</span></span>

   <span data-ttu-id="f5c5b-166">После установки пакета hello Intel NUC — Готово toofunction как шлюз.</span><span class="sxs-lookup"><span data-stu-id="f5c5b-166">After hello package is installed, Intel NUC is ready toofunction as a gateway.</span></span>

## <a name="run-hello-azure-iot-edge-helloworld-sample-application"></a><span data-ttu-id="f5c5b-167">Запустить hello Azure IoT края «hello_world» образец приложения</span><span class="sxs-lookup"><span data-stu-id="f5c5b-167">Run hello Azure IoT Edge "hello_world" sample application</span></span>

<span data-ttu-id="f5c5b-168">Следующий пример приложения Hello создает шлюз из `hello_world.json` файл и использует hello базовые компоненты архитектуры Azure IoT Edge toolog файл tooa сообщение hello world (log.txt) каждые 5 секунд.</span><span class="sxs-lookup"><span data-stu-id="f5c5b-168">hello following sample application creates a gateway from a `hello_world.json` file and uses hello fundamental components of Azure IoT Edge architecture toolog a hello world message tooa file (log.txt) every 5 seconds.</span></span>

<span data-ttu-id="f5c5b-169">Вы можете запустить пример Hello World hello, выполнив следующие команды hello:</span><span class="sxs-lookup"><span data-stu-id="f5c5b-169">You can run hello Hello World sample by executing hello following commands:</span></span>

```bash
cd /usr/share/azureiotgatewaysdk/samples/hello_world/
./hello_world hello_world.json
```

<span data-ttu-id="f5c5b-170">Разрешить приложения hello Hello World работать несколько минут и нажмите клавишу hello ввод ключа toostop его.</span><span class="sxs-lookup"><span data-stu-id="f5c5b-170">Let hello Hello World application run for a few minutes and then hit hello Enter key toostop it.</span></span>
<span data-ttu-id="f5c5b-171">![выходные данные приложения](media/iot-hub-gateway-kit-lessons/lesson1/hello_world.png)</span><span class="sxs-lookup"><span data-stu-id="f5c5b-171">![application output](media/iot-hub-gateway-kit-lessons/lesson1/hello_world.png)</span></span>

> <span data-ttu-id="f5c5b-172">Вы можете игнорировать любые ошибки "Недопустимый дескриптор аргумента (NULL)", которые появляются после нажатия клавиши ВВОД.</span><span class="sxs-lookup"><span data-stu-id="f5c5b-172">You can ignore any 'invalid argument handle(NULL)' errors that appear after you hit Enter.</span></span>

<span data-ttu-id="f5c5b-173">Убедитесь, что шлюз hello выполнено успешно, открыв файл log.txt hello, которая теперь находится в папке hello_world ![log.txt представления каталога](media/iot-hub-gateway-kit-lessons/lesson1/logtxtdir.png)</span><span class="sxs-lookup"><span data-stu-id="f5c5b-173">You can verify that hello gateway ran successfully by opening hello log.txt file that is now in your hello_world folder ![log.txt directory view](media/iot-hub-gateway-kit-lessons/lesson1/logtxtdir.png)</span></span>

<span data-ttu-id="f5c5b-174">Откройте файл log.txt, с помощью hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="f5c5b-174">Open log.txt using hello following command:</span></span>

```bash
vim log.txt
```

<span data-ttu-id="f5c5b-175">Вы увидите содержимое hello log.txt, которой будет выводиться в формате JSON hello ведения журнала сообщений, которые были записаны каждые 5 секунд модулем Hello World hello шлюза.</span><span class="sxs-lookup"><span data-stu-id="f5c5b-175">You will then see hello contents of log.txt, which will be a JSON formatted output of hello logging messages that were written every 5 seconds by hello gateway Hello World module.</span></span>
<span data-ttu-id="f5c5b-176">![Представление каталога log.txt](media/iot-hub-gateway-kit-lessons/lesson1/logtxtview.png)</span><span class="sxs-lookup"><span data-stu-id="f5c5b-176">![log.txt directory view](media/iot-hub-gateway-kit-lessons/lesson1/logtxtview.png)</span></span>

<span data-ttu-id="f5c5b-177">Если у вас возникнут проблемы, искать решения на hello [страницу устранения неполадок](iot-hub-gateway-kit-c-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="f5c5b-177">If you have any problems, look for solutions on hello [troubleshooting page](iot-hub-gateway-kit-c-troubleshooting.md).</span></span>

## <a name="summary"></a><span data-ttu-id="f5c5b-178">Сводка</span><span class="sxs-lookup"><span data-stu-id="f5c5b-178">Summary</span></span>

<span data-ttu-id="f5c5b-179">Поздравляем!</span><span class="sxs-lookup"><span data-stu-id="f5c5b-179">Congratulations!</span></span> <span data-ttu-id="f5c5b-180">Итак, вы завершили настройку Intel NUC в качестве шлюза.</span><span class="sxs-lookup"><span data-stu-id="f5c5b-180">You've finished setting up Intel NUC as a gateway.</span></span> <span data-ttu-id="f5c5b-181">Теперь вы готовы toomove на следующем занятии tooset toohello компьютера узла, создать центр IoT Azure и зарегистрировать логические устройства Azure IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="f5c5b-181">Now you're ready toomove on toohello next lesson tooset up your host computer, create an Azure IoT Hub and register your Azure IoT Hub logical device.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f5c5b-182">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="f5c5b-182">Next steps</span></span>
[<span data-ttu-id="f5c5b-183">Использовать tooconnect шлюза IoT tooAzure устройства центра IoT</span><span class="sxs-lookup"><span data-stu-id="f5c5b-183">Use an IoT gateway tooconnect a device tooAzure IoT Hub</span></span>](iot-hub-gateway-kit-c-iot-gateway-connect-device-to-cloud.md)

