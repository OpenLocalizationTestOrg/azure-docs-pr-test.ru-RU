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
# <a name="azure-mobile-engagement---api-integration"></a>Службы мобильного взаимодействия Azure — интеграция API
В автоматизированной системы маркетинга Создание и активация hello маркетинговых кампаний, также происходит автоматически. Поэтому Службы мобильного взаимодействия Azure поддерживают создание автоматических маркетинговых кампаний с помощью API. 

Обычно клиенты используют hello мобильного охвата обслуживающего интерфейс toocreate объявления/опросов и т. д как часть их маркетинговых кампаний. Однако как hello маркетинговых кампаний, становятся зрелой, есть ли необходимость tooleverage hello данных заблокирован в серверных системах hello (например, в системе CRM или система управления Содержимым, как SharePoint), чтобы полностью автоматизированное конвейера могут быть созданы в Mobile, которая создает кампании Динамически, основываясь на hello потока данных в систем баз hello обязательств. 

![][5]

Этот учебник переход через такие сценарии, когда бизнес-пользователь SharePoint заполнение маркетинговые данные списка SharePoint, а автоматизированный процесс принимает элементы из списка hello и подключается с использованием системы hello мобильного охвата hello доступные интерфейсы API REST toocreate маркетинговой кампании на основе данных SharePoint hello. 

> [!IMPORTANT]
> Как правило можно использовать в этом примере в качестве отправной точки для понимания того, как toocall любой Mobile Engagement API-интерфейса REST, подробно описываются два ключевых аспекта hello вызова hello API-интерфейсов - проверки подлинности и передача параметров. 
> 
> 

## <a name="sharepoint-integration"></a>Интеграция с SharePoint
1. Ниже приведен пример какие hello выглядит списка SharePoint. **Заголовок**, **категории**, **NotificationTitle**, **сообщение** и **URL-адрес** используются для создания объявления «hello». Имеется столбец с именем **IsProcessed** используемой процесса автоматизации образец hello в форме hello консольную программу. Вы может выполнять Эта консольная программа как веб-задание Azure таким образом, вы можете запланировать или можно напрямую использовать tooprogram hello SharePoint рабочий процесс создания и активации объявления «hello» при вставке элемента в списке SharePoint hello. В этом примере мы используем hello консольная программа, который переходит по элементам hello hello SharePoint списка и создать объявление в Azure Mobile Engagement для каждого из них и в заключение отмечает hello **IsProcessed** флаг toobe значение true, если Создание объявления успешно.
   
    ![][1]
2. Мы используем hello кода из образца hello *удаленной проверки подлинности в SharePoint Online с помощью hello клиентской объектной модели* [здесь](https://code.msdn.microsoft.com/Remote-Authentication-in-b7b6f43c) tooauthenticate со списком SharePoint hello.
3. Пройдя проверку подлинности, выполнение цикла через hello toofind элементы списка элементов, созданный (который будет иметь **IsProcessed** = false). 
   
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

## <a name="mobile-engagement-integration"></a>Интеграция со Службами мобильного взаимодействия
1. После мы найти элемент, который требуется обработка — извлечь hello сведения, необходимые toocreate объявления из hello элемент списка и вызвать `CreateAzMECampaign` toocreate его и впоследствии `ActivateAzMECampaign` tooactivate его. Это по сути вызов внутреннего сервера мобильного охвата toohello вызовы REST API. 
2. Hello API-интерфейс REST Mobile Engagement требуют **заголовок авторизации HTTP схемы Обычная проверка подлинности** состоящему из hello `ApplicationId` и hello `ApiKey` получить из hello портал Azure. Убедитесь, что вы используете hello ключ из hello **ключи api** раздел и *не* из hello **ключи sdk** раздела. 
   
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
3. Для создания типа объявления hello Кампания — ссылаться toohello [документации](https://msdn.microsoft.com/library/azure/mt683750.aspx). Необходимо убедиться, что вы указали кампании hello toomake `kind` как *объявления* и hello [полезных данных](https://msdn.microsoft.com/library/azure/mt683751.aspx) и передачи его в качестве FormUrlEncodedContent. 
   
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
4. После создания объявления «hello», вы увидите нечто похожее на портал мобильного охвата hello hello (Обратите внимание, что hello состояние = черновик и Activated = н/д)
   
    ![][3]
5. `CreateAzMECampaign`Создает объявление кампании и возвращает вызывающему объекту toohello идентификатор. `ActivateAzMECampaign`требуется этот идентификатор в качестве hello параметр tooactivate hello кампании. 
   
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
6. После активации объявления «hello» на портале мобильного охвата hello появится примерно hello следующим образом:
   
    ![][4]
7. Сразу после активации кампании hello возвращает какие-либо устройства, которые удовлетворяют критерию hello кампании hello начнется видеть уведомления. 
8. Вы также заметите пометить этот элемент списка hello с IsProcessed = false установил tooTrue после создания кампании объявления hello.  

В этом примере создается простой объявления кампании, указав основном hello необходимые свойства. Этот параметр можно изменить так же, как можно с портала hello, используя сведения о hello [здесь](https://msdn.microsoft.com/library/azure/mt683751.aspx). 

<!-- Images. -->
[1]: ./media/mobile-engagement-sample-backend-integration-sharepoint/sharepointlist.png
[2]: ./media/mobile-engagement-sample-backend-integration-sharepoint/properties.png
[3]: ./media/mobile-engagement-sample-backend-integration-sharepoint/new-announcement.png
[4]: ./media/mobile-engagement-sample-backend-integration-sharepoint/activate-announcement.png
[5]: ./media/mobile-engagement-sample-backend-integration-sharepoint/diagram.png



