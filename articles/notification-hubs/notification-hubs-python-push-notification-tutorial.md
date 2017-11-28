---
title: "Использование концентраторов уведомлений с Python"
description: "Узнайте, как использовать центры уведомлений Azure из серверной части Python."
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
ms.openlocfilehash: 9ceedb9940759427fc8cec74a1307e42472563a6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-notification-hubs-from-python"></a><span data-ttu-id="ff01f-103">Использование концентраторов уведомлений с Python</span><span class="sxs-lookup"><span data-stu-id="ff01f-103">How to use Notification Hubs from Python</span></span>
[!INCLUDE [notification-hubs-backend-how-to-selector](../../includes/notification-hubs-backend-how-to-selector.md)]

<span data-ttu-id="ff01f-104">Вы можете обращаться ко всем функциям центров уведомлений из серверной части Java, PHP, Python или Ruby, используя интерфейс REST в соответствии с описанием в разделе MSDN [Интерфейсы API REST концентраторов уведомлений](http://msdn.microsoft.com/library/dn223264.aspx).</span><span class="sxs-lookup"><span data-stu-id="ff01f-104">You can access all Notification Hubs features from a Java/PHP/Python/Ruby back-end using the Notification Hub REST interface as described in the MSDN topic [Notification Hubs REST APIs](http://msdn.microsoft.com/library/dn223264.aspx).</span></span>

> [!NOTE]
> <span data-ttu-id="ff01f-105">Это образец эталонной реализации для отправки уведомлений в Python, который не является официально поддерживаемым пакетом SDK концентраторов уведомлений Python.</span><span class="sxs-lookup"><span data-stu-id="ff01f-105">This is a sample reference implementation for implementing the notification sends in Python and is not the officially supported Notifications Hub Python SDK.</span></span>
> 
> <span data-ttu-id="ff01f-106">Этот образец написан с помощью Python 3.4.</span><span class="sxs-lookup"><span data-stu-id="ff01f-106">This sample is written using Python 3.4.</span></span>
> 
> 

<span data-ttu-id="ff01f-107">В этой статье описывается:</span><span class="sxs-lookup"><span data-stu-id="ff01f-107">In this topic we show how to:</span></span>

* <span data-ttu-id="ff01f-108">Построение клиента REST для функций концентраторов уведомлений на языке Python.</span><span class="sxs-lookup"><span data-stu-id="ff01f-108">Build a REST client for Notification Hubs features in Python.</span></span>
* <span data-ttu-id="ff01f-109">Отправка уведомлений с помощью интерфейса API REST концентратора уведомления Python.</span><span class="sxs-lookup"><span data-stu-id="ff01f-109">Send notifications using the Python interface to the Notification Hub REST APIs.</span></span> 
* <span data-ttu-id="ff01f-110">Получение дампа запросов и ответов HTTP REST для отладки и образовательных целей.</span><span class="sxs-lookup"><span data-stu-id="ff01f-110">Get a dump of the HTTP REST request/response for debugging/educational purpose.</span></span> 

<span data-ttu-id="ff01f-111">Можно воспользоваться указаниями в разделе [Приступая к работе с центрами уведомлений](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md) для выбранной мобильной платформы, которая реализует серверную часть на языке Python.</span><span class="sxs-lookup"><span data-stu-id="ff01f-111">You can follow the [Get started tutorial](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md) for your mobile platform of choice, implementing the back-end portion in Python.</span></span>

> [!NOTE]
> <span data-ttu-id="ff01f-112">Область действия образца ограничена отправкой уведомлений. Образец не выполняет функции управления регистрацией.</span><span class="sxs-lookup"><span data-stu-id="ff01f-112">The scope of the sample is only limited to send notifications and it doesn't do any registration management.</span></span>
> 
> 

## <a name="client-interface"></a><span data-ttu-id="ff01f-113">Интерфейс клиента</span><span class="sxs-lookup"><span data-stu-id="ff01f-113">Client interface</span></span>
<span data-ttu-id="ff01f-114">Интерфейс основного клиента предоставляет те же методы, что и [пакет SDK центров уведомлений для .NET](http://msdn.microsoft.com/library/jj933431.aspx).</span><span class="sxs-lookup"><span data-stu-id="ff01f-114">The main client interface can provide the same methods that are available in the [.NET Notification Hubs SDK](http://msdn.microsoft.com/library/jj933431.aspx).</span></span> <span data-ttu-id="ff01f-115">Это позволяет напрямую переводить все учебники и примеры, доступные на этом сайте в настоящий момент и пополняемые интернет-сообществом.</span><span class="sxs-lookup"><span data-stu-id="ff01f-115">This will allow you to directly translate all the tutorials and samples currently available on this site, and contributed by the community on the internet.</span></span>

<span data-ttu-id="ff01f-116">Полный код доступен в [примере оболочки REST Python].</span><span class="sxs-lookup"><span data-stu-id="ff01f-116">You can find all the code available in the [Python REST wrapper sample].</span></span>

<span data-ttu-id="ff01f-117">Например, чтобы создать клиента, необходимо выполнить следующие действия.</span><span class="sxs-lookup"><span data-stu-id="ff01f-117">For example, to create a client:</span></span>

    isDebug = True
    hub = NotificationHub("myConnectionString", "myNotificationHubName", isDebug)

<span data-ttu-id="ff01f-118">Чтобы отправить всплывающее уведомление Windows:</span><span class="sxs-lookup"><span data-stu-id="ff01f-118">To send a Windows toast notification:</span></span>

    wns_payload = """<toast><visual><binding template=\"ToastText01\"><text id=\"1\">Hello world!</text></binding></visual></toast>"""
    hub.send_windows_notification(wns_payload)

## <a name="implementation"></a><span data-ttu-id="ff01f-119">Реализация</span><span class="sxs-lookup"><span data-stu-id="ff01f-119">Implementation</span></span>
<span data-ttu-id="ff01f-120">Если вы еще этого не делали, выполните шаги, описанные в [Приступая к работе с центрами уведомлений] , до последнего раздела, в котором вам нужно реализовать серверную часть.</span><span class="sxs-lookup"><span data-stu-id="ff01f-120">If you did not already, please follow our [Get started tutorial] up to the last section where you have to implement the back-end.</span></span>

<span data-ttu-id="ff01f-121">Подробные сведения о реализации полноценной оболочки REST можно найти в [MSDN](http://msdn.microsoft.com/library/dn530746.aspx).</span><span class="sxs-lookup"><span data-stu-id="ff01f-121">All the details to implement a full REST wrapper can be found on [MSDN](http://msdn.microsoft.com/library/dn530746.aspx).</span></span> <span data-ttu-id="ff01f-122">В этом разделе описана реализация основных действий на языке Python, необходимых для доступа к конечным точкам концентраторов уведомлений REST и отправки уведомлений.</span><span class="sxs-lookup"><span data-stu-id="ff01f-122">In this section we will describe the Python implementation of the main steps required to access Notification Hubs REST endpoints and send notifications</span></span>

1. <span data-ttu-id="ff01f-123">Анализ строки подключения</span><span class="sxs-lookup"><span data-stu-id="ff01f-123">Parse the connection string</span></span>
2. <span data-ttu-id="ff01f-124">Создайте маркер проверки подлинности</span><span class="sxs-lookup"><span data-stu-id="ff01f-124">Generate the authorization token</span></span>
3. <span data-ttu-id="ff01f-125">Отправка уведомления с помощью HTTP REST API</span><span class="sxs-lookup"><span data-stu-id="ff01f-125">Send a notification using HTTP REST API</span></span>

### <a name="parse-the-connection-string"></a><span data-ttu-id="ff01f-126">Анализ строки подключения</span><span class="sxs-lookup"><span data-stu-id="ff01f-126">Parse the connection string</span></span>
<span data-ttu-id="ff01f-127">Ниже показан основной класс, реализующий клиента, конструктор которого выполняет анализ строки подключения:</span><span class="sxs-lookup"><span data-stu-id="ff01f-127">Here is the main class implementing the client, whose constructor parses the connection string:</span></span>

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


### <a name="create-security-token"></a><span data-ttu-id="ff01f-128">Создание маркера безопасности</span><span class="sxs-lookup"><span data-stu-id="ff01f-128">Create security token</span></span>
<span data-ttu-id="ff01f-129">Подробные сведения о создании токенов безопасности можно найти [здесь](http://msdn.microsoft.com/library/dn495627.aspx).</span><span class="sxs-lookup"><span data-stu-id="ff01f-129">The details of the security token creation are available [here](http://msdn.microsoft.com/library/dn495627.aspx).</span></span>
<span data-ttu-id="ff01f-130">Для создания маркера на основе универсального кода ресурса (URI) текущего запроса и учетных данных, извлеченных из строки подключения, необходимо добавить следующие методы в класс **NotificationHub** .</span><span class="sxs-lookup"><span data-stu-id="ff01f-130">The following methods have to be added to the **NotificationHub** class to create the token based on the URI of the current request and the credentials extracted from the connection string.</span></span>

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

### <a name="send-a-notification-using-http-rest-api"></a><span data-ttu-id="ff01f-131">Отправка уведомления с помощью HTTP REST API</span><span class="sxs-lookup"><span data-stu-id="ff01f-131">Send a notification using HTTP REST API</span></span>
<span data-ttu-id="ff01f-132">Сначала следует определить класс, представляющий уведомление.</span><span class="sxs-lookup"><span data-stu-id="ff01f-132">First, let use define a class representing a notification.</span></span>

    class Notification:
        def __init__(self, notification_format=None, payload=None, debug=0):
            valid_formats = ['template', 'apple', 'gcm', 'windows', 'windowsphone', "adm", "baidu"]
            if not any(x in notification_format for x in valid_formats):
                raise Exception(
                    "Invalid Notification format. " +
                    "Must be one of the following - 'template', 'apple', 'gcm', 'windows', 'windowsphone', 'adm', 'baidu'")

            self.format = notification_format
            self.payload = payload

            # array with keynames for headers
            # Note: Some headers are mandatory: Windows: X-WNS-Type, WindowsPhone: X-NotificationType
            # Note: For Apple you can set Expiry with header: ServiceBusNotification-ApnsExpiry
            # in W3C DTF, YYYY-MM-DDThh:mmTZD (for example, 1997-07-16T19:20+01:00).
            self.headers = None

<span data-ttu-id="ff01f-133">Этот класс представляет собой контейнер для собственного текста уведомления либо набор свойств (в случае шаблонного уведомления), а также набор заголовков, содержащих свойства формата (собственная платформа или шаблон) и специальные свойства платформы (например, свойство срока действия Apple и заголовки WNS).</span><span class="sxs-lookup"><span data-stu-id="ff01f-133">This class is a container for a native notification body or a set of properties in case of a template notification, a set of headers which contains format (native platform or template) and platform-specific properties (like Apple expiration property and WNS headers).</span></span>

<span data-ttu-id="ff01f-134">Обратитесь к [Документации по REST API для концентраторов уведомлений](http://msdn.microsoft.com/library/dn495827.aspx) и изучите форматы специализированных платформ уведомлений, чтобы узнать обо всех доступных параметрах.</span><span class="sxs-lookup"><span data-stu-id="ff01f-134">Please refer to the [Notification Hubs REST APIs documentation](http://msdn.microsoft.com/library/dn495827.aspx) and the specific notification platforms' formats for all the options available.</span></span>

<span data-ttu-id="ff01f-135">Имея в распоряжении этот класс, можно создавать методы отправки уведомлений внутри класса **NotificationHub** .</span><span class="sxs-lookup"><span data-stu-id="ff01f-135">Now with this class, we can write the send notification methods inside of the **NotificationHub** class.</span></span>

    def make_http_request(self, url, payload, headers):
        parsed_url = urllib.parse.urlparse(url)
        connection = http.client.HTTPSConnection(parsed_url.hostname, parsed_url.port)

        if self.Debug > 0:
            connection.set_debuglevel(self.Debug)
            # adding this querystring parameter gets detailed information about the PNS send notification outcome
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

        # add the tags/tag expressions to the headers collection
        if tag_list != "":
            headers.update({'ServiceBusNotification-Tags': tag_list})

        # add any custom headers to the headers collection that the user may have added
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

<span data-ttu-id="ff01f-136">Указанные выше методы отправляют запрос HTTP POST в конечную точку "/messages" концентратора уведомлений, с надлежащим телом и заголовками для отправки уведомления.</span><span class="sxs-lookup"><span data-stu-id="ff01f-136">The above methods send an HTTP POST request to the /messages endpoint of your notification hub, with the correct body and headers to send the notification.</span></span>

### <a name="using-debug-property-to-enable-detailed-logging"></a><span data-ttu-id="ff01f-137">Включение подробного ведения журнала с помощью свойства отладки</span><span class="sxs-lookup"><span data-stu-id="ff01f-137">Using debug property to enable detailed logging</span></span>
<span data-ttu-id="ff01f-138">Если включить свойство отладки при инициализации концентратора уведомлений, в журнал будут записаны подробные сведения о дампе запроса и ответа HTTP, а также детальные выходные данные об отправке уведомлений.</span><span class="sxs-lookup"><span data-stu-id="ff01f-138">Enabling debug property while initializing the Notification Hub will write out detailed logging information about the HTTP request and response dump as well as detailed Notification message send outcome.</span></span> <span data-ttu-id="ff01f-139">Недавно мы добавили такое свойство — [свойство TestSend центров уведомлений](http://msdn.microsoft.com/library/microsoft.servicebus.notifications.notificationhubclient.enabletestsend.aspx) , которое возвращает подробные сведения о результатах отправки уведомлений.</span><span class="sxs-lookup"><span data-stu-id="ff01f-139">We recently added this property called [Notification Hubs TestSend property](http://msdn.microsoft.com/library/microsoft.servicebus.notifications.notificationhubclient.enabletestsend.aspx) which returns detailed information about the notification send outcome.</span></span> <span data-ttu-id="ff01f-140">Чтобы его использовать, выполните инициализацию следующим образом:</span><span class="sxs-lookup"><span data-stu-id="ff01f-140">To use it - initialize using the following:</span></span>

    hub = NotificationHub("myConnectionString", "myNotificationHubName", isDebug)

<span data-ttu-id="ff01f-141">В результате к URL-адресу типа HTTP запроса на отправку для концентратора уведомлений прикрепляется строка запроса "test".</span><span class="sxs-lookup"><span data-stu-id="ff01f-141">The Notification Hub Send request HTTP URL gets appended with a "test" querystring as a result.</span></span> 

## <span data-ttu-id="ff01f-142"><a name="complete-tutorial"></a>Завершение работы с учебником</span><span class="sxs-lookup"><span data-stu-id="ff01f-142"><a name="complete-tutorial"></a>Complete the tutorial</span></span>
<span data-ttu-id="ff01f-143">Теперь вы можете завершить работу с учебником по началу работы, отправив уведомление из серверной части Python.</span><span class="sxs-lookup"><span data-stu-id="ff01f-143">Now you can complete the Get Started tutorial by sending the notification from a Python back-end.</span></span>

<span data-ttu-id="ff01f-144">Инициализируйте клиент концентратора уведомлений (замените строку подключения и имя концентратора в соответствии с инструкциями в [Приступая к работе с центрами уведомлений]):</span><span class="sxs-lookup"><span data-stu-id="ff01f-144">Initialize your Notification Hubs client (substitute the connection string and hub name as instructed in the [Get started tutorial]):</span></span>

    hub = NotificationHub("myConnectionString", "myNotificationHubName")

<span data-ttu-id="ff01f-145">Затем добавьте код отправки, определяемый целевой мобильной платформой.</span><span class="sxs-lookup"><span data-stu-id="ff01f-145">Then add the send code depending on your target mobile platform.</span></span> <span data-ttu-id="ff01f-146">В этом примере добавлены методы более высокого уровня, чтобы включить отправку уведомлений для определенной платформы, например send_windows_notification (для Windows), send_apple_notification (для Apple) и т. д.</span><span class="sxs-lookup"><span data-stu-id="ff01f-146">This sample also adds higher level methods to enable sending notifications based on the platform e.g. send_windows_notification for windows; send_apple_notification (for apple) etc.</span></span> 

### <a name="windows-store-and-windows-phone-81-non-silverlight"></a><span data-ttu-id="ff01f-147">Магазин Windows и Windows Phone 8.1 (без Silverlight)</span><span class="sxs-lookup"><span data-stu-id="ff01f-147">Windows Store and Windows Phone 8.1 (non-Silverlight)</span></span>
    wns_payload = """<toast><visual><binding template=\"ToastText01\"><text id=\"1\">Test</text></binding></visual></toast>"""
    hub.send_windows_notification(wns_payload)

### <a name="windows-phone-80-and-81-silverlight"></a><span data-ttu-id="ff01f-148">Windows Phone 8.0 и 8.1 Silverlight</span><span class="sxs-lookup"><span data-stu-id="ff01f-148">Windows Phone 8.0 and 8.1 Silverlight</span></span>
    hub.send_mpns_notification(toast)

### <a name="ios"></a><span data-ttu-id="ff01f-149">iOS</span><span class="sxs-lookup"><span data-stu-id="ff01f-149">iOS</span></span>
    alert_payload = {
        'data':
            {
                'msg': 'Hello!'
            }
    }
    hub.send_apple_notification(alert_payload)

### <a name="android"></a><span data-ttu-id="ff01f-150">Android</span><span class="sxs-lookup"><span data-stu-id="ff01f-150">Android</span></span>
    gcm_payload = {
        'data':
            {
                'msg': 'Hello!'
            }
    }
    hub.send_gcm_notification(gcm_payload)

### <a name="kindle-fire"></a><span data-ttu-id="ff01f-151">Kindle Fire</span><span class="sxs-lookup"><span data-stu-id="ff01f-151">Kindle Fire</span></span>
    adm_payload = {
        'data':
            {
                'msg': 'Hello!'
            }
    }
    hub.send_adm_notification(adm_payload)

### <a name="baidu"></a><span data-ttu-id="ff01f-152">Baidu</span><span class="sxs-lookup"><span data-stu-id="ff01f-152">Baidu</span></span>
    baidu_payload = {
        'data':
            {
                'msg': 'Hello!'
            }
    }
    hub.send_baidu_notification(baidu_payload)

<span data-ttu-id="ff01f-153">После выполнения кода Python на целевом устройстве должно отобразиться уведомление.</span><span class="sxs-lookup"><span data-stu-id="ff01f-153">Running your Python code should produce a notification appearing on your target device.</span></span>

## <a name="examples"></a><span data-ttu-id="ff01f-154">Примеры:</span><span class="sxs-lookup"><span data-stu-id="ff01f-154">Examples:</span></span>
### <a name="enabling-debug-property"></a><span data-ttu-id="ff01f-155">Включение свойства отладки</span><span class="sxs-lookup"><span data-stu-id="ff01f-155">Enabling debug property</span></span>
<span data-ttu-id="ff01f-156">Если включить флаг отладки во время инициализации центра уведомлений (NotificationHub), вы увидите подробный дамп HTTP-запроса и HTTP-ответа наряду с данными NotificationOutcome, которые указывают, какие именно заголовки HTTP переданы в запросе и какой HTTP-ответ был получен от центра уведомлений: ![][1]</span><span class="sxs-lookup"><span data-stu-id="ff01f-156">When you enable debug flag while initializing the NotificationHub then you will see detailed HTTP request and response dump as well as NotificationOutcome like the following where you can understand what HTTP headers are passed in the request and what HTTP response was received from the Notification Hub: ![][1]</span></span>

<span data-ttu-id="ff01f-157">Вы увидите подробный результат концентратора уведомлений, например сведения о том,</span><span class="sxs-lookup"><span data-stu-id="ff01f-157">You will see detailed Notification Hub result e.g.</span></span> 

* <span data-ttu-id="ff01f-158">когда сообщение успешно отправлено в службу push-уведомлений.</span><span class="sxs-lookup"><span data-stu-id="ff01f-158">when the message is successfully sent to the Push Notification Service.</span></span> 
  
        <Outcome>The Notification was successfully sent to the Push Notification System</Outcome>
* <span data-ttu-id="ff01f-159">Если какое-либо push-уведомление не достигло адресата, отобразится следующий ответ (указывающий, что, вероятнее всего, регистрации для доставки уведомлений не были найдены из-за несоответствующих тегов).</span><span class="sxs-lookup"><span data-stu-id="ff01f-159">If there were no targets found for any push notification then you are likely going to see the following in the response (which indicates that there were no registrations found to deliver the notification probably because the registrations had some mismatched tags)</span></span>
  
        '<NotificationOutcome xmlns="http://schemas.microsoft.com/netservices/2010/10/servicebus/connect" xmlns:i="http://www.w3.org/2001/XMLSchema-instance"><Success>0</Success><Failure>0</Failure><Results i:nil="true"/></NotificationOutcome>'

### <a name="broadcast-toast-notification-to-windows"></a><span data-ttu-id="ff01f-160">Рассылка всплывающих уведомлений для Windows</span><span class="sxs-lookup"><span data-stu-id="ff01f-160">Broadcast toast notification to Windows</span></span>
<span data-ttu-id="ff01f-161">Обратите внимание на заголовки, которые отправляются при рассылке всплывающих уведомлений клиенту Windows.</span><span class="sxs-lookup"><span data-stu-id="ff01f-161">Notice the headers that get sent out when you are sending a broadcast toast notification to Windows client.</span></span> 

    hub.send_windows_notification(wns_payload)

![][2]

### <a name="send-notification-specifying-a-tag-or-tag-expression"></a><span data-ttu-id="ff01f-162">Отправка уведомления с указанием тега (или регулярного выражения)</span><span class="sxs-lookup"><span data-stu-id="ff01f-162">Send notification specifying a tag (or tag expression)</span></span>
<span data-ttu-id="ff01f-163">Обратите внимание на заголовок Tags HTTP, который будет добавлен к запросу HTTP (в приведенном ниже примере мы отправляем уведомление только для регистраций с полезными данными "sports").</span><span class="sxs-lookup"><span data-stu-id="ff01f-163">Notice the Tags HTTP header which gets added to the HTTP request (in the example below, we are sending the notification only to registrations with 'sports' payload)</span></span>

    hub.send_windows_notification(wns_payload, "sports")

![][3]

### <a name="send-notification-specifying-multiple-tags"></a><span data-ttu-id="ff01f-164">Отправка уведомления с указанием нескольких тегов</span><span class="sxs-lookup"><span data-stu-id="ff01f-164">Send notification specifying multiple tags</span></span>
<span data-ttu-id="ff01f-165">Обратите внимание на изменения заголовка Tags HTTP при отправке нескольких тегов.</span><span class="sxs-lookup"><span data-stu-id="ff01f-165">Notice how the Tags HTTP header changes when multiple tags are sent.</span></span> 

    tags = {'sports', 'politics'}
    hub.send_windows_notification(wns_payload, tags)

![][4]

### <a name="templated-notification"></a><span data-ttu-id="ff01f-166">Шаблон уведомления</span><span class="sxs-lookup"><span data-stu-id="ff01f-166">Templated notification</span></span>
<span data-ttu-id="ff01f-167">Обратите внимание, что происходит изменение заголовка Format HTTP и текст полезных данных отправляется в составе запроса HTTP.</span><span class="sxs-lookup"><span data-stu-id="ff01f-167">Notice that the Format HTTP header changes and the payload body is sent as part of the HTTP request body:</span></span>

<span data-ttu-id="ff01f-168">**Сторона клиента — зарегистрированный шаблон**</span><span class="sxs-lookup"><span data-stu-id="ff01f-168">**Client side - registered template**</span></span>

        var template =
                        @"<toast><visual><binding template=""ToastText01""><text id=""1"">$(greeting_en)</text></binding></visual></toast>";

<span data-ttu-id="ff01f-169">**Серверная сторона — отправка полезных данных**</span><span class="sxs-lookup"><span data-stu-id="ff01f-169">**Server side - sending the payload**</span></span>

        template_payload = {'greeting_en': 'Hello', 'greeting_fr': 'Salut'}
        hub.send_template_notification(template_payload)

![][5]

## <a name="next-steps"></a><span data-ttu-id="ff01f-170">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="ff01f-170">Next Steps</span></span>
<span data-ttu-id="ff01f-171">В этой статье рассмотрено создание простого клиента Python REST для центров уведомлений.</span><span class="sxs-lookup"><span data-stu-id="ff01f-171">In this topic we showed how to create a simple Python REST client for Notification Hubs.</span></span> <span data-ttu-id="ff01f-172">На данном этапе можно сделать следующее.</span><span class="sxs-lookup"><span data-stu-id="ff01f-172">From here you can:</span></span>

* <span data-ttu-id="ff01f-173">Скачать полный [примере оболочки REST Python], содержащий весь используемый выше код.</span><span class="sxs-lookup"><span data-stu-id="ff01f-173">Download the full [Python REST wrapper sample], which contains all the code above.</span></span>
* <span data-ttu-id="ff01f-174">Продолжить изучение функции тегов в центрах уведомлений с помощью [учебника по передаче экстренных новостей]</span><span class="sxs-lookup"><span data-stu-id="ff01f-174">Continue learning about Notification Hubs tagging feature in the [Breaking News tutorial]</span></span>
* <span data-ttu-id="ff01f-175">Продолжить изучение функции шаблонов центров уведомлений в учебнике [по передаче локализованных экстренных новостей]</span><span class="sxs-lookup"><span data-stu-id="ff01f-175">Continue learning about Notification Hubs Templates feature in the [Localizing News tutorial]</span></span>

<!-- URLs -->
<span data-ttu-id="ff01f-176">[примере оболочки REST Python]: https://github.com/Azure/azure-notificationhubs-samples/tree/master/notificationhubs-rest-python</span><span class="sxs-lookup"><span data-stu-id="ff01f-176">[Python REST wrapper sample]: https://github.com/Azure/azure-notificationhubs-samples/tree/master/notificationhubs-rest-python</span></span>
<span data-ttu-id="ff01f-177">[Приступая к работе с центрами уведомлений]: http://azure.microsoft.com/documentation/articles/notification-hubs-windows-store-dotnet-get-started/</span><span class="sxs-lookup"><span data-stu-id="ff01f-177">[Get started tutorial]: http://azure.microsoft.com/documentation/articles/notification-hubs-windows-store-dotnet-get-started/</span></span>
<span data-ttu-id="ff01f-178">[учебника по передаче экстренных новостей]: http://azure.microsoft.com/documentation/articles/notification-hubs-windows-store-dotnet-send-breaking-news/</span><span class="sxs-lookup"><span data-stu-id="ff01f-178">[Breaking News tutorial]: http://azure.microsoft.com/documentation/articles/notification-hubs-windows-store-dotnet-send-breaking-news/</span></span>
<span data-ttu-id="ff01f-179">[по передаче локализованных экстренных новостей]: http://azure.microsoft.com/documentation/articles/notification-hubs-windows-store-dotnet-send-localized-breaking-news/</span><span class="sxs-lookup"><span data-stu-id="ff01f-179">[Localizing News tutorial]: http://azure.microsoft.com/documentation/articles/notification-hubs-windows-store-dotnet-send-localized-breaking-news/</span></span>

<!-- Images. -->
[1]: ./media/notification-hubs-python-backend-how-to/DetailedLoggingInfo.png
[2]: ./media/notification-hubs-python-backend-how-to/BroadcastScenario.png
[3]: ./media/notification-hubs-python-backend-how-to/SendWithOneTag.png
[4]: ./media/notification-hubs-python-backend-how-to/SendWithMultipleTags.png
[5]: ./media/notification-hubs-python-backend-how-to/TemplatedNotification.png

