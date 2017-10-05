---
title: "Настройка пользовательского доменного имени в облачных службах | Документация Майкрософт"
description: "Узнайте, как опубликовать в Интернете приложение или данные Azure на пользовательском домене, настроив параметры DNS.  В этих примерах используется портал Azure."
services: cloud-services
documentationcenter: .net
author: Thraka
manager: timlt
editor: 
ms.assetid: 5783a246-a151-4fb1-b488-441bfb29ee44
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: adegeo
ms.openlocfilehash: cf43d86dddc3a68573e1ba1b09118c54f0b16bc5
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="configuring-a-custom-domain-name-for-an-azure-cloud-service"></a><span data-ttu-id="4dc67-104">Настройка пользовательского доменного имени для облачной службы Azure</span><span class="sxs-lookup"><span data-stu-id="4dc67-104">Configuring a custom domain name for an Azure cloud service</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="4dc67-105">Портал Azure</span><span class="sxs-lookup"><span data-stu-id="4dc67-105">Azure portal</span></span>](cloud-services-custom-domain-name-portal.md)
> * [<span data-ttu-id="4dc67-106">Классический портал Azure</span><span class="sxs-lookup"><span data-stu-id="4dc67-106">Azure classic portal</span></span>](cloud-services-custom-domain-name.md)
> 
> 

<span data-ttu-id="4dc67-107">При создании облачной службы Azure ей назначается поддомен **cloudapp.net**.</span><span class="sxs-lookup"><span data-stu-id="4dc67-107">When you create a Cloud Service, Azure assigns it to a subdomain of **cloudapp.net**.</span></span> <span data-ttu-id="4dc67-108">Например, если облачная служба имеет имя contoso, пользователи будут иметь доступ к приложению по URL-адресу вида http://contoso.cloudapp.net.</span><span class="sxs-lookup"><span data-stu-id="4dc67-108">For example, if your Cloud Service is named "contoso", your users will be able to access your application on a URL like http://contoso.cloudapp.net.</span></span> <span data-ttu-id="4dc67-109">Azure также назначает виртуальный IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="4dc67-109">Azure also assigns a virtual IP address.</span></span>

<span data-ttu-id="4dc67-110">Однако приложение можно сделать доступным и на своем собственном домене, например **contoso.com**. В этой статье объясняется, как зарезервировать или настроить личное доменное имя для веб-ролей облачной службы.</span><span class="sxs-lookup"><span data-stu-id="4dc67-110">However, you can also expose your application on your own domain name, such as **contoso.com**. This article explains how to reserve or configure a custom domain name for Cloud Service web roles.</span></span>

<span data-ttu-id="4dc67-111">Вы уже знаете, что такое записи CNAME и A?</span><span class="sxs-lookup"><span data-stu-id="4dc67-111">Do you already understand what CNAME and A records are?</span></span> <span data-ttu-id="4dc67-112">[Пропустите это объяснение](#add-a-cname-record-for-your-custom-domain).</span><span class="sxs-lookup"><span data-stu-id="4dc67-112">[Jump past the explanation](#add-a-cname-record-for-your-custom-domain).</span></span>

> [!NOTE]
> <span data-ttu-id="4dc67-113">Процедуры в этом задании применяются для облачных служб Azure.</span><span class="sxs-lookup"><span data-stu-id="4dc67-113">The procedures in this task apply to Azure Cloud Services.</span></span> <span data-ttu-id="4dc67-114">Для получения сведений о службах приложений см. [эту статью](../app-service-web/web-sites-custom-domain-name.md).</span><span class="sxs-lookup"><span data-stu-id="4dc67-114">For App Services, see [this](../app-service-web/web-sites-custom-domain-name.md).</span></span> <span data-ttu-id="4dc67-115">Для получения сведений об учетных записях хранения см. [эту статью](../storage/blobs/storage-custom-domain-name.md).</span><span class="sxs-lookup"><span data-stu-id="4dc67-115">For storage accounts, see [this](../storage/blobs/storage-custom-domain-name.md).</span></span>
> 
> 

<p/>

> [!TIP]
> <span data-ttu-id="4dc67-116">Приступите к работе быстрее — воспользуйтесь НОВЫМ [пошаговым руководством](http://support.microsoft.com/kb/2990804)Azure!</span><span class="sxs-lookup"><span data-stu-id="4dc67-116">Get going faster--use the NEW Azure [guided walkthrough](http://support.microsoft.com/kb/2990804)!</span></span>  <span data-ttu-id="4dc67-117">С его помощью вы без труда сможете связать пользовательское доменное имя И защитить обмен данными (SSL) с облачными службами Azure или веб-сайтами Azure.</span><span class="sxs-lookup"><span data-stu-id="4dc67-117">It makes associating a custom domain name AND securing communication (SSL) with Azure Cloud Services or Azure Websites a snap.</span></span>
> 
> 

## <a name="understand-cname-and-a-records"></a><span data-ttu-id="4dc67-118">Что такое записи CNAME и A</span><span class="sxs-lookup"><span data-stu-id="4dc67-118">Understand CNAME and A records</span></span>
<span data-ttu-id="4dc67-119">И записи CNAME (или записи псевдонимов), и записи А позволяют связать имя домена с конкретным сервером (или службой в данном случае), но они работают по-разному.</span><span class="sxs-lookup"><span data-stu-id="4dc67-119">CNAME (or alias records) and A records both allow you to associate a domain name with a specific server (or service in this case,) however they work differently.</span></span> <span data-ttu-id="4dc67-120">При использовании записей А с облачными службами Azure существуют также некоторые особые соображения, которые следует учесть, принимая решение, какие именно записи использовать.</span><span class="sxs-lookup"><span data-stu-id="4dc67-120">There are also some specific considerations when using A records with Azure Cloud services that you should consider before deciding which to use.</span></span>

### <a name="cname-or-alias-record"></a><span data-ttu-id="4dc67-121">Запись CNAME, или запись псевдонима</span><span class="sxs-lookup"><span data-stu-id="4dc67-121">CNAME or Alias record</span></span>
<span data-ttu-id="4dc67-122">Запись CNAME сопоставляет *конкретный* домен, такой как **contoso.com** or **www.contoso.com**, с каноническим именем домена.</span><span class="sxs-lookup"><span data-stu-id="4dc67-122">A CNAME record maps a *specific* domain, such as **contoso.com** or **www.contoso.com**, to a canonical domain name.</span></span> <span data-ttu-id="4dc67-123">В этом случае каноническим доменным именем является доменное имя **[myapp].cloudapp.net** размещенного приложения Azure.</span><span class="sxs-lookup"><span data-stu-id="4dc67-123">In this case, the canonical domain name is the **[myapp].cloudapp.net** domain name of your Azure hosted application.</span></span> <span data-ttu-id="4dc67-124">После создания запись CNAME создает псевдоним для **[myapp].cloudapp.net**.</span><span class="sxs-lookup"><span data-stu-id="4dc67-124">Once created, the CNAME creates an alias for the **[myapp].cloudapp.net**.</span></span> <span data-ttu-id="4dc67-125">Запись CNAME будет автоматически разрешаться в IP-адрес вашей службы **[myapp].cloudapp.net** , поэтому при изменении IP-адреса облачной службы не нужно предпринимать никаких действий.</span><span class="sxs-lookup"><span data-stu-id="4dc67-125">The CNAME entry will resolve to the IP address of your **[myapp].cloudapp.net** service automatically, so if the IP address of the cloud service changes, you do not have to take any action.</span></span>

> [!NOTE]
> <span data-ttu-id="4dc67-126">Некоторые регистраторы доменов позволяют сопоставлять дочерние домены только при использовании записи CNAME, например www.contoso.com, а не корневых имен, таких как contoso.com. Дополнительные сведения о записи CNAME см. в документации вашего регистратора, [статье в Википедии о записи CNAME](http://en.wikipedia.org/wiki/CNAME_record) или в документе [Доменные имена IETF — реализация и спецификация](http://tools.ietf.org/html/rfc1035).</span><span class="sxs-lookup"><span data-stu-id="4dc67-126">Some domain registrars only allow you to map subdomains when using a CNAME record, such as www.contoso.com, and not root names, such as contoso.com. For more information on CNAME records, see the documentation provided by your registrar, [the Wikipedia entry on CNAME record](http://en.wikipedia.org/wiki/CNAME_record), or the [IETF Domain Names - Implementation and Specification](http://tools.ietf.org/html/rfc1035) document.</span></span>
> 
> 

### <a name="a-record"></a><span data-ttu-id="4dc67-127">Запись А</span><span class="sxs-lookup"><span data-stu-id="4dc67-127">A record</span></span>
<span data-ttu-id="4dc67-128">Запись *A* сопоставляет домен, например **contoso.com** или **www.contoso.com**, или *домен с подстановочными знаками*, такой как **\*.contoso.com**, с IP-адресом.</span><span class="sxs-lookup"><span data-stu-id="4dc67-128">An *A* record maps a domain, such as **contoso.com** or **www.contoso.com**, *or a wildcard domain* such as **\*.contoso.com**, to an IP address.</span></span> <span data-ttu-id="4dc67-129">В случае облачной службы Azure — виртуальный IP-адрес службы.</span><span class="sxs-lookup"><span data-stu-id="4dc67-129">In the case of an Azure Cloud Service, the virtual IP of the service.</span></span> <span data-ttu-id="4dc67-130">Так что основным преимуществом записи А перед записью CNAME является то, что у вас может быть одна запись, использующая подстановочные знаки, например \***.contoso.com**, которая будет обрабатывать запросы для нескольких дочерних доменов, например **mail.contoso.com**, **login.contoso.com** или **www.contso.com**.</span><span class="sxs-lookup"><span data-stu-id="4dc67-130">So the main benefit of an A record over a CNAME record is that you can have one entry that uses a wildcard, such as \***.contoso.com**, which would handle requests for multiple sub-domains such as **mail.contoso.com**, **login.contoso.com**, or **www.contso.com**.</span></span>

> [!NOTE]
> <span data-ttu-id="4dc67-131">Так как запись А сопоставляется со статическим IP-адресом, она не может автоматически разрешаться в IP-адрес вашей облачной службы.</span><span class="sxs-lookup"><span data-stu-id="4dc67-131">Since an A record is mapped to a static IP address, it cannot automatically resolve changes to the IP address of your Cloud Service.</span></span> <span data-ttu-id="4dc67-132">IP-адрес, используемый службой облака, выделяется при первом развертывании в пустую область (производственном или промежуточном). При удалении развертывания для слота Azure освобождает IP-адрес, и все будущие развертывания в область могут получить новый IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="4dc67-132">The IP address used by your Cloud Service is allocated the first time you deploy to an empty slot (either production or staging.) If you delete the deployment for the slot, the IP address is released by Azure and any future deployments to the slot may be given a new IP address.</span></span>
> 
> <span data-ttu-id="4dc67-133">Удобно, что IP-адрес данного слота развертывания (производственного или промежуточного) сохраняется при переходе от промежуточного к производственному развертыванию или при выполнении обновления на месте существующего развертывания.</span><span class="sxs-lookup"><span data-stu-id="4dc67-133">Conveniently, the IP address of a given deployment slot (production or staging) is persisted when swapping between staging and production deployments or performing an in-place upgrade of an existing deployment.</span></span> <span data-ttu-id="4dc67-134">Дополнительные сведения о том, как производить эти действия, см. в статье [Управление облачными службами](cloud-services-how-to-manage.md).</span><span class="sxs-lookup"><span data-stu-id="4dc67-134">For more information on performing these actions, see [How to manage cloud services](cloud-services-how-to-manage.md).</span></span>
> 
> 

## <a name="add-a-cname-record-for-your-custom-domain"></a><span data-ttu-id="4dc67-135">Добавление записи CNAME для пользовательского домена</span><span class="sxs-lookup"><span data-stu-id="4dc67-135">Add a CNAME record for your custom domain</span></span>
<span data-ttu-id="4dc67-136">Чтобы создать запись CNAME, необходимо с помощью средств, предоставляемых вашим регистратором, добавить в таблице DNS новую запись для пользовательского домена.</span><span class="sxs-lookup"><span data-stu-id="4dc67-136">To create a CNAME record, you must add a new entry in the DNS table for your custom domain by using the tools provided by your registrar.</span></span> <span data-ttu-id="4dc67-137">Каждый регистратор имеет похожий, но немного отличный способ указания записи CNAME, хотя используется одна и та же концепция.</span><span class="sxs-lookup"><span data-stu-id="4dc67-137">Each registrar has a similar but slightly different method of specifying a CNAME record, but the concepts are the same.</span></span>

1. <span data-ttu-id="4dc67-138">Чтобы найти доменное имя **.cloudapp.net** , назначенное для вашей облачной службы, используйте один из этих методов.</span><span class="sxs-lookup"><span data-stu-id="4dc67-138">Use one of these methods to find the **.cloudapp.net** domain name assigned to your cloud service.</span></span>
   
   * <span data-ttu-id="4dc67-139">Войдите на [портал Azure], выберите облачную службу и найдите **URL-адрес сайта** в разделе **Основное**.</span><span class="sxs-lookup"><span data-stu-id="4dc67-139">Login to the [Azure portal], select your cloud service, look at the **Essentials** section and then find the **Site URL** entry.</span></span>
     
       ![Раздел краткого описания, в котором отображается URL-адрес][csurl]
     
       <span data-ttu-id="4dc67-141">**OR**</span><span class="sxs-lookup"><span data-stu-id="4dc67-141">**OR**</span></span>
   * <span data-ttu-id="4dc67-142">Установите и настройте [Azure Powershell](/powershell/azure/overview), а затем используйте следующую команду:</span><span class="sxs-lookup"><span data-stu-id="4dc67-142">Install and configure [Azure Powershell](/powershell/azure/overview), and then use the following command:</span></span>
     
       ```powershell
       Get-AzureDeployment -ServiceName yourservicename | Select Url
       ```
     
     <span data-ttu-id="4dc67-143">Сохраните имя домена, используемое в URL-адресе, возвращаемом любым методом, так как он понадобится при создании записи CNAME.</span><span class="sxs-lookup"><span data-stu-id="4dc67-143">Save the domain name used in the URL returned by either method, as you will need it when creating a CNAME record.</span></span>
2. <span data-ttu-id="4dc67-144">Войдите на веб-сайт своего регистратора DNS и перейдите на страницу управления DNS.</span><span class="sxs-lookup"><span data-stu-id="4dc67-144">Log on to your DNS registrar's website and go to the page for managing DNS.</span></span> <span data-ttu-id="4dc67-145">Найдите ссылки или области сайта, обозначенные как **Имя домена**, **DNS** или **Управление сервером доменных имен**.</span><span class="sxs-lookup"><span data-stu-id="4dc67-145">Look for links or areas of the site labeled as **Domain Name**, **DNS**, or **Name Server Management**.</span></span>
3. <span data-ttu-id="4dc67-146">Теперь найдите место, где можно выбрать или ввести CNAME.</span><span class="sxs-lookup"><span data-stu-id="4dc67-146">Now find where you can select or enter CNAME's.</span></span> <span data-ttu-id="4dc67-147">Может потребоваться выбрать тип записи из раскрывающегося списка или перейти на страницу дополнительных параметров.</span><span class="sxs-lookup"><span data-stu-id="4dc67-147">You may have to select the record type from a drop down, or go to an advanced settings page.</span></span> <span data-ttu-id="4dc67-148">Ищите слова **CNAME**, **Псевдоним** или **Поддомены**.</span><span class="sxs-lookup"><span data-stu-id="4dc67-148">You should look for the words **CNAME**, **Alias**, or **Subdomains**.</span></span>
4. <span data-ttu-id="4dc67-149">Необходимо также указать псевдоним домена или поддомена для CNAME, такой как **www**, если вы хотите создать псевдоним для **www.customdomain.com**. Если вы хотите создать псевдоним для корневого домена, он может быть указан как символ**@**в инструментах DNS вашего регистратора.</span><span class="sxs-lookup"><span data-stu-id="4dc67-149">You must also provide the domain or subdomain alias for the CNAME, such as **www** if you want to create an alias for **www.customdomain.com**. If you want to create an alias for the root domain, it may be listed as the '**@**' symbol in your registrar's DNS tools.</span></span>
5. <span data-ttu-id="4dc67-150">Затем необходимо предоставить каноническое имя узла, которым в данном случае является домен **cloudapp.net** вашего приложения.</span><span class="sxs-lookup"><span data-stu-id="4dc67-150">Then, you must provide a canonical host name, which is your application's **cloudapp.net** domain in this case.</span></span>

<span data-ttu-id="4dc67-151">Например, следующая запись CNAME перенаправляет весь трафик из **www.contoso.com** в **contoso.cloudapp.net**, пользовательское доменное имя вашего развернутого приложения.</span><span class="sxs-lookup"><span data-stu-id="4dc67-151">For example, the following CNAME record forwards all traffic from **www.contoso.com** to **contoso.cloudapp.net**, the custom domain name of your deployed application:</span></span>

| <span data-ttu-id="4dc67-152">Псевдоним/Имя узла/Поддомен</span><span class="sxs-lookup"><span data-stu-id="4dc67-152">Alias/Host name/Subdomain</span></span> | <span data-ttu-id="4dc67-153">Канонический домен</span><span class="sxs-lookup"><span data-stu-id="4dc67-153">Canonical domain</span></span> |
| --- | --- |
| <span data-ttu-id="4dc67-154">www</span><span class="sxs-lookup"><span data-stu-id="4dc67-154">www</span></span> |<span data-ttu-id="4dc67-155">contoso.cloudapp.net</span><span class="sxs-lookup"><span data-stu-id="4dc67-155">contoso.cloudapp.net</span></span> |

> [!NOTE]
> <span data-ttu-id="4dc67-156">Посетитель сайта **www.contoso.com** никогда не увидит настоящий узел (contoso.cloudapp.net), поэтому процесс перенаправления невидим для конечного пользователя.</span><span class="sxs-lookup"><span data-stu-id="4dc67-156">A visitor of **www.contoso.com** will never see the true host (contoso.cloudapp.net), so the forwarding process is invisible to the end user.</span></span>
> 
> <span data-ttu-id="4dc67-157">Приведенный выше пример применим только к трафику поддомена **www** .</span><span class="sxs-lookup"><span data-stu-id="4dc67-157">The example above only applies to traffic at the **www** subdomain.</span></span> <span data-ttu-id="4dc67-158">Поскольку с записями CNAME нельзя использовать подстановочные знаки, необходимо создать один CNAME для каждого домена или поддомена.</span><span class="sxs-lookup"><span data-stu-id="4dc67-158">Since you cannot use wildcards with CNAME records, you must create one CNAME for each domain/subdomain.</span></span> <span data-ttu-id="4dc67-159">Если вы хотите направить трафик из поддоменов, таких как *.contoso.com, на адрес cloudapp.net, можно настроить элемент **URL-адрес перенаправления** или **URL-адрес переадресации** в параметрах DNS или создать запись A.</span><span class="sxs-lookup"><span data-stu-id="4dc67-159">If you want to direct  traffic from subdomains, such as *.contoso.com, to your cloudapp.net address, you can configure a **URL Redirect** or **URL Forward** entry in your DNS settings, or create an A record.</span></span>
> 
> 

## <a name="add-an-a-record-for-your-custom-domain"></a><span data-ttu-id="4dc67-160">Добавление записи A для пользовательского домена</span><span class="sxs-lookup"><span data-stu-id="4dc67-160">Add an A record for your custom domain</span></span>
<span data-ttu-id="4dc67-161">Чтобы создать запись А, сначала необходимо найти виртуальный IP-адрес облачной службы.</span><span class="sxs-lookup"><span data-stu-id="4dc67-161">To create an A record, you must first find the virtual IP address of your cloud service.</span></span> <span data-ttu-id="4dc67-162">Затем необходимо с помощью средств, предоставляемых вашим регистратором, добавить в таблице DNS новую запись для пользовательского домена.</span><span class="sxs-lookup"><span data-stu-id="4dc67-162">Then add a new entry in the DNS table for your custom domain by using the tools provided by your registrar.</span></span> <span data-ttu-id="4dc67-163">Каждый регистратор имеет похожий, но немного отличный способ указания записи А, хотя используется одна и та же концепция.</span><span class="sxs-lookup"><span data-stu-id="4dc67-163">Each registrar has a similar but slightly different method of specifying an A record, but the concepts are the same.</span></span>

1. <span data-ttu-id="4dc67-164">Чтобы получить IP-адрес для своей облачной службы, используйте один из следующих способов.</span><span class="sxs-lookup"><span data-stu-id="4dc67-164">Use one of the following methods to get the IP address of your cloud service.</span></span>
   
   * <span data-ttu-id="4dc67-165">Войдите на [портал Azure], выберите облачную службу и найдите **Общедоступные IP-адреса** в разделе **Основное**.</span><span class="sxs-lookup"><span data-stu-id="4dc67-165">Login to the [Azure portal], select your cloud service, look at the **Essentials** section and then find the **Public IP addresses** entry.</span></span>
     
       ![Раздел краткого описания, в котором отображается VIP-адрес][vip]
     
       <span data-ttu-id="4dc67-167">**OR**</span><span class="sxs-lookup"><span data-stu-id="4dc67-167">**OR**</span></span>
   * <span data-ttu-id="4dc67-168">Установите и настройте [Azure Powershell](/powershell/azure/overview), а затем используйте следующую команду:</span><span class="sxs-lookup"><span data-stu-id="4dc67-168">Install and configure [Azure Powershell](/powershell/azure/overview), and then use the following command:</span></span>
     
       ```powershell
       get-azurevm -servicename yourservicename | get-azureendpoint -VM {$_.VM} | select Vip
       ```
     
     <span data-ttu-id="4dc67-169">Сохраните IP-адрес, поскольку он понадобится при создании записи А.</span><span class="sxs-lookup"><span data-stu-id="4dc67-169">Save the IP address, as you will need it when creating an A record.</span></span>
2. <span data-ttu-id="4dc67-170">Войдите на веб-сайт своего регистратора DNS и перейдите на страницу управления DNS.</span><span class="sxs-lookup"><span data-stu-id="4dc67-170">Log on to your DNS registrar's website and go to the page for managing DNS.</span></span> <span data-ttu-id="4dc67-171">Найдите ссылки или области сайта, обозначенные как **Имя домена**, **DNS** или **Управление сервером доменных имен**.</span><span class="sxs-lookup"><span data-stu-id="4dc67-171">Look for links or areas of the site labeled as **Domain Name**, **DNS**, or **Name Server Management**.</span></span>
3. <span data-ttu-id="4dc67-172">Теперь найдите место, где можно выбрать или ввести запись А.</span><span class="sxs-lookup"><span data-stu-id="4dc67-172">Now find where you can select or enter A record's.</span></span> <span data-ttu-id="4dc67-173">Может потребоваться выбрать тип записи из раскрывающегося списка или перейти на страницу дополнительных параметров.</span><span class="sxs-lookup"><span data-stu-id="4dc67-173">You may have to select the record type from a drop down, or go to an advanced settings page.</span></span>
4. <span data-ttu-id="4dc67-174">Выберите или введите домен или дочерний домен, который будет использовать эту запись А.</span><span class="sxs-lookup"><span data-stu-id="4dc67-174">Select or enter the domain or subdomain that will use this A record.</span></span> <span data-ttu-id="4dc67-175">Например, выберите **www**, если вы хотите создать псевдоним для **www.customdomain.com**. Если вы хотите создать запись с подстановочными знаками для всех поддоменов, введите "*****".</span><span class="sxs-lookup"><span data-stu-id="4dc67-175">For example, select **www** if you want to create an alias for **www.customdomain.com**. If you want to create a wildcard entry for all subdomains, enter '*****'.</span></span> <span data-ttu-id="4dc67-176">Так будут охвачены все поддомены, такие как **mail.customdomain.com**, **login.customdomain.com** и **www.customdomain.com**.</span><span class="sxs-lookup"><span data-stu-id="4dc67-176">This will cover all sub-domains such as **mail.customdomain.com**, **login.customdomain.com**, and **www.customdomain.com**.</span></span>
   
    <span data-ttu-id="4dc67-177">Если вы хотите создать запись A для корневого домена, она может быть указана как символ**@**в инструментах DNS вашего регистратора.</span><span class="sxs-lookup"><span data-stu-id="4dc67-177">If you want to create an A record for the root domain, it may be listed as the '**@**' symbol in your registrar's DNS tools.</span></span>
5. <span data-ttu-id="4dc67-178">Введите IP-адрес вашей облачной службы в предоставленном поле.</span><span class="sxs-lookup"><span data-stu-id="4dc67-178">Enter the IP address of your cloud service in the provided field.</span></span> <span data-ttu-id="4dc67-179">Это связывает запись домена, используемую в записи А, с IP-адресом развертывания облачной службы.</span><span class="sxs-lookup"><span data-stu-id="4dc67-179">This associates the domain entry used in the A record with the IP address of your cloud service deployment.</span></span>

<span data-ttu-id="4dc67-180">Например, следующая запись A перенаправляет весь трафик из **contoso.com** на **137.135.70.239**, IP-адрес развертываемого приложения:</span><span class="sxs-lookup"><span data-stu-id="4dc67-180">For example, the following A record forwards all traffic from **contoso.com** to **137.135.70.239**, the IP address of your deployed application:</span></span>

| <span data-ttu-id="4dc67-181">Имя узла/Поддомен</span><span class="sxs-lookup"><span data-stu-id="4dc67-181">Host name/Subdomain</span></span> | <span data-ttu-id="4dc67-182">IP-адрес</span><span class="sxs-lookup"><span data-stu-id="4dc67-182">IP address</span></span> |
| --- | --- |
| @ |<span data-ttu-id="4dc67-183">137.135.70.239</span><span class="sxs-lookup"><span data-stu-id="4dc67-183">137.135.70.239</span></span> |

<span data-ttu-id="4dc67-184">В этом примере показано создание записи А для корневого домена.</span><span class="sxs-lookup"><span data-stu-id="4dc67-184">This example demonstrates creating an A record for the root domain.</span></span> <span data-ttu-id="4dc67-185">Если вы хотите создать запись с подстановочными знаками, чтобы охватить все поддомены, введите "*****" в качестве поддомена.</span><span class="sxs-lookup"><span data-stu-id="4dc67-185">If you wish to create a wildcard entry to cover all subdomains, you would enter '*****' as the subdomain.</span></span>

> [!WARNING]
> <span data-ttu-id="4dc67-186">IP-адреса в Azure по умолчанию являются динамическими.</span><span class="sxs-lookup"><span data-stu-id="4dc67-186">IP addresses in Azure are dynamic by default.</span></span> <span data-ttu-id="4dc67-187">Чтобы ваш IP-адрес не изменялся, вы можете использовать [зарезервированный IP-адрес](../virtual-network/virtual-networks-reserved-public-ip.md) .</span><span class="sxs-lookup"><span data-stu-id="4dc67-187">You will probably want to use a [reserved IP address](../virtual-network/virtual-networks-reserved-public-ip.md) to ensure that your IP address does not change.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="4dc67-188">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="4dc67-188">Next steps</span></span>
* [<span data-ttu-id="4dc67-189">Управление облачными службами</span><span class="sxs-lookup"><span data-stu-id="4dc67-189">How to Manage Cloud Services</span></span>](cloud-services-how-to-manage.md)
* [<span data-ttu-id="4dc67-190">Сопоставление содержимого CDN с пользовательским доменом</span><span class="sxs-lookup"><span data-stu-id="4dc67-190">How to Map CDN Content to a Custom Domain</span></span>](../cdn/cdn-map-content-to-custom-domain.md)
* <span data-ttu-id="4dc67-191">[Общая настройка облачной службы](cloud-services-how-to-configure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="4dc67-191">[General configuration of your cloud service](cloud-services-how-to-configure-portal.md).</span></span>
* <span data-ttu-id="4dc67-192">Узнайте, как [развернуть облачную службу](cloud-services-how-to-create-deploy-portal.md).</span><span class="sxs-lookup"><span data-stu-id="4dc67-192">Learn how to [deploy a cloud service](cloud-services-how-to-create-deploy-portal.md).</span></span>
* <span data-ttu-id="4dc67-193">Настройка [SSL-сертификатов](cloud-services-configure-ssl-certificate-portal.md).</span><span class="sxs-lookup"><span data-stu-id="4dc67-193">Configure [ssl certificates](cloud-services-configure-ssl-certificate-portal.md).</span></span>

[Expose Your Application on a Custom Domain]: #access-app
[Add a CNAME Record for Your Custom Domain]: #add-cname
[Expose Your Data on a Custom Domain]: #access-data
[VIP swaps]: cloud-services-how-to-manage-portal.md#how-to-swap-deployments-to-promote-a-staged-deployment-to-production
[Create a CNAME record that associates the subdomain with the storage account]: #create-cname
[портал Azure]: https://portal.azure.com
[vip]: ./media/cloud-services-custom-domain-name-portal/csvip.png
[csurl]: ./media/cloud-services-custom-domain-name-portal/csurl.png
