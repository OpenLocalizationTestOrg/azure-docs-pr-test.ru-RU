---
title: "Подключение Intel Edison (Node) к Интернету вещей Azure. Урок 4. Устранение неполадок | Документация Майкрософт"
description: "Страница со сведениями об устранении неполадок в работе Intel Edison Node.js"
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "устранение неполадок Arduino"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-node-get-started
ms.assetid: f11c5521-8a36-44c0-baad-f5ec26ab4618
ms.service: iot-hub
ms.devlang: nodejs
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: d54dd4a13ed87152fb6c039f38a5ffe8b4470df9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshooting"></a><span data-ttu-id="484e1-104">Устранение неполадок</span><span class="sxs-lookup"><span data-stu-id="484e1-104">Troubleshooting</span></span>
## <a name="hardware-issues"></a><span data-ttu-id="484e1-105">Проблемы с оборудованием</span><span class="sxs-lookup"><span data-stu-id="484e1-105">Hardware issues</span></span>
<span data-ttu-id="484e1-106">Сведения об устранении распространенных проблем на устройстве Intel Edison см. на [этой официальной странице](https://software.intel.com/en-us/node/637974).</span><span class="sxs-lookup"><span data-stu-id="484e1-106">For information about solving common problems on Intel Edison, see the [official troubleshooting page](https://software.intel.com/en-us/node/637974).</span></span>

## <a name="nodejs-package-issues"></a><span data-ttu-id="484e1-107">Проблемы с пакетами Node.js</span><span class="sxs-lookup"><span data-stu-id="484e1-107">Node.js package issues</span></span>
### <a name="no-response-during-gulp-tasks"></a><span data-ttu-id="484e1-108">Нет ответа при выполнении задач Gulp</span><span class="sxs-lookup"><span data-stu-id="484e1-108">No response during gulp tasks</span></span>
<span data-ttu-id="484e1-109">Если при выполнении задач Gulp возникли проблемы, можно добавить параметр `--verbose` для отладки.</span><span class="sxs-lookup"><span data-stu-id="484e1-109">If you encounter problems running gulp tasks, you can add the `--verbose` option for debugging.</span></span> <span data-ttu-id="484e1-110">Попробуйте завершить текущие задачи Gulp, используя клавиши `Ctrl + C`, а затем выполните следующую команду в окне консоли, чтобы просмотреть сообщения отладки.</span><span class="sxs-lookup"><span data-stu-id="484e1-110">Try to terminate current gulp tasks by using `Ctrl + C`, and then run the following command in your console window to see debug messages.</span></span> <span data-ttu-id="484e1-111">В выходных данных консоли должны отобразиться подробные сообщения об ошибках.</span><span class="sxs-lookup"><span data-stu-id="484e1-111">You might see detailed error messages in your console output.</span></span> 

```bash
gulp --verbose
```

### <a name="npm-issues"></a><span data-ttu-id="484e1-112">проблемы с NPM</span><span class="sxs-lookup"><span data-stu-id="484e1-112">NPM issues</span></span>
<span data-ttu-id="484e1-113">Попробуйте обновить пакет NPM, выполнив следующую команду:</span><span class="sxs-lookup"><span data-stu-id="484e1-113">Try to update your NPM package with the following command:</span></span>

```bash
npm install -g npm
```

<span data-ttu-id="484e1-114">Если проблема не исчезла, оставьте комментарии в конце этой статьи или задайте вопрос о проблеме в GitHub в нашем [примере репозитория][sample-repository].</span><span class="sxs-lookup"><span data-stu-id="484e1-114">If the problem still exists, leave your comments at the end of this article or create a GitHub issue in our [sample repository][sample-repository].</span></span>

## <a name="remote-debugging"></a><span data-ttu-id="484e1-115">Удаленная отладка</span><span class="sxs-lookup"><span data-stu-id="484e1-115">Remote debugging</span></span>

### <a name="run-the-sample-application-in-debug-mode"></a><span data-ttu-id="484e1-116">Запуск примера приложения в режиме отладки</span><span class="sxs-lookup"><span data-stu-id="484e1-116">Run the sample application in debug mode</span></span>

```bash
gulp run --debug
```

<span data-ttu-id="484e1-117">Когда модуль отладки будет готов, ```Debugger listening on port 5858``` отобразится в выходных данных консоли.</span><span class="sxs-lookup"><span data-stu-id="484e1-117">Once the debug engine is ready, you should be able to see ```Debugger listening on port 5858``` from the console output.</span></span>

### <a name="configure-vs-code-to-connect-to-the-remote-device"></a><span data-ttu-id="484e1-118">Настройка VSCode для подключения к удаленному устройству</span><span class="sxs-lookup"><span data-stu-id="484e1-118">Configure VS Code to connect to the remote device</span></span>

<span data-ttu-id="484e1-119">Откройте панель **Отладка** слева.</span><span class="sxs-lookup"><span data-stu-id="484e1-119">Open the **Debug** panel from the left side.</span></span>

<span data-ttu-id="484e1-120">Нажмите зеленую кнопку **Начать отладку** (клавиша F5).</span><span class="sxs-lookup"><span data-stu-id="484e1-120">Click the green **Start Debugging** (F5) button.</span></span> <span data-ttu-id="484e1-121">В VSCode откроется файл **launch.json**, который необходимо обновить.</span><span class="sxs-lookup"><span data-stu-id="484e1-121">VS Code would open a **launch.json** file, which you need to update.</span></span>

<span data-ttu-id="484e1-122">Обновите файл **launch.json** с использованием следующего содержимого, заменив `[device hostname or IP address]` IP-адресом или именем узла самого устройства.</span><span class="sxs-lookup"><span data-stu-id="484e1-122">Update the **launch.json** file with the following content, replace `[device hostname or IP address]` with the actual device IP address or hostname.</span></span>  

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

![Конфигурация удаленной отладки](media/iot-hub-intel-edison-lessons/troubleshooting/remote_debugging_configuration.png)

### <a name="attach-to-the-remote-application"></a><span data-ttu-id="484e1-124">Присоединение к удаленному приложению</span><span class="sxs-lookup"><span data-stu-id="484e1-124">Attach to the remote application</span></span>

<span data-ttu-id="484e1-125">Нажмите зеленую кнопку **Начать отладку** (клавиша F5), чтобы запустить отладку.</span><span class="sxs-lookup"><span data-stu-id="484e1-125">Click the green **Start Debugging** (F5) button and enjoy debugging.</span></span>

<span data-ttu-id="484e1-126">Дополнительные сведения об отладчике см. в статье [JavaScript in VS Code](https://code.visualstudio.com/docs/languages/javascript#_debugging) (JavaScript в VSCode).</span><span class="sxs-lookup"><span data-stu-id="484e1-126">You can read [JavaScript in VS Code](https://code.visualstudio.com/docs/languages/javascript#_debugging) to learn more about the debugger.</span></span>

![Интерактивная удаленная отладка](media/iot-hub-intel-edison-lessons/troubleshooting/remote_debugging_interactive.png)

## <a name="azure-cli-issues"></a><span data-ttu-id="484e1-128">Проблемы с Azure CLI</span><span class="sxs-lookup"><span data-stu-id="484e1-128">Azure-CLI issues</span></span>
<span data-ttu-id="484e1-129">Интерфейс командной строки Azure (Azure CLI) — это сборка предварительной версии.</span><span class="sxs-lookup"><span data-stu-id="484e1-129">The Azure command-line interface (Azure CLI) is a preview build.</span></span> <span data-ttu-id="484e1-130">Решения можно найти в [руководстве по установке предварительной версии](https://github.com/Azure/azure-cli/blob/master/doc/preview_install_guide.md).</span><span class="sxs-lookup"><span data-stu-id="484e1-130">Look for solution in the [Preview Install Guide](https://github.com/Azure/azure-cli/blob/master/doc/preview_install_guide.md) to seek solutions.</span></span> <span data-ttu-id="484e1-131">Попытайтесь обновить Azure CLI до последней версии, если команда не работает должным образом.</span><span class="sxs-lookup"><span data-stu-id="484e1-131">Try to upgrade Azure-cli to latest version when commands don’t work as expected.</span></span>

<span data-ttu-id="484e1-132">При появлении ошибок в средстве сообщите о [проблеме](https://github.com/Azure/azure-cli/issues) в разделе **Проблемы** репозитория GitHub.</span><span class="sxs-lookup"><span data-stu-id="484e1-132">If you encounter any bugs with the tool, file an [issue](https://github.com/Azure/azure-cli/issues) in the **Issues** section of the GitHub repo.</span></span>

<span data-ttu-id="484e1-133">Справку по устранению распространенных проблем см. в [файле сведений](https://github.com/Azure/azure-cli/blob/master/README.rst).</span><span class="sxs-lookup"><span data-stu-id="484e1-133">For help troubleshooting common problems, check the [readme](https://github.com/Azure/azure-cli/blob/master/README.rst).</span></span>

<span data-ttu-id="484e1-134">При появлении сообщения "Не удалось найти версию, которая удовлетворяет требованиям" выполните следующую команду, чтобы обновить pip до последней версии.</span><span class="sxs-lookup"><span data-stu-id="484e1-134">If you meet "Could not find a version that satisfies the requirement", please run the following command to upgrade pip to lastest version.</span></span>

```bash
python -m pip install --upgrade pip
```

## <a name="python-installation-issues"></a><span data-ttu-id="484e1-135">Проблемы с установкой Python</span><span class="sxs-lookup"><span data-stu-id="484e1-135">Python installation issues</span></span>
### <a name="legacy-installation-issues-macos"></a><span data-ttu-id="484e1-136">Проблемы с устаревшими установками (macOS)</span><span class="sxs-lookup"><span data-stu-id="484e1-136">Legacy installation issues (macOS)</span></span>
<span data-ttu-id="484e1-137">При установке **pip** возникает ошибка разрешения, если есть устаревшие пакеты, которые устанавливаются с использованием разрешений **su**.</span><span class="sxs-lookup"><span data-stu-id="484e1-137">When you're installing **pip**, a permission error is thrown when older packages that are installed with **su** permissions.</span></span> <span data-ttu-id="484e1-138">Такая ситуация возникает из-за того, что предыдущая установка Python с использованием brew (macOS) удалена не полностью.</span><span class="sxs-lookup"><span data-stu-id="484e1-138">This situation occurs because a previous installation of Python using brew (macOS) is not uninstalled completely.</span></span> <span data-ttu-id="484e1-139">Некоторые пакеты **pip** из предыдущей установки созданы с помощью разрешений корневой папки, что приводит к ошибке разрешения.</span><span class="sxs-lookup"><span data-stu-id="484e1-139">Some **pip** packages from a previous installation were created by root, which causes the permission error.</span></span> <span data-ttu-id="484e1-140">Чтобы решить эту проблему, необходимо удалить эти пакеты, установленные с помощью разрешений корневой папки.</span><span class="sxs-lookup"><span data-stu-id="484e1-140">The solution is to remove those packages installed by root.</span></span> <span data-ttu-id="484e1-141">Для этого необходимо сделать следующее:</span><span class="sxs-lookup"><span data-stu-id="484e1-141">Use the following steps to complete this task:</span></span>

1. <span data-ttu-id="484e1-142">Перейдите к папке /usr/local/lib/python2.7/site-packages.</span><span class="sxs-lookup"><span data-stu-id="484e1-142">Go to: /usr/local/lib/python2.7/site-packages</span></span>
2. <span data-ttu-id="484e1-143">Выведите список пакетов, созданных с использованием разрешений корневой папки: `ls -l | grep root`.</span><span class="sxs-lookup"><span data-stu-id="484e1-143">List packages create by root: `ls -l | grep root`</span></span>
3. <span data-ttu-id="484e1-144">Удалите пакеты из шага 2: `sudo rm -rf {package name}`.</span><span class="sxs-lookup"><span data-stu-id="484e1-144">Uninstall packages from step 2: `sudo rm -rf {package name}`</span></span>
4. <span data-ttu-id="484e1-145">Переустановите Python.</span><span class="sxs-lookup"><span data-stu-id="484e1-145">Reinstall Python.</span></span>

## <a name="azure-iot-hub-issues"></a><span data-ttu-id="484e1-146">Проблемы с Центром Интернета вещей Azure</span><span class="sxs-lookup"><span data-stu-id="484e1-146">Azure IoT Hub issues</span></span>
<span data-ttu-id="484e1-147">Если Центр Интернета вещей Azure успешно подготовлен с помощью `azure-cli` и требуется инструмент для управления устройствами, подключенными к вашему Центру Интернета вещей, воспользуйтесь следующими инструментами:</span><span class="sxs-lookup"><span data-stu-id="484e1-147">If you've successfully provisioned your Azure IoT hub with `azure-cli`, and you need a tool to manage the devices that are connecting to your IoT hub, try the following tools:</span></span>

### <a name="device-explorer"></a><span data-ttu-id="484e1-148">Обозреватель устройств</span><span class="sxs-lookup"><span data-stu-id="484e1-148">Device Explorer</span></span>
<span data-ttu-id="484e1-149">[Обозреватель устройств](https://github.com/Azure/azure-iot-sdk-csharp/tree/master/tools/DeviceExplorer) работает на локальном компьютере Windows и подключается к Центру Интернета вещей в Azure.</span><span class="sxs-lookup"><span data-stu-id="484e1-149">[Device Explorer](https://github.com/Azure/azure-iot-sdk-csharp/tree/master/tools/DeviceExplorer) runs on your Windows local machine and connects to your IoT hub in Azure.</span></span> <span data-ttu-id="484e1-150">Он взаимодействует со следующими [конечными точками Центра Интернета вещей](iot-hub-devguide.md):</span><span class="sxs-lookup"><span data-stu-id="484e1-150">It communicates with the following [IoT Hub endpoints](iot-hub-devguide.md):</span></span>

- <span data-ttu-id="484e1-151">_управление удостоверениями устройств_ для подготовки устройств, зарегистрированных в Центре Интернета вещей, и управления ими;</span><span class="sxs-lookup"><span data-stu-id="484e1-151">_Device identity management_ to provision and manage devices registered with your IoT hub.</span></span>
- <span data-ttu-id="484e1-152">_получение сообщений с устройства в облако_, что позволяет отслеживать сообщения, отправляемые с устройства в Центр Интернета вещей;</span><span class="sxs-lookup"><span data-stu-id="484e1-152">_Receive device-to-cloud_ so you can monitor messages sent from your device to your IoT hub.</span></span>
- <span data-ttu-id="484e1-153">_отправка сообщений из облака на устройство_, что позволяет отправлять сообщения на устройства из вашего Центра Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="484e1-153">_Send cloud-to-device_ so you can send messages to your devices from your IoT hub.</span></span>

<span data-ttu-id="484e1-154">Настройте свою `IoT hub connection string` в этом инструменте, чтобы использовать его возможности.</span><span class="sxs-lookup"><span data-stu-id="484e1-154">Configure your `IoT hub connection string` within this tool to use all its capabilities.</span></span>

### <a name="iot-hub-explorer"></a><span data-ttu-id="484e1-155">Обозреватель Центра Интернета вещей</span><span class="sxs-lookup"><span data-stu-id="484e1-155">IoT hub Explorer</span></span>
<span data-ttu-id="484e1-156">[Обозреватель Центра Интернета вещей](https://github.com/Azure/iothub-explorer) — это пример мультиплатформенного инструмента интерфейса командной строки для управления клиентами устройств.</span><span class="sxs-lookup"><span data-stu-id="484e1-156">[IoT hub Explorer](https://github.com/Azure/iothub-explorer) is a sample multiplatform CLI tool to manage device clients.</span></span> <span data-ttu-id="484e1-157">Инструмент можно использовать для управления устройствами в реестре удостоверений, мониторинга сообщений, отправляемых с устройства в облако, и отправки команд, передаваемых из облака на устройство.</span><span class="sxs-lookup"><span data-stu-id="484e1-157">You can use the tool to manage the devices in the identity registry, monitor device-to-cloud messages, and send cloud-to-device commands.</span></span>

<span data-ttu-id="484e1-158">Чтобы установить последнюю версию (предварительную версию) инструмента iothub-explorer, выполните следующую команду в среде командной строки:</span><span class="sxs-lookup"><span data-stu-id="484e1-158">To install the latest (prerelease) version of the iothub-explorer tool, run the following command in your command-line environment:</span></span>

```bash
npm install -g iothub-explorer@latest
```

<span data-ttu-id="484e1-159">Дополнительную справку о всех командах iothub-explorer и их параметрах можно получить, выполнив следующую команду:</span><span class="sxs-lookup"><span data-stu-id="484e1-159">You can use the following command to get additional help about all the iothub-explorer commands and their parameters:</span></span>

```bash
iothub-explorer help
```

### <a name="azure-portal"></a><span data-ttu-id="484e1-160">Портал Azure</span><span class="sxs-lookup"><span data-stu-id="484e1-160">Azure portal</span></span>
<span data-ttu-id="484e1-161">Все возможности интерфейса командной строки помогают создавать все ресурсы Azure и управлять ими.</span><span class="sxs-lookup"><span data-stu-id="484e1-161">A full CLI experience helps you create and manage all your Azure resources.</span></span> <span data-ttu-id="484e1-162">Для подготовки, отладки ресурсов Azure и управления ими можно также воспользоваться [порталом Azure](../azure-portal-overview.md).</span><span class="sxs-lookup"><span data-stu-id="484e1-162">You might also want to use the [Azure portal](../azure-portal-overview.md) to help provision, manage, and debug your Azure resources.</span></span>

## <a name="azure-storage-issues"></a><span data-ttu-id="484e1-163">Проблемы со службой хранилища Azure</span><span class="sxs-lookup"><span data-stu-id="484e1-163">Azure storage issues</span></span>
<span data-ttu-id="484e1-164">[Обозреватель служб хранилища Microsoft Azure (предварительная версия)](http://storageexplorer.com) — это автономное приложение от корпорации Майкрософт, которое можно использовать для работы с данными из [службы хранилища Azure](https://azure.microsoft.com/en-us/services/storage/) на платформе Windows, macOS и Linux.</span><span class="sxs-lookup"><span data-stu-id="484e1-164">[Microsoft Azure Storage Explorer (preview)](http://storageexplorer.com) is a standalone app from Microsoft that you can use to work with [Azure Storage](https://azure.microsoft.com/en-us/services/storage/) data on Windows, macOS, and Linux.</span></span> <span data-ttu-id="484e1-165">Используя этот инструмент, можно подключаться к таблице и просматривать данные в ней.</span><span class="sxs-lookup"><span data-stu-id="484e1-165">By using this tool, you can connect to your table and see the data in it.</span></span> <span data-ttu-id="484e1-166">Его можно использовать для устранения неполадок в вашей службе хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="484e1-166">You can use this tool to troubleshoot your Azure Storage issues.</span></span>

## <a name="next-steps"></a><span data-ttu-id="484e1-167">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="484e1-167">Next steps</span></span>
<span data-ttu-id="484e1-168">На этой странице приведены только наиболее распространенные проблемы с набором Intel Edison.</span><span class="sxs-lookup"><span data-stu-id="484e1-168">This page only includes the most common problems of Intel Edison kit.</span></span> <span data-ttu-id="484e1-169">Вы также можете оставить комментарии внизу страницы, чтобы сообщить о проблемах для дальнейшего устранения неполадок.</span><span class="sxs-lookup"><span data-stu-id="484e1-169">You can also leave bottom comments to report issues for further troubleshooting.</span></span>

<span data-ttu-id="484e1-170">Вернитесь к изучению статьи [Начало работы с Intel Edison (Node.js)](iot-hub-intel-edison-kit-node-get-started.md)</span><span class="sxs-lookup"><span data-stu-id="484e1-170">Go back to [Get started with Intel Edison (Node.js)](iot-hub-intel-edison-kit-node-get-started.md)</span></span>

<!-- Images and links -->

[sample-repository]: https://github.com/Azure-Samples/iot-hub-node-edison-getting-started