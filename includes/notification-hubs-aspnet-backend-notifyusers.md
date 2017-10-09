## <a name="create-hello-webapi-project"></a><span data-ttu-id="d2d7d-101">Создание проекта WebAPI hello</span><span class="sxs-lookup"><span data-stu-id="d2d7d-101">Create hello WebAPI Project</span></span>
<span data-ttu-id="d2d7d-102">В последующих разделах hello создается новую серверную часть ASP.NET WebAPI и он будет иметь три основные функции:</span><span class="sxs-lookup"><span data-stu-id="d2d7d-102">A new ASP.NET WebAPI backend will be created in hello sections that follow and it will have three main purposes:</span></span>

1. <span data-ttu-id="d2d7d-103">**Проверка подлинности клиентов**: будет добавлен обработчик сообщений, последующие запросы клиента tooauthenticate и свяжите hello пользователя с помощью запроса hello.</span><span class="sxs-lookup"><span data-stu-id="d2d7d-103">**Authenticating Clients**: A message handler will be added later tooauthenticate client requests and associate hello user with hello request.</span></span>
2. <span data-ttu-id="d2d7d-104">**Регистрации уведомлений клиента**: более поздней версии, вы добавите новые регистрации контроллера toohandle tooreceive уведомлений клиента устройства.</span><span class="sxs-lookup"><span data-stu-id="d2d7d-104">**Client Notification Registrations**: Later, you will add a controller toohandle new registrations for a client device tooreceive notifications.</span></span> <span data-ttu-id="d2d7d-105">Hello имя пользователя, прошедшего проверку подлинности будут автоматически добавлены регистрации toohello как [тега](https://msdn.microsoft.com/library/azure/dn530749.aspx).</span><span class="sxs-lookup"><span data-stu-id="d2d7d-105">hello authenticated user name will automatically be added toohello registration as a [tag](https://msdn.microsoft.com/library/azure/dn530749.aspx).</span></span>
3. <span data-ttu-id="d2d7d-106">**Отправка уведомлений tooClients**: более поздней версии, можно добавить контроллер tooprovide способом для пользователя tootrigger toodevices безопасного push и клиенты, связанные с тегом hello.</span><span class="sxs-lookup"><span data-stu-id="d2d7d-106">**Sending Notifications tooClients**: Later, you will also add a controller tooprovide a way for a user tootrigger a secure push toodevices and clients associated with hello tag.</span></span> 

<span data-ttu-id="d2d7d-107">Привет, следующие шаги показывают, как toocreate hello новую серверную часть ASP.NET WebAPI:</span><span class="sxs-lookup"><span data-stu-id="d2d7d-107">hello following steps show how toocreate hello new ASP.NET WebAPI backend:</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="d2d7d-108">Если вы используете Visual Studio 2015 или более ранней версии, прежде чем запустить этот учебник, убедитесь, что вы установили последнюю версию диспетчера пакетов NuGet hello hello.</span><span class="sxs-lookup"><span data-stu-id="d2d7d-108">If you are using Visual Studio 2015 or earlier, before starting this tutorial, please ensure that you have installed hello latest version of hello NuGet Package Manager.</span></span> <span data-ttu-id="d2d7d-109">toocheck запуска Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="d2d7d-109">toocheck, start Visual Studio.</span></span> <span data-ttu-id="d2d7d-110">Из hello **средства** меню, нажмите кнопку **расширения и обновления**.</span><span class="sxs-lookup"><span data-stu-id="d2d7d-110">From hello **Tools** menu, click **Extensions and Updates**.</span></span> <span data-ttu-id="d2d7d-111">Поиск **диспетчера пакетов NuGet** для вашей версии Visual Studio и убедитесь, что у вас есть последняя версия hello.</span><span class="sxs-lookup"><span data-stu-id="d2d7d-111">Search for **NuGet Package Manager** for your version of Visual Studio, and make sure you have hello latest version.</span></span> <span data-ttu-id="d2d7d-112">Если это не так, удалите и переустановите hello диспетчера пакетов NuGet.</span><span class="sxs-lookup"><span data-stu-id="d2d7d-112">If not, please uninstall, then reinstall hello NuGet Package Manager.</span></span>
> 
> ![][B4]
> 
> [!NOTE]
> <span data-ttu-id="d2d7d-113">Убедитесь, что вы установили Visual Studio hello [пакета Azure SDK](https://azure.microsoft.com/downloads/) для развертывания веб-сайта.</span><span class="sxs-lookup"><span data-stu-id="d2d7d-113">Make sure you have installed hello Visual Studio [Azure SDK](https://azure.microsoft.com/downloads/) for website deployment.</span></span>
> 
> 

1. <span data-ttu-id="d2d7d-114">Запустите Visual Studio или Visual Studio Express.</span><span class="sxs-lookup"><span data-stu-id="d2d7d-114">Start Visual Studio or Visual Studio Express.</span></span> <span data-ttu-id="d2d7d-115">Нажмите кнопку **обозревателя серверов** и выполните вход tooyour учетная запись Azure.</span><span class="sxs-lookup"><span data-stu-id="d2d7d-115">Click **Server Explorer** and sign in tooyour Azure account.</span></span> <span data-ttu-id="d2d7d-116">Вы вошли в toocreate hello веб-сайт ресурсов в вашей учетной записи потребуется Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="d2d7d-116">Visual Studio will need you signed in toocreate hello web site resources on your account.</span></span>
2. <span data-ttu-id="d2d7d-117">В Visual Studio щелкните **файл**, нажмите кнопку **New**, затем **проекта**, разверните **шаблоны**, **Visual C#**, нажмите кнопку **Web** и **веб-приложения ASP.NET**, имя типа hello **AppBackend**, а затем нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="d2d7d-117">In Visual Studio, click **File**, then click **New**, then **Project**, expand **Templates**, **Visual C#**, then click **Web** and **ASP.NET Web Application**, type hello name **AppBackend**, and then click **OK**.</span></span> 
   
    ![][B1]
3. <span data-ttu-id="d2d7d-118">В hello **новый проект ASP.NET** диалоговое окно, нажмите кнопку **веб-API**, нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="d2d7d-118">In hello **New ASP.NET Project** dialog, click **Web API**, then click **OK**.</span></span>
   
    ![][B2]
4. <span data-ttu-id="d2d7d-119">В hello **Настройка веб-приложения Microsoft Azure** диалоговое окно, выберите подписку и **план служб приложений** уже создан.</span><span class="sxs-lookup"><span data-stu-id="d2d7d-119">In hello **Configure Microsoft Azure Web App** dialog, choose a subscription, and an **App Service plan** you have already created.</span></span> <span data-ttu-id="d2d7d-120">Вы также можете **создать новый план служб приложений** и создать его в диалоговом окне приветствия.</span><span class="sxs-lookup"><span data-stu-id="d2d7d-120">You can also choose **Create a new app service plan** and create one from hello dialog.</span></span> <span data-ttu-id="d2d7d-121">База данных для этого руководства не требуется.</span><span class="sxs-lookup"><span data-stu-id="d2d7d-121">You do not need a database for this tutorial.</span></span> <span data-ttu-id="d2d7d-122">После выбора ваш план обслуживания приложений, щелкните **ОК** toocreate hello проекта.</span><span class="sxs-lookup"><span data-stu-id="d2d7d-122">Once you have selected your app service plan, click **OK** toocreate hello project.</span></span>
   
    ![][B5]

## <a name="authenticating-clients-toohello-webapi-backend"></a><span data-ttu-id="d2d7d-123">Проверка подлинности клиентов toohello WebAPI серверной части</span><span class="sxs-lookup"><span data-stu-id="d2d7d-123">Authenticating Clients toohello WebAPI Backend</span></span>
<span data-ttu-id="d2d7d-124">В этом разделе вы создадите новый класс обработчика сообщений с именем **AuthenticationTestHandler** для hello новую серверную часть.</span><span class="sxs-lookup"><span data-stu-id="d2d7d-124">In this section, you will create a new message handler class named **AuthenticationTestHandler** for hello new backend.</span></span> <span data-ttu-id="d2d7d-125">Этот класс является производным от [DelegatingHandler](https://msdn.microsoft.com/library/system.net.http.delegatinghandler.aspx) и добавлена в качестве обработчика сообщений, чтобы он мог обрабатывать все запросы, поступающие в серверной части hello.</span><span class="sxs-lookup"><span data-stu-id="d2d7d-125">This class is derived from [DelegatingHandler](https://msdn.microsoft.com/library/system.net.http.delegatinghandler.aspx) and added as a message handler so it can process all requests coming into hello backend.</span></span> 

1. <span data-ttu-id="d2d7d-126">В обозревателе решений щелкните правой кнопкой мыши hello **AppBackend** проекта, нажмите кнопку **добавить**, нажмите кнопку **класса**.</span><span class="sxs-lookup"><span data-stu-id="d2d7d-126">In Solution Explorer, right-click hello **AppBackend** project, click **Add**, then click **Class**.</span></span> <span data-ttu-id="d2d7d-127">Имя нового класса hello **AuthenticationTestHandler.cs**и нажмите кнопку **добавить** toogenerate hello класса.</span><span class="sxs-lookup"><span data-stu-id="d2d7d-127">Name hello new class **AuthenticationTestHandler.cs**, and click **Add** toogenerate hello class.</span></span> <span data-ttu-id="d2d7d-128">Этот класс будет использоваться tooauthenticate пользователей с помощью *обычной проверки подлинности* для простоты.</span><span class="sxs-lookup"><span data-stu-id="d2d7d-128">This class will be used tooauthenticate users using *Basic Authentication* for simplicity.</span></span> <span data-ttu-id="d2d7d-129">Обратите внимание, что ваше приложение может использовать любую схему проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="d2d7d-129">Note that your app can use any authentication scheme.</span></span>
2. <span data-ttu-id="d2d7d-130">В AuthenticationTestHandler.cs, добавьте следующее hello `using` инструкции:</span><span class="sxs-lookup"><span data-stu-id="d2d7d-130">In AuthenticationTestHandler.cs, add hello following `using` statements:</span></span>
   
        using System.Net.Http;
        using System.Threading;
        using System.Security.Principal;
        using System.Net;
        using System.Text;
        using System.Threading.Tasks;

3. <span data-ttu-id="d2d7d-131">В AuthenticationTestHandler.cs, заменив hello `AuthenticationTestHandler` определение класса с hello, следующий код.</span><span class="sxs-lookup"><span data-stu-id="d2d7d-131">In AuthenticationTestHandler.cs, replacing hello `AuthenticationTestHandler` class definition with hello following code.</span></span> 
   
    <span data-ttu-id="d2d7d-132">Этот обработчик авторизует hello запрос, когда hello следующих трех условий:</span><span class="sxs-lookup"><span data-stu-id="d2d7d-132">This handler will authorize hello request when hello following three conditions are all true:</span></span>
   
   * <span data-ttu-id="d2d7d-133">запрос Hello, включенный *авторизации* заголовок.</span><span class="sxs-lookup"><span data-stu-id="d2d7d-133">hello request included an *Authorization* header.</span></span> 
   * <span data-ttu-id="d2d7d-134">использует запрос Hello *основные* проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="d2d7d-134">hello request uses *basic* authentication.</span></span> 
   * <span data-ttu-id="d2d7d-135">Hello строку имени пользователя и пароля строка hello являются hello же строку.</span><span class="sxs-lookup"><span data-stu-id="d2d7d-135">hello user name string and hello password string are hello same string.</span></span>
     
     <span data-ttu-id="d2d7d-136">В противном случае — запрос hello, будут отклонены.</span><span class="sxs-lookup"><span data-stu-id="d2d7d-136">Otherwise, hello request will be rejected.</span></span> <span data-ttu-id="d2d7d-137">Этот подход нельзя назвать настоящим методом аутентификации и авторизации.</span><span class="sxs-lookup"><span data-stu-id="d2d7d-137">This is not a true authentication and authorization approach.</span></span> <span data-ttu-id="d2d7d-138">Это очень простой пример для этого учебника.</span><span class="sxs-lookup"><span data-stu-id="d2d7d-138">It is just a very simple example for this tutorial.</span></span>
     
     <span data-ttu-id="d2d7d-139">Если сообщение hello запроса проверку подлинности или авторизации hello `AuthenticationTestHandler`, то hello обычную проверку подлинности пользователя будет вложенного toohello текущего запроса на hello [HttpContext](https://msdn.microsoft.com/library/system.web.httpcontext.current.aspx).</span><span class="sxs-lookup"><span data-stu-id="d2d7d-139">If hello request message is authenticated and authorized by hello `AuthenticationTestHandler`, then hello basic authentication user will be attached toohello current request on hello [HttpContext](https://msdn.microsoft.com/library/system.web.httpcontext.current.aspx).</span></span> <span data-ttu-id="d2d7d-140">Сведения о пользователе в hello HttpContext будет использоваться другой контроллер (RegisterController) более поздней версии tooadd [тега](https://msdn.microsoft.com/library/azure/dn530749.aspx) запросе регистрации уведомления об toohello.</span><span class="sxs-lookup"><span data-stu-id="d2d7d-140">User information in hello HttpContext will be used by another controller (RegisterController) later tooadd a [tag](https://msdn.microsoft.com/library/azure/dn530749.aspx) toohello notification registration request.</span></span>
     
       <span data-ttu-id="d2d7d-141">public class AuthenticationTestHandler : DelegatingHandler   {       protected override Task<HttpResponseMessage> SendAsync(       HttpRequestMessage request, CancellationToken cancellationToken)       {           var authorizationHeader = request.Headers.GetValues("Authorization").First();</span><span class="sxs-lookup"><span data-stu-id="d2d7d-141">public class AuthenticationTestHandler : DelegatingHandler   {       protected override Task<HttpResponseMessage> SendAsync(       HttpRequestMessage request, CancellationToken cancellationToken)       {           var authorizationHeader = request.Headers.GetValues("Authorization").First();</span></span>
     
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
       <span data-ttu-id="d2d7d-142">}</span><span class="sxs-lookup"><span data-stu-id="d2d7d-142">}</span></span>
     
     > [!NOTE]
     > <span data-ttu-id="d2d7d-143">**Примечание по безопасности**: hello `AuthenticationTestHandler` класс не предоставляет значение true, проверка подлинности.</span><span class="sxs-lookup"><span data-stu-id="d2d7d-143">**Security Note**: hello `AuthenticationTestHandler` class does not provide true authentication.</span></span> <span data-ttu-id="d2d7d-144">Он является обычной проверки подлинности используется только toomimic и не является безопасным.</span><span class="sxs-lookup"><span data-stu-id="d2d7d-144">It is used only toomimic basic authentication and is not secure.</span></span> <span data-ttu-id="d2d7d-145">В реальных приложениях и службах необходимо реализовать безопасный механизм проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="d2d7d-145">You must implement a secure authentication mechanism in your production applications and services.</span></span>                
     > 
     > 
4. <span data-ttu-id="d2d7d-146">Добавьте следующий код в конце hello hello hello `Register` метод в hello **App_Start/WebApiConfig.cs** обработчик сообщений hello tooregister класса:</span><span class="sxs-lookup"><span data-stu-id="d2d7d-146">Add hello following code at hello end of hello `Register` method in hello **App_Start/WebApiConfig.cs** class tooregister hello message handler:</span></span>
   
        config.MessageHandlers.Add(new AuthenticationTestHandler());
5. <span data-ttu-id="d2d7d-147">Сохраните изменения.</span><span class="sxs-lookup"><span data-stu-id="d2d7d-147">Save your changes.</span></span>

## <a name="registering-for-notifications-using-hello-webapi-backend"></a><span data-ttu-id="d2d7d-148">Регистрация для получения уведомлений с помощью hello WebAPI серверной части</span><span class="sxs-lookup"><span data-stu-id="d2d7d-148">Registering for Notifications using hello WebAPI Backend</span></span>
<span data-ttu-id="d2d7d-149">В этом разделе мы будем добавлять новые серверной toohandle WebAPI контроллера toohello запросы tooregister пользователя и устройства для уведомлений с использованием hello клиентская библиотека для концентраторов уведомлений.</span><span class="sxs-lookup"><span data-stu-id="d2d7d-149">In this section, we will add a new controller toohello WebAPI backend toohandle requests tooregister a user and device for notifications using hello client library for notification hubs.</span></span> <span data-ttu-id="d2d7d-150">контроллер Hello добавит тег пользователя для пользователя hello, была выполнена проверка подлинности и присоединены toohello HttpContext по hello `AuthenticationTestHandler`.</span><span class="sxs-lookup"><span data-stu-id="d2d7d-150">hello controller will add a user tag for hello user that was authenticated and attached toohello HttpContext by hello `AuthenticationTestHandler`.</span></span> <span data-ttu-id="d2d7d-151">тег Hello будет иметь формат строки hello, `"username:<actual username>"`.</span><span class="sxs-lookup"><span data-stu-id="d2d7d-151">hello tag will have hello string format, `"username:<actual username>"`.</span></span>

1. <span data-ttu-id="d2d7d-152">В обозревателе решений щелкните правой кнопкой мыши hello **AppBackend** проект и выберите пункт **управление пакетами NuGet**.</span><span class="sxs-lookup"><span data-stu-id="d2d7d-152">In Solution Explorer, right-click hello **AppBackend** project and then click **Manage NuGet Packages**.</span></span>
2. <span data-ttu-id="d2d7d-153">В левой части окна hello, выберите **Online**и выполните поиск **Microsoft.Azure.NotificationHubs** в hello **поиска** поле.</span><span class="sxs-lookup"><span data-stu-id="d2d7d-153">On hello left-hand side, click **Online**, and search for **Microsoft.Azure.NotificationHubs** in hello **Search** box.</span></span>
3. <span data-ttu-id="d2d7d-154">В списке результатов hello, нажмите кнопку **концентраторы уведомлений Microsoft Azure**, а затем нажмите кнопку **установить**.</span><span class="sxs-lookup"><span data-stu-id="d2d7d-154">In hello results list, click **Microsoft Azure Notification Hubs**, and then click **Install**.</span></span> <span data-ttu-id="d2d7d-155">Завершение установки hello, а затем закройте окно диспетчера пакетов NuGet hello.</span><span class="sxs-lookup"><span data-stu-id="d2d7d-155">Complete hello installation, then close hello NuGet package manager window.</span></span>
   
    <span data-ttu-id="d2d7d-156">При этом добавляется ссылка toohello концентраторов уведомлений Azure SDK с помощью hello <a href="http://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/">пакет NuGet концентраторов Microsoft.Azure.Notification</a>.</span><span class="sxs-lookup"><span data-stu-id="d2d7d-156">This adds a reference toohello Azure Notification Hubs SDK using hello <a href="http://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/">Microsoft.Azure.Notification Hubs NuGet package</a>.</span></span>
4. <span data-ttu-id="d2d7d-157">Теперь мы создадим новый файл класса, представляющий подключение hello с уведомлениями toosend использовать концентратор уведомлений.</span><span class="sxs-lookup"><span data-stu-id="d2d7d-157">We will now create a new class file that represents hello connection with notification hub used toosend notifications.</span></span> <span data-ttu-id="d2d7d-158">Hello обозревателе решений щелкните правой кнопкой мыши hello **моделей** папку, нажмите кнопку **добавить**, нажмите кнопку **класса**.</span><span class="sxs-lookup"><span data-stu-id="d2d7d-158">In hello Solution Explorer, right-click hello **Models** folder, click **Add**, then click **Class**.</span></span> <span data-ttu-id="d2d7d-159">Имя нового класса hello **Notifications.cs**, нажмите кнопку **добавить** toogenerate hello класса.</span><span class="sxs-lookup"><span data-stu-id="d2d7d-159">Name hello new class **Notifications.cs**, then click **Add** toogenerate hello class.</span></span> 
   
    ![][B6]
5. <span data-ttu-id="d2d7d-160">В Notifications.cs, добавьте следующее hello `using` в начало файла hello hello инструкцию:</span><span class="sxs-lookup"><span data-stu-id="d2d7d-160">In Notifications.cs, add hello following `using` statement at hello top of hello file:</span></span>
   
        using Microsoft.Azure.NotificationHubs;
6. <span data-ttu-id="d2d7d-161">Замените hello `Notifications` определения следующий hello класса и убедитесь, что tooreplace hello двух местозаполнителей hello строки подключения (с полным доступом) для центра уведомлений hello имя концентратора (найти по адресу [классический портал Azure ](http://manage.windowsazure.com)):</span><span class="sxs-lookup"><span data-stu-id="d2d7d-161">Replace hello `Notifications` class definition with hello following and make sure tooreplace hello two placeholders with hello connection string (with full access) for your notification hub, and hello hub name (available at [Azure Classic Portal](http://manage.windowsazure.com)):</span></span>
   
        public class Notifications
        {
            public static Notifications Instance = new Notifications();
   
            public NotificationHubClient Hub { get; set; }
   
            private Notifications() {
                Hub = NotificationHubClient.CreateClientFromConnectionString("<your hub's DefaultFullSharedAccessSignature>", 
                                                                             "<hub name>");
            }
        }
7. <span data-ttu-id="d2d7d-162">Далее мы создадим новый контроллер с именем **RegisterController**.</span><span class="sxs-lookup"><span data-stu-id="d2d7d-162">Next we will create a new controller named **RegisterController**.</span></span> <span data-ttu-id="d2d7d-163">В обозревателе решений щелкните правой кнопкой мыши hello **контроллеров** папку, нажмите кнопку **добавить**, нажмите кнопку **контроллера**.</span><span class="sxs-lookup"><span data-stu-id="d2d7d-163">In Solution Explorer, right-click hello **Controllers** folder, then click **Add**, then click **Controller**.</span></span> <span data-ttu-id="d2d7d-164">Нажмите кнопку hello **контроллер 2 API веб - пустой** , а затем щелкните **добавить**.</span><span class="sxs-lookup"><span data-stu-id="d2d7d-164">Click hello **Web API 2 Controller -- Empty** item, and then click **Add**.</span></span> <span data-ttu-id="d2d7d-165">Имя нового класса hello **RegisterController**, а затем нажмите кнопку **добавить** снова toogenerate hello контроллера.</span><span class="sxs-lookup"><span data-stu-id="d2d7d-165">Name hello new class **RegisterController**, and then click **Add** again toogenerate hello controller.</span></span>
   
    ![][B7]
   
    ![][B8]
8. <span data-ttu-id="d2d7d-166">В RegisterController.cs, добавьте следующее hello `using` инструкции:</span><span class="sxs-lookup"><span data-stu-id="d2d7d-166">In RegisterController.cs, add hello following `using` statements:</span></span>
   
        using Microsoft.Azure.NotificationHubs;
        using Microsoft.Azure.NotificationHubs.Messaging;
        using AppBackend.Models;
        using System.Threading.Tasks;
        using System.Web;
9. <span data-ttu-id="d2d7d-167">Добавьте следующий код внутри hello hello `RegisterController` определения класса.</span><span class="sxs-lookup"><span data-stu-id="d2d7d-167">Add hello following code inside hello `RegisterController` class definition.</span></span> <span data-ttu-id="d2d7d-168">Обратите внимание, что в этом коде мы добавить тег пользователя для пользователя hello, это присоединен toohello HttpContext.</span><span class="sxs-lookup"><span data-stu-id="d2d7d-168">Note that in this code, we add a user tag for hello user this is attached toohello HttpContext.</span></span> <span data-ttu-id="d2d7d-169">Hello пользователя была выполнена проверка подлинности и присоединенного toohello HttpContext фильтром сообщения hello, мы добавили `AuthenticationTestHandler`.</span><span class="sxs-lookup"><span data-stu-id="d2d7d-169">hello user was authenticated and attached toohello HttpContext by hello message filter we added, `AuthenticationTestHandler`.</span></span> <span data-ttu-id="d2d7d-170">Можно также добавить tooverify дополнительных проверок, hello пользователя имеет права tooregister для hello запрошенный тегов.</span><span class="sxs-lookup"><span data-stu-id="d2d7d-170">You can also add optional checks tooverify that hello user has rights tooregister for hello requested tags.</span></span>
   
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
10. <span data-ttu-id="d2d7d-171">Сохраните изменения.</span><span class="sxs-lookup"><span data-stu-id="d2d7d-171">Save your changes.</span></span>

## <a name="sending-notifications-from-hello-webapi-backend"></a><span data-ttu-id="d2d7d-172">Отправка уведомлений из hello WebAPI серверной части</span><span class="sxs-lookup"><span data-stu-id="d2d7d-172">Sending Notifications from hello WebAPI Backend</span></span>
<span data-ttu-id="d2d7d-173">В этом разделе добавьте новый контроллера, который предоставляет способ для клиентских устройств toosend уведомление на теге hello имя пользователя, с помощью библиотеки управления службы концентраторов уведомлений Azure в серверной части ASP.NET WebAPI hello.</span><span class="sxs-lookup"><span data-stu-id="d2d7d-173">In this section you add a new controller that exposes a way for client devices toosend a notification based on hello username tag using Azure Notification Hubs Service Management Library in hello ASP.NET WebAPI backend.</span></span>

1. <span data-ttu-id="d2d7d-174">Создайте еще один новый контроллер с именем **NotificationsController**.</span><span class="sxs-lookup"><span data-stu-id="d2d7d-174">Create another new controller named **NotificationsController**.</span></span> <span data-ttu-id="d2d7d-175">Создайте его hello так же, как вы создали hello **RegisterController** в предыдущем разделе hello.</span><span class="sxs-lookup"><span data-stu-id="d2d7d-175">Create it hello same way you created hello **RegisterController** in hello previous section.</span></span>
2. <span data-ttu-id="d2d7d-176">В NotificationsController.cs, добавьте следующее hello `using` инструкции:</span><span class="sxs-lookup"><span data-stu-id="d2d7d-176">In NotificationsController.cs, add hello following `using` statements:</span></span>
   
        using AppBackend.Models;
        using System.Threading.Tasks;
        using System.Web;
3. <span data-ttu-id="d2d7d-177">Добавьте следующий метод toohello hello **NotificationsController** класса.</span><span class="sxs-lookup"><span data-stu-id="d2d7d-177">Add hello following method toohello **NotificationsController** class.</span></span>
   
    <span data-ttu-id="d2d7d-178">Этот код отправки уведомлений тип, основанный на hello службы уведомлений платформы (PNS) `pns` параметра.</span><span class="sxs-lookup"><span data-stu-id="d2d7d-178">This code send a notification type based on hello Platform Notification Service (PNS) `pns` parameter.</span></span> <span data-ttu-id="d2d7d-179">Здравствуйте, значение `to_tag` — hello используется tooset *username* тега приветственное сообщение.</span><span class="sxs-lookup"><span data-stu-id="d2d7d-179">hello value of `to_tag` is used tooset hello *username* tag on hello message.</span></span> <span data-ttu-id="d2d7d-180">Этот тег должен соответствовать тегу имени пользователя активной регистрации центра уведомлений.</span><span class="sxs-lookup"><span data-stu-id="d2d7d-180">This tag must match a username tag of an active notification hub registration.</span></span> <span data-ttu-id="d2d7d-181">сообщение уведомления Hello извлечено из hello тексте запроса POST hello и формат для целевого объекта hello PNS.</span><span class="sxs-lookup"><span data-stu-id="d2d7d-181">hello notification message is pulled from hello body of hello POST request and formatted for hello target PNS.</span></span> 
   
    <span data-ttu-id="d2d7d-182">В зависимости от hello платформы уведомления службы (PNS), поддерживаемых устройств использовать уведомления tooreceive различных уведомлений поддерживаются различные форматы.</span><span class="sxs-lookup"><span data-stu-id="d2d7d-182">Depending on hello Platform Notification Service (PNS) that your supported devices use tooreceive notifications, different notifications are supported using different formats.</span></span> <span data-ttu-id="d2d7d-183">Например, на устройствах Windows можно использовать [всплывающие уведомления с помощью WNS](https://msdn.microsoft.com/library/windows/apps/br230849.aspx), которые не поддерживаются другой PNS.</span><span class="sxs-lookup"><span data-stu-id="d2d7d-183">For example on Windows devices, you could use a [toast notification with WNS](https://msdn.microsoft.com/library/windows/apps/br230849.aspx) that isn't directly supported by another PNS.</span></span> <span data-ttu-id="d2d7d-184">Поэтому серверной части понадобится tooformat hello уведомления в поддерживаемых уведомление для hello PNS устройств при планировании toosupport.</span><span class="sxs-lookup"><span data-stu-id="d2d7d-184">So your backend would need tooformat hello notification into a supported notification for hello PNS of devices you plan toosupport.</span></span> <span data-ttu-id="d2d7d-185">Затем с помощью API hello соответствующие отправки на hello [NotificationHubClient-класс](https://msdn.microsoft.com/library/azure/microsoft.azure.notificationhubs.notificationhubclient_methods.aspx)</span><span class="sxs-lookup"><span data-stu-id="d2d7d-185">Then use hello appropriate send API on hello [NotificationHubClient class](https://msdn.microsoft.com/library/azure/microsoft.azure.notificationhubs.notificationhubclient_methods.aspx)</span></span>
   
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
4. <span data-ttu-id="d2d7d-186">Нажмите клавишу **F5** toorun hello и tooensure приложения hello точности своей работы к текущему моменту.</span><span class="sxs-lookup"><span data-stu-id="d2d7d-186">Press **F5** toorun hello application and tooensure hello accuracy of your work so far.</span></span> <span data-ttu-id="d2d7d-187">приложение Hello должен запустить веб-браузер и отобразить hello ASP.NET домашней страницы.</span><span class="sxs-lookup"><span data-stu-id="d2d7d-187">hello app should launch a web browser and display hello ASP.NET home page.</span></span> 

## <a name="publish-hello-new-webapi-backend"></a><span data-ttu-id="d2d7d-188">Публикация hello новую серверную часть WebAPI</span><span class="sxs-lookup"><span data-stu-id="d2d7d-188">Publish hello new WebAPI Backend</span></span>
1. <span data-ttu-id="d2d7d-189">Теперь мы Развернем tooan этого приложения веб-сайта Azure, в порядке toomake доступ из всех устройств.</span><span class="sxs-lookup"><span data-stu-id="d2d7d-189">Now we will deploy this app tooan Azure Website in order toomake it accessible from all devices.</span></span> <span data-ttu-id="d2d7d-190">Щелкните правой кнопкой мыши на hello **AppBackend** проект и выберите **публикации**.</span><span class="sxs-lookup"><span data-stu-id="d2d7d-190">Right-click on hello **AppBackend** project and select **Publish**.</span></span>
2. <span data-ttu-id="d2d7d-191">Выберите **службу приложений Microsoft Azure** в качестве цели публикации и щелкните **Опубликовать**.</span><span class="sxs-lookup"><span data-stu-id="d2d7d-191">Select **Microsoft Azure App Service** as your publish target and click **Publish**.</span></span> <span data-ttu-id="d2d7d-192">Откроется диалоговое окно hello Создание приложения службы, который поможет создать все hello необходимые ресурсы Azure toorun hello, ASP.NET веб-приложения в Azure.</span><span class="sxs-lookup"><span data-stu-id="d2d7d-192">This opens hello Create App Service dialog, which helps you create all hello necessary Azure resources toorun hello ASP.NET web app in Azure.</span></span>

    ![][B15]
3. <span data-ttu-id="d2d7d-193">В hello **Создание приложения службы** диалоговое окно, выберите учетную запись Azure.</span><span class="sxs-lookup"><span data-stu-id="d2d7d-193">In hello **Create App Service** dialog, select your Azure account.</span></span> <span data-ttu-id="d2d7d-194">Щелкните **Изменить тип** и выберите **Веб-приложение**.</span><span class="sxs-lookup"><span data-stu-id="d2d7d-194">Click **Change Type** and select **Web App**.</span></span> <span data-ttu-id="d2d7d-195">Сохранить hello **имя веб-приложения** заданную и выберите hello **подписки**, **группы ресурсов**, и **план служб приложений**.</span><span class="sxs-lookup"><span data-stu-id="d2d7d-195">Keep hello **Web App Name** given and select hello **Subscription**, **Resource Group**, and **App Service Plan**.</span></span>  <span data-ttu-id="d2d7d-196">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="d2d7d-196">Click **Create**.</span></span>

4. <span data-ttu-id="d2d7d-197">Запишите hello **URL-адрес сайта** свойство в hello **Сводка** раздела.</span><span class="sxs-lookup"><span data-stu-id="d2d7d-197">Make a note of hello **Site URL** property in hello **Summary** section.</span></span> <span data-ttu-id="d2d7d-198">Мы будем называть toothis URL-адрес, как ваш *конечную точку серверной части* далее в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="d2d7d-198">We will refer toothis URL as your *backend endpoint* later in this tutorial.</span></span> <span data-ttu-id="d2d7d-199">Щелкните **Опубликовать**.</span><span class="sxs-lookup"><span data-stu-id="d2d7d-199">Click **Publish**.</span></span>

5. <span data-ttu-id="d2d7d-200">После завершения работы мастера hello, он публикует hello ASP.NET web app tooAzure и затем запускает hello приложение в браузере по умолчанию hello.</span><span class="sxs-lookup"><span data-stu-id="d2d7d-200">Once hello wizard completes, it publishes hello ASP.NET web app tooAzure, and then launches hello app in hello default browser.</span></span>  <span data-ttu-id="d2d7d-201">Приложение можно будет просмотреть в службах приложений Azure.</span><span class="sxs-lookup"><span data-stu-id="d2d7d-201">Your application will be viewable in Azure App Services.</span></span>

<span data-ttu-id="d2d7d-202">URL-адрес Hello использует имя веб-приложения hello, указанный ранее, с http://<app_name>.azurewebsites.net формат hello.</span><span class="sxs-lookup"><span data-stu-id="d2d7d-202">hello URL uses hello web app name that you specified earlier, with hello format http://<app_name>.azurewebsites.net.</span></span>

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
