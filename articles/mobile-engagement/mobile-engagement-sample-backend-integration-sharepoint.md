---
title: "Службы мобильного взаимодействия Azure — интеграция с серверной частью"
description: "Подключите Службы мобильного взаимодействия Azure к серверной части SharePoint для создания кампаний из SharePoint."
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 06297b43-579f-46e6-8a58-961a68f9aa09
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-multiple
ms.devlang: dotnet
ms.topic: article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: d49f1094f4c3f170f3618f3e19e42266f9ae8858
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="azure-mobile-engagement---api-integration"></a><span data-ttu-id="67618-103">Службы мобильного взаимодействия Azure — интеграция API</span><span class="sxs-lookup"><span data-stu-id="67618-103">Azure Mobile Engagement - API integration</span></span>
<span data-ttu-id="67618-104">В автоматизированной системе маркетинга создание и активация маркетинговых кампаний также происходит автоматически.</span><span class="sxs-lookup"><span data-stu-id="67618-104">In an automated marketing system, creating and activating the marketing campaigns also occur automatically.</span></span> <span data-ttu-id="67618-105">Поэтому Службы мобильного взаимодействия Azure поддерживают создание автоматических маркетинговых кампаний с помощью API.</span><span class="sxs-lookup"><span data-stu-id="67618-105">For this purpose - Azure Mobile Engagement enables creating such automated marketing campaigns using APIs as well.</span></span> 

<span data-ttu-id="67618-106">Как правило, для создания объявлений и опросов в рамках маркетинговых кампаний клиенты используют интерфейсную часть решений.</span><span class="sxs-lookup"><span data-stu-id="67618-106">Typically customers use the Mobile Engagement front end interface to create announcements/polls etc as part of their marketing campaigns.</span></span> <span data-ttu-id="67618-107">Однако по мере того как маркетинговые кампании становятся более зрелыми, возникает необходимость использовать данные серверной части (например, из CRM или систем управления контентом, таких как SharePoint). Они позволяют полностью автоматизировать динамическое создание кампаний в Службах мобильного взаимодействия на основе данных, поступающих из серверных систем.</span><span class="sxs-lookup"><span data-stu-id="67618-107">However as the marketing campaigns become mature, there is a need to leverage the data locked in the backend systems (like any CRM system or CMS system like SharePoint) so that a fully automated pipeline can be created which creates campaigns in Mobile Engagement dynamically based on the data flowing in from the backend systems.</span></span> 

![][5]

<span data-ttu-id="67618-108">В этом учебнике рассматривается сценарий, в котором бизнес-пользователь SharePoint вносит маркетинговые данные в список SharePoint, а автоматизированный процесс извлекает элементы из списка и, используя интерфейсы API REST, подключается к системе Служб мобильного взаимодействия для создания маркетинговой кампании на основе данных SharePoint.</span><span class="sxs-lookup"><span data-stu-id="67618-108">This tutorial goes through such a scenario where a SharePoint business user populates a SharePoint list with marketing data and an automated process picks up items from the list and connects with the Mobile Engagement system using the available REST APIs to create a marketing campaign from the SharePoint data.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="67618-109">Вы можете использовать приведенный пример в качестве отправной точки для изучения принципов работы любого интерфейса API REST для Служб мобильного взаимодействия, так как здесь подробно рассматриваются два ключевых аспекта вызова API: проверка подлинности и передача параметров.</span><span class="sxs-lookup"><span data-stu-id="67618-109">In general, you can use this sample as a starting point for understanding how to call any Mobile Engagement REST API as it details the two key aspects of calling the APIs - authenticating and passing parameters.</span></span> 
> 
> 

## <a name="sharepoint-integration"></a><span data-ttu-id="67618-110">Интеграция с SharePoint</span><span class="sxs-lookup"><span data-stu-id="67618-110">SharePoint integration</span></span>
1. <span data-ttu-id="67618-111">Вот как выглядит учебный список SharePoint.</span><span class="sxs-lookup"><span data-stu-id="67618-111">Here is what the sample SharePoint list looks like.</span></span> <span data-ttu-id="67618-112">Для создания объявления используются параметры **Title** (Заголовок), **Category** (Категория), **NotificationTitle** (Заголовок уведомления), **Message** (Сообщение) и **URL** (URL-адрес).</span><span class="sxs-lookup"><span data-stu-id="67618-112">**Title**, **Category**, **NotificationTitle**, **Message** and **URL** are used for creating the announcement.</span></span> <span data-ttu-id="67618-113">Также есть столбец **IsProcessed** (обработано), используемый нашим процессом автоматизации в консольной программе.</span><span class="sxs-lookup"><span data-stu-id="67618-113">There is a column called **IsProcessed** which is used by the sample automation process in the form of a console program.</span></span> <span data-ttu-id="67618-114">Можно запустить консольную программу как веб-задание Azure (в этом случае вы сможете планировать ее запуск) или использовать рабочий процесс SharePoint напрямую для программного создания и активации объявлений при вставке элемента в список SharePoint.</span><span class="sxs-lookup"><span data-stu-id="67618-114">You can either run this console program as an Azure WebJob so that you can schedule it or you can directly use the SharePoint workflow to program creating and activating the announcement when an item is inserted into the SharePoint list.</span></span> <span data-ttu-id="67618-115">В этом примере мы используем консольную программу, которая перебирает элементы в списке SharePoint, создает объявление в Службах мобильного взаимодействия Azure для каждого из них, а затем устанавливает флаг **IsProcessed** для подтверждения успешно созданных объявлений.</span><span class="sxs-lookup"><span data-stu-id="67618-115">In this sample we use the console program which goes through the items in the SharePoint list and create announcement in Azure Mobile Engagement for each of them and then finally marks the **IsProcessed** flag to be true on successful announcement creation.</span></span>
   
    ![][1]
2. <span data-ttu-id="67618-116">Для проверки подлинности при работе со списком SharePoint мы будем использовать код из примера *Удаленная проверка подлинности в SharePoint Online с помощью модели COM* [этой ссылке](https://code.msdn.microsoft.com/Remote-Authentication-in-b7b6f43c) .</span><span class="sxs-lookup"><span data-stu-id="67618-116">We are using the code from the sample *Remote Authentication in SharePoint Online Using the Client Object Model* [here](https://code.msdn.microsoft.com/Remote-Authentication-in-b7b6f43c) to authenticate with the SharePoint list.</span></span>
3. <span data-ttu-id="67618-117">После проверки подлинности мы зациклим перебор элементов списка, чтобы выявлять вновь добавленные элементы (флаг **IsProcessed** = false).</span><span class="sxs-lookup"><span data-stu-id="67618-117">Once authenticated, we loop through the list items to find out any newly created items (which will have **IsProcessed** = false).</span></span> 
   
         static async void CreateCampaignFromSharepoint()
        {
            using (ClientContext clientContext = ClaimClientContext.GetAuthenticatedContext(targetSharepointSite))
            {
                // Using https://code.msdn.microsoft.com/Remote-Authentication-in-b7b6f43c for authentication     
                Web site = clientContext.Web;
                List list = site.Lists.GetByTitle("VideoContent");
                CamlQuery query = new CamlQuery();
                query.ViewXml = "<View/>";
                ListItemCollection items = list.GetItems(query);
   
                // Load the SharePoint list
                clientContext.Load(list);
                clientContext.Load(items);
                clientContext.ExecuteQuery();
   
                // Loop through the list to go through all the items which are newly added
                foreach (ListItem item in items)
                    if (item["IsProcessed"].ToString() != "Yes")
                    {
                        string name = item["Title"].ToString();
                        string notificationTitle = item["NotificationTitle"].ToString();
                        string notificationMessage = item["Message"].ToString();
                        string category = item["Category"].ToString();
                        string actionURL = ((FieldUrlValue)item["URL"]).Url;
   
                        // Send an HTTP request to create AzME campaign
                        int campaignId = CreateAzMECampaign
                            (name, notificationTitle, notificationMessage, category, actionURL).Result;
   
                        if (campaignId != -1)
                        {
                            // If creating campaign is successful then set this to true
                            item["IsProcessed"] = "Yes";
   
                            // Now try to activate the campaign also
                            await ActivateAzMECampaign(campaignId);
                        }
                        else
                        {
                            item["IsProcessed"] = "Error";
                        }
                        item.Update();
                    }
                clientContext.ExecuteQuery();
            }
        }

## <a name="mobile-engagement-integration"></a><span data-ttu-id="67618-118">Интеграция со Службами мобильного взаимодействия</span><span class="sxs-lookup"><span data-stu-id="67618-118">Mobile Engagement integration</span></span>
1. <span data-ttu-id="67618-119">Когда мы найдем элемент списка, требующий обработки, мы извлечем из него сведения, необходимые для создания объявления, и вызовем `CreateAzMECampaign`, чтобы создать его, а затем `ActivateAzMECampaign` — чтобы активировать.</span><span class="sxs-lookup"><span data-stu-id="67618-119">Once we find an item which requires processing - we extract the information required to create an announcement from the list item and call `CreateAzMECampaign` to create it and subsequently `ActivateAzMECampaign` to activate it.</span></span> <span data-ttu-id="67618-120">Фактически это вызовы API REST к серверной части Служб мобильного взаимодействия.</span><span class="sxs-lookup"><span data-stu-id="67618-120">These are essentially REST API calls calling to the Mobile Engagement backend.</span></span> 
2. <span data-ttu-id="67618-121">Для интерфейсов REST API для Служб мобильного взаимодействия требуется **HTTP-заголовок авторизации базовой схемы проверки подлинности**, состоящий из компонентов `ApplicationId` и `ApiKey`, которые можно найти на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="67618-121">The Mobile Engagement REST APIs require a **Basic auth scheme authorization HTTP header** which is composed of the `ApplicationId` and the `ApiKey` which you get from the Azure portal.</span></span> <span data-ttu-id="67618-122">Убедитесь, что вы используете ключ из раздела **api keys** (а *не* из раздела **sdk keys**).</span><span class="sxs-lookup"><span data-stu-id="67618-122">Make sure that you are using the Key from the **api keys** section and *not* from the **sdk keys** section.</span></span> 
   
   ![][2]
   
       static string CreateAuthZHeader()
       {
           string BasicAuthzHeaderString = "Basic " + EncodeTo64(ApplicationId + ":" + ApiKey);
           return BasicAuthzHeaderString;
       }
   
       static public string EncodeTo64(string toEncode)
       {
           byte[] toEncodeAsBytes = System.Text.ASCIIEncoding.ASCII.GetBytes(toEncode);
           string returnValue = System.Convert.ToBase64String(toEncodeAsBytes);
           return returnValue;
       }  
3. <span data-ttu-id="67618-123">Сведения о создании кампаний с типом announcement (Объявление) см. в [документации](https://msdn.microsoft.com/library/azure/mt683750.aspx).</span><span class="sxs-lookup"><span data-stu-id="67618-123">For creating the announcement type campaign - refer to the [documentation](https://msdn.microsoft.com/library/azure/mt683750.aspx).</span></span> <span data-ttu-id="67618-124">Убедитесь, что для параметра `kind` кампании вы задаете значение *announcement* и передаете его вместе с [дополнительными параметрами](https://msdn.microsoft.com/library/azure/mt683751.aspx) в виде FormUrlEncodedContent.</span><span class="sxs-lookup"><span data-stu-id="67618-124">You need to make sure that you are specifying the campaign `kind` as *announcement* and the [payload](https://msdn.microsoft.com/library/azure/mt683751.aspx) and passing it as FormUrlEncodedContent.</span></span> 
   
        static async Task<int> CreateAzMECampaign(string campaignName, string notificationTitle, 
            string notificationMessage, string notificationCategory, string actionURL)
        {
            string createURIFragment = "/reach/1/create";
   
            using (var client = new HttpClient())
            {
                // Add Authorization Header
                client.DefaultRequestHeaders.TryAddWithoutValidation("Authorization", CreateAuthZHeader());
   
                // Create the payload to send the content
                // Reference -> https://msdn.microsoft.com/library/dn913749.aspx
                string data =
                    @"{""name"":""" + campaignName + @"""," + 
                    @"""type"":""only_notif""," + 
                    @"""deliveryTime"":""any"","" + 
                    @""notificationTitle"":""" + notificationTitle + 
                    @""",""notificationMessage"":""" + notificationMessage + 
                    @""",""actionUrl"":""" + actionURL + @"""}";
   
                var content = new FormUrlEncodedContent(new[] 
                {
                    new KeyValuePair<string, string>("kind", "announcement"),
                    new KeyValuePair<string, string>("data", data),
                });
   
                // Send the POST request
                var response = await client.PostAsync(url + createURIFragment, content);
                var responseString = response.Content.ReadAsStringAsync().Result;
                int campaignId = -1;
                if (response.StatusCode.ToString() == "OK")
                {
                    // This is the campaign id
                    campaignId = Convert.ToInt32(responseString);
                    Console.WriteLine("Campaign successfully created with id {0}", campaignId);
                }
                else
                {
                    Console.WriteLine("Campaign creation failed with error - '{0}'", responseString);
                }
                return campaignId;
            }
        }
4. <span data-ttu-id="67618-125">После создания объявления вы увидите на портале Служб мобильного взаимодействия примерно следующее (обратите внимание что параметр State (состояние) имеет значение Draft (черновик), а Activated (статус активации) — N/A (недоступно)).</span><span class="sxs-lookup"><span data-stu-id="67618-125">Once you have the announcement created, you will see something like the following on the Mobile Engagement portal (note that the State=Draft and Activated = N/A)</span></span>
   
    ![][3]
5. <span data-ttu-id="67618-126">`CreateAzMECampaign` создает кампанию с типом «Объявление» и возвращает ее идентификатор.</span><span class="sxs-lookup"><span data-stu-id="67618-126">`CreateAzMECampaign` creates an announcement campaign and returns its Id to the caller.</span></span> <span data-ttu-id="67618-127">`ActivateAzMECampaign` в качестве параметра для активации кампании.</span><span class="sxs-lookup"><span data-stu-id="67618-127">`ActivateAzMECampaign` requires this Id as the parameter to activate the campaign.</span></span> 
   
        static async Task<bool> ActivateAzMECampaign(int campaignId)
        {
            string activateUriFragment = "/reach/1/activate";
            using (var client = new HttpClient())
            {
                // Add Authorization Header
                client.DefaultRequestHeaders.TryAddWithoutValidation("Authorization", CreateAuthZHeader());
   
                var content = new FormUrlEncodedContent(new[] 
                {
                    new KeyValuePair<string, string>("kind", "announcement"),
                    new KeyValuePair<string, string>("id", campaignId.ToString()),
                });
   
                // Send the POST request
                var response = await client.PostAsync(url + activateUriFragment, content);
                var responseString = response.Content.ReadAsStringAsync().Result;
                if (response.StatusCode.ToString() == "OK")
                {
                    Console.WriteLine("Campaign successfully activated");
                    return true;
                }
                else
                {
                    Console.WriteLine("Campaign activation failed with error - '{0}'", responseString);
                    return false;
                }
            }
        }
6. <span data-ttu-id="67618-128">После активации объявления вы увидите на портале Служб мобильного взаимодействия примерно следующее.</span><span class="sxs-lookup"><span data-stu-id="67618-128">Once you have the announcement activated, you will see something like the following on the Mobile Engagement portal:</span></span>
   
    ![][4]
7. <span data-ttu-id="67618-129">Сразу после активации кампании все устройства, которые удовлетворяют ее критериям, начнут получать уведомления.</span><span class="sxs-lookup"><span data-stu-id="67618-129">As soon as the campaign gets activated, any devices which satisfy the criterion on the campaign will start seeing notifications.</span></span> 
8. <span data-ttu-id="67618-130">Вы также заметите, что после создания кампании значение флага IsProcessed рассматриваемого элемента списка изменится на True.</span><span class="sxs-lookup"><span data-stu-id="67618-130">You will also notice that the list item marked with IsProcessed = false has been set to True once the announcement campaign is created.</span></span>  

<span data-ttu-id="67618-131">В этом примере создается простая кампания с типом «Объявление», в которой указываются в основном обязательные свойства.</span><span class="sxs-lookup"><span data-stu-id="67618-131">This sample created a simple announcement campaign specifying mostly the required properties.</span></span> <span data-ttu-id="67618-132">Вы можете изменить ее на портале, используя сведения [с этой страницы](https://msdn.microsoft.com/library/azure/mt683751.aspx).</span><span class="sxs-lookup"><span data-stu-id="67618-132">You can customize this as much as you can from the portal by using the information [here](https://msdn.microsoft.com/library/azure/mt683751.aspx).</span></span> 

<!-- Images. -->
[1]: ./media/mobile-engagement-sample-backend-integration-sharepoint/sharepointlist.png
[2]: ./media/mobile-engagement-sample-backend-integration-sharepoint/properties.png
[3]: ./media/mobile-engagement-sample-backend-integration-sharepoint/new-announcement.png
[4]: ./media/mobile-engagement-sample-backend-integration-sharepoint/activate-announcement.png
[5]: ./media/mobile-engagement-sample-backend-integration-sharepoint/diagram.png



