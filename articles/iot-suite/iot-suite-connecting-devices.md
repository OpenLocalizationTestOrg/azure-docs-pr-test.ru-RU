---
title: "aaaConnect устройство с помощью C для Windows | Документы Microsoft"
description: "Описывает, как tooconnect toohello устройства Azure IoT Suite заранее настроенные удаленного мониторинга решения, с помощью приложения, написанного на языке C, работающей под управлением Windows."
services: 
suite: iot-suite
documentationcenter: na
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 34e39a58-2434-482c-b3fa-29438a0c05e8
ms.service: iot-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: dobett
ms.openlocfilehash: 51041e0cec113a5cfa006ab2276096baf928eef5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="connect-your-device-toohello-remote-monitoring-preconfigured-solution-windows"></a><span data-ttu-id="74a85-103">Подключение к toohello устройство, удаленное наблюдение предварительно настроенных решений (Windows)</span><span class="sxs-lookup"><span data-stu-id="74a85-103">Connect your device toohello remote monitoring preconfigured solution (Windows)</span></span>
[!INCLUDE [iot-suite-selector-connecting](../../includes/iot-suite-selector-connecting.md)]

## <a name="create-a-c-sample-solution-on-windows"></a><span data-ttu-id="74a85-104">Создание примера решения на C в Windows</span><span class="sxs-lookup"><span data-stu-id="74a85-104">Create a C sample solution on Windows</span></span>
<span data-ttu-id="74a85-105">Hello, следующие шаги показывают, как toocreate клиентское приложение, которое взаимодействует с удаленного мониторинга hello предварительно настроенных решений.</span><span class="sxs-lookup"><span data-stu-id="74a85-105">hello following steps show you how toocreate a client application that communicates with hello remote monitoring preconfigured solution.</span></span> <span data-ttu-id="74a85-106">Это приложение на языке C, созданное и запущенное на устройстве Windows.</span><span class="sxs-lookup"><span data-stu-id="74a85-106">This application is written in C and built and run on Windows.</span></span>

<span data-ttu-id="74a85-107">Создание начального проекта в Visual Studio 2015 или Visual Studio 2017 г. и добавьте пакеты NuGet клиентских устройств центра IoT hello:</span><span class="sxs-lookup"><span data-stu-id="74a85-107">Create a starter project in Visual Studio 2015 or Visual Studio 2017 and add hello IoT Hub device client NuGet packages:</span></span>

1. <span data-ttu-id="74a85-108">В Visual Studio, создайте консольное приложение C помощью hello Visual C++ **консольное приложение Win32** шаблона.</span><span class="sxs-lookup"><span data-stu-id="74a85-108">In Visual Studio, create a C console application using hello Visual C++ **Win32 Console Application** template.</span></span> <span data-ttu-id="74a85-109">Имя проекта hello **RMDevice**.</span><span class="sxs-lookup"><span data-stu-id="74a85-109">Name hello project **RMDevice**.</span></span>
2. <span data-ttu-id="74a85-110">На hello **параметры приложения** страницу приветствия **мастер приложений Win32**, убедитесь, что **консольное приложение** выбран и снимите флажки **предкомпилированный Заголовок** и **Security Development Lifecycle (SDL) проверяет**.</span><span class="sxs-lookup"><span data-stu-id="74a85-110">On hello **Application Settings** page in hello **Win32 Application Wizard**, ensure that **Console application** is selected, and uncheck **Precompiled header** and **Security Development Lifecycle (SDL) checks**.</span></span>
3. <span data-ttu-id="74a85-111">В **обозревателе решений**, необходимо удалить файлы stdafx.h hello, targetver.h и stdafx.cpp.</span><span class="sxs-lookup"><span data-stu-id="74a85-111">In **Solution Explorer**, delete hello files stdafx.h, targetver.h, and stdafx.cpp.</span></span>
4. <span data-ttu-id="74a85-112">В **обозревателе решений**, переименуйте tooRMDevice.c RMDevice.cpp файл hello.</span><span class="sxs-lookup"><span data-stu-id="74a85-112">In **Solution Explorer**, rename hello file RMDevice.cpp tooRMDevice.c.</span></span>
5. <span data-ttu-id="74a85-113">В **обозревателе решений**, щелкните правой кнопкой мыши на hello **RMDevice** проект и выберите пункт **управление пакетами NuGet**.</span><span class="sxs-lookup"><span data-stu-id="74a85-113">In **Solution Explorer**, right-click on hello **RMDevice** project and then click **Manage NuGet packages**.</span></span> <span data-ttu-id="74a85-114">Нажмите кнопку **Обзор**, а затем найдите и установить следующие пакеты NuGet hello:</span><span class="sxs-lookup"><span data-stu-id="74a85-114">Click **Browse**, then search for and install hello following NuGet packages:</span></span>
   
   * <span data-ttu-id="74a85-115">Microsoft.Azure.IoTHub.Serializer</span><span class="sxs-lookup"><span data-stu-id="74a85-115">Microsoft.Azure.IoTHub.Serializer</span></span>
   * <span data-ttu-id="74a85-116">Microsoft.Azure.IoTHub.IoTHubClient</span><span class="sxs-lookup"><span data-stu-id="74a85-116">Microsoft.Azure.IoTHub.IoTHubClient</span></span>
   * <span data-ttu-id="74a85-117">Microsoft.Azure.IoTHub.MqttTransport.</span><span class="sxs-lookup"><span data-stu-id="74a85-117">Microsoft.Azure.IoTHub.MqttTransport</span></span>
6. <span data-ttu-id="74a85-118">В **обозревателе решений**, щелкните правой кнопкой мыши на hello **RMDevice** проект и выберите пункт **свойства** tooopen hello проекта **страницы свойств**диалоговое окно.</span><span class="sxs-lookup"><span data-stu-id="74a85-118">In **Solution Explorer**, right-click on hello **RMDevice** project and then click **Properties** tooopen hello project's **Property Pages** dialog box.</span></span> <span data-ttu-id="74a85-119">Дополнительные сведения см. в статье [Setting Visual C++ Project Properties][lnk-c-project-properties] (Задание свойств проекта Visual C++).</span><span class="sxs-lookup"><span data-stu-id="74a85-119">For details, see [Setting Visual C++ Project Properties][lnk-c-project-properties].</span></span> 
7. <span data-ttu-id="74a85-120">Щелкните hello **компоновщика** папку, нажмите кнопку hello **ввода** страницу свойств.</span><span class="sxs-lookup"><span data-stu-id="74a85-120">Click hello **Linker** folder, then click hello **Input** property page.</span></span>
8. <span data-ttu-id="74a85-121">Добавить **crypt32.lib** toohello **Дополнительные зависимости** свойство.</span><span class="sxs-lookup"><span data-stu-id="74a85-121">Add **crypt32.lib** toohello **Additional Dependencies** property.</span></span> <span data-ttu-id="74a85-122">Нажмите кнопку **ОК** и затем **ОК** снова toosave hello значения свойства проекта.</span><span class="sxs-lookup"><span data-stu-id="74a85-122">Click **OK** and then **OK** again toosave hello project property values.</span></span>

<span data-ttu-id="74a85-123">Добавить hello Parson JSON библиотеки toohello **RMDevice** проект и добавить необходимые hello `#include` инструкции:</span><span class="sxs-lookup"><span data-stu-id="74a85-123">Add hello Parson JSON library toohello **RMDevice** project and add hello required `#include` statements:</span></span>

1. <span data-ttu-id="74a85-124">В подходящую папку компьютера клона репозитория Parson GitHub hello, с помощью hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="74a85-124">In a suitable folder on your computer, clone hello Parson GitHub repository using hello following command:</span></span>

    ```
    git clone https://github.com/kgabis/parson.git
    ```

1. <span data-ttu-id="74a85-125">Скопируйте файлы parson.h и parson.c hello из hello локальную копию репозитория tooyour hello Parson **RMDevice** папки проекта.</span><span class="sxs-lookup"><span data-stu-id="74a85-125">Copy hello parson.h and parson.c files from hello local copy of hello Parson repository tooyour **RMDevice** project folder.</span></span>

1. <span data-ttu-id="74a85-126">В Visual Studio щелкните правой кнопкой мыши hello **RMDevice** проекта, нажмите кнопку **добавить**, а затем нажмите кнопку **существующий элемент**.</span><span class="sxs-lookup"><span data-stu-id="74a85-126">In Visual Studio, right-click hello **RMDevice** project, click **Add**, and then click **Existing Item**.</span></span>

1. <span data-ttu-id="74a85-127">В hello **Добавление существующего элемента** диалоговое окно, выберите hello parson.h и parson.c файлы в hello **RMDevice** папки проекта.</span><span class="sxs-lookup"><span data-stu-id="74a85-127">In hello **Add Existing Item** dialog, select hello parson.h and parson.c files in hello **RMDevice** project folder.</span></span> <span data-ttu-id="74a85-128">Нажмите кнопку **добавить** tooadd tooyour эти два файла проекта.</span><span class="sxs-lookup"><span data-stu-id="74a85-128">Then click **Add** tooadd these two files tooyour project.</span></span>

1. <span data-ttu-id="74a85-129">В Visual Studio откройте файл RMDevice.c hello.</span><span class="sxs-lookup"><span data-stu-id="74a85-129">In Visual Studio, open hello RMDevice.c file.</span></span> <span data-ttu-id="74a85-130">Заменить существующий hello `#include` инструкции с hello, следующий код:</span><span class="sxs-lookup"><span data-stu-id="74a85-130">Replace hello existing `#include` statements with hello following code:</span></span>
   
    ```c
    #include "iothubtransportmqtt.h"
    #include "schemalib.h"
    #include "iothub_client.h"
    #include "serializer_devicetwin.h"
    #include "schemaserializer.h"
    #include "azure_c_shared_utility/threadapi.h"
    #include "azure_c_shared_utility/platform.h"
    #include "parson.h"
    ```

    > [!NOTE]
    > <span data-ttu-id="74a85-131">Теперь вы можете убедиться, что проект содержит правильные зависимости hello, настройте, для его создания.</span><span class="sxs-lookup"><span data-stu-id="74a85-131">Now you can verify that your project has hello correct dependencies set up by building it.</span></span>

[!INCLUDE [iot-suite-connecting-code](../../includes/iot-suite-connecting-code.md)]

## <a name="build-and-run-hello-sample"></a><span data-ttu-id="74a85-132">Построение и запуск образца hello</span><span class="sxs-lookup"><span data-stu-id="74a85-132">Build and run hello sample</span></span>

<span data-ttu-id="74a85-133">Добавить код hello tooinvoke **удаленного\_мониторинга\_запуска** функции и затем постройте и запустите приложение hello устройства.</span><span class="sxs-lookup"><span data-stu-id="74a85-133">Add code tooinvoke hello **remote\_monitoring\_run** function and then build and run hello device application.</span></span>

1. <span data-ttu-id="74a85-134">Замените hello **основной** функцию с hello tooinvoke следующий код **удаленного\_мониторинг\_запуска** функции:</span><span class="sxs-lookup"><span data-stu-id="74a85-134">Replace hello **main** function with following code tooinvoke hello **remote\_monitoring\_run** function:</span></span>
   
    ```c
    int main()
    {
      remote_monitoring_run();
      return 0;
    }
    ```

1. <span data-ttu-id="74a85-135">Нажмите кнопку **построения** и затем **построить решение** приложение устройства toobuild hello.</span><span class="sxs-lookup"><span data-stu-id="74a85-135">Click **Build** and then **Build Solution** toobuild hello device application.</span></span>

1. <span data-ttu-id="74a85-136">В **обозревателе решений**, щелкните правой кнопкой мыши hello **RMDevice** проекта, нажмите кнопку **отладки**и нажмите кнопку **запустить новый экземпляр** toorun hello Пример.</span><span class="sxs-lookup"><span data-stu-id="74a85-136">In **Solution Explorer**, right-click hello **RMDevice** project, click **Debug**, and then click **Start new instance** toorun hello sample.</span></span> <span data-ttu-id="74a85-137">Hello консоли отображает сообщения, как hello приложение отправляет toohello телеметрии образец предварительно настроенных решений, получает необходимые значения свойств в панели мониторинга решения hello и отвечает toomethods из панели мониторинга hello решения.</span><span class="sxs-lookup"><span data-stu-id="74a85-137">hello console displays messages as hello application sends sample telemetry toohello preconfigured solution, receives desired property values set in hello solution dashboard, and responds toomethods invoked from hello solution dashboard.</span></span>

[!INCLUDE [iot-suite-visualize-connecting](../../includes/iot-suite-visualize-connecting.md)]

[lnk-c-project-properties]: https://msdn.microsoft.com/library/669zx6zc.aspx
