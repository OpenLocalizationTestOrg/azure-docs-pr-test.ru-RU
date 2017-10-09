## <a name="create-hello-webapi-project"></a>Создание проекта WebAPI hello
В последующих разделах hello создается новую серверную часть ASP.NET WebAPI и он будет иметь три основные функции:

1. **Проверка подлинности клиентов**: будет добавлен обработчик сообщений, последующие запросы клиента tooauthenticate и свяжите hello пользователя с помощью запроса hello.
2. **Регистрации уведомлений клиента**: более поздней версии, вы добавите новые регистрации контроллера toohandle tooreceive уведомлений клиента устройства. Hello имя пользователя, прошедшего проверку подлинности будут автоматически добавлены регистрации toohello как [тега](https://msdn.microsoft.com/library/azure/dn530749.aspx).
3. **Отправка уведомлений tooClients**: более поздней версии, можно добавить контроллер tooprovide способом для пользователя tootrigger toodevices безопасного push и клиенты, связанные с тегом hello. 

Привет, следующие шаги показывают, как toocreate hello новую серверную часть ASP.NET WebAPI: 

> [!IMPORTANT]
> Если вы используете Visual Studio 2015 или более ранней версии, прежде чем запустить этот учебник, убедитесь, что вы установили последнюю версию диспетчера пакетов NuGet hello hello. toocheck запуска Visual Studio. Из hello **средства** меню, нажмите кнопку **расширения и обновления**. Поиск **диспетчера пакетов NuGet** для вашей версии Visual Studio и убедитесь, что у вас есть последняя версия hello. Если это не так, удалите и переустановите hello диспетчера пакетов NuGet.
> 
> ![][B4]
> 
> [!NOTE]
> Убедитесь, что вы установили Visual Studio hello [пакета Azure SDK](https://azure.microsoft.com/downloads/) для развертывания веб-сайта.
> 
> 

1. Запустите Visual Studio или Visual Studio Express. Нажмите кнопку **обозревателя серверов** и выполните вход tooyour учетная запись Azure. Вы вошли в toocreate hello веб-сайт ресурсов в вашей учетной записи потребуется Visual Studio.
2. В Visual Studio щелкните **файл**, нажмите кнопку **New**, затем **проекта**, разверните **шаблоны**, **Visual C#**, нажмите кнопку **Web** и **веб-приложения ASP.NET**, имя типа hello **AppBackend**, а затем нажмите кнопку **ОК**. 
   
    ![][B1]
3. В hello **новый проект ASP.NET** диалоговое окно, нажмите кнопку **веб-API**, нажмите кнопку **ОК**.
   
    ![][B2]
4. В hello **Настройка веб-приложения Microsoft Azure** диалоговое окно, выберите подписку и **план служб приложений** уже создан. Вы также можете **создать новый план служб приложений** и создать его в диалоговом окне приветствия. База данных для этого руководства не требуется. После выбора ваш план обслуживания приложений, щелкните **ОК** toocreate hello проекта.
   
    ![][B5]

## <a name="authenticating-clients-toohello-webapi-backend"></a>Проверка подлинности клиентов toohello WebAPI серверной части
В этом разделе вы создадите новый класс обработчика сообщений с именем **AuthenticationTestHandler** для hello новую серверную часть. Этот класс является производным от [DelegatingHandler](https://msdn.microsoft.com/library/system.net.http.delegatinghandler.aspx) и добавлена в качестве обработчика сообщений, чтобы он мог обрабатывать все запросы, поступающие в серверной части hello. 

1. В обозревателе решений щелкните правой кнопкой мыши hello **AppBackend** проекта, нажмите кнопку **добавить**, нажмите кнопку **класса**. Имя нового класса hello **AuthenticationTestHandler.cs**и нажмите кнопку **добавить** toogenerate hello класса. Этот класс будет использоваться tooauthenticate пользователей с помощью *обычной проверки подлинности* для простоты. Обратите внимание, что ваше приложение может использовать любую схему проверки подлинности.
2. В AuthenticationTestHandler.cs, добавьте следующее hello `using` инструкции:
   
        using System.Net.Http;
        using System.Threading;
        using System.Security.Principal;
        using System.Net;
        using System.Text;
        using System.Threading.Tasks;

3. В AuthenticationTestHandler.cs, заменив hello `AuthenticationTestHandler` определение класса с hello, следующий код. 
   
    Этот обработчик авторизует hello запрос, когда hello следующих трех условий:
   
   * запрос Hello, включенный *авторизации* заголовок. 
   * использует запрос Hello *основные* проверки подлинности. 
   * Hello строку имени пользователя и пароля строка hello являются hello же строку.
     
     В противном случае — запрос hello, будут отклонены. Этот подход нельзя назвать настоящим методом аутентификации и авторизации. Это очень простой пример для этого учебника.
     
     Если сообщение hello запроса проверку подлинности или авторизации hello `AuthenticationTestHandler`, то hello обычную проверку подлинности пользователя будет вложенного toohello текущего запроса на hello [HttpContext](https://msdn.microsoft.com/library/system.web.httpcontext.current.aspx). Сведения о пользователе в hello HttpContext будет использоваться другой контроллер (RegisterController) более поздней версии tooadd [тега](https://msdn.microsoft.com/library/azure/dn530749.aspx) запросе регистрации уведомления об toohello.
     
       public class AuthenticationTestHandler : DelegatingHandler   {       protected override Task<HttpResponseMessage> SendAsync(       HttpRequestMessage request, CancellationToken cancellationToken)       {           var authorizationHeader = request.Headers.GetValues("Authorization").First();
     
               if (authorizationHeader != null && authorizationHeader
                   .StartsWith("Basic ", StringComparison.InvariantCultureIgnoreCase))
               {
                   string authorizationUserAndPwdBase64 =
                       authorizationHeader.Substring("Basic ".Length);
                   string authorizationUserAndPwd = Encoding.Default
                       .GetString(Convert.FromBase64String(authorizationUserAndPwdBase64));
                   string user = authorizationUserAndPwd.Split(':')[0];
                   string password = authorizationUserAndPwd.Split(':')[1];
     
                   if (verifyUserAndPwd(user, password))
                   {
                       // Attach hello new principal object toohello current HttpContext object
                       HttpContext.Current.User =
                           new GenericPrincipal(new GenericIdentity(user), new string[0]);
                       System.Threading.Thread.CurrentPrincipal =
                           System.Web.HttpContext.Current.User;
                   }
                   else return Unauthorized();
               }
               else return Unauthorized();
     
               return base.SendAsync(request, cancellationToken);
           }
     
           private bool verifyUserAndPwd(string user, string password)
           {
               // This is not a real authentication scheme.
               return user == password;
           }
     
           private Task<HttpResponseMessage> Unauthorized()
           {
               var response = new HttpResponseMessage(HttpStatusCode.Forbidden);
               var tsc = new TaskCompletionSource<HttpResponseMessage>();
               tsc.SetResult(response);
               return tsc.Task;
           }
       }
     
     > [!NOTE]
     > **Примечание по безопасности**: hello `AuthenticationTestHandler` класс не предоставляет значение true, проверка подлинности. Он является обычной проверки подлинности используется только toomimic и не является безопасным. В реальных приложениях и службах необходимо реализовать безопасный механизм проверки подлинности.                
     > 
     > 
4. Добавьте следующий код в конце hello hello hello `Register` метод в hello **App_Start/WebApiConfig.cs** обработчик сообщений hello tooregister класса:
   
        config.MessageHandlers.Add(new AuthenticationTestHandler());
5. Сохраните изменения.

## <a name="registering-for-notifications-using-hello-webapi-backend"></a>Регистрация для получения уведомлений с помощью hello WebAPI серверной части
В этом разделе мы будем добавлять новые серверной toohandle WebAPI контроллера toohello запросы tooregister пользователя и устройства для уведомлений с использованием hello клиентская библиотека для концентраторов уведомлений. контроллер Hello добавит тег пользователя для пользователя hello, была выполнена проверка подлинности и присоединены toohello HttpContext по hello `AuthenticationTestHandler`. тег Hello будет иметь формат строки hello, `"username:<actual username>"`.

1. В обозревателе решений щелкните правой кнопкой мыши hello **AppBackend** проект и выберите пункт **управление пакетами NuGet**.
2. В левой части окна hello, выберите **Online**и выполните поиск **Microsoft.Azure.NotificationHubs** в hello **поиска** поле.
3. В списке результатов hello, нажмите кнопку **концентраторы уведомлений Microsoft Azure**, а затем нажмите кнопку **установить**. Завершение установки hello, а затем закройте окно диспетчера пакетов NuGet hello.
   
    При этом добавляется ссылка toohello концентраторов уведомлений Azure SDK с помощью hello <a href="http://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/">пакет NuGet концентраторов Microsoft.Azure.Notification</a>.
4. Теперь мы создадим новый файл класса, представляющий подключение hello с уведомлениями toosend использовать концентратор уведомлений. Hello обозревателе решений щелкните правой кнопкой мыши hello **моделей** папку, нажмите кнопку **добавить**, нажмите кнопку **класса**. Имя нового класса hello **Notifications.cs**, нажмите кнопку **добавить** toogenerate hello класса. 
   
    ![][B6]
5. В Notifications.cs, добавьте следующее hello `using` в начало файла hello hello инструкцию:
   
        using Microsoft.Azure.NotificationHubs;
6. Замените hello `Notifications` определения следующий hello класса и убедитесь, что tooreplace hello двух местозаполнителей hello строки подключения (с полным доступом) для центра уведомлений hello имя концентратора (найти по адресу [классический портал Azure ](http://manage.windowsazure.com)):
   
        public class Notifications
        {
            public static Notifications Instance = new Notifications();
   
            public NotificationHubClient Hub { get; set; }
   
            private Notifications() {
                Hub = NotificationHubClient.CreateClientFromConnectionString("<your hub's DefaultFullSharedAccessSignature>", 
                                                                             "<hub name>");
            }
        }
7. Далее мы создадим новый контроллер с именем **RegisterController**. В обозревателе решений щелкните правой кнопкой мыши hello **контроллеров** папку, нажмите кнопку **добавить**, нажмите кнопку **контроллера**. Нажмите кнопку hello **контроллер 2 API веб - пустой** , а затем щелкните **добавить**. Имя нового класса hello **RegisterController**, а затем нажмите кнопку **добавить** снова toogenerate hello контроллера.
   
    ![][B7]
   
    ![][B8]
8. В RegisterController.cs, добавьте следующее hello `using` инструкции:
   
        using Microsoft.Azure.NotificationHubs;
        using Microsoft.Azure.NotificationHubs.Messaging;
        using AppBackend.Models;
        using System.Threading.Tasks;
        using System.Web;
9. Добавьте следующий код внутри hello hello `RegisterController` определения класса. Обратите внимание, что в этом коде мы добавить тег пользователя для пользователя hello, это присоединен toohello HttpContext. Hello пользователя была выполнена проверка подлинности и присоединенного toohello HttpContext фильтром сообщения hello, мы добавили `AuthenticationTestHandler`. Можно также добавить tooverify дополнительных проверок, hello пользователя имеет права tooregister для hello запрошенный тегов.
   
        private NotificationHubClient hub;
   
        public RegisterController()
        {
            hub = Notifications.Instance.Hub;
        }
   
        public class DeviceRegistration
        {
            public string Platform { get; set; }
            public string Handle { get; set; }
            public string[] Tags { get; set; }
        }
   
        // POST api/register
        // This creates a registration id
        public async Task<string> Post(string handle = null)
        {
            string newRegistrationId = null;
   
            // make sure there are no existing registrations for this push handle (used for iOS and Android)
            if (handle != null)
            {
                var registrations = await hub.GetRegistrationsByChannelAsync(handle, 100);
   
                foreach (RegistrationDescription registration in registrations)
                {
                    if (newRegistrationId == null)
                    {
                        newRegistrationId = registration.RegistrationId;
                    }
                    else
                    {
                        await hub.DeleteRegistrationAsync(registration);
                    }
                }
            }
   
            if (newRegistrationId == null) 
                newRegistrationId = await hub.CreateRegistrationIdAsync();
   
            return newRegistrationId;
        }
   
        // PUT api/register/5
        // This creates or updates a registration (with provided channelURI) at hello specified id
        public async Task<HttpResponseMessage> Put(string id, DeviceRegistration deviceUpdate)
        {
            RegistrationDescription registration = null;
            switch (deviceUpdate.Platform)
            {
                case "mpns":
                    registration = new MpnsRegistrationDescription(deviceUpdate.Handle);
                    break;
                case "wns":
                    registration = new WindowsRegistrationDescription(deviceUpdate.Handle);
                    break;
                case "apns":
                    registration = new AppleRegistrationDescription(deviceUpdate.Handle);
                    break;
                case "gcm":
                    registration = new GcmRegistrationDescription(deviceUpdate.Handle);
                    break;
                default:
                    throw new HttpResponseException(HttpStatusCode.BadRequest);
            }
   
            registration.RegistrationId = id;
            var username = HttpContext.Current.User.Identity.Name;
   
            // add check if user is allowed tooadd these tags
            registration.Tags = new HashSet<string>(deviceUpdate.Tags);
            registration.Tags.Add("username:" + username);
   
            try
            {
                await hub.CreateOrUpdateRegistrationAsync(registration);
            }
            catch (MessagingException e)
            {
                ReturnGoneIfHubResponseIsGone(e);
            }
   
            return Request.CreateResponse(HttpStatusCode.OK);
        }
   
        // DELETE api/register/5
        public async Task<HttpResponseMessage> Delete(string id)
        {
            await hub.DeleteRegistrationAsync(id);
            return Request.CreateResponse(HttpStatusCode.OK);
        }
   
        private static void ReturnGoneIfHubResponseIsGone(MessagingException e)
        {
            var webex = e.InnerException as WebException;
            if (webex.Status == WebExceptionStatus.ProtocolError)
            {
                var response = (HttpWebResponse)webex.Response;
                if (response.StatusCode == HttpStatusCode.Gone)
                    throw new HttpRequestException(HttpStatusCode.Gone.ToString());
            }
        }
10. Сохраните изменения.

## <a name="sending-notifications-from-hello-webapi-backend"></a>Отправка уведомлений из hello WebAPI серверной части
В этом разделе добавьте новый контроллера, который предоставляет способ для клиентских устройств toosend уведомление на теге hello имя пользователя, с помощью библиотеки управления службы концентраторов уведомлений Azure в серверной части ASP.NET WebAPI hello.

1. Создайте еще один новый контроллер с именем **NotificationsController**. Создайте его hello так же, как вы создали hello **RegisterController** в предыдущем разделе hello.
2. В NotificationsController.cs, добавьте следующее hello `using` инструкции:
   
        using AppBackend.Models;
        using System.Threading.Tasks;
        using System.Web;
3. Добавьте следующий метод toohello hello **NotificationsController** класса.
   
    Этот код отправки уведомлений тип, основанный на hello службы уведомлений платформы (PNS) `pns` параметра. Здравствуйте, значение `to_tag` — hello используется tooset *username* тега приветственное сообщение. Этот тег должен соответствовать тегу имени пользователя активной регистрации центра уведомлений. сообщение уведомления Hello извлечено из hello тексте запроса POST hello и формат для целевого объекта hello PNS. 
   
    В зависимости от hello платформы уведомления службы (PNS), поддерживаемых устройств использовать уведомления tooreceive различных уведомлений поддерживаются различные форматы. Например, на устройствах Windows можно использовать [всплывающие уведомления с помощью WNS](https://msdn.microsoft.com/library/windows/apps/br230849.aspx), которые не поддерживаются другой PNS. Поэтому серверной части понадобится tooformat hello уведомления в поддерживаемых уведомление для hello PNS устройств при планировании toosupport. Затем с помощью API hello соответствующие отправки на hello [NotificationHubClient-класс](https://msdn.microsoft.com/library/azure/microsoft.azure.notificationhubs.notificationhubclient_methods.aspx)
   
        public async Task<HttpResponseMessage> Post(string pns, [FromBody]string message, string to_tag)
        {
            var user = HttpContext.Current.User.Identity.Name;
            string[] userTag = new string[2];
            userTag[0] = "username:" + to_tag;
            userTag[1] = "from:" + user;
   
            Microsoft.Azure.NotificationHubs.NotificationOutcome outcome = null;
            HttpStatusCode ret = HttpStatusCode.InternalServerError;
   
            switch (pns.ToLower())
            {
                case "wns":
                    // Windows 8.1 / Windows Phone 8.1
                    var toast = @"<toast><visual><binding template=""ToastText01""><text id=""1"">" + 
                                "From " + user + ": " + message + "</text></binding></visual></toast>";
                    outcome = await Notifications.Instance.Hub.SendWindowsNativeNotificationAsync(toast, userTag);
                    break;
                case "apns":
                    // iOS
                    var alert = "{\"aps\":{\"alert\":\"" + "From " + user + ": " + message + "\"}}";
                    outcome = await Notifications.Instance.Hub.SendAppleNativeNotificationAsync(alert, userTag);
                    break;
                case "gcm":
                    // Android
                    var notif = "{ \"data\" : {\"message\":\"" + "From " + user + ": " + message + "\"}}";
                    outcome = await Notifications.Instance.Hub.SendGcmNativeNotificationAsync(notif, userTag);
                    break;
            }
   
            if (outcome != null)
            {
                if (!((outcome.State == Microsoft.Azure.NotificationHubs.NotificationOutcomeState.Abandoned) ||
                    (outcome.State == Microsoft.Azure.NotificationHubs.NotificationOutcomeState.Unknown)))
                {
                    ret = HttpStatusCode.OK;
                }
            }
   
            return Request.CreateResponse(ret);
        }
4. Нажмите клавишу **F5** toorun hello и tooensure приложения hello точности своей работы к текущему моменту. приложение Hello должен запустить веб-браузер и отобразить hello ASP.NET домашней страницы. 

## <a name="publish-hello-new-webapi-backend"></a>Публикация hello новую серверную часть WebAPI
1. Теперь мы Развернем tooan этого приложения веб-сайта Azure, в порядке toomake доступ из всех устройств. Щелкните правой кнопкой мыши на hello **AppBackend** проект и выберите **публикации**.
2. Выберите **службу приложений Microsoft Azure** в качестве цели публикации и щелкните **Опубликовать**. Откроется диалоговое окно hello Создание приложения службы, который поможет создать все hello необходимые ресурсы Azure toorun hello, ASP.NET веб-приложения в Azure.

    ![][B15]
3. В hello **Создание приложения службы** диалоговое окно, выберите учетную запись Azure. Щелкните **Изменить тип** и выберите **Веб-приложение**. Сохранить hello **имя веб-приложения** заданную и выберите hello **подписки**, **группы ресурсов**, и **план служб приложений**.  Щелкните **Создать**.

4. Запишите hello **URL-адрес сайта** свойство в hello **Сводка** раздела. Мы будем называть toothis URL-адрес, как ваш *конечную точку серверной части* далее в этом учебнике. Щелкните **Опубликовать**.

5. После завершения работы мастера hello, он публикует hello ASP.NET web app tooAzure и затем запускает hello приложение в браузере по умолчанию hello.  Приложение можно будет просмотреть в службах приложений Azure.

URL-адрес Hello использует имя веб-приложения hello, указанный ранее, с http://<app_name>.azurewebsites.net формат hello.

[B1]: ./media/notification-hubs-aspnet-backend-notifyusers/notification-hubs-secure-push1.png
[B2]: ./media/notification-hubs-aspnet-backend-notifyusers/notification-hubs-secure-push2.png
[B3]: ./media/notification-hubs-aspnet-backend-notifyusers/notification-hubs-secure-push3.png
[B4]: ./media/notification-hubs-aspnet-backend-notifyusers/notification-hubs-secure-push4.png
[B5]: ./media/notification-hubs-aspnet-backend-notifyusers/notification-hubs-secure-push5.png
[B6]: ./media/notification-hubs-aspnet-backend-notifyusers/notification-hubs-secure-push6.png
[B7]: ./media/notification-hubs-aspnet-backend-notifyusers/notification-hubs-secure-push7.png
[B8]: ./media/notification-hubs-aspnet-backend-notifyusers/notification-hubs-secure-push8.png
[B14]: ./media/notification-hubs-aspnet-backend-notifyusers/notification-hubs-secure-push14.png
[B15]: ./media/notification-hubs-aspnet-backend-notifyusers/publish-to-app-service.png
[B16]: ./media/notification-hubs-aspnet-backend-notifyusers/notification-hubs-notify-users16.PNG
[B18]: ./media/notification-hubs-aspnet-backend-notifyusers/notification-hubs-notify-users18.PNG
