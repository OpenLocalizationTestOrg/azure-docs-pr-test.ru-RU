---
title: "Настройка личного доменного имени в службе приложений Azure (GoDaddy)"
description: "Узнайте, как использовать доменное имя из GoDaddy с веб-приложениями Azure"
services: app-service
documentationcenter: 
author: erikre
manager: erikre
editor: jimbe
ms.assetid: 33233e30-5846-488f-83f3-b32e5c114564
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/12/2016
ms.author: cephalin
ms.openlocfilehash: 158c5dc06f83e16633d3c2fbb4eb27d3e8af030c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="configure-a-custom-domain-name-in-azure-app-service-purchased-directly-from-godaddy"></a><span data-ttu-id="702fa-103">Настройка личного доменного имени в службе приложений Azure (приобретенного непосредственно у GoDaddy)</span><span class="sxs-lookup"><span data-stu-id="702fa-103">Configure a custom domain name in Azure App Service (Purchased directly from GoDaddy)</span></span>
[!INCLUDE [web-selector](../../includes/websites-custom-domain-selector.md)]

[!INCLUDE [intro](../../includes/custom-dns-web-site-intro.md)]

<span data-ttu-id="702fa-104">Если вы приобрели домен через веб-приложения службы приложений Azure, см. последний шаг процесса [Покупка домена для веб-приложений](custom-dns-web-site-buydomains-web-app.md).</span><span class="sxs-lookup"><span data-stu-id="702fa-104">If you have purchased domain through Azure App Service Web Apps then refer to the final step of [Buy Domain for Web Apps](custom-dns-web-site-buydomains-web-app.md).</span></span>

<span data-ttu-id="702fa-105">В этой статье вы найдете указания по использованию личного доменного имени, приобретенного у [GoDaddy](https://godaddy.com), с использованием [веб-приложений службы приложений](http://go.microsoft.com/fwlink/?LinkId=529714).</span><span class="sxs-lookup"><span data-stu-id="702fa-105">This article provides instructions on using a custom domain name that was purchased directly from [GoDaddy](https://godaddy.com) with [App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714).</span></span>

[!INCLUDE [introfooter](../../includes/custom-dns-web-site-intro-notes.md)]

<a name="understanding-records"></a>

## <a name="understanding-dns-records"></a><span data-ttu-id="702fa-106">Общие сведения о записях DNS</span><span class="sxs-lookup"><span data-stu-id="702fa-106">Understanding DNS records</span></span>
[!INCLUDE [understandingdns](../../includes/custom-dns-web-site-understanding-dns-raw.md)]

<a name="bkmk_configurecname"></a>

## <a name="add-a-dns-record-for-your-custom-domain"></a><span data-ttu-id="702fa-107">Добавление записи DNS для пользовательского домена</span><span class="sxs-lookup"><span data-stu-id="702fa-107">Add a DNS record for your custom domain</span></span>
<span data-ttu-id="702fa-108">Чтобы сопоставить личный домен с веб-приложением в службе приложений, добавьте новую запись в таблицу DNS для этого домена с помощью средств, предоставляемых GoDaddy.</span><span class="sxs-lookup"><span data-stu-id="702fa-108">To associate your custom domain with a web app in App Service, you must add a new entry in the DNS table for your custom domain by using tools provided by GoDaddy.</span></span> <span data-ttu-id="702fa-109">Выполните следующие действия, чтобы найти средства DNS для GoDaddy.com.</span><span class="sxs-lookup"><span data-stu-id="702fa-109">Use the following steps to locate the DNS tools for GoDaddy.com</span></span>

1. <span data-ttu-id="702fa-110">Выполните вход на GoDaddy.com с использованием своей учетной записи и выберите **Моя учетная запись**, а затем — **Управление доменами**.</span><span class="sxs-lookup"><span data-stu-id="702fa-110">Log on to your account with GoDaddy.com, and select **My Account** and then **Manage my domains**.</span></span> <span data-ttu-id="702fa-111">Выберите в раскрывающемся меню доменное имя, которое вы хотите использовать для своего веб-приложения Azure, и откройте **Диспетчер DNS**.</span><span class="sxs-lookup"><span data-stu-id="702fa-111">Select the drop-down menu for the domain name that you wish to use with your Azure web app and select **Manage DNS**.</span></span>
   
    ![страница пользовательского домена для GoDaddy](./media/web-sites-godaddy-custom-domain-name/godaddy-customdomain.png)
2. <span data-ttu-id="702fa-113">На странице **Сведения о домене** откройте вкладку **Файл зоны DNS**.</span><span class="sxs-lookup"><span data-stu-id="702fa-113">From the **Domain details** page, scroll to the **DNS Zone File** tab.</span></span> <span data-ttu-id="702fa-114">Этот раздел используется в целях добавления и изменения записей DNS для доменного имени.</span><span class="sxs-lookup"><span data-stu-id="702fa-114">This is the section used for adding and modifying DNS records for your domain name.</span></span>
   
    ![Вкладка файла зоны DNS](./media/web-sites-godaddy-custom-domain-name/godaddy-zonetab.png)
   
    <span data-ttu-id="702fa-116">Выберите **Добавить запись** , чтобы добавить существующую запись.</span><span class="sxs-lookup"><span data-stu-id="702fa-116">Select **Add Record** to add an existing record.</span></span>
   
    <span data-ttu-id="702fa-117">Чтобы **отредактировать** существующую запись, выберите значок с изображением карандаша и бумаги рядом с записью.</span><span class="sxs-lookup"><span data-stu-id="702fa-117">To **edit** an existing record, select the pen & paper icon beside the record.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="702fa-118">Перед добавлением новых записей обратите внимание, что GoDaddy уже создал записи DNS для таких популярных поддоменов (**Узел** в редакторе), как **email**, **files**, **mail** и др.</span><span class="sxs-lookup"><span data-stu-id="702fa-118">Before adding new records, note that GoDaddy has already created DNS records for popular sub-domains (called **Host** in editor,) such as **email**, **files**, **mail**, and others.</span></span> <span data-ttu-id="702fa-119">Если имя, которое вы хотите использовать, уже существует, измените существующую запись вместо того, чтобы создавать новую.</span><span class="sxs-lookup"><span data-stu-id="702fa-119">If the name you wish to use already exists, modify the existing record instead of creating a new one.</span></span>
   > 
   > 
3. <span data-ttu-id="702fa-120">При добавлении записи необходимо сначала выбрать тип записи.</span><span class="sxs-lookup"><span data-stu-id="702fa-120">When adding a record, you must first select the record type.</span></span>
   
    ![выберите тип записи](./media/web-sites-godaddy-custom-domain-name/godaddy-selectrecordtype.png)
   
    <span data-ttu-id="702fa-122">Далее вы должны ввести **Узел** (личный домен или поддомен) и то, что будет значиться в поле **Указывает на**.</span><span class="sxs-lookup"><span data-stu-id="702fa-122">Next, you must provide the **Host** (the custom domain or sub-domain) and what it **Points to**.</span></span>
   
    ![добавление записи о зоне](./media/web-sites-godaddy-custom-domain-name/godaddy-addzonerecord.png)
   
   * <span data-ttu-id="702fa-124">При добавлении **записи A (узел)** нужно указать в поле **Узел** символ **@** (представляющий имя корневого домена, например **contoso.com**), * (подстановочный знак для сопоставления с несколькими поддоменами) либо поддомен, который вы хотите использовать (например, **www**.) Задайте в поле **Указывает на** IP-адрес вашего веб-приложения Azure.</span><span class="sxs-lookup"><span data-stu-id="702fa-124">When adding an **A (host) record** - you must set the **Host** field to either **@** (this represents root domain name, such as **contoso.com**,) * (a wildcard for matching multiple sub-domains,) or the sub-domain you wish to use (for example, **www**.) You must set the **Points to** field to the IP address of your Azure web app.</span></span>
   * <span data-ttu-id="702fa-125">При добавлении **записи (псевдонима) CNAME** необходимо задать в поле **Узел** тот поддомен, который вы хотите использовать.</span><span class="sxs-lookup"><span data-stu-id="702fa-125">When adding a **CNAME (alias) record** - you must set the **Host** field to the sub-domain you wish to use.</span></span> <span data-ttu-id="702fa-126">Например, **www**.</span><span class="sxs-lookup"><span data-stu-id="702fa-126">For example, **www**.</span></span> <span data-ttu-id="702fa-127">Задайте в поле **Указывает на** доменное имя **.azurewebsites.net** вашего веб-приложения Azure.</span><span class="sxs-lookup"><span data-stu-id="702fa-127">You must set the **Points to** field to the **.azurewebsites.net** domain name of your Azure web app.</span></span> <span data-ttu-id="702fa-128">Например, **contoso.azurewebsites.net**.</span><span class="sxs-lookup"><span data-stu-id="702fa-128">For example, **contoso.azurewebsites.net**.</span></span>
4. <span data-ttu-id="702fa-129">Нажмите **Добавить еще одну запись**.</span><span class="sxs-lookup"><span data-stu-id="702fa-129">Click **Add Another**.</span></span>
5. <span data-ttu-id="702fa-130">Выберите **TXT** в качестве типа записи, укажите для параметра **Узел** значение **@**, а для параметра **Указывает на** значение **&lt;имя_вашего_веб_приложения&gt;.azurewebsites.net**.</span><span class="sxs-lookup"><span data-stu-id="702fa-130">Select **TXT** as the record type, then specify a **Host** value of **@** and a **Points to** value of **&lt;yourwebappname&gt;.azurewebsites.net**.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="702fa-131">Запись типа TXT позволяет Azure убедиться, что именно вы являетесь владельцем домена, описанного в записи A или первой записи типа TXT.</span><span class="sxs-lookup"><span data-stu-id="702fa-131">This TXT record is used by Azure to validate that you own the domain described by the A record or the first TXT record.</span></span> <span data-ttu-id="702fa-132">После сопоставления домена с веб-приложением на портале Azure можно удалить запись типа TXT.</span><span class="sxs-lookup"><span data-stu-id="702fa-132">Once the domain has been mapped to the web app in the Azure Portal, this TXT record entry can be removed.</span></span>
   > 
   > 
6. <span data-ttu-id="702fa-133">По завершении добавления или изменения записей нажмите кнопку **Завершить** для сохранения изменений.</span><span class="sxs-lookup"><span data-stu-id="702fa-133">When you have finished adding or modifying records, click **Finish** to save changes.</span></span>

<a name="enabledomain"></a>

## <a name="enable-the-domain-name-on-your-web-app"></a><span data-ttu-id="702fa-134">Включение доменного имени в веб-приложении</span><span class="sxs-lookup"><span data-stu-id="702fa-134">Enable the domain name on your web app</span></span>
[!INCLUDE [modes](../../includes/custom-dns-web-site-enable-on-web-site.md)]

> [!NOTE]
> <span data-ttu-id="702fa-135">Чтобы приступить к работе со службой приложений Azure до создания учетной записи Azure, перейдите к разделу [Пробное использование службы приложений](https://azure.microsoft.com/try/app-service/), где вы можете быстро создать кратковременное веб-приложение начального уровня в службе приложений.</span><span class="sxs-lookup"><span data-stu-id="702fa-135">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="702fa-136">Никаких кредитных карт и обязательств.</span><span class="sxs-lookup"><span data-stu-id="702fa-136">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="whats-changed"></a><span data-ttu-id="702fa-137">Изменения</span><span class="sxs-lookup"><span data-stu-id="702fa-137">What's changed</span></span>
* <span data-ttu-id="702fa-138">Руководство по переходу от веб-сайтов к службе приложений см. в статье [Служба приложений Azure и существующие службы Azure](http://go.microsoft.com/fwlink/?LinkId=529714).</span><span class="sxs-lookup"><span data-stu-id="702fa-138">For a guide to the change from Websites to App Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

