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
# <a name="get-started-with-azure-cdn-development"></a><span data-ttu-id="a27d0-103">Приступая к разработке для Azure CDN</span><span class="sxs-lookup"><span data-stu-id="a27d0-103">Get started with Azure CDN development</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="a27d0-104">Node.js</span><span class="sxs-lookup"><span data-stu-id="a27d0-104">Node.js</span></span>](cdn-app-dev-node.md)
> * [<span data-ttu-id="a27d0-105">.NET</span><span class="sxs-lookup"><span data-stu-id="a27d0-105">.NET</span></span>](cdn-app-dev-net.md)
> 
> 

<span data-ttu-id="a27d0-106">Можно использовать hello [библиотеку CDN Azure для .NET](https://msdn.microsoft.com/library/mt657769.aspx) tooautomate создания и управления профилями CDN и конечных точек.</span><span class="sxs-lookup"><span data-stu-id="a27d0-106">You can use hello [Azure CDN Library for .NET](https://msdn.microsoft.com/library/mt657769.aspx) tooautomate creation and management of CDN profiles and endpoints.</span></span>  <span data-ttu-id="a27d0-107">Этого учебника вы научитесь hello создания простого консольного приложения .NET, демонстрирующий некоторые из доступных операций hello.</span><span class="sxs-lookup"><span data-stu-id="a27d0-107">This tutorial walks through hello creation of a simple .NET console application that demonstrates several of hello available operations.</span></span>  <span data-ttu-id="a27d0-108">Этот учебник является не предназначен toodescribe все аспекты hello библиотеку CDN Azure для .NET подробно.</span><span class="sxs-lookup"><span data-stu-id="a27d0-108">This tutorial is not intended toodescribe all aspects of hello Azure CDN Library for .NET in detail.</span></span>

<span data-ttu-id="a27d0-109">Требуется Visual Studio 2015 toocomplete этого учебника.</span><span class="sxs-lookup"><span data-stu-id="a27d0-109">You need Visual Studio 2015 toocomplete this tutorial.</span></span>  <span data-ttu-id="a27d0-110">[Visual Studio Community 2015](https://www.visualstudio.com/products/visual-studio-community-vs.aspx) .</span><span class="sxs-lookup"><span data-stu-id="a27d0-110">[Visual Studio Community 2015](https://www.visualstudio.com/products/visual-studio-community-vs.aspx) is freely available for download.</span></span>

> [!TIP]
> <span data-ttu-id="a27d0-111">Hello [завершенный проект из этого учебника](https://code.msdn.microsoft.com/Azure-CDN-Management-1f2fba2c) доступен для загрузки на сайте MSDN.</span><span class="sxs-lookup"><span data-stu-id="a27d0-111">hello [completed project from this tutorial](https://code.msdn.microsoft.com/Azure-CDN-Management-1f2fba2c) is available for download on MSDN.</span></span>
> 
> 

[!INCLUDE [cdn-app-dev-prep](../../includes/cdn-app-dev-prep.md)]

## <a name="create-your-project-and-add-nuget-packages"></a><span data-ttu-id="a27d0-112">Создание проекта и добавление пакетов Nuget</span><span class="sxs-lookup"><span data-stu-id="a27d0-112">Create your project and add Nuget packages</span></span>
<span data-ttu-id="a27d0-113">Теперь, что мы создали группу ресурсов для наших CDN профилей и заданным нашей профили CDN toomanage разрешений приложения Azure AD и конечных точек в пределах этой группы, можно начать создание нашего приложения.</span><span class="sxs-lookup"><span data-stu-id="a27d0-113">Now that we've created a resource group for our CDN profiles and given our Azure AD application permission toomanage CDN profiles and endpoints within that group, we can start creating our application.</span></span>

<span data-ttu-id="a27d0-114">В Visual Studio 2015 выберите **файл**, **New**, **проекта...**  диалоговое окно нового проекта tooopen hello.</span><span class="sxs-lookup"><span data-stu-id="a27d0-114">From within Visual Studio 2015, click **File**, **New**, **Project...** tooopen hello new project dialog.</span></span>  <span data-ttu-id="a27d0-115">Разверните **Visual C#**, а затем выберите **Windows** hello панели слева hello.</span><span class="sxs-lookup"><span data-stu-id="a27d0-115">Expand **Visual C#**, then select **Windows** in hello pane on hello left.</span></span>  <span data-ttu-id="a27d0-116">Нажмите кнопку **консольное приложение** hello центральной панели.</span><span class="sxs-lookup"><span data-stu-id="a27d0-116">Click **Console Application** in hello center pane.</span></span>  <span data-ttu-id="a27d0-117">Присвойте проекту имя и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="a27d0-117">Name your project, then click **OK**.</span></span>  

![Новый проект](./media/cdn-app-dev-net/cdn-new-project.png)

<span data-ttu-id="a27d0-119">Наш проект будет toouse некоторые библиотеки Azure, содержащиеся в пакетах Nuget.</span><span class="sxs-lookup"><span data-stu-id="a27d0-119">Our project is going toouse some Azure libraries contained in Nuget packages.</span></span>  <span data-ttu-id="a27d0-120">Давайте добавим эти toohello проекта.</span><span class="sxs-lookup"><span data-stu-id="a27d0-120">Let's add those toohello project.</span></span>

1. <span data-ttu-id="a27d0-121">Нажмите кнопку hello **средства** меню **диспетчера пакетов Nuget**, затем **консоль диспетчера пакетов**.</span><span class="sxs-lookup"><span data-stu-id="a27d0-121">Click hello **Tools** menu, **Nuget Package Manager**, then **Package Manager Console**.</span></span>
   
    ![Управление пакетами NuGet](./media/cdn-app-dev-net/cdn-manage-nuget.png)
2. <span data-ttu-id="a27d0-123">В hello консоль диспетчера пакетов выполните hello, следующая команда hello tooinstall **библиотеку проверки подлинности Active Directory (ADAL)**:</span><span class="sxs-lookup"><span data-stu-id="a27d0-123">In hello Package Manager Console, execute hello following command tooinstall hello **Active Directory Authentication Library (ADAL)**:</span></span>
   
    `Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory`
3. <span data-ttu-id="a27d0-124">Выполните следующие tooinstall hello hello **Библиотека управления Azure CDN**:</span><span class="sxs-lookup"><span data-stu-id="a27d0-124">Execute hello following tooinstall hello **Azure CDN Management Library**:</span></span>
   
    `Install-Package Microsoft.Azure.Management.Cdn`

## <a name="directives-constants-main-method-and-helper-methods"></a><span data-ttu-id="a27d0-125">Директивы, константы, главный метод и вспомогательные методы</span><span class="sxs-lookup"><span data-stu-id="a27d0-125">Directives, constants, main method, and helper methods</span></span>
<span data-ttu-id="a27d0-126">Давайте базовая структура нашей программы, написанной hello.</span><span class="sxs-lookup"><span data-stu-id="a27d0-126">Let's get hello basic structure of our program written.</span></span>

1. <span data-ttu-id="a27d0-127">Назад на вкладке Program.cs hello, замените hello `using` директивы вверху hello hello следующее:</span><span class="sxs-lookup"><span data-stu-id="a27d0-127">Back in hello Program.cs tab, replace hello `using` directives at hello top with hello following:</span></span>
   
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
2. <span data-ttu-id="a27d0-128">Мы должны toodefine некоторые константы, которые будут использовать наши методы.</span><span class="sxs-lookup"><span data-stu-id="a27d0-128">We need toodefine some constants our methods will use.</span></span>  <span data-ttu-id="a27d0-129">В hello `Program` класса, но до hello `Main` метод, добавьте следующее hello.</span><span class="sxs-lookup"><span data-stu-id="a27d0-129">In hello `Program` class, but before hello `Main` method, add hello following.</span></span>  <span data-ttu-id="a27d0-130">Быть заполнители hello, включая hello убедиться, что tooreplace  **&lt;угловые скобки&gt;**, собственными значениями, при необходимости.</span><span class="sxs-lookup"><span data-stu-id="a27d0-130">Be sure tooreplace hello placeholders, including hello **&lt;angle brackets&gt;**, with your own values as needed.</span></span>
   
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
3. <span data-ttu-id="a27d0-131">Также на уровне класса hello, определите эти две переменные.</span><span class="sxs-lookup"><span data-stu-id="a27d0-131">Also at hello class level, define these two variables.</span></span>  <span data-ttu-id="a27d0-132">Мы будем использовать эти toodetermine более поздней версии, если конечная точка и профилей уже существует.</span><span class="sxs-lookup"><span data-stu-id="a27d0-132">We'll use these later toodetermine if our profile and endpoint already exist.</span></span>
   
    ```csharp
    static bool profileAlreadyExists = false;
    static bool endpointAlreadyExists = false;
    ```
4. <span data-ttu-id="a27d0-133">Замените hello `Main` метод следующим образом:</span><span class="sxs-lookup"><span data-stu-id="a27d0-133">Replace hello `Main` method as follows:</span></span>
   
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
5. <span data-ttu-id="a27d0-134">Некоторые другие методы будут tooprompt hello пользователя с вопросами «Да/нет».</span><span class="sxs-lookup"><span data-stu-id="a27d0-134">Some of our other methods are going tooprompt hello user with "Yes/No" questions.</span></span>  <span data-ttu-id="a27d0-135">Добавьте следующий метод toomake hello, немного удобнее:</span><span class="sxs-lookup"><span data-stu-id="a27d0-135">Add hello following method toomake that a little easier:</span></span>
   
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

<span data-ttu-id="a27d0-136">Теперь, когда записывается hello базовой структуры программы, следует создавать hello методы, вызываемые hello `Main` метод.</span><span class="sxs-lookup"><span data-stu-id="a27d0-136">Now that hello basic structure of our program is written, we should create hello methods called by hello `Main` method.</span></span>

## <a name="authentication"></a><span data-ttu-id="a27d0-137">Аутентификация</span><span class="sxs-lookup"><span data-stu-id="a27d0-137">Authentication</span></span>
<span data-ttu-id="a27d0-138">Чтобы мы могли использовать hello Библиотека управления Azure CDN, нам нужна tooauthenticate наша служба основной и получить маркер проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="a27d0-138">Before we can use hello Azure CDN Management Library, we need tooauthenticate our service principal and obtain an authentication token.</span></span>  <span data-ttu-id="a27d0-139">Этот метод использует токен ADAL tooretrieve hello.</span><span class="sxs-lookup"><span data-stu-id="a27d0-139">This method uses ADAL tooretrieve hello token.</span></span>

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

<span data-ttu-id="a27d0-140">При использовании проверки подлинности пользователя hello `GetAccessToken` метод будет выглядят немного иначе.</span><span class="sxs-lookup"><span data-stu-id="a27d0-140">If you are using individual user authentication, hello `GetAccessToken` method will look slightly different.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a27d0-141">Этот пример кода следует используйте только при выборе toohave проверки подлинности пользователя вместо участника-службы.</span><span class="sxs-lookup"><span data-stu-id="a27d0-141">Only use this code sample if you are choosing toohave individual user authentication instead of a service principal.</span></span>
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

<span data-ttu-id="a27d0-142">Убедиться, что tooreplace быть `<redirect URI>` с hello URI перенаправления, который вы ввели при регистрации приложения hello в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a27d0-142">Be sure tooreplace `<redirect URI>` with hello redirect URI you entered when you registered hello application in Azure AD.</span></span>

## <a name="list-cdn-profiles-and-endpoints"></a><span data-ttu-id="a27d0-143">Вывод списка профилей CDN и конечных точек</span><span class="sxs-lookup"><span data-stu-id="a27d0-143">List CDN profiles and endpoints</span></span>
<span data-ttu-id="a27d0-144">Теперь мы готовы tooperform CDN операций.</span><span class="sxs-lookup"><span data-stu-id="a27d0-144">Now we're ready tooperform CDN operations.</span></span>  <span data-ttu-id="a27d0-145">Hello первое, что делает наш метод — список всех профилей hello и конечных точек в нашей группы ресурсов, а при обнаружении совпадения для hello профиль и конечную точку имена, указанные в нашем константы делает Обратите внимание, для использования в дальнейшем, поэтому мы не пытаемся дубликатов toocreate.</span><span class="sxs-lookup"><span data-stu-id="a27d0-145">hello first thing our method does is list all hello profiles and endpoints in our resource group, and if it finds a match for hello profile and endpoint names specified in our constants, makes a note of that for later so we don't try toocreate duplicates.</span></span>

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

## <a name="create-cdn-profiles-and-endpoints"></a><span data-ttu-id="a27d0-146">Создание профилей CDN и конечных точек</span><span class="sxs-lookup"><span data-stu-id="a27d0-146">Create CDN profiles and endpoints</span></span>
<span data-ttu-id="a27d0-147">Далее мы создадим профиль.</span><span class="sxs-lookup"><span data-stu-id="a27d0-147">Next, we'll create a profile.</span></span>

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

<span data-ttu-id="a27d0-148">После создания профиля hello мы создадим конечную точку.</span><span class="sxs-lookup"><span data-stu-id="a27d0-148">Once hello profile is created, we'll create an endpoint.</span></span>

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
> <span data-ttu-id="a27d0-149">приведенном выше примере Hello назначает hello конечной точки с именем источника *Contoso* с именем узла `www.contoso.com`.</span><span class="sxs-lookup"><span data-stu-id="a27d0-149">hello example above assigns hello endpoint an origin named *Contoso* with a hostname `www.contoso.com`.</span></span>  <span data-ttu-id="a27d0-150">Изменяйте этот toopoint tooyour собственные имя узла источника.</span><span class="sxs-lookup"><span data-stu-id="a27d0-150">You should change this toopoint tooyour own origin's hostname.</span></span>
> 
> 

## <a name="purge-an-endpoint"></a><span data-ttu-id="a27d0-151">Очистка конечной точки</span><span class="sxs-lookup"><span data-stu-id="a27d0-151">Purge an endpoint</span></span>
<span data-ttu-id="a27d0-152">Предположим, что hello конечная точка создана, одной из общих задач, может потребоваться tooperform нашей программы удаления hello содержимого в конечной точки.</span><span class="sxs-lookup"><span data-stu-id="a27d0-152">Assuming hello endpoint has been created, one common task that we might want tooperform in our program is purging hello content in our endpoint.</span></span>

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
> <span data-ttu-id="a27d0-153">В приведенном выше примере hello, hello строка `/*` обозначает, что требуется toopurge весь код в корень hello hello путь конечной точки.</span><span class="sxs-lookup"><span data-stu-id="a27d0-153">In hello example above, hello string `/*` denotes that I want toopurge everything in hello root of hello endpoint path.</span></span>  <span data-ttu-id="a27d0-154">Это эквивалент toochecking **очистить все** в hello портал Azure «очистить» диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="a27d0-154">This is equivalent toochecking **Purge All** in hello Azure portal's "purge" dialog.</span></span> <span data-ttu-id="a27d0-155">В hello `CreateCdnProfile` метода, я создал нашей профиля в качестве **CDN Azure из Verizon** профиля с помощью кода hello `Sku = new Sku(SkuName.StandardVerizon)`, поэтому это будет выполнено успешно.</span><span class="sxs-lookup"><span data-stu-id="a27d0-155">In hello `CreateCdnProfile` method, I created our profile as an **Azure CDN from Verizon** profile using hello code `Sku = new Sku(SkuName.StandardVerizon)`, so this will be successful.</span></span>  <span data-ttu-id="a27d0-156">Тем не менее **Azure CDN с Akamai** профилей не поддерживают **очистить все**, поэтому если я использовал профиль Akamai для этого учебника, я бы toopurge tooinclude определенным путям.</span><span class="sxs-lookup"><span data-stu-id="a27d0-156">However, **Azure CDN from Akamai** profiles do not support **Purge All**, so if I was using an Akamai profile for this tutorial, I would need tooinclude specific paths toopurge.</span></span>
> 
> 

## <a name="delete-cdn-profiles-and-endpoints"></a><span data-ttu-id="a27d0-157">Удаление профилей CDN и конечных точек</span><span class="sxs-lookup"><span data-stu-id="a27d0-157">Delete CDN profiles and endpoints</span></span>
<span data-ttu-id="a27d0-158">методы последнего Hello приведет к удалению нашей конечной точки и профиля.</span><span class="sxs-lookup"><span data-stu-id="a27d0-158">hello last methods will delete our endpoint and profile.</span></span>

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

## <a name="running-hello-program"></a><span data-ttu-id="a27d0-159">Запуск программы hello</span><span class="sxs-lookup"><span data-stu-id="a27d0-159">Running hello program</span></span>
<span data-ttu-id="a27d0-160">Теперь можно скомпилировать и запустить программу hello, щелкнув hello **запустить** кнопки в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="a27d0-160">We can now compile and run hello program by clicking hello **Start** button in Visual Studio.</span></span>

![Выполнение программы](./media/cdn-app-dev-net/cdn-program-running-1.png)

<span data-ttu-id="a27d0-162">Когда программа hello достигает hello выше строки, необходимо группы ресурсов может tooreturn tooyour в hello портал Azure и что hello профиль был создан в разделе.</span><span class="sxs-lookup"><span data-stu-id="a27d0-162">When hello program reaches hello above prompt, you should be able tooreturn tooyour resource group in hello Azure portal and see that hello profile has been created.</span></span>

![Готово!](./media/cdn-app-dev-net/cdn-success.png)

<span data-ttu-id="a27d0-164">Затем мы можно подтвердить rest hello toorun hello приглашения программы hello.</span><span class="sxs-lookup"><span data-stu-id="a27d0-164">We can then confirm hello prompts toorun hello rest of hello program.</span></span>

![Завершение программы](./media/cdn-app-dev-net/cdn-program-running-2.png)

## <a name="next-steps"></a><span data-ttu-id="a27d0-166">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="a27d0-166">Next Steps</span></span>
<span data-ttu-id="a27d0-167">toosee hello завершения проекта из этого пошагового руководства [загрузить образец hello](https://code.msdn.microsoft.com/Azure-CDN-Management-1f2fba2c).</span><span class="sxs-lookup"><span data-stu-id="a27d0-167">toosee hello completed project from this walkthrough, [download hello sample](https://code.msdn.microsoft.com/Azure-CDN-Management-1f2fba2c).</span></span>

<span data-ttu-id="a27d0-168">дополнительную документацию по hello Библиотека управления CDN Azure для .NET, представление hello toofind [ссылку на MSDN](https://msdn.microsoft.com/library/mt657769.aspx).</span><span class="sxs-lookup"><span data-stu-id="a27d0-168">toofind additional documentation on hello Azure CDN Management Library for .NET, view hello [reference on MSDN](https://msdn.microsoft.com/library/mt657769.aspx).</span></span>

<span data-ttu-id="a27d0-169">Управление ресурсами CDN с помощью [PowerShell](cdn-manage-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="a27d0-169">Manage your CDN resources with [PowerShell](cdn-manage-powershell.md).</span></span>

