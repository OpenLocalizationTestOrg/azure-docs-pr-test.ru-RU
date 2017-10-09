---
title: "aaaHow toouse концентраторов уведомлений с Python"
description: "Узнайте, как toouse концентраторов уведомлений Azure из внутренней Python."
services: notification-hubs
documentationcenter: 
author: ysxu
manager: erikre
editor: 
ms.assetid: 5640dd4a-a91e-4aa0-a833-93615bde49b4
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: python
ms.devlang: php
ms.topic: article
ms.date: 06/29/2016
ms.author: yuaxu
ms.openlocfilehash: 21d5aaf7fc24c9936fac8e0a8de640c66c51ab0a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-notification-hubs-from-python"></a>Как toouse концентраторов уведомлений с Python
[!INCLUDE [notification-hubs-backend-how-to-selector](../../includes/notification-hubs-backend-how-to-selector.md)]

Все функции концентраторов уведомлений можно получить из внутренней Java и PHP и Python и Ruby с помощью интерфейса REST концентратора уведомлений hello, как описано в разделе MSDN hello [интерфейсы API REST концентраторов уведомлений](http://msdn.microsoft.com/library/dn223264.aspx).

> [!NOTE]
> Это образец реализации реализации hello отправляет уведомление в Python и не является hello официально поддерживается пакет SDK для Python концентратора уведомлений.
> 
> Этот образец написан с помощью Python 3.4.
> 
> 

В этой статье описывается:

* Построение клиента REST для функций концентраторов уведомлений на языке Python.
* Отправьте уведомления, используя toohello интерфейса API REST концентратора уведомления для hello Python. 
* Отладка/образовательных целях получения дампа hello HTTP REST запросов и ответов. 

Можно выполнить hello [учебника запущенную Get](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md) для вашей платформы мобильных устройств по выбору, реализация hello серверную часть в Python.

> [!NOTE]
> Hello образец hello относится только ограниченный toosend уведомления и он не выполняет любой управления регистрацией.
> 
> 

## <a name="client-interface"></a>Интерфейс клиента
Hello основного клиентского интерфейса предоставляет hello же методы, доступные в hello [.NET SDK концентраторы уведомлений](http://msdn.microsoft.com/library/jj933431.aspx). Это позволит вам toodirectly перевести все hello учебники и образцы, доступных в настоящее время этот сайт и предоставленного сообществом hello на hello Интернета.

Можно найти все доступные в hello кода hello [образца программы-оболочки Python REST].

Например toocreate клиента:

    isDebug = True
    hub = NotificationHub("myConnectionString", "myNotificationHubName", isDebug)

toosend Windows всплывающих уведомлений:

    wns_payload = """<toast><visual><binding template=\"ToastText01\"><text id=\"1\">Hello world!</text></binding></visual></toast>"""
    hub.send_windows_notification(wns_payload)

## <a name="implementation"></a>Реализация
Если вы еще не сделали, выполните наши [учебника запущенную Get] вверх toohello последний раздел, при наличии tooimplement hello серверной части.

Здравствуйте, все сведения tooimplement полный оболочки REST можно найти на [MSDN](http://msdn.microsoft.com/library/dn530746.aspx). В этом разделе будут описаны реализация Python hello hello основных шагов требуется tooaccess конечные точки REST концентраторов уведомлений и отправки уведомлений

1. Синтаксический анализ строки соединения hello
2. Создание маркера авторизации hello
3. Отправка уведомления с помощью HTTP REST API

### <a name="parse-hello-connection-string"></a>Синтаксический анализ строки соединения hello
Вот hello основной класс, реализация клиента hello, конструктор которого выполняет синтаксический анализ строки подключения hello.

    class NotificationHub:
        API_VERSION = "?api-version=2013-10"
        DEBUG_SEND = "&test"

        def __init__(self, connection_string=None, hub_name=None, debug=0):
            self.HubName = hub_name
            self.Debug = debug

            # Parse connection string
            parts = connection_string.split(';')
            if len(parts) != 3:
                raise Exception("Invalid ConnectionString.")

            for part in parts:
                if part.startswith('Endpoint'):
                    self.Endpoint = 'https' + part[11:]
                if part.startswith('SharedAccessKeyName'):
                    self.SasKeyName = part[20:]
                if part.startswith('SharedAccessKey'):
                    self.SasKeyValue = part[16:]


### <a name="create-security-token"></a>Создание маркера безопасности
доступны Hello сведения для создания маркера безопасности hello [здесь](http://msdn.microsoft.com/library/dn495627.aspx).
Hello следующие методы имеют добавлены toobe toohello **концентратора уведомлений** класса toocreate hello токены на hello URI текущего запроса hello и hello учетные данные, извлеченные из строки подключения hello.

    @staticmethod
    def get_expiry():
        # By default returns an expiration of 5 minutes (=300 seconds) from now
        return int(round(time.time() + 300))

    @staticmethod
    def encode_base64(data):
        return base64.b64encode(data)

    def sign_string(self, to_sign):
        key = self.SasKeyValue.encode('utf-8')
        to_sign = to_sign.encode('utf-8')
        signed_hmac_sha256 = hmac.HMAC(key, to_sign, hashlib.sha256)
        digest = signed_hmac_sha256.digest()
        encoded_digest = self.encode_base64(digest)
        return encoded_digest

    def generate_sas_token(self):
        target_uri = self.Endpoint + self.HubName
        my_uri = urllib.parse.quote(target_uri, '').lower()
        expiry = str(self.get_expiry())
        to_sign = my_uri + '\n' + expiry
        signature = urllib.parse.quote(self.sign_string(to_sign))
        auth_format = 'SharedAccessSignature sig={0}&se={1}&skn={2}&sr={3}'
        sas_token = auth_format.format(signature, expiry, self.SasKeyName, my_uri)
        return sas_token

### <a name="send-a-notification-using-http-rest-api"></a>Отправка уведомления с помощью HTTP REST API
Сначала следует определить класс, представляющий уведомление.

    class Notification:
        def __init__(self, notification_format=None, payload=None, debug=0):
            valid_formats = ['template', 'apple', 'gcm', 'windows', 'windowsphone', "adm", "baidu"]
            if not any(x in notification_format for x in valid_formats):
                raise Exception(
                    "Invalid Notification format. " +
                    "Must be one of hello following - 'template', 'apple', 'gcm', 'windows', 'windowsphone', 'adm', 'baidu'")

            self.format = notification_format
            self.payload = payload

            # array with keynames for headers
            # Note: Some headers are mandatory: Windows: X-WNS-Type, WindowsPhone: X-NotificationType
            # Note: For Apple you can set Expiry with header: ServiceBusNotification-ApnsExpiry
            # in W3C DTF, YYYY-MM-DDThh:mmTZD (for example, 1997-07-16T19:20+01:00).
            self.headers = None

Этот класс представляет собой контейнер для собственного текста уведомления либо набор свойств (в случае шаблонного уведомления), а также набор заголовков, содержащих свойства формата (собственная платформа или шаблон) и специальные свойства платформы (например, свойство срока действия Apple и заголовки WNS).

См. toohello [документации по API-интерфейс REST концентраторов уведомлений](http://msdn.microsoft.com/library/dn495827.aspx) и hello форматы уведомлений платформы для всех hello доступные параметры.

Теперь с помощью этого класса можно написать методы уведомления внутри hello hello отправки **концентратора уведомлений** класса.

    def make_http_request(self, url, payload, headers):
        parsed_url = urllib.parse.urlparse(url)
        connection = http.client.HTTPSConnection(parsed_url.hostname, parsed_url.port)

        if self.Debug > 0:
            connection.set_debuglevel(self.Debug)
            # adding this querystring parameter gets detailed information about hello PNS send notification outcome
            url += self.DEBUG_SEND
            print("--- REQUEST ---")
            print("URI: " + url)
            print("Headers: " + json.dumps(headers, sort_keys=True, indent=4, separators=(' ', ': ')))
            print("--- END REQUEST ---\n")

        connection.request('POST', url, payload, headers)
        response = connection.getresponse()

        if self.Debug > 0:
            # print out detailed response information for debugging purpose
            print("\n\n--- RESPONSE ---")
            print(str(response.status) + " " + response.reason)
            print(response.msg)
            print(response.read())
            print("--- END RESPONSE ---")

        elif response.status != 201:
            # Successful outcome of send message is HTTP 201 - Created
            raise Exception(
                "Error sending notification. Received HTTP code " + str(response.status) + " " + response.reason)

        connection.close()

    def send_notification(self, notification, tag_or_tag_expression=None):
        url = self.Endpoint + self.HubName + '/messages' + self.API_VERSION

        json_platforms = ['template', 'apple', 'gcm', 'adm', 'baidu']

        if any(x in notification.format for x in json_platforms):
            content_type = "application/json"
            payload_to_send = json.dumps(notification.payload)
        else:
            content_type = "application/xml"
            payload_to_send = notification.payload

        headers = {
            'Content-type': content_type,
            'Authorization': self.generate_sas_token(),
            'ServiceBusNotification-Format': notification.format
        }

        if isinstance(tag_or_tag_expression, set):
            tag_list = ' || '.join(tag_or_tag_expression)
        else:
            tag_list = tag_or_tag_expression

        # add hello tags/tag expressions toohello headers collection
        if tag_list != "":
            headers.update({'ServiceBusNotification-Tags': tag_list})

        # add any custom headers toohello headers collection that hello user may have added
        if notification.headers is not None:
            headers.update(notification.headers)

        self.make_http_request(url, payload_to_send, headers)

    def send_apple_notification(self, payload, tags=""):
        nh = Notification("apple", payload)
        self.send_notification(nh, tags)

    def send_gcm_notification(self, payload, tags=""):
        nh = Notification("gcm", payload)
        self.send_notification(nh, tags)

    def send_adm_notification(self, payload, tags=""):
        nh = Notification("adm", payload)
        self.send_notification(nh, tags)

    def send_baidu_notification(self, payload, tags=""):
        nh = Notification("baidu", payload)
        self.send_notification(nh, tags)

    def send_mpns_notification(self, payload, tags=""):
        nh = Notification("windowsphone", payload)

        if "<wp:Toast>" in payload:
            nh.headers = {'X-WindowsPhone-Target': 'toast', 'X-NotificationClass': '2'}
        elif "<wp:Tile>" in payload:
            nh.headers = {'X-WindowsPhone-Target': 'tile', 'X-NotificationClass': '1'}

        self.send_notification(nh, tags)

    def send_windows_notification(self, payload, tags=""):
        nh = Notification("windows", payload)

        if "<toast>" in payload:
            nh.headers = {'X-WNS-Type': 'wns/toast'}
        elif "<tile>" in payload:
            nh.headers = {'X-WNS-Type': 'wns/tile'}
        elif "<badge>" in payload:
            nh.headers = {'X-WNS-Type': 'wns/badge'}

        self.send_notification(nh, tags)

    def send_template_notification(self, properties, tags=""):
        nh = Notification("template", properties)
        self.send_notification(nh, tags)

Hello выше методы отправки HTTP POST запроса toohello /messages конечной точки с телом правильный hello и заголовки toosend hello уведомления центра уведомлений.

### <a name="using-debug-property-tooenable-detailed-logging"></a>С помощью свойства tooenable отладки подробные журналы
Включение отладки свойства во время инициализации hello концентратор уведомлений будет записи подробное ведение журнала сведений о hello HTTP запроса и ответа дампа, а также подробные сообщения уведомления отправить результат. Недавно мы добавили это свойство с именем [TestSend концентраторы уведомлений свойство](http://msdn.microsoft.com/library/microsoft.servicebus.notifications.notificationhubclient.enabletestsend.aspx) которого возвращает подробные сведения о hello отправки уведомлений. toouse его - инициализировать с помощью следующих hello:

    hub = NotificationHub("myConnectionString", "myNotificationHubName", isDebug)

Hello уведомление концентратора отправить запрос HTTP URL-адрес в результате пополняется с querystring «test». 

## <a name="complete-tutorial"></a>Учебник завершения hello
Теперь можно завершить учебника приступить к работе hello путем отправки уведомления hello из внутренней Python.

Инициализировать концентраторы уведомлений клиента (замените имя концентратора и строка соединения hello, как описано в hello [учебника запущенную Get]):

    hub = NotificationHub("myConnectionString", "myNotificationHubName")

Затем добавьте код отправки hello в зависимости от целевой платформы мобильных устройств. В этом примере также добавляет выше tooenable методы уровня отправки уведомлений на основе платформы hello например send_windows_notification для windows; send_apple_notification (для apple) и т. д. 

### <a name="windows-store-and-windows-phone-81-non-silverlight"></a>Магазин Windows и Windows Phone 8.1 (без Silverlight)
    wns_payload = """<toast><visual><binding template=\"ToastText01\"><text id=\"1\">Test</text></binding></visual></toast>"""
    hub.send_windows_notification(wns_payload)

### <a name="windows-phone-80-and-81-silverlight"></a>Windows Phone 8.0 и 8.1 Silverlight
    hub.send_mpns_notification(toast)

### <a name="ios"></a>iOS
    alert_payload = {
        'data':
            {
                'msg': 'Hello!'
            }
    }
    hub.send_apple_notification(alert_payload)

### <a name="android"></a>Android
    gcm_payload = {
        'data':
            {
                'msg': 'Hello!'
            }
    }
    hub.send_gcm_notification(gcm_payload)

### <a name="kindle-fire"></a>Kindle Fire
    adm_payload = {
        'data':
            {
                'msg': 'Hello!'
            }
    }
    hub.send_adm_notification(adm_payload)

### <a name="baidu"></a>Baidu
    baidu_payload = {
        'data':
            {
                'msg': 'Hello!'
            }
    }
    hub.send_baidu_notification(baidu_payload)

После выполнения кода Python на целевом устройстве должно отобразиться уведомление.

## <a name="examples"></a>Примеры:
### <a name="enabling-debug-property"></a>Включение свойства отладки
При включении флаг отладки во время инициализации hello концентратора уведомлений, то вы увидите подробные дампа запросов и ответов HTTP, а также NotificationOutcome следующего вида hello, где можно понять, какие заголовки HTTP, передаются в запрос hello и какие HTTP получен отклик от hello концентратора уведомлений:![][1]

Вы увидите подробный результат концентратора уведомлений, например сведения о том, 

* Когда сообщение hello успешной отправки toohello службы Push-уведомлений. 
  
        <Outcome>hello Notification was successfully sent toohello Push Notification System</Outcome>
* При наличии не найдены цели для push-уведомления, то скорее всего будет ниже toosee hello в ответ hello (который указывает на наличие регистраций найден toodeliver hello уведомления, скорее всего, так как некоторые hello регистраций несоответствие тегов)
  
        '<NotificationOutcome xmlns="http://schemas.microsoft.com/netservices/2010/10/servicebus/connect" xmlns:i="http://www.w3.org/2001/XMLSchema-instance"><Success>0</Success><Failure>0</Failure><Results i:nil="true"/></NotificationOutcome>'

### <a name="broadcast-toast-notification-toowindows"></a>Всплывающие уведомления tooWindows широковещательных пакетов
Обратите внимание, hello заголовки, которые отправляются out при отправке клиент tooWindows широковещательных всплывающих уведомлений. 

    hub.send_windows_notification(wns_payload)

![][2]

### <a name="send-notification-specifying-a-tag-or-tag-expression"></a>Отправка уведомления с указанием тега (или регулярного выражения)
Обратите внимание hello HTTP теги заголовок, который будет добавлен и toohello HTTP-запроса (в следующем примере hello, мы отправляете hello уведомления только tooregistrations с полезными данными «Спорт»)

    hub.send_windows_notification(wns_payload, "sports")

![][3]

### <a name="send-notification-specifying-multiple-tags"></a>Отправка уведомления с указанием нескольких тегов
Обратите внимание на то, как заголовок HTTP теги hello изменяется при отправке несколько тегов. 

    tags = {'sports', 'politics'}
    hub.send_windows_notification(wns_payload, tags)

![][4]

### <a name="templated-notification"></a>Шаблон уведомления
Обратите внимание, что hello изменения формата HTTP-заголовка и полезных данных текст hello отправляется как часть текста hello HTTP-запроса.

**Сторона клиента — зарегистрированный шаблон**

        var template =
                        @"<toast><visual><binding template=""ToastText01""><text id=""1"">$(greeting_en)</text></binding></visual></toast>";

**Серверный - Отправка hello полезных данных**

        template_payload = {'greeting_en': 'Hello', 'greeting_fr': 'Salut'}
        hub.send_template_notification(template_payload)

![][5]

## <a name="next-steps"></a>Дальнейшие действия
В этом разделе мы показали, как toocreate простой Python REST клиента для концентраторов уведомлений. На данном этапе можно сделать следующее.

* Hello полной загрузки [образца программы-оболочки Python REST], который содержит весь код hello выше.
* Продолжить изучение теги в hello функции концентраторов уведомлений [учебника последние новости]
* Продолжить изучение компонентов шаблоны концентраторов уведомлений в hello [учебника локализация новостей]

<!-- URLs -->
[образца программы-оболочки Python REST]: https://github.com/Azure/azure-notificationhubs-samples/tree/master/notificationhubs-rest-python
[учебника запущенную Get]: http://azure.microsoft.com/documentation/articles/notification-hubs-windows-store-dotnet-get-started/
[учебника последние новости]: http://azure.microsoft.com/documentation/articles/notification-hubs-windows-store-dotnet-send-breaking-news/
[учебника локализация новостей]: http://azure.microsoft.com/documentation/articles/notification-hubs-windows-store-dotnet-send-localized-breaking-news/

<!-- Images. -->
[1]: ./media/notification-hubs-python-backend-how-to/DetailedLoggingInfo.png
[2]: ./media/notification-hubs-python-backend-how-to/BroadcastScenario.png
[3]: ./media/notification-hubs-python-backend-how-to/SendWithOneTag.png
[4]: ./media/notification-hubs-python-backend-how-to/SendWithMultipleTags.png
[5]: ./media/notification-hubs-python-backend-how-to/TemplatedNotification.png

