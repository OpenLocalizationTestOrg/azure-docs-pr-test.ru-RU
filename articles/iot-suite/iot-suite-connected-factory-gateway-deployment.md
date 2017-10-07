---
title: "подключение к Azure IoT Suite aaaDeploy фабрики шлюза | Документы Microsoft"
description: "Способ toodeploy шлюз в Windows или Linux toohello подключения tooenable подключения фабрики предварительно настроенных решений."
services: 
suite: iot-suite
documentationcenter: na
author: dominicbetts
manager: timlt
editor: 
ms.service: iot-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/24/2017
ms.author: dobett
ms.openlocfilehash: 72436dec60eda0de20143f362fe740b0c4412f36
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-gateway-on-windows-or-linux-for-hello-connected-factory-preconfigured-solution"></a>Развертывание шлюза в Windows или Linux для hello подключен фабрики предварительно настроенных решений

Hello программного обеспечения требуемые toodeploy a шлюз для hello подключен фабрики предварительно настроенное решение состоит из двух компонентов:

* Hello *прокси OPC* устанавливает tooIoT подключение концентратора. Hello *прокси OPC* затем ожидает команды и управления сообщения от hello интеграции OPC браузер, в котором выполняется решение портала hello подключенных фабрики.
* Hello *издатель OPC* подключается tooexisting локальных OPC UA серверов и перенаправляет сообщения телеметрии из них tooIoT концентратора.

Оба компонента имеют открытый исходный код и доступны в виде файлов с исходным кодом на GitHub и в качестве контейнеров Docker:

| GitHub | DockerHub |
| ------ | --------- |
| [Издатель OPC][lnk-publisher-github] | [Издатель OPC][lnk-publisher-docker] |
| [Прокси-сервер OPC][lnk-proxy-github] | [Прокси-сервер OPC][lnk-proxy-docker] |

Нет общедоступный IP-адрес или уязвимости в брандмауэре шлюза hello необходимы для любого компонента. Hello OPC прокси-сервер и издатель OPC используют только исходящие порты 443, 5671 и 8883.

Hello действия, описанные в этой статье показано, как toodeploy a шлюз с помощью Docker на либо [Windows](#windows-deployment) или [Linux](#linux-deployment). шлюз Hello позволяет подключения toohello подключен фабрики предварительно настроенных решений.

> [!NOTE]
> программное обеспечение шлюза Hello, работающего в контейнер Docker hello [Azure IoT Edge].

## <a name="windows-deployment"></a>Развертывание в ОС Windows

> [!NOTE]
> Если у вас еще нет устройства шлюза, то корпорация Майкрософт рекомендует приобрести коммерческий шлюз у одного из наших партнеров. Посетите hello [каталога устройства Azure IoT] список шлюза устройств, совместимых с hello подключен фабрики решения. Следуйте инструкциям hello, входящие в состав tooset устройства hello Создание шлюза hello. Кроме того можно используйте следующие инструкции toomanually настроить один из шлюзов существующих hello.

### <a name="install-docker"></a>Установка Docker

Установите [Docker для Windows] на устройстве шлюза, работающем под управлением Windows. Во время установки Windows Docker выберите накопитель на tooshare машины на узле с помощью Docker. Следующий снимок экрана показан общий доступ к диску hello D в системе Windows Hello:

![Установка Docker][img-install-docker]

Затем создайте папку с именем **docker** в корне hello hello общий диск.
Кроме того, этот этап можно выполнить после установки docker из hello **параметры** меню.

### <a name="configure-hello-gateway"></a>Настройка шлюза hello

1. Требуется hello **iothubowner** строка подключения к Azure IoT Suite подключен развертывания шлюза hello toocomplete развертывания фабрики. В hello [портал Azure], перейдите в центр IoT в группе ресурсов hello, созданные при развертывании решения фабрики hello подключен tooyour. Нажмите кнопку **политики общего доступа** tooaccess hello **iothubowner** строка подключения:

    ![Найти строку подключения центр IoT hello][img-hub-connection]

    Копировать hello **строка подключения — первичный ключ** значение.

1. Настройка шлюза hello для вашего центра IoT, выполнив hello двух модулей шлюза **после** из командной строки с помощью:

    `docker run -it --rm -h <ApplicationName> -v //D/docker:/build/src/GatewayApp.NetCore/bin/Debug/netcoreapp1.0/publish/CertificateStores -v //D/docker:/root/.dotnet/corefx/cryptography/x509stores microsoft/iot-gateway-opc-ua:1.0.0 <ApplicationName> "<IoTHubOwnerConnectionString>"`

    `docker run -it --rm -v //D/docker:/mapped microsoft/iot-gateway-opc-ua-proxy:0.1.3 -i -c "<IoTHubOwnerConnectionString>" -D /mapped/cs.db`

    * **&lt;ApplicationName&gt;**  — tooyour toogive hello имя издателя OPC агент пользователя в формате hello **издателя.&lt; свое полное доменное имя&gt;**. Например, если фабрика сети называется **myfactorynetwork.com**, hello **ApplicationName** значение **publisher.myfactorynetwork.com**.
    * **&lt;IoTHubOwnerConnectionString&gt;**  — hello **iothubowner** строку подключения, скопированным на предыдущем шаге hello. Эта строка подключения используется только на этом шаге, он не нужен в hello следующие шаги:

    Вы используете hello сопоставленный диск D:\\папку docker (hello `-v` аргумент) более поздней версии toopersist hello двух сертификатов X.509, использующих модули шлюза hello.

### <a name="run-hello-gateway"></a>Запустите шлюз hello

1. Перезапустите шлюз hello, с помощью hello, следующие команды:

    `docker run -it --rm -h <ApplicationName> --expose 62222 -p 62222:62222 -v //D/docker:/build/src/GatewayApp.NetCore/bin/Debug/netcoreapp1.0/publish/Logs -v //D/docker:/build/src/GatewayApp.NetCore/bin/Debug/netcoreapp1.0/publish/CertificateStores -v //D/docker:/shared -v //D/docker:/root/.dotnet/corefx/cryptography/x509stores -e _GW_PNFP="/shared/publishednodes.JSON" microsoft/iot-gateway-opc-ua:1.0.0 <ApplicationName>`

    `docker run -it --rm -v //D/docker:/mapped microsoft/iot-gateway-opc-ua-proxy:0.1.3 -D /mapped/cs.db`

1. По соображениям безопасности hello двух сертификатов X.509 сохраняется в hello D:\\папку docker содержит hello закрытого ключа. Ограничение доступа к папке toothis toohello, учетные данные (обычно **Администраторы**) использовать контейнер Docker toorun hello. Щелкните правой кнопкой мыши hello D:\\папку docker выберите **свойства**, затем **безопасности**, а затем **изменить**. Предоставьте **администраторам** полный доступ и удалите всех остальных:

    ![Предоставление разрешений tooDocker папки][img-docker-share]

1. Проверьте сетевое подключение. В командной строке введите команду hello `ping publisher.<your fully qualified domain name>` tooping шлюза. Если hello назначения недоступен, добавьте hello IP-адрес и имя файла hosts toohello шлюза на шлюзе. файл hosts Hello находится в hello **Windows\\System32\\драйверы\\и т. д** папки.

1. После этого повторите tooconnect toohello издателя с помощью локального OPC агент пользователя клиента, запущенного на шлюз hello. Здравствуйте, OPC UA-адрес конечной точки `opc.tcp://publisher.<your fully qualified domain name>:62222`. Если у вас нет клиента OPC UA, скачайте и используйте [клиент OPC UA с открытым кодом].

1. Когда эти локальные тесты успешно завершена, Обзор toohello **подключения сервер UA OPC** hello подключенных фабрики решение портала. Введите URL-адрес конечной точки издателя hello (`tcp://publisher.<your fully qualified domain name>:62222`) и нажмите кнопку **Connect**. После отображения предупреждения о сертификате щелкните **Продолжить**. Далее вы получаете сообщение об этом hello hello UA веб-клиента не является доверенным издателем. tooresolve этой ошибки, hello копирования **веб-агент пользователя клиента** сертификат из hello **D:\\docker\\отклонено сертификаты\\сертификаты** папки toohello **D:\\docker\\приложений UA\\сертификаты** папки на шлюзе hello. Toorestart hello шлюза не обязательно. Повторите этот шаг. Шлюз toohello теперь можно подключиться из облака hello и будут готовы tooadd решения toohello серверы OPC UA.

### <a name="add-your-opc-ua-servers"></a>Добавление серверов OPC UA

1. Обзор toohello **подключения сервер UA OPC** hello подключенных фабрики решение портала. Выполните приветствия же действия, как предшествующий tooestablish раздел hello доверие между hello портала подключенных фабрики и hello server OPC UA. Этот шаг устанавливает взаимного доверия сертификатов hello из hello подключен портала фабрики и hello OPC UA server и создает подключение.

1. Обзор hello дерева узлов OPC UA OPC UA сервера, щелкните правой кнопкой мыши узлы OPC hello и выберите **публикации**. Для публикации toowork таким образом, hello OPC UA сервера и hello издатель должен быть на hello одной сети. Другими словами, если hello полное доменное имя домена hello издателя — **publisher.mydomain.com** hello полное доменное имя hello OPC UA сервер должен быть, например, а затем **myopcuaserver.mydomain.com**. Если настройки отличаются, можно вручную добавить узлы toohello publishesnodes.json файл, находящийся в hello **D:\\docker** папки. Hello publishesnodes.json файл создается автоматически на hello сначала успешной публикации узла OPC.

1. Данные телеметрии, направляемые из устройства шлюза hello. Можно просмотреть данные телеметрии hello в hello **расположения фабрики** представление портала подключенных фабрики hello в разделе **новую фабрику**.

## <a name="linux-deployment"></a>Развертывание в ОС Linux

> [!NOTE]
> Если у вас еще нет устройства шлюза, то корпорация Майкрософт рекомендует приобрести коммерческий шлюз у одного из наших партнеров. Посетите hello [каталога устройства Azure IoT] список шлюза устройств, совместимых с hello подключен фабрики решения. Следуйте инструкциям hello, входящие в состав tooset устройства hello Создание шлюза hello. Кроме того можно используйте следующие инструкции toomanually настроить один из шлюзов существующих hello.

[Установите Docker] на устройстве шлюза, работающем под управлением Linux.

### <a name="configure-hello-gateway"></a>Настройка шлюза hello

1. Требуется hello **iothubowner** строка подключения к Azure IoT Suite подключен развертывания шлюза hello toocomplete развертывания фабрики. В hello [портал Azure], перейдите в центр IoT в группе ресурсов hello, созданные при развертывании решения фабрики hello подключен tooyour. Нажмите кнопку **политики общего доступа** tooaccess hello **iothubowner** строка подключения:

    ![Найти строку подключения центр IoT hello][img-hub-connection]

    Копировать hello **строка подключения — первичный ключ** значение.

1. Настройка шлюза hello для вашего центра IoT, выполнив hello двух модулей шлюза **после** из оболочки с:

    `sudo docker run -it --rm -h <ApplicationName> -v /shared:/build/src/GatewayApp.NetCore/bin/Debug/netcoreapp1.0/publish/ -v /shared:/root/.dotnet/corefx/cryptography/x509stores microsoft/iot-gateway-opc-ua:1.0.0 <ApplicationName> "<IoTHubOwnerConnectionString>"`

    `sudo docker run --rm -it -v /shared:/mapped microsoft/iot-gateway-opc-ua-proxy:0.1.3 -i -c "<IoTHubOwnerConnectionString>" -D /mapped/cs.db`

    * **&lt;ApplicationName&gt;**  — имя hello hello создает OPC UA приложения hello шлюза в формате hello **издателя.&lt; свое полное доменное имя&gt;**. Например, **publisher.microsoft.com**.
    * **&lt;IoTHubOwnerConnectionString&gt;**  — hello **iothubowner** строку подключения, скопированным на предыдущем шаге hello. Эта строка подключения используется только на этом шаге, он не нужен в hello следующие шаги:

    Использовать hello **/ shared** папку (hello `-v` аргумент) двух сертификатов X.509, использующих модули шлюза hello hello toopersist более поздней версии.

### <a name="run-hello-gateway"></a>Запустите шлюз hello

1. Перезапустите шлюз hello, с помощью hello, следующие команды:

    `sudo docker run -it -h <ApplicationName> --expose 62222 -p 62222:62222 –-rm -v /shared:/build/src/GatewayApp.NetCore/bin/Debug/netcoreapp1.0/publish/Logs -v /shared:/build/src/GatewayApp.NetCore/bin/Debug/netcoreapp1.0/publish/CertificateStores -v /shared:/shared -v /shared:/root/.dotnet/corefx/cryptography/x509stores -e _GW_PNFP="/shared/publishednodes.JSON" microsoft/iot-gateway-opc-ua:1.0.0 <ApplicationName>`

    `sudo docker run -it -v /shared:/mapped microsoft/iot-gateway-opc-ua-proxy:0.1.3 -D /mapped/cs.db`

1. По соображениям безопасности hello двух сертификатов X.509 сохраняется в hello **/ shared** папки содержит hello закрытого ключа. Ограничение доступа toothis папки toohello учетные данные, используемые toorun hello контейнера Docker. разрешения hello tooset для **корневой** только использовать hello `chmod` команде hello папки оболочки.

1. Проверьте сетевое подключение. Из оболочки, введите команду hello `ping publisher.<your fully qualified domain name>` tooping шлюза. Если hello назначения недоступен, добавьте hello IP-адрес и имя файла hosts tooyour шлюза на шлюзе. файл hosts Hello находится в hello **и т. п.** папки.

1. После этого повторите tooconnect toohello издателя с помощью локального OPC агент пользователя клиента, запущенного на шлюз hello. Здравствуйте, OPC UA-адрес конечной точки `opc.tcp://publisher.<your fully qualified domain name>:62222`. Если у вас нет клиента OPC UA, скачайте и используйте [клиент OPC UA с открытым кодом].

1. Когда эти локальные тесты успешно завершена, Обзор toohello **подключения сервер UA OPC** hello подключенных фабрики решение портала. Введите URL-адрес конечной точки издателя hello (`tcp://publisher.<your fully qualified domain name>:62222`) и нажмите кнопку **Connect**. После отображения предупреждения о сертификате щелкните **Продолжить**. Далее вы получаете сообщение об этом hello hello UA веб-клиента не является доверенным издателем. tooresolve этой ошибки, hello копирования **веб-агент пользователя клиента** сертификат из hello **/общие/отклонено сертификаты и сертификаты** toohello папки **/shared/UA приложения и сертификаты** Папка на шлюзе hello. Toorestart hello шлюза не обязательно. Повторите этот шаг. Шлюз toohello теперь можно подключиться из облака hello и будут готовы tooadd решения toohello серверы OPC UA.

### <a name="add-your-opc-ua-servers"></a>Добавление серверов OPC UA

1. Обзор toohello **подключения сервер UA OPC** hello подключенных фабрики решение портала. Выполните приветствия же действия, как предшествующий tooestablish раздел hello доверие между hello портала подключенных фабрики и hello server OPC UA. Этот шаг устанавливает взаимного доверия сертификатов hello из hello подключен портала фабрики и hello OPC UA server и создает подключение.

1. Обзор hello дерева узлов OPC UA OPC UA сервера, щелкните правой кнопкой мыши узлы OPC hello и выберите **публикации**. Для публикации toowork таким образом, hello OPC UA сервера и hello издатель должен быть на hello одной сети. Другими словами, если hello полное доменное имя домена hello издателя — **publisher.mydomain.com** hello полное доменное имя hello OPC UA сервер должен быть, например, а затем **myopcuaserver.mydomain.com**. Если настройки отличаются, можно вручную добавить узлы toohello publishesnodes.json файл, находящийся в hello **/ shared** папки. Hello publishesnodes.json создается автоматически на hello сначала успешной публикации узла OPC.

1. Данные телеметрии, направляемые из устройства шлюза hello. Можно просмотреть данные телеметрии hello в hello **расположения фабрики** представление портала подключенных фабрики hello в разделе **новую фабрику**.

## <a name="next-steps"></a>Дальнейшие действия

toolearn больше об архитектуре hello подключенных фабрики hello предварительно настроенных решений см. в разделе [подключенных фабрики заранее настроенные Пошаговое руководство по решениям][lnk-walkthrough].

[img-install-docker]: ./media/iot-suite-connected-factory-gateway-deployment/image1.png
[img-hub-connection]: ./media/iot-suite-connected-factory-gateway-deployment/image2.png
[img-docker-share]: ./media/iot-suite-connected-factory-gateway-deployment/image3.png

[Docker для Windows]: https://www.docker.com/docker-windows
[каталога устройства Azure IoT]: https://catalog.azureiotsuite.com/?q=opc
[портал Azure]: http://portal.azure.com/
[клиент OPC UA с открытым кодом]: https://github.com/OPCFoundation/UA-.NETStandardLibrary/tree/master/SampleApplications/Samples/Client.Net4
[Установите Docker]: https://www.docker.com/community-edition#/download
[lnk-walkthrough]: iot-suite-connected-factory-sample-walkthrough.md
[Azure IoT Edge]: https://github.com/Azure/iot-edge (Edge Интернета вещей Azure)

[lnk-publisher-github]: https://github.com/Azure/iot-edge-opc-publisher
[lnk-publisher-docker]: https://hub.docker.com/r/microsoft/iot-gateway-opc-ua
[lnk-proxy-github]: https://github.com/Azure/iot-edge-opc-proxy
[lnk-proxy-docker]: https://hub.docker.com/r/microsoft/iot-gateway-opc-ua-proxy