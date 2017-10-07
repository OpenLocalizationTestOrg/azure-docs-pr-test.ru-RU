---
title: "Connect Raspberry PI (C) tooAzure IoT — Устранение неполадок | Документы Microsoft"
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
ms.openlocfilehash: 4f1ea81dd25d10a39c2939f5ee5f19f6d2ba2b2d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting"></a><span data-ttu-id="f45df-104">Устранение неполадок</span><span class="sxs-lookup"><span data-stu-id="f45df-104">Troubleshooting</span></span>
## <a name="hardware-issues"></a><span data-ttu-id="f45df-105">Проблемы с оборудованием</span><span class="sxs-lookup"><span data-stu-id="f45df-105">Hardware issues</span></span>
### <a name="hello-application-runs-well-but-hello-led-is-not-blinking"></a><span data-ttu-id="f45df-106">приложение Hello также выполняется, но hello Индикатор мигает. это не</span><span class="sxs-lookup"><span data-stu-id="f45df-106">hello application runs well but hello LED is not blinking</span></span>
<span data-ttu-id="f45df-107">Эта проблема не будет всегда связанные toohello оборудования канала связи.</span><span class="sxs-lookup"><span data-stu-id="f45df-107">This issue is always related toohello hardware circuit connectivity.</span></span> <span data-ttu-id="f45df-108">Используйте следующие шаги tooidentify проблемы hello.</span><span class="sxs-lookup"><span data-stu-id="f45df-108">Use hello following steps tooidentify problems.</span></span>

1. <span data-ttu-id="f45df-109">Проверьте, что выбран правильный hello **объект групповой ПОЛИТИКИ** на доске.</span><span class="sxs-lookup"><span data-stu-id="f45df-109">Check that you chose hello correct **GPIO** on your board.</span></span> <span data-ttu-id="f45df-110">Hello двух портов должно быть **Земля объект групповой ПОЛИТИКИ (6 ПИН-код)** и **04 объект групповой ПОЛИТИКИ (7 ПИН-код)**.</span><span class="sxs-lookup"><span data-stu-id="f45df-110">hello two ports should be **GPIO GND (Pin 6)** and **GPIO 04 (Pin 7)**.</span></span>
2. <span data-ttu-id="f45df-111">Проверьте правильность полярности hello вашей индикатора.</span><span class="sxs-lookup"><span data-stu-id="f45df-111">Check that hello polarity of your LED is correct.</span></span> <span data-ttu-id="f45df-112">участок больше Hello должно быть указано hello **положительное**, анод ПИН-код.</span><span class="sxs-lookup"><span data-stu-id="f45df-112">hello longer leg should indicate hello **positive**, anode pin.</span></span>
3. <span data-ttu-id="f45df-113">Используйте hello **закрепить 3,3 в** и **Земля ПИН-код** на Pi Raspberry 3.</span><span class="sxs-lookup"><span data-stu-id="f45df-113">Use hello **3.3V Pin** and **GND Pin** on Raspberry Pi 3.</span></span> <span data-ttu-id="f45df-114">Считать Pi hello питания постоянного ТОКА.</span><span class="sxs-lookup"><span data-stu-id="f45df-114">Treat Pi as hello DC power.</span></span> <span data-ttu-id="f45df-115">Убедитесь, что этот Индикатор hello работает нормально.</span><span class="sxs-lookup"><span data-stu-id="f45df-115">Check that hello LED works fine.</span></span>

![Спецификация светодиодного индикатора](media/iot-hub-raspberry-pi-lessons/troubleshooting/led_spec.png)

### <a name="other-hardware-issues"></a><span data-ttu-id="f45df-117">Другие проблемы с оборудованием</span><span class="sxs-lookup"><span data-stu-id="f45df-117">Other hardware issues</span></span>
<span data-ttu-id="f45df-118">Сведения об устранении типичных проблем на Raspberry Pi 3 см. в разделе hello [официальный по устранению неполадок страницы](http://elinux.org/R-Pi_Troubleshooting).</span><span class="sxs-lookup"><span data-stu-id="f45df-118">For information about solving common problems on Raspberry Pi 3, see hello [official troubleshooting page](http://elinux.org/R-Pi_Troubleshooting).</span></span>

## <a name="nodejs-package-issues"></a><span data-ttu-id="f45df-119">Проблемы с пакетами Node.js</span><span class="sxs-lookup"><span data-stu-id="f45df-119">Node.js package issues</span></span>
### <a name="no-response-during-gulp-tasks"></a><span data-ttu-id="f45df-120">Нет ответа при выполнении задач Gulp</span><span class="sxs-lookup"><span data-stu-id="f45df-120">No response during gulp tasks</span></span>
<span data-ttu-id="f45df-121">Если возникли проблемы при выполнении задачи gulp, можно добавить hello `--verbose` параметра для отладки.</span><span class="sxs-lookup"><span data-stu-id="f45df-121">If you encounter problems running gulp tasks, you can add hello `--verbose` option for debugging.</span></span> <span data-ttu-id="f45df-122">Повторите tooterminate текущие задачи gulp с помощью `Ctrl + C`, а затем выполнения hello следующую команду в сообщения отладки toosee окна консоли.</span><span class="sxs-lookup"><span data-stu-id="f45df-122">Try tooterminate current gulp tasks by using `Ctrl + C`, and then run hello following command in your console window toosee debug messages.</span></span> <span data-ttu-id="f45df-123">В выходных данных консоли должны отобразиться подробные сообщения об ошибках.</span><span class="sxs-lookup"><span data-stu-id="f45df-123">You might see detailed error messages in your console output.</span></span> 

```bash
gulp --verbose
```

### <a name="device-discovery-issues"></a><span data-ttu-id="f45df-124">Проблемы с обнаружением устройств</span><span class="sxs-lookup"><span data-stu-id="f45df-124">Device discovery issues</span></span>
<span data-ttu-id="f45df-125">Для помощи при устранении типичных проблем с hello `devdisco` команды, проверьте hello [readme](https://github.com/Azure/device-discovery-cli/blob/develop/readme.md).</span><span class="sxs-lookup"><span data-stu-id="f45df-125">For help in troubleshooting common problems with hello `devdisco` command, check hello [readme](https://github.com/Azure/device-discovery-cli/blob/develop/readme.md).</span></span>

### <a name="npm-issues"></a><span data-ttu-id="f45df-126">проблемы с NPM</span><span class="sxs-lookup"><span data-stu-id="f45df-126">NPM issues</span></span>
<span data-ttu-id="f45df-127">Попробуйте tooupdate пакета NPM с hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="f45df-127">Try tooupdate your NPM package with hello following command:</span></span>

```bash
npm install -g npm
```

<span data-ttu-id="f45df-128">Если hello проблема остается, оставьте комментарий в конце hello в этой статье, или создать вопрос GitHub в нашем [репозитории примеров](https://github.com/Azure-Samples/iot-hub-c-raspberrypi-getting-started)</span><span class="sxs-lookup"><span data-stu-id="f45df-128">If hello problem still exists, leave your comments at hello end of this article or create a GitHub issue in our [sample repository](https://github.com/Azure-Samples/iot-hub-c-raspberrypi-getting-started)</span></span>

## <a name="remote-debugging"></a><span data-ttu-id="f45df-129">Удаленная отладка</span><span class="sxs-lookup"><span data-stu-id="f45df-129">Remote debugging</span></span>

<span data-ttu-id="f45df-130">Поддержка удаленной отладки скоро станет доступной в расширении C/C++ для Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="f45df-130">Remote debugging support will be available soon in Visual Studio Code C/C++ Extension.</span></span>

<span data-ttu-id="f45df-131">Кроме того, вы можете использовать инструмент GDB через привычный терминал SSH:</span><span class="sxs-lookup"><span data-stu-id="f45df-131">In a meanwhile you can use GDB via your favourite SSH terminal:</span></span>

```bash
cd c-pi-lesson-x
sudo gdb app
```

## <a name="azure-cli-issues"></a><span data-ttu-id="f45df-132">Проблемы с Azure CLI</span><span class="sxs-lookup"><span data-stu-id="f45df-132">Azure-CLI issues</span></span>
<span data-ttu-id="f45df-133">Hello Azure командной строки (CLI Azure) — это построение предварительного просмотра.</span><span class="sxs-lookup"><span data-stu-id="f45df-133">hello Azure command-line interface (Azure CLI) is a preview build.</span></span> <span data-ttu-id="f45df-134">Искать решение в hello [руководство по установке Preview](https://github.com/Azure/azure-cli/blob/master/doc/preview_install_guide.md) tooseek решения.</span><span class="sxs-lookup"><span data-stu-id="f45df-134">Look for solution in hello [Preview Install Guide](https://github.com/Azure/azure-cli/blob/master/doc/preview_install_guide.md) tooseek solutions.</span></span> <span data-ttu-id="f45df-135">Повторите версии toolatest tooupgrade Azure cli, когда команды не работают должным образом.</span><span class="sxs-lookup"><span data-stu-id="f45df-135">Try tooupgrade Azure-cli toolatest version when commands don’t work as expected.</span></span>

<span data-ttu-id="f45df-136">При возникновении любых ошибок с помощью средства hello файл [проблема](https://github.com/Azure/azure-cli/issues) в hello **проблемы** раздел hello в репозитории GitHub.</span><span class="sxs-lookup"><span data-stu-id="f45df-136">If you encounter any bugs with hello tool, file an [issue](https://github.com/Azure/azure-cli/issues) in hello **Issues** section of hello GitHub repo.</span></span>

<span data-ttu-id="f45df-137">Для получения справки по устранению общих проблем, проверьте hello [readme](https://github.com/Azure/azure-cli/blob/master/README.rst).</span><span class="sxs-lookup"><span data-stu-id="f45df-137">For help troubleshooting common problems, check hello [readme](https://github.com/Azure/azure-cli/blob/master/README.rst).</span></span>

<span data-ttu-id="f45df-138">Если соблюдаются «Не удалось найти версию, которая соответствует требованиям hello», проверьте выполнения hello следующая команда tooupgrade pip toolastest версии.</span><span class="sxs-lookup"><span data-stu-id="f45df-138">If you meet "Could not find a version that satisfies hello requirement", please run hello following command tooupgrade pip toolastest version.</span></span>

```bash
python -m pip install --upgrade pip
```

## <a name="python-installation-issues"></a><span data-ttu-id="f45df-139">Проблемы с установкой Python</span><span class="sxs-lookup"><span data-stu-id="f45df-139">Python installation issues</span></span>
### <a name="legacy-installation-issues-macos"></a><span data-ttu-id="f45df-140">Проблемы с устаревшими установками (macOS)</span><span class="sxs-lookup"><span data-stu-id="f45df-140">Legacy installation issues (macOS)</span></span>
<span data-ttu-id="f45df-141">При установке **pip** возникает ошибка разрешения, если есть устаревшие пакеты, которые устанавливаются с использованием разрешений **su**.</span><span class="sxs-lookup"><span data-stu-id="f45df-141">When you're installing **pip**, a permission error is thrown when older packages that are installed with **su** permissions.</span></span> <span data-ttu-id="f45df-142">Такая ситуация возникает из-за того, что предыдущая установка Python с использованием brew (macOS) удалена не полностью.</span><span class="sxs-lookup"><span data-stu-id="f45df-142">This situation occurs because a previous installation of Python using brew (macOS) is not uninstalled completely.</span></span> <span data-ttu-id="f45df-143">Некоторые **pip** пакеты из предыдущей установки были созданы корневым элементом, который приводит к возникновению ошибки разрешение hello.</span><span class="sxs-lookup"><span data-stu-id="f45df-143">Some **pip** packages from a previous installation were created by root, which causes hello permission error.</span></span> <span data-ttu-id="f45df-144">Здравствуйте, решение является tooremove эти пакеты, установленные корневым элементом.</span><span class="sxs-lookup"><span data-stu-id="f45df-144">hello solution is tooremove those packages installed by root.</span></span> <span data-ttu-id="f45df-145">Используйте следующие шаги toocomplete hello этой задачи:</span><span class="sxs-lookup"><span data-stu-id="f45df-145">Use hello following steps toocomplete this task:</span></span>

1. <span data-ttu-id="f45df-146">Перейдите к папке /usr/local/lib/python2.7/site-packages.</span><span class="sxs-lookup"><span data-stu-id="f45df-146">Go to: /usr/local/lib/python2.7/site-packages</span></span>
2. <span data-ttu-id="f45df-147">Выведите список пакетов, созданных с использованием разрешений корневой папки: `ls -l | grep root`.</span><span class="sxs-lookup"><span data-stu-id="f45df-147">List packages create by root: `ls -l | grep root`</span></span>
3. <span data-ttu-id="f45df-148">Удалите пакеты из шага 2: `sudo rm -rf {package name}`.</span><span class="sxs-lookup"><span data-stu-id="f45df-148">Uninstall packages from step 2: `sudo rm -rf {package name}`</span></span>
4. <span data-ttu-id="f45df-149">Переустановите Python.</span><span class="sxs-lookup"><span data-stu-id="f45df-149">Reinstall Python.</span></span>

## <a name="azure-iot-hub-issues"></a><span data-ttu-id="f45df-150">Проблемы с Центром Интернета вещей Azure</span><span class="sxs-lookup"><span data-stu-id="f45df-150">Azure IoT Hub issues</span></span>
<span data-ttu-id="f45df-151">Если успешной подготовки ваш центр Azure IoT с `azure-cli`, и необходимо, чтобы устройства hello toomanage средство, подключающимися центра IoT tooyour, попробуйте hello следующие средства:</span><span class="sxs-lookup"><span data-stu-id="f45df-151">If you've successfully provisioned your Azure IoT hub with `azure-cli`, and you need a tool toomanage hello devices that are connecting tooyour IoT hub, try hello following tools:</span></span>

### <a name="device-explorer"></a><span data-ttu-id="f45df-152">Обозреватель устройств</span><span class="sxs-lookup"><span data-stu-id="f45df-152">Device Explorer</span></span>
<span data-ttu-id="f45df-153">[Обозреватель устройств](https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer) выполняется на локальном компьютере Windows и подключается tooyour центр IoT в Azure.</span><span class="sxs-lookup"><span data-stu-id="f45df-153">[Device Explorer](https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer) runs on your Windows local machine and connects tooyour IoT hub in Azure.</span></span> <span data-ttu-id="f45df-154">Он взаимодействует с hello следующие [конечные точки центра IoT](iot-hub-devguide.md):</span><span class="sxs-lookup"><span data-stu-id="f45df-154">It communicates with hello following [IoT Hub endpoints](iot-hub-devguide.md):</span></span>

* <span data-ttu-id="f45df-155">*Управление устройствами удостоверения* tooprovision и управления ими устройствах, зарегистрированных в центр IoT.</span><span class="sxs-lookup"><span data-stu-id="f45df-155">*Device identity management* tooprovision and manage devices registered with your IoT hub.</span></span>
* <span data-ttu-id="f45df-156">*Получение устройства в облако* можно наблюдать за сообщений, отправленных из центра IoT tooyour вашего устройства.</span><span class="sxs-lookup"><span data-stu-id="f45df-156">*Receive device-to-cloud* so you can monitor messages sent from your device tooyour IoT hub.</span></span>
* <span data-ttu-id="f45df-157">*Отправить облака на устройство* для отправки сообщений tooyour устройств из вашего центра IoT.</span><span class="sxs-lookup"><span data-stu-id="f45df-157">*Send cloud-to-device* so you can send messages tooyour devices from your IoT hub.</span></span>

<span data-ttu-id="f45df-158">Настройка вашего `IoT hub connection string` в этот инструмент toouse его возможности.</span><span class="sxs-lookup"><span data-stu-id="f45df-158">Configure your `IoT hub connection string` within this tool toouse all its capabilities.</span></span>

### <a name="iot-hub-explorer"></a><span data-ttu-id="f45df-159">Обозреватель Центра Интернета вещей</span><span class="sxs-lookup"><span data-stu-id="f45df-159">IoT hub Explorer</span></span>
<span data-ttu-id="f45df-160">[Центр IoT Explorer](https://github.com/Azure/iothub-explorer) -это средство многоплатформенного CLI образец toomanage клиентов устройств.</span><span class="sxs-lookup"><span data-stu-id="f45df-160">[IoT hub Explorer](https://github.com/Azure/iothub-explorer) is a sample multiplatform CLI tool toomanage device clients.</span></span> <span data-ttu-id="f45df-161">Можно использовать hello средство toomanage hello устройства в реестре удостоверений hello, отслеживать сообщения из устройства в облако и отправлять команды облака на устройство.</span><span class="sxs-lookup"><span data-stu-id="f45df-161">You can use hello tool toomanage hello devices in hello identity registry, monitor device-to-cloud messages, and send cloud-to-device commands.</span></span>

<span data-ttu-id="f45df-162">tooinstall hello последняя (Предварительная) версия hello центром IOT-анализатор, запустите следующую команду в среде командной строки hello:</span><span class="sxs-lookup"><span data-stu-id="f45df-162">tooinstall hello latest (prerelease) version of hello iothub-explorer tool, run hello following command in your command-line environment:</span></span>

```
npm install -g iothub-explorer@latest
```

<span data-ttu-id="f45df-163">Можно использовать следующую команду, tooget дополнительную справку обо всех hello центром IOT обозреватель команды и их параметрах hello.</span><span class="sxs-lookup"><span data-stu-id="f45df-163">You can use hello following command tooget additional help about all hello iothub-explorer commands and their parameters:</span></span>

```bash
iothub-explorer help
```

### <a name="azure-portal"></a><span data-ttu-id="f45df-164">Портал Azure</span><span class="sxs-lookup"><span data-stu-id="f45df-164">Azure portal</span></span>
<span data-ttu-id="f45df-165">Все возможности интерфейса командной строки помогают создавать все ресурсы Azure и управлять ими.</span><span class="sxs-lookup"><span data-stu-id="f45df-165">A full CLI experience helps you create and manage all your Azure resources.</span></span> <span data-ttu-id="f45df-166">Можно также toouse hello [портал Azure](../azure-portal-overview.md) toohelp подготовки, управления и отладки ресурсам Azure.</span><span class="sxs-lookup"><span data-stu-id="f45df-166">You might also want toouse hello [Azure portal](../azure-portal-overview.md) toohelp provision, manage, and debug your Azure resources.</span></span>

## <a name="azure-storage-issues"></a><span data-ttu-id="f45df-167">Проблемы со службой хранилища Azure</span><span class="sxs-lookup"><span data-stu-id="f45df-167">Azure storage issues</span></span>
<span data-ttu-id="f45df-168">[Обозреватель хранилищ Microsoft Azure (Предварительная версия)](http://storageexplorer.com) имеет отдельное приложение от Майкрософт, можно использовать toowork с данных из хранилища Azure в Windows, macOS и Linux.</span><span class="sxs-lookup"><span data-stu-id="f45df-168">[Microsoft Azure Storage Explorer (preview)](http://storageexplorer.com) is a standalone app from Microsoft that you can use toowork with Azure Storage data on Windows, macOS, and Linux.</span></span> <span data-ttu-id="f45df-169">С ее помощью можно подключиться tooyour таблицы и просмотра данных hello.</span><span class="sxs-lookup"><span data-stu-id="f45df-169">By using this tool, you can connect tooyour table and see hello data in it.</span></span> <span data-ttu-id="f45df-170">Можно использовать этот инструмент tootroubleshoot вашей проблемы хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="f45df-170">You can use this tool tootroubleshoot your Azure Storage issues.</span></span>
