
1. В файле проекта MainPage.xaml.cs hello, добавьте следующее hello **с помощью** инструкции:
   
        using System.Linq;        
        using Windows.Security.Credentials;
2. Замените hello **AuthenticateAsync** метод с hello, следующий код:
   
        private async System.Threading.Tasks.Task<bool> AuthenticateAsync()
        {
            string message;
            bool success = false;
   
            // This sample uses hello Facebook provider.
            var provider = MobileServiceAuthenticationProvider.Facebook;
   
            // Use hello PasswordVault toosecurely store and access credentials.
            PasswordVault vault = new PasswordVault();
            PasswordCredential credential = null;
   
            try
            {
                // Try tooget an existing credential from hello vault.
                credential = vault.FindAllByResource(provider.ToString()).FirstOrDefault();
            }
            catch (Exception)
            {
                // When there is no matching resource an error occurs, which we ignore.
            }
   
            if (credential != null)
            {
                // Create a user from hello stored credentials.
                user = new MobileServiceUser(credential.UserName);
                credential.RetrievePassword();
                user.MobileServiceAuthenticationToken = credential.Password;
   
                // Set hello user from hello stored credentials.
                App.MobileService.CurrentUser = user;
   
                // Consider adding a check toodetermine if hello token is 
                // expired, as shown in this post: http://aka.ms/jww5vp.
   
                success = true;
                message = string.Format("Cached credentials for user - {0}", user.UserId);
            }
            else
            {
                try
                {
                    // Login with hello identity provider.
                    user = await App.MobileService
                        .LoginAsync(provider);
   
                    // Create and store hello user credentials.
                    credential = new PasswordCredential(provider.ToString(),
                        user.UserId, user.MobileServiceAuthenticationToken);
                    vault.Add(credential);
   
                    success = true;
                    message = string.Format("You are now logged in - {0}", user.UserId);
                }
                catch (MobileServiceInvalidOperationException)
                {
                    message = "You must log in. Login Required";
                }
            }
   
            var dialog = new MessageDialog(message);
            dialog.Commands.Add(new UICommand("OK"));
            await dialog.ShowAsync();
   
            return success;
        }
   
    В этой версии **AuthenticateAsync**, приложение hello пытается toouse учетные данные, хранящиеся в hello **PasswordVault** tooaccess hello службы. Обычная попытка входа предпринимается и при отсутствии хранимых учетных данных.
   
   > [!NOTE]
   > Возможно, истек срок действия кэшированного маркера и срока действия маркера может также возникнуть после проверки подлинности при использовании приложение hello. toodetermine если истек срок действия маркера. в статье toolearn [проверки маркеры с истекшим сроком действия проверки подлинности](http://aka.ms/jww5vp). Ошибки авторизации toohandling решения токены связанные tooexpiring. в разделе блога hello [кэширование и умение работать с истекшим сроком действия токенов в мобильных службах Azure управляемого пакета SDK](http://blogs.msdn.com/b/carlosfigueira/archive/2014/03/13/caching-and-handling-expired-tokens-in-azure-mobile-services-managed-sdk.aspx). 
   > 
   > 
3. Перезапустите приложение hello дважды.
   
    Обратите внимание, что при первом запуске hello, вход с помощью поставщика hello снова не требуется. Тем не менее на второй перезагрузки hello hello в кэше и используют учетные данные входа пропускается. 

