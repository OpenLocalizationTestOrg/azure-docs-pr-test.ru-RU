
<span data-ttu-id="80035-101">Следующий Hello предыдущем примере кода показан стандартный вход, требующий toocontact клиента hello обоих hello удостоверение поставщика и hello внутренней службы Azure каждый раз при запуске приложение hello.</span><span class="sxs-lookup"><span data-stu-id="80035-101">hello previous example showed a standard sign-in, which requires hello client toocontact both hello identity provider and hello back-end Azure service every time hello app starts.</span></span> <span data-ttu-id="80035-102">Этот способ неэффективен и может иметь проблемы, связанные с использования, если многие клиенты пытаются выполнить toostart приложения одновременно.</span><span class="sxs-lookup"><span data-stu-id="80035-102">This method is inefficient, and you can have usage-related issues if many customers try toostart your app simultaneously.</span></span> <span data-ttu-id="80035-103">Лучшим подходом является toocache hello авторизации токен, возвращенный hello службы Azure и попробуйте toouse это перед использованием сначала вход на основе поставщика.</span><span class="sxs-lookup"><span data-stu-id="80035-103">A better approach is toocache hello authorization token returned by hello Azure service, and try toouse this first before using a provider-based sign-in.</span></span>

> [!NOTE]
> <span data-ttu-id="80035-104">Можно кэшировать hello маркера, выданного hello внутренней службы Azure независимо от того, используется ли-управляемый клиент или служба проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="80035-104">You can cache hello token issued by hello back-end Azure service regardless of whether you are using client-managed or service-managed authentication.</span></span> <span data-ttu-id="80035-105">Этот учебник использует управляемую сервером проверку подлинности.</span><span class="sxs-lookup"><span data-stu-id="80035-105">This tutorial uses service-managed authentication.</span></span>
>
>

1. <span data-ttu-id="80035-106">Откройте файл ToDoActivity.java hello и добавьте следующие инструкции импорта hello:</span><span class="sxs-lookup"><span data-stu-id="80035-106">Open hello ToDoActivity.java file and add hello following import statements:</span></span>

        import android.content.Context;
        import android.content.SharedPreferences;
        import android.content.SharedPreferences.Editor;
2. <span data-ttu-id="80035-107">Добавьте следующие элементы toohello hello `ToDoActivity` класса.</span><span class="sxs-lookup"><span data-stu-id="80035-107">Add hello following members toohello `ToDoActivity` class.</span></span>

        public static final String SHAREDPREFFILE = "temp";    
        public static final String USERIDPREF = "uid";    
        public static final String TOKENPREF = "tkn";    
3. <span data-ttu-id="80035-108">Добавьте в файл ToDoActivity.java hello, после определения для hello hello `cacheUserToken` метод.</span><span class="sxs-lookup"><span data-stu-id="80035-108">In hello ToDoActivity.java file, add hello following definition for hello `cacheUserToken` method.</span></span>

        private void cacheUserToken(MobileServiceUser user)
        {
            SharedPreferences prefs = getSharedPreferences(SHAREDPREFFILE, Context.MODE_PRIVATE);
            Editor editor = prefs.edit();
            editor.putString(USERIDPREF, user.getUserId());
            editor.putString(TOKENPREF, user.getAuthenticationToken());
            editor.commit();
        }    

    <span data-ttu-id="80035-109">Этот метод сохраняет hello идентификатор пользователя и маркер в файле предпочтений, помеченного как закрытый.</span><span class="sxs-lookup"><span data-stu-id="80035-109">This method stores hello user ID and token in a preference file that is marked private.</span></span> <span data-ttu-id="80035-110">Таким образом, что другие приложения на устройстве hello не toohello маркер доступа, нужно защитить доступ toohello кэша.</span><span class="sxs-lookup"><span data-stu-id="80035-110">This should protect access toohello cache so that other apps on hello device do not have access toohello token.</span></span> <span data-ttu-id="80035-111">предпочтения Hello изолированного приложения hello.</span><span class="sxs-lookup"><span data-stu-id="80035-111">hello preference is sandboxed for hello app.</span></span> <span data-ttu-id="80035-112">Тем не менее если кто-нибудь получит доступ toohello устройство, возможно, что они могут получить кэш токена доступа toohello другими способами.</span><span class="sxs-lookup"><span data-stu-id="80035-112">However, if someone gains access toohello device, it is possible that they may gain access toohello token cache through other means.</span></span>

   > [!NOTE]
   > <span data-ttu-id="80035-113">Можно также защитить hello маркер с шифрованием, если маркер доступа tooyour данные считаются конфиденциальными и кто-то может получить доступ toohello устройства.</span><span class="sxs-lookup"><span data-stu-id="80035-113">You can further protect hello token with encryption, if token access tooyour data is considered highly sensitive and someone may gain access toohello device.</span></span> <span data-ttu-id="80035-114">Полностью безопасного решения выходит за рамки hello данного учебника но зависит от требований к безопасности.</span><span class="sxs-lookup"><span data-stu-id="80035-114">A completely secure solution is beyond hello scope of this tutorial, however, and depends on your security requirements.</span></span>
   >
   >
4. <span data-ttu-id="80035-115">Добавьте в файл ToDoActivity.java hello, после определения для hello hello `loadUserTokenCache` метод.</span><span class="sxs-lookup"><span data-stu-id="80035-115">In hello ToDoActivity.java file, add hello following definition for hello `loadUserTokenCache` method.</span></span>

        private boolean loadUserTokenCache(MobileServiceClient client)
        {
            SharedPreferences prefs = getSharedPreferences(SHAREDPREFFILE, Context.MODE_PRIVATE);
            String userId = prefs.getString(USERIDPREF, null);
            if (userId == null)
                return false;
            String token = prefs.getString(TOKENPREF, null);
            if (token == null)
                return false;

            MobileServiceUser user = new MobileServiceUser(userId);
            user.setAuthenticationToken(token);
            client.setCurrentUser(user);

            return true;
        }
5. <span data-ttu-id="80035-116">В hello *ToDoActivity.java* файла, замените hello `authenticate` метод с hello следующий метод, который использует кэш маркера.</span><span class="sxs-lookup"><span data-stu-id="80035-116">In hello *ToDoActivity.java* file, replace hello `authenticate` method with hello following method, which uses a token cache.</span></span> <span data-ttu-id="80035-117">Изменить поставщика входа hello toouse, отличную от Google.</span><span class="sxs-lookup"><span data-stu-id="80035-117">Change hello login provider if you want toouse an account other than Google.</span></span>

        private void authenticate() {
            // We first try tooload a token cache if one exists.
            if (loadUserTokenCache(mClient))
            {
                createTable();
            }
            // If we failed tooload a token cache, login and create a token cache
            else
            {
                // Login using hello Google provider.    
                ListenableFuture<MobileServiceUser> mLogin = mClient.login(MobileServiceAuthenticationProvider.Google);

                Futures.addCallback(mLogin, new FutureCallback<MobileServiceUser>() {
                    @Override
                    public void onFailure(Throwable exc) {
                        createAndShowDialog("You must log in. Login Required", "Error");
                    }           
                    @Override
                    public void onSuccess(MobileServiceUser user) {
                        createAndShowDialog(String.format(
                                "You are now logged in - %1$2s",
                                user.getUserId()), "Success");
                        cacheUserToken(mClient.getCurrentUser());
                        createTable();    
                    }
                });
            }
        }
6. <span data-ttu-id="80035-118">Построение hello приложения и тестов проверки подлинности с помощью действительной учетной записи.</span><span class="sxs-lookup"><span data-stu-id="80035-118">Build hello app and test authentication using a valid account.</span></span> <span data-ttu-id="80035-119">Запустите его как минимум дважды.</span><span class="sxs-lookup"><span data-stu-id="80035-119">Run it at least twice.</span></span> <span data-ttu-id="80035-120">Во время первого запуска hello следует получать приглашения toosign в и создать кэш токена hello.</span><span class="sxs-lookup"><span data-stu-id="80035-120">During hello first run, you should receive a prompt toosign in and create hello token cache.</span></span> <span data-ttu-id="80035-121">После этого каждый запуск попыток tooload hello кэш токена для проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="80035-121">After that, each run attempts tooload hello token cache for authentication.</span></span> <span data-ttu-id="80035-122">Не должно быть обязательным toosign в.</span><span class="sxs-lookup"><span data-stu-id="80035-122">You should not be required toosign in.</span></span>
