---
title: "Использование пакета SDK для .NET для доступа к интерфейсам API Служб мобильного взаимодействия Azure"
description: "Описывает, как использовать пакет SDK Служб мобильного взаимодействия для .NET для доступа к интерфейсам API Служб мобильного взаимодействия Azure"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: c07728aa-43f2-4238-8b4a-c9eddf9d838b
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-multiple
ms.devlang: dotnet
ms.topic: article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 6a497189268c5a1b7e269cc57904ebc77c1906fd
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="using-net-sdk-to-access-azure-mobile-engagement-service-apis"></a><span data-ttu-id="1155e-103">Использование пакета SDK для .NET для доступа к интерфейсам API Служб мобильного взаимодействия Azure</span><span class="sxs-lookup"><span data-stu-id="1155e-103">Using .NET SDK to access Azure Mobile Engagement Service APIs</span></span>
<span data-ttu-id="1155e-104">Службы мобильного взаимодействия Azure предоставляют набор интерфейсов API для управления устройствами, кампаниями охвата/продвижения и т. д. Для взаимодействия с этими интерфейсами API мы также предоставляем [файл Swagger](https://github.com/Azure/azure-rest-api-specs/blob/master/arm-mobileengagement/2014-12-01/swagger/mobile-engagement.json), который можно использовать со средствами для создания пакетов SDK для предпочитаемого языка.</span><span class="sxs-lookup"><span data-stu-id="1155e-104">Azure Mobile Engagement exposes a set of APIs for you to manage Devices, Reach/Push campaigns etc. To interact with these APIs, we also provide you a [Swagger file](https://github.com/Azure/azure-rest-api-specs/blob/master/arm-mobileengagement/2014-12-01/swagger/mobile-engagement.json) that you can use with tools to generate SDKs for your preferred language.</span></span> <span data-ttu-id="1155e-105">Мы рекомендуем использовать средство [AutoRest](https://github.com/Azure/AutoRest) для создания пакета SDK из нашего файла Swagger.</span><span class="sxs-lookup"><span data-stu-id="1155e-105">We recommend using the [AutoRest](https://github.com/Azure/AutoRest) tool to generate your SDK from our Swagger file.</span></span>

> [!NOTE]
> <span data-ttu-id="1155e-106">Мы прекратим использование Служб мобильного взаимодействия Azure в марте 2018 г. Сейчас они доступны только существующим клиентам.</span><span class="sxs-lookup"><span data-stu-id="1155e-106">The Azure Mobile Engagement service will be retired March 2018 and is currently only available to existing customers.</span></span> <span data-ttu-id="1155e-107">Дополнительные сведения см. на странице [Службы мобильного взаимодействия](https://azure.microsoft.com/en-us/services/mobile-engagement/).</span><span class="sxs-lookup"><span data-stu-id="1155e-107">For more information, see [Mobile Engagement](https://azure.microsoft.com/en-us/services/mobile-engagement/).</span></span>

<span data-ttu-id="1155e-108">Аналогичным образом мы создали пакет SDK для .NET, который позволяет взаимодействовать с этими интерфейсами API с помощью оболочки C# без самостоятельного согласования маркера проверки подлинности и обновления.</span><span class="sxs-lookup"><span data-stu-id="1155e-108">We have created a .NET SDK in a similar manner which allows you to interact with these APIs using a C# wrapper and you don't have to do the authentication token negotiation and refresh yourself.</span></span>  

<span data-ttu-id="1155e-109">В этом примере используется набор шагов, которые необходимо выполнить для использования пакета SDK для .NET:</span><span class="sxs-lookup"><span data-stu-id="1155e-109">This sample goes through the set of steps to follow to use the .NET SDK:</span></span>

1. <span data-ttu-id="1155e-110">Во-первых, необходимо настроить проверку подлинности для интерфейсов API с помощью Azure Active Directory, как описано [здесь](mobile-engagement-api-authentication.md#authentication).</span><span class="sxs-lookup"><span data-stu-id="1155e-110">First of all, you need to setup the authentication for your APIs using the Azure Active Directory as described [here](mobile-engagement-api-authentication.md#authentication).</span></span> <span data-ttu-id="1155e-111">По завершении этих шагов вы должны иметь допустимые **идентификатор подписки**, **идентификатор клиента**, **идентификатор приложения** и **секрет**.</span><span class="sxs-lookup"><span data-stu-id="1155e-111">At the end of these steps, you should have a valid **SubscriptionId**, **TenantId**, **ApplicationId** and **Secret**.</span></span> 
2. <span data-ttu-id="1155e-112">Мы используем простое консольное приложение Windows для демонстрации работы с пакетом SDK для .NET с помощью сценария создания кампании типа "Объявление".</span><span class="sxs-lookup"><span data-stu-id="1155e-112">We will use a simple Windows Console app to demonstrate working with the .NET SDK with the scenario of creating an Announcement campaign.</span></span> <span data-ttu-id="1155e-113">Откройте Visual Studio и создайте **консольное приложение**.</span><span class="sxs-lookup"><span data-stu-id="1155e-113">So open up Visual Studio and create a **Console Application**.</span></span>   
3. <span data-ttu-id="1155e-114">Далее необходимо загрузить пакет SDK для .NET, который доступен в виде **библиотеки управления Microsoft Azure Engagement** в коллекции Nuget [здесь](https://www.nuget.org/packages/Microsoft.Azure.Management.Engagement/).</span><span class="sxs-lookup"><span data-stu-id="1155e-114">Next you need to download the .NET SDK which is available as **Microsoft Azure Engagement Management Library** in the Nuget gallery [here](https://www.nuget.org/packages/Microsoft.Azure.Management.Engagement/).</span></span>
   <span data-ttu-id="1155e-115">Если вы устанавливаете Nuget из Visual Studio, убедитесь, что при поиске пакета установлен флажок **Включить предварительный выпуск** :</span><span class="sxs-lookup"><span data-stu-id="1155e-115">If you are installing the Nuget from Visual Studio, you need to ensure that you have check marked the **Include prerelease** option while searching for the package:</span></span>
   
    ![][1]
4. <span data-ttu-id="1155e-116">В файле `Program.cs` добавьте следующие пространства имен:</span><span class="sxs-lookup"><span data-stu-id="1155e-116">In the `Program.cs` file, add the following namespaces:</span></span>
   
        using Microsoft.Rest.Azure.Authentication;
        using Microsoft.Azure.Management.Engagement;
        using Microsoft.Azure.Management.Engagement.Models;
5. <span data-ttu-id="1155e-117">Затем необходимо определить следующие константы, которые будут использоваться для проверки подлинности и взаимодействия с приложением Служб мобильного взаимодействия, в котором вы создаете кампанию типа "Объявление":</span><span class="sxs-lookup"><span data-stu-id="1155e-117">Next you need to define the following constants that we will use for authentication and interacting with the Mobile Engagement App in which you are creating the Announcement campaign:</span></span>
   
        // For authentication
        const string TENANT_ID = "<Your TenantId>";
        const string CLIENT_ID = "<Your Application Id>";
        const string CLIENT_SECRET = "<Your Secret>";
        const string SUBSCRIPTION_ID = "<Your Subscription Id>";
   
        // This is the Azure Resource group concept for grouping together resources 
        //  see here: https://azure.microsoft.com/en-us/documentation/articles/resource-group-portal/
        const string RESOURCE_GROUP = "";
   
        // For Mobile Engagement operations
        // App Collection Name 
        const string APP_COLLECTION_NAME = "";
        // Application Resource Name - make sure you are using the one as specified in the Azure portal (NOT the App Name)
        const string APP_RESOURCE_NAME = "";
6. <span data-ttu-id="1155e-118">Определите переменную `EngagementManagementClient`, которая будет использоваться для вызова методов пакета SDK для Служб мобильного взаимодействия:</span><span class="sxs-lookup"><span data-stu-id="1155e-118">Define the `EngagementManagementClient` variable which we will use to call the Mobile Engagement SDK methods:</span></span>
   
        static EngagementManagementClient engagementClient; 
7. <span data-ttu-id="1155e-119">Затем добавьте в метод `Main` следующие строки:</span><span class="sxs-lookup"><span data-stu-id="1155e-119">Add the following to your `Main` method:</span></span>
   
        try
            {
                // Initialize the Engagement SDK to call out APIs. 
                InitEngagementClient().Wait();
   
                // Create a Reach campaign
                CreateCampaign().Wait();
            }
            catch (Exception ex)
            {
                Console.WriteLine(ex.InnerException.Message);
                throw ex;
            }
8. <span data-ttu-id="1155e-120">Определите следующий метод, который отвечает за инициализацию `EngagementManagementClient`, выполняя проверку подлинности и связывая себя с приложением Служб мобильного взаимодействия, в котором вы планируете создать кампанию типа "Объявление":</span><span class="sxs-lookup"><span data-stu-id="1155e-120">Define the following method which takes care of initializing the `EngagementManagementClient` by first authenticating and then associating itself with the Mobile Engagement App in which you plan to create the Announcement campaign:</span></span>
   
        private static async Task InitEngagementClient()
        {
            var credentials = await ApplicationTokenProvider.LoginSilentAsync(TENANT_ID, CLIENT_ID, CLIENT_SECRET);
            engagementClient = new EngagementManagementClient(credentials) { SubscriptionId = SUBSCRIPTION_ID };
   
            // This is the Azure concept of ResourceGroup
            engagementClient.ResourceGroupName = RESOURCE_GROUP;
   
            // This is your Mobile Engagement App Collection & App Resource Name in which you create the campaign
            engagementClient.AppCollection = APP_COLLECTION_NAME;
            engagementClient.AppName = APP_RESOURCE_NAME;
        }
   
   > [!IMPORTANT]
   > <span data-ttu-id="1155e-121">Обратите внимание, что для параметра AppName необходимо использовать **имя ресурса приложения** , определенное в портале управления Azure.</span><span class="sxs-lookup"><span data-stu-id="1155e-121">Note that you need to use the **App Resource Name** as defined in the Azure management portal for the AppName parameter.</span></span> 
   > 
   > 
9. <span data-ttu-id="1155e-122">Наконец, определите метод CreateCampaign, который с помощью ранее инициализированного объекта EngagementClient создаст простую кампанию с характеристиками **любое время** & **Только уведомление** и со следующим заголовком и сообщением:</span><span class="sxs-lookup"><span data-stu-id="1155e-122">Lastly, define the CreateCampaign method which will take care of using the previously initialized EngagementClient to create a simple **AnyTime** & **Notification-only** campaign with a title and message:</span></span> 
   
        private async static Task CreateCampaign()
        {
            //  Refer to the Announcement Campaign format from here - 
            //      https://msdn.microsoft.com/en-us/library/azure/mt683751.aspx
            // Make sure you are passing all the non-optional parameters
            Campaign parameters = new Campaign(
                name:"WelcomeCampaign",
                notificationTitle: "Welcome", 
                notificationMessage: "Thank you for installing the app!",
                type:"only_notif",
                deliveryTime:"any"
                );
   
            // Refer to the Campaign Kinds from here - https://msdn.microsoft.com/en-us/library/azure/mt683742.aspx
            CampaignStateResult result = 
                await engagementClient.Campaigns.CreateAsync(CampaignKinds.Announcements, parameters);
            Console.WriteLine("Campaign Id '{0}' was created successfully and it is in '{1}' state", result.Id, result.State);
        }
10. <span data-ttu-id="1155e-123">Запустите консольное приложение, и при успешном создании кампании вы увидите следующее сообщение:</span><span class="sxs-lookup"><span data-stu-id="1155e-123">Run the console app and you will see the following on successful creation of the campaign:</span></span>
    
    <span data-ttu-id="1155e-124">**Кампания с идентификатором 159 успешно создана и находится в состоянии "черновик"**</span><span class="sxs-lookup"><span data-stu-id="1155e-124">**Campaign Id '159' was created successfully and it is in 'draft' state**</span></span>

<!-- Images. -->

[1]: ./media/mobile-engagement-dotnet-sdk-service-api/include-prerelease.png
