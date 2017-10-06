---
title: "aaaConnect устройство с помощью C в Linux | Документы Microsoft"
description: "Описывает, как tooconnect toohello устройства Azure IoT Suite заранее настроенные удаленного мониторинга решения, с помощью приложения, написанного на языке C, выполняемым на платформе Linux."
services: 
suite: iot-suite
documentationcenter: na
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 0c7c8039-0bbf-4bb5-9e79-ed8cff433629
ms.service: iot-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: dobett
ms.openlocfilehash: 57393817d40d3555177956a01fa71058bc256988
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="connect-your-device-toohello-remote-monitoring-preconfigured-solution-linux"></a><span data-ttu-id="a6ab4-103">Подключение к toohello устройство, удаленное наблюдение предварительно настроенных решений (Linux)</span><span class="sxs-lookup"><span data-stu-id="a6ab4-103">Connect your device toohello remote monitoring preconfigured solution (Linux)</span></span>
[!INCLUDE [iot-suite-selector-connecting](../../includes/iot-suite-selector-connecting.md)]

## <a name="build-and-run-a-sample-c-client-linux"></a><span data-ttu-id="a6ab4-104">Сборка и запуск примера клиента Linux на C</span><span class="sxs-lookup"><span data-stu-id="a6ab4-104">Build and run a sample C client Linux</span></span>
<span data-ttu-id="a6ab4-105">Hello, следующие шаги показывают, как toocreate клиентское приложение, которое взаимодействует с удаленного мониторинга hello предварительно настроенных решений.</span><span class="sxs-lookup"><span data-stu-id="a6ab4-105">hello following steps show you how toocreate a client application that communicates with hello remote monitoring preconfigured solution.</span></span> <span data-ttu-id="a6ab4-106">Это приложение на языке C, созданное и запущенное на устройстве Ubuntu Linux.</span><span class="sxs-lookup"><span data-stu-id="a6ab4-106">This application is written in C and built and run on Ubuntu Linux.</span></span>

<span data-ttu-id="a6ab4-107">toocomplete эти шаги, необходимые на устройстве под управлением Ubuntu версии 15.04 и 15.10.</span><span class="sxs-lookup"><span data-stu-id="a6ab4-107">toocomplete these steps, you need a device running Ubuntu version 15.04 or 15.10.</span></span> <span data-ttu-id="a6ab4-108">Прежде чем продолжить, установите пакеты необходимых компонентов hello на Ubuntu устройства с помощью hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="a6ab4-108">Before proceeding, install hello prerequisite packages on your Ubuntu device using hello following command:</span></span>

```
sudo apt-get install cmake gcc g++
```

## <a name="install-hello-client-libraries-on-your-device"></a><span data-ttu-id="a6ab4-109">Установка клиентских библиотек hello на устройстве</span><span class="sxs-lookup"><span data-stu-id="a6ab4-109">Install hello client libraries on your device</span></span>
<span data-ttu-id="a6ab4-110">Hello клиентские библиотеки центр IoT Azure доступны в виде пакета, можно установить на устройстве с помощью hello Ubuntu **apt get** команды.</span><span class="sxs-lookup"><span data-stu-id="a6ab4-110">hello Azure IoT Hub client libraries are available as a package you can install on your Ubuntu device using hello **apt-get** command.</span></span> <span data-ttu-id="a6ab4-111">Выполните следующие шаги tooinstall hello пакет, который содержит hello центра IoT клиентской библиотеки и заголовочные файлы на вашем компьютере Ubuntu hello.</span><span class="sxs-lookup"><span data-stu-id="a6ab4-111">Complete hello following steps tooinstall hello package that contains hello IoT Hub client library and header files on your Ubuntu computer:</span></span>

1. <span data-ttu-id="a6ab4-112">В оболочке добавьте hello AzureIoT репозитория tooyour компьютера:</span><span class="sxs-lookup"><span data-stu-id="a6ab4-112">In a shell, add hello AzureIoT repository tooyour computer:</span></span>
   
    ```
    sudo add-apt-repository ppa:aziotsdklinux/ppa-azureiot
    sudo apt-get update
    ```
2. <span data-ttu-id="a6ab4-113">Установите пакет azure-iot-sdk-c-dev hello</span><span class="sxs-lookup"><span data-stu-id="a6ab4-113">Install hello azure-iot-sdk-c-dev package</span></span>
   
    ```
    sudo apt-get install -y azure-iot-sdk-c-dev
    ```

## <a name="install-hello-parson-json-parser"></a><span data-ttu-id="a6ab4-114">Установите средство синтаксического анализа Parson JSON hello</span><span class="sxs-lookup"><span data-stu-id="a6ab4-114">Install hello Parson JSON parser</span></span>
<span data-ttu-id="a6ab4-115">Центр IoT клиентские библиотеки используют Hello hello Parson средство синтаксического анализа tooparse сообщение полезные данные JSON.</span><span class="sxs-lookup"><span data-stu-id="a6ab4-115">hello IoT Hub client libraries use hello Parson JSON parser tooparse message payloads.</span></span> <span data-ttu-id="a6ab4-116">В подходящую папку компьютера клона репозитория Parson GitHub hello, с помощью hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="a6ab4-116">In a suitable folder on your computer, clone hello Parson GitHub repository using hello following command:</span></span>

```
git clone https://github.com/kgabis/parson.git
```

## <a name="prepare-your-project"></a><span data-ttu-id="a6ab4-117">Подготовка проекта</span><span class="sxs-lookup"><span data-stu-id="a6ab4-117">Prepare your project</span></span>
<span data-ttu-id="a6ab4-118">На компьютере Ubuntu создайте папку **remote\_monitoring**.</span><span class="sxs-lookup"><span data-stu-id="a6ab4-118">On your Ubuntu machine, create a folder called **remote\_monitoring**.</span></span> <span data-ttu-id="a6ab4-119">В hello **удаленного\_мониторинг** папки:</span><span class="sxs-lookup"><span data-stu-id="a6ab4-119">In hello **remote\_monitoring** folder:</span></span>

- <span data-ttu-id="a6ab4-120">Создайте четыре файла hello **main.c**, **удаленного\_monitoring.c**, **удаленного\_monitoring.h**, и **CMakeLists.txt**.</span><span class="sxs-lookup"><span data-stu-id="a6ab4-120">Create hello four files **main.c**, **remote\_monitoring.c**, **remote\_monitoring.h**, and **CMakeLists.txt**.</span></span>
- <span data-ttu-id="a6ab4-121">Создайте папку с именем **parson**.</span><span class="sxs-lookup"><span data-stu-id="a6ab4-121">Create folder called **parson**.</span></span>

<span data-ttu-id="a6ab4-122">Скопируйте файлы hello **parson.c** и **parson.h** из локальной копии репозитория Parson hello в hello **удаленного\_мониторинг parson** папки.</span><span class="sxs-lookup"><span data-stu-id="a6ab4-122">Copy hello files **parson.c** and **parson.h** from your local copy of hello Parson repository into hello **remote\_monitoring/parson** folder.</span></span>

<span data-ttu-id="a6ab4-123">В текстовом редакторе откройте hello **удаленного\_monitoring.c** файла.</span><span class="sxs-lookup"><span data-stu-id="a6ab4-123">In a text editor, open hello **remote\_monitoring.c** file.</span></span> <span data-ttu-id="a6ab4-124">Добавьте следующее hello `#include` инструкции:</span><span class="sxs-lookup"><span data-stu-id="a6ab4-124">Add hello following `#include` statements:</span></span>
   
```
#include "iothubtransportmqtt.h"
#include "schemalib.h"
#include "iothub_client.h"
#include "serializer_devicetwin.h"
#include "schemaserializer.h"
#include "azure_c_shared_utility/threadapi.h"
#include "azure_c_shared_utility/platform.h"
#include "parson.h"
```

[!INCLUDE [iot-suite-connecting-code](../../includes/iot-suite-connecting-code.md)]

## <a name="call-hello-remotemonitoringrun-function"></a><span data-ttu-id="a6ab4-125">Вызов удаленного hello\_мониторинг\_выполнение функции</span><span class="sxs-lookup"><span data-stu-id="a6ab4-125">Call hello remote\_monitoring\_run function</span></span>
<span data-ttu-id="a6ab4-126">В текстовом редакторе откройте hello **remote_monitoring.h** файла.</span><span class="sxs-lookup"><span data-stu-id="a6ab4-126">In a text editor, open hello **remote_monitoring.h** file.</span></span> <span data-ttu-id="a6ab4-127">Добавьте следующий код hello:</span><span class="sxs-lookup"><span data-stu-id="a6ab4-127">Add hello following code:</span></span>

```
void remote_monitoring_run(void);
```

<span data-ttu-id="a6ab4-128">В текстовом редакторе откройте hello **main.c** файла.</span><span class="sxs-lookup"><span data-stu-id="a6ab4-128">In a text editor, open hello **main.c** file.</span></span> <span data-ttu-id="a6ab4-129">Добавьте следующий код hello:</span><span class="sxs-lookup"><span data-stu-id="a6ab4-129">Add hello following code:</span></span>

```
#include "remote_monitoring.h"

int main(void)
{
    remote_monitoring_run();

    return 0;
}
```

## <a name="build-and-run-hello-application"></a><span data-ttu-id="a6ab4-130">Постройте и запустите приложение hello</span><span class="sxs-lookup"><span data-stu-id="a6ab4-130">Build and run hello application</span></span>
<span data-ttu-id="a6ab4-131">Hello следующие шаги описывают как toouse *CMake* toobuild клиентского приложения.</span><span class="sxs-lookup"><span data-stu-id="a6ab4-131">hello following steps describe how toouse *CMake* toobuild your client application.</span></span>

1. <span data-ttu-id="a6ab4-132">В текстовом редакторе откройте hello **CMakeLists.txt** файла в hello **remote_monitoring** папки.</span><span class="sxs-lookup"><span data-stu-id="a6ab4-132">In a text editor, open hello **CMakeLists.txt** file in hello **remote_monitoring** folder.</span></span>

1. <span data-ttu-id="a6ab4-133">Добавьте следующие инструкции toodefine как hello toobuild клиентского приложения:</span><span class="sxs-lookup"><span data-stu-id="a6ab4-133">Add hello following instructions toodefine how toobuild your client application:</span></span>
   
    ```
    macro(compileAsC99)
      if (CMAKE_VERSION VERSION_LESS "3.1")
        if (CMAKE_C_COMPILER_ID STREQUAL "GNU")
          set (CMAKE_C_FLAGS "--std=c99 ${CMAKE_C_FLAGS}")
          set (CMAKE_CXX_FLAGS "--std=c++11 ${CMAKE_CXX_FLAGS}")
        endif()
      else()
        set (CMAKE_C_STANDARD 99)
        set (CMAKE_CXX_STANDARD 11)
      endif()
    endmacro(compileAsC99)

    cmake_minimum_required(VERSION 2.8.11)
    compileAsC99()

    set(AZUREIOT_INC_FOLDER "${CMAKE_SOURCE_DIR}" "${CMAKE_SOURCE_DIR}/parson" "/usr/include/azureiot" "/usr/include/azureiot/inc")

    include_directories(${AZUREIOT_INC_FOLDER})

    set(sample_application_c_files
        ./parson/parson.c
        ./remote_monitoring.c
        ./main.c
    )

    set(sample_application_h_files
        ./parson/parson.h
        ./remote_monitoring.h
    )

    add_executable(sample_app ${sample_application_c_files} ${sample_application_h_files})

    target_link_libraries(sample_app
        serializer
        iothub_client
        iothub_client_mqtt_transport
        aziotsharedutil
        umqtt
        pthread
        curl
        ssl
        crypto
        m
    )
    ```
1. <span data-ttu-id="a6ab4-134">В hello **remote_monitoring** папки, создайте папку toostore hello *сделать* файлами, CMake приводит к возникновению ошибки, а затем запустите hello **cmake** и **сделать** команд следующим образом:</span><span class="sxs-lookup"><span data-stu-id="a6ab4-134">In hello **remote_monitoring** folder, create a folder toostore hello *make* files that CMake generates and then run hello **cmake** and **make** commands as follows:</span></span>
   
    ```
    mkdir cmake
    cd cmake
    cmake ../
    make
    ```

1. <span data-ttu-id="a6ab4-135">Запуск клиентского приложения hello и отправлять данные телеметрии tooIoT концентратора:</span><span class="sxs-lookup"><span data-stu-id="a6ab4-135">Run hello client application and send telemetry tooIoT Hub:</span></span>
   
    ```
    ./sample_app
    ```

[!INCLUDE [iot-suite-visualize-connecting](../../includes/iot-suite-visualize-connecting.md)]

