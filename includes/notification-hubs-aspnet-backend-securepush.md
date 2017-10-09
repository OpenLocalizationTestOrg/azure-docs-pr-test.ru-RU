## <a name="webapi-project"></a><span data-ttu-id="9bed1-101">Проект веб-интерфейса API</span><span class="sxs-lookup"><span data-stu-id="9bed1-101">WebAPI Project</span></span>
1. <span data-ttu-id="9bed1-102">В Visual Studio откройте hello **AppBackend** проекта, созданного в hello **уведомить пользователей** учебника.</span><span class="sxs-lookup"><span data-stu-id="9bed1-102">In Visual Studio, open hello **AppBackend** project that you created in hello **Notify Users** tutorial.</span></span>
2. <span data-ttu-id="9bed1-103">В Notifications.cs hello замены всего **уведомления** класса hello, следующий код.</span><span class="sxs-lookup"><span data-stu-id="9bed1-103">In Notifications.cs, replace hello whole **Notifications** class with hello following code.</span></span> <span data-ttu-id="9bed1-104">Быть убедиться, что tooreplace hello местозаполнителей строки подключения (с полным доступом) для концентратора уведомлений, а также имя концентратора hello.</span><span class="sxs-lookup"><span data-stu-id="9bed1-104">Be sure tooreplace hello placeholders with your connection string (with full access) for your notification hub, and hello hub name.</span></span> <span data-ttu-id="9bed1-105">Эти значения можно получить из hello [классический портал Azure](http://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="9bed1-105">You can obtain these values from hello [Azure Classic Portal](http://manage.windowsazure.com).</span></span> <span data-ttu-id="9bed1-106">Теперь этот модуль представляет hello различных безопасных уведомлений, которые будут отправляться.</span><span class="sxs-lookup"><span data-stu-id="9bed1-106">This module now represents hello different secure notifications that will be sent.</span></span> <span data-ttu-id="9bed1-107">В полную реализацию hello уведомления будут храниться в базе данных; для простоты в этом случае мы их сохранения в памяти.</span><span class="sxs-lookup"><span data-stu-id="9bed1-107">In a complete implementation, hello notifications will be stored in a database; for simplicity, in this case we store them in memory.</span></span>
   
        public class Notification
        {
            public int Id { get; set; }
            public string Payload { get; set; }
            public bool Read { get; set; }
        }

        public class Notifications
        {
            public static Notifications Instance = new Notifications();

            private List<Notification> notifications = new List<Notification>();

            public NotificationHubClient Hub { get; set; }

            private Notifications() {
                Hub = NotificationHubClient.CreateClientFromConnectionString("{conn string with full access}",     "{hub name}");
            }

            public Notification CreateNotification(string payload)
            {
                var notification = new Notification() {
                Id = notifications.Count,
                Payload = payload,
                Read = false
                };

                notifications.Add(notification);

                return notification;
            }

            public Notification ReadNotification(int id)
            {
                return notifications.ElementAt(id);
            }
        }

1. <span data-ttu-id="9bed1-108">Замените код hello внутри hello в NotificationsController.cs, **NotificationsController** определение класса с hello, следующий код.</span><span class="sxs-lookup"><span data-stu-id="9bed1-108">In NotificationsController.cs, replace hello code inside hello **NotificationsController** class definition with hello following code.</span></span> <span data-ttu-id="9bed1-109">Этот компонент реализует безопасный способ уведомления hello tooretrieve устройства hello и tooyour принудительной безопасности устройств также предоставляет tootrigger способом (для целей данного учебника hello).</span><span class="sxs-lookup"><span data-stu-id="9bed1-109">This component implements a way for hello device tooretrieve hello notification securely, and also provides a way (for hello purposes of this tutorial) tootrigger a secure push tooyour devices.</span></span> <span data-ttu-id="9bed1-110">Обратите внимание, что при отправке концентратора уведомлений toohello уведомления hello, мы только отправлять необработанные уведомление с Идентификатором hello hello уведомления (и не фактическое сообщение об ошибке).</span><span class="sxs-lookup"><span data-stu-id="9bed1-110">Note that when sending hello notification toohello notification hub, we only send a raw notification with hello ID of hello notification (and no actual message):</span></span>
   
       public NotificationsController()
       {
           Notifications.Instance.CreateNotification("This is a secure notification!");
       }
   
       // GET api/notifications/id
       public Notification Get(int id)
       {
           return Notifications.Instance.ReadNotification(id);
       }
   
       public async Task<HttpResponseMessage> Post()
       {
           var secureNotificationInTheBackend = Notifications.Instance.CreateNotification("Secure confirmation.");
           var usernameTag = "username:" + HttpContext.Current.User.Identity.Name;
   
           // windows
           var rawNotificationToBeSent = new Microsoft.Azure.NotificationHubs.WindowsNotification(secureNotificationInTheBackend.Id.ToString(),
                           new Dictionary<string, string> {
                               {"X-WNS-Type", "wns/raw"}
                           });
           await Notifications.Instance.Hub.SendNotificationAsync(rawNotificationToBeSent, usernameTag);
   
           // apns
           await Notifications.Instance.Hub.SendAppleNativeNotificationAsync("{\"aps\": {\"content-available\": 1}, \"secureId\": \"" + secureNotificationInTheBackend.Id.ToString() + "\"}", usernameTag);
   
           // gcm
           await Notifications.Instance.Hub.SendGcmNativeNotificationAsync("{\"data\": {\"secureId\": \"" + secureNotificationInTheBackend.Id.ToString() + "\"}}", usernameTag);

            return Request.CreateResponse(HttpStatusCode.OK);
        }


<span data-ttu-id="9bed1-111">Обратите внимание, что hello `Post` метод теперь не отправляет всплывающее уведомление.</span><span class="sxs-lookup"><span data-stu-id="9bed1-111">Note that hello `Post` method now does not send a toast notification.</span></span> <span data-ttu-id="9bed1-112">Отправляет необработанное уведомление, которое содержит только идентификатор уведомления hello и не конфиденциальное содержимое.</span><span class="sxs-lookup"><span data-stu-id="9bed1-112">It sends a raw notification that contains only hello notification ID, and not any sensitive content.</span></span> <span data-ttu-id="9bed1-113">Также необходимо убедиться, что toocomment hello операции для hello платформ, для которых у вас учетными данными, настроенными на концентратор уведомлений, поскольку они приводят к ошибкам передачи.</span><span class="sxs-lookup"><span data-stu-id="9bed1-113">Also, make sure toocomment hello send operation for hello platforms for which you do not have credentials configured on your notification hub, as they will result in errors.</span></span>

1. <span data-ttu-id="9bed1-114">Теперь мы будет повторное развертывание этого приложения tooan веб-сайта Azure, в порядке toomake доступ из всех устройств.</span><span class="sxs-lookup"><span data-stu-id="9bed1-114">Now we will re-deploy this app tooan Azure Website in order toomake it accessible from all devices.</span></span> <span data-ttu-id="9bed1-115">Щелкните правой кнопкой мыши на hello **AppBackend** проект и выберите **публикации**.</span><span class="sxs-lookup"><span data-stu-id="9bed1-115">Right-click on hello **AppBackend** project and select **Publish**.</span></span>
2. <span data-ttu-id="9bed1-116">Выберите в качестве цели публикации веб-сайт Azure.</span><span class="sxs-lookup"><span data-stu-id="9bed1-116">Select Azure Website as your publish target.</span></span> <span data-ttu-id="9bed1-117">Войти с учетной записью Azure и выберите существующий или новый веб-сайт и запишите hello **URL-адрес назначения** свойство в hello **подключения** вкладки. Мы будем называть toothis URL-адрес, как ваш *конечную точку серверной части* далее в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="9bed1-117">Log in with your Azure account and select an existing or new Website, and make a note of hello **destination URL** property in hello **Connection** tab. We will refer toothis URL as your *backend endpoint* later in this tutorial.</span></span> <span data-ttu-id="9bed1-118">Щелкните **Опубликовать**.</span><span class="sxs-lookup"><span data-stu-id="9bed1-118">Click **Publish**.</span></span>

