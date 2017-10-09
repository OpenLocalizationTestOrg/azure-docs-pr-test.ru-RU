---
title: "aaaAzure IoT Suite часто задаваемые вопросы | Документы Microsoft"
description: "Часто задаваемые вопросы об IoT Suite"
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: cb537749-a8a1-4e53-b3bf-f1b64a38188a
ms.service: iot-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/15/2017
ms.author: corywink
ms.openlocfilehash: cb39e24af6d1ce2afea554285512d05b2d7c721e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="frequently-asked-questions-for-iot-suite"></a>Часто задаваемые вопросы об IoT Suite

См. также определенного подключенного фабрики hello [часто задаваемые вопросы о](iot-suite-faq-cf.md).

### <a name="where-can-i-find-hello-source-code-for-hello-preconfigured-solutions"></a>Где найти hello исходного кода для hello предварительно настроенных решений?

Hello исходный код хранится в hello, следуя репозиториях GitHub:
* [Предварительно настроенное решение для удаленного мониторинга][lnk-remote-monitoring-github]
* [Предварительно настроенное решение по диагностическому обслуживанию][lnk-predictive-maintenance-github]
* [Предварительно настроенное решение для подключенной фабрики](https://github.com/Azure/azure-iot-connected-factory)

### <a name="how-do-i-update-toohello-latest-version-of-hello-remote-monitoring-preconfigured-solution-that-uses-hello-iot-hub-device-management-features"></a>Как обновить toohello последнюю версию решения удаленного мониторинга предварительно настроенных hello hello, использует функциональные возможности управления устройствами центра IoT?

* При развертывании предварительно настроенных решений с сайта https://www.azureiotsuite.com/ hello всегда развертывает новый экземпляр hello последнюю версию решения hello.
* При развертывании предварительно настроенных решений с помощью командной строки hello, можно обновить существующее развертывание с нового кода. В разделе [облако развертывания] [ lnk-cloud-deployment] в hello GitHub [репозитория][lnk-remote-monitoring-github].

### <a name="how-can-i-add-support-for-a-new-device-method-toohello-remote-monitoring-preconfigured-solution"></a>Как добавить поддержку нового устройства метод toohello удаленное наблюдение предварительно настроенных решений?

В разделе hello [добавить поддержку нового симулятор toohello метод] [ lnk-add-method] в hello [настроить предварительно настроенных решений] [ lnk-customize] статьи.

### <a name="hello-simulated-device-is-ignoring-my-desired-property-changes-why"></a>имитированное устройство Hello игнорирует изменения нужное свойство, почему?
В hello удаленный мониторинг предварительно настроенное решение, код hello имитируемые устройства использует только hello **Desired.Config.TemperatureMeanValue** и **Desired.Config.TelemetryInterval** требуемого свойства tooupdate hello сообщил свойства. Все прочие запросы на изменение требуемых свойств игнорируются.

### <a name="my-device-does-not-appear-in-hello-list-of-devices-in-hello-solution-dashboard-why"></a>Устройство не отображается в hello список устройств на панели мониторинга решения hello, почему?

Hello список устройств на панели мониторинга hello решение использует список hello tooreturn запрос устройств. В настоящее время запрос не может возвращать более 10 000 устройств. Попробуйте сделать более строгим hello критериев поиска для запроса.

### <a name="whats-hello-difference-between-deleting-a-resource-group-in-hello-azure-portal-and-clicking-delete-on-a-preconfigured-solution-in-azureiotsuitecom"></a>Что такое hello различие между при удалении группы ресурсов в Azure, портала и затем выбрав удаление предварительно настроенного решения в azureiotsuite.com hello

* При удалении hello предварительно настроенное решение в [azureiotsuite.com][lnk-azureiotsuite], удалить все ресурсы hello, заданные при создании hello предварительно настроенных решений. Если вы добавили группы ресурсов toohello дополнительные ресурсы, эти ресурсы также будут удалены. 
* Если удалить группу ресурсов hello в hello [портал Azure][lnk-azure-portal], необходимо удалить только hello ресурсов в этой группе ресурсов. Необходимо также toodelete hello Azure Active Directory приложение, связанное с hello предварительно настроенное решение в hello [классический портал Azure][lnk-classic-portal].

### <a name="how-many-iot-hub-instances-can-i-provision-in-a-subscription"></a>Сколько экземпляров центров IoT можно подготовить в рамках одной подписки?

По умолчанию [в рамках одной подписки можно подготовить 10 экземпляров Центра Интернета вещей][link-azuresublimits]. Можно создать [обращение в службу поддержки Azure] [ link-azuresupportticket] tooraise это ограничение. В результате после каждой предварительно настроенных решений подготавливает центр IoT, вы можете только подготовки вверх too10 предварительно настроенных решений по данной подписке. 

### <a name="how-many-azure-cosmos-db-instances-can-i-provision-in-a-subscription"></a>Сколько экземпляров Azure Cosmos DB можно подготовить в рамках одной подписки?

Пятьдесят. Можно создать [обращение в службу поддержки Azure] [ link-azuresupportticket] tooraise это ограничение, но по умолчанию можно указать только 50 экземпляров Cosmos DB на подписку. 

### <a name="how-many-free-bing-maps-apis-can-i-provision-in-a-subscription"></a>Сколько бесплатных API-интерфейсов Карт Bing можно подготовить в рамках одной подписки?

Два. В рамках подписки Azure можно создать только две карты Bing уровня 1 с внутренними транзакциями для корпоративных планов. решение для удаленного мониторинга Hello настраивается по умолчанию с планом hello внутренние транзакции уровня 1. В результате могут только подготавливать tootwo удаленный мониторинг решений в подписке без изменений.

### <a name="i-have-a-remote-monitoring-solution-deployment-with-a-static-map-how-do-i-add-an-interactive-bing-map"></a>У меня есть развернутое решение для удаленного мониторинга со статической картой. Как мне добавить интерактивную карту Bing?

1. Получите на [портале Azure][lnk-azure-portal] ключ QueryKey API для Карт Bing для предприятий: 
   
   1. Перейдите toohello группы ресурсов, где находится ваш API службы Bing Maps для предприятия в hello [портал Azure][lnk-azure-portal].
   2. Щелкните **Все параметры** и **Управление ключами**. 
   3. Вы увидите два ключа: **MasterKey** и **QueryKey**. Скопируйте значение hello для **QueryKey**.
      
      > [!NOTE]
      > У вас нет учетной записи Bing Maps API for Enterprise? Создайте его в hello [портал Azure] [ lnk-azure-portal] , щелкнув + новый поиск Bing Maps API для выпусков Enterprise и выполните запрос toocreate.
      > 
      > 
2. Подтягивают последнюю кода hello из hello [Azure IoT-удаленного-мониторинга][lnk-remote-monitoring-github].
3. Запустите локальное или облачные развертывания следующие рекомендации hello развертывания из командной строки в папке /docs/ hello в репозитории hello. 
4. После запуска локальной или облачной развертывания, проверьте в корневой папке для hello *. файл user.config, созданный во время развертывания. Откройте этот файл в текстовом редакторе. 
5. Изменение hello следующая строка hello значение tooinclude, скопированный из вашего **QueryKey**: 
   
   `<setting name="MapApiQueryKey" value="" />`

### <a name="can-i-create-a-preconfigured-solution-if-i-have-microsoft-azure-for-dreamspark"></a>Можно ли создать предварительно настроенное решение при наличии Microsoft Azure для DreamSpark?

Сейчас нельзя создавать предварительно настроенные решения с использованием учетной записи [Microsoft Azure для DreamSpark][lnk-dreamspark]. Но вы можете создать [бесплатную пробную учетную запись Azure][lnk-30daytrial] всего за несколько минут. Это позволит вам создать предварительно настроенное решение.

### <a name="can-i-create-a-preconfigured-solution-if-i-have-cloud-solution-provider-csp-subscription"></a>Можно ли создать предварительно настроенное решение при наличии подписки поставщика облачных решений (CSP)?

В настоящее время создание предварительно настроенных решений с помощью подписки поставщика облачных решений (CSP) недоступно. Но вы можете создать [бесплатную пробную учетную запись Azure][lnk-30daytrial] всего за несколько минут. Это позволит вам создать предварительно настроенное решение.

### <a name="how-do-i-delete-an-aad-tenant"></a>Как удалить клиент AAD?

Ознакомьтесь с записью блога Эрика Голпа (Eric Golpe) [Walkthrough of Deleting an Azure AD Tenant][lnk-delete-aad-tennant] (Пошаговое руководство по удалению клиента Azure AD).

### <a name="next-steps"></a>Дальнейшие действия

Можно также изучить некоторые hello и другие возможности hello IoT Suite предварительно настроенных решений:

* [Обзор предварительно настроенного решения прогнозируемого обслуживания][lnk-predictive-overview]
* [Начало работы с предварительно настроенным решением для подключенной фабрики](iot-suite-connected-factory-overview.md)
* [Основание безопасности IoT из hello,][lnk-security-groundup]

[lnk-predictive-overview]: iot-suite-predictive-overview.md
[lnk-security-groundup]: securing-iot-ground-up.md

[link-azuresupportticket]: https://portal.azure.com/#blade/Microsoft_Azure_Support/HelpAndSupportBlade 
[link-azuresublimits]: https://azure.microsoft.com/documentation/articles/azure-subscription-service-limits/#iot-hub-limits
[lnk-azure-portal]: https://portal.azure.com
[lnk-azureiotsuite]: https://www.azureiotsuite.com/
[lnk-classic-portal]: https://manage.windowsazure.com
[lnk-remote-monitoring-github]: https://github.com/Azure/azure-iot-remote-monitoring 
[lnk-dreamspark]: https://www.dreamspark.com/Product/Product.aspx?productid=99 
[lnk-30daytrial]: https://azure.microsoft.com/free/
[lnk-delete-aad-tennant]: http://blogs.msdn.com/b/ericgolpe/archive/2015/04/30/walkthrough-of-deleting-an-azure-ad-tenant.aspx
[lnk-cloud-deployment]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/Docs/cloud-deployment.md
[lnk-add-method]: iot-suite-guidance-on-customizing-preconfigured-solutions.md#add-support-for-a-new-method-to-the-simulator
[lnk-customize]: iot-suite-guidance-on-customizing-preconfigured-solutions.md
[lnk-remote-monitoring-github]: https://github.com/Azure/azure-iot-remote-monitoring
[lnk-predictive-maintenance-github]: https://github.com/Azure/azure-iot-predictive-maintenance
