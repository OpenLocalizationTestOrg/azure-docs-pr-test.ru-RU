## <a name="obtain-an-azure-resource-manager-token"></a><span data-ttu-id="71ef9-101">Получение маркера Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="71ef9-101">Obtain an Azure Resource Manager token</span></span>
<span data-ttu-id="71ef9-102">Все задачи, выполняемые с ресурсами с помощью диспетчера ресурсов Azure, должны пройти проверку подлинности Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="71ef9-102">Azure Active Directory must authenticate all the tasks that you perform on resources using the Azure Resource Manager.</span></span> <span data-ttu-id="71ef9-103">В примере ниже демонстрируется проверка подлинности с использованием пароля (другие способы см. в [справочнике по Azure REST API][lnk-authenticate-arm]).</span><span class="sxs-lookup"><span data-stu-id="71ef9-103">The example shown here uses password authentication, for other approaches see [Authenticating Azure Resource Manager requests][lnk-authenticate-arm].</span></span>

1. <span data-ttu-id="71ef9-104">Добавьте в метод **Main** в файле Program.cs приведенный ниже код, позволяющий получить из системы Azure AD маркер с помощью идентификатора приложения и пароля.</span><span class="sxs-lookup"><span data-stu-id="71ef9-104">Add the following code to the **Main** method in Program.cs to retrieve a token from Azure AD using the application id and password.</span></span>
   
    ```
    var authContext = new AuthenticationContext(string.Format  
      ("https://login.microsoftonline.com/{0}", tenantId));
    var credential = new ClientCredential(applicationId, password);
    AuthenticationResult token = authContext.AcquireTokenAsync
      ("https://management.core.windows.net/", credential).Result;
   
    if (token == null)
    {
      Console.WriteLine("Failed to obtain the token");
      return;
    }
    ```
2. <span data-ttu-id="71ef9-105">Создайте объект **ResourceManagementClient**, который использует полученный маркер, добавив следующий код в конец метода **Main**:</span><span class="sxs-lookup"><span data-stu-id="71ef9-105">Create a **ResourceManagementClient** object that uses the token by adding the following code to the end of the **Main** method:</span></span>
   
    ```
    var creds = new TokenCredentials(token.AccessToken);
    var client = new ResourceManagementClient(creds);
    client.SubscriptionId = subscriptionId;
    ```
3. <span data-ttu-id="71ef9-106">Создайте группу ресурсов, которую будете использовать, или получите ссылку на нее:</span><span class="sxs-lookup"><span data-stu-id="71ef9-106">Create, or obtain a reference to, the resource group you are using:</span></span>
   
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