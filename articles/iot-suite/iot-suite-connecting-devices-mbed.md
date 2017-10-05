---
title: "Подключение устройства с помощью C в mbed | Документация Майкрософт"
description: "Описывает, как подключить устройство к предварительно настроенному решению для удаленного мониторинга из набора Azure IoT Suite с помощью приложения на C, запущенного на устройстве mbed."
services: 
suite: iot-suite
documentationcenter: na
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 9551075e-dcf9-488f-943e-d0eb0e6260be
ms.service: iot-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/22/2017
ms.author: dobett
ROBOTS: NOINDEX
ms.openlocfilehash: ef7b78f85a787f8fbe22c0e26aa34f0cd1685d58
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="connect-your-device-to-the-remote-monitoring-preconfigured-solution-mbed"></a><span data-ttu-id="0f2c6-103">Подключение устройства к предварительно настроенному решению для удаленного мониторинга (mbed)</span><span class="sxs-lookup"><span data-stu-id="0f2c6-103">Connect your device to the remote monitoring preconfigured solution (mbed)</span></span>

## <a name="scenario-overview"></a><span data-ttu-id="0f2c6-104">Обзор сценария</span><span class="sxs-lookup"><span data-stu-id="0f2c6-104">Scenario overview</span></span>
<span data-ttu-id="0f2c6-105">В этом примере создается устройство, которое отправляет следующие данные телеметрии в [предварительно настроенное решение][lnk-what-are-preconfig-solutions] для удаленного мониторинга:</span><span class="sxs-lookup"><span data-stu-id="0f2c6-105">In this scenario, you create a device that sends the following telemetry to the remote monitoring [preconfigured solution][lnk-what-are-preconfig-solutions]:</span></span>

* <span data-ttu-id="0f2c6-106">наружная температура;</span><span class="sxs-lookup"><span data-stu-id="0f2c6-106">External temperature</span></span>
* <span data-ttu-id="0f2c6-107">внутренняя температура;</span><span class="sxs-lookup"><span data-stu-id="0f2c6-107">Internal temperature</span></span>
* <span data-ttu-id="0f2c6-108">влажность.</span><span class="sxs-lookup"><span data-stu-id="0f2c6-108">Humidity</span></span>

<span data-ttu-id="0f2c6-109">В целях упрощения код на устройстве генерирует образцы значений, но мы рекомендуем расширить пример и подключить к устройству реальные датчики и отправить реальные данные телеметрии.</span><span class="sxs-lookup"><span data-stu-id="0f2c6-109">For simplicity, the code on the device generates sample values, but we encourage you to extend the sample by connecting real sensors to your device and sending real telemetry.</span></span>

<span data-ttu-id="0f2c6-110">Устройство также может отвечать на методы, вызываемые из панели мониторинга решения, и значения требуемых свойств, заданные на панели мониторинга решения.</span><span class="sxs-lookup"><span data-stu-id="0f2c6-110">The device is also able to respond to methods invoked from the solution dashboard and desired property values set in the solution dashboard.</span></span>

<span data-ttu-id="0f2c6-111">Для работы с этим руководством требуется активная учетная запись Azure.</span><span class="sxs-lookup"><span data-stu-id="0f2c6-111">To complete this tutorial, you need an active Azure account.</span></span> <span data-ttu-id="0f2c6-112">Если ее нет, можно создать бесплатную пробную учетную запись всего за несколько минут.</span><span class="sxs-lookup"><span data-stu-id="0f2c6-112">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="0f2c6-113">Дополнительные сведения см. в статье о [бесплатной пробной версии Azure][lnk-free-trial].</span><span class="sxs-lookup"><span data-stu-id="0f2c6-113">For details, see [Azure Free Trial][lnk-free-trial].</span></span>

## <a name="before-you-start"></a><span data-ttu-id="0f2c6-114">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="0f2c6-114">Before you start</span></span>
<span data-ttu-id="0f2c6-115">До написания кода для устройства необходимо подготовить свое предварительно настроенное решение для удаленного мониторинга, а затем подготовить в нем новое пользовательское устройство.</span><span class="sxs-lookup"><span data-stu-id="0f2c6-115">Before you write any code for your device, you must provision your remote monitoring preconfigured solution and provision a new custom device in that solution.</span></span>

### <a name="provision-your-remote-monitoring-preconfigured-solution"></a><span data-ttu-id="0f2c6-116">Подготовка предварительно настроенного решения для удаленного мониторинга</span><span class="sxs-lookup"><span data-stu-id="0f2c6-116">Provision your remote monitoring preconfigured solution</span></span>
<span data-ttu-id="0f2c6-117">Созданное в этом руководстве устройство отправляет данные в экземпляр предварительно настроенного решения для [удаленного мониторинга][lnk-remote-monitoring].</span><span class="sxs-lookup"><span data-stu-id="0f2c6-117">The device you create in this tutorial sends data to an instance of the [remote monitoring][lnk-remote-monitoring] preconfigured solution.</span></span> <span data-ttu-id="0f2c6-118">Если вы еще не подготовили это решение в своей учетной записи Azure, то выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="0f2c6-118">If you haven't already provisioned the remote monitoring preconfigured solution in your Azure account, use the following steps:</span></span>

1. <span data-ttu-id="0f2c6-119">Чтобы создать решение, на странице <https://www.azureiotsuite.com/> щелкните знак **+**.</span><span class="sxs-lookup"><span data-stu-id="0f2c6-119">On the <https://www.azureiotsuite.com/> page, click **+** to create a solution.</span></span>
2. <span data-ttu-id="0f2c6-120">На панели **Удаленный мониторинг** щелкните **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="0f2c6-120">Click **Select** on the **Remote monitoring** panel to create your solution.</span></span>
3. <span data-ttu-id="0f2c6-121">На странице **Create Remote monitoring solution** (Создание решения для удаленного мониторинга) введите **имя решения** по своему усмотрению, выберите **регион** для развертывания и подписку Azure, которую нужно использовать.</span><span class="sxs-lookup"><span data-stu-id="0f2c6-121">On the **Create Remote monitoring solution** page, enter a **Solution name** of your choice, select the **Region** you want to deploy to, and select the Azure subscription to want to use.</span></span> <span data-ttu-id="0f2c6-122">Затем щелкните **Создать решение**.</span><span class="sxs-lookup"><span data-stu-id="0f2c6-122">Then click **Create solution**.</span></span>
4. <span data-ttu-id="0f2c6-123">Дождитесь завершения процесса подготовки.</span><span class="sxs-lookup"><span data-stu-id="0f2c6-123">Wait until the provisioning process completes.</span></span>

> [!WARNING]
> <span data-ttu-id="0f2c6-124">В предварительно настроенных решениях используются платные службы Azure.</span><span class="sxs-lookup"><span data-stu-id="0f2c6-124">The preconfigured solutions use billable Azure services.</span></span> <span data-ttu-id="0f2c6-125">Закончив работу с предварительно настроенным решением, не забудьте удалить его из подписки, чтобы избежать ненужных расходов.</span><span class="sxs-lookup"><span data-stu-id="0f2c6-125">Be sure to remove the preconfigured solution from your subscription when you are done with it to avoid any unnecessary charges.</span></span> <span data-ttu-id="0f2c6-126">На странице <https://www.azureiotsuite.com/> можно полностью удалить предварительно настроенное решение из подписки.</span><span class="sxs-lookup"><span data-stu-id="0f2c6-126">You can completely remove a preconfigured solution from your subscription by visiting the <https://www.azureiotsuite.com/> page.</span></span>
> 
> 

<span data-ttu-id="0f2c6-127">После завершения подготовки решения для удаленного мониторинга щелкните **Запустить** , чтобы открыть панель мониторинга этого решения в браузере.</span><span class="sxs-lookup"><span data-stu-id="0f2c6-127">When the provisioning process for the remote monitoring solution finishes, click **Launch** to open the solution dashboard in your browser.</span></span>

![Панель мониторинга решения][img-dashboard]

### <a name="provision-your-device-in-the-remote-monitoring-solution"></a><span data-ttu-id="0f2c6-129">Подготовка устройства в решении для удаленного мониторинга</span><span class="sxs-lookup"><span data-stu-id="0f2c6-129">Provision your device in the remote monitoring solution</span></span>
> [!NOTE]
> <span data-ttu-id="0f2c6-130">Если вы уже подготовили устройство в решении, пропустите этот шаг.</span><span class="sxs-lookup"><span data-stu-id="0f2c6-130">If you have already provisioned a device in your solution, you can skip this step.</span></span> <span data-ttu-id="0f2c6-131">При создании клиентского приложения необходимо знать учетные данные устройства.</span><span class="sxs-lookup"><span data-stu-id="0f2c6-131">You need to know the device credentials when you create the client application.</span></span>
> 
> 

<span data-ttu-id="0f2c6-132">Чтобы устройство смогло подключиться к предварительно настроенному решению, оно должно пройти идентификацию в центре IoT с использованием допустимых учетных данных.</span><span class="sxs-lookup"><span data-stu-id="0f2c6-132">For a device to connect to the preconfigured solution, it must identify itself to IoT Hub using valid credentials.</span></span> <span data-ttu-id="0f2c6-133">Учетные данные устройства можно получить на панели мониторинга решения.</span><span class="sxs-lookup"><span data-stu-id="0f2c6-133">You can retrieve the device credentials from the solution dashboard.</span></span> <span data-ttu-id="0f2c6-134">Вы добавите их в клиентское приложение далее в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="0f2c6-134">You include the device credentials in your client application later in this tutorial.</span></span>

<span data-ttu-id="0f2c6-135">Чтобы добавить устройство в решение для удаленного мониторинга, выполните следующие действия на панели мониторинга решения:</span><span class="sxs-lookup"><span data-stu-id="0f2c6-135">To add a device to your remote monitoring solution, complete the following steps in the solution dashboard:</span></span>

1. <span data-ttu-id="0f2c6-136">В левом нижнем углу панели мониторинга щелкните **Добавить устройство**.</span><span class="sxs-lookup"><span data-stu-id="0f2c6-136">In the lower left-hand corner of the dashboard, click **Add a device**.</span></span>
   
   ![Добавление устройства][1]
2. <span data-ttu-id="0f2c6-138">На панели **Пользовательское устройство** нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="0f2c6-138">In the **Custom Device** panel, click **Add new**.</span></span>
   
   ![Добавление пользовательского устройства][2]
3. <span data-ttu-id="0f2c6-140">Установите переключатель **Позвольте мне определить собственный идентификатор устройства**.</span><span class="sxs-lookup"><span data-stu-id="0f2c6-140">Choose **Let me define my own Device ID**.</span></span> <span data-ttu-id="0f2c6-141">Введите идентификатор устройства, например **mydevice**, и нажмите кнопку **Проверить идентификатор**, чтобы убедиться, что такое имя не используется. Затем нажмите кнопку **Создать**, чтобы подготовить устройство.</span><span class="sxs-lookup"><span data-stu-id="0f2c6-141">Enter a Device ID such as **mydevice**, click **Check ID** to verify that name isn't already in use, and then click **Create** to provision the device.</span></span>
   
   ![Добавление идентификатора устройства][3]
4. <span data-ttu-id="0f2c6-143">Запишите учетные данные (идентификатор устройства, имя узла в Центре Интернета вещей и ключ устройства).</span><span class="sxs-lookup"><span data-stu-id="0f2c6-143">Make a note the device credentials (Device ID, IoT Hub Hostname, and Device Key).</span></span> <span data-ttu-id="0f2c6-144">Эти значения потребуются клиентскому приложению при подключении к решению для удаленного мониторинга.</span><span class="sxs-lookup"><span data-stu-id="0f2c6-144">Your client application needs these values to connect to the remote monitoring solution.</span></span> <span data-ttu-id="0f2c6-145">Затем нажмите кнопку **Done**(Готово).</span><span class="sxs-lookup"><span data-stu-id="0f2c6-145">Then click **Done**.</span></span>
   
    ![Просмотр учетных данных устройства][4]
5. <span data-ttu-id="0f2c6-147">Выберите устройство в списке устройств на панели мониторинга решения.</span><span class="sxs-lookup"><span data-stu-id="0f2c6-147">Select your device in the device list in the solution dashboard.</span></span> <span data-ttu-id="0f2c6-148">Затем на панели **Сведения об устройстве** щелкните **Включить устройство**.</span><span class="sxs-lookup"><span data-stu-id="0f2c6-148">Then, in the **Device Details** panel, click **Enable Device**.</span></span> <span data-ttu-id="0f2c6-149">Теперь текущее состояние устройства — **Работает**.</span><span class="sxs-lookup"><span data-stu-id="0f2c6-149">The status of your device is now **Running**.</span></span> <span data-ttu-id="0f2c6-150">Решение для удаленного мониторинга теперь может получать данные телеметрии с устройства и вызывать методы на устройстве.</span><span class="sxs-lookup"><span data-stu-id="0f2c6-150">The remote monitoring solution can now receive telemetry from your device and invoke methods on the device.</span></span>

[img-dashboard]: ./media/iot-suite-connecting-devices-mbed/dashboard.png
[1]: ./media/iot-suite-connecting-devices-mbed/suite0.png
[2]: ./media/iot-suite-connecting-devices-mbed/suite1.png
[3]: ./media/iot-suite-connecting-devices-mbed/suite2.png
[4]: ./media/iot-suite-connecting-devices-mbed/suite3.png

[lnk-what-are-preconfig-solutions]: iot-suite-what-are-preconfigured-solutions.md
[lnk-remote-monitoring]: iot-suite-remote-monitoring-sample-walkthrough.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/

## <a name="build-and-run-the-c-sample-solution"></a><span data-ttu-id="0f2c6-151">Выполнение сборки и запуск примера решения на C</span><span class="sxs-lookup"><span data-stu-id="0f2c6-151">Build and run the C sample solution</span></span>

<span data-ttu-id="0f2c6-152">Ниже перечислены инструкции по подключению устройства [Freescale FRDM-K64F с поддержкой mbed][lnk-mbed-home] к решению для удаленного мониторинга.</span><span class="sxs-lookup"><span data-stu-id="0f2c6-152">The following instructions describe the steps for connecting an [mbed-enabled Freescale FRDM-K64F][lnk-mbed-home] device to the remote monitoring solution.</span></span>

### <a name="connect-the-mbed-device-to-your-network-and-desktop-machine"></a><span data-ttu-id="0f2c6-153">Подключение устройства mbed к сети и настольному компьютеру</span><span class="sxs-lookup"><span data-stu-id="0f2c6-153">Connect the mbed device to your network and desktop machine</span></span>

1. <span data-ttu-id="0f2c6-154">Подключите устройство mbed к сети, используя кабель Ethernet.</span><span class="sxs-lookup"><span data-stu-id="0f2c6-154">Connect the mbed device to your network using an Ethernet cable.</span></span> <span data-ttu-id="0f2c6-155">Это необходимо, так как примеру приложения требуется доступ к Интернету.</span><span class="sxs-lookup"><span data-stu-id="0f2c6-155">This step is necessary because the sample application requires internet access.</span></span>

1. <span data-ttu-id="0f2c6-156">Чтобы подключить устройство mbed к настольному компьютеру, см. статью о [начале работы с mbed][lnk-mbed-getstarted].</span><span class="sxs-lookup"><span data-stu-id="0f2c6-156">See [Getting Started with mbed][lnk-mbed-getstarted] to connect your mbed device to your desktop PC.</span></span>

1. <span data-ttu-id="0f2c6-157">Если настольный компьютер работает под управлением Windows, см. раздел о [настройке компьютера][lnk-mbed-pcconnect] для настройки доступа к устройству mbed через последовательный порт.</span><span class="sxs-lookup"><span data-stu-id="0f2c6-157">If your desktop PC is running Windows, see [PC Configuration][lnk-mbed-pcconnect] to configure serial port access to your mbed device.</span></span>

### <a name="create-an-mbed-project-and-import-the-sample-code"></a><span data-ttu-id="0f2c6-158">Создание проекта mbed и импорт примера кода</span><span class="sxs-lookup"><span data-stu-id="0f2c6-158">Create an mbed project and import the sample code</span></span>

<span data-ttu-id="0f2c6-159">Выполните следующие действия, чтобы добавить пример кода в проект mbed.</span><span class="sxs-lookup"><span data-stu-id="0f2c6-159">Follow these steps to add some sample code to an mbed project.</span></span> <span data-ttu-id="0f2c6-160">Мы импортируем начальный проект для удаленного мониторинга, а затем изменим проект для использования протокола MQTT вместо протокола AMQP.</span><span class="sxs-lookup"><span data-stu-id="0f2c6-160">You import the remote monitoring starter project and then change the project to use the MQTT protocol instead of the AMQP protocol.</span></span> <span data-ttu-id="0f2c6-161">В настоящее время необходимо, чтобы протокол MQTT использовал функции управления устройствами Центра Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="0f2c6-161">Currently, you need to use the MQTT protocol to use the device management features of IoT Hub.</span></span>

1. <span data-ttu-id="0f2c6-162">Откройте в веб-браузере [сайт для разработчиков](https://developer.mbed.org/)на портале mbed.org.</span><span class="sxs-lookup"><span data-stu-id="0f2c6-162">In your web browser, go to the mbed.org [developer site](https://developer.mbed.org/).</span></span> <span data-ttu-id="0f2c6-163">Если у вас еще нет учетной записи, зарегистрируйтесь (бесплатно).</span><span class="sxs-lookup"><span data-stu-id="0f2c6-163">If you haven't signed up, you see an option to create an account (it's free).</span></span> <span data-ttu-id="0f2c6-164">Если учетная запись есть, используйте ее для входа.</span><span class="sxs-lookup"><span data-stu-id="0f2c6-164">Otherwise, log in with your account credentials.</span></span> <span data-ttu-id="0f2c6-165">Щелкните **Compiler** (Компилятор) в правом верхнем углу страницы.</span><span class="sxs-lookup"><span data-stu-id="0f2c6-165">Then click **Compiler** in the upper right-hand corner of the page.</span></span> <span data-ttu-id="0f2c6-166">Отобразится интерфейс *Workspace* (Рабочая область).</span><span class="sxs-lookup"><span data-stu-id="0f2c6-166">This action brings you to the *Workspace* interface.</span></span>

1. <span data-ttu-id="0f2c6-167">Убедитесь, что в правом верхнем углу окна отображается аппаратная платформа, которую вы используете. В противном случае щелкните значок и выберите другую платформу.</span><span class="sxs-lookup"><span data-stu-id="0f2c6-167">Make sure the hardware platform you're using appears in the upper right-hand corner of the window, or click the icon in the right-hand corner to select your hardware platform.</span></span>

1. <span data-ttu-id="0f2c6-168">Щелкните **Импорт** в главном меню.</span><span class="sxs-lookup"><span data-stu-id="0f2c6-168">Click **Import** on the main menu.</span></span> <span data-ttu-id="0f2c6-169">Щелкните ссылку **Click here to import from URL** (Щелкните здесь, чтобы импортировать с URL-адреса).</span><span class="sxs-lookup"><span data-stu-id="0f2c6-169">Then click **Click here to import from URL**.</span></span>
   
    ![Запуск импорта в рабочую область mbed][6]

1. <span data-ttu-id="0f2c6-171">Во всплывающем окне введите ссылку на пример кода https://developer.mbed.org/users/AzureIoTClient/code/remote_monitoring/, а затем нажмите кнопку **Import** (Импорт).</span><span class="sxs-lookup"><span data-stu-id="0f2c6-171">In the pop-up window, enter the link for the sample code https://developer.mbed.org/users/AzureIoTClient/code/remote_monitoring/ then click **Import**.</span></span>
   
    ![Импорт примера кода в рабочую область mbed][7]

1. <span data-ttu-id="0f2c6-173">В окне компилятора mbed вы увидите, что при импорте проекта также импортируются различные библиотеки.</span><span class="sxs-lookup"><span data-stu-id="0f2c6-173">You can see in the mbed compiler window that importing this project also imports various libraries.</span></span> <span data-ttu-id="0f2c6-174">Некоторые из них предоставляются и обслуживаются командой разработчиков Центра Интернета вещей Azure ([azureiot_common](https://developer.mbed.org/users/AzureIoTClient/code/azureiot_common/), [iothub_client](https://developer.mbed.org/users/AzureIoTClient/code/iothub_client/), [iothub_amqp_transport](https://developer.mbed.org/users/AzureIoTClient/code/iothub_amqp_transport/), [azure_uamqp](https://developer.mbed.org/users/AzureIoTClient/code/azure_uamqp/)), остальные являются библиотеками сторонних производителей, доступными в каталоге библиотек mbed.</span><span class="sxs-lookup"><span data-stu-id="0f2c6-174">Some are provided and maintained by the Azure IoT team ([azureiot_common](https://developer.mbed.org/users/AzureIoTClient/code/azureiot_common/), [iothub_client](https://developer.mbed.org/users/AzureIoTClient/code/iothub_client/), [iothub_amqp_transport](https://developer.mbed.org/users/AzureIoTClient/code/iothub_amqp_transport/), [azure_uamqp](https://developer.mbed.org/users/AzureIoTClient/code/azure_uamqp/)), while others are third-party libraries available in the mbed libraries catalog.</span></span>
   
    ![Просмотр проекта mbed][8]

1. <span data-ttu-id="0f2c6-176">В **рабочей области программы** щелкните правой кнопкой мыши библиотеку **iothub\_amqp\_transport**, выберите **Delete** (Удалить) и нажмите кнопку **ОК** для подтверждения.</span><span class="sxs-lookup"><span data-stu-id="0f2c6-176">In the **Program Workspace**, right-click the **iothub\_amqp\_transport** library, click **Delete**, and then click **OK** to confirm.</span></span>

1. <span data-ttu-id="0f2c6-177">В **рабочей области программы** щелкните правой кнопкой мыши библиотеку **azure\_amqp\_c**, выберите **Delete** (Удалить) и нажмите кнопку **ОК** для подтверждения.</span><span class="sxs-lookup"><span data-stu-id="0f2c6-177">In the **Program Workspace**, right-click the **azure\_amqp\_c** library, click **Delete**, and then click **OK** to confirm.</span></span>

1. <span data-ttu-id="0f2c6-178">В **рабочей области программы** щелкните правой кнопкой мыши проект **remote_monitoring**, выберите **Import Library** (Импортировать библиотеку), а затем — **From URL** (С URL-адреса).</span><span class="sxs-lookup"><span data-stu-id="0f2c6-178">Right-click the **remote_monitoring** project in the **Program Workspace**, select **Import Library**, then select **From URL**.</span></span>
   
    ![Запуск импорта библиотеки в рабочую область mbed][6]

1. <span data-ttu-id="0f2c6-180">Во всплывающем окне введите ссылку на библиотеку транспорта MQTT https://developer.mbed.org/users/AzureIoTClient/code/iothub\_mqtt\_transport/, а затем нажмите кнопку **Import** (Импорт).</span><span class="sxs-lookup"><span data-stu-id="0f2c6-180">In the pop-up window, enter the link for the MQTT transport library https://developer.mbed.org/users/AzureIoTClient/code/iothub\_mqtt\_transport/ then click **Import**.</span></span>
   
    ![Импорт библиотеки в рабочую область mbed][12]

1. <span data-ttu-id="0f2c6-182">Повторите предыдущий шаг, чтобы добавить библиотеку MQTT с URL-адреса https://developer.mbed.org/users/AzureIoTClient/code/azure\_umqtt\_c/.</span><span class="sxs-lookup"><span data-stu-id="0f2c6-182">Repeat the previous step to add the MQTT library from https://developer.mbed.org/users/AzureIoTClient/code/azure\_umqtt\_c/.</span></span>

1. <span data-ttu-id="0f2c6-183">Теперь рабочая область выглядит так:</span><span class="sxs-lookup"><span data-stu-id="0f2c6-183">Your workspace now looks like the following:</span></span>

    ![Просмотр рабочей области mbed][13]

1. <span data-ttu-id="0f2c6-185">Откройте файл remote\_monitoring\remote_monitoring.c и замените имеющиеся инструкции `#include` следующим кодом:</span><span class="sxs-lookup"><span data-stu-id="0f2c6-185">Open the remote\_monitoring\remote_monitoring.c file and replace the existing `#include` statements with the following code:</span></span>

    ```c
    #include "iothubtransportmqtt.h"
    #include "schemalib.h"
    #include "iothub_client.h"
    #include "serializer_devicetwin.h"
    #include "schemaserializer.h"
    #include "azure_c_shared_utility/threadapi.h"
    #include "azure_c_shared_utility/platform.h"
    #include "parson.h"

    #ifdef MBED_BUILD_TIMESTAMP
    #include "certs.h"
    #endif // MBED_BUILD_TIMESTAMP
    ```
1. <span data-ttu-id="0f2c6-186">Удалить весь остальной код из файла remote\_monitoring\remote\_monitoring.c.</span><span class="sxs-lookup"><span data-stu-id="0f2c6-186">Delete all the remaining code in the remote\_monitoring\remote\_monitoring.c file.</span></span>

[!INCLUDE [iot-suite-connecting-code](../../includes/iot-suite-connecting-code.md)]

## <a name="build-and-run-the-sample"></a><span data-ttu-id="0f2c6-187">Сборка и запуск примера</span><span class="sxs-lookup"><span data-stu-id="0f2c6-187">Build and run the sample</span></span>

<span data-ttu-id="0f2c6-188">Добавьте код для вызова функции **remote\_monitoring\_run**, а затем создайте и запустите приложение устройства.</span><span class="sxs-lookup"><span data-stu-id="0f2c6-188">Add code to invoke the **remote\_monitoring\_run** function and then build and run the device application.</span></span>

1. <span data-ttu-id="0f2c6-189">Добавьте функцию **main**, вставив следующий код в конце файла remote\_monitoring.c для вызова функции **remote\_monitoring\_run**:</span><span class="sxs-lookup"><span data-stu-id="0f2c6-189">Add a **main** function with following code at the end of the remote\_monitoring.c file to invoke the **remote\_monitoring\_run** function:</span></span>
   
    ```c
    int main()
    {
      remote_monitoring_run();
      return 0;
    }
    ```

1. <span data-ttu-id="0f2c6-190">Щелкните **Скомпилировать**, чтобы собрать программу.</span><span class="sxs-lookup"><span data-stu-id="0f2c6-190">Click **Compile** to build the program.</span></span> <span data-ttu-id="0f2c6-191">Вы можете проигнорировать все предупреждения. Однако если при сборке возникают ошибки, исправьте их, прежде чем продолжить.</span><span class="sxs-lookup"><span data-stu-id="0f2c6-191">You can safely ignore any warnings, but if the build generates errors, fix them before proceeding.</span></span>

1. <span data-ttu-id="0f2c6-192">Если сборка выполнена успешно, то на веб-сайте компилятора mbed создается BIN-файл с именем вашего проекта и загружается на локальный компьютер.</span><span class="sxs-lookup"><span data-stu-id="0f2c6-192">If the build is successful, the mbed compiler website generates a .bin file with the name of your project and downloads it to your local machine.</span></span> <span data-ttu-id="0f2c6-193">Скопируйте BIN-файл на устройство.</span><span class="sxs-lookup"><span data-stu-id="0f2c6-193">Copy the .bin file to the device.</span></span> <span data-ttu-id="0f2c6-194">При сохранении BIN-файла на устройство происходит перезапуск устройства и запуск программы, содержащейся в BIN-файле.</span><span class="sxs-lookup"><span data-stu-id="0f2c6-194">Saving the .bin file to the device causes the device to restart and run the program contained in the .bin file.</span></span> <span data-ttu-id="0f2c6-195">Программу можно вручную перезапустить в любое время, нажав кнопку сброса на устройстве mbed.</span><span class="sxs-lookup"><span data-stu-id="0f2c6-195">You can manually restart the program at any time by pressing the reset button on the mbed device.</span></span>

1. <span data-ttu-id="0f2c6-196">Подключитесь к устройству с помощью клиентского SSH-приложения, такого как PuTTY.</span><span class="sxs-lookup"><span data-stu-id="0f2c6-196">Connect to the device using an SSH client application, such as PuTTY.</span></span> <span data-ttu-id="0f2c6-197">Вы можете посмотреть, какой последовательный порт использует устройство, в диспетчере устройств Windows.</span><span class="sxs-lookup"><span data-stu-id="0f2c6-197">You can determine the serial port your device uses by checking Windows Device Manager.</span></span>
   
    ![][11]

1. <span data-ttu-id="0f2c6-198">В PuTTY выберите тип подключения **Serial** (Последовательный).</span><span class="sxs-lookup"><span data-stu-id="0f2c6-198">In PuTTY, click the **Serial** connection type.</span></span> <span data-ttu-id="0f2c6-199">Устройство обычно подключается со скоростью 9600 бод, поэтому введите 9600 в поле **Speed** (Скорость).</span><span class="sxs-lookup"><span data-stu-id="0f2c6-199">The device typically connects at 9600 baud, so enter 9600 in the **Speed** box.</span></span> <span data-ttu-id="0f2c6-200">Затем щелкните **Открыть**.</span><span class="sxs-lookup"><span data-stu-id="0f2c6-200">Then click **Open**.</span></span>

1. <span data-ttu-id="0f2c6-201">Начнется выполнение программы.</span><span class="sxs-lookup"><span data-stu-id="0f2c6-201">The program starts executing.</span></span> <span data-ttu-id="0f2c6-202">Если программа не запускается автоматически при подключении, возможно, нужно перезагрузить плату (для этого нажмите клавиши Ctrl+Break или кнопку сброса на плате).</span><span class="sxs-lookup"><span data-stu-id="0f2c6-202">You may have to reset the board (press CTRL+Break or press the board's reset button) if the program does not start automatically when you connect.</span></span>
   
    ![][10]

[!INCLUDE [iot-suite-visualize-connecting](../../includes/iot-suite-visualize-connecting.md)]

[6]: ./media/iot-suite-connecting-devices-mbed/mbed1.png
[7]: ./media/iot-suite-connecting-devices-mbed/mbed2a.png
[8]: ./media/iot-suite-connecting-devices-mbed/mbed3a.png
[10]: ./media/iot-suite-connecting-devices-mbed/putty.png
[11]: ./media/iot-suite-connecting-devices-mbed/mbed6.png
[12]: ./media/iot-suite-connecting-devices-mbed/mbed7.png
[13]: ./media/iot-suite-connecting-devices-mbed/mbed8.png

[lnk-mbed-home]: https://developer.mbed.org/platforms/FRDM-K64F/
[lnk-mbed-getstarted]: https://developer.mbed.org/platforms/FRDM-K64F/#getting-started-with-mbed
[lnk-mbed-pcconnect]: https://developer.mbed.org/platforms/FRDM-K64F/#pc-configuration
