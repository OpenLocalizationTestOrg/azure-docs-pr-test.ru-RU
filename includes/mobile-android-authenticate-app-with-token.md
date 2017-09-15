
<span data-ttu-id="ee408-101">В предыдущем примере показан стандартный вход, который требует, чтобы клиент подключался как к поставщику удостоверений, так и к серверной службе Azure каждый раз, когда приложение запускается.</span><span class="sxs-lookup"><span data-stu-id="ee408-101">The previous example showed a standard sign-in, which requires the client to contact both the identity provider and the back-end Azure service every time the app starts.</span></span> <span data-ttu-id="ee408-102">Этот метод неэффективен, и вы можете столкнуться с проблемами, связанными с использованием приложения, если большое количество клиентов попытаются запустить приложение одновременно.</span><span class="sxs-lookup"><span data-stu-id="ee408-102">This method is inefficient, and you can have usage-related issues if many customers try to start your app simultaneously.</span></span> <span data-ttu-id="ee408-103">Лучше кэшировать маркер авторизации, который возвратила служба Azure, причем делать это до входа через поставщика.</span><span class="sxs-lookup"><span data-stu-id="ee408-103">A better approach is to cache the authorization token returned by the Azure service, and try to use this first before using a provider-based sign-in.</span></span>

> [!NOTE]
> <span data-ttu-id="ee408-104">Можно кэшировать маркер, выданный серверной службой Azure, независимо от того, какую аутентификацию вы используете: управляемую клиентом или сервером.</span><span class="sxs-lookup"><span data-stu-id="ee408-104">You can cache the token issued by the back-end Azure service regardless of whether you are using client-managed or service-managed authentication.</span></span> <span data-ttu-id="ee408-105">Этот учебник использует управляемую сервером проверку подлинности.</span><span class="sxs-lookup"><span data-stu-id="ee408-105">This tutorial uses service-managed authentication.</span></span>
>
>

1. <span data-ttu-id="ee408-106">Откройте файл ToDoActivity.java и добавьте следующую инструкцию import:</span><span class="sxs-lookup"><span data-stu-id="ee408-106">Open the ToDoActivity.java file and add the following import statements:</span></span>

        import android.content.Context;
        import android.content.SharedPreferences;
        import android.content.SharedPreferences.Editor;
2. <span data-ttu-id="ee408-107">Добавьте в класс `ToDoActivity` следующие методы.</span><span class="sxs-lookup"><span data-stu-id="ee408-107">Add the following members to the `ToDoActivity` class.</span></span>

        public static final String SHAREDPREFFILE = "temp";    
        public static final String USERIDPREF = "uid";    
        public static final String TOKENPREF = "tkn";    
3. <span data-ttu-id="ee408-108">В файле ToDoActivity.java добавьте следующее определение для метода `cacheUserToken`.</span><span class="sxs-lookup"><span data-stu-id="ee408-108">In the ToDoActivity.java file, add the following definition for the `cacheUserToken` method.</span></span>

        private void cacheUserToken(MobileServiceUser user)
        {
            SharedPreferences prefs = getSharedPreferences(SHAREDPREFFILE, Context.MODE_PRIVATE);
            Editor editor = prefs.edit();
            editor.putString(USERIDPREF, user.getUserId());
            editor.putString(TOKENPREF, user.getAuthenticationToken());
            editor.commit();
        }    

    <span data-ttu-id="ee408-109">Этот метод хранит идентификатор пользователя и маркер в закрытом файле настроек.</span><span class="sxs-lookup"><span data-stu-id="ee408-109">This method stores the user ID and token in a preference file that is marked private.</span></span> <span data-ttu-id="ee408-110">Это должно защитить доступ к кэш-памяти, так что другие приложения на устройстве не будут иметь доступа к маркеру,</span><span class="sxs-lookup"><span data-stu-id="ee408-110">This should protect access to the cache so that other apps on the device do not have access to the token.</span></span> <span data-ttu-id="ee408-111">потому что настройки хранятся в изолированной среде приложения.</span><span class="sxs-lookup"><span data-stu-id="ee408-111">The preference is sandboxed for the app.</span></span> <span data-ttu-id="ee408-112">Тем не менее если кто-либо получает доступ к устройству, не исключено, что он сможет получить доступ к кэш-памяти маркера с помощью других средств.</span><span class="sxs-lookup"><span data-stu-id="ee408-112">However, if someone gains access to the device, it is possible that they may gain access to the token cache through other means.</span></span>

   > [!NOTE]
   > <span data-ttu-id="ee408-113">Вы можете дополнительно защитить маркер шифрованием, если маркер доступа к вашим данным имеет высокую степень конфиденциальности и третье лицо сможет получить доступ к устройству.</span><span class="sxs-lookup"><span data-stu-id="ee408-113">You can further protect the token with encryption, if token access to your data is considered highly sensitive and someone may gain access to the device.</span></span> <span data-ttu-id="ee408-114">Тем не менее полностью безопасное решение выходит за рамки данного руководства и зависит от ваших требований безопасности.</span><span class="sxs-lookup"><span data-stu-id="ee408-114">A completely secure solution is beyond the scope of this tutorial, however, and depends on your security requirements.</span></span>
   >
   >
4. <span data-ttu-id="ee408-115">В файле ToDoActivity.java добавьте следующее определение для метода `loadUserTokenCache`.</span><span class="sxs-lookup"><span data-stu-id="ee408-115">In the ToDoActivity.java file, add the following definition for the `loadUserTokenCache` method.</span></span>

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
5. <span data-ttu-id="ee408-116">В файле *ToDoActivity.java* замените метод `authenticate` следующим методом, который использует кэш маркеров.</span><span class="sxs-lookup"><span data-stu-id="ee408-116">In the *ToDoActivity.java* file, replace the `authenticate` method with the following method, which uses a token cache.</span></span> <span data-ttu-id="ee408-117">Измените поставщика входа, если вы хотите использовать учетную запись, отличную от учетной записи Google.</span><span class="sxs-lookup"><span data-stu-id="ee408-117">Change the login provider if you want to use an account other than Google.</span></span>

        private void authenticate() {
            // We first try to load a token cache if one exists.
            if (loadUserTokenCache(mClient))
            {
                createTable();
            }
            // If we failed to load a token cache, login and create a token cache
            else
            {
                // Login using the Google provider.    
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
6. <span data-ttu-id="ee408-118">Соберите приложение и проверьте проверку подлинности, используя действующую учетную запись.</span><span class="sxs-lookup"><span data-stu-id="ee408-118">Build the app and test authentication using a valid account.</span></span> <span data-ttu-id="ee408-119">Запустите его как минимум дважды.</span><span class="sxs-lookup"><span data-stu-id="ee408-119">Run it at least twice.</span></span> <span data-ttu-id="ee408-120">Во время первого запуска вы должны получить приглашение для входа и создать кэш маркера.</span><span class="sxs-lookup"><span data-stu-id="ee408-120">During the first run, you should receive a prompt to sign in and create the token cache.</span></span> <span data-ttu-id="ee408-121">После этого при каждом запуске предпринимается попытка загрузки кэша маркера для проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="ee408-121">After that, each run attempts to load the token cache for authentication.</span></span> <span data-ttu-id="ee408-122">Приглашение для входа в систему не будет появляться.</span><span class="sxs-lookup"><span data-stu-id="ee408-122">You should not be required to sign in.</span></span>
