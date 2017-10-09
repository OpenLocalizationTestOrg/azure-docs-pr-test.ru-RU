---
title: "aaaAzure мобильного охвата - интеграции серверной части"
description: "Подключение Azure Mobile Engagement с серверной части для SharePoint toocreate кампании из SharePoint"
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
ms.openlocfilehash: 89e1ef57db607d63c326a760b20260ad439f08b2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-mobile-engagement---api-integration"></a><span data-ttu-id="50ed9-103">Службы мобильного взаимодействия Azure — интеграция API</span><span class="sxs-lookup"><span data-stu-id="50ed9-103">Azure Mobile Engagement - API integration</span></span>
<span data-ttu-id="50ed9-104">В автоматизированной системы маркетинга Создание и активация hello маркетинговых кампаний, также происходит автоматически.</span><span class="sxs-lookup"><span data-stu-id="50ed9-104">In an automated marketing system, creating and activating hello marketing campaigns also occur automatically.</span></span> <span data-ttu-id="50ed9-105">Поэтому Службы мобильного взаимодействия Azure поддерживают создание автоматических маркетинговых кампаний с помощью API.</span><span class="sxs-lookup"><span data-stu-id="50ed9-105">For this purpose - Azure Mobile Engagement enables creating such automated marketing campaigns using APIs as well.</span></span> 

<span data-ttu-id="50ed9-106">Обычно клиенты используют hello мобильного охвата обслуживающего интерфейс toocreate объявления/опросов и т. д как часть их маркетинговых кампаний.</span><span class="sxs-lookup"><span data-stu-id="50ed9-106">Typically customers use hello Mobile Engagement front end interface toocreate announcements/polls etc as part of their marketing campaigns.</span></span> <span data-ttu-id="50ed9-107">Однако как hello маркетинговых кампаний, становятся зрелой, есть ли необходимость tooleverage hello данных заблокирован в серверных системах hello (например, в системе CRM или система управления Содержимым, как SharePoint), чтобы полностью автоматизированное конвейера могут быть созданы в Mobile, которая создает кампании Динамически, основываясь на hello потока данных в систем баз hello обязательств.</span><span class="sxs-lookup"><span data-stu-id="50ed9-107">However as hello marketing campaigns become mature, there is a need tooleverage hello data locked in hello backend systems (like any CRM system or CMS system like SharePoint) so that a fully automated pipeline can be created which creates campaigns in Mobile Engagement dynamically based on hello data flowing in from hello backend systems.</span></span> 

![][5]

<span data-ttu-id="50ed9-108">Этот учебник переход через такие сценарии, когда бизнес-пользователь SharePoint заполнение маркетинговые данные списка SharePoint, а автоматизированный процесс принимает элементы из списка hello и подключается с использованием системы hello мобильного охвата hello доступные интерфейсы API REST toocreate маркетинговой кампании на основе данных SharePoint hello.</span><span class="sxs-lookup"><span data-stu-id="50ed9-108">This tutorial goes through such a scenario where a SharePoint business user populates a SharePoint list with marketing data and an automated process picks up items from hello list and connects with hello Mobile Engagement system using hello available REST APIs toocreate a marketing campaign from hello SharePoint data.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="50ed9-109">Как правило можно использовать в этом примере в качестве отправной точки для понимания того, как toocall любой Mobile Engagement API-интерфейса REST, подробно описываются два ключевых аспекта hello вызова hello API-интерфейсов - проверки подлинности и передача параметров.</span><span class="sxs-lookup"><span data-stu-id="50ed9-109">In general, you can use this sample as a starting point for understanding how toocall any Mobile Engagement REST API as it details hello two key aspects of calling hello APIs - authenticating and passing parameters.</span></span> 
> 
> 

## <a name="sharepoint-integration"></a><span data-ttu-id="50ed9-110">Интеграция с SharePoint</span><span class="sxs-lookup"><span data-stu-id="50ed9-110">SharePoint integration</span></span>
1. <span data-ttu-id="50ed9-111">Ниже приведен пример какие hello выглядит списка SharePoint.</span><span class="sxs-lookup"><span data-stu-id="50ed9-111">Here is what hello sample SharePoint list looks like.</span></span> <span data-ttu-id="50ed9-112">**Заголовок**, **категории**, **NotificationTitle**, **сообщение** и **URL-адрес** используются для создания объявления «hello».</span><span class="sxs-lookup"><span data-stu-id="50ed9-112">**Title**, **Category**, **NotificationTitle**, **Message** and **URL** are used for creating hello announcement.</span></span> <span data-ttu-id="50ed9-113">Имеется столбец с именем **IsProcessed** используемой процесса автоматизации образец hello в форме hello консольную программу.</span><span class="sxs-lookup"><span data-stu-id="50ed9-113">There is a column called **IsProcessed** which is used by hello sample automation process in hello form of a console program.</span></span> <span data-ttu-id="50ed9-114">Вы может выполнять Эта консольная программа как веб-задание Azure таким образом, вы можете запланировать или можно напрямую использовать tooprogram hello SharePoint рабочий процесс создания и активации объявления «hello» при вставке элемента в списке SharePoint hello.</span><span class="sxs-lookup"><span data-stu-id="50ed9-114">You can either run this console program as an Azure WebJob so that you can schedule it or you can directly use hello SharePoint workflow tooprogram creating and activating hello announcement when an item is inserted into hello SharePoint list.</span></span> <span data-ttu-id="50ed9-115">В этом примере мы используем hello консольная программа, который переходит по элементам hello hello SharePoint списка и создать объявление в Azure Mobile Engagement для каждого из них и в заключение отмечает hello **IsProcessed** флаг toobe значение true, если Создание объявления успешно.</span><span class="sxs-lookup"><span data-stu-id="50ed9-115">In this sample we use hello console program which goes through hello items in hello SharePoint list and create announcement in Azure Mobile Engagement for each of them and then finally marks hello **IsProcessed** flag toobe true on successful announcement creation.</span></span>
   
    ![][1]
2. <span data-ttu-id="50ed9-116">Мы используем hello кода из образца hello *удаленной проверки подлинности в SharePoint Online с помощью hello клиентской объектной модели* [здесь](https://code.msdn.microsoft.com/Remote-Authentication-in-b7b6f43c) tooauthenticate со списком SharePoint hello.</span><span class="sxs-lookup"><span data-stu-id="50ed9-116">We are using hello code from hello sample *Remote Authentication in SharePoint Online Using hello Client Object Model* [here](https://code.msdn.microsoft.com/Remote-Authentication-in-b7b6f43c) tooauthenticate with hello SharePoint list.</span></span>
3. <span data-ttu-id="50ed9-117">Пройдя проверку подлинности, выполнение цикла через hello toofind элементы списка элементов, созданный (который будет иметь **IsProcessed** = false).</span><span class="sxs-lookup"><span data-stu-id="50ed9-117">Once authenticated, we loop through hello list items toofind out any newly created items (which will have **IsProcessed** = false).</span></span> 
   
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
   
                // Load hello SharePoint list
                clientContext.Load(list);
                clientContext.Load(items);
                clientContext.ExecuteQuery();
   
                // Loop through hello list toogo through all hello items which are newly added
                foreach (ListItem item in items)
                    if (item["IsProcessed"].ToString() != "Yes")
                    {
                        string name = item["Title"].ToString();
                        string notificationTitle = item["NotificationTitle"].ToString();
                        string notificationMessage = item["Message"].ToString();
                        string category = item["Category"].ToString();
                        string actionURL = ((FieldUrlValue)item["URL"]).Url;
   
                        // Send an HTTP request toocreate AzME campaign
                        int campaignId = CreateAzMECampaign
                            (name, notificationTitle, notificationMessage, category, actionURL).Result;
   
                        if (campaignId != -1)
                        {
                            // If creating campaign is successful then set this tootrue
                            item["IsProcessed"] = "Yes";
   
                            // Now try tooactivate hello campaign also
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

## <a name="mobile-engagement-integration"></a><span data-ttu-id="50ed9-118">Интеграция со Службами мобильного взаимодействия</span><span class="sxs-lookup"><span data-stu-id="50ed9-118">Mobile Engagement integration</span></span>
1. <span data-ttu-id="50ed9-119">После мы найти элемент, который требуется обработка — извлечь hello сведения, необходимые toocreate объявления из hello элемент списка и вызвать `CreateAzMECampaign` toocreate его и впоследствии `ActivateAzMECampaign` tooactivate его.</span><span class="sxs-lookup"><span data-stu-id="50ed9-119">Once we find an item which requires processing - we extract hello information required toocreate an announcement from hello list item and call `CreateAzMECampaign` toocreate it and subsequently `ActivateAzMECampaign` tooactivate it.</span></span> <span data-ttu-id="50ed9-120">Это по сути вызов внутреннего сервера мобильного охвата toohello вызовы REST API.</span><span class="sxs-lookup"><span data-stu-id="50ed9-120">These are essentially REST API calls calling toohello Mobile Engagement backend.</span></span> 
2. <span data-ttu-id="50ed9-121">Hello API-интерфейс REST Mobile Engagement требуют **заголовок авторизации HTTP схемы Обычная проверка подлинности** состоящему из hello `ApplicationId` и hello `ApiKey` получить из hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="50ed9-121">hello Mobile Engagement REST APIs require a **Basic auth scheme authorization HTTP header** which is composed of hello `ApplicationId` and hello `ApiKey` which you get from hello Azure portal.</span></span> <span data-ttu-id="50ed9-122">Убедитесь, что вы используете hello ключ из hello **ключи api** раздел и *не* из hello **ключи sdk** раздела.</span><span class="sxs-lookup"><span data-stu-id="50ed9-122">Make sure that you are using hello Key from hello **api keys** section and *not* from hello **sdk keys** section.</span></span> 
   
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
3. <span data-ttu-id="50ed9-123">Для создания типа объявления hello Кампания — ссылаться toohello [документации](https://msdn.microsoft.com/library/azure/mt683750.aspx).</span><span class="sxs-lookup"><span data-stu-id="50ed9-123">For creating hello announcement type campaign - refer toohello [documentation](https://msdn.microsoft.com/library/azure/mt683750.aspx).</span></span> <span data-ttu-id="50ed9-124">Необходимо убедиться, что вы указали кампании hello toomake `kind` как *объявления* и hello [полезных данных](https://msdn.microsoft.com/library/azure/mt683751.aspx) и передачи его в качестве FormUrlEncodedContent.</span><span class="sxs-lookup"><span data-stu-id="50ed9-124">You need toomake sure that you are specifying hello campaign `kind` as *announcement* and hello [payload](https://msdn.microsoft.com/library/azure/mt683751.aspx) and passing it as FormUrlEncodedContent.</span></span> 
   
        static async Task<int> CreateAzMECampaign(string campaignName, string notificationTitle, 
            string notificationMessage, string notificationCategory, string actionURL)
        {
            string createURIFragment = "/reach/1/create";
   
            using (var client = new HttpClient())
            {
                // Add Authorization Header
                client.DefaultRequestHeaders.TryAddWithoutValidation("Authorization", CreateAuthZHeader());
   
                // Create hello payload toosend hello content
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
   
                // Send hello POST request
                var response = await client.PostAsync(url + createURIFragment, content);
                var responseString = response.Content.ReadAsStringAsync().Result;
                int campaignId = -1;
                if (response.StatusCode.ToString() == "OK")
                {
                    // This is hello campaign id
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
4. <span data-ttu-id="50ed9-125">После создания объявления «hello», вы увидите нечто похожее на портал мобильного охвата hello hello (Обратите внимание, что hello состояние = черновик и Activated = н/д)</span><span class="sxs-lookup"><span data-stu-id="50ed9-125">Once you have hello announcement created, you will see something like hello following on hello Mobile Engagement portal (note that hello State=Draft and Activated = N/A)</span></span>
   
    ![][3]
5. <span data-ttu-id="50ed9-126">`CreateAzMECampaign`Создает объявление кампании и возвращает вызывающему объекту toohello идентификатор.</span><span class="sxs-lookup"><span data-stu-id="50ed9-126">`CreateAzMECampaign` creates an announcement campaign and returns its Id toohello caller.</span></span> <span data-ttu-id="50ed9-127">`ActivateAzMECampaign`требуется этот идентификатор в качестве hello параметр tooactivate hello кампании.</span><span class="sxs-lookup"><span data-stu-id="50ed9-127">`ActivateAzMECampaign` requires this Id as hello parameter tooactivate hello campaign.</span></span> 
   
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
   
                // Send hello POST request
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
6. <span data-ttu-id="50ed9-128">После активации объявления «hello» на портале мобильного охвата hello появится примерно hello следующим образом:</span><span class="sxs-lookup"><span data-stu-id="50ed9-128">Once you have hello announcement activated, you will see something like hello following on hello Mobile Engagement portal:</span></span>
   
    ![][4]
7. <span data-ttu-id="50ed9-129">Сразу после активации кампании hello возвращает какие-либо устройства, которые удовлетворяют критерию hello кампании hello начнется видеть уведомления.</span><span class="sxs-lookup"><span data-stu-id="50ed9-129">As soon as hello campaign gets activated, any devices which satisfy hello criterion on hello campaign will start seeing notifications.</span></span> 
8. <span data-ttu-id="50ed9-130">Вы также заметите пометить этот элемент списка hello с IsProcessed = false установил tooTrue после создания кампании объявления hello.</span><span class="sxs-lookup"><span data-stu-id="50ed9-130">You will also notice that hello list item marked with IsProcessed = false has been set tooTrue once hello announcement campaign is created.</span></span>  

<span data-ttu-id="50ed9-131">В этом примере создается простой объявления кампании, указав основном hello необходимые свойства.</span><span class="sxs-lookup"><span data-stu-id="50ed9-131">This sample created a simple announcement campaign specifying mostly hello required properties.</span></span> <span data-ttu-id="50ed9-132">Этот параметр можно изменить так же, как можно с портала hello, используя сведения о hello [здесь](https://msdn.microsoft.com/library/azure/mt683751.aspx).</span><span class="sxs-lookup"><span data-stu-id="50ed9-132">You can customize this as much as you can from hello portal by using hello information [here](https://msdn.microsoft.com/library/azure/mt683751.aspx).</span></span> 

<!-- Images. -->
[1]: ./media/mobile-engagement-sample-backend-integration-sharepoint/sharepointlist.png
[2]: ./media/mobile-engagement-sample-backend-integration-sharepoint/properties.png
[3]: ./media/mobile-engagement-sample-backend-integration-sharepoint/new-announcement.png
[4]: ./media/mobile-engagement-sample-backend-integration-sharepoint/activate-announcement.png
[5]: ./media/mobile-engagement-sample-backend-integration-sharepoint/diagram.png



