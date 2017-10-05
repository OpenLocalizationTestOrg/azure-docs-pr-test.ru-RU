---
title: "Подключение Raspberry Pi (C) к Интернету вещей Azure. Устранение неполадок | Документация Майкрософт"
description: "Страница со сведениями об устранении неполадок в работе Raspberry Pi Node.js"
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "неполадки Интернета вещей, проблемы Интернета вещей"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-node-get-started
ms.assetid: 22cf50dc-8206-42a2-a1fc-f75fa85135fa
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: f9058068972ddbb674d3cd159948835dc88c4451
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshooting"></a><span data-ttu-id="029d0-104">Устранение неполадок</span><span class="sxs-lookup"><span data-stu-id="029d0-104">Troubleshooting</span></span>
## <a name="hardware-issues"></a><span data-ttu-id="029d0-105">Проблемы с оборудованием</span><span class="sxs-lookup"><span data-stu-id="029d0-105">Hardware issues</span></span>
### <a name="the-application-runs-well-but-the-led-is-not-blinking"></a><span data-ttu-id="029d0-106">Приложение работает хорошо, но светодиодный индикатор не мигает</span><span class="sxs-lookup"><span data-stu-id="029d0-106">The application runs well but the LED is not blinking</span></span>
<span data-ttu-id="029d0-107">Эта проблема всегда связана с подключением микросхемы оборудования.</span><span class="sxs-lookup"><span data-stu-id="029d0-107">This issue is always related to hardware circuit connectivity.</span></span> <span data-ttu-id="029d0-108">Чтобы определить проблемы, сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="029d0-108">Use the following steps to identify problems:</span></span>

1. <span data-ttu-id="029d0-109">Проверьте, выбран ли правильный порт **GPIO** на плате.</span><span class="sxs-lookup"><span data-stu-id="029d0-109">Check that you chose the correct **GPIO** on your board.</span></span> <span data-ttu-id="029d0-110">Следует использовать два порта: **GPIO GND (штырь 6)** и **GPIO 04 (штырь 7)**.</span><span class="sxs-lookup"><span data-stu-id="029d0-110">The two ports should be **GPIO GND (Pin 6)** and **GPIO 04 (Pin 7)**.</span></span>
2. <span data-ttu-id="029d0-111">Проверьте правильность полярности своего светодиодного индикатора.</span><span class="sxs-lookup"><span data-stu-id="029d0-111">Check that the polarity of your LED is correct.</span></span> <span data-ttu-id="029d0-112">Более длинная ножка должна указывать **положительный**, анодный штырь.</span><span class="sxs-lookup"><span data-stu-id="029d0-112">The longer leg should indicate the **positive**, anode pin.</span></span>
3. <span data-ttu-id="029d0-113">Используйте **штырь 3.3V** и **штырь GND** на устройстве Raspberry Pi 3.</span><span class="sxs-lookup"><span data-stu-id="029d0-113">Use the **3.3V Pin** and **GND Pin** on Raspberry Pi 3.</span></span> <span data-ttu-id="029d0-114">Устройство Pi следует считать источником постоянного тока.</span><span class="sxs-lookup"><span data-stu-id="029d0-114">Treat Pi as the DC power.</span></span> <span data-ttu-id="029d0-115">Проверьте, нормально ли работает светодиодный индикатор.</span><span class="sxs-lookup"><span data-stu-id="029d0-115">Check that the LED works fine.</span></span>

![Спецификация светодиодного индикатора](media/iot-hub-raspberry-pi-lessons/troubleshooting/led_spec.png)

### <a name="other-hardware-issues"></a><span data-ttu-id="029d0-117">Другие проблемы с оборудованием</span><span class="sxs-lookup"><span data-stu-id="029d0-117">Other hardware issues</span></span>
<span data-ttu-id="029d0-118">Сведения об устранении распространенных проблем на устройстве Raspberry Pi 3 см. на [этой официальной странице](http://elinux.org/R-Pi_Troubleshooting).</span><span class="sxs-lookup"><span data-stu-id="029d0-118">For information about solving common problems on Raspberry Pi 3, see the [official troubleshooting page](http://elinux.org/R-Pi_Troubleshooting).</span></span>

## <a name="nodejs-package-issues"></a><span data-ttu-id="029d0-119">Проблемы с пакетами Node.js</span><span class="sxs-lookup"><span data-stu-id="029d0-119">Node.js package issues</span></span>
### <a name="no-response-during-gulp-tasks"></a><span data-ttu-id="029d0-120">Нет ответа при выполнении задач Gulp</span><span class="sxs-lookup"><span data-stu-id="029d0-120">No response during gulp tasks</span></span>
<span data-ttu-id="029d0-121">Если при выполнении задач Gulp возникли проблемы, можно добавить параметр `--verbose` для отладки.</span><span class="sxs-lookup"><span data-stu-id="029d0-121">If you encounter problems in running gulp tasks, you can add the `--verbose` option for debugging.</span></span> <span data-ttu-id="029d0-122">Попробуйте завершить текущие задачи Gulp с помощью клавиш Ctrl + C, а затем выполните следующую команду в окне консоли, чтобы просмотреть сообщения отладки.</span><span class="sxs-lookup"><span data-stu-id="029d0-122">Try to terminate current gulp tasks by using Ctrl + C, and then run the following command in your console window to see debug messages.</span></span> <span data-ttu-id="029d0-123">В выходных данных консоли должны отобразиться подробные сообщения об ошибках.</span><span class="sxs-lookup"><span data-stu-id="029d0-123">You might see detailed error messages in your console output.</span></span>

```bash
gulp --verbose
```

### <a name="device-discovery-issues"></a><span data-ttu-id="029d0-124">Проблемы с обнаружением устройств</span><span class="sxs-lookup"><span data-stu-id="029d0-124">Device discovery issues</span></span>
<span data-ttu-id="029d0-125">Справку по устранению распространенных проблем с помощью команды `devdisco` см. в [файле сведений](https://github.com/Azure/device-discovery-cli/blob/develop/readme.md).</span><span class="sxs-lookup"><span data-stu-id="029d0-125">For help in troubleshooting common problems with the `devdisco` command, check the [readme](https://github.com/Azure/device-discovery-cli/blob/develop/readme.md).</span></span>

### <a name="npm-issues"></a><span data-ttu-id="029d0-126">проблемы с NPM</span><span class="sxs-lookup"><span data-stu-id="029d0-126">npm issues</span></span>
<span data-ttu-id="029d0-127">Попробуйте обновить пакет NPM, выполнив следующую команду.</span><span class="sxs-lookup"><span data-stu-id="029d0-127">Try to update your npm package by using the following command:</span></span>

```bash
npm install -g npm
```

<span data-ttu-id="029d0-128">Если проблема не исчезла, оставьте комментарии в конце этой статьи или задайте вопрос о проблеме в GitHub в нашем [примере репозитория](https://github.com/Azure-Samples/iot-hub-node-raspberrypi-getting-started).</span><span class="sxs-lookup"><span data-stu-id="029d0-128">If the problem still exists, leave your comments at the end of this article or create a GitHub issue in our [sample repository](https://github.com/Azure-Samples/iot-hub-node-raspberrypi-getting-started).</span></span>

## <a name="remote-debugging"></a><span data-ttu-id="029d0-129">Удаленная отладка</span><span class="sxs-lookup"><span data-stu-id="029d0-129">Remote debugging</span></span>
### <a name="run-the-sample-application-in-debug-mode"></a><span data-ttu-id="029d0-130">Запуск примера приложения в режиме отладки</span><span class="sxs-lookup"><span data-stu-id="029d0-130">Run the sample application in debug mode</span></span>
```bash
gulp run --debug
```

<span data-ttu-id="029d0-131">Когда модуль отладки будет готов, вы должны увидеть ```Debugger listening on port 5858``` в выходных данных консоли.</span><span class="sxs-lookup"><span data-stu-id="029d0-131">When the debug engine is ready, you should see ```Debugger listening on port 5858``` in the console output.</span></span>

### <a name="configure-visual-studio-code-to-connect-to-the-remote-device"></a><span data-ttu-id="029d0-132">Настройка Visual Studio Code для подключения к удаленному устройству</span><span class="sxs-lookup"><span data-stu-id="029d0-132">Configure Visual Studio Code to connect to the remote device</span></span>
1. <span data-ttu-id="029d0-133">Откройте панель **Отладка** слева.</span><span class="sxs-lookup"><span data-stu-id="029d0-133">Open the **Debug** panel on the left side.</span></span>
2. <span data-ttu-id="029d0-134">Нажмите зеленую кнопку **Начать отладку** (клавиша F5).</span><span class="sxs-lookup"><span data-stu-id="029d0-134">Click the green **Start Debugging** (F5) button.</span></span> <span data-ttu-id="029d0-135">В Visual Studio Code откроется файл launch.json.</span><span class="sxs-lookup"><span data-stu-id="029d0-135">Visual Studio Code opens a launch.json file.</span></span>
3. <span data-ttu-id="029d0-136">Обновите этот файл с использованием следующего содержимого.</span><span class="sxs-lookup"><span data-stu-id="029d0-136">Update the launch.json file with the following content.</span></span> <span data-ttu-id="029d0-137">Замените `[device hostname or IP address]` на IP-адрес или имя узла самого устройства.</span><span class="sxs-lookup"><span data-stu-id="029d0-137">Replace `[device hostname or IP address]` with the actual device IP address or host name.</span></span>

> [!NOTE]
> <span data-ttu-id="029d0-138">Дополнительные сведения об отладке Visual Studio см. в статье об [отладке в Visual Studio Code](https://code.visualstudio.com/Docs/editor/debugging#_launchjson-attributes).</span><span class="sxs-lookup"><span data-stu-id="029d0-138">To learn more about the Visual Studio Debugging, please refer to [Debugging in Visual Studio Code](https://code.visualstudio.com/Docs/editor/debugging#_launchjson-attributes).</span></span>


```json
{
    "version": "0.2.0",
    "configurations": [
        {
            "name": "Attach",
            "type": "node",
            "request": "attach",
            "port": 5858,
            "address": "[device hostname or IP address]",
            "restart": false,
            "sourceMaps": false,
            "outDir": null,
            "localRoot": "${workspaceRoot}",
            "remoteRoot": null
        }
    ]
}
```

![Конфигурация удаленной отладки](media/iot-hub-raspberry-pi-lessons/troubleshooting/remote_debugging_configuration.png)

### <a name="attach-to-the-remote-application"></a><span data-ttu-id="029d0-140">Присоединение к удаленному приложению</span><span class="sxs-lookup"><span data-stu-id="029d0-140">Attach to the remote application</span></span>
<span data-ttu-id="029d0-141">Нажмите зеленую кнопку **Начать отладку** (клавиша F5), чтобы начать отладку.</span><span class="sxs-lookup"><span data-stu-id="029d0-141">Click the green **Start Debugging** (F5) button to start debugging.</span></span>

<span data-ttu-id="029d0-142">Дополнительные сведения об отладчике см. в статье [JavaScript in VS Code](https://code.visualstudio.com/docs/languages/javascript#_debugging) (JavaScript в VSCode).</span><span class="sxs-lookup"><span data-stu-id="029d0-142">Read [JavaScript in VS Code](https://code.visualstudio.com/docs/languages/javascript#_debugging) to learn more about the debugger.</span></span>

![Интерактивная удаленная отладка](media/iot-hub-raspberry-pi-lessons/troubleshooting/remote_debugging_interactive.png)

## <a name="azure-cli-issues"></a><span data-ttu-id="029d0-144">Проблемы с интерфейсом командной строки Azure</span><span class="sxs-lookup"><span data-stu-id="029d0-144">Azure CLI issues</span></span>
<span data-ttu-id="029d0-145">Интерфейс командной строки Azure (Azure CLI) — это сборка предварительной версии.</span><span class="sxs-lookup"><span data-stu-id="029d0-145">The Azure command-line interface (Azure CLI) is a preview build.</span></span> <span data-ttu-id="029d0-146">Найти решения можно в [руководстве по установке предварительной версии](https://github.com/Azure/azure-cli/blob/master/doc/preview_install_guide.md).</span><span class="sxs-lookup"><span data-stu-id="029d0-146">To seek solutions, you can use the [Preview Install Guide](https://github.com/Azure/azure-cli/blob/master/doc/preview_install_guide.md).</span></span>

<span data-ttu-id="029d0-147">При появлении ошибок в средстве сообщите о [проблеме](https://github.com/Azure/azure-cli/issues) в разделе **Проблемы** репозитория GitHub.</span><span class="sxs-lookup"><span data-stu-id="029d0-147">If you encounter any bugs with the tool, file an [issue](https://github.com/Azure/azure-cli/issues) in the **Issues** section of the GitHub repo.</span></span>

<span data-ttu-id="029d0-148">Справку по устранению распространенных проблем см. в [файле сведений](https://github.com/Azure/azure-cli/blob/master/README.rst).</span><span class="sxs-lookup"><span data-stu-id="029d0-148">For help in troubleshooting common problems, check the [readme](https://github.com/Azure/azure-cli/blob/master/README.rst).</span></span>

## <a name="python-installation-issues"></a><span data-ttu-id="029d0-149">Проблемы с установкой Python</span><span class="sxs-lookup"><span data-stu-id="029d0-149">Python installation issues</span></span>
### <a name="legacy-installation-issues-macos"></a><span data-ttu-id="029d0-150">Проблемы с устаревшими установками (macOS)</span><span class="sxs-lookup"><span data-stu-id="029d0-150">Legacy installation issues (macOS)</span></span>
<span data-ttu-id="029d0-151">При установке pip возникает ошибка разрешения, если есть устаревшие пакеты, которые устанавливаются с использованием разрешений **su**.</span><span class="sxs-lookup"><span data-stu-id="029d0-151">When you're installing pip, a permission error is thrown when older packages are installed with **su** permissions.</span></span> <span data-ttu-id="029d0-152">Такая ситуация возникает из-за того, что предыдущая установка Python с использованием brew (macOS) удалена не полностью.</span><span class="sxs-lookup"><span data-stu-id="029d0-152">This situation occurs because a previous installation of Python using brew (macOS) is not uninstalled completely.</span></span> <span data-ttu-id="029d0-153">Некоторые пакеты pip из предыдущей установки созданы с помощью разрешений корневой папки, что приводит к ошибке разрешения.</span><span class="sxs-lookup"><span data-stu-id="029d0-153">Some pip packages from a previous installation were created by root, which causes the permission error.</span></span> <span data-ttu-id="029d0-154">Чтобы решить эту проблему, необходимо удалить эти пакеты, установленные с помощью разрешений корневой папки.</span><span class="sxs-lookup"><span data-stu-id="029d0-154">The solution is to remove those packages installed by root.</span></span> <span data-ttu-id="029d0-155">Для этого необходимо сделать следующее:</span><span class="sxs-lookup"><span data-stu-id="029d0-155">Use the following steps to complete this task:</span></span>

1. <span data-ttu-id="029d0-156">Перейдите к папке /usr/local/lib/python2.7/site-packages.</span><span class="sxs-lookup"><span data-stu-id="029d0-156">Go to: /usr/local/lib/python2.7/site-packages</span></span>
2. <span data-ttu-id="029d0-157">Выведите список пакетов, созданных с использованием разрешений корневой папки: `ls -l | grep root`.</span><span class="sxs-lookup"><span data-stu-id="029d0-157">List packages created by root: `ls -l | grep root`</span></span>
3. <span data-ttu-id="029d0-158">Удалите пакеты из шага 2: `sudo rm -rf {package name}`.</span><span class="sxs-lookup"><span data-stu-id="029d0-158">Uninstall packages from step 2: `sudo rm -rf {package name}`</span></span>
4. <span data-ttu-id="029d0-159">Переустановите Python.</span><span class="sxs-lookup"><span data-stu-id="029d0-159">Reinstall Python.</span></span>

## <a name="azure-iot-hub-issues"></a><span data-ttu-id="029d0-160">Проблемы с Центром Интернета вещей Azure</span><span class="sxs-lookup"><span data-stu-id="029d0-160">Azure IoT Hub issues</span></span>
<span data-ttu-id="029d0-161">Если Центр Интернета вещей Azure успешно подготовлен с помощью Azure CLI и требуется инструмент для управления устройствами, подключенными к вашему Центру Интернета вещей, воспользуйтесь указанными ниже инструментами.</span><span class="sxs-lookup"><span data-stu-id="029d0-161">If you've successfully provisioned your Azure IoT hub with Azure CLI, and you need a tool to manage the devices that are connecting to your IoT hub, try the following tools.</span></span>

### <a name="device-explorer"></a><span data-ttu-id="029d0-162">Обозреватель устройств</span><span class="sxs-lookup"><span data-stu-id="029d0-162">Device explorer</span></span>
<span data-ttu-id="029d0-163">Инструмент [обозреватель устройств](https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer) работает на локальном компьютере Windows и подключается к Центру Интернета вещей в Azure.</span><span class="sxs-lookup"><span data-stu-id="029d0-163">The [Device explorer](https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer) tool runs on your Windows local machine and connects to your IoT hub in Azure.</span></span> <span data-ttu-id="029d0-164">Он взаимодействует со следующими [конечными точками Центра Интернета вещей](iot-hub-devguide.md):</span><span class="sxs-lookup"><span data-stu-id="029d0-164">It communicates with the following [IoT Hub endpoints](iot-hub-devguide.md):</span></span>


* <span data-ttu-id="029d0-165">*управление удостоверениями устройств* для подготовки устройств, зарегистрированных в Центре Интернета вещей, и управления ими;</span><span class="sxs-lookup"><span data-stu-id="029d0-165">*Device identity management* to provision and manage devices registered with your IoT hub.</span></span>
* <span data-ttu-id="029d0-166">*получение сообщений с устройства в облако*, что позволяет отслеживать сообщения, отправляемые с устройства в Центр Интернета вещей;</span><span class="sxs-lookup"><span data-stu-id="029d0-166">*Receive device-to-cloud* so you can monitor messages sent from your device to your IoT hub.</span></span>
* <span data-ttu-id="029d0-167">*отправка сообщений из облака на устройство*, что позволяет отправлять сообщения на устройства из вашего Центра Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="029d0-167">*Send cloud-to-device* so you can send messages to your devices from your IoT hub.</span></span>

<span data-ttu-id="029d0-168">Настройте свою строку подключения Центра Интернета вещей в этом инструменте, чтобы использовать все его возможности.</span><span class="sxs-lookup"><span data-stu-id="029d0-168">Configure your IoT hub connection string within this tool to use all its capabilities.</span></span>

### <a name="iothub-explorer"></a><span data-ttu-id="029d0-169">iothub-explorer</span><span class="sxs-lookup"><span data-stu-id="029d0-169">iothub-explorer</span></span>
<span data-ttu-id="029d0-170">[iothub-explorer](https://github.com/Azure/iothub-explorer) — это пример мультиплатформенного инструмента интерфейса командной строки для управления устройствами.</span><span class="sxs-lookup"><span data-stu-id="029d0-170">[iothub-explorer](https://github.com/Azure/iothub-explorer) is a sample multiplatform CLI tool to manage devices.</span></span> <span data-ttu-id="029d0-171">Его можно использовать для управления устройствами в реестре удостоверений, мониторинга сообщений, отправляемых с устройства в облако, и отправки сообщений из облака на устройство.</span><span class="sxs-lookup"><span data-stu-id="029d0-171">You can use the tool to manage the devices in the identity registry, monitor device-to-cloud messages, and send cloud-to-device messages.</span></span>

<span data-ttu-id="029d0-172">Чтобы установить последнюю версию (предварительную версию) инструмента iothub-explorer, выполните следующую команду в среде командной строки:</span><span class="sxs-lookup"><span data-stu-id="029d0-172">To install the latest (prerelease) version of the iothub-explorer tool, run the following command in your command-line environment:</span></span>

```bash
npm install -g iothub-explorer@latest
```

<span data-ttu-id="029d0-173">Дополнительную справку о всех командах iothub-explorer и их параметрах можно получить, выполнив следующую команду:</span><span class="sxs-lookup"><span data-stu-id="029d0-173">You can use the following command to get additional help about all the iothub-explorer commands and their parameters:</span></span>

```bash
iothub-explorer help
```

### <a name="azure-portal"></a><span data-ttu-id="029d0-174">Портал Azure</span><span class="sxs-lookup"><span data-stu-id="029d0-174">Azure portal</span></span>
<span data-ttu-id="029d0-175">Все возможности интерфейса командной строки помогают создавать все ресурсы Azure и управлять ими.</span><span class="sxs-lookup"><span data-stu-id="029d0-175">A full CLI experience helps you create and manage all your Azure resources.</span></span> <span data-ttu-id="029d0-176">Для подготовки, отладки ресурсов Azure и управления ими можно также воспользоваться [порталом Azure](../azure-portal-overview.md).</span><span class="sxs-lookup"><span data-stu-id="029d0-176">You might also want to use the [Azure portal](../azure-portal-overview.md) to help provision, manage, and debug your Azure resources.</span></span>

## <a name="azure-storage-issues"></a><span data-ttu-id="029d0-177">Проблемы с хранилищем Azure</span><span class="sxs-lookup"><span data-stu-id="029d0-177">Azure Storage issues</span></span>
<span data-ttu-id="029d0-178">[Обозреватель служб хранилища Microsoft Azure (предварительная версия)](http://storageexplorer.com) — это автономное приложение от корпорации Майкрософт, которое можно использовать для работы с данными из службы хранилища Azure на платформе Windows, macOS и Linux.</span><span class="sxs-lookup"><span data-stu-id="029d0-178">[Microsoft Azure Storage Explorer (preview)](http://storageexplorer.com) is a standalone app from Microsoft that you can use to work with Azure Storage data on Windows, macOS, and Linux.</span></span> <span data-ttu-id="029d0-179">Используя этот инструмент, можно подключаться к таблице и просматривать данные в ней.</span><span class="sxs-lookup"><span data-stu-id="029d0-179">By using this tool, you can connect to your table and see the data in it.</span></span> <span data-ttu-id="029d0-180">Его можно использовать для устранения неполадок в вашей службе хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="029d0-180">You can use this tool to troubleshoot your Azure Storage issues.</span></span>

