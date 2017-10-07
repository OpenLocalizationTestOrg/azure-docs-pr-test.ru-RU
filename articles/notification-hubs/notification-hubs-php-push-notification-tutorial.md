---
title: "aaaHow toouse концентраторов уведомлений с PHP"
description: "Узнайте, как toouse концентраторов уведомлений Azure из внутренней PHP."
services: notification-hubs
documentationcenter: 
author: ysxu
manager: erikre
editor: 
ms.assetid: 0156f994-96d0-4878-b07b-49b7be4fd856
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: php
ms.devlang: php
ms.topic: article
ms.date: 06/07/2016
ms.author: yuaxu
ms.openlocfilehash: 6cd426286a684006a07867fcf44a8ff71be7efa8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-notification-hubs-from-php"></a>Как toouse концентраторы уведомлений из PHP
[!INCLUDE [notification-hubs-backend-how-to-selector](../../includes/notification-hubs-backend-how-to-selector.md)]

Из внутренней Java, PHP и Ruby доступны все функции концентраторов уведомлений с помощью интерфейса REST концентратора уведомлений hello, как описано в разделе MSDN hello [интерфейсы API REST концентраторов уведомлений](http://msdn.microsoft.com/library/dn223264.aspx).

В этом разделе описывается:

* построение клиента REST для функций концентраторов уведомлений на PHP;
* Выполните hello [учебника запущенную Get](notification-hubs-ios-apple-push-notification-apns-get-started.md) для вашей платформы мобильных устройств по выбору, реализация hello серверную часть в PHP.

## <a name="client-interface"></a>Интерфейс клиента
Hello основного клиентского интерфейса предоставляет hello же методы, доступные в hello [.NET SDK концентраторы уведомлений](http://msdn.microsoft.com/library/jj933431.aspx), это позволит вам toodirectly перевести все hello учебники и образцы, доступных в настоящее время этот сайт и hello сообщества hello, представленные Интернета.

Можно найти все доступные в hello кода hello [образца программы-оболочки PHP REST].

Например toocreate клиента:

    $hub = new NotificationHub("connection string", "hubname");    

toosend уведомление о собственном iOS:

    $notification = new Notification("apple", '{"aps":{"alert": "Hello!"}}');
    $hub->sendNotification($notification, null);

## <a name="implementation"></a>Реализация
Если вы еще не сделали, выполните наши [учебника запущенную Get] вверх toohello последний раздел, при наличии tooimplement hello серверной части.
Кроме того, если требуется, можно использовать код hello из hello [образца программы-оболочки PHP REST] и перейти непосредственно toohello [завершения hello учебника](#complete-tutorial) раздела.

Здравствуйте, все сведения tooimplement полный оболочки REST можно найти на [MSDN](http://msdn.microsoft.com/library/dn530746.aspx). В этом разделе описывается реализация PHP hello hello основных шагов требуется tooaccess конечные точки REST концентраторов уведомлений:

1. Синтаксический анализ строки соединения hello
2. Создание маркера авторизации hello
3. Выполнить вызов hello HTTP

### <a name="parse-hello-connection-string"></a>Синтаксический анализ строки соединения hello
Вот hello Главный класс реализации hello клиента, конструктор которого выполняет синтаксический анализ строки соединения hello.

    class NotificationHub {
        const API_VERSION = "?api-version=2013-10";

        private $endpoint;
        private $hubPath;
        private $sasKeyName;
        private $sasKeyValue;

        function __construct($connectionString, $hubPath) {
            $this->hubPath = $hubPath;

            $this->parseConnectionString($connectionString);
        }

        private function parseConnectionString($connectionString) {
            $parts = explode(";", $connectionString);
            if (sizeof($parts) != 3) {
                throw new Exception("Error parsing connection string: " . $connectionString);
            }

            foreach ($parts as $part) {
                if (strpos($part, "Endpoint") === 0) {
                    $this->endpoint = "https" . substr($part, 11);
                } else if (strpos($part, "SharedAccessKeyName") === 0) {
                    $this->sasKeyName = substr($part, 20);
                } else if (strpos($part, "SharedAccessKey") === 0) {
                    $this->sasKeyValue = substr($part, 16);
                }
            }
        }
    }


### <a name="create-security-token"></a>Создание маркера безопасности
доступны Hello сведения для создания маркера безопасности hello [здесь](http://msdn.microsoft.com/library/dn495627.aspx).
Hello следующий метод был добавлен toobe toohello **концентратора уведомлений** класса toocreate hello токены на hello URI текущего запроса hello и hello учетные данные, извлеченные из строки подключения hello.

    private function generateSasToken($uri) {
        $targetUri = strtolower(rawurlencode(strtolower($uri)));

        $expires = time();
        $expiresInMins = 60;
        $expires = $expires + $expiresInMins * 60;
        $toSign = $targetUri . "\n" . $expires;

        $signature = rawurlencode(base64_encode(hash_hmac('sha256', $toSign, $this->sasKeyValue, TRUE)));

        $token = "SharedAccessSignature sr=" . $targetUri . "&sig="
                    . $signature . "&se=" . $expires . "&skn=" . $this->sasKeyName;

        return $token;
    }

### <a name="send-a-notification"></a>Отправка уведомления
Сначала следует определить класс, представляющий уведомление.

    class Notification {
        public $format;
        public $payload;

        # array with keynames for headers
        # Note: Some headers are mandatory: Windows: X-WNS-Type, WindowsPhone: X-NotificationType
        # Note: For Apple you can set Expiry with header: ServiceBusNotification-ApnsExpiry in W3C DTF, YYYY-MM-DDThh:mmTZD (for example, 1997-07-16T19:20+01:00).
        public $headers;

        function __construct($format, $payload) {
            if (!in_array($format, ["template", "apple", "windows", "gcm", "windowsphone"])) {
                throw new Exception('Invalid format: ' . $format);
            }

            $this->format = $format;
            $this->payload = $payload;
        }
    }

Этот класс представляет собой контейнер для собственного тела уведомления, либо набор свойств, в случае с шаблонным уведомлением, а также набор заголовков, содержащих свойства формата (собственная платформа или шаблон) и специальные свойства платформы (например, свойство срока действия Apple и заголовки WNS).

См. toohello [документации по API-интерфейс REST концентраторов уведомлений](http://msdn.microsoft.com/library/dn495827.aspx) и hello форматы уведомлений платформы для всех hello доступные параметры.

Используя этот класс, теперь можно написать отправки hello методы уведомления внутри hello **концентратора уведомлений** класса.

    public function sendNotification($notification, $tagsOrTagExpression="") {
        if (is_array($tagsOrTagExpression)) {
            $tagExpression = implode(" || ", $tagsOrTagExpression);
        } else {
            $tagExpression = $tagsOrTagExpression;
        }

        # build uri
        $uri = $this->endpoint . $this->hubPath . "/messages" . NotificationHub::API_VERSION;
        $ch = curl_init($uri);

        if (in_array($notification->format, ["template", "apple", "gcm"])) {
            $contentType = "application/json";
        } else {
            $contentType = "application/xml";
        }

        $token = $this->generateSasToken($uri);

        $headers = [
            'Authorization: '.$token,
            'Content-Type: '.$contentType,
            'ServiceBusNotification-Format: '.$notification->format
        ];

        if ("" !== $tagExpression) {
            $headers[] = 'ServiceBusNotification-Tags: '.$tagExpression;
        }

        # add headers for other platforms
        if (is_array($notification->headers)) {
            $headers = array_merge($headers, $notification->headers);
        }

        curl_setopt_array($ch, array(
            CURLOPT_POST => TRUE,
            CURLOPT_RETURNTRANSFER => TRUE,
            CURLOPT_SSL_VERIFYPEER => FALSE,
            CURLOPT_HTTPHEADER => $headers,
            CURLOPT_POSTFIELDS => $notification->payload
        ));

        // Send hello request
        $response = curl_exec($ch);

        // Check for errors
        if($response === FALSE){
            throw new Exception(curl_error($ch));
        }

        $info = curl_getinfo($ch);

        if ($info['http_code'] <> 201) {
            throw new Exception('Error sending notificaiton: '. $info['http_code'] . ' msg: ' . $response);
        }
    } 

Hello выше методы отправки HTTP POST запроса toohello /messages конечной точки с телом правильный hello и заголовки toosend hello уведомления центра уведомлений.

## <a name="complete-tutorial"></a>Учебник завершения hello
Теперь можно завершить учебника приступить к работе hello путем отправки уведомления hello из внутренней PHP.

Инициализировать концентраторы уведомлений клиента (замените имя концентратора и строка соединения hello, как описано в hello [учебника запущенную Get]):

    $hub = new NotificationHub("connection string", "hubname");    

Затем добавьте код отправки hello в зависимости от целевой платформы мобильных устройств.

### <a name="windows-store-and-windows-phone-81-non-silverlight"></a>Магазин Windows и Windows Phone 8.1 (без Silverlight)
    $toast = '<toast><visual><binding template="ToastText01"><text id="1">Hello from PHP!</text></binding></visual></toast>';
    $notification = new Notification("windows", $toast);
    $notification->headers[] = 'X-WNS-Type: wns/toast';
    $hub->sendNotification($notification, null);

### <a name="ios"></a>iOS
    $alert = '{"aps":{"alert":"Hello from PHP!"}}';
    $notification = new Notification("apple", $alert);
    $hub->sendNotification($notification, null);

### <a name="android"></a>Android
    $message = '{"data":{"msg":"Hello from PHP!"}}';
    $notification = new Notification("gcm", $message);
    $hub->sendNotification($notification, null);

### <a name="windows-phone-80-and-81-silverlight"></a>Windows Phone 8.0 и 8.1 Silverlight
    $toast = '<?xml version="1.0" encoding="utf-8"?>' .
                '<wp:Notification xmlns:wp="WPNotification">' .
                   '<wp:Toast>' .
                        '<wp:Text1>Hello from PHP!</wp:Text1>' .
                   '</wp:Toast> ' .
                '</wp:Notification>';
    $notification = new Notification("windowsphone", $toast);
    $notification->headers[] = 'X-WindowsPhone-Target : toast';
    $notification->headers[] = 'X-NotificationClass : 2';
    $hub->sendNotification($notification, null);


### <a name="kindle-fire"></a>Kindle Fire
    $message = '{"data":{"msg":"Hello from PHP!"}}';
    $notification = new Notification("adm", $message);
    $hub->sendNotification($notification, null);

После выполнения кода PHP на целевом устройстве должно отобразиться уведомление.

## <a name="next-steps"></a>Дальнейшие действия
В этом разделе мы показали, как toocreate простой Java REST клиента для концентраторов уведомлений. На данном этапе можно сделать следующее.

* Загрузить полный hello [образца программы-оболочки PHP REST], который содержит все приведенный выше код hello.
* Продолжить изучение теги в hello [новостями учебник] функции концентраторов уведомлений
* Дополнительные сведения о принудительной отправке уведомлений tooindividual пользователей в [уведомить пользователей учебник]

Дополнительные сведения см. также: hello [Центр разработчика PHP](/develop/php/).

[образца программы-оболочки PHP REST]: https://github.com/Azure/azure-notificationhubs-samples/tree/master/notificationhubs-rest-php
[учебника запущенную Get]: http://azure.microsoft.com/documentation/articles/notification-hubs-ios-get-started/

