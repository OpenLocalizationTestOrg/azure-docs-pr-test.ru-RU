---
title: "Подготовка имитированного устройства X.509 в Центре Интернета вещей Azure с помощью Java | Документация Майкрософт"
description: "Краткое руководство Azure. Создание и подготовка имитированного устройства X.509 с помощью пакета Java SDK для службы подготовки устройств Центра Интернета вещей"
services: iot-dps
keywords: 
author: msebolt
ms.author: v-masebo
ms.date: 12/21/2017
ms.topic: quickstart
ms.service: iot-dps
documentationcenter: 
manager: timlt
ms.devlang: java
ms.custom: mvc
ms.openlocfilehash: 508df6e7c677d87c6b893519c59b02880e16d7ec
ms.sourcegitcommit: a648f9d7a502bfbab4cd89c9e25aa03d1a0c412b
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/22/2017
---
# <a name="create-and-provision-a-simulated-x509-device-using-java-device-sdk-for-iot-hub-device-provisioning-service"></a>Создание и подготовка имитированного устройства X.509 с помощью пакета Java SDK для службы подготовки устройств Центра Интернета вещей
> [!div class="op_single_selector"]
> * [C](quick-create-simulated-device-x509.md)
> * [Java](quick-create-simulated-device-x509-java.md)
> * [C#](quick-create-simulated-device-x509-csharp.md)
> * [Python](quick-create-simulated-device-x509-python.md)

В этом руководстве показано, как имитировать устройство X.509 на компьютере разработки под управлением ОС Windows, а также как с помощью примера кода подключить имитированное устройство к службе подготовки устройств и Центру Интернета вещей. 

Прежде чем продолжить, выполните инструкции по [настройке службы подготовки устройств Центра Интернета вещей на портале Azure](./quick-setup-auto-provision.md).


## <a name="prepare-the-environment"></a>Подготовка среды 

1. Убедитесь, что на вашем компьютере установлен [пакет SDK 8 для Java SE](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html).

1. Скачайте и установите [Maven](https://maven.apache.org/install.html).

1. Установите на компьютер систему `git` и добавьте ее в переменные среды, доступные в командном окне. Последнюю версию средств `git` для установки, которая включает **Git Bash**, приложение командной строки для взаимодействия с локальным репозиторием Git, можно найти на [этой странице](https://git-scm.com/download/). 

1. Откройте окно командной строки. Клонируйте репозиторий GitHub для примера кода виртуального устройства:
    
    ```cmd/sh
    git clone https://github.com/Azure/azure-iot-sdk-java.git --recursive
    ```

1. Перейдите к проекту генератора сертификатов и выполните сборку этого проекта. 

    ```cmd/sh
    cd azure-iot-sdk-java/provisioning/provisioning-tools/provisioning-x509-cert-generator
    mvn clean install
    ```

1. Перейдите в целевую папку и запустите созданный JAR-файл.

    ```cmd/sh
    cd target
    java -jar ./provisioning-x509-cert-generator-{version}-with-deps.jar
    ```

1. Создайте сведения о регистрации одним из следующих способов, в зависимости от используемой схемы работы.

    - **Индивидуальная регистрация**.

        1. Введите **N** в ответ на запрос _Do you want to input common name_ (Хотите ли вы ввести общее имя). Скопируйте в буфер обмена выходные данные команды `Client Cert`, начиная со строки *---BEGIN CERTIFICATE---* и заканчивая строкой *-----END CERTIFICATE-----*, включительно.

            ![Генератор отдельного сертификата](./media/java-quick-create-simulated-device-x509/individual.png)

        1. На компьютере с ОС Windows создайте файл **_X509individual.pem_**, откройте его в любом удобном редакторе и скопируйте в него содержимое буфера обмена. Сохраните файл.

        1. Введите **N** в ответ на запрос _Do you want to input Verification Code_ (Хотите ли вы ввести код проверки?) и не закрывайте выходные данные программы, поскольку они понадобятся позднее при работе с этим руководством. Запишите значения _Client Cert_ (Сертификат клиента) и _Client Cert Private Key_ (Закрытый ключ сертификата клиента).
    
    - **Группы регистрации**.

        1. Введите **N** в ответ на запрос _Do you want to input common name_ (Хотите ли вы ввести общее имя). Скопируйте в буфер обмена выходные данные команды `Root Cert`, начиная со строки *---BEGIN CERTIFICATE---* и заканчивая строкой *-----END CERTIFICATE-----*, включительно.

            ![Генератор сертификата группы](./media/java-quick-create-simulated-device-x509/group.png)

        1. На компьютере с ОС Windows создайте файл **_X509group.pem_**, откройте его в любом удобном редакторе и скопируйте в него содержимое буфера обмена. Сохраните файл.

        1. Введите **N** в ответ на запрос _Do you want to input Verification Code_ (Хотите ли вы ввести код проверки?) и не закрывайте окно программы, поскольку оно понадобится позднее при работе с этим руководством. Запишите значения _Client Cert_ (Сертификат клиента), _Client Cert Private Key_ (Закрытый ключ сертификата клиента), _Signer Cert_ (Сертификат подписи) и _Root Cert_ (Корневой сертификат).


## <a name="create-a-device-enrollment-entry"></a>Создание записи о регистрации устройства

1. Войдите на портал Azure, нажмите кнопку **Все ресурсы** в меню слева и откройте службу подготовки.

1. Введите сведения о регистрации одним из следующих способов, в зависимости от используемой схемы работы.

    - **Индивидуальная регистрация**. 

        1. В колонке сводки службы подготовки устройств выберите **Управление регистрациями**. На вкладке **Отдельные регистрации** и нажмите кнопку **Добавить** сверху. 

        1. В разделе **Добавление записи в список регистрации**, введите следующее:
            - Выберите **X.509** как *механизм* аттестации удостоверения.
            - В поле *PEM-файл или CER-файл сертификата* выберите созданный ранее файл сертификата **_X509individual.pem_**, используя мини-приложение *Проводник*.
            - При необходимости можно указать следующие сведения:
                - Выберите Центр Интернета вещей, связанный с вашей службой подготовки.
                - Укажите уникальный идентификатор устройства. Убедитесь, что при назначении имен устройства не используются конфиденциальные данные. 
                - Обновите **начальное состояние двойника устройства**, используя требуемую начальную конфигурацию для устройства.
            - Затем нажмите кнопку **Сохранить**. 

        ![Ввод сведений о регистрации устройства X.509 в колонке портала](./media/java-quick-create-simulated-device-x509/enter-device-enrollment.png)  

       После успешной регистрации устройство X.509 отобразится как **microsoftriotcore** в столбце *Идентификатор регистрации* на вкладке *Индивидуальные регистрации*. 

    - **Группы регистрации**. 

        1. В колонке сводной информации о службе подготовки устройств выберите **Сертификаты** и нажмите кнопку **Добавить** в верхней части экрана.

        1. В разделе **Добавление сертификата** введите следующие данные.
            - Введите уникальное имя сертификата.
            - Выберите ранее созданный файл **_X509group.pem_**.
            - Затем нажмите кнопку **Сохранить**.

        ![Добавление сертификата](./media/java-quick-create-simulated-device-x509/add-certificate.png)

        1. Выберите только что созданный сертификат.
            - Щелкните **Создать код проверки**. Скопируйте созданный код.
            - Введите _код проверки_ или щелкните правой кнопкой мыши в открытом окне _provisioning-x509-cert-generator_, чтобы вставить код.  Нажмите клавишу **ВВОД**.
            - Скопируйте в буфер обмена выходные данные команды `Verification Cert`, начиная со строки *---BEGIN CERTIFICATE---* и заканчивая строкой *-----END CERTIFICATE-----*, включительно.
            
                ![Генератор проверки](./media/java-quick-create-simulated-device-x509/validation-generator.png)

            - На компьютере с ОС Windows создайте файл **_X509validation.pem_**, откройте его в любом удобном редакторе и скопируйте в него содержимое буфера обмена. Сохраните файл.
            - Выберите файл **_X509validation.pem_** на портале Azure. Щелкните **Проверить**.

            ![Проверка сертификата](./media/java-quick-create-simulated-device-x509/validate-certificate.png)

        1. Выберите **Управление регистрациями**. Выберите вкладку **Группы регистрации** и нажмите кнопку **Добавить** вверху.
            - Введите уникальное имя группы.
            - Выберите уникальное имя созданного ранее сертификата.
            - При необходимости можно указать следующие сведения:
                - Выберите Центр Интернета вещей, связанный с вашей службой подготовки.
                - Обновите **начальное состояние двойника устройства**, используя требуемую начальную конфигурацию для устройства.

        ![Ввод сведений о группе регистрации X.509 в колонке портала](./media/java-quick-create-simulated-device-x509/enter-group-enrollment.png)

        После успешной регистрации группа устройств X.509 отображается в столбце *Имя группы* на вкладке *Группы регистрации*.


## <a name="simulate-the-device"></a>Имитация устройства

1. В колонке сводной информации о службе подготовки устройств выберите **Обзор** и запишите указанные там значения _Область идентификатора_ и _Provisioning Service Global Endpoint_ (Глобальная конечная точка службы подготовки).

    ![Сведения о службе](./media/java-quick-create-simulated-device-x509/extract-dps-endpoints.png)

1. Откройте окно командной строки. Перейдите к папке с примером проекта.

    ```cmd/sh
    cd azure-iot-sdk-java/provisioning/provisioning-samples/provisioning-X509-sample
    ```

1. Введите сведения о регистрации одним из следующих способов, в зависимости от используемой схемы работы.

    - **Индивидуальная регистрация**. 

        1. Измените `/src/main/java/samples/com/microsoft/azure/sdk/iot/ProvisioningX509Sample.java`, чтобы добавить значения параметров _Область идентификатора_ и _Provisioning Service Global Endpoint_ (Глобальная конечная точка службы подготовки), которые вы записали ранее. Также добавьте в файл _Сертификат клиента_ и _Закрытый ключ сертификата клиента_, которые вы записали ранее.

            ```java
            private static final String idScope = "[Your ID scope here]";
            private static final String globalEndpoint = "[Your Provisioning Service Global Endpoint here]";
            private static final ProvisioningDeviceClientTransportProtocol PROVISIONING_DEVICE_CLIENT_TRANSPORT_PROTOCOL = ProvisioningDeviceClientTransportProtocol.HTTPS;
            private static final String leafPublicPem = "<Your Public PEM Certificate here>";
            private static final String leafPrivateKey = "<Your Private PEM Key here>";
            ```

            - Используйте для сертификата и ключа следующий формат:
            
                ```java
                private static final String leafPublicPem = "-----BEGIN CERTIFICATE-----\n" +
                    "XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX\n" +
                    "XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX\n" +
                    "XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX\n" +
                    "XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX\n" +
                    "+XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX\n" +
                    "-----END CERTIFICATE-----\n";
                private static final String leafPrivateKey = "-----BEGIN PRIVATE KEY-----\n" +
                    "XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX\n" +
                    "XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX\n" +
                    "XXXXXXXXXX\n" +
                    "-----END PRIVATE KEY-----\n";
                ```

    - **Группы регистрации**. 

        1. Следуйте инструкциям, приведенным выше для **индивидуальной регистрации**.

        1. Добавьте в начало функции `main` следующие строки кода.
        
            ```java
            String intermediatePem = "<Your Signer Certificate here>";          
            String rootPem = "<Your Root Certificate here>";
                
            signerCertificates.add(intermediatePem);
            signerCertificates.add(root);
            ```
    
            - Используйте для сертификатов следующий формат:
        
                ```java
                String intermediatePem = "-----BEGIN CERTIFICATE-----\n" +
                    "XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX\n" +
                    "XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX\n" +
                    "XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX\n" +
                    "XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX\n" +
                    "+XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX\n" +
                    "-----END CERTIFICATE-----\n";
                String rootPem = "-----BEGIN CERTIFICATE-----\n" +
                    "XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX\n" +
                    "XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX\n" +
                    "XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX\n" +
                    "XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX\n" +
                    "+XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX\n" +
                    "-----END CERTIFICATE-----\n";
                ```

1. Выполните сборку примера. Перейдите в целевую папку и запустите созданный JAR-файл.

    ```cmd/sh
    mvn clean install
    cd target
    java -jar ./provisioning-x509-sample-{version}-with-deps.jar
    ```

1. На портале перейдите в Центр Интернета вещей, связанный со службой подготовки, и откройте колонку **Обозреватель устройств**. Когда имитированное устройство X.509 будет успешно подготовлено для центра, в колонке **Обозреватель устройств** появится идентификатор этого устройства со значением **Включено** в столбце *Состояние*. Обратите внимание, что может потребоваться нажать кнопку **Обновить** в верхней части окна, если вы уже открывали колонку, прежде чем запустить пример приложения для устройства. 

    ![Устройство зарегистрировано в Центре Интернета вещей](./media/java-quick-create-simulated-device-x509/hub-registration.png) 

> [!NOTE]
> Если в записи регистрации для своего устройства вы изменили значение по умолчанию для *начального состояния двойника устройства*, требуемое состояние двойника будет извлечено из концентратора с последующим выполнением соответствующих действий. См. [общие сведения о двойниках устройств и их использовании в Центре Интернета вещей](../iot-hub/iot-hub-devguide-device-twins.md).
>


## <a name="clean-up-resources"></a>Очистка ресурсов

Если вы планируете продолжить работу с примером клиентского устройства, не удаляйте ресурсы, созданные в ходе работы с этим руководством. Если вы не планируете продолжать работу, следуйте инструкциям ниже, чтобы удалить все созданные ресурсы.

1. Закройте окно выходных данных примера клиентского устройства на компьютере.
1. В меню слева на портале Azure щелкните **Все ресурсы** и откройте службу подготовки устройств. Откройте колонку **Управление регистрациями** для службы, затем откройте вкладку **Индивидуальные регистрации**. Выберите *идентификатор регистрации* устройства, которое вы зарегистрировали в процессе работы с этим руководством, и нажмите кнопку **Удалить** вверху. 
1. В меню слева на портале Azure нажмите кнопку **Все ресурсы** и выберите свой Центр Интернета вещей. Откройте колонку **IoT Devices** (Устройства Интернета вещей) для нужного центра, выберите *идентификатор устройства*, зарегистрированного в процессе работы с руководством, и нажмите кнопку **Удалить** вверху.


## <a name="next-steps"></a>Дополнительная информация

В этом кратком руководстве вы создали имитированное устройство X.509 на компьютере Windows и подготовили его для Центра Интернета вещей с помощью службы подготовки устройств Центра Интернета вещей Azure на портале. Чтобы узнать, как программными средствами зарегистрировать устройство X.509, изучите краткое руководство по программной регистрации устройств X.509. 

> [!div class="nextstepaction"]
> [Краткое руководство по Azure. Регистрация устройств X.509 в службе подготовки устройств Центра Интернета вещей](quick-enroll-device-x509-java.md)
