---
title: "aaaConfigure пользовательское доменное имя в службе приложений Azure (GoDaddy)"
description: "Узнайте, как имя toouse домена GoDaddy с веб-приложениях Azure"
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
ms.openlocfilehash: 48158ee752f9833249bbf85adf80f572d1c68486
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="configure-a-custom-domain-name-in-azure-app-service-purchased-directly-from-godaddy"></a><span data-ttu-id="b2b82-103">Настройка личного доменного имени в службе приложений Azure (приобретенного непосредственно у GoDaddy)</span><span class="sxs-lookup"><span data-stu-id="b2b82-103">Configure a custom domain name in Azure App Service (Purchased directly from GoDaddy)</span></span>
[!INCLUDE [web-selector](../../includes/websites-custom-domain-selector.md)]

[!INCLUDE [intro](../../includes/custom-dns-web-site-intro.md)]

<span data-ttu-id="b2b82-104">Если приобрели домен через веб-приложениях службы приложений Azure, а затем ссылаться на последнем этапе toohello работы [купить домена для веб-приложений](custom-dns-web-site-buydomains-web-app.md).</span><span class="sxs-lookup"><span data-stu-id="b2b82-104">If you have purchased domain through Azure App Service Web Apps then refer toohello final step of [Buy Domain for Web Apps](custom-dns-web-site-buydomains-web-app.md).</span></span>

<span data-ttu-id="b2b82-105">В этой статье вы найдете указания по использованию личного доменного имени, приобретенного у [GoDaddy](https://godaddy.com), с использованием [веб-приложений службы приложений](http://go.microsoft.com/fwlink/?LinkId=529714).</span><span class="sxs-lookup"><span data-stu-id="b2b82-105">This article provides instructions on using a custom domain name that was purchased directly from [GoDaddy](https://godaddy.com) with [App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714).</span></span>

[!INCLUDE [introfooter](../../includes/custom-dns-web-site-intro-notes.md)]

<a name="understanding-records"></a>

## <a name="understanding-dns-records"></a><span data-ttu-id="b2b82-106">Общие сведения о записях DNS</span><span class="sxs-lookup"><span data-stu-id="b2b82-106">Understanding DNS records</span></span>
[!INCLUDE [understandingdns](../../includes/custom-dns-web-site-understanding-dns-raw.md)]

<a name="bkmk_configurecname"></a>

## <a name="add-a-dns-record-for-your-custom-domain"></a><span data-ttu-id="b2b82-107">Добавление записи DNS для пользовательского домена</span><span class="sxs-lookup"><span data-stu-id="b2b82-107">Add a DNS record for your custom domain</span></span>
<span data-ttu-id="b2b82-108">tooassociate свой домен с веб-приложения в службе приложений, необходимо добавить новую запись в таблице hello DNS для личного домена с помощью средств, предоставляемых GoDaddy.</span><span class="sxs-lookup"><span data-stu-id="b2b82-108">tooassociate your custom domain with a web app in App Service, you must add a new entry in hello DNS table for your custom domain by using tools provided by GoDaddy.</span></span> <span data-ttu-id="b2b82-109">Используйте следующие шаги toolocate hello DNS средства для GoDaddy.com hello</span><span class="sxs-lookup"><span data-stu-id="b2b82-109">Use hello following steps toolocate hello DNS tools for GoDaddy.com</span></span>

1. <span data-ttu-id="b2b82-110">Войдите в систему учетной записи tooyour с GoDaddy.com и выберите **Моя учетная запись** и затем **управление Мои домены**.</span><span class="sxs-lookup"><span data-stu-id="b2b82-110">Log on tooyour account with GoDaddy.com, and select **My Account** and then **Manage my domains**.</span></span> <span data-ttu-id="b2b82-111">Выберите hello раскрывающееся меню для имени домена hello обратиться toouse с Azure веб-приложения и выберите **Управление DNS**.</span><span class="sxs-lookup"><span data-stu-id="b2b82-111">Select hello drop-down menu for hello domain name that you wish toouse with your Azure web app and select **Manage DNS**.</span></span>
   
    ![страница пользовательского домена для GoDaddy](./media/web-sites-godaddy-custom-domain-name/godaddy-customdomain.png)
2. <span data-ttu-id="b2b82-113">Из hello **сведения о домене** перейдите toohello **файла зоны DNS** вкладки. Это раздел hello, используются для добавления и изменения записей DNS для имени домена.</span><span class="sxs-lookup"><span data-stu-id="b2b82-113">From hello **Domain details** page, scroll toohello **DNS Zone File** tab. This is hello section used for adding and modifying DNS records for your domain name.</span></span>
   
    ![Вкладка файла зоны DNS](./media/web-sites-godaddy-custom-domain-name/godaddy-zonetab.png)
   
    <span data-ttu-id="b2b82-115">Выберите **добавить запись** tooadd существующей записи.</span><span class="sxs-lookup"><span data-stu-id="b2b82-115">Select **Add Record** tooadd an existing record.</span></span>
   
    <span data-ttu-id="b2b82-116">слишком**изменить** существующую запись, выберите hello перо и бумага значок рядом с записью hello.</span><span class="sxs-lookup"><span data-stu-id="b2b82-116">too**edit** an existing record, select hello pen & paper icon beside hello record.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="b2b82-117">Перед добавлением новых записей обратите внимание, что GoDaddy уже создал записи DNS для таких популярных поддоменов (**Узел** в редакторе), как **email**, **files**, **mail** и др.</span><span class="sxs-lookup"><span data-stu-id="b2b82-117">Before adding new records, note that GoDaddy has already created DNS records for popular sub-domains (called **Host** in editor,) such as **email**, **files**, **mail**, and others.</span></span> <span data-ttu-id="b2b82-118">Если вы хотите toouse имя hello существует, измените существующую запись hello вместо создания нового.</span><span class="sxs-lookup"><span data-stu-id="b2b82-118">If hello name you wish toouse already exists, modify hello existing record instead of creating a new one.</span></span>
   > 
   > 
3. <span data-ttu-id="b2b82-119">Добавление записи, необходимо сначала выбрать тип записи hello.</span><span class="sxs-lookup"><span data-stu-id="b2b82-119">When adding a record, you must first select hello record type.</span></span>
   
    ![выберите тип записи](./media/web-sites-godaddy-custom-domain-name/godaddy-selectrecordtype.png)
   
    <span data-ttu-id="b2b82-121">Затем необходимо указать hello **узла** (hello пользовательский домен или дочерний домен) и что он **указывает**.</span><span class="sxs-lookup"><span data-stu-id="b2b82-121">Next, you must provide hello **Host** (hello custom domain or sub-domain) and what it **Points to**.</span></span>
   
    ![добавление записи о зоне](./media/web-sites-godaddy-custom-domain-name/godaddy-addzonerecord.png)
   
   * <span data-ttu-id="b2b82-123">При добавлении **запись (узла)** -необходимо задать hello **узла** tooeither поле  **@**  (представляет имя корневого домена, такие как  **Contoso.com**,) * (шаблон для сопоставления нескольких поддоменов) или hello дочерний домен, нужно toouse (например, **www**.) Необходимо задать hello **указывает** поле toohello IP-адрес вашего веб-приложение Azure.</span><span class="sxs-lookup"><span data-stu-id="b2b82-123">When adding an **A (host) record** - you must set hello **Host** field tooeither **@** (this represents root domain name, such as **contoso.com**,) * (a wildcard for matching multiple sub-domains,) or hello sub-domain you wish toouse (for example, **www**.) You must set hello **Points to** field toohello IP address of your Azure web app.</span></span>
   * <span data-ttu-id="b2b82-124">При добавлении **запись CNAME (псевдоним)** -необходимо задать hello **узла** поле toohello поддомене нужно toouse.</span><span class="sxs-lookup"><span data-stu-id="b2b82-124">When adding a **CNAME (alias) record** - you must set hello **Host** field toohello sub-domain you wish toouse.</span></span> <span data-ttu-id="b2b82-125">Например, **www**.</span><span class="sxs-lookup"><span data-stu-id="b2b82-125">For example, **www**.</span></span> <span data-ttu-id="b2b82-126">Необходимо задать hello **указывает** toohello поле **. azurewebsites.net** доменное имя вашего веб-приложение Azure.</span><span class="sxs-lookup"><span data-stu-id="b2b82-126">You must set hello **Points to** field toohello **.azurewebsites.net** domain name of your Azure web app.</span></span> <span data-ttu-id="b2b82-127">Например, **contoso.azurewebsites.net**.</span><span class="sxs-lookup"><span data-stu-id="b2b82-127">For example, **contoso.azurewebsites.net**.</span></span>
4. <span data-ttu-id="b2b82-128">Нажмите **Добавить еще одну запись**.</span><span class="sxs-lookup"><span data-stu-id="b2b82-128">Click **Add Another**.</span></span>
5. <span data-ttu-id="b2b82-129">Выберите **TXT** как тип записи hello, затем укажите **узла** значение  **@**  и **указывает** значение  **&lt;yourwebappname&gt;. azurewebsites.net**.</span><span class="sxs-lookup"><span data-stu-id="b2b82-129">Select **TXT** as hello record type, then specify a **Host** value of **@** and a **Points to** value of **&lt;yourwebappname&gt;.azurewebsites.net**.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="b2b82-130">TXT-запись используется Azure toovalidate, что вы являетесь владельцем, что домен hello описываемого hello hello или записи первая запись TXT.</span><span class="sxs-lookup"><span data-stu-id="b2b82-130">This TXT record is used by Azure toovalidate that you own hello domain described by hello A record or hello first TXT record.</span></span> <span data-ttu-id="b2b82-131">После домена hello сопоставленных toohello веб-приложения в hello портал Azure, этой записи TXT-записи можно удалить.</span><span class="sxs-lookup"><span data-stu-id="b2b82-131">Once hello domain has been mapped toohello web app in hello Azure Portal, this TXT record entry can be removed.</span></span>
   > 
   > 
6. <span data-ttu-id="b2b82-132">Когда закончите добавлять или изменение записей, нажмите кнопку **Готово** toosave изменений.</span><span class="sxs-lookup"><span data-stu-id="b2b82-132">When you have finished adding or modifying records, click **Finish** toosave changes.</span></span>

<a name="enabledomain"></a>

## <a name="enable-hello-domain-name-on-your-web-app"></a><span data-ttu-id="b2b82-133">Включить hello доменного имени на веб-приложения</span><span class="sxs-lookup"><span data-stu-id="b2b82-133">Enable hello domain name on your web app</span></span>
[!INCLUDE [modes](../../includes/custom-dns-web-site-enable-on-web-site.md)]

> [!NOTE]
> <span data-ttu-id="b2b82-134">Tooget работы в службе приложений Azure перед регистрацией учетную запись Azure, перейдите слишком[повторите служб приложений](https://azure.microsoft.com/try/app-service/), в котором можно немедленно создать кратковременных начальный веб-приложения в службе приложений.</span><span class="sxs-lookup"><span data-stu-id="b2b82-134">If you want tooget started with Azure App Service before signing up for an Azure account, go too[Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="b2b82-135">Никаких кредитных карт и обязательств.</span><span class="sxs-lookup"><span data-stu-id="b2b82-135">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="whats-changed"></a><span data-ttu-id="b2b82-136">Изменения</span><span class="sxs-lookup"><span data-stu-id="b2b82-136">What's changed</span></span>
* <span data-ttu-id="b2b82-137">Toohello руководство изменений из tooApp веб-сайтов службы. в разделе: [службе приложений Azure и ее влияние на существующие службы Azure](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="b2b82-137">For a guide toohello change from Websites tooApp Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

