---
title: "Подключение Raspberry Pi (C) к Интернету вещей Azure. Устранение неполадок | Документация Майкрософт"
description: "Страница со сведениями об устранении неполадок в работе Raspberry Pi Node.js"
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "неполадки Интернета вещей, проблемы Интернета вещей"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-c-get-started
ms.assetid: 3653c79b-8a0c-41d4-b0bf-f6b4edb4d233
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 828669db23fa8d608029134fbe364033456d935a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshooting"></a><span data-ttu-id="54e08-104">Устранение неполадок</span><span class="sxs-lookup"><span data-stu-id="54e08-104">Troubleshooting</span></span>
## <a name="hardware-issues"></a><span data-ttu-id="54e08-105">Проблемы с оборудованием</span><span class="sxs-lookup"><span data-stu-id="54e08-105">Hardware issues</span></span>
### <a name="the-application-runs-well-but-the-led-is-not-blinking"></a><span data-ttu-id="54e08-106">Приложение работает хорошо, но светодиодный индикатор не мигает</span><span class="sxs-lookup"><span data-stu-id="54e08-106">The application runs well but the LED is not blinking</span></span>
<span data-ttu-id="54e08-107">Эта проблема всегда связана с подключением микросхемы оборудования.</span><span class="sxs-lookup"><span data-stu-id="54e08-107">This issue is always related to the hardware circuit connectivity.</span></span> <span data-ttu-id="54e08-108">Чтобы определить проблемы, сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="54e08-108">Use the following steps to identify problems.</span></span>

1. <span data-ttu-id="54e08-109">Проверьте, выбран ли правильный порт **GPIO** на плате.</span><span class="sxs-lookup"><span data-stu-id="54e08-109">Check that you chose the correct **GPIO** on your board.</span></span> <span data-ttu-id="54e08-110">Следует использовать два порта: **GPIO GND (штырь 6)** и **GPIO 04 (штырь 7)**.</span><span class="sxs-lookup"><span data-stu-id="54e08-110">The two ports should be **GPIO GND (Pin 6)** and **GPIO 04 (Pin 7)**.</span></span>
2. <span data-ttu-id="54e08-111">Проверьте правильность полярности своего светодиодного индикатора.</span><span class="sxs-lookup"><span data-stu-id="54e08-111">Check that the polarity of your LED is correct.</span></span> <span data-ttu-id="54e08-112">Более длинная ножка должна указывать **положительный**, анодный штырь.</span><span class="sxs-lookup"><span data-stu-id="54e08-112">The longer leg should indicate the **positive**, anode pin.</span></span>
3. <span data-ttu-id="54e08-113">Используйте **штырь 3.3V** и **штырь GND** на устройстве Raspberry Pi 3.</span><span class="sxs-lookup"><span data-stu-id="54e08-113">Use the **3.3V Pin** and **GND Pin** on Raspberry Pi 3.</span></span> <span data-ttu-id="54e08-114">Устройство Pi следует считать источником постоянного тока.</span><span class="sxs-lookup"><span data-stu-id="54e08-114">Treat Pi as the DC power.</span></span> <span data-ttu-id="54e08-115">Проверьте, нормально ли работает светодиодный индикатор.</span><span class="sxs-lookup"><span data-stu-id="54e08-115">Check that the LED works fine.</span></span>

![Спецификация светодиодного индикатора](media/iot-hub-raspberry-pi-lessons/troubleshooting/led_spec.png)

### <a name="other-hardware-issues"></a><span data-ttu-id="54e08-117">Другие проблемы с оборудованием</span><span class="sxs-lookup"><span data-stu-id="54e08-117">Other hardware issues</span></span>
<span data-ttu-id="54e08-118">Сведения об устранении распространенных проблем на устройстве Raspberry Pi 3 см. на [этой официальной странице](http://elinux.org/R-Pi_Troubleshooting).</span><span class="sxs-lookup"><span data-stu-id="54e08-118">For information about solving common problems on Raspberry Pi 3, see the [official troubleshooting page](http://elinux.org/R-Pi_Troubleshooting).</span></span>

## <a name="nodejs-package-issues"></a><span data-ttu-id="54e08-119">Проблемы с пакетами Node.js</span><span class="sxs-lookup"><span data-stu-id="54e08-119">Node.js package issues</span></span>
### <a name="no-response-during-gulp-tasks"></a><span data-ttu-id="54e08-120">Нет ответа при выполнении задач Gulp</span><span class="sxs-lookup"><span data-stu-id="54e08-120">No response during gulp tasks</span></span>
<span data-ttu-id="54e08-121">Если при выполнении задач Gulp возникли проблемы, можно добавить параметр `--verbose` для отладки.</span><span class="sxs-lookup"><span data-stu-id="54e08-121">If you encounter problems running gulp tasks, you can add the `--verbose` option for debugging.</span></span> <span data-ttu-id="54e08-122">Попробуйте завершить текущие задачи Gulp, используя клавиши `Ctrl + C`, а затем выполните следующую команду в окне консоли, чтобы просмотреть сообщения отладки.</span><span class="sxs-lookup"><span data-stu-id="54e08-122">Try to terminate current gulp tasks by using `Ctrl + C`, and then run the following command in your console window to see debug messages.</span></span> <span data-ttu-id="54e08-123">В выходных данных консоли должны отобразиться подробные сообщения об ошибках.</span><span class="sxs-lookup"><span data-stu-id="54e08-123">You might see detailed error messages in your console output.</span></span> 

```bash
gulp --verbose
```

### <a name="device-discovery-issues"></a><span data-ttu-id="54e08-124">Проблемы с обнаружением устройств</span><span class="sxs-lookup"><span data-stu-id="54e08-124">Device discovery issues</span></span>
<span data-ttu-id="54e08-125">Справку по устранению распространенных проблем с помощью команды `devdisco` см. в [файле сведений](https://github.com/Azure/device-discovery-cli/blob/develop/readme.md).</span><span class="sxs-lookup"><span data-stu-id="54e08-125">For help in troubleshooting common problems with the `devdisco` command, check the [readme](https://github.com/Azure/device-discovery-cli/blob/develop/readme.md).</span></span>

### <a name="npm-issues"></a><span data-ttu-id="54e08-126">Проблемы с NPM</span><span class="sxs-lookup"><span data-stu-id="54e08-126">NPM issues</span></span>
<span data-ttu-id="54e08-127">Попробуйте обновить пакет NPM, выполнив следующую команду:</span><span class="sxs-lookup"><span data-stu-id="54e08-127">Try to update your NPM package with the following command:</span></span>

```bash
npm install -g npm
```

<span data-ttu-id="54e08-128">Если проблема не исчезла, оставьте комментарии в конце этой статьи или задайте вопрос о проблеме в GitHub в нашем [примере репозитория](https://github.com/Azure-Samples/iot-hub-c-raspberrypi-getting-started).</span><span class="sxs-lookup"><span data-stu-id="54e08-128">If the problem still exists, leave your comments at the end of this article or create a GitHub issue in our [sample repository](https://github.com/Azure-Samples/iot-hub-c-raspberrypi-getting-started)</span></span>

## <a name="remote-debugging"></a><span data-ttu-id="54e08-129">Удаленная отладка</span><span class="sxs-lookup"><span data-stu-id="54e08-129">Remote debugging</span></span>

<span data-ttu-id="54e08-130">Поддержка удаленной отладки скоро станет доступной в расширении C/C++ для Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="54e08-130">Remote debugging support will be available soon in Visual Studio Code C/C++ Extension.</span></span>

<span data-ttu-id="54e08-131">Кроме того, вы можете использовать инструмент GDB через привычный терминал SSH:</span><span class="sxs-lookup"><span data-stu-id="54e08-131">In a meanwhile you can use GDB via your favourite SSH terminal:</span></span>

```bash
cd c-pi-lesson-x
sudo gdb app
```

## <a name="azure-cli-issues"></a><span data-ttu-id="54e08-132">Проблемы с Azure CLI</span><span class="sxs-lookup"><span data-stu-id="54e08-132">Azure-CLI issues</span></span>
<span data-ttu-id="54e08-133">Интерфейс командной строки Azure (Azure CLI) — это сборка предварительной версии.</span><span class="sxs-lookup"><span data-stu-id="54e08-133">The Azure command-line interface (Azure CLI) is a preview build.</span></span> <span data-ttu-id="54e08-134">Решения можно найти в [руководстве по установке предварительной версии](https://github.com/Azure/azure-cli/blob/master/doc/preview_install_guide.md).</span><span class="sxs-lookup"><span data-stu-id="54e08-134">Look for solution in the [Preview Install Guide](https://github.com/Azure/azure-cli/blob/master/doc/preview_install_guide.md) to seek solutions.</span></span> <span data-ttu-id="54e08-135">Попытайтесь обновить Azure CLI до последней версии, если команда не работает должным образом.</span><span class="sxs-lookup"><span data-stu-id="54e08-135">Try to upgrade Azure-cli to latest version when commands don’t work as expected.</span></span>

<span data-ttu-id="54e08-136">При появлении ошибок в средстве сообщите о [проблеме](https://github.com/Azure/azure-cli/issues) в разделе **Проблемы** репозитория GitHub.</span><span class="sxs-lookup"><span data-stu-id="54e08-136">If you encounter any bugs with the tool, file an [issue](https://github.com/Azure/azure-cli/issues) in the **Issues** section of the GitHub repo.</span></span>

<span data-ttu-id="54e08-137">Справку по устранению распространенных проблем см. в [файле сведений](https://github.com/Azure/azure-cli/blob/master/README.rst).</span><span class="sxs-lookup"><span data-stu-id="54e08-137">For help troubleshooting common problems, check the [readme](https://github.com/Azure/azure-cli/blob/master/README.rst).</span></span>

<span data-ttu-id="54e08-138">При появлении сообщения "Не удалось найти версию, которая удовлетворяет требованиям" выполните следующую команду, чтобы обновить pip до последней версии.</span><span class="sxs-lookup"><span data-stu-id="54e08-138">If you meet "Could not find a version that satisfies the requirement", please run the following command to upgrade pip to lastest version.</span></span>

```bash
python -m pip install --upgrade pip
```

## <a name="python-installation-issues"></a><span data-ttu-id="54e08-139">Проблемы с установкой Python</span><span class="sxs-lookup"><span data-stu-id="54e08-139">Python installation issues</span></span>
### <a name="legacy-installation-issues-macos"></a><span data-ttu-id="54e08-140">Проблемы с устаревшими установками (macOS)</span><span class="sxs-lookup"><span data-stu-id="54e08-140">Legacy installation issues (macOS)</span></span>
<span data-ttu-id="54e08-141">При установке **pip** возникает ошибка разрешения, если есть устаревшие пакеты, которые устанавливаются с использованием разрешений **su**.</span><span class="sxs-lookup"><span data-stu-id="54e08-141">When you're installing **pip**, a permission error is thrown when older packages that are installed with **su** permissions.</span></span> <span data-ttu-id="54e08-142">Такая ситуация возникает из-за того, что предыдущая установка Python с использованием brew (macOS) удалена не полностью.</span><span class="sxs-lookup"><span data-stu-id="54e08-142">This situation occurs because a previous installation of Python using brew (macOS) is not uninstalled completely.</span></span> <span data-ttu-id="54e08-143">Некоторые пакеты **pip** из предыдущей установки созданы с помощью разрешений корневой папки, что приводит к ошибке разрешения.</span><span class="sxs-lookup"><span data-stu-id="54e08-143">Some **pip** packages from a previous installation were created by root, which causes the permission error.</span></span> <span data-ttu-id="54e08-144">Чтобы решить эту проблему, необходимо удалить эти пакеты, установленные с помощью разрешений корневой папки.</span><span class="sxs-lookup"><span data-stu-id="54e08-144">The solution is to remove those packages installed by root.</span></span> <span data-ttu-id="54e08-145">Для этого необходимо сделать следующее:</span><span class="sxs-lookup"><span data-stu-id="54e08-145">Use the following steps to complete this task:</span></span>

1. <span data-ttu-id="54e08-146">Перейдите к папке /usr/local/lib/python2.7/site-packages.</span><span class="sxs-lookup"><span data-stu-id="54e08-146">Go to: /usr/local/lib/python2.7/site-packages</span></span>
2. <span data-ttu-id="54e08-147">Выведите список пакетов, созданных с использованием разрешений корневой папки: `ls -l | grep root`.</span><span class="sxs-lookup"><span data-stu-id="54e08-147">List packages create by root: `ls -l | grep root`</span></span>
3. <span data-ttu-id="54e08-148">Удалите пакеты из шага 2: `sudo rm -rf {package name}`.</span><span class="sxs-lookup"><span data-stu-id="54e08-148">Uninstall packages from step 2: `sudo rm -rf {package name}`</span></span>
4. <span data-ttu-id="54e08-149">Переустановите Python.</span><span class="sxs-lookup"><span data-stu-id="54e08-149">Reinstall Python.</span></span>

## <a name="azure-iot-hub-issues"></a><span data-ttu-id="54e08-150">Проблемы с Центром Интернета вещей Azure</span><span class="sxs-lookup"><span data-stu-id="54e08-150">Azure IoT Hub issues</span></span>
<span data-ttu-id="54e08-151">Если Центр Интернета вещей Azure успешно подготовлен с помощью `azure-cli` и требуется инструмент для управления устройствами, подключенными к вашему Центру Интернета вещей, воспользуйтесь следующими инструментами:</span><span class="sxs-lookup"><span data-stu-id="54e08-151">If you've successfully provisioned your Azure IoT hub with `azure-cli`, and you need a tool to manage the devices that are connecting to your IoT hub, try the following tools:</span></span>

### <a name="device-explorer"></a><span data-ttu-id="54e08-152">Обозреватель устройств</span><span class="sxs-lookup"><span data-stu-id="54e08-152">Device Explorer</span></span>
<span data-ttu-id="54e08-153">[Обозреватель устройств](https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer) работает на локальном компьютере Windows и подключается к Центру Интернета вещей в Azure.</span><span class="sxs-lookup"><span data-stu-id="54e08-153">[Device Explorer](https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer) runs on your Windows local machine and connects to your IoT hub in Azure.</span></span> <span data-ttu-id="54e08-154">Он взаимодействует со следующими [конечными точками Центра Интернета вещей](iot-hub-devguide.md):</span><span class="sxs-lookup"><span data-stu-id="54e08-154">It communicates with the following [IoT Hub endpoints](iot-hub-devguide.md):</span></span>

* <span data-ttu-id="54e08-155">*управление удостоверениями устройств* для подготовки устройств, зарегистрированных в Центре Интернета вещей, и управления ими;</span><span class="sxs-lookup"><span data-stu-id="54e08-155">*Device identity management* to provision and manage devices registered with your IoT hub.</span></span>
* <span data-ttu-id="54e08-156">*получение сообщений с устройства в облако*, что позволяет отслеживать сообщения, отправляемые с устройства в Центр Интернета вещей;</span><span class="sxs-lookup"><span data-stu-id="54e08-156">*Receive device-to-cloud* so you can monitor messages sent from your device to your IoT hub.</span></span>
* <span data-ttu-id="54e08-157">*отправка сообщений из облака на устройство*, что позволяет отправлять сообщения на устройства из вашего Центра Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="54e08-157">*Send cloud-to-device* so you can send messages to your devices from your IoT hub.</span></span>

<span data-ttu-id="54e08-158">Настройте свою `IoT hub connection string` в этом инструменте, чтобы использовать его возможности.</span><span class="sxs-lookup"><span data-stu-id="54e08-158">Configure your `IoT hub connection string` within this tool to use all its capabilities.</span></span>

### <a name="iot-hub-explorer"></a><span data-ttu-id="54e08-159">Обозреватель Центра Интернета вещей</span><span class="sxs-lookup"><span data-stu-id="54e08-159">IoT hub Explorer</span></span>
<span data-ttu-id="54e08-160">[Обозреватель Центра Интернета вещей](https://github.com/Azure/iothub-explorer) — это пример мультиплатформенного инструмента интерфейса командной строки для управления клиентами устройств.</span><span class="sxs-lookup"><span data-stu-id="54e08-160">[IoT hub Explorer](https://github.com/Azure/iothub-explorer) is a sample multiplatform CLI tool to manage device clients.</span></span> <span data-ttu-id="54e08-161">Инструмент можно использовать для управления устройствами в реестре удостоверений, мониторинга сообщений, отправляемых с устройства в облако, и отправки команд, передаваемых из облака на устройство.</span><span class="sxs-lookup"><span data-stu-id="54e08-161">You can use the tool to manage the devices in the identity registry, monitor device-to-cloud messages, and send cloud-to-device commands.</span></span>

<span data-ttu-id="54e08-162">Чтобы установить последнюю версию (предварительную версию) инструмента iothub-explorer, выполните следующую команду в среде командной строки:</span><span class="sxs-lookup"><span data-stu-id="54e08-162">To install the latest (prerelease) version of the iothub-explorer tool, run the following command in your command-line environment:</span></span>

```
npm install -g iothub-explorer@latest
```

<span data-ttu-id="54e08-163">Дополнительную справку о всех командах iothub-explorer и их параметрах можно получить, выполнив следующую команду:</span><span class="sxs-lookup"><span data-stu-id="54e08-163">You can use the following command to get additional help about all the iothub-explorer commands and their parameters:</span></span>

```bash
iothub-explorer help
```

### <a name="azure-portal"></a><span data-ttu-id="54e08-164">Портал Azure</span><span class="sxs-lookup"><span data-stu-id="54e08-164">Azure portal</span></span>
<span data-ttu-id="54e08-165">Все возможности интерфейса командной строки помогают создавать все ресурсы Azure и управлять ими.</span><span class="sxs-lookup"><span data-stu-id="54e08-165">A full CLI experience helps you create and manage all your Azure resources.</span></span> <span data-ttu-id="54e08-166">Для подготовки, отладки ресурсов Azure и управления ими можно также воспользоваться [порталом Azure](../azure-portal-overview.md).</span><span class="sxs-lookup"><span data-stu-id="54e08-166">You might also want to use the [Azure portal](../azure-portal-overview.md) to help provision, manage, and debug your Azure resources.</span></span>

## <a name="azure-storage-issues"></a><span data-ttu-id="54e08-167">Проблемы со службой хранилища Azure</span><span class="sxs-lookup"><span data-stu-id="54e08-167">Azure storage issues</span></span>
<span data-ttu-id="54e08-168">[Обозреватель служб хранилища Microsoft Azure (предварительная версия)](http://storageexplorer.com) — это автономное приложение от корпорации Майкрософт, которое можно использовать для работы с данными из службы хранилища Azure на платформе Windows, macOS и Linux.</span><span class="sxs-lookup"><span data-stu-id="54e08-168">[Microsoft Azure Storage Explorer (preview)](http://storageexplorer.com) is a standalone app from Microsoft that you can use to work with Azure Storage data on Windows, macOS, and Linux.</span></span> <span data-ttu-id="54e08-169">Используя этот инструмент, можно подключаться к таблице и просматривать данные в ней.</span><span class="sxs-lookup"><span data-stu-id="54e08-169">By using this tool, you can connect to your table and see the data in it.</span></span> <span data-ttu-id="54e08-170">Его можно использовать для устранения неполадок в вашей службе хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="54e08-170">You can use this tool to troubleshoot your Azure Storage issues.</span></span>
