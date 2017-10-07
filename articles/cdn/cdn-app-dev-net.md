---
title: "aaaGet работы с hello библиотеку CDN Azure для .NET | Документы Microsoft"
description: "Узнайте, как toomanage приложений .NET toowrite CDN Azure с помощью Visual Studio."
services: cdn
documentationcenter: .net
author: zhangmanling
manager: erikre
editor: 
ms.assetid: 63cf4101-92e7-49dd-a155-a90e54a792ca
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: 9753e48c7469072cef6b2ac728e18c78121c97f7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-cdn-development"></a>Приступая к разработке для Azure CDN
> [!div class="op_single_selector"]
> * [Node.js](cdn-app-dev-node.md)
> * [.NET](cdn-app-dev-net.md)
> 
> 

Можно использовать hello [библиотеку CDN Azure для .NET](https://msdn.microsoft.com/library/mt657769.aspx) tooautomate создания и управления профилями CDN и конечных точек.  Этого учебника вы научитесь hello создания простого консольного приложения .NET, демонстрирующий некоторые из доступных операций hello.  Этот учебник является не предназначен toodescribe все аспекты hello библиотеку CDN Azure для .NET подробно.

Требуется Visual Studio 2015 toocomplete этого учебника.  [Visual Studio Community 2015](https://www.visualstudio.com/products/visual-studio-community-vs.aspx) .

> [!TIP]
> Hello [завершенный проект из этого учебника](https://code.msdn.microsoft.com/Azure-CDN-Management-1f2fba2c) доступен для загрузки на сайте MSDN.
> 
> 

[!INCLUDE [cdn-app-dev-prep](../../includes/cdn-app-dev-prep.md)]

## <a name="create-your-project-and-add-nuget-packages"></a>Создание проекта и добавление пакетов Nuget
Теперь, что мы создали группу ресурсов для наших CDN профилей и заданным нашей профили CDN toomanage разрешений приложения Azure AD и конечных точек в пределах этой группы, можно начать создание нашего приложения.

В Visual Studio 2015 выберите **файл**, **New**, **проекта...**  диалоговое окно нового проекта tooopen hello.  Разверните **Visual C#**, а затем выберите **Windows** hello панели слева hello.  Нажмите кнопку **консольное приложение** hello центральной панели.  Присвойте проекту имя и нажмите кнопку **ОК**.  

![Новый проект](./media/cdn-app-dev-net/cdn-new-project.png)

Наш проект будет toouse некоторые библиотеки Azure, содержащиеся в пакетах Nuget.  Давайте добавим эти toohello проекта.

1. Нажмите кнопку hello **средства** меню **диспетчера пакетов Nuget**, затем **консоль диспетчера пакетов**.
   
    ![Управление пакетами NuGet](./media/cdn-app-dev-net/cdn-manage-nuget.png)
2. В hello консоль диспетчера пакетов выполните hello, следующая команда hello tooinstall **библиотеку проверки подлинности Active Directory (ADAL)**:
   
    `Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory`
3. Выполните следующие tooinstall hello hello **Библиотека управления Azure CDN**:
   
    `Install-Package Microsoft.Azure.Management.Cdn`

## <a name="directives-constants-main-method-and-helper-methods"></a>Директивы, константы, главный метод и вспомогательные методы
Давайте базовая структура нашей программы, написанной hello.

1. Назад на вкладке Program.cs hello, замените hello `using` директивы вверху hello hello следующее:
   
    ```csharp
    using System;
    using System.Collections.Generic;
    using Microsoft.Azure.Management.Cdn;
    using Microsoft.Azure.Management.Cdn.Models;
    using Microsoft.Azure.Management.Resources;
    using Microsoft.Azure.Management.Resources.Models;
    using Microsoft.IdentityModel.Clients.ActiveDirectory;
    using Microsoft.Rest;
    ```
2. Мы должны toodefine некоторые константы, которые будут использовать наши методы.  В hello `Program` класса, но до hello `Main` метод, добавьте следующее hello.  Быть заполнители hello, включая hello убедиться, что tooreplace  **&lt;угловые скобки&gt;**, собственными значениями, при необходимости.
   
    ```csharp
    //Tenant app constants
    private const string clientID = "<YOUR CLIENT ID>";
    private const string clientSecret = "<YOUR CLIENT AUTHENTICATION KEY>"; //Only for service principals
    private const string authority = "https://login.microsoftonline.com/<YOUR TENANT ID>/<YOUR TENANT DOMAIN NAME>";
   
    //Application constants
    private const string subscriptionId = "<YOUR SUBSCRIPTION ID>";
    private const string profileName = "CdnConsoleApp";
    private const string endpointName = "<A UNIQUE NAME FOR YOUR CDN ENDPOINT>";
    private const string resourceGroupName = "CdnConsoleTutorial";
    private const string resourceLocation = "<YOUR PREFERRED AZURE LOCATION, SUCH AS Central US>";
    ```
3. Также на уровне класса hello, определите эти две переменные.  Мы будем использовать эти toodetermine более поздней версии, если конечная точка и профилей уже существует.
   
    ```csharp
    static bool profileAlreadyExists = false;
    static bool endpointAlreadyExists = false;
    ```
4. Замените hello `Main` метод следующим образом:
   
   ```csharp
   static void Main(string[] args)
   {
       //Get a token
       AuthenticationResult authResult = GetAccessToken();
   
       // Create CDN client
       CdnManagementClient cdn = new CdnManagementClient(new TokenCredentials(authResult.AccessToken))
           { SubscriptionId = subscriptionId };
   
       ListProfilesAndEndpoints(cdn);
   
       // Create CDN Profile
       CreateCdnProfile(cdn);
   
       // Create CDN Endpoint
       CreateCdnEndpoint(cdn);
   
       Console.WriteLine();
   
       // Purge CDN Endpoint
       PromptPurgeCdnEndpoint(cdn);
   
       // Delete CDN Endpoint
       PromptDeleteCdnEndpoint(cdn);
   
       // Delete CDN Profile
       PromptDeleteCdnProfile(cdn);
   
       Console.WriteLine("Press Enter tooend program.");
       Console.ReadLine();
   }
   ```
5. Некоторые другие методы будут tooprompt hello пользователя с вопросами «Да/нет».  Добавьте следующий метод toomake hello, немного удобнее:
   
    ```csharp
    private static bool PromptUser(string Question)
    {
        Console.Write(Question + " (Y/N): ");
        var response = Console.ReadKey();
        Console.WriteLine();
        if (response.Key == ConsoleKey.Y)
        {
            return true;
        }
        else if (response.Key == ConsoleKey.N)
        {
            return false;
        }
        else
        {
            // They pressed something other than Y or N.  Let's ask them again.
            return PromptUser(Question);
        }
    }
    ```

Теперь, когда записывается hello базовой структуры программы, следует создавать hello методы, вызываемые hello `Main` метод.

## <a name="authentication"></a>Аутентификация
Чтобы мы могли использовать hello Библиотека управления Azure CDN, нам нужна tooauthenticate наша служба основной и получить маркер проверки подлинности.  Этот метод использует токен ADAL tooretrieve hello.

```csharp
private static AuthenticationResult GetAccessToken()
{
    AuthenticationContext authContext = new AuthenticationContext(authority); 
    ClientCredential credential = new ClientCredential(clientID, clientSecret);
    AuthenticationResult authResult = 
        authContext.AcquireTokenAsync("https://management.core.windows.net/", credential).Result;

    return authResult;
}
```

При использовании проверки подлинности пользователя hello `GetAccessToken` метод будет выглядят немного иначе.

> [!IMPORTANT]
> Этот пример кода следует используйте только при выборе toohave проверки подлинности пользователя вместо участника-службы.
> 
> 

```csharp
private static AuthenticationResult GetAccessToken()
{
    AuthenticationContext authContext = new AuthenticationContext(authority);
    AuthenticationResult authResult = authContext.AcquireTokenAsync("https://management.core.windows.net/",
        clientID, new Uri("http://<redirect URI>"), new PlatformParameters(PromptBehavior.RefreshSession)).Result;

    return authResult;
}
```

Убедиться, что tooreplace быть `<redirect URI>` с hello URI перенаправления, который вы ввели при регистрации приложения hello в Azure AD.

## <a name="list-cdn-profiles-and-endpoints"></a>Вывод списка профилей CDN и конечных точек
Теперь мы готовы tooperform CDN операций.  Hello первое, что делает наш метод — список всех профилей hello и конечных точек в нашей группы ресурсов, а при обнаружении совпадения для hello профиль и конечную точку имена, указанные в нашем константы делает Обратите внимание, для использования в дальнейшем, поэтому мы не пытаемся дубликатов toocreate.

```csharp
private static void ListProfilesAndEndpoints(CdnManagementClient cdn)
{
    // List all hello CDN profiles in this resource group
    var profileList = cdn.Profiles.ListByResourceGroup(resourceGroupName);
    foreach (Profile p in profileList)
    {
        Console.WriteLine("CDN profile {0}", p.Name);
        if (p.Name.Equals(profileName, StringComparison.OrdinalIgnoreCase))
        {
            // Hey, that's hello name of hello CDN profile we want toocreate!
            profileAlreadyExists = true;
        }

        //List all hello CDN endpoints on this CDN profile
        Console.WriteLine("Endpoints:");
        var endpointList = cdn.Endpoints.ListByProfile(p.Name, resourceGroupName);
        foreach (Endpoint e in endpointList)
        {
            Console.WriteLine("-{0} ({1})", e.Name, e.HostName);
            if (e.Name.Equals(endpointName, StringComparison.OrdinalIgnoreCase))
            {
                // hello unique endpoint name already exists.
                endpointAlreadyExists = true;
            }
        }
        Console.WriteLine();
    }
}
```

## <a name="create-cdn-profiles-and-endpoints"></a>Создание профилей CDN и конечных точек
Далее мы создадим профиль.

```csharp
private static void CreateCdnProfile(CdnManagementClient cdn)
{
    if (profileAlreadyExists)
    {
        Console.WriteLine("Profile {0} already exists.", profileName);
    }
    else
    {
        Console.WriteLine("Creating profile {0}.", profileName);
        ProfileCreateParameters profileParms =
            new ProfileCreateParameters() { Location = resourceLocation, Sku = new Sku(SkuName.StandardVerizon) };
        cdn.Profiles.Create(profileName, profileParms, resourceGroupName);
    }
}
```

После создания профиля hello мы создадим конечную точку.

```csharp
private static void CreateCdnEndpoint(CdnManagementClient cdn)
{
    if (endpointAlreadyExists)
    {
        Console.WriteLine("Profile {0} already exists.", profileName);
    }
    else
    {
        Console.WriteLine("Creating endpoint {0} on profile {1}.", endpointName, profileName);
        EndpointCreateParameters endpointParms =
            new EndpointCreateParameters()
            {
                Origins = new List<DeepCreatedOrigin>() { new DeepCreatedOrigin("Contoso", "www.contoso.com") },
                IsHttpAllowed = true,
                IsHttpsAllowed = true,
                Location = resourceLocation
            };
        cdn.Endpoints.Create(endpointName, endpointParms, profileName, resourceGroupName);
    }
}
```

> [!NOTE]
> приведенном выше примере Hello назначает hello конечной точки с именем источника *Contoso* с именем узла `www.contoso.com`.  Изменяйте этот toopoint tooyour собственные имя узла источника.
> 
> 

## <a name="purge-an-endpoint"></a>Очистка конечной точки
Предположим, что hello конечная точка создана, одной из общих задач, может потребоваться tooperform нашей программы удаления hello содержимого в конечной точки.

```csharp
private static void PromptPurgeCdnEndpoint(CdnManagementClient cdn)
{
    if (PromptUser(String.Format("Purge CDN endpoint {0}?", endpointName)))
    {
        Console.WriteLine("Purging endpoint. Please wait...");
        cdn.Endpoints.PurgeContent(endpointName, profileName, resourceGroupName, new List<string>() { "/*" });
        Console.WriteLine("Done.");
        Console.WriteLine();
    }
}
```

> [!NOTE]
> В приведенном выше примере hello, hello строка `/*` обозначает, что требуется toopurge весь код в корень hello hello путь конечной точки.  Это эквивалент toochecking **очистить все** в hello портал Azure «очистить» диалогового окна. В hello `CreateCdnProfile` метода, я создал нашей профиля в качестве **CDN Azure из Verizon** профиля с помощью кода hello `Sku = new Sku(SkuName.StandardVerizon)`, поэтому это будет выполнено успешно.  Тем не менее **Azure CDN с Akamai** профилей не поддерживают **очистить все**, поэтому если я использовал профиль Akamai для этого учебника, я бы toopurge tooinclude определенным путям.
> 
> 

## <a name="delete-cdn-profiles-and-endpoints"></a>Удаление профилей CDN и конечных точек
методы последнего Hello приведет к удалению нашей конечной точки и профиля.

```csharp
private static void PromptDeleteCdnEndpoint(CdnManagementClient cdn)
{
    if(PromptUser(String.Format("Delete CDN endpoint {0} on profile {1}?", endpointName, profileName)))
    {
        Console.WriteLine("Deleting endpoint. Please wait...");
        cdn.Endpoints.DeleteIfExists(endpointName, profileName, resourceGroupName);
        Console.WriteLine("Done.");
        Console.WriteLine();
    }
}

private static void PromptDeleteCdnProfile(CdnManagementClient cdn)
{
    if(PromptUser(String.Format("Delete CDN profile {0}?", profileName)))
    {
        Console.WriteLine("Deleting profile. Please wait...");
        cdn.Profiles.DeleteIfExists(profileName, resourceGroupName);
        Console.WriteLine("Done.");
        Console.WriteLine();
    }
}
```

## <a name="running-hello-program"></a>Запуск программы hello
Теперь можно скомпилировать и запустить программу hello, щелкнув hello **запустить** кнопки в Visual Studio.

![Выполнение программы](./media/cdn-app-dev-net/cdn-program-running-1.png)

Когда программа hello достигает hello выше строки, необходимо группы ресурсов может tooreturn tooyour в hello портал Azure и что hello профиль был создан в разделе.

![Готово!](./media/cdn-app-dev-net/cdn-success.png)

Затем мы можно подтвердить rest hello toorun hello приглашения программы hello.

![Завершение программы](./media/cdn-app-dev-net/cdn-program-running-2.png)

## <a name="next-steps"></a>Дальнейшие действия
toosee hello завершения проекта из этого пошагового руководства [загрузить образец hello](https://code.msdn.microsoft.com/Azure-CDN-Management-1f2fba2c).

дополнительную документацию по hello Библиотека управления CDN Azure для .NET, представление hello toofind [ссылку на MSDN](https://msdn.microsoft.com/library/mt657769.aspx).

Управление ресурсами CDN с помощью [PowerShell](cdn-manage-powershell.md).

