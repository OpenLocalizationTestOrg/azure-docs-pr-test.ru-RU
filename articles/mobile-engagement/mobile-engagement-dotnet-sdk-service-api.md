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
# <a name="using-net-sdk-tooaccess-azure-mobile-engagement-service-apis"></a>С помощью пакета SDK для .NET tooaccess API-интерфейсы службы Azure Mobile Engagement
Azure Mobile Engagement предоставляет набор API-интерфейсов для вас toomanage устройств Reach/принудительной кампании toointeract т. д. с этими интерфейсами API, мы предлагаем вам [файл Swagger](https://github.com/Azure/azure-rest-api-specs/blob/master/arm-mobileengagement/2014-12-01/swagger/mobile-engagement.json) , можно использовать с средств toogenerate пакеты SDK для предпочитаемого язык. Мы рекомендуем использовать hello [AutoRest](https://github.com/Azure/AutoRest) средства toogenerate SDK из нашего файла Swagger.

> [!NOTE]
> Служба Azure Mobile Engagement Hello будет прекращено 2018 марта и в настоящее время только доступные tooexisting клиентов. Дополнительные сведения см. на странице [Службы мобильного взаимодействия](https://azure.microsoft.com/en-us/services/mobile-engagement/).

Мы создали таким же способом, что позволяет вам toointeract с этими интерфейсами API с помощью оболочки C# .NET SDK, и у вас нет toodo hello согласование маркера проверки подлинности и обновите самостоятельно.  

В этом примере проходит через набор hello hello toouse toofollow действия .NET SDK:

1. Во-первых, вам требуется проверка подлинности hello toosetup для hello собственные интерфейсы API с помощью Azure Active Directory, как описано [здесь](mobile-engagement-api-authentication.md#authentication). По завершении этих шагов hello, должен иметь допустимое **SubscriptionId**, **TenantId**, **ApplicationId** и **секрет**. 
2. Мы будем использовать простой toodemonstrate приложения консоли Windows, работа с hello .NET SDK с помощью сценария hello создания объявления кампании. Откройте Visual Studio и создайте **консольное приложение**.   
3. Затем следует записать hello toodownload .NET SDK, который доступен в виде **библиотеки управления Microsoft Azure Engagement** в коллекции Nuget hello [здесь](https://www.nuget.org/packages/Microsoft.Azure.Management.Engagement/).
   При установке hello Nuget из Visual Studio, необходимо наличие флажки hello tooensure **включить предварительный выпуск** параметр при поиске hello пакета:
   
    ![][1]
4. В hello `Program.cs` файл, добавить hello следующие пространства имен:
   
        using Microsoft.Rest.Azure.Authentication;
        using Microsoft.Azure.Management.Engagement;
        using Microsoft.Azure.Management.Engagement.Models;
5. Затем следует записать hello toodefine следующие константы, которые будут использоваться для проверки подлинности и работать с ними Engagement hello мобильного приложения, в котором вы создаете кампании объявления hello:
   
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
6. Определение hello `EngagementManagementClient` переменную, которая будет использоваться toocall hello пакет SDK Mobile Engagement методов:
   
        static EngagementManagementClient engagementClient; 
7. Добавьте следующие tooyour hello `Main` метод:
   
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
8. Определить следующий метод, который отвечает за инициализацию hello hello `EngagementManagementClient` , сначала проверки подлинности и затем связывая себя с помощью Engagement hello мобильного приложения, в котором вы планируете кампании объявления hello toocreate:
   
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
   > Обратите внимание, что toouse hello **имя ресурса приложения** , определенный в портале управления Azure hello параметр AppName hello. 
   > 
   > 
9. Наконец, определите hello CreateCampaign метод, который берет на себя с помощью toocreate EngagementClient hello ранее инициализирован простой **в любое время** & **только уведомления** кампании с заголовком и сообщение: 
   
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
10. Hello выполнения консольного приложения, чтобы просмотреть следующие hello для успешного создания кампании hello:
    
    **Кампания с идентификатором 159 успешно создана и находится в состоянии "черновик"**

<!-- Images. -->

[1]: ./media/mobile-engagement-dotnet-sdk-service-api/include-prerelease.png
