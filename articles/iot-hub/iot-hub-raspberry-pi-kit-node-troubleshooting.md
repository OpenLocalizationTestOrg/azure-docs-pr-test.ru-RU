---
title: "Connect Raspberry PI (C) tooAzure IoT — Устранение неполадок | Документы Microsoft"
description: "Устранение неполадок страницы для работы Raspberry Pi Node.js hello"
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
ms.openlocfilehash: 8f0807104550e8e53a132f7741564b33f1db17ea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting"></a><span data-ttu-id="3989a-104">Устранение неполадок</span><span class="sxs-lookup"><span data-stu-id="3989a-104">Troubleshooting</span></span>
## <a name="hardware-issues"></a><span data-ttu-id="3989a-105">Проблемы с оборудованием</span><span class="sxs-lookup"><span data-stu-id="3989a-105">Hardware issues</span></span>
### <a name="hello-application-runs-well-but-hello-led-is-not-blinking"></a><span data-ttu-id="3989a-106">приложение Hello также выполняется, но hello Индикатор мигает. это не</span><span class="sxs-lookup"><span data-stu-id="3989a-106">hello application runs well but hello LED is not blinking</span></span>
<span data-ttu-id="3989a-107">Эта проблема не будет всегда связанные toohardware канала связи.</span><span class="sxs-lookup"><span data-stu-id="3989a-107">This issue is always related toohardware circuit connectivity.</span></span> <span data-ttu-id="3989a-108">Используйте следующие шаги tooidentify проблемы hello.</span><span class="sxs-lookup"><span data-stu-id="3989a-108">Use hello following steps tooidentify problems:</span></span>

1. <span data-ttu-id="3989a-109">Проверьте, что выбран правильный hello **объект групповой ПОЛИТИКИ** на доске.</span><span class="sxs-lookup"><span data-stu-id="3989a-109">Check that you chose hello correct **GPIO** on your board.</span></span> <span data-ttu-id="3989a-110">Hello двух портов должно быть **Земля объект групповой ПОЛИТИКИ (6 ПИН-код)** и **04 объект групповой ПОЛИТИКИ (7 ПИН-код)**.</span><span class="sxs-lookup"><span data-stu-id="3989a-110">hello two ports should be **GPIO GND (Pin 6)** and **GPIO 04 (Pin 7)**.</span></span>
2. <span data-ttu-id="3989a-111">Проверьте правильность полярности hello вашей индикатора.</span><span class="sxs-lookup"><span data-stu-id="3989a-111">Check that hello polarity of your LED is correct.</span></span> <span data-ttu-id="3989a-112">участок больше Hello должно быть указано hello **положительное**, анод ПИН-код.</span><span class="sxs-lookup"><span data-stu-id="3989a-112">hello longer leg should indicate hello **positive**, anode pin.</span></span>
3. <span data-ttu-id="3989a-113">Используйте hello **закрепить 3,3 в** и **Земля ПИН-код** на Pi Raspberry 3.</span><span class="sxs-lookup"><span data-stu-id="3989a-113">Use hello **3.3V Pin** and **GND Pin** on Raspberry Pi 3.</span></span> <span data-ttu-id="3989a-114">Считать Pi hello питания постоянного ТОКА.</span><span class="sxs-lookup"><span data-stu-id="3989a-114">Treat Pi as hello DC power.</span></span> <span data-ttu-id="3989a-115">Убедитесь, что этот Индикатор hello работает нормально.</span><span class="sxs-lookup"><span data-stu-id="3989a-115">Check that hello LED works fine.</span></span>

![Спецификация светодиодного индикатора](media/iot-hub-raspberry-pi-lessons/troubleshooting/led_spec.png)

### <a name="other-hardware-issues"></a><span data-ttu-id="3989a-117">Другие проблемы с оборудованием</span><span class="sxs-lookup"><span data-stu-id="3989a-117">Other hardware issues</span></span>
<span data-ttu-id="3989a-118">Сведения об устранении типичных проблем на Raspberry Pi 3 см. в разделе hello [официальный по устранению неполадок страницы](http://elinux.org/R-Pi_Troubleshooting).</span><span class="sxs-lookup"><span data-stu-id="3989a-118">For information about solving common problems on Raspberry Pi 3, see hello [official troubleshooting page](http://elinux.org/R-Pi_Troubleshooting).</span></span>

## <a name="nodejs-package-issues"></a><span data-ttu-id="3989a-119">Проблемы с пакетами Node.js</span><span class="sxs-lookup"><span data-stu-id="3989a-119">Node.js package issues</span></span>
### <a name="no-response-during-gulp-tasks"></a><span data-ttu-id="3989a-120">Нет ответа при выполнении задач Gulp</span><span class="sxs-lookup"><span data-stu-id="3989a-120">No response during gulp tasks</span></span>
<span data-ttu-id="3989a-121">Если возникли проблемы при выполнении задачи gulp, вы можете добавить hello `--verbose` параметра для отладки.</span><span class="sxs-lookup"><span data-stu-id="3989a-121">If you encounter problems in running gulp tasks, you can add hello `--verbose` option for debugging.</span></span> <span data-ttu-id="3989a-122">Повторите tooterminate текущие задачи gulp, нажав сочетание клавиш Ctrl + C, а затем запустите следующую команду в сообщения отладки toosee окна консоли hello.</span><span class="sxs-lookup"><span data-stu-id="3989a-122">Try tooterminate current gulp tasks by using Ctrl + C, and then run hello following command in your console window toosee debug messages.</span></span> <span data-ttu-id="3989a-123">В выходных данных консоли должны отобразиться подробные сообщения об ошибках.</span><span class="sxs-lookup"><span data-stu-id="3989a-123">You might see detailed error messages in your console output.</span></span>

```bash
gulp --verbose
```

### <a name="device-discovery-issues"></a><span data-ttu-id="3989a-124">Проблемы с обнаружением устройств</span><span class="sxs-lookup"><span data-stu-id="3989a-124">Device discovery issues</span></span>
<span data-ttu-id="3989a-125">Для помощи при устранении типичных проблем с hello `devdisco` команды, проверьте hello [readme](https://github.com/Azure/device-discovery-cli/blob/develop/readme.md).</span><span class="sxs-lookup"><span data-stu-id="3989a-125">For help in troubleshooting common problems with hello `devdisco` command, check hello [readme](https://github.com/Azure/device-discovery-cli/blob/develop/readme.md).</span></span>

### <a name="npm-issues"></a><span data-ttu-id="3989a-126">проблемы с NPM</span><span class="sxs-lookup"><span data-stu-id="3989a-126">npm issues</span></span>
<span data-ttu-id="3989a-127">Попробуйте tooupdate пакета npm с помощью hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="3989a-127">Try tooupdate your npm package by using hello following command:</span></span>

```bash
npm install -g npm
```

<span data-ttu-id="3989a-128">Если hello проблема остается, оставьте комментарий в конце hello в этой статье, или создать вопрос GitHub в нашем [репозитории примеров](https://github.com/Azure-Samples/iot-hub-node-raspberrypi-getting-started).</span><span class="sxs-lookup"><span data-stu-id="3989a-128">If hello problem still exists, leave your comments at hello end of this article or create a GitHub issue in our [sample repository](https://github.com/Azure-Samples/iot-hub-node-raspberrypi-getting-started).</span></span>

## <a name="remote-debugging"></a><span data-ttu-id="3989a-129">Удаленная отладка</span><span class="sxs-lookup"><span data-stu-id="3989a-129">Remote debugging</span></span>
### <a name="run-hello-sample-application-in-debug-mode"></a><span data-ttu-id="3989a-130">Запустить образец приложения hello в режиме отладки</span><span class="sxs-lookup"><span data-stu-id="3989a-130">Run hello sample application in debug mode</span></span>
```bash
gulp run --debug
```

<span data-ttu-id="3989a-131">При готовности модуль отладки hello вы увидите ```Debugger listening on port 5858``` в выходных данных консоли hello.</span><span class="sxs-lookup"><span data-stu-id="3989a-131">When hello debug engine is ready, you should see ```Debugger listening on port 5858``` in hello console output.</span></span>

### <a name="configure-visual-studio-code-tooconnect-toohello-remote-device"></a><span data-ttu-id="3989a-132">Настройка Visual Studio Code tooconnect toohello удаленного устройства</span><span class="sxs-lookup"><span data-stu-id="3989a-132">Configure Visual Studio Code tooconnect toohello remote device</span></span>
1. <span data-ttu-id="3989a-133">Откройте hello **отладки** панели на hello слева.</span><span class="sxs-lookup"><span data-stu-id="3989a-133">Open hello **Debug** panel on hello left side.</span></span>
2. <span data-ttu-id="3989a-134">Щелкните зеленый hello **начать отладку** кнопки (F5).</span><span class="sxs-lookup"><span data-stu-id="3989a-134">Click hello green **Start Debugging** (F5) button.</span></span> <span data-ttu-id="3989a-135">В Visual Studio Code откроется файл launch.json.</span><span class="sxs-lookup"><span data-stu-id="3989a-135">Visual Studio Code opens a launch.json file.</span></span>
3. <span data-ttu-id="3989a-136">Измените файл launch.json hello hello после содержимого.</span><span class="sxs-lookup"><span data-stu-id="3989a-136">Update hello launch.json file with hello following content.</span></span> <span data-ttu-id="3989a-137">Замените `[device hostname or IP address]` с hello само устройство IP адрес или имя узла.</span><span class="sxs-lookup"><span data-stu-id="3989a-137">Replace `[device hostname or IP address]` with hello actual device IP address or host name.</span></span>

> [!NOTE]
> <span data-ttu-id="3989a-138">toolearn Дополнительные сведения о Visual Studio отладка, hello обратитесь слишком[отладки в Visual Studio Code](https://code.visualstudio.com/Docs/editor/debugging#_launchjson-attributes).</span><span class="sxs-lookup"><span data-stu-id="3989a-138">toolearn more about hello Visual Studio Debugging, please refer too[Debugging in Visual Studio Code](https://code.visualstudio.com/Docs/editor/debugging#_launchjson-attributes).</span></span>


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

### <a name="attach-toohello-remote-application"></a><span data-ttu-id="3989a-140">Присоединение удаленного приложения toohello</span><span class="sxs-lookup"><span data-stu-id="3989a-140">Attach toohello remote application</span></span>
<span data-ttu-id="3989a-141">Щелкните зеленый hello **начать отладку** отладки toostart кнопки (F5).</span><span class="sxs-lookup"><span data-stu-id="3989a-141">Click hello green **Start Debugging** (F5) button toostart debugging.</span></span>

<span data-ttu-id="3989a-142">Чтение [JavaScript в VS Code](https://code.visualstudio.com/docs/languages/javascript#_debugging) toolearn Дополнительные сведения об отладчике hello.</span><span class="sxs-lookup"><span data-stu-id="3989a-142">Read [JavaScript in VS Code](https://code.visualstudio.com/docs/languages/javascript#_debugging) toolearn more about hello debugger.</span></span>

![Интерактивная удаленная отладка](media/iot-hub-raspberry-pi-lessons/troubleshooting/remote_debugging_interactive.png)

## <a name="azure-cli-issues"></a><span data-ttu-id="3989a-144">Проблемы с интерфейсом командной строки Azure</span><span class="sxs-lookup"><span data-stu-id="3989a-144">Azure CLI issues</span></span>
<span data-ttu-id="3989a-145">Hello Azure командной строки (CLI Azure) — это построение предварительного просмотра.</span><span class="sxs-lookup"><span data-stu-id="3989a-145">hello Azure command-line interface (Azure CLI) is a preview build.</span></span> <span data-ttu-id="3989a-146">tooseek решений, можно использовать hello [руководство по установке предварительной версии](https://github.com/Azure/azure-cli/blob/master/doc/preview_install_guide.md).</span><span class="sxs-lookup"><span data-stu-id="3989a-146">tooseek solutions, you can use hello [Preview Install Guide](https://github.com/Azure/azure-cli/blob/master/doc/preview_install_guide.md).</span></span>

<span data-ttu-id="3989a-147">При возникновении любых ошибок с помощью средства hello файл [проблема](https://github.com/Azure/azure-cli/issues) в hello **проблемы** раздел hello в репозитории GitHub.</span><span class="sxs-lookup"><span data-stu-id="3989a-147">If you encounter any bugs with hello tool, file an [issue](https://github.com/Azure/azure-cli/issues) in hello **Issues** section of hello GitHub repo.</span></span>

<span data-ttu-id="3989a-148">Для помощи при устранении неполадок проверьте hello [readme](https://github.com/Azure/azure-cli/blob/master/README.rst).</span><span class="sxs-lookup"><span data-stu-id="3989a-148">For help in troubleshooting common problems, check hello [readme](https://github.com/Azure/azure-cli/blob/master/README.rst).</span></span>

## <a name="python-installation-issues"></a><span data-ttu-id="3989a-149">Проблемы с установкой Python</span><span class="sxs-lookup"><span data-stu-id="3989a-149">Python installation issues</span></span>
### <a name="legacy-installation-issues-macos"></a><span data-ttu-id="3989a-150">Проблемы с устаревшими установками (macOS)</span><span class="sxs-lookup"><span data-stu-id="3989a-150">Legacy installation issues (macOS)</span></span>
<span data-ttu-id="3989a-151">При установке pip возникает ошибка разрешения, если есть устаревшие пакеты, которые устанавливаются с использованием разрешений **su**.</span><span class="sxs-lookup"><span data-stu-id="3989a-151">When you're installing pip, a permission error is thrown when older packages are installed with **su** permissions.</span></span> <span data-ttu-id="3989a-152">Такая ситуация возникает из-за того, что предыдущая установка Python с использованием brew (macOS) удалена не полностью.</span><span class="sxs-lookup"><span data-stu-id="3989a-152">This situation occurs because a previous installation of Python using brew (macOS) is not uninstalled completely.</span></span> <span data-ttu-id="3989a-153">Корневым элементом, который приводит к возникновению ошибки разрешение hello были созданы некоторые pip пакеты из предыдущей установки.</span><span class="sxs-lookup"><span data-stu-id="3989a-153">Some pip packages from a previous installation were created by root, which causes hello permission error.</span></span> <span data-ttu-id="3989a-154">Здравствуйте, решение является tooremove эти пакеты, установленные корневым элементом.</span><span class="sxs-lookup"><span data-stu-id="3989a-154">hello solution is tooremove those packages installed by root.</span></span> <span data-ttu-id="3989a-155">Используйте следующие шаги toocomplete hello этой задачи:</span><span class="sxs-lookup"><span data-stu-id="3989a-155">Use hello following steps toocomplete this task:</span></span>

1. <span data-ttu-id="3989a-156">Перейдите к папке /usr/local/lib/python2.7/site-packages.</span><span class="sxs-lookup"><span data-stu-id="3989a-156">Go to: /usr/local/lib/python2.7/site-packages</span></span>
2. <span data-ttu-id="3989a-157">Выведите список пакетов, созданных с использованием разрешений корневой папки: `ls -l | grep root`.</span><span class="sxs-lookup"><span data-stu-id="3989a-157">List packages created by root: `ls -l | grep root`</span></span>
3. <span data-ttu-id="3989a-158">Удалите пакеты из шага 2: `sudo rm -rf {package name}`.</span><span class="sxs-lookup"><span data-stu-id="3989a-158">Uninstall packages from step 2: `sudo rm -rf {package name}`</span></span>
4. <span data-ttu-id="3989a-159">Переустановите Python.</span><span class="sxs-lookup"><span data-stu-id="3989a-159">Reinstall Python.</span></span>

## <a name="azure-iot-hub-issues"></a><span data-ttu-id="3989a-160">Проблемы с Центром Интернета вещей Azure</span><span class="sxs-lookup"><span data-stu-id="3989a-160">Azure IoT Hub issues</span></span>
<span data-ttu-id="3989a-161">Если успешной подготовки ваш центр Azure IoT с помощью Azure CLI, и требуется средство устройств hello toomanage, подключающимися центра IoT tooyour, попробуйте следующие средства hello.</span><span class="sxs-lookup"><span data-stu-id="3989a-161">If you've successfully provisioned your Azure IoT hub with Azure CLI, and you need a tool toomanage hello devices that are connecting tooyour IoT hub, try hello following tools.</span></span>

### <a name="device-explorer"></a><span data-ttu-id="3989a-162">Обозреватель устройств</span><span class="sxs-lookup"><span data-stu-id="3989a-162">Device explorer</span></span>
<span data-ttu-id="3989a-163">Hello [обозреватель устройств](https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer) средство выполняется на локальном компьютере Windows и подключается tooyour центр IoT в Azure.</span><span class="sxs-lookup"><span data-stu-id="3989a-163">hello [Device explorer](https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer) tool runs on your Windows local machine and connects tooyour IoT hub in Azure.</span></span> <span data-ttu-id="3989a-164">Он взаимодействует с hello следующие [конечные точки центра IoT](iot-hub-devguide.md):</span><span class="sxs-lookup"><span data-stu-id="3989a-164">It communicates with hello following [IoT Hub endpoints](iot-hub-devguide.md):</span></span>


* <span data-ttu-id="3989a-165">*Управление устройствами удостоверения* tooprovision и управления ими устройствах, зарегистрированных в центр IoT.</span><span class="sxs-lookup"><span data-stu-id="3989a-165">*Device identity management* tooprovision and manage devices registered with your IoT hub.</span></span>
* <span data-ttu-id="3989a-166">*Получение устройства в облако* можно наблюдать за сообщений, отправленных из центра IoT tooyour вашего устройства.</span><span class="sxs-lookup"><span data-stu-id="3989a-166">*Receive device-to-cloud* so you can monitor messages sent from your device tooyour IoT hub.</span></span>
* <span data-ttu-id="3989a-167">*Отправить облака на устройство* для отправки сообщений tooyour устройств из вашего центра IoT.</span><span class="sxs-lookup"><span data-stu-id="3989a-167">*Send cloud-to-device* so you can send messages tooyour devices from your IoT hub.</span></span>

<span data-ttu-id="3989a-168">Настройка строки подключения концентратора IoT в этот инструмент toouse его возможности.</span><span class="sxs-lookup"><span data-stu-id="3989a-168">Configure your IoT hub connection string within this tool toouse all its capabilities.</span></span>

### <a name="iothub-explorer"></a><span data-ttu-id="3989a-169">iothub-explorer</span><span class="sxs-lookup"><span data-stu-id="3989a-169">iothub-explorer</span></span>
<span data-ttu-id="3989a-170">[обозреватель центром IOT](https://github.com/Azure/iothub-explorer) -это средство многоплатформенного CLI образец toomanage устройств.</span><span class="sxs-lookup"><span data-stu-id="3989a-170">[iothub-explorer](https://github.com/Azure/iothub-explorer) is a sample multiplatform CLI tool toomanage devices.</span></span> <span data-ttu-id="3989a-171">Можно использовать hello средство toomanage hello устройства в реестре удостоверений hello, отслеживать сообщения из устройства в облако и отправки сообщений облака на устройство.</span><span class="sxs-lookup"><span data-stu-id="3989a-171">You can use hello tool toomanage hello devices in hello identity registry, monitor device-to-cloud messages, and send cloud-to-device messages.</span></span>

<span data-ttu-id="3989a-172">tooinstall hello последняя (Предварительная) версия hello центром IOT-анализатор, запустите следующую команду в среде командной строки hello:</span><span class="sxs-lookup"><span data-stu-id="3989a-172">tooinstall hello latest (prerelease) version of hello iothub-explorer tool, run hello following command in your command-line environment:</span></span>

```bash
npm install -g iothub-explorer@latest
```

<span data-ttu-id="3989a-173">Можно использовать следующую команду, tooget дополнительную справку обо всех hello центром IOT обозреватель команды и их параметрах hello.</span><span class="sxs-lookup"><span data-stu-id="3989a-173">You can use hello following command tooget additional help about all hello iothub-explorer commands and their parameters:</span></span>

```bash
iothub-explorer help
```

### <a name="azure-portal"></a><span data-ttu-id="3989a-174">Портал Azure</span><span class="sxs-lookup"><span data-stu-id="3989a-174">Azure portal</span></span>
<span data-ttu-id="3989a-175">Все возможности интерфейса командной строки помогают создавать все ресурсы Azure и управлять ими.</span><span class="sxs-lookup"><span data-stu-id="3989a-175">A full CLI experience helps you create and manage all your Azure resources.</span></span> <span data-ttu-id="3989a-176">Можно также toouse hello [портал Azure](../azure-portal-overview.md) toohelp подготовки, управления и отладки ресурсам Azure.</span><span class="sxs-lookup"><span data-stu-id="3989a-176">You might also want toouse hello [Azure portal](../azure-portal-overview.md) toohelp provision, manage, and debug your Azure resources.</span></span>

## <a name="azure-storage-issues"></a><span data-ttu-id="3989a-177">Проблемы с хранилищем Azure</span><span class="sxs-lookup"><span data-stu-id="3989a-177">Azure Storage issues</span></span>
<span data-ttu-id="3989a-178">[Обозреватель хранилищ Microsoft Azure (Предварительная версия)](http://storageexplorer.com) имеет отдельное приложение от Майкрософт, можно использовать toowork с данных из хранилища Azure в Windows, macOS и Linux.</span><span class="sxs-lookup"><span data-stu-id="3989a-178">[Microsoft Azure Storage Explorer (preview)](http://storageexplorer.com) is a standalone app from Microsoft that you can use toowork with Azure Storage data on Windows, macOS, and Linux.</span></span> <span data-ttu-id="3989a-179">С ее помощью можно подключиться tooyour таблицы и просмотра данных hello.</span><span class="sxs-lookup"><span data-stu-id="3989a-179">By using this tool, you can connect tooyour table and see hello data in it.</span></span> <span data-ttu-id="3989a-180">Можно использовать этот инструмент tootroubleshoot вашей проблемы хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="3989a-180">You can use this tool tootroubleshoot your Azure Storage issues.</span></span>

