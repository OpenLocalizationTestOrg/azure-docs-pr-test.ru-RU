---
title: "часто задаваемые вопросы о фабрики подключен aaaAzure IoT Suite | Документы Microsoft"
description: "Часто задаваемые вопросы о подключенной фабрике IoT Suite."
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 
ms.service: iot-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/15/2017
ms.author: corywink
ms.openlocfilehash: 4ae9beb0daf1b0578850cd652eaca7635b0d039d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="frequently-asked-questions-for-iot-suite-connected-factory-preconfigured-solution"></a>Часто задаваемые вопросы о предварительно настроенном решении для подключенной фабрики IoT Suite

См. также, hello Общие [часто задаваемые вопросы о](iot-suite-faq.md) для IoT Suite.

### <a name="where-can-i-find-hello-source-code-for-hello-preconfigured-solution"></a>Где найти hello исходного кода для hello предварительно настроенное решение?

Hello исходный код хранится в hello, следуя репозитории GitHub:

* [Предварительно настроенное решение для подключенной фабрики](https://github.com/Azure/azure-iot-connected-factory)

### <a name="what-is-opc-ua"></a>Что такое OPC UA?

Унифицированная архитектура OPC (OPC UA, выпущена в 2008 г.) — это независящий от платформы, сервис-ориентированный стандарт взаимодействия. OPC UA используется в различных производственных системах и устройствах, например в производственных компьютерах, контроллерах ПЛК и датчиках. OPC UA интегрирует функции hello спецификации OPC классический hello в один расширяемая инфраструктура с помощью встроенных средств безопасности. Это стандарт, в котором определяется hello OPC Foundation. Hello [OPC Foundation](http://opcfoundation.org/) -организация не для роста прибыли, с более чем 440 членов. Задача Hello hello организации — toouse OPC спецификации toofacilitate нескольких поставщиков, несколькими платформами, безопасным и надежным взаимодействия с использованием:

* Инфраструктура
* спецификации;
* Технология
* Процессы

### <a name="why-did-microsoft-choose-opc-ua-for-hello-connected-factory-preconfigured-solution"></a>Почему корпорация Майкрософт была выбрана UA OPC для hello подключения фабрики предварительно настроенное решение?

Корпорация Майкрософт выбрала OPC UA, потому что это открытый, незапатентованный и общепризнанный отраслевой стандарт, независящий от платформы. Это требование для решений эталонной архитектуры Industrie 4.0 (RAMI 4.0), чтобы обеспечить взаимодействие между разнообразными производственными процессами и оборудованием. Корпорация Майкрософт видит запросу из наших клиентов toobuild Industrie 4.0 решений. Поддержка OPC UA помогает нижней hello барьера для клиентов tooachieve поставленных целей и обеспечивает немедленное business toothem значение.

### <a name="how-do-i-add-a-public-ip-address-toohello-simulation-vm"></a>Как добавить открытый toohello моделирование IP адрес виртуальной Машины?

У вас есть два параметры tooadd hello IP-адрес:

* Использовать сценарий PowerShell hello `Simulation/Factory/Add-SimulationPublicIp.ps1` в hello [репозитория](https://github.com/Azure/azure-iot-connected-factory). Передайте имя развертывания в качестве параметра. Для локального развертывания используйте имя `<your username>ConnFactoryLocal`. сценарий Hello выводит hello IP-адрес hello виртуальной Машины.

* Найдите группы ресурсов hello развертывания hello портал Azure. За исключением локальное развертывание группа ресурсов hello имеет hello имя, указанное в качестве решения или развертывания. Для локального развертывания, с помощью скрипта построения hello, hello имя группы ресурсов hello — `<your username>ConnFactoryLocal`. Теперь добавьте новый **общедоступный IP-адрес** toohello группу ресурсов.

> [!NOTE]
> В любом случае убедитесь, установка последних исправлений hello по инструкциям hello hello [Ubuntu веб-сайт](https://wiki.ubuntu.com/Security/Upgrades). Сохраните hello системы toodate для при условии, что ВМ можно сделать через общедоступный IP-адрес.

### <a name="how-do-i-remove-hello-public-ip-address-toohello-simulation-vm"></a>Как удалить hello открытый IP адрес toohello моделирование виртуальных Машин?

У вас есть два параметры tooremove hello IP-адрес:

* Использовать сценарий PowerShell hello Simulation/Factory/Remove-SimulationPublicIp.ps1 из hello [репозитория](https://github.com/Azure/azure-iot-connected-factory). Передайте имя развертывания в качестве параметра. Для локального развертывания используйте имя `<your username>ConnFactoryLocal`. сценарий Hello выводит hello IP-адрес hello виртуальной Машины.

* Найдите группы ресурсов hello развертывания hello портал Azure. За исключением локальное развертывание группа ресурсов hello имеет hello имя, указанное в качестве решения или развертывания. Для локального развертывания, с помощью скрипта построения hello, hello имя группы ресурсов hello — `<your username>ConnFactoryLocal`. Теперь удалите hello **общедоступный IP-адрес** ресурс из группы ресурсов hello.

### <a name="how-do-i-sign-in-toohello-simulation-vm"></a>Как вход toohello моделирование виртуальных Машин?

Вход toohello симуляции виртуальной Машины поддерживается только при развертывании решения с помощью сценария PowerShell hello `build.ps1` в hello [репозитория](https://github.com/Azure/azure-iot-connected-factory).

При развертывании решения hello из www.azureiotsuite.com не удается войти в toohello виртуальной Машины. Вход невозможен, так как hello пароль формируется случайным образом и не может выполнить его сброс.

1. Добавьте открытый IP адрес toohello виртуальной Машины. В разделе [как добавить открытый toohello моделирование IP адрес виртуальной Машины?](#how-do-i-remove-the-public-ip-address-to-the-simulation-vm)
1. Создание tooyour сеансу SSH виртуальной Машины с помощью IP-адрес hello hello виртуальной Машины.
1. — имя пользователя toouse Hello: `docker`.
1. пароль toouse Hello зависит от версии hello используемых toodeploy:
    * Решения, развертываемого с помощью сценария build.ps1 hello до 1 июня 2017 г., является hello пароль: `Passw0rd`.
    * Для решения, развертываемого с помощью сценария build.ps1 hello после 1 июня 2017 г., можно найти пароль hello в hello `<name of your deployment>.config.user` файла. Hello пароль хранится в hello **VmAdminPassword** параметр. Hello пароль формируется случайным образом во время развертывания если она не указана с помощью hello `build.ps1` параметра сценария`-VmAdminPassword`

### <a name="how-do-i-stop-and-start-all-docker-processes-in-hello-simulation-vm"></a>Как остановка и запуск всех процессов docker в hello моделирование виртуальных Машин?

1. Войдите в toohello симуляции виртуальной Машины. В разделе [как входить в toohello моделирование виртуальных Машин?](#how-do-i-sign-in-to-the-simulation-vm)
1. toocheck какие контейнеры являются активными, запустите: `docker ps`.
1. Запустите все контейнеры моделирование toostop: `./stopsimulation`.
1. toostart все контейнеры моделирования:
    * Экспорт оболочки переменная с именем hello **IOTHUB_CONNECTIONSTRING**. Используйте значение hello hello **IotHubOwnerConnectionString** в hello `<name of your deployment>.config.user` файла. Например:

        ```
        export IOTHUB_CONNECTIONSTRING="HostName={yourdeployment}.azure-devices.net;SharedAccessKeyName=iothubowner;SharedAccessKey={your key}"
        ```

    * Запустите `./startsimulation`.

### <a name="how-do-i-update-hello-simulation-in-hello-vm"></a>Как обновить имитации hello в hello виртуальной Машины?

Если моделирование toohello были внесены изменения, можно использовать сценарий PowerShell hello `build.ps1` в hello [репозитория](https://github.com/Azure/azure-iot-connected-factory) с помощью hello `updatedimulation` команды. Этот сценарий выполняет построение всех компонентов моделирование hello, останавливает имитации hello в hello виртуальной Машины, передает, устанавливает и запускает их.

### <a name="how-do-i-find-out-hello-connection-string-of-hello-iot-hub-used-by-my-solution"></a>Как узнать строка подключения hello центра IoT hello, используемые Мое решение?

При развертывании решения с hello `build.ps1` сценарий в hello [репозитория](https://github.com/Azure/azure-iot-connected-factory), строка соединения hello будет значение hello **IotHubOwnerConnectionString** в hello `<name of your deployment>.config.user` файла.

Также можно найти hello строки соединения, использующей hello портал Azure. Hello центра IoT ресурсов в группе ресурсов hello развертывания найдите hello параметров строки соединения.

### <a name="which-iot-hub-devices-does-hello-connected-factory-simulation-use"></a>Какие устройства центра IoT hello подключенных фабрики, используются моделирования?

Здравствуйте моделирование регистрирует себя hello следующие устройства:

* proxy.beijing.corp.contoso;
* proxy.capetown.corp.contoso;
* proxy.mumbai.corp.contoso;
* proxy.munich0.corp.contoso;
* proxy.rio.corp.contoso;
* proxy.seattle.corp.contoso;
* publisher.beijing.corp.contoso;
* publisher.capetown.corp.contoso;
* publisher.mumbai.corp.contoso;
* publisher.munich0.corp.contoso;
* publisher.rio.corp.contoso;
* publisher.seattle.corp.contoso.

С помощью hello [DeviceExplorer](https://github.com/Azure/azure-iot-sdk-csharp/tree/master/tools/DeviceExplorer) или [explorer центром IOT](https://github.com/azure/iothub-explorer) средство, вы можете проверить, какие устройства регистрируются с помощью решения центром IoT hello. toouse этих средств, необходима строка подключения hello центра IoT hello в развертывании.

### <a name="how-can-i-get-log-data-from-hello-simulation-components"></a>Получение данных журнала из компонентов моделирование hello

Все компоненты в имитационной hello вести журнал в файлах toolog. Эти файлы можно найти в hello виртуальной Машины в папке hello `home/docker/Logs`. журналы hello tooretrieve, можно использовать сценарий PowerShell hello `Simulation/Factory/Get-SimulationLogs.ps1` в hello [репозитория](https://github.com/Azure/azure-iot-connected-factory).

Этот скрипт должен toosign в toohello виртуальной Машины. Может потребоваться tooprovide учетные данные для входа в hello. В разделе [как входить в имитационной toohello ВМ?](#how-do-i-sign-in-to-the-simulation-vm) учетные данные toofind hello.

сценарий Hello добавляет и удаляет открытый IP адрес toohello виртуальной Машины, если он еще не имеют одно и удаляет его. сценарий Hello помещает все файлы журналов в архив и загружает рабочей станции разработки tooyour архив hello.

Можно также войти toohello виртуальной Машины по протоколу SSH и проверять hello файлы журнала во время выполнения.

### <a name="how-can-i-check-if-hello-simulation-is-sending-data-toohello-cloud"></a>Как проверить, если моделирование hello отправляет облако toohello данных?

С hello [DeviceExplorer](https://github.com/Azure/azure-iot-sdk-csharp/tree/master/tools/DeviceExplorer) или hello [explorer центром IOT](https://github.com/azure/iothub-explorer) средство, вы можете проверить hello данные, отправленные tooIoT концентратора с определенными устройствами. toouse этих средств, необходима строка подключения tooknow hello центра IoT hello в развертывании. В разделе [как узнать строка подключения hello центра IoT hello, используемые Мое решение?](#how-do-i-find-out-the-connection-string-of-the-iot-hub-used-by-my-solution)

Проверьте hello данные, посланные с любого устройства hello издателя:

* publisher.beijing.corp.contoso;
* publisher.capetown.corp.contoso;
* publisher.mumbai.corp.contoso;
* publisher.munich0.corp.contoso;
* publisher.rio.corp.contoso;
* publisher.seattle.corp.contoso.

Если вы видите данные не отправляются tooIoT концентратора, наличии проблемы с моделирование hello. В качестве первого шага анализа следует проанализировать файлы журнала hello hello моделирование компонентов. В разделе [как получить данные журнала из hello моделирование компоненты?](#how-can-i-get-log-data-from-the-simulation-components) Затем повторите toostop и запустить моделирование hello и если по-прежнему нет данные, отправляемые, обновить моделирование hello полностью. В разделе [как обновить имитации hello в hello виртуальной Машины?](#how-do-i-update-the-simulation-in-the-vm)

### <a name="next-steps"></a>Дальнейшие действия

Можно также изучить некоторые hello и другие возможности hello IoT Suite предварительно настроенных решений:

* [Обзор предварительно настроенного решения прогнозируемого обслуживания](iot-suite-predictive-overview.md)
* [Начало работы с предварительно настроенным решением для подключенной фабрики](iot-suite-connected-factory-overview.md)
* [Основание безопасности IoT из hello,](securing-iot-ground-up.md)
