---
title: "aaaHow toolog события tooAzure концентраторов событий в службе управления API Azure | Документы Microsoft"
description: "Узнайте, как tooAzure toolog событий концентраторов событий в службе управления API Azure."
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: 88f6507d-7460-4eb2-bffd-76025b73f8c4
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/15/2016
ms.author: apimpm
ms.openlocfilehash: 09ca65fc48a874467c6662858f7594e9b19fcdb9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toolog-events-tooazure-event-hubs-in-azure-api-management"></a>Как tooAzure toolog событий концентраторов событий в службе управления API Azure
Концентраторы событий Azure — служба входящих данных на высокую степень масштабируемости, можно принять миллионов событий в секунду, можно обрабатывать и анализировать hello значительные объемы данных, создаваемых подключенных устройств и приложений. Концентраторов событий действует как hello «дверью» для конвейера событий и сбора данных в концентратор событий, он может преобразовываться и сохраненных с помощью любого поставщика аналитика в реальном времени или адаптеры пакетной обработки хранилища. Концентраторы событий отделяет hello рабочего потока событий из hello использования этих событий, чтобы потребители событий можно получать доступ к событиям hello по собственному расписанию.

Эта статья является toohello дополнительное [интегрируются с концентраторами событий управления API Azure](https://azure.microsoft.com/documentation/videos/integrate-azure-api-management-with-event-hubs/) видео и показывается, как события toolog управления API, с помощью концентраторов событий Azure.

## <a name="create-an-azure-event-hub"></a>Создание концентратора событий Azure
новый концентратор событий входа в toohello toocreate [классический портал Azure](https://manage.windowsazure.com) и нажмите кнопку **New**->**службы приложений**->**Service Bus**  -> **Концентратора событий**->**быстрое создание**. Введите имя концентратора событий, регион, выберите подписку и пространство имен. Если вы еще не создали пространство имен можно создать, введя имя в hello **имен** текстового поля. После настройки всех свойств, нажмите кнопку **создать новый концентратор событий** toocreate hello концентратора событий.

![Создание концентратора событий][create-event-hub]

Далее перейдите toohello **Настройка** вкладке нового концентратора событий и создания двух **политики общего доступа**. Имя первого hello **Отправка** и присвойте ему **отправки** разрешения.

![Политика «Отправка»][sending-policy]

Имя второго hello **получения**, ей следует присвоить **прослушивания** разрешений и нажмите **Сохранить**.

![Политика «Получение»][receiving-policy]

Каждая политика общего доступа позволяет toosend приложений и получают события tooand от hello концентратора событий. строки подключения hello tooaccess для этих политик перейдите toohello **мониторинга** hello концентратора событий и нажмите кнопку **сведения о соединении**.

![Строка подключения][event-hub-dashboard]

Hello **Отправка** строка подключения используется в том случае, если ведение журнала событий и hello **получения** строка подключения используется при загрузке события с hello концентратора событий.

![Строка подключения][event-hub-connection-string]

## <a name="create-an-api-management-logger"></a>Создание средства ведения журнала для управления API
Теперь, когда концентратора событий hello следующим шагом является tooconfigure [средства ведения журнала](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-logger-entity) в вашей службе управления API службы, чтобы его можно записывать в журнал событий toohello концентратора событий.

Управление API средств ведения журнала настроены с использованием hello [API REST управления](http://aka.ms/smapi). Перед использованием hello API-интерфейса REST для hello первый раз, просмотрите hello [необходимые компоненты](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/api-management-rest#Prerequisites) и убедитесь, что [включен доступ toohello API-интерфейса REST](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/api-management-rest#EnableRESTAPI).

toocreate средство ведения журнала, сделать запрос HTTP PUT, используя следующий шаблон URL-адреса hello.

`https://{your service}.management.azure-api.net/loggers/{new logger name}?api-version=2014-02-14-preview`

* Замените `{your service}` hello именем вашего экземпляра службы управления API.
* Замените `{new logger name}` с нужным именем hello для вашего новое средство ведения журнала. Это имя будет ссылаться при настройке hello [журнала eventhub](https://msdn.microsoft.com/library/azure/dn894085.aspx#log-to-eventhub) политики

Добавьте следующие заголовки запроса toohello hello.

* тип содержимого: «application/json»;
* авторизация: SharedAccessSignature 58...
  * Инструкции о создании hello `SharedAccessSignature` разделе [проверки подлинности API REST управления API Azure](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-authentication).

Укажите hello текст запроса, используя следующий шаблон hello.

```json
{
  "type" : "AzureEventHub",
  "description" : "Sample logger description",
  "credentials" : {
    "name" : "Name of hello Event Hub from hello Azure Classic Portal",
    "connectionString" : "Endpoint=Event Hub Sender connection string"
    }
}
```

* `type`необходимо задать слишком`AzureEventHub`.
* `description`предоставляет средства ведения журнала hello необязательное описание и может быть строка нулевой длины, при необходимости.
* `credentials`содержит hello `name` и `connectionString` из концентратора событий Azure.

При выполнении запроса hello hello средства ведения журнала, созданный код состояния `201 Created` возвращается.

> [!NOTE]
> Другие возможные коды возврата и их причины см. в статье, посвященной [созданию средств ведения журнала](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-logger-entity#PUT). toosee, как выполнить другие операции, такие как список, update и delete, в разделе hello [средства ведения журнала](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-logger-entity) документации сущности.
>
>

## <a name="configure-log-to-eventhubs-policies"></a>Настройка политик регистрации в концентраторах событий
После настройки вашей средства ведения журнала в службе управления API можно настроить события журнала eventhubs политики toolog требуемого hello. Hello журнала eventhubs политика может использоваться в любом hello раздел входящей политики или раздел исходящих политики hello.

tooconfigure политик, вход toohello [портал Azure](https://portal.azure.com), перейдите в службе управления API tooyour и нажмите кнопку **портал издателя** tooaccess hello портала издателя.

![Портал издателя][publisher-portal]

Нажмите кнопку **политики** в hello API управления меню слева hello, выберите нужный продукт hello и API и щелкните **Добавление политики**. В этом примере мы добавляем toohello политики **Echo API** в hello **неограниченное количество** продукта.

![добавление политики;][add-policy]

Поместите курсор в hello `inbound` политики и нажмите кнопку hello **tooEventHub журнала** tooinsert hello политики `log-to-eventhub` инструкции шаблона политики.

![Редактор политики][event-hub-policy]

```xml
<log-to-eventhub logger-id ='logger-id'>
  @( string.Join(",", DateTime.UtcNow, context.Deployment.ServiceName, context.RequestId, context.Request.IpAddress, context.Operation.Name))
</log-to-eventhub>
```

Замените `logger-id` с именем hello API управления hello средства ведения журнала, настроенные в предыдущем шаге hello.

Можно использовать любое выражение, возвращающее строку как значение hello для hello `log-to-eventhub` элемента. В этом примере регистрируется строка, содержащая hello даты и времени, имя службы, идентификатор запроса, запрос IP-адрес и имя операции.

Нажмите кнопку **Сохранить** toosave hello обновлена конфигурация политики. Как только он сохраняется hello политика не активна, и события, зарегистрированного toohello назначенному концентратора событий.

## <a name="next-steps"></a>Дальнейшие действия
* Дополнительная информация о концентраторах событий Azure
  * [Приступая к работе с концентраторами событий Azure](../event-hubs/event-hubs-c-getstarted-send.md)
  * [Прием сообщений через EventProcessorHost](../event-hubs/event-hubs-dotnet-standard-getstarted-receive-eph.md)
  * [Руководство по программированию концентраторов событий](../event-hubs/event-hubs-programming-guide.md)
* Дополнительные сведения об интеграции службы управления API и концентраторов событий
  * [Справочник по сущности "Средство ведения журнала"](https://docs.microsoft.com/rest/api/apimanagement/loggers)
  * [Справочник по политике регистрации в концентраторе событий](https://docs.microsoft.com/azure/api-management/api-management-advanced-policies#log-to-eventhub)
  * [Мониторинг API-интерфейсов с помощью службы управления API Azure, концентраторов событий и Runscope](api-management-log-to-eventhub-sample.md)    

## <a name="watch-a-video-walkthrough"></a>Просмотрите видеоруководство
> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Integrate-Azure-API-Management-with-Event-Hubs/player]
>
>

[publisher-portal]: ./media/api-management-howto-log-event-hubs/publisher-portal.png
[create-event-hub]: ./media/api-management-howto-log-event-hubs/create-event-hub.png
[event-hub-connection-string]: ./media/api-management-howto-log-event-hubs/event-hub-connection-string.png
[event-hub-dashboard]: ./media/api-management-howto-log-event-hubs/event-hub-dashboard.png
[receiving-policy]: ./media/api-management-howto-log-event-hubs/receiving-policy.png
[sending-policy]: ./media/api-management-howto-log-event-hubs/sending-policy.png
[event-hub-policy]: ./media/api-management-howto-log-event-hubs/event-hub-policy.png
[add-policy]: ./media/api-management-howto-log-event-hubs/add-policy.png
