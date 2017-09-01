
В предыдущем примере показан стандартный вход, который требует, чтобы клиент подключался как к поставщику удостоверений, так и к серверной службе Azure каждый раз, когда приложение запускается. Этот метод неэффективен, и вы можете столкнуться с проблемами, связанными с использованием приложения, если большое количество клиентов попытаются запустить приложение одновременно. Лучше кэшировать маркер авторизации, который возвратила служба Azure, причем делать это до входа через поставщика.

> [!NOTE]
> Можно кэшировать маркер, выданный серверной службой Azure, независимо от того, какую аутентификацию вы используете: управляемую клиентом или сервером. Этот учебник использует управляемую сервером проверку подлинности.
>
>

1. Откройте файл ToDoActivity.java и добавьте следующую инструкцию import:

        import android.content.Context;
        import android.content.SharedPreferences;
        import android.content.SharedPreferences.Editor;
2. Добавьте в класс `ToDoActivity` следующие методы.

        public static final String SHAREDPREFFILE = "temp";    
        public static final String USERIDPREF = "uid";    
        public static final String TOKENPREF = "tkn";    
3. В файле ToDoActivity.java добавьте следующее определение для метода `cacheUserToken`.

        private void cacheUserToken(MobileServiceUser user)
        {
            SharedPreferences prefs = getSharedPreferences(SHAREDPREFFILE, Context.MODE_PRIVATE);
            Editor editor = prefs.edit();
            editor.putString(USERIDPREF, user.getUserId());
            editor.putString(TOKENPREF, user.getAuthenticationToken());
            editor.commit();
        }    

    Этот метод хранит идентификатор пользователя и маркер в закрытом файле настроек. Это должно защитить доступ к кэш-памяти, так что другие приложения на устройстве не будут иметь доступа к маркеру, потому что настройки хранятся в изолированной среде приложения. Тем не менее если кто-либо получает доступ к устройству, не исключено, что он сможет получить доступ к кэш-памяти маркера с помощью других средств.

   > [!NOTE]
   > Вы можете дополнительно защитить маркер шифрованием, если маркер доступа к вашим данным имеет высокую степень конфиденциальности и третье лицо сможет получить доступ к устройству. Тем не менее полностью безопасное решение выходит за рамки данного руководства и зависит от ваших требований безопасности.
   >
   >
4. В файле ToDoActivity.java добавьте следующее определение для метода `loadUserTokenCache`.

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
5. В файле *ToDoActivity.java* замените метод `authenticate` следующим методом, который использует кэш маркеров. Измените поставщика входа, если вы хотите использовать учетную запись, отличную от учетной записи Google.

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
6. Соберите приложение и проверьте проверку подлинности, используя действующую учетную запись. Запустите его как минимум дважды. Во время первого запуска вы должны получить приглашение для входа и создать кэш маркера. После этого при каждом запуске предпринимается попытка загрузки кэша маркера для проверки подлинности. Приглашение для входа в систему не будет появляться.
