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
# <a name="connect-your-device-toohello-remote-monitoring-preconfigured-solution-linux"></a>Подключение к toohello устройство, удаленное наблюдение предварительно настроенных решений (Linux)
[!INCLUDE [iot-suite-selector-connecting](../../includes/iot-suite-selector-connecting.md)]

## <a name="build-and-run-a-sample-c-client-linux"></a>Сборка и запуск примера клиента Linux на C
Hello, следующие шаги показывают, как toocreate клиентское приложение, которое взаимодействует с удаленного мониторинга hello предварительно настроенных решений. Это приложение на языке C, созданное и запущенное на устройстве Ubuntu Linux.

toocomplete эти шаги, необходимые на устройстве под управлением Ubuntu версии 15.04 и 15.10. Прежде чем продолжить, установите пакеты необходимых компонентов hello на Ubuntu устройства с помощью hello следующую команду:

```
sudo apt-get install cmake gcc g++
```

## <a name="install-hello-client-libraries-on-your-device"></a>Установка клиентских библиотек hello на устройстве
Hello клиентские библиотеки центр IoT Azure доступны в виде пакета, можно установить на устройстве с помощью hello Ubuntu **apt get** команды. Выполните следующие шаги tooinstall hello пакет, который содержит hello центра IoT клиентской библиотеки и заголовочные файлы на вашем компьютере Ubuntu hello.

1. В оболочке добавьте hello AzureIoT репозитория tooyour компьютера:
   
    ```
    sudo add-apt-repository ppa:aziotsdklinux/ppa-azureiot
    sudo apt-get update
    ```
2. Установите пакет azure-iot-sdk-c-dev hello
   
    ```
    sudo apt-get install -y azure-iot-sdk-c-dev
    ```

## <a name="install-hello-parson-json-parser"></a>Установите средство синтаксического анализа Parson JSON hello
Центр IoT клиентские библиотеки используют Hello hello Parson средство синтаксического анализа tooparse сообщение полезные данные JSON. В подходящую папку компьютера клона репозитория Parson GitHub hello, с помощью hello следующую команду:

```
git clone https://github.com/kgabis/parson.git
```

## <a name="prepare-your-project"></a>Подготовка проекта
На компьютере Ubuntu создайте папку **remote\_monitoring**. В hello **удаленного\_мониторинг** папки:

- Создайте четыре файла hello **main.c**, **удаленного\_monitoring.c**, **удаленного\_monitoring.h**, и **CMakeLists.txt**.
- Создайте папку с именем **parson**.

Скопируйте файлы hello **parson.c** и **parson.h** из локальной копии репозитория Parson hello в hello **удаленного\_мониторинг parson** папки.

В текстовом редакторе откройте hello **удаленного\_monitoring.c** файла. Добавьте следующее hello `#include` инструкции:
   
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

## <a name="call-hello-remotemonitoringrun-function"></a>Вызов удаленного hello\_мониторинг\_выполнение функции
В текстовом редакторе откройте hello **remote_monitoring.h** файла. Добавьте следующий код hello:

```
void remote_monitoring_run(void);
```

В текстовом редакторе откройте hello **main.c** файла. Добавьте следующий код hello:

```
#include "remote_monitoring.h"

int main(void)
{
    remote_monitoring_run();

    return 0;
}
```

## <a name="build-and-run-hello-application"></a>Постройте и запустите приложение hello
Hello следующие шаги описывают как toouse *CMake* toobuild клиентского приложения.

1. В текстовом редакторе откройте hello **CMakeLists.txt** файла в hello **remote_monitoring** папки.

1. Добавьте следующие инструкции toodefine как hello toobuild клиентского приложения:
   
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
1. В hello **remote_monitoring** папки, создайте папку toostore hello *сделать* файлами, CMake приводит к возникновению ошибки, а затем запустите hello **cmake** и **сделать** команд следующим образом:
   
    ```
    mkdir cmake
    cd cmake
    cmake ../
    make
    ```

1. Запуск клиентского приложения hello и отправлять данные телеметрии tooIoT концентратора:
   
    ```
    ./sample_app
    ```

[!INCLUDE [iot-suite-visualize-connecting](../../includes/iot-suite-visualize-connecting.md)]

