---
title: "Приступая к работе с библиотекой Azure CDN для .NET | Документация Майкрософт"
description: "Узнайте, как с помощью Visual Studio создавать приложения .NET для управления Azure CDN."
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
ms.openlocfilehash: 5379586355ece98af6295236d6cbd09cb31c742b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-azure-cdn-development"></a><span data-ttu-id="23a9b-103">Приступая к разработке для Azure CDN</span><span class="sxs-lookup"><span data-stu-id="23a9b-103">Get started with Azure CDN development</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="23a9b-104">Node.js</span><span class="sxs-lookup"><span data-stu-id="23a9b-104">Node.js</span></span>](cdn-app-dev-node.md)
> * [<span data-ttu-id="23a9b-105">.NET</span><span class="sxs-lookup"><span data-stu-id="23a9b-105">.NET</span></span>](cdn-app-dev-net.md)
> 
> 

<span data-ttu-id="23a9b-106">С помощью [библиотеки Azure CDN для .NET](https://msdn.microsoft.com/library/mt657769.aspx) можно автоматизировать создание профилей и конечных точек CDN и управление ими.</span><span class="sxs-lookup"><span data-stu-id="23a9b-106">You can use the [Azure CDN Library for .NET](https://msdn.microsoft.com/library/mt657769.aspx) to automate creation and management of CDN profiles and endpoints.</span></span>  <span data-ttu-id="23a9b-107">В этом руководстве описывается создание простого консольного приложения .NET, которое демонстрирует некоторые из доступных операций.</span><span class="sxs-lookup"><span data-stu-id="23a9b-107">This tutorial walks through the creation of a simple .NET console application that demonstrates several of the available operations.</span></span>  <span data-ttu-id="23a9b-108">Данный учебник не содержит подробных сведений о всех аспектах библиотеки Azure CDN для .NET.</span><span class="sxs-lookup"><span data-stu-id="23a9b-108">This tutorial is not intended to describe all aspects of the Azure CDN Library for .NET in detail.</span></span>

<span data-ttu-id="23a9b-109">Для работы с этим руководством требуется Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="23a9b-109">You need Visual Studio 2015 to complete this tutorial.</span></span>  <span data-ttu-id="23a9b-110">[Visual Studio Community 2015](https://www.visualstudio.com/products/visual-studio-community-vs.aspx) .</span><span class="sxs-lookup"><span data-stu-id="23a9b-110">[Visual Studio Community 2015](https://www.visualstudio.com/products/visual-studio-community-vs.aspx) is freely available for download.</span></span>

> [!TIP]
> <span data-ttu-id="23a9b-111">[Завершенный проект из этого учебника](https://code.msdn.microsoft.com/Azure-CDN-Management-1f2fba2c) доступен для скачивания на сайте MSDN.</span><span class="sxs-lookup"><span data-stu-id="23a9b-111">The [completed project from this tutorial](https://code.msdn.microsoft.com/Azure-CDN-Management-1f2fba2c) is available for download on MSDN.</span></span>
> 
> 

[!INCLUDE [cdn-app-dev-prep](../../includes/cdn-app-dev-prep.md)]

## <a name="create-your-project-and-add-nuget-packages"></a><span data-ttu-id="23a9b-112">Создание проекта и добавление пакетов Nuget</span><span class="sxs-lookup"><span data-stu-id="23a9b-112">Create your project and add Nuget packages</span></span>
<span data-ttu-id="23a9b-113">Создав группу ресурсов для профилей CDN и назначив приложению Azure AD разрешения для управления профилями CDN и конечными точками в этой группе, мы можем приступить к созданию своего приложения.</span><span class="sxs-lookup"><span data-stu-id="23a9b-113">Now that we've created a resource group for our CDN profiles and given our Azure AD application permission to manage CDN profiles and endpoints within that group, we can start creating our application.</span></span>

<span data-ttu-id="23a9b-114">В Visual Studio 2015 щелкните **Файл** > **Создать** > **Проект**. Откроется диалоговое окно создания проекта.</span><span class="sxs-lookup"><span data-stu-id="23a9b-114">From within Visual Studio 2015, click **File**, **New**, **Project...** to open the new project dialog.</span></span>  <span data-ttu-id="23a9b-115">В области слева разверните узел **Visual C#** и выберите **Windows**.</span><span class="sxs-lookup"><span data-stu-id="23a9b-115">Expand **Visual C#**, then select **Windows** in the pane on the left.</span></span>  <span data-ttu-id="23a9b-116">В центральной области щелкните **Консольное приложение**.</span><span class="sxs-lookup"><span data-stu-id="23a9b-116">Click **Console Application** in the center pane.</span></span>  <span data-ttu-id="23a9b-117">Присвойте проекту имя и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="23a9b-117">Name your project, then click **OK**.</span></span>  

![Новый проект](./media/cdn-app-dev-net/cdn-new-project.png)

<span data-ttu-id="23a9b-119">В нашем проекте будут использоваться некоторые библиотеки Azure, содержащиеся в пакетах Nuget.</span><span class="sxs-lookup"><span data-stu-id="23a9b-119">Our project is going to use some Azure libraries contained in Nuget packages.</span></span>  <span data-ttu-id="23a9b-120">Давайте добавим их в проект.</span><span class="sxs-lookup"><span data-stu-id="23a9b-120">Let's add those to the project.</span></span>

1. <span data-ttu-id="23a9b-121">В меню **Сервис** выберите **Диспетчер пакетов NuGet**, а затем — **Консоль диспетчера пакетов**.</span><span class="sxs-lookup"><span data-stu-id="23a9b-121">Click the **Tools** menu, **Nuget Package Manager**, then **Package Manager Console**.</span></span>
   
    ![Управление пакетами NuGet](./media/cdn-app-dev-net/cdn-manage-nuget.png)
2. <span data-ttu-id="23a9b-123">В консоли диспетчера пакетов выполните приведенную ниже команду, чтобы установить **библиотеку аутентификации Active Directory (ADAL)**.</span><span class="sxs-lookup"><span data-stu-id="23a9b-123">In the Package Manager Console, execute the following command to install the **Active Directory Authentication Library (ADAL)**:</span></span>
   
    `Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory`
3. <span data-ttu-id="23a9b-124">Выполните следующую команду, чтобы установить **библиотеки управления Azure CDN**.</span><span class="sxs-lookup"><span data-stu-id="23a9b-124">Execute the following to install the **Azure CDN Management Library**:</span></span>
   
    `Install-Package Microsoft.Azure.Management.Cdn`

## <a name="directives-constants-main-method-and-helper-methods"></a><span data-ttu-id="23a9b-125">Директивы, константы, главный метод и вспомогательные методы</span><span class="sxs-lookup"><span data-stu-id="23a9b-125">Directives, constants, main method, and helper methods</span></span>
<span data-ttu-id="23a9b-126">Давайте напишем базовую структуру нашей программы.</span><span class="sxs-lookup"><span data-stu-id="23a9b-126">Let's get the basic structure of our program written.</span></span>

1. <span data-ttu-id="23a9b-127">На вкладке Program.cs замените расположенные вверху директивы `using` на следующие.</span><span class="sxs-lookup"><span data-stu-id="23a9b-127">Back in the Program.cs tab, replace the `using` directives at the top with the following:</span></span>
   
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
2. <span data-ttu-id="23a9b-128">Необходимо определить несколько констант, которые будут использоваться нашими методами.</span><span class="sxs-lookup"><span data-stu-id="23a9b-128">We need to define some constants our methods will use.</span></span>  <span data-ttu-id="23a9b-129">В классе `Program` перед методом `Main` добавьте приведенный ниже код.</span><span class="sxs-lookup"><span data-stu-id="23a9b-129">In the `Program` class, but before the `Main` method, add the following.</span></span>  <span data-ttu-id="23a9b-130">Обязательно замените заполнители, включая **&lt;угловые скобки&gt;**, собственными значениями.</span><span class="sxs-lookup"><span data-stu-id="23a9b-130">Be sure to replace the placeholders, including the **&lt;angle brackets&gt;**, with your own values as needed.</span></span>
   
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
3. <span data-ttu-id="23a9b-131">Кроме того, на уровне класса определите эти две переменные.</span><span class="sxs-lookup"><span data-stu-id="23a9b-131">Also at the class level, define these two variables.</span></span>  <span data-ttu-id="23a9b-132">Мы воспользуемся ими позже, чтобы определить, существует ли профиль или конечная точка.</span><span class="sxs-lookup"><span data-stu-id="23a9b-132">We'll use these later to determine if our profile and endpoint already exist.</span></span>
   
    ```csharp
    static bool profileAlreadyExists = false;
    static bool endpointAlreadyExists = false;
    ```
4. <span data-ttu-id="23a9b-133">Замените метод `Main` следующим кодом.</span><span class="sxs-lookup"><span data-stu-id="23a9b-133">Replace the `Main` method as follows:</span></span>
   
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
   
       Console.WriteLine("Press Enter to end program.");
       Console.ReadLine();
   }
   ```
5. <span data-ttu-id="23a9b-134">Некоторые из других методов будет запрашивать у пользователя ответ на вопрос в формате "Да/нет".</span><span class="sxs-lookup"><span data-stu-id="23a9b-134">Some of our other methods are going to prompt the user with "Yes/No" questions.</span></span>  <span data-ttu-id="23a9b-135">Добавьте следующий метод, чтобы упростить это.</span><span class="sxs-lookup"><span data-stu-id="23a9b-135">Add the following method to make that a little easier:</span></span>
   
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

<span data-ttu-id="23a9b-136">Написав базовую структуру программы, давайте создадим методы, вызываемые методом `Main` .</span><span class="sxs-lookup"><span data-stu-id="23a9b-136">Now that the basic structure of our program is written, we should create the methods called by the `Main` method.</span></span>

## <a name="authentication"></a><span data-ttu-id="23a9b-137">Аутентификация</span><span class="sxs-lookup"><span data-stu-id="23a9b-137">Authentication</span></span>
<span data-ttu-id="23a9b-138">Прежде чем можно будет использовать библиотеку управления Azure CDN, необходимо аутентифицировать наш субъект-службу и получить токен аутентификации.</span><span class="sxs-lookup"><span data-stu-id="23a9b-138">Before we can use the Azure CDN Management Library, we need to authenticate our service principal and obtain an authentication token.</span></span>  <span data-ttu-id="23a9b-139">Этот метод использует ADAL для получения токена.</span><span class="sxs-lookup"><span data-stu-id="23a9b-139">This method uses ADAL to retrieve the token.</span></span>

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

<span data-ttu-id="23a9b-140">Если вы используете аутентификацию отдельных пользователей, метод `GetAccessToken` будет выглядеть немного иначе.</span><span class="sxs-lookup"><span data-stu-id="23a9b-140">If you are using individual user authentication, the `GetAccessToken` method will look slightly different.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="23a9b-141">Используйте приведенный пример кода, только если решили использовать аутентификацию отдельных пользователей, а не субъект-службу.</span><span class="sxs-lookup"><span data-stu-id="23a9b-141">Only use this code sample if you are choosing to have individual user authentication instead of a service principal.</span></span>
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

<span data-ttu-id="23a9b-142">Обязательно замените `<redirect URI>` универсальным кодом ресурса (URI) перенаправления, введенным при регистрации приложения в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="23a9b-142">Be sure to replace `<redirect URI>` with the redirect URI you entered when you registered the application in Azure AD.</span></span>

## <a name="list-cdn-profiles-and-endpoints"></a><span data-ttu-id="23a9b-143">Вывод списка профилей CDN и конечных точек</span><span class="sxs-lookup"><span data-stu-id="23a9b-143">List CDN profiles and endpoints</span></span>
<span data-ttu-id="23a9b-144">Теперь все готово к выполнению операций CDN.</span><span class="sxs-lookup"><span data-stu-id="23a9b-144">Now we're ready to perform CDN operations.</span></span>  <span data-ttu-id="23a9b-145">Первое, что делает наш метод, — выводит список профилей и конечных точек в группе ресурсов и, если он обнаруживает совпадение с именами профиля и конечных точек, указанными в константах, то учитывает это на будущее, чтобы мы не пытались создать повторяющиеся значения.</span><span class="sxs-lookup"><span data-stu-id="23a9b-145">The first thing our method does is list all the profiles and endpoints in our resource group, and if it finds a match for the profile and endpoint names specified in our constants, makes a note of that for later so we don't try to create duplicates.</span></span>

```csharp
private static void ListProfilesAndEndpoints(CdnManagementClient cdn)
{
    // List all the CDN profiles in this resource group
    var profileList = cdn.Profiles.ListByResourceGroup(resourceGroupName);
    foreach (Profile p in profileList)
    {
        Console.WriteLine("CDN profile {0}", p.Name);
        if (p.Name.Equals(profileName, StringComparison.OrdinalIgnoreCase))
        {
            // Hey, that's the name of the CDN profile we want to create!
            profileAlreadyExists = true;
        }

        //List all the CDN endpoints on this CDN profile
        Console.WriteLine("Endpoints:");
        var endpointList = cdn.Endpoints.ListByProfile(p.Name, resourceGroupName);
        foreach (Endpoint e in endpointList)
        {
            Console.WriteLine("-{0} ({1})", e.Name, e.HostName);
            if (e.Name.Equals(endpointName, StringComparison.OrdinalIgnoreCase))
            {
                // The unique endpoint name already exists.
                endpointAlreadyExists = true;
            }
        }
        Console.WriteLine();
    }
}
```

## <a name="create-cdn-profiles-and-endpoints"></a><span data-ttu-id="23a9b-146">Создание профилей CDN и конечных точек</span><span class="sxs-lookup"><span data-stu-id="23a9b-146">Create CDN profiles and endpoints</span></span>
<span data-ttu-id="23a9b-147">Далее мы создадим профиль.</span><span class="sxs-lookup"><span data-stu-id="23a9b-147">Next, we'll create a profile.</span></span>

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

<span data-ttu-id="23a9b-148">После этого мы создадим конечную точку.</span><span class="sxs-lookup"><span data-stu-id="23a9b-148">Once the profile is created, we'll create an endpoint.</span></span>

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
> <span data-ttu-id="23a9b-149">В приведенном выше примере конечной точке назначается источник *Contoso* с именем узла `www.contoso.com`.</span><span class="sxs-lookup"><span data-stu-id="23a9b-149">The example above assigns the endpoint an origin named *Contoso* with a hostname `www.contoso.com`.</span></span>  <span data-ttu-id="23a9b-150">Это следует изменить, указав собственное имя узла источника.</span><span class="sxs-lookup"><span data-stu-id="23a9b-150">You should change this to point to your own origin's hostname.</span></span>
> 
> 

## <a name="purge-an-endpoint"></a><span data-ttu-id="23a9b-151">Очистка конечной точки</span><span class="sxs-lookup"><span data-stu-id="23a9b-151">Purge an endpoint</span></span>
<span data-ttu-id="23a9b-152">После создания конечной точки одной из распространенных задач, которая может выполняться в нашей программе, является очистка содержимого в конечной точке.</span><span class="sxs-lookup"><span data-stu-id="23a9b-152">Assuming the endpoint has been created, one common task that we might want to perform in our program is purging the content in our endpoint.</span></span>

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
> <span data-ttu-id="23a9b-153">В приведенном выше примере строка `/*` означает, что я хочу очистить все содержимое в корне конечной точки.</span><span class="sxs-lookup"><span data-stu-id="23a9b-153">In the example above, the string `/*` denotes that I want to purge everything in the root of the endpoint path.</span></span>  <span data-ttu-id="23a9b-154">Этот тоже самое, что установить флажок **Очистить все** в диалоговом окне "Очистить" на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="23a9b-154">This is equivalent to checking **Purge All** in the Azure portal's "purge" dialog.</span></span> <span data-ttu-id="23a9b-155">В методе `CreateCdnProfile` я создал профиль **Azure CDN от Verizon** с помощью кода `Sku = new Sku(SkuName.StandardVerizon)`, поэтому операция будет выполнена успешно.</span><span class="sxs-lookup"><span data-stu-id="23a9b-155">In the `CreateCdnProfile` method, I created our profile as an **Azure CDN from Verizon** profile using the code `Sku = new Sku(SkuName.StandardVerizon)`, so this will be successful.</span></span>  <span data-ttu-id="23a9b-156">Однако профили **Azure CDN от Akamai** не поддерживают функцию **Очистить все**. Если бы я использовал в этом руководстве профиль Akamai, мне пришлось бы указать конкретные расположения, в которых нужно выполнить очистку.</span><span class="sxs-lookup"><span data-stu-id="23a9b-156">However, **Azure CDN from Akamai** profiles do not support **Purge All**, so if I was using an Akamai profile for this tutorial, I would need to include specific paths to purge.</span></span>
> 
> 

## <a name="delete-cdn-profiles-and-endpoints"></a><span data-ttu-id="23a9b-157">Удаление профилей CDN и конечных точек</span><span class="sxs-lookup"><span data-stu-id="23a9b-157">Delete CDN profiles and endpoints</span></span>
<span data-ttu-id="23a9b-158">Последние методы удаляют конечную точку и профиль.</span><span class="sxs-lookup"><span data-stu-id="23a9b-158">The last methods will delete our endpoint and profile.</span></span>

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

## <a name="running-the-program"></a><span data-ttu-id="23a9b-159">Запуск программы</span><span class="sxs-lookup"><span data-stu-id="23a9b-159">Running the program</span></span>
<span data-ttu-id="23a9b-160">Теперь можно скомпилировать и запустить программу, нажав в Visual Studio кнопку **Запустить** .</span><span class="sxs-lookup"><span data-stu-id="23a9b-160">We can now compile and run the program by clicking the **Start** button in Visual Studio.</span></span>

![Выполнение программы](./media/cdn-app-dev-net/cdn-program-running-1.png)

<span data-ttu-id="23a9b-162">Когда программа дойдет до упомянутого выше запроса, вы сможете вернуться к группе ресурсов на портале Azure и увидеть, что профиль создан.</span><span class="sxs-lookup"><span data-stu-id="23a9b-162">When the program reaches the above prompt, you should be able to return to your resource group in the Azure portal and see that the profile has been created.</span></span>

![Готово!](./media/cdn-app-dev-net/cdn-success.png)

<span data-ttu-id="23a9b-164">Затем мы можем подтвердить запросы, чтобы была выполнена оставшаяся часть программы.</span><span class="sxs-lookup"><span data-stu-id="23a9b-164">We can then confirm the prompts to run the rest of the program.</span></span>

![Завершение программы](./media/cdn-app-dev-net/cdn-program-running-2.png)

## <a name="next-steps"></a><span data-ttu-id="23a9b-166">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="23a9b-166">Next Steps</span></span>
<span data-ttu-id="23a9b-167">Чтобы просмотреть описываемый в этом руководстве готовый проект, [скачайте пример](https://code.msdn.microsoft.com/Azure-CDN-Management-1f2fba2c).</span><span class="sxs-lookup"><span data-stu-id="23a9b-167">To see the completed project from this walkthrough, [download the sample](https://code.msdn.microsoft.com/Azure-CDN-Management-1f2fba2c).</span></span>

<span data-ttu-id="23a9b-168">Чтобы найти дополнительную документацию по библиотеке управления Azure CDN для .NET, воспользуйтесь [справкой на сайте MSDN](https://msdn.microsoft.com/library/mt657769.aspx).</span><span class="sxs-lookup"><span data-stu-id="23a9b-168">To find additional documentation on the Azure CDN Management Library for .NET, view the [reference on MSDN](https://msdn.microsoft.com/library/mt657769.aspx).</span></span>

<span data-ttu-id="23a9b-169">Управление ресурсами CDN с помощью [PowerShell](cdn-manage-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="23a9b-169">Manage your CDN resources with [PowerShell](cdn-manage-powershell.md).</span></span>

