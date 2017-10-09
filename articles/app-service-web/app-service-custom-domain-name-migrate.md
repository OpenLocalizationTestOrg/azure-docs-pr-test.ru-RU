---
title: "aaaMigrate active DNS имя tooAzure службы приложений | Документы Microsoft"
description: "Узнайте, как toomigrate настраиваемого доменного имени DNS, уже назначенный tooa live tooAzure узла служб приложений без простоев."
services: app-service
documentationcenter: 
author: cephalin
manager: erikre
editor: jimbe
tags: top-support-issue
ms.assetid: 10da5b8a-1823-41a3-a2ff-a0717c2b5c2d
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/28/2017
ms.author: cephalin
ms.openlocfilehash: fbc4cc30dcb87efb2e867cb65c5404b667661e62
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-an-active-dns-name-tooazure-app-service"></a><span data-ttu-id="89aee-103">Перенос active tooAzure имя DNS службы приложений</span><span class="sxs-lookup"><span data-stu-id="89aee-103">Migrate an active DNS name tooAzure App Service</span></span>

<span data-ttu-id="89aee-104">В этой статье показано, как toomigrate active DNS имя слишком[службе приложений Azure](../app-service/app-service-value-prop-what-is.md) без простоев.</span><span class="sxs-lookup"><span data-stu-id="89aee-104">This article shows you how toomigrate an active DNS name too[Azure App Service](../app-service/app-service-value-prop-what-is.md) without any downtime.</span></span>

<span data-ttu-id="89aee-105">При миграции действующем сайте и его tooApp имя домена DNS службы DNS-имени уже обслуживает реального трафика.</span><span class="sxs-lookup"><span data-stu-id="89aee-105">When you migrate a live site and its DNS domain name tooApp Service, that DNS name is already serving live traffic.</span></span> <span data-ttu-id="89aee-106">Можно избежать простоя при разрешении DNS во время миграции hello, предварительно привязки hello active DNS имя tooyour приложением служб приложений.</span><span class="sxs-lookup"><span data-stu-id="89aee-106">You can avoid downtime in DNS resolution during hello migration by binding hello active DNS name tooyour App Service app preemptively.</span></span>

<span data-ttu-id="89aee-107">Если вы не сомневаетесь время простоя при разрешении DNS, см. раздел [сопоставления существующих пользовательских DNS имя tooAzure веб-приложений](app-service-web-tutorial-custom-domain.md).</span><span class="sxs-lookup"><span data-stu-id="89aee-107">If you're not worried about downtime in DNS resolution, see [Map an existing custom DNS name tooAzure Web Apps](app-service-web-tutorial-custom-domain.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="89aee-108">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="89aee-108">Prerequisites</span></span>

<span data-ttu-id="89aee-109">toocomplete этом руководства:</span><span class="sxs-lookup"><span data-stu-id="89aee-109">toocomplete this how-to:</span></span>

- <span data-ttu-id="89aee-110">[Убедитесь, что приложение службы приложений не находится в ценовой категории "Бесплатный"](app-service-web-tutorial-custom-domain.md#checkpricing).</span><span class="sxs-lookup"><span data-stu-id="89aee-110">[Make sure that your App Service app is not in FREE tier](app-service-web-tutorial-custom-domain.md#checkpricing).</span></span>

## <a name="bind-hello-domain-name-preemptively"></a><span data-ttu-id="89aee-111">Предварительно привязки имени домена hello</span><span class="sxs-lookup"><span data-stu-id="89aee-111">Bind hello domain name preemptively</span></span>

<span data-ttu-id="89aee-112">При связывании пользовательского домена предварительно выполнить оба следующих hello перед внесением любых изменений в записи DNS.</span><span class="sxs-lookup"><span data-stu-id="89aee-112">When you bind a custom domain preemptively, you accomplish both of hello following before making any changes to your DNS records:</span></span>

- <span data-ttu-id="89aee-113">проверка принадлежности домена;</span><span class="sxs-lookup"><span data-stu-id="89aee-113">Verify domain ownership</span></span>
- <span data-ttu-id="89aee-114">Включить hello имя домена приложения.</span><span class="sxs-lookup"><span data-stu-id="89aee-114">Enable hello domain name for your app</span></span>

<span data-ttu-id="89aee-115">При переносе пользовательской DNS-имя и, наконец из hello старого узла toohello приложением служб приложений во время разрешения DNS будет без простоев.</span><span class="sxs-lookup"><span data-stu-id="89aee-115">When you finally migrate your custom DNS name from hello old site toohello App Service app, there will be no downtime in DNS resolution.</span></span>

[!INCLUDE [Access DNS records with domain provider](../../includes/app-service-web-access-dns-records.md)]

### <a name="create-domain-verification-record"></a><span data-ttu-id="89aee-116">Создание записи для проверки домена</span><span class="sxs-lookup"><span data-stu-id="89aee-116">Create domain verification record</span></span>

<span data-ttu-id="89aee-117">владение tooverify домена, запишите добавить TXT.</span><span class="sxs-lookup"><span data-stu-id="89aee-117">tooverify domain ownership, Add a TXT record.</span></span> <span data-ttu-id="89aee-118">Сопоставляет Hello TXT-запись из _awverify.&lt; дочерний домен >_ too_&lt;appname >. azurewebsites.net_.</span><span class="sxs-lookup"><span data-stu-id="89aee-118">hello TXT record maps from _awverify.&lt;subdomain>_ too_&lt;appname>.azurewebsites.net_.</span></span> 

<span data-ttu-id="89aee-119">Hello TXT-записи, необходимые зависит от DNS-записей, которые требуется toomigrate hello.</span><span class="sxs-lookup"><span data-stu-id="89aee-119">hello TXT record you need depends on hello DNS record you want toomigrate.</span></span> <span data-ttu-id="89aee-120">Примеры см. в следующей таблице hello (`@` обычно представляет hello корневой домен):</span><span class="sxs-lookup"><span data-stu-id="89aee-120">For examples, see hello following table (`@` typically represents hello root domain):</span></span>  

| <span data-ttu-id="89aee-121">Пример записи DNS</span><span class="sxs-lookup"><span data-stu-id="89aee-121">DNS record example</span></span> | <span data-ttu-id="89aee-122">Узел, для которого задается TXT</span><span class="sxs-lookup"><span data-stu-id="89aee-122">TXT Host</span></span> | <span data-ttu-id="89aee-123">Значение TXT</span><span class="sxs-lookup"><span data-stu-id="89aee-123">TXT Value</span></span> |
| - | - | - |
| <span data-ttu-id="89aee-124">@ (корневой домен)</span><span class="sxs-lookup"><span data-stu-id="89aee-124">@ (root)</span></span> | <span data-ttu-id="89aee-125">_awverify_</span><span class="sxs-lookup"><span data-stu-id="89aee-125">_awverify_</span></span> | <span data-ttu-id="89aee-126">_&lt;имя_приложения>.azurewebsites.net_</span><span class="sxs-lookup"><span data-stu-id="89aee-126">_&lt;appname>.azurewebsites.net_</span></span> |
| <span data-ttu-id="89aee-127">www (поддомен)</span><span class="sxs-lookup"><span data-stu-id="89aee-127">www (sub)</span></span> | <span data-ttu-id="89aee-128">_awverify.www_</span><span class="sxs-lookup"><span data-stu-id="89aee-128">_awverify.www_</span></span> | <span data-ttu-id="89aee-129">_&lt;имя_приложения>.azurewebsites.net_</span><span class="sxs-lookup"><span data-stu-id="89aee-129">_&lt;appname>.azurewebsites.net_</span></span> |
| <span data-ttu-id="89aee-130">\* (с подстановочным знаком)</span><span class="sxs-lookup"><span data-stu-id="89aee-130">\* (wildcard)</span></span> | <span data-ttu-id="89aee-131">_awverify.\*_</span><span class="sxs-lookup"><span data-stu-id="89aee-131">_awverify.\*_</span></span> | <span data-ttu-id="89aee-132">_&lt;имя_приложения>.azurewebsites.net_</span><span class="sxs-lookup"><span data-stu-id="89aee-132">_&lt;appname>.azurewebsites.net_</span></span> |

<span data-ttu-id="89aee-133">На странице записей DNS Обратите внимание, hello тип записи для hello требуется toomigrate DNS-имя.</span><span class="sxs-lookup"><span data-stu-id="89aee-133">In your DNS records page, note hello record type of hello DNS name you want toomigrate.</span></span> <span data-ttu-id="89aee-134">Служба приложений поддерживает сопоставление из записей CNAME и записей A.</span><span class="sxs-lookup"><span data-stu-id="89aee-134">App Service supports mappings from CNAME and A records.</span></span>

### <a name="enable-hello-domain-for-your-app"></a><span data-ttu-id="89aee-135">Включить hello домена приложения</span><span class="sxs-lookup"><span data-stu-id="89aee-135">Enable hello domain for your app</span></span>

<span data-ttu-id="89aee-136">В hello [портал Azure](https://portal.azure.com)в левой области навигации страницы приложения hello hello, выберите **пользовательские домены**.</span><span class="sxs-lookup"><span data-stu-id="89aee-136">In hello [Azure portal](https://portal.azure.com), in hello left navigation of hello app page, select **Custom domains**.</span></span> 

![Меню личных доменов](./media/app-service-web-tutorial-custom-domain/custom-domain-menu.png)

<span data-ttu-id="89aee-138">В hello **пользовательские домены** страницу, выберите hello  **+**  значок Далее слишком**добавить имя узла**.</span><span class="sxs-lookup"><span data-stu-id="89aee-138">In hello **Custom domains** page, select hello **+** icon next too**Add hostname**.</span></span>

![Добавление имени узла](./media/app-service-web-tutorial-custom-domain/add-host-name-cname.png)

<span data-ttu-id="89aee-140">Полное доменное имя типа hello, добавлены hello TXT-записи, такие как `www.contoso.com`.</span><span class="sxs-lookup"><span data-stu-id="89aee-140">Type hello fully qualified domain name that you added hello TXT record for, such as `www.contoso.com`.</span></span> <span data-ttu-id="89aee-141">Для домена подстановочный знак (например \*. contoso.com), можно использовать любое имя DNS, которое совпадает с именем домена hello подстановочный знак.</span><span class="sxs-lookup"><span data-stu-id="89aee-141">For a wildcard domain (like \*.contoso.com), you can use any DNS name that matches hello wildcard domain.</span></span> 

<span data-ttu-id="89aee-142">Выберите **Проверка**.</span><span class="sxs-lookup"><span data-stu-id="89aee-142">Select **Validate**.</span></span>

<span data-ttu-id="89aee-143">Hello **добавить имя узла** кнопка активна.</span><span class="sxs-lookup"><span data-stu-id="89aee-143">hello **Add hostname** button is activated.</span></span> 

<span data-ttu-id="89aee-144">Убедитесь, что **тип записи имени узла** задается тип записи DNS toohello требуется toomigrate.</span><span class="sxs-lookup"><span data-stu-id="89aee-144">Make sure that **Hostname record type** is set toohello DNS record type you want toomigrate.</span></span>

<span data-ttu-id="89aee-145">Выберите **Добавить имя узла**.</span><span class="sxs-lookup"><span data-stu-id="89aee-145">Select **Add hostname**.</span></span>

![Добавить приложение toohello имя DNS](./media/app-service-web-tutorial-custom-domain/validate-domain-name-cname.png)

<span data-ttu-id="89aee-147">Он может занять некоторое время для нового узла toobe hello отражаются в приложение hello **пользовательские домены** страницы.</span><span class="sxs-lookup"><span data-stu-id="89aee-147">It might take some time for hello new hostname toobe reflected in hello app's **Custom domains** page.</span></span> <span data-ttu-id="89aee-148">Попробуйте обновить tooupdate hello hello обозревателя данных.</span><span class="sxs-lookup"><span data-stu-id="89aee-148">Try refreshing hello browser tooupdate hello data.</span></span>

![Запись CNAME добавлена](./media/app-service-web-tutorial-custom-domain/cname-record-added.png)

<span data-ttu-id="89aee-150">Теперь DNS-имя включено в приложении Azure.</span><span class="sxs-lookup"><span data-stu-id="89aee-150">Your custom DNS name is now enabled in your Azure app.</span></span> 

## <a name="remap-hello-active-dns-name"></a><span data-ttu-id="89aee-151">Изменить сопоставление hello active DNS-имя</span><span class="sxs-lookup"><span data-stu-id="89aee-151">Remap hello active DNS name</span></span>

<span data-ttu-id="89aee-152">Hello toodo самое левой изменение сопоставления вашей active tooApp toopoint записей DNS службы.</span><span class="sxs-lookup"><span data-stu-id="89aee-152">hello only thing left toodo is remapping your active DNS record toopoint tooApp Service.</span></span> <span data-ttu-id="89aee-153">Право, он по-прежнему указывает tooyour старого веб-сайта.</span><span class="sxs-lookup"><span data-stu-id="89aee-153">Right now, it still points tooyour old site.</span></span>

<a name="info"></a>

### <a name="copy-hello-apps-ip-address-a-record-only"></a><span data-ttu-id="89aee-154">Скопируйте приложение hello IP-адрес (только запись)</span><span class="sxs-lookup"><span data-stu-id="89aee-154">Copy hello app's IP address (A record only)</span></span>

<span data-ttu-id="89aee-155">Если выполняется сопоставление записи CNAME, пропустите этот раздел.</span><span class="sxs-lookup"><span data-stu-id="89aee-155">If you are remapping a CNAME record, skip this section.</span></span> 

<span data-ttu-id="89aee-156">запись A tooremap требуется внешний IP-адрес службы приложений приложение hello, как показано на hello **пользовательские домены** страницы.</span><span class="sxs-lookup"><span data-stu-id="89aee-156">tooremap an A record, you need hello App Service app's external IP address, which is shown in hello **Custom domains** page.</span></span>

<span data-ttu-id="89aee-157">Закрыть hello **добавить имя узла** страницу, выбрав **X** в правом верхнем углу hello.</span><span class="sxs-lookup"><span data-stu-id="89aee-157">Close hello **Add hostname** page by selecting **X** in hello upper-right corner.</span></span> 

<span data-ttu-id="89aee-158">В hello **пользовательские домены** скопируйте приложение hello IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="89aee-158">In hello **Custom domains** page, copy hello app's IP address.</span></span>

![Приложение портала навигации tooAzure](./media/app-service-web-tutorial-custom-domain/mapping-information.png)

### <a name="update-hello-dns-record"></a><span data-ttu-id="89aee-160">Обновление записи DNS hello</span><span class="sxs-lookup"><span data-stu-id="89aee-160">Update hello DNS record</span></span>

<span data-ttu-id="89aee-161">Hello странице записей DNS вашего домена поставщика выберите tooremap записей DNS hello.</span><span class="sxs-lookup"><span data-stu-id="89aee-161">Back in hello DNS records page of your domain provider, select hello DNS record tooremap.</span></span>

<span data-ttu-id="89aee-162">Для hello `contoso.com` корневого домена примере, повторно сопоставить hello A или запись CNAME как примеры hello в hello в следующей таблице:</span><span class="sxs-lookup"><span data-stu-id="89aee-162">For hello `contoso.com` root domain example, remap hello A or CNAME record like hello examples in hello following table:</span></span> 

| <span data-ttu-id="89aee-163">Пример полного доменного имени</span><span class="sxs-lookup"><span data-stu-id="89aee-163">FQDN example</span></span> | <span data-ttu-id="89aee-164">Тип записи</span><span class="sxs-lookup"><span data-stu-id="89aee-164">Record type</span></span> | <span data-ttu-id="89aee-165">Узел</span><span class="sxs-lookup"><span data-stu-id="89aee-165">Host</span></span> | <span data-ttu-id="89aee-166">Значение</span><span class="sxs-lookup"><span data-stu-id="89aee-166">Value</span></span> |
| - | - | - | - |
| <span data-ttu-id="89aee-167">contoso.com (корневой домен)</span><span class="sxs-lookup"><span data-stu-id="89aee-167">contoso.com (root)</span></span> | <span data-ttu-id="89aee-168">A</span><span class="sxs-lookup"><span data-stu-id="89aee-168">A</span></span> | `@` | <span data-ttu-id="89aee-169">IP-адрес из [приложение hello копирования IP-адрес](#info)</span><span class="sxs-lookup"><span data-stu-id="89aee-169">IP address from [Copy hello app's IP address](#info)</span></span> |
| <span data-ttu-id="89aee-170">www.contoso.com (поддомен)</span><span class="sxs-lookup"><span data-stu-id="89aee-170">www.contoso.com (sub)</span></span> | <span data-ttu-id="89aee-171">CNAME</span><span class="sxs-lookup"><span data-stu-id="89aee-171">CNAME</span></span> | `www` | <span data-ttu-id="89aee-172">_&lt;имя_приложения>.azurewebsites.net_</span><span class="sxs-lookup"><span data-stu-id="89aee-172">_&lt;appname>.azurewebsites.net_</span></span> |
| <span data-ttu-id="89aee-173">\*.contoso.com (с подстановочным знаком)</span><span class="sxs-lookup"><span data-stu-id="89aee-173">\*.contoso.com (wildcard)</span></span> | <span data-ttu-id="89aee-174">CNAME</span><span class="sxs-lookup"><span data-stu-id="89aee-174">CNAME</span></span> | _\*_ | <span data-ttu-id="89aee-175">_&lt;имя_приложения>.azurewebsites.net_</span><span class="sxs-lookup"><span data-stu-id="89aee-175">_&lt;appname>.azurewebsites.net_</span></span> |

<span data-ttu-id="89aee-176">Сохраните параметры.</span><span class="sxs-lookup"><span data-stu-id="89aee-176">Save your settings.</span></span>

<span data-ttu-id="89aee-177">Запросы DNS следует приступить к устранению tooyour приложением служб приложений, сразу после распространения DNS происходит.</span><span class="sxs-lookup"><span data-stu-id="89aee-177">DNS queries should start resolving tooyour App Service app immediately after DNS propagation happens.</span></span>

## <a name="next-steps"></a><span data-ttu-id="89aee-178">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="89aee-178">Next steps</span></span>

<span data-ttu-id="89aee-179">Узнайте, как toobind пользовательские SSL-сертификат tooApp службы.</span><span class="sxs-lookup"><span data-stu-id="89aee-179">Learn how toobind a custom SSL certificate tooApp Service.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="89aee-180">Привязать существующий пользовательский SSL сертификат tooAzure веб-приложений</span><span class="sxs-lookup"><span data-stu-id="89aee-180">Bind an existing custom SSL certificate tooAzure Web Apps</span></span>](app-service-web-tutorial-custom-ssl.md)
