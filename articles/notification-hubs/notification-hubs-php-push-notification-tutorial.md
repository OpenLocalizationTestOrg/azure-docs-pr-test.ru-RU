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
# <a name="how-toouse-notification-hubs-from-php"></a><span data-ttu-id="98e8b-103">Как toouse концентраторы уведомлений из PHP</span><span class="sxs-lookup"><span data-stu-id="98e8b-103">How toouse Notification Hubs from PHP</span></span>
[!INCLUDE [notification-hubs-backend-how-to-selector](../../includes/notification-hubs-backend-how-to-selector.md)]

<span data-ttu-id="98e8b-104">Из внутренней Java, PHP и Ruby доступны все функции концентраторов уведомлений с помощью интерфейса REST концентратора уведомлений hello, как описано в разделе MSDN hello [интерфейсы API REST концентраторов уведомлений](http://msdn.microsoft.com/library/dn223264.aspx).</span><span class="sxs-lookup"><span data-stu-id="98e8b-104">You can access all Notification Hubs features from a Java/PHP/Ruby back-end using hello Notification Hub REST interface as described in hello MSDN topic [Notification Hubs REST APIs](http://msdn.microsoft.com/library/dn223264.aspx).</span></span>

<span data-ttu-id="98e8b-105">В этом разделе описывается:</span><span class="sxs-lookup"><span data-stu-id="98e8b-105">In this topic we show how to:</span></span>

* <span data-ttu-id="98e8b-106">построение клиента REST для функций концентраторов уведомлений на PHP;</span><span class="sxs-lookup"><span data-stu-id="98e8b-106">Build a REST client for Notification Hubs features in PHP;</span></span>
* <span data-ttu-id="98e8b-107">Выполните hello [учебника запущенную Get](notification-hubs-ios-apple-push-notification-apns-get-started.md) для вашей платформы мобильных устройств по выбору, реализация hello серверную часть в PHP.</span><span class="sxs-lookup"><span data-stu-id="98e8b-107">Follow hello [Get started tutorial](notification-hubs-ios-apple-push-notification-apns-get-started.md) for your mobile platform of choice, implementing hello back-end portion in PHP.</span></span>

## <a name="client-interface"></a><span data-ttu-id="98e8b-108">Интерфейс клиента</span><span class="sxs-lookup"><span data-stu-id="98e8b-108">Client interface</span></span>
<span data-ttu-id="98e8b-109">Hello основного клиентского интерфейса предоставляет hello же методы, доступные в hello [.NET SDK концентраторы уведомлений](http://msdn.microsoft.com/library/jj933431.aspx), это позволит вам toodirectly перевести все hello учебники и образцы, доступных в настоящее время этот сайт и hello сообщества hello, представленные Интернета.</span><span class="sxs-lookup"><span data-stu-id="98e8b-109">hello main client interface can provide hello same methods that are available in hello [.NET Notification Hubs SDK](http://msdn.microsoft.com/library/jj933431.aspx), this will allow you toodirectly translate all hello tutorials and samples currently available on this site, and contributed by hello community on hello internet.</span></span>

<span data-ttu-id="98e8b-110">Можно найти все доступные в hello кода hello [образца программы-оболочки PHP REST].</span><span class="sxs-lookup"><span data-stu-id="98e8b-110">You can find all hello code available in hello [PHP REST wrapper sample].</span></span>

<span data-ttu-id="98e8b-111">Например toocreate клиента:</span><span class="sxs-lookup"><span data-stu-id="98e8b-111">For example, toocreate a client:</span></span>

    $hub = new NotificationHub("connection string", "hubname");    

<span data-ttu-id="98e8b-112">toosend уведомление о собственном iOS:</span><span class="sxs-lookup"><span data-stu-id="98e8b-112">toosend an iOS native notification:</span></span>

    $notification = new Notification("apple", '{"aps":{"alert": "Hello!"}}');
    $hub->sendNotification($notification, null);

## <a name="implementation"></a><span data-ttu-id="98e8b-113">Реализация</span><span class="sxs-lookup"><span data-stu-id="98e8b-113">Implementation</span></span>
<span data-ttu-id="98e8b-114">Если вы еще не сделали, выполните наши [учебника запущенную Get] вверх toohello последний раздел, при наличии tooimplement hello серверной части.</span><span class="sxs-lookup"><span data-stu-id="98e8b-114">If you did not already, please follow our [Get started tutorial] up toohello last section where you have tooimplement hello back-end.</span></span>
<span data-ttu-id="98e8b-115">Кроме того, если требуется, можно использовать код hello из hello [образца программы-оболочки PHP REST] и перейти непосредственно toohello [завершения hello учебника](#complete-tutorial) раздела.</span><span class="sxs-lookup"><span data-stu-id="98e8b-115">Also, if you want you can use hello code from hello [PHP REST wrapper sample] and go directly toohello [Complete hello tutorial](#complete-tutorial) section.</span></span>

<span data-ttu-id="98e8b-116">Здравствуйте, все сведения tooimplement полный оболочки REST можно найти на [MSDN](http://msdn.microsoft.com/library/dn530746.aspx).</span><span class="sxs-lookup"><span data-stu-id="98e8b-116">All hello details tooimplement a full REST wrapper can be found on [MSDN](http://msdn.microsoft.com/library/dn530746.aspx).</span></span> <span data-ttu-id="98e8b-117">В этом разделе описывается реализация PHP hello hello основных шагов требуется tooaccess конечные точки REST концентраторов уведомлений:</span><span class="sxs-lookup"><span data-stu-id="98e8b-117">In this section we will describe hello PHP implementation of hello main steps required tooaccess Notification Hubs REST endpoints:</span></span>

1. <span data-ttu-id="98e8b-118">Синтаксический анализ строки соединения hello</span><span class="sxs-lookup"><span data-stu-id="98e8b-118">Parse hello connection string</span></span>
2. <span data-ttu-id="98e8b-119">Создание маркера авторизации hello</span><span class="sxs-lookup"><span data-stu-id="98e8b-119">Generate hello authorization token</span></span>
3. <span data-ttu-id="98e8b-120">Выполнить вызов hello HTTP</span><span class="sxs-lookup"><span data-stu-id="98e8b-120">Perform hello HTTP call</span></span>

### <a name="parse-hello-connection-string"></a><span data-ttu-id="98e8b-121">Синтаксический анализ строки соединения hello</span><span class="sxs-lookup"><span data-stu-id="98e8b-121">Parse hello connection string</span></span>
<span data-ttu-id="98e8b-122">Вот hello Главный класс реализации hello клиента, конструктор которого выполняет синтаксический анализ строки соединения hello.</span><span class="sxs-lookup"><span data-stu-id="98e8b-122">Here is hello main class implementing hello client, whose constructor that parses hello connection string:</span></span>

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


### <a name="create-security-token"></a><span data-ttu-id="98e8b-123">Создание маркера безопасности</span><span class="sxs-lookup"><span data-stu-id="98e8b-123">Create security token</span></span>
<span data-ttu-id="98e8b-124">доступны Hello сведения для создания маркера безопасности hello [здесь](http://msdn.microsoft.com/library/dn495627.aspx).</span><span class="sxs-lookup"><span data-stu-id="98e8b-124">hello details of hello security token creation are available [here](http://msdn.microsoft.com/library/dn495627.aspx).</span></span>
<span data-ttu-id="98e8b-125">Hello следующий метод был добавлен toobe toohello **концентратора уведомлений** класса toocreate hello токены на hello URI текущего запроса hello и hello учетные данные, извлеченные из строки подключения hello.</span><span class="sxs-lookup"><span data-stu-id="98e8b-125">hello following method has toobe added toohello **NotificationHub** class toocreate hello token based on hello URI of hello current request and hello credentials extracted from hello connection string.</span></span>

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

### <a name="send-a-notification"></a><span data-ttu-id="98e8b-126">Отправка уведомления</span><span class="sxs-lookup"><span data-stu-id="98e8b-126">Send a notification</span></span>
<span data-ttu-id="98e8b-127">Сначала следует определить класс, представляющий уведомление.</span><span class="sxs-lookup"><span data-stu-id="98e8b-127">First, let us define a class representing a notification.</span></span>

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

<span data-ttu-id="98e8b-128">Этот класс представляет собой контейнер для собственного тела уведомления, либо набор свойств, в случае с шаблонным уведомлением, а также набор заголовков, содержащих свойства формата (собственная платформа или шаблон) и специальные свойства платформы (например, свойство срока действия Apple и заголовки WNS).</span><span class="sxs-lookup"><span data-stu-id="98e8b-128">This class is a container for a native notification body, or a set of properties on case of a template notification, and a set of headers which contains format (native platform or template) and platform-specific properties (like Apple expiration property and WNS headers).</span></span>

<span data-ttu-id="98e8b-129">См. toohello [документации по API-интерфейс REST концентраторов уведомлений](http://msdn.microsoft.com/library/dn495827.aspx) и hello форматы уведомлений платформы для всех hello доступные параметры.</span><span class="sxs-lookup"><span data-stu-id="98e8b-129">Please refer toohello [Notification Hubs REST APIs documentation](http://msdn.microsoft.com/library/dn495827.aspx) and hello specific notification platforms' formats for all hello options available.</span></span>

<span data-ttu-id="98e8b-130">Используя этот класс, теперь можно написать отправки hello методы уведомления внутри hello **концентратора уведомлений** класса.</span><span class="sxs-lookup"><span data-stu-id="98e8b-130">Armed with this class, we can now write hello send notification methods inside of hello **NotificationHub** class.</span></span>

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

<span data-ttu-id="98e8b-131">Hello выше методы отправки HTTP POST запроса toohello /messages конечной точки с телом правильный hello и заголовки toosend hello уведомления центра уведомлений.</span><span class="sxs-lookup"><span data-stu-id="98e8b-131">hello above methods send an HTTP POST request toohello /messages endpoint of your notification hub, with hello correct body and headers toosend hello notification.</span></span>

## <span data-ttu-id="98e8b-132"><a name="complete-tutorial"></a>Учебник завершения hello</span><span class="sxs-lookup"><span data-stu-id="98e8b-132"><a name="complete-tutorial"></a>Complete hello tutorial</span></span>
<span data-ttu-id="98e8b-133">Теперь можно завершить учебника приступить к работе hello путем отправки уведомления hello из внутренней PHP.</span><span class="sxs-lookup"><span data-stu-id="98e8b-133">Now you can complete hello Get Started tutorial by sending hello notification from a PHP back-end.</span></span>

<span data-ttu-id="98e8b-134">Инициализировать концентраторы уведомлений клиента (замените имя концентратора и строка соединения hello, как описано в hello [учебника запущенную Get]):</span><span class="sxs-lookup"><span data-stu-id="98e8b-134">Initialize your Notification Hubs client (substitute hello connection string and hub name as instructed in hello [Get started tutorial]):</span></span>

    $hub = new NotificationHub("connection string", "hubname");    

<span data-ttu-id="98e8b-135">Затем добавьте код отправки hello в зависимости от целевой платформы мобильных устройств.</span><span class="sxs-lookup"><span data-stu-id="98e8b-135">Then add hello send code depending on your target mobile platform.</span></span>

### <a name="windows-store-and-windows-phone-81-non-silverlight"></a><span data-ttu-id="98e8b-136">Магазин Windows и Windows Phone 8.1 (без Silverlight)</span><span class="sxs-lookup"><span data-stu-id="98e8b-136">Windows Store and Windows Phone 8.1 (non-Silverlight)</span></span>
    $toast = '<toast><visual><binding template="ToastText01"><text id="1">Hello from PHP!</text></binding></visual></toast>';
    $notification = new Notification("windows", $toast);
    $notification->headers[] = 'X-WNS-Type: wns/toast';
    $hub->sendNotification($notification, null);

### <a name="ios"></a><span data-ttu-id="98e8b-137">iOS</span><span class="sxs-lookup"><span data-stu-id="98e8b-137">iOS</span></span>
    $alert = '{"aps":{"alert":"Hello from PHP!"}}';
    $notification = new Notification("apple", $alert);
    $hub->sendNotification($notification, null);

### <a name="android"></a><span data-ttu-id="98e8b-138">Android</span><span class="sxs-lookup"><span data-stu-id="98e8b-138">Android</span></span>
    $message = '{"data":{"msg":"Hello from PHP!"}}';
    $notification = new Notification("gcm", $message);
    $hub->sendNotification($notification, null);

### <a name="windows-phone-80-and-81-silverlight"></a><span data-ttu-id="98e8b-139">Windows Phone 8.0 и 8.1 Silverlight</span><span class="sxs-lookup"><span data-stu-id="98e8b-139">Windows Phone 8.0 and 8.1 Silverlight</span></span>
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


### <a name="kindle-fire"></a><span data-ttu-id="98e8b-140">Kindle Fire</span><span class="sxs-lookup"><span data-stu-id="98e8b-140">Kindle Fire</span></span>
    $message = '{"data":{"msg":"Hello from PHP!"}}';
    $notification = new Notification("adm", $message);
    $hub->sendNotification($notification, null);

<span data-ttu-id="98e8b-141">После выполнения кода PHP на целевом устройстве должно отобразиться уведомление.</span><span class="sxs-lookup"><span data-stu-id="98e8b-141">Running your PHP code should produce now a notification appearing on your target device.</span></span>

## <a name="next-steps"></a><span data-ttu-id="98e8b-142">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="98e8b-142">Next Steps</span></span>
<span data-ttu-id="98e8b-143">В этом разделе мы показали, как toocreate простой Java REST клиента для концентраторов уведомлений.</span><span class="sxs-lookup"><span data-stu-id="98e8b-143">In this topic we showed how toocreate a simple Java REST client for Notification Hubs.</span></span> <span data-ttu-id="98e8b-144">На данном этапе можно сделать следующее.</span><span class="sxs-lookup"><span data-stu-id="98e8b-144">From here you can:</span></span>

* <span data-ttu-id="98e8b-145">Загрузить полный hello [образца программы-оболочки PHP REST], который содержит все приведенный выше код hello.</span><span class="sxs-lookup"><span data-stu-id="98e8b-145">Download hello full [PHP REST wrapper sample], which contains all hello code above.</span></span>
* <span data-ttu-id="98e8b-146">Продолжить изучение теги в hello [новостями учебник] функции концентраторов уведомлений</span><span class="sxs-lookup"><span data-stu-id="98e8b-146">Continue learning about Notification Hubs tagging feature in hello [Breaking News tutorial]</span></span>
* <span data-ttu-id="98e8b-147">Дополнительные сведения о принудительной отправке уведомлений tooindividual пользователей в [уведомить пользователей учебник]</span><span class="sxs-lookup"><span data-stu-id="98e8b-147">Learn about pushing notifications tooindividual users in [Notify Users tutorial]</span></span>

<span data-ttu-id="98e8b-148">Дополнительные сведения см. также: hello [Центр разработчика PHP](/develop/php/).</span><span class="sxs-lookup"><span data-stu-id="98e8b-148">For more information, see also hello [PHP Developer Center](/develop/php/).</span></span>

[образца программы-оболочки PHP REST]: https://github.com/Azure/azure-notificationhubs-samples/tree/master/notificationhubs-rest-php
[учебника запущенную Get]: http://azure.microsoft.com/documentation/articles/notification-hubs-ios-get-started/

