---
title: "aaaConfigure пользовательское доменное имя для веб-приложения в службе приложений Azure, который использует диспетчер трафика для балансировки нагрузки."
description: "Используйте личное доменное имя для веб-приложения в службе приложений Azure, которая включает в себя диспетчер трафика."
services: app-service\web
documentationcenter: 
author: cephalin
manager: cfowler
editor: 
ms.assetid: 0f96c0e7-0901-489b-a95a-e3b66ca0a1c2
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2016
ms.author: cephalin
ms.openlocfilehash: dfde5fc6b445b30b10e03dcb03e8d072130d9377
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="configuring-a-custom-domain-name-for-a-web-app-in-azure-app-service-using-traffic-manager"></a><span data-ttu-id="2ede8-103">Настройка личного доменного имени для веб-приложения в службе приложений Azure, использующей диспетчер трафика</span><span class="sxs-lookup"><span data-stu-id="2ede8-103">Configuring a custom domain name for a web app in Azure App Service using Traffic Manager</span></span>
[!INCLUDE [web-selector](../../includes/websites-custom-domain-selector.md)]

[!INCLUDE [intro](../../includes/custom-dns-web-site-intro-traffic-manager.md)]

<span data-ttu-id="2ede8-104">В этой статье содержатся общие инструкции по использованию личного доменного имени со службой приложений Azure, которая использует диспетчер трафика для балансировки нагрузки.</span><span class="sxs-lookup"><span data-stu-id="2ede8-104">This article provides generic instructions for using a custom domain name with Azure App Service that use Traffic Manager for load balancing.</span></span>

[!INCLUDE [tmwebsitefooter](../../includes/custom-dns-web-site-traffic-manager-notes.md)]

[!INCLUDE [introfooter](../../includes/custom-dns-web-site-intro-notes.md)]

<a name="understanding-records"></a>

## <a name="understanding-dns-records"></a><span data-ttu-id="2ede8-105">Общие сведения о записях DNS</span><span class="sxs-lookup"><span data-stu-id="2ede8-105">Understanding DNS records</span></span>
[!INCLUDE [understandingdns](../../includes/custom-dns-web-site-understanding-dns-traffic-manager.md)]

<a name="bkmk_configsharedmode"></a>

## <a name="configure-your-web-apps-for-standard-mode"></a><span data-ttu-id="2ede8-106">Настройка веб-приложений для режима Standard</span><span class="sxs-lookup"><span data-stu-id="2ede8-106">Configure your web apps for standard mode</span></span>
[!INCLUDE [modes](../../includes/custom-dns-web-site-modes-traffic-manager.md)]

<a name="bkmk_configurecname"></a>

## <a name="add-a-dns-record-for-your-custom-domain"></a><span data-ttu-id="2ede8-107">Добавление записи DNS для пользовательского домена</span><span class="sxs-lookup"><span data-stu-id="2ede8-107">Add a DNS record for your custom domain</span></span>
> [!NOTE]
> <span data-ttu-id="2ede8-108">Если вы приобрели домен через веб-приложениях службы приложений Azure пропустите следующие шаги и toohello заключительном этапе см. [купить домена для веб-приложений](custom-dns-web-site-buydomains-web-app.md) статьи.</span><span class="sxs-lookup"><span data-stu-id="2ede8-108">If you have purchased domain through Azure App Service Web Apps then skip following steps and refer toohello final step of [Buy Domain for Web Apps](custom-dns-web-site-buydomains-web-app.md) article.</span></span>
> 
> 

<span data-ttu-id="2ede8-109">tooassociate свой домен с веб-приложения в службе приложений Azure, необходимо добавить новую запись в таблице hello DNS для личного домена с помощью средств, предоставляемых hello регистратора, который вы приобрели доменного имени из.</span><span class="sxs-lookup"><span data-stu-id="2ede8-109">tooassociate your custom domain with a web app in Azure App Service, you must add a new entry in hello DNS table for your custom domain by using tools provided by hello domain registrar that you purchased your domain name from.</span></span> <span data-ttu-id="2ede8-110">Используйте следующие шаги toolocate hello и средства hello DNS.</span><span class="sxs-lookup"><span data-stu-id="2ede8-110">Use hello following steps toolocate and use hello DNS tools.</span></span>

1. <span data-ttu-id="2ede8-111">Войдите в tooyour учетную запись на сайте регистратора домена и найти страницу управления DNS-записей.</span><span class="sxs-lookup"><span data-stu-id="2ede8-111">Sign in tooyour account at your domain registrar, and look for a page for managing DNS records.</span></span> <span data-ttu-id="2ede8-112">Найдите ссылки или области hello узла помечены как **доменное имя**, **DNS**, или **управление сервером имен**.</span><span class="sxs-lookup"><span data-stu-id="2ede8-112">Look for links or areas of hello site labeled as **Domain Name**, **DNS**, or **Name Server Management**.</span></span> <span data-ttu-id="2ede8-113">Часто toothis страницы можно найти ссылку Просмотр сведений учетной записи и Отыскав ссылку например **Мои домены**.</span><span class="sxs-lookup"><span data-stu-id="2ede8-113">Often a link toothis page can be found be viewing your account information, and then looking for a link such as **My domains**.</span></span>
2. <span data-ttu-id="2ede8-114">После обнаружения hello страницы управления для имени домена найдите ссылку, которая позволяет вам tooedit hello DNS-записей.</span><span class="sxs-lookup"><span data-stu-id="2ede8-114">Once you have found hello management page for your domain name, look for a link that allows you tooedit hello DNS records.</span></span> <span data-ttu-id="2ede8-115">Она может иметь название **Файл зоны**, **Записи DNS** или **Дополнительно**.</span><span class="sxs-lookup"><span data-stu-id="2ede8-115">This might be listed as a **Zone file**, **DNS Records**, or as an **Advanced** configuration link.</span></span>
   
   * <span data-ttu-id="2ede8-116">Страница приветствия скорее всего будет иметь несколько записей, которые уже созданы, таких как операции сопоставления "**@**«или»\*" со страницей «парковки домена».</span><span class="sxs-lookup"><span data-stu-id="2ede8-116">hello page will most likely have a few records already created, such as an entry associating '**@**' or '\*' with a 'domain parking' page.</span></span> <span data-ttu-id="2ede8-117">Она также может содержать записи для распространенных поддоменов, таких как **www**.</span><span class="sxs-lookup"><span data-stu-id="2ede8-117">It may also contain records for common sub-domains such as **www**.</span></span>
   * <span data-ttu-id="2ede8-118">Назовите страницу приветствия будет **записи CNAME**, или укажите tooselect раскрывающегося списка тип записи.</span><span class="sxs-lookup"><span data-stu-id="2ede8-118">hello page will mention **CNAME records**, or provide a drop-down tooselect a record type.</span></span> <span data-ttu-id="2ede8-119">На ней также могут упоминаться другие записи, такие как **записи A** и **записи MX**.</span><span class="sxs-lookup"><span data-stu-id="2ede8-119">It may also mention other records such as **A records** and **MX records**.</span></span> <span data-ttu-id="2ede8-120">В некоторых случаях записи CNAME могут называться по-другому, например **записью псевдонима**.</span><span class="sxs-lookup"><span data-stu-id="2ede8-120">In some cases, CNAME records will be called by other names such as an **Alias Record**.</span></span>
   * <span data-ttu-id="2ede8-121">Страница приветствия также будет иметь поля, которые позволяют слишком**карты** из **имя узла** или **доменное имя** tooanother доменное имя.</span><span class="sxs-lookup"><span data-stu-id="2ede8-121">hello page will also have fields that allow you too**map** from a **Host name** or **Domain name** tooanother domain name.</span></span>
3. <span data-ttu-id="2ede8-122">Хотя отличаться hello особенности каждого регистратора, как правило сопоставления *из* пользовательское имя домена (например, **contoso.com**,) *для* имя домена диспетчера трафика hello (**contoso.trafficmanager.net**), используемый для веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="2ede8-122">While hello specifics of each registrar vary, in general you map *from* your custom domain name (such as **contoso.com**,) *to* hello Traffic Manager domain name (**contoso.trafficmanager.net**) that is used for your web app.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="2ede8-123">Кроме того Если записи уже используется, и необходимости toopreemptively привязки tooit вашего приложения, можно создать дополнительные записи CNAME.</span><span class="sxs-lookup"><span data-stu-id="2ede8-123">Alternatively, if a record is already in use and you need toopreemptively bind your apps tooit, you can create an additional CNAME record.</span></span> <span data-ttu-id="2ede8-124">Например, привязка toopreemptively **www.contoso.com** tooyour веб-приложения, создайте запись CNAME из **awverify.www** слишком**contoso.trafficmanager.net**.</span><span class="sxs-lookup"><span data-stu-id="2ede8-124">For example, toopreemptively bind **www.contoso.com** tooyour web app, create a CNAME record from **awverify.www** too**contoso.trafficmanager.net**.</span></span> <span data-ttu-id="2ede8-125">Затем можно добавить tooyour «www.contoso.com» веб-приложения без изменения записи CNAME hello «www».</span><span class="sxs-lookup"><span data-stu-id="2ede8-125">You can then add "www.contoso.com" tooyour Web App without changing hello "www" CNAME record.</span></span> <span data-ttu-id="2ede8-126">Дополнительные сведения см. в статье [Создание записей DNS для веб-приложения в пользовательском домене][CREATEDNS].</span><span class="sxs-lookup"><span data-stu-id="2ede8-126">For more information, see [Create DNS records for a web app in a custom domain][CREATEDNS].</span></span>
   > 
   > 
4. <span data-ttu-id="2ede8-127">После завершения добавления или изменения записей DNS у регистратора, сохраните изменения hello.</span><span class="sxs-lookup"><span data-stu-id="2ede8-127">Once you have finished adding or modifying DNS records at your registrar, save hello changes.</span></span>

<a name="enabledomain"></a>

## <a name="enable-traffic-manager"></a><span data-ttu-id="2ede8-128">Включение диспетчера трафика</span><span class="sxs-lookup"><span data-stu-id="2ede8-128">Enable Traffic Manager</span></span>
[!INCLUDE [modes](../../includes/custom-dns-web-site-enable-on-traffic-manager.md)]

## <a name="next-steps"></a><span data-ttu-id="2ede8-129">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="2ede8-129">Next steps</span></span>
<span data-ttu-id="2ede8-130">Дополнительные сведения см. в разделе hello [Центр разработчика Node.js](/develop/nodejs/).</span><span class="sxs-lookup"><span data-stu-id="2ede8-130">For more information, see hello [Node.js Developer Center](/develop/nodejs/).</span></span>

[!INCLUDE [app-service-web-whats-changed](../../includes/app-service-web-whats-changed.md)]

[!INCLUDE [app-service-web-try-app-service](../../includes/app-service-web-try-app-service.md)]

<!-- URL List -->

[CREATEDNS]: ../dns/dns-web-sites-custom-domain.md
