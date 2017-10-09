
Следующий Hello предыдущем примере кода показан стандартный вход, требующий toocontact клиента hello обоих hello удостоверение поставщика и hello внутренней службы Azure каждый раз при запуске приложение hello. Этот способ неэффективен и может иметь проблемы, связанные с использования, если многие клиенты пытаются выполнить toostart приложения одновременно. Лучшим подходом является toocache hello авторизации токен, возвращенный hello службы Azure и попробуйте toouse это перед использованием сначала вход на основе поставщика.

> [!NOTE]
> Можно кэшировать hello маркера, выданного hello внутренней службы Azure независимо от того, используется ли-управляемый клиент или служба проверки подлинности. Этот учебник использует управляемую сервером проверку подлинности.
>
>

1. Откройте файл ToDoActivity.java hello и добавьте следующие инструкции импорта hello:

        import android.content.Context;
        import android.content.SharedPreferences;
        import android.content.SharedPreferences.Editor;
2. Добавьте следующие элементы toohello hello `ToDoActivity` класса.

        public static final String SHAREDPREFFILE = "temp";    
        public static final String USERIDPREF = "uid";    
        public static final String TOKENPREF = "tkn";    
3. Добавьте в файл ToDoActivity.java hello, после определения для hello hello `cacheUserToken` метод.

        private void cacheUserToken(MobileServiceUser user)
        {
            SharedPreferences prefs = getSharedPreferences(SHAREDPREFFILE, Context.MODE_PRIVATE);
            Editor editor = prefs.edit();
            editor.putString(USERIDPREF, user.getUserId());
            editor.putString(TOKENPREF, user.getAuthenticationToken());
            editor.commit();
        }    

    Этот метод сохраняет hello идентификатор пользователя и маркер в файле предпочтений, помеченного как закрытый. Таким образом, что другие приложения на устройстве hello не toohello маркер доступа, нужно защитить доступ toohello кэша. предпочтения Hello изолированного приложения hello. Тем не менее если кто-нибудь получит доступ toohello устройство, возможно, что они могут получить кэш токена доступа toohello другими способами.

   > [!NOTE]
   > Можно также защитить hello маркер с шифрованием, если маркер доступа tooyour данные считаются конфиденциальными и кто-то может получить доступ toohello устройства. Полностью безопасного решения выходит за рамки hello данного учебника но зависит от требований к безопасности.
   >
   >
4. Добавьте в файл ToDoActivity.java hello, после определения для hello hello `loadUserTokenCache` метод.

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
5. В hello *ToDoActivity.java* файла, замените hello `authenticate` метод с hello следующий метод, который использует кэш маркера. Изменить поставщика входа hello toouse, отличную от Google.

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
6. Построение hello приложения и тестов проверки подлинности с помощью действительной учетной записи. Запустите его как минимум дважды. Во время первого запуска hello следует получать приглашения toosign в и создать кэш токена hello. После этого каждый запуск попыток tooload hello кэш токена для проверки подлинности. Не должно быть обязательным toosign в.
