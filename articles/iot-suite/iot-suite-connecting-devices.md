---
title: "Подключение устройства с помощью C в Windows | Документация Майкрософт"
description: "Описывает, как подключить устройство к предварительно настроенному решению для удаленного мониторинга из набора Azure IoT Suite с помощью приложения на C в среде Windows."
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
ms.openlocfilehash: d222bcbd64f288d4091acb0ecd2922b9ceee57e5
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="connect-your-device-to-the-remote-monitoring-preconfigured-solution-windows"></a><span data-ttu-id="172d3-103">Подключение устройства к предварительно настроенному решению для удаленного мониторинга (Windows)</span><span class="sxs-lookup"><span data-stu-id="172d3-103">Connect your device to the remote monitoring preconfigured solution (Windows)</span></span>
[!INCLUDE [iot-suite-selector-connecting](../../includes/iot-suite-selector-connecting.md)]

## <a name="create-a-c-sample-solution-on-windows"></a><span data-ttu-id="172d3-104">Создание примера решения на C в Windows</span><span class="sxs-lookup"><span data-stu-id="172d3-104">Create a C sample solution on Windows</span></span>
<span data-ttu-id="172d3-105">Описанные ниже действия показывают, как создать клиентское приложение, которое взаимодействует с предварительно настроенным решением для удаленного мониторинга.</span><span class="sxs-lookup"><span data-stu-id="172d3-105">The following steps show you how to create a client application that communicates with the remote monitoring preconfigured solution.</span></span> <span data-ttu-id="172d3-106">Это приложение на языке C, созданное и запущенное на устройстве Windows.</span><span class="sxs-lookup"><span data-stu-id="172d3-106">This application is written in C and built and run on Windows.</span></span>

<span data-ttu-id="172d3-107">Создайте начальный проект в Visual Studio 2015 или Visual Studio 2017 и добавьте клиентские пакеты NuGet для устройства центра IoT:</span><span class="sxs-lookup"><span data-stu-id="172d3-107">Create a starter project in Visual Studio 2015 or Visual Studio 2017 and add the IoT Hub device client NuGet packages:</span></span>

1. <span data-ttu-id="172d3-108">В Visual Studio создайте консольное приложение C, используя шаблон **консольного приложения Win32** в Visual C++.</span><span class="sxs-lookup"><span data-stu-id="172d3-108">In Visual Studio, create a C console application using the Visual C++ **Win32 Console Application** template.</span></span> <span data-ttu-id="172d3-109">Присвойте проекту имя **RMDevice**.</span><span class="sxs-lookup"><span data-stu-id="172d3-109">Name the project **RMDevice**.</span></span>
2. <span data-ttu-id="172d3-110">На странице **Параметры приложения** в **мастере приложений Win32** необходимо установить флажок **Консольное приложение** и снять флажки **Предкомпилированный заголовок** и **Жизненный цикл разработки безопасного ПО (SDL)**.</span><span class="sxs-lookup"><span data-stu-id="172d3-110">On the **Application Settings** page in the **Win32 Application Wizard**, ensure that **Console application** is selected, and uncheck **Precompiled header** and **Security Development Lifecycle (SDL) checks**.</span></span>
3. <span data-ttu-id="172d3-111">В **обозревателе решений**удалите файлы stdafx.h, targetver.h и stdafx.cpp.</span><span class="sxs-lookup"><span data-stu-id="172d3-111">In **Solution Explorer**, delete the files stdafx.h, targetver.h, and stdafx.cpp.</span></span>
4. <span data-ttu-id="172d3-112">В **обозревателе решений**переименуйте файл RMDevice.cpp в RMDevice.c.</span><span class="sxs-lookup"><span data-stu-id="172d3-112">In **Solution Explorer**, rename the file RMDevice.cpp to RMDevice.c.</span></span>
5. <span data-ttu-id="172d3-113">В **обозревателе решений** щелкните проект **RMDevice** правой кнопкой мыши и выберите пункт **Управление пакетами NuGet**.</span><span class="sxs-lookup"><span data-stu-id="172d3-113">In **Solution Explorer**, right-click on the **RMDevice** project and then click **Manage NuGet packages**.</span></span> <span data-ttu-id="172d3-114">Щелкните **Обзор**, а затем найдите и установите следующие пакеты NuGet:</span><span class="sxs-lookup"><span data-stu-id="172d3-114">Click **Browse**, then search for and install the following NuGet packages:</span></span>
   
   * <span data-ttu-id="172d3-115">Microsoft.Azure.IoTHub.Serializer</span><span class="sxs-lookup"><span data-stu-id="172d3-115">Microsoft.Azure.IoTHub.Serializer</span></span>
   * <span data-ttu-id="172d3-116">Microsoft.Azure.IoTHub.IoTHubClient</span><span class="sxs-lookup"><span data-stu-id="172d3-116">Microsoft.Azure.IoTHub.IoTHubClient</span></span>
   * <span data-ttu-id="172d3-117">Microsoft.Azure.IoTHub.MqttTransport.</span><span class="sxs-lookup"><span data-stu-id="172d3-117">Microsoft.Azure.IoTHub.MqttTransport</span></span>
6. <span data-ttu-id="172d3-118">В **обозревателе решений** щелкните правой кнопкой мыши проект **RMDevice**, а затем щелкните **Свойства**, чтобы открыть диалоговое окно **Страницы свойств** проекта.</span><span class="sxs-lookup"><span data-stu-id="172d3-118">In **Solution Explorer**, right-click on the **RMDevice** project and then click **Properties** to open the project's **Property Pages** dialog box.</span></span> <span data-ttu-id="172d3-119">Дополнительные сведения см. в статье [Setting Visual C++ Project Properties][lnk-c-project-properties] (Задание свойств проекта Visual C++).</span><span class="sxs-lookup"><span data-stu-id="172d3-119">For details, see [Setting Visual C++ Project Properties][lnk-c-project-properties].</span></span> 
7. <span data-ttu-id="172d3-120">Выберите папку **Компоновщик**, затем щелкните страницу свойств **Входные данные**.</span><span class="sxs-lookup"><span data-stu-id="172d3-120">Click the **Linker** folder, then click the **Input** property page.</span></span>
8. <span data-ttu-id="172d3-121">В свойство **Дополнительные зависимости** добавьте **crypt32.lib**.</span><span class="sxs-lookup"><span data-stu-id="172d3-121">Add **crypt32.lib** to the **Additional Dependencies** property.</span></span> <span data-ttu-id="172d3-122">Нажмите кнопку **ОК**, а затем еще раз **ОК**, чтобы сохранить значения свойств проекта.</span><span class="sxs-lookup"><span data-stu-id="172d3-122">Click **OK** and then **OK** again to save the project property values.</span></span>

<span data-ttu-id="172d3-123">Добавьте библиотеку JSON Parson в проект **RMDevice** и добавьте обязательные инструкции `#include`:</span><span class="sxs-lookup"><span data-stu-id="172d3-123">Add the Parson JSON library to the **RMDevice** project and add the required `#include` statements:</span></span>

1. <span data-ttu-id="172d3-124">В подходящей папке на компьютере клонируйте репозиторий GitHub для Parson, используя следующую команду:</span><span class="sxs-lookup"><span data-stu-id="172d3-124">In a suitable folder on your computer, clone the Parson GitHub repository using the following command:</span></span>

    ```
    git clone https://github.com/kgabis/parson.git
    ```

1. <span data-ttu-id="172d3-125">Скопируйте файлы parson.h и parson.c из локальной копии репозитория Parson в папку проекта **RMDevice**.</span><span class="sxs-lookup"><span data-stu-id="172d3-125">Copy the parson.h and parson.c files from the local copy of the Parson repository to your **RMDevice** project folder.</span></span>

1. <span data-ttu-id="172d3-126">В Visual Studio щелкните правой кнопкой мыши проект **RMDevice**, а затем выберите **Добавить** > **Существующий элемент**.</span><span class="sxs-lookup"><span data-stu-id="172d3-126">In Visual Studio, right-click the **RMDevice** project, click **Add**, and then click **Existing Item**.</span></span>

1. <span data-ttu-id="172d3-127">В диалоговом окне **Добавление существующего элемента** выберите файлы parson.h и parson.c в папке проекта **RMDevice**.</span><span class="sxs-lookup"><span data-stu-id="172d3-127">In the **Add Existing Item** dialog, select the parson.h and parson.c files in the **RMDevice** project folder.</span></span> <span data-ttu-id="172d3-128">Нажмите кнопку **Добавить**, чтобы добавить эти файлы в проект.</span><span class="sxs-lookup"><span data-stu-id="172d3-128">Then click **Add** to add these two files to your project.</span></span>

1. <span data-ttu-id="172d3-129">В Visual Studio откройте файл RMDevice.c.</span><span class="sxs-lookup"><span data-stu-id="172d3-129">In Visual Studio, open the RMDevice.c file.</span></span> <span data-ttu-id="172d3-130">Замените имеющиеся инструкции `#include` в этом окне следующим кодом.</span><span class="sxs-lookup"><span data-stu-id="172d3-130">Replace the existing `#include` statements with the following code:</span></span>
   
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
    > <span data-ttu-id="172d3-131">Теперь вы можете создать проект, чтобы убедиться, что в нем настроены правильные зависимости.</span><span class="sxs-lookup"><span data-stu-id="172d3-131">Now you can verify that your project has the correct dependencies set up by building it.</span></span>

[!INCLUDE [iot-suite-connecting-code](../../includes/iot-suite-connecting-code.md)]

## <a name="build-and-run-the-sample"></a><span data-ttu-id="172d3-132">Сборка и запуск примера</span><span class="sxs-lookup"><span data-stu-id="172d3-132">Build and run the sample</span></span>

<span data-ttu-id="172d3-133">Добавьте код для вызова функции **remote\_monitoring\_run**, а затем создайте и запустите приложение устройства.</span><span class="sxs-lookup"><span data-stu-id="172d3-133">Add code to invoke the **remote\_monitoring\_run** function and then build and run the device application.</span></span>

1. <span data-ttu-id="172d3-134">Замените функцию **main** следующим кодом для вызова функции **remote\_monitoring\_run**:</span><span class="sxs-lookup"><span data-stu-id="172d3-134">Replace the **main** function with following code to invoke the **remote\_monitoring\_run** function:</span></span>
   
    ```c
    int main()
    {
      remote_monitoring_run();
      return 0;
    }
    ```

1. <span data-ttu-id="172d3-135">Щелкните **Построить**, а затем **Построить решение**, чтобы выполнить сборку приложения устройства.</span><span class="sxs-lookup"><span data-stu-id="172d3-135">Click **Build** and then **Build Solution** to build the device application.</span></span>

1. <span data-ttu-id="172d3-136">В **обозревателе решений** щелкните правой кнопкой мыши проект **RMDevice**, нажмите кнопку **Отладка**, а затем щелкните **Запустить новый экземпляр**, чтобы запустить пример.</span><span class="sxs-lookup"><span data-stu-id="172d3-136">In **Solution Explorer**, right-click the **RMDevice** project, click **Debug**, and then click **Start new instance** to run the sample.</span></span> <span data-ttu-id="172d3-137">В консоли отображаются сообщения, когда приложение отправляет пример данных телеметрии в предварительно настроенное решение, получает наборы значений требуемых свойств в панели мониторинга решения и отвечает на методы, вызываемые из панели мониторинга решения.</span><span class="sxs-lookup"><span data-stu-id="172d3-137">The console displays messages as the application sends sample telemetry to the preconfigured solution, receives desired property values set in the solution dashboard, and responds to methods invoked from the solution dashboard.</span></span>

[!INCLUDE [iot-suite-visualize-connecting](../../includes/iot-suite-visualize-connecting.md)]

[lnk-c-project-properties]: https://msdn.microsoft.com/library/669zx6zc.aspx
