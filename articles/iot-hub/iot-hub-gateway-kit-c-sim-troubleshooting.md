---
title: "Приступая к работе с имитацией устройства и шлюзом Azure IoT. Устранение неполадок | Документация Майкрософт"
description: "Страница со сведениями об устранении неполадок для шлюза Intel NUC"
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "неполадки Интернета вещей, проблемы Интернета вещей"
ROBOTS: NOINDEX
ms.assetid: 3ee8f4b0-5799-40a3-8cf0-8d5aa44dbc2b
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: cc7add6273e66aadeca9a4915a44f5edf61a0a59
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting"></a><span data-ttu-id="056ce-104">Устранение неполадок</span><span class="sxs-lookup"><span data-stu-id="056ce-104">Troubleshooting</span></span>

## <a name="hardware-issues"></a><span data-ttu-id="056ce-105">Проблемы с оборудованием</span><span class="sxs-lookup"><span data-stu-id="056ce-105">Hardware issues</span></span>

### <a name="ti-sensortag-cannot-be-connected"></a><span data-ttu-id="056ce-106">Не удается подключить TI SensorTag</span><span class="sxs-lookup"><span data-stu-id="056ce-106">TI SensorTag cannot be connected</span></span>

<span data-ttu-id="056ce-107">проблемы с подключением SensorTag tootroubleshoot, использовать hello [SensorTag приложения](http://processors.wiki.ti.com/index.php/SensorTag_User_Guide#SensorTag_App_user_guide).</span><span class="sxs-lookup"><span data-stu-id="056ce-107">tootroubleshoot SensorTag connectivity issues, use hello [SensorTag app](http://processors.wiki.ti.com/index.php/SensorTag_User_Guide#SensorTag_App_user_guide).</span></span>

### <a name="have-an-issue-with-intel-nuc"></a><span data-ttu-id="056ce-108">Проблема с Intel NUC</span><span class="sxs-lookup"><span data-stu-id="056ce-108">Have an issue with Intel NUC</span></span>

<span data-ttu-id="056ce-109">ошибки при загрузке tootroubleshoot, см. слишком[устранения неполадок без загрузки на Intel NUC](http://www.intel.com/content/www/us/en/support/boards-and-kits/000005845.html).</span><span class="sxs-lookup"><span data-stu-id="056ce-109">tootroubleshoot boot issues, refer too[troubleshooting No Boot Issues on Intel NUC](http://www.intel.com/content/www/us/en/support/boards-and-kits/000005845.html).</span></span>

<span data-ttu-id="056ce-110">tootroubleshoot проблемы операционной системы, см. слишком[Устранение неполадок операционной системы на Intel NUC](http://www.intel.com/content/www/us/en/support/boards-and-kits/000006018.html).</span><span class="sxs-lookup"><span data-stu-id="056ce-110">tootroubleshoot operating system issues, refer too[troubleshooting Operating System Issues on Intel NUC](http://www.intel.com/content/www/us/en/support/boards-and-kits/000006018.html).</span></span>

<span data-ttu-id="056ce-111">tootroubleshoot слишком ссылаются другие проблемы[Blink коды и звуковой сигнал для Intel NUC](http://www.intel.com/content/www/us/en/support/boards-and-kits/intel-nuc-boards/000005854.html).</span><span class="sxs-lookup"><span data-stu-id="056ce-111">tootroubleshoot other issues, refer too[Blink Codes and Beep Codes for Intel NUC](http://www.intel.com/content/www/us/en/support/boards-and-kits/intel-nuc-boards/000005854.html).</span></span>

## <a name="nodejs-package-issues"></a><span data-ttu-id="056ce-112">Проблемы с пакетами Node.js</span><span class="sxs-lookup"><span data-stu-id="056ce-112">Node.js package issues</span></span>

### <a name="no-response-during-gulp-tasks"></a><span data-ttu-id="056ce-113">Нет ответа при выполнении задач Gulp</span><span class="sxs-lookup"><span data-stu-id="056ce-113">No response during gulp tasks</span></span>

<span data-ttu-id="056ce-114">Если возникли проблемы при выполнении задачи gulp, вы можете добавить hello `--verbose` параметра для отладки.</span><span class="sxs-lookup"><span data-stu-id="056ce-114">If you encounter problems in running gulp tasks, you can add hello `--verbose` option for debugging.</span></span> <span data-ttu-id="056ce-115">Повторите tooterminate текущие задачи gulp с помощью `Ctrl + C`, а затем выполнения hello следующую команду в сообщения отладки toosee окна консоли.</span><span class="sxs-lookup"><span data-stu-id="056ce-115">Try tooterminate current gulp tasks by using `Ctrl + C`, and then run hello following command in your console window toosee debug messages.</span></span> <span data-ttu-id="056ce-116">В выходных данных консоли должны отобразиться подробные сообщения об ошибках.</span><span class="sxs-lookup"><span data-stu-id="056ce-116">You might see detailed error messages in your console output.</span></span>

```bash
gulp --verbose
```

### <a name="device-discovery-issues"></a><span data-ttu-id="056ce-117">Проблемы с обнаружением устройств</span><span class="sxs-lookup"><span data-stu-id="056ce-117">Device discovery issues</span></span>

<span data-ttu-id="056ce-118">Для помощи при устранении типичных проблем с hello `discover-sensortag` команды, проверьте hello [вики-странице](https://wiki.archlinux.org/index.php/bluetooth#Bluetoothctl).</span><span class="sxs-lookup"><span data-stu-id="056ce-118">For help in troubleshooting common problems with hello `discover-sensortag` command, check hello [wiki page](https://wiki.archlinux.org/index.php/bluetooth#Bluetoothctl).</span></span>

### <a name="npm-issues"></a><span data-ttu-id="056ce-119">проблемы с NPM</span><span class="sxs-lookup"><span data-stu-id="056ce-119">npm issues</span></span>

<span data-ttu-id="056ce-120">Попробуйте tooupdate пакета npm, выполнив следующую команду hello.</span><span class="sxs-lookup"><span data-stu-id="056ce-120">Try tooupdate your npm package by running hello following command:</span></span>

```bash
npm install -g npm
```

<span data-ttu-id="056ce-121">Если hello проблема остается, оставьте комментарий в конце hello в этой статье, или создать вопрос GitHub в нашем [репозитории примеров](https://github.com/azure-samples/iot-hub-c-intel-nuc-gateway-getting-started).</span><span class="sxs-lookup"><span data-stu-id="056ce-121">If hello problem still exists, leave your comments at hello end of this article or create a GitHub issue in our [sample repository](https://github.com/azure-samples/iot-hub-c-intel-nuc-gateway-getting-started).</span></span>

## <a name="remote-debugging"></a><span data-ttu-id="056ce-122">Удаленная отладка</span><span class="sxs-lookup"><span data-stu-id="056ce-122">Remote Debugging</span></span>
> <span data-ttu-id="056ce-123">Приведенные ниже инструкции предназначены для отладки сценариев Node.js, используемых в этом руководстве.</span><span class="sxs-lookup"><span data-stu-id="056ce-123">Below instructions are meant for debugging node.js scripts used in this tutorial.</span></span>
### <a name="run-hello-sample-application-in-debug-mode"></a><span data-ttu-id="056ce-124">Запустить образец приложения hello в режиме отладки</span><span class="sxs-lookup"><span data-stu-id="056ce-124">Run hello sample application in debug mode</span></span>

<span data-ttu-id="056ce-125">Выполните пример приложения hello в режиме отладки, запустив hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="056ce-125">Run hello sample application in debug mode by running hello following command:</span></span>

```bash
gulp run --debug
```

<span data-ttu-id="056ce-126">При готовности модуль отладки hello вы увидите `Debugger listening on port 5858` в выходных данных консоли hello.</span><span class="sxs-lookup"><span data-stu-id="056ce-126">When hello debug engine is ready, you should see `Debugger listening on port 5858` in hello console output.</span></span>

### <a name="configure-visual-studio-code-tooconnect-toohello-remote-device"></a><span data-ttu-id="056ce-127">Настройка Visual Studio Code tooconnect toohello удаленного устройства</span><span class="sxs-lookup"><span data-stu-id="056ce-127">Configure Visual Studio Code tooconnect toohello remote device</span></span>

1. <span data-ttu-id="056ce-128">Откройте hello **отладки** панели на hello слева.</span><span class="sxs-lookup"><span data-stu-id="056ce-128">Open hello **Debug** panel on hello left side.</span></span>
2. <span data-ttu-id="056ce-129">Щелкните зеленый hello **начать отладку** кнопки (F5).</span><span class="sxs-lookup"><span data-stu-id="056ce-129">Click hello green **Start Debugging** (F5) button.</span></span> <span data-ttu-id="056ce-130">В Visual Studio Code откроется файл `launch.json`.</span><span class="sxs-lookup"><span data-stu-id="056ce-130">Visual Studio Code opens a `launch.json` file.</span></span>
3. <span data-ttu-id="056ce-131">Обновление hello `launch.json` файл с hello после содержимого.</span><span class="sxs-lookup"><span data-stu-id="056ce-131">Update hello `launch.json` file with hello following content.</span></span> <span data-ttu-id="056ce-132">Замените `[device hostname or IP address]` с hello само устройство IP адрес или имя узла.</span><span class="sxs-lookup"><span data-stu-id="056ce-132">Replace `[device hostname or IP address]` with hello actual device IP address or host name.</span></span>

   ``` json
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
            "remoteRoot": "~/ble_sample"
        }
     ]
   }
   ```

![Конфигурация удаленной отладки](./media/iot-hub-gateway-kit-lessons/troubleshooting/remote_debugging_configuration.png)

### <a name="attach-toohello-remote-application"></a><span data-ttu-id="056ce-134">Присоединение удаленного приложения toohello</span><span class="sxs-lookup"><span data-stu-id="056ce-134">Attach toohello remote application</span></span>

<span data-ttu-id="056ce-135">Щелкните зеленый hello **начать отладку** отладки toostart кнопки (F5).</span><span class="sxs-lookup"><span data-stu-id="056ce-135">Click hello green **Start Debugging** (F5) button toostart debugging.</span></span>

<span data-ttu-id="056ce-136">Чтение [JavaScript в VS Code](https://code.visualstudio.com/docs/languages/javascript#_debugging) toolearn Дополнительные сведения об отладчике hello.</span><span class="sxs-lookup"><span data-stu-id="056ce-136">Read [JavaScript in VS Code](https://code.visualstudio.com/docs/languages/javascript#_debugging) toolearn more about hello debugger.</span></span>

![Отладка примера BLE](./media/iot-hub-gateway-kit-lessons/troubleshooting/debugging_ble_sample.png)

## <a name="azure-cli-issues"></a><span data-ttu-id="056ce-138">Проблемы с интерфейсом командной строки Azure</span><span class="sxs-lookup"><span data-stu-id="056ce-138">Azure CLI issues</span></span>

<span data-ttu-id="056ce-139">Hello Azure командной строки (CLI Azure) — это построение предварительного просмотра.</span><span class="sxs-lookup"><span data-stu-id="056ce-139">hello Azure command-line interface (Azure CLI) is a preview build.</span></span> <span data-ttu-id="056ce-140">tooseek решений, можно использовать hello [руководство по установке предварительной версии](https://github.com/Azure/azure-cli/blob/master/doc/preview_install_guide.md).</span><span class="sxs-lookup"><span data-stu-id="056ce-140">tooseek solutions, you can use hello [Preview Install Guide](https://github.com/Azure/azure-cli/blob/master/doc/preview_install_guide.md).</span></span>

<span data-ttu-id="056ce-141">При возникновении любых ошибок с помощью средства hello файл [проблема](https://github.com/Azure/azure-cli/issues) в hello **проблемы** раздел hello в репозитории GitHub.</span><span class="sxs-lookup"><span data-stu-id="056ce-141">If you encounter any bugs with hello tool, file an [issue](https://github.com/Azure/azure-cli/issues) in hello **Issues** section of hello GitHub repo.</span></span>

<span data-ttu-id="056ce-142">Для помощи при устранении неполадок проверьте hello [readme](https://github.com/Azure/azure-cli/blob/master/README.rst).</span><span class="sxs-lookup"><span data-stu-id="056ce-142">For help in troubleshooting common problems, check hello [readme](https://github.com/Azure/azure-cli/blob/master/README.rst).</span></span>

<span data-ttu-id="056ce-143">Если соблюдаются «Не удалось найти версию, которая соответствует требованиям hello», проверьте выполнения hello следующая команда tooupgrade pip toolastest версии.</span><span class="sxs-lookup"><span data-stu-id="056ce-143">If you meet "Could not find a version that satisfies hello requirement", please run hello following command tooupgrade pip toolastest version.</span></span>

```bash
python -m pip install --upgrade pip
```

## <a name="python-installation-issues"></a><span data-ttu-id="056ce-144">Проблемы с установкой Python</span><span class="sxs-lookup"><span data-stu-id="056ce-144">Python installation issues</span></span>

### <a name="legacy-installation-issues-macos"></a><span data-ttu-id="056ce-145">Проблемы с устаревшими установками (macOS)</span><span class="sxs-lookup"><span data-stu-id="056ce-145">Legacy installation issues (macOS)</span></span>

<span data-ttu-id="056ce-146">При установке pip возникает ошибка разрешения, если есть устаревшие пакеты, которые устанавливаются с использованием разрешений **su**.</span><span class="sxs-lookup"><span data-stu-id="056ce-146">When you're installing pip, a permission error is thrown when older packages are installed with **su** permissions.</span></span> <span data-ttu-id="056ce-147">Такая ситуация возникает из-за того, что предыдущая установка Python с использованием brew (macOS) удалена не полностью.</span><span class="sxs-lookup"><span data-stu-id="056ce-147">This situation occurs because a previous installation of Python using brew (macOS) is not uninstalled completely.</span></span> <span data-ttu-id="056ce-148">Корневым элементом, который приводит к возникновению ошибки разрешение hello были созданы некоторые pip пакеты из предыдущей установки.</span><span class="sxs-lookup"><span data-stu-id="056ce-148">Some pip packages from a previous installation were created by root, which causes hello permission error.</span></span> <span data-ttu-id="056ce-149">Здравствуйте, решение является tooremove эти пакеты, установленные корневым элементом.</span><span class="sxs-lookup"><span data-stu-id="056ce-149">hello solution is tooremove those packages installed by root.</span></span> <span data-ttu-id="056ce-150">Используйте следующие шаги toocomplete hello этой задачи:</span><span class="sxs-lookup"><span data-stu-id="056ce-150">Use hello following steps toocomplete this task:</span></span>

1. <span data-ttu-id="056ce-151">Go слишком`/usr/local/lib/python2.7/site-packages`</span><span class="sxs-lookup"><span data-stu-id="056ce-151">Go too`/usr/local/lib/python2.7/site-packages`</span></span>
2. <span data-ttu-id="056ce-152">Выведите список пакетов, созданных с использованием разрешений корневой папки: `ls -l | grep root`.</span><span class="sxs-lookup"><span data-stu-id="056ce-152">List packages created by root: `ls -l | grep root`</span></span>
3. <span data-ttu-id="056ce-153">Удалите пакеты из шага 2: `sudo rm -rf {package name}`.</span><span class="sxs-lookup"><span data-stu-id="056ce-153">Uninstall packages from step 2: `sudo rm -rf {package name}`</span></span>
4. <span data-ttu-id="056ce-154">Переустановите Python.</span><span class="sxs-lookup"><span data-stu-id="056ce-154">Reinstall Python.</span></span>

## <a name="azure-iot-hub-issues"></a><span data-ttu-id="056ce-155">Проблемы с Центром Интернета вещей Azure</span><span class="sxs-lookup"><span data-stu-id="056ce-155">Azure IoT Hub issues</span></span>

<span data-ttu-id="056ce-156">Если успешной подготовки ваш центр Azure IoT с hello Azure CLI, и требуется средство устройств hello toomanage, подключающимися центра IoT tooyour, попробуйте следующие средства hello.</span><span class="sxs-lookup"><span data-stu-id="056ce-156">If you've successfully provisioned your Azure IoT hub with hello Azure CLI, and you need a tool toomanage hello devices that are connecting tooyour IoT hub, try hello following tools.</span></span>

### <a name="device-explorer"></a><span data-ttu-id="056ce-157">Обозреватель устройств</span><span class="sxs-lookup"><span data-stu-id="056ce-157">Device Explorer</span></span>

<span data-ttu-id="056ce-158">[Обозреватель устройств](https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer) выполняется на локальном компьютере Windows и подключается tooyour центр IoT в Azure.</span><span class="sxs-lookup"><span data-stu-id="056ce-158">[Device Explorer](https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer) runs on your Windows local machine and connects tooyour IoT hub in Azure.</span></span> <span data-ttu-id="056ce-159">Он взаимодействует с hello следующие [конечные точки центра IoT](https://azure.microsoft.com/en-us/documentation/articles/iot-hub-devguide/):</span><span class="sxs-lookup"><span data-stu-id="056ce-159">It communicates with hello following [IoT Hub endpoints](https://azure.microsoft.com/en-us/documentation/articles/iot-hub-devguide/):</span></span>

- <span data-ttu-id="056ce-160">Tooprovision управления удостоверения устройства и управлять ими устройствах, зарегистрированных в центр IoT.</span><span class="sxs-lookup"><span data-stu-id="056ce-160">Device identity management tooprovision and manage devices registered with your IoT hub.</span></span>
- <span data-ttu-id="056ce-161">Получают устройства в облако, поэтому можно отслеживать сообщения, отправляемые из центра IoT tooyour вашего устройства.</span><span class="sxs-lookup"><span data-stu-id="056ce-161">Receive device-to-cloud so you can monitor messages sent from your device tooyour IoT hub.</span></span>
- <span data-ttu-id="056ce-162">Отправьте облака на устройство, чтобы сообщения можно отправлять tooyour устройств из вашего центра IoT.</span><span class="sxs-lookup"><span data-stu-id="056ce-162">Send cloud-to-device so you can send messages tooyour devices from your IoT hub.</span></span>

<span data-ttu-id="056ce-163">Настройка строки подключения концентратора IoT в этот инструмент toouse его возможности.</span><span class="sxs-lookup"><span data-stu-id="056ce-163">Configure your IoT hub connection string within this tool toouse all its capabilities.</span></span>

### <a name="iothub-explorer"></a><span data-ttu-id="056ce-164">iothub-explorer</span><span class="sxs-lookup"><span data-stu-id="056ce-164">iothub-explorer</span></span>

<span data-ttu-id="056ce-165">[обозреватель центром IOT](https://github.com/Azure/iothub-explorer) -это средство многоплатформенного CLI образец toomanage клиентов устройств.</span><span class="sxs-lookup"><span data-stu-id="056ce-165">[iothub-explorer](https://github.com/Azure/iothub-explorer) is a sample multiplatform CLI tool toomanage device clients.</span></span> <span data-ttu-id="056ce-166">Можно использовать hello средство toomanage hello устройства в реестре удостоверений hello, отслеживать сообщения из устройства в облако и отправлять команды облака на устройство.</span><span class="sxs-lookup"><span data-stu-id="056ce-166">You can use hello tool toomanage hello devices in hello identity registry, monitor device-to-cloud messages, and send cloud-to-device commands.</span></span>

<span data-ttu-id="056ce-167">tooinstall hello последняя (Предварительная) версия средства обозревателя центром IOT hello, запустите следующую команду hello:</span><span class="sxs-lookup"><span data-stu-id="056ce-167">tooinstall hello latest (prerelease) version of hello iothub-explorer tool, run hello following command:</span></span>

```bash
npm install -g iothub-explorer@latest
```

<span data-ttu-id="056ce-168">дополнительную справку tooget обо всех hello центром IOT обозреватель команды и их параметрах, запустите hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="056ce-168">tooget additional help about all hello iothub-explorer commands and their parameters, run hello following command:</span></span>

```bash
iothub-explorer help
```

### <a name="hello-azure-portal"></a><span data-ttu-id="056ce-169">Hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="056ce-169">hello Azure portal</span></span>

<span data-ttu-id="056ce-170">Все возможности интерфейса командной строки помогают создавать все ресурсы Azure и управлять ими.</span><span class="sxs-lookup"><span data-stu-id="056ce-170">A full CLI experience helps you create and manage all your Azure resources.</span></span> <span data-ttu-id="056ce-171">Можно также toouse hello [портал Azure](https://azure.microsoft.com/en-us/documentation/articles/azure-portal-overview/) toohelp подготовки, управления и отладки ресурсам Azure.</span><span class="sxs-lookup"><span data-stu-id="056ce-171">You might also want toouse hello [Azure portal](https://azure.microsoft.com/en-us/documentation/articles/azure-portal-overview/) toohelp provision, manage, and debug your Azure resources.</span></span>

## <a name="azure-storage-issues"></a><span data-ttu-id="056ce-172">Проблемы с хранилищем Azure</span><span class="sxs-lookup"><span data-stu-id="056ce-172">Azure Storage issues</span></span>

<span data-ttu-id="056ce-173">[Обозреватель хранилищ Microsoft Azure (Предварительная версия)](http://storageexplorer.com/) имеет отдельное приложение от Майкрософт, можно использовать toowork с данных из хранилища Azure в Windows, macOS и Linux.</span><span class="sxs-lookup"><span data-stu-id="056ce-173">[Microsoft Azure Storage Explorer (preview)](http://storageexplorer.com/) is a standalone app from Microsoft that you can use toowork with Azure Storage data on Windows, macOS, and Linux.</span></span> <span data-ttu-id="056ce-174">С ее помощью можно подключиться tooyour таблицы и просмотра данных hello.</span><span class="sxs-lookup"><span data-stu-id="056ce-174">By using this tool, you can connect tooyour table and see hello data in it.</span></span> <span data-ttu-id="056ce-175">Можно использовать этот инструмент tootroubleshoot вашей проблемы хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="056ce-175">You can use this tool tootroubleshoot your Azure Storage issues.</span></span>
