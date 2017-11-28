---
title: "Подключение Intel Edison (C) к Интернету вещей Azure. Устранение неполадок | Документация Майкрософт"
description: "Страница со сведениями об устранении неполадок в работе Intel Edison C"
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "устранение неполадок Arduino"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-c-get-started
ms.assetid: fe20f2fe-490c-4910-82e1-578ed504ae86
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: dd6338ad29e0bb858c33e5bb24b8f41d3c22575a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshooting"></a><span data-ttu-id="19aee-104">Устранение неполадок</span><span class="sxs-lookup"><span data-stu-id="19aee-104">Troubleshooting</span></span>
## <a name="hardware-issues"></a><span data-ttu-id="19aee-105">Проблемы с оборудованием</span><span class="sxs-lookup"><span data-stu-id="19aee-105">Hardware issues</span></span>
<span data-ttu-id="19aee-106">Сведения об устранении распространенных проблем на устройстве Intel Edison см. на [этой официальной странице](https://software.intel.com/en-us/node/637974).</span><span class="sxs-lookup"><span data-stu-id="19aee-106">For information about solving common problems on Intel Edison, see the [official troubleshooting page](https://software.intel.com/en-us/node/637974).</span></span>

## <a name="nodejs-package-issues"></a><span data-ttu-id="19aee-107">Проблемы с пакетами Node.js</span><span class="sxs-lookup"><span data-stu-id="19aee-107">Node.js package issues</span></span>
### <a name="no-response-during-gulp-tasks"></a><span data-ttu-id="19aee-108">Нет ответа при выполнении задач Gulp</span><span class="sxs-lookup"><span data-stu-id="19aee-108">No response during gulp tasks</span></span>
<span data-ttu-id="19aee-109">Если при выполнении задач Gulp возникли проблемы, можно добавить параметр `--verbose` для отладки.</span><span class="sxs-lookup"><span data-stu-id="19aee-109">If you encounter problems running gulp tasks, you can add the `--verbose` option for debugging.</span></span> <span data-ttu-id="19aee-110">Попробуйте завершить текущие задачи Gulp, используя клавиши `Ctrl + C`, а затем выполните следующую команду в окне консоли, чтобы просмотреть сообщения отладки.</span><span class="sxs-lookup"><span data-stu-id="19aee-110">Try to terminate current gulp tasks by using `Ctrl + C`, and then run the following command in your console window to see debug messages.</span></span> <span data-ttu-id="19aee-111">В выходных данных консоли должны отобразиться подробные сообщения об ошибках.</span><span class="sxs-lookup"><span data-stu-id="19aee-111">You might see detailed error messages in your console output.</span></span> 

```bash
gulp --verbose
```

### <a name="npm-issues"></a><span data-ttu-id="19aee-112">проблемы с NPM</span><span class="sxs-lookup"><span data-stu-id="19aee-112">NPM issues</span></span>
<span data-ttu-id="19aee-113">Попробуйте обновить пакет NPM, выполнив следующую команду:</span><span class="sxs-lookup"><span data-stu-id="19aee-113">Try to update your NPM package with the following command:</span></span>

```bash
npm install -g npm
```

<span data-ttu-id="19aee-114">Если проблема не исчезла, оставьте комментарии в конце этой статьи или задайте вопрос о проблеме в GitHub в нашем [примере репозитория][sample-repository].</span><span class="sxs-lookup"><span data-stu-id="19aee-114">If the problem still exists, leave your comments at the end of this article or create a GitHub issue in our [sample repository][sample-repository].</span></span>

## <a name="azure-cli-issues"></a><span data-ttu-id="19aee-115">Проблемы с Azure CLI</span><span class="sxs-lookup"><span data-stu-id="19aee-115">Azure-CLI issues</span></span>
<span data-ttu-id="19aee-116">Интерфейс командной строки Azure (Azure CLI) — это сборка предварительной версии.</span><span class="sxs-lookup"><span data-stu-id="19aee-116">The Azure command-line interface (Azure CLI) is a preview build.</span></span> <span data-ttu-id="19aee-117">Решения можно найти в [руководстве по установке предварительной версии](https://github.com/Azure/azure-cli/blob/master/doc/preview_install_guide.md).</span><span class="sxs-lookup"><span data-stu-id="19aee-117">Look for solution in the [Preview Install Guide](https://github.com/Azure/azure-cli/blob/master/doc/preview_install_guide.md) to seek solutions.</span></span> <span data-ttu-id="19aee-118">Попытайтесь обновить Azure CLI до последней версии, если команда не работает должным образом.</span><span class="sxs-lookup"><span data-stu-id="19aee-118">Try to upgrade Azure-cli to latest version when commands don’t work as expected.</span></span>

<span data-ttu-id="19aee-119">При появлении ошибок в средстве сообщите о [проблеме](https://github.com/Azure/azure-cli/issues) в разделе **Проблемы** репозитория GitHub.</span><span class="sxs-lookup"><span data-stu-id="19aee-119">If you encounter any bugs with the tool, file an [issue](https://github.com/Azure/azure-cli/issues) in the **Issues** section of the GitHub repo.</span></span>

<span data-ttu-id="19aee-120">Справку по устранению распространенных проблем см. в [файле сведений](https://github.com/Azure/azure-cli/blob/master/README.rst).</span><span class="sxs-lookup"><span data-stu-id="19aee-120">For help troubleshooting common problems, check the [readme](https://github.com/Azure/azure-cli/blob/master/README.rst).</span></span>

<span data-ttu-id="19aee-121">При появлении сообщения "Не удалось найти версию, которая удовлетворяет требованиям" выполните следующую команду, чтобы обновить pip до последней версии.</span><span class="sxs-lookup"><span data-stu-id="19aee-121">If you meet "Could not find a version that satisfies the requirement", please run the following command to upgrade pip to lastest version.</span></span>

```bash
python -m pip install --upgrade pip
```

## <a name="python-installation-issues"></a><span data-ttu-id="19aee-122">Проблемы с установкой Python</span><span class="sxs-lookup"><span data-stu-id="19aee-122">Python installation issues</span></span>
### <a name="legacy-installation-issues-macos"></a><span data-ttu-id="19aee-123">Проблемы с устаревшими установками (macOS)</span><span class="sxs-lookup"><span data-stu-id="19aee-123">Legacy installation issues (macOS)</span></span>
<span data-ttu-id="19aee-124">При установке **pip** возникает ошибка разрешения, если есть устаревшие пакеты, которые устанавливаются с использованием разрешений **su**.</span><span class="sxs-lookup"><span data-stu-id="19aee-124">When you're installing **pip**, a permission error is thrown when older packages that are installed with **su** permissions.</span></span> <span data-ttu-id="19aee-125">Такая ситуация возникает из-за того, что предыдущая установка Python с использованием brew (macOS) удалена не полностью.</span><span class="sxs-lookup"><span data-stu-id="19aee-125">This situation occurs because a previous installation of Python using brew (macOS) is not uninstalled completely.</span></span> <span data-ttu-id="19aee-126">Некоторые пакеты **pip** из предыдущей установки созданы с помощью разрешений корневой папки, что приводит к ошибке разрешения.</span><span class="sxs-lookup"><span data-stu-id="19aee-126">Some **pip** packages from a previous installation were created by root, which causes the permission error.</span></span> <span data-ttu-id="19aee-127">Чтобы решить эту проблему, необходимо удалить эти пакеты, установленные с помощью разрешений корневой папки.</span><span class="sxs-lookup"><span data-stu-id="19aee-127">The solution is to remove those packages installed by root.</span></span> <span data-ttu-id="19aee-128">Для этого необходимо сделать следующее:</span><span class="sxs-lookup"><span data-stu-id="19aee-128">Use the following steps to complete this task:</span></span>

1. <span data-ttu-id="19aee-129">Перейдите к папке /usr/local/lib/python2.7/site-packages.</span><span class="sxs-lookup"><span data-stu-id="19aee-129">Go to: /usr/local/lib/python2.7/site-packages</span></span>
2. <span data-ttu-id="19aee-130">Выведите список пакетов, созданных с использованием разрешений корневой папки: `ls -l | grep root`.</span><span class="sxs-lookup"><span data-stu-id="19aee-130">List packages create by root: `ls -l | grep root`</span></span>
3. <span data-ttu-id="19aee-131">Удалите пакеты из шага 2: `sudo rm -rf {package name}`.</span><span class="sxs-lookup"><span data-stu-id="19aee-131">Uninstall packages from step 2: `sudo rm -rf {package name}`</span></span>
4. <span data-ttu-id="19aee-132">Переустановите Python.</span><span class="sxs-lookup"><span data-stu-id="19aee-132">Reinstall Python.</span></span>

## <a name="azure-iot-hub-issues"></a><span data-ttu-id="19aee-133">Проблемы с Центром Интернета вещей Azure</span><span class="sxs-lookup"><span data-stu-id="19aee-133">Azure IoT Hub issues</span></span>
<span data-ttu-id="19aee-134">Если Центр Интернета вещей Azure успешно подготовлен с помощью `azure-cli` и требуется инструмент для управления устройствами, подключенными к вашему Центру Интернета вещей, воспользуйтесь следующими инструментами:</span><span class="sxs-lookup"><span data-stu-id="19aee-134">If you've successfully provisioned your Azure IoT hub with `azure-cli`, and you need a tool to manage the devices that are connecting to your IoT hub, try the following tools:</span></span>

### <a name="device-explorer"></a><span data-ttu-id="19aee-135">Обозреватель устройств</span><span class="sxs-lookup"><span data-stu-id="19aee-135">Device Explorer</span></span>
<span data-ttu-id="19aee-136">[Обозреватель устройств](https://github.com/Azure/azure-iot-sdk-csharp/tree/master/tools/DeviceExplorer) работает на локальном компьютере Windows и подключается к Центру Интернета вещей в Azure.</span><span class="sxs-lookup"><span data-stu-id="19aee-136">[Device Explorer](https://github.com/Azure/azure-iot-sdk-csharp/tree/master/tools/DeviceExplorer) runs on your Windows local machine and connects to your IoT hub in Azure.</span></span> <span data-ttu-id="19aee-137">Он взаимодействует со следующими [конечными точками Центра Интернета вещей](iot-hub-devguide.md):</span><span class="sxs-lookup"><span data-stu-id="19aee-137">It communicates with the following [IoT Hub endpoints](iot-hub-devguide.md):</span></span>

- <span data-ttu-id="19aee-138">_управление удостоверениями устройств_ для подготовки устройств, зарегистрированных в Центре Интернета вещей, и управления ими;</span><span class="sxs-lookup"><span data-stu-id="19aee-138">_Device identity management_ to provision and manage devices registered with your IoT hub.</span></span>
- <span data-ttu-id="19aee-139">_получение сообщений с устройства в облако_, что позволяет отслеживать сообщения, отправляемые с устройства в Центр Интернета вещей;</span><span class="sxs-lookup"><span data-stu-id="19aee-139">_Receive device-to-cloud_ so you can monitor messages sent from your device to your IoT hub.</span></span>
- <span data-ttu-id="19aee-140">_отправка сообщений из облака на устройство_, что позволяет отправлять сообщения на устройства из вашего Центра Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="19aee-140">_Send cloud-to-device_ so you can send messages to your devices from your IoT hub.</span></span>

<span data-ttu-id="19aee-141">Настройте свою `IoT hub connection string` в этом инструменте, чтобы использовать его возможности.</span><span class="sxs-lookup"><span data-stu-id="19aee-141">Configure your `IoT hub connection string` within this tool to use all its capabilities.</span></span>

### <a name="iot-hub-explorer"></a><span data-ttu-id="19aee-142">Обозреватель Центра Интернета вещей</span><span class="sxs-lookup"><span data-stu-id="19aee-142">IoT hub Explorer</span></span>
<span data-ttu-id="19aee-143">[Обозреватель Центра Интернета вещей](https://github.com/Azure/iothub-explorer) — это пример мультиплатформенного инструмента интерфейса командной строки для управления клиентами устройств.</span><span class="sxs-lookup"><span data-stu-id="19aee-143">[IoT hub Explorer](https://github.com/Azure/iothub-explorer) is a sample multiplatform CLI tool to manage device clients.</span></span> <span data-ttu-id="19aee-144">Инструмент можно использовать для управления устройствами в реестре удостоверений, мониторинга сообщений, отправляемых с устройства в облако, и отправки команд, передаваемых из облака на устройство.</span><span class="sxs-lookup"><span data-stu-id="19aee-144">You can use the tool to manage the devices in the identity registry, monitor device-to-cloud messages, and send cloud-to-device commands.</span></span>

<span data-ttu-id="19aee-145">Чтобы установить последнюю версию (предварительную версию) инструмента iothub-explorer, выполните следующую команду в среде командной строки:</span><span class="sxs-lookup"><span data-stu-id="19aee-145">To install the latest (prerelease) version of the iothub-explorer tool, run the following command in your command-line environment:</span></span>

```bash
npm install -g iothub-explorer@latest
```

<span data-ttu-id="19aee-146">Дополнительную справку о всех командах iothub-explorer и их параметрах можно получить, выполнив следующую команду:</span><span class="sxs-lookup"><span data-stu-id="19aee-146">You can use the following command to get additional help about all the iothub-explorer commands and their parameters:</span></span>

```bash
iothub-explorer help
```

### <a name="azure-portal"></a><span data-ttu-id="19aee-147">Портал Azure</span><span class="sxs-lookup"><span data-stu-id="19aee-147">Azure portal</span></span>
<span data-ttu-id="19aee-148">Все возможности интерфейса командной строки помогают создавать все ресурсы Azure и управлять ими.</span><span class="sxs-lookup"><span data-stu-id="19aee-148">A full CLI experience helps you create and manage all your Azure resources.</span></span> <span data-ttu-id="19aee-149">Для подготовки, отладки ресурсов Azure и управления ими можно также воспользоваться [порталом Azure](../azure-portal-overview.md).</span><span class="sxs-lookup"><span data-stu-id="19aee-149">You might also want to use the [Azure portal](../azure-portal-overview.md) to help provision, manage, and debug your Azure resources.</span></span>

## <a name="azure-storage-issues"></a><span data-ttu-id="19aee-150">Проблемы со службой хранилища Azure</span><span class="sxs-lookup"><span data-stu-id="19aee-150">Azure storage issues</span></span>
<span data-ttu-id="19aee-151">[Обозреватель служб хранилища Microsoft Azure (предварительная версия)](http://storageexplorer.com) — это автономное приложение от корпорации Майкрософт, которое можно использовать для работы с данными из [службы хранилища Azure](https://azure.microsoft.com/en-us/services/storage/) на платформе Windows, macOS и Linux.</span><span class="sxs-lookup"><span data-stu-id="19aee-151">[Microsoft Azure Storage Explorer (preview)](http://storageexplorer.com) is a standalone app from Microsoft that you can use to work with [Azure Storage](https://azure.microsoft.com/en-us/services/storage/) data on Windows, macOS, and Linux.</span></span> <span data-ttu-id="19aee-152">Используя этот инструмент, можно подключаться к таблице и просматривать данные в ней.</span><span class="sxs-lookup"><span data-stu-id="19aee-152">By using this tool, you can connect to your table and see the data in it.</span></span> <span data-ttu-id="19aee-153">Его можно использовать для устранения неполадок в вашей службе хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="19aee-153">You can use this tool to troubleshoot your Azure Storage issues.</span></span>

## <a name="next-steps"></a><span data-ttu-id="19aee-154">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="19aee-154">Next steps</span></span>
<span data-ttu-id="19aee-155">На этой странице приведены только наиболее распространенные проблемы с набором Intel Edison.</span><span class="sxs-lookup"><span data-stu-id="19aee-155">This page only includes the most common problems of Intel Edison kit.</span></span> <span data-ttu-id="19aee-156">Вы также можете оставить комментарии внизу страницы, чтобы сообщить о проблемах для дальнейшего устранения неполадок.</span><span class="sxs-lookup"><span data-stu-id="19aee-156">You can also leave bottom comments to report issues for further troubleshooting.</span></span>

<span data-ttu-id="19aee-157">Вернитесь к изучению статьи [Начало работы с Intel Edison (Node.js)](iot-hub-intel-edison-kit-c-get-started.md)</span><span class="sxs-lookup"><span data-stu-id="19aee-157">Go back to [Get started with Intel Edison (C)](iot-hub-intel-edison-kit-c-get-started.md)</span></span>

<!-- Images and links -->

[sample-repository]: https://github.com/Azure-Samples/iot-hub-c-edison-getting-started