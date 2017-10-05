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
ms.openlocfilehash: eae4c112accaefa8bd1bf85f7b43badc2f491dfd
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="troubleshooting"></a><span data-ttu-id="d7de7-104">Устранение неполадок</span><span class="sxs-lookup"><span data-stu-id="d7de7-104">Troubleshooting</span></span>

## <a name="hardware-issues"></a><span data-ttu-id="d7de7-105">Проблемы с оборудованием</span><span class="sxs-lookup"><span data-stu-id="d7de7-105">Hardware issues</span></span>

### <a name="ti-sensortag-cannot-be-connected"></a><span data-ttu-id="d7de7-106">Не удается подключить TI SensorTag</span><span class="sxs-lookup"><span data-stu-id="d7de7-106">TI SensorTag cannot be connected</span></span>

<span data-ttu-id="d7de7-107">Чтобы устранить проблемы с подключением SensorTag, воспользуйтесь [приложением SensorTag](http://processors.wiki.ti.com/index.php/SensorTag_User_Guide#SensorTag_App_user_guide).</span><span class="sxs-lookup"><span data-stu-id="d7de7-107">To troubleshoot SensorTag connectivity issues, use the [SensorTag app](http://processors.wiki.ti.com/index.php/SensorTag_User_Guide#SensorTag_App_user_guide).</span></span>

### <a name="have-an-issue-with-intel-nuc"></a><span data-ttu-id="d7de7-108">Проблема с Intel NUC</span><span class="sxs-lookup"><span data-stu-id="d7de7-108">Have an issue with Intel NUC</span></span>

<span data-ttu-id="d7de7-109">Сведения об устранении проблем при загрузке в Intel NUC см. [на этой странице](http://www.intel.com/content/www/us/en/support/boards-and-kits/000005845.html).</span><span class="sxs-lookup"><span data-stu-id="d7de7-109">To troubleshoot boot issues, refer to [troubleshooting No Boot Issues on Intel NUC](http://www.intel.com/content/www/us/en/support/boards-and-kits/000005845.html).</span></span>

<span data-ttu-id="d7de7-110">Сведения об устранении проблем с операционной системой в Intel NUC см. [на этой странице](http://www.intel.com/content/www/us/en/support/boards-and-kits/000006018.html).</span><span class="sxs-lookup"><span data-stu-id="d7de7-110">To troubleshoot operating system issues, refer to [troubleshooting Operating System Issues on Intel NUC](http://www.intel.com/content/www/us/en/support/boards-and-kits/000006018.html).</span></span>

<span data-ttu-id="d7de7-111">Сведения об устранении других проблем см. в статье [Blink Codes and Beep Codes for Intel NUC](http://www.intel.com/content/www/us/en/support/boards-and-kits/intel-nuc-boards/000005854.html) (Коды включения индикатора и звуковые сигналы для Intel NUC).</span><span class="sxs-lookup"><span data-stu-id="d7de7-111">To troubleshoot other issues, refer to [Blink Codes and Beep Codes for Intel NUC](http://www.intel.com/content/www/us/en/support/boards-and-kits/intel-nuc-boards/000005854.html).</span></span>

## <a name="nodejs-package-issues"></a><span data-ttu-id="d7de7-112">Проблемы с пакетами Node.js</span><span class="sxs-lookup"><span data-stu-id="d7de7-112">Node.js package issues</span></span>

### <a name="no-response-during-gulp-tasks"></a><span data-ttu-id="d7de7-113">Нет ответа при выполнении задач Gulp</span><span class="sxs-lookup"><span data-stu-id="d7de7-113">No response during gulp tasks</span></span>

<span data-ttu-id="d7de7-114">Если при выполнении задач Gulp возникли проблемы, можно добавить параметр `--verbose` для отладки.</span><span class="sxs-lookup"><span data-stu-id="d7de7-114">If you encounter problems in running gulp tasks, you can add the `--verbose` option for debugging.</span></span> <span data-ttu-id="d7de7-115">Попробуйте завершить текущие задачи Gulp, используя клавиши `Ctrl + C`, а затем выполните следующую команду в окне консоли, чтобы просмотреть сообщения отладки.</span><span class="sxs-lookup"><span data-stu-id="d7de7-115">Try to terminate current gulp tasks by using `Ctrl + C`, and then run the following command in your console window to see debug messages.</span></span> <span data-ttu-id="d7de7-116">В выходных данных консоли должны отобразиться подробные сообщения об ошибках.</span><span class="sxs-lookup"><span data-stu-id="d7de7-116">You might see detailed error messages in your console output.</span></span>

```bash
gulp --verbose
```

### <a name="device-discovery-issues"></a><span data-ttu-id="d7de7-117">Проблемы с обнаружением устройств</span><span class="sxs-lookup"><span data-stu-id="d7de7-117">Device discovery issues</span></span>

<span data-ttu-id="d7de7-118">Справку по устранению распространенных проблем с помощью команды `discover-sensortag` см. на [вики-странице](https://wiki.archlinux.org/index.php/bluetooth#Bluetoothctl).</span><span class="sxs-lookup"><span data-stu-id="d7de7-118">For help in troubleshooting common problems with the `discover-sensortag` command, check the [wiki page](https://wiki.archlinux.org/index.php/bluetooth#Bluetoothctl).</span></span>

### <a name="npm-issues"></a><span data-ttu-id="d7de7-119">проблемы с NPM</span><span class="sxs-lookup"><span data-stu-id="d7de7-119">npm issues</span></span>

<span data-ttu-id="d7de7-120">Попробуйте обновить пакет NPM, выполнив следующую команду:</span><span class="sxs-lookup"><span data-stu-id="d7de7-120">Try to update your npm package by running the following command:</span></span>

```bash
npm install -g npm
```

<span data-ttu-id="d7de7-121">Если проблема не исчезла, оставьте комментарии в конце этой статьи или задайте вопрос о проблеме в GitHub в нашем [примере репозитория](https://github.com/azure-samples/iot-hub-c-intel-nuc-gateway-getting-started).</span><span class="sxs-lookup"><span data-stu-id="d7de7-121">If the problem still exists, leave your comments at the end of this article or create a GitHub issue in our [sample repository](https://github.com/azure-samples/iot-hub-c-intel-nuc-gateway-getting-started).</span></span>

## <a name="remote-debugging"></a><span data-ttu-id="d7de7-122">Удаленная отладка</span><span class="sxs-lookup"><span data-stu-id="d7de7-122">Remote Debugging</span></span>
> <span data-ttu-id="d7de7-123">Приведенные ниже инструкции предназначены для отладки сценариев Node.js, используемых в этом руководстве.</span><span class="sxs-lookup"><span data-stu-id="d7de7-123">Below instructions are meant for debugging node.js scripts used in this tutorial.</span></span>
### <a name="run-the-sample-application-in-debug-mode"></a><span data-ttu-id="d7de7-124">Запуск примера приложения в режиме отладки</span><span class="sxs-lookup"><span data-stu-id="d7de7-124">Run the sample application in debug mode</span></span>

<span data-ttu-id="d7de7-125">Запустите пример приложения в режиме отладки, выполнив следующую команду:</span><span class="sxs-lookup"><span data-stu-id="d7de7-125">Run the sample application in debug mode by running the following command:</span></span>

```bash
gulp run --debug
```

<span data-ttu-id="d7de7-126">Когда модуль отладки будет готов, вы должны увидеть `Debugger listening on port 5858` в выходных данных консоли.</span><span class="sxs-lookup"><span data-stu-id="d7de7-126">When the debug engine is ready, you should see `Debugger listening on port 5858` in the console output.</span></span>

### <a name="configure-visual-studio-code-to-connect-to-the-remote-device"></a><span data-ttu-id="d7de7-127">Настройка Visual Studio Code для подключения к удаленному устройству</span><span class="sxs-lookup"><span data-stu-id="d7de7-127">Configure Visual Studio Code to connect to the remote device</span></span>

1. <span data-ttu-id="d7de7-128">Откройте панель **Отладка** слева.</span><span class="sxs-lookup"><span data-stu-id="d7de7-128">Open the **Debug** panel on the left side.</span></span>
2. <span data-ttu-id="d7de7-129">Нажмите зеленую кнопку **Начать отладку** (клавиша F5).</span><span class="sxs-lookup"><span data-stu-id="d7de7-129">Click the green **Start Debugging** (F5) button.</span></span> <span data-ttu-id="d7de7-130">В Visual Studio Code откроется файл `launch.json`.</span><span class="sxs-lookup"><span data-stu-id="d7de7-130">Visual Studio Code opens a `launch.json` file.</span></span>
3. <span data-ttu-id="d7de7-131">Обновите файл `launch.json` с использованием следующего содержимого.</span><span class="sxs-lookup"><span data-stu-id="d7de7-131">Update the `launch.json` file with the following content.</span></span> <span data-ttu-id="d7de7-132">Замените `[device hostname or IP address]` на IP-адрес или имя узла самого устройства.</span><span class="sxs-lookup"><span data-stu-id="d7de7-132">Replace `[device hostname or IP address]` with the actual device IP address or host name.</span></span>

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

### <a name="attach-to-the-remote-application"></a><span data-ttu-id="d7de7-134">Присоединение к удаленному приложению</span><span class="sxs-lookup"><span data-stu-id="d7de7-134">Attach to the remote application</span></span>

<span data-ttu-id="d7de7-135">Нажмите зеленую кнопку **Начать отладку** (клавиша F5), чтобы начать отладку.</span><span class="sxs-lookup"><span data-stu-id="d7de7-135">Click the green **Start Debugging** (F5) button to start debugging.</span></span>

<span data-ttu-id="d7de7-136">Дополнительные сведения об отладчике см. в статье [JavaScript in VS Code](https://code.visualstudio.com/docs/languages/javascript#_debugging) (JavaScript в VSCode).</span><span class="sxs-lookup"><span data-stu-id="d7de7-136">Read [JavaScript in VS Code](https://code.visualstudio.com/docs/languages/javascript#_debugging) to learn more about the debugger.</span></span>

![Отладка примера BLE](./media/iot-hub-gateway-kit-lessons/troubleshooting/debugging_ble_sample.png)

## <a name="azure-cli-issues"></a><span data-ttu-id="d7de7-138">Проблемы с интерфейсом командной строки Azure</span><span class="sxs-lookup"><span data-stu-id="d7de7-138">Azure CLI issues</span></span>

<span data-ttu-id="d7de7-139">Интерфейс командной строки Azure (Azure CLI) — это сборка предварительной версии.</span><span class="sxs-lookup"><span data-stu-id="d7de7-139">The Azure command-line interface (Azure CLI) is a preview build.</span></span> <span data-ttu-id="d7de7-140">Найти решения можно в [руководстве по установке предварительной версии](https://github.com/Azure/azure-cli/blob/master/doc/preview_install_guide.md).</span><span class="sxs-lookup"><span data-stu-id="d7de7-140">To seek solutions, you can use the [Preview Install Guide](https://github.com/Azure/azure-cli/blob/master/doc/preview_install_guide.md).</span></span>

<span data-ttu-id="d7de7-141">При появлении ошибок в средстве сообщите о [проблеме](https://github.com/Azure/azure-cli/issues) в разделе **Проблемы** репозитория GitHub.</span><span class="sxs-lookup"><span data-stu-id="d7de7-141">If you encounter any bugs with the tool, file an [issue](https://github.com/Azure/azure-cli/issues) in the **Issues** section of the GitHub repo.</span></span>

<span data-ttu-id="d7de7-142">Справку по устранению распространенных проблем см. в [файле сведений](https://github.com/Azure/azure-cli/blob/master/README.rst).</span><span class="sxs-lookup"><span data-stu-id="d7de7-142">For help in troubleshooting common problems, check the [readme](https://github.com/Azure/azure-cli/blob/master/README.rst).</span></span>

<span data-ttu-id="d7de7-143">При появлении сообщения "Не удалось найти версию, которая удовлетворяет требованиям" выполните следующую команду, чтобы обновить pip до последней версии.</span><span class="sxs-lookup"><span data-stu-id="d7de7-143">If you meet "Could not find a version that satisfies the requirement", please run the following command to upgrade pip to lastest version.</span></span>

```bash
python -m pip install --upgrade pip
```

## <a name="python-installation-issues"></a><span data-ttu-id="d7de7-144">Проблемы с установкой Python</span><span class="sxs-lookup"><span data-stu-id="d7de7-144">Python installation issues</span></span>

### <a name="legacy-installation-issues-macos"></a><span data-ttu-id="d7de7-145">Проблемы с устаревшими установками (macOS)</span><span class="sxs-lookup"><span data-stu-id="d7de7-145">Legacy installation issues (macOS)</span></span>

<span data-ttu-id="d7de7-146">При установке pip возникает ошибка разрешения, если есть устаревшие пакеты, которые устанавливаются с использованием разрешений **su**.</span><span class="sxs-lookup"><span data-stu-id="d7de7-146">When you're installing pip, a permission error is thrown when older packages are installed with **su** permissions.</span></span> <span data-ttu-id="d7de7-147">Такая ситуация возникает из-за того, что предыдущая установка Python с использованием brew (macOS) удалена не полностью.</span><span class="sxs-lookup"><span data-stu-id="d7de7-147">This situation occurs because a previous installation of Python using brew (macOS) is not uninstalled completely.</span></span> <span data-ttu-id="d7de7-148">Некоторые пакеты pip из предыдущей установки созданы с помощью разрешений корневой папки, что приводит к ошибке разрешения.</span><span class="sxs-lookup"><span data-stu-id="d7de7-148">Some pip packages from a previous installation were created by root, which causes the permission error.</span></span> <span data-ttu-id="d7de7-149">Чтобы решить эту проблему, необходимо удалить эти пакеты, установленные с помощью разрешений корневой папки.</span><span class="sxs-lookup"><span data-stu-id="d7de7-149">The solution is to remove those packages installed by root.</span></span> <span data-ttu-id="d7de7-150">Для этого необходимо сделать следующее:</span><span class="sxs-lookup"><span data-stu-id="d7de7-150">Use the following steps to complete this task:</span></span>

1. <span data-ttu-id="d7de7-151">Перейдите на сайт `/usr/local/lib/python2.7/site-packages`.</span><span class="sxs-lookup"><span data-stu-id="d7de7-151">Go to `/usr/local/lib/python2.7/site-packages`</span></span>
2. <span data-ttu-id="d7de7-152">Выведите список пакетов, созданных с использованием разрешений корневой папки: `ls -l | grep root`.</span><span class="sxs-lookup"><span data-stu-id="d7de7-152">List packages created by root: `ls -l | grep root`</span></span>
3. <span data-ttu-id="d7de7-153">Удалите пакеты из шага 2: `sudo rm -rf {package name}`.</span><span class="sxs-lookup"><span data-stu-id="d7de7-153">Uninstall packages from step 2: `sudo rm -rf {package name}`</span></span>
4. <span data-ttu-id="d7de7-154">Переустановите Python.</span><span class="sxs-lookup"><span data-stu-id="d7de7-154">Reinstall Python.</span></span>

## <a name="azure-iot-hub-issues"></a><span data-ttu-id="d7de7-155">Проблемы с Центром Интернета вещей Azure</span><span class="sxs-lookup"><span data-stu-id="d7de7-155">Azure IoT Hub issues</span></span>

<span data-ttu-id="d7de7-156">Если Центр Интернета вещей Azure успешно подготовлен с помощью Azure CLI и требуется инструмент для управления устройствами, подключенными к вашему Центру Интернета вещей, воспользуйтесь указанными ниже инструментами.</span><span class="sxs-lookup"><span data-stu-id="d7de7-156">If you've successfully provisioned your Azure IoT hub with the Azure CLI, and you need a tool to manage the devices that are connecting to your IoT hub, try the following tools.</span></span>

### <a name="device-explorer"></a><span data-ttu-id="d7de7-157">Обозреватель устройств</span><span class="sxs-lookup"><span data-stu-id="d7de7-157">Device Explorer</span></span>

<span data-ttu-id="d7de7-158">[Обозреватель устройств](https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer) работает на локальном компьютере Windows и подключается к Центру Интернета вещей в Azure.</span><span class="sxs-lookup"><span data-stu-id="d7de7-158">[Device Explorer](https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer) runs on your Windows local machine and connects to your IoT hub in Azure.</span></span> <span data-ttu-id="d7de7-159">Он взаимодействует со следующими [конечными точками Центра Интернета вещей](https://azure.microsoft.com/en-us/documentation/articles/iot-hub-devguide/):</span><span class="sxs-lookup"><span data-stu-id="d7de7-159">It communicates with the following [IoT Hub endpoints](https://azure.microsoft.com/en-us/documentation/articles/iot-hub-devguide/):</span></span>

- <span data-ttu-id="d7de7-160">управление удостоверениями устройств для подготовки устройств, зарегистрированных в Центре Интернета вещей, и управления ими;</span><span class="sxs-lookup"><span data-stu-id="d7de7-160">Device identity management to provision and manage devices registered with your IoT hub.</span></span>
- <span data-ttu-id="d7de7-161">получение сообщений с устройства в облако, что позволяет отслеживать сообщения, отправляемые с устройства в Центр Интернета вещей;</span><span class="sxs-lookup"><span data-stu-id="d7de7-161">Receive device-to-cloud so you can monitor messages sent from your device to your IoT hub.</span></span>
- <span data-ttu-id="d7de7-162">отправка сообщений из облака на устройство, что позволяет отправлять сообщения на устройства из вашего Центра Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="d7de7-162">Send cloud-to-device so you can send messages to your devices from your IoT hub.</span></span>

<span data-ttu-id="d7de7-163">Настройте свою строку подключения Центра Интернета вещей в этом инструменте, чтобы использовать все его возможности.</span><span class="sxs-lookup"><span data-stu-id="d7de7-163">Configure your IoT hub connection string within this tool to use all its capabilities.</span></span>

### <a name="iothub-explorer"></a><span data-ttu-id="d7de7-164">iothub-explorer</span><span class="sxs-lookup"><span data-stu-id="d7de7-164">iothub-explorer</span></span>

<span data-ttu-id="d7de7-165">[iothub-explorer](https://github.com/Azure/iothub-explorer) — это пример мультиплатформенного инструмента интерфейса командной строки для управления клиентами устройств.</span><span class="sxs-lookup"><span data-stu-id="d7de7-165">[iothub-explorer](https://github.com/Azure/iothub-explorer) is a sample multiplatform CLI tool to manage device clients.</span></span> <span data-ttu-id="d7de7-166">Инструмент можно использовать для управления устройствами в реестре удостоверений, мониторинга сообщений, отправляемых с устройства в облако, и отправки команд, передаваемых из облака на устройство.</span><span class="sxs-lookup"><span data-stu-id="d7de7-166">You can use the tool to manage the devices in the identity registry, monitor device-to-cloud messages, and send cloud-to-device commands.</span></span>

<span data-ttu-id="d7de7-167">Чтобы установить последнюю версию (предварительную версию) инструмента iothub-explorer, выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="d7de7-167">To install the latest (prerelease) version of the iothub-explorer tool, run the following command:</span></span>

```bash
npm install -g iothub-explorer@latest
```

<span data-ttu-id="d7de7-168">Дополнительную справку о всех командах iothub-explorer и их параметрах можно получить, выполнив следующую команду:</span><span class="sxs-lookup"><span data-stu-id="d7de7-168">To get additional help about all the iothub-explorer commands and their parameters, run the following command:</span></span>

```bash
iothub-explorer help
```

### <a name="the-azure-portal"></a><span data-ttu-id="d7de7-169">Портал Azure</span><span class="sxs-lookup"><span data-stu-id="d7de7-169">The Azure portal</span></span>

<span data-ttu-id="d7de7-170">Все возможности интерфейса командной строки помогают создавать все ресурсы Azure и управлять ими.</span><span class="sxs-lookup"><span data-stu-id="d7de7-170">A full CLI experience helps you create and manage all your Azure resources.</span></span> <span data-ttu-id="d7de7-171">Для подготовки, отладки ресурсов Azure и управления ими можно также воспользоваться [порталом Azure](https://azure.microsoft.com/en-us/documentation/articles/azure-portal-overview/).</span><span class="sxs-lookup"><span data-stu-id="d7de7-171">You might also want to use the [Azure portal](https://azure.microsoft.com/en-us/documentation/articles/azure-portal-overview/) to help provision, manage, and debug your Azure resources.</span></span>

## <a name="azure-storage-issues"></a><span data-ttu-id="d7de7-172">Проблемы с хранилищем Azure</span><span class="sxs-lookup"><span data-stu-id="d7de7-172">Azure Storage issues</span></span>

<span data-ttu-id="d7de7-173">[Обозреватель служб хранилища Microsoft Azure (предварительная версия)](http://storageexplorer.com/) — это автономное приложение от корпорации Майкрософт, которое можно использовать для работы с данными из службы хранилища Azure на платформе Windows, macOS и Linux.</span><span class="sxs-lookup"><span data-stu-id="d7de7-173">[Microsoft Azure Storage Explorer (preview)](http://storageexplorer.com/) is a standalone app from Microsoft that you can use to work with Azure Storage data on Windows, macOS, and Linux.</span></span> <span data-ttu-id="d7de7-174">Используя этот инструмент, можно подключаться к таблице и просматривать данные в ней.</span><span class="sxs-lookup"><span data-stu-id="d7de7-174">By using this tool, you can connect to your table and see the data in it.</span></span> <span data-ttu-id="d7de7-175">Его можно использовать для устранения неполадок в вашей службе хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="d7de7-175">You can use this tool to troubleshoot your Azure Storage issues.</span></span>
