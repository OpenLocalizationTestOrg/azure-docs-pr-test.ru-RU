---
title: "aaaConnect устройство с помощью C на mbed | Документы Microsoft"
description: "Описывает, как tooconnect toohello устройства Azure IoT Suite предварительно настроенных удаленных с помощью приложения, написанные на языке C при выполнении на устройстве mbed решение для мониторинга."
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
ms.openlocfilehash: dcd1e74635e8dec678a59bff060a73f7cfabd124
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="connect-your-device-toohello-remote-monitoring-preconfigured-solution-mbed"></a><span data-ttu-id="30f91-103">Подключения на устройстве toohello удаленное наблюдение предварительно настроенных решений (mbed)</span><span class="sxs-lookup"><span data-stu-id="30f91-103">Connect your device toohello remote monitoring preconfigured solution (mbed)</span></span>

## <a name="scenario-overview"></a><span data-ttu-id="30f91-104">Обзор сценария</span><span class="sxs-lookup"><span data-stu-id="30f91-104">Scenario overview</span></span>
<span data-ttu-id="30f91-105">В этом случае создайте устройство, которое отправляет hello следующие удаленный мониторинг телеметрии toohello [предварительно настроенное решение][lnk-what-are-preconfig-solutions]:</span><span class="sxs-lookup"><span data-stu-id="30f91-105">In this scenario, you create a device that sends hello following telemetry toohello remote monitoring [preconfigured solution][lnk-what-are-preconfig-solutions]:</span></span>

* <span data-ttu-id="30f91-106">наружная температура;</span><span class="sxs-lookup"><span data-stu-id="30f91-106">External temperature</span></span>
* <span data-ttu-id="30f91-107">внутренняя температура;</span><span class="sxs-lookup"><span data-stu-id="30f91-107">Internal temperature</span></span>
* <span data-ttu-id="30f91-108">влажность.</span><span class="sxs-lookup"><span data-stu-id="30f91-108">Humidity</span></span>

<span data-ttu-id="30f91-109">Для простоты кода hello на устройстве hello приводит к возникновению ошибки образцы значений, но мы рекомендуем вам tooextend hello образец подключение устройства tooyour реальные датчиков и отправки реальные данные телеметрии.</span><span class="sxs-lookup"><span data-stu-id="30f91-109">For simplicity, hello code on hello device generates sample values, but we encourage you tooextend hello sample by connecting real sensors tooyour device and sending real telemetry.</span></span>

<span data-ttu-id="30f91-110">Hello устройство будет также может toorespond toomethods из панели мониторинга решения hello и требуемого значения свойств, заданные в панели мониторинга hello решения.</span><span class="sxs-lookup"><span data-stu-id="30f91-110">hello device is also able toorespond toomethods invoked from hello solution dashboard and desired property values set in hello solution dashboard.</span></span>

<span data-ttu-id="30f91-111">toocomplete этого учебника требуется активная учетная запись Azure.</span><span class="sxs-lookup"><span data-stu-id="30f91-111">toocomplete this tutorial, you need an active Azure account.</span></span> <span data-ttu-id="30f91-112">Если ее нет, можно создать бесплатную пробную учетную запись всего за несколько минут.</span><span class="sxs-lookup"><span data-stu-id="30f91-112">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="30f91-113">Дополнительные сведения см. в статье о [бесплатной пробной версии Azure][lnk-free-trial].</span><span class="sxs-lookup"><span data-stu-id="30f91-113">For details, see [Azure Free Trial][lnk-free-trial].</span></span>

## <a name="before-you-start"></a><span data-ttu-id="30f91-114">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="30f91-114">Before you start</span></span>
<span data-ttu-id="30f91-115">До написания кода для устройства необходимо подготовить свое предварительно настроенное решение для удаленного мониторинга, а затем подготовить в нем новое пользовательское устройство.</span><span class="sxs-lookup"><span data-stu-id="30f91-115">Before you write any code for your device, you must provision your remote monitoring preconfigured solution and provision a new custom device in that solution.</span></span>

### <a name="provision-your-remote-monitoring-preconfigured-solution"></a><span data-ttu-id="30f91-116">Подготовка предварительно настроенного решения для удаленного мониторинга</span><span class="sxs-lookup"><span data-stu-id="30f91-116">Provision your remote monitoring preconfigured solution</span></span>
<span data-ttu-id="30f91-117">устройство Hello, создан в этом учебнике отправляет экземпляра tooan данных hello [удаленный мониторинг] [ lnk-remote-monitoring] предварительно настроенных решений.</span><span class="sxs-lookup"><span data-stu-id="30f91-117">hello device you create in this tutorial sends data tooan instance of hello [remote monitoring][lnk-remote-monitoring] preconfigured solution.</span></span> <span data-ttu-id="30f91-118">Если это еще не было предоставлено hello удаленное наблюдение предварительно настроенных решений в вашей учетной записью Azure, используйте hello следующие шаги:</span><span class="sxs-lookup"><span data-stu-id="30f91-118">If you haven't already provisioned hello remote monitoring preconfigured solution in your Azure account, use hello following steps:</span></span>

1. <span data-ttu-id="30f91-119">На hello <https://www.azureiotsuite.com/> щелкните  **+**  toocreate решения.</span><span class="sxs-lookup"><span data-stu-id="30f91-119">On hello <https://www.azureiotsuite.com/> page, click **+** toocreate a solution.</span></span>
2. <span data-ttu-id="30f91-120">Нажмите кнопку **выберите** на hello **удаленный мониторинг** панели toocreate решения.</span><span class="sxs-lookup"><span data-stu-id="30f91-120">Click **Select** on hello **Remote monitoring** panel toocreate your solution.</span></span>
3. <span data-ttu-id="30f91-121">На hello **создания удаленного решением для мониторинга** введите **имя решения** по своему усмотрению выберите hello **область** toodeploy для и выберите hello Azure toouse toowant подписки.</span><span class="sxs-lookup"><span data-stu-id="30f91-121">On hello **Create Remote monitoring solution** page, enter a **Solution name** of your choice, select hello **Region** you want toodeploy to, and select hello Azure subscription toowant toouse.</span></span> <span data-ttu-id="30f91-122">Затем щелкните **Создать решение**.</span><span class="sxs-lookup"><span data-stu-id="30f91-122">Then click **Create solution**.</span></span>
4. <span data-ttu-id="30f91-123">Дождитесь завершения процесса подготовки hello.</span><span class="sxs-lookup"><span data-stu-id="30f91-123">Wait until hello provisioning process completes.</span></span>

> [!WARNING]
> <span data-ttu-id="30f91-124">предварительно настроенное Hello решения используют оплаты служб Azure.</span><span class="sxs-lookup"><span data-stu-id="30f91-124">hello preconfigured solutions use billable Azure services.</span></span> <span data-ttu-id="30f91-125">Убедитесь, что tooremove hello предварительно настроенных решений из подписки, когда вы завершили работу с ним tooavoid все ненужные расходы.</span><span class="sxs-lookup"><span data-stu-id="30f91-125">Be sure tooremove hello preconfigured solution from your subscription when you are done with it tooavoid any unnecessary charges.</span></span> <span data-ttu-id="30f91-126">Можно полностью удалить предварительно настроенных решений из подписки, перейдя по адресу hello <https://www.azureiotsuite.com/> страницы.</span><span class="sxs-lookup"><span data-stu-id="30f91-126">You can completely remove a preconfigured solution from your subscription by visiting hello <https://www.azureiotsuite.com/> page.</span></span>
> 
> 

<span data-ttu-id="30f91-127">После завершения процесса для hello удаленного решением для мониторинга инициализации hello, нажмите кнопку **запуска** tooopen hello решения и панели мониторинга в браузере.</span><span class="sxs-lookup"><span data-stu-id="30f91-127">When hello provisioning process for hello remote monitoring solution finishes, click **Launch** tooopen hello solution dashboard in your browser.</span></span>

![Панель мониторинга решения][img-dashboard]

### <a name="provision-your-device-in-hello-remote-monitoring-solution"></a><span data-ttu-id="30f91-129">Подготовка устройства в hello удаленного решением для мониторинга</span><span class="sxs-lookup"><span data-stu-id="30f91-129">Provision your device in hello remote monitoring solution</span></span>
> [!NOTE]
> <span data-ttu-id="30f91-130">Если вы уже подготовили устройство в решении, пропустите этот шаг.</span><span class="sxs-lookup"><span data-stu-id="30f91-130">If you have already provisioned a device in your solution, you can skip this step.</span></span> <span data-ttu-id="30f91-131">Необходимы учетные данные устройства hello tooknow, при создании клиентского приложения hello.</span><span class="sxs-lookup"><span data-stu-id="30f91-131">You need tooknow hello device credentials when you create hello client application.</span></span>
> 
> 

<span data-ttu-id="30f91-132">Для решения tooconnect toohello предварительно настроенных устройств, он должен идентифицировать себя tooIoT концентратора используя действительные учетные данные.</span><span class="sxs-lookup"><span data-stu-id="30f91-132">For a device tooconnect toohello preconfigured solution, it must identify itself tooIoT Hub using valid credentials.</span></span> <span data-ttu-id="30f91-133">Учетные данные устройства hello можно извлечь из панели мониторинга hello решения.</span><span class="sxs-lookup"><span data-stu-id="30f91-133">You can retrieve hello device credentials from hello solution dashboard.</span></span> <span data-ttu-id="30f91-134">Включать учетные данные устройства hello в клиентском приложении, далее в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="30f91-134">You include hello device credentials in your client application later in this tutorial.</span></span>

<span data-ttu-id="30f91-135">tooadd tooyour удаленного мониторинга устройствами завершения hello следующие шаги на панели мониторинга hello решения:</span><span class="sxs-lookup"><span data-stu-id="30f91-135">tooadd a device tooyour remote monitoring solution, complete hello following steps in hello solution dashboard:</span></span>

1. <span data-ttu-id="30f91-136">В hello левом нижнем углу панели мониторинга hello, щелкните **добавить устройство**.</span><span class="sxs-lookup"><span data-stu-id="30f91-136">In hello lower left-hand corner of hello dashboard, click **Add a device**.</span></span>
   
   ![Добавление устройства][1]
2. <span data-ttu-id="30f91-138">В hello **пользовательских устройств** нажмите кнопку **добавить новую**.</span><span class="sxs-lookup"><span data-stu-id="30f91-138">In hello **Custom Device** panel, click **Add new**.</span></span>
   
   ![Добавление пользовательского устройства][2]
3. <span data-ttu-id="30f91-140">Установите переключатель **Позвольте мне определить собственный идентификатор устройства**.</span><span class="sxs-lookup"><span data-stu-id="30f91-140">Choose **Let me define my own Device ID**.</span></span> <span data-ttu-id="30f91-141">Введите идентификатор устройства, например **mydevice**, нажмите кнопку **проверить идентификатор** tooverify таким именем еще не используется и нажмите кнопку **создать** tooprovision hello устройства.</span><span class="sxs-lookup"><span data-stu-id="30f91-141">Enter a Device ID such as **mydevice**, click **Check ID** tooverify that name isn't already in use, and then click **Create** tooprovision hello device.</span></span>
   
   ![Добавление идентификатора устройства][3]
4. <span data-ttu-id="30f91-143">Перевести устройство hello Примечание учетные данные (идентификатор устройства, имя узла концентратора IoT и ключ устройства).</span><span class="sxs-lookup"><span data-stu-id="30f91-143">Make a note hello device credentials (Device ID, IoT Hub Hostname, and Device Key).</span></span> <span data-ttu-id="30f91-144">Клиент приложению эти значения tooconnect toohello удаленного решением для мониторинга.</span><span class="sxs-lookup"><span data-stu-id="30f91-144">Your client application needs these values tooconnect toohello remote monitoring solution.</span></span> <span data-ttu-id="30f91-145">Затем нажмите кнопку **Done**(Готово).</span><span class="sxs-lookup"><span data-stu-id="30f91-145">Then click **Done**.</span></span>
   
    ![Просмотр учетных данных устройства][4]
5. <span data-ttu-id="30f91-147">Выберите устройство в списке устройств hello в панель мониторинга hello решения.</span><span class="sxs-lookup"><span data-stu-id="30f91-147">Select your device in hello device list in hello solution dashboard.</span></span> <span data-ttu-id="30f91-148">Затем в hello **сведений об устройстве** нажмите кнопку **включить устройство**.</span><span class="sxs-lookup"><span data-stu-id="30f91-148">Then, in hello **Device Details** panel, click **Enable Device**.</span></span> <span data-ttu-id="30f91-149">Теперь задано состояние Hello устройства **под управлением**.</span><span class="sxs-lookup"><span data-stu-id="30f91-149">hello status of your device is now **Running**.</span></span> <span data-ttu-id="30f91-150">решение для удаленного мониторинга Hello теперь можно получать данные телеметрии с устройства и вызова методов на устройстве hello.</span><span class="sxs-lookup"><span data-stu-id="30f91-150">hello remote monitoring solution can now receive telemetry from your device and invoke methods on hello device.</span></span>

[img-dashboard]: ./media/iot-suite-connecting-devices-mbed/dashboard.png
[1]: ./media/iot-suite-connecting-devices-mbed/suite0.png
[2]: ./media/iot-suite-connecting-devices-mbed/suite1.png
[3]: ./media/iot-suite-connecting-devices-mbed/suite2.png
[4]: ./media/iot-suite-connecting-devices-mbed/suite3.png

[lnk-what-are-preconfig-solutions]: iot-suite-what-are-preconfigured-solutions.md
[lnk-remote-monitoring]: iot-suite-remote-monitoring-sample-walkthrough.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/

## <a name="build-and-run-hello-c-sample-solution"></a><span data-ttu-id="30f91-151">Постройте и запустите решение образца hello C</span><span class="sxs-lookup"><span data-stu-id="30f91-151">Build and run hello C sample solution</span></span>

<span data-ttu-id="30f91-152">Hello следующие инструкции описывают hello инструкции по подключению [поддержкой mbed Freescale FRDM-K64F] [ lnk-mbed-home] toohello устройства удаленного решением для мониторинга.</span><span class="sxs-lookup"><span data-stu-id="30f91-152">hello following instructions describe hello steps for connecting an [mbed-enabled Freescale FRDM-K64F][lnk-mbed-home] device toohello remote monitoring solution.</span></span>

### <a name="connect-hello-mbed-device-tooyour-network-and-desktop-machine"></a><span data-ttu-id="30f91-153">Подключение сети tooyour устройств mbed hello и настольном компьютере</span><span class="sxs-lookup"><span data-stu-id="30f91-153">Connect hello mbed device tooyour network and desktop machine</span></span>

1. <span data-ttu-id="30f91-154">Подключите hello mbed устройства tooyour сети с помощью кабеля Ethernet.</span><span class="sxs-lookup"><span data-stu-id="30f91-154">Connect hello mbed device tooyour network using an Ethernet cable.</span></span> <span data-ttu-id="30f91-155">Этот шаг необходим, так как пример приложения hello требуется доступ к Интернету.</span><span class="sxs-lookup"><span data-stu-id="30f91-155">This step is necessary because hello sample application requires internet access.</span></span>

1. <span data-ttu-id="30f91-156">В разделе [Приступая к работе с mbed] [ lnk-mbed-getstarted] tooconnect рабочего стола tooyour устройства mbed ПК.</span><span class="sxs-lookup"><span data-stu-id="30f91-156">See [Getting Started with mbed][lnk-mbed-getstarted] tooconnect your mbed device tooyour desktop PC.</span></span>

1. <span data-ttu-id="30f91-157">Если для настольного компьютера работает под управлением Windows, см. раздел [конфигурации ПК] [ lnk-mbed-pcconnect] tooconfigure последовательного порта tooyour mbed доступа.</span><span class="sxs-lookup"><span data-stu-id="30f91-157">If your desktop PC is running Windows, see [PC Configuration][lnk-mbed-pcconnect] tooconfigure serial port access tooyour mbed device.</span></span>

### <a name="create-an-mbed-project-and-import-hello-sample-code"></a><span data-ttu-id="30f91-158">Создайте проект mbed и импортировать hello образец кода</span><span class="sxs-lookup"><span data-stu-id="30f91-158">Create an mbed project and import hello sample code</span></span>

<span data-ttu-id="30f91-159">Выполните эти шаги tooadd некоторые tooan mbed образец кода проекта.</span><span class="sxs-lookup"><span data-stu-id="30f91-159">Follow these steps tooadd some sample code tooan mbed project.</span></span> <span data-ttu-id="30f91-160">Импорт hello удаленного мониторинга начальный проект и измените hello проекта toouse hello протокола MQTT вместо hello протокола AMQP.</span><span class="sxs-lookup"><span data-stu-id="30f91-160">You import hello remote monitoring starter project and then change hello project toouse hello MQTT protocol instead of hello AMQP protocol.</span></span> <span data-ttu-id="30f91-161">В настоящее время необходимо toouse hello MQTT протокола toouse hello функции управления устройствами центра IoT.</span><span class="sxs-lookup"><span data-stu-id="30f91-161">Currently, you need toouse hello MQTT protocol toouse hello device management features of IoT Hub.</span></span>

1. <span data-ttu-id="30f91-162">В веб-браузере перейдите toohello mbed.org [сайта разработчика](https://developer.mbed.org/).</span><span class="sxs-lookup"><span data-stu-id="30f91-162">In your web browser, go toohello mbed.org [developer site](https://developer.mbed.org/).</span></span> <span data-ttu-id="30f91-163">Если вы еще не зарегистрировались, можно увидеть toocreate параметр учетной записи (бесплатно).</span><span class="sxs-lookup"><span data-stu-id="30f91-163">If you haven't signed up, you see an option toocreate an account (it's free).</span></span> <span data-ttu-id="30f91-164">Если учетная запись есть, используйте ее для входа.</span><span class="sxs-lookup"><span data-stu-id="30f91-164">Otherwise, log in with your account credentials.</span></span> <span data-ttu-id="30f91-165">Нажмите кнопку **компилятора** в верхнем правом углу hello страницы приветствия.</span><span class="sxs-lookup"><span data-stu-id="30f91-165">Then click **Compiler** in hello upper right-hand corner of hello page.</span></span> <span data-ttu-id="30f91-166">Это действие переводит toohello *рабочей* интерфейса.</span><span class="sxs-lookup"><span data-stu-id="30f91-166">This action brings you toohello *Workspace* interface.</span></span>

1. <span data-ttu-id="30f91-167">Убедитесь, что аппаратную платформу hello, которую вы используете отображается в верхнем правом углу hello окна hello, или щелкните значок hello в правом углу tooselect hello Аппаратная платформа.</span><span class="sxs-lookup"><span data-stu-id="30f91-167">Make sure hello hardware platform you're using appears in hello upper right-hand corner of hello window, or click hello icon in hello right-hand corner tooselect your hardware platform.</span></span>

1. <span data-ttu-id="30f91-168">Нажмите кнопку **импорта** главного меню hello.</span><span class="sxs-lookup"><span data-stu-id="30f91-168">Click **Import** on hello main menu.</span></span> <span data-ttu-id="30f91-169">Нажмите кнопку **tooimport с URL-адреса щелкните здесь**.</span><span class="sxs-lookup"><span data-stu-id="30f91-169">Then click **Click here tooimport from URL**.</span></span>
   
    ![Запустить рабочую область toombed импорта][6]

1. <span data-ttu-id="30f91-171">Во всплывающем окне приветствия, введите ссылку hello https://developer.mbed.org/users/AzureIoTClient/code/remote_monitoring/ кода образца hello, а затем нажмите кнопку **импорта**.</span><span class="sxs-lookup"><span data-stu-id="30f91-171">In hello pop-up window, enter hello link for hello sample code https://developer.mbed.org/users/AzureIoTClient/code/remote_monitoring/ then click **Import**.</span></span>
   
    ![Импорт рабочей toombed образец кода][7]

1. <span data-ttu-id="30f91-173">В окно компилятора mbed hello можно увидеть, что импорт этого проекта также импортирует различные библиотеки.</span><span class="sxs-lookup"><span data-stu-id="30f91-173">You can see in hello mbed compiler window that importing this project also imports various libraries.</span></span> <span data-ttu-id="30f91-174">Некоторые предоставляются и обслуживается hello Azure IoT team ([azureiot_common](https://developer.mbed.org/users/AzureIoTClient/code/azureiot_common/), [iothub_client](https://developer.mbed.org/users/AzureIoTClient/code/iothub_client/), [iothub_amqp_transport](https://developer.mbed.org/users/AzureIoTClient/code/iothub_amqp_transport/), [azure_uamqp](https://developer.mbed.org/users/AzureIoTClient/code/azure_uamqp/)), а другие представляют собой сторонних библиотек, доступных в каталоге библиотеки mbed hello.</span><span class="sxs-lookup"><span data-stu-id="30f91-174">Some are provided and maintained by hello Azure IoT team ([azureiot_common](https://developer.mbed.org/users/AzureIoTClient/code/azureiot_common/), [iothub_client](https://developer.mbed.org/users/AzureIoTClient/code/iothub_client/), [iothub_amqp_transport](https://developer.mbed.org/users/AzureIoTClient/code/iothub_amqp_transport/), [azure_uamqp](https://developer.mbed.org/users/AzureIoTClient/code/azure_uamqp/)), while others are third-party libraries available in hello mbed libraries catalog.</span></span>
   
    ![Просмотр проекта mbed][8]

1. <span data-ttu-id="30f91-176">В hello **рабочей программы**, щелкните правой кнопкой мыши hello **центром IOT\_amqp\_транспорта** библиотеки, нажмите кнопку **удалить**и нажмите кнопку **ОК** tooconfirm.</span><span class="sxs-lookup"><span data-stu-id="30f91-176">In hello **Program Workspace**, right-click hello **iothub\_amqp\_transport** library, click **Delete**, and then click **OK** tooconfirm.</span></span>

1. <span data-ttu-id="30f91-177">В hello **рабочей программы**, щелкните правой кнопкой мыши hello **azure\_amqp\_c** библиотеки, нажмите кнопку **удалить**и нажмите кнопку **ОК**  tooconfirm.</span><span class="sxs-lookup"><span data-stu-id="30f91-177">In hello **Program Workspace**, right-click hello **azure\_amqp\_c** library, click **Delete**, and then click **OK** tooconfirm.</span></span>

1. <span data-ttu-id="30f91-178">Hello щелкните правой кнопкой мыши **remote_monitoring** проекта в hello **рабочей программы**выберите **библиотека импорта**, а затем выберите **URL-адрес из**.</span><span class="sxs-lookup"><span data-stu-id="30f91-178">Right-click hello **remote_monitoring** project in hello **Program Workspace**, select **Import Library**, then select **From URL**.</span></span>
   
    ![Запуск рабочей toombed библиотеки импорта][6]

1. <span data-ttu-id="30f91-180">Во всплывающем окне приветствия, введите ссылку hello транспорта библиотеки hello MQTT https://developer.mbed.org/users/AzureIoTClient/code/iothub\_mqtt\_транспорта и затем щелкните **импорта**.</span><span class="sxs-lookup"><span data-stu-id="30f91-180">In hello pop-up window, enter hello link for hello MQTT transport library https://developer.mbed.org/users/AzureIoTClient/code/iothub\_mqtt\_transport/ then click **Import**.</span></span>
   
    ![Импорт рабочей toombed библиотеки][12]

1. <span data-ttu-id="30f91-182">Повторите hello предыдущего шага tooadd hello MQTT библиотеки из https://developer.mbed.org/users/AzureIoTClient/code/azure\_umqtt\_c /.</span><span class="sxs-lookup"><span data-stu-id="30f91-182">Repeat hello previous step tooadd hello MQTT library from https://developer.mbed.org/users/AzureIoTClient/code/azure\_umqtt\_c/.</span></span>

1. <span data-ttu-id="30f91-183">Рабочую область теперь выглядит hello следующим образом:</span><span class="sxs-lookup"><span data-stu-id="30f91-183">Your workspace now looks like hello following:</span></span>

    ![Просмотр рабочей области mbed][13]

1. <span data-ttu-id="30f91-185">Откройте hello удаленного\_monitoring\remote_monitoring.c файл и замените существующие hello `#include` инструкции с hello, следующий код:</span><span class="sxs-lookup"><span data-stu-id="30f91-185">Open hello remote\_monitoring\remote_monitoring.c file and replace hello existing `#include` statements with hello following code:</span></span>

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
1. <span data-ttu-id="30f91-186">Удалить все hello, остальной код в удаленном hello\_monitoring\remote\_monitoring.c файла.</span><span class="sxs-lookup"><span data-stu-id="30f91-186">Delete all hello remaining code in hello remote\_monitoring\remote\_monitoring.c file.</span></span>

[!INCLUDE [iot-suite-connecting-code](../../includes/iot-suite-connecting-code.md)]

## <a name="build-and-run-hello-sample"></a><span data-ttu-id="30f91-187">Построение и запуск образца hello</span><span class="sxs-lookup"><span data-stu-id="30f91-187">Build and run hello sample</span></span>

<span data-ttu-id="30f91-188">Добавить код hello tooinvoke **удаленного\_мониторинга\_запуска** функции и затем постройте и запустите приложение hello устройства.</span><span class="sxs-lookup"><span data-stu-id="30f91-188">Add code tooinvoke hello **remote\_monitoring\_run** function and then build and run hello device application.</span></span>

1. <span data-ttu-id="30f91-189">Добавить **основной** функции следующий код в конце hello hello удаленного\_monitoring.c файл tooinvoke hello **удаленного\_мониторинг\_запуска** функции:</span><span class="sxs-lookup"><span data-stu-id="30f91-189">Add a **main** function with following code at hello end of hello remote\_monitoring.c file tooinvoke hello **remote\_monitoring\_run** function:</span></span>
   
    ```c
    int main()
    {
      remote_monitoring_run();
      return 0;
    }
    ```

1. <span data-ttu-id="30f91-190">Нажмите кнопку **компиляции** toobuild hello программы.</span><span class="sxs-lookup"><span data-stu-id="30f91-190">Click **Compile** toobuild hello program.</span></span> <span data-ttu-id="30f91-191">Можно спокойно игнорировать любые предупреждения, но если hello сборки приводит к возникновению ошибки, исправить их перед продолжением.</span><span class="sxs-lookup"><span data-stu-id="30f91-191">You can safely ignore any warnings, but if hello build generates errors, fix them before proceeding.</span></span>

1. <span data-ttu-id="30f91-192">При успешном построении hello веб-сайт компилятора hello mbed приводит к возникновению ошибки Bin-файл с именем hello проекта и загружает его tooyour локального компьютера.</span><span class="sxs-lookup"><span data-stu-id="30f91-192">If hello build is successful, hello mbed compiler website generates a .bin file with hello name of your project and downloads it tooyour local machine.</span></span> <span data-ttu-id="30f91-193">Скопируйте файл toohello hello .bin устройства.</span><span class="sxs-lookup"><span data-stu-id="30f91-193">Copy hello .bin file toohello device.</span></span> <span data-ttu-id="30f91-194">Сохранение файла toohello hello .bin устройство вызывает toorestart hello устройства и запустите программу hello, содержащихся в hello Bin-файл.</span><span class="sxs-lookup"><span data-stu-id="30f91-194">Saving hello .bin file toohello device causes hello device toorestart and run hello program contained in hello .bin file.</span></span> <span data-ttu-id="30f91-195">Программа hello можно перезапустить вручную в любое время, нажав кнопку "сбросить" hello на устройстве mbed hello.</span><span class="sxs-lookup"><span data-stu-id="30f91-195">You can manually restart hello program at any time by pressing hello reset button on hello mbed device.</span></span>

1. <span data-ttu-id="30f91-196">Подключите устройство toohello, с помощью клиентского приложения SSH, например PuTTY.</span><span class="sxs-lookup"><span data-stu-id="30f91-196">Connect toohello device using an SSH client application, such as PuTTY.</span></span> <span data-ttu-id="30f91-197">Можно определить hello последовательного порта, используемого устройства, проверьте в диспетчере устройств Windows.</span><span class="sxs-lookup"><span data-stu-id="30f91-197">You can determine hello serial port your device uses by checking Windows Device Manager.</span></span>
   
    ![][11]

1. <span data-ttu-id="30f91-198">В PuTTY, щелкните hello **последовательной** тип подключения.</span><span class="sxs-lookup"><span data-stu-id="30f91-198">In PuTTY, click hello **Serial** connection type.</span></span> <span data-ttu-id="30f91-199">обычно подключается устройство Hello в 9600 бод, поэтому введите 9600 в hello **скорость** поле.</span><span class="sxs-lookup"><span data-stu-id="30f91-199">hello device typically connects at 9600 baud, so enter 9600 in hello **Speed** box.</span></span> <span data-ttu-id="30f91-200">Затем щелкните **Открыть**.</span><span class="sxs-lookup"><span data-stu-id="30f91-200">Then click **Open**.</span></span>

1. <span data-ttu-id="30f91-201">Программа Hello запускает выполнение.</span><span class="sxs-lookup"><span data-stu-id="30f91-201">hello program starts executing.</span></span> <span data-ttu-id="30f91-202">Если hello программа не запускается автоматически при подключении могут возникнуть tooreset hello доски (нажмите CTRL + Break или кнопки сброса клавишу hello доски).</span><span class="sxs-lookup"><span data-stu-id="30f91-202">You may have tooreset hello board (press CTRL+Break or press hello board's reset button) if hello program does not start automatically when you connect.</span></span>
   
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
