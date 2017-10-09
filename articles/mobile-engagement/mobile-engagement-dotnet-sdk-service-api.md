---
title: "aaaUsing tooaccess .NET SDK Azure Mobile Engagement программные интерфейсы API"
description: "Описывает, каким образом toouse hello tooaccess Mobile Engagement .NET SDK API-интерфейсы службы Azure Mobile Engagement"
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
ms.openlocfilehash: 812be6f507b29f7b2de6454e06face8082c2d161
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="using-net-sdk-tooaccess-azure-mobile-engagement-service-apis"></a><span data-ttu-id="65652-103">С помощью пакета SDK для .NET tooaccess API-интерфейсы службы Azure Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="65652-103">Using .NET SDK tooaccess Azure Mobile Engagement Service APIs</span></span>
<span data-ttu-id="65652-104">Azure Mobile Engagement предоставляет набор API-интерфейсов для вас toomanage устройств Reach/принудительной кампании toointeract т. д. с этими интерфейсами API, мы предлагаем вам [файл Swagger](https://github.com/Azure/azure-rest-api-specs/blob/master/arm-mobileengagement/2014-12-01/swagger/mobile-engagement.json) , можно использовать с средств toogenerate пакеты SDK для предпочитаемого язык.</span><span class="sxs-lookup"><span data-stu-id="65652-104">Azure Mobile Engagement exposes a set of APIs for you toomanage Devices, Reach/Push campaigns etc. toointeract with these APIs, we also provide you a [Swagger file](https://github.com/Azure/azure-rest-api-specs/blob/master/arm-mobileengagement/2014-12-01/swagger/mobile-engagement.json) that you can use with tools toogenerate SDKs for your preferred language.</span></span> <span data-ttu-id="65652-105">Мы рекомендуем использовать hello [AutoRest](https://github.com/Azure/AutoRest) средства toogenerate SDK из нашего файла Swagger.</span><span class="sxs-lookup"><span data-stu-id="65652-105">We recommend using hello [AutoRest](https://github.com/Azure/AutoRest) tool toogenerate your SDK from our Swagger file.</span></span>

> [!NOTE]
> <span data-ttu-id="65652-106">Служба Azure Mobile Engagement Hello будет прекращено 2018 марта и в настоящее время только доступные tooexisting клиентов.</span><span class="sxs-lookup"><span data-stu-id="65652-106">hello Azure Mobile Engagement service will be retired March 2018 and is currently only available tooexisting customers.</span></span> <span data-ttu-id="65652-107">Дополнительные сведения см. на странице [Службы мобильного взаимодействия](https://azure.microsoft.com/en-us/services/mobile-engagement/).</span><span class="sxs-lookup"><span data-stu-id="65652-107">For more information, see [Mobile Engagement](https://azure.microsoft.com/en-us/services/mobile-engagement/).</span></span>

<span data-ttu-id="65652-108">Мы создали таким же способом, что позволяет вам toointeract с этими интерфейсами API с помощью оболочки C# .NET SDK, и у вас нет toodo hello согласование маркера проверки подлинности и обновите самостоятельно.</span><span class="sxs-lookup"><span data-stu-id="65652-108">We have created a .NET SDK in a similar manner which allows you toointeract with these APIs using a C# wrapper and you don't have toodo hello authentication token negotiation and refresh yourself.</span></span>  

<span data-ttu-id="65652-109">В этом примере проходит через набор hello hello toouse toofollow действия .NET SDK:</span><span class="sxs-lookup"><span data-stu-id="65652-109">This sample goes through hello set of steps toofollow toouse hello .NET SDK:</span></span>

1. <span data-ttu-id="65652-110">Во-первых, вам требуется проверка подлинности hello toosetup для hello собственные интерфейсы API с помощью Azure Active Directory, как описано [здесь](mobile-engagement-api-authentication.md#authentication).</span><span class="sxs-lookup"><span data-stu-id="65652-110">First of all, you need toosetup hello authentication for your APIs using hello Azure Active Directory as described [here](mobile-engagement-api-authentication.md#authentication).</span></span> <span data-ttu-id="65652-111">По завершении этих шагов hello, должен иметь допустимое **SubscriptionId**, **TenantId**, **ApplicationId** и **секрет**.</span><span class="sxs-lookup"><span data-stu-id="65652-111">At hello end of these steps, you should have a valid **SubscriptionId**, **TenantId**, **ApplicationId** and **Secret**.</span></span> 
2. <span data-ttu-id="65652-112">Мы будем использовать простой toodemonstrate приложения консоли Windows, работа с hello .NET SDK с помощью сценария hello создания объявления кампании.</span><span class="sxs-lookup"><span data-stu-id="65652-112">We will use a simple Windows Console app toodemonstrate working with hello .NET SDK with hello scenario of creating an Announcement campaign.</span></span> <span data-ttu-id="65652-113">Откройте Visual Studio и создайте **консольное приложение**.</span><span class="sxs-lookup"><span data-stu-id="65652-113">So open up Visual Studio and create a **Console Application**.</span></span>   
3. <span data-ttu-id="65652-114">Затем следует записать hello toodownload .NET SDK, который доступен в виде **библиотеки управления Microsoft Azure Engagement** в коллекции Nuget hello [здесь](https://www.nuget.org/packages/Microsoft.Azure.Management.Engagement/).</span><span class="sxs-lookup"><span data-stu-id="65652-114">Next you need toodownload hello .NET SDK which is available as **Microsoft Azure Engagement Management Library** in hello Nuget gallery [here](https://www.nuget.org/packages/Microsoft.Azure.Management.Engagement/).</span></span>
   <span data-ttu-id="65652-115">При установке hello Nuget из Visual Studio, необходимо наличие флажки hello tooensure **включить предварительный выпуск** параметр при поиске hello пакета:</span><span class="sxs-lookup"><span data-stu-id="65652-115">If you are installing hello Nuget from Visual Studio, you need tooensure that you have check marked hello **Include prerelease** option while searching for hello package:</span></span>
   
    ![][1]
4. <span data-ttu-id="65652-116">В hello `Program.cs` файл, добавить hello следующие пространства имен:</span><span class="sxs-lookup"><span data-stu-id="65652-116">In hello `Program.cs` file, add hello following namespaces:</span></span>
   
        using Microsoft.Rest.Azure.Authentication;
        using Microsoft.Azure.Management.Engagement;
        using Microsoft.Azure.Management.Engagement.Models;
5. <span data-ttu-id="65652-117">Затем следует записать hello toodefine следующие константы, которые будут использоваться для проверки подлинности и работать с ними Engagement hello мобильного приложения, в котором вы создаете кампании объявления hello:</span><span class="sxs-lookup"><span data-stu-id="65652-117">Next you need toodefine hello following constants that we will use for authentication and interacting with hello Mobile Engagement App in which you are creating hello Announcement campaign:</span></span>
   
        // For authentication
        const string TENANT_ID = "<Your TenantId>";
        const string CLIENT_ID = "<Your Application Id>";
        const string CLIENT_SECRET = "<Your Secret>";
        const string SUBSCRIPTION_ID = "<Your Subscription Id>";
   
        // This is hello Azure Resource group concept for grouping together resources 
        //  see here: https://azure.microsoft.com/en-us/documentation/articles/resource-group-portal/
        const string RESOURCE_GROUP = "";
   
        // For Mobile Engagement operations
        // App Collection Name 
        const string APP_COLLECTION_NAME = "";
        // Application Resource Name - make sure you are using hello one as specified in hello Azure portal (NOT hello App Name)
        const string APP_RESOURCE_NAME = "";
6. <span data-ttu-id="65652-118">Определение hello `EngagementManagementClient` переменную, которая будет использоваться toocall hello пакет SDK Mobile Engagement методов:</span><span class="sxs-lookup"><span data-stu-id="65652-118">Define hello `EngagementManagementClient` variable which we will use toocall hello Mobile Engagement SDK methods:</span></span>
   
        static EngagementManagementClient engagementClient; 
7. <span data-ttu-id="65652-119">Добавьте следующие tooyour hello `Main` метод:</span><span class="sxs-lookup"><span data-stu-id="65652-119">Add hello following tooyour `Main` method:</span></span>
   
        try
            {
                // Initialize hello Engagement SDK toocall out APIs. 
                InitEngagementClient().Wait();
   
                // Create a Reach campaign
                CreateCampaign().Wait();
            }
            catch (Exception ex)
            {
                Console.WriteLine(ex.InnerException.Message);
                throw ex;
            }
8. <span data-ttu-id="65652-120">Определить следующий метод, который отвечает за инициализацию hello hello `EngagementManagementClient` , сначала проверки подлинности и затем связывая себя с помощью Engagement hello мобильного приложения, в котором вы планируете кампании объявления hello toocreate:</span><span class="sxs-lookup"><span data-stu-id="65652-120">Define hello following method which takes care of initializing hello `EngagementManagementClient` by first authenticating and then associating itself with hello Mobile Engagement App in which you plan toocreate hello Announcement campaign:</span></span>
   
        private static async Task InitEngagementClient()
        {
            var credentials = await ApplicationTokenProvider.LoginSilentAsync(TENANT_ID, CLIENT_ID, CLIENT_SECRET);
            engagementClient = new EngagementManagementClient(credentials) { SubscriptionId = SUBSCRIPTION_ID };
   
            // This is hello Azure concept of ResourceGroup
            engagementClient.ResourceGroupName = RESOURCE_GROUP;
   
            // This is your Mobile Engagement App Collection & App Resource Name in which you create hello campaign
            engagementClient.AppCollection = APP_COLLECTION_NAME;
            engagementClient.AppName = APP_RESOURCE_NAME;
        }
   
   > [!IMPORTANT]
   > <span data-ttu-id="65652-121">Обратите внимание, что toouse hello **имя ресурса приложения** , определенный в портале управления Azure hello параметр AppName hello.</span><span class="sxs-lookup"><span data-stu-id="65652-121">Note that you need toouse hello **App Resource Name** as defined in hello Azure management portal for hello AppName parameter.</span></span> 
   > 
   > 
9. <span data-ttu-id="65652-122">Наконец, определите hello CreateCampaign метод, который берет на себя с помощью toocreate EngagementClient hello ранее инициализирован простой **в любое время** & **только уведомления** кампании с заголовком и сообщение:</span><span class="sxs-lookup"><span data-stu-id="65652-122">Lastly, define hello CreateCampaign method which will take care of using hello previously initialized EngagementClient toocreate a simple **AnyTime** & **Notification-only** campaign with a title and message:</span></span> 
   
        private async static Task CreateCampaign()
        {
            //  Refer toohello Announcement Campaign format from here - 
            //      https://msdn.microsoft.com/en-us/library/azure/mt683751.aspx
            // Make sure you are passing all hello non-optional parameters
            Campaign parameters = new Campaign(
                name:"WelcomeCampaign",
                notificationTitle: "Welcome", 
                notificationMessage: "Thank you for installing hello app!",
                type:"only_notif",
                deliveryTime:"any"
                );
   
            // Refer toohello Campaign Kinds from here - https://msdn.microsoft.com/en-us/library/azure/mt683742.aspx
            CampaignStateResult result = 
                await engagementClient.Campaigns.CreateAsync(CampaignKinds.Announcements, parameters);
            Console.WriteLine("Campaign Id '{0}' was created successfully and it is in '{1}' state", result.Id, result.State);
        }
10. <span data-ttu-id="65652-123">Hello выполнения консольного приложения, чтобы просмотреть следующие hello для успешного создания кампании hello:</span><span class="sxs-lookup"><span data-stu-id="65652-123">Run hello console app and you will see hello following on successful creation of hello campaign:</span></span>
    
    <span data-ttu-id="65652-124">**Кампания с идентификатором 159 успешно создана и находится в состоянии "черновик"**</span><span class="sxs-lookup"><span data-stu-id="65652-124">**Campaign Id '159' was created successfully and it is in 'draft' state**</span></span>

<!-- Images. -->

[1]: ./media/mobile-engagement-dotnet-sdk-service-api/include-prerelease.png
