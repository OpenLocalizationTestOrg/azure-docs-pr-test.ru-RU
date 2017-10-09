
1. <span data-ttu-id="fb623-101">В файле проекта MainPage.xaml.cs hello, добавьте следующее hello **с помощью** инструкции:</span><span class="sxs-lookup"><span data-stu-id="fb623-101">In hello MainPage.xaml.cs project file, add hello following **using** statements:</span></span>
   
        using System.Linq;        
        using Windows.Security.Credentials;
2. <span data-ttu-id="fb623-102">Замените hello **AuthenticateAsync** метод с hello, следующий код:</span><span class="sxs-lookup"><span data-stu-id="fb623-102">Replace hello **AuthenticateAsync** method with hello following code:</span></span>
   
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
   
    <span data-ttu-id="fb623-103">В этой версии **AuthenticateAsync**, приложение hello пытается toouse учетные данные, хранящиеся в hello **PasswordVault** tooaccess hello службы.</span><span class="sxs-lookup"><span data-stu-id="fb623-103">In this version of **AuthenticateAsync**, hello app tries toouse credentials stored in hello **PasswordVault** tooaccess hello service.</span></span> <span data-ttu-id="fb623-104">Обычная попытка входа предпринимается и при отсутствии хранимых учетных данных.</span><span class="sxs-lookup"><span data-stu-id="fb623-104">A regular sign-in is also performed when there is no stored credential.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="fb623-105">Возможно, истек срок действия кэшированного маркера и срока действия маркера может также возникнуть после проверки подлинности при использовании приложение hello.</span><span class="sxs-lookup"><span data-stu-id="fb623-105">A cached token may be expired, and token expiration can also occur after authentication when hello app is in use.</span></span> <span data-ttu-id="fb623-106">toodetermine если истек срок действия маркера. в статье toolearn [проверки маркеры с истекшим сроком действия проверки подлинности](http://aka.ms/jww5vp).</span><span class="sxs-lookup"><span data-stu-id="fb623-106">toolearn how toodetermine if a token is expired, see [Check for expired authentication tokens](http://aka.ms/jww5vp).</span></span> <span data-ttu-id="fb623-107">Ошибки авторизации toohandling решения токены связанные tooexpiring. в разделе блога hello [кэширование и умение работать с истекшим сроком действия токенов в мобильных службах Azure управляемого пакета SDK](http://blogs.msdn.com/b/carlosfigueira/archive/2014/03/13/caching-and-handling-expired-tokens-in-azure-mobile-services-managed-sdk.aspx).</span><span class="sxs-lookup"><span data-stu-id="fb623-107">For a solution toohandling authorization errors related tooexpiring tokens, see hello post [Caching and handling expired tokens in Azure Mobile Services managed SDK](http://blogs.msdn.com/b/carlosfigueira/archive/2014/03/13/caching-and-handling-expired-tokens-in-azure-mobile-services-managed-sdk.aspx).</span></span> 
   > 
   > 
3. <span data-ttu-id="fb623-108">Перезапустите приложение hello дважды.</span><span class="sxs-lookup"><span data-stu-id="fb623-108">Restart hello app twice.</span></span>
   
    <span data-ttu-id="fb623-109">Обратите внимание, что при первом запуске hello, вход с помощью поставщика hello снова не требуется.</span><span class="sxs-lookup"><span data-stu-id="fb623-109">Notice that on hello first start-up, sign-in with hello provider is again required.</span></span> <span data-ttu-id="fb623-110">Тем не менее на второй перезагрузки hello hello в кэше и используют учетные данные входа пропускается.</span><span class="sxs-lookup"><span data-stu-id="fb623-110">However, on hello second restart hello cached credentials are used and sign-in is bypassed.</span></span> 

