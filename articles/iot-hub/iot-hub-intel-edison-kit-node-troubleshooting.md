---
title: "Подключение Edison Intel (узел) tooAzure IoT — занятия 4: Устранение неполадок | Документы Microsoft"
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
ms.openlocfilehash: 9502300f7f372255572b49bea45dd3e1fdaeeb37
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting"></a><span data-ttu-id="7e9b8-104">Устранение неполадок</span><span class="sxs-lookup"><span data-stu-id="7e9b8-104">Troubleshooting</span></span>
## <a name="hardware-issues"></a><span data-ttu-id="7e9b8-105">Проблемы с оборудованием</span><span class="sxs-lookup"><span data-stu-id="7e9b8-105">Hardware issues</span></span>
<span data-ttu-id="7e9b8-106">Сведения об устранении типичных проблем на Intel Edison см. в разделе hello [официальный по устранению неполадок страницы](https://software.intel.com/en-us/node/637974).</span><span class="sxs-lookup"><span data-stu-id="7e9b8-106">For information about solving common problems on Intel Edison, see hello [official troubleshooting page](https://software.intel.com/en-us/node/637974).</span></span>

## <a name="nodejs-package-issues"></a><span data-ttu-id="7e9b8-107">Проблемы с пакетами Node.js</span><span class="sxs-lookup"><span data-stu-id="7e9b8-107">Node.js package issues</span></span>
### <a name="no-response-during-gulp-tasks"></a><span data-ttu-id="7e9b8-108">Нет ответа при выполнении задач Gulp</span><span class="sxs-lookup"><span data-stu-id="7e9b8-108">No response during gulp tasks</span></span>
<span data-ttu-id="7e9b8-109">Если возникли проблемы при выполнении задачи gulp, можно добавить hello `--verbose` параметра для отладки.</span><span class="sxs-lookup"><span data-stu-id="7e9b8-109">If you encounter problems running gulp tasks, you can add hello `--verbose` option for debugging.</span></span> <span data-ttu-id="7e9b8-110">Повторите tooterminate текущие задачи gulp с помощью `Ctrl + C`, а затем выполнения hello следующую команду в сообщения отладки toosee окна консоли.</span><span class="sxs-lookup"><span data-stu-id="7e9b8-110">Try tooterminate current gulp tasks by using `Ctrl + C`, and then run hello following command in your console window toosee debug messages.</span></span> <span data-ttu-id="7e9b8-111">В выходных данных консоли должны отобразиться подробные сообщения об ошибках.</span><span class="sxs-lookup"><span data-stu-id="7e9b8-111">You might see detailed error messages in your console output.</span></span> 

```bash
gulp --verbose
```

### <a name="npm-issues"></a><span data-ttu-id="7e9b8-112">проблемы с NPM</span><span class="sxs-lookup"><span data-stu-id="7e9b8-112">NPM issues</span></span>
<span data-ttu-id="7e9b8-113">Попробуйте tooupdate пакета NPM с hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="7e9b8-113">Try tooupdate your NPM package with hello following command:</span></span>

```bash
npm install -g npm
```

<span data-ttu-id="7e9b8-114">Если hello проблема остается, оставьте комментарий в конце hello в этой статье, или создать вопрос GitHub в нашем [репозитории примеров][sample-repository].</span><span class="sxs-lookup"><span data-stu-id="7e9b8-114">If hello problem still exists, leave your comments at hello end of this article or create a GitHub issue in our [sample repository][sample-repository].</span></span>

## <a name="remote-debugging"></a><span data-ttu-id="7e9b8-115">Удаленная отладка</span><span class="sxs-lookup"><span data-stu-id="7e9b8-115">Remote debugging</span></span>

### <a name="run-hello-sample-application-in-debug-mode"></a><span data-ttu-id="7e9b8-116">Запустить образец приложения hello в режиме отладки</span><span class="sxs-lookup"><span data-stu-id="7e9b8-116">Run hello sample application in debug mode</span></span>

```bash
gulp run --debug
```

<span data-ttu-id="7e9b8-117">После подготовки hello отладчик должен быть доступ toosee ```Debugger listening on port 5858``` из выходных данных консоли hello.</span><span class="sxs-lookup"><span data-stu-id="7e9b8-117">Once hello debug engine is ready, you should be able toosee ```Debugger listening on port 5858``` from hello console output.</span></span>

### <a name="configure-vs-code-tooconnect-toohello-remote-device"></a><span data-ttu-id="7e9b8-118">Настройте удаленное устройство VS Code tooconnect toohello</span><span class="sxs-lookup"><span data-stu-id="7e9b8-118">Configure VS Code tooconnect toohello remote device</span></span>

<span data-ttu-id="7e9b8-119">Откройте hello **отладки** панели hello слева.</span><span class="sxs-lookup"><span data-stu-id="7e9b8-119">Open hello **Debug** panel from hello left side.</span></span>

<span data-ttu-id="7e9b8-120">Щелкните зеленый hello **начать отладку** кнопки (F5).</span><span class="sxs-lookup"><span data-stu-id="7e9b8-120">Click hello green **Start Debugging** (F5) button.</span></span> <span data-ttu-id="7e9b8-121">Будет открыт VS Code **launch.json** файл, который требуется tooupdate.</span><span class="sxs-lookup"><span data-stu-id="7e9b8-121">VS Code would open a **launch.json** file, which you need tooupdate.</span></span>

<span data-ttu-id="7e9b8-122">Обновление hello **launch.json** с hello следующие содержимое файла, замените `[device hostname or IP address]` с hello само устройство IP-адрес или имя узла.</span><span class="sxs-lookup"><span data-stu-id="7e9b8-122">Update hello **launch.json** file with hello following content, replace `[device hostname or IP address]` with hello actual device IP address or hostname.</span></span>  

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

### <a name="attach-toohello-remote-application"></a><span data-ttu-id="7e9b8-124">Присоединение удаленного приложения toohello</span><span class="sxs-lookup"><span data-stu-id="7e9b8-124">Attach toohello remote application</span></span>

<span data-ttu-id="7e9b8-125">Щелкните зеленый hello **начать отладку** (F5) кнопку и наслаждаться отладки.</span><span class="sxs-lookup"><span data-stu-id="7e9b8-125">Click hello green **Start Debugging** (F5) button and enjoy debugging.</span></span>

<span data-ttu-id="7e9b8-126">Можно прочитать [JavaScript в VS Code](https://code.visualstudio.com/docs/languages/javascript#_debugging) toolearn Дополнительные сведения об отладчике hello.</span><span class="sxs-lookup"><span data-stu-id="7e9b8-126">You can read [JavaScript in VS Code](https://code.visualstudio.com/docs/languages/javascript#_debugging) toolearn more about hello debugger.</span></span>

![Интерактивная удаленная отладка](media/iot-hub-intel-edison-lessons/troubleshooting/remote_debugging_interactive.png)

## <a name="azure-cli-issues"></a><span data-ttu-id="7e9b8-128">Проблемы с Azure CLI</span><span class="sxs-lookup"><span data-stu-id="7e9b8-128">Azure-CLI issues</span></span>
<span data-ttu-id="7e9b8-129">Hello Azure командной строки (CLI Azure) — это построение предварительного просмотра.</span><span class="sxs-lookup"><span data-stu-id="7e9b8-129">hello Azure command-line interface (Azure CLI) is a preview build.</span></span> <span data-ttu-id="7e9b8-130">Искать решение в hello [руководство по установке Preview](https://github.com/Azure/azure-cli/blob/master/doc/preview_install_guide.md) tooseek решения.</span><span class="sxs-lookup"><span data-stu-id="7e9b8-130">Look for solution in hello [Preview Install Guide](https://github.com/Azure/azure-cli/blob/master/doc/preview_install_guide.md) tooseek solutions.</span></span> <span data-ttu-id="7e9b8-131">Повторите версии toolatest tooupgrade Azure cli, когда команды не работают должным образом.</span><span class="sxs-lookup"><span data-stu-id="7e9b8-131">Try tooupgrade Azure-cli toolatest version when commands don’t work as expected.</span></span>

<span data-ttu-id="7e9b8-132">При возникновении любых ошибок с помощью средства hello файл [проблема](https://github.com/Azure/azure-cli/issues) в hello **проблемы** раздел hello в репозитории GitHub.</span><span class="sxs-lookup"><span data-stu-id="7e9b8-132">If you encounter any bugs with hello tool, file an [issue](https://github.com/Azure/azure-cli/issues) in hello **Issues** section of hello GitHub repo.</span></span>

<span data-ttu-id="7e9b8-133">Для получения справки по устранению общих проблем, проверьте hello [readme](https://github.com/Azure/azure-cli/blob/master/README.rst).</span><span class="sxs-lookup"><span data-stu-id="7e9b8-133">For help troubleshooting common problems, check hello [readme](https://github.com/Azure/azure-cli/blob/master/README.rst).</span></span>

<span data-ttu-id="7e9b8-134">Если соблюдаются «Не удалось найти версию, которая соответствует требованиям hello», проверьте выполнения hello следующая команда tooupgrade pip toolastest версии.</span><span class="sxs-lookup"><span data-stu-id="7e9b8-134">If you meet "Could not find a version that satisfies hello requirement", please run hello following command tooupgrade pip toolastest version.</span></span>

```bash
python -m pip install --upgrade pip
```

## <a name="python-installation-issues"></a><span data-ttu-id="7e9b8-135">Проблемы с установкой Python</span><span class="sxs-lookup"><span data-stu-id="7e9b8-135">Python installation issues</span></span>
### <a name="legacy-installation-issues-macos"></a><span data-ttu-id="7e9b8-136">Проблемы с устаревшими установками (macOS)</span><span class="sxs-lookup"><span data-stu-id="7e9b8-136">Legacy installation issues (macOS)</span></span>
<span data-ttu-id="7e9b8-137">При установке **pip** возникает ошибка разрешения, если есть устаревшие пакеты, которые устанавливаются с использованием разрешений **su**.</span><span class="sxs-lookup"><span data-stu-id="7e9b8-137">When you're installing **pip**, a permission error is thrown when older packages that are installed with **su** permissions.</span></span> <span data-ttu-id="7e9b8-138">Такая ситуация возникает из-за того, что предыдущая установка Python с использованием brew (macOS) удалена не полностью.</span><span class="sxs-lookup"><span data-stu-id="7e9b8-138">This situation occurs because a previous installation of Python using brew (macOS) is not uninstalled completely.</span></span> <span data-ttu-id="7e9b8-139">Некоторые **pip** пакеты из предыдущей установки были созданы корневым элементом, который приводит к возникновению ошибки разрешение hello.</span><span class="sxs-lookup"><span data-stu-id="7e9b8-139">Some **pip** packages from a previous installation were created by root, which causes hello permission error.</span></span> <span data-ttu-id="7e9b8-140">Здравствуйте, решение является tooremove эти пакеты, установленные корневым элементом.</span><span class="sxs-lookup"><span data-stu-id="7e9b8-140">hello solution is tooremove those packages installed by root.</span></span> <span data-ttu-id="7e9b8-141">Используйте следующие шаги toocomplete hello этой задачи:</span><span class="sxs-lookup"><span data-stu-id="7e9b8-141">Use hello following steps toocomplete this task:</span></span>

1. <span data-ttu-id="7e9b8-142">Перейдите к папке /usr/local/lib/python2.7/site-packages.</span><span class="sxs-lookup"><span data-stu-id="7e9b8-142">Go to: /usr/local/lib/python2.7/site-packages</span></span>
2. <span data-ttu-id="7e9b8-143">Выведите список пакетов, созданных с использованием разрешений корневой папки: `ls -l | grep root`.</span><span class="sxs-lookup"><span data-stu-id="7e9b8-143">List packages create by root: `ls -l | grep root`</span></span>
3. <span data-ttu-id="7e9b8-144">Удалите пакеты из шага 2: `sudo rm -rf {package name}`.</span><span class="sxs-lookup"><span data-stu-id="7e9b8-144">Uninstall packages from step 2: `sudo rm -rf {package name}`</span></span>
4. <span data-ttu-id="7e9b8-145">Переустановите Python.</span><span class="sxs-lookup"><span data-stu-id="7e9b8-145">Reinstall Python.</span></span>

## <a name="azure-iot-hub-issues"></a><span data-ttu-id="7e9b8-146">Проблемы с Центром Интернета вещей Azure</span><span class="sxs-lookup"><span data-stu-id="7e9b8-146">Azure IoT Hub issues</span></span>
<span data-ttu-id="7e9b8-147">Если успешной подготовки ваш центр Azure IoT с `azure-cli`, и необходимо, чтобы устройства hello toomanage средство, подключающимися центра IoT tooyour, попробуйте hello следующие средства:</span><span class="sxs-lookup"><span data-stu-id="7e9b8-147">If you've successfully provisioned your Azure IoT hub with `azure-cli`, and you need a tool toomanage hello devices that are connecting tooyour IoT hub, try hello following tools:</span></span>

### <a name="device-explorer"></a><span data-ttu-id="7e9b8-148">Обозреватель устройств</span><span class="sxs-lookup"><span data-stu-id="7e9b8-148">Device Explorer</span></span>
<span data-ttu-id="7e9b8-149">[Обозреватель устройств](https://github.com/Azure/azure-iot-sdk-csharp/tree/master/tools/DeviceExplorer) выполняется на локальном компьютере Windows и подключается tooyour центр IoT в Azure.</span><span class="sxs-lookup"><span data-stu-id="7e9b8-149">[Device Explorer](https://github.com/Azure/azure-iot-sdk-csharp/tree/master/tools/DeviceExplorer) runs on your Windows local machine and connects tooyour IoT hub in Azure.</span></span> <span data-ttu-id="7e9b8-150">Он взаимодействует с hello следующие [конечные точки центра IoT](iot-hub-devguide.md):</span><span class="sxs-lookup"><span data-stu-id="7e9b8-150">It communicates with hello following [IoT Hub endpoints](iot-hub-devguide.md):</span></span>

- <span data-ttu-id="7e9b8-151">_Управление устройствами удостоверения_ tooprovision и управления ими устройствах, зарегистрированных в центр IoT.</span><span class="sxs-lookup"><span data-stu-id="7e9b8-151">_Device identity management_ tooprovision and manage devices registered with your IoT hub.</span></span>
- <span data-ttu-id="7e9b8-152">_Получение устройства в облако_ можно наблюдать за сообщений, отправленных из центра IoT tooyour вашего устройства.</span><span class="sxs-lookup"><span data-stu-id="7e9b8-152">_Receive device-to-cloud_ so you can monitor messages sent from your device tooyour IoT hub.</span></span>
- <span data-ttu-id="7e9b8-153">_Отправить облака на устройство_ для отправки сообщений tooyour устройств из вашего центра IoT.</span><span class="sxs-lookup"><span data-stu-id="7e9b8-153">_Send cloud-to-device_ so you can send messages tooyour devices from your IoT hub.</span></span>

<span data-ttu-id="7e9b8-154">Настройка вашего `IoT hub connection string` в этот инструмент toouse его возможности.</span><span class="sxs-lookup"><span data-stu-id="7e9b8-154">Configure your `IoT hub connection string` within this tool toouse all its capabilities.</span></span>

### <a name="iot-hub-explorer"></a><span data-ttu-id="7e9b8-155">Обозреватель Центра Интернета вещей</span><span class="sxs-lookup"><span data-stu-id="7e9b8-155">IoT hub Explorer</span></span>
<span data-ttu-id="7e9b8-156">[Центр IoT Explorer](https://github.com/Azure/iothub-explorer) -это средство многоплатформенного CLI образец toomanage клиентов устройств.</span><span class="sxs-lookup"><span data-stu-id="7e9b8-156">[IoT hub Explorer](https://github.com/Azure/iothub-explorer) is a sample multiplatform CLI tool toomanage device clients.</span></span> <span data-ttu-id="7e9b8-157">Можно использовать hello средство toomanage hello устройства в реестре удостоверений hello, отслеживать сообщения из устройства в облако и отправлять команды облака на устройство.</span><span class="sxs-lookup"><span data-stu-id="7e9b8-157">You can use hello tool toomanage hello devices in hello identity registry, monitor device-to-cloud messages, and send cloud-to-device commands.</span></span>

<span data-ttu-id="7e9b8-158">tooinstall hello последняя (Предварительная) версия hello центром IOT-анализатор, запустите следующую команду в среде командной строки hello:</span><span class="sxs-lookup"><span data-stu-id="7e9b8-158">tooinstall hello latest (prerelease) version of hello iothub-explorer tool, run hello following command in your command-line environment:</span></span>

```bash
npm install -g iothub-explorer@latest
```

<span data-ttu-id="7e9b8-159">Можно использовать следующую команду, tooget дополнительную справку обо всех hello центром IOT обозреватель команды и их параметрах hello.</span><span class="sxs-lookup"><span data-stu-id="7e9b8-159">You can use hello following command tooget additional help about all hello iothub-explorer commands and their parameters:</span></span>

```bash
iothub-explorer help
```

### <a name="azure-portal"></a><span data-ttu-id="7e9b8-160">Портал Azure</span><span class="sxs-lookup"><span data-stu-id="7e9b8-160">Azure portal</span></span>
<span data-ttu-id="7e9b8-161">Все возможности интерфейса командной строки помогают создавать все ресурсы Azure и управлять ими.</span><span class="sxs-lookup"><span data-stu-id="7e9b8-161">A full CLI experience helps you create and manage all your Azure resources.</span></span> <span data-ttu-id="7e9b8-162">Можно также toouse hello [портал Azure](../azure-portal-overview.md) toohelp подготовки, управления и отладки ресурсам Azure.</span><span class="sxs-lookup"><span data-stu-id="7e9b8-162">You might also want toouse hello [Azure portal](../azure-portal-overview.md) toohelp provision, manage, and debug your Azure resources.</span></span>

## <a name="azure-storage-issues"></a><span data-ttu-id="7e9b8-163">Проблемы со службой хранилища Azure</span><span class="sxs-lookup"><span data-stu-id="7e9b8-163">Azure storage issues</span></span>
<span data-ttu-id="7e9b8-164">[Обозреватель хранилищ Microsoft Azure (Предварительная версия)](http://storageexplorer.com) имеет отдельное приложение от Майкрософт, можно использовать toowork с [хранилища Azure](https://azure.microsoft.com/en-us/services/storage/) данных в Windows, macOS и Linux.</span><span class="sxs-lookup"><span data-stu-id="7e9b8-164">[Microsoft Azure Storage Explorer (preview)](http://storageexplorer.com) is a standalone app from Microsoft that you can use toowork with [Azure Storage](https://azure.microsoft.com/en-us/services/storage/) data on Windows, macOS, and Linux.</span></span> <span data-ttu-id="7e9b8-165">С ее помощью можно подключиться tooyour таблицы и просмотра данных hello.</span><span class="sxs-lookup"><span data-stu-id="7e9b8-165">By using this tool, you can connect tooyour table and see hello data in it.</span></span> <span data-ttu-id="7e9b8-166">Можно использовать этот инструмент tootroubleshoot вашей проблемы хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="7e9b8-166">You can use this tool tootroubleshoot your Azure Storage issues.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7e9b8-167">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="7e9b8-167">Next steps</span></span>
<span data-ttu-id="7e9b8-168">Эта страница содержит только наиболее распространенные проблемы hello комплекта Intel Edison.</span><span class="sxs-lookup"><span data-stu-id="7e9b8-168">This page only includes hello most common problems of Intel Edison kit.</span></span> <span data-ttu-id="7e9b8-169">Также можно оставить комментарии нижней tooreport вопросы по устранению неполадок.</span><span class="sxs-lookup"><span data-stu-id="7e9b8-169">You can also leave bottom comments tooreport issues for further troubleshooting.</span></span>

<span data-ttu-id="7e9b8-170">Возврат слишком[Приступая к работе с Edison Intel (Node.js)](iot-hub-intel-edison-kit-node-get-started.md)</span><span class="sxs-lookup"><span data-stu-id="7e9b8-170">Go back too[Get started with Intel Edison (Node.js)](iot-hub-intel-edison-kit-node-get-started.md)</span></span>

<!-- Images and links -->

[sample-repository]: https://github.com/Azure-Samples/iot-hub-node-edison-getting-started