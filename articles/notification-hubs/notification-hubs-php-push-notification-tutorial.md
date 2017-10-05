---
title: "Использование концентраторов уведомлений с PHP"
description: "Узнайте, как использовать центры уведомлений Azure из серверной части PHP."
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
ms.openlocfilehash: c27b6308ff528224a0398e0ff40537db05417bb0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-notification-hubs-from-php"></a><span data-ttu-id="2446e-103">Использование концентраторов уведомлений из PHP</span><span class="sxs-lookup"><span data-stu-id="2446e-103">How to use Notification Hubs from PHP</span></span>
[!INCLUDE [notification-hubs-backend-how-to-selector](../../includes/notification-hubs-backend-how-to-selector.md)]

<span data-ttu-id="2446e-104">Вы можете обращаться ко всем функциям концентраторов уведомлений из серверной части Java/PHP/Ruby, используя интерфейс REST концентраторов уведомлений в соответствии с описанием в разделе MSDN [Интерфейсы REST концентраторов уведомлений](http://msdn.microsoft.com/library/dn223264.aspx).</span><span class="sxs-lookup"><span data-stu-id="2446e-104">You can access all Notification Hubs features from a Java/PHP/Ruby back-end using the Notification Hub REST interface as described in the MSDN topic [Notification Hubs REST APIs](http://msdn.microsoft.com/library/dn223264.aspx).</span></span>

<span data-ttu-id="2446e-105">В этом разделе описывается:</span><span class="sxs-lookup"><span data-stu-id="2446e-105">In this topic we show how to:</span></span>

* <span data-ttu-id="2446e-106">построение клиента REST для функций концентраторов уведомлений на PHP;</span><span class="sxs-lookup"><span data-stu-id="2446e-106">Build a REST client for Notification Hubs features in PHP;</span></span>
* <span data-ttu-id="2446e-107">использование [Учебника по началу работы](notification-hubs-ios-apple-push-notification-apns-get-started.md) с выбранной мобильной платформой, реализация серверной части на PHP.</span><span class="sxs-lookup"><span data-stu-id="2446e-107">Follow the [Get started tutorial](notification-hubs-ios-apple-push-notification-apns-get-started.md) for your mobile platform of choice, implementing the back-end portion in PHP.</span></span>

## <a name="client-interface"></a><span data-ttu-id="2446e-108">Интерфейс клиента</span><span class="sxs-lookup"><span data-stu-id="2446e-108">Client interface</span></span>
<span data-ttu-id="2446e-109">Основной интерфейс клиента может предоставлять те же методы, которые доступны в [пакете SDK Центров уведомлений .NET](http://msdn.microsoft.com/library/jj933431.aspx). Это позволяет напрямую переводить все руководства и примеры, доступные на этом сайте в настоящий момент и пополняемые интернет-сообществом.</span><span class="sxs-lookup"><span data-stu-id="2446e-109">The main client interface can provide the same methods that are available in the [.NET Notification Hubs SDK](http://msdn.microsoft.com/library/jj933431.aspx), this will allow you to directly translate all the tutorials and samples currently available on this site, and contributed by the community on the internet.</span></span>

<span data-ttu-id="2446e-110">Весь доступный код находится в [примера оболочки REST PHP].</span><span class="sxs-lookup"><span data-stu-id="2446e-110">You can find all the code available in the [PHP REST wrapper sample].</span></span>

<span data-ttu-id="2446e-111">Например, чтобы создать клиента, необходимо выполнить следующие действия.</span><span class="sxs-lookup"><span data-stu-id="2446e-111">For example, to create a client:</span></span>

    $hub = new NotificationHub("connection string", "hubname");    

<span data-ttu-id="2446e-112">Отправка собственного уведомления iOS.</span><span class="sxs-lookup"><span data-stu-id="2446e-112">To send an iOS native notification:</span></span>

    $notification = new Notification("apple", '{"aps":{"alert": "Hello!"}}');
    $hub->sendNotification($notification, null);

## <a name="implementation"></a><span data-ttu-id="2446e-113">Реализация</span><span class="sxs-lookup"><span data-stu-id="2446e-113">Implementation</span></span>
<span data-ttu-id="2446e-114">Если вы еще этого не делали, выполните шаги, описанные в [учебнике по началу работы] , до последнего раздела, в котором вам нужно реализовать серверную часть.</span><span class="sxs-lookup"><span data-stu-id="2446e-114">If you did not already, please follow our [Get started tutorial] up to the last section where you have to implement the back-end.</span></span>
<span data-ttu-id="2446e-115">Кроме того, при необходимости можно воспользоваться кодом из [примера оболочки REST PHP] и перейти непосредственно к разделу [Завершение работы с руководством](#complete-tutorial).</span><span class="sxs-lookup"><span data-stu-id="2446e-115">Also, if you want you can use the code from the [PHP REST wrapper sample] and go directly to the [Complete the tutorial](#complete-tutorial) section.</span></span>

<span data-ttu-id="2446e-116">Подробные сведения о реализации полноценной оболочки REST можно найти в [MSDN](http://msdn.microsoft.com/library/dn530746.aspx).</span><span class="sxs-lookup"><span data-stu-id="2446e-116">All the details to implement a full REST wrapper can be found on [MSDN](http://msdn.microsoft.com/library/dn530746.aspx).</span></span> <span data-ttu-id="2446e-117">В этом разделе описывается реализация основных действий на PHP, необходимых для доступа к конечным точкам REST концентраторов уведомлений.</span><span class="sxs-lookup"><span data-stu-id="2446e-117">In this section we will describe the PHP implementation of the main steps required to access Notification Hubs REST endpoints:</span></span>

1. <span data-ttu-id="2446e-118">Проанализируйте строку подключения</span><span class="sxs-lookup"><span data-stu-id="2446e-118">Parse the connection string</span></span>
2. <span data-ttu-id="2446e-119">Создайте маркер проверки подлинности</span><span class="sxs-lookup"><span data-stu-id="2446e-119">Generate the authorization token</span></span>
3. <span data-ttu-id="2446e-120">Выполните вызов HTTP</span><span class="sxs-lookup"><span data-stu-id="2446e-120">Perform the HTTP call</span></span>

### <a name="parse-the-connection-string"></a><span data-ttu-id="2446e-121">Проанализируйте строку подключения</span><span class="sxs-lookup"><span data-stu-id="2446e-121">Parse the connection string</span></span>
<span data-ttu-id="2446e-122">Ниже показан основной класс, реализующий клиента, конструктор которого выполняет анализ строки подключения:</span><span class="sxs-lookup"><span data-stu-id="2446e-122">Here is the main class implementing the client, whose constructor that parses the connection string:</span></span>

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


### <a name="create-security-token"></a><span data-ttu-id="2446e-123">Создание маркера безопасности</span><span class="sxs-lookup"><span data-stu-id="2446e-123">Create security token</span></span>
<span data-ttu-id="2446e-124">Подробные сведения о создании токенов безопасности можно найти [здесь](http://msdn.microsoft.com/library/dn495627.aspx).</span><span class="sxs-lookup"><span data-stu-id="2446e-124">The details of the security token creation are available [here](http://msdn.microsoft.com/library/dn495627.aspx).</span></span>
<span data-ttu-id="2446e-125">Для создания токена на основе универсального кода ресурса (URI) текущего запроса и учетных данных, извлеченных из строки подключения, необходимо добавить следующий метод в класс **NotificationHub** .</span><span class="sxs-lookup"><span data-stu-id="2446e-125">The following method has to be added to the **NotificationHub** class to create the token based on the URI of the current request and the credentials extracted from the connection string.</span></span>

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

### <a name="send-a-notification"></a><span data-ttu-id="2446e-126">Отправка уведомления</span><span class="sxs-lookup"><span data-stu-id="2446e-126">Send a notification</span></span>
<span data-ttu-id="2446e-127">Сначала следует определить класс, представляющий уведомление.</span><span class="sxs-lookup"><span data-stu-id="2446e-127">First, let us define a class representing a notification.</span></span>

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

<span data-ttu-id="2446e-128">Этот класс представляет собой контейнер для собственного тела уведомления, либо набор свойств, в случае с шаблонным уведомлением, а также набор заголовков, содержащих свойства формата (собственная платформа или шаблон) и специальные свойства платформы (например, свойство срока действия Apple и заголовки WNS).</span><span class="sxs-lookup"><span data-stu-id="2446e-128">This class is a container for a native notification body, or a set of properties on case of a template notification, and a set of headers which contains format (native platform or template) and platform-specific properties (like Apple expiration property and WNS headers).</span></span>

<span data-ttu-id="2446e-129">Обратитесь к [Документации по REST API для концентраторов уведомлений](http://msdn.microsoft.com/library/dn495827.aspx) и изучите форматы специализированных платформ уведомлений, чтобы узнать обо всех доступных параметрах.</span><span class="sxs-lookup"><span data-stu-id="2446e-129">Please refer to the [Notification Hubs REST APIs documentation](http://msdn.microsoft.com/library/dn495827.aspx) and the specific notification platforms' formats for all the options available.</span></span>

<span data-ttu-id="2446e-130">Имея этот класс, мы можем создавать методы отправки уведомлений внутри класса **NotificationHub** .</span><span class="sxs-lookup"><span data-stu-id="2446e-130">Armed with this class, we can now write the send notification methods inside of the **NotificationHub** class.</span></span>

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

        // Send the request
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

<span data-ttu-id="2446e-131">Указанные выше методы отправляют запрос HTTP POST в конечную точку "/messages" концентратора уведомлений, с надлежащим телом и заголовками для отправки уведомления.</span><span class="sxs-lookup"><span data-stu-id="2446e-131">The above methods send an HTTP POST request to the /messages endpoint of your notification hub, with the correct body and headers to send the notification.</span></span>

## <span data-ttu-id="2446e-132"><a name="complete-tutorial"></a>Завершение работы с учебником</span><span class="sxs-lookup"><span data-stu-id="2446e-132"><a name="complete-tutorial"></a>Complete the tutorial</span></span>
<span data-ttu-id="2446e-133">Теперь вы можете завершить работу с учебником по началу работы, отправив уведомление из серверной части PHP.</span><span class="sxs-lookup"><span data-stu-id="2446e-133">Now you can complete the Get Started tutorial by sending the notification from a PHP back-end.</span></span>

<span data-ttu-id="2446e-134">Инициализируйте клиент концентратора уведомлений (замените строку подключения и имя концентратора в соответствии с инструкциями в [учебнике по началу работы]):</span><span class="sxs-lookup"><span data-stu-id="2446e-134">Initialize your Notification Hubs client (substitute the connection string and hub name as instructed in the [Get started tutorial]):</span></span>

    $hub = new NotificationHub("connection string", "hubname");    

<span data-ttu-id="2446e-135">Затем добавьте код отправки, определяемый целевой мобильной платформой.</span><span class="sxs-lookup"><span data-stu-id="2446e-135">Then add the send code depending on your target mobile platform.</span></span>

### <a name="windows-store-and-windows-phone-81-non-silverlight"></a><span data-ttu-id="2446e-136">Магазин Windows и Windows Phone 8.1 (без Silverlight)</span><span class="sxs-lookup"><span data-stu-id="2446e-136">Windows Store and Windows Phone 8.1 (non-Silverlight)</span></span>
    $toast = '<toast><visual><binding template="ToastText01"><text id="1">Hello from PHP!</text></binding></visual></toast>';
    $notification = new Notification("windows", $toast);
    $notification->headers[] = 'X-WNS-Type: wns/toast';
    $hub->sendNotification($notification, null);

### <a name="ios"></a><span data-ttu-id="2446e-137">iOS</span><span class="sxs-lookup"><span data-stu-id="2446e-137">iOS</span></span>
    $alert = '{"aps":{"alert":"Hello from PHP!"}}';
    $notification = new Notification("apple", $alert);
    $hub->sendNotification($notification, null);

### <a name="android"></a><span data-ttu-id="2446e-138">Android</span><span class="sxs-lookup"><span data-stu-id="2446e-138">Android</span></span>
    $message = '{"data":{"msg":"Hello from PHP!"}}';
    $notification = new Notification("gcm", $message);
    $hub->sendNotification($notification, null);

### <a name="windows-phone-80-and-81-silverlight"></a><span data-ttu-id="2446e-139">Windows Phone 8.0 и 8.1 Silverlight</span><span class="sxs-lookup"><span data-stu-id="2446e-139">Windows Phone 8.0 and 8.1 Silverlight</span></span>
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


### <a name="kindle-fire"></a><span data-ttu-id="2446e-140">Kindle Fire</span><span class="sxs-lookup"><span data-stu-id="2446e-140">Kindle Fire</span></span>
    $message = '{"data":{"msg":"Hello from PHP!"}}';
    $notification = new Notification("adm", $message);
    $hub->sendNotification($notification, null);

<span data-ttu-id="2446e-141">После выполнения кода PHP на целевом устройстве должно отобразиться уведомление.</span><span class="sxs-lookup"><span data-stu-id="2446e-141">Running your PHP code should produce now a notification appearing on your target device.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2446e-142">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="2446e-142">Next Steps</span></span>
<span data-ttu-id="2446e-143">В этом разделе было показано, как создать простой клиент Java REST для концентраторов уведомлений.</span><span class="sxs-lookup"><span data-stu-id="2446e-143">In this topic we showed how to create a simple Java REST client for Notification Hubs.</span></span> <span data-ttu-id="2446e-144">На данном этапе можно сделать следующее.</span><span class="sxs-lookup"><span data-stu-id="2446e-144">From here you can:</span></span>

* <span data-ttu-id="2446e-145">Загрузить полный [примера оболочки REST PHP], содержащий весь указанный выше код.</span><span class="sxs-lookup"><span data-stu-id="2446e-145">Download the full [PHP REST wrapper sample], which contains all the code above.</span></span>
* <span data-ttu-id="2446e-146">Продолжить изучение функции тегов в концентраторах уведомлений в [учебнике "Срочные новости"]</span><span class="sxs-lookup"><span data-stu-id="2446e-146">Continue learning about Notification Hubs tagging feature in the [Breaking News tutorial]</span></span>
* <span data-ttu-id="2446e-147">Изучить отправку уведомлений отдельным пользователям в [учебнике "Уведомление пользователей"]</span><span class="sxs-lookup"><span data-stu-id="2446e-147">Learn about pushing notifications to individual users in [Notify Users tutorial]</span></span>

<span data-ttu-id="2446e-148">Дополнительную информацию можно найти также в [Центре разработчика PHP](/develop/php/).</span><span class="sxs-lookup"><span data-stu-id="2446e-148">For more information, see also the [PHP Developer Center](/develop/php/).</span></span>

<span data-ttu-id="2446e-149">[примера оболочки REST PHP]: https://github.com/Azure/azure-notificationhubs-samples/tree/master/notificationhubs-rest-php</span><span class="sxs-lookup"><span data-stu-id="2446e-149">[PHP REST wrapper sample]: https://github.com/Azure/azure-notificationhubs-samples/tree/master/notificationhubs-rest-php</span></span>
<span data-ttu-id="2446e-150">[учебнике по началу работы]: http://azure.microsoft.com/documentation/articles/notification-hubs-ios-get-started/</span><span class="sxs-lookup"><span data-stu-id="2446e-150">[Get started tutorial]: http://azure.microsoft.com/documentation/articles/notification-hubs-ios-get-started/</span></span>

