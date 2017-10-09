## <a name="webapi-project"></a>Проект веб-интерфейса API
1. В Visual Studio откройте hello **AppBackend** проекта, созданного в hello **уведомить пользователей** учебника.
2. В Notifications.cs hello замены всего **уведомления** класса hello, следующий код. Быть убедиться, что tooreplace hello местозаполнителей строки подключения (с полным доступом) для концентратора уведомлений, а также имя концентратора hello. Эти значения можно получить из hello [классический портал Azure](http://manage.windowsazure.com). Теперь этот модуль представляет hello различных безопасных уведомлений, которые будут отправляться. В полную реализацию hello уведомления будут храниться в базе данных; для простоты в этом случае мы их сохранения в памяти.
   
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

1. Замените код hello внутри hello в NotificationsController.cs, **NotificationsController** определение класса с hello, следующий код. Этот компонент реализует безопасный способ уведомления hello tooretrieve устройства hello и tooyour принудительной безопасности устройств также предоставляет tootrigger способом (для целей данного учебника hello). Обратите внимание, что при отправке концентратора уведомлений toohello уведомления hello, мы только отправлять необработанные уведомление с Идентификатором hello hello уведомления (и не фактическое сообщение об ошибке).
   
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


Обратите внимание, что hello `Post` метод теперь не отправляет всплывающее уведомление. Отправляет необработанное уведомление, которое содержит только идентификатор уведомления hello и не конфиденциальное содержимое. Также необходимо убедиться, что toocomment hello операции для hello платформ, для которых у вас учетными данными, настроенными на концентратор уведомлений, поскольку они приводят к ошибкам передачи.

1. Теперь мы будет повторное развертывание этого приложения tooan веб-сайта Azure, в порядке toomake доступ из всех устройств. Щелкните правой кнопкой мыши на hello **AppBackend** проект и выберите **публикации**.
2. Выберите в качестве цели публикации веб-сайт Azure. Войти с учетной записью Azure и выберите существующий или новый веб-сайт и запишите hello **URL-адрес назначения** свойство в hello **подключения** вкладки. Мы будем называть toothis URL-адрес, как ваш *конечную точку серверной части* далее в этом учебнике. Щелкните **Опубликовать**.

