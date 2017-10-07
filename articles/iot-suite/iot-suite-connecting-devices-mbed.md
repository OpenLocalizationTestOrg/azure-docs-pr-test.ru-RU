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
# <a name="connect-your-device-toohello-remote-monitoring-preconfigured-solution-mbed"></a>Подключения на устройстве toohello удаленное наблюдение предварительно настроенных решений (mbed)

## <a name="scenario-overview"></a>Обзор сценария
В этом случае создайте устройство, которое отправляет hello следующие удаленный мониторинг телеметрии toohello [предварительно настроенное решение][lnk-what-are-preconfig-solutions]:

* наружная температура;
* внутренняя температура;
* влажность.

Для простоты кода hello на устройстве hello приводит к возникновению ошибки образцы значений, но мы рекомендуем вам tooextend hello образец подключение устройства tooyour реальные датчиков и отправки реальные данные телеметрии.

Hello устройство будет также может toorespond toomethods из панели мониторинга решения hello и требуемого значения свойств, заданные в панели мониторинга hello решения.

toocomplete этого учебника требуется активная учетная запись Azure. Если ее нет, можно создать бесплатную пробную учетную запись всего за несколько минут. Дополнительные сведения см. в статье о [бесплатной пробной версии Azure][lnk-free-trial].

## <a name="before-you-start"></a>Перед началом работы
До написания кода для устройства необходимо подготовить свое предварительно настроенное решение для удаленного мониторинга, а затем подготовить в нем новое пользовательское устройство.

### <a name="provision-your-remote-monitoring-preconfigured-solution"></a>Подготовка предварительно настроенного решения для удаленного мониторинга
устройство Hello, создан в этом учебнике отправляет экземпляра tooan данных hello [удаленный мониторинг] [ lnk-remote-monitoring] предварительно настроенных решений. Если это еще не было предоставлено hello удаленное наблюдение предварительно настроенных решений в вашей учетной записью Azure, используйте hello следующие шаги:

1. На hello <https://www.azureiotsuite.com/> щелкните  **+**  toocreate решения.
2. Нажмите кнопку **выберите** на hello **удаленный мониторинг** панели toocreate решения.
3. На hello **создания удаленного решением для мониторинга** введите **имя решения** по своему усмотрению выберите hello **область** toodeploy для и выберите hello Azure toouse toowant подписки. Затем щелкните **Создать решение**.
4. Дождитесь завершения процесса подготовки hello.

> [!WARNING]
> предварительно настроенное Hello решения используют оплаты служб Azure. Убедитесь, что tooremove hello предварительно настроенных решений из подписки, когда вы завершили работу с ним tooavoid все ненужные расходы. Можно полностью удалить предварительно настроенных решений из подписки, перейдя по адресу hello <https://www.azureiotsuite.com/> страницы.
> 
> 

После завершения процесса для hello удаленного решением для мониторинга инициализации hello, нажмите кнопку **запуска** tooopen hello решения и панели мониторинга в браузере.

![Панель мониторинга решения][img-dashboard]

### <a name="provision-your-device-in-hello-remote-monitoring-solution"></a>Подготовка устройства в hello удаленного решением для мониторинга
> [!NOTE]
> Если вы уже подготовили устройство в решении, пропустите этот шаг. Необходимы учетные данные устройства hello tooknow, при создании клиентского приложения hello.
> 
> 

Для решения tooconnect toohello предварительно настроенных устройств, он должен идентифицировать себя tooIoT концентратора используя действительные учетные данные. Учетные данные устройства hello можно извлечь из панели мониторинга hello решения. Включать учетные данные устройства hello в клиентском приложении, далее в этом учебнике.

tooadd tooyour удаленного мониторинга устройствами завершения hello следующие шаги на панели мониторинга hello решения:

1. В hello левом нижнем углу панели мониторинга hello, щелкните **добавить устройство**.
   
   ![Добавление устройства][1]
2. В hello **пользовательских устройств** нажмите кнопку **добавить новую**.
   
   ![Добавление пользовательского устройства][2]
3. Установите переключатель **Позвольте мне определить собственный идентификатор устройства**. Введите идентификатор устройства, например **mydevice**, нажмите кнопку **проверить идентификатор** tooverify таким именем еще не используется и нажмите кнопку **создать** tooprovision hello устройства.
   
   ![Добавление идентификатора устройства][3]
4. Перевести устройство hello Примечание учетные данные (идентификатор устройства, имя узла концентратора IoT и ключ устройства). Клиент приложению эти значения tooconnect toohello удаленного решением для мониторинга. Затем нажмите кнопку **Done**(Готово).
   
    ![Просмотр учетных данных устройства][4]
5. Выберите устройство в списке устройств hello в панель мониторинга hello решения. Затем в hello **сведений об устройстве** нажмите кнопку **включить устройство**. Теперь задано состояние Hello устройства **под управлением**. решение для удаленного мониторинга Hello теперь можно получать данные телеметрии с устройства и вызова методов на устройстве hello.

[img-dashboard]: ./media/iot-suite-connecting-devices-mbed/dashboard.png
[1]: ./media/iot-suite-connecting-devices-mbed/suite0.png
[2]: ./media/iot-suite-connecting-devices-mbed/suite1.png
[3]: ./media/iot-suite-connecting-devices-mbed/suite2.png
[4]: ./media/iot-suite-connecting-devices-mbed/suite3.png

[lnk-what-are-preconfig-solutions]: iot-suite-what-are-preconfigured-solutions.md
[lnk-remote-monitoring]: iot-suite-remote-monitoring-sample-walkthrough.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/

## <a name="build-and-run-hello-c-sample-solution"></a>Постройте и запустите решение образца hello C

Hello следующие инструкции описывают hello инструкции по подключению [поддержкой mbed Freescale FRDM-K64F] [ lnk-mbed-home] toohello устройства удаленного решением для мониторинга.

### <a name="connect-hello-mbed-device-tooyour-network-and-desktop-machine"></a>Подключение сети tooyour устройств mbed hello и настольном компьютере

1. Подключите hello mbed устройства tooyour сети с помощью кабеля Ethernet. Этот шаг необходим, так как пример приложения hello требуется доступ к Интернету.

1. В разделе [Приступая к работе с mbed] [ lnk-mbed-getstarted] tooconnect рабочего стола tooyour устройства mbed ПК.

1. Если для настольного компьютера работает под управлением Windows, см. раздел [конфигурации ПК] [ lnk-mbed-pcconnect] tooconfigure последовательного порта tooyour mbed доступа.

### <a name="create-an-mbed-project-and-import-hello-sample-code"></a>Создайте проект mbed и импортировать hello образец кода

Выполните эти шаги tooadd некоторые tooan mbed образец кода проекта. Импорт hello удаленного мониторинга начальный проект и измените hello проекта toouse hello протокола MQTT вместо hello протокола AMQP. В настоящее время необходимо toouse hello MQTT протокола toouse hello функции управления устройствами центра IoT.

1. В веб-браузере перейдите toohello mbed.org [сайта разработчика](https://developer.mbed.org/). Если вы еще не зарегистрировались, можно увидеть toocreate параметр учетной записи (бесплатно). Если учетная запись есть, используйте ее для входа. Нажмите кнопку **компилятора** в верхнем правом углу hello страницы приветствия. Это действие переводит toohello *рабочей* интерфейса.

1. Убедитесь, что аппаратную платформу hello, которую вы используете отображается в верхнем правом углу hello окна hello, или щелкните значок hello в правом углу tooselect hello Аппаратная платформа.

1. Нажмите кнопку **импорта** главного меню hello. Нажмите кнопку **tooimport с URL-адреса щелкните здесь**.
   
    ![Запустить рабочую область toombed импорта][6]

1. Во всплывающем окне приветствия, введите ссылку hello https://developer.mbed.org/users/AzureIoTClient/code/remote_monitoring/ кода образца hello, а затем нажмите кнопку **импорта**.
   
    ![Импорт рабочей toombed образец кода][7]

1. В окно компилятора mbed hello можно увидеть, что импорт этого проекта также импортирует различные библиотеки. Некоторые предоставляются и обслуживается hello Azure IoT team ([azureiot_common](https://developer.mbed.org/users/AzureIoTClient/code/azureiot_common/), [iothub_client](https://developer.mbed.org/users/AzureIoTClient/code/iothub_client/), [iothub_amqp_transport](https://developer.mbed.org/users/AzureIoTClient/code/iothub_amqp_transport/), [azure_uamqp](https://developer.mbed.org/users/AzureIoTClient/code/azure_uamqp/)), а другие представляют собой сторонних библиотек, доступных в каталоге библиотеки mbed hello.
   
    ![Просмотр проекта mbed][8]

1. В hello **рабочей программы**, щелкните правой кнопкой мыши hello **центром IOT\_amqp\_транспорта** библиотеки, нажмите кнопку **удалить**и нажмите кнопку **ОК** tooconfirm.

1. В hello **рабочей программы**, щелкните правой кнопкой мыши hello **azure\_amqp\_c** библиотеки, нажмите кнопку **удалить**и нажмите кнопку **ОК**  tooconfirm.

1. Hello щелкните правой кнопкой мыши **remote_monitoring** проекта в hello **рабочей программы**выберите **библиотека импорта**, а затем выберите **URL-адрес из**.
   
    ![Запуск рабочей toombed библиотеки импорта][6]

1. Во всплывающем окне приветствия, введите ссылку hello транспорта библиотеки hello MQTT https://developer.mbed.org/users/AzureIoTClient/code/iothub\_mqtt\_транспорта и затем щелкните **импорта**.
   
    ![Импорт рабочей toombed библиотеки][12]

1. Повторите hello предыдущего шага tooadd hello MQTT библиотеки из https://developer.mbed.org/users/AzureIoTClient/code/azure\_umqtt\_c /.

1. Рабочую область теперь выглядит hello следующим образом:

    ![Просмотр рабочей области mbed][13]

1. Откройте hello удаленного\_monitoring\remote_monitoring.c файл и замените существующие hello `#include` инструкции с hello, следующий код:

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
1. Удалить все hello, остальной код в удаленном hello\_monitoring\remote\_monitoring.c файла.

[!INCLUDE [iot-suite-connecting-code](../../includes/iot-suite-connecting-code.md)]

## <a name="build-and-run-hello-sample"></a>Построение и запуск образца hello

Добавить код hello tooinvoke **удаленного\_мониторинга\_запуска** функции и затем постройте и запустите приложение hello устройства.

1. Добавить **основной** функции следующий код в конце hello hello удаленного\_monitoring.c файл tooinvoke hello **удаленного\_мониторинг\_запуска** функции:
   
    ```c
    int main()
    {
      remote_monitoring_run();
      return 0;
    }
    ```

1. Нажмите кнопку **компиляции** toobuild hello программы. Можно спокойно игнорировать любые предупреждения, но если hello сборки приводит к возникновению ошибки, исправить их перед продолжением.

1. При успешном построении hello веб-сайт компилятора hello mbed приводит к возникновению ошибки Bin-файл с именем hello проекта и загружает его tooyour локального компьютера. Скопируйте файл toohello hello .bin устройства. Сохранение файла toohello hello .bin устройство вызывает toorestart hello устройства и запустите программу hello, содержащихся в hello Bin-файл. Программа hello можно перезапустить вручную в любое время, нажав кнопку "сбросить" hello на устройстве mbed hello.

1. Подключите устройство toohello, с помощью клиентского приложения SSH, например PuTTY. Можно определить hello последовательного порта, используемого устройства, проверьте в диспетчере устройств Windows.
   
    ![][11]

1. В PuTTY, щелкните hello **последовательной** тип подключения. обычно подключается устройство Hello в 9600 бод, поэтому введите 9600 в hello **скорость** поле. Затем щелкните **Открыть**.

1. Программа Hello запускает выполнение. Если hello программа не запускается автоматически при подключении могут возникнуть tooreset hello доски (нажмите CTRL + Break или кнопки сброса клавишу hello доски).
   
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
