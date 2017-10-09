---
title: "пакет SDK устройства Azure IoT aaaThe для C | Документы Microsoft"
description: "Начало работы с устройством Azure IoT hello пакета SDK для C и узнайте, как toocreate приложения для устройств, взаимодействовать с центром IoT."
services: iot-hub
documentationcenter: 
author: olivierbloch
manager: timlt
editor: 
ms.assetid: e448b061-6bdd-470a-a527-15ec03cca7b9
ms.service: iot-hub
ms.devlang: cpp
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/25/2017
ms.author: obloch
ms.openlocfilehash: 9e20742e6ea513c124bfaf28f02f6fba86170daf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-iot-device-sdk-for-c"></a><span data-ttu-id="d7cea-103">Пакет SDK для устройств Azure IoT для C</span><span class="sxs-lookup"><span data-stu-id="d7cea-103">Azure IoT device SDK for C</span></span>

<span data-ttu-id="d7cea-104">Hello **устройств Azure IoT SDK** — набор библиотек, предназначенных toosimplify hello процесс отправки сообщений tooand прием сообщений от hello **центр IoT Azure** службы.</span><span class="sxs-lookup"><span data-stu-id="d7cea-104">hello **Azure IoT device SDK** is a set of libraries designed toosimplify hello process of sending messages tooand receiving messages from hello **Azure IoT Hub** service.</span></span> <span data-ttu-id="d7cea-105">Существуют различные виды hello SDK, направив определенной платформе, но в этой статье описывается hello **устройств Azure IoT SDK для C**.</span><span class="sxs-lookup"><span data-stu-id="d7cea-105">There are different variations of hello SDK, each targeting a specific platform, but this article describes hello **Azure IoT device SDK for C**.</span></span>

<span data-ttu-id="d7cea-106">пакет SDK устройства Azure IoT Hello для C записывается в toomaximize переносимости ANSI C (C99).</span><span class="sxs-lookup"><span data-stu-id="d7cea-106">hello Azure IoT device SDK for C is written in ANSI C (C99) toomaximize portability.</span></span> <span data-ttu-id="d7cea-107">Благодаря этой функции hello toooperate хорошо подходит библиотеки на нескольких платформах и устройствах, особенно в том случае, если к минимуму диска и объем памяти — приоритет.</span><span class="sxs-lookup"><span data-stu-id="d7cea-107">This feature makes hello libraries well-suited toooperate on multiple platforms and devices, especially where minimizing disk and memory footprint is a priority.</span></span>

<span data-ttu-id="d7cea-108">Существует широкий спектр платформы, на какие hello протестирована SDK (hello в разделе [Azure Certified для каталога устройств IoT](https://catalog.azureiotsuite.com/) подробные сведения).</span><span class="sxs-lookup"><span data-stu-id="d7cea-108">There are a broad range of platforms on which hello SDK has been tested (see hello [Azure Certified for IoT device catalog](https://catalog.azureiotsuite.com/) for details).</span></span> <span data-ttu-id="d7cea-109">Несмотря на то, что эта статья содержит пошаговые руководства для примера кода, работающих на платформе Windows hello, кода hello, описанных в этой статье будут одинаковыми для hello диапазон поддерживаемых платформ.</span><span class="sxs-lookup"><span data-stu-id="d7cea-109">Although this article includes walkthroughs of sample code running on hello Windows platform, hello code described in this article is identical across hello range of supported platforms.</span></span>

<span data-ttu-id="d7cea-110">В этой статье описывается архитектура toohello устройства Azure IoT hello пакета SDK для C. Он демонстрирует, как библиотека устройств tooinitialize hello, отправки данных tooIoT концентратора и получения сообщений из него.</span><span class="sxs-lookup"><span data-stu-id="d7cea-110">This article introduces you toohello architecture of hello Azure IoT device SDK for C. It demonstrates how tooinitialize hello device library, send data tooIoT Hub, and receive messages from it.</span></span> <span data-ttu-id="d7cea-111">Hello сведения в этой статье, должно быть достаточно tooget работы с использованием пакета SDK для hello, но также предоставляет указатели tooadditional сведения о библиотеках hello.</span><span class="sxs-lookup"><span data-stu-id="d7cea-111">hello information in this article should be enough tooget started using hello SDK, but also provides pointers tooadditional information about hello libraries.</span></span>

## <a name="sdk-architecture"></a><span data-ttu-id="d7cea-112">Архитектура пакета SDK</span><span class="sxs-lookup"><span data-stu-id="d7cea-112">SDK architecture</span></span>

<span data-ttu-id="d7cea-113">Можно найти hello [ **устройств Azure IoT SDK для C** ](https://github.com/Azure/azure-iot-sdk-c) GitHub репозитория и просмотра сведений из hello API в hello [Справочник по C API](https://azure.github.io/azure-iot-sdk-c/index.html).</span><span class="sxs-lookup"><span data-stu-id="d7cea-113">You can find hello [**Azure IoT device SDK for C**](https://github.com/Azure/azure-iot-sdk-c) GitHub repository and view details of hello API in hello [C API reference](https://azure.github.io/azure-iot-sdk-c/index.html).</span></span>

<span data-ttu-id="d7cea-114">последнюю версию библиотек hello Hello можно найти в hello **master** ветви hello репозитория:</span><span class="sxs-lookup"><span data-stu-id="d7cea-114">hello latest version of hello libraries can be found in hello **master** branch of hello repository:</span></span>

  ![](media/iot-hub-device-sdk-c-intro/01-MasterBranch.PNG)

* <span data-ttu-id="d7cea-115">Hello core реализация hello SDK соответствует hello **центром IOT\_клиента** папку, содержащую реализацию hello hello нижний уровень API в hello SDK: hello **IoTHubClient** библиотеки.</span><span class="sxs-lookup"><span data-stu-id="d7cea-115">hello core implementation of hello SDK is in hello **iothub\_client** folder that contains hello implementation of hello lowest API layer in hello SDK: hello **IoTHubClient** library.</span></span> <span data-ttu-id="d7cea-116">Hello **IoTHubClient** библиотеки содержит API-интерфейсы, реализация необработанных сообщений для отправки сообщений tooIoT концентратора и получения сообщений из центра IoT.</span><span class="sxs-lookup"><span data-stu-id="d7cea-116">hello **IoTHubClient** library contains APIs implementing raw messaging for sending messages tooIoT Hub and receiving messages from IoT Hub.</span></span> <span data-ttu-id="d7cea-117">Если вы используете эту библиотеку, вам нужно самостоятельно реализовать сериализацию сообщений. Другие составляющие процесса взаимодействия с Центром Интернета вещей реализуются автоматически.</span><span class="sxs-lookup"><span data-stu-id="d7cea-117">When using this library, you are responsible for implementing message serialization, but other details of communicating with IoT Hub are handled for you.</span></span>
* <span data-ttu-id="d7cea-118">Hello **сериализатор** папки содержит вспомогательные функции и образцы, которые показывают, как tooserialize данные перед отправкой с помощью центра IoT tooAzure hello клиентской библиотеки.</span><span class="sxs-lookup"><span data-stu-id="d7cea-118">hello **serializer** folder contains helper functions and samples that show you how tooserialize data before sending tooAzure IoT Hub using hello client library.</span></span> <span data-ttu-id="d7cea-119">Использование Hello сериализатор hello не является обязательным и предоставляется для удобства.</span><span class="sxs-lookup"><span data-stu-id="d7cea-119">hello use of hello serializer is not mandatory and is provided as a convenience.</span></span> <span data-ttu-id="d7cea-120">toouse hello **сериализатор** библиотеки, определить модель, которая указывает данных toosend tooIoT концентратора и hello сообщений hello предполагается, что tooreceive от него.</span><span class="sxs-lookup"><span data-stu-id="d7cea-120">toouse hello **serializer** library, you define a model that specifies hello data toosend tooIoT Hub and hello messages you expect tooreceive from it.</span></span> <span data-ttu-id="d7cea-121">После определения модели hello hello SDK содержит рабочую область API, который позволяет tooeasily работы с устройства в облако и сообщения облака на устройство, не беспокоясь о hello сведения о сериализации.</span><span class="sxs-lookup"><span data-stu-id="d7cea-121">Once hello model is defined, hello SDK provides you with an API surface that enables you tooeasily work with device-to-cloud and cloud-to-device messages without worrying about hello serialization details.</span></span> <span data-ttu-id="d7cea-122">Библиотека Hello зависит от других библиотек открытым исходным кодом, реализующие транспорта с помощью протоколов, таких как MQTT и AMQP.</span><span class="sxs-lookup"><span data-stu-id="d7cea-122">hello library depends on other open source libraries that implement transport using protocols such as MQTT and AMQP.</span></span>
* <span data-ttu-id="d7cea-123">Hello **IoTHubClient** библиотеки зависит от других библиотек с открытым исходным кодом:</span><span class="sxs-lookup"><span data-stu-id="d7cea-123">hello **IoTHubClient** library depends on other open source libraries:</span></span>
  * <span data-ttu-id="d7cea-124">Hello [Azure C Общие программы](https://github.com/Azure/azure-c-shared-utility) библиотеку, которая предоставляет общие функциональные возможности для основных задач (например, строки, обработка списка и операции ввода-ВЫВОДА) на несколько связанных с Azure SDK C.</span><span class="sxs-lookup"><span data-stu-id="d7cea-124">hello [Azure C shared utility](https://github.com/Azure/azure-c-shared-utility) library, which provides common functionality for basic tasks (such as strings, list manipulation, and IO) needed across several Azure-related C SDKs.</span></span>
  * <span data-ttu-id="d7cea-125">Hello [Azure uAMQP](https://github.com/Azure/azure-uamqp-c) библиотеку, которая является реализацией клиентского AMQP, оптимизированный для ограниченного ресурсов устройств.</span><span class="sxs-lookup"><span data-stu-id="d7cea-125">hello [Azure uAMQP](https://github.com/Azure/azure-uamqp-c) library, which is a client-side implementation of AMQP optimized for resource constrained devices.</span></span>
  * <span data-ttu-id="d7cea-126">Hello [Azure uMQTT](https://github.com/Azure/azure-umqtt-c) библиотеку, которая является библиотекой общего назначения, реализация протокола MQTT hello и оптимизированный для ограниченного ресурсов устройств.</span><span class="sxs-lookup"><span data-stu-id="d7cea-126">hello [Azure uMQTT](https://github.com/Azure/azure-umqtt-c) library, which is a general-purpose library implementing hello MQTT protocol and optimized for resource constrained devices.</span></span>

<span data-ttu-id="d7cea-127">Эти библиотеки используется проще toounderstand, просмотрев пример кода.</span><span class="sxs-lookup"><span data-stu-id="d7cea-127">Use of these libraries is easier toounderstand by looking at example code.</span></span> <span data-ttu-id="d7cea-128">Hello в следующих разделах описаны шаги несколько hello образцы приложений, которые включены в пакет SDK для hello.</span><span class="sxs-lookup"><span data-stu-id="d7cea-128">hello following sections walk you through several of hello sample applications that are included in hello SDK.</span></span> <span data-ttu-id="d7cea-129">В этом пошаговом руководстве будет предоставлять хорошее вид hello hello уровнях архитектуры hello SDK и API-интерфейсы работают приветствия toohow введение различные функциональные возможности.</span><span class="sxs-lookup"><span data-stu-id="d7cea-129">This walkthrough should give you a good feel for hello various capabilities of hello architectural layers of hello SDK and an introduction toohow hello APIs work.</span></span>

## <a name="before-you-run-hello-samples"></a><span data-ttu-id="d7cea-130">Перед запуском образцов hello</span><span class="sxs-lookup"><span data-stu-id="d7cea-130">Before you run hello samples</span></span>

<span data-ttu-id="d7cea-131">Перед выполнением примеров hello в пакет SDK устройства Azure IoT hello для языка C, необходимо [создания экземпляра службы центра IoT hello](iot-hub-create-through-portal.md) в вашей подписке Azure.</span><span class="sxs-lookup"><span data-stu-id="d7cea-131">Before you can run hello samples in hello Azure IoT device SDK for C, you must [create an instance of hello IoT Hub service](iot-hub-create-through-portal.md) in your Azure subscription.</span></span> <span data-ttu-id="d7cea-132">Затем выполните следующие задачи hello.</span><span class="sxs-lookup"><span data-stu-id="d7cea-132">Then complete hello following tasks:</span></span>

* <span data-ttu-id="d7cea-133">Подготовка среды разработки</span><span class="sxs-lookup"><span data-stu-id="d7cea-133">Prepare your development environment</span></span>
* <span data-ttu-id="d7cea-134">получение учетных данных устройства.</span><span class="sxs-lookup"><span data-stu-id="d7cea-134">Obtain device credentials.</span></span>

### <a name="prepare-your-development-environment"></a><span data-ttu-id="d7cea-135">Подготовка среды разработки</span><span class="sxs-lookup"><span data-stu-id="d7cea-135">Prepare your development environment</span></span>

<span data-ttu-id="d7cea-136">Пакеты предоставляются для распространенных платформ (например, NuGet для Windows или apt_get для Debian и Ubuntu) и образцы hello использовать эти пакеты, если оно доступно.</span><span class="sxs-lookup"><span data-stu-id="d7cea-136">Packages are provided for common platforms (such as NuGet for Windows or apt_get for Debian and Ubuntu) and hello samples use these packages when available.</span></span> <span data-ttu-id="d7cea-137">В некоторых случаях необходимо hello toocompile пакета SDK для или на устройстве.</span><span class="sxs-lookup"><span data-stu-id="d7cea-137">In some cases, you need toocompile hello SDK for or on your device.</span></span> <span data-ttu-id="d7cea-138">Toocompile hello SDK см [подготовить среду разработки](https://github.com/Azure/azure-iot-sdk-c/blob/master/doc/devbox_setup.md) в репозитории GitHub hello.</span><span class="sxs-lookup"><span data-stu-id="d7cea-138">If you need toocompile hello SDK, see [Prepare your development environment](https://github.com/Azure/azure-iot-sdk-c/blob/master/doc/devbox_setup.md) in hello GitHub repository.</span></span>

<span data-ttu-id="d7cea-139">tooobtain hello образец кода приложения, загрузить копию hello SDK с сайта GitHub.</span><span class="sxs-lookup"><span data-stu-id="d7cea-139">tooobtain hello sample application code, download a copy of hello SDK from GitHub.</span></span> <span data-ttu-id="d7cea-140">Получить копию исходного hello из hello **master** ветви hello [репозитории GitHub](https://github.com/Azure/azure-iot-sdk-c).</span><span class="sxs-lookup"><span data-stu-id="d7cea-140">Get your copy of hello source from hello **master** branch of hello [GitHub repository](https://github.com/Azure/azure-iot-sdk-c).</span></span>


### <a name="obtain-hello-device-credentials"></a><span data-ttu-id="d7cea-141">Получить учетные данные устройства hello</span><span class="sxs-lookup"><span data-stu-id="d7cea-141">Obtain hello device credentials</span></span>

<span data-ttu-id="d7cea-142">Теперь, когда исходный код образца hello hello Далее самое toodo — tooget набор учетных данных устройства.</span><span class="sxs-lookup"><span data-stu-id="d7cea-142">Now that you have hello sample source code, hello next thing toodo is tooget a set of device credentials.</span></span> <span data-ttu-id="d7cea-143">Для устройств toobe может tooaccess центра IoT необходимо сначала добавить toohello устройство hello реестра удостоверений центр IoT.</span><span class="sxs-lookup"><span data-stu-id="d7cea-143">For a device toobe able tooaccess an IoT hub, you must first add hello device toohello IoT Hub identity registry.</span></span> <span data-ttu-id="d7cea-144">При добавлении устройства вы получаете набор устройств учетные данные, необходимые для hello устройства toobe может tooconnect toohello центр IoT.</span><span class="sxs-lookup"><span data-stu-id="d7cea-144">When you add your device, you get a set of device credentials that you need for hello device toobe able tooconnect toohello IoT hub.</span></span> <span data-ttu-id="d7cea-145">Hello образцы приложений, описанные в следующем разделе hello ожидается, что эти учетные данные в форме hello **строка подключения устройства**.</span><span class="sxs-lookup"><span data-stu-id="d7cea-145">hello sample applications discussed in hello next section expect these credentials in hello form of a **device connection string**.</span></span>

<span data-ttu-id="d7cea-146">Существует несколько средств toohelp открытым исходным кодом, управлять ваш центр IoT.</span><span class="sxs-lookup"><span data-stu-id="d7cea-146">There are several open source tools toohelp you manage your IoT hub.</span></span>

* <span data-ttu-id="d7cea-147">Приложение Windows — [обозреватель устройств](https://github.com/Azure/azure-iot-sdk-csharp/tree/master/tools/DeviceExplorer).</span><span class="sxs-lookup"><span data-stu-id="d7cea-147">A Windows application called [device explorer](https://github.com/Azure/azure-iot-sdk-csharp/tree/master/tools/DeviceExplorer).</span></span>
* <span data-ttu-id="d7cea-148">Кроссплатформенная программа командной строки Azure на Node.js — [iothub-explorer](https://github.com/azure/iothub-explorer).</span><span class="sxs-lookup"><span data-stu-id="d7cea-148">A cross-platform node.js CLI tool called [iothub-explorer](https://github.com/azure/iothub-explorer).</span></span>

<span data-ttu-id="d7cea-149">В этом учебнике используется графический hello *обозреватель устройств* средства.</span><span class="sxs-lookup"><span data-stu-id="d7cea-149">This tutorial uses hello graphical *device explorer* tool.</span></span> <span data-ttu-id="d7cea-150">Можно также использовать hello *explorer центром IOT* средства при желании toouse средство CLI.</span><span class="sxs-lookup"><span data-stu-id="d7cea-150">You can also use hello *iothub-explorer* tool if you prefer toouse a CLI tool.</span></span>

<span data-ttu-id="d7cea-151">Анализатор устройства Hello использует различные функции hello Azure IoT службы библиотеки tooperform на центра IoT, включая добавление устройств.</span><span class="sxs-lookup"><span data-stu-id="d7cea-151">hello device explorer tool uses hello Azure IoT service libraries tooperform various functions on IoT Hub, including adding devices.</span></span> <span data-ttu-id="d7cea-152">Если вы используете hello устройство обозревателя средство tooadd устройство, вы получаете строку подключения для устройства.</span><span class="sxs-lookup"><span data-stu-id="d7cea-152">If you use hello device explorer tool tooadd a device, you get a connection string for your device.</span></span> <span data-ttu-id="d7cea-153">Необходимо, чтобы это соединение строка toorun hello образцы приложений.</span><span class="sxs-lookup"><span data-stu-id="d7cea-153">You need this connection string toorun hello sample applications.</span></span>

<span data-ttu-id="d7cea-154">Если вы не знакомы с помощью средства обозревателя устройства hello, hello следующая процедура описывает способ toouse его tooadd устройства и получение строки подключения устройства.</span><span class="sxs-lookup"><span data-stu-id="d7cea-154">If you're not familiar with hello device explorer tool, hello following procedure describes how toouse it tooadd a device and obtain a device connection string.</span></span>

<span data-ttu-id="d7cea-155">вспомогательное средство tooinstall hello устройства. в разделе [как toouse hello обозреватель устройств для устройств центра IoT](https://github.com/Azure/azure-iot-sdk-csharp/tree/master/tools/DeviceExplorer).</span><span class="sxs-lookup"><span data-stu-id="d7cea-155">tooinstall hello device explorer tool, see [How toouse hello Device Explorer for IoT Hub devices](https://github.com/Azure/azure-iot-sdk-csharp/tree/master/tools/DeviceExplorer).</span></span>

<span data-ttu-id="d7cea-156">При запуске программы hello, вы видите этот интерфейс:</span><span class="sxs-lookup"><span data-stu-id="d7cea-156">When you run hello program, you see this interface:</span></span>

  ![](media/iot-hub-device-sdk-c-intro/03-DeviceExplorer.PNG)

<span data-ttu-id="d7cea-157">Введите ваш **строка подключения концентратора IoT** в hello первое поле и нажмите кнопку **обновление**.</span><span class="sxs-lookup"><span data-stu-id="d7cea-157">Enter your **IoT Hub Connection String** in hello first field and click **Update**.</span></span> <span data-ttu-id="d7cea-158">Этот шаг позволяет настроить средство hello, чтобы его могли взаимодействовать с центром IoT.</span><span class="sxs-lookup"><span data-stu-id="d7cea-158">This step configures hello tool so that it can communicate with IoT Hub.</span></span>

<span data-ttu-id="d7cea-159">При настройке hello центра IoT строку соединения, нажмите кнопку hello **управления** вкладки:</span><span class="sxs-lookup"><span data-stu-id="d7cea-159">When hello IoT Hub connection string is configured, click hello **Management** tab:</span></span>

  ![](media/iot-hub-device-sdk-c-intro/04-ManagementTab.PNG)

<span data-ttu-id="d7cea-160">Эта вкладка служит для управления hello устройства, зарегистрированные в концентратор IoT.</span><span class="sxs-lookup"><span data-stu-id="d7cea-160">This tab is where you manage hello devices registered in your IoT hub.</span></span>

<span data-ttu-id="d7cea-161">Создать устройство, щелкнув hello **создать** кнопки.</span><span class="sxs-lookup"><span data-stu-id="d7cea-161">You create a device by clicking hello **Create** button.</span></span> <span data-ttu-id="d7cea-162">Откроется диалоговое окно с заполненным набором ключей (первичных и вторичных).</span><span class="sxs-lookup"><span data-stu-id="d7cea-162">A dialog displays with a set of pre-populated keys (primary and secondary).</span></span> <span data-ttu-id="d7cea-163">Введите **идентификатор устройства**, а затем нажмите кнопку **Создать**.</span><span class="sxs-lookup"><span data-stu-id="d7cea-163">Enter a **Device ID** and then click **Create**.</span></span>

  ![](media/iot-hub-device-sdk-c-intro/05-CreateDevice.PNG)

<span data-ttu-id="d7cea-164">При создании устройства hello устройств hello список обновлений с все зарегистрированные hello устройств, включая один только что созданный hello.</span><span class="sxs-lookup"><span data-stu-id="d7cea-164">When hello device is created, hello Devices list updates with all hello registered devices, including hello one you just created.</span></span> <span data-ttu-id="d7cea-165">Если щелкнуть новое устройство правой кнопкой мыши, появится следующее меню:</span><span class="sxs-lookup"><span data-stu-id="d7cea-165">If you right-click your new device, you see this menu:</span></span>

  ![](media/iot-hub-device-sdk-c-intro/06-RightClickDevice.PNG)

<span data-ttu-id="d7cea-166">При выборе **Скопируйте строку подключения для выбранного устройства**, строка подключения устройства hello: скопированный toohello буфер обмена.</span><span class="sxs-lookup"><span data-stu-id="d7cea-166">If you choose **Copy connection string for selected device**, hello device connection string is copied toohello clipboard.</span></span> <span data-ttu-id="d7cea-167">Сохраните копию строки подключения устройств hello.</span><span class="sxs-lookup"><span data-stu-id="d7cea-167">Keep a copy of hello device connection string.</span></span> <span data-ttu-id="d7cea-168">Он нужен, при выполнении hello образцы приложений, описанные в следующих разделах hello.</span><span class="sxs-lookup"><span data-stu-id="d7cea-168">You need it when running hello sample applications described in hello following sections.</span></span>

<span data-ttu-id="d7cea-169">После завершения hello описанные выше действия, вы готовы toostart выполнение некоторых кода.</span><span class="sxs-lookup"><span data-stu-id="d7cea-169">When you've completed hello steps above, you're ready toostart running some code.</span></span> <span data-ttu-id="d7cea-170">Оба примера имеют константа вверху hello hello основной исходный файл, позволяющий tooenter строку подключения.</span><span class="sxs-lookup"><span data-stu-id="d7cea-170">Both samples have a constant at hello top of hello main source file that enables you tooenter a connection string.</span></span> <span data-ttu-id="d7cea-171">Здравствуйте, например, соответствующей строке из hello **центром IOT\_клиента\_пример\_mqtt** приложение имеет следующий вид.</span><span class="sxs-lookup"><span data-stu-id="d7cea-171">For example, hello corresponding line from hello **iothub\_client\_sample\_mqtt** application appears as follows.</span></span>

```c
static const char* connectionString = "[device connection string]";
```

## <a name="use-hello-iothubclient-library"></a><span data-ttu-id="d7cea-172">Используйте библиотеку IoTHubClient hello</span><span class="sxs-lookup"><span data-stu-id="d7cea-172">Use hello IoTHubClient library</span></span>

<span data-ttu-id="d7cea-173">В пределах hello **центром IOT\_клиента** папки в hello [azure iot-sdk c](https://github.com/azure/azure-iot-sdk-c) репозитория, имеется **образцы** папку, содержащую приложение называется **центром IOT\_клиента\_пример\_mqtt**.</span><span class="sxs-lookup"><span data-stu-id="d7cea-173">Within hello **iothub\_client** folder in hello [azure-iot-sdk-c](https://github.com/azure/azure-iot-sdk-c) repository, there is a **samples** folder that contains an application called **iothub\_client\_sample\_mqtt**.</span></span>

<span data-ttu-id="d7cea-174">версия Windows Hello hello **центром IOT\_клиента\_пример\_mqtt** приложение hello следующие решения Visual Studio включает в себя:</span><span class="sxs-lookup"><span data-stu-id="d7cea-174">hello Windows version of hello **iothub\_client\_sample\_mqtt** application includes hello following Visual Studio solution:</span></span>

  ![](media/iot-hub-device-sdk-c-intro/12-iothub-client-sample-mqtt.PNG)

> [!NOTE]
> <span data-ttu-id="d7cea-175">При открытии этого проекта в Visual Studio 2017 г примите hello приглашения tooretarget hello toohello последнюю версию проекта.</span><span class="sxs-lookup"><span data-stu-id="d7cea-175">If you open this project in Visual Studio 2017, accept hello prompts tooretarget hello project toohello latest version.</span></span>

<span data-ttu-id="d7cea-176">Это решение содержит один проект:</span><span class="sxs-lookup"><span data-stu-id="d7cea-176">This solution contains a single project.</span></span> <span data-ttu-id="d7cea-177">В этом решении установлено четыре пакета NuGet:</span><span class="sxs-lookup"><span data-stu-id="d7cea-177">There are four NuGet packages installed in this solution:</span></span>

* <span data-ttu-id="d7cea-178">Microsoft.Azure.C.SharedUtility</span><span class="sxs-lookup"><span data-stu-id="d7cea-178">Microsoft.Azure.C.SharedUtility</span></span>
* <span data-ttu-id="d7cea-179">Microsoft.Azure.IoTHub.MqttTransport.</span><span class="sxs-lookup"><span data-stu-id="d7cea-179">Microsoft.Azure.IoTHub.MqttTransport</span></span>
* <span data-ttu-id="d7cea-180">Microsoft.Azure.IoTHub.IoTHubClient</span><span class="sxs-lookup"><span data-stu-id="d7cea-180">Microsoft.Azure.IoTHub.IoTHubClient</span></span>
* <span data-ttu-id="d7cea-181">Microsoft.Azure.umqtt.</span><span class="sxs-lookup"><span data-stu-id="d7cea-181">Microsoft.Azure.umqtt</span></span>

<span data-ttu-id="d7cea-182">Необходимо всегда hello **Microsoft.Azure.C.SharedUtility** пакета при работе с hello SDK.</span><span class="sxs-lookup"><span data-stu-id="d7cea-182">You always need hello **Microsoft.Azure.C.SharedUtility** package when you are working with hello SDK.</span></span> <span data-ttu-id="d7cea-183">В этом примере используется протокол MQTT hello, поэтому необходимо включить hello **Microsoft.Azure.umqtt** и **Microsoft.Azure.IoTHub.MqttTransport** пакетов (есть эквивалентный пакеты для AMQP и HTTP ).</span><span class="sxs-lookup"><span data-stu-id="d7cea-183">This sample uses hello MQTT protocol, therefore you must include hello **Microsoft.Azure.umqtt** and **Microsoft.Azure.IoTHub.MqttTransport** packages (there are equivalent packages for AMQP and HTTP).</span></span> <span data-ttu-id="d7cea-184">Поскольку образец hello использует hello **IoTHubClient** библиотеки, необходимо также включить hello **Microsoft.Azure.IoTHub.IoTHubClient** пакет в решении.</span><span class="sxs-lookup"><span data-stu-id="d7cea-184">Because hello sample uses hello **IoTHubClient** library, you must also include hello **Microsoft.Azure.IoTHub.IoTHubClient** package in your solution.</span></span>

<span data-ttu-id="d7cea-185">Реализация hello для образца приложения hello можно найти в hello **центром IOT\_клиента\_пример\_mqtt.c** исходный файл.</span><span class="sxs-lookup"><span data-stu-id="d7cea-185">You can find hello implementation for hello sample application in hello **iothub\_client\_sample\_mqtt.c** source file.</span></span>

<span data-ttu-id="d7cea-186">Hello Далее используется этот образец приложения toowalk по также требования toouse hello **IoTHubClient** библиотеки.</span><span class="sxs-lookup"><span data-stu-id="d7cea-186">hello following steps use this sample application toowalk you through what's required toouse hello **IoTHubClient** library.</span></span>

### <a name="initialize-hello-library"></a><span data-ttu-id="d7cea-187">Инициализировать библиотеку hello</span><span class="sxs-lookup"><span data-stu-id="d7cea-187">Initialize hello library</span></span>

> [!NOTE]
> <span data-ttu-id="d7cea-188">Перед началом работы с библиотеками hello может потребоваться tooperform некоторые инициализацию в зависимости от платформы.</span><span class="sxs-lookup"><span data-stu-id="d7cea-188">Before you start working with hello libraries, you may need tooperform some platform-specific initialization.</span></span> <span data-ttu-id="d7cea-189">Например если вы планируете Linux toouse AMQP необходимо инициализировать библиотеки OpenSSL hello.</span><span class="sxs-lookup"><span data-stu-id="d7cea-189">For example, if you plan toouse AMQP on Linux you must initialize hello OpenSSL library.</span></span> <span data-ttu-id="d7cea-190">Здравствуйте, примеры в hello [репозитории GitHub](https://github.com/Azure/azure-iot-sdk-c) вызов функции программы hello **платформы\_init** при hello запускается клиент и вызовите hello **платформы\_deinit**  функция перед выходом.</span><span class="sxs-lookup"><span data-stu-id="d7cea-190">hello samples in hello [GitHub repository](https://github.com/Azure/azure-iot-sdk-c) call hello utility function **platform\_init** when hello client starts and call hello **platform\_deinit** function before exiting.</span></span> <span data-ttu-id="d7cea-191">Эти функции объявляются в файле заголовка platform.h hello.</span><span class="sxs-lookup"><span data-stu-id="d7cea-191">These functions are declared in hello platform.h header file.</span></span> <span data-ttu-id="d7cea-192">Изучите определения hello этих функций для целевой платформы в hello [репозитория](https://github.com/Azure/azure-iot-sdk-c) toodetermine необходимости tooinclude любой код инициализации платформой в клиентском приложении.</span><span class="sxs-lookup"><span data-stu-id="d7cea-192">Examine hello definitions of these functions for your target platform in hello [repository](https://github.com/Azure/azure-iot-sdk-c) toodetermine whether you need tooinclude any platform-specific initialization code in your client.</span></span>

<span data-ttu-id="d7cea-193">Работа с библиотеками hello toostart сначала выделить дескриптор клиента центр IoT:</span><span class="sxs-lookup"><span data-stu-id="d7cea-193">toostart working with hello libraries, first allocate an IoT Hub client handle:</span></span>

```c
if ((iotHubClientHandle = IoTHubClient_LL_CreateFromConnectionString(connectionString, MQTT_Protocol)) == NULL)
{
    (void)printf("ERROR: iotHubClientHandle is NULL!\r\n");
}
else
{
    ...
```

<span data-ttu-id="d7cea-194">Вы передаете копию строки подключения устройства hello, полученную по функции toothis средство обозревателя устройства hello.</span><span class="sxs-lookup"><span data-stu-id="d7cea-194">You pass a copy of hello device connection string you obtained from hello device explorer tool toothis function.</span></span> <span data-ttu-id="d7cea-195">Можно также назначить toouse протокола связи hello.</span><span class="sxs-lookup"><span data-stu-id="d7cea-195">You also designate hello communications protocol toouse.</span></span> <span data-ttu-id="d7cea-196">В этом примере используется протокол MQTT, но вы также можете использовать протоколы AMQP и HTTP.</span><span class="sxs-lookup"><span data-stu-id="d7cea-196">This example uses MQTT, but AMQP and HTTP are also options.</span></span>

<span data-ttu-id="d7cea-197">При наличии допустимого **центром IOT\_КЛИЕНТА\_ОБРАБОТКИ**, можно запустить вызов API-интерфейсы toosend hello и получать сообщения tooand из центра IoT.</span><span class="sxs-lookup"><span data-stu-id="d7cea-197">When you have a valid **IOTHUB\_CLIENT\_HANDLE**, you can start calling hello APIs toosend and receive messages tooand from IoT Hub.</span></span>

### <a name="send-messages"></a><span data-ttu-id="d7cea-198">Отправка сообщений</span><span class="sxs-lookup"><span data-stu-id="d7cea-198">Send messages</span></span>

<span data-ttu-id="d7cea-199">Пример приложения Hello устанавливает концентратор IoT tooyour цикла toosend сообщений.</span><span class="sxs-lookup"><span data-stu-id="d7cea-199">hello sample application sets up a loop toosend messages tooyour IoT hub.</span></span> <span data-ttu-id="d7cea-200">Следующий фрагмент кода Hello:</span><span class="sxs-lookup"><span data-stu-id="d7cea-200">hello following snippet:</span></span>

- <span data-ttu-id="d7cea-201">создает сообщение;</span><span class="sxs-lookup"><span data-stu-id="d7cea-201">Creates a message.</span></span>
- <span data-ttu-id="d7cea-202">Добавляет свойство toohello сообщение.</span><span class="sxs-lookup"><span data-stu-id="d7cea-202">Adds a property toohello message.</span></span>
- <span data-ttu-id="d7cea-203">отправляет сообщение.</span><span class="sxs-lookup"><span data-stu-id="d7cea-203">Sends a message.</span></span>

<span data-ttu-id="d7cea-204">Сначала создайте сообщение:</span><span class="sxs-lookup"><span data-stu-id="d7cea-204">First, create a message:</span></span>

```c
size_t iterator = 0;
do
{
    if (iterator < MESSAGE_COUNT)
    {
        sprintf_s(msgText, sizeof(msgText), "{\"deviceId\":\"myFirstDevice\",\"windSpeed\":%.2f}", avgWindSpeed + (rand() % 4 + 2));
        if ((messages[iterator].messageHandle = IoTHubMessage_CreateFromByteArray((const unsigned char*)msgText, strlen(msgText))) == NULL)
        {
            (void)printf("ERROR: iotHubMessageHandle is NULL!\r\n");
        }
        else
        {
            messages[iterator].messageTrackingId = iterator;
            MAP_HANDLE propMap = IoTHubMessage_Properties(messages[iterator].messageHandle);
            (void)sprintf_s(propText, sizeof(propText), "PropMsg_%zu", iterator);
            if (Map_AddOrUpdate(propMap, "PropName", propText) != MAP_OK)
            {
                (void)printf("ERROR: Map_AddOrUpdate Failed!\r\n");
            }

            if (IoTHubClient_LL_SendEventAsync(iotHubClientHandle, messages[iterator].messageHandle, SendConfirmationCallback, &messages[iterator]) != IOTHUB_CLIENT_OK)
            {
                (void)printf("ERROR: IoTHubClient_LL_SendEventAsync..........FAILED!\r\n");
            }
            else
            {
                (void)printf("IoTHubClient_LL_SendEventAsync accepted message [%d] for transmission tooIoT Hub.\r\n", (int)iterator);
            }
        }
    }
    IoTHubClient_LL_DoWork(iotHubClientHandle);
    ThreadAPI_Sleep(1);

    iterator++;
} while (g_continueRunning);
```

<span data-ttu-id="d7cea-205">Каждый раз при отправке сообщения можно указать функцию обратного вызова tooa ссылку, которая вызывается при отправке данных hello.</span><span class="sxs-lookup"><span data-stu-id="d7cea-205">Every time you send a message, you specify a reference tooa callback function that's invoked when hello data is sent.</span></span> <span data-ttu-id="d7cea-206">В этом примере вызывается функция обратного вызова hello **SendConfirmationCallback**.</span><span class="sxs-lookup"><span data-stu-id="d7cea-206">In this example, hello callback function is called **SendConfirmationCallback**.</span></span> <span data-ttu-id="d7cea-207">Следующий фрагмент кода Hello показывает эту функцию обратного вызова:</span><span class="sxs-lookup"><span data-stu-id="d7cea-207">hello following snippet shows this callback function:</span></span>

```c
static void SendConfirmationCallback(IOTHUB_CLIENT_CONFIRMATION_RESULT result, void* userContextCallback)
{
    EVENT_INSTANCE* eventInstance = (EVENT_INSTANCE*)userContextCallback;
    (void)printf("Confirmation[%d] received for message tracking id = %zu with result = %s\r\n", callbackCounter, eventInstance->messageTrackingId, ENUM_TO_STRING(IOTHUB_CLIENT_CONFIRMATION_RESULT, result));
    /* Some device specific action code goes here... */
    callbackCounter++;
    IoTHubMessage_Destroy(eventInstance->messageHandle);
}
```

<span data-ttu-id="d7cea-208">Обратите внимание, toohello вызов hello **IoTHubMessage\_Destroy** работать после завершения сообщение hello.</span><span class="sxs-lookup"><span data-stu-id="d7cea-208">Note hello call toohello **IoTHubMessage\_Destroy** function when you're done with hello message.</span></span> <span data-ttu-id="d7cea-209">Эта функция освобождает hello ресурсы, выделенные во время создания приветственных сообщений.</span><span class="sxs-lookup"><span data-stu-id="d7cea-209">This function frees hello resources allocated when you created hello message.</span></span>

### <a name="receive-messages"></a><span data-ttu-id="d7cea-210">Получение сообщений</span><span class="sxs-lookup"><span data-stu-id="d7cea-210">Receive messages</span></span>

<span data-ttu-id="d7cea-211">Получение сообщения является асинхронной операцией.</span><span class="sxs-lookup"><span data-stu-id="d7cea-211">Receiving a message is an asynchronous operation.</span></span> <span data-ttu-id="d7cea-212">Сначала необходимо зарегистрировать обратный вызов tooinvoke hello Получив сообщение hello устройства:</span><span class="sxs-lookup"><span data-stu-id="d7cea-212">First, you register hello callback tooinvoke when hello device receives a message:</span></span>

```c
if (IoTHubClient_LL_SetMessageCallback(iotHubClientHandle, ReceiveMessageCallback, &receiveContext) != IOTHUB_CLIENT_OK)
{
    (void)printf("ERROR: IoTHubClient_LL_SetMessageCallback..........FAILED!\r\n");
}
else
{
    (void)printf("IoTHubClient_LL_SetMessageCallback...successful.\r\n");
...
```

<span data-ttu-id="d7cea-213">Последний параметр Hello является toowhatever указателя void, которые нужно.</span><span class="sxs-lookup"><span data-stu-id="d7cea-213">hello last parameter is a void pointer toowhatever you want.</span></span> <span data-ttu-id="d7cea-214">В образце hello, он является целым числом tooan указателя, но это может быть tooa указатель более сложная структура данных.</span><span class="sxs-lookup"><span data-stu-id="d7cea-214">In hello sample, it's a pointer tooan integer but it could be a pointer tooa more complex data structure.</span></span> <span data-ttu-id="d7cea-215">Этот параметр включает hello toooperate функции обратного вызова на общего состояния с вызывающим объектом hello этой функции.</span><span class="sxs-lookup"><span data-stu-id="d7cea-215">This parameter enables hello callback function toooperate on shared state with hello caller of this function.</span></span>

<span data-ttu-id="d7cea-216">Получив сообщение hello устройства hello зарегистрированного обратного вызова вызывается функция.</span><span class="sxs-lookup"><span data-stu-id="d7cea-216">When hello device receives a message, hello registered callback function is invoked.</span></span> <span data-ttu-id="d7cea-217">Эта функция обратного вызова получает следующее:</span><span class="sxs-lookup"><span data-stu-id="d7cea-217">This callback function retrieves:</span></span>

* <span data-ttu-id="d7cea-218">Идентификатор сообщения Hello и идентификатора корреляции из приветственное сообщение.</span><span class="sxs-lookup"><span data-stu-id="d7cea-218">hello message id and correlation id from hello message.</span></span>
* <span data-ttu-id="d7cea-219">содержимое сообщения Hello.</span><span class="sxs-lookup"><span data-stu-id="d7cea-219">hello message content.</span></span>
* <span data-ttu-id="d7cea-220">Пользовательские свойства из сообщения hello.</span><span class="sxs-lookup"><span data-stu-id="d7cea-220">Any custom properties from hello message.</span></span>

```c
static IOTHUBMESSAGE_DISPOSITION_RESULT ReceiveMessageCallback(IOTHUB_MESSAGE_HANDLE message, void* userContextCallback)
{
    int* counter = (int*)userContextCallback;
    const char* buffer;
    size_t size;
    MAP_HANDLE mapProperties;
    const char* messageId;
    const char* correlationId;

    // Message properties
    if ((messageId = IoTHubMessage_GetMessageId(message)) == NULL)
    {
        messageId = "<null>";
    }

    if ((correlationId = IoTHubMessage_GetCorrelationId(message)) == NULL)
    {
        correlationId = "<null>";
    }

    // Message content
    if (IoTHubMessage_GetByteArray(message, (const unsigned char**)&buffer, &size) != IOTHUB_MESSAGE_OK)
    {
        (void)printf("unable tooretrieve hello message data\r\n");
    }
    else
    {
        (void)printf("Received Message [%d]\r\n Message ID: %s\r\n Correlation ID: %s\r\n Data: <<<%.*s>>> & Size=%d\r\n", *counter, messageId, correlationId, (int)size, buffer, (int)size);
        // If we receive hello work 'quit' then we stop running
        if (size == (strlen("quit") * sizeof(char)) && memcmp(buffer, "quit", size) == 0)
        {
            g_continueRunning = false;
        }
    }

    // Retrieve properties from hello message
    mapProperties = IoTHubMessage_Properties(message);
    if (mapProperties != NULL)
    {
        const char*const* keys;
        const char*const* values;
        size_t propertyCount = 0;
        if (Map_GetInternals(mapProperties, &keys, &values, &propertyCount) == MAP_OK)
        {
            if (propertyCount > 0)
            {
                size_t index;

                printf(" Message Properties:\r\n");
                for (index = 0; index < propertyCount; index++)
                {
                    (void)printf("\tKey: %s Value: %s\r\n", keys[index], values[index]);
                }
                (void)printf("\r\n");
            }
        }
    }

    /* Some device specific action code goes here... */
    (*counter)++;
    return IOTHUBMESSAGE_ACCEPTED;
}
```

<span data-ttu-id="d7cea-221">Используйте hello **IoTHubMessage\_GetByteArray** функция tooretrieve приветственное сообщение, которое является строкой в этом примере.</span><span class="sxs-lookup"><span data-stu-id="d7cea-221">Use hello **IoTHubMessage\_GetByteArray** function tooretrieve hello message, which in this example is a string.</span></span>

### <a name="uninitialize-hello-library"></a><span data-ttu-id="d7cea-222">Отмена инициализации библиотеки hello</span><span class="sxs-lookup"><span data-stu-id="d7cea-222">Uninitialize hello library</span></span>

<span data-ttu-id="d7cea-223">При завершения отправки событий и получении сообщений деинициализацию hello IoT библиотеки.</span><span class="sxs-lookup"><span data-stu-id="d7cea-223">When you're done sending events and receiving messages, you can uninitialize hello IoT library.</span></span> <span data-ttu-id="d7cea-224">toodo таким образом, выполните следующий вызов функции hello:</span><span class="sxs-lookup"><span data-stu-id="d7cea-224">toodo so, issue hello following function call:</span></span>

```
IoTHubClient_LL_Destroy(iotHubClientHandle);
```

<span data-ttu-id="d7cea-225">Этот вызов освободит ресурсы hello, ранее выделенный методом hello **IoTHubClient\_CreateFromConnectionString** функции.</span><span class="sxs-lookup"><span data-stu-id="d7cea-225">This call frees up hello resources previously allocated by hello **IoTHubClient\_CreateFromConnectionString** function.</span></span>

<span data-ttu-id="d7cea-226">Как видите, он просто toosend и получать сообщения с hello **IoTHubClient** библиотеки.</span><span class="sxs-lookup"><span data-stu-id="d7cea-226">As you can see, it's easy toosend and receive messages with hello **IoTHubClient** library.</span></span> <span data-ttu-id="d7cea-227">Hello библиотеки hello параметры обрабатываются взаимодействует с центром IoT, включая какие toouse протокола (с точки зрения hello hello разработчика, это параметр конфигурации, простых).</span><span class="sxs-lookup"><span data-stu-id="d7cea-227">hello library handles hello details of communicating with IoT Hub, including which protocol toouse (from hello perspective of hello developer, this is a simple configuration option).</span></span>

<span data-ttu-id="d7cea-228">Hello **IoTHubClient** библиотека также предоставляет полный контроль над как данных hello tooserialize устройство отправляет tooIoT концентратора.</span><span class="sxs-lookup"><span data-stu-id="d7cea-228">hello **IoTHubClient** library also provides precise control over how tooserialize hello data your device sends tooIoT Hub.</span></span> <span data-ttu-id="d7cea-229">В некоторых случаях такой уровень управления является преимуществом, но в других это не нужны посвящена toobe в реализации.</span><span class="sxs-lookup"><span data-stu-id="d7cea-229">In some cases this level of control is an advantage, but in others it is an implementation detail that you don't want toobe concerned with.</span></span> <span data-ttu-id="d7cea-230">Если это так hello, можно использовать hello **сериализатор** библиотеку, которая описана в следующем разделе hello.</span><span class="sxs-lookup"><span data-stu-id="d7cea-230">If that's hello case, you might consider using hello **serializer** library, which is described in hello next section.</span></span>

## <a name="use-hello-serializer-library"></a><span data-ttu-id="d7cea-231">Использование библиотеки сериализатор hello</span><span class="sxs-lookup"><span data-stu-id="d7cea-231">Use hello serializer library</span></span>

<span data-ttu-id="d7cea-232">Здравствуйте, по существу **сериализатор** библиотеки располагается в верхней части hello **IoTHubClient** библиотеки в hello SDK.</span><span class="sxs-lookup"><span data-stu-id="d7cea-232">Conceptually hello **serializer** library sits on top of hello **IoTHubClient** library in hello SDK.</span></span> <span data-ttu-id="d7cea-233">Она использует hello **IoTHubClient** библиотеки для hello базового обмена данными с центра IoT, но он добавляет возможности моделирования, удалите hello нагрузку задач, связанных с сериализацией сообщения hello разработчика.</span><span class="sxs-lookup"><span data-stu-id="d7cea-233">It uses hello **IoTHubClient** library for hello underlying communication with IoT Hub, but it adds modeling capabilities that remove hello burden of dealing with message serialization from hello developer.</span></span> <span data-ttu-id="d7cea-234">Работу этой библиотеки лучше всего продемонстрировать на примере.</span><span class="sxs-lookup"><span data-stu-id="d7cea-234">How this library works is best demonstrated by an example.</span></span>

<span data-ttu-id="d7cea-235">Hello внутри **сериализатор** папки в hello [хранилища azure iot-sdk c](https://github.com/Azure/azure-iot-sdk-c), является **образцы** папку, содержащую приложение называется **simplesample \_mqtt**.</span><span class="sxs-lookup"><span data-stu-id="d7cea-235">Inside hello **serializer** folder in hello [azure-iot-sdk-c repository](https://github.com/Azure/azure-iot-sdk-c), is a **samples** folder that contains an application called **simplesample\_mqtt**.</span></span> <span data-ttu-id="d7cea-236">версия Windows Hello этот образец содержит hello следующие решения Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="d7cea-236">hello Windows version of this sample includes hello following Visual Studio solution:</span></span>

  ![](media/iot-hub-device-sdk-c-intro/14-simplesample_mqtt.PNG)

> [!NOTE]
> <span data-ttu-id="d7cea-237">При открытии этого проекта в Visual Studio 2017 г примите hello приглашения tooretarget hello toohello последнюю версию проекта.</span><span class="sxs-lookup"><span data-stu-id="d7cea-237">If you open this project in Visual Studio 2017, accept hello prompts tooretarget hello project toohello latest version.</span></span>

<span data-ttu-id="d7cea-238">Как и в предыдущем примере hello, это один включает несколько пакетов NuGet:</span><span class="sxs-lookup"><span data-stu-id="d7cea-238">As with hello previous sample, this one includes several NuGet packages:</span></span>

* <span data-ttu-id="d7cea-239">Microsoft.Azure.C.SharedUtility</span><span class="sxs-lookup"><span data-stu-id="d7cea-239">Microsoft.Azure.C.SharedUtility</span></span>
* <span data-ttu-id="d7cea-240">Microsoft.Azure.IoTHub.MqttTransport.</span><span class="sxs-lookup"><span data-stu-id="d7cea-240">Microsoft.Azure.IoTHub.MqttTransport</span></span>
* <span data-ttu-id="d7cea-241">Microsoft.Azure.IoTHub.IoTHubClient</span><span class="sxs-lookup"><span data-stu-id="d7cea-241">Microsoft.Azure.IoTHub.IoTHubClient</span></span>
* <span data-ttu-id="d7cea-242">Microsoft.Azure.IoTHub.Serializer</span><span class="sxs-lookup"><span data-stu-id="d7cea-242">Microsoft.Azure.IoTHub.Serializer</span></span>
* <span data-ttu-id="d7cea-243">Microsoft.Azure.umqtt.</span><span class="sxs-lookup"><span data-stu-id="d7cea-243">Microsoft.Azure.umqtt</span></span>

<span data-ttu-id="d7cea-244">Вы уже видели большинство этих пакетов в предыдущем примере hello, но **Microsoft.Azure.IoTHub.Serializer** новые.</span><span class="sxs-lookup"><span data-stu-id="d7cea-244">You've seen most of these packages in hello previous sample, but **Microsoft.Azure.IoTHub.Serializer** is new.</span></span> <span data-ttu-id="d7cea-245">Этот пакет является обязательным при использовании hello **сериализатор** библиотеки.</span><span class="sxs-lookup"><span data-stu-id="d7cea-245">This package is required when you use hello **serializer** library.</span></span>

<span data-ttu-id="d7cea-246">Реализация hello пример приложения hello можно найти в hello **simplesample\_mqtt.c** файла.</span><span class="sxs-lookup"><span data-stu-id="d7cea-246">You can find hello implementation of hello sample application in hello **simplesample\_mqtt.c** file.</span></span>

<span data-ttu-id="d7cea-247">Hello следующие разделы содержат пошаговые инструкции для hello ключевые элементы в этом примере.</span><span class="sxs-lookup"><span data-stu-id="d7cea-247">hello following sections walk you through hello key parts of this sample.</span></span>

### <a name="initialize-hello-library"></a><span data-ttu-id="d7cea-248">Инициализировать библиотеку hello</span><span class="sxs-lookup"><span data-stu-id="d7cea-248">Initialize hello library</span></span>

<span data-ttu-id="d7cea-249">Работа с hello toostart **сериализатор** библиотеки инициализации hello вызовов API-интерфейсы:</span><span class="sxs-lookup"><span data-stu-id="d7cea-249">toostart working with hello **serializer** library, call hello initialization APIs:</span></span>

```c
if (serializer_init(NULL) != SERIALIZER_OK)
{
    (void)printf("Failed on serializer_init\r\n");
}
else
{
    IOTHUB_CLIENT_LL_HANDLE iotHubClientHandle = IoTHubClient_LL_CreateFromConnectionString(connectionString, MQTT_Protocol);
    srand((unsigned int)time(NULL));
    int avgWindSpeed = 10;

    if (iotHubClientHandle == NULL)
    {
        (void)printf("Failed on IoTHubClient_LL_Create\r\n");
    }
    else
    {
        ContosoAnemometer* myWeather = CREATE_MODEL_INSTANCE(WeatherStation, ContosoAnemometer);
        if (myWeather == NULL)
        {
            (void)printf("Failed on CREATE_MODEL_INSTANCE\r\n");
        }
        else
        {
...
```

<span data-ttu-id="d7cea-250">Hello вызовов toohello **сериализатор\_init** функция одноразового вызова и инициализирует hello базовой библиотеки.</span><span class="sxs-lookup"><span data-stu-id="d7cea-250">hello call toohello **serializer\_init** function is a one-time call and initializes hello underlying library.</span></span> <span data-ttu-id="d7cea-251">Затем вызовите метод hello **IoTHubClient\_LL\_CreateFromConnectionString** функции, которая является hello же API, как и hello **IoTHubClient** образца.</span><span class="sxs-lookup"><span data-stu-id="d7cea-251">Then, you call hello **IoTHubClient\_LL\_CreateFromConnectionString** function, which is hello same API as in hello **IoTHubClient** sample.</span></span> <span data-ttu-id="d7cea-252">Этот вызов устанавливает строки подключения устройства (этот вызов является также где выбрано протокола hello требуется toouse).</span><span class="sxs-lookup"><span data-stu-id="d7cea-252">This call sets your device connection string (this call is also where you choose hello protocol you want toouse).</span></span> <span data-ttu-id="d7cea-253">Этот образец использует MQTT в качестве транспорта hello, но может использовать AMQP или HTTP.</span><span class="sxs-lookup"><span data-stu-id="d7cea-253">This sample uses MQTT as hello transport, but could use AMQP or HTTP.</span></span>

<span data-ttu-id="d7cea-254">Наконец, вызовите hello **создать\_МОДЕЛИ\_ЭКЗЕМПЛЯР** функции.</span><span class="sxs-lookup"><span data-stu-id="d7cea-254">Finally, call hello **CREATE\_MODEL\_INSTANCE** function.</span></span> <span data-ttu-id="d7cea-255">**WeatherStation** hello пространства имен модели hello и **ContosoAnemometer** является именем hello hello модели.</span><span class="sxs-lookup"><span data-stu-id="d7cea-255">**WeatherStation** is hello namespace of hello model and **ContosoAnemometer** is hello name of hello model.</span></span> <span data-ttu-id="d7cea-256">После создания экземпляра hello модели можно использовать toostart отправки и получения сообщений.</span><span class="sxs-lookup"><span data-stu-id="d7cea-256">Once hello model instance is created, you can use it toostart sending and receiving messages.</span></span> <span data-ttu-id="d7cea-257">Однако это важно toounderstand, какая модель —.</span><span class="sxs-lookup"><span data-stu-id="d7cea-257">However, it's important toounderstand what a model is.</span></span>

### <a name="define-hello-model"></a><span data-ttu-id="d7cea-258">Определение модели hello</span><span class="sxs-lookup"><span data-stu-id="d7cea-258">Define hello model</span></span>

<span data-ttu-id="d7cea-259">Модель в hello **сериализатор** библиотека определяет сообщений hello, устройство может отправлять tooIoT концентратора и hello сообщений, называемую *действия* в моделирования язык, который он может получать hello.</span><span class="sxs-lookup"><span data-stu-id="d7cea-259">A model in hello **serializer** library defines hello messages that your device can send tooIoT Hub and hello messages, called *actions* in hello modeling language, which it can receive.</span></span> <span data-ttu-id="d7cea-260">Определить модель, используя набор макросов C, как hello **simplesample\_mqtt** образец приложения:</span><span class="sxs-lookup"><span data-stu-id="d7cea-260">You define a model using a set of C macros as in hello **simplesample\_mqtt** sample application:</span></span>

```c
BEGIN_NAMESPACE(WeatherStation);

DECLARE_MODEL(ContosoAnemometer,
WITH_DATA(ascii_char_ptr, DeviceId),
WITH_DATA(int, WindSpeed),
WITH_ACTION(TurnFanOn),
WITH_ACTION(TurnFanOff),
WITH_ACTION(SetAirResistance, int, Position)
);

END_NAMESPACE(WeatherStation);
```

<span data-ttu-id="d7cea-261">Hello **НАЧАТЬ\_пространства ИМЕН** и **окончания\_ИМЕН** макросы обоих перевести пространство имен hello hello модели в качестве аргумента.</span><span class="sxs-lookup"><span data-stu-id="d7cea-261">hello **BEGIN\_NAMESPACE** and **END\_NAMESPACE** macros both take hello namespace of hello model as an argument.</span></span> <span data-ttu-id="d7cea-262">Что-либо между эти макросы ожидается hello определение модели или моделей и структур данных hello, использующих hello моделей.</span><span class="sxs-lookup"><span data-stu-id="d7cea-262">It's expected that anything between these macros is hello definition of your model or models, and hello data structures that hello models use.</span></span>

<span data-ttu-id="d7cea-263">В этом примере приведена одна модель с именем **ContosoAnemometer**.</span><span class="sxs-lookup"><span data-stu-id="d7cea-263">In this example, there is a single model called **ContosoAnemometer**.</span></span> <span data-ttu-id="d7cea-264">Эта модель определяет два блока данных, что устройство может отправлять tooIoT концентратора: **DeviceId** и **WindSpeed**.</span><span class="sxs-lookup"><span data-stu-id="d7cea-264">This model defines two pieces of data that your device can send tooIoT Hub: **DeviceId** and **WindSpeed**.</span></span> <span data-ttu-id="d7cea-265">Она также определяет три действия (сообщения), которые ваше устройство может получить: **TurnFanOn**, **TurnFanOff** и **SetAirResistance**.</span><span class="sxs-lookup"><span data-stu-id="d7cea-265">It also defines three actions (messages) that your device can receive: **TurnFanOn**, **TurnFanOff**, and **SetAirResistance**.</span></span> <span data-ttu-id="d7cea-266">Каждый элемент данных имеет тип, а каждое действие имеет имя (и при необходимости набор параметров).</span><span class="sxs-lookup"><span data-stu-id="d7cea-266">Each data element has a type, and each action has a name (and optionally a set of parameters).</span></span>

<span data-ttu-id="d7cea-267">данные Hello и действия, определенные в модели hello определить рабочую область API, можно использовать tooIoT сообщения toosend концентратора и отвечать отправляемых toomessages toohello устройства.</span><span class="sxs-lookup"><span data-stu-id="d7cea-267">hello data and actions defined in hello model define an API surface that you can use toosend messages tooIoT Hub, and respond toomessages sent toohello device.</span></span> <span data-ttu-id="d7cea-268">Лучше всего это показать на примере.</span><span class="sxs-lookup"><span data-stu-id="d7cea-268">Use of this model is best understood through an example.</span></span>

### <a name="send-messages"></a><span data-ttu-id="d7cea-269">Отправка сообщений</span><span class="sxs-lookup"><span data-stu-id="d7cea-269">Send messages</span></span>

<span data-ttu-id="d7cea-270">модель Hello определяет hello данные можно отправить tooIoT концентратора.</span><span class="sxs-lookup"><span data-stu-id="d7cea-270">hello model defines hello data you can send tooIoT Hub.</span></span> <span data-ttu-id="d7cea-271">В этом примере, означает одно из hello два элемента данных, определенного с помощью hello **WITH_DATA** макрос.</span><span class="sxs-lookup"><span data-stu-id="d7cea-271">In this example, that means one of hello two data items defined using hello **WITH_DATA** macro.</span></span> <span data-ttu-id="d7cea-272">Существуют несколько шагов, необходимых toosend **DeviceId** и **WindSpeed** центр IoT tooan значения.</span><span class="sxs-lookup"><span data-stu-id="d7cea-272">There are several steps required toosend **DeviceId** and **WindSpeed** values tooan IoT hub.</span></span> <span data-ttu-id="d7cea-273">Во-первых, Hello является tooset hello данных, toosend:</span><span class="sxs-lookup"><span data-stu-id="d7cea-273">hello first is tooset hello data you want toosend:</span></span>

```c
myWeather->DeviceId = "myFirstDevice";
myWeather->WindSpeed = avgWindSpeed + (rand() % 4 + 2);
```

<span data-ttu-id="d7cea-274">Hello модель, определенную ранее позволяет tooset hello значений, установив члены **структуры**.</span><span class="sxs-lookup"><span data-stu-id="d7cea-274">hello model you defined earlier enables you tooset hello values by setting members of a **struct**.</span></span> <span data-ttu-id="d7cea-275">Далее сериализации приветственное сообщение, что нужно toosend:</span><span class="sxs-lookup"><span data-stu-id="d7cea-275">Next, serialize hello message you want toosend:</span></span>

```c
unsigned char* destination;
size_t destinationSize;
if (SERIALIZE(&destination, &destinationSize, myWeather->DeviceId, myWeather->WindSpeed) != CODEFIRST_OK)
{
    (void)printf("Failed tooserialize\r\n");
}
else
{
    sendMessage(iotHubClientHandle, destination, destinationSize);
    free(destination);
}
```

<span data-ttu-id="d7cea-276">Этот код выполняет сериализацию буфера tooa устройства в облако hello (ссылается **назначения**).</span><span class="sxs-lookup"><span data-stu-id="d7cea-276">This code serializes hello device-to-cloud tooa buffer (referenced by **destination**).</span></span> <span data-ttu-id="d7cea-277">Hello код запускает hello **sendMessage** функции tooIoT сообщение hello toosend концентратора:</span><span class="sxs-lookup"><span data-stu-id="d7cea-277">hello code then invokes hello **sendMessage** function toosend hello message tooIoT Hub:</span></span>

```c
static void sendMessage(IOTHUB_CLIENT_LL_HANDLE iotHubClientHandle, const unsigned char* buffer, size_t size)
{
    static unsigned int messageTrackingId;
    IOTHUB_MESSAGE_HANDLE messageHandle = IoTHubMessage_CreateFromByteArray(buffer, size);
    if (messageHandle == NULL)
    {
        printf("unable toocreate a new IoTHubMessage\r\n");
    }
    else
    {
        if (IoTHubClient_LL_SendEventAsync(iotHubClientHandle, messageHandle, sendCallback, (void*)(uintptr_t)messageTrackingId) != IOTHUB_CLIENT_OK)
        {
            printf("failed toohand over hello message tooIoTHubClient");
        }
        else
        {
            printf("IoTHubClient accepted hello message for delivery\r\n");
        }
        IoTHubMessage_Destroy(messageHandle);
    }
    messageTrackingId++;
}
```


<span data-ttu-id="d7cea-278">Здравствуйте, второй параметр toolast **IoTHubClient\_LL\_SendEventAsync** имеет функцию обратного вызова tooa ссылку, которая вызывается, когда данные hello успешно отправлен.</span><span class="sxs-lookup"><span data-stu-id="d7cea-278">hello second toolast parameter of **IoTHubClient\_LL\_SendEventAsync** is a reference tooa callback function that's called when hello data is successfully sent.</span></span> <span data-ttu-id="d7cea-279">В образце hello Вот hello функции обратного вызова.</span><span class="sxs-lookup"><span data-stu-id="d7cea-279">Here's hello callback function in hello sample:</span></span>

```c
void sendCallback(IOTHUB_CLIENT_CONFIRMATION_RESULT result, void* userContextCallback)
{
    unsigned int messageTrackingId = (unsigned int)(uintptr_t)userContextCallback;

    (void)printf("Message Id: %u Received.\r\n", messageTrackingId);

    (void)printf("Result Call Back Called! Result is: %s \r\n", ENUM_TO_STRING(IOTHUB_CLIENT_CONFIRMATION_RESULT, result));
}
```

<span data-ttu-id="d7cea-280">Второй параметр Hello — контекст toouser указателя; Hello же указатель передан слишком**IoTHubClient\_LL\_SendEventAsync**.</span><span class="sxs-lookup"><span data-stu-id="d7cea-280">hello second parameter is a pointer toouser context; hello same pointer passed too**IoTHubClient\_LL\_SendEventAsync**.</span></span> <span data-ttu-id="d7cea-281">В этом случае hello контекста представляет собой простой счетчик, но он может быть любым способом.</span><span class="sxs-lookup"><span data-stu-id="d7cea-281">In this case, hello context is a simple counter, but it can be anything you want.</span></span>

<span data-ttu-id="d7cea-282">Это все, нет сообщений toosending устройства в облако.</span><span class="sxs-lookup"><span data-stu-id="d7cea-282">That's all there is toosending device-to-cloud messages.</span></span> <span data-ttu-id="d7cea-283">Hello только что осталось toocover — как tooreceive сообщений.</span><span class="sxs-lookup"><span data-stu-id="d7cea-283">hello only thing left toocover is how tooreceive messages.</span></span>

### <a name="receive-messages"></a><span data-ttu-id="d7cea-284">Получение сообщений</span><span class="sxs-lookup"><span data-stu-id="d7cea-284">Receive messages</span></span>

<span data-ttu-id="d7cea-285">Получение сообщения работает аналогично toohello, как работают сообщения в hello **IoTHubClient** библиотеки.</span><span class="sxs-lookup"><span data-stu-id="d7cea-285">Receiving a message works similarly toohello way messages work in hello **IoTHubClient** library.</span></span> <span data-ttu-id="d7cea-286">Сначала вам нужно зарегистрировать функцию обратного вызова сообщения:</span><span class="sxs-lookup"><span data-stu-id="d7cea-286">First, you register a message callback function:</span></span>

```c
if (IoTHubClient_LL_SetMessageCallback(iotHubClientHandle, IoTHubMessage, myWeather) != IOTHUB_CLIENT_OK)
{
    printf("unable tooIoTHubClient_SetMessageCallback\r\n");
}
else
{
...
```

<span data-ttu-id="d7cea-287">Затем можно написать hello функции обратного вызова, вызываемый при получении сообщения:</span><span class="sxs-lookup"><span data-stu-id="d7cea-287">Then, you write hello callback function that's invoked when a message is received:</span></span>

```c
static IOTHUBMESSAGE_DISPOSITION_RESULT IoTHubMessage(IOTHUB_MESSAGE_HANDLE message, void* userContextCallback)
{
    IOTHUBMESSAGE_DISPOSITION_RESULT result;
    const unsigned char* buffer;
    size_t size;
    if (IoTHubMessage_GetByteArray(message, &buffer, &size) != IOTHUB_MESSAGE_OK)
    {
        printf("unable tooIoTHubMessage_GetByteArray\r\n");
        result = IOTHUBMESSAGE_ABANDONED;
    }
    else
    {
        /*buffer is not zero terminated*/
        char* temp = malloc(size + 1);
        if (temp == NULL)
        {
            printf("failed toomalloc\r\n");
            result = IOTHUBMESSAGE_ABANDONED;
        }
        else
        {
            (void)memcpy(temp, buffer, size);
            temp[size] = '\0';
            EXECUTE_COMMAND_RESULT executeCommandResult = EXECUTE_COMMAND(userContextCallback, temp);
            result =
                (executeCommandResult == EXECUTE_COMMAND_ERROR) ? IOTHUBMESSAGE_ABANDONED :
                (executeCommandResult == EXECUTE_COMMAND_SUCCESS) ? IOTHUBMESSAGE_ACCEPTED :
                IOTHUBMESSAGE_REJECTED;
            free(temp);
        }
    }
    return result;
}
```

<span data-ttu-id="d7cea-288">Этот код представляет собой шаблон--имеет hello одинаково для любого решения.</span><span class="sxs-lookup"><span data-stu-id="d7cea-288">This code is boilerplate -- it's hello same for any solution.</span></span> <span data-ttu-id="d7cea-289">Эта функция получает приветственное сообщение и отвечает за маршрутизацию toohello соответствующую функцию через вызов hello слишком**EXECUTE\_команда**.</span><span class="sxs-lookup"><span data-stu-id="d7cea-289">This function receives hello message and takes care of routing it toohello appropriate function through hello call too**EXECUTE\_COMMAND**.</span></span> <span data-ttu-id="d7cea-290">Hello функция, вызываемая в этот момент зависит от определения hello hello действий в модели.</span><span class="sxs-lookup"><span data-stu-id="d7cea-290">hello function called at this point depends on hello definition of hello actions in your model.</span></span>

<span data-ttu-id="d7cea-291">При определении действия в модели, вы будете необходимые tooimplement функция, которая вызывается, когда устройство получает соответствующее сообщение hello.</span><span class="sxs-lookup"><span data-stu-id="d7cea-291">When you define an action in your model, you're required tooimplement a function that's called when your device receives hello corresponding message.</span></span> <span data-ttu-id="d7cea-292">Например, если модель определяет следующее действие:</span><span class="sxs-lookup"><span data-stu-id="d7cea-292">For example, if your model defines this action:</span></span>

```c
WITH_ACTION(SetAirResistance, int, Position)
```

<span data-ttu-id="d7cea-293">Определите функцию со следующей сигнатурой:</span><span class="sxs-lookup"><span data-stu-id="d7cea-293">Define a function with this signature:</span></span>

```c
EXECUTE_COMMAND_RESULT SetAirResistance(ContosoAnemometer* device, int Position)
{
    (void)device;
    (void)printf("Setting Air Resistance Position too%d.\r\n", Position);
    return EXECUTE_COMMAND_SUCCESS;
}
```

<span data-ttu-id="d7cea-294">Обратите внимание на то, как имя hello hello функции совпадает с именем hello действия hello в модели hello и hello параметры функции hello соответствуют hello параметры, указанные для действий hello.</span><span class="sxs-lookup"><span data-stu-id="d7cea-294">Note how hello name of hello function matches hello name of hello action in hello model and that hello parameters of hello function match hello parameters specified for hello action.</span></span> <span data-ttu-id="d7cea-295">Первый параметр Hello всегда является обязательным и содержит указатель toohello экземпляр модели.</span><span class="sxs-lookup"><span data-stu-id="d7cea-295">hello first parameter is always required and contains a pointer toohello instance of your model.</span></span>

<span data-ttu-id="d7cea-296">Когда hello устройство получает сообщение, соответствующий данной сигнатуре, вызывается соответствующая функция hello.</span><span class="sxs-lookup"><span data-stu-id="d7cea-296">When hello device receives a message that matches this signature, hello corresponding function is called.</span></span> <span data-ttu-id="d7cea-297">Таким образом, кроме имеющих tooinclude hello стандартный код из **IoTHubMessage**, получения сообщений является простым определения простую функцию для каждого действия, определенный в модели.</span><span class="sxs-lookup"><span data-stu-id="d7cea-297">Therefore, aside from having tooinclude hello boilerplate code from **IoTHubMessage**, receiving messages is just a matter of defining a simple function for each action defined in your model.</span></span>

### <a name="uninitialize-hello-library"></a><span data-ttu-id="d7cea-298">Отмена инициализации библиотеки hello</span><span class="sxs-lookup"><span data-stu-id="d7cea-298">Uninitialize hello library</span></span>

<span data-ttu-id="d7cea-299">При завершения операции отправки данных и получении сообщений деинициализацию hello IoT библиотеки.</span><span class="sxs-lookup"><span data-stu-id="d7cea-299">When you're done sending data and receiving messages, you can uninitialize hello IoT library:</span></span>

```c
...
        DESTROY_MODEL_INSTANCE(myWeather);
    }
    IoTHubClient_LL_Destroy(iotHubClientHandle);
}
serializer_deinit();
```

<span data-ttu-id="d7cea-300">Каждая из этих трех функций выравнивается hello описанных выше трех функций инициализации.</span><span class="sxs-lookup"><span data-stu-id="d7cea-300">Each of these three functions aligns with hello three initialization functions described previously.</span></span> <span data-ttu-id="d7cea-301">Вызов этих API позволит освободить выделенные ранее ресурсы.</span><span class="sxs-lookup"><span data-stu-id="d7cea-301">Calling these APIs ensures that you free previously allocated resources.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d7cea-302">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="d7cea-302">Next Steps</span></span>

<span data-ttu-id="d7cea-303">В этой статье рассматриваются основы использования библиотек hello в hello hello **устройств Azure IoT SDK для C**. Он предоставлен toounderstand достаточно информации, содержание hello SDK, его архитектуры и как tooget начата работа с hello образцов Windows.</span><span class="sxs-lookup"><span data-stu-id="d7cea-303">This article covered hello basics of using hello libraries in hello **Azure IoT device SDK for C**. It provided you with enough information toounderstand what's included in hello SDK, its architecture, and how tooget started working with hello Windows samples.</span></span> <span data-ttu-id="d7cea-304">Далее статья Hello продолжает hello описание hello SDK объясняя [Дополнительные сведения о библиотеке IoTHubClient hello](iot-hub-device-sdk-c-iothubclient.md).</span><span class="sxs-lookup"><span data-stu-id="d7cea-304">hello next article continues hello description of hello SDK by explaining [more about hello IoTHubClient library](iot-hub-device-sdk-c-iothubclient.md).</span></span>

<span data-ttu-id="d7cea-305">toolearn Дополнительные сведения о разработке приложений для центра IoT. в разделе hello [пакеты SDK Azure IoT][lnk-sdks].</span><span class="sxs-lookup"><span data-stu-id="d7cea-305">toolearn more about developing for IoT Hub, see hello [Azure IoT SDKs][lnk-sdks].</span></span>

<span data-ttu-id="d7cea-306">Изучение возможностей hello центра IoT toofurther см. в разделе:</span><span class="sxs-lookup"><span data-stu-id="d7cea-306">toofurther explore hello capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="d7cea-307">[Отправка сообщений с устройства в облако с помощью имитации устройства (Linux) с использованием Edge Интернета вещей Azure][lnk-iotedge]</span><span class="sxs-lookup"><span data-stu-id="d7cea-307">[Simulating a device with Azure IoT Edge][lnk-iotedge]</span></span>

[lnk-file upload]: iot-hub-csharp-csharp-file-upload.md
[lnk-create-hub]: iot-hub-rm-template-powershell.md
[lnk-c-sdk]: iot-hub-device-sdk-c-intro.md
[lnk-sdks]: iot-hub-devguide-sdks.md

[lnk-iotedge]: iot-hub-linux-iot-edge-simulated-device.md
