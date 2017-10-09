---
title: "Connect Intel Edison (C) tooAzure IoT — Устранение неполадок | Документы Microsoft"
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
ms.openlocfilehash: c4a71983e3906cfc5ce7c832cf858852b9bd744a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting"></a><span data-ttu-id="a390f-104">Устранение неполадок</span><span class="sxs-lookup"><span data-stu-id="a390f-104">Troubleshooting</span></span>
## <a name="hardware-issues"></a><span data-ttu-id="a390f-105">Проблемы с оборудованием</span><span class="sxs-lookup"><span data-stu-id="a390f-105">Hardware issues</span></span>
<span data-ttu-id="a390f-106">Сведения об устранении типичных проблем на Intel Edison см. в разделе hello [официальный по устранению неполадок страницы](https://software.intel.com/en-us/node/637974).</span><span class="sxs-lookup"><span data-stu-id="a390f-106">For information about solving common problems on Intel Edison, see hello [official troubleshooting page](https://software.intel.com/en-us/node/637974).</span></span>

## <a name="nodejs-package-issues"></a><span data-ttu-id="a390f-107">Проблемы с пакетами Node.js</span><span class="sxs-lookup"><span data-stu-id="a390f-107">Node.js package issues</span></span>
### <a name="no-response-during-gulp-tasks"></a><span data-ttu-id="a390f-108">Нет ответа при выполнении задач Gulp</span><span class="sxs-lookup"><span data-stu-id="a390f-108">No response during gulp tasks</span></span>
<span data-ttu-id="a390f-109">Если возникли проблемы при выполнении задачи gulp, можно добавить hello `--verbose` параметра для отладки.</span><span class="sxs-lookup"><span data-stu-id="a390f-109">If you encounter problems running gulp tasks, you can add hello `--verbose` option for debugging.</span></span> <span data-ttu-id="a390f-110">Повторите tooterminate текущие задачи gulp с помощью `Ctrl + C`, а затем выполнения hello следующую команду в сообщения отладки toosee окна консоли.</span><span class="sxs-lookup"><span data-stu-id="a390f-110">Try tooterminate current gulp tasks by using `Ctrl + C`, and then run hello following command in your console window toosee debug messages.</span></span> <span data-ttu-id="a390f-111">В выходных данных консоли должны отобразиться подробные сообщения об ошибках.</span><span class="sxs-lookup"><span data-stu-id="a390f-111">You might see detailed error messages in your console output.</span></span> 

```bash
gulp --verbose
```

### <a name="npm-issues"></a><span data-ttu-id="a390f-112">проблемы с NPM</span><span class="sxs-lookup"><span data-stu-id="a390f-112">NPM issues</span></span>
<span data-ttu-id="a390f-113">Попробуйте tooupdate пакета NPM с hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="a390f-113">Try tooupdate your NPM package with hello following command:</span></span>

```bash
npm install -g npm
```

<span data-ttu-id="a390f-114">Если hello проблема остается, оставьте комментарий в конце hello в этой статье, или создать вопрос GitHub в нашем [репозитории примеров][sample-repository].</span><span class="sxs-lookup"><span data-stu-id="a390f-114">If hello problem still exists, leave your comments at hello end of this article or create a GitHub issue in our [sample repository][sample-repository].</span></span>

## <a name="azure-cli-issues"></a><span data-ttu-id="a390f-115">Проблемы с Azure CLI</span><span class="sxs-lookup"><span data-stu-id="a390f-115">Azure-CLI issues</span></span>
<span data-ttu-id="a390f-116">Hello Azure командной строки (CLI Azure) — это построение предварительного просмотра.</span><span class="sxs-lookup"><span data-stu-id="a390f-116">hello Azure command-line interface (Azure CLI) is a preview build.</span></span> <span data-ttu-id="a390f-117">Искать решение в hello [руководство по установке Preview](https://github.com/Azure/azure-cli/blob/master/doc/preview_install_guide.md) tooseek решения.</span><span class="sxs-lookup"><span data-stu-id="a390f-117">Look for solution in hello [Preview Install Guide](https://github.com/Azure/azure-cli/blob/master/doc/preview_install_guide.md) tooseek solutions.</span></span> <span data-ttu-id="a390f-118">Повторите версии toolatest tooupgrade Azure cli, когда команды не работают должным образом.</span><span class="sxs-lookup"><span data-stu-id="a390f-118">Try tooupgrade Azure-cli toolatest version when commands don’t work as expected.</span></span>

<span data-ttu-id="a390f-119">При возникновении любых ошибок с помощью средства hello файл [проблема](https://github.com/Azure/azure-cli/issues) в hello **проблемы** раздел hello в репозитории GitHub.</span><span class="sxs-lookup"><span data-stu-id="a390f-119">If you encounter any bugs with hello tool, file an [issue](https://github.com/Azure/azure-cli/issues) in hello **Issues** section of hello GitHub repo.</span></span>

<span data-ttu-id="a390f-120">Для получения справки по устранению общих проблем, проверьте hello [readme](https://github.com/Azure/azure-cli/blob/master/README.rst).</span><span class="sxs-lookup"><span data-stu-id="a390f-120">For help troubleshooting common problems, check hello [readme](https://github.com/Azure/azure-cli/blob/master/README.rst).</span></span>

<span data-ttu-id="a390f-121">Если соблюдаются «Не удалось найти версию, которая соответствует требованиям hello», проверьте выполнения hello следующая команда tooupgrade pip toolastest версии.</span><span class="sxs-lookup"><span data-stu-id="a390f-121">If you meet "Could not find a version that satisfies hello requirement", please run hello following command tooupgrade pip toolastest version.</span></span>

```bash
python -m pip install --upgrade pip
```

## <a name="python-installation-issues"></a><span data-ttu-id="a390f-122">Проблемы с установкой Python</span><span class="sxs-lookup"><span data-stu-id="a390f-122">Python installation issues</span></span>
### <a name="legacy-installation-issues-macos"></a><span data-ttu-id="a390f-123">Проблемы с устаревшими установками (macOS)</span><span class="sxs-lookup"><span data-stu-id="a390f-123">Legacy installation issues (macOS)</span></span>
<span data-ttu-id="a390f-124">При установке **pip** возникает ошибка разрешения, если есть устаревшие пакеты, которые устанавливаются с использованием разрешений **su**.</span><span class="sxs-lookup"><span data-stu-id="a390f-124">When you're installing **pip**, a permission error is thrown when older packages that are installed with **su** permissions.</span></span> <span data-ttu-id="a390f-125">Такая ситуация возникает из-за того, что предыдущая установка Python с использованием brew (macOS) удалена не полностью.</span><span class="sxs-lookup"><span data-stu-id="a390f-125">This situation occurs because a previous installation of Python using brew (macOS) is not uninstalled completely.</span></span> <span data-ttu-id="a390f-126">Некоторые **pip** пакеты из предыдущей установки были созданы корневым элементом, который приводит к возникновению ошибки разрешение hello.</span><span class="sxs-lookup"><span data-stu-id="a390f-126">Some **pip** packages from a previous installation were created by root, which causes hello permission error.</span></span> <span data-ttu-id="a390f-127">Здравствуйте, решение является tooremove эти пакеты, установленные корневым элементом.</span><span class="sxs-lookup"><span data-stu-id="a390f-127">hello solution is tooremove those packages installed by root.</span></span> <span data-ttu-id="a390f-128">Используйте следующие шаги toocomplete hello этой задачи:</span><span class="sxs-lookup"><span data-stu-id="a390f-128">Use hello following steps toocomplete this task:</span></span>

1. <span data-ttu-id="a390f-129">Перейдите к папке /usr/local/lib/python2.7/site-packages.</span><span class="sxs-lookup"><span data-stu-id="a390f-129">Go to: /usr/local/lib/python2.7/site-packages</span></span>
2. <span data-ttu-id="a390f-130">Выведите список пакетов, созданных с использованием разрешений корневой папки: `ls -l | grep root`.</span><span class="sxs-lookup"><span data-stu-id="a390f-130">List packages create by root: `ls -l | grep root`</span></span>
3. <span data-ttu-id="a390f-131">Удалите пакеты из шага 2: `sudo rm -rf {package name}`.</span><span class="sxs-lookup"><span data-stu-id="a390f-131">Uninstall packages from step 2: `sudo rm -rf {package name}`</span></span>
4. <span data-ttu-id="a390f-132">Переустановите Python.</span><span class="sxs-lookup"><span data-stu-id="a390f-132">Reinstall Python.</span></span>

## <a name="azure-iot-hub-issues"></a><span data-ttu-id="a390f-133">Проблемы с Центром Интернета вещей Azure</span><span class="sxs-lookup"><span data-stu-id="a390f-133">Azure IoT Hub issues</span></span>
<span data-ttu-id="a390f-134">Если успешной подготовки ваш центр Azure IoT с `azure-cli`, и необходимо, чтобы устройства hello toomanage средство, подключающимися центра IoT tooyour, попробуйте hello следующие средства:</span><span class="sxs-lookup"><span data-stu-id="a390f-134">If you've successfully provisioned your Azure IoT hub with `azure-cli`, and you need a tool toomanage hello devices that are connecting tooyour IoT hub, try hello following tools:</span></span>

### <a name="device-explorer"></a><span data-ttu-id="a390f-135">Обозреватель устройств</span><span class="sxs-lookup"><span data-stu-id="a390f-135">Device Explorer</span></span>
<span data-ttu-id="a390f-136">[Обозреватель устройств](https://github.com/Azure/azure-iot-sdk-csharp/tree/master/tools/DeviceExplorer) выполняется на локальном компьютере Windows и подключается tooyour центр IoT в Azure.</span><span class="sxs-lookup"><span data-stu-id="a390f-136">[Device Explorer](https://github.com/Azure/azure-iot-sdk-csharp/tree/master/tools/DeviceExplorer) runs on your Windows local machine and connects tooyour IoT hub in Azure.</span></span> <span data-ttu-id="a390f-137">Он взаимодействует с hello следующие [конечные точки центра IoT](iot-hub-devguide.md):</span><span class="sxs-lookup"><span data-stu-id="a390f-137">It communicates with hello following [IoT Hub endpoints](iot-hub-devguide.md):</span></span>

- <span data-ttu-id="a390f-138">_Управление устройствами удостоверения_ tooprovision и управления ими устройствах, зарегистрированных в центр IoT.</span><span class="sxs-lookup"><span data-stu-id="a390f-138">_Device identity management_ tooprovision and manage devices registered with your IoT hub.</span></span>
- <span data-ttu-id="a390f-139">_Получение устройства в облако_ можно наблюдать за сообщений, отправленных из центра IoT tooyour вашего устройства.</span><span class="sxs-lookup"><span data-stu-id="a390f-139">_Receive device-to-cloud_ so you can monitor messages sent from your device tooyour IoT hub.</span></span>
- <span data-ttu-id="a390f-140">_Отправить облака на устройство_ для отправки сообщений tooyour устройств из вашего центра IoT.</span><span class="sxs-lookup"><span data-stu-id="a390f-140">_Send cloud-to-device_ so you can send messages tooyour devices from your IoT hub.</span></span>

<span data-ttu-id="a390f-141">Настройка вашего `IoT hub connection string` в этот инструмент toouse его возможности.</span><span class="sxs-lookup"><span data-stu-id="a390f-141">Configure your `IoT hub connection string` within this tool toouse all its capabilities.</span></span>

### <a name="iot-hub-explorer"></a><span data-ttu-id="a390f-142">Обозреватель Центра Интернета вещей</span><span class="sxs-lookup"><span data-stu-id="a390f-142">IoT hub Explorer</span></span>
<span data-ttu-id="a390f-143">[Центр IoT Explorer](https://github.com/Azure/iothub-explorer) -это средство многоплатформенного CLI образец toomanage клиентов устройств.</span><span class="sxs-lookup"><span data-stu-id="a390f-143">[IoT hub Explorer](https://github.com/Azure/iothub-explorer) is a sample multiplatform CLI tool toomanage device clients.</span></span> <span data-ttu-id="a390f-144">Можно использовать hello средство toomanage hello устройства в реестре удостоверений hello, отслеживать сообщения из устройства в облако и отправлять команды облака на устройство.</span><span class="sxs-lookup"><span data-stu-id="a390f-144">You can use hello tool toomanage hello devices in hello identity registry, monitor device-to-cloud messages, and send cloud-to-device commands.</span></span>

<span data-ttu-id="a390f-145">tooinstall hello последняя (Предварительная) версия hello центром IOT-анализатор, запустите следующую команду в среде командной строки hello:</span><span class="sxs-lookup"><span data-stu-id="a390f-145">tooinstall hello latest (prerelease) version of hello iothub-explorer tool, run hello following command in your command-line environment:</span></span>

```bash
npm install -g iothub-explorer@latest
```

<span data-ttu-id="a390f-146">Можно использовать следующую команду, tooget дополнительную справку обо всех hello центром IOT обозреватель команды и их параметрах hello.</span><span class="sxs-lookup"><span data-stu-id="a390f-146">You can use hello following command tooget additional help about all hello iothub-explorer commands and their parameters:</span></span>

```bash
iothub-explorer help
```

### <a name="azure-portal"></a><span data-ttu-id="a390f-147">Портал Azure</span><span class="sxs-lookup"><span data-stu-id="a390f-147">Azure portal</span></span>
<span data-ttu-id="a390f-148">Все возможности интерфейса командной строки помогают создавать все ресурсы Azure и управлять ими.</span><span class="sxs-lookup"><span data-stu-id="a390f-148">A full CLI experience helps you create and manage all your Azure resources.</span></span> <span data-ttu-id="a390f-149">Можно также toouse hello [портал Azure](../azure-portal-overview.md) toohelp подготовки, управления и отладки ресурсам Azure.</span><span class="sxs-lookup"><span data-stu-id="a390f-149">You might also want toouse hello [Azure portal](../azure-portal-overview.md) toohelp provision, manage, and debug your Azure resources.</span></span>

## <a name="azure-storage-issues"></a><span data-ttu-id="a390f-150">Проблемы со службой хранилища Azure</span><span class="sxs-lookup"><span data-stu-id="a390f-150">Azure storage issues</span></span>
<span data-ttu-id="a390f-151">[Обозреватель хранилищ Microsoft Azure (Предварительная версия)](http://storageexplorer.com) имеет отдельное приложение от Майкрософт, можно использовать toowork с [хранилища Azure](https://azure.microsoft.com/en-us/services/storage/) данных в Windows, macOS и Linux.</span><span class="sxs-lookup"><span data-stu-id="a390f-151">[Microsoft Azure Storage Explorer (preview)](http://storageexplorer.com) is a standalone app from Microsoft that you can use toowork with [Azure Storage](https://azure.microsoft.com/en-us/services/storage/) data on Windows, macOS, and Linux.</span></span> <span data-ttu-id="a390f-152">С ее помощью можно подключиться tooyour таблицы и просмотра данных hello.</span><span class="sxs-lookup"><span data-stu-id="a390f-152">By using this tool, you can connect tooyour table and see hello data in it.</span></span> <span data-ttu-id="a390f-153">Можно использовать этот инструмент tootroubleshoot вашей проблемы хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="a390f-153">You can use this tool tootroubleshoot your Azure Storage issues.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a390f-154">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="a390f-154">Next steps</span></span>
<span data-ttu-id="a390f-155">Эта страница содержит только наиболее распространенные проблемы hello комплекта Intel Edison.</span><span class="sxs-lookup"><span data-stu-id="a390f-155">This page only includes hello most common problems of Intel Edison kit.</span></span> <span data-ttu-id="a390f-156">Также можно оставить комментарии нижней tooreport вопросы по устранению неполадок.</span><span class="sxs-lookup"><span data-stu-id="a390f-156">You can also leave bottom comments tooreport issues for further troubleshooting.</span></span>

<span data-ttu-id="a390f-157">Возврат слишком[Приступая к работе с Intel Edison (C)](iot-hub-intel-edison-kit-c-get-started.md)</span><span class="sxs-lookup"><span data-stu-id="a390f-157">Go back too[Get started with Intel Edison (C)](iot-hub-intel-edison-kit-c-get-started.md)</span></span>

<!-- Images and links -->

[sample-repository]: https://github.com/Azure-Samples/iot-hub-c-edison-getting-started