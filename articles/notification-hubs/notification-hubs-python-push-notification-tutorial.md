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
# <a name="how-toouse-notification-hubs-from-python"></a><span data-ttu-id="a5fcb-103">Как toouse концентраторов уведомлений с Python</span><span class="sxs-lookup"><span data-stu-id="a5fcb-103">How toouse Notification Hubs from Python</span></span>
[!INCLUDE [notification-hubs-backend-how-to-selector](../../includes/notification-hubs-backend-how-to-selector.md)]

<span data-ttu-id="a5fcb-104">Все функции концентраторов уведомлений можно получить из внутренней Java и PHP и Python и Ruby с помощью интерфейса REST концентратора уведомлений hello, как описано в разделе MSDN hello [интерфейсы API REST концентраторов уведомлений](http://msdn.microsoft.com/library/dn223264.aspx).</span><span class="sxs-lookup"><span data-stu-id="a5fcb-104">You can access all Notification Hubs features from a Java/PHP/Python/Ruby back-end using hello Notification Hub REST interface as described in hello MSDN topic [Notification Hubs REST APIs](http://msdn.microsoft.com/library/dn223264.aspx).</span></span>

> [!NOTE]
> <span data-ttu-id="a5fcb-105">Это образец реализации реализации hello отправляет уведомление в Python и не является hello официально поддерживается пакет SDK для Python концентратора уведомлений.</span><span class="sxs-lookup"><span data-stu-id="a5fcb-105">This is a sample reference implementation for implementing hello notification sends in Python and is not hello officially supported Notifications Hub Python SDK.</span></span>
> 
> <span data-ttu-id="a5fcb-106">Этот образец написан с помощью Python 3.4.</span><span class="sxs-lookup"><span data-stu-id="a5fcb-106">This sample is written using Python 3.4.</span></span>
> 
> 

<span data-ttu-id="a5fcb-107">В этой статье описывается:</span><span class="sxs-lookup"><span data-stu-id="a5fcb-107">In this topic we show how to:</span></span>

* <span data-ttu-id="a5fcb-108">Построение клиента REST для функций концентраторов уведомлений на языке Python.</span><span class="sxs-lookup"><span data-stu-id="a5fcb-108">Build a REST client for Notification Hubs features in Python.</span></span>
* <span data-ttu-id="a5fcb-109">Отправьте уведомления, используя toohello интерфейса API REST концентратора уведомления для hello Python.</span><span class="sxs-lookup"><span data-stu-id="a5fcb-109">Send notifications using hello Python interface toohello Notification Hub REST APIs.</span></span> 
* <span data-ttu-id="a5fcb-110">Отладка/образовательных целях получения дампа hello HTTP REST запросов и ответов.</span><span class="sxs-lookup"><span data-stu-id="a5fcb-110">Get a dump of hello HTTP REST request/response for debugging/educational purpose.</span></span> 

<span data-ttu-id="a5fcb-111">Можно выполнить hello [учебника запущенную Get](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md) для вашей платформы мобильных устройств по выбору, реализация hello серверную часть в Python.</span><span class="sxs-lookup"><span data-stu-id="a5fcb-111">You can follow hello [Get started tutorial](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md) for your mobile platform of choice, implementing hello back-end portion in Python.</span></span>

> [!NOTE]
> <span data-ttu-id="a5fcb-112">Hello образец hello относится только ограниченный toosend уведомления и он не выполняет любой управления регистрацией.</span><span class="sxs-lookup"><span data-stu-id="a5fcb-112">hello scope of hello sample is only limited toosend notifications and it doesn't do any registration management.</span></span>
> 
> 

## <a name="client-interface"></a><span data-ttu-id="a5fcb-113">Интерфейс клиента</span><span class="sxs-lookup"><span data-stu-id="a5fcb-113">Client interface</span></span>
<span data-ttu-id="a5fcb-114">Hello основного клиентского интерфейса предоставляет hello же методы, доступные в hello [.NET SDK концентраторы уведомлений](http://msdn.microsoft.com/library/jj933431.aspx).</span><span class="sxs-lookup"><span data-stu-id="a5fcb-114">hello main client interface can provide hello same methods that are available in hello [.NET Notification Hubs SDK](http://msdn.microsoft.com/library/jj933431.aspx).</span></span> <span data-ttu-id="a5fcb-115">Это позволит вам toodirectly перевести все hello учебники и образцы, доступных в настоящее время этот сайт и предоставленного сообществом hello на hello Интернета.</span><span class="sxs-lookup"><span data-stu-id="a5fcb-115">This will allow you toodirectly translate all hello tutorials and samples currently available on this site, and contributed by hello community on hello internet.</span></span>

<span data-ttu-id="a5fcb-116">Можно найти все доступные в hello кода hello [образца программы-оболочки Python REST].</span><span class="sxs-lookup"><span data-stu-id="a5fcb-116">You can find all hello code available in hello [Python REST wrapper sample].</span></span>

<span data-ttu-id="a5fcb-117">Например toocreate клиента:</span><span class="sxs-lookup"><span data-stu-id="a5fcb-117">For example, toocreate a client:</span></span>

    isDebug = True
    hub = NotificationHub("myConnectionString", "myNotificationHubName", isDebug)

<span data-ttu-id="a5fcb-118">toosend Windows всплывающих уведомлений:</span><span class="sxs-lookup"><span data-stu-id="a5fcb-118">toosend a Windows toast notification:</span></span>

    wns_payload = """<toast><visual><binding template=\"ToastText01\"><text id=\"1\">Hello world!</text></binding></visual></toast>"""
    hub.send_windows_notification(wns_payload)

## <a name="implementation"></a><span data-ttu-id="a5fcb-119">Реализация</span><span class="sxs-lookup"><span data-stu-id="a5fcb-119">Implementation</span></span>
<span data-ttu-id="a5fcb-120">Если вы еще не сделали, выполните наши [учебника запущенную Get] вверх toohello последний раздел, при наличии tooimplement hello серверной части.</span><span class="sxs-lookup"><span data-stu-id="a5fcb-120">If you did not already, please follow our [Get started tutorial] up toohello last section where you have tooimplement hello back-end.</span></span>

<span data-ttu-id="a5fcb-121">Здравствуйте, все сведения tooimplement полный оболочки REST можно найти на [MSDN](http://msdn.microsoft.com/library/dn530746.aspx).</span><span class="sxs-lookup"><span data-stu-id="a5fcb-121">All hello details tooimplement a full REST wrapper can be found on [MSDN](http://msdn.microsoft.com/library/dn530746.aspx).</span></span> <span data-ttu-id="a5fcb-122">В этом разделе будут описаны реализация Python hello hello основных шагов требуется tooaccess конечные точки REST концентраторов уведомлений и отправки уведомлений</span><span class="sxs-lookup"><span data-stu-id="a5fcb-122">In this section we will describe hello Python implementation of hello main steps required tooaccess Notification Hubs REST endpoints and send notifications</span></span>

1. <span data-ttu-id="a5fcb-123">Синтаксический анализ строки соединения hello</span><span class="sxs-lookup"><span data-stu-id="a5fcb-123">Parse hello connection string</span></span>
2. <span data-ttu-id="a5fcb-124">Создание маркера авторизации hello</span><span class="sxs-lookup"><span data-stu-id="a5fcb-124">Generate hello authorization token</span></span>
3. <span data-ttu-id="a5fcb-125">Отправка уведомления с помощью HTTP REST API</span><span class="sxs-lookup"><span data-stu-id="a5fcb-125">Send a notification using HTTP REST API</span></span>

### <a name="parse-hello-connection-string"></a><span data-ttu-id="a5fcb-126">Синтаксический анализ строки соединения hello</span><span class="sxs-lookup"><span data-stu-id="a5fcb-126">Parse hello connection string</span></span>
<span data-ttu-id="a5fcb-127">Вот hello основной класс, реализация клиента hello, конструктор которого выполняет синтаксический анализ строки подключения hello.</span><span class="sxs-lookup"><span data-stu-id="a5fcb-127">Here is hello main class implementing hello client, whose constructor parses hello connection string:</span></span>

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


### <a name="create-security-token"></a><span data-ttu-id="a5fcb-128">Создание маркера безопасности</span><span class="sxs-lookup"><span data-stu-id="a5fcb-128">Create security token</span></span>
<span data-ttu-id="a5fcb-129">доступны Hello сведения для создания маркера безопасности hello [здесь](http://msdn.microsoft.com/library/dn495627.aspx).</span><span class="sxs-lookup"><span data-stu-id="a5fcb-129">hello details of hello security token creation are available [here](http://msdn.microsoft.com/library/dn495627.aspx).</span></span>
<span data-ttu-id="a5fcb-130">Hello следующие методы имеют добавлены toobe toohello **концентратора уведомлений** класса toocreate hello токены на hello URI текущего запроса hello и hello учетные данные, извлеченные из строки подключения hello.</span><span class="sxs-lookup"><span data-stu-id="a5fcb-130">hello following methods have toobe added toohello **NotificationHub** class toocreate hello token based on hello URI of hello current request and hello credentials extracted from hello connection string.</span></span>

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

### <a name="send-a-notification-using-http-rest-api"></a><span data-ttu-id="a5fcb-131">Отправка уведомления с помощью HTTP REST API</span><span class="sxs-lookup"><span data-stu-id="a5fcb-131">Send a notification using HTTP REST API</span></span>
<span data-ttu-id="a5fcb-132">Сначала следует определить класс, представляющий уведомление.</span><span class="sxs-lookup"><span data-stu-id="a5fcb-132">First, let use define a class representing a notification.</span></span>

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

<span data-ttu-id="a5fcb-133">Этот класс представляет собой контейнер для собственного текста уведомления либо набор свойств (в случае шаблонного уведомления), а также набор заголовков, содержащих свойства формата (собственная платформа или шаблон) и специальные свойства платформы (например, свойство срока действия Apple и заголовки WNS).</span><span class="sxs-lookup"><span data-stu-id="a5fcb-133">This class is a container for a native notification body or a set of properties in case of a template notification, a set of headers which contains format (native platform or template) and platform-specific properties (like Apple expiration property and WNS headers).</span></span>

<span data-ttu-id="a5fcb-134">См. toohello [документации по API-интерфейс REST концентраторов уведомлений](http://msdn.microsoft.com/library/dn495827.aspx) и hello форматы уведомлений платформы для всех hello доступные параметры.</span><span class="sxs-lookup"><span data-stu-id="a5fcb-134">Please refer toohello [Notification Hubs REST APIs documentation](http://msdn.microsoft.com/library/dn495827.aspx) and hello specific notification platforms' formats for all hello options available.</span></span>

<span data-ttu-id="a5fcb-135">Теперь с помощью этого класса можно написать методы уведомления внутри hello hello отправки **концентратора уведомлений** класса.</span><span class="sxs-lookup"><span data-stu-id="a5fcb-135">Now with this class, we can write hello send notification methods inside of hello **NotificationHub** class.</span></span>

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

<span data-ttu-id="a5fcb-136">Hello выше методы отправки HTTP POST запроса toohello /messages конечной точки с телом правильный hello и заголовки toosend hello уведомления центра уведомлений.</span><span class="sxs-lookup"><span data-stu-id="a5fcb-136">hello above methods send an HTTP POST request toohello /messages endpoint of your notification hub, with hello correct body and headers toosend hello notification.</span></span>

### <a name="using-debug-property-tooenable-detailed-logging"></a><span data-ttu-id="a5fcb-137">С помощью свойства tooenable отладки подробные журналы</span><span class="sxs-lookup"><span data-stu-id="a5fcb-137">Using debug property tooenable detailed logging</span></span>
<span data-ttu-id="a5fcb-138">Включение отладки свойства во время инициализации hello концентратор уведомлений будет записи подробное ведение журнала сведений о hello HTTP запроса и ответа дампа, а также подробные сообщения уведомления отправить результат.</span><span class="sxs-lookup"><span data-stu-id="a5fcb-138">Enabling debug property while initializing hello Notification Hub will write out detailed logging information about hello HTTP request and response dump as well as detailed Notification message send outcome.</span></span> <span data-ttu-id="a5fcb-139">Недавно мы добавили это свойство с именем [TestSend концентраторы уведомлений свойство](http://msdn.microsoft.com/library/microsoft.servicebus.notifications.notificationhubclient.enabletestsend.aspx) которого возвращает подробные сведения о hello отправки уведомлений.</span><span class="sxs-lookup"><span data-stu-id="a5fcb-139">We recently added this property called [Notification Hubs TestSend property](http://msdn.microsoft.com/library/microsoft.servicebus.notifications.notificationhubclient.enabletestsend.aspx) which returns detailed information about hello notification send outcome.</span></span> <span data-ttu-id="a5fcb-140">toouse его - инициализировать с помощью следующих hello:</span><span class="sxs-lookup"><span data-stu-id="a5fcb-140">toouse it - initialize using hello following:</span></span>

    hub = NotificationHub("myConnectionString", "myNotificationHubName", isDebug)

<span data-ttu-id="a5fcb-141">Hello уведомление концентратора отправить запрос HTTP URL-адрес в результате пополняется с querystring «test».</span><span class="sxs-lookup"><span data-stu-id="a5fcb-141">hello Notification Hub Send request HTTP URL gets appended with a "test" querystring as a result.</span></span> 

## <span data-ttu-id="a5fcb-142"><a name="complete-tutorial"></a>Учебник завершения hello</span><span class="sxs-lookup"><span data-stu-id="a5fcb-142"><a name="complete-tutorial"></a>Complete hello tutorial</span></span>
<span data-ttu-id="a5fcb-143">Теперь можно завершить учебника приступить к работе hello путем отправки уведомления hello из внутренней Python.</span><span class="sxs-lookup"><span data-stu-id="a5fcb-143">Now you can complete hello Get Started tutorial by sending hello notification from a Python back-end.</span></span>

<span data-ttu-id="a5fcb-144">Инициализировать концентраторы уведомлений клиента (замените имя концентратора и строка соединения hello, как описано в hello [учебника запущенную Get]):</span><span class="sxs-lookup"><span data-stu-id="a5fcb-144">Initialize your Notification Hubs client (substitute hello connection string and hub name as instructed in hello [Get started tutorial]):</span></span>

    hub = NotificationHub("myConnectionString", "myNotificationHubName")

<span data-ttu-id="a5fcb-145">Затем добавьте код отправки hello в зависимости от целевой платформы мобильных устройств.</span><span class="sxs-lookup"><span data-stu-id="a5fcb-145">Then add hello send code depending on your target mobile platform.</span></span> <span data-ttu-id="a5fcb-146">В этом примере также добавляет выше tooenable методы уровня отправки уведомлений на основе платформы hello например send_windows_notification для windows; send_apple_notification (для apple) и т. д.</span><span class="sxs-lookup"><span data-stu-id="a5fcb-146">This sample also adds higher level methods tooenable sending notifications based on hello platform e.g. send_windows_notification for windows; send_apple_notification (for apple) etc.</span></span> 

### <a name="windows-store-and-windows-phone-81-non-silverlight"></a><span data-ttu-id="a5fcb-147">Магазин Windows и Windows Phone 8.1 (без Silverlight)</span><span class="sxs-lookup"><span data-stu-id="a5fcb-147">Windows Store and Windows Phone 8.1 (non-Silverlight)</span></span>
    wns_payload = """<toast><visual><binding template=\"ToastText01\"><text id=\"1\">Test</text></binding></visual></toast>"""
    hub.send_windows_notification(wns_payload)

### <a name="windows-phone-80-and-81-silverlight"></a><span data-ttu-id="a5fcb-148">Windows Phone 8.0 и 8.1 Silverlight</span><span class="sxs-lookup"><span data-stu-id="a5fcb-148">Windows Phone 8.0 and 8.1 Silverlight</span></span>
    hub.send_mpns_notification(toast)

### <a name="ios"></a><span data-ttu-id="a5fcb-149">iOS</span><span class="sxs-lookup"><span data-stu-id="a5fcb-149">iOS</span></span>
    alert_payload = {
        'data':
            {
                'msg': 'Hello!'
            }
    }
    hub.send_apple_notification(alert_payload)

### <a name="android"></a><span data-ttu-id="a5fcb-150">Android</span><span class="sxs-lookup"><span data-stu-id="a5fcb-150">Android</span></span>
    gcm_payload = {
        'data':
            {
                'msg': 'Hello!'
            }
    }
    hub.send_gcm_notification(gcm_payload)

### <a name="kindle-fire"></a><span data-ttu-id="a5fcb-151">Kindle Fire</span><span class="sxs-lookup"><span data-stu-id="a5fcb-151">Kindle Fire</span></span>
    adm_payload = {
        'data':
            {
                'msg': 'Hello!'
            }
    }
    hub.send_adm_notification(adm_payload)

### <a name="baidu"></a><span data-ttu-id="a5fcb-152">Baidu</span><span class="sxs-lookup"><span data-stu-id="a5fcb-152">Baidu</span></span>
    baidu_payload = {
        'data':
            {
                'msg': 'Hello!'
            }
    }
    hub.send_baidu_notification(baidu_payload)

<span data-ttu-id="a5fcb-153">После выполнения кода Python на целевом устройстве должно отобразиться уведомление.</span><span class="sxs-lookup"><span data-stu-id="a5fcb-153">Running your Python code should produce a notification appearing on your target device.</span></span>

## <a name="examples"></a><span data-ttu-id="a5fcb-154">Примеры:</span><span class="sxs-lookup"><span data-stu-id="a5fcb-154">Examples:</span></span>
### <a name="enabling-debug-property"></a><span data-ttu-id="a5fcb-155">Включение свойства отладки</span><span class="sxs-lookup"><span data-stu-id="a5fcb-155">Enabling debug property</span></span>
<span data-ttu-id="a5fcb-156">При включении флаг отладки во время инициализации hello концентратора уведомлений, то вы увидите подробные дампа запросов и ответов HTTP, а также NotificationOutcome следующего вида hello, где можно понять, какие заголовки HTTP, передаются в запрос hello и какие HTTP получен отклик от hello концентратора уведомлений:![][1]</span><span class="sxs-lookup"><span data-stu-id="a5fcb-156">When you enable debug flag while initializing hello NotificationHub then you will see detailed HTTP request and response dump as well as NotificationOutcome like hello following where you can understand what HTTP headers are passed in hello request and what HTTP response was received from hello Notification Hub: ![][1]</span></span>

<span data-ttu-id="a5fcb-157">Вы увидите подробный результат концентратора уведомлений, например сведения о том,</span><span class="sxs-lookup"><span data-stu-id="a5fcb-157">You will see detailed Notification Hub result e.g.</span></span> 

* <span data-ttu-id="a5fcb-158">Когда сообщение hello успешной отправки toohello службы Push-уведомлений.</span><span class="sxs-lookup"><span data-stu-id="a5fcb-158">when hello message is successfully sent toohello Push Notification Service.</span></span> 
  
        <Outcome>hello Notification was successfully sent toohello Push Notification System</Outcome>
* <span data-ttu-id="a5fcb-159">При наличии не найдены цели для push-уведомления, то скорее всего будет ниже toosee hello в ответ hello (который указывает на наличие регистраций найден toodeliver hello уведомления, скорее всего, так как некоторые hello регистраций несоответствие тегов)</span><span class="sxs-lookup"><span data-stu-id="a5fcb-159">If there were no targets found for any push notification then you are likely going toosee hello following in hello response (which indicates that there were no registrations found toodeliver hello notification probably because hello registrations had some mismatched tags)</span></span>
  
        '<NotificationOutcome xmlns="http://schemas.microsoft.com/netservices/2010/10/servicebus/connect" xmlns:i="http://www.w3.org/2001/XMLSchema-instance"><Success>0</Success><Failure>0</Failure><Results i:nil="true"/></NotificationOutcome>'

### <a name="broadcast-toast-notification-toowindows"></a><span data-ttu-id="a5fcb-160">Всплывающие уведомления tooWindows широковещательных пакетов</span><span class="sxs-lookup"><span data-stu-id="a5fcb-160">Broadcast toast notification tooWindows</span></span>
<span data-ttu-id="a5fcb-161">Обратите внимание, hello заголовки, которые отправляются out при отправке клиент tooWindows широковещательных всплывающих уведомлений.</span><span class="sxs-lookup"><span data-stu-id="a5fcb-161">Notice hello headers that get sent out when you are sending a broadcast toast notification tooWindows client.</span></span> 

    hub.send_windows_notification(wns_payload)

![][2]

### <a name="send-notification-specifying-a-tag-or-tag-expression"></a><span data-ttu-id="a5fcb-162">Отправка уведомления с указанием тега (или регулярного выражения)</span><span class="sxs-lookup"><span data-stu-id="a5fcb-162">Send notification specifying a tag (or tag expression)</span></span>
<span data-ttu-id="a5fcb-163">Обратите внимание hello HTTP теги заголовок, который будет добавлен и toohello HTTP-запроса (в следующем примере hello, мы отправляете hello уведомления только tooregistrations с полезными данными «Спорт»)</span><span class="sxs-lookup"><span data-stu-id="a5fcb-163">Notice hello Tags HTTP header which gets added toohello HTTP request (in hello example below, we are sending hello notification only tooregistrations with 'sports' payload)</span></span>

    hub.send_windows_notification(wns_payload, "sports")

![][3]

### <a name="send-notification-specifying-multiple-tags"></a><span data-ttu-id="a5fcb-164">Отправка уведомления с указанием нескольких тегов</span><span class="sxs-lookup"><span data-stu-id="a5fcb-164">Send notification specifying multiple tags</span></span>
<span data-ttu-id="a5fcb-165">Обратите внимание на то, как заголовок HTTP теги hello изменяется при отправке несколько тегов.</span><span class="sxs-lookup"><span data-stu-id="a5fcb-165">Notice how hello Tags HTTP header changes when multiple tags are sent.</span></span> 

    tags = {'sports', 'politics'}
    hub.send_windows_notification(wns_payload, tags)

![][4]

### <a name="templated-notification"></a><span data-ttu-id="a5fcb-166">Шаблон уведомления</span><span class="sxs-lookup"><span data-stu-id="a5fcb-166">Templated notification</span></span>
<span data-ttu-id="a5fcb-167">Обратите внимание, что hello изменения формата HTTP-заголовка и полезных данных текст hello отправляется как часть текста hello HTTP-запроса.</span><span class="sxs-lookup"><span data-stu-id="a5fcb-167">Notice that hello Format HTTP header changes and hello payload body is sent as part of hello HTTP request body:</span></span>

<span data-ttu-id="a5fcb-168">**Сторона клиента — зарегистрированный шаблон**</span><span class="sxs-lookup"><span data-stu-id="a5fcb-168">**Client side - registered template**</span></span>

        var template =
                        @"<toast><visual><binding template=""ToastText01""><text id=""1"">$(greeting_en)</text></binding></visual></toast>";

<span data-ttu-id="a5fcb-169">**Серверный - Отправка hello полезных данных**</span><span class="sxs-lookup"><span data-stu-id="a5fcb-169">**Server side - sending hello payload**</span></span>

        template_payload = {'greeting_en': 'Hello', 'greeting_fr': 'Salut'}
        hub.send_template_notification(template_payload)

![][5]

## <a name="next-steps"></a><span data-ttu-id="a5fcb-170">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="a5fcb-170">Next Steps</span></span>
<span data-ttu-id="a5fcb-171">В этом разделе мы показали, как toocreate простой Python REST клиента для концентраторов уведомлений.</span><span class="sxs-lookup"><span data-stu-id="a5fcb-171">In this topic we showed how toocreate a simple Python REST client for Notification Hubs.</span></span> <span data-ttu-id="a5fcb-172">На данном этапе можно сделать следующее.</span><span class="sxs-lookup"><span data-stu-id="a5fcb-172">From here you can:</span></span>

* <span data-ttu-id="a5fcb-173">Hello полной загрузки [образца программы-оболочки Python REST], который содержит весь код hello выше.</span><span class="sxs-lookup"><span data-stu-id="a5fcb-173">Download hello full [Python REST wrapper sample], which contains all hello code above.</span></span>
* <span data-ttu-id="a5fcb-174">Продолжить изучение теги в hello функции концентраторов уведомлений [учебника последние новости]</span><span class="sxs-lookup"><span data-stu-id="a5fcb-174">Continue learning about Notification Hubs tagging feature in hello [Breaking News tutorial]</span></span>
* <span data-ttu-id="a5fcb-175">Продолжить изучение компонентов шаблоны концентраторов уведомлений в hello [учебника локализация новостей]</span><span class="sxs-lookup"><span data-stu-id="a5fcb-175">Continue learning about Notification Hubs Templates feature in hello [Localizing News tutorial]</span></span>

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

