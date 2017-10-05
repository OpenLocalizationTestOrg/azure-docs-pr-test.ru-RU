---
title: "Перенос активного DNS-имени в службу приложений Azure | Документы Майкрософт"
description: "Узнайте, как перенести DNS-имя, которое уже назначено работающему сайту, в службу приложений Azure без простоев."
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
ms.openlocfilehash: 89308c1c684a639950467b72d26703cc07c50c14
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="migrate-an-active-dns-name-to-azure-app-service"></a><span data-ttu-id="89a2c-103">Перенос активного DNS-имени в службу приложений Azure</span><span class="sxs-lookup"><span data-stu-id="89a2c-103">Migrate an active DNS name to Azure App Service</span></span>

<span data-ttu-id="89a2c-104">В этой статье показано, как перенести активное DNS-имя в [службу приложений Azure](../app-service/app-service-value-prop-what-is.md) без простоев.</span><span class="sxs-lookup"><span data-stu-id="89a2c-104">This article shows you how to migrate an active DNS name to [Azure App Service](../app-service/app-service-value-prop-what-is.md) without any downtime.</span></span>

<span data-ttu-id="89a2c-105">При переносе работающего сайта и его DNS-имени в службу приложений такое DNS-имя уже обслуживает реальный трафик.</span><span class="sxs-lookup"><span data-stu-id="89a2c-105">When you migrate a live site and its DNS domain name to App Service, that DNS name is already serving live traffic.</span></span> <span data-ttu-id="89a2c-106">Чтобы избежать простоя при разрешении DNS-имен во время миграции, можно предварительно привязать активное DNS-имя к приложению службы приложений.</span><span class="sxs-lookup"><span data-stu-id="89a2c-106">You can avoid downtime in DNS resolution during the migration by binding the active DNS name to your App Service app preemptively.</span></span>

<span data-ttu-id="89a2c-107">Если вас не беспокоит простой при разрешении DNS-имен, обратитесь к разделу [Сопоставление существующего настраиваемого DNS-имени с веб-приложениями Azure](app-service-web-tutorial-custom-domain.md).</span><span class="sxs-lookup"><span data-stu-id="89a2c-107">If you're not worried about downtime in DNS resolution, see [Map an existing custom DNS name to Azure Web Apps](app-service-web-tutorial-custom-domain.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="89a2c-108">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="89a2c-108">Prerequisites</span></span>

<span data-ttu-id="89a2c-109">Для работы с этим руководством:</span><span class="sxs-lookup"><span data-stu-id="89a2c-109">To complete this how-to:</span></span>

- <span data-ttu-id="89a2c-110">[Убедитесь, что приложение службы приложений не находится в ценовой категории "Бесплатный"](app-service-web-tutorial-custom-domain.md#checkpricing).</span><span class="sxs-lookup"><span data-stu-id="89a2c-110">[Make sure that your App Service app is not in FREE tier](app-service-web-tutorial-custom-domain.md#checkpricing).</span></span>

## <a name="bind-the-domain-name-preemptively"></a><span data-ttu-id="89a2c-111">Заблаговременная привязка доменного имени</span><span class="sxs-lookup"><span data-stu-id="89a2c-111">Bind the domain name preemptively</span></span>

<span data-ttu-id="89a2c-112">Заблаговременно привязывая личный домен, вы выполняете обе из приведенных ниже задач перед внесением каких-либо изменений в записи DNS:</span><span class="sxs-lookup"><span data-stu-id="89a2c-112">When you bind a custom domain preemptively, you accomplish both of the following before making any changes to your DNS records:</span></span>

- <span data-ttu-id="89a2c-113">проверка принадлежности домена;</span><span class="sxs-lookup"><span data-stu-id="89a2c-113">Verify domain ownership</span></span>
- <span data-ttu-id="89a2c-114">включение доменного имени для приложения.</span><span class="sxs-lookup"><span data-stu-id="89a2c-114">Enable the domain name for your app</span></span>

<span data-ttu-id="89a2c-115">Когда впоследствии вы перенесете настраиваемое DNS-имя из старого приложения в приложение службы приложений, разрешение DNS-имен будет выполняться без простоев.</span><span class="sxs-lookup"><span data-stu-id="89a2c-115">When you finally migrate your custom DNS name from the old site to the App Service app, there will be no downtime in DNS resolution.</span></span>

[!INCLUDE [Access DNS records with domain provider](../../includes/app-service-web-access-dns-records.md)]

### <a name="create-domain-verification-record"></a><span data-ttu-id="89a2c-116">Создание записи для проверки домена</span><span class="sxs-lookup"><span data-stu-id="89a2c-116">Create domain verification record</span></span>

<span data-ttu-id="89a2c-117">Чтобы проверить принадлежность домена, добавьте запись типа TXT.</span><span class="sxs-lookup"><span data-stu-id="89a2c-117">To verify domain ownership, Add a TXT record.</span></span> <span data-ttu-id="89a2c-118">Запись типа TXT выполняет сопоставление из _awverify.&lt;поддомен>_ в _&lt;имя_приложения>.azurewebsites.net_.</span><span class="sxs-lookup"><span data-stu-id="89a2c-118">The TXT record maps from _awverify.&lt;subdomain>_ to _&lt;appname>.azurewebsites.net_.</span></span> 

<span data-ttu-id="89a2c-119">Требуемая запись типа TXT зависит от записи DNS, которую требуется перенести.</span><span class="sxs-lookup"><span data-stu-id="89a2c-119">The TXT record you need depends on the DNS record you want to migrate.</span></span> <span data-ttu-id="89a2c-120">Примеры см. в следующей таблице (`@` обычно обозначает корневой домен):</span><span class="sxs-lookup"><span data-stu-id="89a2c-120">For examples, see the following table (`@` typically represents the root domain):</span></span>  

| <span data-ttu-id="89a2c-121">Пример записи DNS</span><span class="sxs-lookup"><span data-stu-id="89a2c-121">DNS record example</span></span> | <span data-ttu-id="89a2c-122">Узел, для которого задается TXT</span><span class="sxs-lookup"><span data-stu-id="89a2c-122">TXT Host</span></span> | <span data-ttu-id="89a2c-123">Значение TXT</span><span class="sxs-lookup"><span data-stu-id="89a2c-123">TXT Value</span></span> |
| - | - | - |
| <span data-ttu-id="89a2c-124">@ (корневой домен)</span><span class="sxs-lookup"><span data-stu-id="89a2c-124">@ (root)</span></span> | <span data-ttu-id="89a2c-125">_awverify_</span><span class="sxs-lookup"><span data-stu-id="89a2c-125">_awverify_</span></span> | <span data-ttu-id="89a2c-126">_&lt;имя_приложения>.azurewebsites.net_</span><span class="sxs-lookup"><span data-stu-id="89a2c-126">_&lt;appname>.azurewebsites.net_</span></span> |
| <span data-ttu-id="89a2c-127">www (поддомен)</span><span class="sxs-lookup"><span data-stu-id="89a2c-127">www (sub)</span></span> | <span data-ttu-id="89a2c-128">_awverify.www_</span><span class="sxs-lookup"><span data-stu-id="89a2c-128">_awverify.www_</span></span> | <span data-ttu-id="89a2c-129">_&lt;имя_приложения>.azurewebsites.net_</span><span class="sxs-lookup"><span data-stu-id="89a2c-129">_&lt;appname>.azurewebsites.net_</span></span> |
| <span data-ttu-id="89a2c-130">\* (с подстановочным знаком)</span><span class="sxs-lookup"><span data-stu-id="89a2c-130">\* (wildcard)</span></span> | <span data-ttu-id="89a2c-131">_awverify.\*_</span><span class="sxs-lookup"><span data-stu-id="89a2c-131">_awverify.\*_</span></span> | <span data-ttu-id="89a2c-132">_&lt;имя_приложения>.azurewebsites.net_</span><span class="sxs-lookup"><span data-stu-id="89a2c-132">_&lt;appname>.azurewebsites.net_</span></span> |

<span data-ttu-id="89a2c-133">На странице записей DNS запомните тип DNS-имени, которое требуется перенести.</span><span class="sxs-lookup"><span data-stu-id="89a2c-133">In your DNS records page, note the record type of the DNS name you want to migrate.</span></span> <span data-ttu-id="89a2c-134">Служба приложений поддерживает сопоставление из записей CNAME и записей A.</span><span class="sxs-lookup"><span data-stu-id="89a2c-134">App Service supports mappings from CNAME and A records.</span></span>

### <a name="enable-the-domain-for-your-app"></a><span data-ttu-id="89a2c-135">Включение домена для приложения</span><span class="sxs-lookup"><span data-stu-id="89a2c-135">Enable the domain for your app</span></span>

<span data-ttu-id="89a2c-136">В левой области навигации страницы приложения на [портале Azure](https://portal.azure.com) выберите **Личные домены**.</span><span class="sxs-lookup"><span data-stu-id="89a2c-136">In the [Azure portal](https://portal.azure.com), in the left navigation of the app page, select **Custom domains**.</span></span> 

![Меню личных доменов](./media/app-service-web-tutorial-custom-domain/custom-domain-menu.png)

<span data-ttu-id="89a2c-138">На странице **Личные домены** щелкните значок **+** рядом с пунктом **Добавить имя узла**.</span><span class="sxs-lookup"><span data-stu-id="89a2c-138">In the **Custom domains** page, select the **+** icon next to **Add hostname**.</span></span>

![Добавление имени узла](./media/app-service-web-tutorial-custom-domain/add-host-name-cname.png)

<span data-ttu-id="89a2c-140">Введите полное доменное имя, для которого вы добавили запись типа TXT, например `www.contoso.com`.</span><span class="sxs-lookup"><span data-stu-id="89a2c-140">Type the fully qualified domain name that you added the TXT record for, such as `www.contoso.com`.</span></span> <span data-ttu-id="89a2c-141">Для домена с подстановочным знаком (например, \*.contoso.com) можно использовать любое DNS-имя, которое совпадает с доменом с подстановочным знаком.</span><span class="sxs-lookup"><span data-stu-id="89a2c-141">For a wildcard domain (like \*.contoso.com), you can use any DNS name that matches the wildcard domain.</span></span> 

<span data-ttu-id="89a2c-142">Выберите **Проверка**.</span><span class="sxs-lookup"><span data-stu-id="89a2c-142">Select **Validate**.</span></span>

<span data-ttu-id="89a2c-143">После этого активируется кнопка **Добавить имя узла**.</span><span class="sxs-lookup"><span data-stu-id="89a2c-143">The **Add hostname** button is activated.</span></span> 

<span data-ttu-id="89a2c-144">Убедитесь, что в качестве значения параметра **Тип записи имени узла** задан тип записи DNS, которую необходимо перенести.</span><span class="sxs-lookup"><span data-stu-id="89a2c-144">Make sure that **Hostname record type** is set to the DNS record type you want to migrate.</span></span>

<span data-ttu-id="89a2c-145">Выберите **Добавить имя узла**.</span><span class="sxs-lookup"><span data-stu-id="89a2c-145">Select **Add hostname**.</span></span>

![Добавление DNS-имени в приложение](./media/app-service-web-tutorial-custom-domain/validate-domain-name-cname.png)

<span data-ttu-id="89a2c-147">Возможно, потребуется некоторое время для того, чтобы новое имя узла отобразилось на странице **Личные домены** вашего приложения.</span><span class="sxs-lookup"><span data-stu-id="89a2c-147">It might take some time for the new hostname to be reflected in the app's **Custom domains** page.</span></span> <span data-ttu-id="89a2c-148">Попробуйте обновить браузер, чтобы обновить данные.</span><span class="sxs-lookup"><span data-stu-id="89a2c-148">Try refreshing the browser to update the data.</span></span>

![Запись CNAME добавлена](./media/app-service-web-tutorial-custom-domain/cname-record-added.png)

<span data-ttu-id="89a2c-150">Теперь DNS-имя включено в приложении Azure.</span><span class="sxs-lookup"><span data-stu-id="89a2c-150">Your custom DNS name is now enabled in your Azure app.</span></span> 

## <a name="remap-the-active-dns-name"></a><span data-ttu-id="89a2c-151">Изменение сопоставления активного DNS-имени</span><span class="sxs-lookup"><span data-stu-id="89a2c-151">Remap the active DNS name</span></span>

<span data-ttu-id="89a2c-152">Теперь осталось только изменить сопоставление вашей активной записи DNS, чтобы она указывала на службу приложений.</span><span class="sxs-lookup"><span data-stu-id="89a2c-152">The only thing left to do is remapping your active DNS record to point to App Service.</span></span> <span data-ttu-id="89a2c-153">В настоящий момент она по-прежнему указывает на ваш старый веб-сайт.</span><span class="sxs-lookup"><span data-stu-id="89a2c-153">Right now, it still points to your old site.</span></span>

<a name="info"></a>

### <a name="copy-the-apps-ip-address-a-record-only"></a><span data-ttu-id="89a2c-154">Копирование IP-адреса приложения (только запись A)</span><span class="sxs-lookup"><span data-stu-id="89a2c-154">Copy the app's IP address (A record only)</span></span>

<span data-ttu-id="89a2c-155">Если выполняется сопоставление записи CNAME, пропустите этот раздел.</span><span class="sxs-lookup"><span data-stu-id="89a2c-155">If you are remapping a CNAME record, skip this section.</span></span> 

<span data-ttu-id="89a2c-156">Чтобы повторно сопоставить запись A, требуется внешний IP-адрес приложения службы приложений, который указан на странице **Личные домены**.</span><span class="sxs-lookup"><span data-stu-id="89a2c-156">To remap an A record, you need the App Service app's external IP address, which is shown in the **Custom domains** page.</span></span>

<span data-ttu-id="89a2c-157">Закройте страницу **Добавить имя узла**, щелкнув значок **X** в правом верхнем углу.</span><span class="sxs-lookup"><span data-stu-id="89a2c-157">Close the **Add hostname** page by selecting **X** in the upper-right corner.</span></span> 

<span data-ttu-id="89a2c-158">На странице **Личные домены** скопируйте IP-адрес приложения.</span><span class="sxs-lookup"><span data-stu-id="89a2c-158">In the **Custom domains** page, copy the app's IP address.</span></span>

![Переход к приложению Azure на портале](./media/app-service-web-tutorial-custom-domain/mapping-information.png)

### <a name="update-the-dns-record"></a><span data-ttu-id="89a2c-160">Обновление записи DNS</span><span class="sxs-lookup"><span data-stu-id="89a2c-160">Update the DNS record</span></span>

<span data-ttu-id="89a2c-161">Вернитесь на страницу записей DNS вашего поставщика домена и выберите запись DNS для повторного сопоставления.</span><span class="sxs-lookup"><span data-stu-id="89a2c-161">Back in the DNS records page of your domain provider, select the DNS record to remap.</span></span>

<span data-ttu-id="89a2c-162">В примере с корневым доменом `contoso.com` повторно сопоставьте запись A или запись CNAME, как показано в примерах в следующей таблице:</span><span class="sxs-lookup"><span data-stu-id="89a2c-162">For the `contoso.com` root domain example, remap the A or CNAME record like the examples in the following table:</span></span> 

| <span data-ttu-id="89a2c-163">Пример полного доменного имени</span><span class="sxs-lookup"><span data-stu-id="89a2c-163">FQDN example</span></span> | <span data-ttu-id="89a2c-164">Тип записи</span><span class="sxs-lookup"><span data-stu-id="89a2c-164">Record type</span></span> | <span data-ttu-id="89a2c-165">Узел</span><span class="sxs-lookup"><span data-stu-id="89a2c-165">Host</span></span> | <span data-ttu-id="89a2c-166">Значение</span><span class="sxs-lookup"><span data-stu-id="89a2c-166">Value</span></span> |
| - | - | - | - |
| <span data-ttu-id="89a2c-167">contoso.com (корневой домен)</span><span class="sxs-lookup"><span data-stu-id="89a2c-167">contoso.com (root)</span></span> | <span data-ttu-id="89a2c-168">Файл ,</span><span class="sxs-lookup"><span data-stu-id="89a2c-168">A</span></span> | `@` | <span data-ttu-id="89a2c-169">IP-адрес из раздела [Копирование IP-адреса приложения](#info).</span><span class="sxs-lookup"><span data-stu-id="89a2c-169">IP address from [Copy the app's IP address](#info)</span></span> |
| <span data-ttu-id="89a2c-170">www.contoso.com (поддомен)</span><span class="sxs-lookup"><span data-stu-id="89a2c-170">www.contoso.com (sub)</span></span> | <span data-ttu-id="89a2c-171">CNAME</span><span class="sxs-lookup"><span data-stu-id="89a2c-171">CNAME</span></span> | `www` | <span data-ttu-id="89a2c-172">_&lt;имя_приложения>.azurewebsites.net_</span><span class="sxs-lookup"><span data-stu-id="89a2c-172">_&lt;appname>.azurewebsites.net_</span></span> |
| <span data-ttu-id="89a2c-173">\*.contoso.com (с подстановочным знаком)</span><span class="sxs-lookup"><span data-stu-id="89a2c-173">\*.contoso.com (wildcard)</span></span> | <span data-ttu-id="89a2c-174">CNAME</span><span class="sxs-lookup"><span data-stu-id="89a2c-174">CNAME</span></span> | _\*_ | <span data-ttu-id="89a2c-175">_&lt;имя_приложения>.azurewebsites.net_</span><span class="sxs-lookup"><span data-stu-id="89a2c-175">_&lt;appname>.azurewebsites.net_</span></span> |

<span data-ttu-id="89a2c-176">Сохраните параметры.</span><span class="sxs-lookup"><span data-stu-id="89a2c-176">Save your settings.</span></span>

<span data-ttu-id="89a2c-177">Разрешение запросов DNS должно начаться в приложении службы приложений сразу после распространения DNS.</span><span class="sxs-lookup"><span data-stu-id="89a2c-177">DNS queries should start resolving to your App Service app immediately after DNS propagation happens.</span></span>

## <a name="next-steps"></a><span data-ttu-id="89a2c-178">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="89a2c-178">Next steps</span></span>

<span data-ttu-id="89a2c-179">Узнайте о том, как привязать настраиваемый SSL-сертификат к службе приложений.</span><span class="sxs-lookup"><span data-stu-id="89a2c-179">Learn how to bind a custom SSL certificate to App Service.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="89a2c-180">Привязывание существующего настраиваемого SSL-сертификата к веб-приложениям Azure</span><span class="sxs-lookup"><span data-stu-id="89a2c-180">Bind an existing custom SSL certificate to Azure Web Apps</span></span>](app-service-web-tutorial-custom-ssl.md)
