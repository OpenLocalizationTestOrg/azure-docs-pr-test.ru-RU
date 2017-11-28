---
title: "Преобразование aaaData на шлюзе IoT Azure IoT границу | Документы Microsoft"
description: "Используйте формат hello tooconvert IoT шлюз данных датчика с помощью специализированный модуль Azure IoT края."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "преобразование данных в шлюзе Интернета вещей, преобразование данных в шлюзе IoT"
ms.assetid: 75f2573d-500b-4405-bff7-61021c4c3500
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/25/2017
ms.author: xshi
ms.openlocfilehash: ae94b1f96f36dfcb4f77fadc0ece3cff3d0bba91
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-iot-gateway-for-sensor-data-transformation-with-azure-iot-edge"></a><span data-ttu-id="7d2dc-104">Использование шлюза Интернета вещей для преобразования данных датчиков с помощью Edge Интернета вещей</span><span class="sxs-lookup"><span data-stu-id="7d2dc-104">Use IoT gateway for sensor data transformation with Azure IoT Edge</span></span>

> [!NOTE]
> <span data-ttu-id="7d2dc-105">Перед началом этого учебника, убедитесь, что вы уже завершенной hello в следующих занятиях:</span><span class="sxs-lookup"><span data-stu-id="7d2dc-105">Before you start this tutorial, make sure you’ve completed hello following lessons in sequence:</span></span>
> * [<span data-ttu-id="7d2dc-106">Настройка Intel NUC в качестве шлюза Интернета вещей</span><span class="sxs-lookup"><span data-stu-id="7d2dc-106">Set up Intel NUC as an IoT gateway</span></span>](iot-hub-gateway-kit-c-lesson1-set-up-nuc.md)
> * [<span data-ttu-id="7d2dc-107">Использование облачного toohello действия tooconnect шлюза IoT - SensorTag tooAzure центра IoT</span><span class="sxs-lookup"><span data-stu-id="7d2dc-107">Use IoT gateway tooconnect things toohello cloud - SensorTag tooAzure IoT Hub</span></span>](iot-hub-gateway-kit-c-iot-gateway-connect-device-to-cloud.md)

<span data-ttu-id="7d2dc-108">Один шлюз Iot предназначен tooprocess собранных данных перед их отправкой toohello облака.</span><span class="sxs-lookup"><span data-stu-id="7d2dc-108">One purpose of an Iot gateway is tooprocess collected data before sending it toohello cloud.</span></span> <span data-ttu-id="7d2dc-109">Azure IoT Edge вводит модули, которые могут быть созданы и собранный tooform hello обработки данных, рабочий процесс.</span><span class="sxs-lookup"><span data-stu-id="7d2dc-109">Azure IoT Edge introduces modules which can be created and assembled tooform hello data processing workflow.</span></span> <span data-ttu-id="7d2dc-110">Модуль получает сообщение, выполняет некоторые действия с его и затем переместить ее для других модулей tooprocess.</span><span class="sxs-lookup"><span data-stu-id="7d2dc-110">A module receives a message, performs some action on it, and then move it on for other modules tooprocess.</span></span>

## <a name="what-you-learn"></a><span data-ttu-id="7d2dc-111">Что вы узнаете</span><span class="sxs-lookup"><span data-stu-id="7d2dc-111">What you learn</span></span>

<span data-ttu-id="7d2dc-112">Вы узнаете, как toocreate tooconvert модуль сообщений hello SensorTag в другой формат.</span><span class="sxs-lookup"><span data-stu-id="7d2dc-112">You learn how toocreate a module tooconvert messages from hello SensorTag into a different format.</span></span>

## <a name="what-you-do"></a><span data-ttu-id="7d2dc-113">В рамках этого руководства мы:</span><span class="sxs-lookup"><span data-stu-id="7d2dc-113">What you do</span></span>

* <span data-ttu-id="7d2dc-114">Создание tooconvert модуль полученного сообщения в формате .json hello.</span><span class="sxs-lookup"><span data-stu-id="7d2dc-114">Create a module tooconvert a received message into hello .json format.</span></span>
* <span data-ttu-id="7d2dc-115">Скомпилируйте модуль hello.</span><span class="sxs-lookup"><span data-stu-id="7d2dc-115">Compile hello module.</span></span>
* <span data-ttu-id="7d2dc-116">Добавьте hello модуля toohello ЛЮЧИТЬ образец приложения Azure IoT края.</span><span class="sxs-lookup"><span data-stu-id="7d2dc-116">Add hello module toohello BLE sample application from Azure IoT Edge.</span></span>
* <span data-ttu-id="7d2dc-117">Запустите образец приложения hello.</span><span class="sxs-lookup"><span data-stu-id="7d2dc-117">Run hello sample application.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="7d2dc-118">Необходимые элементы</span><span class="sxs-lookup"><span data-stu-id="7d2dc-118">What you need</span></span>

* <span data-ttu-id="7d2dc-119">После завершения в последовательности учебники Hello:</span><span class="sxs-lookup"><span data-stu-id="7d2dc-119">hello following tutorials completed in sequence:</span></span>
  * [<span data-ttu-id="7d2dc-120">Настройка Intel NUC в качестве шлюза Интернета вещей</span><span class="sxs-lookup"><span data-stu-id="7d2dc-120">Set up Intel NUC as an IoT gateway</span></span>](iot-hub-gateway-kit-c-lesson1-set-up-nuc.md)
  * [<span data-ttu-id="7d2dc-121">Использование облачного toohello действия tooconnect шлюза IoT - SensorTag tooAzure центра IoT</span><span class="sxs-lookup"><span data-stu-id="7d2dc-121">Use IoT gateway tooconnect things toohello cloud - SensorTag tooAzure IoT Hub</span></span>](iot-hub-gateway-kit-c-iot-gateway-connect-device-to-cloud.md)
* <span data-ttu-id="7d2dc-122">Клиент SSH, который выполняется на главном компьютере.</span><span class="sxs-lookup"><span data-stu-id="7d2dc-122">An SSH client that runs on your host computer.</span></span> <span data-ttu-id="7d2dc-123">В Windows рекомендуется использовать PuTTY.</span><span class="sxs-lookup"><span data-stu-id="7d2dc-123">PuTTY is recommended on Windows.</span></span> <span data-ttu-id="7d2dc-124">Клиент SSH изначально входит в состав ОС Linux и Mac OS.</span><span class="sxs-lookup"><span data-stu-id="7d2dc-124">Linux and macOS already come with an SSH client.</span></span>
* <span data-ttu-id="7d2dc-125">Hello IP-адрес и hello имя пользователя и пароль tooaccess hello шлюза из клиента SSH hello.</span><span class="sxs-lookup"><span data-stu-id="7d2dc-125">hello IP address and hello username and password tooaccess hello gateway from hello SSH client.</span></span>
* <span data-ttu-id="7d2dc-126">Подключение к Интернету.</span><span class="sxs-lookup"><span data-stu-id="7d2dc-126">An Internet connection.</span></span>

## <a name="create-a-module"></a><span data-ttu-id="7d2dc-127">Создание модуля</span><span class="sxs-lookup"><span data-stu-id="7d2dc-127">Create a module</span></span>

1. <span data-ttu-id="7d2dc-128">На главном компьютере hello запустите клиент SSH hello и шлюз IoT toohello подключения.</span><span class="sxs-lookup"><span data-stu-id="7d2dc-128">On hello host computer, run hello SSH client and connect toohello IoT gateway.</span></span>
1. <span data-ttu-id="7d2dc-129">Клонирование hello исходные файлы hello преобразования модуля из GitHub toohello шлюза IoT hello в домашнем каталоге, выполнив следующие команды hello:</span><span class="sxs-lookup"><span data-stu-id="7d2dc-129">Clone hello source files of hello conversion module from GitHub toohello home directory of hello IoT gateway by running hello following commands:</span></span>

   ```bash
   cd ~
   git clone https://github.com/Azure-Samples/iot-hub-c-intel-nuc-gateway-customized-module.git
   ```

   <span data-ttu-id="7d2dc-130">Это собственный модуль Azure Edge на языке hello языка программирования.</span><span class="sxs-lookup"><span data-stu-id="7d2dc-130">This is a native Azure Edge module written in hello C programming language.</span></span> <span data-ttu-id="7d2dc-131">модуль Hello преобразует формат hello полученных сообщений в одном hello:</span><span class="sxs-lookup"><span data-stu-id="7d2dc-131">hello module converts hello format of received messages into hello following one:</span></span>

   ```json
   {"deviceId": "Intel NUC Gateway", "messageId": 0, "temperature": 0.0}
   ```

## <a name="compile-hello-module"></a><span data-ttu-id="7d2dc-132">Скомпилируйте модуль hello</span><span class="sxs-lookup"><span data-stu-id="7d2dc-132">Compile hello module</span></span>

<span data-ttu-id="7d2dc-133">hello модуль toocompile, запустите hello, следующие команды:</span><span class="sxs-lookup"><span data-stu-id="7d2dc-133">toocompile hello module, run hello following commands:</span></span>

```bash
cd iot-hub-c-intel-nuc-gateway-customized-module/my_module
# change hello build script runnable
chmod 777 build.sh
# remove hello invalid windows character
sed -i -e "s/\r$//" build.sh
# run hello build shell script
./build.sh
```

<span data-ttu-id="7d2dc-134">Вы получаете `libmy_module.so` файла после завершения компиляции hello.</span><span class="sxs-lookup"><span data-stu-id="7d2dc-134">You get a `libmy_module.so` file after hello compile is completed.</span></span> <span data-ttu-id="7d2dc-135">Запишите hello абсолютный путь этого файла.</span><span class="sxs-lookup"><span data-stu-id="7d2dc-135">Make a note of hello absolute path of this file.</span></span>

## <a name="add-hello-module-toohello-ble-sample-application"></a><span data-ttu-id="7d2dc-136">Добавить hello модуля toohello ЛЮЧИТЬ примера приложения</span><span class="sxs-lookup"><span data-stu-id="7d2dc-136">Add hello module toohello BLE sample application</span></span>

1. <span data-ttu-id="7d2dc-137">Папка образцов перейдите toohello, выполнив следующую команду hello:</span><span class="sxs-lookup"><span data-stu-id="7d2dc-137">Go toohello samples folder by running hello following command:</span></span>

   ```bash
   cd /usr/share/azureiotgatewaysdk/samples
   ```

1. <span data-ttu-id="7d2dc-138">Откройте файл конфигурации hello, выполнив следующую команду hello:</span><span class="sxs-lookup"><span data-stu-id="7d2dc-138">Open hello configuration file by running hello following command:</span></span>

   ```bash
   vi ble_gateway.json
   ```

1. <span data-ttu-id="7d2dc-139">Добавить модуль, вставив следующий код toohello hello `modules` раздела.</span><span class="sxs-lookup"><span data-stu-id="7d2dc-139">Add a module by inserting hello following code toohello `modules` section.</span></span>

   ```json
   {
       "name": "MyModule",
       "loader": {
           "name": "native",
           "entrypoint":{
               "module.path": "[Your libmy_module.so path]"
               }
            },
        "args": null
    },
    ```

1. <span data-ttu-id="7d2dc-140">Замените `[Your libmy_module.so path]` в коде hello hello абсолютном пути hello libmy_module.so "файла.</span><span class="sxs-lookup"><span data-stu-id="7d2dc-140">Replace `[Your libmy_module.so path]` in hello code with hello absolute path of hello libmy_module.so\` file.</span></span>
1. <span data-ttu-id="7d2dc-141">Замените код hello в hello `links` раздел с hello, выполнив одно:</span><span class="sxs-lookup"><span data-stu-id="7d2dc-141">Replace hello code in hello `links` section with hello following one:</span></span>

   ```json
   {
       "source": "SensorTag",
       "sink": "MyModule"
   },
   {
       "source": "MyModule",
       "sink": "mapping"
   }
   ```

1. <span data-ttu-id="7d2dc-142">Нажмите клавишу `ESC`, а затем введите `:wq` toosave hello файла.</span><span class="sxs-lookup"><span data-stu-id="7d2dc-142">Press `ESC`, and then type `:wq` toosave hello file.</span></span>

## <a name="run-hello-sample-application"></a><span data-ttu-id="7d2dc-143">Запустить образец приложения hello</span><span class="sxs-lookup"><span data-stu-id="7d2dc-143">Run hello sample application</span></span>

1. <span data-ttu-id="7d2dc-144">Включите hello SensorTag.</span><span class="sxs-lookup"><span data-stu-id="7d2dc-144">Power on hello SensorTag.</span></span>
1. <span data-ttu-id="7d2dc-145">Задайте переменную среды SSL_CERT_FILE hello, выполнив hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="7d2dc-145">Set hello SSL_CERT_FILE environment variable by running hello following command:</span></span>

   ```bash
   export SSL_CERT_FILE=/etc/ssl/certs/ca-certificates.crt
   ```

1. <span data-ttu-id="7d2dc-146">Выполните пример приложения hello с hello добавленный модуль, выполнив следующую команду hello:</span><span class="sxs-lookup"><span data-stu-id="7d2dc-146">Run hello sample application with hello added module by running hello following command:</span></span>

   ```bash
   ./ble_gateway ble_gateway.json
   ```

## <a name="next-steps"></a><span data-ttu-id="7d2dc-147">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="7d2dc-147">Next steps</span></span>

<span data-ttu-id="7d2dc-148">Вы успешно использовать hello IoT шлюза tooconvert приветственных сообщений из SensorTag в формат .json hello.</span><span class="sxs-lookup"><span data-stu-id="7d2dc-148">You’ve successfully use hello IoT gateway tooconvert hello message from SensorTag into hello .json format.</span></span>

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
