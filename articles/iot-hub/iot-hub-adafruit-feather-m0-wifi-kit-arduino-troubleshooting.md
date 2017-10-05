---
title: "Подключение Arduino (C) к Интернету вещей Azure. Устранение неполадок | Документация Майкрософт"
description: "Страница со сведениями об устранении неполадок в работе Adafruit Feather M0 WiFi Arduino"
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "Устранение неполадок Arduino"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-adafruit-feather-m0-wifi-kit-arduino-get-started
ms.assetid: fdcc56ff-4420-463c-8a0e-5a1d215a874f
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 3bb369da9148300a80e7d351522a4d908e926996
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshooting"></a><span data-ttu-id="ba756-104">Устранение неполадок</span><span class="sxs-lookup"><span data-stu-id="ba756-104">Troubleshooting</span></span>
## <a name="hardware-issues"></a><span data-ttu-id="ba756-105">Проблемы с оборудованием</span><span class="sxs-lookup"><span data-stu-id="ba756-105">Hardware issues</span></span>
<span data-ttu-id="ba756-106">Сведения об устранении распространенных проблем на плате Adafruit Feather M0 WiFi Arduino см. на [этой официальной странице](https://learn.adafruit.com/adafruit-feather-m0-wifi-atwinc1500?view=all#faq).</span><span class="sxs-lookup"><span data-stu-id="ba756-106">For information about solving common problems on your Adafruit Feather M0 WiFi Arduino board, see the [official troubleshooting page](https://learn.adafruit.com/adafruit-feather-m0-wifi-atwinc1500?view=all#faq).</span></span>

## <a name="nodejs-package-issues"></a><span data-ttu-id="ba756-107">Проблемы с пакетами Node.js</span><span class="sxs-lookup"><span data-stu-id="ba756-107">Node.js package issues</span></span>
### <a name="no-response-during-gulp-tasks"></a><span data-ttu-id="ba756-108">Нет ответа при выполнении задач Gulp</span><span class="sxs-lookup"><span data-stu-id="ba756-108">No response during gulp tasks</span></span>
<span data-ttu-id="ba756-109">Если при выполнении задач Gulp возникли проблемы, можно добавить параметр `--verbose` для отладки.</span><span class="sxs-lookup"><span data-stu-id="ba756-109">If you encounter problems running gulp tasks, you can add the `--verbose` option for debugging.</span></span> <span data-ttu-id="ba756-110">Попробуйте завершить текущие задачи Gulp, используя клавиши `Ctrl + C`, а затем выполните следующую команду в окне консоли, чтобы просмотреть сообщения отладки.</span><span class="sxs-lookup"><span data-stu-id="ba756-110">Try to terminate current gulp tasks by using `Ctrl + C`, and then run the following command in your console window to see debug messages.</span></span> <span data-ttu-id="ba756-111">В выходных данных консоли должны отобразиться подробные сообщения об ошибках.</span><span class="sxs-lookup"><span data-stu-id="ba756-111">You might see detailed error messages in your console output.</span></span>

```bash
gulp --verbose
```

<span data-ttu-id="ba756-112">Или можно добавить `--listen`, чтобы открыть последовательный порт для вывода информации журнала устройства.</span><span class="sxs-lookup"><span data-stu-id="ba756-112">Or you can add `--listen` to open serial port to output device log information.</span></span>

```bash
gulp --listen
``` 

### <a name="npm-issues"></a><span data-ttu-id="ba756-113">Проблемы с NPM</span><span class="sxs-lookup"><span data-stu-id="ba756-113">NPM issues</span></span>
<span data-ttu-id="ba756-114">Попробуйте обновить пакет NPM, выполнив следующую команду:</span><span class="sxs-lookup"><span data-stu-id="ba756-114">Try to update your NPM package with the following command:</span></span>

```bash
npm install -g npm
```

<span data-ttu-id="ba756-115">Если проблема не исчезла, оставьте комментарии в конце этой статьи или задайте вопрос о проблеме в GitHub в нашем [примере репозитория][sample-repository].</span><span class="sxs-lookup"><span data-stu-id="ba756-115">If the problem still exists, leave your comments at the end of this article or create a GitHub issue in our [sample repository][sample-repository].</span></span>

## <a name="azure-cli-issues"></a><span data-ttu-id="ba756-116">Проблемы с Azure CLI</span><span class="sxs-lookup"><span data-stu-id="ba756-116">Azure-CLI issues</span></span>
<span data-ttu-id="ba756-117">Интерфейс командной строки Azure (Azure CLI) — это сборка предварительной версии.</span><span class="sxs-lookup"><span data-stu-id="ba756-117">The Azure command-line interface (Azure CLI) is a preview build.</span></span> <span data-ttu-id="ba756-118">Решения можно найти в [руководстве по установке предварительной версии](https://github.com/Azure/azure-cli/blob/master/doc/preview_install_guide.md).</span><span class="sxs-lookup"><span data-stu-id="ba756-118">Look for solution in the [Preview Install Guide](https://github.com/Azure/azure-cli/blob/master/doc/preview_install_guide.md) to seek solutions.</span></span> <span data-ttu-id="ba756-119">Попытайтесь обновить Azure CLI до последней версии, если команда не работает должным образом.</span><span class="sxs-lookup"><span data-stu-id="ba756-119">Try to upgrade Azure-cli to latest version when commands don’t work as expected.</span></span>

<span data-ttu-id="ba756-120">При появлении ошибок в средстве сообщите о [проблеме](https://github.com/Azure/azure-cli/issues) в разделе **Проблемы** репозитория GitHub.</span><span class="sxs-lookup"><span data-stu-id="ba756-120">If you encounter any bugs with the tool, file an [issue](https://github.com/Azure/azure-cli/issues) in the **Issues** section of the GitHub repo.</span></span>

<span data-ttu-id="ba756-121">Справку по устранению распространенных проблем см. в [файле сведений](https://github.com/Azure/azure-cli/blob/master/README.rst).</span><span class="sxs-lookup"><span data-stu-id="ba756-121">For help troubleshooting common problems, check the [readme](https://github.com/Azure/azure-cli/blob/master/README.rst).</span></span>

<span data-ttu-id="ba756-122">При появлении сообщения "Не удалось найти версию, которая удовлетворяет требованиям" выполните следующую команду, чтобы обновить pip до последней версии.</span><span class="sxs-lookup"><span data-stu-id="ba756-122">If you meet "Could not find a version that satisfies the requirement", please run the following command to upgrade pip to lastest version.</span></span>

```bash
python -m pip install --upgrade pip
```

## <a name="python-installation-issues"></a><span data-ttu-id="ba756-123">Проблемы с установкой Python</span><span class="sxs-lookup"><span data-stu-id="ba756-123">Python installation issues</span></span>
### <a name="legacy-installation-issues-macos"></a><span data-ttu-id="ba756-124">Проблемы с устаревшими установками (macOS)</span><span class="sxs-lookup"><span data-stu-id="ba756-124">Legacy installation issues (macOS)</span></span>
<span data-ttu-id="ba756-125">При установке **pip** возникает ошибка разрешения, если есть устаревшие пакеты, которые устанавливаются с использованием разрешений **su**.</span><span class="sxs-lookup"><span data-stu-id="ba756-125">When you're installing **pip**, a permission error is thrown when older packages that are installed with **su** permissions.</span></span> <span data-ttu-id="ba756-126">Такая ситуация возникает из-за того, что предыдущая установка Python с использованием brew (macOS) удалена не полностью.</span><span class="sxs-lookup"><span data-stu-id="ba756-126">This situation occurs because a previous installation of Python using brew (macOS) is not uninstalled completely.</span></span> <span data-ttu-id="ba756-127">Некоторые пакеты **pip** из предыдущей установки созданы с помощью разрешений корневой папки, что приводит к ошибке разрешения.</span><span class="sxs-lookup"><span data-stu-id="ba756-127">Some **pip** packages from a previous installation were created by root, which causes the permission error.</span></span> <span data-ttu-id="ba756-128">Чтобы решить эту проблему, необходимо удалить эти пакеты, установленные с помощью разрешений корневой папки.</span><span class="sxs-lookup"><span data-stu-id="ba756-128">The solution is to remove those packages installed by root.</span></span> <span data-ttu-id="ba756-129">Для этого необходимо сделать следующее:</span><span class="sxs-lookup"><span data-stu-id="ba756-129">Use the following steps to complete this task:</span></span>

1. <span data-ttu-id="ba756-130">Перейдите к папке /usr/local/lib/python2.7/site-packages.</span><span class="sxs-lookup"><span data-stu-id="ba756-130">Go to: /usr/local/lib/python2.7/site-packages</span></span>
2. <span data-ttu-id="ba756-131">Выведите список пакетов, созданных с использованием разрешений корневой папки: `ls -l | grep root`.</span><span class="sxs-lookup"><span data-stu-id="ba756-131">List packages create by root: `ls -l | grep root`</span></span>
3. <span data-ttu-id="ba756-132">Удалите пакеты из шага 2: `sudo rm -rf {package name}`.</span><span class="sxs-lookup"><span data-stu-id="ba756-132">Uninstall packages from step 2: `sudo rm -rf {package name}`</span></span>
4. <span data-ttu-id="ba756-133">Переустановите Python.</span><span class="sxs-lookup"><span data-stu-id="ba756-133">Reinstall Python.</span></span>

## <a name="azure-iot-hub-issues"></a><span data-ttu-id="ba756-134">Проблемы с Центром Интернета вещей Azure</span><span class="sxs-lookup"><span data-stu-id="ba756-134">Azure IoT Hub issues</span></span>
<span data-ttu-id="ba756-135">Если Центр Интернета вещей Azure успешно подготовлен с помощью `azure-cli` и требуется инструмент для управления устройствами, подключенными к вашему Центру Интернета вещей, воспользуйтесь следующими инструментами:</span><span class="sxs-lookup"><span data-stu-id="ba756-135">If you've successfully provisioned your Azure IoT hub with `azure-cli`, and you need a tool to manage the devices that are connecting to your IoT hub, try the following tools:</span></span>

### <a name="device-explorer"></a><span data-ttu-id="ba756-136">Обозреватель устройств</span><span class="sxs-lookup"><span data-stu-id="ba756-136">Device Explorer</span></span>
<span data-ttu-id="ba756-137">[Обозреватель устройств](https://github.com/Azure/azure-iot-sdk-csharp/tree/master/tools/DeviceExplorer) работает на локальном компьютере Windows и подключается к Центру Интернета вещей в Azure.</span><span class="sxs-lookup"><span data-stu-id="ba756-137">[Device Explorer](https://github.com/Azure/azure-iot-sdk-csharp/tree/master/tools/DeviceExplorer) runs on your Windows local machine and connects to your IoT hub in Azure.</span></span> <span data-ttu-id="ba756-138">Он взаимодействует со следующими [конечными точками Центра Интернета вещей](iot-hub-devguide.md):</span><span class="sxs-lookup"><span data-stu-id="ba756-138">It communicates with the following [IoT Hub endpoints](iot-hub-devguide.md):</span></span>

* <span data-ttu-id="ba756-139">*управление удостоверениями устройств* для подготовки устройств, зарегистрированных в Центре Интернета вещей, и управления ими;</span><span class="sxs-lookup"><span data-stu-id="ba756-139">*Device identity management* to provision and manage devices registered with your IoT hub.</span></span>
* <span data-ttu-id="ba756-140">*получение сообщений с устройства в облако*, что позволяет отслеживать сообщения, отправляемые с устройства в Центр Интернета вещей;</span><span class="sxs-lookup"><span data-stu-id="ba756-140">*Receive device-to-cloud* so you can monitor messages sent from your device to your IoT hub.</span></span>
* <span data-ttu-id="ba756-141">*отправка сообщений из облака на устройство*, что позволяет отправлять сообщения на устройства из вашего Центра Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="ba756-141">*Send cloud-to-device* so you can send messages to your devices from your IoT hub.</span></span>

<span data-ttu-id="ba756-142">Настройте свою `IoT hub connection string` в этом инструменте, чтобы использовать его возможности.</span><span class="sxs-lookup"><span data-stu-id="ba756-142">Configure your `IoT hub connection string` within this tool to use all its capabilities.</span></span>

### <a name="iot-hub-explorer"></a><span data-ttu-id="ba756-143">Обозреватель Центра Интернета вещей</span><span class="sxs-lookup"><span data-stu-id="ba756-143">IoT hub Explorer</span></span>
<span data-ttu-id="ba756-144">[Обозреватель Центра Интернета вещей](https://github.com/Azure/iothub-explorer) — это пример мультиплатформенного инструмента интерфейса командной строки для управления клиентами устройств.</span><span class="sxs-lookup"><span data-stu-id="ba756-144">[IoT hub Explorer](https://github.com/Azure/iothub-explorer) is a sample multiplatform CLI tool to manage device clients.</span></span> <span data-ttu-id="ba756-145">Инструмент можно использовать для управления устройствами в реестре удостоверений, мониторинга сообщений, отправляемых с устройства в облако, и отправки команд, передаваемых из облака на устройство.</span><span class="sxs-lookup"><span data-stu-id="ba756-145">You can use the tool to manage the devices in the identity registry, monitor device-to-cloud messages, and send cloud-to-device commands.</span></span>


<span data-ttu-id="ba756-146">Чтобы установить последнюю версию (предварительную версию) инструмента iothub-explorer, выполните следующую команду в среде командной строки:</span><span class="sxs-lookup"><span data-stu-id="ba756-146">To install the latest (prerelease) version of the iothub-explorer tool, run the following command in your command-line environment:</span></span>

```bash
npm install -g iothub-explorer@latest
```

<span data-ttu-id="ba756-147">Дополнительную справку о всех командах iothub-explorer и их параметрах можно получить, выполнив следующую команду:</span><span class="sxs-lookup"><span data-stu-id="ba756-147">You can use the following command to get additional help about all the iothub-explorer commands and their parameters:</span></span>

```bash
iothub-explorer help
```

### <a name="azure-portal"></a><span data-ttu-id="ba756-148">Портал Azure</span><span class="sxs-lookup"><span data-stu-id="ba756-148">Azure portal</span></span>
<span data-ttu-id="ba756-149">Все возможности интерфейса командной строки помогают создавать все ресурсы Azure и управлять ими.</span><span class="sxs-lookup"><span data-stu-id="ba756-149">A full CLI experience helps you create and manage all your Azure resources.</span></span> <span data-ttu-id="ba756-150">Для подготовки, отладки ресурсов Azure и управления ими можно также воспользоваться [порталом Azure](../azure-portal-overview.md).</span><span class="sxs-lookup"><span data-stu-id="ba756-150">You might also want to use the [Azure portal](../azure-portal-overview.md) to help provision, manage, and debug your Azure resources.</span></span>

## <a name="azure-storage-issues"></a><span data-ttu-id="ba756-151">Проблемы со службой хранилища Azure</span><span class="sxs-lookup"><span data-stu-id="ba756-151">Azure storage issues</span></span>
<span data-ttu-id="ba756-152">[Обозреватель служб хранилища Microsoft Azure (предварительная версия)](http://storageexplorer.com) — это автономное приложение от корпорации Майкрософт, которое можно использовать для работы с данными из службы хранилища Azure на платформе Windows, macOS и Linux.</span><span class="sxs-lookup"><span data-stu-id="ba756-152">[Microsoft Azure Storage Explorer (preview)](http://storageexplorer.com) is a standalone app from Microsoft that you can use to work with Azure Storage data on Windows, macOS, and Linux.</span></span> <span data-ttu-id="ba756-153">Используя этот инструмент, можно подключаться к таблице и просматривать данные в ней.</span><span class="sxs-lookup"><span data-stu-id="ba756-153">By using this tool, you can connect to your table and see the data in it.</span></span> <span data-ttu-id="ba756-154">Его можно использовать для устранения неполадок в вашей службе хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="ba756-154">You can use this tool to troubleshoot your Azure Storage issues.</span></span>

<!-- Images and links -->

[sample-repository]: https://github.com/Azure/azure-cli/blob/master/doc/preview_install_guide.md