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
# <a name="connect-your-device-toohello-remote-monitoring-preconfigured-solution-windows"></a>Подключение к toohello устройство, удаленное наблюдение предварительно настроенных решений (Windows)
[!INCLUDE [iot-suite-selector-connecting](../../includes/iot-suite-selector-connecting.md)]

## <a name="create-a-c-sample-solution-on-windows"></a>Создание примера решения на C в Windows
Hello, следующие шаги показывают, как toocreate клиентское приложение, которое взаимодействует с удаленного мониторинга hello предварительно настроенных решений. Это приложение на языке C, созданное и запущенное на устройстве Windows.

Создание начального проекта в Visual Studio 2015 или Visual Studio 2017 г. и добавьте пакеты NuGet клиентских устройств центра IoT hello:

1. В Visual Studio, создайте консольное приложение C помощью hello Visual C++ **консольное приложение Win32** шаблона. Имя проекта hello **RMDevice**.
2. На hello **параметры приложения** страницу приветствия **мастер приложений Win32**, убедитесь, что **консольное приложение** выбран и снимите флажки **предкомпилированный Заголовок** и **Security Development Lifecycle (SDL) проверяет**.
3. В **обозревателе решений**, необходимо удалить файлы stdafx.h hello, targetver.h и stdafx.cpp.
4. В **обозревателе решений**, переименуйте tooRMDevice.c RMDevice.cpp файл hello.
5. В **обозревателе решений**, щелкните правой кнопкой мыши на hello **RMDevice** проект и выберите пункт **управление пакетами NuGet**. Нажмите кнопку **Обзор**, а затем найдите и установить следующие пакеты NuGet hello:
   
   * Microsoft.Azure.IoTHub.Serializer
   * Microsoft.Azure.IoTHub.IoTHubClient
   * Microsoft.Azure.IoTHub.MqttTransport.
6. В **обозревателе решений**, щелкните правой кнопкой мыши на hello **RMDevice** проект и выберите пункт **свойства** tooopen hello проекта **страницы свойств**диалоговое окно. Дополнительные сведения см. в статье [Setting Visual C++ Project Properties][lnk-c-project-properties] (Задание свойств проекта Visual C++). 
7. Щелкните hello **компоновщика** папку, нажмите кнопку hello **ввода** страницу свойств.
8. Добавить **crypt32.lib** toohello **Дополнительные зависимости** свойство. Нажмите кнопку **ОК** и затем **ОК** снова toosave hello значения свойства проекта.

Добавить hello Parson JSON библиотеки toohello **RMDevice** проект и добавить необходимые hello `#include` инструкции:

1. В подходящую папку компьютера клона репозитория Parson GitHub hello, с помощью hello следующую команду:

    ```
    git clone https://github.com/kgabis/parson.git
    ```

1. Скопируйте файлы parson.h и parson.c hello из hello локальную копию репозитория tooyour hello Parson **RMDevice** папки проекта.

1. В Visual Studio щелкните правой кнопкой мыши hello **RMDevice** проекта, нажмите кнопку **добавить**, а затем нажмите кнопку **существующий элемент**.

1. В hello **Добавление существующего элемента** диалоговое окно, выберите hello parson.h и parson.c файлы в hello **RMDevice** папки проекта. Нажмите кнопку **добавить** tooadd tooyour эти два файла проекта.

1. В Visual Studio откройте файл RMDevice.c hello. Заменить существующий hello `#include` инструкции с hello, следующий код:
   
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
    > Теперь вы можете убедиться, что проект содержит правильные зависимости hello, настройте, для его создания.

[!INCLUDE [iot-suite-connecting-code](../../includes/iot-suite-connecting-code.md)]

## <a name="build-and-run-hello-sample"></a>Построение и запуск образца hello

Добавить код hello tooinvoke **удаленного\_мониторинга\_запуска** функции и затем постройте и запустите приложение hello устройства.

1. Замените hello **основной** функцию с hello tooinvoke следующий код **удаленного\_мониторинг\_запуска** функции:
   
    ```c
    int main()
    {
      remote_monitoring_run();
      return 0;
    }
    ```

1. Нажмите кнопку **построения** и затем **построить решение** приложение устройства toobuild hello.

1. В **обозревателе решений**, щелкните правой кнопкой мыши hello **RMDevice** проекта, нажмите кнопку **отладки**и нажмите кнопку **запустить новый экземпляр** toorun hello Пример. Hello консоли отображает сообщения, как hello приложение отправляет toohello телеметрии образец предварительно настроенных решений, получает необходимые значения свойств в панели мониторинга решения hello и отвечает toomethods из панели мониторинга hello решения.

[!INCLUDE [iot-suite-visualize-connecting](../../includes/iot-suite-visualize-connecting.md)]

[lnk-c-project-properties]: https://msdn.microsoft.com/library/669zx6zc.aspx
