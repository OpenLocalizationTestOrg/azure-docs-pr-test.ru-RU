## <a name="obtain-an-azure-resource-manager-token"></a>Получение маркера Azure Resource Manager
Azure Active Directory должны пройти проверку подлинности всех hello задач, выполняемых с ресурсами с помощью диспетчера ресурсов Azure hello. Hello приведенном примере пароль проверки подлинности, см. в других подходов [запросы проверки подлинности Azure Resource Manager][lnk-authenticate-arm].

1. Добавьте следующий код toohello hello **Main** метод в Program.cs tooretrieve токена из Azure AD, используя идентификатор приложения hello и пароль.
   
    ```
    var authContext = new AuthenticationContext(string.Format  
      ("https://login.microsoftonline.com/{0}", tenantId));
    var credential = new ClientCredential(applicationId, password);
    AuthenticationResult token = authContext.AcquireTokenAsync
      ("https://management.core.windows.net/", credential).Result;
   
    if (token == null)
    {
      Console.WriteLine("Failed tooobtain hello token");
      return;
    }
    ```
2. Создание **ResourceManagementClient** объекта hello, использует маркер, добавив после окончания toohello кода hello hello **Main** метод:
   
    ```
    var creds = new TokenCredentials(token.AccessToken);
    var client = new ResourceManagementClient(creds);
    client.SubscriptionId = subscriptionId;
    ```
3. Создайте или получите ссылку на группу ресурсов hello, которую вы используете:
   
    ```
    var rgResponse = client.ResourceGroups.CreateOrUpdate(rgName,
        new ResourceGroup("East US"));
    if (rgResponse.Properties.ProvisioningState != "Succeeded")
    {
      Console.WriteLine("Problem creating resource group");
      return;
    }
    ```

[lnk-authenticate-arm]: https://msdn.microsoft.com/library/azure/dn790557.aspx