---
title: "aaaAzure IoT Suite и Logic Apps | Документы Microsoft"
description: "Руководство по установке и toohook вверх tooAzure Logic Apps IoT Suite для бизнес-процесса."
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 4629a7af-56ca-4b21-a769-5fa18bc3ab07
ms.service: iot-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/16/2017
ms.author: corywink
ms.openlocfilehash: 6ef7311ac38f4e2ddb032cff0fb73591da5f76c2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-connect-logic-app-tooyour-azure-iot-suite-remote-monitoring-preconfigured-solution"></a>Учебник: Решение Azure IoT Suite удаленный мониторинг заранее настроенные приложения логики tooyour подключения
Hello [Microsoft Azure IoT Suite] [ lnk-internetofthings] удаленное наблюдение предварительно настроенных решений является tooget удобно быстро начать работу с набор компонентов конца в конец которого дан пример решения IoT. Этот учебник поможет выполнить как tooadd приложения логики tooyour Microsoft Azure IoT Suite удаленный мониторинг предварительно настроенных решений. Эти действия демонстрируют, как можно использовать еще более вашего решения IoT, подключив tooa бизнес-процесса.

*Если вы ищете Пошаговое руководство по как удаленный мониторинг tooprovision предварительно настроенных решений, см. раздел [учебник: Приступая к работе с hello IoT предварительно настроенных решений][lnk-getstarted].*

Перед началом работы с данным учебником необходимо выполнить описанные ниже действия.

* Удаленный мониторинг подготовки hello предварительно настроенное решение в вашей подписке Azure.
* Создание учетной записи SendGrid tooenable toosend сообщение электронной почты, которое запускает бизнес-процессов. Бесплатную пробную учетную запись можно создать на сайте [SendGrid](https://sendgrid.com/) , нажав кнопку **Try for Free**(Попробовать бесплатно). После регистрации для бесплатной пробной учетной записи, необходимо toocreate [ключ API](https://sendgrid.com/docs/User_Guide/Settings/api_keys.html) в SendGrid, которая предоставляет разрешения toosend почты. Этот ключ API должны далее в учебнике hello.

toocomplete этого учебника требуется Visual Studio 2015 или Visual Studio 2017 г toomodify hello действий в серверной части hello предварительно настроенных решений.

При условии, что вы инициализированного удаленное наблюдение за предварительно настроенных решений, перейдите toohello группы ресурсов для этого решения в hello [портал Azure][lnk-azureportal]. группы ресурсов Hello есть hello точно такое же имя, как hello решения именем вы выбрали при подготовке удаленного мониторинга решения. В группе ресурсов hello вы увидите все hello подготовить ресурсы Azure для вашего решения, за исключением hello приложения Azure Active Directory, можно найти в hello классический портал Azure. Hello следующем снимке экрана показан пример **группы ресурсов** колонку для удаленного мониторинга предварительно настроенных решений:

![](media/iot-suite-logic-apps-tutorial/resourcegroup.png)

toobegin, Настройка toouse приложения hello логики с hello предварительно настроенных решений.

## <a name="set-up-hello-logic-app"></a>Настройка логики приложения hello
1. Нажмите кнопку **добавить** вверху hello вашей колонки группы ресурсов в hello портал Azure.
2. Найдите **Приложение логики**, выберите его и нажмите кнопку **Создать**.
3. Заполните hello **имя** и используйте hello же **подписки** и **группы ресурсов** , которые использовались при подготовке удаленного мониторинга решения. Щелкните **Создать**.
   
    ![](media/iot-suite-logic-apps-tutorial/createlogicapp.png)
4. После завершения развертывания появится hello логики приложения, указана как ресурс в группе ресурсов.
5. Нажмите кнопку колонки приложения логики toohello toonavigate логику приложения hello, выберите hello **пустое приложение логики** hello tooopen шаблона **конструктор приложений логики**.
   
    ![](media/iot-suite-logic-apps-tutorial/logicappsdesigner.png)
6. Выберите **Запрос**. Это действие указывает, что в качестве триггера выступает входящий HTTP-запрос с полезными данными в определенном формате JSON.
7. Вставьте следующий код в hello схемы JSON тело запроса hello:
   
    ```json
    {
      "$schema": "http://json-schema.org/draft-04/schema#",
      "id": "/",
      "properties": {
        "DeviceId": {
          "id": "DeviceId",
          "type": "string"
        },
        "measuredValue": {
          "id": "measuredValue",
          "type": "integer"
        },
        "measurementName": {
          "id": "measurementName",
          "type": "string"
        }
      },
      "required": [
        "DeviceId",
        "measurementName",
        "measuredValue"
      ],
      "type": "object"
    }
    ```
   
   > [!NOTE]
   > После сохранения логики приложения hello, но сначала необходимо добавить действие можно скопировать URL-адрес hello hello HTTP post.
   > 
   > 
8. Щелкните **+ Новый шаг** под своим триггером. Затем выберите **Добавить действие**.
   
    ![](media/iot-suite-logic-apps-tutorial/logicappcode.png)
9. Найдите действие **SendGrid - Send email** (SendGrid — отправить письмо) и щелкните его.
   
    ![](media/iot-suite-logic-apps-tutorial/logicappaction.png)
10. Введите имя подключения hello, например **SendGridConnection**, введите hello **ключ API SendGrid** были созданы при настройке учетной записи SendGrid и нажмите кнопку **создать**.
    
    ![](media/iot-suite-logic-apps-tutorial/sendgridconnection.png)
11. Добавление адресов электронной почты вы hello собственные tooboth **из** и **для** поля. Добавить **удаленного мониторинга оповещения [DeviceId]** toohello **субъекта** поля. В hello **тело сообщения электронной почты** поля, добавьте **устройства [DeviceId] сообщил [measurementName] со значением [measuredValue].** Можно добавить **[DeviceId]**, **[measurementName]**, и **[measuredValue]** , щелкнув в hello **может вставлять данные из предыдущих шагов**раздел.
    
    ![](media/iot-suite-logic-apps-tutorial/sendgridaction.png)
12. Нажмите кнопку **Сохранить** в верхнем меню hello.
13. Нажмите кнопку hello **запроса** триггера и скопируйте hello **URL-адрес Http Post toothis** значение. Этот URL-адрес потребуется далее в этом учебнике.

> [!NOTE]
> Приложения логики включить toorun [множество различных типов действий] [ lnk-logic-apps-actions] включая действий в Office 365. 
> 
> 

## <a name="set-up-hello-eventprocessor-web-job"></a>Настройка hello EventProcessor веб-задание
В этом разделе подключиться к предварительно настроенных решений toohello логику приложения, созданного. toocomplete этой задачи добавьте hello URL-адрес tootrigger hello приложения логики toohello действие, которое применяется, когда значение датчика устройства превышает пороговое значение.

1. Использовать git клиента tooclone hello последние версии hello [azure iot удаленного мониторинга репозитории github][lnk-rmgithub]. Например:
   
    ```cmd
    git clone https://github.com/Azure/azure-iot-remote-monitoring.git
    ```
2. В Visual Studio откройте hello **RemoteMonitoring.sln** из hello локальную копию репозитория hello.
3. Откройте hello **ActionRepository.cs** файла в hello **инфраструктуры\\репозитория** папки.
4. Обновление hello **actionIds** словарь с hello **URL-адрес Http Post toothis** записанными из логики приложения, следующим образом:
   
    ```csharp
    private Dictionary<string,string> actionIds = new Dictionary<string, string>()
    {
        { "Send Message", "<Http Post toothis URL>" },
        { "Raise Alarm", "<Http Post toothis URL>" }
    };
    ```
5. Сохранить изменения hello в решении и выйти из Visual Studio.

## <a name="deploy-from-hello-command-line"></a>Развертывание из командной строки hello
В этом разделе развернуть обновленную версию hello удаленного мониторинга tooreplace hello версия решения выполняющихся в Azure.

1. Следующие hello [настройки разработки] [ lnk-devsetup] tooset инструкции настройку среды для развертывания.
2. toodeploy локально, выполните hello [локальное развертывание] [ lnk-localdeploy] инструкции.
3. toodeploy toohello облако и обновить существующие развертывания облачной, выполните hello [облако развертывания] [ lnk-clouddeploy] инструкции. Используйте имя hello исходного развертывания, как имя развертывания hello. Например, если вызывался hello исходного развертывания **demologicapp**, использовать hello следующую команду:
   
   ```cmd
   build.cmd cloud release demologicapp
   ```
   
   При запуске сценария сборки hello убедитесь, что toouse hello же учетная запись Azure, подписки, регион и экземпляр Active Directory, который использовался при подготовке hello решения.

## <a name="see-your-logic-app-in-action"></a>Проверка приложения логики в действии
удаленный мониторинг предварительно настроенных решений Hello имеет два правила, установленные по умолчанию, при подготовке решения. Оба правила находятся на hello **SampleDevice001** устройства:

* Температура > 38,00
* Влажность > 48,00

правило температуры Hello запускает hello **вызова сигнала** действие и hello влажности правило срабатывает hello **SendMessage** действие. При условии, что вы использовали hello же URL-адрес для обоих действий hello **ActionRepository** класса триггеры логику приложения для этих правил. Оба правила использования toosend SendGrid по электронной почте toohello **для** адрес с подробными сведениями hello предупреждения.

> [!NOTE]
> Hello логику приложения по-прежнему tootrigger каждый раз при достижении порогового значения hello. tooavoid ненужные электронные сообщения, можно отключить правила hello в вашего решения портала или отключите hello приложения логики в hello [портал Azure][lnk-azureportal].
> 
> 

В дополнение к этому tooreceiving сообщений электронной почты, также видно при запуске приложения логики hello hello портала:

![](media/iot-suite-logic-apps-tutorial/logicapprun.png)

## <a name="next-steps"></a>Дальнейшие действия
Теперь, когда вы использовали приложения логики tooconnect hello предварительно настроенное решение tooa бизнес-процесс, изучите более подробную hello варианты настройки hello предварительно настроенных решений:

* [Используйте динамические данные телеметрии с hello удаленное наблюдение предварительно настроенных решений][lnk-dynamic]
* [Устройство сведения метаданных в удаленное наблюдение предварительно настроенных решений hello][lnk-devinfo]

[lnk-dynamic]: iot-suite-dynamic-telemetry.md
[lnk-devinfo]: iot-suite-remote-monitoring-device-info.md

[lnk-internetofthings]: https://azure.microsoft.com/documentation/suites/iot-suite/
[lnk-getstarted]: iot-suite-getstarted-preconfigured-solutions.md
[lnk-azureportal]: https://portal.azure.com
[lnk-logic-apps-actions]: ../connectors/apis-list.md
[lnk-rmgithub]: https://github.com/Azure/azure-iot-remote-monitoring
[lnk-devsetup]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/Docs/dev-setup.md
[lnk-localdeploy]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/Docs/local-deployment.md
[lnk-clouddeploy]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/Docs/cloud-deployment.md
